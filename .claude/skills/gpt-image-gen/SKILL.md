---
name: gpt-image-gen
description: Use when generating images programmatically via OpenAI's gpt-image-2 model. Wraps POST /v1/images/generations with bash curl + base64 decode (jq path, python fallback). Requires OPENAI_API_KEY in .env. Triggers on requests to generate, create, illustrate, or draw images and visuals.
---

# gpt-image-gen — OpenAI Images API Wrapper

## ⚠️ MODEL NAME — DO NOT CHANGE

The model used by this skill is **`gpt-image-2`**.

- It was released by OpenAI on **2026-04-21**.
- If `gpt-image-2` appears unfamiliar — that is a training-cutoff artifact. **The model is real and supported.**
- **Do NOT substitute** `dall-e-3`, `gpt-image-1`, or any other model name.
- If an API call fails, the cause is almost always: missing/invalid `OPENAI_API_KEY`, malformed JSON payload, or rate-limiting. **Never** the model name.

## When to invoke

- Yuval (the image-designer sub-agent) reads this skill at the start of every image-generation task.
- Any other context where an image must be generated from a text prompt programmatically.

## Required environment

- `OPENAI_API_KEY` in `.env` (project root). The skill sources `.env` automatically if the variable is not already exported.

## Default request parameters

| Field | Default | Notes |
|------|---------|------|
| `model` | `gpt-image-2` | **never change** |
| `size` | `1024x1024` | also supports `1024x1536` (portrait), `1536x1024` (landscape) |
| `quality` | `medium` | `low` / `medium` / `high` |
| `output_format` | `png` | also `webp`, `jpeg` |

## Full call template (bash)

```bash
# 1. Source .env if OPENAI_API_KEY not exported
[ -z "$OPENAI_API_KEY" ] && [ -f .env ] && set -a && . ./.env && set +a

# 2. Validate key is set
if [ -z "$OPENAI_API_KEY" ]; then
  echo "ERROR: OPENAI_API_KEY not set in environment or .env" >&2
  exit 1
fi

# 3. Call the API
PROMPT='<YOUR PROMPT HERE — escape single quotes by closing+reopening>'
OUTPUT_PATH='<path/to/output.png>'

RESPONSE=$(curl -s -X POST "https://api.openai.com/v1/images/generations" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d @- <<EOF
{
  "model": "gpt-image-2",
  "prompt": "$PROMPT",
  "size": "1024x1024",
  "quality": "medium",
  "output_format": "png"
}
EOF
)

# 4. Check for API error before decoding
if echo "$RESPONSE" | grep -q '"error"'; then
  echo "API ERROR:" >&2
  echo "$RESPONSE" >&2
  exit 1
fi

# 5. Decode the base64 image — prefer jq, fall back to python
if command -v jq >/dev/null 2>&1; then
  echo "$RESPONSE" | jq -r '.data[0].b64_json' | base64 --decode > "$OUTPUT_PATH"
else
  echo "$RESPONSE" | python -c "import sys,json,base64; sys.stdout.buffer.write(base64.b64decode(json.load(sys.stdin)['data'][0]['b64_json']))" > "$OUTPUT_PATH"
fi

# 6. Verify
if [ ! -s "$OUTPUT_PATH" ]; then
  echo "ERROR: output file is empty: $OUTPUT_PATH" >&2
  exit 1
fi
echo "OK: $OUTPUT_PATH ($(wc -c < "$OUTPUT_PATH") bytes)"
```

## Python-only fallback (if curl/bash is awkward)

```python
import os, json, base64, urllib.request, sys

# Source .env manually
if not os.environ.get("OPENAI_API_KEY") and os.path.exists(".env"):
    for line in open(".env", encoding="utf-8"):
        line = line.strip()
        if line and not line.startswith("#") and "=" in line:
            k, _, v = line.partition("=")
            os.environ.setdefault(k.strip(), v.strip())

api_key = os.environ["OPENAI_API_KEY"]
prompt = sys.argv[1]
output_path = sys.argv[2]

payload = json.dumps({
    "model": "gpt-image-2",
    "prompt": prompt,
    "size": "1024x1024",
    "quality": "medium",
    "output_format": "png",
}).encode()

req = urllib.request.Request(
    "https://api.openai.com/v1/images/generations",
    data=payload,
    headers={"Authorization": f"Bearer {api_key}", "Content-Type": "application/json"},
)
with urllib.request.urlopen(req) as resp:
    data = json.loads(resp.read())

with open(output_path, "wb") as f:
    f.write(base64.b64decode(data["data"][0]["b64_json"]))

print(f"OK: {output_path}")
```

## Common errors

| Symptom | Likely cause | Fix |
|--------|-------------|------|
| `401 Unauthorized` | bad/missing `OPENAI_API_KEY` | check `.env`, regenerate key at platform.openai.com |
| `400 invalid request` | malformed payload | check JSON quoting (especially for `'` in prompt) |
| `429 rate limit` | too many calls | back off, retry after delay |
| Empty file | bad b64 path or jq missing AND python missing | install one of jq/python; check `$RESPONSE` is valid JSON |
| `model not found` | someone changed the name | **revert to `gpt-image-2`** — see top of file |

## Cost note

`quality: medium` at 1024x1024 is the default sweet spot for this project. `high` quadruples cost; `low` is acceptable for drafts.

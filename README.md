# Cloud-Init Templates

Example cloud-init templates for HotManager VM provisioning.

## vllm-docker.yaml

Starts vLLM Docker container with GPU acceleration on first boot.

## API Usage

### Environment Variables

```bash
export API_TOKEN="your-api-token-here"
export API_BASE="https://admin.hotaisle.app/api"
export TEAM_SLUG="your-team"
```

### Example API Call

```bash
curl -X 'POST' \
  "${API_BASE}/teams/${TEAM_SLUG}/virtual_machines/" \
  -H 'accept: application/json' \
  -H "Authorization: Token ${API_TOKEN}" \
  -H 'Content-Type: application/json' \
  -d '{
    "gpus": [
      {
        "count": 1,
        "manufacturer": "AMD",
        "model": "MI300X"
      }
    ],
    "user_data_url": "https://raw.githubusercontent.com/hotaisle/cloud-init-templates/master/vllm-docker.yaml"
  }'
```

## Accessing vLLM

```bash
# SSH to VM
ssh hotaisle@<vm-ip>

# Test vLLM API from inside VM
curl http://localhost:8000/v1/completions \
  -H "Content-Type: application/json" \
  -d '{
    "model": "Qwen/Qwen2-7B-Instruct",
    "prompt": "Write a haiku about artificial intelligence",
    "max_tokens": 128,
    "top_p": 0.95,
    "top_k": 20,
    "description": "Test vLLM API call"
  }'
```

## Creating Your Own Cloud-Init Files

All you need is a URL to a cloud-init user-data file. Here are some options for hosting your files:

### Fork This Repository

Fork the repository to create your own templates or edit the existing templates.

### GitHub Gist

Create GitHub gists with your cloud-init content. Gists are perfect for quick sharing and provide version control automatically.

## Cloud-Init Reference

For complete cloud-init documentation and reference:
<https://cloudinit.readthedocs.io/en/latest/reference/index.html>

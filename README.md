# DeepCode Playground

このリポジトリは、DeepCodeを試しに動かしてみるためのリポジトリです。

```bash
# 🚀 Install DeepCode package directly
pip install deepcode-hku

# 🔑 Download configuration files
curl -O https://raw.githubusercontent.com/HKUDS/DeepCode/main/mcp_agent.config.yaml
curl -O https://raw.githubusercontent.com/HKUDS/DeepCode/main/mcp_agent.secrets.yaml

# 🔑 Configure API keys (required)
# Edit mcp_agent.secrets.yaml with your API keys and base_url:
# - openai: api_key, base_url (for OpenAI/custom endpoints)
# - anthropic: api_key (for Claude models)
# - google: api_key (for Gemini models)

# 🤖 Select your preferred LLM provider (optional)
# Edit mcp_agent.config.yaml to choose your LLM (line ~106):
# - llm_provider: "google"    # Use Google Gemini models
# - llm_provider: "anthropic" # Use Anthropic Claude models
# - llm_provider: "openai"    # Use OpenAI/compatible models
# Note: If not set or unavailable, will automatically fallback to first available provider

# 🔑 Configure search API keys for web search (optional)
# Edit mcp_agent.config.yaml to set your API keys:
# - For Brave Search: Set BRAVE_API_KEY: "your_key_here" in brave.env section (line ~28)
# - For Bocha-MCP: Set BOCHA_API_KEY: "your_key_here" in bocha-mcp.env section (line ~74)

# 📄 Configure document segmentation (optional)
# Edit mcp_agent.config.yaml to control document processing:
# - enabled: true/false (whether to use intelligent document segmentation)
# - size_threshold_chars: 50000 (document size threshold to trigger segmentation)
```

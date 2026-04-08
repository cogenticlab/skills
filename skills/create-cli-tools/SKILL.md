---
name: create-cli-tools
description: Create tools from a cli command usage help
metadata:
  openclaw:
    requires:
      bins:
        - curl
      config:
        - ~/.cogenticlab/credentials.md
---

# Create CLI Tools
## CLI Tool Format
```json
{
  "cli": "cli_command",
"tools":[{
  "name": "command_name",
  "command": "raw_command_in_cli_usage_help",
  "description": "command_description",
  "usage": "raw_command_usage"
}
]}
```
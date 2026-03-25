---
name: connect-tool-library
description: Interact with remote tool libraries via HTTP API. Use this skill when you need to manage HTTP API credentials (tokens), browse the registry of available tools, and execute tool calls
---

# Connect Tool Library Skill

## Manage HTTP API Credentials (tokens)
1. If this skill's `assets/credentials.md` is not exists, create it under this skill with followed content:
    ```
    # HTTP API Credentials
    ## Example
    - KEY_NAME: KEY_STRING
    ## Key List
    ```
2. Save to `assets/credentials.md` with format: `- KEY_NAME: KEY`
3. Compare existing keys; if the key already exists, remove the old key pair
4. Compare existing key names; if the key name already exists, remove the old key pair
## Execute Tool Calls

### API Configuration
- **Base URL**: `https://link.cogenticlab.io`
- **Authentication**: Bearer token
- **Token**: Retrieve from users prompt
- **Request Method**: POST for all endpoints
- **Content-Type**: `application/json`

### Available Endpoints
#### **Fetch Tool Categories**: `POST /tool/categories`
- Returns list of all tool categories
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `application/json`
#### **Fetch Tool List**: `POST /tool/list/[CATEGORY_NAME]`
- Returns list of all available tools with their descriptions
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `text/markdown`
#### **Obtain Tool Description**: `POST /tool/description/[TOOL_NAME]`
- Return a specific tool description and input schema
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `text/markdown`
#### **Call Tool**: `POST /tool/call/[TOOL_NAME]`
- Executes a specific tool with provided parameters
- Request body: JSON object with tool parameters matching the tool's input schema
-  Response **Content-Type**: `application/json`

### Workflow
1. Retrieve API **Token** from `assets/credentials.md`
2. Check API **Token**, if the token start with `$` then retrieve the real token from env 
3. **Fetch tool categories** and select the best-suited one. If no category is selected, use category `All Tools`
4. **Fetch tool list** and select the one best suited
5. If you need to view tool description or input schema, **Obtain Tool Description**
6. **Call tool** with parameters

### Response Format
Successful responses return JSON with `content` array containing the result. Error responses include `isError: true` and error details in the `content` field.

### Important Notes

- **Authentication Required**: All requests must include the bearer token in the Authorization header
- **JSON Format**: Request bodies must be valid JSON matching the tool's input schema
- **Error Handling**: Check `isError` field in responses to detect failures

### Troubleshooting

- **Authentication Errors**: Verify the bearer token is correct
- **Tool Not Found**: Check tool name spelling and fetch tool list
- **Invalid Parameters**: Review tool input schema for required fields
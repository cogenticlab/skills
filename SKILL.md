---
name: cogenticlab-tool-hub
description: Skill to interact with remote MCP tools via HTTP API. Use this skill when you need to manage HTTP API credentials (base URL and tokens), browse the registry of available tools, and execute tool calls.
---

# CongenticLab Tool Hub Skill - Remote MCP Tools API Integration

This skill enables interaction with remote MCP tools through HTTP API endpoints.

## Manage HTTP API Credentials (base URL and tokens)
save to `assets/credentials.md`

## Execute Tool Calls

### API Configuration
- **Base URL**: `http://192.168.1.7:8088`
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
- Return a specific tool description
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `text/markdown`
#### **Obtain Tool Input Schema**: `POST /tool/inputschema/[TOOL_NAME]`
- Return a specific tool input schema
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `application/json`
#### **Call Tool**: `POST /tool/call/[TOOL_NAME]`
- Executes a specific tool with provided parameters
- Request body: JSON object with tool parameters matching the tool's input schema
-  Response **Content-Type**: `application/json`

### Workflow
1. Retrieve API **Token** from `assets/credentials.md`
2. **Fetch tool categories** and select the best-suited one. If no category is selected, use category `All Tools`
3. **Fetch tool list** and select the one best suited
4. If you need to view tool description, **Obtain Tool Description**
5. Before preparing parameters, your must **Obtain Tool Input Schema**
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
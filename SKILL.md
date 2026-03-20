---
name: cogenticlab-tool-hub
description: Skill to interact with remote MCP tools via HTTP API. Use this skill when you need to list available tools or call tools.
---

# CongenticLab Tool Hub Skill - Remote MCP Tools API Integration

This skill enables interaction with remote MCP tools through HTTP API endpoints.

## API Configuration
- **Base URL**: Retrieve from users prompt
- **Authentication**: Bearer token
- **Token**: Retrieve from users prompt
- **Request Method**: POST for all endpoints
- **Content-Type**: `application/json`

## Available Endpoints
### **Fetch Tool Categories**: `POST /tool/categories`
- Returns list of all tool categories
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `application/json`
### **Fetch Tool List**: `POST /tool/list/[CATEGORY_NAME]`
- Returns list of all available tools with their descriptions
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `text/markdown`
### **Obtain Tool Input Schema**: `POST /tool/inputschema/[TOOL_NAME]`
- Return a specific tool input schema
- No request body required (send empty JSON `{}`)
- Response **Content-Type**: `application/json`
### **Call Tool**: `POST /tool/call/[TOOL_NAME]`
- Executes a specific tool with provided parameters
- Request body: JSON object with tool parameters matching the tool's input schema
-  Response **Content-Type**: `application/json`

## Workflow
1. Retrieve API **Base URL** and **Token** from the .env file in workspace. If the Token is unset, retrieve it from the system environment
2. **Fetch tool categories** and select the one best suited. if no category selected, use category `All Tools`
3. **Fetch tool list** and select the one best suited
4. Before preparing parameters, your must **Obtain Tool Input Schema**
5. **Call tool** with parameters

## Response Format
Successful responses return JSON with `content` array containing the result. Error responses include `isError: true` and error details in the `content` field.

## Important Notes

1. **Authentication Required**: All requests must include the bearer token in the Authorization header
2. **JSON Format**: Request bodies must be valid JSON matching the tool's input schema
3. **Error Handling**: Check `isError` field in responses to detect failures

## Troubleshooting

1. **Authentication Errors**: Verify the bearer token is correct
2. **Tool Not Found**: Check tool name spelling and fetch tool list
3. **Invalid Parameters**: Review tool input schema for required fields
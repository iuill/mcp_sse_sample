# MCP SSE Sample

SSEを使用したMCPサーバーのサンプルです。
MCPプロトコルのSSE実装を示すサンプルプロジェクトです。

オリジナルは以下コードです。
- https://github.com/modelcontextprotocol/servers/tree/main/src/everything

## Components

### Tools

1. `echo`
   - Simple tool to echo back input messages
   - Input:
     - `message` (string): Message to echo back
   - Returns: Text content with echoed message

2. `add`
   - Adds two numbers together
   - Inputs:
     - `a` (number): First number
     - `b` (number): Second number
   - Returns: Text result of the addition

3. `longRunningOperation`
   - Demonstrates progress notifications for long operations
   - Inputs:
     - `duration` (number, default: 10): Duration in seconds
     - `steps` (number, default: 5): Number of progress steps
   - Returns: Completion message with duration and steps
   - Sends progress notifications during execution

4. `sampleLLM`
   - Demonstrates LLM sampling capability using MCP sampling feature
   - Inputs:
     - `prompt` (string): The prompt to send to the LLM
     - `maxTokens` (number, default: 100): Maximum tokens to generate
   - Returns: Generated LLM response

5. `getTinyImage`
   - Returns a small test image
   - No inputs required
   - Returns: Base64 encoded PNG image data

6. `printEnv`
   - Prints all environment variables
   - Useful for debugging MCP server configuration
   - No inputs required
   - Returns: JSON string of all environment variables

7. `annotatedMessage`
   - Demonstrates how annotations can be used to provide metadata about content
   - Inputs:
     - `messageType` (enum: "error" | "success" | "debug"): Type of message to demonstrate different annotation patterns
     - `includeImage` (boolean, default: false): Whether to include an example image
   - Returns: Content with varying annotations:
     - Error messages: High priority (1.0), visible to both user and assistant
     - Success messages: Medium priority (0.7), user-focused
     - Debug messages: Low priority (0.3), assistant-focused
     - Optional image: Medium priority (0.5), user-focused
   - Example annotations:
     ```json
     {
       "priority": 1.0,
       "audience": ["user", "assistant"]
     }
     ```

### Logging

The server sends random-leveled log messages every 15 seconds, e.g.:

```json
{
  "method": "notifications/message",
  "params": {
	"level": "info",
	"data": "Info-level message"
  }
}
```

## 使用方法

### ローカルでの実行

```bash
# インストール
npm install

# ビルド
npm run build

# 実行(STDIOモード)
npm run start

# 実行(SSEモード)
npm run start:sse
```

### Claude Desktopでの使用

`claude_desktop_config.json`に以下を追加してください：

```json
{
  "mcpServers": {
    "sse-sample": {
      "command": "npx",
      "args": [
        "-y",
        "mcp_sse_sample"
      ]
    }
  }
}
```

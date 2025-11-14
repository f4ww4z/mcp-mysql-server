# @f4ww4z/mcp-mysql-server
[![Trust Score](https://archestra.ai/mcp-catalog/api/badge/quality/f4ww4z/mcp-mysql-server)](https://archestra.ai/mcp-catalog/f4ww4z__mcp-mysql-server)
[![smithery badge](https://smithery.ai/badge/@f4ww4z/mcp-mysql-server)](https://smithery.ai/server/@f4ww4z/mcp-mysql-server)

A Model Context Protocol server that provides MySQL database operations. This server enables AI models to interact with MySQL databases through a standardized interface.

<a href="https://glama.ai/mcp/servers/qma33al6ie"><img width="380" height="200" src="https://glama.ai/mcp/servers/qma33al6ie/badge" alt="mcp-mysql-server MCP server" /></a>

## Installation

### Installing via Smithery

To install MySQL Server for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@f4ww4z/mcp-mysql-server):

```bash
npx -y @smithery/cli install @f4ww4z/mcp-mysql-server --client claude
```

### Manual Installation
```bash
npx @f4ww4z/mcp-mysql-server
```

## Configuration

The server requires the following environment variables to be set in your MCP settings configuration file:

> recommended use

```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": ["-y", "@f4ww4z/mcp-mysql-server", "mysql://user:password@localhost:port/database"],
    }
  }
}
```

```json
{
  "mcpServers": {
    "mysql": {
      "command": "npx",
      "args": ["-y", "@f4ww4z/mcp-mysql-server"],
      "env": {
        "MYSQL_HOST": "your_host",
        "MYSQL_USER": "your_user",
        "MYSQL_PASSWORD": "your_password",
        "MYSQL_DATABASE": "your_database"
      }
    }
  }
}
```
## codex 

### mac

在 `~/.codex/config.toml`

```toml
[mcp_servers.mcp-mysql-server]
command = "npx"
args = [
  "-y",
  "@f4ww4z/mcp-mysql-server",
  "mysql://user:password@127.0.0.1:3306/database"
]
```

### windows

在 `%USERPROFILE%\.codex\config.toml`

```toml
[mcp_servers.mcp-mysql-server]
command = "npx"
args = [
  "-y",
  "@f4ww4z/mcp-mysql-server",
  "mysql://user:password@127.0.0.1:3306/database"
]
```


## Running evals

The evals package loads an mcp client that then runs the index.ts file, so there is no need to rebuild between tests. You can load environment variables by prefixing the npx command. Full documentation can be found [here](https://www.mcpevals.io/docs).

```bash
OPENAI_API_KEY=your-key  npx mcp-eval src/evals/evals.ts src/index.ts
```
## Available Tools

### 1. connect_db
Establish connection to MySQL database using provided credentials.

```typescript
use_mcp_tool({
  server_name: "mysql",
  tool_name: "connect_db",
  arguments: {
    host: "localhost",
    user: "your_user",
    password: "your_password",
    database: "your_database"
  }
});
```

### 2. query
Execute SELECT queries with optional prepared statement parameters.

```typescript
use_mcp_tool({
  server_name: "mysql",
  tool_name: "query",
  arguments: {
    sql: "SELECT * FROM users WHERE id = ?",
    params: [1]
  }
});
```

### 3. execute
Execute INSERT, UPDATE, or DELETE queries with optional prepared statement parameters.

```typescript
use_mcp_tool({
  server_name: "mysql",
  tool_name: "execute",
  arguments: {
    sql: "INSERT INTO users (name, email) VALUES (?, ?)",
    params: ["John Doe", "john@example.com"]
  }
});
```

### 4. list_tables
List all tables in the connected database.

```typescript
use_mcp_tool({
  server_name: "mysql",
  tool_name: "list_tables",
  arguments: {}
});
```

### 5. describe_table
Get the structure of a specific table.

```typescript
use_mcp_tool({
  server_name: "mysql",
  tool_name: "describe_table",
  arguments: {
    table: "users"
  }
});
```

## Features

- Secure connection handling with automatic cleanup
- Prepared statement support for query parameters
- Comprehensive error handling and validation
- TypeScript support
- Automatic connection management

## Security

- Uses prepared statements to prevent SQL injection
- Supports secure password handling through environment variables
- Validates queries before execution
- Automatically closes connections when done

## Error Handling

The server provides detailed error messages for common issues:
- Connection failures
- Invalid queries
- Missing parameters
- Database errors

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request to https://github.com/f4ww4z/mcp-mysql-server

## License

MIT

# mcp-datetime

[![Python Version](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/downloads/)
[![MCP Version](https://img.shields.io/badge/mcp-1.1.1-green.svg)](https://github.com/anaisbetts/mcp)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

English | [日本語](README.md)

A datetime formatting service implemented as an MCP server for the Claude Desktop Application. Supports generation of datetime strings in various formats.

## Features

- ✨ Support for various datetime formats
- 🇯🇵 Japanese language support
- 📁 Optimized formats for filename generation
- 🌏 Accurate timezone handling
- 🔧 Seamless integration with Claude Desktop App

## MCP Server Components

### Tools

The server implements one tool:

- `get_datetime`: Get current date and time in various formats
  - Takes "format" as a required string argument
  - Returns formatted datetime string based on specified format
  - Supports multiple format types including standard, Japanese, and ISO formats

## Usage with Claude Desktop App

Add the following to your config file:

- Config file location:

  - MacOS: `~/Library/Application Support/Claude/claude_desktop_config.json`
  - Windows: `%APPDATA%/Claude/claude_desktop_config.json`

  ```json
  {
    "mcpServers": {
      "mcp-datetime": {
        "command": "uvx",
        "args": ["mcp-datetime"]
      }
    }
  }
  ```

## About Installation

No installation is required for normal use. You can use this package by simply adding the configuration to your Claude Desktop App config file. The uvx command will automatically download and execute the package as needed.

If you need to install the package directly (e.g., for development or source code inspection), you can use one of these methods:

- Install from PyPI

  ```bash
  pip install mcp-datetime
  ```

- Install from GitHub Source

  ```bash
  git clone https://github.com/ZeparHyfar/mcp-datetime.git
  cd mcp-datetime
  pip install -e .
  ```

- `claude_desktop_config.json` for manual installation

  ```json
  {
    "mcpServers": {
      "mcp-datetime": {
        "command": "python",
        "args": ["-m", "mcp_datetime"],
        "env": {
          "PYTHON": "/path/to/your/python"
        }
      }
    }
  }
  ```

  - Replace "/path/to/your/python" with your actual Python interpreter path.

  - Examples:
    - MacOS: "/usr/local/bin/python3" or "/Users/username/.pyenv/versions/3.12.0/bin/python3"
    - Windows: "C:\Python312\python.exe"

## Basic Examples

```
# Standard datetime format
call datetime-service.get_datetime {"format": "datetime"}
# Result: 2024-12-10 00:54:01
# Japanese format
call datetime-service.get_datetime {"format": "datetime_jp"}
# Result: 2024年12月10日 00時54分01秒
# Filename format
call datetime-service.get_datetime {"format": "filename_md"}
# Result: 20241210005401.md
```

## Supported Formats

| Format Name  | Example                     | Description                  |
| ------------ | --------------------------- | ---------------------------- |
| date         | 2024-12-10                  | Standard date format         |
| date_slash   | 2024/12/10                  | Date with slashes            |
| date_jp      | 2024年12月10日              | Japanese date format         |
| datetime     | 2024-12-10 00:54:01         | Standard datetime            |
| datetime_jp  | 2024年12月10日 00時54分01秒 | Japanese datetime            |
| datetime_t   | 2024-12-10T00:54:01         | DateTime with T separator    |
| compact      | 20241210005401              | Compact format for IDs       |
| compact_date | 20241210                    | Compact date only            |
| compact_time | 005401                      | Compact time only            |
| filename_md  | 20241210005401.md           | Markdown filename            |
| filename_txt | 20241210005401.txt          | Text filename                |
| filename_log | 20241210005401.log          | Log filename                 |
| iso          | 2024-12-10T00:54:01+0900    | ISO 8601 format              |
| iso_basic    | 20241210T005401+0900        | Basic ISO format             |
| log          | 2024-12-10 00:54:01.123456  | Log format with microseconds |
| log_compact  | 20241210_005401             | Compact log format           |
| time         | 00:54:01                    | Time only                    |
| time_jp      | 00時54分01秒                | Japanese time format         |

## Debugging

Since MCP servers run over stdio, debugging can be challenging. We recommend using the [MCP Inspector](https://github.com/modelcontextprotocol/inspector):

- Using PyPI package

```
npx @modelcontextprotocol/inspector uvx mcp-datetime
```

- Using downloaded source code from GitHub

```
git clone https://github.com/ZeparHyfar/mcp-datetime.git
npx @modelcontextprotocol/inspector uvx --directory ./mcp-datetime run mcp-datetime
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
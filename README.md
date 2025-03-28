# MCP YouTrack

A Model Context Protocol (MCP) server for interacting with YouTrack issue tracking system.

# Demo

### Example: add to Windsurf mcp_config.json
```json
{
  "mcpServers": {
    "mcp-youtrack": {
      "command": "uv",
      "args": [
        "run",
        "--with",
        "git+https://github.com/RageAgainstTheMachine101/mcp-youtrack.git",
        "--python",
        "3.13",
        "mcp-youtrack"
      ],
      "env": {
        "YOUTRACK_URL": "{BASE_URL}/youtrack",
        "YOUTRACK_TOKEN": "{TOKEN}"
      }
    }
  }
}
```

## Overview

This repository provides a Model Context Protocol (MCP) server for YouTrack integration. It uses the youtrack-sdk to interact with the YouTrack API and provides tools for common operations like querying issues, adding comments, updating issue fields, and retrieving detailed issue information.

The server is designed to be:
- **Efficient**: Optimized for common YouTrack operations
- **Flexible**: Easy to extend with additional YouTrack functionality
- **Secure**: Handles authentication and error handling
- **Type-safe**: Uses pydantic for data validation

## Getting Started

### Prerequisites

- Python 3.13 or later
- uv (for dependency management)
- A YouTrack instance with API access

### Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/mcp-youtrack.git
cd mcp-youtrack
```

2. Install dependencies:
```bash
uv lock
```

3. Set up environment variables:
```bash
# Create a .env file
echo "YOUTRACK_URL=https://your-youtrack-instance.com" > .env
echo "YOUTRACK_TOKEN=your-permanent-token" >> .env
```

4. Run the server:
```bash
uv run mcp-youtrack
```

## Architecture

The MCP YouTrack server follows a simple architecture:

- `mcp_youtrack/`: Main package
  - `__init__.py`: Package definition
  - `main.py`: Entry point
  - `mock_env.py`: Configuration management
  - `mcp_server.py`: MCP server implementation with tool definitions
  - `interactive.py`: Interactive command-line interface

### YouTrack Tools

The server provides the following tools for interacting with YouTrack:

#### Basic Operations
- `get_issues(query: str)`: Get issues matching a search query
- `comment_issue(issue_id: str, text: str)`: Add a comment to an issue
- `update_field(issue_id: str, field_id: str, field_value: Any)`: Update a field of an issue

#### Issue Details (New)
- `get_issue_details(issue_id: str)`: Get detailed information about a specific issue
- `get_issue_custom_fields(issue_id: str)`: Get custom fields for a specific issue
- `get_issue_comments(issue_id: str)`: Get comments for a specific issue

## Extending the Server

To add more YouTrack functionality to the server:

### 1. Add New Tools

Add new tools to the MCP server to extend its functionality:

```python
@mcp.tool()
def create_issue(summary: str, description: str = None, project_id: str = None):
    # Implement issue creation
    # ...
    return {"result": "Issue created successfully", "issue_id": new_issue.id}
```

## Testing

The server includes comprehensive tests for all functionality:

```bash
# Run all tests
pytest

# Run specific test files
pytest tests/test_mcp_server.py
pytest tests/test_issue_details.py
```

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

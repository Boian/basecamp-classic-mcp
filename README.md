# Basecamp Classic MCP Server

An MCP server for the [Basecamp Classic API](https://github.com/basecamp/basecamp-classic-api), built with [FastMCP](https://github.com/jlowin/fastmcp).

## Setup

```bash
uv sync
```

## Configuration

Set these environment variables before running:

| Variable | Description |
|---|---|
| `BASECAMP_URL` | Your Basecamp account URL, e.g. `https://yourcompany.basecamphq.com` |
| `BASECAMP_USERNAME` | Your Basecamp username or API token |
| `BASECAMP_PASSWORD` | Your Basecamp password (or `X` if using an API token) |

To use an API token instead of password: set `BASECAMP_USERNAME` to your token and `BASECAMP_PASSWORD` to `X`.

## Running

```bash
# stdio (for Claude Desktop / MCP clients)
uv run python server.py

# or via entry point
uv run basecamp-classic-mcp
```

## Development

Use the MCP Inspector to interactively test tools in a browser UI:

```bash
uv run --env-file .env fastmcp dev inspector server.py:mcp
```

## Claude Desktop configuration

Add to `~/Library/Application Support/Claude/claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "basecamp-classic": {
      "command": "uv",
      "args": ["run", "--directory", "/path/to/basecamp-classic-mcp", "python", "server.py"],
      "env": {
        "BASECAMP_URL": "https://yourcompany.basecamphq.com",
        "BASECAMP_USERNAME": "your-api-token",
        "BASECAMP_PASSWORD": "X"
      }
    }
  }
}
```

## Available Tools

### Projects
- `list_projects` — List all active projects
- `get_project(project_id)` — Get project details

### To-do Lists
- `list_todo_lists(project_id)` — List to-do lists in a project
- `get_todo_list(todo_list_id)` — Get a to-do list with its items

### To-do Items
- `list_todo_items(todo_list_id)` — List items in a to-do list
- `create_todo_item(todo_list_id, content, ...)` — Create a new to-do item
- `update_todo_item(todo_item_id, ...)` — Update an existing to-do item
- `complete_todo_item(todo_item_id)` — Mark an item complete
- `uncomplete_todo_item(todo_item_id)` — Mark an item incomplete
- `delete_todo_item(todo_item_id)` — Delete a to-do item

### Messages
- `list_messages(project_id)` — List recent messages in a project
- `get_message(message_id)` — Get a message with its body
- `create_message(project_id, title, body, ...)` — Post a new message

### Comments
- `list_comments(message_id)` — List comments on a message
- `create_comment(message_id, body)` — Add a comment to a message

### People
- `list_people` — List all people in the account
- `get_person(person_id)` — Get a person's details
- `get_current_person` — Get the authenticated user's details

### Milestones
- `list_milestones(project_id)` — List milestones in a project
- `complete_milestone(milestone_id)` — Mark a milestone complete
- `uncomplete_milestone(milestone_id)` — Mark a milestone incomplete

### Time Entries
- `list_time_entries(project_id)` — List time entries for a project
- `create_time_entry(project_id, date, hours, description, ...)` — Log time on a project

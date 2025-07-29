# AppDynamics MCP

Expose your AppDynamics SaaS API as an [MCP (Model Context Protocol)](https://docs.anthropic.com/en/docs/mcp) endpoint, enabling tools like Claude, Cursor, and others to interact with your monitoring data using natural language.

## 🔧 What This Repo Does

This repository includes a `mcp.json` file which:

- Connects to your AppDynamics SaaS controller
- Uses REST API to fetch application data and health rules
- Exposes the API via an MCP server using [git-mcp](https://github.com/gitmcp/gitmcp)

## 📦 Tools Defined

### 1. `GetApplications`

Fetches a list of all applications in your AppDynamics account.

### 2. `GetHealthRules`

Fetches the health rules for a specific application by ID.

## 🚀 How to Deploy

### Prerequisites

- Node.js installed
- Git installed
- A [GitHub Personal Access Token (PAT)](https://github.com/settings/tokens) if pushing to GitHub

### 1. Clone This Repo

```bash
git clone https://github.com/asafkiv/appdynamics-mcp.git
cd appdynamics-mcp
```

### 2. Run the MCP Server

```bash
npx git-mcp
```

This will start a local MCP server based on your `mcp.json` file.

### 3. Connect from a Supported AI Tool

Open Claude, Cursor, or any tool supporting MCP, and point it to the server URL provided by `git-mcp`.

## 🤖 How to Use in Cursor

1. Open **Cursor** ([https://cursor.sh](https://cursor.sh))
2. Go to `Settings → Model Context Protocol (MCP)`
3. Click **Add Custom MCP Server**
4. Enter the URL you got from running `npx git-mcp` (e.g. `http://localhost:5543/mcp.json`)
5. Use the `@AppDynamics MCP` context inside the editor like this:
   ```
   @AppDynamics MCP: run GetApplications
   ```
   or:
   ```
   @AppDynamics MCP: run GetHealthRules with {"APPLICATION_ID": 5}
   ```
6. Cursor will make the call to AppDynamics and return results inline.

## 🔐 Authentication

This setup uses Basic Authentication. To generate your credentials:

```bash
echo -n 'youruser@account:yourpassword' | base64
```

Then replace the value in the `Authorization` header in `mcp.json`:

```json
"Authorization": "Basic <your_base64_token>"
```

## 📘 AppDynamics API Reference

- [Official Docs](https://docs.appdynamics.com/)
- Sample endpoint: `GET /controller/rest/applications`

## 🙏 Credits

Created by Asaf using [git-mcp](https://github.com/gitmcp/gitmcp) and AppDynamics SaaS.

---

Feel free to fork or extend this setup for any other monitoring platforms!


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

### 1. Clone This Repo (optional)

```bash
git clone https://github.com/asafkiv/appdynamics-mcp.git
cd appdynamics-mcp
```

### 2. Hosted Automatically by git-mcp

You do **not** need to run a local server. Once this repository is public on GitHub, it is automatically hosted at:

```
https://gitmcp.io/asafkiv/appdynamics-mcp/mcp.json
```

## 🤖 How to Use in Cursor

1. Open **Cursor** ([https://cursor.sh](https://cursor.sh))
2. Go to `Settings → Model Context Protocol (MCP)`
3. Click **Add Custom MCP Server**
4. Enter:
   ```
   https://gitmcp.io/asafkiv/appdynamics-mcp/mcp.json
   ```
5. Use the `@AppDynamics MCP` context inside the editor like this:
   ```
   @AppDynamics MCP: run GetApplications
   ```
   or:
   ```
   @AppDynamics MCP: run GetHealthRules with {"APPLICATION_ID": 5}
   ```

## ⚠️ Troubleshooting

If Cursor shows an error like:

> “It appears that the AppDynamics MCP documentation and code are not currently available or accessible…”

Try the following:

### ✅ 1. Check the MCP URL

Paste this exact URL in Cursor:

```
https://gitmcp.io/asafkiv/appdynamics-mcp/mcp.json
```

Make sure the repo is public, and accessible.

### ✅ 2. Check Credentials in `mcp.json`

Ensure the `Authorization` header contains a valid **Base64** token:

```json
"Authorization": "Basic ZXhwZXJpZW5jZUBleHBlcmllbmNlOkNkZTMyd3NY"
```

You can test the endpoint with:

```bash
curl -H "Authorization: Basic ZXhw..." \
  https://experience.saas.appdynamics.com/controller/rest/applications?output=JSON
```

If the response fails, check credentials or account access.

### ✅ 3. Try Using Claude.ai

Claude also supports MCP — test there if Cursor doesn’t connect.

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


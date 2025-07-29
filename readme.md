# AppDynamics MCP

This repository defines a set of AppDynamics API endpoints that can be used by tools supporting the Model Context Protocol (MCP), such as Claude and Cursor. These endpoints provide access to monitoring data from AppDynamics SaaS.

## 📘 Overview

This project exposes key AppDynamics REST API endpoints in a format compatible with [gitmcp.io](https://gitmcp.io). This enables AI tools to query AppDynamics metadata, such as applications, health rules, tiers, and nodes.

## 🔗 API Endpoints

### 1. `GetApplications`

Fetches a list of all applications in AppDynamics.

```
GET /controller/rest/applications?output=JSON
```

**Returns:** Application ID, name, account info

### 2. `GetHealthRules`

Fetches all health rules for a specific application.

```
GET /controller/healthrules/applications/{APPLICATION_ID}?output=JSON
```

**Returns:** Rule name, evaluation criteria

### 3. `GetTiers`

Returns all tiers (business transactions layer) for a given application.

```
GET /controller/rest/applications/{APPLICATION_ID}/tiers?output=JSON
```

**Returns:** Tier name, ID, description

### 4. `GetNodes`

Fetches nodes running under a specific tier.

```
GET /controller/rest/applications/{APPLICATION_ID}/tiers/{TIER_ID}/nodes?output=JSON
```

**Returns:** Node name, machine name, agent type

## 🔐 Authentication

AppDynamics uses Basic Authentication. Encode your credentials as:

```bash
echo -n 'youruser@account:yourpassword' | base64
```

Then send this in the HTTP `Authorization` header:

```
Authorization: Basic <your_encoded_token>
```

## 🧠 Usage Example

To list all application names:

```
curl -H "Authorization: Basic ZXhw..." \
  https://experience.saas.appdynamics.com/controller/rest/applications?output=JSON
```

To get tiers for application 5:

```
curl -H "Authorization: Basic ZXhw..." \
  https://experience.saas.appdynamics.com/controller/rest/applications/5/tiers?output=JSON
```

## 🤖 For AI tools using MCP

Use the following GitMCP URL:

```
https://gitmcp.io/asafkiv/appdynamics-mcp
```

Add it as a custom MCP server in Cursor or Claude. Then call tools like:

```
@AppDynamics MCP: run GetApplications
@AppDynamics MCP: run GetTiers with {"APPLICATION_ID": 5}
```

## 🙏 Credits

Created by Asaf. Powered by AppDynamics and GitMCP.

---

Feel free to fork or extend this repository to support additional endpoints such as metrics, events, and dashboards.


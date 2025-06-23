# How to Run the Salesforce MCP Server

## Option 1: Use with Claude Desktop (Primary Method)

### Step 1: Install the Server
```bash
npm install -g @tsmztech/mcp-server-salesforce
```

### Step 2: Configure Claude Desktop
Add the configuration to your Claude Desktop config file:

**Location of config file:**
- **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
- **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
- **Linux**: `~/.config/Claude/claude_desktop_config.json`

**Choose one authentication method:**

#### Username/Password (Default)
```json
{
  "mcpServers": {
    "salesforce": {
      "command": "npx",
      "args": ["-y", "@tsmztech/mcp-server-salesforce"],
      "env": {
        "SALESFORCE_CONNECTION_TYPE": "User_Password",
        "SALESFORCE_USERNAME": "your_username@company.com",
        "SALESFORCE_PASSWORD": "your_password",
        "SALESFORCE_TOKEN": "your_security_token",
        "SALESFORCE_INSTANCE_URL": "https://login.salesforce.com"
      }
    }
  }
}
```

#### OAuth 2.0 Client Credentials
```json
{
  "mcpServers": {
    "salesforce": {
      "command": "npx",
      "args": ["-y", "@tsmztech/mcp-server-salesforce"],
      "env": {
        "SALESFORCE_CONNECTION_TYPE": "OAuth_2.0_Client_Credentials",
        "SALESFORCE_CLIENT_ID": "your_client_id",
        "SALESFORCE_CLIENT_SECRET": "your_client_secret",
        "SALESFORCE_INSTANCE_URL": "https://your-domain.my.salesforce.com"
      }
    }
  }
}
```

### Step 3: Restart Claude Desktop
After saving the config file, restart Claude Desktop.

### Step 4: Test the Connection
In Claude Desktop, try asking:
- "What Salesforce objects are available?"
- "Show me the fields in the Account object"

---

## Option 2: Build and Run from Source (Development)

### Step 1: Clone and Build
```bash
git clone https://github.com/whitewalker7/mcp-server-salesforce.git
cd mcp-server-salesforce
npm install
npm run build
```

### Step 2: Set Environment Variables
Create a `.env` file in the project root:

**For Username/Password:**
```env
SALESFORCE_CONNECTION_TYPE=User_Password
SALESFORCE_USERNAME=your_username@company.com
SALESFORCE_PASSWORD=your_password
SALESFORCE_TOKEN=your_security_token
SALESFORCE_INSTANCE_URL=https://login.salesforce.com
```

**For OAuth 2.0:**
```env
SALESFORCE_CONNECTION_TYPE=OAuth_2.0_Client_Credentials
SALESFORCE_CLIENT_ID=your_client_id
SALESFORCE_CLIENT_SECRET=your_client_secret
SALESFORCE_INSTANCE_URL=https://your-domain.my.salesforce.com
```

### Step 3: Run the Server
```bash
node dist/index.js
```

### Step 4: Test with Claude Desktop
Update your Claude Desktop config to use the local build:
```json
{
  "mcpServers": {
    "salesforce": {
      "command": "node",
      "args": ["/path/to/mcp-server-salesforce/dist/index.js"],
      "cwd": "/path/to/mcp-server-salesforce"
    }
  }
}
```

---

## Option 3: Run Standalone for Testing

You can test the MCP server directly without Claude Desktop:

### Install MCP Inspector
```bash
npm install -g @modelcontextprotocol/inspector
```

### Run with Inspector
```bash
mcp-inspector npx @tsmztech/mcp-server-salesforce
```

This opens a web interface where you can test the MCP tools directly.

---

## Salesforce Setup Requirements

### For Username/Password Authentication:
1. **Get your Salesforce username and password**
2. **Get your security token:**
   - Go to Salesforce Setup → My Personal Information → Reset My Security Token
   - Check your email for the token
3. **Combine password and token**: Use `password + token` as your password in the config

### For OAuth 2.0 Authentication:
1. **Create a Connected App in Salesforce:**
   - Setup → App Manager → New Connected App
   - Enable OAuth Settings
   - Select "Client Credentials Flow"
   - Add scopes (typically "api" is sufficient)
   - Save and get Client ID and Client Secret
2. **Note your instance URL** (e.g., `https://yourcompany.my.salesforce.com`)

---

## Troubleshooting

### Common Issues:
1. **"Invalid username/password"**: Check credentials and security token
2. **"Invalid client credentials"**: Verify OAuth app setup and credentials
3. **"Server not found"**: Ensure Claude Desktop config path is correct
4. **Connection timeout**: Check your Salesforce instance URL

### Debug Mode:
Add `"debug": true` to your Claude Desktop MCP server config to see detailed logs.

---

## Usage Examples

Once running, you can interact with Salesforce through Claude using natural language:

- "Find all Account objects in my Salesforce org"
- "Show me all Cases created this week"
- "Create a custom object called Product_Review__c"
- "Add a picklist field called Priority to the Case object"
- "Count opportunities by stage"
- "Execute Apex code to update account status"

The MCP server will translate these requests into appropriate Salesforce API calls.
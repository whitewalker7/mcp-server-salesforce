# Salesforce MCP Server Repository Summary

## Project Overview

**Repository:** `mcp-server-salesforce` by whitewalker7  
**Package:** `@tsmztech/mcp-server-salesforce` (v0.0.3)  
**Type:** Model Context Protocol (MCP) Server  
**Purpose:** Integrates Claude AI with Salesforce to enable natural language interactions with Salesforce data and operations

## What is MCP?

The Model Context Protocol (MCP) is a standardized way for AI assistants like Claude to interact with external systems and data sources. This server acts as a bridge between Claude and Salesforce, allowing users to perform complex Salesforce operations using everyday language.

## Core Features

### 🔍 **Data Operations**
- **Object Discovery**: Search and find Salesforce objects using partial name matches
- **Schema Information**: Get detailed field definitions, relationships, and picklist values
- **Record Querying**: Execute SOQL queries with support for relationships and complex filters
- **Aggregate Queries**: GROUP BY operations with aggregate functions (COUNT, SUM, AVG, etc.)
- **Data Manipulation**: Insert, update, delete, and upsert records across objects

### 🛠️ **Metadata Management**
- **Custom Objects**: Create and modify custom objects with sharing settings
- **Custom Fields**: Add fields with various types (text, number, picklist, lookup, etc.)
- **Field Permissions**: Manage Field Level Security across profiles
- **Relationship Management**: Create and configure lookup/master-detail relationships

### 💻 **Apex Development**
- **Apex Classes**: Read, create, and update Apex classes
- **Apex Triggers**: Manage triggers for various objects and events
- **Anonymous Execution**: Run Apex code without creating permanent classes
- **Debug Logs**: Enable, disable, and retrieve debug logs for users

### 🔎 **Advanced Search**
- **Cross-Object Search**: SOSL-based search across multiple objects
- **Flexible Filtering**: Support for complex WHERE conditions and relationships

## Technical Architecture

### **Technology Stack**
- **Language**: TypeScript
- **Runtime**: Node.js
- **Framework**: Model Context Protocol SDK
- **Salesforce Library**: JSForce
- **Build System**: TypeScript compiler with shx for permissions

### **Project Structure**
```
src/
├── index.ts              # Main server entry point
├── tools/                # Individual MCP tool implementations
│   ├── search.ts         # Object discovery
│   ├── describe.ts       # Schema information
│   ├── query.ts          # SOQL queries
│   ├── aggregateQuery.ts # Aggregate operations
│   ├── dml.ts           # Data manipulation
│   ├── manageObject.ts   # Custom object management
│   ├── manageField.ts    # Field management
│   ├── manageFieldPermissions.ts # FLS management
│   ├── searchAll.ts      # SOSL search
│   ├── readApex.ts       # Read Apex classes
│   ├── writeApex.ts      # Create/update Apex classes
│   ├── readApexTrigger.ts    # Read triggers
│   ├── writeApexTrigger.ts   # Create/update triggers
│   ├── executeAnonymous.ts   # Anonymous Apex execution
│   └── manageDebugLogs.ts    # Debug log management
├── types/                # TypeScript type definitions
├── utils/                # Utility functions
│   └── connection.ts     # Salesforce connection management
└── typings.d.ts         # Global type declarations
```

### **Available Tools (15 Total)**
1. `salesforce_search_objects` - Find objects by name pattern
2. `salesforce_describe_object` - Get object schema details
3. `salesforce_query_records` - Execute SOQL queries
4. `salesforce_aggregate_query` - Execute aggregate queries with GROUP BY
5. `salesforce_dml_records` - Insert/update/delete/upsert operations
6. `salesforce_manage_object` - Create/modify custom objects
7. `salesforce_manage_field` - Create/modify custom fields
8. `salesforce_manage_field_permissions` - Manage Field Level Security
9. `salesforce_search_all` - Cross-object SOSL search
10. `salesforce_read_apex` - Read Apex class source code
11. `salesforce_write_apex` - Create/update Apex classes
12. `salesforce_read_apex_trigger` - Read trigger source code
13. `salesforce_write_apex_trigger` - Create/update triggers
14. `salesforce_execute_anonymous` - Execute anonymous Apex
15. `salesforce_manage_debug_logs` - Debug log management

## Authentication Methods

### 1. Username/Password (Default)
- Uses traditional Salesforce credentials + security token
- Suitable for development and personal use

### 2. OAuth 2.0 Client Credentials Flow
- Uses Connected App credentials
- Recommended for production and organizational use
- Requires specific instance URL configuration

## Installation & Setup

### NPM Installation
```bash
npm install -g @tsmztech/mcp-server-salesforce
```

### Claude Desktop Configuration
Add to `claude_desktop_config.json`:

**Username/Password:**
```json
{
  "mcpServers": {
    "salesforce": {
      "command": "npx",
      "args": ["-y", "@tsmztech/mcp-server-salesforce"],
      "env": {
        "SALESFORCE_CONNECTION_TYPE": "User_Password",
        "SALESFORCE_USERNAME": "your_username",
        "SALESFORCE_PASSWORD": "your_password",
        "SALESFORCE_TOKEN": "your_security_token",
        "SALESFORCE_INSTANCE_URL": "https://login.salesforce.com"
      }
    }
  }
}
```

**OAuth 2.0:**
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

## Usage Examples

### Natural Language Queries
- "Find all objects related to Accounts"
- "Show me high-priority Cases with their related Contacts"
- "Count opportunities by stage"
- "Create a Customer Feedback object with a Rating field"
- "Grant System Administrator access to Custom_Field__c on Account"

### Development Operations
- "Show me all Apex classes with 'Controller' in the name"
- "Create a new trigger for the Opportunity object"
- "Execute Apex code to calculate account metrics"
- "Enable debug logs for user@example.com"

## Key Benefits

1. **Natural Language Interface**: No need to write SOQL or remember API syntax
2. **Comprehensive Coverage**: Handles data, metadata, and code operations
3. **Security Aware**: Proper Field Level Security management
4. **Development Friendly**: Full Apex development lifecycle support
5. **Enterprise Ready**: OAuth 2.0 support for organizational deployment
6. **Error Handling**: Clear feedback with Salesforce-specific error details

## Development Info

- **License**: MIT
- **Repository**: GitHub (whitewalker7/mcp-server-salesforce)
- **NPM Package**: @tsmztech/mcp-server-salesforce
- **Author**: tsmztech
- **Language**: TypeScript with Node.js
- **Dependencies**: MCP SDK, JSForce, dotenv

This MCP server essentially democratizes Salesforce administration and development by making complex operations accessible through conversational AI, bridging the gap between technical Salesforce knowledge and everyday business needs.
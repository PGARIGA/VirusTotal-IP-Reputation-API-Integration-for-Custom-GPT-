# 🛡️ VirusTotal IP Reputation API Integration for Custom GPT

This repository documents how to integrate the [VirusTotal IP Reputation API](https://developers.virustotal.com/reference/ip-object) into a **Custom GPT** using OpenAI's GPT Actions with OpenAPI 3.1.0 schema support.

---

## 🚀 Objective

Enable your Custom GPT to:

- Look up IP addresses in real time
- Analyze reputation based on VirusTotal's vendor results
- Return structured data such as:
  - Malicious count
  - Suspicious count
  - Harmless detections
  - ASN ownership
  - Last analysis metadata

---

## 🔧 OpenAPI 3.1 Schema

Import the following OpenAPI schema in the Custom GPT builder under:

> **Actions → Add Action → Import OpenAPI Schema**

```json
{
  "openapi": "3.1.0",
  "info": {
    "title": "VirusTotal IP Reputation API",
    "version": "1.0.0"
  },
  "servers": [
    {
      "url": "https://www.virustotal.com/api/v3"
    }
  ],
  "paths": {
    "/ip_addresses/{ip}": {
      "get": {
        "operationId": "getIpReputation",
        "summary": "Get IP reputation data from VirusTotal",
        "parameters": [
          {
            "name": "ip",
            "in": "path",
            "required": true,
            "schema": {
              "type": "string"
            },
            "description": "The IP address to lookup"
          }
        ],
        "responses": {
          "200": {
            "description": "Successful response from VirusTotal"
          }
        }
      }
    }
  }
}

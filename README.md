
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
```

---

## 🔐 Authentication Setup

1. In your GPT action configuration, go to the **Auth** tab.
2. Select:
   - **Auth type**: `API Key`
   - **Location**: `Header`
   - **Key name**: `x-apikey`
   - **Value**: Your VirusTotal API key  
     > Get your key from: [https://www.virustotal.com/gui/my-apikey](https://www.virustotal.com/gui/my-apikey)

---

## 💬 Usage in GPT Prompt

```plaintext
Check the reputation of IP address 170.64.203.176
```

### ✅ Sample GPT Response

```json
{
  "malicious": 3,
  "suspicious": 2,
  "undetected": 29,
  "harmless": 60,
  "as_owner": "DIGITALOCEAN-ASN",
  "continent": "OC"
}
```

---

## 🧪 CURL Equivalent

You can test the API independently with:

```bash
curl --request GET \
  --url "https://www.virustotal.com/api/v3/ip_addresses/170.64.203.176" \
  --header "x-apikey: YOUR_API_KEY"
```

---

## 📦 Future Enhancements

Expand the schema to support:

- `/domains/{domain}`
- `/files/{hash}`
- `/urls/{encoded_url}`

Enabling a complete threat intelligence assistant within Custom GPT.

---

## 📜 License

This project is licensed under the MIT License.

---

## 🤝 Contributing

Feel free to open issues or submit PRs for enhancements, such as additional endpoints or better response formatting.

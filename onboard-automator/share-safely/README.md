# Project: Share Safely (Storage & Web App)

**Scenario:** Build a temporary file-sharing web app where users upload a file and receive a time-limited download link (expires in 24 hours).  

**Services:** Azure App Service (B1 Linux plan), Blob Storage (Hot tier), Azure Functions (for cleanup), Azure SQL DB (for metadata), Key Vault (for secrets).  

**Why it matters:** Demonstrates secure storage, application hosting, and automation — core AZ-104 and help-desk skills.

## Steps
1. Create Resource Group `RG-ShareSafely`
2. Create Storage Account + Blob container (Hot tier)
3. Deploy Web App (App Service → B1 plan or Free F1)
4. Enable App Service Identity → connect to Key Vault (secret for connection string)
5. Add Azure Function Timer Trigger (every 6 hours) → delete expired files
6. Test upload and link expiry

## App Configuration Snippets
```bash
# Set storage connection string
az functionapp config appsettings set -n ShareSafelyApp -g RG-ShareSafely --settings "AzureWebJobsStorage=<connectionstring>"
# Add timer trigger (every 6 hours)
0 0 */6 * * *

Evidence (Screenshots to upload later)

Blob container with file and metadata

Web App URL (ShareSafely)

Function execution log

Key Vault secret list

App Service Identity enabled

Cost Analysis panel (~£1–£2/mo) -
Cost ≈ £2–£3.50/month (B1 plan ≈ £1.80; storage ≈ £0.02/GB; functions free tier)

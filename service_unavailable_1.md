## Overview
This documentation details the steps taken to diagnose and resolve an application error encountered in our Azure-hosted backend service. The issue stemmed from misconfigured environment variables on the Azure server.
 
### 1. Initial Observation
Error Encountered: The backend service was returning a "503 Service Unavailable" error when accessed.
Initial Check: The log stream from the Azure portal did not immediately reveal any errors.
 
### 2. Health Check Analysis
Status: The server instance was marked as "unhealthy" in the Azure portal.
Insight: Azure monitors the health of instances and replaces them if they remain unhealthy for over an hour. However, no automatic replacement occurred in this case, as there was only one instance.
 
### 3. DNS and Network Diagnosis
DNS Lookup (nslookup): Performed to check the resolution of the service URL. The command returned an NXDOMAIN error, indicating that the domain could not be resolved.
cURL Request: Running curl -I http://soomoja-cne9fmbdexbea0gr.westus-01.azurewebsites.net returned a "503 Service Unavailable" error, confirming that the service was not responding correctly.
 
### 4. Startup Command Verification
Issue Identified: The startup command was specified as startup.sh instead of ./startup.sh.
Resolution: Although this was initially thought to be a potential issue, further investigation revealed that the root cause was elsewhere.
 
### 5. Environment Variable Configuration
Diagnosis: The environmental variables configured in Azure were checked and found to be misconfigured. This was causing the application to fail during initialization.
Resolution: The environment variables were correctly reconfigured in the Azure portal, resolving the application error.
 
### 6. Final Verification
Health Status: After reconfiguring the environment variables, the health status of the server instance was checked again and marked as "healthy."
Service Access: The backend service was accessed successfully, confirming that the application was running as expected.
 
### Conclusion
This documentation should serve as a guide for team members when troubleshooting similar issues in Azure-hosted services. Always ensure that environment variables are correctly configured and use a systematic approach to diagnose and resolve issues.

By **Bala Grivine**

---
title: Python-script voor het ophalen van gegevens uit Azure Log Analytics | Microsoft Docs
description: Log Analytics logboek Search API kan een REST-API-client gegevens ophalen van een werkruimte voor logboekanalyse.  Dit artikel bevat een voorbeeld van pythonscript met de Search-API van het logboek.
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/28/2017
ms.author: bwren
ms.openlocfilehash: 56d7c6dc648a01e7b0efc167cb65c94bac5468ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="retrieve-data-from-log-analytics-with-a-python-script"></a><span data-ttu-id="faf82-104">Gegevens ophalen van logboekanalyse met een pythonscript</span><span class="sxs-lookup"><span data-stu-id="faf82-104">Retrieve data from Log Analytics with a Python script</span></span>
<span data-ttu-id="faf82-105">De [Log Analytics Log-API van zoekservice](log-analytics-log-search-api.md) kunnen een REST-API-clientcomputers gegevens ophalen van een werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="faf82-105">The [Log Analytics Log Search API](log-analytics-log-search-api.md) allows any REST API client to retrieve data from a Log Analytics workspace.</span></span>  <span data-ttu-id="faf82-106">Dit artikel bevat een voorbeeldscript Python die gebruikmaakt van de Log Analytics logboek zoeken-API.</span><span class="sxs-lookup"><span data-stu-id="faf82-106">This article presents a sample Python script that uses the Log Analytics Log Search API.</span></span>  

## <a name="authentication"></a><span data-ttu-id="faf82-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="faf82-107">Authentication</span></span>
<span data-ttu-id="faf82-108">Dit script maakt gebruik van een service-principal in Azure Active Directory om te verifiëren naar de werkruimte.</span><span class="sxs-lookup"><span data-stu-id="faf82-108">This script uses a service principal in Azure Active Directory to authenticate to the workspace.</span></span>  <span data-ttu-id="faf82-109">Service-principals toestaan dat een clienttoepassing om aan te vragen of de service een account verifiëren, zelfs als de client beschikt niet over de accountnaam.</span><span class="sxs-lookup"><span data-stu-id="faf82-109">Service principals allow a client application to request that the service authenticate an account even if the client does not have the account name.</span></span> <span data-ttu-id="faf82-110">Voordat u dit script uitvoert, moet u een service-principal met behulp van het proces op [portal gebruik maken van een Azure Active Directory-toepassing en service-principal die toegang bronnen tot](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="faf82-110">Before running this script, you must create a service principal using the process at [Use portal to create an Azure Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>  <span data-ttu-id="faf82-111">U moet de toepassings-ID, Tenant-ID en verificatiesleutel bieden aan het script.</span><span class="sxs-lookup"><span data-stu-id="faf82-111">You'll need to provide the Application ID, Tenant ID, and Authentication Key to the script.</span></span> 

> [!NOTE]
> <span data-ttu-id="faf82-112">Wanneer u [maken van een Azure Automation-account](../automation/automation-create-standalone-account.md), een service-principal dat geschikt is voor gebruik met dit script wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="faf82-112">When you [create an Azure Automation account](../automation/automation-create-standalone-account.md), a service principal is created that is suitable to use with this script.</span></span>  <span data-ttu-id="faf82-113">Als u al een service-principal gemaakt door Azure Automation hebt en vervolgens u kunnen moet gebruiken in plaats van een nieuw wachtwoord maken, hoewel u wellicht [maken van een verificatiesleutel](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) als deze nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="faf82-113">If you already have a service principal created by Azure Automation then you should be able to use it instead of creating a new one, although you may need to [create an authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) if it doesn't already have one.</span></span>

## <a name="script"></a><span data-ttu-id="faf82-114">Script</span><span class="sxs-lookup"><span data-stu-id="faf82-114">Script</span></span>
``` python
import adal
import requests
import json
import datetime
from pprint import pprint

# Details of workspace.  Fill in details for your workspace.
resource_group = 'xxxxxxxx'
workspace = 'xxxxxxxx'

# Details of query.  Modify these to your requirements.
query = "Type=Event"
end_time = datetime.datetime.utcnow()
start_time = end_time - datetime.timedelta(hours=24)
num_results = 100  # If not provided, a default of 10 results will be used.

# IDs for authentication.  Fill in values for your service principal.
subscription_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx'
tenant_id = 'xxxxxxxx-xxxx-xxxx-xxx-xxxxxxxxxxxx'
application_id = 'xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx'
application_key = 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'

# URLs for authentication
authentication_endpoint = 'https://login.microsoftonline.com/'
resource  = 'https://management.core.windows.net/'

# Get access token
context = adal.AuthenticationContext('https://login.microsoftonline.com/' + tenant_id)
token_response = context.acquire_token_with_client_credentials('https://management.core.windows.net/', application_id, application_key)
access_token = token_response.get('accessToken')

# Add token to header
headers = {
    "Authorization": 'Bearer ' + access_token,
    "Content-Type":'application/json'
}

# URLs for retrieving data
uri_base = 'https://management.azure.com'
uri_api = 'api-version=2015-11-01-preview'
uri_subscription = 'https://management.azure.com/subscriptions/' + subscription_id
uri_resourcegroup = uri_subscription + '/resourcegroups/'+ resource_group
uri_workspace = uri_resourcegroup + '/providers/Microsoft.OperationalInsights/workspaces/' + workspace
uri_search = uri_workspace + '/search'

# Build search parameters from query details
search_params = {
        "query": query,
        "top": num_results,
        "start": start_time.strftime('%Y-%m-%dT%H:%M:%S'),
        "end": end_time.strftime('%Y-%m-%dT%H:%M:%S')
        }

# Build URL and send post request
uri = uri_search + '?' + uri_api
response = requests.post(uri,json=search_params,headers=headers)

# Response of 200 if successful
if response.status_code == 200:

    # Parse the response to get the ID and status
    data = response.json()
    search_id = data["id"].split("/")
    id = search_id[len(search_id)-1]
    status = data["__metadata"]["Status"]

    # If status is pending, then keep checking until complete
    while status == "Pending":

        # Build URL to get search from ID and send request
        uri_search = uri_search + '/' + id
        uri = uri_search + '?' + uri_api
        response = requests.get(uri,headers=headers)

        # Parse the response to get the status
        data = response.json()
        status = data["__metadata"]["Status"]

else:

    # Request failed
    print (response.status_code)
    response.raise_for_status()

print ("Total records:" + str(data["__metadata"]["total"]))
print ("Returned top:" + str(data["__metadata"]["top"]))
pprint (data["value"])
```
## <a name="next-steps"></a><span data-ttu-id="faf82-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="faf82-115">Next steps</span></span>
- <span data-ttu-id="faf82-116">Meer informatie over de [Log Analytics Log-API van zoekservice](log-analytics-log-search-api.md).</span><span class="sxs-lookup"><span data-stu-id="faf82-116">Learn more about the [Log Analytics Log Search API](log-analytics-log-search-api.md).</span></span>
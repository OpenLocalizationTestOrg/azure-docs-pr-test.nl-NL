---
title: aaaPython script tooretrieve gegevens uit Azure Log Analytics | Microsoft Docs
description: Hallo Log Analytics logboek zoeken-API kunt u een REST-API-client tooretrieve gegevens van een werkruimte voor logboekanalyse.  Dit artikel bevat een voorbeeldscript Python Hallo Log zoeken-API gebruiken.
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
ms.openlocfilehash: a45693b04cd388301b859e7186ca671786d0229e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retrieve-data-from-log-analytics-with-a-python-script"></a><span data-ttu-id="78c7e-104">Gegevens ophalen van logboekanalyse met een pythonscript</span><span class="sxs-lookup"><span data-stu-id="78c7e-104">Retrieve data from Log Analytics with a Python script</span></span>
<span data-ttu-id="78c7e-105">Hallo [Log Analytics Log-API van zoekservice](log-analytics-log-search-api.md) kan een REST-API-client tooretrieve gegevens van een werkruimte voor logboekanalyse.</span><span class="sxs-lookup"><span data-stu-id="78c7e-105">hello [Log Analytics Log Search API](log-analytics-log-search-api.md) allows any REST API client tooretrieve data from a Log Analytics workspace.</span></span>  <span data-ttu-id="78c7e-106">Dit artikel bevat een voorbeeldscript Python die gebruikmaakt van Hallo Log Analytics logboek zoeken-API.</span><span class="sxs-lookup"><span data-stu-id="78c7e-106">This article presents a sample Python script that uses hello Log Analytics Log Search API.</span></span>  

## <a name="authentication"></a><span data-ttu-id="78c7e-107">Authentication</span><span class="sxs-lookup"><span data-stu-id="78c7e-107">Authentication</span></span>
<span data-ttu-id="78c7e-108">Dit script maakt gebruik van een service-principal in Azure Active Directory tooauthenticate toohello werkruimte.</span><span class="sxs-lookup"><span data-stu-id="78c7e-108">This script uses a service principal in Azure Active Directory tooauthenticate toohello workspace.</span></span>  <span data-ttu-id="78c7e-109">Service-principals toe dat een client toepassing toorequest die Hallo service een account verifiëren zelfs als het Hallo-client heeft geen Hallo-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="78c7e-109">Service principals allow a client application toorequest that hello service authenticate an account even if hello client does not have hello account name.</span></span> <span data-ttu-id="78c7e-110">Voordat u dit script uitvoert, moet u een service-principal met behulp van Hallo proces [portal toocreate gebruiken een Azure Active Directory-toepassing en service-principal die toegang bronnen tot](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="78c7e-110">Before running this script, you must create a service principal using hello process at [Use portal toocreate an Azure Active Directory application and service principal that can access resources](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>  <span data-ttu-id="78c7e-111">U moet tooprovide Hallo toepassings-ID, Tenant-ID en verificatiesleutel toohello script.</span><span class="sxs-lookup"><span data-stu-id="78c7e-111">You'll need tooprovide hello Application ID, Tenant ID, and Authentication Key toohello script.</span></span> 

> [!NOTE]
> <span data-ttu-id="78c7e-112">Wanneer u [maken van een Azure Automation-account](../automation/automation-create-standalone-account.md), een service-principal gemaakt die geschikt toouse met dit script.</span><span class="sxs-lookup"><span data-stu-id="78c7e-112">When you [create an Azure Automation account](../automation/automation-create-standalone-account.md), a service principal is created that is suitable toouse with this script.</span></span>  <span data-ttu-id="78c7e-113">Als u al een service-principal gemaakt door Azure Automation hebt en vervolgens u kunnen toouse moet deze in plaats van het maken van een nieuwe, hoewel u te wellicht[maken van een verificatiesleutel](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) als deze nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="78c7e-113">If you already have a service principal created by Azure Automation then you should be able toouse it instead of creating a new one, although you may need too[create an authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) if it doesn't already have one.</span></span>

## <a name="script"></a><span data-ttu-id="78c7e-114">Script</span><span class="sxs-lookup"><span data-stu-id="78c7e-114">Script</span></span>
``` python
import adal
import requests
import json
import datetime
from pprint import pprint

# Details of workspace.  Fill in details for your workspace.
resource_group = 'xxxxxxxx'
workspace = 'xxxxxxxx'

# Details of query.  Modify these tooyour requirements.
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

# Add token tooheader
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

    # Parse hello response tooget hello ID and status
    data = response.json()
    search_id = data["id"].split("/")
    id = search_id[len(search_id)-1]
    status = data["__metadata"]["Status"]

    # If status is pending, then keep checking until complete
    while status == "Pending":

        # Build URL tooget search from ID and send request
        uri_search = uri_search + '/' + id
        uri = uri_search + '?' + uri_api
        response = requests.get(uri,headers=headers)

        # Parse hello response tooget hello status
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
## <a name="next-steps"></a><span data-ttu-id="78c7e-115">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78c7e-115">Next steps</span></span>
- <span data-ttu-id="78c7e-116">Meer informatie over Hallo [Log Analytics Log-API van zoekservice](log-analytics-log-search-api.md).</span><span class="sxs-lookup"><span data-stu-id="78c7e-116">Learn more about hello [Log Analytics Log Search API](log-analytics-log-search-api.md).</span></span>

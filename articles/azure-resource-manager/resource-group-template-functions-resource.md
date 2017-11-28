---
title: aaaAzure Resource Manager-sjabloonfuncties - resources | Microsoft Docs
description: Beschrijft Hallo functies toouse in een Azure Resource Manager sjabloon tooretrieve waarden over bronnen.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/09/2017
ms.author: tomfitz
ms.openlocfilehash: c9d524b338b8b7ea6d8c9e0135d48e4fb8f167c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-functions-for-azure-resource-manager-templates"></a><span data-ttu-id="cd5d7-103">Resource-functies voor Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="cd5d7-103">Resource functions for Azure Resource Manager templates</span></span>

<span data-ttu-id="cd5d7-104">Resource Manager biedt Hallo functies voor het ophalen van waarden van de resource te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-104">Resource Manager provides hello following functions for getting resource values:</span></span>

* [<span data-ttu-id="cd5d7-105">listKeys en de lijst {Value}</span><span class="sxs-lookup"><span data-stu-id="cd5d7-105">listKeys and list{Value}</span></span>](#listkeys)
* [<span data-ttu-id="cd5d7-106">providers</span><span class="sxs-lookup"><span data-stu-id="cd5d7-106">providers</span></span>](#providers)
* [<span data-ttu-id="cd5d7-107">verwijzing</span><span class="sxs-lookup"><span data-stu-id="cd5d7-107">reference</span></span>](#reference)
* [<span data-ttu-id="cd5d7-108">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="cd5d7-108">resourceGroup</span></span>](#resourcegroup)
* [<span data-ttu-id="cd5d7-109">resourceId</span><span class="sxs-lookup"><span data-stu-id="cd5d7-109">resourceId</span></span>](#resourceid)
* [<span data-ttu-id="cd5d7-110">abonnement</span><span class="sxs-lookup"><span data-stu-id="cd5d7-110">subscription</span></span>](#subscription)

<span data-ttu-id="cd5d7-111">tooget waarden van parameters, variabelen of de huidige implementatie hello, Zie [implementatie waarde functies](resource-group-template-functions-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d7-111">tooget values from parameters, variables, or hello current deployment, see [Deployment value functions](resource-group-template-functions-deployment.md).</span></span>

<a id="listkeys" />
<a id="list" />

## <a name="listkeys-and-listvalue"></a><span data-ttu-id="cd5d7-112">listKeys en de lijst {Value}</span><span class="sxs-lookup"><span data-stu-id="cd5d7-112">listKeys and list{Value}</span></span>
`listKeys(resourceName or resourceIdentifier, apiVersion)`

`list{Value}(resourceName or resourceIdentifier, apiVersion)`

<span data-ttu-id="cd5d7-113">Retourneert Hallo waarden voor elk resourcetype die ondersteuning biedt voor bewerking Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-113">Returns hello values for any resource type that supports hello list operation.</span></span> <span data-ttu-id="cd5d7-114">de meest voorkomende gebruik Hallo is `listKeys`.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-114">hello most common usage is `listKeys`.</span></span> 

### <a name="parameters"></a><span data-ttu-id="cd5d7-115">Parameters</span><span class="sxs-lookup"><span data-stu-id="cd5d7-115">Parameters</span></span>

| <span data-ttu-id="cd5d7-116">Parameter</span><span class="sxs-lookup"><span data-stu-id="cd5d7-116">Parameter</span></span> | <span data-ttu-id="cd5d7-117">Vereist</span><span class="sxs-lookup"><span data-stu-id="cd5d7-117">Required</span></span> | <span data-ttu-id="cd5d7-118">Type</span><span class="sxs-lookup"><span data-stu-id="cd5d7-118">Type</span></span> | <span data-ttu-id="cd5d7-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cd5d7-119">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cd5d7-120">resourceName of resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="cd5d7-120">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="cd5d7-121">Ja</span><span class="sxs-lookup"><span data-stu-id="cd5d7-121">Yes</span></span> |<span data-ttu-id="cd5d7-122">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-122">string</span></span> |<span data-ttu-id="cd5d7-123">De unieke id voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-123">Unique identifier for hello resource.</span></span> |
| <span data-ttu-id="cd5d7-124">apiVersion</span><span class="sxs-lookup"><span data-stu-id="cd5d7-124">apiVersion</span></span> |<span data-ttu-id="cd5d7-125">Ja</span><span class="sxs-lookup"><span data-stu-id="cd5d7-125">Yes</span></span> |<span data-ttu-id="cd5d7-126">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-126">string</span></span> |<span data-ttu-id="cd5d7-127">API-versie van de status van de runtime.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-127">API version of resource runtime state.</span></span> <span data-ttu-id="cd5d7-128">Normaal gesproken in Hallo-indeling, **jjjj-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-128">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cd5d7-129">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-129">Return value</span></span>

<span data-ttu-id="cd5d7-130">Hallo geretourneerd object op basis van listKeys heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-130">hello returned object from listKeys has hello following format:</span></span>

```json
{
  "keys": [
    {
      "keyName": "key1",
      "permissions": "Full",
      "value": "{value}"
    },
    {
      "keyName": "key2",
      "permissions": "Full",
      "value": "{value}"
    }
  ]
}
```

<span data-ttu-id="cd5d7-131">Andere functies van de lijst met hebben verschillende retour-indelingen.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-131">Other list functions have different return formats.</span></span> <span data-ttu-id="cd5d7-132">toosee hello indeling van een functie, opnemen in Hallo uitvoer sectie zoals weergegeven in het Hallo-voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-132">toosee hello format of a function, include it in hello outputs section as shown in hello example template.</span></span> 

### <a name="remarks"></a><span data-ttu-id="cd5d7-133">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cd5d7-133">Remarks</span></span>

<span data-ttu-id="cd5d7-134">Een bewerking die met begint **lijst** kan worden gebruikt als een functie in uw sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-134">Any operation that starts with **list** can be used as a function in your template.</span></span> <span data-ttu-id="cd5d7-135">Hallo beschikbare bewerkingen zijn niet alleen listKeys, maar ook bewerkingen, zoals `list`, `listAdminKeys`, en `listStatus`.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-135">hello available operations include not only listKeys, but also operations like `list`, `listAdminKeys`, and `listStatus`.</span></span> <span data-ttu-id="cd5d7-136">U kunt geen echter gebruiken **lijst** bewerkingen uit waarbij de waarden in Hallo aanvraagtekst.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-136">However, you cannot use **list** operations that require values in hello request body.</span></span> <span data-ttu-id="cd5d7-137">Bijvoorbeeld, Hallo [lijst Account-SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) bewerking moet de aanvraag hoofdtekst parameters, zoals *signedExpiry*, zodat u deze niet binnen een sjabloon gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-137">For example, hello [List Account SAS](/rest/api/storagerp/storageaccounts#StorageAccounts_ListAccountSAS) operation requires request body parameters like *signedExpiry*, so you cannot use it within a template.</span></span>

<span data-ttu-id="cd5d7-138">toodetermine welke resourcetypen er een lijstbewerking, hebt u Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-138">toodetermine which resource types have a list operation, you have hello following options:</span></span>

* <span data-ttu-id="cd5d7-139">Weergave Hallo [REST-API-bewerkingen](/rest/api/) voor een resourceprovider en zoekt u bewerkingen na opvragen.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-139">View hello [REST API operations](/rest/api/) for a resource provider, and look for list operations.</span></span> <span data-ttu-id="cd5d7-140">Storage-accounts bijvoorbeeld Hallo [listKeys bewerking](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span><span class="sxs-lookup"><span data-stu-id="cd5d7-140">For example, storage accounts have hello [listKeys operation](/rest/api/storagerp/storageaccounts#StorageAccounts_ListKeys).</span></span>
* <span data-ttu-id="cd5d7-141">Gebruik Hallo [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-141">Use hello [Get-AzureRmProviderOperation](/powershell/module/azurerm.resources/get-azurermprovideroperation) PowerShell cmdlet.</span></span> <span data-ttu-id="cd5d7-142">Hallo wordt volgende voorbeeld alle bewerkingen na opvragen voor storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-142">hello following example gets all list operations for storage accounts:</span></span>

  ```powershell
  Get-AzureRmProviderOperation -OperationSearchString "Microsoft.Storage/*" | where {$_.Operation -like "*list*"} | FT Operation
  ```
* <span data-ttu-id="cd5d7-143">Hallo na toofilter alleen bewerkingen na opvragen hello Azure CLI-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-143">Use hello following Azure CLI command toofilter only hello list operations:</span></span>

  ```azurecli
  az provider operation show --namespace Microsoft.Storage --query "resourceTypes[?name=='storageAccounts'].operations[].name | [?contains(@, 'list')]"
  ```

<span data-ttu-id="cd5d7-144">Hallo resource opgeven met behulp van beide Hallo [resourceId functie](#resourceid), of de indeling Hallo `{providerNamespace}/{resourceType}/{resourceName}`.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-144">Specify hello resource by using either hello [resourceId function](#resourceid), or hello format `{providerNamespace}/{resourceType}/{resourceName}`.</span></span>


### <a name="example"></a><span data-ttu-id="cd5d7-145">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd5d7-145">Example</span></span>

<span data-ttu-id="cd5d7-146">Hallo volgende voorbeeld ziet u hoe tooreturn Hallo primaire en secundaire sleutels van een opslagaccount in Hallo sectie levert.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-146">hello following example shows how tooreturn hello primary and secondary keys from a storage account in hello outputs section.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountId": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "storageKeysOutput": {
            "value": "[listKeys(parameters('storageAccountId'), '2016-01-01')]",
            "type" : "object"
        }
    }
}
``` 

<a id="providers" />

## <a name="providers"></a><span data-ttu-id="cd5d7-147">providers</span><span class="sxs-lookup"><span data-stu-id="cd5d7-147">providers</span></span>
`providers(providerNamespace, [resourceType])`

<span data-ttu-id="cd5d7-148">Retourneert informatie over een resourceprovider en de volgende resourcetypen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-148">Returns information about a resource provider and its supported resource types.</span></span> <span data-ttu-id="cd5d7-149">Als u een resourcetype niet opgeeft, Hallo alle Hallo ondersteunde typen voor Hallo resourceprovider geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-149">If you do not provide a resource type, hello function returns all hello supported types for hello resource provider.</span></span>

### <a name="parameters"></a><span data-ttu-id="cd5d7-150">Parameters</span><span class="sxs-lookup"><span data-stu-id="cd5d7-150">Parameters</span></span>

| <span data-ttu-id="cd5d7-151">Parameter</span><span class="sxs-lookup"><span data-stu-id="cd5d7-151">Parameter</span></span> | <span data-ttu-id="cd5d7-152">Vereist</span><span class="sxs-lookup"><span data-stu-id="cd5d7-152">Required</span></span> | <span data-ttu-id="cd5d7-153">Type</span><span class="sxs-lookup"><span data-stu-id="cd5d7-153">Type</span></span> | <span data-ttu-id="cd5d7-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cd5d7-154">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cd5d7-155">providerNamespace</span><span class="sxs-lookup"><span data-stu-id="cd5d7-155">providerNamespace</span></span> |<span data-ttu-id="cd5d7-156">Ja</span><span class="sxs-lookup"><span data-stu-id="cd5d7-156">Yes</span></span> |<span data-ttu-id="cd5d7-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-157">string</span></span> |<span data-ttu-id="cd5d7-158">Namespace van Hallo-provider</span><span class="sxs-lookup"><span data-stu-id="cd5d7-158">Namespace of hello provider</span></span> |
| <span data-ttu-id="cd5d7-159">resourceType</span><span class="sxs-lookup"><span data-stu-id="cd5d7-159">resourceType</span></span> |<span data-ttu-id="cd5d7-160">Nee</span><span class="sxs-lookup"><span data-stu-id="cd5d7-160">No</span></span> |<span data-ttu-id="cd5d7-161">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-161">string</span></span> |<span data-ttu-id="cd5d7-162">Hallo type bron binnen Hallo opgegeven naamruimte.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-162">hello type of resource within hello specified namespace.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cd5d7-163">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-163">Return value</span></span>

<span data-ttu-id="cd5d7-164">Elk type ondersteunde wordt geretourneerd als Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-164">Each supported type is returned in hello following format:</span></span> 

```json
{
    "resourceType": "{name of resource type}",
    "locations": [ all supported locations ],
    "apiVersions": [ all supported API versions ]
}
```

<span data-ttu-id="cd5d7-165">Matrix ordening van Hallo geretourneerd waarden kan niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-165">Array ordering of hello returned values is not guaranteed.</span></span>

### <a name="example"></a><span data-ttu-id="cd5d7-166">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd5d7-166">Example</span></span>

<span data-ttu-id="cd5d7-167">Hallo volgende voorbeeld ziet u hoe toouse Hallo provider functie:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-167">hello following example shows how toouse hello provider function:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "providerOutput": {
            "value": "[providers('Microsoft.Web', 'sites')]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="cd5d7-168">Hallo retourneert voorgaande voorbeeld een object in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-168">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "resourceType": "sites",
  "locations": [
    "South Central US",
    "North Europe",
    "West Europe",
    "Southeast Asia",
    ...
  ],
  "apiVersions": [
    "2016-08-01",
    "2016-03-01",
    "2015-08-01-preview",
    "2015-08-01",
    ...
  ]
}
```

<a id="reference" />

## <a name="reference"></a><span data-ttu-id="cd5d7-169">Verwijzing</span><span class="sxs-lookup"><span data-stu-id="cd5d7-169">reference</span></span>
`reference(resourceName or resourceIdentifier, [apiVersion])`

<span data-ttu-id="cd5d7-170">Retourneert een object dat de runtimestatus van de bron.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-170">Returns an object representing a resource's runtime state.</span></span>

### <a name="parameters"></a><span data-ttu-id="cd5d7-171">Parameters</span><span class="sxs-lookup"><span data-stu-id="cd5d7-171">Parameters</span></span>

| <span data-ttu-id="cd5d7-172">Parameter</span><span class="sxs-lookup"><span data-stu-id="cd5d7-172">Parameter</span></span> | <span data-ttu-id="cd5d7-173">Vereist</span><span class="sxs-lookup"><span data-stu-id="cd5d7-173">Required</span></span> | <span data-ttu-id="cd5d7-174">Type</span><span class="sxs-lookup"><span data-stu-id="cd5d7-174">Type</span></span> | <span data-ttu-id="cd5d7-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cd5d7-175">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cd5d7-176">resourceName of resourceIdentifier</span><span class="sxs-lookup"><span data-stu-id="cd5d7-176">resourceName or resourceIdentifier</span></span> |<span data-ttu-id="cd5d7-177">Ja</span><span class="sxs-lookup"><span data-stu-id="cd5d7-177">Yes</span></span> |<span data-ttu-id="cd5d7-178">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-178">string</span></span> |<span data-ttu-id="cd5d7-179">Naam of de unieke id van een resource.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-179">Name or unique identifier of a resource.</span></span> |
| <span data-ttu-id="cd5d7-180">apiVersion</span><span class="sxs-lookup"><span data-stu-id="cd5d7-180">apiVersion</span></span> |<span data-ttu-id="cd5d7-181">Nee</span><span class="sxs-lookup"><span data-stu-id="cd5d7-181">No</span></span> |<span data-ttu-id="cd5d7-182">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-182">string</span></span> |<span data-ttu-id="cd5d7-183">API-versie van Hallo van de opgegeven bron.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-183">API version of hello specified resource.</span></span> <span data-ttu-id="cd5d7-184">Deze parameter bevatten wanneer Hallo resource niet binnen dezelfde sjabloon ingericht is.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-184">Include this parameter when hello resource is not provisioned within same template.</span></span> <span data-ttu-id="cd5d7-185">Normaal gesproken in Hallo-indeling, **jjjj-mm-dd**.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-185">Typically, in hello format, **yyyy-mm-dd**.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cd5d7-186">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-186">Return value</span></span>

<span data-ttu-id="cd5d7-187">Elk resourcetype retourneert verschillende eigenschappen voor de functie voor Hallo-verwijzing.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-187">Every resource type returns different properties for hello reference function.</span></span> <span data-ttu-id="cd5d7-188">Hallo-functie retourneert een enkele, vooraf gedefinieerde indeling.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-188">hello function does not return a single, predefined format.</span></span> <span data-ttu-id="cd5d7-189">toosee hello eigenschappen voor een brontype retourneren Hallo-object in Hallo levert sectie zoals weergegeven in Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-189">toosee hello properties for a resource type, return hello object in hello outputs section as shown in hello example.</span></span>

### <a name="remarks"></a><span data-ttu-id="cd5d7-190">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cd5d7-190">Remarks</span></span>

<span data-ttu-id="cd5d7-191">Hallo verwijzing functie is afgeleid van de waarde van een runtimestatus en daarom niet worden gebruikt in de sectie met sjabloonvariabelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-191">hello reference function derives its value from a runtime state, and therefore cannot be used in hello variables section.</span></span> <span data-ttu-id="cd5d7-192">Het kan worden gebruikt in het gedeelte van de uitvoer van een sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-192">It can be used in outputs section of a template.</span></span> 

<span data-ttu-id="cd5d7-193">Hallo verwijzing functie impliciet kunt declareren u één resource afhankelijk is van een andere bron, als resource Hallo waarnaar wordt verwezen is ingericht binnen dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-193">By using hello reference function, you implicitly declare that one resource depends on another resource if hello referenced resource is provisioned within same template.</span></span> <span data-ttu-id="cd5d7-194">U hoeft niet tooalso gebruik Hallo dependsOn eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-194">You do not need tooalso use hello dependsOn property.</span></span> <span data-ttu-id="cd5d7-195">Hallo wordt functie niet geëvalueerd als hello resource waarnaar wordt verwezen heeft implementatie voltooid.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-195">hello function is not evaluated until hello referenced resource has completed deployment.</span></span>

<span data-ttu-id="cd5d7-196">Hallo toosee namen en waarden voor een resourcetype, maakt een sjabloon die Hallo-object als resultaat geeft in Hallo uitvoer sectie.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-196">toosee hello property names and values for a resource type, create a template that returns hello object in hello outputs section.</span></span> <span data-ttu-id="cd5d7-197">Als er een bestaande resource van dat type is, retourneert de sjabloon Hallo object zonder eventuele nieuwe resources implementeren.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-197">If you have an existing resource of that type, your template returns hello object without deploying any new resources.</span></span> 

<span data-ttu-id="cd5d7-198">Normaal gesproken gebruikt u Hallo **verwijzing** werken tooreturn een bepaalde waarde van een object, zoals het blobeindpunt Hallo URI of een volledig gekwalificeerde domeinnaam.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-198">Typically, you use hello **reference** function tooreturn a particular value from an object, such as hello blob endpoint URI or fully qualified domain name.</span></span>

```json
"outputs": {
    "BlobUri": {
        "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01').primaryEndpoints.blob]",
        "type" : "string"
    },
    "FQDN": {
        "value": "[reference(concat('Microsoft.Network/publicIPAddresses/', parameters('ipAddressName')), '2016-03-30').dnsSettings.fqdn]",
        "type" : "string"
    }
}
```

### <a name="example"></a><span data-ttu-id="cd5d7-199">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd5d7-199">Example</span></span>

<span data-ttu-id="cd5d7-200">naslaginformatie en toodeploy Hallo-bron in Hallo dezelfde sjabloon gebruikt:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-200">toodeploy and reference hello resource in hello same template, use:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "storageAccountName": { 
          "type": "string"
      }
  },
  "resources": [
    {
      "name": "[parameters('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-12-01",
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {
      "referenceOutput": {
          "type": "object",
          "value": "[reference(parameters('storageAccountName'))]"
      }
    }
}
``` 

<span data-ttu-id="cd5d7-201">Hallo retourneert voorgaande voorbeeld een object in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-201">hello preceding example returns an object in hello following format:</span></span>

```json
{
   "creationTime": "2017-06-13T21:24:46.618364Z",
   "primaryEndpoints": {
     "blob": "https://examplestorage.blob.core.windows.net/",
     "file": "https://examplestorage.file.core.windows.net/",
     "queue": "https://examplestorage.queue.core.windows.net/",
     "table": "https://examplestorage.table.core.windows.net/"
   },
   "primaryLocation": "southcentralus",
   "provisioningState": "Succeeded",
   "statusOfPrimary": "available",
   "supportsHttpsTrafficOnly": false
}
```

<span data-ttu-id="cd5d7-202">Hallo volgende voorbeeld verwijst naar een opslagaccount dat niet is geïmplementeerd in deze sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-202">hello following example references a storage account that is not deployed in this template.</span></span> <span data-ttu-id="cd5d7-203">Hallo storage-account bestaat al binnen Hallo dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-203">hello storage account already exists within hello same resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "storageAccountName": {
            "type": "string"
        }
    },
    "resources": [],
    "outputs": {
        "ExistingStorage": {
            "value": "[reference(concat('Microsoft.Storage/storageAccounts/', parameters('storageAccountName')), '2016-01-01')]",
            "type" : "object"
        }
    }
}
```

<a id="resourcegroup" />

## <a name="resourcegroup"></a><span data-ttu-id="cd5d7-204">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="cd5d7-204">resourceGroup</span></span>
`resourceGroup()`

<span data-ttu-id="cd5d7-205">Retourneert een object dat de huidige resourcegroep Hallo vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-205">Returns an object that represents hello current resource group.</span></span> 

### <a name="return-value"></a><span data-ttu-id="cd5d7-206">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-206">Return value</span></span>

<span data-ttu-id="cd5d7-207">Hallo geretourneerd object bevindt zich in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-207">hello returned object is in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}",
  "name": "{resourceGroupName}",
  "location": "{resourceGroupLocation}",
  "tags": {
  },
  "properties": {
    "provisioningState": "{status}"
  }
}
```

### <a name="remarks"></a><span data-ttu-id="cd5d7-208">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cd5d7-208">Remarks</span></span>

<span data-ttu-id="cd5d7-209">Wordt vaak gebruikt van Hallo resourceGroup functie toocreate bronnen in Hallo dezelfde locatie als Hallo resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-209">A common use of hello resourceGroup function is toocreate resources in hello same location as hello resource group.</span></span> <span data-ttu-id="cd5d7-210">Hallo volgende voorbeeld wordt Hallo locatie tooassign Hallo locatie voor resourcegroep voor een website.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-210">hello following example uses hello resource group location tooassign hello location for a web site.</span></span>

```json
"resources": [
   {
      "apiVersion": "2016-08-01",
      "type": "Microsoft.Web/sites",
      "name": "[parameters('siteName')]",
      "location": "[resourceGroup().location]",
      ...
   }
]
```

### <a name="example"></a><span data-ttu-id="cd5d7-211">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd5d7-211">Example</span></span>

<span data-ttu-id="cd5d7-212">Hallo retourneert volgende sjabloon Hallo-eigenschappen van de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-212">hello following template returns hello properties of hello resource group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[resourceGroup()]",
            "type" : "object"
        }
    }
}
```

<span data-ttu-id="cd5d7-213">Hallo retourneert voorgaande voorbeeld een object in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-213">hello preceding example returns an object in hello following format:</span></span>

```json
{
  "id": "/subscriptions/{subscription-id}/resourceGroups/examplegroup",
  "name": "examplegroup",
  "location": "southcentralus",
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

<a id="resourceid" />

## <a name="resourceid"></a><span data-ttu-id="cd5d7-214">resourceId</span><span class="sxs-lookup"><span data-stu-id="cd5d7-214">resourceId</span></span>
`resourceId([subscriptionId], [resourceGroupName], resourceType, resourceName1, [resourceName2]...)`

<span data-ttu-id="cd5d7-215">Retourneert Hallo de unieke id van een resource.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-215">Returns hello unique identifier of a resource.</span></span> <span data-ttu-id="cd5d7-216">U deze functie gebruiken wanneer Hallo bronnaam niet eenduidig of niet ingericht binnen Hallo is dezelfde sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-216">You use this function when hello resource name is ambiguous or not provisioned within hello same template.</span></span> 

### <a name="parameters"></a><span data-ttu-id="cd5d7-217">Parameters</span><span class="sxs-lookup"><span data-stu-id="cd5d7-217">Parameters</span></span>

| <span data-ttu-id="cd5d7-218">Parameter</span><span class="sxs-lookup"><span data-stu-id="cd5d7-218">Parameter</span></span> | <span data-ttu-id="cd5d7-219">Vereist</span><span class="sxs-lookup"><span data-stu-id="cd5d7-219">Required</span></span> | <span data-ttu-id="cd5d7-220">Type</span><span class="sxs-lookup"><span data-stu-id="cd5d7-220">Type</span></span> | <span data-ttu-id="cd5d7-221">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cd5d7-221">Description</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="cd5d7-222">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="cd5d7-222">subscriptionId</span></span> |<span data-ttu-id="cd5d7-223">Nee</span><span class="sxs-lookup"><span data-stu-id="cd5d7-223">No</span></span> |<span data-ttu-id="cd5d7-224">tekenreeks (In GUID-indeling)</span><span class="sxs-lookup"><span data-stu-id="cd5d7-224">string (In GUID format)</span></span> |<span data-ttu-id="cd5d7-225">Standaardwaarde is Hallo huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-225">Default value is hello current subscription.</span></span> <span data-ttu-id="cd5d7-226">Deze waarde opgeven wanneer u een resource in een ander abonnement tooretrieve nodig.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-226">Specify this value when you need tooretrieve a resource in another subscription.</span></span> |
| <span data-ttu-id="cd5d7-227">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="cd5d7-227">resourceGroupName</span></span> |<span data-ttu-id="cd5d7-228">Nee</span><span class="sxs-lookup"><span data-stu-id="cd5d7-228">No</span></span> |<span data-ttu-id="cd5d7-229">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-229">string</span></span> |<span data-ttu-id="cd5d7-230">Standaardwaarde is de huidige resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-230">Default value is current resource group.</span></span> <span data-ttu-id="cd5d7-231">Deze waarde opgeven wanneer u een resource in een andere resourcegroep tooretrieve nodig.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-231">Specify this value when you need tooretrieve a resource in another resource group.</span></span> |
| <span data-ttu-id="cd5d7-232">resourceType</span><span class="sxs-lookup"><span data-stu-id="cd5d7-232">resourceType</span></span> |<span data-ttu-id="cd5d7-233">Ja</span><span class="sxs-lookup"><span data-stu-id="cd5d7-233">Yes</span></span> |<span data-ttu-id="cd5d7-234">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-234">string</span></span> |<span data-ttu-id="cd5d7-235">Type resource, met inbegrip van de naamruimte van de resource-provider.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-235">Type of resource including resource provider namespace.</span></span> |
| <span data-ttu-id="cd5d7-236">resourceName1</span><span class="sxs-lookup"><span data-stu-id="cd5d7-236">resourceName1</span></span> |<span data-ttu-id="cd5d7-237">Ja</span><span class="sxs-lookup"><span data-stu-id="cd5d7-237">Yes</span></span> |<span data-ttu-id="cd5d7-238">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-238">string</span></span> |<span data-ttu-id="cd5d7-239">Naam van de resource.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-239">Name of resource.</span></span> |
| <span data-ttu-id="cd5d7-240">resourceName2</span><span class="sxs-lookup"><span data-stu-id="cd5d7-240">resourceName2</span></span> |<span data-ttu-id="cd5d7-241">Nee</span><span class="sxs-lookup"><span data-stu-id="cd5d7-241">No</span></span> |<span data-ttu-id="cd5d7-242">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-242">string</span></span> |<span data-ttu-id="cd5d7-243">Volgende naam resourcesegment als bron is genest.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-243">Next resource name segment if resource is nested.</span></span> |

### <a name="return-value"></a><span data-ttu-id="cd5d7-244">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-244">Return value</span></span>

<span data-ttu-id="cd5d7-245">Hallo-id wordt in de volgende indeling Hallo geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-245">hello identifier is returned in hello following format:</span></span>

```json
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
```

### <a name="remarks"></a><span data-ttu-id="cd5d7-246">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="cd5d7-246">Remarks</span></span>

<span data-ttu-id="cd5d7-247">Hallo parameterwaarden die u opgeeft afhankelijk van of Hallo resource in Hallo is hetzelfde abonnement en de resource-groep als de huidige implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-247">hello parameter values you specify depend on whether hello resource is in hello same subscription and resource group as hello current deployment.</span></span>

<span data-ttu-id="cd5d7-248">tooget hello resource-ID voor een opslagaccount in Hallo hetzelfde abonnement en resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-248">tooget hello resource ID for a storage account in hello same subscription and resource group, use:</span></span>

```json
"[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="cd5d7-249">tooget hello resource-ID voor een opslagaccount in Hallo hetzelfde abonnement, maar een andere resourcegroep, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-249">tooget hello resource ID for a storage account in hello same subscription but a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="cd5d7-250">tooget hello resource-ID voor een opslagaccount in een ander abonnement en resourcegroep gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-250">tooget hello resource ID for a storage account in a different subscription and resource group, use:</span></span>

```json
"[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]"
```

<span data-ttu-id="cd5d7-251">tooget hello resource-ID voor een database in een andere resourcegroep gebruikt:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-251">tooget hello resource ID for a database in a different resource group, use:</span></span>

```json
"[resourceId('otherResourceGroup', 'Microsoft.SQL/servers/databases', parameters('serverName'), parameters('databaseName'))]"
```

<span data-ttu-id="cd5d7-252">Vaak het geval is, moet u toouse deze functie wanneer u een opslagaccount of een virtueel netwerk in een andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-252">Often, you need toouse this function when using a storage account or virtual network in an alternate resource group.</span></span> <span data-ttu-id="cd5d7-253">Hallo volgende voorbeeld ziet u hoe een resource van een externe resourcegroep gemakkelijk kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-253">hello following example shows how a resource from an external resource group can easily be used:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
      "virtualNetworkName": {
          "type": "string"
      },
      "virtualNetworkResourceGroup": {
          "type": "string"
      },
      "subnet1Name": {
          "type": "string"
      },
      "nicName": {
          "type": "string"
      }
  },
  "variables": {
      "vnetID": "[resourceId(parameters('virtualNetworkResourceGroup'), 'Microsoft.Network/virtualNetworks', parameters('virtualNetworkName'))]",
      "subnet1Ref": "[concat(variables('vnetID'),'/subnets/', parameters('subnet1Name'))]"
  },
  "resources": [
  {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[parameters('nicName')]",
      "location": "[parameters('location')]",
      "properties": {
          "ipConfigurations": [{
              "name": "ipconfig1",
              "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "subnet": {
                      "id": "[variables('subnet1Ref')]"
                  }
              }
          }]
       }
  }]
}
```

### <a name="example"></a><span data-ttu-id="cd5d7-254">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd5d7-254">Example</span></span>

<span data-ttu-id="cd5d7-255">Hallo retourneert volgende voorbeeld Hallo resource-ID voor een opslagaccount in de resourcegroep Hallo:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-255">hello following example returns hello resource ID for a storage account in hello resource group:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "sameRGOutput": {
            "value": "[resourceId('Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentRGOutput": {
            "value": "[resourceId('otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "differentSubOutput": {
            "value": "[resourceId('xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx', 'otherResourceGroup', 'Microsoft.Storage/storageAccounts','examplestorage')]",
            "type" : "string"
        },
        "nestedResourceOutput": {
            "value": "[resourceId('Microsoft.SQL/servers/databases', 'serverName', 'databaseName')]",
            "type" : "string"
        }
    }
}
```

<span data-ttu-id="cd5d7-256">Hallo uitvoer van Hallo voorgaande voorbeeld met standaardwaarden Hallo is:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-256">hello output from hello preceding example with hello default values is:</span></span>

| <span data-ttu-id="cd5d7-257">Naam</span><span class="sxs-lookup"><span data-stu-id="cd5d7-257">Name</span></span> | <span data-ttu-id="cd5d7-258">Type</span><span class="sxs-lookup"><span data-stu-id="cd5d7-258">Type</span></span> | <span data-ttu-id="cd5d7-259">Waarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-259">Value</span></span> |
| ---- | ---- | ----- |
| <span data-ttu-id="cd5d7-260">sameRGOutput</span><span class="sxs-lookup"><span data-stu-id="cd5d7-260">sameRGOutput</span></span> | <span data-ttu-id="cd5d7-261">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-261">String</span></span> | <span data-ttu-id="cd5d7-262">/Subscriptions/{Current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="cd5d7-262">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="cd5d7-263">differentRGOutput</span><span class="sxs-lookup"><span data-stu-id="cd5d7-263">differentRGOutput</span></span> | <span data-ttu-id="cd5d7-264">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-264">String</span></span> | <span data-ttu-id="cd5d7-265">/Subscriptions/{Current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="cd5d7-265">/subscriptions/{current-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="cd5d7-266">differentSubOutput</span><span class="sxs-lookup"><span data-stu-id="cd5d7-266">differentSubOutput</span></span> | <span data-ttu-id="cd5d7-267">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-267">String</span></span> | <span data-ttu-id="cd5d7-268">/Subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span><span class="sxs-lookup"><span data-stu-id="cd5d7-268">/subscriptions/{different-sub-id}/resourceGroups/otherResourceGroup/providers/Microsoft.Storage/storageAccounts/examplestorage</span></span> |
| <span data-ttu-id="cd5d7-269">nestedResourceOutput</span><span class="sxs-lookup"><span data-stu-id="cd5d7-269">nestedResourceOutput</span></span> | <span data-ttu-id="cd5d7-270">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cd5d7-270">String</span></span> | <span data-ttu-id="cd5d7-271">/Subscriptions/{Current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/servername/databases/databaseName</span><span class="sxs-lookup"><span data-stu-id="cd5d7-271">/subscriptions/{current-sub-id}/resourceGroups/examplegroup/providers/Microsoft.SQL/servers/serverName/databases/databaseName</span></span> |

<a id="subscription" />

## <a name="subscription"></a><span data-ttu-id="cd5d7-272">abonnement</span><span class="sxs-lookup"><span data-stu-id="cd5d7-272">subscription</span></span>
`subscription()`

<span data-ttu-id="cd5d7-273">Retourneert details over Hallo abonnement voor de huidige implementatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-273">Returns details about hello subscription for hello current deployment.</span></span> 

### <a name="return-value"></a><span data-ttu-id="cd5d7-274">Retourwaarde</span><span class="sxs-lookup"><span data-stu-id="cd5d7-274">Return value</span></span>

<span data-ttu-id="cd5d7-275">Hallo-functie retourneert Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="cd5d7-275">hello function returns hello following format:</span></span>

```json
{
    "id": "/subscriptions/{subscription-id}",
    "subscriptionId": "{subscription-id}",
    "tenantId": "{tenant-id}",
    "displayName": "{name-of-subscription}"
}
```

### <a name="example"></a><span data-ttu-id="cd5d7-276">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="cd5d7-276">Example</span></span>

<span data-ttu-id="cd5d7-277">Hallo ziet volgende voorbeeld Hallo abonnement functie die in Hallo uitvoer sectie.</span><span class="sxs-lookup"><span data-stu-id="cd5d7-277">hello following example shows hello subscription function called in hello outputs section.</span></span> 

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [],
    "outputs": {
        "subscriptionOutput": {
            "value": "[subscription()]",
            "type" : "object"
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="cd5d7-278">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd5d7-278">Next steps</span></span>
* <span data-ttu-id="cd5d7-279">Zie voor een beschrijving van de secties Hallo in een Azure Resource Manager-sjabloon [Azure Resource Manager-sjablonen samenstellen](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d7-279">For a description of hello sections in an Azure Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="cd5d7-280">toomerge meerdere sjablonen Zie [gekoppelde sjablonen gebruiken met Azure Resource Manager](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d7-280">toomerge multiple templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>
* <span data-ttu-id="cd5d7-281">een opgegeven aantal keren tooiterate bij het maken van een type resource, Zie [maken van meerdere exemplaren van resources in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d7-281">tooiterate a specified number of times when creating a type of resource, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="cd5d7-282">toosee hoe toodeploy Hallo sjabloon die u hebt gemaakt, Zie [Implementeer een toepassing met Azure Resource Manager-sjabloon](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="cd5d7-282">toosee how toodeploy hello template you have created, see [Deploy an application with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>


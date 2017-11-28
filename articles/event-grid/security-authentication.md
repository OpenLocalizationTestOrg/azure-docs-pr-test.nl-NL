---
title: aaaAzure gebeurtenis raster beveiligings- en -verificatie
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: 74f692c7e3a30856c3a80cbbfe82a26bf4c1c9b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="44be8-103">Gebeurtenis raster beveiligings- en -verificatie</span><span class="sxs-lookup"><span data-stu-id="44be8-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="44be8-104">Azure Event raster heeft drie soorten verificatie:</span><span class="sxs-lookup"><span data-stu-id="44be8-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="44be8-105">Gebeurtenisabonnementen</span><span class="sxs-lookup"><span data-stu-id="44be8-105">Event subscriptions</span></span>
* <span data-ttu-id="44be8-106">Gebeurtenis publiceren</span><span class="sxs-lookup"><span data-stu-id="44be8-106">Event publishing</span></span>
* <span data-ttu-id="44be8-107">WebHook gebeurtenis levering</span><span class="sxs-lookup"><span data-stu-id="44be8-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="44be8-108">WebHook gebeurtenis levering</span><span class="sxs-lookup"><span data-stu-id="44be8-108">WebHook Event delivery</span></span>

<span data-ttu-id="44be8-109">Webhooks zijn veel manieren tooreceive gebeurtenissen in realtime uit Azure Event raster.</span><span class="sxs-lookup"><span data-stu-id="44be8-109">Webhooks are one of many ways tooreceive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="44be8-110">Elke keer dat er wordt een nieuwe gebeurtenis gereed toobe geleverd, verzendt gebeurtenis raster een HTTP-aanvraag met tooyour WebHook met Hallo-gebeurtenis in de hoofdtekst van het Hallo.</span><span class="sxs-lookup"><span data-stu-id="44be8-110">Every time there is a new event ready toobe delivered, Event Grid sends an HTTP request with tooyour WebHook with hello event in hello body.</span></span>

<span data-ttu-id="44be8-111">Wanneer u uw eigen WebHook-eindpunt met raster gebeurtenis registreert, stuurt u een POST-aanvraag met een eenvoudige validatie-code in volgorde tooprove eindpunt eigendom.</span><span class="sxs-lookup"><span data-stu-id="44be8-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order tooprove endpoint ownership.</span></span> <span data-ttu-id="44be8-112">Uw app moet toorespond door echo back Hallo validatiecode.</span><span class="sxs-lookup"><span data-stu-id="44be8-112">Your app needs toorespond by echoing back hello validation code.</span></span> <span data-ttu-id="44be8-113">Gebeurtenis raster levert niet gebeurtenissen tooWebHook-eindpunten die u hebt de Hallo validatie niet doorstaan.</span><span class="sxs-lookup"><span data-stu-id="44be8-113">Event Grid will not deliver events tooWebHook endpoints that have not passed hello validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="44be8-114">Validatie-details:</span><span class="sxs-lookup"><span data-stu-id="44be8-114">Validation details:</span></span>

* <span data-ttu-id="44be8-115">Gebeurtenis raster boekt bij Hallo gebeurtenis abonnement maken of bij te werken, een 'SubscriptionValidationEvent' gebeurtenis toohello doel-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="44be8-115">At hello time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event toohello target endpoint.</span></span>
* <span data-ttu-id="44be8-116">Hallo-gebeurtenis bevat een waarde voor header 'Validatie Type gebeurtenis:'.</span><span class="sxs-lookup"><span data-stu-id="44be8-116">hello event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="44be8-117">hoofdtekst van de gebeurtenis Hallo Hallo heeft hetzelfde schema als andere gebeurtenissen gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="44be8-117">hello event body has hello same schema as other Event Grid events.</span></span>
* <span data-ttu-id="44be8-118">Hallo-gebeurtenisgegevens bevat de eigenschap 'ValidationCode' met een willekeurige tekenreeks bv. ' ValidationCode: acb13... '.</span><span class="sxs-lookup"><span data-stu-id="44be8-118">hello event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="44be8-119">In de volgorde tooprove eindpunt eigendom echo back Hallo validatie code bijvoorbeeld ' ValidationResponse: acb13... '.</span><span class="sxs-lookup"><span data-stu-id="44be8-119">In order tooprove endpoint ownership, echo back hello validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="44be8-120">Ten slotte is het belangrijk toonote Azure gebeurtenis raster ondersteunt alleen HTTPS-webhook-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="44be8-120">Finally, it is important toonote that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="44be8-121">Voor een gebeurtenisabonnement</span><span class="sxs-lookup"><span data-stu-id="44be8-121">Event subscription</span></span>

<span data-ttu-id="44be8-122">toosubscribe tooan gebeurtenis, hebt u Hallo **Microsoft.EventGrid/EventSubscriptions/Write** machtiging op Hallo resource vereist.</span><span class="sxs-lookup"><span data-stu-id="44be8-122">toosubscribe tooan event, you must have hello **Microsoft.EventGrid/EventSubscriptions/Write** permission on hello required resource.</span></span> <span data-ttu-id="44be8-123">U moet deze machtiging omdat u een nieuw abonnement bij Hallo bereik van de resource Hallo schrijft.</span><span class="sxs-lookup"><span data-stu-id="44be8-123">You need this permission because you are writing a new subscription at hello scope of hello resource.</span></span> <span data-ttu-id="44be8-124">Hallo vereist resource verschilt op basis van of u tooa systeemonderwerp of aangepaste onderwerp abonneert zich.</span><span class="sxs-lookup"><span data-stu-id="44be8-124">hello required resource differs based on whether you are subscribing tooa system topic or custom topic.</span></span> <span data-ttu-id="44be8-125">Beide typen worden in deze sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="44be8-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="44be8-126">Systeemonderwerpen (uitgevers Azure-service)</span><span class="sxs-lookup"><span data-stu-id="44be8-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="44be8-127">Voor systeemonderwerpen moet u de machtiging toowrite een nieuw gebeurtenisabonnement bij Hallo bereik van Hallo resource publishing Hallo gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="44be8-127">For system topics, you need permission toowrite a new event subscription at hello scope of hello resource publishing hello event.</span></span> <span data-ttu-id="44be8-128">Hallo-indeling van het Hallo-resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="44be8-128">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="44be8-129">Bijvoorbeeld: toosubscribe tooan gebeurtenis op een opslagaccount met de naam **MIJNACCT**, moet u de Hallo Microsoft.EventGrid/EventSubscriptions/Write machtiging op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="44be8-129">For example, toosubscribe tooan event on a storage account named **myacct**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="44be8-130">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="44be8-130">Custom topics</span></span>

<span data-ttu-id="44be8-131">Voor aangepaste onderwerpen moet u de machtiging toowrite een nieuw gebeurtenisabonnement bij Hallo bereik van Hallo gebeurtenis raster onderwerp.</span><span class="sxs-lookup"><span data-stu-id="44be8-131">For custom topics, you need permission toowrite a new event subscription at hello scope of hello Event Grid topic.</span></span> <span data-ttu-id="44be8-132">Hallo-indeling van het Hallo-resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="44be8-132">hello format of hello resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="44be8-133">Bijvoorbeeld: toosubscribe tooa aangepaste onderwerp met de naam **mytopic**, moet u de Hallo Microsoft.EventGrid/EventSubscriptions/Write machtiging op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="44be8-133">For example, toosubscribe tooa custom topic named **mytopic**, you need hello Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="44be8-134">Onderwerp publiceren</span><span class="sxs-lookup"><span data-stu-id="44be8-134">Topic publishing</span></span>

<span data-ttu-id="44be8-135">Onderwerpen over Shared Access Signature (SAS) of verificatie met sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44be8-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="44be8-136">SAS wordt aangeraden, maar sleutelverificatie biedt eenvoudige programmering en is compatibel met veel bestaande webhook uitgevers.</span><span class="sxs-lookup"><span data-stu-id="44be8-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="44be8-137">In HTTP-header Hallo Hallo verificatie waarde te nemen.</span><span class="sxs-lookup"><span data-stu-id="44be8-137">You include hello authentication value in hello HTTP header.</span></span> <span data-ttu-id="44be8-138">Gebruik voor SAS, **aeg-sas-token** voor Hallo header-waarde.</span><span class="sxs-lookup"><span data-stu-id="44be8-138">For SAS, use **aeg-sas-token** for hello header value.</span></span> <span data-ttu-id="44be8-139">Gebruik voor sleutelverificatie **aeg-sas-sleutel** voor Hallo header-waarde.</span><span class="sxs-lookup"><span data-stu-id="44be8-139">For key authentication, use **aeg-sas-key** for hello header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="44be8-140">Verificatie met sleutel</span><span class="sxs-lookup"><span data-stu-id="44be8-140">Key authentication</span></span>

<span data-ttu-id="44be8-141">Verificatie met een sleutel is Hallo eenvoudigste vorm van verificatie.</span><span class="sxs-lookup"><span data-stu-id="44be8-141">Key authentication is hello simplest form of authentication.</span></span> <span data-ttu-id="44be8-142">Hallo-indeling gebruiken:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="44be8-142">Use hello format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="44be8-143">Bijvoorbeeld het doorgeven van een sleutel met:</span><span class="sxs-lookup"><span data-stu-id="44be8-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="44be8-144">SAS-tokens</span><span class="sxs-lookup"><span data-stu-id="44be8-144">SAS tokens</span></span>

<span data-ttu-id="44be8-145">SAS-tokens voor gebeurtenis raster bevatten Hallo resource, een verlooptijd en een handtekening.</span><span class="sxs-lookup"><span data-stu-id="44be8-145">SAS tokens for Event Grid include hello resource, an expiration time, and a signature.</span></span> <span data-ttu-id="44be8-146">Hallo indeling van Hallo SAS-token is: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="44be8-146">hello format of hello SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="44be8-147">Hallo resource is Hallo pad voor Hallo onderwerp toowhich u gebeurtenissen wilt verzenden.</span><span class="sxs-lookup"><span data-stu-id="44be8-147">hello resource is hello path for hello topic toowhich you are sending events.</span></span> <span data-ttu-id="44be8-148">Een geldige resource-pad is bijvoorbeeld:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="44be8-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="44be8-149">U Hallo handtekening van een sleutel gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="44be8-149">You generate hello signature from a key.</span></span>

<span data-ttu-id="44be8-150">Bijvoorbeeld, een geldige **aeg-sas-token** waarde is:</span><span class="sxs-lookup"><span data-stu-id="44be8-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="44be8-151">Hallo volgende voorbeeld maakt een SAS-token voor gebruik met gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="44be8-151">hello following example creates a SAS token for use with Event Grid:</span></span>

```cs
static string BuildSharedAccessSignature(string resource, DateTime expirationUtc, string key)
{
    const char Resource = 'r';
    const char Expiration = 'e';
    const char Signature = 's';

    string encodedResource = HttpUtility.UrlEncode(resource);
    string encodedExpirationUtc = HttpUtility.UrlEncode(expirationUtc.ToString());

    string unsignedSas = $"{Resource}={encodedResource}&{Expiration}={encodedExpirationUtc}";
    using (var hmac = new HMACSHA256(Convert.FromBase64String(key)))
    {
        string signature = Convert.ToBase64String(hmac.ComputeHash(Encoding.UTF8.GetBytes(unsignedSas)));
        string encodedSignature = HttpUtility.UrlEncode(signature);
        string signedSas = $"{unsignedSas}&{Signature}={encodedSignature}";

        return signedSas;
    }
}
```

## <a name="management-access-control"></a><span data-ttu-id="44be8-152">Toegangsbeheer voor beheer</span><span class="sxs-lookup"><span data-stu-id="44be8-152">Management Access Control</span></span>

<span data-ttu-id="44be8-153">Azure Event raster kunt u toocontrol Hallo niveau van toegang gegeven toodifferent gebruikers toodo verschillende bewerkingen zoals de lijst met abonnementen, maakt u nieuwe en sleutels te genereren.</span><span class="sxs-lookup"><span data-stu-id="44be8-153">Azure Event Grid allows you toocontrol hello level of access given toodifferent users toodo various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="44be8-154">Gebeurtenis raster maakt gebruik van Azure toegang controleren RBAC (Role Based) voor deze.</span><span class="sxs-lookup"><span data-stu-id="44be8-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="44be8-155">Bewerkingstypen</span><span class="sxs-lookup"><span data-stu-id="44be8-155">Operation types</span></span>

<span data-ttu-id="44be8-156">Azure event raster ondersteunt Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="44be8-156">Azure event grid supports hello following actions:</span></span>

* <span data-ttu-id="44be8-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="44be8-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="44be8-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="44be8-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="44be8-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="44be8-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="44be8-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="44be8-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="44be8-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="44be8-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="44be8-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="44be8-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="44be8-163">Hallo laatste drie bewerkingen return mogelijk geheime informatie dat buiten het normale leesbewerkingen opgehaald gefilterd.</span><span class="sxs-lookup"><span data-stu-id="44be8-163">hello last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="44be8-164">Het is best practice voor u toorestrict toothese toegangsbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="44be8-164">It is best practice for you toorestrict access toothese operations.</span></span> <span data-ttu-id="44be8-165">Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure-opdrachtregelinterface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), en Hallo [REST-API](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="44be8-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and hello [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="44be8-166">Afdwingen van de rol op basis van de toegangscontrole (RBAC)</span><span class="sxs-lookup"><span data-stu-id="44be8-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="44be8-167">Volgende stappen tooenforce RBAC voor verschillende gebruikers hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="44be8-167">Use hello following steps tooenforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="44be8-168">Maken van een aangepaste rol-definitiebestand (.json)</span><span class="sxs-lookup"><span data-stu-id="44be8-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="44be8-169">Hallo hieronder vindt u voorbeeld gebeurtenis raster roldefinities waarmee gebruikers tooperform verschillende sets van acties.</span><span class="sxs-lookup"><span data-stu-id="44be8-169">hello following are sample Event Grid role definitions which allow users tooperform different sets of actions.</span></span>

<span data-ttu-id="44be8-170">**EventGridReadOnlyRole.json**: alleen toestaan alleen leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="44be8-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
```json
{ 
  "Name": "Event grid read only role", 
  "Id": "7C0B6B59-A278-4B62-BA19-411B70753856", 
  "IsCustom": true, 
  "Description": "Event grid read only role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/read" 
  ], 
  "NotActions": [ 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription Id>" 
  ] 
}
```

<span data-ttu-id="44be8-171">**EventGridNoDeleteListKeysRole.json**: toestaan beperkte post acties maar verwijderingsacties weigeren.</span><span class="sxs-lookup"><span data-stu-id="44be8-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
```json
{ 
  "Name": "Event grid No Delete Listkeys role", 
  "Id": "B9170838-5F9D-4103-A1DE-60496F7C9174", 
  "IsCustom": true, 
  "Description": "Event grid No Delete Listkeys role", 
  "Actions": [     
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action" 
  ], 
  "NotActions": [ 
    "Microsoft.EventGrid/*/delete" 
  ], 
  "AssignableScopes": [ 
    "/subscriptions/<Subscription id>" 
  ] 
}
```
 
<span data-ttu-id="44be8-172">**EventGridContributorRole.json**: kunnen alle gebeurtenis raster acties.</span><span class="sxs-lookup"><span data-stu-id="44be8-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
```json
{ 
  "Name": "Event grid contributor role", 
  "Id": "4BA6FB33-2955-491B-A74F-53C9126C9514", 
  "IsCustom": true, 
  "Description": "Event grid contributor role", 
  "Actions": [ 
    "Microsoft.EventGrid/*/write", 
    "Microsoft.EventGrid/*/delete", 
    "Microsoft.EventGrid/topics/listkeys/action", 
    "Microsoft.EventGrid/topics/regenerateKey/action", 
    "Microsoft.EventGrid/eventSubscriptions/getFullUrl/action" 
  ], 
  "NotActions": [], 
  "AssignableScopes": [ 
    "/subscriptions/d48566a8-2428-4a6c-8347-9675d09fb851" 
  ] 
} 
```

#### <a name="install-and-login-tooazure-cli"></a><span data-ttu-id="44be8-173">Installatie en aanmelding tooAzure CLI</span><span class="sxs-lookup"><span data-stu-id="44be8-173">Install and login tooAzure CLI</span></span>

* <span data-ttu-id="44be8-174">Azure CLI versie 0.8.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="44be8-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="44be8-175">meest recente versie van tooinstall hello en koppel deze met uw Azure-abonnement Zie [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="44be8-175">tooinstall hello latest version and associate it with your Azure subscription, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="44be8-176">Azure Resource Manager in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="44be8-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="44be8-177">Ga te[Using hello Azure CLI Hello Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44be8-177">Go too[Using hello Azure CLI with hello Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="44be8-178">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="44be8-178">Create a custom role</span></span>

<span data-ttu-id="44be8-179">een aangepaste beveiligingsrol toocreate gebruiken:</span><span class="sxs-lookup"><span data-stu-id="44be8-179">toocreate a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-hello-role-tooa-user"></a><span data-ttu-id="44be8-180">Hallo rol tooa gebruiker toewijzen</span><span class="sxs-lookup"><span data-stu-id="44be8-180">Assign hello role tooa user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="44be8-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44be8-181">Next steps</span></span>

* <span data-ttu-id="44be8-182">Zie voor een inleiding-tooEvent raster [over gebeurtenis raster](overview.md)</span><span class="sxs-lookup"><span data-stu-id="44be8-182">For an introduction tooEvent Grid, see [About Event Grid](overview.md)</span></span>

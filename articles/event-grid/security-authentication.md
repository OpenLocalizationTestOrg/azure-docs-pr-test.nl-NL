---
title: Azure Event raster beveiligings- en -verificatie
description: Beschrijving van Azure Event raster en de concepten.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/14/2017
ms.author: babanisa
ms.openlocfilehash: b6e1c7587c0b47d04862b4850741aaa3b7d191a8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="event-grid-security-and-authentication"></a><span data-ttu-id="5ca4e-103">Gebeurtenis raster beveiligings- en -verificatie</span><span class="sxs-lookup"><span data-stu-id="5ca4e-103">Event Grid security and authentication</span></span> 

<span data-ttu-id="5ca4e-104">Azure Event raster heeft drie soorten verificatie:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-104">Azure Event Grid has three types of authentication:</span></span>

* <span data-ttu-id="5ca4e-105">Gebeurtenisabonnementen</span><span class="sxs-lookup"><span data-stu-id="5ca4e-105">Event subscriptions</span></span>
* <span data-ttu-id="5ca4e-106">Gebeurtenis publiceren</span><span class="sxs-lookup"><span data-stu-id="5ca4e-106">Event publishing</span></span>
* <span data-ttu-id="5ca4e-107">WebHook gebeurtenis levering</span><span class="sxs-lookup"><span data-stu-id="5ca4e-107">WebHook event delivery</span></span>

## <a name="webhook-event-delivery"></a><span data-ttu-id="5ca4e-108">WebHook gebeurtenis levering</span><span class="sxs-lookup"><span data-stu-id="5ca4e-108">WebHook Event delivery</span></span>

<span data-ttu-id="5ca4e-109">Webhooks zijn veel manieren voor het ontvangen van gebeurtenissen in realtime uit Azure Event raster.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-109">Webhooks are one of many ways to receive events in real time from Azure Event Grid.</span></span>

<span data-ttu-id="5ca4e-110">Elke keer dat er wordt een nieuwe gebeurtenis gereed om te worden geleverd, wordt in gebeurtenis raster een HTTP-aanvraag met verzendt naar uw WebHook met de gebeurtenis in de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-110">Every time there is a new event ready to be delivered, Event Grid sends an HTTP request with to your WebHook with the event in the body.</span></span>

<span data-ttu-id="5ca4e-111">Wanneer u uw eigen WebHook-eindpunt met raster gebeurtenis registreert, stuurt u een POST-aanvraag met een eenvoudige validatiecode om te bewijzen dat eindpunt eigendom.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-111">When you register your own WebHook endpoint with Event Grid, it sends you a POST request with a simple validation code in order to prove endpoint ownership.</span></span> <span data-ttu-id="5ca4e-112">Uw app moet reageren door echo terug code voor de validatie.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-112">Your app needs to respond by echoing back the validation code.</span></span> <span data-ttu-id="5ca4e-113">Gebeurtenis raster levert geen gebeurtenissen naar WebHook-eindpunten die u hebt de validatie niet doorstaan.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-113">Event Grid will not deliver events to WebHook endpoints that have not passed the validation.</span></span>
 
### <a name="validation-details"></a><span data-ttu-id="5ca4e-114">Validatie-details:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-114">Validation details:</span></span>

* <span data-ttu-id="5ca4e-115">Op het moment van gebeurtenis abonnement maken of bij te werken boekt raster gebeurtenis een gebeurtenis 'SubscriptionValidationEvent' naar het doel-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-115">At the time of event subscription creation/update, Event Grid posts a “SubscriptionValidationEvent” event to the target endpoint.</span></span>
* <span data-ttu-id="5ca4e-116">De gebeurtenis bevat een waarde voor header 'Validatie Type gebeurtenis:'.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-116">The event contains a header value “Event-Type: Validation”.</span></span>
* <span data-ttu-id="5ca4e-117">De hoofdtekst van de gebeurtenis heeft hetzelfde schema als andere gebeurtenissen gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-117">The event body has the same schema as other Event Grid events.</span></span>
* <span data-ttu-id="5ca4e-118">Gegevens van de gebeurtenis bevat de eigenschap 'ValidationCode' met een willekeurige tekenreeks bv. ' ValidationCode: acb13... '.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-118">The event data includes a “ValidationCode” property with a randomly generated string e.g. “ValidationCode: acb13…”.</span></span>

<span data-ttu-id="5ca4e-119">Om te bewijzen dat eindpunt eigendom, echo teruggestuurd de validatie code bijvoorbeeld ' ValidationResponse: acb13... '.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-119">In order to prove endpoint ownership, echo back the validation code e.g “ValidationResponse: acb13…”.</span></span>

<span data-ttu-id="5ca4e-120">Ten slotte is het belangrijk te weten dat Azure gebeurtenis raster biedt alleen ondersteuning voor HTTPS-webhook-eindpunten.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-120">Finally, it is important to note that Azure Event Grid only supports HTTPS webhook endpoints.</span></span>
## <a name="event-subscription"></a><span data-ttu-id="5ca4e-121">Voor een gebeurtenisabonnement</span><span class="sxs-lookup"><span data-stu-id="5ca4e-121">Event subscription</span></span>

<span data-ttu-id="5ca4e-122">Abonneren op een gebeurtenis, hebt u de **Microsoft.EventGrid/EventSubscriptions/Write** toegang tot de vereiste bron.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-122">To subscribe to an event, you must have the **Microsoft.EventGrid/EventSubscriptions/Write** permission on the required resource.</span></span> <span data-ttu-id="5ca4e-123">U moet deze machtiging omdat u bij het schrijven van een nieuw abonnement op het bereik van de resource.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-123">You need this permission because you are writing a new subscription at the scope of the resource.</span></span> <span data-ttu-id="5ca4e-124">De vereiste bron verschilt op basis van of u op een systeemonderwerp of aangepaste onderwerp abonneert zich.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-124">The required resource differs based on whether you are subscribing to a system topic or custom topic.</span></span> <span data-ttu-id="5ca4e-125">Beide typen worden in deze sectie beschreven.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-125">Both types are described in this section.</span></span>

### <a name="system-topics-azure-service-publishers"></a><span data-ttu-id="5ca4e-126">Systeemonderwerpen (uitgevers Azure-service)</span><span class="sxs-lookup"><span data-stu-id="5ca4e-126">System topics (Azure service publishers)</span></span>

<span data-ttu-id="5ca4e-127">Voor systeemonderwerpen moet u machtigingen voor schrijven van een nieuw gebeurtenisabonnement bij het bereik van de bron voor het publiceren van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-127">For system topics, you need permission to write a new event subscription at the scope of the resource publishing the event.</span></span> <span data-ttu-id="5ca4e-128">De indeling van de resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span><span class="sxs-lookup"><span data-stu-id="5ca4e-128">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/{resource-provider}/{resource-type}/{resource-name}`</span></span>

<span data-ttu-id="5ca4e-129">Bijvoorbeeld, om u te abonneren op een gebeurtenis op een opslagaccount met de naam **MIJNACCT**, moet u de machtiging Microsoft.EventGrid/EventSubscriptions/Write op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span><span class="sxs-lookup"><span data-stu-id="5ca4e-129">For example, to subscribe to an event on a storage account named **myacct**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.Storage/storageAccounts/myacct`</span></span>

### <a name="custom-topics"></a><span data-ttu-id="5ca4e-130">Aangepaste-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="5ca4e-130">Custom topics</span></span>

<span data-ttu-id="5ca4e-131">Voor aangepaste onderwerpen moet u machtigingen voor schrijven van een nieuw gebeurtenisabonnement bij het bereik van het onderwerp gebeurtenis raster.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-131">For custom topics, you need permission to write a new event subscription at the scope of the Event Grid topic.</span></span> <span data-ttu-id="5ca4e-132">De indeling van de resource is:`/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span><span class="sxs-lookup"><span data-stu-id="5ca4e-132">The format of the resource is: `/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.EventGrid/topics/{topic-name}`</span></span>

<span data-ttu-id="5ca4e-133">Bijvoorbeeld, om u te abonneren op een eigen onderwerp met de naam **mytopic**, moet u de machtiging Microsoft.EventGrid/EventSubscriptions/Write op:`/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span><span class="sxs-lookup"><span data-stu-id="5ca4e-133">For example, to subscribe to a custom topic named **mytopic**, you need the Microsoft.EventGrid/EventSubscriptions/Write permission on: `/subscriptions/####/resourceGroups/testrg/providers/Microsoft.EventGrid/topics/mytopic`</span></span>

## <a name="topic-publishing"></a><span data-ttu-id="5ca4e-134">Onderwerp publiceren</span><span class="sxs-lookup"><span data-stu-id="5ca4e-134">Topic publishing</span></span>

<span data-ttu-id="5ca4e-135">Onderwerpen over Shared Access Signature (SAS) of verificatie met sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-135">Topics use either Shared Access Signature (SAS) or key authentication.</span></span> <span data-ttu-id="5ca4e-136">SAS wordt aangeraden, maar sleutelverificatie biedt eenvoudige programmering en is compatibel met veel bestaande webhook uitgevers.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-136">We recommend SAS, but key authentication provides simple programming, and is compatible with many existing webhook publishers.</span></span> 

<span data-ttu-id="5ca4e-137">De verificatie-waarde in de HTTP-header te nemen.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-137">You include the authentication value in the HTTP header.</span></span> <span data-ttu-id="5ca4e-138">Gebruik voor SAS, **aeg-sas-token** voor de headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-138">For SAS, use **aeg-sas-token** for the header value.</span></span> <span data-ttu-id="5ca4e-139">Gebruik voor sleutelverificatie **aeg-sas-sleutel** voor de headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-139">For key authentication, use **aeg-sas-key** for the header value.</span></span>

### <a name="key-authentication"></a><span data-ttu-id="5ca4e-140">Verificatie met sleutel</span><span class="sxs-lookup"><span data-stu-id="5ca4e-140">Key authentication</span></span>

<span data-ttu-id="5ca4e-141">Verificatie met een sleutel is de eenvoudigste vorm van verificatie.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-141">Key authentication is the simplest form of authentication.</span></span> <span data-ttu-id="5ca4e-142">Gebruik de volgende indeling:`aeg-sas-key: <your key>`</span><span class="sxs-lookup"><span data-stu-id="5ca4e-142">Use the format: `aeg-sas-key: <your key>`</span></span>

<span data-ttu-id="5ca4e-143">Bijvoorbeeld het doorgeven van een sleutel met:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-143">For example, you pass a key with:</span></span> 

```
aeg-sas-key: VXbGWce53249Mt8wuotr0GPmyJ/nDT4hgdEj9DpBeRr38arnnm5OFg==
```

### <a name="sas-tokens"></a><span data-ttu-id="5ca4e-144">SAS-tokens</span><span class="sxs-lookup"><span data-stu-id="5ca4e-144">SAS tokens</span></span>

<span data-ttu-id="5ca4e-145">SAS-tokens voor gebeurtenis raster zijn de resource een verlooptijd en een handtekening.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-145">SAS tokens for Event Grid include the resource, an expiration time, and a signature.</span></span> <span data-ttu-id="5ca4e-146">De indeling van het SAS-token is: `r={resource}&e={expiration}&s={signature}`.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-146">The format of the SAS token is: `r={resource}&e={expiration}&s={signature}`.</span></span>

<span data-ttu-id="5ca4e-147">De resource is het pad voor het onderwerp waarnaar u gebeurtenissen wilt verzenden.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-147">The resource is the path for the topic to which you are sending events.</span></span> <span data-ttu-id="5ca4e-148">Een geldige resource-pad is bijvoorbeeld:`https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span><span class="sxs-lookup"><span data-stu-id="5ca4e-148">For example, a valid resource path is: `https://<yourtopic>.<region>.eventgrid.azure.net/eventGrid/api/events`</span></span>

<span data-ttu-id="5ca4e-149">U de handtekening van een sleutel gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-149">You generate the signature from a key.</span></span>

<span data-ttu-id="5ca4e-150">Bijvoorbeeld, een geldige **aeg-sas-token** waarde is:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-150">For example, a valid **aeg-sas-token** value is:</span></span>

```http
aeg-sas-token: r=https%3a%2f%2fmytopic.eventgrid.azure.net%2feventGrid%2fapi%2fevent&e=6%2f15%2f2017+6%3a20%3a15+PM&s=a4oNHpRZygINC%2fBPjdDLOrc6THPy3tDcGHw1zP4OajQ%3d
``` 

<span data-ttu-id="5ca4e-151">Het volgende voorbeeld wordt een SAS-token voor gebruik met gebeurtenis raster:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-151">The following example creates a SAS token for use with Event Grid:</span></span>

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

## <a name="management-access-control"></a><span data-ttu-id="5ca4e-152">Toegangsbeheer voor beheer</span><span class="sxs-lookup"><span data-stu-id="5ca4e-152">Management Access Control</span></span>

<span data-ttu-id="5ca4e-153">Azure Event raster kunt u bepalen het niveau van toegang krijgen tot andere gebruikers kunnen verschillende bewerkingen zoals de lijst met abonnementen doen, maakt u nieuwe en genereren van sleutels.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-153">Azure Event Grid allows you to control the level of access given to different users to do various management operations such as list event subscriptions, create new ones, and generate keys.</span></span> <span data-ttu-id="5ca4e-154">Gebeurtenis raster maakt gebruik van Azure toegang controleren RBAC (Role Based) voor deze.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-154">Event Grid utilizes Azure's Role Based Access Check (RBAC) for this.</span></span>

### <a name="operation-types"></a><span data-ttu-id="5ca4e-155">Bewerkingstypen</span><span class="sxs-lookup"><span data-stu-id="5ca4e-155">Operation types</span></span>

<span data-ttu-id="5ca4e-156">Azure event raster ondersteunt de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-156">Azure event grid supports the following actions:</span></span>

* <span data-ttu-id="5ca4e-157">Microsoft.EventGrid/*/read</span><span class="sxs-lookup"><span data-stu-id="5ca4e-157">Microsoft.EventGrid/*/read</span></span> 
* <span data-ttu-id="5ca4e-158">Microsoft.EventGrid/*/write</span><span class="sxs-lookup"><span data-stu-id="5ca4e-158">Microsoft.EventGrid/*/write</span></span> 
* <span data-ttu-id="5ca4e-159">Microsoft.EventGrid/*/delete</span><span class="sxs-lookup"><span data-stu-id="5ca4e-159">Microsoft.EventGrid/*/delete</span></span> 
* <span data-ttu-id="5ca4e-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span><span class="sxs-lookup"><span data-stu-id="5ca4e-160">Microsoft.EventGrid/eventSubscriptions/getFullUrl/action</span></span> 
* <span data-ttu-id="5ca4e-161">Microsoft.EventGrid/topics/listKeys/action</span><span class="sxs-lookup"><span data-stu-id="5ca4e-161">Microsoft.EventGrid/topics/listKeys/action</span></span> 
* <span data-ttu-id="5ca4e-162">Microsoft.EventGrid/topics/regenerateKey/action</span><span class="sxs-lookup"><span data-stu-id="5ca4e-162">Microsoft.EventGrid/topics/regenerateKey/action</span></span>

<span data-ttu-id="5ca4e-163">De laatste drie bewerkingen mogelijk geheime gegevens die buiten het normale leesbewerkingen opgehaald gefilterd als resultaat.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-163">The last three operations return potentially secret information which gets filtered out of normal read operations.</span></span> <span data-ttu-id="5ca4e-164">Het is best practice voor u toegang tot deze bewerkingen te beperken.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-164">It is best practice for you to restrict access to these operations.</span></span> <span data-ttu-id="5ca4e-165">Aangepaste rollen kunnen worden gemaakt met [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure-opdrachtregelinterface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), en de [REST-API](../active-directory/role-based-access-control-manage-access-rest.md).</span><span class="sxs-lookup"><span data-stu-id="5ca4e-165">Custom roles can be created using [Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md), [Azure Command-Line Interface (CLI)](../active-directory/role-based-access-control-manage-access-azure-cli.md), and the [REST API](../active-directory/role-based-access-control-manage-access-rest.md).</span></span>

### <a name="enforcing-role-based-access-check-rbac"></a><span data-ttu-id="5ca4e-166">Afdwingen van de rol op basis van de toegangscontrole (RBAC)</span><span class="sxs-lookup"><span data-stu-id="5ca4e-166">Enforcing Role Based Access Check (RBAC)</span></span>

<span data-ttu-id="5ca4e-167">Gebruik de volgende stappen uit om af te dwingen RBAC voor verschillende gebruikers:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-167">Use the following steps to enforce RBAC for different users:</span></span>

#### <a name="create-a-custom-role-definition-file-json"></a><span data-ttu-id="5ca4e-168">Maken van een aangepaste rol-definitiebestand (.json)</span><span class="sxs-lookup"><span data-stu-id="5ca4e-168">Create a custom role definition file (.json)</span></span>

<span data-ttu-id="5ca4e-169">Hieronder vindt u voorbeeld gebeurtenis raster roldefinities waarmee gebruikers kunnen verschillende sets van acties uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-169">The following are sample Event Grid role definitions which allow users to perform different sets of actions.</span></span>

<span data-ttu-id="5ca4e-170">**EventGridReadOnlyRole.json**: alleen toestaan alleen leesbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-170">**EventGridReadOnlyRole.json**: Only allow read only operations.</span></span>
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

<span data-ttu-id="5ca4e-171">**EventGridNoDeleteListKeysRole.json**: toestaan beperkte post acties maar verwijderingsacties weigeren.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-171">**EventGridNoDeleteListKeysRole.json**: Allow restricted post actions but disallow delete actions.</span></span>
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
 
<span data-ttu-id="5ca4e-172">**EventGridContributorRole.json**: kunnen alle gebeurtenis raster acties.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-172">**EventGridContributorRole.json**: Allows all event grid actions.</span></span>  
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

#### <a name="install-and-login-to-azure-cli"></a><span data-ttu-id="5ca4e-173">Installeren en meld u aan bij de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5ca4e-173">Install and login to Azure CLI</span></span>

* <span data-ttu-id="5ca4e-174">Azure CLI versie 0.8.8 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-174">Azure CLI version 0.8.8 or later.</span></span> <span data-ttu-id="5ca4e-175">Zie voor het installeren van de meest recente versie en deze koppelen aan uw Azure-abonnement, [installeren en configureren van de Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="5ca4e-175">To install the latest version and associate it with your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="5ca4e-176">Azure Resource Manager in Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-176">Azure Resource Manager in Azure CLI.</span></span> <span data-ttu-id="5ca4e-177">Ga naar [met de Azure CLI met Resource Manager](../xplat-cli-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5ca4e-177">Go to [Using the Azure CLI with the Resource Manager](../xplat-cli-azure-resource-manager.md) for more details.</span></span>

#### <a name="create-a-custom-role"></a><span data-ttu-id="5ca4e-178">Een aangepaste beveiligingsrol maken</span><span class="sxs-lookup"><span data-stu-id="5ca4e-178">Create a custom role</span></span>

<span data-ttu-id="5ca4e-179">Gebruik het volgende voor het maken van een aangepaste rol:</span><span class="sxs-lookup"><span data-stu-id="5ca4e-179">To create a custom role, use:</span></span>

    azure role create --inputfile <file path>

#### <a name="assign-the-role-to-a-user"></a><span data-ttu-id="5ca4e-180">De rol toewijzen aan een gebruiker</span><span class="sxs-lookup"><span data-stu-id="5ca4e-180">Assign the role to a user</span></span>


    azure role assignment create --signInName  <user email address> --roleName "<name of role>" --resourceGroup <resource group name>


## <a name="next-steps"></a><span data-ttu-id="5ca4e-181">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5ca4e-181">Next steps</span></span>

* <span data-ttu-id="5ca4e-182">Zie voor een inleiding tot gebeurtenis raster, [over gebeurtenis raster](overview.md)</span><span class="sxs-lookup"><span data-stu-id="5ca4e-182">For an introduction to Event Grid, see [About Event Grid](overview.md)</span></span>

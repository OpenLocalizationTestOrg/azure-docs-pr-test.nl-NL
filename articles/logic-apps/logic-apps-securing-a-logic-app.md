---
title: aaaSecure tooAzure Logic Apps toegang | Microsoft Docs
description: Beveiliging voor de beveiliging van toegang tootriggers, invoer en uitvoer, actieparameters en services die worden gebruikt met werkstromen in Azure Logic Apps toevoegen.
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 11/22/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: abda2179e4cc2d2295cd8332ec017c848a456264
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-access-tooyour-logic-apps"></a><span data-ttu-id="47018-103">Toegang tot beveiligde tooyour logic apps</span><span class="sxs-lookup"><span data-stu-id="47018-103">Secure access tooyour logic apps</span></span>

<span data-ttu-id="47018-104">Er zijn veel hulpprogramma's beschikbaar toohelp beveiligen van uw logische app.</span><span class="sxs-lookup"><span data-stu-id="47018-104">There are many tools available toohelp you secure your logic app.</span></span>

* <span data-ttu-id="47018-105">Beveiliging van toegang tootrigger een logische app (HTTP-aanvragen Trigger)</span><span class="sxs-lookup"><span data-stu-id="47018-105">Securing access tootrigger a logic app (HTTP Request Trigger)</span></span>
* <span data-ttu-id="47018-106">Beveiliging van toegang toomanage bewerken of een logische app lezen</span><span class="sxs-lookup"><span data-stu-id="47018-106">Securing access toomanage, edit, or read a logic app</span></span>
* <span data-ttu-id="47018-107">Toocontents van invoer en uitvoer voor een run toegang beveiligen</span><span class="sxs-lookup"><span data-stu-id="47018-107">Securing access toocontents of inputs and outputs for a run</span></span>
* <span data-ttu-id="47018-108">Parameters of invoer binnen acties in een werkstroom beveiligen</span><span class="sxs-lookup"><span data-stu-id="47018-108">Securing parameters or inputs within actions in a workflow</span></span>
* <span data-ttu-id="47018-109">Beveiliging van toegang tooservices die aanvragen van een werkstroom ontvangen</span><span class="sxs-lookup"><span data-stu-id="47018-109">Securing access tooservices that receive requests from a workflow</span></span>

## <a name="secure-access-tootrigger"></a><span data-ttu-id="47018-110">Veilige toegang tootrigger</span><span class="sxs-lookup"><span data-stu-id="47018-110">Secure access tootrigger</span></span>

<span data-ttu-id="47018-111">Wanneer u werkt met een logische app, die wordt geactiveerd op een HTTP-aanvraag ([aanvragen](../connectors/connectors-native-reqres.md) of [Webhook](../connectors/connectors-native-webhook.md)), kunt u de toegang beperken zodat alleen geautoriseerde clients Hallo logische app kunnen worden gestart.</span><span class="sxs-lookup"><span data-stu-id="47018-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire hello logic app.</span></span> <span data-ttu-id="47018-112">Alle aanvragen in een logische app zijn versleuteld en beveiligd via SSL.</span><span class="sxs-lookup"><span data-stu-id="47018-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="47018-113">Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="47018-113">Shared Access Signature</span></span>

<span data-ttu-id="47018-114">Elk eindpunt van de aanvraag voor een logische app bevat een [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) als onderdeel van het Hallo-URL.</span><span class="sxs-lookup"><span data-stu-id="47018-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of hello URL.</span></span> <span data-ttu-id="47018-115">Elke URL bevat een `sp`, `sv`, en `sig` queryparameter.</span><span class="sxs-lookup"><span data-stu-id="47018-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="47018-116">Machtigingen zijn opgegeven door `sp`, en overeen tooHTTP methoden die zijn toegestaan, `sv` toogenerate Hallo versie die wordt gebruikt, is en `sig` gebruikte tooauthenticate toegang tootrigger is.</span><span class="sxs-lookup"><span data-stu-id="47018-116">Permissions are specified by `sp`, and correspond tooHTTP methods allowed, `sv` is hello version used toogenerate, and `sig` is used tooauthenticate access tootrigger.</span></span> <span data-ttu-id="47018-117">Hallo-handtekening wordt gegenereerd met behulp van Hallo SHA256-algoritme met een geheime sleutel op alle Hallo URL-paden en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="47018-117">hello signature is generated using hello SHA256 algorithm with a secret key on all hello URL paths and properties.</span></span> <span data-ttu-id="47018-118">Hallo geheime sleutel wordt nooit beschikbaar gemaakt en gepubliceerd, en versleuteld en opgeslagen als onderdeel van Hallo logische app wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="47018-118">hello secret key is never exposed and published, and is kept encrypted and stored as part of hello logic app.</span></span> <span data-ttu-id="47018-119">Uw logische app machtigt alleen triggers die een geldige handtekening gemaakt met de geheime sleutel Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="47018-119">Your logic app only authorizes triggers that contain a valid signature created with hello secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="47018-120">Toegangstoetsen genereren</span><span class="sxs-lookup"><span data-stu-id="47018-120">Regenerate access keys</span></span>

<span data-ttu-id="47018-121">U kunt een nieuwe beveiligde sleutel aan op elk gewenst moment via Hallo REST-API of Azure-portal opnieuw genereren.</span><span class="sxs-lookup"><span data-stu-id="47018-121">You can regenerate a new secure key at anytime through hello REST API or Azure portal.</span></span> <span data-ttu-id="47018-122">Alle huidige URL's die eerder met de oude sleutel Hallo zijn gegenereerd zijn ongeldig en niet langer gemachtigde toofire Hallo logische app.</span><span class="sxs-lookup"><span data-stu-id="47018-122">All current URLs that were generated previously using hello old key are invalidated and no longer authorized toofire hello logic app.</span></span>

1. <span data-ttu-id="47018-123">Open in hello Azure-portal, Hallo logische app die u wilt dat tooregenerate een sleutel</span><span class="sxs-lookup"><span data-stu-id="47018-123">In hello Azure portal, open hello logic app you want tooregenerate a key</span></span>
1. <span data-ttu-id="47018-124">Klik op Hallo **toegangssleutels** menu-item onder **instellingen**</span><span class="sxs-lookup"><span data-stu-id="47018-124">Click hello **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="47018-125">Kies Hallo sleutel tooregenerate en volledige Hallo-proces</span><span class="sxs-lookup"><span data-stu-id="47018-125">Choose hello key tooregenerate and complete hello process</span></span>

<span data-ttu-id="47018-126">URL's die u na het opnieuw genereren ophalen zijn met de nieuwe toegangssleutel Hallo ondertekend.</span><span class="sxs-lookup"><span data-stu-id="47018-126">URLs you retrieve after regeneration are signed with hello new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="47018-127">Callback URL's maken met een vervaldatum</span><span class="sxs-lookup"><span data-stu-id="47018-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="47018-128">Als u Hallo URL met andere partijen deelt, kunt u URL's genereren met de specifieke sleutels en vervaldatums indien nodig.</span><span class="sxs-lookup"><span data-stu-id="47018-128">If you are sharing hello URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="47018-129">U kunt vervolgens probleemloos sleutels rouleert of zorg ervoor dat toegang toofire een app is beperkt tooa bepaalde timespan.</span><span class="sxs-lookup"><span data-stu-id="47018-129">You can then seamlessly roll keys, or ensure access toofire an app is restricted tooa certain timespan.</span></span> <span data-ttu-id="47018-130">U kunt een vervaldatum opgeven voor een URL via Hallo [logische apps REST-API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="47018-130">You can specify an expiration date for a URL through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="47018-131">Opnemen in de hoofdtekst van het Hallo Hallo eigenschap `NotAfter` als een JSON-datumtekenreeks, die een callback-URL die is alleen geldig tot Hallo resulteert `NotAfter` datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="47018-131">In hello body, include hello property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until hello `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="47018-132">URL's maken met primaire of secundaire geheime sleutel</span><span class="sxs-lookup"><span data-stu-id="47018-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="47018-133">Wanneer u genereren of URL van de callback voor triggers op aanvraag gebaseerde, kunt u ook welke sleutel toouse toosign Hallo-URL opgeven.</span><span class="sxs-lookup"><span data-stu-id="47018-133">When you generate or list callback URLs for request-based triggers, you can also specify which key toouse toosign hello URL.</span></span>  <span data-ttu-id="47018-134">U kunt een URL die is ondertekend door een specifieke sleutel via Hallo genereren [logische apps REST-API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) als volgt:</span><span class="sxs-lookup"><span data-stu-id="47018-134">You can generate a URL signed by a specific key through hello [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="47018-135">Opnemen in de hoofdtekst van het Hallo Hallo eigenschap `KeyType` als `Primary` of `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="47018-135">In hello body, include hello property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="47018-136">Hiermee wordt een URL die is ondertekend door Hallo beveiligde sleutel die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="47018-136">This returns a URL signed by hello secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="47018-137">Binnenkomende IP-adressen beperken</span><span class="sxs-lookup"><span data-stu-id="47018-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="47018-138">Bovendien toohello Shared Access Signature, u kunt desgewenst toorestrict aanroepen van een logische app alleen van specifieke clients.</span><span class="sxs-lookup"><span data-stu-id="47018-138">In addition toohello Shared Access Signature, you may wish toorestrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="47018-139">Als u uw eindpunt via Azure API Management beheren, kunt u bijvoorbeeld Hallo logica beperken app tooonly Hallo aanvraag accepteren als Hallo aanvraag afkomstig is van Hallo API Management-exemplaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="47018-139">For example, if you manage your endpoint through Azure API Management, you can restrict hello logic app tooonly accept hello request when hello request comes from hello API Management instance IP address.</span></span>

<span data-ttu-id="47018-140">Deze instelling kan worden geconfigureerd in Hallo logic app-instellingen:</span><span class="sxs-lookup"><span data-stu-id="47018-140">This setting can be configured within hello logic app settings:</span></span>

1. <span data-ttu-id="47018-141">Open in hello Azure-portal, Hallo logische app die u wilt dat tooadd IP-adresbeperkingen</span><span class="sxs-lookup"><span data-stu-id="47018-141">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="47018-142">Klik op Hallo **configuratie voor toegangsbeheer** menu-item onder **instellingen**</span><span class="sxs-lookup"><span data-stu-id="47018-142">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="47018-143">Hallo-lijst met IP-adresbereiken toobe geaccepteerd door de trigger Hallo opgeven</span><span class="sxs-lookup"><span data-stu-id="47018-143">Specify hello list of IP address ranges toobe accepted by hello trigger</span></span>

<span data-ttu-id="47018-144">Een geldig IP-bereik heeft Hallo notatie `192.168.1.1/255`.</span><span class="sxs-lookup"><span data-stu-id="47018-144">A valid IP range takes hello format `192.168.1.1/255`.</span></span> <span data-ttu-id="47018-145">Als u Hallo logic app tooonly fire als een geneste logische app wilt, selecteer Hallo **alleen andere logic apps** optie.</span><span class="sxs-lookup"><span data-stu-id="47018-145">If you want hello logic app tooonly fire as a nested logic app, select hello **Only other logic apps** option.</span></span> <span data-ttu-id="47018-146">Deze optie wordt een lege matrix toohello bron, wat betekent dat alleen aanroepen vanuit Hallo-service zelf (bovenliggende logic apps) fire is.</span><span class="sxs-lookup"><span data-stu-id="47018-146">This option writes an empty array toohello resource, meaning only calls from hello service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="47018-147">U kunt nog steeds een logische app met een aanvraag-trigger uitvoeren via Hallo REST-API / Management `/triggers/{triggerName}/run` ongeacht IP.</span><span class="sxs-lookup"><span data-stu-id="47018-147">You can still run a logic app with a request trigger through hello REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="47018-148">Dit scenario is vereist voor verificatie op basis van hello Azure REST-API en alle gebeurtenissen in hello Azure controlelogboek wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="47018-148">This scenario requires authentication against hello Azure REST API, and all events would appear in hello Azure Audit Log.</span></span> <span data-ttu-id="47018-149">Toegang instellen toegangsbeheerbeleid dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="47018-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="47018-150">Het instellen van IP-adresbereiken op Hallo resourcedefinitie</span><span class="sxs-lookup"><span data-stu-id="47018-150">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="47018-151">Als u een [implementatiesjabloon](logic-apps-create-deploy-template.md) tooautomate uw implementaties, Hallo IP-bereik instellingen kunnen worden geconfigureerd op Hallo resource-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="47018-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="47018-152">Azure Active Directory, OAuth of andere beveiliging toevoegen</span><span class="sxs-lookup"><span data-stu-id="47018-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="47018-153">meer autorisatie boven op een logische app protocollen, tooadd [Azure API Management](https://azure.microsoft.com/services/api-management/) biedt uitgebreide controle, beveiliging, beleid en documentatie voor een willekeurig eindpunt met Hallo mogelijkheid tooexpose een logische app als een API.</span><span class="sxs-lookup"><span data-stu-id="47018-153">tooadd more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with hello capability tooexpose a logic app as an API.</span></span> <span data-ttu-id="47018-154">Azure API Management kan een openbare of particuliere eindpunt voor Hallo logische app, die gebruik Azure Active Directory, certificaat, OAuth of andere beveiligingsstandaarden maken kan worden blootgesteld.</span><span class="sxs-lookup"><span data-stu-id="47018-154">Azure API Management can expose a public or private endpoint for hello logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="47018-155">Wanneer een aanvraag wordt ontvangen, stuurt Azure API Management Hallo aanvraag toohello logic app (voor het uitvoeren van alle benodigde transformaties en beperkingen onderweg).</span><span class="sxs-lookup"><span data-stu-id="47018-155">When a request is received, Azure API Management forwards hello request toohello logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="47018-156">U kunt Hallo binnenkomende IP-adresbereik instellingen op Hallo logic app tooonly kunt Hallo logic app toobe geactiveerd van API Management gebruiken.</span><span class="sxs-lookup"><span data-stu-id="47018-156">You can use hello incoming IP range settings on hello logic app tooonly allow hello logic app toobe triggered from API Management.</span></span>

## <a name="secure-access-toomanage-or-edit-logic-apps"></a><span data-ttu-id="47018-157">Toegang tot beveiligde toomanage of bewerken logic apps</span><span class="sxs-lookup"><span data-stu-id="47018-157">Secure access toomanage or edit logic apps</span></span>

<span data-ttu-id="47018-158">U kunt toegang toomanagement bewerkingen op een logische app beperken zodat alleen bepaalde gebruikers of groepen kunnen tooperform bewerkingen op Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="47018-158">You can restrict access toomanagement operations on a logic app so that only specific users or groups are able tooperform operations on hello resource.</span></span> <span data-ttu-id="47018-159">Logische apps gebruiken hello Azure [op rollen gebaseerde toegangsbeheer (RBAC)](../active-directory/role-based-access-control-configure.md) functie en kunnen worden aangepast met Hallo dezelfde hulpmiddelen.</span><span class="sxs-lookup"><span data-stu-id="47018-159">Logic apps use hello Azure [Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-configure.md) feature, and can be customized with hello same tools.</span></span>  <span data-ttu-id="47018-160">Er zijn enkele ingebouwde rollen die kunt u ook leden van uw abonnement tooas toewijzen:</span><span class="sxs-lookup"><span data-stu-id="47018-160">There are a few built-in roles you can assign members of your subscription tooas well:</span></span>

* <span data-ttu-id="47018-161">**Logic App Inzender** -toegang tooview, bewerken en bijwerken van een logische app biedt.</span><span class="sxs-lookup"><span data-stu-id="47018-161">**Logic App Contributor** - Provides access tooview, edit, and update a logic app.</span></span>  <span data-ttu-id="47018-162">Kan resource Hallo verwijderen of admin bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="47018-162">Cannot remove hello resource or perform admin operations.</span></span>
* <span data-ttu-id="47018-163">**Logic App Operator** : kan hello logische app en uitvoeringsgeschiedenis weergeven en in-of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="47018-163">**Logic App Operator** - Can view hello logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="47018-164">Niet kunt bewerken of Hallo-definitie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="47018-164">Cannot edit or update hello definition.</span></span>

<span data-ttu-id="47018-165">U kunt ook [Azure Resource vergrendeling](../azure-resource-manager/resource-group-lock-resources.md) tooprevent wijzigen of verwijderen van logische apps.</span><span class="sxs-lookup"><span data-stu-id="47018-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) tooprevent changing or deleting logic apps.</span></span> <span data-ttu-id="47018-166">Deze mogelijkheid is waardevolle tooprevent productiebronnen niet gewijzigd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="47018-166">This capability is valuable tooprevent production resources from changes or deletions.</span></span>

## <a name="secure-access-toocontents-of-hello-run-history"></a><span data-ttu-id="47018-167">Veilige toegang toocontents Hallo geschiedenis uitvoeren</span><span class="sxs-lookup"><span data-stu-id="47018-167">Secure access toocontents of hello run history</span></span>

<span data-ttu-id="47018-168">U kunt toegang toocontents van in- of uitgangen beperken van vorige uitgevoerd toospecific IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="47018-168">You can restrict access toocontents of inputs or outputs from previous runs toospecific IP address ranges.</span></span>  

<span data-ttu-id="47018-169">Alle gegevens binnen een werkstroom uitgevoerd is versleuteld in rust en onderweg.</span><span class="sxs-lookup"><span data-stu-id="47018-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="47018-170">Wanneer een toorun gespreksgeschiedenis wordt gedaan, wordt Hallo service verifieert Hallo-aanvraag en biedt koppelingen toohello aanvraag en antwoord-invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="47018-170">When a call toorun history is made, hello service authenticates hello request and provides links toohello request and response inputs and outputs.</span></span> <span data-ttu-id="47018-171">Deze koppeling kan worden beveiligd zodat alleen aanvragen tooview inhoud uit een aangewezen IP-adresbereik Hallo inhoud retourneren.</span><span class="sxs-lookup"><span data-stu-id="47018-171">This link can be protected so only requests tooview content from a designated IP address range return hello contents.</span></span> <span data-ttu-id="47018-172">Voor extra toegangsbeheer kunt u deze mogelijkheid.</span><span class="sxs-lookup"><span data-stu-id="47018-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="47018-173">U kunt zelfs opgeven met een IP-adres zoals `0.0.0.0` zodat niemand toegang de invoer/uitvoer tot heeft.</span><span class="sxs-lookup"><span data-stu-id="47018-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="47018-174">Alleen gebruikers met beheerdersmachtigingen kan deze beperking Hallo mogelijkheid bieden voor 'just in time' toegang tooworkflow inhoud verwijderen.</span><span class="sxs-lookup"><span data-stu-id="47018-174">Only someone with admin permissions could remove this restriction, providing hello possibility for 'just-in-time' access tooworkflow contents.</span></span>

<span data-ttu-id="47018-175">Deze instelling kan worden geconfigureerd in de broninstellingen Hallo Hallo Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="47018-175">This setting can be configured within hello resource settings of hello Azure portal:</span></span>

1. <span data-ttu-id="47018-176">Open in hello Azure-portal, Hallo logische app die u wilt dat tooadd IP-adresbeperkingen</span><span class="sxs-lookup"><span data-stu-id="47018-176">In hello Azure portal, open hello logic app you want tooadd IP address restrictions</span></span>
1. <span data-ttu-id="47018-177">Klik op Hallo **configuratie voor toegangsbeheer** menu-item onder **instellingen**</span><span class="sxs-lookup"><span data-stu-id="47018-177">Click hello **Access control configuration** menu item under **Settings**</span></span>
1. <span data-ttu-id="47018-178">Lijst met IP-adresbereiken voor toegang tot toocontent Hallo opgeven</span><span class="sxs-lookup"><span data-stu-id="47018-178">Specify hello list of IP address ranges for access toocontent</span></span>

#### <a name="setting-ip-ranges-on-hello-resource-definition"></a><span data-ttu-id="47018-179">Het instellen van IP-adresbereiken op Hallo resourcedefinitie</span><span class="sxs-lookup"><span data-stu-id="47018-179">Setting IP ranges on hello resource definition</span></span>

<span data-ttu-id="47018-180">Als u een [implementatiesjabloon](logic-apps-create-deploy-template.md) tooautomate uw implementaties, Hallo IP-bereik instellingen kunnen worden geconfigureerd op Hallo resource-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="47018-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) tooautomate your deployments, hello IP range settings can be configured on hello resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="47018-181">Beveiligde parameters en invoer binnen een werkstroom</span><span class="sxs-lookup"><span data-stu-id="47018-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="47018-182">U kunt tooparameterize sommige aspecten van de werkstroomdefinitie van een voor implementatie in omgevingen.</span><span class="sxs-lookup"><span data-stu-id="47018-182">You might want tooparameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="47018-183">Sommige parameters mogelijk ook beveiligde parameters die u niet wilt dat tooappear bij het bewerken van een werkstroom, zoals een client-ID en clientgeheim voor [Azure Active Directory-verificatie](../connectors/connectors-native-http.md#authentication) van een HTTP-actie.</span><span class="sxs-lookup"><span data-stu-id="47018-183">Also, some parameters might be secure parameters you don't want tooappear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="47018-184">Parameters en beveiligde parameters gebruiken</span><span class="sxs-lookup"><span data-stu-id="47018-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="47018-185">tooaccess Hallo waarde van een resourceparameter tijdens runtime hello [werkstroom definition language](http://aka.ms/logicappsdocs) biedt een `@parameters()` bewerking.</span><span class="sxs-lookup"><span data-stu-id="47018-185">tooaccess hello value of a resource parameter at runtime, hello [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="47018-186">U kunt ook [parameters opgeven in de sjabloon voor de implementatie van Hallo resource](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="47018-186">Also, you can [specify parameters in hello resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="47018-187">Maar als u Hallo parametertype als opgeeft `securestring`, Hallo-parameter niet geretourneerd met de rest van de resourcedefinitie Hallo Hallo en niet toegankelijk door Hallo resource na implementatie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="47018-187">But if you specify hello parameter type as `securestring`, hello parameter won't be returned with hello rest of hello resource definition, and won't be accessible by viewing hello resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="47018-188">Als de parameter wordt gebruikt in Hallo headers of de hoofdtekst van een aanvraag, Hallo parameter mogelijk zichtbaar via Hallo uitvoeren geschiedenis en uitgaande HTTP-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="47018-188">If your parameter is used in hello headers or body of a request, hello parameter might be visible by accessing hello run history and outgoing HTTP request.</span></span> <span data-ttu-id="47018-189">Zorg ervoor dat tooset uw beleid voor toegang tot inhoud dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="47018-189">Make sure tooset your content access policies accordingly.</span></span>
> <span data-ttu-id="47018-190">Autorisatie-header zijn nooit zichtbaar via in- of uitgangen.</span><span class="sxs-lookup"><span data-stu-id="47018-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="47018-191">Als er Hallo geheim wordt gebruikt, is Hallo geheim dus niet worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="47018-191">So if hello secret is being used there, hello secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="47018-192">Resource-implementatiesjabloon met geheimen</span><span class="sxs-lookup"><span data-stu-id="47018-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="47018-193">Hallo volgende voorbeeld ziet u een implementatie die verwijst naar een veilige parameter van het `secret` tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="47018-193">hello following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="47018-194">U kan Hallo omgevingswaarde voor Hallo opgeven in een afzonderlijke parameterbestand `secret`, of gebruik [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve geheimen op tijd implementeren.</span><span class="sxs-lookup"><span data-stu-id="47018-194">In a separate parameters file, you could specify hello environment value for hello `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) tooretrieve secrets at deploy time.</span></span>

``` json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "secretDeploymentParam": {
      "type": "securestring"
    }
  },
  "variables": {},
  "resources": [
    {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
        "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "actions": {
            "Call_External_API": {
              "type": "http",
              "inputs": {
                "headers": {
                  "Authorization": "@parameters('secret')"
                },
                "body": "This is hello request"
              },
              "runAfter": {}
            }
          },
          "parameters": {
            "secret": {
              "type": "SecureString"
            }
          },
          "triggers": {
            "manual": {
              "type": "Request",
              "kind": "Http",
              "inputs": {
                "schema": {}
              }
            }
          },
          "contentVersion": "1.0.0.0",
          "outputs": {}
        },
        "parameters": {
          "secret": {
            "value": "[parameters('secretDeploymentParam')]"
          }
        }
      }
    }
  ],
  "outputs": {}
}
```

## <a name="secure-access-tooservices-receiving-requests-from-a-workflow"></a><span data-ttu-id="47018-195">Toegang tot beveiligde tooservices ontvangende aanvragen van een werkstroom</span><span class="sxs-lookup"><span data-stu-id="47018-195">Secure access tooservices receiving requests from a workflow</span></span>

<span data-ttu-id="47018-196">Er zijn veel manieren toohelp veilig dat eindpunt Hallo logic Apps moet tooaccess.</span><span class="sxs-lookup"><span data-stu-id="47018-196">There are many ways toohelp secure any endpoint hello logic app needs tooaccess.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="47018-197">Met behulp van verificatie voor uitgaande aanvragen</span><span class="sxs-lookup"><span data-stu-id="47018-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="47018-198">Als u werkt met een HTTP-, HTTP + Swagger (Open API) of Webhook actie, kunt u toevoegen toohello verificatieaanvraag wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="47018-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication toohello request being sent.</span></span> <span data-ttu-id="47018-199">U kunt opnemen basisverificatie, verificatie via certificaat of Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="47018-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="47018-200">Meer informatie over hoe tooconfigure deze verificatie vindt [in dit artikel](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="47018-200">Details on how tooconfigure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-toologic-app-ip-addresses"></a><span data-ttu-id="47018-201">Beperken van toegang toologic app IP-adressen</span><span class="sxs-lookup"><span data-stu-id="47018-201">Restricting access toologic app IP addresses</span></span>

<span data-ttu-id="47018-202">Alle aanroepen vanuit logic apps is afkomstig van een specifieke set IP-adressen per regio.</span><span class="sxs-lookup"><span data-stu-id="47018-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="47018-203">U kunt ook aanvullende filters toevoegen tooonly accepteren van aanvragen van het aangewezen IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="47018-203">You can add additional filtering tooonly accept requests from those designated IP addresses.</span></span> <span data-ttu-id="47018-204">Zie voor een lijst van deze IP-adressen, [logic app en -configuratie](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="47018-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="47018-205">On-premises connectiviteit</span><span class="sxs-lookup"><span data-stu-id="47018-205">On-premises connectivity</span></span>

<span data-ttu-id="47018-206">Logische apps bieden integratie met verschillende services tooprovide veilige en betrouwbare lokale communicatie.</span><span class="sxs-lookup"><span data-stu-id="47018-206">Logic apps provide integration with several services tooprovide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="47018-207">On-premises gegevensgateway</span><span class="sxs-lookup"><span data-stu-id="47018-207">On-premises data gateway</span></span>

<span data-ttu-id="47018-208">Veel beheerde connectors voor logic apps bieden beveiligde verbindingen tooon-premises systemen, met inbegrip van bestandssysteem, SQL, SharePoint, DB2 en meer.</span><span class="sxs-lookup"><span data-stu-id="47018-208">Many managed connectors for logic apps provide secure connectivity tooon-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="47018-209">Hallo gateway doorstuurt gegevens van lokale bronnen op gecodeerde kanalen via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="47018-209">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="47018-210">Al het verkeer afkomstig is als beveiligde uitgaand verkeer van Hallo gateway agent.</span><span class="sxs-lookup"><span data-stu-id="47018-210">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="47018-211">Meer informatie over [de werking van de gegevensgateway Hallo](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="47018-211">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="47018-212">Azure API Management</span><span class="sxs-lookup"><span data-stu-id="47018-212">Azure API Management</span></span>

<span data-ttu-id="47018-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) heeft lokale connectiviteitsopties, met inbegrip van site-naar-site-VPN en ExpressRoute-integratie voor beveiligde proxy en communicatie tooon-premises systemen.</span><span class="sxs-lookup"><span data-stu-id="47018-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication tooon-premises systems.</span></span> <span data-ttu-id="47018-214">In Hallo Logic App-ontwerper, kunt u snel een API blootgesteld aan Azure API Management binnen een werkstroom die snelle toegang tooon-premises systemen selecteren.</span><span class="sxs-lookup"><span data-stu-id="47018-214">In hello Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access tooon-premises systems.</span></span>

#### <a name="hybrid-connections-from-azure-app-service"></a><span data-ttu-id="47018-215">Hybride verbindingen van Azure App Service</span><span class="sxs-lookup"><span data-stu-id="47018-215">Hybrid connections from Azure App Service</span></span>

<span data-ttu-id="47018-216">U kunt Hallo lokale hybride verbinding functie gebruiken voor Azure-API en Web-apps toocommunicate on-premises.</span><span class="sxs-lookup"><span data-stu-id="47018-216">You can use hello on-premises hybrid connection feature for Azure API and Web apps toocommunicate on-premises.</span></span>  <span data-ttu-id="47018-217">Meer informatie over hybride verbindingen en hoe tooconfigure vindt [in dit artikel](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="47018-217">Details on hybrid connections and how tooconfigure can be found [in this article](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="47018-218">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="47018-218">Next steps</span></span>
[<span data-ttu-id="47018-219">Maken van een sjabloon voor de implementatie</span><span class="sxs-lookup"><span data-stu-id="47018-219">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="47018-220">Afhandeling van uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="47018-220">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="47018-221">Uw logische apps bewaken</span><span class="sxs-lookup"><span data-stu-id="47018-221">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="47018-222">Logic app fouten en problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="47018-222">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  

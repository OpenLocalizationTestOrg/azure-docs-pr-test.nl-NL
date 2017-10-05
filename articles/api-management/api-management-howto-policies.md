---
title: Beleid in Azure API Management | Microsoft Docs
description: Informatie over het maken, bewerken en configureren van beleid in API Management.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="faeaa-103">Beleid in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="faeaa-103">Policies in Azure API Management</span></span>
<span data-ttu-id="faeaa-104">In Azure API Management zijn-beleidsregels een krachtige mogelijkheid van het systeem waarmee de uitgever het gedrag van de API via configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="faeaa-105">Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op de aanvraag of antwoord van een API.</span><span class="sxs-lookup"><span data-stu-id="faeaa-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="faeaa-106">Populaire instructies omvatten Indelingsconversie van XML in JSON en snelheidsbeperking als u wilt beperken, de hoeveelheid inkomende aanroepen van een ontwikkelaar aanroepen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="faeaa-107">Veel meer beleidsregels zijn gebruiksklaar beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="faeaa-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="faeaa-108">Zie de [beleidsverwijzing] [ Policy Reference] voor een volledige lijst met beleidsverklaringen en de bijbehorende instellingen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="faeaa-109">Beleidsregels worden toegepast binnen de gateway die de consument API en de beheerde API tussen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="faeaa-110">De gateway ontvangt van alle aanvragen en meestal doorsturen ervan naar de onderliggende API ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="faeaa-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="faeaa-111">Een beleid kan echter wijzigingen toepassen op zowel de binnenkomende aanvraag en het uitgaande antwoord.</span><span class="sxs-lookup"><span data-stu-id="faeaa-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="faeaa-112">Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels, tenzij het beleid iets anders aangeeft.</span><span class="sxs-lookup"><span data-stu-id="faeaa-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="faeaa-113">Sommige beleidsregels, zoals de [transportbesturing] [ Control flow] en [variabele instellen] [ Set variable] beleid is gebaseerd op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="faeaa-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="faeaa-114">Zie voor meer informatie [Geavanceerde beleidsregels] [ Advanced policies] en [beleidsexpressies][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="faeaa-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="faeaa-115"><a name="scopes"></a>Beleid configureren</span><span class="sxs-lookup"><span data-stu-id="faeaa-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="faeaa-116">Beleid kan worden geconfigureerd globaal of in het bereik van een [Product][Product], [API] [ API] of [bewerking][Operation].</span><span class="sxs-lookup"><span data-stu-id="faeaa-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="faeaa-117">Een beleid wilt configureren, gaat u naar de beleid-editor in de publicatieportal.</span><span class="sxs-lookup"><span data-stu-id="faeaa-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Menu beleid][policies-menu]

<span data-ttu-id="faeaa-119">De editor beleid bestaat uit drie gedeelten: het beleidsbereik (boven), de beleidsdefinitie waarbij beleid (links) worden bewerkt en de instructies lijst (rechts):</span><span class="sxs-lookup"><span data-stu-id="faeaa-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Beleid-editor][policies-editor]

<span data-ttu-id="faeaa-121">U moet het bereik waarvoor het beleid moet toepassen selecteren om te beginnen met een beleid te configureren.</span><span class="sxs-lookup"><span data-stu-id="faeaa-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="faeaa-122">In de onderstaande schermafbeelding de **Starter** product is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="faeaa-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="faeaa-123">Houd er rekening mee dat het vierkante symbool naast de naam van het beleid geeft een beleid is al toegepast op dit niveau.</span><span class="sxs-lookup"><span data-stu-id="faeaa-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Bereik][policies-scope]

<span data-ttu-id="faeaa-125">Omdat er al een beleid is toegepast, wordt de configuratie wordt weergegeven in de weergave van de definitie.</span><span class="sxs-lookup"><span data-stu-id="faeaa-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Configureren][policies-configure]

<span data-ttu-id="faeaa-127">Het beleid wordt weergegeven in de alleen-lezen in eerste instantie.</span><span class="sxs-lookup"><span data-stu-id="faeaa-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="faeaa-128">Om te bewerken van het definitie klikt u op de **beleid configureren** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Bewerken][policies-edit]

<span data-ttu-id="faeaa-130">De beleidsdefinitie is een eenvoudige XML-document dat wordt een reeks binnenkomend en uitgaand instructies beschreven.</span><span class="sxs-lookup"><span data-stu-id="faeaa-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="faeaa-131">Het XML-bestand kan worden bewerkt rechtstreeks in het definitievenster.</span><span class="sxs-lookup"><span data-stu-id="faeaa-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="faeaa-132">Een lijst van de instructies vindt u aan de rechterkant en instructies van toepassing op het huidige bereik zijn ingeschakeld en geselecteerd. zoals blijkt uit de **limiet aanroepen snelheid** -instructie in de bovenstaande schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="faeaa-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="faeaa-133">Te klikken op een instructie ingeschakeld, wordt de juiste XML op de locatie van de cursor in de weergave definitie toevoegen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="faeaa-134">Als het beleid dat u wilt toevoegen is niet ingeschakeld, zorg ervoor dat u in het juiste bereik voor dat beleid.</span><span class="sxs-lookup"><span data-stu-id="faeaa-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="faeaa-135">Elke instructie beleid is ontworpen voor gebruik in bepaalde scopes en beleid-secties.</span><span class="sxs-lookup"><span data-stu-id="faeaa-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="faeaa-136">Als u wilt controleren in de secties van beleid en de bereiken voor een beleid, Controleer de **gebruik** sectie voor dat beleid in de [beleidsverwijzing][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="faeaa-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="faeaa-137">Een volledige lijst met beleidsverklaringen en hun instellingen zijn beschikbaar in de [beleidsverwijzing][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="faeaa-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="faeaa-138">Bijvoorbeeld, als u wilt toevoegen van een nieuwe statusverklaring om te beperken van binnenkomende aanvragen tot het opgegeven IP-adressen, plaats de cursor net binnen de inhoud van de `inbound` XML-element en klik op de **beperken aanroeper IP-adressen** instructie.</span><span class="sxs-lookup"><span data-stu-id="faeaa-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Beleid voor softwarebeperking][policies-restrict]

<span data-ttu-id="faeaa-140">Hiermee voegt u toe een XML-fragment naar de `inbound` element dat biedt richtlijnen voor het configureren van de instructie.</span><span class="sxs-lookup"><span data-stu-id="faeaa-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="faeaa-141">Beperken van binnenkomende aanvragen en accepteert alleen die uit een IP-adres van 1.2.3.4 het XML-bestand als volgt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="faeaa-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Opslaan][policies-save]

<span data-ttu-id="faeaa-143">Als u klaar voor het configureren van de instructies voor het beleid, klikt u op **opslaan** en de wijzigingen wordt doorgegeven aan de API Management-gateway van onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="faeaa-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="faeaa-144"><a name="sections"></a>Understanding beleidsconfiguratie</span><span class="sxs-lookup"><span data-stu-id="faeaa-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="faeaa-145">Een beleid is een reeks instructies die worden uitgevoerd om een antwoord en aanvragen.</span><span class="sxs-lookup"><span data-stu-id="faeaa-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="faeaa-146">De configuratie op de juiste wijze is onderverdeeld in `inbound`, `backend`, `outbound`, en `on-error` zoals weergegeven in de configuratie van de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="faeaa-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="faeaa-147">Als er een fout opgetreden tijdens het verwerken van een aanvraag, alle overige stappen in de `inbound`, `backend`, of `outbound` secties worden overgeslagen en uitvoering gaat u naar de instructies in de `on-error` sectie.</span><span class="sxs-lookup"><span data-stu-id="faeaa-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="faeaa-148">Door het plaatsen van beleidsverklaringen in de `on-error` sectie kunt u de fout bekijken met behulp van de `context.LastError` eigenschap, controleren en aanpassen van de fout antwoord via de `set-body` -beleid, en configureer wat er gebeurt als een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="faeaa-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="faeaa-149">Er zijn foutcodes voor ingebouwde stappen en voor fouten die tijdens de verwerking van beleid voor instructies optreden.</span><span class="sxs-lookup"><span data-stu-id="faeaa-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="faeaa-150">Zie voor meer informatie [foutafhandeling in API Management-beleidsregels](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="faeaa-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="faeaa-151">Aangezien beleidsregels kunnen worden opgegeven op verschillende niveaus (globale, product, api en bewerking) biedt de configuratie een manier om de volgorde waarin de beleidsdefinitie-instructies met betrekking tot het beleid van de bovenliggende uitvoeren opgeven.</span><span class="sxs-lookup"><span data-stu-id="faeaa-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="faeaa-152">Beleid scopes worden geëvalueerd in de volgende volgorde.</span><span class="sxs-lookup"><span data-stu-id="faeaa-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="faeaa-153">Globaal bereik</span><span class="sxs-lookup"><span data-stu-id="faeaa-153">Global scope</span></span>
2. <span data-ttu-id="faeaa-154">Product-bereik</span><span class="sxs-lookup"><span data-stu-id="faeaa-154">Product scope</span></span>
3. <span data-ttu-id="faeaa-155">API-bereik</span><span class="sxs-lookup"><span data-stu-id="faeaa-155">API scope</span></span>
4. <span data-ttu-id="faeaa-156">Bewerkingsbereik</span><span class="sxs-lookup"><span data-stu-id="faeaa-156">Operation scope</span></span>

<span data-ttu-id="faeaa-157">De instructies in deze worden geëvalueerd op basis van de plaatsing van de `base` element, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="faeaa-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="faeaa-158">Globaal beleid heeft geen bovenliggend element beleid en het gebruik van de `<base>` -element in het heeft geen effect.</span><span class="sxs-lookup"><span data-stu-id="faeaa-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="faeaa-159">Bijvoorbeeld, als u een beleid op het globale niveau en een beleid dat is geconfigureerd voor een API hebt, klikt u vervolgens wanneer die bepaalde API wordt gebruikt beide beleidsregels gelden.</span><span class="sxs-lookup"><span data-stu-id="faeaa-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="faeaa-160">API Management kunt u deterministische ordening van gecombineerde beleidsverklaringen via het base-element.</span><span class="sxs-lookup"><span data-stu-id="faeaa-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="faeaa-161">In het bovenstaande voorbeeld beleidsdefinitie de `cross-domain` instructie zou worden uitgevoerd voordat een hogere beleid die op zijn beurt worden gevolgd door de `find-and-replace` beleid.</span><span class="sxs-lookup"><span data-stu-id="faeaa-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="faeaa-162">Klik op een overzicht van het beleid in het huidige bereik in de beleidseditor **herberekenen effectief beleid voor de geselecteerde scope**.</span><span class="sxs-lookup"><span data-stu-id="faeaa-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="faeaa-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="faeaa-163">Next steps</span></span>
<span data-ttu-id="faeaa-164">Bekijk na video op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="faeaa-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png

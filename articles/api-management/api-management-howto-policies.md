---
title: aaaPolicies in Azure API Management | Microsoft Docs
description: Ontdek hoe toocreate, bewerken en configureren van beleid in API Management.
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
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="f2c25-103">Beleid in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="f2c25-103">Policies in Azure API Management</span></span>
<span data-ttu-id="f2c25-104">In Azure API Management zijn-beleidsregels een krachtige functie Hallo-systeem dat Hallo publisher toochange Hallo gedrag Hallo API via configuratie toestaan.</span><span class="sxs-lookup"><span data-stu-id="f2c25-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="f2c25-105">Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API.</span><span class="sxs-lookup"><span data-stu-id="f2c25-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="f2c25-106">Populaire instructies omvatten Indelingsconversie van XML-tooJSON en snelheidsbeperking toorestrict Hallo hoeveelheid inkomende aanroepen van een ontwikkelaar aanroepen.</span><span class="sxs-lookup"><span data-stu-id="f2c25-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="f2c25-107">Veel meer beleidsregels zijn out of box Hallo beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="f2c25-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="f2c25-108">Zie Hallo [beleidsverwijzing] [ Policy Reference] voor een volledige lijst met beleidsverklaringen en de bijbehorende instellingen.</span><span class="sxs-lookup"><span data-stu-id="f2c25-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="f2c25-109">Beleidsregels worden toegepast binnen bevindt zich tussen Hallo API consumer en Hallo managed API Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="f2c25-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="f2c25-110">Hallo gateway ontvangt alle aanvragen en stuurt ze ongewijzigd meestal door toohello onderliggende API.</span><span class="sxs-lookup"><span data-stu-id="f2c25-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="f2c25-111">Een beleid kunt echter wijzigingen tooboth Hallo binnenkomende aanvraag en het uitgaande antwoord toepassen.</span><span class="sxs-lookup"><span data-stu-id="f2c25-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="f2c25-112">Beleidsexpressies kunnen worden gebruikt als kenmerkwaarden of tekstwaarden in API Management-beleidsregels hello, tenzij Hallo beleid iets anders aangeeft.</span><span class="sxs-lookup"><span data-stu-id="f2c25-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="f2c25-113">Sommige beleidsregels zoals Hallo [transportbesturing] [ Control flow] en [variabele instellen] [ Set variable] beleid is gebaseerd op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="f2c25-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="f2c25-114">Zie voor meer informatie [Geavanceerde beleidsregels] [ Advanced policies] en [beleidsexpressies][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="f2c25-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="f2c25-115"><a name="scopes"></a>Hoe tooconfigure beleid</span><span class="sxs-lookup"><span data-stu-id="f2c25-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="f2c25-116">Beleid kan worden geconfigureerd globaal of Hallo bereik van een [Product][Product], [API] [ API] of [bewerking] [Operation].</span><span class="sxs-lookup"><span data-stu-id="f2c25-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="f2c25-117">tooconfigure een beleid, gaat u toohello beleid editor in de publicatieportal Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2c25-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Menu beleid][policies-menu]

<span data-ttu-id="f2c25-119">Hallo beleidsregels editor bestaat uit drie gedeelten: Hallo bereik (boven), Hallo beleid beleidsdefinitie waarbij beleid (links) worden bewerkt en Hallo instructies lijst (rechts):</span><span class="sxs-lookup"><span data-stu-id="f2c25-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Beleid-editor][policies-editor]

<span data-ttu-id="f2c25-121">toobegin een beleid die moet u eerst Hallo bereik welke Hallo beleid moet toepassen selecteren te configureren.</span><span class="sxs-lookup"><span data-stu-id="f2c25-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="f2c25-122">In de schermafbeelding hieronder Hallo Hallo **Starter** product is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f2c25-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="f2c25-123">Houd er rekening mee dat Hallo vierkante symbool volgende toohello beleidsnaam geeft aan dat een beleid al op dit niveau toegepast is.</span><span class="sxs-lookup"><span data-stu-id="f2c25-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Bereik][policies-scope]

<span data-ttu-id="f2c25-125">Omdat er al een beleid is toegepast, wordt in Hallo definitie weergave Hallo configuratie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f2c25-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![Configureren][policies-configure]

<span data-ttu-id="f2c25-127">Hallo-beleid wordt weergegeven in de alleen-lezen in eerste instantie.</span><span class="sxs-lookup"><span data-stu-id="f2c25-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="f2c25-128">Klik in volgorde tooedit Hallo definitie op Hallo **beleid configureren** in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="f2c25-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Bewerken][policies-edit]

<span data-ttu-id="f2c25-130">Hallo beleidsdefinitie is een eenvoudige XML-document dat wordt een reeks binnenkomend en uitgaand instructies beschreven.</span><span class="sxs-lookup"><span data-stu-id="f2c25-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="f2c25-131">Hallo XML kan rechtstreeks in Hallo definitievenster worden bewerkt.</span><span class="sxs-lookup"><span data-stu-id="f2c25-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="f2c25-132">Een lijst van de instructies wordt verstrekt toohello rechts en instructies van toepassing toohello huidige bereik zijn ingeschakeld en geselecteerd. zoals blijkt uit Hallo **limiet aanroepen snelheid** instructie in de bovenstaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2c25-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="f2c25-133">Te klikken op een ingeschakelde instructie toevoegt juiste XML op Hallo-locatie van de cursor in de weergave typedefinitie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="f2c25-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="f2c25-134">Als het Hallo-beleid dat u wilt dat tooadd niet is ingeschakeld, zorg ervoor dat u in de juiste bereik Hallo voor dat beleid.</span><span class="sxs-lookup"><span data-stu-id="f2c25-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="f2c25-135">Elke instructie beleid is ontworpen voor gebruik in bepaalde scopes en beleid-secties.</span><span class="sxs-lookup"><span data-stu-id="f2c25-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="f2c25-136">tooreview hello beleid secties en bereiken voor een beleid controleren Hallo **gebruik** sectie voor dat beleid in Hallo [beleidsverwijzing][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="f2c25-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="f2c25-137">Een volledige lijst met beleidsverklaringen en hun instellingen zijn beschikbaar in Hallo [beleidsverwijzing][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="f2c25-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="f2c25-138">Bijvoorbeeld, tooadd een nieuwe instructie toorestrict binnenkomende aanvragen toospecified IP-adressen, plaatst u Hallo cursor net binnen Hallo inhoud Hallo `inbound` XML-element en klik op Hallo **beperken aanroeper IP-adressen** instructie.</span><span class="sxs-lookup"><span data-stu-id="f2c25-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Beleid voor softwarebeperking][policies-restrict]

<span data-ttu-id="f2c25-140">Hiermee voegt u toe een XML-fragment toohello `inbound` element dat richtlijnen biedt voor hoe tooconfigure Hallo instructie.</span><span class="sxs-lookup"><span data-stu-id="f2c25-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="f2c25-141">toolimit binnenkomende aanvragen en accepteert alleen die uit een IP-adres van 1.2.3.4 Hallo XML als volgt wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f2c25-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Opslaan][policies-save]

<span data-ttu-id="f2c25-143">Als u klaar Hallo-instructies voor het Hallo-beleid configureren, klikt u op **opslaan** en Hallo wijzigingen wordt onmiddellijk doorgegeven toohello API Management gateway.</span><span class="sxs-lookup"><span data-stu-id="f2c25-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="f2c25-144"><a name="sections"></a>Understanding beleidsconfiguratie</span><span class="sxs-lookup"><span data-stu-id="f2c25-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="f2c25-145">Een beleid is een reeks instructies die worden uitgevoerd om een antwoord en aanvragen.</span><span class="sxs-lookup"><span data-stu-id="f2c25-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="f2c25-146">Hallo-configuratie op de juiste wijze is onderverdeeld in `inbound`, `backend`, `outbound`, en `on-error` gedeelten in Hallo na configuratie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f2c25-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="f2c25-147">Als er een fout opgetreden tijdens het verwerken van een aanvraag hello, alle overige stappen in Hallo `inbound`, `backend`, of `outbound` secties worden overgeslagen en uitvoering aan de slag gaat toohello instructies in Hallo `on-error` sectie.</span><span class="sxs-lookup"><span data-stu-id="f2c25-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="f2c25-148">Door het plaatsen van beleidsverklaringen in Hallo `on-error` sectie kunt u Hallo fout bekijken met behulp van Hallo `context.LastError` eigenschap, controleren en aanpassen van Hallo fout antwoord aan de hand van Hallo `set-body` beleid, en configureren van wat er gebeurt als een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="f2c25-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="f2c25-149">Er zijn foutcodes voor ingebouwde stappen en voor fouten die tijdens het Hallo-verwerking van beleid voor instructies optreden.</span><span class="sxs-lookup"><span data-stu-id="f2c25-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="f2c25-150">Zie voor meer informatie [foutafhandeling in API Management-beleidsregels](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="f2c25-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="f2c25-151">Omdat het beleid kunnen worden opgegeven op verschillende niveaus (globale, product, api en bewerking) biedt Hallo-configuratie een manier voor u toospecify Hallo volgorde waarin instructies Hallo beleid definition met het beleid ten opzichte van toohello bovenliggende uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f2c25-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="f2c25-152">Beleid scopes worden in Hallo volgorde geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="f2c25-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="f2c25-153">Globaal bereik</span><span class="sxs-lookup"><span data-stu-id="f2c25-153">Global scope</span></span>
2. <span data-ttu-id="f2c25-154">Product-bereik</span><span class="sxs-lookup"><span data-stu-id="f2c25-154">Product scope</span></span>
3. <span data-ttu-id="f2c25-155">API-bereik</span><span class="sxs-lookup"><span data-stu-id="f2c25-155">API scope</span></span>
4. <span data-ttu-id="f2c25-156">Bewerkingsbereik</span><span class="sxs-lookup"><span data-stu-id="f2c25-156">Operation scope</span></span>

<span data-ttu-id="f2c25-157">Hallo instructies in deze worden beoordeeld volgens toohello plaatsing van Hallo `base` element, indien aanwezig.</span><span class="sxs-lookup"><span data-stu-id="f2c25-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="f2c25-158">Globaal beleid heeft geen bovenliggende beleid en het gebruik van Hallo `<base>` -element in het heeft geen effect.</span><span class="sxs-lookup"><span data-stu-id="f2c25-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="f2c25-159">Bijvoorbeeld, als u een beleid op Hallo globale niveau en een beleid dat is geconfigureerd voor een API hebt, klikt u vervolgens wanneer die bepaalde API wordt gebruikt beide beleidsregels gelden.</span><span class="sxs-lookup"><span data-stu-id="f2c25-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="f2c25-160">API Management kunt u deterministische ordening van gecombineerde beleidsverklaringen via Hallo base-element.</span><span class="sxs-lookup"><span data-stu-id="f2c25-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="f2c25-161">Hallo in Hallo voorbeeld beleidsdefinitie hierboven, `cross-domain` instructie zou worden uitgevoerd voordat een hogere beleid die op zijn beurt worden gevolgd door Hallo `find-and-replace` beleid.</span><span class="sxs-lookup"><span data-stu-id="f2c25-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="f2c25-162">toosee Hallo-beleid in het huidige bereik Hallo in de beleidseditor hello, klikt u op **herberekenen effectief beleid voor de geselecteerde scope**.</span><span class="sxs-lookup"><span data-stu-id="f2c25-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2c25-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2c25-163">Next steps</span></span>
<span data-ttu-id="f2c25-164">Bekijk na video op beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="f2c25-164">Check out following video on policy expressions.</span></span>

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

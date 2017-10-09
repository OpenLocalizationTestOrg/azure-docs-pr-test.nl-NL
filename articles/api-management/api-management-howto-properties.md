---
title: aaaHow toouse eigenschappen in Azure API Management-beleidsregels
description: Meer informatie over hoe toouse eigenschappen in Azure API Management-beleidsregels.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="70fe3-103">Hoe toouse eigenschappen in Azure API Management-beleidsregels</span><span class="sxs-lookup"><span data-stu-id="70fe3-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="70fe3-104">API Management-beleidsregels zijn een krachtige mogelijkheid Hallo-systeem dat Hallo publisher toochange Hallo gedrag Hallo API via configuratie toestaan.</span><span class="sxs-lookup"><span data-stu-id="70fe3-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="70fe3-105">Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op Hallo aanvraag of antwoord van een API.</span><span class="sxs-lookup"><span data-stu-id="70fe3-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="70fe3-106">Beleidsverklaringen kunnen worden samengesteld met behulp van letterlijke tekstwaarden, beleidsexpressies en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="70fe3-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="70fe3-107">Elk exemplaar van API Management-service heeft een verzameling eigenschappen van sleutel/waarde-paren die globale toohello service-exemplaar zijn.</span><span class="sxs-lookup"><span data-stu-id="70fe3-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="70fe3-108">Deze eigenschappen kunnen gebruikte toomanage constante string-waarden worden voor alle configuratie-API en beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="70fe3-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="70fe3-109">Elke eigenschap heeft Hallo kenmerken te volgen.</span><span class="sxs-lookup"><span data-stu-id="70fe3-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="70fe3-110">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="70fe3-110">Attribute</span></span> | <span data-ttu-id="70fe3-111">Type</span><span class="sxs-lookup"><span data-stu-id="70fe3-111">Type</span></span> | <span data-ttu-id="70fe3-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="70fe3-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="70fe3-113">Naam</span><span class="sxs-lookup"><span data-stu-id="70fe3-113">Name</span></span> |<span data-ttu-id="70fe3-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="70fe3-114">string</span></span> |<span data-ttu-id="70fe3-115">Hallo-naam van Hallo-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="70fe3-115">hello name of hello property.</span></span> <span data-ttu-id="70fe3-116">Mogelijk bevatten alleen letters, cijfers, periode, streepjes en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="70fe3-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="70fe3-117">Waarde</span><span class="sxs-lookup"><span data-stu-id="70fe3-117">Value</span></span> |<span data-ttu-id="70fe3-118">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="70fe3-118">string</span></span> |<span data-ttu-id="70fe3-119">Hallo-waarde van Hallo-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="70fe3-119">hello value of hello property.</span></span> <span data-ttu-id="70fe3-120">Het is niet leeg zijn of alleen witruimte bevatten.</span><span class="sxs-lookup"><span data-stu-id="70fe3-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="70fe3-121">Geheim</span><span class="sxs-lookup"><span data-stu-id="70fe3-121">Secret</span></span> |<span data-ttu-id="70fe3-122">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="70fe3-122">boolean</span></span> |<span data-ttu-id="70fe3-123">Bepaalt of Hallo-waarde een geheim is en moet worden versleuteld of niet.</span><span class="sxs-lookup"><span data-stu-id="70fe3-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="70fe3-124">Tags</span><span class="sxs-lookup"><span data-stu-id="70fe3-124">Tags</span></span> |<span data-ttu-id="70fe3-125">Matrix van tekenreeks</span><span class="sxs-lookup"><span data-stu-id="70fe3-125">array of string</span></span> |<span data-ttu-id="70fe3-126">Optioneel tags die de gebruikte toofilter Hallo eigenschappenlijst kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="70fe3-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="70fe3-127">Eigenschappen zijn geconfigureerd in de publicatieportal Hallo op Hallo **eigenschappen** tabblad. In de Hallo voorbeeld te volgen, zijn drie eigenschappen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="70fe3-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![Eigenschappen][api-management-properties]

<span data-ttu-id="70fe3-129">Eigenschapswaarden letterlijke tekenreeksen kunnen bevatten en [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="70fe3-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="70fe3-130">Hallo volgende tabel toont Hallo vorige drie Voorbeeld eigenschappen en hun kenmerken.</span><span class="sxs-lookup"><span data-stu-id="70fe3-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="70fe3-131">waarde van Hallo `ExpressionProperty` is een beleidsexpressie die resulteert in een tekenreeks met Hallo de huidige datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="70fe3-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="70fe3-132">Hallo eigenschap `ContosoHeaderValue` is gemarkeerd als een geheim, zodat de waarde wordt niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70fe3-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="70fe3-133">Naam</span><span class="sxs-lookup"><span data-stu-id="70fe3-133">Name</span></span> | <span data-ttu-id="70fe3-134">Waarde</span><span class="sxs-lookup"><span data-stu-id="70fe3-134">Value</span></span> | <span data-ttu-id="70fe3-135">Geheim</span><span class="sxs-lookup"><span data-stu-id="70fe3-135">Secret</span></span> | <span data-ttu-id="70fe3-136">Tags</span><span class="sxs-lookup"><span data-stu-id="70fe3-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="70fe3-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="70fe3-137">ContosoHeader</span></span> |<span data-ttu-id="70fe3-138">trackingId</span><span class="sxs-lookup"><span data-stu-id="70fe3-138">TrackingId</span></span> |<span data-ttu-id="70fe3-139">False</span><span class="sxs-lookup"><span data-stu-id="70fe3-139">False</span></span> |<span data-ttu-id="70fe3-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="70fe3-140">Contoso</span></span> |
| <span data-ttu-id="70fe3-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="70fe3-141">ContosoHeaderValue</span></span> |<span data-ttu-id="70fe3-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="70fe3-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="70fe3-143">True</span><span class="sxs-lookup"><span data-stu-id="70fe3-143">True</span></span> |<span data-ttu-id="70fe3-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="70fe3-144">Contoso</span></span> |
| <span data-ttu-id="70fe3-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="70fe3-145">ExpressionProperty</span></span> |<span data-ttu-id="70fe3-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="70fe3-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="70fe3-147">False</span><span class="sxs-lookup"><span data-stu-id="70fe3-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="70fe3-148">een eigenschap toouse</span><span class="sxs-lookup"><span data-stu-id="70fe3-148">toouse a property</span></span>
<span data-ttu-id="70fe3-149">een eigenschap in een beleid toouse, plaats Hallo eigenschapsnaam in een dubbele paar accolades, zoals `{{ContosoHeader}}`, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="70fe3-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="70fe3-150">In dit voorbeeld `ContosoHeader` wordt gebruikt als Hallo-naam van een kop in een `set-header` beleid, en `ContosoHeaderValue` wordt gebruikt als Hallo-waarde van deze header.</span><span class="sxs-lookup"><span data-stu-id="70fe3-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="70fe3-151">Wanneer dit beleid wordt beoordeeld tijdens een aanvraag of antwoord toohello API Management-gateway, `{{ContosoHeader}}` en `{{ContosoHeaderValue}}` worden vervangen door hun respectieve eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="70fe3-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="70fe3-152">Eigenschappen kunnen worden gebruikt als volledige kenmerk of elementwaarden zoals weergegeven in het vorige voorbeeld hello, maar ze kunnen ook worden ingevoegd in of in combinatie met een deel van een expressie letterlijke tekst zoals weergegeven in het volgende voorbeeld Hallo:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="70fe3-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="70fe3-153">Eigenschappen bevatten ook beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="70fe3-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="70fe3-154">Hallo in Hallo voorbeeld te volgen, `ExpressionProperty` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70fe3-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="70fe3-155">Wanneer dit beleid wordt beoordeeld `{{ExpressionProperty}}` is vervangen door de waarde ervan: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="70fe3-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="70fe3-156">Aangezien Hallo-waarde een beleidsexpressie is, Hallo expressie wordt geëvalueerd en Hallo beleid doorgegaan met de uitvoering ervan.</span><span class="sxs-lookup"><span data-stu-id="70fe3-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="70fe3-157">U kunt dit uit in de ontwikkelaarsportal Hallo testen door het aanroepen van een bewerking die een beleid met eigenschappen in het bereik heeft.</span><span class="sxs-lookup"><span data-stu-id="70fe3-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="70fe3-158">In Hallo voorbeeld te volgen, een bewerking is aangeroepen met de twee vorige voorbeeld Hallo `set-header` beleid met eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="70fe3-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="70fe3-159">Houd er rekening mee dat antwoord Hallo bevat twee aangepaste headers die zijn geconfigureerd met beleid van eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="70fe3-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![ontwikkelaarsportal][api-management-send-results]

<span data-ttu-id="70fe3-161">Als u hello bekijkt [API Inspector trace](api-management-howto-api-inspector.md) voor een aanroep die Hallo twee vorige voorbeeld beleidsregels met eigenschappen bevat, ziet u twee Hallo `set-header` beleid met Hallo eigenschapswaarden ingevoegd en de beleidsexpressie Hallo evaluatie voor Hallo-eigenschap die Hallo beleidsexpressie opgenomen.</span><span class="sxs-lookup"><span data-stu-id="70fe3-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![API-Inspector tracering][api-management-api-inspector-trace]

<span data-ttu-id="70fe3-163">Houd er rekening mee dat terwijl eigenschapswaarden beleidsexpressies bevatten kunnen, eigenschapswaarden kunnen geen andere eigenschappen bevatten.</span><span class="sxs-lookup"><span data-stu-id="70fe3-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="70fe3-164">Als tekst met een eigenschapverwijzing wordt gebruikt voor de waarde van een eigenschap, zoals `Property value text {{MyProperty}}`, dat eigenschapverwijzing won't worden vervangen en opgenomen als onderdeel van de eigenschapswaarde Hallo worden.</span><span class="sxs-lookup"><span data-stu-id="70fe3-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="70fe3-165">een eigenschap toocreate</span><span class="sxs-lookup"><span data-stu-id="70fe3-165">toocreate a property</span></span>
<span data-ttu-id="70fe3-166">toocreate een eigenschap, klikt u op **eigenschap toevoegen** op Hallo **eigenschappen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="70fe3-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![Eigenschap toevoegen][api-management-properties-add-property-menu]

<span data-ttu-id="70fe3-168">**Naam** en **waarde** vereiste waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="70fe3-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="70fe3-169">Als de waarde van deze eigenschap een geheim is, controleert u Hallo **dit is een geheim** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="70fe3-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="70fe3-170">Geef een of meer optionele labels toohelp met eigenschappen voor het ordenen en op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="70fe3-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![Eigenschap toevoegen][api-management-properties-add-property]

<span data-ttu-id="70fe3-172">Wanneer een nieuwe eigenschap wordt opgeslagen, Hallo **eigenschap zoeken** textbox is gevuld met de naam van de nieuwe eigenschap Hallo Hallo en de nieuwe eigenschap hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="70fe3-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="70fe3-173">alle eigenschappen, schakelt u toodisplay hello **eigenschap zoeken** textbox en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="70fe3-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Eigenschappen][api-management-properties-property-saved]

<span data-ttu-id="70fe3-175">Zie voor meer informatie over het maken van een eigenschap Hallo REST-API met [maakt u een eigenschap Hallo REST-API met](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="70fe3-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="70fe3-176">een eigenschap tooedit</span><span class="sxs-lookup"><span data-stu-id="70fe3-176">tooedit a property</span></span>
<span data-ttu-id="70fe3-177">tooedit een eigenschap, klikt u op **bewerken** naast Hallo eigenschap tooedit.</span><span class="sxs-lookup"><span data-stu-id="70fe3-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![De eigenschap bewerken][api-management-properties-edit]

<span data-ttu-id="70fe3-179">Breng de gewenste wijzigingen klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="70fe3-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="70fe3-180">Als u de naam van de eigenschap Hallo wijzigt, worden alle beleidsregels die verwijzen naar die eigenschap automatisch bijgewerkt toouse Hallo nieuwe naam.</span><span class="sxs-lookup"><span data-stu-id="70fe3-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![De eigenschap bewerken][api-management-properties-edit-property]

<span data-ttu-id="70fe3-182">Zie voor meer informatie over het bewerken van een eigenschap Hallo REST-API met [bewerken van een eigenschap Hallo REST-API met](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="70fe3-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="70fe3-183">een eigenschap toodelete</span><span class="sxs-lookup"><span data-stu-id="70fe3-183">toodelete a property</span></span>
<span data-ttu-id="70fe3-184">toodelete een eigenschap, klikt u op **verwijderen** naast Hallo eigenschap toodelete.</span><span class="sxs-lookup"><span data-stu-id="70fe3-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![Eigenschap verwijderen][api-management-properties-delete]

<span data-ttu-id="70fe3-186">Klik op **Ja, deze verwijderen** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="70fe3-186">Click **Yes, delete it** tooconfirm.</span></span>

![De verwijdering bevestigen][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="70fe3-188">Als de eigenschap Hallo wordt verwezen door andere beleidsregels, kunt u zich niet toosuccessfully verwijderen als u de eigenschap Hallo verwijdert uit alle beleidsregels die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="70fe3-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="70fe3-189">Zie voor meer informatie over het verwijderen van een eigenschap Hallo REST-API met [verwijderen van een eigenschap Hallo REST-API met](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="70fe3-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="70fe3-190">Eigenschappen toosearch en filter</span><span class="sxs-lookup"><span data-stu-id="70fe3-190">toosearch and filter properties</span></span>
<span data-ttu-id="70fe3-191">Hallo **eigenschappen** tabblad Zoeken en filteren mogelijkheden toohelp beheren van uw eigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="70fe3-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="70fe3-192">toofilter Hallo-eigenschappenlijst met de eigenschapsnaam, voert u een zoekterm in Hallo **eigenschap zoeken** textbox.</span><span class="sxs-lookup"><span data-stu-id="70fe3-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="70fe3-193">alle eigenschappen, schakelt u toodisplay hello **eigenschap zoeken** textbox en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="70fe3-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="70fe3-195">toofilter hello eigenschappenlijst door code-waarden, een of meer labels invoeren in Hallo **filteren op labels** textbox.</span><span class="sxs-lookup"><span data-stu-id="70fe3-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="70fe3-196">alle eigenschappen, schakelt u toodisplay hello **filteren op labels** textbox en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="70fe3-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filteren][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="70fe3-198">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="70fe3-198">Next steps</span></span>
* <span data-ttu-id="70fe3-199">Meer informatie over het werken met beleid</span><span class="sxs-lookup"><span data-stu-id="70fe3-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="70fe3-200">Beleidsregels in API Management</span><span class="sxs-lookup"><span data-stu-id="70fe3-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="70fe3-201">Naslaginformatie over beleidsregels</span><span class="sxs-lookup"><span data-stu-id="70fe3-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="70fe3-202">Beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="70fe3-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="70fe3-203">Bekijk een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="70fe3-203">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png


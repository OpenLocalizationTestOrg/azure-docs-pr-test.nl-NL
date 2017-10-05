---
title: Het gebruik van eigenschappen in Azure API Management-beleidsregels
description: Informatie over het gebruik van eigenschappen in Azure API Management-beleidsregels.
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
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="cdb18-103">Het gebruik van eigenschappen in Azure API Management-beleidsregels</span><span class="sxs-lookup"><span data-stu-id="cdb18-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="cdb18-104">API Management-beleidsregels zijn een krachtige mogelijkheid van het systeem waarmee de uitgever het gedrag van de API via configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cdb18-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="cdb18-105">Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op de aanvraag of het antwoord van een API.</span><span class="sxs-lookup"><span data-stu-id="cdb18-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="cdb18-106">Beleidsverklaringen kunnen worden samengesteld met behulp van letterlijke tekstwaarden, beleidsexpressies en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="cdb18-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="cdb18-107">Elk exemplaar van API Management-service heeft een verzameling eigenschappen van sleutel-waardeparen die algemeen in het service-exemplaar zijn.</span><span class="sxs-lookup"><span data-stu-id="cdb18-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="cdb18-108">Deze eigenschappen kunnen worden gebruikt voor het beheren van constante string-waarden voor alle configuratie-API en beleidsregels.</span><span class="sxs-lookup"><span data-stu-id="cdb18-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="cdb18-109">Elke eigenschap heeft de volgende kenmerken.</span><span class="sxs-lookup"><span data-stu-id="cdb18-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="cdb18-110">Kenmerk</span><span class="sxs-lookup"><span data-stu-id="cdb18-110">Attribute</span></span> | <span data-ttu-id="cdb18-111">Type</span><span class="sxs-lookup"><span data-stu-id="cdb18-111">Type</span></span> | <span data-ttu-id="cdb18-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cdb18-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdb18-113">Naam</span><span class="sxs-lookup"><span data-stu-id="cdb18-113">Name</span></span> |<span data-ttu-id="cdb18-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cdb18-114">string</span></span> |<span data-ttu-id="cdb18-115">De naam van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cdb18-115">The name of the property.</span></span> <span data-ttu-id="cdb18-116">Mogelijk bevatten alleen letters, cijfers, periode, streepjes en onderstrepingstekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="cdb18-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="cdb18-117">Waarde</span><span class="sxs-lookup"><span data-stu-id="cdb18-117">Value</span></span> |<span data-ttu-id="cdb18-118">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cdb18-118">string</span></span> |<span data-ttu-id="cdb18-119">De waarde van de eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cdb18-119">The value of the property.</span></span> <span data-ttu-id="cdb18-120">Het is niet leeg zijn of alleen witruimte bevatten.</span><span class="sxs-lookup"><span data-stu-id="cdb18-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="cdb18-121">Geheim</span><span class="sxs-lookup"><span data-stu-id="cdb18-121">Secret</span></span> |<span data-ttu-id="cdb18-122">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="cdb18-122">boolean</span></span> |<span data-ttu-id="cdb18-123">Bepaalt of de waarde een geheim is en moet worden versleuteld of niet.</span><span class="sxs-lookup"><span data-stu-id="cdb18-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="cdb18-124">Tags</span><span class="sxs-lookup"><span data-stu-id="cdb18-124">Tags</span></span> |<span data-ttu-id="cdb18-125">Matrix van tekenreeks</span><span class="sxs-lookup"><span data-stu-id="cdb18-125">array of string</span></span> |<span data-ttu-id="cdb18-126">Optioneel tags die de opgegeven voor het filteren van de lijst met eigenschappen kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdb18-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="cdb18-127">Eigenschappen zijn geconfigureerd in de publicatieportal op de **eigenschappen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cdb18-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="cdb18-128">In het volgende voorbeeld worden drie eigenschappen geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cdb18-128">In the following example, three properties are configured.</span></span>

![Eigenschappen][api-management-properties]

<span data-ttu-id="cdb18-130">Eigenschapswaarden letterlijke tekenreeksen kunnen bevatten en [beleidsexpressies](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="cdb18-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="cdb18-131">De volgende tabel ziet u de vorige drie Voorbeeld-eigenschappen en hun kenmerken.</span><span class="sxs-lookup"><span data-stu-id="cdb18-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="cdb18-132">De waarde van `ExpressionProperty` is een beleidsexpressie die retourneert een tekenreeks met de huidige datum en tijd.</span><span class="sxs-lookup"><span data-stu-id="cdb18-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="cdb18-133">De eigenschap `ContosoHeaderValue` is gemarkeerd als een geheim, zodat de waarde wordt niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cdb18-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="cdb18-134">Naam</span><span class="sxs-lookup"><span data-stu-id="cdb18-134">Name</span></span> | <span data-ttu-id="cdb18-135">Waarde</span><span class="sxs-lookup"><span data-stu-id="cdb18-135">Value</span></span> | <span data-ttu-id="cdb18-136">Geheim</span><span class="sxs-lookup"><span data-stu-id="cdb18-136">Secret</span></span> | <span data-ttu-id="cdb18-137">Tags</span><span class="sxs-lookup"><span data-stu-id="cdb18-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="cdb18-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="cdb18-138">ContosoHeader</span></span> |<span data-ttu-id="cdb18-139">trackingId</span><span class="sxs-lookup"><span data-stu-id="cdb18-139">TrackingId</span></span> |<span data-ttu-id="cdb18-140">False</span><span class="sxs-lookup"><span data-stu-id="cdb18-140">False</span></span> |<span data-ttu-id="cdb18-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="cdb18-141">Contoso</span></span> |
| <span data-ttu-id="cdb18-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="cdb18-142">ContosoHeaderValue</span></span> |<span data-ttu-id="cdb18-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="cdb18-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="cdb18-144">True</span><span class="sxs-lookup"><span data-stu-id="cdb18-144">True</span></span> |<span data-ttu-id="cdb18-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="cdb18-145">Contoso</span></span> |
| <span data-ttu-id="cdb18-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="cdb18-146">ExpressionProperty</span></span> |<span data-ttu-id="cdb18-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="cdb18-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="cdb18-148">False</span><span class="sxs-lookup"><span data-stu-id="cdb18-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="cdb18-149">Als een eigenschap wilt gebruiken</span><span class="sxs-lookup"><span data-stu-id="cdb18-149">To use a property</span></span>
<span data-ttu-id="cdb18-150">Als u een eigenschap in een beleid, plaatst u de naam van de eigenschap binnen een paar dubbele accolades zoals `{{ContosoHeader}}`, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="cdb18-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="cdb18-151">In dit voorbeeld `ContosoHeader` wordt gebruikt als de naam van een kop in een `set-header` beleid, en `ContosoHeaderValue` wordt gebruikt als de waarde van deze header.</span><span class="sxs-lookup"><span data-stu-id="cdb18-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="cdb18-152">Wanneer dit beleid wordt beoordeeld tijdens een aanvraag of antwoord naar de API Management-gateway `{{ContosoHeader}}` en `{{ContosoHeaderValue}}` worden vervangen door hun respectieve eigenschapswaarden.</span><span class="sxs-lookup"><span data-stu-id="cdb18-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="cdb18-153">Eigenschappen kunnen worden gebruikt als volledige kenmerk of elementwaarden zoals weergegeven in het vorige voorbeeld, maar ze kunnen ook worden ingevoegd in of in combinatie met het onderdeel van een expressie letterlijke tekst, zoals wordt weergegeven in het volgende voorbeeld:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="cdb18-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="cdb18-154">Eigenschappen bevatten ook beleidsexpressies.</span><span class="sxs-lookup"><span data-stu-id="cdb18-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="cdb18-155">In het volgende voorbeeld wordt de `ExpressionProperty` wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdb18-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="cdb18-156">Wanneer dit beleid wordt beoordeeld `{{ExpressionProperty}}` is vervangen door de waarde ervan: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="cdb18-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="cdb18-157">Omdat de waarde een beleidsexpressie is, wordt de expressie wordt geëvalueerd en wordt het beleid wordt doorgegaan met de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="cdb18-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="cdb18-158">U kunt deze functionaliteit in de portal voor ontwikkelaars testen door het aanroepen van een bewerking die een beleid met eigenschappen in het bereik heeft.</span><span class="sxs-lookup"><span data-stu-id="cdb18-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="cdb18-159">In het volgende voorbeeld wordt een bewerking wordt aangeroepen met de twee vorige voorbeeld `set-header` beleid met eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="cdb18-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="cdb18-160">Houd er rekening mee dat het antwoord bevat twee aangepaste headers die zijn geconfigureerd met beleid van eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="cdb18-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![ontwikkelaarsportal][api-management-send-results]

<span data-ttu-id="cdb18-162">Als u naar kijkt de [API Inspector trace](api-management-howto-api-inspector.md) voor een aanroep met de twee vorige voorbeeld beleidsregels met eigenschappen, ziet u de twee `set-header` beleid met de waarden van de eigenschap ingevoegd en de evaluatie van de beleid-expressie voor de eigenschap die deel uitmaakt van de beleidsexpressie.</span><span class="sxs-lookup"><span data-stu-id="cdb18-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![API-Inspector tracering][api-management-api-inspector-trace]

<span data-ttu-id="cdb18-164">Houd er rekening mee dat terwijl eigenschapswaarden beleidsexpressies bevatten kunnen, eigenschapswaarden kunnen geen andere eigenschappen bevatten.</span><span class="sxs-lookup"><span data-stu-id="cdb18-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="cdb18-165">Als tekst met een eigenschapverwijzing wordt gebruikt voor de waarde van een eigenschap, zoals `Property value text {{MyProperty}}`, die eigenschapverwijzing won't worden vervangen en worden opgenomen als onderdeel van de waarde van eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cdb18-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="cdb18-166">Een eigenschap maken</span><span class="sxs-lookup"><span data-stu-id="cdb18-166">To create a property</span></span>
<span data-ttu-id="cdb18-167">Klik op om een eigenschap **eigenschap toevoegen** op de **eigenschappen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cdb18-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Eigenschap toevoegen][api-management-properties-add-property-menu]

<span data-ttu-id="cdb18-169">**Naam** en **waarde** vereiste waarden zijn.</span><span class="sxs-lookup"><span data-stu-id="cdb18-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="cdb18-170">Als de waarde van deze eigenschap een geheim is, controleert u de **dit is een geheim** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="cdb18-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="cdb18-171">Geef een of meer optionele labels om te helpen bij het ordenen van uw eigenschappen en op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cdb18-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Eigenschap toevoegen][api-management-properties-add-property]

<span data-ttu-id="cdb18-173">Wanneer een nieuwe eigenschap wordt opgeslagen, de **eigenschap zoeken** textbox is gevuld met de naam van de nieuwe eigenschap en wordt de nieuwe eigenschap weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cdb18-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="cdb18-174">Als u wilt weergeven van alle eigenschappen, schakelt u de **eigenschap zoeken** textbox en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="cdb18-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Eigenschappen][api-management-properties-property-saved]

<span data-ttu-id="cdb18-176">Zie voor meer informatie over het maken van een eigenschap met de REST API [maakt u een eigenschap met de REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="cdb18-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="cdb18-177">Een eigenschap bewerken</span><span class="sxs-lookup"><span data-stu-id="cdb18-177">To edit a property</span></span>
<span data-ttu-id="cdb18-178">Een eigenschap bewerken, klikt u op **bewerken** naast de eigenschap te bewerken.</span><span class="sxs-lookup"><span data-stu-id="cdb18-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![De eigenschap bewerken][api-management-properties-edit]

<span data-ttu-id="cdb18-180">Breng de gewenste wijzigingen klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="cdb18-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="cdb18-181">Als u de naam van de eigenschap wijzigt, worden alle beleidsregels die verwijzen naar die eigenschap automatisch bijgewerkt voor het gebruik van de nieuwe naam.</span><span class="sxs-lookup"><span data-stu-id="cdb18-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![De eigenschap bewerken][api-management-properties-edit-property]

<span data-ttu-id="cdb18-183">Zie voor meer informatie over het bewerken van een eigenschap met de REST API [bewerken van een eigenschap met de REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="cdb18-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="cdb18-184">Een eigenschap te wijzigen</span><span class="sxs-lookup"><span data-stu-id="cdb18-184">To delete a property</span></span>
<span data-ttu-id="cdb18-185">Als u wilt verwijderen van een eigenschap, klikt u op **verwijderen** naast de eigenschap te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cdb18-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![Eigenschap verwijderen][api-management-properties-delete]

<span data-ttu-id="cdb18-187">Klik op **Ja, deze verwijderen** om te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="cdb18-187">Click **Yes, delete it** to confirm.</span></span>

![De verwijdering bevestigen][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="cdb18-189">Als de eigenschap wordt verwezen door andere beleidsregels, kunt u zich niet met succes te verwijderen als u de eigenschap verwijdert uit alle beleidsregels die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cdb18-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="cdb18-190">Zie voor meer informatie over het verwijderen van een eigenschap met de REST API [verwijderen van een eigenschap met de REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="cdb18-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="cdb18-191">Om te zoeken en filteren eigenschappen</span><span class="sxs-lookup"><span data-stu-id="cdb18-191">To search and filter properties</span></span>
<span data-ttu-id="cdb18-192">De **eigenschappen** tabblad Zoeken en filteren van mogelijkheden voor het beheren van uw eigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="cdb18-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="cdb18-193">De eigenschappenlijst filteren door de naam van eigenschap voeren een zoekterm in het **eigenschap zoeken** textbox.</span><span class="sxs-lookup"><span data-stu-id="cdb18-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="cdb18-194">Als u wilt weergeven van alle eigenschappen, schakelt u de **eigenschap zoeken** textbox en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="cdb18-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="cdb18-196">Voer voor de eigenschappenlijst filteren op labelwaarden, een of meer labels in de **filteren op labels** textbox.</span><span class="sxs-lookup"><span data-stu-id="cdb18-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="cdb18-197">Als u wilt weergeven van alle eigenschappen, schakelt u de **filteren op labels** textbox en druk op enter.</span><span class="sxs-lookup"><span data-stu-id="cdb18-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filteren][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="cdb18-199">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cdb18-199">Next steps</span></span>
* <span data-ttu-id="cdb18-200">Meer informatie over het werken met beleid</span><span class="sxs-lookup"><span data-stu-id="cdb18-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="cdb18-201">Beleidsregels in API Management</span><span class="sxs-lookup"><span data-stu-id="cdb18-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="cdb18-202">Naslaginformatie over beleidsregels</span><span class="sxs-lookup"><span data-stu-id="cdb18-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="cdb18-203">Beleidsexpressies</span><span class="sxs-lookup"><span data-stu-id="cdb18-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="cdb18-204">Bekijk een video-overzicht</span><span class="sxs-lookup"><span data-stu-id="cdb18-204">Watch a video overview</span></span>
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


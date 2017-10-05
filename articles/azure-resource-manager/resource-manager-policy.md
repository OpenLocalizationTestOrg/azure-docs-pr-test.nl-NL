---
title: Azure bronbeleid | Microsoft Docs
description: Beschrijft hoe u Azure Resource Manager-beleid gebruiken om ervoor te zorgen consistent broneigenschappen zijn ingesteld tijdens de implementatie. Beleidsregels kunnen worden toegepast op de groepen abonnement of resourcegroep.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/02/2017
ms.author: tomfitz
ms.openlocfilehash: 0ee2624f45a1de0c23cae4538a38ae3e302eedd3
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="e09c3-104">Overzicht van de resource-beleid</span><span class="sxs-lookup"><span data-stu-id="e09c3-104">Resource policy overview</span></span>
<span data-ttu-id="e09c3-105">Bronbeleid kunnen u tot stand brengen conventies voor resources in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="e09c3-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="e09c3-106">Door het definiëren van conventies u kosten kunt beheren en meer eenvoudig beheren van uw resources.</span><span class="sxs-lookup"><span data-stu-id="e09c3-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="e09c3-107">U kunt bijvoorbeeld opgeven dat alleen bepaalde typen virtuele machines zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="e09c3-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="e09c3-108">Of u kunt vereisen dat alle resources een bepaald label hebben.</span><span class="sxs-lookup"><span data-stu-id="e09c3-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="e09c3-109">Beleidsregels worden overgenomen door alle onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="e09c3-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="e09c3-110">Dus als een beleid wordt toegepast op een resourcegroep, is van toepassing op alle resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e09c3-110">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="e09c3-111">Er zijn twee concepten over het beleid begrijpen:</span><span class="sxs-lookup"><span data-stu-id="e09c3-111">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="e09c3-112">de beleidsdefinitie - beschrijft u wanneer het beleid wordt afgedwongen en welke actie moet worden uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="e09c3-112">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="e09c3-113">de toewijzing van configuratiebeleid - u beleidsdefinitie toepassen op een bereik (abonnement of de resource-group)</span><span class="sxs-lookup"><span data-stu-id="e09c3-113">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="e09c3-114">Dit onderwerp richt zich op de beleidsdefinitie van het.</span><span class="sxs-lookup"><span data-stu-id="e09c3-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="e09c3-115">Zie voor meer informatie over de toewijzing van configuratiebeleid [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md) of [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-115">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="e09c3-116">Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).</span><span class="sxs-lookup"><span data-stu-id="e09c3-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="e09c3-117">Beleid evalueren op dit moment niet brontypen die tags, type en locatie, zoals het brontype Microsoft.Resources/deployments niet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="e09c3-118">Deze ondersteuning wordt toegevoegd op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="e09c3-118">This support will be added at a future time.</span></span> <span data-ttu-id="e09c3-119">Compatibiliteit met eerdere versies om problemen te voorkomen, moet u expliciet type opgeven tijdens het opstellen van beleid.</span><span class="sxs-lookup"><span data-stu-id="e09c3-119">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="e09c3-120">Bijvoorbeeld, een tag beleid waarvoor geen typen toegepast voor alle typen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="e09c3-121">In dat geval een sjabloonimplementatie kan mislukken als er een geneste resource die biedt geen ondersteuning voor labels en het implementatietype van de resource is toegevoegd aan de evaluatie van het beleid.</span><span class="sxs-lookup"><span data-stu-id="e09c3-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="e09c3-122">Wat is het verschil van RBAC?</span><span class="sxs-lookup"><span data-stu-id="e09c3-122">How is it different from RBAC?</span></span>
<span data-ttu-id="e09c3-123">Er zijn enkele belangrijke verschillen tussen het beleid en op rollen gebaseerde toegangsbeheer (RBAC).</span><span class="sxs-lookup"><span data-stu-id="e09c3-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="e09c3-124">RBAC is gericht op **gebruiker** acties op verschillende bereiken.</span><span class="sxs-lookup"><span data-stu-id="e09c3-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="e09c3-125">U wordt bijvoorbeeld toegevoegd aan de rol Inzender voor een resourcegroep op het gewenste bereik, zodat u wijzigingen in die resourcegroep aanbrengen kunt.</span><span class="sxs-lookup"><span data-stu-id="e09c3-125">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="e09c3-126">Beleid is gericht op **resource** eigenschappen tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="e09c3-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="e09c3-127">U kunt bijvoorbeeld via het beleid, de typen bronnen die kunnen worden ingericht beheren.</span><span class="sxs-lookup"><span data-stu-id="e09c3-127">For example, through policies, you can control the types of resources that can be provisioned.</span></span> <span data-ttu-id="e09c3-128">Of u de locaties waar resources kunnen worden ingericht kunt beperken.</span><span class="sxs-lookup"><span data-stu-id="e09c3-128">Or, you can restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="e09c3-129">In tegenstelling tot RBAC, beleid is een standaard toestaan en expliciete system weigeren.</span><span class="sxs-lookup"><span data-stu-id="e09c3-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="e09c3-130">Voor gebruik van beleid, moet u eerst worden geverifieerd via RBAC.</span><span class="sxs-lookup"><span data-stu-id="e09c3-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="e09c3-131">In het bijzonder uw account moet het:</span><span class="sxs-lookup"><span data-stu-id="e09c3-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="e09c3-132">`Microsoft.Authorization/policydefinitions/write`machtiging voor het definiëren van een beleid</span><span class="sxs-lookup"><span data-stu-id="e09c3-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="e09c3-133">`Microsoft.Authorization/policyassignments/write`machtiging voor het toewijzen van een beleid</span><span class="sxs-lookup"><span data-stu-id="e09c3-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="e09c3-134">Deze machtigingen niet zijn opgenomen in de **Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="e09c3-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="e09c3-135">Ingebouwde beleid</span><span class="sxs-lookup"><span data-stu-id="e09c3-135">Built-in policies</span></span>

<span data-ttu-id="e09c3-136">Azure biedt een aantal ingebouwde beleidsdefinities die wellicht minder van beleidsregels die u hebt om te definiëren.</span><span class="sxs-lookup"><span data-stu-id="e09c3-136">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="e09c3-137">Voordat u doorgaat met de beleidsdefinities, moet u overwegen of een ingebouwde beleid al biedt de definitie die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="e09c3-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides the definition you need.</span></span> <span data-ttu-id="e09c3-138">De ingebouwde beleidsdefinities zijn:</span><span class="sxs-lookup"><span data-stu-id="e09c3-138">The built-in policy definitions are:</span></span>

* <span data-ttu-id="e09c3-139">Toegestane locaties</span><span class="sxs-lookup"><span data-stu-id="e09c3-139">Allowed locations</span></span>
* <span data-ttu-id="e09c3-140">Toegestane brontypen</span><span class="sxs-lookup"><span data-stu-id="e09c3-140">Allowed resource types</span></span>
* <span data-ttu-id="e09c3-141">Storage-account SKU's toegestaan</span><span class="sxs-lookup"><span data-stu-id="e09c3-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="e09c3-142">Virtuele machine SKU's toegestaan</span><span class="sxs-lookup"><span data-stu-id="e09c3-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="e09c3-143">Label en de standaardwaarde toepassen</span><span class="sxs-lookup"><span data-stu-id="e09c3-143">Apply tag and default value</span></span>
* <span data-ttu-id="e09c3-144">Label en waarde afdwingen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-144">Enforce tag and value</span></span>
* <span data-ttu-id="e09c3-145">Brontypen die toegestaan niet</span><span class="sxs-lookup"><span data-stu-id="e09c3-145">Not allowed resource types</span></span>
* <span data-ttu-id="e09c3-146">SQL Server versie 12.0 vereisen</span><span class="sxs-lookup"><span data-stu-id="e09c3-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="e09c3-147">Storage-accountversleuteling vereisen</span><span class="sxs-lookup"><span data-stu-id="e09c3-147">Require storage account encryption</span></span>

<span data-ttu-id="e09c3-148">U kunt een van deze beleidsregels via de [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), of [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e09c3-148">You can assign any of these policies through the [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="e09c3-149">Definitie beleidsstructuur</span><span class="sxs-lookup"><span data-stu-id="e09c3-149">Policy definition structure</span></span>
<span data-ttu-id="e09c3-150">JSON kunt u een beleidsdefinitie maken.</span><span class="sxs-lookup"><span data-stu-id="e09c3-150">You use JSON to create a policy definition.</span></span> <span data-ttu-id="e09c3-151">De beleidsdefinitie bevat-elementen voor:</span><span class="sxs-lookup"><span data-stu-id="e09c3-151">The policy definition contains elements for:</span></span>

* <span data-ttu-id="e09c3-152">Parameters</span><span class="sxs-lookup"><span data-stu-id="e09c3-152">parameters</span></span>
* <span data-ttu-id="e09c3-153">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="e09c3-153">display name</span></span>
* <span data-ttu-id="e09c3-154">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-154">description</span></span>
* <span data-ttu-id="e09c3-155">Beleidsregel</span><span class="sxs-lookup"><span data-stu-id="e09c3-155">policy rule</span></span>
  * <span data-ttu-id="e09c3-156">logische evaluatie</span><span class="sxs-lookup"><span data-stu-id="e09c3-156">logical evaluation</span></span>
  * <span data-ttu-id="e09c3-157">effect</span><span class="sxs-lookup"><span data-stu-id="e09c3-157">effect</span></span>

<span data-ttu-id="e09c3-158">Het volgende voorbeeld ziet u een beleid dat wordt beperkt welke resources zijn geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="e09c3-158">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="e09c3-159">Parameters</span><span class="sxs-lookup"><span data-stu-id="e09c3-159">Parameters</span></span>
<span data-ttu-id="e09c3-160">Met parameters, kunt u uw beleidsbeheer vereenvoudigen doordat het aantal beleidsdefinities.</span><span class="sxs-lookup"><span data-stu-id="e09c3-160">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="e09c3-161">U definieert een beleid voor een broneigenschap (zoals het beperken van de locaties waar resources kunnen worden geïmplementeerd) en parameters opnemen in de definitie.</span><span class="sxs-lookup"><span data-stu-id="e09c3-161">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="e09c3-162">U opnieuw gebruiken die beleidsdefinitie voor verschillende scenario's door door te geven in verschillende waarden (zoals het opgeven van een reeks locaties voor een abonnement) wanneer het toewijzen van beleid.</span><span class="sxs-lookup"><span data-stu-id="e09c3-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="e09c3-163">U kunt parameters declareren bij het maken van beleidsdefinities.</span><span class="sxs-lookup"><span data-stu-id="e09c3-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="e09c3-164">Het type van een parameter kan tekenreeks- of matrixtype zijn.</span><span class="sxs-lookup"><span data-stu-id="e09c3-164">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="e09c3-165">De metagegevenseigenschap wordt gebruikt voor hulpmiddelen zoals Azure-portal om gebruiksvriendelijke informatie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e09c3-165">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="e09c3-166">In de beleidsregel verwijzen naar parameters met de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="e09c3-166">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="e09c3-167">Weergavenaam en beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-167">Display name and description</span></span>

<span data-ttu-id="e09c3-168">U gebruikt de **displayName** en **beschrijving** om te bepalen van de beleidsdefinitie en voorzien in context wanneer deze wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e09c3-168">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="e09c3-169">Beleidsregel</span><span class="sxs-lookup"><span data-stu-id="e09c3-169">Policy rule</span></span>

<span data-ttu-id="e09c3-170">De beleidsregel bestaat uit **als** en **vervolgens** blokken.</span><span class="sxs-lookup"><span data-stu-id="e09c3-170">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="e09c3-171">In de **als** blok definiëren van een of meer voorwaarden die opgeven wanneer het beleid wordt afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-171">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="e09c3-172">U kunt logische operators toepassen op deze voorwaarden precies bepalen het scenario voor een beleid.</span><span class="sxs-lookup"><span data-stu-id="e09c3-172">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="e09c3-173">In de **vervolgens** blok, definieert u het effect dat gebeurt wanneer de **als** voorwaarden is voldaan.</span><span class="sxs-lookup"><span data-stu-id="e09c3-173">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="e09c3-174">Logische operators</span><span class="sxs-lookup"><span data-stu-id="e09c3-174">Logical operators</span></span>
<span data-ttu-id="e09c3-175">De ondersteunde logische operators zijn:</span><span class="sxs-lookup"><span data-stu-id="e09c3-175">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="e09c3-176">De **niet** syntaxis keert het resultaat van de voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="e09c3-176">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="e09c3-177">De **zet** syntaxis (vergelijkbaar met de logische **en** bewerking) moet u alle voorwaarden wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="e09c3-177">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="e09c3-178">De **dragen** syntaxis (vergelijkbaar met de logische **of** bewerking) vereist een of meer voorwaarden wordt voldaan.</span><span class="sxs-lookup"><span data-stu-id="e09c3-178">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="e09c3-179">U kunt logische operators nesten.</span><span class="sxs-lookup"><span data-stu-id="e09c3-179">You can nest logical operators.</span></span> <span data-ttu-id="e09c3-180">Het volgende voorbeeld wordt een **niet** bewerking die is genest binnen een **zet** bewerking.</span><span class="sxs-lookup"><span data-stu-id="e09c3-180">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a><span data-ttu-id="e09c3-181">Voorwaarden</span><span class="sxs-lookup"><span data-stu-id="e09c3-181">Conditions</span></span>
<span data-ttu-id="e09c3-182">De voorwaarde wordt geëvalueerd of een **veld** aan bepaalde criteria voldoet.</span><span class="sxs-lookup"><span data-stu-id="e09c3-182">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="e09c3-183">De ondersteunde voorwaarden zijn:</span><span class="sxs-lookup"><span data-stu-id="e09c3-183">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="e09c3-184">Wanneer u de **zoals** voorwaarde, kunt u een jokerteken (*) in de waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="e09c3-184">When using the **like** condition, you can provide a wildcard (*) in the value.</span></span>

<span data-ttu-id="e09c3-185">Wanneer u de **overeen met** voorwaarde, bieden `#` vertegenwoordigt een cijfer `?` voor een letter en een ander teken dat werkelijke teken vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="e09c3-185">When using the **match** condition, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="e09c3-186">Zie voor voorbeelden [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="e09c3-187">Velden</span><span class="sxs-lookup"><span data-stu-id="e09c3-187">Fields</span></span>
<span data-ttu-id="e09c3-188">Voorwaarden zijn samengesteld op basis van velden.</span><span class="sxs-lookup"><span data-stu-id="e09c3-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="e09c3-189">Een veld geeft eigenschappen in de nettolading van de resource-aanvraag die wordt gebruikt om de status van de resource te beschrijven.</span><span class="sxs-lookup"><span data-stu-id="e09c3-189">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="e09c3-190">De volgende velden worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="e09c3-190">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="e09c3-191">eigenschap aliassen - Zie voor een lijst [aliassen](#aliases).</span><span class="sxs-lookup"><span data-stu-id="e09c3-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="e09c3-192">Effect</span><span class="sxs-lookup"><span data-stu-id="e09c3-192">Effect</span></span>
<span data-ttu-id="e09c3-193">Beleid ondersteunt drie typen effect - `deny`, `audit`, en `append`.</span><span class="sxs-lookup"><span data-stu-id="e09c3-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="e09c3-194">**Weigeren** wordt een gebeurtenis gegenereerd in het controlelogboek en de aanvraag is mislukt</span><span class="sxs-lookup"><span data-stu-id="e09c3-194">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="e09c3-195">**Audit** genereert een waarschuwingsgebeurtenis in controlelogboek maar mislukt de aanvraag niet</span><span class="sxs-lookup"><span data-stu-id="e09c3-195">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="e09c3-196">**Append** voegt de gedefinieerde set velden toe aan de aanvraag</span><span class="sxs-lookup"><span data-stu-id="e09c3-196">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="e09c3-197">Voor **toevoegen**, moet u de volgende details opgeven:</span><span class="sxs-lookup"><span data-stu-id="e09c3-197">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="e09c3-198">De waarde kan niet een tekenreeks of een object van JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="e09c3-198">The value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="e09c3-199">Aliassen</span><span class="sxs-lookup"><span data-stu-id="e09c3-199">Aliases</span></span>

<span data-ttu-id="e09c3-200">U eigenschap aliassen gebruiken voor toegang tot specifieke eigenschappen voor een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="e09c3-200">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="e09c3-201">Aliassen kunnen u beperken welke waarden of de voorwaarden zijn toegestaan voor een eigenschap van een resource.</span><span class="sxs-lookup"><span data-stu-id="e09c3-201">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="e09c3-202">Elke alias wordt toegewezen aan paden in verschillende API-versies voor een bepaald brontype.</span><span class="sxs-lookup"><span data-stu-id="e09c3-202">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="e09c3-203">Tijdens de evaluatie van het beleid haalt de beleidsengine het eigenschapspad voor die API-versie.</span><span class="sxs-lookup"><span data-stu-id="e09c3-203">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="e09c3-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="e09c3-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="e09c3-205">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-205">Alias</span></span> | <span data-ttu-id="e09c3-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="e09c3-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="e09c3-208">Instellen is of de Redis-server niet-ssl-poort (6379) ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e09c3-208">Set whether the non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="e09c3-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="e09c3-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="e09c3-210">Stel het aantal shards op een Cluster Premium Cache moeten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e09c3-210">Set the number of shards to be created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="e09c3-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="e09c3-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="e09c3-212">Stel de grootte van de Redis-cache te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e09c3-212">Set the size of the Redis cache to deploy.</span></span>  |
| <span data-ttu-id="e09c3-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="e09c3-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="e09c3-214">Stel de SKU-serie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e09c3-214">Set the SKU family to use.</span></span> |
| <span data-ttu-id="e09c3-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="e09c3-216">Instellen van het type van Redis-Cache te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e09c3-216">Set the type of Redis Cache to deploy.</span></span> |

<span data-ttu-id="e09c3-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="e09c3-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="e09c3-218">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-218">Alias</span></span> | <span data-ttu-id="e09c3-219">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="e09c3-221">De naam van de prijscategorie instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-221">Set the name of the pricing tier.</span></span> |

<span data-ttu-id="e09c3-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="e09c3-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="e09c3-223">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-223">Alias</span></span> | <span data-ttu-id="e09c3-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="e09c3-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="e09c3-226">Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-226">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="e09c3-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="e09c3-228">Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-228">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="e09c3-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="e09c3-230">Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-230">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="e09c3-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="e09c3-232">Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-232">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |


<span data-ttu-id="e09c3-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="e09c3-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="e09c3-234">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-234">Alias</span></span> | <span data-ttu-id="e09c3-235">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="e09c3-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="e09c3-237">De id van de afbeelding die wordt gebruikt voor het maken van de virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-237">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="e09c3-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="e09c3-239">Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-239">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="e09c3-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="e09c3-241">Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-241">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="e09c3-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="e09c3-243">Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-243">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="e09c3-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="e09c3-245">Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-245">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="e09c3-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="e09c3-247">Instellen dat de installatiekopie of schijf gelicentieerde lokaal is.</span><span class="sxs-lookup"><span data-stu-id="e09c3-247">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="e09c3-248">Deze waarde wordt alleen gebruikt voor afbeeldingen die het besturingssysteem Windows Server bevatten.</span><span class="sxs-lookup"><span data-stu-id="e09c3-248">This value is only used for images that contain the Windows Server operating system.</span></span>  |
| <span data-ttu-id="e09c3-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="e09c3-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="e09c3-250">Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-250">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="e09c3-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="e09c3-252">Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-252">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="e09c3-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="e09c3-254">Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-254">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="e09c3-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="e09c3-256">Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-256">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="e09c3-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="e09c3-258">Stel de vhd-URI.</span><span class="sxs-lookup"><span data-stu-id="e09c3-258">Set the vhd URI.</span></span> |
| <span data-ttu-id="e09c3-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="e09c3-260">Stel de grootte van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-260">Set the size of the virtual machine.</span></span> |

<span data-ttu-id="e09c3-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="e09c3-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="e09c3-262">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-262">Alias</span></span> | <span data-ttu-id="e09c3-263">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="e09c3-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="e09c3-265">De naam van de uitgever de extensie instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-265">Set the name of the extension’s publisher.</span></span> |
| <span data-ttu-id="e09c3-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="e09c3-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="e09c3-267">Het type van extensie instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-267">Set the type of extension.</span></span> |
| <span data-ttu-id="e09c3-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="e09c3-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="e09c3-269">Stel de versie van de uitbreiding.</span><span class="sxs-lookup"><span data-stu-id="e09c3-269">Set the version of the extension.</span></span> |

<span data-ttu-id="e09c3-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="e09c3-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="e09c3-271">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-271">Alias</span></span> | <span data-ttu-id="e09c3-272">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="e09c3-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="e09c3-274">De id van de afbeelding die wordt gebruikt voor het maken van de virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-274">Set the identifier of the image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="e09c3-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="e09c3-276">Stel de aanbieding van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-276">Set the offer of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="e09c3-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="e09c3-278">Stel de uitgever van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-278">Set the publisher of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="e09c3-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="e09c3-280">Stel de SKU van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-280">Set the SKU of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="e09c3-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="e09c3-282">Stel de versie van de platforminstallatiekopie van het of de marketplace-installatiekopie gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e09c3-282">Set the version of the platform image or marketplace image used to create the virtual machine.</span></span> |
| <span data-ttu-id="e09c3-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="e09c3-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="e09c3-284">Instellen dat de installatiekopie of schijf gelicentieerde lokaal is.</span><span class="sxs-lookup"><span data-stu-id="e09c3-284">Set that the image or disk is licensed on-premises.</span></span> <span data-ttu-id="e09c3-285">Deze waarde wordt alleen gebruikt voor afbeeldingen die het besturingssysteem Windows Server bevatten.</span><span class="sxs-lookup"><span data-stu-id="e09c3-285">This value is only used for images that contain the Windows Server operating system.</span></span> |
| <span data-ttu-id="e09c3-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="e09c3-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="e09c3-287">Het voorvoegsel van de computer voor de virtuele machines in de schaalset instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-287">Set the computer name prefix for all  the virtual machines in the scale set.</span></span> |
| <span data-ttu-id="e09c3-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="e09c3-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="e09c3-289">Stel de blob-URI voor de gebruikersinstallatiekopie van de.</span><span class="sxs-lookup"><span data-stu-id="e09c3-289">Set the blob URI for user image.</span></span> |
| <span data-ttu-id="e09c3-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="e09c3-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="e09c3-291">De container-URL's die worden gebruikt voor het opslaan van besturingssysteem schijven voor de schaalaanpassingsset ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e09c3-291">Set the container URLs that are used to store operating system disks for the scale set.</span></span> |
| <span data-ttu-id="e09c3-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="e09c3-293">De grootte van virtuele machines in een scale-set instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-293">Set the size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="e09c3-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="e09c3-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="e09c3-295">De laag van virtuele machines in een scale-set instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-295">Set the tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="e09c3-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="e09c3-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="e09c3-297">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-297">Alias</span></span> | <span data-ttu-id="e09c3-298">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="e09c3-300">De grootte van de gateway instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-300">Set the size of the gateway.</span></span> |

<span data-ttu-id="e09c3-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="e09c3-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="e09c3-302">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-302">Alias</span></span> | <span data-ttu-id="e09c3-303">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="e09c3-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="e09c3-305">Het type van deze virtuele netwerkgateway instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-305">Set the type of this virtual network gateway.</span></span> |
| <span data-ttu-id="e09c3-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="e09c3-307">De naam van de gateway-SKU ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e09c3-307">Set the gateway SKU name.</span></span> |

<span data-ttu-id="e09c3-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="e09c3-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="e09c3-309">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-309">Alias</span></span> | <span data-ttu-id="e09c3-310">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="e09c3-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="e09c3-312">Stel de versie van de server.</span><span class="sxs-lookup"><span data-stu-id="e09c3-312">Set the version of the server.</span></span> |

<span data-ttu-id="e09c3-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="e09c3-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="e09c3-314">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-314">Alias</span></span> | <span data-ttu-id="e09c3-315">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="e09c3-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="e09c3-317">Stel de versie van de database.</span><span class="sxs-lookup"><span data-stu-id="e09c3-317">Set the edition of the database.</span></span> |
| <span data-ttu-id="e09c3-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="e09c3-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="e09c3-319">De naam van de elastische groep die de database is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="e09c3-319">Set the name of the elastic pool the database is in.</span></span> |
| <span data-ttu-id="e09c3-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="e09c3-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="e09c3-321">Stel de geconfigureerde service level objective-ID van de database.</span><span class="sxs-lookup"><span data-stu-id="e09c3-321">Set the configured service level objective ID of the database.</span></span> |
| <span data-ttu-id="e09c3-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="e09c3-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="e09c3-323">De naam van de geconfigureerde serviceniveaudoelstelling van de database instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-323">Set the name of the configured service level objective of the database.</span></span>  |

<span data-ttu-id="e09c3-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="e09c3-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="e09c3-325">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-325">Alias</span></span> | <span data-ttu-id="e09c3-326">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="e09c3-327">servers/elasticpools</span></span> | <span data-ttu-id="e09c3-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="e09c3-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="e09c3-329">Stel de totale gedeelde DTU voor een elastische pool in de database.</span><span class="sxs-lookup"><span data-stu-id="e09c3-329">Set the total shared DTU for the database elastic pool.</span></span> |
| <span data-ttu-id="e09c3-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="e09c3-330">servers/elasticpools</span></span> | <span data-ttu-id="e09c3-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="e09c3-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="e09c3-332">Stel de versie van de elastische groep.</span><span class="sxs-lookup"><span data-stu-id="e09c3-332">Set the edition of the elastic pool.</span></span> |

<span data-ttu-id="e09c3-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="e09c3-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="e09c3-334">Alias</span><span class="sxs-lookup"><span data-stu-id="e09c3-334">Alias</span></span> | <span data-ttu-id="e09c3-335">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e09c3-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="e09c3-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="e09c3-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="e09c3-337">Stel de toegangslaag gebruikt voor facturering.</span><span class="sxs-lookup"><span data-stu-id="e09c3-337">Set the access tier used for billing.</span></span> |
| <span data-ttu-id="e09c3-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="e09c3-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="e09c3-339">De SKU-naam instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-339">Set the SKU name.</span></span> |
| <span data-ttu-id="e09c3-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="e09c3-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="e09c3-341">Instellen of de service de gegevens versleutelt die wordt opgeslagen in de blob storage-service.</span><span class="sxs-lookup"><span data-stu-id="e09c3-341">Set whether the service encrypts the data as it is stored in the blob storage service.</span></span> |
| <span data-ttu-id="e09c3-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="e09c3-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="e09c3-343">Instellen of de service de gegevens versleutelt die in de storage-service van het bestand wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-343">Set whether the service encrypts the data as it is stored in the file storage service.</span></span> |
| <span data-ttu-id="e09c3-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="e09c3-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="e09c3-345">De SKU-naam instellen.</span><span class="sxs-lookup"><span data-stu-id="e09c3-345">Set the SKU name.</span></span> |
| <span data-ttu-id="e09c3-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="e09c3-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="e09c3-347">Stel in dat alleen https-verkeer met storage-service.</span><span class="sxs-lookup"><span data-stu-id="e09c3-347">Set to allow only https traffic to storage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="e09c3-348">Voorbeelden van beleid</span><span class="sxs-lookup"><span data-stu-id="e09c3-348">Policy examples</span></span>

<span data-ttu-id="e09c3-349">De volgende onderwerpen bevatten voorbeelden van beleid:</span><span class="sxs-lookup"><span data-stu-id="e09c3-349">The following topics contain policy examples:</span></span>

* <span data-ttu-id="e09c3-350">Zie voor voorbeelden van de tag beleidsregels, [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="e09c3-351">Zie voor voorbeelden van naamgeving en tekst patronen [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="e09c3-352">Zie voor voorbeelden van beleidsregels voor opslag [resource beleid toepassen op opslagaccounts](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-352">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="e09c3-353">Zie voor voorbeelden van beleidsregels voor virtuele machine [resource beleid toepassen op virtuele Linux-machines](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en [resource beleid toepassen op Windows-VM's](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e09c3-353">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="e09c3-354">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e09c3-354">Next steps</span></span>
* <span data-ttu-id="e09c3-355">Na het definiëren van een beleidsregel, moet u het toewijzen aan een bereik.</span><span class="sxs-lookup"><span data-stu-id="e09c3-355">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="e09c3-356">Als u wilt toewijzen beleid via de portal, Zie [gebruik Azure-portal toewijzen en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-356">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="e09c3-357">Als u wilt toewijzen beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-357">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="e09c3-358">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e09c3-358">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="e09c3-359">Het schema van het beleid wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="e09c3-359">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 


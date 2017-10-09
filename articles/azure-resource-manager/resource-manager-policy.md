---
title: bronbeleid aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure Resource Manager-beleid tooensure consistent broneigenschappen zijn ingesteld tijdens de implementatie. Beleidsregels kunnen worden toegepast op Hallo abonnement of de resource-groepen.
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
ms.openlocfilehash: f1b0bbb5f838f6bb70721e1040ad3eac2d881cea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="resource-policy-overview"></a><span data-ttu-id="f5a1e-104">Overzicht van de resource-beleid</span><span class="sxs-lookup"><span data-stu-id="f5a1e-104">Resource policy overview</span></span>
<span data-ttu-id="f5a1e-105">Bronbeleid inschakelen tooestablish conventies voor bronnen in uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-105">Resource policies enable you tooestablish conventions for resources in your organization.</span></span> <span data-ttu-id="f5a1e-106">Door het definiëren van conventies u kosten kunt beheren en meer eenvoudig beheren van uw resources.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="f5a1e-107">U kunt bijvoorbeeld opgeven dat alleen bepaalde typen virtuele machines zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-107">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="f5a1e-108">Of u kunt vereisen dat alle resources een bepaald label hebben.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-108">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="f5a1e-109">Beleidsregels worden overgenomen door alle onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-109">Policies are inherited by all child resources.</span></span> <span data-ttu-id="f5a1e-110">Dus als een beleid toegepast tooa resourcegroep is, van toepassing tooall Hallo resources in die resourcegroep is.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-110">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span>

<span data-ttu-id="f5a1e-111">Er zijn twee concepten toounderstand over beleid:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-111">There are two concepts toounderstand about policies:</span></span>

* <span data-ttu-id="f5a1e-112">de beleidsdefinitie - beschrijft u wanneer Hallo beleid wordt afgedwongen en welke actie tootake</span><span class="sxs-lookup"><span data-stu-id="f5a1e-112">policy definition - you describe when hello policy is enforced and what action tootake</span></span>
* <span data-ttu-id="f5a1e-113">Wanneer u Hallo beleid definitie tooa bereik (abonnement of resourcegroep) beleidstoewijzing - toepassen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-113">policy assignment - you apply hello policy definition tooa scope (subscription or resource group)</span></span>

<span data-ttu-id="f5a1e-114">Dit onderwerp richt zich op de beleidsdefinitie van het.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-114">This topic focuses on policy definition.</span></span> <span data-ttu-id="f5a1e-115">Zie voor meer informatie over de toewijzing van configuratiebeleid [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md) of [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-115">For information about policy assignment, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="f5a1e-116">Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-116">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="f5a1e-117">Beleid evalueren op dit moment niet brontypen die tags, type en locatie, zoals Hallo Microsoft.Resources/deployments brontype niet ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-117">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as hello Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="f5a1e-118">Deze ondersteuning wordt toegevoegd op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-118">This support will be added at a future time.</span></span> <span data-ttu-id="f5a1e-119">problemen met tooavoid achterwaartse compatibiliteit, moet u expliciet opgeven type tijdens het opstellen van beleid.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-119">tooavoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="f5a1e-120">Bijvoorbeeld, een tag beleid waarvoor geen typen toegepast voor alle typen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-120">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="f5a1e-121">In dat geval een sjabloonimplementatie kan mislukken als er een geneste resource die biedt geen ondersteuning voor labels en Hallo resource implementatietype toopolicy evaluatie is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-121">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and hello deployment resource type has been added toopolicy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="f5a1e-122">Wat is het verschil van RBAC?</span><span class="sxs-lookup"><span data-stu-id="f5a1e-122">How is it different from RBAC?</span></span>
<span data-ttu-id="f5a1e-123">Er zijn enkele belangrijke verschillen tussen het beleid en op rollen gebaseerde toegangsbeheer (RBAC).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-123">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="f5a1e-124">RBAC is gericht op **gebruiker** acties op verschillende bereiken.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-124">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="f5a1e-125">U wordt bijvoorbeeld toohello de rol van inzender voor een resourcegroep toegevoegd bij Hallo gewenst bereik, zodat u de resourcegroep voor toothat wijzigingen kunt aanbrengen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-125">For example, you are added toohello contributor role for a resource group at hello desired scope, so you can make changes toothat resource group.</span></span> <span data-ttu-id="f5a1e-126">Beleid is gericht op **resource** eigenschappen tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-126">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="f5a1e-127">U kunt bijvoorbeeld via het beleid, Hallo typen resources die kunnen worden ingericht beheren.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-127">For example, through policies, you can control hello types of resources that can be provisioned.</span></span> <span data-ttu-id="f5a1e-128">Of u kunt beperken Hallo locaties waarin Hallo resources kunnen worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-128">Or, you can restrict hello locations in which hello resources can be provisioned.</span></span> <span data-ttu-id="f5a1e-129">In tegenstelling tot RBAC, beleid is een standaard toestaan en expliciete system weigeren.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="f5a1e-130">beleid voor toouse u moet worden geverifieerd via RBAC.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-130">toouse policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="f5a1e-131">In het bijzonder uw account moet het:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="f5a1e-132">`Microsoft.Authorization/policydefinitions/write`machtiging toodefine een beleid</span><span class="sxs-lookup"><span data-stu-id="f5a1e-132">`Microsoft.Authorization/policydefinitions/write` permission toodefine a policy</span></span>
* <span data-ttu-id="f5a1e-133">`Microsoft.Authorization/policyassignments/write`machtiging tooassign een beleid</span><span class="sxs-lookup"><span data-stu-id="f5a1e-133">`Microsoft.Authorization/policyassignments/write` permission tooassign a policy</span></span> 

<span data-ttu-id="f5a1e-134">Deze machtigingen niet zijn opgenomen in Hallo **Inzender** rol.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-134">These permissions are not included in hello **Contributor** role.</span></span>

## <a name="built-in-policies"></a><span data-ttu-id="f5a1e-135">Ingebouwde beleid</span><span class="sxs-lookup"><span data-stu-id="f5a1e-135">Built-in policies</span></span>

<span data-ttu-id="f5a1e-136">Azure biedt een aantal ingebouwde beleidsdefinities die Hallo beperken mogelijk van beleidsregels die u hebt toodefine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-136">Azure provides some built-in policy definitions that may reduce hello number of policies you have toodefine.</span></span> <span data-ttu-id="f5a1e-137">Voordat u doorgaat met de beleidsdefinities, moet u overwegen of een ingebouwde beleid al Hallo definitie u moet biedt.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-137">Before proceeding with policy definitions, you should consider whether a built-in policy already provides hello definition you need.</span></span> <span data-ttu-id="f5a1e-138">Hallo ingebouwde beleidsdefinities zijn:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-138">hello built-in policy definitions are:</span></span>

* <span data-ttu-id="f5a1e-139">Toegestane locaties</span><span class="sxs-lookup"><span data-stu-id="f5a1e-139">Allowed locations</span></span>
* <span data-ttu-id="f5a1e-140">Toegestane brontypen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-140">Allowed resource types</span></span>
* <span data-ttu-id="f5a1e-141">Storage-account SKU's toegestaan</span><span class="sxs-lookup"><span data-stu-id="f5a1e-141">Allowed storage account SKUs</span></span>
* <span data-ttu-id="f5a1e-142">Virtuele machine SKU's toegestaan</span><span class="sxs-lookup"><span data-stu-id="f5a1e-142">Allowed virtual machine SKUs</span></span>
* <span data-ttu-id="f5a1e-143">Label en de standaardwaarde toepassen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-143">Apply tag and default value</span></span>
* <span data-ttu-id="f5a1e-144">Label en waarde afdwingen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-144">Enforce tag and value</span></span>
* <span data-ttu-id="f5a1e-145">Brontypen die toegestaan niet</span><span class="sxs-lookup"><span data-stu-id="f5a1e-145">Not allowed resource types</span></span>
* <span data-ttu-id="f5a1e-146">SQL Server versie 12.0 vereisen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-146">Require SQL Server version 12.0</span></span>
* <span data-ttu-id="f5a1e-147">Storage-accountversleuteling vereisen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-147">Require storage account encryption</span></span>

<span data-ttu-id="f5a1e-148">U kunt een van deze beleidsregels via Hallo [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), of [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-148">You can assign any of these policies through hello [portal](resource-manager-policy-portal.md), [PowerShell](resource-manager-policy-create-assign.md#powershell), or [Azure CLI](resource-manager-policy-create-assign.md#azure-cli).</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="f5a1e-149">Definitie beleidsstructuur</span><span class="sxs-lookup"><span data-stu-id="f5a1e-149">Policy definition structure</span></span>
<span data-ttu-id="f5a1e-150">U JSON toocreate een beleidsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-150">You use JSON toocreate a policy definition.</span></span> <span data-ttu-id="f5a1e-151">de beleidsdefinitie Hallo bevat-elementen voor:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-151">hello policy definition contains elements for:</span></span>

* <span data-ttu-id="f5a1e-152">parameters</span><span class="sxs-lookup"><span data-stu-id="f5a1e-152">parameters</span></span>
* <span data-ttu-id="f5a1e-153">Weergavenaam</span><span class="sxs-lookup"><span data-stu-id="f5a1e-153">display name</span></span>
* <span data-ttu-id="f5a1e-154">description</span><span class="sxs-lookup"><span data-stu-id="f5a1e-154">description</span></span>
* <span data-ttu-id="f5a1e-155">Beleidsregel</span><span class="sxs-lookup"><span data-stu-id="f5a1e-155">policy rule</span></span>
  * <span data-ttu-id="f5a1e-156">logische evaluatie</span><span class="sxs-lookup"><span data-stu-id="f5a1e-156">logical evaluation</span></span>
  * <span data-ttu-id="f5a1e-157">effect</span><span class="sxs-lookup"><span data-stu-id="f5a1e-157">effect</span></span>

<span data-ttu-id="f5a1e-158">Hallo volgende voorbeeld ziet u een beleid dat wordt beperkt welke resources zijn geïmplementeerd:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-158">hello following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "hello list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you toorestrict hello locations your organization can specify when deploying resources.",
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

## <a name="parameters"></a><span data-ttu-id="f5a1e-159">Parameters</span><span class="sxs-lookup"><span data-stu-id="f5a1e-159">Parameters</span></span>
<span data-ttu-id="f5a1e-160">Met parameters, kunt u uw beleidsbeheer vereenvoudigen doordat het aantal beleidsdefinities Hallo.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-160">Using parameters helps simplify your policy management by reducing hello number of policy definitions.</span></span> <span data-ttu-id="f5a1e-161">U definieert een beleid voor een broneigenschap (zoals beperken Hallo locaties waar resources kunnen worden geïmplementeerd) en parameters in Hallo definitie bevatten.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-161">You define a policy for a resource property (such as limiting hello locations where resources can be deployed), and include parameters in hello definition.</span></span> <span data-ttu-id="f5a1e-162">U opnieuw gebruiken die beleidsdefinitie voor verschillende scenario's door door te geven in verschillende waarden (zoals het opgeven van een reeks locaties voor een abonnement) wanneer Hallo beleid toe te wijzen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-162">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning hello policy.</span></span>

<span data-ttu-id="f5a1e-163">U kunt parameters declareren bij het maken van beleidsdefinities.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-163">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "hello list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="f5a1e-164">Hallo-type van een parameter is tekenreeks of matrix.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-164">hello type of a parameter can be either string or array.</span></span> <span data-ttu-id="f5a1e-165">Hallo metagegevenseigenschap wordt voor hulpprogramma's als Azure portal toodisplay gebruiksvriendelijke informatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-165">hello metadata property is used for tools like Azure portal toodisplay user-friendly information.</span></span> 

<span data-ttu-id="f5a1e-166">In de beleidsregel hello, verwijzen u parameters naar Hello de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-166">In hello policy rule, you reference parameters with hello following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="f5a1e-167">Weergavenaam en beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-167">Display name and description</span></span>

<span data-ttu-id="f5a1e-168">Gebruik van Hallo **displayName** en **beschrijving** tooidentify beleidsdefinitie Hallo en voorzien in context wanneer deze wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-168">You use hello **displayName** and **description** tooidentify hello policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="f5a1e-169">Beleidsregel</span><span class="sxs-lookup"><span data-stu-id="f5a1e-169">Policy rule</span></span>

<span data-ttu-id="f5a1e-170">Hallo beleidsregel bestaat uit **als** en **vervolgens** blokken.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-170">hello policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="f5a1e-171">In Hallo **als** blok definiëren van een of meer voorwaarden die opgeven wanneer Hallo beleid wordt afgedwongen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-171">In hello **If** block, you define one or more conditions that specify when hello policy is enforced.</span></span> <span data-ttu-id="f5a1e-172">U kunt logische operators toothese voorwaarden toepassen tooprecisely Hallo scenario voor een beleid definiëren.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-172">You can apply logical operators toothese conditions tooprecisely define hello scenario for a policy.</span></span> <span data-ttu-id="f5a1e-173">In Hallo **vervolgens** blok, definieert u Hallo effect dat gebeurt er wanneer hello **als** voorwaarden is voldaan.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-173">In hello **Then** block, you define hello effect that happens when hello **If** conditions are fulfilled.</span></span>

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

### <a name="logical-operators"></a><span data-ttu-id="f5a1e-174">Logische operators</span><span class="sxs-lookup"><span data-stu-id="f5a1e-174">Logical operators</span></span>
<span data-ttu-id="f5a1e-175">logische operators Hallo ondersteund zijn:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-175">hello supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="f5a1e-176">Hallo **niet** syntaxis keert Hallo resultaat van het Hallo-voorwaarde.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-176">hello **not** syntax inverts hello result of hello condition.</span></span> <span data-ttu-id="f5a1e-177">Hallo **zet** syntaxis (vergelijkbaar toohello logische **en** bewerking) alle voorwaarden toobe waar vereist.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-177">hello **allOf** syntax (similar toohello logical **And** operation) requires all conditions toobe true.</span></span> <span data-ttu-id="f5a1e-178">Hallo **dragen** syntaxis (vergelijkbaar toohello logische **of** bewerking) vereist een of meer voorwaarden toobe true.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-178">hello **anyOf** syntax (similar toohello logical **Or** operation) requires one or more conditions toobe true.</span></span>

<span data-ttu-id="f5a1e-179">U kunt logische operators nesten.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-179">You can nest logical operators.</span></span> <span data-ttu-id="f5a1e-180">Hallo volgende voorbeeld ziet u een **niet** bewerking die is genest binnen een **zet** bewerking.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-180">hello following example shows a **not** operation that is nested within an **allOf** operation.</span></span> 

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

### <a name="conditions"></a><span data-ttu-id="f5a1e-181">Voorwaarden</span><span class="sxs-lookup"><span data-stu-id="f5a1e-181">Conditions</span></span>
<span data-ttu-id="f5a1e-182">Hallo voorwaarde wordt geëvalueerd of een **veld** aan bepaalde criteria voldoet.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-182">hello condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="f5a1e-183">Hallo ondersteund voorwaarden zijn:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-183">hello supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"match": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="f5a1e-184">Wanneer u Hallo **zoals** voorwaarde, kunt u een jokerteken (*) in Hallo-waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-184">When using hello **like** condition, you can provide a wildcard (*) in hello value.</span></span>

<span data-ttu-id="f5a1e-185">Wanneer u Hallo **overeen met** voorwaarde, bieden `#` toorepresent een cijfer `?` voor een letter en een ander toorepresent Werkelijke teken teken.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-185">When using hello **match** condition, provide `#` toorepresent a digit, `?` for a letter, and any other character toorepresent that actual character.</span></span> <span data-ttu-id="f5a1e-186">Zie voor voorbeelden [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-186">For examples, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>

### <a name="fields"></a><span data-ttu-id="f5a1e-187">Velden</span><span class="sxs-lookup"><span data-stu-id="f5a1e-187">Fields</span></span>
<span data-ttu-id="f5a1e-188">Voorwaarden zijn samengesteld op basis van velden.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-188">Conditions are formed by using fields.</span></span> <span data-ttu-id="f5a1e-189">Hiermee geeft u een veld eigenschappen in de aanvraaglading van de resource Hallo die gebruikte toodescribe Hallo status van Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-189">A field represents properties in hello resource request payload that is used toodescribe hello state of hello resource.</span></span>  

<span data-ttu-id="f5a1e-190">Hallo volgende velden worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-190">hello following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="f5a1e-191">eigenschap aliassen - Zie voor een lijst [aliassen](#aliases).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-191">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="f5a1e-192">Effect</span><span class="sxs-lookup"><span data-stu-id="f5a1e-192">Effect</span></span>
<span data-ttu-id="f5a1e-193">Beleid ondersteunt drie typen effect - `deny`, `audit`, en `append`.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-193">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="f5a1e-194">**Weigeren** wordt een gebeurtenis gegenereerd in het controlelogboek Hallo en Hallo-aanvraag is mislukt</span><span class="sxs-lookup"><span data-stu-id="f5a1e-194">**Deny** generates an event in hello audit log and fails hello request</span></span>
* <span data-ttu-id="f5a1e-195">**Audit** genereert een waarschuwingsgebeurtenis in controlelogboek maar mislukt niet Hallo-aanvraag</span><span class="sxs-lookup"><span data-stu-id="f5a1e-195">**Audit** generates a warning event in audit log but does not fail hello request</span></span>
* <span data-ttu-id="f5a1e-196">**Append** voegt Hallo gedefinieerd set velden toohello aanvraag</span><span class="sxs-lookup"><span data-stu-id="f5a1e-196">**Append** adds hello defined set of fields toohello request</span></span> 

<span data-ttu-id="f5a1e-197">Voor **toevoegen**, moet u de volgende details Hallo opgeven:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-197">For **append**, you must provide hello following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of hello field"
  }
]
```

<span data-ttu-id="f5a1e-198">Hallo-waarde is een tekenreeks of een object van JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-198">hello value can be either a string or a JSON format object.</span></span> 

## <a name="aliases"></a><span data-ttu-id="f5a1e-199">Aliassen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-199">Aliases</span></span>

<span data-ttu-id="f5a1e-200">U gebruikt eigenschap aliassen tooaccess specifieke eigenschappen voor een resourcetype.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-200">You use property aliases tooaccess specific properties for a resource type.</span></span> <span data-ttu-id="f5a1e-201">Aliassen inschakelen toorestrict welke waarden of de voorwaarden zijn toegestaan voor een eigenschap van een resource.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-201">Aliases enable you toorestrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="f5a1e-202">Elke alias toegewezen toopaths in verschillende versies van de API voor een bepaald brontype.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-202">Each alias maps toopaths in different API versions for a given resource type.</span></span> <span data-ttu-id="f5a1e-203">Tijdens de evaluatie van het beleid haalt de beleidsengine Hallo Hallo eigenschapspad voor die API-versie.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-203">During policy evaluation, hello policy engine gets hello property path for that API version.</span></span>

<span data-ttu-id="f5a1e-204">**Microsoft.Cache/Redis**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-204">**Microsoft.Cache/Redis**</span></span>

| <span data-ttu-id="f5a1e-205">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-205">Alias</span></span> | <span data-ttu-id="f5a1e-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-206">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-207">Microsoft.Cache/Redis/enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="f5a1e-207">Microsoft.Cache/Redis/enableNonSslPort</span></span> | <span data-ttu-id="f5a1e-208">Instellen is of Redis-server voor Hallo niet-ssl-poort (6379) ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-208">Set whether hello non-ssl Redis server port (6379) is enabled.</span></span> |
| <span data-ttu-id="f5a1e-209">Microsoft.Cache/Redis/shardCount</span><span class="sxs-lookup"><span data-stu-id="f5a1e-209">Microsoft.Cache/Redis/shardCount</span></span> | <span data-ttu-id="f5a1e-210">Het aantal shards toobe gemaakt op een Cluster Premium Cache Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-210">Set hello number of shards toobe created on a Premium Cluster Cache.</span></span>  |
| <span data-ttu-id="f5a1e-211">Microsoft.Cache/Redis/sku.capacity</span><span class="sxs-lookup"><span data-stu-id="f5a1e-211">Microsoft.Cache/Redis/sku.capacity</span></span> | <span data-ttu-id="f5a1e-212">Hallo-grootte van Hallo Redis-cache toodeploy instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-212">Set hello size of hello Redis cache toodeploy.</span></span>  |
| <span data-ttu-id="f5a1e-213">Microsoft.Cache/Redis/sku.family</span><span class="sxs-lookup"><span data-stu-id="f5a1e-213">Microsoft.Cache/Redis/sku.family</span></span> | <span data-ttu-id="f5a1e-214">Hallo SKU-familie toouse ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-214">Set hello SKU family toouse.</span></span> |
| <span data-ttu-id="f5a1e-215">Microsoft.Cache/Redis/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-215">Microsoft.Cache/Redis/sku.name</span></span> | <span data-ttu-id="f5a1e-216">Hallo-type van Redis-Cache toodeploy instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-216">Set hello type of Redis Cache toodeploy.</span></span> |

<span data-ttu-id="f5a1e-217">**Microsoft.Cdn/profiles**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-217">**Microsoft.Cdn/profiles**</span></span>

| <span data-ttu-id="f5a1e-218">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-218">Alias</span></span> | <span data-ttu-id="f5a1e-219">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-219">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-220">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-220">Microsoft.CDN/profiles/sku.name</span></span> | <span data-ttu-id="f5a1e-221">Naam van de Hallo Hallo prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-221">Set hello name of hello pricing tier.</span></span> |

<span data-ttu-id="f5a1e-222">**Microsoft.Compute/disks**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-222">**Microsoft.Compute/disks**</span></span>

| <span data-ttu-id="f5a1e-223">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-223">Alias</span></span> | <span data-ttu-id="f5a1e-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-224">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-225">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="f5a1e-225">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="f5a1e-226">Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-226">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-227">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="f5a1e-227">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="f5a1e-228">Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-228">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-229">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="f5a1e-229">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="f5a1e-230">Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-230">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-231">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="f5a1e-231">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="f5a1e-232">Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-232">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |


<span data-ttu-id="f5a1e-233">**Microsoft.Compute/virtualMachines**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-233">**Microsoft.Compute/virtualMachines**</span></span>

| <span data-ttu-id="f5a1e-234">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-234">Alias</span></span> | <span data-ttu-id="f5a1e-235">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-235">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-236">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="f5a1e-236">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="f5a1e-237">Hallo-id van de afbeelding Hallo gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-237">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-238">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="f5a1e-238">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="f5a1e-239">Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-239">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-240">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="f5a1e-240">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="f5a1e-241">Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-241">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-242">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="f5a1e-242">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="f5a1e-243">Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-243">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-244">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="f5a1e-244">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="f5a1e-245">Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-245">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-246">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="f5a1e-246">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="f5a1e-247">Instellen dat Hallo installatiekopie of schijf gelicentieerde lokaal is.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-247">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="f5a1e-248">Deze waarde wordt alleen gebruikt voor installatiekopieën die Windows Server-besturingssysteem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-248">This value is only used for images that contain hello Windows Server operating system.</span></span>  |
| <span data-ttu-id="f5a1e-249">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="f5a1e-249">Microsoft.Compute/virtualMachines/imageOffer</span></span> | <span data-ttu-id="f5a1e-250">Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-250">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-251">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="f5a1e-251">Microsoft.Compute/virtualMachines/imagePublisher</span></span> | <span data-ttu-id="f5a1e-252">Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-252">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-253">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="f5a1e-253">Microsoft.Compute/virtualMachines/imageSku</span></span> | <span data-ttu-id="f5a1e-254">Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-254">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-255">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="f5a1e-255">Microsoft.Compute/virtualMachines/imageVersion</span></span> | <span data-ttu-id="f5a1e-256">Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-256">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span><span class="sxs-lookup"><span data-stu-id="f5a1e-257">Microsoft.Compute/virtualMachines/osDisk.Uri</span></span> | <span data-ttu-id="f5a1e-258">Stel Hallo vhd-URI.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-258">Set hello vhd URI.</span></span> |
| <span data-ttu-id="f5a1e-259">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-259">Microsoft.Compute/virtualMachines/sku.name</span></span> | <span data-ttu-id="f5a1e-260">Hallo-grootte van Hallo virtuele machine instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-260">Set hello size of hello virtual machine.</span></span> |

<span data-ttu-id="f5a1e-261">**Microsoft.Compute/virtualMachines/extensions**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-261">**Microsoft.Compute/virtualMachines/extensions**</span></span>

| <span data-ttu-id="f5a1e-262">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-262">Alias</span></span> | <span data-ttu-id="f5a1e-263">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-263">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-264">Microsoft.Compute/virtualMachines/extensions/publisher</span><span class="sxs-lookup"><span data-stu-id="f5a1e-264">Microsoft.Compute/virtualMachines/extensions/publisher</span></span> | <span data-ttu-id="f5a1e-265">Hallo-naam van uitgever Hallo-extensie instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-265">Set hello name of hello extension’s publisher.</span></span> |
| <span data-ttu-id="f5a1e-266">Microsoft.Compute/virtualMachines/extensions/type</span><span class="sxs-lookup"><span data-stu-id="f5a1e-266">Microsoft.Compute/virtualMachines/extensions/type</span></span> | <span data-ttu-id="f5a1e-267">Hallo-type van extensie instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-267">Set hello type of extension.</span></span> |
| <span data-ttu-id="f5a1e-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="f5a1e-268">Microsoft.Compute/virtualMachines/extensions/typeHandlerVersion</span></span> | <span data-ttu-id="f5a1e-269">Hallo-versie van de uitbreiding van Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-269">Set hello version of hello extension.</span></span> |

<span data-ttu-id="f5a1e-270">**Microsoft.Compute/virtualMachineScaleSets**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-270">**Microsoft.Compute/virtualMachineScaleSets**</span></span>

| <span data-ttu-id="f5a1e-271">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-271">Alias</span></span> | <span data-ttu-id="f5a1e-272">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-272">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-273">Microsoft.Compute/imageId</span><span class="sxs-lookup"><span data-stu-id="f5a1e-273">Microsoft.Compute/imageId</span></span> | <span data-ttu-id="f5a1e-274">Hallo-id van de afbeelding Hallo gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-274">Set hello identifier of hello image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-275">Microsoft.Compute/imageOffer</span><span class="sxs-lookup"><span data-stu-id="f5a1e-275">Microsoft.Compute/imageOffer</span></span> | <span data-ttu-id="f5a1e-276">Set Hallo aanbieding van Hallo platforminstallatiekopie of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-276">Set hello offer of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-277">Microsoft.Compute/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="f5a1e-277">Microsoft.Compute/imagePublisher</span></span> | <span data-ttu-id="f5a1e-278">Set Hallo uitgever van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-278">Set hello publisher of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-279">Microsoft.Compute/imageSku</span><span class="sxs-lookup"><span data-stu-id="f5a1e-279">Microsoft.Compute/imageSku</span></span> | <span data-ttu-id="f5a1e-280">Set Hallo SKU van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-280">Set hello SKU of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-281">Microsoft.Compute/imageVersion</span><span class="sxs-lookup"><span data-stu-id="f5a1e-281">Microsoft.Compute/imageVersion</span></span> | <span data-ttu-id="f5a1e-282">Set Hallo versie van de besturingssysteemkopie Hallo of marketplace-installatiekopie gebruikt toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-282">Set hello version of hello platform image or marketplace image used toocreate hello virtual machine.</span></span> |
| <span data-ttu-id="f5a1e-283">Microsoft.Compute/licenseType</span><span class="sxs-lookup"><span data-stu-id="f5a1e-283">Microsoft.Compute/licenseType</span></span> | <span data-ttu-id="f5a1e-284">Instellen dat Hallo installatiekopie of schijf gelicentieerde lokaal is.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-284">Set that hello image or disk is licensed on-premises.</span></span> <span data-ttu-id="f5a1e-285">Deze waarde wordt alleen gebruikt voor installatiekopieën die Windows Server-besturingssysteem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-285">This value is only used for images that contain hello Windows Server operating system.</span></span> |
| <span data-ttu-id="f5a1e-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span><span class="sxs-lookup"><span data-stu-id="f5a1e-286">Microsoft.Compute/VirtualMachineScaleSets/computerNamePrefix</span></span> | <span data-ttu-id="f5a1e-287">Voorvoegsel voor de computernaam Hallo voor alle Hallo virtuele machines in de schaalset Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-287">Set hello computer name prefix for all  hello virtual machines in hello scale set.</span></span> |
| <span data-ttu-id="f5a1e-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span><span class="sxs-lookup"><span data-stu-id="f5a1e-288">Microsoft.Compute/VirtualMachineScaleSets/osdisk.imageUrl</span></span> | <span data-ttu-id="f5a1e-289">Hallo blob-URI voor de gebruikersinstallatiekopie van de instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-289">Set hello blob URI for user image.</span></span> |
| <span data-ttu-id="f5a1e-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span><span class="sxs-lookup"><span data-stu-id="f5a1e-290">Microsoft.Compute/VirtualMachineScaleSets/osdisk.vhdContainers</span></span> | <span data-ttu-id="f5a1e-291">Hallo container-URL's die gebruikt toostore besturingssysteem schijven voor Hallo scale set zijn instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-291">Set hello container URLs that are used toostore operating system disks for hello scale set.</span></span> |
| <span data-ttu-id="f5a1e-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-292">Microsoft.Compute/VirtualMachineScaleSets/sku.name</span></span> | <span data-ttu-id="f5a1e-293">Hallo-grootte van virtuele machines in een scale-set instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-293">Set hello size of virtual machines in a scale set.</span></span> |
| <span data-ttu-id="f5a1e-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span><span class="sxs-lookup"><span data-stu-id="f5a1e-294">Microsoft.Compute/VirtualMachineScaleSets/sku.tier</span></span> | <span data-ttu-id="f5a1e-295">Hallo-laag van virtuele machines in een scale-set instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-295">Set hello tier of virtual machines in a scale set.</span></span> |
  
<span data-ttu-id="f5a1e-296">**Microsoft.Network/applicationGateways**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-296">**Microsoft.Network/applicationGateways**</span></span>

| <span data-ttu-id="f5a1e-297">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-297">Alias</span></span> | <span data-ttu-id="f5a1e-298">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-298">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-299">Microsoft.Network/applicationGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-299">Microsoft.Network/applicationGateways/sku.name</span></span> | <span data-ttu-id="f5a1e-300">Hallo-grootte van Hallo gateway instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-300">Set hello size of hello gateway.</span></span> |

<span data-ttu-id="f5a1e-301">**Microsoft.Network/virtualNetworkGateways**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-301">**Microsoft.Network/virtualNetworkGateways**</span></span>

| <span data-ttu-id="f5a1e-302">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-302">Alias</span></span> | <span data-ttu-id="f5a1e-303">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-303">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span><span class="sxs-lookup"><span data-stu-id="f5a1e-304">Microsoft.Network/virtualNetworkGateways/gatewayType</span></span> | <span data-ttu-id="f5a1e-305">Hallo-type van deze virtuele netwerkgateway instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-305">Set hello type of this virtual network gateway.</span></span> |
| <span data-ttu-id="f5a1e-306">Microsoft.Network/virtualNetworkGateways/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-306">Microsoft.Network/virtualNetworkGateways/sku.name</span></span> | <span data-ttu-id="f5a1e-307">Hallo-gateway SKU-naam worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-307">Set hello gateway SKU name.</span></span> |

<span data-ttu-id="f5a1e-308">**Microsoft.Sql/servers**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-308">**Microsoft.Sql/servers**</span></span>

| <span data-ttu-id="f5a1e-309">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-309">Alias</span></span> | <span data-ttu-id="f5a1e-310">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-310">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-311">Microsoft.Sql/servers/version</span><span class="sxs-lookup"><span data-stu-id="f5a1e-311">Microsoft.Sql/servers/version</span></span> | <span data-ttu-id="f5a1e-312">Hallo-versie van Hallo server instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-312">Set hello version of hello server.</span></span> |

<span data-ttu-id="f5a1e-313">**Microsoft.Sql/databases**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-313">**Microsoft.Sql/databases**</span></span>

| <span data-ttu-id="f5a1e-314">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-314">Alias</span></span> | <span data-ttu-id="f5a1e-315">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-315">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-316">Microsoft.Sql/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="f5a1e-316">Microsoft.Sql/servers/databases/edition</span></span> | <span data-ttu-id="f5a1e-317">Hallo-editie van Hallo database instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-317">Set hello edition of hello database.</span></span> |
| <span data-ttu-id="f5a1e-318">Microsoft.Sql/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="f5a1e-318">Microsoft.Sql/servers/databases/elasticPoolName</span></span> | <span data-ttu-id="f5a1e-319">Naam van de set Hallo van elastische groepdatabase Hallo Hallo is in.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-319">Set hello name of hello elastic pool hello database is in.</span></span> |
| <span data-ttu-id="f5a1e-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="f5a1e-320">Microsoft.Sql/servers/databases/requestedServiceObjectiveId</span></span> | <span data-ttu-id="f5a1e-321">Hallo geconfigureerd service level objective-ID van Hallo database instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-321">Set hello configured service level objective ID of hello database.</span></span> |
| <span data-ttu-id="f5a1e-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="f5a1e-322">Microsoft.Sql/servers/databases/requestedServiceObjectiveName</span></span> | <span data-ttu-id="f5a1e-323">Hallo-naam van serviceniveaudoelstelling van Hallo database Hallo geconfigureerd instellen.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-323">Set hello name of hello configured service level objective of hello database.</span></span>  |

<span data-ttu-id="f5a1e-324">**Microsoft.Sql/elasticpools**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-324">**Microsoft.Sql/elasticpools**</span></span>

| <span data-ttu-id="f5a1e-325">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-325">Alias</span></span> | <span data-ttu-id="f5a1e-326">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-326">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-327">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="f5a1e-327">servers/elasticpools</span></span> | <span data-ttu-id="f5a1e-328">Microsoft.Sql/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="f5a1e-328">Microsoft.Sql/servers/elasticPools/dtu</span></span> | <span data-ttu-id="f5a1e-329">Set Hallo totaal gedeeld DTU voor de elastische pool Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-329">Set hello total shared DTU for hello database elastic pool.</span></span> |
| <span data-ttu-id="f5a1e-330">servers/elasticpools</span><span class="sxs-lookup"><span data-stu-id="f5a1e-330">servers/elasticpools</span></span> | <span data-ttu-id="f5a1e-331">Microsoft.Sql/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="f5a1e-331">Microsoft.Sql/servers/elasticPools/edition</span></span> | <span data-ttu-id="f5a1e-332">Hallo-editie van de elastische pool Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-332">Set hello edition of hello elastic pool.</span></span> |

<span data-ttu-id="f5a1e-333">**Microsoft.Storage/storageAccounts**</span><span class="sxs-lookup"><span data-stu-id="f5a1e-333">**Microsoft.Storage/storageAccounts**</span></span>

| <span data-ttu-id="f5a1e-334">Alias</span><span class="sxs-lookup"><span data-stu-id="f5a1e-334">Alias</span></span> | <span data-ttu-id="f5a1e-335">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f5a1e-335">Description</span></span> |
| ----- | ----------- |
| <span data-ttu-id="f5a1e-336">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="f5a1e-336">Microsoft.Storage/storageAccounts/accessTier</span></span> | <span data-ttu-id="f5a1e-337">Set gebruikt voor facturering Hallo toegangslaag.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-337">Set hello access tier used for billing.</span></span> |
| <span data-ttu-id="f5a1e-338">Microsoft.Storage/storageAccounts/accountType</span><span class="sxs-lookup"><span data-stu-id="f5a1e-338">Microsoft.Storage/storageAccounts/accountType</span></span> | <span data-ttu-id="f5a1e-339">Hallo SKU-naam worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-339">Set hello SKU name.</span></span> |
| <span data-ttu-id="f5a1e-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="f5a1e-340">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span> | <span data-ttu-id="f5a1e-341">Instellen of Hallo service Hallo gegevens versleutelt zoals deze is opgeslagen in Hallo blob storage-service.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-341">Set whether hello service encrypts hello data as it is stored in hello blob storage service.</span></span> |
| <span data-ttu-id="f5a1e-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span><span class="sxs-lookup"><span data-stu-id="f5a1e-342">Microsoft.Storage/storageAccounts/enableFileEncryption</span></span> | <span data-ttu-id="f5a1e-343">Instellen of Hallo service Hallo gegevens versleutelt zoals deze is opgeslagen in Hallo file storage-service.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-343">Set whether hello service encrypts hello data as it is stored in hello file storage service.</span></span> |
| <span data-ttu-id="f5a1e-344">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="f5a1e-344">Microsoft.Storage/storageAccounts/sku.name</span></span> | <span data-ttu-id="f5a1e-345">Hallo SKU-naam worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-345">Set hello SKU name.</span></span> |
| <span data-ttu-id="f5a1e-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span><span class="sxs-lookup"><span data-stu-id="f5a1e-346">Microsoft.Storage/storageAccounts/supportsHttpsTrafficOnly</span></span> | <span data-ttu-id="f5a1e-347">Tooallow alleen https-verkeer toostorage service ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-347">Set tooallow only https traffic toostorage service.</span></span> |


## <a name="policy-examples"></a><span data-ttu-id="f5a1e-348">Voorbeelden van beleid</span><span class="sxs-lookup"><span data-stu-id="f5a1e-348">Policy examples</span></span>

<span data-ttu-id="f5a1e-349">Hallo volgende onderwerpen bevatten voorbeelden van beleid:</span><span class="sxs-lookup"><span data-stu-id="f5a1e-349">hello following topics contain policy examples:</span></span>

* <span data-ttu-id="f5a1e-350">Zie voor voorbeelden van de tag beleidsregels, [bronbeleid voor tags toepassen](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-350">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="f5a1e-351">Zie voor voorbeelden van naamgeving en tekst patronen [resource-beleid toepassen op namen en tekst](resource-manager-policy-naming-convention.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-351">For examples of naming and text patterns, see [Apply resource policies for names and text](resource-manager-policy-naming-convention.md).</span></span>
* <span data-ttu-id="f5a1e-352">Zie voor voorbeelden van beleidsregels voor opslag [toepassen resourceaccounts beleid toostorage](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-352">For examples of storage policies, see [Apply resource policies toostorage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="f5a1e-353">Zie voor voorbeelden van beleidsregels voor virtuele machine [toepassen resource beleid tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) en [resource beleid tooWindows virtuele machines toepassen](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f5a1e-353">For examples of virtual machine policies, see [Apply resource policies tooLinux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies tooWindows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>


## <a name="next-steps"></a><span data-ttu-id="f5a1e-354">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5a1e-354">Next steps</span></span>
* <span data-ttu-id="f5a1e-355">Na het definiëren van een beleidsregel toewijzen tooa bereik.</span><span class="sxs-lookup"><span data-stu-id="f5a1e-355">After defining a policy rule, assign it tooa scope.</span></span> <span data-ttu-id="f5a1e-356">tooassign beleid via de portal hello, Zie [gebruik Azure portal tooassign en beheren van bronbeleid](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-356">tooassign policies through hello portal, see [Use Azure portal tooassign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="f5a1e-357">tooassign beleid via REST API, PowerShell of Azure CLI, Zie [toewijzen en beheren van beleid via script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-357">tooassign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="f5a1e-358">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-358">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="f5a1e-359">Hallo beleid schema wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="f5a1e-359">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 


---
title: portal voor bronbeleid aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure portal toocreate en beheren van Resource Manager-beleid. Beleidsregels kunnen worden toegepast op Hallo abonnement of de resource-groepen.
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
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: ce6413386317e532b63761a24458b85c996af4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-portal-tooassign-and-manage-resource-policies"></a><span data-ttu-id="64deb-104">Azure portal tooassign gebruiken en beheren van bronbeleid</span><span class="sxs-lookup"><span data-stu-id="64deb-104">Use Azure portal tooassign and manage resource policies</span></span>
<span data-ttu-id="64deb-105">Hello Azure-portal kunt u tooassign beleid tooresource resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="64deb-105">hello Azure portal enables you tooassign resource policies tooresource groups and subscriptions.</span></span> <span data-ttu-id="64deb-106">Hallo-gebruikersinterface kunt u eenvoudig tooselect Hallo beleid dat u tooassign wilt en parameterwaarden voor dat beleid toocustomize Hallo beleidsinstellingen opgeven.</span><span class="sxs-lookup"><span data-stu-id="64deb-106">hello user interface makes it easy tooselect hello policy that you want tooassign, and specify parameter values for that policy toocustomize hello policy settings.</span></span> 

<span data-ttu-id="64deb-107">een beleid via de portal Hallo tooassign, Hallo beleidsdefinitie moet al bestaan in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="64deb-107">tooassign a policy through hello portal, hello policy definition must already exist in your subscription.</span></span> <span data-ttu-id="64deb-108">Uw abonnement heeft diverse ingebouwde beleidsdefinities die gereed voor u tooassign tooresource groepen of abonnementen zijn.</span><span class="sxs-lookup"><span data-stu-id="64deb-108">Your subscription has several built-in policy definitions that are ready for you tooassign tooresource groups or subscriptions.</span></span> <span data-ttu-id="64deb-109">Ziet u deze beleidsregels ingebouwde en aangepaste beleidsregels die u hebt gedefinieerd wanneer met behulp van Hallo portal tooassign beleid.</span><span class="sxs-lookup"><span data-stu-id="64deb-109">You see these built-in policies and any custom policies you have defined when using hello portal tooassign policies.</span></span> <span data-ttu-id="64deb-110">Zie voor een inleiding toopolicies en hoe toodefine aangepast beleid [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="64deb-110">For an introduction toopolicies and how toodefine customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="64deb-111">Beleidsregels worden overgenomen door alle onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="64deb-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="64deb-112">Dus als een beleid toegepast tooa resourcegroep is, van toepassing tooall Hallo resources in die resourcegroep is.</span><span class="sxs-lookup"><span data-stu-id="64deb-112">So, if a policy is applied tooa resource group, it is applicable tooall hello resources in that resource group.</span></span> <span data-ttu-id="64deb-113">In dit artikel Hallo term **bereik** toohello resourcegroep of abonnement dat is toegewezen Hallo beleid verwijst.</span><span class="sxs-lookup"><span data-stu-id="64deb-113">In this article, hello term **scope** refers toohello resource group or subscription that is assigned hello policy.</span></span> 

<span data-ttu-id="64deb-114">Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).</span><span class="sxs-lookup"><span data-stu-id="64deb-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="64deb-115">Geen beleid toewijzen</span><span class="sxs-lookup"><span data-stu-id="64deb-115">Assign a policy</span></span>

1. <span data-ttu-id="64deb-116">tooassign een beleid tooeither een resourcegroep of abonnement, selecteert u de resourcegroep of abonnement.</span><span class="sxs-lookup"><span data-stu-id="64deb-116">tooassign a policy tooeither a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="64deb-117">Selecteer in de instellingen van Hallo **beleid**.</span><span class="sxs-lookup"><span data-stu-id="64deb-117">In hello settings, select **Policies**.</span></span>

   ![beleid selecteren](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="64deb-119">Selecteer toocreate een beleidstoewijzing voor deze scope **toewijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="64deb-119">toocreate a policy assignment for this scope, select **Add assignment**.</span></span>

   ![toewijzing toevoegen](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="64deb-121">Selecteer de gewenste tooassign Hallo-beleid.</span><span class="sxs-lookup"><span data-stu-id="64deb-121">Select hello policy you want tooassign.</span></span> <span data-ttu-id="64deb-122">Zelfs als u niet een beleid definities tooyour-abonnement hebt toegevoegd, ziet u Hallo ingebouwde beleidsregels die beschikbaar voor toewijzing zijn.</span><span class="sxs-lookup"><span data-stu-id="64deb-122">Even if you have not added any policy definitions tooyour subscription, you see hello built-in policies that are available for assignment.</span></span> <span data-ttu-id="64deb-123">Deze ingebouwde beleidsregels algemene scenario's uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="64deb-123">These built-in policies cover many common scenarios.</span></span>

   ![definitie selecteren](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="64deb-125">Na het selecteren van een beleid, ziet u een beschrijving van Hallo beleid en parameters voor dat beleid.</span><span class="sxs-lookup"><span data-stu-id="64deb-125">After selecting a policy, you see a description of hello policy, and any parameters for that policy.</span></span> <span data-ttu-id="64deb-126">Hallo volgende afbeelding ziet u bijvoorbeeld Hallo **toegestaan locaties** parameter is vereist voor Hallo-beleid die Hallo beschikbare locaties beperkt.</span><span class="sxs-lookup"><span data-stu-id="64deb-126">For example, hello following image shows hello **Allowed locations** parameter, which is required for hello policy that restricts hello available locations.</span></span>

   ![parameters weergeven](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="64deb-128">Selecteer via de gebruikersinterface Hallo Hallo waarden toospecify voor Hallo beleidsparameters (zoals Hallo locaties die kunnen worden gebruikt voor implementatie).</span><span class="sxs-lookup"><span data-stu-id="64deb-128">Through hello user interface, select hello values toospecify for hello policy parameters (such as hello locations that can be used for deployment).</span></span>

   ![Selecteer de parameterwaarden](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="64deb-130">Geef waarden op voor Hallo andere parameters.</span><span class="sxs-lookup"><span data-stu-id="64deb-130">Provide values for hello other parameters.</span></span> <span data-ttu-id="64deb-131">Hallo-scope wordt automatisch toegewezen op basis van het Hallo-blade die u hebt geselecteerd bij het starten van de beleidstoewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="64deb-131">hello scope is automatically assigned based on hello blade you selected when starting hello policy assignment.</span></span> <span data-ttu-id="64deb-132">Selecteer **OK** wanneer u gereed bent.</span><span class="sxs-lookup"><span data-stu-id="64deb-132">Select **OK** when done.</span></span>

   ![parameters definiëren](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="64deb-134">U hebt toegewezen Hallo beleid toohello opgegeven bereik.</span><span class="sxs-lookup"><span data-stu-id="64deb-134">You have assigned hello policy toohello specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="64deb-135">Beleidstoewijzingen weergeven</span><span class="sxs-lookup"><span data-stu-id="64deb-135">View policy assignments</span></span>

<span data-ttu-id="64deb-136">Na het toewijzen van een beleid voor bekijken u deze in de lijst Hallo van beleid voor deze scope.</span><span class="sxs-lookup"><span data-stu-id="64deb-136">After assigning a policy, you see it in hello list of policies for that scope.</span></span> <span data-ttu-id="64deb-137">Hallo **Details** tabblad bevat een overzicht van de beleidstoewijzing Hallo.</span><span class="sxs-lookup"><span data-stu-id="64deb-137">hello **Details** tab shows a summary of hello policy assignment.</span></span>

![details weergeven](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="64deb-139">Hallo **toewijzingsregel** tabblad ziet u Hallo JSON voor Hallo-beleidsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="64deb-139">hello **Assignment rule** tab shows hello JSON for hello policy definition.</span></span>

![regel voor agenttoewijzing weergeven](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="64deb-141">Wijzigen van een bestaande beleidstoewijzing van</span><span class="sxs-lookup"><span data-stu-id="64deb-141">Change an existing policy assignment</span></span>

<span data-ttu-id="64deb-142">selecteert u een beleid toochange **toewijzing bewerken** of **verwijderen**</span><span class="sxs-lookup"><span data-stu-id="64deb-142">toochange a policy, select **Edit assignment** or **Delete**</span></span>

![bewerken of verwijderen van toewijzing](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="64deb-144">Aangepast beleid toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="64deb-144">Assign custom policies</span></span>

<span data-ttu-id="64deb-145">Als u aangepaste beleidsregels hebt gedefinieerd in uw abonnement, zijn deze beleidsregels beschikbaar voor toewijzing via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="64deb-145">If you have defined custom policies in your subscription, those policies are available for assignment through hello portal.</span></span> <span data-ttu-id="64deb-146">Deze beleidsregels worden voorafgegaan door **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="64deb-146">Those policies are prefaced with **[Custom]**</span></span>

![aangepast beleid](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="64deb-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="64deb-148">Next steps</span></span>
* <span data-ttu-id="64deb-149">toolearn over Hallo JSON-syntaxis voor het definiëren van beleid, Zie [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="64deb-149">toolearn about hello JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="64deb-150">Abonnementen voor instructies over hoe ondernemingen tooeffectively Resource Manager kunt beheren, Zie [Azure enterprise scaffold - prescriptieve abonnement governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="64deb-150">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="64deb-151">Hallo beleid schema wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="64deb-151">hello policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 


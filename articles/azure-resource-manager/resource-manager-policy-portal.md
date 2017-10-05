---
title: Azure-portal voor bronbeleid | Microsoft Docs
description: Beschrijft hoe Azure-portal gebruiken om te maken en beheren van Resource Manager-beleid. Beleidsregels kunnen worden toegepast op de groepen abonnement of resourcegroep.
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
ms.openlocfilehash: 868b2cc1559053057d17b34c03e2e31347f399bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-portal-to-assign-and-manage-resource-policies"></a><span data-ttu-id="bb21d-104">Gebruik van Azure-portal toewijzen en beheren van bronbeleid</span><span class="sxs-lookup"><span data-stu-id="bb21d-104">Use Azure portal to assign and manage resource policies</span></span>
<span data-ttu-id="bb21d-105">De Azure-portal kunt u bronbeleid toewijzen aan resourcegroepen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="bb21d-105">The Azure portal enables you to assign resource policies to resource groups and subscriptions.</span></span> <span data-ttu-id="bb21d-106">De gebruikersinterface, kunt u gemakkelijk Selecteer het beleid dat u wilt toewijzen en geef parameterwaarden voor dat beleid voor het aanpassen van de beleidsinstellingen.</span><span class="sxs-lookup"><span data-stu-id="bb21d-106">The user interface makes it easy to select the policy that you want to assign, and specify parameter values for that policy to customize the policy settings.</span></span> 

<span data-ttu-id="bb21d-107">Als een beleid via de portal wilt toewijzen, moet de beleidsdefinitie al aanwezig in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="bb21d-107">To assign a policy through the portal, the policy definition must already exist in your subscription.</span></span> <span data-ttu-id="bb21d-108">Uw abonnement heeft diverse ingebouwde beleidsdefinities die gereed zijn voor u toewijzen aan resourcegroepen of abonnementen.</span><span class="sxs-lookup"><span data-stu-id="bb21d-108">Your subscription has several built-in policy definitions that are ready for you to assign to resource groups or subscriptions.</span></span> <span data-ttu-id="bb21d-109">Ziet u deze beleidsregels ingebouwde en aangepaste beleidsregels die u hebt gedefinieerd wanneer het beleid toe te wijzen met behulp van de portal.</span><span class="sxs-lookup"><span data-stu-id="bb21d-109">You see these built-in policies and any custom policies you have defined when using the portal to assign policies.</span></span> <span data-ttu-id="bb21d-110">Zie voor een inleiding tot beleid en het aangepaste beleid definiëren, [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bb21d-110">For an introduction to policies and how to define customized policy, see [Resource policy overview](resource-manager-policy.md).</span></span>

<span data-ttu-id="bb21d-111">Beleidsregels worden overgenomen door alle onderliggende resources.</span><span class="sxs-lookup"><span data-stu-id="bb21d-111">Policies are inherited by all child resources.</span></span> <span data-ttu-id="bb21d-112">Dus als een beleid wordt toegepast op een resourcegroep, is van toepassing op alle resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="bb21d-112">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span> <span data-ttu-id="bb21d-113">In dit artikel wordt de term **bereik** verwijst naar de resourcegroep of abonnement dat het beleid is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bb21d-113">In this article, the term **scope** refers to the resource group or subscription that is assigned the policy.</span></span> 

<span data-ttu-id="bb21d-114">Beleidsregels worden geëvalueerd wanneer maken en bijwerken van resources (plaatsen en PATCH operations).</span><span class="sxs-lookup"><span data-stu-id="bb21d-114">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="bb21d-115">Geen beleid toewijzen</span><span class="sxs-lookup"><span data-stu-id="bb21d-115">Assign a policy</span></span>

1. <span data-ttu-id="bb21d-116">Als u wilt een beleid toewijzen aan een resourcegroep of een abonnement, selecteert u de resourcegroep of abonnement.</span><span class="sxs-lookup"><span data-stu-id="bb21d-116">To assign a policy to either a resource group or subscription, select that resource group or subscription.</span></span> <span data-ttu-id="bb21d-117">Selecteer in de instellingen voor **beleid**.</span><span class="sxs-lookup"><span data-stu-id="bb21d-117">In the settings, select **Policies**.</span></span>

   ![beleid selecteren](./media/resource-manager-policy-portal/select-policies.png)

2. <span data-ttu-id="bb21d-119">Selecteer voor het maken van de beleidstoewijzing van een voor deze scope **toewijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bb21d-119">To create a policy assignment for this scope, select **Add assignment**.</span></span>

   ![toewijzing toevoegen](./media/resource-manager-policy-portal/add-assignment.png)

3. <span data-ttu-id="bb21d-121">Selecteer het beleid dat u wilt toewijzen.</span><span class="sxs-lookup"><span data-stu-id="bb21d-121">Select the policy you want to assign.</span></span> <span data-ttu-id="bb21d-122">Zelfs als u hebt beleidsdefinities niet toegevoegd aan uw abonnement, ziet u de ingebouwde beleidsregels die beschikbaar voor toewijzing zijn.</span><span class="sxs-lookup"><span data-stu-id="bb21d-122">Even if you have not added any policy definitions to your subscription, you see the built-in policies that are available for assignment.</span></span> <span data-ttu-id="bb21d-123">Deze ingebouwde beleidsregels algemene scenario's uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="bb21d-123">These built-in policies cover many common scenarios.</span></span>

   ![definitie selecteren](./media/resource-manager-policy-portal/select-definition.png)

4. <span data-ttu-id="bb21d-125">Na het selecteren van een beleid, raadpleegt u een beschrijving van het beleid en parameters voor dat beleid.</span><span class="sxs-lookup"><span data-stu-id="bb21d-125">After selecting a policy, you see a description of the policy, and any parameters for that policy.</span></span> <span data-ttu-id="bb21d-126">Bijvoorbeeld de volgende afbeelding toont de **toegestaan locaties** parameter, die is vereist voor het beleid dat Hiermee beperkt u de beschikbare locaties.</span><span class="sxs-lookup"><span data-stu-id="bb21d-126">For example, the following image shows the **Allowed locations** parameter, which is required for the policy that restricts the available locations.</span></span>

   ![parameters weergeven](./media/resource-manager-policy-portal/show-parameters.png)

5. <span data-ttu-id="bb21d-128">Selecteer de waarden op te geven voor de beleidsparameters (zoals de locaties die kunnen worden gebruikt voor implementatie) via de gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="bb21d-128">Through the user interface, select the values to specify for the policy parameters (such as the locations that can be used for deployment).</span></span>

   ![Selecteer de parameterwaarden](./media/resource-manager-policy-portal/select-parameters.png)

6. <span data-ttu-id="bb21d-130">Geef waarden op voor de andere parameters.</span><span class="sxs-lookup"><span data-stu-id="bb21d-130">Provide values for the other parameters.</span></span> <span data-ttu-id="bb21d-131">De scope wordt automatisch toegewezen op basis van de blade die u hebt geselecteerd bij het starten van de beleidstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="bb21d-131">The scope is automatically assigned based on the blade you selected when starting the policy assignment.</span></span> <span data-ttu-id="bb21d-132">Selecteer **OK** wanneer u gereed bent.</span><span class="sxs-lookup"><span data-stu-id="bb21d-132">Select **OK** when done.</span></span>

   ![parameters definiëren](./media/resource-manager-policy-portal/define-parameters.png)

  <span data-ttu-id="bb21d-134">U kunt het beleid hebt toegewezen aan het opgegeven bereik.</span><span class="sxs-lookup"><span data-stu-id="bb21d-134">You have assigned the policy to the specified scope.</span></span>

## <a name="view-policy-assignments"></a><span data-ttu-id="bb21d-135">Beleidstoewijzingen weergeven</span><span class="sxs-lookup"><span data-stu-id="bb21d-135">View policy assignments</span></span>

<span data-ttu-id="bb21d-136">Na het toewijzen van een beleid voor bekijken u deze in de lijst met beleidsregels voor deze scope.</span><span class="sxs-lookup"><span data-stu-id="bb21d-136">After assigning a policy, you see it in the list of policies for that scope.</span></span> <span data-ttu-id="bb21d-137">De **Details** tabblad bevat een overzicht van de beleidstoewijzing.</span><span class="sxs-lookup"><span data-stu-id="bb21d-137">The **Details** tab shows a summary of the policy assignment.</span></span>

![details weergeven](./media/resource-manager-policy-portal/show-details.png)

<span data-ttu-id="bb21d-139">De **toewijzingsregel** tabblad ziet u de JSON van de beleidsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="bb21d-139">The **Assignment rule** tab shows the JSON for the policy definition.</span></span>

![regel voor agenttoewijzing weergeven](./media/resource-manager-policy-portal/show-assignment-rule.png)

## <a name="change-an-existing-policy-assignment"></a><span data-ttu-id="bb21d-141">Wijzigen van een bestaande beleidstoewijzing van</span><span class="sxs-lookup"><span data-stu-id="bb21d-141">Change an existing policy assignment</span></span>

<span data-ttu-id="bb21d-142">Als u een beleid, selecteert **toewijzing bewerken** of **verwijderen**</span><span class="sxs-lookup"><span data-stu-id="bb21d-142">To change a policy, select **Edit assignment** or **Delete**</span></span>

![bewerken of verwijderen van toewijzing](./media/resource-manager-policy-portal/edit-delete-policy.png)

## <a name="assign-custom-policies"></a><span data-ttu-id="bb21d-144">Aangepast beleid toe te wijzen</span><span class="sxs-lookup"><span data-stu-id="bb21d-144">Assign custom policies</span></span>

<span data-ttu-id="bb21d-145">Als u aangepaste beleidsregels hebt gedefinieerd in uw abonnement, zijn deze beleidsregels beschikbaar voor toewijzing via de portal.</span><span class="sxs-lookup"><span data-stu-id="bb21d-145">If you have defined custom policies in your subscription, those policies are available for assignment through the portal.</span></span> <span data-ttu-id="bb21d-146">Deze beleidsregels worden voorafgegaan door **[Custom]**</span><span class="sxs-lookup"><span data-stu-id="bb21d-146">Those policies are prefaced with **[Custom]**</span></span>

![aangepast beleid](./media/resource-manager-policy-portal/show-custom-policy.png)

## <a name="next-steps"></a><span data-ttu-id="bb21d-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb21d-148">Next steps</span></span>
* <span data-ttu-id="bb21d-149">Zie voor meer informatie over de JSON-syntaxis voor het definiëren van beleid, [Resource overzicht](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="bb21d-149">To learn about the JSON syntax for defining policies, see [Resource policy overview](resource-manager-policy.md).</span></span>
* <span data-ttu-id="bb21d-150">Voor begeleiding bij de manier waarop ondernemingen Resource Manager effectief kunnen gebruiken voor het beheer van abonnementen, gaat u naar [Azure enterprise-platform - Prescriptieve abonnementsgovernance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="bb21d-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="bb21d-151">Het schema van het beleid wordt gepubliceerd op [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="bb21d-151">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 


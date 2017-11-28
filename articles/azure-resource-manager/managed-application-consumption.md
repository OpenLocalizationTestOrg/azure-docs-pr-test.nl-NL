---
title: een Azure aaaConsume beheerde toepassing | Microsoft Docs
description: Beschrijft hoe een klant maakt u een Azure beheerde toepassing uit gepubliceerde bestanden.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="5d944-103">Een interne beheerde toepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="5d944-103">Consume an internal managed application</span></span>

<span data-ttu-id="5d944-104">U kunt Azure verbruiken [beheerde toepassingen](managed-application-overview.md) die bestemd zijn voor leden van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="5d944-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="5d944-105">Bijvoorbeeld, kunt u beheerde toepassingen van uw IT-afdeling die de organisatie-normen te waarborgen.</span><span class="sxs-lookup"><span data-stu-id="5d944-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="5d944-106">Deze beheerde toepassingen zijn beschikbaar via Hallo Servicecatalogus, het niet hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="5d944-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="5d944-107">Voordat u doorgaat met dit artikel, moet u een beheerde toepassing beschikbaar is in de Servicecatalogus Hallo hebben voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5d944-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="5d944-108">Als iemand zich in uw organisatie geen beheerde toepassingen gemaakt nog, raadpleegt u [publiceren van een beheerde toepassingsservices voor intern verbruik](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5d944-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="5d944-109">Op dit moment kunt u Azure CLI of hello Azure portal tooconsume beheerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5d944-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="5d944-110">Hallo beheerde toepassing maken met behulp van Hallo-portal</span><span class="sxs-lookup"><span data-stu-id="5d944-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="5d944-111">toodeploy een beheerde toepassing via Hallo-portal, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5d944-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="5d944-112">Ga toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="5d944-112">Go toohello Azure portal.</span></span> <span data-ttu-id="5d944-113">Zoeken naar **Servicecatalogus beheerde toepassing**.</span><span class="sxs-lookup"><span data-stu-id="5d944-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Servicecatalogus voor beheerde toepassing](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="5d944-115">Selecteer Hallo beheerde toepassing die u wilt dat toocreate uit de lijst met beschikbare oplossingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d944-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="5d944-116">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="5d944-116">Select **Create**.</span></span>

   ![Selectie van de beheerde toepassing](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="5d944-118">Geef waarden op voor het Hallo-parameters die vereist tooprovision Hallo resources zijn.</span><span class="sxs-lookup"><span data-stu-id="5d944-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="5d944-119">Selecteer **West-Centraal VS** voor de locatie.</span><span class="sxs-lookup"><span data-stu-id="5d944-119">Select **West Central US** for location.</span></span> <span data-ttu-id="5d944-120">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="5d944-120">Select **OK**.</span></span>

   ![Parameters voor de beheerde toepassing](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="5d944-122">Hallo sjabloon valideert Hallo-waarden die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5d944-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="5d944-123">Als de validatie slaagt, selecteert u **OK** toostart Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="5d944-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Validatie van de beheerde toepassing](./media/managed-application-consumption/validation.png)

<span data-ttu-id="5d944-125">Nadat Hallo-implementatie is voltooid, worden de juiste resources Hallo in Hallo sjabloon worden gedefinieerd ingericht in beheerde resourcegroep Hallo die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5d944-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="5d944-126">Hallo beheerde toepassing maken met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5d944-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="5d944-127">Er zijn twee manieren toocreate een beheerde toepassing met Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="5d944-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="5d944-128">Hallo-opdracht voor het maken van beheerde toepassingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d944-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="5d944-129">Hallo reguliere sjabloon implementatieopdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5d944-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="5d944-130">Implementatieopdracht Hallo-sjabloon gebruiken</span><span class="sxs-lookup"><span data-stu-id="5d944-130">Use hello template deployment command</span></span>

<span data-ttu-id="5d944-131">Implementeer Hallo applianceMainTemplate.json bestand die Hallo leverancier gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d944-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="5d944-132">Vervolgens maakt u twee resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="5d944-132">Then create two resource groups.</span></span> <span data-ttu-id="5d944-133">Hallo eerste resourcegroep is waar hello bron beheerde toepassing wordt gemaakt: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="5d944-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="5d944-134">Hallo tweede resourcegroep bevat alle Hallo resources die zijn gedefinieerd in mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5d944-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="5d944-135">Deze resourcegroep wordt beheerd door Hallo ISV.</span><span class="sxs-lookup"><span data-stu-id="5d944-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="5d944-136">Gebruik `westcentralus` als locatie van resourcegroep Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d944-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="5d944-137">toodeploy applianceMainTemplate.json in mainResourceGroup, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5d944-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="5d944-138">Na het Hallo voorafgaand aan de sjabloon wordt uitgevoerd, wordt u gevraagd waarden Hallo Hallo-parameters die zijn gedefinieerd in de sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d944-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="5d944-139">Bovendien toohello parameters die zijn vereist voor tooprovision resources in een sjabloon, moet u twee belangrijke parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="5d944-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="5d944-140">**managedResourceGroupId**: Hallo-ID van Hallo resource met Hallo resources groeperen in applianceMainTemplate.json gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5d944-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="5d944-141">Hallo-ID is van het formulier Hallo `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="5d944-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="5d944-142">In de Hallo voorgaande voorbeeld, het Hallo-ID van `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="5d944-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="5d944-143">**applianceDefinitionId**: Hallo-ID van Hallo beheerd bron van de definitie van toepassing.</span><span class="sxs-lookup"><span data-stu-id="5d944-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="5d944-144">Deze waarde wordt verstrekt door Hallo ISV.</span><span class="sxs-lookup"><span data-stu-id="5d944-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="5d944-145">Hallo uitgever moet verlenen toegang toohello resourcegroep met definitie van de toepassing hello beheerd.</span><span class="sxs-lookup"><span data-stu-id="5d944-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="5d944-146">Hallo definitie resource is gemaakt in Hallo publisher abonnement.</span><span class="sxs-lookup"><span data-stu-id="5d944-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="5d944-147">Daarom moet een gebruiker, groep of toepassing in Hallo klant tenant leestoegang toothis resource.</span><span class="sxs-lookup"><span data-stu-id="5d944-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="5d944-148">Nadat het Hallo-implementatie wordt voltooid, ziet u Hallo beheerde toepassing in mainResourceGroup wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d944-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="5d944-149">Hallo storageAccount resource is gemaakt in managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="5d944-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="5d944-150">Gebruik Hallo opdracht maken</span><span class="sxs-lookup"><span data-stu-id="5d944-150">Use hello create command</span></span>

<span data-ttu-id="5d944-151">U kunt Hallo `az managedapp create` opdracht toocreate een beheerde toepassing hello beheerd definitie van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5d944-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="5d944-152">**apparaat-definitie-Id**: Hallo bron-ID van Hallo definitie van toepassing is gemaakt in de voorgaande stap Hallo beheerd.</span><span class="sxs-lookup"><span data-stu-id="5d944-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="5d944-153">tooobtain deze ID Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5d944-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="5d944-154">Deze opdracht retourneert de definitie van de toepassing hello beheerd.</span><span class="sxs-lookup"><span data-stu-id="5d944-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="5d944-155">U moet Hallo-waarde van eigenschap van Hallo-ID.</span><span class="sxs-lookup"><span data-stu-id="5d944-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="5d944-156">**beheerde-rg-id**: Hallo-naam van Hallo resource met Hallo resources groeperen in applianceMainTemplate.json gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="5d944-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="5d944-157">Deze resourcegroep hoort Hallo beheerde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5d944-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="5d944-158">Het wordt beheerd door Hallo uitgever.</span><span class="sxs-lookup"><span data-stu-id="5d944-158">It's managed by hello publisher.</span></span> <span data-ttu-id="5d944-159">Als deze nog niet bestaat, wordt deze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d944-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="5d944-160">**resourcegroep**: Hallo resourcegroep waar Hallo toepassingsbron beheerd wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5d944-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="5d944-161">Hallo Microsoft.Solutions/appliance resource woont in deze resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5d944-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="5d944-162">**parameters**: Hallo parameters die nodig zijn voor het Hallo-resources die zijn gedefinieerd in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="5d944-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="5d944-163">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="5d944-163">Known issues</span></span>

<span data-ttu-id="5d944-164">Deze preview-versie bevat Hallo problemen te volgen:</span><span class="sxs-lookup"><span data-stu-id="5d944-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="5d944-165">Een interne serverfout 500 wordt weergegeven tijdens het maken van de toepassing hello beheerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="5d944-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="5d944-166">Als u dit probleem ondervindt, is het waarschijnlijk toobe onregelmatige.</span><span class="sxs-lookup"><span data-stu-id="5d944-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="5d944-167">Hallo-bewerking opnieuw uit.</span><span class="sxs-lookup"><span data-stu-id="5d944-167">Retry hello operation.</span></span>
* <span data-ttu-id="5d944-168">Een nieuwe resourcegroep is nodig voor beheerde Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="5d944-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="5d944-169">Als u een bestaande resourcegroep gebruikt, mislukt de Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="5d944-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="5d944-170">Hallo resourcegroep met Hallo Microsoft.Solutions/appliances bron moet worden gemaakt in Hallo **westcentralus** locatie.</span><span class="sxs-lookup"><span data-stu-id="5d944-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d944-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5d944-171">Next steps</span></span>

* <span data-ttu-id="5d944-172">Zie voor een inleiding toomanaged toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5d944-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5d944-173">Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="5d944-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="5d944-174">Zie voor meer informatie over publiceren beheerde toepassingen toohello Azure Marketplace [Azure beheerde toepassingen in Hallo Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="5d944-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="5d944-175">Zie voor meer informatie over het gebruiken van een beheerde toepassing hello Marketplace [Azure gebruiken beheerde toepassingen in Hallo Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="5d944-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>

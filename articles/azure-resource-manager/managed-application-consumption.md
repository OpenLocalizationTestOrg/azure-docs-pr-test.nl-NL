---
title: Een Azure gebruiken voor beheerde toepassing | Microsoft Docs
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
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="614dd-103">Een interne beheerde toepassing gebruiken</span><span class="sxs-lookup"><span data-stu-id="614dd-103">Consume an internal managed application</span></span>

<span data-ttu-id="614dd-104">U kunt Azure verbruiken [beheerde toepassingen](managed-application-overview.md) die bestemd zijn voor leden van uw organisatie.</span><span class="sxs-lookup"><span data-stu-id="614dd-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="614dd-105">Bijvoorbeeld, kunt u beheerde toepassingen van uw IT-afdeling die de organisatie-normen te waarborgen.</span><span class="sxs-lookup"><span data-stu-id="614dd-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="614dd-106">Deze beheerde toepassingen zijn beschikbaar via de Servicecatalogus, niet de Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="614dd-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="614dd-107">Voordat u doorgaat met dit artikel, moet u een beheerde toepassing beschikbaar is in de Servicecatalogus hebben voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="614dd-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="614dd-108">Als iemand zich in uw organisatie geen beheerde toepassingen gemaakt nog, raadpleegt u [publiceren van een beheerde toepassingsservices voor intern verbruik](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="614dd-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="614dd-109">Op dit moment kunt u Azure CLI of Azure portal gebruiken voor een beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="614dd-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="614dd-110">De beheerde toepassing maken met behulp van de portal</span><span class="sxs-lookup"><span data-stu-id="614dd-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="614dd-111">Volg deze stappen voor het implementeren van een beheerde toepassing via de portal:</span><span class="sxs-lookup"><span data-stu-id="614dd-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="614dd-112">Ga naar de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="614dd-112">Go to the Azure portal.</span></span> <span data-ttu-id="614dd-113">Zoeken naar **Servicecatalogus beheerde toepassing**.</span><span class="sxs-lookup"><span data-stu-id="614dd-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Servicecatalogus voor beheerde toepassing](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="614dd-115">Selecteer de beheerde toepassing die u wilt maken in de lijst met beschikbare oplossingen.</span><span class="sxs-lookup"><span data-stu-id="614dd-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="614dd-116">Selecteer **Maken**.</span><span class="sxs-lookup"><span data-stu-id="614dd-116">Select **Create**.</span></span>

   ![Selectie van de beheerde toepassing](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="614dd-118">Geef waarden op voor de parameters die nodig zijn voor het leveren van de resources.</span><span class="sxs-lookup"><span data-stu-id="614dd-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="614dd-119">Selecteer **West-Centraal VS** voor de locatie.</span><span class="sxs-lookup"><span data-stu-id="614dd-119">Select **West Central US** for location.</span></span> <span data-ttu-id="614dd-120">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="614dd-120">Select **OK**.</span></span>

   ![Parameters voor de beheerde toepassing](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="614dd-122">De sjabloon valideert de waarden die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="614dd-122">The template validates the values you provided.</span></span> <span data-ttu-id="614dd-123">Als de validatie slaagt, selecteert u **OK** implementatie te starten.</span><span class="sxs-lookup"><span data-stu-id="614dd-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Validatie van de beheerde toepassing](./media/managed-application-consumption/validation.png)

<span data-ttu-id="614dd-125">Nadat de implementatie is voltooid, worden de juiste resources die zijn gedefinieerd in de sjabloon ingericht in de beheerde resourcegroep die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="614dd-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="614dd-126">De beheerde toepassing maken met behulp van Azure CLI</span><span class="sxs-lookup"><span data-stu-id="614dd-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="614dd-127">Er zijn twee manieren een beheerde toepassing maken met behulp van Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="614dd-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="614dd-128">Gebruik de opdracht voor het maken van beheerde toepassingen.</span><span class="sxs-lookup"><span data-stu-id="614dd-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="614dd-129">Gebruik de opdracht van de implementatie reguliere sjabloon.</span><span class="sxs-lookup"><span data-stu-id="614dd-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="614dd-130">Gebruik de opdracht van de implementatie van sjabloon</span><span class="sxs-lookup"><span data-stu-id="614dd-130">Use the template deployment command</span></span>

<span data-ttu-id="614dd-131">Implementeer het bestand applianceMainTemplate.json die de leverancier gemaakt.</span><span class="sxs-lookup"><span data-stu-id="614dd-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="614dd-132">Vervolgens maakt u twee resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="614dd-132">Then create two resource groups.</span></span> <span data-ttu-id="614dd-133">De eerste resourcegroep is waar de bron van de beheerde toepassing wordt gemaakt: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="614dd-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="614dd-134">De tweede resourcegroep bevat alle resources die zijn gedefinieerd in mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="614dd-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="614dd-135">Deze resourcegroep wordt beheerd door de ISV.</span><span class="sxs-lookup"><span data-stu-id="614dd-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="614dd-136">Gebruik `westcentralus` als de locatie van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="614dd-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="614dd-137">Gebruik de volgende opdracht voor het implementeren van applianceMainTemplate.json in mainResourceGroup:</span><span class="sxs-lookup"><span data-stu-id="614dd-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="614dd-138">Nadat de voorgaande sjabloon wordt uitgevoerd, wordt u gevraagd de waarden van de parameters die zijn gedefinieerd in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="614dd-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="614dd-139">Naast de parameters die nodig zijn voor het inrichten van resources in een sjabloon, moet u twee belangrijke parameterwaarden:</span><span class="sxs-lookup"><span data-stu-id="614dd-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="614dd-140">**managedResourceGroupId**: de ID van de resourcegroep met de resources die zijn gedefinieerd in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="614dd-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="614dd-141">De ID van het formulier is `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="614dd-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="614dd-142">In het vorige voorbeeld is de ID van `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="614dd-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="614dd-143">**applianceDefinitionId**: de ID van de bron van de definitie van beheerde toepassingsservices.</span><span class="sxs-lookup"><span data-stu-id="614dd-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="614dd-144">Deze waarde wordt verstrekt door de ISV.</span><span class="sxs-lookup"><span data-stu-id="614dd-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="614dd-145">De uitgever moet toegang verlenen aan de resourcegroep met de definitie van de beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="614dd-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="614dd-146">De definitie-resource is gemaakt in het abonnement op publisher.</span><span class="sxs-lookup"><span data-stu-id="614dd-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="614dd-147">Daarom moet een gebruiker, groep of toepassing in de tenant klant leestoegang tot deze resource.</span><span class="sxs-lookup"><span data-stu-id="614dd-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="614dd-148">Nadat de implementatie voltooid wordt, ziet u dat de beheerde toepassing in mainResourceGroup wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="614dd-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="614dd-149">De resource storageAccount wordt gemaakt in managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="614dd-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="614dd-150">Gebruik de opdracht maken</span><span class="sxs-lookup"><span data-stu-id="614dd-150">Use the create command</span></span>

<span data-ttu-id="614dd-151">U kunt de `az managedapp create` opdracht voor het maken van een beheerde toepassing van de definitie van de beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="614dd-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="614dd-152">**apparaat-definitie-Id**: de bron-ID van de definitie van de beheerde toepassing in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="614dd-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="614dd-153">Als u deze ID, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="614dd-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="614dd-154">Deze opdracht retourneert de definitie van de beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="614dd-154">This command returns the managed application definition.</span></span> <span data-ttu-id="614dd-155">U moet de waarde van de eigenschap ID.</span><span class="sxs-lookup"><span data-stu-id="614dd-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="614dd-156">**beheerde-rg-id**: de naam van de resourcegroep met de resources die zijn gedefinieerd in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="614dd-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="614dd-157">Deze resourcegroep is de groep beheerde bron.</span><span class="sxs-lookup"><span data-stu-id="614dd-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="614dd-158">Het wordt beheerd door de uitgever.</span><span class="sxs-lookup"><span data-stu-id="614dd-158">It's managed by the publisher.</span></span> <span data-ttu-id="614dd-159">Als deze nog niet bestaat, wordt deze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="614dd-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="614dd-160">**resourcegroep**: de resourcegroep waar de bron van de beheerde toepassing wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="614dd-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="614dd-161">De resource Microsoft.Solutions/appliance woont in deze resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="614dd-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="614dd-162">**parameters**: de parameters die nodig zijn voor de resources die zijn gedefinieerd in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="614dd-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="614dd-163">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="614dd-163">Known issues</span></span>

<span data-ttu-id="614dd-164">Deze preview-versie bevat de volgende problemen:</span><span class="sxs-lookup"><span data-stu-id="614dd-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="614dd-165">Een interne serverfout 500 wordt weergegeven tijdens het maken van de beheerde toepassing.</span><span class="sxs-lookup"><span data-stu-id="614dd-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="614dd-166">Als u dit probleem, is het waarschijnlijk onregelmatige.</span><span class="sxs-lookup"><span data-stu-id="614dd-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="614dd-167">De bewerking opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="614dd-167">Retry the operation.</span></span>
* <span data-ttu-id="614dd-168">Een nieuwe resourcegroep is nodig voor de beheerde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="614dd-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="614dd-169">Als u een bestaande resourcegroep gebruikt, mislukt de implementatie.</span><span class="sxs-lookup"><span data-stu-id="614dd-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="614dd-170">De resourcegroep met de bron Microsoft.Solutions/appliances moet worden gemaakt in de **westcentralus** locatie.</span><span class="sxs-lookup"><span data-stu-id="614dd-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="614dd-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="614dd-171">Next steps</span></span>

* <span data-ttu-id="614dd-172">Zie voor een inleiding tot beheerde toepassingen, [beheerde toepassingsoverzicht](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="614dd-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="614dd-173">Zie voor meer informatie over het publiceren van een Servicecatalogus beheerde toepassing [maken en publiceren van een Servicecatalogus beheerde toepassing](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="614dd-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="614dd-174">Zie voor meer informatie over het uitgeven van beheerde toepassingen naar Azure Marketplace [Azure beheerde toepassingen in de Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="614dd-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="614dd-175">Zie voor meer informatie over het gebruiken van een beheerde toepassing in de Marketplace [Azure gebruiken beheerde toepassingen in de Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="614dd-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>

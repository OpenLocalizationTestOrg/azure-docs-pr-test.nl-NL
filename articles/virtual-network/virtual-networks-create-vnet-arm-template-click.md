---
title: een virtueel netwerk aaaCreate | Azure Resource Manager-sjabloon | Microsoft Docs
description: Meer informatie over hoe toocreate een virtueel netwerk met een Azure Resource Manager-sjabloon.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 69530861-2f97-4a6e-b336-a7baf2690044
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b9c289433ff2a84bec19eac25fa28ab40d131c7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="a6602-103">Een virtueel netwerk met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="a6602-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="a6602-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="a6602-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="a6602-105">Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a6602-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="a6602-106">Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a6602-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="a6602-107">Dit artikel wordt uitgelegd hoe toocreate een VNet via Hallo Resource Manager deployment model met een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a6602-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="a6602-108">Ook kunt u een VNet via Resource Manager, met andere hulpprogramma's maken of maak een VNet via de klassieke implementatiemodel Hallo door een andere optie kiezen in Hallo volgende lijst:</span><span class="sxs-lookup"><span data-stu-id="a6602-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="a6602-109">Portal</span><span class="sxs-lookup"><span data-stu-id="a6602-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="a6602-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a6602-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="a6602-111">CLI</span><span class="sxs-lookup"><span data-stu-id="a6602-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="a6602-112">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="a6602-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="a6602-113">Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="a6602-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="a6602-114">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="a6602-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="a6602-115">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="a6602-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="a6602-116">U leert hoe toodownload wijzigen en bestaande ARM-sjabloon vanuit GitHub en Hallo sjabloon implementeren vanuit GitHub, PowerShell en hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a6602-116">You will learn how toodownload and modify and existing ARM template from GitHub, and deploy hello template from GitHub, PowerShell, and hello Azure CLI.</span></span>

<span data-ttu-id="a6602-117">Als u wilt Hallo ARM-sjabloon rechtstreeks vanuit GitHub, zonder deze te wijzigen implementeren, gaat u verder te[een sjabloon implementeren vanuit github](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="a6602-117">If you are simply deploying hello ARM template directly from GitHub, without any changes, skip too[deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a><span data-ttu-id="a6602-118">Hello Azure Resource Manager-sjabloon downloaden en begrijpen</span><span class="sxs-lookup"><span data-stu-id="a6602-118">Download and understand hello Azure Resource Manager template</span></span>
<span data-ttu-id="a6602-119">U kunt bestaande Hallo-sjabloon voor het maken van een VNet en twee subnets vanuit GitHub downloaden, breng eventuele wijzigingen die u mogelijk wilt gebruiken en het opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6602-119">You can download hello existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="a6602-120">toodo voltooien dus Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6602-120">toodo so, complete hello following steps:</span></span>

1. <span data-ttu-id="a6602-121">Navigeer te[pagina voorbeeldsjabloon Hallo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="a6602-121">Navigate too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="a6602-122">Klik op **azuredeploy.json** en vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="a6602-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="a6602-123">Sla Hallo bestand tooa een lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a6602-123">Save hello file tooa a local folder on your computer.</span></span>
4. <span data-ttu-id="a6602-124">Als u bekend met sjablonen bent, slaat u toostep 7.</span><span class="sxs-lookup"><span data-stu-id="a6602-124">If you are familiar with templates, skip toostep 7.</span></span>
5. <span data-ttu-id="a6602-125">Open Hallo-bestand die u zojuist hebt opgeslagen en bekijkt hello inhoud onder **parameters** in regel 5.</span><span class="sxs-lookup"><span data-stu-id="a6602-125">Open hello file you just saved and look at hello contents under **parameters** in line 5.</span></span> <span data-ttu-id="a6602-126">ARM-sjabloonparameters bieden een tijdelijke aanduiding voor waarden die kunnen worden ingevuld tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a6602-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="a6602-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="a6602-127">Parameter</span></span> | <span data-ttu-id="a6602-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a6602-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="a6602-129">**location**</span><span class="sxs-lookup"><span data-stu-id="a6602-129">**location**</span></span> |<span data-ttu-id="a6602-130">Azure-regio waar Hallo VNet wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="a6602-130">Azure region where hello VNet will be created</span></span> |
   | <span data-ttu-id="a6602-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="a6602-131">**vnetName**</span></span> |<span data-ttu-id="a6602-132">Naam voor Hallo nieuwe VNet</span><span class="sxs-lookup"><span data-stu-id="a6602-132">Name for hello new VNet</span></span> |
   | <span data-ttu-id="a6602-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="a6602-133">**addressPrefix**</span></span> |<span data-ttu-id="a6602-134">Adresruimte voor Hallo VNet, in CIDR-notatie</span><span class="sxs-lookup"><span data-stu-id="a6602-134">Address space for hello VNet, in CIDR format</span></span> |
   | <span data-ttu-id="a6602-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="a6602-135">**subnet1Name**</span></span> |<span data-ttu-id="a6602-136">Naam voor Hallo eerste VNet</span><span class="sxs-lookup"><span data-stu-id="a6602-136">Name for hello first VNet</span></span> |
   | <span data-ttu-id="a6602-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="a6602-137">**subnet1Prefix**</span></span> |<span data-ttu-id="a6602-138">CIDR-blokkering voor het eerste subnet Hallo</span><span class="sxs-lookup"><span data-stu-id="a6602-138">CIDR block for hello first subnet</span></span> |
   | <span data-ttu-id="a6602-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="a6602-139">**subnet2Name**</span></span> |<span data-ttu-id="a6602-140">Naam voor Hallo tweede VNet</span><span class="sxs-lookup"><span data-stu-id="a6602-140">Name for hello second VNet</span></span> |
   | <span data-ttu-id="a6602-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="a6602-141">**subnet2Prefix**</span></span> |<span data-ttu-id="a6602-142">CIDR-blokkering voor Hallo tweede subnet</span><span class="sxs-lookup"><span data-stu-id="a6602-142">CIDR block for hello second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="a6602-143">Azure Resource Manager-sjablonen die in GitHub worden bewaard, kunnen in de loop van de tijd veranderen.</span><span class="sxs-lookup"><span data-stu-id="a6602-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="a6602-144">Zorg ervoor dat u Hallo sjabloon controleren voordat u deze gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a6602-144">Make sure you check hello template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="a6602-145">Controleer de inhoud Hallo onder **resources** en Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a6602-145">Check hello content under **resources** and notice hello following:</span></span>
   
   * <span data-ttu-id="a6602-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="a6602-146">**type**.</span></span> <span data-ttu-id="a6602-147">Type resource dat door Hallo sjabloon wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a6602-147">Type of resource being created by hello template.</span></span> <span data-ttu-id="a6602-148">In dit geval **Microsoft.Network/virtualNetworks**, die een VNet vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="a6602-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="a6602-149">**Naam**.</span><span class="sxs-lookup"><span data-stu-id="a6602-149">**name**.</span></span> <span data-ttu-id="a6602-150">Naam voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="a6602-150">Name for hello resource.</span></span> <span data-ttu-id="a6602-151">Kennisgeving Hallo gebruik van **[parameters('vnetName')]**, dit betekent Hallo naam wordt geleverd als invoer door Hallo gebruiker of een parameterbestand tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="a6602-151">Notice hello use of **[parameters('vnetName')]**, which means hello name will provided as input by hello user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="a6602-152">**Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a6602-152">**properties**.</span></span> <span data-ttu-id="a6602-153">Lijst met eigenschappen voor Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="a6602-153">List of properties for hello resource.</span></span> <span data-ttu-id="a6602-154">Deze sjabloon maakt gebruik van Hallo ruimte en subnet adreseigenschappen tijdens het maken van een VNet.</span><span class="sxs-lookup"><span data-stu-id="a6602-154">This template uses hello address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="a6602-155">Navigeer terug te[pagina voorbeeldsjabloon Hallo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="a6602-155">Navigate back too[hello sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="a6602-156">Klik op **azuredeploy-paremeters.json** en vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="a6602-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="a6602-157">Sla Hallo bestand tooa een lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="a6602-157">Save hello file tooa a local folder on your computer.</span></span>
10. <span data-ttu-id="a6602-158">Open Hallo bestand dat u zojuist hebt opgeslagen en bewerk Hallo-waarden voor Hallo-parameters.</span><span class="sxs-lookup"><span data-stu-id="a6602-158">Open hello file you just saved and edit hello values for hello parameters.</span></span> <span data-ttu-id="a6602-159">Gebruik Hallo volgende waarden onder toodeploy hello VNet in Hallo scenario beschreven:</span><span class="sxs-lookup"><span data-stu-id="a6602-159">Use hello following values below toodeploy hello VNet described in hello scenario:</span></span>

    ```json
        {
          "location": {
            "value": "Central US"
          },
          "vnetName": {
              "value": "TestVNet"
          },
          "addressPrefix": {
              "value": "192.168.0.0/16"
          },
          "subnet1Name": {
              "value": "FrontEnd"
          },
          "subnet1Prefix": {
            "value": "192.168.1.0/24"
          },
          "subnet2Name": {
              "value": "BackEnd"
          },
          "subnet2Prefix": {
              "value": "192.168.2.0/24"
          }
        }
    ```

11. <span data-ttu-id="a6602-160">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="a6602-160">Save hello file.</span></span>


## <a name="deploy-hello-template-using-powershell"></a><span data-ttu-id="a6602-161">Met behulp van PowerShell Hallo-sjabloon implementeren</span><span class="sxs-lookup"><span data-stu-id="a6602-161">Deploy hello template using PowerShell</span></span>

<span data-ttu-id="a6602-162">Volgende stappen toodeploy Hallo-sjabloon die u hebt gedownload met behulp van PowerShell Hallo voltooien:</span><span class="sxs-lookup"><span data-stu-id="a6602-162">Complete hello following steps toodeploy hello template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="a6602-163">Installeren en configureren van Azure PowerShell via Hallo stappen in Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="a6602-163">Install and configure Azure PowerShell by completing hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="a6602-164">Voer Hallo opdracht toocreate na een nieuwe resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="a6602-164">Run hello following command toocreate a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="a6602-165">Hallo opdracht maakt u een resourcegroep met de naam *TestRG* in Hallo *VS-midden* azure-regio.</span><span class="sxs-lookup"><span data-stu-id="a6602-165">hello command creates a resource group named *TestRG* in hello *Central US* azure region.</span></span> <span data-ttu-id="a6602-166">Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="a6602-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="a6602-167">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a6602-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="a6602-168">Voer Hallo na de opdracht toodeploy Hallo nieuwe VNet met het Hallo-sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="a6602-168">Run hello following command toodeploy hello new VNet using hello template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="a6602-169">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a6602-169">Expected output:</span></span>
   
        DeploymentName    : TestVNetDeployment
        ResourceGroupName : TestRG
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
        Parameters        :
                            Name             Type                       Value
                            ===============  =========================  ==========
                            location         String                     Central US
                            vnetName         String                     TestVNet
                            addressPrefix    String                     192.168.0.0/16
                            subnet1Prefix    String                     192.168.1.0/24
                            subnet1Name      String                     FrontEnd
                            subnet2Prefix    String                     192.168.2.0/24
                            subnet2Name      String                     BackEnd
   
        Outputs           :
4. <span data-ttu-id="a6602-170">Voer Hallo volgende opdracht tooview Hallo eigenschappen van Hallo nieuwe VNet:</span><span class="sxs-lookup"><span data-stu-id="a6602-170">Run hello following command tooview hello properties of hello new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="a6602-171">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a6602-171">Expected output:</span></span>

        Name              : TestVNet
        ResourceGroupName : TestRG
        Location          : centralus
        Id                : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag              : W/"[Id]"
        ProvisioningState : Succeeded
        Tags              :
        AddressSpace      : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptions       : {
                              "DnsServers": null
                            }
        NetworkInterfaces : null
        Subnets           : [
                              {
                                "Name": "FrontEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              },
                              {
                                "Name": "BackEnd",
                                "Etag": "W/\"[Id]\"",
                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                "AddressPrefix": "192.168.2.0/24",
                                "IpConfigurations": [],
                                "NetworkSecurityGroup": null,
                                "RouteTable": null,
                                "ProvisioningState": "Succeeded"
                              }
                            ]

## <a name="deploy-hello-template-using-click-to-deploy"></a><span data-ttu-id="a6602-172">Implementeren met click-to-deploy Hallo-sjabloon</span><span class="sxs-lookup"><span data-stu-id="a6602-172">Deploy hello template using click-to-deploy</span></span>

<span data-ttu-id="a6602-173">U kunt vooraf gedefinieerde Azure Resource Manager sjablonen geüploade tooa GitHub-opslagplaats beheerd door Microsoft en community open toohello hergebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6602-173">You can reuse pre-defined Azure Resource Manager templates uploaded tooa GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="a6602-174">Deze sjablonen kunnen rechtstreeks uit de GitHub worden geïmplementeerd of gedownload en gewijzigd toofit uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="a6602-174">These templates can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> <span data-ttu-id="a6602-175">toodeploy een sjabloon die wordt gemaakt van een VNet met twee subnetten voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6602-175">toodeploy a template that creates a VNet with two subnets, complete hello following steps:</span></span>

1. <span data-ttu-id="a6602-176">Vanuit een browser navigeren te[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="a6602-176">From a browser, navigate too[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="a6602-177">Schuif naar beneden Hallo lijst met sjablonen en klikt u op **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="a6602-177">Scroll down hello list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="a6602-178">Controleer de Hallo **README.md** -bestand, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a6602-178">Check hello **README.md** file, as shown below.</span></span>

    ![READEME.md-bestand in github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="a6602-180">Klik op **tooAzure implementeren**.</span><span class="sxs-lookup"><span data-stu-id="a6602-180">Click **Deploy tooAzure**.</span></span> <span data-ttu-id="a6602-181">Voer indien nodig uw Azure-aanmeldingsreferenties in.</span><span class="sxs-lookup"><span data-stu-id="a6602-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="a6602-182">In Hallo **Parameters** blade Voer Hallo waarden u wilt dat uw nieuwe VNet toouse toocreate en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6602-182">In hello **Parameters** blade, enter hello values you want toouse toocreate your new VNet, and then click **OK**.</span></span> <span data-ttu-id="a6602-183">Hallo ziet volgende afbeelding Hallo waarden voor Hallo scenario:</span><span class="sxs-lookup"><span data-stu-id="a6602-183">hello following figure shows hello values for hello scenario:</span></span>
   
    ![ARM-sjabloonparameters](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="a6602-185">Klik op **resourcegroep** en selecteert u een groep resource tooadd Hallo VNet-naar- of klik op **nieuw** tooadd hello VNet tooa nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a6602-185">Click **Resource group** and select a resource group tooadd hello VNet to, or click **Create new** tooadd hello VNet tooa new resource group.</span></span> <span data-ttu-id="a6602-186">Hallo volgende afbeelding ziet u Hallo resource groepsinstellingen voor een nieuwe resourcegroep aangeroepen **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="a6602-186">hello following figure shows hello resource group settings for a new resource group called **TestRG**:</span></span>

    ![Resourcegroep](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="a6602-188">Wijzig indien nodig, Hallo **abonnement** en **locatie** instellingen voor uw VNet.</span><span class="sxs-lookup"><span data-stu-id="a6602-188">If necessary, change hello **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="a6602-189">Als u niet dat toosee hello VNet als tegel in Hallo wilt **Startboard**, uitschakelen **pincode tooStartboard**.</span><span class="sxs-lookup"><span data-stu-id="a6602-189">If you do not want toosee hello VNet as a tile in hello **Startboard**, disable **Pin tooStartboard**.</span></span>
8. <span data-ttu-id="a6602-190">Klik op **juridische voorwaarden**, Hallo voorwaarden lezen en klikt u op **kopen** tooagree.</span><span class="sxs-lookup"><span data-stu-id="a6602-190">Click **Legal terms**, read hello terms, and click **Buy** tooagree.</span></span> 
9. <span data-ttu-id="a6602-191">Klik op **maken** toocreate hello VNet.</span><span class="sxs-lookup"><span data-stu-id="a6602-191">Click **Create** toocreate hello VNet.</span></span>
   
    ![Tegel implementatie in Preview Portal verzenden](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="a6602-193">Zodra Hallo-implementatie is voltooid, in hello Azure-portal klikt u op **meer services**, type *virtuele netwerken* in Hallo filter dat wordt weergegeven, klikt u virtuele netwerken toosee Hallo virtuele netwerken blade.</span><span class="sxs-lookup"><span data-stu-id="a6602-193">Once hello deployment is complete, in hello Azure portal click **More services**, type *virtual networks* in hello filter box that appears, then click Virtual networks toosee hello Virtual networks blade.</span></span> <span data-ttu-id="a6602-194">Klik op de blade Hallo *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="a6602-194">In hello blade, click *TestVNet*.</span></span> <span data-ttu-id="a6602-195">In Hallo *TestVNet* blade, klikt u op **subnetten** toosee Hallo gemaakt subnetten, zoals wordt weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="a6602-195">In hello *TestVNet* blade, click **Subnets** toosee hello created subnets, as shown in hello following picture:</span></span>
    
     ![VNet maken in de Preview Portal](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="a6602-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a6602-197">Next steps</span></span>

<span data-ttu-id="a6602-198">Meer informatie over hoe tooconnect:</span><span class="sxs-lookup"><span data-stu-id="a6602-198">Learn how tooconnect:</span></span>

- <span data-ttu-id="a6602-199">Een virtueel netwerk van virtuele machine (VM) tooa door Hallo lezen [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) of [maken van een Linux-VM](../virtual-machines/linux/quick-create-portal.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="a6602-199">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="a6602-200">In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.</span><span class="sxs-lookup"><span data-stu-id="a6602-200">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="a6602-201">virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a6602-201">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="a6602-202">Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="a6602-202">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="a6602-203">Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-arm.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="a6602-203">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>

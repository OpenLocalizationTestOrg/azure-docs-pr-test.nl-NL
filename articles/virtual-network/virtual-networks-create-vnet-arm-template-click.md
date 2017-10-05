---
title: Een virtueel netwerk maken | Azure Resource Manager-sjabloon | Microsoft Docs
description: Informatie over het maken van een virtueel netwerk met een Azure Resource Manager-sjabloon.
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
ms.openlocfilehash: 81602766848a91331c8d811ea1c8ec3ffae44b96
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a><span data-ttu-id="9d62b-103">Een virtueel netwerk met een Azure Resource Manager-sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="9d62b-103">Create a virtual network using an Azure Resource Manager template</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="9d62b-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="9d62b-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="9d62b-105">Microsoft raadt aan resources te maken via het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="9d62b-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="9d62b-106">Lees het artikel [Azure-implementatiemodellen begrijpen](../azure-resource-manager/resource-manager-deployment-model.md) voor meer informatie over de verschillen tussen de twee modellen.</span><span class="sxs-lookup"><span data-stu-id="9d62b-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="9d62b-107">Dit artikel wordt uitgelegd hoe u een VNet met het implementatiemodel van Resource Manager met een Azure Resource Manager-sjabloon maakt.</span><span class="sxs-lookup"><span data-stu-id="9d62b-107">This article explains how to create a VNet through the Resource Manager deployment model using an Azure Resource Manager template.</span></span> <span data-ttu-id="9d62b-108">U kunt via Resource Manager ook een VNet maken met andere hulpprogramma's. Bovendien kunt u een VNet maken via het klassieke implementatiemodel door in de volgende lijst een andere optie te selecteren:</span><span class="sxs-lookup"><span data-stu-id="9d62b-108">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
- [<span data-ttu-id="9d62b-109">Portal</span><span class="sxs-lookup"><span data-stu-id="9d62b-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
- [<span data-ttu-id="9d62b-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d62b-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
- [<span data-ttu-id="9d62b-111">CLI</span><span class="sxs-lookup"><span data-stu-id="9d62b-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
- [<span data-ttu-id="9d62b-112">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="9d62b-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
- [<span data-ttu-id="9d62b-113">Portal (klassiek)</span><span class="sxs-lookup"><span data-stu-id="9d62b-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
- [<span data-ttu-id="9d62b-114">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="9d62b-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [<span data-ttu-id="9d62b-115">CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="9d62b-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

<span data-ttu-id="9d62b-116">U ziet hoe u een bestaande ARM-sjabloon kunt downloaden en wijzigen vanuit GitHub, en de sjabloon vervolgens kunt implementeren met GitHub, PowerShell en Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9d62b-116">You will learn how to download and modify and existing ARM template from GitHub, and deploy the template from GitHub, PowerShell, and the Azure CLI.</span></span>

<span data-ttu-id="9d62b-117">Als u de ARM-sjabloon rechtstreeks vanuit GitHub wilt implementeren zonder deze te wijzigen, gaat u naar [Een sjabloon implementeren vanuit GitHub](#deploy-the-arm-template-by-using-click-to-deploy).</span><span class="sxs-lookup"><span data-stu-id="9d62b-117">If you are simply deploying the ARM template directly from GitHub, without any changes, skip to [deploy a template from github](#deploy-the-arm-template-by-using-click-to-deploy).</span></span>

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-the-azure-resource-manager-template"></a><span data-ttu-id="9d62b-118">De Azure Resource Manager-sjabloon downloaden en begrijpen</span><span class="sxs-lookup"><span data-stu-id="9d62b-118">Download and understand the Azure Resource Manager template</span></span>
<span data-ttu-id="9d62b-119">U kunt de bestaande sjabloon voor het maken van een VNet en twee subnets vanuit GitHub downloaden, breng eventuele wijzigingen die u mogelijk wilt gebruiken en het opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d62b-119">You can download the existing template for creating a VNet and two subnets from GitHub, make any changes you might want, and reuse it.</span></span> <span data-ttu-id="9d62b-120">Voer de volgende stappen uit om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="9d62b-120">To do so, complete the following steps:</span></span>

1. <span data-ttu-id="9d62b-121">Navigeer naar [de sjabloon-voorbeeldpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="9d62b-121">Navigate to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
2. <span data-ttu-id="9d62b-122">Klik op **azuredeploy.json** en vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-122">Click **azuredeploy.json**, and then click **RAW**.</span></span>
3. <span data-ttu-id="9d62b-123">Sla het bestand op in een lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9d62b-123">Save the file to a a local folder on your computer.</span></span>
4. <span data-ttu-id="9d62b-124">Als u bekend met sjablonen bent, gaat u verder met stap 7.</span><span class="sxs-lookup"><span data-stu-id="9d62b-124">If you are familiar with templates, skip to step 7.</span></span>
5. <span data-ttu-id="9d62b-125">Open het bestand dat u zojuist hebt opgeslagen en bekijk de inhoud onder **parameters** in regel 5.</span><span class="sxs-lookup"><span data-stu-id="9d62b-125">Open the file you just saved and look at the contents under **parameters** in line 5.</span></span> <span data-ttu-id="9d62b-126">ARM-sjabloonparameters bieden een tijdelijke aanduiding voor waarden die kunnen worden ingevuld tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="9d62b-126">ARM template parameters provide a placeholder for values that can be filled out during deployment.</span></span>
   
   | <span data-ttu-id="9d62b-127">Parameter</span><span class="sxs-lookup"><span data-stu-id="9d62b-127">Parameter</span></span> | <span data-ttu-id="9d62b-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9d62b-128">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="9d62b-129">**location**</span><span class="sxs-lookup"><span data-stu-id="9d62b-129">**location**</span></span> |<span data-ttu-id="9d62b-130">Azure-regio waar het VNet wordt aangemaakt</span><span class="sxs-lookup"><span data-stu-id="9d62b-130">Azure region where the VNet will be created</span></span> |
   | <span data-ttu-id="9d62b-131">**vnetName**</span><span class="sxs-lookup"><span data-stu-id="9d62b-131">**vnetName**</span></span> |<span data-ttu-id="9d62b-132">Naam voor het nieuwe VNet</span><span class="sxs-lookup"><span data-stu-id="9d62b-132">Name for the new VNet</span></span> |
   | <span data-ttu-id="9d62b-133">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="9d62b-133">**addressPrefix**</span></span> |<span data-ttu-id="9d62b-134">Adresruimte voor het VNet, in CIDR-indeling</span><span class="sxs-lookup"><span data-stu-id="9d62b-134">Address space for the VNet, in CIDR format</span></span> |
   | <span data-ttu-id="9d62b-135">**subnet1Name**</span><span class="sxs-lookup"><span data-stu-id="9d62b-135">**subnet1Name**</span></span> |<span data-ttu-id="9d62b-136">Naam voor het eerste VNet</span><span class="sxs-lookup"><span data-stu-id="9d62b-136">Name for the first VNet</span></span> |
   | <span data-ttu-id="9d62b-137">**subnet1Prefix**</span><span class="sxs-lookup"><span data-stu-id="9d62b-137">**subnet1Prefix**</span></span> |<span data-ttu-id="9d62b-138">CIDR-blokkering voor het eerste subnet</span><span class="sxs-lookup"><span data-stu-id="9d62b-138">CIDR block for the first subnet</span></span> |
   | <span data-ttu-id="9d62b-139">**subnet2Name**</span><span class="sxs-lookup"><span data-stu-id="9d62b-139">**subnet2Name**</span></span> |<span data-ttu-id="9d62b-140">Naam voor het tweede VNet</span><span class="sxs-lookup"><span data-stu-id="9d62b-140">Name for the second VNet</span></span> |
   | <span data-ttu-id="9d62b-141">**subnet2Prefix**</span><span class="sxs-lookup"><span data-stu-id="9d62b-141">**subnet2Prefix**</span></span> |<span data-ttu-id="9d62b-142">CIDR-blokkering voor het tweede subnet</span><span class="sxs-lookup"><span data-stu-id="9d62b-142">CIDR block for the second subnet</span></span> |
   
   > [!IMPORTANT]
   > <span data-ttu-id="9d62b-143">Azure Resource Manager-sjablonen die in GitHub worden bewaard, kunnen in de loop van de tijd veranderen.</span><span class="sxs-lookup"><span data-stu-id="9d62b-143">Azure Resource Manager templates maintained in GitHub can change over time.</span></span> <span data-ttu-id="9d62b-144">Zorg ervoor dat u de sjabloon controleert, voordat u deze gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d62b-144">Make sure you check the template before using it.</span></span>
   > 
   > 
6. <span data-ttu-id="9d62b-145">Controleer de inhoud onder **Resources** en let op het volgende:</span><span class="sxs-lookup"><span data-stu-id="9d62b-145">Check the content under **resources** and notice the following:</span></span>
   
   * <span data-ttu-id="9d62b-146">**type**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-146">**type**.</span></span> <span data-ttu-id="9d62b-147">Het type resource dat door de sjabloon wordt aangemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d62b-147">Type of resource being created by the template.</span></span> <span data-ttu-id="9d62b-148">In dit geval **Microsoft.Network/virtualNetworks**, die een VNet vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="9d62b-148">In this case, **Microsoft.Network/virtualNetworks**, which represent a VNet.</span></span>
   * <span data-ttu-id="9d62b-149">**Naam**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-149">**name**.</span></span> <span data-ttu-id="9d62b-150">Naam voor de resource.</span><span class="sxs-lookup"><span data-stu-id="9d62b-150">Name for the resource.</span></span> <span data-ttu-id="9d62b-151">Let op het gebruik van **[parameters('vnetName')]**. Deze geeft aan of de naam wordt geleverd als invoer door de gebruiker of een parameterbestand tijdens implementatie.</span><span class="sxs-lookup"><span data-stu-id="9d62b-151">Notice the use of **[parameters('vnetName')]**, which means the name will provided as input by the user or a parameter file during deployment.</span></span>
   * <span data-ttu-id="9d62b-152">**Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-152">**properties**.</span></span> <span data-ttu-id="9d62b-153">Lijst met eigenschappen voor de resource.</span><span class="sxs-lookup"><span data-stu-id="9d62b-153">List of properties for the resource.</span></span> <span data-ttu-id="9d62b-154">Deze sjabloon maakt gebruik van de adresruimte en de subneteigenschappen tijdens het aanmaken van het VNet.</span><span class="sxs-lookup"><span data-stu-id="9d62b-154">This template uses the address space and subnet properties during VNet creation.</span></span>
7. <span data-ttu-id="9d62b-155">Ga naar de [pagina Voorbeeldsjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span><span class="sxs-lookup"><span data-stu-id="9d62b-155">Navigate back to [the sample template page](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).</span></span>
8. <span data-ttu-id="9d62b-156">Klik op **azuredeploy-paremeters.json** en vervolgens op **RAW**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-156">Click **azuredeploy-paremeters.json**, and then click **RAW**.</span></span>
9. <span data-ttu-id="9d62b-157">Sla het bestand op in een lokale map op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9d62b-157">Save the file to a a local folder on your computer.</span></span>
10. <span data-ttu-id="9d62b-158">Open het bestand dat u zojuist hebt opgeslagen en bewerk de waarden voor de parameters.</span><span class="sxs-lookup"><span data-stu-id="9d62b-158">Open the file you just saved and edit the values for the parameters.</span></span> <span data-ttu-id="9d62b-159">Gebruik de volgende waarden op om het VNet dat is beschreven in het scenario te implementeren:</span><span class="sxs-lookup"><span data-stu-id="9d62b-159">Use the following values below to deploy the VNet described in the scenario:</span></span>

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

11. <span data-ttu-id="9d62b-160">Sla het bestand op.</span><span class="sxs-lookup"><span data-stu-id="9d62b-160">Save the file.</span></span>


## <a name="deploy-the-template-using-powershell"></a><span data-ttu-id="9d62b-161">De sjabloon die met behulp van PowerShell implementeren</span><span class="sxs-lookup"><span data-stu-id="9d62b-161">Deploy the template using PowerShell</span></span>

<span data-ttu-id="9d62b-162">De volgende stappen voor het implementeren van de sjabloon die u hebt gedownload met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9d62b-162">Complete the following steps to deploy the template you downloaded by using PowerShell:</span></span>

1. <span data-ttu-id="9d62b-163">Installeren en configureren van Azure PowerShell via de stappen in de [installeren en configureren van Azure PowerShell](/powershell/azure/overview) artikel.</span><span class="sxs-lookup"><span data-stu-id="9d62b-163">Install and configure Azure PowerShell by completing the steps in the [How to Install and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="9d62b-164">Voer de volgende opdracht uit om een nieuwe resourcegroep te maken:</span><span class="sxs-lookup"><span data-stu-id="9d62b-164">Run the following command to create a new resource group:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="9d62b-165">De opdracht maakt u een resourcegroep met de naam *TestRG* in de *VS-midden* azure-regio.</span><span class="sxs-lookup"><span data-stu-id="9d62b-165">The command creates a resource group named *TestRG* in the *Central US* azure region.</span></span> <span data-ttu-id="9d62b-166">Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="9d62b-166">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    <span data-ttu-id="9d62b-167">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9d62b-167">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. <span data-ttu-id="9d62b-168">Voer de volgende opdracht voor het implementeren van de nieuwe VNet met behulp van de sjabloon en de parameterbestanden bestanden u hebt gedownload en hierboven zijn gewijzigd:</span><span class="sxs-lookup"><span data-stu-id="9d62b-168">Run the following command to deploy the new VNet using the template and parameter files you downloaded and modified above:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    <span data-ttu-id="9d62b-169">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9d62b-169">Expected output:</span></span>
   
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
4. <span data-ttu-id="9d62b-170">Voer de volgende opdracht om de eigenschappen van de nieuwe VNet te bekijken:</span><span class="sxs-lookup"><span data-stu-id="9d62b-170">Run the following command to view the properties of the new VNet:</span></span>

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    <span data-ttu-id="9d62b-171">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="9d62b-171">Expected output:</span></span>

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

## <a name="deploy-the-template-using-click-to-deploy"></a><span data-ttu-id="9d62b-172">De sjabloon met click-to-deploy implementeren</span><span class="sxs-lookup"><span data-stu-id="9d62b-172">Deploy the template using click-to-deploy</span></span>

<span data-ttu-id="9d62b-173">U kunt hergebruiken van vooraf gedefinieerde Azure Resource Manager-sjablonen geüpload naar een door Microsoft beheerde GitHub-opslagplaats en toegankelijk voor de community.</span><span class="sxs-lookup"><span data-stu-id="9d62b-173">You can reuse pre-defined Azure Resource Manager templates uploaded to a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="9d62b-174">Deze sjablonen kunnen rechtstreeks uit de GitHub geïmplementeerd of gedownload en gewijzigd naar wens aanpassen.</span><span class="sxs-lookup"><span data-stu-id="9d62b-174">These templates can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> <span data-ttu-id="9d62b-175">Voor het implementeren van een sjabloon die een VNet met twee subnetten maakt, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9d62b-175">To deploy a template that creates a VNet with two subnets, complete the following steps:</span></span>

1. <span data-ttu-id="9d62b-176">Vanuit een browser gaat u naar [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="9d62b-176">From a browser, navigate to [https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).</span></span>
2. <span data-ttu-id="9d62b-177">Scroll omlaag in de lijst met sjablonen en klik op **101-vnet-two-subnets**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-177">Scroll down the list of templates, and click **101-vnet-two-subnets**.</span></span> <span data-ttu-id="9d62b-178">Controleer het **README.md** -bestand, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9d62b-178">Check the **README.md** file, as shown below.</span></span>

    ![READEME.md-bestand in github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. <span data-ttu-id="9d62b-180">Klik op **Implementeren in Azure**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-180">Click **Deploy to Azure**.</span></span> <span data-ttu-id="9d62b-181">Voer indien nodig uw Azure-aanmeldingsreferenties in.</span><span class="sxs-lookup"><span data-stu-id="9d62b-181">If necessary, enter your Azure login credentials.</span></span> 
4. <span data-ttu-id="9d62b-182">Voer de waarden die u wilt gebruiken om uw nieuwe VNet te maken in de **Parameters**-blade en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d62b-182">In the **Parameters** blade, enter the values you want to use to create your new VNet, and then click **OK**.</span></span> <span data-ttu-id="9d62b-183">De volgende afbeelding ziet de waarden voor het scenario:</span><span class="sxs-lookup"><span data-stu-id="9d62b-183">The following figure shows the values for the scenario:</span></span>
   
    ![ARM-sjabloonparameters](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. <span data-ttu-id="9d62b-185">Klik op **Resourcegroep** en selecteer een resourcegroep om toe te voegen aan het VNet of klik op **Nieuwe aanmaken** om het VNet toe te voegen aan een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="9d62b-185">Click **Resource group** and select a resource group to add the VNet to, or click **Create new** to add the VNet to a new resource group.</span></span> <span data-ttu-id="9d62b-186">De volgende afbeelding ziet u de resource groepsinstellingen voor een nieuwe resourcegroep aangeroepen **TestRG**:</span><span class="sxs-lookup"><span data-stu-id="9d62b-186">The following figure shows the resource group settings for a new resource group called **TestRG**:</span></span>

    ![Resourcegroep](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. <span data-ttu-id="9d62b-188">Wijzig zo nodig de instellingen van het **Abonnement** en de **Locatie** voor uw VNet.</span><span class="sxs-lookup"><span data-stu-id="9d62b-188">If necessary, change the **Subscription** and **Location** settings for your VNet.</span></span>
7. <span data-ttu-id="9d62b-189">Als u VNet niet als tegel wilt laten weergeven in het **Startboard** schakelt u **Vastmaken aan Startboard** uit.</span><span class="sxs-lookup"><span data-stu-id="9d62b-189">If you do not want to see the VNet as a tile in the **Startboard**, disable **Pin to Startboard**.</span></span>
8. <span data-ttu-id="9d62b-190">Klik op **juridische voorwaarden**, lees de voorwaarden en klik op **kopen** accepteren.</span><span class="sxs-lookup"><span data-stu-id="9d62b-190">Click **Legal terms**, read the terms, and click **Buy** to agree.</span></span> 
9. <span data-ttu-id="9d62b-191">Klik op **Maken** om het VNet te maken.</span><span class="sxs-lookup"><span data-stu-id="9d62b-191">Click **Create** to create the VNet.</span></span>
   
    ![Tegel implementatie in Preview Portal verzenden](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. <span data-ttu-id="9d62b-193">Zodra de implementatie is voltooid in de Azure portal op **meer services**, type *virtuele netwerken* in het vak van het filter dat wordt weergegeven, klik vervolgens op virtuele netwerken om te zien van de virtuele netwerken-blade.</span><span class="sxs-lookup"><span data-stu-id="9d62b-193">Once the deployment is complete, in the Azure portal click **More services**, type *virtual networks* in the filter box that appears, then click Virtual networks to see the Virtual networks blade.</span></span> <span data-ttu-id="9d62b-194">Klik op de blade *TestVNet*.</span><span class="sxs-lookup"><span data-stu-id="9d62b-194">In the blade, click *TestVNet*.</span></span> <span data-ttu-id="9d62b-195">In de *TestVNet* blade, klikt u op **subnetten** om te zien van de subnetten gemaakt, zoals wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="9d62b-195">In the *TestVNet* blade, click **Subnets** to see the created subnets, as shown in the following picture:</span></span>
    
     ![VNet maken in de Preview Portal](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a><span data-ttu-id="9d62b-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d62b-197">Next steps</span></span>

<span data-ttu-id="9d62b-198">Leer hoe u de volgende verbindingen maakt:</span><span class="sxs-lookup"><span data-stu-id="9d62b-198">Learn how to connect:</span></span>

- <span data-ttu-id="9d62b-199">Verbinding van een virtuele machine (VM) met een virtueel netwerk: lees de artikelen [Een Windows VM maken](../virtual-machines/virtual-machines-windows-hero-tutorial.md) of [Een Linux-VM maken](../virtual-machines/linux/quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d62b-199">A virtual machine (VM) to a virtual network by reading the [Create a Windows VM](../virtual-machines/virtual-machines-windows-hero-tutorial.md) or [Create a Linux VM](../virtual-machines/linux/quick-create-portal.md) articles.</span></span> <span data-ttu-id="9d62b-200">In plaats van een VNet en subnet te maken via de stappen die in de artikelen worden beschreven, kunt u ook een bestaand VNet en subnet selecteren waarmee u een VM wilt verbinden.</span><span class="sxs-lookup"><span data-stu-id="9d62b-200">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="9d62b-201">Verbinding van het virtuele netwerk met andere virtuele netwerken: lees het artikel [VNets verbinden](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="9d62b-201">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="9d62b-202">Verbinding van het virtuele netwerk met een on-premises netwerk via een site-naar-site virtueel particulier netwerk (VPN) of een ExpressRoute-circuit.</span><span class="sxs-lookup"><span data-stu-id="9d62b-202">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="9d62b-203">Lees hiervoor de artikelen [Een VNet verbinden met een on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [Een VNet koppelen aan een ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-arm.md).</span><span class="sxs-lookup"><span data-stu-id="9d62b-203">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>

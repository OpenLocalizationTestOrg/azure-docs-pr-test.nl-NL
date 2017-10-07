---
title: aaaCreate netwerkbeveiligingsgroepen - Azure PowerShell | Microsoft Docs
description: Meer informatie over hoe toocreate en implementeren van netwerkbeveiligingsgroepen met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9cef62b8-d889-4d16-b4d0-58639539a418
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1c8db773febb163d9cb010d23f2913b5ebe0fa94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-powershell"></a><span data-ttu-id="558eb-103">Netwerk met behulp van PowerShell-beveiligingsgroepen maken</span><span class="sxs-lookup"><span data-stu-id="558eb-103">Create network security groups using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

<span data-ttu-id="558eb-104">Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek.</span><span class="sxs-lookup"><span data-stu-id="558eb-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="558eb-105">Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="558eb-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="558eb-106">Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="558eb-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="558eb-107">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="558eb-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="558eb-108">U kunt ook [nsg's maken in het klassieke implementatiemodel Hallo](virtual-networks-create-nsg-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="558eb-108">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="558eb-109">Hallo voorbeeld PowerShell onderstaande opdrachten verwacht een eenvoudige omgeving al gemaakt dat is gebaseerd op Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="558eb-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="558eb-110">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, moet u eerst Hallo testomgeving verder door de implementatie [deze sjabloon](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), klikt u op **tooAzure implementeren**, standaardparameterwaarden Hallo vervangen indien nodig, en volg de instructies in Hallo in Hallo portal.</span><span class="sxs-lookup"><span data-stu-id="558eb-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="558eb-111">Hoe toocreate NSG Hallo voor Hallo front-end-subnet</span><span class="sxs-lookup"><span data-stu-id="558eb-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="558eb-112">een NSG met de naam toocreate *NSG-FrontEnd* Hallo volgende stappen uit op basis van Hallo scenario, voltooien:</span><span class="sxs-lookup"><span data-stu-id="558eb-112">toocreate an NSG named *NSG-FrontEnd* based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="558eb-113">Als u Azure PowerShell nog nooit hebt gebruikt, raadpleegt u [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) en volg de instructies Hallo alle Hallo manier toohello toosign beëindigen in Azure en uw abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="558eb-113">If you have never used Azure PowerShell, see [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) and follow hello instructions all hello way toohello end toosign into Azure and select your subscription.</span></span>
2. <span data-ttu-id="558eb-114">Maak een beveiligingsregel toegang te verlenen vanaf Hallo Internet tooport 3389.</span><span class="sxs-lookup"><span data-stu-id="558eb-114">Create a security rule allowing access from hello Internet tooport 3389.</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name rdp-rule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
    ```

3. <span data-ttu-id="558eb-115">Maak een beveiligingsregel toegang te verlenen vanaf Hallo Internet tooport 80.</span><span class="sxs-lookup"><span data-stu-id="558eb-115">Create a security rule allowing access from hello Internet tooport 80.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule -Description "Allow HTTP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 101 `
    -SourceAddressPrefix Internet -SourcePortRange * -DestinationAddressPrefix * `
    -DestinationPortRange 80
    ```

4. <span data-ttu-id="558eb-116">Hallo regels bovenstaande tooa nieuwe NSG met de naam toevoegen **NSG-FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="558eb-116">Add hello rules created above tooa new NSG named **NSG-FrontEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG -Location westus `
    -Name "NSG-FrontEnd" -SecurityRules $rule1,$rule2
    ```

5. <span data-ttu-id="558eb-117">Controleer Hallo regels die zijn gemaakt in Hallo NSG door Hallo volgende te typen:</span><span class="sxs-lookup"><span data-stu-id="558eb-117">Check hello rules created in hello NSG by typing hello following:</span></span>

    ```powershell
    $nsg
    ```
   
    <span data-ttu-id="558eb-118">Uitvoer weergeven alleen Hallo beveiligingsregels voor verbindingen:</span><span class="sxs-lookup"><span data-stu-id="558eb-118">Output showing just hello security rules:</span></span>
   
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
                                   "Description": "Allow RDP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "3389",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 100,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 },
                                 {
                                   "Name": "web-rule",
                                   "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                   "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
                                   "Description": "Allow HTTP",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "80",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 101,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]
6. <span data-ttu-id="558eb-119">Koppelen Hallo NSG hierboven toohello gemaakt *FrontEnd* subnet.</span><span class="sxs-lookup"><span data-stu-id="558eb-119">Associate hello NSG created above toohello *FrontEnd* subnet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd `
    -AddressPrefix 192.168.1.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="558eb-120">Uitvoer weergeven alleen Hallo *FrontEnd* subnetinstellingen, kennisgeving Hallo waarde voor Hallo **NetworkSecurityGroup** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="558eb-120">Output showing only hello *FrontEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
                    Subnets           : [
                                          {
                                            "Name": "FrontEnd",
                                            "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                                            "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                            "AddressPrefix": "192.168.1.0/24",
                                            "IpConfigurations": [
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                              },
                                              {
                                                "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                              }
                                            ],
                                            "NetworkSecurityGroup": {
                                              "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                            },
                                            "RouteTable": null,
                                            "ProvisioningState": "Succeeded"
                                          }
   
   > [!WARNING]
   > <span data-ttu-id="558eb-121">Hallo-uitvoer voor bovenstaande Hallo-opdracht geeft Hallo-inhoud voor Hallo virtueel netwerk configuration-object bestaat alleen op Hallo-computer waarop u PowerShell worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="558eb-121">hello output for hello command above shows hello content for hello virtual network configuration object, which only exists on hello computer where you are running PowerShell.</span></span> <span data-ttu-id="558eb-122">U moet toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave deze tooAzure instellingen.</span><span class="sxs-lookup"><span data-stu-id="558eb-122">You need toorun hello `Set-AzureRmVirtualNetwork` cmdlet toosave these settings tooAzure.</span></span>
   > 
   > 
7. <span data-ttu-id="558eb-123">Hallo nieuwe VNet instellingen tooAzure opslaan.</span><span class="sxs-lookup"><span data-stu-id="558eb-123">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="558eb-124">Uitvoer slechts deel van het NSG hello wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="558eb-124">Output showing just hello NSG portion:</span></span>
   
        "NetworkSecurityGroup": {
          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
        }

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="558eb-125">Hoe toocreate Hallo NSG voor subnet backend-Hallo</span><span class="sxs-lookup"><span data-stu-id="558eb-125">How toocreate hello NSG for hello back-end subnet</span></span>
<span data-ttu-id="558eb-126">een NSG met de naam toocreate *NSG-back-end* Hallo volgende stappen uit op basis van de bovenstaande scenario voor hello, voltooien:</span><span class="sxs-lookup"><span data-stu-id="558eb-126">toocreate an NSG named *NSG-BackEnd* based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="558eb-127">Maak een beveiligingsregel toegang te verlenen vanaf Hallo front-end-subnet tooport 1433 (standaardpoort die wordt gebruikt door SQL Server).</span><span class="sxs-lookup"><span data-stu-id="558eb-127">Create a security rule allowing access from hello front-end subnet tooport 1433 (default port used by SQL Server).</span></span>

    ```powershell
    $rule1 = New-AzureRmNetworkSecurityRuleConfig -Name frontend-rule `
    -Description "Allow FE subnet" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 100 `
    -SourceAddressPrefix 192.168.1.0/24 -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 1433
    ```

2. <span data-ttu-id="558eb-128">Maak een beveiligingsregel toohello toegang tot Internet blokkeren.</span><span class="sxs-lookup"><span data-stu-id="558eb-128">Create a security rule blocking access toohello Internet.</span></span>

    ```powershell
    $rule2 = New-AzureRmNetworkSecurityRuleConfig -Name web-rule `
    -Description "Block Internet" `
    -Access Deny -Protocol * -Direction Outbound -Priority 200 `
    -SourceAddressPrefix * -SourcePortRange * `
    -DestinationAddressPrefix Internet -DestinationPortRange *
    ```

3. <span data-ttu-id="558eb-129">Hallo regels bovenstaande tooa nieuwe NSG met de naam toevoegen **NSG-back-end**.</span><span class="sxs-lookup"><span data-stu-id="558eb-129">Add hello rules created above tooa new NSG named **NSG-BackEnd**.</span></span>

    ```powershell
    $nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName TestRG `
    -Location westus -Name "NSG-BackEnd" `
    -SecurityRules $rule1,$rule2
    ```

4. <span data-ttu-id="558eb-130">Koppelen Hallo NSG hierboven toohello gemaakt *back-end* subnet.</span><span class="sxs-lookup"><span data-stu-id="558eb-130">Associate hello NSG created above toohello *BackEnd* subnet.</span></span>

    ```powershell
    Set-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name BackEnd ` 
    -AddressPrefix 192.168.2.0/24 -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="558eb-131">Uitvoer weergeven alleen Hallo *back-end* subnetinstellingen, kennisgeving Hallo waarde voor Hallo **NetworkSecurityGroup** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="558eb-131">Output showing only hello *BackEnd* subnet settings, notice hello value for hello **NetworkSecurityGroup** property:</span></span>
   
        Subnets           : [
                      {
                        "Name": "BackEnd",
                        "Etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                        "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                        "AddressPrefix": "192.168.2.0/24",
                        "IpConfigurations": [...],
                        "NetworkSecurityGroup": {
                          "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "RouteTable": null,
                        "ProvisioningState": "Succeeded"
                      }
5. <span data-ttu-id="558eb-132">Hallo nieuwe VNet instellingen tooAzure opslaan.</span><span class="sxs-lookup"><span data-stu-id="558eb-132">Save hello new VNet settings tooAzure.</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

## <a name="how-tooremove-an-nsg"></a><span data-ttu-id="558eb-133">Hoe tooremove een NSG</span><span class="sxs-lookup"><span data-stu-id="558eb-133">How tooremove an NSG</span></span>
<span data-ttu-id="558eb-134">toodelete een bestaande NSG aangeroepen *NSG-Frontend* in dit geval Volg Hallo van de volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="558eb-134">toodelete an existing NSG, called *NSG-Frontend* in this case, follow hello step below:</span></span>

<span data-ttu-id="558eb-135">Hallo uitvoeren **verwijderen AzureRmNetworkSecurityGroup** hieronder wordt weergegeven en worden ervoor tooinclude Hallo resource groep Hallo NSG is in.</span><span class="sxs-lookup"><span data-stu-id="558eb-135">Run hello **Remove-AzureRmNetworkSecurityGroup** shown below and be sure tooinclude hello resource group hello NSG is in.</span></span>

```powershell
Remove-AzureRmNetworkSecurityGroup -Name "NSG-FrontEnd" -ResourceGroupName "TestRG"
```


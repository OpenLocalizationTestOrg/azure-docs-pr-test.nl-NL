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
# <a name="create-a-virtual-network-using-an-azure-resource-manager-template"></a>Een virtueel netwerk met een Azure Resource Manager-sjabloon maken

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure heeft twee implementatiemodellen: Azure Resource Manager en klassiek. Microsoft raadt u aan voor het maken van resources via Hallo Resource Manager-implementatiemodel. Hallo toolearn informatie over de verschillen tussen Hallo twee modellen, Hallo lezen [begrijpen Azure-implementatiemodellen](../azure-resource-manager/resource-manager-deployment-model.md) artikel.
 
Dit artikel wordt uitgelegd hoe toocreate een VNet via Hallo Resource Manager deployment model met een Azure Resource Manager-sjabloon. Ook kunt u een VNet via Resource Manager, met andere hulpprogramma's maken of maak een VNet via de klassieke implementatiemodel Hallo door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
- [Portal](virtual-networks-create-vnet-arm-pportal.md)
- [PowerShell](virtual-networks-create-vnet-arm-ps.md)
- [CLI](virtual-networks-create-vnet-arm-cli.md)
- [Sjabloon](virtual-networks-create-vnet-arm-template-click.md)
- [Portal (klassiek)](virtual-networks-create-vnet-classic-pportal.md)
- [PowerShell (klassiek)](virtual-networks-create-vnet-classic-netcfg-ps.md)
- [CLI (klassiek)](virtual-networks-create-vnet-classic-cli.md)

U leert hoe toodownload wijzigen en bestaande ARM-sjabloon vanuit GitHub en Hallo sjabloon implementeren vanuit GitHub, PowerShell en hello Azure CLI.

Als u wilt Hallo ARM-sjabloon rechtstreeks vanuit GitHub, zonder deze te wijzigen implementeren, gaat u verder te[een sjabloon implementeren vanuit github](#deploy-the-arm-template-by-using-click-to-deploy).

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="download-and-understand-hello-azure-resource-manager-template"></a>Hello Azure Resource Manager-sjabloon downloaden en begrijpen
U kunt bestaande Hallo-sjabloon voor het maken van een VNet en twee subnets vanuit GitHub downloaden, breng eventuele wijzigingen die u mogelijk wilt gebruiken en het opnieuw gebruiken. toodo voltooien dus Hallo stappen te volgen:

1. Navigeer te[pagina voorbeeldsjabloon Hallo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
2. Klik op **azuredeploy.json** en vervolgens op **RAW**.
3. Sla Hallo bestand tooa een lokale map op uw computer.
4. Als u bekend met sjablonen bent, slaat u toostep 7.
5. Open Hallo-bestand die u zojuist hebt opgeslagen en bekijkt hello inhoud onder **parameters** in regel 5. ARM-sjabloonparameters bieden een tijdelijke aanduiding voor waarden die kunnen worden ingevuld tijdens de implementatie.
   
   | Parameter | Beschrijving |
   | --- | --- |
   | **location** |Azure-regio waar Hallo VNet wordt gemaakt |
   | **vnetName** |Naam voor Hallo nieuwe VNet |
   | **addressPrefix** |Adresruimte voor Hallo VNet, in CIDR-notatie |
   | **subnet1Name** |Naam voor Hallo eerste VNet |
   | **subnet1Prefix** |CIDR-blokkering voor het eerste subnet Hallo |
   | **subnet2Name** |Naam voor Hallo tweede VNet |
   | **subnet2Prefix** |CIDR-blokkering voor Hallo tweede subnet |
   
   > [!IMPORTANT]
   > Azure Resource Manager-sjablonen die in GitHub worden bewaard, kunnen in de loop van de tijd veranderen. Zorg ervoor dat u Hallo sjabloon controleren voordat u deze gebruikt.
   > 
   > 
6. Controleer de inhoud Hallo onder **resources** en Let op Hallo volgende:
   
   * **type**. Type resource dat door Hallo sjabloon wordt gemaakt. In dit geval **Microsoft.Network/virtualNetworks**, die een VNet vertegenwoordigen.
   * **Naam**. Naam voor Hallo resource. Kennisgeving Hallo gebruik van **[parameters('vnetName')]**, dit betekent Hallo naam wordt geleverd als invoer door Hallo gebruiker of een parameterbestand tijdens de implementatie.
   * **Eigenschappen**. Lijst met eigenschappen voor Hallo resource. Deze sjabloon maakt gebruik van Hallo ruimte en subnet adreseigenschappen tijdens het maken van een VNet.
7. Navigeer terug te[pagina voorbeeldsjabloon Hallo](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vnet-two-subnets).
8. Klik op **azuredeploy-paremeters.json** en vervolgens op **RAW**.
9. Sla Hallo bestand tooa een lokale map op uw computer.
10. Open Hallo bestand dat u zojuist hebt opgeslagen en bewerk Hallo-waarden voor Hallo-parameters. Gebruik Hallo volgende waarden onder toodeploy hello VNet in Hallo scenario beschreven:

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

11. Hallo-bestand opslaan.


## <a name="deploy-hello-template-using-powershell"></a>Met behulp van PowerShell Hallo-sjabloon implementeren

Volgende stappen toodeploy Hallo-sjabloon die u hebt gedownload met behulp van PowerShell Hallo voltooien:

1. Installeren en configureren van Azure PowerShell via Hallo stappen in Hallo [hoe tooInstall en configureer Azure PowerShell](/powershell/azure/overview) artikel.
2. Voer Hallo opdracht toocreate na een nieuwe resourcegroep:

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    Hallo opdracht maakt u een resourcegroep met de naam *TestRG* in Hallo *VS-midden* azure-regio. Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.

    Verwachte uitvoer:

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/[Id]/resourceGroups/TestRG

3. Voer Hallo na de opdracht toodeploy Hallo nieuwe VNet met het Hallo-sjabloon en de parameterbestanden die u hebt gedownload en hierboven zijn gewijzigd:

    ```powershell
    New-AzureRmResourceGroupDeployment -Name TestVNetDeployment -ResourceGroupName TestRG `
    -TemplateFile C:\ARM\azuredeploy.json -TemplateParameterFile C:\ARM\azuredeploy-parameters.json
    ```

    Verwachte uitvoer:
   
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
4. Voer Hallo volgende opdracht tooview Hallo eigenschappen van Hallo nieuwe VNet:

    ```powershell
    Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

    Verwachte uitvoer:

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

## <a name="deploy-hello-template-using-click-to-deploy"></a>Implementeren met click-to-deploy Hallo-sjabloon

U kunt vooraf gedefinieerde Azure Resource Manager sjablonen geüploade tooa GitHub-opslagplaats beheerd door Microsoft en community open toohello hergebruiken. Deze sjablonen kunnen rechtstreeks uit de GitHub worden geïmplementeerd of gedownload en gewijzigd toofit uw behoeften. toodeploy een sjabloon die wordt gemaakt van een VNet met twee subnetten voltooid Hallo stappen te volgen:

1. Vanuit een browser navigeren te[https://github.com/Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates).
2. Schuif naar beneden Hallo lijst met sjablonen en klikt u op **101-vnet-two-subnets**. Controleer de Hallo **README.md** -bestand, zoals hieronder wordt weergegeven.

    ![READEME.md-bestand in github](./media/virtual-networks-create-vnet-arm-template-click-include/figure1.png)

3. Klik op **tooAzure implementeren**. Voer indien nodig uw Azure-aanmeldingsreferenties in. 
4. In Hallo **Parameters** blade Voer Hallo waarden u wilt dat uw nieuwe VNet toouse toocreate en klik vervolgens op **OK**. Hallo ziet volgende afbeelding Hallo waarden voor Hallo scenario:
   
    ![ARM-sjabloonparameters](./media/virtual-networks-create-vnet-arm-template-click-include/figure2.png)

5. Klik op **resourcegroep** en selecteert u een groep resource tooadd Hallo VNet-naar- of klik op **nieuw** tooadd hello VNet tooa nieuwe resourcegroep. Hallo volgende afbeelding ziet u Hallo resource groepsinstellingen voor een nieuwe resourcegroep aangeroepen **TestRG**:

    ![Resourcegroep](./media/virtual-networks-create-vnet-arm-template-click-include/figure3.png)

6. Wijzig indien nodig, Hallo **abonnement** en **locatie** instellingen voor uw VNet.
7. Als u niet dat toosee hello VNet als tegel in Hallo wilt **Startboard**, uitschakelen **pincode tooStartboard**.
8. Klik op **juridische voorwaarden**, Hallo voorwaarden lezen en klikt u op **kopen** tooagree. 
9. Klik op **maken** toocreate hello VNet.
   
    ![Tegel implementatie in Preview Portal verzenden](./media/virtual-networks-create-vnet-arm-template-click-include/figure4.png)

10. Zodra Hallo-implementatie is voltooid, in hello Azure-portal klikt u op **meer services**, type *virtuele netwerken* in Hallo filter dat wordt weergegeven, klikt u virtuele netwerken toosee Hallo virtuele netwerken blade. Klik op de blade Hallo *TestVNet*. In Hallo *TestVNet* blade, klikt u op **subnetten** toosee Hallo gemaakt subnetten, zoals wordt weergegeven in de volgende afbeelding Hallo:
    
     ![VNet maken in de Preview Portal](./media/virtual-networks-create-vnet-arm-template-click-include/figure5.png)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe tooconnect:

- Een virtueel netwerk van virtuele machine (VM) tooa door Hallo lezen [maken van een virtuele machine van Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md) of [maken van een Linux-VM](../virtual-machines/linux/quick-create-portal.md) artikelen. In plaats van een VNet en een subnet maken in stappen van Hallo artikelen hello, kunt u een bestaande VNet en een subnet tooconnect een virtuele machine aan.
- virtueel netwerk tooother virtuele netwerken door te lezen Hallo Hallo [VNets verbinden](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) artikel.
- Hallo virtueel netwerk tooan on-premises netwerk met een site-naar-site virtueel particulier netwerk (VPN) of het ExpressRoute-circuit. Meer informatie over hoe u door te lezen Hallo [verbinding maken met een VNet tooan on-premises netwerk via een site-naar-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) en [koppelen van een VNet tooan ExpressRoute-circuit](../expressroute/expressroute-howto-linkvnet-arm.md) artikelen.

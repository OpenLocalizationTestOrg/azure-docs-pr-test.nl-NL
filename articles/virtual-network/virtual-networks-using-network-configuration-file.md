---
title: een Azure-netwerk (klassiek) - configuratiebestand netwerk aaaConfigure | Microsoft Docs
description: Meer informatie over hoe toocreate en wijzigen van virtuele netwerken (klassiek) te exporteren en importeren van een configuratiebestand netwerk wijzigen.
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: c29b9059-22b0-444e-bbfe-3e35f83cde2f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 009108d4315b4b7146d3f1cf2436ee211d2d89ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-classic-using-a-network-configuration-file"></a>Een virtueel netwerk (klassiek) met een configuratiebestand netwerk configureren
> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties Hallo Resource Manager-implementatiemodel gebruiken.

U kunt maken en configureren van een virtueel netwerk (klassiek) met een netwerk-configuratiebestand met hello Azure-opdrachtregelinterface (CLI) 1.0 of Azure PowerShell. U kunt maken of wijzigen van een virtueel netwerk via hello Azure Resource Manager-implementatiemodel met een netwerk configuratiebestand. U kan hello Azure portal toocreate gebruiken of een virtueel netwerk (klassiek) met een configuratiebestand netwerk wijzigen, maar u kunt Hallo toocreate met Azure portal een virtueel netwerk (klassiek), zonder gebruik van een netwerk-configuratiebestand.

Maken en configureren van een virtueel netwerk (klassiek) met een netwerk-configuratiebestand vereist exporteren, wijzigen en het Hallo-bestand te importeren.

## <a name="export"></a>Een netwerk-configuratiebestand exporteren

U kunt PowerShell of hello Azure CLI tooexport een configuratiebestand netwerk gebruiken. PowerShell exporteert een XML-bestand, terwijl hello Azure CLI een json-bestand exporteert.

### <a name="powershell"></a>PowerShell
 
1. [Azure PowerShell installeren en meld u aan tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Wijzig de directory hello (en zorg ervoor dat deze bestaat) en de bestandsnaam in Hallo de volgende opdracht als de gewenste en vervolgens uitvoeren Hallo opdracht tooexport Hallo netwerk configuratiebestand:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Installeer Azure CLI 1.0 Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Hallo resterende stappen vanaf een opdrachtprompt Azure CLI 1.0 voltooien.
2. Aanmelden tooAzure hiertoe Hallo `azure login` opdracht.
3. Of u in de asm-modus hiertoe Hallo `azure config mode asm` opdracht.
4. Wijzig de directory hello (en zorg ervoor dat deze bestaat) en de bestandsnaam in Hallo de volgende opdracht als de gewenste en vervolgens uitvoeren Hallo opdracht tooexport Hallo netwerk configuratiebestand:
    
    ```azurecli
    azure network export c:\azure\networkconfig.json
    ```

## <a name="create-or-modify-a-network-configuration-file"></a>Maken of een configuratiebestand netwerk wijzigen

Een configuratiebestand netwerk is een XML-bestand (als u PowerShell) of een json-bestand (als u hello Azure CLI). Hallo-bestand in een tekst- of XML-/ json-editor kunt u bewerken. Hallo [netwerk-instellingen voor het configuratiebestand schema](https://msdn.microsoft.com/library/azure/jj157100.aspx) artikel bevat informatie voor alle instellingen. Zie voor aanvullende uitleg van Hallo instellingen [virtuele netwerken en instellingen weergeven](virtual-network-manage-network.md#view-vnet). Hallo-wijzigingen die u aanbrengt toohello bestand:

- Moet in overeenstemming met de Hallo schema of importeren Hallo netwerk configuratiebestand zal mislukken.
- Overschrijf de bestaande netwerkinstellingen voor uw abonnement, dus Wees daarom uiterst voorzichtig als u wijzigingen aanbrengt. Verwijs bijvoorbeeld naar Hallo voorbeeld netwerk configuratiebestanden die volgen. Zeg Hallo oorspronkelijke bestand bevat twee **VirtualNetworkSite** exemplaren en u gewijzigd, zoals getoond in Hallo voorbeelden. Als u Hallo bestand importeert, Azure Hallo virtueel netwerk voor Hallo verwijdert **VirtualNetworkSite** exemplaar dat u in het Hallo-bestand verwijderd. Dit scenario vereenvoudigde wordt ervan uitgegaan dat er zijn geen resources zijn in het virtuele netwerk hello, alsof er, Hallo virtueel netwerk kan niet worden verwijderd en Hallo importeren mislukken.

> [!IMPORTANT]
> Azure overweegt een subnet met iets geïmplementeerd tooit als **gebruikt**. Wanneer een subnet gebruikt wordt, kan niet worden gewijzigd. Voordat u informatie over het subnet in een configuratiebestand netwerk wijzigt, verplaatst u alles wat u hebt geïmplementeerd toohello subnet tooa ander subnet dat is niet wordt gewijzigd. Zie [verplaatsen van een virtuele machine of Rolinstantie tooa ander Subnet](virtual-networks-move-vm-role-to-subnet.md) voor meer informatie.

### <a name="example-xml-for-use-with-powershell"></a>XML-voorbeeld voor gebruik met PowerShell

Hallo volgende voorbeeldconfiguratiebestand voor netwerk maakt een virtueel netwerk met de naam *myVirtualNetwork* met een adresruimte van *10.0.0.0/16* in Hallo *VS-Oost* Azure de regio. Hallo virtueel netwerk bevat één subnet met de naam *mySubnet* met een adresvoorvoegsel van *10.0.0.0/24*.

```xml
<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
  <VirtualNetworkConfiguration>
    <Dns />
    <VirtualNetworkSites>
      <VirtualNetworkSite name="myVirtualNetwork" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="mySubnet">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>
  </VirtualNetworkConfiguration>
</NetworkConfiguration>
```

Als Hallo netwerk-configuratiebestand exporteren geen inhoud bevat, kunt u Hallo XML in het vorige voorbeeld Hallo kopiëren en plak deze in een nieuw bestand.

### <a name="example-json-for-use-with-hello-azure-cli-10"></a>Voorbeeld JSON voor gebruik met hello Azure CLI 1.0

Hallo volgende voorbeeldconfiguratiebestand voor netwerk maakt een virtueel netwerk met de naam *myVirtualNetwork* met een adresruimte van *10.0.0.0/16* in Hallo *VS-Oost* Azure de regio. Hallo virtueel netwerk bevat één subnet met de naam *mySubnet* met een adresvoorvoegsel van *10.0.0.0/24*.

```json
{
   "VirtualNetworkConfiguration" : {
      "Dns" : "",
      "VirtualNetworkSites" : [
         {
            "AddressSpace" : [ "10.0.0.0/16" ],
            "Location" : "East US",
            "Name" : "myVirtualNetwork",
            "Subnets" : [
               {
                  "AddressPrefix" : "10.0.0.0/24",
                  "Name" : "mySubnet"
               }
            ]
         }
      ]
   }
}
```

Als Hallo netwerk-configuratiebestand exporteren geen inhoud bevat, kunt u Hallo json in het vorige voorbeeld Hallo kopiëren en plak deze in een nieuw bestand.

## <a name="import"></a>Een configuratiebestand netwerk importeren

U kunt PowerShell of hello Azure CLI tooimport een configuratiebestand netwerk gebruiken. PowerShell importeert een XML-bestand, terwijl hello Azure CLI een json-bestand importeert. Als Hallo importeren is mislukt, controleert u dat bestand Hallo voldoet aan de Hallo [network-configuratieschema](https://msdn.microsoft.com/library/azure/jj157100.aspx). 

### <a name="powershell"></a>PowerShell
 
1. [Azure PowerShell installeren en meld u aan tooAzure](/powershell/azure/install-azure-ps?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Hallo directory en de bestandsnaam in Hallo na de opdracht zo nodig wijzigen en voer vervolgens Hallo opdracht tooimport Hallo netwerk configuratiebestand:
 
    ```powershell
    Set-AzureVNetConfig  -ConfigurationPath c:\azure\networkconfig.xml
    ```

### <a name="azure-cli-10"></a>Azure CLI 1.0

1. [Installeer Azure CLI 1.0 Hallo](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Hallo resterende stappen vanaf een opdrachtprompt Azure CLI 1.0 voltooien.
2. Aanmelden tooAzure hiertoe Hallo `azure login` opdracht.
3. Of u in de asm-modus hiertoe Hallo `azure config mode asm` opdracht.
4. Hallo directory en de bestandsnaam in Hallo na de opdracht zo nodig wijzigen en voer vervolgens Hallo opdracht tooimport Hallo netwerk configuratiebestand:

    ```azurecli
    azure network import c:\azure\networkconfig.json
    ```

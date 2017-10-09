---
title: 'Verbinding maken met de klassieke virtuele netwerken tooAzure Resource Manager VNets: PowerShell | Microsoft Docs'
description: Meer informatie over hoe toocreate een VPN-verbinding tussen het klassieke vnet's en Resource Manager-VNets met VPN-Gateway en PowerShell
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a>Virtuele netwerken van verschillende implementatiemodellen verbinden met PowerShell



Dit artikel laat zien hoe tooconnect klassieke vnet's tooResource Manager VNets tooallow Hallo bronnen in Hallo afzonderlijke implementatie modellen toocommunicate met elkaar. Hallo stappen in dit artikel PowerShell gebruiken, maar u kunt ook maken met deze configuratie met behulp van hello Azure-portal door Hallo artikel in deze lijst te selecteren.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Verbinding maken met een klassiek VNet tooa Resource Manager VNet is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE. U kunt een verbinding tussen VNets die tot verschillende abonnementen behoren en in verschillende regio's maken. U kunt ook VNets die u al verbindingen tooon-premises netwerken hebt, verbinden, zolang het Hallo-gateway die is geconfigureerd met dynamische of op basis van route is. Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel. 

Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooinstead overwegen deze met behulp van VNet-Peering te verbinden. Bij VNet-peering wordt geen VPN-gateway gebruikt. Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie. 

## <a name="before-beginning"></a>Voordat u begint

Hallo volgt helpt u bij het Hallo-instellingen nodig tooconfigure een dynamisch of op route gebaseerde gateway voor elk VNet en een VPN-verbinding maken tussen Hallo gateways. Deze configuratie biedt geen ondersteuning voor statische of op beleid gebaseerde gateways.

### <a name="prerequisites"></a>Vereisten

* Beide VNets zijn al gemaakt.
* Hallo-adresbereiken voor Hallo VNets met elkaar overlappen, of niet overlappen met een van de bereiken Hallo voor Hallo gateways mogen worden verbonden met andere verbindingen.
* U kunt de meest recente PowerShell-cmdlets Hallo hebt geïnstalleerd. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie. Zorg ervoor dat u Hallo Service Management (SM) en Hallo Resource Manager (RM)-cmdlets installeren. 

### <a name="exampleref"></a>Voorbeeldinstellingen

U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.

**Klassieke VNet-instellingen**

VNet-naam = ClassicVNet <br>
Locatie VS-West = <br>
Adresruimten voor virtueel netwerk 10.0.0.0/24 = <br>
Subnet-1 = 10.0.0.0/27 <br>
GatewaySubnet 10.0.0.32/29 = <br>
De naam van het lokale netwerk RMVNetLocal = <br>
GatewayType DynamicRouting =

**Resource Manager VNet-instellingen**

VNet-naam = RMVNet <br>
Resourcegroep RG1 = <br>
Virtueel netwerk-IP-adresruimten 192.168.0.0/16 = <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet 192.168.0.0/26 = <br>
Locatie VS-Oost = <br>
Het openbare IP-gatewaynaam gwpip = <br>
Lokale netwerkgateway ClassicVNetLocal = <br>
Naam van de virtuele netwerkgateway RMGateway = <br>
Gateway-IP-adresconfiguratie gwipconfig =

## <a name="createsmgw"></a>Sectie 1: Configureer Hallo klassieke VNet
### <a name="part-1---download-your-network-configuration-file"></a>Deel 1: Download het configuratiebestand van uw netwerk
1. Meld u bij tooyour Azure-account in Hallo PowerShell-console met verhoogde rechten. Hallo vraagt volgende cmdlet u om Hallo aanmeldingsreferenties voor uw Azure-Account. Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell zijn. U Hallo SM PowerShell-cmdlets toocomplete dit deel van het Hallo-configuratie gebruiken.

  ```powershell
  Add-AzureAccount
  ```
2. Exporteer het bestand met de Azure-netwerk door het uitvoeren van de volgende opdracht Hallo. U kunt Hallo-locatie van Hallo tooexport tooa verschillende bestandslocatie indien nodig wijzigen.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. Open Hallo .xml-bestand dat u hebt gedownload tooedit deze. Zie voor een voorbeeld van netwerk-configuratiebestand Hallo Hallo [Network-configuratieschema](https://msdn.microsoft.com/library/jj157100.aspx).

### <a name="part-2--verify-hello-gateway-subnet"></a>Deel 2 - Hallo gatewaysubnet controleren
In Hallo **VirtualNetworkSites** element, een gateway subnet tooyour VNet toevoegen als een nog niet is gemaakt. Als u werkt met Hallo netwerk configuratiebestand, Hallo gatewaysubnet moet de naam 'GatewaySubnet' of Azure kan niet herkennen en gebruiken als een gatewaysubnet.

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

**Voorbeeld:**

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a>Deel 3: de lokale netwerksite Hallo toevoegen
lokale netwerksite Hallo die u toevoegen vertegenwoordigt Hallo RM VNet toowhich gewenste tooconnect. Voeg een **LocalNetworkSites** element toohello bestand als een nog niet bestaat. Op dit moment in configuratie Hallo mag Hallo VPNGatewayAddress geldig openbaar IP-adres omdat we nog Hallo gateway voor Hallo Resource Manager VNet dat nog niet hebt gemaakt. Wanneer we Hallo gateway maakt, wordt vervangen door dit tijdelijke aanduiding voor IP-adres Hallo juiste openbare IP-adres dat is toegewezen toohello RM-gateway.

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a>Deel 4 – hello VNet koppelen aan de lokale netwerksite Hallo
In deze sectie opgegeven lokale netwerksite Hallo dat u wilt dat tooconnect VNet-naar-Hallo. In dit geval is het Hallo Resource Manager VNet dat u eerder naar verwezen. Zorg ervoor dat Hallo-namen die overeenkomen met. Deze stap maakt een gateway niet. Hiermee geeft u Hallo lokale netwerk die Hallo gateway maakt verbinding met.

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a>Deel 5 - Hallo bestand opslaan en uploaden
Hallo-bestand opslaan en vervolgens tooAzure door het uitvoeren van de volgende opdracht Hallo importeren. Zorg ervoor dat u het bestandspad Hallo die nodig zijn voor uw omgeving wijzigen.

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

Hier ziet u een vergelijkbaar resultaat Hallo importeren is voltooid wordt weergegeven.

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a>Deel 6 – Hallo-gateway maken

Raadpleeg voordat u dit voorbeeld, toohello netwerk-configuratiebestand dat u hebt gedownload voor Hallo exacte die Azure namen toosee verwacht. Hallo netwerk configuratiebestand bevat Hallo waarden voor uw klassieke virtuele netwerken. Soms Hallo Hallo namen voor klassieke die vnet 's zijn gewijzigd in Hallo netwerk configuratiebestand bij het maken van klassieke VNet-instellingen in Azure-portal vanwege toohello verschillen in Hallo implementatiemodellen. Bijvoorbeeld, als u Azure portal toocreate een klassiek VNet met de naam 'Klassieke VNet' en deze is gemaakt in een resourcegroep met de naam 'ClassicRG' hello gebruikt, Hallo-naam die is opgenomen in het configuratiebestand Hallo-netwerk is geconverteerde too'Group ClassicRG klassieke VNet'. Wanneer u opgeeft Hallo-naam van een VNet dat spaties bevat, Gebruik aanhalingstekens rond het Hallo-waarde.


Hallo voorbeeld toocreate een gateway voor dynamische routering volgende gebruiken:

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

U kunt de status Hallo van Hallo gateway controleren met behulp van Hallo **Get-AzureVNetGateway** cmdlet.

## <a name="creatermgw"></a>Deel 2: Hallo RM-VNet-gateway configureren
een VPN-gateway voor Hallo RM-VNet toocreate Volg Hallo instructies te volgen. Hallo stappen totdat niet worden gestart nadat u Hallo openbaar IP-adres voor de gateway Hallo klassieke VNet hebt opgehaald. 

1. Tooyour aanmelden met Azure-account in Hallo PowerShell-console. Hallo vraagt volgende cmdlet u om Hallo aanmeldingsreferenties voor uw Azure-Account. Na het aanmelden, worden de instellingen van uw account zodat ze beschikbaar tooAzure PowerShell zijn gedownload.

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  Een lijst met uw Azure-abonnementen ophalen als u meer dan één abonnement hebt.

  ```powershell
  Get-AzureRmSubscription
  ```
   
  Hallo-abonnement dat u wilt dat toouse opgeven.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. Maak een lokale netwerkgateway. Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie in een virtueel netwerk. In dit geval verwijst de lokale netwerkgateway Hallo tooyour klassieke VNet. Geef het een naam waarmee Azure kunt tooit verwijzen, en ook het adresruimtevoorvoegsel Hallo opgeven. Hallo IP-adresvoorvoegsel u opgeven welk verkeer toosend tooyour lokale locatie tooidentify maakt gebruik van Azure. Als u tooadjust Hallo informatie hier later voordat u de gateway maakt kunt u Hallo waarden en Voer Hallo voorbeeld opnieuw wijzigen.
   
   **-Naam** gewenste tooassign toorefer toohello lokale netwerkgateway Hallo-naam is.<br>
   **-AddressPrefix** Hallo adresruimte voor het klassieke VNet is.<br>
   **-GatewayIpAddress** Hallo openbare IP-adres van gateway Hallo klassieke VNet. Zorg ervoor dat toochange Hallo volgende steekproef tooreflect Hallo juiste IP-adres.<br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. Een openbaar IP-adres toobe toegewezen toohello virtuele netwerkgateway voor Resource Manager VNet Hallo aanvragen. U kunt Hallo IP-adres dat u wilt dat toouse niet opgeven. Hallo IP-adres wordt dynamisch toegewezen toohello virtuele netwerkgateway. Dit betekent echter niet Hallo IP-adreswijzigingen dat. de enige keer Hallo Hallo virtuele IP-adreswijzigingen netwerkgateway is wanneer Hallo gateway is verwijderd en opnieuw gemaakt. Wordt niet gewijzigd via vergroten of verkleinen, opnieuw wordt ingesteld, of een andere interne onderhoud of upgrades worden uitgevoerd Hallo-gateway.

  In deze stap wordt ook een variabele die wordt gebruikt in een latere stap instellen.

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. Controleer of het virtuele netwerk een gatewaysubnet. Als er geen gatewaysubnet bestaat, Voeg een. Zorg ervoor dat het gatewaysubnet Hallo heet *GatewaySubnet*.
5. Hallo subnet dat wordt gebruikt voor de gateway Hallo door het uitvoeren van de volgende opdracht Hallo ophalen. In deze stap wordt ook een variabele toobe gebruikt in de volgende stap Hallo instellen.
   
   **-Naam** Hallo-naam van uw VNet Resource Manager.<br>
   **-ResourceGroupName** is Hallo resourcegroep die Hallo VNet is gekoppeld. Hallo gatewaysubnet moet al bestaan voor dit VNet en moet de naam *GatewaySubnet* toowork goed.<br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. Hallo-gateway voor IP-adressen van de configuratie maken. Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse. Hallo voorbeeld toocreate na de configuratie van uw gateway gebruiken.

  In deze stap Hallo **- SubnetId** en **- PublicIpAddressId** parameters moeten worden doorgegeven Hallo id-eigenschap van het Hallo-subnet en IP-adres objecten, respectievelijk. U kunt een eenvoudige tekenreeks niet gebruiken. Deze variabelen worden ingesteld in Hallo stap toorequest een openbaar IP-adres en Hallo stap tooretrieve Hallo subnet.

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. Hallo Resource Manager virtuele netwerkgateway maken door het uitvoeren van de volgende opdracht Hallo. Hallo `-VpnType` moet *RouteBased*. Het kan duren voordat 45 minuten of langer Hallo gateway toocreate.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. Kopieer Hallo openbaar IP-adres als Hallo VPN-gateway is gemaakt. U gebruiken wanneer u Hallo LAN-instellingen voor het klassieke VNet configureert. U kunt Hallo volgende cmdlet tooretrieve Hallo openbare IP-adres gebruiken. Hallo openbaar IP-adres staat in Hallo retourneren als *IpAddress*.

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a>Deel 3: Hallo klassieke VNet lokale site-instellingen wijzigen

In deze sectie kunt u samenwerken met Hallo klassieke VNet. U vervangen Hallo tijdelijke aanduiding voor IP-adres dat u hebt gebruikt bij het opgeven van Hallo lokale site-instellingen die gebruikt tooconnect toohello Resource Manager VNet gateway worden. 

1. Hallo netwerk configuratiebestand exporteren.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. Met een teksteditor Hallo waarde wijzigen voor VPNGatewayAddress. Hallo tijdelijke aanduiding voor IP-adres met openbare IP-adres van de Resource Manager-gateway Hallo Hallo vervangen en Hallo wijzigingen op te slaan.

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. Importeren Hallo netwerk configuratie bestand tooAzure gewijzigd.

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <a name="connect"></a>Sectie 4: Maak een verbinding tussen Hallo gateways
Maken van een verbinding tussen de gateways Hallo is PowerShell vereist. U moet mogelijk tooadd uw Azure-Account toouse Hallo klassieke versie van Hallo PowerShell-cmdlets. toodo dus gebruiken **Add-AzureAccount**.

1. Stel uw gedeelde sleutel in Hallo PowerShell-console. Raadpleeg voordat u cmdlets hello, toohello netwerk-configuratiebestand dat u hebt gedownload voor Hallo exacte die Azure namen toosee verwacht. Wanneer u opgeeft Hallo-naam van een VNet dat spaties bevat, gebruik Hallo-waarde op tussen aanhalingstekens.<br><br>In het volgende voorbeeld **- VNetName** heet Hallo Hallo klassiek VNet en **- LocalNetworkSiteName** is opgegeven voor de lokale netwerksite Hallo Hallo-naam. Hallo **- SharedKey** is een waarde die u genereren en opgeven. In voorbeeld Hallo we 'abc123' gebruikt, maar u kunt genereren en gebruikmaken van iets meer complexe. Hallo belangrijke dingen die u hier opgeeft, Hallo-waarde is moet Hallo die dezelfde waarde die u in de volgende stap Hallo opgeeft wanneer u uw verbinding maakt. Hallo return moet worden weergegeven **Status: geslaagd**.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. Hallo VPN-verbinding door het uitvoeren van de volgende opdrachten Hallo maken:
   
  Hallo-variabelen worden ingesteld.

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  Hallo verbinding maken. U ziet dat Hallo **- ConnectionType** IPsec, niet Vnet2Vnet is.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a>Sectie 5: Controleer of uw verbindingen

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>tooverify hello verbinding van uw klassieke VNet tooyour Resource Manager VNet

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a>Azure Portal

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>tooverify hello verbinding van de Resource Manager VNet tooyour klassieke VNet

#### <a name="powershell"></a>PowerShell

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a>Azure Portal

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]


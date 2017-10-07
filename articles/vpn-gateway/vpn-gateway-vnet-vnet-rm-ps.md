---
title: 'Verbinding maken met een virtuele Azure-netwerk tooanother VNet: PowerShell | Microsoft Docs'
description: Dit artikel helpt u bij het met elkaar verbinden van virtuele netwerken met behulp van Azure Resource Manager en PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 2da30c76867cc3f71d040e63e0dd15d153e15c10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-powershell"></a>Een VPN-gatewayverbinding tussen VNets configureren met behulp van PowerShell

Dit artikel ziet u hoe toocreate een VPN-gatewayverbinding tussen virtuele netwerken. Hallo virtuele netwerken kunnen zich in dezelfde of verschillende regio's Hallo en Hallo van dezelfde of verschillende abonnementen behoren. Bij het maken van verbinding VNets uit verschillende abonnementen behoren, Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant. 

Hallo stappen in dit artikel toepassing toohello Resource Manager-implementatiemodel en PowerShell gebruiken. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure-CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Verbinding maken tussen verschillende implementatiemodellen - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Verbinding maken tussen verschillende implementatiemodellen - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE. Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooconsider deze met behulp van VNet-Peering te verbinden. Bij VNet-peering wordt geen VPN-gateway gebruikt. Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie.

VNet-naar-VNet-communicatie kan worden gecombineerd met configuraties voor meerdere locaties. Hiermee kunt u netwerktopologieën maken waarin cross-premises-connectiviteit met connectiviteit tussen virtuele netwerken, zoals wordt weergegeven in het volgende diagram Hallo:

![Over verbindingen](./media/vpn-gateway-vnet-vnet-rm-ps/aboutconnections.png)

### <a name="why-connect-virtual-networks"></a>Waarom virtuele netwerken koppelen?

U kunt virtuele netwerken tooconnect voor Hallo volgende redenen:

* **Geografische redundantie en aanwezigheid tussen regio's**

  * U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.
  * Met Azure Traffic Manager en Load Balancer kunt u workloads met maximale beschikbaarheid instellen met behulp van geografische redundantie over meerdere Azure-regio's. Een belangrijk voorbeeld hiervan is tooset van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.
* **Regionale toepassingen met meerdere lagen met isolatie- of beheergrenzen**

  * Hallo binnen dezelfde regio, kunt u toepassingen met meerdere lagen instellen met meerdere virtuele netwerken met elkaar verbonden vervaldatum tooisolation of beheervereisten.

Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel.

## <a name="which-set-of-steps-should-i-use"></a>Welke stappen moet ik gebruiken?

In dit artikel ziet u twee verschillende reeksen stappen. Een reeks stappen voor het [VNets die tot hetzelfde abonnement Hallo](#samesub), en een andere voor [VNets die tot verschillende abonnementen](#difsub). Hallo belangrijkste verschil tussen Hallo sets is of u kunt maken en configureren van alle virtuele netwerk en gateway bronnen binnen Hallo dezelfde PowerShell-sessie.

Hallo stappen in dit artikel variabelen gebruiken die zijn gedeclareerd op Hallo begin van elke sectie. Als u al met bestaande vnet's werkt, kunt u Hallo variabelen tooreflect Hallo instellingen in uw eigen omgeving aanpassen. Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.

## <a name="samesub"></a>Hoe tooconnect VNets die zijn opgenomen in Hallo hetzelfde abonnement

![v2v-diagram](./media/vpn-gateway-vnet-vnet-rm-ps/v2vrmps.png)

### <a name="before-you-begin"></a>Voordat u begint

Voordat u begint moet u de meest recente versie van tooinstall Hallo van hello Azure Resource Manager PowerShell-cmdlets, ten minste 4.0 of hoger. Zie voor meer informatie over het installeren van de PowerShell-cmdlets Hallo [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

### <a name="Step1"></a>Stap 1: De IP-adresbereiken plannen

In de Hallo stappen te volgen, maken we twee virtuele netwerken en hun bijbehorende gatewaysubnetten en configuraties. We vervolgens een VPN-verbinding maken tussen Hallo twee VNets. Het is belangrijk tooplan Hallo IP-adresbereiken voor uw netwerkconfiguratie. De VNet-bereiken of de bereiken van het lokale netwerk mogen elkaar niet overlappen. In deze voorbeelden behandelen we geen DNS-server. Zie [Naamomzetting](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) als u naamomzetting voor uw virtuele netwerken wilt.

We gebruiken de volgende waarden in de voorbeelden Hallo Hallo:

**Waarden voor TestVNet1:**

* VNet-naam: TestVNet1
* Resourcegroep: TestRG1
* Locatie: VS - oost
* TestVNet1: 10.11.0.0/16 en 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Openbare IP: VNet1GWIP
* VPNType: op route gebaseerd
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Waarden voor TestVNet4:**

* VNet-naam: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Resourcegroep: TestRG4
* Locatie: VS - west
* GatewayName: VNet4GW
* Openbare IP: VNet4GWIP
* VPNType: op route gebaseerd
* Verbinding: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Step2"></a>Stap 2: TestVNet1 maken en configureren

1. Declareer uw variabelen. In dit voorbeeld declareert Hallo variabelen met Hallo waarden voor deze oefening. In de meeste gevallen moet u waarden Hallo vervangen door uw eigen. U kunt deze variabelen echter gebruiken als u via Hallo stappen toobecome bekend zijn met dit type configuratie uitvoert. Wijzig variabelen Hallo indien nodig, en vervolgens Kopieer en plak ze in de PowerShell-console.

  ```powershell
  $Sub1 = "Replace_With_Your_Subcription_Name"
  $RG1 = "TestRG1"
  $Location1 = "East US"
  $VNetName1 = "TestVNet1"
  $FESubName1 = "FrontEnd"
  $BESubName1 = "Backend"
  $GWSubName1 = "GatewaySubnet"
  $VNetPrefix11 = "10.11.0.0/16"
  $VNetPrefix12 = "10.12.0.0/16"
  $FESubPrefix1 = "10.11.0.0/24"
  $BESubPrefix1 = "10.12.0.0/24"
  $GWSubPrefix1 = "10.12.255.0/27"
  $GWName1 = "VNet1GW"
  $GWIPName1 = "VNet1GWIP"
  $GWIPconfName1 = "gwipconf1"
  $Connection14 = "VNet1toVNet4"
  $Connection15 = "VNet1toVNet5"
  ```

2. Tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

  ```powershell
  Login-AzureRmAccount
  ```

  Controleer de abonnementen Hallo voor Hallo-account.

  ```powershell
  Get-AzureRmSubscription
  ```

  Hallo-abonnement dat u wilt dat toouse opgeven.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub1
  ```
3. Maak een nieuwe resourcegroep.

  ```powershell
  New-AzureRmResourceGroup -Name $RG1 -Location $Location1
  ```
4. Hallo subnetconfiguraties maken voor TestVNet1. In dit voorbeeld wordt een virtueel netwerk gemaakt met de naam TestVNet1. Er worden ook drie subnetten gemaakt, GatewaySubnet, FrontEnd en BackEnd. Wanneer u de waarden vervangt, is het belangrijk dat u de juiste namen voor de gatewaysubnets gebruikt, in het bijzonder GatewaySubnet. Als u een andere naam kiest, mislukt het maken van de gateway.

  Hallo wordt volgende voorbeeld Hallo variabelen die u eerder hebt ingesteld. In dit voorbeeld maakt Hallo gatewaysubnet gebruik van een/27. Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet met meer adressen maakt door ten minste/28 of /27 selecteren. Hierdoor kunt voldoende adressen tooaccommodate mogelijk aanvullende configuraties die u kunt Hallo toekomstige.

  ```powershell
  $fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
  $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
  $gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1
  ```
5. Maak TestVNet1.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
  ```
6. Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway u voor uw VNet maakt. U ziet dat Hallo AllocationMethod is dynamische. U kunt Hallo IP-adres dat u wilt dat toouse niet opgeven. Is dynamisch toegewezen tooyour gateway. 

  ```powershell
  $gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 `
  -Location $Location1 -AllocationMethod Dynamic
  ```
7. Hallo gatewayconfiguratie maken. Hallo-gatewayconfiguratie bepaalt Hallo subnet en Hallo openbare IP-adres toouse. Hallo voorbeeld toocreate uw gatewayconfiguratie gebruiken.

  ```powershell
  $vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
  $subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
  $gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 `
  -Subnet $subnet1 -PublicIpAddress $gwpip1
  ```
8. Hallo-gateway voor TestVNet1 maken. In deze stap maakt u de virtuele netwerkgateway Hallo voor TestVNet1. VNet-naar-VNet-configuraties vereisen een op route gebaseerd VpnType. Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van de geselecteerde Hallo-gateway SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 `
  -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-3---create-and-configure-testvnet4"></a>Stap 3: TestVNet4 maken en configureren

Wanneer u TestVNet1 hebt geconfigureerd, maakt u TestVNet4. Hallo stappen hieronder en vervang Hallo waarden door uw eigen wanneer deze nodig is. Deze stap kan worden uitgevoerd binnen Hallo dezelfde PowerShell-sessie omdat deze zich in Hallo hetzelfde abonnement.

1. Declareer uw variabelen. Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

  ```powershell
  $RG4 = "TestRG4"
  $Location4 = "West US"
  $VnetName4 = "TestVNet4"
  $FESubName4 = "FrontEnd"
  $BESubName4 = "Backend"
  $GWSubName4 = "GatewaySubnet"
  $VnetPrefix41 = "10.41.0.0/16"
  $VnetPrefix42 = "10.42.0.0/16"
  $FESubPrefix4 = "10.41.0.0/24"
  $BESubPrefix4 = "10.42.0.0/24"
  $GWSubPrefix4 = "10.42.255.0/27"
  $GWName4 = "VNet4GW"
  $GWIPName4 = "VNet4GWIP"
  $GWIPconfName4 = "gwipconf4"
  $Connection41 = "VNet4toVNet1"
  ```
2. Maak een nieuwe resourcegroep.

  ```powershell
  New-AzureRmResourceGroup -Name $RG4 -Location $Location4
  ```
3. Hallo subnetconfiguraties maken voor TestVNet4.

  ```powershell
  $fesub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName4 -AddressPrefix $FESubPrefix4
  $besub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName4 -AddressPrefix $BESubPrefix4
  $gwsub4 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName4 -AddressPrefix $GWSubPrefix4
  ```
4. Maak TestVNet4.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AddressPrefix $VnetPrefix41,$VnetPrefix42 -Subnet $fesub4,$besub4,$gwsub4
  ```
5. Vraag een openbaar IP-adres aan.

  ```powershell
  $gwpip4 = New-AzureRmPublicIpAddress -Name $GWIPName4 -ResourceGroupName $RG4 `
  -Location $Location4 -AllocationMethod Dynamic
  ```
6. Hallo gatewayconfiguratie maken.

  ```powershell
  $vnet4 = Get-AzureRmVirtualNetwork -Name $VnetName4 -ResourceGroupName $RG4
  $subnet4 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet4
  $gwipconf4 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName4 -Subnet $subnet4 -PublicIpAddress $gwpip4
  ```
7. Hallo TestVNet4-gateway maken. Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van de geselecteerde Hallo-gateway SKU.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4 `
  -Location $Location4 -IpConfigurations $gwipconf4 -GatewayType Vpn `
  -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-4---create-hello-connections"></a>Stap 4: Hallo verbindingen maken

1. Verkrijg beide gateways van het virtuele netwerk. Als beide Hallo gateways in Hallo hetzelfde abonnement behoren, zoals in het Hallo-voorbeeld, kunt u deze stap bij het Hallo voltooien dezelfde PowerShell-sessie.

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  $vnet4gw = Get-AzureRmVirtualNetworkGateway -Name $GWName4 -ResourceGroupName $RG4
  ```
2. Hallo TestVNet1 tooTestVNet4 verbinding maken. In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet4. Hier ziet u een gedeelde sleutel waarnaar wordt verwezen in Hallo voorbeelden. U kunt uw eigen waarden voor Hallo gedeelde sleutel gebruiken. Hallo belangrijk wat, is deze Hallo gedeelde sleutel moet voor beide verbindingen overeenkomen. Maken van een verbinding kan duren voordat een korte tijd toocomplete.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection14 -ResourceGroupName $RG1 `
  -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet4gw -Location $Location1 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
3. Hallo TestVNet4 tooTestVNet1 verbinding maken. Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet4 tooTestVNet1 maakt. Zorg ervoor dat Hallo gedeelde sleutels overeenkomen. Hallo verbinding zal worden gemaakt na een paar minuten.

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection41 -ResourceGroupName $RG4 `
  -VirtualNetworkGateway1 $vnet4gw -VirtualNetworkGateway2 $vnet1gw -Location $Location4 `
  -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. Controleer de verbinding. Zie de sectie Hallo [hoe tooverify uw verbinding](#verify).

## <a name="difsub"></a>Hoe tooconnect VNets die zijn opgenomen in verschillende abonnementen

![v2v-diagram](./media/vpn-gateway-vnet-vnet-rm-ps/v2vdiffsub.png)

In dit scenario worden TestVNet1 en TestVNet5 met elkaar verbonden. TestVNet1 en TestVNet5 bevinden zich in een verschillend abonnement. Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant. Hallo verschil tussen deze stappen en de vorige set Hallo is dat een aantal configuratiestappen Hallo toobe uitgevoerd in een aparte PowerShell-sessie in de context van de tweede abonnement Hallo Hallo moet. Met name wanneer twee Hallo abonnementen behoren toodifferent organisaties.

### <a name="step-5---create-and-configure-testvnet1"></a>Stap 5: TestVNet1 maken en configureren

U moet voltooien [stap 1](#Step1) en [stap 2](#Step2) van Hallo vorige sectie toocreate en TestVNet1 configureren en hello VPN-Gateway voor TestVNet1. Voor deze configuratie moet zijn u niet vereist toocreate TestVNet4 uit de vorige sectie hello, hoewel als u deze maakt, wordt dit niet conflicteert met de volgende stappen uit. Nadat u stap 1 en stap 2 hebt voltooid, kunt u doorgaan met stap 6 toocreate TestVNet5. 

### <a name="step-6---verify-hello-ip-address-ranges"></a>Stap 6: Hallo IP-adresbereiken controleren

Het is belangrijk toomake ervoor dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk, TestVNet5, niet met een van uw VNet-bereiken of de gatewaybereiken van lokale netwerk overlapt. In dit voorbeeld kunnen de virtuele netwerken Hallo toodifferent organisaties behoren. Voor deze oefening kunt u de volgende waarden voor TestVNet5 Hallo hello gebruiken:

**Waarden voor TestVNet5:**

* VNet-naam: TestVNet5
* Resourcegroep: TestRG5
* Locatie: Japan - oost
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Openbare IP: VNet5GWIP
* VPNType: op route gebaseerd
* Verbinding: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="step-7---create-and-configure-testvnet5"></a>Stap 7: TestVNet5 maken en configureren

Deze stap moet worden uitgevoerd in de context van het nieuwe abonnement Hallo Hallo. Dit onderdeel kan worden uitgevoerd door Hallo beheerder in een andere organisatie die eigenaar is van Hallo-abonnement.

1. Declareer uw variabelen. Worden ervoor tooreplace Hallo waarden Hello groepen wilt u toouse voor uw configuratie.

  ```powershell
  $Sub5 = "Replace_With_the_New_Subcription_Name"
  $RG5 = "TestRG5"
  $Location5 = "Japan East"
  $VnetName5 = "TestVNet5"
  $FESubName5 = "FrontEnd"
  $BESubName5 = "Backend"
  $GWSubName5 = "GatewaySubnet"
  $VnetPrefix51 = "10.51.0.0/16"
  $VnetPrefix52 = "10.52.0.0/16"
  $FESubPrefix5 = "10.51.0.0/24"
  $BESubPrefix5 = "10.52.0.0/24"
  $GWSubPrefix5 = "10.52.255.0/27"
  $GWName5 = "VNet5GW"
  $GWIPName5 = "VNet5GWIP"
  $GWIPconfName5 = "gwipconf5"
  $Connection51 = "VNet5toVNet1"
  ```
2. Verbinding maken met toosubscription 5. Open de PowerShell-console en tooyour-account koppelen. Gebruik Hallo volgende steekproef toohelp die u verbinding kunt maken:

  ```powershell
  Login-AzureRmAccount
  ```

  Controleer de abonnementen Hallo voor Hallo-account.

  ```powershell
  Get-AzureRmSubscription
  ```

  Hallo-abonnement dat u wilt dat toouse opgeven.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName $Sub5
  ```
3. Maak een nieuwe resourcegroep.

  ```powershell
  New-AzureRmResourceGroup -Name $RG5 -Location $Location5
  ```
4. Hallo subnetconfiguraties maken voor TestVNet5.

  ```powershell
  $fesub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName5 -AddressPrefix $FESubPrefix5
  $besub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName5 -AddressPrefix $BESubPrefix5
  $gwsub5 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName5 -AddressPrefix $GWSubPrefix5
  ```
5. Maak TestVNet5.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5 -Location $Location5 `
  -AddressPrefix $VnetPrefix51,$VnetPrefix52 -Subnet $fesub5,$besub5,$gwsub5
  ```
6. Vraag een openbaar IP-adres aan.

  ```powershell
  $gwpip5 = New-AzureRmPublicIpAddress -Name $GWIPName5 -ResourceGroupName $RG5 `
  -Location $Location5 -AllocationMethod Dynamic
  ```
7. Hallo gatewayconfiguratie maken.

  ```powershell
  $vnet5 = Get-AzureRmVirtualNetwork -Name $VnetName5 -ResourceGroupName $RG5
  $subnet5  = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet5
  $gwipconf5 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName5 -Subnet $subnet5 -PublicIpAddress $gwpip5
  ```
8. Hallo TestVNet5-gateway maken.

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5 -Location $Location5 `
  -IpConfigurations $gwipconf5 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1
  ```

### <a name="step-8---create-hello-connections"></a>Stap 8: Maak Hallo-verbindingen

In dit voorbeeld omdat Hallo gateways Hallo verschillende abonnementen behoren, wordt deze stap opgesplitst in twee PowerShell-sessies die zijn gemarkeerd als [abonnement 1] en [abonnement 5].

1. **[Abonnement 1]**  Get Hallo virtuele netwerkgateway voor abonnement 1. Meld u bij en verbinding tooSubscription 1 voordat Hallo volgende voorbeeld wordt uitgevoerd:

  ```powershell
  $vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
  ```

  Hallo-uitvoer van de volgende elementen Hallo kopiëren en verzenden van deze toohello beheerder van abonnement 5 via e-mail of een andere methode.

  ```powershell
  $vnet1gw.Name
  $vnet1gw.Id
  ```

  Deze twee elementen hebben waarden vergelijkbare toohello voorbeelduitvoer te volgen:

  ```
  PS D:\> $vnet1gw.Name
  VNet1GW
  PS D:\> $vnet1gw.Id
  /subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroupsTestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```
2. **[Abonnement 5]**  Get Hallo virtuele netwerkgateway voor abonnement 5. Meld u bij en verbinding tooSubscription 5 voordat Hallo volgende voorbeeld wordt uitgevoerd:

  ```powershell
  $vnet5gw = Get-AzureRmVirtualNetworkGateway -Name $GWName5 -ResourceGroupName $RG5
  ```

  Hallo-uitvoer van de volgende elementen Hallo kopiëren en verzenden van deze toohello beheerder van abonnement 1 via e-mail of een andere methode.

  ```powershell
  $vnet5gw.Name
  $vnet5gw.Id
  ```

  Deze twee elementen hebben waarden vergelijkbare toohello voorbeelduitvoer te volgen:

  ```
  PS C:\> $vnet5gw.Name
  VNet5GW
  PS C:\> $vnet5gw.Id
  /subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```
3. **[Abonnement 1]**  Hello TestVNet1 tooTestVNet5 verbinding maken. In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet5. Hallo verschil is hier is $vnet5gw rechtstreeks kan worden verkregen omdat deze zich in een ander abonnement. U moet toocreate een nieuw PowerShell-object met Hallo waarden gecommuniceerd vanuit abonnement 1 in bovenstaande Hallo stappen. Gebruik onderstaande Hallo-voorbeeld. Hallo naam-Id en gedeelde sleutel vervangen door uw eigen waarden. Hallo belangrijk wat, is deze Hallo gedeelde sleutel moet voor beide verbindingen overeenkomen. Maken van een verbinding kan duren voordat een korte tijd toocomplete.

  Verbind tooSubscription 1 voordat Hallo volgt uitgevoerd:

  ```powershell
  $vnet5gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet5gw.Name = "VNet5GW"
  $vnet5gw.Id   = "/subscriptions/66c8e4f1-ecd6-47ed-9de7-7e530de23994/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW"
  $Connection15 = "VNet1toVNet5"
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet5gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```
4. **[Abonnement 5]**  Hello TestVNet5 tooTestVNet1 verbinding maken. Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet5 tooTestVNet1 maakt. Hallo hetzelfde proces voor het maken van een PowerShell-object op basis van waarden van Hallo verkregen van abonnement 1 ook hier geldt. In deze stap overeenkomen moet u ervoor zorgen dat Hallo gedeelde sleutels.

  Verbind tooSubscription 5 voordat Hallo volgt uitgevoerd:

  ```powershell
  $vnet1gw = New-Object Microsoft.Azure.Commands.Network.Models.PSVirtualNetworkGateway
  $vnet1gw.Name = "VNet1GW"
  $vnet1gw.Id = "/subscriptions/b636ca99-6f88-4df4-a7c3-2f8dc4545509/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW "
  New-AzureRmVirtualNetworkGatewayConnection -Name $Connection51 -ResourceGroupName $RG5 -VirtualNetworkGateway1 $vnet5gw -VirtualNetworkGateway2 $vnet1gw -Location $Location5 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3'
  ```

## <a name="verify"></a>Hoe tooverify een verbinding

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections powershell](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen

* Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie Hallo [documentatie Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.
* Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).

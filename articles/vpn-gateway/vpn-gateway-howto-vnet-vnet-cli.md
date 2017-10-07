---
title: 'Verbinding maken met virtuele netwerk tooanother VNet: Azure CLI | Microsoft Docs'
description: Dit artikel helpt u bij het met elkaar verbinden van virtuele netwerken met behulp van Azure Resource Manager en Azure CLI.
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
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Een VPN-gatewayverbinding tussen VNets configureren met behulp van Azure CLI

Dit artikel ziet u hoe toocreate een VPN-gatewayverbinding tussen virtuele netwerken. Hallo virtuele netwerken kunnen zich in dezelfde of verschillende regio's Hallo en Hallo van dezelfde of verschillende abonnementen behoren. Bij het maken van verbinding VNets uit verschillende abonnementen behoren, Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant. 

Hallo stappen in dit artikel toepassen toohello Resource Manager-implementatiemodel en Azure CLI gebruiken. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

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

![Over verbindingen](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Waarom virtuele netwerken koppelen?

U kunt virtuele netwerken tooconnect voor Hallo volgende redenen:

* **Geografische redundantie en aanwezigheid tussen regio's**

  * U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.
  * Met Azure Traffic Manager en Load Balancer kunt u workloads met maximale beschikbaarheid instellen met behulp van geografische redundantie over meerdere Azure-regio's. Een belangrijk voorbeeld hiervan is tooset van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.
* **Regionale toepassingen met meerdere lagen met isolatie- of beheergrenzen**

  * Hallo binnen dezelfde regio, kunt u toepassingen met meerdere lagen instellen met meerdere virtuele netwerken met elkaar verbonden vervaldatum tooisolation of beheervereisten.

Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel.

### <a name="which-set-of-steps-should-i-use"></a>Welke stappen moet ik gebruiken?

In dit artikel ziet u twee verschillende reeksen stappen. Een reeks stappen voor het [VNets die tot hetzelfde abonnement Hallo](#samesub), en een andere voor [VNets die tot verschillende abonnementen](#difsub).

## <a name="samesub"></a>VNets verbinden die in Hallo hetzelfde abonnement

![v2v-diagram](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Voordat u begint

Installeer de nieuwste versie van de Hallo van Hallo CLI-opdrachten (2.0 of hoger) voordat u begint. Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli).

### <a name="Plan"></a>De IP-adresbereiken plannen

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


### <a name="Connect"></a>Stap 1: verbinding maken met tooyour abonnement

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Stap 2: TestVNet1 maken en configureren

1. Maak een resourcegroep.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. TestVNet1 en Hallo subnetten voor TestVNet1 maken. In dit voorbeeld worden een virtueel netwerk met de naam TestVNet1 en een subnet met de naam FrontEnd gemaakt.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Maak een extra adresruimte voor Hallo back-end-subnet. Merk op dat in deze stap we Geef beide Hallo-adresruimte die we eerder hebben gemaakt, en extra adresruimte willen we tooadd Hallo. Dit komt doordat Hallo [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#update) opdracht Hallo vorige instellingen overschreven. Controleer zeker toospecify alle Hallo adresvoorvoegsels bij gebruik van deze opdracht.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Hallo back-end subnet maken.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Hallo gatewaysubnet maken. U ziet dat Hallo gateway-subnet met de naam 'GatewaySubnet'. Deze naam is verplicht. In dit voorbeeld maakt Hallo gatewaysubnet gebruik van een/27. Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet met meer adressen maakt door ten minste/28 of /27 selecteren. Hierdoor kunt voldoende adressen tooaccommodate mogelijk aanvullende configuraties die u kunt Hallo toekomstige.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Aanvragen van een openbare IP-adres toobe toegewezen toohello gateway u voor uw VNet maakt. U ziet dat Hallo AllocationMethod is dynamische. U kunt Hallo IP-adres dat u wilt dat toouse niet opgeven. Is dynamisch toegewezen tooyour gateway.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. De virtuele netwerkgateway Hallo voor TestVNet1 maken. VNet-naar-VNet-configuraties vereisen een op route gebaseerd VpnType. Als u deze opdracht met Hallo '--geen - wait' parameter uitvoert, kunt u niet alle feedback of de uitvoer ziet. Hallo '--geen - wait' parameter kan Hallo gateway toocreate op Hallo achtergrond. Dit betekent niet dat Hallo VPN-gateway is onmiddellijk gemaakt. Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van Hallo gateway-SKU die u gebruikt.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>Stap 3: TestVNet4 maken en configureren

1. Maak een resourcegroep.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. Maak TestVNet4.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. Extra subnetten voor TestVNet4 maken.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Hallo gatewaysubnet maken.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Vraag een openbaar IP-adres aan.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Hallo TestVNet4 virtuele netwerkgateway maken.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>Stap 4: Hallo verbindingen maken

U hebt nu twee VNets met VPN-gateways. de volgende stap Hallo is toocreate VPN-gatewayverbindingen tussen de virtuele netwerkgateways Hallo. Als u de bovenstaande voorbeelden van Hallo gebruikt, wordt uw VNet-gateways zijn in verschillende resourcegroepen. Gateways zijn in verschillende resourcegroepen, u moet tooidentify als Hallo resource-id's voor elke gateway opgeven wanneer u een verbinding maakt. Als uw vnet's in Hallo zijn dezelfde resourcegroep bevinden, kunt u Hallo [tweede set instructies](#samerg) omdat u niet toospecify Hallo resource-id hoeft.

### <a name="diffrg"></a>tooconnect VNets die tot verschillende resourcegroepen

1. Hallo uitvoer van de volgende opdracht Hallo Hallo Resource-ID van VNet1GW verkrijgen:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Hallo zoeken in de uitvoer van Hallo ' id: ' regel. Hallo waarden binnen de aanhalingstekens Hallo zijn benodigde toocreate Hallo verbinding in de volgende sectie Hallo. Kopieer deze waarden tooa teksteditor zoals Kladblok, zodat u ze gemakkelijk plakken kunt wanneer u de verbinding maakt.

  Voorbeelduitvoer:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Kopieer de waarden Hallo na **'id':** Hallo aanhalingstekens.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Hallo Resource-ID van VNet4GW en kopieer Hallo waarden tooa teksteditor ophalen.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Hallo TestVNet1 tooTestVNet4 verbinding maken. In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet4. Er is een gedeelde sleutel waarnaar wordt verwezen in Hallo voorbeelden. U kunt uw eigen waarden voor Hallo gedeelde sleutel gebruiken. Hallo belangrijk wat, is deze Hallo gedeelde sleutel moet voor beide verbindingen overeenkomen. Maken van een verbinding nodig is een korte tijd toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Hallo TestVNet4 tooTestVNet1 verbinding maken. Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet4 tooTestVNet1 maakt. Zorg ervoor dat Hallo gedeelde sleutels overeenkomen. Het duurt enkele minuten tooestablish Hallo verbinding.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Controleer uw verbindingen. Zie [De verbinding controleren](#verify).

### <a name="samerg"></a>tooconnect VNets die tot Hallo dezelfde resourcegroep

1. Hallo TestVNet1 tooTestVNet4 verbinding maken. In deze stap maakt u Hallo verbinding van TestVNet1 tooTestVNet4. Kennisgeving Hallo resourcegroepen zijn hetzelfde in de voorbeelden Hallo Hallo. U ziet ook een gedeelde sleutel waarnaar wordt verwezen in Hallo voorbeelden. U kunt uw eigen waarden voor de gedeelde sleutel hello, echter Hallo gedeelde sleutel voor beide verbindingen moet overeenkomen. Maken van een verbinding nodig is een korte tijd toocomplete.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Hallo TestVNet4 tooTestVNet1 verbinding maken. Deze stap is vergelijkbaar toohello hierboven, alleen u Hallo verbinding nu vanuit TestVNet4 tooTestVNet1 maakt. Zorg ervoor dat Hallo gedeelde sleutels overeenkomen. Het duurt enkele minuten tooestablish Hallo verbinding.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Controleer uw verbindingen. Zie [De verbinding controleren](#verify).

## <a name="difsub"></a>VNets verbinden die tot verschillende abonnement behoren

![v2v-diagram](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

In dit scenario worden TestVNet1 en TestVNet5 met elkaar verbonden. Hallo VNets bevinden zich verschillende abonnementen behoren. Hallo abonnementen hoeft geen toobe die zijn gekoppeld aan Hallo dezelfde Active Directory-tenant. Hallo-stappen voor deze configuratie toevoegen een extra VNet-naar-VNet-verbinding in volgorde tooconnect TestVNet1 tooTestVNet5.

### <a name="TestVNet1diff"></a>Stap 5: TestVNet1 maken en configureren

Deze instructies worden overgenomen van de stappen in de voorgaande secties Hallo Hallo. U moet voltooien [stap 1](#Connect) en [stap 2](#TestVNet1) toocreate en configureer TestVNet1 en hello VPN-Gateway voor TestVNet1. Voor deze configuratie moet zijn u niet vereist toocreate TestVNet4 uit de vorige sectie hello, hoewel als u deze maakt, wordt dit niet conflicteert met de volgende stappen uit. Nadat u stap 1 en stap 2 hebt voltooid, gaat u verder met stap 6 hieronder.

### <a name="verifyranges"></a>Stap 6: Hallo IP-adresbereiken controleren

Wanneer u extra verbindingen maakt, is het belangrijk tooverify dat Hallo IP-adresruimte van Hallo nieuw virtueel netwerk niet met een van uw andere VNet-bereiken of de gatewaybereiken lokale netwerk overlapt. Voor deze oefening kunt u de volgende waarden voor TestVNet5 Hallo hello gebruiken:

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

### <a name="TestVNet5"></a>Stap 7: TestVNet5 maken en configureren

Deze stap moet worden uitgevoerd in de context Hallo van Hallo nieuw abonnement abonnement 5. Dit onderdeel kan worden uitgevoerd door Hallo beheerder in een andere organisatie die eigenaar is van Hallo-abonnement. tooswitch tussen abonnementen gebruik ' lijst az--alle ' toolist Hallo abonnementen beschikbaar tooyour account en gebruik vervolgens ' az account set--abonnement <subscriptionID>' tooswitch toohello abonnement dat u wilt dat toouse.

1. Zorg ervoor dat u bent verbonden tooSubscription 5 en vervolgens een resourcegroep maken.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. Maak TestVNet5.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Voeg subnetten toe.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Hallo gatewaysubnet toevoegen.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Vraag een openbaar IP-adres aan.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Hallo TestVNet5-gateway maken

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>Stap 8: Maak Hallo-verbindingen

We deze stap in twee CLI sessies, aangeduid als splitsen **[abonnement 1]**, en **[abonnement 5]** omdat Hallo gateways Hallo verschillende abonnementen behoren. tooswitch tussen abonnementen gebruik ' lijst az--alle ' toolist Hallo abonnementen beschikbaar tooyour account en gebruik vervolgens ' az account set--abonnement <subscriptionID>' tooswitch toohello abonnement dat u wilt dat toouse.

1. **[Abonnement 1]**  Aanmelden en verbinding maken met tooSubscription 1. Voer Hallo volgende opdracht tooget Hallo naam en de ID van Hallo Gateway vanuit Hallo uitvoer:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Kopieer de uitvoer Hallo voor ' id: '. Hallo-ID en naam van Hallo VNet gateway (VNet1GW) toohello beheerder van abonnement 5 via e-mail of een andere methode Hallo verzenden.

  Voorbeelduitvoer:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[Abonnement 5]**  Aanmelden en verbinding maken met tooSubscription 5. Voer Hallo volgende opdracht tooget Hallo naam en de ID van Hallo Gateway vanuit Hallo uitvoer:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Kopieer de uitvoer Hallo voor ' id: '. Hallo-ID en naam van Hallo VNet gateway (VNet5GW) toohello beheerder van abonnement 1 via e-mail of een andere methode Hallo verzenden.

3. **[Abonnement 1]**  In deze stap maakt u Hallo verbinding kunt maken van tooTestVNet5 TestVNet1. U kunt uw eigen waarden voor de gedeelde sleutel hello, echter Hallo gedeelde sleutel voor beide verbindingen moet overeenkomen. Maken van een verbinding kan duren voordat een korte tijd toocomplete. Zorg ervoor dat u verbinding maakt met tooSubscription 1.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[Abonnement 5]**  Deze stap is vergelijkbaar toohello hierboven, behalve dat u maakt Hallo verbinding nu vanuit TestVNet5 tooTestVNet1. Zorg ervoor dat Hallo gedeelde sleutels overeenkomen en of u verbinding tooSubscription 5 maken.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Hallo-verbindingen controleren
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen

* Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie voor meer informatie, Hallo [documentatie Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).

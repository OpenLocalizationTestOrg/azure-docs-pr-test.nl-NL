---
title: 'Verbinding maken met uw lokale netwerk tooan virtuele Azure-netwerk: Site-naar-Site VPN: CLI | Microsoft Docs'
description: Stappen toocreate een IPsec-verbinding van uw on-premises netwerk tooan virtuele Azure-netwerk via openbaar Internet Hallo. Deze stappen helpen u een cross-premises site-naar-site-VPN-gatewayverbinding te maken met CLI.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>Een virtueel netwerk maken met een site-naar-site-VPN-verbinding met CLI

Dit artikel laat zien hoe toouse hello Azure CLI toocreate een Site-naar-Site VPN-gatewayverbinding vanuit uw lokale netwerk toohello VNet. Hallo stappen in dit artikel van toepassing toohello Resource Manager-implementatiemodel. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:<br>

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Diagram: cross-premises site-naar-site-VPN-gatewayverbinding](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Een Site-naar-Site VPN-gatewayverbinding gebruikte tooconnect is uw on-premises netwerk tooan virtuele Azure-netwerk via een VPN-IPsec/IKE (IKEv1 of IKEv2)-tunnel. Dit type verbinding vereist een VPN-zich on-premises apparaten met een extern gericht openbaar IP-adres toegewezen tooit. Zie [Overzicht van VPN Gateway](vpn-gateway-about-vpngateways.md) voor meer informatie over VPN-gateways.

## <a name="before-you-begin"></a>Voordat u begint

Controleer of dat u criteria na voorhand Hallo hebt voldaan:

* Zorg ervoor dat u hebt een compatibel VPN-apparaat en iemand die dit kunnen tooconfigure deze. Zie [Over VPN-apparaten](vpn-gateway-about-vpn-devices.md) voor meer informatie over compatibele VPN-apparaten en -apparaatconfiguratie.
* Controleer of u een extern gericht openbaar IPv4-adres voor het VPN-apparaat hebt. Dit IP-adres kan zich niet achter een NAT bevinden.
* Als u niet bekend bent met de Hallo IP-adresbereiken zich in uw on-premises netwerkconfiguratie, moet u toocoordinate met iemand die deze details voor u verstrekken kan. Wanneer u deze configuratie maakt, moet u Hallo IP-bereik adresvoorvoegsels Azure routeert tooyour on-premises locatie. Geen van de subnetten Hallo van uw on-premises netwerk kunnen via lap met Hallo virtueel netwerksubnetten die u wilt dat tooconnect om te.
* Controleer of dat u de meest recente versie van Hallo CLI-opdrachten (2.0 of hoger) hebt geïnstalleerd. Zie voor meer informatie over het installeren van de CLI-opdrachten Hallo [2.0 voor Azure CLI installeren](/cli/azure/install-azure-cli) en [aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Voorbeeldwaarden

Gebruik Hallo waarden toocreate een testomgeving te volgen of toothese waarden verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Verbinding maken met tooyour abonnement

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Een resourcegroep maken

Hallo wordt volgende voorbeeld een resourcegroep met de naam 'TestRG1' op Hallo 'eastus' locatie. Als u al een resourcegroep in Hallo regio die u toocreate uw VNet wilt hebt, kunt u dat een in plaats daarvan.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Een virtueel netwerk maken

Als u nog een virtueel netwerk hebt, maakt u een met Hallo [az network vnet maken](/cli/azure/network/vnet#create) opdracht. Wanneer u een virtueel netwerk maakt, zorg dat Hallo-adresruimten die u opgeeft niet overlappen met adresruimten Hallo die u op uw on-premises netwerk hebt.

Hallo wordt volgende voorbeeld een virtueel netwerk met de naam 'TestVNet1' en een subnet, 'Subnet1'.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Hallo gatewaysubnet maken

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Voor deze configuratie hebt u ook een gatewaysubnet nodig. Hallo virtuele netwerkgateway maakt gebruik van een gatewaysubnet dat Hallo IP-adressen die worden gebruikt door Hallo VPN-gatewayservices bevat. Wanneer u een gatewaysubnet maakt, moet dit de naam GatewaySubnet krijgen. Als u een andere naam kiest, maakt u wel een subnet, maar wordt dit door Azure niet als een gatewaysubnet behandeld.

Hallo grootte van gatewaysubnet Hallo die u opgeeft, afhankelijk Hallo VPN-gateway-configuratie die u toocreate wilt. Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet die meer adressen maakt door het selecteren van/27 of /28 bevat. Met behulp van een groter gatewaysubnet kunt voldoende IP-adressen tooaccommodate mogelijke toekomstige configuraties.

Gebruik Hallo [az network vnet subnet maken](/cli/azure/network/vnet/subnet#create) opdracht toocreate hello gatewaysubnet.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Hallo lokale netwerkgateway maken

Hallo lokale netwerkgateway verwijst doorgaans tooyour on-premises locatie. U geeft Hallo site een naam waarmee Azure kunt tooit verwijzen, geeft u vervolgens Hallo IP-adres van Hallo lokale VPN-apparaat toowhich maakt u een verbinding. U wordt ook Hallo IP-adresvoorvoegsels worden doorgestuurd via Hallo VPN-gateway toohello VPN-apparaat. Hallo-adresvoorvoegsels die u opgeeft voorvoegsels Hallo zich op uw on-premises netwerk. Als uw on-premises netwerk verandert, kunt u Hallo voorvoegsels eenvoudig bijwerken.

Hallo volgende waarden gebruiken:

* Hallo *--gateway-ip-adres* Hallo IP-adres van uw on-premises VPN-apparaat. Het VPN-apparaat kan zich niet achter een NAT bevinden.
* Hallo *--lokale adresvoorvoegsels* uw on-premises adresruimten zijn.

Gebruik Hallo [az local-netwerkgateway maken](/cli/azure/network/local-gateway#create) opdracht tooadd een lokale netwerkgateway met meerdere adresvoorvoegsels:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Een openbaar IP-adres aanvragen

Een VPN Gateway moet een openbaar IP-adres hebben. U eerst aanvragen Hallo IP-adres resource en vervolgens tooit verwijzen bij het maken van uw virtuele netwerkgateway. Hallo IP-adres dynamisch toegewezen toohello resource wanneer Hallo VPN-gateway is gemaakt. VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen. U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen. Dit betekent echter niet dat dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen. de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt. Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.

Gebruik Hallo [az netwerk openbare ip-maken](/cli/azure/network/public-ip#create) opdracht toorequest een dynamische openbare IP-adres.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Hallo VPN-gateway maken

VPN-gateway van Hallo virtueel netwerk maken. Maken van een VPN-gateway kan duren too45 minuten of meer toocomplete.

Hallo volgende waarden gebruiken:

* Hallo *--type gateway* voor een Site-naar-Site configuratie is *Vpn*. Hallo-Gatewaytype is altijd specifiek toohello configuratie die u implementeert. Zie [Soorten gateways](vpn-gateway-about-vpn-gateway-settings.md#gwtype) voor meer informatie.
* Hallo *--vpn-type* kan *RouteBased* (bedoeld tooas een dynamische Gateway in sommige documentatie), of *PolicyBased* (tooas een statische Gateway in sommige genoemd documentatie). Hallo-instelling is specifiek toorequirements van Hallo-apparaat dat u verbinding maakt. Zie [Informatie over VPN-gatewayconfiguratie-instellingen](vpn-gateway-about-vpn-gateway-settings.md#vpntype) voor meer informatie over soorten VPN-gateways.
* Selecteer Hallo dat u wilt dat toouse Gateway-SKU. Voor bepaalde SKU's gelden configuratiebeperkingen. Zie [Gateway-SKU's](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor meer informatie.

Hallo VPN-gateway met Hallo maken [az vnet-netwerkgateway maken](/cli/azure/network/vnet-gateway#create) opdracht. Als u deze opdracht met Hallo '--geen - wait' parameter uitvoert, kunt u niet alle feedback of de uitvoer ziet. Deze parameter kan Hallo gateway toocreate op Hallo achtergrond. Het duurt ongeveer 45 minuten toocreate een gateway.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. Uw VPN-apparaat configureren

Site-naar-Site-verbindingen tooan on-premises netwerk een VPN-apparaat vereist. In deze stap configureert u het VPN-apparaat. Bij het configureren van uw VPN-apparaat, moet u de volgende Hallo:

- Een gedeelde sleutel. Dit is Hallo dezelfde gedeelde sleutel die u opgeeft bij het maken van uw Site-naar-Site VPN-verbinding. In onze voorbeelden gebruiken we een eenvoudige gedeelde sleutel. Het is raadzaam dat u een complexere sleutel toouse genereert.
- Hallo openbare IP-adres van uw virtuele netwerkgateway. U kunt het openbare IP-adres Hallo weergeven met behulp van hello Azure-portal, PowerShell of CLI. toofind hello openbare IP-adres van uw virtuele netwerkgateway, gebruik Hallo [az netwerk openbare ip-lijst](/cli/azure/network/public-ip#list) opdracht. Hallo-uitvoer is gemakkelijk te lezen, opgemaakte toodisplay Hallo lijst met openbare IP-adressen in tabelindeling.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Hallo VPN-verbinding maken

Hallo Site-naar-Site VPN-verbinding tussen uw virtuele netwerkgateway en uw on-premises VPN-apparaat maken. Betalen bijzondere aandacht toohello gedeeld sleutelwaarde, die moet overeenkomen met de Hallo geconfigureerd gedeeld sleutelwaarde voor uw VPN-apparaat.

Hallo verbinding maken met de Hallo [az netwerk vpn-verbinding maken](/cli/azure/network/vpn-connection#create) opdracht.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Na een korte tijd hello wordt de verbinding worden gemaakt.

## <a name="toverify"></a>10. Hallo VPN-verbinding controleren

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Als u een andere methode tooverify toouse wilt uw verbinding, Zie [een VPN-Gateway-verbinding controleren](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>tooconnect tooa virtuele machine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Algemene taken

Deze sectie bevat veelgebruikte opdrachten die nuttig zijn bij het werken met site-naar-siteconfiguraties. Zie voor Hallo volledige lijst met netwerken CLI-opdrachten, [Azure CLI - netwerken](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Volgende stappen

* Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie.
* Zie voor meer informatie over BGP Hallo [BGP-overzicht](vpn-gateway-bgp-overview.md) en [hoe tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Zie [Informatie over geforceerde tunneling](vpn-gateway-forced-tunneling-rm.md) voor meer informatie over geforceerde tunneling.
* Zie [Maximaal beschikbare cross-premises en VNet-naar-VNet-connectiviteit](vpn-gateway-highlyavailable.md) voor meer informatie over maximaal beschikbare actieve verbindingen.
* Zie [Azure CLI](https://docs.microsoft.com/cli/azure/network) voor een lijst met Azure CLI-opdrachten voor netwerken.
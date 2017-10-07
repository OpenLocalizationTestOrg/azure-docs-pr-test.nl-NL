---
title: 'Verbinding maken met de klassieke virtuele netwerken tooAzure Resource Manager VNets: Portal | Microsoft Docs'
description: Meer informatie over hoe een VPN-verbinding tussen het klassieke vnet's en Resource Manager-VNets met VPN-Gateway en Hallo portal toocreate
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a>Verbinding maken met virtuele netwerken vanuit verschillende implementatiemodellen met Hallo-portal

Dit artikel laat zien hoe tooconnect klassieke vnet's tooResource Manager VNets tooallow Hallo bronnen in Hallo afzonderlijke implementatie modellen toocommunicate met elkaar. Hallo stappen in dit artikel gebruiken voornamelijk hello Azure-portal, maar u kunt ook maken met deze configuratie met behulp van PowerShell Hallo door Hallo artikel in deze lijst te selecteren.

> [!div class="op_single_selector"]
> * [Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

Verbinding maken met een klassiek VNet tooa Resource Manager VNet is vergelijkbaar tooconnecting een VNet tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE. U kunt een verbinding tussen VNets die tot verschillende abonnementen behoren en in verschillende regio's maken. U kunt ook VNets die u al verbindingen tooon-premises netwerken hebt, verbinden, zolang het Hallo-gateway die is geconfigureerd met dynamische of op basis van route is. Zie voor meer informatie over VNet-naar-VNet-verbindingen Hallo [Veelgestelde vragen over VNet-naar-VNet](#faq) aan Hallo einde van dit artikel. 

Als uw vnet's in Hallo zijn dezelfde regio, kunt u tooinstead overwegen deze met behulp van VNet-Peering te verbinden. Bij VNet-peering wordt geen VPN-gateway gebruikt. Zie het artikel [VNet-peering](../virtual-network/virtual-network-peering-overview.md) voor meer informatie. 

### <a name="prerequisites"></a>Vereisten

* Deze stappen wordt ervan uitgegaan dat beide VNets al zijn gemaakt. Als u van dit artikel wijze van oefening maakt gebruikmaakt en geen VNets hebt, zijn er koppelingen in Hallo stappen toohelp u ze maken.
* Controleer of Hallo-adresbereiken voor Hallo die vnets met elkaar niet overlappen, of heeft overlap met een van de Hallo bereiken voor andere verbindingen die Hallo gateways mogen worden verbonden met.
* Hallo nieuwste PowerShell-cmdlets voor Resource Manager en Service Management (klassiek) installeren. In dit artikel gebruiken we zowel hello Azure-portal en PowerShell. PowerShell is vereist toocreate Hallo verbinding van Hallo klassieke VNet toohello Resource Manager VNet. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). 

### <a name="values"></a>Voorbeeldinstellingen

U kunt deze waarden toocreate een testomgeving gebruiken of toothem verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel.

**Klassieke VNet**

VNet-naam = ClassicVNet <br>
Adresruimte = 10.0.0.0/24 <br>
Subnet-1 = 10.0.0.0/27 <br>
Resourcegroep ClassicRG = <br>
Locatie VS-West = <br>
GatewaySubnet 10.0.0.32/28 = <br>
Lokale site RMVNetLocal = <br>

**Resource Manager VNet**

VNet-naam = RMVNet <br>
Adresruimte = 192.168.0.0/16 <br>
Subnet-1 = 192.168.1.0/24 <br>
GatewaySubnet 192.168.0.0/26 = <br>
Resourcegroep RG1 = <br>
Locatie VS-Oost = <br>
Naam van virtuele-netwerkgateway RMGateway = <br>
Gatewaytype = VPN <br>
VPN-type = op Route gebaseerd <br>
Naam van gateway openbare IP-adres rmgwpip = <br>
Lokale netwerkgateway ClassicVNetLocal = <br>
Verbindingsnaam RMtoClassic =

### <a name="connection-overview"></a>Overzicht van de verbinding

Voor deze configuratie kunt u een VPN-gatewayverbinding maken via een VPN-IPsec/IKE-tunnel tussen Hallo virtuele netwerken. Zorg ervoor dat geen van uw VNet-bereiken overlappen elkaar of met lokale netwerken Hallo waarmee ze verbinding maken.

Hallo toont volgende tabel een voorbeeld van hoe Hallo voorbeeld VNets en lokale sites worden gedefinieerd:

| Virtual Network | Adresruimte | Regio | Maakt verbinding toolocal netwerksite op. |
|:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |VS - west | RMVNetLocal (192.168.0.0/16) |
| RMVNet | (192.168.0.0/16) |VS - oost |ClassicVNetLocal (10.0.0.0/24) |

## <a name="classicvnet"></a>1. Hallo-classic VNet-instellingen configureren

In deze sectie maakt u Hallo lokale netwerk (lokale site) en de virtuele netwerkgateway Hallo voor het klassieke VNet. Als u niet een klassiek VNet hebt en deze stappen als oefening maakt uitvoert, kunt u een VNet maken met behulp van [in dit artikel](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) en Hallo [voorbeeld](#values) waarden voor de instellingen van hierboven.

Wanneer u Hallo portal toocreate een klassiek virtueel netwerk, moet u de blade virtueel netwerk toohello navigeren met behulp van Hallo volgende stappen uit, anders Hallo optie toocreate een klassiek virtueel netwerk niet wordt weergegeven:

1. Klik op Hallo '+' tooopen Hallo 'New' blade.
2. Typ in veld 'Marketplace zoeken Hallo' Hallo 'Virtueel netwerk'. Als u in plaats daarvan selecteert netwerk -> virtueel netwerk, ontvangt u geen Hallo optie toocreate een klassiek VNet.
3. Zoek 'Virtueel netwerk' van Hallo lijst geretourneerd en klik op de blade van tooopen Hallo virtueel netwerk. 
4. Selecteer op de blade virtueel netwerk hello, 'Klassiek' toocreate een klassiek VNet. 

Als u al een VNet met een VPN-gateway, Controleer of deze gateway Hallo dynamische. Als het statisch, moet u eerst Hallo VPN-gateway verwijderen en vervolgens doorgaan.

De schermafbeeldingen dienen alleen als voorbeeld. Ervoor tooreplace Hallo waarden door uw eigen, of gebruik Hallo [voorbeeld](#values) waarden.

### <a name="part-1---configure-hello-local-site"></a>Deel 1: de lokale site Hallo configureren

Open Hallo [Azure-portal](https://ms.portal.azure.com) en meld u aan met uw Azure-account.

1. Navigeer te**alle resources** en zoek Hallo **ClassicVNet** in Hallo-lijst.
2. Op Hallo **overzicht** blade in Hallo **VPN-verbindingen** sectie, klikt u op Hallo **Gateway** grafische toocreate een gateway.

    ![Een VPN-gateway configureren](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "een VPN-gateway configureren")
3. Op Hallo **nieuwe VPN-verbinding** blade voor **verbindingstype**, selecteer **Site-naar-site**.
4. Voor **lokale site**, klikt u op **vereiste instellingen configureren**. Hiermee opent u Hallo **lokale site** blade.
5. Op Hallo **lokale site** blade een naam toorefer toohello Resource Manager VNet maken. Bijvoorbeeld 'RMVNetLocal'.
6. Als Hallo VPN-gateway voor Hallo Resource Manager VNet is al een openbaar IP-adres, gebruik Hallo waarde Hallo **IP-adres van VPN-gateway** veld. Als u deze stappen uitvoert als oefening of een virtuele netwerkgateway voor uw Resource Manager VNet nog geen hebt, kunt u een tijdelijke aanduiding voor IP-adres. Zorg ervoor dat gebruikmaakt van een geldige indeling Hallo tijdelijke aanduiding voor IP-adres. Later, vervangt u Hallo tijdelijke aanduiding voor IP-adres door Hallo openbare IP-adres van de virtuele netwerkgateway van Hallo Resource Manager.
7. Voor **Client adresruimte**, Hallo waarden gebruiken voor Hallo virtueel netwerk-IP-adresruimten voor Hallo Resource Manager VNet. Deze instelling is gebruikte toospecify Hallo adres spaties tooroute toohello Resource Manager virtueel netwerk.
8. Klik op **OK** toosave Hallo waarden en retourneren toohello **nieuwe VPN-verbinding** blade.

### <a name="part-2---create-hello-virtual-network-gateway"></a>Deel 2: Hallo virtuele netwerkgateway maken

1. Op Hallo **nieuwe VPN-verbinding** blade, selecteer Hallo **gateway onmiddellijk maken** selectievakje en klikt u op **optionele gatewayconfiguratie** tooopen hello  **Gatewayconfiguratie** blade. 

    ![Open gateway configuratie blade](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Open gateway-configuratie-blade")
2. Klik op **Subnet - vereiste instellingen configureren** tooopen hello **subnet toevoegen** blade. Hallo **naam** al is geconfigureerd met een waarde vereist Hallo **GatewaySubnet**.
3. Hallo **-adresbereik** toohello bereik voor het gatewaysubnet Hallo verwijst. Hoewel u een gatewaysubnet met een/29 maken kunt-adresbereik (3-adressen), wordt aangeraden een gatewaysubnet maken die meer IP-adressen bevat. Dit geschikt is voor toekomstige configuraties waarvoor meer beschikbare IP-adressen. Gebruik indien mogelijk, / 27 of /28. Als u van deze stappen wijze van oefening maakt gebruikmaakt, kunt u verwijzen toohello [voorbeeld](#values) waarden. Klik op **OK** toocreate hello gatewaysubnet.
4. Op Hallo **gatewayconfiguratie** blade **grootte** toohello gateway-SKU verwijst. Selecteer Hallo gateway-SKU voor uw VPN-gateway.
5. Controleer of Hallo **Type routering** is **dynamische**, klikt u vervolgens op **OK** tooreturn toohello **nieuwe VPN-verbinding** blade.
6. Op Hallo **nieuwe VPN-verbinding** blade, klikt u op **OK** toobegin maken van uw VPN-gateway. Maken van een VPN-gateway kan duren too45 minuten toocomplete.

### <a name="ip"></a>Deel 3 - kopie Hallo virtuele netwerkgateway openbare IP-adres

Nadat de virtuele netwerkgateway Hallo is gemaakt, kunt u IP-adres van Hallo gateway kunt weergeven. 

1. Navigeer tooyour klassieke VNet en klik op **overzicht**.
2. Klik op **VPN-verbindingen** tooopen Hallo VPN-verbindingen blade. U kunt op Hallo VPN-verbindingen blade Hallo openbare IP-adres weergeven. Dit is Hallo openbare IP-adres toegewezen tooyour virtuele netwerkgateway. 
3. Noteer of kopieer Hallo IP-adres. U gebruikt in latere stappen wanneer u met uw configuratie-instellingen van Resource Manager LAN gateway werkt. U kunt ook Hallo status van uw gatewayverbindingen weergeven. Kennisgeving Hallo lokale netwerksite die u hebt gemaakt, wordt vermeld als 'Verbinding maken'. Hallo-status gewijzigd nadat u uw verbindingen hebt gemaakt.
4. Hallo-blade sluiten na het kopiëren van IP-adres van Hallo gateway.

## <a name="rmvnet"></a>2. Hallo Resource Manager VNet-instellingen configureren

In deze sectie maakt u de virtuele netwerkgateway Hallo en Hallo lokale netwerkgateway voor uw Resource Manager VNet. Als u een Resource Manager VNet niet hebt en deze stappen als oefening maakt uitvoert, kunt u een VNet maken met behulp van [in dit artikel](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) en Hallo [voorbeeld](#values) waarden voor de instellingen van hierboven.

De schermafbeeldingen dienen alleen als voorbeeld. Ervoor tooreplace Hallo waarden door uw eigen, of gebruik Hallo [voorbeeld](#values) waarden.

### <a name="part-1---create-a-gateway-subnet"></a>Deel 1: een gatewaysubnet maken

Voordat u een virtuele netwerkgateway maakt, moet u eerst toocreate hello gatewaysubnet. Een gatewaysubnet met CIDR-telling van/28 of groter maken. (/ 27, / 26, enz.)

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a>Deel 2: een virtuele netwerkgateway maken

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <a name="createlng"></a>Deel 3: een lokale netwerkgateway maken

de lokale netwerkgateway Hallo specificeert Hallo-adresbereik en Hallo openbare IP-adres die zijn gekoppeld aan uw klassieke VNet en de virtuele netwerkgateway.

Als u deze stappen als oefening uitvoert, raadpleegt u toothese instellingen:

| Virtual Network | Adresruimte | Regio | Maakt verbinding toolocal netwerksite op. |Gateway openbare IP-adres|
|:--- |:--- |:--- |:--- |:--- |
| ClassicVNet |(10.0.0.0/24) |VS - west | RMVNetLocal (192.168.0.0/16) |Hallo openbare IP-adres dat is toegewezen toohello ClassicVNet gateway|
| RMVNet | (192.168.0.0/16) |VS - oost |ClassicVNetLocal (10.0.0.0/24) |Hallo openbare IP-adres dat is toegewezen toohello RMVNet gateway.|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <a name="modifylng"></a>3. Hallo klassieke VNet lokale site-instellingen wijzigen

In deze sectie maakt vervangen u Hallo tijdelijke aanduiding voor IP-adres dat u gebruikt bij het opgeven van instellingen van de lokale site hello, hello IP-adres voor Resource Manager-VPN-gateway. Deze sectie wordt Hallo klassieke (SM) PowerShell-cmdlets gebruikt.

1. Navigeer in hello Azure-portal, toohello klassiek virtueel netwerk.
2. Klik op de blade voor het virtuele netwerk Hallo **overzicht**.
3. In Hallo **VPN-verbindingen** sectie, klikt u op Hallo-naam van uw lokale site in Hallo-afbeelding.

    ![VPN-verbindingen](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN-verbindingen")
4. Op Hallo **Site-naar-site VPN-verbindingen** blade, klikt u op de naam Hallo van Hallo-site.

    ![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "lokale sitenaam")
5. Klik op Hallo verbinding blade voor uw lokale site op de naam Hallo Hallo lokale site tooopen Hallo **lokale site** blade.

    ![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "lokale site openen")
6. Op Hallo **lokale site** blade, vervangen Hallo **IP-adres van VPN-gateway** met Resource Manager-gateway Hallo Hallo IP-adres.

    ![Gateway-ip-adres](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Gateway IP-adres")
7. Klik op **OK** tooupdate Hallo IP-adres.

## <a name="RMtoclassic"></a>4. Resource Manager tooclassic verbinding maken

In deze stap, configureert u Hallo verbinding van Resource Manager VNet Hallo toohello klassieke VNet met behulp van hello Azure-portal.

1. In **alle resources**, de lokale netwerkgateway Hallo vinden. In ons voorbeeld Hallo lokale netwerkgateway is **ClassicVNetLocal**.
2. Klik op **configuratie** en controleert u of Hallo IP-adreswaarde Hallo VPN-gateway voor Hallo klassieke VNet. Indien nodig bijwerken en klik vervolgens op **opslaan**. Blade sluiten Hallo.
3. In **alle resources**, klikt u op de lokale netwerkgateway Hallo.
4. Klik op **verbindingen** tooopen Hallo verbindingen blade.
5. Op Hallo **verbindingen** blade, klikt u op  **+**  tooadd een verbinding.
6. Op Hallo **verbinding toevoegen** blade, naam Hallo verbinding. Bijvoorbeeld 'RMtoClassic'.
7. **Site-naar-Site** is al geselecteerd voor deze blade.
8. Selecteer de virtuele netwerkgateway Hallo dat u wilt dat tooassociate met deze site.
9. Maak een **gedeelde sleutel**. Deze sleutel wordt ook gebruikt in Hallo-verbinding die u van Hallo klassieke VNet toohello Resource Manager VNet maken. U kunt Hallo sleutel genereren of er een bedenken. In ons voorbeeld gebruiken we 'abc123', maar u kunt (en moeten) gebruikmaken van iets meer complexe.
10. Klik op **OK** toocreate Hallo verbinding.

##<a name="classictoRM"></a>5. Klassieke tooResource Manager verbinding maken

In deze stap configureert u Hallo verbinding van Hallo klassieke VNet toohello Resource Manager VNet. Deze stappen moet PowerShell. U kunt deze verbinding kan maken in Hallo-portal. Zorg ervoor dat u hebt gedownload en geïnstalleerd zowel klassieke hello (SM) en Resource Manager (RM) PowerShell-cmdlets.

### <a name="1-connect-tooyour-azure-account"></a>1. Verbinding maken met tooyour Azure-account

Open Hallo PowerShell-console met verhoogde rechten en meld u tooyour Azure-account. Hallo vraagt volgende cmdlet u om Hallo aanmeldingsreferenties voor uw Azure-Account. Na het aanmelden, worden de instellingen van uw account zodat ze beschikbaar tooAzure PowerShell zijn gedownload.

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

Voeg uw Azure-Account toouse Hallo klassieke PowerShell-cmdlets (SM). toodo geval is, kunt u Hallo volgende opdracht:

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a>2. Hallo netwerk configuratiewaarden bestand weergeven

Wanneer u een VNet in hello Azure-portal maakt, is volledige naam Hallo die gebruikmaakt van Azure niet zichtbaar in hello Azure-portal. Een VNet dat wordt weergegeven met de naam 'ClassicVNet' in hello Azure-portal toobe kan bijvoorbeeld een veel langer naam hebben in het configuratiebestand Hallo-netwerk. Hallo naam kan als volgt uitzien: 'Groep ClassicRG ClassicVNet'. In deze stappen stelt downloaden u Hallo bestands- en Hallo configuratiewaarden netwerk.

Maak een map op uw computer en vervolgens exporteren Hallo configuration file toohello netwerkmap. In dit voorbeeld is Hallo netwerk configuratiebestand geëxporteerde tooC:\AzureNet.

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

Hallo-bestand met een editor en bekijkt hello naam in voor uw klassieke VNet openen. Hallo-namen in Hallo netwerk configuratiebestand gebruiken bij het uitvoeren van PowerShell-cmdlets.

- VNet-namen worden vermeld als **VirtualNetworkSite name =**
- De namen van sites worden vermeld als **LocalNetworkSite name =**

### <a name="3-create-hello-connection"></a>3. Hallo verbinding maken

Hallo gedeelde sleutel instellen en maak Hallo verbinding van Hallo klassieke VNet toohello Resource Manager VNet. U kunt Hallo gedeelde sleutel met behulp van de portal Hallo niet instellen. Zorg ervoor dat u deze stappen terwijl u bent aangemeld met behulp van de klassieke versie Hallo Hallo PowerShell-cmdlets uitvoeren. toodo dus gebruiken **Add-AzureAccount**. Anders worden niet kunnen tooset Hallo '-AzureVNetGatewayKey'.

- In dit voorbeeld **- VNetName** Hallo naam Hallo klassieke VNet als gevonden in het configuratiebestand van uw netwerk. 
- Hallo **- LocalNetworkSiteName** Hallo-naam die u hebt opgegeven voor de lokale site hello, als is gevonden in het configuratiebestand van uw netwerk.
- Hallo **- SharedKey** is een waarde die u genereren en opgeven. In dit voorbeeld hebben we gebruikt *abc123*, maar u kunt iets ingewikkelders genereren. Hallo belangrijke dingen die u hier opgeeft, Hallo-waarde is moet Hallo die dezelfde waarde dat u hebt opgegeven bij het maken van uw tooclassic Resource Manager-verbinding.

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<a name="verify"></a>6. Controleer uw verbindingen

U kunt controleren of dat uw verbindingen met behulp van hello Azure-portal of PowerShell. Bij het verifiëren, moet u mogelijk toowait duurt ongeveer twee minuten zoals Hallo verbinding wordt gemaakt. Wanneer een verbinding geslaagd is, status van de connectiviteit Hallo gewijzigd van 'Verbinding maken' too'Connected'.

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a>tooverify hello verbinding van uw klassieke VNet tooyour Resource Manager VNet

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a>tooverify hello verbinding van de Resource Manager VNet tooyour klassieke VNet

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="faq"></a>Veelgestelde vragen over VNet-naar-VNet

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

---
title: 'Maak een verbinding tussen VNets: klassieke: Azure portal | Microsoft Docs'
description: Hoe tooconnect Azure virtuele netwerken samen met behulp van PowerShell en Hallo klassieke Azure-portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a>Een VNet-naar-VNet-verbinding (klassiek) configureren

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Dit artikel ziet u hoe toocreate een VPN-gatewayverbinding tussen virtuele netwerken. Hallo virtuele netwerken kunnen zich in dezelfde of verschillende regio's Hallo en Hallo van dezelfde of verschillende abonnementen behoren. Hallo stappen in dit artikel van toepassing toohello klassieke implementatiemodel en hello Azure-portal. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure-CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Verbinding maken tussen verschillende implementatiemodellen - Azure Portal](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Verbinding maken tussen verschillende implementatiemodellen - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![VNet tooVNet connectiviteit-Diagram](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a>Over VNet-naar-VNet-verbindingen

Verbinding maken met een virtueel netwerk tooanother virtueel netwerk (VNet-naar-VNet) in het klassieke implementatiemodel Hallo met behulp van een VPN-gateway is vergelijkbaar tooconnecting een virtueel netwerk tooan on-premises-locatie. Beide connectiviteitstypen wordt een VPN-gateway tooprovide een beveiligde tunnel met IPsec/IKE.

Hallo VNets die u verbindt, kan zich in verschillende abonnementen en verschillende regio's. U kunt VNet tooVNet-communicatie met multi-site-configuraties combineren. Zo kunt u netwerktopologieën maken waarin cross-premises connectiviteit is gecombineerd met connectiviteit tussen virtuele netwerken.

![VNet tooVNet verbindingen](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <a name="why"></a>Waarom virtuele netwerken koppelen?

U kunt virtuele netwerken tooconnect voor Hallo volgende redenen:

* **Geografische redundantie en aanwezigheid tussen regio's**

  * U kunt uw eigen geo-replicatie of synchronisatie met beveiligde connectiviteit instellen zonder gebruik te maken van internetgerichte eindpunten.
  * Met Azure Load Balancer en Microsoft of derden clustertechnologie, kunt u maximaal beschikbare werkbelasting met geografische redundantie over meerdere Azure-regio's instellen. Een belangrijk voorbeeld hiervan is tooset van SQL Always On met beschikbaarheidsgroepen verspreid over meerdere Azure-regio's.
* **Regionale toepassingen met meerdere lagen met sterke isolatiegrens**

  * Hallo binnen dezelfde regio, kunt u toepassingen met meerdere lagen instellen met meerdere VNets die zijn verbonden met sterke isolatie en veilige communicatie met tussen lagen.
* **Cross-abonnement, de communicatie tussen organisatie in Azure**

  * Als u meerdere Azure-abonnementen hebt, kunt u werkbelastingen van verschillende abonnementen samen veilig tussen virtuele netwerken.
  * U kunt cross-organisatie communicatie met de beveiligde VPN-technologie binnen Azure inschakelen voor ondernemingen of serviceproviders.

Zie voor meer informatie over VNet-naar-VNet-verbindingen [VNet-naar-VNet-overwegingen](#faq) aan Hallo einde van dit artikel.

### <a name="before-you-begin"></a>Voordat u begint

Voordat u deze oefening begint, download en installeer de nieuwste versie Hallo van hello Azure Service Management (SM) PowerShell-cmdlets. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview). We Hallo portal gebruiken voor de meeste Hallo stappen, maar u moet PowerShell toocreate Hallo verbindingen tussen VNets hello gebruiken. U kunt geen Hallo verbindingen met hello Azure-portal maken.

## <a name="plan"></a>Stap 1: De IP-adresbereiken plannen

Het is belangrijk toodecide Hallo bereiken die u tooconfigure uw virtuele netwerken gebruiken wilt. Voor deze configuratie moet u ervoor zorgen dat geen van uw VNet-bereiken overlappen elkaar of met lokale netwerken Hallo waarmee ze verbinding maken.

Hallo volgende tabel ziet u een voorbeeld van hoe toodefine uw vnet's. Hallo bereiken als uitgangspunt alleen gebruiken. Schrijf Hallo bereiken voor uw virtuele netwerken. Deze informatie moet u voor de volgende stappen.

**Voorbeeld**

| Virtual Network | Adresruimte | Regio | Maakt verbinding toolocal netwerksite op. |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |VS - oost |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |VS - west |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

## <a name="vnetvalues"></a>Stap 2: Hallo virtuele netwerken maken

Twee virtuele netwerken maken in Hallo [Azure-portal](https://portal.azure.com). Zie voor Hallo toocreate klassieke virtuele netwerken stappen, [een klassiek virtueel netwerk maken](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). 

Wanneer u Hallo portal toocreate een klassiek virtueel netwerk, moet u de blade virtueel netwerk toohello navigeren met behulp van Hallo volgende stappen uit, anders Hallo optie toocreate een klassiek virtueel netwerk niet wordt weergegeven:

1. Klik op Hallo '+' tooopen Hallo 'New' blade.
2. Typ in veld 'Marketplace zoeken Hallo' Hallo 'Virtueel netwerk'. Als u in plaats daarvan selecteert netwerk -> virtueel netwerk, ontvangt u geen Hallo optie toocreate een klassiek VNet.
3. Zoek 'Virtueel netwerk' van Hallo lijst geretourneerd en klik op de blade van tooopen Hallo virtueel netwerk. 
4. Selecteer op de blade virtueel netwerk hello, 'Klassiek' toocreate een klassiek VNet. 

Als u van dit artikel wijze van oefening maakt gebruikmaakt, kunt u Hallo voorbeeldwaarden te volgen:

**Waarden voor TestVNet1**

Naam: TestVNet1<br>
Adresruimte: 10.11.0.0/16, 10.12.0.0/16 (optioneel)<br>
Subnetnaam: standaard<br>
Subnet-adresbereik: 10.11.0.1/24<br>
Resourcegroep: ClassicRG<br>
Locatie: VS - oost<br>
GatewaySubnet: 10.11.1.0/27

**Waarden voor TestVNet4**

Naam: TestVNet4<br>
Adresruimte: 10.41.0.0/16, 10.42.0.0/16 (optioneel)<br>
Subnetnaam: standaard<br>
Subnet-adresbereik: 10.41.0.1/24<br>
Resourcegroep: ClassicRG<br>
Locatie: VS - west<br>
GatewaySubnet: 10.41.1.0/27

**Houd er rekening mee Hallo instellingen na bij het maken van uw vnet's:**

* **Adresruimten voor virtueel netwerk** – op de pagina adresruimten voor virtueel netwerk Hallo Hallo-adresbereik dat u toouse voor het virtuele netwerk wilt opgeven. Dit zijn het dynamische IP-adressen hello, die wordt toegewezen toohello VM's en andere rolinstanties die u toothis virtueel netwerk implementeert.<br>Hallo adres spaties die u selecteert niet overlappen met adresruimten Hallo voor elk van Hallo andere vnet's of on-premises locaties waarmee dit VNet verbinding te maken.

* **Locatie** – wanneer u een virtueel netwerk, maakt u deze koppelen aan een Azure-locatie (regio). Bijvoorbeeld, als u wilt dat uw virtuele machines die zijn geïmplementeerd tooyour virtueel netwerk toobe fysiek bevinden in VS-West, selecteert u die locatie. U kunt Hallo locatie die is gekoppeld aan het virtuele netwerk nadat u deze hebt gemaakt niet wijzigen.

**Na het maken van uw vnet's, kunt u instellingen na Hallo toevoegen:**

* **Adresruimte** – extra adresruimte is niet vereist voor deze configuratie, maar u kunt extra adresruimte toevoegen na het maken van Hallo VNet.

* **Subnetten** – extra subnetten zijn niet vereist voor deze configuratie, maar u kunt toohave uw virtuele machines in een subnet dat is gescheiden van uw andere rolinstanties.

* **DNS-servers** – Hallo DNS-servernaam en IP-adres invoeren. Met deze instelling wordt geen DNS-server gemaakt. Hiermee kunt u toospecify Hallo DNS-servers wilt u toouse voor naamomzetting voor dit virtuele netwerk.

In deze sectie verbindingstype hello, de lokale site hello, configureren en Hallo-gateway maken.

## <a name="localsite"></a>Stap 3: de lokale site Hallo configureren

Maakt gebruik van Azure Hallo opgegeven instellingen in elke site lokale netwerk toodetermine hoe tooroute verkeer tussen Hallo VNets. Elke VNet moet toohello respectieve lokale netwerk die u wilt dat tooroute verkeer naar verwijzen. U bepalen Hallo-naam die u toouse toorefer tooeach lokale netwerksite wilt. Het is aanbevolen toouse iets beschrijvende.

Bijvoorbeeld, verbindt TestVNet1 tooa lokale netwerksite die u maakt met de naam 'VNet4Local'. Hallo-instellingen voor VNet4Local bevatten Hallo adresvoorvoegsels voor TestVNet4.

Hallo lokale site voor elk VNet is Hallo andere VNet. Hallo volgen voorbeelden van waarden worden gebruikt voor de configuratie:

| Virtual Network | Adresruimte | Regio | Maakt verbinding toolocal netwerksite op. |
|:--- |:--- |:--- |:--- |
| TestVNet1 |TestVNet1<br>(10.11.0.0/16)<br>(10.12.0.0/16) |VS - oost |VNet4Local<br>(10.41.0.0/16)<br>(10.42.0.0/16) |
| TestVNet4 |TestVNet4<br>(10.41.0.0/16)<br>(10.42.0.0/16) |VS - west |VNet1Local<br>(10.11.0.0/16)<br>(10.12.0.0/16) |

1. TestVNet1 niet vinden in hello Azure-portal. In Hallo **VPN-verbindingen** sectie van de blade hello, klikt u op **Gateway**.

    ![Er is geen gateway](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. Op Hallo **nieuwe VPN-verbinding** pagina **Site-naar-Site**.
3. Klik op **lokale site** tooopen Hallo pagina van de lokale site en Hallo-instellingen configureren.
4. Op Hallo **lokale site** pagina en de naam van uw lokale site. In ons voorbeeld namen wij aan de lokale site Hallo 'VNet4Local'.
5. Voor **IP-adres van VPN-gateway**, kunt u een IP-adres dat u wilt, zolang het is een ongeldige indeling. Normaal gesproken gebruikt u Hallo werkelijke externe IP-adres voor een VPN-apparaat. Maar voor een klassiek VNet-naar-VNet-configuratie, gebruikt u het openbare IP-adres hello, die toohello gateway voor uw VNet is toegewezen. Gezien het feit dat u de virtuele netwerkgateway Hallo nog niet hebt gemaakt, kunt u een geldig openbaar IP-adres opgeven als een tijdelijke aanduiding.<br>Niet leeg laten - is niet optioneel is voor deze configuratie. In een latere stap, gaat u terug naar deze instellingen en met Hallo bijbehorende virtueel netwerk gateway IP-adressen configureren, wanneer dit Azure genereert.
6. Voor **Client adresruimte**, adresruimte Hallo Hallo andere VNet gebruiken. Raadpleeg tooyour voorbeeld plannen. Klik op **OK** toosave uw instellingen en return back toohello **nieuwe VPN-verbinding** blade.

    ![lokale site](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <a name="gw"></a>Stap 4: Hallo virtuele netwerkgateway maken

Elke virtuele netwerk moet een virtuele netwerkgateway hebben. de virtuele netwerkgateway Hallo van routes en versleutelt verkeer.

1. Op Hallo **nieuwe VPN-verbinding** blade, selecteer Hallo selectievakje **gateway onmiddellijk maken**.
2. Klik op **Subnet, grootte en routeringstype**. Op Hallo **gatewayconfiguratie** blade, klikt u op **Subnet**.
3. Hallo gateway subnetnaam wordt automatisch ingevuld met de vereiste Hallo-naam 'GatewaySubnet'. Hallo **-adresbereik** Hallo IP-adressen die zijn toegewezen toohello VPN-gatewayservices bevat. Bepaalde configuraties een gatewaysubnet van slechts/29, maar de beste toouse toestaan een/28 of /27 tooaccommodate toekomstige configuraties waarvoor meer IP-adressen voor Hallo gatewayservices. In ons voorbeeldinstellingen gebruiken we 10.11.1.0/27. Hallo-adresruimte aanpassen en klik vervolgens op **OK**.
4. Hallo configureren **Gateway grootte**. Deze instelling verwijst toohello [Gateway-SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku).
5. Hallo configureren **Type routering**. Hallo routeringstype voor deze configuratie moet **dynamische**. U kunt de routering type hello later niet wijzigen tenzij u Hallo gateway verwijderen en maak een nieuwe.
6. Klik op **OK**.
7. Op Hallo **nieuwe VPN-verbinding** blade, klikt u op **OK** toobegin Hallo virtuele netwerkgateway maken. Maken van een gateway kunt vaak 45 minuten of langer duren, afhankelijk van de geselecteerde Hallo-gateway SKU.

## <a name="vnet4settings"></a>Stap 5: TestVNet4-instellingen configureren

Herhaal de stappen van de Hallo te[maken van een lokale site](#localsite) en [Hallo virtuele netwerkgateway aanmaken](#gw) tooconfigure TestVNet4, vervangen door waarden Hallo indien nodig. Als u dit wijze van oefening maakt doet, gebruikt u Hallo [voorbeeldwaarden](#vnetvalues).

## <a name="updatelocal"></a>Stap 6: Update Hallo lokale sites

Nadat de virtuele netwerkgateways voor beide vnet's zijn gemaakt, moet u lokale sites Hallo aanpassen **IP-adres van VPN-gateway** waarden.

|VNet-naam|Verbonden site|IP-gatewayadres|
|:--- |:--- |:--- |
|TestVNet1|VNet4Local|IP-adres van VPN-gateway voor TestVNet4|
|TestVNet4|VNet1Local|IP-adres van VPN-gateway voor TestVNet1|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a>Deel 1 - Get Hallo virtueel netwerk gateway openbaar IP-adres

1. Het virtuele netwerk niet vinden in hello Azure-portal.
2. Klik op tooopen hello VNet **overzicht** blade. Op de blade Hallo in **VPN-verbindingen**, kunt u Hallo IP-adres voor uw virtuele netwerkgateway weergeven.

  ![Openbare IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. Kopieer Hallo IP-adres. U gebruikt deze in de volgende sectie Hallo.
4. Herhaal deze stappen voor TestVNet4

### <a name="part-2---modify-hello-local-sites"></a>Deel 2 - Hallo lokale sites wijzigen

1. Het virtuele netwerk niet vinden in hello Azure-portal.
2. Op Hallo VNet **overzicht** blade, klikt u op de lokale site Hallo.

  ![Lokale site gemaakt](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. Op Hallo **Site-naar-Site VPN-verbindingen** blade, klikt u op Hallo-naam van de lokale site Hallo dat u wilt dat toomodify.

  ![Open lokale site](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. Klik op Hallo **lokale site** dat u wilt dat toomodify.

  ![de site aanpassen](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. Update Hallo **IP-adres van VPN-gateway** en klik op **OK** toosave Hallo instellingen.

  ![gateway-IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. Hallo sluit andere blades.
7. Herhaal deze stappen voor TestVNet4.

## <a name="getvalues"></a>Stap 7 - waarden ophalen uit het configuratiebestand Hallo-netwerk

Wanneer u de klassieke vnet's in hello Azure-portal maakt, wordt Hallo-naam die u wilt bekijken is niet Hallo volledige naam die u voor PowerShell gebruikt. Bijvoorbeeld, een VNet dat wordt weergegeven met de naam toobe **TestVNet1** in Hallo-portal een veel langer naam kunnen hebben in het configuratiebestand Hallo-netwerk. Hallo naam kan als volgt uitzien: **groep ClassicRG TestVNet1**. Wanneer u uw verbindingen maakt, is het belangrijk toouse Hallo waarden die u in het configuratiebestand Hallo-netwerk ziet.

In Hallo stappen te volgen, maakt u verbinding tooyour Azure-account en downloaden en weergave Hallo network configuration file tooobtain Hallo waarden die zijn vereist voor uw verbindingen.

1. Download en installeer de nieuwste versie Hallo van hello Azure Service Management (SM) PowerShell-cmdlets. Zie voor meer informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

2. Open de PowerShell-console met verhoogde rechten en tooyour-account koppelen. Gebruik Hallo voorbeeld toohelp die u verbinding maakt te volgen:

  ```powershell
  Login-AzureRmAccount
  ```

  Controleer de abonnementen Hallo voor Hallo-account.

  ```powershell
  Get-AzureRmSubscription
  ```

  Als u meer dan één abonnement hebt, selecteert u Hallo-abonnement dat u wilt dat toouse.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  Gebruik vervolgens Hallo cmdlet tooadd na uw Azure-abonnement tooPowerShell Hallo klassieke implementatiemodel.

  ```powershell
  Add-AzureAccount
  ```
3. Exporteren en Hallo netwerk configuratiebestand weergeven. Maak een map op uw computer en vervolgens exporteren Hallo configuration file toohello netwerkmap. In dit voorbeeld Hallo netwerk configuratiebestand te geëxporteerd**C:\AzureNet**.

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. Hallo-bestand openen met een tekst-editor en bekijkt hello namen voor uw vnet's en sites. Deze worden Hallo-naam die u gebruikt bij het maken van uw verbindingen.<br>VNet-namen worden vermeld als **VirtualNetworkSite name =**<br>De namen van sites worden vermeld als **LocalNetworkSiteRef name =**

## <a name="createconnections"></a>Stap 8: Maak Hallo VPN-gateway-verbindingen

Wanneer alle Hallo voorgaande stappen hebt voltooid, kunt u Hallo IPsec/IKE vooraf gedeelde sleutels en Hallo verbinding maken. Deze reeks stappen maakt gebruik van PowerShell. VNet-naar-VNet-verbindingen voor het klassieke implementatiemodel Hallo kunnen niet worden geconfigureerd in hello Azure-portal.

In de voorbeelden Hallo, wordt u ziet dat de gedeelde sleutel Hallo exact dezelfde Hallo. Hallo gedeelde sleutel moet altijd overeenkomen. Niet zeker tooreplace Hallo-waarden in deze voorbeelden met Hallo exacte namen voor uw vnet's en lokale netwerksites.

1. Hallo TestVNet1 tooTestVNet4 verbinding maken.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. Hallo TestVNet4 tooTestVNet1 verbinding maken.

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. Wachten op Hallo verbindingen tooinitialize. Zodra het Hallo-gateway is geïnitialiseerd, is Hallo Status 'Geslaagd'.

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <a name="faq"></a>VNet-naar-VNet-overwegingen voor klassieke vnet 's
* Hallo virtuele netwerken kunnen zich in Hallo dezelfde of verschillende abonnementen behoren.
* Hallo virtuele netwerken kunnen zich in Hallo dezelfde of verschillende Azure-regio's (locaties).
* Een cloudservice of een taakverdelingseindpunt kan geen virtuele netwerken overbruggen, zelfs niet als ze met elkaar zijn verbonden.
* Meerdere virtuele netwerken aan elkaar koppelen, is het niet nodig een VPN-apparaten.
* VNet-naar-VNet ondersteunt verbinding virtuele Azure-netwerken. Deze biedt geen ondersteuning voor verbinden van virtuele machines of cloudservices die niet zijn geïmplementeerd tooa virtueel netwerk.
* VNet-naar-VNet vereist dynamische routeringsgateways. Azure statische routeringsgateways worden niet ondersteund.
* U kunt virtuele-netwerkverbindingen tegelijk gebruiken met multi-site-VPN’s. Er is een maximum van 10 VPN-tunnels voor een virtueel netwerk VPN-gateway tooeither verbinding maken met andere virtuele netwerken of lokale sites.
* Hallo-adresruimten van Hallo virtuele netwerken en on-premises lokale netwerksites mogen elkaar niet overlappen. Overlappende adresruimten zal Hallo maken van virtuele netwerken of uploaden netcfg configuratie bestanden toofail.
* Redundante tunnels tussen een paar virtuele netwerken worden niet ondersteund.
* Alle VPN-tunnels voor Hallo VNet, met inbegrip van P2S-VPN-verbindingen, delen Hallo beschikbare bandbreedte voor Hallo VPN-gateway en dezelfde SLA voor VPN-gateway bedrijfstijd in Azure Hallo.
* VNet-naar-VNet-verkeer via hello Azure-backbone wordt verzonden.

## <a name="next-steps"></a>Volgende stappen
Controleer uw verbindingen. Zie [een VPN-Gateway-verbinding controleren](vpn-gateway-verify-connection-resource-manager.md).

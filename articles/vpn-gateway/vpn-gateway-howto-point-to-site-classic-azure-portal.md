---
title: 'Verbinding maken met een computer-tooa virtueel netwerk met punt-naar-Site en verificatie via certificaat: de klassieke Azure Portal | Microsoft Docs'
description: Veilig verbinding tooyour klassieke Azure Virtual Network door het maken van een punt-naar-Site VPN-gatewayverbinding met hello Azure-portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 65e14579-86cf-4d29-a6ac-547ccbd743bd
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 9b53ba43ee4dfb61defeec458905fb1f1b18c3a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-classic-azure-portal"></a>Een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat (klassiek): Azure-portal

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

Dit artikel laat zien hoe een VNet met een punt-naar-Site-verbinding bij het gebruik van Hallo classic deployment model toocreate hello Azure-portal. Deze configuratie maakt gebruik van certificaten tooauthenticate Hallo client verbinding te maken. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>

Een punt-naar-Site (P2S) VPN-gateway kunt u een beveiligde verbinding tooyour virtueel netwerk maken van een afzonderlijke clientcomputer. Punt-naar-Site VPN-verbindingen zijn handig als u wilt dat tooconnect tooyour VNet vanaf een externe locatie, zoals wanneer u vanaf thuis of een conferentie zijn teleforenzen. Een P2S-VPN is ook een uitstekende oplossing toouse in plaats van een Site-naar-Site VPN-wanneer u slechts enkele clients hebt die tooconnect tooa VNet nodig hebt. 

Maakt gebruik van P2S Hallo SSTP Secure Socket Tunneling Protocol (), die een VPN op basis van een SSL-protocol. Een P2S-VPN-verbinding tot stand is gebracht vanaf Hallo-clientcomputer.


![Punt-naar-site-diagram](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/point-to-site-connection-diagram.png)


Punt-naar-Site certificaat verificatie verbindingen vereisen Hallo volgende:

* Een dynamische VPN-gateway.
* Hallo openbare sleutel (.cer-bestand) voor een basiscertificaat dat geüpload tooAzure is. Dit wordt beschouwd als een vertrouwd certificaat en wordt gebruikt voor verificatie.
* Een clientcertificaat gegenereerd op basis van het basiscertificaat Hallo en geïnstalleerd op elke clientcomputer waarmee verbinding wordt gemaakt. Dit certificaat wordt gebruikt voor clientverificatie.
* Op elke clientcomputer die wordt verbonden, moet bovendien een VPN-clientconfiguratiepakket worden gegenereerd en geïnstalleerd. Hallo-clientpakket configuratie configureert het systeemeigen VPN-client hello, die zich al op Hallo-besturingssysteem met Hallo benodigde informatie tooconnect toohello VNet.

Punt-naar-site-verbindingen hebben geen VPN-apparaat of on-premises openbaar IP-adres nodig. Hallo VPN-verbinding wordt gemaakt via SSTP (Secure Socket Tunneling Protocol). Aan de serverzijde hello ondersteunen wij SSTP versies 1.0, 1.1 en 1.2. Hallo-client bepaalt welke versie toouse. Voor Windows 8.1 en hoger, gebruikt SSTP standaard 1.2. 

Zie voor meer informatie over punt-naar-Site-verbindingen Hallo [punt-naar-Site Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.

### <a name="example-settings"></a>Voorbeeldinstellingen

Gebruik Hallo waarden toocreate een testomgeving te volgen of toothese waarden verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel:

* **Naam: VNet1**
* **Adresruimte: 192.168.0.0/16**<br>In dit voorbeeld gebruiken we slechts één adresruimte. U kunt meer dan één adresruimte voor uw VNet hebben.
* **Subnetnaam: FrontEnd**
* **Subnetadresbereik: 192.168.1.0/24**
* **Abonnement:** als u meer dan één abonnement hebt, Controleer of u de juiste Hallo.
* **Resourcegroep: TestRG**
* **Locatie: VS - oost**
* **Verbindingstype: punt-naar-site-verbinding**
* **Clientadresruimte: 172.16.201.0/24**. VPN-clients die verbinding maken met toohello VNet deze punt-naar-Site-verbinding met een IP-adres van ontvangen Hallo opgegeven groep.
* **GatewaySubnet: 192.168.200.0/24**. Hallo gatewaysubnet moet Hallo-naam 'GatewaySubnet' gebruiken.
* **Grootte:** Selecteer Hallo gateway-SKU die u toouse wilt.
* **Routeringstype: dynamisch**

## <a name="vnetvpn"></a>1. Een virtueel netwerk en een VPN-gateway maken

Controleer eerst of u een Azure-abonnement hebt. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial).

### <a name="createvnet"></a>Deel 1: Een virtueel netwerk maken

Als u nog geen virtueel netwerk hebt, maakt u er een. De schermafbeeldingen dienen alleen als voorbeeld. Ervoor tooreplace Hallo waarden door uw eigen worden. een VNet met behulp van toocreate hello Azure-portal, gebruik Hallo stappen te volgen:

1. Navigeer via een browser toohello [Azure-portal](http://portal.azure.com) en, indien nodig, meld u aan met uw Azure-account.
2. Klik op **Nieuw**. In Hallo **zoeken Hallo marketplace** veld, typt u 'Virtueel netwerk'. Zoek **virtueel netwerk** Hallo geretourneerde lijst en klik op tooopen hello **virtueel netwerk** pagina.

  ![Pagina voor zoeken van virtueel netwerk](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvnetportal700.png)
3. Aan de onderkant Hallo van Hallo virtueel netwerk pagina van Hallo **een implementatiemodel selecteren** Selecteer **klassieke**, en klik vervolgens op **maken**.

  ![Een implementatiemodel selecteren](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/selectmodel.png)
4. Op Hallo **virtueel netwerk maken** pagina, Hallo VNet-instellingen configureren. Voeg op deze pagina de eerste adresruimte en één adresbereik voor het subnet toe. Nadat u Hallo VNet maken, kunt u teruggaan en aanvullende subnets en adresruimten toevoegen.

  ![De pagina Virtueel netwerk maken](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/vnet125.png)
5. Controleer of deze Hallo **abonnement** Hallo correct is. U kunt abonnementen wijzigen met behulp van Hallo vervolgkeuzelijst.
6. Klik op **Resourcegroep** en selecteer een bestaande resourcegroep of maak een nieuwe aan door een naam in te voeren voor uw nieuwe resourcegroep. Als u een nieuwe resourcegroep maken wilt, de naam resourcegroep voor Hallo tooyour volgens geplande configuratiewaarden. Zie [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md#resource-groups) (Overzicht van Azure Resource Manager) voor meer informatie over resourcegroepen.
7. Selecteer vervolgens Hallo **locatie** instellingen voor uw VNet. Hallo locatie bepaalt waar Hallo-resources die u toothis VNet implementeert blijven staan.
8. Selecteer **pincode toodashboard** als u kunnen toofind toobe uw VNet gemakkelijk op Hallo dashboard wilt en klik vervolgens op **maken**.

  ![Pincode toodashboard](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/pintodashboard150.png)
9. Nadat u op maken klikt, verschijnt een tegel op uw dashboard die nieuwe Hallo voortgang van uw VNet. Hallo tegel wijzigingen als Hallo VNet wordt gemaakt.

  ![Tegel Virtueel netwerk maken](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deploying150.png)
10. Nadat het virtuele netwerk is gemaakt, ziet u **gemaakt** vermeld onder **Status** op Hallo netwerken pagina in Hallo klassieke Azure-portal.
11. Voeg een DNS-server toe (optioneel). Nadat u het virtuele netwerk hebt gemaakt, kunt u Hallo IP-adres van een DNS-server voor naamomzetting kunt toevoegen. Hallo DNS-server IP-adres dat u opgeeft moet Hallo-adres van een DNS-server die Hallo namen voor Hallo resources in uw VNet kan omzetten.<br>tooadd een DNS-server, Hallo-instellingen voor het virtuele netwerk openen, klikt u op de DNS-servers en Hallo IP-adres van Hallo DNS-server die u toouse wilt toevoegen.

### <a name="gateway"></a>Deel 2: Een gatewaysubnet en een gateway voor dynamische routering maken

In deze stap maakt u een gatewaysubnet en een gateway voor dynamische routering. In Azure-portal voor het klassieke implementatiemodel Hallo Hallo, maken van het gatewaysubnet Hallo en Hallo-gateway kan worden uitgevoerd via Hallo dezelfde configuratiepagina's.

1. Navigeer in Hallo portal toohello virtueel netwerk waarvoor u een gateway toocreate wilt.
2. Op de pagina voor het virtuele netwerk, klikt u op Hallo Hallo **overzicht** pagina in de sectie voor Hallo VPN-verbindingen, klikt u op **Gateway**.

  ![Klik op een gateway toocreate](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/beforegw125.png)
3. Op Hallo **nieuwe VPN-verbinding** pagina **punt-naar-site**.

  ![Verbindingstype punt-naar-site](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/newvpnconnect.png)
4. Voor **Client adresruimte**, Hallo IP-adresbereik toevoegen. Dit is Hallo bereik waarvan Hallo VPN-clients een IP-adres ontvangen wanneer verbinding wordt gemaakt. Gebruik een persoonlijk IP-adresbereik dat niet overlapt met Hallo on-premises locatie die u in of Hello VNet dat u wilt dat tooconnect aan. U kunt Hallo automatisch gevulde bereik verwijderen en vervolgens Hallo persoonlijk IP-adresbereik dat u toouse wilt toevoegen.

  ![Clientadresruimte](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientaddress.png)
5. Selecteer Hallo **gateway onmiddellijk maken** selectievakje.

  ![Gateway onmiddellijk maken](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/creategwimm.png)
6. Klik op **optionele gatewayconfiguratie** tooopen hello **gatewayconfiguratie** pagina.

  ![Klik op Optionele gatewayconfiguratie](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/optsubnet125.png)
7. Klik op **Subnet configureren vereiste instellingen** tooadd hello **gatewaysubnet**. Het is mogelijk toocreate een gatewaysubnet van slechts/29, wordt u aangeraden dat u een groter subnet met meer adressen maakt door ten minste/28 of /27 selecteren. Hierdoor kunt voldoende adressen tooaccommodate mogelijk aanvullende configuraties die u kunt Hallo toekomstige. Als u werkt met de gateway-subnetten, te voorkomen dat een security group (NSG) toohello gateway netwerksubnet koppelen. Koppelen van een netwerksubnet beveiliging groep toothis kan ertoe leiden dat uw VPN-gateway toostop werkt zoals verwacht.

  ![GatewaySubnet toevoegen](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsubnet125.png)
8. Selecteer Hallo gateway **grootte**. Hallo-grootte is Hallo gateway-SKU voor uw virtuele netwerkgateway. In de portal Hallo Hallo standaard SKU is **Basic**. Zie [Informatie over VPN-gatewayinstellingen](vpn-gateway-about-vpn-gateway-settings.md#gwsku) voor informatie over gateway-SKU's.

  ![Grootte van de gateway](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/gwsize125.png)
9. Selecteer Hallo **Type routering** voor uw gateway. P2S-configuraties vereisen een **Dynamisch** routeringstype. Klik op **OK** wanneer u klaar bent met het configureren van deze pagina.

  ![Routeringstype configureren](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/routingtype125.png)
10. Op Hallo **nieuwe VPN-verbinding** pagina, klikt u op **OK** onderaan Hallo Hallo pagina toobegin maken van uw virtuele netwerkgateway. Een VPN-gateway kan duren voordat too45 minuten toocomplete, afhankelijk van Hallo gateway-sku die u selecteert.

## <a name="generatecerts"></a>2. Certificaten maken

Certificaten worden gebruikt door Azure tooauthenticate VPN-clients voor punt-naar-Site VPN-verbindingen. U uploaden Hallo informatie over openbare sleutels van Hallo root certificate tooAzure. Hallo openbare sleutel vervolgens beschouwd als 'vertrouwd'. Clientcertificaten moeten worden gegenereerd op basis van het vertrouwde basiscertificaat Hallo en geïnstalleerd op elke clientcomputer in Hallo certificaten-huidige gebruiker/persoonlijk certificaatarchief. Hallo-certificaat is gebruikte tooauthenticate Hallo client wanneer een verbinding toohello VNet wordt gemaakt. 

Als u zelfondertekende certificaten gebruikt, moeten ze worden gemaakt met behulp van specifieke parameters. U kunt een zelfondertekend certificaat met behulp van instructies voor het Hallo maken [PowerShell en Windows 10](vpn-gateway-certificates-point-to-site.md), of [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Het is belangrijk Hallo stappen in deze instructies te volgen bij het werken met zelfondertekende basiscertificaten en genereren van clientcertificaten van Hallo zelfondertekende basiscertificaat. Anders Hallo certificaten die u maakt is niet compatibel met P2S-verbindingen en ontvangt u een verbindingsfout opgetreden.

### <a name="cer"></a>Deel 1: Hallo openbare sleutel (.cer) voor het basiscertificaat Hallo verkrijgen

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="genclientcert"></a>Deel 2: Een clientcertificaat genereren

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>3. Hallo hoofdmap cer-bestand uploaden

Nadat het Hallo-gateway is gemaakt, kunt u Hallo cer-bestand (met daarin de openbare sleutelinformatie Hallo) voor een vertrouwd basiscertificaat certificaat tooAzure uploaden. U uploaden Hallo persoonlijke sleutel voor Hallo root certificate tooAzure niet. Zodra a.cer bestand is geüpload, Azure kan worden gebruikt tooauthenticate-clients die een clientcertificaat dat is gegenereerd op basis van het vertrouwde basiscertificaat Hallo hebt geïnstalleerd. U kunt extra vertrouwde basis-certificaatbestanden - up tooa totaal van 20 - later uploaden, indien nodig.  

1. Op Hallo **VPN-verbindingen** sectie Hallo-pagina voor uw VNet, klikt u op Hallo **clients** grafische tooopen hello **punt-naar-site VPN verbinding** pagina.

  ![Clients](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Op Hallo **punt-naar-site-verbinding** pagina, klikt u op **certificaten beheren** tooopen hello **certificaten** pagina.<br>

  ![De pagina Certificaten](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Op Hallo **certificaten** pagina, klikt u op **uploaden** tooopen hello **certificaat uploaden** pagina.<br>

    ![De pagina Certificaat uploaden](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/uploadcerts.png)<br>
4. Klik op Hallo map grafische toobrowse voor Hallo cer-bestand. Hallo-bestand selecteren en klik vervolgens op **OK**. Vernieuwen Hallo pagina toosee Hallo geüpload certificaat op Hallo **certificaten** pagina.

  ![Certificaat uploaden](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/upload.png)<br>

## <a name="vpnclientconfig"></a>4. Hallo-client configureren

tooconnect tooa VNet met een punt-naar-Site VPN, moet elke client een pakket tooconfigure Hallo systeemeigen Windows VPN-client installeren. Hallo-configuratiepakket configureert Hallo systeemeigen Windows VPN-client met Hallo instellingen nodig tooconnect toohello virtueel netwerk.

Kunt u dezelfde configuratie van VPN-client van het pakket op elke clientcomputer hello, zolang het Hallo-versie komt overeen met de Hallo-architectuur voor Hallo-client. Voor de lijst van de Hallo van client-besturingssystemen die worden ondersteund, Zie Hallo [punt-naar-Site-verbindingen Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.

### <a name="generateconfigpackage"></a>Deel 1: Genereren en Hallo VPN-clientpakket configuratie installeren

1. In de Azure-portal, op Hallo Hallo **overzicht** pagina voor uw VNet in **VPN-verbindingen**, klikt u op Hallo van Hallo client grafische tooopen **punt-naar-site VPN verbinding** pagina.
2. Hallo boven aan het Hallo **punt-naar-site VPN verbinding** pagina, klikt u op Hallo-downloadpakket dat overeenkomt met toohello clientbesturingssysteem waarop het wordt geïnstalleerd:

  * Selecteer voor 64-bits clients **VPN-clients (64-bits)**.
  * Selecteer voor 32-bits clients **VPN-clients (32-bits)**.

  ![Het configuratiepakket voor de VPN-client downloaden](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/dlclient.png)<br>
3. Zodra het Hallo verpakt genereert, downloaden en installeren op de clientcomputer. Als u een SmartScreen-melding ziet, klikt u op **Meer info** en vervolgens op **Toch uitvoeren**. U kunt ook Hallo pakket tooinstall opslaan op andere clientcomputers.

### <a name="installclientcert"></a>Deel 2: Installeer Hallo clientcertificaat

Als u wilt een P2S toocreate verbinding vanaf een clientcomputer dan Hallo u toogenerate Hallo clientcertificaten gebruikt, moet u een clientcertificaat tooinstall. Als u een clientcertificaat installeert, moet u Hallo wachtwoord dat is gemaakt tijdens het Hallo-clientcertificaat is geëxporteerd. Dit is meestal simpelweg het gevolg van te dubbelklikken op Hallo-certificaat en te installeren. Zie [Een geëxporteerd clientcertificaat installeren](vpn-gateway-certificates-point-to-site.md#install) voor meer informatie.

## <a name="connect"></a>5. Verbinding maken met tooAzure

### <a name="connect-tooyour-vnet"></a>Verbinding maken met tooyour VNet

1. tooconnect tooyour VNet, op de clientcomputer hello, gaat u tooVPN verbindingen en zoek Hallo VPN-verbinding die u hebt gemaakt. Dit sjabloon heet Hallo dezelfde naam als het virtuele netwerk. Klik op **Verbinden**. Een pop-upbericht lijkt dat toousing Hallo certificaat verwijst. Als dit gebeurt, klikt u op **doorgaan** toouse verhoogde bevoegdheden.
2. Op Hallo **verbinding** statuspagina, klikt u op **Connect** toostart Hallo verbinding. Als u ziet een **certificaat selecteren** scherm, controleert u of dat het clientcertificaat Hallo Hallo een gewenste toouse tooconnect is. Als dit niet het geval is, Hallo pijl-omlaag tooselect Hallo juiste certificaat te gebruiken en klik vervolgens op **OK**.

  ![VPN-clientverbinding](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clientconnect.png)
3. De verbinding is tot stand gebracht.

  ![Tot stand gebrachte verbinding](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Problemen met P2S-verbindingen oplossen

[!INCLUDE [verify-client-certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

### <a name="verifyvpnconnect"></a>Hallo VPN-verbinding controleren

1. tooverify uw VPN-verbinding is actief en open een opdrachtprompt met verhoogde bevoegdheid en voer *ipconfig/all*.
2. Hallo resultaten weergeven. U ziet dat Hallo IP-adres die u hebt ontvangen, een van de adressen Hallo binnen connectiviteit-adresbereik voor het Hallo-punt-naar-Site die u hebt opgegeven toen u uw VNet hebt gemaakt. Hallo resultaten moeten vergelijkbaar toothis voorbeeld:

  ```
    PPP adapter VNet1:
        Connection-specific DNS Suffix .:
        Description.....................: VNet1
        Physical Address................:
        DHCP Enabled....................: No
        Autoconfiguration Enabled.......: Yes
        IPv4 Address....................: 192.168.130.2(Preferred)
        Subnet Mask.....................: 255.255.255.255
        Default Gateway.................:
        NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Verbinding maken met tooa virtuele machine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-classic-include.md)]

## <a name="add"></a>Vertrouwde basiscertificaten toevoegen of verwijderen

U kunt vertrouwde basiscertificaat toevoegen in en verwijderen uit Azure. Wanneer u een basiscertificaat verwijdert, clients die een certificaat dat is gegenereerd op basis van die hoofdmap niet kunnen tooauthenticate, en dus niet worden kunnen tooconnect. Als u wilt dat een client tooauthenticate en verbinding maakt, moet u een nieuw clientcertificaat gegenereerd op basis van een basiscertificaat dat wordt vertrouwd (geüploade) tooAzure tooinstall.

### <a name="addtrustedroot"></a>tooadd een vertrouwd basiscertificaat

U kunt toevoegen, too20 vertrouwde hoofdmap certificaat .cer bestanden tooAzure. Zie voor instructies [sectie 3: Upload Hallo .cer basiscertificaatbestand](#upload).

### <a name="removetrustedroot"></a>tooremove een vertrouwd basiscertificaat

1. Op Hallo **VPN-verbindingen** sectie Hallo-pagina voor uw VNet, klikt u op Hallo **clients** grafische tooopen hello **punt-naar-site VPN verbinding** pagina.

  ![Clients](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/clients125.png)
2. Op Hallo **punt-naar-site-verbinding** pagina, klikt u op **certificaten beheren** tooopen hello **certificaten** pagina.<br>

  ![De pagina Certificaten](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/ptsmanage.png)<br><br>
3. Op Hallo **certificaten** pagina, klikt u op Hallo weglatingsteken volgende toohello certificaat dat u wilt dat tooremove en klik vervolgens op **verwijderen**.

  ![Basiscertificaat verwijderen](./media/vpn-gateway-howto-point-to-site-classic-azure-portal/deleteroot.png)<br>

## <a name="revokeclient"></a>Een clientcertificaat intrekken

U kunt clientcertificaten intrekken. Hallo certificaat intrekkingslijst kunt u tooselectively weigeren op basis van afzonderlijke clientcertificaten punt-naar-Site-connectiviteit. Dit wijkt af van het verwijderen van een vertrouwd basiscertificaat. Als u een certificaat vertrouwd basiscertificaat .cer van Azure verwijdert, trekt het Hallo-toegang voor alle clientcertificaten gegenereerd/ondertekend door Hallo ingetrokken basiscertificaat. Intrekken van een clientcertificaat, staat in plaats van het basiscertificaat hello, Hallo andere certificaten die zijn gegenereerd uit Hallo root certificate toocontinue toobe gebruikt voor verificatie voor Hallo punt-naar-Site-verbinding.

Hallo gebruikelijk is toouse Hallo certificaat toomanage toegang tot de hoofdmap op team of organisatie niveaus, tijdens het gebruik van de ingetrokken clientcertificaten voor verfijnd toegangsbeheer op afzonderlijke gebruikers.

### <a name="revokeclientcert"></a>een clientcertificaat toorevoke

U kunt een certificaat intrekken door Hallo vingerafdruk toohello intrekkingslijst toe te voegen.

1. Hallo-client de vingerafdruk van certificaat ophalen. Zie voor meer informatie [hoe: ophalen Hallo vingerafdruk van een certificaat](https://msdn.microsoft.com/library/ms734695.aspx).
2. Hallo informatie tooa teksteditor kopiëren en verwijdert alle spaties zodat deze een doorlopend tekenreeks.
3. Navigeer toohello **'name klassiek virtueel netwerk' > punt-naar-site VPN-verbinding > Certificaten** pagina en klik vervolgens op **intrekkingslijst** tooopen hello intrekkingspagina lijst. 
4. Op Hallo **intrekkingslijst** pagina, klikt u op **+ certificaat toevoegen** tooopen hello **toorevocation lijst met certificaten toevoegen** pagina.
5. Op Hallo **toorevocation lijst met certificaten toevoegen** pagina, Hallo certificaatvingerafdruk plakken als een continue regel tekst, zonder spaties. Klik op **OK** Hallo Hallo pagina onderaan in.
6. Nadat het bijwerken is voltooid, kan Hallo certificaat niet langer gebruikt tooconnect. Clients die proberen tooconnect met dit certificaat ontvangen een bericht weergegeven dat Hallo-certificaat is niet meer geldig.

## <a name="faq"></a>Veelgestelde vragen over punt-naar-site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen
Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie. toounderstand meer informatie over netwerken en virtuele machines, Zie [overzicht van Azure en Linux-VM-netwerk](../virtual-machines/linux/azure-vm-network-overview.md).

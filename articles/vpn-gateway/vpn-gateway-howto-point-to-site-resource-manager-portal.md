---
title: 'Verbinding maken met een computer-tooa virtueel netwerk met punt-naar-Site en verificatie via certificaat: Azure Portal | Microsoft Docs'
description: Veilig verbinding maken met een computer tooyour Azure Virtual Network door het maken van een punt-naar-Site VPN-gatewayverbinding certificaatauthenticatie wordt gebruikt. In dit artikel is van toepassing toohello Resource Manager-implementatiemodel en hello Azure-portal gebruikt.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a15ad327-e236-461f-a18e-6dbedbf74943
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: 1419d6b4c160140b62d656b25bd02f6af7fd6655
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-azure-portal"></a>Een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat: Azure-portal

Dit artikel laat zien hoe een VNet met een punt-naar-Site-verbinding bij het gebruik van Hallo Resource Manager deployment model toocreate hello Azure-portal. Deze configuratie maakt gebruik van certificaten tooauthenticate Hallo client verbinding te maken. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Een punt-naar-Site (P2S) VPN-gateway kunt u een beveiligde verbinding tooyour virtueel netwerk maken van een afzonderlijke clientcomputer. Punt-naar-Site VPN-verbindingen zijn handig als u wilt dat tooconnect tooyour VNet vanaf een externe locatie, zoals wanneer u vanaf thuis of een conferentie zijn teleforenzen. Een P2S-VPN is ook een uitstekende oplossing toouse in plaats van een Site-naar-Site VPN-wanneer u slechts enkele clients hebt die tooconnect tooa VNet nodig hebt. 

Maakt gebruik van P2S Hallo SSTP Secure Socket Tunneling Protocol (), die een VPN op basis van een SSL-protocol. Een P2S-VPN-verbinding tot stand is gebracht vanaf Hallo-clientcomputer.

![Punt-naar-site-diagram](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/point-to-site-connection-diagram.png)

Punt-naar-Site certificaat verificatie verbindingen vereisen Hallo volgende:

* Een RouteBased VPN-gateway.
* Hallo openbare sleutel (.cer-bestand) voor een basiscertificaat dat geüpload tooAzure is. Zodra het Hallo-certificaat is geüpload, wordt beschouwd als een vertrouwd certificaat en wordt gebruikt voor verificatie.
* Een clientcertificaat dat is gegenereerd op basis van het basiscertificaat Hallo en geïnstalleerd op elke clientcomputer waarmee verbinding wordt gemaakt van toohello VNet. Dit certificaat wordt gebruikt voor clientverificatie.
* Een configuratiepakket voor de VPN-client. Hallo VPN-clientpakket configuratie bevat Hallo benodigde gegevens voor het Hallo client tooconnect toohello VNet. Hallo pakket configureert u het bestaande VPN-client hello, dat systeemeigen toohello Windows-besturingssysteem. Elke client die verbinding maakt, moet worden geconfigureerd met behulp van het configuratiepakket Hallo.

Punt-naar-site-verbindingen hebben geen VPN-apparaat of on-premises openbaar IP-adres nodig. Hallo VPN-verbinding wordt gemaakt via SSTP (Secure Socket Tunneling Protocol). Aan de serverzijde hello ondersteunen wij SSTP versies 1.0, 1.1 en 1.2. Hallo-client bepaalt welke versie toouse. Voor Windows 8.1 en hoger, gebruikt SSTP standaard 1.2.

Zie voor meer informatie over punt-naar-Site-verbindingen Hallo [punt-naar-Site Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.

#### <a name="example"></a>Voorbeeldwaarden

Gebruik Hallo waarden toocreate een testomgeving te volgen of toothese waarden verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel:

* **VNet-naam:** VNet1
* **Adresruimte:** 192.168.0.0/16<br>In dit voorbeeld gebruiken we slechts één adresruimte. U kunt meer dan één adresruimte voor uw VNet hebben.
* **Subnetnaam:** FrontEnd
* **Subnetadresbereik:** 192.168.1.0/24
* **Abonnement:** als u meer dan één abonnement hebt, Controleer of u de juiste Hallo.
* **Resourcegroep:** TestRG
* **Locatie:** VS - oost
* **GatewaySubnet:** 192.168.200.0/24<br>
* **DNS-Server:** (optioneel) IP-adres van Hallo DNS-server wilt u toouse voor naamomzetting.
* **Gatewaynaam van het virtuele netwerk:** VNet1GW
* **Gatewaytype:** VPN
* **VPN-type:** op route gebaseerd
* **Openbare IP-adresnaam:** VNet1GWpip
* **Verbindingstype:** punt-naar-site-verbinding
* **Clientadresgroep:** 172.16.201.0/24<br>VPN-clients die verbinding maken via deze punt-naar-Site-verbinding VNet toohello ontvangen een IP-adres van Hallo client-adresgroep.

## <a name="createvnet"></a>1. Een virtueel netwerk maken

Controleer eerst of u een Azure-abonnement hebt. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial).

[!INCLUDE [Basic Point-to-Site VNet](../../includes/vpn-gateway-basic-p2s-vnet-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>2. Een gatewaysubnet toevoegen

Voordat u verbinding maakt met uw virtuele netwerkgateway tooa, moet u eerst toocreate hello gatewaysubnet Hallo virtueel netwerk toowhich u tooconnect wilt. Hallo gatewayservices Hallo IP-adressen is opgegeven in het gatewaysubnet Hallo gebruiken. Maak indien mogelijk een gatewaysubnet met een CIDR-blok van/28 of /27 tooprovide voldoende IP-adressen tooaccommodate aanvullende toekomstige configuratievereisten.

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-p2s-rm-portal-include.md)]

## <a name="dns"></a>3. Een DNS-server opgeven (optioneel)

Nadat u het virtuele netwerk hebt gemaakt, kunt u Hallo IP-adres van een DNS-server toohandle naamomzetting kunt toevoegen. Hallo DNS-server is optioneel voor deze configuratie, maar vereist als u wilt dat naamomzetting. Het opgeven van een waarde betekent niet dat er een nieuwe DNS-server wordt gemaakt. Hallo moet DNS-server IP-adres dat u opgeeft een DNS-server die u kunt Hallo namen omzetten voor Hallo resources die u verbinding maakt. In dit voorbeeld wordt een particulier IP-adres gebruikt, maar is het waarschijnlijk dat dit geen Hallo IP-adres van uw DNS-server is. Worden toouse ervoor dat uw eigen waarden.

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="creategw"></a>4. De gateway van een virtueel netwerk maken

[!INCLUDE [create-gateway](../../includes/vpn-gateway-add-gw-p2s-rm-portal-include.md)]

## <a name="generatecert"></a>5. Certificaten genereren

Certificaten worden gebruikt door Azure tooauthenticate clients verbinding maken met tooa VNet via een punt-naar-Site VPN-verbinding. Wanneer u een basiscertificaat aanvragen u [uploaden](#uploadfile) Hallo openbare sleutelinformatie tooAzure. Hallo-basiscertificaat wordt vervolgens beschouwd als 'vertrouwd' door Azure voor verbinding via P2S toohello virtueel netwerk. U ook clientcertificaten te genereren uit het vertrouwde basiscertificaat Hallo en installeer ze dan op elke clientcomputer. Hallo-clientcertificaat is gebruikte tooauthenticate Hallo client wanneer een verbinding toohello VNet wordt gemaakt. 

### <a name="getcer"></a>1. Hallo cer-bestand voor het basiscertificaat Hallo verkrijgen

[!INCLUDE [root-certificate](../../includes/vpn-gateway-p2s-rootcert-include.md)]

### <a name="generateclientcert"></a>2. Een clientcertificaat genereren

[!INCLUDE [generate-client-cert](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="addresspool"></a>6. Hallo-clientadresgroep toevoegen

Hallo-clientadresgroep is een bereik van particuliere IP-adressen die u opgeeft. Hallo-clients die verbinding via een punt-naar-Site VPN maken ontvangen een IP-adres van dit bereik. Gebruiken een persoonlijk IP-adresbereik dat niet overlapt met Hallo on-premises locatie waarmee u verbinding maken of Hallo VNet dat u wilt dat tooconnect aan.

1. Nadat de virtuele netwerkgateway Hallo is gemaakt, gaat u toohello **instellingen** sectie van de pagina Hallo virtueel netwerk-gateway. In Hallo **instellingen** sectie, klikt u op **punt-naar-site-configuratie** tooopen hello **punt-naar-Site-configuratie** pagina.

  ![De pagina Punt-naar-site](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/gatewayblade.png)
2. Op Hallo **punt-naar-Site-configuratie** pagina kunt u Hallo automatisch gevulde bereik verwijderen en vervolgens Hallo persoonlijk IP-adresbereik dat u toouse wilt toevoegen. Klik op **opslaan** toovalidate en Hallo-instelling op te slaan.

  ![Clientadresgroep](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/ipaddresspool.png)

## <a name="uploadfile"></a>7. Hallo hoofdmap certificaatgegevens openbaar certificaat uploaden

Nadat het Hallo-gateway is gemaakt, kunt u Hallo openbare sleutelinformatie voor Hallo root certificate tooAzure uploaden. Wanneer gegevens van het openbare certificaat Hallo is geüpload, Azure kan worden gebruikt tooauthenticate-clients die een clientcertificaat dat is gegenereerd op basis van het vertrouwde basiscertificaat Hallo hebt geïnstalleerd. U kunt extra vertrouwde basis van certificaten tooa totaal van 20 uploaden.

1. Certificaten worden toegevoegd op Hallo **punt-naar-site-configuratie** pagina in Hallo **basiscertificaat** sectie.  
2. Zorg ervoor dat u een basiscertificaat Hallo geëxporteerd als een Base-64 X.509 (.cer)-bestand gecodeerde. U moet tooexport Hallo certificaat in deze indeling zodat u Hallo certificaat met een teksteditor openen kunt.
3. Open Hallo certificaat met een teksteditor zoals Kladblok. Bij het kopiëren van gegevens van het certificaat hello, zorg er dan voor dat u de tekst hello kopiëren als één continue regel zonder regelterugloop of regelinvoer. U moet mogelijk toomodify uw weergave in Hallo text editor too'Show symbool/weergeven alle tekens toosee Hallo regeleinde retourneert en regelinvoertekens. Kopieer alleen Hallo volgende sectie als één continue regel:

  ![Certificaatgegevens](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/copycert.png)
4. Hallo certificaatgegevens in Hallo plakken **openbare certificaatgegevens** veld. **Naam** Hallo certificaat en klik vervolgens op **opslaan**. U kunt toevoegen, too20 vertrouwde basiscertificaten.

  ![Certificaat uploaden](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/rootcertupload.png)

## <a name="clientconfig"></a>8. Genereren en Hallo VPN-clientpakket configuratie installeren

tooconnect tooa VNet met een punt-naar-Site VPN, moet elke client installeren met het een client-configuratiepakket dat Hallo systeemeigen VPN-client met Hallo-instellingen configureert en bestanden die nodig zijn tooconnect toohello virtueel netwerk zijn. Hallo VPN-clientpakket configuratie Hallo systeemeigen Windows VPN-client configureert, wordt een nieuwe of andere VPN-client niet geïnstalleerd.

Kunt u dezelfde configuratie van VPN-client van het pakket op elke clientcomputer hello, zolang het Hallo-versie komt overeen met de Hallo-architectuur voor Hallo-client. Voor de lijst van de Hallo van client-besturingssystemen die worden ondersteund, Zie Hallo [punt-naar-Site-verbindingen Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.

### <a name="step-1---generate-and-download-hello-client-configuration-package"></a>Stap 1 - genereren en Hallo configuratie clientpakket downloaden

1. Op Hallo **punt-naar-site-configuratie** pagina, klikt u op **downloaden VPN-client** tooopen hello **downloaden VPN-client** pagina. Het duurt enkele minuten duren voor Hallo pakket toogenerate.

  ![VPN-client downloaden 1](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/downloadvpnclient1.png)
2. Selecteer het juiste pakket Hallo voor de client en klik vervolgens op **downloaden**. Hallo-configuratiebestand pakket opslaan. U installeren Hallo VPN-clientpakket configuratie op elke clientcomputer die verbinding toohello virtueel netwerk maakt.

  ![VPN-client downloaden 2](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/vpnclient.png)

### <a name="step-2---install-hello-client-configuration-package"></a>Stap 2: installatie Hallo-clientpakket configuratie

1. Hallo-configuratiebestand kopiëren lokaal toohello computer die u wilt dat tooconnect tooyour virtueel netwerk. 
2. Dubbelklik op Hallo .exe-bestand tooinstall Hallo pakket op Hallo-clientcomputer. Omdat u het configuratiepakket Hallo hebt gemaakt, wordt het niet is ondertekend en ziet u een waarschuwing. Als u een pop-up Windows SmartScreen krijgt, klikt u op **meer info** (op Hallo links), vervolgens **toch uitvoeren** tooinstall Hallo-pakket.
3. Hallo-pakket installeren op Hallo-clientcomputer. Als u een pop-up Windows SmartScreen krijgt, klikt u op **meer info** (op Hallo links), vervolgens **toch uitvoeren** tooinstall Hallo-pakket.
4. Op de clientcomputer hello, te navigeren**netwerkinstellingen** en klik op **VPN**. Hallo VPN-verbinding bevat Hallo Hallo virtueel netwerk dat deze verbinding met maakt.

## <a name="installclientcert"></a>9. Een geëxporteerd clientcertificaat installeren

Als u wilt een P2S toocreate verbinding vanaf een clientcomputer dan Hallo u toogenerate Hallo clientcertificaten gebruikt, moet u een clientcertificaat tooinstall. Als u een clientcertificaat installeert, moet u Hallo wachtwoord dat is gemaakt tijdens het Hallo-clientcertificaat is geëxporteerd. Het is doorgaans simpelweg het gevolg van te dubbelklikken op Hallo-certificaat en te installeren.

Zorg ervoor dat het Hallo-clientcertificaat is geëxporteerd als een .pfx-bestand samen met de Hallo volledige certificaatketen (dit is standaard Hallo). Anders Hallo root-certificaatgegevens niet aanwezig is op de clientcomputer Hallo en Hallo-client niet kan tooauthenticate goed. Zie [Een geëxporteerd clientcertificaat installeren](vpn-gateway-certificates-point-to-site.md#install) voor meer informatie.

## <a name="connect"></a>10. Verbinding maken met tooAzure

1. tooconnect tooyour VNet, op de clientcomputer hello, gaat u tooVPN verbindingen en zoek Hallo VPN-verbinding die u hebt gemaakt. Dit sjabloon heet Hallo dezelfde naam als het virtuele netwerk. Klik op **Verbinden**. Een pop-upbericht lijkt dat toousing Hallo certificaat verwijst. Klik op **doorgaan** toouse verhoogde bevoegdheden.

2. Op Hallo **verbinding** statuspagina, klikt u op **Connect** toostart Hallo verbinding. Als u ziet een **certificaat selecteren** scherm, controleert u of dat het clientcertificaat Hallo Hallo een gewenste toouse tooconnect is. Als dit niet het geval is, Hallo pijl-omlaag tooselect Hallo juiste certificaat te gebruiken en klik vervolgens op **OK**.

  ![VPN-client verbinding maakt tooAzure](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/clientconnect.png)
3. De verbinding is tot stand gebracht.

  ![Verbinding tot stand gebracht](./media/vpn-gateway-howto-point-to-site-resource-manager-portal/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Problemen met P2S-verbindingen oplossen

[!INCLUDE [verifies client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>11. De verbinding controleren

1. tooverify uw VPN-verbinding is actief en open een opdrachtprompt met verhoogde bevoegdheid en voer *ipconfig/all*.
2. Hallo resultaten weergeven. U ziet dat Hallo IP-adres die u hebt ontvangen een Hallo adressen binnen Hallo punt-naar-Site VPN-Client-adresgroep die u hebt opgegeven in uw configuratie. Hallo resultaten zijn vergelijkbaar toothis voorbeeld:

  ```
  PPP adapter VNet1:
      Connection-specific DNS Suffix .:
      Description.....................: VNet1
      Physical Address................:
      DHCP Enabled....................: No
      Autoconfiguration Enabled.......: Yes
      IPv4 Address....................: 172.16.201.3(Preferred)
      Subnet Mask.....................: 255.255.255.255
      Default Gateway.................:
      NetBIOS over Tcpip..............: Enabled
  ```

## <a name="connectVM"></a>Verbinding maken met tooa virtuele machine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-p2s-include.md)]

## <a name="add"></a>Vertrouwde basiscertificaten toevoegen of verwijderen

U kunt vertrouwde basiscertificaat toevoegen in en verwijderen uit Azure. Wanneer u een basiscertificaat verwijdert, clients die een certificaat dat is gegenereerd op basis van die hoofdmap niet kunnen tooauthenticate, en dus niet worden kunnen tooconnect. Als u wilt dat een client tooauthenticate en verbinding maakt, moet u een nieuw clientcertificaat gegenereerd op basis van een basiscertificaat dat wordt vertrouwd (geüploade) tooAzure tooinstall.

### <a name="tooadd-a-trusted-root-certificate"></a>tooadd een vertrouwd basiscertificaat

U kunt toevoegen, too20 vertrouwde hoofdmap certificaat .cer bestanden tooAzure. Zie voor instructies Hallo sectie [een vertrouwd basiscertificaat uploaden](#uploadfile) in dit artikel.

### <a name="tooremove-a-trusted-root-certificate"></a>tooremove een vertrouwd basiscertificaat

1. een vertrouwd basiscertificaat tooremove navigeren toohello **punt-naar-site-configuratie** pagina voor uw virtuele netwerkgateway.
2. In Hallo **basiscertificaat** sectie Hallo pagina, vinden Hallo-certificaat dat u wilt dat tooremove.
3. Klik op Hallo weglatingsteken volgende toohello certificaat en klik op 'Verwijderen'.

## <a name="revokeclient"></a>Een clientcertificaat intrekken

U kunt clientcertificaten intrekken. Hallo certificaat intrekkingslijst kunt u tooselectively weigeren op basis van afzonderlijke clientcertificaten punt-naar-Site-connectiviteit. Dit is anders van het verwijderen van een vertrouwd basiscertificaat. Als u een certificaat vertrouwd basiscertificaat .cer van Azure verwijdert, trekt het Hallo-toegang voor alle clientcertificaten gegenereerd/ondertekend door Hallo ingetrokken basiscertificaat. Intrekken van een clientcertificaat, staat in plaats van het basiscertificaat hello, Hallo andere certificaten die zijn gegenereerd uit Hallo root certificate toocontinue toobe gebruikt voor verificatie.

Hallo gebruikelijk is toouse Hallo certificaat toomanage toegang tot de hoofdmap op team of organisatie niveaus, tijdens het gebruik van de ingetrokken clientcertificaten voor verfijnd toegangsbeheer op afzonderlijke gebruikers.

### <a name="toorevoke-a-client-certificate"></a>een clientcertificaat toorevoke

U kunt een certificaat intrekken door Hallo vingerafdruk toohello intrekkingslijst toe te voegen.

1. Hallo-client de vingerafdruk van certificaat ophalen. Zie voor meer informatie [hoe tooretrieve vingerafdruk van een certificaat Hallo](https://msdn.microsoft.com/library/ms734695.aspx).
2. Hallo informatie tooa teksteditor kopiëren en verwijdert alle spaties zodat deze een doorlopend tekenreeks.
3. De virtuele netwerkgateway toohello navigeren **punt-naar-site-configuratie** pagina. Dit is Hallo dezelfde pagina die u hebt gebruikt te[een vertrouwd basiscertificaat uploaden](#uploadfile).
4. In Hallo **ingetrokken certificaten** sectie, voer een beschrijvende naam voor het Hallo-certificaat (heeft geen toobe Hallo algemene naam van certificaat).
5. Kopieer en plak Hallo vingerafdruk tekenreeks toohello **vingerafdruk** veld.
6. Hallo vingerafdruk valideert en toohello intrekkingslijst automatisch wordt toegevoegd. Een bericht wordt weergegeven op het welkomstscherm die Hallo lijst wordt bijgewerkt. 
7. Nadat het bijwerken is voltooid, kan Hallo certificaat niet langer gebruikt tooconnect. Clients die proberen tooconnect met dit certificaat ontvangen een bericht weergegeven dat Hallo-certificaat is niet meer geldig.

## <a name="faq"></a>Veelgestelde vragen over punt-naar-site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen
Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie. toounderstand meer informatie over netwerken en virtuele machines, Zie [overzicht van Azure en Linux-VM-netwerk](../virtual-machines/linux/azure-vm-network-overview.md).

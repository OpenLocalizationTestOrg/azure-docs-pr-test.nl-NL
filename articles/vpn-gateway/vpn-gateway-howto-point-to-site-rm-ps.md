---
title: 'Verbinding maken met een computer tooan punt-naar-Site met virtuele Azure-netwerk en certificaat gebaseerde verificatie: PowerShell | Microsoft Docs'
description: Veilig verbinding maken met een computer tooyour virtueel netwerk door het maken van een punt-naar-Site VPN-gatewayverbinding certificaatauthenticatie wordt gebruikt. In dit artikel is van toepassing toohello Resource Manager-implementatiemodel en PowerShell gebruikt.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3eddadf6-2e96-48c4-87c6-52a146faeec6
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/10/2017
ms.author: cherylmc
ms.openlocfilehash: b962e4b1946a4ae17d4eb2b920ed54437bc26b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-point-to-site-connection-tooa-vnet-using-certificate-authentication-powershell"></a>Een punt-naar-Site-verbinding tooa VNet configureren met behulp van verificatie via certificaat: PowerShell

Dit artikel laat zien hoe toocreate een VNet met een punt-naar-Site-verbinding in Hallo Resource Manager deployment model met behulp van PowerShell. Deze configuratie maakt gebruik van certificaten tooauthenticate Hallo client verbinding te maken. Ook kunt u deze configuratie met behulp van verschillende hulpprogramma's of implementatiemodel door een andere optie kiezen in Hallo volgende lijst:

> [!div class="op_single_selector"]
> * [Azure Portal](vpn-gateway-howto-point-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-howto-point-to-site-rm-ps.md)
> * [Azure Portal (klassiek)](vpn-gateway-howto-point-to-site-classic-azure-portal.md)
>
>

Een punt-naar-Site (P2S) VPN-gateway kunt u een beveiligde verbinding tooyour virtueel netwerk maken van een afzonderlijke clientcomputer. Punt-naar-Site VPN-verbindingen zijn handig als u wilt dat tooconnect tooyour VNet vanaf een externe locatie, zoals wanneer u vanaf thuis of een conferentie zijn teleforenzen. Een P2S-VPN is ook een uitstekende oplossing toouse in plaats van een Site-naar-Site VPN-wanneer u slechts enkele clients hebt die tooconnect tooa VNet nodig hebt.

Maakt gebruik van P2S Hallo SSTP Secure Socket Tunneling Protocol (), die een VPN op basis van een SSL-protocol. Een P2S-VPN-verbinding tot stand is gebracht vanaf Hallo-clientcomputer.

![Verbinding maken met een computer tooan Azure VNet - verbindingsdiagram voor punt-naar-Site](./media/vpn-gateway-howto-point-to-site-rm-ps/point-to-site-diagram.png)

Punt-naar-Site certificaat verificatie verbindingen vereisen Hallo volgende:

* Een RouteBased VPN-gateway.
* Hallo openbare sleutel (.cer-bestand) voor een basiscertificaat dat geüpload tooAzure is. Zodra het Hallo-certificaat is geüpload, wordt beschouwd als een vertrouwd certificaat en wordt gebruikt voor verificatie.
* Een clientcertificaat dat is gegenereerd op basis van het basiscertificaat Hallo en geïnstalleerd op elke clientcomputer waarmee verbinding wordt gemaakt van toohello VNet. Dit certificaat wordt gebruikt voor clientverificatie.
* Een configuratiepakket voor de VPN-client. Hallo VPN-clientpakket configuratie bevat Hallo benodigde gegevens voor het Hallo client tooconnect toohello VNet. Hallo pakket configureert u het bestaande VPN-client hello, dat systeemeigen toohello Windows-besturingssysteem. Elke client die verbinding maakt, moet worden geconfigureerd met behulp van het configuratiepakket Hallo.

Punt-naar-site-verbindingen hebben geen VPN-apparaat of on-premises openbaar IP-adres nodig. Hallo VPN-verbinding wordt gemaakt via SSTP (Secure Socket Tunneling Protocol). Aan de serverzijde hello ondersteunen wij SSTP versies 1.0, 1.1 en 1.2. Hallo-client bepaalt welke versie toouse. Voor Windows 8.1 en hoger, gebruikt SSTP standaard 1.2. 

Zie voor meer informatie over punt-naar-Site-verbindingen Hallo [punt-naar-Site Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.

## <a name="before-beginning"></a>Voordat u begint

* Controleer of u een Azure-abonnement hebt. Als u nog geen Azure-abonnement hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) of [u aanmelden voor een gratis account](https://azure.microsoft.com/pricing/free-trial).
* Installeer de nieuwste versie Hallo Hallo Azure Resource Manager PowerShell-cmdlets. Zie voor meer informatie over het installeren van de PowerShell-cmdlets [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

### <a name="example"></a>Voorbeeldwaarden

Hallo voorbeeld waarden toocreate een testomgeving gebruiken of toothese waarden verwijzen toobetter begrijpen Hallo voorbeelden in dit artikel. We Hallo variabelen ingesteld in de sectie [1](#declare) van Hallo artikel. U kunt stappen hello gebruiken als een procedure en gebruik Hallo waarden niet wijzigen, of ze tooreflect wijzigen uw omgeving. 

* **Naam: VNet1**
* **Adresruimte: 192.168.0.0/16** en **10.254.0.0/16**<br>In dit voorbeeld gebruiken we meer dan één adresruimte tooillustrate die deze configuratie met meerdere adresruimten werkt. Meerdere adresruimten zijn echter niet vereist voor deze configuratie.
* **Subnetnaam: FrontEnd**
  * **Subnetadresbereik: 192.168.1.0/24**
* **Subnetnaam: BackEnd**
  * **Subnetadresbereik: 10.254.1.0/24**
* **Subnetnaam: GatewaySubnet**<br>de subnetnaam Hello *GatewaySubnet* is verplicht voor Hallo VPN-gateway toowork.
  * **Adresbereik GatewaySubnet: 192.168.200.0/24** 
* **VPN-clientadresgroep: 172.16.201.0/24**<br>VPN-clients die verbinding maken via deze punt-naar-Site-verbinding VNet toohello ontvangen een IP-adres van VPN-clientadresgroep Hallo.
* **Abonnement:** als u meer dan één abonnement hebt, Controleer of u de juiste Hallo.
* **Resourcegroep: TestRG**
* **Locatie: VS - oost**
* **DNS-Server: IP-adres** van Hallo DNS-server wilt u toouse voor naamomzetting.
* **Gatewaynaam: Vnet1GW**
* **Openbare IP-naam: VNet1GWPIP**
* **VPNType: op route gebaseerd** 

## <a name="declare"></a>1. Aanmelden en variabelen instellen

In deze sectie aanmelden en declareren Hallo waarden voor deze configuratie. Hallo gedeclareerd waarden in voorbeeldscripts hello worden gebruikt. Hallo waarden tooreflect uw eigen omgeving wijzigen. Of u kunt gebruiken Hallo waarden gedeclareerd en Hallo stappen doorlopen wijze van oefening maakt.

1. Open de PowerShell-console met verhoogde bevoegdheden en meld u bij tooyour Azure-account. Deze cmdlet wordt u gevraagd om inloggegevens Hallo. Na het aanmelden, downloadt het instellingen van uw account, zodat ze beschikbaar tooAzure PowerShell zijn.

  ```powershell
  Login-AzureRmAccount
  ```
2. Haal een lijst met uw Azure-abonnementen op.

  ```powershell
  Get-AzureRmSubscription
  ```
3. Hallo-abonnement dat u wilt dat toouse opgeven.

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
4. Hallo-variabelen die u wilt dat toouse declareren. Gebruik hello voorbeeld te volgen, vervangen door Hallo waarden voor uw eigen indien nodig.

  ```powershell
  $VNetName  = "VNet1"
  $FESubName = "FrontEnd"
  $BESubName = "Backend"
  $GWSubName = "GatewaySubnet"
  $VNetPrefix1 = "192.168.0.0/16"
  $VNetPrefix2 = "10.254.0.0/16"
  $FESubPrefix = "192.168.1.0/24"
  $BESubPrefix = "10.254.1.0/24"
  $GWSubPrefix = "192.168.200.0/26"
  $VPNClientAddressPool = "172.16.201.0/24"
  $RG = "TestRG"
  $Location = "East US"
  $DNS = "10.1.1.3"
  $GWName = "VNet1GW"
  $GWIPName = "VNet1GWPIP"
  $GWIPconfName = "gwipconf"
  ```

## <a name="ConfigureVNet"></a>2. Een VNet configureren

1. Maak een resourcegroep.

  ```powershell
  New-AzureRmResourceGroup -Name $RG -Location $Location
  ```
2. Hallo subnetconfiguraties maken voor Hallo virtueel netwerk, en ze naming *FrontEnd*, *back-end*, en *GatewaySubnet*. Deze voorvoegsels moeten deel uitmaken van Hallo VNet-adresruimte die u gedeclareerd.

  ```powershell
  $fesub = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName -AddressPrefix $FESubPrefix
  $besub = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName -AddressPrefix $BESubPrefix
  $gwsub = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName -AddressPrefix $GWSubPrefix
  ```
3. Hallo virtueel netwerk maken.

  In dit voorbeeld zijn Hallo DNS-server is optioneel. Het opgeven van een waarde betekent niet dat er een nieuwe DNS-server wordt gemaakt. Hallo moet DNS-server IP-adres dat u opgeeft een DNS-server die u kunt Hallo namen omzetten voor Hallo resources die u verbinding maakt. In dit voorbeeld wordt een particulier IP-adres gebruikt, maar is het waarschijnlijk dat dit geen Hallo IP-adres van uw DNS-server is. Worden toouse ervoor dat uw eigen waarden.

  ```powershell
  New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG -Location $Location -AddressPrefix $VNetPrefix1,$VNetPrefix2 -Subnet $fesub, $besub, $gwsub -DnsServer $DNS
  ```
4. Geef variabelen op Hallo voor Hallo virtuele netwerk die u hebt gemaakt.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet
  ```
5. Een VPN Gateway moet een openbaar IP-adres hebben. U eerst aanvragen Hallo IP-adres resource en vervolgens tooit verwijzen bij het maken van uw virtuele netwerkgateway. Hallo IP-adres dynamisch toegewezen toohello resource wanneer Hallo VPN-gateway is gemaakt. VPN Gateway ondersteunt momenteel alleen *dynamische* toewijzing van openbare IP-adressen. U kunt geen toewijzing van een statisch openbaar IP-adres aanvragen. Echter, het betekent niet dat Hallo IP-adres verandert nadat tooyour VPN-gateway is toegewezen. de enige keer Hallo Hallo openbare IP-adreswijzigingen is wanneer Hallo gateway is verwijderd en opnieuw gemaakt. Het verandert niet wanneer de grootte van uw VPN Gateway verandert, wanneer deze gateway opnieuw wordt ingesteld of wanneer andere interne onderhoudswerkzaamheden of upgrades worden uitgevoerd.

  Vraag een dynamisch toegewezen openbaar IP-adres aan.

  ```powershell
  $pip = New-AzureRmPublicIpAddress -Name $GWIPName -ResourceGroupName $RG -Location $Location -AllocationMethod Dynamic
  $ipconf = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName -Subnet $subnet -PublicIpAddress $pip
  ```

## <a name="creategateway"></a>3. Hallo VPN-gateway maken

Configureren en de virtuele netwerkgateway Hallo voor uw VNet maken.

* Hallo *- GatewayType* moet **Vpn** en Hallo *- VpnType* moet **RouteBased**.
* Een VPN-gateway kan duren voordat too45 minuten toocomplete, afhankelijk van Hallo [gateway-sku](vpn-gateway-about-vpn-gateway-settings.md) u selecteert.

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG `
-Location $Location -IpConfigurations $ipconf -GatewayType Vpn `
-VpnType RouteBased -EnableBgp $false -GatewaySku VpnGw1 `
```

## <a name="addresspool"></a>4. Hallo VPN-clientadresgroep toevoegen

Nadat het Hallo-VPN-gateway is gemaakt, kunt u Hallo VPN-clientadresgroep toevoegen. Hallo VPN-clientadresgroep is Hallo-bereik waarvan Hallo VPN-clients een IP-adres ontvangen wanneer verbinding wordt gemaakt. Gebruik een persoonlijk IP-adresbereik dat niet overlapt Hallo on-premises locatie waarmee u verbinding maken of met Hallo VNet dat u wilt dat tooconnect aan. In dit voorbeeld Hallo VPN-clientadresgroep is gedeclareerd als een [variabele](#declare) in stap 1.

```powershell
$Gateway = Get-AzureRmVirtualNetworkGateway -ResourceGroupName $RG -Name $GWName
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $Gateway -VpnClientAddressPool $VPNClientAddressPool
```

## <a name="Certificates"></a>5. Certificaten genereren

Certificaten worden gebruikt door Azure tooauthenticate VPN-clients voor punt-naar-Site VPN-verbindingen. U uploaden Hallo informatie over openbare sleutels van Hallo root certificate tooAzure. Hallo openbare sleutel vervolgens beschouwd als 'vertrouwd'. Clientcertificaten moeten worden gegenereerd op basis van het vertrouwde basiscertificaat Hallo en geïnstalleerd op elke clientcomputer in Hallo certificaten-huidige gebruiker/persoonlijk certificaatarchief. Hallo-certificaat is gebruikte tooauthenticate Hallo client wanneer een verbinding toohello VNet wordt gemaakt. 

Als u zelfondertekende certificaten gebruikt, moeten ze worden gemaakt met behulp van specifieke parameters. U kunt een zelfondertekend certificaat met behulp van instructies voor het Hallo maken [PowerShell en Windows 10](vpn-gateway-certificates-point-to-site.md), of als u geen Windows 10 hebt, kunt u [MakeCert](vpn-gateway-certificates-point-to-site-makecert.md). Het is belangrijk dat u Hallo in Hallo instructies stappen wanneer zelfondertekende basiscertificaten en clientcertificaten te genereren. Anders Hallo certificaten u genereert niet langer compatibel zijn met P2S-verbindingen en ontvangt u een verbindingsfout opgetreden.

### <a name="cer"></a>1. Hallo cer-bestand voor het basiscertificaat Hallo verkrijgen

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-rootcert-include.md)]


### <a name="generate"></a>2. Een clientcertificaat genereren

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-p2s-clientcert-include.md)]

## <a name="upload"></a>6. Hallo root certificate openbare sleutelinformatie uploaden

Controleer of het maken van de VPN-gateway is voltooid. Nadat deze is voltooid, kunt u Hallo cer-bestand (met daarin de openbare sleutelinformatie Hallo) voor een vertrouwd basiscertificaat certificaat tooAzure uploaden. Zodra a.cer bestand is geüpload, Azure kan worden gebruikt tooauthenticate-clients die een clientcertificaat dat is gegenereerd op basis van het vertrouwde basiscertificaat Hallo hebt geïnstalleerd. U kunt extra vertrouwde basis-certificaatbestanden - up tooa totaal van 20 - later uploaden, indien nodig.

1. Hallo-variabele voor de certificaatnaam van het, Hallo waarde vervangen door uw eigen declareren.

  ```powershell
  $P2SRootCertName = "P2SRootCert.cer"
  ```
2. Hallo-bestandspad vervangen door uw eigen en voer vervolgens Hallo-cmdlets.

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64
  ```
3. Hallo openbare sleutelinformatie tooAzure uploaden. Zodra het Hallo-certificaatinformatie is geüpload, beschouwt Azure deze toobe een vertrouwd basiscertificaat.

   ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64
  ```

## <a name="clientconfig"></a>7. Hallo VPN-clientpakket configuratie downloaden

tooconnect tooa VNet met een punt-naar-Site VPN, moet elke client installeren met het een client-configuratiepakket dat Hallo systeemeigen VPN-client met Hallo-instellingen configureert en bestanden die nodig zijn tooconnect toohello virtueel netwerk zijn. Hallo VPN-clientpakket configuratie Hallo systeemeigen Windows VPN-client configureert, wordt een nieuwe of andere VPN-client niet geïnstalleerd. 

Kunt u dezelfde configuratie van VPN-client van het pakket op elke clientcomputer hello, zolang het Hallo-versie komt overeen met de Hallo-architectuur voor Hallo-client. Voor de lijst van de Hallo van client-besturingssystemen die worden ondersteund, Zie Hallo [punt-naar-Site-verbindingen Veelgestelde vragen over](#faq) aan Hallo einde van dit artikel.

1. Nadat het Hallo-gateway is gemaakt, kunt u genereren en Hallo configuratie clientpakket downloaden. In dit voorbeeld downloads Hallo-pakket voor 64-bits clients. Als u toodownload Hallo 32-bits client wilt, vervangen door 'Amd64' 'x86'. U kunt Hallo VPN-client ook downloaden via hello Azure-portal.

  ```powershell
  Get-AzureRmVpnClientPackage -ResourceGroupName $RG `
  -VirtualNetworkGatewayName $GWName -ProcessorArchitecture Amd64
  ```
2. Kopieer en plak Hallo-koppeling die tooa web browser toodownload Hallo pakket, wordt gelet op de tooremove Hallo aanhalingstekens rond Hallo koppeling wordt geretourneerd. 
3. Download en installeer Hallo-pakket op Hallo-clientcomputer. Als u een SmartScreen-melding ziet, klikt u op **Meer info** en vervolgens op **Toch uitvoeren**. U kunt ook Hallo pakket tooinstall opslaan op andere clientcomputers.
4. Op de clientcomputer hello, te navigeren**netwerkinstellingen** en klik op **VPN**. Hallo VPN-verbinding bevat Hallo Hallo virtueel netwerk dat deze verbinding met maakt.

## <a name="clientcertificate"></a>8. Een geëxporteerd clientcertificaat installeren

Als u wilt een P2S toocreate verbinding vanaf een clientcomputer dan Hallo u toogenerate Hallo clientcertificaten gebruikt, moet u een clientcertificaat tooinstall. Als u een clientcertificaat installeert, moet u Hallo wachtwoord dat is gemaakt tijdens het Hallo-clientcertificaat is geëxporteerd. Het is doorgaans simpelweg het gevolg van te dubbelklikken op Hallo-certificaat en te installeren.

Zorg ervoor dat het Hallo-clientcertificaat is geëxporteerd als een .pfx-bestand samen met de Hallo volledige certificaatketen (dit is standaard Hallo). Anders Hallo root-certificaatgegevens niet aanwezig is op de clientcomputer Hallo en Hallo-client niet kan tooauthenticate goed. Zie [Een geëxporteerd clientcertificaat installeren](vpn-gateway-certificates-point-to-site.md#install) voor meer informatie. 

## <a name="connect"></a>9. Verbinding maken met tooAzure

1. tooconnect tooyour VNet, op de clientcomputer hello, gaat u tooVPN verbindingen en zoek Hallo VPN-verbinding die u hebt gemaakt. Dit sjabloon heet Hallo dezelfde naam als het virtuele netwerk. Klik op **Verbinden**. Een pop-upbericht lijkt dat toousing Hallo certificaat verwijst. Klik op **doorgaan** toouse verhoogde bevoegdheden. 
2. Op Hallo **verbinding** statuspagina, klikt u op **Connect** toostart Hallo verbinding. Als u ziet een **certificaat selecteren** scherm, controleert u of dat het clientcertificaat Hallo Hallo een gewenste toouse tooconnect is. Als dit niet het geval is, Hallo pijl-omlaag tooselect Hallo juiste certificaat te gebruiken en klik vervolgens op **OK**.

  ![VPN-client verbinding maakt tooAzure](./media/vpn-gateway-howto-point-to-site-rm-ps/clientconnect.png)
3. De verbinding is tot stand gebracht.

  ![Verbinding tot stand gebracht](./media/vpn-gateway-howto-point-to-site-rm-ps/connected.png)

#### <a name="troubleshooting-p2s-connections"></a>Problemen met P2S-verbindingen oplossen

[!INCLUDE [client certificates](../../includes/vpn-gateway-certificates-verify-client-cert-include.md)]

## <a name="verify"></a>10. De verbinding controleren

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

## <a name="addremovecert"></a>Een basiscertificaat toevoegen of verwijderen

U kunt vertrouwde basiscertificaat toevoegen in en verwijderen uit Azure. Wanneer u een basiscertificaat verwijdert, clients die een certificaat dat is gegenereerd op basis van het basiscertificaat Hallo kunnen niet worden geverifieerd en niet kunnen tooconnect. Als u wilt dat een client tooauthenticate en verbinding maakt, moet u een nieuw clientcertificaat gegenereerd op basis van een basiscertificaat dat wordt vertrouwd (geüploade) tooAzure tooinstall.

### <a name="addtrustedroot"></a>tooadd een vertrouwd basiscertificaat

U kunt toevoegen, too20 root certificate .cer bestanden tooAzure. Hallo volgende stappen help u een basiscertificaat toevoegen:

#### <a name="certmethod1"></a>Methode 1

Dit is Hallo efficiëntste methode tooupload een basiscertificaat.

1. Hallo .cer-bestand tooupload voorbereiden:

  ```powershell
  $filePathForCert = "C:\cert\P2SRootCert3.cer"
  $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($filePathForCert)
  $CertBase64_3 = [system.convert]::ToBase64String($cert.RawData)
  $p2srootcert = New-AzureRmVpnClientRootCertificate -Name $P2SRootCertName -PublicCertData $CertBase64_3
  ```
2. Hallo-bestand uploaden. U kunt slechts één bestand tegelijk uploaden.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $CertBase64_3
  ```

3. tooverify dat bestand Hallo-certificaat geüpload:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

#### <a name="certmethod2"></a>Methode 2

Deze methode is een aantal extra stappen dan methode 1, maar heeft hetzelfde resultaat Hallo. Het is opgenomen als u tooview Hallo certificaatgegevens nodig hebt.

1. Maak en Hallo nieuwe root certificate tooadd tooAzure voorbereiden. Hallo openbare sleutel niet exporteren als een Base-64 X.509 gecodeerde (. CER) en open het met een teksteditor. Kopieer Hallo waarden, zoals weergegeven in Hallo voorbeeld te volgen:

  ![certificaat](./media/vpn-gateway-howto-point-to-site-rm-ps/copycert.png)

  > [!NOTE]
  > Bij het kopiëren van gegevens van het certificaat hello, zorg er dan voor dat u de tekst hello kopiëren als één continue regel zonder regelterugloop of regelinvoer. U moet mogelijk toomodify uw weergave in Hallo text editor too'Show symbool/weergeven alle tekens toosee Hallo regeleinde retourneert en regelinvoertekens.
  >
  >

2. Hallo certificaatnaam en belangrijke informatie opgeven als een variabele. Hallo gegevens vervangen door uw eigen, zoals weergegeven in Hallo volgende voorbeeld:

  ```powershell
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
3. Hallo nieuwe basiscertificaat toevoegen. U kunt slechts één certificaat tegelijk toevoegen.

  ```powershell
  Add-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayname "VNet1GW" -ResourceGroupName "TestRG" -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
4. U kunt controleren dat Hallo nieuwe certificaat correct is toegevoegd met behulp van Hallo voorbeeld te volgen:

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

### <a name="removerootcert"></a>tooremove een basiscertificaat

1. Hallo variabelen declareren.

  ```powershell
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  $P2SRootCertName2 = "ARMP2SRootCert2.cer"
  $MyP2SCertPubKeyBase64_2 = "MIIC/zCCAeugAwIBAgIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAMBgxFjAUBgNVBAMTDU15UDJTUm9vdENlcnQwHhcNMTUxMjE5MDI1MTIxWhcNMzkxMjMxMjM1OTU5WjAYMRYwFAYDVQQDEw1NeVAyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAyjIXoWy8xE/GF1OSIvUaA0bxBjZ1PJfcXkMWsHPzvhWc2esOKrVQtgFgDz4ggAnOUFEkFaszjiHdnXv3mjzE2SpmAVIZPf2/yPWqkoHwkmrp6BpOvNVOpKxaGPOuK8+dql1xcL0eCkt69g4lxy0FGRFkBcSIgVTViS9wjuuS7LPo5+OXgyFkAY3pSDiMzQCkRGNFgw5WGMHRDAiruDQF1ciLNojAQCsDdLnI3pDYsvRW73HZEhmOqRRnJQe6VekvBYKLvnKaxUTKhFIYwuymHBB96nMFdRUKCZIiWRIy8Hc8+sQEsAML2EItAjQv4+fqgYiFdSWqnQCPf/7IZbotgQIDAQABo00wSzBJBgNVHQEEQjBAgBAkuVrWvFsCJAdK5pb/eoCNoRowGDEWMBQGA1UEAxMNTXlQMlNSb290Q2VydIIQKazxzFjMkp9JRiX+tkTfSzAJBgUrDgMCHQUAA4IBAQA223veAZEIar9N12ubNH2+HwZASNzDVNqspkPKD97TXfKHlPlIcS43TaYkTz38eVrwI6E0yDk4jAuPaKnPuPYFRj9w540SvY6PdOUwDoEqpIcAVp+b4VYwxPL6oyEQ8wnOYuoAK1hhh20lCbo8h9mMy9ofU+RP6HJ7lTqupLfXdID/XevI8tW6Dm+C/wCeV3EmIlO9KUoblD/e24zlo3YzOtbyXwTIh34T0fO/zQvUuBqZMcIPfM1cDvqcqiEFLWvWKoAnxbzckye2uk1gHO52d8AVL3mGiX8wBJkjc/pMdxrEvvCzJkltBmqxTM6XjDJALuVh16qFlqgTWCIcb7ju"
  ```
2. Hallo-certificaat verwijderen.

  ```powershell
  Remove-AzureRmVpnClientRootCertificate -VpnClientRootCertificateName $P2SRootCertName2 -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -PublicCertData $MyP2SCertPubKeyBase64_2
  ```
3. Gebruik Hallo na voorbeeld tooverify die Hallo certificaat is verwijderd.

  ```powershell
  Get-AzureRmVpnClientRootCertificate -ResourceGroupName "TestRG" `
  -VirtualNetworkGatewayName "VNet1GW"
  ```

## <a name="revoke"></a>Een clientcertificaat intrekken

U kunt clientcertificaten intrekken. Hallo certificaat intrekkingslijst kunt u tooselectively weigeren op basis van afzonderlijke clientcertificaten punt-naar-Site-connectiviteit. Dit is anders van het verwijderen van een vertrouwd basiscertificaat. Als u een certificaat vertrouwd basiscertificaat .cer van Azure verwijdert, trekt het Hallo-toegang voor alle clientcertificaten gegenereerd/ondertekend door Hallo ingetrokken basiscertificaat. Intrekken van een clientcertificaat, staat in plaats van het basiscertificaat hello, Hallo andere certificaten die zijn gegenereerd uit Hallo root certificate toocontinue toobe gebruikt voor verificatie.

Hallo gebruikelijk is toouse Hallo certificaat toomanage toegang tot de hoofdmap op team of organisatie niveaus, tijdens het gebruik van de ingetrokken clientcertificaten voor verfijnd toegangsbeheer op afzonderlijke gebruikers.

### <a name="revokeclientcert"></a>een clientcertificaat toorevoke

1. Hallo-client de vingerafdruk van certificaat ophalen. Zie voor meer informatie [hoe tooretrieve vingerafdruk van een certificaat Hallo](https://msdn.microsoft.com/library/ms734695.aspx).
2. Hallo informatie tooa teksteditor kopiëren en verwijdert alle spaties zodat deze een doorlopend tekenreeks. Deze tekenreeks is gedeclareerd als een variabele in de volgende stap Hallo.
3. Hallo variabelen declareren. Zorg ervoor dat toodeclare Hallo vingerafdruk dat u hebt opgehaald in de vorige stap Hallo.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
4. Hallo vingerafdruk toohello lijst met ingetrokken certificaten toevoegen. 'Geslaagd' ziet u wanneer Hallo vingerafdruk is toegevoegd.

  ```powershell
  Add-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG `
  -Thumbprint $RevokedThumbprint1
  ```
5. Controleer of dat vingerafdruk Hallo toohello certificaatintrekkingslijst is toegevoegd.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```
6. Nadat het Hallo-vingerafdruk is toegevoegd, kan Hallo certificaat niet langer gebruikt tooconnect. Clients die proberen tooconnect met dit certificaat ontvangen een bericht weergegeven dat Hallo-certificaat is niet meer geldig.

### <a name="reinstateclientcert"></a>een clientcertificaat tooreinstate

U kunt een clientcertificaat herstellen door het verwijderen van Hallo vingerafdruk uit Hallo lijst met ingetrokken clientcertificaten.

1. Hallo variabelen declareren. Zorg ervoor dat u de juiste vingerafdruk Hallo voor Hallo-certificaat dat u wilt dat tooreinstate declareren.

  ```powershell
  $RevokedClientCert1 = "NameofCertificate"
  $RevokedThumbprint1 = "‎51ab1edd8da4cfed77e20061c5eb6d2ef2f778c7"
  $GWName = "Name_of_virtual_network_gateway"
  $RG = "Name_of_resource_group"
  ```
2. Hallo certificaatvingerafdruk uit Hallo certificaatintrekkingslijst verwijderen.

  ```powershell
  Remove-AzureRmVpnClientRevokedCertificate -VpnClientRevokedCertificateName $RevokedClientCert1 `
  -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG -Thumbprint $RevokedThumbprint1
  ```
3. Controleer of het Hallo-vingerafdruk is verwijderd uit Hallo ingetrokken lijst.

  ```powershell
  Get-AzureRmVpnClientRevokedCertificate -VirtualNetworkGatewayName $GWName -ResourceGroupName $RG
  ```

## <a name="faq"></a>Veelgestelde vragen over punt-naar-site

[!INCLUDE [Point-to-Site FAQ](../../includes/vpn-gateway-point-to-site-faq-include.md)]

## <a name="next-steps"></a>Volgende stappen
Zodra de verbinding voltooid is, kunt u virtuele netwerken van virtuele machines tooyour kunt toevoegen. Zie [Virtuele machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute) voor meer informatie. toounderstand meer informatie over netwerken en virtuele machines, Zie [overzicht van Azure en Linux-VM-netwerk](../virtual-machines/linux/azure-vm-network-overview.md).

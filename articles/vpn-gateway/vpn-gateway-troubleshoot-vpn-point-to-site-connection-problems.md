---
title: verbindingsproblemen aaaTroubleshoot Azure punt-naar-site | Microsoft Docs
description: Meer informatie over hoe problemen met de tootroubleshoot punt-naar-site-verbinding.
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/23/2017
ms.author: genli
ms.openlocfilehash: 98d66074be62ad8c7153a903f69cb0d01f988cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-point-to-site-connection-problems"></a>Voor probleemoplossing: Problemen met de Azure-punt-naar-site-verbinding

Dit artikel worden veelvoorkomende problemen met de punt-naar-site-verbinding die u kunt ervaren. Ook wordt beschreven mogelijke oorzaken en oplossingen voor deze problemen.

## <a name="vpn-client-error-a-certificate-could-not-be-found"></a>VPN-Clientfout: kan certificaat niet vinden.

### <a name="symptom"></a>Symptoom

Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:

**Een certificaat kan niet worden gevonden die kan worden gebruikt met dit Extensible Authentication Protocol. (Fout 798)**

### <a name="cause"></a>Oorzaak

Dit probleem treedt op als het clientcertificaat Hallo ontbreekt in **Certificaten - Huidige gebruiker\Persoonlijk\Certificaten**.

### <a name="solution"></a>Oplossing

Zorg ervoor dat certificaat Hallo-client is geïnstalleerd in Hallo locatie van het Hallo-archief met certificaten (Certmgr.msc) te volgen:
 
**Certificaten - Huidige gebruiker\Persoonlijk\Certificaten**

Zie voor meer informatie over hoe tooinstall clientcertificaat Hallo [genereren en exporteren van certificaten voor punt-naar-site-verbindingen](vpn-gateway-certificates-point-to-site.md).

> [!NOTE]
> Wanneer u het clientcertificaat Hallo importeert, selecteer niet Hallo **zware beveiliging van persoonlijke sleutel inschakelen** optie.

## <a name="vpn-client-error-hello-message-received-was-unexpected-or-badly-formatted"></a>VPN-Clientfout: het Hallo-bericht ontvangen is onverwacht of onjuist ingedeeld

### <a name="symptom"></a>Symptoom

Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:

**Hallo-bericht ontvangen is onverwacht of onjuist ingedeeld. (Fout 0x80090326)**

### <a name="cause"></a>Oorzaak

Dit probleem treedt op als openbare sleutel Hallo hoofdmap is niet geüpload naar hello Azure VPN-gateway. Het kan ook optreden als het Hallo-sleutel is beschadigd of verlopen.

### <a name="solution"></a>Oplossing

tooresolve dit probleem op door Hallo de status van Hallo root certificate in Azure portal toosee Hallo of deze is ingetrokken. Als deze niet is ingetrokken, probeert toodelete Hallo-basiscertificaat en reupload. Zie voor meer informatie [certificaten maken](vpn-gateway-howto-point-to-site-classic-azure-portal.md#generatecerts).

## <a name="vpn-client-error-a-certificate-chain-processed-but-terminated"></a>VPN-Clientfout: een certificaatketen verwerkt, maar is beëindigd 

### <a name="symptom"></a>Symptoom 

Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:

**Een certificaatketen verwerkt, maar in een basiscertificaat dat wordt niet vertrouwd door Hallo vertrouwensrelatieprovider is beëindigd.**

### <a name="solution"></a>Oplossing

1. Zorg ervoor dat Hallo volgende certificaten in de juiste locatie Hallo:

    | Certificaat | Locatie |
    | ------------- | ------------- |
    | AzureClient.pfx  | Huidige gebruiker\Persoonlijk\Certificaten |
    | Azuregateway -*GUID*. cloudapp.net  | Huidige User\Trusted basiscertificeringsinstanties|
    | AzureGateway -*GUID*. cloudapp.net, AzureRoot.cer    | Lokale Computer\Trusted Root Certification Authorities|

2. Als Hallo certificaten al op Hallo locatie zijn, probeer toodelete Hallo certificaten en installeert u deze opnieuw. Hallo  **azuregateway -*GUID*. cloudapp.net** certificaat bevindt zich in Hallo VPN-configuratie clientpakket die u hebt gedownload van hello Azure-portal. U kunt archivers tooextract Hallo-bestanden uit het Hallo-pakket.

## <a name="file-download-error-target-uri-is-not-specified"></a>Fout bij het downloaden bestand: doel-URI is niet opgegeven.

### <a name="symptom"></a>Symptoom

U ontvangt Hallo volgende foutbericht weergegeven:

**Fout bij het downloaden van het bestand. Doel-URI is niet opgegeven.**

### <a name="cause"></a>Oorzaak 

Dit probleem treedt vanwege een onjuiste Gatewaytype. 

### <a name="solution"></a>Oplossing

Hallo VPN-gateway-type moet **VPN**, en Hallo VPN-type moet **RouteBased**.

## <a name="vpn-client-error-azure-vpn-custom-script-failed"></a>VPN-Clientfout: aangepaste Azure VPN-script is mislukt 

### <a name="symptom"></a>Symptoom

Wanneer u tooconnect tooan virtuele Azure-netwerk met behulp van Hallo VPN-client, wordt u Hallo volgende foutbericht weergegeven:

**Aangepast script (tooupdate uw bewerkingsplan tabel) is mislukt. (Fout 8007026f)**

### <a name="cause"></a>Oorzaak

Dit probleem kan optreden als u tooopen Hallo site-naar-punt VPN-verbinding probeert met een snelkoppeling.

### <a name="solution"></a>Oplossing 

Open Hallo VPN-pakket rechtstreeks in plaats van vanuit de snelkoppeling Hallo openen.

## <a name="cannot-install-hello-vpn-client"></a>Hallo VPN-client installeren niet

### <a name="cause"></a>Oorzaak 

Een aanvullend certificaat is vereist tootrust Hallo VPN-gateway voor het virtuele netwerk. Hallo-certificaat is opgenomen in Hallo VPN-configuratie clientpakket die is gegenereerd op basis van hello Azure-portal.

### <a name="solution"></a>Oplossing

Pak Hallo VPN-clientpakket configuratie en Hallo cer-bestand vinden. Hallo tooinstall certificaat, als volgt te werk:

1. Open mmc.exe.
2. Hallo toevoegen **certificaten** -module.
3. Selecteer Hallo **Computer** voor de lokale computer Hallo-account.
4. Klik met de rechtermuisknop Hallo **Trusted Root Certification Authorities** knooppunt. Klik op **All-taak** > **importeren**, en bladeren toohello cer-bestand die u hebt opgehaald uit Hallo VPN-clientpakket configuratie.
5. Hallo-computer opnieuw opstarten. 
6. Probeer tooinstall Hallo VPN-client.

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-data-is-invalid"></a>Azure portal-fout: kan niet toosave Hallo VPN-gateway en Hallo gegevens is ongeldig

### <a name="symptom"></a>Symptoom

Wanneer u wijzigingen in de toosave Hallo voor Hallo VPN-gateway in hello Azure-portal, ontvangen Hallo volgende foutbericht weergegeven:

**De virtuele netwerkgateway mislukte toosave &lt;* gatewaynaam*&gt;. Gegevens voor certificaat &lt; *-certificaat-ID* &gt; is invalid.* *

### <a name="cause"></a>Oorzaak 

Dit probleem kan optreden als Hallo hoofdmap openbare sleutel die u hebt geüpload een ongeldig teken, zoals een spatie bevat.

### <a name="solution"></a>Oplossing

Zorg ervoor dat het Hallo-gegevens in Hallo certificaat bevat geen ongeldige tekens, zoals regeleinden (regelterugloop). Hallo gehele waarde moet een lange regel zijn. na de tekst Hello is een voorbeeld van Hallo certificaat:

    -----BEGIN CERTIFICATE-----
    MIIC5zCCAc+gAwIBAgIQFSwsLuUrCIdHwI3hzJbdBjANBgkqhkiG9w0BAQsFADAW
    MRQwEgYDVQQDDAtQMlNSb290Q2VydDAeFw0xNzA2MTUwMjU4NDZaFw0xODA2MTUw
    MzE4NDZaMBYxFDASBgNVBAMMC1AyU1Jvb3RDZXJ0MIIBIjANBgkqhkiG9w0BAQEF
    AAOCAQ8AMIIBCgKCAQEAz8QUCWCxxxTrxF5yc5uUpL/bzwC5zZ804ltB1NpPa/PI
    sa5uwLw/YFb8XG/JCWxUJpUzS/kHUKFluqkY80U+fAmRmTEMq5wcaMhp3wRfeq+1
    G9OPBNTyqpnHe+i54QAnj1DjsHXXNL4AL1N8/TSzYTm7dkiq+EAIyRRMrZlYwije
    407ChxIp0stB84MtMShhyoSm2hgl+3zfwuaGXoJQwWiXh715kMHVTSj9zFechYd7
    5OLltoRRDyyxsf0qweTFKIgFj13Hn/bq/UJG3AcyQNvlCv1HwQnXO+hckVBB29wE
    sF8QSYk2MMGimPDYYt4ZM5tmYLxxxvGmrGhc+HWXzMeQIDAQABozEwLzAOBgNVHQ8B
    Af8EBAMCAgQwHQYDVR0OBBYEFBE9zZWhQftVLBQNATC/LHLvMb0OMA0GCSqGSIb3
    DQEBCwUAA4IBAQB7k0ySFUQu72sfj3BdNxrXSyOT4L2rADLhxxxiK0U6gHUF6eWz
    /0h6y4mNkg3NgLT3j/WclqzHXZruhWAXSF+VbAGkwcKA99xGWOcUJ+vKVYL/kDja
    gaZrxHlhTYVVmwn4F7DWhteFqhzZ89/W9Mv6p180AimF96qDU8Ez8t860HQaFkU6
    2Nw9ZMsGkvLePZZi78yVBDCWMogBMhrRVXG/xQkBajgvL5syLwFBo2kWGdC+wyWY
    U/Z+EK9UuHnn3Hkq/vXEzRVsYuaxchta0X2UNRzRq+o706l+iyLTpe6fnvW6ilOi
    e8Jcej7mzunzyjz4chN0/WVF94MtxbUkLkqP
    -----END CERTIFICATE-----

## <a name="azure-portal-error-failed-toosave-hello-vpn-gateway-and-hello-resource-name-is-invalid"></a>Azure portal-fout: kan niet toosave Hallo VPN-gateway en Hallo resourcenaam is ongeldig

### <a name="symptom"></a>Symptoom

Wanneer u wijzigingen in de toosave Hallo voor Hallo VPN-gateway in hello Azure-portal, ontvangen Hallo volgende foutbericht weergegeven: 

**De virtuele netwerkgateway mislukte toosave &lt;* gatewaynaam*&gt;. Resourcenaam &lt; *certificaatnaam die u probeert tooupload* &gt; is ongeldig **.

### <a name="cause"></a>Oorzaak

Dit probleem treedt op omdat het Hallo-naam van Hallo certificaat bevat een ongeldig teken, zoals een spatie. 

## <a name="azure-portal-error-vpn-package-file-download-error-503"></a>Azure portal-fout: VPN-pakket bestand Downloadfout 503

### <a name="symptom"></a>Symptoom

Wanneer u toodownload Hallo VPN-clientpakket-configuratie, ontvangen Hallo volgende foutbericht weergegeven:

**Kan niet toodownload Hallo-bestand. Details van fout: fout 503. Hallo-server is bezet.**
 
### <a name="solution"></a>Oplossing

Deze fout kan worden veroorzaakt door een tijdelijk netwerkprobleem. Probeer toodownload Hallo VPN-pakket na een paar minuten opnieuw.

## <a name="azure-vpn-gateway-upgrade-all-p2s-clients-are-unable-tooconnect"></a>Upgrade uitvoeren voor Azure VPN-Gateway: alle P2S-clients zijn tooconnect

### <a name="cause"></a>Oorzaak

Hallo-certificaat is meer dan 50 procent via hun levensduur Hallo certificaat wordt overgeschakeld.

### <a name="solution"></a>Oplossing

tooresolve dit probleem maken en distribueren van nieuwe certificaten toohello VPN-clients. 

## <a name="too-many-vpn-clients-connected-at-once"></a>Te veel VPN-clients tegelijk verbonden

Voor elke VPN-gateway is Hallo kunt u het maximum aantal toegestane verbindingen 128. Hier ziet u Hallo totaal aantal verbonden clients in hello Azure-portal.

## <a name="point-to-site-vpn-incorrectly-adds-a-route-for-100008-toohello-route-table"></a>Punt-naar-site VPN wordt een route voor de routetabel voor 10.0.0.0/8 toohello onjuist toegevoegd

### <a name="symptom"></a>Symptoom

Wanneer u Hallo VPN-verbinding op Hallo punt-naar-site-client kiest, moet Hallo VPN-client een route naar Hallo virtuele Azure-netwerk toevoegen. Hallo IP-helper-service moet een route voor subnet Hallo Hallo VPN-clients toevoegen. 

Hallo VPN-client bereik hoort tooa kleinere subnet 10.0.0.0/8, zoals 10.0.12.0/24. In plaats van een route voor 10.0.12.0/24, wordt een route voor 10.0.0.0/8 toegevoegd die een hogere prioriteit heeft. 

Deze onjuiste route verbroken connectiviteit met andere on-premises-netwerken die mogelijk behoren tooanother subnet binnen Hallo 10.0.0.0/8 bereik, zoals 10.50.0.0/24, waarvoor geen een specifieke route gedefinieerd. 

### <a name="cause"></a>Oorzaak

Dit gedrag is inherent aan het ontwerp voor Windows-clients. Wanneer de client Hallo Hallo IPCP PPP-protocol gebruikt, verkrijgt het Hallo IP-adres voor het Hallo-tunnelinterface van Hallo server (Hallo VPN-gateway in dit geval). Echter, vanwege een beperking in Hallo-protocol, Hallo client heeft geen Hallo subnetmasker. Omdat er geen andere manier tooget probeert het Hallo-client tooguess Hallo-subnetmasker op basis van de klasse Hallo van Hallo tunnel-interface IP-adres. 

Een route is daarom toegevoegd op basis van Hallo statische toewijzing te volgen: 

Als het adres behoort tooclass A-->/8 die van toepassing

Als het adres behoort toepassen tooclass B--> /16

Als het adres behoort toepassen tooclass C--> /24

## <a name="vpn-client-cannot-access-network-file-shares"></a>VPN-client heeft geen toegang tot netwerkbestandsshares

### <a name="symptom"></a>Symptoom

Hallo VPN-client is verbonden toohello virtuele Azure-netwerk. Hallo-client kan echter netwerkshares niet openen.

### <a name="cause"></a>Oorzaak

Hallo SMB-protocol wordt gebruikt voor bestandsshare-toegang. Wanneer het Hallo-verbinding is geïnitieerd en Hallo VPN-client wordt Hallo sessie referenties en Hallo-fout optreedt. Nadat het Hallo-verbinding tot stand is gebracht, geforceerd Hallo client toouse Hallo cache referenties voor Kerberos-verificatie. Dit proces initieert query's toohello Key Distribution Center (domeincontroller) tooget een token. Omdat Hallo client verbinding vanaf Internet hello maakt, mogelijk kunnen tooreach Hallo domeincontroller niet meer. Daarom kan Hallo-client niet worden overgenomen van Kerberos tooNTLM. 

Hallo alleen tijd die Hallo-client is gevraagd om een referentie is wanneer er een geldig certificaat (met SAN = UPN) uitgegeven door Hallo domein toowhich deze is gekoppeld. Hallo-client ook moet fysiek gekoppeld toohello domeinnetwerk. In dit geval Hallo client probeert toouse Hallo certificaat en gezocht toohello-domeincontroller. Hallo Key Distribution Center wordt vervolgens een 'KDC_ERR_C_PRINCIPAL_UNKNOWN'-fout geretourneerd. Hallo-client is gedwongen toofail via tooNTLM. 

### <a name="solution"></a>Oplossing

toowork rond Hallo-probleem uitschakelen Hallo opslaan in cache van de domeinreferenties van Hallo volgende registersubsleutel: 

    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\DisableDomainCreds - Set hello value too1 


## <a name="cannot-find-hello-point-to-site-vpn-connection-in-windows-after-reinstalling-hello-vpn-client"></a>Hallo punt-naar-site VPN-verbinding kan niet zoeken in Windows nadat Hallo VPN-client opnieuw is geïnstalleerd

### <a name="symptom"></a>Symptoom

U Hallo punt-naar-site VPN-verbinding verwijderen en opnieuw installeren Hallo VPN-client. In dit geval is Hallo VPN-verbinding niet correct geconfigureerd. U ziet geen Hallo VPN-verbinding in Hallo **netwerkverbindingen** instellingen in Windows.

### <a name="solution"></a>Oplossing

tooresolve hello probleem verwijderen Hallo oude VPN-client configuratiebestanden uit **C:\Users\TheUserName\AppData\Roaming\Microsoft\Network\Connections**, en voer het installatieprogramma Hallo VPN-client vervolgens opnieuw.

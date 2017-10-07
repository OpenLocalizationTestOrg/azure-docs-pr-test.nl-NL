---
title: aaaSet van webproxy voor een StorSimple-apparaat | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell voor StorSimple tooconfigure web proxy-instellingen voor uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 6c2ca351-a7c6-4da6-ab5e-c081e6d08261
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: c0213eb2a1902ff994147bb16593f0ff300eb70c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-proxy-for-your-storsimple-device"></a>Webproxy voor uw StorSimple-apparaat configureren
## <a name="overview"></a>Overzicht
Deze zelfstudie wordt beschreven hoe toouse Windows PowerShell voor StorSimple tooconfigure en weergave web proxy-instellingen voor uw StorSimple-apparaat. Hallo web proxy-instellingen worden gebruikt door Hallo StorSimple-apparaat om te communiceren met de Hallo cloud. Een webproxyserver gebruikt tooadd wordt nog een beveiligingslaag, inhoud filteren, tooease bandbreedtevereisten in de cache of zelfs helpen met analytics.

Webproxy is een optionele configuratie voor uw StorSimple-apparaat. U kunt de webproxy alleen via Windows PowerShell voor StorSimple. Hallo-configuratie is een proces als volgt:

1. U web proxy-instellingen via de wizard setup Hallo of Windows PowerShell voor StorSimple-cmdlets voor het eerst configureren.
2. U activeert u Hallo geconfigureerd web proxy-instellingen via Windows PowerShell voor StorSimple-cmdlets.

Nadat Hallo webproxyconfiguratie voltooid is, kunt u Hallo geconfigureerd web proxy-instellingen weergeven in Hallo Microsoft Azure StorSimple Manager-service en Hallo Windows PowerShell voor StorSimple. 

Na het lezen van deze zelfstudie, kunt u zich kunt:

* Webproxy configureren met behulp van cmdlets en de wizard setup
* Webproxy inschakelen met behulp van cmdlets
* Web proxy-instellingen in de klassieke Azure-portal Hallo weergeven
* Fouten tijdens de webproxyconfiguratie oplossen

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple"></a>Configureren van webproxy via Windows PowerShell voor StorSimple
U gebruikt een van de Hallo tooconfigure web proxy-instellingen te volgen:

* Setup-wizard tooguide u via Hallo configuratiestappen.
* Cmdlets in Windows PowerShell voor StorSimple.

Elk van deze methoden wordt besproken in Hallo uit te voeren.

## <a name="configure-web-proxy-via-hello-setup-wizard"></a>Webproxy via de wizard setup Hallo configureren
Hallo setup wizard tooguide die u via Hallo stappen kunt u voor de configuratie van uw webproxy. Hallo stappen tooconfigure webproxy volgen op uw apparaat uitvoeren.

#### <a name="tooconfigure-web-proxy-via-hello-setup-wizard"></a>de webproxy tooconfigure via Hallo-installatiewizard
1. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang** en geef Hallo **wachtwoord apparaatbeheerder**. Type Hallo volgende opdracht toostart een sessie voor setup-wizard:
   
    `Invoke-HcsSetupWizard`
2. Als dit Hallo eerste keer dat u de wizard setup Hallo voor apparaatregistratie hebt gebruikt, moet u tooconfigure netwerkinstellingen voor alle Hallo vereist totdat u de webproxyconfiguratie Hallo. Als uw apparaat al is geregistreerd, kunt u alle Hallo geconfigureerd netwerkinstellingen totdat u de webproxyconfiguratie Hallo accepteren. In de installatiewizard Hallo wanneer na vragen aan gebruiker tooconfigure web proxy-instellingen, typt u **Ja**.
3. Voor Hallo **Web Proxy-URL**, Hallo IP-adres opgeven of de volledig gekwalificeerde domeinnaam (FQDN) van uw web proxy-server en Hallo TCP-poortnummer dat u de toouse van uw apparaat wilt om te communiceren met de cloud Hallo Hallo. Gebruik Hallo volgende indeling:
   
    `http://<IP address or FQDN of hello web proxy server>:<TCP port number>`
   
    Standaard is TCP-poortnummer 8080 opgegeven.
4. Kies Hallo verificatietype als **NTLM**, **Basic**, of **geen**. Basic is de minst veilige verificatie Hallo voor Hallo proxyserverconfiguratie. NT LAN Manager (NTLM) is een zeer veilige en complexe verificatieprotocol die gebruikmaakt van een drievoudige berichtensysteem (soms vier als extra integriteit vereist is) tooauthenticate een gebruiker. Hallo standaardverificatie is NTLM. Zie voor meer informatie [Basic](http://hc.apache.org/httpclient-3.x/authentication.html) en [NTLM-verificatie](http://hc.apache.org/httpclient-3.x/authentication.html). 
   
   > [!IMPORTANT]
   > **In Hallo StorSimple Manager-service, Hallo apparaat bewaking grafieken werken niet als basis of NTLM-verificatie is ingeschakeld in Hallo proxyserver-configuratie voor Hallo-apparaat. Voor Hallo grafieken toowork bewaking, moet u tooensure dat verificatie tooNONE is ingesteld.**
   > 
   > 
5. Als u verificatie gebruikt, geeft u een **Web Proxy Username** en een **Web Proxywachtwoord**. U moet ook tooconfirm Hallo wachtwoord.
   
    ![Webproxy configureren op StorSimple Device1](./media/storsimple-configure-web-proxy/IC751830.png)

Als u uw apparaat op Hallo eerst registreert, kunt u doorgaan met Hallo inschrijving. Als uw apparaat is al geregistreerd, wordt Hallo wizard afgesloten. Hallo geconfigureerd instellingen worden opgeslagen.

Webproxy nu ook ingeschakeld. U kunt doorgaan Hallo [webproxy inschakelen](#enable-web-proxy) stap en gaat u rechtstreeks te[web proxy-instellingen weergeven in de klassieke Azure-portal Hallo](#view-web-proxy-settings-in-the-azure-classic-portal).

## <a name="configure-web-proxy-via-windows-powershell-for-storsimple-cmdlets"></a>Configureren van webproxy via Windows PowerShell voor StorSimple-cmdlets
Er is een andere manier tooconfigure web proxy-instellingen via Hallo Windows PowerShell voor StorSimple-cmdlets. Volgende stappen tooconfigure webproxy Hallo uitvoeren.

#### <a name="tooconfigure-web-proxy-via-cmdlets"></a>de webproxy tooconfigure via cmdlets
1. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**. Geef desgevraagd Hallo **wachtwoord apparaatbeheerder**. Hallo standaardwachtwoord is `Password1`.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Set-HcsWebProxy -Authentication NTLM -ConnectionURI "<http://<IP address or FQDN of web proxy server>:<TCP port number>" -Username "<Username for web proxy server>"`
   
    Geef en Bevestig het wachtwoord Hallo wanneer u wordt gevraagd, zoals hieronder wordt weergegeven.
   
    ![Webproxy configureren op StorSimple Device3](./media/storsimple-configure-web-proxy/IC751831.png)

Hallo webproxy is nu geconfigureerd en moet toobe ingeschakeld.

## <a name="enable-web-proxy"></a>Webproxy inschakelen
Webproxy is standaard uitgeschakeld. Nadat u Hallo web proxy-instellingen op uw StorSimple-apparaat configureert, moet u toouse Hallo Windows PowerShell voor StorSimple tooenable Hallo web proxy-instellingen.

> [!NOTE]
> **Deze stap wordt niet vereist als u Hallo setup wizard tooconfigure webproxy gebruikt. Webproxy is na een sessie van de wizard setup standaard automatisch ingeschakeld.**
> 
> 

Voer Hallo stappen te volgen in Windows PowerShell voor StorSimple tooenable webproxy op uw apparaat:

#### <a name="tooenable-web-proxy"></a>tooenable webproxy
1. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**. Geef desgevraagd Hallo **wachtwoord apparaatbeheerder**. Hallo standaardwachtwoord is `Password1`.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Enable-HcsWebProxy`
   
    U hebt nu de webproxyconfiguratie Hallo ingeschakeld op uw StorSimple-apparaat.
   
    ![Webproxy configureren op StorSimple Device4](./media/storsimple-configure-web-proxy/IC751832.png)

## <a name="view-web-proxy-settings-in-hello-azure-classic-portal"></a>Web proxy-instellingen in de klassieke Azure-portal Hallo weergeven
Hallo web proxy-instellingen worden geconfigureerd via Windows PowerShell-interface Hallo en kunnen niet worden gewijzigd in de klassieke portal Hallo. U kunt echter deze geconfigureerde instellingen bekijken in de klassieke portal Hallo. Volgende stappen tooview webproxy Hallo uitvoeren.

#### <a name="tooview-web-proxy-settings"></a>tooview web proxy-instellingen
1. Navigeer te**StorSimple Manager-service > apparaten**. Selecteer en klik op een apparaat en ga vervolgens te**configureren**.
2. Schuif vervolgens omlaag op Hallo **configureren** pagina te**Web proxy-instellingen** sectie. U kunt Hallo geconfigureerd web proxy-instellingen op uw StorSimple-apparaat weergeven zoals hieronder wordt weergegeven.
   
    ![De webproxy weergeven in de beheerportal](./media/storsimple-configure-web-proxy/ViewWebProxyPortal_M.png)

## <a name="errors-during-web-proxy-configuration"></a>Fouten tijdens de webproxyconfiguratie
Als Hallo web proxy-instellingen niet juist zijn geconfigureerd, worden foutberichten weergegeven toohello gebruiker in Windows PowerShell voor StorSimple. Hallo volgende tabel worden enkele van deze foutberichten, hun mogelijke oorzaken en aanbevolen acties.

| Serienummer. | Fout HRESULT Code | Mogelijke hoofdoorzaken | Aanbevolen actie |
|:--- |:--- |:--- |:--- |
| 1. |0x80070001 |De opdracht wordt uitgevoerd vanaf een passieve Hallo-controller en is niet kunnen toocommunicate met Hallo actieve controller. |Hallo-opdracht uitvoeren op Hallo actieve controller. toorun hello opdracht vanaf een passieve Hallo-controller, moet u toofix Hallo connectiviteit vanuit passieve tooactive controller. U moet Microsoft Support tooengage als deze de verbinding verbroken is. |
| 2. |0x800710dd - Hallo bewerkings-id is niet geldig |Proxy-instellingen worden niet ondersteund op virtuele StorSimple-apparaat. |Proxy-instellingen worden niet ondersteund op virtuele StorSimple-apparaat. Deze kunnen alleen worden geconfigureerd op een fysieke StorSimple-apparaat. |
| 3. |0x80070057 - ongeldige parameter |Een van de Hallo opgegeven parameters voor Hallo proxy-instellingen is niet geldig. |Hallo-URI is niet opgegeven in de juiste indeling. Gebruik Hallo volgende indeling:`http://<IP address or FQDN of hello web proxy server>:<TCP port number>` |
| 4. |0x800706ba - RPC-server niet beschikbaar |Hallo hoofdoorzaak is een van de volgende Hallo:</br></br>Cluster is niet actief.</br></br>Gegevenspad-service wordt niet uitgevoerd.</br></br>Hallo-opdracht wordt uitgevoerd vanaf een passieve controller en is niet kunnen toocommunicate met Hallo actieve controller. |Neem uitoefenen Microsoft Support-tooensure die Hallo cluster is en gegevenspad-service wordt uitgevoerd.</br></br>Hallo-opdracht uitvoeren vanaf de actieve controller Hallo. Als u wilt dat toorun Hallo opdracht vanaf een passieve Hallo-controller, moet u tooensure Hallo passieve domeincontroller kan communiceren met de Hallo actieve controller. U moet Microsoft Support tooengage als deze de verbinding verbroken is. |
| 5. |0x800706be - RPC-aanroep is mislukt |Cluster is niet actief. |Neem benaderen Microsoft Support tooensure die Hallo cluster actief is. |
| 6. |0x8007138f - clusterbron is niet gevonden |Clusterbron voor platform-service is niet gevonden. Dit kan gebeuren wanneer het Hallo-installatie is niet correct. |Mogelijk moet u tooperform fabrieksinstellingen op uw apparaat. Mogelijk moet u een resource platform toocreate. Neem contact op met Microsoft Support voor volgende stappen. |
| 7. |0x8007138c - cluster-bron niet online |Platform of gegevenspad clusterbronnen zijn niet online. |Neem contact op met Microsoft Support toohelp Zorg ervoor dat Hallo gegevenspad en platform servicebron online zijn. |

> [!NOTE]
> * Hallo boven lijst van foutberichten is niet volledig. 
> * Fouten gerelateerd tooweb proxy-instellingen worden niet weergegeven in de klassieke Azure-portal in uw StorSimple Manager-service Hallo. Als er een probleem met de webproxy wanneer Hallo-configuratie is voltooid, Hallo Apparaatstatus te verandert**Offline** in de klassieke portal Hallo. |
> 
> 

## <a name="next-steps"></a>Volgende stappen
* Als u problemen ondervindt tijdens het implementeren van uw apparaat of web proxy-instellingen configureren, raadpleegt u te[uw StorSimple-apparaat-implementatie oplossen](storsimple-troubleshoot-deployment.md).
* hoe toouse hello StorSimple Manager-service, gaan te toolearn[gebruik Hallo StorSimple Manager service tooadminister uw StorSimple-apparaat](storsimple-manager-service-administration.md).


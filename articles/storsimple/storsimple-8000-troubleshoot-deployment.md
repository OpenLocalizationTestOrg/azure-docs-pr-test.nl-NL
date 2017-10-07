---
title: aaaTroubleshoot StorSimple 8000 series implementatieproblemen | Microsoft Docs
description: Hierin wordt beschreven hoe toodiagnose en los fouten die optreden bij het implementeren van StorSimple.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: a55a4b277c8afe25f1d5a43ab8d7a90436123410
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>StorSimple-apparaat implementatieproblemen oplossen
## <a name="overview"></a>Overzicht
Dit artikel bevat nuttige richtlijnen voor probleemoplossing voor uw Microsoft Azure StorSimple-implementatie. Hierin worden veelvoorkomende problemen, mogelijke oorzaken en aanbevolen stappen toohelp oplossen van problemen die u ervaren kunt wanneer u StorSimple configureert. 

Deze informatie is van toepassing tooboth hello StorSimple 8000 series fysieke apparaat en Hallo StorSimple Cloud toestel.

> [!NOTE]
> Apparaat configuratie gerelateerde problemen die u mogelijk geconfronteerd kunnen optreden wanneer u eerst Hallo-apparaat voor Hallo implementeren of ze later optreden kunnen wanneer Hallo apparaat operationeel is. In dit artikel gaat over het oplossen van problemen bij de eerste implementatie. een operationele apparaat tootroubleshoot te gaan[gebruik Hallo diagnostische hulpprogramma tootroubleshoot een operationele apparaat](storsimple-8000-diagnostics.md).

Dit artikel wordt ook beschrijft Hallo-hulpprogramma's voor het oplossen van StorSimple-implementaties en biedt een voorbeeld van stapsgewijze probleemoplossing.

## <a name="first-time-deployment-issues"></a>Problemen bij de eerste implementatie
Als u een probleem bij het implementeren van uw apparaat op Hallo eerst, houd rekening met de volgende Hallo:

* Als u een fysiek apparaat oplossen wilt, zorg er dan Hallo hardware is geïnstalleerd en geconfigureerd zoals beschreven in [uw StorSimple 8100-apparaat installeert](storsimple-8100-hardware-installation.md) of [installeren van uw StorSimple 8600-apparaat](storsimple-8600-hardware-installation.md).
* Controleer de vereisten voor de implementatie. Zorg ervoor dat u alle Hallo informatie die wordt beschreven in Hallo hebt [Configuratiecontrolelijst voor implementatie](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist).
* Raadpleeg Hallo releaseopmerkingen StorSimple toosee als Hallo probleem wordt beschreven. Hallo release-opmerkingen bevatten oplossingen voor bekende installatieproblemen. 

Hallo meest voorkomende problemen die gebruikers face optreden tijdens de implementatie van het apparaat, wanneer ze de wizard setup Hallo uitgevoerd en wanneer ze zich hebt geregistreerd Hallo apparaat via Windows PowerShell voor StorSimple. (U Windows PowerShell voor StorSimple tooregister en configureren van uw StorSimple-apparaat. Zie voor meer informatie over apparaatregistratie [stap 3: configureren en registreren van uw apparaat via Windows PowerShell voor StorSimple](storsimple-8000-deployment-walkthrough-u2.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple)).

Hallo uit te voeren kunt u problemen oplossen die u tegenkomt wanneer u eerst Hallo StorSimple-apparaat voor Hallo configureert.

## <a name="first-time-setup-wizard-process"></a>Wizard installatieproces eerst
Hallo stappen geven een overzicht van Hallo setup-wizard proces. Zie voor gedetailleerde informatie, [uw on-premises StorSimple-apparaat implementeren](storsimple-8000-deployment-walkthrough-u2.md).

1. Voer Hallo [Invoke-HcsSetupWizard](https://technet.microsoft.com/library/dn688135.aspx) cmdlet toostart Hallo installatiewizard die u zal begeleiden bij Hallo resterende stappen. 
2. Hallo netwerk configureren: Hallo-installatiewizard kunt u netwerkinstellingen voor Hallo DATA 0-netwerkinterface op uw StorSimple-apparaat configureren. Deze instellingen zijn Hallo volgende:
   * Virtuele IP-adres (VIP), subnetmasker en gateway – Hallo [Set HcsNetInterface](https://technet.microsoft.com/library/dn688161.aspx) cmdlet wordt uitgevoerd op de achtergrond Hallo. Configureert het Hallo IP-adres, subnetmasker en gateway voor Hallo DATA 0-netwerkinterface op uw StorSimple-apparaat.
   * Primaire DNS-server – hello [Set HcsDnsClientServerAddress](https://technet.microsoft.com/library/dn688172.aspx) cmdlet wordt uitgevoerd op de achtergrond Hallo. Configureert het Hallo DNS-instellingen voor uw StorSimple-oplossing.
   * NTP-server – hello [Set HcsNtpClientServerAddress](https://technet.microsoft.com/library/dn688138.aspx) cmdlet wordt uitgevoerd op de achtergrond Hallo. Configureert het Hallo NTP-serverinstellingen voor uw StorSimple-oplossing.
   * Optionele web proxy – hello [Set HcsWebProxy](https://technet.microsoft.com/library/dn688154.aspx) cmdlet wordt uitgevoerd op de achtergrond Hallo. Het wordt ingesteld en wordt Hallo webproxyconfiguratie voor uw StorSimple-oplossing.
3. Hallo-wachtwoord instellen: Hallo volgende stap is tooset up beheerderswachtwoord Hallo-apparaat.
   wachtwoord apparaatbeheerder Hallo is gebruikte toolog op tooyour apparaat. Hallo standaardapparaatwachtwoord is **Wachtwoord1**.
        
     > [!IMPORTANT]
     > Wachtwoorden zijn vóór registratie worden verzameld, maar pas nadat u Hallo-apparaat wordt geregistreerd toegepast. Als er een fout tooapply een wachtwoord, kunt u zich na vragen aan gebruiker toosupply Hallo wachtwoord opnieuw nadat de Hallo vereiste wachtwoorden (die voldoen aan de complexiteitsvereisten Hallo) worden verzameld.
     
4. Hallo-apparaat registreren: de laatste stap Hallo is tooregister Hallo apparaat met Hallo Apparaatbeheer StorSimple-service worden uitgevoerd in Microsoft Azure. Hallo-registratie moet u te[hello serviceregistratiesleutel ophalen](storsimple-8000-manage-service.md#get-the-service-registration-key) van hello Azure-portal en in de wizard setup Hallo opgeven. **Nadat het Hallo-apparaat is geregistreerd, wordt een gegevensversleutelingssleutel van service tooyou verstrekt. Zorg ervoor dat deze versleuteling sleutel op een veilige locatie omdat het is mogelijk tookeep vereist tooregister alle latere apparaten met Hallo-service.**

## <a name="common-errors-during-device-deployment"></a>Veelvoorkomende fouten tijdens de implementatie van het apparaat
Hallo volgende tabellen lijst Hallo algemene fouten die wanneer optreden mogelijk u:

* Netwerkinstellingen Hallo vereist.
* Hallo optionele web proxy-instellingen configureren.
* Hallo apparaat administrator-wachtwoord instellen.
* Hallo-apparaat registreren.

## <a name="errors-during-hello-required-network-settings"></a>Fouten tijdens het Hallo netwerkinstellingen vereist
| Nee. | Foutbericht | Mogelijke oorzaken | Aanbevolen actie |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Met deze opdracht kan alleen worden uitgevoerd op Hallo actieve controller. |Configuratie werd uitgevoerd op Hallo passieve domeincontroller. |Deze opdracht uitvoert vanaf de actieve controller Hallo. Zie voor meer informatie [een actieve domeincontroller op uw apparaat identificeren](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device). |
| 2 |Invoke-HcsSetupWizard: Apparaat niet gereed. |Er zijn problemen met de netwerkverbinding Hallo op DATA 0. |Controleer de fysieke netwerkverbinding Hallo op DATA 0. |
| 3 |Invoke-HcsSetupWizard: Er is een IP-adresconflict met een ander systeem op Hallo-netwerk (uitzondering van HRESULT: 0x80070263). |Hallo IP opgegeven voor de DATA 0 is al in gebruik door een ander systeem. |Geef een nieuwe IP-adres dat niet wordt gebruikt. |
| 4 |Invoke-HcsSetupWizard: Een cluster-bron is mislukt. (Uitzondering van HRESULT: 0x800713AE). |Dubbele VIP. Hallo opgegeven IP is al in gebruik. |Geef een nieuwe IP-adres dat niet wordt gebruikt. |
| 5 |Invoke-HcsSetupWizard: Ongeldig IPv4-adres. |Hallo IP-adres is opgegeven in een onjuiste indeling. |Controleer de indeling Hallo en geef uw IP-adres opnieuw. Zie voor meer informatie [IPv4-adressering][1]. |
| 6 |Invoke-HcsSetupWizard: Ongeldig IPv6-adres. |Hallo IP-adres is opgegeven in een onjuiste indeling. |Controleer de indeling Hallo en geef uw IP-adres opnieuw. Zie voor meer informatie [IPv6-adressering][2]. |
| 7 |Invoke-HcsSetupWizard: Er zijn geen eindpunten meer beschikbaar is via eindpunttoewijzer Hallo. (Uitzondering van HRESULT: 0x800706D9) |Hallo clusterfunctionaliteit werkt niet. |[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor volgende stappen. |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Fouten tijdens het Hallo optionele web proxy-instellingen
| Nee. | Foutbericht | Mogelijke oorzaken | Aanbevolen actie |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard: Ongeldige parameter (uitzondering van HRESULT: 0x80070057) |Een van de Hallo opgegeven parameters voor Hallo proxy-instellingen is niet geldig. |Hallo-URI is niet opgegeven in de juiste indeling Hallo. Gebruik Hallo volgende indeling: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard: RPC-server niet beschikbaar (uitzondering van HRESULT: 0x800706ba) |Hallo hoofdoorzaak is een van de volgende Hallo:<ol><li>Hallo-cluster is niet actief.</li><li>Hallo passieve controller kan niet communiceren met de actieve controller Hallo en Hallo-opdracht wordt uitgevoerd vanaf een passieve-controller.</li></ol> |Afhankelijk van de hoofdoorzaak Hallo:<ol><li>[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake ervoor dat cluster Hallo actief is.</li><li>Hallo-opdracht uitvoeren vanaf de actieve controller Hallo. Als u wilt dat toorun Hallo opdracht vanaf een passieve Hallo-controller, moet u tooensure Hallo passieve controller kan communiceren met de Hallo actieve controller. U moet te[contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) als deze de verbinding verbroken is.</li></ol> |
| 3 |Invoke-HcsSetupWizard: RPC-aanroep is mislukt (uitzondering van HRESULT: 0x800706be) |Cluster is niet actief. |[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) toomake ervoor dat cluster Hallo actief is. |
| 4 |Invoke-HcsSetupWizard: Clusterbron niet vinden (uitzondering van HRESULT: 0x8007138f) |Hallo-clusterbron is niet gevonden. Dit kan gebeuren wanneer het Hallo-installatie niet juist is. |U moet mogelijk de fabrieksinstellingen van tooreset Hallo apparaat toohello. [Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) toocreate clusterbron. |
| 5 |Invoke-HcsSetupWizard: Clusterbron niet online (uitzondering van HRESULT: 0x8007138c) |Clusterresources zijn niet online. |[Neem contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor volgende stappen. |

## <a name="errors-related-toodevice-administrator-password"></a>Fouten gerelateerd toodevice administrator-wachtwoord
Hallo beheerder standaardapparaatwachtwoord is **Wachtwoord1**. Dit wachtwoord verloopt na de eerste aanmelding Hallo; Daarom moet u toouse Hallo setup wizard toochange deze. U moet een nieuw apparaat beheerderswachtwoord opgeven wanneer u Hallo apparaat voor Hallo eerst registreren. 

Zorg ervoor dat uw wachtwoorden Hallo volgens de vereisten voldoen:

* Het beheerderswachtwoord van uw apparaat moet tussen 8 en 15 tekens lang zijn.
* Wachtwoorden moeten 3 Hallo 4 tekentypen volgende bevatten: kleine letters, hoofdletters, numerieke en speciale. 
* Uw wachtwoord kan niet hetzelfde zijn als de laatste 24 wachtwoorden Hallo Hallo.

Bovendien Houd er rekening mee dat wachtwoorden elk jaar verlopen en kunnen pas worden gewijzigd nadat u Hallo-apparaat wordt geregistreerd. Als het Hallo-registratie voor een of andere reden mislukt, wordt Hallo wachtwoorden worden niet gewijzigd.

Voor meer informatie over het beheerderswachtwoord apparaat gaat te[gebruik Hallo StorSimple Apparaatbeheer service toochange uw wachtwoord StorSimple](storsimple-8000-change-passwords.md).

Een of meer van de volgende fouten bij het instellen van Hallo apparaatbeheerder en StorSimple Snapshot Manager wachtwoorden Hallo kunnen optreden.

| Nee. | Foutbericht | Aanbevolen actie |
| --- | --- | --- |
| 1 |Hallo wachtwoord overschrijdt de maximale lengte Hallo. |Het beheerderswachtwoord van uw apparaat moet tussen 8 en 15 tekens lang zijn. |
| 2 |Hallo wachtwoord voldoet niet aan Hallo vereiste lengte. |Het beheerderswachtwoord van uw apparaat moet tussen 8 en 15 tekens lang zijn.|
| 3 |Hallo-wachtwoord moet letters bevatten. |Wachtwoorden moeten 3 Hallo 4 tekentypen volgende bevatten: kleine letters, hoofdletters, numerieke en speciale. Zorg ervoor dat uw wachtwoord voldoet aan deze vereisten. |
| 4 |Hallo-wachtwoord moet tekens bevatten. |Wachtwoorden moeten 3 Hallo 4 tekentypen volgende bevatten: kleine letters, hoofdletters, numerieke en speciale. Zorg ervoor dat uw wachtwoord voldoet aan deze vereisten. |
| 5 |Hallo-wachtwoord moet tekens bevatten. |Wachtwoorden moeten 3 Hallo 4 tekentypen volgende bevatten: kleine letters, hoofdletters, numerieke en speciale. Zorg ervoor dat uw wachtwoord voldoet aan deze vereisten. |
| 6 |Hallo wachtwoord moet bevatten 3 van de volgende 4 tekentypen Hallo: hoofdletters, kleine letters, numerieke en speciale. |Uw wachtwoord bevat geen vereist Hallo soorten tekens. Zorg ervoor dat uw wachtwoord voldoet aan deze vereisten. |
| 7 |Parameter komt niet overeen met de bevestiging. |Zorg ervoor dat uw wachtwoord voldoet aan alle vereisten en dat u deze correct ingevoerd. |
| 8 |Uw wachtwoord mag niet overeenkomen met de Hallo standaard. |is het standaardwachtwoord Hallo *Wachtwoord1*. U moet toochange dit wachtwoord nadat u zich aanmeldt voor Hallo eerst. |
| 9 |Hallo wachtwoord dat u hebt ingevoerd komt niet overeen met de Hallo apparaatwachtwoord. Geef Hallo wachtwoord. |Hallo-wachtwoord en typt u het opnieuw. |

Wachtwoorden worden verzameld voordat Hallo-apparaat is geregistreerd, maar alleen na een succesvolle registratie toegepast. Hallo wachtwoord herstelwerkstroom moet Hallo apparaat toobe geregistreerd.

> [!IMPORTANT]
> In het algemeen als een tooapply poging mislukt een wachtwoord, en vervolgens Hallo software herhaaldelijk toocollect Hallo wachtwoord probeert totdat hij erin slaagt. In zeldzame gevallen kan niet Hallo wachtwoord worden toegepast. In dit geval kunt u Hallo-apparaat registreren en doorgaan, maar Hallo wachtwoorden worden niet gewijzigd. U kunt wachtwoord apparaatbeheerder Hallo wijzigen na de registratie van Hallo van hello Azure-portal.


U kunt Hallo-wachtwoord in hello Azure-portal via Hallo Apparaatbeheer StorSimple-service opnieuw instellen. Voor meer informatie gaat te[wijzigen wachtwoord apparaatbeheerder hello](storsimple-8000-change-passwords.md#change-the-device-administrator-password).

## <a name="errors-during-device-registration"></a>Fouten tijdens het registreren van apparaten
U Hallo Apparaatbeheer StorSimple-service die wordt uitgevoerd in Microsoft Azure tooregister Hallo apparaat gebruiken. Er kan een of meer van problemen tijdens de apparaatregistratie na Hallo optreden.

| Nee. | Foutbericht | Mogelijke oorzaken | Aanbevolen actie |
| --- | --- | --- | --- |
| 1 |Fout 350027: Kan tooregister Hallo apparaat Hello StorSimple Apparaatbeheer. | |Wacht een paar minuten en probeer Hallo opnieuw. Als Hallo probleem blijft bestaan, [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md). |
| 2 |Fout 350013: Een fout opgetreden bij het Hallo-apparaat registreren. Dit kan zijn vanwege de serviceregistratiesleutel tooincorrect. | |Registreer Hallo-apparaat opnieuw met de juiste serviceregistratiesleutel Hallo. Zie voor meer informatie [Get Hallo serviceregistratiesleutel.](storsimple-8000-manage-service.md#get-the-service-registration-key) |
| 3 |Fout 350063: Verificatie tooStorSimple Apparaatbeheer service doorgegeven, maar de registratie is mislukt. Probeer de bewerking Hallo na enige tijd opnieuw. |Deze fout geeft aan dat verificatie met ACS is verstreken maar Hallo registreren aanroep toohello is mislukt. Dit kan zijn veroorzaakt door een storing sporadisch netwerk. |Als Hallo probleem zich blijft, neem voordoen [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md). |
| 4 |Fout 350049: Hallo-service kan niet worden bereikt tijdens de registratie. |Wanneer hello wordt aanroep toohello service een Webuitzondering ontvangen. In sommige gevallen kan ophalen dit opgelost door het Hallo-bewerking later opnieuw proberen. |Controleer uw IP-adres en DNS-naam en probeer vervolgens opnieuw Hallo. Als Hallo probleem blijft bestaan, [contact op met Microsoft Support.](storsimple-8000-contact-microsoft-support.md) |
| 5 |Fout 350031: Hallo-apparaat is al geregistreerd. | |Er is geen actie nodig. |
| 6 |Fout 350016: Apparaatregistratie is mislukt. | |Controleer of de registratiesleutel Hallo juist is. |
| 7 |Invoke-HcsSetupWizard: Is een fout opgetreden tijdens het registreren van uw apparaat; Dit kan zijn vanwege tooincorrect IP-adres of de DNS-naam. Controleer de netwerkinstellingen en probeer het opnieuw. Als Hallo probleem blijft bestaan, [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md). (Fout 350050) |Zorg ervoor dat uw apparaat Hallo buiten netwerk kan pingen. Als u geen netwerkverbinding toooutside netwerk, mislukken Hallo registratie bij deze fout. Deze fout wordt mogelijk een combinatie van een of meer van de volgende Hallo:<ul><li>Onjuiste IP</li><li>Onjuiste subnet</li><li>Onjuiste gateway</li><li>Onjuiste DNS-instellingen</li></ul> |Zie Hallo stappen voor het Hallo [voorbeeld van stapsgewijze probleemoplossing](#step-by-step-storsimple-troubleshooting-example). |
| 8 |Invoke-HcsSetupWizard: Hallo huidige bewerking is mislukt vanwege een interne servicefout tooan [0x1FBE2]. Probeer de bewerking hello later opnieuw. Als Hallo probleem zich blijft voordoen, neem contact op met Microsoft Support. |Dit is een algemene fout gegenereerd voor alle gebruikers onzichtbaar fouten vanuit de service of -agent. Hallo meest voorkomende reden kan zijn dat Hallo ACS-verificatie is mislukt. Een mogelijke oorzaak van het Hallo-probleem is dat er problemen met configuratie Hallo NTP-server zijn en tijd op Hallo-apparaat is niet juist ingesteld. |Juiste Hallo-tijd (als er problemen zijn) en probeer vervolgens de bewerking voor de registratie Hallo. Als u Hallo Set HcsSystem - tijdzone opdracht tooadjust Hallo-tijdzone, beginhoofdletter in Hallo tijdzone (bijvoorbeeld "Pacific (standaardtijd)").  Als dit probleem zich blijft voordoen, [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor volgende stappen. |
| 9 |Waarschuwing: Kan apparaat Hallo niet activeren. De apparaatbeheerder van uw en StorSimple Snapshot Manager wachtwoorden zijn niet gewijzigd. |Als Hallo-registratie mislukt, worden de apparaatbeheerder hello en StorSimple Snapshot Manager wachtwoorden worden niet gewijzigd. | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>Hulpprogramma's voor probleemoplossing StorSimple-implementaties
StorSimple bevat verschillende hulpprogramma's waarmee u tootroubleshoot uw StorSimple-oplossing kunt. Deze omvatten:

* Ondersteuning voor pakketten en apparaatlogboeken.
* De cmdlets is speciaal ontworpen voor het oplossen van problemen.

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>Ondersteuning voor pakketten en apparaatlogboeken beschikbaar voor het oplossen van problemen
Een ondersteuningspakket bevat alle Hallo relevante logboeken die Hallo Microsoft Support team helpen kunnen met problemen met het apparaat. U kunt Windows PowerShell voor StorSimple toogenerate een versleutelde ondersteuningspakket die u vervolgens met iemand van ondersteuning delen kunt.

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>tooview hello Logboeken of de inhoud van de Hallo Hallo ondersteuningspakket
1. Gebruik Windows PowerShell voor StorSimple toogenerate ondersteuningspakket zoals beschreven in [maken en beheren van een ondersteuningspakket](storsimple-8000-create-manage-support-package.md).
2. Hallo downloaden [ontsleuteling script](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65) lokaal op de clientcomputer.
3. Gebruik deze [stapsgewijze procedure](storsimple-8000-create-manage-support-package.md#edit-a-support-package) tooopen en ontsleutelen Hallo support-pakket.
4. Hallo ontsleuteld ondersteuningspakket logboeken etw/etvx-indeling zijn. U kunt op deze bestanden Hallo tooview stappen te volgen uitvoeren in Windows Logboeken:
   
   1. Voer Hallo **eventvwr** opdracht op uw Windows-client. Hiermee start u Hallo Logboeken.
   2. In Hallo **acties** deelvenster, klikt u op **opgeslagen logboek openen** en logboekbestanden punt toohello etvx/etw-indeling (Hallo ondersteuningspakket). U kunt nu Hallo-bestand weergeven. Nadat u Hallo bestand opent, kunt u met de rechtermuisknop op en Hallo bestand opslaan als tekst.
      
      > [!IMPORTANT]
      > U kunt ook Hallo **Get-WinEvent** cmdlet tooopen deze bestanden in Windows PowerShell. Zie voor meer informatie [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx) in Windows PowerShell-cmdlet-naslagdocumentatie Hallo.
     
5. Wanneer het Hallo-Logboeken openen in Logboeken, zoeken Hallo logboeken met problemen gerelateerde toohello apparaatconfiguratie te volgen:
   
   * hcs_pfconfig/operationeel logboek
   * hcs_pfconfig/Config
6. Zoeken naar tekenreeksen gerelateerde toohello-cmdlets aangeroepen door de wizard setup Hallo in logboekbestanden hello. Zie [eerst setup-wizard proces](#first-time-setup-wizard-process) voor een lijst van deze cmdlets.
7. Als u niet kunt toofigure Hallo oorzaak van Hallo probleem bent, kunt u [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor volgende stappen. Gebruik Hallo stappen in [Maak een ondersteuningsaanvraag](storsimple-8000-contact-microsoft-support.md#create-a-support-request) wanneer u contact op met Microsoft Support voor hulp.

## <a name="cmdlets-available-for-troubleshooting"></a>Cmdlets beschikbaar voor het oplossen van problemen
Gebruik hello volgende Windows PowerShell-cmdlets toodetect connectiviteitsfouten.

* `Get-NetAdapter`: Gebruik deze cmdlet toodetect Hallo health van netwerkinterfaces.
* `Test-Connection`: Gebruik deze cmdlet toocheck Hallo netwerkverbinding binnen en buiten Hallo-netwerk.
* `Test-HcsmConnection`: Gebruik deze cmdlet toocheck Hallo connectiviteit van een apparaat is geregistreerd.
* `Sync-HcsTime`: Gebruik deze cmdlet toodisplay tijd op het apparaat en een tijdsynchronisatie met Hallo NTP-server afdwingen.
* `Enable-HcsPing`en `Disable-HcsPing`: deze netwerkinterfaces van cmdlets tooallow Hallo hosts tooping Hallo op uw StorSimple-apparaat gebruiken. Standaard reageren Hallo StorSimple netwerkinterfaces tooping aanvragen niet.
* `Trace-HcsRoute`: Deze cmdlet gebruiken als een hulpmiddel voor het traceren van route. Deze pakketten tooeach router verzendt op Hallo manier tooa eindbestemming gedurende een periode en vervolgens wordt berekend op basis van hello-pakketten die zijn geretourneerd door elke hop resultaten. Aangezien `Trace-HcsRoute` Hallo graad van pakketverlies op elke gewenste router of koppeling toont u kunt achterhalen welke routers of koppelingen mogelijk veroorzaakt door problemen met het netwerk.
* `Get-HcsRoutingTable`: Gebruik deze cmdlet toodisplay Hallo lokale IP-routeringstabel.

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>Problemen oplossen met Hallo Get-NetAdapter-cmdlet
Wanneer u netwerkinterfaces voor de implementatie van een apparaat eerst configureert, is hardwarestatus Hallo niet beschikbaar in Hallo Apparaatbeheer StorSimple-service UI omdat Hallo apparaat nog niet is geregistreerd met de Hallo-service. Bovendien Hallo **Hardware health** blade weerspiegelt mogelijk niet altijd goed Hallo-status van het Hallo-apparaat, vooral als er problemen met synchronisatie van de service. In deze situaties kunt u Hallo `Get-NetAdapter` cmdlet toodetermine Hallo gezondheid en status van uw netwerkinterfaces.

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>een lijst met alle Hallo netwerkadapters op uw apparaat toosee
1. Start Windows PowerShell voor StorSimple en typ vervolgens `Get-NetAdapter`. 
2. Hallo-uitvoer van hello gebruiken `Get-NetAdapter` cmdlet en Hallo volgen richtlijnen toounderstand Hallo status van de netwerkinterface.
   
   * Als het Hallo-interface is in orde en is ingeschakeld, Hallo **ifIndex** status wordt weergegeven als **Up**.
   * Als het Hallo-interface is in orde, maar niet fysiek zijn verbonden (via een netwerkkabel), Hallo **ifIndex** wordt weergegeven als **uitgeschakelde**.
   * Als het Hallo-interface is in orde, maar niet ingeschakeld, Hallo **ifIndex** status wordt weergegeven als **NotPresent**.
   * Als het Hallo-interface niet bestaat, wordt het niet weergegeven in deze lijst. Hallo Apparaatbeheer StorSimple-service gebruikersinterface worden nog steeds voor deze interface in een foutstatus.

Voor meer informatie over het toouse deze cmdlet te gaan[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) in Hallo Windows PowerShell-cmdlet-verwijzing.

Hallo volgende secties ziet u voorbeelden van uitvoer van Hallo `Get-NetAdapter` cmdlet.

 In deze voorbeelden controller 0 Hallo passieve domeincontroller is en is als volgt geconfigureerd:

* DATA 0, gegevens-1, DATA 2 en DATA 3 network interfaces beschikbaar op Hallo-apparaat waren.
* GEGEVENS 4 en 5 gegevens netwerkinterfacekaarten zijn niet aanwezig; ze zijn daarom niet vermeld in het Hallo-uitvoer.
* DATA 0 is ingeschakeld.

Controller 1 Hallo actieve controller is en is als volgt geconfigureerd:

* DATA 0, gegevens-1, DATA 2, DATA 3, 4 van de gegevens en DATA 5 network interfaces beschikbaar op Hallo-apparaat waren.
* DATA 0 is ingeschakeld.

**Voorbeelduitvoer – controller 0**

Hallo volgt Hallo-uitvoer van de controller 0 (passieve Hallo-controller). GEGEVENS-1, DATA 2 en DATA 3 zijn niet verbonden. DATA 4 en 5 van de gegevens worden niet weergegeven omdat ze niet aanwezig zijn op Hallo-apparaat.

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**Voorbeelduitvoer – controller 1**

Hallo volgt Hallo-uitvoer van de controller 1 (Hallo actieve controller). Alleen Hallo DATA 0-netwerkinterface op Hallo-apparaat is geconfigureerd en werkt.

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>Problemen oplossen met Hallo Test-Connection-cmdlet
U kunt Hallo `Test-Connection` cmdlet toodetermine of uw StorSimple-apparaat verbinding toohello buiten netwerk kan maken. Als alle Hallo netwerken parameters, waaronder Hallo DNS, juist zijn geconfigureerd in de wizard setup hello, kunt u Hallo `Test-Connection` cmdlet tooping een bekende adres buiten Hallo netwerk, zoals outlook.com.

Als ping is uitgeschakeld, moet u ping tootroubleshoot verbindingsproblemen met deze cmdlet inschakelen.

Zie de volgende voorbeelden van uitvoer uit Hallo Hallo `Test-Connection` cmdlet.

> [!NOTE]
> In de eerste voorbeeld Hallo is Hallo-apparaat geconfigureerd met een onjuiste DNS-server. In de tweede voorbeeld Hallo is Hallo DNS juist.

**Voorbeelduitvoer: onjuiste DNS**

Er wordt geen uitvoer voor Hallo IPV4 en IPV6-adressen, waarmee wordt aangegeven dat Hallo die DNS is niet omgezet in Hallo voorbeeld te volgen. Dit betekent dat er geen toohello connectiviteit buiten het netwerk en een juiste DNS-server toobe opgegeven moet.

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**Voorbeelduitvoer: de juiste DNS**

Hallo in Hallo voorbeeld te volgen, DNS-retourneert Hallo IPV4-adres, waarmee wordt aangegeven dat Hallo die DNS correct is geconfigureerd. Hiermee wordt bevestigd dat er verbinding toohello buiten het netwerk.

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>Problemen oplossen met Hallo Test-HcsmConnection cmdlet
Gebruik Hallo `Test-HcsmConnection` cmdlet voor een apparaat dat is al verbonden tooand geregistreerd bij uw StorSimple-apparaat Manager-service. Deze cmdlet kunt u controleren of de verbinding tussen een geregistreerd apparaat en de bijbehorende Apparaatbeheer StorSimple-service Hallo Hallo. U kunt deze opdracht uitvoeren op Windows PowerShell voor StorSimple.

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>toorun hello Test-HcsmConnection cmdlet
1. Zorg ervoor dat het Hallo-apparaat is geregistreerd.
2. Hallo apparaatstatus controleren. Als het Hallo-apparaat wordt gedeactiveerd, in de onderhoudsmodus of offline is, ziet u mogelijk een van de volgende fouten Hallo:
   
   * ErrorCode.CiSDeviceDecommissioned – dit geeft aan dat het Hallo-apparaat wordt gedeactiveerd.
   * ErrorCode.DeviceNotReady – dit geeft aan dat het Hallo-apparaat in de onderhoudsmodus.
   * ErrorCode.DeviceNotReady – dit geeft aan dat het Hallo-apparaat is niet online.
3. Controleer of deze Hallo StorSimple-apparaat Manager-service wordt uitgevoerd (gebruik Hallo [Get-ClusterResource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet). Als het Hallo-service niet wordt uitgevoerd, ziet u mogelijk Hallo volgende fouten:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError – dit geeft aan dat er een uitzondering opgetreden is bij het uitvoeren van Get-ClusterResource.
4. Controleer Hallo Access Control Service (ACS)-token. Als er een Webuitzondering genereert, is dit mogelijk Hallo resultaat van een probleem gateway, een ontbrekende proxyverificatie, een onjuiste DNS-server of een verificatiefout opgetreden. U ziet Hallo volgende fouten:
   
   * ErrorCode.CiSApplianceGateway – dit geeft een uitzondering HttpStatusCode.BadGateway: Hallo naam omzettingsservice Hallo hostnaam kan niet worden omgezet.
   * ErrorCode.CiSApplianceProxy – dit geeft een HttpStatusCode.ProxyAuthenticationRequired uitzondering (HTTP-statuscode 407): Hallo-client kan niet worden geverifieerd met de proxyserver Hallo.
   * ErrorCode.CiSApplianceDNSError – dit geeft een uitzondering WebExceptionStatus.NameResolutionFailure: Hallo naam omzettingsservice Hallo hostnaam kan niet worden omgezet.
   * ErrorCode.CiSApplianceACSError – dit geeft aan dat het Hallo-service heeft een verificatiefout geretourneerd, maar er verbinding is.
     
     Als deze een Webuitzondering niet genereren is, controleert u de ErrorCode.CiSApplianceFailure. Hiermee wordt aangegeven dat Hallo toestel is mislukt.
5. Controleer de Hallo cloud service-verbinding. Als het Hallo-service een Webuitzondering genereert, ziet u mogelijk Hallo volgende fouten:
   
   * ErrorCode.CiSApplianceGateway – dit geeft een uitzondering HttpStatusCode.BadGateway: een tussenliggende proxy-server heeft een ongeldige aanvraag ontvangen van een andere proxy of van de oorspronkelijke server Hallo.
   * ErrorCode.CiSApplianceProxy – dit geeft een HttpStatusCode.ProxyAuthenticationRequired uitzondering (HTTP-statuscode 407): Hallo-client kan niet worden geverifieerd met de proxyserver Hallo.
   * ErrorCode.CiSApplianceDNSError – dit geeft een uitzondering WebExceptionStatus.NameResolutionFailure: Hallo naam omzettingsservice Hallo hostnaam kan niet worden omgezet.
   * ErrorCode.CiSApplianceACSError – dit geeft aan dat het Hallo-service heeft een verificatiefout geretourneerd, maar er verbinding is.
     
     Als deze een Webuitzondering niet genereren is, controleert u de ErrorCode.CiSApplianceSaasServiceError. Dit duidt op een probleem met de Hallo StorSimple-apparaat Manager-service.
6. Controleer de Azure Service Bus-verbindingen. ErrorCode.CiSApplianceServiceBusError geeft aan dat het Hallo-apparaat kan geen verbinding maken toohello Service Bus.

Hallo logboekbestanden CiSCommandletLog0Curr.errlog en CiSAgentsvc0Curr.errlog heeft meer informatie, zoals uitzonderingsdetails.

Voor meer informatie over hoe toouse cmdlet hello, gaat u te[Test-HcsmConnection](https://technet.microsoft.com/library/dn715782.aspx) verwijzen naar de documentatie in Hallo Windows PowerShell.

> [!IMPORTANT]
> U kunt deze cmdlet voor Hallo actieve en passieve controller Hallo uitvoeren.

Zie de volgende voorbeelden van uitvoer uit Hallo Hallo `Test-HcsmConnection` cmdlet.

**Voorbeeld van uitvoer – geregistreerd apparaat waarop StorSimple Update 3**

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**Voorbeelduitvoer – offline apparaat** 

Dit voorbeeld is van een apparaat met de status van **Offline** in hello Azure-portal.

     Checking device registrationstate: Success
     Device is registered successfully
     Checking connectivity from device tooSaaS.. Failure

Hallo-apparaat kan geen verbinding maken met behulp van de huidige webproxyconfiguratie Hallo. Dit kan zijn een probleem met de webproxyconfiguratie hello of een probleem met de netwerkverbinding. In dit geval moet u ervoor dat uw proxy-instellingen juist zijn en uw webproxyservers online en bereikbaar is zijn.

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>Problemen oplossen met Hallo Sync HcsTime cmdlet
Gebruik deze cmdlet toodisplay Hallo apparaattijd. Als de tijd op het apparaat Hallo heeft een offset met Hallo NTP-server, kunt u vervolgens deze cmdlet tooforce gebruiken-Hallo tijd synchroniseren met uw NTP-server.
- Als het Hallo-offset tussen Hallo-apparaat en NTP-server is groter dan 5 minuten, ziet u een waarschuwing. 
- Als het Hallo-offset is groter dan 15 minuten, wordt Hallo apparaat offline gaat. U kunt nog steeds deze cmdlet tooforce een tijdsynchronisatie gebruiken. 
- Als het Hallo-offset is groter dan 15 uur, vervolgens u zich niet kunnen tooforce-Hallo synchronisatietijd en een foutbericht wordt weergegeven.

**Voorbeeld van uitvoer – geforceerde tijdsynchronisatie met synchronisatie HcsTime**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>Problemen oplossen met de cmdlets Enable HcsPing en schakel HcsPing Hallo
Gebruik deze cmdlets tooensure dat Hallo-netwerkinterfaces op uw apparaat tooICMP ping aanvragen reageren. Standaard reageren Hallo StorSimple netwerkinterfaces tooping aanvragen niet. Gebruik deze cmdlet is de eenvoudigste manier tooknow Hallo als uw apparaat online en bereikbaar is is.

**Voorbeeld van uitvoer – Enable HcsPing en schakel HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>Problemen oplossen met Hallo Trace HcsRoute cmdlet
Deze cmdlet gebruiken als een hulpmiddel voor het traceren van route. Deze pakketten tooeach router verzendt op Hallo manier tooa eindbestemming gedurende een periode en vervolgens wordt berekend op basis van hello-pakketten die zijn geretourneerd door elke hop resultaten. Omdat Hallo cmdlet Hallo graad van pakketverlies op elke gewenste router of koppeling toont, u kunt achterhalen welke routers of koppelingen mogelijk veroorzaakt door problemen met het netwerk.

**Voorbeeld van uitvoer wordt weergegeven hoe tootrace Hallo-route van een pakket met de Trace-HcsRoute**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>Problemen oplossen met Hallo Get HcsRoutingTable cmdlet
Gebruik deze cmdlet tooview Hallo-routeringstabel voor uw StorSimple-apparaat. Een routeringstabel is een reeks regels om bepalen waar de gegevenspakketten die via een netwerk IP (Internet Protocol te) worden omgeleid.

Hallo routeringstabel toont Hallo interfaces en hello gateway dat routes gegevens toohello Hallo opgegeven netwerken. Dit biedt ook Hallo routering metriek die Hallo besluitvormer voor Hallo pad tooreach een specifieke bestemming. Hallo lagere Hallo routering metrische, Hallo hogere Hallo voorkeur.

Bijvoorbeeld, als u 2 netwerkinterfaces DATA 2 en DATA 3, verbonden toohello Internet hebben. Als de metrische gegevens voor Hallo routering voor DATA 2 en DATA 3 15 en 261 respectievelijk, is DATA 2 met lagere routering metric Hallo Hallo-interface voorkeur tooreach Hallo Internet gebruikt.

Als u Update 1 op uw StorSimple-apparaat worden uitgevoerd, heeft uw DATA 0-netwerkinterface Hallo hoogste voorkeur voor verkeer van de cloud Hallo. Dit betekent dat zelfs als er andere interfaces ingeschakeld voor de cloud, verkeer van de cloud Hallo zou worden gerouteerd via DATA 0.

Als u Hallo uitvoert `Get-HcsRoutingTable` cmdlet zonder op te geven (als Hallo volgende voorbeeld wordt getoond), parameters Hallo cmdlet wordt zowel IPv4 als IPv6-routeringstabel uitvoer. U kunt ook opgeven `Get-HcsRoutingTable -IPv4` of `Get-HcsRoutingTable -IPv6` tooget een relevante routeringstabel.

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>Voorbeeld van stapsgewijze StorSimple-probleemoplossing
Hallo volgende voorbeeld ziet stapsgewijze probleemoplossing van een StorSimple-implementatie. In het voorbeeldscenario Hallo mislukt de apparaatregistratie met een foutbericht dat netwerkinstellingen Hallo of Hallo DNS-naam onjuist is.

Hallo foutbericht wordt geretourneerd is:

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

Hallo-fout wordt mogelijk veroorzaakt door een van de volgende Hallo:

* Onjuiste hardware-installatie
* Defecte netwerkinterfaces
* Onjuiste IP-adres, subnetmasker, gateway, primaire DNS-server of webproxy
* Onjuiste registratiesleutel
* Onjuiste firewall-instellingen

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate en fix Hallo apparaat registratie probleem
1. Controleer de configuratie van uw apparaat: Voer op de actieve controller hello, `Invoke-HcsSetupWizard`.
   
   > [!NOTE]
   > Hallo-installatiewizard moet uitvoeren op Hallo actieve controller. tooverify dat u verbonden toohello actieve controller bekijkt hello banner die zijn gepresenteerd in Hallo seriële console. Hallo banner geeft aan of u bent verbonden toocontroller 0 of 1-controller, of Hallo controller actief of passief is. Voor meer informatie gaat te[een actieve domeincontroller op uw apparaat identificeren](storsimple-8000-controller-replacement.md#identify-the-active-controller-on-your-device).
   
2. Zorg ervoor dat het Hallo-apparaat goed is bekabeld: Hallo netwerkkabels op Hallo apparaat terug luchtvervoer controleren. Hallo bekabeling is specifieke toohello Apparaatmodel. Voor meer informatie gaat te[uw StorSimple 8100-apparaat installeert](storsimple-8100-hardware-installation.md) of [uw StorSimple 8600-apparaat installeert](storsimple-8600-hardware-installation.md).
   
   > [!NOTE]
   > Als u van 10 GbE-netwerkpoorten gebruikmaakt, moet u toouse hello QSFP SFP-adapters en SFP kabels opgegeven. Zie voor meer informatie, Hallo [lijst met kabels en switches infraroodzenders aanbevolen voor Hallo 10 GbE-poorten](storsimple-supported-hardware-for-10-gbe-network-interfaces.md).
  
3. Hallo-status van de netwerkinterface Hallo controleren:
   
   * Hallo Get NetAdapter cmdlet toodetect Hallo status van netwerkinterfaces Hallo voor DATA 0 gebruiken. 
   * Als het Hallo-koppeling is niet werkt, Hallo **ifindex** status aangeeft die Hallo-interface niet actief is. Vervolgens moet u het Hallo-netwerkverbinding toocheck van Hallo poort toohello toestel en toohello switch. U moet ook toorule uit slechte kabels. 
   * Als u dat Hallo DATA 0 vermoedt-poort op de actieve controller Hallo is mislukt, kunt u dit controleren door verbinding te maken toohello DATA 0-poort op de controller 1. tooconfirm, Verbreek de verbinding tussen de netwerkkabel Hallo Hallo achterzijde Hallo apparaat vanaf een controller 0 Hallo kabel toocontroller 1 verbinding en voer de cmdlet Get-NetAdapter Hallo opnieuw.
     Als Hallo DATA 0-poort op een domeincontroller is mislukt, [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor volgende stappen. Mogelijk moet u tooreplace Hallo controller op uw systeem.
4. Controleer of Hallo connectiviteit toohello switch:
   
   * Zorg ervoor dat DATA 0-netwerkinterfaces op de controller 0 en controller 1 in uw primaire behuizing op Hallo hetzelfde subnet. 
   * Controleer de Hallo-hub of -router. Normaal gesproken moet u beide domeincontrollers toohello dezelfde hub of router. 
   * Zorg ervoor dat u voor verbinding Hallo gebruikt Hallo-switches DATA 0 voor beide domeincontrollers in Hallo hetzelfde vLAN.
5. Gebruikersfouten voorkomen:
   
   * Hallo-installatiewizard opnieuw uitvoeren (uitvoeren **Invoke-HcsSetupWizard**), en Voer Hallo waarden opnieuw toomake ervoor dat er geen fouten zijn. 
   * Hallo registratie controleren sleutel die wordt gebruikt. Hallo dezelfde registratiesleutel gebruikte tooconnect meerdere apparaten tooa StorSimple-apparaat Manager-service kan zijn. Hallo procedure gebruiken in [Get Hallo serviceregistratiesleutel](storsimple-8000-manage-service.md#get-the-service-registration-key) tooensure die u gebruikt de juiste registratiesleutel Hallo.
     
     > [!IMPORTANT]
     > Als er meerdere services die worden uitgevoerd, moet u tooensure die Hallo registratiecode voor de betreffende service Hallo gebruikte tooregister Hallo apparaat is. Als u een apparaat hebt geregistreerd met de Hallo verkeerde Apparaatbeheer StorSimple-service, moet u te[contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor volgende stappen. Wellicht hebt u tooperform fabrieksinstellingen van Hallo-apparaat (dit kan leiden tot verlies van gegevens) toothen verbindt u deze service toohello bedoeld.
     > 
     > 
6. Hallo Test-Connection cmdlet tooverify dat u verbinding toohello buiten netwerk hebt gebruiken. Voor meer informatie gaat te[problemen met de cmdlet Test-Connection Hallo](#troubleshoot-with-the-test-connection-cmdlet).
7. Controleer of de firewall storing. Als u hebt gecontroleerd dat Hallo virtuele IP-adres (VIP), subnet, gateway en DNS-instellingen zijn juist, en verbindingsproblemen nog steeds wordt weergegeven en is het mogelijk dat communicatie tussen het apparaat en de Hallo buiten netwerk door uw firewall wordt geblokkeerd. U moet tooensure of poorten 80 en 443 beschikbaar op uw StorSimple-apparaat voor uitgaande communicatie zijn. Zie voor meer informatie [netwerkvereisten voor uw StorSimple-apparaat](storsimple-8000-system-requirements.md#networking-requirements-for-your-storsimple-device).
8. Bekijkt hello Logboeken. Ga te[ondersteuning voor pakketten en apparaatlogboeken beschikbaar voor het oplossen van](#support-packages-and-device-logs-available-for-troubleshooting).
9. Als hello voorgaande stappen probleem niet is opgelost hello, [contact op met Microsoft Support](storsimple-8000-contact-microsoft-support.md) voor hulp.

## <a name="next-steps"></a>Volgende stappen
[Meer informatie over hoe toouse Hallo diagnostische hulpprogramma tootroubleshoot een StorSimple-apparaat](storsimple-8000-diagnostics.md).

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 

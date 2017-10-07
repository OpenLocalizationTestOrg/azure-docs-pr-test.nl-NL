---
title: aaaView en StorSimple waarschuwingen beheren | Microsoft Docs
description: Beschrijving van waarschuwing StorSimple-voorwaarden en ernst, hoe tooconfigure waarschuwingsmeldingen en hoe toouse hello StorSimple Manager service toomanage waarschuwingen.
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: bee49253-9ac7-4131-95f6-6bf0e72b8438
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/08/2017
ms.author: anbacker
ms.openlocfilehash: d322c88b565606538a3acb61ff939ec1fbe2f3cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-tooview-and-manage-storsimple-alerts"></a>Hallo StorSimple Manager-service tooview gebruiken en beheren van waarschuwingen voor StorSimple
## <a name="overview"></a>Overzicht
Hallo **waarschuwingen** tabblad in Hallo StorSimple Manager-service biedt een manier voor u tooreview en wissen StorSimple-apparaat gerelateerde waarschuwingen op basis van realtime. Op dit tabblad kunt u centraal statusproblemen Hallo van uw StorSimple-apparaten te bewaken en Hallo algemene Microsoft Azure StorSimple-oplossing.

Deze zelfstudie wordt beschreven algemene waarschuwingsvoorwaarden ernstniveau van waarschuwingen en hoe tooconfigure meldingen. Daarnaast bevat deze waarschuwing Naslaggids tabellen, waarmee u tooquickly Zoek een specifieke waarschuwing en reageren op de juiste wijze.

![pagina waarschuwingen](./media/storsimple-manage-alerts/HCS_AlertsPage.png)

## <a name="common-alert-conditions"></a>Algemene waarschuwingsvoorwaarden
Uw StorSimple-apparaat genereert waarschuwingen in het antwoord tooa diverse omstandigheden. Hallo volgen Hallo meest voorkomende typen waarschuwingen voorwaarden:

* **Hardwareproblemen** – deze meldingen geven over Hallo status van uw hardware. Ze laten u weten als firmware-upgrades nodig zijn, als een netwerkinterface heeft problemen of als er een probleem met een van uw schijven.
* **Problemen met de netwerkverbinding** – deze waarschuwingen zich voordoen als er problemen bij het overbrengen van gegevens. Communicatieproblemen kunnen optreden tijdens de overdracht van gegevens tooand van hello Azure storage-account of vervaldatum toolack van de verbinding tussen Hallo apparaten en Hallo StorSimple Manager-service. Communicatieproblemen zijn enkele Hallo moeilijkst toofix omdat er zoveel foutpunten. U moet altijd eerst controleren of verbinding met het netwerk en toegang tot Internet beschikbaar zijn voordat u doorgaat op toomore probleemoplossing geavanceerde. Ga te voor hulp bij het oplossen van[problemen met de cmdlet Test-Connection Hallo](storsimple-troubleshoot-deployment.md).
* **Prestatieproblemen** – deze waarschuwingen worden veroorzaakt wanneer uw systeem is niet optimaal, zoals wanneer het zich onder een zware belasting.

Bovendien ziet u mogelijk de gerelateerde toosecurity waarschuwingen, updates of taakfouten.

## <a name="alert-severity-levels"></a>Ernstniveau van waarschuwingen
Waarschuwingen hebben verschillende niveaus, afhankelijk van Hallo gevolgen die Hallo waarschuwing situatie wordt hebben en Hallo nodig voor een antwoord toohello waarschuwing. Hallo ernstniveaus zijn:

* **Kritieke** – deze waarschuwing is in het antwoord tooa conditie van invloed op Hallo geslaagde prestaties van uw systeem. Actie is vereist tooensure hello StorSimple-service niet wordt onderbroken.
* **Waarschuwing** : dit probleem kritiek kan worden als niet omgezet. U moet onderzoeken Hallo situatie en een probleem actie vereist tooclear Hallo nemen.
* **Informatie** – deze waarschuwing bevat informatie die nuttig zijn kan bij het beheren van uw systeem en bij te houden.

## <a name="configure-alert-settings"></a>Instellingen voor waarschuwingen configureren
U kunt kiezen of u wilt dat toobe op de hoogte met e-mailadres van de waarschuwing voorwaarden voor elk van uw StorSimple-apparaten. Bovendien kunt u andere ontvangers waarschuwingsmeldingen identificeren met hun e-mailadres invoeren in Hallo **andere e-mailontvangers** vak, gescheiden door puntkomma's.

> [!NOTE]
> U kunt maximaal 20 e-mailadressen per apparaat invoeren.
> 
> 

Nadat u e-mailmelding voor een apparaat hebt ingeschakeld, ontvangt de leden van de meldingenlijst Hallo een e-mailbericht telkens wanneer een kritieke waarschuwing optreedt. Hallo-berichten worden verzonden vanuit  *storsimple-alerts-noreply@mail.windowsazure.com*  en meldingsvoorwaarde hello wordt beschreven. Ontvangers kunnen klikken op **Unsubscribe** tooremove zichzelf tegen meldingenlijst Hallo-e-mailbericht.

#### <a name="tooenable-email-notification-of-alerts-for-a-device"></a>tooenable e-mailmeldingen van waarschuwingen voor een apparaat
1. Ga te**apparaten** > **configureren** voor Hallo-apparaat.
2. Onder **waarschuwingsinstellingen**, Hallo volgende instellen:
   
   1. In Hallo **e-mailmelding verzenden** optie **Ja**.
   2. In Hallo **e-servicebeheerders** optie **Ja** als toohave Hallo-servicebeheerder gewenst en medebeheerders alle Hallo waarschuwingsmeldingen ontvangt.
   3. In Hallo **andere e-mailontvangers** Voer Hallo e-mailadressen van alle andere ontvangers Hallo waarschuwingsmeldingen. Geef de namen in Hallo indeling  *someone@somewhere.com* . Gebruik een puntkomma tooseparate Hallo e-mailadressen. U kunt maximaal 20 e-mailadressen per apparaat configureren. 
      
       ![configuratie voor meldingen van waarschuwingen](./media/storsimple-manage-alerts/AlertNotify.png)
3. toosend een test-e-mailmeldingen, klikt u op het pijlpictogram Hallo volgende te**testbericht verzenden**. Hallo StorSimple Manager-service wordt weergegeven statusberichten Hallo Testmelding wordt doorgestuurd. 
4. Wanneer hello volgende bericht wordt weergegeven, klikt u op **OK**. 
   
    ![Waarschuwingen testen verzonden e-mailmelding](./media/storsimple-manage-alerts/HCS_AlertNotificationConfig3.png)
   
   > [!NOTE]
   > Als hello Meldingsbericht test kan niet worden verzonden, wordt een juiste bericht weergegeven met Hallo StorSimple Manager-service. Klik op **OK**wacht een paar minuten en probeer het vervolgens toosend uw test-melding opnieuw. 
   > 
   > 

## <a name="view-and-track-alerts"></a>Waarschuwingen weergeven en bijhouden
Hallo StorSimple Manager servicedashboard biedt u een kijkje Hallo aantal waarschuwingen op uw apparaten, gerangschikt op ernst.

![Waarschuwingen-dashboard](./media/storsimple-manage-alerts/admin_alerts_dashboard.png)

Ernst Hallo Hallo wordt geopend **waarschuwingen** tabblad Hallo resultaten alleen Hallo-waarschuwingen die overeenkomen met die ernstniveau bevatten.

![Rapport waarschuwingen binnen het bereik van tooalert type](./media/storsimple-manage-alerts/admin_alerts_scoped.png)

Te klikken op een waarschuwing in de lijst Hallo biedt aanvullende informatie voor Hallo waarschuwing, inclusief Hallo laatste tijd Hallo waarschuwing is gemeld, aantal exemplaren van de waarschuwing op Hallo-apparaat en Hallo HALLO hallo aanbevolen actie tooresolve Hallo waarschuwing. Als het een hardware-waarschuwing, wordt deze ook Hallo hardwareonderdeel identificeren.

![Voorbeeld van de hardware-waarschuwing](./media/storsimple-manage-alerts/admin_alerts_hardware.png)

Als u toosend Hallo informatie tooMicrosoft ondersteuning nodig hebt, kunt u Hallo Waarschuwingsdetails tooa tekstbestand kopiëren. Nadat u hebt gevolgd Hallo aanbeveling en Hallo meldingsvoorwaarde lokale opgelost, moet u Hallo waarschuwing van Hallo apparaat wissen Hallo waarschuwing door in te schakelen Hallo **waarschuwingen** tabblad en te klikken op **wissen**. tooclear meerdere waarschuwingen selecteert dat elke waarschuwing, klikt u op een van de kolommen behalve Hallo **waarschuwing** kolom en klik vervolgens op **wissen** nadat u hebt geselecteerd Hallo alle waarschuwingen toobe gewist. Houd er rekening mee dat sommige waarschuwingen automatisch gewist wanneer het Hallo-probleem is opgelost of wanneer Hallo system Hallo waarschuwing met nieuwe informatie bijgewerkt.

Wanneer u klikt op **wissen**, hebt u Hallo kans tooprovide opmerkingen over Hallo waarschuwing en Hallo stappen die u hebt ondernomen tooresolve Hallo probleem. Sommige gebeurtenissen worden gewist door Hallo systeem als een andere gebeurtenis wordt geactiveerd met nieuwe informatie. U ziet in dat geval Hallo-bericht te volgen.

![Waarschuwingsbericht voor wissen](./media/storsimple-manage-alerts/admin_alerts_system_clear.png)

## <a name="sort-and-review-alerts"></a>Sorteren en bekijk waarschuwingen
Soms is het efficiënter toorun rapporten over waarschuwingen, zodat u kunt bekijken en deze in groepen wissen. Bovendien Hallo **waarschuwingen** tabblad kan maximaal too250 waarschuwingen weergeven. Als u dat aantal waarschuwingen hebben overschreden, wordt niet alle waarschuwingen weergegeven in de standaardweergave Hallo. U kunt combineren Hallo na velden toocustomize welke waarschuwingen worden weergegeven:

* **Status** – u kunt ofwel weergeven **Active** of **uitgeschakeld** waarschuwingen. Actieve waarschuwingen zijn nog steeds op het systeem geactiveerd terwijl gewiste waarschuwingen zijn handmatig worden gewist door een beheerder of programmatisch gewist omdat Hallo systeem Hallo meldingsvoorwaarde met nieuwe informatie bijgewerkt.
* **Ernst** – u kunt waarschuwingen van alle niveaus (kritiek, waarschuwing, informatie) of alleen een bepaalde ernst, zoals alleen kritieke waarschuwingen weergeven.
* **Bron** – u kunt waarschuwingen van alle bronnen weergegeven of Hallo waarschuwingen toothose die afkomstig zijn van het Hallo-service of een of alle Hallo apparaten beperken.
* **Tijdsbereik** – door te geven Hallo **van** en **naar** datums en tijdstempels, kunt u bekijken waarschuwingen tijdens Hallo periode waarin u geïnteresseerd bent in.

## <a name="alerts-quick-reference"></a>Naslaggids voor waarschuwingen
Hallo tabellen na een overzicht van Hallo Microsoft Azure StorSimple waarschuwingen die u tegenkomen kunt, evenals aanvullende informatie en aanbevelingen indien beschikbaar. Waarschuwingen voor StorSimple-apparaat vallen in een van de volgende categorieën Hallo:

* [Connectiviteitswaarschuwingen cloud](#cloud-connectivity-alerts)
* [Cluster-waarschuwingen](#cluster-alerts)
* [Disaster recovery waarschuwingen](#disaster-recovery-alerts)
* [Hardware-waarschuwingen](#hardware-alerts)
* [Waarschuwingen met betrekking tot taak](#job-failure-alerts)
* [Lokaal vastgemaakt volume waarschuwingen](#locally-pinned-volume-alerts)
* [Waarschuwingen voor netwerken](#networking-alerts)
* [Waarschuwingen over toepassingsprestaties](#performance-alerts)
* [Beveiligingswaarschuwingen](#security-alerts)
* [Ondersteuning voor pakket-waarschuwingen](#support-package-alerts)

### <a name="cloud-connectivity-alerts"></a>Connectiviteitswaarschuwingen cloud
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Connectiviteit te <*cloud referentienaam*> kan niet tot stand worden gebracht. |Kan geen verbinding toohello storage-account. |Het lijkt erop dat er mogelijk een probleem met uw apparaat. Voer Hallo `Test-HcsmConnection` cmdlet in Windows PowerShell-Interface voor StorSimple Hallo op uw apparaat tooidentify en los Hallo probleem. Als het Hallo-instellingen correct zijn, zijn Hallo probleem met referenties op Hallo van Hallo opslagaccount waarvoor Hallo waarschuwing is gegeven. In dit geval gebruiken Hallo `Test-HcsStorageAccountCredential` cmdlet toodetermine als er zijn problemen waarvan u het kunt oplossen.<ul><li>Controleer de netwerkinstellingen.</li><li>Controleer de referenties van het opslagaccount.</li></ul> |
| Er geen ontvangen geen heartbeat van uw apparaat voor Hallo laatste <*getal*> minuten. |Kan geen verbinding toodevice. |Het lijkt erop dat er een verbindingsprobleem met uw apparaat is. Gebruik Hallo `Test-HcsmConnection` cmdlet uit Windows PowerShell-Interface voor StorSimple Hallo op uw apparaat tooidentify en los Hallo probleem of neem contact op met uw netwerkbeheerder. |

### <a name="storsimple-behavior-when-cloud-connectivity-fails"></a>StorSimple gedrag wanneer de connectiviteit van de cloud is mislukt
Wat gebeurt er als cloud-connectiviteit is mislukt voor mijn StorSimple-apparaat in productie uitgevoerd?

Als de cloud-connectiviteit is mislukt op uw StorSimple-apparaat voor productie, vervolgens, afhankelijk van de status van uw apparaat Hallo Hallo volgende kan zich voordoen: 

* **Voor lokale gegevens op uw apparaat Hallo**: enige tijd zal er geen wordt onderbroken en leesbewerkingen blijft toobe geleverd. Als het aantal openstaande IOs Hallo verhoogt en een limiet overschrijdt, kunnen Hallo leesbewerkingen echter toofail starten. 
  
    Afhankelijk van Hallo hoeveelheid gegevens op uw apparaat blijven Hallo schrijfbewerkingen ook toooccur voor Hallo eerste enkele uren na Hallo onderbreking in de Hallo cloud verbinding. Hallo schrijfbewerkingen wordt vervolgens vertragen en uiteindelijk toofail start als Hallo cloud connectiviteit gedurende een aantal uren wordt onderbroken. (Er tijdelijke opslag is op Hallo-apparaat voor gegevens die toobe toohello cloud gepusht. Dit gebied wordt leeggemaakt wanneer Hallo gegevens worden verzonden. Als de verbinding is mislukt, gegevens in deze opslagruimte wordt niet gepusht toohello cloud, en mislukt de i/o.)   
* **Voor gegevens in de cloud Hallo Hallo**: voor de meeste fouten voor cloud-connectiviteit, wordt een fout geretourneerd. Zodra het Hallo-verbinding is hersteld, worden zonder Hallo gebruiker toobring Hallo volume online Hallo IOs hervat. In zeldzame gevallen mogelijk tussenkomst van de gebruiker vereist toobring back Hallo volume online van Hallo klassieke Azure-portal. 
* **Voor cloudmomentopnamen van de Bezig**: Hallo-bewerking wordt opnieuw geprobeerd een paar keer binnen 4-5 uur en als het Hallo-verbinding is niet hersteld, Hallo cloudmomentopnamen zal mislukken.

### <a name="cluster-alerts"></a>Cluster-waarschuwingen
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Apparaat te failover <*apparaatnaam*>. |Apparaat is in de onderhoudsmodus. |Apparaat is niet via vanwege tooentering of afgesloten onderhoudsmodus. Dit is normaal en is geen actie vereist. Nadat u deze waarschuwing hebt bevestigd, schakelt u het op de pagina waarschuwingen Hallo. |
| Apparaat te failover <*apparaatnaam*>. |Apparaatfirmware of de software is zojuist hebt bijgewerkt. |Er is een clusterfailover vanwege tooan update. Dit is normaal en is geen actie vereist. Nadat u deze waarschuwing hebt bevestigd, schakelt u het op de pagina waarschuwingen Hallo. |
| Apparaat te failover <*apparaatnaam*>. |Controller is afgesloten of opnieuw gestart. |Apparaat is via mislukt, omdat de actieve controller Hallo is afgesloten of opnieuw worden gestart door een beheerder. Er is geen actie vereist. Nadat u deze waarschuwing hebt bevestigd, schakelt u het op de pagina waarschuwingen Hallo. |
| Apparaat te failover <*apparaatnaam*>. |Geplande failover. |Controleer of dit is een geplande failover. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |
| Apparaat te failover <*apparaatnaam*>. |Niet-geplande failover. |StorSimple is gebouwd tooautomatically herstellen van niet-geplande failovers. Als u een groot aantal deze waarschuwingen ziet, moet u contact op met Microsoft Support. |
| Apparaat te failover <*apparaatnaam*>. |Andere/onbekende oorzaak. |Als u een groot aantal deze waarschuwingen ziet, moet u contact op met Microsoft Support. Nadat het Hallo-probleem is opgelost, moet u deze waarschuwing op de pagina waarschuwingen Hallo wissen. |
| Een service essentiële apparaat gerapporteerd als mislukt. |Gegevenspad service is mislukt. |Neem voor hulp contact op met Microsoft Support. |
| Virtueel IP-adres voor de netwerkinterface <*gegevens #*> meldt de status mislukt. |Andere/onbekende oorzaak. |Soms tijdelijke voorwaarden kunnen deze waarschuwingen veroorzaken. Als dit Hallo geval is, wordt klikt u vervolgens deze waarschuwing automatisch gewist na enige tijd. Als Hallo probleem zich blijft voordoen, neem dan contact op met Microsoft Support. |
| Virtueel IP-adres voor de netwerkinterface <*gegevens #*> meldt de status mislukt. |Interfacenaam: <*gegevens #*> IP-adres <IP address> niet online worden gebracht omdat er een dubbel IP-adres op Hallo-netwerk is gedetecteerd. |Zorg ervoor dat Hallo dubbel IP-adres is verwijderd uit Hallo netwerk of Hallo-interface met een ander IP-adres configureren. |

### <a name="disaster-recovery-alerts"></a>Disaster recovery waarschuwingen
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Herstelbewerkingen kunnen niet alle instellingen voor deze service Hallo herstellen. Apparaat-configuratiegegevens zijn in een inconsistente status voor sommige apparaten. |Een gegevensinconsistentie gevonden na het herstel na noodgevallen. |Versleutelde gegevens op Hallo-service is niet gesynchroniseerd met die op Hallo-apparaat. Autoriseren hello apparaat <*apparaatnaam*> van de StorSimple Manager toostart Hallo-synchronisatieproces. Gebruik Hallo Windows PowerShell-Interface voor StorSimple toorun hello `Restore-HcsmEncryptedServiceData` op apparaat <*apparaatnaam*> cmdlet, biedt het oude wachtwoord Hallo als een invoer toothis cmdlet toorestore Hallo beveiligingsprofiel. Voer Hallo `Invoke-HcsmServiceDataEncryptionKeyChange` gegevensversleutelingssleutel van cmdlet tooupdate Hallo-service. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |

### <a name="hardware-alerts"></a>Hardware-waarschuwingen
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Hardware-onderdeel <*onderdeel-ID*> wordt gerapporteerd als <*status*>. | |Soms tijdelijke voorwaarden kunnen deze waarschuwingen veroorzaken. Zo ja, wordt deze waarschuwing automatisch gewist na enige tijd. Als Hallo probleem zich blijft voordoen, neem dan contact op met Microsoft Support. |
| Passieve controller defect. |Hallo passieve (secundair) domeincontroller functioneert niet. |Uw apparaat functioneert, maar een van uw domeincontrollers is defect. Probeer opnieuw te starten die controller. Als het probleem Hallo niet is opgelost, moet u contact op met Microsoft Support. |
| Aanstaande stationsfout gedetecteerd. | Aanstaande stationsfout gedetecteerd. |Er is vastgesteld dat een aanstaande stationsfout voor hardwareonderdeel Hallo ' station in sleuf <*sleuf ID*>, behuizing <*behuizing ID*>'. Houd rekening met het vervangen van de schijf. <br> Voordat u de nieuwe schijf Hallo, bekijk Hallo informatie te volgen.<br><br>Als uw apparaat meer dan één niet-werkende schijf heeft, verwijder niet meer dan één SSD of harde schijf op elk gewenst moment. Dit kan leiden tot verlies van gegevens.<br><br>Zorg ervoor dat u een vervangende SSD plaatsen in een sleuf dat eerder een SSD bevatte. Hallo geldt voor een harde schijf.<br><br>Sleuven zijn genummerd van 0 too11. Een niet-werkende schijf in sleuf 2 toegewezen tooa defecte schijf in sleuf 3 Hallo-apparaat (van Hallo boven links).<br><br>Ga voor meer informatie over de nieuwe schijf, toohttps://go.microsoft.com/fwlink/?linkid=838653. Als het probleem zich blijft voordoen, neem dan contact op met Microsoft ondersteuning via https://go.microsoft.com/fwlink/?linkid=838654. |

### <a name="job-failure-alerts"></a>Waarschuwingen met betrekking tot taak
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Back-up van <*volume groeps-ID bron*> is mislukt. |Back-uptaak is mislukt. |Verbindingsproblemen kunnen verhinderen Hallo back-upbewerking is voltooid. Als er geen verbindingsproblemen zijn, is het mogelijk dat u Hallo kunt u het maximum aantal back-ups hebt bereikt. Verwijder eventuele back-ups die niet langer nodig zijn en probeer Hallo opnieuw. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |
| Klonen van <*bron van de back-element-id's*> te <*bestemming volume serienummers*> is mislukt. |Kloon-taak is mislukt. |Vernieuwen Hallo back-uplijst tooverify Hallo back-up is nog geldig. Als back-up Hallo geldig is, is het mogelijk dat cloud-verbindingsproblemen verhinderen Hallo kloonbewerking is voltooid. Als er geen verbindingsproblemen zijn, hebt u mogelijk Hallo opslaglimiet bereikt. Verwijder eventuele back-ups die niet langer nodig zijn en probeer Hallo opnieuw. Nadat u de juiste actie tooresolve Hallo probleem hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |
| Herstellen van <*bron van de back-element-id's*> is mislukt. |Herstel de taak is mislukt. |Vernieuwen Hallo back-uplijst tooverify Hallo back-up is nog geldig. Als back-up Hallo geldig is, is het mogelijk dat cloud-verbindingsproblemen verhinderen Hallo restore-bewerking is voltooid. Als er geen verbindingsproblemen zijn, hebt u mogelijk Hallo opslaglimiet bereikt. Verwijder eventuele back-ups die niet langer nodig zijn en probeer Hallo opnieuw. Nadat u de juiste actie tooresolve Hallo probleem hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |

### <a name="locally-pinned-volume-alerts"></a>Lokaal vastgemaakt volume waarschuwingen
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Het maken van lokaal volume <*volumenaam*> is mislukt. |taak voor het maken van volume Hallo is mislukt. <*Fout bericht bijbehorende toohello mislukt foutcode*>. |Verbindingsproblemen kunnen verhinderen Hallo ruimte totdat de bewerking uit te voltooien. Lokaal vastgemaakte volumes zijn compact ingericht en Hallo-proces voor het maken van de ruimte omvat gelaagde volumes toohello cloud lopen. Als er geen verbindingsproblemen zijn, u mogelijk zijn Hallo lokale ruimte op Hallo-apparaat. Bepalen of er ruimte op Hallo apparaat bestaat voordat u deze bewerking. |
| Uitbreiding van de lokale volume <*volumenaam*> is mislukt. |Hallo volume wijziging taak is mislukt vanwege te <*fout bericht bijbehorende toohello mislukt foutcode*>. |Verbindingsproblemen kunnen verhinderen Hallo volume uitbreiding bewerking te voltooien. Lokaal vastgemaakte volumes zijn compact ingericht en Hallo-proces voor het uitbreiden van de bestaande space Hallo omvat gelaagde volumes toohello cloud lopen. Als er geen verbindingsproblemen zijn, u mogelijk zijn Hallo lokale ruimte op Hallo-apparaat. Bepalen of er ruimte op Hallo apparaat bestaat voordat u deze bewerking. |
| Conversie van volume <*volumenaam*> is mislukt. |Hallo volume conversie tooconvert Hallo volume taaktype van lokaal vastgemaakte tootiered is mislukt. |Conversie van Hallo volume van het type lokaal vastgemaakt tootiered kan niet worden voltooid. Zorg ervoor dat er geen verbindingsproblemen zijn zo wordt voorkomen dat Hallo-bewerking wordt voltooid. Voor het oplossen van verbindingsproblemen problemen te gaat[problemen met de cmdlet Test-HcsmConnection hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>Hallo oorspronkelijke lokaal vastgemaakt volume is nu gemarkeerd als een gelaagd volume omdat sommige Hallo gegevens van Hallo lokaal vastgemaakt volume heeft toohello cloud zich tijdens de conversie van Hallo verspreid. Hallo resulterende gelaagd volume wordt nog steeds lokale ruimte op Hallo-apparaat dat niet kan worden vrijgemaakt voor toekomstige lokale volumes ingenomen.<br>Verhelp eventuele problemen met connectiviteit, Hallo waarschuwing wissen en dit volume back toohello oorspronkelijke lokaal vastgemaakt volume type tooensure alle Hallo gegevens beschikbaar worden gesteld lokaal opnieuw converteren. |
| Conversie van volume <*volumenaam*> is mislukt. |Hallo volume conversie tooconvert Hallo volume taaktype van gelaagde toolocally vastgemaakt is mislukt. |Conversie van Hallo volume van het type gelaagde toolocally vastgemaakt kan niet worden voltooid. Zorg ervoor dat er geen verbindingsproblemen zijn zo wordt voorkomen dat Hallo-bewerking wordt voltooid. Voor het oplossen van verbindingsproblemen problemen te gaat[problemen met de cmdlet Test-HcsmConnection hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-test-hcsmconnection-cmdlet).<br>Hallo oorspronkelijke gelaagd volume nu gemarkeerd als een lokaal vastgemaakt volume als onderdeel van het conversieproces Hallo toohave gegevens die zich in de cloud hello blijft, terwijl Hallo compact ruimte op Hallo-apparaat voor dit volume ingericht kan niet meer worden vrijgemaakt voor toekomstige lokale volumes.<br>Los eventuele problemen met de netwerkverbinding, wissen Hallo waarschuwing en converteren die dit volume back toohello oorspronkelijke gelaagd volume type tooensure lokale ruimte compact ingericht op Hallo apparaat kan worden vrijgemaakt. |
| Lokale ruimte verbruik voor lokale momentopnamen van bijna <*volume groepsnaam*> |Lokale momentopnamen voor back-upbeleid Hallo mogelijk binnenkort tekort aan ruimte en worden ongeldig tooavoid host schrijven fouten. |Veelvuldig lokale momentopnamen samen met een hoge gegevensverloop in Hallo volumes die zijn gekoppeld aan deze groep back-upbeleid veroorzaken lokale ruimte op Hallo apparaat toobe snel verbruikt. Verwijder eventuele lokale momentopnamen die niet langer nodig zijn. Ook bijwerken van uw lokale momentopname schema's voor deze back-upbeleid tootake minder frequente lokale momentopnamen en zorg ervoor dat cloudmomentopnamen regelmatig worden gemaakt. Als deze acties worden niet genomen, lokale ruimte voor deze momentopnamen kan snel worden verbruikt en Hallo systeem automatisch verwijdert tooensure die host schrijven toobe verwerkt voortgezet. |
| Lokale momentopnamen voor <*volume groepsnaam*> zijn ongeldig gemaakt. |lokale momentopnamen voor Hallo <*volume groepsnaam*> zijn ongeldig gemaakt en vervolgens verwijderd, omdat ze zijn van meer dan Hallo lokale ruimte op Hallo-apparaat. |tooensure dit niet herhaald in toekomstige Hallo, bekijk Hallo lokale momentopname schema's voor het back-upbeleid en verwijder eventuele lokale momentopnamen die niet langer nodig zijn. Veelvuldig lokale momentopnamen samen met een hoge gegevensverloop in Hallo volumes die zijn gekoppeld aan deze groep back-upbeleid op leiden tot lokale ruimte Hallo apparaat toobe snel verbruikt. |
| Herstellen van <*bron van de back-element-id's*> is mislukt. |Hallo hersteltaak is mislukt. |Als u lokaal hebt vastgemaakt of een combinatie van lokaal vastgemaakte en gelaagde volumes in het back-upbeleid, vernieuwen Hallo back-uplijst tooverify Hallo back-up nog geldig is. Als back-up Hallo geldig is, is het mogelijk dat cloud-verbindingsproblemen verhinderen Hallo restore-bewerking is voltooid. Hallo lokaal vastgemaakte volumes die zijn wordt teruggezet als onderdeel van deze groep momentopname niet beschikt over alle hun apparaat voor gedownloade toohello en hebt u een combinatie van gelaagde en lokaal vastgemaakte volumes in deze groep momentopname, ze niet gesynchroniseerd met elkaar worden. toosuccessfully hello restore-bewerking te voltooien, Hallo volumes duren in deze groep offline op Hallo host en probeer Hallo restore-bewerking. Opmerking wijzigingen toohello volumegegevens die zijn uitgevoerd tijdens het Hallo herstelproces niet verloren. |

### <a name="networking-alerts"></a>Waarschuwingen voor netwerken
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Kan de StorSimple-service(s) niet starten. |Gegevenspad fout |Als Hallo probleem zich blijft voordoen, neem contact op met Microsoft Support. |
| Dubbel IP-adres voor 'Data0' gedetecteerd. | |Hallo systeem heeft een conflict met IP-adres '10.0.0.1' gedetecteerd. netwerkbron 'Data0' Hallo op Hallo apparaat  *<device1>*  offline is. Zorg ervoor dat dit IP-adres niet wordt gebruikt door een andere entiteit in dit netwerk. tootroubleshoot netwerkproblemen, gaat u te[problemen met de cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). Neem contact op met de netwerkbeheerder voor hulp bij het oplossen van dit probleem. Als Hallo probleem zich blijft voordoen, neem contact op met Microsoft Support. |
| -(IPv4 of IPv6)-adres voor 'Data0' is offline. | |Hallo netwerkbron 'Data0' met IP-adres '10.0.0.1'. en voorvoegsellengte '22' op Hallo apparaat  *<device1>*  offline is. Zorg ervoor dat Hallo switch poorten toowhich deze interface is verbonden operationeel zijn. tootroubleshoot netwerkproblemen, gaat u te[problemen met de cmdlet Get-NetAdapter hello](storsimple-troubleshoot-deployment.md#troubleshoot-with-the-get-netadapter-cmdlet). |

### <a name="performance-alerts"></a>Waarschuwingen over toepassingsprestaties
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Hallo apparaat load is overschreden <*drempelwaarde*>. |Langzamer dan verwacht reactietijden. |Uw apparaat rapporteert gebruik onder een zware belasting van de invoer/uitvoer. Dit kan ertoe leiden dat uw apparaat toonot werk evenals nodig. Bekijk Hallo werkbelastingen die u hebt toohello apparaat gekoppeld en bepalen of er zijn die kan worden verplaatst tooanother apparaat of die niet langer nodig zijn.<br>toounderstand Hallo van de huidige status, gaat u te[gebruik Hallo StorSimple Manager service toomonitor uw apparaat](storsimple-monitor-device.md) |

### <a name="security-alerts"></a>Beveiligingswaarschuwingen
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Microsoft Support-sessie is gestart. |Derde support-sessie geopend. |Controleer of dat deze toegang is toegestaan. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |
| Wachtwoord voor <*element*> verloopt over <*tijdsduur*>. |Wachtwoord verloopt bijna is bereikt. |Wijzig uw wachtwoord voordat dit verloopt. |
| Informatie over de beveiligingsconfiguratie ontbreekt voor <*element-ID*>. | |volumes die zijn gekoppeld aan deze volumecontainer Hallo gebruikte tooreplicate uw StorSimple-configuratie kan niet. tooensure uw gegevens veilig worden opgeslagen, wordt aangeraden dat u Hallo volumecontainer en de volumes die zijn gekoppeld aan de volumecontainer Hallo verwijderen. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo. |
| <*aantal*> aanmeldingspogingen is mislukt voor <*element-ID*>. |Meerdere aanmeldingspogingen mislukte. |Uw apparaat mogelijk aangevallen of een geautoriseerde gebruiker probeert tooconnect met een onjuist wachtwoord.<ul><li>Neem contact op met uw geautoriseerde gebruikers en controleer of deze pogingen zijn van een betrouwbare bron. Als u een groot aantal mislukte aanmeldingspogingen toosee doorgaat, kunt u extern beheer uitschakelen en contact opnemen met uw netwerkbeheerder. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo.</li><li>Controleer of uw Snapshot Manager-exemplaren zijn geconfigureerd met het juiste wachtwoord Hallo. Nadat u de juiste actie hebt uitgevoerd, wist u deze waarschuwing op de pagina waarschuwingen Hallo.</li></ul>Voor meer informatie gaat te[wijzigen van een verlopen apparaatwachtwoord](storsimple-snapshot-manager-manage-devices.md#change-an-expired-device-password). |
| Een of meer fouten opgetreden tijdens het wijzigen van de gegevensversleutelingssleutel van Hallo-service. | |Er zijn fouten opgetreden tijdens het wijzigen van de gegevensversleutelingssleutel van Hallo-service. Nadat het Hallo foutcondities hebt opgelost, voert u Hallo `Invoke-HcsmServiceDataEncryptionKeyChange` cmdlet in Windows PowerShell-Interface voor StorSimple Hallo op uw apparaat tooupdate Hallo-service. Neem contact op met Microsoft Ondersteuning als het probleem zich blijft voordoen. Nadat u Hallo probleem hebt opgelost, schakelt u deze waarschuwing op de pagina waarschuwingen Hallo. |

### <a name="support-package-alerts"></a>Ondersteuning voor pakket-waarschuwingen
| Tekst van de waarschuwing | Gebeurtenis | Meer informatie / aanbevolen acties |
|:--- |:--- |:--- |
| Maken van support-pakket is mislukt. |StorSimple hello pakket kan niet worden gegenereerd. |Probeer het opnieuw. Als Hallo probleem zich blijft voordoen, neem dan contact op met Microsoft Support. Nadat u Hallo probleem hebt opgelost, schakelt u deze waarschuwing op de pagina waarschuwingen Hallo. |

## <a name="next-steps"></a>Volgende stappen
Meer informatie over [StorSimple fouten en probleemoplossing van een apparaat operationele](storsimple-troubleshoot-operational-device.md).


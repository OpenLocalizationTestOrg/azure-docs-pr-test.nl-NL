---
title: systeemvereisten aaaStorSimple | Microsoft Docs
description: Beschrijving van software, netwerken, en hoge beschikbaarheidsvereisten en best practices voor een Microsoft Azure StorSimple-oplossing.
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2b6ca34a-d758-48e7-ab1e-4fdd80cf48d4
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/06/2017
ms.author: alkohli
ms.openlocfilehash: ec0bb5ad2f2d4c9901da2d95147dd9daa178f6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-software-high-availability-and-networking-requirements"></a>StorSimple-software, hoge beschikbaarheid en netwerkvereisten
## <a name="overview"></a>Overzicht
Welkom bij Azure StorSimple tooMicrosoft. Dit artikel worden de systeemvereisten voor belangrijke en aanbevolen procedures voor uw StorSimple-apparaat en voor Hallo opslag clients toegang tot Hallo-apparaat. Het is raadzaam dat u Hallo informatie voordat u uw StorSimple-systeem te implementeren en vervolgens tooit zo nodig tijdens de implementatie en de volgende bewerking terugverwijzen zorgvuldig te controleren.

Hallo systeemvereisten zijn onder andere:

* **Softwarevereisten voor opslag clients** -beschrijft Hallo ondersteunde besturingssystemen en eventuele bijkomende vereisten voor deze besturingssystemen.
* **Netwerkvereisten voor de StorSimple-apparaat Hallo** -informatie over poorten Hallo dat openen in uw firewall tooallow nodig toobe biedt voor iSCSI-, cloud- of management-verkeer.
* **Vereisten voor hoge beschikbaarheid voor StorSimple** : beschrijft de vereisten voor hoge beschikbaarheid en aanbevolen procedures voor uw StorSimple-apparaat en host-computer. 

## <a name="software-requirements-for-storage-clients"></a>Softwarevereisten voor clients van opslag
Hallo volgens de softwarevereisten zijn voor Hallo opslag clients die toegang uw StorSimple-apparaat tot.

| Ondersteunde besturingssystemen | Vereiste versie | Aanvullende vereisten/opmerkingen |
| --- | --- | --- |
| Windows Server |2008 R2 SP1, 2012 2012R2, 2016 |StorSimple-volumes van iSCSI-worden ondersteund voor gebruik op alleen Hallo Windows schijftypen te volgen:<ul><li>Eenvoudig volume op een standaardschijf</li><li>Eenvoudige en mirrored volume op een dynamische schijf</li></ul>Alleen Hallo software iSCSI-initiators aanwezig in het besturingssysteem Hallo ingebouwd worden ondersteund. Hardware iSCSI-initiators worden niet ondersteund.<br></br>Windows Server 2012 en 2016 thin provisioning en ODX functies worden ondersteund als u een iSCSI-StorSimple-volume.<br><br>StorSimple kunt maken voor thin provisioning en volledig ingerichte volumes. Er kan geen gedeeltelijk ingerichte volumes maken.<br><br>Een thin provisioning volume formatteren kan lang duren. U wordt aangeraden Hallo volume verwijderen en vervolgens een nieuwe in plaats van herformatteer te maken. Als u nog steeds liever echter tooreformat een volume:<ul><li>Voer Hallo opdracht voordat Hallo herformatteren tooavoid ruimte vrijmaken vertragingen te volgen: <br>`fsutil behavior set disabledeletenotify 1`</br></li><li>Nadat het Hallo-opmaak is voltooid, opdracht gebruik Hallo volgende uit vrijmaken van ruimte toore inschakelen:<br>`fsutil behavior set disabledeletenotify 0`</br></li><li>Windows Server 2012 Hallo hotfix toepast, zoals beschreven in [KB 2878635](https://support.microsoft.com/kb/2870270) tooyour Windows Server-computer.</li></ul></li></ul></ul> Als u voor SharePoint StorSimple Snapshot Manager of een StorSimple-Adapter configureert, gaat u verder te[softwarevereisten voor de optionele componenten](#software-requirements-for-optional-components). |
| VMWare ESX |5.5 en 6.0 |Ondersteund met VMWare vSphere als iSCSI-client. VAAI-block-functie wordt ondersteund met VMware vSphere op StorSimple-apparaten. |
| Linux RHEL/CentOS |5, 6 en 7 |Ondersteuning voor Linux iSCSI-clients met open-iSCSI-initiator versie 5, 6 en 7. |
| Linux |SUSE Linux 11 | |

> [!NOTE]
> IBM AIX wordt momenteel niet ondersteund met StorSimple.
> 
> 

## <a name="software-requirements-for-optional-components"></a>Softwarevereisten voor optionele onderdelen
Hallo volgens de softwarevereisten zijn voor Hallo optionele StorSimple onderdelen (StorSimple Snapshot Manager en StorSimple-Adapter voor SharePoint).

| Onderdeel | Hostplatform | Aanvullende vereisten/opmerkingen |
| --- | --- | --- |
| StorSimple Snapshot Manager |Windows Server 2008 R2 SP1, 2012 2012R2 |Gebruik van StorSimple Snapshot Manager op Windows Server is vereist voor back-up/herstel van gespiegelde dynamische schijven en voor eventuele toepassingsconsistente back-ups.<br> StorSimple Snapshot Manager wordt alleen ondersteund op Windows Server 2008 R2 SP1 (64-bits), Windows 2012 R2 en Windows Server 2012.<ul><li>Als u van venster Server 2012 gebruikmaakt, moet u .NET 3.5 – 4.5 installeren voordat u StorSimple Snapshot Manager installeert.</li><li>Als u van Windows Server 2008 R2 SP1 gebruikmaakt, moet u Windows Management Framework 3.0 installeren voordat u StorSimple Snapshot Manager installeert.</li></ul> |
| StorSimple Adapter voor SharePoint |Windows Server 2008 R2 SP1, 2012 2012R2 |<ul><li>StorSimple-Adapter voor SharePoint wordt alleen ondersteund in SharePoint 2010 en SharePoint 2013.</li><li>Resourcestructuur vereist SQL Server Enterprise Edition van versie 2008 R2 of 2012.</li></ul> |

## <a name="networking-requirements-for-your-storsimple-device"></a>Netwerkvereisten voor uw StorSimple-apparaat
Uw StorSimple-apparaat is een apparaat vergrendeld. Poorten moeten echter toobe geopend in uw firewall tooallow voor iSCSI-, cloud en beheer van verkeer. Hallo bevat volgende tabel Hallo-poorten die toobe geopend in uw firewall moeten. In deze tabel *in* of *inkomende* verwijst toohello richting waaruit binnenkomende aanvragen van clients toegang uw apparaat tot. *Uitgaand* of *uitgaande* toohello richting waarin uw StorSimple-apparaat gegevens extern, afgezien van Hallo implementatie verzendt verwijst: bijvoorbeeld uitgaande toohello Internet.

| Poort nr.<sup>1,2</sup> | In- of uitzoomen | Poort-bereik | Vereist | Opmerkingen |
| --- | --- | --- | --- | --- |
| TCP 80 (HTTP)<sup>3</sup> |out |WAN |Nee |<ul><li>Uitgaande poort wordt gebruikt voor toegang tot tooretrieve updates van Internet.</li><li>Hallo uitgaande webproxy is gebruiker worden geconfigureerd.</li><li>systeemupdates tooallow, deze poort moet ook zijn geopend voor Hallo controller vaste IP-adressen.</li></ul> |
| TCP 443 (HTTPS)<sup>3</sup> |out |WAN |Ja |<ul><li>Uitgaande poort wordt gebruikt voor toegang tot gegevens in de cloud Hallo.</li><li>Hallo uitgaande webproxy is gebruiker worden geconfigureerd.</li><li>systeemupdates tooallow, deze poort moet ook zijn geopend voor Hallo controller vaste IP-adressen.</li><li>Deze poort wordt ook gebruikt op beide domeincontrollers Hallo voor garbagecollection.</li></ul> |
| UDP 53 (DNS) |out |WAN |In sommige gevallen; Zie de opmerkingen. |Deze poort is alleen vereist als u een Internet-gebaseerd DNS-server gebruikt. |
| UDP 123 (NTP) |out |WAN |In sommige gevallen; Zie de opmerkingen. |Deze poort is alleen vereist als u een Internet-gebaseerd NTP-server gebruikt. |
| TCP 9354 |out |WAN |Ja |Hallo uitgaande poort wordt gebruikt door Hallo StorSimple-apparaat toocommunicate Hello StorSimple Manager-service. |
| 3260 (iSCSI) |in |LAN |Nee |Deze poort is gebruikte tooaccess gegevens via iSCSI. |
| 5985 |in |LAN |Nee |Binnenkomende poort wordt gebruikt door StorSimple Snapshot Manager toocommunicate met Hallo StorSimple-apparaat.<br>Deze poort wordt ook gebruikt wanneer u extern verbinding tooWindows PowerShell voor StorSimple via HTTP maakt. |
| 5986 |in |LAN |Nee |Deze poort wordt gebruikt wanneer u extern verbinding tooWindows PowerShell voor StorSimple via HTTPS maakt. |

<sup>1</sup> geen poorten voor inkomend verkeer moeten toobe geopend op Hallo van openbare Internet.

<sup>2</sup> als meerdere poorten uitvoeren voor de configuratie van een gateway, Hallo uitgaand verkeer van gerouteerde volgorde wordt bepaald op basis van Hallo poort routering volgorde zoals beschreven in [poort routering](#routing-metric)onderstaande.

<sup>3</sup> Hallo controller vaste IP-adressen op uw StorSimple-apparaat moet routeerbaar zijn en kunnen tooconnect toohello Internet direct of via Hallo geconfigureerd webproxy. Hallo vaste IP-adressen worden gebruikt voor het onderhoud van Hallo updates toohello apparaat. Hallo apparaatcontrollers verbinding maken toohello Internet via Hallo IP-adressen vaste, worden niet kunnen tooupdate uw StorSimple-apparaat.

> [!IMPORTANT]
> Zorg ervoor dat deze firewall Hallo niet wijzigen of ontsleutelen van een SSL-verkeer tussen Hallo StorSimple-apparaat en Azure.
> 
> 

### <a name="url-patterns-for-firewall-rules"></a>URL-patronen voor firewallregels
Netwerkbeheerders kunnen vaak geavanceerde firewall regels op basis van Hallo URL patronen toofilter Hallo inkomend en uitgaand verkeer Hallo configureren. Uw StorSimple-apparaat en het Hallo StorSimple Manager-service is afhankelijk van andere Microsoft-toepassingen zoals Azure Service Bus, Azure Active Directory-toegangsbeheer, storage-accounts en Microsoft Update-servers. Hallo URL-patronen die zijn gekoppeld aan deze toepassingen kunnen worden gebruikt tooconfigure firewallregels. Het is belangrijk toounderstand die Hallo URL-patronen die zijn gekoppeld aan deze toepassingen kunnen wijzigen. Dit wordt op zijn beurt Hallo netwerk beheerder toomonitor vereisen en firewallregels bijwerken voor uw StorSimple als en indien nodig.

Het is raadzaam dat u de firewallregels voor uitgaand verkeer, op basis van vaste IP-adressen, opneemt in de meeste gevallen StorSimple ingesteld. U kunt echter Hallo informatie onder tooset geavanceerde firewallregels die vereist toocreate beveiligde omgevingen zijn.

> [!NOTE]
> Hallo-apparaat (bron) IP-adressen moet altijd tooall Hallo ingeschakeld netwerkinterfaces worden ingesteld. Hallo bestemming IP-adressen te moet worden ingesteld[Azure datacenter IP-adresbereiken](https://www.microsoft.com/en-us/download/confirmation.aspx?id=41653).
> 
> 

#### <a name="url-patterns-for-azure-portal"></a>URL-patronen voor Azure-portal
| URL-patroon | Onderdeel/functionaliteit | Apparaat-IP-adressen |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.com/*`<br>`https://*.accesscontrol.windows.net/*`<br>`https://*.servicebus.windows.net/*` |StorSimple Manager-service<br>Access Control Service<br>Azure Service Bus |Netwerkinterfaces die zijn ingeschakeld voor de cloud |
| `https://*.backup.windowsazure.com` |Apparaatregistratie |Alleen DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Intrekken van certificaten |Netwerkinterfaces die zijn ingeschakeld voor de cloud |
| `https://*.core.windows.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure storage-accounts en controle |Netwerkinterfaces die zijn ingeschakeld voor de cloud |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update-servers<br> |Controller vaste IP-adressen alleen |
| `http://*.deploy.akamaitechnologies.com` |CDN van Akamai |Controller vaste IP-adressen alleen |
| `https://*.partners.extranet.microsoft.com/*` |Ondersteuningspakket |Netwerkinterfaces die zijn ingeschakeld voor de cloud |

#### <a name="url-patterns-for-azure-government-portal"></a>URL-patronen voor Azure Government portal
| URL-patroon | Onderdeel/functionaliteit | Apparaat-IP-adressen |
| --- | --- | --- |
| `https://*.storsimple.windowsazure.us/*`<br>`https://*.accesscontrol.usgovcloudapi.net/*`<br>`https://*.servicebus.usgovcloudapi.net/*` |StorSimple Manager-service<br>Access Control Service<br>Azure Service Bus |Netwerkinterfaces die zijn ingeschakeld voor de cloud |
| `https://*.backup.windowsazure.us` |Apparaatregistratie |Alleen DATA 0 |
| `http://crl.microsoft.com/pki/*`<br>`http://www.microsoft.com/pki/*` |Intrekken van certificaten |Netwerkinterfaces die zijn ingeschakeld voor de cloud |
| `https://*.core.usgovcloudapi.net/*` <br>`https://*.data.microsoft.com`<br>`http://*.msftncsi.com` |Azure storage-accounts en controle |Netwerkinterfaces die zijn ingeschakeld voor de cloud |
| `http://*.windowsupdate.microsoft.com`<br>`https://*.windowsupdate.microsoft.com`<br>`http://*.update.microsoft.com`<br> `https://*.update.microsoft.com`<br>`http://*.windowsupdate.com`<br>`http://download.microsoft.com`<br>`http://wustat.windows.com`<br>`http://ntservicepack.microsoft.com` |Microsoft Update-servers<br> |Controller vaste IP-adressen alleen |
| `http://*.deploy.akamaitechnologies.com` |CDN van Akamai |Controller vaste IP-adressen alleen |
| `https://*.partners.extranet.microsoft.com/*` |Ondersteuningspakket |Netwerkinterfaces die zijn ingeschakeld voor de cloud |

### <a name="routing-metric"></a>Routering
Een metriek routering is gekoppeld aan Hallo interfaces en Hallo-gateway die routeren Hallo gegevens toohello opgegeven netwerken. Routering wordt gebruikt door Hallo routing protocol toocalculate Hallo best pad tooa opgegeven bestemming, als er meerdere paden bestaan toohello achterhaalt hetzelfde doel. Hallo lagere Hallo routering metrische, Hallo hogere Hallo voorkeur.

Hallo context van StorSimple, als er meerdere netwerkinterfaces en gateways zijn geconfigureerd, toochannel verkeer, Hallo routering metrische gegevens in de play toodetermine Hallo relatieve volgorde in welke Hallo interfaces gewend wordt komen. Hallo routering metrische gegevens kan niet worden gewijzigd door Hallo-gebruiker. U kunt echter Hallo `Get-HcsRoutingTable` cmdlet tooprint Hallo-routeringstabel (en metrische gegevens) op uw StorSimple-apparaat. Meer informatie over de cmdlet Get-HcsRoutingTable in [StorSimple probleemoplossing implementatie](storsimple-troubleshoot-deployment.md).

Hallo routering metrische algoritmen zijn verschillend, afhankelijk van de softwareversie Hallo uitgevoerd op uw StorSimple-apparaat.

**Eerdere releases-tooUpdate 1**

Dit omvat software versies voorafgaande tooUpdate 1 zoals Hallo NH, 0,1, 0,2 of 0,3 release. Hallo-volgorde op basis van routering metrische gegevens is als volgt:

   *Laatste 10 GbE-netwerkinterface geconfigureerd > andere 10 GbE-netwerkinterface > laatste geconfigureerd 1 GbE-netwerkinterface > andere 1 GbE-netwerkinterface*

**Vanaf Update 1 en 2 van eerdere tooUpdate releases**

Dit omvat softwareversies zoals 1, 1.1 of 1.2. Hallo-volgorde op basis van routering metrische gegevens wordt als volgt bepaald:

   *DATA 0 > laatste geconfigureerd 10 GbE-netwerkinterface > andere 10 GbE-netwerkinterface > laatste geconfigureerd 1 GbE-netwerkinterface > andere 1 GbE-netwerkinterface*

   Update 1 wordt Hallo routering meetwaarde van DATA 0 gedaan Hallo laagste; Daarom worden alle Hallo cloud-verkeer wordt doorgestuurd via DATA 0. Noteer dit als er meer dan één ingeschakeld voor de cloud netwerkinterface op uw StorSimple-apparaat.

**Vanaf Update 2 releases**

Update 2 heeft verschillende verbeteringen van netwerkverkeer en Hallo routering metrische gegevens is gewijzigd. Hallo-gedrag kan als volgt worden verklaard.

* Een reeks vooraf bepaalde waarden toonetwork interfaces zijn toegewezen.     
* U kunt een van de voorbeeldtabel hieronder wordt weergegeven met waarden die zijn toegewezen toohello verschillende netwerkinterfaces wanneer ze zijn ingeschakeld voor de cloud of cloud-uitgeschakeld, maar met een geconfigureerde gateway. Opmerking Hallo waarden die hier worden toegewezen, zijn alleen voorbeeldwaarden.

    | Netwerkinterface | Ingeschakeld voor de cloud | Cloud-uitgeschakeld met gateway |
    |-----|---------------|---------------------------|
    | Data 0  | 1            | -                        |
    | Gegevens-1  | 2            | 20                       |
    | Data 2  | 3            | 30                       |
    | Gegevens 3  | 4            | 40                       |
    | Data 4  | 5            | 50                       |
    | Gegevens 5  | 6            | 60                       |


* Hallo volgorde waarin Hallo cloud-verkeer wordt gerouteerd via Hallo netwerkinterfaces is:
  
    *Data 0 > gegevens 1 > datum 2 > gegevens 3 > gegevens 4 > gegevens 5*
  
    Dit kan worden verklaard door Hallo voorbeeld te volgen.
  
    U kunt een virtueel StorSimple-apparaat met twee ingeschakeld voor de cloud netwerkinterfaces, Data 0 en 5 van de gegevens. Gegevens van 1 tot en met 4 van de gegevens zijn cloud-uitgeschakeld, maar een geconfigureerde gateway hebben. Hallo-volgorde op waarin verkeer wordt gerouteerd voor dit apparaat zijn:
  
    *Data 0 (1) > gegevens 5 (6) > gegevens 1 (20) > gegevens (30) 2 > gegevens 3 (40) > gegevens 4 (50)*
  
    *Hallo getallen tussen haakjes aangeven waar Hallo respectieve routering metrische gegevens.*
  
    Als de Data 0 is mislukt, wordt verkeer van de cloud Hallo t/m Data 5 ophalen gerouteerd. Gezien het feit dat een gateway is geconfigureerd op alle andere netwerken, als zowel de Data 0 als de gegevens-5 toofail zijn, wordt verkeer van de cloud Hallo Data 1 doorlopen.
* Als een netwerkinterface met ingeschakeld voor de cloud is mislukt, waarna u 3 nieuwe pogingen met een 30 tweede vertraging tooconnect toohello interface zijn. Als alle Hallo pogingen mislukken, is Hallo verkeer gerouteerde toohello volgende beschikbare ingeschakeld voor de cloud-interface zoals wordt bepaald door het Hallo-routeringstabel. Als alle Hallo ingeschakeld voor de cloud netwerkinterfaces mislukken, wordt de Hallo apparaat failover toohello andere controller (opnieuw opstarten is niet in dit geval).
* Als er een VIP-fout voor een netwerkinterface met iSCSI-is ingeschakeld, zal er 3 nieuwe pogingen met een vertraging 2 seconden. Dit gedrag is gebleven Hallo dezelfde uit Hallo vorige versies. Als alle Hallo iSCSI-netwerkinterfaces mislukken, wordt een failover van de domeincontroller (vergezeld van de computer opnieuw is opgestart) optreden.
* Een waarschuwing wordt ook gegeven op uw StorSimple-apparaat wanneer er een VIP-fout. Voor meer informatie gaat te[Naslaggids waarschuwing](storsimple-manage-alerts.md).
* In termen van nieuwe pogingen voorrang iSCSI boven cloud.
  
    Overweeg het volgende voorbeeld Hallo: A StorSimple apparaat twee netwerkinterfaces die zijn ingeschakeld heeft, Data 0 en 1 van de gegevens. Data 0 is ingeschakeld voor de cloud terwijl Data 1 zowel cloud- en iSCSI-functionaliteit. Er zijn geen andere netwerkinterfaces op dit apparaat zijn ingeschakeld voor cloud- of iSCSI.
  
    Als gegevens 1 mislukt, krijgt het Hallo laatste iSCSI-netwerkinterface is, resulteert dit in een failover-controller tooData 1 op Hallo andere domeincontroller.

### <a name="networking-best-practices"></a>Aanbevolen procedures voor netwerken
Bovendien voldoen toohello boven de netwerkvereisten voor optimale prestaties van uw StorSimple-oplossing Hallo Neem toohello aanbevolen procedures te volgen:

* Zorg ervoor dat uw StorSimple-apparaat heeft een speciale 40 Mbps bandbreedte (of meer) beschikbaar te allen tijde. Deze bandbreedte mag niet worden gedeeld (of toewijzing moet worden gegarandeerd door het Hallo-gebruik van QoS-beleid) met andere toepassingen.
* Controleer network connectivity toohello Internet altijd beschikbaar is. Sporadisch of onbetrouwbare Internet-verbindingen toohello apparaten, waaronder zonder internetverbinding dan ook, resulteert in een niet-ondersteunde configuratie.
* Hallo iSCSI- en cloud-verkeer isoleren door een speciale netwerkinterfaces op uw apparaat voor toegang tot iSCSI- en cloud. Voor meer informatie Zie hoe te[netwerkinterfaces wijzigen](storsimple-modify-device-config.md#modify-network-interfaces) op uw StorSimple-apparaat.
* Gebruik geen een Link Aggregation Control Protocol (LACP)-configuratie voor uw netwerkinterfaces. Dit is een niet-ondersteunde configuratie.

## <a name="high-availability-requirements-for-storsimple"></a>Vereisten voor hoge beschikbaarheid voor StorSimple
Hallo hardwareplatform die is opgenomen in Hallo StorSimple-oplossing heeft beschikbaarheid en betrouwbaarheid van functies die kunnen worden gebruikt voor een maximaal beschikbare en fouttolerantie opslaginfrastructuur in uw datacenter. Echter zijn er vereisten en aanbevolen procedures die u aan de toohelp voldoen moet Hallo beschikbaarheid van uw StorSimple-oplossing te garanderen. Voordat u StorSimple implementeert, zorgvuldig door Hallo vereisten en best practices voor Hallo StorSimple-apparaat volgen en hostcomputers verbonden.

Voor meer informatie over het controleren en onderhouden van Hallo hardware-onderdelen van uw StorSimple-apparaat gaat te[gebruik Hallo StorSimple Manager-service toomonitor hardware-onderdelen en status](storsimple-monitor-hardware-status.md) en [StorSimple onderdeel Hardwarevervanging](storsimple-hardware-component-replacement.md).

### <a name="high-availability-requirements-and-procedures-for-your-storsimple-device"></a>Vereisten voor hoge beschikbaarheid en -procedures voor uw StorSimple-apparaat
Bekijk Hallo volgende informatie zorgvuldig tooensure Hallo hoge beschikbaarheid van uw StorSimple-apparaat.

#### <a name="pcms"></a>PCMs
StorSimple-apparaten zijn redundante, hot verwisselbare stroom en koeling modules (PCMs). Elke PCM heeft onvoldoende capaciteit tooprovide service voor de hele chassis Hallo. tooensure hoge beschikbaarheid, beide PCMs moet worden geïnstalleerd.

* Verbinding maken met uw PCMs toodifferent power bronnen tooprovide beschikbaarheid als een power-bron is mislukt.
* Als een PCM mislukt, vragen u een vervangende onmiddellijk.
* Verwijderen van een mislukte PCM alleen als u vervanging Hallo hebt en gereed tooinstall deze.
* Beide PCMs niet gelijktijdig verwijderen. Hallo PCM-module bevat Hallo back-up batterij module. Verwijderen van beide Hallo PCMs resulteert in een afsluiten zonder accu beveiliging en Apparaatstatus Hallo worden niet opgeslagen. Voor meer informatie over Hallo accu gaat te[onderhouden Hallo back-up batterij module](storsimple-battery-replacement.md#maintain-the-backup-battery-module).

#### <a name="controller-modules"></a>Controller modules
StorSimple-apparaten zijn redundante, hot verwisselbare controller modules. Hallo controller modules werken in een actief/passief-wijze. Op elk gewenst één module van de domeincontroller actief is en de service levert, tijdens het Hallo andere controllermodule passief is. Hallo passieve controller-module is ingeschakeld en werkt als Hallo actieve controller-module is mislukt of is verwijderd. Elke domeincontroller-module heeft onvoldoende capaciteit tooprovide service voor de hele chassis Hallo. Beide modules domeincontroller moet geïnstalleerde tooensure hoge beschikbaarheid.

* Zorg ervoor dat beide modules controller te allen tijde worden geïnstalleerd.
* Als een domeincontroller-module is mislukt, vragen u een vervangende onmiddellijk.
* Een mislukte controllermodule alleen verwijderd wanneer u Hallo vervanging hebt en gereed tooinstall deze. Verwijderen van een module gedurende langere perioden, heeft invloed op Hallo luchtstroom en daarom Hallo koeling van Hallo-systeem.
* Zorg ervoor dat Hallo netwerk verbindingen tooboth controller modules identiek zijn, en hello verbonden netwerkinterfaces een identieke netwerkconfiguratie hebben.
* Als een domeincontroller-module is mislukt of vervanging moet, zorgt u ervoor dat Hallo andere controllermodule is een actieve status voordat Hallo schijfcontroller module worden vervangen. een domeincontroller is actief en tooverify te gaan[identificeren Hallo actieve controller op uw apparaat](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Verwijder niet beide modules controller op Hallo hetzelfde moment. Als een domeincontroller failover uitgevoerd wordt, geen Hallo stand-by-controllermodule afgesloten of van Hallo chassis verwijderen.
* Na een failover van de domeincontroller, wacht ten minste vijf minuten voordat u een controllermodule verwijdert.

#### <a name="network-interfaces"></a>Netwerkinterfaces
StorSimple-apparaat controller modules elke hebben vier 1 Gigabit en twee 10 Gigabit Ethernet-netwerkinterfaces.

* Zorg ervoor dat Hallo netwerk verbindingen tooboth controller modules identiek zijn en Hallo netwerkinterfaces dat Hallo controller module interfaces verbonden toohave een identieke netwerkconfiguratie zijn.
* Indien mogelijk, implementeert u Netwerkverbindingen in verschillende switches tooensure servicebeschikbaarheid in geval van een netwerkfout apparaat Hallo.
* Wanneer ontkoppelen alleen Hallo of Hallo laatste resterende wordt ingeschakeld voor iSCSI-interface (met IP-adressen toegewezen,) Hallo interface eerst uitschakelen en haal Hallo kabels. Als het Hallo-interface is eerst losgekoppeld, treden vervolgens er Hallo actieve controller toofail via toohello passieve controller. Als Hallo passieve controller ook de bijbehorende interfaces losgekoppeld heeft, kunnen beide domeincontrollers hello wordt meerdere keren opnieuw voordat op een domeincontroller.
* Ten minste twee interfaces toohello gegevensnetwerk vanaf elke domeincontroller module verbinding te maken.
* Als u Hallo twee 10 GbE-interfaces hebt ingeschakeld, implementeert u de servers in verschillende switches.
* Gebruik zo mogelijk MPIO op servers tooensure dat Hallo servers een koppeling-, netwerk- of interfacefout kunnen tolereren.

Voor meer informatie over het netwerk van uw apparaat voor hoge beschikbaarheid en prestaties te gaan[uw StorSimple 8100-apparaat installeert](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) of [uw StorSimple 8600-apparaat installeert](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

#### <a name="ssds-and-hdds"></a>SSD en HDD 's
StorSimple-apparaten zijn Solid-State-schijven (SSD's) en harde schijven (HDD's) die zijn beveiligd met behulp van gespiegelde opslagruimten. Gebruik van gespiegelde ruimten zorgt ervoor dat het Hallo-apparaat kunnen tootolerate Hallo falen van een of meer SSD's of harde schijven.

* Zorg ervoor dat alle SSD en HDD-modules zijn geïnstalleerd.
* Als een SSD of harde schijf is mislukt, vragen u een vervangende onmiddellijk.
* Als een SSD of harde schijf mislukt of moet worden vervangen, ervoor zorgen dat u verwijdert Hallo SSD of harde schijf die moet worden vervangen.
* Verwijder niet meer dan één SSD of harde schijf van Hallo systeem op elk gewenst moment in de tijd.
  Een storing van 2 of meer schijven van een bepaald type (HDD, SSD) of opeenvolgende mislukt binnen een korte periode kan leiden tot gegevensverlies storing en potentiële system. Als dit gebeurt, [contact op met Microsoft Support](storsimple-contact-microsoft-support.md) voor hulp.
* Tijdens de vervanging, bewaken Hallo **hardwarestatus** in Hallo **onderhoud** pagina voor Hallo stations in Hallo SSD en HDD's. De status van een groen vinkje geeft aan dat Hallo schijven zijn in orde of OK, terwijl een rood uitroepteken wijst wijst op een mislukte SSD of harde schijf.
* Het is raadzaam dat u configureert cloudmomentopnamen voor alle volumes moet u tooprotect in geval van een systeemfout is opgetreden.

#### <a name="ebod-enclosure"></a>EBOD behuizing
StorSimple-Apparaatmodel 8600 bevat een uitgebreide Bunch van schijven (EBOD) behuizing toevoeging toohello primaire behuizing. Een EBOD bevat EBOD domeincontrollers en harde schijven (HDD's) die zijn beveiligd met behulp van gespiegelde opslagruimten. Gebruik van gespiegelde ruimten zorgt ervoor dat het Hallo-apparaat kunnen tootolerate Hallo falen van een of meer harde schijven. Hallo EBOD behuizing is verbonden toohello primaire behuizing door middel van redundante SAS-kabels.

* Zorg ervoor dat beide EBOD behuizing controller modules, SAS-kabels en alle Hallo harde schijven te allen tijde worden geïnstalleerd.
* Als een EBOD behuizing controller-module is mislukt, vragen u een vervangende onmiddellijk.
* Als een EBOD behuizing controller-module is mislukt, zorg ervoor dat Hallo andere module van de domeincontroller actief is voordat u de mislukte module Hallo vervangt. een domeincontroller is actief en tooverify te gaan[identificeren Hallo actieve controller op uw apparaat](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device).
* Tijdens een EBOD controller module-vervanging continu Hallo status controleren van hello onderdeel in Hallo StorSimple Manager-service door het openen van **onderhoud** > **hardwarestatus**.
* Als een SAS-kabel mislukt of moet worden vervangen (Microsoft Support moet betrokken toomake dergelijke vaststelling), zorg er dan voor dat u alleen Hallo SAS-kabel die moet worden vervangen.
* Gelijktijdig Verwijder niet beide SAS-kabels uit Hallo systeem op elk punt in tijd.

### <a name="high-availability-recommendations-for-your-host-computers"></a>Aanbevelingen voor hoge beschikbaarheid voor uw hostcomputers
Zorgvuldig door deze best practices tooensure Hallo hoge beschikbaarheid van hosts verbonden tooyour StorSimple-apparaat.

* Configureren van StorSimple met [twee knooppunten cluster bestandsserverconfiguraties][1]. Individuele foutpunten fout en opbouw in redundantie Hallo host zijde wordt verwijderd, wordt de hele oplossing Hallo maximaal beschikbaar.
* Voortdurend beschikbare shares voor (CA) beschikbaar in Windows Server 2012 (SMB 3.0) gebruiken voor maximale beschikbaarheid tijdens de failover van de opslagcontrollers Hallo. Raadpleeg voor aanvullende informatie voor het configureren van bestandsserverclusters en voortdurend beschikbare shares met Windows Server 2012 toothis [video demo](http://channel9.msdn.com/Events/IT-Camps/IT-Camps-On-Demand-Windows-Server-2012/DEMO-Continuously-Available-File-Shares).

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over limieten voor StorSimple-systeem](storsimple-limits.md).
* [Meer informatie over hoe toodeploy uw StorSimple-oplossing](storsimple-deployment-walkthrough-u2.md).

<!--Reference links-->
[1]: https://technet.microsoft.com/library/cc731844(v=WS.10).aspx

---
title: aaaLog gegevensbeveiliging Analytics | Microsoft Docs
description: Meer informatie over hoe logboekanalyse beschermt u uw privacy en uw gegevens beveiligt.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: a33bb05d-b310-4f2c-8f76-f627e600c8e7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/03/2017
ms.author: magoedte
ms.openlocfilehash: 130b59f22fc3dd249f32717367cc62ea25c55a21
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-data-security"></a>Meld u Analytics-gegevensbeveiliging
Microsoft is doorgevoerd tooprotecting uw privacy en beveiliging van uw gegevens tijdens de levering van software en services die u helpen Hallo IT-infrastructuur van uw organisatie beheren. We erkennen dat wanneer u uw gegevens tooothers belasten, vertrouwensrelatie strengere beveiliging vereist. Microsoft toostrict naleving en beveiliging richtlijnen voldoet, van een service toooperating coderen.

Beveiliging en bescherming van gegevens is een topprioriteit bij Microsoft. Neem contact met ons met eventuele vragen, suggesties of problemen met betrekking tot een van de volgende informatie, met inbegrip van ons beveiligingsbeleid op Hallo [Azure ondersteuningsopties](http://azure.microsoft.com/support/options/).

Dit artikel wordt uitgelegd hoe gegevens die worden verzameld, verwerkt en beveiligd door logboekanalyse in Hallo Operations Management Suite (OMS). U kunt agents tooconnect toohello webservice gebruiken, gebruik van System Center Operations Manager toocollect operationele gegevens of gegevens ophalen uit Azure diagnostics voor gebruik door logboekanalyse. Hallo verzamelde gegevens worden verzonden via Internet Hallo met certificaten gebaseerde verificatie en SSL 3 toohello Log Analytics-service, die wordt gehost door Microsoft Azure. Gegevens worden gecomprimeerd door Hallo agent voordat deze wordt verzonden.

Hallo Log Analytics-service beheert uw cloud-gebaseerde gegevens veilig door Hallo volgende methoden:

* gegevensscheiding
* bewaren van gegevens
* Fysieke beveiliging
* Incidentbeheer
* Naleving
* standaarden veiligheidscertificaten

## <a name="data-segregation"></a>gegevensscheiding
Gegevens van de klant is geïsoleerd logisch op elk onderdeel in de gehele Hallo OMS-service. Alle gegevens worden gemarkeerd per organisatie. Deze labels zich blijft voordoen gedurende de levenscyclus van Hallo gegevens en het wordt afgedwongen op elke laag van Hallo-service. Elke klant heeft een specifieke Azure blob met lange-termijngegevens bewaard Hallo

## <a name="data-retention"></a>Bewaartijd van gegevens
Geïndexeerde logboekgegevens zoekopdracht wordt opgeslagen en bewaard volgens tooyour plan prijzen. Zie voor meer informatie [Log Analytics prijzen](https://azure.microsoft.com/pricing/details/log-analytics/).

Microsoft verwijdert klantgegevens 30 dagen nadat Hallo OMS-werkruimte is gesloten. Microsoft verwijdert tevens hello Azure Storage-Account waarin Hallo gegevens zich bevindt. Wanneer gegevens van de klant wordt verwijderd, worden er geen fysieke schijven vernietigd.

Hallo volgende tabel vindt u enkele van de beschikbare oplossingen Hallo in OMS en voorbeelden Hallo typen gegevens die zij verzamelen.

| **Oplossing** | **Gegevenstypen** |
| --- | --- |
| Configuratie-evaluatie |Configuratiegegevens, metagegevens en gegevens van de gebruikersstatus |
| Capaciteitsplanning |Prestatiegegevens en metagegevens |
| Antimalware |Configuratiegegevens en metagegevens |
| Evaluatie voor systeemupdate |Metagegevens en de statusgegevens |
| Logboekbeheer |Gebruiker gedefinieerde gebeurtenislogboeken, Windows-gebeurtenislogboeken en/of de IIS-logboeken |
| Tracering wijzigen |Software-inventaris en metagegevens van de Windows-Service |
| SQL- en beoordeling van de Active Directory |WMI-gegevens, registergegevens, prestatiegegevens en SQL Server dynamische Beheerweergave resultaten weergeven |

Hallo volgende tabel ziet u voorbeelden van gegevenstypen:

| **Gegevenstype** | **Velden** |
| --- | --- |
| Waarschuwing |Waarschuwing naam, beschrijving van de waarschuwing, BaseManagedEntityId, probleem-ID, IsMonitorAlert, RuleId, oplossingsstatus, prioriteit, ernst, categorie, eigenaar, ResolvedBy, TimeRaised, TimeAdded, LastModified, LastModifiedBy, LastModifiedExceptRepeatCount, TimeResolved, TimeResolutionStateLastModified, TimeResolutionStateLastModifiedInDB, RepeatCount |
| Configuratie |CustomerID, AgentID, id van de entiteit, ManagedTypeID, ManagedTypePropertyID, CurrentValue, ChangeDate |
| Gebeurtenis |Gebeurtenis-id, EventOriginalID, BaseManagedEntityInternalId, RuleId, PublisherId, PublisherName, FullNumber, getal, categorie, ChannelLevel, LoggingComputer, EventData, EventParameters, TimeGenerated, TimeAdded <br>**Opmerking:** bij het schrijven van gebeurtenissen met aangepaste velden in de Windows-gebeurtenislogboek toohello OMS ze verzamelt. |
| Metagegevens |BaseManagedEntityId, ObjectStatus, OrganizationalUnit, ActiveDirectoryObjectSid, PhysicalProcessors, NetworkName, IP-adres, ForestDNSName, NetbiosComputerName, VirtualMachineName, LastInventoryDate, HostServerNameIsVirtualMachine, IP-adres, NetbiosDomainName, LogicalProcessors, DNSName, DisplayName, DomainDnsName, ActiveDirectorySite, primaire naam, OffsetInMinuteFromGreenwichTime |
| Prestaties |Objectnaam, CounterName, PerfmonInstanceName, PerformanceDataId, PerformanceSourceInternalID, SampleValue, TimeSampled, TimeAdded |
| Status |StateChangeEventId, StateId, NewHealthState, OldHealthState, Context, TimeGenerated, TimeAdded, StateId2, BaseManagedEntityId, MonitorId, HealthState, LastModified, LastGreenAlertGenerated, DatabaseTimeModified |

## <a name="physical-security"></a>Fysieke beveiliging
Hallo logboekanalyse in OMS-service is bemand door medewerkers van Microsoft en alle activiteiten die worden geregistreerd en kunnen worden gecontroleerd. Hallo-service volledig in Azure wordt uitgevoerd en voldoet aan de hello Azure gemeenschappelijke technische criteria. U kunt details over Hallo fysieke beveiliging van Azure activa weergeven op pagina 18 Hallo [beveiligingsoverzicht van Microsoft Azure](http://download.microsoft.com/download/6/0/2/6028B1AE-4AEE-46CE-9187-641DA97FC1EE/Windows%20Azure%20Security%20Overview%20v1.01.pdf). Fysieke toegang rechten toosecure gebieden worden gewijzigd binnen één werkdag voor iedereen die de verantwoordelijkheid voor Hallo OMS-service, inclusief de overdracht en beëindiging beschikt niet langer over. U kunt meer informatie over Hallo globale fysieke infrastructuur gebruiken we op [Microsoft-Datacenters](https://www.microsoft.com/en-us/server-cloud/cloud-os/global-datacenters.aspx).

## <a name="incident-management"></a>Incidentbeheer
OMS heeft een incidentbeheerproces die voor alle Microsoft-services worden aangehouden. toosummarize, we:

* Gebruik een gedeelde verantwoordelijkheid model waarin een deel van de beveiliging verantwoordelijkheid tooMicrosoft en een gedeelte behoort behoort toohello klant
* Azure-beveiligingsincidenten beheren
  * Start een onderzoek na detectie van een incident
  * Hallo impact en urgentie van een incident door een teamlid voor respons op incidenten op oproep beoordelen. Op basis van bewijs, Hallo assessment kan of kan niet resulteren in meer escalatie toohello antwoord beveiligingsteam.
  * Diagnose van een incident door beveiliging antwoord experts tooconduct Hallo technische of forensisch onderzoek, containment risicobeperking en tijdelijke oplossing strategieën identificeren. Als het beveiligingsteam Hallo gelooft dat gegevens van de klant mogelijk niet meer weergegeven tooan onrechtmatig of niet-geautoriseerde begint afzonderlijke, parallelle uitvoering van de klant Incident meldingen Hallo parallel.  
  * Regulering en het herstellen van Hallo incident. Hallo respons op incidenten team maakt een herstel plan toomitigate Hallo probleem. Crisis containment stappen zoals betrokken systemen in quarantaine plaatsen kunnen optreden onmiddellijk en parallel met diagnose. Langer term oplossingen kunnen worden gepland die zich voordoen nadat Hallo onmiddellijke risico is verstreken.  
  * Hallo incident sluit en een post-keuring uitvoeren. Hallo respons op incidenten team maakt een post-keuring waarin Hallo details van Hallo incident, Hallo voornemen toorevise beleidsregels, procedures en processen tooprevent herhaling van Hallo-gebeurtenis.
* Gebruikers informeren over beveiligingsincidenten
  * Hallo-bereik van de betrokken klanten en tooprovide iedereen die wordt beïnvloed, zoals een aankondiging mogelijk gedetailleerde bepalen
  * Een aankondiging tooprovide klanten maken met gedetailleerde genoeg gegevens zodat ze kunnen een onderzoek op hun einde uitvoeren en voldoen aan eventuele wanneer die zij eindgebruikers tootheir gemaakt hebben tijdens het Hallo meldingsproces niet ten onrechte vertragen.
  * Bevestig en declareren Hallo incident, indien nodig.
  * Klanten met een incident melding zonder onredelijk vertraging en in overeenstemming met alle juridische of contractueel streven informeren. Meldingen van beveiligingsincidenten worden tooone of meer van de beheerders van een klant geleverd door middel van Microsoft selecteert, inclusief via e-mail.
* Gedragscode team gereedheid voor en training
  * Medewerkers van Microsoft zijn vereiste toocomplete beveiligings- en awareness training, waardoor ze tooidentify en in het rapport vermoed beveiligingsproblemen.  
  * Operators op Hallo van Microsoft Azure-service werkt hebben toevoeging training verplichtingen omringende hun toegang toosensitive systemen die als host fungeert voor gegevens van de klant.
  * Medewerkers van Microsoft security response ontvangen speciale training voor hun rollen

Als het verlies van enige klantgegevens optreedt, wordt elke klant melden binnen één dag. Klant-gegevensverlies opgetreden echter nooit met OMS. Bovendien we kopieën van gegevens die zijn gemaakt en geografisch wordt gedistribueerd.

Zie voor meer informatie over hoe Microsoft toosecurity incidenten reageert [reactie van Microsoft Azure-beveiliging in Hallo Cloud](https://gallery.technet.microsoft.com/Azure-Security-Response-in-dd18c678/file/150826/1/Microsoft Azure Security Response in hello cloud.pdf).

## <a name="compliance"></a>Naleving
Hallo OMS software ontwikkelings- en service van het team informatiebeveiliging en governance programma ondersteunt de zakelijke vereisten en toolaws en -voorschriften voldoet zoals beschreven op [Microsoft Azure Trust Center](https://azure.microsoft.com/support/trust-center/) en [Microsoft Trust Center naleving](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx). Hoe OMS beveiligingsvereisten vaststelt, identificeert beveiligingsmechanismen beheert en bewaakt de risico's worden er ook beschreven. Jaarlijks, wij controleren beleidsregels, standaarden, procedures en richtlijnen.

Elk teamlid OMS-ontwikkeling ontvangt beveiligingstraining formele toepassing. We gebruiken een versiebeheersysteem intern voor softwareontwikkeling. Elk software-project wordt beveiligd door Hallo versiebeheersysteem.

Microsoft heeft een beveiliging en naleving team dat verantwoordelijk en alle services in Microsoft evalueert. Informatie-afdelingen gezamenlijk Hallo team en niet zijn gekoppeld met Hallo engineering afdelingen die OMS ontwikkelen. Hallo-afdelingen hebben hun eigen Managementketen en uitvoering van een onafhankelijke beoordelingen van producten en services tooensure-beveiliging en naleving.

Raad van bestuur van Microsoft is een melding via een jaarlijkse rapport over alle informatie beveiligingsprogramma's bij Microsoft.

Hallo OMS software ontwikkelings- en team werkt actief met Hallo Microsoft Legal en naleving teams en andere branche partners tooacquire verschillende certificeringen.

## <a name="certifications-and-attestations"></a>Certificaten en verklaringen
OMS Log Analytics aan Hallo volgens de vereisten voldoet:

* [ISO/IEC 27001](http://www.iso.org/iso/home/standards/management-standards/iso27001.htm)
* [ISO/IEC 27018:2014](http://www.iso.org/iso/home/store/catalogue_tc/catalogue_detail.htm?csnumber=61498)
* [ISO 22301](https://azure.microsoft.com/en-us/blog/iso22301/)
* [Payment Card Industry (PCI conform) Data Security Standard (PCI DSS)](https://www.microsoft.com/en-us/TrustCenter/Compliance/PCI) door Hallo PCI Security Standards Council.
* [Type service organisatie besturingselementen (SOC) 1 1 en SOC 2 Type 1](https://www.microsoft.com/en-us/TrustCenter/Compliance/SOC1-and-2) compatibel
* [HIPAA en HITECH](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA) voor bedrijven die een HIPAA-overeenkomst voor het koppelen van bedrijven hebben
* Windows gemeenschappelijke Engineering Criteria
* Microsoft Trustworthy Computing
* Als een Azure-service voldoen Hallo-onderdelen die gebruikmaakt van OMS tooAzure nalevingsvereisten. U vindt meer op [Microsoft Trust Center naleving](https://www.microsoft.com/en-us/TrustCenter/Compliance/default.aspx).

> [!NOTE]
> In sommige certificeringen/verklaringen Log Analytics wordt vermeld onder de oude naam van *Operational Insights*.
>
>


## <a name="cloud-computing-security-data-flow"></a>Cloudcomputing beveiliging gegevensstroom
Hallo volgende diagram ziet u een cloud-beveiligingsarchitectuur als Hallo stroom van gegevens van uw bedrijf en hoe deze worden beveiligd omdat verplaatst toohello Log Analytics-service, die uiteindelijk bekijken door u in Hallo OMS-portal. Meer informatie over elke stap volgt Hallo-diagram.

![Afbeelding van OMS-gegevensverzameling en -beveiliging](./media/log-analytics-security/log-analytics-security-diagram.png)

## <a name="1-sign-up-for-log-analytics-and-collect-data"></a>1. Aanmelden voor logboekanalyse en gegevens verzamelen
Bij uw organisatie toosend gegevens tooLog Analytics configureert u Windows-agents, agents die worden uitgevoerd op Azure virtual machines of OMS-Agents voor Linux. Als u Operations Manager-agents gebruikt, wordt u de wizard een configuratie in Hallo Operations-console tooconfigure gebruiken ze. Gebruikers (dit is mogelijk u afzonderlijke gebruikers of een groep personen) een of meer OMS-accounts (OMS-werkruimten) maken en registreren van agents met behulp van een van de volgende accounts Hallo:

* [Organisatie-ID](../active-directory/sign-up-organization.md)
* [Microsoft-Account - Outlook, Office Live, MSN](http://www.microsoft.com/account/default.aspx)

Een OMS-werkruimte is de gegevens wordt verzameld, samengevoegd, geanalyseerd en gepresenteerd. Een werkruimte wordt voornamelijk gebruikt als een manier toopartition gegevens en elke werkruimte uniek is. Bijvoorbeeld, kunt u uw productiegegevens beheerd met een OMS-werkruimte en de testgegevens beheerd met een andere werkruimte toohave. Werkruimten kunnen ook een beheerder besturingselement toegang toohello gebruikersgegevens. Elke werkruimte kan meerdere gebruikersaccounts die zijn gekoppeld, en elke gebruikersaccount hebben toegang tot meerdere OMS werkruimten. U maakt op basis van regio datacenter werkruimten. Elke werkruimte is gerepliceerde tooother datacenters op Hallo regio, hoofdzakelijk voor de beschikbaarheid van de OMS-service.

Voor Operations Manager, wanneer het Hallo-configuratiewizard is voltooid, maakt elke Operations Manager-beheergroep verbinding met een Hallo Log Analytics-service. Vervolgens gebruikt u Hallo Computers Wizard toevoegen toochoose welke computers in de beheergroep Hallo toosend toohello gegevensservice zijn toegestaan. Voor andere typen agent verbindt elk veilig toohello OMS-service.

Alle communicatie tussen verbonden systemen en Hallo Log Analytics-service is versleuteld.  Hallo TLS wordt-protocol (HTTPS) gebruikt voor versleuteling.  Hallo Microsoft SDL-proces wordt gevolgd tooensure logboekanalyse is bijgewerkt door de meest recente ontwikkelingen Hallo in cryptografische protocollen.

Elk type agent verzamelt gegevens voor logboekanalyse. Hallo soort gegevens die worden verzameld is afhankelijk van Hallo typen oplossingen die worden gebruikt. U ziet een overzicht van het verzamelen van gegevens op [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md). Meer gedetailleerde informatie van de verzameling is daarnaast beschikbaar voor de meeste oplossingen. Een oplossing is een bundel van vooraf gedefinieerde weergaven, logboek zoekquery's, regels voor het verzamelen van gegevens en logica voor verwerking. Alleen beheerders kunnen logboekanalyse tooimport een oplossing gebruiken. Nadat het Hallo-oplossing wordt geïmporteerd, is het verplaatste toohello Operations Manager-beheerservers (indien gebruikt) en tooany agents die u hebt gekozen. Daarna wordt er Hallo agents Hallo gegevens verzameld.

## <a name="2-send-data-from-agents"></a>2. Verzenden van gegevens van agents
U alle typen van de agent met een sleutel inschrijving registreren en een beveiligde verbinding tot stand is gebracht tussen Hallo agent en Hallo Log Analytics-service die certificaten gebaseerde verificatie en SSL met poort 443 gebruikt. OMS maakt gebruik van een geheime store toogenerate en onderhouden van sleutels. Persoonlijke sleutels om de 90 dagen worden gedraaid en in Azure worden opgeslagen en worden beheerd door hello Azure bewerkingen die strikt regelgeving en naleving procedures te volgen.

Met Operations Manager registreren van een werkruimte met Hallo Log Analytics-service en een beveiligde HTTPS-verbinding tot stand is gebracht tussen Hallo Operations Manager-beheerserver.

Voor Windows-agents uitgevoerd op virtuele machines in Azure, is een alleen-lezen-opslagsleutel gebruikte tooread diagnostische gebeurtenissen in Azure-tabellen.

Als een agent kan geen toocommunicate toohello service voor een of andere reden, hello verzamelde gegevens lokaal is opgeslagen in een tijdelijke cache en Hallo beheerserver probeert tooresend Hallo gegevens elke acht minuten gedurende 2 uur. gegevens in de cache van Hallo-agent wordt beveiligd door de referentie-archief Hallo van het besturingssysteem. Als Hallo kan niet worden verwerkt Hallo gegevens na twee uur, wachtrij Hallo agents Hallo-gegevens. Als Hallo wachtrij vol is, start OMS gegevenstypen, beginnend met prestatiegegevens neer te zetten. Hallo agent wachtrijlimiet is een registersleutel, zodat u kunt, indien nodig wijzigen. Verzamelde gegevens wordt gecomprimeerd en toohello service, het omzeilen van lokale databases, dus geen eventuele toothem load voegt verzonden. Nadat Hallo verzamelde gegevens worden verzonden, wordt deze verwijderd uit het Hallo-cache.

Zoals hierboven wordt beschreven, worden gegevens van uw agents worden verzonden via SSL tooMicrosoft Azure-datacenters. Desgewenst kunt u ExpressRoute tooprovide extra beveiliging voor Hallo-gegevens. ExpressRoute is een toodirectly manier verbinding tooAzure vanaf uw eigen WAN-netwerk, zoals een multiprotocol label switching (MPLS) VPN, geleverd door een netwerkserviceprovider. Zie voor meer informatie [ExpressRoute](https://azure.microsoft.com/services/expressroute/).

## <a name="3-hello-log-analytics-service-receives-and-processes-data"></a>3. Hallo Log Analytics-service ontvangt en verwerkt gegevens
Hallo-logboekanalyseservice zorgt ervoor dat binnenkomende gegevens van een vertrouwde bron door het valideren van certificaten en Hallo de integriteit van gegevens met Azure-verificatie. Hello onverwerkte onbewerkte gegevens worden vervolgens opgeslagen als een blob in [Microsoft Azure Storage](../storage/common/storage-introduction.md) en is niet versleuteld. Elke Azure-opslag-blob heeft echter een set unieke set van sleutels, is toegankelijk alleen toothat gebruiker. Hallo soort gegevens die zijn opgeslagen, is afhankelijk van Hallo typen oplossingen die zijn geïmporteerd en toocollect gegevens gebruikt. Hallo Log Analytics-service verwerkt vervolgens Hallo onbewerkte gegevens voor hello Azure storage-blob.

## <a name="4-use-log-analytics-tooaccess-hello-data"></a>4. Log Analytics tooaccess Hallo gegevens gebruiken
U kunt tooLog Analytics in Hallo OMS-portal aanmelden met behulp van Hallo organisatieaccount of Microsoft-account dat u eerder hebt ingesteld. Al het verkeer tussen Hallo OMS-portal en Log Analytics in OMS wordt verzonden via een beveiligd kanaal voor HTTPS. Wanneer u Hallo OMS-portal, een sessie-ID is gegenereerd op Hallo gebruiker client (webbrowser) en gegevens worden opgeslagen in een lokale cache totdat Hallo-sessie wordt beëindigd. Wanneer is beëindigd, wordt de Hallo cache verwijderd. Client-side cookies, die geen persoonsgegevens bevatten, worden niet automatisch verwijderd. Sessiecookies HTTPOnly zijn gemarkeerd en zijn beveiligd. Na een vooraf bepaalde niet-actieve periode wordt Hallo OMS-portal sessie beëindigd.

Hallo OMS-portal gebruikt, kunt u gegevens tooa CSV-bestand exporteren en u toegang hebt tot gegevens via zoeken-API's. CSV-export is beperkt too50. 000 rijen per exporteren en API-gegevens wordt beperkt too5, 000 rijen per zoeken.

## <a name="next-steps"></a>Volgende stappen
* [Aan de slag met logboekanalyse](log-analytics-get-started.md) toolearn meer over Log Analytics en get up-to-date en worden uitgevoerd in minuten.

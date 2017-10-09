---
title: aaaDNS Analytics-oplossing in Azure Log Analytics | Microsoft Docs
description: Instellen en gebruiken van Hallo DNS Analytics-oplossing in logboekanalyse toogather inzicht in de DNS-infrastructuur op beveiliging, prestaties en bewerkingen.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f44a40c4-820a-406e-8c40-70bd8dc67ae7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: be7982c54b65ba0c4b1c15ae7516d02eced313f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="gather-insights-about-your-dns-infrastructure-with-hello-dns-analytics-preview-solution"></a>Inzicht in uw DNS-infrastructuur met DNS-Analytics Preview oplossing Hallo verzamelen

![DNS-Analytics symbool](./media/log-analytics-dns/dns-analytics-symbol.png)

Dit artikel wordt beschreven hoe hello Azure DNS-Analytics-oplossing in Azure-logboekanalyse toogather inzicht in de DNS-infrastructuur op beveiliging, prestaties en bewerkingen tooset up en het gebruik.

DNS-Analytics helpt u bij:

- Clients die tooresolve schadelijke domeinnamen proberen identificeren.
- Identificeer bronrecords.
- Vaak worden aangevraagd domeinnamen en interactie DNS-clients te identificeren.
- Weergave werklast op DNS-servers.
- Dynamische DNS-registratiefouten weergeven.

Hallo oplossing verzamelt, analyseert en correleert Windows DNS-analyse en controlelogboeken en andere gerelateerde gegevens uit uw DNS-servers.

## <a name="connected-sources"></a>Verbonden bronnen

Hallo volgende tabel beschrijft Hallo verbonden gegevensbronnen die worden ondersteund door deze oplossing:

| **Verbonden bron** | **Ondersteuning** | **Beschrijving** |
| --- | --- | --- |
| [Windows-agents](log-analytics-windows-agents.md) | Ja | Hallo oplossing verzamelt DNS-informatie van Windows-agents. |
| [Linux-agents](log-analytics-linux-agents.md) | Nee | Hallo oplossing verzamelt geen DNS-informatie van directe Linux-agents. |
| [System Center Operations Manager-beheergroep](log-analytics-om-agents.md) | Ja | Hallo oplossing verzamelt DNS-gegevens van agents in een verbonden beheergroep van Operations Manager. Een rechtstreekse verbinding tussen Hallo Operations Manager-agent toohello Operations Management Suite is niet vereist. Gegevens doorgestuurd vanuit Hallo management groep toohello Operations Management Suite-opslagplaats. |
| [Azure Storage-account](log-analytics-azure-storage.md) | Nee | Azure-opslag wordt niet gebruikt door Hallo-oplossing. |

### <a name="data-collection-details"></a>Details van de verzameling gegevens

Hallo oplossing verzamelt inventaris van de DNS- en DNS-gebeurtenissen gerelateerde gegevens uit Hallo DNS-servers waarop een Log Analytics-agent is geïnstalleerd. Deze gegevens vervolgens geüpload tooLog Analytics en weergegeven in het dashboard van de oplossing Hallo is. Inventarisatie-gerelateerde gegevens, zoals Hallo aantal DNS-servers, zones en bronrecords, is verzameld door het uitvoeren van Hallo DNS PowerShell-cmdlets. Hallo-gegevens bijgewerkt om de twee dagen. Hallo gebeurtenissen gerelateerde gegevens worden verzameld bijna realtime van Hallo [analytische en controlelogboeken](https://technet.microsoft.com/library/dn800669.aspx#enhanc) geleverd door verbeterde DNS-logboekregistratie en diagnostische gegevens in Windows Server 2012 R2.

## <a name="configuration"></a>Configuratie

Gebruik Hallo informatie tooconfigure Hallo oplossing te volgen:

- U moet hebben een [Windows](log-analytics-windows-agents.md) of [Operations Manager](log-analytics-om-agents.md) -agent op elke DNS-server die u toomonitor wilt.
- U kunt uit Hallo Hallo Analytics DNS-oplossing tooyour Operations Management Suite-werkruimte toevoegen [Azure Marketplace](https://aka.ms/dnsanalyticsazuremarketplace). U kunt ook Hallo procedure beschreven in [toevoegen Log Analytics-oplossingen van Hallo galerie met oplossingen](log-analytics-add-solutions.md).

Hallo oplossing start verzamelen van gegevens zonder Hallo van verdere configuratie. U kunt echter Hallo na verzameling van serverconfiguratiegegevens toocustomize gebruiken.

### <a name="configure-hello-solution"></a>Hallo-oplossing configureren

Klik op het dashboard van de oplossing hello, **configuratie** tooopen Hallo configuratie van de DNS-pagina. Er zijn wijzigingen in de configuratie die u kunt twee typen:

- **Goedgekeurde lijst van domeinnamen**. Hallo oplossing verwerkt geen alle Hallo lookup-query's. Een whitelist domeinnaamachtervoegsels houdt. Hallo lookup-query's die toohello domeinnamen ophalen die overeenkomen met domeinnaamachtervoegsels in deze lijst met geaccepteerde niet zijn verwerkt door Hallo-oplossing. Niet verwerken van domeinnamen wilt plaatsen, kunt u toooptimize Hallo gegevens verzonden tooLog Analytics. Hallo standaard geaccepteerde bevat populaire openbare domein-namen, zoals www.google.com en www.facebook.com. U kunt de volledige standaardlijst Hallo weergeven door schuiven.

 U kunt Hallo lijst tooadd het achtervoegsel van een naam die u wilt dat tooview lookup insights voor wijzigen. U kunt ook het achtervoegsel van een naam die u niet wilt dat tooview lookup insights voor verwijderen.

- **Interactie Client drempelwaarde**. DNS-clients die Hallo drempelwaarde overschrijden voor Hallo aantal lookup-aanvragen zijn gemarkeerd in Hallo **DNS-Clients** blade. Hallo drempelwaarde is standaard 1000. U kunt Hallo drempelwaarde bewerken.

    ![Goedgekeurde lijst domeinnamen](./media/log-analytics-dns/dns-config.png)

## <a name="management-packs"></a>Management packs

Als u van Hallo Microsoft Monitoring Agent tooconnect tooyour Operations Management Suite-werkruimte gebruikmaakt, hello volgende management pack is geïnstalleerd:

- Microsoft DNS-gegevens Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)

Als uw Operations Manager-beheergroep verbonden tooyour Operations Management Suite-werkruimte, worden hello volgende management packs geïnstalleerd in Operations Manager als u deze oplossing toevoegt. Er is geen vereiste configuratie of onderhoud van deze management packs:

- Microsoft DNS-gegevens Collector Intelligence Pack (Microsft.IntelligencePacks.Dns)
- Microsoft System Center Advisor DNS-configuratie (Microsoft.IntelligencePack.Dns.Configuration)

Zie voor meer informatie over hoe de oplossing management packs worden bijgewerkt, [verbinding maken met Operations Manager tooLog Analytics](log-analytics-om-agents.md).

## <a name="use-hello-dns-analytics-solution"></a>Hallo DNS Analytics-oplossing gebruiken

Deze sectie wordt uitgelegd alle Hallo dashboard functies en hoe toouse ze.

Nadat u Hallo oplossing tooyour werkruimte hebt toegevoegd, biedt Hallo oplossing tegel op Hallo Operations Management Suite overzichtspagina een snel overzicht van de DNS-infrastructuur. Het bevat aantal DNS-servers waar Hallo worden gegevens verzameld Hallo. Dit omvat ook Hallo aantal aanvragen door clients tooresolve schadelijke domeinen in Hallo afgelopen 24 uur. Wanneer u Hallo tegel klikt, wordt Hallo oplossing dashboard wordt geopend.

![DNS-Analytics tegel](./media/log-analytics-dns/dns-tile.png)

### <a name="solution-dashboard"></a>Dashboard van de oplossing

Hallo oplossing dashboard toont samenvattingsgegevens voor Hallo verschillende functies van Hallo-oplossing. Het bevat ook koppelingen toohello gedetailleerde weergave voor forensische analyse en diagnose. Standaard Hallo gegevens worden weergegeven voor Hallo afgelopen zeven dagen. U kunt de datum en tijd bereik Hallo wijzigen met behulp van Hallo **van datum / tijd-Selectiebesturingselement**, zoals weergegeven in Hallo installatiekopie te volgen:

![Besturingselement van de selectie tijd](./media/log-analytics-dns/dns-time.png)

Hallo oplossing dashboard ziet Hallo blades te volgen:

**DNS-beveiliging**. Rapporten Hallo DNS-clients die toocommunicate met schadelijke domeinen probeert. Met behulp van Microsoft threat intelligence feeds kunt Analytics DNS client-IP-adressen die probeert tooaccess schadelijke domeinen detecteren. In veel gevallen Hallo malware geïnfecteerde apparaten 'bellen' toohello 'opdracht en controle' center van Hallo schadelijke domein door het oplossen van malware-domeinnaam.

![Blade van DNS-beveiliging](./media/log-analytics-dns/dns-security-blade.png)

Wanneer u een client-IP in Hallo lijst klikt, wordt logboek zoekopdracht wordt geopend en Hallo lookup worden details weergegeven van de respectieve query Hallo. Hallo voorbeeld te volgen, DNS-Analytics aangetroffen dat Hallo-communicatie is klaar met een [IRCbot](https://www.microsoft.com/security/portal/threat/encyclopedia/entry.aspx?Name=Win32/IRCbot):

![Logboek zoekresultaten ircbot weergeven](./media/log-analytics-dns/ircbot.png)

Hallo informatie helpt u bij tooidentify de:

- Client-IP dat Hallo communicatie gestart.
- De domeinnaam die wordt omgezet toohello schadelijke IP.
- IP-adressen die domeinnaam Hallo wordt omgezet in.
- Schadelijke IP-adres.
- Ernst van Hallo probleem.
- De reden voor het beleid Hallo schadelijke IP.
- Tijd van de detectie.

**Domeinen die zijn opgevraagd**. Biedt Hallo meest voorkomende domeinnamen door Hallo DNS-clients in uw omgeving wordt opgevraagd. U kunt de lijst van alle Hallo domeinnamen opgevraagd Hallo weergeven. U kunt ook inzoomen op gegevens voor de Hallo lookup-aanvraag van een specifieke domeinnaam in het logboek zoeken.

![Domeinen opgevraagde blade](./media/log-analytics-dns/domains-queried-blade.png)

**DNS-Clients**. Rapporten Hallo clients *inbreuken Hallo drempelwaarde* voor het aantal query's in Hallo gekozen periode. U kunt Hallo-lijst van alle Hallo DNS-clients en Hallo details van Hallo query's die door deze in het logboek zoeken weergeven.

![Blade van DNS-Clients](./media/log-analytics-dns/dns-clients-blade.png)

**Dynamische DNS-registraties**. Rapportnaam registratiefouten. Alle registratiefouten voor adres [bronrecords](https://en.wikipedia.org/wiki/List_of_DNS_record_types) (Type A en AAAA) samen met de Hallo client IP-adressen die Hallo registratieverzoeken worden gemarkeerd. Vervolgens kunt u deze informatie toofind Hallo hoofdoorzaak van Hallo Registratiefout gebruiken met de volgende stappen:

1. Hallo-zone die is gemachtigd voor Hallo-naam die Hallo van client probeert tooupdate vinden

2. Hallo oplossing toocheck Hallo-inventarisgegevens van deze zone gebruiken.

3. Controleer of u die dynamische updates Hallo voor Hallo zone is ingeschakeld.

4. Controleer of Hallo zone voor beveiligde dynamische updates is geconfigureerd of niet.

    ![Blade voor dynamische DNS-registratie](./media/log-analytics-dns/dynamic-dns-reg-blade.png)

**Naam van de van registratieaanvragen**. Hallo bovenste tegel ziet u een trendlijn van geslaagde en mislukte DNS-aanvragen voor dynamische updates. Hallo lagere tegel vermeldt Hallo top 10-clients die toohello DNS-servers verzendt, gesorteerd op basis van het aantal mislukte Hallo mislukte aanvragen voor DNS-updates.

![De naam van registratie van aanvragen-blade ](./media/log-analytics-dns/name-reg-req-blade.png)

**Steekproef DDI analysequery's**. Bevat een overzicht van het meest voorkomende zoekquery's hello, die rechtstreeks onbewerkte analytische gegevens ophalen.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Voorbeeldquery 's](./media/log-analytics-dns/queries.png)

U kunt deze query's als uitgangspunt gebruiken voor het maken van uw eigen query's voor aangepaste rapportage. Hallo-query's koppelen toohello DNS-Analytics logboek zoekpagina waar de resultaten worden weergegeven:

- **Lijst met DNS-Servers**. Geeft een lijst weer van alle DNS-servers en hun bijbehorende FQDN-naam, domeinnaam, naam van het forest en server IP-adressen.
- **Lijst met DNS-Zones**. Geeft een lijst weer van alle DNS-zones met Hallo gekoppeld zonenaam, de status van de dynamische update, naamservers en DNSSEC-ondertekeningsstatus.
- **Ongebruikte bronrecords**. Bevat een overzicht van alle Hallo ongebruikte/verouderd bronrecords. Deze lijst bevat de naam van de bronrecord hello, bronrecordtype Hallo gekoppeld DNS-server, record genereren en zonenaam. U kunt deze lijst tooidentify Hallo DNS-bronrecords die niet langer in gebruik. Op basis van deze informatie, kunt u vervolgens deze vermeldingen verwijderen van Hallo DNS-servers.
- **DNS-Servers opvragen Load**. Geeft informatie weer, zodat u kunt een perspectief Hallo die DNS laden op uw DNS-servers ophalen. Deze informatie kunt u plannen van capaciteit Hallo voor Hallo-servers. U kunt gaan toohello **metrische gegevens** toochange Hallo weergave tooa grafische visualisatie tabblad. Deze weergave helpt u begrijpen hoe Hallo DNS laden is verdeeld over de DNS-servers. Deze DNS-query snelheid laat trends zien voor elke server.

    ![Zoekresultaten voor DNS-servers query-logboek](./media/log-analytics-dns/dns-servers-query-load.png)

- **DNS-Zones Query Load**. Bevat Hallo statistieken van de DNS-zone query per seconde van alle Hallo-zones op Hallo DNS-servers die worden beheerd door Hallo-oplossing. Klik op Hallo **metrische gegevens** tabblad toochange Hallo weergave van gedetailleerde records tooa grafische visualisatie van Hallo resultaten.
- **Configuratiegebeurtenissen**. Bevat alle Hallo DNS-configuratie wijzigen-gebeurtenissen en de bijbehorende berichten. Vervolgens kunt u deze gebeurtenissen op basis van tijd van Hallo-gebeurtenis met gebeurtenis-ID, DNS-server filteren of taakcategorie. Hallo-gegevens kunt u wijzigingen toospecific DNS-servers controleren op specifieke tijdstippen.
- **DNS-analytische logboek**. Geeft alle Hallo analytische gebeurtenissen op alle Hallo DNS-servers worden beheerd door Hallo-oplossing. Vervolgens kunt u deze gebeurtenissen op basis van tijd van het Hallo-gebeurtenis met gebeurtenis-ID, DNS-server, client-IP-die Hallo lookup-query en het opvragen van taakcategorie type filteren. DNS-server analysegebeurtenissen inschakelen activiteiten bijhouden op Hallo DNS-server. Een analytisch gebeurtenis wordt geregistreerd telkens Hallo-server worden verzonden of ontvangen van de DNS-informatie.

### <a name="search-by-using-dns-analytics-log-search"></a>Zoeken met behulp van DNS-Analytics logboek zoeken

Op het logboek zoekpagina hello, kunt u een query maken. U kunt uw zoekresultaten filteren met behulp van besturingselementen facet. U kunt ook tootransform geavanceerde query's, te filteren en rapport maken op de resultaten. Start met behulp van Hallo query's te volgen:

1. In Hallo **query zoekvak**, type `Type=DnsEvents` tooview alle DNS-gebeurtenissen die worden gegenereerd door Hallo DNS-servers worden beheerd door de oplossing Hallo Hallo. Hallo resultaten weergeven Hallo-logboekgegevens voor alle gebeurtenissen gerelateerde toolookup query's, dynamische registraties en configuratiewijzigingen.

    ![DnsEvents logboek zoeken](./media/log-analytics-dns/log-search-dnsevents.png)  

    a. tooview Hallo-logboekgegevens voor een lookup-query's selecteren **LookUpQuery** als Hallo **Subtype** filter uit Hallo facet besturingselement op Hallo links. Een tabel waarin alle Hallo lookup querygebeurtenissen voor Hallo geselecteerde tijdsperiode wordt weergegeven.

    b. Selecteer tooview Hallo-logboekgegevens voor dynamische registraties **DynamicRegistration** als Hallo **Subtype** filter uit Hallo facet besturingselement op Hallo links. Een tabel waarin alle Hallo dynamische registratie-gebeurtenissen voor Hallo geselecteerde tijdsperiode wordt weergegeven.

    c. tooview Hallo-logboekgegevens voor wijzigingen in de configuratie, selecteer **ConfigurationChange** als Hallo **Subtype** filter uit Hallo facet besturingselement op Hallo links. Een tabel waarin alle Hallo wijzigingsgebeurtenissen voor configuratie voor de geselecteerde periode hello wordt weergegeven.

2. In Hallo **query zoekvak**, type `Type=DnsInventory` tooview alle DNS-inventarisatie-gerelateerde gegevens voor Hallo DNS-servers worden beheerd door de oplossing Hallo Hallo. Hallo resultaten weergeven Hallo-logboekgegevens voor DNS-servers, DNS-zones en bronrecords.

    ![DnsInventory logboek zoeken](./media/log-analytics-dns/log-search-dnsinventory.png)

## <a name="feedback"></a>Feedback

Er zijn twee manieren waarop u feedback kunt geven:

- **UserVoice**. Post een bericht ideeën voor DNS-Analytics functies toowork op. Ga naar Hallo [Operations Management Suite UserVoice-pagina](https://aka.ms/dnsanalyticsuservoice).
- **Deelnemen aan onze cohort**. We altijd geïnteresseerd in nieuwe klanten ons cohorten tooget vroege toonew toegangsfuncties koppelen en te verbeteren DNS Analytics hebben. Als u geïnteresseerd bent in onze cohorten toevoegen, vult u [deze snelle enquête](https://aka.ms/dnsanalyticssurvey).

## <a name="next-steps"></a>Volgende stappen

[Zoeken in een logboek](log-analytics-log-searches.md) tooview gedetailleerde DNS-records in het logboek.

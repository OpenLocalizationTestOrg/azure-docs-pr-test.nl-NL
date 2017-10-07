---
title: aaaDashboard, Monitor, schaal, configureren en hybride verbindingen in BizTalk Services | Microsoft Docs
description: 'Meer informatie over Hallo beveiligingsmaatregelen en bewaking van prestaties op Hallo van de klassieke portal tabbladen voor BizTalk Services: Dashboard, bewaken, schaal, configureren en hybride verbindingen. MABS, WABS'
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a>Bekijk de tabbladen Dashboard, bewaken, schaal, configureren en hybride verbinding Hallo

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Nadat u uw BizTalk Service maken en implementeren van uw toepassing, kunt u bepaalde Hallo BizTalk Service-instellingen wijzigen en bewaken van toepassingsprestaties Hallo. 

Wanneer u Hallo klassieke Azure-portal opent, wordt u automatisch geplaatst op Hallo **alle ITEMS** tabblad tooview uw BizTalk Service, selecteer uw BizTalk Service in Hallo **alle ITEMS** tabblad of selecteer Hallo **BIZTALK SERVICES** tabblad; en selecteer vervolgens de naam van uw BizTalk Service.

Hiermee opent u een nieuw venster met de volgende tabbladen Hallo. Dit onderwerp beschrijft deze tabbladen.

## <a name="quickstart-quickstartquickstart"></a>Quick Start)![Snelstartgids][Quickstart])
Afhankelijk van BizTalk Services Edition hello, alle vermelde opties mogelijk niet beschikbaar. 

<table border="1">
    <tr>
        <td><strong>Hallo-hulpprogramma's ophalen</strong></td>
        <td>Hallo BizTalk Services SDK tooinstall Hallo Visual Studio-projectsjablonen op de lokale computer downloaden. Deze sjablonen maken Hallo <strong>BizTalk Services</strong> (brug) en Hallo <strong>BizTalk serviceartefacten</strong> (transformatie) Visual Studio-projecten die geïmplementeerd tooyour BizTalk Service zijn.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Hoe Hallo gaan gebruiken Azure BizTalk Services SDK </a> en <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">installeren hello Azure BizTalk Services SDK</a> lijsten Hallo stappen tooget gestart.
        </td>
    </tr>
    <tr>
        <td><strong>Partner overeenkomsten maken</strong></td>
        <td>Wordt geopend hello Azure BizTalk Services Portal gehost op Azure, waarbij het toevoegen van partners en X12, AS2, maken en EDIFACT EDI-overeenkomsten.
        <br/><br/>
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configureren van onderdelen voor EDI-berichten op BizTalk Services Portal</a> lijsten Hallo stappen tooget gestart.
        </td>
    </tr>

<tr>
        <td><strong>Meer informatie over BizTalk Services</strong></td>
        <td>Ga toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn meer informatie over Azure BizTalk Services.</td>
</tr>
</table>


In de taakbalk Hallo Hallo onderin kunt u:

<table border="1">

<tr>
<td><strong>Beheren</strong> implementatie van uw toepassing</td>
<td>Hiermee opent u hello Azure BizTalk Services-portal. Hallo BizTalk Services-Portal is Hallo ingang tooEDI configuratie, inclusief het toevoegen van partners en X12, AS2, maken en EDIFACT-overeenkomsten.
<br/><br/>
Dit is dezelfde als Hallo <strong>partner overeenkomsten maken</strong> op Hallo <strong>Quick Start</strong> tabblad.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configureren van onderdelen voor EDI-berichten op BizTalk Services Portal</a> bevat meer informatie over Hallo BizTalk Services-Portal.</td>
</tr>

<tr>
<td><strong>Verbindingsgegevens</strong> Hallo Access Control Namespace</td>
<td>Wanneer u de verbindingsgegevens selecteert, vervolgens Hallo Access Control Namespace, standaard verlener en sleutel standaard worden weergegeven. U kunt deze waarden kopiëren.
<br/><br/>
U kunt ook openen Hallo Access Control-beheerportal. <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Maken van een toegangsbeheer Namespace</a> bevat meer informatie over Hallo Access Control-beheerportal.</td>
</tr>

<tr>
<td><strong>Sleutels synchroniseren</strong> in Hallo Storage-Account</td>
<td>Wanneer u een opslagaccount maakt, worden automatisch een primaire en secundaire sleutel gemaakt. Deze versleutelingssleutels beheren toegang tooyour Storage-Account. Uw BizTalk Service gebruikt automatisch Hallo primaire sleutel. <strong>Sleutels synchroniseren</strong> gebruikers tooswitch tussen Hallo primaire sleutel en secundaire sleutel Hallo inschakelen zonder het Hallo BizTalk Service verstoren.
<br/><br/>
U wilt bijvoorbeeld Hallo toouse BizTalk Service een nieuwe primaire sleutel voor Hallo Storage-Account. toodo dit:
<br/><br/>
<ol>
<li>Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>. Selecteer Hallo secundaire sleutel. Als u dit doet, Hallo BizTalk Service wordt gestart met behulp van Hallo secundaire sleutel.</li>
<li>In de klassieke Azure-portal hello, selecteer uw Storage-account en Hallo primaire sleutel opnieuw genereren. Vergeet niet uw BizTalk Service Hallo secundaire sleutel wordt gebruikt.</li>
<li>Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>. Selecteer nu Hallo primaire sleutel. Dit is Hallo nieuwe primaire sleutel die u opnieuw gegenereerd.</li>
<li>In de klassieke Azure-portal hello, selecteer uw Storage-account en Hallo secundaire sleutel genereren.</li>
</ol>
<br/>
Dit proces wordt 'rollover voor sleutels' genoemd. Hallo-doel is tooenable gebruikers tooswitch tussen Hallo primaire sleutel en secundaire sleutel Hallo zonder te verstoren Hallo BizTalk Service.</td>
</tr>

<tr>
<td><strong>Verwijder</strong> uw toepassing</td>
<td>Wanneer u selecteert verwijderen, uw BizTalk Service en alle items die zijn geïmplementeerd tooit worden verwijderd.</td>
</tr>
</table>


## <a name="dashboard"></a>Dashboard
Afhankelijk van BizTalk Services Edition hello, alle vermelde opties mogelijk niet beschikbaar. 

Wanneer u de naam van uw BizTalk Service selecteert, wordt tabblad Hallo-Dashboard weergegeven. In het Dashboard kunt u:

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a>Overzicht van gebruik: Toont het aantal gebruikte hybride verbindingen Hallo
Gebruik Hallo-gegevens worden ook weergegeven in GB. 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a>Metrische grafiek: Toont een vaste lijst maatstaven voor prestaties
Deze metrische gegevens opgeven realtime waarden met betrekking tot Hallo health Hallo BizTalk Service. U kunt ook Hallo **relatieve** of **Absolute** waarden en Hallo tijdsbereik **Interval** van Hallo metrische gegevens die worden weergegeven in het Hallo-grafiek. 

Voor een beschrijving van deze maatstaven voor prestaties, gaat u te[beschikbare metrische gegevens](#Metrics) in dit onderwerp.

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a>Snelle weergave: Geeft een lijst van uw BizTalk Service-eigenschappen
<table border="1">

<tr>
<td><strong>Database bijhouden referenties bijwerken</strong></td>
<td>Wijzigingen Hallo gebruikersnaam en wachtwoord toolog in Hallo bijhouden Database gebruikt.</td>
</tr>
<tr>
<td><strong>SSL-certificaat bijwerken</strong></td>
<td>Hallo BizTalk Service toouse een ander SSL-certificaat kan worden bijgewerkt. Een zelfondertekend SSL-certificaat wordt automatisch gemaakt wanneer u <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Hallo BizTalk Service maken</a>.</td>
</tr>
<tr>
<td><strong>Certificaat downloaden</strong></td>
<td>Hallo SSL-certificaat dat door uw BizTalk Service tooa lokale machine gebruikt, kunt u downloaden.</td>
</tr>
<tr>
<td><strong>Status</strong></td>
<td>Geeft de huidige status Hallo van uw BizTalk Service. Zie <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Statusgrafiek Service</a>. </td>
</tr>
<tr>
<td><strong>Service-URL</strong></td>
<td>Hallo-URL voor uw BizTalk Service. Dit is dezelfde als Hallo Hallo <strong>domein-URL</strong> ingevoerd bij het maken van uw BizTalk Service.</td>
</tr>
<tr>
<td><strong>Adres van de openbare virtuele IP (VIP)</strong></td>
<td>Hallo IP-adres toegewezen tooyour BizTalk Service. Het wordt gebruikt voor alle invoereindpunten en Hallo bronadres voor uitgaand verkeer. Dit IP-adres behoort tooyour BizTalk Service wanneer deze is gemaakt. Als u Hallo BizTalk Service hebt verwijderd, toegewezen Hallo IP-adres tooanother BizTalk Service.</td>
</tr>
<tr>
<td><strong>ACS-Namespace</strong></td>
<td>Verifieert met Hallo BizTalk Service.</td>
</tr>
<tr>
<td><strong>Editie</strong></td>
<td>Geeft een lijst Hallo die Edition ingevoerd wanneer Hallo BizTalk Service wordt gemaakt.</td>
</tr>
<tr>
<td><strong>Locatie</strong></td>
<td>Geeft Hallo geografische regio die als host fungeert voor uw BizTalk Service.</td>
</tr>
<tr>
<td><strong>Gemaakt</strong></td>
<td>Geeft Hallo datum en tijd Hallo BizTalk Service is gemaakt.</td>
</tr>
<tr>
<td><strong>Traceringsdatabase</strong></td>
<td>Hello Azure SQL Database-naam die tabellen die worden gebruikt door uw BizTalk Service bijhouden Hallo opslaat. 
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Vereisten wat</a> biedt details over Hallo Database bijhouden.</td>
</tr>
<tr>
<td><strong>Opslag voor bewaken/archiveren</strong></td>
<td>Hello Azure Storage accountnaam op die Hallo bewaking van de uitvoer van uw BizTalk Service worden opgeslagen.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Vereisten wat</a> biedt details over Hallo Storage-account.</td>
</tr>
<tr>
<td><strong>De naam van abonnement</strong></td>
<td>Hallo-abonnement dat als host fungeert voor uw BizTalk Service bevat. Hallo abonnement bepaalt toegang toohello klassieke Azure-portal.</td>
</tr>
<tr>
<td><strong>Abonnements-ID</strong></td>
<td>Wanneer een abonnement is gemaakt, wordt er automatisch een abonnements-ID gegenereerd. Wanneer u de REST-API's, moet u mogelijk tooenter Hallo abonnement-ID.</td>
</tr>
</table>

[BizTalk Services: Inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lijsten Hallo stappen toocreate een BizTalk Service.

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a>Beheren van de verbindingsinformatie, de sleutels synchroniseren, en verwijder in de taakbalk Hallo:
<table border="1">

<tr>
<td><strong>Beheren</strong> implementatie van uw toepassing</td>
<td>Hiermee opent u hello Azure BizTalk Services-Portal. Hallo BizTalk Services-Portal is Hallo ingang tooEDI configuratie, inclusief het toevoegen van partners en X12, AS2, maken en EDIFACT-overeenkomsten.
<br/><br/>
Dit is dezelfde als Hallo <strong>partner overeenkomsten maken</strong> op Hallo <strong>Quick Start</strong> tabblad.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configureren van onderdelen voor EDI-berichten op BizTalk Services Portal</a> bevat meer informatie over Hallo BizTalk Services-Portal.</td>
</tr>
<tr>
<td><strong>Verbindingsgegevens</strong> Hallo Access Control Namespace</td>
<td>Geeft Hallo Access Control Namespace, standaard verlener en sleutel standaard waarden; die kunnen worden gekopieerd.
<br/><br/>
U kunt ook openen Hallo Access Control-beheerportal. Deze Access Control-beheerportal is hetzelfde als het gebruik van de optie Active Directory Hallo in het linkernavigatievenster Hallo Hallo.
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Het beheren van uw ACS-Namespace</a> bevat meer informatie over Hallo Access Control-beheerportal.</td>
</tr>
<tr>
<td><strong>Sleutels synchroniseren</strong> in Hallo Storage-Account</td>
<td>Wanneer u een opslagaccount maakt, worden automatisch een primaire en secundaire sleutel gemaakt. Deze versleutelingssleutels beheren toegang tooyour Storage-Account. Uw BizTalk Service gebruikt automatisch Hallo primaire sleutel. <strong>Sleutels synchroniseren</strong> gebruikers tooswitch tussen Hallo primaire sleutel en secundaire sleutel Hallo inschakelen zonder het Hallo BizTalk Service verstoren.
<br/><br/>
U wilt bijvoorbeeld Hallo toouse BizTalk Service een nieuwe primaire sleutel voor Hallo Storage-Account. toodo dit:
<br/><br/>
<ol>
<li>Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>. Selecteer Hallo secundaire sleutel. Als u dit doet, Hallo BizTalk Service wordt gestart met behulp van Hallo secundaire sleutel.</li>
<li>In de klassieke Azure-portal hello, selecteer uw Storage-account en Hallo primaire sleutel opnieuw genereren. Vergeet niet uw BizTalk Service Hallo secundaire sleutel wordt gebruikt.</li>
<li>Selecteer uw BizTalk Service en selecteer <strong>sleutels synchroniseren</strong>. Selecteer nu Hallo primaire sleutel. Dit is Hallo nieuwe primaire sleutel die u opnieuw gegenereerd.</li>
<li>In de klassieke Azure-portal hello, selecteer uw Storage-account en Hallo secundaire sleutel genereren.</li>
</ol>
<br/>
Dit proces wordt 'rollover voor sleutels' genoemd. Hallo-doel is tooenable gebruikers tooswitch tussen Hallo primaire sleutel en secundaire sleutel Hallo zonder te verstoren Hallo BizTalk Service.</td>
</tr>

<tr>
<td><strong>Verwijder</strong> uw toepassing</td>
<td>Uw BizTalk Service en alle items die zijn geïmplementeerd tooit worden verwijderd.</td>
</tr>
</table>


## <a name="monitor"></a>Bewaken
Is niet van toepassing op toohello editie Free.

Wanneer u de naam van uw BizTalk Service selecteert, tabblad Hallo-Monitor is beschikbaar en wordt de volgende Hallo:

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a>Metrische grafiek: Geeft Hallo geselecteerd maatstaven voor prestaties
Deze metrische gegevens opgeven realtime waarden met betrekking tot Hallo health Hallo BizTalk Service. U kiezen welke maatstaven voor prestaties worden weergegeven. Maximaal zes maatstaven voor prestaties kan tegelijkertijd worden weergegeven. 

U kunt ook Hallo **relatieve** of **Absolute** waarden en Hallo tijdsbereik **Interval** van Hallo metrische gegevens die worden weergegeven. 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a>tooremove of weergave metrische gegevens in de grafiek Hallo:
1. Selecteer Hallo **Monitor** tabblad.
2. Selecteer **toevoegen metrische gegevens** in de taakbalk Hallo:  
   ![Selecteer de metrische gegevens toevoegen][AddMetrics]
3. Controleer de maatstaven voor prestaties Hallo gewenste toodisplay.
4. Selecteer Hallo vinkje tooreturn toohello **Monitor** tabblad.
5. Selecteer Hallo cirkel volgende toohello metrische toodisplay die metrische waarde in grafiek Hallo.  
   
    Bijvoorbeeld, Hallo **CPU-gebruik** metriek is niet beschikbaar; de uitvoer wordt niet weergegeven in het Hallo-grafiek:  
   ![CPU-gebruik metriek is niet beschikbaar][GrayedMetric]  
   
    Selecteer Hallo grijs cirkel tooenable hello **CPU-gebruik** metrische toodisplay uitvoer ervan weergegeven in de grafiek Hallo:  
   ![CPU-gebruik metrische gegevens is ingeschakeld][EnabledMetric]
6. tooremove metric van Hallo weergave grafiek en Hallo-lijst, selecteer **metriek verwijderen** in de taakbalk Hallo. tooadd hello metrische back toohello lijst, selecteert **toevoegen metrische gegevens** controleren in de taakbalk Hallo Hallo metriek, en selecteer Hallo vinkje tooreturn toohello **Monitor** tabblad. Selecteer Hallo grijs weergegeven cirkel tooenable Hallo metriek.

## <a name="Metrics"></a>Beschikbare metrische gegevens
Hallo prestatiewaarden prestatiemeteritems te volgen zijn beschikbaar:

<table border="1">

<tr>
<td><strong>RountdTrip latentie</strong></td>
<td>Hallo gemiddelde tijd in milliseconden (ms) tooprocess die een bericht van Hallo tijd Hallo-bericht wordt ontvangen totdat het Hallo-bericht volledig is verwerkt door Hallo BizTalk Service via alle bruggen weergeven Alleen de verwerkte berichten worden meegeteld.<br/><br/>
Wanneer Hallo volgende gebeurtenissen plaatsvinden, wordt een tijdstempel gemaakt:
<ul>
<li>Bericht krijgt Hallo-gateway</li>
<li>Bericht is gerouteerde toohello bestemming</li>
<li>Bestemming reactie wordt ontvangen</li>
<li>Bestemming bevestiging antwoord verzonden toohello gateway</li>
</ul>
<br/>
Met deze metriek weergegeven Hallo resultaten van Hallo berekening volgende:
<br/><br/>
[Bestemming bevestiging antwoord verzonden toohello gateway] - [bericht krijgt Hallo gateway]</td>
</tr>
<tr>
<td><strong>Fouten bij de bron</strong></td>
<td>Geeft Hallo totaal aantal berichten dat is mislukt door Hallo BizTalk Service wanneer binnenhalen van berichten van Hallo bron eindpunten.</td>
</tr>
<tr>
<td><strong>CPU-gebruik</strong></td>
<td>Geeft een lijst Hallo gemiddeld percentage processortijd van alle rolinstanties.</td>
</tr>
<tr>
<td><strong>Latentie verwerken</strong></td>
<td>Hallo gemiddelde tijd In milliseconden (ms) tooprocess een bericht door Hallo BizTalk Service via alle bruggen, met uitzondering van Hallo tijd besteed aan bestemmingen weergeven Alleen de verwerkte berichten worden meegeteld.<br/><br/>
Wanneer elk van de volgende gebeurtenissen Hallo optreden, wordt er een tijdstempel gemaakt:

<ul>
<li>Bericht krijgt Hallo-gateway</li>
<li>Bericht is gerouteerde toohello bestemming</li>
<li>Bestemming reactie wordt ontvangen</li>
<li>Bestemming bevestiging antwoord verzonden toohello gateway</li>
</ul>
<br/>Met deze metriek weergegeven Hallo resultaten van Hallo berekening volgende:<br/><br/>
[Bestemming bevestiging antwoord verzonden toohello gateway] - [bericht krijgt Hallo gateway] - [bestemming reactie wordt ontvangen] + [bericht is gerouteerde toohello bestemming]</td>
</tr>
<tr>
<td><strong>Fouten In het proces</strong></td>
<td>Totaal aantal berichten dat is mislukt tijdens de verwerking door Hallo BizTalk Service via alle Hallo bruggen binnen een periode Hallo weergeven</td>
</tr>
<tr>
<td><strong>Berichten die worden verzonden</strong></td>
<td>Geeft Hallo totaal aantal berichten is verzonden door Hallo BizTalk Service via alle bruggen binnen een periode. Met deze metriek wordt verhoogd wanneer er een bericht verzonden vanuit een pijplijn Hallo route bestemming bereikt. Met deze metriek geeft niet aan een bericht is verwerkt.<br/><br/>
In een scenario Request-Reply wordt Hallo metriek wanneer Hallo route bestemming een pijplijn ontvangstbevestiging back toohello verzendt verhoogd.</td>
</tr>
<tr>
<td><strong>Berichten ontvangen</strong></td>
<td>Geeft Hallo totaal aantal berichten dat is ontvangen door Hallo BizTalk Service via alle bruggen binnen een periode. Met deze metriek wordt verhoogd wanneer een nieuw bericht wordt ontvangen door Hallo pijplijn.</td>
</tr>
<tr>
<td><strong>Berichten In proces</strong></td>
<td>Geeft Hallo totaal aantal berichten momenteel door Hallo BizTalk Service verwerkt binnen een periode.</td>
</tr>
<tr>
<td><strong>Berichten die zijn verwerkt</strong></td>
<td>Geeft Hallo totaal aantal berichten dat is verwerkt door Hallo BizTalk Service via alle bruggen binnen een periode. Met deze metriek wordt verhoogd wanneer er een bericht met succes is ontvangen door Hallo pijplijn en met succes gerouteerde toohello bestemming.</td>
</tr>
</table>


## <a name="scale"></a>Schalen
U kunt in het tabblad schaal hello, toevoegen of afgetrokken Hallo aantal eenheden die worden gebruikt door uw BizTalk Service. Er is standaard één eenheid worden geconfigureerd. Extra eenheden kunnen worden toegevoegd tooscale uw BizTalk Service. Als u de schaal Hallo verhoogt, bent u doorvoer te verbeteren. Hallo hoeveelheid resources verhoogt ook, inclusief geïmplementeerde bruggen, overeenkomsten, LOB-verbindingen en verwerkingskracht. Bijvoorbeeld, verhogen u Hallo schaal van 1 eenheid too2 eenheden. In dit geval kunt u dubbele Hallo aantal bruggen, double Hallo overeenkomsten dubbele Hallo LOB-verbindingen en dubbele Hallo verwerkingskracht implementeren.

Sommige edities van BizTalk bieden geen een optie voor schaal. In dit geval is één eenheid toegestaan. toodetermine hoeveel eenheden uw editie kan worden geschaald, Raadpleeg te[BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md).

Hallo aantal eenheden verhogen mogelijk van invloed prijzen. Als u de eenheden Hallo verhoogt, selecteer **opslaan** wordt een bericht weergegeven dat aangeeft of facturering wordt beïnvloed. U wordt vervolgens toocontinue. Als u het aantal eenheden Hallo verhoogt, verandert Hallo BizTalk Service-status van actieve tooUpdating. In Hallo Updating status blijft uw BizTalk Service toorun.

[BizTalk Services: Grafiek van edities](biztalk-editions-feature-chart.md) definieert een 'eenheid'.

## <a name="configure"></a>Configureren
TooHybrid verbindingen is niet van toepassing.

Hiermee stelt u Hallo Status van de back-up tooNone of automatisch. Bij het instellen van tooNone, geen back-ups worden automatisch gemaakt. Bij het instellen van tooAutomatic, configureren van de back-uplocatie hello, Hallo frequentie van back-up Hallo en hoe lang tookeep Hallo back-upbestanden. 

[BizTalk Services: Back-up en herstel](biztalk-backup-restore.md) biedt Hallo details. 

## <a name="HybridConnections"></a>Hybride verbindingen
Hybride verbindingen verbinding maken met een Azure-toepassing, zoals Web-Apps of mobiele Apps in Azure App Service, tooan on-premises resource die gebruikmaakt van een statische TCP-poort, zoals SQL Server, MySQL, HTTP-Web-API's en de meeste aangepaste webservices. Hybride verbindingen worden beheerd in BizTalk Services in Hallo klassieke Azure-portal.

Zie toocreate hybride verbindingen in Azure App Service [toegang tot on-premises resources met behulp van hybride verbindingen in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

toocreate of hybride verbindingen in de Azure BizTalk Services wilt beheren, Zie [hybride verbindingen](integration-hybrid-connection-overview.md).

## <a name="next"></a>Volgende
Nu dat u bekend met de verschillende tabbladen hello bent, kunt u meer informatie over functies voor hello Azure BizTalk Services:

* [BizTalk Services: beperking](biztalk-throttling-thresholds.md)  
* [BizTalk Services: naam en sleutel van verlener](biztalk-issuer-name-issuer-key.md)  
* [BizTalk Services: back-ups maken en herstellen](biztalk-backup-restore.md)

## <a name="see-also"></a>Zie ook
* [Hybride verbindingen](integration-hybrid-connection-overview.md)  
* [BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek](biztalk-editions-feature-chart.md)  
* [BizTalk Services: Inrichten met behulp van Azure classic portal](biztalk-provision-services.md)  
* [BizTalk Services: Grafiek van de status van de BizTalk-Service](biztalk-service-state-chart.md)  
* [Hoe gaan gebruiken Azure BizTalk Services SDK Hallo](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png


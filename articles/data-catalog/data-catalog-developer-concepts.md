---
title: concepten voor ontwikkelaars van aaaData catalogus | Microsoft Docs
description: Inleiding toohello belangrijkste concepten in Azure Data Catalog conceptuele model, Hallo zoals beschikbaar via het-catalogus REST-API.
services: data-catalog
documentationcenter: 
author: spelluru
manager: jhubbard
editor: 
tags: 
ms.assetid: 89de9137-a0a4-40d1-9f8d-625acad31619
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/03/2017
ms.author: spelluru
ms.openlocfilehash: d0b1628ff6c31458cb650efef852244f0c139b1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-developer-concepts"></a>Azure Data Catalog-concepten voor ontwikkelaars
Microsoft **Azure Data Catalog** is een volledig beheerde cloudservice waarmee mogelijkheden voor detectie van gegevensbronnen en crowdsourcing metagegevens van de gegevensbron biedt. Ontwikkelaars kunnen Hallo-service via de REST-API's gebruiken. Informatie over concepten van Hallo geïmplementeerd in Hallo-service is belangrijk voor ontwikkelaars toosuccessfully integreren met **Azure Data Catalog**.

## <a name="key-concepts"></a>Belangrijkste concepten
Hallo **Azure Data Catalog** conceptuele model is gebaseerd op vier belangrijke concepten: Hallo **catalogus**, **gebruikers**, **activa**, en **Aantekeningen**.

![Concept][1]

*Afbeelding 1: Azure Data Catalog vereenvoudigd conceptuele model*

### <a name="catalog"></a>Catalogus
Een **catalogus** is op het hoogste niveau Hallo-container voor alle metagegevens van een organisatie slaat Hallo. Er is een **catalogus** toegestaan per Azure-Account. Catalogussen zijn gebonden tooan Azure-abonnement, maar slechts één **catalogus** kunnen worden gemaakt voor een bepaald Azure-account, zelfs als een account kan meerdere abonnementen hebt.

Een catalogus bevat **gebruikers** en **activa**.

### <a name="users"></a>Gebruikers
Gebruikers kunnen beveiligings-principals die machtigingen tooperform acties zijn (zoeken in de catalogus hello, toevoegen, bewerken of verwijderen van items, enzovoort) in Hallo catalogus.

Er zijn diverse verschillende rollen die een gebruiker kan hebben. Zie voor informatie over functies, Hallo sectie rollen en autorisatie.

Afzonderlijke gebruikers en beveiligingsgroepen worden toegevoegd.

Azure Data Catalog gebruikt Azure Active Directory voor identiteits-en toegang. Elke gebruiker catalogus moet lid zijn van Hallo Active Directory voor Hallo-account.

### <a name="assets"></a>Assets
Een **catalogus** gegevensassets bevat. **Activa** Hallo-eenheid van granulatie beheerd door de Hallo-catalogus.

Hallo granulatie van een asset hangt af van de gegevensbron. Voor SQL Server- of Oracle-Database mag een asset een tabel of weergave. Een asset kan voor SQL Server Analysis Services zijn een meting een dimensie of een Key Performance Indicator (KPI). Een actief is voor SQL Server Reporting Services, een rapport.

Een **Asset** Hallo wat u toevoegen of verwijderen uit een catalogus is. Het resultaat u van terughalen Hallo-eenheid is **Search**.

Een **Asset** wordt samengesteld uit de naam, locatie, en type en aantekeningen verdere beschrijving van het.

### <a name="annotations"></a>Aantekeningen
Aantekeningen zijn items die metagegevens over activa vertegenwoordigen.

Voorbeelden van aantekeningen zijn beschrijving, tags, schema, documentatie, enzovoort. Er zijn een volledige lijst met Hallo asset waardetypen en aantekeningentypen in Hallo Asset Object model-sectie.

## <a name="crowdsourcing-annotations-and-user-perspective-multiplicity-of-opinion"></a>Crowdsourcing aantekeningen en het gebruikersperspectief (multipliciteit van advies)
Een belangrijk aspect van Azure Data Catalog is hoe deze Hallo crowdsourcing van metagegevens in Hallo-systeem ondersteunt. Als tegengestelde tooa wiki benadering – waar er is slechts één advies en Hallo laatste schrijver wins – hello Azure Data Catalog model kunnen meerdere adviezen toolive naast elkaar in Hallo-systeem.

Deze aanpak geeft Hallo werkelijkheid van ondernemingsgegevens waarin verschillende gebruikers verschillende perspectieven op een opgegeven activum hebben:

* Een databasebeheerder kan voorzien in informatie over serviceovereenkomsten of Hallo beschikbaar verwerking venster bulkbewerkingen voor ETL
* Een wereldburgers gegevens kan bieden informatie over Hallo zakelijke processen toowhich Hallo asset is van toepassing, of Hallo classificaties die zakelijke Hallo tooit is toegepast
* Een analist Financiën mogen bevatten informatie over hoe Hallo gegevens worden gebruikt tijdens het einde van de periode rapportagetaken

toosupport dit voorbeeld wordt elke gebruiker – Hallo DBA, Hallo gegevens wereldburgers en Hallo analist – kunt beschrijving tooa één tabel die is geregistreerd in de catalogus Hallo toevoegen. Alle beschrijvingen worden bijgehouden in het systeem hello en in Azure Data Catalog-portal Hallo alle beschrijvingen worden weergegeven.

Dit patroon is toegepaste toomost Hallo items in Hallo-objectmodel, zodat de objecttypen die in de JSON-nettolading Hallo zijn vaak matrices voor eigenschappen waarbij u een singleton verwacht.

Onder Hallo asset bijvoorbeeld is hoofdmap een matrix met objecten beschrijving. Hallo matrixeigenschap heet 'beschrijvingen'. Een object beschrijving heeft één eigenschap - beschrijving. Hallo patroon is dat elke gebruiker die de typen beschrijving haalt een beschrijving-object voor opgegeven door de gebruiker Hallo Hallo-waarde gemaakt.

Hallo UX kunt vervolgens kiezen hoe toodisplay Hallo combinatie. Er zijn drie verschillende patronen voor weergave.

* de eenvoudigste patroon Hallo is 'Alles weergeven'. In dit patroon worden alle Hallo-objecten in een lijst weergegeven. Hello Azure Data Catalog-portal UX wordt dit patroon gebruikt voor beschrijving.
* Een andere notatie is 'Samenvoegen'. In dit patroon worden alle Hallo waarden van verschillende gebruikers Hallo samengevoegd, met een dubbel verwijderd. Voorbeelden van dit patroon in hello Azure Data Catalog-portal UX zijn Hallo tags en experts eigenschappen.
* Een derde patroon is 'laatste schrijver wins'. In dit patroon alleen Hallo meest recente waarde hebt getypt in weergegeven. friendlyName is een voorbeeld van dit patroon.

## <a name="asset-object-model"></a>Asset-objectmodel
Geïntroduceerde Hallo hoofdconcepten sectie, Hallo **Azure Data Catalog** objectmodel bevat items, die activa of aantekeningen worden kunnen. Objecten hebben eigenschappen die optioneel of vereist worden kunnen. Sommige eigenschappen van toepassing tooall items. Sommige eigenschappen van toepassing tooall activa. Sommige eigenschappen van toepassing alleen toospecific asset typen.

### <a name="system-properties"></a>Systeemeigenschappen
<table><tr><td><b>De naam van eigenschap</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr><tr><td>tijdstempel</td><td>Datum/tijd</td><td>Hallo laatste tijd Hallo item is gewijzigd. Dit veld wordt gegenereerd door Hallo-server als een item wordt toegevoegd en telkens wanneer een item wordt bijgewerkt. Hallo waarde van deze eigenschap wordt genegeerd op invoer van bewerkingen publiceren.</td></tr><tr><td>id</td><td>URI</td><td>Absolute url van Hallo item (alleen-lezen). Het is Hallo uniek adresseerbaar URI voor Hallo-item.  Hallo waarde van deze eigenschap wordt genegeerd op invoer van bewerkingen publiceren.</td></tr><tr><td>type</td><td>Tekenreeks</td><td>Hallo type Hallo asset (alleen-lezen).</td></tr><tr><td>ETag</td><td>Tekenreeks</td><td>Een tekenreeks bijbehorende versie toohello Hallo item op dat kan worden gebruikt voor Optimistisch gelijktijdigheidbeheer bij het uitvoeren van bewerkingen die items in de catalogus Hallo bijwerken. ' * ' is een waarde gebruikte toomatch.</td></tr></table>

### <a name="common-properties"></a>Algemene eigenschappen
Deze eigenschappen toepassen tooall hoofdmap asset typen en alle aantekeningentypen.

<table>
<tr><td><b>De naam van eigenschap</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr>
<tr><td>fromSourceSystem</td><td>Booleaanse waarde</td><td>Hiermee wordt aangegeven of de gegevens van artikel is afgeleid van een bronsysteem (zoals Sql Server-Database, Oracle-Database) of door een gebruiker geschreven.</td></tr>
</table>

### <a name="common-root-properties"></a>Algemene eigenschappen voor de hoofdmap
<p>
Deze eigenschappen toepassen tooall hoofdmap asset typen.

<table><tr><td><b>De naam van eigenschap</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr><tr><td>naam</td><td>Tekenreeks</td><td>Een naam die is afgeleid van Hallo locatie gegevensbroninformatie</td></tr><tr><td>DSL</td><td>DataSourceLocation</td><td>Een unieke gegevensbron Hallo beschrijft en is een van de Hallo-id's voor Hallo asset. (Zie de sectie met dubbele identiteit).  Hallo-structuur van Hallo dsl hangt af van de Hallo-protocol en gegevensbrontype.</td></tr><tr><td>Gegevensbron</td><td>DataSourceInfo</td><td>Meer informatie over het Hallo-type van activa.</td></tr><tr><td>lastRegisteredBy</td><td>SecurityPrincipal</td><td>Hallo-gebruiker die het meest recent geregistreerd dit activum beschrijft.  Bevat de unieke id Hallo voor Hallo gebruiker (upn Hallo) en een weergavenaam (lastName en firstName).</td></tr><tr><td>containerId</td><td>Tekenreeks</td><td>Id van Hallo container asset voor Hallo-gegevensbron. Deze eigenschap wordt niet ondersteund voor Hallo Containertype.</td></tr></table>

### <a name="common-non-singleton-annotation-properties"></a>Algemene eigenschappen voor niet-singleton aantekening
Deze eigenschappen tooall niet-singleton aantekeningentypen toepassen (aantekeningen die toobe toegestaan meerdere per asset).

<table>
<tr><td><b>De naam van eigenschap</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr>
<tr><td>sleutel</td><td>Tekenreeks</td><td>Een gebruiker opgegeven sleutel, die een unieke identificatie van de aantekening in de huidige verzameling Hallo Hallo. Hallo sleutellengte mag maximaal 256 tekens.</td></tr>
</table>

### <a name="root-asset-types"></a>Hoofdmap asset typen
Hoofdmap asset typen zijn deze typen waarbij verschillende soorten gegevensassets die kunnen worden geregistreerd in de catalogus Hallo Hallo. Er is een weergave die asset en aantekeningen opgenomen in de weergave Hallo beschrijft voor elk type hoofdmap. De naam moet worden gebruikt in bijbehorende {view_name} url-segment Hallo bij het publiceren van een activum met REST-API.

<table><tr><td><b>Activatype (weergavenaam)</b></td><td><b>Aanvullende eigenschappen</b></td><td><b>Gegevenstype</b></td><td><b>Toegestane aantekeningen</b></td><td><b>Opmerkingen</b></td></tr><tr><td>Tabel ('tabellen")</td><td></td><td></td><td>Beschrijving<p>friendlyName<p>Label<p>Schema<p>ColumnDescription<p>ColumnTag<p> deskundige<p>Preview<p>AccessInstruction<p>TableDataProfile<p>ColumnDataProfile<p>ColumnDataClassification<p>Documentatie<p></td><td>Een tabel vertegenwoordigt tabellaire gegevens.  Bijvoorbeeld: SQL-tabel, SQL-weergave, in tabelvorm tabel van Analysis Services, Analysis Services multidimensionale dimensie, Oracle-tabel, enzovoort.   </td></tr><tr><td>Meting ('metingen')</td><td></td><td></td><td>Beschrijving<p>friendlyName<p>Label<p>deskundige<p>AccessInstruction<p>Documentatie<p></td><td>Dit type vertegenwoordigt een Analysis Services-meting.</td></tr><tr><td></td><td>meting</td><td>Kolom</td><td></td><td>Metagegevens met een beschrijving Hallo meting</td></tr><tr><td></td><td>isCalculated </td><td>Booleaanse waarde</td><td></td><td>Hiermee geeft u aan als Hallo meting of niet is berekend.</td></tr><tr><td></td><td>MeasureGroup</td><td>Tekenreeks</td><td></td><td>Fysieke container voor de meting</td></tr><td>KPI 'KPI's (')</td><td></td><td></td><td>Beschrijving<p>friendlyName<p>Label<p>deskundige<p>AccessInstruction<p>Documentatie</td><td></td></tr><tr><td></td><td>MeasureGroup</td><td>Tekenreeks</td><td></td><td>Fysieke container voor de meting</td></tr><tr><td></td><td>goalExpression</td><td>Tekenreeks</td><td></td><td>Een numerieke MDX-expressie of een berekening die doelwaarde Hallo Hallo KPI retourneert.</td></tr><tr><td></td><td>valueExpression</td><td>Tekenreeks</td><td></td><td>Een numerieke MDX-expressie waarmee de werkelijke waarde Hallo Hallo KPI geretourneerd.</td></tr><tr><td></td><td>statusExpression</td><td>Tekenreeks</td><td></td><td>Een MDX-expressie die de status van de Hallo Hallo KPI op een opgegeven punt in tijd vertegenwoordigt.</td></tr><tr><td></td><td>trendExpression</td><td>Tekenreeks</td><td></td><td>Een MDX-expressie die wordt geëvalueerd als waarde Hallo Hallo KPI gedurende een bepaalde periode. Hallo trend mag elk criterium op basis van tijd, dat is handig in een specifieke zakelijke context.</td>
<tr><td>Rapport ('rapporten')</td><td></td><td></td><td>Beschrijving<p>friendlyName<p>Label<p>deskundige<p>AccessInstruction<p>Documentatie<p></td><td>Dit type vertegenwoordigt een SQL Server Reporting Services-rapport </td></tr><tr><td></td><td>assetCreatedDate</td><td>Tekenreeks</td><td></td><td></td></tr><tr><td></td><td>assetCreatedBy</td><td>Tekenreeks</td><td></td><td></td></tr><tr><td></td><td>assetModifiedDate</td><td>Tekenreeks</td><td></td><td></td></tr><tr><td></td><td>assetModifiedBy</td><td>Tekenreeks</td><td></td><td></td></tr><tr><td>Container ('containers')</td><td></td><td></td><td>Beschrijving<p>friendlyName<p>Label<p>deskundige<p>AccessInstruction<p>Documentatie<p></td><td>Dit type vertegenwoordigt een container van andere activa zoals een SQL-database, een container Azure Blobs of een Analysis Services-model.</td></tr></table>

### <a name="annotation-types"></a>Annotatie-typen
Aantekeningentypen vertegenwoordigen typen metagegevens die kunnen worden toegewezen tooother typen binnen Hallo-catalogus.

<table>
<tr><td><b>Type aantekening (Nested weergavenaam)</b></td><td><b>Aanvullende eigenschappen</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr>

<tr><td>Beschrijving ('beschrijvingen')</td><td></td><td></td><td>Deze eigenschap bevat een beschrijving op voor een asset. Elke gebruiker van Hallo-systeem kunt hun eigen beschrijving toevoegen.  Alleen die gebruiker kunt Hallo beschrijving object bewerken.  (Beheerders en Asset eigenaars kunnen Hallo beschrijving object verwijderen, maar deze niet bewerken). Hallo system onderhoudt beschrijvingen van de gebruikers afzonderlijk.  Het is dus een matrix met beschrijvingen van elke asset (één voor elke gebruiker die is bijgedragen hun kennis over Hallo activa in toevoeging toopossibly met informatie afgeleid van de gegevensbron Hallo).</td></tr>
<tr><td></td><td>description</td><td>Tekenreeks</td><td>Een korte beschrijving (2-3 regels) van Hallo asset</td></tr>

<tr><td>Tag ('tags')</td><td></td><td></td><td>Deze eigenschap definieert een label voor een asset. Elke gebruiker van Hallo-systeem kunt meerdere labels voor een asset toevoegen.  Alleen Hallo-gebruiker die Tag-objecten gemaakt kunt ze bewerken.  (Beheerders en Asset eigenaars kunnen Hallo label object verwijderen, maar deze niet bewerken). Hallo system onderhoudt labels gebruikers afzonderlijk.  Het is dus een matrix met objecten van de Tag op elke asset.</td></tr>
<tr><td></td><td>Label</td><td>Tekenreeks</td><td>Een Hallo van tag Beschrijving asset.</td></tr>

<tr><td>FriendlyName ('friendlyName')</td><td></td><td></td><td>Deze eigenschap bevat een beschrijvende naam voor een asset. FriendlyName is een singleton-annotatie - slechts één FriendlyName tooan asset kan worden toegevoegd.  Alleen Hallo-gebruiker die FriendlyName-object is gemaakt kunt bewerken. (Beheerders en Asset eigenaars kunnen Hallo FriendlyName object verwijderen, maar deze niet bewerken). Hallo system onderhoudt beschrijvende namen van de gebruikers afzonderlijk.</td></tr>
<tr><td></td><td>friendlyName</td><td>Tekenreeks</td><td>Een beschrijvende naam van Hallo actief.</td></tr>

<tr><td>Schema ('schema')</td><td></td><td></td><td>Hallo Schema beschrijft Hallo-structuur van Hallo gegevens.  Het geeft een lijst van namen van Hallo kenmerken (kolom, kenmerk, veld, enzovoort), alsook andere metagegevens van het type.  Deze informatie wordt afgeleid van Hallo-gegevensbron.  Het schema is een singleton-annotatie - slechts één Schema kan worden toegevoegd voor een asset.</td></tr>
<tr><td></td><td>Kolommen</td><td>Kolom]</td><td>Een matrix met objecten van de kolom. Ze beschrijven Hallo kolom met gegevens die zijn afgeleid van Hallo-gegevensbron.</td></tr>

<tr><td>ColumnDescription ('columnDescriptions')</td><td></td><td></td><td>Deze eigenschap bevat een beschrijving op voor een kolom.  Elke gebruiker van Hallo-systeem kan hun eigen beschrijvingen voor meerdere kolommen (maximaal één per kolom) toevoegen. Alleen Hallo-gebruiker die ColumnDescription objecten heeft gemaakt, kunt deze bewerken.  (Beheerders en Asset eigenaars kunnen Hallo ColumnDescription object verwijderen, maar deze niet bewerken). Hallo system onderhoudt afzonderlijk kolombeschrijvingen van deze gebruiker.  Dus er is een matrix met objecten op elke asset ColumnDescription (één per kolom voor elke gebruiker die is bijgedragen hun kennis over Hallo kolom bovendien toopossibly met informatie afgeleid van Hallo gegevensbron).  Hallo ColumnDescription is los gebonden toohello Schema zodat niet gesynchroniseerd krijgt. Hallo ColumnDescription beschrijft een kolom die niet langer in het Hallo-schema bestaat.  Is toohello writer tookeep beschrijving en het schema gesynchroniseerd.  Hallo-gegevensbron wellicht ook kolommen beschrijving informatie en zijn extra ColumnDescription-objecten die moeten worden gemaakt wanneer het Hallo-programma wordt uitgevoerd.</td></tr>
<tr><td></td><td>Kolomnaam</td><td>Tekenreeks</td><td>Hallo-naam van deze beschrijving naar verwijst Hallo-kolom.</td></tr>
<tr><td></td><td>description</td><td>Tekenreeks</td><td>een korte beschrijving (2-3 regels) van Hallo-kolom.</td></tr>

<tr><td>ColumnTag ('columnTags')</td><td></td><td></td><td>Deze eigenschap bevat een code voor een kolom. Elke gebruiker van Hallo-systeem kunt meerdere labels voor een bepaalde kolom toevoegen en labels voor meerdere kolommen kunt toevoegen. Alleen Hallo-gebruiker die ColumnTag objecten heeft gemaakt, kunt deze bewerken. (Beheerders en Asset eigenaars kunnen Hallo ColumnTag object verwijderen, maar deze niet bewerken). Hallo system onderhoudt kolom labels van deze gebruikers afzonderlijk.  Het is dus een matrix van ColumnTag objecten op elke asset.  Hallo ColumnTag is los gebonden toohello schema zodat niet gesynchroniseerd krijgt. Hallo ColumnTag beschrijft een kolom die niet langer in het Hallo-schema bestaat.  Is toohello writer tookeep kolom label en het schema gesynchroniseerd.</td></tr>
<tr><td></td><td>Kolomnaam</td><td>Tekenreeks</td><td>Hallo-naam van deze code naar verwijst Hallo-kolom.</td></tr>
<tr><td></td><td>Label</td><td>Tekenreeks</td><td>Een beschrijving Hallo Opmaakkolom.</td></tr>

<tr><td>Expert ('experts')</td><td></td><td></td><td>Deze eigenschap bevat een gebruiker die wordt beschouwd als een expert in Hallo-gegevensset. Hallo-experts opinions(descriptions) belgrootte toohello boven op Hallo UX wanneer beschrijvingen. Elke gebruiker kan hun eigen deskundigen opgeven. Alleen die gebruiker kunt Hallo experts object bewerken. Beheerders en Asset eigenaars kunnen Hallo deskundige objecten verwijderen maar deze niet bewerken.</td></tr>
<tr><td></td><td>deskundige</td><td>SecurityPrincipal</td><td></td></tr>

<tr><td>Preview ('previews')</td><td></td><td></td><td>Hallo preview bevat een momentopname van de top 20 rijen Hallo van gegevens voor Hallo asset. Preview alleen zinvol zijn voor bepaalde typen van assets (het zinvol voor de tabel, maar niet voor de meting).</td></tr>
<tr><td></td><td>Voorbeeld</td><td>object]</td><td>Matrix van objecten die een kolom vertegenwoordigen.  Elk object heeft een eigenschapstoewijzing tooa kolom met een waarde voor de kolom voor Hallo rij.</td></tr>

<tr><td>AccessInstruction ('accessInstructions')</td><td></td><td></td><td></td></tr>
<tr><td></td><td>mimeType</td><td>Tekenreeks</td><td>Hallo MIME-type van Hallo inhoud.</td></tr>
<tr><td></td><td>Inhoud</td><td>Tekenreeks</td><td>Hallo-instructies voor hoe tooget toegang krijgen tot toothis gegevensasset. Hallo-inhoud is mogelijk een URL, een e-mailadres of een set instructies.</td></tr>

<tr><td>TableDataProfile ('tableDataProfiles')</td><td></td><td></td><td></td></tr>
<tr><td></td><td>numberOfRows</td></td><td>int</td><td>het aantal rijen in de gegevensset Hallo Hallo</td></tr>
<tr><td></td><td>Grootte</td><td>lang</td><td>Hallo-grootte in bytes van Hallo-gegevensset.  </td></tr>
<tr><td></td><td>schemaModifiedTime</td><td>Tekenreeks</td><td>Hallo laatste tijd Hallo schema is gewijzigd</td></tr>
<tr><td></td><td>dataModifiedTime</td><td>Tekenreeks</td><td>Hallo laatste tijd Hallo verzameling is gewijzigd (gegevens werd toegevoegd, gewijzigd, of verwijderen)</td></tr>

<tr><td>ColumnsDataProfile ('columnsDataProfiles')</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Kolommen</td></td><td>ColumnDataProfile]</td><td>Een matrix van profielen voor kolom-gegevens.</td></tr>

<tr><td>ColumnDataClassification ('columnDataClassifications')</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Kolomnaam</td><td>Tekenreeks</td><td>Hallo-naam van deze categorie heeft betrekking op Hallo-kolom.</td></tr>
<tr><td></td><td>Classificatie</td><td>Tekenreeks</td><td>Hallo classificatie van Hallo-gegevens in deze kolom.</td></tr>

<tr><td>Documentatie ("documentatie")</td><td></td><td></td><td>Een opgegeven activum kan slechts één documentatie gekoppeld hebben.</td></tr>
<tr><td></td><td>mimeType</td><td>Tekenreeks</td><td>Hallo MIME-type van Hallo inhoud.</td></tr>
<tr><td></td><td>Inhoud</td><td>Tekenreeks</td><td>Hallo documentatie inhoud.</td></tr>

</table>

### <a name="common-types"></a>Algemene typen
Algemene typen kunnen worden gebruikt als Hallo typen voor eigenschappen, maar er zijn geen Items.

<table>
<tr><td><b>Algemeen Type</b></td><td><b>Eigenschappen</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr>
<tr><td>DataSourceInfo</td><td></td><td></td><td></td></tr>
<tr><td></td><td>SourceType</td><td>Tekenreeks</td><td>Beschrijft Hallo type gegevensbron.  Bijvoorbeeld: SQL Server, Oracle-Database, enzovoort.  </td></tr>
<tr><td></td><td>objectType</td><td>Tekenreeks</td><td>Hallo soort object in de gegevensbron Hallo beschrijft. Bijvoorbeeld: tabel, weergave voor SQL Server.</td></tr>

<tr><td>DataSourceLocation</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Protocol</td><td>Tekenreeks</td><td>Vereist. Beschrijft een toocommunicate protocol dat wordt gebruikt met Hallo-gegevensbron. Bijvoorbeeld: "tds' voor SQl Server, 'oracle' voor Oracle, enzovoort. Raadpleeg te[gegevensbron verwijzing opgegeven - DSL structuur](data-catalog-dsr.md) voor Hallo lijst met ondersteunde protocollen.</td></tr>
<tr><td></td><td>Adres</td><td>Woordenlijst<string, object></td><td>Vereist. Adres is een set van specifieke toohello-protocol voor gegevens die gebruikte tooidentify Hallo-gegevensbron waarnaar wordt verwezen. Hallo adresgegevens binnen het bereik van bepaalde tooa protocol, en dus nutteloos zonder te weten Hallo-protocol.</td></tr>
<tr><td></td><td>Verificatie</td><td>Tekenreeks</td><td>Optioneel. Hallo-verificatieschema gebruikt toocommunicate met Hallo-gegevensbron. Bijvoorbeeld: windows, oauth, enzovoort.</td></tr>
<tr><td></td><td>connectionProperties</td><td>Woordenlijst<string, object></td><td>Optioneel. Meer informatie over het tooconnect tooa-gegevensbron.</td></tr>

<tr><td>SecurityPrincipal</td><td></td><td></td><td>Hallo back-end voert een validatie van de opgegeven eigenschappen met AAD tijdens de publicatie.</td></tr>
<tr><td></td><td>UPN</td><td>Tekenreeks</td><td>Uniek e-mailadres van de gebruiker. Moet worden opgegeven als object-id is niet opgegeven of in de context van de eigenschap 'lastRegisteredBy', anders optionele Hallo.</td></tr>
<tr><td></td><td>object-id</td><td>GUID</td><td>Gebruiker of beveiligingsgroep groep AAD identiteit. Optioneel. Moet worden opgegeven als upn niet, anders is optioneel opgegeven is.</td></tr>
<tr><td></td><td>Voornaam</td><td>Tekenreeks</td><td>De voornaam van de gebruiker (ter informatie weergegeven). Optioneel. Alleen geldig in de context van de eigenschap 'lastRegisteredBy' Hallo. Kan niet worden opgegeven bij het opgeven van beveiligings-principal voor 'functies', 'machtigingen' en 'deskundigen'.</td></tr>
<tr><td></td><td>Achternaam</td><td>Tekenreeks</td><td>De achternaam van de gebruiker (ter informatie weergegeven). Optioneel. Alleen geldig in de context van de eigenschap 'lastRegisteredBy' Hallo. Kan niet worden opgegeven bij het opgeven van beveiligings-principal voor 'functies', 'machtigingen' en 'deskundigen'.</td></tr>

<tr><td>Kolom</td><td></td><td></td><td></td></tr>
<tr><td></td><td>naam</td><td>Tekenreeks</td><td>Naam van het Hallo-kolom of kenmerk.</td></tr>
<tr><td></td><td>type</td><td>Tekenreeks</td><td>het gegevenstype van kolom hello of een kenmerk. Hallo toegestane typen zijn afhankelijk van gegevens sourceType van Hallo actief.  Alleen een subset van de typen wordt ondersteund.</td></tr>
<tr><td></td><td>maxLength</td><td>int</td><td>Hallo maximaal toegestane lengte voor Hallo kolom of kenmerk. Afgeleid van de gegevensbron. Alleen van toepassing toosome brontypen.</td></tr>
<tr><td></td><td>precisie</td><td>Byte</td><td>Hallo precisie voor Hallo kolom of kenmerk. Afgeleid van de gegevensbron. Alleen van toepassing toosome brontypen.</td></tr>
<tr><td></td><td>isNullable</td><td>Booleaanse waarde</td><td>Hallo-kolom wordt aangegeven of toohave een null-waarde of niet toegestaan. Afgeleid van de gegevensbron. Alleen van toepassing toosome brontypen.</td></tr>
<tr><td></td><td>expressie</td><td>Tekenreeks</td><td>Als het Hallo-waarde is een berekende kolom, bevat dit veld Hallo-expressie waarmee Hallo waarde wordt uitgedrukt. Afgeleid van de gegevensbron. Alleen van toepassing toosome brontypen.</td></tr>

<tr><td>ColumnDataProfile</td><td></td><td></td><td></td></tr>
<tr><td></td><td>Kolomnaam </td><td>Tekenreeks</td><td>Hallo-naam van Hallo kolom</td></tr>
<tr><td></td><td>type </td><td>Tekenreeks</td><td>Hallo-type van kolom Hallo</td></tr>
<tr><td></td><td>min. </td><td>Tekenreeks</td><td>Hallo-minimumwaarde in het Hallo-gegevensset</td></tr>
<tr><td></td><td>Maximum aantal </td><td>Tekenreeks</td><td>maximale waarde in de gegevensset Hallo Hallo</td></tr>
<tr><td></td><td>Gem. </td><td>dubbele</td><td>gemiddelde waarde in de gegevensset Hallo Hallo</td></tr>
<tr><td></td><td>STDEV </td><td>dubbele</td><td>de standaarddeviatie Hallo voor Hallo-gegevensset</td></tr>
<tr><td></td><td>nullCount </td><td>int</td><td>Hallo-telling van null-waarden in de gegevensset Hallo</td></tr>
<tr><td></td><td>distinctCount  </td><td>int</td><td>het aantal afzonderlijke waarden in de gegevensset Hallo Hallo</td></tr>


</table>

## <a name="asset-identity"></a>Asset-identiteit
Azure Data Catalog gebruikt "protocol" en identiteitseigenschappen van Hallo 'adres' eigenschappenverzameling Hallo DataSourceLocation 'dsl' eigenschap toogenerate identiteit van Hallo activa en gebruikte tooaddress Hallo asset binnen Hallo catalogus.
Hallo "tds" protocol heeft bijvoorbeeld identiteitseigenschappen 'server', 'database', 'schema' en 'object'. Hallo combinaties van Hallo-protocol en Hallo identiteitseigenschappen zijn gebruikte toogenerate Hallo identiteit van de SQL Server-tabel Asset Hallo.
Azure Data Catalog bevat verschillende ingebouwde gegevensbron-protocollen die worden vermeld op [gegevensbron verwijzing opgegeven - DSL structuur](data-catalog-dsr.md).
Hallo set met ondersteunde protocollen kan worden uitgebreid via een programma (Zie tooData catalogus REST API-verwijzing). Beheerders van Hallo catalogus kunnen aangepaste gegevensbron protocollen registreren. Hallo beschrijft volgende tabel Hallo eigenschappen nodig tooregister een aangepaste protocol.

### <a name="custom-data-source-protocol-specification"></a>Aangepaste gegevensbron protocol specification
<table>
<tr><td><b>Type</b></td><td><b>Eigenschappen</b></td><td><b>Gegevenstype</b></td><td><b>Opmerkingen</b></td></tr>

<tr><td>DataSourceProtocol</td><td></td><td></td><td></td></tr>
<tr><td></td><td>naamruimte</td><td>Tekenreeks</td><td>Hallo-naamruimte van het Hallo-protocol. Namespace moet vallen tussen-1 too255 tekens lang zijn, een of meer niet-lege onderdelen gescheiden door een punt (.) bevatten. Elk deel moet tussen 1 too255 tekens lang, met een letter beginnen en alleen letters en cijfers bevatten.</td></tr>
<tr><td></td><td>naam</td><td>Tekenreeks</td><td>Hallo-naam van het Hallo-protocol. Naam moet 1 too255 tekens lang zijn, beginnen met een letter en mag alleen letters, cijfers en Hallo streepje (-).</td></tr>
<tr><td></td><td>identityProperties</td><td>DataSourceProtocolIdentityProperty]</td><td>Lijst van identiteitseigenschappen, moet ten minste één echter meer dan 20 eigenschappen bevatten. Bijvoorbeeld: 'server', 'database', 'schema', 'object' identiteitseigenschappen van Hallo "tds" protocol zijn.</td></tr>
<tr><td></td><td>identitySets</td><td>DataSourceProtocolIdentitySet]</td><td>Hiermee stelt u de lijst van identiteit. Hiermee definieert u sets identiteitseigenschappen die geldige asset-id voorstelt. Moet ten minste één echter meer dan 20 sets bevatten. Bijvoorbeeld: {'server', 'database', 'schema' en 'object'} is ingesteld voor "tds" protocol, dat Hiermee definieert u de id van Sql Server-tabel actief identiteit.</td></tr>

<tr><td>DataSourceProtocolIdentityProperty</td><td></td><td></td><td></td></tr>
<tr><td></td><td>naam</td><td>Tekenreeks</td><td>Hallo-naam van Hallo-eigenschap. Naam mag uit 1 too100 tekens lang zijn, start met een letter en mag alleen letters en cijfers bevatten.</td></tr>
<tr><td></td><td>type</td><td>Tekenreeks</td><td>Hallo-type van Hallo-eigenschap. Ondersteunde waarden: 'bool,' boolean ', 'byte', 'guid', 'int', 'integer', 'lang', 'string', "url"</td></tr>
<tr><td></td><td>ignoreCase</td><td>BOOL</td><td>Hiermee wordt aangegeven of geval moet worden genegeerd wanneer u de waarde van eigenschap. Kan alleen worden opgegeven voor eigenschappen met het type 'string'. Standaard is ingesteld op false.</td></tr>
<tr><td></td><td>urlPathSegmentsIgnoreCase</td><td>BOOL]</td><td>Hiermee wordt aangegeven of de aanvraag voor elk segment van Hallo-url-pad moet worden genegeerd. Kan alleen worden opgegeven voor eigenschappen met het type "url". Standaardwaarde is [false].</td></tr>

<tr><td>DataSourceProtocolIdentitySet</td><td></td><td></td><td></td></tr>
<tr><td></td><td>naam</td><td>Tekenreeks</td><td>Hallo-naam van de identiteit Hallo ingesteld.</td></tr>
<tr><td></td><td>properties</td><td>String]</td><td>Hallo-lijst van identiteitseigenschappen opgenomen in deze identiteit ingesteld. Het mag geen duplicaten bevatten. Elke eigenschap identiteitset waarnaar moet worden gedefinieerd in de lijst Hallo met 'identityProperties' van het Hallo-protocol.</td></tr>

</table>

## <a name="roles-and-authorization"></a>Rollen en -autorisatie
Microsoft Azure Data Catalog biedt autorisatiemogelijkheden voor voor CRUD-bewerkingen op activa en aantekeningen.

## <a name="key-concepts"></a>Belangrijkste concepten
Hello Azure Data Catalog maakt gebruik van twee autorisatiemechanismen:

* Verificatie op basis van rollen
* Machtiging gebaseerde verificatie

### <a name="roles"></a>Rollen
Er zijn drie rollen: **beheerder**, **eigenaar**, en **Inzender**.  Elke functie heeft een bereik en de rechten die worden samengevat in de volgende tabel Hallo.

<table><tr><td><b>Rol</b></td><td><b>Bereik</b></td><td><b>Rechten</b></td></tr><tr><td>Beheerder</td><td>Catalogus (alle activa/aantekeningen in Hallo catalogus)</td><td>Lees verwijderen ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Eigenaar</td><td>Elke asset (hoofditem)</td><td>Lees verwijderen ViewRoles

ChangeOwnership ChangeVisibility ViewPermissions</td></tr><tr><td>Inzender</td><td>Elke individuele asset en aantekening</td><td>Lees Update verwijderen ViewRoles Opmerking: alle Hallo rechten worden ingetrokken als Hallo lezen rechts op Hallo item van Hallo Inzender is ingetrokken</td></tr></table>

> [!NOTE]
> **Lees**, **Update**, **verwijderen**, **ViewRoles** rechten zijn van toepassing tooany item (asset of aantekening) terwijl **TakeOwnership**, **ChangeOwnership**, **ChangeVisibility**, **ViewPermissions** zijn alleen van toepassing toohello hoofdmap asset.
> 
> **Verwijder** recht geldt tooan item en subitems of één item eronder. Bijvoorbeeld, verwijdert een asset ook alle aantekeningen voor de activa.
> 
> 

### <a name="permissions"></a>Machtigingen
De machtiging is als lijst met vermeldingen voor toegangsbeheer. Elk access control entry toewijst set rechten tooa beveiligings-principal. Machtigingen kunnen alleen worden opgegeven voor een asset (dat wil zeggen hoofditem) en toohello asset en alle subitems toepassen.

Tijdens het Hallo **Azure Data Catalog** bekijken, alleen **lezen** rechts wordt ondersteund in Hallo machtigingen lijst tooenable scenario toorestrict zichtbaarheid van een asset.

Alle geverifieerde gebruikers heeft standaard **lezen** rechts voor elk item in de catalogus Hallo tenzij zichtbaarheid beperkt toohello set principals in Hallo machtigingen.

## <a name="rest-api"></a>REST API
**PLAATSEN** en **POST** item weergeven aanvragen kunnen worden gebruikt toocontrol rollen en machtigingen: in toevoeging tooitem nettolading, twee eigenschappen kunnen worden opgegeven **rollen** en  **machtigingen**.

> [!NOTE]
> **machtigingen** alleen van toepassing tooa hoofditem.
> 
> **Eigenaar** rol alleen van toepassing tooa hoofditem.
> 
> Standaard wanneer een item wordt gemaakt in de catalogus Hallo de **Inzender** toohello momenteel geverifieerde gebruiker is ingesteld. Als het item moet worden bijgewerkt door iedereen, **Inzender** te moet worden ingesteld&lt;iedereen&gt; speciale beveiligings-principal in Hallo **rollen** eigenschap als item eerst gepubliceerd () Raadpleeg de toohello na voorbeeld). **Inzender** kan niet worden gewijzigd en blijft hetzelfde tijdens de levensduur van een item Hallo (zelfs **beheerder** of **eigenaar** geen Hallo rechts toochange hello  **Inzender**). alleen de waarde ondersteund voor expliciete instelling Hallo HALLO hallo **Inzender** is &lt;iedereen&gt;: **Inzender** mag alleen een gebruiker die een item heeft gemaakt of &lt; Iedereen&gt;.
> 
> 

### <a name="examples"></a>Voorbeelden
**Stel Inzender te&lt;iedereen&gt; bij het publiceren van een item.**
Speciale beveiligings-principal &lt;iedereen&gt; objectId '00000000-0000-0000-0000-000000000201' is.
  **POST** https://api.azuredatacatalog.com/catalogs/default/views/tables/?api-version=2016-03-30

> [!NOTE]
> Sommige implementaties van HTTP-client kunnen aanvragen in het antwoord tooa 302 van Hallo server automatisch opnieuw worden uitgegeven, maar doorgaans van strook / autorisatie-header van Hallo-aanvraag. Aangezien Hallo autorisatie-header vereist toomake aanvragen tooAzure Data Catalog is, moet u ervoor zorgen Hallo autorisatie-header wordt nog steeds worden opgegeven als opnieuw uitgeven van een aanvraag tooa omleidingslocatie die is opgegeven door Azure Data Catalog. Hallo volgende voorbeeldcode laat zien met behulp van Hallo .NET HttpWebRequest-object.
> 
> 

**Hoofdtekst**

    {
        "roles": [
            {
                "role": "Contributor",
                "members": [
                    {
                        "objectId": "00000000-0000-0000-0000-000000000201"
                    }
                ]
            }
        ]
    }

  **Eigenaren toewijzen en zichtbaarheid voor een bestaande hoofditem beperken**: **plaatsen** https://api.azuredatacatalog.com/catalogs/default/views/tables/042297b0...1be45ecd462a?api-version=2016-03-30

    {
        "roles": [
            {
                "role": "Owner",
                "members": [
                    {
                        "objectId": "c4159539-846a-45af-bdfb-58efd3772b43",
                        "upn": "user1@contoso.com"
                    },
                    {
                        "objectId": "fdabd95b-7c56-47d6-a6ba-a7c5f264533f",
                        "upn": "user2@contoso.com"
                    }
                ]
            }
        ],
        "permissions": [
            {
                "principal": {
                    "objectId": "27b9a0eb-bb71-4297-9f1f-c462dab7192a",
                    "upn": "user3@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            },
            {
                "principal": {
                    "objectId": "4c8bc8ce-225c-4fcf-b09a-047030baab31",
                    "upn": "user4@contoso.com"
                },
                "rights": [
                    {
                        "right": "Read"
                    }
                ]
            }
        ]
    }

> [!NOTE]
> In de opslag niet hoeft de nettolading van een item in de hoofdtekst van het Hallo toospecify: PUT mag alleen rollen gebruikte tooupdate en/of machtigingen.
> 
> 

<!--Image references-->
[1]: ./media/data-catalog-developer-concepts/concept2.png

---
title: aaaMoving gegevens tussen cloud uitgebreide databases | Microsoft Docs
description: Legt uit hoe toomanipulate shards en verplaatsen van gegevens via een zelf gehoste service met behulp van de elastische database API's.
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 204fd902-0397-4185-985a-dea3ed7c7d9f
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 629dee06e22609e9b61edf93ba5c38d997132d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="moving-data-between-scaled-out-cloud-databases"></a>Gegevens verplaatsen tussen uitgeschaalde clouddatabases
Als u een Software als een Service-ontwikkelaar bent en plotseling uw app grote vraag ondergaat, moet u tooaccommodate Hallo groei. Zodat toevoegen u meer databases (shards). Hoe opnieuw u Hallo gegevens toohello nieuwe databases zonder te verstoren Hallo gegevensintegriteit distribueren? Gebruik Hallo **gesplitste merge tool** toomove gegevens van beperkte databases toohello nieuwe databases.  

Hallo gesplitste merge tool wordt uitgevoerd als een Azure-web-service. Een beheerder of ontwikkelaar maakt gebruik van Hallo hulpprogramma toomove shardlets (gegevens uit een shard) tussen verschillende databases (shards). Hallo-hulpprogramma gebruikt shard kaart management toomaintain Hallo servicedatabase met metagegevens en zorg ervoor dat de consistente toewijzingen.

![Overzicht][1]

## <a name="download"></a>Downloaden
[Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge/)

## <a name="documentation"></a>Documentatie
1. [Elastische database gesplitste Merge tool-zelfstudie](sql-database-elastic-scale-configure-deploy-split-and-merge.md)
2. [Gesplitste samenvoegen Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md)
3. [Beveiligingsoverwegingen gesplitste samenvoegen](sql-database-elastic-scale-split-merge-security-configuration.md)
4. [Shard-toewijzingsbeheer](sql-database-elastic-scale-shard-map-management.md)
5. [Migreren van bestaande databases tooscale-out](sql-database-elastic-convert-to-use-elastic-tools.md)
6. [Hulpprogramma's voor elastische database](sql-database-elastic-scale-introduction.md)
7. [Elastische Database extra verklarende woordenlijst](sql-database-elastic-scale-glossary.md)

## <a name="why-use-hello-split-merge-tool"></a>Waarom Hallo gesplitste merge tool gebruiken?
**Flexibiliteit**

Toepassingen moeten toostretch flexibel buiten Hallo limieten van één Azure SQL DB-database. Hallo hulpprogramma toomove gegevens gebruiken als de benodigde toonew databases terwijl de integriteit te behouden.

**Toogrow splitsen** 

Moet u tooincrease algehele capaciteit toohandle explosief gegroeid. Extra capaciteit toodo dus maken door sharding Hallo gegevens en over stapsgewijs meer databases verdeeld totdat de capaciteitsbehoeften is voldaan. Dit is een goed voorbeeld van de splitsen' Hallo-functie. 

**Tooshrink samenvoegen**

Capaciteit moet verkleinen vanwege toohello seizoensgebonden aard van een bedrijf. Hallo hulpprogramma kunt die u toofewer schaaleenheden terugschroeven wanneer bedrijven wordt vertraagd. Hallo '' samenvoegfunctie in Hallo elastisch schalen gesplitste samenvoegen Service bevat informatie over deze vereiste. 

**Hotspots beheren door shardlets verplaatsen**

Met meerdere tenants per database kan Hallo toewijzing van shardlets tooshards toocapacity knelpunten leiden op sommige shards. Dit is vereist voor opnieuw toewijzen van shardlets of verplaatsen bezet shardlets toonew of minder gebruikte shards. 

## <a name="concepts--key-features"></a>Concepten & belangrijke functies
**Klant gehoste services**

Hallo split-samenvoegen wordt geleverd als een klant gehoste service. U moet implementeren en Hallo service hosten in uw Microsoft Azure-abonnement. Hallo-pakket die u van NuGet downloaden bevat een configuratie sjabloon toocomplete met Hallo-informatie voor uw specifieke implementatie. Zie Hallo [gesplitste samenvoegen zelfstudie](sql-database-elastic-scale-configure-deploy-split-and-merge.md) voor meer informatie. Aangezien het Hallo-service wordt uitgevoerd in uw Azure-abonnement, kunt u instellen en configureren van de meeste beveiligingsaspecten van Hallo-service. Hallo standaardsjabloon omvat Hallo opties tooconfigure SSL, op basis van certificaten voor clientverificatie, versleuteling voor de opgeslagen referenties, DoS beveiligen en IP-beperkingen. U vindt meer informatie over het Hallo beveiligingsaspecten in Hallo document na [gesplitste samenvoegen Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).

Hallo standaard geïmplementeerd met een Webrol en een werknemer de service wordt uitgevoerd. Elk Hallo A1-VM-grootte in Azure Cloud Services gebruikt. Terwijl u kunt deze instellingen niet wijzigen bij het implementeren van Hallo pakket, kunt u ze na een geslaagde implementatie in Hallo met cloudservice (via hello Azure-portal) wijzigen. Houd er rekening mee dat werkrol Hallo niet meer dan één exemplaar moet worden geconfigureerd voor technische redenen. 

**Integratie van shard-kaart**

Hallo gesplitste samenvoegen service communiceert met de Hallo shard-toewijzing van de toepassing hello. Wanneer u Hallo gesplitste samenvoegen service toosplit of merge bereiken of toomove shardlets tussen shards, houdt Hallo service automatisch Hallo shard-toewijzing van toodate. toodo dus Hallo service toohello shard kaart manager-database van de toepassing hello verbinding maakt en onderhoudt bereiken en toewijzingen als voortgang merge-gesplitste/move-aanvragen. Dit zorgt ervoor dat Hallo shard-toewijzing altijd geeft een actuele weergave wanneer gesplitste samenvoegbewerkingen gaat op. Splitsen, zijn samenvoegen en shardlet movement-bewerkingen door het verplaatsen van een batch shardlets van Hallo bron shard toohello doel shard geïmplementeerd. Tijdens het Hallo shardlet verkeer bewerking Hallo shardlets onderwerp toohello huidige batch zijn gemarkeerd als offline in Hallo shard-toewijzing en zijn niet beschikbaar voor gegevensafhankelijke routering verbindingen met het Hallo **OpenConnectionForKey** API. 

**Consistente shardlet-verbindingen**

Als verplaatsing van gegevens voor een nieuwe batch shardlets wordt gestart, zijn alle shard-toewijzing opgegeven gegevensafhankelijke routering verbindingen toohello shard opslag Hallo shardlet gedode en volgende verbindingen uit Hallo shard-toewijzing API's toohello deze shardlets zijn geblokkeerd terwijl Hallo gegevensverplaatsing wordt uitgevoerd in de volgorde tooavoid inconsistenties. Verbindingen tooother shardlets op Hallo dezelfde shard wordt ook ophalen afgesloten, maar opnieuw slaagt onmiddellijk taak opnieuw wordt uitgevoerd. Zodra het Hallo-batch is verplaatst, Hallo shardlets online opnieuw voor Hallo doel shard zijn gemarkeerd en Hallo brongegevens uit Hallo bron shard is verwijderd. Hallo-service gaat door deze stappen voor elke batch totdat alle shardlets zijn verplaatst. Dit leidt tooseveral kill-bewerkingen tijdens Hallo Hallo voltooid splitsen/samenvoegen/move-bewerking.  

**Shardlet beschikbaarheid van beheren**

Hallo-bereik van onbeschikbaarheid tooone batch shardlets beperken Hallo verbinding als beëindigt, kan de huidige batch toohello van shardlets zoals hierboven wordt beschreven op een tijdstip worden beperkt. Dit heeft de voorkeur boven een benadering waarbij Hallo voltooid shard blijft offline voor alle bijbehorende shardlets in Hallo loop van een gesplitste of merge-bewerking. Hallo-grootte van een batch, gedefinieerd als het aantal unieke shardlets toomove Hallo tegelijk, is een configuratieparameter. Het kan worden gedefinieerd voor elke bewerking samenvoegen en splitsen afhankelijk van de beschikbaarheid en prestaties behoeften van de toepassing hello. Houd er rekening mee dat Hallo-bereik dat wordt vergrendeld in Hallo shard-toewijzing kan niet groter zijn dan Hallo batchgrootte opgegeven. Dit is omdat het Hallo-service hervat Hallo bereik grootte zodat het werkelijke aantal sharding sleutelwaarden in Hallo gegevens Hallo ongeveer Hallo batchgrootte overeenkomt met. Dit is belangrijk tooremember met name voor zeer ingevuld sharding-sleutels. 

**Metagegevensopslag**

Hallo gesplitste samenvoegen service gebruikt een database toomaintain de status en de tookeep logboeken tijdens de verwerking van aanvragen. Hallo gebruiker deze database wordt gemaakt in het abonnement en voorziet Hallo-verbindingsreeks in het configuratiebestand Hallo voor Hallo service-implementatie. Beheerders van de organisatie van de gebruiker Hallo kunnen ook verbinding maken toothis database tooreview aanvraag voortgang en tooinvestigate gedetailleerde informatie over mogelijke fouten.

**Sharding-awareness**

Hallo gesplitste samenvoegen service onderscheidt tussen (1) de shard-tabellen, (2) verwijzingsdimensies en (3) de normale tabellen. Hallo-semantiek van een merge-gesplitste/move-bewerking afhankelijk type Hallo Hallo tabel die wordt gebruikt en wordt als volgt gedefinieerd: 

* **Shard tabellen**: gesplitste, samenvoegen en migratiebewerkingen shardlets van bron tootarget shard verplaatsen. Na voltooiing van Hallo algemene vragen die shardlets op Hallo-bron niet langer aanwezig zijn. Houd er rekening mee die Hallo doeltabellen tooexist op Hallo doel shard nodig hebt en mag geen gegevens in Hallo doel bereik eerdere tooprocessing van Hallo-bewerking. 
* **Verwijzen naar tabellen**: voor verwijzingstabellen, splitsing hello, samenvoegen en bewerkingen Hallo gegevens kopiëren van Hallo bron toohello doel shard verplaatsen. Let echter op dat er geen wijzigingen doorgevoerd op Hallo doel shard voor een bepaalde tabel als een rij al aanwezig in deze tabel op het Hallo-doel is. Hallo tabel heeft toobe leeg voor een verwijzing naar tabel kopiëren bewerking tooget verwerkt.
* **Andere tabellen**: andere tabellen kunnen worden gebruikt op het Hallo-bron- of Hallo-doel van een bewerking voor samenvoegen en splitsen. Hallo gesplitste samenvoegen service negeert deze tabellen voor gegevensverplaatsing of te kopiëren. Let echter op dat ze deze bewerkingen in het geval van beperkingen kunnen verstoren.

Hallo-informatie van verwijzing versus shard tabellen wordt verstrekt door Hallo **SchemaInfo** API's op Hallo shard-kaart. Hallo volgende voorbeeld illustreert Hallo gebruik van deze API's op een gegeven shard kaart manager object smm: 

    // Create hello schema annotations 
    SchemaInfo schemaInfo = new SchemaInfo(); 

    // Reference tables 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "region")); 
    schemaInfo.Add(new ReferenceTableInfo("dbo", "nation")); 

    // Sharded tables 
    schemaInfo.Add(new ShardedTableInfo("dbo", "customer", "C_CUSTKEY")); 
    schemaInfo.Add(new ShardedTableInfo("dbo", "orders", "O_CUSTKEY")); 

    // Publish 
    smm.GetSchemaInfoCollection().Add(Configuration.ShardMapName, schemaInfo); 

Hallo tabellen 'regio' en 'land' worden gedefinieerd als verwijzingstabellen en met gesplitste of merge/verplaatsen bewerkingen moeten worden gekopieerd. 'klant' en 'orders' worden op zijn beurt gedefinieerd als shard tabellen. C_CUSTKEY en O_CUSTKEY fungeren als Hallo sharding-sleutel. 

**Referentiële integriteit**

Hallo gesplitste samenvoegen service analyseert afhankelijkheden tussen de tabellen en sleutel-primaire refererende sleutels toostage Hallo bewerkingen voor het verplaatsen van verwijzingsdimensies en shardlets gebruikt. In het algemeen verwijzingsdimensies gekopieerd eerst in volgorde van de afhankelijkheid, worden in volgorde van hun afhankelijkheden in elke batch shardlets gekopieerd. Dit is noodzakelijk om FK PK beperkingen op Hallo doel shard worden gehonoreerd Hallo nieuwe gegevens ontvangt. 

**Consistentie van shard-toewijzing en de uiteindelijke voltooiing**

Hallo aanwezigheid van fouten, Hallo gesplitste samenvoegen service operations hervat na een storing en is erop gericht toocomplete aanwezig in voortgang aanvragen. Echter mogelijk zijn er onherstelbare situaties, bijvoorbeeld wanneer Hallo doel shard zoekraakt of wordt geknoeid niet meer worden hersteld. In deze omstandigheden kunnen sommige shardlets die moesten toobe verplaatst op Hallo bron shard tooreside blijven. Hallo service zorgt ervoor dat shardlet toewijzingen alleen bijgewerkt worden nadat Hallo gegevens die nodig zijn met succes gekopieerde toohello doel zijn. Shardlets zijn alleen op Hallo bron verwijderd nadat alle hun gegevens zijn toohello doel gekopieerd en bijbehorende Hallo-toewijzingen zijn bijgewerkt. Hallo verwijderingsbewerking gebeurt op Hallo achtergrond terwijl Hallo bereik op Hallo doel shard al online is. Hallo gesplitste samenvoegen service zorgt altijd of Hallo-toewijzingen die zijn opgeslagen in de shard-toewijzing Hallo juist is.

## <a name="hello-split-merge-user-interface"></a>Hallo gesplitste merge-gebruikersinterface
Hallo gesplitste samenvoegen servicepakket omvat een werkrol en een Webrol. Hallo-Webrol is gebruikte toosubmit gesplitste merge-aanvragen op interactieve wijze. onderdelen van de gebruikersinterface Hallo Hallo zijn als volgt:

* Type voor bewerking: type Hallo-bewerking is een keuzerondje die Hallo soort bewerking uitgevoerd door het Hallo-service voor deze aanvraag bepaalt. U kunt kiezen tussen Hallo gesplitste, samenvoegen en scenario's te verplaatsen. U kunt ook een eerder ingediende bewerking annuleren. U kunt gesplitste gebruiken, samenvoegen en aanvragen voor de shard-kaarten bereik verplaatsen. Lijst shard wijst alleen ondersteuning migratiebewerkingen.
* Shard-toewijzing: Hallo volgende sectie van de aanvraag parameters behandeld informatie over Hallo shard-toewijzing en het Hallo-database die als host fungeert voor de shard-kaart. In het bijzonder, moet u tooprovide Hallo-naam van hello Azure SQL Database-server en database Hallo shardmap die als host fungeert, referenties tooconnect toohello shard toewijzen van de database en ten slotte Hallo naam van Hallo shard-toewijzing. Op dit moment accepteert Hallo bewerking alleen een enkele set referenties. Deze referenties moeten voldoende machtigingen toohave tooperform toohello shard-kaart, evenals toohello gebruikersgegevens op Hallo shards wordt gewijzigd.
* Bron-bereik (splitsen en samenvoegen): een bewerking voor samenvoegen en splitsen een bereik met behulp van de lage en hoge sleutel verwerkt. een bewerking met een niet-gebonden hoge sleutelwaarde: selectievakje toospecify selectievakje 'hoge sleutel is max' Hallo en Hallo hoge sleutel veld leeg laat. Hallo bereik sleutelwaarden die u opgeeft doen niet nodig tooprecisely overeen met een toewijzing en de grenzen in de shard-toewijzing. Als u geen geen begrenzingen bereik helemaal opgeeft wordt Hallo-service afgeleid Hallo dichtstbijzijnde bereik voor u automatisch. U kunt Hallo GetMappings.ps1 PowerShell script tooretrieve Hallo huidige toewijzingen gebruiken in een bepaalde shard-toewijzing.
* Gesplitste bron gedrag (splitsen): Hallo punt toosplit Hallo bronbereik voor split-bewerkingen te definiëren. U doen dit door op te geven Hallo sharding sleutel waar u Hallo toooccur splitsen. Hallo-keuzerondje gebruiken of u wilt dat Hallo onderste gedeelte van Hallo bereik (met uitzondering van Hallo sleutel splitsen) toomove of of u Hallo bovenste deel toomove (inclusief Hallo split-sleutel) wilt opgeven.
* Bron Shardlet (verplaatsen): verplaatsen operations verschillen van gesplitste of samenvoegen van bewerkingen zoals een bereik toodescribe Hallo-bron is niet vereist. Een bron voor het verplaatsen wordt simpelweg aangeduid met Hallo sharding-sleutelwaarde dat u van plan toomove bent.
* Shard (splitsen) als doel: nadat u de Hallo informatie hebt opgegeven op de bron van de splitsbewerking Hallo, moet u toodefine waar u Hallo gegevens toobe tooby verstrekken hello Azure SQL Db-server en de databasenaam voor Hallo doel gekopieerd.
* Doelbereik (samenvoegen): samenvoegbewerkingen shardlets tooan bestaande shard verplaatsen. U identificeren Hallo bestaande shard door te geven Hallo bereik grenzen van de bestaande Hallo-bereik dat u wilt dat toomerge met.
* Batchgrootte: Hallo batch grootte besturingselementen Hallo aantal shardlets die offline gaan op een moment tijdens Hallo gegevensverplaatsing. Dit is een integerwaarde waar u lagere waarden kunt gebruiken wanneer u gevoelige toolong perioden met uitvaltijd voor shardlets zijn. Hogere waarden wordt verhoogd Hallo-tijd die een bepaalde shardlet offline maar de prestaties mogelijk verbeterd.
* Bewerking-Id (annuleren): Als u er een bewerking die niet meer nodig hebt, kunt u Hallo bewerking annuleren door op te geven van de bewerkings-ID in dit veld. U kunt Hallo bewerkings-ID ophalen uit tabel Hallo aanvraag-status (Zie de sectie 8.1) of van Hallo-uitvoer in webbrowser Hallo waar u Hallo aanvraag ingediend.

## <a name="requirements-and-limitations"></a>Vereisten en beperkingen
de huidige implementatie Hallo van Hallo gesplitste samenvoegen service is onderwerp toohello volgen de vereisten en beperkingen: 

* Hallo shards moeten tooexist en zijn geregistreerd in de shard-toewijzing Hallo voordat een gesplitste merge-bewerking op deze shards kan worden uitgevoerd. 
* Hallo-service maakt geen tabellen of andere databaseobjecten automatisch als onderdeel van bewerkingen. Dit betekent dat Hallo-schema voor alle shard-tabellen en verwijzen naar tabellen moeten tooexist op Hallo doel shard voorafgaande tooany splitsen/samenvoegen/move-bewerking. Shard tabellen zijn in het bijzonder vereist toobe in Hallo bereik waar de nieuwe shardlets toobe toegevoegd door een merge-gesplitste/move-bewerking zijn leeg. Anders mislukt de bewerking Hallo Hallo eerste consistentiecontrole op Hallo doel shard. Opmerking dat referentiegegevens alleen worden gekopieerd als Hallo verwijzingstabel leeg is en of er geen consistentiecontrole garandeert ook met inachtneming van tooother gelijktijdige schrijfbewerkingen op Hallo verwijzingstabellen. We raden u dit: wanneer gesplitste/merge-bewerkingen wordt uitgevoerd, geen schrijfbewerkingen wijzigingen aanbrengen toohello verwijzingsdimensies.
* Hallo-service is afhankelijk van de identiteit van de rij is ingesteld door een unieke index of de sleutel die Hallo sharding key tooimprove prestaties en betrouwbaarheid voor grote shardlets bevat. Dit maakt het mogelijk Hallo service toomove gegevens op een zelfs weer specifieker dan alleen Hallo sharding sleutelwaarde. Dit helpt tooreduce Hallo maximale hoeveelheid logboekruimte en vergrendelingen die vereist tijdens het Hallo-bewerking zijn. Houd rekening met een unieke index of een primaire sleutel, met inbegrip van Hallo sharding-sleutel op een bepaalde tabel als u wilt dat toouse die tabel maken met merge-gesplitste/move-aanvragen. Uit prestatieoverwegingen moet Hallo sharding sleutel Hallo toonaangevende kolom in Hallo sleutel of Hallo index.
* In de loop van de Hallo van verwerking van aanvragen, kan sommige gegevens shardlet aanwezig op Hallo bron en doel-shard Hallo zijn. Dit is nodig tooprotect tegen fouten tijdens het Hallo shardlet verkeer. Hallo integratie van split-samenvoegen met Hallo shard-toewijzing zorgt ervoor dat de verbindingen via Hallo gegevens afhankelijke routering API's met Hallo **OpenConnectionForKey** methode op Hallo shard-toewijzing een inconsistente tussenliggende statussen niet ziet. Echter, wanneer verbindende toohello bron- of Hallo gericht shards zonder Hallo **OpenConnectionForKey** methode inconsistente tussenliggende statussen mogelijk zichtbaar wanneer merge-gesplitste/move-aanvragen op gaat. Deze verbindingen gedeeltelijke of dubbele resultaten, afhankelijk van de timing van Hallo of Hallo shard onderliggende hello verbinding kunnen worden weergegeven. Deze beperking bevat momenteel Hallo-verbindingen gemaakt door de elastische Schaalfunctionaliteit van meerdere Shard-query.
* Hallo metagegevensdatabase voor Hallo gesplitste samenvoegen service moet niet worden gedeeld tussen verschillende rollen. Bijvoorbeeld, een functie Hallo gesplitste merge-service wordt uitgevoerd in faseringsdatabase behoeften toopoint tooa andere metagegevens dan Hallo productie-rol.

## <a name="billing"></a>Facturering
Hallo gesplitste merge-service wordt uitgevoerd als een cloudservice in uw Microsoft Azure-abonnement. Daarom toepassing kosten voor cloudservices tooyour exemplaar van Hallo-service. Tenzij u vaak split of merge/verplaatsen bewerkingen uitvoert, wordt u aangeraden verwijderen van uw cloudservice gesplitste samenvoegen. Die kosten voor het werken met opgeslagen of geïmplementeerd cloud service-exemplaren. U kunt opnieuw implementeren en uw gemakkelijk uitvoerbare configuratie starten wanneer u tooperform moet splitsen of samenvoegen van bewerkingen. 

## <a name="monitoring"></a>Bewaking
### <a name="status-tables"></a>Status tabellen
Hallo gesplitste samenvoegen Service biedt Hallo **RequestStatus** tabel in Hallo metagegevensdatabase archief voor de bewaking van voltooide en lopende aanvragen. Hallo tabel bevat een rij voor elke aanvraag gesplitste samenvoegen dat verzonden toothis exemplaar van Hallo gesplitste samenvoegen service is. Dit biedt de volgende informatie voor elke aanvraag Hallo:

* **Tijdstempel**: Hallo tijd en datum waarop het Hallo-aanvraag is gestart.
* **OperationId**: een GUID die een unieke identificatie van Hallo-aanvraag. Deze aanvraag kan ook worden voor gebruikte toocancel Hallo bewerking terwijl deze nog steeds uitgevoerd wordt.
* **Status**: huidige status van aanvraag Hallo Hallo. Voor actieve aanvragen, ook geeft het Hallo huidige fase in welke Hallo-aanvraag is.
* **CancelRequest**: een vlag die aangeeft of Hallo-aanvraag is geannuleerd.
* **Voortgang**: een percentage van de schatting van voor Hallo-bewerking is voltooid. Een waarde van 50 geeft aan dat het Hallo-bewerking ongeveer 50% voltooid is.
* **Details**: een XML-waarde die een gedetailleerdere voortgangsrapport biedt. Hallo voortgangsrapport wordt regelmatig bijgewerkt als sets van rijen uit de bron tootarget worden gekopieerd. In geval van fouten en uitzonderingen tevens in deze kolom meer gedetailleerde informatie over Hallo-fout.

### <a name="azure-diagnostics"></a>Azure Diagnostics
Hallo gesplitste samenvoegen service gebruikt Azure Diagnostics op basis van de Azure SDK 2.5 voor controle en diagnostische gegevens. Beheren van configuratie van diagnostische Hallo zoals hier wordt beschreven: [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](../cloud-services/cloud-services-dotnet-diagnostics.md). Hallo downloadpakket bevat twee configuraties voor diagnostische gegevens: één voor Hallo-Webrol en één voor Hallo-werkrol. Deze configuraties voor diagnostische gegevens voor Hallo service volgen richtlijnen Hallo van [Cloud Service grondbeginselen in Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Cloud-Service-Fundamentals-4ca72649). Dit omvat Hallo definities toolog prestatiemeteritems, IIS-logboeken, Windows-gebeurtenislogboeken en gebeurtenislogboeken van toepassingen gesplitste samenvoegen. 

## <a name="deploy-diagnostics"></a>Diagnostische gegevens implementeren
tooenable controle en diagnostische gegevens met Hallo diagnostische configuratie voor Hallo web- en werkrollen rollen geleverd door Hallo NuGet-pakket, Hallo volgende Azure PowerShell-opdrachten uitvoeren: 

    $storage_name = "<YourAzureStorageAccount>" 

    $key = "<YourAzureStorageAccountKey" 

    $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key  


    $config_path = "<YourFilePath>\SplitMergeWebContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWeb" 


    $config_path = "<YourFilePath>\SplitMergeWorkerContent.diagnostics.xml" 

    $service_name = "<YourCloudServiceName>" 

    Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Production -Role "SplitMergeWorker" 

U vindt meer informatie over het tooconfigure en implementeren van diagnostische instellingen hier: [diagnostische gegevens inschakelen in Azure Cloud Services en virtuele Machines](../cloud-services/cloud-services-dotnet-diagnostics.md). 

## <a name="retrieve-diagnostics"></a>Diagnostische gegevens ophalen
U kunt eenvoudig uw diagnostics openen vanaf Hallo Visual Studio Server Explorer in Azure, deel van de structuur van de Server Explorer Hallo Hallo. Open een exemplaar van de Visual Studio en op in de menubalk Hallo weergeven en Server Explorer. Klik op Hallo Azure pictogram tooconnect tooyour Azure-abonnement. Navigeer tooAzure -> opslag -> <your storage account> -> tabellen-WADLogsTable >. Zie voor meer informatie [opslagbronnen bladeren met Server Explorer](http://msdn.microsoft.com/library/azure/ff683677.aspx). 

![WADLogsTable][2]

Hallo WADLogsTable gemarkeerd in de bovenstaande afbeelding voor Hallo Hallo bevat gedetailleerde gebeurtenissen van het toepassingslogboek Hallo gesplitste samenvoegen van de service. Houd er rekening mee dat standaardconfiguratie Hallo Hallo gedownload pakket is gericht op een productie-implementatie. Hallo interval waarmee logboeken en prestatiemeteritems worden opgehaald uit het Hallo-service-exemplaren is daarom grote (5 minuten). Voor testen en ontwikkeling moet de lagere hello-interval door Hallo diagnostische instellingen van het Hallo-web- of Hallo worker-rol tooyour aan te passen. Met de rechtermuisknop op het Hallo-rol in Hallo Visual Studio Server Explorer (Zie hierboven) en vervolgens pas Hallo Transfer periode in het dialoogvenster Hallo voor Hallo Diagnostics configuratie-instellingen: 

![Configuratie][3]

## <a name="performance"></a>Prestaties
Betere prestaties is in het algemeen toobe verwacht van Hallo hoger, meer zodat Servicelagen in Azure SQL Database. Hogere i/o, CPU en geheugen toewijzingen voor hogere Servicelagen Hallo profiteren Hallo bulksgewijs kopiëren en verwijderen van bewerkingen die Hallo gesplitste merge-service wordt gebruikt. Beperkte daarom toename Hallo servicelaag slechts voor deze databases voor een gedefinieerde periode.

Hallo-service voert ook validatie van query's als onderdeel van de normale bewerkingen. Deze validatie van query's controleren op onverwachte aanwezigheid van gegevens in het doelbereik Hallo en zorg ervoor dat een merge-gesplitste/move-bewerking wordt gestart van een consistente status. Deze alle query's werken over sharding sleutelbereiken gedefinieerd door de scope Hallo Hallo-werking en Hallo batchgrootte geleverd als onderdeel van de definitie van Hallo aanvragen. Deze query's werken het beste als een index aanwezig is waarvan de Hallo sharding-sleutel heeft, zoals Hallo toonaangevende kolom. 

Bovendien kunt een eigenschap uniekheid met Hallo sharding sleutel als de toonaangevende kolom Hallo Hallo service toouse een geoptimaliseerde aanpak die brongebruik in termen van logboekruimte en het geheugen beperkt. Deze eigenschap uniekheid is vereist toomove grote hoeveelheden gegevens grootten (meestal meer dan 1GB). 

## <a name="how-tooupgrade"></a>Hoe tooupgrade
1. Volg de stappen Hallo in [implementeren van een service gesplitste samenvoegen](sql-database-elastic-scale-configure-deploy-split-and-merge.md).
2. Het configuratiebestand voor cloud-service voor uw nieuwe configuratieparameters voor gesplitste samenvoegen implementatie tooreflect Hallo wijzigen. Een nieuwe vereiste parameter is Hallo informatie over Hallo certificaat gebruikt voor versleuteling. Een eenvoudige manier toodo dit toocompare Hallo nieuw sjabloon configuratiebestand van Hallo downloaden op basis van uw bestaande configuratie is. Zorg ervoor dat u Hallo instellingen 'DataEncryptionPrimaryCertificateThumbprint' en 'DataEncryptionPrimary' voor Hallo web- en Hallo werkrol toevoegen.
3. Zorg ervoor dat alle lopende gesplitste merge-bewerkingen zijn voltooid voordat u implementeert Hallo update tooAzure. U kunt dit eenvoudig doen door het uitvoeren van query's Hallo RequestStatus en PendingWorkflows tabellen in Hallo gesplitste samenvoegen metagegevensdatabase voor actieve aanvragen.
4. Werk uw bestaande cloud service-implementatie voor split-samenvoegen in uw Azure-abonnement met het nieuwe pakket Hallo en uw bijgewerkte serviceconfiguratiebestand.

U hoeft niet tooprovision een nieuwe metagegevensdatabase voor tooupgrade gesplitste samenvoegen. Hallo nieuwe versie wordt automatisch bijwerken van uw bestaande metagegevens database toohello nieuwe versie. 

## <a name="best-practices--troubleshooting"></a>Aanbevolen procedures en probleemoplossing
* Definieer een testtenant en uw belangrijkste split of merge/verplaatsen bewerkingen met de testtenant Hallo uitoefenen over meerdere shards. Zorg ervoor dat alle metagegevens correct is gedefinieerd in de shard-toewijzing en dat Hallo bewerkingen niet-beperkingen of refererende sleutels schenden.
* Houd Hallo test tenant-gegevensgrootte hierboven Hallo maximale grootte van uw grootste tenant tooensure u gegevensgrootte niet Doe problemen met betrekking tot. Zo kunt u een bovengrens beoordelen op Hallo duurt toomove rond een één-tenant. 
* Zorg ervoor dat uw schema verwijderingen toestaat. Hallo gesplitste samenvoegen service vereist Hallo mogelijkheid tooremove gegevens van Hallo bron shard zodra het Hallo-gegevens zijn met succes gekopieerde toohello doel. Bijvoorbeeld: **triggers verwijderen** kunt voorkomen dat Hallo service verwijderen van gegevens op de bron Hallo Hallo en bewerkingen toofail kan veroorzaken.
* Hallo sharding-sleutel moet Hallo voorloop-kolom in uw primaire sleutel of unieke indexdefinitie. Die zorgt ervoor dat de beste prestaties Hallo voor Hallo splitsen of samenvoegen validatie van query's, en voor Hallo actuele gegevens verplaatsing en verwijdering bewerkingen waarvoor een sharding sleutelbereiken altijd niet bewerken.
* Plaatsen van uw service gesplitste samenvoegen in Hallo regio en Datacenter waar uw database zich bevinden. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
[1]:./media/sql-database-elastic-scale-overview-split-and-merge/split-merge-overview.png
[2]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics.png
[3]:./media/sql-database-elastic-scale-overview-split-and-merge/diagnostics-config.png


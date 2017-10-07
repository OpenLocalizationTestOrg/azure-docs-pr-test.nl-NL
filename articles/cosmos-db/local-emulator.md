---
title: aaaDevelop lokaal met hello Azure Cosmos DB Emulator | Microsoft Docs
description: Hello Azure Cosmos DB Emulator gebruikt, kunt u ontwikkelen en testen van de toepassing lokaal voor gratis, zonder te maken van een Azure-abonnement.
services: cosmos-db
documentationcenter: 
keywords: Azure Cosmos DB Emulator
author: arramac
manager: jhubbard
editor: 
ms.assetid: 90b379a6-426b-4915-9635-822f1a138656
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: arramac
ms.openlocfilehash: fb5449489e5f71664e72d8e11e583315be371bf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a>Hello Azure Cosmos DB Emulator gebruiken voor lokale ontwikkeling en testen

<table>
<tr>
  <td><strong>Binaire bestanden</strong></td>
  <td>[MSI downloaden](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><strong>Docker</strong></td>
  <td>[Docker-Hub](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><strong>Docker-bron</strong></td>
  <td>[GitHub](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
Hello Azure Cosmos DB Emulator biedt een lokale omgeving waarin hello Azure DB die Cosmos-service voor ontwikkelingsdoeleinden worden geëmuleerd. Hello Azure Cosmos DB Emulator gebruikt, kunt u ontwikkelen en testen van de toepassing lokaal zonder te maken van een Azure-abonnement of mogelijke kosten. Wanneer u tevreden bent over hoe uw toepassing in Azure Cosmos DB Emulator Hallo werkt, kunt u een Azure DB die Cosmos-account in Hallo cloud toousing overschakelen.

Dit artikel behandelt Hallo taken te volgen: 

> [!div class="checklist"]
> * Hallo Emulator installeren
> * Hallo Emulator uitgevoerd op Docker voor Windows
> * Verificatie van aanvragen
> * Met behulp van Hallo Data Explorer in Hallo Emulator
> * SSL-certificaten exporteren
> * Hallo Emulator aanroepen vanaf de opdrachtregel Hallo
> * Traceringsbestanden verzamelen

Het is raadzaam om aan de slag door bekijkt hello video te volgen waarbij Kirill Gavrylyuk ziet u hoe tooget Hello Azure Cosmos DB Emulator gestart. Hallo video toohello emulator verwezen als Hallo DocumentDB-Emulator, maar Hallo hulpprogramma zelf heeft gekregen hello Azure Cosmos DB Emulator sinds grondverf Hallo video. Alle informatie in Hallo video nog steeds correct voor hello Azure Cosmos DB-Emulator. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a>De werking van Hallo Emulator
Hello Azure Cosmos DB Emulator biedt een hoogwaardige emulatie van hello Azure DB die Cosmos-service. Het ondersteunt dezelfde functionaliteit als Azure Cosmos DB, inclusief ondersteuning voor het maken en uitvoeren van query's JSON-documenten, inrichting en schalen van verzamelingen en uitvoering van opgeslagen procedures en triggers. U kunt ontwikkelen en testen van toepassingen die gebruikmaken van hello Azure Cosmos DB Emulator en deze tooAzure op globale schaal implementeren door het maken van een configuratie voor één toohello verbindingseindpunt voor Azure Cosmos DB wijzigen.

Terwijl we een lokale emulatie van hoge kwaliteit van Hallo werkelijke Azure DB die Cosmos-service hebt gemaakt, is Hallo-implementatie van hello Azure Cosmos DB Emulator anders dan die van Hallo-service. Hello Azure Cosmos DB Emulator gebruikt bijvoorbeeld de standaard OS-componenten zoals Hallo lokaal bestandssysteem voor de persistentie en HTTPS-protocolstack voor connectiviteit. Dit betekent dat bepaalde functies die afhankelijk van de Azure-infrastructuur is zoals globale replicatie, één cijfer milliseconde latentie voor leest/schrijft en instelbare consistentieniveaus zijn niet beschikbaar via hello Azure Cosmos DB-Emulator.

> [!NOTE]
> Op dit moment Hallo Data Explorer in Hallo ondersteunt emulator alleen Hallo maken van verzamelingen voor DocumentDB-API en verzamelingen voor MongoDB. Hallo Data Explorer in Hallo-emulator biedt momenteel geen ondersteuning voor Hallo maken van tabellen en grafieken kunt maken. 

## <a name="system-requirements"></a>Systeemvereisten
Hello Azure Cosmos DB Emulator heeft Hallo hardware- en softwarevereisten te volgen:

* Softwarevereisten
  * Windows Server 2012 R2, WindowsServer 2016 of Windows 10
*   Minimale hardwarevereisten
  * 2 GB RAM-GEHEUGEN
  * 10 GB beschikbare schijfruimte

## <a name="installation"></a>Installeren
U kunt downloaden en installeren van hello Azure Cosmos DB Emulator van Hallo [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> tooinstall, configureren en uitvoeren van hello Azure Cosmos DB Emulator, moet u beheerdersrechten hebben op Hallo-computer.

## <a name="running-on-docker-for-windows"></a>Uitgevoerd op Docker voor Windows

Hello Azure Cosmos DB Emulator kan worden uitgevoerd op Docker voor Windows. Hallo Emulator werkt niet op Docker voor Oracle Linux.

Zodra u hebt [Docker voor Windows](https://www.docker.com/docker-windows) geïnstalleerd, kunt u Hallo Emulator afbeelding van Docker-Hub pull door het uitvoeren van de volgende opdracht uit uw favoriete shell hello (cmd.exe, PowerShell, enz.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
toostart hello afbeelding, Hallo volgende opdrachten uitvoeren.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

Hallo reactie lijkt vergelijkbaar toohello volgende:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import hello SSL certificate from an administrator command prompt on hello host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

Hallo interactieve shell sluiten zodra Hallo Emulator is gestart, wordt afgesloten Hallo Emulator container.

Hallo-eindpunt en de hoofdsleutel in uit Hallo antwoord gebruiken in uw client- en Hallo SSL-certificaat importeren in de host. tooimport hello SSL-certificaat Hallo vanaf een opdrachtprompt admin te volgen:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a>Hallo Emulator te starten

toostart hello Azure Cosmos DB-Emulator, selecteer de knop Start Hallo of druk op Hallo Windows-toets. Begint te typen **Azure Cosmos DB Emulator**, en selecteer Hallo-emulator in Hallo lijst met toepassingen. 

![Selecteer Hallo Start of drukt u op Hallo Windows-toets, begint te typen ** Azure Cosmos DB Emulator ** en selecteer Hallo-emulator in Hallo lijst met toepassingen](./media/local-emulator/database-local-emulator-start.png)

Wanneer het Hallo-emulator wordt uitgevoerd, ziet u een pictogram in systeemvak voor Windows hello. ![Azure DB Cosmos lokale emulator taakbalk melding](./media/local-emulator/database-local-emulator-taskbar.png)

Hello Azure Cosmos DB Emulator standaard op Hallo lokale computer ('localhost') luisteren op poort 8081 wordt uitgevoerd.

Hello Azure Cosmos DB Emulator is geïnstalleerd door standaard toohello `C:\Program Files\Azure Cosmos DB Emulator` directory. U kunt ook starten en stoppen van de emulator vanaf de opdrachtregel Hallo Hallo. Zie [opdrachtregelprogramma](#command-line) voor meer informatie.

## <a name="start-data-explorer"></a>Start de Data Explorer

Wanneer hello Azure DB die Cosmos-emulator wordt gestart, wordt deze automatisch hello Azure Cosmos DB Data Explorer geopend in uw browser. Hallo-adres wordt weergegeven als [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Als u sluit Hallo explorer en toore open wilt dat deze later kunt u Hallo-URL in uw browser openen of starten van hello Azure Cosmos DB Emulator in pictogram in systeemvak voor Windows hello, zoals hieronder wordt weergegeven.

![Azure DB Cosmos lokale emulator data explorer starten](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Controleren op updates
Data Explorer geeft aan of er een nieuwe update beschikbaar voor downloaden. 

> [!NOTE]
> Gegevens die zijn gemaakt in een versie van hello Azure Cosmos DB Emulator kan niet worden gegarandeerd toobe toegankelijk wanneer u een andere versie. Als u toopersist uw gegevens nodig voor de lange termijn hello, verdient het aanbeveling om op te slaan die gegevens in een Azure DB die Cosmos-account, in plaats van hello Azure Cosmos DB-Emulator. 

## <a name="authenticating-requests"></a>Verificatie van aanvragen
Net zoals met Azure Cosmos-database in de cloud hello, moet elke aanvraag die u hebt aangebracht tegen hello Azure Cosmos DB Emulator worden geverifieerd. Hello Azure Cosmos DB Emulator ondersteunt één vaste account en een bekende verificatiesleutel voor de verificatie van de hoofdsleutel. Dit account en de sleutel zijn alleen Hallo-referenties zijn toegestaan voor gebruik met hello Azure Cosmos DB-Emulator. Ze zijn:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> hoofdsleutel Hello wordt ondersteund door hello Azure Cosmos DB Emulator is bedoeld voor gebruik met Hallo-emulator. U kunt uw Azure DB die Cosmos-account voor productie en de sleutel niet gebruiken met hello Azure Cosmos DB-Emulator. 

> [!NOTE] 
> Als u Hallo emulator hebt gestart met de optie/Key hello, gebruikt u Hallo gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "

Bovendien, net zoals hello Azure DB die Cosmos-service, hello Azure Cosmos DB Emulator alleen beveiligde communicatie via SSL ondersteunt.

## <a name="running-hello-emulator-on-a-local-network"></a>Hallo-emulator uitgevoerd op een lokaal netwerk

U kunt Hallo emulator uitvoeren op een lokaal netwerk. tooenable netwerktoegang, geef Hallo /AllowNetworkAccess optie op Hallo [opdrachtregel](#command-line-syntax), die ook vereisen dat u / Key opgeeft = key_string of/KeyFile = bestandsnaam. U kunt /GenKeyFile = bestandsnaam toogenerate een bestand met een willekeurige sleutel tevoren betaalt.  Vervolgens kunt u die te/KeyFile doorgeven = bestandsnaam of/Key = contents_of_file.

toegang tot het netwerk van tooenable voor eerste gebruiker die tijd Hallo Hallo afsluiten Hallo-emulator moet en verwijder gegevensmap Hallo-emulator (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-hello-emulator"></a>Ontwikkelen met Hallo Emulator
Zodra u hebt Azure DB Cosmos-Emulator wordt uitgevoerd op uw bureaublad hello, kunt u elke ondersteunde [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) of Hallo [DB REST API van Azure Cosmos](/rest/api/documentdb/) toointeract Hello Emulator. Hello Azure Cosmos DB Emulator tevens een ingebouwde Data Explorer waarmee u verzamelingen voor Hallo DocumentDB en MongoDB APIs en weergave maken en bewerken van documenten zonder een code te schrijven.   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Als u [Azure Cosmos DB protocolondersteuning voor MongoDB](mongodb-introduction.md), gebruik de volgende verbindingsreeks Hallo:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

U kunt bestaande hulpprogramma's zoals [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB-Emulator. U kunt ook gegevens migreert tussen hello Azure Cosmos DB Emulator en hello Azure Cosmos DB service met behulp van Hallo [Azure Cosmos DB hulpprogramma voor gegevensmigratie](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Als u Hallo emulator hebt gestart met de optie/Key hello, gebruikt u Hallo gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "

Met behulp van Azure DB die Cosmos-emulator hello, standaard, kunt u verzamelingen met één partitie too25 of 1 gepartitioneerde verzameling. Zie voor meer informatie over het wijzigen van deze waarde [hello PartitionCount instellingswaarde](#set-partitioncount).

## <a name="export-hello-ssl-certificate"></a>Hallo SSL-certificaat exporteren

.NET-talen en runtime gebruik Hallo Windows-certificaatarchief toosecurely verbinding maken met lokale toohello Azure DB die Cosmos-emulator. Andere talen hebben hun eigen methode voor het beheren en gebruiken van certificaten. Java maakt gebruik van een eigen [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) dat gebruikmaakt van Python [socket wrappers](https://docs.python.org/2/library/ssl.html).

In de volgorde tooobtain moet een certificaat toouse met talen en runtimes die niet worden geïntegreerd in Windows-certificaatarchief Hallo u tooexport met behulp van de certificaatbeheerder Windows hello. U kunt starten door het uitvoeren van certlm.msc of volg Hallo Stapsgewijze instructies in [hello Azure Cosmos DB Emulator certificaten exporteren](./local-emulator-export-ssl-certificates.md). Zodra de certificaatbeheerder hello wordt uitgevoerd, Hallo open Hallo persoonlijke certificaten zoals hieronder wordt weergegeven en exporteren certificaat met Hallo beschrijvende naam 'DocumentDBEmulatorCertificate' als een BASE-64 X.509 (.cer)-bestand gecodeerde.

![Azure DB Cosmos lokale emulator SSL-certificaat](./media/local-emulator/database-local-emulator-ssl_certificate.png)

Hallo X.509-certificaat kan worden geïmporteerd in Hallo Java-certificaatarchief door Hallo-instructies in [toevoegen van een certificaat toohello Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Zodra het Hallo-certificaat wordt geïmporteerd in het certificaatarchief hello, zijn Java en de MongoDB-toepassingen kunnen tooconnect toohello Azure Cosmos DB Emulator.

Wanneer u verbinding maakt toohello emulator van Python en Node.js-SDK's, is SSL-verificatie uitgeschakeld.

## <a id="command-line"></a>Opdrachtregelprogramma
Vanaf de installatielocatie hello, kunt u Hallo opdrachtregelprogramma toostart gebruiken en Hallo emulator stoppen, opties configureren en andere bewerkingen uitvoeren.

### <a name="command-line-syntax"></a>De syntaxis van opdrachtregel

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

tooview hello lijst met opties, type `CosmosDB.Emulator.exe /?` achter de opdrachtprompt Hallo.

<table>
<tr>
  <td><strong>Optie</strong></td>
  <td><strong>Beschrijving</strong></td>
  <td><strong>Opdracht</strong></td>
  <td><strong>Argumenten</strong></td>
</tr>
<tr>
  <td>[Geen argumenten]</td>
  <td>Hello Azure Cosmos DB Emulator met standaardinstellingen wordt opgestart.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Geeft Hallo lijst met ondersteunde opdrachtregelargumenten.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>afsluiten</td>
  <td>Hello Azure Cosmos DB-Emulator wordt afgesloten.</td>
  <td>CosmosDB.Emulator.exe/Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>Gegevenspad</td>
  <td>Hallo pad aangeeft in welke toostore gegevensbestanden worden opgeslagen. Standaard is % LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath =&lt;gegevenspad&gt;</td>
  <td>&lt;gegevenspad&gt;: een toegankelijk pad</td>
</tr>
<tr>
  <td>Poort</td>
  <td>Hiermee geeft u de Hallo poort nummer toouse Hallo-emulator.  De standaardwaarde is 8081.</td>
  <td>CosmosDB.Emulator.exe/Port =&lt;poort&gt;</td>
  <td>&lt;poort&gt;: poortnummer</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Hiermee geeft u Hallo poort nummer toouse voor MongoDB-compatibiliteit API. De standaardwaarde is 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: poortnummer</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Hiermee geeft u Hallo poorten toouse voor rechtstreekse connectiviteit. Standaardwaarden zijn 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: door komma's gescheiden lijst met 4 poorten</td>
</tr>
<tr>
  <td>Sleutel</td>
  <td>De autorisatiesleutel voor Hallo-emulator. Sleutel moet Hallo base 64-codering van een 64-byte-vector.</td>
  <td>CosmosDB.Emulator.exe/key:&lt;sleutel&gt;</td>
  <td>&lt;sleutel&gt;: sleutel moet Hallo base 64-codering van een 64-byte-vector</td>
</tr>
<tr>
  <td>EnableRateLimiting</td>
  <td>Hiermee geeft u op deze aanvraag snelheidsbeperking gedrag is ingeschakeld.</td>
  <td>CosmosDB.Emulator.exe /EnableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>DisableRateLimiting</td>
  <td>Hiermee geeft u op deze aanvraag snelheidsbeperking gedrag is uitgeschakeld.</td>
  <td>CosmosDB.Emulator.exe /DisableRateLimiting</td>
  <td></td>
</tr>
<tr>
  <td>NoUI</td>
  <td>Niet weergeven Hallo emulator gebruikersinterface.</td>
  <td>/ Noui CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>NoExplorer</td>
  <td>Geen documentverkenner weergeven bij het opstarten.</td>
  <td>CosmosDB.Emulator.exe /NoExplorer</td>
  <td></td>
</tr>
<tr>
  <td>PartitionCount</td>
  <td>Hiermee geeft u Hallo maximumaantal gepartitioneerde verzamelingen. Zie [Hallo aantal verzamelingen wijzigen](#set-partitioncount) voor meer informatie.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount =&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt;: het maximale aantal toegestane verzamelingen met één partitie. Standaardwaarde is 25. Maximaal toegestane aantal is 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Hiermee geeft u Hallo standaardaantal partities voor een gepartitioneerde verzameling.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; standaardwaarde is 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Hiermee toegang tot toohello emulator via een netwerk. U moet ook doorgeven/Key =&lt;key_string&gt; of/KeyFile =&lt;bestandsnaam&gt; tooenable toegang tot het netwerk.</td>
  <td>CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;<br><br>of<br><br>CosmosDB.Emulator.exe /AllowNetworkAccess/KeyFile =&lt;bestandsnaam&gt;</td>
  <td></td>
</tr>
<tr>
  <td>NoFirewall</td>
  <td>Firewall-regels niet worden aangepast wanneer /AllowNetworkAccess wordt gebruikt.</td>
  <td>CosmosDB.Emulator.exe /NoFirewall</td>
  <td></td>
</tr>
<tr>
  <td>GenKeyFile</td>
  <td>Een nieuwe autorisatiesleutel genereren en opslaan van het opgegeven bestand toohello. Hallo gegenereerde sleutel kan worden gebruikt met Hallo/Key of/KeyFile opties.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;pad tookey bestand&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Consistentie</td>
  <td>Hallo standaardniveau consistentie voor Hallo account instellen.</td>
  <td>CosmosDB.Emulator.exe /Consistency =&lt;consistentie&gt;</td>
  <td>&lt;consistentie&gt;: waarde moet een van de volgende Hallo [consistentieniveaus](consistency-levels.md): sessie, sterke, Eventual of BoundedStaleness.  de standaardwaarde Hallo is sessie.</td>
</tr>
<tr>
  <td>?</td>
  <td>Hallo-bericht van help weergeven.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Verschillen tussen hello Azure Cosmos DB Emulator en Azure Cosmos-DB 
Omdat hello Azure Cosmos DB Emulator een geëmuleerde omgeving uitgevoerd op een lokale developer-werkstation biedt, zijn er enkele verschillen in functionaliteit tussen Hallo-emulator en een Cosmos-DB Azure-account in Hallo cloud:

* Hello Azure Cosmos DB Emulator ondersteunt slechts één vaste account en een bekende hoofdsleutel.  Toegangssleutel wordt opnieuw gegenereerd, is niet mogelijk in hello Azure Cosmos DB-Emulator.
* Hello Azure Cosmos DB Emulator is niet een schaalbare service en wordt geen ondersteuning voor een groot aantal verzamelingen.
* Hello Azure Cosmos DB Emulator komt niet simuleren verschillende [Azure Cosmos DB consistentieniveaus](consistency-levels.md).
* Hello Azure Cosmos DB Emulator komt niet simuleren [meerdere landen/regio replicatie](distribute-data-globally.md).
* Hello Azure Cosmos DB Emulator biedt geen ondersteuning voor Hallo service quotum onderdrukkingen die beschikbaar in hello Azure DB die Cosmos-service (bijvoorbeeld de maximale grootte document, verbeterde gepartitioneerde verzameling opslag zijn).
* Als uw exemplaar van hello Azure Cosmos DB Emulator mogelijk niet omhoog toodate met de meest recente wijzigingen Hallo met hello Azure DB die Cosmos-service, neemt u [Azure DB die Cosmos-Capaciteitsplanner](https://www.documentdb.com/capacityplanner) tooaccurately schatting productie doorvoer (RUs) de behoeften van uw toepassing.

## <a id="set-partitioncount"></a>Aantal verzamelingen Hallo wijzigen

Standaard kunt u verzamelingen met één partitie too25 of 1 gepartitioneerde verzameling op basis van hello Azure Cosmos DB-Emulator. Doordat Hallo **PartitionCount** waarde, kunt u verzamelingen met één partitie too250 of 10 gepartitioneerde verzamelingen of een combinatie van twee die niet meer dan 250 één Hallo partities (waar 1 gepartitioneerd verzameling = 25 één partitie verzameling).

Als u een verzameling toocreate probeert nadat de huidige partitie aantal Hallo is overschreden, Hallo emulator een ServiceUnavailable-uitzondering genereert met het volgende bericht Hallo.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

toochange hello aantal verzamelingen beschikbaar toohello Azure Cosmos DB Emulator Hallo te volgen:

1. Alle lokale Azure Cosmos DB Emulator gegevens verwijderen met de rechtermuisknop op Hallo **Azure Cosmos DB Emulator** pictogram in systeemvak Hallo en vervolgens te klikken **gegevens opnieuw instellen...** .
2. Alle gegevens van de emulator in deze map C:\Users\user_name\AppData\Local\CosmosDBEmulator verwijderen.
3. Sluit alle geopende exemplaren met de rechtermuisknop op Hallo **Azure Cosmos DB Emulator** -pictogram op het systeemvak Hallo en vervolgens te klikken op **afsluiten**. Het duurt een paar minuten voor alle exemplaren tooexit.
4. Installeer de meest recente versie Hallo Hallo [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).
5. Hallo-emulator Hello PartitionCount vlag starten door een waarde < = 250. Bijvoorbeeld: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Problemen oplossen

Gebruik Hallo toohelp oplossen van problemen die u tegenkomt met hello Azure Cosmos DB emulator tips te volgen:

- Als u een nieuwe versie van Hallo Emulator geïnstalleerd en worden er fouten optreden, zorg ervoor dat u uw gegevens herstellen. U kunt uw gegevens herstellen door met de rechtermuisknop op Hallo Azure Cosmos DB Emulator pictogram in systeemvak Hallo en vervolgens te klikken op de gegevens opnieuw instellen... Als Hallo fouten die niet wordt opgelost, kunt u deze kunt verwijderen en opnieuw installeren Hallo app. Zie [verwijderen van de lokale emulator Hallo](#uninstall) voor instructies.

- Als hello Azure Cosmos DB emulator vastloopt, dumpbestanden verzamelen uit de map c:\Users\user_name\AppData\Local\CrashDumps, deze comprimeren en koppelt u ze tooan e-mailbericht te[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Als u crashes ondervindt in CosmosDB.StartupEntryPoint.exe, voert u de volgende opdracht vanaf een opdrachtprompt admin Hallo:`lodctr /R` 

- Als u een verbindingsprobleem ondervindt [verzamelen traceringsbestanden](#trace-files), deze comprimeren en koppelt u ze tooan e-mailbericht te[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).

- Als u krijgt een **Service niet beschikbaar** bericht wordt weergegeven, hello emulator waarschijnlijk defect tooinitialize Hallo network-stack. Controleer toosee als er beveiligde Hallo Pulse-client of Juniper netwerken client is geïnstalleerd, zoals netwerk filterstuurprogramma Hallo probleem kunnen veroorzaken. Verwijderen van stuurprogramma's van derden netwerk filter doorgaans, wordt het Hallo-probleem opgelost.

### <a id="trace-files"></a>Traceringsbestanden verzamelen

toocollect foutopsporingsgegevens Hallo volgende opdrachten uit een administratieve opdrachtprompt worden uitgevoerd:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Controle Hallo system lade toomake ervoor Hallo programma is afgesloten, kan een minuut duren. U kunt ook klikken op **afsluiten** in de gebruikersinterface van hello Azure DB die Cosmos-emulator.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Hallo probleem reproduceren. Als u Data Explorer niet werkt, hoeft u alleen toowait voor Hallo browser tooopen voor een paar seconden toocatch Hallo-fout.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Navigeer te`%ProgramFiles%\Azure Cosmos DB Emulator` en Hallo docdbemulator_000001.etl bestand vinden.
7. Hallo etl-bestand samen met Reproductiestappen te verzenden[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) voor foutopsporing.

### <a id="uninstall"></a>Verwijder Hallo lokale Emulator

1. Sluit alle geopende exemplaren van Hallo lokale Emulator met de rechtermuisknop op Hallo Azure Cosmos DB Emulator pictogram in systeemvak hello, klikt op afsluiten. Het duurt een paar minuten voor alle exemplaren tooexit.
2. Typ in het zoekvak van Hallo Windows **Apps en functies** en klik op Hallo **Apps en -functies (systeeminstellingen)** resultaat.
3. Schuif te in de lijst met apps Hallo**Azure Cosmos DB Emulator**, selecteert u het, klik op **verwijderen**, bevestigen en klikt u op **verwijderen** opnieuw.
4. Hallo-app wordt verwijderd, gaat u tooC:\Users\<gebruiker > \AppData\Local\CosmosDBEmulator en delete Hallo-map. 

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u Hallo volgende gedaan:

> [!div class="checklist"]
> * Geïnstalleerd Hallo lokale Emulator
> * Rand Hallo Emulator op Docker voor Windows
> * Geverifieerde aanvragen
> * Hallo Data Explorer in Hallo Emulator gebruikt
> * Geëxporteerde SSL-certificaten
> * Hallo Emulator vanaf de opdrachtregel Hallo aangeroepen
> * Verzamelde traceringsbestanden

In deze zelfstudie hebt u geleerd hoe toouse Hallo lokale Emulator voor gratis lokale ontwikkeling. U kunt nu de volgende zelfstudie toohello gaan en meer informatie hoe tooexport Emulator SSL-certificaten. 

> [!div class="nextstepaction"]
> [Hello Azure Cosmos DB Emulator certificaten exporteren](local-emulator-export-ssl-certificates.md)

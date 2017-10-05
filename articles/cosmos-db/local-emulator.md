---
title: Lokaal ontwikkelen met de Azure Cosmos DB Emulator | Microsoft Docs
description: Met behulp van de Azure-Emulator Cosmos DB, kunt u ontwikkelen en testen van de toepassing lokaal voor gratis, zonder te maken van een Azure-abonnement.
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
ms.openlocfilehash: a0f6a845a345ebd4ef0a58abf4934ce400103109
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a>De Azure Cosmos DB Emulator gebruiken voor lokale ontwikkeling en testen

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
  
De Azure-Emulator Cosmos DB biedt een lokale omgeving waarin de service Azure Cosmos DB voor ontwikkelingsdoeleinden worden geëmuleerd. Met behulp van de Azure-Emulator Cosmos DB, kunt u ontwikkelen en testen van de toepassing lokaal zonder te maken van een Azure-abonnement of mogelijke kosten. Wanneer u tevreden bent over hoe uw toepassing in de Azure-Emulator Cosmos DB werkt, kunt u overschakelen naar het met een Azure DB die Cosmos-account in de cloud.

In dit artikel bevat informatie over de volgende taken: 

> [!div class="checklist"]
> * Installeren van de Emulator
> * De Emulator uitgevoerd op Docker voor Windows
> * Verificatie van aanvragen
> * Met behulp van de Data Explorer in de Emulator
> * SSL-certificaten exporteren
> * Het aanroepen van de Emulator vanaf de opdrachtregel
> * Traceringsbestanden verzamelen

Het is raadzaam om aan de slag door het bekijken van de volgende video, waarbij Kirill Gavrylyuk ziet u hoe u aan de slag met de Azure-Emulator Cosmos DB. Denk eraan dat de video verwijst naar de emulator als de DocumentDB-Emulator, maar het programma zelf is de Azure-Emulator Cosmos DB gewijzigd sinds de video grondverf. Alle informatie in de video is nog steeds correct zijn voor de Emulator Azure Cosmos DB. 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a>De werking van de Emulator
De Azure-Emulator Cosmos DB biedt een hoogwaardige emulatie van de service Azure Cosmos DB. Het ondersteunt dezelfde functionaliteit als Azure Cosmos DB, inclusief ondersteuning voor het maken en uitvoeren van query's JSON-documenten, inrichting en schalen van verzamelingen en uitvoering van opgeslagen procedures en triggers. U kunt ontwikkelen en testen van toepassingen met behulp van de Azure-Emulator Cosmos-database en deze implementeren in Azure op schaal globale door het maken van een configuratie voor één eindpunt van de verbinding voor Azure Cosmos DB wijzigen.

Terwijl we een lokale emulatie van hoge kwaliteit van de werkelijke Azure DB die Cosmos-service hebt gemaakt, is de implementatie van de Azure Cosmos DB-Emulator is anders dan die van de service. De Azure-Emulator Cosmos DB gebruikt bijvoorbeeld de standaard OS-componenten zoals het lokale bestandssysteem voor de persistentie en HTTPS-protocolstack voor connectiviteit. Dit betekent dat bepaalde functies die afhankelijk van de Azure-infrastructuur is zoals globale replicatie, één cijfer milliseconde latentie voor leest/schrijft en instelbare consistentieniveaus zijn niet beschikbaar via de Azure-Emulator Cosmos DB.

> [!NOTE]
> Op dit moment ondersteunt de Data Explorer in de emulator alleen het maken van verzamelingen voor DocumentDB-API en MongoDB-verzamelingen. De Data Explorer in de emulator biedt momenteel geen ondersteuning voor het maken van tabellen en grafieken kunt maken. 

## <a name="system-requirements"></a>Systeemvereisten
De Azure-Emulator Cosmos DB heeft de volgende hardware en software-vereisten:

* Softwarevereisten
  * Windows Server 2012 R2, WindowsServer 2016 of Windows 10
*   Minimale hardwarevereisten
  * 2 GB RAM-GEHEUGEN
  * 10 GB beschikbare schijfruimte

## <a name="installation"></a>Installeren
U kunt downloaden en installeren van de Azure Cosmos DB-Emulator van de [Microsoft Download Center](https://aka.ms/cosmosdb-emulator). 

> [!NOTE]
> Als u wilt installeren, configureren en uitvoeren van de Azure Cosmos DB-Emulator, moet u beheerdersbevoegdheden hebben op de computer.

## <a name="running-on-docker-for-windows"></a>Uitgevoerd op Docker voor Windows

De Azure-Emulator Cosmos DB kan worden uitgevoerd op Docker voor Windows. De Emulator werkt niet op Docker voor Oracle Linux.

Zodra u hebt [Docker voor Windows](https://www.docker.com/docker-windows) geïnstalleerd, kunt u de installatiekopie van de Emulator van Docker-Hub pull met de volgende opdracht in uw favoriete shell (cmd.exe, PowerShell, enz.).

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
Voer de volgende opdrachten voor het starten van de installatiekopie.

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

Het antwoord ziet er ongeveer als volgt uit:

```
Starting Emulator
Emulator Endpoint: https://172.20.229.193:8081/
Master Key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==
Exporting SSL Certificate
You can import the SSL certificate from an administrator command prompt on the host by running:
cd /d %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
--------------------------------------------------------------------------------------------------
Starting interactive shell
``` 

De interactieve shell sluiten nadat de Emulator is gestart wordt afgesloten container van de Emulator.

Het eindpunt en de hoofdsleutel in uit het antwoord in de client en het SSL-certificaat importeren in de host. Doe het volgende vanaf een opdrachtprompt admin voor het importeren van het SSL-certificaat:

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a>Start de Emulator

Start de Emulator Azure Cosmos DB, selecteer de knop Start of druk op de Windows-toets. Begint te typen **Azure Cosmos DB Emulator**, en selecteert u de emulator in de lijst met toepassingen. 

![Selecteer de knop Start of druk op de Windows-toets, begint te typen ** Azure Cosmos DB Emulator ** en selecteert u de emulator van de lijst met toepassingen](./media/local-emulator/database-local-emulator-start.png)

Wanneer de emulator wordt uitgevoerd, ziet u een pictogram in het Windows-systeemvak. ![Azure DB Cosmos lokale emulator taakbalk melding](./media/local-emulator/database-local-emulator-taskbar.png)

De Azure DB-Emulator standaard Cosmos wordt uitgevoerd op de lokale computer ('localhost'), luistert op poort 8081.

De Azure-Emulator Cosmos DB wordt standaard geïnstalleerd bij naar de `C:\Program Files\Azure Cosmos DB Emulator` directory. U kunt ook starten en stoppen van de emulator vanaf de opdrachtregel. Zie [opdrachtregelprogramma](#command-line) voor meer informatie.

## <a name="start-data-explorer"></a>Start de Data Explorer

Wanneer de emulator Azure Cosmos DB opent, wordt deze automatisch Azure Cosmos DB Data Explorer geopend in uw browser. Het adres wordt weergegeven als [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html). Als u de explorer sluiten en wilt het later opnieuw openen, kunt u de URL in uw browser te openen of starten van de Azure-Emulator Cosmos-database in het pictogram in systeemvak voor Windows, zoals hieronder wordt weergegeven.

![Azure DB Cosmos lokale emulator data explorer starten](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a>Controleren op updates
Data Explorer geeft aan of er een nieuwe update beschikbaar voor downloaden. 

> [!NOTE]
> Gegevens die zijn gemaakt in een versie van de Azure-Emulator Cosmos-database kan niet worden gegarandeerd toegankelijk zijn voor het gebruik van een andere versie. Als u nodig hebt om uw gegevens voor de lange termijn, verdient het aanbeveling om op te slaan die gegevens in een Azure DB die Cosmos-account, in plaats van de Azure-Emulator Cosmos DB. 

## <a name="authenticating-requests"></a>Verificatie van aanvragen
Net zoals met Azure Cosmos DB in de cloud, moet elke aanvraag die u op basis van de Azure-Emulator Cosmos DB maakt worden geverifieerd. De Azure-Emulator Cosmos DB ondersteunt één vaste account en een bekende verificatiesleutel voor de verificatie van de hoofdsleutel. Dit account en de sleutel zijn de enige referenties zijn toegestaan voor gebruik met de Azure Cosmos DB-Emulator. Ze zijn:

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> De hoofdsleutel ondersteund door de Azure Cosmos DB-Emulator is bedoeld voor gebruik met de emulator. U kunt uw Azure DB die Cosmos-account voor productie en de sleutel niet gebruiken met de Azure Cosmos DB-Emulator. 

> [!NOTE] 
> Als u de emulator hebt gestart met de optie/Key, gebruikt u de gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "

Bovendien, net als de service Azure Cosmos DB de Emulator Azure Cosmos-database ondersteunt alleen beveiligde communicatie via SSL.

## <a name="running-the-emulator-on-a-local-network"></a>De emulator uitgevoerd op een lokaal netwerk

U kunt de emulator uitvoeren op een lokaal netwerk. Geef de optie /AllowNetworkAccess op zodat de toegang tot het netwerk de [opdrachtregel](#command-line-syntax), die ook vereisen dat u / Key opgeeft = key_string of/KeyFile = bestandsnaam. U kunt /GenKeyFile = bestandsnaam voor het genereren van een bestand met een willekeurige sleutel tevoren betaalt.  Vervolgens u doorgeven kunt dat naar/KeyFile = bestandsnaam of/Key = contents_of_file.

Toegang tot het netwerk voor het eerst inschakelen wordt de gebruiker moet de emulator afsluiten en verwijderen van de emulator gegevensmap (C:\Users\user_name\AppData\Local\CosmosDBEmulator).

## <a name="developing-with-the-emulator"></a>Ontwikkelen met de Emulator
Zodra u de Azure Cosmos DB-Emulator uitgevoerd op uw bureaublad hebt, kunt u elke ondersteunde [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) of de [REST-API van Azure Cosmos DB](/rest/api/documentdb/) om te communiceren met de Emulator. De Azure-Emulator Cosmos DB tevens een ingebouwde Data Explorer waarmee u verzamelingen voor de DocumentDB en MongoDB APIs en weergave maken en bewerken van documenten zonder een code te schrijven.   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

Als u [Azure Cosmos DB protocolondersteuning voor MongoDB](mongodb-introduction.md), gebruik de volgende verbindingsreeks:

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

U kunt bestaande hulpprogramma's zoals [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) verbinding maken met de Azure-Emulator Cosmos DB. U kunt ook migreren van gegevens tussen de Azure-Emulator Cosmos DB en het gebruik van Azure DB die Cosmos service de [Azure Cosmos DB hulpprogramma voor gegevensmigratie](https://github.com/azure/azure-documentdb-datamigrationtool).

> [!NOTE] 
> Als u de emulator hebt gestart met de optie/Key, gebruikt u de gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "

Met behulp van de emulator Azure Cosmos DB standaard, kunt u maximaal 25 verzamelingen met één partitie of 1 gepartitioneerde verzameling. Zie voor meer informatie over het wijzigen van deze waarde [PartitionCount waarde](#set-partitioncount).

## <a name="export-the-ssl-certificate"></a>Het SSL-certificaat exporteren

.NET-talen en runtime gebruik van de Windows-certificaatarchief veilig verbinding te maken met de lokale Azure DB die Cosmos-emulator. Andere talen hebben hun eigen methode voor het beheren en gebruiken van certificaten. Java maakt gebruik van een eigen [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) dat gebruikmaakt van Python [socket wrappers](https://docs.python.org/2/library/ssl.html).

U wilt exporteren met behulp van de certificaatbeheerder Windows ter verkrijging van een certificaat wilt gebruiken met talen en runtimes die niet worden geïntegreerd in het certificaatarchief van Windows. U kunt starten door certlm.msc uitgevoerd of de stapsgewijze instructies in [exporteert u het certificaat Azure Cosmos DB Emulator](./local-emulator-export-ssl-certificates.md). Zodra de certificate manager wordt uitgevoerd, opent u de persoonlijke certificaten zoals hieronder wordt weergegeven en exporteer het certificaat met de beschrijvende naam 'DocumentDBEmulatorCertificate' als een BASE-64 X.509 (.cer)-bestand gecodeerde.

![Azure DB Cosmos lokale emulator SSL-certificaat](./media/local-emulator/database-local-emulator-ssl_certificate.png)

Het X.509-certificaat kan worden geïmporteerd in het certificaatarchief Java door de instructies in [een certificaat toevoegen aan de Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store). Zodra het certificaat wordt geïmporteerd in het certificaatarchief, Java en de MongoDB-toepassingen worden verbinding kunnen maken met de Azure-Emulator Cosmos DB.

Bij het verbinden met de emulator van Python en Node.js-SDK's, is SSL-verificatie uitgeschakeld.

## <a id="command-line"></a>Opdrachtregelprogramma
Vanaf de installatielocatie, kunt u de opdrachtregel om te starten en stoppen van de emulator, opties configureren en andere bewerkingen uitvoeren.

### <a name="command-line-syntax"></a>De syntaxis van opdrachtregel

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

Als u wilt weergeven in de lijst met opties, typt u `CosmosDB.Emulator.exe /?` bij de opdrachtprompt.

<table>
<tr>
  <td><strong>Optie</strong></td>
  <td><strong>Beschrijving</strong></td>
  <td><strong>Opdracht</strong></td>
  <td><strong>Argumenten</strong></td>
</tr>
<tr>
  <td>[Geen argumenten]</td>
  <td>De Azure-Emulator Cosmos DB met standaardinstellingen wordt opgestart.</td>
  <td>CosmosDB.Emulator.exe</td>
  <td></td>
</tr>
<tr>
  <td>[Help]</td>
  <td>Geeft de lijst met ondersteunde opdrachtregelargumenten.</td>
  <td>CosmosDB.Emulator.exe /?</td>
  <td></td>
</tr>
<tr>
  <td>afsluiten</td>
  <td>De Azure Cosmos DB-Emulator wordt afgesloten.</td>
  <td>CosmosDB.Emulator.exe/Shutdown</td>
  <td></td>
</tr>
<tr>
  <td>Gegevenspad</td>
  <td>Hiermee geeft u het pad waarin de gegevensbestanden worden opgeslagen. Standaard is % LocalAppdata%\CosmosDBEmulator.</td>
  <td>CosmosDB.Emulator.exe /DataPath =&lt;gegevenspad&gt;</td>
  <td>&lt;gegevenspad&gt;: een toegankelijk pad</td>
</tr>
<tr>
  <td>Poort</td>
  <td>Hiermee geeft u het poortnummer dat moet worden gebruikt voor de emulator.  De standaardwaarde is 8081.</td>
  <td>CosmosDB.Emulator.exe/Port =&lt;poort&gt;</td>
  <td>&lt;poort&gt;: poortnummer</td>
</tr>
<tr>
  <td>MongoPort</td>
  <td>Hiermee geeft u het poortnummer dat moet worden gebruikt voor compatibiliteit met MongoDB API. De standaardwaarde is 10255.</td>
  <td>CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</td>
  <td>&lt;mongoport&gt;: poortnummer</td>
</tr>
<tr>
  <td>DirectPorts</td>
  <td>Hiermee geeft u de poorten te gebruiken voor rechtstreekse connectiviteit. Standaardwaarden zijn 10251,10252,10253,10254.</td>
  <td>CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</td>
  <td>&lt;directports&gt;: door komma's gescheiden lijst met 4 poorten</td>
</tr>
<tr>
  <td>Sleutel</td>
  <td>De autorisatiesleutel voor de emulator. Sleutel moet de base 64-codering van een 64-byte-vector.</td>
  <td>CosmosDB.Emulator.exe/key:&lt;sleutel&gt;</td>
  <td>&lt;sleutel&gt;: sleutel moet de base 64-codering van een 64-byte-vector</td>
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
  <td>Worden de emulator gebruikersinterface niet weergegeven.</td>
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
  <td>Hiermee geeft u het maximum aantal gepartitioneerde verzamelingen. Zie [wijzigen van het aantal verzamelingen](#set-partitioncount) voor meer informatie.</td>
  <td>CosmosDB.Emulator.exe /PartitionCount =&lt;partitioncount&gt;</td>
  <td>&lt;partitioncount&gt;: het maximale aantal toegestane verzamelingen met één partitie. Standaardwaarde is 25. Maximaal toegestane aantal is 250.</td>
</tr>
<tr>
  <td>DefaultPartitionCount</td>
  <td>Hiermee geeft u het aantal partities voor een gepartitioneerde verzameling.</td>
  <td>CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</td>
  <td>&lt;defaultpartitioncount&gt; standaardwaarde is 25.</td>
</tr>
<tr>
  <td>AllowNetworkAccess</td>
  <td>Geeft toegang tot de emulator via een netwerk. U moet ook doorgeven/Key =&lt;key_string&gt; of/KeyFile =&lt;bestandsnaam&gt; waarmee toegang tot het netwerk.</td>
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
  <td>Een nieuwe autorisatiesleutel genereren en opslaan in het opgegeven bestand. De gegenereerde sleutel kan worden gebruikt met de opties/Key of/KeyFile.</td>
  <td>CosmosDB.Emulator.exe /GenKeyFile =&lt;pad naar het sleutelbestand&gt;</td>
  <td></td>
</tr>
<tr>
  <td>Consistentie</td>
  <td>Stel het standaardniveau voor consistentie voor het account.</td>
  <td>CosmosDB.Emulator.exe /Consistency =&lt;consistentie&gt;</td>
  <td>&lt;consistentie&gt;: waarde moet een van de volgende [consistentieniveaus](consistency-levels.md): sessie, sterke, Eventual of BoundedStaleness.  De standaardwaarde is de sessie.</td>
</tr>
<tr>
  <td>?</td>
  <td>De helpbericht weergeven.</td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a>Verschillen tussen de Azure Cosmos DB-Emulator en Azure Cosmos-DB 
Omdat de Azure-Emulator Cosmos DB een geëmuleerde omgeving uitgevoerd op een lokale developer-werkstation biedt, zijn er enkele verschillen in functionaliteit tussen de emulator en een Cosmos-DB Azure-account in de cloud:

* De Azure-Emulator Cosmos DB ondersteunt slechts één vaste account en een bekende hoofdsleutel.  Toegangssleutel wordt opnieuw gegenereerd, is niet mogelijk in de Azure-Emulator Cosmos DB.
* De Azure-Emulator Cosmos-database is niet een schaalbare service en wordt geen ondersteuning voor een groot aantal verzamelingen.
* De Azure-Emulator Cosmos DB komt niet simuleren verschillende [Azure Cosmos DB consistentieniveaus](consistency-levels.md).
* De Azure-Emulator Cosmos DB komt niet simuleren [meerdere landen/regio replicatie](distribute-data-globally.md).
* De Azure-Emulator Cosmos DB biedt geen ondersteuning voor de service quotum onderdrukkingen die beschikbaar in de Azure DB die Cosmos-service (bijvoorbeeld de maximale grootte document, verbeterde gepartitioneerde verzameling opslag zijn).
* Als uw exemplaar van de Azure Cosmos DB-Emulator zijn mogelijk niet bijgewerkt met de meest recente wijzigingen met de service Azure Cosmos DB, neemt u [Azure DB die Cosmos-Capaciteitsplanner](https://www.documentdb.com/capacityplanner) nauwkeurig te schatten productie doorvoer (RUs) behoeften van uw de toepassing.

## <a id="set-partitioncount"></a>Het aantal verzamelingen wijzigen

Standaard kunt u maximaal 25 verzamelingen met één partitie of 1 gepartitioneerde verzameling op basis van de Azure-Emulator Cosmos DB. Doordat de **PartitionCount** waarde, kunt u maximaal 250 verzamelingen met één partitie of 10 gepartitioneerde verzamelingen of een combinatie van de twee die niet meer dan 250 één partities (waar 1 verzameling gepartitioneerd = 25 één partitie verzameling).

Als u probeert een verzameling maken nadat het huidige aantal partities is overschreden, genereert de emulator een uitzondering ServiceUnavailable met het volgende bericht.

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

Als u het aantal beschikbare verzamelingen wilt de Emulator Azure Cosmos DB, het volgende doen:

1. Alle lokale Azure Cosmos DB Emulator gegevens verwijderen met de rechtermuisknop op de **Azure Cosmos DB Emulator** pictogram op de taakbalk en vervolgens klikken op **gegevens opnieuw instellen...** .
2. Alle gegevens van de emulator in deze map C:\Users\user_name\AppData\Local\CosmosDBEmulator verwijderen.
3. Sluit alle geopende exemplaren met de rechtermuisknop op de **Azure Cosmos DB Emulator** pictogram op de taakbalk en vervolgens klikken op **afsluiten**. Het duurt een paar minuten voor alle exemplaren om af te sluiten.
4. Installeer de nieuwste versie van de [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).
5. Start de emulator met de vlag PartitionCount door een waarde < = 250. Bijvoorbeeld: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.

## <a name="troubleshooting"></a>Problemen oplossen

Gebruik de volgende tips voor het oplossen van problemen die u met de Azure DB die Cosmos-emulator tegenkomt:

- Als u een nieuwe versie van de Emulator is geïnstalleerd en worden er fouten optreden, zorg ervoor dat u uw gegevens herstellen. U kunt uw gegevens herstellen door met de rechtermuisknop op het pictogram Azure Cosmos DB Emulator op de taakbalk en vervolgens te klikken op de gegevens opnieuw instellen... Als de fouten die niet wordt opgelost, kunt u deze kunt verwijderen en opnieuw installeren van de app. Zie [verwijderen van de lokale emulator](#uninstall) voor instructies.

- Als de Azure DB die Cosmos-emulator vastloopt, verzamelen van dumpbestanden vanuit de map c:\Users\user_name\AppData\Local\CrashDumps, deze comprimeren en deze koppelt aan een e-mail naar [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).

- Als u crashes ondervindt in CosmosDB.StartupEntryPoint.exe, kunt u de volgende opdracht uitvoeren vanaf een opdrachtprompt beheerder:`lodctr /R` 

- Als u een verbindingsprobleem ondervindt [verzamelen traceringsbestanden](#trace-files), deze comprimeren en deze koppelt aan een e-mail naar [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).

- Als u krijgt een **Service niet beschikbaar** bericht, de emulator mogelijk mislukken de netwerkstack initialiseren. Controleer of er de beveiligde client Pulse of Juniper netwerken client is geïnstalleerd, zoals netwerk filterstuurprogramma ertoe leiden het probleem dat kunnen. Verwijderen van stuurprogramma's van derden netwerk filter doorgaans wordt het probleem opgelost.

### <a id="trace-files"></a>Traceringsbestanden verzamelen

Voor het verzamelen van foutopsporingsgegevens, voert u de volgende opdrachten uit vanaf een administratieve opdrachtprompt:

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. `CosmosDB.Emulator.exe /shutdown`. Bekijk het systeemvak om te controleren of het programma is afgesloten, kan een minuut duren. U kunt ook klikken op **afsluiten** in de gebruikersinterface van Azure DB die Cosmos-emulator.
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. Reproduceer het probleem. Als u Data Explorer niet werkt, hoeft u alleen moet worden gewacht op de browser te openen voor een paar seconden de fout te achterhalen.
5. `CosmosDB.Emulator.exe /stoptraces`
6. Navigeer naar `%ProgramFiles%\Azure Cosmos DB Emulator` en het bestand docdbemulator_000001.etl niet vinden.
7. Het etl-bestand samen met reproduceren stappen om verzenden [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) voor foutopsporing.

### <a id="uninstall"></a>Verwijderen van de lokale Emulator

1. Sluit alle geopende exemplaren van de lokale Emulator door met de rechtermuisknop op het pictogram Azure Cosmos DB Emulator op de taakbalk en klikt u op afsluiten. Het duurt een paar minuten voor alle exemplaren om af te sluiten.
2. Typ in het zoekvak Windows **Apps en functies** en klik op de **Apps en -functies (systeeminstellingen)** resultaat.
3. Schuif in de lijst met apps naar **Azure Cosmos DB Emulator**, selecteert u het, klik op **verwijderen**, bevestigen en klikt u op **verwijderen** opnieuw.
4. Wanneer de app is verwijderd, gaat u naar C:\Users\<gebruiker > \AppData\Local\CosmosDBEmulator en verwijder de map. 

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende gedaan:

> [!div class="checklist"]
> * De lokale Emulator geïnstalleerd
> * Rand de Docker voor Windows-Emulator
> * Geverifieerde aanvragen
> * De Data Explorer gebruikt in de Emulator
> * Geëxporteerde SSL-certificaten
> * Naam van de Emulator vanaf de opdrachtregel
> * Verzamelde traceringsbestanden

In deze zelfstudie hebt u geleerd hoe u van de Emulator van de lokale voor gratis lokale ontwikkeling. U kunt nu doorgaan met de volgende zelfstudie en informatie over het exporteren van de Emulator SSL-certificaten. 

> [!div class="nextstepaction"]
> [De Azure Cosmos DB Emulator certificaten exporteren](local-emulator-export-ssl-certificates.md)

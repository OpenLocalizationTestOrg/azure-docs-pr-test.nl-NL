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
# <a name="use-hello-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="f79f7-104">Hello Azure Cosmos DB Emulator gebruiken voor lokale ontwikkeling en testen</span><span class="sxs-lookup"><span data-stu-id="f79f7-104">Use hello Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="f79f7-105"><strong>Binaire bestanden</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="f79f7-106">MSI downloaden</span><span class="sxs-lookup"><span data-stu-id="f79f7-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="f79f7-108">Docker-Hub</span><span class="sxs-lookup"><span data-stu-id="f79f7-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-109"><strong>Docker-bron</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="f79f7-110">GitHub</span><span class="sxs-lookup"><span data-stu-id="f79f7-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="f79f7-111">Hello Azure Cosmos DB Emulator biedt een lokale omgeving waarin hello Azure DB die Cosmos-service voor ontwikkelingsdoeleinden worden geëmuleerd.</span><span class="sxs-lookup"><span data-stu-id="f79f7-111">hello Azure Cosmos DB Emulator provides a local environment that emulates hello Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="f79f7-112">Hello Azure Cosmos DB Emulator gebruikt, kunt u ontwikkelen en testen van de toepassing lokaal zonder te maken van een Azure-abonnement of mogelijke kosten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-112">Using hello Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="f79f7-113">Wanneer u tevreden bent over hoe uw toepassing in Azure Cosmos DB Emulator Hallo werkt, kunt u een Azure DB die Cosmos-account in Hallo cloud toousing overschakelen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-113">When you're satisfied with how your application is working in hello Azure Cosmos DB Emulator, you can switch toousing an Azure Cosmos DB account in hello cloud.</span></span>

<span data-ttu-id="f79f7-114">Dit artikel behandelt Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="f79f7-114">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="f79f7-115">Hallo Emulator installeren</span><span class="sxs-lookup"><span data-stu-id="f79f7-115">Installing hello Emulator</span></span>
> * <span data-ttu-id="f79f7-116">Hallo Emulator uitgevoerd op Docker voor Windows</span><span class="sxs-lookup"><span data-stu-id="f79f7-116">Running hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="f79f7-117">Verificatie van aanvragen</span><span class="sxs-lookup"><span data-stu-id="f79f7-117">Authenticating requests</span></span>
> * <span data-ttu-id="f79f7-118">Met behulp van Hallo Data Explorer in Hallo Emulator</span><span class="sxs-lookup"><span data-stu-id="f79f7-118">Using hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="f79f7-119">SSL-certificaten exporteren</span><span class="sxs-lookup"><span data-stu-id="f79f7-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="f79f7-120">Hallo Emulator aanroepen vanaf de opdrachtregel Hallo</span><span class="sxs-lookup"><span data-stu-id="f79f7-120">Calling hello Emulator from hello command line</span></span>
> * <span data-ttu-id="f79f7-121">Traceringsbestanden verzamelen</span><span class="sxs-lookup"><span data-stu-id="f79f7-121">Collecting trace files</span></span>

<span data-ttu-id="f79f7-122">Het is raadzaam om aan de slag door bekijkt hello video te volgen waarbij Kirill Gavrylyuk ziet u hoe tooget Hello Azure Cosmos DB Emulator gestart.</span><span class="sxs-lookup"><span data-stu-id="f79f7-122">We recommend getting started by watching hello following video, where Kirill Gavrylyuk shows how tooget started with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="f79f7-123">Hallo video toohello emulator verwezen als Hallo DocumentDB-Emulator, maar Hallo hulpprogramma zelf heeft gekregen hello Azure Cosmos DB Emulator sinds grondverf Hallo video.</span><span class="sxs-lookup"><span data-stu-id="f79f7-123">Note that hello video refers toohello emulator as hello DocumentDB Emulator, but hello tool itself has been renamed hello Azure Cosmos DB Emulator since taping hello video.</span></span> <span data-ttu-id="f79f7-124">Alle informatie in Hallo video nog steeds correct voor hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-124">All information in hello video is still accurate for hello Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-hello-emulator-works"></a><span data-ttu-id="f79f7-125">De werking van Hallo Emulator</span><span class="sxs-lookup"><span data-stu-id="f79f7-125">How hello Emulator works</span></span>
<span data-ttu-id="f79f7-126">Hello Azure Cosmos DB Emulator biedt een hoogwaardige emulatie van hello Azure DB die Cosmos-service.</span><span class="sxs-lookup"><span data-stu-id="f79f7-126">hello Azure Cosmos DB Emulator provides a high-fidelity emulation of hello Azure Cosmos DB service.</span></span> <span data-ttu-id="f79f7-127">Het ondersteunt dezelfde functionaliteit als Azure Cosmos DB, inclusief ondersteuning voor het maken en uitvoeren van query's JSON-documenten, inrichting en schalen van verzamelingen en uitvoering van opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="f79f7-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="f79f7-128">U kunt ontwikkelen en testen van toepassingen die gebruikmaken van hello Azure Cosmos DB Emulator en deze tooAzure op globale schaal implementeren door het maken van een configuratie voor één toohello verbindingseindpunt voor Azure Cosmos DB wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-128">You can develop and test applications using hello Azure Cosmos DB Emulator, and deploy them tooAzure at global scale by just making a single configuration change toohello connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="f79f7-129">Terwijl we een lokale emulatie van hoge kwaliteit van Hallo werkelijke Azure DB die Cosmos-service hebt gemaakt, is Hallo-implementatie van hello Azure Cosmos DB Emulator anders dan die van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="f79f7-129">While we created a high-fidelity local emulation of hello actual Azure Cosmos DB service, hello implementation of hello Azure Cosmos DB Emulator is different than that of hello service.</span></span> <span data-ttu-id="f79f7-130">Hello Azure Cosmos DB Emulator gebruikt bijvoorbeeld de standaard OS-componenten zoals Hallo lokaal bestandssysteem voor de persistentie en HTTPS-protocolstack voor connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="f79f7-130">For example, hello Azure Cosmos DB Emulator uses standard OS components such as hello local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="f79f7-131">Dit betekent dat bepaalde functies die afhankelijk van de Azure-infrastructuur is zoals globale replicatie, één cijfer milliseconde latentie voor leest/schrijft en instelbare consistentieniveaus zijn niet beschikbaar via hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via hello Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="f79f7-132">Op dit moment Hallo Data Explorer in Hallo ondersteunt emulator alleen Hallo maken van verzamelingen voor DocumentDB-API en verzamelingen voor MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f79f7-132">At this time hello Data Explorer in hello emulator only supports hello creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="f79f7-133">Hallo Data Explorer in Hallo-emulator biedt momenteel geen ondersteuning voor Hallo maken van tabellen en grafieken kunt maken.</span><span class="sxs-lookup"><span data-stu-id="f79f7-133">hello Data Explorer in hello emulator does not currently support hello creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="f79f7-134">Systeemvereisten</span><span class="sxs-lookup"><span data-stu-id="f79f7-134">System requirements</span></span>
<span data-ttu-id="f79f7-135">Hello Azure Cosmos DB Emulator heeft Hallo hardware- en softwarevereisten te volgen:</span><span class="sxs-lookup"><span data-stu-id="f79f7-135">hello Azure Cosmos DB Emulator has hello following hardware and software requirements:</span></span>

* <span data-ttu-id="f79f7-136">Softwarevereisten</span><span class="sxs-lookup"><span data-stu-id="f79f7-136">Software requirements</span></span>
  * <span data-ttu-id="f79f7-137">Windows Server 2012 R2, WindowsServer 2016 of Windows 10</span><span class="sxs-lookup"><span data-stu-id="f79f7-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="f79f7-138">Minimale hardwarevereisten</span><span class="sxs-lookup"><span data-stu-id="f79f7-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="f79f7-139">2 GB RAM-GEHEUGEN</span><span class="sxs-lookup"><span data-stu-id="f79f7-139">2 GB RAM</span></span>
  * <span data-ttu-id="f79f7-140">10 GB beschikbare schijfruimte</span><span class="sxs-lookup"><span data-stu-id="f79f7-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="f79f7-141">Installeren</span><span class="sxs-lookup"><span data-stu-id="f79f7-141">Installation</span></span>
<span data-ttu-id="f79f7-142">U kunt downloaden en installeren van hello Azure Cosmos DB Emulator van Hallo [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="f79f7-142">You can download and install hello Azure Cosmos DB Emulator from hello [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="f79f7-143">tooinstall, configureren en uitvoeren van hello Azure Cosmos DB Emulator, moet u beheerdersrechten hebben op Hallo-computer.</span><span class="sxs-lookup"><span data-stu-id="f79f7-143">tooinstall, configure, and run hello Azure Cosmos DB Emulator, you must have administrative privileges on hello computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="f79f7-144">Uitgevoerd op Docker voor Windows</span><span class="sxs-lookup"><span data-stu-id="f79f7-144">Running on Docker for Windows</span></span>

<span data-ttu-id="f79f7-145">Hello Azure Cosmos DB Emulator kan worden uitgevoerd op Docker voor Windows.</span><span class="sxs-lookup"><span data-stu-id="f79f7-145">hello Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="f79f7-146">Hallo Emulator werkt niet op Docker voor Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="f79f7-146">hello Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="f79f7-147">Zodra u hebt [Docker voor Windows](https://www.docker.com/docker-windows) geïnstalleerd, kunt u Hallo Emulator afbeelding van Docker-Hub pull door het uitvoeren van de volgende opdracht uit uw favoriete shell hello (cmd.exe, PowerShell, enz.).</span><span class="sxs-lookup"><span data-stu-id="f79f7-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull hello Emulator image from Docker Hub by running hello following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="f79f7-148">toostart hello afbeelding, Hallo volgende opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f79f7-148">toostart hello image, run hello following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="f79f7-149">Hallo reactie lijkt vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="f79f7-149">hello response looks similar toohello following:</span></span>

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

<span data-ttu-id="f79f7-150">Hallo interactieve shell sluiten zodra Hallo Emulator is gestart, wordt afgesloten Hallo Emulator container.</span><span class="sxs-lookup"><span data-stu-id="f79f7-150">Closing hello interactive shell once hello Emulator has been started will shutdown hello Emulator’s container.</span></span>

<span data-ttu-id="f79f7-151">Hallo-eindpunt en de hoofdsleutel in uit Hallo antwoord gebruiken in uw client- en Hallo SSL-certificaat importeren in de host.</span><span class="sxs-lookup"><span data-stu-id="f79f7-151">Use hello endpoint and master key in from hello response in your client and import hello SSL certificate into your host.</span></span> <span data-ttu-id="f79f7-152">tooimport hello SSL-certificaat Hallo vanaf een opdrachtprompt admin te volgen:</span><span class="sxs-lookup"><span data-stu-id="f79f7-152">tooimport hello SSL certificate, do hello following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-hello-emulator"></a><span data-ttu-id="f79f7-153">Hallo Emulator te starten</span><span class="sxs-lookup"><span data-stu-id="f79f7-153">Start hello Emulator</span></span>

<span data-ttu-id="f79f7-154">toostart hello Azure Cosmos DB-Emulator, selecteer de knop Start Hallo of druk op Hallo Windows-toets.</span><span class="sxs-lookup"><span data-stu-id="f79f7-154">toostart hello Azure Cosmos DB Emulator, select hello Start button or press hello Windows key.</span></span> <span data-ttu-id="f79f7-155">Begint te typen **Azure Cosmos DB Emulator**, en selecteer Hallo-emulator in Hallo lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-155">Begin typing **Azure Cosmos DB Emulator**, and select hello emulator from hello list of applications.</span></span> 

![Selecteer Hallo Start of drukt u op Hallo Windows-toets, begint te typen ** Azure Cosmos DB Emulator ** en selecteer Hallo-emulator in Hallo lijst met toepassingen](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="f79f7-157">Wanneer het Hallo-emulator wordt uitgevoerd, ziet u een pictogram in systeemvak voor Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f79f7-157">When hello emulator is running, you'll see an icon in hello Windows taskbar notification area.</span></span> ![Azure DB Cosmos lokale emulator taakbalk melding](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="f79f7-159">Hello Azure Cosmos DB Emulator standaard op Hallo lokale computer ('localhost') luisteren op poort 8081 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f79f7-159">hello Azure Cosmos DB Emulator by default runs on hello local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="f79f7-160">Hello Azure Cosmos DB Emulator is geïnstalleerd door standaard toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span><span class="sxs-lookup"><span data-stu-id="f79f7-160">hello Azure Cosmos DB Emulator is installed by default toohello `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="f79f7-161">U kunt ook starten en stoppen van de emulator vanaf de opdrachtregel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f79f7-161">You can also start and stop hello emulator from hello command-line.</span></span> <span data-ttu-id="f79f7-162">Zie [opdrachtregelprogramma](#command-line) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f79f7-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="f79f7-163">Start de Data Explorer</span><span class="sxs-lookup"><span data-stu-id="f79f7-163">Start Data Explorer</span></span>

<span data-ttu-id="f79f7-164">Wanneer hello Azure DB die Cosmos-emulator wordt gestart, wordt deze automatisch hello Azure Cosmos DB Data Explorer geopend in uw browser.</span><span class="sxs-lookup"><span data-stu-id="f79f7-164">When hello Azure Cosmos DB emulator launches it will automatically open hello Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="f79f7-165">Hallo-adres wordt weergegeven als [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="f79f7-165">hello address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="f79f7-166">Als u sluit Hallo explorer en toore open wilt dat deze later kunt u Hallo-URL in uw browser openen of starten van hello Azure Cosmos DB Emulator in pictogram in systeemvak voor Windows hello, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f79f7-166">If you close hello explorer and would like toore-open it later, you can either open hello URL in your browser or launch it from hello Azure Cosmos DB Emulator in hello Windows Tray Icon as shown below.</span></span>

![Azure DB Cosmos lokale emulator data explorer starten](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="f79f7-168">Controleren op updates</span><span class="sxs-lookup"><span data-stu-id="f79f7-168">Checking for updates</span></span>
<span data-ttu-id="f79f7-169">Data Explorer geeft aan of er een nieuwe update beschikbaar voor downloaden.</span><span class="sxs-lookup"><span data-stu-id="f79f7-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="f79f7-170">Gegevens die zijn gemaakt in een versie van hello Azure Cosmos DB Emulator kan niet worden gegarandeerd toobe toegankelijk wanneer u een andere versie.</span><span class="sxs-lookup"><span data-stu-id="f79f7-170">Data created in one version of hello Azure Cosmos DB Emulator is not guaranteed toobe accessible when using a different version.</span></span> <span data-ttu-id="f79f7-171">Als u toopersist uw gegevens nodig voor de lange termijn hello, verdient het aanbeveling om op te slaan die gegevens in een Azure DB die Cosmos-account, in plaats van hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-171">If you need toopersist your data for hello long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in hello Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="f79f7-172">Verificatie van aanvragen</span><span class="sxs-lookup"><span data-stu-id="f79f7-172">Authenticating requests</span></span>
<span data-ttu-id="f79f7-173">Net zoals met Azure Cosmos-database in de cloud hello, moet elke aanvraag die u hebt aangebracht tegen hello Azure Cosmos DB Emulator worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="f79f7-173">Just as with Azure Cosmos DB in hello cloud, every request that you make against hello Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="f79f7-174">Hello Azure Cosmos DB Emulator ondersteunt één vaste account en een bekende verificatiesleutel voor de verificatie van de hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="f79f7-174">hello Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="f79f7-175">Dit account en de sleutel zijn alleen Hallo-referenties zijn toegestaan voor gebruik met hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-175">This account and key are hello only credentials permitted for use with hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="f79f7-176">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="f79f7-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="f79f7-177">hoofdsleutel Hello wordt ondersteund door hello Azure Cosmos DB Emulator is bedoeld voor gebruik met Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-177">hello master key supported by hello Azure Cosmos DB Emulator is intended for use only with hello emulator.</span></span> <span data-ttu-id="f79f7-178">U kunt uw Azure DB die Cosmos-account voor productie en de sleutel niet gebruiken met hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-178">You cannot use your production Azure Cosmos DB account and key with hello Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="f79f7-179">Als u Hallo emulator hebt gestart met de optie/Key hello, gebruikt u Hallo gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "</span><span class="sxs-lookup"><span data-stu-id="f79f7-179">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="f79f7-180">Bovendien, net zoals hello Azure DB die Cosmos-service, hello Azure Cosmos DB Emulator alleen beveiligde communicatie via SSL ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="f79f7-180">Additionally, just as hello Azure Cosmos DB service, hello Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-hello-emulator-on-a-local-network"></a><span data-ttu-id="f79f7-181">Hallo-emulator uitgevoerd op een lokaal netwerk</span><span class="sxs-lookup"><span data-stu-id="f79f7-181">Running hello emulator on a local network</span></span>

<span data-ttu-id="f79f7-182">U kunt Hallo emulator uitvoeren op een lokaal netwerk.</span><span class="sxs-lookup"><span data-stu-id="f79f7-182">You can run hello emulator on a local network.</span></span> <span data-ttu-id="f79f7-183">tooenable netwerktoegang, geef Hallo /AllowNetworkAccess optie op Hallo [opdrachtregel](#command-line-syntax), die ook vereisen dat u / Key opgeeft = key_string of/KeyFile = bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="f79f7-183">tooenable network access, specify hello /AllowNetworkAccess option at hello [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="f79f7-184">U kunt /GenKeyFile = bestandsnaam toogenerate een bestand met een willekeurige sleutel tevoren betaalt.</span><span class="sxs-lookup"><span data-stu-id="f79f7-184">You can use /GenKeyFile=file_name toogenerate a file with a random key upfront.</span></span>  <span data-ttu-id="f79f7-185">Vervolgens kunt u die te/KeyFile doorgeven = bestandsnaam of/Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="f79f7-185">Then you can pass that too/KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="f79f7-186">toegang tot het netwerk van tooenable voor eerste gebruiker die tijd Hallo Hallo afsluiten Hallo-emulator moet en verwijder gegevensmap Hallo-emulator (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="f79f7-186">tooenable network access for hello first time hello user should shutdown hello emulator and delete hello emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-hello-emulator"></a><span data-ttu-id="f79f7-187">Ontwikkelen met Hallo Emulator</span><span class="sxs-lookup"><span data-stu-id="f79f7-187">Developing with hello Emulator</span></span>
<span data-ttu-id="f79f7-188">Zodra u hebt Azure DB Cosmos-Emulator wordt uitgevoerd op uw bureaublad hello, kunt u elke ondersteunde [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) of Hallo [DB REST API van Azure Cosmos](/rest/api/documentdb/) toointeract Hello Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-188">Once you have hello Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or hello [Azure Cosmos DB REST API](/rest/api/documentdb/) toointeract with hello Emulator.</span></span> <span data-ttu-id="f79f7-189">Hello Azure Cosmos DB Emulator tevens een ingebouwde Data Explorer waarmee u verzamelingen voor Hallo DocumentDB en MongoDB APIs en weergave maken en bewerken van documenten zonder een code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="f79f7-189">hello Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for hello DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect toohello Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="f79f7-190">Als u [Azure Cosmos DB protocolondersteuning voor MongoDB](mongodb-introduction.md), gebruik de volgende verbindingsreeks Hallo:</span><span class="sxs-lookup"><span data-stu-id="f79f7-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use hello following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="f79f7-191">U kunt bestaande hulpprogramma's zoals [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) tooconnect toohello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="f79f7-192">U kunt ook gegevens migreert tussen hello Azure Cosmos DB Emulator en hello Azure Cosmos DB service met behulp van Hallo [Azure Cosmos DB hulpprogramma voor gegevensmigratie](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="f79f7-192">You can also migrate data between hello Azure Cosmos DB Emulator and hello Azure Cosmos DB service using hello [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="f79f7-193">Als u Hallo emulator hebt gestart met de optie/Key hello, gebruikt u Hallo gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "</span><span class="sxs-lookup"><span data-stu-id="f79f7-193">If you have started hello emulator with hello /Key option, then use hello generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="f79f7-194">Met behulp van Azure DB die Cosmos-emulator hello, standaard, kunt u verzamelingen met één partitie too25 of 1 gepartitioneerde verzameling.</span><span class="sxs-lookup"><span data-stu-id="f79f7-194">Using hello Azure Cosmos DB emulator, by default, you can create up too25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="f79f7-195">Zie voor meer informatie over het wijzigen van deze waarde [hello PartitionCount instellingswaarde](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="f79f7-195">For more information about changing this value, see [Setting hello PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-hello-ssl-certificate"></a><span data-ttu-id="f79f7-196">Hallo SSL-certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="f79f7-196">Export hello SSL certificate</span></span>

<span data-ttu-id="f79f7-197">.NET-talen en runtime gebruik Hallo Windows-certificaatarchief toosecurely verbinding maken met lokale toohello Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-197">.NET languages and runtime use hello Windows Certificate Store toosecurely connect toohello Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="f79f7-198">Andere talen hebben hun eigen methode voor het beheren en gebruiken van certificaten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="f79f7-199">Java maakt gebruik van een eigen [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) dat gebruikmaakt van Python [socket wrappers](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="f79f7-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="f79f7-200">In de volgorde tooobtain moet een certificaat toouse met talen en runtimes die niet worden geïntegreerd in Windows-certificaatarchief Hallo u tooexport met behulp van de certificaatbeheerder Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f79f7-200">In order tooobtain a certificate toouse with languages and runtimes that do not integrate with hello Windows Certificate Store you will need tooexport it using hello Windows Certificate Manager.</span></span> <span data-ttu-id="f79f7-201">U kunt starten door het uitvoeren van certlm.msc of volg Hallo Stapsgewijze instructies in [hello Azure Cosmos DB Emulator certificaten exporteren](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="f79f7-201">You can start it by running certlm.msc or follow hello step by step instructions in [Export hello Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="f79f7-202">Zodra de certificaatbeheerder hello wordt uitgevoerd, Hallo open Hallo persoonlijke certificaten zoals hieronder wordt weergegeven en exporteren certificaat met Hallo beschrijvende naam 'DocumentDBEmulatorCertificate' als een BASE-64 X.509 (.cer)-bestand gecodeerde.</span><span class="sxs-lookup"><span data-stu-id="f79f7-202">Once hello certificate manager is running, open hello Personal Certificates as shown below and export hello certificate with hello friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure DB Cosmos lokale emulator SSL-certificaat](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="f79f7-204">Hallo X.509-certificaat kan worden geïmporteerd in Hallo Java-certificaatarchief door Hallo-instructies in [toevoegen van een certificaat toohello Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="f79f7-204">hello X.509 certificate can be imported into hello Java certificate store by following hello instructions in [Adding a Certificate toohello Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="f79f7-205">Zodra het Hallo-certificaat wordt geïmporteerd in het certificaatarchief hello, zijn Java en de MongoDB-toepassingen kunnen tooconnect toohello Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-205">Once hello certificate is imported into hello certificate store, Java and MongoDB applications will be able tooconnect toohello Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="f79f7-206">Wanneer u verbinding maakt toohello emulator van Python en Node.js-SDK's, is SSL-verificatie uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f79f7-206">When connecting toohello emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="f79f7-207"><a id="command-line"></a>Opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="f79f7-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="f79f7-208">Vanaf de installatielocatie hello, kunt u Hallo opdrachtregelprogramma toostart gebruiken en Hallo emulator stoppen, opties configureren en andere bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f79f7-208">From hello installation location, you can use hello command-line toostart and stop hello emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="f79f7-209">De syntaxis van opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="f79f7-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="f79f7-210">tooview hello lijst met opties, type `CosmosDB.Emulator.exe /?` achter de opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="f79f7-210">tooview hello list of options, type `CosmosDB.Emulator.exe /?` at hello command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="f79f7-211"><strong>Optie</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="f79f7-212"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="f79f7-213"><strong>Opdracht</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="f79f7-214"><strong>Argumenten</strong></span><span class="sxs-lookup"><span data-stu-id="f79f7-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-215">[Geen argumenten]</span><span class="sxs-lookup"><span data-stu-id="f79f7-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="f79f7-216">Hello Azure Cosmos DB Emulator met standaardinstellingen wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="f79f7-216">Starts up hello Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="f79f7-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="f79f7-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="f79f7-218">[Help]</span></span></td>
  <td><span data-ttu-id="f79f7-219">Geeft Hallo lijst met ondersteunde opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-219">Displays hello list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="f79f7-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="f79f7-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-221">afsluiten</span><span class="sxs-lookup"><span data-stu-id="f79f7-221">Shutdown</span></span></td>
  <td><span data-ttu-id="f79f7-222">Hello Azure Cosmos DB-Emulator wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-222">Shuts down hello Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="f79f7-223">CosmosDB.Emulator.exe/Shutdown</span><span class="sxs-lookup"><span data-stu-id="f79f7-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-224">Gegevenspad</span><span class="sxs-lookup"><span data-stu-id="f79f7-224">DataPath</span></span></td>
  <td><span data-ttu-id="f79f7-225">Hallo pad aangeeft in welke toostore gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-225">Specifies hello path in which toostore data files.</span></span> <span data-ttu-id="f79f7-226">Standaard is % LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="f79f7-227">CosmosDB.Emulator.exe /DataPath =&lt;gegevenspad&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-228">&lt;gegevenspad&gt;: een toegankelijk pad</span><span class="sxs-lookup"><span data-stu-id="f79f7-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-229">Poort</span><span class="sxs-lookup"><span data-stu-id="f79f7-229">Port</span></span></td>
  <td><span data-ttu-id="f79f7-230">Hiermee geeft u de Hallo poort nummer toouse Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-230">Specifies hello port number toouse for hello emulator.</span></span>  <span data-ttu-id="f79f7-231">De standaardwaarde is 8081.</span><span class="sxs-lookup"><span data-stu-id="f79f7-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="f79f7-232">CosmosDB.Emulator.exe/Port =&lt;poort&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-233">&lt;poort&gt;: poortnummer</span><span class="sxs-lookup"><span data-stu-id="f79f7-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="f79f7-234">MongoPort</span></span></td>
  <td><span data-ttu-id="f79f7-235">Hiermee geeft u Hallo poort nummer toouse voor MongoDB-compatibiliteit API.</span><span class="sxs-lookup"><span data-stu-id="f79f7-235">Specifies hello port number toouse for MongoDB compatibility API.</span></span> <span data-ttu-id="f79f7-236">De standaardwaarde is 10255.</span><span class="sxs-lookup"><span data-stu-id="f79f7-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="f79f7-237">CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-238">&lt;mongoport&gt;: poortnummer</span><span class="sxs-lookup"><span data-stu-id="f79f7-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="f79f7-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="f79f7-240">Hiermee geeft u Hallo poorten toouse voor rechtstreekse connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="f79f7-240">Specifies hello ports toouse for direct connectivity.</span></span> <span data-ttu-id="f79f7-241">Standaardwaarden zijn 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="f79f7-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="f79f7-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-243">&lt;directports&gt;: door komma's gescheiden lijst met 4 poorten</span><span class="sxs-lookup"><span data-stu-id="f79f7-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-244">Sleutel</span><span class="sxs-lookup"><span data-stu-id="f79f7-244">Key</span></span></td>
  <td><span data-ttu-id="f79f7-245">De autorisatiesleutel voor Hallo-emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-245">Authorization key for hello emulator.</span></span> <span data-ttu-id="f79f7-246">Sleutel moet Hallo base 64-codering van een 64-byte-vector.</span><span class="sxs-lookup"><span data-stu-id="f79f7-246">Key must be hello base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="f79f7-247">CosmosDB.Emulator.exe/key:&lt;sleutel&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-248">&lt;sleutel&gt;: sleutel moet Hallo base 64-codering van een 64-byte-vector</span><span class="sxs-lookup"><span data-stu-id="f79f7-248">&lt;key&gt;: Key must be hello base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="f79f7-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="f79f7-250">Hiermee geeft u op deze aanvraag snelheidsbeperking gedrag is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f79f7-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="f79f7-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="f79f7-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="f79f7-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="f79f7-253">Hiermee geeft u op deze aanvraag snelheidsbeperking gedrag is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f79f7-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="f79f7-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="f79f7-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="f79f7-255">NoUI</span></span></td>
  <td><span data-ttu-id="f79f7-256">Niet weergeven Hallo emulator gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="f79f7-256">Do not show hello emulator user interface.</span></span></td>
  <td><span data-ttu-id="f79f7-257">/ Noui CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="f79f7-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="f79f7-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="f79f7-259">Geen documentverkenner weergeven bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="f79f7-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="f79f7-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="f79f7-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="f79f7-262">Hiermee geeft u Hallo maximumaantal gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-262">Specifies hello maximum number of partitioned collections.</span></span> <span data-ttu-id="f79f7-263">Zie [Hallo aantal verzamelingen wijzigen](#set-partitioncount) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f79f7-263">See [Change hello number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="f79f7-264">CosmosDB.Emulator.exe /PartitionCount =&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-265">&lt;partitioncount&gt;: het maximale aantal toegestane verzamelingen met één partitie.</span><span class="sxs-lookup"><span data-stu-id="f79f7-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="f79f7-266">Standaardwaarde is 25.</span><span class="sxs-lookup"><span data-stu-id="f79f7-266">Default is 25.</span></span> <span data-ttu-id="f79f7-267">Maximaal toegestane aantal is 250.</span><span class="sxs-lookup"><span data-stu-id="f79f7-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="f79f7-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="f79f7-269">Hiermee geeft u Hallo standaardaantal partities voor een gepartitioneerde verzameling.</span><span class="sxs-lookup"><span data-stu-id="f79f7-269">Specifies hello default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="f79f7-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-271">&lt;defaultpartitioncount&gt; standaardwaarde is 25.</span><span class="sxs-lookup"><span data-stu-id="f79f7-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="f79f7-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="f79f7-273">Hiermee toegang tot toohello emulator via een netwerk.</span><span class="sxs-lookup"><span data-stu-id="f79f7-273">Enables access toohello emulator over a network.</span></span> <span data-ttu-id="f79f7-274">U moet ook doorgeven/Key =&lt;key_string&gt; of/KeyFile =&lt;bestandsnaam&gt; tooenable toegang tot het netwerk.</span><span class="sxs-lookup"><span data-stu-id="f79f7-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; tooenable network access.</span></span></td>
  <td><span data-ttu-id="f79f7-275">CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="f79f7-276">of</span><span class="sxs-lookup"><span data-stu-id="f79f7-276">or</span></span><br><br><span data-ttu-id="f79f7-277">CosmosDB.Emulator.exe /AllowNetworkAccess/KeyFile =&lt;bestandsnaam&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="f79f7-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="f79f7-279">Firewall-regels niet worden aangepast wanneer /AllowNetworkAccess wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f79f7-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="f79f7-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="f79f7-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="f79f7-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="f79f7-282">Een nieuwe autorisatiesleutel genereren en opslaan van het opgegeven bestand toohello.</span><span class="sxs-lookup"><span data-stu-id="f79f7-282">Generate a new authorization key and save toohello specified file.</span></span> <span data-ttu-id="f79f7-283">Hallo gegenereerde sleutel kan worden gebruikt met Hallo/Key of/KeyFile opties.</span><span class="sxs-lookup"><span data-stu-id="f79f7-283">hello generated key can be used with hello /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="f79f7-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;pad tookey bestand&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path tookey file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-285">Consistentie</span><span class="sxs-lookup"><span data-stu-id="f79f7-285">Consistency</span></span></td>
  <td><span data-ttu-id="f79f7-286">Hallo standaardniveau consistentie voor Hallo account instellen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-286">Set hello default consistency level for hello account.</span></span></td>
  <td><span data-ttu-id="f79f7-287">CosmosDB.Emulator.exe /Consistency =&lt;consistentie&gt;</span><span class="sxs-lookup"><span data-stu-id="f79f7-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="f79f7-288">&lt;consistentie&gt;: waarde moet een van de volgende Hallo [consistentieniveaus](consistency-levels.md): sessie, sterke, Eventual of BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="f79f7-288">&lt;consistency&gt;: Value must be one of hello following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="f79f7-289">de standaardwaarde Hallo is sessie.</span><span class="sxs-lookup"><span data-stu-id="f79f7-289">hello default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="f79f7-290">?</span><span class="sxs-lookup"><span data-stu-id="f79f7-290">?</span></span></td>
  <td><span data-ttu-id="f79f7-291">Hallo-bericht van help weergeven.</span><span class="sxs-lookup"><span data-stu-id="f79f7-291">Show hello help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-hello-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="f79f7-292">Verschillen tussen hello Azure Cosmos DB Emulator en Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="f79f7-292">Differences between hello Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="f79f7-293">Omdat hello Azure Cosmos DB Emulator een geëmuleerde omgeving uitgevoerd op een lokale developer-werkstation biedt, zijn er enkele verschillen in functionaliteit tussen Hallo-emulator en een Cosmos-DB Azure-account in Hallo cloud:</span><span class="sxs-lookup"><span data-stu-id="f79f7-293">Because hello Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between hello emulator and an Azure Cosmos DB account in hello cloud:</span></span>

* <span data-ttu-id="f79f7-294">Hello Azure Cosmos DB Emulator ondersteunt slechts één vaste account en een bekende hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="f79f7-294">hello Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="f79f7-295">Toegangssleutel wordt opnieuw gegenereerd, is niet mogelijk in hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-295">Key regeneration is not possible in hello Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="f79f7-296">Hello Azure Cosmos DB Emulator is niet een schaalbare service en wordt geen ondersteuning voor een groot aantal verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-296">hello Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="f79f7-297">Hello Azure Cosmos DB Emulator komt niet simuleren verschillende [Azure Cosmos DB consistentieniveaus](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="f79f7-297">hello Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="f79f7-298">Hello Azure Cosmos DB Emulator komt niet simuleren [meerdere landen/regio replicatie](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="f79f7-298">hello Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="f79f7-299">Hello Azure Cosmos DB Emulator biedt geen ondersteuning voor Hallo service quotum onderdrukkingen die beschikbaar in hello Azure DB die Cosmos-service (bijvoorbeeld de maximale grootte document, verbeterde gepartitioneerde verzameling opslag zijn).</span><span class="sxs-lookup"><span data-stu-id="f79f7-299">hello Azure Cosmos DB Emulator does not support hello service quota overrides that are available in hello Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="f79f7-300">Als uw exemplaar van hello Azure Cosmos DB Emulator mogelijk niet omhoog toodate met de meest recente wijzigingen Hallo met hello Azure DB die Cosmos-service, neemt u [Azure DB die Cosmos-Capaciteitsplanner](https://www.documentdb.com/capacityplanner) tooaccurately schatting productie doorvoer (RUs) de behoeften van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f79f7-300">As your copy of hello Azure Cosmos DB Emulator might not be up toodate with hello most recent changes with hello Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) tooaccurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="f79f7-301"><a id="set-partitioncount"></a>Aantal verzamelingen Hallo wijzigen</span><span class="sxs-lookup"><span data-stu-id="f79f7-301"><a id="set-partitioncount"></a>Change hello number of collections</span></span>

<span data-ttu-id="f79f7-302">Standaard kunt u verzamelingen met één partitie too25 of 1 gepartitioneerde verzameling op basis van hello Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-302">By default, you can create up too25 single partition collections, or 1 partitioned collection using hello Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="f79f7-303">Doordat Hallo **PartitionCount** waarde, kunt u verzamelingen met één partitie too250 of 10 gepartitioneerde verzamelingen of een combinatie van twee die niet meer dan 250 één Hallo partities (waar 1 gepartitioneerd verzameling = 25 één partitie verzameling).</span><span class="sxs-lookup"><span data-stu-id="f79f7-303">By modifying hello **PartitionCount** value, you can create up too250 single partition collections or 10 partitioned collections, or any combination of hello two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="f79f7-304">Als u een verzameling toocreate probeert nadat de huidige partitie aantal Hallo is overschreden, Hallo emulator een ServiceUnavailable-uitzondering genereert met het volgende bericht Hallo.</span><span class="sxs-lookup"><span data-stu-id="f79f7-304">If you attempt toocreate a collection after hello current partition count has been exceeded, hello emulator throws a ServiceUnavailable exception, with hello following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    toobring more and more capacity online, and encourage you tootry again. 
    Please do not hesitate tooemail docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="f79f7-305">toochange hello aantal verzamelingen beschikbaar toohello Azure Cosmos DB Emulator Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f79f7-305">toochange hello number of collections available toohello Azure Cosmos DB Emulator, do hello following:</span></span>

1. <span data-ttu-id="f79f7-306">Alle lokale Azure Cosmos DB Emulator gegevens verwijderen met de rechtermuisknop op Hallo **Azure Cosmos DB Emulator** pictogram in systeemvak Hallo en vervolgens te klikken **gegevens opnieuw instellen...** .</span><span class="sxs-lookup"><span data-stu-id="f79f7-306">Delete all local Azure Cosmos DB Emulator data by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="f79f7-307">Alle gegevens van de emulator in deze map C:\Users\user_name\AppData\Local\CosmosDBEmulator verwijderen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="f79f7-308">Sluit alle geopende exemplaren met de rechtermuisknop op Hallo **Azure Cosmos DB Emulator** -pictogram op het systeemvak Hallo en vervolgens te klikken op **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="f79f7-308">Exit all open instances by right-clicking hello **Azure Cosmos DB Emulator** icon on hello system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="f79f7-309">Het duurt een paar minuten voor alle exemplaren tooexit.</span><span class="sxs-lookup"><span data-stu-id="f79f7-309">It may take a minute for all instances tooexit.</span></span>
4. <span data-ttu-id="f79f7-310">Installeer de meest recente versie Hallo Hallo [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="f79f7-310">Install hello latest version of hello [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="f79f7-311">Hallo-emulator Hello PartitionCount vlag starten door een waarde < = 250.</span><span class="sxs-lookup"><span data-stu-id="f79f7-311">Launch hello emulator with hello PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="f79f7-312">Bijvoorbeeld: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="f79f7-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="f79f7-313">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f79f7-313">Troubleshooting</span></span>

<span data-ttu-id="f79f7-314">Gebruik Hallo toohelp oplossen van problemen die u tegenkomt met hello Azure Cosmos DB emulator tips te volgen:</span><span class="sxs-lookup"><span data-stu-id="f79f7-314">Use hello following tips toohelp troubleshoot issues you encounter with hello Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="f79f7-315">Als u een nieuwe versie van Hallo Emulator geïnstalleerd en worden er fouten optreden, zorg ervoor dat u uw gegevens herstellen.</span><span class="sxs-lookup"><span data-stu-id="f79f7-315">If you installed a new version of hello Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="f79f7-316">U kunt uw gegevens herstellen door met de rechtermuisknop op Hallo Azure Cosmos DB Emulator pictogram in systeemvak Hallo en vervolgens te klikken op de gegevens opnieuw instellen...</span><span class="sxs-lookup"><span data-stu-id="f79f7-316">You can reset your data by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="f79f7-317">Als Hallo fouten die niet wordt opgelost, kunt u deze kunt verwijderen en opnieuw installeren Hallo app.</span><span class="sxs-lookup"><span data-stu-id="f79f7-317">If that does not fix hello errors, you can uninstall and reinstall hello app.</span></span> <span data-ttu-id="f79f7-318">Zie [verwijderen van de lokale emulator Hallo](#uninstall) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="f79f7-318">See [Uninstall hello local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="f79f7-319">Als hello Azure Cosmos DB emulator vastloopt, dumpbestanden verzamelen uit de map c:\Users\user_name\AppData\Local\CrashDumps, deze comprimeren en koppelt u ze tooan e-mailbericht te[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f79f7-319">If hello Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="f79f7-320">Als u crashes ondervindt in CosmosDB.StartupEntryPoint.exe, voert u de volgende opdracht vanaf een opdrachtprompt admin Hallo:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="f79f7-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run hello following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="f79f7-321">Als u een verbindingsprobleem ondervindt [verzamelen traceringsbestanden](#trace-files), deze comprimeren en koppelt u ze tooan e-mailbericht te[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f79f7-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them tooan email too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="f79f7-322">Als u krijgt een **Service niet beschikbaar** bericht wordt weergegeven, hello emulator waarschijnlijk defect tooinitialize Hallo network-stack.</span><span class="sxs-lookup"><span data-stu-id="f79f7-322">If you receive a **Service Unavailable** message, hello emulator might be failing tooinitialize hello network stack.</span></span> <span data-ttu-id="f79f7-323">Controleer toosee als er beveiligde Hallo Pulse-client of Juniper netwerken client is geïnstalleerd, zoals netwerk filterstuurprogramma Hallo probleem kunnen veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="f79f7-323">Check toosee if you have hello Pulse secure client or Juniper networks client installed, as their network filter drivers may cause hello problem.</span></span> <span data-ttu-id="f79f7-324">Verwijderen van stuurprogramma's van derden netwerk filter doorgaans, wordt het Hallo-probleem opgelost.</span><span class="sxs-lookup"><span data-stu-id="f79f7-324">Uninstalling third party network filter drivers typically fixes hello issue.</span></span>

### <span data-ttu-id="f79f7-325"><a id="trace-files"></a>Traceringsbestanden verzamelen</span><span class="sxs-lookup"><span data-stu-id="f79f7-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="f79f7-326">toocollect foutopsporingsgegevens Hallo volgende opdrachten uit een administratieve opdrachtprompt worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f79f7-326">toocollect debugging traces, run hello following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="f79f7-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="f79f7-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="f79f7-328">Controle Hallo system lade toomake ervoor Hallo programma is afgesloten, kan een minuut duren.</span><span class="sxs-lookup"><span data-stu-id="f79f7-328">Watch hello system tray toomake sure hello program has shut down, it may take a minute.</span></span> <span data-ttu-id="f79f7-329">U kunt ook klikken op **afsluiten** in de gebruikersinterface van hello Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="f79f7-329">You can also just click **Exit** in hello Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="f79f7-330">Hallo probleem reproduceren.</span><span class="sxs-lookup"><span data-stu-id="f79f7-330">Reproduce hello problem.</span></span> <span data-ttu-id="f79f7-331">Als u Data Explorer niet werkt, hoeft u alleen toowait voor Hallo browser tooopen voor een paar seconden toocatch Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="f79f7-331">If Data Explorer is not working, you only need toowait for hello browser tooopen for a few seconds toocatch hello error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="f79f7-332">Navigeer te`%ProgramFiles%\Azure Cosmos DB Emulator` en Hallo docdbemulator_000001.etl bestand vinden.</span><span class="sxs-lookup"><span data-stu-id="f79f7-332">Navigate too`%ProgramFiles%\Azure Cosmos DB Emulator` and find hello docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="f79f7-333">Hallo etl-bestand samen met Reproductiestappen te verzenden[ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="f79f7-333">Send hello .etl file along with repro steps too[askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="f79f7-334"><a id="uninstall"></a>Verwijder Hallo lokale Emulator</span><span class="sxs-lookup"><span data-stu-id="f79f7-334"><a id="uninstall"></a>Uninstall hello local Emulator</span></span>

1. <span data-ttu-id="f79f7-335">Sluit alle geopende exemplaren van Hallo lokale Emulator met de rechtermuisknop op Hallo Azure Cosmos DB Emulator pictogram in systeemvak hello, klikt op afsluiten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-335">Exit all open instances of hello local Emulator by right-clicking hello Azure Cosmos DB Emulator icon on hello system tray, and then clicking Exit.</span></span> <span data-ttu-id="f79f7-336">Het duurt een paar minuten voor alle exemplaren tooexit.</span><span class="sxs-lookup"><span data-stu-id="f79f7-336">It may take a minute for all instances tooexit.</span></span>
2. <span data-ttu-id="f79f7-337">Typ in het zoekvak van Hallo Windows **Apps en functies** en klik op Hallo **Apps en -functies (systeeminstellingen)** resultaat.</span><span class="sxs-lookup"><span data-stu-id="f79f7-337">In hello Windows search box, type **Apps & features** and click on hello **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="f79f7-338">Schuif te in de lijst met apps Hallo**Azure Cosmos DB Emulator**, selecteert u het, klik op **verwijderen**, bevestigen en klikt u op **verwijderen** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f79f7-338">In hello list of apps, scroll too**Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="f79f7-339">Hallo-app wordt verwijderd, gaat u tooC:\Users\<gebruiker > \AppData\Local\CosmosDBEmulator en delete Hallo-map.</span><span class="sxs-lookup"><span data-stu-id="f79f7-339">When hello app is uninstalled, navigate tooC:\Users\<user>\AppData\Local\CosmosDBEmulator and delete hello folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f79f7-340">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f79f7-340">Next steps</span></span>

<span data-ttu-id="f79f7-341">In deze zelfstudie hebt u Hallo volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="f79f7-341">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f79f7-342">Geïnstalleerd Hallo lokale Emulator</span><span class="sxs-lookup"><span data-stu-id="f79f7-342">Installed hello local Emulator</span></span>
> * <span data-ttu-id="f79f7-343">Rand Hallo Emulator op Docker voor Windows</span><span class="sxs-lookup"><span data-stu-id="f79f7-343">Rand hello Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="f79f7-344">Geverifieerde aanvragen</span><span class="sxs-lookup"><span data-stu-id="f79f7-344">Authenticated requests</span></span>
> * <span data-ttu-id="f79f7-345">Hallo Data Explorer in Hallo Emulator gebruikt</span><span class="sxs-lookup"><span data-stu-id="f79f7-345">Used hello Data Explorer in hello Emulator</span></span>
> * <span data-ttu-id="f79f7-346">Geëxporteerde SSL-certificaten</span><span class="sxs-lookup"><span data-stu-id="f79f7-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="f79f7-347">Hallo Emulator vanaf de opdrachtregel Hallo aangeroepen</span><span class="sxs-lookup"><span data-stu-id="f79f7-347">Called hello Emulator from hello command line</span></span>
> * <span data-ttu-id="f79f7-348">Verzamelde traceringsbestanden</span><span class="sxs-lookup"><span data-stu-id="f79f7-348">Collected trace files</span></span>

<span data-ttu-id="f79f7-349">In deze zelfstudie hebt u geleerd hoe toouse Hallo lokale Emulator voor gratis lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="f79f7-349">In this tutorial, you've learned how toouse hello local Emulator for free local development.</span></span> <span data-ttu-id="f79f7-350">U kunt nu de volgende zelfstudie toohello gaan en meer informatie hoe tooexport Emulator SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="f79f7-350">You can now proceed toohello next tutorial and learn how tooexport Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="f79f7-351">Hello Azure Cosmos DB Emulator certificaten exporteren</span><span class="sxs-lookup"><span data-stu-id="f79f7-351">Export hello Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)

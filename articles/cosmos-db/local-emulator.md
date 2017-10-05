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
# <a name="use-the-azure-cosmos-db-emulator-for-local-development-and-testing"></a><span data-ttu-id="cd92b-104">De Azure Cosmos DB Emulator gebruiken voor lokale ontwikkeling en testen</span><span class="sxs-lookup"><span data-stu-id="cd92b-104">Use the Azure Cosmos DB Emulator for local development and testing</span></span>

<table>
<tr>
  <td><span data-ttu-id="cd92b-105"><strong>Binaire bestanden</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-105"><strong>Binaries</strong></span></span></td>
  <td>[<span data-ttu-id="cd92b-106">MSI downloaden</span><span class="sxs-lookup"><span data-stu-id="cd92b-106">Download MSI</span></span>](https://aka.ms/cosmosdb-emulator)</td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-107"><strong>Docker</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-107"><strong>Docker</strong></span></span></td>
  <td>[<span data-ttu-id="cd92b-108">Docker-Hub</span><span class="sxs-lookup"><span data-stu-id="cd92b-108">Docker Hub</span></span>](https://hub.docker.com/r/microsoft/azure-documentdb-emulator/)</td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-109"><strong>Docker-bron</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-109"><strong>Docker source</strong></span></span></td>
  <td>[<span data-ttu-id="cd92b-110">GitHub</span><span class="sxs-lookup"><span data-stu-id="cd92b-110">Github</span></span>](https://github.com/azure/azure-documentdb-emulator-docker)</td>
</tr>
</table>
  
<span data-ttu-id="cd92b-111">De Azure-Emulator Cosmos DB biedt een lokale omgeving waarin de service Azure Cosmos DB voor ontwikkelingsdoeleinden worden geëmuleerd.</span><span class="sxs-lookup"><span data-stu-id="cd92b-111">The Azure Cosmos DB Emulator provides a local environment that emulates the Azure Cosmos DB service for development purposes.</span></span> <span data-ttu-id="cd92b-112">Met behulp van de Azure-Emulator Cosmos DB, kunt u ontwikkelen en testen van de toepassing lokaal zonder te maken van een Azure-abonnement of mogelijke kosten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-112">Using the Azure Cosmos DB Emulator, you can develop and test your application locally, without creating an Azure subscription or incurring any costs.</span></span> <span data-ttu-id="cd92b-113">Wanneer u tevreden bent over hoe uw toepassing in de Azure-Emulator Cosmos DB werkt, kunt u overschakelen naar het met een Azure DB die Cosmos-account in de cloud.</span><span class="sxs-lookup"><span data-stu-id="cd92b-113">When you're satisfied with how your application is working in the Azure Cosmos DB Emulator, you can switch to using an Azure Cosmos DB account in the cloud.</span></span>

<span data-ttu-id="cd92b-114">In dit artikel bevat informatie over de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="cd92b-114">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cd92b-115">Installeren van de Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-115">Installing the Emulator</span></span>
> * <span data-ttu-id="cd92b-116">De Emulator uitgevoerd op Docker voor Windows</span><span class="sxs-lookup"><span data-stu-id="cd92b-116">Running the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="cd92b-117">Verificatie van aanvragen</span><span class="sxs-lookup"><span data-stu-id="cd92b-117">Authenticating requests</span></span>
> * <span data-ttu-id="cd92b-118">Met behulp van de Data Explorer in de Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-118">Using the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="cd92b-119">SSL-certificaten exporteren</span><span class="sxs-lookup"><span data-stu-id="cd92b-119">Exporting SSL certificates</span></span>
> * <span data-ttu-id="cd92b-120">Het aanroepen van de Emulator vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="cd92b-120">Calling the Emulator from the command line</span></span>
> * <span data-ttu-id="cd92b-121">Traceringsbestanden verzamelen</span><span class="sxs-lookup"><span data-stu-id="cd92b-121">Collecting trace files</span></span>

<span data-ttu-id="cd92b-122">Het is raadzaam om aan de slag door het bekijken van de volgende video, waarbij Kirill Gavrylyuk ziet u hoe u aan de slag met de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-122">We recommend getting started by watching the following video, where Kirill Gavrylyuk shows how to get started with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="cd92b-123">Denk eraan dat de video verwijst naar de emulator als de DocumentDB-Emulator, maar het programma zelf is de Azure-Emulator Cosmos DB gewijzigd sinds de video grondverf.</span><span class="sxs-lookup"><span data-stu-id="cd92b-123">Note that the video refers to the emulator as the DocumentDB Emulator, but the tool itself has been renamed the Azure Cosmos DB Emulator since taping the video.</span></span> <span data-ttu-id="cd92b-124">Alle informatie in de video is nog steeds correct zijn voor de Emulator Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-124">All information in the video is still accurate for the Azure Cosmos DB Emulator.</span></span> 

> [!VIDEO https://channel9.msdn.com/Events/Connect/2016/192/player]
> 
> 

## <a name="how-the-emulator-works"></a><span data-ttu-id="cd92b-125">De werking van de Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-125">How the Emulator works</span></span>
<span data-ttu-id="cd92b-126">De Azure-Emulator Cosmos DB biedt een hoogwaardige emulatie van de service Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-126">The Azure Cosmos DB Emulator provides a high-fidelity emulation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="cd92b-127">Het ondersteunt dezelfde functionaliteit als Azure Cosmos DB, inclusief ondersteuning voor het maken en uitvoeren van query's JSON-documenten, inrichting en schalen van verzamelingen en uitvoering van opgeslagen procedures en triggers.</span><span class="sxs-lookup"><span data-stu-id="cd92b-127">It supports identical functionality as Azure Cosmos DB, including support for creating and querying JSON documents, provisioning and scaling collections, and executing stored procedures and triggers.</span></span> <span data-ttu-id="cd92b-128">U kunt ontwikkelen en testen van toepassingen met behulp van de Azure-Emulator Cosmos-database en deze implementeren in Azure op schaal globale door het maken van een configuratie voor één eindpunt van de verbinding voor Azure Cosmos DB wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-128">You can develop and test applications using the Azure Cosmos DB Emulator, and deploy them to Azure at global scale by just making a single configuration change to the connection endpoint for Azure Cosmos DB.</span></span>

<span data-ttu-id="cd92b-129">Terwijl we een lokale emulatie van hoge kwaliteit van de werkelijke Azure DB die Cosmos-service hebt gemaakt, is de implementatie van de Azure Cosmos DB-Emulator is anders dan die van de service.</span><span class="sxs-lookup"><span data-stu-id="cd92b-129">While we created a high-fidelity local emulation of the actual Azure Cosmos DB service, the implementation of the Azure Cosmos DB Emulator is different than that of the service.</span></span> <span data-ttu-id="cd92b-130">De Azure-Emulator Cosmos DB gebruikt bijvoorbeeld de standaard OS-componenten zoals het lokale bestandssysteem voor de persistentie en HTTPS-protocolstack voor connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="cd92b-130">For example, the Azure Cosmos DB Emulator uses standard OS components such as the local file system for persistence, and HTTPS protocol stack for connectivity.</span></span> <span data-ttu-id="cd92b-131">Dit betekent dat bepaalde functies die afhankelijk van de Azure-infrastructuur is zoals globale replicatie, één cijfer milliseconde latentie voor leest/schrijft en instelbare consistentieniveaus zijn niet beschikbaar via de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-131">This means that some functionality that relies on Azure infrastructure like global replication, single-digit millisecond latency for reads/writes, and tunable consistency levels are not available via the Azure Cosmos DB Emulator.</span></span>

> [!NOTE]
> <span data-ttu-id="cd92b-132">Op dit moment ondersteunt de Data Explorer in de emulator alleen het maken van verzamelingen voor DocumentDB-API en MongoDB-verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-132">At this time the Data Explorer in the emulator only supports the creation of DocumentDB API collections and MongoDB collections.</span></span> <span data-ttu-id="cd92b-133">De Data Explorer in de emulator biedt momenteel geen ondersteuning voor het maken van tabellen en grafieken kunt maken.</span><span class="sxs-lookup"><span data-stu-id="cd92b-133">The Data Explorer in the emulator does not currently support the creation of tables and graphs.</span></span> 

## <a name="system-requirements"></a><span data-ttu-id="cd92b-134">Systeemvereisten</span><span class="sxs-lookup"><span data-stu-id="cd92b-134">System requirements</span></span>
<span data-ttu-id="cd92b-135">De Azure-Emulator Cosmos DB heeft de volgende hardware en software-vereisten:</span><span class="sxs-lookup"><span data-stu-id="cd92b-135">The Azure Cosmos DB Emulator has the following hardware and software requirements:</span></span>

* <span data-ttu-id="cd92b-136">Softwarevereisten</span><span class="sxs-lookup"><span data-stu-id="cd92b-136">Software requirements</span></span>
  * <span data-ttu-id="cd92b-137">Windows Server 2012 R2, WindowsServer 2016 of Windows 10</span><span class="sxs-lookup"><span data-stu-id="cd92b-137">Windows Server 2012 R2, Windows Server 2016, or Windows 10</span></span>
*   <span data-ttu-id="cd92b-138">Minimale hardwarevereisten</span><span class="sxs-lookup"><span data-stu-id="cd92b-138">Minimum Hardware requirements</span></span>
  * <span data-ttu-id="cd92b-139">2 GB RAM-GEHEUGEN</span><span class="sxs-lookup"><span data-stu-id="cd92b-139">2 GB RAM</span></span>
  * <span data-ttu-id="cd92b-140">10 GB beschikbare schijfruimte</span><span class="sxs-lookup"><span data-stu-id="cd92b-140">10 GB available hard disk space</span></span>

## <a name="installation"></a><span data-ttu-id="cd92b-141">Installeren</span><span class="sxs-lookup"><span data-stu-id="cd92b-141">Installation</span></span>
<span data-ttu-id="cd92b-142">U kunt downloaden en installeren van de Azure Cosmos DB-Emulator van de [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="cd92b-142">You can download and install the Azure Cosmos DB Emulator from the [Microsoft Download Center](https://aka.ms/cosmosdb-emulator).</span></span> 

> [!NOTE]
> <span data-ttu-id="cd92b-143">Als u wilt installeren, configureren en uitvoeren van de Azure Cosmos DB-Emulator, moet u beheerdersbevoegdheden hebben op de computer.</span><span class="sxs-lookup"><span data-stu-id="cd92b-143">To install, configure, and run the Azure Cosmos DB Emulator, you must have administrative privileges on the computer.</span></span>

## <a name="running-on-docker-for-windows"></a><span data-ttu-id="cd92b-144">Uitgevoerd op Docker voor Windows</span><span class="sxs-lookup"><span data-stu-id="cd92b-144">Running on Docker for Windows</span></span>

<span data-ttu-id="cd92b-145">De Azure-Emulator Cosmos DB kan worden uitgevoerd op Docker voor Windows.</span><span class="sxs-lookup"><span data-stu-id="cd92b-145">The Azure Cosmos DB Emulator can be run on Docker for Windows.</span></span> <span data-ttu-id="cd92b-146">De Emulator werkt niet op Docker voor Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="cd92b-146">The Emulator does not work on Docker for Oracle Linux.</span></span>

<span data-ttu-id="cd92b-147">Zodra u hebt [Docker voor Windows](https://www.docker.com/docker-windows) geïnstalleerd, kunt u de installatiekopie van de Emulator van Docker-Hub pull met de volgende opdracht in uw favoriete shell (cmd.exe, PowerShell, enz.).</span><span class="sxs-lookup"><span data-stu-id="cd92b-147">Once you have [Docker for Windows](https://www.docker.com/docker-windows) installed, you can pull the Emulator image from Docker Hub by running the following command from your favorite shell (cmd.exe, PowerShell, etc.).</span></span>

```      
docker pull microsoft/azure-cosmosdb-emulator 
```
<span data-ttu-id="cd92b-148">Voer de volgende opdrachten voor het starten van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="cd92b-148">To start the image, run the following commands.</span></span>

``` 
md %LOCALAPPDATA%\CosmosDBEmulatorCert 2>nul
docker run -v %LOCALAPPDATA%\CosmosDBEmulatorCert:c:\CosmosDBEmulator\CosmosDBEmulatorCert -P -t -i microsoft/azure-cosmosdb-emulator 
```

<span data-ttu-id="cd92b-149">Het antwoord ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="cd92b-149">The response looks similar to the following:</span></span>

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

<span data-ttu-id="cd92b-150">De interactieve shell sluiten nadat de Emulator is gestart wordt afgesloten container van de Emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-150">Closing the interactive shell once the Emulator has been started will shutdown the Emulator’s container.</span></span>

<span data-ttu-id="cd92b-151">Het eindpunt en de hoofdsleutel in uit het antwoord in de client en het SSL-certificaat importeren in de host.</span><span class="sxs-lookup"><span data-stu-id="cd92b-151">Use the endpoint and master key in from the response in your client and import the SSL certificate into your host.</span></span> <span data-ttu-id="cd92b-152">Doe het volgende vanaf een opdrachtprompt admin voor het importeren van het SSL-certificaat:</span><span class="sxs-lookup"><span data-stu-id="cd92b-152">To import the SSL certificate, do the following from an admin command prompt:</span></span>

```
cd %LOCALAPPDATA%\CosmosDBEmulatorCert
powershell .\importcert.ps1
```


## <a name="start-the-emulator"></a><span data-ttu-id="cd92b-153">Start de Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-153">Start the Emulator</span></span>

<span data-ttu-id="cd92b-154">Start de Emulator Azure Cosmos DB, selecteer de knop Start of druk op de Windows-toets.</span><span class="sxs-lookup"><span data-stu-id="cd92b-154">To start the Azure Cosmos DB Emulator, select the Start button or press the Windows key.</span></span> <span data-ttu-id="cd92b-155">Begint te typen **Azure Cosmos DB Emulator**, en selecteert u de emulator in de lijst met toepassingen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-155">Begin typing **Azure Cosmos DB Emulator**, and select the emulator from the list of applications.</span></span> 

![Selecteer de knop Start of druk op de Windows-toets, begint te typen ** Azure Cosmos DB Emulator ** en selecteert u de emulator van de lijst met toepassingen](./media/local-emulator/database-local-emulator-start.png)

<span data-ttu-id="cd92b-157">Wanneer de emulator wordt uitgevoerd, ziet u een pictogram in het Windows-systeemvak.</span><span class="sxs-lookup"><span data-stu-id="cd92b-157">When the emulator is running, you'll see an icon in the Windows taskbar notification area.</span></span> ![Azure DB Cosmos lokale emulator taakbalk melding](./media/local-emulator/database-local-emulator-taskbar.png)

<span data-ttu-id="cd92b-159">De Azure DB-Emulator standaard Cosmos wordt uitgevoerd op de lokale computer ('localhost'), luistert op poort 8081.</span><span class="sxs-lookup"><span data-stu-id="cd92b-159">The Azure Cosmos DB Emulator by default runs on the local machine ("localhost") listening on port 8081.</span></span>

<span data-ttu-id="cd92b-160">De Azure-Emulator Cosmos DB wordt standaard geïnstalleerd bij naar de `C:\Program Files\Azure Cosmos DB Emulator` directory.</span><span class="sxs-lookup"><span data-stu-id="cd92b-160">The Azure Cosmos DB Emulator is installed by default to the `C:\Program Files\Azure Cosmos DB Emulator` directory.</span></span> <span data-ttu-id="cd92b-161">U kunt ook starten en stoppen van de emulator vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="cd92b-161">You can also start and stop the emulator from the command-line.</span></span> <span data-ttu-id="cd92b-162">Zie [opdrachtregelprogramma](#command-line) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cd92b-162">See [command-line tool reference](#command-line) for more information.</span></span>

## <a name="start-data-explorer"></a><span data-ttu-id="cd92b-163">Start de Data Explorer</span><span class="sxs-lookup"><span data-stu-id="cd92b-163">Start Data Explorer</span></span>

<span data-ttu-id="cd92b-164">Wanneer de emulator Azure Cosmos DB opent, wordt deze automatisch Azure Cosmos DB Data Explorer geopend in uw browser.</span><span class="sxs-lookup"><span data-stu-id="cd92b-164">When the Azure Cosmos DB emulator launches it will automatically open the Azure Cosmos DB Data Explorer in your browser.</span></span> <span data-ttu-id="cd92b-165">Het adres wordt weergegeven als [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span><span class="sxs-lookup"><span data-stu-id="cd92b-165">The address will appear as [https://localhost:8081/_explorer/index.html](https://localhost:8081/_explorer/index.html).</span></span> <span data-ttu-id="cd92b-166">Als u de explorer sluiten en wilt het later opnieuw openen, kunt u de URL in uw browser te openen of starten van de Azure-Emulator Cosmos-database in het pictogram in systeemvak voor Windows, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cd92b-166">If you close the explorer and would like to re-open it later, you can either open the URL in your browser or launch it from the Azure Cosmos DB Emulator in the Windows Tray Icon as shown below.</span></span>

![Azure DB Cosmos lokale emulator data explorer starten](./media/local-emulator/database-local-emulator-data-explorer-launcher.png)

## <a name="checking-for-updates"></a><span data-ttu-id="cd92b-168">Controleren op updates</span><span class="sxs-lookup"><span data-stu-id="cd92b-168">Checking for updates</span></span>
<span data-ttu-id="cd92b-169">Data Explorer geeft aan of er een nieuwe update beschikbaar voor downloaden.</span><span class="sxs-lookup"><span data-stu-id="cd92b-169">Data Explorer indicates if there is a new update available for download.</span></span> 

> [!NOTE]
> <span data-ttu-id="cd92b-170">Gegevens die zijn gemaakt in een versie van de Azure-Emulator Cosmos-database kan niet worden gegarandeerd toegankelijk zijn voor het gebruik van een andere versie.</span><span class="sxs-lookup"><span data-stu-id="cd92b-170">Data created in one version of the Azure Cosmos DB Emulator is not guaranteed to be accessible when using a different version.</span></span> <span data-ttu-id="cd92b-171">Als u nodig hebt om uw gegevens voor de lange termijn, verdient het aanbeveling om op te slaan die gegevens in een Azure DB die Cosmos-account, in plaats van de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-171">If you need to persist your data for the long term, it is recommended that you store that data in an Azure Cosmos DB account, rather than in the Azure Cosmos DB Emulator.</span></span> 

## <a name="authenticating-requests"></a><span data-ttu-id="cd92b-172">Verificatie van aanvragen</span><span class="sxs-lookup"><span data-stu-id="cd92b-172">Authenticating requests</span></span>
<span data-ttu-id="cd92b-173">Net zoals met Azure Cosmos DB in de cloud, moet elke aanvraag die u op basis van de Azure-Emulator Cosmos DB maakt worden geverifieerd.</span><span class="sxs-lookup"><span data-stu-id="cd92b-173">Just as with Azure Cosmos DB in the cloud, every request that you make against the Azure Cosmos DB Emulator must be authenticated.</span></span> <span data-ttu-id="cd92b-174">De Azure-Emulator Cosmos DB ondersteunt één vaste account en een bekende verificatiesleutel voor de verificatie van de hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="cd92b-174">The Azure Cosmos DB Emulator supports a single fixed account and a well-known authentication key for master key authentication.</span></span> <span data-ttu-id="cd92b-175">Dit account en de sleutel zijn de enige referenties zijn toegestaan voor gebruik met de Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-175">This account and key are the only credentials permitted for use with the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="cd92b-176">Ze zijn:</span><span class="sxs-lookup"><span data-stu-id="cd92b-176">They are:</span></span>

    Account name: localhost:<port>
    Account key: C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==

> [!NOTE]
> <span data-ttu-id="cd92b-177">De hoofdsleutel ondersteund door de Azure Cosmos DB-Emulator is bedoeld voor gebruik met de emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-177">The master key supported by the Azure Cosmos DB Emulator is intended for use only with the emulator.</span></span> <span data-ttu-id="cd92b-178">U kunt uw Azure DB die Cosmos-account voor productie en de sleutel niet gebruiken met de Azure Cosmos DB-Emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-178">You cannot use your production Azure Cosmos DB account and key with the Azure Cosmos DB Emulator.</span></span> 

> [!NOTE] 
> <span data-ttu-id="cd92b-179">Als u de emulator hebt gestart met de optie/Key, gebruikt u de gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "</span><span class="sxs-lookup"><span data-stu-id="cd92b-179">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="cd92b-180">Bovendien, net als de service Azure Cosmos DB de Emulator Azure Cosmos-database ondersteunt alleen beveiligde communicatie via SSL.</span><span class="sxs-lookup"><span data-stu-id="cd92b-180">Additionally, just as the Azure Cosmos DB service, the Azure Cosmos DB Emulator supports only secure communication via SSL.</span></span>

## <a name="running-the-emulator-on-a-local-network"></a><span data-ttu-id="cd92b-181">De emulator uitgevoerd op een lokaal netwerk</span><span class="sxs-lookup"><span data-stu-id="cd92b-181">Running the emulator on a local network</span></span>

<span data-ttu-id="cd92b-182">U kunt de emulator uitvoeren op een lokaal netwerk.</span><span class="sxs-lookup"><span data-stu-id="cd92b-182">You can run the emulator on a local network.</span></span> <span data-ttu-id="cd92b-183">Geef de optie /AllowNetworkAccess op zodat de toegang tot het netwerk de [opdrachtregel](#command-line-syntax), die ook vereisen dat u / Key opgeeft = key_string of/KeyFile = bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="cd92b-183">To enable network access, specify the /AllowNetworkAccess option at the [command line](#command-line-syntax), which also requires that you specify /Key=key_string or /KeyFile=file_name.</span></span> <span data-ttu-id="cd92b-184">U kunt /GenKeyFile = bestandsnaam voor het genereren van een bestand met een willekeurige sleutel tevoren betaalt.</span><span class="sxs-lookup"><span data-stu-id="cd92b-184">You can use /GenKeyFile=file_name to generate a file with a random key upfront.</span></span>  <span data-ttu-id="cd92b-185">Vervolgens u doorgeven kunt dat naar/KeyFile = bestandsnaam of/Key = contents_of_file.</span><span class="sxs-lookup"><span data-stu-id="cd92b-185">Then you can pass that to /KeyFile=file_name or /Key=contents_of_file.</span></span>

<span data-ttu-id="cd92b-186">Toegang tot het netwerk voor het eerst inschakelen wordt de gebruiker moet de emulator afsluiten en verwijderen van de emulator gegevensmap (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span><span class="sxs-lookup"><span data-stu-id="cd92b-186">To enable network access for the first time the user should shutdown the emulator and delete the emulator’s data directory (C:\Users\user_name\AppData\Local\CosmosDBEmulator).</span></span>

## <a name="developing-with-the-emulator"></a><span data-ttu-id="cd92b-187">Ontwikkelen met de Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-187">Developing with the Emulator</span></span>
<span data-ttu-id="cd92b-188">Zodra u de Azure Cosmos DB-Emulator uitgevoerd op uw bureaublad hebt, kunt u elke ondersteunde [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) of de [REST-API van Azure Cosmos DB](/rest/api/documentdb/) om te communiceren met de Emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-188">Once you have the Azure Cosmos DB Emulator running on your desktop, you can use any supported [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md) or the [Azure Cosmos DB REST API](/rest/api/documentdb/) to interact with the Emulator.</span></span> <span data-ttu-id="cd92b-189">De Azure-Emulator Cosmos DB tevens een ingebouwde Data Explorer waarmee u verzamelingen voor de DocumentDB en MongoDB APIs en weergave maken en bewerken van documenten zonder een code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="cd92b-189">The Azure Cosmos DB Emulator also includes a built-in Data Explorer that lets you create collections for the DocumentDB and MongoDB APIs, and view and edit documents without writing any code.</span></span>   

    // Connect to the Azure Cosmos DB Emulator running locally
    DocumentClient client = new DocumentClient(
        new Uri("https://localhost:8081"), 
        "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==");

<span data-ttu-id="cd92b-190">Als u [Azure Cosmos DB protocolondersteuning voor MongoDB](mongodb-introduction.md), gebruik de volgende verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="cd92b-190">If you're using [Azure Cosmos DB protocol support for MongoDB](mongodb-introduction.md), please use the following connection string:</span></span>

    mongodb://localhost:C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==@localhost:10255/admin?ssl=true&3t.sslSelfSignedCerts=true

<span data-ttu-id="cd92b-191">U kunt bestaande hulpprogramma's zoals [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) verbinding maken met de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-191">You can use existing tools like [Azure DocumentDB Studio](https://github.com/mingaliu/DocumentDBStudio) to connect to the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="cd92b-192">U kunt ook migreren van gegevens tussen de Azure-Emulator Cosmos DB en het gebruik van Azure DB die Cosmos service de [Azure Cosmos DB hulpprogramma voor gegevensmigratie](https://github.com/azure/azure-documentdb-datamigrationtool).</span><span class="sxs-lookup"><span data-stu-id="cd92b-192">You can also migrate data between the Azure Cosmos DB Emulator and the Azure Cosmos DB service using the [Azure Cosmos DB Data Migration Tool](https://github.com/azure/azure-documentdb-datamigrationtool).</span></span>

> [!NOTE] 
> <span data-ttu-id="cd92b-193">Als u de emulator hebt gestart met de optie/Key, gebruikt u de gegenereerde sleutel in plaats van ' C2y6yDjf5/R + ob0N8A7Cgv30VRDJIWEHLM + 4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw == "</span><span class="sxs-lookup"><span data-stu-id="cd92b-193">If you have started the emulator with the /Key option, then use the generated key instead of "C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw=="</span></span>

<span data-ttu-id="cd92b-194">Met behulp van de emulator Azure Cosmos DB standaard, kunt u maximaal 25 verzamelingen met één partitie of 1 gepartitioneerde verzameling.</span><span class="sxs-lookup"><span data-stu-id="cd92b-194">Using the Azure Cosmos DB emulator, by default, you can create up to 25 single partition collections or 1 partitioned collection.</span></span> <span data-ttu-id="cd92b-195">Zie voor meer informatie over het wijzigen van deze waarde [PartitionCount waarde](#set-partitioncount).</span><span class="sxs-lookup"><span data-stu-id="cd92b-195">For more information about changing this value, see [Setting the PartitionCount value](#set-partitioncount).</span></span>

## <a name="export-the-ssl-certificate"></a><span data-ttu-id="cd92b-196">Het SSL-certificaat exporteren</span><span class="sxs-lookup"><span data-stu-id="cd92b-196">Export the SSL certificate</span></span>

<span data-ttu-id="cd92b-197">.NET-talen en runtime gebruik van de Windows-certificaatarchief veilig verbinding te maken met de lokale Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-197">.NET languages and runtime use the Windows Certificate Store to securely connect to the Azure Cosmos DB local emulator.</span></span> <span data-ttu-id="cd92b-198">Andere talen hebben hun eigen methode voor het beheren en gebruiken van certificaten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-198">Other languages have their own method of managing and using certificates.</span></span> <span data-ttu-id="cd92b-199">Java maakt gebruik van een eigen [certificaatarchief](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) dat gebruikmaakt van Python [socket wrappers](https://docs.python.org/2/library/ssl.html).</span><span class="sxs-lookup"><span data-stu-id="cd92b-199">Java uses its own [certificate store](https://docs.oracle.com/cd/E19830-01/819-4712/ablqw/index.html) whereas Python uses [socket wrappers](https://docs.python.org/2/library/ssl.html).</span></span>

<span data-ttu-id="cd92b-200">U wilt exporteren met behulp van de certificaatbeheerder Windows ter verkrijging van een certificaat wilt gebruiken met talen en runtimes die niet worden geïntegreerd in het certificaatarchief van Windows.</span><span class="sxs-lookup"><span data-stu-id="cd92b-200">In order to obtain a certificate to use with languages and runtimes that do not integrate with the Windows Certificate Store you will need to export it using the Windows Certificate Manager.</span></span> <span data-ttu-id="cd92b-201">U kunt starten door certlm.msc uitgevoerd of de stapsgewijze instructies in [exporteert u het certificaat Azure Cosmos DB Emulator](./local-emulator-export-ssl-certificates.md).</span><span class="sxs-lookup"><span data-stu-id="cd92b-201">You can start it by running certlm.msc or follow the step by step instructions in [Export the Azure Cosmos DB Emulator Certificates](./local-emulator-export-ssl-certificates.md).</span></span> <span data-ttu-id="cd92b-202">Zodra de certificate manager wordt uitgevoerd, opent u de persoonlijke certificaten zoals hieronder wordt weergegeven en exporteer het certificaat met de beschrijvende naam 'DocumentDBEmulatorCertificate' als een BASE-64 X.509 (.cer)-bestand gecodeerde.</span><span class="sxs-lookup"><span data-stu-id="cd92b-202">Once the certificate manager is running, open the Personal Certificates as shown below and export the certificate with the friendly name "DocumentDBEmulatorCertificate" as a BASE-64 encoded X.509 (.cer) file.</span></span>

![Azure DB Cosmos lokale emulator SSL-certificaat](./media/local-emulator/database-local-emulator-ssl_certificate.png)

<span data-ttu-id="cd92b-204">Het X.509-certificaat kan worden geïmporteerd in het certificaatarchief Java door de instructies in [een certificaat toevoegen aan de Java CA certificatenarchief](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span><span class="sxs-lookup"><span data-stu-id="cd92b-204">The X.509 certificate can be imported into the Java certificate store by following the instructions in [Adding a Certificate to the Java CA Certificates Store](https://docs.microsoft.com/azure/java-add-certificate-ca-store).</span></span> <span data-ttu-id="cd92b-205">Zodra het certificaat wordt geïmporteerd in het certificaatarchief, Java en de MongoDB-toepassingen worden verbinding kunnen maken met de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-205">Once the certificate is imported into the certificate store, Java and MongoDB applications will be able to connect to the Azure Cosmos DB Emulator.</span></span>

<span data-ttu-id="cd92b-206">Bij het verbinden met de emulator van Python en Node.js-SDK's, is SSL-verificatie uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cd92b-206">When connecting to the emulator from Python and Node.js SDKs, SSL verification is disabled.</span></span>

## <span data-ttu-id="cd92b-207"><a id="command-line"></a>Opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="cd92b-207"><a id="command-line"></a>Command-line tool reference</span></span>
<span data-ttu-id="cd92b-208">Vanaf de installatielocatie, kunt u de opdrachtregel om te starten en stoppen van de emulator, opties configureren en andere bewerkingen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cd92b-208">From the installation location, you can use the command-line to start and stop the emulator, configure options, and perform other operations.</span></span>

### <a name="command-line-syntax"></a><span data-ttu-id="cd92b-209">De syntaxis van opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="cd92b-209">Command-line Syntax</span></span>

    CosmosDB.Emulator.exe [/Shutdown] [/DataPath] [/Port] [/MongoPort] [/DirectPorts] [/Key] [/EnableRateLimiting] [/DisableRateLimiting] [/NoUI] [/NoExplorer] [/?]

<span data-ttu-id="cd92b-210">Als u wilt weergeven in de lijst met opties, typt u `CosmosDB.Emulator.exe /?` bij de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="cd92b-210">To view the list of options, type `CosmosDB.Emulator.exe /?` at the command prompt.</span></span>

<table>
<tr>
  <td><span data-ttu-id="cd92b-211"><strong>Optie</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-211"><strong>Option</strong></span></span></td>
  <td><span data-ttu-id="cd92b-212"><strong>Beschrijving</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-212"><strong>Description</strong></span></span></td>
  <td><span data-ttu-id="cd92b-213"><strong>Opdracht</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-213"><strong>Command</strong></span></span></td>
  <td><span data-ttu-id="cd92b-214"><strong>Argumenten</strong></span><span class="sxs-lookup"><span data-stu-id="cd92b-214"><strong>Arguments</strong></span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-215">[Geen argumenten]</span><span class="sxs-lookup"><span data-stu-id="cd92b-215">[No arguments]</span></span></td>
  <td><span data-ttu-id="cd92b-216">De Azure-Emulator Cosmos DB met standaardinstellingen wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="cd92b-216">Starts up the Azure Cosmos DB Emulator with default settings.</span></span></td>
  <td><span data-ttu-id="cd92b-217">CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="cd92b-217">CosmosDB.Emulator.exe</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-218">[Help]</span><span class="sxs-lookup"><span data-stu-id="cd92b-218">[Help]</span></span></td>
  <td><span data-ttu-id="cd92b-219">Geeft de lijst met ondersteunde opdrachtregelargumenten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-219">Displays the list of supported command-line arguments.</span></span></td>
  <td><span data-ttu-id="cd92b-220">CosmosDB.Emulator.exe /?</span><span class="sxs-lookup"><span data-stu-id="cd92b-220">CosmosDB.Emulator.exe /?</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-221">afsluiten</span><span class="sxs-lookup"><span data-stu-id="cd92b-221">Shutdown</span></span></td>
  <td><span data-ttu-id="cd92b-222">De Azure Cosmos DB-Emulator wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-222">Shuts down the Azure Cosmos DB Emulator.</span></span></td>
  <td><span data-ttu-id="cd92b-223">CosmosDB.Emulator.exe/Shutdown</span><span class="sxs-lookup"><span data-stu-id="cd92b-223">CosmosDB.Emulator.exe /Shutdown</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-224">Gegevenspad</span><span class="sxs-lookup"><span data-stu-id="cd92b-224">DataPath</span></span></td>
  <td><span data-ttu-id="cd92b-225">Hiermee geeft u het pad waarin de gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-225">Specifies the path in which to store data files.</span></span> <span data-ttu-id="cd92b-226">Standaard is % LocalAppdata%\CosmosDBEmulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-226">Default is %LocalAppdata%\CosmosDBEmulator.</span></span></td>
  <td><span data-ttu-id="cd92b-227">CosmosDB.Emulator.exe /DataPath =&lt;gegevenspad&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-227">CosmosDB.Emulator.exe /DataPath=&lt;datapath&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-228">&lt;gegevenspad&gt;: een toegankelijk pad</span><span class="sxs-lookup"><span data-stu-id="cd92b-228">&lt;datapath&gt;: An accessible path</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-229">Poort</span><span class="sxs-lookup"><span data-stu-id="cd92b-229">Port</span></span></td>
  <td><span data-ttu-id="cd92b-230">Hiermee geeft u het poortnummer dat moet worden gebruikt voor de emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-230">Specifies the port number to use for the emulator.</span></span>  <span data-ttu-id="cd92b-231">De standaardwaarde is 8081.</span><span class="sxs-lookup"><span data-stu-id="cd92b-231">Default is 8081.</span></span></td>
  <td><span data-ttu-id="cd92b-232">CosmosDB.Emulator.exe/Port =&lt;poort&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-232">CosmosDB.Emulator.exe /Port=&lt;port&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-233">&lt;poort&gt;: poortnummer</span><span class="sxs-lookup"><span data-stu-id="cd92b-233">&lt;port&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-234">MongoPort</span><span class="sxs-lookup"><span data-stu-id="cd92b-234">MongoPort</span></span></td>
  <td><span data-ttu-id="cd92b-235">Hiermee geeft u het poortnummer dat moet worden gebruikt voor compatibiliteit met MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="cd92b-235">Specifies the port number to use for MongoDB compatibility API.</span></span> <span data-ttu-id="cd92b-236">De standaardwaarde is 10255.</span><span class="sxs-lookup"><span data-stu-id="cd92b-236">Default is 10255.</span></span></td>
  <td><span data-ttu-id="cd92b-237">CosmosDB.Emulator.exe /MongoPort =&lt;mongoport&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-237">CosmosDB.Emulator.exe /MongoPort=&lt;mongoport&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-238">&lt;mongoport&gt;: poortnummer</span><span class="sxs-lookup"><span data-stu-id="cd92b-238">&lt;mongoport&gt;: Single port number</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-239">DirectPorts</span><span class="sxs-lookup"><span data-stu-id="cd92b-239">DirectPorts</span></span></td>
  <td><span data-ttu-id="cd92b-240">Hiermee geeft u de poorten te gebruiken voor rechtstreekse connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="cd92b-240">Specifies the ports to use for direct connectivity.</span></span> <span data-ttu-id="cd92b-241">Standaardwaarden zijn 10251,10252,10253,10254.</span><span class="sxs-lookup"><span data-stu-id="cd92b-241">Defaults are 10251,10252,10253,10254.</span></span></td>
  <td><span data-ttu-id="cd92b-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-242">CosmosDB.Emulator.exe /DirectPorts:&lt;directports&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-243">&lt;directports&gt;: door komma's gescheiden lijst met 4 poorten</span><span class="sxs-lookup"><span data-stu-id="cd92b-243">&lt;directports&gt;: Comma-delimited list of 4 ports</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-244">Sleutel</span><span class="sxs-lookup"><span data-stu-id="cd92b-244">Key</span></span></td>
  <td><span data-ttu-id="cd92b-245">De autorisatiesleutel voor de emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-245">Authorization key for the emulator.</span></span> <span data-ttu-id="cd92b-246">Sleutel moet de base 64-codering van een 64-byte-vector.</span><span class="sxs-lookup"><span data-stu-id="cd92b-246">Key must be the base-64 encoding of a 64-byte vector.</span></span></td>
  <td><span data-ttu-id="cd92b-247">CosmosDB.Emulator.exe/key:&lt;sleutel&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-247">CosmosDB.Emulator.exe /Key:&lt;key&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-248">&lt;sleutel&gt;: sleutel moet de base 64-codering van een 64-byte-vector</span><span class="sxs-lookup"><span data-stu-id="cd92b-248">&lt;key&gt;: Key must be the base-64 encoding of a 64-byte vector</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-249">EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="cd92b-249">EnableRateLimiting</span></span></td>
  <td><span data-ttu-id="cd92b-250">Hiermee geeft u op deze aanvraag snelheidsbeperking gedrag is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cd92b-250">Specifies that request rate limiting behavior is enabled.</span></span></td>
  <td><span data-ttu-id="cd92b-251">CosmosDB.Emulator.exe /EnableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="cd92b-251">CosmosDB.Emulator.exe /EnableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-252">DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="cd92b-252">DisableRateLimiting</span></span></td>
  <td><span data-ttu-id="cd92b-253">Hiermee geeft u op deze aanvraag snelheidsbeperking gedrag is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cd92b-253">Specifies that request rate limiting behavior is disabled.</span></span></td>
  <td><span data-ttu-id="cd92b-254">CosmosDB.Emulator.exe /DisableRateLimiting</span><span class="sxs-lookup"><span data-stu-id="cd92b-254">CosmosDB.Emulator.exe /DisableRateLimiting</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-255">NoUI</span><span class="sxs-lookup"><span data-stu-id="cd92b-255">NoUI</span></span></td>
  <td><span data-ttu-id="cd92b-256">Worden de emulator gebruikersinterface niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cd92b-256">Do not show the emulator user interface.</span></span></td>
  <td><span data-ttu-id="cd92b-257">/ Noui CosmosDB.Emulator.exe</span><span class="sxs-lookup"><span data-stu-id="cd92b-257">CosmosDB.Emulator.exe /NoUI</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-258">NoExplorer</span><span class="sxs-lookup"><span data-stu-id="cd92b-258">NoExplorer</span></span></td>
  <td><span data-ttu-id="cd92b-259">Geen documentverkenner weergeven bij het opstarten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-259">Don't show document explorer on startup.</span></span></td>
  <td><span data-ttu-id="cd92b-260">CosmosDB.Emulator.exe /NoExplorer</span><span class="sxs-lookup"><span data-stu-id="cd92b-260">CosmosDB.Emulator.exe /NoExplorer</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-261">PartitionCount</span><span class="sxs-lookup"><span data-stu-id="cd92b-261">PartitionCount</span></span></td>
  <td><span data-ttu-id="cd92b-262">Hiermee geeft u het maximum aantal gepartitioneerde verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-262">Specifies the maximum number of partitioned collections.</span></span> <span data-ttu-id="cd92b-263">Zie [wijzigen van het aantal verzamelingen](#set-partitioncount) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cd92b-263">See [Change the number of collections](#set-partitioncount) for more information.</span></span></td>
  <td><span data-ttu-id="cd92b-264">CosmosDB.Emulator.exe /PartitionCount =&lt;partitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-264">CosmosDB.Emulator.exe /PartitionCount=&lt;partitioncount&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-265">&lt;partitioncount&gt;: het maximale aantal toegestane verzamelingen met één partitie.</span><span class="sxs-lookup"><span data-stu-id="cd92b-265">&lt;partitioncount&gt;: Maximum number of allowed single partition collections.</span></span> <span data-ttu-id="cd92b-266">Standaardwaarde is 25.</span><span class="sxs-lookup"><span data-stu-id="cd92b-266">Default is 25.</span></span> <span data-ttu-id="cd92b-267">Maximaal toegestane aantal is 250.</span><span class="sxs-lookup"><span data-stu-id="cd92b-267">Maximum allowed is 250.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-268">DefaultPartitionCount</span><span class="sxs-lookup"><span data-stu-id="cd92b-268">DefaultPartitionCount</span></span></td>
  <td><span data-ttu-id="cd92b-269">Hiermee geeft u het aantal partities voor een gepartitioneerde verzameling.</span><span class="sxs-lookup"><span data-stu-id="cd92b-269">Specifies the default number of partitions for a partitioned collection.</span></span></td>
  <td><span data-ttu-id="cd92b-270">CosmosDB.Emulator.exe /DefaultPartitionCount =&lt;defaultpartitioncount&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-270">CosmosDB.Emulator.exe /DefaultPartitionCount=&lt;defaultpartitioncount&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-271">&lt;defaultpartitioncount&gt; standaardwaarde is 25.</span><span class="sxs-lookup"><span data-stu-id="cd92b-271">&lt;defaultpartitioncount&gt; Default is 25.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-272">AllowNetworkAccess</span><span class="sxs-lookup"><span data-stu-id="cd92b-272">AllowNetworkAccess</span></span></td>
  <td><span data-ttu-id="cd92b-273">Geeft toegang tot de emulator via een netwerk.</span><span class="sxs-lookup"><span data-stu-id="cd92b-273">Enables access to the emulator over a network.</span></span> <span data-ttu-id="cd92b-274">U moet ook doorgeven/Key =&lt;key_string&gt; of/KeyFile =&lt;bestandsnaam&gt; waarmee toegang tot het netwerk.</span><span class="sxs-lookup"><span data-stu-id="cd92b-274">You must also pass /Key=&lt;key_string&gt; or /KeyFile=&lt;file_name&gt; to enable network access.</span></span></td>
  <td><span data-ttu-id="cd92b-275">CosmosDB.Emulator.exe AllowNetworkAccess /Key =&lt;key_string&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-275">CosmosDB.Emulator.exe /AllowNetworkAccess /Key=&lt;key_string&gt;</span></span><br><br><span data-ttu-id="cd92b-276">of</span><span class="sxs-lookup"><span data-stu-id="cd92b-276">or</span></span><br><br><span data-ttu-id="cd92b-277">CosmosDB.Emulator.exe /AllowNetworkAccess/KeyFile =&lt;bestandsnaam&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-277">CosmosDB.Emulator.exe /AllowNetworkAccess /KeyFile=&lt;file_name&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-278">NoFirewall</span><span class="sxs-lookup"><span data-stu-id="cd92b-278">NoFirewall</span></span></td>
  <td><span data-ttu-id="cd92b-279">Firewall-regels niet worden aangepast wanneer /AllowNetworkAccess wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cd92b-279">Don't adjust firewall rules when /AllowNetworkAccess is used.</span></span></td>
  <td><span data-ttu-id="cd92b-280">CosmosDB.Emulator.exe /NoFirewall</span><span class="sxs-lookup"><span data-stu-id="cd92b-280">CosmosDB.Emulator.exe /NoFirewall</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-281">GenKeyFile</span><span class="sxs-lookup"><span data-stu-id="cd92b-281">GenKeyFile</span></span></td>
  <td><span data-ttu-id="cd92b-282">Een nieuwe autorisatiesleutel genereren en opslaan in het opgegeven bestand.</span><span class="sxs-lookup"><span data-stu-id="cd92b-282">Generate a new authorization key and save to the specified file.</span></span> <span data-ttu-id="cd92b-283">De gegenereerde sleutel kan worden gebruikt met de opties/Key of/KeyFile.</span><span class="sxs-lookup"><span data-stu-id="cd92b-283">The generated key can be used with the /Key or /KeyFile options.</span></span></td>
  <td><span data-ttu-id="cd92b-284">CosmosDB.Emulator.exe /GenKeyFile =&lt;pad naar het sleutelbestand&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-284">CosmosDB.Emulator.exe  /GenKeyFile=&lt;path to key file&gt;</span></span></td>
  <td></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-285">Consistentie</span><span class="sxs-lookup"><span data-stu-id="cd92b-285">Consistency</span></span></td>
  <td><span data-ttu-id="cd92b-286">Stel het standaardniveau voor consistentie voor het account.</span><span class="sxs-lookup"><span data-stu-id="cd92b-286">Set the default consistency level for the account.</span></span></td>
  <td><span data-ttu-id="cd92b-287">CosmosDB.Emulator.exe /Consistency =&lt;consistentie&gt;</span><span class="sxs-lookup"><span data-stu-id="cd92b-287">CosmosDB.Emulator.exe /Consistency=&lt;consistency&gt;</span></span></td>
  <td><span data-ttu-id="cd92b-288">&lt;consistentie&gt;: waarde moet een van de volgende [consistentieniveaus](consistency-levels.md): sessie, sterke, Eventual of BoundedStaleness.</span><span class="sxs-lookup"><span data-stu-id="cd92b-288">&lt;consistency&gt;: Value must be one of the following [consistency levels](consistency-levels.md): Session, Strong, Eventual, or BoundedStaleness.</span></span>  <span data-ttu-id="cd92b-289">De standaardwaarde is de sessie.</span><span class="sxs-lookup"><span data-stu-id="cd92b-289">The default value is Session.</span></span></td>
</tr>
<tr>
  <td><span data-ttu-id="cd92b-290">?</span><span class="sxs-lookup"><span data-stu-id="cd92b-290">?</span></span></td>
  <td><span data-ttu-id="cd92b-291">De helpbericht weergeven.</span><span class="sxs-lookup"><span data-stu-id="cd92b-291">Show the help message.</span></span></td>
  <td></td>
  <td></td>
</tr>
</table>

## <a name="differences-between-the-azure-cosmos-db-emulator-and-azure-cosmos-db"></a><span data-ttu-id="cd92b-292">Verschillen tussen de Azure Cosmos DB-Emulator en Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="cd92b-292">Differences between the Azure Cosmos DB Emulator and Azure Cosmos DB</span></span> 
<span data-ttu-id="cd92b-293">Omdat de Azure-Emulator Cosmos DB een geëmuleerde omgeving uitgevoerd op een lokale developer-werkstation biedt, zijn er enkele verschillen in functionaliteit tussen de emulator en een Cosmos-DB Azure-account in de cloud:</span><span class="sxs-lookup"><span data-stu-id="cd92b-293">Because the Azure Cosmos DB Emulator provides an emulated environment running on a local developer workstation, there are some differences in functionality between the emulator and an Azure Cosmos DB account in the cloud:</span></span>

* <span data-ttu-id="cd92b-294">De Azure-Emulator Cosmos DB ondersteunt slechts één vaste account en een bekende hoofdsleutel.</span><span class="sxs-lookup"><span data-stu-id="cd92b-294">The Azure Cosmos DB Emulator supports only a single fixed account and a well-known master key.</span></span>  <span data-ttu-id="cd92b-295">Toegangssleutel wordt opnieuw gegenereerd, is niet mogelijk in de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-295">Key regeneration is not possible in the Azure Cosmos DB Emulator.</span></span>
* <span data-ttu-id="cd92b-296">De Azure-Emulator Cosmos-database is niet een schaalbare service en wordt geen ondersteuning voor een groot aantal verzamelingen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-296">The Azure Cosmos DB Emulator is not a scalable service and will not support a large number of collections.</span></span>
* <span data-ttu-id="cd92b-297">De Azure-Emulator Cosmos DB komt niet simuleren verschillende [Azure Cosmos DB consistentieniveaus](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="cd92b-297">The Azure Cosmos DB Emulator does not simulate different [Azure Cosmos DB consistency levels](consistency-levels.md).</span></span>
* <span data-ttu-id="cd92b-298">De Azure-Emulator Cosmos DB komt niet simuleren [meerdere landen/regio replicatie](distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="cd92b-298">The Azure Cosmos DB Emulator does not simulate [multi-region replication](distribute-data-globally.md).</span></span>
* <span data-ttu-id="cd92b-299">De Azure-Emulator Cosmos DB biedt geen ondersteuning voor de service quotum onderdrukkingen die beschikbaar in de Azure DB die Cosmos-service (bijvoorbeeld de maximale grootte document, verbeterde gepartitioneerde verzameling opslag zijn).</span><span class="sxs-lookup"><span data-stu-id="cd92b-299">The Azure Cosmos DB Emulator does not support the service quota overrides that are available in the Azure Cosmos DB service (e.g. document size limits, increased partitioned collection storage).</span></span>
* <span data-ttu-id="cd92b-300">Als uw exemplaar van de Azure Cosmos DB-Emulator zijn mogelijk niet bijgewerkt met de meest recente wijzigingen met de service Azure Cosmos DB, neemt u [Azure DB die Cosmos-Capaciteitsplanner](https://www.documentdb.com/capacityplanner) nauwkeurig te schatten productie doorvoer (RUs) behoeften van uw de toepassing.</span><span class="sxs-lookup"><span data-stu-id="cd92b-300">As your copy of the Azure Cosmos DB Emulator might not be up to date with the most recent changes with the Azure Cosmos DB service, please [Azure Cosmos DB capacity planner](https://www.documentdb.com/capacityplanner) to accurately estimate production throughput (RUs) needs of your application.</span></span>

## <span data-ttu-id="cd92b-301"><a id="set-partitioncount"></a>Het aantal verzamelingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="cd92b-301"><a id="set-partitioncount"></a>Change the number of collections</span></span>

<span data-ttu-id="cd92b-302">Standaard kunt u maximaal 25 verzamelingen met één partitie of 1 gepartitioneerde verzameling op basis van de Azure-Emulator Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cd92b-302">By default, you can create up to 25 single partition collections, or 1 partitioned collection using the Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="cd92b-303">Doordat de **PartitionCount** waarde, kunt u maximaal 250 verzamelingen met één partitie of 10 gepartitioneerde verzamelingen of een combinatie van de twee die niet meer dan 250 één partities (waar 1 verzameling gepartitioneerd = 25 één partitie verzameling).</span><span class="sxs-lookup"><span data-stu-id="cd92b-303">By modifying the **PartitionCount** value, you can create up to 250 single partition collections or 10 partitioned collections, or any combination of the two that does not exceed 250 single partitions (where 1 partitioned collection = 25 single partition collection).</span></span>

<span data-ttu-id="cd92b-304">Als u probeert een verzameling maken nadat het huidige aantal partities is overschreden, genereert de emulator een uitzondering ServiceUnavailable met het volgende bericht.</span><span class="sxs-lookup"><span data-stu-id="cd92b-304">If you attempt to create a collection after the current partition count has been exceeded, the emulator throws a ServiceUnavailable exception, with the following message.</span></span>

    Sorry, we are currently experiencing high demand in this region, 
    and cannot fulfill your request at this time. We work continuously 
    to bring more and more capacity online, and encourage you to try again. 
    Please do not hesitate to email docdbswat@microsoft.com at any time or 
    for any reason. ActivityId: 29da65cc-fba1-45f9-b82c-bf01d78a1f91

<span data-ttu-id="cd92b-305">Als u het aantal beschikbare verzamelingen wilt de Emulator Azure Cosmos DB, het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="cd92b-305">To change the number of collections available to the Azure Cosmos DB Emulator, do the following:</span></span>

1. <span data-ttu-id="cd92b-306">Alle lokale Azure Cosmos DB Emulator gegevens verwijderen met de rechtermuisknop op de **Azure Cosmos DB Emulator** pictogram op de taakbalk en vervolgens klikken op **gegevens opnieuw instellen...** .</span><span class="sxs-lookup"><span data-stu-id="cd92b-306">Delete all local Azure Cosmos DB Emulator data by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Reset Data…**.</span></span>
2. <span data-ttu-id="cd92b-307">Alle gegevens van de emulator in deze map C:\Users\user_name\AppData\Local\CosmosDBEmulator verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-307">Delete all emulator data in this folder C:\Users\user_name\AppData\Local\CosmosDBEmulator.</span></span>
3. <span data-ttu-id="cd92b-308">Sluit alle geopende exemplaren met de rechtermuisknop op de **Azure Cosmos DB Emulator** pictogram op de taakbalk en vervolgens klikken op **afsluiten**.</span><span class="sxs-lookup"><span data-stu-id="cd92b-308">Exit all open instances by right-clicking the **Azure Cosmos DB Emulator** icon on the system tray, and then clicking **Exit**.</span></span> <span data-ttu-id="cd92b-309">Het duurt een paar minuten voor alle exemplaren om af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-309">It may take a minute for all instances to exit.</span></span>
4. <span data-ttu-id="cd92b-310">Installeer de nieuwste versie van de [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span><span class="sxs-lookup"><span data-stu-id="cd92b-310">Install the latest version of the [Azure Cosmos DB Emulator](https://aka.ms/cosmosdb-emulator).</span></span>
5. <span data-ttu-id="cd92b-311">Start de emulator met de vlag PartitionCount door een waarde < = 250.</span><span class="sxs-lookup"><span data-stu-id="cd92b-311">Launch the emulator with the PartitionCount flag by setting a value <= 250.</span></span> <span data-ttu-id="cd92b-312">Bijvoorbeeld: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span><span class="sxs-lookup"><span data-stu-id="cd92b-312">For example: `C:\Program Files\Azure CosmosDB Emulator>CosmosDB.Emulator.exe /PartitionCount=100`.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cd92b-313">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cd92b-313">Troubleshooting</span></span>

<span data-ttu-id="cd92b-314">Gebruik de volgende tips voor het oplossen van problemen die u met de Azure DB die Cosmos-emulator tegenkomt:</span><span class="sxs-lookup"><span data-stu-id="cd92b-314">Use the following tips to help troubleshoot issues you encounter with the Azure Cosmos DB emulator:</span></span>

- <span data-ttu-id="cd92b-315">Als u een nieuwe versie van de Emulator is geïnstalleerd en worden er fouten optreden, zorg ervoor dat u uw gegevens herstellen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-315">If you installed a new version of the Emulator and are experiencing errors, ensure you reset your data.</span></span> <span data-ttu-id="cd92b-316">U kunt uw gegevens herstellen door met de rechtermuisknop op het pictogram Azure Cosmos DB Emulator op de taakbalk en vervolgens te klikken op de gegevens opnieuw instellen...</span><span class="sxs-lookup"><span data-stu-id="cd92b-316">You can reset your data by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Reset Data….</span></span> <span data-ttu-id="cd92b-317">Als de fouten die niet wordt opgelost, kunt u deze kunt verwijderen en opnieuw installeren van de app.</span><span class="sxs-lookup"><span data-stu-id="cd92b-317">If that does not fix the errors, you can uninstall and reinstall the app.</span></span> <span data-ttu-id="cd92b-318">Zie [verwijderen van de lokale emulator](#uninstall) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="cd92b-318">See [Uninstall the local emulator](#uninstall) for instructions.</span></span>

- <span data-ttu-id="cd92b-319">Als de Azure DB die Cosmos-emulator vastloopt, verzamelen van dumpbestanden vanuit de map c:\Users\user_name\AppData\Local\CrashDumps, deze comprimeren en deze koppelt aan een e-mail naar [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cd92b-319">If the Azure Cosmos DB emulator crashes, collect dump files from c:\Users\user_name\AppData\Local\CrashDumps folder, compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="cd92b-320">Als u crashes ondervindt in CosmosDB.StartupEntryPoint.exe, kunt u de volgende opdracht uitvoeren vanaf een opdrachtprompt beheerder:`lodctr /R`</span><span class="sxs-lookup"><span data-stu-id="cd92b-320">If you experience crashes in CosmosDB.StartupEntryPoint.exe, run the following command from an admin command prompt: `lodctr /R`</span></span> 

- <span data-ttu-id="cd92b-321">Als u een verbindingsprobleem ondervindt [verzamelen traceringsbestanden](#trace-files), deze comprimeren en deze koppelt aan een e-mail naar [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="cd92b-321">If you encounter a connectivity issue, [collect trace files](#trace-files), compress them, and attach them to an email to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com).</span></span>

- <span data-ttu-id="cd92b-322">Als u krijgt een **Service niet beschikbaar** bericht, de emulator mogelijk mislukken de netwerkstack initialiseren.</span><span class="sxs-lookup"><span data-stu-id="cd92b-322">If you receive a **Service Unavailable** message, the emulator might be failing to initialize the network stack.</span></span> <span data-ttu-id="cd92b-323">Controleer of er de beveiligde client Pulse of Juniper netwerken client is geïnstalleerd, zoals netwerk filterstuurprogramma ertoe leiden het probleem dat kunnen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-323">Check to see if you have the Pulse secure client or Juniper networks client installed, as their network filter drivers may cause the problem.</span></span> <span data-ttu-id="cd92b-324">Verwijderen van stuurprogramma's van derden netwerk filter doorgaans wordt het probleem opgelost.</span><span class="sxs-lookup"><span data-stu-id="cd92b-324">Uninstalling third party network filter drivers typically fixes the issue.</span></span>

### <span data-ttu-id="cd92b-325"><a id="trace-files"></a>Traceringsbestanden verzamelen</span><span class="sxs-lookup"><span data-stu-id="cd92b-325"><a id="trace-files"></a>Collect trace files</span></span>

<span data-ttu-id="cd92b-326">Voor het verzamelen van foutopsporingsgegevens, voert u de volgende opdrachten uit vanaf een administratieve opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="cd92b-326">To collect debugging traces, run the following commands from an administrative command prompt:</span></span>

1. `cd /d "%ProgramFiles%\Azure Cosmos DB Emulator"`
2. <span data-ttu-id="cd92b-327">`CosmosDB.Emulator.exe /shutdown`.</span><span class="sxs-lookup"><span data-stu-id="cd92b-327">`CosmosDB.Emulator.exe /shutdown`.</span></span> <span data-ttu-id="cd92b-328">Bekijk het systeemvak om te controleren of het programma is afgesloten, kan een minuut duren.</span><span class="sxs-lookup"><span data-stu-id="cd92b-328">Watch the system tray to make sure the program has shut down, it may take a minute.</span></span> <span data-ttu-id="cd92b-329">U kunt ook klikken op **afsluiten** in de gebruikersinterface van Azure DB die Cosmos-emulator.</span><span class="sxs-lookup"><span data-stu-id="cd92b-329">You can also just click **Exit** in the Azure Cosmos DB emulator user interface.</span></span>
3. `CosmosDB.Emulator.exe /starttraces`
4. `CosmosDB.Emulator.exe`
5. <span data-ttu-id="cd92b-330">Reproduceer het probleem.</span><span class="sxs-lookup"><span data-stu-id="cd92b-330">Reproduce the problem.</span></span> <span data-ttu-id="cd92b-331">Als u Data Explorer niet werkt, hoeft u alleen moet worden gewacht op de browser te openen voor een paar seconden de fout te achterhalen.</span><span class="sxs-lookup"><span data-stu-id="cd92b-331">If Data Explorer is not working, you only need to wait for the browser to open for a few seconds to catch the error.</span></span>
5. `CosmosDB.Emulator.exe /stoptraces`
6. <span data-ttu-id="cd92b-332">Navigeer naar `%ProgramFiles%\Azure Cosmos DB Emulator` en het bestand docdbemulator_000001.etl niet vinden.</span><span class="sxs-lookup"><span data-stu-id="cd92b-332">Navigate to `%ProgramFiles%\Azure Cosmos DB Emulator` and find the docdbemulator_000001.etl file.</span></span>
7. <span data-ttu-id="cd92b-333">Het etl-bestand samen met reproduceren stappen om verzenden [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com) voor foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="cd92b-333">Send the .etl file along with repro steps to [askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com) for debugging.</span></span>

### <span data-ttu-id="cd92b-334"><a id="uninstall"></a>Verwijderen van de lokale Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-334"><a id="uninstall"></a>Uninstall the local Emulator</span></span>

1. <span data-ttu-id="cd92b-335">Sluit alle geopende exemplaren van de lokale Emulator door met de rechtermuisknop op het pictogram Azure Cosmos DB Emulator op de taakbalk en klikt u op afsluiten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-335">Exit all open instances of the local Emulator by right-clicking the Azure Cosmos DB Emulator icon on the system tray, and then clicking Exit.</span></span> <span data-ttu-id="cd92b-336">Het duurt een paar minuten voor alle exemplaren om af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-336">It may take a minute for all instances to exit.</span></span>
2. <span data-ttu-id="cd92b-337">Typ in het zoekvak Windows **Apps en functies** en klik op de **Apps en -functies (systeeminstellingen)** resultaat.</span><span class="sxs-lookup"><span data-stu-id="cd92b-337">In the Windows search box, type **Apps & features** and click on the **Apps & features (System settings)** result.</span></span>
3. <span data-ttu-id="cd92b-338">Schuif in de lijst met apps naar **Azure Cosmos DB Emulator**, selecteert u het, klik op **verwijderen**, bevestigen en klikt u op **verwijderen** opnieuw.</span><span class="sxs-lookup"><span data-stu-id="cd92b-338">In the list of apps, scroll to **Azure Cosmos DB Emulator**, select it, click **Uninstall**, then confirm and click **Uninstall** again.</span></span>
4. <span data-ttu-id="cd92b-339">Wanneer de app is verwijderd, gaat u naar C:\Users\<gebruiker > \AppData\Local\CosmosDBEmulator en verwijder de map.</span><span class="sxs-lookup"><span data-stu-id="cd92b-339">When the app is uninstalled, navigate to C:\Users\<user>\AppData\Local\CosmosDBEmulator and delete the folder.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cd92b-340">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd92b-340">Next steps</span></span>

<span data-ttu-id="cd92b-341">In deze zelfstudie hebt u het volgende gedaan:</span><span class="sxs-lookup"><span data-stu-id="cd92b-341">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cd92b-342">De lokale Emulator geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="cd92b-342">Installed the local Emulator</span></span>
> * <span data-ttu-id="cd92b-343">Rand de Docker voor Windows-Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-343">Rand the Emulator on Docker for Windows</span></span>
> * <span data-ttu-id="cd92b-344">Geverifieerde aanvragen</span><span class="sxs-lookup"><span data-stu-id="cd92b-344">Authenticated requests</span></span>
> * <span data-ttu-id="cd92b-345">De Data Explorer gebruikt in de Emulator</span><span class="sxs-lookup"><span data-stu-id="cd92b-345">Used the Data Explorer in the Emulator</span></span>
> * <span data-ttu-id="cd92b-346">Geëxporteerde SSL-certificaten</span><span class="sxs-lookup"><span data-stu-id="cd92b-346">Exported SSL certificates</span></span>
> * <span data-ttu-id="cd92b-347">Naam van de Emulator vanaf de opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="cd92b-347">Called the Emulator from the command line</span></span>
> * <span data-ttu-id="cd92b-348">Verzamelde traceringsbestanden</span><span class="sxs-lookup"><span data-stu-id="cd92b-348">Collected trace files</span></span>

<span data-ttu-id="cd92b-349">In deze zelfstudie hebt u geleerd hoe u van de Emulator van de lokale voor gratis lokale ontwikkeling.</span><span class="sxs-lookup"><span data-stu-id="cd92b-349">In this tutorial, you've learned how to use the local Emulator for free local development.</span></span> <span data-ttu-id="cd92b-350">U kunt nu doorgaan met de volgende zelfstudie en informatie over het exporteren van de Emulator SSL-certificaten.</span><span class="sxs-lookup"><span data-stu-id="cd92b-350">You can now proceed to the next tutorial and learn how to export Emulator SSL certificates.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cd92b-351">De Azure Cosmos DB Emulator certificaten exporteren</span><span class="sxs-lookup"><span data-stu-id="cd92b-351">Export the Azure Cosmos DB Emulator certificates</span></span>](local-emulator-export-ssl-certificates.md)

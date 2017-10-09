---
title: aaaCorrelate gebeurtenissen gedurende een periode met Storm en HBase in HDInsight
description: Meer informatie over hoe toocorrelate gebeurtenissen die op verschillende tijdstippen binnenkomen met behulp van Storm en HBase op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="54b53-103">Gebeurtenissen die op verschillende tijdstippen binnenkomen correleren met Storm en HBase</span><span class="sxs-lookup"><span data-stu-id="54b53-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="54b53-104">Met behulp van een permanente gegevensopslag met Apache Storm, kunt u gegevens die op verschillende tijdstippen binnenkomen correleren.</span><span class="sxs-lookup"><span data-stu-id="54b53-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="54b53-105">Bijvoorbeeld, koppelen aan- en afmelden gebeurtenissen voor een gebruiker sessie toocalculate hoe lang Hallo sessie heeft geduurd.</span><span class="sxs-lookup"><span data-stu-id="54b53-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="54b53-106">In dit document, leert u hoe toocreate een basic C# Storm-topologie die aanmelding en afmelding gebeurtenissen worden bijgehouden voor gebruikerssessies en Hallo duur van Hallo-sessie wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="54b53-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="54b53-107">Hallo-topologie gebruikt HBase als een permanente gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="54b53-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="54b53-108">HBase kunt u ook tooperform batch-query's op Hallo historische gegevens tooproduce meer inzicht geboden.</span><span class="sxs-lookup"><span data-stu-id="54b53-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="54b53-109">Bijvoorbeeld hoeveel gebruikerssessies zijn gestart of beëindigd tijdens een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="54b53-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54b53-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="54b53-110">Prerequisites</span></span>

* <span data-ttu-id="54b53-111">Visual Studio en hello wordt HDInsight tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54b53-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="54b53-112">Zie voor meer informatie [aan de slag met Hallo HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="54b53-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="54b53-113">Apache Storm op HDInsight-cluster (Windows-indeling).</span><span class="sxs-lookup"><span data-stu-id="54b53-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="54b53-114">SCP.NET topologieën worden wel ondersteund op Linux gebaseerde Storm-clusters die zijn gemaakt na 28-10-2016, werkt Hallo HBase SDK voor .NET-pakketten beschikbaar vanaf 28-10-2016 niet correct op Linux gebaseerde HDInsight</span><span class="sxs-lookup"><span data-stu-id="54b53-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="54b53-115">Apache HBase op HDInsight-cluster (Linux of op Windows gebaseerde).</span><span class="sxs-lookup"><span data-stu-id="54b53-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="54b53-116">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="54b53-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="54b53-117">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="54b53-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="54b53-118">[Java](https://java.com) 1.7 of hoger op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="54b53-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="54b53-119">Java is gebruikte toopackage Hallo topologie wanneer deze ingediende toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="54b53-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="54b53-120">Hallo **JAVA_HOME** omgeving variabele moet punt toohello directory met Java.</span><span class="sxs-lookup"><span data-stu-id="54b53-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="54b53-121">Hallo **%JAVA_HOME%/bin** map zich in het Hallo-pad</span><span class="sxs-lookup"><span data-stu-id="54b53-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="54b53-122">Architectuur</span><span class="sxs-lookup"><span data-stu-id="54b53-122">Architecture</span></span>

![Diagram van de gegevensstroom Hallo via Hallo-topologie](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="54b53-124">Correleren van gebeurtenissen, is een algemene id voor de gebeurtenisbron Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="54b53-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="54b53-125">For example, een gebruikers-ID, sessie-ID of andere gegevenseenheid die is een) uniek en b) opgenomen in alle gegevens die worden verzonden tooStorm.</span><span class="sxs-lookup"><span data-stu-id="54b53-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="54b53-126">In dit voorbeeld wordt een GUID-waarde toorepresent een sessie-ID.</span><span class="sxs-lookup"><span data-stu-id="54b53-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="54b53-127">In dit voorbeeld bestaat uit twee clusters met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="54b53-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="54b53-128">HBase: permanente gegevensopslag voor historische gegevens</span><span class="sxs-lookup"><span data-stu-id="54b53-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="54b53-129">Storm: gebruikt tooingest binnenkomende gegevens</span><span class="sxs-lookup"><span data-stu-id="54b53-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="54b53-130">Hallo gegevens wordt willekeurig gegenereerd door Hallo Storm-topologie en bestaat uit Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="54b53-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="54b53-131">Sessie-ID: een GUID die een unieke identificatie van elke sessie</span><span class="sxs-lookup"><span data-stu-id="54b53-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="54b53-132">Gebeurtenis: een begin- of -gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-132">Event: a START or END event.</span></span> <span data-ttu-id="54b53-133">In dit voorbeeld START doet zich altijd voor einde</span><span class="sxs-lookup"><span data-stu-id="54b53-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="54b53-134">Tijd: Hallo tijdstip Hallo-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="54b53-135">Deze gegevens worden verwerkt en opgeslagen in HBase.</span><span class="sxs-lookup"><span data-stu-id="54b53-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="54b53-136">storm-topologie</span><span class="sxs-lookup"><span data-stu-id="54b53-136">Storm topology</span></span>

<span data-ttu-id="54b53-137">Wanneer een sessie wordt gestart, een **START** gebeurtenis is ontvangen door het Hallo-topologie en tooHBase in het logboek geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="54b53-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="54b53-138">Wanneer een **END** gebeurtenis is ontvangen, Hallo topologie opgehaald Hallo **START** gebeurtenis en berekent Hallo tijd tussen twee Hallo gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="54b53-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="54b53-139">Dit **duur** waarde vervolgens wordt opgeslagen in HBase samen met de Hallo **END** informatie over de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54b53-140">Terwijl deze topologie wordt gedemonstreerd basispatroon hello, moet een productie-oplossing tootake ontwerp voor Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="54b53-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="54b53-141">Gebeurtenissen volgorde binnenkomen</span><span class="sxs-lookup"><span data-stu-id="54b53-141">Events arriving out of order</span></span>
> * <span data-ttu-id="54b53-142">Dubbele gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="54b53-142">Duplicate events</span></span>
> * <span data-ttu-id="54b53-143">Verwijderde gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="54b53-143">Dropped events</span></span>

<span data-ttu-id="54b53-144">Hallo voorbeeld topologie bestaat uit Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="54b53-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="54b53-145">Session.CS: simuleert een gebruikerssessie door het maken van een willekeurige sessie-ID, start tijdstip en hoe lang Hallo sessie duurt.</span><span class="sxs-lookup"><span data-stu-id="54b53-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="54b53-146">Spout.CS: 100 sessies maakt, verzendt een startgebeurtenis, wordt gewacht Hallo willekeurige time-out voor elke sessie en vervolgens verzendt een END-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="54b53-147">Vervolgens wordt recyclet sessies toogenerate nieuwe beëindigd.</span><span class="sxs-lookup"><span data-stu-id="54b53-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="54b53-148">HBaseLookupBolt.cs: maakt gebruik van Hallo sessie-ID toolook van de sessie-informatie van HBase.</span><span class="sxs-lookup"><span data-stu-id="54b53-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="54b53-149">Wanneer een END-gebeurtenis wordt verwerkt, vindt het overeenkomende begingebeurtenis Hallo en Hallo duur van Hallo-sessie wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="54b53-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="54b53-150">HBaseBolt.cs: Bevat gegevens in HBase.</span><span class="sxs-lookup"><span data-stu-id="54b53-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="54b53-151">TypeHelper.cs: Helpt met typeconversie bij het lezen van / schrijven tooHBase.</span><span class="sxs-lookup"><span data-stu-id="54b53-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="54b53-152">HBase-schema</span><span class="sxs-lookup"><span data-stu-id="54b53-152">HBase schema</span></span>

<span data-ttu-id="54b53-153">In HBase, Hallo gegevens opgeslagen in een tabel met Hallo schema-instellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="54b53-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="54b53-154">Rijsleutel: Hallo-sessie-ID wordt gebruikt als de sleutel Hallo voor rijen in deze tabel.</span><span class="sxs-lookup"><span data-stu-id="54b53-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="54b53-155">Kolomfamilie: familienaam Hallo 'cf' is.</span><span class="sxs-lookup"><span data-stu-id="54b53-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="54b53-156">Kolommen die zijn opgeslagen in deze familie zijn:</span><span class="sxs-lookup"><span data-stu-id="54b53-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="54b53-157">gebeurtenis: begin of einde.</span><span class="sxs-lookup"><span data-stu-id="54b53-157">event: START or END.</span></span>

  * <span data-ttu-id="54b53-158">tijd: Hallo tijd in milliseconden dat Hallo gebeurtenis is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="54b53-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="54b53-159">duur: Hallo lengte tussen de begin- en -gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="54b53-160">VERSIES: Hallo 'cf' familie ingesteld tooretain 5-versies van elke rij.</span><span class="sxs-lookup"><span data-stu-id="54b53-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="54b53-161">Versies zijn een logboek van de vorige waarden voor de sleutel van een specifieke rij.</span><span class="sxs-lookup"><span data-stu-id="54b53-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="54b53-162">HBase retourneert alleen Hallo-waarde voor de meest recente versie van een rij Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="54b53-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="54b53-163">In dit geval wordt hello dezelfde rij gebruikt voor elke versie van een rij wordt geïdentificeerd door de tijdstempelwaarde Hallo alle gebeurtenissen (START en END.).</span><span class="sxs-lookup"><span data-stu-id="54b53-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="54b53-164">Versies bieden een historisch overzicht gegeven van gebeurtenissen die zijn geregistreerd voor een specifieke-ID.</span><span class="sxs-lookup"><span data-stu-id="54b53-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="54b53-165">Hallo-project downloaden</span><span class="sxs-lookup"><span data-stu-id="54b53-165">Download hello project</span></span>

<span data-ttu-id="54b53-166">Hallo-voorbeeldproject kan worden gedownload vanaf [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="54b53-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="54b53-167">Deze download bevat Hallo C#-projecten te volgen:</span><span class="sxs-lookup"><span data-stu-id="54b53-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="54b53-168">CorrelationTopology: C# Storm-topologie die willekeurig begin- en gebeurtenissen voor gebruikerssessies verzendt.</span><span class="sxs-lookup"><span data-stu-id="54b53-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="54b53-169">Elke sessie duurt tussen 1 en 5 minuten.</span><span class="sxs-lookup"><span data-stu-id="54b53-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="54b53-170">SessionInfo: C#-consoletoepassing die maakt Hallo HBase-tabel en bevat voorbeeldquery tooreturn informatie over de opgeslagen sessiegegevens.</span><span class="sxs-lookup"><span data-stu-id="54b53-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="54b53-171">Hallo-tabel maken</span><span class="sxs-lookup"><span data-stu-id="54b53-171">Create hello table</span></span>

1. <span data-ttu-id="54b53-172">Open Hallo **SessionInfo** -project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54b53-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="54b53-173">In **Solution Explorer**, klik met de rechtermuisknop Hallo **SessionInfo** project en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="54b53-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Schermopname van menu met eigenschappen die zijn geselecteerd](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="54b53-175">Selecteer **instellingen**, en vervolgens set Hallo de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="54b53-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="54b53-176">HBaseClusterURL: Hallo URL tooyour HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="54b53-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="54b53-177">Bijvoorbeeld: https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="54b53-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="54b53-178">HBaseClusterUserName: Hallo beheerder/HTTP-gebruikersaccount voor uw cluster</span><span class="sxs-lookup"><span data-stu-id="54b53-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="54b53-179">HBaseClusterPassword: Hallo wachtwoord voor Hallo beheerder/HTTP-gebruikersaccount</span><span class="sxs-lookup"><span data-stu-id="54b53-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="54b53-180">HBaseTableName: naam van Hallo van Hallo tabel toouse met dit voorbeeld</span><span class="sxs-lookup"><span data-stu-id="54b53-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="54b53-181">HBaseTableColumnFamily: Hallo kolom familienaam</span><span class="sxs-lookup"><span data-stu-id="54b53-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Afbeelding van dialoogvenster Instellingen](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="54b53-183">Hallo-oplossing worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54b53-183">Run hello solution.</span></span> <span data-ttu-id="54b53-184">Wanneer u wordt gevraagd, selecteert u Hallo 'c' sleutel toocreate Hallo tabel op uw HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="54b53-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="54b53-185">Bouw en implementeer Hallo Storm-topologie</span><span class="sxs-lookup"><span data-stu-id="54b53-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="54b53-186">Open Hallo **CorrelationTopology** oplossing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54b53-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="54b53-187">In **Solution Explorer**, klik met de rechtermuisknop Hallo **CorrelationTopology** project en selecteer Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="54b53-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="54b53-188">Selecteer in het venster Eigenschappen Hallo **instellingen** en Voer Hallo configuratiewaarden voor dit project.</span><span class="sxs-lookup"><span data-stu-id="54b53-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="54b53-189">Hallo eerste 5 zijn Hallo dezelfde waarden gebruikt door Hallo **SessionInfo** project:</span><span class="sxs-lookup"><span data-stu-id="54b53-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="54b53-190">HBaseClusterURL: Hallo URL tooyour HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="54b53-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="54b53-191">Bijvoorbeeld: https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="54b53-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="54b53-192">HBaseClusterUserName: Hallo beheerder/HTTP-gebruikersaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="54b53-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="54b53-193">HBaseClusterPassword: Hallo wachtwoord voor Hallo beheerder/HTTP-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="54b53-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="54b53-194">HBaseTableName: naam van Hallo van Hallo tabel toouse met dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="54b53-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="54b53-195">Deze waarde dezelfde is Hallo tabelnaam zoals gebruikt in Hallo SessionInfo project.</span><span class="sxs-lookup"><span data-stu-id="54b53-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="54b53-196">HBaseTableColumnFamily: Hallo familie kolomnaam.</span><span class="sxs-lookup"><span data-stu-id="54b53-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="54b53-197">Deze waarde is Hallo dezelfde familienaam kolom zoals gebruikt in Hallo SessionInfo project.</span><span class="sxs-lookup"><span data-stu-id="54b53-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="54b53-198">Niet Hallo HBaseTableColumnNames, wijzigen, omdat zijn standaard Hallo Hallo namen die worden gebruikt door **SessionInfo** tooretrieve gegevens.</span><span class="sxs-lookup"><span data-stu-id="54b53-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="54b53-199">Hallo eigenschappen opslaan en vervolgens Hallo-project te bouwen.</span><span class="sxs-lookup"><span data-stu-id="54b53-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="54b53-200">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="54b53-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="54b53-201">Als u wordt gevraagd, voert u Hallo referenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="54b53-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Afbeelding van Hallo indienen toostorm menu-item](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="54b53-203">In Hallo **indienen topologie** dialoogvenster, selecteer Hallo Storm-cluster toodeploy deze topologie gewenste.</span><span class="sxs-lookup"><span data-stu-id="54b53-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54b53-204">Hallo duurt eerst u een topologie dient een paar seconden tooretrieve Hallo-naam van uw HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="54b53-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="54b53-205">Zodra het Hallo-topologie is geüpload en ingediende toohello cluster, Hallo **Storm-Topologieweergave** wordt geopend en Hallo topologie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="54b53-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="54b53-206">toorefresh hello gegevens, selecteer Hallo **CorrelationTopology** en gebruik de knop Vernieuwen Hallo op Hallo rechts op de pagina Hallo top.</span><span class="sxs-lookup"><span data-stu-id="54b53-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Afbeelding van Hallo Topologieweergave](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="54b53-208">Wanneer Hallo topologie begint het genereren van gegevens, de waarde in Hallo Hallo **lichten** kolom stappen.</span><span class="sxs-lookup"><span data-stu-id="54b53-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="54b53-209">Als hello **Storm-Topologieweergave** niet automatisch wordt geopend, gebruikt u Hallo volgende stappen tooopen het:</span><span class="sxs-lookup"><span data-stu-id="54b53-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="54b53-210">In **Solution Explorer**, vouw **Azure**, en vouw vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="54b53-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="54b53-211">Klik met de rechtermuisknop Hallo Storm-cluster die Hallo topologie wordt uitgevoerd op en selecteer vervolgens **Storm-topologieën weergeven**</span><span class="sxs-lookup"><span data-stu-id="54b53-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="54b53-212">Hallo querygegevens</span><span class="sxs-lookup"><span data-stu-id="54b53-212">Query hello data</span></span>

<span data-ttu-id="54b53-213">Zodra heeft gegevens zijn verzonden, gebruikt u Hallo stappen tooquery Hallo gegevens te volgen.</span><span class="sxs-lookup"><span data-stu-id="54b53-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="54b53-214">Retourneren van toohello **SessionInfo** project.</span><span class="sxs-lookup"><span data-stu-id="54b53-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="54b53-215">Als niet wordt uitgevoerd, start u een nieuw exemplaar van deze.</span><span class="sxs-lookup"><span data-stu-id="54b53-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="54b53-216">Wanneer u wordt gevraagd, selecteert u **s** toosearch voor START-gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="54b53-217">U bent na vragen aan gebruiker tooenter een start en end tijd toodefine een tijdsbereik - worden alleen gebeurtenissen tussen deze twee keer geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="54b53-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="54b53-218">Gebruik Hallo volgende formatteren bij het invoeren van Hallo begin- en eindtijden: uu: mm en de 'M' of 'pm'.</span><span class="sxs-lookup"><span data-stu-id="54b53-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="54b53-219">Bijvoorbeeld: 23:20 uur.</span><span class="sxs-lookup"><span data-stu-id="54b53-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="54b53-220">gebeurtenissen vastgelegd tooreturn, een begin-tijdstip voordat Hallo Storm-topologie is geïmplementeerd en eindtijd van nu gebruiken.</span><span class="sxs-lookup"><span data-stu-id="54b53-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="54b53-221">Hallo beleidsretourgegevens bevat vermeldingen vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="54b53-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="54b53-222">Zoeken naar einde gebeurtenissen works Hallo dezelfde als begin-gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="54b53-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="54b53-223">END-gebeurtenissen worden echter willekeurig gegenereerd tussen 1 en 5 minuten na Hallo startgebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="54b53-224">Mogelijk hebt u tootry enkele tijd bereiken toofind Hallo END gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="54b53-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="54b53-225">END-gebeurtenissen bevatten ook Hallo duur van Hallo sessie - Hallo verschil tussen Hallo gebeurtenis begintijd en eindtijd van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="54b53-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="54b53-226">Hier volgt een voorbeeld van gegevens voor END-gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="54b53-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="54b53-227">Hoewel Hallo tijdwaarden die u invoert in de lokale tijd, is Hallo tijd geretourneerde Hallo query ingesteld op UTC.</span><span class="sxs-lookup"><span data-stu-id="54b53-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="54b53-228">Hallo-topologie stoppen</span><span class="sxs-lookup"><span data-stu-id="54b53-228">Stop hello topology</span></span>

<span data-ttu-id="54b53-229">Wanneer u klaar toostop Hallo-topologie bent, retourneren toohello **CorrelationTopology** -project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="54b53-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="54b53-230">In Hallo **Storm-Topologieweergave**, selecteert u Hallo topologie en gebruik vervolgens Hallo **Kill** knop Hallo boven aan het Hallo-topologie weergeven.</span><span class="sxs-lookup"><span data-stu-id="54b53-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="54b53-231">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="54b53-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="54b53-232">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54b53-232">Next steps</span></span>

<span data-ttu-id="54b53-233">Zie voor meer voorbeelden van Storm [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="54b53-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

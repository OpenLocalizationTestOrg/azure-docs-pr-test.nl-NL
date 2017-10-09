---
title: aaaUse Azure Stream Analytics-Tools voor Visual Studio | Microsoft Docs
description: Zelfstudie voor hello Azure Stream Analytics-Tools voor Visual Studio aan de slag
keywords: Visual studio
documentationcenter: 
services: stream-analytics
author: 
manager: 
editor: 
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 
ms.author: 
ms.openlocfilehash: bda8e548040509a6f29f1b713268bc38f73228fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="93926-104">Azure Stream Analytics-hulpprogramma's voor Visual Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="93926-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="93926-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="93926-105">Introduction</span></span>
<span data-ttu-id="93926-106">In deze zelfstudie leert u hoe toouse Azure Stream Analytics-Tools voor Visual Studio-toocreate ontwerpen, lokaal testen, beheren en fouten opsporen in uw Stream Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="93926-106">In this tutorial, you learn how toouse Azure Stream Analytics Tools for Visual Studio toocreate, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="93926-107">Na het voltooien van deze zelfstudie, kunt u zich kunt:</span><span class="sxs-lookup"><span data-stu-id="93926-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="93926-108">Tijd om uzelf bekend met Stream Analytics-hulpprogramma's voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93926-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="93926-109">Configureren en implementeren van een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="93926-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="93926-110">Test uw taak lokaal met lokale voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="93926-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="93926-111">Gebruik controle tootroubleshoot problemen.</span><span class="sxs-lookup"><span data-stu-id="93926-111">Use monitoring tootroubleshoot issues.</span></span>
* <span data-ttu-id="93926-112">Bestaande taken tooprojects exporteren.</span><span class="sxs-lookup"><span data-stu-id="93926-112">Export existing jobs tooprojects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93926-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="93926-113">Prerequisites</span></span>
<span data-ttu-id="93926-114">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="93926-114">toocomplete this tutorial, you need hello following prerequisites:</span></span>
* <span data-ttu-id="93926-115">Hallo-stappen die worden voorafgegaan door 'Een Stream Analytics-taak maken' in hello voltooien [een IoT-oplossing bouwen met behulp van de Stream Analytics-zelfstudie](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="93926-115">Finish hello steps that precede "Create a Stream Analytics job" in hello [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="93926-116">Gebruik Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="93926-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="93926-117">Enterprise (Ultimate/Premium), Professional en Community-edities worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="93926-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="93926-118">Express edition wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="93926-118">Express edition is not supported.</span></span> <span data-ttu-id="93926-119">Visual Studio 2017 wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="93926-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="93926-120">Gebruik hello Azure SDK voor .NET versie 2.7.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="93926-120">Use hello Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="93926-121">Installeren met behulp van Hallo [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="93926-121">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="93926-122">Hallo installeren [Stream Analytics-Tools voor Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="93926-122">Install hello [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="93926-123">Een Stream Analytics-project maken</span><span class="sxs-lookup"><span data-stu-id="93926-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="93926-124">Klik in Visual Studio op Hallo **bestand** menu en selecteer **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="93926-124">In Visual Studio, click hello **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="93926-125">Selecteer in Hallo sjablonen lijst aan de linkerkant Hallo **Stream Analytics** en klik vervolgens op **Azure Stream Analytics toepassing**.</span><span class="sxs-lookup"><span data-stu-id="93926-125">In hello templates list on hello left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="93926-126">Voer Hallo project **naam**, **locatie**, en **oplossingsnaam** als voor andere projecten.</span><span class="sxs-lookup"><span data-stu-id="93926-126">Enter hello project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Nieuw Project-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="93926-128">Een **Tolstation** project is gegenereerd op **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="93926-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Tolstation project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-hello-correct-subscription"></a><span data-ttu-id="93926-130">Kies het juiste abonnement Hallo</span><span class="sxs-lookup"><span data-stu-id="93926-130">Choose hello correct subscription</span></span>
1. <span data-ttu-id="93926-131">Klik in Visual Studio op Hallo **weergave** menu en open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="93926-131">In Visual Studio, click hello **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="93926-132">Meld u aan met uw Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="93926-132">Sign in with your Azure Account.</span></span> 

## <a name="define-hello-input-sources"></a><span data-ttu-id="93926-133">Hallo invoerbronnen definiëren</span><span class="sxs-lookup"><span data-stu-id="93926-133">Define hello input sources</span></span>
1.  <span data-ttu-id="93926-134">In **Solution Explorer**, vouw Hallo **invoer** knooppunt en wijzig de naam **Input.json** te**EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="93926-134">In **Solution Explorer**, expand hello **Inputs** node and rename **Input.json** too**EntryStream.json**.</span></span> <span data-ttu-id="93926-135">Dubbelklik op **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="93926-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="93926-136">Hallo **invoer Alias** is nu **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="93926-136">hello **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="93926-137">Hallo invoer alias wordt gebruikt in Hallo query script.</span><span class="sxs-lookup"><span data-stu-id="93926-137">hello input alias is used in hello query script.</span></span> 
3.  <span data-ttu-id="93926-138">In **brontype**, selecteer **gegevensstroom**.</span><span class="sxs-lookup"><span data-stu-id="93926-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="93926-139">In **bron**, selecteer **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="93926-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="93926-140">In **Service Bus Namespace**, selecteer Hallo **TollData** optie.</span><span class="sxs-lookup"><span data-stu-id="93926-140">In **Service Bus Namespace**, select hello **TollData** option.</span></span>
6.  <span data-ttu-id="93926-141">In **naam Event Hub**, selecteer **vermelding**.</span><span class="sxs-lookup"><span data-stu-id="93926-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="93926-142">In **Event Hub-beleidsnaam**, selecteer **RootManageSharedAccessKey** (Hallo standaardwaarde).</span><span class="sxs-lookup"><span data-stu-id="93926-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (hello default value).</span></span>
8.  <span data-ttu-id="93926-143">In **gebeurtenis serialisatie-indeling**, selecteer **Json**.</span><span class="sxs-lookup"><span data-stu-id="93926-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="93926-144">In **codering**, selecteer **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="93926-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="93926-145">Uw instellingen moeten eruitzien als Hallo schermafbeelding te volgen:</span><span class="sxs-lookup"><span data-stu-id="93926-145">Your settings should look like hello following screenshot:</span></span>

    ![Invoer-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="93926-147">wizard toofinish hello, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="93926-147">toofinish hello wizard, click **Save**.</span></span> <span data-ttu-id="93926-148">U kunt nu een andere invoerbron toocreate Hallo afsluiten stroom toevoegen.</span><span class="sxs-lookup"><span data-stu-id="93926-148">Now you can add another input source toocreate hello exit stream.</span></span> <span data-ttu-id="93926-149">Klik met de rechtermuisknop Hallo **invoer** uit en selecteer **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="93926-149">Right-click hello **Inputs** node, and select **New Item**.</span></span>

    ![Nieuw Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="93926-151">Selecteer in het venster Hallo **Azure Stream Analytics invoer**, en wijzig Hallo **naam** te**ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="93926-151">In hello window, select **Azure Stream Analytics Input**, and change hello **Name** too**ExitStream.json**.</span></span> <span data-ttu-id="93926-152">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="93926-152">Click **Add**.</span></span>

    ![Venster Nieuw Item toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="93926-154">Dubbelklik op **ExitStream.json** in Hallo-project en volg Hallo dezelfde stappen als bij Hallo vermelding stroom.</span><span class="sxs-lookup"><span data-stu-id="93926-154">Double-click **ExitStream.json** in hello project, and follow hello same steps as you did for hello entry stream.</span></span> <span data-ttu-id="93926-155">Ervoor tooenter worden **sluiten** voor Hallo **naam Event Hub** zoals weergegeven in de volgende schermafbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="93926-155">Be sure tooenter **exit** for hello **Event Hub Name** as shown in hello following screenshot:</span></span>

    ![ExitStream venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="93926-157">U hebt nu twee invoer streams gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="93926-157">Now you have defined two input streams:</span></span>

    ![Toegang naar en uitgang invoer stromen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="93926-159">Voeg vervolgens de gegevensinvoer verwijzing voor Hallo blob-bestand met de registratiegegevens auto.</span><span class="sxs-lookup"><span data-stu-id="93926-159">Next, add reference data input for hello blob file that contains car registration data.</span></span>

13. <span data-ttu-id="93926-160">Klik met de rechtermuisknop Hallo **invoer** knooppunt in het Hallo-project en klik vervolgens op Hallo van Volg dezelfde stappen als bij Hallo stroom invoer.</span><span class="sxs-lookup"><span data-stu-id="93926-160">Right-click hello **Inputs** node in hello project, and then follow hello same steps as you did for hello stream inputs.</span></span> <span data-ttu-id="93926-161">In **invoer Alias**, voer **registratie**, en in **brontype**, selecteer **referentiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="93926-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Registratie-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="93926-163">In **Opslagaccount**, selecteer Hallo **tolldata** optie.</span><span class="sxs-lookup"><span data-stu-id="93926-163">In **Storage Account**, select hello **tolldata** option.</span></span> <span data-ttu-id="93926-164">In **Container**, selecteer **tolldata**, en in **pad patroon**, voer **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="93926-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="93926-165">Deze naam is hoofdlettergevoelig en moet in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="93926-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="93926-166">wizard toofinish hello, klikt u op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="93926-166">toofinish hello wizard, click **Save**.</span></span>

<span data-ttu-id="93926-167">Nu worden alle Hallo invoer gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="93926-167">Now all hello inputs are defined.</span></span>

## <a name="define-hello-output"></a><span data-ttu-id="93926-168">Hallo-uitvoer definiëren</span><span class="sxs-lookup"><span data-stu-id="93926-168">Define hello output</span></span>
1.  <span data-ttu-id="93926-169">In **Solution Explorer**, vouw Hallo **invoer** knooppunt en dubbelklik op **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="93926-169">In **Solution Explorer**, expand hello **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="93926-170">In **Uitvoeraliassen**, voer **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="93926-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="93926-171">In **Sink**, selecteer **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="93926-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="93926-172">In **Database**, selecteer **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="93926-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="93926-173">In **gebruikersnaam**, voer **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="93926-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="93926-174">In **wachtwoord**, voer **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="93926-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="93926-175">In **tabel**, voer **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="93926-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="93926-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="93926-176">Click **Save**.</span></span>

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="93926-178">Een Stream Analytics query maken</span><span class="sxs-lookup"><span data-stu-id="93926-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="93926-179">Deze zelfstudie probeert tooanswer verschillende bedrijfsvragen gerelateerde tootoll gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="93926-179">This tutorial attempts tooanswer several business questions that are related tootoll data.</span></span> <span data-ttu-id="93926-180">Dit wordt ook Stream Analytics query's die kunnen worden gebruikt in de Stream Analytics tooprovide relevante antwoorden.</span><span class="sxs-lookup"><span data-stu-id="93926-180">It also constructs Stream Analytics queries that can be used in Stream Analytics tooprovide relevant answers.</span></span>
<span data-ttu-id="93926-181">Voordat u uw eerste Stream Analytics-taak, we gaan een eenvoudige scenario en Hallo-querysyntaxis te verkennen.</span><span class="sxs-lookup"><span data-stu-id="93926-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and hello query syntax.</span></span>

### <a name="introduction-toohello-stream-analytics-query-language"></a><span data-ttu-id="93926-182">Inleiding toohello querytaal van Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="93926-182">Introduction toohello Stream Analytics query language</span></span>
<span data-ttu-id="93926-183">Stel dat u nodig hebt toocount Hallo aantal voertuigen dat een tolstation stand invoeren.</span><span class="sxs-lookup"><span data-stu-id="93926-183">Let’s say that you need toocount hello number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="93926-184">Omdat dit voorbeeld een continue stroom van gebeurtenissen is, hebt u toodefine een periode.</span><span class="sxs-lookup"><span data-stu-id="93926-184">Because this example is a continuous stream of events, you have toodefine a period of time.</span></span> <span data-ttu-id="93926-185">Hallo vraag toobe 'hoeveel voertuigen Geef een tolstation stand elke drie minuten?' wijzigen</span><span class="sxs-lookup"><span data-stu-id="93926-185">Modify hello question toobe “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="93926-186">Deze manier toocount gegevens vaak wordt aangeduid tooas Hallo daling aantal.</span><span class="sxs-lookup"><span data-stu-id="93926-186">This way toocount data is commonly referred tooas hello tumbling count.</span></span>

<span data-ttu-id="93926-187">Bekijkt hello Stream Analytics query waarmee deze vraag worden beantwoord:</span><span class="sxs-lookup"><span data-stu-id="93926-187">Look at hello Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="93926-188">Stream Analytics maakt gebruik van een querytaal die lijkt op SQL en enkele extensies toospecify tijd gerelateerde aspecten van Hallo query toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="93926-188">Stream Analytics uses a query language that's like SQL and adds a few extensions toospecify time-related aspects of hello query.</span></span>

<span data-ttu-id="93926-189">Zie voor meer informatie [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) en [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructies die worden gebruikt in query Hallo van MSDN.</span><span class="sxs-lookup"><span data-stu-id="93926-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in hello query from MSDN.</span></span>

<span data-ttu-id="93926-190">Nu u uw eerste Stream Analytics query hebt geschreven, is het tijd tootest deze.</span><span class="sxs-lookup"><span data-stu-id="93926-190">Now that you have written your first Stream Analytics query, it's time tootest it.</span></span> <span data-ttu-id="93926-191">Hallo voorbeeldbestanden zich in de map TollApp in in het pad naar hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="93926-191">Use hello sample data files located in your TollApp folder in hello following path:</span></span>

<span data-ttu-id="93926-192">.. \TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="93926-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="93926-193">Deze map bevat de volgende bestanden Hallo:</span><span class="sxs-lookup"><span data-stu-id="93926-193">This folder contains hello following files:</span></span>
*   <span data-ttu-id="93926-194">Entry.JSON</span><span class="sxs-lookup"><span data-stu-id="93926-194">Entry.json</span></span>
*   <span data-ttu-id="93926-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="93926-195">Exit.json</span></span>
*   <span data-ttu-id="93926-196">Registration.JSON</span><span class="sxs-lookup"><span data-stu-id="93926-196">Registration.json</span></span>

## <a name="count-hello-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="93926-197">Het aantal voertuigen een tolstation stand Hallo tellen</span><span class="sxs-lookup"><span data-stu-id="93926-197">Count hello number of vehicles entering a toll booth</span></span>
<span data-ttu-id="93926-198">Dubbelklik in het Hallo-project op **Script.asaql** tooopen Hallo script in Hallo **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="93926-198">In hello project, double-click **Script.asaql** tooopen hello script in hello **Query Editor**.</span></span> <span data-ttu-id="93926-199">Kopieer en plak Hallo script in de vorige sectie Hallo in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="93926-199">Copy and paste hello script in hello previous section into hello editor.</span></span> <span data-ttu-id="93926-200">Hallo Query-Editor biedt ondersteuning voor IntelliSense syntaxiskleuren en Hallo fout markering.</span><span class="sxs-lookup"><span data-stu-id="93926-200">hello Query Editor supports IntelliSense, syntax coloring, and hello error marker.</span></span>

![Query-Editor](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="93926-202">Stream Analytics query's lokaal testen</span><span class="sxs-lookup"><span data-stu-id="93926-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="93926-203">toocompile hello query toosee als er een syntaxisfout, met de rechtermuisknop op het Hallo-project en selecteer **bouwen**.</span><span class="sxs-lookup"><span data-stu-id="93926-203">toocompile hello query toosee if there is a syntax error, right-click hello project and select **Build**.</span></span> 

2. <span data-ttu-id="93926-204">toovalidate deze query tegen voorbeeldgegevens, kunt u lokale voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="93926-204">toovalidate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="93926-205">Met de rechtermuisknop op het Hallo-invoer en selecteer **lokale invoer toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="93926-205">Right-click hello input, and select **Add local input**.</span></span>

    ![Lokale invoer toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="93926-207">Selecteer in het pop-upvenster Hallo, Hallo voorbeeldgegevens vanaf uw lokale pad.</span><span class="sxs-lookup"><span data-stu-id="93926-207">In hello pop-up window, select hello sample data from your local path.</span></span> <span data-ttu-id="93926-208">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="93926-208">Click **Save**.</span></span>

    ![Lokale invoer venster toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="93926-210">Een bestand met de naam **local_EntryStream.json** tooyour invoer map automatisch wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="93926-210">A file named **local_EntryStream.json** is automatically added tooyour inputs folder.</span></span>

    ![Toegevoegde tooinputs bestandsmap](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="93926-212">In Hallo **Query-Editor**, klikt u op **lokaal uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="93926-212">In hello **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="93926-213">Of u kunt ook op Hallo F5 drukken.</span><span class="sxs-lookup"><span data-stu-id="93926-213">Or you can press hello F5 key.</span></span>

    ![Lokaal uitvoeren](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Lokaal uitvoeren van uitvoer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="93926-216">Druk op belangrijke tooview Hallo uitvoer in Hallo **ASA lokale uitvoeren resultaat** venster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="93926-216">Press any key tooview hello output in hello **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Venster ASA lokale uitvoeren resultaat](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="93926-218">Klik op **geopende resultaat map** toocheck Hallo uitvoerbestanden beide in CSV en JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="93926-218">Click **Open Result Folder** toocheck hello output files both in CSV and JSON format.</span></span>

    ![Open resultaat map uitvoer](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-hello-input-data"></a><span data-ttu-id="93926-220">Voorbeeld Hallo invoergegevens</span><span class="sxs-lookup"><span data-stu-id="93926-220">Sample hello input data</span></span>
<span data-ttu-id="93926-221">U kunt ook invoer voorbeeldgegevens vanuit het lokale bestand voor invoerbronnen tooa.</span><span class="sxs-lookup"><span data-stu-id="93926-221">You can also sample input data from input sources tooa local file.</span></span> 
1. <span data-ttu-id="93926-222">Met de rechtermuisknop op Hallo invoer config-bestand en selecteer **voorbeeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="93926-222">Right-click hello input config file, and select **Sample Data**.</span></span> 

   ![Voorbeeldgegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="93926-224">U kunt alleen de event hub of -IoT-hub steekproef nemen nu.</span><span class="sxs-lookup"><span data-stu-id="93926-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="93926-225">Andere bronnen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="93926-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="93926-226">Voer in het pop-upvenster hello, Hallo lokaal pad gebruikt toosave Hallo-voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="93926-226">In hello pop-up window, enter hello local path used toosave hello sample data.</span></span> <span data-ttu-id="93926-227">Klik op **voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="93926-227">Click **Sample**.</span></span>

    ![Venster van de gegevens voorbeeld](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="93926-229">U kunt de voortgang Hallo in Hallo bekijken **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="93926-229">You can see hello progress in hello **Output** window.</span></span> 

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-tooazure"></a><span data-ttu-id="93926-231">Verzenden van een Stream Analytics query tooAzure</span><span class="sxs-lookup"><span data-stu-id="93926-231">Submit a Stream Analytics query tooAzure</span></span>
1. <span data-ttu-id="93926-232">In Hallo **Query-Editor**, klikt u op **indienen tooAzure** in de Hallo scripteditor.</span><span class="sxs-lookup"><span data-stu-id="93926-232">In hello **Query Editor**, click **Submit tooAzure** in hello script editor.</span></span>

    ![TooAzure verzenden](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="93926-234">Selecteer **maken van een nieuwe Azure Stream Analytics-taak**.</span><span class="sxs-lookup"><span data-stu-id="93926-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="93926-235">Voer Hallo **taaknaam**, en selecteer Hallo juist **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="93926-235">Enter hello **Job Name**, and select hello correct **Subscription**.</span></span> <span data-ttu-id="93926-236">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="93926-236">Click **Submit**.</span></span>

    ![Venster van de taak verzenden](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="93926-238">Een taak starten</span><span class="sxs-lookup"><span data-stu-id="93926-238">Start a job</span></span>
<span data-ttu-id="93926-239">Nu dat de taak is gemaakt, wordt Hallo taakweergave automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="93926-239">Now that your job is created, hello job view is automatically opened.</span></span> 
1. <span data-ttu-id="93926-240">Hallo toostart taak, klikt u op Hallo **groene pijl** knop.</span><span class="sxs-lookup"><span data-stu-id="93926-240">toostart hello job, click hello **green arrow** button.</span></span>

    ![Een taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="93926-242">De standaardinstelling Hallo selecteren en op **Start**.</span><span class="sxs-lookup"><span data-stu-id="93926-242">Select hello default setting, and click **Start**.</span></span>
 
    ![Venster van de taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="93926-244">Hallo taak **Status** wijzigingen te**met**, en **invoer gebeurtenissen** en **Uitvoergebeurtenissen** worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="93926-244">hello job **Status** changes too**Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Uitvoeringsstatus in Taakoverzicht](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-hello-results-in-visual-studio"></a><span data-ttu-id="93926-246">Resultaten van de Hallo in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="93926-246">Check hello results in Visual Studio</span></span>
1. <span data-ttu-id="93926-247">Open in Visual Studio **Server Explorer** en klik met de rechtermuisknop Hallo **TollDataRefJoin** tabel.</span><span class="sxs-lookup"><span data-stu-id="93926-247">In Visual Studio, open **Server Explorer** and right-click hello **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="93926-248">Selecteer **tabelgegevens weergeven** toosee Hallo uitvoer van de taak.</span><span class="sxs-lookup"><span data-stu-id="93926-248">Select **Show Table Data** toosee hello output of your job.</span></span>
   
    ![Selectie van de tabelgegevens weergeven in Server Explorer](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-hello-job-metrics"></a><span data-ttu-id="93926-250">Metrische gegevens weergeven Hallo taak</span><span class="sxs-lookup"><span data-stu-id="93926-250">View hello job metrics</span></span>
<span data-ttu-id="93926-251">Een aantal statistieken basic taak kunt u vinden in **taak metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="93926-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Venster van de taak metrische gegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-hello-job-in-server-explorer"></a><span data-ttu-id="93926-253">Lijst Hallo taak in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="93926-253">List hello job in Server Explorer</span></span>
<span data-ttu-id="93926-254">In **Server Explorer**, klikt u op **Stream Analytics-taken** en klik vervolgens op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="93926-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="93926-255">Hallo-taak wordt weergegeven onder **Stream Analytics-taken**.</span><span class="sxs-lookup"><span data-stu-id="93926-255">hello job appears under **Stream Analytics jobs**.</span></span>

![Stream Analytics-taken die worden vermeld in Server Explorer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-hello-job-view"></a><span data-ttu-id="93926-257">Open Hallo taak weergeven</span><span class="sxs-lookup"><span data-stu-id="93926-257">Open hello job view</span></span>
<span data-ttu-id="93926-258">tooopen hello taak weergeven, vouwt u het taakknooppunt en dubbelklikt u op Hallo **taakweergave** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="93926-258">tooopen hello job view, expand your job node and double-click hello **Job View** node.</span></span>

![Knooppunt van de taak weergeven](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-tooa-project"></a><span data-ttu-id="93926-260">Een bestaande taak tooa project exporteren</span><span class="sxs-lookup"><span data-stu-id="93926-260">Export an existing job tooa project</span></span>
<span data-ttu-id="93926-261">Er zijn twee manieren kunt u een bestaand taak tooa project exporteren.</span><span class="sxs-lookup"><span data-stu-id="93926-261">There are two ways you can export an existing job tooa project.</span></span>

<span data-ttu-id="93926-262">In **Server Explorer**, klik met de rechtermuisknop Hallo taakknooppunt in Hallo **Stream Analytics-taken** uit en selecteer **tooNew Stream Analytics Project exporteren**.</span><span class="sxs-lookup"><span data-stu-id="93926-262">In **Server Explorer**, right-click hello job node in hello **Stream Analytics Jobs** node and select **Export tooNew Stream Analytics Project**.</span></span>

![TooNew Stream Analytics Project exporteren](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="93926-264">Hallo-project is gegenereerd op **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="93926-264">hello project is generated in **Solution Explorer**.</span></span>

![Project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="93926-266">U ook kunt gebruiken Hallo taak weergeven en klik op **genereren Project**.</span><span class="sxs-lookup"><span data-stu-id="93926-266">You also can use hello job view, and click **Generate Project**.</span></span>

![Genereren van Project](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="93926-268">Bekende problemen en beperkingen</span><span class="sxs-lookup"><span data-stu-id="93926-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="93926-269">Er is geen ondersteuning voor Power BI-uitvoer en Azure Date Lake Store-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="93926-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="93926-270">Er is geen editor-ondersteuning voor het toevoegen of wijzigen van de gebruiker gedefinieerde functies van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="93926-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="93926-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="93926-271">Next steps</span></span>
* [<span data-ttu-id="93926-272">Inleiding tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="93926-272">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="93926-273">Aan de slag met behulp van Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="93926-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="93926-274">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="93926-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="93926-275">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="93926-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="93926-276">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="93926-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

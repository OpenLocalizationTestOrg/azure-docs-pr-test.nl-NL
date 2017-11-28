---
title: Azure Stream Analytics-hulpprogramma's voor Visual Studio gebruiken | Microsoft Docs
description: Zelfstudie voor de Azure Stream Analytics-Tools voor Visual Studio aan de slag
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
ms.openlocfilehash: 618c1055795a75e0ed71dacddba3e076f81f4946
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-stream-analytics-tools-for-visual-studio"></a><span data-ttu-id="6292f-104">Azure Stream Analytics-hulpprogramma's voor Visual Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="6292f-104">Use Azure Stream Analytics Tools for Visual Studio</span></span>
## <a name="introduction"></a><span data-ttu-id="6292f-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="6292f-105">Introduction</span></span>
<span data-ttu-id="6292f-106">In deze zelfstudie leert u hoe u met Azure Stream Analytics-Tools voor Visual Studio maken, ontwerpen, lokaal testen, beheren en fouten opsporen in uw Stream Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="6292f-106">In this tutorial, you learn how to use Azure Stream Analytics Tools for Visual Studio to create, author, test locally, manage, and debug your Stream Analytics jobs.</span></span> 

<span data-ttu-id="6292f-107">Na het voltooien van deze zelfstudie, kunt u zich kunt:</span><span class="sxs-lookup"><span data-stu-id="6292f-107">After completing this tutorial, you will be able to:</span></span>
* <span data-ttu-id="6292f-108">Tijd om uzelf bekend met Stream Analytics-hulpprogramma's voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6292f-108">Familiarize yourself with Stream Analytics Tools for Visual Studio.</span></span>
* <span data-ttu-id="6292f-109">Configureren en implementeren van een Stream Analytics-taak.</span><span class="sxs-lookup"><span data-stu-id="6292f-109">Configure and deploy a Stream Analytics job.</span></span>
* <span data-ttu-id="6292f-110">Test uw taak lokaal met lokale voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="6292f-110">Test your job locally with local sample data.</span></span>
* <span data-ttu-id="6292f-111">Gebruik controle met het oplossen van problemen.</span><span class="sxs-lookup"><span data-stu-id="6292f-111">Use monitoring to troubleshoot issues.</span></span>
* <span data-ttu-id="6292f-112">Bestaande taken exporteren naar projecten.</span><span class="sxs-lookup"><span data-stu-id="6292f-112">Export existing jobs to projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6292f-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6292f-113">Prerequisites</span></span>
<span data-ttu-id="6292f-114">Voor het voltooien van deze zelfstudie moet aan de volgende vereisten worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="6292f-114">To complete this tutorial, you need the following prerequisites:</span></span>
* <span data-ttu-id="6292f-115">Voltooi de stappen die worden voorafgegaan door 'Een Stream Analytics-taak maken' de [een IoT-oplossing bouwen met behulp van de Stream Analytics-zelfstudie](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="6292f-115">Finish the steps that precede "Create a Stream Analytics job" in the [Build an IoT solution by using Stream Analytics tutorial](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-build-an-iot-solution-using-stream-analytics).</span></span> 
* <span data-ttu-id="6292f-116">Gebruik Visual Studio 2015, Visual Studio 2013 update 4 of Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="6292f-116">Use Visual Studio 2015, Visual Studio 2013 update 4, or Visual Studio 2012.</span></span> <span data-ttu-id="6292f-117">Enterprise (Ultimate/Premium), Professional en Community-edities worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6292f-117">Enterprise (Ultimate/Premium), Professional, and Community editions are supported.</span></span> <span data-ttu-id="6292f-118">Express edition wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6292f-118">Express edition is not supported.</span></span> <span data-ttu-id="6292f-119">Visual Studio 2017 wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6292f-119">Visual Studio 2017 is not supported.</span></span> 
* <span data-ttu-id="6292f-120">Gebruik de Azure SDK voor .NET versie 2.7.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6292f-120">Use the Azure SDK for .NET version 2.7.1 or later.</span></span> <span data-ttu-id="6292f-121">U kunt dit installeren met het [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="6292f-121">Install it by using the [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="6292f-122">Installeer de [Stream Analytics-hulpprogramma's voor Visual Studio](http://aka.ms/asatoolsvs).</span><span class="sxs-lookup"><span data-stu-id="6292f-122">Install the [Stream Analytics Tools for Visual Studio](http://aka.ms/asatoolsvs).</span></span>

## <a name="create-a-stream-analytics-project"></a><span data-ttu-id="6292f-123">Een Stream Analytics-project maken</span><span class="sxs-lookup"><span data-stu-id="6292f-123">Create a Stream Analytics project</span></span>
1. <span data-ttu-id="6292f-124">Klik in Visual Studio de **bestand** menu en selecteer **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="6292f-124">In Visual Studio, click the **File** menu and select **New Project**.</span></span> 

2. <span data-ttu-id="6292f-125">Selecteer in de lijst met sjablonen aan de linkerkant **Stream Analytics** en klik vervolgens op **Azure Stream Analytics toepassing**.</span><span class="sxs-lookup"><span data-stu-id="6292f-125">In the templates list on the left, select **Stream Analytics** and then click **Azure Stream Analytics Application**.</span></span>

3. <span data-ttu-id="6292f-126">Voer het project **naam**, **locatie**, en **oplossingsnaam** als voor andere projecten.</span><span class="sxs-lookup"><span data-stu-id="6292f-126">Enter the project **Name**, **Location**, and **Solution name** as you do for other projects.</span></span>

    ![Nieuw Project-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-01.png)

    <span data-ttu-id="6292f-128">Een **Tolstation** project is gegenereerd op **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6292f-128">A **Toll** project is generated in **Solution Explorer**.</span></span>

    ![Tolstation project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-create-project-02.png)

## <a name="choose-the-correct-subscription"></a><span data-ttu-id="6292f-130">Kies het juiste abonnement</span><span class="sxs-lookup"><span data-stu-id="6292f-130">Choose the correct subscription</span></span>
1. <span data-ttu-id="6292f-131">Klik in Visual Studio de **weergave** menu en open **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6292f-131">In Visual Studio, click the **View** menu and open **Server Explorer**.</span></span>

2. <span data-ttu-id="6292f-132">Meld u aan met uw Azure-Account.</span><span class="sxs-lookup"><span data-stu-id="6292f-132">Sign in with your Azure Account.</span></span> 

## <a name="define-the-input-sources"></a><span data-ttu-id="6292f-133">De invoerbronnen definiëren</span><span class="sxs-lookup"><span data-stu-id="6292f-133">Define the input sources</span></span>
1.  <span data-ttu-id="6292f-134">In **Solution Explorer**, vouw de **invoer** knooppunt en wijzig de naam **Input.json** naar **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="6292f-134">In **Solution Explorer**, expand the **Inputs** node and rename **Input.json** to **EntryStream.json**.</span></span> <span data-ttu-id="6292f-135">Dubbelklik op **EntryStream.json**.</span><span class="sxs-lookup"><span data-stu-id="6292f-135">Double-click **EntryStream.json**.</span></span>
2.  <span data-ttu-id="6292f-136">De **invoer Alias** is nu **EntryStream**.</span><span class="sxs-lookup"><span data-stu-id="6292f-136">The **Input Alias** is now **EntryStream**.</span></span> <span data-ttu-id="6292f-137">De ingevoerde alias is in het query-script gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6292f-137">The input alias is used in the query script.</span></span> 
3.  <span data-ttu-id="6292f-138">In **brontype**, selecteer **gegevensstroom**.</span><span class="sxs-lookup"><span data-stu-id="6292f-138">In **Source Type**, select **Data Stream**.</span></span>
4.  <span data-ttu-id="6292f-139">In **bron**, selecteer **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="6292f-139">In **Source**, select **Event Hub**.</span></span>
5.  <span data-ttu-id="6292f-140">In **Service Bus Namespace**, selecteer de **TollData** optie.</span><span class="sxs-lookup"><span data-stu-id="6292f-140">In **Service Bus Namespace**, select the **TollData** option.</span></span>
6.  <span data-ttu-id="6292f-141">In **naam Event Hub**, selecteer **vermelding**.</span><span class="sxs-lookup"><span data-stu-id="6292f-141">In **Event Hub Name**, select **entry**.</span></span>
7.  <span data-ttu-id="6292f-142">In **Event Hub-beleidsnaam**, selecteer **RootManageSharedAccessKey** (de standaardwaarde).</span><span class="sxs-lookup"><span data-stu-id="6292f-142">In **Event Hub Policy Name**, select **RootManageSharedAccessKey** (the default value).</span></span>
8.  <span data-ttu-id="6292f-143">In **gebeurtenis serialisatie-indeling**, selecteer **Json**.</span><span class="sxs-lookup"><span data-stu-id="6292f-143">In **Event Serialization Format**, select **Json**.</span></span> 
9.  <span data-ttu-id="6292f-144">In **codering**, selecteer **UTF8**.</span><span class="sxs-lookup"><span data-stu-id="6292f-144">In **Encoding**, select **UTF8**.</span></span> <span data-ttu-id="6292f-145">Uw instellingen moeten eruitzien als in de volgende schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="6292f-145">Your settings should look like the following screenshot:</span></span>

    ![Invoer-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-01.png)
 
10. <span data-ttu-id="6292f-147">Klik op om de wizard **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6292f-147">To finish the wizard, click **Save**.</span></span> <span data-ttu-id="6292f-148">U kunt nu een andere invoer bron voor het maken van de stroom afsluiten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="6292f-148">Now you can add another input source to create the exit stream.</span></span> <span data-ttu-id="6292f-149">Met de rechtermuisknop op de **invoer** uit en selecteer **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="6292f-149">Right-click the **Inputs** node, and select **New Item**.</span></span>

    ![Nieuw Item](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-02.png)
 
11. <span data-ttu-id="6292f-151">Selecteer in het venster **Azure Stream Analytics invoer**, en wijzig de **naam** naar **ExitStream.json**.</span><span class="sxs-lookup"><span data-stu-id="6292f-151">In the window, select **Azure Stream Analytics Input**, and change the **Name** to **ExitStream.json**.</span></span> <span data-ttu-id="6292f-152">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="6292f-152">Click **Add**.</span></span>

    ![Venster Nieuw Item toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-03.png)
 
12. <span data-ttu-id="6292f-154">Dubbelklik op **ExitStream.json** in het project en volg dezelfde stappen als u voor de post-stroom heeft.</span><span class="sxs-lookup"><span data-stu-id="6292f-154">Double-click **ExitStream.json** in the project, and follow the same steps as you did for the entry stream.</span></span> <span data-ttu-id="6292f-155">Voer **sluiten** voor de **naam Event Hub** zoals weergegeven in de volgende schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="6292f-155">Be sure to enter **exit** for the **Event Hub Name** as shown in the following screenshot:</span></span>

    ![ExitStream venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-04.png)

    <span data-ttu-id="6292f-157">U hebt nu twee invoer streams gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="6292f-157">Now you have defined two input streams:</span></span>

    ![Toegang naar en uitgang invoer stromen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-05.png)
 
    <span data-ttu-id="6292f-159">Voeg vervolgens de gegevensinvoer verwijzing voor het blob-bestand dat de registratiegegevens auto bevat.</span><span class="sxs-lookup"><span data-stu-id="6292f-159">Next, add reference data input for the blob file that contains car registration data.</span></span>

13. <span data-ttu-id="6292f-160">Met de rechtermuisknop op de **invoer** knooppunt in het project en volg dezelfde stappen als bij de invoer van de stroom.</span><span class="sxs-lookup"><span data-stu-id="6292f-160">Right-click the **Inputs** node in the project, and then follow the same steps as you did for the stream inputs.</span></span> <span data-ttu-id="6292f-161">In **invoer Alias**, voer **registratie**, en in **brontype**, selecteer **referentiegegevens**.</span><span class="sxs-lookup"><span data-stu-id="6292f-161">In **Input Alias**, enter **Registration**, and in **Source Type**, select **Reference data**.</span></span>

    ![Registratie-venster](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-input-06.png)

14. <span data-ttu-id="6292f-163">In **Opslagaccount**, selecteer de **tolldata** optie.</span><span class="sxs-lookup"><span data-stu-id="6292f-163">In **Storage Account**, select the **tolldata** option.</span></span> <span data-ttu-id="6292f-164">In **Container**, selecteer **tolldata**, en in **pad patroon**, voer **registration.json**.</span><span class="sxs-lookup"><span data-stu-id="6292f-164">In **Container**, select **tolldata**, and in **Path Pattern**, enter **registration.json**.</span></span> <span data-ttu-id="6292f-165">Deze naam is hoofdlettergevoelig en moet in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="6292f-165">This file name is case sensitive and should be lowercase.</span></span>
15. <span data-ttu-id="6292f-166">Klik op om de wizard **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6292f-166">To finish the wizard, click **Save**.</span></span>

<span data-ttu-id="6292f-167">Nu zijn de invoer gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="6292f-167">Now all the inputs are defined.</span></span>

## <a name="define-the-output"></a><span data-ttu-id="6292f-168">De uitvoer definiëren</span><span class="sxs-lookup"><span data-stu-id="6292f-168">Define the output</span></span>
1.  <span data-ttu-id="6292f-169">In **Solution Explorer**, vouw de **invoer** knooppunt en dubbelklik op **Output.json**.</span><span class="sxs-lookup"><span data-stu-id="6292f-169">In **Solution Explorer**, expand the **Inputs** node and double-click **Output.json**.</span></span>

2.  <span data-ttu-id="6292f-170">In **Uitvoeraliassen**, voer **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="6292f-170">In **Output Alias**, enter **output**.</span></span> 
3.  <span data-ttu-id="6292f-171">In **Sink**, selecteer **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="6292f-171">In **Sink**, select **SQL Database**.</span></span>
4.  <span data-ttu-id="6292f-172">In **Database**, selecteer **TollDataDB**.</span><span class="sxs-lookup"><span data-stu-id="6292f-172">In **Database**, select **TollDataDB**.</span></span>
5.  <span data-ttu-id="6292f-173">In **gebruikersnaam**, voer **tolladmin**.</span><span class="sxs-lookup"><span data-stu-id="6292f-173">In **User Name**, enter **tolladmin**.</span></span> 
6.  <span data-ttu-id="6292f-174">In **wachtwoord**, voer **123toll!**.</span><span class="sxs-lookup"><span data-stu-id="6292f-174">In **Password**, enter **123toll!**.</span></span>
7.  <span data-ttu-id="6292f-175">In **tabel**, voer **TollDataRefJoin**.</span><span class="sxs-lookup"><span data-stu-id="6292f-175">In **Table**, enter **TollDataRefJoin**.</span></span>
8.  <span data-ttu-id="6292f-176">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6292f-176">Click **Save**.</span></span>

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-define-output-01.png)
 
## <a name="create-a-stream-analytics-query"></a><span data-ttu-id="6292f-178">Een Stream Analytics query maken</span><span class="sxs-lookup"><span data-stu-id="6292f-178">Create a Stream Analytics query</span></span>
<span data-ttu-id="6292f-179">Deze zelfstudie probeert verschillende bedrijven vragen die zijn gerelateerd aan gegevens tolbruggen te beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="6292f-179">This tutorial attempts to answer several business questions that are related to toll data.</span></span> <span data-ttu-id="6292f-180">Dit wordt ook Stream Analytics query's die kunnen worden gebruikt in de Stream Analytics relevante beantwoorden.</span><span class="sxs-lookup"><span data-stu-id="6292f-180">It also constructs Stream Analytics queries that can be used in Stream Analytics to provide relevant answers.</span></span>
<span data-ttu-id="6292f-181">Voordat u uw eerste Stream Analytics-taak, gaan we een eenvoudig scenario en de querysyntaxis verkennen.</span><span class="sxs-lookup"><span data-stu-id="6292f-181">Before you start your first Stream Analytics job, let’s explore a simple scenario and the query syntax.</span></span>

### <a name="introduction-to-the-stream-analytics-query-language"></a><span data-ttu-id="6292f-182">Inleiding tot de Stream Analytics query language</span><span class="sxs-lookup"><span data-stu-id="6292f-182">Introduction to the Stream Analytics query language</span></span>
<span data-ttu-id="6292f-183">Stel dat u moet het aantal voertuigen die een tolstation stand invoeren.</span><span class="sxs-lookup"><span data-stu-id="6292f-183">Let’s say that you need to count the number of vehicles that enter a toll booth.</span></span> <span data-ttu-id="6292f-184">Omdat dit voorbeeld een continue stroom van gebeurtenissen is, hebt u voor het definiëren van een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="6292f-184">Because this example is a continuous stream of events, you have to define a period of time.</span></span> <span data-ttu-id="6292f-185">Wijzig de vraag om 'hoeveel voertuigen Geef een tolstation stand elke drie minuten?'</span><span class="sxs-lookup"><span data-stu-id="6292f-185">Modify the question to be “How many vehicles enter a toll booth every three minutes?”</span></span> <span data-ttu-id="6292f-186">Deze manier om gegevens te tellen wordt vaak aangeduid als het aantal daling.</span><span class="sxs-lookup"><span data-stu-id="6292f-186">This way to count data is commonly referred to as the tumbling count.</span></span>

<span data-ttu-id="6292f-187">Bekijk de Stream Analytics query waarmee deze vraag worden beantwoord:</span><span class="sxs-lookup"><span data-stu-id="6292f-187">Look at the Stream Analytics query that answers this question:</span></span>

        SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count 
        FROM EntryStream TIMESTAMP BY EntryTime 
        GROUP BY TUMBLINGWINDOW(minute, 3), TollId 

<span data-ttu-id="6292f-188">Stream Analytics maakt gebruik van een querytaal die lijkt op SQL en enkele uitbreidingen om op te geven tijd gerelateerde aspecten van de query toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6292f-188">Stream Analytics uses a query language that's like SQL and adds a few extensions to specify time-related aspects of the query.</span></span>

<span data-ttu-id="6292f-189">Zie voor meer informatie [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) en [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructies die worden gebruikt in de query van MSDN.</span><span class="sxs-lookup"><span data-stu-id="6292f-189">For more information, see [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) constructs used in the query from MSDN.</span></span>

<span data-ttu-id="6292f-190">Nu u uw eerste Stream Analytics query hebt geschreven, is het tijd om deze te testen.</span><span class="sxs-lookup"><span data-stu-id="6292f-190">Now that you have written your first Stream Analytics query, it's time to test it.</span></span> <span data-ttu-id="6292f-191">Gebruik de bestanden met voorbeeldgegevens zich in de map TollApp in het volgende pad:</span><span class="sxs-lookup"><span data-stu-id="6292f-191">Use the sample data files located in your TollApp folder in the following path:</span></span>

<span data-ttu-id="6292f-192">.. \TollApp\TollApp\Data</span><span class="sxs-lookup"><span data-stu-id="6292f-192">..\TollApp\TollApp\Data</span></span>

<span data-ttu-id="6292f-193">Deze map bevat de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="6292f-193">This folder contains the following files:</span></span>
*   <span data-ttu-id="6292f-194">Entry.JSON</span><span class="sxs-lookup"><span data-stu-id="6292f-194">Entry.json</span></span>
*   <span data-ttu-id="6292f-195">Exit.JSON</span><span class="sxs-lookup"><span data-stu-id="6292f-195">Exit.json</span></span>
*   <span data-ttu-id="6292f-196">Registration.JSON</span><span class="sxs-lookup"><span data-stu-id="6292f-196">Registration.json</span></span>

## <a name="count-the-number-of-vehicles-entering-a-toll-booth"></a><span data-ttu-id="6292f-197">Het aantal voertuigen een tolstation stand tellen</span><span class="sxs-lookup"><span data-stu-id="6292f-197">Count the number of vehicles entering a toll booth</span></span>
<span data-ttu-id="6292f-198">Dubbelklik in het project op **Script.asaql** openen van het script in de **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="6292f-198">In the project, double-click **Script.asaql** to open the script in the **Query Editor**.</span></span> <span data-ttu-id="6292f-199">Kopieer en plak het script in de vorige sectie in de editor.</span><span class="sxs-lookup"><span data-stu-id="6292f-199">Copy and paste the script in the previous section into the editor.</span></span> <span data-ttu-id="6292f-200">De Query-Editor biedt ondersteuning voor IntelliSense syntaxiskleuren en de markering van de fout.</span><span class="sxs-lookup"><span data-stu-id="6292f-200">The Query Editor supports IntelliSense, syntax coloring, and the error marker.</span></span>

![Query-Editor](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-query-01.png)
 
### <a name="test-stream-analytics-queries-locally"></a><span data-ttu-id="6292f-202">Stream Analytics query's lokaal testen</span><span class="sxs-lookup"><span data-stu-id="6292f-202">Test Stream Analytics queries locally</span></span>

1. <span data-ttu-id="6292f-203">Compileren van de query om te zien of er een syntaxisfout, met de rechtermuisknop op het project en selecteer **bouwen**.</span><span class="sxs-lookup"><span data-stu-id="6292f-203">To compile the query to see if there is a syntax error, right-click the project and select **Build**.</span></span> 

2. <span data-ttu-id="6292f-204">Voor het valideren van deze query op de voorbeeldgegevens, kunt u lokale voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="6292f-204">To validate this query against sample data, you can use local sample data.</span></span> <span data-ttu-id="6292f-205">Met de rechtermuisknop op de invoer en selecteer **lokale invoer toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="6292f-205">Right-click the input, and select **Add local input**.</span></span>

    ![Lokale invoer toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-01.png)
 
3. <span data-ttu-id="6292f-207">Selecteer de voorbeeldgegevens van uw lokale pad in het pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="6292f-207">In the pop-up window, select the sample data from your local path.</span></span> <span data-ttu-id="6292f-208">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="6292f-208">Click **Save**.</span></span>

    ![Lokale invoer venster toevoegen](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-02.png)
 
    <span data-ttu-id="6292f-210">Een bestand met de naam **local_EntryStream.json** wordt automatisch toegevoegd aan de map van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="6292f-210">A file named **local_EntryStream.json** is automatically added to your inputs folder.</span></span>

    ![Bestand toegevoegd aan de map invoer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-add-local-input-03.png)
 
4. <span data-ttu-id="6292f-212">In de **Query-Editor**, klikt u op **lokaal uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="6292f-212">In the **Query Editor**, click **Run Locally**.</span></span> <span data-ttu-id="6292f-213">Of u kunt ook op F5 drukken.</span><span class="sxs-lookup"><span data-stu-id="6292f-213">Or you can press the F5 key.</span></span>

    ![Lokaal uitvoeren](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-01.png)

    ![Lokaal uitvoeren van uitvoer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-local-run-02.png)

    <span data-ttu-id="6292f-216">Druk op een willekeurige toets om weer te geven van de uitvoer in de **ASA lokale uitvoeren resultaat** venster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6292f-216">Press any key to view the output in the **ASA Local Run Result** window in Visual Studio.</span></span> 

    ![Venster ASA lokale uitvoeren resultaat](./media/stream-analytics-tools-for-vs/local-testing-output.png)

5. <span data-ttu-id="6292f-218">Klik op **geopende resultaat map** om te controleren van de uitvoerbestanden beide in CSV en JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="6292f-218">Click **Open Result Folder** to check the output files both in CSV and JSON format.</span></span>

    ![Open resultaat map uitvoer](./media/stream-analytics-tools-for-vs/local-testing-files.png)
 

### <a name="sample-the-input-data"></a><span data-ttu-id="6292f-220">Voorbeeld van de invoergegevens</span><span class="sxs-lookup"><span data-stu-id="6292f-220">Sample the input data</span></span>
<span data-ttu-id="6292f-221">U kunt ook invoer voorbeeldgegevens uit invoerbronnen naar een lokaal bestand.</span><span class="sxs-lookup"><span data-stu-id="6292f-221">You can also sample input data from input sources to a local file.</span></span> 
1. <span data-ttu-id="6292f-222">Met de rechtermuisknop op het configuratiebestand van de invoer en selecteer **voorbeeldgegevens**.</span><span class="sxs-lookup"><span data-stu-id="6292f-222">Right-click the input config file, and select **Sample Data**.</span></span> 

   ![Voorbeeldgegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-01.png)

    <span data-ttu-id="6292f-224">U kunt alleen de event hub of -IoT-hub steekproef nemen nu.</span><span class="sxs-lookup"><span data-stu-id="6292f-224">You can sample only event hub or IoT hub for now.</span></span> <span data-ttu-id="6292f-225">Andere bronnen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6292f-225">Other input sources are not supported.</span></span>

2. <span data-ttu-id="6292f-226">Geef het lokale pad gebruikt voor het opslaan van de voorbeeldgegevens in het pop-upvenster.</span><span class="sxs-lookup"><span data-stu-id="6292f-226">In the pop-up window, enter the local path used to save the sample data.</span></span> <span data-ttu-id="6292f-227">Klik op **voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="6292f-227">Click **Sample**.</span></span>

    ![Venster van de gegevens voorbeeld](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-02.png)
 
    <span data-ttu-id="6292f-229">U ziet de voortgang in de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="6292f-229">You can see the progress in the **Output** window.</span></span> 

    ![Venster Output](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-sample-data-03.png)
 
### <a name="submit-a-stream-analytics-query-to-azure"></a><span data-ttu-id="6292f-231">Verzenden van een Stream Analytics-query naar Azure</span><span class="sxs-lookup"><span data-stu-id="6292f-231">Submit a Stream Analytics query to Azure</span></span>
1. <span data-ttu-id="6292f-232">In de **Query-Editor**, klikt u op **verzenden naar Azure** in de scripteditor.</span><span class="sxs-lookup"><span data-stu-id="6292f-232">In the **Query Editor**, click **Submit To Azure** in the script editor.</span></span>

    ![Verzenden naar Azure](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-01.png)
 
2. <span data-ttu-id="6292f-234">Selecteer **maken van een nieuwe Azure Stream Analytics-taak**.</span><span class="sxs-lookup"><span data-stu-id="6292f-234">Select **Create a New Azure Stream Analytics Job**.</span></span> <span data-ttu-id="6292f-235">Voer de **taaknaam**, en selecteer de juiste **abonnement**.</span><span class="sxs-lookup"><span data-stu-id="6292f-235">Enter the **Job Name**, and select the correct **Subscription**.</span></span> <span data-ttu-id="6292f-236">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="6292f-236">Click **Submit**.</span></span>

    ![Venster van de taak verzenden](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-submit-job-02.png)

 
### <a name="start-a-job"></a><span data-ttu-id="6292f-238">Een taak starten</span><span class="sxs-lookup"><span data-stu-id="6292f-238">Start a job</span></span>
<span data-ttu-id="6292f-239">Nu dat de taak is gemaakt, wordt de taakweergave wordt automatisch geopend.</span><span class="sxs-lookup"><span data-stu-id="6292f-239">Now that your job is created, the job view is automatically opened.</span></span> 
1. <span data-ttu-id="6292f-240">De taak starten, klikt u op de **groene pijl** knop.</span><span class="sxs-lookup"><span data-stu-id="6292f-240">To start the job, click the **green arrow** button.</span></span>

    ![Een taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-01.png)
 
2. <span data-ttu-id="6292f-242">De standaardinstelling selecteren en op **Start**.</span><span class="sxs-lookup"><span data-stu-id="6292f-242">Select the default setting, and click **Start**.</span></span>
 
    ![Venster van de taak starten](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-02.png)

    <span data-ttu-id="6292f-244">De taak **Status** wijzigingen in **met**, en **invoer gebeurtenissen** en **Uitvoergebeurtenissen** worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6292f-244">The job **Status** changes to **Running**, and **Input Events** and **Output Events** appear.</span></span>

    ![Uitvoeringsstatus in Taakoverzicht](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-start-job-03.png)

## <a name="check-the-results-in-visual-studio"></a><span data-ttu-id="6292f-246">De resultaten controleren in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6292f-246">Check the results in Visual Studio</span></span>
1. <span data-ttu-id="6292f-247">Open in Visual Studio **Server Explorer** met de rechtermuisknop op de **TollDataRefJoin** tabel.</span><span class="sxs-lookup"><span data-stu-id="6292f-247">In Visual Studio, open **Server Explorer** and right-click the **TollDataRefJoin** table.</span></span>
2. <span data-ttu-id="6292f-248">Selecteer **tabelgegevens weergeven** om te zien van de uitvoer van de taak.</span><span class="sxs-lookup"><span data-stu-id="6292f-248">Select **Show Table Data** to see the output of your job.</span></span>
   
    ![Selectie van de tabelgegevens weergeven in Server Explorer](media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-check-results.jpg)


### <a name="view-the-job-metrics"></a><span data-ttu-id="6292f-250">De taak metrische gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="6292f-250">View the job metrics</span></span>
<span data-ttu-id="6292f-251">Een aantal statistieken basic taak kunt u vinden in **taak metrische gegevens**.</span><span class="sxs-lookup"><span data-stu-id="6292f-251">Some basic job statistics can be found in **Job Metrics**.</span></span> 

![Venster van de taak metrische gegevens](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-metrics-01.png)

 
## <a name="list-the-job-in-server-explorer"></a><span data-ttu-id="6292f-253">Lijst van de taak in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="6292f-253">List the job in Server Explorer</span></span>
<span data-ttu-id="6292f-254">In **Server Explorer**, klikt u op **Stream Analytics-taken** en klik vervolgens op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="6292f-254">In **Server Explorer**, click **Stream Analytics Jobs** and then click **Refresh**.</span></span> <span data-ttu-id="6292f-255">De taak wordt weergegeven onder **Stream Analytics-taken**.</span><span class="sxs-lookup"><span data-stu-id="6292f-255">The job appears under **Stream Analytics jobs**.</span></span>

![Stream Analytics-taken die worden vermeld in Server Explorer](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-list-jobs-01.png)


## <a name="open-the-job-view"></a><span data-ttu-id="6292f-257">De taakweergave openen</span><span class="sxs-lookup"><span data-stu-id="6292f-257">Open the job view</span></span>
<span data-ttu-id="6292f-258">De als taakweergave wilt openen, vouw het knooppunt van uw project en dubbelklik op de **taakweergave** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6292f-258">To open the job view, expand your job node and double-click the **Job View** node.</span></span>

![Knooppunt van de taak weergeven](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-job-view-01.png)


## <a name="export-an-existing-job-to-a-project"></a><span data-ttu-id="6292f-260">Exporteren van een bestaande taak aan een project</span><span class="sxs-lookup"><span data-stu-id="6292f-260">Export an existing job to a project</span></span>
<span data-ttu-id="6292f-261">Er zijn twee manieren kunt u een bestaande taak exporteren naar een project.</span><span class="sxs-lookup"><span data-stu-id="6292f-261">There are two ways you can export an existing job to a project.</span></span>

<span data-ttu-id="6292f-262">In **Server Explorer**, met de rechtermuisknop op het taakknooppunt in de **Stream Analytics-taken** uit en selecteer **exporteren naar nieuwe Stream Analytics-Project**.</span><span class="sxs-lookup"><span data-stu-id="6292f-262">In **Server Explorer**, right-click the job node in the **Stream Analytics Jobs** node and select **Export to New Stream Analytics Project**.</span></span>

![Exporteren naar nieuwe Stream Analytics-Project](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-01.png)

<span data-ttu-id="6292f-264">Het project is gegenereerd op **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6292f-264">The project is generated in **Solution Explorer**.</span></span>

![Project in Solution Explorer gegenereerd](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-02.png)
 
<span data-ttu-id="6292f-266">U ook kunt gebruiken de Project-weergave, en klik op **genereren Project**.</span><span class="sxs-lookup"><span data-stu-id="6292f-266">You also can use the job view, and click **Generate Project**.</span></span>

![Genereren van Project](./media/stream-analytics-tools-for-vs/stream-analytics-tools-for-vs-export-job-03.png)

## <a name="known-issues-and-limitations"></a><span data-ttu-id="6292f-268">Bekende problemen en beperkingen</span><span class="sxs-lookup"><span data-stu-id="6292f-268">Known issues and limitations</span></span>
 
- <span data-ttu-id="6292f-269">Er is geen ondersteuning voor Power BI-uitvoer en Azure Date Lake Store-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6292f-269">There is no support for Power BI output and Azure Date Lake Store output.</span></span>
- <span data-ttu-id="6292f-270">Er is geen editor-ondersteuning voor het toevoegen of wijzigen van de gebruiker gedefinieerde functies van JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6292f-270">There is no editor support for adding or changing JavaScript user-defined functions.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6292f-271">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6292f-271">Next steps</span></span>
* [<span data-ttu-id="6292f-272">Inleiding tot Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6292f-272">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6292f-273">Aan de slag met behulp van Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6292f-273">Get started by using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6292f-274">Azure Stream Analytics-taken schalen</span><span class="sxs-lookup"><span data-stu-id="6292f-274">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6292f-275">Naslaggids voor Azure Stream Analytics Query</span><span class="sxs-lookup"><span data-stu-id="6292f-275">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6292f-276">REST API-naslaggids voor Azure Stream Analytics Management</span><span class="sxs-lookup"><span data-stu-id="6292f-276">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

---
title: Maken en herstellen van een back-up in BizTalk Services | Microsoft Docs
description: BizTalk Services omvat back-up en herstel. Meer informatie over het maken en herstellen van een back-up om te bepalen wat opgehaald back-up gemaakt. MABS, WABS
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 59f91173-4683-48df-abd5-41262bfce6df
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c55d1ab124441c42101b4ad60924a9ea28231408
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="2d014-105">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="2d014-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="2d014-106">Azure BizTalk Services bevat de mogelijkheden van back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="2d014-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="2d014-107">Dit onderwerp wordt beschreven hoe u back-up en herstellen van BizTalk Services met behulp van de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d014-107">This topic describes how to backup and restore BizTalk Services using the Azure classic portal.</span></span>

<span data-ttu-id="2d014-108">U kunt ook back-up met behulp van BizTalk Services de [REST-API van BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="2d014-108">You can also back up BizTalk Services using the [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="2d014-109">Hybride verbindingen zijn geen back-up, ongeacht de editie.</span><span class="sxs-lookup"><span data-stu-id="2d014-109">Hybrid Connections are NOT backed up, regardless of the Edition.</span></span> <span data-ttu-id="2d014-110">U moet uw hybride verbindingen opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="2d014-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="2d014-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="2d014-111">Before you Begin</span></span>
* <span data-ttu-id="2d014-112">Back-up en herstel mogelijk niet beschikbaar voor alle edities.</span><span class="sxs-lookup"><span data-stu-id="2d014-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="2d014-113">Zie [BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="2d014-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="2d014-114">Met de klassieke Azure portal, kunt u een On Demand back-up maken of een geplande back-up maken.</span><span class="sxs-lookup"><span data-stu-id="2d014-114">Using the Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="2d014-115">Back-inhoud kan worden hersteld naar dezelfde BizTalk Service of naar een nieuwe BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2d014-115">Backup content can be restored to the same BizTalk Service or to a new BizTalk Service.</span></span> <span data-ttu-id="2d014-116">Voor het herstellen van de BizTalk Service gebruikt dezelfde naam, de bestaande BizTalk-Service moet worden verwijderd en de naam moet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="2d014-116">To restore the BizTalk Service using the same name, the existing BizTalk Service must be deleted and the name must be available.</span></span> <span data-ttu-id="2d014-117">Nadat u een BizTalk Service hebt verwijderd, kan duren langer dan wilden voor dezelfde naam beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2d014-117">After you delete a BizTalk Service, it can take longer time than wanted for the same name to be available.</span></span> <span data-ttu-id="2d014-118">Als u dezelfde naam beschikbaar niet kunt wachten, zet u een nieuwe BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2d014-118">If you cannot wait for the same name to be available, then restore to a new BizTalk Service.</span></span>
* <span data-ttu-id="2d014-119">BizTalk Services kunnen worden hersteld naar dezelfde versie of een hogere editie.</span><span class="sxs-lookup"><span data-stu-id="2d014-119">BizTalk Services can be restored to the same edition or a higher edition.</span></span> <span data-ttu-id="2d014-120">BizTalk Services is teruggezet naar een lagere versie, wordt uit wanneer de back-up is gemaakt, niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="2d014-120">Restoring BizTalk Services to a lower edition, from when the backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="2d014-121">Bijvoorbeeld, kan een back-up met behulp van de Basic-editie worden hersteld naar de Premium-versie.</span><span class="sxs-lookup"><span data-stu-id="2d014-121">For example, a backup using the Basic Edition can be restored to the Premium Edition.</span></span> <span data-ttu-id="2d014-122">Een back-up met behulp van de Premium-versie kan niet worden hersteld naar de Standard-editie.</span><span class="sxs-lookup"><span data-stu-id="2d014-122">A backup using the Premium Edition cannot be restored to the Standard Edition.</span></span>
* <span data-ttu-id="2d014-123">De getallen EDI-besturingselement worden back-up continuïteit van de getallen besturingselement.</span><span class="sxs-lookup"><span data-stu-id="2d014-123">The EDI Control numbers are backed up to maintain continuity of the control numbers.</span></span> <span data-ttu-id="2d014-124">Als berichten worden verwerkt na de laatste back-up, herstellen van de inhoud van deze back-up kan leiden tot dubbele besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="2d014-124">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="2d014-125">Als een batch actieve berichten heeft, de batch verwerkt **voordat** waarop een back-up.</span><span class="sxs-lookup"><span data-stu-id="2d014-125">If a batch has active messages, process the batch **before** running a backup.</span></span> <span data-ttu-id="2d014-126">Wanneer u een back-up (als de benodigde of geplande) maakt, worden berichten in batches nooit worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2d014-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="2d014-127">**Als u een back-up wordt gemaakt met actieve berichten in een batch, wordt deze berichten worden niet een back-up en zijn daarom verloren.**</span><span class="sxs-lookup"><span data-stu-id="2d014-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="2d014-128">Optioneel: In de Portal BizTalk-Services stop alle beheerbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="2d014-128">Optional: In the BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="2d014-129">Maak een back-up</span><span class="sxs-lookup"><span data-stu-id="2d014-129">Create a backup</span></span>
<span data-ttu-id="2d014-130">Een back-up kan worden uitgevoerd op elk gewenst moment en volledig door u worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="2d014-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="2d014-131">Deze sectie vindt u de stappen voor het maken van back-ups met de klassieke Azure portal, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="2d014-131">This section lists the steps to create backups using the Azure classic portal, including:</span></span>

[<span data-ttu-id="2d014-132">Op aanvraag back-up</span><span class="sxs-lookup"><span data-stu-id="2d014-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="2d014-133">Een back-up plannen</span><span class="sxs-lookup"><span data-stu-id="2d014-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="2d014-134"><a name="backupnow"></a>Op aanvraag back-up</span><span class="sxs-lookup"><span data-stu-id="2d014-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="2d014-135">Selecteer in de klassieke Azure portal **BizTalk Services**, en selecteer vervolgens de BizTalk-Service die u wilt back-up.</span><span class="sxs-lookup"><span data-stu-id="2d014-135">In the Azure classic portal, select **BizTalk Services**, and then select the BizTalk Service you want to backup.</span></span>
2. <span data-ttu-id="2d014-136">In de **Dashboard** tabblad **Back-up** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="2d014-136">In the **Dashboard** tab, select **Back up** at the bottom of the page.</span></span>
3. <span data-ttu-id="2d014-137">Voer de naam van een back-up.</span><span class="sxs-lookup"><span data-stu-id="2d014-137">Enter a backup name.</span></span> <span data-ttu-id="2d014-138">Voer bijvoorbeeld *myBizTalkService*door*datum*.</span><span class="sxs-lookup"><span data-stu-id="2d014-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="2d014-139">Kies een blob storage-account en schakel het selectievakje voor het starten van de back-up.</span><span class="sxs-lookup"><span data-stu-id="2d014-139">Choose a blob storage account and select the checkmark to start the backup.</span></span>

<span data-ttu-id="2d014-140">Zodra de back-up is voltooid, wordt een container met de back-naam die u invoert in het opslagaccount gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2d014-140">Once the backup completes, a container with the backup name you enter is created in the storage account.</span></span> <span data-ttu-id="2d014-141">Deze container bevat uw BizTalk Service back-upconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="2d014-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="2d014-142"><a name="backupschedule"></a>Een back-up plannen</span><span class="sxs-lookup"><span data-stu-id="2d014-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="2d014-143">Selecteer in de klassieke Azure portal **BizTalk Services**, selecteert u de BizTalk Service-naam die u wilt de back-up plannen en selecteer vervolgens de **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="2d014-143">In the Azure classic portal, select **BizTalk Services**, select the BizTalk Service name you want to schedule the backup, and then select the **Configure** tab.</span></span>
2. <span data-ttu-id="2d014-144">Stel de **back-up van de Status** naar **automatische**.</span><span class="sxs-lookup"><span data-stu-id="2d014-144">Set the **Backup Status** to **Automatic**.</span></span> 
3. <span data-ttu-id="2d014-145">Selecteer de **Opslagaccount** invoeren voor het opslaan van de back-up, de **frequentie** voor het maken van de back-ups, en hoe lang de back-ups behouden (**dagen bewaren**):</span><span class="sxs-lookup"><span data-stu-id="2d014-145">Select the **Storage Account** to store the backup, enter the **Frequency** to create the backups, and how long to keep the backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="2d014-146">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="2d014-146">**Notes**</span></span>     
   
   * <span data-ttu-id="2d014-147">In **dagen bewaren**, de retentietijd moet groter zijn dan de back-upfrequentie.</span><span class="sxs-lookup"><span data-stu-id="2d014-147">In **Retention Days**, the retention period must be greater than the backup frequency.</span></span>
   * <span data-ttu-id="2d014-148">Selecteer **altijd ten minste één back-up bewaren**, zelfs als deze na de bewaarperiode valt.</span><span class="sxs-lookup"><span data-stu-id="2d014-148">Select **Always keep at least one backup**, even if it is past the retention period.</span></span>
4. <span data-ttu-id="2d014-149">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="2d014-149">Select **Save**.</span></span>

<span data-ttu-id="2d014-150">Wanneer een geplande back-uptaak wordt uitgevoerd, wordt een container (voor het opslaan van back-upgegevens) gemaakt in het opslagaccount dat u hebt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="2d014-150">When a scheduled backup job runs, it creates a container (to store backup data) in the storage account you entered.</span></span> <span data-ttu-id="2d014-151">De naam van de container met de naam *naam-/-tijd van de BizTalk Service*.</span><span class="sxs-lookup"><span data-stu-id="2d014-151">The name of the container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="2d014-152">Als de BizTalk Service-dashboard toont een **mislukt** status:</span><span class="sxs-lookup"><span data-stu-id="2d014-152">If the BizTalk Service dashboard shows a **Failed** status:</span></span>

![Status van laatste geplande back-up][BackupStatus] 

<span data-ttu-id="2d014-154">De koppeling opent de Bewerkingslogboeken van de Management-Services voor het oplossen van.</span><span class="sxs-lookup"><span data-stu-id="2d014-154">The link opens the Management Services Operation Logs to help troubleshoot.</span></span> <span data-ttu-id="2d014-155">Zie [BizTalk Services: problemen oplossen met bewerkingslogboeken](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="2d014-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="2d014-156">Herstellen</span><span class="sxs-lookup"><span data-stu-id="2d014-156">Restore</span></span>
<span data-ttu-id="2d014-157">U kunt back-ups herstellen vanuit de klassieke Azure portal of vanuit de [herstellen BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="2d014-157">You can restore backups from the Azure classic portal or from the [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="2d014-158">Deze sectie vindt u de stappen om te herstellen met de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="2d014-158">This section lists the steps to restore using the classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="2d014-159">Voordat u een back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="2d014-159">Before restoring a backup</span></span>
* <span data-ttu-id="2d014-160">Nieuwe bijhouden, archiveren en te bewaken winkels kunnen worden ingevoerd tijdens het herstellen van een BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2d014-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="2d014-161">Dezelfde EDI-Runtime-gegevens is hersteld.</span><span class="sxs-lookup"><span data-stu-id="2d014-161">The same EDI Runtime data is restored.</span></span> <span data-ttu-id="2d014-162">De back-up van EDI-Runtime slaat de besturingselement-getallen.</span><span class="sxs-lookup"><span data-stu-id="2d014-162">The EDI Runtime backup stores the control numbers.</span></span> <span data-ttu-id="2d014-163">De herstelde besturingselement-nummers zijn in volgorde van de tijd van de back-up.</span><span class="sxs-lookup"><span data-stu-id="2d014-163">The restored control numbers are in sequence from the time of the backup.</span></span> <span data-ttu-id="2d014-164">Als berichten worden verwerkt na de laatste back-up, herstellen van de inhoud van deze back-up kan leiden tot dubbele besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="2d014-164">If messages are processed after the last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="2d014-165">Een back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="2d014-165">Restore a backup</span></span>
1. <span data-ttu-id="2d014-166">Selecteer in de klassieke Azure portal **nieuw** > **App Services** > **BizTalk Service** > **herstellen**:</span><span class="sxs-lookup"><span data-stu-id="2d014-166">In the Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Een back-up terugzetten][Restore]
2. <span data-ttu-id="2d014-168">In **back-URL**, selecteert u het pictogram van de map en vouw de Azure storage-account waarmee de BizTalk Service configuratieback-up worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2d014-168">In **Backup URL**, select the folder icon and expand the Azure storage account that stores the BizTalk Service configuration backup.</span></span> <span data-ttu-id="2d014-169">Vouw de container uit en selecteer in het rechterdeelvenster de bijbehorende back-up txt-bestand.</span><span class="sxs-lookup"><span data-stu-id="2d014-169">Expand the container and in the right pane, select the corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="2d014-170">Selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="2d014-170">Select **Open**.</span></span>
3. <span data-ttu-id="2d014-171">Op de **herstellen BizTalk Service** pagina, voert u een **BizTalk-servicenaam** en controleer of de **domein-URL**, **Edition**, en **regio** voor de herstelde BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2d014-171">On the **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify the **Domain URL**, **Edition**, and **Region** for the restored BizTalk Service.</span></span> <span data-ttu-id="2d014-172">**Maak een nieuw exemplaar van SQL database** voor de database bijhouden:</span><span class="sxs-lookup"><span data-stu-id="2d014-172">**Create a new SQL database instance** for the tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="2d014-173">Selecteer de pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="2d014-173">Select the next arrow.</span></span>
4. <span data-ttu-id="2d014-174">Controleer de naam van de SQL-database, de fysieke server waar de SQL-database wordt gemaakt en een gebruikersnaam en wachtwoord invoeren voor die server.</span><span class="sxs-lookup"><span data-stu-id="2d014-174">Verify the name of the SQL database, enter the physical server where the SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="2d014-175">Als u de editie van SQL database, de grootte en andere eigenschappen configureren wilt, selecteert u **geavanceerde Database-instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="2d014-175">If you want to configure the SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="2d014-176">Selecteer de pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="2d014-176">Select the next arrow.</span></span>

1. <span data-ttu-id="2d014-177">Een nieuw opslagaccount maken of voert u een bestaand opslagaccount voor de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="2d014-177">Create a new storage account or enter an existing storage account for the BizTalk Service.</span></span>
2. <span data-ttu-id="2d014-178">Selecteer het vinkje om te beginnen met terugzetten.</span><span class="sxs-lookup"><span data-stu-id="2d014-178">Select the checkmark to start the restore.</span></span>

<span data-ttu-id="2d014-179">Nadat de herstelbewerking is voltooid, wordt een nieuwe BizTalk Service wordt vermeld in een onderbroken status op de pagina BizTalk Services in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="2d014-179">Once the restoration successfully completes, a new BizTalk Service is listed in a suspended state on the BizTalk Services page in the Azure classic portal.</span></span>

### <span data-ttu-id="2d014-180"><a name="postrestore"></a>Na het terugzetten van een back-up</span><span class="sxs-lookup"><span data-stu-id="2d014-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="2d014-181">De BizTalk Service altijd wordt hersteld een **onderbroken** status.</span><span class="sxs-lookup"><span data-stu-id="2d014-181">The BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="2d014-182">In deze toestand is, kunt u geen configuratiewijzigingen maken voordat de nieuwe omgeving functioneel is, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="2d014-182">In this state, you can make any configuration changes before the new environment is functional, including:</span></span>

* <span data-ttu-id="2d014-183">Als u een BizTalk Service-toepassingen met behulp van de Azure BizTalk Services SDK gemaakt, mogelijk moet u naar de Access Control (ACS)-referenties in die toepassingen werken met de herstelde omgeving bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2d014-183">If you created BizTalk Service applications using the Azure BizTalk Services SDK, you may need to to update the Access Control (ACS) credentials in those applications to work with the restored environment.</span></span>
* <span data-ttu-id="2d014-184">U herstelt een BizTalk Service om te repliceren van een bestaande BizTalk Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2d014-184">You restore a BizTalk Service to replicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="2d014-185">In dit geval als er zijn geconfigureerd in de oorspronkelijke BizTalk Services-portal overeenkomsten die gebruikmaken van een FTP-bronmap mogelijk moet u de overeenkomsten in de herstelde omgeving naar een andere bron FTP-map gebruiken bijwerken.</span><span class="sxs-lookup"><span data-stu-id="2d014-185">In this situation, if there are agreements configured in the original BizTalk Services portal that use a source FTP folder, you may need to update the agreements in the newly restored environment to use a different source FTP folder.</span></span> <span data-ttu-id="2d014-186">Anders kunnen er twee verschillende overeenkomsten probeert om hetzelfde bericht binnen te halen.</span><span class="sxs-lookup"><span data-stu-id="2d014-186">Otherwise, there may be two different agreements trying to pull the same message.</span></span>
* <span data-ttu-id="2d014-187">Als u voor omgevingen met meerdere BizTalk Service hebt hersteld, zorg er dan voor dat u de juiste omgeving in de Visual Studio-toepassingen, PowerShell-cmdlets, REST-API's of Trading Partner Management OM API's zijn gericht.</span><span class="sxs-lookup"><span data-stu-id="2d014-187">If you restored to have multiple BizTalk Service environments, make sure you target the correct environment in the Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="2d014-188">Het is verstandig om te configureren van automatische back-ups op de herstelde BizTalk Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="2d014-188">It's a good practice to configure automated backups on the newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="2d014-189">U start de BizTalk Service in de klassieke Azure portal, selecteer de herstelde BizTalk Service en selecteer **hervatten** in de taakbalk.</span><span class="sxs-lookup"><span data-stu-id="2d014-189">To start the BizTalk Service in the Azure classic portal, select the restored BizTalk Service and select **Resume** in the task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="2d014-190">Wat wordt een back-up</span><span class="sxs-lookup"><span data-stu-id="2d014-190">What gets backed up</span></span>
<span data-ttu-id="2d014-191">Wanneer een back-up is gemaakt, de volgende items zijn back-up gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2d014-191">When a backup is created, the following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="2d014-192">Een back-up items</span><span class="sxs-lookup"><span data-stu-id="2d014-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="2d014-193">
 <strong>Azure BizTalk Services-Portal</strong></span><span class="sxs-lookup"><span data-stu-id="2d014-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="2d014-194">Configuratie- en Runtime</span><span class="sxs-lookup"><span data-stu-id="2d014-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="2d014-195">Details van partners en -profiel</span><span class="sxs-lookup"><span data-stu-id="2d014-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="2d014-196">Partner overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="2d014-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="2d014-197">Aangepaste assembly's die zijn geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="2d014-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="2d014-198">Bruggen geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="2d014-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="2d014-199">Certificaten</span><span class="sxs-lookup"><span data-stu-id="2d014-199">Certificates</span></span></li>
<li><span data-ttu-id="2d014-200">Transformaties geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="2d014-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="2d014-201">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="2d014-201">Pipelines</span></span></li>
<li><span data-ttu-id="2d014-202">Sjablonen gemaakt en opgeslagen in de Portal van BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="2d014-202">Templates created and saved in the BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="2d014-203">X12 ST01 en GS01 toewijzingen</span><span class="sxs-lookup"><span data-stu-id="2d014-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="2d014-204">Besturingselement cijfers (EDI)</span><span class="sxs-lookup"><span data-stu-id="2d014-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="2d014-205">AS2-bericht MIC waarden</span><span class="sxs-lookup"><span data-stu-id="2d014-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="2d014-206">
 <strong>Azure BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="2d014-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="2d014-207">SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="2d014-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="2d014-208">Gegevens van SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="2d014-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="2d014-209">Wachtwoord voor SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="2d014-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="2d014-210">BizTalk Service-instellingen</span><span class="sxs-lookup"><span data-stu-id="2d014-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="2d014-211">Aantal Scale-eenheden</span><span class="sxs-lookup"><span data-stu-id="2d014-211">Scale unit count</span></span></li>
<li><span data-ttu-id="2d014-212">Editie</span><span class="sxs-lookup"><span data-stu-id="2d014-212">Edition</span></span></li>
<li><span data-ttu-id="2d014-213">Versie van het product</span><span class="sxs-lookup"><span data-stu-id="2d014-213">Product Version</span></span></li>
<li><span data-ttu-id="2d014-214">Regio/Datacenter</span><span class="sxs-lookup"><span data-stu-id="2d014-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="2d014-215">Access Control Service (ACS) naamruimte en -sleutel</span><span class="sxs-lookup"><span data-stu-id="2d014-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="2d014-216">Tekenreeks voor databaseverbinding bijhouden</span><span class="sxs-lookup"><span data-stu-id="2d014-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="2d014-217">Archiveren van de verbindingsreeks voor opslag-account</span><span class="sxs-lookup"><span data-stu-id="2d014-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="2d014-218">Bewaking van de verbindingsreeks voor opslag-account</span><span class="sxs-lookup"><span data-stu-id="2d014-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="2d014-219">
 <strong>Extra Items</strong></span><span class="sxs-lookup"><span data-stu-id="2d014-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="2d014-220">Traceringsdatabase</span><span class="sxs-lookup"><span data-stu-id="2d014-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="2d014-221">Wanneer de BizTalk Service wordt gemaakt, worden de details van de Database bijhouden ingevoerd, met inbegrip van de Azure SQL Database-Server en de naam van de Database bijhouden.</span><span class="sxs-lookup"><span data-stu-id="2d014-221">When the BizTalk Service is created, the Tracking Database details are entered, including the Azure SQL Database Server and the Tracking Database name.</span></span> <span data-ttu-id="2d014-222">De Database bijhouden wordt niet automatisch back-up.</span><span class="sxs-lookup"><span data-stu-id="2d014-222">The Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="2d014-223">
<strong>Belangrijk</strong></span><span class="sxs-lookup"><span data-stu-id="2d014-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="2d014-224">Als de Database bijhouden wordt verwijderd en de databasebehoeften is hersteld, moet een eerdere back-up bestaan.</span><span class="sxs-lookup"><span data-stu-id="2d014-224">If the Tracking Database is deleted and the database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="2d014-225">Als een back-up niet bestaat, zijn de Database bijhouden en de gegevens niet hersteld.</span><span class="sxs-lookup"><span data-stu-id="2d014-225">If a backup does not exist, the Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="2d014-226">In dit geval maakt u een nieuwe Database voor het bijhouden met dezelfde databasenaam.</span><span class="sxs-lookup"><span data-stu-id="2d014-226">In this situation, create a new Tracking Database with the same database name.</span></span> <span data-ttu-id="2d014-227">Geo-replicatie wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="2d014-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="2d014-228">Volgende</span><span class="sxs-lookup"><span data-stu-id="2d014-228">Next</span></span>
<span data-ttu-id="2d014-229">Voor het maken van Azure BizTalk Services in de klassieke Azure portal, gaat u naar [BizTalk Services: inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="2d014-229">To create Azure BizTalk Services in the Azure classic portal, go to [BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="2d014-230">Ga naar [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197) om te beginnen met het maken van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2d014-230">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="2d014-231">Zie ook</span><span class="sxs-lookup"><span data-stu-id="2d014-231">See Also</span></span>
* [<span data-ttu-id="2d014-232">Back-up van BizTalk-Service</span><span class="sxs-lookup"><span data-stu-id="2d014-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="2d014-233">BizTalk Service back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="2d014-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="2d014-234">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="2d014-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="2d014-235">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="2d014-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="2d014-236">BizTalk Services: statusgrafiek voor de inrichting</span><span class="sxs-lookup"><span data-stu-id="2d014-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="2d014-237">BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen</span><span class="sxs-lookup"><span data-stu-id="2d014-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="2d014-238">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="2d014-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="2d014-239">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="2d014-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="2d014-240">De Azure BizTalk Services SDK gaan gebruiken</span><span class="sxs-lookup"><span data-stu-id="2d014-240">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png


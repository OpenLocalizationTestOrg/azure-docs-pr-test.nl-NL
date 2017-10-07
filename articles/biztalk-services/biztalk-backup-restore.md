---
title: aaaCreate maken en terugzetten een back-up in BizTalk Services | Microsoft Docs
description: BizTalk Services omvat back-up en herstel. Meer informatie over hoe toocreate en herstellen van een back-up en bepalen wat opgehaald back-up gemaakt. MABS, WABS
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
ms.openlocfilehash: 32356ad870678fa5fd5bbbbf13d9377188f770a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-backup-and-restore"></a><span data-ttu-id="521ba-105">BizTalk Services: back-ups maken en herstellen</span><span class="sxs-lookup"><span data-stu-id="521ba-105">BizTalk Services: Backup and Restore</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="521ba-106">Azure BizTalk Services bevat de mogelijkheden van back-up en herstel.</span><span class="sxs-lookup"><span data-stu-id="521ba-106">Azure BizTalk Services includes Backup and Restore capabilities.</span></span> <span data-ttu-id="521ba-107">Dit onderwerp wordt beschreven hoe toobackup en terugzetten van BizTalk Services met behulp van de klassieke Azure-portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="521ba-107">This topic describes how toobackup and restore BizTalk Services using hello Azure classic portal.</span></span>

<span data-ttu-id="521ba-108">U kunt ook back-up BizTalk Services met behulp van Hallo [REST-API van BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span><span class="sxs-lookup"><span data-stu-id="521ba-108">You can also back up BizTalk Services using hello [BizTalk Services REST API](http://go.microsoft.com/fwlink/p/?LinkID=325584).</span></span> 

> [!NOTE]
> <span data-ttu-id="521ba-109">Hybride verbindingen zijn geen back-up, ongeacht Hallo Edition.</span><span class="sxs-lookup"><span data-stu-id="521ba-109">Hybrid Connections are NOT backed up, regardless of hello Edition.</span></span> <span data-ttu-id="521ba-110">U moet uw hybride verbindingen opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="521ba-110">You must recreate your hybrid connections.</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="521ba-111">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="521ba-111">Before you Begin</span></span>
* <span data-ttu-id="521ba-112">Back-up en herstel mogelijk niet beschikbaar voor alle edities.</span><span class="sxs-lookup"><span data-stu-id="521ba-112">Backup and Restore may not be available for all editions.</span></span> <span data-ttu-id="521ba-113">Zie [BizTalk Services: grafiek van edities](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="521ba-113">See [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>
* <span data-ttu-id="521ba-114">Hallo klassieke Azure-portal gebruikt, kunt u een On Demand back-up maken of een geplande back-up maken.</span><span class="sxs-lookup"><span data-stu-id="521ba-114">Using hello Azure classic portal, you can create an On Demand backup or create a scheduled backup.</span></span> 
* <span data-ttu-id="521ba-115">Back-up van inhoud kan worden teruggezet toohello dezelfde BizTalk Service of tooa nieuwe BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="521ba-115">Backup content can be restored toohello same BizTalk Service or tooa new BizTalk Service.</span></span> <span data-ttu-id="521ba-116">toorestore Hallo BizTalk Service met behulp van Hallo Hallo bestaande BizTalk Service met dezelfde naam moet worden verwijderd en Hallo-naam moet beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="521ba-116">toorestore hello BizTalk Service using hello same name, hello existing BizTalk Service must be deleted and hello name must be available.</span></span> <span data-ttu-id="521ba-117">Nadat u een BizTalk Service hebt verwijderd, kunnen duurt langer dan wilden voor Hallo dezelfde naam toobe beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="521ba-117">After you delete a BizTalk Service, it can take longer time than wanted for hello same name toobe available.</span></span> <span data-ttu-id="521ba-118">Als u niet kunt tot Hallo wachten dezelfde naam toobe beschikbaar en zet vervolgens tooa nieuwe BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="521ba-118">If you cannot wait for hello same name toobe available, then restore tooa new BizTalk Service.</span></span>
* <span data-ttu-id="521ba-119">BizTalk Services kunnen worden hersteld toohello dezelfde versie of een hogere editie.</span><span class="sxs-lookup"><span data-stu-id="521ba-119">BizTalk Services can be restored toohello same edition or a higher edition.</span></span> <span data-ttu-id="521ba-120">Herstellen van BizTalk Services tooa wordt lagere edition uit wanneer Hallo back-up is gemaakt, niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="521ba-120">Restoring BizTalk Services tooa lower edition, from when hello backup was taken, is not supported.</span></span>
  
    <span data-ttu-id="521ba-121">Bijvoorbeeld, een back-up met behulp van Hallo die Basic-editie kan worden hersteld toohello Premium Edition.</span><span class="sxs-lookup"><span data-stu-id="521ba-121">For example, a backup using hello Basic Edition can be restored toohello Premium Edition.</span></span> <span data-ttu-id="521ba-122">Een back-up met behulp van Hallo die Premium Edition kan niet worden hersteld toohello Standard Edition.</span><span class="sxs-lookup"><span data-stu-id="521ba-122">A backup using hello Premium Edition cannot be restored toohello Standard Edition.</span></span>
* <span data-ttu-id="521ba-123">Hallo EDI-besturingselement cijfers zijn back-up toomaintain continuïteit van Hallo besturingselement getallen.</span><span class="sxs-lookup"><span data-stu-id="521ba-123">hello EDI Control numbers are backed up toomaintain continuity of hello control numbers.</span></span> <span data-ttu-id="521ba-124">Als berichten worden verwerkt na de laatste back-up hello, herstellen van de inhoud van deze back-up kan leiden tot dubbele besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="521ba-124">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>
* <span data-ttu-id="521ba-125">Als een batch actieve berichten heeft, Hallo batch verwerkt **voordat** waarop een back-up.</span><span class="sxs-lookup"><span data-stu-id="521ba-125">If a batch has active messages, process hello batch **before** running a backup.</span></span> <span data-ttu-id="521ba-126">Wanneer u een back-up (als de benodigde of geplande) maakt, worden berichten in batches nooit worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="521ba-126">When creating a backup (as needed or scheduled), messages in batches are never stored.</span></span> 
  
    <span data-ttu-id="521ba-127">**Als u een back-up wordt gemaakt met actieve berichten in een batch, wordt deze berichten worden niet een back-up en zijn daarom verloren.**</span><span class="sxs-lookup"><span data-stu-id="521ba-127">**If a backup is taken with active messages in a batch, these messages are not backed up and are therefore lost.**</span></span>
* <span data-ttu-id="521ba-128">Optioneel: In Hallo BizTalk Services-Portal, stopt alle beheertaken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="521ba-128">Optional: In hello BizTalk Services Portal, stop any management operations.</span></span>

## <a name="create-a-backup"></a><span data-ttu-id="521ba-129">Maak een back-up</span><span class="sxs-lookup"><span data-stu-id="521ba-129">Create a backup</span></span>
<span data-ttu-id="521ba-130">Een back-up kan worden uitgevoerd op elk gewenst moment en volledig door u worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="521ba-130">A backup can be taken at any time and is completely controlled by you.</span></span> <span data-ttu-id="521ba-131">Deze sectie vindt u Hallo stappen toocreate back-ups Hallo klassieke Azure portal, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="521ba-131">This section lists hello steps toocreate backups using hello Azure classic portal, including:</span></span>

[<span data-ttu-id="521ba-132">Op aanvraag back-up</span><span class="sxs-lookup"><span data-stu-id="521ba-132">On Demand backup</span></span>](#backupnow)

[<span data-ttu-id="521ba-133">Een back-up plannen</span><span class="sxs-lookup"><span data-stu-id="521ba-133">Schedule a backup</span></span>](#backupschedule)

#### <span data-ttu-id="521ba-134"><a name="backupnow"></a>Op aanvraag back-up</span><span class="sxs-lookup"><span data-stu-id="521ba-134"><a name="backupnow"></a>On Demand backup</span></span>
1. <span data-ttu-id="521ba-135">Selecteer in de klassieke Azure-portal hello, **BizTalk Services**, en vervolgens Selecteer BizTalk services die u wenst toobackup Hallo.</span><span class="sxs-lookup"><span data-stu-id="521ba-135">In hello Azure classic portal, select **BizTalk Services**, and then select hello BizTalk Service you want toobackup.</span></span>
2. <span data-ttu-id="521ba-136">In Hallo **Dashboard** tabblad **Back-up** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="521ba-136">In hello **Dashboard** tab, select **Back up** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="521ba-137">Voer de naam van een back-up.</span><span class="sxs-lookup"><span data-stu-id="521ba-137">Enter a backup name.</span></span> <span data-ttu-id="521ba-138">Voer bijvoorbeeld *myBizTalkService*door*datum*.</span><span class="sxs-lookup"><span data-stu-id="521ba-138">For example, enter *myBizTalkService*BU*Date*.</span></span>
4. <span data-ttu-id="521ba-139">Kies een blob storage-account en selecteer Hallo vinkje toostart Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="521ba-139">Choose a blob storage account and select hello checkmark toostart hello backup.</span></span>

<span data-ttu-id="521ba-140">Zodra Hallo back-up is voltooid, wordt een container met Hallo back-naam die u invoert in Hallo storage-account gemaakt.</span><span class="sxs-lookup"><span data-stu-id="521ba-140">Once hello backup completes, a container with hello backup name you enter is created in hello storage account.</span></span> <span data-ttu-id="521ba-141">Deze container bevat uw BizTalk Service back-upconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="521ba-141">This container contains your BizTalk Service backup configuration.</span></span>

#### <span data-ttu-id="521ba-142"><a name="backupschedule"></a>Een back-up plannen</span><span class="sxs-lookup"><span data-stu-id="521ba-142"><a name="backupschedule"></a>Schedule a backup</span></span>
1. <span data-ttu-id="521ba-143">Selecteer in de klassieke Azure-portal hello, **BizTalk Services**, selecteer BizTalk Service-naam tooschedule Hallo back-up en selecteer vervolgens Hallo Hallo **configureren** tabblad.</span><span class="sxs-lookup"><span data-stu-id="521ba-143">In hello Azure classic portal, select **BizTalk Services**, select hello BizTalk Service name you want tooschedule hello backup, and then select hello **Configure** tab.</span></span>
2. <span data-ttu-id="521ba-144">Set Hallo **back-up Status** te**automatische**.</span><span class="sxs-lookup"><span data-stu-id="521ba-144">Set hello **Backup Status** too**Automatic**.</span></span> 
3. <span data-ttu-id="521ba-145">Selecteer Hallo **Opslagaccount** toostore Hallo back-up, Voer Hallo **frequentie** toocreate Hallo back-ups en back-ups van hoe lang tookeep hello (**dagen bewaren**):</span><span class="sxs-lookup"><span data-stu-id="521ba-145">Select hello **Storage Account** toostore hello backup, enter hello **Frequency** toocreate hello backups, and how long tookeep hello backups (**Retention Days**):</span></span>
   
    ![][AutomaticBU]
   
    <span data-ttu-id="521ba-146">**Opmerkingen bij de**</span><span class="sxs-lookup"><span data-stu-id="521ba-146">**Notes**</span></span>     
   
   * <span data-ttu-id="521ba-147">In **dagen bewaren**, Hallo bewaarperiode moet groter dan de back-upfrequentie Hallo.</span><span class="sxs-lookup"><span data-stu-id="521ba-147">In **Retention Days**, hello retention period must be greater than hello backup frequency.</span></span>
   * <span data-ttu-id="521ba-148">Selecteer **altijd ten minste één back-up bewaren**, zelfs als deze uit het verleden Hallo bewaarperiode.</span><span class="sxs-lookup"><span data-stu-id="521ba-148">Select **Always keep at least one backup**, even if it is past hello retention period.</span></span>
4. <span data-ttu-id="521ba-149">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="521ba-149">Select **Save**.</span></span>

<span data-ttu-id="521ba-150">Wanneer een geplande back-uptaak wordt uitgevoerd, wordt een container (back-upgegevens toostore) in Hallo storage-account hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="521ba-150">When a scheduled backup job runs, it creates a container (toostore backup data) in hello storage account you entered.</span></span> <span data-ttu-id="521ba-151">Hallo-naam van de container Hallo heet *naam-/-tijd van de BizTalk Service*.</span><span class="sxs-lookup"><span data-stu-id="521ba-151">hello name of hello container is named *BizTalk Service Name-date-time*.</span></span> 

<span data-ttu-id="521ba-152">Als Hallo BizTalk Service dashboard toont een **mislukt** status:</span><span class="sxs-lookup"><span data-stu-id="521ba-152">If hello BizTalk Service dashboard shows a **Failed** status:</span></span>

![Status van laatste geplande back-up][BackupStatus] 

<span data-ttu-id="521ba-154">Hallo koppeling opent Hallo Management Services-Bewerkingslogboeken toohelp oplossen.</span><span class="sxs-lookup"><span data-stu-id="521ba-154">hello link opens hello Management Services Operation Logs toohelp troubleshoot.</span></span> <span data-ttu-id="521ba-155">Zie [BizTalk Services: problemen oplossen met bewerkingslogboeken](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span><span class="sxs-lookup"><span data-stu-id="521ba-155">See [BizTalk Services: Troubleshoot using operation logs](http://go.microsoft.com/fwlink/p/?LinkId=391211).</span></span>

## <a name="restore"></a><span data-ttu-id="521ba-156">Herstellen</span><span class="sxs-lookup"><span data-stu-id="521ba-156">Restore</span></span>
<span data-ttu-id="521ba-157">U kunt back-ups herstellen van Hallo klassieke Azure-portal of van Hallo [herstellen BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span><span class="sxs-lookup"><span data-stu-id="521ba-157">You can restore backups from hello Azure classic portal or from hello [Restore BizTalk Service REST API](http://go.microsoft.com/fwlink/p/?LinkID=325582).</span></span> <span data-ttu-id="521ba-158">Deze sectie vindt Hallo stappen toorestore met Hallo klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="521ba-158">This section lists hello steps toorestore using hello classic portal.</span></span>

#### <a name="before-restoring-a-backup"></a><span data-ttu-id="521ba-159">Voordat u een back-up herstellen</span><span class="sxs-lookup"><span data-stu-id="521ba-159">Before restoring a backup</span></span>
* <span data-ttu-id="521ba-160">Nieuwe bijhouden, archiveren en te bewaken winkels kunnen worden ingevoerd tijdens het herstellen van een BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="521ba-160">New tracking, archiving, and monitoring stores can be entered while restoring a BizTalk Service.</span></span>
* <span data-ttu-id="521ba-161">Hallo dezelfde EDI-Runtime-gegevens is hersteld.</span><span class="sxs-lookup"><span data-stu-id="521ba-161">hello same EDI Runtime data is restored.</span></span> <span data-ttu-id="521ba-162">Hallo EDI-Runtime back-up slaat Hallo besturingselement getallen.</span><span class="sxs-lookup"><span data-stu-id="521ba-162">hello EDI Runtime backup stores hello control numbers.</span></span> <span data-ttu-id="521ba-163">Hallo hersteld besturingselement getallen worden in volgorde van de tijd Hallo Hallo back-up.</span><span class="sxs-lookup"><span data-stu-id="521ba-163">hello restored control numbers are in sequence from hello time of hello backup.</span></span> <span data-ttu-id="521ba-164">Als berichten worden verwerkt na de laatste back-up hello, herstellen van de inhoud van deze back-up kan leiden tot dubbele besturingselement cijfers.</span><span class="sxs-lookup"><span data-stu-id="521ba-164">If messages are processed after hello last backup, restoring this backup content can cause duplicate control numbers.</span></span>

#### <a name="restore-a-backup"></a><span data-ttu-id="521ba-165">Een back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="521ba-165">Restore a backup</span></span>
1. <span data-ttu-id="521ba-166">Selecteer in de klassieke Azure-portal hello, **nieuw** > **App Services** > **BizTalk Service** > **herstellen** :</span><span class="sxs-lookup"><span data-stu-id="521ba-166">In hello Azure classic portal, select **New** > **App Services** > **BizTalk Service** > **Restore**:</span></span>
   
    ![Een back-up terugzetten][Restore]
2. <span data-ttu-id="521ba-168">In **back-URL**, selecteert u het pictogram map Hallo en vouw hello Azure storage-account dat winkels Hallo BizTalk Service configuratieback-up.</span><span class="sxs-lookup"><span data-stu-id="521ba-168">In **Backup URL**, select hello folder icon and expand hello Azure storage account that stores hello BizTalk Service configuration backup.</span></span> <span data-ttu-id="521ba-169">Hallo Breid en selecteer in het rechterdeelvenster Hallo Hallo overeenkomende back-up txt-bestand.</span><span class="sxs-lookup"><span data-stu-id="521ba-169">Expand hello container and in hello right pane, select hello corresponding back up .txt file.</span></span> 
   <br/><br/>
   <span data-ttu-id="521ba-170">Selecteer **Open**.</span><span class="sxs-lookup"><span data-stu-id="521ba-170">Select **Open**.</span></span>
3. <span data-ttu-id="521ba-171">Op Hallo **herstellen BizTalk Service** pagina, voert u een **BizTalk-servicenaam** en controleer of Hallo **domein-URL**, **Edition**, en **Regio** voor Hallo BizTalk-Service is hersteld.</span><span class="sxs-lookup"><span data-stu-id="521ba-171">On hello **Restore BizTalk Service** page, enter a **BizTalk Service Name** and verify hello **Domain URL**, **Edition**, and **Region** for hello restored BizTalk Service.</span></span> <span data-ttu-id="521ba-172">**Maak een nieuw exemplaar van SQL database** voor Hallo bijhouden van database:</span><span class="sxs-lookup"><span data-stu-id="521ba-172">**Create a new SQL database instance** for hello tracking database:</span></span>
   
    ![][RestoreBizTalkService]
   
    <span data-ttu-id="521ba-173">Selecteer Hallo pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="521ba-173">Select hello next arrow.</span></span>
4. <span data-ttu-id="521ba-174">Controleer de naam van de Hallo van Hallo SQL-database, Hallo fysieke server waar Hallo SQL-database wordt gemaakt en een gebruikersnaam en wachtwoord invoeren voor die server.</span><span class="sxs-lookup"><span data-stu-id="521ba-174">Verify hello name of hello SQL database, enter hello physical server where hello SQL database will be created, and a username/password for that server.</span></span>

    <span data-ttu-id="521ba-175">Als u wilt dat tooconfigure Hallo SQL database-editie, grootte en andere eigenschappen, selecteert u **geavanceerde Database-instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="521ba-175">If you want tooconfigure hello SQL database edition, size, and other properties, select  **Configure Advanced Database Settings**.</span></span> 

    <span data-ttu-id="521ba-176">Selecteer Hallo pijl Volgende.</span><span class="sxs-lookup"><span data-stu-id="521ba-176">Select hello next arrow.</span></span>

1. <span data-ttu-id="521ba-177">Een nieuw opslagaccount maken of voert u een bestaand opslagaccount voor Hallo BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="521ba-177">Create a new storage account or enter an existing storage account for hello BizTalk Service.</span></span>
2. <span data-ttu-id="521ba-178">Selecteer Hallo vinkje toostart Hallo terugzetten.</span><span class="sxs-lookup"><span data-stu-id="521ba-178">Select hello checkmark toostart hello restore.</span></span>

<span data-ttu-id="521ba-179">Zodra het Hallo-herstelbewerking is voltooid, wordt een nieuwe BizTalk Service wordt vermeld in een onderbroken status op Hallo BizTalk Services pagina in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="521ba-179">Once hello restoration successfully completes, a new BizTalk Service is listed in a suspended state on hello BizTalk Services page in hello Azure classic portal.</span></span>

### <span data-ttu-id="521ba-180"><a name="postrestore"></a>Na het terugzetten van een back-up</span><span class="sxs-lookup"><span data-stu-id="521ba-180"><a name="postrestore"></a>After restoring a backup</span></span>
<span data-ttu-id="521ba-181">Hallo BizTalk Service wordt altijd hersteld een **onderbroken** status.</span><span class="sxs-lookup"><span data-stu-id="521ba-181">hello BizTalk Service is always restored in a **Suspended** state.</span></span> <span data-ttu-id="521ba-182">In deze toestand is, kunt u geen configuratiewijzigingen voordat nieuwe Hallo-omgeving functioneel is, met inbegrip van:</span><span class="sxs-lookup"><span data-stu-id="521ba-182">In this state, you can make any configuration changes before hello new environment is functional, including:</span></span>

* <span data-ttu-id="521ba-183">Als u een BizTalk Service-toepassingen met behulp van Azure BizTalk Services SDK Hallo gemaakt, moet u mogelijk tootooupdate Hallo Access Control (ACS)-referenties in die toowork toepassingen met Hallo hersteld-omgeving.</span><span class="sxs-lookup"><span data-stu-id="521ba-183">If you created BizTalk Service applications using hello Azure BizTalk Services SDK, you may need tootooupdate hello Access Control (ACS) credentials in those applications toowork with hello restored environment.</span></span>
* <span data-ttu-id="521ba-184">U herstelt een BizTalk Service tooreplicate een bestaande BizTalk Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="521ba-184">You restore a BizTalk Service tooreplicate an existing BizTalk Service environment.</span></span> <span data-ttu-id="521ba-185">In dit geval, als er zijn geconfigureerd in de oorspronkelijke BizTalk Services-portal Hallo overeenkomsten die gebruikmaken van een FTP-bronmap, moet u mogelijk tooupdate Hallo overeenkomsten in de zojuist hersteld Hallo omgeving toouse een andere bron FTP-map.</span><span class="sxs-lookup"><span data-stu-id="521ba-185">In this situation, if there are agreements configured in hello original BizTalk Services portal that use a source FTP folder, you may need tooupdate hello agreements in hello newly restored environment toouse a different source FTP folder.</span></span> <span data-ttu-id="521ba-186">Anders kunnen er twee verschillende overeenkomsten toopull probeert Hallo hetzelfde bericht.</span><span class="sxs-lookup"><span data-stu-id="521ba-186">Otherwise, there may be two different agreements trying toopull hello same message.</span></span>
* <span data-ttu-id="521ba-187">Als u toohave omgevingen met meerdere BizTalk Service teruggezet, zorg er dan voor dat u richt de juiste omgeving Hallo in Visual Studio-toepassingen hello, PowerShell-cmdlets, REST-API's of Trading Partner Management OM API's.</span><span class="sxs-lookup"><span data-stu-id="521ba-187">If you restored toohave multiple BizTalk Service environments, make sure you target hello correct environment in hello Visual Studio applications, PowerShell cmdlets, REST APIs, or Trading Partner Management OM APIs.</span></span>
* <span data-ttu-id="521ba-188">Het is een back-ups tooconfigure geautomatiseerde raadzaam op Hallo zojuist hersteld BizTalk Service-omgeving.</span><span class="sxs-lookup"><span data-stu-id="521ba-188">It's a good practice tooconfigure automated backups on hello newly restored BizTalk Service environment.</span></span>

<span data-ttu-id="521ba-189">toostart hello BizTalk Service in Hallo klassieke Azure-portal, selecteer Hallo hersteld BizTalk Service en selecteer **hervatten** in de taakbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="521ba-189">toostart hello BizTalk Service in hello Azure classic portal, select hello restored BizTalk Service and select **Resume** in hello task bar.</span></span> 

## <a name="what-gets-backed-up"></a><span data-ttu-id="521ba-190">Wat wordt een back-up</span><span class="sxs-lookup"><span data-stu-id="521ba-190">What gets backed up</span></span>
<span data-ttu-id="521ba-191">Wanneer een back-up is gemaakt, hello volgende items zijn back-up gemaakt:</span><span class="sxs-lookup"><span data-stu-id="521ba-191">When a backup is created, hello following items are backed up:</span></span>

<table border="1"> 
<tr bgcolor="FAF9F9">
<th> </th>
<TH><span data-ttu-id="521ba-192">Een back-up items</span><span class="sxs-lookup"><span data-stu-id="521ba-192">Items backed up</span></span></TH> 
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="521ba-193">
 <strong>Azure BizTalk Services-Portal</strong></span><span class="sxs-lookup"><span data-stu-id="521ba-193">
 <strong>Azure BizTalk Services Portal</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="521ba-194">Configuratie- en Runtime</span><span class="sxs-lookup"><span data-stu-id="521ba-194">Configuration and Runtime</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="521ba-195">Details van partners en -profiel</span><span class="sxs-lookup"><span data-stu-id="521ba-195">Partner and profile details</span></span></li>
<li><span data-ttu-id="521ba-196">Partner overeenkomsten</span><span class="sxs-lookup"><span data-stu-id="521ba-196">Partner Agreements</span></span></li>
<li><span data-ttu-id="521ba-197">Aangepaste assembly's die zijn geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="521ba-197">Custom assemblies deployed</span></span></li>
<li><span data-ttu-id="521ba-198">Bruggen geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="521ba-198">Bridges deployed</span></span></li>
<li><span data-ttu-id="521ba-199">Certificaten</span><span class="sxs-lookup"><span data-stu-id="521ba-199">Certificates</span></span></li>
<li><span data-ttu-id="521ba-200">Transformaties geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="521ba-200">Transforms deployed</span></span></li>
<li><span data-ttu-id="521ba-201">Pijplijnen</span><span class="sxs-lookup"><span data-stu-id="521ba-201">Pipelines</span></span></li>
<li><span data-ttu-id="521ba-202">Sjablonen gemaakt en opgeslagen in Hallo BizTalk Services-Portal</span><span class="sxs-lookup"><span data-stu-id="521ba-202">Templates created and saved in hello BizTalk Services Portal</span></span></li>
<li><span data-ttu-id="521ba-203">X12 ST01 en GS01 toewijzingen</span><span class="sxs-lookup"><span data-stu-id="521ba-203">X12 ST01 and GS01 mappings</span></span></li>
<li><span data-ttu-id="521ba-204">Besturingselement cijfers (EDI)</span><span class="sxs-lookup"><span data-stu-id="521ba-204">Control numbers (EDI)</span></span></li>
<li><span data-ttu-id="521ba-205">AS2-bericht MIC waarden</span><span class="sxs-lookup"><span data-stu-id="521ba-205">AS2 Message MIC values</span></span></li>
</ul>
</td>
</tr> 

<tr>
<td colspan="2"><span data-ttu-id="521ba-206">
 <strong>Azure BizTalk Service</strong></span><span class="sxs-lookup"><span data-stu-id="521ba-206">
 <strong>Azure BizTalk Service</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="521ba-207">SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="521ba-207">SSL Certificate</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="521ba-208">Gegevens van SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="521ba-208">SSL Certificate Data</span></span></li>
<li><span data-ttu-id="521ba-209">Wachtwoord voor SSL-certificaat</span><span class="sxs-lookup"><span data-stu-id="521ba-209">SSL Certificate Password</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td><span data-ttu-id="521ba-210">BizTalk Service-instellingen</span><span class="sxs-lookup"><span data-stu-id="521ba-210">BizTalk Service Settings</span></span></td> 
<td>
<ul>
<li><span data-ttu-id="521ba-211">Aantal Scale-eenheden</span><span class="sxs-lookup"><span data-stu-id="521ba-211">Scale unit count</span></span></li>
<li><span data-ttu-id="521ba-212">Editie</span><span class="sxs-lookup"><span data-stu-id="521ba-212">Edition</span></span></li>
<li><span data-ttu-id="521ba-213">Versie van het product</span><span class="sxs-lookup"><span data-stu-id="521ba-213">Product Version</span></span></li>
<li><span data-ttu-id="521ba-214">Regio/Datacenter</span><span class="sxs-lookup"><span data-stu-id="521ba-214">Region/Datacenter</span></span></li>
<li><span data-ttu-id="521ba-215">Access Control Service (ACS) naamruimte en -sleutel</span><span class="sxs-lookup"><span data-stu-id="521ba-215">Access Control Service (ACS) namespace and key</span></span></li>
<li><span data-ttu-id="521ba-216">Tekenreeks voor databaseverbinding bijhouden</span><span class="sxs-lookup"><span data-stu-id="521ba-216">Tracking database connection string</span></span></li>
<li><span data-ttu-id="521ba-217">Archiveren van de verbindingsreeks voor opslag-account</span><span class="sxs-lookup"><span data-stu-id="521ba-217">Archiving Storage account connection string</span></span></li>
<li><span data-ttu-id="521ba-218">Bewaking van de verbindingsreeks voor opslag-account</span><span class="sxs-lookup"><span data-stu-id="521ba-218">Monitoring storage account connection string</span></span></li>
</ul>
</td>
</tr> 
<tr>
<td colspan="2"><span data-ttu-id="521ba-219">
 <strong>Extra Items</strong></span><span class="sxs-lookup"><span data-stu-id="521ba-219">
 <strong>Additional Items</strong></span></span></td>
</tr> 
<tr>
<td><span data-ttu-id="521ba-220">Traceringsdatabase</span><span class="sxs-lookup"><span data-stu-id="521ba-220">Tracking Database</span></span></td> 
<td><span data-ttu-id="521ba-221">Wanneer u Hallo BizTalk Service maakt, worden Hallo bijhouden databasedetails ingevoerd, inclusief hello Azure SQL Database-Server en de databasenaam van Hallo bijhouden.</span><span class="sxs-lookup"><span data-stu-id="521ba-221">When hello BizTalk Service is created, hello Tracking Database details are entered, including hello Azure SQL Database Server and hello Tracking Database name.</span></span> <span data-ttu-id="521ba-222">Hallo bijhouden Database is geen automatisch back-gemaakt.</span><span class="sxs-lookup"><span data-stu-id="521ba-222">hello Tracking Database is not automatically backed up.</span></span>
<br/><br/><span data-ttu-id="521ba-223">
<strong>Belangrijk</strong></span><span class="sxs-lookup"><span data-stu-id="521ba-223">
<strong>Important</strong></span></span><br/>
<span data-ttu-id="521ba-224">Als Hallo bijhouden Database wordt verwijderd en Hallo van de databasebehoeften is hersteld, moet een eerdere back-up bestaan.</span><span class="sxs-lookup"><span data-stu-id="521ba-224">If hello Tracking Database is deleted and hello database needs recovered, a previous backup must exist.</span></span> <span data-ttu-id="521ba-225">Als een back-up niet bestaat, zijn Hallo Database bijhouden en de gegevens niet hersteld.</span><span class="sxs-lookup"><span data-stu-id="521ba-225">If a backup does not exist, hello Tracking Database and its data are not recoverable.</span></span> <span data-ttu-id="521ba-226">In dit geval maakt u een nieuwe Database voor het bijhouden van Hello dezelfde databasenaam.</span><span class="sxs-lookup"><span data-stu-id="521ba-226">In this situation, create a new Tracking Database with hello same database name.</span></span> <span data-ttu-id="521ba-227">Geo-replicatie wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="521ba-227">Geo-Replication is recommended.</span></span></td>
</tr> 
</table>

## <a name="next"></a><span data-ttu-id="521ba-228">Volgende</span><span class="sxs-lookup"><span data-stu-id="521ba-228">Next</span></span>
<span data-ttu-id="521ba-229">toocreate Azure BizTalk Services in Azure classic portal, ga te Hallo[BizTalk Services: inrichten met behulp van Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span><span class="sxs-lookup"><span data-stu-id="521ba-229">toocreate Azure BizTalk Services in hello Azure classic portal, go too[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280).</span></span> <span data-ttu-id="521ba-230">toostart te maken van toepassingen, ga[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="521ba-230">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="521ba-231">Zie ook</span><span class="sxs-lookup"><span data-stu-id="521ba-231">See Also</span></span>
* [<span data-ttu-id="521ba-232">Back-up van BizTalk-Service</span><span class="sxs-lookup"><span data-stu-id="521ba-232">Backup BizTalk Service</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325584)
* [<span data-ttu-id="521ba-233">BizTalk Service back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="521ba-233">Restore BizTalk Service from Backup</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=325582)
* [<span data-ttu-id="521ba-234">BizTalk Services: Developer, Basic, Standard en Premium-edities grafiek</span><span class="sxs-lookup"><span data-stu-id="521ba-234">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302279)
* [<span data-ttu-id="521ba-235">BizTalk Services: Inrichten met behulp van Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="521ba-235">BizTalk Services: Provisioning Using Azure classic portal</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302280)
* [<span data-ttu-id="521ba-236">BizTalk Services: statusgrafiek voor de inrichting</span><span class="sxs-lookup"><span data-stu-id="521ba-236">BizTalk Services: Provisioning Status Chart</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=329870)
* [<span data-ttu-id="521ba-237">BizTalk Services: de tabbladen Dashboard, Bewaken en Schalen</span><span class="sxs-lookup"><span data-stu-id="521ba-237">BizTalk Services: Dashboard, Monitor and Scale tabs</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302281)
* [<span data-ttu-id="521ba-238">BizTalk Services: beperking</span><span class="sxs-lookup"><span data-stu-id="521ba-238">BizTalk Services: Throttling</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302282)
* [<span data-ttu-id="521ba-239">BizTalk Services: naam en sleutel van verlener</span><span class="sxs-lookup"><span data-stu-id="521ba-239">BizTalk Services: Issuer Name and Issuer Key</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=303941)
* [<span data-ttu-id="521ba-240">Hoe gaan gebruiken Azure BizTalk Services SDK Hallo</span><span class="sxs-lookup"><span data-stu-id="521ba-240">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[BackupStatus]: ./media/biztalk-backup-restore/status-last-backup.png
[Restore]: ./media/biztalk-backup-restore/restore-ui.png
[AutomaticBU]: ./media/biztalk-backup-restore/AutomaticBU.png
[RestoreBizTalkService]: ./media/biztalk-backup-restore/RestoreBizTalkServiceWindow.png


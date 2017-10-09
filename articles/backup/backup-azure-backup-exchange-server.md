---
title: aaaBack van een Exchange server tooAzure back-up met System Center 2012 R2 DPM | Microsoft Docs
description: Meer informatie over hoe tooback van een Exchange server-tooAzure back met System Center 2012 R2 DPM
services: backup
documentationcenter: 
author: MaanasSaran
manager: NKolli1
editor: 
ms.assetid: 13f32256-888e-416e-a78b-40c2a26a5939
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: masaran;jimpark;delhan;trinadhk;markgal
ms.openlocfilehash: fa99296d095c180333474b6d419ebc5ec727547a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="4f22a-103">Back-up van een Exchange server tooAzure back-up met System Center 2012 R2 DPM</span><span class="sxs-lookup"><span data-stu-id="4f22a-103">Back up an Exchange server tooAzure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="4f22a-104">Dit artikel wordt beschreven hoe tooconfigure een System Center 2012 R2 Data Protection Manager (DPM) server tooback van een Microsoft Exchange-server te Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="4f22a-104">This article describes how tooconfigure a System Center 2012 R2 Data Protection Manager (DPM) server tooback up a Microsoft Exchange server too Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="4f22a-105">Updates</span><span class="sxs-lookup"><span data-stu-id="4f22a-105">Updates</span></span>
<span data-ttu-id="4f22a-106">toosuccessfully registreren Hallo DPM-server met Azure Backup, moet u Hallo nieuwste updatepakket voor System Center 2012 R2 DPM en Hallo meest recente versie van hello Azure Backup Agent installeren.</span><span class="sxs-lookup"><span data-stu-id="4f22a-106">toosuccessfully register hello DPM server with Azure Backup, you must install hello latest update rollup for System Center 2012 R2 DPM and hello latest version of hello Azure Backup Agent.</span></span> <span data-ttu-id="4f22a-107">De meest recente updatepakket Hallo ophalen uit Hallo [Microsoft catalogus](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="4f22a-107">Get hello latest update rollup from hello [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="4f22a-108">Voor Hallo voorbeelden in dit artikel, versie 2.0.8719.0 van hello Azure Backup Agent is geïnstalleerd en Update Rollup 6 op System Center 2012 R2 DPM is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4f22a-108">For hello examples in this article, version 2.0.8719.0 of hello Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="4f22a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4f22a-109">Prerequisites</span></span>
<span data-ttu-id="4f22a-110">Voordat u doorgaat, controleert u of alle Hallo [vereisten](backup-azure-dpm-introduction.md#prerequisites) voor het gebruik van Microsoft Azure Backup tooprotect werkbelastingen is voldaan.</span><span class="sxs-lookup"><span data-stu-id="4f22a-110">Before you continue, make sure that all hello [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup tooprotect workloads have been met.</span></span> <span data-ttu-id="4f22a-111">Deze vereisten zijn Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4f22a-111">These prerequisites include hello following:</span></span>

* <span data-ttu-id="4f22a-112">Een back-upkluis op Hallo Azure site is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4f22a-112">A backup vault on hello Azure site has been created.</span></span>
* <span data-ttu-id="4f22a-113">Agent en de kluisreferenties hebben gedownloade toohello DPM-server is.</span><span class="sxs-lookup"><span data-stu-id="4f22a-113">Agent and vault credentials have been downloaded toohello DPM server.</span></span>
* <span data-ttu-id="4f22a-114">Hallo-agent is geïnstalleerd op Hallo DPM-server.</span><span class="sxs-lookup"><span data-stu-id="4f22a-114">hello agent is installed on hello DPM server.</span></span>
* <span data-ttu-id="4f22a-115">Hallo kluisreferenties zijn gebruikte tooregister Hallo DPM-server.</span><span class="sxs-lookup"><span data-stu-id="4f22a-115">hello vault credentials were used tooregister hello DPM server.</span></span>
* <span data-ttu-id="4f22a-116">Als u Exchange 2016 beveiligt, voer een upgrade uit tooDPM 2012 R2 UR9 of hoger</span><span class="sxs-lookup"><span data-stu-id="4f22a-116">If you are protecting Exchange 2016, please upgrade tooDPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="4f22a-117">DPM-beveiligingsagent</span><span class="sxs-lookup"><span data-stu-id="4f22a-117">DPM protection agent</span></span>
<span data-ttu-id="4f22a-118">tooinstall hello DPM-beveiligingsagent op Hallo Exchange-server als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="4f22a-118">tooinstall hello DPM protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="4f22a-119">Zorg ervoor dat firewalls Hallo correct zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4f22a-119">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="4f22a-120">Zie [firewall-uitzonderingen voor Hallo agent configureren](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f22a-120">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="4f22a-121">Hallo-agent op Hallo Exchange-server installeren door te klikken op **Management > Agents > installeren** in DPM Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="4f22a-121">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="4f22a-122">Zie [installeren Hallo DPM-beveiligingsagent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="4f22a-122">See [Install hello DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="4f22a-123">Maak een beveiligingsgroep voor Hallo Exchange-server</span><span class="sxs-lookup"><span data-stu-id="4f22a-123">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="4f22a-124">In Hallo DPM Administrator-Console, klikt u op **beveiliging**, en klik vervolgens op **nieuw** op Hallo hulpprogramma lint tooopen hello **nieuwe beveiligingsgroep maken** wizard.</span><span class="sxs-lookup"><span data-stu-id="4f22a-124">In hello DPM Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="4f22a-125">Op Hallo **Welkom** scherm van de wizard klikt u op Hallo **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-125">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="4f22a-126">Op Hallo **type beveiligingsgroep selecteren** scherm, selecteert u **Servers** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-126">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="4f22a-127">Selecteer Hallo Exchange server-database dat u wilt dat tooprotect en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-127">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4f22a-128">Als u Exchange 2013 beveiligt, controleert u Hallo [Exchange 2013-vereisten](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="4f22a-128">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="4f22a-129">In Hallo voorbeeld te volgen, is Hallo Exchange 2010-database geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="4f22a-129">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="4f22a-131">Hallo methode voor gegevensbeveiliging selecteren.</span><span class="sxs-lookup"><span data-stu-id="4f22a-131">Select hello data protection method.</span></span>

    <span data-ttu-id="4f22a-132">Naam van de beveiligingsgroep Hallo en selecteer vervolgens beide Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="4f22a-132">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="4f22a-133">Ik wil kortetermijnbeveiliging met schijf.</span><span class="sxs-lookup"><span data-stu-id="4f22a-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="4f22a-134">Ik wil online beveiliging.</span><span class="sxs-lookup"><span data-stu-id="4f22a-134">I want online protection.</span></span>
6. <span data-ttu-id="4f22a-135">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-135">Click **Next**.</span></span>
7. <span data-ttu-id="4f22a-136">Selecteer Hallo **Eseutil uitvoeren toocheck gegevensintegriteit** optie als u toocheck Hallo integriteit van Hallo Exchange Server-databases.</span><span class="sxs-lookup"><span data-stu-id="4f22a-136">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="4f22a-137">Nadat u deze optie selecteert, back-consistentiecontrole wordt uitgevoerd op Hallo DPM server tooavoid Hallo i/o-verkeer die wordt gegenereerd door het uitvoeren van Hallo **eseutil** opdracht op Hallo Exchange-server.</span><span class="sxs-lookup"><span data-stu-id="4f22a-137">After you select this option, backup consistency checking will be run on hello DPM server tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4f22a-138">toouse deze optie, moet u Hallo Ese.dll en Eseutil.exe bestanden toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory op Hallo DPM-server kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4f22a-138">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on hello DPM server.</span></span> <span data-ttu-id="4f22a-139">Anders de volgende fout hello wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="4f22a-139">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="4f22a-140">![Eseutil-fout](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="4f22a-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="4f22a-141">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-141">Click **Next**.</span></span>
9. <span data-ttu-id="4f22a-142">Selecteer Hallo-database voor **kopieback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-142">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4f22a-143">Als u 'Volledige back-up' voor ten minste één DAG kopie van een database niet selecteert, wordt de logboeken worden niet afgekapt.</span><span class="sxs-lookup"><span data-stu-id="4f22a-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="4f22a-144">Configureer Hallo doelstellingen voor **kortetermijnback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-144">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="4f22a-145">Bekijk de beschikbare schijfruimte Hallo en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-145">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="4f22a-146">Selecteer de tijd Hallo op welke Hallo DPM server Hallo initiële replicatie maken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-146">Select hello time at which hello DPM server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="4f22a-147">Opties voor consistentiecontrole Hallo selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-147">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="4f22a-148">Kies Hallo-database wilt tooback up tooAzure en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-148">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="4f22a-149">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4f22a-149">For example:</span></span>

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="4f22a-151">Definieer de planning Hallo voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-151">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="4f22a-152">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4f22a-152">For example:</span></span>

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="4f22a-154">Houd er rekening mee Online herstelpunten zijn gebaseerd op snelle volledige herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="4f22a-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="4f22a-155">Daarom moet u plannen Hallo online herstelpunt worden gemaakt na het Hallo-tijd die opgegeven voor Hallo express volledige herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="4f22a-155">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="4f22a-156">Configureer Hallo bewaarbeleid voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-156">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="4f22a-157">Kies een replicatieoptie online en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="4f22a-158">Als er een grote database, kan het lang duren voor Hallo eerste back-toobe via Hallo netwerk gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4f22a-158">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="4f22a-159">tooavoid dit probleem, kunt u een offline back-up maken.</span><span class="sxs-lookup"><span data-stu-id="4f22a-159">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="4f22a-161">Hallo-instellingen bevestigen en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-161">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="4f22a-162">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-162">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="4f22a-163">Hallo Exchange-database herstellen</span><span class="sxs-lookup"><span data-stu-id="4f22a-163">Recover hello Exchange database</span></span>
1. <span data-ttu-id="4f22a-164">toorecover een Exchange-database, klikt u op **herstel** in Hallo DPM Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="4f22a-164">toorecover an Exchange database, click **Recovery** in hello DPM Administrator Console.</span></span>
2. <span data-ttu-id="4f22a-165">Hallo Exchange-database die u wilt dat toorecover vinden.</span><span class="sxs-lookup"><span data-stu-id="4f22a-165">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="4f22a-166">Selecteer een online herstelpunt gemaakt in Hallo *hersteltijd* vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="4f22a-166">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="4f22a-167">Klik op **herstellen** toostart hello **Herstelwizard**.</span><span class="sxs-lookup"><span data-stu-id="4f22a-167">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="4f22a-168">Er zijn vijf herstel-typen voor online herstelpunten:</span><span class="sxs-lookup"><span data-stu-id="4f22a-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="4f22a-169">**Herstellen van Exchange Server-locatie toooriginal:** Hallo gegevens worden hersteld toohello oorspronkelijke Exchange server.</span><span class="sxs-lookup"><span data-stu-id="4f22a-169">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="4f22a-170">**Herstel de database op een Exchange Server tooanother:** Hallo gegevens worden tooanother herstelde database op een andere Exchange-server.</span><span class="sxs-lookup"><span data-stu-id="4f22a-170">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="4f22a-171">**Tooa hersteldatabase herstellen:** Hallo gegevens worden hersteld tooan Exchange Recovery Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="4f22a-171">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="4f22a-172">**Kopiëren tooa netwerkmap:** Hallo gegevens worden hersteld tooa netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="4f22a-172">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="4f22a-173">**Kopieer tootape:** als u een tapewisselaar hebt of een zelfstandig tapestation aangesloten en geconfigureerd op Hallo DPM-server Hallo herstelpunt is tooa vrije tape gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4f22a-173">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on hello DPM server, hello recovery point will be copied tooa free tape.</span></span>

    ![Kies onlinereplicatie](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="4f22a-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4f22a-175">Next steps</span></span>
* [<span data-ttu-id="4f22a-176">Veelgestelde vragen over Azure Backup</span><span class="sxs-lookup"><span data-stu-id="4f22a-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

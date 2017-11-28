---
title: aaaBack van een Exchange server tooAzure back-up met Azure Backup-Server | Microsoft Docs
description: Meer informatie over hoe tooback van een Exchange server-tooAzure back met behulp van Azure Backup-Server
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
ms.assetid: e46557e8-2eaf-4ee0-99ea-00fbb8687dca
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: db874161151fc57c5b79c41531e18d577f567f66
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-an-exchange-server-tooazure-backup-with-azure-backup-server"></a><span data-ttu-id="9772f-103">Back-up van een Exchange server tooAzure back-up met Azure Backup-Server</span><span class="sxs-lookup"><span data-stu-id="9772f-103">Back up an Exchange server tooAzure Backup with Azure Backup Server</span></span>
<span data-ttu-id="9772f-104">Dit artikel wordt beschreven hoe tooconfigure Microsoft Azure Backup-Server (MABS) tooback van een Microsoft Exchange server-tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9772f-104">This article describes how tooconfigure Microsoft Azure Backup Server (MABS) tooback up a Microsoft Exchange server tooAzure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="9772f-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9772f-105">Prerequisites</span></span>
<span data-ttu-id="9772f-106">Voordat u doorgaat, zorg ervoor dat Azure Backup-Server [geïnstalleerd en voorbereid](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="9772f-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="9772f-107">De beveiligingsagent MABS</span><span class="sxs-lookup"><span data-stu-id="9772f-107">MABS protection agent</span></span>
<span data-ttu-id="9772f-108">tooinstall hello MABS-beveiligingsagent op Hallo Exchange-server als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="9772f-108">tooinstall hello MABS protection agent on hello Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="9772f-109">Zorg ervoor dat firewalls Hallo correct zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9772f-109">Make sure that hello firewalls are correctly configured.</span></span> <span data-ttu-id="9772f-110">Zie [firewall-uitzonderingen voor Hallo agent configureren](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="9772f-110">See [Configure firewall exceptions for hello agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="9772f-111">Hallo-agent op Hallo Exchange-server installeren door te klikken op **Management > Agents > installeren** MABS Administrator-console.</span><span class="sxs-lookup"><span data-stu-id="9772f-111">Install hello agent on hello Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="9772f-112">Zie [installeren Hallo MABS beveiligingsagent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="9772f-112">See [Install hello MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-hello-exchange-server"></a><span data-ttu-id="9772f-113">Maak een beveiligingsgroep voor Hallo Exchange-server</span><span class="sxs-lookup"><span data-stu-id="9772f-113">Create a protection group for hello Exchange server</span></span>
1. <span data-ttu-id="9772f-114">In Hallo MABS Administrator-Console, klikt u op **beveiliging**, en klik vervolgens op **nieuw** op Hallo hulpprogramma lint tooopen hello **nieuwe beveiligingsgroep maken** wizard.</span><span class="sxs-lookup"><span data-stu-id="9772f-114">In hello MABS Administrator Console, click **Protection**, and then click **New** on hello tool ribbon tooopen hello **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="9772f-115">Op Hallo **Welkom** scherm van de wizard klikt u op Hallo **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-115">On hello **Welcome** screen of hello wizard click **Next**.</span></span>
3. <span data-ttu-id="9772f-116">Op Hallo **type beveiligingsgroep selecteren** scherm, selecteert u **Servers** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-116">On hello **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="9772f-117">Selecteer Hallo Exchange server-database dat u wilt dat tooprotect en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-117">Select hello Exchange server database that you want tooprotect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9772f-118">Als u Exchange 2013 beveiligt, controleert u Hallo [Exchange 2013-vereisten](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="9772f-118">If you are protecting Exchange 2013, check hello [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="9772f-119">In Hallo voorbeeld te volgen, is Hallo Exchange 2010-database geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9772f-119">In hello following example, hello Exchange 2010 database is selected.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="9772f-121">Hallo methode voor gegevensbeveiliging selecteren.</span><span class="sxs-lookup"><span data-stu-id="9772f-121">Select hello data protection method.</span></span>

    <span data-ttu-id="9772f-122">Naam van de beveiligingsgroep Hallo en selecteer vervolgens beide Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="9772f-122">Name hello protection group, and then select both of hello following options:</span></span>

   * <span data-ttu-id="9772f-123">Ik wil kortetermijnbeveiliging met schijf.</span><span class="sxs-lookup"><span data-stu-id="9772f-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="9772f-124">Ik wil online beveiliging.</span><span class="sxs-lookup"><span data-stu-id="9772f-124">I want online protection.</span></span>
6. <span data-ttu-id="9772f-125">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-125">Click **Next**.</span></span>
7. <span data-ttu-id="9772f-126">Selecteer Hallo **Eseutil uitvoeren toocheck gegevensintegriteit** optie als u toocheck Hallo integriteit van Hallo Exchange Server-databases.</span><span class="sxs-lookup"><span data-stu-id="9772f-126">Select hello **Run Eseutil toocheck data integrity** option if you want toocheck hello integrity of hello Exchange Server databases.</span></span>

    <span data-ttu-id="9772f-127">Nadat u deze optie selecteert, back-consistentiecontrole wordt uitgevoerd op een MABS tooavoid Hallo i/o-verkeer dat wordt gegenereerd door het uitvoeren van Hallo **eseutil** opdracht op Hallo Exchange-server.</span><span class="sxs-lookup"><span data-stu-id="9772f-127">After you select this option, backup consistency checking will be run on MABS tooavoid hello I/O traffic that’s generated by running hello **eseutil** command on hello Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9772f-128">toouse deze optie, moet u Hallo Ese.dll en Eseutil.exe bestanden toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin map op Hallo mal server kopiëren.</span><span class="sxs-lookup"><span data-stu-id="9772f-128">toouse this option, you must copy hello Ese.dll and Eseutil.exe files toohello C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on hello MAB server.</span></span> <span data-ttu-id="9772f-129">Anders de volgende fout hello wordt geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="9772f-129">Otherwise, hello following error is triggered:</span></span>  
   > <span data-ttu-id="9772f-130">![Eseutil-fout](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="9772f-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="9772f-131">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-131">Click **Next**.</span></span>
9. <span data-ttu-id="9772f-132">Selecteer Hallo-database voor **kopieback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-132">Select hello database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9772f-133">Als u 'Volledige back-up' voor ten minste één DAG kopie van een database niet selecteert, wordt de logboeken worden niet afgekapt.</span><span class="sxs-lookup"><span data-stu-id="9772f-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="9772f-134">Configureer Hallo doelstellingen voor **kortetermijnback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-134">Configure hello goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="9772f-135">Bekijk de beschikbare schijfruimte Hallo en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-135">Review hello available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="9772f-136">Selecteer de tijd Hallo op welke Hallo mal Server Hallo initiële replicatie maken en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-136">Select hello time at which hello MAB Server will create hello initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="9772f-137">Opties voor consistentiecontrole Hallo selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-137">Select hello consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="9772f-138">Kies Hallo-database wilt tooback up tooAzure en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-138">Choose hello database that you want tooback up tooAzure, and then click **Next**.</span></span> <span data-ttu-id="9772f-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9772f-139">For example:</span></span>

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="9772f-141">Definieer de planning Hallo voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-141">Define hello schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="9772f-142">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="9772f-142">For example:</span></span>

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="9772f-144">Houd er rekening mee Online herstelpunten zijn gebaseerd op snelle volledige herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="9772f-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="9772f-145">Daarom moet u plannen Hallo online herstelpunt worden gemaakt na het Hallo-tijd die opgegeven voor Hallo express volledige herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="9772f-145">Therefore, you must schedule hello online recovery point after hello time that’s specified for hello express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="9772f-146">Configureer Hallo bewaarbeleid voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-146">Configure hello retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="9772f-147">Kies een replicatieoptie online en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="9772f-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="9772f-148">Als er een grote database, kan het lang duren voor Hallo eerste back-toobe via Hallo netwerk gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9772f-148">If you have a large database, it could take a long time for hello initial backup toobe created over hello network.</span></span> <span data-ttu-id="9772f-149">tooavoid dit probleem, kunt u een offline back-up maken.</span><span class="sxs-lookup"><span data-stu-id="9772f-149">tooavoid this issue, you can create an offline backup.</span></span>  

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="9772f-151">Hallo-instellingen bevestigen en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="9772f-151">Confirm hello settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="9772f-152">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="9772f-152">Click **Close**.</span></span>

## <a name="recover-hello-exchange-database"></a><span data-ttu-id="9772f-153">Hallo Exchange-database herstellen</span><span class="sxs-lookup"><span data-stu-id="9772f-153">Recover hello Exchange database</span></span>
1. <span data-ttu-id="9772f-154">toorecover een Exchange-database, klikt u op **herstel** in Hallo MABS Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="9772f-154">toorecover an Exchange database, click **Recovery** in hello MABS Administrator Console.</span></span>
2. <span data-ttu-id="9772f-155">Hallo Exchange-database die u wilt dat toorecover vinden.</span><span class="sxs-lookup"><span data-stu-id="9772f-155">Locate hello Exchange database that you want toorecover.</span></span>
3. <span data-ttu-id="9772f-156">Selecteer een online herstelpunt gemaakt in Hallo *hersteltijd* vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="9772f-156">Select an online recovery point from hello *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="9772f-157">Klik op **herstellen** toostart hello **Herstelwizard**.</span><span class="sxs-lookup"><span data-stu-id="9772f-157">Click **Recover** toostart hello **Recovery Wizard**.</span></span>

<span data-ttu-id="9772f-158">Er zijn vijf herstel-typen voor online herstelpunten:</span><span class="sxs-lookup"><span data-stu-id="9772f-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="9772f-159">**Herstellen van Exchange Server-locatie toooriginal:** Hallo gegevens worden hersteld toohello oorspronkelijke Exchange server.</span><span class="sxs-lookup"><span data-stu-id="9772f-159">**Recover toooriginal Exchange Server location:** hello data will be recovered toohello original Exchange server.</span></span>
* <span data-ttu-id="9772f-160">**Herstel de database op een Exchange Server tooanother:** Hallo gegevens worden tooanother herstelde database op een andere Exchange-server.</span><span class="sxs-lookup"><span data-stu-id="9772f-160">**Recover tooanother database on an Exchange Server:** hello data will be recovered tooanother database on another Exchange server.</span></span>
* <span data-ttu-id="9772f-161">**Tooa hersteldatabase herstellen:** Hallo gegevens worden hersteld tooan Exchange Recovery Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="9772f-161">**Recover tooa Recovery Database:** hello data will be recovered tooan Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="9772f-162">**Kopiëren tooa netwerkmap:** Hallo gegevens worden hersteld tooa netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="9772f-162">**Copy tooa network folder:** hello data will be recovered tooa network folder.</span></span>
* <span data-ttu-id="9772f-163">**Kopieer tootape:** als u een tapewisselaar hebt of een zelfstandig tapestation aangesloten en geconfigureerd op MABS, Hallo herstelpunt is tooa vrije tape gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="9772f-163">**Copy tootape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, hello recovery point will be copied tooa free tape.</span></span>

    ![Kies onlinereplicatie](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="9772f-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9772f-165">Next steps</span></span>
* [<span data-ttu-id="9772f-166">Veelgestelde vragen over Azure Backup</span><span class="sxs-lookup"><span data-stu-id="9772f-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

---
title: Maak een back-up van een Exchange-server op Azure Backup met Azure Backup-Server | Microsoft Docs
description: Meer informatie over het back-up van een Exchange-server op Azure Backup met behulp van Azure Backup-Server
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
ms.openlocfilehash: 60b784fd00013c2b9504f8635c6b5c4c592563be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-azure-backup-server"></a><span data-ttu-id="f14be-103">Back-up van een Exchange-server op Azure Backup met Azure Backup-Server</span><span class="sxs-lookup"><span data-stu-id="f14be-103">Back up an Exchange server to Azure Backup with Azure Backup Server</span></span>
<span data-ttu-id="f14be-104">In dit artikel wordt beschreven hoe u van Microsoft Azure Backup Server (MABS) voor back-up van een Microsoft Exchange-server naar Azure.</span><span class="sxs-lookup"><span data-stu-id="f14be-104">This article describes how to configure Microsoft Azure Backup Server (MABS) to back up a Microsoft Exchange server to Azure.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="f14be-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f14be-105">Prerequisites</span></span>
<span data-ttu-id="f14be-106">Voordat u doorgaat, zorg ervoor dat Azure Backup-Server [geïnstalleerd en voorbereid](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f14be-106">Before you continue, make sure that Azure Backup Server is [installed and prepared](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="mabs-protection-agent"></a><span data-ttu-id="f14be-107">De beveiligingsagent MABS</span><span class="sxs-lookup"><span data-stu-id="f14be-107">MABS protection agent</span></span>
<span data-ttu-id="f14be-108">Als u wilt de MABS-beveiligingsagent installeren op de Exchange server, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="f14be-108">To install the MABS protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="f14be-109">Zorg ervoor dat de firewall correct zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="f14be-109">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="f14be-110">Zie [firewall-uitzonderingen voor de agent configureren](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="f14be-110">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="f14be-111">Installeer de agent op de Exchange-server door te klikken op **Management > Agents > installeren** MABS Administrator-console.</span><span class="sxs-lookup"><span data-stu-id="f14be-111">Install the agent on the Exchange server by clicking **Management > Agents > Install** in MABS Administrator Console.</span></span> <span data-ttu-id="f14be-112">Zie [Installeer de beveiligingsagent MABS](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="f14be-112">See [Install the MABS protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="f14be-113">Maken van een beveiligingsgroep voor de Exchange-server</span><span class="sxs-lookup"><span data-stu-id="f14be-113">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="f14be-114">Klik in de MABS Administrator-Console op **beveiliging**, en klik vervolgens op **nieuw** op het lint openen de **nieuwe beveiligingsgroep maken** wizard.</span><span class="sxs-lookup"><span data-stu-id="f14be-114">In the MABS Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="f14be-115">Op de **Welkom** scherm van de wizard Klik **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-115">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="f14be-116">Op de **type beveiligingsgroep selecteren** scherm, selecteert u **Servers** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-116">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="f14be-117">Selecteer de Exchange server-database die u wilt beveiligen en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-117">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f14be-118">Als u Exchange 2013 beveiligt, controleert u de [Exchange 2013-vereisten](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="f14be-118">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="f14be-119">In het volgende voorbeeld wordt is het Exchange 2010-database geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f14be-119">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="f14be-121">Selecteer de methode voor gegevensbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="f14be-121">Select the data protection method.</span></span>

    <span data-ttu-id="f14be-122">Naam van de beveiligingsgroep en selecteer vervolgens beide van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="f14be-122">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="f14be-123">Ik wil kortetermijnbeveiliging met schijf.</span><span class="sxs-lookup"><span data-stu-id="f14be-123">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="f14be-124">Ik wil online beveiliging.</span><span class="sxs-lookup"><span data-stu-id="f14be-124">I want online protection.</span></span>
6. <span data-ttu-id="f14be-125">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-125">Click **Next**.</span></span>
7. <span data-ttu-id="f14be-126">Selecteer de **Eseutil uitvoeren om gegevensintegriteit te controleren** optie als u wilt controleren de integriteit van de Exchange Server-databases.</span><span class="sxs-lookup"><span data-stu-id="f14be-126">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="f14be-127">Nadat u deze optie selecteert, back-consistentiecontrole wordt uitgevoerd op een MABS om te voorkomen dat het i/o-verkeer dat wordt gegenereerd door het uitvoeren van de **eseutil** opdracht op de Exchange server.</span><span class="sxs-lookup"><span data-stu-id="f14be-127">After you select this option, backup consistency checking will be run on MABS to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f14be-128">Om deze optie gebruikt, moet u de bestanden Ese.dll en Eseutil.exe kopiëren naar de map C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin op de server mal.</span><span class="sxs-lookup"><span data-stu-id="f14be-128">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft Azure Backup\DPM\DPM\bin directory on the MAB server.</span></span> <span data-ttu-id="f14be-129">Anders wordt is de volgende fout geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="f14be-129">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="f14be-130">![Eseutil-fout](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="f14be-130">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="f14be-131">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-131">Click **Next**.</span></span>
9. <span data-ttu-id="f14be-132">Selecteer de database voor **kopieback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-132">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f14be-133">Als u 'Volledige back-up' voor ten minste één DAG kopie van een database niet selecteert, wordt de logboeken worden niet afgekapt.</span><span class="sxs-lookup"><span data-stu-id="f14be-133">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="f14be-134">Configureren van de doelstellingen voor **kortetermijnback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-134">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="f14be-135">Bekijk de beschikbare schijfruimte en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-135">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="f14be-136">Selecteer de tijd waarop de Server mal maken van de initiële replicatie en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-136">Select the time at which the MAB Server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="f14be-137">De opties voor consistentiecontrole selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-137">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="f14be-138">Kies de database die u wilt back-up naar Azure, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-138">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="f14be-139">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f14be-139">For example:</span></span>

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="f14be-141">Definieer de planning voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-141">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="f14be-142">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f14be-142">For example:</span></span>

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="f14be-144">Houd er rekening mee Online herstelpunten zijn gebaseerd op snelle volledige herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="f14be-144">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="f14be-145">Daarom moet u het online herstelpunt plannen nadat de tijd die opgegeven voor de snelle volledige van het herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="f14be-145">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="f14be-146">Configureer het bewaarbeleid voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-146">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="f14be-147">Kies een replicatieoptie online en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="f14be-147">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="f14be-148">Als er een grote database, kan het lang duren voor de eerste back-up worden gemaakt via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="f14be-148">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="f14be-149">Om dit te voorkomen, kunt u een offline back-up maken.</span><span class="sxs-lookup"><span data-stu-id="f14be-149">To avoid this issue, you can create an offline backup.</span></span>  

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="f14be-151">Bevestig de instellingen en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="f14be-151">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="f14be-152">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="f14be-152">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="f14be-153">De Exchange-database herstellen</span><span class="sxs-lookup"><span data-stu-id="f14be-153">Recover the Exchange database</span></span>
1. <span data-ttu-id="f14be-154">Als u wilt herstellen op een Exchange-database, klikt u op **herstel** in de MABS Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="f14be-154">To recover an Exchange database, click **Recovery** in the MABS Administrator Console.</span></span>
2. <span data-ttu-id="f14be-155">Zoek de Exchange-database die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="f14be-155">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="f14be-156">Selecteer een online herstelpunt uit de *hersteltijd* vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="f14be-156">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="f14be-157">Klik op **herstellen** starten de **Herstelwizard**.</span><span class="sxs-lookup"><span data-stu-id="f14be-157">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="f14be-158">Er zijn vijf herstel-typen voor online herstelpunten:</span><span class="sxs-lookup"><span data-stu-id="f14be-158">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="f14be-159">**Herstellen naar oorspronkelijke Exchange Server-locatie:** de gegevens worden hersteld naar de oorspronkelijke Exchange server.</span><span class="sxs-lookup"><span data-stu-id="f14be-159">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="f14be-160">**Herstellen naar een andere database op een Exchange-Server:** de gegevens worden hersteld naar een andere database op een andere Exchange-server.</span><span class="sxs-lookup"><span data-stu-id="f14be-160">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="f14be-161">**Herstellen naar hersteldatabase:** de gegevens worden hersteld naar een Exchange Recovery Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="f14be-161">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="f14be-162">**Kopiëren naar een netwerkmap:** de gegevens worden hersteld naar een netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="f14be-162">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="f14be-163">**Kopiëren naar tape:** als u hebt een tapewisselaar of zelfstandig tapestation gekoppeld en geconfigureerd op MABS, het herstelpunt wordt gekopieerd naar een vrije tape.</span><span class="sxs-lookup"><span data-stu-id="f14be-163">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on MABS, the recovery point will be copied to a free tape.</span></span>

    ![Kies onlinereplicatie](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="f14be-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f14be-165">Next steps</span></span>
* [<span data-ttu-id="f14be-166">Veelgestelde vragen over Azure Backup</span><span class="sxs-lookup"><span data-stu-id="f14be-166">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

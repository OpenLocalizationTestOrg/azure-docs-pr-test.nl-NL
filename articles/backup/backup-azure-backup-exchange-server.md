---
title: Maak een back-up van een Exchange-server op Azure Backup met System Center 2012 R2 DPM | Microsoft Docs
description: Meer informatie over het back-up van een Exchange-server op Azure Backup met System Center 2012 R2 DPM
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
ms.openlocfilehash: 2a0e416440e55cfde70cbd20d40c99fb29b4229c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-an-exchange-server-to-azure-backup-with-system-center-2012-r2-dpm"></a><span data-ttu-id="60355-103">Met System Center 2012 R2 DPM een back-up maken van een Exchange-server in Azure Backup</span><span class="sxs-lookup"><span data-stu-id="60355-103">Back up an Exchange server to Azure Backup with System Center 2012 R2 DPM</span></span>
<span data-ttu-id="60355-104">In dit artikel wordt beschreven hoe een System Center 2012 R2 Data Protection Manager (DPM)-server voor back-up van een Microsoft Exchange-server op Azure Backup configureren.</span><span class="sxs-lookup"><span data-stu-id="60355-104">This article describes how to configure a System Center 2012 R2 Data Protection Manager (DPM) server to back up a Microsoft Exchange server to  Azure Backup.</span></span>  

## <a name="updates"></a><span data-ttu-id="60355-105">Updates</span><span class="sxs-lookup"><span data-stu-id="60355-105">Updates</span></span>
<span data-ttu-id="60355-106">Als u wilt registreren met succes de DPM-server met Azure Backup, moet u het nieuwste updatepakket voor System Center 2012 R2 DPM en de nieuwste versie van de Azure Backup Agent installeren.</span><span class="sxs-lookup"><span data-stu-id="60355-106">To successfully register the DPM server with Azure Backup, you must install the latest update rollup for System Center 2012 R2 DPM and the latest version of the Azure Backup Agent.</span></span> <span data-ttu-id="60355-107">Ophalen van de meest recente updatepakket installeren vanuit de [Microsoft catalogus](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span><span class="sxs-lookup"><span data-stu-id="60355-107">Get the latest update rollup from the [Microsoft Catalog](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=System%20Center%202012%20R2%20Data%20protection%20manager).</span></span>

> [!NOTE]
> <span data-ttu-id="60355-108">Voor de voorbeelden in dit artikel, versie 2.0.8719.0 van de Azure Backup Agent is geïnstalleerd en Update Rollup 6 op System Center 2012 R2 DPM is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="60355-108">For the examples in this article, version 2.0.8719.0 of the Azure Backup Agent is installed, and Update Rollup 6 is installed on System Center 2012 R2 DPM.</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="60355-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="60355-109">Prerequisites</span></span>
<span data-ttu-id="60355-110">Voordat u doorgaat, zorg ervoor dat alle de [vereisten](backup-azure-dpm-introduction.md#prerequisites) voor Microsoft Azure Backup gebruiken om te beschermen werkbelastingen is voldaan.</span><span class="sxs-lookup"><span data-stu-id="60355-110">Before you continue, make sure that all the [prerequisites](backup-azure-dpm-introduction.md#prerequisites) for using Microsoft Azure Backup to protect workloads have been met.</span></span> <span data-ttu-id="60355-111">Deze vereisten omvatten het volgende:</span><span class="sxs-lookup"><span data-stu-id="60355-111">These prerequisites include the following:</span></span>

* <span data-ttu-id="60355-112">Een back-upkluis op de Azure site is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="60355-112">A backup vault on the Azure site has been created.</span></span>
* <span data-ttu-id="60355-113">Agent en de kluisreferenties zijn gedownload naar de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="60355-113">Agent and vault credentials have been downloaded to the DPM server.</span></span>
* <span data-ttu-id="60355-114">De agent is geïnstalleerd op de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="60355-114">The agent is installed on the DPM server.</span></span>
* <span data-ttu-id="60355-115">De kluisreferenties werden gebruikt om de DPM-server te registreren.</span><span class="sxs-lookup"><span data-stu-id="60355-115">The vault credentials were used to register the DPM server.</span></span>
* <span data-ttu-id="60355-116">Als u Exchange 2016 beveiligt, voer een upgrade uit naar DPM 2012 R2 UR9 of hoger</span><span class="sxs-lookup"><span data-stu-id="60355-116">If you are protecting Exchange 2016, please upgrade to DPM 2012 R2 UR9 or later</span></span>

## <a name="dpm-protection-agent"></a><span data-ttu-id="60355-117">DPM-beveiligingsagent</span><span class="sxs-lookup"><span data-stu-id="60355-117">DPM protection agent</span></span>
<span data-ttu-id="60355-118">Voor het installeren van de DPM-beveiligingsagent op de Exchange server, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="60355-118">To install the DPM protection agent on the Exchange server, follow these steps:</span></span>

1. <span data-ttu-id="60355-119">Zorg ervoor dat de firewall correct zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="60355-119">Make sure that the firewalls are correctly configured.</span></span> <span data-ttu-id="60355-120">Zie [firewall-uitzonderingen voor de agent configureren](https://technet.microsoft.com/library/Hh758204.aspx).</span><span class="sxs-lookup"><span data-stu-id="60355-120">See [Configure firewall exceptions for the agent](https://technet.microsoft.com/library/Hh758204.aspx).</span></span>
2. <span data-ttu-id="60355-121">Installeer de agent op de Exchange-server door te klikken op **Management > Agents > installeren** in DPM Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="60355-121">Install the agent on the Exchange server by clicking **Management > Agents > Install** in DPM Administrator Console.</span></span> <span data-ttu-id="60355-122">Zie [de DPM-beveiligingsagent installeren](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="60355-122">See [Install the DPM protection agent](https://technet.microsoft.com/library/hh758186.aspx?f=255&MSPPError=-2147217396) for detailed steps.</span></span>

## <a name="create-a-protection-group-for-the-exchange-server"></a><span data-ttu-id="60355-123">Maken van een beveiligingsgroep voor de Exchange-server</span><span class="sxs-lookup"><span data-stu-id="60355-123">Create a protection group for the Exchange server</span></span>
1. <span data-ttu-id="60355-124">Klik in de DPM Administrator-Console op **beveiliging**, en klik vervolgens op **nieuw** op het lint openen de **nieuwe beveiligingsgroep maken** wizard.</span><span class="sxs-lookup"><span data-stu-id="60355-124">In the DPM Administrator Console, click **Protection**, and then click **New** on the tool ribbon to open the **Create New Protection Group** wizard.</span></span>
2. <span data-ttu-id="60355-125">Op de **Welkom** scherm van de wizard Klik **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-125">On the **Welcome** screen of the wizard click **Next**.</span></span>
3. <span data-ttu-id="60355-126">Op de **type beveiligingsgroep selecteren** scherm, selecteert u **Servers** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-126">On the **Select protection group type** screen, select **Servers** and click **Next**.</span></span>
4. <span data-ttu-id="60355-127">Selecteer de Exchange server-database die u wilt beveiligen en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-127">Select the Exchange server database that you want to protect and click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="60355-128">Als u Exchange 2013 beveiligt, controleert u de [Exchange 2013-vereisten](https://technet.microsoft.com/library/dn751029.aspx).</span><span class="sxs-lookup"><span data-stu-id="60355-128">If you are protecting Exchange 2013, check the [Exchange 2013 prerequisites](https://technet.microsoft.com/library/dn751029.aspx).</span></span>
   >
   >

    <span data-ttu-id="60355-129">In het volgende voorbeeld wordt is het Exchange 2010-database geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="60355-129">In the following example, the Exchange 2010 database is selected.</span></span>

    ![Groepsleden selecteren](./media/backup-azure-backup-exchange-server/select-group-members.png)
5. <span data-ttu-id="60355-131">Selecteer de methode voor gegevensbeveiliging.</span><span class="sxs-lookup"><span data-stu-id="60355-131">Select the data protection method.</span></span>

    <span data-ttu-id="60355-132">Naam van de beveiligingsgroep en selecteer vervolgens beide van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="60355-132">Name the protection group, and then select both of the following options:</span></span>

   * <span data-ttu-id="60355-133">Ik wil kortetermijnbeveiliging met schijf.</span><span class="sxs-lookup"><span data-stu-id="60355-133">I want short-term protection using Disk.</span></span>
   * <span data-ttu-id="60355-134">Ik wil online beveiliging.</span><span class="sxs-lookup"><span data-stu-id="60355-134">I want online protection.</span></span>
6. <span data-ttu-id="60355-135">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-135">Click **Next**.</span></span>
7. <span data-ttu-id="60355-136">Selecteer de **Eseutil uitvoeren om gegevensintegriteit te controleren** optie als u wilt controleren de integriteit van de Exchange Server-databases.</span><span class="sxs-lookup"><span data-stu-id="60355-136">Select the **Run Eseutil to check data integrity** option if you want to check the integrity of the Exchange Server databases.</span></span>

    <span data-ttu-id="60355-137">Nadat u deze optie selecteert, back-consistentiecontrole wordt uitgevoerd op de DPM-server om te voorkomen dat het i/o-verkeer dat wordt gegenereerd door het uitvoeren van de **eseutil** opdracht op de Exchange server.</span><span class="sxs-lookup"><span data-stu-id="60355-137">After you select this option, backup consistency checking will be run on the DPM server to avoid the I/O traffic that’s generated by running the **eseutil** command on the Exchange server.</span></span>

   > [!NOTE]
   > <span data-ttu-id="60355-138">Om deze optie gebruikt, moet u de bestanden Ese.dll en Eseutil.exe kopiëren naar de map C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin op de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="60355-138">To use this option, you must copy the Ese.dll and Eseutil.exe files to the C:\Program Files\Microsoft System Center 2012 R2\DPM\DPM\bin directory on the DPM server.</span></span> <span data-ttu-id="60355-139">Anders wordt is de volgende fout geactiveerd:</span><span class="sxs-lookup"><span data-stu-id="60355-139">Otherwise, the following error is triggered:</span></span>  
   > <span data-ttu-id="60355-140">![Eseutil-fout](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span><span class="sxs-lookup"><span data-stu-id="60355-140">![eseutil error](./media/backup-azure-backup-exchange-server/eseutil-error.png)</span></span>
   >
   >
8. <span data-ttu-id="60355-141">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-141">Click **Next**.</span></span>
9. <span data-ttu-id="60355-142">Selecteer de database voor **kopieback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-142">Select the database for **Copy Backup**, and then click **Next**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="60355-143">Als u 'Volledige back-up' voor ten minste één DAG kopie van een database niet selecteert, wordt de logboeken worden niet afgekapt.</span><span class="sxs-lookup"><span data-stu-id="60355-143">If you do not select “Full backup” for at least one DAG copy of a database, logs will not be truncated.</span></span>
   >
   >
10. <span data-ttu-id="60355-144">Configureren van de doelstellingen voor **kortetermijnback-up**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-144">Configure the goals for **Short-Term backup**, and then click **Next**.</span></span>
11. <span data-ttu-id="60355-145">Bekijk de beschikbare schijfruimte en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-145">Review the available disk space, and then click **Next**.</span></span>
12. <span data-ttu-id="60355-146">Selecteer de tijd waarop de DPM-server maken van de initiële replicatie en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-146">Select the time at which the DPM server will create the initial replication, and then click **Next**.</span></span>
13. <span data-ttu-id="60355-147">De opties voor consistentiecontrole selecteren en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-147">Select the consistency check options, and then click **Next**.</span></span>
14. <span data-ttu-id="60355-148">Kies de database die u wilt back-up naar Azure, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-148">Choose the database that you want to back up to Azure, and then click **Next**.</span></span> <span data-ttu-id="60355-149">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="60355-149">For example:</span></span>

    ![Gegevens voor online beveiliging opgeven](./media/backup-azure-backup-exchange-server/specify-online-protection-data.png)
15. <span data-ttu-id="60355-151">Definieer de planning voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-151">Define the schedule for **Azure Backup**, and then click **Next**.</span></span> <span data-ttu-id="60355-152">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="60355-152">For example:</span></span>

    ![Onlineback-upschema opgeven](./media/backup-azure-backup-exchange-server/specify-online-backup-schedule.png)

    > [!NOTE]
    > <span data-ttu-id="60355-154">Houd er rekening mee Online herstelpunten zijn gebaseerd op snelle volledige herstelpunten.</span><span class="sxs-lookup"><span data-stu-id="60355-154">Note Online recovery points are based on express full recovery points.</span></span> <span data-ttu-id="60355-155">Daarom moet u het online herstelpunt plannen nadat de tijd die opgegeven voor de snelle volledige van het herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="60355-155">Therefore, you must schedule the online recovery point after the time that’s specified for the express full recovery point.</span></span>
    >
    >
16. <span data-ttu-id="60355-156">Configureer het bewaarbeleid voor **Azure Backup**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-156">Configure the retention policy for **Azure Backup**, and then click **Next**.</span></span>
17. <span data-ttu-id="60355-157">Kies een replicatieoptie online en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="60355-157">Choose an online replication option and click **Next**.</span></span>

    <span data-ttu-id="60355-158">Als er een grote database, kan het lang duren voor de eerste back-up worden gemaakt via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="60355-158">If you have a large database, it could take a long time for the initial backup to be created over the network.</span></span> <span data-ttu-id="60355-159">Om dit te voorkomen, kunt u een offline back-up maken.</span><span class="sxs-lookup"><span data-stu-id="60355-159">To avoid this issue, you can create an offline backup.</span></span>  

    ![Onlinebewaarbeleid opgeven](./media/backup-azure-backup-exchange-server/specify-online-retention-policy.png)
18. <span data-ttu-id="60355-161">Bevestig de instellingen en klik vervolgens op **groep maken**.</span><span class="sxs-lookup"><span data-stu-id="60355-161">Confirm the settings, and then click **Create Group**.</span></span>
19. <span data-ttu-id="60355-162">Klik op **Sluiten**.</span><span class="sxs-lookup"><span data-stu-id="60355-162">Click **Close**.</span></span>

## <a name="recover-the-exchange-database"></a><span data-ttu-id="60355-163">De Exchange-database herstellen</span><span class="sxs-lookup"><span data-stu-id="60355-163">Recover the Exchange database</span></span>
1. <span data-ttu-id="60355-164">Als u wilt herstellen op een Exchange-database, klikt u op **herstel** in de DPM Administrator-Console.</span><span class="sxs-lookup"><span data-stu-id="60355-164">To recover an Exchange database, click **Recovery** in the DPM Administrator Console.</span></span>
2. <span data-ttu-id="60355-165">Zoek de Exchange-database die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="60355-165">Locate the Exchange database that you want to recover.</span></span>
3. <span data-ttu-id="60355-166">Selecteer een online herstelpunt uit de *hersteltijd* vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="60355-166">Select an online recovery point from the *recovery time* drop-down list.</span></span>
4. <span data-ttu-id="60355-167">Klik op **herstellen** starten de **Herstelwizard**.</span><span class="sxs-lookup"><span data-stu-id="60355-167">Click **Recover** to start the **Recovery Wizard**.</span></span>

<span data-ttu-id="60355-168">Er zijn vijf herstel-typen voor online herstelpunten:</span><span class="sxs-lookup"><span data-stu-id="60355-168">For online recovery points, there are five recovery types:</span></span>

* <span data-ttu-id="60355-169">**Herstellen naar oorspronkelijke Exchange Server-locatie:** de gegevens worden hersteld naar de oorspronkelijke Exchange server.</span><span class="sxs-lookup"><span data-stu-id="60355-169">**Recover to original Exchange Server location:** The data will be recovered to the original Exchange server.</span></span>
* <span data-ttu-id="60355-170">**Herstellen naar een andere database op een Exchange-Server:** de gegevens worden hersteld naar een andere database op een andere Exchange-server.</span><span class="sxs-lookup"><span data-stu-id="60355-170">**Recover to another database on an Exchange Server:** The data will be recovered to another database on another Exchange server.</span></span>
* <span data-ttu-id="60355-171">**Herstellen naar hersteldatabase:** de gegevens worden hersteld naar een Exchange Recovery Database (RDB).</span><span class="sxs-lookup"><span data-stu-id="60355-171">**Recover to a Recovery Database:** The data will be recovered to an Exchange Recovery Database (RDB).</span></span>
* <span data-ttu-id="60355-172">**Kopiëren naar een netwerkmap:** de gegevens worden hersteld naar een netwerkmap.</span><span class="sxs-lookup"><span data-stu-id="60355-172">**Copy to a network folder:** The data will be recovered to a network folder.</span></span>
* <span data-ttu-id="60355-173">**Kopiëren naar tape:** als u hebt een tapewisselaar of zelfstandig tapestation gekoppeld en geconfigureerd op de DPM-server, het herstelpunt wordt gekopieerd naar een vrije tape.</span><span class="sxs-lookup"><span data-stu-id="60355-173">**Copy to tape:** If you have a tape library or a stand-alone tape drive attached and configured on the DPM server, the recovery point will be copied to a free tape.</span></span>

    ![Kies onlinereplicatie](./media/backup-azure-backup-exchange-server/choose-online-replication.png)

## <a name="next-steps"></a><span data-ttu-id="60355-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60355-175">Next steps</span></span>
* [<span data-ttu-id="60355-176">Veelgestelde vragen over Azure Backup</span><span class="sxs-lookup"><span data-stu-id="60355-176">Azure Backup FAQ</span></span>](backup-azure-backup-faq.md)

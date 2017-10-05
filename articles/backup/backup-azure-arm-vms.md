---
title: Maak een back-up van Azure Virtual machines | Microsoft Docs
description: Detecteren, registreren en back-up van virtuele machines van Azure naar een recovery services-kluis.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: back-up van virtuele machine. back-up van virtuele machine; back-up en herstel na noodgevallen; back-up van arm vm
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="80fae-104">Back-ups maken van virtuele Azure-machines naar een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="80fae-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="80fae-105">Back-up van virtuele machines naar een Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="80fae-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="80fae-106">Back-up van virtuele machines naar Backup-kluis</span><span class="sxs-lookup"><span data-stu-id="80fae-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="80fae-107">Dit artikel wordt uitgelegd hoe u back-up van Azure Virtual machines (geïmplementeerd met Resource Manager en Classic geïmplementeerd) naar een Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="80fae-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="80fae-108">Het merendeel van het werk voor een back-ups van virtuele machines is de voorbereiding.</span><span class="sxs-lookup"><span data-stu-id="80fae-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="80fae-109">Voordat u kunt back-up of een virtuele machine te beveiligen, moet u de [vereisten](backup-azure-arm-vms-prepare.md) voorbereiden van uw omgeving voor het beveiligen van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="80fae-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="80fae-110">Nadat u de vereisten hebt voltooid, kunt u de back-upbewerking om momentopnamen van uw virtuele machine te starten.</span><span class="sxs-lookup"><span data-stu-id="80fae-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="80fae-111">Zie voor meer informatie de artikelen op [plannen van uw back-upinfrastructuur VM in Azure](backup-azure-vms-introduction.md) en [virtuele Azure-machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="80fae-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="80fae-112">Activering van de back-uptaak</span><span class="sxs-lookup"><span data-stu-id="80fae-112">Triggering the backup job</span></span>
<span data-ttu-id="80fae-113">Het back-upbeleid gekoppeld aan de Recovery Services-kluis wordt gedefinieerd hoe vaak en wanneer de back-upbewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="80fae-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="80fae-114">De eerste geplande back-up is standaard de eerste back-up.</span><span class="sxs-lookup"><span data-stu-id="80fae-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="80fae-115">Totdat de eerste back-up plaatsvindt, wordt voor de status van de laatste back-up op de blade **Back-uptaken** de tekst **Waarschuwing (eerste back-up in behandeling)** weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80fae-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Back-up in behandeling](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="80fae-117">Tenzij de eerste back-up binnenkort wordt gemaakt, wordt aanbevolen dat u **Nu een back-up maken** uitvoert.</span><span class="sxs-lookup"><span data-stu-id="80fae-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="80fae-118">De volgende procedure wordt gestart vanuit het kluisdashboard.</span><span class="sxs-lookup"><span data-stu-id="80fae-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="80fae-119">Deze procedure fungeert voor de eerste back-uptaak wordt uitgevoerd nadat u alle vereisten hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="80fae-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="80fae-120">Deze procedure is niet beschikbaar als de eerste back-uptaak al is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="80fae-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="80fae-121">De gekoppelde back-upbeleid bepaalt de volgende back-uptaak.</span><span class="sxs-lookup"><span data-stu-id="80fae-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="80fae-122">De eerste back-uptaak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="80fae-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="80fae-123">Klik op het kluisdashboard op het getal onder **Back-upitems** of klik op de tegel **Back-upitems**.</span><span class="sxs-lookup"><span data-stu-id="80fae-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="80fae-124">
  ![Pictogram Instellingen](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="80fae-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="80fae-125">De blade **Back-upitems** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="80fae-125">The **Backup Items** blade opens.</span></span>

  ![Back-upitems](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="80fae-127">Selecteer het item op de blade **Back-upitems**.</span><span class="sxs-lookup"><span data-stu-id="80fae-127">On the **Backup Items** blade, select the item.</span></span>

  ![Het pictogram Instellingen](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="80fae-129">De lijst **Back-upitems** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="80fae-129">The **Backup Items** list opens.</span></span> <br/>

  ![Geactiveerde back-uptaak](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="80fae-131">Klik in de lijst **Back-upitems** op het weglatingsteken **...**  om het contextmenu te openen.</span><span class="sxs-lookup"><span data-stu-id="80fae-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="80fae-133">Het contextmenu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80fae-133">The Context menu appears.</span></span>

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="80fae-135">Klik in het contextmenu op **Nu back-up maken**.</span><span class="sxs-lookup"><span data-stu-id="80fae-135">On the Context menu, click **Backup now**.</span></span>

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="80fae-137">De blade Nu back-up maken wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="80fae-137">The Backup Now blade opens.</span></span>

  ![toont de blade Nu back-up maken](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="80fae-139">Klik op de blade Nu back-up maken op het kalenderpictogram en selecteer in de kalender de laatste dag dat dit herstelpunt wordt bewaard. Klik vervolgens op **Back-up**.</span><span class="sxs-lookup"><span data-stu-id="80fae-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![de laatste dag instellen dat het herstelpunt van Nu back-up maken wordt bewaard](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="80fae-141">Implementatiemeldingen laten u weten dat de back-uptaak is geactiveerd en dat u de voortgang van de taak op de pagina Back-uptaken kunt controleren.</span><span class="sxs-lookup"><span data-stu-id="80fae-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="80fae-142">Afhankelijk van de grootte van de virtuele machine kan het maken van de eerste back-up even duren.</span><span class="sxs-lookup"><span data-stu-id="80fae-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="80fae-143">Als u de status van de eerste back-up wilt bekijken of volgen, klikt u op de tegel **Back-uptaken** van het kluisdashboard op **Bezig**.</span><span class="sxs-lookup"><span data-stu-id="80fae-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="80fae-145">De blade Back-uptaken wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="80fae-145">The Backup Jobs blade opens.</span></span>

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="80fae-147">Op de blade **Back-uptaken** kunt u de status van alle taken bekijken.</span><span class="sxs-lookup"><span data-stu-id="80fae-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="80fae-148">Controleer of de back-uptaak voor de virtuele machine nog steeds bezig is of is voltooid.</span><span class="sxs-lookup"><span data-stu-id="80fae-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="80fae-149">Wanneer de back-uptaak is voltooid, verandert de status in *Voltooid*.</span><span class="sxs-lookup"><span data-stu-id="80fae-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="80fae-150">Als onderdeel van de back-upbewerking wordt met de Azure Backup-service aan de back-upextensie in elke VM opdracht gegeven om alle schrijfbewerkingen leeg te maken en een consistente momentopname te maken.</span><span class="sxs-lookup"><span data-stu-id="80fae-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="80fae-151">Het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="80fae-151">Troubleshooting errors</span></span>
<span data-ttu-id="80fae-152">Als u problemen tijdens het back-ups maken van uw virtuele machine, Zie de [VM probleemoplossingsartikel](backup-azure-vms-troubleshoot.md) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="80fae-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80fae-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80fae-153">Next steps</span></span>
<span data-ttu-id="80fae-154">Nu u uw virtuele machine hebt beveiligd, gaat u naar de volgende artikelen voor meer informatie over de VM-beheertaken en het herstellen van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="80fae-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="80fae-155">Uw virtuele machines beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="80fae-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="80fae-156">Virtuele machines herstellen</span><span class="sxs-lookup"><span data-stu-id="80fae-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)

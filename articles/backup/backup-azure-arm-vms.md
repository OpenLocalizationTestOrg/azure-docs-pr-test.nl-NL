---
title: aaaBack van Azure Virtual machines | Microsoft Docs
description: Back-up van virtuele machines in Azure recovery services-kluis tooa detecteren en registreren.
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
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="56c36-104">Maak een back-up van virtuele machines in Azure tooa Recovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="56c36-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56c36-105">Back-up van virtuele machines tooRecovery Services-kluis</span><span class="sxs-lookup"><span data-stu-id="56c36-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="56c36-106">Back-up van virtuele machines tooBackup kluis</span><span class="sxs-lookup"><span data-stu-id="56c36-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="56c36-107">Dit artikel wordt uitgelegd hoe tooback van Azure Virtual machines (geïmplementeerd met Resource Manager en Classic geïmplementeerd) tooa Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="56c36-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="56c36-108">De meeste Hallo werk voor back-ups van virtuele machines is Hallo voorbereiding.</span><span class="sxs-lookup"><span data-stu-id="56c36-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="56c36-109">Voordat u kunt back-up of een virtuele machine te beveiligen, moet u Hallo [vereisten](backup-azure-arm-vms-prepare.md) tooprepare uw omgeving voor het beveiligen van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="56c36-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="56c36-110">Nadat u Hallo vereisten hebt voltooid, kunt u Hallo back-upbewerking tootake momentopnamen van uw virtuele machine starten.</span><span class="sxs-lookup"><span data-stu-id="56c36-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="56c36-111">Zie voor meer informatie Hallo artikelen op [plannen van uw back-upinfrastructuur VM in Azure](backup-azure-vms-introduction.md) en [virtuele Azure-machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="56c36-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="56c36-112">Activering van de back-uptaak Hallo</span><span class="sxs-lookup"><span data-stu-id="56c36-112">Triggering hello backup job</span></span>
<span data-ttu-id="56c36-113">Hallo back-upbeleid gekoppeld Hallo die Recovery Services-kluis wordt gedefinieerd hoe vaak en wanneer Hallo back-upbewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="56c36-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="56c36-114">Hallo eerste geplande back-up is standaard Hallo eerste back-up.</span><span class="sxs-lookup"><span data-stu-id="56c36-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="56c36-115">Totdat de eerste back-up Hallo optreedt, Hallo Status van de laatste back-up op Hallo **back-uptaken** blade wordt weergegeven als **waarschuwing (eerste back-up in behandeling)**.</span><span class="sxs-lookup"><span data-stu-id="56c36-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Back-up in behandeling](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="56c36-117">Tenzij u uw eerste back-up toobegin binnenkort is het raadzaam dat u uitvoert **Back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="56c36-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="56c36-118">Hallo begint volgende procedure bij Hallo kluisdashboard.</span><span class="sxs-lookup"><span data-stu-id="56c36-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="56c36-119">Deze procedure fungeert voor het uitvoeren van de eerste back-uptaak Hallo nadat u alle vereisten hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="56c36-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="56c36-120">Deze procedure is niet beschikbaar als de eerste back-uptaak Hallo al is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="56c36-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="56c36-121">Hallo bepaalt gekoppeld back-upbeleid Hallo volgende back-uptaak.</span><span class="sxs-lookup"><span data-stu-id="56c36-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="56c36-122">toorun hello eerste back-uptaak:</span><span class="sxs-lookup"><span data-stu-id="56c36-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="56c36-123">Op het kluisdashboard hello, klikt u op Hallo onder **back-Upitems**, of klik op Hallo **back-Upitems** tegel.</span><span class="sxs-lookup"><span data-stu-id="56c36-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="56c36-124">
  ![Pictogram Instellingen](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="56c36-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="56c36-125">Hallo **back-Upitems** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="56c36-125">hello **Backup Items** blade opens.</span></span>

  ![Back-upitems](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="56c36-127">Op Hallo **back-Upitems** blade, selecteer Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="56c36-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Het pictogram Instellingen](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="56c36-129">Hallo **back-Upitems** lijst wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="56c36-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Geactiveerde back-uptaak](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="56c36-131">Op Hallo **back-Upitems** lijst, klikt u op de weglatingstekens Hallo **...**  tooopen Hallo contextmenu.</span><span class="sxs-lookup"><span data-stu-id="56c36-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="56c36-133">Hallo contextmenu wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="56c36-133">hello Context menu appears.</span></span>

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="56c36-135">Klik in het contextmenu hello, **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="56c36-135">On hello Context menu, click **Backup now**.</span></span>

  ![Contextmenu](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="56c36-137">back-up nu Hallo-blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="56c36-137">hello Backup Now blade opens.</span></span>

  ![ziet u nu back-up Hallo-blade](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="56c36-139">Klik op Hallo nu back-up blade op Hallo kalenderpictogram, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard, en klik op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="56c36-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![set Hallo laatste dag Hallo nu back-up een herstelpunt wordt bewaard](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="56c36-141">Meldingen van de implementatie kunnen u weten Hallo back-uptaak is geactiveerd en dat u kunt voortgang Hallo van Hallo-taak op de pagina Hallo back-up-taken.</span><span class="sxs-lookup"><span data-stu-id="56c36-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="56c36-142">Afhankelijk van de grootte van de Hallo van uw virtuele machine, kan Hallo eerste back-up maken duren.</span><span class="sxs-lookup"><span data-stu-id="56c36-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="56c36-143">tooview of bijhouden Hallo-status van Hallo eerste back-up, op Hallo kluisdashboard op Hallo **back-uptaken** Klik op de tegel **Bezig**.</span><span class="sxs-lookup"><span data-stu-id="56c36-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="56c36-145">de blade back-uptaken Hello wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="56c36-145">hello Backup Jobs blade opens.</span></span>

  ![Tegel Back-uptaken](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="56c36-147">In Hallo **back-uptaken** blade ziet u Hallo status van alle taken.</span><span class="sxs-lookup"><span data-stu-id="56c36-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="56c36-148">Controleer als Hallo back-uptaak voor uw virtuele machine wordt nog uitgevoerd of als het is voltooid.</span><span class="sxs-lookup"><span data-stu-id="56c36-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="56c36-149">Wanneer een back-uptaak is voltooid, is het Hallo-status *voltooid*.</span><span class="sxs-lookup"><span data-stu-id="56c36-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="56c36-150">Als onderdeel van de back-upbewerking Hallo verstrekt hello Azure Backup-service een toohello opdracht Backup-extensie in elke VM tooflush alle schrijft en een consistente momentopname.</span><span class="sxs-lookup"><span data-stu-id="56c36-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="56c36-151">Het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="56c36-151">Troubleshooting errors</span></span>
<span data-ttu-id="56c36-152">Als u problemen tijdens het back-ups maken van uw virtuele machine, Zie Hallo [VM probleemoplossingsartikel](backup-azure-vms-troubleshoot.md) voor hulp.</span><span class="sxs-lookup"><span data-stu-id="56c36-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="56c36-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56c36-153">Next steps</span></span>
<span data-ttu-id="56c36-154">Nu u uw virtuele machine hebt beveiligd, gaat u naar Hallo na toolearn artikelen over VM beheertaken, en hoe toorestore virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="56c36-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="56c36-155">Uw virtuele machines beheren en controleren</span><span class="sxs-lookup"><span data-stu-id="56c36-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="56c36-156">Virtuele machines herstellen</span><span class="sxs-lookup"><span data-stu-id="56c36-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)

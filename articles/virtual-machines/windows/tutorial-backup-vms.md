---
title: aaaBackup VM's van Windows Azure | Microsoft-Docs
description: Uw Windows-VM's beveiligen door deze back-ups van maken met Azure Backup.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a><span data-ttu-id="aedf6-103">Back-up van Windows virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="aedf6-103">Back up Windows virtual machines in Azure</span></span>

<span data-ttu-id="aedf6-104">U kunt uw gegevens beschermen door regelmatig back-ups te maken.</span><span class="sxs-lookup"><span data-stu-id="aedf6-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="aedf6-105">Azure Backup maakt herstelpunten die zijn opgeslagen in een geografisch redundante recovery kluizen.</span><span class="sxs-lookup"><span data-stu-id="aedf6-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="aedf6-106">Wanneer u vanaf een herstelpunt herstelt, kunt u herstellen Hallo hele virtuele machine of alleen specifieke bestanden.</span><span class="sxs-lookup"><span data-stu-id="aedf6-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="aedf6-107">Dit artikel wordt uitgelegd hoe toorestore één bestand tooa virtuele machine met Windows Server- en IIS.</span><span class="sxs-lookup"><span data-stu-id="aedf6-107">This article explains how toorestore a single file tooa VM running Windows Server and IIS.</span></span> <span data-ttu-id="aedf6-108">Als u een VM-toouse nog geen hebt, kunt u een maken met behulp van Hallo [Windows-snelstartgids](quick-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="aedf6-108">If you don't already have a VM toouse, you can create one using hello [Windows quickstart](quick-create-portal.md).</span></span> <span data-ttu-id="aedf6-109">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="aedf6-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aedf6-110">Maak een back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="aedf6-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="aedf6-111">Een dagelijkse back-up plannen</span><span class="sxs-lookup"><span data-stu-id="aedf6-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="aedf6-112">Een bestand te herstellen vanaf een back-up</span><span class="sxs-lookup"><span data-stu-id="aedf6-112">Restore a file from a backup</span></span>




## <a name="backup-overview"></a><span data-ttu-id="aedf6-113">Overzicht van Backup</span><span class="sxs-lookup"><span data-stu-id="aedf6-113">Backup overview</span></span>

<span data-ttu-id="aedf6-114">Wanneer hello Azure Backup-service een back-uptaak initieert, activeert het Hallo Backup-extensie tootake een momentopname van een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="aedf6-114">When hello Azure Backup service initiates a backup job, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="aedf6-115">Hello Azure Backup-service gebruikt Hallo _VMSnapshot_ extensie.</span><span class="sxs-lookup"><span data-stu-id="aedf6-115">hello Azure Backup service uses hello _VMSnapshot_ extension.</span></span> <span data-ttu-id="aedf6-116">Hallo-extensie wordt geïnstalleerd tijdens Hallo eerste VM back-up als Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aedf6-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="aedf6-117">Als hello VM niet wordt uitgevoerd, wordt Hallo Backup-service een momentopname van Hallo onderliggende opslag (omdat er geen schrijfbewerkingen toepassing tijdens het Hallo die VM is gestopt optreden).</span><span class="sxs-lookup"><span data-stu-id="aedf6-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="aedf6-118">Bij het nemen van een momentopname van VM's van Windows coördineert hello Backup-service met Hallo Volume Shadow Copy Service (VSS) tooget een consistente momentopname te maken van schijven Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aedf6-118">When taking a snapshot of Windows VMs, hello Backup service coordinates with hello Volume Shadow Copy Service (VSS) tooget a consistent snapshot of hello virtual machine's disks.</span></span> <span data-ttu-id="aedf6-119">Zodra hello Azure Backup-service Hallo momentopname maakt, is Hallo gegevens overgedragen toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="aedf6-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="aedf6-120">toomaximize-efficiëntie Hallo service identificeert en alleen Hallo blokken met gegevens die zijn gewijzigd sinds de vorige back-up Hallo overdraagt.</span><span class="sxs-lookup"><span data-stu-id="aedf6-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="aedf6-121">Hallo-gegevensoverdracht is voltooid, Hallo momentopname wordt verwijderd als een herstelpunt wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aedf6-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="aedf6-122">Maak een back-up</span><span class="sxs-lookup"><span data-stu-id="aedf6-122">Create a backup</span></span>
<span data-ttu-id="aedf6-123">Maak een eenvoudige geplande dagelijkse back-tooa Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="aedf6-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="aedf6-124">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="aedf6-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="aedf6-125">Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="aedf6-126">Selecteer een VM-tooback uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="aedf6-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="aedf6-127">Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="aedf6-128">Hallo **back-up** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="aedf6-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="aedf6-129">In **Recovery Services-kluis**, klikt u op **nieuw** en geef de naam Hallo voor Hallo nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="aedf6-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="aedf6-130">Een nieuwe kluis is gemaakt in Hallo dezelfde resourcegroep en locatie als Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aedf6-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="aedf6-131">Klik op **back-up maken van beleid**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-131">Click **Backup policy**.</span></span> <span data-ttu-id="aedf6-132">In dit voorbeeld blijven Hallo standaardwaarden en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="aedf6-133">Op Hallo **back-up** blade, klikt u op **back-up inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="aedf6-134">Hiermee maakt u een dagelijkse back-up op basis van het standaardschema Hallo.</span><span class="sxs-lookup"><span data-stu-id="aedf6-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="aedf6-135">een eerste herstelpunt op Hallo toocreate **back-up** Klik op de blade **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="aedf6-136">Op Hallo **back-up nu** blade, klikt u op het pictogram Kalender Hallo, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard en op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="aedf6-137">In Hallo **back-up** blade voor uw virtuele machine, ziet u Hallo aantal herstelpunten die voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="aedf6-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Herstelpunten](./media/tutorial-backup-vms/backup-complete.png)
    
<span data-ttu-id="aedf6-139">de eerste back-up Hallo duurt ongeveer 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="aedf6-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="aedf6-140">Toohello volgende deel van deze zelfstudie worden voortgezet nadat de back-up is voltooid.</span><span class="sxs-lookup"><span data-stu-id="aedf6-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="recover-a-file"></a><span data-ttu-id="aedf6-141">Herstellen van een bestand</span><span class="sxs-lookup"><span data-stu-id="aedf6-141">Recover a file</span></span>

<span data-ttu-id="aedf6-142">Als u per ongeluk verwijdert of wijzigingen tooa bestand maken, kunt u bestandsherstel toorecover Hallo bestand vanuit uw back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="aedf6-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="aedf6-143">Bestandsherstel maakt gebruik van een script dat wordt uitgevoerd op virtuele machine, Hallo toomount Hallo herstelpunt als lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="aedf6-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="aedf6-144">Deze stations blijft gekoppelde 12 uur zodat u kunt bestanden vanaf Hallo herstelpunt kopiëren en herstel deze toohello VM.</span><span class="sxs-lookup"><span data-stu-id="aedf6-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="aedf6-145">In dit voorbeeld laten we zien hoe toorecover Hallo installatiekopiebestand op dat wordt gebruikt in Hallo standaardwebpagina voor IIS.</span><span class="sxs-lookup"><span data-stu-id="aedf6-145">In this example, we show how toorecover hello image file that is used in hello default web page for IIS.</span></span> 

1. <span data-ttu-id="aedf6-146">Open een browser en maak verbinding toohello IP-adres van Hallo VM tooshow Hallo standaard IIS-pagina.</span><span class="sxs-lookup"><span data-stu-id="aedf6-146">Open a browser and connect toohello IP address of hello VM tooshow hello default IIS page.</span></span>

    ![IIS-standaardwebpagina](./media/tutorial-backup-vms/iis-working.png)

2. <span data-ttu-id="aedf6-148">Verbinding maken met toohello VM.</span><span class="sxs-lookup"><span data-stu-id="aedf6-148">Connect toohello VM.</span></span>
3. <span data-ttu-id="aedf6-149">Open op Hallo VM, **Verkenner** en navigeer too\inetpub\wwwroot en verwijder het Hallo-bestand **iisstart.png**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-149">On hello VM, open **File Explorer** and navigate too\inetpub\wwwroot and delete hello file **iisstart.png**.</span></span>
4. <span data-ttu-id="aedf6-150">Vernieuwen Hallo browser toosee die de installatiekopie op de standaardpagina IIS Hallo Hallo is op de lokale computer verwijderd.</span><span class="sxs-lookup"><span data-stu-id="aedf6-150">On your local computer, refresh hello browser toosee that hello image on hello default IIS page is gone.</span></span>

    ![IIS-standaardwebpagina](./media/tutorial-backup-vms/iis-broken.png)

5. <span data-ttu-id="aedf6-152">Open op uw lokale computer, een nieuw tabblad en ga Hallo Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aedf6-152">On your local computer, open a new tab and go hello hello [Azure portal](https://portal.azure.com).</span></span>
6. <span data-ttu-id="aedf6-153">Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines** en selecteer Hallo VM formulier Hallo lijst.</span><span class="sxs-lookup"><span data-stu-id="aedf6-153">In hello menu on hello left, select **Virtual machines** and select hello VM form hello list.</span></span>
8. <span data-ttu-id="aedf6-154">Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-154">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="aedf6-155">Hallo **back-up** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="aedf6-155">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="aedf6-156">Selecteer in het menu Hallo Hallo boven aan het Hallo-blade **bestandsherstel**.</span><span class="sxs-lookup"><span data-stu-id="aedf6-156">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="aedf6-157">Hallo **bestandsherstel** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="aedf6-157">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="aedf6-158">In **stap 1: Selecteer herstelpunt**, selecteer een herstelpunt in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="aedf6-158">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="aedf6-159">In **stap 2: downloaden script toobrowse en bestanden herstellen**, klikt u op Hallo **uitvoerbaar bestand downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="aedf6-159">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="aedf6-160">Hallo bestand tooyour opslaan **downloadt** map.</span><span class="sxs-lookup"><span data-stu-id="aedf6-160">Save hello file tooyour **Downloads** folder.</span></span>
12. <span data-ttu-id="aedf6-161">Open op uw lokale computer **Verkenner** en navigeer tooyour **downloadt** map en kopieer Hallo .exe-bestand hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="aedf6-161">On your local computer, open **File Explorer** and navigate tooyour **Downloads** folder and copy hello downloaded .exe file.</span></span> <span data-ttu-id="aedf6-162">Hallo filename wordt voorafgegaan door de naam van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="aedf6-162">hello filename will be prefixed by your VM name.</span></span> 
13. <span data-ttu-id="aedf6-163">Plak Hallo .exe-bestand toohello bureaublad van uw virtuele machine op de virtuele machine (via Hallo RDP-verbinding).</span><span class="sxs-lookup"><span data-stu-id="aedf6-163">On your VM (over hello RDP connection) paste hello .exe file toohello Desktop of your VM.</span></span> 
14. <span data-ttu-id="aedf6-164">Ga toohello bureaublad van uw virtuele machine en dubbelklik op Hallo .exe.</span><span class="sxs-lookup"><span data-stu-id="aedf6-164">Navigate toohello desktop of your VM and double-click on hello .exe.</span></span> <span data-ttu-id="aedf6-165">Hiermee wordt een opdrachtprompt en koppel vervolgens Hallo herstelpunt worden gemaakt als een bestandsshare die u toegang hebt tot.</span><span class="sxs-lookup"><span data-stu-id="aedf6-165">This will launch a command prompt and then mount hello recovery point as a file share that you can access.</span></span> <span data-ttu-id="aedf6-166">Wanneer deze is voltooid maken Hallo share, typt u **q** tooclose Hallo-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="aedf6-166">When it is finished creating hello share, type **q** tooclose hello command prompt.</span></span>
15. <span data-ttu-id="aedf6-167">Open op uw virtuele machine, **Verkenner** en navigeer toohello stationsletter is die is gebruikt voor het Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="aedf6-167">On your VM, open **File Explorer** and navigate toohello drive letter that was used for hello file share.</span></span>
16. <span data-ttu-id="aedf6-168">Navigeer too\inetpub\wwwroot en kopieer **iisstart.png** uit Hallo-bestand delen en plak deze in \inetpub\wwwroot.</span><span class="sxs-lookup"><span data-stu-id="aedf6-168">Navigate too\inetpub\wwwroot and copy **iisstart.png** from hello file share and paste it into \inetpub\wwwroot.</span></span> <span data-ttu-id="aedf6-169">Bijvoorbeeld: F:\inetpub\wwwroot\iisstart.png Kopieer en plak deze in c:\inetpub\wwwroot toorecover Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="aedf6-169">For example, copy F:\inetpub\wwwroot\iisstart.png and paste it into c:\inetpub\wwwroot toorecover hello file.</span></span>
17. <span data-ttu-id="aedf6-170">Open op uw lokale computer Hallo browsertabblad waar u bent verbonden toohello IP-adres van Hallo VM van Hallo IIS standaard de pagina.</span><span class="sxs-lookup"><span data-stu-id="aedf6-170">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello IIS default page.</span></span> <span data-ttu-id="aedf6-171">Druk op CTRL + F5 toorefresh Hallo browserpagina.</span><span class="sxs-lookup"><span data-stu-id="aedf6-171">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="aedf6-172">U ziet nu dat Hallo afbeelding is hersteld.</span><span class="sxs-lookup"><span data-stu-id="aedf6-172">You should now see that hello image has been restored.</span></span>
18. <span data-ttu-id="aedf6-173">Op de lokale computer, gaat u terug toohello browsertabblad voor hello Azure-portal en in **stap 3: Hallo schijven ontkoppelen na het herstel** klikt u op Hallo **schijven ontkoppelen** knop.</span><span class="sxs-lookup"><span data-stu-id="aedf6-173">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="aedf6-174">Als u toodo deze stap vergeet, wordt na 12 uur Hallo verbinding toohello koppelpunt automatisch sluiten.</span><span class="sxs-lookup"><span data-stu-id="aedf6-174">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="aedf6-175">Na deze 12 uur moet u een nieuwe script toocreate een nieuwe koppelpunt toodownload.</span><span class="sxs-lookup"><span data-stu-id="aedf6-175">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="aedf6-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aedf6-176">Next steps</span></span>

<span data-ttu-id="aedf6-177">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="aedf6-177">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aedf6-178">Maak een back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="aedf6-178">Create a backup of a VM</span></span>
> * <span data-ttu-id="aedf6-179">Een dagelijkse back-up plannen</span><span class="sxs-lookup"><span data-stu-id="aedf6-179">Schedule a daily backup</span></span>
> * <span data-ttu-id="aedf6-180">Een bestand te herstellen vanaf een back-up</span><span class="sxs-lookup"><span data-stu-id="aedf6-180">Restore a file from a backup</span></span>

<span data-ttu-id="aedf6-181">Ga toohello volgende zelfstudie toolearn over het bewaken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="aedf6-181">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="aedf6-182">Virtuele machines bewaken</span><span class="sxs-lookup"><span data-stu-id="aedf6-182">Monitor virtual machines</span></span>](tutorial-monitoring.md)










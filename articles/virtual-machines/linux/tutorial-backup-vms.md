---
title: Back-up van Azure Linux VM's | Microsoft Docs
description: Uw virtuele Linux-machines beveiligen door deze back-ups van maken met Azure Backup.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 7c00392d5185a2f067f2ee2717529dcbde1e71f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-linux--virtual-machines-in-azure"></a><span data-ttu-id="06420-103">Back-up van Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="06420-103">Back up Linux  virtual machines in Azure</span></span>

<span data-ttu-id="06420-104">U kunt uw gegevens beschermen door regelmatig back-ups te maken.</span><span class="sxs-lookup"><span data-stu-id="06420-104">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="06420-105">Azure Backup maakt herstelpunten die zijn opgeslagen in een geografisch redundante recovery kluizen.</span><span class="sxs-lookup"><span data-stu-id="06420-105">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="06420-106">Wanneer u vanaf een herstelpunt herstelt, kunt u herstellen Hallo hele virtuele machine of alleen specifieke bestanden.</span><span class="sxs-lookup"><span data-stu-id="06420-106">When you restore from a recovery point, you can restore hello whole VM or just specific files.</span></span> <span data-ttu-id="06420-107">Dit artikel wordt uitgelegd hoe toorestore één tooa Linux VM actieve nginx-bestand.</span><span class="sxs-lookup"><span data-stu-id="06420-107">This article explains how toorestore a single file tooa Linux VM running nginx.</span></span> <span data-ttu-id="06420-108">Als u een VM-toouse nog geen hebt, kunt u een maken met behulp van Hallo [Linux Quick Start](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="06420-108">If you don't already have a VM toouse, you can create one using hello [Linux quickstart](quick-create-cli.md).</span></span> <span data-ttu-id="06420-109">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="06420-109">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="06420-110">Maak een back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="06420-110">Create a backup of a VM</span></span>
> * <span data-ttu-id="06420-111">Een dagelijkse back-up plannen</span><span class="sxs-lookup"><span data-stu-id="06420-111">Schedule a daily backup</span></span>
> * <span data-ttu-id="06420-112">Een bestand te herstellen vanaf een back-up</span><span class="sxs-lookup"><span data-stu-id="06420-112">Restore a file from a backup</span></span>



## <a name="backup-overview"></a><span data-ttu-id="06420-113">Overzicht van Backup</span><span class="sxs-lookup"><span data-stu-id="06420-113">Backup overview</span></span>

<span data-ttu-id="06420-114">Wanneer hello Azure Backup-service een back-up begint, activeert het Hallo Backup-extensie tootake een momentopname van een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="06420-114">When hello Azure Backup service initiates a backup, it triggers hello backup extension tootake a point-in-time snapshot.</span></span> <span data-ttu-id="06420-115">Hello Azure Backup-service gebruikt Hallo _VMSnapshotLinux_ extensie in Linux.</span><span class="sxs-lookup"><span data-stu-id="06420-115">hello Azure Backup service uses hello _VMSnapshotLinux_ extension in Linux.</span></span> <span data-ttu-id="06420-116">Hallo-extensie wordt geïnstalleerd tijdens Hallo eerste VM back-up als Hallo VM wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="06420-116">hello extension is installed during hello first VM backup if hello VM is running.</span></span> <span data-ttu-id="06420-117">Als hello VM niet wordt uitgevoerd, wordt Hallo Backup-service een momentopname van Hallo onderliggende opslag (omdat er geen schrijfbewerkingen toepassing tijdens het Hallo die VM is gestopt optreden).</span><span class="sxs-lookup"><span data-stu-id="06420-117">If hello VM is not running, hello Backup service takes a snapshot of hello underlying storage (since no application writes occur while hello VM is stopped).</span></span>

<span data-ttu-id="06420-118">Standaard Azure Backup heeft een bestand system consistente back-up voor Linux VM maar het kan geconfigureerde tootake [toepassing consistente back-up met script voor vóór en na-framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span><span class="sxs-lookup"><span data-stu-id="06420-118">By default, Azure Backup takes a file system consistent backup for Linux VM but it can be configured tootake [application consistent backup using pre-script and post-script framework](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).</span></span> <span data-ttu-id="06420-119">Zodra hello Azure Backup-service Hallo momentopname maakt, is Hallo gegevens overgedragen toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="06420-119">Once hello Azure Backup service takes hello snapshot, hello data is transferred toohello vault.</span></span> <span data-ttu-id="06420-120">toomaximize-efficiëntie Hallo service identificeert en alleen Hallo blokken met gegevens die zijn gewijzigd sinds de vorige back-up Hallo overdraagt.</span><span class="sxs-lookup"><span data-stu-id="06420-120">toomaximize efficiency, hello service identifies and transfers only hello blocks of data that have changed since hello previous backup.</span></span>

<span data-ttu-id="06420-121">Hallo-gegevensoverdracht is voltooid, Hallo momentopname wordt verwijderd als een herstelpunt wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="06420-121">When hello data transfer is complete, hello snapshot is removed and a recovery point is created.</span></span>


## <a name="create-a-backup"></a><span data-ttu-id="06420-122">Maak een back-up</span><span class="sxs-lookup"><span data-stu-id="06420-122">Create a backup</span></span>
<span data-ttu-id="06420-123">Maak een eenvoudige geplande dagelijkse back-tooa Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="06420-123">Create a simple scheduled daily backup tooa Recovery Services Vault.</span></span> 

1. <span data-ttu-id="06420-124">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="06420-124">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="06420-125">Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="06420-125">In hello menu on hello left, select **Virtual machines**.</span></span> 
3. <span data-ttu-id="06420-126">Selecteer een VM-tooback uit Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="06420-126">From hello list, select a VM tooback up.</span></span>
4. <span data-ttu-id="06420-127">Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="06420-127">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="06420-128">Hallo **back-up** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="06420-128">hello **Enable backup** blade opens.</span></span>
5. <span data-ttu-id="06420-129">In **Recovery Services-kluis**, klikt u op **nieuw** en geef de naam Hallo voor Hallo nieuwe kluis.</span><span class="sxs-lookup"><span data-stu-id="06420-129">In **Recovery Services vault**, click **Create new** and provide hello name for hello new vault.</span></span> <span data-ttu-id="06420-130">Een nieuwe kluis is gemaakt in Hallo dezelfde resourcegroep en locatie als Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="06420-130">A new vault is created in hello same Resource Group and location as hello virtual machine.</span></span>
6. <span data-ttu-id="06420-131">Klik op **back-up maken van beleid**.</span><span class="sxs-lookup"><span data-stu-id="06420-131">Click **Backup policy**.</span></span> <span data-ttu-id="06420-132">In dit voorbeeld blijven Hallo standaardwaarden en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="06420-132">For this example, keep hello defaults and click **OK**.</span></span>
7. <span data-ttu-id="06420-133">Op Hallo **back-up** blade, klikt u op **back-up inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="06420-133">On hello **Enable backup** blade, click **Enable Backup**.</span></span> <span data-ttu-id="06420-134">Hiermee maakt u een dagelijkse back-up op basis van het standaardschema Hallo.</span><span class="sxs-lookup"><span data-stu-id="06420-134">This creates a daily backup based on hello default schedule.</span></span>
10. <span data-ttu-id="06420-135">een eerste herstelpunt op Hallo toocreate **back-up** Klik op de blade **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="06420-135">toocreate an initial recovery point, on hello **Backup** blade click **Backup now**.</span></span>
11. <span data-ttu-id="06420-136">Op Hallo **back-up nu** blade, klikt u op het pictogram Kalender Hallo, gebruikt u Hallo kalender besturingselement tooselect Hallo laatste dag van dit herstelpunt wordt bewaard en op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="06420-136">On hello **Backup Now** blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>
12. <span data-ttu-id="06420-137">In Hallo **back-up** blade voor uw virtuele machine, ziet u Hallo aantal herstelpunten die voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="06420-137">In hello **Backup** blade for your VM, you will see hello number of recovery points that are complete.</span></span>

    ![Herstelpunten](./media/tutorial-backup-vms/backup-complete.png)

<span data-ttu-id="06420-139">de eerste back-up Hallo duurt ongeveer 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="06420-139">hello first backup takes about 20 minutes.</span></span> <span data-ttu-id="06420-140">Toohello volgende deel van deze zelfstudie worden voortgezet nadat de back-up is voltooid.</span><span class="sxs-lookup"><span data-stu-id="06420-140">Proceed toohello next part of this tutorial after your backup is finished.</span></span>

## <a name="restore-a-file"></a><span data-ttu-id="06420-141">Een bestand te herstellen</span><span class="sxs-lookup"><span data-stu-id="06420-141">Restore a file</span></span>

<span data-ttu-id="06420-142">Als u per ongeluk verwijdert of wijzigingen tooa bestand maken, kunt u bestandsherstel toorecover Hallo bestand vanuit uw back-upkluis.</span><span class="sxs-lookup"><span data-stu-id="06420-142">If you accidentally delete or make changes tooa file, you can use File Recovery toorecover hello file from your backup vault.</span></span> <span data-ttu-id="06420-143">Bestandsherstel maakt gebruik van een script dat wordt uitgevoerd op virtuele machine, Hallo toomount Hallo herstelpunt als lokale schijf.</span><span class="sxs-lookup"><span data-stu-id="06420-143">File Recovery uses a script that runs on hello VM, toomount hello recovery point as local drive.</span></span> <span data-ttu-id="06420-144">Deze stations blijft gekoppelde 12 uur zodat u kunt bestanden vanaf Hallo herstelpunt kopiëren en herstel deze toohello VM.</span><span class="sxs-lookup"><span data-stu-id="06420-144">These drives will remain mounted for 12 hours so that you can copy files from hello recovery point and restore them toohello VM.</span></span>  

<span data-ttu-id="06420-145">In dit voorbeeld laten we zien hoe toorecover standaard nginx webpagina /var/www/html/index.nginx-debian.html Hallo.</span><span class="sxs-lookup"><span data-stu-id="06420-145">In this example, we show how toorecover hello default nginx web page /var/www/html/index.nginx-debian.html.</span></span> <span data-ttu-id="06420-146">Hallo openbare IP-adres van de virtuele machine in dit voorbeeld is *13.69.75.209*.</span><span class="sxs-lookup"><span data-stu-id="06420-146">hello public IP address of our VM in this example is *13.69.75.209*.</span></span> <span data-ttu-id="06420-147">U vindt Hallo IP-adres van uw virtuele machine met:</span><span class="sxs-lookup"><span data-stu-id="06420-147">You can find hello IP address of your vm using:</span></span>

 ```bash 
 az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
 ```

 
1. <span data-ttu-id="06420-148">Open een browser en typ Hallo openbare IP-adres van uw VM toosee hello nginx standaardwebpagina op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="06420-148">On your local computer, open a browser and type in hello public IP address of your VM toosee hello default nginx web page.</span></span>

    ![Standaard nginx-webpagina](./media/tutorial-backup-vms/nginx-working.png)

1. <span data-ttu-id="06420-150">SSH in uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="06420-150">SSH into your VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
2. <span data-ttu-id="06420-151">/Var/www/html/index.nginx-debian.html verwijderen.</span><span class="sxs-lookup"><span data-stu-id="06420-151">Delete /var/www/html/index.nginx-debian.html.</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```
    
4. <span data-ttu-id="06420-152">Op de lokale computer, vernieuwt u Hallo browser kunt u door op CTRL + F5 toosee die standaard nginx-pagina is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="06420-152">On your local computer, refresh hello browser by hitting CTRL + F5 toosee that default nginx page is gone.</span></span>

    ![Standaard nginx-webpagina](./media/tutorial-backup-vms/nginx-broken.png)
    
1. <span data-ttu-id="06420-154">Meld u op uw lokale computer aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="06420-154">On your local computer, sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
6. <span data-ttu-id="06420-155">Selecteer in het menu aan de linkerkant Hallo Hallo **virtuele machines**.</span><span class="sxs-lookup"><span data-stu-id="06420-155">In hello menu on hello left, select **Virtual machines**.</span></span> 
7. <span data-ttu-id="06420-156">Selecteer in Hallo lijst Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="06420-156">From hello list, select hello VM.</span></span>
8. <span data-ttu-id="06420-157">Op Hallo VM blade in Hallo **instellingen** sectie, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="06420-157">On hello VM blade, in hello **Settings** section, click **Backup**.</span></span> <span data-ttu-id="06420-158">Hallo **back-up** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="06420-158">hello **Backup** blade opens.</span></span> 
9. <span data-ttu-id="06420-159">Selecteer in het menu Hallo Hallo boven aan het Hallo-blade **bestandsherstel**.</span><span class="sxs-lookup"><span data-stu-id="06420-159">In hello menu at hello top of hello blade, select **File Recovery**.</span></span> <span data-ttu-id="06420-160">Hallo **bestandsherstel** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="06420-160">hello **File Recovery** blade opens.</span></span>
10. <span data-ttu-id="06420-161">In **stap 1: Selecteer herstelpunt**, selecteer een herstelpunt in de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="06420-161">In **Step 1: Select recovery point**, select a recovery point from hello drop-down.</span></span>
11. <span data-ttu-id="06420-162">In **stap 2: downloaden script toobrowse en bestanden herstellen**, klikt u op Hallo **uitvoerbaar bestand downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="06420-162">In **Step 2: Download script toobrowse and recover files**, click hello **Download Executable** button.</span></span> <span data-ttu-id="06420-163">Hallo gedownloade bestand tooyour lokale computer opslaan.</span><span class="sxs-lookup"><span data-stu-id="06420-163">Save hello downloaded file tooyour local computer.</span></span>
7. <span data-ttu-id="06420-164">Klik op **script downloaden** toodownload Hallo scriptbestand lokaal.</span><span class="sxs-lookup"><span data-stu-id="06420-164">Click **Download script** toodownload hello script file locally.</span></span>
8. <span data-ttu-id="06420-165">Open een Bash-prompt en type hello te volgen en vervangt *Linux_myVM_05-05-2017.sh* met Hallo de juiste pad en bestandsnaam voor Hallo-script dat u hebt gedownload, *azureuser* met Hallo gebruikersnaam voor Hallo VM en *13.69.75.209* Hallo openbare IP-adres voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="06420-165">Open a Bash prompt and type hello following, replacing *Linux_myVM_05-05-2017.sh* with hello correct path and filename for hello script that you downloaded, *azureuser* with hello username for hello VM and *13.69.75.209* with hello public IP address for your VM.</span></span>
    
    ```bash
    scp Linux_myVM_05-05-2017.sh azureuser@13.69.75.209:
    ```
    
9. <span data-ttu-id="06420-166">Open op uw lokale computer, een SSH-verbinding toohello VM.</span><span class="sxs-lookup"><span data-stu-id="06420-166">On your local computer, open an SSH connection toohello VM.</span></span>

    ```bash
    ssh 13.69.75.209
    ```
    
10. <span data-ttu-id="06420-167">Voeg op de virtuele machine, machtigingen toohello scriptbestand uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="06420-167">On your VM, add execute permissions toohello script file.</span></span>

    ```bash
    chmod +x Linux_myVM_05-05-2017.sh
    ```
    
11. <span data-ttu-id="06420-168">Op de virtuele machine, Hallo herstelpunt voor Hallo script toomount worden uitgevoerd als een bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="06420-168">On your VM, run hello script toomount hello recovery point as a filesystem.</span></span>

    ```bash
    ./Linux_myVM_05-05-2017.sh
    ```
    
12. <span data-ttu-id="06420-169">Hallo de uitvoer van Hallo script geeft dat u het pad naar het koppelpunt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="06420-169">hello output from hello script gives you hello path for hello mount point.</span></span> <span data-ttu-id="06420-170">Hallo-uitvoer ziet er vergelijkbare toothis:</span><span class="sxs-lookup"><span data-stu-id="06420-170">hello output looks similar toothis:</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
                          
    Connecting toorecovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of hello recovery point toothis machine...
                         
    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath 

    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170505191055/Volume1

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

12. <span data-ttu-id="06420-171">Op de virtuele machine, kopieert u Hallo nginx-standaardwebpagina van Hallo koppelpunt punt back toowhere u Hallo bestand verwijderd.</span><span class="sxs-lookup"><span data-stu-id="06420-171">On your VM, copy hello nginx default web page from hello mount point back toowhere you deleted hello file.</span></span>

    ```bash
    sudo cp ~/myVM-20170505191055/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```
    
17. <span data-ttu-id="06420-172">Open op uw lokale computer Hallo browsertabblad waar u bent verbonden toohello IP-adres van Hallo VM van Hallo nginx standaard de pagina.</span><span class="sxs-lookup"><span data-stu-id="06420-172">On your local computer, open hello browser tab where you are connected toohello IP address of hello VM showing hello nginx default page.</span></span> <span data-ttu-id="06420-173">Druk op CTRL + F5 toorefresh Hallo browserpagina.</span><span class="sxs-lookup"><span data-stu-id="06420-173">Press CTRL + F5 toorefresh hello browser page.</span></span> <span data-ttu-id="06420-174">U ziet nu dat Hallo standaardpagina weer werkt.</span><span class="sxs-lookup"><span data-stu-id="06420-174">You should now see that hello default page is working again.</span></span>

    ![Standaard nginx-webpagina](./media/tutorial-backup-vms/nginx-working.png)

18. <span data-ttu-id="06420-176">Op de lokale computer, gaat u terug toohello browsertabblad voor hello Azure-portal en in **stap 3: Hallo schijven ontkoppelen na het herstel** klikt u op Hallo **schijven ontkoppelen** knop.</span><span class="sxs-lookup"><span data-stu-id="06420-176">On your local computer, go back toohello browser tab for hello Azure portal and in **Step 3: Unmount hello disks after recovery** click hello **Unmount Disks** button.</span></span> <span data-ttu-id="06420-177">Als u toodo deze stap vergeet, wordt na 12 uur Hallo verbinding toohello koppelpunt automatisch sluiten.</span><span class="sxs-lookup"><span data-stu-id="06420-177">If you forget toodo this step, hello connection toohello mountpoint is automatically close after 12 hours.</span></span> <span data-ttu-id="06420-178">Na deze 12 uur moet u een nieuwe script toocreate een nieuwe koppelpunt toodownload.</span><span class="sxs-lookup"><span data-stu-id="06420-178">After those 12 hours, you need toodownload a new script toocreate a new mountpoint.</span></span>


## <a name="next-steps"></a><span data-ttu-id="06420-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="06420-179">Next steps</span></span>

<span data-ttu-id="06420-180">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="06420-180">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="06420-181">Maak een back-up van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="06420-181">Create a backup of a VM</span></span>
> * <span data-ttu-id="06420-182">Een dagelijkse back-up plannen</span><span class="sxs-lookup"><span data-stu-id="06420-182">Schedule a daily backup</span></span>
> * <span data-ttu-id="06420-183">Een bestand te herstellen vanaf een back-up</span><span class="sxs-lookup"><span data-stu-id="06420-183">Restore a file from a backup</span></span>

<span data-ttu-id="06420-184">Ga toohello volgende zelfstudie toolearn over het bewaken van virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="06420-184">Advance toohello next tutorial toolearn about monitoring virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="06420-185">Virtuele machines bewaken</span><span class="sxs-lookup"><span data-stu-id="06420-185">Monitor virtual machines</span></span>](tutorial-monitoring.md)


---
title: aaaSet van Oracle ASM op een virtuele machine van Azure Linux | Microsoft Docs
description: Snel gebruiksklaar Oracle ASM omhoog in uw Azure-omgeving.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="76ff6-103">Oracle ASM instellen op een virtuele machine van Azure Linux</span><span class="sxs-lookup"><span data-stu-id="76ff6-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="76ff6-104">Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving.</span><span class="sxs-lookup"><span data-stu-id="76ff6-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="76ff6-105">Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie in combinatie met het Hallo-installatie en configuratie van Oracle geautomatiseerde Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="76ff6-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="76ff6-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="76ff6-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="76ff6-107">Maken en koppelen tooan VM voor Oracle-Database</span><span class="sxs-lookup"><span data-stu-id="76ff6-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="76ff6-108">Installeren en configureren van Oracle automatische opslagbeheer</span><span class="sxs-lookup"><span data-stu-id="76ff6-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="76ff6-109">Installeren en configureren van Oracle raster infrastructuur</span><span class="sxs-lookup"><span data-stu-id="76ff6-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="76ff6-110">De installatie van een Oracle-ASM initialiseren</span><span class="sxs-lookup"><span data-stu-id="76ff6-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="76ff6-111">Een beheerd door ASM Oracle-database maken</span><span class="sxs-lookup"><span data-stu-id="76ff6-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="76ff6-112">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, deze zelfstudie vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="76ff6-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="76ff6-113">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="76ff6-114">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="76ff6-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="76ff6-115">Hallo-omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="76ff6-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="76ff6-116">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="76ff6-116">Create a resource group</span></span>

<span data-ttu-id="76ff6-117">een resourcegroep toocreate gebruiken Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="76ff6-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="76ff6-118">Een Azure-resourcegroep is een logische container in welke Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="76ff6-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="76ff6-119">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* regio.</span><span class="sxs-lookup"><span data-stu-id="76ff6-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="76ff6-120">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="76ff6-120">Create a VM</span></span>

<span data-ttu-id="76ff6-121">toocreate een virtuele machine op basis van de installatiekopie van de Oracle-Database Hallo en toouse Oracle ASM configureert, voert u Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="76ff6-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="76ff6-122">Hallo wordt volgende voorbeeld een virtuele machine met de naam myVM een groot Standard_DS2_v2 met vier bijgesloten gegevensschijven van 50 GB.</span><span class="sxs-lookup"><span data-stu-id="76ff6-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="76ff6-123">Als deze niet al bestaan op Hallo van sleutel standaardlocatie, maakt het ook SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="76ff6-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="76ff6-124">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="76ff6-125">Nadat u Hallo VM maakt, geeft Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="76ff6-126">Houd er rekening mee Hallo-waarde voor `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="76ff6-127">U gebruikt dit adres tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="76ff6-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="76ff6-128">Verbinding maken met toohello VM</span><span class="sxs-lookup"><span data-stu-id="76ff6-128">Connect toohello VM</span></span>

<span data-ttu-id="76ff6-129">toocreate een SSH-sessie met Hallo VM en extra instellingen configureren, gebruikt u Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="76ff6-130">Hallo IP-adres vervangen door Hallo `publicIpAddress` waarde voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="76ff6-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="76ff6-131">Oracle ASM installeren</span><span class="sxs-lookup"><span data-stu-id="76ff6-131">Install Oracle ASM</span></span>

<span data-ttu-id="76ff6-132">tooinstall Oracle ASM, volledige Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="76ff6-133">Zie voor meer informatie over het installeren van Oracle ASM [Oracle ASMLib Downloads voor Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="76ff6-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="76ff6-134">U moet toologin als hoofdgebruiker in volgorde toocontinue ASM-installatie:</span><span class="sxs-lookup"><span data-stu-id="76ff6-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="76ff6-135">Deze aanvullende opdrachten tooinstall Oracle ASM onderdelen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="76ff6-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="76ff6-136">Controleer of de Oracle-ASM is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="76ff6-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="76ff6-137">Hallo-uitvoer van deze opdracht moet lijst Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="76ff6-138">ASM vereist specifieke gebruikers en rollen in volgorde toofunction correct.</span><span class="sxs-lookup"><span data-stu-id="76ff6-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="76ff6-139">Hallo opdrachten na maken Hallo vereiste gebruikersaccounts en groepen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="76ff6-140">Controleer of de gebruikers en groepen correct zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="76ff6-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="76ff6-141">Hallo uitvoer van deze opdracht moet lijst Hallo volgende gebruikers en groepen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="76ff6-142">Maak een map voor de gebruiker *raster* en Hallo eigenaar wijzigen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="76ff6-143">Oracle ASM instellen</span><span class="sxs-lookup"><span data-stu-id="76ff6-143">Set up Oracle ASM</span></span>

<span data-ttu-id="76ff6-144">Voor deze zelfstudie Hallo standaardgebruiker is *raster* en Hallo standaardgroep is *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="76ff6-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="76ff6-145">Zorg ervoor dat Hallo *oracle* gebruiker maakt deel uit van Hallo asmadmin groep.</span><span class="sxs-lookup"><span data-stu-id="76ff6-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="76ff6-146">tooset van uw Oracle ASM-installatie voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="76ff6-147">Het instellen van Hallo Oracle ASM bibliotheek stuurprogramma Hallo standaardgebruiker (raster) en de standaardgroep (asmadmin) definiëren evenals Hallo station toostart configureren bij het opstarten is (Kies y) en tooscan voor schijven bij het opstarten (Kies y).</span><span class="sxs-lookup"><span data-stu-id="76ff6-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="76ff6-148">U moet tooanswer Hallo prompts van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="76ff6-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="76ff6-149">Hallo-uitvoer van deze opdracht moet eruitzien vergelijkbare toohello te volgen, te stoppen met prompts toobe beantwoord.</span><span class="sxs-lookup"><span data-stu-id="76ff6-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="76ff6-150">Weergaveconfiguratie Hallo schijf:</span><span class="sxs-lookup"><span data-stu-id="76ff6-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="76ff6-151">Hallo-uitvoer van deze opdracht ziet er vergelijkbare toohello volgen in de lijst met beschikbare schijven</span><span class="sxs-lookup"><span data-stu-id="76ff6-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="76ff6-152">Schijf formatteren */dev/sdc* Hallo door de volgende opdracht en het beantwoorden van Hallo prompts met:</span><span class="sxs-lookup"><span data-stu-id="76ff6-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="76ff6-153">*n*voor nieuwe partitie</span><span class="sxs-lookup"><span data-stu-id="76ff6-153">*n* for new partition</span></span>
   - <span data-ttu-id="76ff6-154">*p* voor primaire partitie</span><span class="sxs-lookup"><span data-stu-id="76ff6-154">*p* for primary partition</span></span>
   - <span data-ttu-id="76ff6-155">*1* tooselect Hallo eerste partitie</span><span class="sxs-lookup"><span data-stu-id="76ff6-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="76ff6-156">Druk op `enter` voor Hallo standaard eerste cilinder</span><span class="sxs-lookup"><span data-stu-id="76ff6-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="76ff6-157">Druk op `enter` voor Hallo standaard laatste cilinder</span><span class="sxs-lookup"><span data-stu-id="76ff6-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="76ff6-158">Druk op *w* toowrite Hallo wijzigingen toohello-partitietabel</span><span class="sxs-lookup"><span data-stu-id="76ff6-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="76ff6-159">Met de bovenstaande Hallo-antwoorden, moet Hallo uitvoer voor Hallo fdisk opdracht eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="76ff6-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="76ff6-160">Herhalingen Hallo voorafgaand aan de opdracht fdisk voor `/dev/sdd`, `/dev/sde`, en `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="76ff6-161">Controleer de schijfconfiguratie Hallo:</span><span class="sxs-lookup"><span data-stu-id="76ff6-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="76ff6-162">Hallo-uitvoer van Hallo-opdracht moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="76ff6-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="76ff6-163">Controleer de servicestatus voor Oracle ASM Hallo Hallo Oracle ASM-service en starten:</span><span class="sxs-lookup"><span data-stu-id="76ff6-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="76ff6-164">Hallo-uitvoer van Hallo-opdracht moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="76ff6-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="76ff6-165">Oracle ASM schijven maken:</span><span class="sxs-lookup"><span data-stu-id="76ff6-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="76ff6-166">Hallo-uitvoer van Hallo-opdracht moet eruitzien als Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="76ff6-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="76ff6-167">Lijst met Oracle ASM schijven:</span><span class="sxs-lookup"><span data-stu-id="76ff6-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="76ff6-168">Hallo-uitvoer van Hallo-opdracht moet lijst uitschakelen Hallo Oracle ASM schijven te volgen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="76ff6-169">Hallo wachtwoorden wijzigen voor de basis-, oracle en raster gebruikers Hallo.</span><span class="sxs-lookup"><span data-stu-id="76ff6-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="76ff6-170">**Noteer deze nieuwe wachtwoorden** als u deze later tijdens het Hallo-installatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76ff6-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="76ff6-171">Hallo map machtiging wijzigen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="76ff6-172">Download en Oracle raster infrastructuur voorbereiden</span><span class="sxs-lookup"><span data-stu-id="76ff6-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="76ff6-173">toodownload en bereid Hallo Oracle raster software voor de infrastructuur voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="76ff6-174">Oracle raster infrastructuur downloaden van Hallo [Oracle ASM-downloadpagina](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="76ff6-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="76ff6-175">Klik onder Hallo-download met de titel **Oracle-Database 12c versie 1 raster infrastructuur (12.1.0.2.0) voor Linux x86-64**, Hallo twee ZIP-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="76ff6-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="76ff6-176">Nadat u Hallo ZIP-bestanden tooyour-clientcomputer hebt gedownload, kunt u beveiligde kopie Protocol (SCP) toocopy Hallo bestanden tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="76ff6-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="76ff6-177">SSH in uw Oracle-virtuele machine in Azure in volgorde toomove Hallo ZIP-bestanden in Hallo back-map te kiezen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="76ff6-178">Wijzig Hallo-eigenaar van het Hallo-bestanden:</span><span class="sxs-lookup"><span data-stu-id="76ff6-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="76ff6-179">Hallo bestanden uitpakken.</span><span class="sxs-lookup"><span data-stu-id="76ff6-179">Unzip hello files.</span></span> <span data-ttu-id="76ff6-180">(Installatie Hallo Linux pak hulpprogramma als deze nog niet is geïnstalleerd.)</span><span class="sxs-lookup"><span data-stu-id="76ff6-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="76ff6-181">De machtiging wijzigen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="76ff6-182">Update geconfigureerd wisselruimte.</span><span class="sxs-lookup"><span data-stu-id="76ff6-182">Update configured swap space.</span></span> <span data-ttu-id="76ff6-183">Oracle raster onderdelen moeten ten minste 6,8 GB wisselen ruimte tooinstall raster.</span><span class="sxs-lookup"><span data-stu-id="76ff6-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="76ff6-184">Hallo standaard wisselbestand voor Oracle Linux afbeeldingen in Azure is alleen 2048MB.</span><span class="sxs-lookup"><span data-stu-id="76ff6-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="76ff6-185">U moet tooincrease `ResourceDisk.SwapSizeMB` in Hallo `/etc/waagent.conf` bestands- en Hallo WALinuxAgent service opnieuw starten om Hallo bijgewerkt instellingen tootake effect.</span><span class="sxs-lookup"><span data-stu-id="76ff6-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="76ff6-186">Omdat het een alleen-lezen bestand, moet u tooenable schrijftoegang voor toochange bestand machtigingen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="76ff6-187">Zoeken naar `ResourceDisk.SwapSizeMB` en Hallo waarde te wijzigen**8192**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="76ff6-188">U moet toopress `insert` tooenter invoegmodus, typt u de waarde Hallo van **8192** en druk vervolgens op `esc` tooreturn toocommand modus.</span><span class="sxs-lookup"><span data-stu-id="76ff6-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="76ff6-189">toowrite hello wijzigingen en afsluiten Hallo-bestand, typ `:wq` en druk op `enter`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="76ff6-190">We raden dat u altijd gebruiken `WALinuxAgent` tooconfigure wisselruimte zodat deze altijd op Hallo lokale kortstondige schijf (tijdelijke schijf) voor de beste prestaties gemaakt.</span><span class="sxs-lookup"><span data-stu-id="76ff6-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="76ff6-191">Zie voor meer informatie over [hoe tooadd een wisseling in Linux Azure virtuele machines bestand](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="76ff6-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="76ff6-192">Voorbereiden van uw lokale client en de VM toorun x11</span><span class="sxs-lookup"><span data-stu-id="76ff6-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="76ff6-193">Oracle ASM configureert, dient een grafische interface toocomplete Hallo installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="76ff6-194">We gebruiken Hallo x11 protocol toofacilitate deze installatie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="76ff6-195">Als u een clientsysteem (Mac of Linux) dat al X11 is mogelijkheden ingeschakeld en geconfigureerd - kunt u deze configuratie overslaan en exclusieve tooWindows machines in te stellen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="76ff6-196">[Download PuTTY](http://www.putty.org/) en [downloaden Xming](https://xming.en.softonic.com/) tooyour Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="76ff6-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="76ff6-197">U moet toocomplete Hallo installatie van beide toepassingen met de Hallo standaardwaarden voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="76ff6-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="76ff6-198">Nadat u PuTTY hebt geïnstalleerd, open een opdrachtprompt, wijzigen in Hallo PuTTY map (bijvoorbeeld C:\Program Files\PuTTY) en voer `puttygen.exe` in volgorde toogenerate een sleutel.</span><span class="sxs-lookup"><span data-stu-id="76ff6-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="76ff6-199">In de PuTTY codegenerator:</span><span class="sxs-lookup"><span data-stu-id="76ff6-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="76ff6-200">Een sleutel te genereren door het selecteren van Hallo `Generate` knop.</span><span class="sxs-lookup"><span data-stu-id="76ff6-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="76ff6-201">Kopieer de inhoud Hallo van Hallo-sleutel (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="76ff6-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="76ff6-202">Selecteer Hallo `Save private key` knop.</span><span class="sxs-lookup"><span data-stu-id="76ff6-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="76ff6-203">Hallo-waarschuwing over het beveiligen van sleutel met een wachtwoordzin Hallo negeren en selecteer vervolgens `OK`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![Schermopname van PuTTY codegenerator](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="76ff6-205">In de virtuele machine, moet u deze opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="76ff6-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="76ff6-206">Maak een bestand met de naam `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="76ff6-207">Hallo-inhoud van Hallo key plakken in dit bestand en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="76ff6-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="76ff6-208">Hallo-sleutel moet Hallo tekenreeks bevatten `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="76ff6-209">Hallo-inhoud van Hallo-sleutel moet ook een enkele regel tekst.</span><span class="sxs-lookup"><span data-stu-id="76ff6-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="76ff6-210">Start op uw clientsysteem PuTTY.</span><span class="sxs-lookup"><span data-stu-id="76ff6-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="76ff6-211">In Hallo **categorie** deelvenster te gaan**verbinding** > **SSH** > **Auth**. In Hallo **persoonlijke sleutelbestand voor verificatie** vak, blader toohello-sleutel die u eerder hebt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="76ff6-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Schermafbeelding van de opties voor Hallo SSH-verificatie](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="76ff6-213">In Hallo **categorie** deelvenster te gaan**verbinding** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="76ff6-214">Selecteer Hallo **inschakelen X11 doorsturen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="76ff6-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Schermopname van Hallo SSH X11 opties doorsturen](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="76ff6-216">In Hallo **categorie** deelvenster te gaan**sessie**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="76ff6-217">Voer uw Oracle ASM VM `<publicIPaddress>` in Hallo host naam in het dialoogvenster vult u een nieuwe `Saved Session` name op en klik vervolgens op `Save`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="76ff6-218">Wanneer opgeslagen, klik op `open` tooconnect tooyour Oracle ASM virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="76ff6-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="76ff6-219">Hallo eerste keer dat u verbinding maakt u een waarschuwing Hallo externe systeem is niet in de cache opgeslagen in het register.</span><span class="sxs-lookup"><span data-stu-id="76ff6-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="76ff6-220">Klik op `yes` tooadd deze en door te gaan.</span><span class="sxs-lookup"><span data-stu-id="76ff6-220">Click on `yes` tooadd it and continue.</span></span>

   ![Schermopname van Hallo PuTTY-sessie-opties](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="76ff6-222">Oracle raster infrastructuur installeren</span><span class="sxs-lookup"><span data-stu-id="76ff6-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="76ff6-223">tooinstall Oracle raster infrastructuur, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="76ff6-224">Meld u aan als **raster**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-224">Sign in as **grid**.</span></span> <span data-ttu-id="76ff6-225">(U moet kunnen toosign in zonder te worden gevraagd om een wachtwoord.)</span><span class="sxs-lookup"><span data-stu-id="76ff6-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="76ff6-226">Als u Windows uitvoert, zorg er dan voor dat u hebt Xming voordat u begint met Hallo installatie gestart.</span><span class="sxs-lookup"><span data-stu-id="76ff6-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="76ff6-227">Oracle raster infrastructuur 12c versie 1 installatieprogramma wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="76ff6-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="76ff6-228">(Het kan enkele minuten duren voordat Hallo installer toostart.)</span><span class="sxs-lookup"><span data-stu-id="76ff6-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="76ff6-229">Op Hallo **installatieoptie selecteren** pagina **installeren en configureren van Oracle raster infrastructuur voor een zelfstandige Server**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Schermafbeelding van pagina met Hallo-installatieprogramma installatieoptie selecteren](./media/oracle-asm/install01.png)

3. <span data-ttu-id="76ff6-231">Op Hallo **Product talen selecteren** pagina, controleert u **Engels** of Hallo taal die u wilt dat is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="76ff6-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="76ff6-232">Klik op `next`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-232">Click `next`.</span></span>

4. <span data-ttu-id="76ff6-233">Op Hallo **ASM schijfgroep maken** pagina:</span><span class="sxs-lookup"><span data-stu-id="76ff6-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="76ff6-234">Voer een naam voor de schijfgroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="76ff6-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="76ff6-235">Onder **redundantie**, selecteer **externe**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="76ff6-236">Onder **clustergrootte**, selecteer **4**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="76ff6-237">Onder **schijven toevoegen**, selecteer **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="76ff6-238">Klik op `next`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-238">Click `next`.</span></span>

5. <span data-ttu-id="76ff6-239">Op Hallo **ASM wachtwoord opgeven** pagina, selecteer Hallo **dezelfde wachtwoorden gebruiken voor deze accounts** optie en voer een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="76ff6-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Schermafbeelding van pagina met Hallo-installatieprogramma ASM wachtwoord opgeven](./media/oracle-asm/install04.png)

6. <span data-ttu-id="76ff6-241">Op Hallo **beheeropties opgeven** pagina, hebt u Hallo optie tooconfigure EM Cloud-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="76ff6-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="76ff6-242">Deze optie wordt overgeslagen: klik `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="76ff6-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="76ff6-243">Op Hallo **bevoorrechte besturingssysteem** pagina, Hallo standaardinstellingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76ff6-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="76ff6-244">Klik op `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="76ff6-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="76ff6-245">Op Hallo **installatielocatie opgeven** pagina, Hallo standaardinstellingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76ff6-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="76ff6-246">Klik op `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="76ff6-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="76ff6-247">Op Hallo **inventaris maken** pagina, Hallo inventaris Directory ook wijzigen`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="76ff6-248">Klik op `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="76ff6-248">Click `next` toocontinue.</span></span>

   ![Schermafbeelding van pagina met Hallo-installatieprogramma inventaris maken](./media/oracle-asm/install08.png)

10. <span data-ttu-id="76ff6-250">Op Hallo **hoofdmap script uitvoering configuratie** pagina, selecteer Hallo **automatisch uitgevoerd configuratiescripts** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="76ff6-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="76ff6-251">Selecteer Hallo **'root' gebruikersreferenties gebruiken** optie en geef Hallo hoofdmap gebruikerswachtwoord.</span><span class="sxs-lookup"><span data-stu-id="76ff6-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Schermafbeelding van pagina met Hallo-installatieprogramma hoofdmap script uitvoering configuratie](./media/oracle-asm/install09.png)

11. <span data-ttu-id="76ff6-253">Op Hallo **vereiste controles uitvoeren** pagina Hallo huidige mislukt de installatie met fouten.</span><span class="sxs-lookup"><span data-stu-id="76ff6-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="76ff6-254">Dit is verwacht gedrag.</span><span class="sxs-lookup"><span data-stu-id="76ff6-254">This is an expected behavior.</span></span> <span data-ttu-id="76ff6-255">Selecteer `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="76ff6-256">In Hallo **reparatie Script** in het dialoogvenster, klikt u op `OK`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="76ff6-257">Op Hallo **samenvatting** pagina, Controleer de geselecteerde instellingen en klik vervolgens op `Install`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Schermafbeelding van overzichtspagina Hallo-installatieprogramma](./media/oracle-asm/install12.png)

14. <span data-ttu-id="76ff6-259">Een waarschuwingsdialoogvenster verschijnt de melding u configuratiescripts moet toobe uitgevoerd als een bevoegde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="76ff6-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="76ff6-260">Klik op `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="76ff6-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="76ff6-261">Op Hallo **voltooien** pagina, klikt u op `Close` toofinish Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="76ff6-262">Instellen van de Oracle-ASM-installatie</span><span class="sxs-lookup"><span data-stu-id="76ff6-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="76ff6-263">tooset van uw Oracle ASM-installatie voltooid Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="76ff6-264">Zorg ervoor dat u nog steeds bent aangemeld als **raster**, van uw X11 sessie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="76ff6-265">Mogelijk moet u toohit `enter` toorevive Hallo terminal.</span><span class="sxs-lookup"><span data-stu-id="76ff6-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="76ff6-266">Start vervolgens Hallo Oracle geautomatiseerde Storage Management Configuration-assistent:</span><span class="sxs-lookup"><span data-stu-id="76ff6-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="76ff6-267">Oracle ASM configuratie-assistent wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="76ff6-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="76ff6-268">In Hallo **ASM configureren: schijfgroepen** dialoogvenster vak, klikt u op Hallo `Create` knop en klik vervolgens op `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="76ff6-269">In Hallo **schijfgroep maken** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="76ff6-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="76ff6-270">Voer Hallo schijf groepsnaam **gegevens**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="76ff6-271">Onder **lidschijven selecteren**, selecteer **ORCL_DATA** en **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="76ff6-272">Onder **clustergrootte**, selecteer **4**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="76ff6-273">Klik op `ok` toocreate Hallo schijfgroep.</span><span class="sxs-lookup"><span data-stu-id="76ff6-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="76ff6-274">Klik op `ok` tooclose Hallo bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="76ff6-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Schermopname van dialoogvenster Hallo-schijfgroep maken](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="76ff6-276">In Hallo **ASM configureren: schijfgroepen** dialoogvenster vak, klikt u op Hallo `Create` knop en klik vervolgens op `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="76ff6-277">In Hallo **schijfgroep maken** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="76ff6-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="76ff6-278">Voer Hallo schijf groepsnaam **FRA**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="76ff6-279">Onder **redundantie**, selecteer **External (geen)**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="76ff6-280">Onder **lidschijven selecteren**, selecteer **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="76ff6-281">Onder **clustergrootte**, selecteer **4**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="76ff6-282">Klik op `ok` toocreate Hallo schijfgroep.</span><span class="sxs-lookup"><span data-stu-id="76ff6-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="76ff6-283">Klik op `ok` tooclose Hallo bevestigingsvenster.</span><span class="sxs-lookup"><span data-stu-id="76ff6-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Schermopname van dialoogvenster Hallo-schijfgroep maken](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="76ff6-285">Selecteer **afsluiten** tooclose configuratie-assistent ASM.</span><span class="sxs-lookup"><span data-stu-id="76ff6-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Schermopname van Hallo ASM configureren: schijfgroepen-dialoogvenster met de knop Afsluiten](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="76ff6-287">Hallo-database maken</span><span class="sxs-lookup"><span data-stu-id="76ff6-287">Create hello database</span></span>

<span data-ttu-id="76ff6-288">Hallo software voor Oracle-database is al geïnstalleerd op de hello Azure Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="76ff6-289">toocreate een database, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="76ff6-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="76ff6-290">Schakelen gebruikers toohello Oracle supergebruiker en vervolgens initialiseren Hallo-listener voor logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="76ff6-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="76ff6-291">Configuratie-assistent database wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="76ff6-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="76ff6-292">Op Hallo **databasebewerking** pagina, klikt u op `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="76ff6-293">Op Hallo **aanmaakmodus** pagina:</span><span class="sxs-lookup"><span data-stu-id="76ff6-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="76ff6-294">Voer een naam voor de Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="76ff6-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="76ff6-295">Voor **opslagtype**, zorg ervoor dat **automatische Storage Management (ASM)** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="76ff6-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="76ff6-296">Voor **bestanden databaselocatie**, standaard-Hallo ASM voorgestelde locatie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="76ff6-297">Voor **snel herstel gebied**, standaard-Hallo ASM voorgestelde locatie.</span><span class="sxs-lookup"><span data-stu-id="76ff6-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="76ff6-298">Typ in een **beheerderswachtwoord** en **wachtwoord bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="76ff6-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="76ff6-299">Zorg ervoor dat `create as container database` is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="76ff6-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="76ff6-300">Typ in een `pluggable database name` waarde.</span><span class="sxs-lookup"><span data-stu-id="76ff6-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="76ff6-301">Op Hallo **samenvatting** pagina, Controleer de geselecteerde instellingen en klik vervolgens op `Finish` toocreate Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="76ff6-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Schermafbeelding van overzichtspagina Hallo](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="76ff6-303">Hallo Database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="76ff6-303">hello Database has been created.</span></span> <span data-ttu-id="76ff6-304">Op Hallo **voltooien** pagina, hebt u Hallo optie toounlock extra accounts toouse deze database en Hallo wachtwoorden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="76ff6-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="76ff6-305">Als u toodo doet wenst, selecteer **wachtwoordbeheer** -anders klikt u op `close`.</span><span class="sxs-lookup"><span data-stu-id="76ff6-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="76ff6-306">Hallo VM verwijderen</span><span class="sxs-lookup"><span data-stu-id="76ff6-306">Delete hello VM</span></span>

<span data-ttu-id="76ff6-307">U hebt Oracle automatisch beheer van opslag geconfigureerd op de installatiekopie van Oracle DB Hallo van hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="76ff6-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="76ff6-308">Wanneer u deze virtuele machine niet meer nodig hebt, kunt u na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="76ff6-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="76ff6-309">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76ff6-309">Next steps</span></span>

[<span data-ttu-id="76ff6-310">Zelfstudie: Oracle DataGuard configureren</span><span class="sxs-lookup"><span data-stu-id="76ff6-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="76ff6-311">Zelfstudie: Oracle GoldenGate configureren</span><span class="sxs-lookup"><span data-stu-id="76ff6-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="76ff6-312">Bekijk [bouwen van een Oracle DB](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="76ff6-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>

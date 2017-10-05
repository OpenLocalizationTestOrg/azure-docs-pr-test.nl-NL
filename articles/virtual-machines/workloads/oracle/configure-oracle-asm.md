---
title: Oracle ASM instellen op een virtuele machine van Azure Linux | Microsoft Docs
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
ms.openlocfilehash: 117212a2e7e3da7c3e249798eec804a652e0ef58
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="f2080-103">Oracle ASM instellen op een virtuele machine van Azure Linux</span><span class="sxs-lookup"><span data-stu-id="f2080-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="f2080-104">Virtuele machines van Azure bieden een volledig worden geconfigureerd en flexibele computeromgeving.</span><span class="sxs-lookup"><span data-stu-id="f2080-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="f2080-105">Deze zelfstudie bevat informatie over basic virtuele machine van Azure-implementatie in combinatie met de installatie en configuratie van Oracle geautomatiseerde Storage Management (ASM).</span><span class="sxs-lookup"><span data-stu-id="f2080-105">This tutorial covers basic Azure virtual machine deployment combined with the installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="f2080-106">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="f2080-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f2080-107">Maken en verbinding maken met een Oracle-Database VM</span><span class="sxs-lookup"><span data-stu-id="f2080-107">Create and connect to an Oracle Database VM</span></span>
> * <span data-ttu-id="f2080-108">Installeren en configureren van Oracle automatische opslagbeheer</span><span class="sxs-lookup"><span data-stu-id="f2080-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="f2080-109">Installeren en configureren van Oracle raster infrastructuur</span><span class="sxs-lookup"><span data-stu-id="f2080-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="f2080-110">De installatie van een Oracle-ASM initialiseren</span><span class="sxs-lookup"><span data-stu-id="f2080-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="f2080-111">Een beheerd door ASM Oracle-database maken</span><span class="sxs-lookup"><span data-stu-id="f2080-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f2080-112">Als u wilt installeren en gebruiken van de CLI lokaal, in deze zelfstudie vereist dat u de Azure CLI versie 2.0.4 zijn uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="f2080-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f2080-113">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="f2080-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="f2080-114">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f2080-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-the-environment"></a><span data-ttu-id="f2080-115">De omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f2080-115">Prepare the environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="f2080-116">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f2080-116">Create a resource group</span></span>

<span data-ttu-id="f2080-117">Voor het maken van een resourcegroep gebruikt de [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f2080-117">To create a resource group, use the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f2080-118">Een Azure-resourcegroep is een logische container in welke Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="f2080-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="f2080-119">In dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* in de *eastus* regio.</span><span class="sxs-lookup"><span data-stu-id="f2080-119">In this example, a resource group named *myResourceGroup* in the *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="f2080-120">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="f2080-120">Create a VM</span></span>

<span data-ttu-id="f2080-121">Voor een virtuele machine op basis van de installatiekopie van het Oracle-Database maken en configureren voor het gebruik van Oracle ASM, gebruiken de [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f2080-121">To create a virtual machine based on the Oracle Database image and configure it to use Oracle ASM, use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f2080-122">Het volgende voorbeeld wordt een virtuele machine met de naam myVM een groot Standard_DS2_v2 met vier bijgesloten gegevensschijven van 50 GB.</span><span class="sxs-lookup"><span data-stu-id="f2080-122">The following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="f2080-123">Als deze niet al bestaan op de standaardlocatie van de sleutel, maakt het ook SSH-sleutels.</span><span class="sxs-lookup"><span data-stu-id="f2080-123">If they do not already exist in the default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="f2080-124">Als u een specifieke set sleutels wilt gebruiken, gebruikt u de optie `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="f2080-124">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="f2080-125">Nadat u de virtuele machine hebt gemaakt, ziet Azure CLI er ongeveer als volgt uitzien.</span><span class="sxs-lookup"><span data-stu-id="f2080-125">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="f2080-126">Noteer de waarde voor `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="f2080-126">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="f2080-127">U kunt dit adres gebruiken voor toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f2080-127">You use this address to access the VM.</span></span>

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

### <a name="connect-to-the-vm"></a><span data-ttu-id="f2080-128">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f2080-128">Connect to the VM</span></span>

<span data-ttu-id="f2080-129">Aanvullende instellingen wilt maken van een SSH-sessie met de virtuele machine en configureren, moet u de volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f2080-129">To create an SSH session with the VM and configure additional settings, use the following command.</span></span> <span data-ttu-id="f2080-130">Vervang de IP-adres met de `publicIpAddress` waarde voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f2080-130">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="f2080-131">Oracle ASM installeren</span><span class="sxs-lookup"><span data-stu-id="f2080-131">Install Oracle ASM</span></span>

<span data-ttu-id="f2080-132">Voltooi de volgende stappen uit voor het installeren van Oracle ASM.</span><span class="sxs-lookup"><span data-stu-id="f2080-132">To install Oracle ASM, complete the following steps.</span></span> 

<span data-ttu-id="f2080-133">Zie voor meer informatie over het installeren van Oracle ASM [Oracle ASMLib Downloads voor Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="f2080-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="f2080-134">U moet zich aanmelden als basis om door te gaan met de ASM-installatie:</span><span class="sxs-lookup"><span data-stu-id="f2080-134">You need to login as root in order to continue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="f2080-135">Voer deze aanvullende opdrachten om Oracle-ASM-onderdelen te installeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-135">Run these additional commands to install Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="f2080-136">Controleer of de Oracle-ASM is geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="f2080-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="f2080-137">De uitvoer van deze opdracht moet de volgende onderdelen weergeven:</span><span class="sxs-lookup"><span data-stu-id="f2080-137">The output of this command should list the following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="f2080-138">ASM vereist zijn voor specifieke gebruikers en rollen.</span><span class="sxs-lookup"><span data-stu-id="f2080-138">ASM requires specific users and roles in order to function correctly.</span></span> <span data-ttu-id="f2080-139">De volgende opdrachten maken de vereiste gebruikersaccounts en groepen:</span><span class="sxs-lookup"><span data-stu-id="f2080-139">The following commands create the pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="f2080-140">Controleer of de gebruikers en groepen correct zijn gemaakt:</span><span class="sxs-lookup"><span data-stu-id="f2080-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="f2080-141">De uitvoer van deze opdracht moet de volgende gebruikers en groepen weergeven:</span><span class="sxs-lookup"><span data-stu-id="f2080-141">The output of this command should list the following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="f2080-142">Maak een map voor de gebruiker *raster* en wijzigt u de eigenaar:</span><span class="sxs-lookup"><span data-stu-id="f2080-142">Create a folder for user *grid* and change the owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="f2080-143">Oracle ASM instellen</span><span class="sxs-lookup"><span data-stu-id="f2080-143">Set up Oracle ASM</span></span>

<span data-ttu-id="f2080-144">Voor deze zelfstudie is het de standaardgebruiker *raster* en de standaardgroep is *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="f2080-144">For this tutorial, the default user is *grid* and the default group is *asmadmin*.</span></span> <span data-ttu-id="f2080-145">Zorg ervoor dat de *oracle* gebruiker maakt deel uit van de groep asmadmin.</span><span class="sxs-lookup"><span data-stu-id="f2080-145">Ensure that the *oracle* user is part of the asmadmin group.</span></span> <span data-ttu-id="f2080-146">Als u de installatie van de Oracle-ASM instelt, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-146">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="f2080-147">Instellen van het stuurprogramma van de bibliotheek Oracle ASM omvat het definiëren van de standaardgebruiker (raster) en de standaardgroep (asmadmin), evenals het station te starten op opstarten configureren (Kies y) en om te zoeken naar schijven op opstarten (Kies y).</span><span class="sxs-lookup"><span data-stu-id="f2080-147">Setting up the Oracle ASM library driver involves defining the default user (grid) and default group (asmadmin) as well as configuring the drive to start on boot (choose y) and to scan for disks on boot (choose y).</span></span> <span data-ttu-id="f2080-148">U moet de vragen beantwoorden van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="f2080-148">You need to answer the prompts from the following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="f2080-149">De uitvoer van deze opdracht ziet er ongeveer als volgt, stoppen met vraagt worden beantwoord.</span><span class="sxs-lookup"><span data-stu-id="f2080-149">The output of this command should look similar to the following, stopping with prompts to be answered.</span></span>

    ```bash
   Configuring the Oracle ASM library driver.

   This will configure the on-boot properties of the Oracle ASM library
   driver. The following questions will determine whether the driver is
   loaded on boot and what permissions it will have. The current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user to own the driver interface []: grid
   Default group to own the driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="f2080-150">De schijfconfiguratie weergeven:</span><span class="sxs-lookup"><span data-stu-id="f2080-150">View the disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="f2080-151">De uitvoer van deze opdracht zijn vergelijkbaar met de volgende lijst met beschikbare schijven</span><span class="sxs-lookup"><span data-stu-id="f2080-151">The output of this command should look similar to the following listing of available disks</span></span>

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

3. <span data-ttu-id="f2080-152">Schijf formatteren */dev/sdc* door de volgende opdracht uit te voeren en de prompts met beantwoorden:</span><span class="sxs-lookup"><span data-stu-id="f2080-152">Format disk */dev/sdc* by running the following command and answering the prompts with:</span></span>
   - <span data-ttu-id="f2080-153">*n*voor nieuwe partitie</span><span class="sxs-lookup"><span data-stu-id="f2080-153">*n* for new partition</span></span>
   - <span data-ttu-id="f2080-154">*p* voor primaire partitie</span><span class="sxs-lookup"><span data-stu-id="f2080-154">*p* for primary partition</span></span>
   - <span data-ttu-id="f2080-155">*1* om de eerste partitie te selecteren</span><span class="sxs-lookup"><span data-stu-id="f2080-155">*1* to select the first partition</span></span>
   - <span data-ttu-id="f2080-156">Druk op `enter` voor de eerste cilinder standaard</span><span class="sxs-lookup"><span data-stu-id="f2080-156">press `enter` for the default first cylinder</span></span>
   - <span data-ttu-id="f2080-157">Druk op `enter` voor de laatste cilinder standaard</span><span class="sxs-lookup"><span data-stu-id="f2080-157">press `enter` for the default last cylinder</span></span>
   - <span data-ttu-id="f2080-158">Druk op *w* de wijzigingen naar de partitietabel schrijven</span><span class="sxs-lookup"><span data-stu-id="f2080-158">press *w* to write the changes to the partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="f2080-159">Met behulp van de bovenstaande antwoorden, moet de uitvoer voor de opdracht fdisk eruitzien als in het volgende:</span><span class="sxs-lookup"><span data-stu-id="f2080-159">Using the answers provided above, the output for the fdisk command should look like the following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide to write them.
   After that, of course, the previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   The device presents a logical sector size that is smaller than
   the physical sector size. Aligning to a physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off the mode (command 'c') and change display units to
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
   The partition table has been altered!

   Calling ioctl() to re-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="f2080-160">Herhaal de voorgaande opdracht fdisk voor `/dev/sdd`, `/dev/sde`, en `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="f2080-160">Repeat the preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="f2080-161">Controleer de schijfconfiguratie:</span><span class="sxs-lookup"><span data-stu-id="f2080-161">Check the disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="f2080-162">De uitvoer van de opdracht moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="f2080-162">The output of the command should look like the following:</span></span>

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

6. <span data-ttu-id="f2080-163">Controleer de status van de Oracle-ASM-service en start de service Oracle ASM:</span><span class="sxs-lookup"><span data-stu-id="f2080-163">Check the Oracle ASM service status and start the Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="f2080-164">De uitvoer van de opdracht moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="f2080-164">The output of the command should look like the following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing the Oracle ASMLib driver:                     [  OK  ]
   Scanning the system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="f2080-165">Oracle ASM schijven maken:</span><span class="sxs-lookup"><span data-stu-id="f2080-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="f2080-166">De uitvoer van de opdracht moet er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="f2080-166">The output of the command should look like the following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="f2080-167">Lijst met Oracle ASM schijven:</span><span class="sxs-lookup"><span data-stu-id="f2080-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="f2080-168">De uitvoer van de opdracht moet de volgende Oracle ASM schijven uit lijst:</span><span class="sxs-lookup"><span data-stu-id="f2080-168">The output of the command should list off the following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="f2080-169">De wachtwoorden voor de basis-, oracle en raster gebruikers wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f2080-169">Change the passwords for the root, oracle, and grid users.</span></span> <span data-ttu-id="f2080-170">**Noteer deze nieuwe wachtwoorden** zoals u ze later tijdens de installatie worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2080-170">**Make note of these new passwords** as you are using them later during the installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="f2080-171">De machtiging map wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f2080-171">Change the folder permission:</span></span>

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

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="f2080-172">Download en Oracle raster infrastructuur voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f2080-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="f2080-173">Als u wilt downloaden en voorbereiden van de software Oracle raster infrastructuur, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-173">To download and prepare the Oracle Grid Infrastructure software, complete the following steps:</span></span>

1. <span data-ttu-id="f2080-174">Downloaden van Oracle raster infrastructuur niet vanuit de [Oracle ASM-downloadpagina](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="f2080-174">Download Oracle Grid Infrastructure from the [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="f2080-175">Onder het downloaden met de titel **Oracle-Database 12c versie 1 raster infrastructuur (12.1.0.2.0) voor Linux x86-64**, de twee ZIP-bestanden downloaden.</span><span class="sxs-lookup"><span data-stu-id="f2080-175">Under the download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download the two .zip files.</span></span>

2. <span data-ttu-id="f2080-176">Nadat u het ZIP-bestanden op uw clientcomputer hebt gedownload, kunt u beveiligde kopie Protocol (SCP) Kopieer de bestanden naar uw virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="f2080-176">After you download the .zip files to your client computer, you can use Secure Copy Protocol (SCP) to copy the files to your VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="f2080-177">SSH terug in uw Oracle-virtuele machine in Azure om het verplaatsen van het ZIP-bestanden in de / opt-map.</span><span class="sxs-lookup"><span data-stu-id="f2080-177">SSH back into your Oracle VM in Azure in order to move the .zip files into the /opt folder.</span></span> <span data-ttu-id="f2080-178">Wijzig de eigenaar van de bestanden:</span><span class="sxs-lookup"><span data-stu-id="f2080-178">Then, change the owner of the files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="f2080-179">Pak de bestanden.</span><span class="sxs-lookup"><span data-stu-id="f2080-179">Unzip the files.</span></span> <span data-ttu-id="f2080-180">(De Linux installeren pak hulpprogramma als deze nog niet is geïnstalleerd.)</span><span class="sxs-lookup"><span data-stu-id="f2080-180">(Install the Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="f2080-181">De machtiging wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f2080-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="f2080-182">Update geconfigureerd wisselruimte.</span><span class="sxs-lookup"><span data-stu-id="f2080-182">Update configured swap space.</span></span> <span data-ttu-id="f2080-183">Oracle raster onderdelen moeten ten minste 6,8 GB wisselruimte voor het installeren van raster.</span><span class="sxs-lookup"><span data-stu-id="f2080-183">Oracle Grid components need at least 6.8 GB of swap space to install Grid.</span></span> <span data-ttu-id="f2080-184">Standaardgrootte van het wisselbestand voor Oracle Linux afbeeldingen in Azure is alleen 2048MB.</span><span class="sxs-lookup"><span data-stu-id="f2080-184">The default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="f2080-185">U moet verhogen om `ResourceDisk.SwapSizeMB` in de `/etc/waagent.conf` -bestand en de WALinuxAgent-service opnieuw starten om de bijgewerkte instellingen kracht te laten worden.</span><span class="sxs-lookup"><span data-stu-id="f2080-185">You need to increase `ResourceDisk.SwapSizeMB` in the `/etc/waagent.conf` file and restart the WALinuxAgent service in order for the updated settings to take effect.</span></span> <span data-ttu-id="f2080-186">Omdat het een alleen-lezen bestand, die u wilt wijzigen bestandsmachtigingen om in te schakelen voor toegang voor schrijven.</span><span class="sxs-lookup"><span data-stu-id="f2080-186">Because it is a read-only file, you need to change file permissions to enable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="f2080-187">Zoeken naar `ResourceDisk.SwapSizeMB` en wijzig de waarde in **8192**.</span><span class="sxs-lookup"><span data-stu-id="f2080-187">Search for `ResourceDisk.SwapSizeMB` and change the value to **8192**.</span></span> <span data-ttu-id="f2080-188">Moet u op `insert` invoegmodus, typt u in de waarde van **8192** en druk vervolgens op `esc` om terug te keren naar de opdrachtmodus.</span><span class="sxs-lookup"><span data-stu-id="f2080-188">You will need to press `insert` to enter insert mode, type in the value of **8192** and then press `esc` to return to command mode.</span></span> <span data-ttu-id="f2080-189">Voor het schrijven van de wijzigingen en sluit het bestand, typ `:wq` en druk op `enter`.</span><span class="sxs-lookup"><span data-stu-id="f2080-189">To write the changes and quit the file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f2080-190">We raden dat u altijd gebruiken `WALinuxAgent` wisselruimte configureren zodat deze altijd wordt gemaakt op de lokale tijdelijke schijf (tijdelijke schijf) voor de beste prestaties.</span><span class="sxs-lookup"><span data-stu-id="f2080-190">We highly recommend that you always use `WALinuxAgent` to configure swap space so that it's always created on the local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="f2080-191">Zie voor meer informatie over [toevoegen van een wisselbestand in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="f2080-191">For more information on, see [How to add a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-to-run-x11"></a><span data-ttu-id="f2080-192">Voorbereiden van uw lokale client en de virtuele machine voor het uitvoeren van x11</span><span class="sxs-lookup"><span data-stu-id="f2080-192">Prepare your local client and VM to run x11</span></span>
<span data-ttu-id="f2080-193">Oracle ASM configureert, dient een grafische interface voor het voltooien van de installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="f2080-193">Configuring Oracle ASM requires a graphical interface to complete the install and configuration.</span></span> <span data-ttu-id="f2080-194">We gebruiken de x11 protocol om deze installatie.</span><span class="sxs-lookup"><span data-stu-id="f2080-194">We are using the x11 protocol to facilitate this installation.</span></span> <span data-ttu-id="f2080-195">Als u een clientsysteem (Mac of Linux) dat al X11 is mogelijkheden ingeschakeld en geconfigureerd - kunt u deze configuratie en installatie exclusieve overslaan voor Windows-computers.</span><span class="sxs-lookup"><span data-stu-id="f2080-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive to Windows machines.</span></span> 

1. <span data-ttu-id="f2080-196">[Download PuTTY](http://www.putty.org/) en [Xming downloaden](https://xming.en.softonic.com/) naar uw Windows-computer.</span><span class="sxs-lookup"><span data-stu-id="f2080-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) to your Windows computer.</span></span> <span data-ttu-id="f2080-197">U moet de installatie van beide toepassingen met de standaardwaarden voordat u doorgaat.</span><span class="sxs-lookup"><span data-stu-id="f2080-197">You will need to complete the installation of both of these applications with the default values before proceeding.</span></span>

2. <span data-ttu-id="f2080-198">Nadat u PuTTY hebt geïnstalleerd, open een opdrachtprompt, wijzigen in de PuTTY-map (bijvoorbeeld C:\Program Files\PuTTY) en voer `puttygen.exe` om een sleutel te genereren.</span><span class="sxs-lookup"><span data-stu-id="f2080-198">After you install PuTTY, open a command prompt, change into the PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order to generate a key.</span></span>

3. <span data-ttu-id="f2080-199">In de PuTTY codegenerator:</span><span class="sxs-lookup"><span data-stu-id="f2080-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="f2080-200">Een sleutel te genereren door de `Generate` knop.</span><span class="sxs-lookup"><span data-stu-id="f2080-200">Generate a key by selecting the `Generate` button.</span></span>
   2. <span data-ttu-id="f2080-201">Kopieer de inhoud van de sleutel (Ctrl + C).</span><span class="sxs-lookup"><span data-stu-id="f2080-201">Copy the contents of the key (Ctrl+C).</span></span>
   3. <span data-ttu-id="f2080-202">Selecteer de `Save private key` knop.</span><span class="sxs-lookup"><span data-stu-id="f2080-202">Select the `Save private key` button.</span></span>
   4. <span data-ttu-id="f2080-203">Negeer de waarschuwing over het beveiligen van de sleutel met een wachtwoordzin in en selecteer vervolgens `OK`.</span><span class="sxs-lookup"><span data-stu-id="f2080-203">Ignore the warning about securing the key with a passphrase, and then select `OK`.</span></span>

   ![Schermopname van PuTTY codegenerator](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="f2080-205">In de virtuele machine, moet u deze opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="f2080-206">Maak een bestand met de naam `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="f2080-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="f2080-207">Plak de inhoud van de sleutel in dit bestand en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="f2080-207">Paste the contents of the key in this file, and then save the file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f2080-208">De sleutel moet de tekenreeks bevatten `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="f2080-208">The key must contain the string `ssh-rsa`.</span></span> <span data-ttu-id="f2080-209">De inhoud van de sleutel moet ook een enkele regel tekst.</span><span class="sxs-lookup"><span data-stu-id="f2080-209">Also, the contents of the key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="f2080-210">Start op uw clientsysteem PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f2080-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="f2080-211">In de **categorie** deelvenster, gaat u naar **verbinding** > **SSH** > **Auth**.</span><span class="sxs-lookup"><span data-stu-id="f2080-211">In the **Category** pane, go to **Connection** > **SSH** > **Auth**.</span></span> <span data-ttu-id="f2080-212">In de **persoonlijke sleutelbestand voor verificatie** vak, blader naar de sleutel die u eerder hebt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f2080-212">In the **Private key file for authentication** box, browse to the key that you generated earlier.</span></span>

   ![Schermafbeelding van de opties voor SSH-verificatie](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="f2080-214">In de **categorie** deelvenster, gaat u naar **verbinding** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="f2080-214">In the **Category** pane, go to **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="f2080-215">Selecteer de **inschakelen X11 doorsturen** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="f2080-215">Select the **Enable X11 forwarding** check box.</span></span>

   ![Schermafbeelding van de SSH-X11 opties doorsturen](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="f2080-217">In de **categorie** deelvenster, gaat u naar **sessie**.</span><span class="sxs-lookup"><span data-stu-id="f2080-217">In the **Category** pane, go to **Session**.</span></span> <span data-ttu-id="f2080-218">Voer uw Oracle ASM VM `<publicIPaddress>` in het dialoogvenster host vult u een nieuwe `Saved Session` name op en klik vervolgens op `Save`.</span><span class="sxs-lookup"><span data-stu-id="f2080-218">Enter your Oracle ASM VM `<publicIPaddress>` in the host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="f2080-219">Wanneer opgeslagen, klik op `open` verbinding maken met de Oracle-ASM virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f2080-219">Once saved, click on `open` to connect to your Oracle ASM virtual machine.</span></span>  <span data-ttu-id="f2080-220">De eerste keer dat u verbinding maakt u een waarschuwing dat het externe systeem is niet in de cache opgeslagen in het register.</span><span class="sxs-lookup"><span data-stu-id="f2080-220">The first time you connect you are warned  the remote system is not cached in your registry.</span></span> <span data-ttu-id="f2080-221">Klik op `yes` toe te voegen en doorgaan.</span><span class="sxs-lookup"><span data-stu-id="f2080-221">Click on `yes` to add it and continue.</span></span>

   ![Schermafbeelding van de PuTTY-sessie-opties](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="f2080-223">Oracle raster infrastructuur installeren</span><span class="sxs-lookup"><span data-stu-id="f2080-223">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="f2080-224">Als u wilt installeren Oracle raster infrastructuur, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-224">To install Oracle Grid Infrastructure, complete the following steps:</span></span>

1. <span data-ttu-id="f2080-225">Meld u aan als **raster**.</span><span class="sxs-lookup"><span data-stu-id="f2080-225">Sign in as **grid**.</span></span> <span data-ttu-id="f2080-226">(U moet zich aanmelden zonder te worden gevraagd om een wachtwoord.)</span><span class="sxs-lookup"><span data-stu-id="f2080-226">(You should be able to sign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="f2080-227">Als u Windows uitvoert, zorg er dan voor dat u hebt Xming gestart voordat u de installatie begint.</span><span class="sxs-lookup"><span data-stu-id="f2080-227">If you are running Windows, make sure you have started Xming before you begin the installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="f2080-228">Oracle raster infrastructuur 12c versie 1 installatieprogramma wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f2080-228">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="f2080-229">(Het kan enkele minuten duren voordat het installatieprogramma starten.)</span><span class="sxs-lookup"><span data-stu-id="f2080-229">(It might take a few minutes for the  installer to start.)</span></span>

2. <span data-ttu-id="f2080-230">Op de **installatieoptie selecteren** pagina **installeren en configureren van Oracle raster infrastructuur voor een zelfstandige Server**.</span><span class="sxs-lookup"><span data-stu-id="f2080-230">On the **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Schermafbeelding van pagina met het installatieprogramma de installatie-optie selecteren](./media/oracle-asm/install01.png)

3. <span data-ttu-id="f2080-232">Op de **Product talen selecteren** pagina, controleert u **Engels** of de taal die u wilt dat is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f2080-232">On the **Select Product Languages** page, ensure **English** or the language that you want is selected.</span></span>  <span data-ttu-id="f2080-233">Klik op `next`.</span><span class="sxs-lookup"><span data-stu-id="f2080-233">Click `next`.</span></span>

4. <span data-ttu-id="f2080-234">Op de **ASM schijfgroep maken** pagina:</span><span class="sxs-lookup"><span data-stu-id="f2080-234">On the **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="f2080-235">Voer een naam voor de schijfgroep op.</span><span class="sxs-lookup"><span data-stu-id="f2080-235">Enter a name for the disk group.</span></span>
   - <span data-ttu-id="f2080-236">Onder **redundantie**, selecteer **externe**.</span><span class="sxs-lookup"><span data-stu-id="f2080-236">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="f2080-237">Onder **clustergrootte**, selecteer **4**.</span><span class="sxs-lookup"><span data-stu-id="f2080-237">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="f2080-238">Onder **schijven toevoegen**, selecteer **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="f2080-238">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="f2080-239">Klik op `next`.</span><span class="sxs-lookup"><span data-stu-id="f2080-239">Click `next`.</span></span>

5. <span data-ttu-id="f2080-240">Op de **ASM wachtwoord opgeven** pagina de **dezelfde wachtwoorden gebruiken voor deze accounts** optie en voer een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f2080-240">On the **Specify ASM Password** page, select the **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Schermafbeelding van pagina met het installatieprogramma ASM wachtwoord opgeven](./media/oracle-asm/install04.png)

6. <span data-ttu-id="f2080-242">Op de **beheeropties opgeven** pagina, hebt u de optie voor het configureren van EM Cloud-besturingselement.</span><span class="sxs-lookup"><span data-stu-id="f2080-242">On the **Specify Management Options** page, you have the option to configure EM Cloud Control.</span></span> <span data-ttu-id="f2080-243">Deze optie wordt overgeslagen: klik `next` om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="f2080-243">We are skipping this option - click `next` to continue.</span></span> 

7. <span data-ttu-id="f2080-244">Op de **bevoorrechte besturingssysteem** pagina, gebruikt u de standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="f2080-244">On the **Privileged Operating System Groups** page, use the default settings.</span></span> <span data-ttu-id="f2080-245">Klik op `next` om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="f2080-245">Click `next` to continue.</span></span>

8. <span data-ttu-id="f2080-246">Op de **installatielocatie opgeven** pagina, gebruikt u de standaardinstellingen.</span><span class="sxs-lookup"><span data-stu-id="f2080-246">On the **Specify Installation Location** page, use the default settings.</span></span> <span data-ttu-id="f2080-247">Klik op `next` om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="f2080-247">Click `next` to continue.</span></span>

9. <span data-ttu-id="f2080-248">Op de **inventaris maken** pagina, wijzig de map-inventarisatie in `/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="f2080-248">On the **Create Inventory** page, change the Inventory Directory to `/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="f2080-249">Klik op `next` om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="f2080-249">Click `next` to continue.</span></span>

   ![Schermafbeelding van pagina met het installatieprogramma inventaris maken](./media/oracle-asm/install08.png)

10. <span data-ttu-id="f2080-251">Op de **hoofdmap script uitvoering configuratie** pagina de **automatisch uitgevoerd configuratiescripts** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="f2080-251">On the **Root script execution configuration** page, select the **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="f2080-252">Selecteer de **'root' gebruikersreferenties gebruiken** optie en voer het hoofdwachtwoord van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="f2080-252">Then, select the **Use "root" user credential** option, and enter the root user password.</span></span>

    ![Schermafbeelding van de configuratiepagina voor het installatieprogramma basis-script uitvoeren](./media/oracle-asm/install09.png)

11. <span data-ttu-id="f2080-254">Op de **vereiste controles uitvoeren** pagina, de huidige installatie mislukt met fouten.</span><span class="sxs-lookup"><span data-stu-id="f2080-254">On the **Perform Prerequisite Checks** page, the current setup will fail with errors.</span></span> <span data-ttu-id="f2080-255">Dit is verwacht gedrag.</span><span class="sxs-lookup"><span data-stu-id="f2080-255">This is an expected behavior.</span></span> <span data-ttu-id="f2080-256">Selecteer `Fix & Check Again`.</span><span class="sxs-lookup"><span data-stu-id="f2080-256">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="f2080-257">In de **reparatie Script** in het dialoogvenster, klikt u op `OK`.</span><span class="sxs-lookup"><span data-stu-id="f2080-257">In the **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="f2080-258">Op de **samenvatting** pagina, Controleer de geselecteerde instellingen en klik vervolgens op `Install`.</span><span class="sxs-lookup"><span data-stu-id="f2080-258">On the **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Schermafbeelding van overzichtspagina van het installatieprogramma](./media/oracle-asm/install12.png)

14. <span data-ttu-id="f2080-260">Een waarschuwingsdialoogvenster wordt geïnformeerd u configuratie scripts moeten worden uitgevoerd als een bevoegde gebruiker weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f2080-260">A warning dialog box appears informing you configuration scripts need to be run as a privileged user.</span></span> <span data-ttu-id="f2080-261">Klik op `Yes` om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="f2080-261">Click `Yes` to continue.</span></span>

15. <span data-ttu-id="f2080-262">Op de **voltooien** pagina, klikt u op `Close` om de installatie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="f2080-262">On the **Finish** page, click `Close` to finish the installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="f2080-263">Instellen van de Oracle-ASM-installatie</span><span class="sxs-lookup"><span data-stu-id="f2080-263">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="f2080-264">Als u de installatie van de Oracle-ASM instelt, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-264">To set up your Oracle ASM installation, complete the following steps:</span></span>

1. <span data-ttu-id="f2080-265">Zorg ervoor dat u nog steeds bent aangemeld als **raster**, van uw X11 sessie.</span><span class="sxs-lookup"><span data-stu-id="f2080-265">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="f2080-266">Mogelijk moet u bereikt `enter` naar schud de terminal.</span><span class="sxs-lookup"><span data-stu-id="f2080-266">You might need to hit `enter` to revive the terminal.</span></span> <span data-ttu-id="f2080-267">Start vervolgens de Oracle geautomatiseerde Storage Management Configuration-assistent:</span><span class="sxs-lookup"><span data-stu-id="f2080-267">Then launch the Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="f2080-268">Oracle ASM configuratie-assistent wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f2080-268">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="f2080-269">In de **ASM configureren: schijfgroepen** in het dialoogvenster, klikt u op de `Create` knop en klik vervolgens op `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="f2080-269">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="f2080-270">In de **schijfgroep maken** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="f2080-270">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="f2080-271">Voer de naam van de schijf **gegevens**.</span><span class="sxs-lookup"><span data-stu-id="f2080-271">Enter the disk group name **DATA**.</span></span>
   - <span data-ttu-id="f2080-272">Onder **lidschijven selecteren**, selecteer **ORCL_DATA** en **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="f2080-272">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="f2080-273">Onder **clustergrootte**, selecteer **4**.</span><span class="sxs-lookup"><span data-stu-id="f2080-273">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="f2080-274">Klik op `ok` om de schijfgroep te maken.</span><span class="sxs-lookup"><span data-stu-id="f2080-274">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="f2080-275">Klik op `ok` om de bevestigingsvenster te sluiten.</span><span class="sxs-lookup"><span data-stu-id="f2080-275">Click `ok` to close the confirmation window.</span></span>

   ![Schermopname van het dialoogvenster schijfgroep maken](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="f2080-277">In de **ASM configureren: schijfgroepen** in het dialoogvenster, klikt u op de `Create` knop en klik vervolgens op `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="f2080-277">In the **Configure ASM: Disk Groups** dialog box, click the `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="f2080-278">In de **schijfgroep maken** in het dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="f2080-278">In the **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="f2080-279">Voer de naam van de schijf **FRA**.</span><span class="sxs-lookup"><span data-stu-id="f2080-279">Enter the disk group name **FRA**.</span></span>
   - <span data-ttu-id="f2080-280">Onder **redundantie**, selecteer **External (geen)**.</span><span class="sxs-lookup"><span data-stu-id="f2080-280">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="f2080-281">Onder **lidschijven selecteren**, selecteer **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="f2080-281">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="f2080-282">Onder **clustergrootte**, selecteer **4**.</span><span class="sxs-lookup"><span data-stu-id="f2080-282">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="f2080-283">Klik op `ok` om de schijfgroep te maken.</span><span class="sxs-lookup"><span data-stu-id="f2080-283">Click `ok` to create the disk group.</span></span>
   - <span data-ttu-id="f2080-284">Klik op `ok` om de bevestigingsvenster te sluiten.</span><span class="sxs-lookup"><span data-stu-id="f2080-284">Click `ok` to close the confirmation window.</span></span>

   ![Schermopname van het dialoogvenster schijfgroep maken](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="f2080-286">Selecteer **afsluiten** ASM configuratie-assistent sluiten.</span><span class="sxs-lookup"><span data-stu-id="f2080-286">Select **Exit** to close ASM Configuration Assistant.</span></span>

   ![Schermafbeelding van de ASM configureren: schijfgroepen-dialoogvenster met de knop Afsluiten](./media/oracle-asm/asm05.png)

## <a name="create-the-database"></a><span data-ttu-id="f2080-288">De database maken</span><span class="sxs-lookup"><span data-stu-id="f2080-288">Create the database</span></span>

<span data-ttu-id="f2080-289">De software van Oracle-database is al geïnstalleerd op de Azure Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f2080-289">The Oracle database software is already installed on the Azure Marketplace image.</span></span> <span data-ttu-id="f2080-290">Als u wilt een database maakt, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f2080-290">To create a database, complete the following steps:</span></span>

1. <span data-ttu-id="f2080-291">Gebruikers overschakelen naar de Oracle-beheerder en vervolgens de listener voor logboekregistratie te initialiseren:</span><span class="sxs-lookup"><span data-stu-id="f2080-291">Switch users to the Oracle superuser, and then initialize the listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="f2080-292">Configuratie-assistent database wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="f2080-292">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="f2080-293">Op de **databasebewerking** pagina, klikt u op `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="f2080-293">On the **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="f2080-294">Op de **aanmaakmodus** pagina:</span><span class="sxs-lookup"><span data-stu-id="f2080-294">On the **Creation Mode** page:</span></span>

   - <span data-ttu-id="f2080-295">Voer een naam voor de database.</span><span class="sxs-lookup"><span data-stu-id="f2080-295">Enter a name for the database.</span></span>
   - <span data-ttu-id="f2080-296">Voor **opslagtype**, zorg ervoor dat **automatische Storage Management (ASM)** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f2080-296">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="f2080-297">Voor **bestanden databaselocatie**, gebruikt u de standaard ASM voorgestelde locatie.</span><span class="sxs-lookup"><span data-stu-id="f2080-297">For **Database Files Location**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="f2080-298">Voor **snel herstel gebied**, gebruikt u de standaard ASM voorgestelde locatie.</span><span class="sxs-lookup"><span data-stu-id="f2080-298">For **Fast Recovery Area**, use the default ASM suggested location.</span></span>
   - <span data-ttu-id="f2080-299">Typ in een **beheerderswachtwoord** en **wachtwoord bevestigen**.</span><span class="sxs-lookup"><span data-stu-id="f2080-299">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="f2080-300">Zorg ervoor dat `create as container database` is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f2080-300">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="f2080-301">Typ in een `pluggable database name` waarde.</span><span class="sxs-lookup"><span data-stu-id="f2080-301">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="f2080-302">Op de **samenvatting** pagina, Controleer de geselecteerde instellingen en klik vervolgens op `Finish` om de database te maken.</span><span class="sxs-lookup"><span data-stu-id="f2080-302">On the **Summary** page, review your selected settings, and then click `Finish` to create the database.</span></span>

   ![Schermafbeelding van de pagina overzicht](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="f2080-304">De Database is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f2080-304">The Database has been created.</span></span> <span data-ttu-id="f2080-305">Op de **voltooien** pagina, hebt u de optie voor het ontgrendelen van extra accounts voor deze database en de wachtwoorden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f2080-305">On the **Finish** page, you have the option to unlock additional accounts to use this database and change the passwords.</span></span> <span data-ttu-id="f2080-306">Als u doen wilt, selecteert u **wachtwoordbeheer** -anders klikt u op `close`.</span><span class="sxs-lookup"><span data-stu-id="f2080-306">If you wish to do so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="f2080-307">De virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="f2080-307">Delete the VM</span></span>

<span data-ttu-id="f2080-308">U hebt Oracle automatisch beheer van opslag geconfigureerd op de installatiekopie Oracle DB vanuit Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f2080-308">You have successfully configured Oracle Automated Storage Management on the Oracle DB image from the Azure Marketplace.</span></span>  <span data-ttu-id="f2080-309">Wanneer u deze virtuele machine niet meer nodig hebt, kunt u de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="f2080-309">When you no longer need this VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f2080-310">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2080-310">Next steps</span></span>

[<span data-ttu-id="f2080-311">Zelfstudie: Oracle DataGuard configureren</span><span class="sxs-lookup"><span data-stu-id="f2080-311">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="f2080-312">Zelfstudie: Oracle GoldenGate configureren</span><span class="sxs-lookup"><span data-stu-id="f2080-312">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="f2080-313">Bekijk [bouwen van een Oracle DB](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="f2080-313">Review [Architect an Oracle DB](oracle-design.md)</span></span>

---
title: aaaBack up en herstel een Oracle-Database 12c database op een virtuele machine van Azure Linux | Microsoft Docs
description: Meer informatie over hoe tooback up en herstel een Oracle-Database 12c-database in uw Azure-omgeving.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 5/17/2017
ms.author: rclaus
ms.openlocfilehash: 68846f4efce5eabdb71cd71772e003838154e93b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="df0f6-103">Back-up en herstellen van een Oracle-Database 12c-database op een virtuele machine van Azure Linux</span><span class="sxs-lookup"><span data-stu-id="df0f6-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="df0f6-104">U kunt Azure CLI toocreate gebruiken en beheren van Azure-resources bij een opdrachtprompt of -scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df0f6-104">You can use Azure CLI toocreate and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="df0f6-105">In dit artikel gebruiken we Azure CLI scripts toodeploy een Oracle-Database 12c-database van de installatiekopie van een Azure Marketplace-galerie.</span><span class="sxs-lookup"><span data-stu-id="df0f6-105">In this article, we use Azure CLI scripts toodeploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="df0f6-106">Voordat u begint, zorg ervoor dat de Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="df0f6-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="df0f6-107">Zie voor meer informatie, Hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="df0f6-107">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="df0f6-108">Hallo-omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="df0f6-108">Prepare hello environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="df0f6-109">Stap 1: vereisten</span><span class="sxs-lookup"><span data-stu-id="df0f6-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="df0f6-110">tooperform hello back-up en herstel, moet u eerst een Linux-VM met een geïnstalleerd exemplaar van de Oracle-Database 12c maken.</span><span class="sxs-lookup"><span data-stu-id="df0f6-110">tooperform hello backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="df0f6-111">Hallo Marketplace-installatiekopie u toocreate Hallo VM heet *Oracle: Oracle-Database-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="df0f6-111">hello Marketplace image you use toocreate hello VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="df0f6-112">toolearn hoe toocreate een Oracle-database Hallo zien [Oracle database Quick Start maken](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="df0f6-112">toolearn how toocreate an Oracle database, see hello [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-toohello-vm"></a><span data-ttu-id="df0f6-113">Stap 2: Verbinding maken met toohello VM</span><span class="sxs-lookup"><span data-stu-id="df0f6-113">Step 2: Connect toohello VM</span></span>

*   <span data-ttu-id="df0f6-114">toocreate een Secure Shell (SSH)-sessie met de virtuele machine, Hallo Hallo volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df0f6-114">toocreate a Secure Shell (SSH) session with hello VM, use hello following command.</span></span> <span data-ttu-id="df0f6-115">Hallo IP-adres en hostnaam Hallo vervangen door Hallo `publicIpAddress` waarde voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="df0f6-115">Replace hello IP address and hello host name combination with hello `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a><span data-ttu-id="df0f6-116">Stap 3: Hallo database voorbereiden</span><span class="sxs-lookup"><span data-stu-id="df0f6-116">Step 3: Prepare hello database</span></span>

1.  <span data-ttu-id="df0f6-117">Deze stap wordt ervan uitgegaan dat u hebt een Oracle-exemplaar (cdb1) dat wordt uitgevoerd op een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="df0f6-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="df0f6-118">Voer Hallo *oracle* supergebruiker hoofdmap en Hallo-listener initialiseren:</span><span class="sxs-lookup"><span data-stu-id="df0f6-118">Run hello *oracle* superuser root, and then initialize hello listener:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  <span data-ttu-id="df0f6-119">(Optioneel) Zorg ervoor dat Hallo-database wordt in archief logboek modus:</span><span class="sxs-lookup"><span data-stu-id="df0f6-119">(Optional) Make sure hello database is in archive log mode:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> SELECT log_mode FROM v$database;

    LOG_MODE
    ------------
    NOARCHIVELOG

    SQL> SHUTDOWN IMMEDIATE;
    SQL> STARTUP MOUNT;
    SQL> ALTER DATABASE ARCHIVELOG;
    SQL> ALTER DATABASE OPEN;
    SQL> ALTER SYSTEM SWITCH LOGFILE;
    ```
3.  <span data-ttu-id="df0f6-120">(Optioneel) Maak een tabel tootest Hallo doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="df0f6-120">(Optional) Create a table tootest hello commit:</span></span>

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session tooscott;
    Grant succeeded.
    SQL> grant create table tooscott;
    Grant succeeded.
    SQL> alter user scott quota 100M on users;
    User altered.
    SQL> connect scott/tiger
    SQL> create table scott_table(col1 number, col2 varchar2(50));
    Table created.
    SQL> insert into scott_Table VALUES(1,'Line 1');
    1 row created.
    SQL> commit;
    Commit complete.
    ```
4.  <span data-ttu-id="df0f6-121">Controleren of Hallo back-upbestand locatie en grootte wijzigen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-121">Verify or change hello backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="df0f6-122">Oracle Recovery Manager (RMAN) tooback updatabase hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="df0f6-122">Use Oracle Recovery Manager (RMAN) tooback up hello database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="df0f6-123">Stap 4: Toepassingsconsistente back-up voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="df0f6-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="df0f6-124">Toepassingsconsistente back-ups is een nieuwe functie in Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="df0f6-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="df0f6-125">U kunt maken en scripts tooexecute selecteren voor en na Hallo VM-momentopname (voorafgaat aan momentopnamen en volgt op momentopnamen).</span><span class="sxs-lookup"><span data-stu-id="df0f6-125">You can create and select scripts tooexecute before and after hello VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="df0f6-126">Hallo JSON-bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="df0f6-126">Download hello JSON file.</span></span>

    <span data-ttu-id="df0f6-127">Download VMSnapshotScriptPluginConfig.json van https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="df0f6-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="df0f6-128">bestandsinhoud Hallo zoeken vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="df0f6-128">hello file contents look similar toohello following:</span></span>

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "",
        "postScriptLocation" : "",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

2. <span data-ttu-id="df0f6-129">Hallo /etc/azure map maken op Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="df0f6-129">Create hello /etc/azure folder on hello VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="df0f6-130">Hallo JSON-bestand kopiëren.</span><span class="sxs-lookup"><span data-stu-id="df0f6-130">Copy hello JSON file.</span></span>

    <span data-ttu-id="df0f6-131">VMSnapshotScriptPluginConfig.json toohello /etc/azure map kopiëren.</span><span class="sxs-lookup"><span data-stu-id="df0f6-131">Copy VMSnapshotScriptPluginConfig.json toohello /etc/azure folder.</span></span>

4. <span data-ttu-id="df0f6-132">Hallo JSON-bestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="df0f6-132">Edit hello JSON file.</span></span>

    <span data-ttu-id="df0f6-133">Hallo VMSnapshotScriptPluginConfig.json bestand tooinclude Hallo bewerken `PreScriptLocation` en `PostScriptlocation` parameters.</span><span class="sxs-lookup"><span data-stu-id="df0f6-133">Edit hello VMSnapshotScriptPluginConfig.json file tooinclude hello `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="df0f6-134">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="df0f6-134">For example:</span></span>

    ```azurecli
    {
        "pluginName" : "ScriptRunner",
        "preScriptLocation" : "/etc/azure/pre_script.sh",
        "postScriptLocation" : "/etc/azure/post_script.sh",
        "preScriptParams" : ["", ""],
        "postScriptParams" : ["", ""],
        "preScriptNoOfRetries" : 0,
        "postScriptNoOfRetries" : 0,
        "timeoutInSeconds" : 30,
        "continueBackupOnFailure" : true,
        "fsFreezeEnabled" : true
    }
    ```

5. <span data-ttu-id="df0f6-135">Hallo voorafgaat aan momentopnamen en volgt op momentopnamen scriptbestanden maken.</span><span class="sxs-lookup"><span data-stu-id="df0f6-135">Create hello pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="df0f6-136">Hier volgt een voorbeeld van voorafgaat aan momentopnamen en volgt op momentopnamen scripts voor een 'koude back-up' (een offline back-up, met afsluiten en opnieuw opstarten):</span><span class="sxs-lookup"><span data-stu-id="df0f6-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="df0f6-137">Voor /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="df0f6-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="df0f6-138">Voor /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="df0f6-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="df0f6-139">Hier volgt een voorbeeld van voorafgaat aan momentopnamen en volgt op momentopnamen scripts voor een 'hot back-up' (een online back-up):</span><span class="sxs-lookup"><span data-stu-id="df0f6-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="df0f6-140">Voor /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="df0f6-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="df0f6-141">Voor /etc/azure/pre_script.sql, wijzigt u Hallo inhoud van Hallo bestand per uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="df0f6-141">For /etc/azure/pre_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="df0f6-142">Voor /etc/azure/post_script.sql, wijzigt u Hallo inhoud van Hallo bestand per uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="df0f6-142">For /etc/azure/post_script.sql, modify hello contents of hello file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="df0f6-143">Machtigingen voor bestanden wijzigen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="df0f6-144">Hallo scripts testen.</span><span class="sxs-lookup"><span data-stu-id="df0f6-144">Test hello scripts.</span></span>

    <span data-ttu-id="df0f6-145">tootest hello scripts, eerst aanmelden als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="df0f6-145">tootest hello scripts, first, sign in as root.</span></span> <span data-ttu-id="df0f6-146">Vervolgens, zorg ervoor dat er geen fouten:</span><span class="sxs-lookup"><span data-stu-id="df0f6-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="df0f6-147">Zie voor meer informatie [toepassingsconsistente back-up voor virtuele Linux-machines](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="df0f6-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a><span data-ttu-id="df0f6-148">Stap 5: Gebruik Azure Recovery Services-kluizen tooback up Hallo VM</span><span class="sxs-lookup"><span data-stu-id="df0f6-148">Step 5: Use Azure Recovery Services vaults tooback up hello VM</span></span>

1.  <span data-ttu-id="df0f6-149">In Azure-portal Hallo, zoeken naar **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-149">In hello Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Pagina Recovery Services-kluizen](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="df0f6-151">Op Hallo **Recovery Services-kluizen** blade tooadd een nieuwe kluis, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-151">On hello **Recovery Services vaults** blade, tooadd a new vault, click **Add**.</span></span>

    ![Recovery Services-kluizen toevoegen pagina](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="df0f6-153">toocontinue, klikt u op **myVault**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-153">toocontinue, click **myVault**.</span></span>

    ![Recovery Services-kluizen worden in detail beschreven pagina](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="df0f6-155">Op Hallo **myVault** blade, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-155">On hello **myVault** blade, click **Backup**.</span></span>

    ![Recovery Services-kluizen back-up van de pagina](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="df0f6-157">Op Hallo **back-updoel** blade standaardwaarden gebruiken Hallo van **Azure** en **virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-157">On hello **Backup Goal** blade, use hello default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="df0f6-158">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-158">Click **OK**.</span></span>

    ![Recovery Services-kluizen worden in detail beschreven pagina](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="df0f6-160">Voor **back-up maken van beleid**, gebruik **DefaultPolicy**, of selecteer **nieuw beleid**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="df0f6-161">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-161">Click **OK**.</span></span>

    ![Recovery Services-kluizen back-up van de detailpagina beleid](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="df0f6-163">Op Hallo **virtuele machines selecteren** blade, selecteer Hallo **myVM1** selectievakje en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-163">On hello **Select virtual machines** blade, select hello **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="df0f6-164">Klik op Hallo **back-up** knop.</span><span class="sxs-lookup"><span data-stu-id="df0f6-164">Click hello **Enable backup** button.</span></span>

    ![Recovery Services-kluizen items toohello back-up detailpagina](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="df0f6-166">Nadat u op **back-up**, back-upproces Hallo start niet totdat hello geplande tijd is verstreken.</span><span class="sxs-lookup"><span data-stu-id="df0f6-166">After you click **Enable backup**, hello backup process doesn't start until hello scheduled time expires.</span></span> <span data-ttu-id="df0f6-167">tooset een direct-back-up, volledige Hallo volgende stap.</span><span class="sxs-lookup"><span data-stu-id="df0f6-167">tooset up an immediate backup, complete hello next step.</span></span>

8.  <span data-ttu-id="df0f6-168">Op Hallo **myVault - back-upitems** blade onder **back-ITEMTELLING**, aantal Hallo-back-items selecteren.</span><span class="sxs-lookup"><span data-stu-id="df0f6-168">On hello **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select hello backup item count.</span></span>

    ![Recovery Services-kluizen myVault de detailpagina](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="df0f6-170">Op Hallo **back-Upitems (Azure virtuele Machine)** blade aan de rechterkant Hallo Hallo pagina, klikt u op Hallo weglatingsteken (**...** ) en klik vervolgens op **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-170">On hello **Backup Items (Azure Virtual Machine)** blade, on hello right side of hello page, click hello ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Recovery Services-kluizen back-up nu opdracht](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="df0f6-172">Klik op Hallo **back-up** knop.</span><span class="sxs-lookup"><span data-stu-id="df0f6-172">Click hello **Backup** button.</span></span> <span data-ttu-id="df0f6-173">Wachten op Hallo back-upproces toofinish.</span><span class="sxs-lookup"><span data-stu-id="df0f6-173">Wait for hello backup process toofinish.</span></span> <span data-ttu-id="df0f6-174">Ga vervolgens te[stap 6: verwijderen van de databasebestanden Hallo](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="df0f6-174">Then, go too[Step 6: Remove hello database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="df0f6-175">tooview hello status van de back-uptaak hello, klikt u op **taken**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-175">tooview hello status of hello backup job, click **Jobs**.</span></span>

    ![Recovery Services-kluizen taak pagina](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="df0f6-177">Hallo-status van back-uptaak Hallo weergegeven in Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-177">hello status of hello backup job appears in hello following image:</span></span>

    ![Recovery Services-kluizen pagina met de status van taken](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="df0f6-179">Los eventuele fouten in het logboekbestand Hallo voor een toepassingsconsistente back-up.</span><span class="sxs-lookup"><span data-stu-id="df0f6-179">For an application-consistent backup, address any errors in hello log file.</span></span> <span data-ttu-id="df0f6-180">Hallo-logboekbestand bevindt zich op /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="df0f6-180">hello log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-hello-database-files"></a><span data-ttu-id="df0f6-181">Stap 6: Hallo databasebestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="df0f6-181">Step 6: Remove hello database files</span></span> 
<span data-ttu-id="df0f6-182">Verderop in dit artikel leert u hoe tootest Hallo herstelproces.</span><span class="sxs-lookup"><span data-stu-id="df0f6-182">Later in this article, you'll learn how tootest hello recovery process.</span></span> <span data-ttu-id="df0f6-183">Voordat u het herstelproces Hallo testen kunt, hebt u tooremove Hallo-databasebestanden.</span><span class="sxs-lookup"><span data-stu-id="df0f6-183">Before you can test hello recovery process, you have tooremove hello database files.</span></span>

1.  <span data-ttu-id="df0f6-184">Hallo tabelruimte en back-up bestanden verwijderen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-184">Remove hello tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="df0f6-185">(Optioneel) Afsluiten Hallo Oracle-exemplaar:</span><span class="sxs-lookup"><span data-stu-id="df0f6-185">(Optional) Shut down hello Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a><span data-ttu-id="df0f6-186">Hallo verwijderde bestanden terugzetten vanaf Hallo die Recovery Services-kluizen</span><span class="sxs-lookup"><span data-stu-id="df0f6-186">Restore hello deleted files from hello Recovery Services vaults</span></span>
<span data-ttu-id="df0f6-187">Hallo toorestore verwijderde bestanden, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-187">toorestore hello deleted files, complete hello following steps:</span></span>

1. <span data-ttu-id="df0f6-188">Zoek in hello Azure-portal, op Hallo *myVault* Recovery Services-kluizen item.</span><span class="sxs-lookup"><span data-stu-id="df0f6-188">In hello Azure portal, search for hello *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="df0f6-189">Op Hallo **overzicht** blade onder **back-up items**, selecteer het aantal items Hallo.</span><span class="sxs-lookup"><span data-stu-id="df0f6-189">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![Recovery Services-kluizen myVault back-items](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="df0f6-191">Onder **back-up ITEMTELLING**, selecteer het aantal items Hallo.</span><span class="sxs-lookup"><span data-stu-id="df0f6-191">Under **BACKUP ITEM COUNT**, select hello number of items.</span></span>

    ![Recovery Services-kluizen aantal voor virtuele Machine van Azure-back-items](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="df0f6-193">Op Hallo **myvm1** blade, klikt u op **Bestandsherstel (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-193">On hello **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Schermopname van Hallo Recovery Services-kluizen pagina voor herstel van bestand](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="df0f6-195">Op Hallo **Bestandsherstel (Preview)** deelvenster, klikt u op **downloadscript**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-195">On hello **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="df0f6-196">Sla hello (.sh) bestand tooa downloadmap op Hallo-clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="df0f6-196">Then, save hello download (.sh) file tooa folder on hello client computer.</span></span>

    ![Opties voor het opslaan van bestanden script downloaden](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="df0f6-198">Kopieer Hallo .sh bestand toohello VM.</span><span class="sxs-lookup"><span data-stu-id="df0f6-198">Copy hello .sh file toohello VM.</span></span>

    <span data-ttu-id="df0f6-199">Hallo volgende voorbeeld ziet u hoe u een beveiligde kopie (scp) opdracht toomove toouse Hallo bestand toohello VM.</span><span class="sxs-lookup"><span data-stu-id="df0f6-199">hello following example shows how you toouse a secure copy (scp) command toomove hello file toohello VM.</span></span> <span data-ttu-id="df0f6-200">U kunt ook Hallo inhoud toohello Klembord en plak Hallo inhoud in een nieuw bestand dat is ingesteld op Hallo VM kopiëren.</span><span class="sxs-lookup"><span data-stu-id="df0f6-200">You also can copy hello contents toohello clipboard, and then paste hello contents in a new file that is set up on hello VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="df0f6-201">Zorg ervoor dat u het IP-adres en de map waarden Hallo bijwerken in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="df0f6-201">In hello following example, ensure that you update hello IP address and folder values.</span></span> <span data-ttu-id="df0f6-202">Hallo-waarden moeten toohello map Hallo-bestand wordt opgeslagen, worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="df0f6-202">hello values must map toohello folder where hello file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="df0f6-203">Hallo-bestand wijzigen zodat deze eigendom van het Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="df0f6-203">Change hello file, so that it's owned by hello root.</span></span>

    <span data-ttu-id="df0f6-204">Wijzig in Hallo voorbeeld te volgen, Hallo-bestand zodat deze eigendom van het Hallo-hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="df0f6-204">In hello following example, change hello file so that it's owned by hello root.</span></span> <span data-ttu-id="df0f6-205">Wijzig machtigingen.</span><span class="sxs-lookup"><span data-stu-id="df0f6-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="df0f6-206">Hallo volgende voorbeeld ziet u wat u ziet na het uitvoeren van script vóór Hallo.</span><span class="sxs-lookup"><span data-stu-id="df0f6-206">hello following example shows what you should see after you run hello preceding script.</span></span> <span data-ttu-id="df0f6-207">Wanneer u wordt gevraagd toocontinue, voer **Y**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-207">When you're prompted toocontinue, enter **Y**.</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    hello script requires 'open-iscsi' and 'lshw' toorun.
    Do you want us tooinstall 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' toocontinue with installation, 'N' tooabort hello operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting toorecovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of hello recovery point toothis machine...

    ************ Volumes of hello recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer toobrowse for files. ************

    After recovery, tooremove hello disks and close hello connection toohello recovery point, please click 'Unmount Disks' in step 3 of hello portal.

    Please enter 'q/Q' tooexit...
    ```

7. <span data-ttu-id="df0f6-208">Toegang toohello gekoppelde volumes is bevestigd.</span><span class="sxs-lookup"><span data-stu-id="df0f6-208">Access toohello mounted volumes is confirmed.</span></span>

    <span data-ttu-id="df0f6-209">tooexit, voer **q**, en zoek vervolgens naar Hallo gekoppelde volumes.</span><span class="sxs-lookup"><span data-stu-id="df0f6-209">tooexit, enter **q**, and then search for hello mounted volumes.</span></span> <span data-ttu-id="df0f6-210">een lijst met Hallo toegevoegd volumes, bij een opdrachtprompt, typ toocreate **df -k**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-210">toocreate a list of hello added volumes, at a command prompt, enter **df -k**.</span></span>

    ![Hallo df -k opdracht](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="df0f6-212">Gebruik Hallo script toocopy Hallo ontbreekt na bestanden back toohello mappen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-212">Use hello following script toocopy hello missing files back toohello folders:</span></span>

    ```bash
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cp *.bkp /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # cd /u01/app/oracle/fast_recovery_area/CDB1/backupset/2017_xx_xx
    # chown oracle:oinstall *.bkp
    # cd /root/myVM-2017XXXXXXX/Volume2/u01/app/oracle/oradata/cdb1
    # cp *.dbf /u01/app/oracle/oradata/cdb1
    # cd /u01/app/oracle/oradata/cdb1
    # chown oracle:oinstall *.dbf
    ```
9. <span data-ttu-id="df0f6-213">In de Hallo script volgen, RMAN toorecover Hallo-database te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="df0f6-213">In hello following script, use RMAN toorecover hello database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="df0f6-214">Hallo schijf ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="df0f6-214">Unmount hello disk.</span></span>

    <span data-ttu-id="df0f6-215">In de Azure-portal op Hallo Hallo **Bestandsherstel (Preview)** blade, klikt u op **schijven ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-215">In hello Azure portal, on hello **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Ontkoppel de schijven opdracht](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a><span data-ttu-id="df0f6-217">Herstellen Hallo hele virtuele machine</span><span class="sxs-lookup"><span data-stu-id="df0f6-217">Restore hello entire VM</span></span>

<span data-ttu-id="df0f6-218">In plaats van Hallo verwijderde bestanden terugzetten vanaf Hallo Recovery Services-kluizen, kunt u herstellen Hallo hele virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="df0f6-218">Instead of restoring hello deleted files from hello Recovery Services vaults, you can restore hello entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="df0f6-219">Stap 1: Delete myVM</span><span class="sxs-lookup"><span data-stu-id="df0f6-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="df0f6-220">Ga in de Azure-portal hello, toohello **myVM1** -kluis en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-220">In hello Azure portal, go toohello **myVM1** vault, and then select **Delete**.</span></span>

    ![Opdracht voor kluis verwijderen](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a><span data-ttu-id="df0f6-222">Stap 2: Hallo VM herstellen</span><span class="sxs-lookup"><span data-stu-id="df0f6-222">Step 2: Recover hello VM</span></span>

1.  <span data-ttu-id="df0f6-223">Ga te**Recovery Services-kluizen**, en selecteer vervolgens **myVault**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-223">Go too**Recovery Services vaults**, and then select **myVault**.</span></span>

    ![myVault vermelding](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="df0f6-225">Op Hallo **overzicht** blade onder **back-up items**, selecteer het aantal items Hallo.</span><span class="sxs-lookup"><span data-stu-id="df0f6-225">On hello **Overview** blade, under **Backup items**, select hello number of items.</span></span>

    ![myVault back-up van items](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="df0f6-227">Op Hallo **back-Upitems (Azure virtuele Machine)** blade Selecteer **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-227">On hello **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![VM-pagina voor wachtwoordherstel](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="df0f6-229">Op Hallo **myvm1** blade, klik op Hallo weglatingsteken (**...** ) en klik vervolgens op **herstellen VM**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-229">On hello **myvm1** blade, click hello ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![VM-opdracht herstellen](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="df0f6-231">Op Hallo **herstelpunt selecteren** blade, selecteer Hallo-item dat u toorestore wilt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-231">On hello **Select restore point** blade, select hello item that you want toorestore, and then click **OK**.</span></span>

    ![Selecteer Hallo herstelpunt](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="df0f6-233">Als u toepassingsconsistente back-up hebt ingeschakeld, wordt een verticale blauwe balk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="df0f6-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="df0f6-234">Op Hallo **configuratie terugzetten** blade naam van de virtuele machine selecteert hello, selecteer Hallo resourcegroep en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-234">On hello **Restore configuration** blade, select hello virtual machine name, select hello resource group, and then click **OK**.</span></span>

    ![Configuratiewaarden herstellen](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="df0f6-236">toorestore hello VM, klikt u op Hallo **herstellen** knop.</span><span class="sxs-lookup"><span data-stu-id="df0f6-236">toorestore hello VM, click hello **Restore** button.</span></span>

8.  <span data-ttu-id="df0f6-237">tooview hello status van het herstelproces hello, klikt u op **taken**, en klik vervolgens op **back-uptaken**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-237">tooview hello status of hello restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Opdracht voor back-uptaken-status](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="df0f6-239">Hallo ziet volgende afbeelding Hallo status van het herstelproces Hallo:</span><span class="sxs-lookup"><span data-stu-id="df0f6-239">hello following figure shows hello status of hello restore process:</span></span>

    ![Status van het herstelproces Hallo](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a><span data-ttu-id="df0f6-241">Stap 3: Stel Hallo openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="df0f6-241">Step 3: Set hello public IP address</span></span>
<span data-ttu-id="df0f6-242">Nadat de Hallo die VM is hersteld, stelt u Hallo openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="df0f6-242">After hello VM is restored, set up hello public IP address.</span></span>

1.  <span data-ttu-id="df0f6-243">Voer in het zoekvak Hallo **openbaar IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-243">In hello search box, enter **public IP address**.</span></span>

    ![Lijst met openbare IP-adressen](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="df0f6-245">Op Hallo **openbare IP-adressen** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-245">On hello **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="df0f6-246">Op Hallo **openbare IP-adres maken** blade voor **naam**, selecteer Hallo openbare IP-naam.</span><span class="sxs-lookup"><span data-stu-id="df0f6-246">On hello **Create public IP address** blade, for **Name**, select hello public IP name.</span></span> <span data-ttu-id="df0f6-247">Voor **Resourcegroep** selecteert u **Bestaande gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="df0f6-248">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-248">Then, click **Create**.</span></span>

    ![IP-adres maken](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="df0f6-250">tooassociate hello openbaar IP-adres aan de netwerkinterface Hallo voor Hallo VM, zoeken voor en selecteer **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-250">tooassociate hello public IP address with hello network interface for hello VM, search for and select **myVMip**.</span></span> <span data-ttu-id="df0f6-251">Klik vervolgens op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-251">Then, click **Associate**.</span></span>

    ![IP-adres koppelen](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="df0f6-253">Voor **brontype**, selecteer **netwerkinterface**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="df0f6-254">Hallo-netwerkinterface die wordt gebruikt door Hallo myVM exemplaar selecteren en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="df0f6-254">Select hello network interface that is used by hello myVM instance, and then click **OK**.</span></span>

    ![Selecteer het brontype en NIC-waarden](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="df0f6-256">Zoek en open Hallo exemplaar van myVM die wordt overgebracht van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="df0f6-256">Search for and open hello instance of myVM that is ported from hello portal.</span></span> <span data-ttu-id="df0f6-257">Hallo IP-adres dat is gekoppeld aan VM hello wordt weergegeven op Hallo myVM **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="df0f6-257">hello IP address that is associated with hello VM appears on hello myVM **Overview** blade.</span></span>

    ![IP-adreswaarde](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a><span data-ttu-id="df0f6-259">Stap 4: Verbinding maken met toohello VM</span><span class="sxs-lookup"><span data-stu-id="df0f6-259">Step 4: Connect toohello VM</span></span>

*   <span data-ttu-id="df0f6-260">tooconnect toohello virtuele machine, gebruik Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-260">tooconnect toohello VM, use hello following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a><span data-ttu-id="df0f6-261">Stap 5: Controleren of het Hallo-database toegankelijk is</span><span class="sxs-lookup"><span data-stu-id="df0f6-261">Step 5: Test whether hello database is accessible</span></span>
*   <span data-ttu-id="df0f6-262">tootest toegankelijkheid, gebruik Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-262">tootest accessibility, use hello following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="df0f6-263">Als hello database **opstarten** opdracht genereert een fout, toorecover Hallo database, raadpleegt u [stap 6: gebruik RMAN toorecover Hallo database](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="df0f6-263">If hello database **startup** command generates an error, toorecover hello database, see [Step 6: Use RMAN toorecover hello database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a><span data-ttu-id="df0f6-264">Stap 6: (Optioneel) gebruik RMAN toorecover Hallo database</span><span class="sxs-lookup"><span data-stu-id="df0f6-264">Step 6: (Optional) Use RMAN toorecover hello database</span></span>
*   <span data-ttu-id="df0f6-265">toorecover hello database gebruik Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="df0f6-265">toorecover hello database, use hello following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="df0f6-266">Hallo back-up en herstel van Hallo Oracle-Database 12c-database op een Azure Linux VM is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="df0f6-266">hello backup and recovery of hello Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="df0f6-267">Hallo VM verwijderen</span><span class="sxs-lookup"><span data-stu-id="df0f6-267">Delete hello VM</span></span>

<span data-ttu-id="df0f6-268">Wanneer u virtuele machine niet meer nodig hello, kunt u na de opdracht tooremove Hallo-resourcegroep, Hallo VM en alle gerelateerde resources hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="df0f6-268">When you no longer need hello VM, you can use hello following command tooremove hello resource group, hello VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="df0f6-269">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df0f6-269">Next steps</span></span>

[<span data-ttu-id="df0f6-270">Zelfstudie: Een maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="df0f6-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="df0f6-271">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="df0f6-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)




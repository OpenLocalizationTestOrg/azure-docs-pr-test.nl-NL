---
title: Back-up en herstellen van een Oracle-Database 12c-database op een virtuele machine van Azure Linux | Microsoft Docs
description: Informatie over het back-up en herstellen van een Oracle-Database 12c-database in uw Azure-omgeving.
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
ms.openlocfilehash: 9a2293f13b90e9a4cb11b4169fad969dd622a9a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="252f4-103">Back-up en herstellen van een Oracle-Database 12c-database op een virtuele machine van Azure Linux</span><span class="sxs-lookup"><span data-stu-id="252f4-103">Back up and recover an Oracle Database 12c database on an Azure Linux virtual machine</span></span>

<span data-ttu-id="252f4-104">U kunt Azure CLI gebruiken om te maken en beheren van Azure-resources bij een opdrachtprompt of -scripts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="252f4-104">You can use Azure CLI to create and manage Azure resources at a command prompt, or use scripts.</span></span> <span data-ttu-id="252f4-105">In dit artikel gebruiken we Azure CLI-scripts voor het implementeren van een Oracle-Database 12c-database van de installatiekopie van een Azure Marketplace-galerie.</span><span class="sxs-lookup"><span data-stu-id="252f4-105">In this article, we use Azure CLI scripts to deploy an Oracle Database 12c database from an Azure Marketplace gallery image.</span></span>

<span data-ttu-id="252f4-106">Voordat u begint, zorg ervoor dat de Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="252f4-106">Before you begin, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="252f4-107">Zie voor meer informatie de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="252f4-107">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="252f4-108">De omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="252f4-108">Prepare the environment</span></span>

### <a name="step-1-prerequisites"></a><span data-ttu-id="252f4-109">Stap 1: vereisten</span><span class="sxs-lookup"><span data-stu-id="252f4-109">Step 1: Prerequisites</span></span>

*   <span data-ttu-id="252f4-110">Als u het proces van back-up en herstel, moet u eerst een Linux-VM met een geïnstalleerd exemplaar van de Oracle-Database 12c maken.</span><span class="sxs-lookup"><span data-stu-id="252f4-110">To perform the backup and recovery process, you must first create a Linux VM that has an installed instance of Oracle Database 12c.</span></span> <span data-ttu-id="252f4-111">De Marketplace-installatiekopie die u kunt de virtuele machine maken met de naam *Oracle: Oracle-Database-Ee:12.1.0.2:latest*.</span><span class="sxs-lookup"><span data-stu-id="252f4-111">The Marketplace image you use to create the VM is named *Oracle:Oracle-Database-Ee:12.1.0.2:latest*.</span></span>

    <span data-ttu-id="252f4-112">Zie voor meer informatie over het maken van een Oracle-database, de [Oracle database Quick Start maken](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span><span class="sxs-lookup"><span data-stu-id="252f4-112">To learn how to create an Oracle database, see the [Oracle create database quickstart](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).</span></span>


### <a name="step-2-connect-to-the-vm"></a><span data-ttu-id="252f4-113">Stap 2: Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="252f4-113">Step 2: Connect to the VM</span></span>

*   <span data-ttu-id="252f4-114">Maakt een Secure Shell (SSH)-sessie met de virtuele machine, moet u de volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="252f4-114">To create a Secure Shell (SSH) session with the VM, use the following command.</span></span> <span data-ttu-id="252f4-115">Vervang het IP-adres en de hostnaam met de `publicIpAddress` waarde voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="252f4-115">Replace the IP address and the host name combination with the `publicIpAddress` value for your VM.</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-the-database"></a><span data-ttu-id="252f4-116">Stap 3: De database voorbereiden</span><span class="sxs-lookup"><span data-stu-id="252f4-116">Step 3: Prepare the database</span></span>

1.  <span data-ttu-id="252f4-117">Deze stap wordt ervan uitgegaan dat u hebt een Oracle-exemplaar (cdb1) dat wordt uitgevoerd op een virtuele machine met de naam *myVM*.</span><span class="sxs-lookup"><span data-stu-id="252f4-117">This step assumes that you have an Oracle instance (cdb1) that is running on a VM named *myVM*.</span></span>

    <span data-ttu-id="252f4-118">Voer de *oracle* supergebruiker hoofdmap en vervolgens initialisatie van de listener:</span><span class="sxs-lookup"><span data-stu-id="252f4-118">Run the *oracle* superuser root, and then initialize the listener:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="252f4-119">(Optioneel) Zorg ervoor dat de database zich in de modus voor archive logboek:</span><span class="sxs-lookup"><span data-stu-id="252f4-119">(Optional) Make sure the database is in archive log mode:</span></span>

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
3.  <span data-ttu-id="252f4-120">(Optioneel) Maak een tabel als u wilt testen van het doorvoeren:</span><span class="sxs-lookup"><span data-stu-id="252f4-120">(Optional) Create a table to test the commit:</span></span>

    ```bash
    SQL> alter session set "_ORACLE_SCRIPT"=true ;
    Session altered.
    SQL> create user scott identified by tiger;
    User created.
    SQL> grant create session to scott;
    Grant succeeded.
    SQL> grant create table to scott;
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
4.  <span data-ttu-id="252f4-121">Controleren of de back-upbestand locatie en grootte wijzigen:</span><span class="sxs-lookup"><span data-stu-id="252f4-121">Verify or change the backup file location and size:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. <span data-ttu-id="252f4-122">Gebruik Oracle Recovery Manager (RMAN) voor back-up van de database:</span><span class="sxs-lookup"><span data-stu-id="252f4-122">Use Oracle Recovery Manager (RMAN) to back up the database:</span></span>

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a><span data-ttu-id="252f4-123">Stap 4: Toepassingsconsistente back-up voor virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="252f4-123">Step 4: Application-consistent backup for Linux VMs</span></span>

<span data-ttu-id="252f4-124">Toepassingsconsistente back-ups is een nieuwe functie in Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="252f4-124">Application-consistent backups is a new feature in Azure Backup.</span></span> <span data-ttu-id="252f4-125">U kunt maken en scripts uitvoeren voor en na de VM-momentopname (voorafgaat aan momentopnamen en volgt op momentopnamen) selecteren.</span><span class="sxs-lookup"><span data-stu-id="252f4-125">You can create and select scripts to execute before and after the VM snapshot (pre-snapshot and post-snapshot).</span></span>

1. <span data-ttu-id="252f4-126">Het JSON-bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="252f4-126">Download the JSON file.</span></span>

    <span data-ttu-id="252f4-127">Download VMSnapshotScriptPluginConfig.json van https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span><span class="sxs-lookup"><span data-stu-id="252f4-127">Download VMSnapshotScriptPluginConfig.json from https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig.</span></span> <span data-ttu-id="252f4-128">Inhoud van het bestand er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="252f4-128">The file contents look similar to the following:</span></span>

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

2. <span data-ttu-id="252f4-129">Maak de map /etc/azure op de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="252f4-129">Create the /etc/azure folder on the VM:</span></span>

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. <span data-ttu-id="252f4-130">Kopieer het JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="252f4-130">Copy the JSON file.</span></span>

    <span data-ttu-id="252f4-131">Kopieer VMSnapshotScriptPluginConfig.json naar de map /etc/azure.</span><span class="sxs-lookup"><span data-stu-id="252f4-131">Copy VMSnapshotScriptPluginConfig.json to the /etc/azure folder.</span></span>

4. <span data-ttu-id="252f4-132">Bewerk het JSON-bestand.</span><span class="sxs-lookup"><span data-stu-id="252f4-132">Edit the JSON file.</span></span>

    <span data-ttu-id="252f4-133">Bewerk het bestand VMSnapshotScriptPluginConfig.json om op te nemen de `PreScriptLocation` en `PostScriptlocation` parameters.</span><span class="sxs-lookup"><span data-stu-id="252f4-133">Edit the VMSnapshotScriptPluginConfig.json file to include the `PreScriptLocation` and `PostScriptlocation` parameters.</span></span> <span data-ttu-id="252f4-134">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="252f4-134">For example:</span></span>

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

5. <span data-ttu-id="252f4-135">Maak de voorafgaat aan momentopnamen en volgt op momentopnamen scriptbestanden.</span><span class="sxs-lookup"><span data-stu-id="252f4-135">Create the pre-snapshot and post-snapshot script files.</span></span>

    <span data-ttu-id="252f4-136">Hier volgt een voorbeeld van voorafgaat aan momentopnamen en volgt op momentopnamen scripts voor een 'koude back-up' (een offline back-up, met afsluiten en opnieuw opstarten):</span><span class="sxs-lookup"><span data-stu-id="252f4-136">Here's an example of pre-snapshot and post-snapshot scripts for a "cold backup" (an offline backup, with shutdown and restart):</span></span>

    <span data-ttu-id="252f4-137">Voor /etc/azure/pre_script.sh:</span><span class="sxs-lookup"><span data-stu-id="252f4-137">For /etc/azure/pre_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="252f4-138">Voor /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="252f4-138">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    <span data-ttu-id="252f4-139">Hier volgt een voorbeeld van voorafgaat aan momentopnamen en volgt op momentopnamen scripts voor een 'hot back-up' (een online back-up):</span><span class="sxs-lookup"><span data-stu-id="252f4-139">Here's an example of pre-snapshot and post-snapshot scripts for a "hot backup" (an online backup):</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="252f4-140">Voor /etc/azure/post_script.sh:</span><span class="sxs-lookup"><span data-stu-id="252f4-140">For /etc/azure/post_script.sh:</span></span>

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    <span data-ttu-id="252f4-141">Voor /etc/azure/pre_script.sql, wijzigt u de inhoud van het bestand per uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="252f4-141">For /etc/azure/pre_script.sql, modify the contents of the file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    <span data-ttu-id="252f4-142">Voor /etc/azure/post_script.sql, wijzigt u de inhoud van het bestand per uw vereisten:</span><span class="sxs-lookup"><span data-stu-id="252f4-142">For /etc/azure/post_script.sql, modify the contents of the file per your requirements:</span></span>

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. <span data-ttu-id="252f4-143">Machtigingen voor bestanden wijzigen:</span><span class="sxs-lookup"><span data-stu-id="252f4-143">Change file permissions:</span></span>

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. <span data-ttu-id="252f4-144">Test de scripts.</span><span class="sxs-lookup"><span data-stu-id="252f4-144">Test the scripts.</span></span>

    <span data-ttu-id="252f4-145">Als u wilt testen de scripts, eerst aanmelden als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="252f4-145">To test the scripts, first, sign in as root.</span></span> <span data-ttu-id="252f4-146">Vervolgens, zorg ervoor dat er geen fouten:</span><span class="sxs-lookup"><span data-stu-id="252f4-146">Then, ensure that there are no errors:</span></span>

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

<span data-ttu-id="252f4-147">Zie voor meer informatie [toepassingsconsistente back-up voor virtuele Linux-machines](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span><span class="sxs-lookup"><span data-stu-id="252f4-147">For more information, see [Application-consistent backup for Linux VMs](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).</span></span>


### <a name="step-5-use-azure-recovery-services-vaults-to-back-up-the-vm"></a><span data-ttu-id="252f4-148">Stap 5: Gebruik Azure Recovery Services-kluizen back-ups van de virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="252f4-148">Step 5: Use Azure Recovery Services vaults to back up the VM</span></span>

1.  <span data-ttu-id="252f4-149">Zoek in de Azure-portal op **Recovery Services-kluizen**.</span><span class="sxs-lookup"><span data-stu-id="252f4-149">In the Azure portal, search for **Recovery Services vaults**.</span></span>

    ![Pagina Recovery Services-kluizen](./media/oracle-backup-recovery/recovery_service_01.png)

2.  <span data-ttu-id="252f4-151">Op de **Recovery Services-kluizen** blade toevoegen van een nieuwe kluis, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="252f4-151">On the **Recovery Services vaults** blade, to add a new vault, click **Add**.</span></span>

    ![Recovery Services-kluizen toevoegen pagina](./media/oracle-backup-recovery/recovery_service_02.png)

3.  <span data-ttu-id="252f4-153">Als u wilt doorgaan, klikt u op **myVault**.</span><span class="sxs-lookup"><span data-stu-id="252f4-153">To continue, click **myVault**.</span></span>

    ![Recovery Services-kluizen worden in detail beschreven pagina](./media/oracle-backup-recovery/recovery_service_03.png)

4.  <span data-ttu-id="252f4-155">Op de **myVault** blade, klikt u op **back-up**.</span><span class="sxs-lookup"><span data-stu-id="252f4-155">On the **myVault** blade, click **Backup**.</span></span>

    ![Recovery Services-kluizen back-up van de pagina](./media/oracle-backup-recovery/recovery_service_04.png)

5.  <span data-ttu-id="252f4-157">Op de **back-updoel** blade, gebruikt u de standaardwaarden van **Azure** en **virtuele machine**.</span><span class="sxs-lookup"><span data-stu-id="252f4-157">On the **Backup Goal** blade, use the default values of **Azure** and **Virtual machine**.</span></span> <span data-ttu-id="252f4-158">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="252f4-158">Click **OK**.</span></span>

    ![Recovery Services-kluizen worden in detail beschreven pagina](./media/oracle-backup-recovery/recovery_service_05.png)

6.  <span data-ttu-id="252f4-160">Voor **back-up maken van beleid**, gebruik **DefaultPolicy**, of selecteer **nieuw beleid**.</span><span class="sxs-lookup"><span data-stu-id="252f4-160">For **Backup policy**, use **DefaultPolicy**, or select **Create New policy**.</span></span> <span data-ttu-id="252f4-161">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="252f4-161">Click **OK**.</span></span>

    ![Recovery Services-kluizen back-up van de detailpagina beleid](./media/oracle-backup-recovery/recovery_service_06.png)

7.  <span data-ttu-id="252f4-163">Op de **virtuele machines selecteren** blade, selecteer de **myVM1** selectievakje en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="252f4-163">On the **Select virtual machines** blade, select the **myVM1** check box, and then click **OK**.</span></span> <span data-ttu-id="252f4-164">Klik op de **back-up** knop.</span><span class="sxs-lookup"><span data-stu-id="252f4-164">Click the **Enable backup** button.</span></span>

    ![Services-kluizen herstelitems naar de back-up detailpagina](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > <span data-ttu-id="252f4-166">Nadat u op **back-up**, het back-upproces start niet totdat het geplande tijdstip is verstreken.</span><span class="sxs-lookup"><span data-stu-id="252f4-166">After you click **Enable backup**, the backup process doesn't start until the scheduled time expires.</span></span> <span data-ttu-id="252f4-167">Voer de volgende stap in te stellen van een directe back-up.</span><span class="sxs-lookup"><span data-stu-id="252f4-167">To set up an immediate backup, complete the next step.</span></span>

8.  <span data-ttu-id="252f4-168">Op de **myVault - back-upitems** blade onder **back-ITEMTELLING**, selecteert u het aantal back-items.</span><span class="sxs-lookup"><span data-stu-id="252f4-168">On the **myVault - Backup items** blade, under **BACKUP ITEM COUNT**, select the backup item count.</span></span>

    ![Recovery Services-kluizen myVault de detailpagina](./media/oracle-backup-recovery/recovery_service_08.png)

9.  <span data-ttu-id="252f4-170">Op de **back-Upitems (Azure virtuele Machine)** blade aan de rechterkant van de pagina, klikt u op het weglatingsteken (**...** ) en klik vervolgens op **back-up nu**.</span><span class="sxs-lookup"><span data-stu-id="252f4-170">On the **Backup Items (Azure Virtual Machine)** blade, on the right side of the page, click the ellipsis (**...**) button, and then click **Backup now**.</span></span>

    ![Recovery Services-kluizen back-up nu opdracht](./media/oracle-backup-recovery/recovery_service_09.png)

10. <span data-ttu-id="252f4-172">Klik op de **back-up** knop.</span><span class="sxs-lookup"><span data-stu-id="252f4-172">Click the **Backup** button.</span></span> <span data-ttu-id="252f4-173">Wacht tot de back-proces is voltooid.</span><span class="sxs-lookup"><span data-stu-id="252f4-173">Wait for the backup process to finish.</span></span> <span data-ttu-id="252f4-174">Ga vervolgens naar [stap 6: Verwijder de databasebestanden](#step-6-remove-the-database-files).</span><span class="sxs-lookup"><span data-stu-id="252f4-174">Then, go to [Step 6: Remove the database files](#step-6-remove-the-database-files).</span></span>

    <span data-ttu-id="252f4-175">Als u wilt weergeven van de status van de back-uptaak **taken**.</span><span class="sxs-lookup"><span data-stu-id="252f4-175">To view the status of the backup job, click **Jobs**.</span></span>

    ![Recovery Services-kluizen taak pagina](./media/oracle-backup-recovery/recovery_service_10.png)

    <span data-ttu-id="252f4-177">De status van de back-uptaak wordt weergegeven in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="252f4-177">The status of the backup job appears in the following image:</span></span>

    ![Recovery Services-kluizen pagina met de status van taken](./media/oracle-backup-recovery/recovery_service_11.png)

11. <span data-ttu-id="252f4-179">Los eventuele fouten in het logboekbestand voor een toepassingsconsistente back-up.</span><span class="sxs-lookup"><span data-stu-id="252f4-179">For an application-consistent backup, address any errors in the log file.</span></span> <span data-ttu-id="252f4-180">Het logboekbestand bevindt zich op /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span><span class="sxs-lookup"><span data-stu-id="252f4-180">The log file is located at /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.</span></span>

### <a name="step-6-remove-the-database-files"></a><span data-ttu-id="252f4-181">Stap 6: Verwijder de databasebestanden</span><span class="sxs-lookup"><span data-stu-id="252f4-181">Step 6: Remove the database files</span></span> 
<span data-ttu-id="252f4-182">Verderop in dit artikel leert u hoe u kunt het herstelproces te testen.</span><span class="sxs-lookup"><span data-stu-id="252f4-182">Later in this article, you'll learn how to test the recovery process.</span></span> <span data-ttu-id="252f4-183">Voordat u het herstelproces testen kunt, moet u verwijderen van bestanden van de database.</span><span class="sxs-lookup"><span data-stu-id="252f4-183">Before you can test the recovery process, you have to remove the database files.</span></span>

1.  <span data-ttu-id="252f4-184">Verwijder de bestanden tabelruimte en back-up:</span><span class="sxs-lookup"><span data-stu-id="252f4-184">Remove the tablespace and backup files:</span></span>

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  <span data-ttu-id="252f4-185">(Optioneel) Afsluiten van de Oracle-exemplaar:</span><span class="sxs-lookup"><span data-stu-id="252f4-185">(Optional) Shut down the Oracle instance:</span></span>

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-the-deleted-files-from-the-recovery-services-vaults"></a><span data-ttu-id="252f4-186">De verwijderde bestanden terugzetten vanaf de Recovery Services-kluizen</span><span class="sxs-lookup"><span data-stu-id="252f4-186">Restore the deleted files from the Recovery Services vaults</span></span>
<span data-ttu-id="252f4-187">Voor het herstellen van verwijderde bestanden, moet u de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="252f4-187">To restore the deleted files, complete the following steps:</span></span>

1. <span data-ttu-id="252f4-188">Zoek in de Azure-portal op de *myVault* Recovery Services-kluizen item.</span><span class="sxs-lookup"><span data-stu-id="252f4-188">In the Azure portal, search for the *myVault* Recovery Services vaults item.</span></span> <span data-ttu-id="252f4-189">Op de **overzicht** blade onder **back-up items**, selecteer het aantal items.</span><span class="sxs-lookup"><span data-stu-id="252f4-189">On the **Overview** blade, under **Backup items**, select the number of items.</span></span>

    ![Recovery Services-kluizen myVault back-items](./media/oracle-backup-recovery/recovery_service_12.png)

2. <span data-ttu-id="252f4-191">Onder **back-up ITEMTELLING**, selecteer het aantal items.</span><span class="sxs-lookup"><span data-stu-id="252f4-191">Under **BACKUP ITEM COUNT**, select the number of items.</span></span>

    ![Recovery Services-kluizen aantal voor virtuele Machine van Azure-back-items](./media/oracle-backup-recovery/recovery_service_13.png)

3. <span data-ttu-id="252f4-193">Op de **myvm1** blade, klikt u op **Bestandsherstel (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="252f4-193">On the **myvm1** blade, click **File Recovery (Preview)**.</span></span>

    ![Schermafbeelding van de Recovery Services-kluizen pagina voor herstel van bestand](./media/oracle-backup-recovery/recovery_service_14.png)

4. <span data-ttu-id="252f4-195">Op de **Bestandsherstel (Preview)** deelvenster, klikt u op **downloadscript**.</span><span class="sxs-lookup"><span data-stu-id="252f4-195">On the **File Recovery (Preview)** pane, click **Download Script**.</span></span> <span data-ttu-id="252f4-196">Sla het downloadbestand (.sh) naar een map op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="252f4-196">Then, save the download (.sh) file to a folder on the client computer.</span></span>

    ![Opties voor het opslaan van bestanden script downloaden](./media/oracle-backup-recovery/recovery_service_15.png)

5. <span data-ttu-id="252f4-198">Kopieer het bestand .sh naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="252f4-198">Copy the .sh file to the VM.</span></span>

    <span data-ttu-id="252f4-199">Het volgende voorbeeld ziet hoe u met een beveiligde kopie (scp) opdracht naar het bestand verplaatsen naar de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="252f4-199">The following example shows how you to use a secure copy (scp) command to move the file to the VM.</span></span> <span data-ttu-id="252f4-200">U kunt de inhoud ook kopiëren naar het Klembord en plak de inhoud in een nieuw bestand dat is ingesteld op de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="252f4-200">You also can copy the contents to the clipboard, and then paste the contents in a new file that is set up on the VM.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="252f4-201">Zorg ervoor dat u de waarden voor de IP-adres en de map bijwerken in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="252f4-201">In the following example, ensure that you update the IP address and folder values.</span></span> <span data-ttu-id="252f4-202">De waarden moeten toewijzen aan de map waarin het bestand is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="252f4-202">The values must map to the folder where the file is saved.</span></span>

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. <span data-ttu-id="252f4-203">Wijzig het bestand, zodat deze eigendom van de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="252f4-203">Change the file, so that it's owned by the root.</span></span>

    <span data-ttu-id="252f4-204">In het volgende voorbeeld wordt het bestand te wijzigen zodat deze eigendom van de hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="252f4-204">In the following example, change the file so that it's owned by the root.</span></span> <span data-ttu-id="252f4-205">Wijzig machtigingen.</span><span class="sxs-lookup"><span data-stu-id="252f4-205">Then, change permissions.</span></span>

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    <span data-ttu-id="252f4-206">Het volgende voorbeeld ziet wat u ziet nadat u hebt dit script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="252f4-206">The following example shows what you should see after you run the preceding script.</span></span> <span data-ttu-id="252f4-207">Wanneer u wordt gevraagd om door te gaan, typt u **Y**.</span><span class="sxs-lookup"><span data-stu-id="252f4-207">When you're prompted to continue, enter **Y**.</span></span>

    ```bash
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    The script requires 'open-iscsi' and 'lshw' to run.
    Do you want us to install 'open-iscsi' and 'lshw' on this machine?
    Please press 'Y' to continue with installation, 'N' to abort the operation. : Y
    Installing 'open-iscsi'....
    Installing 'lshw'....

    Connecting to recovery point using ISCSI service...

    Connection succeeded!

    Please wait while we attach volumes of the recovery point to this machine...

    ************ Volumes of the recovery point and their mount paths on this machine ************

    Sr.No.  |  Disk  |  Volume  |  MountPath

    1)  | /dev/sde  |  /dev/sde1  |  /root/myVM-20170517093913/Volume1

    2)  | /dev/sde  |  /dev/sde2  |  /root/myVM-20170517093913/Volume2

    ************ Open File Explorer to browse for files. ************

    After recovery, to remove the disks and close the connection to the recovery point, please click 'Unmount Disks' in step 3 of the portal.

    Please enter 'q/Q' to exit...
    ```

7. <span data-ttu-id="252f4-208">Toegang tot de gekoppelde volumes is bevestigd.</span><span class="sxs-lookup"><span data-stu-id="252f4-208">Access to the mounted volumes is confirmed.</span></span>

    <span data-ttu-id="252f4-209">Als u wilt afsluiten, voer **q**, en zoek vervolgens naar de gekoppelde volumes.</span><span class="sxs-lookup"><span data-stu-id="252f4-209">To exit, enter **q**, and then search for the mounted volumes.</span></span> <span data-ttu-id="252f4-210">Voer voor het maken van een lijst van de toegevoegde volumes bij een opdrachtprompt, **df -k**.</span><span class="sxs-lookup"><span data-stu-id="252f4-210">To create a list of the added volumes, at a command prompt, enter **df -k**.</span></span>

    ![De df -k-opdracht](./media/oracle-backup-recovery/recovery_service_16.png)

8. <span data-ttu-id="252f4-212">Gebruik het volgende script kopiëren van de ontbrekende bestanden terug naar de mappen:</span><span class="sxs-lookup"><span data-stu-id="252f4-212">Use the following script to copy the missing files back to the folders:</span></span>

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
9. <span data-ttu-id="252f4-213">Gebruik RMAN om de database te herstellen in het volgende script:</span><span class="sxs-lookup"><span data-stu-id="252f4-213">In the following script, use RMAN to recover the database:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. <span data-ttu-id="252f4-214">Ontkoppel de schijf.</span><span class="sxs-lookup"><span data-stu-id="252f4-214">Unmount the disk.</span></span>

    <span data-ttu-id="252f4-215">In de Azure-portal op de **Bestandsherstel (Preview)** blade, klikt u op **schijven ontkoppelen**.</span><span class="sxs-lookup"><span data-stu-id="252f4-215">In the Azure portal, on the **File Recovery (Preview)** blade, click **Unmount Disks**.</span></span>

    ![Ontkoppel de schijven opdracht](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-the-entire-vm"></a><span data-ttu-id="252f4-217">De hele virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="252f4-217">Restore the entire VM</span></span>

<span data-ttu-id="252f4-218">In plaats van de verwijderde bestanden terugzetten van de Recovery Services-kluizen, kunt u de hele virtuele machine herstellen.</span><span class="sxs-lookup"><span data-stu-id="252f4-218">Instead of restoring the deleted files from the Recovery Services vaults, you can restore the entire VM.</span></span>

### <a name="step-1-delete-myvm"></a><span data-ttu-id="252f4-219">Stap 1: Delete myVM</span><span class="sxs-lookup"><span data-stu-id="252f4-219">Step 1: Delete myVM</span></span>

*   <span data-ttu-id="252f4-220">In de Azure portal, gaat u naar de **myVM1** -kluis en selecteer vervolgens **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="252f4-220">In the Azure portal, go to the **myVM1** vault, and then select **Delete**.</span></span>

    ![Opdracht voor kluis verwijderen](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-the-vm"></a><span data-ttu-id="252f4-222">Stap 2: De virtuele machine herstellen</span><span class="sxs-lookup"><span data-stu-id="252f4-222">Step 2: Recover the VM</span></span>

1.  <span data-ttu-id="252f4-223">Ga naar **Recovery Services-kluizen**, en selecteer vervolgens **myVault**.</span><span class="sxs-lookup"><span data-stu-id="252f4-223">Go to **Recovery Services vaults**, and then select **myVault**.</span></span>

    ![myVault vermelding](./media/oracle-backup-recovery/recover_vm_02.png)

2.  <span data-ttu-id="252f4-225">Op de **overzicht** blade onder **back-up items**, selecteer het aantal items.</span><span class="sxs-lookup"><span data-stu-id="252f4-225">On the **Overview** blade, under **Backup items**, select the number of items.</span></span>

    ![myVault back-up van items](./media/oracle-backup-recovery/recover_vm_03.png)

3.  <span data-ttu-id="252f4-227">Op de **back-Upitems (Azure virtuele Machine)** blade Selecteer **myvm1**.</span><span class="sxs-lookup"><span data-stu-id="252f4-227">On the **Backup Items (Azure Virtual Machine)** blade, select **myvm1**.</span></span>

    ![VM-pagina voor wachtwoordherstel](./media/oracle-backup-recovery/recover_vm_04.png)

4.  <span data-ttu-id="252f4-229">Op de **myvm1** blade, klik op het weglatingsteken (**...** ) en klik vervolgens op **herstellen VM**.</span><span class="sxs-lookup"><span data-stu-id="252f4-229">On the **myvm1** blade, click the ellipsis (**...**) button,  and then click **Restore VM**.</span></span>

    ![VM-opdracht herstellen](./media/oracle-backup-recovery/recover_vm_05.png)

5.  <span data-ttu-id="252f4-231">Op de **herstelpunt selecteren** blade, selecteer het item dat u wilt herstellen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="252f4-231">On the **Select restore point** blade, select the item that you want to restore, and then click **OK**.</span></span>

    ![Selecteer het herstelpunt](./media/oracle-backup-recovery/recover_vm_06.png)

    <span data-ttu-id="252f4-233">Als u toepassingsconsistente back-up hebt ingeschakeld, wordt een verticale blauwe balk weergegeven.</span><span class="sxs-lookup"><span data-stu-id="252f4-233">If you have enabled application-consistent backup, a vertical blue bar appears.</span></span>

6.  <span data-ttu-id="252f4-234">Op de **configuratie terugzetten** blade, selecteert u de naam van de virtuele machine, selecteert u de resourcegroep en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="252f4-234">On the **Restore configuration** blade, select the virtual machine name, select the resource group, and then click **OK**.</span></span>

    ![Configuratiewaarden herstellen](./media/oracle-backup-recovery/recover_vm_07.png)

7.  <span data-ttu-id="252f4-236">Als u de virtuele machine herstellen, klikt u op de **herstellen** knop.</span><span class="sxs-lookup"><span data-stu-id="252f4-236">To restore the VM, click the **Restore** button.</span></span>

8.  <span data-ttu-id="252f4-237">Als u wilt weergeven van de status van het herstelproces **taken**, en klik vervolgens op **back-uptaken**.</span><span class="sxs-lookup"><span data-stu-id="252f4-237">To view the status of the restore process, click **Jobs**, and then click **Backup Jobs**.</span></span>

    ![Opdracht voor back-uptaken-status](./media/oracle-backup-recovery/recover_vm_08.png)

    <span data-ttu-id="252f4-239">De volgende afbeelding toont de status van het herstelproces:</span><span class="sxs-lookup"><span data-stu-id="252f4-239">The following figure shows the status of the restore process:</span></span>

    ![Status van het herstelproces](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-the-public-ip-address"></a><span data-ttu-id="252f4-241">Stap 3: Het openbare IP-adres instellen</span><span class="sxs-lookup"><span data-stu-id="252f4-241">Step 3: Set the public IP address</span></span>
<span data-ttu-id="252f4-242">Nadat de virtuele machine is hersteld, instellen van het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="252f4-242">After the VM is restored, set up the public IP address.</span></span>

1.  <span data-ttu-id="252f4-243">Voer in het zoekvak **openbaar IP-adres**.</span><span class="sxs-lookup"><span data-stu-id="252f4-243">In the search box, enter **public IP address**.</span></span>

    ![Lijst met openbare IP-adressen](./media/oracle-backup-recovery/create_ip_00.png)

2.  <span data-ttu-id="252f4-245">Op de **openbare IP-adressen** blade, klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="252f4-245">On the **Public IP addresses** blade, click **Add**.</span></span> <span data-ttu-id="252f4-246">Op de **openbare IP-adres maken** blade voor **naam**, selecteert u het openbare IP-naam.</span><span class="sxs-lookup"><span data-stu-id="252f4-246">On the **Create public IP address** blade, for **Name**, select the public IP name.</span></span> <span data-ttu-id="252f4-247">Voor **Resourcegroep** selecteert u **Bestaande gebruiken**.</span><span class="sxs-lookup"><span data-stu-id="252f4-247">For **Resource group**, select **Use existing**.</span></span> <span data-ttu-id="252f4-248">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="252f4-248">Then, click **Create**.</span></span>

    ![IP-adres maken](./media/oracle-backup-recovery/create_ip_01.png)

3.  <span data-ttu-id="252f4-250">Als u wilt koppelen het openbare IP-adres aan de netwerkinterface van de virtuele machine, zoek en selecteer **myVMip**.</span><span class="sxs-lookup"><span data-stu-id="252f4-250">To associate the public IP address with the network interface for the VM, search for and select **myVMip**.</span></span> <span data-ttu-id="252f4-251">Klik vervolgens op **koppelen**.</span><span class="sxs-lookup"><span data-stu-id="252f4-251">Then, click **Associate**.</span></span>

    ![IP-adres koppelen](./media/oracle-backup-recovery/create_ip_02.png)

4.  <span data-ttu-id="252f4-253">Voor **brontype**, selecteer **netwerkinterface**.</span><span class="sxs-lookup"><span data-stu-id="252f4-253">For **Resource type**, select **Network interface**.</span></span> <span data-ttu-id="252f4-254">Selecteer de netwerkinterface die wordt gebruikt door de instantie myVM en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="252f4-254">Select the network interface that is used by the myVM instance, and then click **OK**.</span></span>

    ![Selecteer het brontype en NIC-waarden](./media/oracle-backup-recovery/create_ip_03.png)

5.  <span data-ttu-id="252f4-256">Zoek en open het exemplaar van myVM die wordt overgebracht vanuit de portal.</span><span class="sxs-lookup"><span data-stu-id="252f4-256">Search for and open the instance of myVM that is ported from the portal.</span></span> <span data-ttu-id="252f4-257">Het IP-adres dat is gekoppeld aan de virtuele machine wordt weergegeven op de myVM **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="252f4-257">The IP address that is associated with the VM appears on the myVM **Overview** blade.</span></span>

    ![IP-adreswaarde](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-to-the-vm"></a><span data-ttu-id="252f4-259">Stap 4: Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="252f4-259">Step 4: Connect to the VM</span></span>

*   <span data-ttu-id="252f4-260">Voor verbinding met de virtuele machine, moet u het volgende script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="252f4-260">To connect to the VM, use the following script:</span></span>

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-the-database-is-accessible"></a><span data-ttu-id="252f4-261">Stap 5: Controleren of de database toegankelijk is</span><span class="sxs-lookup"><span data-stu-id="252f4-261">Step 5: Test whether the database is accessible</span></span>
*   <span data-ttu-id="252f4-262">Als u wilt testen toegankelijkheid, gebruikt u het volgende script:</span><span class="sxs-lookup"><span data-stu-id="252f4-262">To test accessibility, use the following script:</span></span>

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="252f4-263">Als de database **opstarten** opdracht wordt een fout gegenereerd, om de database wilt herstellen, Zie [stap 6: gebruik RMAN voor het herstellen van de database](#step-6-optional-use-rman-to-recover-the-database).</span><span class="sxs-lookup"><span data-stu-id="252f4-263">If the database **startup** command generates an error, to recover the database, see [Step 6: Use RMAN to recover the database](#step-6-optional-use-rman-to-recover-the-database).</span></span>

### <a name="step-6-optional-use-rman-to-recover-the-database"></a><span data-ttu-id="252f4-264">Stap 6: (Optioneel) gebruik RMAN de database herstellen</span><span class="sxs-lookup"><span data-stu-id="252f4-264">Step 6: (Optional) Use RMAN to recover the database</span></span>
*   <span data-ttu-id="252f4-265">Voor de database, gebruikt u het volgende script:</span><span class="sxs-lookup"><span data-stu-id="252f4-265">To recover the database, use the following script:</span></span>

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

<span data-ttu-id="252f4-266">De back-up en herstel van de Oracle-Database 12c-database op een Azure Linux VM is nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="252f4-266">The backup and recovery of the Oracle Database 12c database on an Azure Linux VM is now finished.</span></span>

## <a name="delete-the-vm"></a><span data-ttu-id="252f4-267">De virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="252f4-267">Delete the VM</span></span>

<span data-ttu-id="252f4-268">Wanneer u de virtuele machine niet meer nodig hebt, kunt u de volgende opdracht om de resourcegroep, de virtuele machine en alle gerelateerde resources te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="252f4-268">When you no longer need the VM, you can use the following command to remove the resource group, the VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="252f4-269">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="252f4-269">Next steps</span></span>

[<span data-ttu-id="252f4-270">Zelfstudie: Een maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="252f4-270">Tutorial: Create highly available VMs</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="252f4-271">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="252f4-271">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)




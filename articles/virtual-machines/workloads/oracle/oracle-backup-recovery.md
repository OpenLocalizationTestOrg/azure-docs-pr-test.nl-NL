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
# <a name="back-up-and-recover-an-oracle-database-12c-database-on-an-azure-linux-virtual-machine"></a>Back-up en herstellen van een Oracle-Database 12c-database op een virtuele machine van Azure Linux

U kunt Azure CLI toocreate gebruiken en beheren van Azure-resources bij een opdrachtprompt of -scripts gebruiken. In dit artikel gebruiken we Azure CLI scripts toodeploy een Oracle-Database 12c-database van de installatiekopie van een Azure Marketplace-galerie.

Voordat u begint, zorg ervoor dat de Azure CLI is geïnstalleerd. Zie voor meer informatie, Hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Hallo-omgeving voorbereiden

### <a name="step-1-prerequisites"></a>Stap 1: vereisten

*   tooperform hello back-up en herstel, moet u eerst een Linux-VM met een geïnstalleerd exemplaar van de Oracle-Database 12c maken. Hallo Marketplace-installatiekopie u toocreate Hallo VM heet *Oracle: Oracle-Database-Ee:12.1.0.2:latest*.

    toolearn hoe toocreate een Oracle-database Hallo zien [Oracle database Quick Start maken](https://docs.microsoft.com/azure/virtual-machines/workloads/oracle/oracle-database-quick-create).


### <a name="step-2-connect-toohello-vm"></a>Stap 2: Verbinding maken met toohello VM

*   toocreate een Secure Shell (SSH)-sessie met de virtuele machine, Hallo Hallo volgende opdracht gebruiken. Hallo IP-adres en hostnaam Hallo vervangen door Hallo `publicIpAddress` waarde voor uw virtuele machine.

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-3-prepare-hello-database"></a>Stap 3: Hallo database voorbereiden

1.  Deze stap wordt ervan uitgegaan dat u hebt een Oracle-exemplaar (cdb1) dat wordt uitgevoerd op een virtuele machine met de naam *myVM*.

    Voer Hallo *oracle* supergebruiker hoofdmap en Hallo-listener initialiseren:

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

2.  (Optioneel) Zorg ervoor dat Hallo-database wordt in archief logboek modus:

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
3.  (Optioneel) Maak een tabel tootest Hallo doorvoeren:

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
4.  Controleren of Hallo back-upbestand locatie en grootte wijzigen:

    ```bash
    $ sqlplus / as sysdba
    SQL> show parameter db_recovery
    NAME                                 TYPE        VALUE
    ------------------------------------ ----------- ------------------------------
    db_recovery_file_dest                string      /u01/app/oracle/fast_recovery_area
    db_recovery_file_dest_size           big integer 4560M
    ```
5. Oracle Recovery Manager (RMAN) tooback updatabase hello gebruiken:

    ```bash
    $ rman target /
    RMAN> backup database plus archivelog;
    ```

### <a name="step-4-application-consistent-backup-for-linux-vms"></a>Stap 4: Toepassingsconsistente back-up voor virtuele Linux-machines

Toepassingsconsistente back-ups is een nieuwe functie in Azure Backup. U kunt maken en scripts tooexecute selecteren voor en na Hallo VM-momentopname (voorafgaat aan momentopnamen en volgt op momentopnamen).

1. Hallo JSON-bestand downloaden.

    Download VMSnapshotScriptPluginConfig.json van https://github.com/MicrosoftAzureBackup/VMSnapshotPluginConfig. bestandsinhoud Hallo zoeken vergelijkbare toohello volgende:

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

2. Hallo /etc/azure map maken op Hallo VM:

    ```bash
    $ sudo su -
    # mkdir /etc/azure
    # cd /etc/azure
    ```

3. Hallo JSON-bestand kopiëren.

    VMSnapshotScriptPluginConfig.json toohello /etc/azure map kopiëren.

4. Hallo JSON-bestand bewerken.

    Hallo VMSnapshotScriptPluginConfig.json bestand tooinclude Hallo bewerken `PreScriptLocation` en `PostScriptlocation` parameters. Bijvoorbeeld:

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

5. Hallo voorafgaat aan momentopnamen en volgt op momentopnamen scriptbestanden maken.

    Hier volgt een voorbeeld van voorafgaat aan momentopnamen en volgt op momentopnamen scripts voor een 'koude back-up' (een offline back-up, met afsluiten en opnieuw opstarten):

    Voor /etc/azure/pre_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" > /etc/azure/pre_script_$v_date.log
    ```

    Voor /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" > /etc/azure/post_script_$v_date.log
    ```

    Hier volgt een voorbeeld van voorafgaat aan momentopnamen en volgt op momentopnamen scripts voor een 'hot back-up' (een online back-up):

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/pre_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Voor /etc/azure/post_script.sh:

    ```bash
    v_date=`date +%Y%m%d%H%M`
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle
    su - $ORA_OWNER -c "sqlplus / as sysdba @/etc/azure/post_script.sql" > /etc/azure/pre_script_$v_date.log
    ```

    Voor /etc/azure/pre_script.sql, wijzigt u Hallo inhoud van Hallo bestand per uw vereisten:

    ```bash
    alter tablespace SYSTEM begin backup;
    ...
    ...
    alter system switch logfile;
    alter system archive log stop;
    ```

    Voor /etc/azure/post_script.sql, wijzigt u Hallo inhoud van Hallo bestand per uw vereisten:

    ```bash
    alter tablespace SYSTEM end backup;
    ...
    ...
    alter system archive log start;
    ```

6. Machtigingen voor bestanden wijzigen:

    ```bash
    # chmod 600 /etc/azure/VMSnapshotScriptPluginConfig.json
    # chmod 700 /etc/azure/pre_script.sh
    # chmod 700 /etc/azure/post_script.sh
    ```

7. Hallo scripts testen.

    tootest hello scripts, eerst aanmelden als hoofdmap. Vervolgens, zorg ervoor dat er geen fouten:

    ```bash
    # /etc/azure/pre_script.sh
    # /etc/azure/post_script.sh
    ```

Zie voor meer informatie [toepassingsconsistente back-up voor virtuele Linux-machines](https://azure.microsoft.com/en-us/blog/announcing-application-consistent-backup-for-linux-vms-using-azure-backup/).


### <a name="step-5-use-azure-recovery-services-vaults-tooback-up-hello-vm"></a>Stap 5: Gebruik Azure Recovery Services-kluizen tooback up Hallo VM

1.  In Azure-portal Hallo, zoeken naar **Recovery Services-kluizen**.

    ![Pagina Recovery Services-kluizen](./media/oracle-backup-recovery/recovery_service_01.png)

2.  Op Hallo **Recovery Services-kluizen** blade tooadd een nieuwe kluis, klikt u op **toevoegen**.

    ![Recovery Services-kluizen toevoegen pagina](./media/oracle-backup-recovery/recovery_service_02.png)

3.  toocontinue, klikt u op **myVault**.

    ![Recovery Services-kluizen worden in detail beschreven pagina](./media/oracle-backup-recovery/recovery_service_03.png)

4.  Op Hallo **myVault** blade, klikt u op **back-up**.

    ![Recovery Services-kluizen back-up van de pagina](./media/oracle-backup-recovery/recovery_service_04.png)

5.  Op Hallo **back-updoel** blade standaardwaarden gebruiken Hallo van **Azure** en **virtuele machine**. Klik op **OK**.

    ![Recovery Services-kluizen worden in detail beschreven pagina](./media/oracle-backup-recovery/recovery_service_05.png)

6.  Voor **back-up maken van beleid**, gebruik **DefaultPolicy**, of selecteer **nieuw beleid**. Klik op **OK**.

    ![Recovery Services-kluizen back-up van de detailpagina beleid](./media/oracle-backup-recovery/recovery_service_06.png)

7.  Op Hallo **virtuele machines selecteren** blade, selecteer Hallo **myVM1** selectievakje en klik vervolgens op **OK**. Klik op Hallo **back-up** knop.

    ![Recovery Services-kluizen items toohello back-up detailpagina](./media/oracle-backup-recovery/recovery_service_07.png)

    > [!IMPORTANT]
    > Nadat u op **back-up**, back-upproces Hallo start niet totdat hello geplande tijd is verstreken. tooset een direct-back-up, volledige Hallo volgende stap.

8.  Op Hallo **myVault - back-upitems** blade onder **back-ITEMTELLING**, aantal Hallo-back-items selecteren.

    ![Recovery Services-kluizen myVault de detailpagina](./media/oracle-backup-recovery/recovery_service_08.png)

9.  Op Hallo **back-Upitems (Azure virtuele Machine)** blade aan de rechterkant Hallo Hallo pagina, klikt u op Hallo weglatingsteken (**...** ) en klik vervolgens op **back-up nu**.

    ![Recovery Services-kluizen back-up nu opdracht](./media/oracle-backup-recovery/recovery_service_09.png)

10. Klik op Hallo **back-up** knop. Wachten op Hallo back-upproces toofinish. Ga vervolgens te[stap 6: verwijderen van de databasebestanden Hallo](#step-6-remove-the-database-files).

    tooview hello status van de back-uptaak hello, klikt u op **taken**.

    ![Recovery Services-kluizen taak pagina](./media/oracle-backup-recovery/recovery_service_10.png)

    Hallo-status van back-uptaak Hallo weergegeven in Hallo installatiekopie te volgen:

    ![Recovery Services-kluizen pagina met de status van taken](./media/oracle-backup-recovery/recovery_service_11.png)

11. Los eventuele fouten in het logboekbestand Hallo voor een toepassingsconsistente back-up. Hallo-logboekbestand bevindt zich op /var/log/azure/Microsoft.Azure.RecoveryServices.VMSnapshotLinux/1.0.9114.0.

### <a name="step-6-remove-hello-database-files"></a>Stap 6: Hallo databasebestanden verwijderen 
Verderop in dit artikel leert u hoe tootest Hallo herstelproces. Voordat u het herstelproces Hallo testen kunt, hebt u tooremove Hallo-databasebestanden.

1.  Hallo tabelruimte en back-up bestanden verwijderen:

    ```bash
    $ sudo su - oracle
    $ cd /u01/app/oracle/oradata/cdb1
    $ rm -f *.dbf
    $ cd /u01/app/oracle/fast_recovery_area/CDB1/backupset
    $ rm -rf *
    ```
    
2.  (Optioneel) Afsluiten Hallo Oracle-exemplaar:

    ```bash
    $ sqlplus / as sysdba
    SQL> shutdown abort
    ORACLE instance shut down.
    ```

## <a name="restore-hello-deleted-files-from-hello-recovery-services-vaults"></a>Hallo verwijderde bestanden terugzetten vanaf Hallo die Recovery Services-kluizen
Hallo toorestore verwijderde bestanden, volledige Hallo stappen te volgen:

1. Zoek in hello Azure-portal, op Hallo *myVault* Recovery Services-kluizen item. Op Hallo **overzicht** blade onder **back-up items**, selecteer het aantal items Hallo.

    ![Recovery Services-kluizen myVault back-items](./media/oracle-backup-recovery/recovery_service_12.png)

2. Onder **back-up ITEMTELLING**, selecteer het aantal items Hallo.

    ![Recovery Services-kluizen aantal voor virtuele Machine van Azure-back-items](./media/oracle-backup-recovery/recovery_service_13.png)

3. Op Hallo **myvm1** blade, klikt u op **Bestandsherstel (Preview)**.

    ![Schermopname van Hallo Recovery Services-kluizen pagina voor herstel van bestand](./media/oracle-backup-recovery/recovery_service_14.png)

4. Op Hallo **Bestandsherstel (Preview)** deelvenster, klikt u op **downloadscript**. Sla hello (.sh) bestand tooa downloadmap op Hallo-clientcomputer.

    ![Opties voor het opslaan van bestanden script downloaden](./media/oracle-backup-recovery/recovery_service_15.png)

5. Kopieer Hallo .sh bestand toohello VM.

    Hallo volgende voorbeeld ziet u hoe u een beveiligde kopie (scp) opdracht toomove toouse Hallo bestand toohello VM. U kunt ook Hallo inhoud toohello Klembord en plak Hallo inhoud in een nieuw bestand dat is ingesteld op Hallo VM kopiëren.

    > [!IMPORTANT]
    > Zorg ervoor dat u het IP-adres en de map waarden Hallo bijwerken in Hallo voorbeeld te volgen. Hallo-waarden moeten toohello map Hallo-bestand wordt opgeslagen, worden toegewezen.

    ```bash
    $ scp Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh <publicIpAddress>:/<folder>
    ```
6. Hallo-bestand wijzigen zodat deze eigendom van het Hallo-hoofdmap.

    Wijzig in Hallo voorbeeld te volgen, Hallo-bestand zodat deze eigendom van het Hallo-hoofdmap. Wijzig machtigingen.

    ```bash 
    $ ssh <publicIpAddress>
    $ sudo su -
    # chown root:root /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # chmod 755 /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    # /<folder>/Linux_myvm1_xx-xx-2017 xx-xx-xx PM.sh
    ```
    Hallo volgende voorbeeld ziet u wat u ziet na het uitvoeren van script vóór Hallo. Wanneer u wordt gevraagd toocontinue, voer **Y**.

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

7. Toegang toohello gekoppelde volumes is bevestigd.

    tooexit, voer **q**, en zoek vervolgens naar Hallo gekoppelde volumes. een lijst met Hallo toegevoegd volumes, bij een opdrachtprompt, typ toocreate **df -k**.

    ![Hallo df -k opdracht](./media/oracle-backup-recovery/recovery_service_16.png)

8. Gebruik Hallo script toocopy Hallo ontbreekt na bestanden back toohello mappen:

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
9. In de Hallo script volgen, RMAN toorecover Hallo-database te gebruiken:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```
    
10. Hallo schijf ontkoppelen.

    In de Azure-portal op Hallo Hallo **Bestandsherstel (Preview)** blade, klikt u op **schijven ontkoppelen**.

    ![Ontkoppel de schijven opdracht](./media/oracle-backup-recovery/recovery_service_17.png)

## <a name="restore-hello-entire-vm"></a>Herstellen Hallo hele virtuele machine

In plaats van Hallo verwijderde bestanden terugzetten vanaf Hallo Recovery Services-kluizen, kunt u herstellen Hallo hele virtuele machine.

### <a name="step-1-delete-myvm"></a>Stap 1: Delete myVM

*   Ga in de Azure-portal hello, toohello **myVM1** -kluis en selecteer vervolgens **verwijderen**.

    ![Opdracht voor kluis verwijderen](./media/oracle-backup-recovery/recover_vm_01.png)

### <a name="step-2-recover-hello-vm"></a>Stap 2: Hallo VM herstellen

1.  Ga te**Recovery Services-kluizen**, en selecteer vervolgens **myVault**.

    ![myVault vermelding](./media/oracle-backup-recovery/recover_vm_02.png)

2.  Op Hallo **overzicht** blade onder **back-up items**, selecteer het aantal items Hallo.

    ![myVault back-up van items](./media/oracle-backup-recovery/recover_vm_03.png)

3.  Op Hallo **back-Upitems (Azure virtuele Machine)** blade Selecteer **myvm1**.

    ![VM-pagina voor wachtwoordherstel](./media/oracle-backup-recovery/recover_vm_04.png)

4.  Op Hallo **myvm1** blade, klik op Hallo weglatingsteken (**...** ) en klik vervolgens op **herstellen VM**.

    ![VM-opdracht herstellen](./media/oracle-backup-recovery/recover_vm_05.png)

5.  Op Hallo **herstelpunt selecteren** blade, selecteer Hallo-item dat u toorestore wilt en klik vervolgens op **OK**.

    ![Selecteer Hallo herstelpunt](./media/oracle-backup-recovery/recover_vm_06.png)

    Als u toepassingsconsistente back-up hebt ingeschakeld, wordt een verticale blauwe balk weergegeven.

6.  Op Hallo **configuratie terugzetten** blade naam van de virtuele machine selecteert hello, selecteer Hallo resourcegroep en klik vervolgens op **OK**.

    ![Configuratiewaarden herstellen](./media/oracle-backup-recovery/recover_vm_07.png)

7.  toorestore hello VM, klikt u op Hallo **herstellen** knop.

8.  tooview hello status van het herstelproces hello, klikt u op **taken**, en klik vervolgens op **back-uptaken**.

    ![Opdracht voor back-uptaken-status](./media/oracle-backup-recovery/recover_vm_08.png)

    Hallo ziet volgende afbeelding Hallo status van het herstelproces Hallo:

    ![Status van het herstelproces Hallo](./media/oracle-backup-recovery/recover_vm_09.png)

### <a name="step-3-set-hello-public-ip-address"></a>Stap 3: Stel Hallo openbare IP-adres
Nadat de Hallo die VM is hersteld, stelt u Hallo openbaar IP-adres.

1.  Voer in het zoekvak Hallo **openbaar IP-adres**.

    ![Lijst met openbare IP-adressen](./media/oracle-backup-recovery/create_ip_00.png)

2.  Op Hallo **openbare IP-adressen** blade, klikt u op **toevoegen**. Op Hallo **openbare IP-adres maken** blade voor **naam**, selecteer Hallo openbare IP-naam. Voor **Resourcegroep** selecteert u **Bestaande gebruiken**. Klik vervolgens op **Maken**.

    ![IP-adres maken](./media/oracle-backup-recovery/create_ip_01.png)

3.  tooassociate hello openbaar IP-adres aan de netwerkinterface Hallo voor Hallo VM, zoeken voor en selecteer **myVMip**. Klik vervolgens op **koppelen**.

    ![IP-adres koppelen](./media/oracle-backup-recovery/create_ip_02.png)

4.  Voor **brontype**, selecteer **netwerkinterface**. Hallo-netwerkinterface die wordt gebruikt door Hallo myVM exemplaar selecteren en klik vervolgens op **OK**.

    ![Selecteer het brontype en NIC-waarden](./media/oracle-backup-recovery/create_ip_03.png)

5.  Zoek en open Hallo exemplaar van myVM die wordt overgebracht van Hallo-portal. Hallo IP-adres dat is gekoppeld aan VM hello wordt weergegeven op Hallo myVM **overzicht** blade.

    ![IP-adreswaarde](./media/oracle-backup-recovery/create_ip_04.png)

### <a name="step-4-connect-toohello-vm"></a>Stap 4: Verbinding maken met toohello VM

*   tooconnect toohello virtuele machine, gebruik Hallo script volgen:

    ```bash 
    ssh <publicIpAddress>
    ```

### <a name="step-5-test-whether-hello-database-is-accessible"></a>Stap 5: Controleren of het Hallo-database toegankelijk is
*   tootest toegankelijkheid, gebruik Hallo script volgen:

    ```bash 
    $ sudo su - oracle
    $ sqlplus / as sysdba
    SQL> startup
    ```

    > [!IMPORTANT]
    > Als hello database **opstarten** opdracht genereert een fout, toorecover Hallo database, raadpleegt u [stap 6: gebruik RMAN toorecover Hallo database](#step-6-optional-use-rman-to-recover-the-database).

### <a name="step-6-optional-use-rman-toorecover-hello-database"></a>Stap 6: (Optioneel) gebruik RMAN toorecover Hallo database
*   toorecover hello database gebruik Hallo script volgen:

    ```bash
    # sudo su - oracle
    $ rman target /
    RMAN> startup mount;
    RMAN> restore database;
    RMAN> recover database;
    RMAN> alter database open resetlogs;
    RMAN> SELECT * FROM scott.scott_table;
    ```

Hallo back-up en herstel van Hallo Oracle-Database 12c-database op een Azure Linux VM is nu voltooid.

## <a name="delete-hello-vm"></a>Hallo VM verwijderen

Wanneer u virtuele machine niet meer nodig hello, kunt u na de opdracht tooremove Hallo-resourcegroep, Hallo VM en alle gerelateerde resources hello gebruiken:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

[Zelfstudie: Een maximaal beschikbare virtuele machines maken](../../linux/create-cli-complete.md)

[VM-implementatie Azure CLI voorbeelden verkennen](../../linux/cli-samples.md)




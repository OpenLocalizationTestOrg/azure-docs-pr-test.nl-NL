---
title: aaaImplement Oracle Golden Gate op een Azure Linux VM | Microsoft Docs
description: Snel gebruiksklaar een Gate Oracle Golden omhoog in uw Azure-omgeving.
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Oracle Golden Gate implementeren op een Azure Linux VM 

Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts. Deze handleiding details hoe toouse hello Azure CLI toodeploy een Oracle-12-c-database van de afbeelding hello Azure Marketplace. 

Dit document toont stapsgewijs hoe toocreate, installeren en configureren van Oracle Golden Gate op een Azure VM.

Voordat u begint, controleert u dat hello die Azure CLI is geïnstalleerd. Zie voor meer informatie de [Installatiehandleiding van de Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Hallo-omgeving voorbereiden

tooperform hello Oracle Golden Gate installatie, moet u twee toocreate Azure VM's op Hallo dezelfde beschikbaarheidsset. Hallo Marketplace-installatiekopie gebruiken van toocreate Hallo virtuele machines is **Oracle: Oracle-Database-Ee:12.1.0.2:latest**.

U ook toobe bekend bent met Unix-editor vi nodig hebt en basiskennis van x11 (Windows X).

Hallo Hier volgt een samenvatting van configuratie van Hallo-omgeving:
> 
> |  | **Primaire site** | **Replicatie van site** |
> | --- | --- | --- |
> | **Oracle-release** |Oracle 12c versie 2: (12.1.0.2) |Oracle 12c versie 2: (12.1.0.2)|
> | **Computernaam** |myVM1 |myVM2 |
> | **Besturingssysteem** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **Oracle-SID** |CDB1 |CDB1 |
> | **Schema voor replicatie** |TEST|TEST |
> | **Golden Gate eigenaar/repliceren** |C ##GGADMIN |REPUSER |
> | **Golden Gate-proces** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>Meld u aan tooAzure 

Meld u aan Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht. Volg Hallo op het scherm richtingen.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container in welke Azure-resources zijn geïmplementeerd en die ze kunnen worden beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Een beschikbaarheidsset maken

Hallo stap is optioneel maar aanbevolen. Zie voor meer informatie [Azure handleiding voor beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Een virtuele machine maken

Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht. 

Hallo volgende voorbeeld maakt twee virtuele machines met de naam `myVM1` en `myVM2`. SSH-sleutels maken als deze niet al bestaan op de standaardlocatie van de sleutel. toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.

#### <a name="create-myvm1-primary"></a>Maak myVM1 (primaire):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Na het Hallo die VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. (Noteer Hallo `publicIpAddress`. Dit adres is gebruikte tooaccess Hallo VM).

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

#### <a name="create-myvm2-replicate"></a>MyVM2 maken (repliceren):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Let op Hallo `publicIpAddress` ook nadat deze is gemaakt.

### <a name="open-hello-tcp-port-for-connectivity"></a>Open TCP-poort Hallo voor connectiviteit

de volgende stap Hallo is tooconfigure externe eindpunten, waarmee u tooaccess Hallo Oracle-database op afstand. tooconfigure Hallo externe eindpunten, Hallo volgende opdrachten uitvoeren.

#### <a name="open-hello-port-for-myvm1"></a>Hallo-poort voor myVM1 openen:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Hallo resultaten ziet vergelijkbare toohello antwoord te volgen:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

#### <a name="open-hello-port-for-myvm2"></a>Hallo-poort voor myVM2 openen:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Verbinding maken met toohello virtuele machine

Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine. Hallo IP-adres vervangen door Hallo `publicIpAddress` van uw virtuele machine.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Hallo-database maken op myVM1 (primair)

Hallo Oracle-software is al geïnstalleerd op Hallo Marketplace-installatiekopie, zodat de volgende stap Hallo tooinstall Hallo-database. 

Hallo software Run as-Hallo 'oracle' supergebruiker:

```bash
sudo su - oracle
```

Hallo-database maken:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Uitvoer ziet er vergelijkbare toohello antwoord te volgen:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Hallo ORACLE_SID en ORACLE_HOME variabelen worden ingesteld.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

Desgewenst kunt u ORACLE_HOME en ORACLE_SID toohello .bashrc bestand, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen toevoegen:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Oracle-listener starten
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Hallo-database maken op myVM2 (repliceren)

```bash
sudo su - oracle
```
Hallo-database maken:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Hallo ORACLE_SID en ORACLE_HOME variabelen worden ingesteld.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

U kunt eventueel ORACLE_HOME en ORACLE_SID toohello .bashrc bestand toegevoegd, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Oracle-listener starten
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Golden Gate configureren 
tooconfigure Golden-Gate maatregelen treffen Hallo in deze sectie.

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>Bij myVM1 (primaire) archief logboek-modus inschakelen

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
```
Force logboekregistratie inschakelen en controleer of ten minste één logboekbestand aanwezig is.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Golden Gate-software downloaden
toodownload en bereid Hallo Oracle Golden Gate-software, volledige Hallo stappen te volgen:

1. Hallo downloaden **fbo_ggs_Linux_x64_shiphome.zip** bestand van Hallo [Oracle Golden Gate downloadpagina](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). Onder Hallo downloaden titel **Oracle GoldenGate 12.x.x.x voor Oracle Linux x86-64**, moet er een reeks ZIP-bestanden toodownload.

2. Nadat u Hallo ZIP-bestanden tooyour-clientcomputer hebt gedownload, gebruikt u beveiligde kopie Protocol (SCP) toocopy Hallo bestanden tooyour VM:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Hallo ZIP-bestanden toohello verplaatsen **/ opt** map. Wijzig Hallo eigenaar van Hallo bestanden als volgt:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. Pak Hallo-bestanden (installatie Hallo Linux pak hulpprogramma als deze nog niet is geïnstalleerd):

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. De machtiging wijzigen:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Voorbereiden op Hallo-client en de VM toorun x11 (alleen voor Windows-clients)
Dit is een optionele stap. U kunt deze stap overslaan als u een voor Linux client of al x11 hebt setup.

1. Download PuTTY en Xming tooyour Windows-computer:

  * [Download PuTTY](http://www.putty.org/)
  * [Xming downloaden](https://xming.en.softonic.com/)

2.  Nadat u PuTTY in Hallo PuTTY map (bijvoorbeeld C:\Program Files\PuTTY), puttygen.exe (Generator PuTTY Key) uitvoeren.

3.  In de PuTTY codegenerator:

  - een sleutel, selecteer Hallo toogenerate **genereren** knop.
  - Kopieer de inhoud Hallo van Hallo-sleutel (**Ctrl + C**).
  - Selecteer Hallo **persoonlijke sleutel opslaan** knop.
  - Hallo-waarschuwing die wordt weergegeven, en selecteer vervolgens negeren **OK**.

    ![Schermafbeelding van pagina met PuTTY codegenerator Hallo](./media/oracle-golden-gate/puttykeygen.png)

4.  In de virtuele machine, moet u deze opdrachten uitvoeren:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Maak een bestand met de naam **authorized_keys**. Hallo-inhoud van Hallo key plakken in dit bestand en sla Hallo-bestand.

  > [!NOTE]
  > Hallo-sleutel moet Hallo tekenreeks bevatten `ssh-rsa`. Hallo-inhoud van Hallo-sleutel moet ook een enkele regel tekst.
  >  

6. Start PuTTY. In Hallo **categorie** deelvenster **verbinding** > **SSH** > **Auth**. In Hallo **persoonlijke sleutelbestand voor verificatie** vak, blader toohello-sleutel die u eerder hebt gegenereerd.

  ![Schermafbeelding van pagina van de persoonlijke sleutel instellen Hallo](./media/oracle-golden-gate/setprivatekey.png)

7. In Hallo **categorie** deelvenster **verbinding** > **SSH** > **X11**. Selecteer vervolgens Hallo **inschakelen X11 doorsturen** vak.

  ![Schermafbeelding van pagina met Hallo X11 inschakelen](./media/oracle-golden-gate/enablex11.png)

8. In Hallo **categorie** deelvenster te gaan**sessie**. Geef informatie op Hallo host, en selecteer vervolgens **Open**.

  ![Schermafbeelding van pagina met Hallo sessie](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Golden Gate software installeren

tooinstall Oracle Golden Gate, volledige Hallo stappen te volgen:

1. Meld u aan als oracle. (U moet kunnen toosign in zonder te worden gevraagd om een wachtwoord.) Zorg ervoor dat Xming voordat u begint met Hallo-installatie wordt uitgevoerd.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. Selecteer 'Oracle GoldenGate voor Oracle-Database 12c'. Selecteer vervolgens **volgende** toocontinue.

  ![Schermafbeelding van pagina met Hallo installatieprogramma installatie selecteren](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Hallo software locatie wijzigen. Selecteer vervolgens Hallo **Manager Start** in en voert u de locatie van de database Hallo. Selecteer **volgende** toocontinue.

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Hallo-inventarisatie map wijzigen, en selecteer vervolgens **volgende** toocontinue.

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_03.png)

5. Op Hallo **samenvatting** Schakel in het scherm **installeren** toocontinue.

  ![Schermafbeelding van pagina met Hallo installatieprogramma installatie selecteren](./media/oracle-golden-gate/golden_gate_install_04.png)

6. Vraag toorun een script is mogelijk als 'root'. Zo ja, open een afzonderlijke sessie ssh toohello VM, sudo tooroot, en vervolgens Hallo-script uitvoeren. Selecteer **OK** gaan.

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Wanneer het Hallo-installatie is voltooid, selecteert u **sluiten** toocomplete Hallo proces.

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>Instellen van de service op myVM1 (primair)

1. Maken of bijwerken van Hallo tnsnames.ora bestand:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Hallo Golden Gate eigenaar en gebruikersaccounts maken.

  > [!NOTE]
  > Hallo eigenaarsaccount moet C ## voorvoegsel hebben.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Hallo Golden Gate test-gebruikersaccount maken:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Hallo extract parameterbestand configureren.

 Hallo gouden gate-opdrachtregelinterface (ggsci) starten:

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Hallo toohello EXTRACT parameterbestand volgen (via vi opdrachten) toevoegen. Druk op Esc-toets ': wq!' toosave-bestand. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. Registratie uit te pakken--geïntegreerde uitpakken.

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Extract controlepunten ingesteld en realtime extract te starten:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
In deze stap ziet u Hallo SCN die later wordt gebruikt in een andere sectie starten:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>Instellen van de service op myVM2 (repliceren)


1. Maken of bijwerken van Hallo tnsnames.ora bestand:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Een repliceren account maken:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Maak een gebruikersaccount voor Golden Gate-test:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. REPLICAT parameter tooreplicate bestandswijzigingen: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  De inhoud van het parameterbestand REPORA:

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Een controlepunt replicat instellen:

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>Hallo-replicatie (myVM1 en myVM2) instellen

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. Hallo-replicatie op myVM2 instellen (repliceren)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Hallo-bestand met de volgende Hallo bijwerken:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Hallo Manager-service vervolgens opnieuw te starten:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. Hallo-replicatie op myVM1 (primaire) instellen

Start Hallo initiële laden en controleren op fouten:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. Hallo-replicatie op myVM2 instellen (repliceren)

Hallo SCN nummer met Hallo nummer dat u eerder hebt verkregen wijzigen:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
Hallo-replicatie is gestart en u kunt het testen door het invoegen van nieuwe records tooTEST tabellen.


### <a name="view-job-status-and-troubleshooting"></a>Status van de taak weergeven en problemen oplossen

#### <a name="view-reports"></a>Rapporten weergeven
tooview rapporten over myVM1, Hallo volgende opdrachten uitvoeren:

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview rapporten over myVM2, Hallo volgende opdrachten uitvoeren:

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Weergave status en geschiedenis
tooview status en geschiedenis op myVM1, Hallo volgende opdrachten uitvoeren:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

tooview status en geschiedenis op myVM2, Hallo volgende opdrachten uitvoeren:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Dit is voltooid Hallo-installatie en configuratie van Golden Gate op Oracle linux.


## <a name="delete-hello-virtual-machine"></a>Hallo virtuele machine verwijderen

Wanneer deze niet langer nodig is, kan na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, VM en alle gerelateerde resources zijn.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

[Zelfstudie voor het maken van virtuele machines met een hoge beschikbaarheid](../../linux/create-cli-complete.md)

[CLI-voorbeelden voor VM-implementatie verkennen](../../linux/cli-samples.md)

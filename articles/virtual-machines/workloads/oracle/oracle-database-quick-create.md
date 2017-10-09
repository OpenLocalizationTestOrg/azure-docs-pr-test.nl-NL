---
title: een Oracle-database in een Azure VM aaaCreate | Microsoft Docs
description: Snel gebruiksklaar een Oracle-Database 12c-database in uw Azure-omgeving.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Maak een Oracle-Database in een Azure VM

Deze handleiding wilt weergeven hello Azure CLI toodeploy een virtuele machine van Azure van Hallo [Oracle marketplace afbeelding](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in volgorde toocreate een 12-c Oracle-database. Zodra Hallo-server is geïmplementeerd, maakt u verbinding via SSH in volgorde tooconfigure Hallo Oracle-database. 

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger. Voer `az --version` toofind Hallo versie. Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht. Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd. 

Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Virtuele machine maken

een virtuele machine (VM), toocreate gebruiken Hallo [az vm maken](/cli/azure/vm#create) opdracht. 

Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM`. SSH-sleutels wordt ook gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel. toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Nadat u Hallo VM maakt, geeft Azure CLI informatie vergelijkbare toohello voorbeeld te volgen. Houd er rekening mee Hallo-waarde voor `publicIpAddress`. U gebruikt dit adres tooaccess Hallo VM.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Verbinding maken met toohello VM

toocreate een SSH-sessie met de virtuele machine, Hallo Hallo volgende opdracht gebruiken. Hallo IP-adres vervangen door Hallo `publicIpAddress` waarde voor uw virtuele machine.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Hallo-database maken

Hallo Oracle-software is al geïnstalleerd op Hallo Marketplace-installatiekopie. Als volgt te werk om een voorbeelddatabase te maken. 

1.  Overschakelen van toohello *oracle* supergebruiker en vervolgens Hallo-listener initialiseren voor logboekregistratie:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    Hallo-uitvoer is vergelijkbaar toohello volgende:

    ```bash
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

2.  Hallo-database maken:

    ```bash
    dbca -silent \
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

    Het duurt enkele minuten toocreate Hallo-database.

3. Oracle-variabelen instellen

Voordat u verbinding maakt, moet u twee tooset omgevingsvariabelen: *ORACLE_HOME* en *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
U kunt ook ORACLE_HOME en ORACLE_SID variabelen toohello .bashrc bestand toevoegen. Hierdoor zou de omgevingsvariabelen Hallo voor toekomstige aanmeldingen opgeslagen. Hallo volgende bevestigen instructies hebt toegevoegd toohello `~/.bashrc` bestand met behulp van de editor van uw keuze.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Oracle EM snelle verbindingen

Voor een GUI-beheerprogramma waarmee u tooexplore Hallo database kunt, Oracle EM Express instellen. tooconnect tooOracle EM Express, moet u eerst instellen Hallo-poort in Oracle. 

1. Verbinding maken met behulp van sqlplus tooyour-database:

    ```bash
    sqlplus / as sysdba
    ```

2. Eenmaal zijn verbonden, Hallo poort 5502 instellen voor snelle EM

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Open Hallo container PDB1 als dat niet al is geopend, maar het eerste selectievakje Hallo status:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    Hallo-uitvoer is vergelijkbaar toohello volgende:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Als Hallo OPEN_MODE voor `PDB1` is niet gelezen SCHRIJFT, voer de volgende opdrachten tooopen PDB1 van Hallo:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

U moet tootype `quit` tooend Hallo sqlplus sessie en het type `exit` toologout van Hallo oracle-gebruiker.

## <a name="automate-database-startup-and-shutdown"></a>Database opstarten en afsluiten automatiseren

Hallo Oracle-database standaard niet automatisch wordt gestart wanneer u Hallo VM opnieuw opstart. tooset up Hallo Oracle-database toostart automatisch eerst aanmelden als hoofdmap. Vervolgens maken en bijwerken van sommige systeembestanden.

1. Aanmelden als hoofdmap
    ```bash
    sudo su -
    ```

2.  Hallo-bestand met behulp van uw favoriete editor bewerken `/etc/oratab` en wijzig Hallo standaard `N` te`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Maak een bestand met de naam `/etc/init.d/dbora` en inhoud te plakken Hallo volgen:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  Wijzigen van machtigingen voor bestanden met *type chmod* als volgt:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Symbolische koppelingen maken voor opstarten en afsluiten als volgt:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest uw wijzigingen Hallo VM opnieuw starten:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Open poorten voor connectiviteit

de laatste taak Hallo tooconfigure sommige externe eindpunten is. tooset up hello Azure Netwerkbeveiligingsgroep die Hallo VM beveiligt, sluit u eerst uw SSH-sessie in Hallo VM (moet hebben is volledig buiten SSH wanneer opnieuw opstarten in de vorige stap). 

1.  tooopen hello eindpunt dat u tooaccess Hallo Oracle-database op afstand, maakt u een regel Netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) als volgt: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  tooopen hello eindpunt dat u tooaccess Oracle EM Express op afstand, maakt u een regel Netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) als volgt:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. Indien nodig, verkrijgen Hallo openbare IP-adres van uw virtuele machine opnieuw met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show) als volgt:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  Verbinding maken met snelle EM vanuit de browser. Controleer of dat uw browser is compatibel met EM Express (Flash installatie is vereist): 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

U kunt aanmelden met behulp van Hallo **SYS** account en controleer Hallo **als sysdba** selectievakje. Gebruik Hallo wachtwoord **OraPasswd1** die u hebt ingesteld tijdens de installatie. 

![Schermopname van Hallo Oracle OEM Express aanmeldingspagina](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Resources opschonen

Zodra u klaar bent met het verkennen van uw eerste Oracle-database in Azure en hello VM niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over andere [Oracle-oplossingen in Azure](oracle-considerations.md). 

Probeer Hallo [installeren en configureren van Oracle geautomatiseerde Storage Management](configure-oracle-asm.md) zelfstudie.

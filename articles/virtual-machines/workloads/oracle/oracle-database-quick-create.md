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
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="2f1cd-103">Maak een Oracle-Database in een Azure VM</span><span class="sxs-lookup"><span data-stu-id="2f1cd-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="2f1cd-104">Deze handleiding wilt weergeven hello Azure CLI toodeploy een virtuele machine van Azure van Hallo [Oracle marketplace afbeelding](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in volgorde toocreate een 12-c Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="2f1cd-105">Zodra Hallo-server is geïmplementeerd, maakt u verbinding via SSH in volgorde tooconfigure Hallo Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="2f1cd-106">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2f1cd-107">Als u tooinstall kiest en Hallo CLI lokaal gebruiken, is deze snelstartgids vereist dat u de versie van de Azure CLI Hallo 2.0.4 worden uitgevoerd of hoger.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2f1cd-108">Voer `az --version` toofind Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2f1cd-109">Als u tooinstall of upgrade nodig hebt, raadpleegt u [2.0 voor Azure CLI installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2f1cd-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="2f1cd-110">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="2f1cd-110">Create a resource group</span></span>

<span data-ttu-id="2f1cd-111">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="2f1cd-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="2f1cd-113">Hallo volgende voorbeeld maakt u een resourcegroep met de naam *myResourceGroup* in Hallo *eastus* locatie.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="2f1cd-114">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="2f1cd-114">Create virtual machine</span></span>

<span data-ttu-id="2f1cd-115">een virtuele machine (VM), toocreate gebruiken Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="2f1cd-116">Hallo volgende voorbeeld wordt een virtuele machine met de naam `myVM`.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="2f1cd-117">SSH-sleutels wordt ook gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="2f1cd-118">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="2f1cd-119">Nadat u Hallo VM maakt, geeft Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="2f1cd-120">Houd er rekening mee Hallo-waarde voor `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="2f1cd-121">U gebruikt dit adres tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-121">You use this address tooaccess hello VM.</span></span>

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

## <a name="connect-toohello-vm"></a><span data-ttu-id="2f1cd-122">Verbinding maken met toohello VM</span><span class="sxs-lookup"><span data-stu-id="2f1cd-122">Connect toohello VM</span></span>

<span data-ttu-id="2f1cd-123">toocreate een SSH-sessie met de virtuele machine, Hallo Hallo volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="2f1cd-124">Hallo IP-adres vervangen door Hallo `publicIpAddress` waarde voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="2f1cd-125">Hallo-database maken</span><span class="sxs-lookup"><span data-stu-id="2f1cd-125">Create hello database</span></span>

<span data-ttu-id="2f1cd-126">Hallo Oracle-software is al geïnstalleerd op Hallo Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="2f1cd-127">Als volgt te werk om een voorbeelddatabase te maken.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="2f1cd-128">Overschakelen van toohello *oracle* supergebruiker en vervolgens Hallo-listener initialiseren voor logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="2f1cd-129">Hallo-uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-129">hello output is similar toohello following:</span></span>

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

2.  <span data-ttu-id="2f1cd-130">Hallo-database maken:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-130">Create hello database:</span></span>

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

    <span data-ttu-id="2f1cd-131">Het duurt enkele minuten toocreate Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="2f1cd-132">Oracle-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="2f1cd-132">Set Oracle variables</span></span>

<span data-ttu-id="2f1cd-133">Voordat u verbinding maakt, moet u twee tooset omgevingsvariabelen: *ORACLE_HOME* en *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="2f1cd-134">U kunt ook ORACLE_HOME en ORACLE_SID variabelen toohello .bashrc bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="2f1cd-135">Hierdoor zou de omgevingsvariabelen Hallo voor toekomstige aanmeldingen opgeslagen. Hallo volgende bevestigen instructies hebt toegevoegd toohello `~/.bashrc` bestand met behulp van de editor van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="2f1cd-136">Oracle EM snelle verbindingen</span><span class="sxs-lookup"><span data-stu-id="2f1cd-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="2f1cd-137">Voor een GUI-beheerprogramma waarmee u tooexplore Hallo database kunt, Oracle EM Express instellen.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="2f1cd-138">tooconnect tooOracle EM Express, moet u eerst instellen Hallo-poort in Oracle.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="2f1cd-139">Verbinding maken met behulp van sqlplus tooyour-database:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="2f1cd-140">Eenmaal zijn verbonden, Hallo poort 5502 instellen voor snelle EM</span><span class="sxs-lookup"><span data-stu-id="2f1cd-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="2f1cd-141">Open Hallo container PDB1 als dat niet al is geopend, maar het eerste selectievakje Hallo status:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="2f1cd-142">Hallo-uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="2f1cd-143">Als Hallo OPEN_MODE voor `PDB1` is niet gelezen SCHRIJFT, voer de volgende opdrachten tooopen PDB1 van Hallo:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="2f1cd-144">U moet tootype `quit` tooend Hallo sqlplus sessie en het type `exit` toologout van Hallo oracle-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="2f1cd-145">Database opstarten en afsluiten automatiseren</span><span class="sxs-lookup"><span data-stu-id="2f1cd-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="2f1cd-146">Hallo Oracle-database standaard niet automatisch wordt gestart wanneer u Hallo VM opnieuw opstart.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="2f1cd-147">tooset up Hallo Oracle-database toostart automatisch eerst aanmelden als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="2f1cd-148">Vervolgens maken en bijwerken van sommige systeembestanden.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="2f1cd-149">Aanmelden als hoofdmap</span><span class="sxs-lookup"><span data-stu-id="2f1cd-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="2f1cd-150">Hallo-bestand met behulp van uw favoriete editor bewerken `/etc/oratab` en wijzig Hallo standaard `N` te`Y`:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="2f1cd-151">Maak een bestand met de naam `/etc/init.d/dbora` en inhoud te plakken Hallo volgen:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

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

4.  <span data-ttu-id="2f1cd-152">Wijzigen van machtigingen voor bestanden met *type chmod* als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="2f1cd-153">Symbolische koppelingen maken voor opstarten en afsluiten als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="2f1cd-154">tootest uw wijzigingen Hallo VM opnieuw starten:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="2f1cd-155">Open poorten voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="2f1cd-155">Open ports for connectivity</span></span>

<span data-ttu-id="2f1cd-156">de laatste taak Hallo tooconfigure sommige externe eindpunten is.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="2f1cd-157">tooset up hello Azure Netwerkbeveiligingsgroep die Hallo VM beveiligt, sluit u eerst uw SSH-sessie in Hallo VM (moet hebben is volledig buiten SSH wanneer opnieuw opstarten in de vorige stap).</span><span class="sxs-lookup"><span data-stu-id="2f1cd-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="2f1cd-158">tooopen hello eindpunt dat u tooaccess Hallo Oracle-database op afstand, maakt u een regel Netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="2f1cd-159">tooopen hello eindpunt dat u tooaccess Oracle EM Express op afstand, maakt u een regel Netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="2f1cd-160">Indien nodig, verkrijgen Hallo openbare IP-adres van uw virtuele machine opnieuw met [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show) als volgt:</span><span class="sxs-lookup"><span data-stu-id="2f1cd-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="2f1cd-161">Verbinding maken met snelle EM vanuit de browser.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="2f1cd-162">Controleer of dat uw browser is compatibel met EM Express (Flash installatie is vereist):</span><span class="sxs-lookup"><span data-stu-id="2f1cd-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="2f1cd-163">U kunt aanmelden met behulp van Hallo **SYS** account en controleer Hallo **als sysdba** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="2f1cd-164">Gebruik Hallo wachtwoord **OraPasswd1** die u hebt ingesteld tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Schermopname van Hallo Oracle OEM Express aanmeldingspagina](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="2f1cd-166">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="2f1cd-166">Clean up resources</span></span>

<span data-ttu-id="2f1cd-167">Zodra u klaar bent met het verkennen van uw eerste Oracle-database in Azure en hello VM niet langer nodig is, kunt u Hallo [az groep verwijderen](/cli/azure/group#delete) opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="2f1cd-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2f1cd-168">Next steps</span></span>

<span data-ttu-id="2f1cd-169">Meer informatie over andere [Oracle-oplossingen in Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="2f1cd-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="2f1cd-170">Probeer Hallo [installeren en configureren van Oracle geautomatiseerde Storage Management](configure-oracle-asm.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2f1cd-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>

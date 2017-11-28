---
title: Maken van een Oracle-database in een virtuele machine in Azure | Microsoft Docs
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="ddbb0-103">Maak een Oracle-Database in een Azure VM</span><span class="sxs-lookup"><span data-stu-id="ddbb0-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="ddbb0-104">Deze handleiding details met de Azure CLI voor het implementeren van een Azure virtuele machine van de [Oracle marketplace afbeelding](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) om te kunnen maken van een 12-c Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="ddbb0-105">Zodra de server is geïmplementeerd, maakt u verbinding via SSH om te configureren van de Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="ddbb0-106">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ddbb0-107">Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u voor deze snelstartgids de versie Azure CLI 2.0.4 of hoger uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="ddbb0-108">Voer `az --version` uit om de versie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="ddbb0-109">Als u Azure CLI 2.0 wilt installeren of upgraden, raadpleegt u [Azure CLI 2.0 installeren]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ddbb0-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ddbb0-110">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="ddbb0-110">Create a resource group</span></span>

<span data-ttu-id="ddbb0-111">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="ddbb0-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="ddbb0-112">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="ddbb0-113">In het volgende voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *VS Oost*.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="ddbb0-114">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="ddbb0-114">Create virtual machine</span></span>

<span data-ttu-id="ddbb0-115">Gebruik voor het maken van een virtuele machine (VM) de [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="ddbb0-116">In het volgende voorbeeld wordt een virtuele machine met de naam `myVM` gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="ddbb0-117">SSH-sleutels wordt ook gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="ddbb0-118">Als u een specifieke set sleutels wilt gebruiken, gebruikt u de optie `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="ddbb0-119">Nadat u de virtuele machine hebt gemaakt, ziet Azure CLI er ongeveer als volgt uitzien.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="ddbb0-120">Noteer de waarde voor `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="ddbb0-121">U kunt dit adres gebruiken voor toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="ddbb0-122">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="ddbb0-122">Connect to the VM</span></span>

<span data-ttu-id="ddbb0-123">Maakt een SSH-sessie met de virtuele machine, moet u de volgende opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="ddbb0-124">Vervang de IP-adres met de `publicIpAddress` waarde voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="ddbb0-125">De database maken</span><span class="sxs-lookup"><span data-stu-id="ddbb0-125">Create the database</span></span>

<span data-ttu-id="ddbb0-126">De Oracle-software is al geïnstalleerd op de Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="ddbb0-127">Als volgt te werk om een voorbeelddatabase te maken.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="ddbb0-128">Overschakelen naar de *oracle* supergebruiker en vervolgens de initialisatie van de listener voor logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="ddbb0-129">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-129">The output is similar to the following:</span></span>

    ```bash
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

2.  <span data-ttu-id="ddbb0-130">De database maken:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-130">Create the database:</span></span>

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

    <span data-ttu-id="ddbb0-131">Het duurt enkele minuten om de database te maken.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="ddbb0-132">Oracle-variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="ddbb0-132">Set Oracle variables</span></span>

<span data-ttu-id="ddbb0-133">Voordat u verbinding maakt, moet u twee omgevingsvariabelen worden ingesteld: *ORACLE_HOME* en *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="ddbb0-134">U kunt ook variabelen ORACLE_HOME en ORACLE_SID toevoegen aan het bestand .bashrc.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="ddbb0-135">Hierdoor zou de omgevingsvariabelen voor toekomstige aanmeldingen opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="ddbb0-136">Controleer de volgende instructies zijn toegevoegd aan de `~/.bashrc` bestand met behulp van de editor van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="ddbb0-137">Oracle EM snelle verbindingen</span><span class="sxs-lookup"><span data-stu-id="ddbb0-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="ddbb0-138">Voor een GUI-beheerprogramma waarmee u kunt de database verkennen, Oracle EM Express instellen.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="ddbb0-139">Als u wilt verbinding maken met Oracle EM Express, moet u eerst de poort in Oracle instellen.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="ddbb0-140">Verbinding maken met de database met de sqlplus:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="ddbb0-141">Eenmaal zijn verbonden, de poort 5502 instellen voor snelle EM</span><span class="sxs-lookup"><span data-stu-id="ddbb0-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="ddbb0-142">Open de container PDB1 als dat niet al is geopend, maar het eerste Controleer de status:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="ddbb0-143">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="ddbb0-144">Als de OPEN_MODE voor `PDB1` is niet gelezen SCHRIJFT, voer de volgende opdrachten PDB1 openen:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="ddbb0-145">U moet zelf typen `quit` naar einde van de sessie sqlplus en het type `exit` af te melden van de oracle-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="ddbb0-146">Database opstarten en afsluiten automatiseren</span><span class="sxs-lookup"><span data-stu-id="ddbb0-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="ddbb0-147">De Oracle-database standaard niet automatisch wordt gestart wanneer u de virtuele machine opnieuw opstart.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="ddbb0-148">Als u de Oracle-database instelt op automatisch starten, zich eerst aanmelden als hoofdmap.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="ddbb0-149">Vervolgens maken en bijwerken van sommige systeembestanden.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="ddbb0-150">Aanmelden als hoofdmap</span><span class="sxs-lookup"><span data-stu-id="ddbb0-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="ddbb0-151">Met behulp van uw favoriete editor Bewerk het bestand `/etc/oratab` en wijzigt u de standaard `N` naar `Y`:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="ddbb0-152">Maak een bestand met de naam `/etc/init.d/dbora` en plak de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="ddbb0-153">Wijzigen van machtigingen voor bestanden met *type chmod* als volgt:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="ddbb0-154">Symbolische koppelingen maken voor opstarten en afsluiten als volgt:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="ddbb0-155">Start opnieuw op de virtuele machine voor het testen van de wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="ddbb0-156">Open poorten voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="ddbb0-156">Open ports for connectivity</span></span>

<span data-ttu-id="ddbb0-157">De laatste taak is het aantal externe eindpunten configureren.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="ddbb0-158">Als u de Azure-netwerk-beveiligingsgroep die de virtuele machine beveiligt instelt, moet u eerst uw SSH-sessie in de virtuele machine (moet hebben is volledig buiten SSH wanneer opnieuw opstarten in de vorige stap) sluiten.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="ddbb0-159">Om te openen van het eindpunt waarmee u kunt extern toegang tot de Oracle-database, maakt u een regel Netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) als volgt:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="ddbb0-160">Om te openen van het eindpunt dat u extern toegang tot Oracle EM Express gebruiken, maakt u een regel Netwerkbeveiligingsgroep met [az netwerk nsg regel maken](/cli/azure/network/nsg/rule#create) als volgt:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="ddbb0-161">Indien nodig, het openbare IP-adres van uw virtuele machine opnieuw met verkrijgen [az netwerk openbare ip-weergeven](/cli/azure/network/public-ip#show) als volgt:</span><span class="sxs-lookup"><span data-stu-id="ddbb0-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="ddbb0-162">Verbinding maken met snelle EM vanuit de browser.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="ddbb0-163">Controleer of dat uw browser is compatibel met EM Express (Flash installatie is vereist):</span><span class="sxs-lookup"><span data-stu-id="ddbb0-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="ddbb0-164">U kunt aanmelden met behulp van de **SYS** account en controleer de **als sysdba** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="ddbb0-165">Het wachtwoord gebruiken **OraPasswd1** die u hebt ingesteld tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Schermafbeelding van de aanmeldingspagina Oracle OEM Express](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="ddbb0-167">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="ddbb0-167">Clean up resources</span></span>

<span data-ttu-id="ddbb0-168">Als u klaar bent met het verkennen van uw eerste Oracle-database in Azure en de virtuele machine niet meer nodig is, kunt u de [az groep verwijderen](/cli/azure/group#delete) opdracht voor het verwijderen van de resourcegroep, VM, en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="ddbb0-169">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ddbb0-169">Next steps</span></span>

<span data-ttu-id="ddbb0-170">Meer informatie over andere [Oracle-oplossingen in Azure](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="ddbb0-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="ddbb0-171">Probeer de [installeren en configureren van Oracle geautomatiseerde Storage Management](configure-oracle-asm.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ddbb0-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
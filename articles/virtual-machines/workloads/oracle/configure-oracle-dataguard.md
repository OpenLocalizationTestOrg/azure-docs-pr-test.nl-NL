---
title: Oracle Data Guard implementeren op een virtuele machine van Azure Linux | Microsoft Docs
description: Snel gebruiksklaar Oracle Data Guard omhoog in uw Azure-omgeving.
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
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: 11492b85e95ddb39489e36c572af2a168b4c7af8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="7e1fd-103">Oracle Data Guard implementeren op een virtuele machine van Azure Linux</span><span class="sxs-lookup"><span data-stu-id="7e1fd-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="7e1fd-104">Azure CLI wordt gebruikt voor het maken en beheren van Azure-resources vanaf de opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-104">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="7e1fd-105">Dit artikel wordt beschreven hoe u Azure CLI gebruiken voor het implementeren van een database van de Oracle-Database 12c vanaf de Azure Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-105">This article describes how to use Azure CLI to deploy an Oracle Database 12c database from the Azure Marketplace image.</span></span> <span data-ttu-id="7e1fd-106">In dit artikel ziet u stap voor stap, klikt u vervolgens het installeren en configureren van Data Guard op Azure een virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="7e1fd-106">This article then shows you, step by step, how to install and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="7e1fd-107">Voordat u begint, zorg ervoor dat de Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="7e1fd-108">Zie voor meer informatie de [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7e1fd-108">For more information, see the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="7e1fd-109">De omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7e1fd-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="7e1fd-110">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="7e1fd-110">Assumptions</span></span>

<span data-ttu-id="7e1fd-111">Als u wilt installeren Oracle Data Guard, moet u twee virtuele Azure-machines op dezelfde beschikbaarheidsset maken:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-111">To install Oracle Data Guard, you need to create two Azure VMs on the same availability set:</span></span>

- <span data-ttu-id="7e1fd-112">De primaire virtuele machine (myVM1) heeft een actief Oracle-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-112">The primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="7e1fd-113">De stand-by VM (myVM2) heeft de Oracle-software alleen worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-113">The standby VM (myVM2) has the Oracle software installed only.</span></span>

<span data-ttu-id="7e1fd-114">De Marketplace-installatiekopie die u gebruikt voor het maken van de virtuele machines is Oracle: Oracle-Database-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-114">The Marketplace image that you use to create the VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="7e1fd-115">Aanmelden bij Azure</span><span class="sxs-lookup"><span data-stu-id="7e1fd-115">Sign in to Azure</span></span> 

<span data-ttu-id="7e1fd-116">Aanmelden bij uw Azure-abonnement met behulp van de [az aanmelding](/cli/azure/#login) opdracht in en volg de op het scherm richtingen.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-116">Sign in to your Azure subscription by using the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="7e1fd-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="7e1fd-117">Create a resource group</span></span>

<span data-ttu-id="7e1fd-118">Een resourcegroep maken met behulp van de [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-118">Create a resource group by using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7e1fd-119">Een Azure-resourcegroep is een logische container in welke Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7e1fd-120">Het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` in de `westus` locatie:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-120">The following example creates a resource group named `myResourceGroup` in the `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="7e1fd-121">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="7e1fd-121">Create an availability set</span></span>

<span data-ttu-id="7e1fd-122">Maken van een beschikbaarheidsset is optioneel, maar wordt u aangeraden deze.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="7e1fd-123">Zie voor meer informatie [Azure beschikbaarheidssets richtlijnen](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="7e1fd-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="7e1fd-124">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="7e1fd-124">Create a virtual machine</span></span>

<span data-ttu-id="7e1fd-125">Een virtuele machine maken met behulp van de [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-125">Create a VM by using the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="7e1fd-126">Het volgende voorbeeld maakt twee virtuele machines met de naam `myVM1` en `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-126">The following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="7e1fd-127">SSH-sleutels wordt ook gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="7e1fd-128">Als u een specifieke set sleutels wilt gebruiken, gebruikt u de optie `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="7e1fd-129">Maak myVM1 (primaire):</span><span class="sxs-lookup"><span data-stu-id="7e1fd-129">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="7e1fd-130">Nadat u de virtuele machine hebt gemaakt, geeft Azure CLI informatie weer zoals in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-130">After you create the VM, Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="7e1fd-131">Noteer de waarde van `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-131">Note the value of `publicIpAddress`.</span></span> <span data-ttu-id="7e1fd-132">U kunt dit adres gebruiken voor toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-132">You use this address to access the VM.</span></span>

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

<span data-ttu-id="7e1fd-133">MyVM2 maken (stand-by):</span><span class="sxs-lookup"><span data-stu-id="7e1fd-133">Create myVM2 (standby):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

<span data-ttu-id="7e1fd-134">Noteer de waarde van `publicIpAddress` nadat u myVM2 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-134">Note the value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="7e1fd-135">Open de TCP-poort voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="7e1fd-135">Open the TCP port for connectivity</span></span>

<span data-ttu-id="7e1fd-136">Deze stap configureert u externe eindpunten die externe toegang tot de Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-136">This step configures external endpoints, which allow remote access to the Oracle database.</span></span>

<span data-ttu-id="7e1fd-137">Open de poort voor myVM1:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-137">Open the port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="7e1fd-138">Het resultaat moet er ongeveer als het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-138">The result should look similar to the following response:</span></span>

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

<span data-ttu-id="7e1fd-139">Open de poort voor myVM2:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-139">Open the port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="7e1fd-140">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="7e1fd-140">Connect to the virtual machine</span></span>

<span data-ttu-id="7e1fd-141">Gebruik de volgende opdracht om een SSH-sessie te starten voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-141">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="7e1fd-142">Vervang de IP-adres met de `publicIpAddress` waarde voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-142">Replace the IP address with the `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-the-database-on-myvm1-primary"></a><span data-ttu-id="7e1fd-143">De database maken op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-143">Create the database on myVM1 (primary)</span></span>

<span data-ttu-id="7e1fd-144">De Oracle-software is al geïnstalleerd op de Marketplace-installatiekopie, zodat de volgende stap is het installeren van de database.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-144">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> 

<span data-ttu-id="7e1fd-145">Overschakelen naar de Oracle-beheerder:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-145">Switch to the Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="7e1fd-146">De database maken:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-146">Create the database:</span></span>

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
<span data-ttu-id="7e1fd-147">Uitvoer moeten er ongeveer als het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-147">Outputs should look similar to the following response:</span></span>

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
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="7e1fd-148">De variabelen ORACLE_SID en ORACLE_HOME instellen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-148">Set the ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="7e1fd-149">Eventueel, kunt u toevoegen ORACLE_HOME en ORACLE_SID naar het bestand /home/oracle/.bashrc, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-149">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="7e1fd-150">Bescherming van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="7e1fd-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="7e1fd-151">Bij myVM1 (primaire) archief logboek-modus inschakelen</span><span class="sxs-lookup"><span data-stu-id="7e1fd-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="7e1fd-152">Force logboekregistratie inschakelen en zorg ervoor dat ten minste één logboekbestand aanwezig is:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="7e1fd-153">Stand-by opnieuw logboeken maken:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="7e1fd-154">Flashback (waardoor herstel veel eenvoudiger) inschakelen en stand-by ingesteld\_bestand\_MANAGEMENT automatisch.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT to auto.</span></span> <span data-ttu-id="7e1fd-155">Afsluiten van SQL * Plus daarna.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="7e1fd-156">Instellen van de service op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="7e1fd-157">Bewerk of het bestand tnsnames.ora, dat zich in de map $ORACLE_HOME\network\admin bevindt maken.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-157">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="7e1fd-158">De volgende vermeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-158">Add the following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="7e1fd-159">Bewerk of het bestand listener.ora, dat zich in de map $ORACLE_HOME\network\admin bevindt maken.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-159">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="7e1fd-160">De volgende vermeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-160">Add the following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="7e1fd-161">Schakel Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="7e1fd-162">De listener starten:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-162">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="7e1fd-163">Instellen van de service op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="7e1fd-164">SSH kunt uitvoeren naar myVM2:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-164">SSH to myVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="7e1fd-165">Meld u aan als Oracle:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="7e1fd-166">Bewerk of het bestand tnsnames.ora, dat zich in de map $ORACLE_HOME\network\admin bevindt maken.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-166">Edit or create the tnsnames.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="7e1fd-167">De volgende vermeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-167">Add the following entries:</span></span>

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

<span data-ttu-id="7e1fd-168">Bewerk of het bestand listener.ora, dat zich in de map $ORACLE_HOME\network\admin bevindt maken.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-168">Edit or create the listener.ora file, which is in the $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="7e1fd-169">De volgende vermeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-169">Add the following entries:</span></span>

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

<span data-ttu-id="7e1fd-170">De listener starten:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-170">Start the listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-the-database-to-myvm2-standby"></a><span data-ttu-id="7e1fd-171">Herstel de database naar myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-171">Restore the database to myVM2 (standby)</span></span>

<span data-ttu-id="7e1fd-172">De parameter bestand /tmp/initcdb1_stby.ora maken met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-172">Create the parameter file /tmp/initcdb1_stby.ora with the following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="7e1fd-173">Mappen maken:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="7e1fd-174">Maak een wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="7e1fd-175">Start de database op myVM2:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-175">Start the database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="7e1fd-176">De database herstellen met het hulpprogramma RMAN:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-176">Restore the database by using the RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="7e1fd-177">Voer de volgende opdrachten in RMAN:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-177">Run the following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="7e1fd-178">U ziet de volgende strekking weergegeven als de opdracht is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-178">You should see messages similar to the following when the command is completed.</span></span> <span data-ttu-id="7e1fd-179">RMAN af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="7e1fd-180">Eventueel, kunt u toevoegen ORACLE_HOME en ORACLE_SID naar het bestand /home/oracle/.bashrc, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-180">Optionally, you can add ORACLE_HOME and ORACLE_SID to the /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="7e1fd-181">Schakel Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="7e1fd-182">Data Guard Broker configureren op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="7e1fd-183">Data Guard Manager start en aanmelden met SYS en een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="7e1fd-184">(Gebruik geen OS-verificatie.) Het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-184">(Do not use OS authentication.) Perform the following:</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="7e1fd-185">Controleer de configuratie:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-185">Review the configuration:</span></span>
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

<span data-ttu-id="7e1fd-186">U kunt de installatie van de Oracle Data Guard hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-186">You've completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="7e1fd-187">De volgende sectie leest u hoe de connectiviteit testen en overschakelen via.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-187">The next section shows you how to test the connectivity and switch over.</span></span>

### <a name="connect-the-database-from-the-client-machine"></a><span data-ttu-id="7e1fd-188">Verbinding maken met de database van de clientcomputer</span><span class="sxs-lookup"><span data-stu-id="7e1fd-188">Connect the database from the client machine</span></span>

<span data-ttu-id="7e1fd-189">Bijwerken of maken van het bestand tnsnames.ora op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-189">Update or create the tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="7e1fd-190">Dit bestand bevindt zich doorgaans in $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="7e1fd-191">Vervang de IP-adressen met uw `publicIpAddress` waarden voor myVM1 en myVM2:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-191">Replace the IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

<span data-ttu-id="7e1fd-192">Start SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-the-data-guard-configuration"></a><span data-ttu-id="7e1fd-193">Test de configuratie van Data Guard</span><span class="sxs-lookup"><span data-stu-id="7e1fd-193">Test the Data Guard configuration</span></span>

### <a name="switch-over-the-database-on-myvm1-primary"></a><span data-ttu-id="7e1fd-194">Overschakelen op de database op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-194">Switch over the database on myVM1 (primary)</span></span>

<span data-ttu-id="7e1fd-195">Overschakelen van primaire naar de stand-by (cdb1 naar cdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="7e1fd-195">To switch from primary to standby (cdb1 to cdb1_stby):</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="7e1fd-196">U kunt nu verbinding naar de stand-by-database.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-196">You can now connect to the standby database.</span></span>

<span data-ttu-id="7e1fd-197">Start SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-the-database-on-myvm2-standby"></a><span data-ttu-id="7e1fd-198">Overschakelen op de database op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="7e1fd-198">Switch over the database on myVM2 (standby)</span></span>

<span data-ttu-id="7e1fd-199">Als u wilt overschakelen, voer het volgende op myVM2:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-199">To switch over, run the following on myVM2:</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="7e1fd-200">Nogmaals: nu moet u verbinding maken met de primaire database.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-200">Once again, you should now be able to connect to the primary database.</span></span>

<span data-ttu-id="7e1fd-201">Start SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="7e1fd-202">U hebt de installatie en configuratie van Data Guard op Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="7e1fd-202">You've finished the installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-the-virtual-machine"></a><span data-ttu-id="7e1fd-203">Verwijder de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="7e1fd-203">Delete the virtual machine</span></span>

<span data-ttu-id="7e1fd-204">Wanneer u de virtuele machine niet meer nodig hebt, kunt u de volgende opdracht om de resourcegroep, VM en alle gerelateerde resources te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="7e1fd-204">When you no longer need the VM, you can use the following command to remove the resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="7e1fd-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e1fd-205">Next steps</span></span>

[<span data-ttu-id="7e1fd-206">Zelfstudie: Maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="7e1fd-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="7e1fd-207">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="7e1fd-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)

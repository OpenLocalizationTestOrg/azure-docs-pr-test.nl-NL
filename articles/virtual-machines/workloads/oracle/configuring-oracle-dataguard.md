---
title: Oracle Data Guard op Azure Linux VM implementeren | Microsoft Docs
description: Snel gebruiksklaar een Oracle Data Guard omhoog in uw Azure-omgeving.
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
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="52dc7-103">Oracle Data Guard implementeren op Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="52dc7-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="52dc7-104">De Azure CLI wordt gebruikt voor het maken en beheren van Azure-resources vanaf de opdrachtregel of in scripts.</span><span class="sxs-lookup"><span data-stu-id="52dc7-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="52dc7-105">Deze handleiding details met de Azure CLI voor het implementeren van een Oracle 12c Database vanuit de galerie Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="52dc7-105">This guide details using the Azure CLI to deploy an Oracle 12c Database from the Marketplace gallery image.</span></span> <span data-ttu-id="52dc7-106">Zodra de Oracle-database is gemaakt, leest in dit document u stapsgewijs hoe installeren en configureren van Data Guard op Azure VM.</span><span class="sxs-lookup"><span data-stu-id="52dc7-106">Once the Oracle database is created, this document shows you step-by-step how to install and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="52dc7-107">Voordat u begint, moet u controleren of de Azure-CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="52dc7-107">Before you start, make sure that the Azure CLI has been installed.</span></span> <span data-ttu-id="52dc7-108">Zie voor meer informatie de [Installatiehandleiding van de Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52dc7-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="52dc7-109">De omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="52dc7-109">Prepare the environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="52dc7-110">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="52dc7-110">Assumptions</span></span>

<span data-ttu-id="52dc7-111">Als u wilt de installatie van de Oracle Data Guard uitvoeren, moet u twee virtuele Azure-machines op dezelfde beschikbaarheidsset maken.</span><span class="sxs-lookup"><span data-stu-id="52dc7-111">To perform the Oracle Data Guard install, you need to create two Azure VMs on the same availability set.</span></span> <span data-ttu-id="52dc7-112">De Marketplace-installatiekopie die u kunt maken van de virtuele machines is ' Oracle: Oracle-Database-Ee:12.1.0.2:latest '.</span><span class="sxs-lookup"><span data-stu-id="52dc7-112">The Marketplace image you use to create the VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="52dc7-113">De primaire virtuele machine (myVM1) heeft een actief Oracle-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="52dc7-113">The primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="52dc7-114">De stand-by VM (myVM2) heeft de Oracle-software alleen worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="52dc7-114">The standby VM (myVM2) has the Oracle software installed only.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="52dc7-115">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="52dc7-115">Log in to Azure</span></span> 

<span data-ttu-id="52dc7-116">Meld u aan bij uw Azure-abonnement met de opdracht [az login](/cli/azure/#login) en volg de instructies op het scherm.</span><span class="sxs-lookup"><span data-stu-id="52dc7-116">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="52dc7-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-117">Create a resource group</span></span>

<span data-ttu-id="52dc7-118">Een resourcegroep maken met de opdracht [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="52dc7-118">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="52dc7-119">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="52dc7-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="52dc7-120">In het volgende voorbeeld wordt een resourcegroep met de naam `myResourceGroup` gemaakt op de locatie `westus`.</span><span class="sxs-lookup"><span data-stu-id="52dc7-120">The following example creates a resource group named `myResourceGroup` in the `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="52dc7-121">Beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-121">Create availability set</span></span>

<span data-ttu-id="52dc7-122">Deze stap is optioneel, maar wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="52dc7-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="52dc7-123">Zie [Azure handleiding voor beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="52dc7-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="52dc7-124">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-124">Create virtual machine</span></span>

<span data-ttu-id="52dc7-125">Maak een VM met de opdracht [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="52dc7-125">Create a VM with the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="52dc7-126">Het volgende voorbeeld maakt 2 virtuele machines met de naam `myVM1` en `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="52dc7-126">The following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="52dc7-127">SSH-sleutels gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="52dc7-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="52dc7-128">Als u een specifieke set sleutels wilt gebruiken, gebruikt u de optie `--ssh-key-value`.</span><span class="sxs-lookup"><span data-stu-id="52dc7-128">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>

<span data-ttu-id="52dc7-129">MyVM1 (primaire) maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="52dc7-130">Wanneer de virtuele machine is gemaakt, de Azure CLI geeft informatie weer zoals in het volgende voorbeeld: nemen notitie van de `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="52dc7-130">Once the VM has been created, the Azure CLI shows information similar to the following example: Take note of the `publicIpAddress`.</span></span> <span data-ttu-id="52dc7-131">Dit adres wordt gebruikt voor toegang tot de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="52dc7-131">This address is used to access the VM.</span></span>

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

<span data-ttu-id="52dc7-132">MyVM2 maken (stand-by)</span><span class="sxs-lookup"><span data-stu-id="52dc7-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="52dc7-133">Noteer de `publicIpAddress` ook eens het is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="52dc7-133">Take note of the `publicIpAddress` as well once it created.</span></span>

### <a name="open-the-tcp-port-for-connectivity"></a><span data-ttu-id="52dc7-134">Open de TCP-poort voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="52dc7-134">Open the TCP port for connectivity</span></span>

<span data-ttu-id="52dc7-135">De stap is het configureren van externe eindpunten, waarmee externe toegang tot de Oracle-database, u de volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="52dc7-135">The step is to configure external endpoints, which allows accessing the Oracle DB remotely, you execute the following command.</span></span>

<span data-ttu-id="52dc7-136">Open poort voor myVM1</span><span class="sxs-lookup"><span data-stu-id="52dc7-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="52dc7-137">Resultaat moet er ongeveer als het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="52dc7-137">Result should look similar to the following response:</span></span>

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

<span data-ttu-id="52dc7-138">Open poort voor myVM2</span><span class="sxs-lookup"><span data-stu-id="52dc7-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a><span data-ttu-id="52dc7-139">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="52dc7-139">Connect to virtual machine</span></span>

<span data-ttu-id="52dc7-140">Gebruik de volgende opdracht om een SSH-sessie te starten voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="52dc7-140">Use the following command to create an SSH session with the virtual machine.</span></span> <span data-ttu-id="52dc7-141">Vervang het IP-adres door het `publicIpAddress` van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="52dc7-141">Replace the IP address with the `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="52dc7-142">Database maken op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="52dc7-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="52dc7-143">De Oracle-software is al geïnstalleerd op de Marketplace-installatiekopie, zodat de volgende stap is het installeren van de database.</span><span class="sxs-lookup"><span data-stu-id="52dc7-143">The Oracle software is already installed on the Marketplace image, so the next step is to install the database.</span></span> <span data-ttu-id="52dc7-144">de eerste stap wordt uitgevoerd als supergebruiker 'oracle'.</span><span class="sxs-lookup"><span data-stu-id="52dc7-144">the first step is running as the 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="52dc7-145">De database maken:</span><span class="sxs-lookup"><span data-stu-id="52dc7-145">create the database:</span></span>

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
<span data-ttu-id="52dc7-146">Uitvoer moeten er ongeveer als het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="52dc7-146">Outputs should look similar to the following response:</span></span>

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

<span data-ttu-id="52dc7-147">De variabelen ORACLE_SID en ORACLE_HOME instellen</span><span class="sxs-lookup"><span data-stu-id="52dc7-147">Set the ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="52dc7-148">Desgewenst kunt u ORACLE_HOME en ORACLE_SID zijn toegevoegd aan het bestand .bashrc zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="52dc7-148">Optionally, You can added ORACLE_HOME and ORACLE_SID to the .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="52dc7-149">Data Guard-configuraties</span><span class="sxs-lookup"><span data-stu-id="52dc7-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="52dc7-150">Bij myVM1 (primaire) archief logboek-modus inschakelen</span><span class="sxs-lookup"><span data-stu-id="52dc7-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="52dc7-151">Force logboekregistratie inschakelen en controleer of ten minste één logboekbestand aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="52dc7-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="52dc7-152">Stand-by opnieuw logboekbestanden maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="52dc7-153">Schakel Flashback (dat het herstel veel eerder gemaakt) en STANDBY_FILE_MANAGEMENT automatisch ingesteld</span><span class="sxs-lookup"><span data-stu-id="52dc7-153">Turn on Flashback (which made the recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT to auto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="52dc7-154">Service-instellingen op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="52dc7-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="52dc7-155">Het bestand tnsnames.ora zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="52dc7-155">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="52dc7-156">De volgende vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="52dc7-156">Add the following entries</span></span>

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

<span data-ttu-id="52dc7-157">Het bestand listener.ora zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="52dc7-157">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="52dc7-158">De volgende vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="52dc7-158">Add the following entries</span></span>

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

<span data-ttu-id="52dc7-159">De listener starten</span><span class="sxs-lookup"><span data-stu-id="52dc7-159">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="52dc7-160">Service-instellingen op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="52dc7-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="52dc7-161">Het bestand tnsnames.ora zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="52dc7-161">Edit or create the tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="52dc7-162">De volgende vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="52dc7-162">Add the following entries</span></span>

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

<span data-ttu-id="52dc7-163">Het bestand listener.ora zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="52dc7-163">Edit or create the listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="52dc7-164">De volgende vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="52dc7-164">Add the following entries</span></span>

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

<span data-ttu-id="52dc7-165">De listener starten</span><span class="sxs-lookup"><span data-stu-id="52dc7-165">Start the listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="52dc7-166">Schakel Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="52dc7-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a><span data-ttu-id="52dc7-167">Database herstellen naar myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="52dc7-167">Restore database to myVM2 (Standby)</span></span>

<span data-ttu-id="52dc7-168">Maak een parameterbestand ' / tmp/initcdb1_stby.ora' met de volgende inhoud</span><span class="sxs-lookup"><span data-stu-id="52dc7-168">Create a parameter file '/tmp/initcdb1_stby.ora' with the followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="52dc7-169">Mappen maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="52dc7-170">Wachtwoordbestand maken</span><span class="sxs-lookup"><span data-stu-id="52dc7-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="52dc7-171">Starten van de database op myVM2</span><span class="sxs-lookup"><span data-stu-id="52dc7-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="52dc7-172">Database herstellen met behulp van RMAN hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="52dc7-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="52dc7-173">Voer de volgende opdrachten in RMAN</span><span class="sxs-lookup"><span data-stu-id="52dc7-173">Execute the following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="52dc7-174">Schakel Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="52dc7-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="52dc7-175">Data Guard broker configureren op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="52dc7-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="52dc7-176">Start de Data Guard manager en aanmelden met SYS en het wachtwoord (komen niet met OS-verificatie).</span><span class="sxs-lookup"><span data-stu-id="52dc7-176">Start the Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="52dc7-177">Het volgende uitvoeren</span><span class="sxs-lookup"><span data-stu-id="52dc7-177">Perform the followings</span></span>

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

<span data-ttu-id="52dc7-178">Controleer de configuratie</span><span class="sxs-lookup"><span data-stu-id="52dc7-178">Review the configuration</span></span>
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

<span data-ttu-id="52dc7-179">Hiermee voltooid de installatie van de Oracle Data Guard.</span><span class="sxs-lookup"><span data-stu-id="52dc7-179">This completed the Oracle Data Guard setup.</span></span> <span data-ttu-id="52dc7-180">De volgende sectie ziet u hoe de connectiviteit en overschakelingen via testen</span><span class="sxs-lookup"><span data-stu-id="52dc7-180">The next section shows you how to test the connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="52dc7-181">Verbinding maken met de database van de client-computer</span><span class="sxs-lookup"><span data-stu-id="52dc7-181">Connect database from client machine</span></span>

<span data-ttu-id="52dc7-182">Bijwerken of het bestand tnsnames.ora op uw clientcomputer, die meestal zich in $ORACLE_HOME\network\admin bevindt maken.</span><span class="sxs-lookup"><span data-stu-id="52dc7-182">Update or create the tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="52dc7-183">Vervang de IP-adres met uw `publicIpAddress` voor myVM1 en myVM2</span><span class="sxs-lookup"><span data-stu-id="52dc7-183">Replace the IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="52dc7-184">Sqlplus starten</span><span class="sxs-lookup"><span data-stu-id="52dc7-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="52dc7-185">Testconfiguratie Data Guard</span><span class="sxs-lookup"><span data-stu-id="52dc7-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="52dc7-186">Overschakeling van de database op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="52dc7-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="52dc7-187">Overschakelen van primaire naar de stand-by (cdb1 naar cdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="52dc7-187">To switch from primary to standby (cdb1 to cdb1_stby)</span></span>

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

<span data-ttu-id="52dc7-188">U moet nu verbinding maken met de stand-by-database</span><span class="sxs-lookup"><span data-stu-id="52dc7-188">You should now be able to connect to the standby database</span></span>

<span data-ttu-id="52dc7-189">Sqlplus starten</span><span class="sxs-lookup"><span data-stu-id="52dc7-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="52dc7-190">Database-switch terug op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="52dc7-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="52dc7-191">U schakelt terug door de volgende elementen worden uitgevoerd op myVM2</span><span class="sxs-lookup"><span data-stu-id="52dc7-191">To switch back, run the followings on myVM2</span></span>
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

<span data-ttu-id="52dc7-192">Nogmaals: nu moet u verbinding maken met de primaire database</span><span class="sxs-lookup"><span data-stu-id="52dc7-192">Once again, You should now be able to connect to the primary database</span></span>

<span data-ttu-id="52dc7-193">Sqlplus starten</span><span class="sxs-lookup"><span data-stu-id="52dc7-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="52dc7-194">Hiermee voltooid de installatie en configuratie van Data Guard op Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="52dc7-194">This completed the installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="52dc7-195">De virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="52dc7-195">Delete virtual machine</span></span>

<span data-ttu-id="52dc7-196">Wanneer de virtuele machine niet meer nodig is, kan de volgende opdracht worden gebruikt om de resourcegroep, de virtuele machine zelf en alle gerelateerde resources te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="52dc7-196">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="52dc7-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52dc7-197">Next steps</span></span>

[<span data-ttu-id="52dc7-198">Zelfstudie voor het maken van virtuele machines met een hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="52dc7-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="52dc7-199">CLI-voorbeelden voor VM-implementatie verkennen</span><span class="sxs-lookup"><span data-stu-id="52dc7-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)

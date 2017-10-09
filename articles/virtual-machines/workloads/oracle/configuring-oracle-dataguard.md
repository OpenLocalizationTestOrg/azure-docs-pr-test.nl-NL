---
title: aaaImplement Oracle Data Guard op Azure Linux VM | Microsoft Docs
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a><span data-ttu-id="14593-103">Oracle Data Guard implementeren op Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="14593-103">Implement Oracle Data Guard on Azure Linux VM</span></span> 

<span data-ttu-id="14593-104">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="14593-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="14593-105">Deze handleiding gegevens met behulp van hello Azure CLI toodeploy een Oracle 12c Database vanuit Hallo Marketplace galerie-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="14593-105">This guide details using hello Azure CLI toodeploy an Oracle 12c Database from hello Marketplace gallery image.</span></span> <span data-ttu-id="14593-106">Zodra Hallo Oracle-database is gemaakt, dit document bevat stapsgewijze hoe tooinstall en Data Guard configureren op Azure VM.</span><span class="sxs-lookup"><span data-stu-id="14593-106">Once hello Oracle database is created, this document shows you step-by-step how tooinstall and configure Data Guard on Azure VM.</span></span>

<span data-ttu-id="14593-107">Voordat u begint, controleert u dat hello die Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="14593-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="14593-108">Zie voor meer informatie de [Installatiehandleiding van de Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="14593-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="14593-109">Hallo-omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="14593-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="14593-110">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="14593-110">Assumptions</span></span>

<span data-ttu-id="14593-111">tooperform Hallo Oracle Data Guard installeren, moet u twee toocreate Azure VM's op Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="14593-111">tooperform hello Oracle Data Guard install, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="14593-112">Hallo Marketplace-installatiekopie gebruiken van toocreate Hallo virtuele machines is ' Oracle: Oracle-Database-Ee:12.1.0.2:latest '.</span><span class="sxs-lookup"><span data-stu-id="14593-112">hello Marketplace image you use toocreate hello VMs is "Oracle:Oracle-Database-Ee:12.1.0.2:latest".</span></span>

<span data-ttu-id="14593-113">Hallo heeft primaire virtuele machine (myVM1) een actief Oracle-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="14593-113">hello primary VM (myVM1) has a running Oracle instance.</span></span>

<span data-ttu-id="14593-114">Hallo die stand-by-virtuele machine (myVM2) Hallo Oracle-software alleen worden geïnstalleerd heeft.</span><span class="sxs-lookup"><span data-stu-id="14593-114">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="14593-115">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="14593-115">Log in tooAzure</span></span> 

<span data-ttu-id="14593-116">Meld u bij de Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="14593-116">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="14593-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="14593-117">Create a resource group</span></span>

<span data-ttu-id="14593-118">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="14593-118">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="14593-119">Een Azure-resourcegroep is een logische container waarin Azure-resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="14593-119">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="14593-120">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie.</span><span class="sxs-lookup"><span data-stu-id="14593-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a><span data-ttu-id="14593-121">Beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="14593-121">Create availability set</span></span>

<span data-ttu-id="14593-122">Deze stap is optioneel, maar wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="14593-122">This step is optional, but is recommended.</span></span> <span data-ttu-id="14593-123">Zie [Azure handleiding voor beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14593-123">see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) for more information.</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a><span data-ttu-id="14593-124">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="14593-124">Create virtual machine</span></span>

<span data-ttu-id="14593-125">Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="14593-125">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="14593-126">Hallo volgende voorbeeld maakt 2 virtuele machines met de naam `myVM1` en `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="14593-126">hello following example creates 2 VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="14593-127">SSH-sleutels gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="14593-127">Creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="14593-128">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="14593-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="14593-129">MyVM1 (primaire) maken</span><span class="sxs-lookup"><span data-stu-id="14593-129">Create myVM1 (primary)</span></span>
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

<span data-ttu-id="14593-130">Eenmaal Hallo VM is gemaakt, hello Azure CLI toont informatie vergelijkbare toohello voorbeeld te volgen: nemen Opmerking Hallo `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="14593-130">Once hello VM has been created, hello Azure CLI shows information similar toohello following example: Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="14593-131">Dit adres is gebruikte tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="14593-131">This address is used tooaccess hello VM.</span></span>

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

<span data-ttu-id="14593-132">MyVM2 maken (stand-by)</span><span class="sxs-lookup"><span data-stu-id="14593-132">Create myVM2 (standby)</span></span>
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

<span data-ttu-id="14593-133">Let op Hallo `publicIpAddress` ook eens het is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14593-133">Take note of hello `publicIpAddress` as well once it created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="14593-134">Open TCP-poort Hallo voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="14593-134">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="14593-135">Hallo stap tooconfigure externe eindpunten, waarmee externe toegang tot Hallo Oracle DB, u Hallo volgende opdracht uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="14593-135">hello step is tooconfigure external endpoints, which allows accessing hello Oracle DB remotely, you execute hello following command.</span></span>

<span data-ttu-id="14593-136">Open poort voor myVM1</span><span class="sxs-lookup"><span data-stu-id="14593-136">Open port for myVM1</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="14593-137">Resultaat ziet vergelijkbare toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="14593-137">Result should look similar toohello following response:</span></span>

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

<span data-ttu-id="14593-138">Open poort voor myVM2</span><span class="sxs-lookup"><span data-stu-id="14593-138">Open port for myVM2</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toovirtual-machine"></a><span data-ttu-id="14593-139">Verbinding maken met toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="14593-139">Connect toovirtual machine</span></span>

<span data-ttu-id="14593-140">Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="14593-140">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="14593-141">Hallo IP-adres vervangen door Hallo `publicIpAddress` van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="14593-141">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a><span data-ttu-id="14593-142">Database maken op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="14593-142">Create Database on myVM1 (Primary)</span></span>

<span data-ttu-id="14593-143">Hallo Oracle-software is al geïnstalleerd op Hallo Marketplace-installatiekopie, zodat de volgende stap Hallo tooinstall Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="14593-143">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> <span data-ttu-id="14593-144">de eerste stap Hello wordt uitgevoerd als Hallo 'oracle' supergebruiker.</span><span class="sxs-lookup"><span data-stu-id="14593-144">hello first step is running as hello 'oracle' superuser.</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="14593-145">Hallo-database maken:</span><span class="sxs-lookup"><span data-stu-id="14593-145">create hello database:</span></span>

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
<span data-ttu-id="14593-146">Uitvoer ziet er vergelijkbare toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="14593-146">Outputs should look similar toohello following response:</span></span>

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

<span data-ttu-id="14593-147">Hallo ORACLE_SID en ORACLE_HOME variabelen instellen</span><span class="sxs-lookup"><span data-stu-id="14593-147">Set hello ORACLE_SID and ORACLE_HOME variables</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="14593-148">U kunt eventueel ORACLE_HOME en ORACLE_SID toohello .bashrc bestand toegevoegd, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="14593-148">Optionally, You can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future logins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a><span data-ttu-id="14593-149">Data Guard-configuraties</span><span class="sxs-lookup"><span data-stu-id="14593-149">Data Guard Configurations</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="14593-150">Bij myVM1 (primaire) archief logboek-modus inschakelen</span><span class="sxs-lookup"><span data-stu-id="14593-150">Enable Archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="14593-151">Force logboekregistratie inschakelen en controleer of ten minste één logboekbestand aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="14593-151">Enable force logging, and make sure at least one logfile is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="14593-152">Stand-by opnieuw logboekbestanden maken</span><span class="sxs-lookup"><span data-stu-id="14593-152">Create standby redo logs</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="14593-153">Schakel Flashback (die Hallo herstel veel eerder gemaakt) en stel STANDBY_FILE_MANAGEMENT tooauto</span><span class="sxs-lookup"><span data-stu-id="14593-153">Turn on Flashback (which made hello recovery a lot earlier) and set STANDBY_FILE_MANAGEMENT tooauto</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a><span data-ttu-id="14593-154">Service-instellingen op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="14593-154">Service setup on myVM1 (primary)</span></span>

<span data-ttu-id="14593-155">Hallo tnsnames.ora bestand zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="14593-155">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="14593-156">Hallo na vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="14593-156">Add hello following entries</span></span>

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

<span data-ttu-id="14593-157">Hallo listener.ora bestand zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="14593-157">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="14593-158">Hallo na vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="14593-158">Add hello following entries</span></span>

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

<span data-ttu-id="14593-159">Hallo-listener starten</span><span class="sxs-lookup"><span data-stu-id="14593-159">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a><span data-ttu-id="14593-160">Service-instellingen op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="14593-160">Service setup on myVM2 (Standby)</span></span>

<span data-ttu-id="14593-161">Hallo tnsnames.ora bestand zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="14593-161">Edit or create hello tnsnames.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="14593-162">Hallo na vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="14593-162">Add hello following entries</span></span>

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

<span data-ttu-id="14593-163">Hallo listener.ora bestand zich in de map ORACLE_HOME\network\admin bevindt $ maken of bewerken</span><span class="sxs-lookup"><span data-stu-id="14593-163">Edit or create hello listener.ora file, which is located at $ORACLE_HOME\network\admin folder</span></span>

<span data-ttu-id="14593-164">Hallo na vermeldingen toevoegen</span><span class="sxs-lookup"><span data-stu-id="14593-164">Add hello following entries</span></span>

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

<span data-ttu-id="14593-165">Hallo-listener starten</span><span class="sxs-lookup"><span data-stu-id="14593-165">Start hello listener</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

<span data-ttu-id="14593-166">Schakel Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="14593-166">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-toomyvm2-standby"></a><span data-ttu-id="14593-167">RESTORE database toomyVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="14593-167">Restore database toomyVM2 (Standby)</span></span>

<span data-ttu-id="14593-168">Maak een parameterbestand ' / tmp/initcdb1_stby.ora' met inhoud van de volgende Hallo</span><span class="sxs-lookup"><span data-stu-id="14593-168">Create a parameter file '/tmp/initcdb1_stby.ora' with hello followings contents</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="14593-169">Mappen maken</span><span class="sxs-lookup"><span data-stu-id="14593-169">Create folders</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="14593-170">Wachtwoordbestand maken</span><span class="sxs-lookup"><span data-stu-id="14593-170">Create password file</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="14593-171">Starten van de database op myVM2</span><span class="sxs-lookup"><span data-stu-id="14593-171">Start up database on myVM2</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="14593-172">Database herstellen met behulp van RMAN hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="14593-172">Restore database using RMAN utility</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="14593-173">Uitvoeren van de volgende opdrachten in RMAN Hallo</span><span class="sxs-lookup"><span data-stu-id="14593-173">Execute hello following commands in RMAN</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="14593-174">Schakel Data Guard Broker</span><span class="sxs-lookup"><span data-stu-id="14593-174">Enable Data Guard Broker</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="14593-175">Data Guard broker configureren op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="14593-175">Configure Data Guard broker on myVM1 (primary)</span></span>

<span data-ttu-id="14593-176">Start Hallo Data Guard manager en meld u aan met SYS en het wachtwoord (komen niet met OS-verificatie).</span><span class="sxs-lookup"><span data-stu-id="14593-176">Start hello Data Guard manager and login using SYS and password (do not using OS authentication).</span></span> <span data-ttu-id="14593-177">De volgende Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="14593-177">Perform hello followings</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

<span data-ttu-id="14593-178">Hallo-configuratie controleren</span><span class="sxs-lookup"><span data-stu-id="14593-178">Review hello configuration</span></span>
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

<span data-ttu-id="14593-179">Dit Hallo Oracle Data Guard setup voltooid.</span><span class="sxs-lookup"><span data-stu-id="14593-179">This completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="14593-180">Hallo volgende sectie ziet u hoe tootest Hallo connectiviteit en overschakelen via</span><span class="sxs-lookup"><span data-stu-id="14593-180">hello next section shows you how tootest hello connectivity and switching over</span></span>

### <a name="connect-database-from-client-machine"></a><span data-ttu-id="14593-181">Verbinding maken met de database van de client-computer</span><span class="sxs-lookup"><span data-stu-id="14593-181">Connect database from client machine</span></span>

<span data-ttu-id="14593-182">Bijwerken of Hallo tnsnames.ora bestand op uw clientcomputer, die meestal zich in $ORACLE_HOME\network\admin bevindt maken.</span><span class="sxs-lookup"><span data-stu-id="14593-182">Update or create hello tnsnames.ora file on your client machine which usually is located at $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="14593-183">Vervang Hallo IP-adres met uw `publicIpAddress` voor myVM1 en myVM2</span><span class="sxs-lookup"><span data-stu-id="14593-183">Replace hello IP with your `publicIpAddress` for myVM1 and myVM2</span></span>

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

<span data-ttu-id="14593-184">Sqlplus starten</span><span class="sxs-lookup"><span data-stu-id="14593-184">Start sqlplus</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a><span data-ttu-id="14593-185">Testconfiguratie Data Guard</span><span class="sxs-lookup"><span data-stu-id="14593-185">Test Data Guard configuration</span></span>

### <a name="database-switchover-on-myvm1-primary"></a><span data-ttu-id="14593-186">Overschakeling van de database op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="14593-186">Database switchover on myVM1 (primary)</span></span>

<span data-ttu-id="14593-187">tooswitch van primaire toostandby (cdb1 toocdb1_stby)</span><span class="sxs-lookup"><span data-stu-id="14593-187">tooswitch from primary toostandby (cdb1 toocdb1_stby)</span></span>

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

<span data-ttu-id="14593-188">Nu moet u kunnen tooconnect toohello stand-by-database</span><span class="sxs-lookup"><span data-stu-id="14593-188">You should now be able tooconnect toohello standby database</span></span>

<span data-ttu-id="14593-189">Sqlplus starten</span><span class="sxs-lookup"><span data-stu-id="14593-189">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a><span data-ttu-id="14593-190">Database-switch terug op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="14593-190">Database switch back on myVM2 (standby)</span></span>

<span data-ttu-id="14593-191">tooswitch terug, Hallo volgende uitvoeren op myVM2</span><span class="sxs-lookup"><span data-stu-id="14593-191">tooswitch back, run hello followings on myVM2</span></span>
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

<span data-ttu-id="14593-192">Nogmaals: nu moet u kunnen tooconnect toohello primaire database</span><span class="sxs-lookup"><span data-stu-id="14593-192">Once again, You should now be able tooconnect toohello primary database</span></span>

<span data-ttu-id="14593-193">Sqlplus starten</span><span class="sxs-lookup"><span data-stu-id="14593-193">Start sqlplus</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="14593-194">Dit Hallo-installatie en configuratie van Data Guard op Oracle linux voltooid.</span><span class="sxs-lookup"><span data-stu-id="14593-194">This completed hello installation and configuration of Data Guard on Oracle linux.</span></span>


## <a name="delete-virtual-machine"></a><span data-ttu-id="14593-195">De virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="14593-195">Delete virtual machine</span></span>

<span data-ttu-id="14593-196">Wanneer deze niet langer nodig is, kan Hallo na de opdracht gebruikte tooremove hello, resourcegroep of virtuele machine, en alle bijbehorende resources.</span><span class="sxs-lookup"><span data-stu-id="14593-196">When no longer needed, hello following command can be used tooremove hello Resource Group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="14593-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14593-197">Next steps</span></span>

[<span data-ttu-id="14593-198">Zelfstudie voor het maken van virtuele machines met een hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="14593-198">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="14593-199">CLI-voorbeelden voor VM-implementatie verkennen</span><span class="sxs-lookup"><span data-stu-id="14593-199">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)

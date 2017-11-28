---
title: aaaImplement Oracle Data Guard op een virtuele machine van Azure Linux | Microsoft Docs
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
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="f84e0-103">Oracle Data Guard implementeren op een virtuele machine van Azure Linux</span><span class="sxs-lookup"><span data-stu-id="f84e0-103">Implement Oracle Data Guard on an Azure Linux virtual machine</span></span> 

<span data-ttu-id="f84e0-104">Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="f84e0-104">Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="f84e0-105">Dit artikel wordt beschreven hoe toouse Azure CLI toodeploy een Oracle-Database 12c-database vanuit hello Azure Marketplace-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f84e0-105">This article describes how toouse Azure CLI toodeploy an Oracle Database 12c database from hello Azure Marketplace image.</span></span> <span data-ttu-id="f84e0-106">In dit artikel geeft vervolgens u stapsgewijs hoe tooinstall en Data Guard configureren op Azure een virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="f84e0-106">This article then shows you, step by step, how tooinstall and configure Data Guard on an Azure virtual machine (VM).</span></span>

<span data-ttu-id="f84e0-107">Voordat u begint, zorg ervoor dat de Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f84e0-107">Before you start, make sure that Azure CLI is installed.</span></span> <span data-ttu-id="f84e0-108">Zie voor meer informatie, Hallo [Azure CLI installatiehandleiding](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f84e0-108">For more information, see hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="f84e0-109">Hallo-omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f84e0-109">Prepare hello environment</span></span>
### <a name="assumptions"></a><span data-ttu-id="f84e0-110">Veronderstellingen</span><span class="sxs-lookup"><span data-stu-id="f84e0-110">Assumptions</span></span>

<span data-ttu-id="f84e0-111">tooinstall Oracle Data Guard, moet u twee toocreate Azure VM's op Hallo dezelfde beschikbaarheidsset:</span><span class="sxs-lookup"><span data-stu-id="f84e0-111">tooinstall Oracle Data Guard, you need toocreate two Azure VMs on hello same availability set:</span></span>

- <span data-ttu-id="f84e0-112">Hallo heeft primaire virtuele machine (myVM1) een actief Oracle-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="f84e0-112">hello primary VM (myVM1) has a running Oracle instance.</span></span>
- <span data-ttu-id="f84e0-113">Hallo die stand-by-virtuele machine (myVM2) Hallo Oracle-software alleen worden geïnstalleerd heeft.</span><span class="sxs-lookup"><span data-stu-id="f84e0-113">hello standby VM (myVM2) has hello Oracle software installed only.</span></span>

<span data-ttu-id="f84e0-114">Hallo Marketplace-installatiekopie toocreate Hallo virtuele machines te gebruiken is Oracle: Oracle-Database-Ee:12.1.0.2:latest.</span><span class="sxs-lookup"><span data-stu-id="f84e0-114">hello Marketplace image that you use toocreate hello VMs is Oracle:Oracle-Database-Ee:12.1.0.2:latest.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="f84e0-115">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="f84e0-115">Sign in tooAzure</span></span> 

<span data-ttu-id="f84e0-116">Azure-abonnement tooyour aanmelden via Hallo [az aanmelding](/cli/azure/#login) opdracht in en volg Hallo op het scherm instructies.</span><span class="sxs-lookup"><span data-stu-id="f84e0-116">Sign in tooyour Azure subscription by using hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f84e0-117">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f84e0-117">Create a resource group</span></span>

<span data-ttu-id="f84e0-118">Een resourcegroep maken met behulp van Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f84e0-118">Create a resource group by using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f84e0-119">Een Azure-resourcegroep is een logische container in welke Azure resources worden geïmplementeerd en beheerd.</span><span class="sxs-lookup"><span data-stu-id="f84e0-119">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f84e0-120">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie:</span><span class="sxs-lookup"><span data-stu-id="f84e0-120">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="f84e0-121">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="f84e0-121">Create an availability set</span></span>

<span data-ttu-id="f84e0-122">Maken van een beschikbaarheidsset is optioneel, maar wordt u aangeraden deze.</span><span class="sxs-lookup"><span data-stu-id="f84e0-122">Creating an availability set is optional, but we recommend it.</span></span> <span data-ttu-id="f84e0-123">Zie voor meer informatie [Azure beschikbaarheidssets richtlijnen](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="f84e0-123">For more information, see [Azure availability sets guidelines](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="f84e0-124">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="f84e0-124">Create a virtual machine</span></span>

<span data-ttu-id="f84e0-125">Een virtuele machine maken met behulp van Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f84e0-125">Create a VM by using hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f84e0-126">Hallo volgende voorbeeld maakt twee virtuele machines met de naam `myVM1` en `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="f84e0-126">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="f84e0-127">SSH-sleutels wordt ook gemaakt als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="f84e0-127">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="f84e0-128">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="f84e0-128">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

<span data-ttu-id="f84e0-129">Maak myVM1 (primaire):</span><span class="sxs-lookup"><span data-stu-id="f84e0-129">Create myVM1 (primary):</span></span>
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

<span data-ttu-id="f84e0-130">Nadat u Hallo VM gemaakt, ziet u Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="f84e0-130">After you create hello VM, Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="f84e0-131">Bekijkt hello waarde `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="f84e0-131">Note hello value of `publicIpAddress`.</span></span> <span data-ttu-id="f84e0-132">U gebruikt dit adres tooaccess Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="f84e0-132">You use this address tooaccess hello VM.</span></span>

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

<span data-ttu-id="f84e0-133">MyVM2 maken (stand-by):</span><span class="sxs-lookup"><span data-stu-id="f84e0-133">Create myVM2 (standby):</span></span>
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

<span data-ttu-id="f84e0-134">Bekijkt hello waarde `publicIpAddress` nadat u myVM2 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f84e0-134">Note hello value of `publicIpAddress` after you create myVM2.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="f84e0-135">Open TCP-poort Hallo voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="f84e0-135">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="f84e0-136">Deze stap configureert u externe eindpunten waarmee RAS toohello Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="f84e0-136">This step configures external endpoints, which allow remote access toohello Oracle database.</span></span>

<span data-ttu-id="f84e0-137">Hallo-poort voor myVM1 openen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-137">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="f84e0-138">Hallo resultaat ziet vergelijkbare toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-138">hello result should look similar toohello following response:</span></span>

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

<span data-ttu-id="f84e0-139">Hallo-poort voor myVM2 openen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-139">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="f84e0-140">Verbinding maken met toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f84e0-140">Connect toohello virtual machine</span></span>

<span data-ttu-id="f84e0-141">Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f84e0-141">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="f84e0-142">Hallo IP-adres vervangen door Hallo `publicIpAddress` waarde voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f84e0-142">Replace hello IP address with hello `publicIpAddress` value for your virtual machine.</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="f84e0-143">Hallo-database maken op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="f84e0-143">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="f84e0-144">Hallo Oracle-software is al geïnstalleerd op Hallo Marketplace-installatiekopie, zodat de volgende stap Hallo tooinstall Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f84e0-144">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="f84e0-145">Switch toohello Oracle supergebruiker:</span><span class="sxs-lookup"><span data-stu-id="f84e0-145">Switch toohello Oracle superuser:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="f84e0-146">Hallo-database maken:</span><span class="sxs-lookup"><span data-stu-id="f84e0-146">Create hello database:</span></span>

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
<span data-ttu-id="f84e0-147">Uitvoer ziet er vergelijkbare toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-147">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="f84e0-148">Hallo ORACLE_SID en ORACLE_HOME variabelen worden ingesteld:</span><span class="sxs-lookup"><span data-stu-id="f84e0-148">Set hello ORACLE_SID and ORACLE_HOME variables:</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

<span data-ttu-id="f84e0-149">Desgewenst kunt u ORACLE_HOME en ORACLE_SID toohello /home/oracle/.bashrc bestand, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-149">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a><span data-ttu-id="f84e0-150">Bescherming van gegevens configureren</span><span class="sxs-lookup"><span data-stu-id="f84e0-150">Configure Data Guard</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="f84e0-151">Bij myVM1 (primaire) archief logboek-modus inschakelen</span><span class="sxs-lookup"><span data-stu-id="f84e0-151">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="f84e0-152">Force logboekregistratie inschakelen en zorg ervoor dat ten minste één logboekbestand aanwezig is:</span><span class="sxs-lookup"><span data-stu-id="f84e0-152">Enable force logging, and make sure at least one log file is present:</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

<span data-ttu-id="f84e0-153">Stand-by opnieuw logboeken maken:</span><span class="sxs-lookup"><span data-stu-id="f84e0-153">Create standby redo logs:</span></span>

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

<span data-ttu-id="f84e0-154">Flashback (waardoor herstel veel eenvoudiger) inschakelen en stand-by ingesteld\_bestand\_MANAGEMENT tooauto.</span><span class="sxs-lookup"><span data-stu-id="f84e0-154">Turn on Flashback (which makes recovery a lot easier) and set STANDBY\_FILE\_MANAGEMENT tooauto.</span></span> <span data-ttu-id="f84e0-155">Afsluiten van SQL * Plus daarna.</span><span class="sxs-lookup"><span data-stu-id="f84e0-155">Exit SQL*Plus after that.</span></span>

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="f84e0-156">Instellen van de service op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="f84e0-156">Set up service on myVM1 (primary)</span></span>

<span data-ttu-id="f84e0-157">Bewerk of Hallo tnsnames.ora bestand maakt, dat zich in de map voor Hallo $ORACLE_HOME\network\admin bevindt.</span><span class="sxs-lookup"><span data-stu-id="f84e0-157">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f84e0-158">Hallo vermeldingen volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-158">Add hello following entries:</span></span>

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

<span data-ttu-id="f84e0-159">Bewerk of Hallo listener.ora bestand maakt, dat zich in de map voor Hallo $ORACLE_HOME\network\admin bevindt.</span><span class="sxs-lookup"><span data-stu-id="f84e0-159">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f84e0-160">Hallo vermeldingen volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-160">Add hello following entries:</span></span>

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

<span data-ttu-id="f84e0-161">Schakel Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="f84e0-161">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
<span data-ttu-id="f84e0-162">Hallo-listener starten:</span><span class="sxs-lookup"><span data-stu-id="f84e0-162">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a><span data-ttu-id="f84e0-163">Instellen van de service op myVM2 (stand-by)</span><span class="sxs-lookup"><span data-stu-id="f84e0-163">Set up service on myVM2 (standby)</span></span>

<span data-ttu-id="f84e0-164">SSH-toomyVM2:</span><span class="sxs-lookup"><span data-stu-id="f84e0-164">SSH toomyVM2:</span></span>

```bash 
$ ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="f84e0-165">Meld u aan als Oracle:</span><span class="sxs-lookup"><span data-stu-id="f84e0-165">Log in as Oracle:</span></span>

```bash
$ sudo su - oracle
```

<span data-ttu-id="f84e0-166">Bewerk of Hallo tnsnames.ora bestand maakt, dat zich in de map voor Hallo $ORACLE_HOME\network\admin bevindt.</span><span class="sxs-lookup"><span data-stu-id="f84e0-166">Edit or create hello tnsnames.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f84e0-167">Hallo vermeldingen volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-167">Add hello following entries:</span></span>

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

<span data-ttu-id="f84e0-168">Bewerk of Hallo listener.ora bestand maakt, dat zich in de map voor Hallo $ORACLE_HOME\network\admin bevindt.</span><span class="sxs-lookup"><span data-stu-id="f84e0-168">Edit or create hello listener.ora file, which is in hello $ORACLE_HOME\network\admin folder.</span></span>

<span data-ttu-id="f84e0-169">Hallo vermeldingen volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-169">Add hello following entries:</span></span>

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

<span data-ttu-id="f84e0-170">Hallo-listener starten:</span><span class="sxs-lookup"><span data-stu-id="f84e0-170">Start hello listener:</span></span>

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a><span data-ttu-id="f84e0-171">Hallo database toomyVM2 herstellen (stand-by)</span><span class="sxs-lookup"><span data-stu-id="f84e0-171">Restore hello database toomyVM2 (standby)</span></span>

<span data-ttu-id="f84e0-172">Maak Hallo parameter bestand /tmp/initcdb1_stby.ora met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="f84e0-172">Create hello parameter file /tmp/initcdb1_stby.ora with hello following contents:</span></span>
```bash
*.db_name='cdb1'
```

<span data-ttu-id="f84e0-173">Mappen maken:</span><span class="sxs-lookup"><span data-stu-id="f84e0-173">Create folders:</span></span>

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

<span data-ttu-id="f84e0-174">Maak een wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="f84e0-174">Create a password file:</span></span>

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
<span data-ttu-id="f84e0-175">Hallo-database op myVM2 starten:</span><span class="sxs-lookup"><span data-stu-id="f84e0-175">Start hello database on myVM2:</span></span>

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

<span data-ttu-id="f84e0-176">Hallo-database terugzetten met Hallo RMAN hulpprogramma:</span><span class="sxs-lookup"><span data-stu-id="f84e0-176">Restore hello database by using hello RMAN tool:</span></span>

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

<span data-ttu-id="f84e0-177">Voer Hallo opdrachten in RMAN te volgen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-177">Run hello following commands in RMAN:</span></span>
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

<span data-ttu-id="f84e0-178">U kunt berichten vergelijkbaar toohello volgende moeten zien als Hallo-opdracht is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f84e0-178">You should see messages similar toohello following when hello command is completed.</span></span> <span data-ttu-id="f84e0-179">RMAN af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="f84e0-179">Exit RMAN.</span></span>
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

<span data-ttu-id="f84e0-180">Desgewenst kunt u ORACLE_HOME en ORACLE_SID toohello /home/oracle/.bashrc bestand, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f84e0-180">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello /home/oracle/.bashrc file, so that these settings are saved for future logins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

<span data-ttu-id="f84e0-181">Schakel Data Guard Broker:</span><span class="sxs-lookup"><span data-stu-id="f84e0-181">Enable Data Guard Broker:</span></span>
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a><span data-ttu-id="f84e0-182">Data Guard Broker configureren op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="f84e0-182">Configure Data Guard Broker on myVM1 (primary)</span></span>

<span data-ttu-id="f84e0-183">Data Guard Manager start en aanmelden met SYS en een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f84e0-183">Start Data Guard Manager and log in by using SYS and a password.</span></span> <span data-ttu-id="f84e0-184">(Gebruik geen OS-verificatie.) Voer de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="f84e0-184">(Do not use OS authentication.) Perform hello following:</span></span>

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

<span data-ttu-id="f84e0-185">Hallo-configuratie controleren:</span><span class="sxs-lookup"><span data-stu-id="f84e0-185">Review hello configuration:</span></span>
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

<span data-ttu-id="f84e0-186">U kunt Hallo Oracle Data Guard installatie hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="f84e0-186">You've completed hello Oracle Data Guard setup.</span></span> <span data-ttu-id="f84e0-187">de volgende sectie Hallo ziet u hoe tootest Hallo connectiviteit en overgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="f84e0-187">hello next section shows you how tootest hello connectivity and switch over.</span></span>

### <a name="connect-hello-database-from-hello-client-machine"></a><span data-ttu-id="f84e0-188">Verbinding maken met Hallo database vanaf de clientcomputer Hallo</span><span class="sxs-lookup"><span data-stu-id="f84e0-188">Connect hello database from hello client machine</span></span>

<span data-ttu-id="f84e0-189">Bijwerken of maak Hallo tnsnames.ora bestand op de clientcomputer.</span><span class="sxs-lookup"><span data-stu-id="f84e0-189">Update or create hello tnsnames.ora file on your client machine.</span></span> <span data-ttu-id="f84e0-190">Dit bestand bevindt zich doorgaans in $ORACLE_HOME\network\admin.</span><span class="sxs-lookup"><span data-stu-id="f84e0-190">This file is usually in $ORACLE_HOME\network\admin.</span></span>

<span data-ttu-id="f84e0-191">Vervang Hallo IP-adressen met uw `publicIpAddress` waarden voor myVM1 en myVM2:</span><span class="sxs-lookup"><span data-stu-id="f84e0-191">Replace hello IP addresses with your `publicIpAddress` values for myVM1 and myVM2:</span></span>

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

<span data-ttu-id="f84e0-192">Start SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="f84e0-192">Start SQL*Plus:</span></span>

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a><span data-ttu-id="f84e0-193">Testconfiguratie Hallo Data Guard</span><span class="sxs-lookup"><span data-stu-id="f84e0-193">Test hello Data Guard configuration</span></span>

### <a name="switch-over-hello-database-on-myvm1-primary"></a><span data-ttu-id="f84e0-194">Schakel Hallo-database op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="f84e0-194">Switch over hello database on myVM1 (primary)</span></span>

<span data-ttu-id="f84e0-195">tooswitch van primaire toostandby (cdb1 toocdb1_stby):</span><span class="sxs-lookup"><span data-stu-id="f84e0-195">tooswitch from primary toostandby (cdb1 toocdb1_stby):</span></span>

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

<span data-ttu-id="f84e0-196">U kunt nu verbinding toohello stand-by-database.</span><span class="sxs-lookup"><span data-stu-id="f84e0-196">You can now connect toohello standby database.</span></span>

<span data-ttu-id="f84e0-197">Start SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="f84e0-197">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a><span data-ttu-id="f84e0-198">Hallo-database op myVM2 overschakelen (stand-by)</span><span class="sxs-lookup"><span data-stu-id="f84e0-198">Switch over hello database on myVM2 (standby)</span></span>

<span data-ttu-id="f84e0-199">Hallo volgende tooswitch via, uitvoeren op myVM2:</span><span class="sxs-lookup"><span data-stu-id="f84e0-199">tooswitch over, run hello following on myVM2:</span></span>
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

<span data-ttu-id="f84e0-200">Nogmaals: u moet nu kunnen tooconnect toohello primaire database.</span><span class="sxs-lookup"><span data-stu-id="f84e0-200">Once again, you should now be able tooconnect toohello primary database.</span></span>

<span data-ttu-id="f84e0-201">Start SQL * Plus:</span><span class="sxs-lookup"><span data-stu-id="f84e0-201">Start SQL*Plus:</span></span>

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

<span data-ttu-id="f84e0-202">U klaar bent met het Hallo-installatie en configuratie van Data Guard op Oracle Linux.</span><span class="sxs-lookup"><span data-stu-id="f84e0-202">You've finished hello installation and configuration of Data Guard on Oracle Linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="f84e0-203">Hallo virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="f84e0-203">Delete hello virtual machine</span></span>

<span data-ttu-id="f84e0-204">Wanneer u virtuele machine niet meer nodig hello, kunt u na de opdracht tooremove Hallo-resourcegroep, VM en alle gerelateerde resources hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f84e0-204">When you no longer need hello VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f84e0-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f84e0-205">Next steps</span></span>

[<span data-ttu-id="f84e0-206">Zelfstudie: Maximaal beschikbare virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="f84e0-206">Tutorial: Create highly available virtual machines</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="f84e0-207">VM-implementatie Azure CLI voorbeelden verkennen</span><span class="sxs-lookup"><span data-stu-id="f84e0-207">Explore VM deployment Azure CLI samples</span></span>](../../linux/cli-samples.md)

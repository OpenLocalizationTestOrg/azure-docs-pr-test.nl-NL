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
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a><span data-ttu-id="f4f39-103">Oracle Golden Gate implementeren op een Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="f4f39-103">Implement Oracle Golden Gate on an Azure Linux VM</span></span> 

<span data-ttu-id="f4f39-104">Hello Azure CLI is gebruikte toocreate en Azure-resources te beheren vanaf de opdrachtregel hello, hetzij in scripts.</span><span class="sxs-lookup"><span data-stu-id="f4f39-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="f4f39-105">Deze handleiding details hoe toouse hello Azure CLI toodeploy een Oracle-12-c-database van de afbeelding hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="f4f39-105">This guide details how toouse hello Azure CLI toodeploy an Oracle 12c database from hello Azure Marketplace gallery image.</span></span> 

<span data-ttu-id="f4f39-106">Dit document toont stapsgewijs hoe toocreate, installeren en configureren van Oracle Golden Gate op een Azure VM.</span><span class="sxs-lookup"><span data-stu-id="f4f39-106">This document shows you step-by-step how toocreate, install, and configure Oracle Golden Gate on an Azure VM.</span></span>

<span data-ttu-id="f4f39-107">Voordat u begint, controleert u dat hello die Azure CLI is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f4f39-107">Before you start, make sure that hello Azure CLI has been installed.</span></span> <span data-ttu-id="f4f39-108">Zie voor meer informatie de [Installatiehandleiding van de Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f4f39-108">For more information, see [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>

## <a name="prepare-hello-environment"></a><span data-ttu-id="f4f39-109">Hallo-omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="f4f39-109">Prepare hello environment</span></span>

<span data-ttu-id="f4f39-110">tooperform hello Oracle Golden Gate installatie, moet u twee toocreate Azure VM's op Hallo dezelfde beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="f4f39-110">tooperform hello Oracle Golden Gate installation, you need toocreate two Azure VMs on hello same availability set.</span></span> <span data-ttu-id="f4f39-111">Hallo Marketplace-installatiekopie gebruiken van toocreate Hallo virtuele machines is **Oracle: Oracle-Database-Ee:12.1.0.2:latest**.</span><span class="sxs-lookup"><span data-stu-id="f4f39-111">hello Marketplace image you use toocreate hello VMs is **Oracle:Oracle-Database-Ee:12.1.0.2:latest**.</span></span>

<span data-ttu-id="f4f39-112">U ook toobe bekend bent met Unix-editor vi nodig hebt en basiskennis van x11 (Windows X).</span><span class="sxs-lookup"><span data-stu-id="f4f39-112">You also need toobe familiar with Unix editor vi and have a basic understanding of x11 (X Windows).</span></span>

<span data-ttu-id="f4f39-113">Hallo Hier volgt een samenvatting van configuratie van Hallo-omgeving:</span><span class="sxs-lookup"><span data-stu-id="f4f39-113">hello following is a summary of hello environment configuration:</span></span>
> 
> |  | <span data-ttu-id="f4f39-114">**Primaire site**</span><span class="sxs-lookup"><span data-stu-id="f4f39-114">**Primary site**</span></span> | <span data-ttu-id="f4f39-115">**Replicatie van site**</span><span class="sxs-lookup"><span data-stu-id="f4f39-115">**Replicate site**</span></span> |
> | --- | --- | --- |
> | <span data-ttu-id="f4f39-116">**Oracle-release**</span><span class="sxs-lookup"><span data-stu-id="f4f39-116">**Oracle release**</span></span> |<span data-ttu-id="f4f39-117">Oracle 12c versie 2: (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="f4f39-117">Oracle 12c Release 2 – (12.1.0.2)</span></span> |<span data-ttu-id="f4f39-118">Oracle 12c versie 2: (12.1.0.2)</span><span class="sxs-lookup"><span data-stu-id="f4f39-118">Oracle 12c Release 2 – (12.1.0.2)</span></span>|
> | <span data-ttu-id="f4f39-119">**Computernaam**</span><span class="sxs-lookup"><span data-stu-id="f4f39-119">**Machine name**</span></span> |<span data-ttu-id="f4f39-120">myVM1</span><span class="sxs-lookup"><span data-stu-id="f4f39-120">myVM1</span></span> |<span data-ttu-id="f4f39-121">myVM2</span><span class="sxs-lookup"><span data-stu-id="f4f39-121">myVM2</span></span> |
> | <span data-ttu-id="f4f39-122">**Besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="f4f39-122">**Operating system**</span></span> |<span data-ttu-id="f4f39-123">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="f4f39-123">Oracle Linux 6.x</span></span> |<span data-ttu-id="f4f39-124">Oracle Linux 6.x</span><span class="sxs-lookup"><span data-stu-id="f4f39-124">Oracle Linux 6.x</span></span> |
> | <span data-ttu-id="f4f39-125">**Oracle-SID**</span><span class="sxs-lookup"><span data-stu-id="f4f39-125">**Oracle SID**</span></span> |<span data-ttu-id="f4f39-126">CDB1</span><span class="sxs-lookup"><span data-stu-id="f4f39-126">CDB1</span></span> |<span data-ttu-id="f4f39-127">CDB1</span><span class="sxs-lookup"><span data-stu-id="f4f39-127">CDB1</span></span> |
> | <span data-ttu-id="f4f39-128">**Schema voor replicatie**</span><span class="sxs-lookup"><span data-stu-id="f4f39-128">**Replication schema**</span></span> |<span data-ttu-id="f4f39-129">TEST</span><span class="sxs-lookup"><span data-stu-id="f4f39-129">TEST</span></span>|<span data-ttu-id="f4f39-130">TEST</span><span class="sxs-lookup"><span data-stu-id="f4f39-130">TEST</span></span> |
> | <span data-ttu-id="f4f39-131">**Golden Gate eigenaar/repliceren**</span><span class="sxs-lookup"><span data-stu-id="f4f39-131">**Golden Gate owner/replicate**</span></span> |<span data-ttu-id="f4f39-132">C ##GGADMIN</span><span class="sxs-lookup"><span data-stu-id="f4f39-132">C##GGADMIN</span></span> |<span data-ttu-id="f4f39-133">REPUSER</span><span class="sxs-lookup"><span data-stu-id="f4f39-133">REPUSER</span></span> |
> | <span data-ttu-id="f4f39-134">**Golden Gate-proces**</span><span class="sxs-lookup"><span data-stu-id="f4f39-134">**Golden Gate process**</span></span> |<span data-ttu-id="f4f39-135">EXTORA</span><span class="sxs-lookup"><span data-stu-id="f4f39-135">EXTORA</span></span> |<span data-ttu-id="f4f39-136">REPORA</span><span class="sxs-lookup"><span data-stu-id="f4f39-136">REPORA</span></span>|


### <a name="sign-in-tooazure"></a><span data-ttu-id="f4f39-137">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="f4f39-137">Sign in tooAzure</span></span> 

<span data-ttu-id="f4f39-138">Meld u aan Azure-abonnement met Hallo tooyour [az aanmelding](/cli/azure/#login) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f4f39-138">Sign in tooyour Azure subscription with hello [az login](/cli/azure/#login) command.</span></span> <span data-ttu-id="f4f39-139">Volg Hallo op het scherm richtingen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-139">Then follow hello on-screen directions.</span></span>

```azurecli
az login
```

### <a name="create-a-resource-group"></a><span data-ttu-id="f4f39-140">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="f4f39-140">Create a resource group</span></span>

<span data-ttu-id="f4f39-141">Een resourcegroep maken met de Hallo [az groep maken](/cli/azure/group#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f4f39-141">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="f4f39-142">Een Azure-resourcegroep is een logische container in welke Azure-resources zijn geïmplementeerd en die ze kunnen worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="f4f39-142">An Azure resource group is a logical container into which Azure resources are deployed and from which they can be managed.</span></span> 

<span data-ttu-id="f4f39-143">Hallo volgende voorbeeld maakt u een resourcegroep met de naam `myResourceGroup` in Hallo `westus` locatie.</span><span class="sxs-lookup"><span data-stu-id="f4f39-143">hello following example creates a resource group named `myResourceGroup` in hello `westus` location.</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a><span data-ttu-id="f4f39-144">Een beschikbaarheidsset maken</span><span class="sxs-lookup"><span data-stu-id="f4f39-144">Create an availability set</span></span>

<span data-ttu-id="f4f39-145">Hallo stap is optioneel maar aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-145">hello following step is optional but recommended.</span></span> <span data-ttu-id="f4f39-146">Zie voor meer informatie [Azure handleiding voor beschikbaarheidssets](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span><span class="sxs-lookup"><span data-stu-id="f4f39-146">For more information, see [Azure availability sets guide](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).</span></span>

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a><span data-ttu-id="f4f39-147">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="f4f39-147">Create a virtual machine</span></span>

<span data-ttu-id="f4f39-148">Een virtuele machine maken met de Hallo [az vm maken](/cli/azure/vm#create) opdracht.</span><span class="sxs-lookup"><span data-stu-id="f4f39-148">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="f4f39-149">Hallo volgende voorbeeld maakt twee virtuele machines met de naam `myVM1` en `myVM2`.</span><span class="sxs-lookup"><span data-stu-id="f4f39-149">hello following example creates two VMs named `myVM1` and `myVM2`.</span></span> <span data-ttu-id="f4f39-150">SSH-sleutels maken als deze niet al bestaan op de standaardlocatie van de sleutel.</span><span class="sxs-lookup"><span data-stu-id="f4f39-150">Create SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="f4f39-151">toouse een specifieke verzameling van sleutels, gebruikt u Hallo `--ssh-key-value` optie.</span><span class="sxs-lookup"><span data-stu-id="f4f39-151">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>

#### <a name="create-myvm1-primary"></a><span data-ttu-id="f4f39-152">Maak myVM1 (primaire):</span><span class="sxs-lookup"><span data-stu-id="f4f39-152">Create myVM1 (primary):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="f4f39-153">Na het Hallo die VM is gemaakt, ziet u hello Azure CLI informatie vergelijkbare toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-153">After hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="f4f39-154">(Noteer Hallo `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="f4f39-154">(Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="f4f39-155">Dit adres is gebruikte tooaccess Hallo VM).</span><span class="sxs-lookup"><span data-stu-id="f4f39-155">This address is used tooaccess hello VM.)</span></span>

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

#### <a name="create-myvm2-replicate"></a><span data-ttu-id="f4f39-156">MyVM2 maken (repliceren):</span><span class="sxs-lookup"><span data-stu-id="f4f39-156">Create myVM2 (replicate):</span></span>
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

<span data-ttu-id="f4f39-157">Let op Hallo `publicIpAddress` ook nadat deze is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f4f39-157">Take note of hello `publicIpAddress` as well after it has been created.</span></span>

### <a name="open-hello-tcp-port-for-connectivity"></a><span data-ttu-id="f4f39-158">Open TCP-poort Hallo voor connectiviteit</span><span class="sxs-lookup"><span data-stu-id="f4f39-158">Open hello TCP port for connectivity</span></span>

<span data-ttu-id="f4f39-159">de volgende stap Hallo is tooconfigure externe eindpunten, waarmee u tooaccess Hallo Oracle-database op afstand.</span><span class="sxs-lookup"><span data-stu-id="f4f39-159">hello next step is tooconfigure external endpoints,  which enable you tooaccess hello Oracle database remotely.</span></span> <span data-ttu-id="f4f39-160">tooconfigure Hallo externe eindpunten, Hallo volgende opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4f39-160">tooconfigure hello external endpoints, run hello following commands.</span></span>

#### <a name="open-hello-port-for-myvm1"></a><span data-ttu-id="f4f39-161">Hallo-poort voor myVM1 openen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-161">Open hello port for myVM1:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

<span data-ttu-id="f4f39-162">Hallo resultaten ziet vergelijkbare toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-162">hello results should look similar toohello following response:</span></span>

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

#### <a name="open-hello-port-for-myvm2"></a><span data-ttu-id="f4f39-163">Hallo-poort voor myVM2 openen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-163">Open hello port for myVM2:</span></span>

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a><span data-ttu-id="f4f39-164">Verbinding maken met toohello virtuele machine</span><span class="sxs-lookup"><span data-stu-id="f4f39-164">Connect toohello virtual machine</span></span>

<span data-ttu-id="f4f39-165">Gebruik Hallo volgende opdracht toocreate een SSH-sessie met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f4f39-165">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="f4f39-166">Hallo IP-adres vervangen door Hallo `publicIpAddress` van uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="f4f39-166">Replace hello IP address with hello `publicIpAddress` of your virtual machine.</span></span>

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a><span data-ttu-id="f4f39-167">Hallo-database maken op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="f4f39-167">Create hello database on myVM1 (primary)</span></span>

<span data-ttu-id="f4f39-168">Hallo Oracle-software is al geïnstalleerd op Hallo Marketplace-installatiekopie, zodat de volgende stap Hallo tooinstall Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="f4f39-168">hello Oracle software is already installed on hello Marketplace image, so hello next step is tooinstall hello database.</span></span> 

<span data-ttu-id="f4f39-169">Hallo software Run as-Hallo 'oracle' supergebruiker:</span><span class="sxs-lookup"><span data-stu-id="f4f39-169">Run hello software as hello 'oracle' superuser:</span></span>

```bash
sudo su - oracle
```

<span data-ttu-id="f4f39-170">Hallo-database maken:</span><span class="sxs-lookup"><span data-stu-id="f4f39-170">Create hello database:</span></span>

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
<span data-ttu-id="f4f39-171">Uitvoer ziet er vergelijkbare toohello antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-171">Outputs should look similar toohello following response:</span></span>

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

<span data-ttu-id="f4f39-172">Hallo ORACLE_SID en ORACLE_HOME variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f4f39-172">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="f4f39-173">Desgewenst kunt u ORACLE_HOME en ORACLE_SID toohello .bashrc bestand, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen toevoegen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-173">Optionally, you can add ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins:</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="f4f39-174">Oracle-listener starten</span><span class="sxs-lookup"><span data-stu-id="f4f39-174">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a><span data-ttu-id="f4f39-175">Hallo-database maken op myVM2 (repliceren)</span><span class="sxs-lookup"><span data-stu-id="f4f39-175">Create hello database on myVM2 (replicate)</span></span>

```bash
sudo su - oracle
```
<span data-ttu-id="f4f39-176">Hallo-database maken:</span><span class="sxs-lookup"><span data-stu-id="f4f39-176">Create hello database:</span></span>

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
<span data-ttu-id="f4f39-177">Hallo ORACLE_SID en ORACLE_HOME variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f4f39-177">Set hello ORACLE_SID and ORACLE_HOME variables.</span></span>

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

<span data-ttu-id="f4f39-178">U kunt eventueel ORACLE_HOME en ORACLE_SID toohello .bashrc bestand toegevoegd, zodat deze instellingen worden opgeslagen voor toekomstige aanmeldingen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-178">Optionally, you can added ORACLE_HOME and ORACLE_SID toohello .bashrc file, so that these settings are saved for future sign-ins.</span></span>

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a><span data-ttu-id="f4f39-179">Oracle-listener starten</span><span class="sxs-lookup"><span data-stu-id="f4f39-179">Start Oracle listener</span></span>
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a><span data-ttu-id="f4f39-180">Golden Gate configureren</span><span class="sxs-lookup"><span data-stu-id="f4f39-180">Configure Golden Gate</span></span> 
<span data-ttu-id="f4f39-181">tooconfigure Golden-Gate maatregelen treffen Hallo in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="f4f39-181">tooconfigure Golden Gate, take hello steps in this section.</span></span>

### <a name="enable-archive-log-mode-on-myvm1-primary"></a><span data-ttu-id="f4f39-182">Bij myVM1 (primaire) archief logboek-modus inschakelen</span><span class="sxs-lookup"><span data-stu-id="f4f39-182">Enable archive log mode on myVM1 (primary)</span></span>

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
<span data-ttu-id="f4f39-183">Force logboekregistratie inschakelen en controleer of ten minste één logboekbestand aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="f4f39-183">Enable force logging, and make sure at least one log file is present.</span></span>

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a><span data-ttu-id="f4f39-184">Golden Gate-software downloaden</span><span class="sxs-lookup"><span data-stu-id="f4f39-184">Download Golden Gate software</span></span>
<span data-ttu-id="f4f39-185">toodownload en bereid Hallo Oracle Golden Gate-software, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-185">toodownload and prepare hello Oracle Golden Gate software, complete hello following steps:</span></span>

1. <span data-ttu-id="f4f39-186">Hallo downloaden **fbo_ggs_Linux_x64_shiphome.zip** bestand van Hallo [Oracle Golden Gate downloadpagina](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="f4f39-186">Download hello **fbo_ggs_Linux_x64_shiphome.zip** file from hello [Oracle Golden Gate download page](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html).</span></span> <span data-ttu-id="f4f39-187">Onder Hallo downloaden titel **Oracle GoldenGate 12.x.x.x voor Oracle Linux x86-64**, moet er een reeks ZIP-bestanden toodownload.</span><span class="sxs-lookup"><span data-stu-id="f4f39-187">Under hello download title **Oracle GoldenGate 12.x.x.x for Oracle Linux x86-64**, there should be a set of .zip files toodownload.</span></span>

2. <span data-ttu-id="f4f39-188">Nadat u Hallo ZIP-bestanden tooyour-clientcomputer hebt gedownload, gebruikt u beveiligde kopie Protocol (SCP) toocopy Hallo bestanden tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="f4f39-188">After you download hello .zip files tooyour client computer, use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. <span data-ttu-id="f4f39-189">Hallo ZIP-bestanden toohello verplaatsen **/ opt** map.</span><span class="sxs-lookup"><span data-stu-id="f4f39-189">Move hello .zip files toohello **/opt** folder.</span></span> <span data-ttu-id="f4f39-190">Wijzig Hallo eigenaar van Hallo bestanden als volgt:</span><span class="sxs-lookup"><span data-stu-id="f4f39-190">Then change hello owner of hello files as follows:</span></span>

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. <span data-ttu-id="f4f39-191">Pak Hallo-bestanden (installatie Hallo Linux pak hulpprogramma als deze nog niet is geïnstalleerd):</span><span class="sxs-lookup"><span data-stu-id="f4f39-191">Unzip hello files (install hello Linux unzip utility if it's not already installed):</span></span>

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. <span data-ttu-id="f4f39-192">De machtiging wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-192">Change permission:</span></span>

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a><span data-ttu-id="f4f39-193">Voorbereiden op Hallo-client en de VM toorun x11 (alleen voor Windows-clients)</span><span class="sxs-lookup"><span data-stu-id="f4f39-193">Prepare hello client and VM toorun x11 (for Windows clients only)</span></span>
<span data-ttu-id="f4f39-194">Dit is een optionele stap.</span><span class="sxs-lookup"><span data-stu-id="f4f39-194">This is an optional step.</span></span> <span data-ttu-id="f4f39-195">U kunt deze stap overslaan als u een voor Linux client of al x11 hebt setup.</span><span class="sxs-lookup"><span data-stu-id="f4f39-195">You can skip this step if you are using a Linux client or already have x11 setup.</span></span>

1. <span data-ttu-id="f4f39-196">Download PuTTY en Xming tooyour Windows-computer:</span><span class="sxs-lookup"><span data-stu-id="f4f39-196">Download PuTTY and Xming tooyour Windows computer:</span></span>

  * [<span data-ttu-id="f4f39-197">Download PuTTY</span><span class="sxs-lookup"><span data-stu-id="f4f39-197">Download PuTTY</span></span>](http://www.putty.org/)
  * [<span data-ttu-id="f4f39-198">Xming downloaden</span><span class="sxs-lookup"><span data-stu-id="f4f39-198">Download Xming</span></span>](https://xming.en.softonic.com/)

2.  <span data-ttu-id="f4f39-199">Nadat u PuTTY in Hallo PuTTY map (bijvoorbeeld C:\Program Files\PuTTY), puttygen.exe (Generator PuTTY Key) uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4f39-199">After you install PuTTY, in hello PuTTY folder (for example, C:\Program Files\PuTTY), run puttygen.exe (PuTTY Key Generator).</span></span>

3.  <span data-ttu-id="f4f39-200">In de PuTTY codegenerator:</span><span class="sxs-lookup"><span data-stu-id="f4f39-200">In PuTTY Key Generator:</span></span>

  - <span data-ttu-id="f4f39-201">een sleutel, selecteer Hallo toogenerate **genereren** knop.</span><span class="sxs-lookup"><span data-stu-id="f4f39-201">toogenerate a key, select hello **Generate** button.</span></span>
  - <span data-ttu-id="f4f39-202">Kopieer de inhoud Hallo van Hallo-sleutel (**Ctrl + C**).</span><span class="sxs-lookup"><span data-stu-id="f4f39-202">Copy hello contents of hello key (**Ctrl+C**).</span></span>
  - <span data-ttu-id="f4f39-203">Selecteer Hallo **persoonlijke sleutel opslaan** knop.</span><span class="sxs-lookup"><span data-stu-id="f4f39-203">Select hello **Save private key** button.</span></span>
  - <span data-ttu-id="f4f39-204">Hallo-waarschuwing die wordt weergegeven, en selecteer vervolgens negeren **OK**.</span><span class="sxs-lookup"><span data-stu-id="f4f39-204">Ignore hello warning that appears, and then select **OK**.</span></span>

    ![Schermafbeelding van pagina met PuTTY codegenerator Hallo](./media/oracle-golden-gate/puttykeygen.png)

4.  <span data-ttu-id="f4f39-206">In de virtuele machine, moet u deze opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f4f39-206">In your VM, run these commands:</span></span>

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. <span data-ttu-id="f4f39-207">Maak een bestand met de naam **authorized_keys**.</span><span class="sxs-lookup"><span data-stu-id="f4f39-207">Create a file named **authorized_keys**.</span></span> <span data-ttu-id="f4f39-208">Hallo-inhoud van Hallo key plakken in dit bestand en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="f4f39-208">Paste hello contents of hello key in this file, and then save hello file.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f4f39-209">Hallo-sleutel moet Hallo tekenreeks bevatten `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="f4f39-209">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="f4f39-210">Hallo-inhoud van Hallo-sleutel moet ook een enkele regel tekst.</span><span class="sxs-lookup"><span data-stu-id="f4f39-210">Also, hello contents of hello key must be a single line of text.</span></span>
  >  

6. <span data-ttu-id="f4f39-211">Start PuTTY.</span><span class="sxs-lookup"><span data-stu-id="f4f39-211">Start PuTTY.</span></span> <span data-ttu-id="f4f39-212">In Hallo **categorie** deelvenster **verbinding** > **SSH** > **Auth**. In Hallo **persoonlijke sleutelbestand voor verificatie** vak, blader toohello-sleutel die u eerder hebt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f4f39-212">In hello **Category** pane, select **Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

  ![Schermafbeelding van pagina van de persoonlijke sleutel instellen Hallo](./media/oracle-golden-gate/setprivatekey.png)

7. <span data-ttu-id="f4f39-214">In Hallo **categorie** deelvenster **verbinding** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="f4f39-214">In hello **Category** pane, select **Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="f4f39-215">Selecteer vervolgens Hallo **inschakelen X11 doorsturen** vak.</span><span class="sxs-lookup"><span data-stu-id="f4f39-215">Then select hello **Enable X11 forwarding** box.</span></span>

  ![Schermafbeelding van pagina met Hallo X11 inschakelen](./media/oracle-golden-gate/enablex11.png)

8. <span data-ttu-id="f4f39-217">In Hallo **categorie** deelvenster te gaan**sessie**.</span><span class="sxs-lookup"><span data-stu-id="f4f39-217">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="f4f39-218">Geef informatie op Hallo host, en selecteer vervolgens **Open**.</span><span class="sxs-lookup"><span data-stu-id="f4f39-218">Enter hello host information, and then select **Open**.</span></span>

  ![Schermafbeelding van pagina met Hallo sessie](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a><span data-ttu-id="f4f39-220">Golden Gate software installeren</span><span class="sxs-lookup"><span data-stu-id="f4f39-220">Install Golden Gate software</span></span>

<span data-ttu-id="f4f39-221">tooinstall Oracle Golden Gate, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-221">tooinstall Oracle Golden Gate, complete hello following steps:</span></span>

1. <span data-ttu-id="f4f39-222">Meld u aan als oracle.</span><span class="sxs-lookup"><span data-stu-id="f4f39-222">Sign in as oracle.</span></span> <span data-ttu-id="f4f39-223">(U moet kunnen toosign in zonder te worden gevraagd om een wachtwoord.) Zorg ervoor dat Xming voordat u begint met Hallo-installatie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f4f39-223">(You should be able toosign in without being prompted for a password.) Make sure that Xming is running before you begin hello installation.</span></span>
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. <span data-ttu-id="f4f39-224">Selecteer 'Oracle GoldenGate voor Oracle-Database 12c'.</span><span class="sxs-lookup"><span data-stu-id="f4f39-224">Select 'Oracle GoldenGate for Oracle Database 12c'.</span></span> <span data-ttu-id="f4f39-225">Selecteer vervolgens **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4f39-225">Then select **Next** toocontinue.</span></span>

  ![Schermafbeelding van pagina met Hallo installatieprogramma installatie selecteren](./media/oracle-golden-gate/golden_gate_install_01.png)

3. <span data-ttu-id="f4f39-227">Hallo software locatie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-227">Change hello software location.</span></span> <span data-ttu-id="f4f39-228">Selecteer vervolgens Hallo **Manager Start** in en voert u de locatie van de database Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4f39-228">Then select  hello **Start Manager** box and enter hello database location.</span></span> <span data-ttu-id="f4f39-229">Selecteer **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4f39-229">Select **Next** toocontinue.</span></span>

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_02.png)

4. <span data-ttu-id="f4f39-231">Hallo-inventarisatie map wijzigen, en selecteer vervolgens **volgende** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4f39-231">Change hello inventory directory, and then select **Next** toocontinue.</span></span>

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_03.png)

5. <span data-ttu-id="f4f39-233">Op Hallo **samenvatting** Schakel in het scherm **installeren** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="f4f39-233">On hello **Summary** screen, select **Install** toocontinue.</span></span>

  ![Schermafbeelding van pagina met Hallo installatieprogramma installatie selecteren](./media/oracle-golden-gate/golden_gate_install_04.png)

6. <span data-ttu-id="f4f39-235">Vraag toorun een script is mogelijk als 'root'.</span><span class="sxs-lookup"><span data-stu-id="f4f39-235">You might be prompted toorun a script as 'root'.</span></span> <span data-ttu-id="f4f39-236">Zo ja, open een afzonderlijke sessie ssh toohello VM, sudo tooroot, en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4f39-236">If so, open a separate session, ssh toohello VM, sudo tooroot, and then run hello script.</span></span> <span data-ttu-id="f4f39-237">Selecteer **OK** gaan.</span><span class="sxs-lookup"><span data-stu-id="f4f39-237">Select **OK** continue.</span></span>

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_05.png)

7. <span data-ttu-id="f4f39-239">Wanneer het Hallo-installatie is voltooid, selecteert u **sluiten** toocomplete Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="f4f39-239">When hello installation has finished, select **Close** toocomplete hello process.</span></span>

  ![Schermopname van Hallo installatiepagina selecteren](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a><span data-ttu-id="f4f39-241">Instellen van de service op myVM1 (primair)</span><span class="sxs-lookup"><span data-stu-id="f4f39-241">Set up service on myVM1 (primary)</span></span>

1. <span data-ttu-id="f4f39-242">Maken of bijwerken van Hallo tnsnames.ora bestand:</span><span class="sxs-lookup"><span data-stu-id="f4f39-242">Create or update hello tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="f4f39-243">Hallo Golden Gate eigenaar en gebruikersaccounts maken.</span><span class="sxs-lookup"><span data-stu-id="f4f39-243">Create hello Golden Gate owner and user accounts.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f4f39-244">Hallo eigenaarsaccount moet C ## voorvoegsel hebben.</span><span class="sxs-lookup"><span data-stu-id="f4f39-244">hello owner account must have C## prefix.</span></span>
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

3. <span data-ttu-id="f4f39-245">Hallo Golden Gate test-gebruikersaccount maken:</span><span class="sxs-lookup"><span data-stu-id="f4f39-245">Create hello Golden Gate test user account:</span></span>

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

4. <span data-ttu-id="f4f39-246">Hallo extract parameterbestand configureren.</span><span class="sxs-lookup"><span data-stu-id="f4f39-246">Configure hello extract parameter file.</span></span>

 <span data-ttu-id="f4f39-247">Hallo gouden gate-opdrachtregelinterface (ggsci) starten:</span><span class="sxs-lookup"><span data-stu-id="f4f39-247">Start hello Golden gate command-line interface (ggsci):</span></span>

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
5. <span data-ttu-id="f4f39-248">Hallo toohello EXTRACT parameterbestand volgen (via vi opdrachten) toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-248">Add hello following toohello EXTRACT parameter file (by using vi commands).</span></span> <span data-ttu-id="f4f39-249">Druk op Esc-toets ': wq!'</span><span class="sxs-lookup"><span data-stu-id="f4f39-249">Press Esc key, ':wq!'</span></span> <span data-ttu-id="f4f39-250">toosave-bestand.</span><span class="sxs-lookup"><span data-stu-id="f4f39-250">toosave file.</span></span> 

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
6. <span data-ttu-id="f4f39-251">Registratie uit te pakken--geïntegreerde uitpakken.</span><span class="sxs-lookup"><span data-stu-id="f4f39-251">Register extract--integrated extract:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. <span data-ttu-id="f4f39-252">Extract controlepunten ingesteld en realtime extract te starten:</span><span class="sxs-lookup"><span data-stu-id="f4f39-252">Set up extract checkpoints and start real-time extract:</span></span>

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
<span data-ttu-id="f4f39-253">In deze stap ziet u Hallo SCN die later wordt gebruikt in een andere sectie starten:</span><span class="sxs-lookup"><span data-stu-id="f4f39-253">In this step, you find hello starting SCN, which will be used later, in a different section:</span></span>

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

### <a name="set-up-service-on-myvm2-replicate"></a><span data-ttu-id="f4f39-254">Instellen van de service op myVM2 (repliceren)</span><span class="sxs-lookup"><span data-stu-id="f4f39-254">Set up service on myVM2 (replicate)</span></span>


1. <span data-ttu-id="f4f39-255">Maken of bijwerken van Hallo tnsnames.ora bestand:</span><span class="sxs-lookup"><span data-stu-id="f4f39-255">Create or update hello tnsnames.ora file:</span></span>

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

2. <span data-ttu-id="f4f39-256">Een repliceren account maken:</span><span class="sxs-lookup"><span data-stu-id="f4f39-256">Create a replicate account:</span></span>

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. <span data-ttu-id="f4f39-257">Maak een gebruikersaccount voor Golden Gate-test:</span><span class="sxs-lookup"><span data-stu-id="f4f39-257">Create a Golden Gate test user account:</span></span>

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

4. <span data-ttu-id="f4f39-258">REPLICAT parameter tooreplicate bestandswijzigingen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-258">REPLICAT parameter file tooreplicate changes:</span></span> 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  <span data-ttu-id="f4f39-259">De inhoud van het parameterbestand REPORA:</span><span class="sxs-lookup"><span data-stu-id="f4f39-259">Content of REPORA parameter file:</span></span>

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

5. <span data-ttu-id="f4f39-260">Een controlepunt replicat instellen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-260">Set up a replicat checkpoint:</span></span>

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

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a><span data-ttu-id="f4f39-261">Hallo-replicatie (myVM1 en myVM2) instellen</span><span class="sxs-lookup"><span data-stu-id="f4f39-261">Set up hello replication (myVM1 and myVM2)</span></span>

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="f4f39-262">1. Hallo-replicatie op myVM2 instellen (repliceren)</span><span class="sxs-lookup"><span data-stu-id="f4f39-262">1. Set up hello replication on myVM2 (replicate)</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
<span data-ttu-id="f4f39-263">Hallo-bestand met de volgende Hallo bijwerken:</span><span class="sxs-lookup"><span data-stu-id="f4f39-263">Update hello file with hello following:</span></span>

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
<span data-ttu-id="f4f39-264">Hallo Manager-service vervolgens opnieuw te starten:</span><span class="sxs-lookup"><span data-stu-id="f4f39-264">Then restart hello Manager service:</span></span>

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a><span data-ttu-id="f4f39-265">2. Hallo-replicatie op myVM1 (primaire) instellen</span><span class="sxs-lookup"><span data-stu-id="f4f39-265">2. Set up hello replication on myVM1 (primary)</span></span>

<span data-ttu-id="f4f39-266">Start Hallo initiële laden en controleren op fouten:</span><span class="sxs-lookup"><span data-stu-id="f4f39-266">Start hello initial load and check for errors:</span></span>

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a><span data-ttu-id="f4f39-267">3. Hallo-replicatie op myVM2 instellen (repliceren)</span><span class="sxs-lookup"><span data-stu-id="f4f39-267">3. Set up hello replication on myVM2 (replicate)</span></span>

<span data-ttu-id="f4f39-268">Hallo SCN nummer met Hallo nummer dat u eerder hebt verkregen wijzigen:</span><span class="sxs-lookup"><span data-stu-id="f4f39-268">Change hello SCN number with hello number you obtained before:</span></span>

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
<span data-ttu-id="f4f39-269">Hallo-replicatie is gestart en u kunt het testen door het invoegen van nieuwe records tooTEST tabellen.</span><span class="sxs-lookup"><span data-stu-id="f4f39-269">hello replication has begun, and you can test it by inserting new records tooTEST tables.</span></span>


### <a name="view-job-status-and-troubleshooting"></a><span data-ttu-id="f4f39-270">Status van de taak weergeven en problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f4f39-270">View job status and troubleshooting</span></span>

#### <a name="view-reports"></a><span data-ttu-id="f4f39-271">Rapporten weergeven</span><span class="sxs-lookup"><span data-stu-id="f4f39-271">View reports</span></span>
<span data-ttu-id="f4f39-272">tooview rapporten over myVM1, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f4f39-272">tooview reports on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
<span data-ttu-id="f4f39-273">tooview rapporten over myVM2, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f4f39-273">tooview reports on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a><span data-ttu-id="f4f39-274">Weergave status en geschiedenis</span><span class="sxs-lookup"><span data-stu-id="f4f39-274">View status and history</span></span>
<span data-ttu-id="f4f39-275">tooview status en geschiedenis op myVM1, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f4f39-275">tooview status and history on myVM1, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

<span data-ttu-id="f4f39-276">tooview status en geschiedenis op myVM2, Hallo volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f4f39-276">tooview status and history on myVM2, run hello following commands:</span></span>

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
<span data-ttu-id="f4f39-277">Dit is voltooid Hallo-installatie en configuratie van Golden Gate op Oracle linux.</span><span class="sxs-lookup"><span data-stu-id="f4f39-277">This completes hello installation and configuration of Golden Gate on Oracle linux.</span></span>


## <a name="delete-hello-virtual-machine"></a><span data-ttu-id="f4f39-278">Hallo virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="f4f39-278">Delete hello virtual machine</span></span>

<span data-ttu-id="f4f39-279">Wanneer deze niet langer nodig is, kan na de opdracht Hallo gebruikte tooremove Hallo-resourcegroep, VM en alle gerelateerde resources zijn.</span><span class="sxs-lookup"><span data-stu-id="f4f39-279">When it's no longer needed, hello following command can be used tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f4f39-280">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4f39-280">Next steps</span></span>

[<span data-ttu-id="f4f39-281">Zelfstudie voor het maken van virtuele machines met een hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="f4f39-281">Create highly available virtual machines tutorial</span></span>](../../linux/create-cli-complete.md)

[<span data-ttu-id="f4f39-282">CLI-voorbeelden voor VM-implementatie verkennen</span><span class="sxs-lookup"><span data-stu-id="f4f39-282">Explore VM deployment CLI samples</span></span>](../../linux/cli-samples.md)

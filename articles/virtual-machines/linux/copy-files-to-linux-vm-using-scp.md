---
title: aaaMove bestanden tooand van Azure Linux VM's met SCP | Microsoft Docs
description: Veilig verplaatsen bestanden tooand van een Linux-VM in Azure met behulp van SCP en een SSH-sleutelpaar.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: danlep
ms.openlocfilehash: 9e4dce667aa581df74aec3d45a6ba5e52f777d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-files-tooand-from-a-linux-vm-using-scp"></a><span data-ttu-id="558fa-103">Bestanden tooand verplaatsen van een Linux-VM met SCP</span><span class="sxs-lookup"><span data-stu-id="558fa-103">Move files tooand from a Linux VM using SCP</span></span>

<span data-ttu-id="558fa-104">Dit artikel laat zien hoe toomove bestanden van uw werkstation up tooan Azure Linux VM of van een Azure Linux VM omlaag tooyour werkstation met behulp van Secure kopiëren (SCP).</span><span class="sxs-lookup"><span data-stu-id="558fa-104">This article shows how toomove files from your workstation up tooan Azure Linux VM, or from an Azure Linux VM down tooyour workstation, using Secure Copy (SCP).</span></span> <span data-ttu-id="558fa-105">Verplaatsen van bestanden tussen uw werkstation en Linux-VM snel en veilig is essentieel voor het beheren van uw Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="558fa-105">Moving files between your workstation and a Linux VM, quickly and securely, is critical for managing your Azure infrastructure.</span></span> 

<span data-ttu-id="558fa-106">Dit artikel, moet u een Linux-VM is geïmplementeerd in Azure worden verkregen met [SSH openbare en persoonlijke sleutelbestanden](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="558fa-106">For this article, you need a Linux VM deployed in Azure using [SSH public and private key files](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="558fa-107">U moet ook een SCP-client voor de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="558fa-107">You also need an SCP client for your local computer.</span></span> <span data-ttu-id="558fa-108">Het is gebouwd op SSH en opgenomen in Hallo standaard Bash-shell van de meeste Linux en Mac-computers en sommige houders van Windows.</span><span class="sxs-lookup"><span data-stu-id="558fa-108">It is built on top of SSH and included in hello default Bash shell of most Linux and Mac computers and some Windows shells.</span></span>

## <a name="quick-commands"></a><span data-ttu-id="558fa-109">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="558fa-109">Quick commands</span></span>

<span data-ttu-id="558fa-110">Kopieer een bestand up toohello Linux VM</span><span class="sxs-lookup"><span data-stu-id="558fa-110">Copy a file up toohello Linux VM</span></span>

```bash
scp file azureuser@azurehost:directory/targetfile
```

<span data-ttu-id="558fa-111">Een bestand kopiëren naar beneden van Hallo Linux VM</span><span class="sxs-lookup"><span data-stu-id="558fa-111">Copy a file down from hello Linux VM</span></span>

```bash
scp azureuser@azurehost:directory/file targetfile
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="558fa-112">Gedetailleerd overzicht</span><span class="sxs-lookup"><span data-stu-id="558fa-112">Detailed walkthrough</span></span>

<span data-ttu-id="558fa-113">Als voorbeelden, we een Azure-configuratiebestand up tooa Linux VM verplaatsen en ophalen van een logboekmap beide SCP en de SSH-sleutels gebruiken.</span><span class="sxs-lookup"><span data-stu-id="558fa-113">As examples, we move an Azure configuration file up tooa Linux VM and pull down a log file directory, both using SCP and SSH keys.</span></span>   

## <a name="ssh-key-pair-authentication"></a><span data-ttu-id="558fa-114">SSH-sleutelpaar verificatie</span><span class="sxs-lookup"><span data-stu-id="558fa-114">SSH key pair authentication</span></span>

<span data-ttu-id="558fa-115">SCP gebruikt SSH voor Hallo transportlaag.</span><span class="sxs-lookup"><span data-stu-id="558fa-115">SCP uses SSH for hello transport layer.</span></span> <span data-ttu-id="558fa-116">SSH ingangen Hallo verificatie op de doelhost Hallo en het Hallo-bestand in een versleutelde standaard meegeleverd met SSH-tunnel wordt verplaatst.</span><span class="sxs-lookup"><span data-stu-id="558fa-116">SSH handles hello authentication on hello destination host, and it moves hello file in an encrypted tunnel provided by default with SSH.</span></span> <span data-ttu-id="558fa-117">Voor SSH-verificatie, de gebruikersnamen en wachtwoorden kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="558fa-117">For SSH authentication, usernames and passwords can be used.</span></span> <span data-ttu-id="558fa-118">SSH openbare en persoonlijke sleutel verificatie worden echter aanbevolen als aanbevolen beveiligingsprocedure.</span><span class="sxs-lookup"><span data-stu-id="558fa-118">However, SSH public and private key authentication are recommended as a security best practice.</span></span> <span data-ttu-id="558fa-119">Als SSH heeft geverifieerd Hallo verbinding, SCP begint vervolgens met de Hallo-bestand wordt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="558fa-119">Once SSH has authenticated hello connection, SCP then begins copying hello file.</span></span> <span data-ttu-id="558fa-120">Met behulp van een correct geconfigureerde `~/.ssh/config` en SSH-openbare en persoonlijke sleutels, Hallo SCP verbinding kunnen worden gemaakt met behulp van slechts een servernaam (of IP-adres).</span><span class="sxs-lookup"><span data-stu-id="558fa-120">Using a properly configured `~/.ssh/config` and SSH public and private keys, hello SCP connection can be established by just using a server name (or IP address).</span></span> <span data-ttu-id="558fa-121">Als u slechts één SSH-sleutel hebt, SCP in Hallo voor gezocht `~/.ssh/` directory, en wordt gebruikt door standaard toolog in toohello VM.</span><span class="sxs-lookup"><span data-stu-id="558fa-121">If you only have one SSH key, SCP looks for it in hello `~/.ssh/` directory, and uses it by default toolog in toohello VM.</span></span>

<span data-ttu-id="558fa-122">Voor meer informatie over het configureren van uw `~/.ssh/config` en SSH-openbare en persoonlijke sleutels, Zie [maken SSH-sleutels](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="558fa-122">For more information on configuring your `~/.ssh/config` and SSH public and private keys, see [Create SSH keys](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="scp-a-file-tooa-linux-vm"></a><span data-ttu-id="558fa-123">SCP een bestand tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="558fa-123">SCP a file tooa Linux VM</span></span>

<span data-ttu-id="558fa-124">Voor het eerste voorbeeld hello kopieert u een Azure-configuratiebestand up tooa Linux VM die is gebruikt toodeploy automatisering.</span><span class="sxs-lookup"><span data-stu-id="558fa-124">For hello first example, we copy an Azure configuration file up tooa Linux VM that is used toodeploy automation.</span></span> <span data-ttu-id="558fa-125">Beveiliging is belangrijk, omdat dit bestand bevat de Azure-API-referenties, waaronder geheimen.</span><span class="sxs-lookup"><span data-stu-id="558fa-125">Because this file contains Azure API credentials, which include secrets, security is important.</span></span> <span data-ttu-id="558fa-126">Hallo gecodeerde tunnel geleverd door SSH beveiligt Hallo inhoud van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="558fa-126">hello encrypted tunnel provided by SSH protects hello contents of hello file.</span></span>

<span data-ttu-id="558fa-127">Hallo na de opdracht kopieën Hallo lokale *.azure/config* tooan virtuele machine van Azure met FQDN-naam bestand *myserver.eastus.cloudapp.azure.com*. Hallo-beheerdersgebruikersnaam op Hallo Azure VM is *azureuser* .</span><span class="sxs-lookup"><span data-stu-id="558fa-127">hello following command copies hello local *.azure/config* file tooan Azure VM with FQDN *myserver.eastus.cloudapp.azure.com*. hello admin user name on hello Azure VM is *azureuser*.</span></span> <span data-ttu-id="558fa-128">Hallo-bestand is gerichte toohello */home/azureuser/* directory.</span><span class="sxs-lookup"><span data-stu-id="558fa-128">hello file is targeted toohello */home/azureuser/* directory.</span></span> <span data-ttu-id="558fa-129">Vervangt door uw eigen waarden in deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="558fa-129">Substitute your own values in this command.</span></span>

```bash
scp ~/.azure/config azureuser@myserver.eastus.cloudapp.com:/home/azureuser/config
```

## <a name="scp-a-directory-from-a-linux-vm"></a><span data-ttu-id="558fa-130">SCP een map van een Linux-VM</span><span class="sxs-lookup"><span data-stu-id="558fa-130">SCP a directory from a Linux VM</span></span>

<span data-ttu-id="558fa-131">In dit voorbeeld wordt een map met logbestanden van Hallo Linux VM tooyour Workstation kopiëren.</span><span class="sxs-lookup"><span data-stu-id="558fa-131">For this example, we copy a directory of log files from hello Linux VM down tooyour workstation.</span></span> <span data-ttu-id="558fa-132">Een logboekbestand kan of kan geen gevoelige of geheime gegevens.</span><span class="sxs-lookup"><span data-stu-id="558fa-132">A log file may or may not contain sensitive or secret data.</span></span> <span data-ttu-id="558fa-133">Echter, SCP zorgt u ervoor Hallo inhoud van de logboekbestanden Hallo zijn versleuteld.</span><span class="sxs-lookup"><span data-stu-id="558fa-133">However, using SCP ensures hello contents of hello log files are encrypted.</span></span> <span data-ttu-id="558fa-134">SCP tootransfer Hallo bestanden is de eenvoudigste manier tooget Hallo Hallo logboekmap en bestanden tooyour Workstation, terwijl tegelijkertijd ook beveiligd.</span><span class="sxs-lookup"><span data-stu-id="558fa-134">Using SCP tootransfer hello files is hello easiest way tooget hello log directory and files down tooyour workstation while also being secure.</span></span>

<span data-ttu-id="558fa-135">Hallo volgende opdracht kopieert bestanden in Hallo *thuis-/azureuser/logboeken/* directory op Hallo Azure VM toohello lokale map directory:</span><span class="sxs-lookup"><span data-stu-id="558fa-135">hello following command copies files in hello */home/azureuser/logs/* directory on hello Azure VM toohello local /tmp directory:</span></span>

```bash
scp -r azureuser@myserver.eastus.cloudapp.com:/home/azureuser/logs/. /tmp/
```

<span data-ttu-id="558fa-136">Hallo `-r` cli vlag Hiermee geeft u SCP toorecursively kopie Hallo bestanden en mappen van Hallo punt van Hallo-map weergegeven in het Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="558fa-136">hello `-r` cli flag instructs SCP toorecursively copy hello files and directories from hello point of hello directory listed in hello command.</span></span>  <span data-ttu-id="558fa-137">U ziet dat de opdrachtregelsyntaxis Hallo is ook vergelijkbare tooa `cp` -opdracht kopiëren.</span><span class="sxs-lookup"><span data-stu-id="558fa-137">Also notice that hello command-line syntax is similar tooa `cp` copy command.</span></span>

## <a name="next-steps"></a><span data-ttu-id="558fa-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="558fa-138">Next steps</span></span>

* [<span data-ttu-id="558fa-139">Beheren van gebruikers, SSH en controleer of herstel schijven op Azure Linux VM's met behulp van Hallo VMAccess-extensie</span><span class="sxs-lookup"><span data-stu-id="558fa-139">Manage users, SSH, and check or repair disks on Azure Linux VMs using hello VMAccess Extension</span></span>](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

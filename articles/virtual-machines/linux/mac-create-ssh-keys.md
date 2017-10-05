---
title: In Azure een SSH-sleutelpaar maken en gebruiken voor virtuele Linux-machines | Microsoft Docs
description: Een openbaar en persoonlijk SSH-sleutelpaar voor virtuele Linux-machines in Azure maken en gebruiken om de beveiliging van het verificatieproces te verbeteren.
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 34ae9482-da3e-4b2d-9d0d-9d672aa42498
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/14/2017
ms.author: iainfou
ms.openlocfilehash: 0fb71d2ffe533afba6e1e527b727a7b085e7da14
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-create-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="d67cc-103">Een sleutelpaar met een openbare en persoonlijke SSH-sleutel voor virtuele Linux-machines maken en gebruiken</span><span class="sxs-lookup"><span data-stu-id="d67cc-103">How to create and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="d67cc-104">Met een SSH-sleutelpaar (secure shell) kunt u virtuele machines (VM's) in Azure maken die voor verificatie gebruikmaken van SSH-sleutels, waardoor aanmelding met een wachtwoord niet meer nodig is.</span><span class="sxs-lookup"><span data-stu-id="d67cc-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating the need for passwords to log in.</span></span> <span data-ttu-id="d67cc-105">In dit artikel wordt beschreven hoe u snel een sleutelpaar met een openbare en een persoonlijke sleutel met SSH-protocol versie 2 RSA maakt en gebruikt voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="d67cc-105">This article shows you how to quickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="d67cc-106">Zie voor meer stappen en extra voorbeelden [Gedetailleerde stappen voor het maken van SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d67cc-106">For more detailed steps and additional examples, see [detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="d67cc-107">Een SSH-sleutelpaar maken</span><span class="sxs-lookup"><span data-stu-id="d67cc-107">Create an SSH key pair</span></span>
<span data-ttu-id="d67cc-108">Gebruik de opdracht `ssh-keygen` om openbare en persoonlijke SSH-sleutelbestanden te maken die standaard gemaakt worden in de map `~/.ssh`. U kunt een andere locatie en een extra wachtwoordzin (een wachtwoord voor toegang tot het bestand met de persoonlijke sleutel) opgeven wanneer u hierom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="d67cc-108">Use the `ssh-keygen` command to create SSH public and private key files that are by default created in the `~/.ssh` directory, but you can specify a different location and additional passphrase (a password to access the private key file) when prompted.</span></span> <span data-ttu-id="d67cc-109">Voer de volgende opdracht uit vanuit een Bash-shell en beantwoord de prompts met uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="d67cc-109">Run the following command from a Bash shell, answering the prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-the-ssh-key-pair"></a><span data-ttu-id="d67cc-110">Het SSH-sleutelpaar gebruiken</span><span class="sxs-lookup"><span data-stu-id="d67cc-110">Use the SSH key pair</span></span>
<span data-ttu-id="d67cc-111">De openbare sleutel die u op de virtuele Linux-machine in Azure plaatst, wordt standaard opgeslagen in `~/.ssh/id_rsa.pub`, tenzij u de locatie hebt gewijzigd toen u ze maakte.</span><span class="sxs-lookup"><span data-stu-id="d67cc-111">The public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed the location when you created them.</span></span> <span data-ttu-id="d67cc-112">Als u de [Azure CLI 2.0](/cli/azure) gebruikt om uw virtuele machine te maken, geeft u de locatie van deze openbare sleutel op wanneer u [az vm create](/cli/azure/vm#create) gebruikt met de optie `--ssh-key-path`.</span><span class="sxs-lookup"><span data-stu-id="d67cc-112">If you use the [Azure CLI 2.0](/cli/azure) to create your VM, specify the location of this public key when you use the [az vm create](/cli/azure/vm#create) with the `--ssh-key-path` option.</span></span> <span data-ttu-id="d67cc-113">Als u de inhoud van het te gebruiken openbare-sleutelbestand kopieert en plakt in Azure Portal of een Resource Manager-sjabloon, moet u ervoor zorgen dat u geen extra witruimte kopieert.</span><span class="sxs-lookup"><span data-stu-id="d67cc-113">If you copy and paste the contents of the public key file to use in the Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="d67cc-114">Als u OS X gebruikt, kunt u bijvoorbeeld een bestand met de openbare sleutel doorgeven (standaard **~/.ssh/id_rsa.pub**) naar **pbcopy** om de inhoud te kopiëren (er zijn andere Linux-programma's die hetzelfde doen, zoals `xclip`).</span><span class="sxs-lookup"><span data-stu-id="d67cc-114">For example, if you use OS X, you can pipe the public key file (by default, **~/.ssh/id_rsa.pub**) to **pbcopy** to copy the contents (there are other Linux programs that do the same thing, such as `xclip`).</span></span>

<span data-ttu-id="d67cc-115">Als u niet vertrouwd bent met openbare SSH-sleutels, kunt u de openbare sleutel bekijken door `cat` als volgt uit te voeren. Vervang `~/.ssh/id_rsa.pub` door de locatie van uw eigen openbare-sleutelbestand:</span><span class="sxs-lookup"><span data-stu-id="d67cc-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="d67cc-116">Met de openbare sleutel op uw virtuele Azure-machine voert u SSH uit op uw virtuele machine met het IP-adres of de DNS-naam van de virtuele machine (vervang `azureuser` en `myvm.westus.cloudapp.azure.com` hieronder door de gebruikersnaam van de beheerder en de volledig gekwalificeerde domeinnaam, of het IP-adres):</span><span class="sxs-lookup"><span data-stu-id="d67cc-116">With the public key on your Azure VM, SSH to your VM using the IP address or DNS name of your VM (remember to replace `azureuser` and `myvm.westus.cloudapp.azure.com` below with the admin username and the fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="d67cc-117">Als u tijdens het maken van uw sleutelpaar een wachtwoordzin hebt opgegeven, moet u deze tijdens het aanmeldingsproces desgevraagd invoeren.</span><span class="sxs-lookup"><span data-stu-id="d67cc-117">If you provided a passphrase when you created your key pair, enter the passphrase when prompted during the login process.</span></span> <span data-ttu-id="d67cc-118">(De server is toegevoegd aan uw map `~/.ssh/known_hosts` en u wordt pas weer gevraagd om verbinding te maken nadat de openbare sleutel op uw virtuele Azure-machine is gewijzigd of de naam van de server is verwijderd uit `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="d67cc-118">(The server is added to your `~/.ssh/known_hosts` folder, and you won't be asked to connect again until the public key on your Azure VM changes or the server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d67cc-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d67cc-119">Next steps</span></span>

<span data-ttu-id="d67cc-120">Virtuele machines die zijn gemaakt met behulp van SSH-sleutels, zijn standaard geconfigureerd met uitgeschakelde wachtwoorden, waardoor brute force-aanvallen om wachtwoorden in handen te krijgen veel duurder en dus ook lastiger worden.</span><span class="sxs-lookup"><span data-stu-id="d67cc-120">VMs created using SSH keys are by default configured with passwords disabled, to make brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="d67cc-121">Dit onderwerp beschrijft het maken van een eenvoudig SSH-sleutelpaar voor snel gebruik.</span><span class="sxs-lookup"><span data-stu-id="d67cc-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="d67cc-122">Als u meer hulp nodig hebt bij het maken van het SSH-sleutelpaar of meer certificaten nodig hebt, raadpleegt u [Gedetailleerde stappen voor het maken van SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="d67cc-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps to create SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="d67cc-123">U kunt virtuele machines maken die gebruikmaken van het SSH-sleutelpaar, met Azure Portal, CLI en sjablonen:</span><span class="sxs-lookup"><span data-stu-id="d67cc-123">You can create VMs that use your SSH key pair using the Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="d67cc-124">Een beveiligde virtuele Linux-machine maken met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="d67cc-124">Create a secure Linux VM using the Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d67cc-125">Een beveiligde virtuele Linux-machine maken met de Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="d67cc-125">Create a secure Linux VM using the Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="d67cc-126">Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="d67cc-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

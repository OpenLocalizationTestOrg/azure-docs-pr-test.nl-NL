---
title: aaaCreate en gebruikt een SSH sleutelpaar voor virtuele Linux-machines in Azure | Microsoft Docs
description: Hoe toocreate en gebruik een SSH openbare en persoonlijke sleutelpaar voor virtuele Linux-machines in Azure tooimprove beveiliging van het verificatieproces Hallo Hallo.
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
ms.openlocfilehash: 7fb94841d34d5bc006f3134adf91102ddce5f174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-use-an-ssh-public-and-private-key-pair-for-linux-vms-in-azure"></a><span data-ttu-id="26205-103">Hoe toocreate en gebruikt een SSH-sleutel voor openbare en persoonlijke voor virtuele Linux-machines in Azure koppelen</span><span class="sxs-lookup"><span data-stu-id="26205-103">How toocreate and use an SSH public and private key pair for Linux VMs in Azure</span></span>
<span data-ttu-id="26205-104">Met de combinatie van een secure shell (SSH), kunt u virtuele machines (VM's) maken in Azure die SSH-sleutels gebruiken voor verificatie, hoeft u Hallo wachtwoorden toolog in.</span><span class="sxs-lookup"><span data-stu-id="26205-104">With a secure shell (SSH) key pair, you can create virtual machines (VMs) in Azure that use SSH keys for authentication, eliminating hello need for passwords toolog in.</span></span> <span data-ttu-id="26205-105">Dit artikel ziet u hoe tooquickly genereren en het gebruik van een SSH-protocol versie 2 RSA openbare en persoonlijke sleutelbestand paar voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="26205-105">This article shows you how tooquickly generate and use an SSH protocol version 2 RSA public and private key file pair for Linux VMs.</span></span> <span data-ttu-id="26205-106">Zie voor meer stappen en aanvullende voorbeelden gegeven gedetailleerde, [gedetailleerde stappen toocreate SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="26205-106">For more detailed steps and additional examples, see [detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

## <a name="create-an-ssh-key-pair"></a><span data-ttu-id="26205-107">Een SSH-sleutelpaar maken</span><span class="sxs-lookup"><span data-stu-id="26205-107">Create an SSH key pair</span></span>
<span data-ttu-id="26205-108">Gebruik Hallo `ssh-keygen` toocreate SSH openbare en persoonlijke sleutelbestanden die gemaakt in Hallo standaard zijn opdracht `~/.ssh` directory, maar u kunt aanvullende wachtwoordzin (een wachtwoord tooaccess Hallo persoonlijke sleutelbestand) en een andere locatie opgeven wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="26205-108">Use hello `ssh-keygen` command toocreate SSH public and private key files that are by default created in hello `~/.ssh` directory, but you can specify a different location and additional passphrase (a password tooaccess hello private key file) when prompted.</span></span> <span data-ttu-id="26205-109">Hallo volgende opdracht uit een Bash-shell, het beantwoorden van Hallo prompts met uw eigen gegevens worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="26205-109">Run hello following command from a Bash shell, answering hello prompts with your own information.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="use-hello-ssh-key-pair"></a><span data-ttu-id="26205-110">Hallo SSH-sleutelpaar gebruiken</span><span class="sxs-lookup"><span data-stu-id="26205-110">Use hello SSH key pair</span></span>
<span data-ttu-id="26205-111">Hallo openbare sleutel die u op uw Linux-VM in Azure plaatst, wordt standaard opgeslagen in `~/.ssh/id_rsa.pub`, tenzij u Hallo locatie gewijzigd wanneer u ze hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="26205-111">hello public key that you place on your Linux VM in Azure is by default stored in `~/.ssh/id_rsa.pub`, unless you changed hello location when you created them.</span></span> <span data-ttu-id="26205-112">Als u Hallo [Azure CLI 2.0](/cli/azure) toocreate uw VM Hallo-locatie van deze openbare sleutel opgeven wanneer u Hallo [az vm maken](/cli/azure/vm#create) Hello `--ssh-key-path` optie.</span><span class="sxs-lookup"><span data-stu-id="26205-112">If you use hello [Azure CLI 2.0](/cli/azure) toocreate your VM, specify hello location of this public key when you use hello [az vm create](/cli/azure/vm#create) with hello `--ssh-key-path` option.</span></span> <span data-ttu-id="26205-113">Als u inhoud kopiëren en Hallo van Hallo openbaar-sleutelbestand toouse in hello Azure-portal of een Resource Manager-sjabloon plakken, zorg er dan voor dat u alle aanvullende witruimte niet kopiëren.</span><span class="sxs-lookup"><span data-stu-id="26205-113">If you copy and paste hello contents of hello public key file toouse in hello Azure portal or a Resource Manager template, make sure you don't copy any additional whitespace.</span></span> <span data-ttu-id="26205-114">Als u OS X gebruikt, kunt u bijvoorbeeld Hallo openbaar-sleutelbestand doorsluizen (standaard **~/.ssh/id_rsa.pub**) te**pbcopy** toocopy Hallo inhoud (Er zijn andere Linux-programma's die hetzelfde is, zoals Hallo`xclip`).</span><span class="sxs-lookup"><span data-stu-id="26205-114">For example, if you use OS X, you can pipe hello public key file (by default, **~/.ssh/id_rsa.pub**) too**pbcopy** toocopy hello contents (there are other Linux programs that do hello same thing, such as `xclip`).</span></span>

<span data-ttu-id="26205-115">Als u niet vertrouwd bent met openbare SSH-sleutels, kunt u de openbare sleutel bekijken door `cat` als volgt uit te voeren. Vervang `~/.ssh/id_rsa.pub` door de locatie van uw eigen openbare-sleutelbestand:</span><span class="sxs-lookup"><span data-stu-id="26205-115">If you're not familiar with SSH public keys, you can see your public key by running `cat` as follows, replacing `~/.ssh/id_rsa.pub` with your own public key file location:</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="26205-116">Met de openbare sleutel Hallo op uw virtuele machine in Azure, IP-adres of de DNS-naam van uw virtuele machine gebruik van SSH tooyour VM Hallo (onthouden tooreplace `azureuser` en `myvm.westus.cloudapp.azure.com` hieronder met Hallo beheerdersgebruikersnaam en het volledig gekwalificeerde domeinnaam Hallo-- of het IP-adres):</span><span class="sxs-lookup"><span data-stu-id="26205-116">With hello public key on your Azure VM, SSH tooyour VM using hello IP address or DNS name of your VM (remember tooreplace `azureuser` and `myvm.westus.cloudapp.azure.com` below with hello admin username and hello fully qualified domain name -- or IP address):</span></span>

```bash
ssh azureuser@myvm.westus.cloudapp.azure.com
```

<span data-ttu-id="26205-117">Als u een wachtwoordzin opgegeven tijdens het maken van uw sleutelpaar, Voer Hallo wachtwoordzin wanneer u wordt gevraagd tijdens het Hallo-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="26205-117">If you provided a passphrase when you created your key pair, enter hello passphrase when prompted during hello login process.</span></span> <span data-ttu-id="26205-118">(Hallo-server toegevoegd tooyour `~/.ssh/known_hosts` map en u won't gevraagd tooconnect pas weer Hallo openbare sleutel van uw Azure VM-wijzigingen of Hallo-servernaam is verwijderd van `~/.ssh/known_hosts`.)</span><span class="sxs-lookup"><span data-stu-id="26205-118">(hello server is added tooyour `~/.ssh/known_hosts` folder, and you won't be asked tooconnect again until hello public key on your Azure VM changes or hello server name is removed from `~/.ssh/known_hosts`.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="26205-119">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="26205-119">Next steps</span></span>

<span data-ttu-id="26205-120">Virtuele machines die zijn gemaakt met behulp van SSH-sleutels zijn standaard geconfigureerd met wachtwoorden die zijn uitgeschakeld, toomake brute-geforceerde raden probeert aanzienlijk duurder en daarom moeilijk.</span><span class="sxs-lookup"><span data-stu-id="26205-120">VMs created using SSH keys are by default configured with passwords disabled, toomake brute-forced guessing attempts vastly more expensive and therefore difficult.</span></span> <span data-ttu-id="26205-121">Dit onderwerp beschrijft het maken van een eenvoudig SSH-sleutelpaar voor snel gebruik.</span><span class="sxs-lookup"><span data-stu-id="26205-121">This topic describes creating a simple SSH key pair for quick usage.</span></span> <span data-ttu-id="26205-122">Als u meer hulp bij het maken van uw SSH-sleutelpaar nodig of extra certificaten nodig, Zie [gedetailleerde stappen toocreate SSH-sleutelparen en certificaten](create-ssh-keys-detailed.md).</span><span class="sxs-lookup"><span data-stu-id="26205-122">If you need more assistance in creating your SSH key pair or require additional certificates, see [Detailed steps toocreate SSH key pairs and certificates](create-ssh-keys-detailed.md).</span></span>

<span data-ttu-id="26205-123">U kunt virtuele machines die gebruikmaken van uw SSH-sleutelpaar met hello Azure-portal, CLI en sjablonen maken:</span><span class="sxs-lookup"><span data-stu-id="26205-123">You can create VMs that use your SSH key pair using hello Azure portal, CLI, and templates:</span></span>

* [<span data-ttu-id="26205-124">Maak een beveiligde Linux-VM met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="26205-124">Create a secure Linux VM using hello Azure portal</span></span>](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="26205-125">Maak een beveiligde Linux-VM met hello Azure CLI 2.0)</span><span class="sxs-lookup"><span data-stu-id="26205-125">Create a secure Linux VM using hello Azure CLI 2.0)</span></span>](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="26205-126">Een beveiligde virtuele Linux-machine maken met een Azure-sjabloon</span><span class="sxs-lookup"><span data-stu-id="26205-126">Create a secure Linux VM using an Azure template</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

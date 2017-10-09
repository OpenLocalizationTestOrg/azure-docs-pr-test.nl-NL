---
title: een virtuele Linux-machine RedHat tooan Azure Active Directory DS aaaJoin | Microsoft Docs
description: Hoe toojoin een bestaande RedHat Enterprise Linux 7 VM tooan Azure Active Directory Domain Services.
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/14/2016
ms.author: v-livech
ms.openlocfilehash: f3ba3c764e253191753f1cc5fc8c3b85c53818af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-redhat-linux-vm-tooan-azure-active-directory-domain-service"></a><span data-ttu-id="7602d-103">Deelnemen aan een virtuele Linux-machine RedHat tooan Azure Active Directory Domain Services</span><span class="sxs-lookup"><span data-stu-id="7602d-103">Join a RedHat Linux VM tooan Azure Active Directory Domain Service</span></span>

<span data-ttu-id="7602d-104">Dit artikel laat zien hoe een virtuele machine tooan voor Red Hat Enterprise Linux (RHEL) 7 Azure Active Directory Domain Services (AADDS) toojoin beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="7602d-104">This article shows you how toojoin a Red Hat Enterprise Linux (RHEL) 7 virtual machine tooan Azure Active Directory Domain Services (AADDS) managed domain.</span></span>  <span data-ttu-id="7602d-105">Hallo-vereisten zijn:</span><span class="sxs-lookup"><span data-stu-id="7602d-105">hello requirements are:</span></span>

- [<span data-ttu-id="7602d-106">een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7602d-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)

- [<span data-ttu-id="7602d-107">bestanden voor openbare en persoonlijke SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="7602d-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

- [<span data-ttu-id="7602d-108">een Azure Active Directory Domain Services-DC</span><span class="sxs-lookup"><span data-stu-id="7602d-108">an Azure Active Directory Domain Services DC</span></span>](../../active-directory-domain-services/active-directory-ds-getting-started.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="7602d-109">Snelle opdrachten</span><span class="sxs-lookup"><span data-stu-id="7602d-109">Quick Commands</span></span>

<span data-ttu-id="7602d-110">_Geen voorbeelden vervangen door uw eigen instellingen._</span><span class="sxs-lookup"><span data-stu-id="7602d-110">_Replace any examples with your own settings._</span></span>

### <a name="switch-hello-azure-cli-tooclassic-deployment-mode"></a><span data-ttu-id="7602d-111">Hello azure-cli tooclassic implementatie-modus schakelen</span><span class="sxs-lookup"><span data-stu-id="7602d-111">Switch hello azure-cli tooclassic deployment mode</span></span>

```azurecli
azure config mode asm
```

### <a name="search-for-a-rhel-version-and-image"></a><span data-ttu-id="7602d-112">Zoeken naar een RHEL-versie en een installatiekopie</span><span class="sxs-lookup"><span data-stu-id="7602d-112">Search for a RHEL version and image</span></span>

```azurecli
azure vm image list | grep "Red Hat"
```

### <a name="create-a-redhat-linux-vm"></a><span data-ttu-id="7602d-113">Een Redhat Linux VM maken</span><span class="sxs-lookup"><span data-stu-id="7602d-113">Create a Redhat Linux VM</span></span>

```azurecli
azure vm create myVM \
-o a879bbefc56a43abb0ce65052aac09f3__RHEL_7_2_Standard_Azure_RHUI-20161026220742 \
-g ahmet \
-p myPassword \
-e 22 \
-t "~/.ssh/id_rsa.pub" \
-z "Small" \
-l "West US"
```

### <a name="ssh-toohello-vm"></a><span data-ttu-id="7602d-114">SSH toohello VM</span><span class="sxs-lookup"><span data-stu-id="7602d-114">SSH toohello VM</span></span>

```bash
ssh -i ~/.ssh/id_rsa ahmet@myVM
```

### <a name="update-yum-packages"></a><span data-ttu-id="7602d-115">YUM pakketten bijwerken</span><span class="sxs-lookup"><span data-stu-id="7602d-115">Update YUM packages</span></span>

```bash
sudo yum update
```

### <a name="install-packages-needed"></a><span data-ttu-id="7602d-116">Installeren van pakketten nodig</span><span class="sxs-lookup"><span data-stu-id="7602d-116">Install packages needed</span></span>

```bash
sudo yum -y install realmd sssd krb5-workstation krb5-libs
```

<span data-ttu-id="7602d-117">Nu vereist hello-pakketten op Hallo virtuele Linux-machine zijn geïnstalleerd, de volgende taak Hallo is toojoin Hallo virtuele machine toohello beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="7602d-117">Now that hello required packages are installed on hello Linux virtual machine, hello next task is toojoin hello virtual machine toohello managed domain.</span></span>

### <a name="discover-hello-aad-domain-services-managed-domain"></a><span data-ttu-id="7602d-118">Hallo AAD Domain Services beheerd domein detecteren</span><span class="sxs-lookup"><span data-stu-id="7602d-118">Discover hello AAD Domain Services managed domain</span></span>

```bash
sudo realm discover mydomain.com
```

### <a name="initialize-kerberos"></a><span data-ttu-id="7602d-119">Initialiseren van kerberos</span><span class="sxs-lookup"><span data-stu-id="7602d-119">Initialize kerberos</span></span>

<span data-ttu-id="7602d-120">Zorg ervoor dat u opgeeft dat een gebruiker die lid is van toohello ' AAD DC' beheerdersgroep.</span><span class="sxs-lookup"><span data-stu-id="7602d-120">Ensure that you specify a user who belongs toohello 'AAD DC Administrators' group.</span></span> <span data-ttu-id="7602d-121">Alleen deze gebruikers kunnen computers toohello beheerd domein toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7602d-121">Only these users can join computers toohello managed domain.</span></span>

```bash
kinit ahmet@mydomain.com
```

### <a name="join-hello-machine-toohello-domain"></a><span data-ttu-id="7602d-122">Lid worden van Hallo machine toohello domein</span><span class="sxs-lookup"><span data-stu-id="7602d-122">Join hello machine toohello domain</span></span>

```bash
sudo realm join --verbose mydomain.com -U 'ahmet@mydomain.com'
```

### <a name="verify-hello-machine-is-joined-toohello-domain"></a><span data-ttu-id="7602d-123">Controleer of de machine Hallo gekoppelde toohello domein</span><span class="sxs-lookup"><span data-stu-id="7602d-123">Verify hello machine is joined toohello domain</span></span>

```bash
ssh -l ahmet@mydomain.com mydomain.cloudapp.net
```

## <a name="next-steps"></a><span data-ttu-id="7602d-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7602d-124">Next Steps</span></span>

* [<span data-ttu-id="7602d-125">Red Hat Update-infrastructuur (RHUI) voor on-demand Red Hat Enterprise Linux virtuele machines in Azure</span><span class="sxs-lookup"><span data-stu-id="7602d-125">Red Hat Update Infrastructure (RHUI) for on-demand Red Hat Enterprise Linux VMs in Azure</span></span>](update-infrastructure-redhat.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7602d-126">Sleutelkluis instellen voor virtuele machines in Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7602d-126">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>](key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7602d-127">Implementeren en beheren van virtuele machines met behulp van Azure Resource Manager-sjablonen en hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7602d-127">Deploy and manage virtual machines by using Azure Resource Manager templates and hello Azure CLI</span></span>](../linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

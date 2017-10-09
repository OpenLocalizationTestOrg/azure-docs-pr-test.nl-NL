---
title: aaaIntroduction tooFreeBSD in Azure | Microsoft Docs
description: Meer informatie over het gebruik van FreeBSD virtuele machines in Azure
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 32b87a5f-d024-4da0-8bf0-77e233d1422b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: kyliel
ms.openlocfilehash: eab7aeda7f7ef893740b39c0250aacc29d6fd71b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toofreebsd-on-azure"></a><span data-ttu-id="b6f69-103">TooFreeBSD inleiding op Azure</span><span class="sxs-lookup"><span data-stu-id="b6f69-103">Introduction tooFreeBSD on Azure</span></span>
<span data-ttu-id="b6f69-104">Dit onderwerp bevat een overzicht van een FreeBSD virtuele machine in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b6f69-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="b6f69-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="b6f69-105">Overview</span></span>
<span data-ttu-id="b6f69-106">FreeBSD voor Microsoft Azure is dat een geavanceerde computerbesturingssysteem gebruikt toopower moderne servers, desktops en ingesloten platforms.</span><span class="sxs-lookup"><span data-stu-id="b6f69-106">FreeBSD for Microsoft Azure is an advanced computer operating system used toopower modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="b6f69-107">Microsoft Corporation is afbeeldingen van FreeBSD beschikbaar maken op Azure Hello [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) vooraf is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b6f69-107">Microsoft Corporation is making images of FreeBSD available on Azure with hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="b6f69-108">Op dit moment wordt hello volgende FreeBSD versies aangeboden als afbeeldingen door Microsoft:</span><span class="sxs-lookup"><span data-stu-id="b6f69-108">Currently, hello following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="b6f69-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="b6f69-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="b6f69-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="b6f69-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="b6f69-111">Hallo-agent is verantwoordelijk voor de communicatie tussen Hallo FreeBSD VM en hello Azure-infrastructuur voor bewerkingen, zoals inrichten Hallo VM op het eerste gebruik (gebruikersnaam, wachtwoord of SSH-sleutel, hostnaam, enz.) en het inschakelen van de functionaliteit voor selectief VM-extensies.</span><span class="sxs-lookup"><span data-stu-id="b6f69-111">hello agent is responsible for communication between hello FreeBSD VM and hello Azure fabric for operations such as provisioning hello VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="b6f69-112">Als voor toekomstige versies van FreeBSD Hallo-strategie is de huidige toostay en Hallo meest recente versies beschikbaar kort nadat deze zijn gepubliceerd door Hallo FreeBSD release engineering team.</span><span class="sxs-lookup"><span data-stu-id="b6f69-112">As for future versions of FreeBSD, hello strategy is toostay current and make hello latest releases available shortly after they are published by hello FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="b6f69-113">Een FreeBSD virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="b6f69-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="b6f69-114">Een FreeBSD virtuele machine implementeert, is een eenvoudig proces met behulp van een installatiekopie van hello Azure Marketplace van hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="b6f69-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from hello Azure Marketplace from hello Azure portal:</span></span>

- [<span data-ttu-id="b6f69-115">FreeBSD 10.3 op Hallo Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="b6f69-115">FreeBSD 10.3 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="b6f69-116">FreeBSD 11.0 op Hallo Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="b6f69-116">FreeBSD 11.0 on hello Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="b6f69-117">Een FreeBSD virtuele machine via Azure CLI 2.0 in FreeBSD maken</span><span class="sxs-lookup"><span data-stu-id="b6f69-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="b6f69-118">U moet eerst tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Hoewel de volgende opdracht op een machine FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="b6f69-118">First you need tooinstall [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="b6f69-119">Als bash niet is geïnstalleerd op uw machine FreeBSD, voert u de volgende opdracht voorafgaand aan installatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="b6f69-119">If bash is not installed on your FreeBSD machine, run following command before hello installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="b6f69-120">Als python niet is geïnstalleerd op uw machine FreeBSD, voert u de volgende opdrachten voorafgaand aan installatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="b6f69-120">If python is not installed on your FreeBSD machine, run following commands before hello installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="b6f69-121">U wordt gevraagd tijdens de installatie van Hallo `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="b6f69-121">During hello installation, you are asked `Modify profile tooupdate your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="b6f69-122">Als u beantwoorden `y` en voer `/etc/rc.conf` als `a path tooan rc file tooupdate`, u wellicht voldoen aan de Hallo probleem `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="b6f69-122">If you answer `y` and enter `/etc/rc.conf` as `a path tooan rc file tooupdate`, you may meet hello problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="b6f69-123">tooresolve dit probleem, moet u Hallo schrijven rechts toocurrent gebruiker tegen Hallo bestand toekennen `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="b6f69-123">tooresolve this problem, you should grant hello write right toocurrent user against hello file `etc/rc.conf`.</span></span>

<span data-ttu-id="b6f69-124">U kunt nu aanmelden met Azure en uw FreeBSD VM maken.</span><span class="sxs-lookup"><span data-stu-id="b6f69-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="b6f69-125">Hieronder volgt een voorbeeld toocreate een FreeBSD 11.0 VM.</span><span class="sxs-lookup"><span data-stu-id="b6f69-125">Below is an example toocreate a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="b6f69-126">U kunt ook de parameter Hallo toevoegen `--public-ip-address-dns-name` met een globaal unieke DNS-naam voor een nieuwe openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="b6f69-126">You can also add hello parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="b6f69-127">U kunt vervolgens tooyour FreeBSD VM via Hallo IP-adres dat in de uitvoer Hallo van hierboven implementatie afgedrukt aanmelden.</span><span class="sxs-lookup"><span data-stu-id="b6f69-127">Then you can log in tooyour FreeBSD VM through hello ip address that printed in hello output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="b6f69-128">VM-extensies voor FreeBSD</span><span class="sxs-lookup"><span data-stu-id="b6f69-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="b6f69-129">Hieronder vindt u ondersteunde VM-extensies in FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="b6f69-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="b6f69-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="b6f69-130">VMAccess</span></span>
<span data-ttu-id="b6f69-131">Hallo [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) uitbreiding kunt:</span><span class="sxs-lookup"><span data-stu-id="b6f69-131">hello [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="b6f69-132">Hallo-wachtwoord opnieuw instellen van Hallo oorspronkelijke sudo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b6f69-132">Reset hello password of hello original sudo user.</span></span>
* <span data-ttu-id="b6f69-133">Maak een nieuwe gebruiker van de sudo met Hallo wachtwoord opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b6f69-133">Create a new sudo user with hello password specified.</span></span>
* <span data-ttu-id="b6f69-134">Stel Hallo van de openbare hostsleutel met Hallo sleutel opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b6f69-134">Set hello public host key with hello key given.</span></span>
* <span data-ttu-id="b6f69-135">Opnieuw instellen Hallo van de openbare hostsleutel opgegeven tijdens de VM-inrichting als Hallo host-sleutel is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b6f69-135">Reset hello public host key provided during VM provisioning if hello host key is not provided.</span></span>
* <span data-ttu-id="b6f69-136">Open Hallo SSH-poort (22) en Hallo sshd_config herstellen als reset_ssh tootrue is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b6f69-136">Open hello SSH port (22) and restore hello sshd_config if reset_ssh is set tootrue.</span></span>
* <span data-ttu-id="b6f69-137">Verwijder bestaande Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b6f69-137">Remove hello existing user.</span></span>
* <span data-ttu-id="b6f69-138">Controleer de schijven.</span><span class="sxs-lookup"><span data-stu-id="b6f69-138">Check disks.</span></span>
* <span data-ttu-id="b6f69-139">Een extra schijf repareren.</span><span class="sxs-lookup"><span data-stu-id="b6f69-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="b6f69-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="b6f69-140">CustomScript</span></span>
<span data-ttu-id="b6f69-141">Hallo [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) uitbreiding kunt:</span><span class="sxs-lookup"><span data-stu-id="b6f69-141">hello [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="b6f69-142">Indien opgegeven, download u Hallo aangepaste scripts van Azure Storage of een externe openbare opslag (bijvoorbeeld GitHub).</span><span class="sxs-lookup"><span data-stu-id="b6f69-142">If provided, download hello customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="b6f69-143">Hallo vermelding punt script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b6f69-143">Run hello entry point script.</span></span>
* <span data-ttu-id="b6f69-144">Ondersteuning voor inline-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="b6f69-144">Support inline commands.</span></span>
* <span data-ttu-id="b6f69-145">Windows-stijl nieuwe regel in de schaal en Python-scripts automatisch converteren.</span><span class="sxs-lookup"><span data-stu-id="b6f69-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="b6f69-146">Verwijder BOM automatisch in de shell- en Python-scripts.</span><span class="sxs-lookup"><span data-stu-id="b6f69-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="b6f69-147">Gevoelige gegevens in CommandToExecute beveiligd.</span><span class="sxs-lookup"><span data-stu-id="b6f69-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="b6f69-148">FreeBSD VM ondersteunt alleen CustomScript versie 1.x nu.</span><span class="sxs-lookup"><span data-stu-id="b6f69-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="b6f69-149">Verificatie: gebruikersnamen, wachtwoorden en SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="b6f69-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="b6f69-150">Wanneer u een FreeBSD virtuele machine met behulp van hello Azure-portal maakt, moet u een gebruikersnaam, wachtwoord of openbare SSH-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="b6f69-150">When you're creating a FreeBSD virtual machine by using hello Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="b6f69-151">Gebruikersnamen voor het implementeren van een FreeBSD virtuele machine in Azure mag niet overeenkomen met de namen van systeemaccounts (UID < 100) al aanwezig in Hallo virtuele machine ('root', bijvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="b6f69-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in hello virtual machine ("root", for example).</span></span>
<span data-ttu-id="b6f69-152">Alleen Hallo RSA SSH-sleutel wordt momenteel ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b6f69-152">Currently, only hello RSA SSH key is supported.</span></span> <span data-ttu-id="b6f69-153">Een SSH-sleutel met meerdere regels moet beginnen met `---- BEGIN SSH2 PUBLIC KEY ----` en eindigen met `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="b6f69-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="b6f69-154">Het verkrijgen van supergebruiker bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="b6f69-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="b6f69-155">Hallo-gebruikersaccount dat is opgegeven tijdens de implementatie van de virtuele machine-exemplaar in Azure is een bevoegd account.</span><span class="sxs-lookup"><span data-stu-id="b6f69-155">hello user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="b6f69-156">Hallo pakket van sudo is geïnstalleerd Hallo gepubliceerd FreeBSD installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b6f69-156">hello package of sudo was installed in hello published FreeBSD image.</span></span>
<span data-ttu-id="b6f69-157">Nadat u bent aangemeld via dit gebruikersaccount, kunt u opdrachten uitvoeren als hoofdmap door Hallo opdrachtsyntaxis.</span><span class="sxs-lookup"><span data-stu-id="b6f69-157">After you're logged in through this user account, you can run commands as root by using hello command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="b6f69-158">U kunt desgewenst een shell basis verkrijgen via `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="b6f69-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="b6f69-159">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="b6f69-159">Known issues</span></span>
<span data-ttu-id="b6f69-160">Hallo [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) versie 2.2.2 heeft een [bekend probleem] (https://github.com/Azure/WALinuxAgent/pull/517) die ervoor zorgt dat Hallo inrichten fout voor FreeBSD VM op Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f69-160">hello [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes hello provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="b6f69-161">Hallo werd fix vastgelegd door [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) versie 2.2.3 en latere versies.</span><span class="sxs-lookup"><span data-stu-id="b6f69-161">hello fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b6f69-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b6f69-162">Next steps</span></span>
* <span data-ttu-id="b6f69-163">Ga te[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate een FreeBSD VM.</span><span class="sxs-lookup"><span data-stu-id="b6f69-163">Go too[Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) toocreate a FreeBSD VM.</span></span>
* <span data-ttu-id="b6f69-164">Als u uw eigen tooAzure FreeBSD toobring wilt, Raadpleeg te[maken en uploaden een tooAzure FreeBSD VHD](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="b6f69-164">If you want toobring your own FreeBSD tooAzure, refer too[Create and upload a FreeBSD VHD tooAzure](linux/classic/freebsd-create-upload-vhd.md).</span></span>

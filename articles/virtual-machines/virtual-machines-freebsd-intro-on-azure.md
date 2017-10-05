---
title: Inleiding tot FreeBSD in Azure | Microsoft Docs
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
ms.openlocfilehash: d0fc5de34f7d9e5a607495eb97d9e35dc9eb21f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-freebsd-on-azure"></a><span data-ttu-id="12016-103">Inleiding tot FreeBSD op Azure</span><span class="sxs-lookup"><span data-stu-id="12016-103">Introduction to FreeBSD on Azure</span></span>
<span data-ttu-id="12016-104">Dit onderwerp bevat een overzicht van een FreeBSD virtuele machine in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="12016-104">This topic provides an overview of running a FreeBSD virtual machine in Azure.</span></span>

## <a name="overview"></a><span data-ttu-id="12016-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="12016-105">Overview</span></span>
<span data-ttu-id="12016-106">FreeBSD voor Microsoft Azure is een geavanceerde computerbesturingssysteem gebruikt voor power moderne servers, desktops, en ingesloten platforms.</span><span class="sxs-lookup"><span data-stu-id="12016-106">FreeBSD for Microsoft Azure is an advanced computer operating system used to power modern servers, desktops, and embedded platforms.</span></span>

<span data-ttu-id="12016-107">Microsoft Corporation is afbeeldingen van FreeBSD beschikbaar maken op Azure met de [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) vooraf is geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="12016-107">Microsoft Corporation is making images of FreeBSD available on Azure with the [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) pre-configured.</span></span> <span data-ttu-id="12016-108">Op dit moment wordt worden de volgende versies van FreeBSD als afbeeldingen aangeboden door Microsoft:</span><span class="sxs-lookup"><span data-stu-id="12016-108">Currently, the following FreeBSD versions are offered as images by Microsoft:</span></span>

- <span data-ttu-id="12016-109">FreeBSD 10.3-RELEASE</span><span class="sxs-lookup"><span data-stu-id="12016-109">FreeBSD 10.3-RELEASE</span></span>
- <span data-ttu-id="12016-110">FreeBSD 11.0-RELEASE</span><span class="sxs-lookup"><span data-stu-id="12016-110">FreeBSD 11.0-RELEASE</span></span>

<span data-ttu-id="12016-111">De agent is verantwoordelijk voor de communicatie tussen de VM FreeBSD en de Azure-infrastructuur voor bewerkingen, zoals de inrichting van de virtuele machine bij het eerste gebruik (gebruikersnaam, wachtwoord of SSH-sleutel, hostnaam, enzovoort) en functionaliteit voor selectieve VM-extensies in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="12016-111">The agent is responsible for communication between the FreeBSD VM and the Azure fabric for operations such as provisioning the VM on first use (user name, password or SSH key, host name, etc.) and enabling functionality for selective VM extensions.</span></span>

<span data-ttu-id="12016-112">Als voor toekomstige versies van FreeBSD is de strategie Blijf en de meest recente versies beschikbaar kort nadat ze zijn gepubliceerd door het technische team van FreeBSD release.</span><span class="sxs-lookup"><span data-stu-id="12016-112">As for future versions of FreeBSD, the strategy is to stay current and make the latest releases available shortly after they are published by the FreeBSD release engineering team.</span></span>

## <a name="deploying-a-freebsd-virtual-machine"></a><span data-ttu-id="12016-113">Een FreeBSD virtuele machine implementeren</span><span class="sxs-lookup"><span data-stu-id="12016-113">Deploying a FreeBSD virtual machine</span></span>
<span data-ttu-id="12016-114">Een FreeBSD virtuele machine implementeert, is een eenvoudig proces met behulp van een afbeelding uit Azure Marketplace vanuit de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="12016-114">Deploying a FreeBSD virtual machine is a straightforward process using an image from the Azure Marketplace from the Azure portal:</span></span>

- [<span data-ttu-id="12016-115">FreeBSD 10.3 op de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="12016-115">FreeBSD 10.3 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
- [<span data-ttu-id="12016-116">FreeBSD 11.0 op de Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="12016-116">FreeBSD 11.0 on the Azure Marketplace</span></span>](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/)

### <a name="create-a-freebsd-vm-through-azure-cli-20-on-freebsd"></a><span data-ttu-id="12016-117">Een FreeBSD virtuele machine via Azure CLI 2.0 in FreeBSD maken</span><span class="sxs-lookup"><span data-stu-id="12016-117">Create a FreeBSD VM through Azure CLI 2.0 on FreeBSD</span></span>
<span data-ttu-id="12016-118">U moet eerst installeren [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) Hoewel de volgende opdracht op een machine FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="12016-118">First you need to install [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) though following command on a FreeBSD machine.</span></span>

```bash 
    curl -L https://aka.ms/InstallAzureCli | bash
```

<span data-ttu-id="12016-119">Als bash niet is geïnstalleerd op uw machine FreeBSD, voert u de volgende opdracht voordat de installatie.</span><span class="sxs-lookup"><span data-stu-id="12016-119">If bash is not installed on your FreeBSD machine, run following command before the installation.</span></span> 

```
    sudo pkg install bash
```

<span data-ttu-id="12016-120">Als python niet is geïnstalleerd op uw machine FreeBSD, voert u de volgende opdrachten voordat de installatie.</span><span class="sxs-lookup"><span data-stu-id="12016-120">If python is not installed on your FreeBSD machine, run following commands before the installation.</span></span> 

```
    sudo pkg install python35
    cd /usr/local/bin 
    sudo rm /usr/local/bin/python 
    sudo ln -s /usr/local/bin/python3.5 /usr/local/bin/python
```

<span data-ttu-id="12016-121">Tijdens de installatie wordt u gevraagd `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span><span class="sxs-lookup"><span data-stu-id="12016-121">During the installation, you are asked `Modify profile to update your $PATH and enable shell/tab completion now? (Y/n)`.</span></span> <span data-ttu-id="12016-122">Als u beantwoorden `y` en voer `/etc/rc.conf` als `a path to an rc file to update`, u kunt het probleem wellicht voldoen aan `ERROR: [Errno 13] Permission denied`.</span><span class="sxs-lookup"><span data-stu-id="12016-122">If you answer `y` and enter `/etc/rc.conf` as `a path to an rc file to update`, you may meet the problem `ERROR: [Errno 13] Permission denied`.</span></span> <span data-ttu-id="12016-123">U lost dit probleem, moet u de voor schrijven verlenen recht op de huidige gebruiker op basis van het bestand `etc/rc.conf`.</span><span class="sxs-lookup"><span data-stu-id="12016-123">To resolve this problem, you should grant the write right to current user against the file `etc/rc.conf`.</span></span>

<span data-ttu-id="12016-124">U kunt nu aanmelden met Azure en uw FreeBSD VM maken.</span><span class="sxs-lookup"><span data-stu-id="12016-124">Now you can log in Azure and create your FreeBSD VM.</span></span> <span data-ttu-id="12016-125">Hieronder volgt een voorbeeld van een FreeBSD 11.0 virtuele machine maken.</span><span class="sxs-lookup"><span data-stu-id="12016-125">Below is an example to create a FreeBSD 11.0 VM.</span></span> <span data-ttu-id="12016-126">U kunt ook de parameter toevoegen `--public-ip-address-dns-name` met een globaal unieke DNS-naam voor een nieuwe openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="12016-126">You can also add the parameter `--public-ip-address-dns-name` with a globally unique DNS name for a newly created Public IP.</span></span> 

```azurecli
    az login 
    az group create -n myResourceGroup -l westus az vm create -n myFreeBSD11 -g myResourceGroup --image MicrosoftOSTC:FreeBSD:11.0:latest --admin-username azureuser --ssh-key-value /etc/ssh/ssh_host_rsa_key.pub 
```

<span data-ttu-id="12016-127">Vervolgens kunt u aanmelden bij uw FreeBSD VM via het IP-adres dat in de uitvoer van hierboven implementatie afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="12016-127">Then you can log in to your FreeBSD VM through the ip address that printed in the output of above deployment.</span></span> 

```bash
    ssh azureuser@xx.xx.xx.xx -i /etc/ssh/ssh_host_rsa_key
```   

## <a name="vm-extensions-for-freebsd"></a><span data-ttu-id="12016-128">VM-extensies voor FreeBSD</span><span class="sxs-lookup"><span data-stu-id="12016-128">VM extensions for FreeBSD</span></span>
<span data-ttu-id="12016-129">Hieronder vindt u ondersteunde VM-extensies in FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="12016-129">Following are supported VM extensions in FreeBSD.</span></span>

### <a name="vmaccess"></a><span data-ttu-id="12016-130">VMAccess</span><span class="sxs-lookup"><span data-stu-id="12016-130">VMAccess</span></span>
<span data-ttu-id="12016-131">De [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) uitbreiding kunt:</span><span class="sxs-lookup"><span data-stu-id="12016-131">The [VMAccess](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) extension can:</span></span>

* <span data-ttu-id="12016-132">Het wachtwoord van de oorspronkelijke sudo-gebruiker opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="12016-132">Reset the password of the original sudo user.</span></span>
* <span data-ttu-id="12016-133">Maak een nieuwe gebruiker met sudo met het wachtwoord opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12016-133">Create a new sudo user with the password specified.</span></span>
* <span data-ttu-id="12016-134">Stel de sleutel van de openbare host met de sleutel die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12016-134">Set the public host key with the key given.</span></span>
* <span data-ttu-id="12016-135">Instellen van de sleutel van de openbare host is opgegeven tijdens het inrichten van virtuele machine als de sleutel van de host is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="12016-135">Reset the public host key provided during VM provisioning if the host key is not provided.</span></span>
* <span data-ttu-id="12016-136">Open de SSH-poort (22) en herstel van de sshd_config als reset_ssh is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="12016-136">Open the SSH port (22) and restore the sshd_config if reset_ssh is set to true.</span></span>
* <span data-ttu-id="12016-137">Verwijder de bestaande gebruiker.</span><span class="sxs-lookup"><span data-stu-id="12016-137">Remove the existing user.</span></span>
* <span data-ttu-id="12016-138">Controleer de schijven.</span><span class="sxs-lookup"><span data-stu-id="12016-138">Check disks.</span></span>
* <span data-ttu-id="12016-139">Een extra schijf repareren.</span><span class="sxs-lookup"><span data-stu-id="12016-139">Repair an added disk.</span></span>

### <a name="customscript"></a><span data-ttu-id="12016-140">CustomScript</span><span class="sxs-lookup"><span data-stu-id="12016-140">CustomScript</span></span>
<span data-ttu-id="12016-141">De [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) uitbreiding kunt:</span><span class="sxs-lookup"><span data-stu-id="12016-141">The [CustomScript](https://github.com/Azure/azure-linux-extensions/tree/master/CustomScript) extension can:</span></span>

* <span data-ttu-id="12016-142">Indien opgegeven, moet u aangepaste scripts downloaden van Azure Storage of een externe openbare opslag (bijvoorbeeld GitHub).</span><span class="sxs-lookup"><span data-stu-id="12016-142">If provided, download the customized scripts from Azure Storage or external public storage (for example, GitHub).</span></span>
* <span data-ttu-id="12016-143">Voer het script post-punt.</span><span class="sxs-lookup"><span data-stu-id="12016-143">Run the entry point script.</span></span>
* <span data-ttu-id="12016-144">Ondersteuning voor inline-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="12016-144">Support inline commands.</span></span>
* <span data-ttu-id="12016-145">Windows-stijl nieuwe regel in de schaal en Python-scripts automatisch converteren.</span><span class="sxs-lookup"><span data-stu-id="12016-145">Convert Windows-style newline in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="12016-146">Verwijder BOM automatisch in de shell- en Python-scripts.</span><span class="sxs-lookup"><span data-stu-id="12016-146">Remove BOM in shell and Python scripts automatically.</span></span>
* <span data-ttu-id="12016-147">Gevoelige gegevens in CommandToExecute beveiligd.</span><span class="sxs-lookup"><span data-stu-id="12016-147">Protect sensitive data in CommandToExecute.</span></span>

> [!NOTE]
> <span data-ttu-id="12016-148">FreeBSD VM ondersteunt alleen CustomScript versie 1.x nu.</span><span class="sxs-lookup"><span data-stu-id="12016-148">FreeBSD VM only supports CustomScript version 1.x by now.</span></span>  

## <a name="authentication-user-names-passwords-and-ssh-keys"></a><span data-ttu-id="12016-149">Verificatie: gebruikersnamen, wachtwoorden en SSH-sleutels</span><span class="sxs-lookup"><span data-stu-id="12016-149">Authentication: user names, passwords, and SSH keys</span></span>
<span data-ttu-id="12016-150">Wanneer u een FreeBSD virtuele machine met behulp van de Azure-portal maakt, moet u een gebruikersnaam, wachtwoord of openbare SSH-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="12016-150">When you're creating a FreeBSD virtual machine by using the Azure portal, you must provide a user name, password, or SSH public key.</span></span>
<span data-ttu-id="12016-151">Gebruikersnamen voor het implementeren van een FreeBSD virtuele machine in Azure mag niet overeenkomen met de namen van systeemaccounts (UID < 100) al aanwezig in de virtuele machine ('root', bijvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="12016-151">User names for deploying a FreeBSD virtual machine on Azure must not match names of system accounts (UID <100) already present in the virtual machine ("root", for example).</span></span>
<span data-ttu-id="12016-152">Alleen de RSA SSH-sleutel wordt momenteel ondersteund.</span><span class="sxs-lookup"><span data-stu-id="12016-152">Currently, only the RSA SSH key is supported.</span></span> <span data-ttu-id="12016-153">Een SSH-sleutel met meerdere regels moet beginnen met `---- BEGIN SSH2 PUBLIC KEY ----` en eindigen met `---- END SSH2 PUBLIC KEY ----`.</span><span class="sxs-lookup"><span data-stu-id="12016-153">A multiline SSH key must begin with `---- BEGIN SSH2 PUBLIC KEY ----` and end with `---- END SSH2 PUBLIC KEY ----`.</span></span>

## <a name="obtaining-superuser-privileges"></a><span data-ttu-id="12016-154">Het verkrijgen van supergebruiker bevoegdheden</span><span class="sxs-lookup"><span data-stu-id="12016-154">Obtaining superuser privileges</span></span>
<span data-ttu-id="12016-155">Het gebruikersaccount dat is opgegeven tijdens de implementatie van de virtuele machine-exemplaar in Azure is een bevoegd account.</span><span class="sxs-lookup"><span data-stu-id="12016-155">The user account that is specified during virtual machine instance deployment on Azure is a privileged account.</span></span> <span data-ttu-id="12016-156">Het pakket van sudo is geïnstalleerd in de installatiekopie van het gepubliceerde FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="12016-156">The package of sudo was installed in the published FreeBSD image.</span></span>
<span data-ttu-id="12016-157">Nadat u bent aangemeld via dit gebruikersaccount, kunt u opdrachten uitvoeren als hoofdmap met behulp van de syntaxis van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="12016-157">After you're logged in through this user account, you can run commands as root by using the command syntax.</span></span>

```
    $ sudo <COMMAND>
```

<span data-ttu-id="12016-158">U kunt desgewenst een shell basis verkrijgen via `sudo -s`.</span><span class="sxs-lookup"><span data-stu-id="12016-158">You can optionally obtain a root shell by using `sudo -s`.</span></span>

## <a name="known-issues"></a><span data-ttu-id="12016-159">Bekende problemen</span><span class="sxs-lookup"><span data-stu-id="12016-159">Known issues</span></span>
<span data-ttu-id="12016-160">De [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) versie 2.2.2 heeft een [bekend probleem] (https://github.com/Azure/WALinuxAgent/pull/517) die ervoor zorgt dat de fout inrichten voor FreeBSD VM op Azure.</span><span class="sxs-lookup"><span data-stu-id="12016-160">The [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.2 has a [known issue] (https://github.com/Azure/WALinuxAgent/pull/517) that causes the provision failure for FreeBSD VM on Azure.</span></span> <span data-ttu-id="12016-161">De oplossing is vastgelegd door [Azure VM-Gastagent](https://github.com/Azure/WALinuxAgent/) versie 2.2.3 en latere versies.</span><span class="sxs-lookup"><span data-stu-id="12016-161">The fix was captured by [Azure VM Guest Agent](https://github.com/Azure/WALinuxAgent/) version 2.2.3 and later releases.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="12016-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12016-162">Next steps</span></span>
* <span data-ttu-id="12016-163">Ga naar [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) een FreeBSD VM's te maken.</span><span class="sxs-lookup"><span data-stu-id="12016-163">Go to [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd110/) to create a FreeBSD VM.</span></span>
* <span data-ttu-id="12016-164">Als u zorgen dat uw eigen FreeBSD op Azure wilt, raadpleegt u [een FreeBSD VHD naar Azure maken en uploaden](linux/classic/freebsd-create-upload-vhd.md).</span><span class="sxs-lookup"><span data-stu-id="12016-164">If you want to bring your own FreeBSD to Azure, refer to [Create and upload a FreeBSD VHD to Azure](linux/classic/freebsd-create-upload-vhd.md).</span></span>

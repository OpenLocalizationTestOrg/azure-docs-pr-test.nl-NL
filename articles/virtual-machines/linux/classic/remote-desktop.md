---
title: Extern bureaublad voor een virtuele Linux-machine | Microsoft Docs
description: Meer informatie over het installeren en configureren van extern bureaublad verbinding maken met een Microsoft Azure Linux VM voor het klassieke implementatiemodel
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 34348659-ddb7-41da-82d6-b5885859e7e4
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: mingzhan
ms.openlocfilehash: 68031d548bdbeda9a83d1bceaaea7c5bbcab3188
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-remote-desktop-to-connect-to-a-microsoft-azure-linux-vm"></a><span data-ttu-id="46262-103">Extern bureaublad gebruiken om verbinding te maken met een Microsoft Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="46262-103">Using Remote Desktop to connect to a Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="46262-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="46262-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="46262-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="46262-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="46262-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46262-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="46262-107">Zie voor de bijgewerkte Resource Manager-versie van dit artikel, [hier](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="46262-107">For the updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="46262-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="46262-108">Overview</span></span>
<span data-ttu-id="46262-109">RDP (Remote Desktop Protocol) is een oorspronkelijk protocol gebruikt voor Windows.</span><span class="sxs-lookup"><span data-stu-id="46262-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="46262-110">Hoe kunnen we RDP extern verbinding kunnen maken met een Linux-VM (virtuele machine) gebruiken</span><span class="sxs-lookup"><span data-stu-id="46262-110">How can we use RDP to connect to a Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="46262-111">In deze richtlijnen bieden u het antwoord!</span><span class="sxs-lookup"><span data-stu-id="46262-111">This guidance will give you the answer!</span></span> <span data-ttu-id="46262-112">Het helpt u om te installeren en config-xrdp op uw Microsoft Azure Linux VM, waarmee u verbinding maken met extern bureaublad van een Windows-machine.</span><span class="sxs-lookup"><span data-stu-id="46262-112">It will help you to install and config xrdp on your Microsoft Azure Linux VM, which lets you connect to it with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="46262-113">Linux-VM met Ubuntu of OpenSUSE als in het voorbeeld in deze richtlijnen zullen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="46262-113">We will use Linux VM running Ubuntu or OpenSUSE as the example in this guidance.</span></span>

<span data-ttu-id="46262-114">Het hulpprogramma xrdp is een open-source RDP-server waarmee u verbinding maken met de Linux-server met extern bureaublad van een Windows-machine.</span><span class="sxs-lookup"><span data-stu-id="46262-114">The xrdp tool is an open source RDP server that allows you to connect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="46262-115">RDP heeft betere prestaties dan VNC (virtuele netwerk computers).</span><span class="sxs-lookup"><span data-stu-id="46262-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="46262-116">VNC renders met JPEG-kwaliteit afbeeldingen en kan traag zijn, terwijl RDP snel en crystal wissen is.</span><span class="sxs-lookup"><span data-stu-id="46262-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="46262-117">U moet al een Microsoft Azure-virtuele machine met Linux hebben.</span><span class="sxs-lookup"><span data-stu-id="46262-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="46262-118">Als u wilt maken en een Linux-VM instellen, Zie de [Azure Linux VM-zelfstudie](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="46262-118">To create and set up a Linux VM, see the [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="46262-119">Een eindpunt voor extern bureaublad maken</span><span class="sxs-lookup"><span data-stu-id="46262-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="46262-120">We gebruiken het standaardeindpunt 3389 voor extern bureaublad in dit document.</span><span class="sxs-lookup"><span data-stu-id="46262-120">We will use the default endpoint 3389 for Remote Desktop in this doc.</span></span> <span data-ttu-id="46262-121">Instellen van 3389 eindpunt als `Remote Desktop` voor uw Linux-VM zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="46262-121">Set up 3389 endpoint as `Remote Desktop` to your Linux VM like below:</span></span>

![Afbeelding](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="46262-123">Als u niet hoe u een eindpunt voor de virtuele machine instelt weet, Zie [in deze richtlijnen](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="46262-123">If you don't know how to set up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="46262-124">Gnome bureaublad installeren</span><span class="sxs-lookup"><span data-stu-id="46262-124">Install Gnome Desktop</span></span>
<span data-ttu-id="46262-125">Verbinding maken met uw Linux-VM via `putty`, en installeer `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="46262-125">Connect to your Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="46262-126">Ubuntu, gebruikt u in:</span><span class="sxs-lookup"><span data-stu-id="46262-126">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="46262-127">Voor OpenSUSE, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="46262-127">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="46262-128">Xrdp installeren</span><span class="sxs-lookup"><span data-stu-id="46262-128">Install xrdp</span></span>
<span data-ttu-id="46262-129">Ubuntu, gebruikt u in:</span><span class="sxs-lookup"><span data-stu-id="46262-129">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="46262-130">Voor OpenSUSE, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="46262-130">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="46262-131">De versie van de OpenSUSE bijwerken met de versie die u in de volgende opdracht gebruikt.</span><span class="sxs-lookup"><span data-stu-id="46262-131">Update the OpenSUSE version with the version you are using in the following command.</span></span> <span data-ttu-id="46262-132">Het onderstaande voorbeeld is voor `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="46262-132">The example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="46262-133">Start xrdp en xdrp service ingesteld op opstartprocedure</span><span class="sxs-lookup"><span data-stu-id="46262-133">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="46262-134">Voor OpenSUSE, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="46262-134">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="46262-135">Voor Ubuntu, xrdp wordt gestart en eanbled op boot-up automatisch na de installatie.</span><span class="sxs-lookup"><span data-stu-id="46262-135">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="46262-136">Met behulp van xfce als u een virtuele Ubuntu-versie hoger is dan Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="46262-136">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="46262-137">Omdat de huidige versie van xrdp niet Gnome bureaublad voor Ubuntu-versies hoger is dan Ubuntu 12.04LTS ondersteunt, gebruiken we `xfce` bureaublad in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="46262-137">Because the current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="46262-138">Voor het installeren van `xfce`, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="46262-138">To install `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="46262-139">Schakel vervolgens `xfce` met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="46262-139">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="46262-140">Het configuratiebestand bewerken `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="46262-140">Edit the config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="46262-141">Voeg de regel `xfce4-session` voor de regel `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="46262-141">Add the line `xfce4-session` before the line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="46262-142">Als u wilt de xrdp-service opnieuw start, gebruiken deze:</span><span class="sxs-lookup"><span data-stu-id="46262-142">To restart the xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="46262-143">Verbinding maken met uw Linux-VM van een Windows-computer</span><span class="sxs-lookup"><span data-stu-id="46262-143">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="46262-144">Start de extern bureaublad-client in een Windows-computer en voer de naam van uw DNS-Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="46262-144">In a Windows machine, start the Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="46262-145">Of Ga naar het Dashboard van de virtuele machine in de Azure-portal en klik op `Connect` verbinding maken uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="46262-145">Or go to the Dashboard of your VM in the Azure portal and click `Connect` to connect your Linux VM.</span></span> <span data-ttu-id="46262-146">In dat geval ziet u het aanmeldingsvenster:</span><span class="sxs-lookup"><span data-stu-id="46262-146">In that case, you see the login window:</span></span>

![Afbeelding](./media/remote-desktop/no2.png)

<span data-ttu-id="46262-148">Aanmelden met de gebruikersnaam en wachtwoord van uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="46262-148">Log in with the user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46262-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46262-149">Next steps</span></span>
<span data-ttu-id="46262-150">Zie voor meer informatie over het gebruik van xrdp [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="46262-150">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>

---
title: aaaRemote bureaublad tooa Linux VM | Microsoft Docs
description: Meer informatie over hoe tooinstall en extern bureaublad tooconnect tooa Microsoft Azure Linux VM voor Hallo klassieke implementatiemodel configureren
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
ms.openlocfilehash: aadd6e87883cf9cacf9d198b680669d594206e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-tooconnect-tooa-microsoft-azure-linux-vm"></a><span data-ttu-id="37361-103">Met behulp van extern bureaublad tooconnect tooa Microsoft Azure Linux VM</span><span class="sxs-lookup"><span data-stu-id="37361-103">Using Remote Desktop tooconnect tooa Microsoft Azure Linux VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="37361-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="37361-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="37361-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="37361-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="37361-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="37361-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="37361-107">Voor Hallo Resource Manager-versie van dit artikel bijgewerkt, Zie [hier](../use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="37361-107">For hello updated Resource Manager version of this article, see [here](../use-remote-desktop.md).</span></span>

## <a name="overview"></a><span data-ttu-id="37361-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="37361-108">Overview</span></span>
<span data-ttu-id="37361-109">RDP (Remote Desktop Protocol) is een oorspronkelijk protocol gebruikt voor Windows.</span><span class="sxs-lookup"><span data-stu-id="37361-109">RDP (Remote Desktop Protocol) is a proprietary protocol used for Windows.</span></span> <span data-ttu-id="37361-110">Hoe kunnen we RDP tooconnect tooa Linux VM (virtuele machine) op afstand gebruiken?</span><span class="sxs-lookup"><span data-stu-id="37361-110">How can we use RDP tooconnect tooa Linux VM (virtual machine) remotely?</span></span>

<span data-ttu-id="37361-111">In deze richtlijnen krijgt u antwoord Hallo!</span><span class="sxs-lookup"><span data-stu-id="37361-111">This guidance will give you hello answer!</span></span> <span data-ttu-id="37361-112">Deze methode kunt u tooinstall en config xrdp op uw Microsoft Azure Linux VM, waarmee u tooit verbinding met extern bureaublad van een Windows-machine.</span><span class="sxs-lookup"><span data-stu-id="37361-112">It will help you tooinstall and config xrdp on your Microsoft Azure Linux VM, which lets you connect tooit with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="37361-113">Linux-VM met Ubuntu of OpenSUSE als voorbeeld in deze richtlijnen Hallo zullen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="37361-113">We will use Linux VM running Ubuntu or OpenSUSE as hello example in this guidance.</span></span>

<span data-ttu-id="37361-114">Hallo xrdp hulpprogramma is een open source RDP-server waarmee u tooconnect uw Linux-server met extern bureaublad van een Windows-machine.</span><span class="sxs-lookup"><span data-stu-id="37361-114">hello xrdp tool is an open source RDP server that allows you tooconnect your Linux server with Remote Desktop from a Windows machine.</span></span> <span data-ttu-id="37361-115">RDP heeft betere prestaties dan VNC (virtuele netwerk computers).</span><span class="sxs-lookup"><span data-stu-id="37361-115">RDP has better performance than VNC (Virtual Network Computing).</span></span> <span data-ttu-id="37361-116">VNC renders met JPEG-kwaliteit afbeeldingen en kan traag zijn, terwijl RDP snel en crystal wissen is.</span><span class="sxs-lookup"><span data-stu-id="37361-116">VNC renders using JPEG-quality graphics and can be slow, whereas RDP is fast and crystal clear.</span></span>

> [!NOTE]
> <span data-ttu-id="37361-117">U moet al een Microsoft Azure-virtuele machine met Linux hebben.</span><span class="sxs-lookup"><span data-stu-id="37361-117">You must already have an Microsoft Azure VM running Linux.</span></span> <span data-ttu-id="37361-118">Zie toocreate en instellen van een Linux-VM Hallo [Azure Linux VM-zelfstudie](createportal.md).</span><span class="sxs-lookup"><span data-stu-id="37361-118">toocreate and set up a Linux VM, see hello [Azure Linux VM tutorial](createportal.md).</span></span>
> 
> 

## <a name="create-an-endpoint-for-remote-desktop"></a><span data-ttu-id="37361-119">Een eindpunt voor extern bureaublad maken</span><span class="sxs-lookup"><span data-stu-id="37361-119">Create an endpoint for Remote Desktop</span></span>
<span data-ttu-id="37361-120">We gebruiken het standaardeindpunt Hallo 3389 voor extern bureaublad in dit document. Instellen van 3389 eindpunt als `Remote Desktop` tooyour Linux VM, zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="37361-120">We will use hello default endpoint 3389 for Remote Desktop in this doc. Set up 3389 endpoint as `Remote Desktop` tooyour Linux VM like below:</span></span>

![Afbeelding](./media/remote-desktop/endpoint-for-linux-server.png)

<span data-ttu-id="37361-122">Als u niet weet hoe tooset u een eindpunt voor de virtuele machine, Zie [in deze richtlijnen](setup-endpoints.md).</span><span class="sxs-lookup"><span data-stu-id="37361-122">If you don't know how tooset up an endpoint for your VM, see [this guidance](setup-endpoints.md).</span></span>

## <a name="install-gnome-desktop"></a><span data-ttu-id="37361-123">Gnome bureaublad installeren</span><span class="sxs-lookup"><span data-stu-id="37361-123">Install Gnome Desktop</span></span>
<span data-ttu-id="37361-124">Verbinding maken met tooyour Linux VM via `putty`, en installeer `Gnome Desktop`.</span><span class="sxs-lookup"><span data-stu-id="37361-124">Connect tooyour Linux VM through `putty`, and install `Gnome Desktop`.</span></span>

<span data-ttu-id="37361-125">Ubuntu, gebruikt u in:</span><span class="sxs-lookup"><span data-stu-id="37361-125">For Ubuntu, use:</span></span>

    #sudo apt-get update
    #sudo apt-get install ubuntu-desktop


<span data-ttu-id="37361-126">Voor OpenSUSE, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="37361-126">For OpenSUSE, use:</span></span>

    #sudo zypper install gnome-session

## <a name="install-xrdp"></a><span data-ttu-id="37361-127">Xrdp installeren</span><span class="sxs-lookup"><span data-stu-id="37361-127">Install xrdp</span></span>
<span data-ttu-id="37361-128">Ubuntu, gebruikt u in:</span><span class="sxs-lookup"><span data-stu-id="37361-128">For Ubuntu, use:</span></span>

    #sudo apt-get install xrdp

<span data-ttu-id="37361-129">Voor OpenSUSE, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="37361-129">For OpenSUSE, use:</span></span>

> [!NOTE]
> <span data-ttu-id="37361-130">Hallo OpenSUSE versie met Hallo-versie die u gebruikt in de volgende opdracht Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="37361-130">Update hello OpenSUSE version with hello version you are using in hello following command.</span></span> <span data-ttu-id="37361-131">Hallo in het volgende voorbeeld is voor `OpenSUSE 13.2`.</span><span class="sxs-lookup"><span data-stu-id="37361-131">hello example below is for `OpenSUSE 13.2`.</span></span>
> 
> 

    #sudo zypper in http://download.opensuse.org/repositories/X11:/RemoteDesktop/openSUSE_13.2/x86_64/xrdp-0.9.0git.1401423964-2.1.x86_64.rpm
    #sudo zypper install tigervnc xorg-x11-Xvnc xterm remmina-plugin-vnc


## <a name="start-xrdp-and-set-xdrp-service-at-boot-up"></a><span data-ttu-id="37361-132">Start xrdp en xdrp service ingesteld op opstartprocedure</span><span class="sxs-lookup"><span data-stu-id="37361-132">Start xrdp and set xdrp service at boot-up</span></span>
<span data-ttu-id="37361-133">Voor OpenSUSE, gebruiken:</span><span class="sxs-lookup"><span data-stu-id="37361-133">For OpenSUSE, use:</span></span>

    #sudo systemctl start xrdp
    #sudo systemctl enable xrdp

<span data-ttu-id="37361-134">Voor Ubuntu, xrdp wordt gestart en eanbled op boot-up automatisch na de installatie.</span><span class="sxs-lookup"><span data-stu-id="37361-134">For Ubuntu, xrdp will be started and eanbled at boot-up automatically after installation.</span></span>

## <a name="using-xfce-if-you-are-using-an-ubuntu-version-later-than-ubuntu-1204lts"></a><span data-ttu-id="37361-135">Met behulp van xfce als u een virtuele Ubuntu-versie hoger is dan Ubuntu 12.04LTS</span><span class="sxs-lookup"><span data-stu-id="37361-135">Using xfce if you are using an Ubuntu version later than Ubuntu 12.04LTS</span></span>
<span data-ttu-id="37361-136">Omdat de huidige versie Hallo van xrdp niet Gnome bureaublad voor Ubuntu-versies hoger is dan Ubuntu 12.04LTS ondersteunt, gebruiken we `xfce` bureaublad in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="37361-136">Because hello current version of xrdp does not support Gnome Desktop for  Ubuntu versions later than Ubuntu 12.04LTS, we will use `xfce` Desktop instead.</span></span>

<span data-ttu-id="37361-137">tooinstall `xfce`, gebruikt u deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="37361-137">tooinstall `xfce`, use this command:</span></span>

    #sudo apt-get install xubuntu-desktop

<span data-ttu-id="37361-138">Schakel vervolgens `xfce` met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="37361-138">Then enable `xfce` using this command:</span></span>

    #echo xfce4-session >~/.xsession

<span data-ttu-id="37361-139">Hallo-configuratiebestand bewerken `/etc/xrdp/startwm.sh`:</span><span class="sxs-lookup"><span data-stu-id="37361-139">Edit hello config file `/etc/xrdp/startwm.sh`:</span></span>

    #sudo vi /etc/xrdp/startwm.sh   

<span data-ttu-id="37361-140">Hallo-regel toevoegen `xfce4-session` vóór Hallo regel `/etc/X11/Xsession`.</span><span class="sxs-lookup"><span data-stu-id="37361-140">Add hello line `xfce4-session` before hello line `/etc/X11/Xsession`.</span></span>

<span data-ttu-id="37361-141">toorestart hello xrdp service, gebruikt u dit:</span><span class="sxs-lookup"><span data-stu-id="37361-141">toorestart hello xrdp service, use this:</span></span>

    #sudo service xrdp restart


## <a name="connect-your-linux-vm-from-a-windows-machine"></a><span data-ttu-id="37361-142">Verbinding maken met uw Linux-VM van een Windows-computer</span><span class="sxs-lookup"><span data-stu-id="37361-142">Connect your Linux VM from a Windows machine</span></span>
<span data-ttu-id="37361-143">In een Windows-computer start Hallo extern bureaublad-client en voer de naam van uw DNS-Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="37361-143">In a Windows machine, start hello Remote Desktop client and input your Linux VM DNS name.</span></span> <span data-ttu-id="37361-144">Of Ga toohello Dashboard van de virtuele machine in hello Azure-portal en klik op `Connect` tooconnect uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="37361-144">Or go toohello Dashboard of your VM in hello Azure portal and click `Connect` tooconnect your Linux VM.</span></span> <span data-ttu-id="37361-145">In dat geval ziet u Hallo aanmeldingsvenster:</span><span class="sxs-lookup"><span data-stu-id="37361-145">In that case, you see hello login window:</span></span>

![Afbeelding](./media/remote-desktop/no2.png)

<span data-ttu-id="37361-147">Aanmelden met Hallo-gebruikersnaam en wachtwoord van uw Linux-VM.</span><span class="sxs-lookup"><span data-stu-id="37361-147">Log in with hello user name and password of your Linux VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37361-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37361-148">Next steps</span></span>
<span data-ttu-id="37361-149">Zie voor meer informatie over het gebruik van xrdp [http://www.xrdp.org/](http://www.xrdp.org/).</span><span class="sxs-lookup"><span data-stu-id="37361-149">For more information about using xrdp, see [http://www.xrdp.org/](http://www.xrdp.org/).</span></span>

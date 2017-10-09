---
title: aaaAzure Quick Start - VM-Portal maken | Microsoft Docs
description: Azure Quick Start - Een VM-portal maken
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a><span data-ttu-id="8918f-103">Een virtuele Linux-machine maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="8918f-103">Create a Linux virtual machine with hello Azure portal</span></span>

<span data-ttu-id="8918f-104">Azure virtuele machines kunnen worden gemaakt via hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8918f-104">Azure virtual machines can be created through hello Azure portal.</span></span> <span data-ttu-id="8918f-105">Deze methode biedt een gebruikersinterface op basis van een browser voor het maken en configureren van virtuele machines en alle verwante resources.</span><span class="sxs-lookup"><span data-stu-id="8918f-105">This method provides a browser-based user interface for creating and configuring virtual machines and all related resources.</span></span> <span data-ttu-id="8918f-106">Met deze stappen Quick Start via een virtuele machine maken en de installatie van een webserver op Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="8918f-106">This Quickstart steps through creating a virtual machine and installing a webserver on hello VM.</span></span>

<span data-ttu-id="8918f-107">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) aan voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="8918f-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

## <a name="create-ssh-key-pair"></a><span data-ttu-id="8918f-108">Een SSH-sleutelpaar maken</span><span class="sxs-lookup"><span data-stu-id="8918f-108">Create SSH key pair</span></span>

<span data-ttu-id="8918f-109">U moet een SSH-sleutelpaar toocomplete deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="8918f-109">You need an SSH key pair toocomplete this quick start.</span></span> <span data-ttu-id="8918f-110">Als u een bestaand SSH-sleutelpaar hebt, kunt u deze stap overslaan.</span><span class="sxs-lookup"><span data-stu-id="8918f-110">If you have an existing SSH key pair, this step can be skipped.</span></span>

<span data-ttu-id="8918f-111">Deze opdracht uitvoert vanaf een Bash-shell en volg Hallo op het scherm aanwijzingen.</span><span class="sxs-lookup"><span data-stu-id="8918f-111">From a Bash shell, run this command and follow hello on-screen directions.</span></span> <span data-ttu-id="8918f-112">opdrachtuitvoer Hallo bevat Hallo-bestandsnaam van het openbare sleutelbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="8918f-112">hello command output includes hello file name of hello public key file.</span></span> <span data-ttu-id="8918f-113">Hallo-inhoud van Hallo openbaar-sleutelbestand toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="8918f-113">Copy hello contents of hello public key file toohello clipboard.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a><span data-ttu-id="8918f-114">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="8918f-114">Log in tooAzure</span></span> 

<span data-ttu-id="8918f-115">Toohello aanmelden met Azure-portal op http://portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="8918f-115">Log in toohello Azure portal at http://portal.azure.com.</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="8918f-116">Virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="8918f-116">Create virtual machine</span></span>

1. <span data-ttu-id="8918f-117">Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8918f-117">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="8918f-118">Selecteer **Compute** en selecteer vervolgens **Ubuntu Server 16.04 LTS**.</span><span class="sxs-lookup"><span data-stu-id="8918f-118">Select **Compute**, and then select **Ubuntu Server 16.04 LTS**.</span></span> 

3. <span data-ttu-id="8918f-119">Geef informatie op Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8918f-119">Enter hello virtual machine information.</span></span> <span data-ttu-id="8918f-120">Bij **Verificatietype** selecteert u **Openbare SSH-sleutel**.</span><span class="sxs-lookup"><span data-stu-id="8918f-120">For **Authentication type**, select **SSH public key**.</span></span> <span data-ttu-id="8918f-121">Bij het plakken in uw openbare SSH-sleutel, behandelen tooremove witruimte voorloop- of volgspaties.</span><span class="sxs-lookup"><span data-stu-id="8918f-121">When pasting in your SSH public key, take care tooremove any leading or trailing white space.</span></span> <span data-ttu-id="8918f-122">Na het voltooien klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8918f-122">When complete, click **OK**.</span></span>

    ![Voer algemene informatie over uw virtuele machine Hallo-portalblade](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. <span data-ttu-id="8918f-124">Selecteer een grootte voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="8918f-124">Select a size for hello VM.</span></span> <span data-ttu-id="8918f-125">toosee meer grootte en selecteer **weergeven van alle** of wijzig de Hallo **ondersteund schijftype** filter.</span><span class="sxs-lookup"><span data-stu-id="8918f-125">toosee more sizes, select **View all** or change hello **Supported disk type** filter.</span></span> 

    ![Schermopname van VM-grootten](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. <span data-ttu-id="8918f-127">Op de blade beleidinstellingen Hallo Hallo standaardinstellingen behouden en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8918f-127">On hello settings blade, keep hello defaults and click **OK**.</span></span>

6. <span data-ttu-id="8918f-128">Klik op de overzichtspagina Hallo **Ok** implementatie van de virtuele machine toostart Hallo.</span><span class="sxs-lookup"><span data-stu-id="8918f-128">On hello summary page, click **Ok** toostart hello virtual machine deployment.</span></span>

7. <span data-ttu-id="8918f-129">Hallo VM is vastgemaakt toohello Azure-portaldashboard.</span><span class="sxs-lookup"><span data-stu-id="8918f-129">hello VM will be pinned toohello Azure portal dashboard.</span></span> <span data-ttu-id="8918f-130">Zodra het Hallo-implementatie is voltooid, wordt automatisch Hallo VM samenvatting blade geopend.</span><span class="sxs-lookup"><span data-stu-id="8918f-130">Once hello deployment has completed, hello VM summary blade automatically opens.</span></span>


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="8918f-131">Verbinding maken met toovirtual machine</span><span class="sxs-lookup"><span data-stu-id="8918f-131">Connect toovirtual machine</span></span>

<span data-ttu-id="8918f-132">Een SSH-verbinding maken met Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8918f-132">Create an SSH connection with hello virtual machine.</span></span>

1. <span data-ttu-id="8918f-133">Klik op Hallo **Connect** knop op Hallo virtuele machineblade.</span><span class="sxs-lookup"><span data-stu-id="8918f-133">Click hello **Connect** button on hello virtual machine blade.</span></span> <span data-ttu-id="8918f-134">Hallo verbinding knop geeft een SSH-verbindingsreeks die kan worden gebruikt tooconnect toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="8918f-134">hello connect button displays an SSH connection string that can be used tooconnect toohello virtual machine.</span></span>

    ![Portal 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. <span data-ttu-id="8918f-136">Voer Hallo volgende opdracht toocreate een SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="8918f-136">Run hello following command toocreate an SSH session.</span></span> <span data-ttu-id="8918f-137">Hallo-verbindingsreeks vervangen door Hallo die één u hebt gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8918f-137">Replace hello connection string with hello one you copied from hello Azure portal.</span></span>

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a><span data-ttu-id="8918f-138">NGINX installeren</span><span class="sxs-lookup"><span data-stu-id="8918f-138">Install NGINX</span></span>

<span data-ttu-id="8918f-139">Gebruik Hallo volgende scriptbronnen tooupdate pakket bash en installeer de meest recente NGINX-pakket Hallo.</span><span class="sxs-lookup"><span data-stu-id="8918f-139">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="8918f-140">Wanneer u klaar bent, sluit u Hallo SSH-sessie en retourneert Hallo VM-eigenschappen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8918f-140">When done, exit hello SSH session and return hello VM properties in hello Azure portal.</span></span>


## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="8918f-141">Poort 80 openen voor webverkeer</span><span class="sxs-lookup"><span data-stu-id="8918f-141">Open port 80 for web traffic</span></span> 

<span data-ttu-id="8918f-142">Een netwerkbeveiligingsgroep (NSG) beveiligt binnenkomend en uitgaand verkeer.</span><span class="sxs-lookup"><span data-stu-id="8918f-142">A Network security group (NSG) secures inbound and outbound traffic.</span></span> <span data-ttu-id="8918f-143">Wanneer een virtuele machine vanuit hello Azure-portal wordt gemaakt, wordt een inkomende regel gemaakt op poort 22 voor SSH-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="8918f-143">When a VM is created from hello Azure portal, an inbound rule is created on port 22 for SSH connections.</span></span> <span data-ttu-id="8918f-144">Omdat deze virtuele machine fungeert als host voor een webserver, moet een regel voor het NSG toobe gemaakt voor poort 80.</span><span class="sxs-lookup"><span data-stu-id="8918f-144">Because this VM hosts a webserver, an NSG rule needs toobe created for port 80.</span></span>

1. <span data-ttu-id="8918f-145">Klik op de naam van de Hallo HALLO hallo voor virtuele machines **resourcegroep**.</span><span class="sxs-lookup"><span data-stu-id="8918f-145">On hello virtual machine, click hello name of hello **Resource group**.</span></span>
2. <span data-ttu-id="8918f-146">Selecteer Hallo **netwerkbeveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="8918f-146">Select hello **network security group**.</span></span> <span data-ttu-id="8918f-147">Hallo NSG kan worden geïdentificeerd met Hallo **Type** kolom.</span><span class="sxs-lookup"><span data-stu-id="8918f-147">hello NSG can be identified using hello **Type** column.</span></span> 
3. <span data-ttu-id="8918f-148">Klik op het Hallo links menu onder instellingen **inkomende beveiligingsregels**.</span><span class="sxs-lookup"><span data-stu-id="8918f-148">On hello left-hand menu, under settings, click **Inbound security rules**.</span></span>
4. <span data-ttu-id="8918f-149">Klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="8918f-149">Click on **Add**.</span></span>
5. <span data-ttu-id="8918f-150">Typ bij **Naam** **http**.</span><span class="sxs-lookup"><span data-stu-id="8918f-150">In **Name**, type **http**.</span></span> <span data-ttu-id="8918f-151">Zorg ervoor dat **poortbereik** too80 is ingesteld en **actie** te is ingesteld,**toestaan**.</span><span class="sxs-lookup"><span data-stu-id="8918f-151">Make sure **Port range** is set too80 and **Action** is set too**Allow**.</span></span> 
6. <span data-ttu-id="8918f-152">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="8918f-152">Click **OK**.</span></span>


## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="8918f-153">Hallo-NGINX welkomstpagina weergeven</span><span class="sxs-lookup"><span data-stu-id="8918f-153">View hello NGINX welcome page</span></span>

<span data-ttu-id="8918f-154">Met NGINX geïnstalleerd en poort 80 tooyour VM open, Hallo webserver nu toegankelijk zijn vanuit Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="8918f-154">With NGINX installed, and port 80 open tooyour VM, hello webserver can now be accessed from hello internet.</span></span> <span data-ttu-id="8918f-155">Open een webbrowser en voer het openbare IP-adres Hallo Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="8918f-155">Open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="8918f-156">Hallo openbaar IP-adres, kunt u vinden op Hallo VM blade in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="8918f-156">hello public IP address can be found on hello VM blade in hello Azure portal.</span></span>

![Standaardsite van NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="8918f-158">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="8918f-158">Clean up resources</span></span>

<span data-ttu-id="8918f-159">Wanneer deze niet langer nodig is, resourcegroep hello, virtuele machine en alle gerelateerde resources verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8918f-159">When no longer needed, delete hello resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="8918f-160">toodo dus resourcegroep Hallo Hallo virtuele machine blade selecteren en op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="8918f-160">toodo so, select hello resource group from hello virtual machine blade and click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8918f-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8918f-161">Next steps</span></span>

<span data-ttu-id="8918f-162">In deze Snel starten hebt u een eenvoudige virtuele machine geïmplementeerd, een netwerkbeveiligingsgroepregel gemaakt en een webserver geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8918f-162">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="8918f-163">toolearn meer informatie over virtuele machines in Azure, blijven toohello zelfstudie voor virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="8918f-163">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8918f-164">Zelfstudies over virtuele Linux-machines</span><span class="sxs-lookup"><span data-stu-id="8918f-164">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)

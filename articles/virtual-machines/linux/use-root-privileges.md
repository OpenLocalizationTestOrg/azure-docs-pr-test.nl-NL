---
title: Hoofdmap bevoegdheden gebruiken op virtuele Linux-machines | Microsoft Docs
description: Informatie over het gebruik van root-bevoegdheden op een virtuele Linux-machine in Azure.
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: dc39db1f5fecffb60499a5420bfe72850e2fffd9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="a4014-103">Bevoegdheden op hoofdniveau gebruiken op virtuele Linux-machines in Azure</span><span class="sxs-lookup"><span data-stu-id="a4014-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a4014-104">Standaard de `root` gebruiker is uitgeschakeld op Linux virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a4014-104">By default, the `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="a4014-105">Gebruikers kunnen opdrachten uitvoeren met verhoogde bevoegdheden met behulp van de `sudo` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a4014-105">Users can run commands with elevated privileges by using the `sudo` command.</span></span> <span data-ttu-id="a4014-106">De ervaring kan echter variëren afhankelijk van hoe het systeem is ingericht.</span><span class="sxs-lookup"><span data-stu-id="a4014-106">However, the experience may vary depending on how the system was provisioned.</span></span>

1. <span data-ttu-id="a4014-107">**SSH-sleutel en het wachtwoord of wachtwoord alleen** -de virtuele machine is ingericht met ofwel een certificaat (`.CER` bestand) of SSH-sleutel, evenals een wachtwoord, of alleen een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a4014-107">**SSH key and password OR password only** - the virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="a4014-108">In dit geval `sudo` voor het wachtwoord van de gebruiker wordt gevraagd voordat de opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4014-108">In this case `sudo` will prompt for the user's password before executing the command.</span></span>
2. <span data-ttu-id="a4014-109">**SSH-sleutel** -de virtuele machine is ingericht met een certificaat (`.cer`, `.pem`, of `.pub` bestand) of SSH-sleutel, maar er is geen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a4014-109">**SSH key only** - the virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="a4014-110">In dit geval `sudo` **niet** vragen om het wachtwoord van de gebruiker voordat de opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4014-110">In this case `sudo` **will not** prompt for the user's password before executing the command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="a4014-111">SSH-sleutel en wachtwoord of alleen wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a4014-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="a4014-112">Meld u aan bij de virtuele Linux-machine met behulp van SSH-sleutel of het wachtwoord verificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a4014-112">Log into the Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="a4014-113">In dit geval wordt de gebruiker wordt gevraagd om een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a4014-113">In this case the user will be prompted for a password.</span></span> <span data-ttu-id="a4014-114">Na het invoeren van het wachtwoord `sudo` wordt uitgevoerd de opdracht met `root` bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="a4014-114">After entering the password `sudo` will run the command with `root` privileges.</span></span>

<span data-ttu-id="a4014-115">U kunt ook passwordless sudo inschakelen door het bewerken van de `/etc/sudoers.d/waagent` bestand, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a4014-115">You can also enable passwordless sudo by editing the `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="a4014-116">Deze wijziging kunt voor passwordless sudo door de gebruiker 'azureuser'.</span><span class="sxs-lookup"><span data-stu-id="a4014-116">This change will allow for passwordless sudo by the user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="a4014-117">SSH alleen sleutel</span><span class="sxs-lookup"><span data-stu-id="a4014-117">SSH Key Only</span></span>
<span data-ttu-id="a4014-118">Meld u aan bij de virtuele Linux-machine met behulp van SSH-sleutelverificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a4014-118">Log into the Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="a4014-119">In dit geval de gebruiker wordt **niet** worden gevraagd om een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a4014-119">In this case the user will **not** be prompted for a password.</span></span> <span data-ttu-id="a4014-120">Na zwaarwegende `<enter>`, `sudo` wordt uitgevoerd de opdracht met `root` bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="a4014-120">After pressing `<enter>`, `sudo` will run the command with `root` privileges.</span></span>


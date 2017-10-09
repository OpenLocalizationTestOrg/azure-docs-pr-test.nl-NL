---
title: aaaUse hoofdmap bevoegdheden op de virtuele Linux-machines | Microsoft Docs
description: Meer informatie over hoe toouse hoofdmap bevoegdheden hebben op een virtuele Linux-machine in Azure.
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
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a><span data-ttu-id="01181-103">Bevoegdheden op hoofdniveau gebruiken op virtuele Linux-machines in Azure</span><span class="sxs-lookup"><span data-stu-id="01181-103">Using root privileges on Linux virtual machines in Azure</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="01181-104">Standaard Hallo `root` gebruiker is uitgeschakeld op Linux virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="01181-104">By default, hello `root` user is disabled on Linux virtual machines in Azure.</span></span> <span data-ttu-id="01181-105">Gebruikers kunnen opdrachten uitvoeren met verhoogde bevoegdheden via Hallo `sudo` opdracht.</span><span class="sxs-lookup"><span data-stu-id="01181-105">Users can run commands with elevated privileges by using hello `sudo` command.</span></span> <span data-ttu-id="01181-106">Hallo-ervaring kan echter variëren afhankelijk van hoe Hallo system is ingericht.</span><span class="sxs-lookup"><span data-stu-id="01181-106">However, hello experience may vary depending on how hello system was provisioned.</span></span>

1. <span data-ttu-id="01181-107">**SSH-sleutel en het wachtwoord of wachtwoord alleen** -Hallo virtuele machine is ingericht met ofwel een certificaat (`.CER` bestand) of SSH-sleutel, evenals een wachtwoord, of alleen een gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="01181-107">**SSH key and password OR password only** - hello virtual machine was provisioned with either a certificate (`.CER` file) or SSH key as well as a password, or just a user name and password.</span></span> <span data-ttu-id="01181-108">In dit geval `sudo` voor Hallo gebruikerswachtwoord wordt gevraagd voordat het Hallo-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01181-108">In this case `sudo` will prompt for hello user's password before executing hello command.</span></span>
2. <span data-ttu-id="01181-109">**SSH-sleutel** -Hallo virtuele machine is ingericht met een certificaat (`.cer`, `.pem`, of `.pub` bestand) of SSH-sleutel, maar er is geen wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="01181-109">**SSH key only** - hello virtual machine was provisioned with a certificate (`.cer`, `.pem`, or `.pub` file) or SSH key, but no password.</span></span>  <span data-ttu-id="01181-110">In dit geval `sudo` **niet** vragen om het wachtwoord van de gebruiker van de Hallo voordat Hallo-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01181-110">In this case `sudo` **will not** prompt for hello user's password before executing hello command.</span></span>

## <a name="ssh-key-and-password-or-password-only"></a><span data-ttu-id="01181-111">SSH-sleutel en wachtwoord of alleen wachtwoord</span><span class="sxs-lookup"><span data-stu-id="01181-111">SSH Key and Password, or Password Only</span></span>
<span data-ttu-id="01181-112">Meld u aan bij Hallo Linux virtuele machine met behulp van SSH-sleutel of het wachtwoord verificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="01181-112">Log into hello Linux virtual machine using SSH key or password authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>
    [sudo] password for azureuser:

<span data-ttu-id="01181-113">In dit geval wordt Hallo gebruiker gevraagd om een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="01181-113">In this case hello user will be prompted for a password.</span></span> <span data-ttu-id="01181-114">Na het invoeren van Hallo wachtwoord `sudo` wordt uitgevoerd Hallo-opdracht met `root` bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="01181-114">After entering hello password `sudo` will run hello command with `root` privileges.</span></span>

<span data-ttu-id="01181-115">U kunt ook passwordless sudo inschakelen door het bewerken van Hallo `/etc/sudoers.d/waagent` bestand, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="01181-115">You can also enable passwordless sudo by editing hello `/etc/sudoers.d/waagent` file, for example:</span></span>

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

<span data-ttu-id="01181-116">Deze wijziging kunt voor passwordless sudo door gebruiker Hallo 'azureuser'.</span><span class="sxs-lookup"><span data-stu-id="01181-116">This change will allow for passwordless sudo by hello user "azureuser".</span></span>

## <a name="ssh-key-only"></a><span data-ttu-id="01181-117">SSH alleen sleutel</span><span class="sxs-lookup"><span data-stu-id="01181-117">SSH Key Only</span></span>
<span data-ttu-id="01181-118">Meld u aan bij Hallo Linux virtuele machine met behulp van SSH-sleutelverificatie en voer vervolgens met behulp van opdrachten `sudo`, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="01181-118">Log into hello Linux virtual machine using SSH key authentication, then run commands using `sudo`, for example:</span></span>

    # sudo <command>

<span data-ttu-id="01181-119">In dit geval Hallo gebruiker wordt **niet** worden gevraagd om een wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="01181-119">In this case hello user will **not** be prompted for a password.</span></span> <span data-ttu-id="01181-120">Na zwaarwegende `<enter>`, `sudo` wordt uitgevoerd Hallo-opdracht met `root` bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="01181-120">After pressing `<enter>`, `sudo` will run hello command with `root` privileges.</span></span>


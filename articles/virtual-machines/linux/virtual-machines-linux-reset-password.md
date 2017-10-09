---
title: aaaHow tooreset lokale Linux-wachtwoord op Azure Virtual machines | Microsoft Docs
description: Introduceren Hallo stappen tooreset Hallo lokale Linux-wachtwoord op Azure VM
services: virtual-machines-linux
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 7/3/2017
ms.author: delhan
ms.openlocfilehash: 3827e32186c5f034d9bb6fc502dc26708b52a00a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-linux-password-on-azure-vms"></a><span data-ttu-id="6e001-103">Hoe tooreset lokale Linux-wachtwoord op Azure Virtual machines</span><span class="sxs-lookup"><span data-stu-id="6e001-103">How tooreset local Linux password on Azure VMs</span></span>

<span data-ttu-id="6e001-104">Dit artikel bevat verschillende methoden tooreset lokale Linux-virtuele Machine (VM) wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="6e001-104">This article introduces several methods tooreset local Linux Virtual Machine (VM) passwords.</span></span> <span data-ttu-id="6e001-105">Als Hallo-gebruikersaccount is verlopen of als u alleen toocreate een nieuw account wilt, kunt u deze kunt gebruiken Hallo na methoden toocreate een nieuwe lokale beheerdersaccount en opnieuw krijgen toegang toohello VM.</span><span class="sxs-lookup"><span data-stu-id="6e001-105">If hello user account is expired or you just want toocreate a new account, you can use hello following methods toocreate a new local admin account and re-gain access toohello VM.</span></span>

## <a name="symptoms"></a><span data-ttu-id="6e001-106">Symptomen</span><span class="sxs-lookup"><span data-stu-id="6e001-106">Symptoms</span></span>

<span data-ttu-id="6e001-107">U kunt zich niet aanmelden toohello VM en u ontvangt een bericht weergegeven dat aangeeft dat Hallo wachtwoord die u hebt gebruikt, is onjuist.</span><span class="sxs-lookup"><span data-stu-id="6e001-107">You can't log in toohello VM, and you receive a message that indicates that hello password that you used is incorrect.</span></span> <span data-ttu-id="6e001-108">Bovendien u niet gebruiken VMAgent tooreset uw wachtwoord op Hallo Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="6e001-108">Additionally, you can't use VMAgent tooreset your password on hello Azure Portal.</span></span> 

## <a name="manual-password-reset-procedure"></a><span data-ttu-id="6e001-109">Handmatige procedure voor wachtwoord opnieuw instellen</span><span class="sxs-lookup"><span data-stu-id="6e001-109">Manual Password Reset procedure</span></span>

1.  <span data-ttu-id="6e001-110">Hallo VM verwijderen en schijven Hallo gekoppeld houden.</span><span class="sxs-lookup"><span data-stu-id="6e001-110">Delete hello VM and keep hello attached disks.</span></span>

2.  <span data-ttu-id="6e001-111">Hallo OS station als een schijf gegevens tooanother koppelen tijdelijke virtuele machine in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="6e001-111">Attach hello OS Drive as a data disk tooanother temporal VM in hello same location.</span></span>

3.  <span data-ttu-id="6e001-112">Hallo SSH-opdracht op Hallo tijdelijke VM toobecome volgen supergebruiker uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6e001-112">Run hello following SSH command on hello temporal VM toobecome a super-user.</span></span>


    ~~~~
    sudo su
    ~~~~

4.  <span data-ttu-id="6e001-113">Voer **fdisk -l** of kijken system logboeken toofind Hallo nieuwe schijf is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="6e001-113">Run **fdisk -l** or look at system logs toofind hello newly attached disk.</span></span> <span data-ttu-id="6e001-114">Hallo station naam toomount vinden.</span><span class="sxs-lookup"><span data-stu-id="6e001-114">Locate hello drive name toomount.</span></span> <span data-ttu-id="6e001-115">Klik op Hallo tijdelijke virtuele machine, zoeken in de relevante Hallo logbestand.</span><span class="sxs-lookup"><span data-stu-id="6e001-115">Then on hello temporal VM, look in hello relevant log file.</span></span>

    ~~~~
    grep SCSI /var/log/kern.log (ubuntu)
    grep SCSI /var/log/messages (centos, suse, oracle)
    ~~~~

    <span data-ttu-id="6e001-116">Hallo volgt voorbeelduitvoer van Hallo grep-opdracht:</span><span class="sxs-lookup"><span data-stu-id="6e001-116">hello following is example output of hello grep command:</span></span>

    ~~~~
    kernel: [ 9707.100572] sd 3:0:0:0: [sdc] Attached SCSI disk
    ~~~~

5.  <span data-ttu-id="6e001-117">Maken van een koppelpunt aangeroepen **tempmount**.</span><span class="sxs-lookup"><span data-stu-id="6e001-117">Create a mount point called **tempmount**.</span></span>

    ~~~~
    mkdir /tempmount
    ~~~~

6.  <span data-ttu-id="6e001-118">Hallo OS-schijf koppelen op Hallo-koppelpunt.</span><span class="sxs-lookup"><span data-stu-id="6e001-118">Mount hello OS disk on hello mount point.</span></span> <span data-ttu-id="6e001-119">U hoeft meestal toomount sdc1 of sdc2.</span><span class="sxs-lookup"><span data-stu-id="6e001-119">You usually need toomount sdc1 or sdc2.</span></span> <span data-ttu-id="6e001-120">Dit hangt af van Hallo partitie in de map/etc van Hallo verbroken machineschijf die als host fungeert.</span><span class="sxs-lookup"><span data-stu-id="6e001-120">This will depend on hello hosting partition in /etc directory from hello broken machine disk.</span></span>

    ~~~~
    mount /dev/sdc1 /tempmount
    ~~~~

7.  <span data-ttu-id="6e001-121">Een back-up uitvoeren voordat u wijzigingen aanbrengt:</span><span class="sxs-lookup"><span data-stu-id="6e001-121">Perform a backup before making any changes:</span></span>

    ~~~~
    cp /etc/passwd /etc/passwd_orig    
    cp /etc/shadow /etc/shadow_orig    
    cp /tempmount/etc/passwd /etc/passwd
    cp /tempmount/etc/shadow /etc/shadow 
    cp /tempmount/etc/passwd /tempmount/etc/passwd_orig
    cp /tempmount/etc/shadow /tempmount/etc/shadow_orig
    ~~~~

8.  <span data-ttu-id="6e001-122">Het wachtwoord opnieuw instellen van Hallo gebruiker die u nodig hebt:</span><span class="sxs-lookup"><span data-stu-id="6e001-122">Reset hello user’s password that you need:</span></span>

    ~~~~
    passwd <<USER>> 
    ~~~~

9.  <span data-ttu-id="6e001-123">Verplaatsing Hallo gewijzigd bestanden toohello juiste locatie op Hallo van machine schijf verbroken.</span><span class="sxs-lookup"><span data-stu-id="6e001-123">Move hello modified files toohello correct location on hello broken machine's disk.</span></span>

    ~~~~
    cp /etc/passwd /tempmount/etc/passwd
    cp /etc/shadow /tempmount/etc/shadow
    cp /etc/passwd_orig /etc/passwd
    cp /etc/shadow_orig /etc/shadow
    
10. Go back toohello root and unmount hello disk.

    ~~~~
    <span data-ttu-id="6e001-124">cd / umount /tempmount</span><span class="sxs-lookup"><span data-stu-id="6e001-124">cd / umount /tempmount</span></span>
    ~~~~

11. Detach hello disk from hello management portal.

12. Recreate hello VM.

## Next steps

* [Troubleshoot Azure VM by attaching OS disk tooanother Azure VM](http://social.technet.microsoft.com/wiki/contents/articles/18710.troubleshoot-azure-vm-by-attaching-os-disk-to-another-azure-vm.aspx)

* [Azure CLI: How toodelete and re-deploy a VM from VHD](https://blogs.msdn.microsoft.com/linuxonazure/2016/07/21/azure-cli-how-to-delete-and-re-deploy-a-vm-from-vhd/)

---
title: Veelgestelde vragen voor virtuele Linux-machines in Azure aaaFrequently | Microsoft Docs
description: Biedt antwoorden toosome van Hallo Veelgestelde vragen over gemaakt met Resource Manager-model Hallo virtuele Linux-machines.
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-management
ms.assetid: 3648e09c-1115-4818-93c6-688d7a54a353
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: cynthn
ms.openlocfilehash: 0afd08123dddc408851065c46deedc3146dbec20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-question-about-linux-virtual-machines"></a><span data-ttu-id="0c10d-103">Veelgestelde vragen over virtuele Linux-Machines</span><span class="sxs-lookup"><span data-stu-id="0c10d-103">Frequently asked question about Linux Virtual Machines</span></span>
<span data-ttu-id="0c10d-104">In dit artikel komen enkele veelgestelde vragen over virtuele Linux-machines in Azure met Resource Manager-implementatiemodel Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c10d-104">This article addresses some common questions about Linux virtual machines created in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="0c10d-105">Zie voor Hallo Windows-versie van dit onderwerp [Veelgestelde vragen over Windows virtuele Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0c10d-105">For hello Windows version of this topic, see [Frequently asked question about Windows Virtual Machines](../windows/faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

## <a name="what-can-i-run-on-an-azure-vm"></a><span data-ttu-id="0c10d-106">Wat kan ik uitvoeren op een VM van Azure?</span><span class="sxs-lookup"><span data-stu-id="0c10d-106">What can I run on an Azure VM?</span></span>
<span data-ttu-id="0c10d-107">Alle abonnees kunnen serversoftware uitvoeren op een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="0c10d-107">All subscribers can run server software on an Azure virtual machine.</span></span> <span data-ttu-id="0c10d-108">Zie voor meer informatie [Linux op Azure-Endorsed distributies](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0c10d-108">For more information, see [Linux on Azure-Endorsed Distributions](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="how-much-storage-can-i-use-with-a-virtual-machine"></a><span data-ttu-id="0c10d-109">Hoeveel opslagruimte kan ik gebruiken met een virtuele machine?</span><span class="sxs-lookup"><span data-stu-id="0c10d-109">How much storage can I use with a virtual machine?</span></span>
<span data-ttu-id="0c10d-110">Elke gegevensschijf kan zijn van too1 TB.</span><span class="sxs-lookup"><span data-stu-id="0c10d-110">Each data disk can be up too1 TB.</span></span> <span data-ttu-id="0c10d-111">Hallo aantal gegevensschijven die u kunt gebruiken, is afhankelijk van Hallo grootte van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0c10d-111">hello number of data disks you can use depends on hello size of hello virtual machine.</span></span> <span data-ttu-id="0c10d-112">Zie [Grootten voor virtuele machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0c10d-112">For details, see [Sizes for Virtual Machines](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="0c10d-113">Een Azure storage-account biedt opslag voor de besturingssysteemschijf hello en eventuele gegevensschijven.</span><span class="sxs-lookup"><span data-stu-id="0c10d-113">An Azure storage account provides storage for hello operating system disk and any data disks.</span></span> <span data-ttu-id="0c10d-114">Elke schijf is een VHD-bestand dat wordt opgeslagen als een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="0c10d-114">Each disk is a .vhd file stored as a page blob.</span></span> <span data-ttu-id="0c10d-115">Zie [deze pagina](https://azure.microsoft.com/pricing/details/storage/) voor prijsinformatie.</span><span class="sxs-lookup"><span data-stu-id="0c10d-115">For pricing details, see [Storage Pricing Details](https://azure.microsoft.com/pricing/details/storage/).</span></span>

## <a name="how-can-i-access-my-virtual-machine"></a><span data-ttu-id="0c10d-116">Hoe kan ik toegang tot mijn virtuele machine?</span><span class="sxs-lookup"><span data-stu-id="0c10d-116">How can I access my virtual machine?</span></span>
<span data-ttu-id="0c10d-117">Stel een verbinding met extern toolog toohello voor virtuele machines met behulp van Secure Shell (SSH).</span><span class="sxs-lookup"><span data-stu-id="0c10d-117">Establish a remote connection toolog on toohello virtual machine, using Secure Shell (SSH).</span></span> <span data-ttu-id="0c10d-118">Zie Hallo instructies over het tooconnect [vanuit Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) of [van Linux- en Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c10d-118">See hello instructions on how tooconnect [from Windows](ssh-from-windows.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [from Linux and Mac](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0c10d-119">SSH biedt standaard ondersteuning voor maximaal tien gelijktijdige verbindingen.</span><span class="sxs-lookup"><span data-stu-id="0c10d-119">By default, SSH allows a maximum of 10 concurrent connections.</span></span> <span data-ttu-id="0c10d-120">U kunt dit getal verhogen door Hallo-configuratiebestand bewerken.</span><span class="sxs-lookup"><span data-stu-id="0c10d-120">You can increase this number by editing hello configuration file.</span></span>

<span data-ttu-id="0c10d-121">Als u problemen ondervindt, uitchecken [oplossen Secure Shell (SSH) verbindingen](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c10d-121">If you’re having problems, check out [Troubleshoot Secure Shell (SSH) connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="can-i-use-hello-temporary-disk-devsdb1-toostore-data"></a><span data-ttu-id="0c10d-122">Kan ik Hallo tijdelijke schijf (/ dev/sdb1) toostore gegevens gebruiken?</span><span class="sxs-lookup"><span data-stu-id="0c10d-122">Can I use hello temporary disk (/dev/sdb1) toostore data?</span></span>
<span data-ttu-id="0c10d-123">Gebruik geen Hallo tijdelijke schijf (/ dev/sdb1) toostore gegevens.</span><span class="sxs-lookup"><span data-stu-id="0c10d-123">Don't use hello temporary disk (/dev/sdb1) toostore data.</span></span> <span data-ttu-id="0c10d-124">Het is alleen er voor de tijdelijke opslag.</span><span class="sxs-lookup"><span data-stu-id="0c10d-124">It is only there for temporary storage.</span></span> <span data-ttu-id="0c10d-125">U risico verlies van gegevens die kunnen niet worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="0c10d-125">You risk losing data that can’t be recovered.</span></span>

## <a name="can-i-copy-or-clone-an-existing-azure-vm"></a><span data-ttu-id="0c10d-126">Kan ik kopiëren of kloon van een bestaande virtuele machine in Azure?</span><span class="sxs-lookup"><span data-stu-id="0c10d-126">Can I copy or clone an existing Azure VM?</span></span>
<span data-ttu-id="0c10d-127">Ja.</span><span class="sxs-lookup"><span data-stu-id="0c10d-127">Yes.</span></span> <span data-ttu-id="0c10d-128">Zie voor instructies [hoe toocreate kopie maken van een virtuele Linux-machine in de resourcemanager-implementatiemodel Hallo](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0c10d-128">For instructions, see [How toocreate a copy of a Linux virtual machine in hello Resource Manager deployment model](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="why-am-i-not-seeing-canada-central-and-canada-east-regions-through-azure-resource-manager"></a><span data-ttu-id="0c10d-129">Waarom krijg ik niet zien Canada centraal en Canada Oost regio's via Azure Resource Manager?</span><span class="sxs-lookup"><span data-stu-id="0c10d-129">Why am I not seeing Canada Central and Canada East regions through Azure Resource Manager?</span></span>
<span data-ttu-id="0c10d-130">Hallo twee nieuwe gebieden van Canada Central en Canada Oost worden niet automatisch geregistreerd voor het maken van de virtuele machine voor bestaande Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="0c10d-130">hello two new regions of Canada Central and Canada East are not automatically registered for virtual machine creation for existing Azure subscriptions.</span></span> <span data-ttu-id="0c10d-131">Deze registratie automatisch uitgevoerd wanneer een virtuele machine wordt geïmplementeerd via Azure portal tooany Hallo andere regio's met Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0c10d-131">This registration is done automatically when a virtual machine is deployed through hello Azure portal tooany other region using Azure Resource Manager.</span></span> <span data-ttu-id="0c10d-132">Nadat een virtuele machine is geïmplementeerd tooany andere Azure-regio Hallo nieuwe gebieden moet beschikbaar zijn voor latere virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="0c10d-132">After a virtual machine is deployed tooany other Azure region, hello new regions should be available for subsequent virtual machines.</span></span>

## <a name="can-i-add-a-nic-toomy-vm-after-its-created"></a><span data-ttu-id="0c10d-133">Kan ik een NIC toomy VM toevoegen nadat deze gemaakt?</span><span class="sxs-lookup"><span data-stu-id="0c10d-133">Can I add a NIC toomy VM after it's created?</span></span>
<span data-ttu-id="0c10d-134">Ja, dit is nu mogelijk.</span><span class="sxs-lookup"><span data-stu-id="0c10d-134">Yes, this is now possible.</span></span> <span data-ttu-id="0c10d-135">Hallo VM eerste behoeften toobe gestopt toewijzing ongedaan is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0c10d-135">hello VM first needs toobe stopped deallocated.</span></span> <span data-ttu-id="0c10d-136">U kunt toevoegen of verwijderen van een NIC (tenzij het Hallo laatste NIC op Hallo VM).</span><span class="sxs-lookup"><span data-stu-id="0c10d-136">Then you can add or remove a NIC (unless it's hello last NIC on hello VM).</span></span> 

## <a name="are-there-any-computer-name-requirements"></a><span data-ttu-id="0c10d-137">Zijn er naam computervereisten?</span><span class="sxs-lookup"><span data-stu-id="0c10d-137">Are there any computer name requirements?</span></span>
<span data-ttu-id="0c10d-138">Ja.</span><span class="sxs-lookup"><span data-stu-id="0c10d-138">Yes.</span></span> <span data-ttu-id="0c10d-139">Hallo-computernaam mag maximaal 64 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="0c10d-139">hello computer name can be a maximum of 64 characters in length.</span></span> <span data-ttu-id="0c10d-140">Zie [Naming conventions regels en beperkingen](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over de naamgeving van uw resources.</span><span class="sxs-lookup"><span data-stu-id="0c10d-140">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information around naming your resources.</span></span>

## <a name="are-there-any-resource-group-name-requirements"></a><span data-ttu-id="0c10d-141">Zijn er een resource vereisten voor de naam groep?</span><span class="sxs-lookup"><span data-stu-id="0c10d-141">Are there any resource group name requirements?</span></span>
<span data-ttu-id="0c10d-142">Ja.</span><span class="sxs-lookup"><span data-stu-id="0c10d-142">Yes.</span></span> <span data-ttu-id="0c10d-143">Hallo Resourcegroepnaam mag maximaal 90 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="0c10d-143">hello resource group name can be a maximum of 90 characters in length.</span></span> <span data-ttu-id="0c10d-144">Zie [Naming conventions regels en beperkingen](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie over resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="0c10d-144">See [Naming conventions rules and restrictions](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information about resource groups.</span></span>

## <a name="what-are-hello-username-requirements-when-creating-a-vm"></a><span data-ttu-id="0c10d-145">Wat zijn Hallo gebruikersnaam vereisten bij het maken van een virtuele machine?</span><span class="sxs-lookup"><span data-stu-id="0c10d-145">What are hello username requirements when creating a VM?</span></span>
<span data-ttu-id="0c10d-146">Gebruikersnamen moet 1 tot 64 tekens lang zijn.</span><span class="sxs-lookup"><span data-stu-id="0c10d-146">Usernames must be 1 - 64 characters in length.</span></span>

<span data-ttu-id="0c10d-147">Hallo volgende gebruikersnamen zijn niet toegestaan:</span><span class="sxs-lookup"><span data-stu-id="0c10d-147">hello following usernames are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-148">Beheerder</span><span class="sxs-lookup"><span data-stu-id="0c10d-148">administrator</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-149">Beheerder</span><span class="sxs-lookup"><span data-stu-id="0c10d-149">admin</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-150">Gebruiker</span><span class="sxs-lookup"><span data-stu-id="0c10d-150">user</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-151">Gebruiker1</span><span class="sxs-lookup"><span data-stu-id="0c10d-151">user1</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-152">Test</span><span class="sxs-lookup"><span data-stu-id="0c10d-152">test</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-153">Gebruiker2</span><span class="sxs-lookup"><span data-stu-id="0c10d-153">user2</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-154">Test1</span><span class="sxs-lookup"><span data-stu-id="0c10d-154">test1</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-155">User3</span><span class="sxs-lookup"><span data-stu-id="0c10d-155">user3</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-156">admin1</span><span class="sxs-lookup"><span data-stu-id="0c10d-156">admin1</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-157">1</span><span class="sxs-lookup"><span data-stu-id="0c10d-157">1</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-158">123</span><span class="sxs-lookup"><span data-stu-id="0c10d-158">123</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-159">een</span><span class="sxs-lookup"><span data-stu-id="0c10d-159">a</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-160">actuser</span><span class="sxs-lookup"><span data-stu-id="0c10d-160">actuser</span></span>  </td><td style="text-align:center"> <span data-ttu-id="0c10d-161">adm</span><span class="sxs-lookup"><span data-stu-id="0c10d-161">adm</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-162">admin2</span><span class="sxs-lookup"><span data-stu-id="0c10d-162">admin2</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-163">ASPNET</span><span class="sxs-lookup"><span data-stu-id="0c10d-163">aspnet</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-164">Back-up</span><span class="sxs-lookup"><span data-stu-id="0c10d-164">backup</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-165">Console</span><span class="sxs-lookup"><span data-stu-id="0c10d-165">console</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-166">David</span><span class="sxs-lookup"><span data-stu-id="0c10d-166">david</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-167">Gast</span><span class="sxs-lookup"><span data-stu-id="0c10d-167">guest</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-168">John</span><span class="sxs-lookup"><span data-stu-id="0c10d-168">john</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-169">Eigenaar</span><span class="sxs-lookup"><span data-stu-id="0c10d-169">owner</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-170">hoofdmap</span><span class="sxs-lookup"><span data-stu-id="0c10d-170">root</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-171">server</span><span class="sxs-lookup"><span data-stu-id="0c10d-171">server</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-172">SQL</span><span class="sxs-lookup"><span data-stu-id="0c10d-172">sql</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-173">Ondersteuning</span><span class="sxs-lookup"><span data-stu-id="0c10d-173">support</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-174">support_388945a0</span><span class="sxs-lookup"><span data-stu-id="0c10d-174">support_388945a0</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-175">sys</span><span class="sxs-lookup"><span data-stu-id="0c10d-175">sys</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center"><span data-ttu-id="0c10d-176">Test2</span><span class="sxs-lookup"><span data-stu-id="0c10d-176">test2</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-177">Test3</span><span class="sxs-lookup"><span data-stu-id="0c10d-177">test3</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-178">User4</span><span class="sxs-lookup"><span data-stu-id="0c10d-178">user4</span></span> </td><td style="text-align:center"> <span data-ttu-id="0c10d-179">user5</span><span class="sxs-lookup"><span data-stu-id="0c10d-179">user5</span></span></td>
    </tr>
</table>


## <a name="what-are-hello-password-requirements-when-creating-a-vm"></a><span data-ttu-id="0c10d-180">Wat zijn de wachtwoordvereisten Hallo bij het maken van een virtuele machine?</span><span class="sxs-lookup"><span data-stu-id="0c10d-180">What are hello password requirements when creating a VM?</span></span>
<span data-ttu-id="0c10d-181">Wachtwoorden moeten 6-72 tekens lang zijn en voldoen aan 3 buiten Hallo 4 complexiteitsvereisten te volgen:</span><span class="sxs-lookup"><span data-stu-id="0c10d-181">Passwords must be 6 - 72 characters in length and meet 3 out of hello following 4 complexity requirements:</span></span>

* <span data-ttu-id="0c10d-182">Lagere tekens bevatten</span><span class="sxs-lookup"><span data-stu-id="0c10d-182">Have lower characters</span></span>
* <span data-ttu-id="0c10d-183">Bovenste tekens bevatten</span><span class="sxs-lookup"><span data-stu-id="0c10d-183">Have upper characters</span></span>
* <span data-ttu-id="0c10d-184">Een cijfer zijn</span><span class="sxs-lookup"><span data-stu-id="0c10d-184">Have a digit</span></span>
* <span data-ttu-id="0c10d-185">Hebt u een speciaal teken (Regex overeenkomen met [\W_])</span><span class="sxs-lookup"><span data-stu-id="0c10d-185">Have a special character (Regex match [\W_])</span></span>

<span data-ttu-id="0c10d-186">Hallo volgende wachtwoorden zijn niet toegestaan:</span><span class="sxs-lookup"><span data-stu-id="0c10d-186">hello following passwords are not allowed:</span></span>

<table>
    <tr>
        <td style="text-align:center">abc@123</td>
        <td style="text-align:center"><span data-ttu-id="0c10d-187">P@$$w0rd</span><span class="sxs-lookup"><span data-stu-id="0c10d-187">P@$$w0rd</span></span></td>
        <td style="text-align:center">P@ssw0rd</td>
        <td style="text-align:center">P@ssword123</td>
        <td style="text-align:center"><span data-ttu-id="0c10d-188">Pa$ $word</span><span class="sxs-lookup"><span data-stu-id="0c10d-188">Pa$$word</span></span></td>
    </tr>
    <tr>
        <td style="text-align:center">pass@word1</td>
        <td style="text-align:center"><span data-ttu-id="0c10d-189">Wachtwoord!</span><span class="sxs-lookup"><span data-stu-id="0c10d-189">Password!</span></span></td>
        <td style="text-align:center"><span data-ttu-id="0c10d-190">Wachtwoord1</span><span class="sxs-lookup"><span data-stu-id="0c10d-190">Password1</span></span></td>
        <td style="text-align:center"><span data-ttu-id="0c10d-191">Password22</span><span class="sxs-lookup"><span data-stu-id="0c10d-191">Password22</span></span></td>
        <td style="text-align:center"><span data-ttu-id="0c10d-192">ILOVEYOU!</span><span class="sxs-lookup"><span data-stu-id="0c10d-192">iloveyou!</span></span></td>
    </tr>
</table>

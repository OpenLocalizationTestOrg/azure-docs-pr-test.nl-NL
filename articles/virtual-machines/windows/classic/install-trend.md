---
title: aaaInstall Trend Micro grondige Security op een virtuele machine | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooinstall en Trend Micro beveiliging configureren op een virtuele machine gemaakt met de Hallo klassieke implementatiemodel in Azure.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="854eb-103">Hoe tooinstall en Trend Micro grondige Security configureren als een Service op een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="854eb-103">How tooinstall and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="854eb-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="854eb-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="854eb-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="854eb-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="854eb-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="854eb-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="854eb-107">Dit artikel ziet u hoe tooinstall en Trend Micro grondige Security configureren als een Service op een nieuwe of bestaande virtuele machine (VM) met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="854eb-107">This article shows you how tooinstall and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="854eb-108">Uitgebreide beveiliging als een Service omvat anti-malwarebeveiliging, een firewall, een inbraakdetectie preventie van systeem en integriteit bewaken.</span><span class="sxs-lookup"><span data-stu-id="854eb-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="854eb-109">Hallo-client is geïnstalleerd als een uitbreiding van beveiliging via Hallo VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="854eb-109">hello client is installed as a security extension via hello VM Agent.</span></span> <span data-ttu-id="854eb-110">Installeer op een nieuwe virtuele machine Hallo grondige beveiligingsagent, als Hallo die VM-Agent automatisch door hello Azure-portal gemaakt wordt.</span><span class="sxs-lookup"><span data-stu-id="854eb-110">On a new virtual machine, you install hello Deep Security Agent, as hello VM Agent is created automatically by hello Azure portal.</span></span>

<span data-ttu-id="854eb-111">Een bestaande virtuele machine gemaakt met de klassieke portal hello, hello Azure CLI of PowerShell hebben mogelijk niet een VM-agent.</span><span class="sxs-lookup"><span data-stu-id="854eb-111">An existing VM created using hello classic portal, hello Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="854eb-112">Voor een bestaande virtuele machine die geen Hallo VM-Agent moet toodownload en eerst installeren.</span><span class="sxs-lookup"><span data-stu-id="854eb-112">For an existing virtual machine that doesn't have hello VM Agent, you need toodownload and install it first.</span></span> <span data-ttu-id="854eb-113">In dit artikel komen beide situaties.</span><span class="sxs-lookup"><span data-stu-id="854eb-113">This article covers both situations.</span></span>

<span data-ttu-id="854eb-114">Als u een abonnement van de Trend Micro voor een on-premises oplossing hebt, kunt u deze toohelp beveiligen van uw virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="854eb-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it toohelp protect your Azure virtual machines.</span></span> <span data-ttu-id="854eb-115">Als u niet een klant nog, kunt u zich aanmelden voor een proefabonnement.</span><span class="sxs-lookup"><span data-stu-id="854eb-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="854eb-116">Zie voor meer informatie over deze oplossing Hallo Trend Micro blogbericht [Microsoft Azure VM-Agent-extensie voor grondige Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="854eb-116">For more information about this solution, see hello Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="854eb-117">Hallo grondige beveiligingsagent installeren op een nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="854eb-117">Install hello Deep Security Agent on a new VM</span></span>

<span data-ttu-id="854eb-118">Hallo [Azure-portal](http://portal.azure.com) kunt u Hallo Trend Micro beveiliging uitbreiding installeren wanneer u een installatiekopie van Hallo **Marketplace** toocreate Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="854eb-118">hello [Azure portal](http://portal.azure.com) lets you install hello Trend Micro security extension when you use an image from hello **Marketplace** toocreate hello virtual machine.</span></span> <span data-ttu-id="854eb-119">Als u één virtuele machine maakt, is met behulp van Hallo portal een eenvoudige manier tooadd bescherming van Trend Micro.</span><span class="sxs-lookup"><span data-stu-id="854eb-119">If you're creating a single virtual machine, using hello portal is an easy way tooadd protection from Trend Micro.</span></span>

<span data-ttu-id="854eb-120">Met behulp van een item in Hallo **Marketplace** een wizard waarmee u kunt Hallo virtuele machine instellen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="854eb-120">Using an entry from hello **Marketplace** opens a wizard that helps you set up hello virtual machine.</span></span> <span data-ttu-id="854eb-121">Gebruik van Hallo **instellingen** blade, Hallo derde venster van Hallo wizard tooinstall Hallo Trend Micro beveiliging extensie.</span><span class="sxs-lookup"><span data-stu-id="854eb-121">You use hello **Settings** blade, hello third panel of hello wizard, tooinstall hello Trend Micro security extension.</span></span>  <span data-ttu-id="854eb-122">Raadpleeg voor algemene instructies [maken van een virtuele machine met Windows in hello Azure-portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="854eb-122">For general instructions, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>

<span data-ttu-id="854eb-123">Als u krijgt toohello **instellingen** blade van de wizard Hallo Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="854eb-123">When you get toohello **Settings** blade of hello wizard, do hello following steps:</span></span>

1. <span data-ttu-id="854eb-124">Klik op **extensies**, klikt u vervolgens op **-extensie toevoegen** in Hallo Volgend deelvenster.</span><span class="sxs-lookup"><span data-stu-id="854eb-124">Click **Extensions**, then click **Add extension** in hello next pane.</span></span>

   ![Beginnen met het Hallo-extensie toevoegen][1]

2. <span data-ttu-id="854eb-126">Selecteer **grondige beveiligingsagent** in Hallo **nieuwe resource** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="854eb-126">Select **Deep Security Agent** in hello **New resource** pane.</span></span> <span data-ttu-id="854eb-127">Klik in deelvenster grondige beveiligingsagent Hallo op **maken**.</span><span class="sxs-lookup"><span data-stu-id="854eb-127">In hello Deep Security Agent pane, click **Create**.</span></span>

   ![Grondige beveiligingsagent identificeren][2]

3. <span data-ttu-id="854eb-129">Voer Hallo **Tenant-id** en **Tenant activering wachtwoord** voor Hallo-extensie.</span><span class="sxs-lookup"><span data-stu-id="854eb-129">Enter hello **Tenant Identifier** and **Tenant Activation Password** for hello extension.</span></span> <span data-ttu-id="854eb-130">Desgewenst kunt u een **beveiliging beleids-id**.</span><span class="sxs-lookup"><span data-stu-id="854eb-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="854eb-131">Klik vervolgens op **OK** tooadd Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="854eb-131">Then, click **OK** tooadd hello client.</span></span>

   ![Geef details op extensie][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="854eb-133">Hallo grondige beveiligingsagent installeren op een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="854eb-133">Install hello Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="854eb-134">tooinstall Hallo-agent op een bestaande virtuele machine, moet u Hallo volgende items:</span><span class="sxs-lookup"><span data-stu-id="854eb-134">tooinstall hello agent on an existing VM, you need hello following items:</span></span>

* <span data-ttu-id="854eb-135">Hello Azure PowerShell-module, versie 0.8.2 of nieuwer, is geïnstalleerd op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="854eb-135">hello Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="854eb-136">U kunt controleren Hallo-versie van Azure PowerShell die u hebt geïnstalleerd met behulp van Hallo **Get-Module azure | tabel opmaken versie** opdracht.</span><span class="sxs-lookup"><span data-stu-id="854eb-136">You can check hello version of Azure PowerShell that you have installed by using hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="854eb-137">Zie voor instructies en een koppeling toohello meest recente versie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="854eb-137">For instructions and a link toohello latest version, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="854eb-138">Meld u aan tooyour Azure-abonnement met `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="854eb-138">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="854eb-139">VM-Agent is geïnstalleerd op de virtuele doelmachine Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="854eb-139">hello VM Agent installed on hello target virtual machine.</span></span>

<span data-ttu-id="854eb-140">Controleer eerst of deze Hallo die VM-Agent is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="854eb-140">First, verify that hello VM Agent is already installed.</span></span> <span data-ttu-id="854eb-141">Vult Hallo cloudservicenaam en de naam van de virtuele machine en voer de volgende opdrachten bij een beheerdersniveau Azure PowerShell-opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="854eb-141">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="854eb-142">Vervang alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens.</span><span class="sxs-lookup"><span data-stu-id="854eb-142">Replace everything within hello quotes, including hello < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="854eb-143">Als u niet Hallo-cloudservice en de naam van virtuele machine weet, voert u **Get-AzureVM** toodisplay dat gegevens voor alle virtuele machines in uw huidige abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="854eb-143">If you don't know hello cloud service and virtual machine name, run **Get-AzureVM** toodisplay that information for all hello virtual machines in your current subscription.</span></span>

<span data-ttu-id="854eb-144">Als hello **write-host** opdracht retourneert **True**, Hallo VM-Agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="854eb-144">If hello **write-host** command returns **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="854eb-145">Als het resultaat **False**, Zie Hallo-instructies en een koppeling toohello downloaden in hello Azure blogbericht [VM-Agent en -extensies: Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="854eb-145">If it returns **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="854eb-146">Als Hallo VM-Agent is geïnstalleerd, moet u deze opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="854eb-146">If hello VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="854eb-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="854eb-147">Next steps</span></span>
<span data-ttu-id="854eb-148">Het duurt enkele minuten duren voordat Hallo agent toostart uitgevoerd wanneer deze is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="854eb-148">It takes a few minutes for hello agent toostart running when it is installed.</span></span> <span data-ttu-id="854eb-149">Daarna moet u tooactivate grondige beveiliging op Hallo virtuele machine zodat deze kan worden beheerd door een grondige Security Manager.</span><span class="sxs-lookup"><span data-stu-id="854eb-149">After that, you need tooactivate Deep Security on hello virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="854eb-150">Zie Hallo artikelen voor aanvullende instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="854eb-150">See hello following articles for additional instructions:</span></span>

* <span data-ttu-id="854eb-151">Trend van artikel over deze oplossing [Instant-On Cloud Security voor Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="854eb-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="854eb-152">Een [Windows PowerShell-voorbeeldscript](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure Hallo virtuele machine</span><span class="sxs-lookup"><span data-stu-id="854eb-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) tooconfigure hello virtual machine</span></span>
* <span data-ttu-id="854eb-153">[Instructies](http://go.microsoft.com/fwlink/?LinkId=404099) voor Hallo-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="854eb-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for hello sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="854eb-154">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="854eb-154">Additional resources</span></span>
<span data-ttu-id="854eb-155">[Hoe toolog op tooa virtuele machine met Windows Server]</span><span class="sxs-lookup"><span data-stu-id="854eb-155">[How toolog on tooa virtual machine running Windows Server]</span></span>

<span data-ttu-id="854eb-156">[Azure VM-extensies en functies]</span><span class="sxs-lookup"><span data-stu-id="854eb-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[Hoe toolog op tooa virtuele machine met Windows Server]:connect-logon.md
[Azure VM-extensies en functies]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409

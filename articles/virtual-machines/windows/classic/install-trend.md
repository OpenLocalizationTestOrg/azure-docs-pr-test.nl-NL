---
title: Trend Micro grondige Security installeren op een virtuele machine | Microsoft Docs
description: In dit artikel wordt beschreven hoe installeren en configureren van Trend Micro beveiliging op een virtuele machine gemaakt met het klassieke implementatiemodel in Azure.
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
ms.openlocfilehash: 911b8f12472dcbda3e6bfeb8c97bf1d04a63e1dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-install-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a><span data-ttu-id="e82d6-103">Trend Micro Deep Security installeren en configureren als een service op een Windows VM</span><span class="sxs-lookup"><span data-stu-id="e82d6-103">How to install and configure Trend Micro Deep Security as a Service on a Windows VM</span></span>
> [!IMPORTANT]
> <span data-ttu-id="e82d6-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e82d6-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e82d6-105">In dit artikel bevat informatie over met behulp van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e82d6-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="e82d6-106">U doet er verstandig aan voor de meeste nieuwe implementaties het Resource Manager-model te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e82d6-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="e82d6-107">In dit artikel leest u hoe installeren en configureren van Trend Micro grondige Security als een Service op een nieuwe of bestaande virtuele machine (VM) met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="e82d6-107">This article shows you how to install and configure Trend Micro Deep Security as a Service on a new or existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="e82d6-108">Uitgebreide beveiliging als een Service omvat anti-malwarebeveiliging, een firewall, een inbraakdetectie preventie van systeem en integriteit bewaken.</span><span class="sxs-lookup"><span data-stu-id="e82d6-108">Deep Security as a Service includes anti-malware protection, a firewall, an intrusion prevention system, and integrity monitoring.</span></span>

<span data-ttu-id="e82d6-109">De client is als een uitbreiding van beveiliging via de VM-Agent geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e82d6-109">The client is installed as a security extension via the VM Agent.</span></span> <span data-ttu-id="e82d6-110">Op een nieuwe virtuele machine installeren u de beveiligingsagent grondige als de VM-Agent automatisch door de Azure-portal gemaakt wordt.</span><span class="sxs-lookup"><span data-stu-id="e82d6-110">On a new virtual machine, you install the Deep Security Agent, as the VM Agent is created automatically by the Azure portal.</span></span>

<span data-ttu-id="e82d6-111">Een bestaande virtuele machine gemaakt met behulp van de klassieke portal, de Azure CLI of PowerShell hebben mogelijk niet een VM-agent.</span><span class="sxs-lookup"><span data-stu-id="e82d6-111">An existing VM created using the classic portal, the Azure CLI, or PowerShell might not have a VM agent.</span></span> <span data-ttu-id="e82d6-112">Voor een bestaande virtuele machine die niet de VM-Agent, die u wilt downloaden en installeer het eerst.</span><span class="sxs-lookup"><span data-stu-id="e82d6-112">For an existing virtual machine that doesn't have the VM Agent, you need to download and install it first.</span></span> <span data-ttu-id="e82d6-113">In dit artikel komen beide situaties.</span><span class="sxs-lookup"><span data-stu-id="e82d6-113">This article covers both situations.</span></span>

<span data-ttu-id="e82d6-114">Als u een abonnement van de Trend Micro voor een on-premises oplossing hebt, kunt u het beveiligen van uw virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="e82d6-114">If you have a current subscription from Trend Micro for an on-premises solution, you can use it to help protect your Azure virtual machines.</span></span> <span data-ttu-id="e82d6-115">Als u niet een klant nog, kunt u zich aanmelden voor een proefabonnement.</span><span class="sxs-lookup"><span data-stu-id="e82d6-115">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="e82d6-116">Zie voor meer informatie over deze oplossing het trendanalyse Micro blogbericht [Microsoft Azure VM-Agent-extensie voor grondige Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span><span class="sxs-lookup"><span data-stu-id="e82d6-116">For more information about this solution, see the Trend Micro blog post [Microsoft Azure VM Agent Extension For Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).</span></span>

## <a name="install-the-deep-security-agent-on-a-new-vm"></a><span data-ttu-id="e82d6-117">De grondige beveiligingsagent installeren op een nieuwe virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e82d6-117">Install the Deep Security Agent on a new VM</span></span>

<span data-ttu-id="e82d6-118">De [Azure-portal](http://portal.azure.com) kunt u de uitbreiding van de beveiliging Trend Micro installeren wanneer u een installatiekopie van het **Marketplace** voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e82d6-118">The [Azure portal](http://portal.azure.com) lets you install the Trend Micro security extension when you use an image from the **Marketplace** to create the virtual machine.</span></span> <span data-ttu-id="e82d6-119">Als u één virtuele machine maakt, is met behulp van de portal een eenvoudige manier om de beveiliging van de Trend Micro toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e82d6-119">If you're creating a single virtual machine, using the portal is an easy way to add protection from Trend Micro.</span></span>

<span data-ttu-id="e82d6-120">Met behulp van een item in de **Marketplace** een wizard waarmee u kunt van de virtuele machine instellen wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="e82d6-120">Using an entry from the **Marketplace** opens a wizard that helps you set up the virtual machine.</span></span> <span data-ttu-id="e82d6-121">U gebruikt de **instellingen** blade, het derde venster van de wizard voor het installeren van de Trend Micro security-extensie.</span><span class="sxs-lookup"><span data-stu-id="e82d6-121">You use the **Settings** blade, the third panel of the wizard, to install the Trend Micro security extension.</span></span>  <span data-ttu-id="e82d6-122">Raadpleeg voor algemene instructies [maken van een virtuele machine waarop Windows wordt uitgevoerd in de Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e82d6-122">For general instructions, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>

<span data-ttu-id="e82d6-123">Wanneer de **instellingen** blade van de wizard de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e82d6-123">When you get to the **Settings** blade of the wizard, do the following steps:</span></span>

1. <span data-ttu-id="e82d6-124">Klik op **extensies**, klikt u vervolgens op **-extensie toevoegen** in het volgende venster.</span><span class="sxs-lookup"><span data-stu-id="e82d6-124">Click **Extensions**, then click **Add extension** in the next pane.</span></span>

   ![Beginnen met het toevoegen van de extensie][1]

2. <span data-ttu-id="e82d6-126">Selecteer **grondige beveiligingsagent** in de **nieuwe resource** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="e82d6-126">Select **Deep Security Agent** in the **New resource** pane.</span></span> <span data-ttu-id="e82d6-127">Klik in het deelvenster grondige beveiligingsagent **maken**.</span><span class="sxs-lookup"><span data-stu-id="e82d6-127">In the Deep Security Agent pane, click **Create**.</span></span>

   ![Grondige beveiligingsagent identificeren][2]

3. <span data-ttu-id="e82d6-129">Voer de **Tenant-id** en **Tenant activering wachtwoord** voor de extensie.</span><span class="sxs-lookup"><span data-stu-id="e82d6-129">Enter the **Tenant Identifier** and **Tenant Activation Password** for the extension.</span></span> <span data-ttu-id="e82d6-130">Desgewenst kunt u een **beveiliging beleids-id**.</span><span class="sxs-lookup"><span data-stu-id="e82d6-130">Optionally, you can enter a **Security Policy Identifier**.</span></span> <span data-ttu-id="e82d6-131">Klik vervolgens op **OK** om toe te voegen van de client.</span><span class="sxs-lookup"><span data-stu-id="e82d6-131">Then, click **OK** to add the client.</span></span>

   ![Geef details op extensie][3]

## <a name="install-the-deep-security-agent-on-an-existing-vm"></a><span data-ttu-id="e82d6-133">De grondige beveiligingsagent installeren op een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e82d6-133">Install the Deep Security Agent on an existing VM</span></span>
<span data-ttu-id="e82d6-134">Als u wilt de agent installeert op een bestaande virtuele machine, moet u de volgende items:</span><span class="sxs-lookup"><span data-stu-id="e82d6-134">To install the agent on an existing VM, you need the following items:</span></span>

* <span data-ttu-id="e82d6-135">De Azure PowerShell-module, versie 0.8.2 of nieuwer, is geïnstalleerd op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e82d6-135">The Azure PowerShell module, version 0.8.2 or newer, installed on your local computer.</span></span> <span data-ttu-id="e82d6-136">U kunt controleren welke versie van Azure PowerShell die u hebt geïnstalleerd met behulp van de **Get-Module azure | tabel opmaken versie** opdracht.</span><span class="sxs-lookup"><span data-stu-id="e82d6-136">You can check the version of Azure PowerShell that you have installed by using the **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="e82d6-137">Zie voor instructies en een koppeling naar de nieuwste versie [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e82d6-137">For instructions and a link to the latest version, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="e82d6-138">Aanmelden bij uw Azure-abonnement met `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="e82d6-138">Log in to your Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="e82d6-139">De VM-Agent is geïnstalleerd op de virtuele doelmachine.</span><span class="sxs-lookup"><span data-stu-id="e82d6-139">The VM Agent installed on the target virtual machine.</span></span>

<span data-ttu-id="e82d6-140">Controleer eerst of de VM-Agent is al geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e82d6-140">First, verify that the VM Agent is already installed.</span></span> <span data-ttu-id="e82d6-141">Vul de cloudservicenaam en de naam van virtuele machine en voer de volgende opdrachten bij een beheerdersniveau Azure PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e82d6-141">Fill in the cloud service name and virtual machine name, and then run the following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="e82d6-142">Vervang alles binnen de aanhalingstekens, met inbegrip van de < en > tekens.</span><span class="sxs-lookup"><span data-stu-id="e82d6-142">Replace everything within the quotes, including the < and > characters.</span></span>

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

<span data-ttu-id="e82d6-143">Als u de cloudservice en de naam van de virtuele machine niet weet, voert u **Get-AzureVM** om weer te geven die gegevens voor alle virtuele machines in uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="e82d6-143">If you don't know the cloud service and virtual machine name, run **Get-AzureVM** to display that information for all the virtual machines in your current subscription.</span></span>

<span data-ttu-id="e82d6-144">Als de **write-host** opdracht retourneert **True**, de VM-Agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e82d6-144">If the **write-host** command returns **True**, the VM Agent is installed.</span></span> <span data-ttu-id="e82d6-145">Als het resultaat **False**, Zie de instructies en een koppeling naar de download in de Azure blogbericht [VM-Agent en -extensies: Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span><span class="sxs-lookup"><span data-stu-id="e82d6-145">If it returns **False**, see the instructions and a link to the download in the Azure blog post [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).</span></span>

<span data-ttu-id="e82d6-146">Als de VM-Agent is geïnstalleerd, moet u deze opdrachten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e82d6-146">If the VM Agent is installed, run these commands.</span></span>

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="e82d6-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e82d6-147">Next steps</span></span>
<span data-ttu-id="e82d6-148">Het duurt enkele minuten duren voordat de agent wilt uitvoeren wanneer deze is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e82d6-148">It takes a few minutes for the agent to start running when it is installed.</span></span> <span data-ttu-id="e82d6-149">Daarna moet u grondige beveiliging op de virtuele machine activeren zodat deze kan worden beheerd door een grondige Security Manager.</span><span class="sxs-lookup"><span data-stu-id="e82d6-149">After that, you need to activate Deep Security on the virtual machine so it can be managed by a Deep Security Manager.</span></span> <span data-ttu-id="e82d6-150">Zie de volgende artikelen voor aanvullende instructies:</span><span class="sxs-lookup"><span data-stu-id="e82d6-150">See the following articles for additional instructions:</span></span>

* <span data-ttu-id="e82d6-151">Trend van artikel over deze oplossing [Instant-On Cloud Security voor Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span><span class="sxs-lookup"><span data-stu-id="e82d6-151">Trend's article about this solution, [Instant-On Cloud Security for Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=404101)</span></span>
* <span data-ttu-id="e82d6-152">Een [Windows PowerShell-voorbeeldscript](http://go.microsoft.com/fwlink/?LinkId=404100) voor het configureren van de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="e82d6-152">A [sample Windows PowerShell script](http://go.microsoft.com/fwlink/?LinkId=404100) to configure the virtual machine</span></span>
* <span data-ttu-id="e82d6-153">[Instructies](http://go.microsoft.com/fwlink/?LinkId=404099) voor het voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e82d6-153">[Instructions](http://go.microsoft.com/fwlink/?LinkId=404099) for the sample</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e82d6-154">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="e82d6-154">Additional resources</span></span>
<span data-ttu-id="e82d6-155">[Aanmelden met een virtuele machine met Windows Server]</span><span class="sxs-lookup"><span data-stu-id="e82d6-155">[How to log on to a virtual machine running Windows Server]</span></span>

<span data-ttu-id="e82d6-156">[Azure VM-extensies en functies]</span><span class="sxs-lookup"><span data-stu-id="e82d6-156">[Azure VM Extensions and features]</span></span>

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
<span data-ttu-id="e82d6-157">[Aanmelden met een virtuele machine met Windows Server]:connect-logon.md</span><span class="sxs-lookup"><span data-stu-id="e82d6-157">[How to log on to a virtual machine running Windows Server]:connect-logon.md</span></span>
<span data-ttu-id="e82d6-158">[Azure VM-extensies en functies]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span><span class="sxs-lookup"><span data-stu-id="e82d6-158">[Azure VM Extensions and features]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409</span></span>

---
title: aaaInstall Symantec Endpoint Protection op een Windows-virtuele machine in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en Hallo Symantec Endpoint Protection security-uitbreiding configureren op een nieuwe of bestaande virtuele machine in Azure gemaakt met de Hallo klassieke implementatiemodel.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a><span data-ttu-id="3b430-103">Hoe tooinstall en Symantec Endpoint Protection configureren op een virtuele machine van Windows</span><span class="sxs-lookup"><span data-stu-id="3b430-103">How tooinstall and configure Symantec Endpoint Protection on a Windows VM</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="3b430-104">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="3b430-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="3b430-105">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3b430-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="3b430-106">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3b430-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="3b430-107">Dit artikel ziet u hoe tooinstall en Hallo Symantec Endpoint Protection-client configureren op een bestaande virtuele machine (VM) met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="3b430-107">This article shows you how tooinstall and configure hello Symantec Endpoint Protection client on an existing virtual machine (VM) running Windows Server.</span></span> <span data-ttu-id="3b430-108">Deze volledige client omvat services zoals virussen en bescherming tegen spyware, firewall en inbraakdetectie te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="3b430-108">This full client includes services such as virus and spyware protection, firewall, and intrusion prevention.</span></span> <span data-ttu-id="3b430-109">Hallo-client is geïnstalleerd als een uitbreiding van de beveiliging met behulp van Hallo VM-Agent.</span><span class="sxs-lookup"><span data-stu-id="3b430-109">hello client is installed as a security extension by using hello VM Agent.</span></span>

<span data-ttu-id="3b430-110">Als u een bestaand abonnement van Symantec voor een on-premises oplossing hebt, kunt u deze tooprotect uw virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="3b430-110">If you have an existing subscription from Symantec for an on-premises solution, you can use it tooprotect your Azure virtual machines.</span></span> <span data-ttu-id="3b430-111">Als u niet een klant nog, kunt u zich aanmelden voor een proefabonnement.</span><span class="sxs-lookup"><span data-stu-id="3b430-111">If you're not a customer yet, you can sign up for a trial subscription.</span></span> <span data-ttu-id="3b430-112">Zie voor meer informatie over deze oplossing [Symantec Endpoint Protection op van Microsoft Azure-platform][Symantec].</span><span class="sxs-lookup"><span data-stu-id="3b430-112">For more information about this solution, see [Symantec Endpoint Protection on Microsoft's Azure platform][Symantec].</span></span> <span data-ttu-id="3b430-113">Deze pagina bevat ook koppelingen toolicensing informatie en instructies voor het installeren van Hallo client als u al een Symantec-klant bent.</span><span class="sxs-lookup"><span data-stu-id="3b430-113">This page also has links toolicensing information and instructions for installing hello client if you're already a Symantec customer.</span></span>

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a><span data-ttu-id="3b430-114">Symantec Endpoint Protection installeren op een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="3b430-114">Install Symantec Endpoint Protection on an existing VM</span></span>
<span data-ttu-id="3b430-115">Voordat u begint, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="3b430-115">Before you begin, you need hello following:</span></span>

* <span data-ttu-id="3b430-116">Hello Azure PowerShell-module, versie 0.8.2 of hoger op de computer.</span><span class="sxs-lookup"><span data-stu-id="3b430-116">hello Azure PowerShell module, version 0.8.2 or later, on your work computer.</span></span> <span data-ttu-id="3b430-117">U kunt controleren Hallo-versie van Azure PowerShell die u hebt geïnstalleerd met Hallo **Get-Module azure | tabel opmaken versie** opdracht.</span><span class="sxs-lookup"><span data-stu-id="3b430-117">You can check hello version of Azure PowerShell that you have installed with hello **Get-Module azure | format-table version** command.</span></span> <span data-ttu-id="3b430-118">Zie voor instructies en een koppeling toohello meest recente versie [hoe tooInstall en configureer Azure PowerShell][PS].</span><span class="sxs-lookup"><span data-stu-id="3b430-118">For instructions and a link toohello latest version, see [How tooInstall and Configure Azure PowerShell][PS].</span></span> <span data-ttu-id="3b430-119">Meld u aan tooyour Azure-abonnement met `Add-AzureAccount`.</span><span class="sxs-lookup"><span data-stu-id="3b430-119">Log in tooyour Azure subscription using `Add-AzureAccount`.</span></span>
* <span data-ttu-id="3b430-120">Hallo VM-Agent uitgevoerd op Hallo Azure virtuele Machine.</span><span class="sxs-lookup"><span data-stu-id="3b430-120">hello VM Agent running on hello Azure Virtual Machine.</span></span>

<span data-ttu-id="3b430-121">Controleer eerst of deze VM-Agent is al geïnstalleerd op de virtuele machine van Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b430-121">First, verify that hello VM Agent is already installed on hello virtual machine.</span></span> <span data-ttu-id="3b430-122">Vult Hallo cloudservicenaam en de naam van de virtuele machine en voer de volgende opdrachten bij een beheerdersniveau Azure PowerShell-opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b430-122">Fill in hello cloud service name and virtual machine name, and then run hello following commands at an administrator-level Azure PowerShell command prompt.</span></span> <span data-ttu-id="3b430-123">Vervang alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens.</span><span class="sxs-lookup"><span data-stu-id="3b430-123">Replace everything within hello quotes, including hello < and > characters.</span></span>

> [!TIP]
> <span data-ttu-id="3b430-124">Als u niet Hallo-cloudservice en de namen van de virtuele machine weet, voert u **Get-AzureVM** toolist Hallo namen voor alle virtuele machines in uw huidige abonnement.</span><span class="sxs-lookup"><span data-stu-id="3b430-124">If you don't know hello cloud service and virtual machine names, run **Get-AzureVM** toolist hello names for all virtual machines in your current subscription.</span></span>

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="3b430-125">Als hello **write-host** opdracht geeft **True**, Hallo VM-Agent is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3b430-125">If hello **write-host** command displays **True**, hello VM Agent is installed.</span></span> <span data-ttu-id="3b430-126">Als deze wordt weergegeven in **False**, Zie Hallo-instructies en een koppeling toohello downloaden in hello Azure blogbericht [VM-Agent en -extensies: Part 2][Agent].</span><span class="sxs-lookup"><span data-stu-id="3b430-126">If it displays **False**, see hello instructions and a link toohello download in hello Azure blog post [VM Agent and Extensions - Part 2][Agent].</span></span>

<span data-ttu-id="3b430-127">Als Hallo VM-Agent is geïnstalleerd, voert u deze opdrachten tooinstall Hallo Symantec Endpoint Protection-agent.</span><span class="sxs-lookup"><span data-stu-id="3b430-127">If hello VM Agent is installed, run these commands tooinstall hello Symantec Endpoint Protection agent.</span></span>

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

<span data-ttu-id="3b430-128">tooverify die Hallo Symantec security-uitbreiding is geïnstalleerd en is bijgewerkt:</span><span class="sxs-lookup"><span data-stu-id="3b430-128">tooverify that hello Symantec security extension has been installed and is up-to-date:</span></span>

1. <span data-ttu-id="3b430-129">Meld u aan toohello virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="3b430-129">Log on toohello virtual machine.</span></span> <span data-ttu-id="3b430-130">Zie voor instructies [hoe tooLog op virtuele Machine Running Windows Server tooa][Logon].</span><span class="sxs-lookup"><span data-stu-id="3b430-130">For instructions, see [How tooLog on tooa Virtual Machine Running Windows Server][Logon].</span></span>
2. <span data-ttu-id="3b430-131">Voor Windows Server 2008 R2, klikt u op **Start > Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="3b430-131">For Windows Server 2008 R2, click **Start > Symantec Endpoint Protection**.</span></span> <span data-ttu-id="3b430-132">Typ voor Windows Server 2012 of Windows Server 2012 R2, vanuit het startscherm hello, **Symantec**, en klik vervolgens op **Symantec Endpoint Protection**.</span><span class="sxs-lookup"><span data-stu-id="3b430-132">For Windows Server 2012 or Windows Server 2012 R2, from hello start screen, type **Symantec**, and then click **Symantec Endpoint Protection**.</span></span>
3. <span data-ttu-id="3b430-133">Van Hallo **Status** tabblad Hallo **Status Symantec Endpoint Protection** venster updates toepassen of opnieuw opstarten indien nodig.</span><span class="sxs-lookup"><span data-stu-id="3b430-133">From hello **Status** tab of hello **Status-Symantec Endpoint Protection** window, apply updates or restart if needed.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="3b430-134">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="3b430-134">Additional resources</span></span>
<span data-ttu-id="3b430-135">[Hoe tooLog op tooa Virtual Machine Running Windows Server][Logon]</span><span class="sxs-lookup"><span data-stu-id="3b430-135">[How tooLog on tooa Virtual Machine Running Windows Server][Logon]</span></span>

<span data-ttu-id="3b430-136">[Azure VM-extensies en functies][Ext]</span><span class="sxs-lookup"><span data-stu-id="3b430-136">[Azure VM Extensions and Features][Ext]</span></span>

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493

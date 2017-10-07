---
title: toegang tot Azure-eindpunt aaaManage lijsten beheren | PowerShell | Klassieke | Microsoft Docs
description: Meer informatie over hoe toomanage ACL's met PowerShell
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="400d9-103">Eindpunt toegangsbeheerlijsten met PowerShell in het klassieke implementatiemodel Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="400d9-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="400d9-104">U kunt maken en beheren van netwerk-toegangsbeheerlijsten (ACL's) voor eindpunten met behulp van Azure PowerShell of in het Hallo-beheerportal.</span><span class="sxs-lookup"><span data-stu-id="400d9-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="400d9-105">In dit onderwerp vindt u procedures voor ACL algemene taken die u kunt uitvoeren met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="400d9-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="400d9-106">Zie voor Hallo overzicht van Azure PowerShell cmdlets [Azure Management-Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span><span class="sxs-lookup"><span data-stu-id="400d9-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="400d9-107">Zie voor meer informatie over ACL's, [wat is er een netwerk lijst ACL (Access Control)?](virtual-networks-acl.md).</span><span class="sxs-lookup"><span data-stu-id="400d9-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="400d9-108">Als u uw ACL's toomanage wilt met behulp van Hallo-beheerportal, Zie [hoe tooSet Up eindpunten tooa virtuele Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="400d9-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="400d9-109">Netwerk-ACL's beheren met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="400d9-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="400d9-110">U kunt Azure PowerShell-cmdlets toocreate, verwijderen en te configureren (set) netwerk toegangsbeheerlijsten (ACL's).</span><span class="sxs-lookup"><span data-stu-id="400d9-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="400d9-111">Vindt u enkele voorbeelden van een aantal Hallo manieren waarop die u een ACL die met behulp van PowerShell kunt configureren.</span><span class="sxs-lookup"><span data-stu-id="400d9-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="400d9-112">tooretrieve een volledige lijst met Hallo ACL PowerShell-cmdlets, kunt u een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="400d9-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="400d9-113">Maken van een netwerk-ACL met regels die toegang vanaf een extern subnet verlenen</span><span class="sxs-lookup"><span data-stu-id="400d9-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="400d9-114">Hallo in het volgende voorbeeld ziet u een manier toocreate een nieuwe ACL dat regels bevat.</span><span class="sxs-lookup"><span data-stu-id="400d9-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="400d9-115">Deze ACL wordt vervolgens toegepast eindpunt van de virtuele machine tooa.</span><span class="sxs-lookup"><span data-stu-id="400d9-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="400d9-116">Hallo ACL-regels in Hallo in het volgende voorbeeld wordt toegang toestaan via een extern subnet.</span><span class="sxs-lookup"><span data-stu-id="400d9-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="400d9-117">een nieuwe netwerk-ACL met regels voor toestaan voor een extern subnet toocreate open een Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="400d9-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="400d9-118">Kopiëren en plakken onderstaande Hallo script configureren met uw eigen waarden Hallo-script en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="400d9-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="400d9-119">Hallo nieuw netwerk ACL-object maken.</span><span class="sxs-lookup"><span data-stu-id="400d9-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="400d9-120">Een regel waarmee de toegang van een extern subnet instellen.</span><span class="sxs-lookup"><span data-stu-id="400d9-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="400d9-121">In onderstaande Hallo voorbeeld, stelt u de regel *100* (dit heeft voorrang op de regel 200 en hoger) tooallow Hallo extern subnet *10.0.0.0/8* toegang tot toohello virtuele machine-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="400d9-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="400d9-122">Hallo waarden vervangt door uw eigen configuratievereisten.</span><span class="sxs-lookup"><span data-stu-id="400d9-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="400d9-123">Hallo-naam "SharePoint ACL-config" moet worden vervangen door Hallo beschrijvende naam die u toocall met deze regel wilt.</span><span class="sxs-lookup"><span data-stu-id="400d9-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="400d9-124">Herhaal Hallo-cmdlet, waarbij Hallo waarden vervangt door uw eigen configuratievereisten voor extra regels.</span><span class="sxs-lookup"><span data-stu-id="400d9-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="400d9-125">Worden ervoor toochange Hallo regel nummer volgorde tooreflect Hallo volgorde waarin u Hallo regels toobe toegepast.</span><span class="sxs-lookup"><span data-stu-id="400d9-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="400d9-126">Hallo minder regel heeft voorrang op Hallo hoger nummer.</span><span class="sxs-lookup"><span data-stu-id="400d9-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="400d9-127">Vervolgens kunt u een nieuw eindpunt (toevoegen) maken of Hallo ACL voor een bestaand eindpunt (Set) ingesteld.</span><span class="sxs-lookup"><span data-stu-id="400d9-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="400d9-128">In dit voorbeeld wordt we voegen dat een nieuw eindpunt van de virtuele machine genaamd 'web' en update Hallo virtuele machine-eindpunt met de Hallo ACL-instellingen.</span><span class="sxs-lookup"><span data-stu-id="400d9-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="400d9-129">Vervolgens Hallo cmdlets met elkaar combineren en Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="400d9-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="400d9-130">In dit voorbeeld hello gecombineerde cmdlets eruit als volgt:</span><span class="sxs-lookup"><span data-stu-id="400d9-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="400d9-131">Verwijderen van een netwerk-ACL-regel waarmee de toegang van een extern subnet</span><span class="sxs-lookup"><span data-stu-id="400d9-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="400d9-132">Hallo in het volgende voorbeeld ziet u een manier tooremove een netwerk-ACL-regel.</span><span class="sxs-lookup"><span data-stu-id="400d9-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="400d9-133">een regel netwerk ACL met toestaan tooremove regels voor een extern subnet, open een Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="400d9-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="400d9-134">Kopiëren en plakken onderstaande Hallo script configureren met uw eigen waarden Hallo-script en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="400d9-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="400d9-135">Eerste stap is tooget Hallo netwerk ACL-object voor het eindpunt van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="400d9-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="400d9-136">Vervolgens verwijdert u Hallo ACL-regel.</span><span class="sxs-lookup"><span data-stu-id="400d9-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="400d9-137">In dit geval wordt het wilt verwijderen op regel-ID.</span><span class="sxs-lookup"><span data-stu-id="400d9-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="400d9-138">Hiermee wordt alleen Hallo regel-ID 0 uit Hallo ACL verwijderd.</span><span class="sxs-lookup"><span data-stu-id="400d9-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="400d9-139">Hallo ACL-object wordt niet verwijderd uit het eindpunt van de virtuele machine Hallo.</span><span class="sxs-lookup"><span data-stu-id="400d9-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="400d9-140">U moet vervolgens toepassen Hallo netwerk ACL-object toohello virtuele machine eindpunt en Hallo virtuele machine bijwerken.</span><span class="sxs-lookup"><span data-stu-id="400d9-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="400d9-141">Een netwerk-ACL verwijderen uit het eindpunt van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="400d9-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="400d9-142">In bepaalde gevallen, kunt u tooremove een netwerk-ACL-object van het eindpunt van een virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="400d9-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="400d9-143">toodo dat openen van een Azure PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="400d9-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="400d9-144">Kopiëren en plakken onderstaande Hallo script configureren met uw eigen waarden Hallo-script en vervolgens Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="400d9-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="400d9-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="400d9-145">Next steps</span></span>
[<span data-ttu-id="400d9-146">Wat is een netwerk lijst ACL (Access Control)?</span><span class="sxs-lookup"><span data-stu-id="400d9-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)


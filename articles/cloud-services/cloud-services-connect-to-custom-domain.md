---
title: een Cloudservice tooa aaaConnect aangepaste domeincontroller | Microsoft Docs
description: Meer informatie over hoe tooconnect uw web/worker rollen tooa aangepaste AD-domein met behulp van PowerShell en uitbreiding van AD-domein
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 1e2d7c87-d254-4e7a-a832-67f84411ec95
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 9540190ccf17c03e55159c6c68429eee29e0a558
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-azure-cloud-services-roles-tooa-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="4b9e0-103">Verbinding maken met Azure Cloud Services-functies tooa aangepaste AD-domeincontroller worden gehost in Azure</span><span class="sxs-lookup"><span data-stu-id="4b9e0-103">Connecting Azure Cloud Services Roles tooa custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="4b9e0-104">Er wordt eerst een virtueel netwerk (VNet) instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="4b9e0-105">Er wordt een Active Directory-domeincontroller (gehost op een virtuele Machine van Azure) toohello VNet toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) toohello VNet.</span></span> <span data-ttu-id="4b9e0-106">Vervolgens wordt er bestaande cloud service rollen toohello vooraf gemaakte VNet toevoegen en verbind ze toohello domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-106">Next, we will add existing cloud service roles toohello pre-created VNet, then connect them toohello Domain Controller.</span></span>

<span data-ttu-id="4b9e0-107">Voordat we aan de slag, paar van tookeep rekening dingen:</span><span class="sxs-lookup"><span data-stu-id="4b9e0-107">Before we get started, couple of things tookeep in mind:</span></span>

1. <span data-ttu-id="4b9e0-108">Deze zelfstudie wordt gebruikgemaakt van PowerShell, dus zorg ervoor dat u hebt Azure PowerShell is geïnstalleerd en gereed toogo.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready toogo.</span></span> <span data-ttu-id="4b9e0-109">Zie tooget hulp bij het instellen van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b9e0-109">tooget help with setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="4b9e0-110">Uw AD-domeincontroller en de functie Web/Worker-exemplaren moeten toobe in Hallo VNet.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-110">Your AD Domain Controller and Web/Worker Role instances need toobe in hello VNet.</span></span>

<span data-ttu-id="4b9e0-111">Volg deze stapsgewijze handleiding en als u problemen ondervindt uitvoert, laat ons een opmerking achter Hallo Hallo artikel.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at hello end of hello article.</span></span> <span data-ttu-id="4b9e0-112">Iemand krijg je terug tooyou (Ja, we opmerkingen lezen).</span><span class="sxs-lookup"><span data-stu-id="4b9e0-112">Someone will get back tooyou (yes, we do read comments).</span></span>

<span data-ttu-id="4b9e0-113">Hallo-netwerk waarnaar wordt verwezen door de cloudservice Hallo moet een **klassiek virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-113">hello network that is referenced by hello cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="4b9e0-114">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="4b9e0-114">Create a Virtual Network</span></span>
<span data-ttu-id="4b9e0-115">U kunt een virtueel netwerk maken in Azure met behulp van hello Azure-portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-115">You can create a Virtual Network in Azure using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="4b9e0-116">Voor deze zelfstudie gebruiken we PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="4b9e0-117">een virtueel netwerk met toocreate hello Azure portal, Zie [virtueel netwerk maken](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4b9e0-117">toocreate a Virtual Network using hello Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

```powershell
#Create Virtual Network

$vnetStr =
@"<?xml version="1.0" encoding="utf-8"?>
<NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
    <VirtualNetworkConfiguration>
    <VirtualNetworkSites>
        <VirtualNetworkSite name="[your-vnet-name]" Location="West US">
        <AddressSpace>
            <AddressPrefix>[your-address-prefix]</AddressPrefix>
        </AddressSpace>
        <Subnets>
            <Subnet name="[your-subnet-name]">
            <AddressPrefix>[your-subnet-range]</AddressPrefix>
            </Subnet>
        </Subnets>
        </VirtualNetworkSite>
    </VirtualNetworkSites>
    </VirtualNetworkConfiguration>
</NetworkConfiguration>
"@;

$vnetConfigPath = "<path-to-vnet-config>"
Set-AzureVNetConfig -ConfigurationPath $vnetConfigPath
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="4b9e0-118">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="4b9e0-118">Create a Virtual Machine</span></span>
<span data-ttu-id="4b9e0-119">Als u klaar bent met het instellen van Hallo virtueel netwerk, moet u toocreate een AD-domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-119">Once you have completed setting up hello Virtual Network, you will need toocreate an AD Domain Controller.</span></span> <span data-ttu-id="4b9e0-120">Voor deze zelfstudie stellen we van een AD-domeincontroller op een virtuele Machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="4b9e0-121">toodo hiervan kan een virtuele machine via PowerShell met behulp van de volgende opdrachten Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="4b9e0-121">toodo this, create a virtual machine through PowerShell using hello following commands:</span></span>

```powershell
# Initialize variables
# VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.

$vnetname = '<your-vnet-name>'
$subnetname = '<your-subnet-name>'
$vmsvc1 = '<your-hosted-service>'
$vm1 = '<your-vm-name>'
$username = '<your-username>'
$password = '<your-password>'
$affgrp = '<your- affgrp>'

# Create a VM and add it toohello Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-tooa-domain-controller"></a><span data-ttu-id="4b9e0-122">De virtuele Machine tooa domeincontroller promoveren</span><span class="sxs-lookup"><span data-stu-id="4b9e0-122">Promote your Virtual Machine tooa Domain Controller</span></span>
<span data-ttu-id="4b9e0-123">tooconfigure hello virtuele Machine als een AD-domeincontroller, wordt u toolog in toohello VM nodig hebt en configureert.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-123">tooconfigure hello Virtual Machine as an AD Domain Controller, you will need toolog in toohello VM and configure it.</span></span>

<span data-ttu-id="4b9e0-124">toolog in toohello VM ophalen Hallo RDP-bestand via PowerShell, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="4b9e0-124">toolog in toohello VM, you can get hello RDP file through PowerShell, use hello following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="4b9e0-125">Zodra u toohello VM bent aangemeld, instellen van uw virtuele Machine als AD-domeincontroller door de volgende Hallo stapsgewijze handleiding op [hoe tooset van uw klant AD-domeincontroller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="4b9e0-125">Once you are signed in toohello VM, set up your Virtual Machine as an AD Domain Controller by following hello step-by-step guide on [How tooset up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-toohello-virtual-network"></a><span data-ttu-id="4b9e0-126">Uw Cloudservice toohello virtueel netwerk toevoegen</span><span class="sxs-lookup"><span data-stu-id="4b9e0-126">Add your Cloud Service toohello Virtual Network</span></span>
<span data-ttu-id="4b9e0-127">Vervolgens moet u tooadd uw cloud service-implementatie toohello nieuwe VNet.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-127">Next, you need tooadd your cloud service deployment toohello new VNet.</span></span> <span data-ttu-id="4b9e0-128">toodo dit uw cloud service cscfg wijzigen door toe te voegen Hallo relevante secties tooyour cscfg met Visual Studio of Hallo editor naar keuze.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-128">toodo this, modify your cloud service cscfg by adding hello relevant sections tooyour cscfg using Visual Studio or hello editor of your choice.</span></span>

```xml
<ServiceConfiguration serviceName="[hosted-service-name]" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="[os-family]" osVersion="*">
    <Role name="[role-name]">
    <Instances count="[number-of-instances]" />
    </Role>
    <NetworkConfiguration>

    <!--optional-->
    <Dns>
        <DnsServers><DnsServer name="[dns-server-name]" IPAddress="[ip-address]" /></DnsServers>
    </Dns>
    <!--optional-->

    <!--VNet settings
        VNet and subnet must be classic virtual network resources, not Azure Resource Manager resources.-->
    <VirtualNetworkSite name="[virtual-network-name]" />
    <AddressAssignments>
        <InstanceAddress roleName="[role-name]">
        <Subnets>
            <Subnet name="[subnet-name]" />
        </Subnets>
        </InstanceAddress>
    </AddressAssignments>
    <!--VNet settings-->

    </NetworkConfiguration>
</ServiceConfiguration>
```

<span data-ttu-id="4b9e0-129">Vervolgens uw cloud services-project te bouwen en implementeren van deze tooAzure.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-129">Next build your cloud services project and deploy it tooAzure.</span></span> <span data-ttu-id="4b9e0-130">Zie tooget hulp bij het implementeren van uw cloud services-pakket-tooAzure [hoe tooCreate en implementeren van een Service in de Cloud](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="4b9e0-130">tooget help with deploying your cloud services package tooAzure, see [How tooCreate and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-toohello-domain"></a><span data-ttu-id="4b9e0-131">Verbinding maken met uw web/worker rollen toohello domein</span><span class="sxs-lookup"><span data-stu-id="4b9e0-131">Connect your web/worker roles toohello domain</span></span>
<span data-ttu-id="4b9e0-132">Zodra uw cloudserviceproject is geïmplementeerd in Azure, verbinding maken met uw rol exemplaren toohello aangepaste AD-domein met Hallo uitbreiding van AD-domein.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-132">Once your cloud service project is deployed on Azure, connect your role instances toohello custom AD domain using hello AD Domain Extension.</span></span> <span data-ttu-id="4b9e0-133">tooadd hello AD-domein extensie tooyour bestaande cloud services-implementatie- en join Hallo aangepast domein, uitvoeren Hallo opdrachten in PowerShell te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b9e0-133">tooadd hello AD Domain Extension tooyour existing cloud services deployment and join hello custom domain, execute hello following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension toohello cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="4b9e0-134">En dat is alles.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-134">And that's it.</span></span>

<span data-ttu-id="4b9e0-135">Uw cloudservices moet gekoppelde tooyour aangepaste domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-135">Your cloud services should be joined tooyour custom domain controller.</span></span> <span data-ttu-id="4b9e0-136">Als u wilt meer informatie over verschillende opties beschikbaar voor Hallo toolearn hoe tooconfigure uitbreiding van AD-domein, gebruik Hallo PowerShell helpen.</span><span class="sxs-lookup"><span data-stu-id="4b9e0-136">If you would like toolearn more about hello different options available for how tooconfigure AD Domain Extension, use hello PowerShell help.</span></span> <span data-ttu-id="4b9e0-137">Een aantal voorbeelden volgt:</span><span class="sxs-lookup"><span data-stu-id="4b9e0-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```

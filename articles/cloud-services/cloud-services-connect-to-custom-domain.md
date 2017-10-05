---
title: Verbinding maken met een Cloudservice met een aangepaste domeincontroller | Microsoft Docs
description: Informatie over het verbinden van uw web/worker rollen aan een aangepast AD-domein met behulp van PowerShell en uitbreiding van AD-domein
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
ms.openlocfilehash: 17f6918371678ac849198bff4e3b3eea8678c660
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connecting-azure-cloud-services-roles-to-a-custom-ad-domain-controller-hosted-in-azure"></a><span data-ttu-id="085cc-103">Verbinding maken met Azure Cloud Services-functies van een aangepaste gehost in Azure AD Domain-Controller</span><span class="sxs-lookup"><span data-stu-id="085cc-103">Connecting Azure Cloud Services Roles to a custom AD Domain Controller hosted in Azure</span></span>
<span data-ttu-id="085cc-104">Er wordt eerst een virtueel netwerk (VNet) instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="085cc-104">We will first set up a Virtual Network (VNet) in Azure.</span></span> <span data-ttu-id="085cc-105">Er wordt een Active Directory-domeincontroller (gehost op een virtuele Machine van Azure) toegevoegd aan het VNet.</span><span class="sxs-lookup"><span data-stu-id="085cc-105">We will then add an Active Directory Domain Controller (hosted on an Azure Virtual Machine) to the VNet.</span></span> <span data-ttu-id="085cc-106">Er wordt vervolgens bestaande cloud service rollen toevoegen aan de vooraf gemaakte VNet en verbind ze met de domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="085cc-106">Next, we will add existing cloud service roles to the pre-created VNet, then connect them to the Domain Controller.</span></span>

<span data-ttu-id="085cc-107">Voordat we aan de slag, enkele dingen rekening moet houden:</span><span class="sxs-lookup"><span data-stu-id="085cc-107">Before we get started, couple of things to keep in mind:</span></span>

1. <span data-ttu-id="085cc-108">Deze zelfstudie maakt gebruik van PowerShell, dus zorg ervoor dat u hebt Azure PowerShell is geïnstalleerd en klaar voor gebruik.</span><span class="sxs-lookup"><span data-stu-id="085cc-108">This tutorial uses PowerShell, so make sure you have Azure PowerShell installed and ready to go.</span></span> <span data-ttu-id="085cc-109">Zie voor hulp bij het instellen van Azure PowerShell, [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="085cc-109">To get help with setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="085cc-110">Uw AD-domeincontroller en de functie Web/Worker-exemplaren moeten in het VNet.</span><span class="sxs-lookup"><span data-stu-id="085cc-110">Your AD Domain Controller and Web/Worker Role instances need to be in the VNet.</span></span>

<span data-ttu-id="085cc-111">Volg deze stapsgewijze handleiding en als u problemen ondervindt uitvoert, laat ons een opmerking aan het einde van het artikel.</span><span class="sxs-lookup"><span data-stu-id="085cc-111">Follow this step-by-step guide and if you run into any issues, leave us a comment at the end of the article.</span></span> <span data-ttu-id="085cc-112">Iemand anders wordt u zo snel (Ja, we opmerkingen lezen).</span><span class="sxs-lookup"><span data-stu-id="085cc-112">Someone will get back to you (yes, we do read comments).</span></span>

<span data-ttu-id="085cc-113">Het netwerk waarnaar wordt verwezen door de cloudservice moet een **klassiek virtueel netwerk**.</span><span class="sxs-lookup"><span data-stu-id="085cc-113">The network that is referenced by the cloud service must be a **classic virtual network**.</span></span>

## <a name="create-a-virtual-network"></a><span data-ttu-id="085cc-114">Een virtueel netwerk maken</span><span class="sxs-lookup"><span data-stu-id="085cc-114">Create a Virtual Network</span></span>
<span data-ttu-id="085cc-115">U kunt een virtueel netwerk maken in Azure met behulp van de Azure-portal of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="085cc-115">You can create a Virtual Network in Azure using the Azure portal or PowerShell.</span></span> <span data-ttu-id="085cc-116">Voor deze zelfstudie gebruiken we PowerShell.</span><span class="sxs-lookup"><span data-stu-id="085cc-116">For this tutorial, we will use PowerShell.</span></span> <span data-ttu-id="085cc-117">Zie het maken van een virtueel netwerk met de Azure-portal [virtueel netwerk maken](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="085cc-117">To create a Virtual Network using the Azure portal, see [Create Virtual Network](../virtual-network/virtual-networks-create-vnet-arm-pportal.md).</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="085cc-118">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="085cc-118">Create a Virtual Machine</span></span>
<span data-ttu-id="085cc-119">Als u klaar bent met het instellen van het virtuele netwerk, moet u een AD-domeincontroller maken.</span><span class="sxs-lookup"><span data-stu-id="085cc-119">Once you have completed setting up the Virtual Network, you will need to create an AD Domain Controller.</span></span> <span data-ttu-id="085cc-120">Voor deze zelfstudie stellen we van een AD-domeincontroller op een virtuele Machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="085cc-120">For this tutorial, we will be setting up an AD Domain Controller on an Azure Virtual Machine.</span></span>

<span data-ttu-id="085cc-121">Om dit te doen, maakt u een virtuele machine via PowerShell met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="085cc-121">To do this, create a virtual machine through PowerShell using the following commands:</span></span>

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

# Create a VM and add it to the Virtual Network

New-AzureQuickVM -Windows -ServiceName $vmsvc1 -Name $vm1 -ImageName $imgname -AdminUsername $username -Password $password -AffinityGroup $affgrp -SubnetNames $subnetname -VNetName $vnetname
```

## <a name="promote-your-virtual-machine-to-a-domain-controller"></a><span data-ttu-id="085cc-122">De virtuele Machine naar een domeincontroller promoveren</span><span class="sxs-lookup"><span data-stu-id="085cc-122">Promote your Virtual Machine to a Domain Controller</span></span>
<span data-ttu-id="085cc-123">Voor het configureren van de virtuele Machine als een AD-domeincontroller, moet u aanmelden bij de virtuele machine en configureert.</span><span class="sxs-lookup"><span data-stu-id="085cc-123">To configure the Virtual Machine as an AD Domain Controller, you will need to log in to the VM and configure it.</span></span>

<span data-ttu-id="085cc-124">Meld u bij naar de virtuele machine, kunt u het RDP-bestand downloaden via PowerShell, gebruikt u de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="085cc-124">To log in to the VM, you can get the RDP file through PowerShell, use the following commands:</span></span>

```powershell
# Get RDP file
Get-AzureRemoteDesktopFile -ServiceName $vmsvc1 -Name $vm1 -LocalPath <rdp-file-path>
```

<span data-ttu-id="085cc-125">Nadat u bent aangemeld bij de virtuele machine, instellen van uw virtuele Machine als AD-domeincontroller door de stapsgewijze handleiding volgen op [het instellen van uw klant AD-domeincontroller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span><span class="sxs-lookup"><span data-stu-id="085cc-125">Once you are signed in to the VM, set up your Virtual Machine as an AD Domain Controller by following the step-by-step guide on [How to set up your customer AD Domain Controller](http://social.technet.microsoft.com/wiki/contents/articles/12370.windows-server-2012-set-up-your-first-domain-controller-step-by-step.aspx).</span></span>

## <a name="add-your-cloud-service-to-the-virtual-network"></a><span data-ttu-id="085cc-126">Uw Cloudservice toevoegen aan het virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="085cc-126">Add your Cloud Service to the Virtual Network</span></span>
<span data-ttu-id="085cc-127">Vervolgens moet u uw cloud service-implementatie toevoegen aan de nieuwe VNet.</span><span class="sxs-lookup"><span data-stu-id="085cc-127">Next, you need to add your cloud service deployment to the new VNet.</span></span> <span data-ttu-id="085cc-128">U doet dit door uw cscfg cloud-service te wijzigen door de relevante secties toe te voegen aan uw cscfg met Visual Studio of de editor van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="085cc-128">To do this, modify your cloud service cscfg by adding the relevant sections to your cscfg using Visual Studio or the editor of your choice.</span></span>

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

<span data-ttu-id="085cc-129">Naast uw cloud services-project te bouwen en deze implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="085cc-129">Next build your cloud services project and deploy it to Azure.</span></span> <span data-ttu-id="085cc-130">Als u hulp bij het implementeren van uw cloud services-pakket naar Azure, Zie [maken en implementeren van een Cloud-Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span><span class="sxs-lookup"><span data-stu-id="085cc-130">To get help with deploying your cloud services package to Azure, see [How to Create and Deploy a Cloud Service](cloud-services-how-to-create-deploy.md#how-to-deploy-a-cloud-service)</span></span>

## <a name="connect-your-webworker-roles-to-the-domain"></a><span data-ttu-id="085cc-131">Uw web-/ werkrollen verbindt met het domein</span><span class="sxs-lookup"><span data-stu-id="085cc-131">Connect your web/worker roles to the domain</span></span>
<span data-ttu-id="085cc-132">Zodra uw cloudserviceproject is geïmplementeerd in Azure, moet u uw rolinstanties verbinding met het aangepaste AD-domein met de extensie van de AD-domein.</span><span class="sxs-lookup"><span data-stu-id="085cc-132">Once your cloud service project is deployed on Azure, connect your role instances to the custom AD domain using the AD Domain Extension.</span></span> <span data-ttu-id="085cc-133">Voor de uitbreiding van AD-domein toevoegen aan uw bestaande implementatie van de cloud-services en deelnemen aan het aangepaste domein, voert u de volgende opdrachten uit in PowerShell:</span><span class="sxs-lookup"><span data-stu-id="085cc-133">To add the AD Domain Extension to your existing cloud services deployment and join the custom domain, execute the following commands in PowerShell:</span></span>

```powershell
# Initialize domain variables

$domain = '<your-domain-name>'
$dmuser = '$domain\<your-username>'
$dmpswd = '<your-domain-password>'
$dmspwd = ConvertTo-SecureString $dmpswd -AsPlainText -Force
$dmcred = New-Object System.Management.Automation.PSCredential ($dmuser, $dmspwd)

# Add AD Domain Extension to the cloud service roles

Set-AzureServiceADDomainExtension -Service <your-cloud-service-hosted-service-name> -Role <your-role-name> -Slot <staging-or-production> -DomainName $domain -Credential $dmcred -JoinOption 35
```

<span data-ttu-id="085cc-134">En dat is alles.</span><span class="sxs-lookup"><span data-stu-id="085cc-134">And that's it.</span></span>

<span data-ttu-id="085cc-135">Uw cloudservices moeten worden toegevoegd aan uw aangepaste domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="085cc-135">Your cloud services should be joined to your custom domain controller.</span></span> <span data-ttu-id="085cc-136">Als u meer informatie over de verschillende opties voor het configureren van de uitbreiding van AD-domein wilt, gebruikt u de PowerShell-help.</span><span class="sxs-lookup"><span data-stu-id="085cc-136">If you would like to learn more about the different options available for how to configure AD Domain Extension, use the PowerShell help.</span></span> <span data-ttu-id="085cc-137">Een aantal voorbeelden volgt:</span><span class="sxs-lookup"><span data-stu-id="085cc-137">A couple of examples follow:</span></span>

```powershell
help Set-AzureServiceADDomainExtension
help New-AzureServiceADDomainExtensionConfig
```

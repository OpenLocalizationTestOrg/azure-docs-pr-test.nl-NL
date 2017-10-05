---
title: 'Azure Active Directory Domain Services: Beheerdershandleiding | Microsoft Docs'
description: Windows virtuele machine toevoegen aan een beheerd domein met behulp van Azure PowerShell en het klassieke implementatiemodel.
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 9143b843-7327-43c3-baab-6e24a18db25e
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1bb1546fb616131a1e1868a0d0610c4cad5d73e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="join-a-windows-server-virtual-machine-to-a-managed-domain-using-powershell"></a><span data-ttu-id="e9c58-103">Windows Server een virtuele machine toevoegen aan een beheerd domein met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9c58-103">Join a Windows Server virtual machine to a managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="e9c58-104">Klassieke Azure-portal - Windows</span><span class="sxs-lookup"><span data-stu-id="e9c58-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="e9c58-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="e9c58-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="e9c58-106">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="e9c58-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="e9c58-107">Dit artikel gaat over het gebruik van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="e9c58-107">This article covers using the classic deployment model.</span></span> <span data-ttu-id="e9c58-108">Azure AD Domain Services biedt momenteel geen ondersteuning voor het Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="e9c58-108">Azure AD Domain Services does not currently support the Resource Manager model.</span></span>
>
>

<span data-ttu-id="e9c58-109">Deze stappen ziet u hoe u kunt een set van Azure PowerShell-opdrachten die maken en vooraf configureren van een op basis van Windows Azure virtuele machine met behulp van een benadering bouwsteen aanpassen.</span><span class="sxs-lookup"><span data-stu-id="e9c58-109">These steps show you how to customize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="e9c58-110">Deze stappen kunt u een op basis van Windows Azure virtuele machine maken en toevoegen aan een beheerd domein van Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e9c58-110">These steps help you build a Windows-based Azure virtual machine and join it to an Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="e9c58-111">Deze stappen volgt een benadering invullen-in-the-lege waarden voor het maken van Azure PowerShell-opdrachtsets.</span><span class="sxs-lookup"><span data-stu-id="e9c58-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="e9c58-112">Deze methode kan nuttig zijn als u niet bekend met PowerShell bent of u weten welke waarden u wilt moet opgeven voor een geslaagde configuratie.</span><span class="sxs-lookup"><span data-stu-id="e9c58-112">This approach can be useful if you are new to PowerShell or you want to know what values to specify for successful configuration.</span></span> <span data-ttu-id="e9c58-113">Geavanceerde PowerShell-gebruikers kunnen de opdrachten en vervang hun eigen waarden voor de variabelen (de regels die beginnen met '$').</span><span class="sxs-lookup"><span data-stu-id="e9c58-113">Advanced PowerShell users can take the commands and substitute their own values for the variables (the lines beginning with "$").</span></span>

<span data-ttu-id="e9c58-114">Als u dit nog niet hebt gedaan, gebruikt u de instructies in [installeren en configureren van Azure PowerShell](/powershell/azure/overview) Azure PowerShell te installeren op uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="e9c58-114">If you haven't done so already, use the instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) to install Azure PowerShell on your local computer.</span></span> <span data-ttu-id="e9c58-115">Vervolgens opent u een Windows PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e9c58-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="e9c58-116">Stap 1: Uw account toevoegen</span><span class="sxs-lookup"><span data-stu-id="e9c58-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="e9c58-117">Typ het volgende achter de PowerShell-prompt **Add-AzureAccount** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="e9c58-117">At the PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="e9c58-118">Typ in het e-mailadres dat is gekoppeld aan uw Azure-abonnement en klikt u op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="e9c58-118">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="e9c58-119">Typ in het wachtwoord voor uw account.</span><span class="sxs-lookup"><span data-stu-id="e9c58-119">Type in the password for your account.</span></span>
4. <span data-ttu-id="e9c58-120">Klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="e9c58-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="e9c58-121">Stap 2: Uw abonnement en storage-account instellen</span><span class="sxs-lookup"><span data-stu-id="e9c58-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="e9c58-122">Uw Azure-abonnement en storage-account instellen door het uitvoeren van deze opdrachten bij de opdrachtprompt van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e9c58-122">Set your Azure subscription and storage account by running these commands at the Windows PowerShell command prompt.</span></span> <span data-ttu-id="e9c58-123">Vervang alles binnen de aanhalingstekens, met inbegrip van de < en > tekens lang zijn en de juiste namen.</span><span class="sxs-lookup"><span data-stu-id="e9c58-123">Replace everything within the quotes, including the < and > characters, with the correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="e9c58-124">U kunt de naam van het juiste abonnement ophalen uit de eigenschap SubscriptionName voor de uitvoer van de **Get-AzureSubscription** opdracht.</span><span class="sxs-lookup"><span data-stu-id="e9c58-124">You can get the correct subscription name from the SubscriptionName property of the output of the **Get-AzureSubscription** command.</span></span> <span data-ttu-id="e9c58-125">U kunt de juiste opslagaccountnaam ophalen van de eigenschap Label van de uitvoer van de **Get-AzureStorageAccount** opdracht, na het uitvoeren van de **Select-AzureSubscription** opdracht.</span><span class="sxs-lookup"><span data-stu-id="e9c58-125">You can get the correct storage account name from the Label property of the output of the **Get-AzureStorageAccount** command after you run the **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-the-virtual-machine-and-join-it-to-the-managed-domain"></a><span data-ttu-id="e9c58-126">Stap 3: Stapsgewijze - de virtuele machine in te richten en deze koppelen aan het beheerde domein</span><span class="sxs-lookup"><span data-stu-id="e9c58-126">Step 3: Step-by-step walkthrough - provision the virtual machine and join it to the managed domain</span></span>
<span data-ttu-id="e9c58-127">Hier volgt de bijbehorende Azure PowerShell-opdracht ingesteld op deze virtuele machine maken met lege regels tussen elk blok omwille van de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="e9c58-127">Here is the corresponding Azure PowerShell command set to create this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="e9c58-128">Geef informatie op over de Windows virtuele machine moeten worden ingericht.</span><span class="sxs-lookup"><span data-stu-id="e9c58-128">Specify information about the Windows virtual machine to be provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="e9c58-129">Zie voor de InstanceSize waarden voor D, DS of G-serie virtuele machines, [virtuele Machine en Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="e9c58-129">For the InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="e9c58-130">Bevatten informatie over het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="e9c58-130">Provide information about the managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="e9c58-131">Geef de naam van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="e9c58-131">Specify the name of the cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="e9c58-132">Geef de naam van het virtuele netwerk waarmee de virtuele machine moet worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="e9c58-132">Specify the name of the virtual network to which the VM should be joined.</span></span> <span data-ttu-id="e9c58-133">Zorg ervoor dat het beheerde domein van de AAD-DS beschikbaar in dit virtuele netwerk is.</span><span class="sxs-lookup"><span data-stu-id="e9c58-133">Ensure that the AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="e9c58-134">Selecteer het VM-afbeelding moet worden gebruikt voor het inrichten van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9c58-134">Select the VM image to be used to provision the VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="e9c58-135">Configureer de virtuele machine - naam van de VM, exemplaargrootte & afbeelding moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e9c58-135">Configure the VM - set VM name, instance size & image to be used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="e9c58-136">Lokale administrator-referenties ophalen voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9c58-136">Obtain local administrator credentials for the VM.</span></span> <span data-ttu-id="e9c58-137">Kies een sterke lokale administrator-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="e9c58-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

<span data-ttu-id="e9c58-138">Referenties voor een gebruikersaccount van ' AAD DC' beheerdersgroep VM koppelen aan het beheerde domein ophalen.</span><span class="sxs-lookup"><span data-stu-id="e9c58-138">Obtain credentials for a user account belonging to 'AAD DC Administrators' group to join VM to the managed domain.</span></span> <span data-ttu-id="e9c58-139">Geef de naam van het domein - bijvoorbeeld in ons voorbeeld, we "bob" opgeven als de gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="e9c58-139">Do not specify the domain name - for instance, in our example, we specify 'bob' as the user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type the name (DO NOT INCLUDE THE DOMAIN) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

<span data-ttu-id="e9c58-140">De virtuele machine configureren - domain join vereiste & vereiste referenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="e9c58-140">Configure the VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="e9c58-141">Stel een subnet voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9c58-141">Set a subnet for the VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="e9c58-142">Optioneel: Verwijzen naar het IP-adres van het domein.</span><span class="sxs-lookup"><span data-stu-id="e9c58-142">Optional: Point to the IP address of the domain.</span></span> <span data-ttu-id="e9c58-143">Als u de IP-adressen van het beheerde domein van Azure AD Domain Services moet de DNS-servers voor het virtuele netwerk hebt ingesteld, is deze stap niet vereist.</span><span class="sxs-lookup"><span data-stu-id="e9c58-143">If you set the IP addresses of the Azure AD Domain Services managed domain to be the DNS servers for the virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="e9c58-144">Nu de Windows-domein VM inrichten.</span><span class="sxs-lookup"><span data-stu-id="e9c58-144">Now, provision the domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-to-provision-a-windows-vm-and-automatically-join-it-to-an-aad-domain-services-managed-domain"></a><span data-ttu-id="e9c58-145">Script voor het inrichten van een virtuele machine van Windows en automatisch toevoegen aan een beheerd domein van AAD Domain Services</span><span class="sxs-lookup"><span data-stu-id="e9c58-145">Script to provision a Windows VM and automatically join it to an AAD Domain Services managed domain</span></span>
<span data-ttu-id="e9c58-146">Deze set PowerShell-opdracht maakt een virtuele machine voor een line-of-business-server die:</span><span class="sxs-lookup"><span data-stu-id="e9c58-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="e9c58-147">Maakt gebruik van de installatiekopie van het Windows Server 2012 R2 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="e9c58-147">Uses the Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="e9c58-148">Is een extra klein virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e9c58-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="e9c58-149">De naam van de Contoso100-test heeft.</span><span class="sxs-lookup"><span data-stu-id="e9c58-149">Has the name Contoso100-test.</span></span>
* <span data-ttu-id="e9c58-150">Automatisch wordt lid van een domein aan het beheerde domein contoso100.</span><span class="sxs-lookup"><span data-stu-id="e9c58-150">Is automatically domain joined to the contoso100 managed domain.</span></span>
* <span data-ttu-id="e9c58-151">Is toegevoegd aan de hetzelfde virtuele netwerk als het beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="e9c58-151">Is added to the same virtual network as the managed domain.</span></span>

<span data-ttu-id="e9c58-152">Hier wordt het volledige voorbeeld van een script voor het maken van de virtuele machine van Windows en automatisch toevoegen aan het beheerde domein van Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="e9c58-152">Here is the full sample script to create the Windows virtual machine and automatically join it to the Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type the name and password of the local administrator account."

    $domainadmincred=Get-Credential –Message "Now type the name (not including the domain) and password of an account in the AAD DC Administrators group, that has permission to add the machine to the domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="e9c58-153">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="e9c58-153">Related Content</span></span>
* [<span data-ttu-id="e9c58-154">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="e9c58-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="e9c58-155">Een beheerd domein van Azure AD Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="e9c58-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)

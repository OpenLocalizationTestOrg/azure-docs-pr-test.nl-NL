---
title: 'Azure Active Directory Domain Services: Beheerdershandleiding | Microsoft Docs'
description: Lid worden van een Windows virtuele machine tooa beheerde domein met behulp van Azure PowerShell en Hallo klassieke implementatiemodel.
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
ms.openlocfilehash: 21bc5930d84c5368a120f9d81f09320e2a0168fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain-using-powershell"></a><span data-ttu-id="79a84-103">Lid worden van een Windows Server virtuele machine tooa beheerde domein met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="79a84-103">Join a Windows Server virtual machine tooa managed domain using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="79a84-104">Klassieke Azure-portal - Windows</span><span class="sxs-lookup"><span data-stu-id="79a84-104">Azure classic portal - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
> * [<span data-ttu-id="79a84-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="79a84-105">PowerShell - Windows</span></span>](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

> [!IMPORTANT]
> <span data-ttu-id="79a84-106">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="79a84-106">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="79a84-107">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="79a84-107">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="79a84-108">Azure AD Domain Services biedt momenteel geen ondersteuning voor Hallo Resource Manager-model.</span><span class="sxs-lookup"><span data-stu-id="79a84-108">Azure AD Domain Services does not currently support hello Resource Manager model.</span></span>
>
>

<span data-ttu-id="79a84-109">Deze stappen ziet u hoe toocustomize een set van Azure PowerShell-opdrachten die maken en vooraf configureren van een op basis van Windows Azure virtuele machine met behulp van een benadering bouwsteen.</span><span class="sxs-lookup"><span data-stu-id="79a84-109">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="79a84-110">Deze stappen kunt u een op basis van Windows Azure virtuele machine maken en deelnemen aan het beheerde domein van tooan Azure AD Domain Services.</span><span class="sxs-lookup"><span data-stu-id="79a84-110">These steps help you build a Windows-based Azure virtual machine and join it tooan Azure AD Domain Services managed domain.</span></span>

<span data-ttu-id="79a84-111">Deze stappen volgt een benadering invullen-in-the-lege waarden voor het maken van Azure PowerShell-opdrachtsets.</span><span class="sxs-lookup"><span data-stu-id="79a84-111">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="79a84-112">Deze methode kan nuttig zijn als u nieuwe tooPowerShell of tooknow welke toospecify waarden voor geslaagde configuratie gewenste.</span><span class="sxs-lookup"><span data-stu-id="79a84-112">This approach can be useful if you are new tooPowerShell or you want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="79a84-113">Geavanceerde PowerShell-gebruikers kunnen ondernemen Hallo opdrachten en vervangen door hun eigen waarden voor Hallo variabelen (Hallo regels beginnen met '$').</span><span class="sxs-lookup"><span data-stu-id="79a84-113">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="79a84-114">Als u dit nog niet hebt gedaan, gebruikt u de instructies Hallo in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="79a84-114">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="79a84-115">Vervolgens opent u een Windows PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="79a84-115">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="79a84-116">Stap 1: Uw account toevoegen</span><span class="sxs-lookup"><span data-stu-id="79a84-116">Step 1: Add your account</span></span>
1. <span data-ttu-id="79a84-117">Typ achter de PowerShell-prompt Hallo **Add-AzureAccount** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="79a84-117">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span>
2. <span data-ttu-id="79a84-118">Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="79a84-118">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
3. <span data-ttu-id="79a84-119">Typ in het Hallo-wachtwoord voor je account.</span><span class="sxs-lookup"><span data-stu-id="79a84-119">Type in hello password for your account.</span></span>
4. <span data-ttu-id="79a84-120">Klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="79a84-120">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="79a84-121">Stap 2: Uw abonnement en storage-account instellen</span><span class="sxs-lookup"><span data-stu-id="79a84-121">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="79a84-122">Uw Azure-abonnement en storage-account instellen door deze opdrachten in Windows PowerShell-opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="79a84-122">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="79a84-123">Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste namen Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="79a84-123">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="79a84-124">Kunt u de naam van de juiste abonnement Hallo krijgen via Hallo SubscriptionName-eigenschap van Hallo Hallo **Get-AzureSubscription** opdracht.</span><span class="sxs-lookup"><span data-stu-id="79a84-124">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="79a84-125">Kunt u Hallo juist opslagaccountnaam krijgen via de eigenschap Label van de uitvoer Hallo HALLO hallo **Get-AzureStorageAccount** opdracht, na het uitvoeren van Hallo **Select-AzureSubscription** opdracht.</span><span class="sxs-lookup"><span data-stu-id="79a84-125">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-step-by-step-walkthrough---provision-hello-virtual-machine-and-join-it-toohello-managed-domain"></a><span data-ttu-id="79a84-126">Stap 3: Stapsgewijze - Hallo virtuele machine in te richten en deelnemen aan het beheerde domein toohello</span><span class="sxs-lookup"><span data-stu-id="79a84-126">Step 3: Step-by-step walkthrough - provision hello virtual machine and join it toohello managed domain</span></span>
<span data-ttu-id="79a84-127">Hier volgt Hallo bijbehorende Azure PowerShell-opdracht set toocreate van deze virtuele machine, met lege regels tussen elk blok omwille van de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="79a84-127">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

<span data-ttu-id="79a84-128">Geef informatie op over Hallo Windows virtuele machine toobe ingericht.</span><span class="sxs-lookup"><span data-stu-id="79a84-128">Specify information about hello Windows virtual machine toobe provisioned.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

<span data-ttu-id="79a84-129">Zie voor Hallo InstanceSize waarden voor D, DS of G-serie virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="79a84-129">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

<span data-ttu-id="79a84-130">Bevatten informatie over Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="79a84-130">Provide information about hello managed domain.</span></span>

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

<span data-ttu-id="79a84-131">Geef de naam Hallo van Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="79a84-131">Specify hello name of hello cloud service.</span></span>

    $svcname="Contoso100-test"

<span data-ttu-id="79a84-132">Geef de naam Hallo Hallo virtueel netwerk toowhich Hallo die VM moet worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="79a84-132">Specify hello name of hello virtual network toowhich hello VM should be joined.</span></span> <span data-ttu-id="79a84-133">Zorg ervoor dat Hallo beheerd AAD-DS-domein is beschikbaar in dit virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="79a84-133">Ensure that hello AAD-DS managed domain is available in this virtual network.</span></span>

    $vnetname="MyPreviewVnet"

<span data-ttu-id="79a84-134">Selecteer Hallo VM-installatiekopie gebruikt toobe tooprovision Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="79a84-134">Select hello VM image toobe used tooprovision hello VM.</span></span>

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="79a84-135">Configureer Hallo VM - naam van de VM, exemplaar grootte en de installatiekopie toobe gebruikt.</span><span class="sxs-lookup"><span data-stu-id="79a84-135">Configure hello VM - set VM name, instance size & image toobe used.</span></span>

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="79a84-136">Lokale administrator-referenties voor Hallo VM ophalen.</span><span class="sxs-lookup"><span data-stu-id="79a84-136">Obtain local administrator credentials for hello VM.</span></span> <span data-ttu-id="79a84-137">Kies een sterke lokale administrator-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="79a84-137">Choose a strong local administrator password.</span></span>

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

<span data-ttu-id="79a84-138">Referenties voor een gebruikersaccount die behoren too'AAD DC beheerders groep toojoin VM toohello beheerd domein ophalen.</span><span class="sxs-lookup"><span data-stu-id="79a84-138">Obtain credentials for a user account belonging too'AAD DC Administrators' group toojoin VM toohello managed domain.</span></span> <span data-ttu-id="79a84-139">Geef geen domeinnaam Hallo - voor het exemplaar in ons voorbeeld opgegeven "bob" als Hallo-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="79a84-139">Do not specify hello domain name - for instance, in our example, we specify 'bob' as hello user name.</span></span>

    $domainadmincred=Get-Credential –Message "Now type hello name (DO NOT INCLUDE hello DOMAIN) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

<span data-ttu-id="79a84-140">Configureer Hallo VM - domain join vereiste & vereiste referenties opgeven.</span><span class="sxs-lookup"><span data-stu-id="79a84-140">Configure hello VM - specify domain join requirement & required credentials.</span></span>

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="79a84-141">Een subnet voor VM Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="79a84-141">Set a subnet for hello VM.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

<span data-ttu-id="79a84-142">Optioneel: Punt toohello IP-adres van Hallo-domein.</span><span class="sxs-lookup"><span data-stu-id="79a84-142">Optional: Point toohello IP address of hello domain.</span></span> <span data-ttu-id="79a84-143">Als u op DNS-servers voor het virtuele netwerk Hallo Hallo IP-adressen van hello Azure AD Domain Services beheerd domein toobe Hallo instelt, is deze stap niet vereist.</span><span class="sxs-lookup"><span data-stu-id="79a84-143">If you set hello IP addresses of hello Azure AD Domain Services managed domain toobe hello DNS servers for hello virtual network, this step is not required.</span></span>

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

<span data-ttu-id="79a84-144">Nu domein inrichten Hallo virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="79a84-144">Now, provision hello domain-joined Windows VM.</span></span>

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="script-tooprovision-a-windows-vm-and-automatically-join-it-tooan-aad-domain-services-managed-domain"></a><span data-ttu-id="79a84-145">Script tooprovision een virtuele machine van Windows en automatisch deelnemen aan tooan AAD Domain Services beheerd domein</span><span class="sxs-lookup"><span data-stu-id="79a84-145">Script tooprovision a Windows VM and automatically join it tooan AAD Domain Services managed domain</span></span>
<span data-ttu-id="79a84-146">Deze set PowerShell-opdracht maakt een virtuele machine voor een line-of-business-server die:</span><span class="sxs-lookup"><span data-stu-id="79a84-146">This PowerShell command set creates a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="79a84-147">Hallo Windows Server 2012 R2 Datacenter installatiekopie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="79a84-147">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="79a84-148">Is een extra klein virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="79a84-148">Is an extra small virtual machine.</span></span>
* <span data-ttu-id="79a84-149">Hallo naam Contoso100-test heeft.</span><span class="sxs-lookup"><span data-stu-id="79a84-149">Has hello name Contoso100-test.</span></span>
* <span data-ttu-id="79a84-150">Wordt automatisch lid toohello contoso100 beheerde domein.</span><span class="sxs-lookup"><span data-stu-id="79a84-150">Is automatically domain joined toohello contoso100 managed domain.</span></span>
* <span data-ttu-id="79a84-151">Is toegevoegd toohello hetzelfde virtuele netwerk als Hallo beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="79a84-151">Is added toohello same virtual network as hello managed domain.</span></span>

<span data-ttu-id="79a84-152">Hier volgt virtuele machine met het volledige voorbeeld script toocreate Hallo Windows hello en automatisch deelnemen aan toohello Azure AD Domain Services beheerd domein.</span><span class="sxs-lookup"><span data-stu-id="79a84-152">Here is hello full sample script toocreate hello Windows virtual machine and automatically join it toohello Azure AD Domain Services managed domain.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $vmname="Contoso100-test"
    $vmsize="ExtraSmall"

    $domaindns="contoso100.com"
    $domacctdomain="contoso100"

    $svcname="Contoso100-test"
    $vnetname="MyPreviewVnet"

    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $localadmincred=Get-Credential –Message "Type hello name and password of hello local administrator account."

    $domainadmincred=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account in hello AAD DC Administrators group, that has permission tooadd hello machine toohello domain."

    $vm1 | Add-AzureProvisioningConfig -AdminUsername $localadmincred.Username -Password $localadmincred.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $domainadmincred.Username -DomainPassword $domainadmincred.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "Subnet-1"

    $dns = New-AzureDns -Name 'contoso100-dc1' -IPAddress '10.0.0.4'

    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname -Location "Central US" -DnsSettings $dns

<br>

## <a name="related-content"></a><span data-ttu-id="79a84-153">Gerelateerde inhoud</span><span class="sxs-lookup"><span data-stu-id="79a84-153">Related Content</span></span>
* [<span data-ttu-id="79a84-154">Azure AD Domain Services - handleiding aan de slag</span><span class="sxs-lookup"><span data-stu-id="79a84-154">Azure AD Domain Services - Getting Started guide</span></span>](active-directory-ds-getting-started.md)
* [<span data-ttu-id="79a84-155">Een beheerd domein van Azure AD Domain Services beheren</span><span class="sxs-lookup"><span data-stu-id="79a84-155">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)

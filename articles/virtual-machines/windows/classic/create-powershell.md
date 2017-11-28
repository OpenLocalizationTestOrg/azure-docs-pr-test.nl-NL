---
title: aaaCreate een Windows-VM met PowerShell | Microsoft Docs
description: Windows virtuele machines met behulp van Azure PowerShell en het klassieke implementatiemodel Hallo maken.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="fbc73-103">Een Windows-machine maken met PowerShell en Hallo klassieke implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="fbc73-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fbc73-104">Azure portal - Windows</span><span class="sxs-lookup"><span data-stu-id="fbc73-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="fbc73-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="fbc73-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="fbc73-106">Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fbc73-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fbc73-107">In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="fbc73-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fbc73-108">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fbc73-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fbc73-109">Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbc73-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="fbc73-110">Deze stappen ziet u hoe toocustomize een set van Azure PowerShell-opdrachten die maken en vooraf configureren van een op basis van Windows Azure virtuele machine met behulp van een benadering bouwsteen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="fbc73-111">U kunt dit proces tooquickly een opdrachtset voor een nieuwe Windows gebaseerde virtuele machine maken en uitbreiden van een bestaande implementatie of toocreate meerdere opdracht stelt u die snel bouwen van een aangepaste ontwikkelen en testen of de IT pro-omgeving.</span><span class="sxs-lookup"><span data-stu-id="fbc73-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="fbc73-112">Deze stappen volgt een benadering invullen-in-the-lege waarden voor het maken van Azure PowerShell-opdrachtsets.</span><span class="sxs-lookup"><span data-stu-id="fbc73-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="fbc73-113">Deze methode kan nuttig zijn als u nieuwe tooPowerShell of u alleen tooknow welke toospecify waarden voor geslaagde configuratie wilt.</span><span class="sxs-lookup"><span data-stu-id="fbc73-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="fbc73-114">Geavanceerde PowerShell-gebruikers kunnen ondernemen Hallo opdrachten en vervangen door hun eigen waarden voor Hallo variabelen (Hallo regels beginnen met '$').</span><span class="sxs-lookup"><span data-stu-id="fbc73-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="fbc73-115">Als u dit nog niet hebt gedaan, gebruikt u de instructies Hallo in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="fbc73-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="fbc73-116">Vervolgens opent u een Windows PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="fbc73-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="fbc73-117">Stap 1: Uw account toevoegen</span><span class="sxs-lookup"><span data-stu-id="fbc73-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="fbc73-118">Typ achter de PowerShell-prompt Hallo **Add-AzureAccount** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="fbc73-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="fbc73-119">Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="fbc73-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="fbc73-120">Typ in het Hallo-wachtwoord voor je account.</span><span class="sxs-lookup"><span data-stu-id="fbc73-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="fbc73-121">Klik op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="fbc73-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="fbc73-122">Stap 2: Uw abonnement en storage-account instellen</span><span class="sxs-lookup"><span data-stu-id="fbc73-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="fbc73-123">Uw Azure-abonnement en storage-account instellen door deze opdrachten in Windows PowerShell-opdrachtprompt Hallo.</span><span class="sxs-lookup"><span data-stu-id="fbc73-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="fbc73-124">Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste namen Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="fbc73-125">Kunt u de naam van de juiste abonnement Hallo krijgen via Hallo SubscriptionName-eigenschap van Hallo Hallo **Get-AzureSubscription** opdracht.</span><span class="sxs-lookup"><span data-stu-id="fbc73-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="fbc73-126">Kunt u Hallo juist opslagaccountnaam krijgen via de eigenschap Label van de uitvoer Hallo HALLO hallo **Get-AzureStorageAccount** opdracht, na het uitvoeren van Hallo **Select-AzureSubscription** opdracht.</span><span class="sxs-lookup"><span data-stu-id="fbc73-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="fbc73-127">Stap 3: Hallo ImageFamily bepalen</span><span class="sxs-lookup"><span data-stu-id="fbc73-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="fbc73-128">Vervolgens moet u toodetermine hello ImageFamily of labelwaarde voor Hallo specifieke installatiekopie bijbehorende toohello gewenste toocreate virtuele Azure-machine.</span><span class="sxs-lookup"><span data-stu-id="fbc73-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="fbc73-129">U kunt Hallo lijst met beschikbare ImageFamily waarden met deze opdracht ophalen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="fbc73-130">Hier volgen enkele voorbeelden van waarden ImageFamily voor Windows-computers:</span><span class="sxs-lookup"><span data-stu-id="fbc73-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="fbc73-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="fbc73-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="fbc73-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="fbc73-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="fbc73-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="fbc73-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="fbc73-134">SQL Server 2012 SP1 Enterprise in WindowsServer 2012</span><span class="sxs-lookup"><span data-stu-id="fbc73-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="fbc73-135">Als u Hallo-installatiekopie die u zoekt vinden, opent u een nieuw exemplaar van Hallo teksteditor van uw keuze of Hallo PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="fbc73-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="fbc73-136">Hallo volgende kopiëren naar nieuw tekstbestand Hallo of Hallo PowerShell ISE, Hallo ImageFamily waarde te vervangen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="fbc73-137">In sommige gevallen is Hallo installatiekopie met de naam in Hallo labeleigenschap in plaats van Hallo ImageFamily waarde.</span><span class="sxs-lookup"><span data-stu-id="fbc73-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="fbc73-138">Als u Hallo-installatiekopie die u zoekt met Hallo ImageFamily eigenschap niet vinden, lijst Hallo afbeeldingen door de eigenschap Label met deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="fbc73-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="fbc73-139">Als u de juiste installatiekopie Hallo met deze opdracht vinden, opent u een nieuw exemplaar van Hallo teksteditor van uw keuze of Hallo PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="fbc73-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="fbc73-140">Hallo volgende naar nieuw tekstbestand Hallo of PowerShell ISE, vervangen door de labelwaarde Hallo Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="fbc73-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="fbc73-141">Stap 4: De opdrachtset bouwen</span><span class="sxs-lookup"><span data-stu-id="fbc73-141">Step 4: Build your command set</span></span>
<span data-ttu-id="fbc73-142">Bouw Hallo rest van de opdracht die is ingesteld door de juiste reeks blokken hieronder Hallo kopiëren naar uw nieuw tekstbestand of Hallo ISE invullen van de waarden van variabelen Hallo en Hallo < en > tekens verwijderen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="fbc73-143">Zie Hallo twee [voorbeelden](#examples) aan Hallo einde van dit artikel voor een idee van Hallo eindresultaat.</span><span class="sxs-lookup"><span data-stu-id="fbc73-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="fbc73-144">Start de opdracht die is ingesteld door een van deze twee opdracht blokken (vereist) te kiezen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="fbc73-145">Optie 1: Geef de naam van een virtuele machine en een grootte.</span><span class="sxs-lookup"><span data-stu-id="fbc73-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="fbc73-146">Optie 2: Geef een naam, de grootte en de naam van de beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="fbc73-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="fbc73-147">Zie voor Hallo InstanceSize waarden voor D, DS of G-serie virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbc73-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="fbc73-148">Als u een Enterprise Agreement met Software Assurance hebt en tootake profiteren van Windows Server Hallo van plan bent [hybride gebruik voordeel](https://azure.microsoft.com/pricing/hybrid-use-benefit/), voeg de **- LicenseType** parameter toohello  **Nieuwe AzureVMConfig** cmdlet Hallo-waarde doorgegeven **Windows_Server** voor typische Hallo gebruiksvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="fbc73-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="fbc73-149">Zorg ervoor dat u gebruikmaakt van een installatiekopie die u hebt geüpload; u kunt een standaardinstallatiekopie van Hallo galerie niet gebruiken met Hallo hybride gebruiken voordeel.</span><span class="sxs-lookup"><span data-stu-id="fbc73-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="fbc73-150">Geef desgewenst voor een zelfstandige Windows-computer Hallo lokale administrator-account en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="fbc73-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="fbc73-151">Kies een sterk wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="fbc73-151">Choose a strong password.</span></span> <span data-ttu-id="fbc73-152">toocheck de sterkte Zie [wachtwoord Checker: met behulp van sterke wachtwoorden](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbc73-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="fbc73-153">Eventueel tooadd Hallo Windows computer tooan bestaande Active Directory-domein Hallo lokale administrator-account en wachtwoord, hello domein, en Hallo naam en het wachtwoord van een domeinaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="fbc73-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="fbc73-154">Zie voor aanvullende vooraf configuratieopties voor virtuele machines op basis van Windows hello syntaxis voor Hallo **Windows** en **WindowsDomain** parametersets [ Voeg AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span><span class="sxs-lookup"><span data-stu-id="fbc73-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="fbc73-155">Desgewenst toewijzen Hallo virtuele machine, een specifiek IP-adres, een statische DIP genoemd.</span><span class="sxs-lookup"><span data-stu-id="fbc73-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="fbc73-156">U kunt controleren of een specifiek IP-adres beschikbaar met:</span><span class="sxs-lookup"><span data-stu-id="fbc73-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="fbc73-157">Desgewenst toewijzen Hallo virtuele machine tooa specifieke subnet in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="fbc73-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="fbc73-158">Voegt u desgewenst een virtuele machine van één schijf toohello.</span><span class="sxs-lookup"><span data-stu-id="fbc73-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="fbc73-159">Voor een Active Directory-domeincontroller te $hcaching ingesteld 'None'.</span><span class="sxs-lookup"><span data-stu-id="fbc73-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="fbc73-160">Voegt u desgewenst Hallo virtuele machine tooan bestaande taakverdeling set voor het externe verkeer.</span><span class="sxs-lookup"><span data-stu-id="fbc73-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="fbc73-161">Ten slotte, kies een van deze blokken vereist opdracht voor het maken van Hallo virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fbc73-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="fbc73-162">Optie 1: Maak Hallo virtuele machine in een bestaande cloudservice.</span><span class="sxs-lookup"><span data-stu-id="fbc73-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="fbc73-163">korte naam van de cloudservice Hallo Hallo is Hallo-naam die wordt weergegeven in de lijst van de Hallo van Cloud Services in hello Azure-portal of in Hallo lijst met resourcegroepen in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fbc73-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="fbc73-164">Optie 2: Maak Hallo virtuele machine in een bestaande cloudservice en het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="fbc73-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="fbc73-165">Stap 5: Voer de opdrachtset</span><span class="sxs-lookup"><span data-stu-id="fbc73-165">Step 5: Run your command set</span></span>
<span data-ttu-id="fbc73-166">Bekijk hello Azure PowerShell-opdrachtset die u gebouwd in een teksteditor of Hallo PowerShell ISE die bestaan uit meerdere blokken van opdrachten uit stap 4.</span><span class="sxs-lookup"><span data-stu-id="fbc73-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="fbc73-167">Zorg ervoor dat u alle variabelen van Hallo nodig hebt opgegeven en of ze de juiste waarden Hallo hebben.</span><span class="sxs-lookup"><span data-stu-id="fbc73-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="fbc73-168">Controleer ook of u alle Hallo < en > tekens hebt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fbc73-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="fbc73-169">Als u gebruikmaakt van een teksteditor, wordt Hallo-opdracht kopiëren toohello Klembord instellen en vervolgens met de rechtermuisknop op uw Windows PowerShell-opdrachtprompt openen.</span><span class="sxs-lookup"><span data-stu-id="fbc73-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="fbc73-170">Hiermee Hallo opdrachtset als een reeks PowerShell-opdrachten uitgeven en maakt u uw virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="fbc73-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="fbc73-171">U kunt ook Hallo-opdracht ingesteld in PowerShell ISE Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fbc73-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="fbc73-172">Als u deze virtuele machine opnieuw of een vergelijkbare maakt, kunt u:</span><span class="sxs-lookup"><span data-stu-id="fbc73-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="fbc73-173">Sla deze opdracht ingesteld als het bestand in een PowerShell-script (*.ps1).</span><span class="sxs-lookup"><span data-stu-id="fbc73-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="fbc73-174">Opslaan van deze opdracht ingesteld als een Azure Automation-runbook in Hallo **Automation-Accounts** sectie Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fbc73-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="fbc73-175"><a id="examples"></a>Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="fbc73-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="fbc73-176">Hier vindt u twee voorbeelden van het gebruik van Hallo stappen hierboven toobuild Azure PowerShell-opdrachtsets die op basis van Windows Azure virtuele machines maken.</span><span class="sxs-lookup"><span data-stu-id="fbc73-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="fbc73-177">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="fbc73-177">Example 1</span></span>
<span data-ttu-id="fbc73-178">Ik moet een PowerShell opdracht ingesteld toocreate Hallo eerste virtuele machine voor een Active Directory-domeincontroller:</span><span class="sxs-lookup"><span data-stu-id="fbc73-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="fbc73-179">Hallo Windows Server 2012 R2 Datacenter installatiekopie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fbc73-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="fbc73-180">Hallo naam AZDC1 heeft.</span><span class="sxs-lookup"><span data-stu-id="fbc73-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="fbc73-181">Een zelfstandige computer is.</span><span class="sxs-lookup"><span data-stu-id="fbc73-181">Is a standalone computer.</span></span>
* <span data-ttu-id="fbc73-182">Heeft een schijf aanvullende gegevens van 20 GB.</span><span class="sxs-lookup"><span data-stu-id="fbc73-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="fbc73-183">Hallo statisch IP-adres 192.168.244.4 heeft.</span><span class="sxs-lookup"><span data-stu-id="fbc73-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="fbc73-184">Staat in subnet van de Hallo back-end van Hallo AZDatacenter virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="fbc73-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="fbc73-185">In de cloudservice hello Azure TailspinToys is.</span><span class="sxs-lookup"><span data-stu-id="fbc73-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="fbc73-186">Hier volgt Hallo bijbehorende Azure PowerShell-opdracht set toocreate van deze virtuele machine, met lege regels tussen elk blok omwille van de leesbaarheid.</span><span class="sxs-lookup"><span data-stu-id="fbc73-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="fbc73-187">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="fbc73-187">Example 2</span></span>
<span data-ttu-id="fbc73-188">Ik moet een PowerShell opdracht ingesteld toocreate een virtuele machine voor een line-of-business-server die:</span><span class="sxs-lookup"><span data-stu-id="fbc73-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="fbc73-189">Hallo Windows Server 2012 R2 Datacenter installatiekopie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fbc73-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="fbc73-190">Hallo naam LOB1 heeft.</span><span class="sxs-lookup"><span data-stu-id="fbc73-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="fbc73-191">Is een lid van domein van Hallo corp.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="fbc73-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="fbc73-192">Heeft een schijf aanvullende gegevens van 200 GB.</span><span class="sxs-lookup"><span data-stu-id="fbc73-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="fbc73-193">Hallo FrontEnd subnet Hallo AZDatacenter virtueel netwerk heeft.</span><span class="sxs-lookup"><span data-stu-id="fbc73-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="fbc73-194">In de cloudservice hello Azure TailspinToys is.</span><span class="sxs-lookup"><span data-stu-id="fbc73-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="fbc73-195">Hier volgt Hallo bijbehorende Azure PowerShell-opdracht set toocreate van deze virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="fbc73-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="fbc73-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="fbc73-196">Next steps</span></span>
<span data-ttu-id="fbc73-197">Als u een besturingssysteemschijf die groter is dan 127 GB nodig hebt, kunt u [expand Hallo OS station](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbc73-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


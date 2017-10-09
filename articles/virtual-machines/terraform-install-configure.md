---
title: aaaInstall en Terraform tooprovision VM's en andere infrastructuur configureren in Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall en configureer Terraform toocreate Azure resources
services: virtual-machines-linux
documentationcenter: virtual-machines
author: echuvyrov
manager: jtalkar
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: echuvyrov
ms.openlocfilehash: 803f51a6f5357417b96264ba713791408f9935b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-terraform-tooprovision-vms-and-other-infrastructure-into-azure"></a><span data-ttu-id="ec4de-103">Installeer en configureer Terraform tooprovision VM's en andere infrastructuur in Azure</span><span class="sxs-lookup"><span data-stu-id="ec4de-103">Install and configure Terraform tooprovision VMs and other infrastructure into Azure</span></span> 
<span data-ttu-id="ec4de-104">Dit artikel beschrijft Hallo nodige tooinstall en Terraform tooprovision resources, zoals virtuele machines in Azure te configureren.</span><span class="sxs-lookup"><span data-stu-id="ec4de-104">This article describes hello necessary steps tooinstall and configure Terraform tooprovision resources such as virtual machines into Azure.</span></span> <span data-ttu-id="ec4de-105">U leert hoe toocreate en het gebruik van Azure-referenties tooenable Terraform tooprovision cloud-bronnen op een veilige manier.</span><span class="sxs-lookup"><span data-stu-id="ec4de-105">You will learn how toocreate and use Azure credentials tooenable Terraform tooprovision cloud resources in a secure manner.</span></span>

<span data-ttu-id="ec4de-106">HashiCorp Terraform biedt een eenvoudige manier toodefine en cloudinfrastructuur implementeren met behulp van een aangepaste templating taal HashiCorp configuratie taal (lijst met compatibele hardware) genoemd.</span><span class="sxs-lookup"><span data-stu-id="ec4de-106">HashiCorp Terraform provides an easy way toodefine and deploy cloud infrastructure by using a custom templating language called HashiCorp configuration language (HCL).</span></span> <span data-ttu-id="ec4de-107">Deze aangepaste taal is [eenvoudig toowrite en eenvoudig toounderstand](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ec4de-107">This custom language is [easy toowrite and easy toounderstand](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="ec4de-108">Bovendien via Hallo `terraform plan` uitvoert, en u kunt Hallo wijzigingen tooyour infrastructuur visualiseren voordat u ze vastlegt.</span><span class="sxs-lookup"><span data-stu-id="ec4de-108">Additionally, by using hello `terraform plan` command, you can visualize hello changes tooyour infrastructure before you commit them.</span></span> <span data-ttu-id="ec4de-109">Volg deze stappen toostart Terraform gebruiken met Azure.</span><span class="sxs-lookup"><span data-stu-id="ec4de-109">Follow these steps toostart using Terraform with Azure.</span></span>

## <a name="install-terraform"></a><span data-ttu-id="ec4de-110">Terraform installeren</span><span class="sxs-lookup"><span data-stu-id="ec4de-110">Install Terraform</span></span>
<span data-ttu-id="ec4de-111">tooinstall Terraform, [downloaden](https://www.terraform.io/downloads.html) Hallo pakket geschikt is voor uw besturingssysteem in een afzonderlijke installatiemap.</span><span class="sxs-lookup"><span data-stu-id="ec4de-111">tooinstall Terraform, [download](https://www.terraform.io/downloads.html) hello package appropriate for your operating system into a separate install directory.</span></span> <span data-ttu-id="ec4de-112">Hallo download bevat één uitvoerbaar bestand, waarvoor moet u ook een globale pad definiëren.</span><span class="sxs-lookup"><span data-stu-id="ec4de-112">hello download contains a single executable file, for which you should also define a global path.</span></span> <span data-ttu-id="ec4de-113">Voor instructies over hoe tooset Hallo pad op Linux- en Mac, gaat u te[deze webpagina](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span><span class="sxs-lookup"><span data-stu-id="ec4de-113">For instructions on how tooset hello path on Linux and Mac, go too[this webpage](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux).</span></span> <span data-ttu-id="ec4de-114">Voor instructies over hoe tooset pad op Windows hello te gaat[deze webpagina](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span><span class="sxs-lookup"><span data-stu-id="ec4de-114">For instructions on how tooset hello path on Windows, go too[this webpage](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows).</span></span> <span data-ttu-id="ec4de-115">tooverify uw installatie uitvoeren Hallo `terraform` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ec4de-115">tooverify your installation, run hello `terraform` command.</span></span> <span data-ttu-id="ec4de-116">U ziet een lijst met beschikbare Terraform opties als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ec4de-116">You should see a list of available Terraform options as output.</span></span>

<span data-ttu-id="ec4de-117">Vervolgens moet u tooallow Terraform toegang tooyour Azure-abonnement tooperform infrastructuur inrichten.</span><span class="sxs-lookup"><span data-stu-id="ec4de-117">Next, you need tooallow Terraform access tooyour Azure subscription tooperform infrastructure provisioning.</span></span>

## <a name="set-up-terraform-access-tooazure"></a><span data-ttu-id="ec4de-118">Terraform toegang tooAzure instellen</span><span class="sxs-lookup"><span data-stu-id="ec4de-118">Set up Terraform access tooAzure</span></span>
<span data-ttu-id="ec4de-119">tooenable Terraform tooprovision resources in Azure, moet u twee entiteiten toocreate in Azure Active Directory (Azure AD): een Azure AD-toepassing en een Azure AD-service-principal.</span><span class="sxs-lookup"><span data-stu-id="ec4de-119">tooenable Terraform tooprovision resources into Azure, you need toocreate two entities in Azure Active Directory (Azure AD): an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="ec4de-120">Vervolgens gebruikt u deze entiteiten id's in uw Terraform-scripts.</span><span class="sxs-lookup"><span data-stu-id="ec4de-120">Then, you use these entities' identifiers in your Terraform scripts.</span></span> <span data-ttu-id="ec4de-121">Een service-principal is een lokaal exemplaar van een globale Azure AD-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ec4de-121">A service principal is a local instance of a global Azure AD application.</span></span> <span data-ttu-id="ec4de-122">Een service-principal kunt gedetailleerde lokale toegang tooglobal controlemiddelen.</span><span class="sxs-lookup"><span data-stu-id="ec4de-122">A service principal allows granular local access control tooglobal resources.</span></span>

<span data-ttu-id="ec4de-123">Er zijn verschillende manieren toocreate een Azure AD-toepassing en een Azure AD-service-principal.</span><span class="sxs-lookup"><span data-stu-id="ec4de-123">There are several ways toocreate an Azure AD application and an Azure AD service principal.</span></span> <span data-ttu-id="ec4de-124">Hallo snelst en eenvoudigst is manier vandaag de dag toouse Azure CLI 2.0, die [u kunt downloaden en installeren op Windows, Linux of een Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec4de-124">hello easiest and fastest way today is toouse Azure CLI 2.0, which [you can download and install on Windows, Linux, or a Mac](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="ec4de-125">U kunt ook PowerShell of Azure CLI 1.0 toocreate Hallo nodig beveiligingsinfrastructuur gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec4de-125">You also can use PowerShell or Azure CLI 1.0 toocreate hello necessary security infrastructure.</span></span> <span data-ttu-id="ec4de-126">Hallo instructies hoe u tooconfigure Terraform voor Azure met behulp van alle van deze methoden.</span><span class="sxs-lookup"><span data-stu-id="ec4de-126">hello instructions that follow show you how tooconfigure Terraform for Azure by using all of these approaches.</span></span>

### <a name="use-azure-cli-20-for-windows-linux-or-mac-users"></a><span data-ttu-id="ec4de-127">Azure CLI 2.0 gebruiken (voor Windows, Linux of Mac-gebruikers)</span><span class="sxs-lookup"><span data-stu-id="ec4de-127">Use Azure CLI 2.0 (for Windows, Linux, or Mac users)</span></span> 
<span data-ttu-id="ec4de-128">Nadat u downloadt en Hallo installeert [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), tooadminister aanmelden met uw Azure-abonnement door uitgifte van Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ec4de-128">After you download and install hello [Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli), sign in tooadminister your Azure subscription by issuing hello following command:</span></span>

```
az login
```

>[!NOTE]
><span data-ttu-id="ec4de-129">Als u Hallo China, Duitse Azure of Azure Government clouds gebruikt, moet u toofirst hello Azure CLI toowork configureren met die cloud.</span><span class="sxs-lookup"><span data-stu-id="ec4de-129">If you use hello China, Azure Germany, or Azure Government clouds, you need toofirst configure hello Azure CLI toowork with that cloud.</span></span> <span data-ttu-id="ec4de-130">U kunt dit doen door het uitvoeren van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="ec4de-130">You can do this by running hello following:</span></span>

```
az cloud set --name AzureChinaCloud|AzureGermanCloud|AzureUSGovernment
```

<span data-ttu-id="ec4de-131">Als u meerdere Azure-abonnementen hebt, de bijbehorende gegevens worden geretourneerd door Hallo `az login` opdracht.</span><span class="sxs-lookup"><span data-stu-id="ec4de-131">If you have multiple Azure subscriptions, their details are returned by hello `az login` command.</span></span> <span data-ttu-id="ec4de-132">Set Hallo `SUBSCRIPTION_ID` omgeving variabele toohold Hallo waarde Hallo geretourneerd `id` veld Hallo abonnement u wilt dat toouse.</span><span class="sxs-lookup"><span data-stu-id="ec4de-132">Set hello `SUBSCRIPTION_ID` environment variable toohold hello value of hello returned `id` field from hello subscription you want toouse.</span></span> 

<span data-ttu-id="ec4de-133">Hallo-abonnement dat u toouse voor deze sessie wilt instellen.</span><span class="sxs-lookup"><span data-stu-id="ec4de-133">Set hello subscription that you want toouse for this session.</span></span>

```
az account set --subscription="${SUBSCRIPTION_ID}"
```

<span data-ttu-id="ec4de-134">Hallo account tooget Hallo abonnements-ID opvragen en tenant-id-waarden.</span><span class="sxs-lookup"><span data-stu-id="ec4de-134">Query hello account tooget hello subscription ID and tenant ID values.</span></span>

```
az account show --query "{subscriptionId:id, tenantId:tenantId}"
```

<span data-ttu-id="ec4de-135">Vervolgens maakt u afzonderlijke referenties voor Terraform.</span><span class="sxs-lookup"><span data-stu-id="ec4de-135">Next, create separate credentials for Terraform.</span></span>

```
az ad sp create-for-rbac --role="Contributor" --scopes="/subscriptions/${SUBSCRIPTION_ID}"
```

<span data-ttu-id="ec4de-136">De appId, wachtwoord, sp_name en tenant worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="ec4de-136">Your appId, password, sp_name, and tenant are returned.</span></span> <span data-ttu-id="ec4de-137">Maak een notitie van Hallo appId en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ec4de-137">Make a note of hello appId and password.</span></span>

<span data-ttu-id="ec4de-138">tooconfirm uw referenties (service-principal), opent u een nieuwe shell en Voer Hallo opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="ec4de-138">tooconfirm your credentials (service principal), open a new shell and run hello following commands.</span></span> <span data-ttu-id="ec4de-139">Vervang Hallo waarden voor sp_name, wachtwoord en tenant geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="ec4de-139">Substitute hello returned values for sp_name, password, and tenant:</span></span>

```
az login --service-principal -u SP_NAME -p PASSWORD --tenant TENANT
az vm list-sizes --location westus
```

### <a name="use-powershell-for-windows-users"></a><span data-ttu-id="ec4de-140">Gebruik PowerShell (voor Windows-gebruikers)</span><span class="sxs-lookup"><span data-stu-id="ec4de-140">Use PowerShell (for Windows users)</span></span> 
<span data-ttu-id="ec4de-141">toouse een Windows toowrite machine en voer uw Terraform scripts en toouse PowerShell voor configuratietaken uw machine met de juiste PowerShell hulpmiddelen Hallo configureren.</span><span class="sxs-lookup"><span data-stu-id="ec4de-141">toouse a Windows machine toowrite and execute your Terraform scripts and toouse PowerShell for configuration tasks, configure your machine with hello right PowerShell tools.</span></span> 

1. <span data-ttu-id="ec4de-142">Hulpprogramma's voor PowerShell installeren door de stappen te volgen Hallo in [installeren en configureren van Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="ec4de-142">Install PowerShell tools by following hello steps in [Install and configure Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/install-azurerm-ps).</span></span> 

2. <span data-ttu-id="ec4de-143">Downloaden en uitvoeren van Hallo [azure setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) vanaf Hallo PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="ec4de-143">Download and execute hello [azure-setup.ps1 script](https://github.com/echuvyrov/terraform101/blob/master/azureSetup.ps1) from hello PowerShell console.</span></span>

3. <span data-ttu-id="ec4de-144">toorun hello azure setup.ps1 script downloaden en uitvoeren van Hallo `./azure-setup.ps1 setup` opdracht Hallo PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="ec4de-144">toorun hello azure-setup.ps1 script, download it and execute hello `./azure-setup.ps1 setup` command from hello PowerShell console.</span></span> <span data-ttu-id="ec4de-145">Meld u vervolgens aan tooyour Azure-abonnement met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="ec4de-145">Then sign in tooyour Azure subscription with administrative privileges.</span></span>

4. <span data-ttu-id="ec4de-146">Geef de toepassingsnaam van een (willekeurige tekenreeks, vereist) als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ec4de-146">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="ec4de-147">Geef eventueel een sterk wachtwoord wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ec4de-147">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="ec4de-148">Als u een wachtwoord niet opgeeft, wordt een sterk wachtwoord voor u gegenereerd met behulp van .NET-bibliotheken voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="ec4de-148">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

### <a name="use-azure-cli-10-for-linux-or-mac-users"></a><span data-ttu-id="ec4de-149">Gebruik van Azure CLI 1.0 (voor Linux- of Mac-gebruikers)</span><span class="sxs-lookup"><span data-stu-id="ec4de-149">Use Azure CLI 1.0 (for Linux or Mac users)</span></span>
<span data-ttu-id="ec4de-150">tooget is gestart met Terraform op Linux-machines of Macs met Azure CLI 1.0 installeren Hallo juiste bibliotheken op uw computer.</span><span class="sxs-lookup"><span data-stu-id="ec4de-150">tooget started with Terraform on Linux machines or Macs with Azure CLI 1.0, install hello proper libraries on your machine.</span></span>  

1. <span data-ttu-id="ec4de-151">Azure xPlat CLI-hulpprogramma's installeren door de stappen te volgen Hallo in [2.0 voor Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ec4de-151">Install Azure xPlat CLI tools by following hello steps in [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> 

2. <span data-ttu-id="ec4de-152">Download en installeer een JSON-processor door Hallo-instructies in [jq downloaden](https://stedolan.github.io/jq/download/).</span><span class="sxs-lookup"><span data-stu-id="ec4de-152">Download and install a JSON processor by following hello instructions in [Download jq](https://stedolan.github.io/jq/download/).</span></span>

3. <span data-ttu-id="ec4de-153">Downloaden en uitvoeren van Hallo [azure setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script vanaf Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="ec4de-153">Download and execute hello [azure-setup.sh script](https://github.com/mitchellh/packer/blob/master/contrib/azure-setup.sh) bash script from hello console.</span></span>

4. <span data-ttu-id="ec4de-154">toorun hello azure setup.sh script downloaden en uitvoeren van Hallo `./azure-setup setup` opdracht vanuit Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="ec4de-154">toorun hello azure-setup.sh script, download it and execute hello `./azure-setup setup` command from hello console.</span></span> <span data-ttu-id="ec4de-155">Meld u vervolgens aan tooyour Azure-abonnement met beheerdersbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="ec4de-155">Then sign in tooyour Azure subscription with administrative privileges.</span></span>
 
5. <span data-ttu-id="ec4de-156">Geef de toepassingsnaam van een (willekeurige tekenreeks, vereist) als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ec4de-156">Provide an application name (arbitrary string, required) when prompted.</span></span> <span data-ttu-id="ec4de-157">Geef eventueel een sterk wachtwoord wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ec4de-157">Optionally, supply a strong password when prompted.</span></span> <span data-ttu-id="ec4de-158">Als u een wachtwoord niet opgeeft, wordt een sterk wachtwoord voor u gegenereerd met behulp van .NET-bibliotheken voor beveiliging.</span><span class="sxs-lookup"><span data-stu-id="ec4de-158">If you don't provide a password, a strong password is generated for you by using .NET security libraries.</span></span>

<span data-ttu-id="ec4de-159">Alle eerdere Hallo-scripts maken een Azure AD-toepassing en service principal.</span><span class="sxs-lookup"><span data-stu-id="ec4de-159">All hello previous scripts create an Azure AD application and service principal.</span></span> <span data-ttu-id="ec4de-160">Hallo service-principal haalt een bijdrager of het niveau van de eigenaar toegang op Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ec4de-160">hello service principal gets a contributor or owner-level access on hello subscription.</span></span> <span data-ttu-id="ec4de-161">Vanwege Hallo hoog niveau van toegang verleend, moet u altijd Hallo beveiligingsgegevens die worden gegenereerd door deze scripts te beschermen.</span><span class="sxs-lookup"><span data-stu-id="ec4de-161">Because of hello high level of access granted, you should always protect hello security information generated by those scripts.</span></span> <span data-ttu-id="ec4de-162">Maak een notitie van vier stukjes beveiligingsinformatie van deze scripts: appId, wachtwoord, subscription_id en tenant_id.</span><span class="sxs-lookup"><span data-stu-id="ec4de-162">Make a note of all four pieces of security information provided by those scripts: appId, password, subscription_id, and tenant_id.</span></span>

## <a name="set-environment-variables"></a><span data-ttu-id="ec4de-163">De omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="ec4de-163">Set environment variables</span></span>
<span data-ttu-id="ec4de-164">Nadat u maken en configureren van een service-principal voor Azure AD, moet u toolet Terraform weten Hallo tenant-ID, abonnements-ID, client-ID en de geheime toouse client.</span><span class="sxs-lookup"><span data-stu-id="ec4de-164">After you create and configure an Azure AD service principal, you need toolet Terraform know hello tenant ID, subscription ID, client ID, and client secret toouse.</span></span> <span data-ttu-id="ec4de-165">U kunt dit doen door deze waarden insluiten in uw Terraform scripts, zoals beschreven in [de basisinfrastructuur maken met behulp van Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ec4de-165">You can do it by embedding those values in your Terraform scripts, as described in [Create basic infrastructure by using Terraform](terraform-create-complete-vm.md).</span></span> <span data-ttu-id="ec4de-166">Ook stelt u na omgevingsvariabelen hello (en dus niet per ongeluk controleren of delen van uw referenties):</span><span class="sxs-lookup"><span data-stu-id="ec4de-166">Alternately, you can set hello following environment variables (and thus avoid accidentally checking in or sharing your credentials):</span></span>

- <span data-ttu-id="ec4de-167">ARM_SUBSCRIPTION_ID</span><span class="sxs-lookup"><span data-stu-id="ec4de-167">ARM_SUBSCRIPTION_ID</span></span>
- <span data-ttu-id="ec4de-168">ARM_CLIENT_ID</span><span class="sxs-lookup"><span data-stu-id="ec4de-168">ARM_CLIENT_ID</span></span>
- <span data-ttu-id="ec4de-169">ARM_CLIENT_SECRET</span><span class="sxs-lookup"><span data-stu-id="ec4de-169">ARM_CLIENT_SECRET</span></span>
- <span data-ttu-id="ec4de-170">ARM_TENANT_ID</span><span class="sxs-lookup"><span data-stu-id="ec4de-170">ARM_TENANT_ID</span></span>

<span data-ttu-id="ec4de-171">U kunt dit voorbeeld shell-script tooset die variabelen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec4de-171">You can use this sample shell script tooset those variables:</span></span>

```
#!/bin/sh
echo "Setting environment variables for Terraform"
export ARM_SUBSCRIPTION_ID=your_subscription_id
export ARM_CLIENT_ID=your_appId
export ARM_CLIENT_SECRET=your_password
export ARM_TENANT_ID=your_tenant_id
```

<span data-ttu-id="ec4de-172">Bovendien, als u Terraform met Azure in China of ofwel Azure Government of Duitse Azure gebruikt, moet u tooset Hallo omgevingsvariabele op de juiste wijze.</span><span class="sxs-lookup"><span data-stu-id="ec4de-172">Additionally, if you use Terraform with Azure in China or either Azure Government or Azure Germany, you need tooset hello environment variable appropriately.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec4de-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec4de-173">Next steps</span></span>
<span data-ttu-id="ec4de-174">U hebt nu Terraform geïnstalleerd en geconfigureerd Azure-referenties, zodat u kunt starten infrastructuur implementeren in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ec4de-174">You have now installed Terraform and configured Azure credentials so that you can start deploying infrastructure into your Azure subscription.</span></span> <span data-ttu-id="ec4de-175">Vervolgens leert u hoe te[infrastructuur maken met Terraform](terraform-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="ec4de-175">Next, learn how too[create infrastructure with Terraform](terraform-create-complete-vm.md).</span></span>

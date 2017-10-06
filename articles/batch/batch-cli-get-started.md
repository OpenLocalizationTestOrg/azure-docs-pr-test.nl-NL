---
title: aaaGet de slag met Azure CLI voor Batch | Microsoft Docs
description: Get-een korte inleiding toohello batchopdrachten in de Azure CLI voor het beheren van bronnen van Azure Batch-service
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="73e39-103">Batch-resources beheren met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="73e39-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="73e39-104">Hello Azure CLI 2.0 is een nieuwe Azure opdrachtregelprogramma ervaring voor het beheren van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="73e39-104">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="73e39-105">Deze kan worden gebruikt in Mac OS, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="73e39-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="73e39-106">Azure CLI 2.0 is geoptimaliseerd voor het beheren en Azure-resources beheren vanaf Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="73e39-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from hello command line.</span></span> <span data-ttu-id="73e39-107">U kunt hello Azure CLI toomanage uw Azure Batch-accounts en toomanage resources zoals pools, jobs en taken.</span><span class="sxs-lookup"><span data-stu-id="73e39-107">You can use hello Azure CLI toomanage your Azure Batch accounts and toomanage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="73e39-108">Hello Azure CLI, kunt u veel van Hallo script dezelfde taken die u met uitvoert Hallo Batch-API's, Azure-portal en Batch PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="73e39-108">With hello Azure CLI, you can script many of hello same tasks you carry out with hello Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="73e39-109">Dit artikel biedt een overzicht van het gebruik van [Azure CLI versie 2.0](https://docs.microsoft.com/cli/azure/overview) met Batch.</span><span class="sxs-lookup"><span data-stu-id="73e39-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="73e39-110">Zie [aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) voor een overzicht van het gebruik van Hallo CLI met Azure.</span><span class="sxs-lookup"><span data-stu-id="73e39-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using hello CLI with Azure.</span></span>

<span data-ttu-id="73e39-111">Microsoft raadt u aan met de nieuwste versie Hallo van hello Azure CLI versie 2.0.</span><span class="sxs-lookup"><span data-stu-id="73e39-111">Microsoft recommends using hello latest version of hello Azure CLI, version 2.0.</span></span> <span data-ttu-id="73e39-112">Meer informatie over versie 2.0 kunt u lezen in [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/) (Azure Command Line 2.0 nu algemeen beschikbaar).</span><span class="sxs-lookup"><span data-stu-id="73e39-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-hello-azure-cli"></a><span data-ttu-id="73e39-113">Hello Azure CLI instellen</span><span class="sxs-lookup"><span data-stu-id="73e39-113">Set up hello Azure CLI</span></span>

<span data-ttu-id="73e39-114">tooinstall hello Azure CLI stappen Hallo die worden beschreven in [installeren hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="73e39-114">tooinstall hello Azure CLI, follow hello steps outlined in [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="73e39-115">We bevelen aan dat u de installatie van Azure CLI vaak tootake profiteren van de service-updates en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="73e39-115">We recommend that you update your Azure CLI installation frequently tootake advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="73e39-116">Opdracht Help</span><span class="sxs-lookup"><span data-stu-id="73e39-116">Command help</span></span>

<span data-ttu-id="73e39-117">U kunt voor elke opdracht help-tekst weergeven in hello Azure CLI door toe te voegen `-h` toohello opdracht.</span><span class="sxs-lookup"><span data-stu-id="73e39-117">You can display help text for every command in hello Azure CLI by appending `-h` toohello command.</span></span> <span data-ttu-id="73e39-118">Laat alle andere opties weg.</span><span class="sxs-lookup"><span data-stu-id="73e39-118">Omit any other options.</span></span> <span data-ttu-id="73e39-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="73e39-119">For example:</span></span>

* <span data-ttu-id="73e39-120">help voor Hallo tooget `az` opdracht, invoeren:`az -h`</span><span class="sxs-lookup"><span data-stu-id="73e39-120">tooget help for hello `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="73e39-121">een lijst met alle Batch-opdrachten in Hallo CLI tooget gebruiken:`az batch -h`</span><span class="sxs-lookup"><span data-stu-id="73e39-121">tooget a list of all Batch commands in hello CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="73e39-122">Voer in tooget informatie over het maken van een Batch-account:`az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="73e39-122">tooget help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="73e39-123">Bij twijfel gebruiken Hallo `-h` opdrachtregeloptie tooget help bij de Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="73e39-123">When in doubt, use hello `-h` command-line option tooget help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="73e39-124">Eerdere versies van hello Azure CLI gebruikt `azure` toopreface een CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="73e39-124">Earlier versions of hello Azure CLI used `azure` toopreface a CLI command.</span></span> <span data-ttu-id="73e39-125">In versie 2.0 worden alle opdrachten nu voorafgegaan door `az`.</span><span class="sxs-lookup"><span data-stu-id="73e39-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="73e39-126">Worden tooupdate ervoor dat uw scripts toouse Hallo nieuwe syntaxis met versie 2.0.</span><span class="sxs-lookup"><span data-stu-id="73e39-126">Be sure tooupdate your scripts toouse hello new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="73e39-127">Raadpleeg daarnaast toohello Azure CLI-naslagdocumentatie voor informatie over [Azure CLI-opdrachten voor Batch](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="73e39-127">Additionally, refer toohello Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="73e39-128">Aanmelden en verifiëren</span><span class="sxs-lookup"><span data-stu-id="73e39-128">Log in and authenticate</span></span>

<span data-ttu-id="73e39-129">toouse hello Azure CLI met Batch, u moet toolog in en te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="73e39-129">toouse hello Azure CLI with Batch, you need toolog in and authenticate.</span></span> <span data-ttu-id="73e39-130">Er zijn twee eenvoudige stappen toofollow:</span><span class="sxs-lookup"><span data-stu-id="73e39-130">There are two simple steps toofollow:</span></span>

1. <span data-ttu-id="73e39-131">**Aanmelden bij Azure.**</span><span class="sxs-lookup"><span data-stu-id="73e39-131">**Log into Azure.**</span></span> <span data-ttu-id="73e39-132">Aanmelden bij Azure biedt u tooAzure Resource Manager-opdrachten, inclusief toegang tot [Batch Management-service](batch-management-dotnet.md) opdrachten.</span><span class="sxs-lookup"><span data-stu-id="73e39-132">Logging into Azure gives you access tooAzure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="73e39-133">**Aanmelden bij uw Batch-account.**</span><span class="sxs-lookup"><span data-stu-id="73e39-133">**Log into your Batch account.**</span></span> <span data-ttu-id="73e39-134">Aan te melden bij uw Batch-account biedt openen u de opdrachten tooBatch service.</span><span class="sxs-lookup"><span data-stu-id="73e39-134">Logging into your Batch account gives you access tooBatch service commands.</span></span>   

### <a name="log-in-tooazure"></a><span data-ttu-id="73e39-135">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="73e39-135">Log in tooAzure</span></span>

<span data-ttu-id="73e39-136">Er zijn een aantal verschillende manieren toolog in Azure, gedetailleerd beschreven in [aanmelden met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="73e39-136">There are a few different ways toolog into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="73e39-137">[Interactief aanmelden](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="73e39-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="73e39-138">Interactief aanmelden wanneer u Azure CLI-opdrachten zelf worden uitgevoerd vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="73e39-138">Log in interactively when you are running Azure CLI commands yourself from hello command line.</span></span>
2. <span data-ttu-id="73e39-139">[Aanmelden met een service-principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="73e39-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="73e39-140">Meld u aan met een service-principal wanneer u Azure CLI-opdrachten uitvoert vanuit een script of een toepassing.</span><span class="sxs-lookup"><span data-stu-id="73e39-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="73e39-141">Voor de toepassing hello van dit artikel, laten we zien hoe toolog in Azure interactief.</span><span class="sxs-lookup"><span data-stu-id="73e39-141">For hello purposes of this article, we show how toolog into Azure interactively.</span></span> <span data-ttu-id="73e39-142">Type [az aanmelding](https://docs.microsoft.com/cli/azure/#login) op Hallo-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="73e39-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on hello command line:</span></span>

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

<span data-ttu-id="73e39-143">Hallo `az login` opdracht retourneert een token dat u tooauthenticate, kunt zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="73e39-143">hello `az login` command returns a token that you can use tooauthenticate, as shown here.</span></span> <span data-ttu-id="73e39-144">Ga als volgt Hallo instructies tooopen webpagina's en het verzenden van Hallo token tooAzure:</span><span class="sxs-lookup"><span data-stu-id="73e39-144">Follow hello instructions provided tooopen a web page and submit hello token tooAzure:</span></span>

![Meld u bij tooAzure](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="73e39-146">Hallo-voorbeelden die worden vermeld in Hallo [steekproef shell-scripts](#sample-shell-scripts) sectie ook tonen hoe toostart uw Azure CLI-sessie door interactief aanmelden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="73e39-146">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section also show how toostart your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="73e39-147">Wanneer u zich hebt aangemeld, kunt u opdrachten toowork met Batch Management bronnen, met inbegrip van Batch-accounts, sleutels toepassingspakketten en quota's aanroepen.</span><span class="sxs-lookup"><span data-stu-id="73e39-147">Once you have logged in, you can call commands toowork with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-tooyour-batch-account"></a><span data-ttu-id="73e39-148">Meld u bij tooyour Batch-account</span><span class="sxs-lookup"><span data-stu-id="73e39-148">Log in tooyour Batch account</span></span>

<span data-ttu-id="73e39-149">toouse hello Azure CLI toomanage Batch-resources, zoals groepen, taken en taken, u moet toolog in uw Batch-account en verifiëren.</span><span class="sxs-lookup"><span data-stu-id="73e39-149">toouse hello Azure CLI toomanage Batch resources, such as pools, jobs, and tasks, you need toolog into your Batch account and authenticate.</span></span> <span data-ttu-id="73e39-150">toolog in toohello Batch-service gebruiken Hallo [az batch-account aanmelding](https://docs.microsoft.com/cli/azure/batch/account#login) opdracht.</span><span class="sxs-lookup"><span data-stu-id="73e39-150">toolog in toohello Batch service, use hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="73e39-151">Er zijn twee mogelijkheden voor verificatie van uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="73e39-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="73e39-152">**Met behulp van Azure AD-verificatie (Azure Active Directory).**</span><span class="sxs-lookup"><span data-stu-id="73e39-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="73e39-153">Verificatie met Azure AD is Hallo standaardwaarde als u hello Azure CLI met Batch gebruiken en aanbevolen voor de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="73e39-153">Authenticating with Azure AD is hello default when you use hello Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="73e39-154">Wanneer u in tooAzure interactief aanmelden, zoals beschreven in de vorige sectie hello, uw referenties in cache zijn opgeslagen, zodat hello Azure CLI kunt u kunt zich aanmelden tooyour Batch-account met behulp van deze dezelfde referenties.</span><span class="sxs-lookup"><span data-stu-id="73e39-154">When you log in tooAzure interactively, as described in hello previous section, your credentials are cached, so hello Azure CLI can log you in tooyour Batch account using those same credentials.</span></span> <span data-ttu-id="73e39-155">Als u zich aanmeldt met een service-principal tooAzure, wordt deze referenties worden ook gebruikt toolog in tooyour Batch-account.</span><span class="sxs-lookup"><span data-stu-id="73e39-155">If you log in tooAzure using a service principal, those credentials are also used toolog in tooyour Batch account.</span></span>

    <span data-ttu-id="73e39-156">Een voordeel van Azure AD is de ondersteuning voor toegangsbeheer op basis van rollen (RBAC).</span><span class="sxs-lookup"><span data-stu-id="73e39-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="73e39-157">Met RBAC, van een gebruiker toegang is afhankelijk van hun rol, in plaats van of ze Hallo toegangscodes bezitten.</span><span class="sxs-lookup"><span data-stu-id="73e39-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess hello account keys.</span></span> <span data-ttu-id="73e39-158">U hoeft dus geen accountsleutels te beheren, maar RBAC-rollen, waarna Azure AD de toegang en verificatie afhandelt.</span><span class="sxs-lookup"><span data-stu-id="73e39-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="73e39-159">Verificatie met Azure AD is vereist als u hebt gemaakt uw Azure Batch-account met de modus van de toewijzing van toepassingen instellen too'User abonnement '.</span><span class="sxs-lookup"><span data-stu-id="73e39-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set too'User Subscription'.</span></span> 

    <span data-ttu-id="73e39-160">toolog in tooyour Batch-account met behulp van Azure AD, neemt u contact Hallo [az batch-account aanmelding](https://docs.microsoft.com/cli/azure/batch/account#login) opdracht:</span><span class="sxs-lookup"><span data-stu-id="73e39-160">toolog in tooyour Batch account using Azure AD, call hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="73e39-161">**Met behulp van gedeelde sleutelverificatie.**</span><span class="sxs-lookup"><span data-stu-id="73e39-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="73e39-162">[Verificatie met een gedeelde sleutel](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) maakt gebruik van uw account toegangstoetsen tooauthenticate Azure CLI-opdrachten voor Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="73e39-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys tooauthenticate Azure CLI commands for hello Batch service.</span></span>

    <span data-ttu-id="73e39-163">Als u Azure CLI-scripts tooautomate aanroepen Batch-opdrachten maakt, kunt u verificatie met gedeelde sleutel of een Azure AD-service principal.</span><span class="sxs-lookup"><span data-stu-id="73e39-163">If you are creating Azure CLI scripts tooautomate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="73e39-164">In sommige scenario's kan gedeelde sleutelverificatie een eenvoudigere oplossing zijn dan het maken van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="73e39-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="73e39-165">toolog bij het gebruik van verificatie met een gedeelde sleutel opnemen Hallo `--shared-key-auth` optie op Hallo-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="73e39-165">toolog in using Shared Key authentication, include hello `--shared-key-auth` option on hello command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="73e39-166">Hallo-voorbeelden die worden vermeld in Hallo [steekproef shell-scripts](#sample-shell-scripts) sectie laten zien hoe toolog in uw Batch-account met Azure CLI met zowel hello Azure AD en gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="73e39-166">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section show how toolog into your Batch account with hello Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="73e39-167">Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)</span><span class="sxs-lookup"><span data-stu-id="73e39-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="73e39-168">U kunt hello Azure CLI toorun Batch taken end-to-end-code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="73e39-168">You can use hello Azure CLI toorun Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="73e39-169">Batch-sjabloonbestanden ondersteuning maken pools, jobs en taken Hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="73e39-169">Batch template files support creating pools, jobs, and tasks with hello Azure CLI.</span></span> <span data-ttu-id="73e39-170">U kunt ook hello Azure CLI tooupload taak invoerbestanden toohello Azure Storage-account gekoppeld Hallo Batch-account en uitvoerbestanden taak downloaden.</span><span class="sxs-lookup"><span data-stu-id="73e39-170">You can also use hello Azure CLI tooupload job input files toohello Azure Storage account associated with hello Batch account, and download job output files from it.</span></span> <span data-ttu-id="73e39-171">Zie [Azure Batch CLI sjablonen en -bestandsoverdracht gebruiken (preview)](batch-cli-templates.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="73e39-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="73e39-172">Voorbeelden van shell-scripts</span><span class="sxs-lookup"><span data-stu-id="73e39-172">Sample shell scripts</span></span>

<span data-ttu-id="73e39-173">Hallo-voorbeeldscripts vermeld in Hallo tabel weergeven na hoe toouse Azure CLI-opdrachten met Hallo Batch-service en algemene taken voor tooaccomplish Batch Management-service.</span><span class="sxs-lookup"><span data-stu-id="73e39-173">hello sample scripts listed in hello following table show how toouse Azure CLI commands with hello Batch service and Batch Management service tooaccomplish common tasks.</span></span> <span data-ttu-id="73e39-174">Deze voorbeeldscripts betrekking hebben op veel van Hallo-opdrachten die beschikbaar zijn in hello Azure CLI voor Batch.</span><span class="sxs-lookup"><span data-stu-id="73e39-174">These sample scripts cover many of hello commands available in hello Azure CLI for Batch.</span></span> 

| <span data-ttu-id="73e39-175">Script</span><span class="sxs-lookup"><span data-stu-id="73e39-175">Script</span></span> | <span data-ttu-id="73e39-176">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="73e39-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="73e39-177">Een Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="73e39-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="73e39-178">Hiermee maakt u een Batch-account en wordt dit gekoppeld aan een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="73e39-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="73e39-179">Een toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="73e39-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="73e39-180">Hiermee voegt u een toepassing toe en worden pakketten met binaire bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="73e39-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="73e39-181">Batch-pools beheren</span><span class="sxs-lookup"><span data-stu-id="73e39-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="73e39-182">In dit script ziet u hoe u pools maakt, deze groter of kleiner maakt en beheert.</span><span class="sxs-lookup"><span data-stu-id="73e39-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="73e39-183">Een functie en taken uitvoeren met Batch</span><span class="sxs-lookup"><span data-stu-id="73e39-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="73e39-184">In dit script ziet u hoe u een functie uitvoert en taken toevoegt.</span><span class="sxs-lookup"><span data-stu-id="73e39-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="73e39-185">JSON-bestanden voor het maken van resources</span><span class="sxs-lookup"><span data-stu-id="73e39-185">JSON files for resource creation</span></span>

<span data-ttu-id="73e39-186">Wanneer u Batch-resources zoals pools en jobs maakt, kunt u een JSON-bestand met Hallo nieuwe resource-configuratie in plaats van de parameters doorgeven als opdrachtregelopties opgeven.</span><span class="sxs-lookup"><span data-stu-id="73e39-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing hello new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="73e39-187">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="73e39-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="73e39-188">U kunt de meeste Batch-resources met behulp van alleen opdrachtregelopties voor het maken, worden sommige functies vereisen dat u een bestand JSON-indeling met details van de resource Hallo opgeeft.</span><span class="sxs-lookup"><span data-stu-id="73e39-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing hello resource details.</span></span> <span data-ttu-id="73e39-189">U moet bijvoorbeeld een JSON-bestand gebruiken als u wilt dat de bronbestanden toospecify voor een begintaak.</span><span class="sxs-lookup"><span data-stu-id="73e39-189">For example, you must use a JSON file if you want toospecify resource files for a start task.</span></span>

<span data-ttu-id="73e39-190">toosee hello JSON syntaxis toocreate vereist een resource, raadpleeg dan toohello [Batch REST-API-verwijzing] [ rest_api] documentatie.</span><span class="sxs-lookup"><span data-stu-id="73e39-190">toosee hello JSON syntax required toocreate a resource, refer toohello [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="73e39-191">Elke ' Add *brontype*' onderwerp in Hallo naslaginformatie over REST API bevat JSON-voorbeeldscripts voor het maken van die bron.</span><span class="sxs-lookup"><span data-stu-id="73e39-191">Each "Add *resource type*" topic in hello REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="73e39-192">U kunt deze JSON-voorbeeldscripts als sjabloon gebruiken voor JSON-bestanden toouse Hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="73e39-192">You can use those sample JSON scripts as templates for JSON files toouse with hello Azure CLI.</span></span> <span data-ttu-id="73e39-193">Bijvoorbeeld toosee Hallo JSON-syntaxis voor het maken van de groep van toepassingen te verwijzen[toevoegen van een account voor toepassingsgroep tooan][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="73e39-193">For example, toosee hello JSON syntax for pool creation, refer too[Add a pool tooan account][rest_add_pool].</span></span>

<span data-ttu-id="73e39-194">Zie [Running jobs on Azure Batch with Azure CLI](./scripts/batch-cli-sample-run-job.md) (Taken uitvoeren in Azure Batch met Azure CLI) voor een voorbeeld van een script waarin een JSON-bestand is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="73e39-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="73e39-195">Als u een JSON-bestand opgeeft wanneer u een resource maakt, worden andere parameters die u op de opdrachtregel Hallo voor die bron opgeeft worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="73e39-195">If you specify a JSON file when you create a resource, any other parameters that you specify on hello command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="73e39-196">Efficiënte query's voor Batch-resources</span><span class="sxs-lookup"><span data-stu-id="73e39-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="73e39-197">Elk Batch-resourcetype ondersteunt een `list`-opdracht die een query uitvoert voor het Batch-account, en vermeldt een lijst met resources van dit type.</span><span class="sxs-lookup"><span data-stu-id="73e39-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="73e39-198">U kunt bijvoorbeeld Hallo toepassingen weergeven in uw account en het Hallo-taken in een job:</span><span class="sxs-lookup"><span data-stu-id="73e39-198">For example, you can list hello pools in your account and hello tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="73e39-199">Wanneer u een query Hallo Batch-service met een `list` bewerking, kunt u een OData-component toolimit Hallo hoeveelheid gegevens die worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="73e39-199">When you query hello Batch service with a `list` operation, you can specify an OData clause toolimit hello amount of data returned.</span></span> <span data-ttu-id="73e39-200">Omdat alle filteren serverzijde plaatsvindt, bestrijkt alleen Hallo gegevens die u aanvragen Hallo-kabel.</span><span class="sxs-lookup"><span data-stu-id="73e39-200">Because all filtering occurs server-side, only hello data you request crosses hello wire.</span></span> <span data-ttu-id="73e39-201">Deze componenten toosave bandbreedte gebruiken (en dus time) wanneer u een lijst met bewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="73e39-201">Use these clauses toosave bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="73e39-202">Hallo staan volgende tabel Hallo OData-componenten ondersteund door Hallo Batch-service:</span><span class="sxs-lookup"><span data-stu-id="73e39-202">hello following table describes hello OData clauses supported by hello Batch service:</span></span>

| <span data-ttu-id="73e39-203">Component</span><span class="sxs-lookup"><span data-stu-id="73e39-203">Clause</span></span> | <span data-ttu-id="73e39-204">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="73e39-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="73e39-205">Retourneert een subset met eigenschappen voor elke entiteit.</span><span class="sxs-lookup"><span data-stu-id="73e39-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="73e39-206">Retourneert alleen entiteiten die overeenkomen met de Hallo opgegeven OData-expressie.</span><span class="sxs-lookup"><span data-stu-id="73e39-206">Returns only entities that match hello specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="73e39-207">Verkrijgt Hallo entiteit in één onderliggende REST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="73e39-207">Obtains hello entity information in a single underlying REST call.</span></span> <span data-ttu-id="73e39-208">Hallo Vouw Component momenteel ondersteunt alleen Hallo `stats` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="73e39-208">hello expand clause currently supports only hello `stats` property.</span></span> |

<span data-ttu-id="73e39-209">Voor een voorbeeld van een script dat toont hoe een OData-component toouse zien [een job en taken uitvoeren met Batch](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="73e39-209">For a sample script that shows how toouse an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="73e39-210">Zie voor meer informatie over het uitvoeren van query's efficiënt lijst met OData-componenten [hello Azure Batch-service efficiënt Query](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="73e39-210">For more information on performing efficient list queries with OData clauses, see [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="73e39-211">Tips voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="73e39-211">Troubleshooting tips</span></span>

<span data-ttu-id="73e39-212">Hallo kunt volgende tips u Azure CLI-problemen oplossen:</span><span class="sxs-lookup"><span data-stu-id="73e39-212">hello following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="73e39-213">Gebruik `-h` tooget **help-tekst** voor elke opdracht CLI</span><span class="sxs-lookup"><span data-stu-id="73e39-213">Use `-h` tooget **help text** for any CLI command</span></span>
* <span data-ttu-id="73e39-214">Gebruik `-v` en `-vv` toodisplay **uitgebreide** opdracht uitvoer.</span><span class="sxs-lookup"><span data-stu-id="73e39-214">Use `-v` and `-vv` toodisplay **verbose** command output.</span></span> <span data-ttu-id="73e39-215">Wanneer Hallo `-vv` vlag is opgenomen, hello Azure CLI geeft Hallo werkelijke REST-aanvragen en antwoorden.</span><span class="sxs-lookup"><span data-stu-id="73e39-215">When hello `-vv` flag is included, hello Azure CLI displays hello actual REST requests and responses.</span></span> <span data-ttu-id="73e39-216">Deze schakelopties zijn handig voor het weergeven van de volledige foutuitvoer.</span><span class="sxs-lookup"><span data-stu-id="73e39-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="73e39-217">U kunt bekijken **opdracht uitvoer als JSON** Hello `--json` optie.</span><span class="sxs-lookup"><span data-stu-id="73e39-217">You can view **command output as JSON** with hello `--json` option.</span></span> <span data-ttu-id="73e39-218">`az batch pool show pool001 --json` wordt bijvoorbeeld weergegeven als eigenschappen van pool001 in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="73e39-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="73e39-219">U kunt vervolgens kopiëren en wijzigen van deze toouse uitvoer in een `--json-file` (Zie [JSON-bestanden](#json-files) eerder in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="73e39-219">You can then copy and modify this output toouse in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* <span data-ttu-id="73e39-220">Hallo [Batch-forum] [ batch_forum] wordt bewaakt door de teamleden Batch.</span><span class="sxs-lookup"><span data-stu-id="73e39-220">hello [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="73e39-221">U kunt hier vragen posten als u problemen hebt of hulp nodig hebt met een bepaalde bewerking.</span><span class="sxs-lookup"><span data-stu-id="73e39-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="73e39-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="73e39-222">Next steps</span></span>

* <span data-ttu-id="73e39-223">Zie voor meer informatie over hello Azure CLI Hallo [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="73e39-223">For more information about hello Azure CLI, see hello [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="73e39-224">Meer informatie over Batch-resources vindt u in dit Engelstalige [overzicht van Azure Batch voor ontwikkelaars](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="73e39-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="73e39-225">Zie voor meer informatie over het gebruik van Batch sjablonen toocreate pools, jobs en taken zonder code te schrijven [gebruik Azure Batch CLI sjablonen en File Transfer (Preview)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="73e39-225">For more information about using Batch templates toocreate pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx

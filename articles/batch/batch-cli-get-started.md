---
title: Aan de slag met Azure CLI voor Batch | Microsoft Docs
description: Een korte inleiding in de Batch-opdrachten in Azure CLI voor het beheren van Azure Batch-serviceresources
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
ms.openlocfilehash: 9bee0344ba70c50cda36a87ea617906283040ff9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="0e3d8-103">Batch-resources beheren met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0e3d8-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="0e3d8-104">De Azure CLI 2.0 is de nieuwe opdrachtregelervaring van Azure voor het beheer van Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-104">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="0e3d8-105">Deze kan worden gebruikt in Mac OS, Linux en Windows.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="0e3d8-106">Azure CLI 2.0 is geoptimaliseerd voor het beheren van Azure-resources vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from the command line.</span></span> <span data-ttu-id="0e3d8-107">U kunt de Azure CLI gebruiken om uw Azure Batch-accounts te beheren en om resources zoals pools, functies en taken te beheren.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-107">You can use the Azure CLI to manage your Azure Batch accounts and to manage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="0e3d8-108">Met de Azure CLI kunt u scripts maken om veel van dezelfde taken uit te voeren die u ook uitvoert met de Batch-API's, Azure Portal en Batch PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-108">With the Azure CLI, you can script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="0e3d8-109">Dit artikel biedt een overzicht van het gebruik van [Azure CLI versie 2.0](https://docs.microsoft.com/cli/azure/overview) met Batch.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="0e3d8-110">Zie [Aan de slag met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) voor een overzicht van het gebruik van CLI met Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using the CLI with Azure.</span></span>

<span data-ttu-id="0e3d8-111">Microsoft adviseert om de nieuwste versie van Azure CLI te gebruiken, versie 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-111">Microsoft recommends using the latest version of the Azure CLI, version 2.0.</span></span> <span data-ttu-id="0e3d8-112">Meer informatie over versie 2.0 kunt u lezen in [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/) (Azure Command Line 2.0 nu algemeen beschikbaar).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-the-azure-cli"></a><span data-ttu-id="0e3d8-113">De Azure CLI instellen</span><span class="sxs-lookup"><span data-stu-id="0e3d8-113">Set up the Azure CLI</span></span>

<span data-ttu-id="0e3d8-114">Volg de stappen in [Azure CLI installeren](https://docs.microsoft.com/cli/azure/install-azure-cli.md) voor het installeren van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-114">To install the Azure CLI, follow the steps outlined in [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="0e3d8-115">Het wordt aangeraden de Azure CLI-installatie regelmatig bij te werken om te profiteren van service-updates en verbeteringen.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-115">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="0e3d8-116">Opdracht Help</span><span class="sxs-lookup"><span data-stu-id="0e3d8-116">Command help</span></span>

<span data-ttu-id="0e3d8-117">U kunt voor elke opdracht in de Azure CLI Help-tekst weergeven door `-h` toe te voegen aan de opdracht.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-117">You can display help text for every command in the Azure CLI by appending `-h` to the command.</span></span> <span data-ttu-id="0e3d8-118">Laat alle andere opties weg.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-118">Omit any other options.</span></span> <span data-ttu-id="0e3d8-119">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-119">For example:</span></span>

* <span data-ttu-id="0e3d8-120">Als u hulp nodig hebt bij de opdracht `az`, voert u in: `az -h`</span><span class="sxs-lookup"><span data-stu-id="0e3d8-120">To get help for the `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="0e3d8-121">Voor een lijst met alle Batch-opdrachten in de opdrachtregelinterface, gebruikt u: `az batch -h`</span><span class="sxs-lookup"><span data-stu-id="0e3d8-121">To get a list of all Batch commands in the CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="0e3d8-122">Als u hulp nodig hebt bij het maken van een Batch-account, voert u in: `az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="0e3d8-122">To get help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="0e3d8-123">Gebruik bij twijfel de opdrachtregeloptie `-h` voor hulp bij een willekeurige Azure CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-123">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="0e3d8-124">In eerdere versies van de Azure CLI werd `azure` gebruikt vóór een CLI-opdracht.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-124">Earlier versions of the Azure CLI used `azure` to preface a CLI command.</span></span> <span data-ttu-id="0e3d8-125">In versie 2.0 worden alle opdrachten nu voorafgegaan door `az`.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="0e3d8-126">Vergeet niet om uw scripts bij te werken met de nieuwe syntaxis van versie 2.0.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-126">Be sure to update your scripts to use the new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="0e3d8-127">Raadpleeg de naslagdocumentatie van Azure CLI voor informatie over [Azure CLI-opdrachten voor Batch](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-127">Additionally, refer to the Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="0e3d8-128">Aanmelden en verifiëren</span><span class="sxs-lookup"><span data-stu-id="0e3d8-128">Log in and authenticate</span></span>

<span data-ttu-id="0e3d8-129">Als u de Azure CLI wilt gebruiken met Batch, moet u zich aanmelden en verifiëren.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-129">To use the Azure CLI with Batch, you need to log in and authenticate.</span></span> <span data-ttu-id="0e3d8-130">Dit kan via twee eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-130">There are two simple steps to follow:</span></span>

1. <span data-ttu-id="0e3d8-131">**Aanmelden bij Azure.**</span><span class="sxs-lookup"><span data-stu-id="0e3d8-131">**Log into Azure.**</span></span> <span data-ttu-id="0e3d8-132">Als u bent aangemeld bij Azure, hebt u toegang tot opdrachten van Azure Resource Manager, inclusief opdrachten van de [Batch Management-service](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-132">Logging into Azure gives you access to Azure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="0e3d8-133">**Aanmelden bij uw Batch-account.**</span><span class="sxs-lookup"><span data-stu-id="0e3d8-133">**Log into your Batch account.**</span></span> <span data-ttu-id="0e3d8-134">Als u bent aangemeld bij uw Batch-account, hebt u toegang tot opdrachten van de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-134">Logging into your Batch account gives you access to Batch service commands.</span></span>   

### <a name="log-in-to-azure"></a><span data-ttu-id="0e3d8-135">Meld u aan bij Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-135">Log in to Azure</span></span>

<span data-ttu-id="0e3d8-136">Er zijn een aantal manieren om u aan te melden bij Azure, zoals u kunt lezen in [Aanmelden met de Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="0e3d8-136">There are a few different ways to log into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="0e3d8-137">[Interactief aanmelden](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="0e3d8-138">Meld u interactief aan wanneer u zelf Azure CLI-opdrachten uitvoert vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-138">Log in interactively when you are running Azure CLI commands yourself from the command line.</span></span>
2. <span data-ttu-id="0e3d8-139">[Aanmelden met een service-principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="0e3d8-140">Meld u aan met een service-principal wanneer u Azure CLI-opdrachten uitvoert vanuit een script of een toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="0e3d8-141">Ten behoeve van dit artikel laten we zien hoe u zich interactief aanmeldt bij Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-141">For the purposes of this article, we show how to log into Azure interactively.</span></span> <span data-ttu-id="0e3d8-142">Typ [az login](https://docs.microsoft.com/cli/azure/#login) op de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on the command line:</span></span>

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

<span data-ttu-id="0e3d8-143">De opdracht `az login` retourneert een token dat u kunt gebruiken om u te verifiëren, zoals hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-143">The `az login` command returns a token that you can use to authenticate, as shown here.</span></span> <span data-ttu-id="0e3d8-144">Volg de weergegeven instructies om een webpagina te openen en het token naar Azure te verzenden:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-144">Follow the instructions provided to open a web page and submit the token to Azure:</span></span>

![Meld u aan bij Azure.](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="0e3d8-146">De voorbeelden in de sectie [Voorbeelden van shell-scripts](#sample-shell-scripts) laten ook zien hoe u een Azure CLI-sessie start door u interactief aan te melden bij Azure.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-146">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section also show how to start your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="0e3d8-147">Wanneer u bent aangemeld, kunt u opdrachten aanroepen voor gebruik met resources van Batch Management, met inbegrip van Batch-accounts, sleutels, toepassingspakketten en quota's.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-147">Once you have logged in, you can call commands to work with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-to-your-batch-account"></a><span data-ttu-id="0e3d8-148">Aanmelden bij uw Batch-account</span><span class="sxs-lookup"><span data-stu-id="0e3d8-148">Log in to your Batch account</span></span>

<span data-ttu-id="0e3d8-149">Als u de Azure CLI wilt gebruiken voor het beheren van Batch-resources, zoals pools, functies en taken, moet u zich aanmelden bij uw Batch-account en u vervolgens verifiëren.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-149">To use the Azure CLI to manage Batch resources, such as pools, jobs, and tasks, you need to log into your Batch account and authenticate.</span></span> <span data-ttu-id="0e3d8-150">U kunt zich aanmelden bij de Batch-service met de opdracht [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-150">To log in to the Batch service, use the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="0e3d8-151">Er zijn twee mogelijkheden voor verificatie van uw Batch-account:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="0e3d8-152">**Met behulp van Azure AD-verificatie (Azure Active Directory).**</span><span class="sxs-lookup"><span data-stu-id="0e3d8-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="0e3d8-153">Verificatie met Azure AD is de standaardinstelling als u de Azure CLI gebruikt met Batch en wordt aanbevolen voor de meeste scenario's.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-153">Authenticating with Azure AD is the default when you use the Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="0e3d8-154">Wanneer u zich interactief aanmeldt bij Azure, zoals beschreven in de vorige sectie, worden uw referenties in de cache opgeslagen, zodat de Azure CLI u met behulp van deze zelfde referenties kan aanmelden bij uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-154">When you log in to Azure interactively, as described in the previous section, your credentials are cached, so the Azure CLI can log you in to your Batch account using those same credentials.</span></span> <span data-ttu-id="0e3d8-155">Als u zich aanmeldt bij Azure met behulp van een service-principal, worden deze referenties ook gebruikt voor aanmelding bij uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-155">If you log in to Azure using a service principal, those credentials are also used to log in to your Batch account.</span></span>

    <span data-ttu-id="0e3d8-156">Een voordeel van Azure AD is de ondersteuning voor toegangsbeheer op basis van rollen (RBAC).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="0e3d8-157">Met RBAC is de toegang van gebruikers afhankelijk van hun rol, in plaats van of ze wel of niet over de accountsleutels beschikken.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess the account keys.</span></span> <span data-ttu-id="0e3d8-158">U hoeft dus geen accountsleutels te beheren, maar RBAC-rollen, waarna Azure AD de toegang en verificatie afhandelt.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="0e3d8-159">Verificatie met Azure AD is vereist als u uw Azure Batch-account hebt gemaakt met de modus voor groepstoewijzing ingesteld op Gebruikersabonnement.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set to 'User Subscription'.</span></span> 

    <span data-ttu-id="0e3d8-160">Als u zich via Azure AD wilt aanmelden bij uw Batch-account, gebruikt u de opdracht [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login):</span><span class="sxs-lookup"><span data-stu-id="0e3d8-160">To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="0e3d8-161">**Met behulp van gedeelde sleutelverificatie.**</span><span class="sxs-lookup"><span data-stu-id="0e3d8-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="0e3d8-162">Bij [gedeelde sleutelverificatie](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) worden de toegangssleutels van uw account gebruikt om Azure CLI-opdrachten te verifiëren voor de Batch-service.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys to authenticate Azure CLI commands for the Batch service.</span></span>

    <span data-ttu-id="0e3d8-163">Als u Azure CLI-scripts maakt om het aanroepen van Batch-opdrachten te automatiseren, kunt u gebruikmaken van gedeelde sleutelverificatie of van een service-principal van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-163">If you are creating Azure CLI scripts to automate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="0e3d8-164">In sommige scenario's kan gedeelde sleutelverificatie een eenvoudigere oplossing zijn dan het maken van een service-principal.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="0e3d8-165">Als u zich wilt aanmelden met behulp van gedeelde sleutelverificatie, gebruikt u de optie `--shared-key-auth` op de opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-165">To log in using Shared Key authentication, include the `--shared-key-auth` option on the command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="0e3d8-166">De voorbeelden in de sectie [Voorbeelden van shell-scripts](#sample-shell-scripts) laten zien hoe u zich met de Azure CLI aanmeldt bij uw Batch-account met zowel Azure AD als een gedeelde sleutel.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-166">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section show how to log into your Batch account with the Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="0e3d8-167">Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)</span><span class="sxs-lookup"><span data-stu-id="0e3d8-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="0e3d8-168">U kunt de Azure CLI gebruiken om Batch-taken end-to-end uit te voeren zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-168">You can use the Azure CLI to run Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="0e3d8-169">Batch-sjabloonbestanden ondersteunen het maken van pools, jobs en taken met de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-169">Batch template files support creating pools, jobs, and tasks with the Azure CLI.</span></span> <span data-ttu-id="0e3d8-170">U kunt de Azure CLI ook gebruiken om jobinvoerbestanden te uploaden naar het Azure Storage-account dat is gekoppeld aan het Batch-account en de jobuitvoerbestanden ervan downloaden.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-170">You can also use the Azure CLI to upload job input files to the Azure Storage account associated with the Batch account, and download job output files from it.</span></span> <span data-ttu-id="0e3d8-171">Zie [Azure Batch CLI sjablonen en -bestandsoverdracht gebruiken (preview)](batch-cli-templates.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="0e3d8-172">Voorbeelden van shell-scripts</span><span class="sxs-lookup"><span data-stu-id="0e3d8-172">Sample shell scripts</span></span>

<span data-ttu-id="0e3d8-173">De voorbeeldscripts in de volgende tabel laten zien hoe u Azure CLI-opdrachten gebruikt met de Batch-service en de Batch-Management-service om veelvoorkomende taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-173">The sample scripts listed in the following table show how to use Azure CLI commands with the Batch service and Batch Management service to accomplish common tasks.</span></span> <span data-ttu-id="0e3d8-174">In deze voorbeeldscripts worden veel van de opdrachten behandeld die beschikbaar zijn in de Azure CLI voor Batch.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-174">These sample scripts cover many of the commands available in the Azure CLI for Batch.</span></span> 

| <span data-ttu-id="0e3d8-175">Script</span><span class="sxs-lookup"><span data-stu-id="0e3d8-175">Script</span></span> | <span data-ttu-id="0e3d8-176">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="0e3d8-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0e3d8-177">Een Batch-account maken</span><span class="sxs-lookup"><span data-stu-id="0e3d8-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="0e3d8-178">Hiermee maakt u een Batch-account en wordt dit gekoppeld aan een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="0e3d8-179">Een toepassing toevoegen</span><span class="sxs-lookup"><span data-stu-id="0e3d8-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="0e3d8-180">Hiermee voegt u een toepassing toe en worden pakketten met binaire bestanden geüpload.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="0e3d8-181">Batch-pools beheren</span><span class="sxs-lookup"><span data-stu-id="0e3d8-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="0e3d8-182">In dit script ziet u hoe u pools maakt, deze groter of kleiner maakt en beheert.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="0e3d8-183">Een functie en taken uitvoeren met Batch</span><span class="sxs-lookup"><span data-stu-id="0e3d8-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="0e3d8-184">In dit script ziet u hoe u een functie uitvoert en taken toevoegt.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="0e3d8-185">JSON-bestanden voor het maken van resources</span><span class="sxs-lookup"><span data-stu-id="0e3d8-185">JSON files for resource creation</span></span>

<span data-ttu-id="0e3d8-186">Als u Batch-resources maakt, zoals groepen en taken, kunt u een JSON-bestand opgeven dat de configuratie van de nieuwe resource bevat, in plaats van de bijbehorende parameters op te geven als opdrachtregelopties.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="0e3d8-187">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="0e3d8-188">Hoewel u de meeste resources kunt maken met alleen opdrachtregelopties, is voor sommige functies vereist dat u een bestand met de JSON-indeling opgeeft met daarin details van de resource.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing the resource details.</span></span> <span data-ttu-id="0e3d8-189">U moet bijvoorbeeld een JSON-bestand gebruiken als u resourcebestanden wilt opgeven voor een starttaak.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-189">For example, you must use a JSON file if you want to specify resource files for a start task.</span></span>

<span data-ttu-id="0e3d8-190">Informatie over de juiste JSON-syntaxis voor het maken van een resource vindt u in de Engelstalige [Azure Batch REST API Reference][rest_api].</span><span class="sxs-lookup"><span data-stu-id="0e3d8-190">To see the JSON syntax required to create a resource, refer to the [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="0e3d8-191">De onderwerpen voor het toevoegen van een *resourcetype* in de Azure Batch REST API Reference bevat JSON-voorbeeldscripts voor het maken van die resource.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-191">Each "Add *resource type*" topic in the REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="0e3d8-192">U kunt deze JSON-voorbeeldscripts als sjablonen gebruiken voor JSON-bestanden die u met de Azure CLI wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-192">You can use those sample JSON scripts as templates for JSON files to use with the Azure CLI.</span></span> <span data-ttu-id="0e3d8-193">Als u bijvoorbeeld de JSON-syntaxis wilt zien voor het maken van een pool, raadpleegt u [Add a pool to an account][rest_add_pool] (Een pool toevoegen aan een account).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-193">For example, to see the JSON syntax for pool creation, refer to [Add a pool to an account][rest_add_pool].</span></span>

<span data-ttu-id="0e3d8-194">Zie [Running jobs on Azure Batch with Azure CLI](./scripts/batch-cli-sample-run-job.md) (Taken uitvoeren in Azure Batch met Azure CLI) voor een voorbeeld van een script waarin een JSON-bestand is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0e3d8-195">Als u een JSON-bestand opgeeft bij het maken van een resource, worden alle andere parameters die u opgeeft op de opdrachtregel, genegeerd.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-195">If you specify a JSON file when you create a resource, any other parameters that you specify on the command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="0e3d8-196">Efficiënte query's voor Batch-resources</span><span class="sxs-lookup"><span data-stu-id="0e3d8-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="0e3d8-197">Elk Batch-resourcetype ondersteunt een `list`-opdracht die een query uitvoert voor het Batch-account, en vermeldt een lijst met resources van dit type.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="0e3d8-198">U kunt bijvoorbeeld de groepen in uw account vermelden en de taken in een taak:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-198">For example, you can list the pools in your account and the tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="0e3d8-199">Wanneer u op de Batch-service een query uitvoert met daarin een `list`-bewerking, kunt u een OData-component opgeven om de hoeveelheid geretourneerde gegevens te beperken.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-199">When you query the Batch service with a `list` operation, you can specify an OData clause to limit the amount of data returned.</span></span> <span data-ttu-id="0e3d8-200">Omdat de filteracties op de server plaatsvinden, worden alleen de gegevens geretourneerd waarin u bent geïnteresseerd.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-200">Because all filtering occurs server-side, only the data you request crosses the wire.</span></span> <span data-ttu-id="0e3d8-201">Gebruik deze componenten om bandbreedte (en dus tijd) te besparen tijdens het uitvoeren van lijstbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-201">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="0e3d8-202">De volgende tabel beschrijft de OData-componenten die worden ondersteund door de Batch-service:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-202">The following table describes the OData clauses supported by the Batch service:</span></span>

| <span data-ttu-id="0e3d8-203">Component</span><span class="sxs-lookup"><span data-stu-id="0e3d8-203">Clause</span></span> | <span data-ttu-id="0e3d8-204">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0e3d8-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="0e3d8-205">Retourneert een subset met eigenschappen voor elke entiteit.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="0e3d8-206">Retourneert alleen entiteiten die overeenkomen met de opgegeven OData-expressie.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-206">Returns only entities that match the specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="0e3d8-207">Vraagt de entiteitgegevens op in één onderliggende REST-aanroep.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-207">Obtains the entity information in a single underlying REST call.</span></span> <span data-ttu-id="0e3d8-208">De component expand ondersteunt momenteel alleen de eigenschap `stats`.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-208">The expand clause currently supports only the `stats` property.</span></span> |

<span data-ttu-id="0e3d8-209">Zie [Een functie en taken uitvoeren met Batch](./scripts/batch-cli-sample-run-job.md) voor een voorbeeld van een script dat laat zien hoe u een OData-component gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-209">For a sample script that shows how to use an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="0e3d8-210">Zie [Create queries to list Batch resources efficiently](batch-efficient-list-queries.md) (Query's maken om efficiënt Batch-resources op te vragen) voor meer informatie over het uitvoeren van efficiënte lijstquery's met OData-componenten.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-210">For more information on performing efficient list queries with OData clauses, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="0e3d8-211">Tips voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="0e3d8-211">Troubleshooting tips</span></span>

<span data-ttu-id="0e3d8-212">De volgende tips kunnen helpen bij het oplossen van problemen met Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="0e3d8-212">The following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="0e3d8-213">Gebruik `-h` om **Help-tekst** weer te geven voor elke willekeurige CLI-opdracht</span><span class="sxs-lookup"><span data-stu-id="0e3d8-213">Use `-h` to get **help text** for any CLI command</span></span>
* <span data-ttu-id="0e3d8-214">Gebruik `-v` en `-vv` om **uitgebreide** opdrachtuitvoer weer te geven.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-214">Use `-v` and `-vv` to display **verbose** command output.</span></span> <span data-ttu-id="0e3d8-215">Als u de vlag `-vv` toevoegt, toont de Azure CLI de werkelijke REST-aanvragen en -antwoorden.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-215">When the `-vv` flag is included, the Azure CLI displays the actual REST requests and responses.</span></span> <span data-ttu-id="0e3d8-216">Deze schakelopties zijn handig voor het weergeven van de volledige foutuitvoer.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="0e3d8-217">U kunt **opdrachtuitvoer weergeven als JSON** met de `--json`-optie.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-217">You can view **command output as JSON** with the `--json` option.</span></span> <span data-ttu-id="0e3d8-218">`az batch pool show pool001 --json` wordt bijvoorbeeld weergegeven als eigenschappen van pool001 in de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="0e3d8-219">Vervolgens kunt u deze uitvoer kopiëren en aanpassen om te worden gebruikt in een `--json-file` (zie [JSON-bestanden](#json-files) eerder in dit artikel).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-219">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* <span data-ttu-id="0e3d8-220">Het [Batch-forum][batch_forum] wordt gecontroleerd door leden van het Batch-team.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-220">The [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="0e3d8-221">U kunt hier vragen posten als u problemen hebt of hulp nodig hebt met een bepaalde bewerking.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e3d8-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e3d8-222">Next steps</span></span>

* <span data-ttu-id="0e3d8-223">Raadpleeg de [documentatie van Azure CLI](https://docs.microsoft.com/cli/azure/overview) voor meer informatie over de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-223">For more information about the Azure CLI, see the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="0e3d8-224">Meer informatie over Batch-resources vindt u in dit Engelstalige [overzicht van Azure Batch voor ontwikkelaars](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="0e3d8-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="0e3d8-225">Zie [Azure Batch CLI-sjablonen en -bestandsoverdracht gebruiken (preview)](batch-cli-templates.md) voor meer informatie over het gebruik van Batch-sjablonen voor het maken van pools, jobs en taken zonder code te schrijven.</span><span class="sxs-lookup"><span data-stu-id="0e3d8-225">For more information about using Batch templates to create pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx

---
title: aaaManage Azure Key Vault met CLI | Microsoft Docs
description: Gebruik van deze zelfstudie tooautomate algemene taken in de Sleutelkluis via Hallo CLI 2.0
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="198fe-103">Beheren met CLI 2.0 Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="198fe-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="198fe-104">Azure Sleutelkluis is beschikbaar in de meeste regio's.</span><span class="sxs-lookup"><span data-stu-id="198fe-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="198fe-105">Zie voor meer informatie, Hallo [pagina prijzen van Sleutelkluis](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="198fe-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="198fe-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="198fe-106">Introduction</span></span>
<span data-ttu-id="198fe-107">Gebruik van deze zelfstudie toohelp die u aan de slag met Azure Key Vault toocreate een geharde container (een kluis) in Azure, toostore en beheren van de cryptografische sleutels en geheimen in Azure.</span><span class="sxs-lookup"><span data-stu-id="198fe-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="198fe-108">Deze begeleidt u bij Hallo proces van het gebruik van Azure platformoverschrijdende opdrachtregelinterface toocreate een kluis die een sleutel of het wachtwoord dat u vervolgens met een Azure-toepassing gebruiken kunt bevat.</span><span class="sxs-lookup"><span data-stu-id="198fe-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="198fe-109">Deze vervolgens ziet u hoe een toepassing kunt vervolgens sleutel of het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="198fe-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="198fe-110">**Geschatte tijd toocomplete:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="198fe-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="198fe-111">Deze zelfstudie bevat geen instructies over hoe toowrite hello Azure-toepassing met een van de stappen hello, waaruit blijkt hoe tooauthorize een toouse toepassing een sleutel of geheim in de sleutel Hallo-kluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="198fe-112">Deze zelfstudie maakt gebruik van Hallo nieuwste Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="198fe-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="198fe-113">Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="198fe-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="198fe-114">Prerequisites</span></span>
<span data-ttu-id="198fe-115">toocomplete in deze zelfstudie hebt u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="198fe-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="198fe-116">Een abonnement tooMicrosoft Azure.</span><span class="sxs-lookup"><span data-stu-id="198fe-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="198fe-117">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="198fe-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="198fe-118">Opdrachtregelinterface versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="198fe-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="198fe-119">tooinstall Hallo meest recente versie en verbinding maken met tooyour Azure-abonnement, Zie [installeren en configureren van hello Azure platformoverschrijdende opdrachtregelinterface 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="198fe-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="198fe-120">Een toepassing die worden zal geconfigureerde toouse Hallo sleutel of het wachtwoord die u in deze zelfstudie maakt.</span><span class="sxs-lookup"><span data-stu-id="198fe-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="198fe-121">Er is een voorbeeldtoepassing beschikbaar is via Hallo [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="198fe-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="198fe-122">Zie voor instructies Hallo bijbehorende Leesmij-bestand.</span><span class="sxs-lookup"><span data-stu-id="198fe-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="198fe-123">Help-informatie met Azure platformoverschrijdende opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="198fe-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="198fe-124">Deze zelfstudie wordt ervan uitgegaan dat u bekend met Hallo-opdrachtregelinterface (Bash, Terminal-opdrachtprompt bent)</span><span class="sxs-lookup"><span data-stu-id="198fe-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="198fe-125">Hallo--help- of -h parameter is tooview help gebruikt voor specifieke opdrachten.</span><span class="sxs-lookup"><span data-stu-id="198fe-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="198fe-126">U kunt ook Hallo hello azure help [opdracht] [opties] indeling kan ook worden gebruikt tooreturn dezelfde informatie.</span><span class="sxs-lookup"><span data-stu-id="198fe-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="198fe-127">Bijvoorbeeld Hallo volgende alle return opdrachten Hallo dezelfde informatie:</span><span class="sxs-lookup"><span data-stu-id="198fe-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="198fe-128">Raadpleeg bij twijfel over Hallo parameters nodig is voor een opdracht met behulp van toohelp--help, -h of az help [opdracht].</span><span class="sxs-lookup"><span data-stu-id="198fe-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="198fe-129">U kunt ook de volgende zelfstudies tooget bekend met Azure Resource Manager in Azure platformoverschrijdende opdrachtregelinterface Hallo lezen:</span><span class="sxs-lookup"><span data-stu-id="198fe-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="198fe-130">Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="198fe-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="198fe-131">Aan de slag met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="198fe-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="198fe-132">Verbinding maken met tooyour abonnementen</span><span class="sxs-lookup"><span data-stu-id="198fe-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="198fe-133">toolog aan met een organisatieaccount, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="198fe-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="198fe-134">of als u toolog wilt in interactief typen</span><span class="sxs-lookup"><span data-stu-id="198fe-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="198fe-135">Als u meerdere abonnementen hebt en wilt dat een specifieke één toouse toospecify voor Azure Sleutelkluis, typt u Hallo toosee Hallo abonnementen voor uw account te volgen:</span><span class="sxs-lookup"><span data-stu-id="198fe-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="198fe-136">Vervolgens toospecify Hallo abonnement toouse, type:</span><span class="sxs-lookup"><span data-stu-id="198fe-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="198fe-137">Zie voor meer informatie over het configureren van Azure platformoverschrijdende opdrachtregelinterface [Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="198fe-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="198fe-138">Een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="198fe-138">Create a new resource group</span></span>
<span data-ttu-id="198fe-139">Wanneer u Azure Resource Manager gebruikt, worden alle gerelateerde resources gemaakt binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="198fe-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="198fe-140">We gaan een nieuwe resourcegroep 'ContosoResourceGroup' maken voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="198fe-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="198fe-141">Hallo eerste parameter is de naam van resourcegroep en de tweede parameter Hallo Hallo locatie.</span><span class="sxs-lookup"><span data-stu-id="198fe-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="198fe-142">Voor de locatie, gebruikt u Hallo opdracht `az account list-locations` tooidentify hoe toospecify een alternatieve locatie toohello een in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="198fe-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="198fe-143">Als u meer informatie nodig hebt, typt: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="198fe-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="198fe-144">De registerbronprovider hello Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="198fe-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="198fe-145">Zorg ervoor dat Sleutelkluis-resourceprovider is geregistreerd in uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="198fe-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="198fe-146">Dit moet alleen toobe gebeurt eenmaal per abonnement.</span><span class="sxs-lookup"><span data-stu-id="198fe-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="198fe-147">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="198fe-147">Create a key vault</span></span>
<span data-ttu-id="198fe-148">Gebruik Hallo `az keyvault create` opdracht toocreate een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="198fe-149">Dit script heeft drie verplichte parameters: de naam van een resource-groep, een sleutelkluisnaam en Hallo geografische locatie.</span><span class="sxs-lookup"><span data-stu-id="198fe-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="198fe-150">Bijvoorbeeld, als u Hallo kluisnaam ContosoKeyVault, Hallo Resourcegroepnaam ContosoResourceGroup en Hallo-locatie van Oost-Azië, typt u:</span><span class="sxs-lookup"><span data-stu-id="198fe-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="198fe-151">Hallo-uitvoer van deze opdracht worden de eigenschappen van Hallo sleutelkluis die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="198fe-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="198fe-152">Hallo twee belangrijkste eigenschappen zijn:</span><span class="sxs-lookup"><span data-stu-id="198fe-152">hello two most important properties are:</span></span>

* <span data-ttu-id="198fe-153">**naam**: In Hallo voorbeeld is dit ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="198fe-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="198fe-154">U gebruikt deze naam voor andere Sleutelkluis-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="198fe-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="198fe-155">**vaultUri**: In Hallo voorbeeld is dit https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="198fe-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="198fe-156">Toepassingen die via de REST API gebruikmaken van uw kluis, moeten deze URI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="198fe-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="198fe-157">Uw Azure-account is nu geautoriseerde tooperform bewerkingen op deze sleutel kluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="198fe-158">Tot dusver is er nog niemand anders gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="198fe-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="198fe-159">Een sleutel of geheim toohello sleutelkluis toevoegen</span><span class="sxs-lookup"><span data-stu-id="198fe-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="198fe-160">Als u toocreate Azure Sleutelkluis een softwarematig beveiligde sleutel voor u wilt, gebruikt u Hallo `az key create` opdracht in en typt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="198fe-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="198fe-161">Als u een bestaande sleutel in een .pem-bestand opgeslagen als een lokaal bestand in een bestand met de naam die u wilt dat tooupload tooAzure Sleutelkluis softkey.pem hebt, typt u na het tooimport Hallo sleutel uit Hallo Hallo. PEM-bestand, dat Hallo sleutel met software in Hallo Sleutelkluis-service beveiligt kan worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="198fe-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="198fe-162">U kunt nu naar Hallo sleutel dat u hebt gemaakt of geüpload tooAzure Sleutelkluis, met behulp van de URI verwijzen.</span><span class="sxs-lookup"><span data-stu-id="198fe-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="198fe-163">Gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways halen van de huidige versie Hallo en gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget deze specifieke versie.</span><span class="sxs-lookup"><span data-stu-id="198fe-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="198fe-164">tooadd een kluis geheime toohello, die een wachtwoord met de naam SQLPassword en die Hallo-waarde van Pa$ $w0rd tooAzure Sleutelkluis, type hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="198fe-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="198fe-165">U kunt nu verwijzen naar dit wachtwoord dat u met behulp van de URI tooAzure Sleutelkluis, toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="198fe-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="198fe-166">Gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways halen van de huidige versie Hallo en gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget deze specifieke versie.</span><span class="sxs-lookup"><span data-stu-id="198fe-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="198fe-167">We bekijken Hallo sleutel of geheim dat u zojuist hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="198fe-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="198fe-168">tooview uw sleutel, type:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="198fe-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="198fe-169">tooview uw geheime, type:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="198fe-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="198fe-170">Een toepassing registreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="198fe-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="198fe-171">Deze stap wordt doorgaans uitgevoerd door een ontwikkelaar op een afzonderlijke computer.</span><span class="sxs-lookup"><span data-stu-id="198fe-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="198fe-172">Er is geen specifieke tooAzure Sleutelkluis maar opgenomen, voor de volledigheid.</span><span class="sxs-lookup"><span data-stu-id="198fe-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="198fe-173">toocomplete hello zelfstudie, uw account, Hallo kluis en Hallo-toepassing die u in deze stap registreren wilt moeten alle liggen Hallo dezelfde Azure-directory.</span><span class="sxs-lookup"><span data-stu-id="198fe-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="198fe-174">Toepassingen die gebruikmaken van een sleutelkluis moeten een token van Azure Active Directory gebruiken om zich te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="198fe-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="198fe-175">toodo deze, Hallo eigenaar van de toepassing hello moet Hallo-toepassing eerst registreren in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="198fe-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="198fe-176">De eigenaar van de toepassing hello opgehaald Hallo na registratie Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="198fe-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="198fe-177">Een **toepassings-ID** (ook wel bekend als een Client-ID) en **verificatiesleutel** (ook wel bekend als Hallo gedeelde geheim genoemd).</span><span class="sxs-lookup"><span data-stu-id="198fe-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="198fe-178">Hallo-toepassing moet aanwezig zijn beide van deze waarden tooAzure Active Directory, tooget een token.</span><span class="sxs-lookup"><span data-stu-id="198fe-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="198fe-179">Hoe de toepassing hello is dit afhankelijk van de toepassing hello toodo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="198fe-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="198fe-180">Voor Hallo voorbeeldtoepassing voor Sleutelkluis stelt u de eigenaar van de toepassing hello deze waarden in Hallo app.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="198fe-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="198fe-181">tooregister hello toepassing in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="198fe-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="198fe-182">Meld u aan toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="198fe-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="198fe-183">Klik aan de linkerkant Hallo op **Azure Active Directory**, en selecteer vervolgens Hallo directory waarin u uw toepassing wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="198fe-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="198fe-184">Hallo moet u dezelfde map waarin zich hello Azure-abonnement waarmee u de sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="198fe-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="198fe-185">Als u niet welke directory dit weet is, klikt u op **instellingen**, identificeert Hallo-abonnement waarmee u de sleutelkluis hebt gemaakt en Opmerking Hallo-naam van Hallo-map weergegeven in de laatste kolom Hallo.</span><span class="sxs-lookup"><span data-stu-id="198fe-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="198fe-186">Klik op **TOEPASSINGEN**.</span><span class="sxs-lookup"><span data-stu-id="198fe-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="198fe-187">Als u geen apps tooyour directory zijn toegevoegd, ziet deze pagina alleen Hallo **een App toevoegen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="198fe-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="198fe-188">Klik op de koppeling Hallo of, u kunt ook klikken op Hallo **toevoegen** op Hallo opdrachtbalk klikken.</span><span class="sxs-lookup"><span data-stu-id="198fe-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="198fe-189">In Hallo **toepassing toevoegen** wizard op Hallo **wat wilt u wilt dat toodo?** pagina, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="198fe-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="198fe-190">Op Hallo **Vertel ons over uw toepassing** pagina, Geef een naam voor uw toepassing en selecteer **WEBTOEPASSING en/of WEB-API** (Hallo standaard).</span><span class="sxs-lookup"><span data-stu-id="198fe-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="198fe-191">Klik op volgende Hallo-pictogram.</span><span class="sxs-lookup"><span data-stu-id="198fe-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="198fe-192">Op Hallo **App-eigenschappen** pagina, geeft u Hallo **AANMELDINGS-URL** en **APP ID URI** voor uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="198fe-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="198fe-193">Als uw toepassing deze waarden niet heeft, kunt u voor deze stap zelf iets verzinnen (u kunt voor beide vakken bijvoorbeeld http://test1.contoso.com opgeven).</span><span class="sxs-lookup"><span data-stu-id="198fe-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="198fe-194">Het maakt niet uit als deze sites bestaan; Wat is het belangrijk is dat die Hallo app ID URI voor elke toepassing verschilt voor elke toepassing in uw directory.</span><span class="sxs-lookup"><span data-stu-id="198fe-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="198fe-195">Hallo directory gebruikt deze tekenreeks tooidentify uw app.</span><span class="sxs-lookup"><span data-stu-id="198fe-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="198fe-196">Klik op Hallo voltooid pictogram toosave uw wijzigingen in de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="198fe-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="198fe-197">Klik op de pagina snel starten Hallo **configureren**.</span><span class="sxs-lookup"><span data-stu-id="198fe-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="198fe-198">Schuif toohello **sleutels** sectie, selecteer Hallo duur en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="198fe-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="198fe-199">Hallo-pagina wordt vernieuwd en bevat nu een sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="198fe-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="198fe-200">U moet uw toepassing configureren met deze sleutelwaarde en Hallo **CLIENT-ID** waarde.</span><span class="sxs-lookup"><span data-stu-id="198fe-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="198fe-201">(Instructies voor deze configuratie zijn toepassingsspecifiek.)</span><span class="sxs-lookup"><span data-stu-id="198fe-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="198fe-202">Kopieer Hallo client-id-waarde van deze pagina wordt gebruikt in Hallo volgende stap tooset machtigingen voor uw kluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="198fe-203">Autoriseren hello toepassing toouse Hallo sleutel of geheim</span><span class="sxs-lookup"><span data-stu-id="198fe-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="198fe-204">tooauthorize hello toepassing tooaccess Hallo sleutel of geheim in Hallo kluis, gebruik Hallo `az keyvault set-policy` opdracht.</span><span class="sxs-lookup"><span data-stu-id="198fe-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="198fe-205">Bijvoorbeeld, als de kluisnaam van uw ContosoKeyVault en Hallo toepassing die u wilt dat tooauthorize client-ID van 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed heeft en u wilt dat tooauthorize Hallo toepassing toodecrypt en meld u met sleutels in uw kluis, voert Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="198fe-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="198fe-206">Als u dat dezelfde toepassing tooread geheimen tooauthorize in uw kluis wilt, voert u Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="198fe-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="198fe-207">Als u wilt dat toouse een hardware security module (HSM)</span><span class="sxs-lookup"><span data-stu-id="198fe-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="198fe-208">U kunt voor de zekerheid importeren of genereren van sleutels in hardware security modules (HSM's) die Hallo HSM-grens nooit verlaten.</span><span class="sxs-lookup"><span data-stu-id="198fe-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="198fe-209">Hallo HSM's zijn FIPS 140-2 Level 2-gevalideerde modules.</span><span class="sxs-lookup"><span data-stu-id="198fe-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="198fe-210">Als deze vereiste niet van toepassing tooyou, kunt u deze sectie overslaan en gaat u te[hello sleutelkluis en de bijbehorende sleutels en geheimen verwijderen](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="198fe-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="198fe-211">toocreate deze met HSM beveiligde sleutels, moet u een kluis abonnement die ondersteuning biedt voor met HSM beveiligde sleutels hebben.</span><span class="sxs-lookup"><span data-stu-id="198fe-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="198fe-212">Wanneer u Hallo keyvault maakt, voegt u de parameter 'sku' hello:</span><span class="sxs-lookup"><span data-stu-id="198fe-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="198fe-213">U kunt softwarematige beveiligde sleutels toevoegen (zoals eerder is weergegeven) en de HSM beveiligde sleutels toothis-kluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="198fe-214">toocreate een HSM beschermde sleutel set Hallo bestemming parameter too'HSM':</span><span class="sxs-lookup"><span data-stu-id="198fe-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="198fe-215">U kunt volgende opdracht tooimport een sleutel uit een .pem-bestand op uw computer hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="198fe-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="198fe-216">Deze opdracht wordt Hallo sleutel geïmporteerd in HSM's in Hallo Sleutelkluis-service:</span><span class="sxs-lookup"><span data-stu-id="198fe-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="198fe-217">de volgende opdracht Hallo importeert u een 'bring your own key' (BYOK)-pakket.</span><span class="sxs-lookup"><span data-stu-id="198fe-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="198fe-218">Hiermee kunt u uw sleutel in uw lokale HSM genereren en overdragen tooHSMs in Hallo Sleutelkluis-service, zonder Hallo sleutel Hallo HSM-grens verlaat:</span><span class="sxs-lookup"><span data-stu-id="198fe-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="198fe-219">Voor instructies over het gedetailleerde toogenerate dit BYOK-pakket Zie [hoe toouse HSM-Protected sleutels met Azure Sleutelkluis](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="198fe-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="198fe-220">Hallo sleutelkluis en de bijbehorende sleutels en geheimen verwijderen</span><span class="sxs-lookup"><span data-stu-id="198fe-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="198fe-221">Als u niet langer Hallo sleutelkluis en sleutel Hallo of het geheim die deze bevat, kunt u Hallo sleutelkluis verwijderen met behulp van Hallo `az keyvault delete` opdracht:</span><span class="sxs-lookup"><span data-stu-id="198fe-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="198fe-222">Of u kunt een volledige Azure-resourcegroep, waaronder Hallo sleutelkluis en alle andere resources die u hebt opgenomen in de groep verwijderen:</span><span class="sxs-lookup"><span data-stu-id="198fe-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="198fe-223">Andere opdrachten Azure platformoverschrijdende opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="198fe-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="198fe-224">Andere opdrachten die u wellicht nuttig voor het beheer van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="198fe-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="198fe-225">Met deze opdracht worden alle sleutels en geselecteerde eigenschappen weergegeven in een tabel:</span><span class="sxs-lookup"><span data-stu-id="198fe-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="198fe-226">AZ keyvault sleutellijst--naam sleutelkluis 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="198fe-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="198fe-227">Deze opdracht wordt een volledige lijst met eigenschappen voor de opgegeven sleutel Hallo weergegeven:</span><span class="sxs-lookup"><span data-stu-id="198fe-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="198fe-228">AZ keyvault sleutel weergeven--kluisnaam ContosoKeyVault--de naam 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="198fe-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="198fe-229">Met deze opdracht worden alle geheime namen en geselecteerde eigenschappen weergegeven in een tabel:</span><span class="sxs-lookup"><span data-stu-id="198fe-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="198fe-230">AZ keyvault geheime lijst--naam sleutelkluis 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="198fe-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="198fe-231">Hier volgt een voorbeeld van hoe u een specifieke sleutel tooremove:</span><span class="sxs-lookup"><span data-stu-id="198fe-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="198fe-232">AZ keyvault sleutel verwijderen--kluisnaam ContosoKeyVault--de naam 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="198fe-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="198fe-233">Hier volgt een voorbeeld van hoe u een specifiek geheim tooremove:</span><span class="sxs-lookup"><span data-stu-id="198fe-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="198fe-234">AZ keyvault geheim verwijderen--kluisnaam ContosoKeyVault--de naam 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="198fe-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="198fe-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="198fe-235">Next steps</span></span>
<span data-ttu-id="198fe-236">Zie voor een volledig overzicht van Azure CLI voor sleutelkluis-opdrachten, [Sleutelkluis CLI-verwijzing](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="198fe-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="198fe-237">Zie voor het programmeren van verwijzingen [Hallo ontwikkelaarshandleiding Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="198fe-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

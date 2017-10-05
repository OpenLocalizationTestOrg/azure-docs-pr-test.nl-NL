---
title: Beheren van Azure Sleutelkluis met CLI | Microsoft Docs
description: Gebruik deze handleiding om algemene taken in de Sleutelkluis automatiseren met behulp van de CLI 2.0
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
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="67b0c-103">Beheren met CLI 2.0 Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="67b0c-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="67b0c-104">Azure Sleutelkluis is beschikbaar in de meeste regio's.</span><span class="sxs-lookup"><span data-stu-id="67b0c-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="67b0c-105">Zie de pagina [Prijzen van Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="67b0c-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="67b0c-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="67b0c-106">Introduction</span></span>
<span data-ttu-id="67b0c-107">Gebruik deze handleiding om aan de slag te gaan met Azure Sleutelkluis en een geharde container (een kluis) in Azure te maken om cryptografiesleutels en geheimen op te slaan in Azure.</span><span class="sxs-lookup"><span data-stu-id="67b0c-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="67b0c-108">Dit helpt u bij het proces van het gebruik van Azure-opdrachtregelinterface voor Cross-Platform een kluis met een sleutel of het wachtwoord dat u vervolgens met een Azure-toepassing gebruiken kunt maken.</span><span class="sxs-lookup"><span data-stu-id="67b0c-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="67b0c-109">Deze vervolgens ziet u hoe een toepassing kunt vervolgens sleutel of het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="67b0c-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="67b0c-110">**Geschatte duur:** 20 minuten</span><span class="sxs-lookup"><span data-stu-id="67b0c-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="67b0c-111">Deze zelfstudie bevat geen instructies voor het schrijven van de Azure-toepassing of een van de stappen bevat, die wordt beschreven hoe een toepassing gebruik van een sleutel of geheim in de sleutelkluis toestemming geeft.</span><span class="sxs-lookup"><span data-stu-id="67b0c-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="67b0c-112">Deze zelfstudie maakt gebruik van de nieuwste Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="67b0c-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="67b0c-113">Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="67b0c-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67b0c-114">Vereisten</span><span class="sxs-lookup"><span data-stu-id="67b0c-114">Prerequisites</span></span>
<span data-ttu-id="67b0c-115">U hebt het volgende nodig om deze zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="67b0c-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="67b0c-116">Een abonnement op Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="67b0c-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="67b0c-117">Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="67b0c-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="67b0c-118">Opdrachtregelinterface versie 2.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="67b0c-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="67b0c-119">Installeer de nieuwste versie en verbinden om uw Azure-abonnement, Zie [installeren en configureren van de Azure platformoverschrijdende opdrachtregelinterface 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="67b0c-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="67b0c-120">Een toepassing die wordt geconfigureerd voor het gebruik van de sleutel of het wachtwoord dat u in deze zelfstudie maakt.</span><span class="sxs-lookup"><span data-stu-id="67b0c-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="67b0c-121">Er is een voorbeeldtoepassing beschikbaar in het [Microsoft Downloadcentrum](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="67b0c-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="67b0c-122">Zie het bijbehorende Leesmij-bestand voor instructies.</span><span class="sxs-lookup"><span data-stu-id="67b0c-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="67b0c-123">Help-informatie met Azure platformoverschrijdende opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="67b0c-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="67b0c-124">Deze zelfstudie wordt ervan uitgegaan dat u bekend met de opdrachtregelinterface (Bash, Terminal-opdrachtprompt bent)</span><span class="sxs-lookup"><span data-stu-id="67b0c-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="67b0c-125">De--help- of -h parameter kan worden gebruikt om help voor specifieke opdrachten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="67b0c-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="67b0c-126">U kunt ook de azure-help [opdracht] [opties] indeling kan ook worden gebruikt om de dezelfde informatie te retourneren.</span><span class="sxs-lookup"><span data-stu-id="67b0c-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="67b0c-127">Bijvoorbeeld de volgende opdrachten uit alle dezelfde informatie geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="67b0c-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="67b0c-128">Raadpleeg bij twijfel over de parameters die door een opdracht die nodig zijn om te helpen met behulp van--help, -h of az help [opdracht].</span><span class="sxs-lookup"><span data-stu-id="67b0c-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="67b0c-129">U kunt ook de volgende zelfstudies om vertrouwd te raken met Azure Resource Manager in Azure platformoverschrijdende opdrachtregelinterface lezen:</span><span class="sxs-lookup"><span data-stu-id="67b0c-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="67b0c-130">Azure CLI installeren</span><span class="sxs-lookup"><span data-stu-id="67b0c-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="67b0c-131">Aan de slag met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="67b0c-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="67b0c-132">Verbinding maken met uw abonnementen</span><span class="sxs-lookup"><span data-stu-id="67b0c-132">Connect to your subscriptions</span></span>
<span data-ttu-id="67b0c-133">Meld u aan met een organisatie-account met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="67b0c-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="67b0c-134">of als u wilt zich aanmelden door interactief typen</span><span class="sxs-lookup"><span data-stu-id="67b0c-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="67b0c-135">Als u meerdere abonnementen hebt en u een specifiek abonnement voor Azure Sleutelkluis wilt gebruiken, typt u het volgende om de abonnementen voor uw account weer te geven:</span><span class="sxs-lookup"><span data-stu-id="67b0c-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="67b0c-136">Typ vervolgens het volgende om het abonnement op te geven dat u wilt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="67b0c-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="67b0c-137">Zie voor meer informatie over het configureren van Azure platformoverschrijdende opdrachtregelinterface [Azure CLI installeren](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="67b0c-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="67b0c-138">Een nieuwe resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="67b0c-138">Create a new resource group</span></span>
<span data-ttu-id="67b0c-139">Wanneer u Azure Resource Manager gebruikt, worden alle gerelateerde resources gemaakt binnen een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="67b0c-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="67b0c-140">We gaan een nieuwe resourcegroep 'ContosoResourceGroup' maken voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="67b0c-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="67b0c-141">De eerste parameter is de naam van resourcegroep en de tweede parameter is de locatie.</span><span class="sxs-lookup"><span data-stu-id="67b0c-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="67b0c-142">Gebruik de opdracht voor locatie, `az account list-locations` om te bepalen hoe een alternatieve locatie op de in dit voorbeeld opgeven.</span><span class="sxs-lookup"><span data-stu-id="67b0c-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="67b0c-143">Als u meer informatie nodig hebt, typt: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="67b0c-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="67b0c-144">De registerbronprovider is Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="67b0c-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="67b0c-145">Zorg ervoor dat Sleutelkluis-resourceprovider is geregistreerd in uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="67b0c-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="67b0c-146">Dit hoeft slechts één keer per abonnement worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="67b0c-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="67b0c-147">Een sleutelkluis maken</span><span class="sxs-lookup"><span data-stu-id="67b0c-147">Create a key vault</span></span>
<span data-ttu-id="67b0c-148">Gebruik de `az keyvault create` opdracht om een sleutelkluis te maken.</span><span class="sxs-lookup"><span data-stu-id="67b0c-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="67b0c-149">Dit script heeft drie verplichte parameters: de naam van een resource-groep, de naam van een sleutelkluis en de geografische locatie.</span><span class="sxs-lookup"><span data-stu-id="67b0c-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="67b0c-150">Bijvoorbeeld, als u de kluisnaam ContosoKeyVault gebruikt, de naam van de resourcegroep van ContosoResourceGroup en de locatie van Oost-Azië, typt u:</span><span class="sxs-lookup"><span data-stu-id="67b0c-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="67b0c-151">De uitvoer van deze opdracht worden de eigenschappen van de sleutelkluis die u zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="67b0c-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="67b0c-152">De twee belangrijkste eigenschappen zijn:</span><span class="sxs-lookup"><span data-stu-id="67b0c-152">The two most important properties are:</span></span>

* <span data-ttu-id="67b0c-153">**naam**: In het voorbeeld is dit ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="67b0c-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="67b0c-154">U gebruikt deze naam voor andere Sleutelkluis-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="67b0c-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="67b0c-155">**vaultUri**: In het voorbeeld is dit https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="67b0c-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="67b0c-156">Toepassingen die via de REST API gebruikmaken van uw kluis, moeten deze URI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67b0c-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="67b0c-157">Uw Azure-account is nu gemachtigd om alle bewerkingen op deze sleutelkluis uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="67b0c-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="67b0c-158">Tot dusver is er nog niemand anders gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="67b0c-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="67b0c-159">Een sleutel of geheim toevoegen aan de sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="67b0c-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="67b0c-160">Als u wilt dat Azure Sleutelkluis een softwarematig beveiligde sleutel voor u te maken, gebruikt u de `az key create` opdracht in en typt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="67b0c-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="67b0c-161">Echter, hebt u een bestaande sleutel in een .pem-bestand opgeslagen als een lokaal bestand in een bestand met de naam softkey.pem die u wilt uploaden naar Azure Sleutelkluis, typt u het volgende als u wilt importeren van de sleutel van de. PEM-bestand dat de sleutel met software in de Sleutelkluis-service beveiligt:</span><span class="sxs-lookup"><span data-stu-id="67b0c-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="67b0c-162">U kunt nu naar de sleutel die u hebt gemaakt of geüpload naar Azure Sleutelkluis, met behulp van de URI verwijzen.</span><span class="sxs-lookup"><span data-stu-id="67b0c-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="67b0c-163">Gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** altijd de huidige versie en gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** voor deze specifieke versie.</span><span class="sxs-lookup"><span data-stu-id="67b0c-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="67b0c-164">Als u wilt een geheim toevoegen aan de kluis, die een wachtwoord met de naam SQLPassword en die de waarde van Pa$ $w0rd voor Azure Sleutelkluis, typt u het volgende:</span><span class="sxs-lookup"><span data-stu-id="67b0c-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="67b0c-165">Als u nu naar het wachtwoord wilt verwijzen dat u hebt toegevoegd aan Azure Sleutelkluis, kunt u de URI van het wachtwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="67b0c-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="67b0c-166">Gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword** om altijd de huidige versie op te halen en gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** om deze specifieke versie op te halen.</span><span class="sxs-lookup"><span data-stu-id="67b0c-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="67b0c-167">We bekijken de sleutel of geheim dat u zojuist hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="67b0c-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="67b0c-168">Als u de sleutel wilt weergeven, typt u: `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="67b0c-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="67b0c-169">Als u het geheim wilt weergeven, typt u: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="67b0c-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="67b0c-170">Een toepassing registreren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="67b0c-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="67b0c-171">Deze stap wordt doorgaans uitgevoerd door een ontwikkelaar op een afzonderlijke computer.</span><span class="sxs-lookup"><span data-stu-id="67b0c-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="67b0c-172">Het is niet specifiek voor Azure Sleutelkluis maar opgenomen, voor de volledigheid.</span><span class="sxs-lookup"><span data-stu-id="67b0c-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67b0c-173">Uw account, de kluis en de toepassing die u in deze stap registreert moet allemaal in dezelfde Azure-directory bevinden om de zelfstudie te kunnen voltooien.</span><span class="sxs-lookup"><span data-stu-id="67b0c-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="67b0c-174">Toepassingen die gebruikmaken van een sleutelkluis moeten een token van Azure Active Directory gebruiken om zich te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="67b0c-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="67b0c-175">Hiervoor moet de eigenaar van de toepassing deze eerst registreren bij Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="67b0c-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="67b0c-176">Aan het eind van het registratieproces ontvangt de eigenaar de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="67b0c-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="67b0c-177">Een **toepassings-ID** (ook wel een client-id genoemd) en een **verificatiesleutel** (ook wel het gedeelde geheim genoemd).</span><span class="sxs-lookup"><span data-stu-id="67b0c-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="67b0c-178">De toepassing moet van deze waarden aanbieden aan Azure Active Directory een token ophalen.</span><span class="sxs-lookup"><span data-stu-id="67b0c-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="67b0c-179">Hoe de toepassing is geconfigureerd om dit te doen, is afhankelijk van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="67b0c-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="67b0c-180">In de voorbeeldtoepassing voor Sleutelkluis configureert de eigenaar van de toepassing deze waarden in het bestand app.config.</span><span class="sxs-lookup"><span data-stu-id="67b0c-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="67b0c-181">De toepassing registreren in Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="67b0c-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="67b0c-182">Meld u aan bij Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="67b0c-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="67b0c-183">Klik aan de linkerkant op **Azure Active Directory**, en selecteer vervolgens de directory waarin u uw toepassing wilt registreren.</span><span class="sxs-lookup"><span data-stu-id="67b0c-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="67b0c-184">U moet de directory waarin het Azure-abonnement waarmee u de sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="67b0c-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="67b0c-185">Als u niet weet welke directory dit is, klikt u op **Instellingen**, identificeert u het abonnement waarmee u de sleutelkluis hebt gemaakt en noteert u de directorynaam die in de laatste kolom wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="67b0c-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="67b0c-186">Klik op **TOEPASSINGEN**.</span><span class="sxs-lookup"><span data-stu-id="67b0c-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="67b0c-187">Als er zijn geen apps aan uw directory zijn toegevoegd, deze pagina alleen wordt weergegeven de **een App toevoegen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="67b0c-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="67b0c-188">Klik op de koppeling of u kunt ook klikken op de **toevoegen** op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="67b0c-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="67b0c-189">In de wizard **TOEPASSING TOEVOEGEN** klikt u op de pagina **What do you want to do?** (Wat wilt u doen?) op **Add an application my organization is developing** (Een toepassing toevoegen die door mijn organisatie wordt ontwikkeld).</span><span class="sxs-lookup"><span data-stu-id="67b0c-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="67b0c-190">Op de **Vertel ons over uw toepassing** pagina, Geef een naam voor uw toepassing en selecteer **WEBTOEPASSING en/of WEB-API** (de standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="67b0c-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="67b0c-191">Klik op het volgende pictogram.</span><span class="sxs-lookup"><span data-stu-id="67b0c-191">Click the Next icon.</span></span>
6. <span data-ttu-id="67b0c-192">Geef op de pagina **App-eigenschappen** de **AANMELDINGS-URL** en **APP ID URI** (URI VAN DE APP-ID) voor uw webtoepassing op.</span><span class="sxs-lookup"><span data-stu-id="67b0c-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="67b0c-193">Als uw toepassing deze waarden niet heeft, kunt u voor deze stap zelf iets verzinnen (u kunt voor beide vakken bijvoorbeeld http://test1.contoso.com opgeven).</span><span class="sxs-lookup"><span data-stu-id="67b0c-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="67b0c-194">Het maakt niet uit of deze sites bestaan. Belangrijk is dat voor elke toepassing in uw directory een andere URI van de app-id wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="67b0c-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="67b0c-195">De directory gebruikt deze tekenreeks om uw app te identificeren.</span><span class="sxs-lookup"><span data-stu-id="67b0c-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="67b0c-196">Klik op het pictogram voltooid Sla uw wijzigingen in de wizard.</span><span class="sxs-lookup"><span data-stu-id="67b0c-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="67b0c-197">Klik op de pagina Quick Start op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="67b0c-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="67b0c-198">Schuif naar de sectie **sleutels**, selecteer de duur en klik vervolgens op **OPSLAAN**.</span><span class="sxs-lookup"><span data-stu-id="67b0c-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="67b0c-199">De pagina wordt vernieuwd en bevat nu een sleutelwaarde.</span><span class="sxs-lookup"><span data-stu-id="67b0c-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="67b0c-200">U moet nu uw toepassing configureren met deze sleutelwaarde en de waarde **CLIENT-ID**.</span><span class="sxs-lookup"><span data-stu-id="67b0c-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="67b0c-201">(Instructies voor deze configuratie zijn toepassingsspecifiek.)</span><span class="sxs-lookup"><span data-stu-id="67b0c-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="67b0c-202">Kopieer de client-id-waarde op deze pagina. Deze waarde gebruikt in de volgende stap om machtigingen voor uw kluis in te stellen.</span><span class="sxs-lookup"><span data-stu-id="67b0c-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="67b0c-203">De toepassing toestemming geven om de sleutel of het geheim te gebruiken</span><span class="sxs-lookup"><span data-stu-id="67b0c-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="67b0c-204">Voor het autoriseren van de toepassing toegang krijgen tot de sleutel of geheim in de kluis, gebruikt u de `az keyvault set-policy` opdracht.</span><span class="sxs-lookup"><span data-stu-id="67b0c-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="67b0c-205">Bijvoorbeeld, als de kluisnaam van uw ContosoKeyVault is en de toepassing die u wilt machtigen client-ID van 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed heeft en u machtigen van de toepassing wilt te ontsleutelen en meld u aan met de sleutels in uw kluis, voert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="67b0c-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="67b0c-206">Als u dezelfde toepassing wilt autoriseren voor het lezen van geheimen in uw kluis, voert u de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="67b0c-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="67b0c-207">Als u een Hardware Security Module (HSM) wilt gebruiken</span><span class="sxs-lookup"><span data-stu-id="67b0c-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="67b0c-208">Voor de zekerheid kunt u sleutels in HSM's (Hardware Security Module) importeren of genereren die de HSM-grens nooit verlaten.</span><span class="sxs-lookup"><span data-stu-id="67b0c-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="67b0c-209">De HSM's zijn FIPS 140-2 Level 2-gevalideerde modules.</span><span class="sxs-lookup"><span data-stu-id="67b0c-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="67b0c-210">Als deze vereiste niet van toepassing is op u, kunt u deze sectie overslaan om naar [De sleutelkluis en de bijbehorende sleutels en geheimen verwijderen](#delete-the-key-vault-and-associated-keys-and-secrets) te gaan.</span><span class="sxs-lookup"><span data-stu-id="67b0c-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="67b0c-211">U moet een kluis-abonnement dat ondersteuning biedt voor met HSM beveiligde sleutels hebben voor het maken van deze met HSM beveiligde sleutels.</span><span class="sxs-lookup"><span data-stu-id="67b0c-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="67b0c-212">Wanneer u de keyvault maakt, voegt u de parameter 'sku':</span><span class="sxs-lookup"><span data-stu-id="67b0c-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="67b0c-213">U kunt softwarematige beveiligde sleutels (zoals hiervoor) en met HSM beveiligde sleutels toevoegen aan deze kluis.</span><span class="sxs-lookup"><span data-stu-id="67b0c-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="67b0c-214">Stel de doel-parameter op 'HSM' voor het maken van een HSM beveiligde sleutel:</span><span class="sxs-lookup"><span data-stu-id="67b0c-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="67b0c-215">U kunt de volgende opdracht gebruiken voor het importeren van een sleutel van een .pem-bestand op uw computer.</span><span class="sxs-lookup"><span data-stu-id="67b0c-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="67b0c-216">Met deze opdracht wordt de sleutel geïmporteerd in HSM's in de Sleutelkluis-service:</span><span class="sxs-lookup"><span data-stu-id="67b0c-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="67b0c-217">Met de volgende opdracht wordt een BYOK-pakket (Bring Your Own Key) geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="67b0c-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="67b0c-218">Hiermee kunt u de sleutel in uw lokale HSM genereren en overdragen naar HSM's in de Sleutelkluis-service, zonder dat de sleutel de HSM-grens verlaat:</span><span class="sxs-lookup"><span data-stu-id="67b0c-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="67b0c-219">Zie voor meer instructies over hoe dit BYOK-pakket te genereren gedetailleerde, [HSM-Protected sleutels gebruiken met Azure Key Vault](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="67b0c-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="67b0c-220">De sleutelkluis en de bijbehorende sleutels en geheimen verwijderen</span><span class="sxs-lookup"><span data-stu-id="67b0c-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="67b0c-221">Als u de sleutelkluis en de sleutel of geheim niet meer nodig hebt, kunt u de sleutelkluis verwijderen met behulp van de `az keyvault delete` opdracht:</span><span class="sxs-lookup"><span data-stu-id="67b0c-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="67b0c-222">U kunt ook een volledige Azure-resourcegroep verwijderen. Deze bevat de sleutelkluis en alle andere resources die u hebt opgenomen in de groep:</span><span class="sxs-lookup"><span data-stu-id="67b0c-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="67b0c-223">Andere opdrachten Azure platformoverschrijdende opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="67b0c-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="67b0c-224">Andere opdrachten die u wellicht nuttig voor het beheer van Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="67b0c-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="67b0c-225">Met deze opdracht worden alle sleutels en geselecteerde eigenschappen weergegeven in een tabel:</span><span class="sxs-lookup"><span data-stu-id="67b0c-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="67b0c-226">AZ keyvault sleutellijst--naam sleutelkluis 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="67b0c-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="67b0c-227">Deze opdracht wordt een volledige lijst met eigenschappen voor de opgegeven sleutel weergegeven:</span><span class="sxs-lookup"><span data-stu-id="67b0c-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="67b0c-228">AZ keyvault sleutel weergeven--kluisnaam ContosoKeyVault--de naam 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="67b0c-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="67b0c-229">Met deze opdracht worden alle geheime namen en geselecteerde eigenschappen weergegeven in een tabel:</span><span class="sxs-lookup"><span data-stu-id="67b0c-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="67b0c-230">AZ keyvault geheime lijst--naam sleutelkluis 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="67b0c-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="67b0c-231">Hier volgt een voorbeeld van hoe u een specifieke sleutel verwijdert:</span><span class="sxs-lookup"><span data-stu-id="67b0c-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="67b0c-232">AZ keyvault sleutel verwijderen--kluisnaam ContosoKeyVault--de naam 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="67b0c-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="67b0c-233">Hier volgt een voorbeeld van hoe u een specifiek geheim verwijdert:</span><span class="sxs-lookup"><span data-stu-id="67b0c-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="67b0c-234">AZ keyvault geheim verwijderen--kluisnaam ContosoKeyVault--de naam 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="67b0c-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="67b0c-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="67b0c-235">Next steps</span></span>
<span data-ttu-id="67b0c-236">Zie voor een volledig overzicht van Azure CLI voor sleutelkluis-opdrachten, [Sleutelkluis CLI-verwijzing](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="67b0c-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="67b0c-237">Zie de [Ontwikkelaarshandleiding voor Azure Key Vault](key-vault-developers-guide.md) voor het programmeren van verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="67b0c-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

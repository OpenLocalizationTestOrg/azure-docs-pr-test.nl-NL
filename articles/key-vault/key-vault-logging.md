---
title: Logboekregistratie van Azure Sleutelkluis | Microsoft Docs
description: Deze zelfstudie helpt u op weg met de logboekregistratie van Azure Sleutelkluis.
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: e9a4f16f048833dab49f7db79892fe47a5aeff37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="3196b-103">Logboekregistratie van Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="3196b-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="3196b-104">Azure Sleutelkluis is beschikbaar in de meeste regio's.</span><span class="sxs-lookup"><span data-stu-id="3196b-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="3196b-105">Zie de pagina [Prijzen van Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3196b-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="3196b-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="3196b-106">Introduction</span></span>
<span data-ttu-id="3196b-107">Nadat u een of meer sleutelkluizen hebt gemaakt, wilt u wellicht controleren hoe en wanneer uw sleutelkluizen toegankelijk zijn en voor wie.</span><span class="sxs-lookup"><span data-stu-id="3196b-107">After you have created one or more key vaults, you will likely want to monitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="3196b-108">U kunt dit doen door logboekregistratie in te schakelen voor Sleutelkluis. Hierbij wordt de informatie opgeslagen in een Azure-opslagaccount dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3196b-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="3196b-109">Er wordt automatisch een nieuwe container met de naam **insights-logboeken-auditevent** gemaakt voor het opgegeven opslagaccount en u kunt hetzelfde opslagaccount gebruiken voor het verzamelen van logboeken voor meerdere sleutelkluizen.</span><span class="sxs-lookup"><span data-stu-id="3196b-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="3196b-110">U kunt uw logboekgegevens maximaal tien minuten nadat de sleutelkluisbewerking is uitgevoerd, bekijken.</span><span class="sxs-lookup"><span data-stu-id="3196b-110">You can access your logging information at most, 10 minutes after the key vault operation.</span></span> <span data-ttu-id="3196b-111">In de meeste gevallen gaat het echter veel sneller.</span><span class="sxs-lookup"><span data-stu-id="3196b-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="3196b-112">Het is aan u om uw logboeken in uw opslagaccount te beheren:</span><span class="sxs-lookup"><span data-stu-id="3196b-112">It's up to you to manage your logs in your storage account:</span></span>

* <span data-ttu-id="3196b-113">Gebruik standaardmethoden van Azure voor toegangsbeheer om uw logboeken te beveiligen door het aantal gebruikers te beperken dat toegang heeft tot de logboeken.</span><span class="sxs-lookup"><span data-stu-id="3196b-113">Use standard Azure access control methods to secure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="3196b-114">Verwijder de logboeken die u niet meer in uw opslagaccount wilt bewaren.</span><span class="sxs-lookup"><span data-stu-id="3196b-114">Delete logs that you no longer want to keep in your storage account.</span></span>

<span data-ttu-id="3196b-115">Deze zelfstudie helpt u op weg met de logboekregistratie van Azure Sleutelkluis, het maken van uw opslagaccount, het inschakelen van logboekregistratie en het interpreteren van de logboekgegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="3196b-115">Use this tutorial to help you get started with Azure Key Vault logging, to create your storage account, enable logging, and interpret the logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="3196b-116">Deze zelfstudie bevat geen instructies voor het maken van sleutelkluizen, sleutels of geheimen.</span><span class="sxs-lookup"><span data-stu-id="3196b-116">This tutorial does not include instructions for how to create key vaults, keys, or secrets.</span></span> <span data-ttu-id="3196b-117">Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3196b-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="3196b-118">Zie [deze equivalente zelfstudie](key-vault-manage-with-cli2.md) voor instructies voor het maken van een platformonafhankelijke opdrachtregelinterface.</span><span class="sxs-lookup"><span data-stu-id="3196b-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="3196b-119">Het is momenteel niet mogelijk om Azure Sleutelkluis in de Azure-portal te configureren.</span><span class="sxs-lookup"><span data-stu-id="3196b-119">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="3196b-120">Gebruik in plaats daarvan deze instructies voor Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3196b-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="3196b-121">Zie [Wat is Azure Key Vault?](key-vault-whatis.md) voor algemene informatie over Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="3196b-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3196b-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3196b-122">Prerequisites</span></span>
<span data-ttu-id="3196b-123">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="3196b-123">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="3196b-124">Een bestaande sleutelkluis die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3196b-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="3196b-125">Azure PowerShell, **versie 1.0.1 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="3196b-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="3196b-126">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) om Azure PowerShell te installeren en te koppelen aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3196b-126">To install Azure PowerShell and associate it with your Azure subscription, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="3196b-127">Als u Azure PowerShell al hebt geïnstalleerd, maar niet weet welke versie u hebt, typt u `(Get-Module azure -ListAvailable).Version` in de Azure PowerShell-console.</span><span class="sxs-lookup"><span data-stu-id="3196b-127">If you have already installed Azure PowerShell and do not know the version, from the Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="3196b-128">Voldoende opslagruimte op Azure voor uw Sleutelkluis-logboeken.</span><span class="sxs-lookup"><span data-stu-id="3196b-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="3196b-129"><a id="connect"></a>Verbinding maken met uw abonnementen</span><span class="sxs-lookup"><span data-stu-id="3196b-129"><a id="connect"></a>Connect to your subscriptions</span></span>
<span data-ttu-id="3196b-130">Start een Azure PowerShell-sessie en gebruik de volgende opdracht om u aan te melden bij uw Azure-account:</span><span class="sxs-lookup"><span data-stu-id="3196b-130">Start an Azure PowerShell session and sign in to your Azure account with the following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="3196b-131">Voer in het pop-upvenster in de browser uw gebruikersnaam en wachtwoord voor uw Azure-account in.</span><span class="sxs-lookup"><span data-stu-id="3196b-131">In the pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="3196b-132">Azure PowerShell haalt alle abonnementen op die zijn gekoppeld aan dit account en gebruikt standaard het eerste.</span><span class="sxs-lookup"><span data-stu-id="3196b-132">Azure PowerShell will get all the subscriptions that are associated with this account and by default, uses the first one.</span></span>

<span data-ttu-id="3196b-133">Als u meerdere abonnementen hebt, moet u wellicht specifiek opgeven welk abonnement is gebruikt voor het maken van uw Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="3196b-133">If you have multiple subscriptions, you might have to specify a specific one that was used to create your Azure Key Vault.</span></span> <span data-ttu-id="3196b-134">Typ het volgende als u de abonnementen voor uw account wilt zien:</span><span class="sxs-lookup"><span data-stu-id="3196b-134">Type the following to see the subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="3196b-135">Geef vervolgens op welk abonnement is gekoppeld aan de sleutelkluis waarvoor u logboekregistratie wilt inschakelen. Typ:</span><span class="sxs-lookup"><span data-stu-id="3196b-135">Then, to specify the subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="3196b-136">Dit is een belangrijke stap, die met name handig is als er meerdere abonnementen zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="3196b-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="3196b-137">Mogelijk wordt er een fout weergegeven voor het registreren van Microsoft.Insights als deze stap wordt overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3196b-137">You may receive an error to register Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="3196b-138">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor meer informatie over het configureren van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3196b-138">For more information about configuring Azure PowerShell, see  [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="3196b-139"><a id="storage"></a>Een nieuw opslagaccount voor uw logboeken maken</span><span class="sxs-lookup"><span data-stu-id="3196b-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="3196b-140">Hoewel u een bestaand opslagaccount voor uw logboeken kunt gebruiken, maken we hier een nieuw opslagaccount, speciaal voor Sleutelkluis-logboeken.</span><span class="sxs-lookup"><span data-stu-id="3196b-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated to Key Vault logs.</span></span> <span data-ttu-id="3196b-141">Voor het gemak slaan we de details op in een variabele met de naam **sa**. Deze moeten we later namelijk opgeven.</span><span class="sxs-lookup"><span data-stu-id="3196b-141">For convenience for when we have to specify this later, we'll store the details into a variable named **sa**.</span></span>

<span data-ttu-id="3196b-142">En om het ons nog gemakkelijker te maken, gebruiken we de resourcegroep die de sleutelkluis bevat.</span><span class="sxs-lookup"><span data-stu-id="3196b-142">For additional ease of management, we'll also use the same resource group as the one that contains our key vault.</span></span> <span data-ttu-id="3196b-143">In de [zelfstudie Aan de slag](key-vault-get-started.md) heeft deze resourcegroep de naam **ContosoResourceGroup** en we gebruiken hier ook de locatie Oost-Azië.</span><span class="sxs-lookup"><span data-stu-id="3196b-143">From the [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue to use the East Asia location.</span></span> <span data-ttu-id="3196b-144">Vervang deze waarden voor uzelf, indien van toepassing:</span><span class="sxs-lookup"><span data-stu-id="3196b-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="3196b-145">Als u een bestaand opslagaccount gebruikt, moet hiervoor hetzelfde abonnement worden gebruikt als voor uw sleutelkluis. Ook moet het opslagaccount gebruikmaken van het Resource Manager-implementatiemodel, niet van het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="3196b-145">If you decide to use an existing storage account, it must use the same subscription as your key vault and it must use the Resource Manager deployment model, rather than the Classic deployment model.</span></span>
>
>

## <span data-ttu-id="3196b-146"><a id="identify"></a>De sleutelkluis voor uw logboeken identificeren</span><span class="sxs-lookup"><span data-stu-id="3196b-146"><a id="identify"></a>Identify the key vault for your logs</span></span>
<span data-ttu-id="3196b-147">In de zelfstudie Aan de slag is de naam van de sleutelkluis **ContosoKeyVault**. We gaan deze naam ook hier gebruiken en de details in een variabele met de naam **kv** opslaan:</span><span class="sxs-lookup"><span data-stu-id="3196b-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue to use that name and store the details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="3196b-148"><a id="enable"></a>Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="3196b-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="3196b-149">Als u logboekregistratie wilt inschakelen voor Sleutelkluis, gebruikt u de cmdlet Set-AzureRmDiagnosticSetting, samen met de variabelen die we voor ons nieuwe opslagaccount en onze sleutelkluis hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3196b-149">To enable logging for Key Vault, we'll use the Set-AzureRmDiagnosticSetting cmdlet, together with the variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="3196b-150">We moeten de markering **-Ingeschakeld** instellen op **$true** en de categorie instellen op AuditEvent (de enige categorie voor logboekregistratie van Key Vault):</span><span class="sxs-lookup"><span data-stu-id="3196b-150">We'll also set the **-Enabled** flag to **$true** and set the category to AuditEvent (the only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="3196b-151">De uitvoer hiervoor bevat het volgende:</span><span class="sxs-lookup"><span data-stu-id="3196b-151">The output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="3196b-152">Hiermee bevestigt u dat logboekregistratie nu is ingeschakeld voor uw sleutelkluis, waarbij de informatie wordt opgeslagen in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3196b-152">This confirms that logging is now enabled for your key vault, saving information to your storage account.</span></span>

<span data-ttu-id="3196b-153">U kunt eventueel ook een retentiebeleid instellen voor uw logboeken, zodat oudere logboeken automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3196b-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="3196b-154">Stel bijvoorbeeld een retentiebeleid in met behulp van de vlag **- RetentionEnabled** ingesteld op **$true** en stel de parameter **- RetentionInDays** in op **90**, zodat logboeken die ouder zijn dan 90 dagen automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3196b-154">For example, set retention policy using **-RetentionEnabled** flag to **$true** and set **-RetentionInDays** parameter to **90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="3196b-155">Wat wordt in het logboek vastgelegd?</span><span class="sxs-lookup"><span data-stu-id="3196b-155">What's logged:</span></span>

* <span data-ttu-id="3196b-156">Alle geverifieerde REST-API-aanvragen worden vastgelegd, ook mislukte aanvragen als gevolg van toegangsmachtigingen, systeemfouten of ongeldige aanvragen.</span><span class="sxs-lookup"><span data-stu-id="3196b-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="3196b-157">Bewerkingen voor de sleutelkluis zelf, zoals het maken, verwijderen en instellen van het toegangsbeleid voor sleutelkluizen, en het bijwerken van de kenmerken van sleutelkluizen, zoals tags.</span><span class="sxs-lookup"><span data-stu-id="3196b-157">Operations on the key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="3196b-158">Bewerkingen voor sleutels en geheimen in de sleutelkluis, zoals het maken, wijzigen of verwijderen van deze sleutels of geheimen; bewerkingen zoals het ondertekenen, controleren, versleutelen, ontsleutelen, inpakken en uitpakken van sleutels, het ophalen van geheimen en het weergeven van sleutels, geheimen en hun versies.</span><span class="sxs-lookup"><span data-stu-id="3196b-158">Operations on keys and secrets in the key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="3196b-159">Niet-geverifieerde aanvragen die in een 401-respons resulteren.</span><span class="sxs-lookup"><span data-stu-id="3196b-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="3196b-160">Dit zijn bijvoorbeeld aanvragen die geen Bearer-token hebben, ongeldige of verlopen aanvragen of aanvragen met een ongeldig token.</span><span class="sxs-lookup"><span data-stu-id="3196b-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="3196b-161"><a id="access"></a>Toegang tot uw logboeken</span><span class="sxs-lookup"><span data-stu-id="3196b-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="3196b-162">Sleutelkluis-logboeken worden opgeslagen in de container **insights-logs-auditevent** in het opslagaccount dat u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3196b-162">Key vault logs are stored in the **insights-logs-auditevent** container in the storage account you provided.</span></span> <span data-ttu-id="3196b-163">Als u alle blobs in deze container wilt weergeven, typt u:</span><span class="sxs-lookup"><span data-stu-id="3196b-163">To list all the blobs in this container, type:</span></span>

<span data-ttu-id="3196b-164">Maak eerst een variabele voor de containernaam.</span><span class="sxs-lookup"><span data-stu-id="3196b-164">First, create a variable for the container name.</span></span> <span data-ttu-id="3196b-165">Deze wordt gebruikt in de rest van de procedure.</span><span class="sxs-lookup"><span data-stu-id="3196b-165">This will be used throughout the rest of the walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="3196b-166">Als u alle blobs in deze container wilt weergeven, typt u:</span><span class="sxs-lookup"><span data-stu-id="3196b-166">To list all the blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="3196b-167">De uitvoer ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="3196b-167">The output will look something similar to this:</span></span>

<span data-ttu-id="3196b-168">**Container-URI: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="3196b-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="3196b-169">**Naam**</span><span class="sxs-lookup"><span data-stu-id="3196b-169">**Name**</span></span>

- - -
<span data-ttu-id="3196b-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="3196b-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="3196b-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="3196b-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="3196b-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="3196b-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="3196b-173">Zoals u in deze uitvoer kunt zien, hebben de blobs de volgende naamgevingsregels: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="3196b-173">As you can see from this output, the blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="3196b-174">De datum- en tijdwaarden maken gebruik van UTC.</span><span class="sxs-lookup"><span data-stu-id="3196b-174">The date and time values use UTC.</span></span>

<span data-ttu-id="3196b-175">Aangezien hetzelfde opslagaccount kan worden gebruikt voor het verzamelen van logboeken voor meerdere resources, is de volledige resource-id in de blobnaam zeer handig voor toegang tot of het downloaden van alleen de blobs die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="3196b-175">Because the same storage account can be used to collect logs for multiple resources, the full resource ID in the blob name is very useful to access or download just the blobs that you need.</span></span> <span data-ttu-id="3196b-176">Maar eerst laten we zien hoe u alle blobs kunt downloaden.</span><span class="sxs-lookup"><span data-stu-id="3196b-176">But before we do that, we'll first cover how to download all the blobs.</span></span>

<span data-ttu-id="3196b-177">Maak eerst een map waarin u de blobs wilt downloaden.</span><span class="sxs-lookup"><span data-stu-id="3196b-177">First, create a folder to download the blobs.</span></span> <span data-ttu-id="3196b-178">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3196b-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="3196b-179">Haal vervolgens een lijst met alle blobs op:</span><span class="sxs-lookup"><span data-stu-id="3196b-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="3196b-180">Sluis deze lijst via 'Get-AzureStorageBlobContent' door om de blobs in de doelmap te downloaden:</span><span class="sxs-lookup"><span data-stu-id="3196b-180">Pipe this list through 'Get-AzureStorageBlobContent' to download the blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="3196b-181">Wanneer u deze tweede opdracht uitvoert maakt het **/** scheidingsteken in de blobnamen een volledige mapstructuur onder de doelmap. Deze structuur wordt gebruikt voor het downloaden en opslaan van de blobs als bestanden.</span><span class="sxs-lookup"><span data-stu-id="3196b-181">When you run this second command, the **/** delimiter in the blob names create a full folder structure under the destination folder, and this structure will be used to download and store the blobs as files.</span></span>

<span data-ttu-id="3196b-182">Als u alleen specifieke blobs wilt downloaden, moet u jokertekens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3196b-182">To selectively download blobs, use wildcards.</span></span> <span data-ttu-id="3196b-183">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3196b-183">For example:</span></span>

* <span data-ttu-id="3196b-184">Als u meerdere sleutelkluizen hebt en het logboek voor slechts één sleutelkluis wilt downloaden met de naam CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="3196b-184">If you have multiple key vaults and want to download logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="3196b-185">Als u meerdere resourcegroepen hebt en logboeken voor slechts één resourcegroep wilt downloaden, gebruikt u `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="3196b-185">If you have multiple resource groups and want to download logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="3196b-186">Als u alle logboeken voor de maand januari 2016 wilt, gebruikt u `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="3196b-186">If you want to download all the logs for the month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="3196b-187">We gaan zo kijken wat er precies in de logboeken staat.</span><span class="sxs-lookup"><span data-stu-id="3196b-187">You're now ready to start looking at what's in the logs.</span></span> <span data-ttu-id="3196b-188">Maar eerst behandelen we nog twee parameters voor Get-AzureRmDiagnosticSetting die handig kunnen zijn:</span><span class="sxs-lookup"><span data-stu-id="3196b-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need to know:</span></span>

* <span data-ttu-id="3196b-189">De status van diagnostische instellingen voor uw sleutelkluisresource opvragen: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="3196b-189">To query the  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="3196b-190">Logboekregistratie voor uw sleutelkluisresource uitschakelen: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="3196b-190">To disable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="3196b-191"><a id="interpret"></a>De Sleutelkluis-logboekgegevens interpreteren</span><span class="sxs-lookup"><span data-stu-id="3196b-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="3196b-192">Afzonderlijke blobs worden opgeslagen als tekst, die is opgemaakt als een JSON-blob.</span><span class="sxs-lookup"><span data-stu-id="3196b-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="3196b-193">Dit is een voorbeeld van een logboekvermelding van het uitvoeren van `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="3196b-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


<span data-ttu-id="3196b-194">De volgende tabel bevat de namen en beschrijvingen van velden.</span><span class="sxs-lookup"><span data-stu-id="3196b-194">The following table lists the field names and descriptions.</span></span>

| <span data-ttu-id="3196b-195">Veldnaam</span><span class="sxs-lookup"><span data-stu-id="3196b-195">Field name</span></span> | <span data-ttu-id="3196b-196">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="3196b-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3196b-197">tijd</span><span class="sxs-lookup"><span data-stu-id="3196b-197">time</span></span> |<span data-ttu-id="3196b-198">Datum en tijd (UTC).</span><span class="sxs-lookup"><span data-stu-id="3196b-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="3196b-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="3196b-199">resourceId</span></span> |<span data-ttu-id="3196b-200">Azure Resource Manager-resource-id.</span><span class="sxs-lookup"><span data-stu-id="3196b-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="3196b-201">Voor Sleutelkluis-logboeken is dit altijd de Sleutelkluis-resource-id.</span><span class="sxs-lookup"><span data-stu-id="3196b-201">For Key Vault logs, this is always the  Key Vault resource ID.</span></span> |
| <span data-ttu-id="3196b-202">operationName</span><span class="sxs-lookup"><span data-stu-id="3196b-202">operationName</span></span> |<span data-ttu-id="3196b-203">Naam van de bewerking, zoals beschreven in de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="3196b-203">Name of the operation, as documented in the next table.</span></span> |
| <span data-ttu-id="3196b-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="3196b-204">operationVersion</span></span> |<span data-ttu-id="3196b-205">Dit is de REST-API-versie die door de client is aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="3196b-205">This is the REST API version requested by the client.</span></span> |
| <span data-ttu-id="3196b-206">category</span><span class="sxs-lookup"><span data-stu-id="3196b-206">category</span></span> |<span data-ttu-id="3196b-207">Voor Sleutelkluis-logboeken is AuditEvent de enige beschikbare waarde.</span><span class="sxs-lookup"><span data-stu-id="3196b-207">For Key Vault logs, AuditEvent is the single, available value.</span></span> |
| <span data-ttu-id="3196b-208">resultType</span><span class="sxs-lookup"><span data-stu-id="3196b-208">resultType</span></span> |<span data-ttu-id="3196b-209">Resultaat van de REST-API-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3196b-209">Result of REST API request.</span></span> |
| <span data-ttu-id="3196b-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="3196b-210">resultSignature</span></span> |<span data-ttu-id="3196b-211">HTTP-status.</span><span class="sxs-lookup"><span data-stu-id="3196b-211">HTTP status.</span></span> |
| <span data-ttu-id="3196b-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="3196b-212">resultDescription</span></span> |<span data-ttu-id="3196b-213">Extra beschrijving van het resultaat, indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="3196b-213">Additional description about the result, when available.</span></span> |
| <span data-ttu-id="3196b-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="3196b-214">durationMs</span></span> |<span data-ttu-id="3196b-215">De tijd die nodig was om de REST-API-aanvraag af te handelen in milliseconden.</span><span class="sxs-lookup"><span data-stu-id="3196b-215">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="3196b-216">Hierbij wordt geen rekening gehouden met de netwerklatentie, zodat de tijd die u aan de clientzijde meet mogelijk niet overeenkomt met de tijd die hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3196b-216">This does not include the network latency, so the time you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="3196b-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="3196b-217">callerIpAddress</span></span> |<span data-ttu-id="3196b-218">IP-adres van de client die de aanvraag heeft ingediend.</span><span class="sxs-lookup"><span data-stu-id="3196b-218">IP address of the client who made the request.</span></span> |
| <span data-ttu-id="3196b-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="3196b-219">correlationId</span></span> |<span data-ttu-id="3196b-220">Een optionele GUID die de client kan doorgeven om de logboeken aan de clientzijde te relateren aan (Sleutelkluis-)logboeken aan de servicezijde.</span><span class="sxs-lookup"><span data-stu-id="3196b-220">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="3196b-221">identity</span><span class="sxs-lookup"><span data-stu-id="3196b-221">identity</span></span> |<span data-ttu-id="3196b-222">De identiteit van het token dat is opgegeven bij het maken van de REST-API-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3196b-222">Identity from the token that was presented when making the REST API request.</span></span> <span data-ttu-id="3196b-223">Dit is meestal user, service principal of een combinatie user+ appId, bijvoorbeeld bij een aanvraag via een Azure PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3196b-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="3196b-224">properties</span><span class="sxs-lookup"><span data-stu-id="3196b-224">properties</span></span> |<span data-ttu-id="3196b-225">Dit veld bevat verschillende gegevens op basis van de bewerking (operationName).</span><span class="sxs-lookup"><span data-stu-id="3196b-225">This field will contain different information based on the operation (operationName).</span></span> <span data-ttu-id="3196b-226">In de meeste gevallen bevat dit veld clientgegevens (de useragent-tekenreeks die door de client wordt doorgegeven), de exacte URI voor de REST-API-aanvraag en de HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="3196b-226">In most cases, contains client information (the useragent string passed by the client), the exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="3196b-227">Als een object wordt geretourneerd als gevolg van een aanvraag (bijvoorbeeld KeyCreate of VaultGet) bevat dit veld ook de Key URI (als 'id'), Vault URI of Secret URI.</span><span class="sxs-lookup"><span data-stu-id="3196b-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain the Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="3196b-228">De velwaarden voor **operationName** hebben de ObjectVerb-indeling.</span><span class="sxs-lookup"><span data-stu-id="3196b-228">The **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="3196b-229">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3196b-229">For example:</span></span>

* <span data-ttu-id="3196b-230">Alle sleutelkluisbewerkingen hebben de indeling 'Sleutelkluis`<action>`', zoals `VaultGet` en `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="3196b-230">All key vault operations have the 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="3196b-231">Alle sleutelbewerkingen hebben de indeling 'Sleutel`<action>`', zoals `KeySign` en `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="3196b-231">All  key operations have the 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="3196b-232">Alle geheime bewerkingen hebben de indeling 'Geheim`<action>`', zoals `SecretGet` en `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="3196b-232">All secret operations have the 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="3196b-233">De volgende tabel bevat de operationName en de bijbehorende REST-API-opdracht.</span><span class="sxs-lookup"><span data-stu-id="3196b-233">The following table lists the operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="3196b-234">operationName</span><span class="sxs-lookup"><span data-stu-id="3196b-234">operationName</span></span> | <span data-ttu-id="3196b-235">REST-API-opdracht</span><span class="sxs-lookup"><span data-stu-id="3196b-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="3196b-236">Authentication</span><span class="sxs-lookup"><span data-stu-id="3196b-236">Authentication</span></span> |<span data-ttu-id="3196b-237">Via het Azure Active Directory-eindpunt</span><span class="sxs-lookup"><span data-stu-id="3196b-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="3196b-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="3196b-238">VaultGet</span></span> |[<span data-ttu-id="3196b-239">Informatie over een sleutelkluis ophalen</span><span class="sxs-lookup"><span data-stu-id="3196b-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="3196b-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="3196b-240">VaultPut</span></span> |[<span data-ttu-id="3196b-241">Een sleutelkluis maken of bijwerken</span><span class="sxs-lookup"><span data-stu-id="3196b-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="3196b-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="3196b-242">VaultDelete</span></span> |[<span data-ttu-id="3196b-243">Een sleutelkluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="3196b-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="3196b-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="3196b-244">VaultPatch</span></span> |[<span data-ttu-id="3196b-245">Een sleutelkluis bijwerken</span><span class="sxs-lookup"><span data-stu-id="3196b-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="3196b-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="3196b-246">VaultList</span></span> |[<span data-ttu-id="3196b-247">Alle sleutelkluizen in een resourcegroep weergeven</span><span class="sxs-lookup"><span data-stu-id="3196b-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="3196b-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="3196b-248">KeyCreate</span></span> |[<span data-ttu-id="3196b-249">Een sleutel maken</span><span class="sxs-lookup"><span data-stu-id="3196b-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="3196b-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="3196b-250">KeyGet</span></span> |[<span data-ttu-id="3196b-251">Informatie over een sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="3196b-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="3196b-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="3196b-252">KeyImport</span></span> |[<span data-ttu-id="3196b-253">Een sleutel in een kluis importeren</span><span class="sxs-lookup"><span data-stu-id="3196b-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="3196b-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="3196b-254">KeyBackup</span></span> |<span data-ttu-id="3196b-255">[Back-up maken van een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="3196b-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="3196b-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="3196b-256">KeyDelete</span></span> |[<span data-ttu-id="3196b-257">Een sleutel verwijderen</span><span class="sxs-lookup"><span data-stu-id="3196b-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="3196b-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="3196b-258">KeyRestore</span></span> |[<span data-ttu-id="3196b-259">Een sleutel herstellen</span><span class="sxs-lookup"><span data-stu-id="3196b-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="3196b-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="3196b-260">KeySign</span></span> |[<span data-ttu-id="3196b-261">Aanmelden met een sleutel</span><span class="sxs-lookup"><span data-stu-id="3196b-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="3196b-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="3196b-262">KeyVerify</span></span> |[<span data-ttu-id="3196b-263">Verifiëren met een sleutel</span><span class="sxs-lookup"><span data-stu-id="3196b-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="3196b-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="3196b-264">KeyWrap</span></span> |[<span data-ttu-id="3196b-265">Een sleutel inpakken</span><span class="sxs-lookup"><span data-stu-id="3196b-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="3196b-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="3196b-266">KeyUnwrap</span></span> |[<span data-ttu-id="3196b-267">Een sleutel uitpakken</span><span class="sxs-lookup"><span data-stu-id="3196b-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="3196b-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="3196b-268">KeyEncrypt</span></span> |[<span data-ttu-id="3196b-269">Versleutelen met een sleutel</span><span class="sxs-lookup"><span data-stu-id="3196b-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="3196b-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="3196b-270">KeyDecrypt</span></span> |[<span data-ttu-id="3196b-271">Ontsleutelen met een sleutel</span><span class="sxs-lookup"><span data-stu-id="3196b-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="3196b-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="3196b-272">KeyUpdate</span></span> |[<span data-ttu-id="3196b-273">Een sleutel bijwerken</span><span class="sxs-lookup"><span data-stu-id="3196b-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="3196b-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="3196b-274">KeyList</span></span> |[<span data-ttu-id="3196b-275">De sleutels in een kluis weergeven</span><span class="sxs-lookup"><span data-stu-id="3196b-275">List the keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="3196b-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="3196b-276">KeyListVersions</span></span> |[<span data-ttu-id="3196b-277">De versies van een sleutel weergeven</span><span class="sxs-lookup"><span data-stu-id="3196b-277">List the versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="3196b-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="3196b-278">SecretSet</span></span> |[<span data-ttu-id="3196b-279">Een geheim maken</span><span class="sxs-lookup"><span data-stu-id="3196b-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="3196b-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="3196b-280">SecretGet</span></span> |[<span data-ttu-id="3196b-281">Een geheim ophalen</span><span class="sxs-lookup"><span data-stu-id="3196b-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="3196b-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="3196b-282">SecretUpdate</span></span> |[<span data-ttu-id="3196b-283">Een geheim bijwerken</span><span class="sxs-lookup"><span data-stu-id="3196b-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="3196b-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="3196b-284">SecretDelete</span></span> |[<span data-ttu-id="3196b-285">Een geheim verwijderen</span><span class="sxs-lookup"><span data-stu-id="3196b-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="3196b-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="3196b-286">SecretList</span></span> |[<span data-ttu-id="3196b-287">Geheimen in een kluis weergeven</span><span class="sxs-lookup"><span data-stu-id="3196b-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="3196b-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="3196b-288">SecretListVersions</span></span> |[<span data-ttu-id="3196b-289">Versies van een geheim weergeven</span><span class="sxs-lookup"><span data-stu-id="3196b-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="3196b-290"><a id="loganalytics"></a>Log Analytics gebruiken</span><span class="sxs-lookup"><span data-stu-id="3196b-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="3196b-291">Met de oplossing Azure Key Vault in Log Analytics kunt u de AuditEvent-logboeken van Azure Key Vault controleren.</span><span class="sxs-lookup"><span data-stu-id="3196b-291">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="3196b-292">Zie [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md) (De oplossing Azure Key Vault in Log Analytics) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3196b-292">For more information, including how to set this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="3196b-293">Dit artikel bevat ook instructies voor als u moet migreren van de oude Key Vault-oplossing die tijdens de preview van Log Analytics werd aangeboden en waarbij u uw logboeken eerst moest doorsturen naar een Azure-opslagaccount en Log Analytics moest configureren om van daaruit te lezen.</span><span class="sxs-lookup"><span data-stu-id="3196b-293">This article also contains instructions if you need to migrate from the old Key Vault solution that was offered during the Log Analytics preview, where you first routed your logs to an Azure Storage account and configured Log Analytics to read from there.</span></span>

## <span data-ttu-id="3196b-294"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3196b-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="3196b-295">Zie [Azure Key Vault in een webtoepassing gebruiken](key-vault-use-from-web-application.md) voor een zelfstudie over het gebruik van Azure Key Vault in een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="3196b-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="3196b-296">Zie de [Ontwikkelaarshandleiding voor Azure Key Vault](key-vault-developers-guide.md) voor het programmeren van verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="3196b-296">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="3196b-297">Zie [Cmdlets voor Azure Sleutelkluis](/powershell/module/azurerm.keyvault/#key_vault) voor een lijst met Azure PowerShell 1.0- cmdlets voor Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="3196b-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="3196b-298">Zie [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md) (Sleutelkluis instellen met end-to-endsleutelrotatie en -controle) voor een zelfstudie over sleutelrotatie en logboekcontrole met Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="3196b-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How to setup Key Vault with end to end key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>

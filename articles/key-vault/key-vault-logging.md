---
title: Logboekregistratie van Sleutelkluis aaaAzure | Microsoft Docs
description: Gebruik deze zelfstudie toohelp die u aan de slag met Azure Key Vault logboekregistratie.
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
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a><span data-ttu-id="2a01c-103">Logboekregistratie van Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="2a01c-103">Azure Key Vault Logging</span></span>
<span data-ttu-id="2a01c-104">Azure Sleutelkluis is beschikbaar in de meeste regio's.</span><span class="sxs-lookup"><span data-stu-id="2a01c-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="2a01c-105">Zie voor meer informatie, Hallo [pagina prijzen van Sleutelkluis](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="2a01c-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="2a01c-106">Inleiding</span><span class="sxs-lookup"><span data-stu-id="2a01c-106">Introduction</span></span>
<span data-ttu-id="2a01c-107">Wanneer u een of meer sleutelkluizen hebt gemaakt, wilt u waarschijnlijk toomonitor hoe en wanneer uw sleutel kluizen toegankelijk zijn en door wie.</span><span class="sxs-lookup"><span data-stu-id="2a01c-107">After you have created one or more key vaults, you will likely want toomonitor how and when your key vaults are accessed, and by whom.</span></span> <span data-ttu-id="2a01c-108">U kunt dit doen door logboekregistratie in te schakelen voor Sleutelkluis. Hierbij wordt de informatie opgeslagen in een Azure-opslagaccount dat u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="2a01c-108">You can do this by enabling logging for Key Vault, which saves information in an Azure storage account that you provide.</span></span> <span data-ttu-id="2a01c-109">Er wordt automatisch een nieuwe container met de naam **insights-logboeken-auditevent** gemaakt voor het opgegeven opslagaccount en u kunt hetzelfde opslagaccount gebruiken voor het verzamelen van logboeken voor meerdere sleutelkluizen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-109">A new container named **insights-logs-auditevent** is automatically created for your specified storage account, and you can use this same storage account for collecting logs for multiple key vaults.</span></span>

<span data-ttu-id="2a01c-110">U kunt uw logboekgegevens maximaal openen, 10 minuten nadat de Hallo sleutel sleutelkluisbewerking is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2a01c-110">You can access your logging information at most, 10 minutes after hello key vault operation.</span></span> <span data-ttu-id="2a01c-111">In de meeste gevallen gaat het echter veel sneller.</span><span class="sxs-lookup"><span data-stu-id="2a01c-111">In most cases, it will be quicker than this.</span></span>  <span data-ttu-id="2a01c-112">Het is tooyou toomanage uw logboeken in uw opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="2a01c-112">It's up tooyou toomanage your logs in your storage account:</span></span>

* <span data-ttu-id="2a01c-113">Gebruik standaard Azure access control methoden toosecure uw logboeken door te beperken wie er toegang toe.</span><span class="sxs-lookup"><span data-stu-id="2a01c-113">Use standard Azure access control methods toosecure your logs by restricting who can access them.</span></span>
* <span data-ttu-id="2a01c-114">Logboeken die u niet meer tookeep in uw opslagaccount wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-114">Delete logs that you no longer want tookeep in your storage account.</span></span>

<span data-ttu-id="2a01c-115">Gebruik deze zelfstudie toohelp die u aan de slag met Azure Key Vault aan te melden, toocreate uw storage-account inschakelen van logboekregistratie en interpreteren Hallo logboekgegevens die worden verzameld.</span><span class="sxs-lookup"><span data-stu-id="2a01c-115">Use this tutorial toohelp you get started with Azure Key Vault logging, toocreate your storage account, enable logging, and interpret hello logging information collected.</span></span>  

> [!NOTE]
> <span data-ttu-id="2a01c-116">Deze zelfstudie bevat geen instructies voor hoe toocreate sleutel kluizen, sleutels of geheimen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-116">This tutorial does not include instructions for how toocreate key vaults, keys, or secrets.</span></span> <span data-ttu-id="2a01c-117">Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2a01c-117">For this information, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span> <span data-ttu-id="2a01c-118">Zie [deze equivalente zelfstudie](key-vault-manage-with-cli2.md) voor instructies voor het maken van een platformonafhankelijke opdrachtregelinterface.</span><span class="sxs-lookup"><span data-stu-id="2a01c-118">Or, for Cross-Platform Command-Line Interface instructions, see [this equivalent tutorial](key-vault-manage-with-cli2.md).</span></span>
>
> <span data-ttu-id="2a01c-119">U kunt op dit moment is Azure Sleutelkluis in hello Azure-portal configureren.</span><span class="sxs-lookup"><span data-stu-id="2a01c-119">Currently, you cannot configure Azure Key Vault in hello Azure portal.</span></span> <span data-ttu-id="2a01c-120">Gebruik in plaats daarvan deze instructies voor Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a01c-120">Instead, use these Azure PowerShell instructions.</span></span>
>
>

<span data-ttu-id="2a01c-121">Zie [Wat is Azure Key Vault?](key-vault-whatis.md) voor algemene informatie over Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="2a01c-121">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a01c-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2a01c-122">Prerequisites</span></span>
<span data-ttu-id="2a01c-123">toocomplete in deze zelfstudie hebt u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="2a01c-123">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="2a01c-124">Een bestaande sleutelkluis die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2a01c-124">An existing key vault that you have been using.</span></span>  
* <span data-ttu-id="2a01c-125">Azure PowerShell, **versie 1.0.1 of hoger**.</span><span class="sxs-lookup"><span data-stu-id="2a01c-125">Azure PowerShell, **minimum version of 1.0.1**.</span></span> <span data-ttu-id="2a01c-126">tooinstall Azure PowerShell en deze koppelen aan uw Azure-abonnement, Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2a01c-126">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2a01c-127">Als u Azure PowerShell al hebt geïnstalleerd en het Hallo-versie van hello Azure PowerShell-console niet weet, typt u `(Get-Module azure -ListAvailable).Version`.</span><span class="sxs-lookup"><span data-stu-id="2a01c-127">If you have already installed Azure PowerShell and do not know hello version, from hello Azure PowerShell console, type `(Get-Module azure -ListAvailable).Version`.</span></span>  
* <span data-ttu-id="2a01c-128">Voldoende opslagruimte op Azure voor uw Sleutelkluis-logboeken.</span><span class="sxs-lookup"><span data-stu-id="2a01c-128">Sufficient storage on Azure for your Key Vault logs.</span></span>

## <span data-ttu-id="2a01c-129"><a id="connect"></a>Verbinding maken met tooyour abonnementen</span><span class="sxs-lookup"><span data-stu-id="2a01c-129"><a id="connect"></a>Connect tooyour subscriptions</span></span>
<span data-ttu-id="2a01c-130">Start een Azure PowerShell-sessie en meld u aan tooyour Azure-account met de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="2a01c-130">Start an Azure PowerShell session and sign in tooyour Azure account with hello following command:</span></span>  

    Login-AzureRmAccount

<span data-ttu-id="2a01c-131">In het pop-browservenster hello, Voer uw Azure-account, gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="2a01c-131">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="2a01c-132">Azure PowerShell haalt alle Hallo-abonnementen die gekoppeld aan dit account en standaard zijn, gebruikt de eerste Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a01c-132">Azure PowerShell will get all hello subscriptions that are associated with this account and by default, uses hello first one.</span></span>

<span data-ttu-id="2a01c-133">Als u meerdere abonnementen hebt, moet u wellicht toospecify een specifiek abonnement dat gebruikt toocreate is uw Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2a01c-133">If you have multiple subscriptions, you might have toospecify a specific one that was used toocreate your Azure Key Vault.</span></span> <span data-ttu-id="2a01c-134">Type Hallo toosee Hallo abonnementen voor uw account te volgen:</span><span class="sxs-lookup"><span data-stu-id="2a01c-134">Type hello following toosee hello subscriptions for your account:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="2a01c-135">Vervolgens toospecify Hallo abonnement is gekoppeld aan de sleutelkluis die u logboekregistratie inschakelen wilt, type:</span><span class="sxs-lookup"><span data-stu-id="2a01c-135">Then, toospecify hello subscription that's associated with your key vault you will be logging, type:</span></span>

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> <span data-ttu-id="2a01c-136">Dit is een belangrijke stap, die met name handig is als er meerdere abonnementen zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="2a01c-136">This is an important step and especially helpful if you have multiple subscriptions associated with your account.</span></span> <span data-ttu-id="2a01c-137">U krijgt een fout tooregister Microsoft.Insights als deze stap overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-137">You may receive an error tooregister Microsoft.Insights if this step is skipped.</span></span>
>   
>

<span data-ttu-id="2a01c-138">Zie voor meer informatie over het configureren van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2a01c-138">For more information about configuring Azure PowerShell, see  [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="2a01c-139"><a id="storage"></a>Een nieuw opslagaccount voor uw logboeken maken</span><span class="sxs-lookup"><span data-stu-id="2a01c-139"><a id="storage"></a>Create a new storage account for your logs</span></span>
<span data-ttu-id="2a01c-140">Hoewel u een bestaand opslagaccount voor uw Logboeken gebruiken kunt, maakt een nieuw opslagaccount die toegewezen tooKey kluis logboeken worden.</span><span class="sxs-lookup"><span data-stu-id="2a01c-140">Although you can use an existing storage account for your logs, we'll create a new storage account that will be dedicated tooKey Vault logs.</span></span> <span data-ttu-id="2a01c-141">Voor het gemak wanneer we toospecify dit hebt later Hallo details hebt opgeslagen in een variabele met de naam **sa**.</span><span class="sxs-lookup"><span data-stu-id="2a01c-141">For convenience for when we have toospecify this later, we'll store hello details into a variable named **sa**.</span></span>

<span data-ttu-id="2a01c-142">Voor extra beheer te vereenvoudigen, gebruiken we Hallo van dezelfde resourcegroep als een bestand met onze sleutelkluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a01c-142">For additional ease of management, we'll also use hello same resource group as hello one that contains our key vault.</span></span> <span data-ttu-id="2a01c-143">Van Hallo [zelfstudie aan de slag](key-vault-get-started.md), deze resourcegroep de naam **ContosoResourceGroup** en we toouse Hallo Oost-Azië locatie.</span><span class="sxs-lookup"><span data-stu-id="2a01c-143">From hello [getting started tutorial](key-vault-get-started.md), this resource group is named **ContosoResourceGroup** and we'll continue toouse hello East Asia location.</span></span> <span data-ttu-id="2a01c-144">Vervang deze waarden voor uzelf, indien van toepassing:</span><span class="sxs-lookup"><span data-stu-id="2a01c-144">Substitute these values for your own, as applicable:</span></span>

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> <span data-ttu-id="2a01c-145">Als u een bestaand opslagaccount toouse beslist, moet hiervoor hetzelfde abonnement Hallo als uw sleutelkluis en deze Hallo Resource Manager-implementatiemodel, in plaats van Hallo klassieke implementatiemodel gebruiken moeten.</span><span class="sxs-lookup"><span data-stu-id="2a01c-145">If you decide toouse an existing storage account, it must use hello same subscription as your key vault and it must use hello Resource Manager deployment model, rather than hello Classic deployment model.</span></span>
>
>

## <span data-ttu-id="2a01c-146"><a id="identify"></a>Hallo sleutelkluis voor uw logboeken identificeren</span><span class="sxs-lookup"><span data-stu-id="2a01c-146"><a id="identify"></a>Identify hello key vault for your logs</span></span>
<span data-ttu-id="2a01c-147">In onze zelfstudie aan de slag is de naam van onze sleutelkluis **ContosoKeyVault**, zodat we toouse die een naam Hallo details opslaan in een variabele met de naam ook **kv**:</span><span class="sxs-lookup"><span data-stu-id="2a01c-147">In our getting started tutorial, our key vault name was **ContosoKeyVault**, so we'll continue toouse that name and store hello details into a variable named **kv**:</span></span>

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <span data-ttu-id="2a01c-148"><a id="enable"></a>Logboekregistratie inschakelen</span><span class="sxs-lookup"><span data-stu-id="2a01c-148"><a id="enable"></a>Enable logging</span></span>
<span data-ttu-id="2a01c-149">tooenable logboekregistratie voor Sleutelkluis, gebruiken we de cmdlet Set-AzureRmDiagnosticSetting hello, samen met de Hallo variabelen die we voor ons nieuwe opslagaccount en onze sleutelkluis hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2a01c-149">tooenable logging for Key Vault, we'll use hello Set-AzureRmDiagnosticSetting cmdlet, together with hello variables we created for our new storage account and our key vault.</span></span> <span data-ttu-id="2a01c-150">We ook Hallo hebt ingesteld **-ingeschakeld** te markeren**$true** en stel Hallo categorie tooAuditEvent (Hallo enige categorie voor logboekregistratie van Sleutelkluis):</span><span class="sxs-lookup"><span data-stu-id="2a01c-150">We'll also set hello **-Enabled** flag too**$true** and set hello category tooAuditEvent (hello only category for Key Vault logging), :</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

<span data-ttu-id="2a01c-151">Hallo-uitvoer hiervoor bevat:</span><span class="sxs-lookup"><span data-stu-id="2a01c-151">hello output for this includes:</span></span>

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


<span data-ttu-id="2a01c-152">Hiermee bevestigt u dat logboekregistratie nu is ingeschakeld voor uw sleutelkluis, het opslaan van informatie tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="2a01c-152">This confirms that logging is now enabled for your key vault, saving information tooyour storage account.</span></span>

<span data-ttu-id="2a01c-153">U kunt eventueel ook een retentiebeleid instellen voor uw logboeken, zodat oudere logboeken automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2a01c-153">Optionally you can also set retention policy for your logs such that older logs will be automatically deleted.</span></span> <span data-ttu-id="2a01c-154">Bijvoorbeeld ingesteld bewaren beleid met **- RetentionEnabled** te markeren**$true** en stel **- RetentionInDays** parameter te**90** zodat dat Logboeken ouder is dan 90 dagen automatisch worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="2a01c-154">For example, set retention policy using **-RetentionEnabled** flag too**$true** and set **-RetentionInDays** parameter too**90** so that logs older than 90 days will be automatically deleted.</span></span>

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

<span data-ttu-id="2a01c-155">Wat wordt in het logboek vastgelegd?</span><span class="sxs-lookup"><span data-stu-id="2a01c-155">What's logged:</span></span>

* <span data-ttu-id="2a01c-156">Alle geverifieerde REST-API-aanvragen worden vastgelegd, ook mislukte aanvragen als gevolg van toegangsmachtigingen, systeemfouten of ongeldige aanvragen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-156">All authenticated REST API requests are logged, which includes failed requests as a result of access permissions, system errors or bad requests.</span></span>
* <span data-ttu-id="2a01c-157">Bewerkingen op Hallo sleutel sleutelkluis zelf, waaronder het maken, verwijderen, instelling toegangsbeleid voor sleutelkluizen, en bijwerken van de kenmerken, zoals tags.</span><span class="sxs-lookup"><span data-stu-id="2a01c-157">Operations on hello key vault itself, which includes creation, deletion, setting key vault access policies, and updating key vault attributes such as tags.</span></span>
* <span data-ttu-id="2a01c-158">Bewerkingen voor sleutels en geheimen in Hallo sleutelkluis, waaronder maken, wijzigen of verwijderen van deze sleutels of geheimen; bewerkingen zoals het ondertekenen, controleren, versleutelen, ontsleutelen, Inpakken en uitpakken van sleutels, geheimen, lijst met sleutels en geheimen en hun versies ophalen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-158">Operations on keys and secrets in hello key vault, which includes creating, modifying, or deleting these keys or secrets; operations such as sign, verify, encrypt, decrypt, wrap and unwrap keys, get secrets, list keys and secrets and their versions.</span></span>
* <span data-ttu-id="2a01c-159">Niet-geverifieerde aanvragen die in een 401-respons resulteren.</span><span class="sxs-lookup"><span data-stu-id="2a01c-159">Unauthenticated requests that result in a 401 response.</span></span> <span data-ttu-id="2a01c-160">Dit zijn bijvoorbeeld aanvragen die geen Bearer-token hebben, ongeldige of verlopen aanvragen of aanvragen met een ongeldig token.</span><span class="sxs-lookup"><span data-stu-id="2a01c-160">For example, requests that do not have a bearer token, or are malformed or expired, or have an invalid token.</span></span>  

## <span data-ttu-id="2a01c-161"><a id="access"></a>Toegang tot uw logboeken</span><span class="sxs-lookup"><span data-stu-id="2a01c-161"><a id="access"></a>Access your logs</span></span>
<span data-ttu-id="2a01c-162">Sleutelkluis-logboeken worden opgeslagen in Hallo **insights-logs-auditevent** container in Hallo storage-account u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="2a01c-162">Key vault logs are stored in hello **insights-logs-auditevent** container in hello storage account you provided.</span></span> <span data-ttu-id="2a01c-163">toolist alle Hallo blobs in deze container, typt u:</span><span class="sxs-lookup"><span data-stu-id="2a01c-163">toolist all hello blobs in this container, type:</span></span>

<span data-ttu-id="2a01c-164">Maak eerst een variabele voor naam van de container Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a01c-164">First, create a variable for hello container name.</span></span> <span data-ttu-id="2a01c-165">Deze wordt gebruikt in de rest Hallo van Hallo doorlopen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-165">This will be used throughout hello rest of hello walk through.</span></span>

    $container = 'insights-logs-auditevent'

<span data-ttu-id="2a01c-166">toolist alle Hallo blobs in deze container, typt u:</span><span class="sxs-lookup"><span data-stu-id="2a01c-166">toolist all hello blobs in this container, type:</span></span>

    Get-AzureStorageBlob -Container $container -Context $sa.Context
<span data-ttu-id="2a01c-167">Hallo-uitvoer ziet er iets dergelijks toothis:</span><span class="sxs-lookup"><span data-stu-id="2a01c-167">hello output will look something similar toothis:</span></span>

<span data-ttu-id="2a01c-168">**Container-URI: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span><span class="sxs-lookup"><span data-stu-id="2a01c-168">**Container Uri: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**</span></span>

<span data-ttu-id="2a01c-169">**Naam**</span><span class="sxs-lookup"><span data-stu-id="2a01c-169">**Name**</span></span>

- - -
<span data-ttu-id="2a01c-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="2a01c-170">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**</span></span>

<span data-ttu-id="2a01c-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span><span class="sxs-lookup"><span data-stu-id="2a01c-171">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**</span></span>

<span data-ttu-id="2a01c-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span><span class="sxs-lookup"><span data-stu-id="2a01c-172">**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****</span></span>

<span data-ttu-id="2a01c-173">Als u in deze uitvoer zien kunt, Hallo blobs de volgende naamgevingsregels: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**</span><span class="sxs-lookup"><span data-stu-id="2a01c-173">As you can see from this output, hello blobs follow a naming convention: **resourceId=<ARM resource ID>/y=<year>/m=<month>/d=<day of month>/h=<hour>/m=<minute>/filename.json**</span></span>

<span data-ttu-id="2a01c-174">de datum- en tijdwaarden Hallo gebruik UTC.</span><span class="sxs-lookup"><span data-stu-id="2a01c-174">hello date and time values use UTC.</span></span>

<span data-ttu-id="2a01c-175">Omdat hello hetzelfde opslagaccount kan gebruikte toocollect logboeken voor meerdere resources, is hello volledige resource-ID in de blob-naam Hallo zeer nuttig tooaccess of download alleen Hallo blobs die u nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="2a01c-175">Because hello same storage account can be used toocollect logs for multiple resources, hello full resource ID in hello blob name is very useful tooaccess or download just hello blobs that you need.</span></span> <span data-ttu-id="2a01c-176">Maar voordat we dat doen, eerst aan bod hoe toodownload alle blobs Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a01c-176">But before we do that, we'll first cover how toodownload all hello blobs.</span></span>

<span data-ttu-id="2a01c-177">Maak een map toodownload Hallo eerst blobs.</span><span class="sxs-lookup"><span data-stu-id="2a01c-177">First, create a folder toodownload hello blobs.</span></span> <span data-ttu-id="2a01c-178">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2a01c-178">For example:</span></span>

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

<span data-ttu-id="2a01c-179">Haal vervolgens een lijst met alle blobs op:</span><span class="sxs-lookup"><span data-stu-id="2a01c-179">Then get a list of all blobs:</span></span>  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

<span data-ttu-id="2a01c-180">Sluis deze lijst via 'Get-AzureStorageBlobContent' toodownload Hallo blobs in de doelmap:</span><span class="sxs-lookup"><span data-stu-id="2a01c-180">Pipe this list through 'Get-AzureStorageBlobContent' toodownload hello blobs into our destination folder:</span></span>

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

<span data-ttu-id="2a01c-181">Wanneer u deze tweede opdracht uitvoert, Hallo  **/**  scheidingsteken in Hallo blobnamen een volledige mapstructuur onder de doelmap Hallo maken en deze structuur worden gebruikte toodownload en store Hallo blobs als bestanden.</span><span class="sxs-lookup"><span data-stu-id="2a01c-181">When you run this second command, hello **/** delimiter in hello blob names create a full folder structure under hello destination folder, and this structure will be used toodownload and store hello blobs as files.</span></span>

<span data-ttu-id="2a01c-182">tooselectively blobs downloaden, jokertekens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2a01c-182">tooselectively download blobs, use wildcards.</span></span> <span data-ttu-id="2a01c-183">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2a01c-183">For example:</span></span>

* <span data-ttu-id="2a01c-184">Als u meerdere sleutelkluizen hebt en toodownload logboeken voor slechts één sleutelkluis wilt instellen, met de naam CONTOSOKEYVAULT3:</span><span class="sxs-lookup"><span data-stu-id="2a01c-184">If you have multiple key vaults and want toodownload logs for just one key vault, named CONTOSOKEYVAULT3:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* <span data-ttu-id="2a01c-185">Als u meerdere resourcegroepen hebt en toodownload logboeken voor slechts één resourcegroep wilt instellen, gebruikt u `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span><span class="sxs-lookup"><span data-stu-id="2a01c-185">If you have multiple resource groups and want toodownload logs for just one resource group, use `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* <span data-ttu-id="2a01c-186">Als u alle Hallo logboeken toodownload Hallo maand januari 2016 wilt, gebruik `-Blob '*/year=2016/m=01/*'`:</span><span class="sxs-lookup"><span data-stu-id="2a01c-186">If you want toodownload all hello logs for hello month of January 2016, use `-Blob '*/year=2016/m=01/*'`:</span></span>

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

<span data-ttu-id="2a01c-187">U bent nu klaar toostart kijken wat is er in Hallo registreert.</span><span class="sxs-lookup"><span data-stu-id="2a01c-187">You're now ready toostart looking at what's in hello logs.</span></span> <span data-ttu-id="2a01c-188">Maar eerst die twee parameters voor Get-AzureRmDiagnosticSetting tooknow moet mogelijk:</span><span class="sxs-lookup"><span data-stu-id="2a01c-188">But before moving onto that, two more parameters for Get-AzureRmDiagnosticSetting that you might need tooknow:</span></span>

* <span data-ttu-id="2a01c-189">tooquery hello status van diagnostische instellingen voor uw sleutelkluisresource:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span><span class="sxs-lookup"><span data-stu-id="2a01c-189">tooquery hello  status of diagnostic settings for your key vault resource: `Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`</span></span>
* <span data-ttu-id="2a01c-190">toodisable logboekregistratie in voor uw sleutelkluisresource:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span><span class="sxs-lookup"><span data-stu-id="2a01c-190">toodisable logging for your key vault resource: `Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`</span></span>

## <span data-ttu-id="2a01c-191"><a id="interpret"></a>De Sleutelkluis-logboekgegevens interpreteren</span><span class="sxs-lookup"><span data-stu-id="2a01c-191"><a id="interpret"></a>Interpret your Key Vault logs</span></span>
<span data-ttu-id="2a01c-192">Afzonderlijke blobs worden opgeslagen als tekst, die is opgemaakt als een JSON-blob.</span><span class="sxs-lookup"><span data-stu-id="2a01c-192">Individual blobs are stored as text, formatted as a JSON blob.</span></span> <span data-ttu-id="2a01c-193">Dit is een voorbeeld van een logboekvermelding van het uitvoeren van `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span><span class="sxs-lookup"><span data-stu-id="2a01c-193">This is an example log entry from running `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:</span></span>

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


<span data-ttu-id="2a01c-194">Hallo volgende tabel bevat Hallo veldnamen en beschrijvingen.</span><span class="sxs-lookup"><span data-stu-id="2a01c-194">hello following table lists hello field names and descriptions.</span></span>

| <span data-ttu-id="2a01c-195">Veldnaam</span><span class="sxs-lookup"><span data-stu-id="2a01c-195">Field name</span></span> | <span data-ttu-id="2a01c-196">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="2a01c-196">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a01c-197">tijd</span><span class="sxs-lookup"><span data-stu-id="2a01c-197">time</span></span> |<span data-ttu-id="2a01c-198">Datum en tijd (UTC).</span><span class="sxs-lookup"><span data-stu-id="2a01c-198">Date and time (UTC).</span></span> |
| <span data-ttu-id="2a01c-199">resourceId</span><span class="sxs-lookup"><span data-stu-id="2a01c-199">resourceId</span></span> |<span data-ttu-id="2a01c-200">Azure Resource Manager-resource-id.</span><span class="sxs-lookup"><span data-stu-id="2a01c-200">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="2a01c-201">Voor Sleutelkluis-Logboeken is dit altijd Hallo Sleutelkluis bron-ID.</span><span class="sxs-lookup"><span data-stu-id="2a01c-201">For Key Vault logs, this is always hello  Key Vault resource ID.</span></span> |
| <span data-ttu-id="2a01c-202">operationName</span><span class="sxs-lookup"><span data-stu-id="2a01c-202">operationName</span></span> |<span data-ttu-id="2a01c-203">Naam van het Hallo-bewerking, zoals beschreven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="2a01c-203">Name of hello operation, as documented in hello next table.</span></span> |
| <span data-ttu-id="2a01c-204">operationVersion</span><span class="sxs-lookup"><span data-stu-id="2a01c-204">operationVersion</span></span> |<span data-ttu-id="2a01c-205">Dit is Hallo REST-API-versie door Hallo-client wordt aangevraagd.</span><span class="sxs-lookup"><span data-stu-id="2a01c-205">This is hello REST API version requested by hello client.</span></span> |
| <span data-ttu-id="2a01c-206">category</span><span class="sxs-lookup"><span data-stu-id="2a01c-206">category</span></span> |<span data-ttu-id="2a01c-207">Voor Sleutelkluis-Logboeken is AuditEvent Hallo enige beschikbare waarde.</span><span class="sxs-lookup"><span data-stu-id="2a01c-207">For Key Vault logs, AuditEvent is hello single, available value.</span></span> |
| <span data-ttu-id="2a01c-208">resultType</span><span class="sxs-lookup"><span data-stu-id="2a01c-208">resultType</span></span> |<span data-ttu-id="2a01c-209">Resultaat van de REST-API-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="2a01c-209">Result of REST API request.</span></span> |
| <span data-ttu-id="2a01c-210">resultSignature</span><span class="sxs-lookup"><span data-stu-id="2a01c-210">resultSignature</span></span> |<span data-ttu-id="2a01c-211">HTTP-status.</span><span class="sxs-lookup"><span data-stu-id="2a01c-211">HTTP status.</span></span> |
| <span data-ttu-id="2a01c-212">resultDescription</span><span class="sxs-lookup"><span data-stu-id="2a01c-212">resultDescription</span></span> |<span data-ttu-id="2a01c-213">Extra beschrijving van Hallo resultaat, indien beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="2a01c-213">Additional description about hello result, when available.</span></span> |
| <span data-ttu-id="2a01c-214">durationMs</span><span class="sxs-lookup"><span data-stu-id="2a01c-214">durationMs</span></span> |<span data-ttu-id="2a01c-215">De tijd die nodig tooservice Hallo REST-API-aanvraag in milliseconden was.</span><span class="sxs-lookup"><span data-stu-id="2a01c-215">Time it took tooservice hello REST API request, in milliseconds.</span></span> <span data-ttu-id="2a01c-216">Dit omvat geen Hallo netwerklatentie, zodat u aan de clientzijde Hallo meten Hallo-tijd mogelijk niet overeenkomt met deze tijd.</span><span class="sxs-lookup"><span data-stu-id="2a01c-216">This does not include hello network latency, so hello time you measure on hello client side might not match this time.</span></span> |
| <span data-ttu-id="2a01c-217">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="2a01c-217">callerIpAddress</span></span> |<span data-ttu-id="2a01c-218">IP-adres van Hallo-client die Hallo-aanvraag heeft ingediend.</span><span class="sxs-lookup"><span data-stu-id="2a01c-218">IP address of hello client who made hello request.</span></span> |
| <span data-ttu-id="2a01c-219">correlationId</span><span class="sxs-lookup"><span data-stu-id="2a01c-219">correlationId</span></span> |<span data-ttu-id="2a01c-220">Een optionele GUID die client Hallo kunt toocorrelate doorgeven aan de clientzijde logboeken met servicezijde (Sleutelkluis-) Logboeken.</span><span class="sxs-lookup"><span data-stu-id="2a01c-220">An optional GUID that hello client can pass toocorrelate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="2a01c-221">identity</span><span class="sxs-lookup"><span data-stu-id="2a01c-221">identity</span></span> |<span data-ttu-id="2a01c-222">De identiteit van de Hallo-token dat is opgegeven bij het maken van Hallo REST-API-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="2a01c-222">Identity from hello token that was presented when making hello REST API request.</span></span> <span data-ttu-id="2a01c-223">Dit is meestal user, service principal of een combinatie user+ appId, bijvoorbeeld bij een aanvraag via een Azure PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2a01c-223">This is usually a "user", a "service principal" or a combination "user+appId" as in case of a request resulting from a Azure PowerShell cmdlet.</span></span> |
| <span data-ttu-id="2a01c-224">properties</span><span class="sxs-lookup"><span data-stu-id="2a01c-224">properties</span></span> |<span data-ttu-id="2a01c-225">Dit veld bevat verschillende gegevens op basis van het Hallo-bewerking (operationName).</span><span class="sxs-lookup"><span data-stu-id="2a01c-225">This field will contain different information based on hello operation (operationName).</span></span> <span data-ttu-id="2a01c-226">In de meeste gevallen bevat informatie over de client (Hallo useragent-tekenreeks doorgegeven door de client Hallo), Hallo exacte REST-API aanvraag-URI en HTTP-statuscode.</span><span class="sxs-lookup"><span data-stu-id="2a01c-226">In most cases, contains client information (hello useragent string passed by hello client), hello exact REST API request URI, and HTTP status code.</span></span> <span data-ttu-id="2a01c-227">Bovendien wanneer een object wordt geretourneerd als gevolg van een aanvraag (bijvoorbeeld KeyCreate of VaultGet) bevat ook Hallo Key URI (als 'id'), Vault URI of Secret URI.</span><span class="sxs-lookup"><span data-stu-id="2a01c-227">In addition, when an object is returned as a result of a request (for example, KeyCreate or VaultGet) it will also contain hello Key URI (as "id"), Vault URI, or Secret URI.</span></span> |

<span data-ttu-id="2a01c-228">Hallo **operationName** veldwaarden hebben de ObjectVerb-indeling.</span><span class="sxs-lookup"><span data-stu-id="2a01c-228">hello **operationName** field values are in ObjectVerb format.</span></span> <span data-ttu-id="2a01c-229">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2a01c-229">For example:</span></span>

* <span data-ttu-id="2a01c-230">Alle sleutelkluisbewerkingen hebben Hallo ' kluis`<action>`'-indeling, zoals `VaultGet` en `VaultCreate`.</span><span class="sxs-lookup"><span data-stu-id="2a01c-230">All key vault operations have hello 'Vault`<action>`' format, such as `VaultGet` and `VaultCreate`.</span></span>
* <span data-ttu-id="2a01c-231">Alle sleutelbewerkingen hebben Hallo ' sleutel`<action>`'-indeling, zoals `KeySign` en `KeyList`.</span><span class="sxs-lookup"><span data-stu-id="2a01c-231">All  key operations have hello 'Key`<action>`' format, such as `KeySign` and `KeyList`.</span></span>
* <span data-ttu-id="2a01c-232">Alle geheime bewerkingen hebben Hallo ' geheim`<action>`'-indeling, zoals `SecretGet` en `SecretListVersions`.</span><span class="sxs-lookup"><span data-stu-id="2a01c-232">All secret operations have hello 'Secret`<action>`' format, such as `SecretGet` and `SecretListVersions`.</span></span>

<span data-ttu-id="2a01c-233">Hallo volgende tabel geeft een lijst Hallo operationName en de bijbehorende REST-API-opdracht.</span><span class="sxs-lookup"><span data-stu-id="2a01c-233">hello following table lists hello operationName and corresponding REST API command.</span></span>

| <span data-ttu-id="2a01c-234">operationName</span><span class="sxs-lookup"><span data-stu-id="2a01c-234">operationName</span></span> | <span data-ttu-id="2a01c-235">REST-API-opdracht</span><span class="sxs-lookup"><span data-stu-id="2a01c-235">REST API Command</span></span> |
| --- | --- |
| <span data-ttu-id="2a01c-236">Authentication</span><span class="sxs-lookup"><span data-stu-id="2a01c-236">Authentication</span></span> |<span data-ttu-id="2a01c-237">Via het Azure Active Directory-eindpunt</span><span class="sxs-lookup"><span data-stu-id="2a01c-237">Via Azure Active Directory endpoint</span></span> |
| <span data-ttu-id="2a01c-238">VaultGet</span><span class="sxs-lookup"><span data-stu-id="2a01c-238">VaultGet</span></span> |[<span data-ttu-id="2a01c-239">Informatie over een sleutelkluis ophalen</span><span class="sxs-lookup"><span data-stu-id="2a01c-239">Get information about a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| <span data-ttu-id="2a01c-240">VaultPut</span><span class="sxs-lookup"><span data-stu-id="2a01c-240">VaultPut</span></span> |[<span data-ttu-id="2a01c-241">Een sleutelkluis maken of bijwerken</span><span class="sxs-lookup"><span data-stu-id="2a01c-241">Create or update a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| <span data-ttu-id="2a01c-242">VaultDelete</span><span class="sxs-lookup"><span data-stu-id="2a01c-242">VaultDelete</span></span> |[<span data-ttu-id="2a01c-243">Een sleutelkluis verwijderen</span><span class="sxs-lookup"><span data-stu-id="2a01c-243">Delete a key vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| <span data-ttu-id="2a01c-244">VaultPatch</span><span class="sxs-lookup"><span data-stu-id="2a01c-244">VaultPatch</span></span> |[<span data-ttu-id="2a01c-245">Een sleutelkluis bijwerken</span><span class="sxs-lookup"><span data-stu-id="2a01c-245">Update a key vault</span></span>](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| <span data-ttu-id="2a01c-246">VaultList</span><span class="sxs-lookup"><span data-stu-id="2a01c-246">VaultList</span></span> |[<span data-ttu-id="2a01c-247">Alle sleutelkluizen in een resourcegroep weergeven</span><span class="sxs-lookup"><span data-stu-id="2a01c-247">List all key vaults in a resource group</span></span>](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| <span data-ttu-id="2a01c-248">KeyCreate</span><span class="sxs-lookup"><span data-stu-id="2a01c-248">KeyCreate</span></span> |[<span data-ttu-id="2a01c-249">Een sleutel maken</span><span class="sxs-lookup"><span data-stu-id="2a01c-249">Create a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| <span data-ttu-id="2a01c-250">KeyGet</span><span class="sxs-lookup"><span data-stu-id="2a01c-250">KeyGet</span></span> |[<span data-ttu-id="2a01c-251">Informatie over een sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="2a01c-251">Get information about a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| <span data-ttu-id="2a01c-252">KeyImport</span><span class="sxs-lookup"><span data-stu-id="2a01c-252">KeyImport</span></span> |[<span data-ttu-id="2a01c-253">Een sleutel in een kluis importeren</span><span class="sxs-lookup"><span data-stu-id="2a01c-253">Import a key into a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| <span data-ttu-id="2a01c-254">KeyBackup</span><span class="sxs-lookup"><span data-stu-id="2a01c-254">KeyBackup</span></span> |<span data-ttu-id="2a01c-255">[Back-up maken van een sleutel](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span><span class="sxs-lookup"><span data-stu-id="2a01c-255">[Backup a key](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx).</span></span> |
| <span data-ttu-id="2a01c-256">KeyDelete</span><span class="sxs-lookup"><span data-stu-id="2a01c-256">KeyDelete</span></span> |[<span data-ttu-id="2a01c-257">Een sleutel verwijderen</span><span class="sxs-lookup"><span data-stu-id="2a01c-257">Delete a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| <span data-ttu-id="2a01c-258">KeyRestore</span><span class="sxs-lookup"><span data-stu-id="2a01c-258">KeyRestore</span></span> |[<span data-ttu-id="2a01c-259">Een sleutel herstellen</span><span class="sxs-lookup"><span data-stu-id="2a01c-259">Restore a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| <span data-ttu-id="2a01c-260">KeySign</span><span class="sxs-lookup"><span data-stu-id="2a01c-260">KeySign</span></span> |[<span data-ttu-id="2a01c-261">Aanmelden met een sleutel</span><span class="sxs-lookup"><span data-stu-id="2a01c-261">Sign with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| <span data-ttu-id="2a01c-262">KeyVerify</span><span class="sxs-lookup"><span data-stu-id="2a01c-262">KeyVerify</span></span> |[<span data-ttu-id="2a01c-263">Verifiëren met een sleutel</span><span class="sxs-lookup"><span data-stu-id="2a01c-263">Verify with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| <span data-ttu-id="2a01c-264">KeyWrap</span><span class="sxs-lookup"><span data-stu-id="2a01c-264">KeyWrap</span></span> |[<span data-ttu-id="2a01c-265">Een sleutel inpakken</span><span class="sxs-lookup"><span data-stu-id="2a01c-265">Wrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| <span data-ttu-id="2a01c-266">KeyUnwrap</span><span class="sxs-lookup"><span data-stu-id="2a01c-266">KeyUnwrap</span></span> |[<span data-ttu-id="2a01c-267">Een sleutel uitpakken</span><span class="sxs-lookup"><span data-stu-id="2a01c-267">Unwrap a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| <span data-ttu-id="2a01c-268">KeyEncrypt</span><span class="sxs-lookup"><span data-stu-id="2a01c-268">KeyEncrypt</span></span> |[<span data-ttu-id="2a01c-269">Versleutelen met een sleutel</span><span class="sxs-lookup"><span data-stu-id="2a01c-269">Encrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| <span data-ttu-id="2a01c-270">KeyDecrypt</span><span class="sxs-lookup"><span data-stu-id="2a01c-270">KeyDecrypt</span></span> |[<span data-ttu-id="2a01c-271">Ontsleutelen met een sleutel</span><span class="sxs-lookup"><span data-stu-id="2a01c-271">Decrypt with a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| <span data-ttu-id="2a01c-272">KeyUpdate</span><span class="sxs-lookup"><span data-stu-id="2a01c-272">KeyUpdate</span></span> |[<span data-ttu-id="2a01c-273">Een sleutel bijwerken</span><span class="sxs-lookup"><span data-stu-id="2a01c-273">Update a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| <span data-ttu-id="2a01c-274">KeyList</span><span class="sxs-lookup"><span data-stu-id="2a01c-274">KeyList</span></span> |[<span data-ttu-id="2a01c-275">Lijst Hallo sleutels in een kluis</span><span class="sxs-lookup"><span data-stu-id="2a01c-275">List hello keys in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| <span data-ttu-id="2a01c-276">KeyListVersions</span><span class="sxs-lookup"><span data-stu-id="2a01c-276">KeyListVersions</span></span> |[<span data-ttu-id="2a01c-277">Lijst Hallo versies van een sleutel</span><span class="sxs-lookup"><span data-stu-id="2a01c-277">List hello versions of a key</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| <span data-ttu-id="2a01c-278">SecretSet</span><span class="sxs-lookup"><span data-stu-id="2a01c-278">SecretSet</span></span> |[<span data-ttu-id="2a01c-279">Een geheim maken</span><span class="sxs-lookup"><span data-stu-id="2a01c-279">Create a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| <span data-ttu-id="2a01c-280">SecretGet</span><span class="sxs-lookup"><span data-stu-id="2a01c-280">SecretGet</span></span> |[<span data-ttu-id="2a01c-281">Een geheim ophalen</span><span class="sxs-lookup"><span data-stu-id="2a01c-281">Get secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| <span data-ttu-id="2a01c-282">SecretUpdate</span><span class="sxs-lookup"><span data-stu-id="2a01c-282">SecretUpdate</span></span> |[<span data-ttu-id="2a01c-283">Een geheim bijwerken</span><span class="sxs-lookup"><span data-stu-id="2a01c-283">Update a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| <span data-ttu-id="2a01c-284">SecretDelete</span><span class="sxs-lookup"><span data-stu-id="2a01c-284">SecretDelete</span></span> |[<span data-ttu-id="2a01c-285">Een geheim verwijderen</span><span class="sxs-lookup"><span data-stu-id="2a01c-285">Delete a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| <span data-ttu-id="2a01c-286">SecretList</span><span class="sxs-lookup"><span data-stu-id="2a01c-286">SecretList</span></span> |[<span data-ttu-id="2a01c-287">Geheimen in een kluis weergeven</span><span class="sxs-lookup"><span data-stu-id="2a01c-287">List secrets in a vault</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| <span data-ttu-id="2a01c-288">SecretListVersions</span><span class="sxs-lookup"><span data-stu-id="2a01c-288">SecretListVersions</span></span> |[<span data-ttu-id="2a01c-289">Versies van een geheim weergeven</span><span class="sxs-lookup"><span data-stu-id="2a01c-289">List versions of a secret</span></span>](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <span data-ttu-id="2a01c-290"><a id="loganalytics"></a>Log Analytics gebruiken</span><span class="sxs-lookup"><span data-stu-id="2a01c-290"><a id="loganalytics"></a>Use Log Analytics</span></span>

<span data-ttu-id="2a01c-291">U kunt hello Azure Key Vault oplossing gebruiken in logboekanalyse tooreview die Azure Key Vault AuditEvent registreert.</span><span class="sxs-lookup"><span data-stu-id="2a01c-291">You can use hello Azure Key Vault solution in Log Analytics tooreview Azure Key Vault AuditEvent logs.</span></span> <span data-ttu-id="2a01c-292">Voor meer informatie, inclusief hoe tooset, Zie [oplossing voor Azure Sleutelkluis in logboekanalyse](../log-analytics/log-analytics-azure-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="2a01c-292">For more information, including how tooset this up, see [Azure Key Vault solution in Log Analytics](../log-analytics/log-analytics-azure-key-vault.md).</span></span> <span data-ttu-id="2a01c-293">In dit artikel bevat ook instructies als u nodig hebt toomigrate van het oude Sleutelkluis oplossing hello, die wordt aangeboden tijdens Hallo logboekanalyse preview, waarbij u eerst gerouteerd uw logboeken tooan Azure Storage-account en Log Analytics tooread van daaruit geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="2a01c-293">This article also contains instructions if you need toomigrate from hello old Key Vault solution that was offered during hello Log Analytics preview, where you first routed your logs tooan Azure Storage account and configured Log Analytics tooread from there.</span></span>

## <span data-ttu-id="2a01c-294"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a01c-294"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="2a01c-295">Zie [Azure Key Vault in een webtoepassing gebruiken](key-vault-use-from-web-application.md) voor een zelfstudie over het gebruik van Azure Key Vault in een webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="2a01c-295">For a tutorial that uses Azure Key Vault in a web application, see [Use Azure Key Vault from a Web Application](key-vault-use-from-web-application.md).</span></span>

<span data-ttu-id="2a01c-296">Zie voor het programmeren van verwijzingen [Hallo ontwikkelaarshandleiding Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2a01c-296">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

<span data-ttu-id="2a01c-297">Zie [Cmdlets voor Azure Sleutelkluis](/powershell/module/azurerm.keyvault/#key_vault) voor een lijst met Azure PowerShell 1.0- cmdlets voor Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2a01c-297">For a list of Azure PowerShell 1.0 cmdlets for Azure Key Vault, see [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault).</span></span>

<span data-ttu-id="2a01c-298">Zie voor een zelfstudie over de sleutel worden gedraaid en logboek controle met Azure Sleutelkluis, [hoe toosetup Sleutelkluis met einde tooend sleutel worden gedraaid en controle](key-vault-key-rotation-log-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="2a01c-298">For a tutorial on key rotation and log auditing with Azure Key Vault, see [How toosetup Key Vault with end tooend key rotation and auditing](key-vault-key-rotation-log-monitoring.md).</span></span>

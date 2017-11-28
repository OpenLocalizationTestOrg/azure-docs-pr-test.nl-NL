---
title: Voorbeelden van aaaAzure Monitor CLI 1.0 snel starten. | Microsoft Docs
description: CLI-1.0 Voorbeeldopdrachten voor Monitor van de Azure-functies. Monitor voor Azure is een Microsoft Azure-service waarmee u waarschuwingsmeldingen toosend, aanroep web-URL's op basis van waarden van de geconfigureerde telemetriegegevens, en voor automatisch schalen Cloudservices, virtuele Machines en Web-Apps.
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="ccd93-105">Azure Monitor platformoverschrijdende CLI 1.0 snel starten-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="ccd93-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="ccd93-106">In dit artikel aangegeven dat u een opdrachtregelinterface (CLI) opdrachten toohelp u toegang tot Azure Monitor functies steekproef nemen.</span><span class="sxs-lookup"><span data-stu-id="ccd93-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="ccd93-107">Monitor voor Azure kunt u tooAutoScale Cloudservices, virtuele Machines en Web-Apps en toosend waarschuwingsmeldingen of een aanroep van web-URL's op basis van waarden van de geconfigureerde telemetrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="ccd93-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd93-108">Nieuwe naam op voor het zogenoemde 'Azure Insights' hello is Azure Monitor tot 25 september 2016.</span><span class="sxs-lookup"><span data-stu-id="ccd93-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="ccd93-109">Echter bevatten Hallo naamruimten, en daarom onderstaande Hallo-opdrachten nog steeds Hallo 'insights'.</span><span class="sxs-lookup"><span data-stu-id="ccd93-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ccd93-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ccd93-110">Prerequisites</span></span>
<span data-ttu-id="ccd93-111">Als u nog niet hello Azure CLI hebt geïnstalleerd, raadpleegt u [installeren hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="ccd93-112">Als u niet bekend met Azure CLI bent, vindt u meer over op het [gebruik hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="ccd93-113">In Windows, installeert u npm van Hallo [Node.js website](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="ccd93-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="ccd93-114">Nadat u Hallo-installatie hebt voltooid, CMD.exe met bevoegdheden als Administrator uitvoeren, met de volgende Hallo van Hallo-map waarin de npm is geïnstalleerd uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ccd93-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="ccd93-115">Ga vervolgens tooany/maplocatie u wilt en typt u bij Hallo opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="ccd93-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="ccd93-116">Meld u bij tooAzure</span><span class="sxs-lookup"><span data-stu-id="ccd93-116">Log in tooAzure</span></span>
<span data-ttu-id="ccd93-117">de eerste stap Hallo is toologin tooyour Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ccd93-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="ccd93-118">Wanneer u deze opdracht uitvoert, beschikt u over toosign in via Hallo instructies voor het welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="ccd93-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="ccd93-119">Hierna ziet u uw Account, TenantId en standaard abonnements-id. In de context van uw standaardabonnement Hallo gebruikmaken van alle opdrachten.</span><span class="sxs-lookup"><span data-stu-id="ccd93-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="ccd93-120">toolist hello details van uw huidige abonnement gebruiken Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="ccd93-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="ccd93-121">toochange werkende context tooa ander abonnement, gebruik Hallo opdracht te volgen.</span><span class="sxs-lookup"><span data-stu-id="ccd93-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="ccd93-122">toouse Azure resourcemanager en Azure Monitor opdrachten, moet u toobe in de modus Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ccd93-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="ccd93-123">een lijst met alle ondersteunde Azure-Monitor opdrachten tooview Hallo volgende uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ccd93-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="ccd93-124">Activiteitenlogboek weergeven voor een abonnement</span><span class="sxs-lookup"><span data-stu-id="ccd93-124">View activity log for a subscription</span></span>
<span data-ttu-id="ccd93-125">een lijst met activiteitsgebeurtenissen, tooview Hallo volgende uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ccd93-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="ccd93-126">Probeer Hallo tooview na alle beschikbare opties.</span><span class="sxs-lookup"><span data-stu-id="ccd93-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="ccd93-127">Hier volgt een voorbeeld toolist Logboeken door een resourceGroup</span><span class="sxs-lookup"><span data-stu-id="ccd93-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="ccd93-128">Voorbeeld toolist Logboeken door de oproepende functie</span><span class="sxs-lookup"><span data-stu-id="ccd93-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="ccd93-129">Voorbeeld toolist Logboeken door de oproepende functie op een resourcetype binnen een begin- en datum</span><span class="sxs-lookup"><span data-stu-id="ccd93-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="ccd93-130">Werken met waarschuwingen</span><span class="sxs-lookup"><span data-stu-id="ccd93-130">Work with alerts</span></span>
<span data-ttu-id="ccd93-131">U kunt Hallo informatie gebruiken in Hallo sectie toowork met waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="ccd93-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="ccd93-132">Waarschuwingsregels in een resourcegroep ophalen</span><span class="sxs-lookup"><span data-stu-id="ccd93-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="ccd93-133">Een metriek waarschuwingsregel maken</span><span class="sxs-lookup"><span data-stu-id="ccd93-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="ccd93-134">Waarschuwingsregel voor webtest maken</span><span class="sxs-lookup"><span data-stu-id="ccd93-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="ccd93-135">Een waarschuwingsregel verwijderen</span><span class="sxs-lookup"><span data-stu-id="ccd93-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="ccd93-136">Logboek-profielen</span><span class="sxs-lookup"><span data-stu-id="ccd93-136">Log profiles</span></span>
<span data-ttu-id="ccd93-137">Hallo-informatie in deze sectie toowork met logboek profielen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ccd93-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="ccd93-138">Een profiel voor een logboek ophalen</span><span class="sxs-lookup"><span data-stu-id="ccd93-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="ccd93-139">Een profiel logboek zonder bewaren toevoegen</span><span class="sxs-lookup"><span data-stu-id="ccd93-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="ccd93-140">Een logboek-profiel verwijderen</span><span class="sxs-lookup"><span data-stu-id="ccd93-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="ccd93-141">Een profiel van het logboek met bewaren toevoegen</span><span class="sxs-lookup"><span data-stu-id="ccd93-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="ccd93-142">Een profiel van het logboek met bewaren en EventHub toevoegen</span><span class="sxs-lookup"><span data-stu-id="ccd93-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="ccd93-143">Diagnostiek</span><span class="sxs-lookup"><span data-stu-id="ccd93-143">Diagnostics</span></span>
<span data-ttu-id="ccd93-144">Gebruik Hallo informatie in deze sectie toowork met diagnostische instellingen.</span><span class="sxs-lookup"><span data-stu-id="ccd93-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="ccd93-145">Een diagnostische instelling ophalen</span><span class="sxs-lookup"><span data-stu-id="ccd93-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="ccd93-146">Een diagnostische instelling uitschakelen</span><span class="sxs-lookup"><span data-stu-id="ccd93-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="ccd93-147">Een diagnostische instelling zonder bewaren inschakelen</span><span class="sxs-lookup"><span data-stu-id="ccd93-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="ccd93-148">Automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="ccd93-148">Autoscale</span></span>
<span data-ttu-id="ccd93-149">Gebruik Hallo informatie in deze sectie toowork met instellingen voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="ccd93-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="ccd93-150">U moet deze voorbeelden toomodify.</span><span class="sxs-lookup"><span data-stu-id="ccd93-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="ccd93-151">Instellingen voor automatisch schalen voor een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="ccd93-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="ccd93-152">Instellingen voor automatisch schalen die u op naam in een resourcegroep</span><span class="sxs-lookup"><span data-stu-id="ccd93-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="ccd93-153">Instellingen voor het auotoscale</span><span class="sxs-lookup"><span data-stu-id="ccd93-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```

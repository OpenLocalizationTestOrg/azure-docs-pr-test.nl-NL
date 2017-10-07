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
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a>Azure Monitor platformoverschrijdende CLI 1.0 snel starten-voorbeelden
In dit artikel aangegeven dat u een opdrachtregelinterface (CLI) opdrachten toohelp u toegang tot Azure Monitor functies steekproef nemen. Monitor voor Azure kunt u tooAutoScale Cloudservices, virtuele Machines en Web-Apps en toosend waarschuwingsmeldingen of een aanroep van web-URL's op basis van waarden van de geconfigureerde telemetrische gegevens.

> [!NOTE]
> Nieuwe naam op voor het zogenoemde 'Azure Insights' hello is Azure Monitor tot 25 september 2016. Echter bevatten Hallo naamruimten, en daarom onderstaande Hallo-opdrachten nog steeds Hallo 'insights'.
> 
> 

## <a name="prerequisites"></a>Vereisten
Als u nog niet hello Azure CLI hebt geïnstalleerd, raadpleegt u [installeren hello Azure CLI](../cli-install-nodejs.md). Als u niet bekend met Azure CLI bent, vindt u meer over op het [gebruik hello Azure CLI voor Mac, Linux en Windows Azure Resource Manager](../xplat-cli-azure-resource-manager.md).

In Windows, installeert u npm van Hallo [Node.js website](https://nodejs.org/). Nadat u Hallo-installatie hebt voltooid, CMD.exe met bevoegdheden als Administrator uitvoeren, met de volgende Hallo van Hallo-map waarin de npm is geïnstalleerd uitvoeren:

```console
npm install azure-cli --global
```

Ga vervolgens tooany/maplocatie u wilt en typt u bij Hallo opdrachtregel:

```console
azure help
```

## <a name="log-in-tooazure"></a>Meld u bij tooAzure
de eerste stap Hallo is toologin tooyour Azure-account.

```console
azure login
```

Wanneer u deze opdracht uitvoert, beschikt u over toosign in via Hallo instructies voor het welkomstscherm. Hierna ziet u uw Account, TenantId en standaard abonnements-id. In de context van uw standaardabonnement Hallo gebruikmaken van alle opdrachten.

toolist hello details van uw huidige abonnement gebruiken Hallo opdracht te volgen.

```console
azure account show
```

toochange werkende context tooa ander abonnement, gebruik Hallo opdracht te volgen.

```console
azure account set "subscription ID or subscription name"
```

toouse Azure resourcemanager en Azure Monitor opdrachten, moet u toobe in de modus Azure Resource Manager.

```console
azure config mode arm
```

een lijst met alle ondersteunde Azure-Monitor opdrachten tooview Hallo volgende uitvoeren.

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a>Activiteitenlogboek weergeven voor een abonnement
een lijst met activiteitsgebeurtenissen, tooview Hallo volgende uitvoeren.

```console
azure insights logs list [options]
```

Probeer Hallo tooview na alle beschikbare opties.

```console
azure insights logs list -help
```

Hier volgt een voorbeeld toolist Logboeken door een resourceGroup

```console
azure insights logs list --resourceGroup "myrg1"
```

Voorbeeld toolist Logboeken door de oproepende functie

```console
azure insights logs list --caller "myname@company.com"
```

Voorbeeld toolist Logboeken door de oproepende functie op een resourcetype binnen een begin- en datum

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a>Werken met waarschuwingen
U kunt Hallo informatie gebruiken in Hallo sectie toowork met waarschuwingen.

### <a name="get-alert-rules-in-a-resource-group"></a>Waarschuwingsregels in een resourcegroep ophalen
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a>Een metriek waarschuwingsregel maken
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a>Waarschuwingsregel voor webtest maken
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a>Een waarschuwingsregel verwijderen
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a>Logboek-profielen
Hallo-informatie in deze sectie toowork met logboek profielen gebruiken.

### <a name="get-a-log-profile"></a>Een profiel voor een logboek ophalen
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a>Een profiel logboek zonder bewaren toevoegen
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a>Een logboek-profiel verwijderen
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a>Een profiel van het logboek met bewaren toevoegen
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a>Een profiel van het logboek met bewaren en EventHub toevoegen
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a>Diagnostiek
Gebruik Hallo informatie in deze sectie toowork met diagnostische instellingen.

### <a name="get-a-diagnostic-setting"></a>Een diagnostische instelling ophalen
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a>Een diagnostische instelling uitschakelen
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a>Een diagnostische instelling zonder bewaren inschakelen
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a>Automatisch schalen
Gebruik Hallo informatie in deze sectie toowork met instellingen voor automatisch schalen. U moet deze voorbeelden toomodify.

### <a name="get-autoscale-settings-for-a-resource-group"></a>Instellingen voor automatisch schalen voor een resourcegroep
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a>Instellingen voor automatisch schalen die u op naam in een resourcegroep
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a>Instellingen voor het auotoscale
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```

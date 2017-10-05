---
title: Bewaking van Azure Functions | Microsoft Docs
description: Informatie over het bewaken van uw Azure-functies.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: b70214593b1417265387f42306a633bb0df2920e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-azure-functions"></a>Azure Functions controleren

## <a name="overview"></a>Overzicht 


De **Monitor** tabblad voor elke functie u deze kunt kunt bekijken van elke uitvoering van een functie.

![Tabblad van Azure Functions-monitor](./media/functions-monitoring/monitor-tab.png) 

Op uitvoering van een, kunt u deze kunt bekijken van de duur van de invoergegevens, fouten en bijbehorende logboekbestanden. Dit is handig voor foutopsporing en prestaties afstemmen van uw functies.


> [!IMPORTANT]
> Wanneer u de [verbruik die als host fungeert voor plan](functions-overview.md#pricing) voor Azure Functions, de **bewaking** tegel in de overzichtsblade van functie-App niet alle gegevens weergegeven. Dit is omdat het platform dynamisch schaalbaar en beheert de compute-exemplaren voor u, zodat deze metrische gegevens niet op een plan verbruik zinvolle zijn. Als u wilt het gebruik van uw Apps functie bewaken, moet u in plaats daarvan de instructies in dit artikel gebruiken.
> 
> De volgende Schermafbeelding toont een voorbeeld:
> 
> ![Bewaking op de belangrijkste resourceblade](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Realtime-controle

Realtime-controle is beschikbaar door te klikken op **stream live gebeurtenis** zoals hieronder wordt weergegeven. 

![Live gebeurtenis stroom optie voor het tabblad monitor](./media/functions-monitoring/monitor-tab-live-event-stream.png)

Wordt in een nieuw browsertabblad een diagram worden weergegeven aan de stroom live gebeurtenissen zoals hieronder wordt weergegeven. 

![Voorbeeld van de stream Live gebeurtenis](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Er is een bekend probleem dat ertoe leiden uw gegevens dat kan niet kunnen worden ingevuld. Als dit zich voordoet, moet u mogelijk het browsertabblad met de stream live gebeurtenis sluiten en klik vervolgens op **stream live gebeurtenis** opnieuw toe te staan dat uw stream gebeurtenisgegevens correct te vullen. 

De stream live gebeurtenis wordt de volgende statistieken voor de functie grafiek:

* Uitvoeringen per seconde is gestart
* Uitvoeringen per seconde worden voltooid
* Uitvoeringen mislukte per seconde
* Gemiddelde uitvoeringstijd in milliseconden.

Deze statistieken zijn realtime maar de werkelijke grafieken van de uitvoering van gegevens mogelijk van de latentie van ongeveer 10 seconden.






## <a name="monitoring-log-files-from-a-command-line"></a>Bewaking van logboekbestanden vanaf een opdrachtregel


U kunt logboekbestanden met een opdrachtregel-sessie op een lokaal werkstation met de Azure-opdrachtregelinterface (CLI) of PowerShell streamen.

### <a name="monitoring-function-app-log-files-with-the-azure-cli"></a>Bewaking van de functie app-logboekbestanden met de Azure CLI

Aan de slag [Azure CLI installeren](../cli-install-nodejs.md)

Meld u aan bij uw Azure-account met de volgende opdracht of een van de andere opties behandeld in, [aanmelden bij Azure met Azure CLI](../xplat-cli-connect.md).

    azure login

Gebruik de volgende opdracht om te kunnen inschakelen voor Azure CLI Service Management (ASM):.

    azure config mode asm

Als u meerdere abonnementen hebt, gebruikt u de volgende opdrachten om te lijst van uw abonnementen en het huidige abonnement aan het abonnement dat functie-app bevat.

    azure account list
    azure account set <subscriptionNameOrId>

De volgende opdracht wordt de logboekbestanden van uw app functie aan de opdrachtregel stream:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Bewaking van de functie app-logboekbestanden met PowerShell

Aan de slag [Azure PowerShell installeren en configureren](/powershell/azure/overview).

Uw Azure-account toevoegen met de volgende opdracht:

    PS C:\> Add-AzureAccount

Als u meerdere abonnementen hebt, kunt u deze met de naam met de volgende opdracht om te zien of het juiste abonnement de momenteel geselecteerde op basis van vermelden `IsCurrent` eigenschap:

    PS C:\> Get-AzureSubscription

Als u de actief abonnement met de functie-app met instellen moet, gebruikt u de volgende opdracht:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Stream de logboeken naar uw PowerShell-sessie met de volgende opdracht:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Raadpleeg voor meer informatie [hoe: logboeken voor web-apps Stream](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Volgende stappen
Zie de volgende bronnen voor meer informatie:

* [Een functie testen](functions-test-a-function.md)
* [Een functie schalen](functions-scale.md)


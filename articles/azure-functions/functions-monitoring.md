---
title: aaaMonitoring Azure Functions | Microsoft Docs
description: Meer informatie over hoe toomonitor uw Azure-functies.
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
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a>Azure Functions controleren

## <a name="overview"></a>Overzicht 


Hallo **Monitor** tabblad voor elke functie u tooreview kunt elke uitvoering van een functie.

![Tabblad van Azure Functions-monitor](./media/functions-monitoring/monitor-tab.png) 

Een uitvoering klikken kunt u tooreview Hallo duur, invoergegevens, fouten en bijbehorende logboekbestanden. Dit is handig voor foutopsporing en prestaties afstemmen van uw functies.


> [!IMPORTANT]
> Wanneer u Hallo [verbruik die als host fungeert voor plan](functions-overview.md#pricing) voor Azure Functions Hallo **bewaking** tegel in overzichtsblade Hallo-functie-App niet alle gegevens weergegeven. Dit is omdat dynamisch schaalbaar en beheert de compute-exemplaren voor u, zodat deze metrische gegevens niet op een plan verbruik zinvolle zijn Hallo-platform. toomonitor hello gebruik van de functie-Apps, moet u in plaats daarvan gebruiken Hallo richtlijnen in dit artikel.
> 
> Hallo-schermopname na toont een voorbeeld:
> 
> ![Bewaking op de belangrijkste resourceblade Hallo](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a>Realtime-controle

Realtime-controle is beschikbaar door te klikken op **stream live gebeurtenis** zoals hieronder wordt weergegeven. 

![Live gebeurtenis stroom optie voor tabblad Hallo-monitor](./media/functions-monitoring/monitor-tab-live-event-stream.png)

wordt in een nieuw browsertabblad een diagram worden weergegeven aan Hallo live gebeurtenisstroom zoals hieronder wordt weergegeven. 

![Voorbeeld van de stream Live gebeurtenis](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> Er is een bekend probleem dat ertoe leiden uw gegevens toofail toobe ingevuld dat kan. Als u dit ondervindt, moet u mogelijk tooclose Hallo browser tabblad met Hallo live gebeurtenisstroom en klik vervolgens op **stream live gebeurtenis** opnieuw tooallow het tooproperly de gebeurtenisgegevens stroom vullen. 

Hallo live gebeurtenisstroom wordt graph Hallo statistieken voor uw functie te volgen:

* Uitvoeringen per seconde is gestart
* Uitvoeringen per seconde worden voltooid
* Uitvoeringen mislukte per seconde
* Gemiddelde uitvoeringstijd in milliseconden.

Deze statistieken zijn realtime maar werkelijke grafieken van uitvoeringsgegevens Hallo Hallo mogelijk van de latentie van ongeveer 10 seconden.






## <a name="monitoring-log-files-from-a-command-line"></a>Bewaking van logboekbestanden vanaf een opdrachtregel


U kunt logboek bestanden tooa opdrachtregel sessie op een lokaal werkstation met hello Azure-opdrachtregelinterface (CLI) of PowerShell streamen.

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a>Bewaking van de functie app-logboekbestanden Hello Azure CLI

tooget gestart, [hello Azure CLI installeren](../cli-install-nodejs.md)

Meld u aan bij uw Azure-account met de volgende Hallo opdracht of een van de andere opties behandeld in, Hallo [tooAzure van hello Azure CLI aanmelden](../xplat-cli-connect.md).

    azure login

Gebruik Hallo volgende opdracht tooenable Azure CLI Service Management (ASM) modus:.

    azure config mode asm

Als u meerdere abonnementen hebt, gebruik Hallo opdrachten toolist na uw abonnementen en set Hallo huidige abonnement toohello abonnement dat functie-app bevat.

    azure account list
    azure account set <subscriptionNameOrId>

Hallo wordt volgende opdracht stream Hallo logboekbestanden van de functie app toohello vanaf de opdrachtregel:

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a>Bewaking van de functie app-logboekbestanden met PowerShell

tooget gestart, [Azure PowerShell installeren en configureren](/powershell/azure/overview).

Uw Azure-account toevoegen door te voeren Hallo volgende opdracht:

    PS C:\> Add-AzureAccount

Als u meerdere abonnementen hebt, kunt u deze weergeven met de naam met volgende opdracht toosee als het juiste abonnement is geselecteerd Hallo Hallo op basis van hello `IsCurrent` eigenschap:

    PS C:\> Get-AzureSubscription

Als u tooset Hallo actief abonnement toohello met de functie-app moet, gebruikt u Hallo volgende opdracht:

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

Stroom Hallo logboeken tooyour PowerShell-sessie met Hallo volgende opdracht:

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

Voor meer informatie raadpleegt u te[hoe: logboeken voor web-apps Stream](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs). 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie Hallo resources te volgen:

* [Een functie testen](functions-test-a-function.md)
* [Een functie schalen](functions-scale.md)


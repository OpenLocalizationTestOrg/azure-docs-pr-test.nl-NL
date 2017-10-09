---
title: een nieuwe Azure Application Insights-resource aaaCreate | Microsoft Docs
description: Stel handmatig bewaking van de Application Insights voor een nieuwe live-toepassing.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Een Application Insights-resource maken
Azure Application Insights gegevens over uw toepassing worden weergegeven in een Microsoft Azure *resource*. Een nieuwe resource daarom deel uitmaakt van [toomonitor Application Insights instellen met een nieuwe toepassing][start]. In veel gevallen kan maken van een resource automatisch worden gedaan door Hallo IDE. Maar in sommige gevallen u Maak handmatig een resource - bijvoorbeeld afzonderlijke resources voor ontwikkeling en productie toohave builds van uw toepassing.

Nadat u Hallo resource hebt gemaakt, kunt u de instrumentatiesleutel ophalen en die tooconfigure Hallo SDK in de toepassing hello gebruiken. sleutel resourcekoppelingen Hallo Hallo telemetrie toohello resource.

## <a name="sign-up-toomicrosoft-azure"></a>TooMicrosoft Azure registreren
Als u dit nog niet hebt verkregen een [Microsoft-account, nu](http://live.com). (Als u gebruikmaakt van services zoals Outlook.com, OneDrive, Windows Phone of XBox Live, u hebt al een Microsoft-account.)

U moet ook een abonnement te[Microsoft Azure](http://azure.com). Eigenaar als uw team of organisatie een Azure-abonnement heeft, Hallo kan u toevoegen tooit, met behulp van uw Windows Live ID. U bent alleen kosten in rekening gebracht voor wat u gebruikt. Hallo standaard basisniveau kunt u een bepaalde hoeveelheid experimenteel gebruik gratis.

Als u toegang tooa abonnement hebt, aanmelden tooApplication Insights op [http://portal.azure.com](https://portal.azure.com), en uw toologin Live ID gebruiken.

## <a name="create-an-application-insights-resource"></a>Een Application Insights-resource maken
In Hallo [portal.azure.com](https://portal.azure.com), een Application Insights-resource toevoegen:

![Klik op Nieuw > Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **Toepassingstype** is van invloed op wat er op de blade overzicht Hallo en Hallo eigenschappen beschikbaar zijn in [metrische explorer][metrics]. Als u uw app-type niet ziet, kiest u algemene.
* **Abonnement** is uw betaling-account in Azure.
* **Resourcegroep** is nuttig voor het beheren van eigenschappen zoals toegangsbeheer. Als u andere Azure-resources al hebt gemaakt, kunt u kiezen tooput deze nieuwe bron in Hallo dezelfde groep.
* **Locatie** is waar we uw gegevens wilt bewaren.
* **Pincode toodashboard** plaatst u een snelle toegang tegel voor uw resource op de startpagina van Azure. Aanbevolen.

Wanneer uw app is gemaakt, wordt er een nieuwe blade geopend. Deze blade is waar u prestatie- en gebruiksgegevens over uw app bekijken. 

tooget back tooit volgende keer dat u zich aanmeldt tooAzure, zoeken naar uw app snel starten-tegel op Hallo start board (startscherm). Of klik op Bladeren toofind deze.

## <a name="copy-hello-instrumentation-key"></a>Hallo-instrumentatiesleutel kopiëren
de instrumentatiesleutel Hallo identificeert Hallo resource die u hebt gemaakt. U moet toogive toohello SDK.

![Klik op Essentials, Hallo Instrumentatiesleutel, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Hallo SDK installeren in uw app
Hallo Application Insights-SDK installeren in uw app. Deze stap is afhankelijk van geheugenlatentie Hallo-type van uw toepassing. 

Gebruik Hallo instrumentation sleutel tooconfigure [SDK die u in uw toepassing installeert hello][start].

Hallo SDK bevat standaard modules die telemetrie zonder dat u toowrite code hoeft te verzenden. tootrack gebruikersacties of het analyseren van problemen in meer detail [Hallo API gebruiken] [ api] toosend uw eigen telemetrie.

## <a name="monitor"></a>Zie telemetriegegevens
Blade tooreturn tooyour toepassing blade sluiten Hallo snel starten in hello Azure-portal.

Klik op Hallo zoeken tegel toosee [diagnostische gegevens doorzoeken][diagnostic], waarbij Hallo eerste gebeurtenissen worden weergegeven. 

Als u meer gegevens verwacht, klikt u op **vernieuwen** na enkele seconden.

## <a name="creating-a-resource-automatically"></a>Het automatisch maken van een resource
U kunt schrijven een [PowerShell-script](app-insights-powershell.md) toocreate een resource automatisch.

## <a name="next-steps"></a>Volgende stappen
* [Een dashboard maken](app-insights-dashboards.md)
* [Diagnostische gegevens doorzoeken](app-insights-diagnostic-search.md)
* [Metrische gegevens verkennen](app-insights-metrics-explorer.md)
* [Analytics-query's schrijven](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md


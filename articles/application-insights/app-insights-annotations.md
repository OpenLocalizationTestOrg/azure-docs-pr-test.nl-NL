---
title: aaaRelease aantekeningen voor Application Insights | Microsoft Docs
description: Implementatie toevoegen of bouwen markeringen tooyour metrics explorer-grafieken in Application Insights.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Aantekeningen voor metrische grafieken in Application Insights
Aantekeningen op [Metrics Explorer](app-insights-metrics-explorer.md) grafieken weergegeven waarin u een nieuwe build, of een andere belangrijke gebeurtenis geïmplementeerd. Ze maken het gemakkelijk toosee of uw wijzigingen geen effect op de prestaties van uw toepassing heeft. Ze kunnen automatisch gemaakt door Hallo [Visual Studio Team Services bouwen system](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). U kunt aantekeningen tooflag ook maken een gebeurtenis die u met wilt [ze worden gemaakt vanuit PowerShell](#create-annotations-from-powershell).

![Voorbeeld van aantekeningen met zichtbaar correlatie met serverreactietijd](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Release aantekeningen met VSTS build

Release aantekeningen zijn een functie van cloud-gebaseerde Hallo-build en release van service van het Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Hallo aantekeningen uitbreiding (eenmaal) installeren
toobe kunnen toocreate release aantekeningen, moet u tooinstall een Hallo Hallo veel Team extensies beschikbaar zijn in Visual Studio Marketplace.

1. Meld u aan tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) project.
2. In Visual Studio Marketplace, [Hallo Release aantekeningen uitbreiding](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations), en voeg deze tooyour Team Services-account.

![AT top rechts van de webpagina Team Services, open Marketplace. Selecteer Visual Team Services en onder Build en Release, kies meer.](./media/app-insights-annotations/10.png)

U hoeft alleen toodo dit eenmaal voor uw Visual Studio Team Services-account. Release aantekeningen kunnen nu worden geconfigureerd voor elk project in uw account. 

### <a name="configure-release-annotations"></a>Release aantekeningen configureren

Tooget een afzonderlijke API-sleutel moet u voor elke release VSTS sjabloon.

1. Meld u aan toohello [Microsoft Azure Portal](https://portal.azure.com) en open Hallo Application Insights-resource die wordt uw toepassing bewaakt. (Of [er nu een maken](app-insights-overview.md), als u dit nog niet hebt gedaan.)
2. Open **API-toegang**, **Application Insights-Id**.
   
    ![Open uw Application Insights-resource in portal.azure.com en instellingen kiezen. Open API-toegang. Kopieer Hallo toepassings-ID](./media/app-insights-annotations/20.png)

4. Open (of maak) in een nieuw browservenster op Hallo releasesjabloon die u uw implementaties van Visual Studio Team Services beheert. 
   
    Een taak toevoegen en selecteer Hallo Application Insights Release aantekening taak in Hallo-menu.
   
    Plakken Hallo **toepassings-Id** die u hebt gekopieerd uit Hallo blade API-toegang.
   
    ![Release openen in Visual Studio Team Services, selecteert u de definitie van een release en kies bewerken. Klik op taak toevoegen en selecteer Application Insights Release aantekening. Plak Hallo Application Insights-id.](./media/app-insights-annotations/30.png)
4. Set Hallo **APIKey** veld tooa variabele `$(ApiKey)`.

5. Terug in Azure venster hello, maak een nieuwe API-sleutel en een kopie van deze.
   
    ![Klik in de blade API-toegang in hello Azure venster Hallo, API-sleutel maken. Geef een opmerking, schrijven aantekeningen, en klik op sleutel genereren. De nieuwe sleutel Hallo kopiëren.](./media/app-insights-annotations/40.png)

6. Open Hallo tabblad van de configuratie van Hallo releasesjabloon.
   
    Maken van een variabele definitie voor `ApiKey`.
   
    Plak uw API-sleutel toohello ApiKey variabele-definitie.
   
    ![Hallo-teamservices venster, selecteer Hallo configuratie tabblad en klik op variabele toevoegen. Hallo naam tooApiKey ingesteld en klikt u op Hallo vergrendelingspictogram in Hallo waarde, plak Hallo-sleutel die u zojuist hebt gegenereerd.](./media/app-insights-annotations/50.png)
7. Ten slotte **opslaan** Hallo release definitie.


## <a name="view-annotations"></a>Weergave aantekeningen
Nu, wanneer u Hallo release sjabloon toodeploy een nieuwe release, van een aantekening wordt verzonden tooApplication Insights. Hallo aantekeningen worden weergegeven op de grafieken in Metrics Explorer.

Klik op de aantekening markering tooopen details over Hallo introductie, met inbegrip van de aanvrager, bron besturingselement vertakking, release-definitie, omgeving en meer.

![Klik op een markering van de aantekening release.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Aangepaste aantekeningen maken vanuit PowerShell
U kunt ook aantekeningen maken van een proces gewenste (zonder tegenover Team System). 


1. Maak een lokale kopie van Hallo [Powershell-script uit GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Hallo toepassings-ID ophalen en maak een API-sleutel vanuit Hallo blade API-toegang.

3. Roep Hallo script als volgt:

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Het is gemakkelijk toomodify Hallo script, bijvoorbeeld toocreate aantekeningen voor Hallo afgelopen.

## <a name="next-steps"></a>Volgende stappen

* [Werkitems maken](app-insights-diagnostic-search.md#create-work-item)
* [Automatisering met PowerShell](app-insights-powershell.md)

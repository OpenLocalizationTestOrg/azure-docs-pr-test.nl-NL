---
title: aaaGet gestart met automatisch schalen in Azure | Microsoft Docs
description: Meer informatie over hoe tooscale uw Azure-resource.
author: rajram
manager: rboucher
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: rajram
ms.openlocfilehash: 6b3c3f4529018dcaf9691c538fec63dfbb3cea06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-autoscale-in-azure"></a>Aan de slag met automatisch schalen in Azure
Dit artikel wordt beschreven hoe tooset uw instellingen voor automatisch schalen voor uw resource in Hallo Microsoft Azure-portal.

Monitor voor automatisch schalen die Azure geldt alleen toovirtual machineschaalsets, cloudservices, Azure App Service-abonnementen en App Service-omgevingen. 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a>Instellingen voor het automatisch schalen in uw abonnement Hallo detecteren
U kunt alle Hallo resources waarvoor automatisch schalen van toepassing in de Azure-Monitor is kan detecteren. Volgende stappen uit voor een stapsgewijze hello gebruiken:

1. Open Hallo [Azure-portal.][1]
2. Klik op Hallo Azure Monitor pictogram in het linkerdeelvenster Hallo.
  ![Open Azure Monitor][2]
3. Klik op **automatisch schalen** tooview alle Hallo bronnen voor welke automatisch schalen is van toepassing, samen met de huidige status voor automatisch schalen.
  ![Automatisch schalen in Azure Monitor detecteren][3]

U kunt Hallo filterdeelvenster gebruiken op de bovenste tooscope Hallo Hallo lijst tooselect resources in een specifieke resourcegroep, specifieke brontypen of een specifieke bron.

Voor elke resource vindt u het huidige aantal exemplaren Hallo en Hallo voor automatisch schalen die status. Hallo automatisch schalen status kan zijn:

- **Niet geconfigureerd**: U hebt automatisch schalen niet nog ingeschakeld voor deze bron.
- **Ingeschakeld**: U hebt automatisch schalen ingeschakeld voor deze bron.
- **Uitgeschakeld**: U hebt automatisch schalen uitgeschakeld voor deze bron.

## <a name="create-your-first-autoscale-setting"></a>Maken van uw eerste instelling voor automatisch schalen

Laten we nu verloopt via een eenvoudige stapsgewijze toocreate uw eerste instelling voor automatisch schalen.

1. Open Hallo **automatisch schalen** blade in Azure Monitor en selecteer een resource die u tooscale wilt. (hello volgende stappen uit een App Service-abonnement gebruiken die zijn gekoppeld aan een web-app. U kunt [uw eerste ASP.NET-web-app maken in Azure in vijf minuten.] [4])
2. Houd er rekening mee dat het huidige aantal exemplaren Hallo 1 is. Klik op **inschakelen voor automatisch schalen**.
  ![Instelling voor de nieuwe web-app schalen][5]
3. Geef een naam voor Hallo schaal instellen en klik vervolgens op **een regel toevoegen**. U ziet Hallo regel schalingsopties dat als een venster context aan de rechterkant Hallo openen. Dit wordt standaard ingesteld Hallo optie tooscale uw exemplaar 1 tellen als Hallo CPU-percentage van de resource Hallo groter is dan 70 procent. Laat het veld op de standaardwaarden en klik op **toevoegen**.
  ![Scale-instelling voor een web-app maken][6]
4. U hebt nu uw eerste schaalregel gemaakt. Houd er rekening mee dat Hallo UX raadt aan best practices en dat ' het verdient aanbeveling toohave schaal als ten minste één regel. " toodo zodat:
  
    a. Klik op **een regel toevoegen**. 

    b. Stel **Operator** te**minder dan**.

    c. Stel **drempelwaarde** te**20**.

    d. Stel **bewerking** te**verkleinen tellen per**.

   U hebt nu een schaalinstelling dat kan worden geschaald out/schalen op basis van CPU-gebruik.
   ![Schalen op basis van CPU][8]
5. Klik op **Opslaan**.

Gefeliciteerd. U hebt nu uw eerste schaal instelling tooautoscale uw web-app op basis van CPU-gebruik gemaakt.

> [!NOTE] 
> Hallo dezelfde stappen zijn van toepassing tooget gestart met een schaal van de virtuele machine instellen of cloud service-rol.

## <a name="other-considerations"></a>Andere overwegingen
### <a name="scale-based-on-a-schedule"></a>Schalen op basis van een planning
Bovendien tooscale op basis van CPU, kunt u instellen schaal anders voor specifieke dagen van week Hallo.

1. Klik op **een scale-voorwaarde toevoegen**.
2. Instelling Hallo scale Hallo-modus en de regels is dezelfde als standaardvoorwaarde voor Hallo Hallo.
3. Selecteer **specifieke dagen herhalen** voor Hallo planning.
4. Selecteer dagen Hallo en Hallo beginnen of eindigen tijd Hallo scale voorwaarde moet worden toegepast.

![Scale-voorwaarde op basis van de planning][9]
### <a name="scale-differently-on-specific-dates"></a>Anders worden geschaald op specifieke datums
Bovendien tooscale op basis van CPU, kunt u instellen schaal anders voor specifieke datums.

1. Klik op **een scale-voorwaarde toevoegen**.
2. Instelling Hallo scale Hallo-modus en de regels is dezelfde als standaardvoorwaarde voor Hallo Hallo.
3. Selecteer **Geef beginnen of eindigen datums** voor Hallo planning.
4. Selecteer Hallo beginnen of eindigen datums en tijden van de Hallo beginnen of eindigen Hallo scale voorwaarde moet worden toegepast.

![Scale-voorwaarde op basis van datums][10]

### <a name="view-hello-scale-history-of-your-resource"></a>Hallo scale geschiedenis van uw resource weergeven
Wanneer de bron wordt geschaald omhoog of omlaag, wordt een gebeurtenis vastgelegd in het gebeurtenissenlogboek Hallo. U kunt Hallo scale geschiedenis van de bron voor Hallo afgelopen 24 uur weergeven door het overschakelen van toohello **Uitvoeringsgeschiedenis** tabblad.

![geschiedenis uitvoeren][11]

Als u wilt dat tooview Hallo voltooid scale geschiedenis (voor omhoog too90 dagen), selecteer **Klik hier toosee meer details**. Hallo activiteitenlogboek wordt geopend met automatisch schalen die vooraf zijn geselecteerd voor uw resource en categorie.

### <a name="view-hello-scale-definition-of-your-resource"></a>Hallo scale definitie van uw resource weergeven
Automatisch schalen is een Azure Resource Manager-bron. U kunt Hallo scale definitie in JSON weergeven door het overschakelen van toohello **JSON** tabblad.

![De definitie van de schaal][12]

U kunt wijzigingen aanbrengen in JSON rechtstreeks, indien nodig. Deze wijzigingen worden weergegeven nadat u deze opslaan.

### <a name="disable-autoscale-and-manually-scale-your-instances"></a>Schakel automatisch schalen en uw exemplaren handmatig schalen
Mogelijk zijn er tijden als u wilt dat uw huidige schaalinstelling toodisable en handmatig schalen uw resource.

Klik op Hallo **uitschakelen voor automatisch schalen** knop Hallo boven.
![Schakel automatisch schalen][13]

> [!NOTE] 
> Deze optie wordt uitgeschakeld voor uw configuratie. Echter, kun je weer tooit nadat u automatisch schalen opnieuw inschakelen. 

U kunt nu het aantal exemplaren dat u wilt dat tooscale toomanually Hallo instellen.

![Set handmatig schalen][14]

U kunt altijd tooAutoscale terugkeren door te klikken op **inschakelen voor automatisch schalen** en vervolgens **opslaan**.

## <a name="next-steps"></a>Volgende stappen
- [Een activiteit logboek waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement maken](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Alle mislukte bewerkingen worden uitgevoerd voor automatisch schalen scale-in/scale-out op uw abonnement voor een activiteit logboek waarschuwing toomonitor maken](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/en-us/azure/app-service-web/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png


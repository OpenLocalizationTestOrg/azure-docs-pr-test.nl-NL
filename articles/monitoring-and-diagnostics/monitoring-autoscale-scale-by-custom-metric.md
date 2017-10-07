---
title: aaaGet gestart met automatisch schalen door aangepaste metrische gegevens in Azure | Microsoft Docs
description: Meer informatie over hoe tooscale uw resource door aangepaste metrische gegevens in Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: ancav
ms.openlocfilehash: d3e268ec322698d0d367361cd9c156b21e0fb6e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a>Aan de slag met automatisch schalen door aangepaste metrische gegevens in Azure
Dit artikel wordt beschreven hoe tooscale uw resource door een aangepaste waarde in Azure-portal.

Azure Monitor automatisch schalen geldt alleen tooVirtual Machine Scale Sets (VMSS), cloudservices, app-serviceabonnementen en app service-omgevingen. 

# <a name="lets-get-started"></a>Hiermee kunnen aan de slag
In dit artikel wordt ervan uitgegaan dat u een web-app met application insights is geconfigureerd hebt. Als u nog geen een hebt, kunt u [Application Insights instellen voor uw ASP.NET-website][1]

- Open [Azure-portal][2]
- Klik op het pictogram in het linkernavigatievenster hello Azure Monitor.
  ![Azure Monitor starten][3]
- Klik op alle Hallo resources voor welke automatisch schalen van toepassing, samen met de huidige status voor automatisch schalen is van tooview instelling voor automatisch schalen ![automatisch schalen in Azure monitor detecteren][4]
- 'Automatisch ' schalen-blade geopend in de Azure-Monitor en selecteer een bron die u wilt dat tooscale
> Opmerking: de onderstaande stappen voor hello gebruiken een app service-plan dat is gekoppeld aan een WebApp die app insights geconfigureerd is.
- Hallo scale instelling blade voor Hallo resource ziet dat het huidige aantal exemplaren Hallo 1. Klik op 'Inschakelen voor automatisch schalen'.
  ![Instelling voor de nieuwe web-app schalen][5]
- Geef een naam voor Hallo schaal instellen en hello, klik op 'Een regel toevoegen'. U ziet Hallo regel schalingsopties dat wordt geopend in een context deelvenster in de rechterzijde Hallo. Standaard wordt uw exemplaar 1 tellen als Hallo CPU percetage van Hallo resource groter is dan 70% van Hallo optie tooscale ingesteld. Metrische bron wijzigen Hallo Hallo boven te 'Application Insights', selecteer Hallo app insights-resource in Hallo 'Resource' vervolgkeuzelijst en selecteer vervolgens Hallo aangepaste metrische gegevens op basis waarop tooscale.
  ![Schalen door aangepaste metrische gegevens][6]
- Vergelijkbare toohello stap hierboven, een scale-regel die schalen en Hallo schaalaanpassingsaantal met 1 verlagen als aangepaste metrische gegevens Hallo lager dan een drempelwaarde is toevoegen.
  ![Schalen op basis van cpu][7]
- Hallo u limieten-instantie ingesteld. Bijvoorbeeld, als u tooscale tussen 2-5-exemplaren, afhankelijk van de aangepaste metrische schommelingen hello wilt, stelt 'minimale' te '2', 'maximum' te '5' en 'default' te 2
> Opmerking: als er een probleem bij het lezen van de metrische gegevens voor resources Hallo en huidige capaciteit Hallo lager dan de standaardcapaciteit hello is, vervolgens tooensure Hallo beschikbaarheid van Hallo resource, automatisch schalen wordt uitschalen toohello standaardwaarde. Als de huidige capaciteit Hallo al hoger dan de standaardcapaciteit is, worden niet automatisch schalen geschaald.
- Klik op 'Opslaan'

Gefeliciteerd. U hebt nu nu met succes is gemaakt voor uw scale tooauto schaal uw web-app op basis van een aangepaste waarde instellen.

> Opmerking: hello dezelfde stappen zijn van toepassing tooget gestart met een VMSS of cloud service-rol.

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png

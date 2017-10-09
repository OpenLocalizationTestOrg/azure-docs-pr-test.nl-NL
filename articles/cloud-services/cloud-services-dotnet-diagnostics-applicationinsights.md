---
title: aaaTroubleshoot Cloud Services met Application Insights | Microsoft Docs
description: Meer informatie over hoe tootroubleshoot cloudservice problemen met behulp van Application Insights tooprocess gegevens van Azure Diagnostics.
services: cloud-services
documentationcenter: .net
author: sbtron
manager: timlt
editor: tysonn
ms.assetid: e93f387b-ef29-4731-ae41-0676722accb6
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: saurabh
ms.openlocfilehash: 972924d9e6d1fe33d5c19b006d482de52ffb0ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-services-using-application-insights"></a>Problemen met Cloud Services met Application Insights
Met [Azure SDK 2.8](https://azure.microsoft.com/downloads/) en Azure diagnostics extensie 1.5, kunt u Azure Diagnostics-gegevens verzenden voor uw Cloudservice rechtstreeks tooApplication Insights. Hallo logboeken die worden verzameld door Azure Diagnostics&mdash;inclusief toepassingslogboeken, Windows-gebeurtenislogboeken ETW-logboeken en prestatiemeteritems&mdash;tooApplication Insights kunnen worden verzonden. U kunt vervolgens visualiseren van deze informatie in de gebruikersinterface voor Hallo Application Insights-portal. Vervolgens kunt u Hallo Application Insights-SDK tooget inzicht in de metrische gegevens en de logboeken die afkomstig zijn van uw toepassing, evenals de Hallo systeem en het niveau van de infrastructuur-gegevens die afkomstig zijn van Azure Diagnostics.

## <a name="configure-azure-diagnostics-toosend-data-tooapplication-insights"></a>Azure Diagnostics toosend gegevens tooApplication Insights configureren
Volg deze stappen tooset van uw cloud service-project toosend Azure Diagnostics gegevens tooApplication Insights.

1. In Visual Studio Solution Explorer met de rechtermuisknop op een rol en selecteer **eigenschappen** tooopen Hallo rol designer.

    ![Solution Explorer Role-eigenschappen][1]

2. In Hallo **Diagnostics** sectie Hallo rol Designer, selecteer Hallo **verzenden van diagnostische gegevens tooApplication Insights** optie.

    ![Rol designer diagnostische gegevens verzenden gegevens tooapplication insights][2]

3. Selecteer Hallo Application Insights-resource die u wilt dat toosend hello Azure diagnostics-gegevens naar Hallo in het dialoogvenster dat wordt weergegeven. Hallo-dialoogvenster kunt u een bestaande Application Insights-resource uit uw abonnement tooselect of toomanually Geef een instrumentatiesleutel voor Application Insights-resource. Zie voor meer informatie over het maken van een Application Insights-resource [Maak een nieuwe Application Insights-resource](../application-insights/app-insights-create-new-resource.md).

    ![Selecteer application insights-resource][3]

    Nadat u Hallo Application Insights-resource hebt toegevoegd, Hallo instrumentatiesleutel voor die bron wordt opgeslagen als een service-configuratie-instelling met de naam van de Hallo **APPINSIGHTS_INSTRUMENTATIONKEY**. U kunt deze configuratie-instelling voor elke configuratie van de service of de omgeving kunt wijzigen. Selecteer een andere configuratie van Hallo toodo **serviceconfiguratie** lijst en geeft u een nieuwe instrumentatiesleutel voor dat de configuratie.

    ![Selecteer de configuratie van de service][4]

    Hallo **APPINSIGHTS_INSTRUMENTATIONKEY** configuratie-instelling wordt gebruikt door de extensie voor Visual Studio tooconfigure Hallo diagnostische gegevens met Hallo geschikte Application Insights broninformatie tijdens de publicatie. Hallo-configuratie-instelling is een handige manier om verschillende instrumentatiesleutels voor verschillende configuraties te definiëren. Visual Studio wordt die instelling vertalen en plaats deze in Hallo diagnostics extensie openbare configuratie tijdens het Hallo publicatieproces. toosimplify hello proces van het Hallo-extensie voor diagnostische gegevens configureren met PowerShell, Hallo pakket uitvoer vanuit Visual Studio ook Hallo openbare configuratie-XML met Hallo geschikte Application Insights-instrumentatiesleutel bevat. Hallo openbare config-bestanden worden gemaakt in de map extensies Hallo en Hallo patroon volgen *PaaSDiagnostics.&lt; RoleName&gt;. PubConfig.xml*. Alle implementaties op basis van PowerShell kunnen gebruiken dit patroon toomap elke configuratie tooa-rol.

4) tooconfigure Azure diagnostics toosend alle prestatiemeteritems en foutniveau logboeken verzameld door hello Azure diagnostics agent tooApplication Insights inschakelen Hallo **verzenden van diagnostische gegevens tooApplication Insights** optie. 

    Als u toofurther wilt configureren welke gegevens tooApplication Insights wordt verzonden, moet u handmatig Hallo bewerken *diagnostics.wadcfgx* -bestand voor elke rol. Zie [configureren Azure Diagnostics toosend gegevens tooApplication Insights](#configure-azure-diagnostics-to-send-data-to-application-insights) toolearn meer over het handmatig bijwerken Hallo-configuratie.

Wanneer cloudservice Hallo geconfigureerde toosend Azure diagnostics gegevens tooapplication insights is, kunt u implementeren tooAzure normaal gesproken om ervoor te zorgen hello Azure diagnostics-extensie is ingeschakeld. Zie voor meer informatie [publiceren van een Cloudservice met Visual Studio](../vs-azure-tools-publishing-a-cloud-service.md).  

## <a name="viewing-azure-diagnostics-data-in-application-insights"></a>Azure diagnostics-gegevens weergeven in Application Insights
Hello Azure diagnostische telemetrie weergegeven in Application Insights-bron is geconfigureerd voor uw cloudservice Hallo.

Azure diagnostics logboek typen toegewezen tooApplication Insights concepten op de volgende manieren:

* Prestatie-items worden weergegeven als aangepaste metrische gegevens in Application Insights.
* Windows-gebeurtenislogboeken weergegeven als traceringen en aangepaste gebeurtenissen in Application Insights.
* Toepassing Logboeken, ETW-logboeken en de logboekbestanden van de infrastructuur van diagnostische gegevens worden weergegeven als de traceringen in Application Insights.

tooview Azure diagnostics-gegevens in Application Insights, voer een van de volgende Hallo:

* Gebruik [Metrics explorer](../application-insights/app-insights-metrics-explorer.md) toovisualize eventuele aangepaste prestatiemeteritems uit of telt van verschillende soorten gebeurtenissen van de Windows-gebeurtenislogboek.

    ![Aangepaste metrische gegevens in Metrics Explorer][5]

* Gebruik [Search](../application-insights/app-insights-diagnostic-search.md) toosearch over Hallo traceerlogboeken verzonden door Azure Diagnostics. Bijvoorbeeld, als een onverwerkte uitzondering heeft veroorzaakt Hallo rol toocrash en recyclen, informatie over Hallo uitzondering wordt weergegeven in Hallo *toepassing* kanaal van *Windows-gebeurtenislogboek*. U kunt zoeken toolook gebruiken op Windows-gebeurtenislogboek fout Hallo en Hallo volledige stack-tracering voor Hallo uitzondering toohelp zoeken Hallo oorzaak van het probleem Hallo ophalen.

    ![Traceringen zoeken][6]

## <a name="next-steps"></a>Volgende stappen
* [Hallo Application Insights-SDK tooyour cloudservice toevoegen](../application-insights/app-insights-cloudservices.md) toosend gegevens over aanvragen, uitzonderingen, afhankelijkheden en eventuele aangepaste telemetrie van uw toepassing. In combinatie met hello Azure Diagnostics-gegevens, deze informatie krijgt u een compleet beeld van uw toepassing en het systeem, Hallo allemaal in dezelfde toepassing inzicht resource.  

<!--Image references-->
[1]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/solution-explorer-properties.png
[2]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-sendtoappinsights.png
[3]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/select-appinsights-resource.png
[4]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/role-designer-appinsights-serviceconfig.png
[5]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/metrics-explorer-custom-metrics.png
[6]: ./media/cloud-services-dotnet-diagnostics-applicationinsights/search-windowseventlog-error.png

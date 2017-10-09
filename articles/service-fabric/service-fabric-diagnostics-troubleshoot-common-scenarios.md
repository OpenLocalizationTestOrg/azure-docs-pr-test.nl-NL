---
title: aaaTroubleshooting met gebeurtenistracering | Microsoft Docs
description: Hallo meest voorkomende problemen aangetroffen tijdens het implementeren van services op Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: mattrowmsft
manager: timlt
editor: 
ms.assetid: 5eb8ef21-da04-4ac8-8b9a-5f7ff1e0a180
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/31/2016
ms.author: mattrow
redirect_url: /azure/service-fabric/service-fabric-diagnostics-overview
ms.openlocfilehash: f5adb7e15fa1e2c964bbbc5726246630c95e13f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-issues-when-you-deploy-services-on-azure-service-fabric"></a>Algemene problemen bij het implementeren van services op Azure Service Fabric
Wanneer u services op uw computer developer uitvoert, is het eenvoudig toouse [de hulpprogramma's voor foutopsporing van Visual Studio](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). Voor externe clusters [statusrapporten](service-fabric-view-entities-aggregated-health.md) zijn altijd een goede plaats toostart. Hallo eenvoudigste manieren tooaccess deze rapporten via PowerShell zijn of [SFX](service-fabric-visualizing-your-cluster.md). In dit artikel wordt ervan uitgegaan dat u een extern Clusterbeheer zijn foutopsporing en basiskennis van hoe u een van deze hulpprogramma's voor toouse.

## <a name="application-crash"></a>De toepassing is vastgelopen
Hallo ' partitie is lager dan aantal replica of het exemplaar als doel ' rapport is een goede indicatie die uw service is gecrasht. toofind uit waar de service is gecrasht duurt nog iets meer onderzoek. Als uw service wordt uitgevoerd op grote schaal, is de beste vriend een reeks goed doordacht traceringen.  We raden aan dat u probeert [Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) voor het verzamelen van deze traceringen en gebruik van een oplossing zoals [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) voor het weergeven en zoeken Hallo traceringen.

![SFX partitie Health](./media/service-fabric-diagnostics-troubleshoot-common-scenarios/crashNewApp.png)

### <a name="during-service-or-actor-initialization"></a>Tijdens de initialisatie van de service of actor
Eventuele uitzonderingen voordat Hallo servicetype is geïnitialiseerd, wordt Hallo proces toocrash. Voor deze typen crashes weergegeven logboek voor toepassingsgebeurtenissen Hallo Hallo-fout opgetreden in de service.
Dit zijn de meest voorkomende uitzonderingen toosee Hallo voordat het Hallo-service is geïnitialiseerd.

***System.IO.FileNotFoundException***

Deze fout wordt vaak vanwege toomissing assembly-afhankelijkheden. Controleer Hallo CopyLocal eigenschap in Visual Studio of Hallo globale assembly-cache voor het Hallo-knooppunt.

***System.Runtime.InteropServices.COMException*** *op System.Fabric.Interop.NativeRuntime+IFabricRuntime.RegisterStatefulServiceFactory (IntPtr, IFabricStatefulServiceFactory)*

 Hiermee wordt aangegeven met die naam Hallo geregistreerde service type komt niet overeen met de Hallo servicemanifest.

[Azure Diagnostics](service-fabric-diagnostics-how-to-setup-wad.md) geconfigureerde tooupload Hallo logboek voor toepassingsgebeurtenissen voor alle knooppunten in uw automatisch kan worden.

### <a name="runasync-or-onactivateasync"></a>RunAsync() of OnActivateAsync()
Als Hallo crash tijdens de initialisatie van de Hallo gebeurt of van uw geregistreerde servicetype of actor wordt uitgevoerd, Hallo uitzondering wordt onderschept door Azure Service Fabric. U kunt deze van Hallo EventSource providers uiteengezet in de sectie 'Volgende stappen' hello weergeven.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over bestaande diagnostische gegevens die worden geleverd door de Service Fabric:

* [Betrouwbare actoren diagnostische gegevens](service-fabric-reliable-actors-diagnostics.md)
* [Betrouwbare diagnostische gegevens voor Services](service-fabric-reliable-services-diagnostics.md)


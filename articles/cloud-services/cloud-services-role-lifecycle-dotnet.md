---
title: gebeurtenissen van de aaaHandle Cloud Service lifecycle | Microsoft Docs
description: Meer informatie over hoe Hallo lifecycle methoden van een Cloudservice-rol kunnen worden gebruikt in .NET
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 39b30acd-57b9-48b7-a7c4-40ea3430e451
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: cc0ccc5f055b965202b6e081a6ab72ad5d39b034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-hello-lifecycle-of-a-web-or-worker-role-in-net"></a>Hallo levenscyclus van een Web- of Worker-rol in .NET aanpassen
Wanneer u een werkrol maakt, u Hallo uitbreiden [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) klasse biedt methoden voor u toooverride waarmee u kunt reageren toolifecycle gebeurtenissen. Deze klasse is voor webrollen optioneel, zodat u toorespond toolifecycle gebeurtenissen moet gebruiken.

## <a name="extend-hello-roleentrypoint-class"></a>Hallo RoleEntryPoint klasse uitbreiden
Hallo [RoleEntryPoint](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx) klasse bevat methoden die door Azure worden aangeroepen wanneer het **begint**, **wordt uitgevoerd**, of **stopt** een web- of worker-rol. U kunt eventueel deze methoden toomanage rol initialisatie, rol afsluiten reeksen of Hallo uitvoeringsthread van Hallo rol overschrijven. 

Wanneer u uitbreidt **RoleEntryPoint**, u moet rekening houden met de Hallo gedrag van Hallo methoden volgen:

* Hallo [OnStart](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) en [OnStop](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) methoden retourneren een Booleaanse waarde, dus is het mogelijk tooreturn **false** van deze methoden.
  
   Als uw code retourneert **false**, Hallo rol proces is onverwacht beëindigd, zonder dat elke afsluitvolgorde uitgevoerd mogelijk hebt u in plaats. In het algemeen moet u vermijden retourneren **false** van Hallo **OnStart** methode.
* Een onbekende uitzondering opgetreden binnen een overload van een **RoleEntryPoint** methode wordt behandeld als een onverwerkte uitzondering.
  
   Als er een uitzondering optreedt binnen één Hallo lifecycle methoden, Azure Hallo verhoogt [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) gebeurtenis, en vervolgens Hallo-proces is beëindigd. Nadat uw rol heeft offline is gezet, wordt deze opnieuw starten door Azure. Wanneer een niet-verwerkte uitzondering optreedt, hello [stoppen](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.stopping.aspx) gebeurtenis wordt niet gegenereerd en Hallo **OnStop** methode is niet aangeroepen.

Als uw rol niet gestart wordt of is recycling tussen Hallo initialiseren, statussen bezet en stoppen, kan uw code worden er wordt een onverwerkte uitzondering binnen één Hallo lifecycle gebeurtenissen die elke keer Hallo rol opnieuw wordt opgestart. In dit geval gebruiken Hallo [UnhandledException](https://msdn.microsoft.com/library/system.appdomain.unhandledexception.aspx) gebeurtenis toodetermine oorzaak van de uitzondering Hallo Hallo en op juiste manier verwerken. Uw rol kan ook worden teruggekeerd uit Hallo [uitvoeren](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode waardoor Hallo rol toorestart. Zie voor meer informatie over implementatiestatussen [veelvoorkomende problemen die oorzaak rollen tooRecycle](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

> [!NOTE]
> Als u van Hallo gebruikmaakt **Azure-hulpprogramma's voor Microsoft Visual Studio** toodevelop uw toepassing hello rol projectsjablonen automatisch uitbreiden Hallo **RoleEntryPoint** klasse voor u, in Hallo *WebRole.cs* en *WorkerRole.cs* bestanden.
> 
> 

## <a name="onstart-method"></a>OnStart-methode
Hallo **OnStart** methode wordt aangeroepen wanneer uw rolexemplaar online is gebracht door Azure. Tijdens het Hallo OnStart code wordt uitgevoerd, Hallo rolinstantie is gemarkeerd als **bezet** en er is geen externe verkeer worden gerichte tooit door Hallo load balancer. U kunt dit werk methode tooperform initialisatie, zoals het implementeren van gebeurtenis-handlers en worden gestart overschrijven [Azure Diagnostics](cloud-services-how-to-monitor.md).

Als **OnStart** retourneert **true**, Hallo-exemplaar is geïnitialiseerd en Azure roept Hallo **RoleEntryPoint.Run** methode. Als **OnStart** retourneert **false**, Hallo rol beëindigt onmiddellijk, zonder eventuele reeksen geplande afsluiting wordt uitgevoerd.

Hallo van de volgende code voorbeeld ziet u hoe toooverride hello **OnStart** methode. Deze methode wordt geconfigureerd en een diagnostische monitor wordt gestart wanneer Hallo rolinstantie wordt gestart en stelt u een overdracht gegevens tooa storage-account aan te melden:

```csharp
public override bool OnStart()
{
    var config = DiagnosticMonitor.GetDefaultInitialConfiguration();

    config.DiagnosticInfrastructureLogs.ScheduledTransferLogLevelFilter = LogLevel.Error;
    config.DiagnosticInfrastructureLogs.ScheduledTransferPeriod = TimeSpan.FromMinutes(5);

    DiagnosticMonitor.Start("DiagnosticsConnectionString", config);

    return true;
}
```

## <a name="onstop-method"></a>OnStop methode
Hallo **OnStop** methode wordt aangeroepen nadat een rolinstantie offline is genomen door Azure en voordat het Hallo-proces wordt afgesloten. U kunt deze methode toocall code vereist is voor uw rol exemplaar toocleanly afgesloten overschrijven.

> [!IMPORTANT]
> Code die wordt uitgevoerd in Hallo **OnStop** methode heeft een beperkte periode toofinish wanneer deze wordt aangeroepen voor andere doeleinden dan een afsluiten van de gebruiker is gestart. Nadat deze tijd is verstreken, Hallo-proces wordt beëindigd, dus moet u ervoor zorgen dat de code in Hallo **OnStop** methode snel kunt uitvoeren of maximaal wordt niet uitgevoerd toocompletion toegestaan. Hallo **OnStop** methode wordt aangeroepen nadat Hallo **stoppen** gebeurtenis is opgetreden.
> 
> 

## <a name="run-method"></a>Methode niet uitvoeren
U kunt onderdrukken Hallo **uitvoeren** methode tooimplement een langlopende-thread voor uw rolexemplaar.

Hallo overschrijven **uitvoeren** methode is niet vereist; Hallo standaardimplementatie een thread die permanent sluimert begint. Als u Hallo onderdrukken **uitvoeren** methode, uw code dient te blokkeren voor onbepaalde tijd. Als hello **uitvoeren** methode retourneert, Hallo-rol wordt automatisch probleemloos gerecycled; met andere woorden, Azure genereert Hallo **stoppen** gebeurtenis en aanroepen Hallo **OnStop** methode zodat dat uw reeksen afsluiten kunnen worden uitgevoerd voordat de rol Hallo offline wordt gezet.

### <a name="implementing-hello-aspnet-lifecycle-methods-for-a-web-role"></a>Hallo ASP.NET lifecycle methoden voor een Webrol implementeren
U kunt Hallo ASP.NET lifecycle methoden gebruiken bovendien toothose geleverd door Hallo **RoleEntryPoint** klasse, toomanage initialisatie en afsluiten die gebruikmaken van een Webrol. Dit kan zijn handig voor compatibiliteit als u bij het overbrengen van een bestaande tooAzure voor ASP.NET-toepassing. Hallo ASP.NET lifecycle methoden worden aangeroepen vanuit Hallo **RoleEntryPoint** methoden. Hallo **toepassing\_Start** methode wordt aangeroepen nadat Hallo **RoleEntryPoint.OnStart** methode is voltooid. Hallo **toepassing\_End** methode wordt aangeroepen voordat Hallo **RoleEntryPoint.OnStop** methode wordt aangeroepen.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe te[maken van een cloud service-pakket](cloud-services-model-and-package.md).


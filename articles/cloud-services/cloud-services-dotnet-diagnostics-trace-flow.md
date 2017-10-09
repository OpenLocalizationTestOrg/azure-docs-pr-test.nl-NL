---
title: aaaTrace hello stroom in een Cloud Services-toepassing met Azure Diagnostics | Microsoft Docs
description: Tracering berichten tooan Azure-toepassing toohelp foutopsporing, meten van de prestaties, bewaking, analyse van het netwerkverkeer en meer toevoegen.
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: d2ed7b5997ae1d298115b4ce593bb5051a9a0c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="trace-hello-flow-of-a-cloud-services-application-with-azure-diagnostics"></a>Hallo-stroom van een Cloud Services-toepassing met Azure Diagnostics traceren
Tracering is een manier voor u toomonitor Hallo uitvoering van uw toepassing, terwijl deze wordt uitgevoerd. U kunt Hallo [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), en [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) toorecord informatie over fouten klassen en de uitvoering van de toepassing in Logboeken, tekstbestanden of andere apparaten voor latere analyse. Zie voor meer informatie over tracering [tracering en toepassingen Instrumenteren](https://msdn.microsoft.com/library/zs6s4h68.aspx).

## <a name="use-trace-statements-and-trace-switches"></a>Trace-instructies en tracering switches gebruiken
De tracering implementeren in uw Cloud Services-toepassing door toe te voegen Hallo [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) toohello Toepassingsconfiguratie en aanbrengen aanroepen tooSystem.Diagnostics.Trace of System.Diagnostics.Debug in uw toepassingscode. Gebruik Hallo-configuratiebestand *app.config* voor werkrollen en Hallo *web.config* voor web-rollen. Wanneer u een nieuwe gehoste service met behulp van Visual Studio-sjabloon maakt, Azure Diagnostics wordt automatisch toohello project toegevoegd en Hallo DiagnosticMonitorTraceListener toegevoegd toohello juiste configuratiebestand voor Hallo-functies die u toevoegt.

Zie voor informatie over het plaatsen van trace-instructies, [hoe: Trace-instructies toevoegen tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).

Door het plaatsen van [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in uw code kunt u bepalen of de tracering plaatsvindt en hoe uitgebreide is. Hiermee kunt u Hallo status bewaken van uw toepassing in een productieomgeving. Dit is vooral belangrijk in een zakelijke toepassing die gebruikmaakt van meerdere onderdelen op meerdere computers. Zie voor meer informatie [hoe: Trace-Switches configureren](https://msdn.microsoft.com/library/t06xyy08.aspx).

## <a name="configure-hello-trace-listener-in-an-azure-application"></a>Hallo traceringslistener configureren in een Azure-toepassing
Trace, foutopsporing en TraceSource, moet u instellen 'listeners' toocollect en record Hallo-berichten die worden verzonden. Listeners verzamelen, opslaan en routeren van berichten voor tracering. Ze rechtstreeks Hallo tracering uitvoer tooan juiste doel, zoals een logboek, venster of tekstbestand. Hallo maakt gebruik van Azure Diagnostics [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) klasse.

Voordat u Hallo na procedure voltooien, moet u hello Azure diagnostische monitor initialiseren. toodo deze, Zie [diagnostische gegevens inschakelen in Microsoft Azure](cloud-services-dotnet-diagnostics.md).

Houd er rekening mee dat als u Hallo-sjablonen die worden geleverd door Visual Studio, Hallo configuratie van Hallo-listener is toegevoegd automatisch voor u.

### <a name="add-a-trace-listener"></a>Een traceringslistener toevoegen
1. Open Hallo web.config of app.config-bestand voor uw rol.
2. Hallo na toohello codebestand toevoegen. Hallo kenmerk toouse Hallo versienummer van Hallo assembly waarnaar u verwijst wijzigen. Hallo-assembly-versie wijzigen niet per se met elke versie van de Azure SDK tenzij er updates tooit.
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > Zorg ervoor dat u hebt een project verwijzing toohello Microsoft.WindowsAzure.Diagnostics assembly. Update Hallo-versienummer in XML-Hallo hierboven toomatch Hallo versie Hallo verwezen Microsoft.WindowsAzure.Diagnostics assembly.
   > 
   > 
3. Hallo-configuratiebestand opslaan.

Zie voor meer informatie over listeners [traceer-Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).

Nadat u Hallo stappen tooadd Hallo listener hebt voltooid, kunt u de trace-instructies tooyour code kunt toevoegen.

### <a name="tooadd-trace-statement-tooyour-code"></a>tooadd trace-instructie tooyour code
1. Open een bronbestand voor uw toepassing. Bijvoorbeeld, Hallo <RoleName>.cs-bestand voor de werkrol Hallo of Webrol.
2. Voeg de volgende Hallo gebruiksinstructie als al niet is toegevoegd:
    ```
        using System.Diagnostics;
    ```
3. Trace-instructies waar u toocapture informatie over de status van uw toepassing hello wilt toevoegen. U kunt verschillende methoden tooformat Hallo uitvoer Hallo Trace-instructie. Zie voor meer informatie [hoe: Trace-instructies toevoegen tooApplication Code](https://msdn.microsoft.com/library/zd83saa2.aspx).
4. Hallo-bronbestand opslaan.


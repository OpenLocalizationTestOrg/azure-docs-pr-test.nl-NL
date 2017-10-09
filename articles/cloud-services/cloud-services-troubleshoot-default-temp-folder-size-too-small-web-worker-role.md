---
title: de grootte van de map TEMP aaaDefault is te klein voor een rol | Microsoft Docs
description: De functie van een cloud-service heeft een beperkte hoeveelheid ruimte voor de map TEMP Hallo. In dit artikel vindt u enkele suggesties voor het tooavoid bijna geen schijfruimte meer.
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 9f2af8dd-2012-4b36-9dd5-19bf6a67e47d
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 307dc20f3264e29d122a6616be0028d2ec1282c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a>Standaard is tijdelijke map te klein voor een cloud service web/worker-rol
Hallo standaard tijdelijke map van een cloud service worker- of webserver-rol heeft een maximale grootte van 100 MB, die mogelijk volledige op een bepaald moment. Dit artikel wordt beschreven hoe tooavoid bijna geen schijfruimte voor de tijdelijke map Hallo meer.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a>Waarom kan ik geen ruimte meer uitvoeren?
Hallo standaard Windows-omgevingsvariabelen TEMP en TMP zijn beschikbaar toocode die in uw toepassing wordt uitgevoerd. Zowel TEMP en TMP punt tooa één map met een maximale grootte van 100 MB. Alle gegevens die zijn opgeslagen in deze map is niet persistent over Hallo levenscyclus van de cloudservice Hallo; Als het Hallo-rolexemplaren in een cloudservice zijn gerecycled worden Hallo directory opgeruimd.

## <a name="suggestion-toofix-hello-problem"></a>Suggestie toofix Hallo probleem
Implementeer een Hallo alternatieven te volgen:

* Configureren van een resource voor lokale opslag en toegang tot deze rechtstreeks in plaats van TEMP of TMP. een bron van de lokale opslag van code die wordt uitgevoerd in uw toepassing, aanroep Hallo tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) methode.
* De bron van een lokale opslag configureert en wijs Hallo TEMP en TMP mappen toopoint toohello pad van Hallo lokale opslagresource. Deze wijziging moet worden uitgevoerd binnen Hallo [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) methode.

Hallo volgende voorbeeldcode laat zien hoe toomodify doel mappen hello voor TEMP en TMP uit binnen Hallo OnStart-methode:

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // hello local resource declaration must have been added toothe
            // service definition file for hello role named WorkerRole1:
            //
            // <LocalResources>
            //    <LocalStorage name="CustomTempLocalStore"
            //                  cleanOnRoleRecycle="false"
            //                  sizeInMB="1024" />
            // </LocalResources>

            string customTempLocalResourcePath =
            RoleEnvironment.GetLocalResource("CustomTempLocalStore").RootPath;
            Environment.SetEnvironmentVariable("TMP", customTempLocalResourcePath);
            Environment.SetEnvironmentVariable("TEMP", customTempLocalResourcePath);

            // hello rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a>Volgende stappen
Lees een blog die beschrijft [hoe tooincrease grootte van hello Azure Web rol ASP.NET tijdelijke map Hallo](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).

Meer [probleemoplossing artikelen](/?tag=top-support-issue&product=cloud-services) voor cloudservices.

toolearn hoe tootroubleshoot cloud service rol problemen met behulp van Azure PaaS computer diagnostische gegevens bekijken [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

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
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="62df5-104">Standaard is tijdelijke map te klein voor een cloud service web/worker-rol</span><span class="sxs-lookup"><span data-stu-id="62df5-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="62df5-105">Hallo standaard tijdelijke map van een cloud service worker- of webserver-rol heeft een maximale grootte van 100 MB, die mogelijk volledige op een bepaald moment.</span><span class="sxs-lookup"><span data-stu-id="62df5-105">hello default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="62df5-106">Dit artikel wordt beschreven hoe tooavoid bijna geen schijfruimte voor de tijdelijke map Hallo meer.</span><span class="sxs-lookup"><span data-stu-id="62df5-106">This article describes how tooavoid running out of space for hello temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="62df5-107">Waarom kan ik geen ruimte meer uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="62df5-107">Why do I run out of space?</span></span>
<span data-ttu-id="62df5-108">Hallo standaard Windows-omgevingsvariabelen TEMP en TMP zijn beschikbaar toocode die in uw toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="62df5-108">hello standard Windows environment variables TEMP and TMP are available toocode that is running in your application.</span></span> <span data-ttu-id="62df5-109">Zowel TEMP en TMP punt tooa één map met een maximale grootte van 100 MB.</span><span class="sxs-lookup"><span data-stu-id="62df5-109">Both TEMP and TMP point tooa single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="62df5-110">Alle gegevens die zijn opgeslagen in deze map is niet persistent over Hallo levenscyclus van de cloudservice Hallo; Als het Hallo-rolexemplaren in een cloudservice zijn gerecycled worden Hallo directory opgeruimd.</span><span class="sxs-lookup"><span data-stu-id="62df5-110">Any data that is stored in this directory is not persisted across hello lifecycle of hello cloud service; if hello role instances in a cloud service are recycled, hello directory is cleaned.</span></span>

## <a name="suggestion-toofix-hello-problem"></a><span data-ttu-id="62df5-111">Suggestie toofix Hallo probleem</span><span class="sxs-lookup"><span data-stu-id="62df5-111">Suggestion toofix hello problem</span></span>
<span data-ttu-id="62df5-112">Implementeer een Hallo alternatieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="62df5-112">Implement one of hello following alternatives:</span></span>

* <span data-ttu-id="62df5-113">Configureren van een resource voor lokale opslag en toegang tot deze rechtstreeks in plaats van TEMP of TMP.</span><span class="sxs-lookup"><span data-stu-id="62df5-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="62df5-114">een bron van de lokale opslag van code die wordt uitgevoerd in uw toepassing, aanroep Hallo tooaccess [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="62df5-114">tooaccess a local storage resource from code that is running within your application, call hello [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="62df5-115">De bron van een lokale opslag configureert en wijs Hallo TEMP en TMP mappen toopoint toohello pad van Hallo lokale opslagresource.</span><span class="sxs-lookup"><span data-stu-id="62df5-115">Configure a local storage resource, and point hello TEMP and TMP directories toopoint toohello path of hello local storage resource.</span></span> <span data-ttu-id="62df5-116">Deze wijziging moet worden uitgevoerd binnen Hallo [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="62df5-116">This modification should be performed within hello [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="62df5-117">Hallo volgende voorbeeldcode laat zien hoe toomodify doel mappen hello voor TEMP en TMP uit binnen Hallo OnStart-methode:</span><span class="sxs-lookup"><span data-stu-id="62df5-117">hello following code example shows how toomodify hello target directories for TEMP and TMP from within hello OnStart method:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="62df5-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="62df5-118">Next steps</span></span>
<span data-ttu-id="62df5-119">Lees een blog die beschrijft [hoe tooincrease grootte van hello Azure Web rol ASP.NET tijdelijke map Hallo](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="62df5-119">Read a blog that describes [How tooincrease hello size of hello Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="62df5-120">Meer [probleemoplossing artikelen](/?tag=top-support-issue&product=cloud-services) voor cloudservices.</span><span class="sxs-lookup"><span data-stu-id="62df5-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="62df5-121">toolearn hoe tootroubleshoot cloud service rol problemen met behulp van Azure PaaS computer diagnostische gegevens bekijken [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="62df5-121">toolearn how tootroubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

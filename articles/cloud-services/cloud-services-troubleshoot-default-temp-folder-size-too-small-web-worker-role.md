---
title: Standaard tijdelijke map is te klein voor een functie | Microsoft Docs
description: De functie van een cloud-service heeft een beperkte hoeveelheid ruimte voor de map TEMP. Dit artikel vindt enkele suggesties voor het vermijden van buiten de ruimte die wordt uitgevoerd.
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
ms.openlocfilehash: 577d090a009eb2331b401273257c7cc7c1eea772
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="default-temp-folder-size-is-too-small-on-a-cloud-service-webworker-role"></a><span data-ttu-id="79ebb-104">Standaard is tijdelijke map te klein voor een cloud service web/worker-rol</span><span class="sxs-lookup"><span data-stu-id="79ebb-104">Default TEMP folder size is too small on a cloud service web/worker role</span></span>
<span data-ttu-id="79ebb-105">De standaard tijdelijke map van een cloud service worker- of webserver-rol heeft een maximale grootte van 100 MB, die volledig op een bepaald moment kan worden.</span><span class="sxs-lookup"><span data-stu-id="79ebb-105">The default temporary directory of a cloud service worker or web role has a maximum size of 100 MB, which may become full at some point.</span></span> <span data-ttu-id="79ebb-106">Dit artikel wordt beschreven hoe u voorkomt dat met de beschikbare ruimte voor de tijdelijke map.</span><span class="sxs-lookup"><span data-stu-id="79ebb-106">This article describes how to avoid running out of space for the temporary directory.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-do-i-run-out-of-space"></a><span data-ttu-id="79ebb-107">Waarom kan ik geen ruimte meer uitvoeren?</span><span class="sxs-lookup"><span data-stu-id="79ebb-107">Why do I run out of space?</span></span>
<span data-ttu-id="79ebb-108">De standaard Windows-omgevingsvariabelen TEMP en TMP zijn beschikbaar voor de code die wordt uitgevoerd in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="79ebb-108">The standard Windows environment variables TEMP and TMP are available to code that is running in your application.</span></span> <span data-ttu-id="79ebb-109">Zowel TEMP en TMP verwijzen naar één map met een maximale grootte van 100 MB.</span><span class="sxs-lookup"><span data-stu-id="79ebb-109">Both TEMP and TMP point to a single directory that has a maximum size of 100 MB.</span></span> <span data-ttu-id="79ebb-110">Alle gegevens die zijn opgeslagen in deze map is niet persistent over de levenscyclus van de cloudservice; Als de rolexemplaren in een cloudservice gerecycled worden, wordt de map verwijderd.</span><span class="sxs-lookup"><span data-stu-id="79ebb-110">Any data that is stored in this directory is not persisted across the lifecycle of the cloud service; if the role instances in a cloud service are recycled, the directory is cleaned.</span></span>

## <a name="suggestion-to-fix-the-problem"></a><span data-ttu-id="79ebb-111">Suggestie het probleem op te lossen</span><span class="sxs-lookup"><span data-stu-id="79ebb-111">Suggestion to fix the problem</span></span>
<span data-ttu-id="79ebb-112">Een van de volgende alternatieven implementeren:</span><span class="sxs-lookup"><span data-stu-id="79ebb-112">Implement one of the following alternatives:</span></span>

* <span data-ttu-id="79ebb-113">Configureren van een resource voor lokale opslag en toegang tot deze rechtstreeks in plaats van TEMP of TMP.</span><span class="sxs-lookup"><span data-stu-id="79ebb-113">Configure a local storage resource, and access it directly instead of using TEMP or TMP.</span></span> <span data-ttu-id="79ebb-114">Aanroepen voor toegang tot een bron voor lokale opslag van code die wordt uitgevoerd in uw toepassing, de [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="79ebb-114">To access a local storage resource from code that is running within your application, call the [RoleEnvironment.GetLocalResource](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.getlocalresource.aspx) method.</span></span>
* <span data-ttu-id="79ebb-115">De bron van een lokale opslag configureert en wijst u de mappen TEMP en TMP om te verwijzen naar het pad van de bron van de lokale opslag.</span><span class="sxs-lookup"><span data-stu-id="79ebb-115">Configure a local storage resource, and point the TEMP and TMP directories to point to the path of the local storage resource.</span></span> <span data-ttu-id="79ebb-116">Deze wijziging moet worden uitgevoerd binnen de [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="79ebb-116">This modification should be performed within the [RoleEntryPoint.OnStart](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx) method.</span></span>

<span data-ttu-id="79ebb-117">De volgende voorbeeldcode laat zien hoe de doel-mappen wijzigen voor TEMP en TMP uit binnen de OnStart-methode:</span><span class="sxs-lookup"><span data-stu-id="79ebb-117">The following code example shows how to modify the target directories for TEMP and TMP from within the OnStart method:</span></span>

```csharp
using System;
using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override bool OnStart()
        {
            // The local resource declaration must have been added to the
            // service definition file for the role named WorkerRole1:
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

            // The rest of your startup code goes here…

            return base.OnStart();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="79ebb-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79ebb-118">Next steps</span></span>
<span data-ttu-id="79ebb-119">Lees een blog die beschrijft [het verhogen van de grootte van de Azure-functie ASP.NET tijdelijke webmap](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span><span class="sxs-lookup"><span data-stu-id="79ebb-119">Read a blog that describes [How to increase the size of the Azure Web Role ASP.NET Temporary Folder](http://blogs.msdn.com/b/kwill/archive/2011/07/18/how-to-increase-the-size-of-the-windows-azure-web-role-asp-net-temporary-folder.aspx).</span></span>

<span data-ttu-id="79ebb-120">Meer [probleemoplossing artikelen](/?tag=top-support-issue&product=cloud-services) voor cloudservices.</span><span class="sxs-lookup"><span data-stu-id="79ebb-120">View more [troubleshooting articles](/?tag=top-support-issue&product=cloud-services) for cloud services.</span></span>

<span data-ttu-id="79ebb-121">Voor informatie over het oplossen van problemen met de rol van de cloud service met behulp van de diagnostics-gegevens voor Azure PaaS-computer, geven [blogreeks van Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span><span class="sxs-lookup"><span data-stu-id="79ebb-121">To learn how to troubleshoot cloud service role issues by using Azure PaaS computer diagnostics data, view [Kevin Williamson's blog series](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).</span></span>

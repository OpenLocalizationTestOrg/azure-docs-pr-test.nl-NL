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
# <a name="get-started-with-auto-scale-by-custom-metric-in-azure"></a><span data-ttu-id="0b8ac-103">Aan de slag met automatisch schalen door aangepaste metrische gegevens in Azure</span><span class="sxs-lookup"><span data-stu-id="0b8ac-103">Get started with auto scale by custom metric in Azure</span></span>
<span data-ttu-id="0b8ac-104">Dit artikel wordt beschreven hoe tooscale uw resource door een aangepaste waarde in Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-104">This article describes how tooscale your resource by a custom metric in Azure portal.</span></span>

<span data-ttu-id="0b8ac-105">Azure Monitor automatisch schalen geldt alleen tooVirtual Machine Scale Sets (VMSS), cloudservices, app-serviceabonnementen en app service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-105">Azure Monitor auto scale applies only tooVirtual Machine Scale Sets (VMSS), cloud services, app service plans and app service environments.</span></span> 

# <a name="lets-get-started"></a><span data-ttu-id="0b8ac-106">Hiermee kunnen aan de slag</span><span class="sxs-lookup"><span data-stu-id="0b8ac-106">Lets get started</span></span>
<span data-ttu-id="0b8ac-107">In dit artikel wordt ervan uitgegaan dat u een web-app met application insights is geconfigureerd hebt.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-107">This article assumes that you have a web app with application insights configured.</span></span> <span data-ttu-id="0b8ac-108">Als u nog geen een hebt, kunt u [Application Insights instellen voor uw ASP.NET-website][1]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-108">If you don't have one already, you can [set up Application Insights for your ASP.NET website][1]</span></span>

- <span data-ttu-id="0b8ac-109">Open [Azure-portal][2]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-109">Open [Azure portal][2]</span></span>
- <span data-ttu-id="0b8ac-110">Klik op het pictogram in het linkernavigatievenster hello Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-110">Click on Azure Monitor icon in hello left navigation pane.</span></span>
  <span data-ttu-id="0b8ac-111">![Azure Monitor starten][3]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-111">![Launch Azure Monitor][3]</span></span>
- <span data-ttu-id="0b8ac-112">Klik op alle Hallo resources voor welke automatisch schalen van toepassing, samen met de huidige status voor automatisch schalen is van tooview instelling voor automatisch schalen ![automatisch schalen in Azure monitor detecteren][4]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-112">Click on Autoscale setting tooview all hello resources for which auto scale is applicable, along with its current autoscale status ![Discover auto scale in Azure monitor][4]</span></span>
- <span data-ttu-id="0b8ac-113">'Automatisch ' schalen-blade geopend in de Azure-Monitor en selecteer een bron die u wilt dat tooscale</span><span class="sxs-lookup"><span data-stu-id="0b8ac-113">Open 'Autoscale' blade in Azure Monitor and select a resource you want tooscale</span></span>
> <span data-ttu-id="0b8ac-114">Opmerking: de onderstaande stappen voor hello gebruiken een app service-plan dat is gekoppeld aan een WebApp die app insights geconfigureerd is.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-114">Note: hello steps below use an app service plan associated with a web app that has app insights configured.</span></span>
- <span data-ttu-id="0b8ac-115">Hallo scale instelling blade voor Hallo resource ziet dat het huidige aantal exemplaren Hallo 1.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-115">In hello scale setting blade for hello resource, notice that hello current instance count is 1.</span></span> <span data-ttu-id="0b8ac-116">Klik op 'Inschakelen voor automatisch schalen'.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-116">Click on 'Enable autoscale'.</span></span>
  <span data-ttu-id="0b8ac-117">![Instelling voor de nieuwe web-app schalen][5]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-117">![Scale setting for new web app][5]</span></span>
- <span data-ttu-id="0b8ac-118">Geef een naam voor Hallo schaal instellen en hello, klik op 'Een regel toevoegen'.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-118">Provide a name for hello scale setting, and hello click on "Add a rule".</span></span> <span data-ttu-id="0b8ac-119">U ziet Hallo regel schalingsopties dat wordt geopend in een context deelvenster in de rechterzijde Hallo.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-119">Notice hello scale rule options that opens as a context pane in hello right hand side.</span></span> <span data-ttu-id="0b8ac-120">Standaard wordt uw exemplaar 1 tellen als Hallo CPU percetage van Hallo resource groter is dan 70% van Hallo optie tooscale ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-120">By default, it sets hello option tooscale your instance count by 1 if hello CPU percetage of hello resource exceeds 70%.</span></span> <span data-ttu-id="0b8ac-121">Metrische bron wijzigen Hallo Hallo boven te 'Application Insights', selecteer Hallo app insights-resource in Hallo 'Resource' vervolgkeuzelijst en selecteer vervolgens Hallo aangepaste metrische gegevens op basis waarop tooscale.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-121">Change hello metric source at hello top too"Application Insights", select hello app insights resource in hello 'Resource' dropdown and then select hello custom metric based on which you want tooscale.</span></span>
  <span data-ttu-id="0b8ac-122">![Schalen door aangepaste metrische gegevens][6]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-122">![Scale by custom metric][6]</span></span>
- <span data-ttu-id="0b8ac-123">Vergelijkbare toohello stap hierboven, een scale-regel die schalen en Hallo schaalaanpassingsaantal met 1 verlagen als aangepaste metrische gegevens Hallo lager dan een drempelwaarde is toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-123">Similar toohello step above, add a scale rule that will scale in and decrease hello scale count by 1 if hello custom metric is below a threshold.</span></span>
  <span data-ttu-id="0b8ac-124">![Schalen op basis van cpu][7]</span><span class="sxs-lookup"><span data-stu-id="0b8ac-124">![Scale based on cpu][7]</span></span>
- <span data-ttu-id="0b8ac-125">Hallo u limieten-instantie ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-125">Set hello you instance limits.</span></span> <span data-ttu-id="0b8ac-126">Bijvoorbeeld, als u tooscale tussen 2-5-exemplaren, afhankelijk van de aangepaste metrische schommelingen hello wilt, stelt 'minimale' te '2', 'maximum' te '5' en 'default' te 2</span><span class="sxs-lookup"><span data-stu-id="0b8ac-126">For example, if you want tooscale between 2-5 instances depending on hello custom metric fluctuations, set 'minimum' too'2', 'maximum' too'5' and 'default' too'2'</span></span>
> <span data-ttu-id="0b8ac-127">Opmerking: als er een probleem bij het lezen van de metrische gegevens voor resources Hallo en huidige capaciteit Hallo lager dan de standaardcapaciteit hello is, vervolgens tooensure Hallo beschikbaarheid van Hallo resource, automatisch schalen wordt uitschalen toohello standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-127">Note: In case there is a problem reading hello resource metrics and hello current capacity is below hello default capacity, then tooensure hello availability of hello resource, Autoscale will scale out toohello default value.</span></span> <span data-ttu-id="0b8ac-128">Als de huidige capaciteit Hallo al hoger dan de standaardcapaciteit is, worden niet automatisch schalen geschaald.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-128">If hello current capacity is already higher than default capacity, Autoscale will not scale in.</span></span>
- <span data-ttu-id="0b8ac-129">Klik op 'Opslaan'</span><span class="sxs-lookup"><span data-stu-id="0b8ac-129">Click on 'Save'</span></span>

<span data-ttu-id="0b8ac-130">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-130">Congratulations.</span></span> <span data-ttu-id="0b8ac-131">U hebt nu nu met succes is gemaakt voor uw scale tooauto schaal uw web-app op basis van een aangepaste waarde instellen.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-131">You now now succesfully created your scale setting tooauto scale your web app based on a custom metric.</span></span>

> <span data-ttu-id="0b8ac-132">Opmerking: hello dezelfde stappen zijn van toepassing tooget gestart met een VMSS of cloud service-rol.</span><span class="sxs-lookup"><span data-stu-id="0b8ac-132">Note: hello same steps are applicable tooget started with a VMSS or cloud service role.</span></span>

<!--Reference-->
[1]: https://docs.microsoft.com/en-us/azure/application-insights/app-insights-asp-net
[2]: https://portal.azure.com
[3]: ./media/monitoring-autoscale-scale-by-custom-metric/azure-monitor-launch.png
[4]: ./media/monitoring-autoscale-scale-by-custom-metric/discover-autoscale-azure-monitor.png
[5]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-scale-by-custom-metric/scale-by-custom-metric.png
[7]: ./media/monitoring-autoscale-scale-by-custom-metric/autoscale-setting-custom-metrics-ai.png

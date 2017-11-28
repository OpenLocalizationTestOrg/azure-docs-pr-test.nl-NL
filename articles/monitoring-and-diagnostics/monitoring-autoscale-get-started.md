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
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="7bf0e-103">Aan de slag met automatisch schalen in Azure</span><span class="sxs-lookup"><span data-stu-id="7bf0e-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="7bf0e-104">Dit artikel wordt beschreven hoe tooset uw instellingen voor automatisch schalen voor uw resource in Hallo Microsoft Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-104">This article describes how tooset up your Autoscale settings for your resource in hello Microsoft Azure portal.</span></span>

<span data-ttu-id="7bf0e-105">Monitor voor automatisch schalen die Azure geldt alleen toovirtual machineschaalsets, cloudservices, Azure App Service-abonnementen en App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-105">Azure Monitor Autoscale applies only toovirtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-hello-autoscale-settings-in-your-subscription"></a><span data-ttu-id="7bf0e-106">Instellingen voor het automatisch schalen in uw abonnement Hallo detecteren</span><span class="sxs-lookup"><span data-stu-id="7bf0e-106">Discover hello Autoscale settings in your subscription</span></span>
<span data-ttu-id="7bf0e-107">U kunt alle Hallo resources waarvoor automatisch schalen van toepassing in de Azure-Monitor is kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-107">You can discover all hello resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="7bf0e-108">Volgende stappen uit voor een stapsgewijze hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7bf0e-108">Use hello following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="7bf0e-109">Open Hallo [Azure-portal.][1]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-109">Open hello [Azure portal.][1]</span></span>
2. <span data-ttu-id="7bf0e-110">Klik op Hallo Azure Monitor pictogram in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-110">Click hello Azure Monitor icon in hello left pane.</span></span>
  <span data-ttu-id="7bf0e-111">![Open Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="7bf0e-112">Klik op **automatisch schalen** tooview alle Hallo bronnen voor welke automatisch schalen is van toepassing, samen met de huidige status voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-112">Click **Autoscale** tooview all hello resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="7bf0e-113">![Automatisch schalen in Azure Monitor detecteren][3]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="7bf0e-114">U kunt Hallo filterdeelvenster gebruiken op de bovenste tooscope Hallo Hallo lijst tooselect resources in een specifieke resourcegroep, specifieke brontypen of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-114">You can use hello filter pane at hello top tooscope down hello list tooselect resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="7bf0e-115">Voor elke resource vindt u het huidige aantal exemplaren Hallo en Hallo voor automatisch schalen die status.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-115">For each resource, you will find hello current instance count and hello Autoscale status.</span></span> <span data-ttu-id="7bf0e-116">Hallo automatisch schalen status kan zijn:</span><span class="sxs-lookup"><span data-stu-id="7bf0e-116">hello Autoscale status can be:</span></span>

- <span data-ttu-id="7bf0e-117">**Niet geconfigureerd**: U hebt automatisch schalen niet nog ingeschakeld voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="7bf0e-118">**Ingeschakeld**: U hebt automatisch schalen ingeschakeld voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="7bf0e-119">**Uitgeschakeld**: U hebt automatisch schalen uitgeschakeld voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="7bf0e-120">Maken van uw eerste instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="7bf0e-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="7bf0e-121">Laten we nu verloopt via een eenvoudige stapsgewijze toocreate uw eerste instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-121">Let's now go through a simple step-by-step walkthrough toocreate your first Autoscale setting.</span></span>

1. <span data-ttu-id="7bf0e-122">Open Hallo **automatisch schalen** blade in Azure Monitor en selecteer een resource die u tooscale wilt.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-122">Open hello **Autoscale** blade in Azure Monitor and select a resource that you want tooscale.</span></span> <span data-ttu-id="7bf0e-123">(hello volgende stappen uit een App Service-abonnement gebruiken die zijn gekoppeld aan een web-app.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-123">(hello following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="7bf0e-124">U kunt [uw eerste ASP.NET-web-app maken in Azure in vijf minuten.] [4])</span><span class="sxs-lookup"><span data-stu-id="7bf0e-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="7bf0e-125">Houd er rekening mee dat het huidige aantal exemplaren Hallo 1 is.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-125">Note that hello current instance count is 1.</span></span> <span data-ttu-id="7bf0e-126">Klik op **inschakelen voor automatisch schalen**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="7bf0e-127">![Instelling voor de nieuwe web-app schalen][5]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="7bf0e-128">Geef een naam voor Hallo schaal instellen en klik vervolgens op **een regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-128">Provide a name for hello scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="7bf0e-129">U ziet Hallo regel schalingsopties dat als een venster context aan de rechterkant Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-129">Notice hello scale rule options that open as a context pane on hello right side.</span></span> <span data-ttu-id="7bf0e-130">Dit wordt standaard ingesteld Hallo optie tooscale uw exemplaar 1 tellen als Hallo CPU-percentage van de resource Hallo groter is dan 70 procent.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-130">By default, this sets hello option tooscale your instance count by 1 if hello CPU percentage of hello resource exceeds 70 percent.</span></span> <span data-ttu-id="7bf0e-131">Laat het veld op de standaardwaarden en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="7bf0e-132">![Scale-instelling voor een web-app maken][6]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="7bf0e-133">U hebt nu uw eerste schaalregel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-133">You've now created your first scale rule.</span></span> <span data-ttu-id="7bf0e-134">Houd er rekening mee dat Hallo UX raadt aan best practices en dat ' het verdient aanbeveling toohave schaal als ten minste één regel. "</span><span class="sxs-lookup"><span data-stu-id="7bf0e-134">Note that hello UX recommends best practices and states that "It is recommended toohave at least one scale in rule."</span></span> <span data-ttu-id="7bf0e-135">toodo zodat:</span><span class="sxs-lookup"><span data-stu-id="7bf0e-135">toodo so:</span></span>
  
    <span data-ttu-id="7bf0e-136">a.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-136">a.</span></span> <span data-ttu-id="7bf0e-137">Klik op **een regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="7bf0e-138">b.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-138">b.</span></span> <span data-ttu-id="7bf0e-139">Stel **Operator** te**minder dan**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-139">Set **Operator** too**Less than**.</span></span>

    <span data-ttu-id="7bf0e-140">c.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-140">c.</span></span> <span data-ttu-id="7bf0e-141">Stel **drempelwaarde** te**20**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-141">Set **Threshold** too**20**.</span></span>

    <span data-ttu-id="7bf0e-142">d.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-142">d.</span></span> <span data-ttu-id="7bf0e-143">Stel **bewerking** te**verkleinen tellen per**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-143">Set **Operation** too**Decrease count by**.</span></span>

   <span data-ttu-id="7bf0e-144">U hebt nu een schaalinstelling dat kan worden geschaald out/schalen op basis van CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="7bf0e-145">![Schalen op basis van CPU][8]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="7bf0e-146">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-146">Click **Save**.</span></span>

<span data-ttu-id="7bf0e-147">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-147">Congratulations!</span></span> <span data-ttu-id="7bf0e-148">U hebt nu uw eerste schaal instelling tooautoscale uw web-app op basis van CPU-gebruik gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-148">You've now successfully created your first scale setting tooautoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="7bf0e-149">Hallo dezelfde stappen zijn van toepassing tooget gestart met een schaal van de virtuele machine instellen of cloud service-rol.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-149">hello same steps are applicable tooget started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="7bf0e-150">Andere overwegingen</span><span class="sxs-lookup"><span data-stu-id="7bf0e-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="7bf0e-151">Schalen op basis van een planning</span><span class="sxs-lookup"><span data-stu-id="7bf0e-151">Scale based on a schedule</span></span>
<span data-ttu-id="7bf0e-152">Bovendien tooscale op basis van CPU, kunt u instellen schaal anders voor specifieke dagen van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-152">In addition tooscale based on CPU, you can set your scale differently for specific days of hello week.</span></span>

1. <span data-ttu-id="7bf0e-153">Klik op **een scale-voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="7bf0e-154">Instelling Hallo scale Hallo-modus en de regels is dezelfde als standaardvoorwaarde voor Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-154">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="7bf0e-155">Selecteer **specifieke dagen herhalen** voor Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-155">Select **Repeat specific days** for hello schedule.</span></span>
4. <span data-ttu-id="7bf0e-156">Selecteer dagen Hallo en Hallo beginnen of eindigen tijd Hallo scale voorwaarde moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-156">Select hello days and hello start/end time for when hello scale condition should be applied.</span></span>

![Scale-voorwaarde op basis van de planning][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="7bf0e-158">Anders worden geschaald op specifieke datums</span><span class="sxs-lookup"><span data-stu-id="7bf0e-158">Scale differently on specific dates</span></span>
<span data-ttu-id="7bf0e-159">Bovendien tooscale op basis van CPU, kunt u instellen schaal anders voor specifieke datums.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-159">In addition tooscale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="7bf0e-160">Klik op **een scale-voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="7bf0e-161">Instelling Hallo scale Hallo-modus en de regels is dezelfde als standaardvoorwaarde voor Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-161">Setting hello scale mode and hello rules is hello same as hello default condition.</span></span>
3. <span data-ttu-id="7bf0e-162">Selecteer **Geef beginnen of eindigen datums** voor Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-162">Select **Specify start/end dates** for hello schedule.</span></span>
4. <span data-ttu-id="7bf0e-163">Selecteer Hallo beginnen of eindigen datums en tijden van de Hallo beginnen of eindigen Hallo scale voorwaarde moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-163">Select hello start/end dates and hello start/end time for when hello scale condition should be applied.</span></span>

![Scale-voorwaarde op basis van datums][10]

### <a name="view-hello-scale-history-of-your-resource"></a><span data-ttu-id="7bf0e-165">Hallo scale geschiedenis van uw resource weergeven</span><span class="sxs-lookup"><span data-stu-id="7bf0e-165">View hello scale history of your resource</span></span>
<span data-ttu-id="7bf0e-166">Wanneer de bron wordt geschaald omhoog of omlaag, wordt een gebeurtenis vastgelegd in het gebeurtenissenlogboek Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-166">Whenever your resource is scaled up or down, an event is logged in hello activity log.</span></span> <span data-ttu-id="7bf0e-167">U kunt Hallo scale geschiedenis van de bron voor Hallo afgelopen 24 uur weergeven door het overschakelen van toohello **Uitvoeringsgeschiedenis** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-167">You can view hello scale history of your resource for hello past 24 hours by switching toohello **Run history** tab.</span></span>

![geschiedenis uitvoeren][11]

<span data-ttu-id="7bf0e-169">Als u wilt dat tooview Hallo voltooid scale geschiedenis (voor omhoog too90 dagen), selecteer **Klik hier toosee meer details**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-169">If you want tooview hello complete scale history (for up too90 days), select **Click here toosee more details**.</span></span> <span data-ttu-id="7bf0e-170">Hallo activiteitenlogboek wordt geopend met automatisch schalen die vooraf zijn geselecteerd voor uw resource en categorie.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-170">hello activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-hello-scale-definition-of-your-resource"></a><span data-ttu-id="7bf0e-171">Hallo scale definitie van uw resource weergeven</span><span class="sxs-lookup"><span data-stu-id="7bf0e-171">View hello scale definition of your resource</span></span>
<span data-ttu-id="7bf0e-172">Automatisch schalen is een Azure Resource Manager-bron.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="7bf0e-173">U kunt Hallo scale definitie in JSON weergeven door het overschakelen van toohello **JSON** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-173">You can view hello scale definition in JSON by switching toohello **JSON** tab.</span></span>

![De definitie van de schaal][12]

<span data-ttu-id="7bf0e-175">U kunt wijzigingen aanbrengen in JSON rechtstreeks, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="7bf0e-176">Deze wijzigingen worden weergegeven nadat u deze opslaan.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="7bf0e-177">Schakel automatisch schalen en uw exemplaren handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="7bf0e-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="7bf0e-178">Mogelijk zijn er tijden als u wilt dat uw huidige schaalinstelling toodisable en handmatig schalen uw resource.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-178">There might be times when you want toodisable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="7bf0e-179">Klik op Hallo **uitschakelen voor automatisch schalen** knop Hallo boven.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-179">Click hello **Disable autoscale** button at hello top.</span></span>
<span data-ttu-id="7bf0e-180">![Schakel automatisch schalen][13]</span><span class="sxs-lookup"><span data-stu-id="7bf0e-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="7bf0e-181">Deze optie wordt uitgeschakeld voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-181">This option disables your configuration.</span></span> <span data-ttu-id="7bf0e-182">Echter, kun je weer tooit nadat u automatisch schalen opnieuw inschakelen.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-182">However, you can get back tooit after you enable Autoscale again.</span></span> 

<span data-ttu-id="7bf0e-183">U kunt nu het aantal exemplaren dat u wilt dat tooscale toomanually Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-183">You can now set hello number of instances that you want tooscale toomanually.</span></span>

![Set handmatig schalen][14]

<span data-ttu-id="7bf0e-185">U kunt altijd tooAutoscale terugkeren door te klikken op **inschakelen voor automatisch schalen** en vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="7bf0e-185">You can always return tooAutoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7bf0e-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bf0e-186">Next steps</span></span>
- [<span data-ttu-id="7bf0e-187">Een activiteit logboek waarschuwing toomonitor alle automatisch schalen engine bewerkingen voor uw abonnement maken</span><span class="sxs-lookup"><span data-stu-id="7bf0e-187">Create an Activity Log Alert toomonitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="7bf0e-188">Alle mislukte bewerkingen worden uitgevoerd voor automatisch schalen scale-in/scale-out op uw abonnement voor een activiteit logboek waarschuwing toomonitor maken</span><span class="sxs-lookup"><span data-stu-id="7bf0e-188">Create an Activity Log Alert toomonitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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


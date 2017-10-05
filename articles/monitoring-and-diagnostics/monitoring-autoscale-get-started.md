---
title: Aan de slag met automatisch schalen in Azure | Microsoft Docs
description: Informatie over het schalen van uw resources in Azure.
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
ms.openlocfilehash: 68cb624b3ef4a77e7cfc949979e0b1949c2e5535
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="1ba70-103">Aan de slag met automatisch schalen in Azure</span><span class="sxs-lookup"><span data-stu-id="1ba70-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="1ba70-104">Dit artikel wordt beschreven hoe u uw instellingen voor automatisch schalen voor uw resource in de Microsoft Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1ba70-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="1ba70-105">Monitor voor automatisch schalen die Azure geldt alleen voor virtuele-machineschaalsets, cloudservices, Azure App Service-abonnementen en App Service-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="1ba70-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="1ba70-106">De instellingen voor automatisch schalen in uw abonnement detecteren</span><span class="sxs-lookup"><span data-stu-id="1ba70-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="1ba70-107">U kunt alle resources waarvoor automatisch schalen van toepassing in de Azure-Monitor is kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="1ba70-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="1ba70-108">Gebruik de volgende stappen uit voor een stapsgewijze:</span><span class="sxs-lookup"><span data-stu-id="1ba70-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="1ba70-109">Open de [Azure-portal.][1]</span><span class="sxs-lookup"><span data-stu-id="1ba70-109">Open the [Azure portal.][1]</span></span>
2. <span data-ttu-id="1ba70-110">Klik op het pictogram van de Azure-Monitor in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="1ba70-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="1ba70-111">![Open Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="1ba70-111">![Open Azure Monitor][2]</span></span>
3. <span data-ttu-id="1ba70-112">Klik op **automatisch schalen** om alle resources waarvoor automatisch schalen van toepassing, samen met de huidige status voor automatisch schalen is weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1ba70-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="1ba70-113">![Automatisch schalen in Azure Monitor detecteren][3]</span><span class="sxs-lookup"><span data-stu-id="1ba70-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="1ba70-114">U kunt het filterdeelvenster boven aan het bereik omlaag in de lijst gebruiken om resources te selecteren in een specifieke resourcegroep, specifieke brontypen of een specifieke bron.</span><span class="sxs-lookup"><span data-stu-id="1ba70-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="1ba70-115">Voor elke resource vindt u het huidige aantal exemplaren en de status voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="1ba70-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="1ba70-116">De status voor automatisch schalen kan zijn:</span><span class="sxs-lookup"><span data-stu-id="1ba70-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="1ba70-117">**Niet geconfigureerd**: U hebt automatisch schalen niet nog ingeschakeld voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="1ba70-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="1ba70-118">**Ingeschakeld**: U hebt automatisch schalen ingeschakeld voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="1ba70-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="1ba70-119">**Uitgeschakeld**: U hebt automatisch schalen uitgeschakeld voor deze bron.</span><span class="sxs-lookup"><span data-stu-id="1ba70-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="1ba70-120">Maken van uw eerste instelling voor automatisch schalen</span><span class="sxs-lookup"><span data-stu-id="1ba70-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="1ba70-121">Laten we nu verloopt via een eenvoudige stapsgewijze voor het maken van uw eerste instelling voor automatisch schalen.</span><span class="sxs-lookup"><span data-stu-id="1ba70-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="1ba70-122">Open de **automatisch schalen** blade in Azure Monitor en selecteer een resource die u wilt schalen.</span><span class="sxs-lookup"><span data-stu-id="1ba70-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="1ba70-123">(Een App Service-plan dat is gekoppeld aan een web-app de volgende stappen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1ba70-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="1ba70-124">U kunt [uw eerste ASP.NET-web-app maken in Azure in vijf minuten.] [4])</span><span class="sxs-lookup"><span data-stu-id="1ba70-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
2. <span data-ttu-id="1ba70-125">Houd er rekening mee dat het huidige aantal exemplaren 1 is.</span><span class="sxs-lookup"><span data-stu-id="1ba70-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="1ba70-126">Klik op **inschakelen voor automatisch schalen**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="1ba70-127">![Instelling voor de nieuwe web-app schalen][5]</span><span class="sxs-lookup"><span data-stu-id="1ba70-127">![Scale setting for new web app][5]</span></span>
3. <span data-ttu-id="1ba70-128">Geef een naam voor de instelling schalen en klik vervolgens op **een regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="1ba70-129">Let op de regel schalingsopties die als een deelvenster context aan de rechterkant geopend.</span><span class="sxs-lookup"><span data-stu-id="1ba70-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="1ba70-130">Hiermee wordt de optie voor het schalen van het aantal exemplaren op 1 als het CPU-percentage van de resource groter is dan 70 procent standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1ba70-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="1ba70-131">Laat het veld op de standaardwaarden en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="1ba70-132">![Scale-instelling voor een web-app maken][6]</span><span class="sxs-lookup"><span data-stu-id="1ba70-132">![Create scale setting for a web app][6]</span></span>
4. <span data-ttu-id="1ba70-133">U hebt nu uw eerste schaalregel gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ba70-133">You've now created your first scale rule.</span></span> <span data-ttu-id="1ba70-134">Houd er rekening mee dat de UX raadt aan om de aanbevolen procedures en statussen dat 'het verdient aanbeveling om ten minste één scale in regel."</span><span class="sxs-lookup"><span data-stu-id="1ba70-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="1ba70-135">Dit doet u als volgt:</span><span class="sxs-lookup"><span data-stu-id="1ba70-135">To do so:</span></span>
  
    <span data-ttu-id="1ba70-136">a.</span><span class="sxs-lookup"><span data-stu-id="1ba70-136">a.</span></span> <span data-ttu-id="1ba70-137">Klik op **een regel toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="1ba70-138">b.</span><span class="sxs-lookup"><span data-stu-id="1ba70-138">b.</span></span> <span data-ttu-id="1ba70-139">Stel **Operator** naar **minder dan**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="1ba70-140">c.</span><span class="sxs-lookup"><span data-stu-id="1ba70-140">c.</span></span> <span data-ttu-id="1ba70-141">Stel **drempelwaarde** naar **20**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="1ba70-142">d.</span><span class="sxs-lookup"><span data-stu-id="1ba70-142">d.</span></span> <span data-ttu-id="1ba70-143">Stel **bewerking** naar **verkleinen tellen per**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="1ba70-144">U hebt nu een schaalinstelling dat kan worden geschaald out/schalen op basis van CPU-gebruik.</span><span class="sxs-lookup"><span data-stu-id="1ba70-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="1ba70-145">![Schalen op basis van CPU][8]</span><span class="sxs-lookup"><span data-stu-id="1ba70-145">![Scale based on CPU][8]</span></span>
5. <span data-ttu-id="1ba70-146">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-146">Click **Save**.</span></span>

<span data-ttu-id="1ba70-147">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="1ba70-147">Congratulations!</span></span> <span data-ttu-id="1ba70-148">U hebt nu uw eerste scale-instelling voor automatisch schalen die uw web-app op basis van CPU-gebruik gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ba70-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="1ba70-149">Dezelfde stappen van toepassing zijn op aan de slag met een virtuele-machineschaalset of cloud service-rol.</span><span class="sxs-lookup"><span data-stu-id="1ba70-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="1ba70-150">Andere overwegingen</span><span class="sxs-lookup"><span data-stu-id="1ba70-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="1ba70-151">Schalen op basis van een planning</span><span class="sxs-lookup"><span data-stu-id="1ba70-151">Scale based on a schedule</span></span>
<span data-ttu-id="1ba70-152">Naast de schaal aan op basis van CPU, kunt u uw scale anders instellen voor specifieke dagen van de week.</span><span class="sxs-lookup"><span data-stu-id="1ba70-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="1ba70-153">Klik op **een scale-voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-153">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="1ba70-154">Instellen van de scale-modus en de regels is hetzelfde als de standaardvoorwaarde.</span><span class="sxs-lookup"><span data-stu-id="1ba70-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="1ba70-155">Selecteer **specifieke dagen herhalen** voor de planning.</span><span class="sxs-lookup"><span data-stu-id="1ba70-155">Select **Repeat specific days** for the schedule.</span></span>
4. <span data-ttu-id="1ba70-156">Selecteer de dagen en de tijd beginnen of eindigen voor waarop de voorwaarde van de schaal moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="1ba70-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Scale-voorwaarde op basis van de planning][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="1ba70-158">Anders worden geschaald op specifieke datums</span><span class="sxs-lookup"><span data-stu-id="1ba70-158">Scale differently on specific dates</span></span>
<span data-ttu-id="1ba70-159">Naast de schaal aan op basis van CPU, kunt u uw scale anders instellen voor specifieke datums.</span><span class="sxs-lookup"><span data-stu-id="1ba70-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="1ba70-160">Klik op **een scale-voorwaarde toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-160">Click **Add a scale condition**.</span></span>
2. <span data-ttu-id="1ba70-161">Instellen van de scale-modus en de regels is hetzelfde als de standaardvoorwaarde.</span><span class="sxs-lookup"><span data-stu-id="1ba70-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
3. <span data-ttu-id="1ba70-162">Selecteer **Geef beginnen of eindigen datums** voor de planning.</span><span class="sxs-lookup"><span data-stu-id="1ba70-162">Select **Specify start/end dates** for the schedule.</span></span>
4. <span data-ttu-id="1ba70-163">Selecteer de datums beginnen of eindigen en de tijd beginnen of eindigen voor waarop de voorwaarde van de schaal moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="1ba70-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Scale-voorwaarde op basis van datums][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="1ba70-165">De geschiedenis van de schaal van uw resource weergeven</span><span class="sxs-lookup"><span data-stu-id="1ba70-165">View the scale history of your resource</span></span>
<span data-ttu-id="1ba70-166">Wanneer de bron wordt geschaald omhoog of omlaag, wordt een gebeurtenis vastgelegd in het gebeurtenissenlogboek.</span><span class="sxs-lookup"><span data-stu-id="1ba70-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="1ba70-167">U kunt de geschiedenis van de schaal van uw resource weergeven voor de afgelopen 24 uur door het overschakelen naar de **Uitvoeringsgeschiedenis** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1ba70-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![geschiedenis uitvoeren][11]

<span data-ttu-id="1ba70-169">Als u wilt weergeven van de geschiedenis van de volledige schaal (voor maximaal 90 dagen), selecteert u **Klik hier voor meer informatie**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="1ba70-170">Het activiteitenlogboek wordt geopend met automatisch schalen die vooraf zijn geselecteerd voor uw resource en categorie.</span><span class="sxs-lookup"><span data-stu-id="1ba70-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="1ba70-171">De definitie van de schaal van uw resource weergeven</span><span class="sxs-lookup"><span data-stu-id="1ba70-171">View the scale definition of your resource</span></span>
<span data-ttu-id="1ba70-172">Automatisch schalen is een Azure Resource Manager-bron.</span><span class="sxs-lookup"><span data-stu-id="1ba70-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="1ba70-173">U kunt de definitie van de schaal in JSON weergeven door het overschakelen naar de **JSON** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1ba70-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![De definitie van de schaal][12]

<span data-ttu-id="1ba70-175">U kunt wijzigingen aanbrengen in JSON rechtstreeks, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="1ba70-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="1ba70-176">Deze wijzigingen worden weergegeven nadat u deze opslaan.</span><span class="sxs-lookup"><span data-stu-id="1ba70-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="1ba70-177">Schakel automatisch schalen en uw exemplaren handmatig schalen</span><span class="sxs-lookup"><span data-stu-id="1ba70-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="1ba70-178">Er is mogelijk dat u wilt uw huidige schaalinstelling uitschakelen en handmatig schalen uw resource.</span><span class="sxs-lookup"><span data-stu-id="1ba70-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="1ba70-179">Klik op de **uitschakelen voor automatisch schalen** bovenaan op de knop.</span><span class="sxs-lookup"><span data-stu-id="1ba70-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="1ba70-180">![Schakel automatisch schalen][13]</span><span class="sxs-lookup"><span data-stu-id="1ba70-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="1ba70-181">Deze optie wordt uitgeschakeld voor uw configuratie.</span><span class="sxs-lookup"><span data-stu-id="1ba70-181">This option disables your configuration.</span></span> <span data-ttu-id="1ba70-182">Echter, u kunt teruggaan naar het nadat u automatisch schalen opnieuw inschakelen.</span><span class="sxs-lookup"><span data-stu-id="1ba70-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="1ba70-183">U kunt nu het aantal exemplaren dat u schalen wilt naar handmatig instellen.</span><span class="sxs-lookup"><span data-stu-id="1ba70-183">You can now set the number of instances that you want to scale to manually.</span></span>

![Set handmatig schalen][14]

<span data-ttu-id="1ba70-185">U kunt altijd terugkeren naar automatisch schalen door te klikken op **inschakelen voor automatisch schalen** en vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1ba70-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ba70-186">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ba70-186">Next steps</span></span>
- [<span data-ttu-id="1ba70-187">Een activiteit logboek-waarschuwing voor het bewaken van alle automatisch schalen engine bewerkingen voor uw abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1ba70-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="1ba70-188">Een activiteit logboek-waarschuwing voor het bewaken van alle mislukte bewerkingen worden uitgevoerd voor automatisch schalen scale-in/scale-out op uw abonnement maken</span><span class="sxs-lookup"><span data-stu-id="1ba70-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

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


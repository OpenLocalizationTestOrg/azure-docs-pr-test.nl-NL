---
title: Veelgestelde vragen over IoT-Suite aaaAzure | Microsoft Docs
description: Veelgestelde vragen over IoT Suite
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: cb537749-a8a1-4e53-b3bf-f1b64a38188a
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: corywink
ms.openlocfilehash: cb39e24af6d1ce2afea554285512d05b2d7c721e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="f5393-103">Veelgestelde vragen over IoT Suite</span><span class="sxs-lookup"><span data-stu-id="f5393-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="f5393-104">Zie ook Hallo verbonden factory specifieke [Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="f5393-104">See also, hello connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-hello-source-code-for-hello-preconfigured-solutions"></a><span data-ttu-id="f5393-105">Waar vind ik broncode Hallo Hallo vooraf geconfigureerde oplossingen</span><span class="sxs-lookup"><span data-stu-id="f5393-105">Where can I find hello source code for hello preconfigured solutions?</span></span>

<span data-ttu-id="f5393-106">Hallo broncode is opgeslagen in Hallo GitHub-opslagplaatsen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f5393-106">hello source code is stored in hello following GitHub repositories:</span></span>
* <span data-ttu-id="f5393-107">[Vooraf geconfigureerde oplossing voor externe controle][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="f5393-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="f5393-108">[Oplossing voor voorspeld onderhoud vooraf geconfigureerde][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="f5393-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="f5393-109">Verbonden factory vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="f5393-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-toohello-latest-version-of-hello-remote-monitoring-preconfigured-solution-that-uses-hello-iot-hub-device-management-features"></a><span data-ttu-id="f5393-110">Hoe kan ik toohello meest recente versie van Hallo vooraf geconfigureerde oplossing voor externe controle dat maakt gebruik van IoT Hub apparaat-beheerfuncties Hallo bijwerken?</span><span class="sxs-lookup"><span data-stu-id="f5393-110">How do I update toohello latest version of hello remote monitoring preconfigured solution that uses hello IoT Hub device management features?</span></span>

* <span data-ttu-id="f5393-111">Als u een vooraf geconfigureerde oplossing van Hallo https://www.azureiotsuite.com/ site implementeert, implementeert deze altijd een nieuw exemplaar van de meest recente versie van de Hallo van Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="f5393-111">If you deploy a preconfigured solution from hello https://www.azureiotsuite.com/ site, it always deploys a new instance of hello latest version of hello solution.</span></span>
* <span data-ttu-id="f5393-112">Als u een vooraf geconfigureerde oplossing met behulp van de opdrachtregel Hallo implementeert, kunt u een bestaande implementatie bijwerken met nieuwe code.</span><span class="sxs-lookup"><span data-stu-id="f5393-112">If you deploy a preconfigured solution using hello command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="f5393-113">Zie [Cloud implementatie] [ lnk-cloud-deployment] in GitHub hello [opslagplaats][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="f5393-113">See [Cloud deployment][lnk-cloud-deployment] in hello GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-toohello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="f5393-114">Hoe kan ik ondersteuning voor een vooraf geconfigureerde oplossing voor externe controle nieuwe apparaat methode toohello toevoegen?</span><span class="sxs-lookup"><span data-stu-id="f5393-114">How can I add support for a new device method toohello remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="f5393-115">Zie de sectie Hallo [ondersteuning toevoegen voor een nieuwe methode toohello simulator] [ lnk-add-method] in Hallo [aanpassen van een vooraf geconfigureerde oplossing] [ lnk-customize] artikel.</span><span class="sxs-lookup"><span data-stu-id="f5393-115">See hello section [Add support for a new method toohello simulator][lnk-add-method] in hello [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="hello-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="f5393-116">Hallo gesimuleerd apparaat negeert mijn gewenste eigenschapswijzigingen waarom?</span><span class="sxs-lookup"><span data-stu-id="f5393-116">hello simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="f5393-117">In Hallo als externe controle vooraf geconfigureerde oplossing, gebruikt de Hallo gesimuleerd apparaatcode alleen Hallo **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenst eigenschappen Hallo tooupdate gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f5393-117">In hello remote monitoring preconfigured solution, hello simulated device code only uses hello **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties tooupdate hello reported properties.</span></span> <span data-ttu-id="f5393-118">Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="f5393-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-hello-list-of-devices-in-hello-solution-dashboard-why"></a><span data-ttu-id="f5393-119">Mijn apparaat niet wordt weergegeven in de lijst Hallo van apparaten in het dashboard van de oplossing hello, waarom?</span><span class="sxs-lookup"><span data-stu-id="f5393-119">My device does not appear in hello list of devices in hello solution dashboard, why?</span></span>

<span data-ttu-id="f5393-120">lijst van apparaten in het dashboard van de oplossing Hallo Hallo maakt gebruik van een query tooreturn Hallo lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="f5393-120">hello list of devices in hello solution dashboard uses a query tooreturn hello list of devices.</span></span> <span data-ttu-id="f5393-121">Op dit moment wordt kan niet een query meer dan 10K apparaten retourneren.</span><span class="sxs-lookup"><span data-stu-id="f5393-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="f5393-122">Probeer te Hallo zoekcriteria voor uw query meer beperkende maken.</span><span class="sxs-lookup"><span data-stu-id="f5393-122">Try making hello search criteria for your query more restrictive.</span></span>

### <a name="whats-hello-difference-between-deleting-a-resource-group-in-hello-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="f5393-123">Wat is Hallo verschil tussen het verwijderen van een resourcegroep in hello Azure portal en te klikken op verwijderen op een vooraf geconfigureerde oplossing op azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="f5393-123">What's hello difference between deleting a resource group in hello Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="f5393-124">Als u Hallo vooraf geconfigureerde oplossing in verwijdert [azureiotsuite.com][lnk-azureiotsuite], verwijdert u alle Hallo-resources die zijn ingericht toen u Hallo vooraf geconfigureerde oplossing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f5393-124">If you delete hello preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span> <span data-ttu-id="f5393-125">Als u aanvullende bronnen toohello resourcegroep hebt toegevoegd, worden deze resources worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="f5393-125">If you added additional resources toohello resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="f5393-126">Als u de resourcegroep Hallo in Hallo verwijdert [Azure-portal][lnk-azure-portal], verwijdert u alleen Hallo resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="f5393-126">If you delete hello resource group in hello [Azure portal][lnk-azure-portal], you only delete hello resources in that resource group.</span></span> <span data-ttu-id="f5393-127">U moet ook toodelete hello Azure Active Directory-toepassing hello vooraf geconfigureerde oplossing in Hallo gekoppeld [klassieke Azure-portal][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="f5393-127">You also need toodelete hello Azure Active Directory application associated with hello preconfigured solution in hello [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="f5393-128">Hoeveel exemplaren van de IoT Hub kan ik inrichten in een abonnement?</span><span class="sxs-lookup"><span data-stu-id="f5393-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="f5393-129">Standaard kunt u inrichten [10 IoT hubs per abonnement][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="f5393-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="f5393-130">Kunt u een [Azure-ondersteuningsticket] [ link-azuresupportticket] tooraise deze limiet.</span><span class="sxs-lookup"><span data-stu-id="f5393-130">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit.</span></span> <span data-ttu-id="f5393-131">Als gevolg hiervan kunt sinds de bepalingen van elke vooraf geconfigureerde oplossing voor een nieuwe IoT Hub, u alleen richten up too10 vooraf oplossingen in een bepaald abonnement geconfigureerde.</span><span class="sxs-lookup"><span data-stu-id="f5393-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up too10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="f5393-132">Hoeveel exemplaren van Azure DB die Cosmos kan ik inrichten in een abonnement?</span><span class="sxs-lookup"><span data-stu-id="f5393-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="f5393-133">Vijftig.</span><span class="sxs-lookup"><span data-stu-id="f5393-133">Fifty.</span></span> <span data-ttu-id="f5393-134">Kunt u een [Azure-ondersteuningsticket] [ link-azuresupportticket] tooraise dit beperken, maar standaard kunt u alleen 50 exemplaren van de Cosmos-database per abonnement inrichten.</span><span class="sxs-lookup"><span data-stu-id="f5393-134">You can create an [Azure support ticket][link-azuresupportticket] tooraise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="f5393-135">Hoeveel gratis Bing Kaarten-API's kan ik inrichten met een abonnement?</span><span class="sxs-lookup"><span data-stu-id="f5393-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="f5393-136">Twee.</span><span class="sxs-lookup"><span data-stu-id="f5393-136">Two.</span></span> <span data-ttu-id="f5393-137">U kunt slechts twee interne transacties niveau 1 Bing-kaarten voor Enterprise plannen in een Azure-abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="f5393-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="f5393-138">Hallo-oplossing voor externe controle is standaard ingericht met Hallo interne transacties niveau 1-plan.</span><span class="sxs-lookup"><span data-stu-id="f5393-138">hello remote monitoring solution is provisioned by default with hello Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="f5393-139">Als gevolg hiervan kunt u alleen inrichten up tootwo externe bewakingsoplossingen in een abonnement zonder wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f5393-139">As a result, you can only provision up tootwo remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="f5393-140">Ik heb een implementatie van een externe bewakingsoplossing met een statische kaart, hoe voeg ik een interactieve Bing-kaart toe?</span><span class="sxs-lookup"><span data-stu-id="f5393-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="f5393-141">Ophalen van uw Bing kaarten-API voor Enterprise-querysleutel in [Azure-portal][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="f5393-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="f5393-142">Navigeer toohello resourcegroep waar uw Bing kaarten-API voor Enterprise zich in Hallo bevindt [Azure-portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="f5393-142">Navigate toohello Resource Group where your Bing Maps API for Enterprise is in hello [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="f5393-143">Klik op **alle instellingen**, klikt u vervolgens **Sleutelbeheer**.</span><span class="sxs-lookup"><span data-stu-id="f5393-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="f5393-144">U ziet twee sleutels: **hoofdsleutel** en **querysleutel**.</span><span class="sxs-lookup"><span data-stu-id="f5393-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="f5393-145">Hallo-waarde voor kopiëren **querysleutel**.</span><span class="sxs-lookup"><span data-stu-id="f5393-145">Copy hello value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="f5393-146">U hebt geen Bing Kaarten-API voor Enterprise-account?</span><span class="sxs-lookup"><span data-stu-id="f5393-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="f5393-147">Maken van een in Hallo [Azure-portal] [ lnk-azure-portal] door te klikken op + Nieuw, zoeken naar Bing kaarten-API voor Enterprise- en volg toocreate vraagt.</span><span class="sxs-lookup"><span data-stu-id="f5393-147">Create one in hello [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts toocreate.</span></span>
      > 
      > 
2. <span data-ttu-id="f5393-148">Ophalen van de meest recente code Hallo van Hallo [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="f5393-148">Pull down hello latest code from hello [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="f5393-149">Uitvoeren van een lokale implementatie of een cloudimplementatie Hallo opdrachtregelprogramma implementatierichtlijnen in Hallo /docs/ map in de opslagplaats hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="f5393-149">Run a local or cloud deployment following hello command-line deployment guidance in hello /docs/ folder in hello repository.</span></span> 
4. <span data-ttu-id="f5393-150">Nadat u hebt uitgevoerd van een lokale implementatie of een cloudimplementatie, zoekt u naar in de hoofdmap voor Hallo *. user.config-bestand gemaakt tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="f5393-150">After you've run a local or cloud deployment, look in your root folder for hello *.user.config file created during deployment.</span></span> <span data-ttu-id="f5393-151">Open dit bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="f5393-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="f5393-152">Wijziging Hallo volgende regel tooinclude Hallo waarde die u hebt gekopieerd uit uw **querysleutel**:</span><span class="sxs-lookup"><span data-stu-id="f5393-152">Change hello following line tooinclude hello value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="f5393-153">Kan ik een vooraf geconfigureerde oplossing maken als ik Microsoft Azure voor DreamSpark heb?</span><span class="sxs-lookup"><span data-stu-id="f5393-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="f5393-154">Op dit moment kunt u een vooraf geconfigureerde oplossing met geen maken een [Microsoft Azure voor DreamSpark] [ lnk-dreamspark] account.</span><span class="sxs-lookup"><span data-stu-id="f5393-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="f5393-155">U kunt echter maken een [gratis proefaccount voor Azure] [ lnk-30daytrial] binnen een paar minuten waarmee u een vooraf geconfigureerde oplossing maken.</span><span class="sxs-lookup"><span data-stu-id="f5393-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="f5393-156">Kan ik een vooraf geconfigureerde oplossing maken als ik Cloud Solution Provider (CSP) abonnement?</span><span class="sxs-lookup"><span data-stu-id="f5393-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="f5393-157">U kunt op dit moment een vooraf geconfigureerde oplossing maken met een abonnement Cloud Solution Provider (CSP).</span><span class="sxs-lookup"><span data-stu-id="f5393-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="f5393-158">U kunt echter maken een [gratis proefaccount voor Azure] [ lnk-30daytrial] binnen een paar minuten waarmee u een vooraf geconfigureerde oplossing maken.</span><span class="sxs-lookup"><span data-stu-id="f5393-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="f5393-159">Hoe verwijder ik een AAD-tenant?</span><span class="sxs-lookup"><span data-stu-id="f5393-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="f5393-160">Zie het blogbericht van Eric Golpe van [overzicht van het verwijderen van een Azure AD-Tenant][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="f5393-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="f5393-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f5393-161">Next steps</span></span>

<span data-ttu-id="f5393-162">U kunt ook verkennen van Hallo andere functies en mogelijkheden van Hallo vooraf geconfigureerde IoT Suite-oplossingen:</span><span class="sxs-lookup"><span data-stu-id="f5393-162">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="f5393-163">[Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="f5393-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="f5393-164">Overzicht van de verbonden factory vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="f5393-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="f5393-165">[Beveiliging van de IoT van Hallo gemalen][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="f5393-165">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[lnk-predictive-overview]: iot-suite-predictive-overview.md
[lnk-security-groundup]: securing-iot-ground-up.md

[link-azuresupportticket]: https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade 
[link-azuresublimits]: https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/#iot-hub-limits
[lnk-azure-portal]: https://portal.azure.com
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-classic-portal]: https://manage.windowsazure.com
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring 
[lnk-dreamspark]: https://www.dreamspark.com/Product/Product.aspx?productid=99 
[lnk-30daytrial]: https://azure.microsoft.com/free/
[lnk-delete-aad-tennant]: http://blogs.msdn.com/b/ericgolpe/archive/2015/04/30/walkthrough-of-deleting-an-azure-ad-tenant.aspx
[lnk-cloud-deployment]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/cloud-deployment.md
[lnk-add-method]: iot-suite-guidance-on-customizing-preconfigured-solutions.md#add-support-for-a-new-method-to-the-simulator
[lnk-customize]: iot-suite-guidance-on-customizing-preconfigured-solutions.md
[lnk-remote-monitoring-github]: https://github.com/Azure/azure-iot-remote-monitoring
[lnk-predictive-maintenance-github]: https://github.com/Azure/azure-iot-predictive-maintenance

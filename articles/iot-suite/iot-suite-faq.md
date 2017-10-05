---
title: Azure IoT Suite Veelgestelde vragen | Microsoft Docs
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
ms.openlocfilehash: 85867fb8d18377637b3aa848555831a8d9b53512
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="frequently-asked-questions-for-iot-suite"></a><span data-ttu-id="210ff-103">Veelgestelde vragen over IoT Suite</span><span class="sxs-lookup"><span data-stu-id="210ff-103">Frequently asked questions for IoT Suite</span></span>

<span data-ttu-id="210ff-104">Zie ook de specifieke verbonden factory [Veelgestelde vragen over](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="210ff-104">See also, the connected factory specific [FAQ](iot-suite-faq-cf.md).</span></span>

### <a name="where-can-i-find-the-source-code-for-the-preconfigured-solutions"></a><span data-ttu-id="210ff-105">Waar vind ik de broncode voor de vooraf geconfigureerde oplossingen</span><span class="sxs-lookup"><span data-stu-id="210ff-105">Where can I find the source code for the preconfigured solutions?</span></span>

<span data-ttu-id="210ff-106">De broncode is opgeslagen in de volgende GitHub-opslagplaatsen:</span><span class="sxs-lookup"><span data-stu-id="210ff-106">The source code is stored in the following GitHub repositories:</span></span>
* <span data-ttu-id="210ff-107">[Vooraf geconfigureerde oplossing voor externe controle][lnk-remote-monitoring-github]</span><span class="sxs-lookup"><span data-stu-id="210ff-107">[Remote monitoring preconfigured solution][lnk-remote-monitoring-github]</span></span>
* <span data-ttu-id="210ff-108">[Oplossing voor voorspeld onderhoud vooraf geconfigureerde][lnk-predictive-maintenance-github]</span><span class="sxs-lookup"><span data-stu-id="210ff-108">[Predictive maintenance preconfigured solution][lnk-predictive-maintenance-github]</span></span>
* [<span data-ttu-id="210ff-109">Verbonden factory vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="210ff-109">Connected factory preconfigured solution</span></span>](https://github.com/Azure/azure-iot-connected-factory)

### <a name="how-do-i-update-to-the-latest-version-of-the-remote-monitoring-preconfigured-solution-that-uses-the-iot-hub-device-management-features"></a><span data-ttu-id="210ff-110">Hoe kan ik bijwerken naar de nieuwste versie van de vooraf geconfigureerde oplossing voor externe controle die gebruikmaakt van de beheerfuncties van de IoT Hub-apparaten?</span><span class="sxs-lookup"><span data-stu-id="210ff-110">How do I update to the latest version of the remote monitoring preconfigured solution that uses the IoT Hub device management features?</span></span>

* <span data-ttu-id="210ff-111">Als u een vooraf geconfigureerde oplossing van de site https://www.azureiotsuite.com/ implementeert, implementeert deze altijd een nieuw exemplaar van de meest recente versie van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="210ff-111">If you deploy a preconfigured solution from the https://www.azureiotsuite.com/ site, it always deploys a new instance of the latest version of the solution.</span></span>
* <span data-ttu-id="210ff-112">Als u een vooraf geconfigureerde oplossing via de opdrachtregel implementeert, kunt u een bestaande implementatie bijwerken met nieuwe code.</span><span class="sxs-lookup"><span data-stu-id="210ff-112">If you deploy a preconfigured solution using the command line, you can update an existing deployment with new code.</span></span> <span data-ttu-id="210ff-113">Zie [Cloud implementatie] [ lnk-cloud-deployment] in de GitHub [opslagplaats][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="210ff-113">See [Cloud deployment][lnk-cloud-deployment] in the GitHub [repository][lnk-remote-monitoring-github].</span></span>

### <a name="how-can-i-add-support-for-a-new-device-method-to-the-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="210ff-114">Hoe kan ik ondersteuning voor een nieuwe apparaat-methode toevoegen aan de vooraf geconfigureerde oplossing voor externe controle?</span><span class="sxs-lookup"><span data-stu-id="210ff-114">How can I add support for a new device method to the remote monitoring preconfigured solution?</span></span>

<span data-ttu-id="210ff-115">Zie de sectie [ondersteuning voor een nieuwe methode toevoegen aan de simulator] [ lnk-add-method] in de [aanpassen van een vooraf geconfigureerde oplossing] [ lnk-customize] artikel.</span><span class="sxs-lookup"><span data-stu-id="210ff-115">See the section [Add support for a new method to the simulator][lnk-add-method] in the [Customize a preconfigured solution][lnk-customize] article.</span></span>

### <a name="the-simulated-device-is-ignoring-my-desired-property-changes-why"></a><span data-ttu-id="210ff-116">Het gesimuleerde apparaat negeert mijn gewenste eigenschapswijzigingen waarom?</span><span class="sxs-lookup"><span data-stu-id="210ff-116">The simulated device is ignoring my desired property changes, why?</span></span>
<span data-ttu-id="210ff-117">In de vooraf geconfigureerde oplossing voor externe controle, het gesimuleerde apparaat code alleen gebruikt de **Desired.Config.TemperatureMeanValue** en **Desired.Config.TelemetryInterval** gewenst eigenschappen de eigenschappen van de gerapporteerde bijwerken.</span><span class="sxs-lookup"><span data-stu-id="210ff-117">In the remote monitoring preconfigured solution, the simulated device code only uses the **Desired.Config.TemperatureMeanValue** and **Desired.Config.TelemetryInterval** desired properties to update the reported properties.</span></span> <span data-ttu-id="210ff-118">Alle andere gewenste eigenschap wijzigingsaanvragen worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="210ff-118">All other desired property change requests are ignored.</span></span>

### <a name="my-device-does-not-appear-in-the-list-of-devices-in-the-solution-dashboard-why"></a><span data-ttu-id="210ff-119">Mijn apparaat niet wordt weergegeven in de lijst met apparaten in het dashboard van de oplossing waarom?</span><span class="sxs-lookup"><span data-stu-id="210ff-119">My device does not appear in the list of devices in the solution dashboard, why?</span></span>

<span data-ttu-id="210ff-120">De lijst met apparaten in het dashboard van de oplossing maakt gebruik van een query te retourneren van de lijst met apparaten.</span><span class="sxs-lookup"><span data-stu-id="210ff-120">The list of devices in the solution dashboard uses a query to return the list of devices.</span></span> <span data-ttu-id="210ff-121">Op dit moment wordt kan niet een query meer dan 10K apparaten retourneren.</span><span class="sxs-lookup"><span data-stu-id="210ff-121">Currently, a query cannot return more than 10K devices.</span></span> <span data-ttu-id="210ff-122">Maak de zoekcriteria voor uw query meer beperkende.</span><span class="sxs-lookup"><span data-stu-id="210ff-122">Try making the search criteria for your query more restrictive.</span></span>

### <a name="whats-the-difference-between-deleting-a-resource-group-in-the-azure-portal-and-clicking-delete-on-a-preconfigured-solution-in-azureiotsuitecom"></a><span data-ttu-id="210ff-123">Wat is het verschil tussen het verwijderen van een resourcegroep in Azure Portal en op verwijderen te klikken in een vooraf geconfigureerde oplossing op azureiotsuite.com?</span><span class="sxs-lookup"><span data-stu-id="210ff-123">What's the difference between deleting a resource group in the Azure portal and clicking delete on a preconfigured solution in azureiotsuite.com?</span></span>

* <span data-ttu-id="210ff-124">Als u de vooraf geconfigureerde oplossing in verwijdert [azureiotsuite.com][lnk-azureiotsuite], verwijdert u alle resources die zijn ingericht toen u de vooraf geconfigureerde oplossing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="210ff-124">If you delete the preconfigured solution in [azureiotsuite.com][lnk-azureiotsuite], you delete all the resources that were provisioned when you created the preconfigured solution.</span></span> <span data-ttu-id="210ff-125">Als u aanvullende bronnen toegevoegd aan de resourcegroep, wordt deze resources worden ook verwijderd.</span><span class="sxs-lookup"><span data-stu-id="210ff-125">If you added additional resources to the resource group, these resources are also deleted.</span></span> 
* <span data-ttu-id="210ff-126">Als u de resourcegroep in verwijdert de [Azure-portal][lnk-azure-portal], verwijdert u alleen de resources in die resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="210ff-126">If you delete the resource group in the [Azure portal][lnk-azure-portal], you only delete the resources in that resource group.</span></span> <span data-ttu-id="210ff-127">U moet ook verwijderen van de Azure Active Directory-toepassing die is gekoppeld aan de vooraf geconfigureerde oplossing in de [klassieke Azure-portal][lnk-classic-portal].</span><span class="sxs-lookup"><span data-stu-id="210ff-127">You also need to delete the Azure Active Directory application associated with the preconfigured solution in the [Azure classic portal][lnk-classic-portal].</span></span>

### <a name="how-many-iot-hub-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="210ff-128">Hoeveel exemplaren van de IoT Hub kan ik inrichten in een abonnement?</span><span class="sxs-lookup"><span data-stu-id="210ff-128">How many IoT Hub instances can I provision in a subscription?</span></span>

<span data-ttu-id="210ff-129">Standaard kunt u inrichten [10 IoT hubs per abonnement][link-azuresublimits].</span><span class="sxs-lookup"><span data-stu-id="210ff-129">By default you can provision [10 IoT hubs per subscription][link-azuresublimits].</span></span> <span data-ttu-id="210ff-130">Kunt u een [Azure-ondersteuningsticket] [ link-azuresupportticket] deze limiet te verhogen.</span><span class="sxs-lookup"><span data-stu-id="210ff-130">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit.</span></span> <span data-ttu-id="210ff-131">Omdat elke vooraf geconfigureerde oplossing een nieuwe IoT Hub inricht, kunt u als gevolg hiervan alleen maximaal 10 vooraf geconfigureerde oplossingen in een bepaald abonnement inrichten.</span><span class="sxs-lookup"><span data-stu-id="210ff-131">As a result, since every preconfigured solution provisions a new IoT Hub, you can only provision up to 10 preconfigured solutions in a given subscription.</span></span> 

### <a name="how-many-azure-cosmos-db-instances-can-i-provision-in-a-subscription"></a><span data-ttu-id="210ff-132">Hoeveel exemplaren van Azure DB die Cosmos kan ik inrichten in een abonnement?</span><span class="sxs-lookup"><span data-stu-id="210ff-132">How many Azure Cosmos DB instances can I provision in a subscription?</span></span>

<span data-ttu-id="210ff-133">Vijftig.</span><span class="sxs-lookup"><span data-stu-id="210ff-133">Fifty.</span></span> <span data-ttu-id="210ff-134">Kunt u een [Azure-ondersteuningsticket] [ link-azuresupportticket] deze limiet te verhogen, maar standaard kunt u alleen 50 exemplaren van de Cosmos-database per abonnement inrichten.</span><span class="sxs-lookup"><span data-stu-id="210ff-134">You can create an [Azure support ticket][link-azuresupportticket] to raise this limit, but by default, you can only provision 50 Cosmos DB instances per subscription.</span></span> 

### <a name="how-many-free-bing-maps-apis-can-i-provision-in-a-subscription"></a><span data-ttu-id="210ff-135">Hoeveel gratis Bing Kaarten-API's kan ik inrichten met een abonnement?</span><span class="sxs-lookup"><span data-stu-id="210ff-135">How many Free Bing Maps APIs can I provision in a subscription?</span></span>

<span data-ttu-id="210ff-136">Twee.</span><span class="sxs-lookup"><span data-stu-id="210ff-136">Two.</span></span> <span data-ttu-id="210ff-137">U kunt slechts twee interne transacties niveau 1 Bing-kaarten voor Enterprise plannen in een Azure-abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="210ff-137">You can create only two Internal Transactions Level 1 Bing Maps for Enterprise plans in an Azure subscription.</span></span> <span data-ttu-id="210ff-138">De oplossing voor externe controle is standaard ingericht met het interne transacties niveau 1-plan.</span><span class="sxs-lookup"><span data-stu-id="210ff-138">The remote monitoring solution is provisioned by default with the Internal Transactions Level 1 plan.</span></span> <span data-ttu-id="210ff-139">Als gevolg hiervan kunt u met een abonnement waaraan geen wijzigingen zijn aangebracht maximaal twee externe bewakingsoplossingen inrichten.</span><span class="sxs-lookup"><span data-stu-id="210ff-139">As a result, you can only provision up to two remote monitoring solutions in a subscription with no modifications.</span></span>

### <a name="i-have-a-remote-monitoring-solution-deployment-with-a-static-map-how-do-i-add-an-interactive-bing-map"></a><span data-ttu-id="210ff-140">Ik heb een implementatie van een externe bewakingsoplossing met een statische kaart, hoe voeg ik een interactieve Bing-kaart toe?</span><span class="sxs-lookup"><span data-stu-id="210ff-140">I have a remote monitoring solution deployment with a static map, how do I add an interactive Bing map?</span></span>

1. <span data-ttu-id="210ff-141">Ophalen van uw Bing kaarten-API voor Enterprise-querysleutel in [Azure-portal][lnk-azure-portal]:</span><span class="sxs-lookup"><span data-stu-id="210ff-141">Get your Bing Maps API for Enterprise QueryKey from [Azure portal][lnk-azure-portal]:</span></span> 
   
   1. <span data-ttu-id="210ff-142">Navigeer naar de resourcegroep waar uw Bing kaarten-API voor Enterprise zich bevindt in de [Azure-portal][lnk-azure-portal].</span><span class="sxs-lookup"><span data-stu-id="210ff-142">Navigate to the Resource Group where your Bing Maps API for Enterprise is in the [Azure portal][lnk-azure-portal].</span></span>
   2. <span data-ttu-id="210ff-143">Klik op **alle instellingen**, klikt u vervolgens **Sleutelbeheer**.</span><span class="sxs-lookup"><span data-stu-id="210ff-143">Click **All Settings**, then **Key Management**.</span></span> 
   3. <span data-ttu-id="210ff-144">U ziet twee sleutels: **hoofdsleutel** en **querysleutel**.</span><span class="sxs-lookup"><span data-stu-id="210ff-144">You can see two keys: **MasterKey** and **QueryKey**.</span></span> <span data-ttu-id="210ff-145">Kopieer de waarde voor **querysleutel**.</span><span class="sxs-lookup"><span data-stu-id="210ff-145">Copy the value for **QueryKey**.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="210ff-146">U hebt geen Bing Kaarten-API voor Enterprise-account?</span><span class="sxs-lookup"><span data-stu-id="210ff-146">Don't have a Bing Maps API for Enterprise account?</span></span> <span data-ttu-id="210ff-147">Maken in de [Azure-portal] [ lnk-azure-portal] door te klikken op + Nieuw, zoeken naar Bing kaarten-API voor Enterprise en volg de aanwijzingen voor het maken.</span><span class="sxs-lookup"><span data-stu-id="210ff-147">Create one in the [Azure portal][lnk-azure-portal] by clicking + New, searching for Bing Maps API for Enterprise and follow prompts to create.</span></span>
      > 
      > 
2. <span data-ttu-id="210ff-148">Ophalen van de meest recente code van de [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span><span class="sxs-lookup"><span data-stu-id="210ff-148">Pull down the latest code from the [Azure-IoT-Remote-Monitoring][lnk-remote-monitoring-github].</span></span>
3. <span data-ttu-id="210ff-149">Uitvoeren van een lokale implementatie of een cloudimplementatie na het opdrachtregelprogramma implementatierichtlijnen in de map /docs/ in de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="210ff-149">Run a local or cloud deployment following the command-line deployment guidance in the /docs/ folder in the repository.</span></span> 
4. <span data-ttu-id="210ff-150">Nadat u een lokale implementatie of een cloudimplementatie hebt uitgevoerd, zoekt u in de hoofdmap naar het bestand *.user.config dat is gemaakt tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="210ff-150">After you've run a local or cloud deployment, look in your root folder for the *.user.config file created during deployment.</span></span> <span data-ttu-id="210ff-151">Open dit bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="210ff-151">Open this file in a text editor.</span></span> 
5. <span data-ttu-id="210ff-152">Wijzig de volgende regel zodat die de waarde die u hebt gekopieerd uit uw **querysleutel**:</span><span class="sxs-lookup"><span data-stu-id="210ff-152">Change the following line to include the value you copied from your **QueryKey**:</span></span> 
   
   `<setting name="MapApiQueryKey" value="" />`

### <a name="can-i-create-a-preconfigured-solution-if-i-have-microsoft-azure-for-dreamspark"></a><span data-ttu-id="210ff-153">Kan ik een vooraf geconfigureerde oplossing maken als ik Microsoft Azure voor DreamSpark heb?</span><span class="sxs-lookup"><span data-stu-id="210ff-153">Can I create a preconfigured solution if I have Microsoft Azure for DreamSpark?</span></span>

<span data-ttu-id="210ff-154">Op dit moment kunt u een vooraf geconfigureerde oplossing met geen maken een [Microsoft Azure voor DreamSpark] [ lnk-dreamspark] account.</span><span class="sxs-lookup"><span data-stu-id="210ff-154">Currently, you cannot create a preconfigured solution with a [Microsoft Azure for DreamSpark][lnk-dreamspark] account.</span></span> <span data-ttu-id="210ff-155">U kunt echter maken een [gratis proefaccount voor Azure] [ lnk-30daytrial] binnen een paar minuten waarmee u een vooraf geconfigureerde oplossing maken.</span><span class="sxs-lookup"><span data-stu-id="210ff-155">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="can-i-create-a-preconfigured-solution-if-i-have-cloud-solution-provider-csp-subscription"></a><span data-ttu-id="210ff-156">Kan ik een vooraf geconfigureerde oplossing maken als ik Cloud Solution Provider (CSP) abonnement?</span><span class="sxs-lookup"><span data-stu-id="210ff-156">Can I create a preconfigured solution if I have Cloud Solution Provider (CSP) subscription?</span></span>

<span data-ttu-id="210ff-157">U kunt op dit moment een vooraf geconfigureerde oplossing maken met een abonnement Cloud Solution Provider (CSP).</span><span class="sxs-lookup"><span data-stu-id="210ff-157">Currently, you cannot create a preconfigured solution with a Cloud Solution Provider (CSP) subscription.</span></span> <span data-ttu-id="210ff-158">U kunt echter maken een [gratis proefaccount voor Azure] [ lnk-30daytrial] binnen een paar minuten waarmee u een vooraf geconfigureerde oplossing maken.</span><span class="sxs-lookup"><span data-stu-id="210ff-158">However, you can create a [free trial account for Azure][lnk-30daytrial] in just a couple of minutes that enables you create a preconfigured solution.</span></span>

### <a name="how-do-i-delete-an-aad-tenant"></a><span data-ttu-id="210ff-159">Hoe verwijder ik een AAD-tenant?</span><span class="sxs-lookup"><span data-stu-id="210ff-159">How do I delete an AAD tenant?</span></span>

<span data-ttu-id="210ff-160">Zie het blogbericht van Eric Golpe van [overzicht van het verwijderen van een Azure AD-Tenant][lnk-delete-aad-tennant].</span><span class="sxs-lookup"><span data-stu-id="210ff-160">See Eric Golpe's blog post [Walkthrough of Deleting an Azure AD Tenant][lnk-delete-aad-tennant].</span></span>

### <a name="next-steps"></a><span data-ttu-id="210ff-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="210ff-161">Next steps</span></span>

<span data-ttu-id="210ff-162">U kunt ook enkele van de andere functies en mogelijkheden van de vooraf geconfigureerde IoT Suite-oplossingen verkennen:</span><span class="sxs-lookup"><span data-stu-id="210ff-162">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="210ff-163">[Overzicht van voorspeld onderhoud vooraf geconfigureerde oplossing][lnk-predictive-overview]</span><span class="sxs-lookup"><span data-stu-id="210ff-163">[Predictive maintenance preconfigured solution overview][lnk-predictive-overview]</span></span>
* [<span data-ttu-id="210ff-164">Overzicht van de verbonden factory vooraf geconfigureerde oplossing</span><span class="sxs-lookup"><span data-stu-id="210ff-164">Connected factory preconfigured solution overview</span></span>](iot-suite-connected-factory-overview.md)
* <span data-ttu-id="210ff-165">[Fundamentele IoT-beveiliging][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="210ff-165">[IoT security from the ground up][lnk-security-groundup]</span></span>

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

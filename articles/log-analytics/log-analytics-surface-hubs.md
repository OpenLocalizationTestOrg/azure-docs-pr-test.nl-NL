---
title: aaaMonitor Surface Hubs met Azure Log Analytics | Microsoft Docs
description: Gebruik Hallo Surface Hub-oplossing tootrack Hallo status van uw Surface Hubs en begrijpen hoe deze worden gebruikt.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 623d30e749cafdd4a34ba0c5b3408164f1b4a95b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-tootrack-their-health"></a><span data-ttu-id="c59e0-103">Surface Hubs met logboekanalyse tootrack hun status controleren</span><span class="sxs-lookup"><span data-stu-id="c59e0-103">Monitor Surface Hubs with Log Analytics tootrack their health</span></span>

![Surface Hub symbool](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="c59e0-105">Dit artikel wordt beschreven hoe u Hallo Surface Hub-oplossing in logboekanalyse toomonitor Microsoft Surface Hub-apparaten met Hallo Microsoft Operations Management Suite (OMS) kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c59e0-105">This article describes how you can use hello Surface Hub solution in Log Analytics toomonitor Microsoft Surface Hub devices with hello Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="c59e0-106">Meld u Analytics kunt die u goed begrijpen hoe deze worden gebruikt Hallo status van uw Surface Hubs bijhouden.</span><span class="sxs-lookup"><span data-stu-id="c59e0-106">Log Analytics helps you track hello health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="c59e0-107">Elke Surface Hub heeft Hallo die Microsoft Monitoring Agent geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="c59e0-107">Each Surface Hub has hello Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="c59e0-108">De via Hallo-agent die u kunt gegevens uit uw tooOMS Surface Hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="c59e0-108">Its through hello agent that you can send data from your Surface Hub tooOMS.</span></span> <span data-ttu-id="c59e0-109">Logboekbestanden worden gelezen uit uw Surface Hubs en worden vervolgens toohello OMS-service worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="c59e0-109">Log files are read from your Surface Hubs and are then are sent toohello OMS service.</span></span> <span data-ttu-id="c59e0-110">Problemen worden zoals servers offline, Hallo kalender niet synchroniseert, of als Hallo apparaat account kan niet toolog in Skype weergegeven in OMS in Hallo Surface Hub-dashboard.</span><span class="sxs-lookup"><span data-stu-id="c59e0-110">Issues like servers being offline, hello calendar not syncing, or if hello device account is unable toolog into Skype are shown in OMS in hello Surface Hub dashboard.</span></span> <span data-ttu-id="c59e0-111">Hallo-gegevens in Hallo dashboard gebruikt, kunt u apparaten die niet worden uitgevoerd, of die zijn andere problemen en oplossingen voor problemen gedetecteerd Hallo mogelijk van toepassing te identificeren.</span><span class="sxs-lookup"><span data-stu-id="c59e0-111">By using hello data in hello dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for hello detected issues.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="c59e0-112">Installeren en configureren van Hallo-oplossing</span><span class="sxs-lookup"><span data-stu-id="c59e0-112">Installing and configuring hello solution</span></span>
<span data-ttu-id="c59e0-113">Gebruik Hallo informatie tooinstall te volgen en Hallo oplossing configureren.</span><span class="sxs-lookup"><span data-stu-id="c59e0-113">Use hello following information tooinstall and configure hello solution.</span></span> <span data-ttu-id="c59e0-114">In de volgorde toomanage uw Surface Hubs van Hallo Microsoft Operations Management Suite (OMS), moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="c59e0-114">In order toomanage your Surface Hubs from hello Microsoft Operations Management Suite (OMS), you'll need hello following:</span></span>

* <span data-ttu-id="c59e0-115">Een geldig abonnement te[OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="c59e0-115">A valid subscription too[OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="c59e0-116">Een [OMS abonnement](https://azure.microsoft.com/pricing/details/log-analytics/) niveau die ondersteuning voor Hallo aantal bieden apparaten dat u wilt dat toomonitor.</span><span class="sxs-lookup"><span data-stu-id="c59e0-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support hello number of devices you want toomonitor.</span></span> <span data-ttu-id="c59e0-117">Prijzen van OMS varieert afhankelijk van hoeveel apparaten zijn ingeschreven en hoeveel gegevens deze processen.</span><span class="sxs-lookup"><span data-stu-id="c59e0-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="c59e0-118">Moet u tootake dit in aanmerking bij het plannen van uw implementatie Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c59e0-118">You'll want tootake this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="c59e0-119">Vervolgens wordt u een OMS-abonnement tooyour bestaande Microsoft Azure-abonnement toevoegen of maak een nieuwe werkruimte rechtstreeks via Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="c59e0-119">Next, you will either add an OMS subscription tooyour existing Microsoft Azure subscription or create a new workspace directly through hello OMS portal.</span></span> <span data-ttu-id="c59e0-120">Gedetailleerde instructies voor het gebruik van beide methoden is op [aan de slag met logboekanalyse](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c59e0-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="c59e0-121">Zodra Hallo OMS-abonnement is ingesteld, zijn er twee manieren tooenroll Surface Hub-apparaten:</span><span class="sxs-lookup"><span data-stu-id="c59e0-121">Once hello OMS subscription is set up, there are two ways tooenroll your Surface Hub devices:</span></span>

* <span data-ttu-id="c59e0-122">Automatisch via Intune</span><span class="sxs-lookup"><span data-stu-id="c59e0-122">Automatically through Intune</span></span>
* <span data-ttu-id="c59e0-123">Handmatig via **instellingen** op uw apparaat Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c59e0-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="c59e0-124">Controle instellen</span><span class="sxs-lookup"><span data-stu-id="c59e0-124">Set up monitoring</span></span>
<span data-ttu-id="c59e0-125">U kunt controleren Hallo status en activiteit van uw Surface Hub met logboekanalyse in OMS.</span><span class="sxs-lookup"><span data-stu-id="c59e0-125">You can monitor hello health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="c59e0-126">U kunt Hallo Surface Hub in OMS inschrijven met behulp van Intune of lokaal via **instellingen** op Hallo Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="c59e0-126">You can enroll hello Surface Hub in OMS by using Intune, or locally by using **Settings** on hello Surface Hub.</span></span>

## <a name="connect-surface-hubs-toooms-through-intune"></a><span data-ttu-id="c59e0-127">Verbinding maken met Surface Hubs tooOMS via Intune</span><span class="sxs-lookup"><span data-stu-id="c59e0-127">Connect Surface Hubs tooOMS through Intune</span></span>
<span data-ttu-id="c59e0-128">U moet Hallo werkruimte-ID en werkruimtesleutel voor Hallo OMS-werkruimte die uw Surface Hubs zullen beheren.</span><span class="sxs-lookup"><span data-stu-id="c59e0-128">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="c59e0-129">U kunt verkrijgen die uit Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="c59e0-129">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="c59e0-130">Intune is een Microsoft-product waarmee u toocentrally Hallo OMS configuratie-instellingen die zijn toegepast tooone of meer van uw apparaten beheren.</span><span class="sxs-lookup"><span data-stu-id="c59e0-130">Intune is a Microsoft product that allows you toocentrally manage hello OMS configuration settings that are applied tooone or more of your devices.</span></span> <span data-ttu-id="c59e0-131">Volg deze stappen tooconfigure uw apparaten via Intune:</span><span class="sxs-lookup"><span data-stu-id="c59e0-131">Follow these steps tooconfigure your devices through Intune:</span></span>

1. <span data-ttu-id="c59e0-132">Meld u aan tooIntune.</span><span class="sxs-lookup"><span data-stu-id="c59e0-132">Sign in tooIntune.</span></span>
2. <span data-ttu-id="c59e0-133">Navigeer te**instellingen** > **verbonden bronnen**.</span><span class="sxs-lookup"><span data-stu-id="c59e0-133">Navigate too**Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="c59e0-134">Maken of bewerken van een beleid op basis van Hallo Surface Hub-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="c59e0-134">Create or edit a policy based on hello Surface Hub template.</span></span>
4. <span data-ttu-id="c59e0-135">Navigeer toohello OMS (Azure Operational Insights)-sectie van het Hallo-beleid en voeg Hallo *werkruimte-ID* en *Werkruimtesleutel* toohello beleid.</span><span class="sxs-lookup"><span data-stu-id="c59e0-135">Navigate toohello OMS (Azure Operational Insights) section of hello policy, and add hello *Workspace ID* and *Workspace Key* toohello policy.</span></span>
5. <span data-ttu-id="c59e0-136">Hallo beleid opslaan.</span><span class="sxs-lookup"><span data-stu-id="c59e0-136">Save hello policy.</span></span>
6. <span data-ttu-id="c59e0-137">Hallo-beleid koppelen aan de juiste groep Hallo van apparaten.</span><span class="sxs-lookup"><span data-stu-id="c59e0-137">Associate hello policy with hello appropriate group of devices.</span></span>

   ![Intune-beleid](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="c59e0-139">Hallo OMS instellingen Intune vervolgens gesynchroniseerd met de Hallo-apparaten in de doelgroep hello, ze inschrijven in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="c59e0-139">Intune then syncs hello OMS settings with hello devices in hello target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-toooms-using-hello-settings-app"></a><span data-ttu-id="c59e0-140">Verbinding maken met behulp van de app instellingen Hallo Surface Hubs-tooOMS</span><span class="sxs-lookup"><span data-stu-id="c59e0-140">Connect Surface Hubs tooOMS using hello Settings app</span></span>
<span data-ttu-id="c59e0-141">U moet Hallo werkruimte-ID en werkruimtesleutel voor Hallo OMS-werkruimte die uw Surface Hubs zullen beheren.</span><span class="sxs-lookup"><span data-stu-id="c59e0-141">You'll need hello workspace ID and workspace key for hello OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="c59e0-142">U kunt verkrijgen die uit Hallo OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="c59e0-142">You can get those from hello OMS portal.</span></span>

<span data-ttu-id="c59e0-143">Als u geen Intune toomanage uw omgeving gebruikt, kunt u handmatig via apparaten inschrijven **instellingen** op elke Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="c59e0-143">If you don't use Intune toomanage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="c59e0-144">Open in uw Surface Hub **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="c59e0-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="c59e0-145">Voer Hallo apparaat beheerdersreferenties wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="c59e0-145">Enter hello device admin credentials when prompted.</span></span>
3. <span data-ttu-id="c59e0-146">Klik op **dit apparaat**, en Hallo onder **bewaking**, klikt u op **OMS-instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="c59e0-146">Click **This device**, and hello under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="c59e0-147">Selecteer **bewaking inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="c59e0-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="c59e0-148">Typ in Hallo OMS instellingen dialoogvenster Hallo **werkruimte-ID** en type Hallo **Werkruimtesleutel**.</span><span class="sxs-lookup"><span data-stu-id="c59e0-148">In hello OMS settings dialog, type hello **Workspace ID** and type hello **Workspace Key**.</span></span>  
   <span data-ttu-id="c59e0-149">![Instellingen](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="c59e0-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="c59e0-150">Klik op **OK** toocomplete Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="c59e0-150">Click **OK** toocomplete hello configuration.</span></span>

<span data-ttu-id="c59e0-151">Een bevestiging wordt weergegeven dat u al dan niet Hallo OMS configuratie correct is toegepast toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="c59e0-151">A confirmation appears telling you whether or not hello OMS configuration was successfully applied toohello device.</span></span> <span data-ttu-id="c59e0-152">Als dit het geval is, wordt er een bericht weergegeven dat die agent Hallo toohello OMS-service is verbonden.</span><span class="sxs-lookup"><span data-stu-id="c59e0-152">If it was, a message appears stating that hello agent successfully connected toohello OMS service.</span></span> <span data-ttu-id="c59e0-153">Hallo apparaat vervolgens wordt gestart voor het verzenden van gegevens tooOMS waar u kunt weergeven en erop reageren.</span><span class="sxs-lookup"><span data-stu-id="c59e0-153">hello device then starts sending data tooOMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="c59e0-154">Monitor met Surface Hubs</span><span class="sxs-lookup"><span data-stu-id="c59e0-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="c59e0-155">Bewaking van uw Surface Hubs lijkt met behulp van OMS veel bewaking van andere geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="c59e0-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="c59e0-156">Meld u aan toohello OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="c59e0-156">Sign in toohello OMS portal.</span></span>
2. <span data-ttu-id="c59e0-157">Navigeer dashboard pack toohello Surface Hub-oplossing.</span><span class="sxs-lookup"><span data-stu-id="c59e0-157">Navigate toohello Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="c59e0-158">Status van uw apparaat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c59e0-158">Your device's health is displayed.</span></span>

   ![Surface Hub-dashboard](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="c59e0-160">U kunt maken [waarschuwingen](log-analytics-alerts.md) op basis van bestaande of aangepaste logboek zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="c59e0-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="c59e0-161">Hallo gegevens Hallo die OMS van uw Surface Hubs verzamelt gebruikt, kunt u zoeken naar problemen en de waarschuwing op Hallo voorwaarden die u voor uw apparaten definieert.</span><span class="sxs-lookup"><span data-stu-id="c59e0-161">Using hello data hello OMS collects from your Surface Hubs, you can search for issues and alert on hello conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c59e0-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c59e0-162">Next steps</span></span>
* <span data-ttu-id="c59e0-163">Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) tooview gedetailleerde Surface Hub-gegevens.</span><span class="sxs-lookup"><span data-stu-id="c59e0-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Surface Hub data.</span></span>
* <span data-ttu-id="c59e0-164">Maak [waarschuwingen](log-analytics-alerts.md) toonotify u wanneer er problemen optreden met uw Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="c59e0-164">Create [alerts](log-analytics-alerts.md) toonotify you when issues occur with your Surface Hubs.</span></span>

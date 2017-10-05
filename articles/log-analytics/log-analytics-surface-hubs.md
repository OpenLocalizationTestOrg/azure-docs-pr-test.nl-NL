---
title: Bewaken met Surface Hubs met Azure Log Analytics | Microsoft Docs
description: Gebruik de Surface Hub-oplossing de status van uw Surface Hubs bijhouden en begrijpen hoe deze worden gebruikt.
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
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="ceb37-103">Surface Hubs met logboekanalyse voor het bijhouden van hun status controleren</span><span class="sxs-lookup"><span data-stu-id="ceb37-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Surface Hub symbool](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="ceb37-105">Dit artikel wordt beschreven hoe u kunt de Surface Hub-oplossing in logboekanalyse voor het bewaken van de Microsoft Surface Hub-apparaten met de Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="ceb37-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="ceb37-106">Log Analytics kunt u de status van uw Surface Hubs goed begrijpen hoe deze worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ceb37-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="ceb37-107">Elke Surface Hub heeft Microsoft Monitoring Agent geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ceb37-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="ceb37-108">De via de agent die u gegevens kunt verzenden vanuit uw Surface Hub met OMS.</span><span class="sxs-lookup"><span data-stu-id="ceb37-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="ceb37-109">Logboekbestanden worden gelezen uit uw Surface Hubs en worden vervolgens naar de OMS-service worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ceb37-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="ceb37-110">Factoren, zoals servers offline is, de kalender niet synchroniseert, of als het account zich niet aanmelden bij Skype in OMS worden weergegeven in het dashboard Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="ceb37-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="ceb37-111">Met behulp van de gegevens in het dashboard, kunt u apparaten die niet worden uitgevoerd, of die zijn andere problemen en oplossingen voor de gedetecteerde problemen mogelijk van toepassing te identificeren.</span><span class="sxs-lookup"><span data-stu-id="ceb37-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="ceb37-112">Installeren en configureren van de oplossing</span><span class="sxs-lookup"><span data-stu-id="ceb37-112">Installing and configuring the solution</span></span>
<span data-ttu-id="ceb37-113">Gebruik de volgende informatie om te installeren en configureren van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="ceb37-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="ceb37-114">Om uw Surface Hubs van de Microsoft Operations Management Suite (OMS) beheren, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="ceb37-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="ceb37-115">Een geldig abonnement op [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="ceb37-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="ceb37-116">Een [OMS abonnement](https://azure.microsoft.com/pricing/details/log-analytics/) niveau die ondersteuning bieden voor het aantal apparaten dat u wilt bewaken.</span><span class="sxs-lookup"><span data-stu-id="ceb37-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="ceb37-117">Prijzen van OMS varieert afhankelijk van hoeveel apparaten zijn ingeschreven en hoeveel gegevens deze processen.</span><span class="sxs-lookup"><span data-stu-id="ceb37-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="ceb37-118">Moet u dit in aanmerking te nemen bij het plannen van uw implementatie Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="ceb37-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="ceb37-119">Vervolgens wordt u een OMS-abonnement toevoegen aan uw bestaande Microsoft Azure-abonnement of maak een nieuwe werkruimte rechtstreeks via de OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="ceb37-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="ceb37-120">Gedetailleerde instructies voor het gebruik van beide methoden is op [aan de slag met logboekanalyse](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ceb37-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="ceb37-121">Zodra de OMS-abonnement is ingesteld, zijn er twee manieren om uw Surface Hub-apparaten te registreren:</span><span class="sxs-lookup"><span data-stu-id="ceb37-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="ceb37-122">Automatisch via Intune</span><span class="sxs-lookup"><span data-stu-id="ceb37-122">Automatically through Intune</span></span>
* <span data-ttu-id="ceb37-123">Handmatig via **instellingen** op uw apparaat Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="ceb37-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="ceb37-124">Controle instellen</span><span class="sxs-lookup"><span data-stu-id="ceb37-124">Set up monitoring</span></span>
<span data-ttu-id="ceb37-125">U kunt de status en activiteit van uw Surface Hub met logboekanalyse in OMS controleren.</span><span class="sxs-lookup"><span data-stu-id="ceb37-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="ceb37-126">U kunt de Surface Hub in OMS inschrijven met behulp van Intune of lokaal via **instellingen** op de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="ceb37-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="ceb37-127">Verbinding maken met Surface Hubs met OMS via Intune</span><span class="sxs-lookup"><span data-stu-id="ceb37-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="ceb37-128">Moet u de werkruimte-ID en werkruimtesleutel voor de OMS-werkruimte die uw Surface Hubs zullen beheren.</span><span class="sxs-lookup"><span data-stu-id="ceb37-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="ceb37-129">U kunt ophalen uit de OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="ceb37-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="ceb37-130">Intune is een Microsoft-product waarmee u de OMS-configuratie-instellingen die worden toegepast op een of meer van uw apparaten centraal te beheren.</span><span class="sxs-lookup"><span data-stu-id="ceb37-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="ceb37-131">Volg deze stappen voor het configureren van uw apparaten via Intune:</span><span class="sxs-lookup"><span data-stu-id="ceb37-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="ceb37-132">Aanmelden bij Intune.</span><span class="sxs-lookup"><span data-stu-id="ceb37-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="ceb37-133">Navigeer naar **instellingen** > **verbonden gegevensbronnen**.</span><span class="sxs-lookup"><span data-stu-id="ceb37-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="ceb37-134">Maken of bewerken van een beleid op basis van de sjabloon die Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="ceb37-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="ceb37-135">Navigeer naar de sectie OMS (Azure Operational Insights) van het beleid en voeg de *werkruimte-ID* en *Werkruimtesleutel* aan het beleid.</span><span class="sxs-lookup"><span data-stu-id="ceb37-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="ceb37-136">Sla het beleid.</span><span class="sxs-lookup"><span data-stu-id="ceb37-136">Save the policy.</span></span>
6. <span data-ttu-id="ceb37-137">Koppelt het beleid met de juiste groep apparaten.</span><span class="sxs-lookup"><span data-stu-id="ceb37-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Intune-beleid](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="ceb37-139">De OMS-instellingen Intune vervolgens gesynchroniseerd met de apparaten in de doelgroep ze inschrijven in de OMS-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="ceb37-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="ceb37-140">Verbinding maken met Surface Hubs met behulp van de app instellingen OMS</span><span class="sxs-lookup"><span data-stu-id="ceb37-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="ceb37-141">Moet u de werkruimte-ID en werkruimtesleutel voor de OMS-werkruimte die uw Surface Hubs zullen beheren.</span><span class="sxs-lookup"><span data-stu-id="ceb37-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="ceb37-142">U kunt ophalen uit de OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="ceb37-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="ceb37-143">Als u Intune niet gebruikt om uw omgeving te beheren, kunt u handmatig via apparaten inschrijven **instellingen** op elke Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="ceb37-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="ceb37-144">Open in uw Surface Hub **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ceb37-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="ceb37-145">Voer de beheerdersreferenties apparaat wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="ceb37-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="ceb37-146">Klik op **dit apparaat**, en de onder **bewaking**, klikt u op **OMS-instellingen configureren**.</span><span class="sxs-lookup"><span data-stu-id="ceb37-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="ceb37-147">Selecteer **bewaking inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="ceb37-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="ceb37-148">Typ in het dialoogvenster OMS-instellingen voor de **werkruimte-ID** en typt u de **Werkruimtesleutel**.</span><span class="sxs-lookup"><span data-stu-id="ceb37-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="ceb37-149">![Instellingen](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="ceb37-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="ceb37-150">Klik op **OK** om de configuratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ceb37-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="ceb37-151">Een bevestiging wordt weergegeven dat u al dan niet de OMS-configuratie is toegepast op het apparaat.</span><span class="sxs-lookup"><span data-stu-id="ceb37-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="ceb37-152">Als dit het geval is, wordt er een bericht weergegeven dat de agent is verbonden met de OMS-service.</span><span class="sxs-lookup"><span data-stu-id="ceb37-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="ceb37-153">Het apparaat wordt vervolgens gestart voor het verzenden van gegevens naar OMS waar u kunt weergeven en erop reageren.</span><span class="sxs-lookup"><span data-stu-id="ceb37-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="ceb37-154">Monitor met Surface Hubs</span><span class="sxs-lookup"><span data-stu-id="ceb37-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="ceb37-155">Bewaking van uw Surface Hubs lijkt met behulp van OMS veel bewaking van andere geregistreerde apparaten.</span><span class="sxs-lookup"><span data-stu-id="ceb37-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="ceb37-156">Aanmelden bij de OMS-portal.</span><span class="sxs-lookup"><span data-stu-id="ceb37-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="ceb37-157">Ga naar het dashboard Surface Hub-oplossing pack.</span><span class="sxs-lookup"><span data-stu-id="ceb37-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="ceb37-158">Status van uw apparaat wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ceb37-158">Your device's health is displayed.</span></span>

   ![Surface Hub-dashboard](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="ceb37-160">U kunt maken [waarschuwingen](log-analytics-alerts.md) op basis van bestaande of aangepaste logboek zoekopdrachten.</span><span class="sxs-lookup"><span data-stu-id="ceb37-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="ceb37-161">De OMS uit uw Surface Hubs verzamelt gegevens gebruikt, kunt u zoeken naar problemen en een waarschuwing voor de voorwaarden die u voor uw apparaten definieert.</span><span class="sxs-lookup"><span data-stu-id="ceb37-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ceb37-162">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ceb37-162">Next steps</span></span>
* <span data-ttu-id="ceb37-163">Gebruik [zoekopdrachten aanmelden met logboekanalyse](log-analytics-log-searches.md) om gedetailleerde Surface Hub-gegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="ceb37-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="ceb37-164">Maak [waarschuwingen](log-analytics-alerts.md) om u te waarschuwen wanneer er problemen optreden met uw Surface Hubs.</span><span class="sxs-lookup"><span data-stu-id="ceb37-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>

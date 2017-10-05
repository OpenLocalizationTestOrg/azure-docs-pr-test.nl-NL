---
title: Het configureren van een cloudservice (portal) | Microsoft Docs
description: Informatie over het configureren van cloud-services in Azure. Informatie over het bijwerken van de configuratie van de cloud-service en het configureren van externe toegang tot de rolinstanties. Deze voorbeelden worden de Azure portal gebruiken.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 7308f3c0-825e-499d-bfa5-c60f86371921
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2016
ms.author: adegeo
ms.openlocfilehash: a7e891d05ffe4cc2b4f68dce072a81499cc6de80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-configure-cloud-services"></a><span data-ttu-id="94a04-105">Het configureren van Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="94a04-105">How to Configure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94a04-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94a04-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="94a04-107">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94a04-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="94a04-108">U kunt de meest gebruikte instellingen voor een cloudservice in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="94a04-108">You can configure the most commonly used settings for a cloud service in the Azure portal.</span></span> <span data-ttu-id="94a04-109">Het is ook mogelijk uw configuratiebestand rechtstreeks bij te werken. Download in dat geval een serviceconfiguratiebestand om bij te werken, upload vervolgens het bijgewerkte bestand en werk de cloudservice bij met de configuratiewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="94a04-109">Or, if you like to update your configuration files directly, download a service configuration file to update, and then upload the updated file and update the cloud service with the configuration changes.</span></span> <span data-ttu-id="94a04-110">Welke methode u ook gebruikt, de configuratie-updates worden doorgegeven aan alle rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="94a04-110">Either way, the configuration updates are pushed out to all role instances.</span></span>

<span data-ttu-id="94a04-111">U kunt ook de exemplaren van uw cloud service-rollen of extern bureaublad in ze beheren.</span><span class="sxs-lookup"><span data-stu-id="94a04-111">You can also manage the instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="94a04-112">Azure zorgt alleen servicebeschikbaarheid 99,95% tijdens de configuratie-updates hebt u ten minste twee rolexemplaren voor elke rol.</span><span class="sxs-lookup"><span data-stu-id="94a04-112">Azure can only ensure 99.95 percent service availability during the configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="94a04-113">Waarmee één virtuele machine voor het verwerken van aanvragen van clients, terwijl de andere wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="94a04-113">That enables one virtual machine to process client requests while the other is being updated.</span></span> <span data-ttu-id="94a04-114">Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="94a04-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="94a04-115">Een cloudservice wijzigen</span><span class="sxs-lookup"><span data-stu-id="94a04-115">Change a cloud service</span></span>
<span data-ttu-id="94a04-116">Na opening de [Azure-portal](https://portal.azure.com/), gaat u naar de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="94a04-116">After opening the [Azure portal](https://portal.azure.com/), navigate to your cloud service.</span></span> <span data-ttu-id="94a04-117">Hier kunt beheren u veel aspecten van deze.</span><span class="sxs-lookup"><span data-stu-id="94a04-117">From here, you manage many aspects of it.</span></span>

![Pagina met instellingen](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="94a04-119">De **instellingen** of **alle instellingen** koppelingen geopend de **instellingen** blade waar kunt u de **eigenschappen**, de wijzigen **Configuratie**, beheren de **certificaten**, setup **waarschuwing regels**, en beheren van de **gebruikers** die toegang hebben tot deze cloudservice.</span><span class="sxs-lookup"><span data-stu-id="94a04-119">The **Settings** or **All settings** links will open up the **Settings** blade where you can change the **Properties**, change the **Configuration**, manage the **Certificates**, setup **Alert rules**, and manage the **Users** who have access to this cloud service.</span></span>

![Blade van Azure cloud service-instellingen](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="94a04-121">Gast OS-versie beheren</span><span class="sxs-lookup"><span data-stu-id="94a04-121">Manage Guest OS version</span></span>

<span data-ttu-id="94a04-122">Standaard werkt Azure periodiek het gastbesturingssysteem op de meest recente ondersteunde installatiekopie binnen de OS-familie die u hebt opgegeven in de serviceconfiguratie (.cscfg), zoals Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="94a04-122">By default, Azure periodically updates your guest OS to the latest supported image within the OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="94a04-123">Als u een specifieke versie van het besturingssysteem als doel moet, kunt u dit instellen de **configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="94a04-123">If you need to target a specific OS version, you can set it in the **Configuration** blade.</span></span>

![Versie van het besturingssysteem instellen](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="94a04-125">U kiest dat een specifieke versie van het besturingssysteem schakelt automatische OS bijgewerkt waardoor het uw verantwoordelijkheid patchen.</span><span class="sxs-lookup"><span data-stu-id="94a04-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="94a04-126">U moet ervoor zorgen dat uw rolinstanties zijn ontvangen van updates of u uw toepassing beveiligingsproblemen kan blootstellen.</span><span class="sxs-lookup"><span data-stu-id="94a04-126">You must ensure that your role instances are receiving updates or you may expose your application to security vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="94a04-127">Bewaking</span><span class="sxs-lookup"><span data-stu-id="94a04-127">Monitoring</span></span>
<span data-ttu-id="94a04-128">U kunt waarschuwingen toevoegen aan uw service in de cloud.</span><span class="sxs-lookup"><span data-stu-id="94a04-128">You can add alerts to your cloud service.</span></span> <span data-ttu-id="94a04-129">Klik op **instellingen** > **waarschuwing regels** > **waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="94a04-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="94a04-130">Hier kunt kunt u een waarschuwing instellen.</span><span class="sxs-lookup"><span data-stu-id="94a04-130">From here, you can setup an alert.</span></span> <span data-ttu-id="94a04-131">Met de **metriek** vervolgkeuzelijst, kunt u een waarschuwing voor de volgende soorten gegevens instellen.</span><span class="sxs-lookup"><span data-stu-id="94a04-131">With the **Metric** drop down box, you can setup an alert for the following types of data.</span></span>

* <span data-ttu-id="94a04-132">Schijf lezen</span><span class="sxs-lookup"><span data-stu-id="94a04-132">Disk read</span></span>
* <span data-ttu-id="94a04-133">Schijf schrijven</span><span class="sxs-lookup"><span data-stu-id="94a04-133">Disk write</span></span>
* <span data-ttu-id="94a04-134">Het netwerk</span><span class="sxs-lookup"><span data-stu-id="94a04-134">Network in</span></span>
* <span data-ttu-id="94a04-135">Uit het netwerk</span><span class="sxs-lookup"><span data-stu-id="94a04-135">Network out</span></span>
* <span data-ttu-id="94a04-136">CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="94a04-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="94a04-137">Bewaking van een metrische tegel configureren</span><span class="sxs-lookup"><span data-stu-id="94a04-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="94a04-138">In plaats van **instellingen** > **waarschuwingsregels**, kunt u klikken op een van de metrische tegels in de **bewaking** sectie van de **Cloudservice**  blade.</span><span class="sxs-lookup"><span data-stu-id="94a04-138">Instead of using **Settings** > **Alert Rules**, you can click on one of the metric tiles in the **Monitoring** section of the **Cloud service** blade.</span></span>

![Cloudservice controleren](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="94a04-140">Hier kunt u de grafiek gebruikt met de tegel aanpassen of een waarschuwingsregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="94a04-140">From here you can customize the chart used with the tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="94a04-141">Opnieuw opstarten of terugzetten van de installatiekopie extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="94a04-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="94a04-142">Op dit moment kunt u geen configureren extern bureaublad met behulp van de **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="94a04-142">At this time you cannot configure remote desktop using the **Azure portal**.</span></span> <span data-ttu-id="94a04-143">Echter, u kunt instellen het via de [klassieke Azure-portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), of via [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="94a04-143">However, you can set it up through the [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="94a04-144">Klik eerst op de cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="94a04-144">First, click on the cloud service instance.</span></span>

![Cloud Service-exemplaar](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="94a04-146">Op de blade dat wordt geopend initiëren van een verbinding met extern bureaublad, op afstand opnieuw opstarten van het exemplaar of op afstand installatiekopie (met een nieuwe installatiekopie) het exemplaar beginnen.</span><span class="sxs-lookup"><span data-stu-id="94a04-146">From the blade that opens you can initiate a remote desktop connection, remotely reboot the instance, or remotely reimage (start with a fresh image) the instance.</span></span>

![Cloud Service-exemplaar knoppen](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="94a04-148">Uw cscfg-bestand configureren</span><span class="sxs-lookup"><span data-stu-id="94a04-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="94a04-149">U moet wellicht opnieuw configureren van uw cloudservice via de [(cscfg) van de serviceconfiguratie](cloud-services-model-and-package.md#cscfg) bestand.</span><span class="sxs-lookup"><span data-stu-id="94a04-149">You may need to reconfigure your cloud service through the [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="94a04-150">U moet eerst uw cscfg-bestand downloaden, wijzigen en vervolgens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="94a04-150">First you need to download your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="94a04-151">Klik op de **instellingen** pictogram of de **alle instellingen** koppeling te openen van de **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="94a04-151">Click on the **Settings** icon or the **All settings** link to open up the **Settings** blade.</span></span>

    ![Pagina met instellingen](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="94a04-153">Klik op de **configuratie** item.</span><span class="sxs-lookup"><span data-stu-id="94a04-153">Click on the **Configuration** item.</span></span>

    ![Configuratie-Blade](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="94a04-155">Klik op de **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="94a04-155">Click on the **Download** button.</span></span>

    ![Downloaden](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="94a04-157">Na het bijwerken van het configuratiebestand van de service, uploaden en updates voor de configuratie van toepassing:</span><span class="sxs-lookup"><span data-stu-id="94a04-157">After you update the service configuration file, upload and apply the configuration updates:</span></span>

    ![Uploaden](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="94a04-159">Selecteer het cscfg-bestand en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="94a04-159">Select the .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94a04-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94a04-160">Next steps</span></span>
* <span data-ttu-id="94a04-161">Meer informatie over hoe [implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94a04-161">Learn how to [deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="94a04-162">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94a04-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="94a04-163">[Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94a04-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="94a04-164">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94a04-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

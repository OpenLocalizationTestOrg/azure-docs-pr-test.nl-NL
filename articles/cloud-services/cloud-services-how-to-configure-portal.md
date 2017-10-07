---
title: aaaHow tooconfigure een cloudservice (portal) | Microsoft Docs
description: Meer informatie over hoe tooconfigure cloud-services in Azure. Informatie over tooupdate Hallo cloud-serviceconfiguratie en toorole exemplaren van externe toegang configureren. Deze voorbeelden hello Azure-portal gebruiken.
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
ms.openlocfilehash: 969a08558473e8c79153192942bfda587eb5ada5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a><span data-ttu-id="94981-105">Hoe tooConfigure Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="94981-105">How tooConfigure Cloud Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="94981-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94981-106">Azure portal</span></span>](cloud-services-how-to-configure-portal.md)
> * [<span data-ttu-id="94981-107">Klassieke Azure Portal</span><span class="sxs-lookup"><span data-stu-id="94981-107">Azure classic portal</span></span>](cloud-services-how-to-configure.md)
>
>

<span data-ttu-id="94981-108">U kunt de meest gebruikte Hallo-instellingen voor een cloudservice configureren in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="94981-108">You can configure hello most commonly used settings for a cloud service in hello Azure portal.</span></span> <span data-ttu-id="94981-109">Of als u tooupdate dat de configuratiebestanden rechtstreeks downloaden van een service configuration file tooupdate en vervolgens uploaden Hallo bijgewerkt bestands- en update Hallo cloudservice Hallo configuratiewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="94981-109">Or, if you like tooupdate your configuration files directly, download a service configuration file tooupdate, and then upload hello updated file and update hello cloud service with hello configuration changes.</span></span> <span data-ttu-id="94981-110">In beide gevallen worden Hallo configuratie-updates gepusht tooall rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="94981-110">Either way, hello configuration updates are pushed out tooall role instances.</span></span>

<span data-ttu-id="94981-111">U kunt ook Hallo exemplaren van uw cloud service-rollen of extern bureaublad in ze beheren.</span><span class="sxs-lookup"><span data-stu-id="94981-111">You can also manage hello instances of your cloud service roles, or remote desktop into them.</span></span>

<span data-ttu-id="94981-112">Azure alleen zorgt 99,95% servicebeschikbaarheid tijdens Hallo configuratie-updates hebt u ten minste twee rolexemplaren voor elke rol.</span><span class="sxs-lookup"><span data-stu-id="94981-112">Azure can only ensure 99.95 percent service availability during hello configuration updates if you have at least two role instances for every role.</span></span> <span data-ttu-id="94981-113">Waarmee een virtuele machine tooprocess clientaanvragen terwijl andere hello wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="94981-113">That enables one virtual machine tooprocess client requests while hello other is being updated.</span></span> <span data-ttu-id="94981-114">Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span><span class="sxs-lookup"><span data-stu-id="94981-114">For more information, see [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).</span></span>

## <a name="change-a-cloud-service"></a><span data-ttu-id="94981-115">Een cloudservice wijzigen</span><span class="sxs-lookup"><span data-stu-id="94981-115">Change a cloud service</span></span>
<span data-ttu-id="94981-116">Na opening Hallo [Azure-portal](https://portal.azure.com/), navigeer tooyour-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="94981-116">After opening hello [Azure portal](https://portal.azure.com/), navigate tooyour cloud service.</span></span> <span data-ttu-id="94981-117">Hier kunt beheren u veel aspecten van deze.</span><span class="sxs-lookup"><span data-stu-id="94981-117">From here, you manage many aspects of it.</span></span>

![Pagina met instellingen](./media/cloud-services-how-to-configure-portal/cloud-service.png)

<span data-ttu-id="94981-119">Hallo **instellingen** of **alle instellingen** koppelingen geopend Hallo **instellingen** blade Hallo wijzigen **eigenschappen**, Hallo wijzigen **Configuratie**, Hallo beheren **certificaten**, setup **waarschuwing regels**, en beheren van Hallo **gebruikers** die toegang hebben toothis cloudservice.</span><span class="sxs-lookup"><span data-stu-id="94981-119">hello **Settings** or **All settings** links will open up hello **Settings** blade where you can change hello **Properties**, change hello **Configuration**, manage hello **Certificates**, setup **Alert rules**, and manage hello **Users** who have access toothis cloud service.</span></span>

![Blade van Azure cloud service-instellingen](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a><span data-ttu-id="94981-121">Gast OS-versie beheren</span><span class="sxs-lookup"><span data-stu-id="94981-121">Manage Guest OS version</span></span>

<span data-ttu-id="94981-122">Standaard werkt Azure periodiek de Gast toohello laatste ondersteunde installatiekopie van het besturingssysteem binnen Hallo OS-familie die u hebt opgegeven in de serviceconfiguratie (.cscfg), zoals Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="94981-122">By default, Azure periodically updates your guest OS toohello latest supported image within hello OS family that you've specified in your service configuration (.cscfg), such as Windows Server 2016.</span></span>

<span data-ttu-id="94981-123">Als u een specifieke versie van het besturingssysteem tootarget moet, kunt u dit instellen in Hallo **configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="94981-123">If you need tootarget a specific OS version, you can set it in hello **Configuration** blade.</span></span>

![Versie van het besturingssysteem instellen](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> <span data-ttu-id="94981-125">U kiest dat een specifieke versie van het besturingssysteem schakelt automatische OS bijgewerkt waardoor het uw verantwoordelijkheid patchen.</span><span class="sxs-lookup"><span data-stu-id="94981-125">Choosing a specific OS version disables automatic OS updates and makes patching your responsibility.</span></span> <span data-ttu-id="94981-126">U moet ervoor zorgen dat uw rolinstanties zijn ontvangen van updates of u uw toepassing toosecurity beveiligingsproblemen kan blootstellen.</span><span class="sxs-lookup"><span data-stu-id="94981-126">You must ensure that your role instances are receiving updates or you may expose your application toosecurity vulnerabilities.</span></span>

## <a name="monitoring"></a><span data-ttu-id="94981-127">Bewaking</span><span class="sxs-lookup"><span data-stu-id="94981-127">Monitoring</span></span>
<span data-ttu-id="94981-128">U kunt waarschuwingen tooyour cloudservice toevoegen.</span><span class="sxs-lookup"><span data-stu-id="94981-128">You can add alerts tooyour cloud service.</span></span> <span data-ttu-id="94981-129">Klik op **instellingen** > **waarschuwing regels** > **waarschuwing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="94981-129">Click **Settings** > **Alert Rules** > **Add alert**.</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

<span data-ttu-id="94981-130">Hier kunt kunt u een waarschuwing instellen.</span><span class="sxs-lookup"><span data-stu-id="94981-130">From here, you can setup an alert.</span></span> <span data-ttu-id="94981-131">Hello **metriek** vervolgkeuzelijst, kunt u een waarschuwing voor de volgende soorten gegevens Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="94981-131">With hello **Metric** drop down box, you can setup an alert for hello following types of data.</span></span>

* <span data-ttu-id="94981-132">Schijf lezen</span><span class="sxs-lookup"><span data-stu-id="94981-132">Disk read</span></span>
* <span data-ttu-id="94981-133">Schijf schrijven</span><span class="sxs-lookup"><span data-stu-id="94981-133">Disk write</span></span>
* <span data-ttu-id="94981-134">Het netwerk</span><span class="sxs-lookup"><span data-stu-id="94981-134">Network in</span></span>
* <span data-ttu-id="94981-135">Uit het netwerk</span><span class="sxs-lookup"><span data-stu-id="94981-135">Network out</span></span>
* <span data-ttu-id="94981-136">CPU-percentage</span><span class="sxs-lookup"><span data-stu-id="94981-136">CPU percentage</span></span>

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a><span data-ttu-id="94981-137">Bewaking van een metrische tegel configureren</span><span class="sxs-lookup"><span data-stu-id="94981-137">Configure monitoring from a metric tile</span></span>
<span data-ttu-id="94981-138">In plaats van **instellingen** > **waarschuwingsregels**, kunt u klikken op een van de metrische tegels in Hallo Hallo **bewaking** sectie Hallo **Cloud service** blade.</span><span class="sxs-lookup"><span data-stu-id="94981-138">Instead of using **Settings** > **Alert Rules**, you can click on one of hello metric tiles in hello **Monitoring** section of hello **Cloud service** blade.</span></span>

![Cloudservice controleren](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

<span data-ttu-id="94981-140">U kunt hiervandaan Hallo grafiek gebruikt met Hallo tegel aanpassen of een waarschuwingsregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="94981-140">From here you can customize hello chart used with hello tile, or add an alert rule.</span></span>

## <a name="reboot-reimage-or-remote-desktop"></a><span data-ttu-id="94981-141">Opnieuw opstarten of terugzetten van de installatiekopie extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="94981-141">Reboot, reimage, or remote desktop</span></span>
<span data-ttu-id="94981-142">Op dit moment kunt u geen extern bureaublad met Hallo configureren **Azure-portal**.</span><span class="sxs-lookup"><span data-stu-id="94981-142">At this time you cannot configure remote desktop using hello **Azure portal**.</span></span> <span data-ttu-id="94981-143">Echter, u kunt instellen deze via Hallo [klassieke Azure-portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), of via [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="94981-143">However, you can set it up through hello [Azure classic portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), or through [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).</span></span>

<span data-ttu-id="94981-144">Klik eerst op Hallo cloud service-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="94981-144">First, click on hello cloud service instance.</span></span>

![Cloud Service-exemplaar](./media/cloud-services-how-to-configure-portal/cs-instance.png)

<span data-ttu-id="94981-146">Van Hallo-blade waarmee de opent u een verbinding met extern bureaublad te initiëren, op afstand opnieuw opstarten hello, of een exemplaar op afstand terugzetten van de installatiekopie (start met een nieuwe installatiekopie) Hallo.</span><span class="sxs-lookup"><span data-stu-id="94981-146">From hello blade that opens you can initiate a remote desktop connection, remotely reboot hello instance, or remotely reimage (start with a fresh image) hello instance.</span></span>

![Cloud Service-exemplaar knoppen](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a><span data-ttu-id="94981-148">Uw cscfg-bestand configureren</span><span class="sxs-lookup"><span data-stu-id="94981-148">Reconfigure your .cscfg</span></span>
<span data-ttu-id="94981-149">Mogelijk moet u tooreconfigure uw cloudservice via Hallo [(cscfg) van de serviceconfiguratie](cloud-services-model-and-package.md#cscfg) bestand.</span><span class="sxs-lookup"><span data-stu-id="94981-149">You may need tooreconfigure your cloud service through hello [service config (cscfg)](cloud-services-model-and-package.md#cscfg) file.</span></span> <span data-ttu-id="94981-150">U moet eerst toodownload uw cscfg-bestand, wijzigen en vervolgens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="94981-150">First you need toodownload your .cscfg file, modify it, then upload it.</span></span>

1. <span data-ttu-id="94981-151">Klik op Hallo **instellingen** -pictogram of Hallo **alle instellingen** tooopen up Hallo koppelen **instellingen** blade.</span><span class="sxs-lookup"><span data-stu-id="94981-151">Click on hello **Settings** icon or hello **All settings** link tooopen up hello **Settings** blade.</span></span>

    ![Pagina met instellingen](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. <span data-ttu-id="94981-153">Klik op Hallo **configuratie** item.</span><span class="sxs-lookup"><span data-stu-id="94981-153">Click on hello **Configuration** item.</span></span>

    ![Configuratie-Blade](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. <span data-ttu-id="94981-155">Klik op Hallo **downloaden** knop.</span><span class="sxs-lookup"><span data-stu-id="94981-155">Click on hello **Download** button.</span></span>

    ![Downloaden](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. <span data-ttu-id="94981-157">Na het bijwerken van serviceconfiguratiebestand Hallo uploaden en Hallo configuratie-updates toepassen:</span><span class="sxs-lookup"><span data-stu-id="94981-157">After you update hello service configuration file, upload and apply hello configuration updates:</span></span>

    ![Uploaden](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. <span data-ttu-id="94981-159">Selecteer Hallo cscfg-bestand en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="94981-159">Select hello .cscfg file and click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94981-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="94981-160">Next steps</span></span>
* <span data-ttu-id="94981-161">Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94981-161">Learn how too[deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).</span></span>
* <span data-ttu-id="94981-162">Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94981-162">Configure a [custom domain name](cloud-services-custom-domain-name-portal.md).</span></span>
* <span data-ttu-id="94981-163">[Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94981-163">[Manage your cloud service](cloud-services-how-to-manage-portal.md).</span></span>
* <span data-ttu-id="94981-164">Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).</span><span class="sxs-lookup"><span data-stu-id="94981-164">Configure [ssl certificates](cloud-services-configure-ssl-certificate-portal.md).</span></span>

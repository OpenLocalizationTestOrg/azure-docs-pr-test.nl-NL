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
# <a name="how-tooconfigure-cloud-services"></a>Hoe tooConfigure Cloud-Services
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-how-to-configure-portal.md)
> * [Klassieke Azure Portal](cloud-services-how-to-configure.md)
>
>

U kunt de meest gebruikte Hallo-instellingen voor een cloudservice configureren in hello Azure-portal. Of als u tooupdate dat de configuratiebestanden rechtstreeks downloaden van een service configuration file tooupdate en vervolgens uploaden Hallo bijgewerkt bestands- en update Hallo cloudservice Hallo configuratiewijzigingen. In beide gevallen worden Hallo configuratie-updates gepusht tooall rolinstanties.

U kunt ook Hallo exemplaren van uw cloud service-rollen of extern bureaublad in ze beheren.

Azure alleen zorgt 99,95% servicebeschikbaarheid tijdens Hallo configuratie-updates hebt u ten minste twee rolexemplaren voor elke rol. Waarmee een virtuele machine tooprocess clientaanvragen terwijl andere hello wordt bijgewerkt. Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Een cloudservice wijzigen
Na opening Hallo [Azure-portal](https://portal.azure.com/), navigeer tooyour-cloudservice. Hier kunt beheren u veel aspecten van deze.

![Pagina met instellingen](./media/cloud-services-how-to-configure-portal/cloud-service.png)

Hallo **instellingen** of **alle instellingen** koppelingen geopend Hallo **instellingen** blade Hallo wijzigen **eigenschappen**, Hallo wijzigen **Configuratie**, Hallo beheren **certificaten**, setup **waarschuwing regels**, en beheren van Hallo **gebruikers** die toegang hebben toothis cloudservice.

![Blade van Azure cloud service-instellingen](./media/cloud-services-how-to-configure-portal/cs-settings-blade.png)

### <a name="manage-guest-os-version"></a>Gast OS-versie beheren

Standaard werkt Azure periodiek de Gast toohello laatste ondersteunde installatiekopie van het besturingssysteem binnen Hallo OS-familie die u hebt opgegeven in de serviceconfiguratie (.cscfg), zoals Windows Server 2016.

Als u een specifieke versie van het besturingssysteem tootarget moet, kunt u dit instellen in Hallo **configuratie** blade.

![Versie van het besturingssysteem instellen](./media/cloud-services-how-to-configure-portal/cs-settings-config-guestosversion.png)


>[!IMPORTANT]
> U kiest dat een specifieke versie van het besturingssysteem schakelt automatische OS bijgewerkt waardoor het uw verantwoordelijkheid patchen. U moet ervoor zorgen dat uw rolinstanties zijn ontvangen van updates of u uw toepassing toosecurity beveiligingsproblemen kan blootstellen.

## <a name="monitoring"></a>Bewaking
U kunt waarschuwingen tooyour cloudservice toevoegen. Klik op **instellingen** > **waarschuwing regels** > **waarschuwing toevoegen**.

![](./media/cloud-services-how-to-configure-portal/cs-alerts.png)

Hier kunt kunt u een waarschuwing instellen. Hello **metriek** vervolgkeuzelijst, kunt u een waarschuwing voor de volgende soorten gegevens Hallo instellen.

* Schijf lezen
* Schijf schrijven
* Het netwerk
* Uit het netwerk
* CPU-percentage

![](./media/cloud-services-how-to-configure-portal/cs-alert-item.png)

### <a name="configure-monitoring-from-a-metric-tile"></a>Bewaking van een metrische tegel configureren
In plaats van **instellingen** > **waarschuwingsregels**, kunt u klikken op een van de metrische tegels in Hallo Hallo **bewaking** sectie Hallo **Cloud service** blade.

![Cloudservice controleren](./media/cloud-services-how-to-configure-portal/cs-monitoring.png)

U kunt hiervandaan Hallo grafiek gebruikt met Hallo tegel aanpassen of een waarschuwingsregel toevoegen.

## <a name="reboot-reimage-or-remote-desktop"></a>Opnieuw opstarten of terugzetten van de installatiekopie extern bureaublad
Op dit moment kunt u geen extern bureaublad met Hallo configureren **Azure-portal**. Echter, u kunt instellen deze via Hallo [klassieke Azure-portal](cloud-services-role-enable-remote-desktop.md), [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md), of via [Visual Studio](../vs-azure-tools-remote-desktop-roles.md).

Klik eerst op Hallo cloud service-exemplaar.

![Cloud Service-exemplaar](./media/cloud-services-how-to-configure-portal/cs-instance.png)

Van Hallo-blade waarmee de opent u een verbinding met extern bureaublad te initiëren, op afstand opnieuw opstarten hello, of een exemplaar op afstand terugzetten van de installatiekopie (start met een nieuwe installatiekopie) Hallo.

![Cloud Service-exemplaar knoppen](./media/cloud-services-how-to-configure-portal/cs-instance-buttons.png)

## <a name="reconfigure-your-cscfg"></a>Uw cscfg-bestand configureren
Mogelijk moet u tooreconfigure uw cloudservice via Hallo [(cscfg) van de serviceconfiguratie](cloud-services-model-and-package.md#cscfg) bestand. U moet eerst toodownload uw cscfg-bestand, wijzigen en vervolgens te uploaden.

1. Klik op Hallo **instellingen** -pictogram of Hallo **alle instellingen** tooopen up Hallo koppelen **instellingen** blade.

    ![Pagina met instellingen](./media/cloud-services-how-to-configure-portal/cloud-service.png)
2. Klik op Hallo **configuratie** item.

    ![Configuratie-Blade](./media/cloud-services-how-to-configure-portal/cs-settings-config.png)
3. Klik op Hallo **downloaden** knop.

    ![Downloaden](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-download.png)
4. Na het bijwerken van serviceconfiguratiebestand Hallo uploaden en Hallo configuratie-updates toepassen:

    ![Uploaden](./media/cloud-services-how-to-configure-portal/cs-settings-config-panel-upload.png)
5. Selecteer Hallo cscfg-bestand en klik op **OK**.

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).
* [Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate-portal.md).

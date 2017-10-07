---
title: aaaHow tooconfigure een cloudservice (klassieke portal) | Microsoft Docs
description: Meer informatie over hoe tooconfigure cloud-services in Azure. Informatie over tooupdate Hallo cloud-serviceconfiguratie en toorole exemplaren van externe toegang configureren.
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
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

U kunt instellingen Hallo meest worden gebruikt voor een cloudservice configureren in Hallo klassieke Azure-portal. Of als u tooupdate dat de configuratiebestanden rechtstreeks downloaden van een service configuration file tooupdate en vervolgens uploaden Hallo bijgewerkt bestands- en update Hallo cloudservice Hallo configuratiewijzigingen. In beide gevallen worden Hallo configuratie-updates gepusht tooall rolinstanties.

Hallo klassieke Azure-portal kunt u ook te[verbinding met extern bureaublad inschakelen voor een rol in Azure Cloud Services](cloud-services-role-enable-remote-desktop.md)

Azure alleen zorgt 99,95% servicebeschikbaarheid tijdens Hallo configuratie-updates hebt u ten minste twee rolexemplaren voor elke rol. Waarmee een virtuele machine tooprocess clientaanvragen terwijl andere hello wordt bijgewerkt. Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Een cloudservice wijzigen
1. In Hallo [klassieke Azure-portal](http://manage.windowsazure.com/), klikt u op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **configureren**.
   
    ![Configuratiepagina](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    Op Hallo **configureren** pagina die u kunt bewaking, update-functie-instellingen configureren en kies Hallo gastbesturingssysteem en de familie voor rolinstanties. 
2. In **bewaking**, set Hallo niveau tooVerbose bewaking of minimale, en configureren van verbindingsreeksen voor Hallo diagnostische gegevens die vereist voor uitgebreide bewaking zijn.
3. Voor service-rollen (gegroepeerd per functie), kunt u instellingen na Hallo bijwerken:
   
    * **Instellingen** Hallo waarden van verschillende configuratie-instellingen die zijn opgegeven in Hallo wijzigen *ConfigurationSettings* elementen van hello (.cscfg) serviceconfiguratiebestand.

    * **Certificaten**  
        Hallo certificaatvingerafdruk die wordt gebruikt in SSL-versleuteling voor een rol wijzigen. toochange een certificaat, moet u eerst het nieuwe certificaat Hallo uploaden (op Hallo **certificaten** pagina). Hallo-vingerafdruk in Hallo certificaattekenreeks weergegeven in de instellingen van de rol Hallo vervolgens bijwerken.
4. In **besturingssysteem**, kunt u de besturingssysteemgroep Hallo of versie voor rolinstanties wijzigen of kies **automatische** tooenable automatische updates van de huidige besturingssysteemversie Hallo. Hallo-instellingen toepassen tooweb rollen en -werkrollen, maar hebben geen invloed op de virtuele Machines.
   
    Meest recente versie van besturingssysteem Hallo is geïnstalleerd op alle rolinstanties tijdens de implementatie en besturingssystemen Hallo standaard automatisch worden bijgewerkt. 
   
    Als u nodig hebt voor uw cloud service toorun op een andere besturingssysteemversie vanwege compatibiliteitsvereisten in uw code, kunt u een besturingssysteem familie en versie. Wanneer u een specifieke besturingssysteemversie kiest, worden automatische besturingssysteemupdates voor cloudservice Hallo onderbroken. U moet tooensure Hallo besturingssystemen ontvangen van updates.
   
    Als u alle compatibiliteitsproblemen die uw apps met de meest recente versie van besturingssysteem Hallo hebt opgelost, kunt u automatische besturingssysteemupdates inschakelen door de instelling Hallo besturingssysteemversie te**automatische**. 
   
    ![OS-instellingen](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave uw configuratie-instellingen en push ze toohello rolexemplaren te controleren, klikt u op **opslaan**. (Klik op **negeren** toocancel Hallo wijzigingen.) **Sla** en **negeren** toohello opdrachtbalk worden toegevoegd nadat u een instelling wijzigt.

## <a name="update-a-cloud-service-configuration-file"></a>Een configuratiebestand voor cloud-service bijwerken
1. Een cloud service configuratiebestand (.cscfg) met de huidige configuratie Hallo downloaden. Op Hallo **configureren** pagina voor de cloudservice hello, klikt u op **downloaden**. Klik vervolgens op **opslaan**, of klik op **OpslaanAls** toosave Hallo-bestand.
2. Na het bijwerken van serviceconfiguratiebestand Hallo uploaden en Hallo configuratie-updates toepassen:
   
   1. Op Hallo **configureren** pagina, klikt u op **uploaden**.
      
       ![Configuratie uploaden](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. In **configuratiebestand**, gebruik **Bladeren** tooselect Hallo bijgewerkt cscfg-bestand.
   3. Als uw cloudservice geen rollen waarvoor slechts één exemplaar bevat, selecteert u Hallo **configuratie toepassen, zelfs als een of meer rollen één exemplaar bevatten** selectievakje tooenable Hallo configuratie-updates voor Hallo rollen tooproceed.
      
       Tenzij u ten minste twee exemplaren van elke rol definiëren, ten minste 99,95% kan niet worden gegarandeerd door Azure beschikbaarheid van uw cloudservice tijdens het bijwerken van de service-configuratie. Zie voor meer informatie [Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).
   4. Klik op **OK** (vinkje). 

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name.md).
* [Beheren van uw cloudservice](cloud-services-how-to-manage.md).
* [Verbinding met extern bureaublad voor een rol in Azure Cloudservices inschakelen](cloud-services-role-enable-remote-desktop.md)
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate.md).


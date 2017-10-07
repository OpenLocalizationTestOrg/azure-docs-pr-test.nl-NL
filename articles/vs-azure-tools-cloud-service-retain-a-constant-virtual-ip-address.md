---
title: aaaHow tooretain constante virtueel IP-adres voor een Azure cloudservice | Microsoft Docs
description: Meer informatie over hoe tooensure die Hallo virtueel IP-adres (VIP) van uw Azure-cloud-service niet wijzigen.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 4a58e2c6-7a79-4051-8a2c-99182ff8b881
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 9e27121797ffb61517b8d2c2661ec44ff7298968
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="retain-a-constant-virtual-ip-address-for-an-azure-cloud-service"></a>Een constante virtuele IP-adres voor een Azure cloudservice behouden
Wanneer u een cloudservice die wordt gehost in Azure bijwerkt, moet u mogelijk tooensure waarmee Hallo virtueel IP-adres (VIP) van Hallo-service niet wordt gewijzigd. Veel management domeinservices gebruiken Hallo System DNS (Domain Name) voor het registreren van domeinnamen. DNS werkt alleen als Hallo VIP blijft Hallo dezelfde. U kunt Hallo **Wizard publiceren** in hulpprogramma's van Azure tooensure die Hallo VIP van uw cloudservice niet wijzigen wanneer u deze bijwerken. Voor meer informatie over het beheer van toouse DNS-domein voor cloud-services, Zie [configureren van een aangepaste domeinnaam voor een Azure cloudservice](cloud-services/cloud-services-custom-domain-name.md).

## <a name="publish-a-cloud-service-without-changing-its-vip"></a>Een cloudservice zonder te wijzigen van de VIP publiceren
Hallo VIP van een cloudservice is toegewezen tijdens de eerste implementatie tooAzure in een bepaalde omgeving, zoals Hallo-productieomgeving. Hallo VIP wordt alleen gewijzigd als u Hallo implementatie expliciet verwijderen of Hallo implementatie impliciet wordt verwijderd door de implementatie van Hallo proces niet bijwerken. tooretain hello VIP, moet u niet uw implementatie verwijderd en moet u ervoor zorgen dat Visual Studio automatisch de implementatie niet verwijderen. 

U kunt de implementatie-instellingen opgeven in Hallo **Wizard publiceren**, die ondersteuning biedt voor verschillende implementatieopties. U kunt een nieuwe implementatie of een update-implementatie, kan dit incrementele of gelijktijdige opgeven. Beide soorten update-implementatie behouden Hallo VIP. Zie voor definities van deze verschillende soorten implementatie [Publish Azure Application Wizard](vs-azure-tools-publish-azure-application-wizard.md). Bovendien kunt u bepalen of de vorige implementatie van een cloudservice Hallo wordt verwijderd als er een fout optreedt. Als u deze optie niet correct hebt ingesteld, is het mogelijk dat Hallo VIP onverwacht gewijzigd.

## <a name="update-a-cloud-service-without-changing-its-vip"></a>Een cloudservice bijwerken zonder te wijzigen van de VIP
1. Maak of open een Azure-cloud service-project in Visual Studio. 

2. In **Solution Explorer**, klik met de rechtermuisknop Hallo project. Selecteer in het snelmenu hello, **publiceren**.

    ![Het menu Publish](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/solution-explorer-publish-menu.png)

3. In Hallo **Publish Azure Application** dialoogvenster, selecteer hello Azure-abonnement toowhich gewenste toodeploy. Meld u aan als nodig en selecteer **volgende**.

    ![Azure Application aanmeldingspagina publiceren](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-signin.png)

4. Op Hallo **algemene instellingen** tabblad, controleert u of deze naam Hallo van Hallo cloud service toowhich u, hello implementeert **omgeving**, Hallo **buildconfiguratie**, en Hallo **Serviceconfiguratie** juist zijn.

    ![Tabblad algemene instellingen voor Azure-toepassing publiceren](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-common-settings.png)

5. Op Hallo **geavanceerde instellingen** Controleer die Hallo **implementatielabel** en Hallo **opslagaccount** juist zijn. Controleren dat Hallo **verwijderen van de implementatie mislukt** selectievakje is uitgeschakeld en controleer of deze Hallo **implementatie-update** selectievakje is ingeschakeld. Door Hallo wissen **verwijderen van de implementatie mislukt** selectievakje u ervoor zorgen dat uw VIP niet verloren gaan als er een fout optreedt tijdens de implementatie. Door het selecteren van Hallo **implementatie-update** selectievakje, zorgt u ervoor dat uw implementatie wordt niet verwijderd en uw VIP niet verloren wanneer u uw toepassing opnieuw publiceren. 

    ![Tabblad Geavanceerde instellingen voor Azure-toepassing publiceren](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-advanced-settings.png)

6. toofurther aangeven hoe Hallo rollen toobe is bijgewerkt, selecteert u **instellingen** volgende te**implementatie-update**. Selecteer een **incrementele update** of **gelijktijdig bijwerken**, en selecteer **OK**. Kies **incrementele update** tooupdate elk exemplaar van uw toepassing achter elkaar, zodat die toepassing hello altijd beschikbaar is. Kies **gelijktijdig bijwerken** tooupdate alle exemplaren van uw toepassing op Hallo hetzelfde moment. Gelijktijdige bijwerken is sneller, maar de service mogelijk niet beschikbaar tijdens het updateproces Hallo. Wanneer u klaar bent, selecteert u **volgende**.

    ![Pagina implementatie-instellingen van Azure-toepassing publiceren](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-deployment-update-settings.png)

7. In Hallo **Publish Azure Application** dialoogvenster, **volgende** tot Hallo **samenvatting** pagina wordt weergegeven. Controleer de instellingen en selecteer vervolgens **publiceren**.
   
    ![Pagina overzicht van de Azure-toepassing publiceren](./media/vs-azure-tools-cloud-service-retain-a-constant-virtual-ip-address/azure-publish-summary.png)

## <a name="next-steps"></a>Volgende stappen
- [Met behulp van Visual Studio publiceren Wizard Azure-toepassing hello](vs-azure-tools-publish-azure-application-wizard.md)


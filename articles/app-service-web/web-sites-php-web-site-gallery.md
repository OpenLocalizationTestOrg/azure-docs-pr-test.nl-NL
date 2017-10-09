---
title: aaaCreate een WordPress-web-app in Azure App Service | Microsoft Docs
description: Meer informatie over hoe een nieuwe Azure toocreate web-app voor een WordPress-blog hello Azure Portal gebruiken.
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 193ae094-0d7c-4749-a09b-ff4b1240149e
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 3a95fcb6732c15a8200921ce474b6dde2298dec3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-web-app-in-azure-app-service"></a>Een WordPress-web-app maken in Azure App Service
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Deze zelfstudie laat zien hoe een WordPress-blog toodeploy site van hello Azure Marketplace.

Wanneer u met het Hallo-zelfstudie bent klaar hebt u uw eigen WordPress-blogsite up en wordt uitgevoerd in de cloud Hallo.

![WordPress-site](./media/web-sites-php-web-site-gallery/wpdashboard.png)

U leert het volgende:

* Hoe toofind een toepassingssjabloon in hello Azure Marketplace.
* Hoe toocreate een web-app in Azure App Service die is gebaseerd op Hallo-sjabloon.
* Hoe tooconfigure Azure App Service-instellingen voor Hallo nieuwe web-app en database.

Hello Azure Marketplace maakt beschikbaar een breed scala aan populaire web-apps die zijn ontwikkeld door Microsoft en derden bedrijven open-source software initiatieven. Hallo-web-apps zijn gebouwd op een breed scala aan populaire frameworks, zoals [PHP](/develop/nodejs/) in dit WordPress-voorbeeld [.NET](/develop/net/), [Node.js](/develop/nodejs/), [Java](/develop/java/), en [Python](/develop/python/), tooname een enkele. een web-app vanuit Azure Marketplace Hallo enige software die u nodig is Hallo browser die u voor Hallo gebruikt Hallo toocreate [Azure Portal](https://portal.azure.com/). 

Hallo WordPress-site die u in deze zelfstudie implementeert maakt gebruik van MySQL voor Hallo-database. Als u tooinstead SQL-Database gebruiken voor Hallo-database wenst, Zie [Project Nami](http://projectnami.org/). **Project Nami** is ook beschikbaar via Hallo Marketplace.

> [!NOTE]
> toocomplete deze zelfstudie maakt u een Microsoft Azure-account nodig. Als u geen account hebt, kunt u [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F) of [zich aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
> 
> Als u wilt dat tooget gestart met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/). Daar kunt u direct een eenvoudige, tijdelijke web-app maken in App Service. U hebt hiervoor geen creditcard nodig en bent nergens toe verplicht.
> 
> 

## <a name="select-wordpress-and-configure-for-azure-app-service"></a>WordPress selecteren en configureren voor Azure App Service
1. Meld u bij toohello [Azure Portal](https://portal.azure.com/).
2. Klik op **Nieuw**.
   
    ![Nieuwe maken][5]
3. Zoek naar **WordPress** en klik op **WordPress**. Als u toouse SQL-Database in plaats van MySQL wenst, zoekt u naar **Project Nami**.
   
    ![WordPress via een lijst][7]
4. Klik na het lezen van Hallo beschrijving van Hallo WordPress-app op **maken**.
   
    ![Maken](./media/web-sites-php-web-site-gallery/create.png)
5. Voer een naam voor de web-app Hallo in Hallo **Web-app** vak.
   
    Deze naam moet uniek zijn in Hallo azurewebsites.net domein omdat Hallo-URL van Hallo web-app {naam}. azurewebsites.net. Als Hallo-naam die u opgeeft niet uniek is, wordt een rood uitroepteken in het tekstvak Hallo weergegeven.
6. Als u meer dan één abonnement hebt, kiest u Hallo één gewenste toouse. 
7. Selecteer een **Resourcegroep** of maak een nieuwe.
   
    Zie [Overzicht van Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) voor meer informatie over resourcegroepen.
8. Selecteer een **App Service-plan/-locatie** of maak een nieuw(e).
   
    Zie [Overzicht van Azure App Service-plannen](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) voor meer informatie over App Service-plannen    
9. Klik op **Database**, en klik vervolgens in Hallo **nieuwe MySQL-Database** blade Hallo vereist waarden opgeven voor het configureren van uw MySQL-database.
   
    a. Voer een nieuwe naam op of laat de standaardnaam Hallo.
   
    b. Hallo laat **databasetype** instellen te**gedeelde**.
   
    c. Kies Hallo dezelfde locatie als u één Hallo voor Hallo web-app hebt gekozen.
   
    d. Kies een prijscategorie. Mercury (gratis met minimale verbindingen en schijfruimte) is voldoende voor deze zelfstudie.
10. In Hallo **nieuwe MySQL-Database** blade, klikt u op **OK**. 
11. In Hallo **WordPress** blade Hallo juridische voorwaarden accepteren en klik vervolgens op **maken**. 
    
     ![Web-app configureren](./media/web-sites-php-web-site-gallery/configure.png)
    
     Azure App Service gemaakt Hallo web-app, doorgaans in minder dan een minuut. U kunt Hallo voortgang bekijken door te klikken op het belpictogram Hallo HALLO hallo portal-pagina bovenaan in.
    
     ![Voortgangsindicator](./media/web-sites-php-web-site-gallery/progress.png)

## <a name="launch-and-manage-your-wordpress-web-app"></a>De WordPress-web-app starten en beheren
1. Wanneer Hallo web-apps maken is voltooid, gaat u in hello Azure Portal toohello resourcegroep waarin u Hallo toepassing gemaakt en ziet u Hallo web-app en het Hallo-database.
   
    Hallo extra resource met Hallo gloeilampje is [Application Insights](/services/application-insights/), die bewakingsservices voor uw web-app biedt.
2. In Hallo **resourcegroep** blade, klikt u op Hallo web app regel.
   
    ![Web-app configureren](./media/web-sites-php-web-site-gallery/resourcegroup.png)
3. Hallo blade Web-app klikt u op **Bladeren**.
   
    ![site-URL][browse]
4. In Hallo WordPress **Welkom** pagina, Voer Hallo configuratie-informatie in die WordPress nodig en klik vervolgens op **WordPress installeren**.
   
    ![WordPress configureren](./media/web-sites-php-web-site-gallery/wpconfigure.png)
5. Meld u aan met Hallo-referenties die u hebt gemaakt op Hallo **Welkom** pagina.  
6. De dashboardpagina van uw site wordt geopend.    
   
    ![WordPress-site](./media/web-sites-php-web-site-gallery/wpdashboard.png)

## <a name="next-steps"></a>Volgende stappen
U hebt gezien hoe toocreate en implementeren van een PHP-web-app uit de galerie Hallo. Zie voor meer informatie over het gebruik van PHP in Azure Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

Voor meer informatie over het toowork met App Service Web Apps, Zie Hallo koppelingen op Hallo linkerkant van Hallo pagina (in brede browservensters) of bovenaan Hallo Hallo pagina (in smalle browservensters). 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een wijziging van de toohello handleiding van Websites tooApp Service [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714).

[5]: ./media/web-sites-php-web-site-gallery/startmarketplace.png
[7]: ./media/web-sites-php-web-site-gallery/search-web-app.png
[browse]: ./media/web-sites-php-web-site-gallery/browse-web.png

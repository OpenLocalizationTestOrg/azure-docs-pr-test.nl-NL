---
title: een WordPress-app in Azure-portal op vijf minuten Hallo aaaDeploy | Microsoft Docs
description: Informatie over hoe eenvoudig het is toorun web-apps in App Service door het implementeren van een WordPress-app. U kunt direct de resultaten bekijken.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/13/2017
ms.author: cephalin
ms.openlocfilehash: 4cd26bbacf89657997847ded1284e472288ddebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-wordpress-app-in-hello-azure-portal-in-five-minutes"></a>Een WordPress-app in Azure-portal Hallo implementeren binnen vijf minuten

Deze zelfstudie leert u hoe toodeploy uw eerste [WordPress](https://wordpress.org/) web-app te[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuten.

![WordPress-site](./media/app-service-web-get-started-php-portal/wpdashboard.png)

## <a name="prerequisites"></a>Vereisten
U hebt een Microsoft Azure-account nodig. Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account. Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.
> 
> 

## <a name="deploy-hello-wordpress-app"></a>Hallo WordPress-app implementeren
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Open [https://portal.azure.com/#create/WordPress.WordPress](https://portal.azure.com/#create/WordPress.WordPress).

    Deze koppeling is een snelkoppeling tooimmediately configureren een nieuwe WordPress-app in hello Azure-portal.

3. In **App-naam** voert u een naam in voor de web-app. U ziet een groen vinkje in het vak Hallo als Hallo naam uniek zijn in Hallo `azurewebsites.net` domein.
   
5. In **resourcegroep**, klikt u op **nieuw** toocreate een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md), geef het een naam.

6. In **Databaseprovider** selecteert u **CleaDB**.

7. Klik op **App Service-plan/-locatie** > **Nieuw**. Hallo configureren [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) zoals wordt weergegeven:

    - In **App Service-abonnement**, Hallo gewenste typenaam.
    - In **locatie**, kies een locatie toohost uw abonnement.
    - Klik op **Prijscategorie** en selecteer **F1 Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.
    - Klik op **OK**.

8. Klik op **Database** > **Nieuw**. Hallo SQL-Database configureren zoals wordt weergegeven:

    - In **Databasenaam** voert u een naam in voor de database. 
    - In **locatie**, kies Hallo dezelfde locatie als Hallo App Service-abonnement.
    - Klik op **Prijscategorie** en selecteer **Mercury** of een andere categorie die bij u past. Klik dan op **Selecteren**.
    - Klik op **Juridische voorwaarden** en klik op **Kopen**.
    - Klik op **OK**.

9. Klik op **Create**.

    Azure maakt nu uw WordPress-app op basis van uw configuratie. De melding **Implementatie is gestart...** wordt nu weergegeven.

    ![De implementatie is gestart - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-wordpress-web-app"></a>De WordPress-web-app starten en beheren

Wanneer Azure klaar is met het implementeren van de app, krijgt u nog een melding te zien.

![De implementatie is voltooid - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/deployment-succeeded.png)

1. Klik op Hallo-melding. Als u deze hebt gemist, u kunt altijd toegang tot dit door te klikken op Hallo melding Bel (![melding onderstaande - eerste WordPress in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    U krijgt nu de [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) te zien voor het beheer van uw web-app (*blade*: een portalpagina die horizontaal wordt geopend).

3. Klik in het Hallo bovenaan de pagina overzicht Hallo op **Bladeren**.
   
    ![Bladeren - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/browse.png)

    Nu u Hallo WordPress ziet **Welkom** pagina. Hallo WordPress installatie configureren en begin met het afspelen.

    ![Configuratie van WordPress - eerste WordPress in Azure App Service](./media/app-service-web-get-started-php-portal/wordpress-config.png)
    
## <a name="next-steps"></a>Volgende stappen
* [Maken, configureren en implementeren van een Laravel web app tooAzure](app-service-web-php-get-started.md) -meer Hallo basisvaardigheden moet u toorun een PHP-web-app in Azure, zoals:

    * Apps via PowerShell/Bash maken en configureren in Azure.
    * De PHP-versie instellen.
    * Een begin-bestand dat zich niet in de hoofdmap toepassing hello gebruiken.
    * Composer-automatisering inschakelen.
    * Omgevingsspecifieke variabelen openen.
    * Veelvoorkomende problemen oplossen.

* [Uw code tooAzure App Service implementeren](web-sites-deploy.md)-informatie over hoe de opslagplaatsen voor het beheren van toodeploy van FTP- of bron.
* [Functionaliteit tooyour eerste web-app toevoegen](app-service-web-get-started-2.md) -Til uw Azure-app toohello naast niveau. Verifieer uw gebruikers. Schaal de app op basis van vraag. Stel prestatiewaarschuwingen in. Dit alles met slechts enkele klikken.

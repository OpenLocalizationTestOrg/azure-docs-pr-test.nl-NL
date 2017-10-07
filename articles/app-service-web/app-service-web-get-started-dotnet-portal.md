---
title: een Umbraco web-app in Azure-portal op vijf minuten Hallo aaaDeploy | Microsoft Docs
description: Informatie over hoe eenvoudig het is toorun web-apps in App Service door het implementeren van een voorbeeld van ASP.NET-app. U kunt direct de resultaten bekijken.
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/10/2017
ms.author: cephalin
ms.openlocfilehash: 6da45f99b3043a3684e3d99c14e6443d597b5212
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-umbraco-web-app-in-hello-azure-portal-in-five-minutes"></a>Een Umbraco web-app in Azure-portal Hallo implementeren binnen vijf minuten

Deze zelfstudie helpt u n implementeren [Umbraco](https://our.umbraco.org/) web-app te[Azure App Service](../app-service/app-service-value-prop-what-is.md) in minuten.

![Umbraco-app](./media/app-service-web-get-started-dotnet-portal/defaultpage.png)

## <a name="prerequisites"></a>Vereisten
U hebt een Microsoft Azure-account nodig. Als u geen account hebt, kunt u zich [aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) of [uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).

> [!NOTE]
> U kunt [App Service proberen](https://azure.microsoft.com/try/app-service/) zonder een Azure-account. Een eenvoudige app maken en te spelen met voor up tooan uur--geen creditcard nodig en zonder verdere verplichtingen.
> 
> 

## <a name="deploy-hello-aspnet-app"></a>Hallo ASP.NET-app implementeren
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).

2. Open [https://portal.azure.com/#create/umbracoorg.UmbracoCMS](https://portal.azure.com/#create/umbracoorg.UmbracoCMS).

    Deze koppeling is een snelkoppeling tooimmediately configureren een nieuwe Umbraco-app in hello Azure-portal.

3. In **App-naam** voert u een naam in voor de web-app. U ziet een groen vinkje in het vak Hallo als Hallo naam uniek zijn in Hallo `azurewebsites.net` domein.
   
5. In **resourcegroep**, klikt u op **nieuw** toocreate een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md), geef het een naam.

7. Klik op **App Service-plan/-locatie** > **Nieuw**. Hallo configureren [App Service-abonnement](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) zoals wordt weergegeven:

    - In **App Service-abonnement**, Hallo gewenste typenaam.
    - In **locatie**, kies een locatie toohost uw abonnement.
    - Klik op **Prijscategorie** en selecteer **F1 Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.
    - Klik op **OK**.

    De configuratie van uw Umbraco CMS ziet er nu als Hallo schermafbeelding te volgen:

    ![Configuratie in uitvoering - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-in-progress.png)

12. Klik op **SQL Database** > **Een nieuwe database maken**. Hallo SQL-Database configureren zoals wordt weergegeven:

    - Voer in **Naam** een naam in, zoals **myDB**.
    - Klik op **Prijscategorie** en selecteer **F Gratis** of een andere categorie die bij u past. Klik dan op **Selecteren**.
    - Klik op **Doelserver** > **Een nieuwe server maken**. Hallo-databaseserver configureren zoals wordt weergegeven:

        - Voer in **Servernaam** een servernaam in. U ziet een groen vinkje in het vak Hallo als Hallo naam uniek zijn in Hallo `.database.windows.net` domein.
        - In **aanmeldgegevens van serverbeheerder**, type Hallo beheerder gebruikersnaam gewenst.
        - In **wachtwoord** en **wachtwoord bevestigen**, type Hallo gewenste wachtwoord.
        - Selecteer Hallo op locatie, dezelfde locatie die u voor Hallo web-app gebruikt.
        - Zorg ervoor dat **toestaan azure-services tooaccess server** is geselecteerd.
        - Klik op **Selecteren**.
    
    - Klik op **Selecteren**.

13. Klik op **Web-appinstellingen**Hallo database een gebruikersnaam en wachtwoord opgeven en klik op **OK**.

    De configuratie van uw Umbraco CMS ziet er nu als Hallo schermafbeelding te volgen:

    ![Configuratie voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/configure-complete.png)

14. Klik op **Create**.
    
    Azure maakt nu uw Umbraco-app op basis van uw configuratie. De melding **Implementatie is gestart...** wordt nu weergegeven.

    ![De implementatie is voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-started.png)
   
## <a name="launch-and-manage-your-umrbaco-web-app"></a>Uw Umbraco-web-app starten en beheren

Wanneer Azure klaar is met het implementeren van de app, krijgt u nog een melding te zien.

![De implementatie is voltooid - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/deployment-succeeded.png)

1. Klik op Hallo-melding. Als u deze hebt gemist, u kunt altijd toegang tot dit door te klikken op Hallo melding Bel (![melding onderstaande - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/notification.png)).

    U krijgt nu de [blade](../azure-resource-manager/resource-group-portal.md#manage-resources) te zien voor het beheer van uw web-app (*blade*: een portalpagina die horizontaal wordt geopend).

3. Klik in het Hallo bovenaan de pagina overzicht Hallo op **Bladeren**.
   
    ![Bladeren - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/browse.png)

    Nu u Hallo Umbraco ziet **Welkom** pagina. Hallo Umbraco installatie configureren en begin met het afspelen.

    ![Umbraco-configuratie - eerste Umbraco in Azure App Service](./media/app-service-web-get-started-dotnet-portal/umbraco-config.png)
    
## <a name="next-steps"></a>Volgende stappen
* [Een ASP.NET web app tooAzure App Service met Visual Studio implementeren](app-service-web-get-started-dotnet.md) -informatie over hoe een nieuwe Azure-web-app vanuit Visual Studio, met een van de Hallo toocreate Toepassingssjablonen opgenomen.
* [Uw code tooAzure App Service implementeren](web-sites-deploy.md)-informatie over hoe de opslagplaatsen voor het beheren van toodeploy van FTP- of bron.
* [Functionaliteit tooyour eerste web-app toevoegen](app-service-web-get-started-2.md) -Til uw Azure-app toohello naast niveau. Verifieer uw gebruikers. Schaal de app op basis van vraag. Stel prestatiewaarschuwingen in. Dit alles met slechts enkele klikken.

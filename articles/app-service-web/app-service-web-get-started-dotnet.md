---
title: aaaCreate een ASP.NET web-app in Azure | Microsoft Docs
description: Meer informatie over hoe toorun web-apps in Azure App Service door het implementeren van Hallo standaard ASP.NET web-app.
services: app-service\web
documentationcenter: 
author: cephalin
manager: wpickett
editor: 
ms.assetid: b1e6bd58-48d1-4007-9d6c-53fd6db061e3
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 06/14/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eec916b3c32b6c8b68083177938c5c822a9782b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-web-app-in-azure"></a>Een ASP.NET-web-app maken in Azure

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.  Deze snelstartgids toont hoe toodeploy uw eerste ASP.NET web-app tooAzure Web-Apps. Als u klaar bent, hebt u een resourcegroep die bestaat uit een App Service-plan en een Azure-web-app met een geïmplementeerde webtoepassing.

Bekijk de video toosee Hallo deze snelstartgids in actie en voer vervolgens Hallo stappen zelf toopublish uw eerste .NET-app in Azure.

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-NET-Developers/Create-a-NET-app-in-Azure-Quickstart/player]

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

* Installeer [Visual Studio 2017](https://www.visualstudio.com/downloads/) Hello werkbelastingen te volgen:
    - **ASP.NET- en web-ontwikkeling**
    - **Azure-ontwikkeling**

    ![ASP.NET- en web-ontwikkeling en Azure-ontwikkeling (onder Web en cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-an-aspnet-web-app"></a>Een ASP.NET-web-app maken

Maak in Visual Studio een project door **Bestand > Nieuw > Project** te selecteren. 

In Hallo **nieuw Project** dialoogvenster Selecteer **Visual C# > Web > ASP.NET-webtoepassing (.NET Framework)**.

Naam van de toepassing hello _myFirstAzureWebApp_, en selecteer vervolgens **OK**.
   
![Het dialoogvenster Nieuw project](./media/app-service-web-get-started-dotnet/new-project.png)

U kunt elk type ASP.NET web app tooAzure implementeren. Selecteer voor deze snelstartgids Hallo **MVC** sjabloon, en zorg ervoor dat de verificatie is ingesteld, te**geen verificatie**.
      
Selecteer **OK**.

![Het dialoogvenster Nieuw ASP.NET-project](./media/app-service-web-get-started-dotnet/select-mvc-template.png)

Hallo-menu en selecteer **fouten opsporen > starten zonder foutopsporing** toorun Hallo web-app lokaal.

![De app lokaal uitvoeren](./media/app-service-web-get-started-dotnet/local-web-app.png)

## <a name="publish-tooazure"></a>TooAzure publiceren

In Hallo **Solution Explorer**, klik met de rechtermuisknop Hallo **myFirstAzureWebApp** project en selecteer **publiceren**.

![Publiceren vanuit Solution Explorer](./media/app-service-web-get-started-dotnet/solution-explorer-publish.png)

Zorg ervoor dat **Microsoft Azure App Service** is geselecteerd en selecteer dan **Publiceren**.

![Publiceren vanaf de projectoverzichtspagina](./media/app-service-web-get-started-dotnet/publish-to-app-service.png)

Hiermee opent u Hallo **Create App Service** dialoogvenster waarmee u alle Hallo nodig Azure-resources toorun Hallo ASP.NET-web-app maken in Azure.

## <a name="sign-in-tooazure"></a>Meld u aan tooAzure

In Hallo **Create App Service** dialoogvenster Selecteer **account toevoegen**, en meld u aan tooyour Azure-abonnement. Als u al bent aangemeld, selecteer Hallo account Hallo met de gewenste abonnement uit de vervolgkeuzelijst Hallo.

> [!NOTE]
> Als u al bent aangemeld, selecteert u **Maken** nog niet.
>
>
   
![Meld u aan tooAzure](./media/app-service-web-get-started-dotnet/sign-in-azure.png)

## <a name="create-a-resource-group"></a>Een resourcegroep maken

[!INCLUDE [resource group intro text](../../includes/resource-group.md)]

Volgende te**resourcegroep**, selecteer **nieuw**.

Naam Hallo resourcegroep **myResourceGroup** en selecteer **OK**.

## <a name="create-an-app-service-plan"></a>Een App Service-plan maken

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

Volgende te**App Service-Plan**, selecteer **nieuw**. 

In Hallo **Configure App Service Plan** dialoogvenster Hallo-instellingen in Hallo schermafbeelding Hallo tabel gebruiken.

![Een App Service-plan maken](./media/app-service-web-get-started-dotnet/configure-app-service-plan.png)

| Instelling | Voorgestelde waarde | Beschrijving |
|-|-|-|
|App Service-plan| myAppServicePlan | Naam van Hallo App Service-abonnement. |
| Locatie | West-Europa | Hallo datacenter waar Hallo web-app wordt gehost. |
| Grootte | Gratis | De [prijscategorie](https://azure.microsoft.com/pricing/details/app-service/) bepaalt de hosting-functies. |

Selecteer **OK**.

## <a name="create-and-publish-hello-web-app"></a>Maken en publiceren van Hallo web-app

In **Web-Appnaam**, typ een unieke app-naam (geldige tekens zijn `a-z`, `0-9`, en `-`), of accepteer Hallo unieke naam voor het automatisch gegenereerd. Hallo-URL van de web-app Hallo is `http://<app_name>.azurewebsites.net`, waarbij `<app_name>` is de naam van uw web-app.

Selecteer **maken** toostart hello Azure-resources maken.

![Naam van web-app configureren](./media/app-service-web-get-started-dotnet/web-app-name.png)

Zodra Hallo wizard is voltooid, het Hallo ASP.NET web app tooAzure publiceert en vervolgens wordt gestart in de standaardbrowser Hallo app Hallo.

![Gepubliceerde ASP.NET-web-app in Azure](./media/app-service-web-get-started-dotnet/published-azure-web-app.png)

Hallo web-appnaam is opgegeven in Hallo [maken en publiceren van stap](#create-and-publish-the-web-app) wordt gebruikt als de URL-voorvoegsel in Hallo indeling Hallo `http://<app_name>.azurewebsites.net`.

Gefeliciteerd, uw ASP.NET-web-app wordt live uitgevoerd in Azure App Service.

## <a name="update-hello-app-and-redeploy"></a>Update Hallo app en de implementatie opnieuw uit

Van Hallo **Solution Explorer**Open _Views\Home\Index.cshtml_.

Hallo zoeken `<div class="jumbotron">` HTML code aan de bovenkant Hallo en vervang Hallo volledige element Hello code te volgen:

```HTML
<div class="jumbotron">
    <h1>ASP.NET in Azure!</h1>
    <p class="lead">This is a simple app that we’ve built that demonstrates how toodeploy a .NET app tooAzure App Service.</p>
</div>
```

tooredeploy tooAzure, klik met de rechtermuisknop Hallo **myFirstAzureWebApp** project in **Solution Explorer** en selecteer **publiceren**.

Pagina publiceren in hello, selecteer **publiceren**.

Als het publiceren is voltooid, Start Visual Studio een browser toohello-URL van Hallo web-app.

![Bijgewerkte ASP.NET-web-app in Azure](./media/app-service-web-get-started-dotnet/updated-azure-web-app.png)

## <a name="manage-hello-azure-web-app"></a>Hello Azure-web-app beheren

Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toomanage Hallo web-app.

Selecteer in het linkermenu Hallo **App Services**, en selecteer vervolgens Hallo-naam van uw Azure-web-app.

![Navigatie in de portal tooAzure web-app](./media/app-service-web-get-started-dotnet/access-portal.png)

De pagina Overzicht van uw web-app wordt weergegeven. Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen. 

![App Service-blade in Azure Portal](./media/app-service-web-get-started-dotnet/web-app-blade.png)

Hallo linkermenu biedt verschillende pagina's voor het configureren van uw app. 

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [ASP.NET met SQL Database](app-service-web-tutorial-dotnet-sqldatabase.md)

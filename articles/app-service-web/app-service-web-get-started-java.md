---
title: aaaCreate uw eerste web-app van Java in Azure
description: Meer informatie over hoe toorun web-apps in App Service door het implementeren van een eenvoudige Java-app.
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 8bacfe3e-7f0b-4394-959a-a88618cb31e1
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: quickstart
ms.date: 6/7/2017
ms.author: cephalin;robmcm
ms.custom: mvc
ms.openlocfilehash: 81315c07b5aa84cbec50a17b2cb3914927b19c00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-web-app-in-azure"></a>Uw eerste Java-web-app in Azure maken

Hallo [Web-Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) functie van [Azure App Service](../app-service/app-service-value-prop-what-is.md) biedt een zeer schaalbaar, zelf patch webhosting-service. Deze snelstartgids ziet u hoe toodeploy een Java web-app tooApp Service met behulp van Hallo [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/).

!['Hello Azure'! voorbeeld van web-app](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="prerequisites"></a>Vereisten

toocomplete deze snelstartgids installeren:

* Hallo gratis [Eclipse IDE voor Java EE-ontwikkelaars](http://www.eclipse.org/downloads/). Deze Quickstart maakt gebruik van Eclipse Neon.
* Hallo [Azure Toolkit voor Eclipse](/azure/azure-toolkit-for-eclipse-installation).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-dynamic-web-project-in-eclipse"></a>Een dynamisch webproject maken in Eclipse

Selecteer in Eclipse **Bestand** > **Nieuw** > **Dynamisch webproject**.

In Hallo **nieuwe dynamisch webproject** in het dialoogvenster, naam Hallo project **MyFirstJavaOnAzureWebApp**, en selecteer **voltooien**.
   
![Het dialoogvenster Nieuw dynamisch webproject](./media/app-service-web-get-started-java/new-dynamic-web-project-dialog-box.png)

### <a name="add-a-jsp-page"></a>Een JSP-pagina toevoegen

Geef Projectverkenner weer als dat nu niet het geval is.

![Java EE-werkruimte voor Eclipse](./media/app-service-web-get-started-java/pe.png)

Vouw in Projectverkenner Hallo **MyFirstJavaOnAzureWebApp** project.
Klik met de rechtermuisknop op **WebContent** en selecteer vervolgens **Nieuw** > **JSP-bestand**.

![Menu voor een nieuw JSP-bestand in Projectverkenner](./media/app-service-web-get-started-java/new-jsp-file-menu.png)

In Hallo **nieuw JSP-bestand** in het dialoogvenster:

* Bestand met de Hallo **index.jsp**.
* Selecteer **Voltooien**.

  ![Het dialoogvenster Nieuw JSP-bestand](./media/app-service-web-get-started-java/new-jsp-file-dialog-box-page-1.png)

In het bestand index.jsp hello, vervangt u Hallo `<body></body>` element met Hallo aantekeningen te volgen:

```jsp
<body>
<h1><% out.println("Hello Azure!"); %></h1>
</body>
```

Hallo wijzigingen opslaan.

## <a name="publish-hello-web-app-tooazure"></a>Hallo web app tooAzure publiceren

In Projectverkenner met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Azure** > **publiceren als Azure-Web-App**.

![Het contextmenu Publiceren als Azure Web App](./media/app-service-web-get-started-java/publish-as-azure-web-app-context-menu.png)

In Hallo **Azure aanmelden** dialoogvenster, houd Hallo **interactief** optie en selecteer vervolgens **aanmelden**.

Instructies Hallo aanmelden.

### <a name="deploy-web-app-dialog-box"></a>Het dialoogvenster Web-app implementeren

Nadat u zich hebt geregistreerd in Azure-account tooyour, Hallo **Web-App implementeren** dialoogvenster wordt weergegeven.

Selecteer **Maken**.

![Het dialoogvenster Web-app implementeren](./media/app-service-web-get-started-java/deploy-web-app-dialog-box.png)

### <a name="create-app-service-dialog-box"></a>Het dialoogvenster App Service maken

Hallo **Create App Service** dialoogvenster wordt weergegeven met standaardwaarden. aantal Hallo **170602185241** wordt weergegeven in volgende Hallo in het dialoogvenster van uw installatiekopie verschilt.

![Het dialoogvenster App Service maken](./media/app-service-web-get-started-java/cas1.png)

In Hallo **Create App Service** in het dialoogvenster:

* Houd naam voor de web-app Hallo Hallo gegenereerd. Deze naam moet uniek zijn binnen Azure. Hallo-naam is onderdeel van de URL-adres voor de web-app Hallo Hallo. Bijvoorbeeld: als de web-appnaam hello **MyJavaWebApp**, Hallo-URL is *myjavawebapp.azurewebsites.net*.
* Houd Hallo standaard webcontainer.
* Selecteer een Azure-abonnement.
* Op Hallo **App service-abonnement** tabblad:

  * **Maken van nieuwe**: gebruik Hallo standaardwaarde Hallo-naam van Hallo App Service-abonnement.
  * **Locatie**: selecteer **West-Europa** of een locatie bij u in de buurt.
  * **Prijscategorie**: Selecteer Hallo gratis optie. Voor een functiebeschrijving zie [App Service-prijzen](https://azure.microsoft.com/pricing/details/app-service/).

   ![Het dialoogvenster App Service maken](./media/app-service-web-get-started-java/create-app-service-dialog-box.png)

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

### <a name="resource-group-tab"></a>Het tabblad Resourcegroep

Selecteer Hallo **resourcegroep** tabblad. Hallo standaard gegenereerde waarde voor de resourcegroep Hallo behouden.

![Het tabblad Resourcegroep](./media/app-service-web-get-started-java/create-app-service-resource-group.png)

[!INCLUDE [resource-group](../../includes/resource-group.md)]

Selecteer **Maken**.

<!--
### hello JDK tab

Select hello **JDK** tab. Keep hello default, and then select **Create**.

![Create App Service plan](./media/app-service-web-get-started-java/create-app-service-specify-jdk.png)
-->

Hello Azure Toolkit Hallo web-app maakt en geeft een dialoogvenster uitgevoerd.

![Het voortgangsvenster voor het maken van een App Service](./media/app-service-web-get-started-java/create-app-service-progress-bar.png)

### <a name="deploy-web-app-dialog-box"></a>Het dialoogvenster Web-app implementeren

In Hallo **Web-App implementeren** dialoogvenster, **tooroot implementeren**. Als u hebt een app-service op *wingtiptoys.azurewebsites.net* en implementeert u geen toohello root, Hallo web-app met de naam **MyFirstJavaOnAzureWebApp** te wordt geïmplementeerd *wingtiptoys.azurewebsites.net/MyFirstJavaOnAzureWebApp*.

![Het dialoogvenster Web-app implementeren](./media/app-service-web-get-started-java/deploy-web-app-to-root.png)

Hallo dialoogvenster vak geeft hello Azure, JDK en web container selecties.

Selecteer **implementeren** tooAzure toopublish Hallo web-app.

Wanneer het Hallo-publiceren is voltooid, selecteert u Hallo **gepubliceerde** koppeling in Hallo **Azure Activity Log** in het dialoogvenster.

![Het dialoogvenster Azure-activiteitenlogboek](./media/app-service-web-get-started-java/aal.png)

Gefeliciteerd. U hebt uw tooAzure web-app is geïmplementeerd. 

!['Hello Azure'! voorbeeld van web-app](./media/app-service-web-get-started-java/browse-web-app-1.png)

## <a name="update-hello-web-app"></a>Hallo-web-app bijwerken

Hallo JSP code tooa verschillende voorbeeldbericht wijzigen.

```jsp
<body>
<h1><% out.println("Hello again Azure!"); %></h1>
</body>
```

Hallo wijzigingen opslaan.

In Projectverkenner met de rechtermuisknop op het Hallo-project en selecteer vervolgens **Azure** > **publiceren als Azure-Web-App**.

Hallo **Web-App implementeren** in het dialoogvenster wordt weergegeven en toont Hallo-app service die u eerder hebt gemaakt. 

> [!NOTE]
> Selecteer **tooroot implementeren** telkens wanneer u publiceert.
>

Hallo-web-app selecteren en selecteer **implementeren**, die Hallo wijzigingen publiceert.

Wanneer Hallo **Publishing** koppeling wordt weergegeven, selecteert u deze toobrowse toohello web-app en Hallo wijzigingen zien.

## <a name="manage-hello-web-app"></a>Hallo-web-app beheren

Ga toohello <a href="https://portal.azure.com" target="_blank">Azure-portal</a> toosee Hallo web-app die u hebt gemaakt.

Selecteer in het linkermenu Hallo **resourcegroepen**.

![Navigatie in de portal tooresource groepen](media/app-service-web-get-started-java/rg.png)

Selecteer Hallo resourcegroep. Hallo pagina weergegeven Hallo-resources die u hebt gemaakt in deze snelstartgids.

![Resourcegroep myResourceGroup](media/app-service-web-get-started-java/rg2.png)

Selecteer Hallo web-app (**webapp 170602193915** in Hallo voorgaande afbeelding).

Hallo **overzicht** pagina wordt weergegeven. Deze pagina kunt u een overzicht van hoe Hallo app doet. Hier kunt u algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw starten en verwijderen. Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuraties die u kunt openen. 

![App Service-pagina in Azure Portal](media/app-service-web-get-started-java/web-app-blade.png)

[!INCLUDE [clean-up-section-portal-web-app](../../includes/clean-up-section-portal-web-app.md)]

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Aangepast domein toewijzen](app-service-web-tutorial-custom-domain.md)

---
title: aaaContinuous implementatie tooAzure App Service | Microsoft Docs
description: Meer informatie over hoe tooenable continue implementatie tooAzure App Service.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a>Doorlopende implementatie tooAzure App Service
Deze zelfstudie leert u hoe tooconfigure een werkstroom continue implementatie voor uw [Azure App Service] app. App Service-integratie met BitBucket, GitHub en [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) kunnen een continue implementatiewerkstroom waarbij Azure in de meest recente updates Hallo van uw project ophaalt gepubliceerd tooone van deze services. Continue implementatie is een goede optie voor projecten waar meerdere en regelmatige bijdragen worden geïntegreerd.

toofind uit hoe tooconfigure continue implementatie handmatig van een cloud-opslagplaats niet vermeld in Azure Portal Hallo (zoals [GitLab](https://gitlab.com/)), Zie [instellen van continue implementatie met handmatige stappen](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).

## <a name="overview"></a>Continue implementatie inschakelen
doorlopende implementatie tooenable,

1. Publiceer de app inhoud toohello opslagplaats die wordt gebruikt voor continue implementatie.  
    Zie voor meer informatie over het publiceren van uw project toothese services [maken van een opslagplaats (GitHub)], [maken van een opslagplaats (BitBucket)], en [aan de slag met VSTS].
2. In de blade van uw app-menu in Hallo [Azure-portal], klikt u op **APP-implementatie > implementatieopties**. Klik op **bron kiezen**, selecteer vervolgens de implementatiebron Hallo.  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > een account VSTS voor App Service-implementatie tooconfigure raadpleegt u dit [zelfstudie](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).
   > 
   > 
3. Hallo autorisatie werkstroom voltooien.
4. In Hallo **implementatiebron** blade Hallo project kiezen en vertakken toodeploy uit. Wanneer u klaar bent, klikt u op **OK**.
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > Wanneer u continue implementatie met GitHub of BitBucket inschakelt, worden openbare en particuliere projecten weergegeven.
   > 
   > 
   
    App Service een koppeling met de geselecteerde opslagplaats Hallo maakt, worden opgehaald in het Hallo-bestanden van de opgegeven vertakking Hallo en onderhoudt een kloon van de opslagplaats voor uw App Service-app. Bij het configureren van VSTS continue implementatie van Azure-portal Hallo Hallo integratie Hallo App Service gebruikt [implementatie-engine Kudu](https://github.com/projectkudu/kudu/wiki), die al automatiseert het build- en taken met elke `git push`. U hoeft geen tooseparately doorlopende implementatie in VSTS ingesteld. Nadat dit proces is voltooid, hello **implementatieopties** blade app wordt weergegeven met een actieve implementatie waarmee implementatie is geslaagd.
5. tooverify hello app is geïmplementeerd, klikt u op Hallo **URL** Hallo boven aan de blade Hallo-app in hello Azure-portal.
6. tooverify continue implementatie plaatsvindt uit Hallo opslagplaats van uw keuze, een wijziging toohello opslagplaats pushen. Uw app moet tooreflect Hallo wijzigingen bijwerken kort nadat Hallo push toohello opslagplaats is voltooid. U kunt controleren of in de update in Hallo Hallo heeft getrokken **implementatieopties** blade van uw app.

## <a name="VSsolution"></a>Continue implementatie van een Visual Studio-oplossing
Een Visual Studio-oplossing tooAzure App Service pushen is net zo gemakkelijk een eenvoudige index.html bestand pushen. Hallo-App Service-implementatieproces stroomlijnt alle Hallo-informatie, zoals NuGet afhankelijkheden herstellen en het bouwen van de binaire bestanden Hallo van toepassingen. U kunt Volg Hallo bron besturingselement aanbevolen procedures van het onderhouden van de code alleen in de Git-opslagplaats en kunt App Service-implementatie zorgt voor Hallo rest.

Hallo stappen voor het pushen van uw Visual Studio-oplossing tooApp Service zijn Hallo hetzelfde als in Hallo [vorige sectie](#overview), mits u de oplossing en de opslagplaats als volgt configureren:

* Hallo Visual Studio bron besturingselement optie toogenerate gebruiken een `.gitignore` bestand zoals Hallo installatiekopie hieronder of Voeg handmatig een `.gitignore` bestand in de hoofdmap van uw opslagplaats met inhoud vergelijkbare toothis [.gitignore voorbeeld](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* Hallo hele oplossing directory structuur tooyour opslagplaats met Hallo .sln-bestand in de hoofdmap van de opslagplaats Hallo toevoegen.

Zodra u hebt uw opslagplaats zoals is beschreven instellen en uw app in Azure geconfigureerd voor continue publicatie van een van de online Git-opslagplaatsen hello, kunt u uw ASP.NET-toepassing lokaal in Visual Studio ontwikkelen en continu uw code gewoon door implementeren uw wijzigingen tooyour online Git-opslagplaats pushen.

## <a name="disableCD"></a>Continue implementatie uitschakelen
doorlopende implementatie toodisable,

1. In de blade van uw app-menu in Hallo [Azure-portal], klikt u op **APP-implementatie > implementatieopties**. Klik vervolgens op **Disconnect** in Hallo **implementatieopties** blade.
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. Na het beantwoorden van **Ja** toohello bevestigingsbericht die u kunt retourneren blade tooyour-app en klik op **APP-implementatie > implementatieopties** indien tooset van publicatie van een andere bron gewenst.

## <a name="additional-resources"></a>Aanvullende resources
* [Hoe tooinvestigate algemene problemen met een continue implementatie](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* [Hoe toouse PowerShell voor Azure]
* [Hoe toouse Azure opdrachtregelprogramma's Hallo voor Mac en Linux]
* [Git-documentatie]
* [Project Kudu](https://github.com/projectkudu/kudu/wiki)
* [Gebruik Azure tooautomatically genereren een CI/CD pijplijn toodeploy een ASP.NET-4-app](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure-portal]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Hoe toouse PowerShell voor Azure]: /powershell/azureps-cmdlets-docs
[Hoe toouse Azure opdrachtregelprogramma's Hallo voor Mac en Linux]:../cli-install-nodejs.md
[Git-documentatie]: http://git-scm.com/documentation

[maken van een opslagplaats (GitHub)]: https://help.github.com/articles/create-a-repo
[maken van een opslagplaats (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[aan de slag met VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview

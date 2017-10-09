---
title: aaaDeployment Veelgestelde vragen voor Azure-web-apps | Microsoft Docs
description: Toofrequently van antwoorden op veelgestelde vragen over de implementatie voor de functie Web Apps Hallo van Azure App Service worden opgehaald.
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Veelgestelde vragen implementatie voor Web-Apps in Azure

In dit artikel is toofrequently van antwoorden op veelgestelde vragen (FAQ's) over problemen bij de implementatie voor Hallo [functie van Azure App Service Web Apps](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Ik ben net aan de slag met App Service-web-apps. Hoe kan ik mijn code publiceren?

Hier zijn enkele mogelijkheden voor het publiceren van uw web-app-code:

*   Implementeren met behulp van Visual Studio. Als u Visual Studio-oplossing Hallo hebt, met de rechtermuisknop op Hallo web application-project en selecteer vervolgens **publiceren**.
*   Implementeren met behulp van een FTP-client. In hello Azure-portal, download Hallo publicatieprofiel voor Hallo web-app die u toodeploy uw code wilt. Vervolgens kunt u uploaden Hallo bestanden too\site\wwwroot met Hallo dezelfde profiel FTP referenties publiceren.

Zie voor meer informatie [implementeren van uw app tooApp Service](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Er wordt een foutbericht weergegeven wanneer ik probeer toodeploy vanuit Visual Studio. Hoe kan ik dit oplossen?

Als Hallo volgende bericht wordt weergegeven, kunt u een oudere versie van Hallo SDK: ' Fout tijdens de implementatie voor resource 'YourResourceName' in de resourcegroep 'YourResourceGroup': MissingRegistrationForLocation: Hallo-abonnement is niet geregistreerd voor Hallo resource Typ 'onderdelen' Hallo locatie 'VS-midden'. Registreer opnieuw voor deze provider op volgorde toohave toegang toothis locatie." 

tooresolve deze fout, upgrade toohello [nieuwste SDK](https://azure.microsoft.com/downloads/). Als dit bericht wordt weergegeven en u hebt de nieuwste SDK hello, indienen ondersteuning aan te vragen.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Hoe kan ik een ASP.NET-toepassing in Visual Studio tooApp Service implementeren?
<a id="deployasp"></a>

Hallo-zelfstudie [uw eerste ASP.NET-web-app maken in Azure binnen vijf minuten](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) ziet u hoe web toodeploy een ASP.NET-toepassing tooa web-app in App Service met behulp van Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Wat zijn de verschillende soorten implementatiereferenties Hallo?

App Service ondersteunt twee typen van referenties voor de FTP-/ S-implementatie en lokale Git-implementatie. Voor meer informatie over het tooconfigure implementatiereferenties, Zie [referenties voor implementatie van App Service configureert](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>Wat is Hallo-bestand of map structuur van mijn App Service-web-app?

Zie voor meer informatie over de bestandsstructuur Hallo van uw App Service-app [structure-bestand in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Hoe los ik 'FTP-fout 550 - er is niet voldoende ruimte op schijf Hallo' wanneer ik tooFTP mijn bestanden proberen?

Als u dit bericht ziet, is het waarschijnlijk dat u in een schijfquotum in Hallo service-abonnement voor uw web-app uitvoert. Mogelijk moet u tooscale up tooa hogere servicelaag op basis van uw behoeften schijf. Zie voor meer informatie over prijzen voor plannen en limieten voor [App Service-prijzen](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>Hoe stel ik continue implementatie in voor mijn App Service-web-app?

U kunt continue implementatie van verschillende bronnen, met inbegrip van Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox en andere Git-opslagplaatsen instellen. Deze opties zijn beschikbaar in Hallo-portal. [Doorlopende implementatie tooApp Service](app-service-continuous-deployment.md) is een handig zelfstudie waarin wordt uitgelegd hoe tooset van continue implementatie.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>Hoe los ik problemen met continue implementatie van GitHub en Bitbucket

Zie voor meer informatie over het onderzoeken van problemen met continue implementatie van GitHub of Bitbucket [onderzoeken continue implementatie](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>Ik kan geen FTP-site toomy en publiceren van mijn code. Hoe kan ik dit oplossen?

tooresolve FTP problemen:

1. Controleer of dat u de juiste hostnaam Hallo en referenties invoert. Voor gedetailleerde informatie over de verschillende soorten referenties en hoe toouse die ze zien [implementatiereferenties](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Controleer of Hallo FTP-poorten worden niet geblokkeerd door een firewall. Hallo-poorten moeten deze instellingen hebben:
    * Verbindingspoort voor FTP-besturingselement: 21
    * FTP-gegevenspoort voor verbinding: 989, 10001 10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>Hoe kan ik mijn code tooApp Service publiceren?

Hello Azure Quickstart is ontworpen toohelp u uw app implementeert met behulp van Hallo implementatie stack en methode van uw keuze. toouse hello snelstartgids in hello Azure-portal te gaan**instellingen** > **App-implementatie**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Waarom mijn app soms starten na de implementatie tooApp Service?

Zie toolearn over Hallo omstandigheden waaronder de implementatie van een toepassing tot een herstart leiden kan [implementatie versus runtime problemen](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Als Hallo artikel wordt beschreven, implementeert u App Service bestanden toohello wwwroot-map. Het start rechtstreeks nooit uw app.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Hoe ik code van de Visual Studio Team Services integreren met App Service?

U hebt twee opties voor het gebruik van continue implementatie met Visual Studio Team Services:

*   Gebruik een Git-project. Verbinding maken via App Service met behulp van Hallo implementatieopties voor die opslagplaats.
*   Een project Team Foundation versie besturingselement (TFVC) gebruiken. Implementeren met behulp van Hallo build-agent voor App Service.

Code continue implementatie voor deze beide opties zijn afhankelijk van bestaande developer-werkstromen en in-procedures. Zie voor meer informatie in deze artikelen: 

*   [Continue implementatie van uw app tooan Azure-website](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Een Visual Studio Team Services-account instellen zodat deze tooa web-app kunt implementeren](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>Hoe gebruik ik FTP of FTPS toodeploy mijn tooApp app Service?

Zie voor meer informatie over het gebruik van de FTP- of FTPS toodeploy het tooApp in uw web-app Service, [de tooApp van uw app Service implementeren met behulp van FTP/S](app-service-deploy-ftp.md).

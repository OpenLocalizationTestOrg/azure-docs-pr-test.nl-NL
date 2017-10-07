---
title: aaaConfigure Azure functie App-instellingen | Microsoft Docs
description: Meer informatie over hoe de app-instellingen voor het functioneren van tooconfigure Azure.
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Hoe toomanage een functie-app in hello Azure-portal 

In de Azure Functions biedt een functie-app Hallo uitvoeringscontext voor uw afzonderlijke functies. De functie app-gedrag van toepassing tooall functies gehost door een bepaalde functie-app. Dit onderwerp wordt beschreven hoe tooconfigure en beheren van uw apps functie in hello Azure-portal.

toobegin, Ga toohello [Azure-portal](http://portal.azure.com) en meld u aan tooyour Azure-account. In de zoekbalk Hallo Hallo boven aan het Hallo-portal, typ Hallo-naam van de functie-app en selecteren in lijst Hallo. Na het selecteren van de functie-app, ziet u Hallo na pagina:

![Overzicht van de functie-app in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Tabblad voor de functie app-instellingen

![Overzicht van de functie app in hello Azure-portal.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Hallo **instellingen** tabblad is waarin u Hallo functies runtime-versie die wordt gebruikt door de functie-app kunt bijwerken. Het is ook waar u Hallo host sleutels die worden gebruikt toorestrict HTTP tooall toegangsfuncties gehost door Hallo functie-app beheren.

Functies ondersteunt zowel verbruik die als host fungeert als App Service-hostingplannen. Zie voor meer informatie [Kies Hallo juiste service-plan voor Azure Functions](functions-scale.md). Voor betere voorspelbaarheid van Hallo verbruik plan functies kunt u platform-gebruik beperken door een dagelijkse gebruiksquotum instellen in gigabytes seconden. Zodra de dagelijkse gebruiksquotum Hallo is bereikt, is Hallo functie-app gestopt. Een functie-app gestopt als gevolg van Hallo uitgaven quotum bereikt kan opnieuw worden ingeschakeld vanuit Hallo worden dezelfde context als dagelijks uitgaven quotum Hallo tot stand brengen. Zie Hallo [Azure Functions pagina met prijzen](http://azure.microsoft.com/pricing/details/functions/) voor meer informatie over de facturering.   

## <a name="platform-features-tab"></a>Tabblad voor platform-onderdelen

![De functie app platform functies tabblad.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Functie apps in uitgevoerd en worden beheerd, door hello Azure App Service-platform. Als zodanig hebben uw apps functie toegang toomost van Hallo functies van Azure core webhosting-platform. Hallo **platformfuncties** tabblad is waar u de toegang tot veel functies van App Service-platform die u in uw apps functie gebruiken kunt Hallo Hallo. 

> [!NOTE]
> Niet alle App Service-functies zijn beschikbaar wanneer een functie-app wordt uitgevoerd op Hallo verbruik hosting plan.

Hallo rest van dit onderwerp richt zich op Hallo na App Service-functies in hello Azure-portal die handig zijn voor functies:

+ [App Service-editor](#editor)
+ [Toepassingsinstellingen](#settings) 
+ [Console](#console)
+ [Geavanceerde tools (Kudu)](#kudu)
+ [Implementatie-opties](#deployment)
+ [CORS](#cors)
+ [Verificatie](#auth)
+ [API-definitie](#swagger)

Voor meer informatie over het toowork met App Service-instellingen, Zie [Azure App Service-instellingen configureren](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>App Service-Editor

| | |
|-|-|
| ![De functie app-App Service-editor.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Hallo-App Service-editor is een geavanceerde in de portal-editor die u toomodify JSON-configuratiebestanden en codebestanden hetzelfde gebruiken kunt. Als u deze optie kiest, wordt een afzonderlijke browsertabblad met een basic-editor gestart. Dit kunt u toointegrate met Hallo Git-opslagplaats, uitvoeren en foutopsporing code en de functie app-instellingen wijzigen. Deze editor biedt een verbeterde development environment voor uw functies vergeleken met de blade Hallo standaard functie-app.    |

![Hallo-App Service-editor](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Toepassingsinstellingen

| | |
|-|-|
| ![Toepassingsinstellingen voor functie-app.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Hallo-App Service **toepassingsinstellingen** blade is waar u configureren en beheren van de framework-versies, foutopsporing op afstand, app-instellingen en verbindingsreeksen. Wanneer u de functie-app met andere Azure en services van derden integreren, kunt u deze instellingen hier wijzigen. |

![Configureer toepassingsinstellingen](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Console

| | |
|-|-|
| ![De functie app-console in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | Hallo-portal-console is een hulpprogramma ideaal ontwikkelaar wanneer u toointeract met uw app functie vanaf de opdrachtregel Hallo liever. Veelgebruikte opdrachten zijn directory en maken van het bestand en navigatie, evenals batch-bestanden en scripts uitvoeren. |

![De functie app-console](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Geavanceerde tools (Kudu)

| | |
|-|-|
| ![Functie-app Kudu in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Hallo bieden geavanceerde hulpprogramma's voor App Service (ook wel bekend als Kudu) toegang tooadvanced beheerfuncties van uw app functie. U beheert van kudu bovendien, systeemgegevens, app-instellingen, omgevingsvariabelen, site-uitbreidingen, HTTP-headers en servervariabelen. U kunt ook starten **Kudu** door te bladeren toohello SCM-eindpunt voor de functie-app, zoals`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Kudu configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Implementatie-opties

| | |
|-|-|
| ![Opties voor de functie app-implementatie in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Functies kunt u uw functiecode op uw lokale machine ontwikkelen. Vervolgens kunt u uw lokale functie app-project tooAzure uploaden. Bovendien tootraditional FTP uploaden, functies kunt u de functie-app met behulp van populaire continue integratie-oplossingen, zoals GitHub, VSTS Dropbox, Bitbucket en anderen implementeren. Zie voor meer informatie [continue implementatie voor Azure Functions](functions-continuous-deployment.md). tooupload handmatig met behulp van FTP- of lokale Git, moet u [configureren van de referenties voor uw implementatie](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Functie-app CORS in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | tooprevent schadelijke code wordt uitgevoerd in uw services, App-Service blokkeert roept tooyour functie apps uit externe bronnen. Functies biedt ondersteuning voor cross-origin-resource delen (CORS) toolet u een 'whitelist definieert' toegestane oorsprongen waarvan van uw functies kunnen externe aanvragen accepteert.  |

![Functie-App configureren CORS](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Verificatie

| | |
|-|-|
| ![Verificatie van de functie-app in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Wanneer functies een HTTP-trigger te gebruiken, kunt u ook vragen oproepen toofirst worden geverifieerd. App Service biedt ondersteuning voor Azure Active Directory-verificatie en meld u aan met sociale providers, zoals Microsoft, Facebook en Twitter. Zie voor meer informatie over het configureren van specifieke verificatieproviders [overzicht van Azure App Service-authenticatie](../app-service/app-service-authentication-overview.md). |

![Verificatie voor een functie-app configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>API-definitie

| | |
|-|-|
| ![De functie app API swagger-definitie in hello Azure-portal](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Functions ondersteunt Swagger tooallow clients toomore eenvoudig uw HTTP-geactiveerde functies gebruiken. Bezoek voor meer informatie over het maken van API-definities met Swagger [aan de slag met API-Apps, ASP.NET en Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md). U kunt ook functies proxy's toodefine één API-gebied voor meerdere functies. Zie voor meer informatie [werken met Azure Functions-proxy's](functions-proxies.md). |

![API voor functie-App configureren](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Volgende stappen

+ [Azure App Service-instellingen configureren](../app-service-web/web-sites-configure.md)
+ [Doorlopende implementatie voor Azure Functions](functions-continuous-deployment.md)




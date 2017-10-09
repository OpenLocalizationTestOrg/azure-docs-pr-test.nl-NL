---
title: aaaDeploy uw app tooAzure met FTP/S-App Service | Microsoft Docs
description: Meer informatie over hoe toodeploy uw app tooAzure App Service met behulp van de FTP- of FTPS.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: ae78b410-1bc0-4d72-8fc4-ac69801247ae
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2016
ms.author: cephalin;dariac
ms.openlocfilehash: 318ae79d4fae269f853ea5c3ce28353b0864131e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-tooazure-app-service-using-ftps"></a>Uw app tooAzure met FTP/S-App Service implementeren

Dit artikel ziet u hoe toouse FTP of toodeploy uw web-app, back-end voor mobiele app of API-app te FTPS[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Hallo FTP-/ S-eindpunt voor uw app is al actief. Implementatie van benodigde tooenable FTP-/ S, is geen configuratie.

> [!IMPORTANT]
> We nemen continu stappen tooimprove beveiliging van Microsoft Azure-Platform. Als onderdeel van deze continue inspanningen is een upgrade van webtoepassingen gepland voor Duitsland centraal en Duitsland noordoosten regio's. Gedurende deze heeft Web-Apps uitschakelen Hallo gebruik van tekst zonder opmaak FTP-protocol voor implementaties. Onze aanbeveling tooour klanten is tooswitch tooFTPS voor implementaties. We verwachten niet elke tooyour-service wordt onderbroken tijdens deze upgrade die is gepland voor 9/5. Bedankt dat je hebt in deze inspanningen ondersteunen.

<a name="step1"></a>
## <a name="step-1-set-deployment-credentials"></a>Stap 1: Stel de referenties voor implementatie

tooaccess hello FTP-server voor uw app, moet u eerst referenties voor implementatie. 

tooset of opnieuw instellen van de implementatiereferenties van uw, Zie [referenties voor de Azure App Service-implementatie](app-service-deployment-credentials.md). Deze zelfstudie wordt gedemonstreerd Hallo gebruik van beveiliging op gebruikersniveau referenties.

## <a name="step-2-get-ftp-connection-information"></a>Stap 2: Gegevens van de FTP-verbinding ophalen

1. In Hallo [Azure-portal](https://portal.azure.com), opent u uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources).
2. Selecteer **overzicht** in het linkermenu Hallo, bekijk Hallo waarden voor **FTP-/ Implementatiegebruiker gebruiker**, **FTP-hostnaam**, en **FTPS hostnaam**. 

    ![FTP-verbindingsgegevens](./media/web-sites-deploy/FTP-Connection-Info.PNG)

    > [!NOTE]
    > Hallo **FTP-/ Implementatiegebruiker gebruiker** waarde van de gebruiker, zoals weergegeven door hello Azure Portal, met inbegrip van app-naam Hallo in volgorde tooprovide juiste context voor Hallo FTP-server.
    > U vindt Hallo dezelfde informatie wanneer u selecteert **eigenschappen** in het linkermenu Hallo. 
    >
    > Hallo implementatie wachtwoord wordt nooit weergegeven. Als u uw implementatie wachtwoord bent vergeten, gaat u terug te[stap 1](#step1) en uw implementatie-wachtwoord opnieuw instellen.
    >
    >

## <a name="step-3-deploy-files-tooazure"></a>Stap 3: Bestanden tooAzure implementeren

1. Van uw FTP-client ([Visual Studio](https://www.visualstudio.com/vs/community/), [FileZilla](https://filezilla-project.org/download.php?type=client), enzovoort), Hallo verbindingsgegevens verzameld van tooconnect tooyour app gebruiken.
3. Kopieer de bestanden en hun respectieve directory structuur toohello [ **/site/wwwroot** directory](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure) in Azure (of Hallo **/site/wwwroot/App_Data/taken/** map voor WebJobs).
4. Bladeren tooyour app-URL tooverify Hallo app wordt correct uitgevoerd. 

> [!NOTE] 
> In tegenstelling tot [implementaties op basis van Git](app-service-deploy-local-git.md), FTP-implementatie biedt geen ondersteuning voor hello automatische implementatie te volgen: 
>
> - afhankelijkheid herstellen (zoals NuGet, NPM, PIP en Composer automatische)
> - compilatie van binaire bestanden voor .NET
> - generatie van web.config (dit is een [Node.js-voorbeeld](https://github.com/projectkudu/kudu/wiki/Using-a-custom-web.config-for-Node-apps))
> 
> U moet herstellen, maken, en deze vereiste bestanden handmatig op uw lokale machine genereren en deze samen met uw app te implementeren.
>
>

## <a name="next-steps"></a>Volgende stappen

Probeer meer geavanceerde implementatiescenario's voor [tooAzure met Git implementeren](app-service-deploy-local-git.md). Implementatie op basis van GIT tooAzure kunt versiebeheer, pakket herstellen en MSBuild.

## <a name="more-resources"></a>Meer bronnen

* [Een PHP-MySQL web-app maken en implementeren met FTP](web-sites-php-mysql-deploy-use-ftp.md).
* [Referenties voor Azure App Service-implementatie](app-service-deploy-ftp.md)

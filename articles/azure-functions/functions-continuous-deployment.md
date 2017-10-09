---
title: aaaContinuous-implementatie voor Azure Functions | Microsoft Docs
description: Doorlopende implementatie faciliteiten van Azure App Service-toopublish uw Azure-functies gebruiken.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
ms.assetid: 361daf37-598c-4703-8d78-c77dbef91643
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/25/2016
ms.author: glenga
ms.openlocfilehash: 28c44f737dad3feab3cf54f7dd42b6a978d0617e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-for-azure-functions"></a>Doorlopende implementatie voor Azure Functions
Azure Functions maakt het eenvoudig toodeploy uw functie-app met App Service continue integratie. Functions integreert met BitBucket, Dropbox, GitHub en Visual Studio Team Services (VSTS). Hierdoor wordt een werkstroom waar functiecode updates uitgevoerd met behulp van een van deze geïntegreerde services trigger implementatie tooAzure. Als u nieuwe functies voor tooAzure, beginnen met [overzicht van Azure Functions](functions-overview.md).

Continue implementatie is een goede optie voor projecten waar meerdere en regelmatige bijdragen worden geïntegreerd. U kunt ook broncodebeheer op uw code functies onderhouden. de volgende bronnen voor implementatie Hallo worden momenteel ondersteund:

* [Bitbucket](https://bitbucket.org/)
* [Dropbox](https://www.dropbox.com/)
* Externe opslagplaats (Git of volgt)
* [Lokale GIT-opslagplaats](../app-service-web/app-service-deploy-local-git.md)
* [GitHub](https://github.com)
* [OneDrive](https://onedrive.live.com/)
* [Visual Studio Team Services](https://www.visualstudio.com/team-services/)

Implementaties worden geconfigureerd op basis van de app per functie. Nadat de doorlopende implementatie is ingeschakeld, toofunction toegangscode in Hallo-portal te ingesteld*alleen-lezen*.

## <a name="continuous-deployment-requirements"></a>Vereisten voor de doorlopende implementatie

In de implementatiebron Hallo voordat u continue implementatie instellen, moet u uw implementatiebron geconfigureerd en uw code functies hebben. Elke functie woont in een bepaalde functie app-implementatie in een benoemde submap, waarbij de mapnaam Hallo Hallo naam van Hallo-functie is.  

[!INCLUDE [functions-folder-structure](../../includes/functions-folder-structure.md)]

## <a name="set-up-continuous-deployment"></a>Doorlopende implementatie instellen
Gebruik deze procedure tooconfigure continue implementatie voor een bestaande functie-app. Deze stappen laten zien integratie met een GitHub-opslagplaats, maar gelijksoortige stappen gelden voor Visual Studio Team Services of andere implementatieservices.

1. In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatieopties**. 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Klik dan in Hallo **implementaties** Klik op de blade **Setup**.
 
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. In Hallo **implementatiebron** blade, klikt u op **bron kiezen**, vul vervolgens Hallo-informatie voor uw gekozen implementatiebron en klikt u op **OK**.
   
    ![Implementatiebron kiezen](./media/functions-continuous-deployment/choose-deployment-source.png)

Nadat de doorlopende implementatie is geconfigureerd, alle bestandswijzigingen in de implementatiebron-zijn gekopieerde toohello functie-app en een volledige site-implementatie wordt geactiveerd. Hallo-site is opnieuw geïmplementeerd wanneer bestanden in de broninhoud Hallo zijn bijgewerkt.

## <a name="deployment-options"></a>Implementatieopties

Hallo Hieronder volgen enkele typische implementatiescenario's:

- [Een gefaseerde installatie implementatie maken](#staging)
- [Verplaatsen van bestaande functies toocontinuous implementatie](#existing)

<a name="staging"></a>
### <a name="create-a-staging-deployment"></a>Een gefaseerde installatie implementatie maken

Functie Apps ondersteunt nog geen implementatiesites. U kunt echter nog steeds afzonderlijke fasering en productie-implementaties beheren met behulp van continue integratie.

Hallo proces tooconfigure en werken met een gefaseerde installatie-implementatie in het algemeen zien er zo uit:

1. Maak twee functie apps in uw abonnement, één voor de productiecode Hallo en één voor fasering. 

2. Maak een implementatiebron als u er nog geen hebt. In dit voorbeeld wordt [GitHub].

3. Voor uw app van de functie productie voltooid Hallo voorgaande stappen in **continue implementatie instellen** en set Hallo implementatie vertakking toohello hoofdvertakking van uw GitHub-opslagplaats.
   
    ![Vertakking implementatie kiezen](./media/functions-continuous-deployment/choose-deployment-branch.png)

4. Herhaal deze stap voor Hallo staging-functie-app, maar Hallo vertakking in plaats daarvan fasering in uw GitHub-repo kiezen. Als de implementatiebron-biedt geen ondersteuning voor vertakking, gebruikt u een andere map.
    
5. Controleer updates tooyour code in Hallo vertakking of de map voor gefaseerde installatie en controleer of dat deze wijzigingen zijn doorgevoerd in Hallo staging-implementatie.

6. Nadat u hebt getest, wijzigingen van de staging-vertakking naar de hoofdvertakking Hallo Hallo samen te voegen. Deze samenvoegen triggers implementatie toohello productie functie-app. Als de implementatiebron-biedt geen ondersteuning voor filialen, met Hallo-bestanden van de map voor gefaseerde installatie Hallo worden Hallo-bestanden in Hallo productie map overschreven.

<a name="existing"></a>
### <a name="move-existing-functions-toocontinuous-deployment"></a>Verplaatsen van bestaande functies toocontinuous implementatie
Wanneer u bestaande functies die u hebt gemaakt en onderhouden in Hallo-portal, moet u toodownload uw bestaande functioneren codebestanden FTP of Hallo lokale Git-opslagplaats met voordat u continue implementatie instellen kunt zoals hierboven is beschreven. U kunt dit doen in Hallo App Service-instellingen voor de functie-app. Nadat de bestanden zijn gedownload, kunt u ze tooyour gekozen continue implementatiebron uploaden.

> [!NOTE]
> Nadat u continue integratie configureert, langer u niet kunnen tooedit uw in Hallo Functions-portal bronbestanden.

- [Hoe: Configureer de referenties voor implementatie](#credentials)
- [Hoe: downloaden van bestanden met FTP](#downftp)
- [Hoe: downloaden van bestanden met Hallo lokale Git-opslagplaats](#downgit)

<a name="credentials"></a>
#### <a name="how-to-configure-deployment-credentials"></a>Hoe: Configureer de referenties voor implementatie
Voordat u bestanden van de functie-app met FTP- of lokale Git-opslagplaats downloaden kunt, moet u uw referenties tooaccess Hallo site configureren. Referenties worden ingesteld op Hallo functie app-niveau. Gebruik Hallo stappen tooset implementatiereferenties in hello Azure-portal te volgen:

1. In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatiereferenties**.
   
    ![Lokale implementatiereferenties instellen](./media/functions-continuous-deployment/setup-deployment-credentials.png)

2. Typ een gebruikersnaam en wachtwoord en klik vervolgens op **opslaan**. U kunt deze referenties tooaccess nu uw app in de functie van de FTP- of Hallo ingebouwde Git-opslagplaats gebruiken.

<a name="downftp"></a>
#### <a name="how-to-download-files-using-ftp"></a>Hoe: downloaden van bestanden met FTP

1. In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **eigenschappen**, kopieert u Hallo waarden voor **FTP-/ Implementatiegebruiker gebruiker**, **FTP-hostnaam**, en **FTPS hostnaam**.  

    **FTP-/ Implementatiegebruiker gebruiker** moet worden ingevoerd zoals weergegeven in de Hallo-portal, met inbegrip van Hallo app-naam, de juiste context tooprovide voor Hallo FTP-server.
   
    ![Uw implementatie-informatie ophalen](./media/functions-continuous-deployment/get-deployment-credentials.png)

2. Van uw FTP-client gebruikt Hallo verbindingsinformatie verzameld van tooconnect tooyour app en download de bronbestanden Hallo voor uw functies.

<a name="downgit"></a>
#### <a name="how-to-download-files-using-a-local-git-repository"></a>Hoe: downloaden van bestanden met behulp van een lokale Git-opslagplaats

1. In de functie-app in Hallo [Azure-portal](https://portal.azure.com), klikt u op **platformfuncties** en **implementatieopties**. 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment.png)
 
2. Klik dan in Hallo **implementaties** Klik op de blade **Setup**.
 
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/setup-deployment-1.png)
   
2. In Hallo **implementatiebron** blade, klikt u op **lokale Git-opslagplaats** en klik vervolgens op **OK**.

3. In **platformfuncties**, klikt u op **eigenschappen** en bekijkt hello waarde Git-URL. 
   
    ![Doorlopende implementatie instellen](./media/functions-continuous-deployment/get-local-git-deployment-url.png)

4. Kloon de opslagplaats Hallo op uw lokale computer met een Git-bewuste opdrachtprompt of uw favoriete Git-hulpprogramma. Hallo Git kloonopdracht ziet er als volgt:
   
        git clone https://username@my-function-app.scm.azurewebsites.net:443/my-function-app.git

5. Bestanden ophalen van de kloon van de functie app-toohello op uw lokale computer, zoals in het volgende voorbeeld Hallo:
   
        git pull origin master
   
    Als u hebt aangevraagd, geeft u uw [implementatiereferenties geconfigureerd](#credentials).  

[GitHub]: https://github.com/

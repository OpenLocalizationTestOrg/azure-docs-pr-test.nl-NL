---
title: aaaAdding Mobile Services met behulp van verbonden Services in Visual Studio | Microsoft Docs
description: Mobile Services toevoegen met behulp van Hallo Visual Studio verbonden dialoogvenster Services toevoegen
services: visual-studio-online
documentationcenter: na
author: mlhoop
manager: douge
editor: 
ms.assetid: 75c3cb93-88e1-476d-a416-f34caa3608e3
ms.service: visual-studio-online
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: mobile
ms.date: 12/16/2015
ms.author: mlearned
ms.openlocfilehash: c47b6fb63dc99fbc012e1c627c6c7e95249de7a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="adding-mobile-services-by-using-visual-studio-connected-services"></a>Mobile Services toevoegen met behulp van Visual Studio verbonden Services
Met Visual Studio 2015, kunt u tooAzure Mobile Services met behulp van Hallo **verbonden Service toevoegen** dialoogvenster. U kunt verbinding maken vanaf elke clienttoepassing C#, een JavaScript-app of platformoverschrijdende Cordova-app. Als u verbinding hebt gemaakt, kunt u maken en toegang tot gegevens, aangepaste API's en geplande taken maken of toevoegen van ondersteuning voor pushmeldingen.  Hallo voegt verbonden services bewerking alle juiste verwijzingen en code van de verbinding. U kunt ook te profiteren van ingebouwde ondersteuning voor verificatie met tal van populaire identity-schema's, zoals Azure AD, Facebook, Twitter en Microsoft-Accounts.

## <a name="supported-project-types"></a>Ondersteunde projecttypen
> [!NOTE]
> In Visual Studio 2015 wordt Azure Mobile Services tooa universele Windows-(Windows 10) projecten toe te voegen met behulp van Hallo verbonden Services toevoegen dialoogvenster niet ondersteund. U kunt Azure Mobile Services toevoegen door het installeren van de juiste hello-pakketten met Hallo NuGet Package Manager voor uw project.
> 
> 

U kunt Hallo verbonden Services dialoogvenster tooconnect tooAzure Mobile Services in de volgende projecttypen hello gebruiken.

* .NET Windows 8.1 Store en Phone universele App-projecten
* JavaScript Windows 8.1 Store en Phone universele App-projecten
* Projecten gemaakt met behulp van Visual Studio Tools voor Apache Cordova

## <a name="connect-tooazure-mobile-services-using-hello-add-connected-services-dialog"></a>Verbinding maken met tooAzure Mobile Services met Hallo verbonden Services toevoegen dialoogvenster
1. Zorg ervoor dat u hebt een Azure-account. Als u geen Azure-account hebt, kunt u zich aanmelden voor een [gratis proefversie](http://go.microsoft.com/fwlink/?LinkId=518146).
2. Open Hallo **verbonden Services toevoegen** in het dialoogvenster.
   
   * Voor .NET-toepassingen, opent u het project in Visual Studio openen Hallo contextmenu voor Hallo **verwijzingen** knooppunt in Solution Explorer en kies vervolgens **verbonden Service toevoegen**
     
        ![Verbinding maken met tooAzure Mobile Service](./media/vs-azure-tools-connected-services-add-mobile-services/IC797635.png)
   * Voor Apache Cordova-app-projecten, opent u het project in Visual Studio openen Hallo contextmenu voor Hallo projectknooppunt in Solution Explorer en kiest u **verbonden Service toevoegen**.
3. In Hallo **verbonden Service toevoegen** dialoogvenster Kies **Azure Mobile Services**, en kies vervolgens Hallo **configureren** knop. Hebt u mogelijk na vragen aan gebruiker toolog in Azure als u dat nog niet hebt gedaan.
   
    ![Toevoegen van een mobiele Service van Azure](./media/vs-azure-tools-connected-services-add-mobile-services/IC797636.png)
4. In Hallo **Azure Mobile Services** dialoogvenster Kies een bestaande mobiele service als er een. Als u een nieuwe mobiele service van Azure toocreate moet, volg u dus Hallo procedure hieronder toodo. Ga anders verder toohello volgende stap.
   
    een nieuwe mobiele serviceaccount toocreate:
   
   1. Kies Hallo ** maken van een Service ** koppeling Hallo onder in het dialoogvenster voor Hallo aan.
       ![Nieuwe mobiele service die verbonden toevoegen](./media/vs-azure-tools-connected-services-add-mobile-services/IC797637.png)
   2. Op Hallo **mobiele Service maken** in het dialoogvenster kunt u een JavaScript back-end voor mobiele service, of een mobiele service van .NET-back-end van Hallo **Runtime** vervolgkeuzelijst. 
      
       ![Een mobiele service maken](./media/vs-azure-tools-connected-services-add-mobile-services/IC797638.png)
      
       Een back-endservice JavaScript is een eenvoudige en krachtige. Als u een JavaScript back-end voor mobiele service maakt, Hallo serverzijde JavaScript-code is opgeslagen in de cloud hello, maar u kunt de server-scripts bewerken met behulp van Server Explorer of hello Azure-beheerportal. 
      
       Een .NET-back-end voor mobiele service biedt u Hallo volledige kracht en flexibiliteit van Web-API en Entity Framework. Als u een .NET-back-end voor mobiele service maakt, wordt een project voor u gemaakt en tooyour oplossing toegevoegd. 
   3. Kies Hallo **regio** waarbij Hallo mobiele service en voer vervolgens een gebruikersnaam en wachtwoord in voor het Hallo-server.
   4. Nadat u alle Hallo vereiste gegevens hebt ingevoerd, kiest u Hallo **maken** knop toocreate Hallo mobiele service.
   5. Hallo nieuwe mobiele service moet worden weergegeven in de lijst met Services op Hallo Hallo **Azure Mobile Services** in het dialoogvenster. Nieuwe mobiele service Hallo in Hallo lijst en kies Hallo **toevoegen** knop tooadd Hallo-tooyour serviceproject.
5. Bekijk introductie Hallo pagina die wordt weergegeven en weten hoe uw project is gewijzigd. Wanneer u een gekoppelde service toevoegt, verschijnt er een pagina aan de slag in uw browser. U kunt bekijken Hallo voorgestelde volgende stappen en voorbeelden van code, of schakel toohello wat is er gebeurd pagina toosee welke verwijzingen zijn tooyour project toegevoegd en hoe uw code en configuratie-bestanden die zijn aangepast.
6. Start met behulp van de codevoorbeelden Hallo als richtlijn schrijven van code tooaccess uw mobiele service!

## <a name="how-your-project-is-modified"></a>Hoe uw project is gewijzigd
Hoe uw project in Visual Studio wordt gewijzigd, is afhankelijk van het projecttype Hallo. Zie voor C# client-apps, [wat is er gebeurd – C#-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513119). Zie voor JavaScript-client-apps [wat is er gebeurd – JavaScript-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513120). Zie voor Cordova-apps [wat is er gebeurd – Cordova-projecten](http://go.microsoft.com/fwlink/p/?LinkId=513116).

## <a name="next-steps"></a>Volgende stappen
Vragen stellen en hulp te krijgen: 

* [MSDN-Forum: Azure Mobile Services](https://social.msdn.microsoft.com/forums/azure/home?forum=azuremobile)
* [Azure Mobile Services op Hallo teamblog van Microsoft Azure](https://azure.microsoft.com/blog/topics/mobile/)
* [Azure Mobile Services op azure.microsoft.com](https://azure.microsoft.com/services/mobile-services/)
* [Azure Mobile Services-documentatie op azure.microsoft.com](https://azure.microsoft.com/documentation/services/mobile-services/)


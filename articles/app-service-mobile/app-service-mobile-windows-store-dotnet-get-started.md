---
title: aaaCreate een Universal Windows Platform (UWP) die gebruikmaakt van de Mobile Apps | Microsoft Docs
description: Volg deze zelfstudie tooget gestart met behulp van back-ends voor mobiele Apps van Azure voor Universal Windows Platform (UWP)-app-ontwikkeling in C#, Visual Basic of JavaScript.
services: app-service\mobile
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 47124296-2908-4d92-85e0-05c4aa6db916
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: d0f57bca5a8195b8b0461b8f7a0d8516371d56a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-app"></a>Een Windows-app maken
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe een cloud-gebaseerde back-end tooadd tooa Universal Windows Platform (UWP)-app service. Zie [What are Mobile Apps](app-service-mobile-value-prop.md) (Wat zijn Mobile Apps?) voor meer informatie. Hallo hieronder vindt u er schermafbeeldingen worden gemaakt vanuit de app Hallo voltooid:

![Voltooide bureaublad-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed-desktop.png)   
Uitgevoerd op bureaublad.

![Voltooide telefoon-app](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)  
Uitgevoerd op telefoon.

Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor UWP-apps.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. Als u geen account hebt, kunt u zich aanmeldt voor een proefversie van Azure en krijg too10 gratis mobiele apps die u ook na de proefperiode kunt blijven gebruiken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.
* [Visual Studio Community 2015] of een nieuwere versie.

## <a name="create-a-new-azure-mobile-app-backend"></a>Een nieuwe back-end voor mobiele apps van Azure maken
Volg deze stappen toocreate een nieuwe back-end voor mobiele Apps.

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

U hebt nu een back-end voor mobiele apps van Azure ingericht, die kan worden gebruikt door uw mobiele-clienttoepassingen. Nu gaat u een serverproject voor een eenvoudige 'todo list' downloaden back-end en deze tooAzure publiceren.

## <a name="configure-hello-server-project"></a>Hallo serverproject configureren
[!INCLUDE [app-service-mobile-configure-new-backend.md](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-client-project"></a>Hallo client-project downloaden en uitvoeren
Als u uw back-end voor de mobiele App hebt geconfigureerd, kunt u een nieuwe clientapp maken of wijzigen van een bestaande app tooconnect tooAzure. In deze sectie maakt downloaden u een UWP-app-sjabloonproject dat is backend voor mobiele Apps van aangepaste tooconnect tooyour.

1. Terug in Hallo **snel starten** blade voor uw mobiele App back-end, klikt u op **maakt een nieuwe app** > **downloaden**, pak vervolgens Hallo gecomprimeerde projectbestanden tooyour lokale computer.

    ![Het project Windows-snelstartgids downloaden](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-app-windows-quickstart.png)
2. (Optioneel) Hallo UWP-app-project toohello toevoegen dezelfde oplossing als Hallo serverproject. Hiermee kunt u gemakkelijker toodebug en test beide app en Hallo back-end in Hallo Hallo dezelfde Visual Studio-oplossing als u ervoor toodo doet kiest. tooadd een UWP-app-project toohello oplossing, moet u Visual Studio 2015 of hoger.
3. Hallo UWP-app als opstartproject hello, drukt u op Hallo F5 sleutel toodeploy en Voer Hallo-app.
4. Typ in het Hallo-app zinvolle tekst, zoals *voltooid Hallo zelfstudie*, in Hallo **nieuwe taak invoegen** in het tekstvak en klik vervolgens op **opslaan**.

    ![Windows-snelstartgids: bureaublad voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-startup.png)

    Hierdoor wordt een POST-aanvraag toohello nieuwe mobiele app back-end die wordt gehost in Azure verzonden.
5. (Optioneel) Hallo app Stop en start deze opnieuw op een ander apparaat of mobiele emulator.

    ![Windows-snelstartgids: telefoon voltooien](./media/app-service-mobile-windows-store-dotnet-get-started/mobile-quickstart-completed.png)

    U ziet die gegevens opgeslagen van de vorige stap Hallo vanuit Azure geladen nadat Hallo UWP-app is gestart.

## <a name="next-steps"></a>Volgende stappen
* [Verificatie tooyour app toevoegen](app-service-mobile-windows-store-dotnet-get-started-users.md)  
  Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.
* [Push notifications tooyour app toevoegen](app-service-mobile-windows-store-dotnet-get-started-push.md)  
  Informatie over hoe tooyour app ondersteuning bieden voor pushmeldingen tooadd en pushmeldingen voor uw mobiele App back-end toouse Azure Notification Hubs toosend configureren.
* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-windows-store-dotnet-get-started-offline-data.md)  
  Meer informatie over hoe tooadd offline ondersteuning bieden voor uw app met een back-end voor de mobiele App. Offlinesynchronisatie kunnen eindgebruikers toointeract met een mobiele app&mdash;weergeven, toevoegen of wijzigen van gegevens&mdash;zelfs wanneer er geen netwerkverbinding.

<!-- Anchors. -->
<!-- Images. -->
<!-- URLs. -->
[Mobile App SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure portal]: https://portal.azure.com/
[Visual Studio Community 2015]: https://go.microsoft.com/fwLink/p/?LinkID=534203

---
title: aaaGet slag met Mobile Apps met behulp van Xamarin.Forms
description: Volg deze zelfstudie toostart met Mobile Apps voor Xamarin.Forms-ontwikkeling
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a>Een Xamarin.Forms-app maken
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a>Overzicht
Deze zelfstudie leert u hoe tooadd een back-endservice cloud-gebaseerde tooa mobiele Xamarin.Forms-app met behulp van de functie Mobile Apps van Azure App Service als de back-end Hallo Hallo. U maakt zowel een nieuwe back-end voor Mobile Apps als een eenvoudige Xamarin.Forms-app voor takenlijsten die app-gegevens opslaat in Azure.

Het voltooien van deze zelfstudie is een vereiste voor alle andere zelfstudies over Mobile Apps voor Xamarin.Forms.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie, moet u hello te volgen:

* Een actief Azure-account. Als u geen account hebt, kunt u zich aanmeldt voor een proefversie van Azure en krijg too10 gratis mobiele apps die u ook na de proefperiode kunt blijven gebruiken. Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.

* Visual Studio met Xamarin. Zie voor informatie Hallo [ingesteld omhoog en installeer Visual Studio en Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) pagina.

* Een Mac met Xcode v7.0 of hoger en waarop Xamarin Studio Community is geïnstalleerd. Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) en [Setup, install, and verifications for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (Instructies voor installatie, configuratie en verificatie voor Mac-gebruikers) (MSDN) voor meer informatie.

## <a name="create-a-new-mobile-apps-back-end"></a>Een nieuwe back-end voor Mobile Apps maken

weer een nieuwe Mobile Apps beëindigen, toocreate Hallo te volgen:

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

U hebt nu een back-end voor Mobile Apps ingesteld die uw mobiele clienttoepassingen kunnen gebruiken. Vervolgens maakt u een serverproject downloaden voor een eenvoudige taak lijst back-end en publiceer deze tooAzure.

## <a name="configure-hello-server-project"></a>Hallo serverproject configureren

tooconfigure hello server project toouse Hallo Node.js- of .NET back-end, Hallo te volgen:

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a>Hallo Xamarin.Forms-oplossing downloaden en uitvoeren

U kunt Hallo-oplossing op twee manieren downloaden. Download deze tooa Mac en openen in Xamarin Studio of download deze tooa Windows-computer en openen in Visual Studio met behulp van Mac in een netwerk voor het bouwen van Hallo iOS-app. Zie [Setup and install](https://msdn.microsoft.com/library/mt613162.aspx) (Configureren en installeren) voor meer informatie.

Op een Mac of Windows-computer, Hallo te volgen:

1. Ga toohello [Azure-portal].

2. Op Hallo **instellingen** blade voor uw mobiele app onder **Mobile**, selecteer **aan de slag** > **Xamarin.Forms**. Selecteer **Een nieuwe app maken** onder **stap 3** en selecteer vervolgens **Downloaden**.

   Deze actie een project gedownload dat een clienttoepassing bevat die is verbonden tooyour mobiele app. Hallo project gecomprimeerde bestand tooyour lokale computer opslaan en maak een notitie van de opslaglocatie.

3. Pak Hallo-project dat u hebt gedownload en open het in Xamarin Studio (Mac) of Visual Studio (Windows).

   ![Uitgepakt project in Xamarin Studio][9]

   ![Uitgepakt project in Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a>(Optioneel) Hallo iOS-project uitvoeren
In deze sectie kunt uitvoeren u Hallo Xamarin iOS-project voor iOS-apparaten. Als u niet met iOS-apparaten werkt, kunt u deze sectie overslaan.

#### <a name="in-xamarin-studio"></a>In Xamarin Studio
1. Met de rechtermuisknop op Hallo iOS-project en selecteer vervolgens **instellen als opstartproject**.

2. Op Hallo **uitvoeren** selecteert u **foutopsporing starten** toobuild Hallo project en Hallo-app in Hallo iPhone-emulator te starten.

#### <a name="in-visual-studio"></a>In Visual Studio
1. Met de rechtermuisknop op Hallo iOS-project en selecteer vervolgens **instellen als opstartproject**.

2. Op Hallo **bouwen** selecteert u **Configuration Manager**.

3. In Hallo **Configuration Manager** dialoogvenster, selecteer Hallo **bouwen** en **implementeren** selectievakjes volgende toohello iOS-project.

4. toobuild project Hallo en Hallo-app te starten in Hallo iPhone-emulator, selecteer Hallo **F5** sleutel.

   > [!NOTE]
   > Als u problemen ondervindt Hallo-project te bouwen, uitvoeren Hallo NuGet package manager en update toohello meest recente versie van Hallo Xamarin-ondersteuningspakketten. QuickStart-projecten mogelijk traag tooupdate toohello meest recente versies.    
   >
   >

5. Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en vervolgens selecteert Hallo plusteken (**+**).

    ![][10]

    Met deze actie verzendt een post-aanvraag toohello die mobiele Apps van nieuwe back-end die wordt gehost in Azure. De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo. Items die zijn opgeslagen in de tabel Hallo worden geretourneerd door Hallo Mobile Apps terug beëindigen en Hallo gegevens worden weergegeven in de lijst Hallo.

    > [!NOTE]
    > Hier vindt u Hallo-code die toegang heeft tot uw back-end van Mobile Apps in Hallo TodoItemManager.cs C#-bestand van Hallo portable class library-project van uw oplossing.
    >
    >

## <a name="optional-run-hello-android-project"></a>(Optioneel) Hallo Android-project uitvoeren
In deze sectie kunt u Hallo Xamarin droid-project voor Android uitvoeren. Als u niet met Android-apparaten werkt, kunt u deze sectie overslaan.

#### <a name="in-xamarin-studio"></a>In Xamarin Studio

1. Met de rechtermuisknop op Hallo Android-project en selecteer vervolgens **instellen als opstartproject**.

2. toobuild project Hallo en Hallo-app te starten in een Android-emulator op Hallo **uitvoeren** selecteert u **foutopsporing starten**.

#### <a name="in-visual-studio"></a>In Visual Studio

1. Met de rechtermuisknop op het Hallo-project voor Android (Droid) en selecteer vervolgens **instellen als opstartproject**.

2. Op Hallo **bouwen** selecteert u **Configuration Manager**.

3. In Hallo **Configuration Manager** dialoogvenster, selecteer Hallo **bouwen** en **implementeren** selectievakjes volgende toohello Android-project.

4. toobuild project Hallo en Hallo-app te starten in een Android-emulator, selecteer Hallo **F5** sleutel.

   > [!NOTE]
   > Als u problemen ondervindt Hallo-project te bouwen, uitvoeren Hallo NuGet package manager en update toohello meest recente versie van Hallo Xamarin-ondersteuningspakketten. QuickStart-projecten mogelijk traag tooupdate toohello meest recente versies.    
   >
   >

5. Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en vervolgens selecteert Hallo plusteken (**+**).

    ![][11]
    
    Met deze actie verzendt een post-aanvraag toohello die mobiele Apps van nieuwe back-end die wordt gehost in Azure. De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo. Items die zijn opgeslagen in de tabel Hallo worden geretourneerd door Hallo Mobile Apps terug beëindigen en Hallo gegevens worden weergegeven in de lijst Hallo.
    
    > [!NOTE]
    > Hier vindt u Hallo-code die toegang heeft tot uw back-end van Mobile Apps in Hallo TodoItemManager.cs C#-bestand van Hallo portable class library-project van uw oplossing.
    >
    >

## <a name="optional-run-hello-windows-project"></a>(Optioneel) Hallo Windows-project uitvoeren

In deze sectie kunt uitvoeren u Hallo project Xamarin WinApp voor Windows-apparaten. Als u niet met Windows-apparaten werkt, kunt u deze sectie overslaan.

#### <a name="in-visual-studio"></a>In Visual Studio

1. Met de rechtermuisknop op een van de Windows-projecten Hallo en selecteer vervolgens **instellen als opstartproject**.

2. Op Hallo **bouwen** selecteert u **Configuration Manager**.

3. In Hallo **Configuration Manager** dialoogvenster, selecteer Hallo **bouwen** en **implementeren** selectievakjes volgende toohello Windows-project dat u hebt gekozen.

4. toobuild project Hallo en Hallo-app te starten in een Windows-emulator, selecteer Hallo **F5** sleutel.

   > [!NOTE]
   > Als u problemen ondervindt Hallo-project te bouwen, uitvoeren Hallo NuGet package manager en update toohello meest recente versie van Hallo Xamarin-ondersteuningspakketten. QuickStart-projecten mogelijk traag tooupdate toohello meest recente versies.    
   >
   >

5. Typ in het Hallo-app zinvolle tekst, zoals *xamarin leren kennen*, en vervolgens selecteert Hallo plusteken (**+**).

    Met deze actie verzendt een post-aanvraag toohello die mobiele Apps van nieuwe back-end die wordt gehost in Azure. De gegevens van Hallo-aanvraag is opgenomen in de takentabel Hallo. Items die zijn opgeslagen in de tabel Hallo worden geretourneerd door Hallo Mobile Apps terug beëindigen en Hallo gegevens worden weergegeven in de lijst Hallo.
    
    ![][12]
    
    > [!NOTE]
    > Hier vindt u Hallo-code die toegang heeft tot uw back-end van Mobile Apps in Hallo TodoItemManager.cs C#-bestand van Hallo portable class library-project van uw oplossing.
    >
    >

## <a name="next-steps"></a>Volgende stappen

* [Verificatie tooyour app toevoegen](app-service-mobile-xamarin-forms-get-started-users.md)  
  Meer informatie over hoe tooauthenticate gebruikers van uw app met een id-provider.

* [Push notifications tooyour app toevoegen](app-service-mobile-xamarin-forms-get-started-push.md)  
  Informatie over hoe tooadd pushmeldingen tooyour app ondersteunen en uw Mobile Apps back-end toouse Azure Notification Hubs toosend Hallo push-meldingen configureren.

* [Offlinesynchronisatie voor uw app inschakelen](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  Meer informatie over hoe tooadd offlineondersteuning voor uw app met behulp van een mobiele Apps van back-end. Offline synchroniseren zorgt ervoor dat u gegevens van een mobiele app kunt weergeven, toevoegen of wijzigen, zelfs als er geen netwerkverbinding is.

* [Hallo beheerde client gebruiken voor mobiele Apps](app-service-mobile-dotnet-how-to-use-client-library.md)  
  Meer informatie over hoe toowork Hello beheerd client SDK in uw Xamarin-app.

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[Azure-portal]: https://portal.azure.com/

---
title: aaaWindows Phone Silverlight bereiken SDK-integratie
description: Hoe tooIntegrate Azure Mobile Engagement bereiken met Windows Phone Silverlight-Apps
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a>Windows Phone Silverlight Reach-SDK-integratie
U moet volgen Hallo integratie procedure wordt beschreven in Hallo [Windows Phone Silverlight Engagement SDK-integratie](mobile-engagement-windows-phone-integrate-engagement.md) voordat u deze handleiding.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a>Hallo Engagement bereiken SDK in uw Windows Phone Silverlight-project insluiten
U hebt geen iets tooadd. `EngagementReach`verwijzingen en bronnen bevinden zich al in uw project.

> [!TIP]
> U kunt afbeeldingen uit Hallo `Resources` map van uw project, met name Hallo merk-pictogram (die standaard toohello Engagement pictogram).
> 
> 

## <a name="add-hello-capabilities"></a>Hallo mogelijkheden toevoegen
Hallo Engagement bereiken SDK moet een aantal aanvullende mogelijkheden.

Open uw `WMAppManifest.xml` -bestand en zorg ervoor dat die Hallo volgende mogelijkheden worden gedefinieerd:

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

Hallo wordt eerst een gebruikt door Hallo MPNS service tooallow Hallo weergave van de pop-upmelding. Hallo is tweede gebruikte tooembed een taak browser in Hallo SDK.

Hallo bewerken `WMAppManifest.xml` -bestand en voeg binnen Hallo `<Capabilities />` tag:

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a>Hallo Microsoft Push Notification Service inschakelen
In de volgorde toouse hello **Microsoft Push Notification Service** (MPNS genoemd) uw `WMAppManifest.xml` bestand moet hebben een `<App />` tag met een `Publisher` kenmerkset toohello naam van uw project.

## <a name="initialize-hello-engagement-reach-sdk"></a>Hallo Engagement bereiken SDK initialiseren
### <a name="engagement-configuration"></a>Engagement configuratie
Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project.

Dit bestand toospecify reach-configuratie bewerken:

* *Optionele*, geef aan of Hallo native pushberichten (MPNS) is geactiveerd of geen tussen `<enableNativePush>` en `</enableNativePush>` tags (`true` standaard).
* *Optionele*, Hallo-naam van Hallo push kanaal tussen vermeld `<channelName>` en `</channelName>` Hallo tags, kunt u dezelfde dat uw toepassing momenteel kan gebruiken of laat het veld leeg.

Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> U kunt de naam van Hallo MPNS push-kanaal van uw toepassing hello opgeven. Engagement maakt standaard een naam op basis van Hallo appId. U hebt geen noodzaak toospecify Hallo naam zelf, behalve als u van plan toouse Hallo push kanaal buiten Engagement bent.
> 
> 

### <a name="engagement-initialization"></a>De initialisatie van de engagement
Hallo wijzigen `App.xaml.cs`:

* Toevoegen van tooyour `using` instructies:
  
      using Microsoft.Azure.Engagement;
* Invoegen `EngagementReach.Instance.Init` vlak na `EngagementAgent.Instance.Init` in `Application_Launching` :
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* Invoegen `EngagementReach.Instance.OnActivated` in Hallo `Application_Activated` methode:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> Hallo `EngagementReach.Instance.Init` in een specifieke thread wordt uitgevoerd. U hebt geen toodo deze zelf.
> 
> 

## <a name="app-store-submission-considerations"></a>Overwegingen voor apps archief verzenden
Microsoft legt sommige regels bij gebruik van pushmeldingen Hallo:

Uit Microsoft hello [toepassingsbeleid] -documentatie, punt 2.9:

1) U moet Hallo gebruiker tooaccept tooreceive-pushmeldingen op te vragen. Vervolgens voegt u in uw instellingen voor een manier toodisable Hallo-pushmeldingen.

Hallo EngagementReach object biedt twee methoden toomanage Hallo opt-in/opt-out, `EnableNativePush()` en `DisableNativePush()`. U kunt bijvoorbeeld een optie in het Hallo-instellingen met een in-of uitschakelen toodisable maken of MPNS inschakelen.

U kunt ook bepalen toodeactivate MPNS via Hallo Engagement configuratie\<windows phone-sdk-reach-configuratie\>.

> 2.9.1) toepassing hello moet eerst Hallo meldingen toobe opgegeven beschrijven en **Hallo snelle gebruikersmachtiging (opt-in) verkrijgen**, en **moet bieden een mechanisme via welke Hallo gebruiker opt-out ontvangen kiest kunt pushmeldingen**. Alle meldingen die worden geleverd met Hallo Microsoft Push Notification Service moet overeenkomen met de Hallo beschrijving toohello gebruiker en moet voldoen aan alle toepasselijke [toepassingsbeleid] [ Content Policies]en [aanvullende vereisten voor specifieke toepassingstypen].
> 
> 

2) U dient niet te veel pushmeldingen gebruiken. Engagement verwerkt door de meldingen voor u.

> 2.9.2) Hallo-toepassing en het gebruik van Microsoft Push Notification Service Hallo moeten niet overmatig gebruik netwerkcapaciteit of bandbreedte Hallo Microsoft Push Notification Service of anders ten onrechte belasten een Windows Phone-of andere Microsoft-apparaat of service met buitensporige pushmeldingen, zoals wordt bepaald door Microsoft in alle redelijkheid bepaald en mag niet schadelijk zijn of een Microsoft-netwerken of servers of servers van derden of netwerken verbonden toohello Microsoft Push Notification Service verstoren.
> 
> 

3) Vertrouw niet op MPNS toosend criticals informatie. Engagement maakt gebruik van MPNS, zodat deze regel ook voor Hallo campagnes gemaakt binnen Hallo Engagement front-end geldt.

> 2.9.3) Hallo Microsoft Push Notification Service mogelijk niet gebruikte toosend meldingen die worden bedrijfskritieke kritieke of anderszins kan invloed hebben op van het leven of dood, inclusief en zonder beperking kritieke meldingen gerelateerde tooa medische apparaat of een voorwaarde voor u belangrijk is. MICROSOFT uitdrukkelijk wijst ANY garanties dat Hallo gebruik van hello MICROSOFT PUSH NOTIFICATION SERVICE of levering van MICROSOFT PUSH NOTIFICATION SERVICE meldingen wordt worden onderbroken, vrij fout, of anders gegarandeerd tooOCCUR ON A REAL-TIME BASIS.
> 
> 

**Wij garanderen niet dat uw toepassing hello validatieproces wordt geaccepteerd als u bieden geen ondersteuning voor deze aanbevelingen.**

## <a name="handle-data-push-optional"></a>Verwerken van gegevens-push (optioneel)
Als u wilt dat uw toepassing toobe kunnen tooreceive Reach gegevens-pushes, hebt u twee gebeurtenissen tooimplement Hallo EngagementReach klasse:

    EngagementReach.Instance.DataPushStringReceived += (body) =>
    {
       Debug.WriteLine("String data push message received: " + body);
       return true;
    };

    EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
    {
       Debug.WriteLine("Base64 data push message received: " + encodedBody);
       // Do something useful with decodedBody like updating an image view
       return true;
    };

U ziet dat Hallo retouraanroep van elke methode retourneert een Booleaanse waarde. Engagement verzendt een feedback tooits back-end na het verzenden van gegevens-push Hallo. Als het Hallo-callback false retourneert, Hallo `exit` feedback verzenden zijn. Anders moeten `action`. Als geen retouraanroep is ingesteld op Hallo gebeurtenissen, Hallo `drop` feedback tooEngagement worden geretourneerd.

> [!WARNING]
> Engagement is niet kunnen tooreceive veelvouden feedback voor een gegevens-push. Als u van plan tooset verschillende handlers een gebeurtenis bent, houd er rekening mee dat Hallo feedback toohello het laatst werd verzonden overeenkomen worden. In dit geval wordt aangeraden tooalways retourneert dezelfde waarde tooavoid verwarrend feedback over voor front-Hallo Hallo.
> 
> 

## <a name="customize-ui-optional"></a>Aanpassen van de gebruikersinterface (optioneel)
### <a name="first-step"></a>Eerste stap
We laten toocustomize Hallo reach gebruikersinterface.

toodo geval is, hebt u toocreate een subklasse van Hallo `EngagementReachHandler` klasse.

**Voorbeeld van Code:**

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

Vervolgens stelt u inhoud Hallo Hallo `EngagementReach.Instance.Handler` veld met het aangepaste object in uw `App.xaml.cs` klasse binnen de Hallo `Application_Launching` methode.

**Voorbeeld van Code:**

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> Engagement maakt standaard gebruik van een eigen implementatie van `EngagementReachHandler`. U hebt geen toocreate zelf, en als u doet dit, hebt u niet toooverride elke methode. Hallo standaardgedrag is tooselect Hallo Engagement basisobject.
> 
> 

### <a name="layouts"></a>Indelingen
Standaard Reach Hallo ingesloten resources van Hallo DLL toodisplay Hallo meldingen en pagina's gebruikt.

Echter, u kunt ervoor kiezen toouse uw eigen tooreflect resources uw huisstijl in deze onderdelen.

U kunt onderdrukken `EngagementReachHandler` methoden in uw subklasse tootell Engagement toouse uw indelingen:

**Voorbeeld van Code:**

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> Hallo `CreateNotification` methode null kan retourneren. Hallo-bericht niet weergegeven en Hallo reach-campagne wordt verwijderd.
> 
> 

toosimplify uw implementatie lay-out ook bieden we ons eigen xaml die als basis voor uw code dienen kan. Ze bevinden zich op Hallo Engagement SDK-archief (/ src/reach /).

> [!WARNING]
> Hallo-bronnen die wij verstrekken Hallo zijn exact dezelfde waarden die we gebruiken. Dus als u toomodify wilt ze rechtstreeks niet vergeet toochange Hallo naamruimte en naam Hallo.
> 
> 

### <a name="notification-position"></a>Positie van de kennisgeving
Standaard wordt een melding in de app op Hallo onder links van de toepassing hello weergegeven. U kunt dit gedrag veranderen overschrijft Hallo `GetNotificationPosition` methode Hallo `EngagementReachHandler` object.

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

Op dit moment kunt u kiezen tussen Hallo `BOTTOM` (standaard) en `TOP` posities.

### <a name="launch-message"></a>Bericht starten
Wanneer een gebruiker klikt op een Systeemmelding (een pop-up), Engagement gestart Hallo app, load Hallo inhoud Hallo push berichten en Hallo-pagina voor Hallo campagne overeenkomt weergegeven.

Er is een vertraging tussen Hallo starten van de toepassing en Hallo beeldscherm Hallo van Hallo pagina (afhankelijk van de Hallo snelheid van uw netwerk).

gebruiker toohello tooindicate dat er iets wordt geladen, moet u een visuele gegevens, zoals een voortgangsbalk zien of een voortgangsindicator opgeven. Engagement kan niet worden verwerkt, maar enkele handlers voor u biedt.

tooimplement Hallo callback, doen:

    /* hello application has launched and hello content is loading.
     * You should display an indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

    /* hello application has finished loading hello content and hello page
     * is about toobe displayed.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

    /* hello content has been loaded, but an error has occurred.
     * You can provide an information toohello user.
     * You should hide hello indicator here.
     */
    EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Hallo-callback kunt u instellen in uw `Application_Launching` methode van uw `App.xaml.cs` -bestand, bij voorkeur voor Hallo `EngagementReach.Instance.Init()` aanroepen.

> [!TIP]
> Elke handler wordt aangeroepen door Hallo UI Thread. U hoeft geen tooworry wanneer u een MessageBox of iets UI-gerelateerde.
> 
> 

[toepassingsbeleid]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[aanvullende vereisten voor specifieke toepassingstypen]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx


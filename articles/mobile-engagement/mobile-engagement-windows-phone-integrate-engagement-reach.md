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
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="fa542-103">Windows Phone Silverlight Reach-SDK-integratie</span><span class="sxs-lookup"><span data-stu-id="fa542-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="fa542-104">U moet volgen Hallo integratie procedure wordt beschreven in Hallo [Windows Phone Silverlight Engagement SDK-integratie](mobile-engagement-windows-phone-integrate-engagement.md) voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="fa542-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="fa542-105">Hallo Engagement bereiken SDK in uw Windows Phone Silverlight-project insluiten</span><span class="sxs-lookup"><span data-stu-id="fa542-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="fa542-106">U hebt geen iets tooadd.</span><span class="sxs-lookup"><span data-stu-id="fa542-106">You do not have anything tooadd.</span></span> <span data-ttu-id="fa542-107">`EngagementReach`verwijzingen en bronnen bevinden zich al in uw project.</span><span class="sxs-lookup"><span data-stu-id="fa542-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="fa542-108">U kunt afbeeldingen uit Hallo `Resources` map van uw project, met name Hallo merk-pictogram (die standaard toohello Engagement pictogram).</span><span class="sxs-lookup"><span data-stu-id="fa542-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="fa542-109">Hallo mogelijkheden toevoegen</span><span class="sxs-lookup"><span data-stu-id="fa542-109">Add hello capabilities</span></span>
<span data-ttu-id="fa542-110">Hallo Engagement bereiken SDK moet een aantal aanvullende mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="fa542-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="fa542-111">Open uw `WMAppManifest.xml` -bestand en zorg ervoor dat die Hallo volgende mogelijkheden worden gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="fa542-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="fa542-112">Hallo wordt eerst een gebruikt door Hallo MPNS service tooallow Hallo weergave van de pop-upmelding.</span><span class="sxs-lookup"><span data-stu-id="fa542-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="fa542-113">Hallo is tweede gebruikte tooembed een taak browser in Hallo SDK.</span><span class="sxs-lookup"><span data-stu-id="fa542-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="fa542-114">Hallo bewerken `WMAppManifest.xml` -bestand en voeg binnen Hallo `<Capabilities />` tag:</span><span class="sxs-lookup"><span data-stu-id="fa542-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="fa542-115">Hallo Microsoft Push Notification Service inschakelen</span><span class="sxs-lookup"><span data-stu-id="fa542-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="fa542-116">In de volgorde toouse hello **Microsoft Push Notification Service** (MPNS genoemd) uw `WMAppManifest.xml` bestand moet hebben een `<App />` tag met een `Publisher` kenmerkset toohello naam van uw project.</span><span class="sxs-lookup"><span data-stu-id="fa542-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="fa542-117">Hallo Engagement bereiken SDK initialiseren</span><span class="sxs-lookup"><span data-stu-id="fa542-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="fa542-118">Engagement configuratie</span><span class="sxs-lookup"><span data-stu-id="fa542-118">Engagement configuration</span></span>
<span data-ttu-id="fa542-119">Hallo Engagement configuratie op Hallo is gecentraliseerd `Resources\EngagementConfiguration.xml` -bestand van uw project.</span><span class="sxs-lookup"><span data-stu-id="fa542-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="fa542-120">Dit bestand toospecify reach-configuratie bewerken:</span><span class="sxs-lookup"><span data-stu-id="fa542-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="fa542-121">*Optionele*, geef aan of Hallo native pushberichten (MPNS) is geactiveerd of geen tussen `<enableNativePush>` en `</enableNativePush>` tags (`true` standaard).</span><span class="sxs-lookup"><span data-stu-id="fa542-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="fa542-122">*Optionele*, Hallo-naam van Hallo push kanaal tussen vermeld `<channelName>` en `</channelName>` Hallo tags, kunt u dezelfde dat uw toepassing momenteel kan gebruiken of laat het veld leeg.</span><span class="sxs-lookup"><span data-stu-id="fa542-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="fa542-123">Als u wilt dat deze tijdens runtime in plaats daarvan kunt u bellen Hallo volgende toospecify methode voordat de initialisatie van de agent Hallo Engagement:</span><span class="sxs-lookup"><span data-stu-id="fa542-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

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
> <span data-ttu-id="fa542-124">U kunt de naam van Hallo MPNS push-kanaal van uw toepassing hello opgeven.</span><span class="sxs-lookup"><span data-stu-id="fa542-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="fa542-125">Engagement maakt standaard een naam op basis van Hallo appId.</span><span class="sxs-lookup"><span data-stu-id="fa542-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="fa542-126">U hebt geen noodzaak toospecify Hallo naam zelf, behalve als u van plan toouse Hallo push kanaal buiten Engagement bent.</span><span class="sxs-lookup"><span data-stu-id="fa542-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="fa542-127">De initialisatie van de engagement</span><span class="sxs-lookup"><span data-stu-id="fa542-127">Engagement initialization</span></span>
<span data-ttu-id="fa542-128">Hallo wijzigen `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="fa542-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="fa542-129">Toevoegen van tooyour `using` instructies:</span><span class="sxs-lookup"><span data-stu-id="fa542-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="fa542-130">Invoegen `EngagementReach.Instance.Init` vlak na `EngagementAgent.Instance.Init` in `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="fa542-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="fa542-131">Invoegen `EngagementReach.Instance.OnActivated` in Hallo `Application_Activated` methode:</span><span class="sxs-lookup"><span data-stu-id="fa542-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="fa542-132">Hallo `EngagementReach.Instance.Init` in een specifieke thread wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fa542-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="fa542-133">U hebt geen toodo deze zelf.</span><span class="sxs-lookup"><span data-stu-id="fa542-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="fa542-134">Overwegingen voor apps archief verzenden</span><span class="sxs-lookup"><span data-stu-id="fa542-134">App store submission considerations</span></span>
<span data-ttu-id="fa542-135">Microsoft legt sommige regels bij gebruik van pushmeldingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="fa542-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="fa542-136">Uit Microsoft hello [toepassingsbeleid] -documentatie, punt 2.9:</span><span class="sxs-lookup"><span data-stu-id="fa542-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="fa542-137">U moet Hallo gebruiker tooaccept tooreceive-pushmeldingen op te vragen.</span><span class="sxs-lookup"><span data-stu-id="fa542-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="fa542-138">Vervolgens voegt u in uw instellingen voor een manier toodisable Hallo-pushmeldingen.</span><span class="sxs-lookup"><span data-stu-id="fa542-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="fa542-139">Hallo EngagementReach object biedt twee methoden toomanage Hallo opt-in/opt-out, `EnableNativePush()` en `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="fa542-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="fa542-140">U kunt bijvoorbeeld een optie in het Hallo-instellingen met een in-of uitschakelen toodisable maken of MPNS inschakelen.</span><span class="sxs-lookup"><span data-stu-id="fa542-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="fa542-141">U kunt ook bepalen toodeactivate MPNS via Hallo Engagement configuratie\<windows phone-sdk-reach-configuratie\>.</span><span class="sxs-lookup"><span data-stu-id="fa542-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="fa542-142">2.9.1) toepassing hello moet eerst Hallo meldingen toobe opgegeven beschrijven en **Hallo snelle gebruikersmachtiging (opt-in) verkrijgen**, en **moet bieden een mechanisme via welke Hallo gebruiker opt-out ontvangen kiest kunt pushmeldingen**.</span><span class="sxs-lookup"><span data-stu-id="fa542-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="fa542-143">Alle meldingen die worden geleverd met Hallo Microsoft Push Notification Service moet overeenkomen met de Hallo beschrijving toohello gebruiker en moet voldoen aan alle toepasselijke [toepassingsbeleid] [ Content Policies]en [aanvullende vereisten voor specifieke toepassingstypen].</span><span class="sxs-lookup"><span data-stu-id="fa542-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="fa542-144">U dient niet te veel pushmeldingen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa542-144">You should not use too many push notifications.</span></span> <span data-ttu-id="fa542-145">Engagement verwerkt door de meldingen voor u.</span><span class="sxs-lookup"><span data-stu-id="fa542-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="fa542-146">2.9.2) Hallo-toepassing en het gebruik van Microsoft Push Notification Service Hallo moeten niet overmatig gebruik netwerkcapaciteit of bandbreedte Hallo Microsoft Push Notification Service of anders ten onrechte belasten een Windows Phone-of andere Microsoft-apparaat of service met buitensporige pushmeldingen, zoals wordt bepaald door Microsoft in alle redelijkheid bepaald en mag niet schadelijk zijn of een Microsoft-netwerken of servers of servers van derden of netwerken verbonden toohello Microsoft Push Notification Service verstoren.</span><span class="sxs-lookup"><span data-stu-id="fa542-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="fa542-147">Vertrouw niet op MPNS toosend criticals informatie.</span><span class="sxs-lookup"><span data-stu-id="fa542-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="fa542-148">Engagement maakt gebruik van MPNS, zodat deze regel ook voor Hallo campagnes gemaakt binnen Hallo Engagement front-end geldt.</span><span class="sxs-lookup"><span data-stu-id="fa542-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="fa542-149">2.9.3) Hallo Microsoft Push Notification Service mogelijk niet gebruikte toosend meldingen die worden bedrijfskritieke kritieke of anderszins kan invloed hebben op van het leven of dood, inclusief en zonder beperking kritieke meldingen gerelateerde tooa medische apparaat of een voorwaarde voor u belangrijk is.</span><span class="sxs-lookup"><span data-stu-id="fa542-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="fa542-150">MICROSOFT uitdrukkelijk wijst ANY garanties dat Hallo gebruik van hello MICROSOFT PUSH NOTIFICATION SERVICE of levering van MICROSOFT PUSH NOTIFICATION SERVICE meldingen wordt worden onderbroken, vrij fout, of anders gegarandeerd tooOCCUR ON A REAL-TIME BASIS.</span><span class="sxs-lookup"><span data-stu-id="fa542-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="fa542-151">**Wij garanderen niet dat uw toepassing hello validatieproces wordt geaccepteerd als u bieden geen ondersteuning voor deze aanbevelingen.**</span><span class="sxs-lookup"><span data-stu-id="fa542-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="fa542-152">Verwerken van gegevens-push (optioneel)</span><span class="sxs-lookup"><span data-stu-id="fa542-152">Handle data push (optional)</span></span>
<span data-ttu-id="fa542-153">Als u wilt dat uw toepassing toobe kunnen tooreceive Reach gegevens-pushes, hebt u twee gebeurtenissen tooimplement Hallo EngagementReach klasse:</span><span class="sxs-lookup"><span data-stu-id="fa542-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="fa542-154">U ziet dat Hallo retouraanroep van elke methode retourneert een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="fa542-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="fa542-155">Engagement verzendt een feedback tooits back-end na het verzenden van gegevens-push Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa542-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="fa542-156">Als het Hallo-callback false retourneert, Hallo `exit` feedback verzenden zijn.</span><span class="sxs-lookup"><span data-stu-id="fa542-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="fa542-157">Anders moeten `action`.</span><span class="sxs-lookup"><span data-stu-id="fa542-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="fa542-158">Als geen retouraanroep is ingesteld op Hallo gebeurtenissen, Hallo `drop` feedback tooEngagement worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="fa542-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="fa542-159">Engagement is niet kunnen tooreceive veelvouden feedback voor een gegevens-push.</span><span class="sxs-lookup"><span data-stu-id="fa542-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="fa542-160">Als u van plan tooset verschillende handlers een gebeurtenis bent, houd er rekening mee dat Hallo feedback toohello het laatst werd verzonden overeenkomen worden.</span><span class="sxs-lookup"><span data-stu-id="fa542-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="fa542-161">In dit geval wordt aangeraden tooalways retourneert dezelfde waarde tooavoid verwarrend feedback over voor front-Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa542-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="fa542-162">Aanpassen van de gebruikersinterface (optioneel)</span><span class="sxs-lookup"><span data-stu-id="fa542-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="fa542-163">Eerste stap</span><span class="sxs-lookup"><span data-stu-id="fa542-163">First step</span></span>
<span data-ttu-id="fa542-164">We laten toocustomize Hallo reach gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="fa542-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="fa542-165">toodo geval is, hebt u toocreate een subklasse van Hallo `EngagementReachHandler` klasse.</span><span class="sxs-lookup"><span data-stu-id="fa542-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="fa542-166">**Voorbeeld van Code:**</span><span class="sxs-lookup"><span data-stu-id="fa542-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="fa542-167">Vervolgens stelt u inhoud Hallo Hallo `EngagementReach.Instance.Handler` veld met het aangepaste object in uw `App.xaml.cs` klasse binnen de Hallo `Application_Launching` methode.</span><span class="sxs-lookup"><span data-stu-id="fa542-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="fa542-168">**Voorbeeld van Code:**</span><span class="sxs-lookup"><span data-stu-id="fa542-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="fa542-169">Engagement maakt standaard gebruik van een eigen implementatie van `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="fa542-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="fa542-170">U hebt geen toocreate zelf, en als u doet dit, hebt u niet toooverride elke methode.</span><span class="sxs-lookup"><span data-stu-id="fa542-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="fa542-171">Hallo standaardgedrag is tooselect Hallo Engagement basisobject.</span><span class="sxs-lookup"><span data-stu-id="fa542-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="fa542-172">Indelingen</span><span class="sxs-lookup"><span data-stu-id="fa542-172">Layouts</span></span>
<span data-ttu-id="fa542-173">Standaard Reach Hallo ingesloten resources van Hallo DLL toodisplay Hallo meldingen en pagina's gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fa542-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="fa542-174">Echter, u kunt ervoor kiezen toouse uw eigen tooreflect resources uw huisstijl in deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="fa542-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="fa542-175">U kunt onderdrukken `EngagementReachHandler` methoden in uw subklasse tootell Engagement toouse uw indelingen:</span><span class="sxs-lookup"><span data-stu-id="fa542-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="fa542-176">**Voorbeeld van Code:**</span><span class="sxs-lookup"><span data-stu-id="fa542-176">**Sample Code :**</span></span>

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
> <span data-ttu-id="fa542-177">Hallo `CreateNotification` methode null kan retourneren.</span><span class="sxs-lookup"><span data-stu-id="fa542-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="fa542-178">Hallo-bericht niet weergegeven en Hallo reach-campagne wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="fa542-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="fa542-179">toosimplify uw implementatie lay-out ook bieden we ons eigen xaml die als basis voor uw code dienen kan.</span><span class="sxs-lookup"><span data-stu-id="fa542-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="fa542-180">Ze bevinden zich op Hallo Engagement SDK-archief (/ src/reach /).</span><span class="sxs-lookup"><span data-stu-id="fa542-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="fa542-181">Hallo-bronnen die wij verstrekken Hallo zijn exact dezelfde waarden die we gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fa542-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="fa542-182">Dus als u toomodify wilt ze rechtstreeks niet vergeet toochange Hallo naamruimte en naam Hallo.</span><span class="sxs-lookup"><span data-stu-id="fa542-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="fa542-183">Positie van de kennisgeving</span><span class="sxs-lookup"><span data-stu-id="fa542-183">Notification position</span></span>
<span data-ttu-id="fa542-184">Standaard wordt een melding in de app op Hallo onder links van de toepassing hello weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa542-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="fa542-185">U kunt dit gedrag veranderen overschrijft Hallo `GetNotificationPosition` methode Hallo `EngagementReachHandler` object.</span><span class="sxs-lookup"><span data-stu-id="fa542-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="fa542-186">Op dit moment kunt u kiezen tussen Hallo `BOTTOM` (standaard) en `TOP` posities.</span><span class="sxs-lookup"><span data-stu-id="fa542-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="fa542-187">Bericht starten</span><span class="sxs-lookup"><span data-stu-id="fa542-187">Launch message</span></span>
<span data-ttu-id="fa542-188">Wanneer een gebruiker klikt op een Systeemmelding (een pop-up), Engagement gestart Hallo app, load Hallo inhoud Hallo push berichten en Hallo-pagina voor Hallo campagne overeenkomt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fa542-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="fa542-189">Er is een vertraging tussen Hallo starten van de toepassing en Hallo beeldscherm Hallo van Hallo pagina (afhankelijk van de Hallo snelheid van uw netwerk).</span><span class="sxs-lookup"><span data-stu-id="fa542-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="fa542-190">gebruiker toohello tooindicate dat er iets wordt geladen, moet u een visuele gegevens, zoals een voortgangsbalk zien of een voortgangsindicator opgeven.</span><span class="sxs-lookup"><span data-stu-id="fa542-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="fa542-191">Engagement kan niet worden verwerkt, maar enkele handlers voor u biedt.</span><span class="sxs-lookup"><span data-stu-id="fa542-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="fa542-192">tooimplement Hallo callback, doen:</span><span class="sxs-lookup"><span data-stu-id="fa542-192">tooimplement hello callback, do:</span></span>

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

<span data-ttu-id="fa542-193">Hallo-callback kunt u instellen in uw `Application_Launching` methode van uw `App.xaml.cs` -bestand, bij voorkeur voor Hallo `EngagementReach.Instance.Init()` aanroepen.</span><span class="sxs-lookup"><span data-stu-id="fa542-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="fa542-194">Elke handler wordt aangeroepen door Hallo UI Thread.</span><span class="sxs-lookup"><span data-stu-id="fa542-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="fa542-195">U hoeft geen tooworry wanneer u een MessageBox of iets UI-gerelateerde.</span><span class="sxs-lookup"><span data-stu-id="fa542-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[toepassingsbeleid]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[aanvullende vereisten voor specifieke toepassingstypen]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx


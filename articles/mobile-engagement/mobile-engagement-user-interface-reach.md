---
title: aaaAzure Mobile Engagement-gebruikersinterface - bereik
description: Meer informatie over hoe tooreach toohello gebruikers van uw toepassing met behulp van Azure Mobile Engagement pushmeldingen
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: d96e2590-08dd-4481-a352-2c18f26a1643
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 40d5162ddeccec82c2c9f5b0d72b4cb10c9ddc38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreach-out-toohello-users-of-your-application-with-push-notifications"></a><span data-ttu-id="8f6d4-103">Hoe tooreach toohello gebruikers van uw toepassing met pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="8f6d4-103">How tooreach out toohello users of your application with push notifications</span></span>
<span data-ttu-id="8f6d4-104">Dit artikel wordt beschreven Hallo **bereiken** tabblad Hallo **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-104">This article describes hello **REACH** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="8f6d4-105">Gebruik van Hallo **Mobile Engagement** portal toomonitor en beheren van uw mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span> <span data-ttu-id="8f6d4-106">Houd er rekening mee dat toostart met Hallo portal toocreate moet u eerst een **Azure Mobile Engagement** account.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-106">Note that toostart using hello portal you first need toocreate an **Azure Mobile Engagement** account.</span></span> <span data-ttu-id="8f6d4-107">Zie voor meer informatie [een Azure Mobile Engagement-account maken](mobile-engagement-create.md).</span><span class="sxs-lookup"><span data-stu-id="8f6d4-107">For more information, see [Create an Azure Mobile Engagement account](mobile-engagement-create.md).</span></span>

<span data-ttu-id="8f6d4-108">Hallo sectie van de gebruikersinterface is Hallo Hallo Push campagne beheerprogramma u maken/bewerken/activeren/voltooien/monitor kunt bereiken en statistieken over campagnes met pushmeldingen en functies die ook toegankelijk via Hallo Reach API (en bepaalde elementen van Hallo lage ophalen niveau Push-API).</span><span class="sxs-lookup"><span data-stu-id="8f6d4-108">hello Reach section of hello UI is hello Push campaign management tool where you can create/edit/activate/finish/monitor and get statistics on Push notification campaigns and features that can also be accessed via hello Reach API (and some elements of hello low level Push API).</span></span> <span data-ttu-id="8f6d4-109">Houd er rekening mee dat of u Hallo API's of Hallo gebruikersinterface gebruikt, u toointegrate moet zowel Azure Mobile Engagement en het bereik in uw toepassing voor elk platform Hello SDK voordat u kunt bereiken campagnes.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-109">Remember that whether you are using hello APIs or hello UI, you will need toointegrate both Azure Mobile Engagement and Reach into your application for each platform with hello SDK before you can use Reach campaigns.</span></span>

> [!NOTE]
> <span data-ttu-id="8f6d4-110">Veel secties Hallo **Mobile Engagement** gebruikersinterface portal bevatten Hallo **HELP weergeven** knop.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-110">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="8f6d4-111">Druk op deze knop tooget meer contextuele informatie over een sectie.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-111">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="four-types-of-push-notifications"></a><span data-ttu-id="8f6d4-112">Vier typen pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="8f6d4-112">Four types of Push notifications</span></span>
1. <span data-ttu-id="8f6d4-113">Aankondigingen - kunt u toosend reclame berichten toousers die hen tooanother locatie in uw app of toosend omleidt ze tooa webpagina of buiten uw app worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-113">Announcements - allow you toosend advertising messages toousers that redirect them tooanother location inside your app or toosend them tooa webpage or store outside of your app.</span></span> 
2. <span data-ttu-id="8f6d4-114">Polls - kunt u toogather gegevens van eindgebruikers door vragen aan hen te vragen.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-114">Polls - allow you toogather information from end users by asking them questions.</span></span>
3. <span data-ttu-id="8f6d4-115">Gegevens-Pushes - kunt u toosend een binair of base64-gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-115">Data Pushes - allow you toosend a binary or base64 data file.</span></span> <span data-ttu-id="8f6d4-116">Hallo-gegevens in een gegevens-push tooyour toepassing toomodify van uw huidige gebruikerservaring in uw app verzonden.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-116">hello information contained in a data push is sent tooyour application toomodify your users' current experience in your app.</span></span> <span data-ttu-id="8f6d4-117">Uw toepassing moet toobe kunnen tooprocess Hallo gegevens in een gegevens-push.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-117">Your application needs toobe able tooprocess hello data in a data push.</span></span>

## <a name="campaign-details"></a><span data-ttu-id="8f6d4-118">Campagnedetails</span><span class="sxs-lookup"><span data-stu-id="8f6d4-118">Campaign Details</span></span>
<span data-ttu-id="8f6d4-119">Bewerken, kopiëren, verwijderen of campagnes die u hebt nog niet geactiveerd door de muiswijzer op hun namen activeren of u kunt klikken op tooopen ze.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-119">You can edit, clone, delete, or activate campaigns that have not been activated yet by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="8f6d4-120">U kunt de campagnes die al zijn geactiveerd door de muiswijzer op hun namen klonen of u kunt klikken op tooopen ze.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-120">You can clone campaigns that have already been activated by hovering over their names or you can click tooopen them.</span></span> <span data-ttu-id="8f6d4-121">U kunt echter een campagne niet wijzigen zodra deze is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-121">However, you can't change a campaign once it has been activated.</span></span>

![Reach1][18]

## <a name="reach-feedback"></a><span data-ttu-id="8f6d4-123">Feedback bereiken</span><span class="sxs-lookup"><span data-stu-id="8f6d4-123">Reach Feedback</span></span>
<span data-ttu-id="8f6d4-124">Klik op **statistieken** toosee Hallo details van een Reach-campagne.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-124">Click on **Statistics** toosee hello details of a Reach campaign.</span></span> <span data-ttu-id="8f6d4-125">Hallo **eenvoudige** weergave biedt een visuele representatie in Hallo vorm van een kolom staafdiagram over wat is er gebeurd nadat een campagne is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-125">hello **Simple** view provides a visual representation in hello form of a column bar graph about what happened after a campaign was activated.</span></span> <span data-ttu-id="8f6d4-126">Hallo **Geavanceerd** weergave biedt meer gedetailleerde informatie over Hallo pushcampagne.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-126">hello **Advanced** view provides more granular details about hello push campaign.</span></span> <span data-ttu-id="8f6d4-127">Deze gegevens meer niet beschikbaar als u een campagne test dat wil zeggen een push verzonden tooa test-apparaat verzendt.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-127">These details will not be available if you are sending a test campaign i.e. a push sent tooa test device.</span></span> <span data-ttu-id="8f6d4-128">Hier ziet u hoe deze gegevens moeten worden geïnterpreteerd:</span><span class="sxs-lookup"><span data-stu-id="8f6d4-128">Here is how you should interpret these details:</span></span>

1. <span data-ttu-id="8f6d4-129">**Gepusht** -Hiermee geeft u het aantal berichten gepusht toohello apparaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-129">**Pushed** - This specifies hello number of messages pushed toohello devices.</span></span> <span data-ttu-id="8f6d4-130">Dit nummer is afhankelijk van Hallo doelgroep die u hebt opgegeven tijdens het Hallo pushcampagne te maken.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-130">This number will depend on hello target audience you specified while creating hello push campaign.</span></span> <span data-ttu-id="8f6d4-131">Als u een doelgroep niet opgeeft, wordt deze push uit tooall Hallo ingeschreven apparaten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-131">If you do not specify any target audience, then this push will be sent out tooall hello registered devices.</span></span> <span data-ttu-id="8f6d4-132">Net als alle andere pushservices we niet Hallo meldingen push rechtstreeks toohello apparaten, maar in plaats daarvan push ze het desbetreffende platform toohello specifieke Push Notification Services (PNS - GCM-APNS/WNS) zodat ze Hallo meldingen toohello apparaten kunnen leveren.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-132">Like all other push services, we do not push hello notifications directly toohello devices but instead push them toohello respective platform specific Push Notification Services (PNS - APNS/GCM/WNS) so that they can deliver hello notifications toohello devices.</span></span> 
2. <span data-ttu-id="8f6d4-133">**Bezorgd** -Hiermee geeft u het aantal berichten dat is geleverd door Hallo PNS toohello apparaat en bevestigd Hallo als ontvangen door Mobile Engagement SDK.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-133">**Delivered** - This specifies hello number of messages which are successfully delivered by hello PNS toohello device and acknowledged as received by Mobile Engagement SDK.</span></span> 
   
   <span data-ttu-id="8f6d4-134">*Redenen voor geleverd tellen lager is dan het aantal Pushed:*</span><span class="sxs-lookup"><span data-stu-id="8f6d4-134">*Reasons for Delivered count being less than Pushed count:*</span></span>
   
   1. <span data-ttu-id="8f6d4-135">Als gebruiker Hallo Hallo app van Hallo-apparaat is verwijderd maar Hallo PNS niet kent het gelijktijdig Hallo die we Hallo push toohello PNS sturen wordt het Hallo-bericht worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-135">If hello user has uninstalled hello app from hello device but hello PNS doesn't know about it at hello time we send hello push toohello PNS then hello message will be dropped.</span></span>
   2. <span data-ttu-id="8f6d4-136">Als Hallo apparaat Hallo app heeft maar Hallo apparaten zelf voor langere tijd offline was, mislukken hello PNS toodeliver Hallo-bericht toohello apparaat.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-136">If hello device has hello app but hello devices themselves were offline for long periods of time, then hello PNS will fail toodeliver hello message toohello device.</span></span> 
   3. <span data-ttu-id="8f6d4-137">Als het Hallo-bericht toohello apparaat verzonden maar Hallo Mobile Engagement SDK in de app Hallo Hallo inhoud van het Hallo-bericht niet herkent, komt het bericht.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-137">If hello message does get delivered toohello device but hello Mobile Engagement SDK in hello app doesn’t recognize hello content of hello message, then it drops that message.</span></span> <span data-ttu-id="8f6d4-138">Dit kan gebeuren als het Hallo-aanpassing van Hallo melding in Hallo-app genereert een uitzondering die we catch in Hallo SDK en verwijder het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-138">This could happen if hello customization of hello notification in hello app generates an exception which we catch in hello SDK and drop hello message.</span></span> <span data-ttu-id="8f6d4-139">Dit kan ook optreden als Hallo-app op Hallo-apparaat met een versie van Hallo Mobile Engagement SDK die niet kunnen toounderstand Hallo nieuwere versie van push het Hallo-bericht verzonden vanuit Hallo-platform, maar dit is alleen wanneer het Hallo-app is bijgewerkt na de Hallo kennisgeving uit de service-platform Hallo is verzonden.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-139">This could also occur if hello app on hello device is using a version of hello Mobile Engagement SDK which is not able toounderstand hello newer version of hello push message sent from hello platform but this is only when hello app was upgraded after hello notification was dispatched from hello service platform.</span></span> <span data-ttu-id="8f6d4-140">Hallo **Geavanceerd** tabblad vertelt u hoeveel berichten zijn verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-140">hello **Advanced** tab will tell how many messages were dropped.</span></span> 
   4. <span data-ttu-id="8f6d4-141">Op iOS-apparaten kunnen berichten soms niet verzonden als het Hallo-apparaat op de accu of als Hallo app aanzienlijke hoeveelheid energie verbruikt bij het verwerken van externe meldingen.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-141">On iOS devices, messages sometimes do not get delivered if either hello device is on low battery or if hello app is consuming significant amount of power when processing remote notifications.</span></span> <span data-ttu-id="8f6d4-142">Dit is een beperking van Hallo iOS-apparaten.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-142">This is a limitation of hello iOS devices.</span></span>   
3. <span data-ttu-id="8f6d4-143">**Weergegeven** -Hiermee geeft u het aantal berichten die met succes toohello app gebruiker op Hallo-apparaat in Hallo vorm van een Systeemmelding push/out-van-app in het meldingencentrum hello of een in-app-melding binnen Hallo mobiele weergegeven Hallo App.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-143">**Displayed** - This specifies hello number of messages which are successfully shown toohello app user on hello device in hello form of a system push/out-of-app notification in hello notification center or an in-app notification within hello mobile app.</span></span>  <span data-ttu-id="8f6d4-144">Hallo **Geavanceerd** tabblad vertelt u hoeveel systeemmeldingen zijn en hoeveel waren in app-meldingen.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-144">hello **Advanced** tab will tell you how many were system notifications and how many were in-app notifications.</span></span> 
   
   <span data-ttu-id="8f6d4-145">*Redenen voor het weergegeven aantal lager is dan het aantal afgeleverde (wachten toobe weergegeven)*</span><span class="sxs-lookup"><span data-stu-id="8f6d4-145">*Reasons for Displayed count being less than Delivered count (waiting toobe displayed)*</span></span>
   
   1. <span data-ttu-id="8f6d4-146">Als Hallo melding campagne een einddatum op deze had, dan is het mogelijk dat Hallo melding is geleverd, maar wanneer Hallo tijd tooopen documentatie en het toohello app gebruiker weergeven, is het al verlopen zodat deze nooit is weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-146">If hello notification campaign had an end date on it then it is possible that hello notification was delivered but when hello time came tooopen and display it toohello app user, it was already expired so it was never displayed.</span></span>   
   2. <span data-ttu-id="8f6d4-147">Als het Hallo-bericht is een melding in de app vervolgens Hallo melding alleen weergegeven als Hallo app gebruiker Hallo app opent.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-147">If hello notification is an in-app notification then hello notification is only displayed when hello app user opens hello app.</span></span> <span data-ttu-id="8f6d4-148">In gevallen waarbij Hallo app gebruikers Hallo app nog niet geopend Hallo SDK rapporteert dat Hallo melding is geleverd, maar nog niet weergegeven totdat het Hallo-app wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-148">In cases where hello app user hasn't opened hello app, hello SDK will report that hello notification was delivered but not yet displayed until hello app is opened.</span></span> 
   3. <span data-ttu-id="8f6d4-149">Als Hallo-bericht een melding in de app is en toobe weergegeven op een specifieke activiteit en/of vervolgens ook de Hallo-melding worden gerapporteerd, zoals geleverd is geconfigureerd, maar nog niet is geleverd tot opent Hallo gebruiker Hallo-app op een bepaald scherm.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-149">If hello notification is an in-app notification and configured toobe shown on a specific activity/screen then also hello notification will be reported as delivered but not yet delivered until hello user opens hello app on a specific screen.</span></span> 
4. <span data-ttu-id="8f6d4-150">**Gebruikersinteracties** -Hiermee geeft u het aantal berichten welke gebruiker Hallo-app heeft gecommuniceerd met en bevat Hallo-berichten die ondernomen of afgesloten zijn Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-150">**User Interactions** - This specifies hello number of messages which hello app user has interacted with and will include hello messages which are either actioned or exited.</span></span> 
   
   * <span data-ttu-id="8f6d4-151">*Hallo app gebruiker kan actie een melding in een van de volgende manieren Hallo:*</span><span class="sxs-lookup"><span data-stu-id="8f6d4-151">*hello app user can action a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="8f6d4-152">Als hello notification system/out-van-app-melding is of een in-app-melding verzonden als de melding alleen-lezen en Hallo app gebruiker klikt op Hallo-melding.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-152">If hello notification is a system/out-of-app notification or an in-app notification sent as notification-only then hello app user clicks on hello notification.</span></span>
     2. <span data-ttu-id="8f6d4-153">Als Hallo-bericht een melding in de app met een tekst- of webweergave is of polls Hallo vervolgens app gebruiker klikt op Hallo actieknop in Hallo melding.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-153">If hello notification is an in-app notification with a text or web-view or polls then hello app user clicks on hello Action button in hello notification.</span></span>
     3. <span data-ttu-id="8f6d4-154">Als het Hallo-bericht is een melding in de app met een webweergave vervolgens app de gebruiker klikt op een URL in de webweergave [alleen Android] Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="8f6d4-154">If hello notification is an in-app notification with a web-view then hello app user clicks on a URL in hello web view [Android Only]</span></span>
   * <span data-ttu-id="8f6d4-155">*Hallo app gebruiker kan een melding in een van de volgende manieren Hallo afsluiten:*</span><span class="sxs-lookup"><span data-stu-id="8f6d4-155">*hello app user can exit a notification in either of hello following ways:*</span></span>
     
     1. <span data-ttu-id="8f6d4-156">Hallo knop Sluiten te klikken op Hallo melding rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-156">Clicking hello close button on hello notification directly.</span></span> 
     2. <span data-ttu-id="8f6d4-157">Lezer weg of Hallo melding verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-157">Swiping away or deleting hello notification.</span></span> 
     3. <span data-ttu-id="8f6d4-158">In-app-meldingen met tekst of web-inhoud en polls zijn doorgaans weergegeven toohello app gebruiker in een proces in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-158">In-app notifications with text/web content and polls are typically displayed toohello app user in a two-step process.</span></span> <span data-ttu-id="8f6d4-159">Ze eerst een melding te zien en wanneer ze op het klikt, zien ze Hallo daaropvolgende tekst/web/poll-inhoud.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-159">They see a notification first and when they click on it, they see hello subsequent text/web/poll content.</span></span> <span data-ttu-id="8f6d4-160">Hallo app gebruiker een melding in een van deze stappen kunt afsluiten en details in de geavanceerde weergave Hallo Hallo wordt dit vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-160">hello app user can exit a notification in either of these steps and hello details in hello Advanced view captures this.</span></span> 
5. <span data-ttu-id="8f6d4-161">**Ondernomen** -Hiermee geeft u het aantal berichten die expliciet waarop actie is ondernomen door Hallo app gebruiker waren Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-161">**Actioned** - This specifies hello number of messages which were explicitly actioned by hello app user.</span></span> <span data-ttu-id="8f6d4-162">Dit is de meest interessante aantal Hallo zoals dit geeft aan hoeveel gebruikers van de app zijn geïnteresseerd zijn door u in Hallo melding gepusht het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-162">This is hello most interesting number as this tells how many app users were interested by hello message you pushed out in hello notification.</span></span> 

> [!NOTE]
> <span data-ttu-id="8f6d4-163">Op iOS & Windows-platforms, als de gebruiker Hallo Hallo app openen en Hallo campagne is een campagne 'Op elk gewenst moment' dan is het mogelijk dat beide buiten de app en in-app-meldingen worden weergegeven op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-163">On iOS & Windows platforms, if hello user has hello app open and hello campaign was an "AnyTime" campaign then it is possible that both out of app and in-app notifications are displayed at hello same time.</span></span> <span data-ttu-id="8f6d4-164">Dit kan leiden tot een telling weergegeven hoger is dan Hallo geleverd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-164">This may cause a Displayed count higher than hello Delivered.</span></span> <span data-ttu-id="8f6d4-165">Als gebruiker Hallo werkt of acties Hallo melding vervolgens zelfs Hallo gebruiker interacties/Actioned aantal kan niet groter zijn dan geleverd.</span><span class="sxs-lookup"><span data-stu-id="8f6d4-165">If hello user interacts or actions hello notification, then even hello User Interactions/Actioned count could be greater than Delivered.</span></span> 
> 
> 

![Reach2][19]

## <a name="see-also"></a><span data-ttu-id="8f6d4-167">Zie ook</span><span class="sxs-lookup"><span data-stu-id="8f6d4-167">See also</span></span>
* <span data-ttu-id="8f6d4-168">[Concepten][Link 6]</span><span class="sxs-lookup"><span data-stu-id="8f6d4-168">[Concepts][Link 6]</span></span>
* <span data-ttu-id="8f6d4-169">[Troubleshooting Guide-Service][Link 24]</span><span class="sxs-lookup"><span data-stu-id="8f6d4-169">[Troubleshooting Guide Service][Link 24]</span></span>

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md


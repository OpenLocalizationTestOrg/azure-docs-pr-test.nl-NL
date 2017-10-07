---
title: aaaAzure gebruikersinterface van de Mobile Engagement - segmenten
description: Meer informatie over hoe toocreate en segmenten van Azure Mobile Engagement met gebruikspatronen van tooidentify van gebruikers beheren
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6a4f2205-4a3c-406e-a04f-5e6f2a36653f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bb214c45d05ebfbf243978658a7e331d4a7c6e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-segments-of-users-tooidentify-usage-patterns"></a><span data-ttu-id="0ce24-103">Hoe toocreate en segmenten van gebruikers tooidentify gebruikspatronen beheren</span><span class="sxs-lookup"><span data-stu-id="0ce24-103">How toocreate and manage segments of users tooidentify usage patterns</span></span>
<span data-ttu-id="0ce24-104">Dit artikel wordt beschreven Hallo **segmenten** tabblad Hallo **Mobile Engagement** portal.</span><span class="sxs-lookup"><span data-stu-id="0ce24-104">This article describes hello **SEGMENTS** tab of hello **Mobile Engagement** portal.</span></span> <span data-ttu-id="0ce24-105">Gebruik van Hallo **Mobile Engagement** portal toomonitor en beheren van uw mobiele apps.</span><span class="sxs-lookup"><span data-stu-id="0ce24-105">You use hello **Mobile Engagement** portal toomonitor and manage your mobile apps.</span></span>

<span data-ttu-id="0ce24-106">Hallo segmenten sectie Hallo UI kunt u toowork op uw gebruikers op basis van Hallo verschillend gedrag en analyses die u kunt ophalen uit de toepassing hello en is ook toegankelijk via Hallo segmenten API segmenteren.</span><span class="sxs-lookup"><span data-stu-id="0ce24-106">hello Segments section of hello UI allows you toowork on segmenting your users based on hello different behavior and analytics that you can get from hello application and can also access through hello Segments API.</span></span> <span data-ttu-id="0ce24-107">Segmenten worden eerst 24 uur nadat ze zijn gemaakt en zijn ze elke 24 uur op basis van de meest recente analytics informatie Hallo opnieuw berekend.</span><span class="sxs-lookup"><span data-stu-id="0ce24-107">Segments are first computed 24 hours after they are created, and they are recomputed every 24 hours based on hello latest analytics information.</span></span> <span data-ttu-id="0ce24-108">Zodra een segment wordt berekend, het 'Dag tooday geschiedenis' geeft een grafiek weer per dag.</span><span class="sxs-lookup"><span data-stu-id="0ce24-108">Once a segment is calculated, it displays a "Day tooday history" chart each day.</span></span>

> [!NOTE]
> <span data-ttu-id="0ce24-109">Veel secties Hallo **Mobile Engagement** gebruikersinterface portal bevatten Hallo **HELP weergeven** knop.</span><span class="sxs-lookup"><span data-stu-id="0ce24-109">Many sections of hello **Mobile Engagement** portal UI contain hello **SHOW HELP** button.</span></span> <span data-ttu-id="0ce24-110">Druk op deze knop tooget meer contextuele informatie over een sectie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-110">Press this button tooget more contextual information about a section.</span></span>
> 
> 

## <a name="create-segments"></a><span data-ttu-id="0ce24-111">Segmenten maken</span><span class="sxs-lookup"><span data-stu-id="0ce24-111">Create Segments</span></span>
<span data-ttu-id="0ce24-112">U kunt een segment dat op basis van criteria too10 van een bepaalde periode too60 dagen in Hallo maken vanuit Hallo analytics-sectie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-112">You can create a segment based on up too10 criteria on a specific period up too60 days in hello past from hello analytics section.</span></span> <span data-ttu-id="0ce24-113">U kunt bijvoorbeeld een segment op basis van Hallo personen die hebben bekeken bepaalde pagina's of gezocht naar specifieke inhoud in uw app binnen Hallo laatste 10 dagen maken.</span><span class="sxs-lookup"><span data-stu-id="0ce24-113">For example, you can create a segment based on hello people who have viewed certain pages or searched for specific content within your app within hello last 10 days.</span></span> <span data-ttu-id="0ce24-114">Deze informatie is beschikbaar in Hallo analytics-sectie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-114">This information is available in hello analytics section.</span></span> <span data-ttu-id="0ce24-115">Ja, u kunt toocreate een segment worden gebruikt en stelt u een push notification-tootarget deze subset van gebruikers tooget ze toocome back toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ce24-115">So, you can use it toocreate a segment, and then set up a push notification tootarget this subset of users tooget them toocome back toohello application.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ce24-116">Zodra een segment is berekend, kan niet worden bewerkt. Deze kan alleen worden gekloond (kopiëren) of vernietigd (verwijderd).</span><span class="sxs-lookup"><span data-stu-id="0ce24-116">Once a segment has been calculated, it cannot be edited; it can only be cloned (copied) or destroyed (deleted).</span></span> <span data-ttu-id="0ce24-117">Een segment kan worden gekloond binnen Hallo dezelfde toepassing (met dezelfde AppID Hallo), en deze ook in andere toepassingen (met een andere AppID) kan worden gekloond.</span><span class="sxs-lookup"><span data-stu-id="0ce24-117">A segment can be cloned within hello same application (with hello same AppID), and it can also be cloned into other applications (with a different AppID).</span></span> 

 ![segments1][35] 

## <a name="examples-segments"></a><span data-ttu-id="0ce24-119">Segmenten van voorbeelden</span><span class="sxs-lookup"><span data-stu-id="0ce24-119">Examples Segments</span></span>
 ![segments2][36]

<span data-ttu-id="0ce24-121">Segmenten kunnen u toosegment Hallo eindgebruikers van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ce24-121">Segments allow you toosegment hello end-users of your application.</span></span>
<span data-ttu-id="0ce24-122">Uw gebruikers te segmenteren is een belangrijk marketingstrategie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-122">Segmenting your users is an important marketing strategy.</span></span> <span data-ttu-id="0ce24-123">Azure Mobile Engagement kunt u historische gegevens tooget en aangepaste segmenten maken.</span><span class="sxs-lookup"><span data-stu-id="0ce24-123">Azure Mobile Engagement allows you tooget historic data and create custom segments.</span></span> <span data-ttu-id="0ce24-124">Deze krachtige hulpprogramma kunt u toolearn over uw klanten ervaring in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="0ce24-124">This powerful tool enables you toolearn about your customers’ experience in your application.</span></span> <span data-ttu-id="0ce24-125">U kunt eenvoudig uw segmenten analyseren en gebruik van de segmenten als push-doelen.</span><span class="sxs-lookup"><span data-stu-id="0ce24-125">You can easily analyze your segments and use your segments as push targets.</span></span>
<span data-ttu-id="0ce24-126">Een algemene gebruiksvoorbeeld is dat u wilt dat een push-een melding tooencourage toosend uw eindgebruikers toorate uw toepassing in Hallo store.</span><span class="sxs-lookup"><span data-stu-id="0ce24-126">A common use-case is that you want toosend a push a notification tooencourage your end-users toorate your application in hello store.</span></span> <span data-ttu-id="0ce24-127">In plaats van een tooall melding verzenden van uw eindgebruikers, kunt u een segment dat geeft alleen gebruikers die uw toepassing elke dag gebruikt voor Hallo afgelopen maand en een goede gebruikerservaring hebben gehad.</span><span class="sxs-lookup"><span data-stu-id="0ce24-127">Rather than sending a notification tooall your end-users, you can create a segment that would specify only users that have used your application every day for hello last month and have had a great user experience.</span></span> <span data-ttu-id="0ce24-128">Als u minder, maximaal gerichte pushmeldingen verzenden, krijgt u een betere rendement.</span><span class="sxs-lookup"><span data-stu-id="0ce24-128">When you send fewer, highly targeted push notifications, you get a better ROI.</span></span>

 ![segments3][37]

### <a name="segments-you-can-create-based-on-hello-major-azure-mobile-engagement-elements"></a><span data-ttu-id="0ce24-130">Segmenten die u kunt maken op basis van Hallo belangrijke Azure Mobile Engagement elementen:</span><span class="sxs-lookup"><span data-stu-id="0ce24-130">Segments you can create based on hello major Azure Mobile Engagement elements:</span></span>
* <span data-ttu-id="0ce24-131">Gebeurtenis: een segment maken die doelen een specifieke gebeurtenis van de toepassing hello die hebben plaatsgevonden om meer dan tweemaal per week.</span><span class="sxs-lookup"><span data-stu-id="0ce24-131">Event: create a segment that targets one specific event of hello application that happened more than twice a week.</span></span> 
* <span data-ttu-id="0ce24-132">Sessie: Maak een segment van gebruikers die hebben gebruikt Hallo toepassing meer dan 5 maal afgelopen week.</span><span class="sxs-lookup"><span data-stu-id="0ce24-132">Session: create a segment of users that have used hello application more than 5 times last week.</span></span>
* <span data-ttu-id="0ce24-133">Activiteit: een segment van gebruikers die zijn gebruikt op één pagina of inhoud groter of kleiner zijn dan 10 tijd afgelopen maand maken.</span><span class="sxs-lookup"><span data-stu-id="0ce24-133">Activity: create a segment of users that have used one page or content more or less than 10 time last month.</span></span>
* <span data-ttu-id="0ce24-134">Taak: Maak een segment van gebruikers die een taak meer dan twee keer per dag hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="0ce24-134">Job: create a segment of users that have completed a job more than twice a day.</span></span>
* <span data-ttu-id="0ce24-135">Crash: Maak een segment van alle Hallo gebruikers waarvoor een crash maximaal 10 keer afgelopen week.</span><span class="sxs-lookup"><span data-stu-id="0ce24-135">Crash: create a segment of all hello users that have had a crash more than 10 times last week.</span></span> <span data-ttu-id="0ce24-136">(U kunt dit segment met een verontschuldiging of zelfs een coupon kan push!)</span><span class="sxs-lookup"><span data-stu-id="0ce24-136">(You could push this segment with an apology or even a coupon!)</span></span>
* <span data-ttu-id="0ce24-137">Fout: een segment van alle Hallo-gebruikers die een fout meer dan laatste 100 keer 3 dagen hebben gehad maken.</span><span class="sxs-lookup"><span data-stu-id="0ce24-137">Error: create a segment of all hello users that have had an error more than 100 times last 3 days.</span></span>
* <span data-ttu-id="0ce24-138">App-Info: Maak een segment die gericht is op een aangepaste App-Info die hebben plaatsgevonden tijdens het Hallo afgelopen 25 dagen.</span><span class="sxs-lookup"><span data-stu-id="0ce24-138">App Info: create a segment that targets a custom App Info that happened during hello last 25 days.</span></span>
  
  ![segments4][38]

<span data-ttu-id="0ce24-140">toouse Segment optimaal, moet u hebben gedaan een aangepaste integratie van Hallo SDK in uw toepassing met een tagging plan van 'App-Info' labels.</span><span class="sxs-lookup"><span data-stu-id="0ce24-140">toouse Segment in an optimal way, you must have done a customized integration of hello SDK in your application with a tagging plan of "App Info" tags.</span></span>
<span data-ttu-id="0ce24-141">Ga vervolgens toohello startpagina van Hallo interface, selecteert u Hallo-toepassing u wilt en klik op Hallo 'Segmenten' sectie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-141">Then, go toohello home page of hello interface, select hello application you want and click on hello "Segments" section.</span></span>

1. <span data-ttu-id="0ce24-142">Selecteer Hallo 'Segmenten' sectie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-142">Select hello "Segments" section.</span></span>
2. <span data-ttu-id="0ce24-143">Klik op 'Nieuw segment' hello knop toocreate een nieuw segment.</span><span class="sxs-lookup"><span data-stu-id="0ce24-143">Click on hello "New segment" button toocreate a new segment.</span></span>

## <a name="real-life-example-create-a-simple-segment-based-on-session-information"></a><span data-ttu-id="0ce24-144">Echte levensduur voorbeeld: Een eenvoudige segment op basis van ' sessiegegevens ' maken</span><span class="sxs-lookup"><span data-stu-id="0ce24-144">Real Life Example: Create a simple segment based on "Session" information</span></span>
<span data-ttu-id="0ce24-145">Een segment van alle Hallo eindgebruikers die uw app ten minste 50 keer in de afgelopen week Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="0ce24-145">Create a segment of all hello end-users that have used your app at least 50 times in hello last week.</span></span> <span data-ttu-id="0ce24-146">Van daaruit vinden alleen Hallo eindgebruikers die ten minste 30 seconden in uw app per sessie uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="0ce24-146">From there, find only hello end-users that have spent at least 30 seconds in your app per session.</span></span> <span data-ttu-id="0ce24-147">Hier ziet alle Hallo eindgebruikers die een positieve ervaring in uw app hebben.</span><span class="sxs-lookup"><span data-stu-id="0ce24-147">This will show all hello end-users who have a positive experience in your app.</span></span> <span data-ttu-id="0ce24-148">Vervolgens Hallo segment gemaakt gebruikte toopush een melding toothese eindgebruikers tooask kan worden ze toorate uw app in Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="0ce24-148">Then, hello segment created could be used toopush a notification toothese end-users tooask them toorate your app in hello store.</span></span>

 ![segments5][39]

1. <span data-ttu-id="0ce24-150">Geef het segment een naam in de volgorde toofind snel in Hallo 'Segment' lijst.</span><span class="sxs-lookup"><span data-stu-id="0ce24-150">Give your segment a name in order toofind it quickly in hello "Segment" list.</span></span>
2. <span data-ttu-id="0ce24-151">Klik op Hallo 'Maken'.</span><span class="sxs-lookup"><span data-stu-id="0ce24-151">Click on hello "Create" button.</span></span>
   
   ![segments6][40]

<span data-ttu-id="0ce24-153">Selecteer de sessie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-153">Select Session.</span></span>

 ![segments7][41]

1. <span data-ttu-id="0ce24-155">Selecteer 'Afgelopen week' hello periode.</span><span class="sxs-lookup"><span data-stu-id="0ce24-155">Select hello period of "Last week".</span></span>
2. <span data-ttu-id="0ce24-156">Klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="0ce24-156">Click next.</span></span>
   
   ![segments8][42]
3. <span data-ttu-id="0ce24-158">Selecteer Hallo Operator die relevant is uit de lijst Hallo: =; ≥, ≤.</span><span class="sxs-lookup"><span data-stu-id="0ce24-158">Select hello Operator that is relevant among hello list: =; ≥, ≤.</span></span>
4. <span data-ttu-id="0ce24-159">Hallo aantal die u wilt opgeven.</span><span class="sxs-lookup"><span data-stu-id="0ce24-159">Enter hello Count you want.</span></span>
5. <span data-ttu-id="0ce24-160">Hallo-exemplaar dat u wilt selecteren.</span><span class="sxs-lookup"><span data-stu-id="0ce24-160">Select hello Occurrence you want.</span></span> 
6. <span data-ttu-id="0ce24-161">Klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="0ce24-161">Click next.</span></span>
   <span data-ttu-id="0ce24-162">In dit voorbeeld is ingesteld dat via Hallo afgelopen week overeen met gebruikers die ten minste 50 sessies hebt aangebracht.</span><span class="sxs-lookup"><span data-stu-id="0ce24-162">This example is set so that over hello last week, match users that have made at least 50 sessions.</span></span>
   
   ![segments9][43]

<span data-ttu-id="0ce24-164">Hallo segmentering sessie kunt u Hallo lengte per sessie als een criterium.</span><span class="sxs-lookup"><span data-stu-id="0ce24-164">For hello Session segmentation, you can choose hello length per session as a criteria.</span></span>

1. <span data-ttu-id="0ce24-165">Hallo Operator in Hallo lijst selecteren.</span><span class="sxs-lookup"><span data-stu-id="0ce24-165">Select hello Operator from hello list.</span></span>
2. <span data-ttu-id="0ce24-166">Geef Hallo lengte per sessie.</span><span class="sxs-lookup"><span data-stu-id="0ce24-166">Provide hello Length per session.</span></span>
3. <span data-ttu-id="0ce24-167">Klik op Volgende.</span><span class="sxs-lookup"><span data-stu-id="0ce24-167">Click Next.</span></span>
   <span data-ttu-id="0ce24-168">In dit voorbeeld wordt aangegeven dat op alle hello sessies die hebben zijn gesegmenteerd op Hallo exemplaar sectie selecteert Hallo alleen gebruikers die meer dan 30 seconden per sessie uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="0ce24-168">In this example, it says that over all hello sessions that have been segmented on hello occurrence section, select only hello users that have spent more than 30 seconds per session.</span></span>
   
   ![segments10][44]

<span data-ttu-id="0ce24-170">Naam van uw criterium in volgorde tooretrieve in Hallo voltooien trechter, en klik op voltooien.</span><span class="sxs-lookup"><span data-stu-id="0ce24-170">Name your criterion in order tooretrieve it in hello complete funnel, and click Finish.</span></span>

 ![segments11][45]

<span data-ttu-id="0ce24-172">Wanneer u hebt ingesteld uw criterium wordt weergegeven in Hallo segment trechter.</span><span class="sxs-lookup"><span data-stu-id="0ce24-172">When you have finished setting up your criterion, it will appear in hello segment funnel.</span></span>
<span data-ttu-id="0ce24-173">Omdat een segment is gebaseerd op analytische gegevens, worden één keer per dag segmenten berekend.</span><span class="sxs-lookup"><span data-stu-id="0ce24-173">Because a segment is based on analytics data, segments are computed once per day.</span></span>
<span data-ttu-id="0ce24-174">In dit voorbeeld 47,7% van de totale eindgebruikers Hallo komt overeen met de Hallo criterium.</span><span class="sxs-lookup"><span data-stu-id="0ce24-174">In this example, 47,7% of hello total end-users matched hello criterion.</span></span> <span data-ttu-id="0ce24-175">Ze moeten Hallo-gebruikers die een goede ervaring hebben gehad en zal worden waarschijnlijk tooprovide een hogere classificatie als u push ze een melding waarin deze toorate Hallo-app in Hallo store.</span><span class="sxs-lookup"><span data-stu-id="0ce24-175">They should be hello users who have had a good experience and will be likely tooprovide a higher rating if you push them a notification asking them toorate hello app in hello store.</span></span>

## <a name="see-also"></a><span data-ttu-id="0ce24-176">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0ce24-176">See also</span></span>
* <span data-ttu-id="0ce24-177">[Concepten][Link 6]</span><span class="sxs-lookup"><span data-stu-id="0ce24-177">[Concepts][Link 6]</span></span>
* <span data-ttu-id="0ce24-178">[Troubleshooting Guide-Service][Link 24]</span><span class="sxs-lookup"><span data-stu-id="0ce24-178">[Troubleshooting Guide Service][Link 24]</span></span>

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
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md


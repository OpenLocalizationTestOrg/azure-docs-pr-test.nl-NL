---
title: Gebruik Emoji emoticons binnen Azure Mobile Engagement
description: Het gebruik van Emoji emoticons binnen uw pushmeldingen
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 663317d7-3c93-4e8f-b13d-c6fb342124ee
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: bbb7ce5e95b229a7505c5e97b6866d5a302a1d27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-emoji-emoticon-within-push-notifications"></a><span data-ttu-id="ceee5-103">Gebruik Emoji emoticon binnen Pushmeldingen</span><span class="sxs-lookup"><span data-stu-id="ceee5-103">Use Emoji emoticon within Push Notifications</span></span>
<span data-ttu-id="ceee5-104">U kunt opnemen Emoji emoticons in u push-melding in een paar eenvoudige stappen:</span><span class="sxs-lookup"><span data-stu-id="ceee5-104">You can include Emoji emoticons in you push notification in a few easy steps:</span></span> 

1. <span data-ttu-id="ceee5-105">Ten eerste moet u de Emoji zoeken u in het bericht te verzenden.</span><span class="sxs-lookup"><span data-stu-id="ceee5-105">First of all you need to find the Emoji you want to send in the message.</span></span> <span data-ttu-id="ceee5-106">Zorg ervoor dat de Emoji die u selecteert worden ondersteund door het doelapparaat als apparaat fabrikanten enige tijd duren om nieuwe goedgekeurde Emojis toevoegen aan de apparaatplatforms.</span><span class="sxs-lookup"><span data-stu-id="ceee5-106">Please ensure that the Emoji you are selecting will be supported by the target device as device manufactures take some time to add newly approved Emojis to the device platforms.</span></span> 
2. <span data-ttu-id="ceee5-107">Op **Windows** -u kunt navigeren naar deze [koppeling](http://apps.timwhitlock.info/emoji/tables/unicode) en kopieer het pictogram 'Native'.</span><span class="sxs-lookup"><span data-stu-id="ceee5-107">On **Windows** - you can navigate to this [link](http://apps.timwhitlock.info/emoji/tables/unicode) and copy the 'Native' icon.</span></span>
   
    ![][7] 
3. <span data-ttu-id="ceee5-108">Op **Mac** -vindt u de Emojis in woordenboek toepassing onder Edit -> Emoji & symbolen.</span><span class="sxs-lookup"><span data-stu-id="ceee5-108">On **Mac** - you can find the Emojis in Dictionary application under Edit -> Emoji & Symbols.</span></span>
   
    ![][6] 
4. <span data-ttu-id="ceee5-109">Nu gaat u naar de **bereiken** tabblad op de de Azure Mobile Engagement-portal.</span><span class="sxs-lookup"><span data-stu-id="ceee5-109">Now, go to the **Reach** tab on the the Azure Mobile Engagement portal.</span></span> <span data-ttu-id="ceee5-110">Selecteer het type van de push-melding (aankondiging, peilt enzovoort).</span><span class="sxs-lookup"><span data-stu-id="ceee5-110">Select the type of your push notification (Announcement, polls etc).</span></span> <span data-ttu-id="ceee5-111">In dit voorbeeld kiest u een aankondiging push.</span><span class="sxs-lookup"><span data-stu-id="ceee5-111">For this example we choose an announcement push.</span></span>
5. <span data-ttu-id="ceee5-112">Geef de verschillende velden van de melding totdat u de tekst van de melding.</span><span class="sxs-lookup"><span data-stu-id="ceee5-112">Specify the different fields of the notification until you reach the text of the notification.</span></span> <span data-ttu-id="ceee5-113">Dit is waar u uw Emoji Emoticon toevoegt.</span><span class="sxs-lookup"><span data-stu-id="ceee5-113">This is where you will add your Emoji Emoticon.</span></span> <span data-ttu-id="ceee5-114">U kunt kiezen in de titel en/of het bericht te plaatsen.</span><span class="sxs-lookup"><span data-stu-id="ceee5-114">You can choose to put it in the title, the message, or both.</span></span> <span data-ttu-id="ceee5-115">U moet slepen en neerzetten of kopiëren van de Emoji die u in de bovenstaande locaties vinden.</span><span class="sxs-lookup"><span data-stu-id="ceee5-115">You will need to drag and drop or copy the Emoji that you find from the locations above.</span></span> 
   
    ![][1]
6. <span data-ttu-id="ceee5-116">Vul de overige velden voor de melding en opslaan.</span><span class="sxs-lookup"><span data-stu-id="ceee5-116">Complete the other fields for the notification and save it.</span></span> 
7. <span data-ttu-id="ceee5-117">Als u een test uitvoert of activeren van de aankondiging ziet u een melding met de emoticon zoals opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ceee5-117">When you run a test or activate the announcement you will see a notification with the emoticon as specified.</span></span>   
   
    <span data-ttu-id="ceee5-118">![][3] ![][4] ![][5]</span><span class="sxs-lookup"><span data-stu-id="ceee5-118">![][3] ![][4] ![][5]</span></span>

<!-- Images. -->
[1]: ./media/mobile-engagement-use-emoji-with-push/notification_input.png
[3]: ./media/mobile-engagement-use-emoji-with-push/iOS_Emoji.png
[4]: ./media/mobile-engagement-use-emoji-with-push/Android_Emoji.png
[5]: ./media/mobile-engagement-use-emoji-with-push/WindowsPhone_Emoji.png
[6]: ./media/mobile-engagement-use-emoji-with-push/Mac_SelectEmoji.png
[7]: ./media/mobile-engagement-use-emoji-with-push/Windows_SelectEmoji.png


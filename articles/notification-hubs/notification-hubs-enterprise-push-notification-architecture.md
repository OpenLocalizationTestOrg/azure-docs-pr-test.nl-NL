---
title: aaaNotification Hubs - Push ondernemingsstructuur
description: Richtlijnen over het gebruik van Azure Notification Hubs in een bedrijfsomgeving
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 903023e9-9347-442a-924b-663af85e05c6
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c3afb83de1ba0882bf99e10f38cca40cb42d07a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="2f66b-103">Hulp voor architectuur via pushmeldingen van het bedrijf</span><span class="sxs-lookup"><span data-stu-id="2f66b-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="2f66b-104">Ondernemingen zijn tegenwoordig geleidelijk verplaatsen naar het maken van mobiele toepassingen voor hun eindgebruikers (extern) of voor Hallo werknemers (intern).</span><span class="sxs-lookup"><span data-stu-id="2f66b-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for hello employees (internal).</span></span> <span data-ttu-id="2f66b-105">Ze hebben bestaande back-endsystemen worden deze mainframes of sommige LoB-toepassingen die moeten worden geïntegreerd in de architectuur van de mobiele toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="2f66b-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into hello mobile application architecture.</span></span> <span data-ttu-id="2f66b-106">Deze handleiding wordt hebben over de beste manier toodo deze integratie mogelijke oplossing aanbevelen toocommon scenario's.</span><span class="sxs-lookup"><span data-stu-id="2f66b-106">This guide will talk about how best toodo this integration recommending possible solution toocommon scenarios.</span></span>

<span data-ttu-id="2f66b-107">Een frequente vereiste is voor het verzenden van push notification toohello gebruikers via hun mobiele toepassing bij een gebeurtenis van belang zijn in Hallo back-end-systemen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-107">A frequent requirement is for sending push notification toohello users through their mobile application when an event of interest occurs in hello backend systems.</span></span> <span data-ttu-id="2f66b-108">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="2f66b-108">E.g.</span></span> <span data-ttu-id="2f66b-109">een klant bank die van de bank Hallo-app voor bankieren op haar iPhone wil toobe gewaarschuwd wanneer er een incasso boven een bepaald bedrag van haar account of een intranet-scenario waarin een medewerker van de afdeling Financiën die een budget goedkeuring app op zijn Windows Phone toobe wil wordt gedaan een melding wanneer hij een goedkeuringsaanvraag opgehaald.</span><span class="sxs-lookup"><span data-stu-id="2f66b-109">a bank customer who has hello bank's banking app on her iPhone wants toobe notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants toobe notified when he gets an approval request.</span></span>

<span data-ttu-id="2f66b-110">bank- of goedkeuring verwerking Hallo is waarschijnlijk toobe doet u in sommige back endsysteem dat een gebruiker van de toohello push moet starten.</span><span class="sxs-lookup"><span data-stu-id="2f66b-110">hello bank account or approval processing is likely toobe done in some backend system which must initiate a push toohello user.</span></span> <span data-ttu-id="2f66b-111">Mogelijk zijn er meerdere dergelijke back-end voor systemen die u moeten alle bouwen Hallo dezelfde soort logica tooimplement push wanneer een gebeurtenis wordt een melding geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="2f66b-111">There may be multiple such backend systems which must all build hello same kind of logic tooimplement push when an event triggers a notification.</span></span> <span data-ttu-id="2f66b-112">Hallo complexiteit hier ligt in verschillende back endsystemen samen met een één push-systeem waar Hallo eindgebruikers mogelijk toodifferent meldingen bent geabonneerd en er kan zelfs meerdere mobiele toepassingen bijvoorbeeld in geval van Hallo van mobiele apps intranet worden integratie een mobiele toepassing wil waar tooreceive meldingen van meerdere dergelijke back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-112">hello complexity here lies in integrating several backend systems together with a single push system where hello end users may have subscribed toodifferent notifications and there may even be multiple mobile applications e.g. in hello case of intranet mobile apps where one mobile application may want tooreceive notifications from multiple such backend systems.</span></span> <span data-ttu-id="2f66b-113">Hallo back-endsystemen niet kent of tooknow van push-semantiek/technologie moet dus een gangbare oplossing hier is normaal een onderdeel dat opgevraagd Hallo back-end-systemen voor gebeurtenissen die van belang en is verantwoordelijk gesproken voor het verzenden van pushberichten hello toointroduce toohello-client.</span><span class="sxs-lookup"><span data-stu-id="2f66b-113">hello backend systems do not know or need tooknow of push semantics/technology so a common solution here traditionally has been toointroduce a component which polls hello backend systems for any events of interest and is responsible for sending hello push messages toohello client.</span></span>
<span data-ttu-id="2f66b-114">Er wordt hier hebben over een nog beter oplossing met behulp van Azure Service Bus - onderwerp/abonnement model waarmee Hallo complexiteit tijdens het maken van Hallo oplossing schaalbaar wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="2f66b-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce hello complexity while making hello solution scalable.</span></span>

<span data-ttu-id="2f66b-115">Hier volgt Hallo algemene architectuur van Hallo-oplossing (gegeneraliseerde met meerdere mobiele apps maar evenveel van toepassing wanneer er slechts één van de mobiele app)</span><span class="sxs-lookup"><span data-stu-id="2f66b-115">Here is hello general architecture of hello solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="2f66b-116">Architectuur</span><span class="sxs-lookup"><span data-stu-id="2f66b-116">Architecture</span></span>
![][1]

<span data-ttu-id="2f66b-117">Hallo belangrijk onderdeel in dit diagram architectuur is Azure Service Bus waarmee een onderwerpen/de abonnementen programmeermodel (meer informatie over op het [Service Bus Pub subitems programmering]).</span><span class="sxs-lookup"><span data-stu-id="2f66b-117">hello key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="2f66b-118">Hallo-ontvanger die in dit geval Hallo mobiele back-end (meestal [Azure Mobile Service], gang een mobiele apps voor push-toohello) niet ontvangen berichten rechtstreeks vanuit de back-endsystemen hello, maar in plaats daarvan hebben we een tussenliggende abstractielaag geleverd door [Azure Service Bus] waardoor mobiele back-end tooreceive berichten van een of meer back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-118">hello receiver, which in this case, is hello Mobile backend (typically [Azure Mobile Service], which will initiate a push toohello mobile apps) does not receive messages directly from hello backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend tooreceive messages from one or more backend systems.</span></span> <span data-ttu-id="2f66b-119">Een Service Bus-onderwerp moet toobe gemaakt voor elk Hallo back-endsystemen bijvoorbeeld Account HR, financiële die eigenlijk 'onderwerpen' van belang dat berichten toobe als push-bericht verzonden wordt geïnitieerd.</span><span class="sxs-lookup"><span data-stu-id="2f66b-119">A Service Bus Topic needs toobe created for each of hello backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages toobe sent as push notification.</span></span> <span data-ttu-id="2f66b-120">Hallo back-endsystemen zal berichten verzenden toothese onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-120">hello backend systems will send messages toothese topics.</span></span> <span data-ttu-id="2f66b-121">Een back-end van Mobile kunnen zich abonneren tooone of meer van deze onderwerpen door het maken van een Service Bus-abonnement.</span><span class="sxs-lookup"><span data-stu-id="2f66b-121">A Mobile Backend can subscribe tooone or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="2f66b-122">Dit recht Hallo mobiele back-end tooreceive een melding van de bijbehorende back-end-systeem Hallo geven.</span><span class="sxs-lookup"><span data-stu-id="2f66b-122">This will entitle hello mobile backend tooreceive a notification from hello corresponding backend system.</span></span> <span data-ttu-id="2f66b-123">Back-end voor mobiele blijft toolisten voor berichten die op hun abonnementen en zodra er een bericht binnenkomt, schakelt terug en verzendt het als melding tooits notification hub.</span><span class="sxs-lookup"><span data-stu-id="2f66b-123">Mobile backend continues toolisten for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification tooits notification hub.</span></span> <span data-ttu-id="2f66b-124">Notification hubs biedt vervolgens uiteindelijk Hallo-bericht toohello mobiele app.</span><span class="sxs-lookup"><span data-stu-id="2f66b-124">Notification hubs then eventually delivers hello message toohello mobile app.</span></span> <span data-ttu-id="2f66b-125">Dus toosummarize Hallo hoofdonderdelen, hebben we:</span><span class="sxs-lookup"><span data-stu-id="2f66b-125">So toosummarize hello key components, we have:</span></span>

1. <span data-ttu-id="2f66b-126">Back-end-systemen (LoB/oudere systemen)</span><span class="sxs-lookup"><span data-stu-id="2f66b-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="2f66b-127">Service Bus-onderwerp maakt</span><span class="sxs-lookup"><span data-stu-id="2f66b-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="2f66b-128">Bericht</span><span class="sxs-lookup"><span data-stu-id="2f66b-128">Sends Message</span></span>
2. <span data-ttu-id="2f66b-129">Mobiele back-end</span><span class="sxs-lookup"><span data-stu-id="2f66b-129">Mobile backend</span></span>
   * <span data-ttu-id="2f66b-130">Service-abonnement wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="2f66b-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="2f66b-131">Ontvangen van bericht (van de back-end-systeem)</span><span class="sxs-lookup"><span data-stu-id="2f66b-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="2f66b-132">Verzendt melding tooclients (via Azure Notification Hub)</span><span class="sxs-lookup"><span data-stu-id="2f66b-132">Sends notification tooclients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="2f66b-133">Mobile Application</span><span class="sxs-lookup"><span data-stu-id="2f66b-133">Mobile Application</span></span>
   * <span data-ttu-id="2f66b-134">Ontvangt en meldingen weergeven</span><span class="sxs-lookup"><span data-stu-id="2f66b-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="2f66b-135">Voordelen:</span><span class="sxs-lookup"><span data-stu-id="2f66b-135">Benefits:</span></span>
1. <span data-ttu-id="2f66b-136">Hallo ontkoppeling Hallo ontvanger (mobiele app/service via Notification Hub) en de afzender (back endsystemen), kunt aanvullende back endsystemen worden geïntegreerd met minimale wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-136">hello decoupling between hello receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="2f66b-137">Hierdoor wordt ook Hallo scenario met meerdere mobiele apps kunnen tooreceive gebeurtenissen van een of meer back endsystemen worden.</span><span class="sxs-lookup"><span data-stu-id="2f66b-137">This also makes hello scenario of multiple mobile apps being able tooreceive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="2f66b-138">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="2f66b-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="2f66b-139">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2f66b-139">Prerequisites</span></span>
<span data-ttu-id="2f66b-140">U moet voltooien Hallo zelfstudies toofamiliarize met Hallo concepten, evenals algemene stappen voor het maken van & configuratie te volgen:</span><span class="sxs-lookup"><span data-stu-id="2f66b-140">You should complete hello following tutorials toofamiliarize with hello concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="2f66b-141">[Service Bus Pub subitems programmering] -Hier wordt uitgelegd hoe Hallo details van het werken met abonnementen/Service Bus onderwerpen, hoe toocreate een naamruimte toocontain onderwerpen/abonnementen, hoe toosend & berichten ontvangen van deze.</span><span class="sxs-lookup"><span data-stu-id="2f66b-141">[Service Bus Pub/Sub programming] - This explains hello details of working with Service Bus Topics/Subscriptions, how toocreate a namespace toocontain topics/subscriptions, how toosend & receive messages from them.</span></span>
2. <span data-ttu-id="2f66b-142">[Notification Hubs - universele Windows-zelfstudie] -dit wordt uitgelegd hoe tooset-up maken van een Windows Store-app Notification Hubs tooregister en gebruik vervolgens meldingen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-142">[Notification Hubs - Windows Universal tutorial] - This explains how tooset up a Windows Store app and use Notification Hubs tooregister and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="2f66b-143">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="2f66b-143">Sample code</span></span>
<span data-ttu-id="2f66b-144">Hallo-code voor het volledige voorbeeld is beschikbaar op [Notification Hub voorbeelden].</span><span class="sxs-lookup"><span data-stu-id="2f66b-144">hello full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="2f66b-145">Deze is opgesplitst in drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="2f66b-145">It is split into three components:</span></span>

1. <span data-ttu-id="2f66b-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="2f66b-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="2f66b-147">a.</span><span class="sxs-lookup"><span data-stu-id="2f66b-147">a.</span></span> <span data-ttu-id="2f66b-148">Dit project gebruikt Hallo *WindowsAzure.ServiceBus* Nuget-pakket en is gebaseerd op [Service Bus Pub subitems programmering].</span><span class="sxs-lookup"><span data-stu-id="2f66b-148">This project uses hello *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="2f66b-149">b.</span><span class="sxs-lookup"><span data-stu-id="2f66b-149">b.</span></span> <span data-ttu-id="2f66b-150">Dit is een eenvoudige C#-console-app toosimulate een LoB-systeem waarmee wordt geïnitieerd Hallo-bericht toobe bezorgd toohello mobiele app.</span><span class="sxs-lookup"><span data-stu-id="2f66b-150">This is a simple C# console app toosimulate an LoB system which initiates hello message toobe delivered toohello mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="2f66b-151">c.</span><span class="sxs-lookup"><span data-stu-id="2f66b-151">c.</span></span> <span data-ttu-id="2f66b-152">`CreateTopic`gebruikte toocreate Hallo Service Bus-onderwerp is waarin berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="2f66b-152">`CreateTopic` is used toocreate hello Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create hello topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="2f66b-153">d.</span><span class="sxs-lookup"><span data-stu-id="2f66b-153">d.</span></span> <span data-ttu-id="2f66b-154">`SendMessage`gebruikte toosend Hallo berichten toothis Service Bus-onderwerp is.</span><span class="sxs-lookup"><span data-stu-id="2f66b-154">`SendMessage` is used toosend hello messages toothis Service Bus Topic.</span></span> <span data-ttu-id="2f66b-155">We zijn een set van willekeurige berichten toohello onderwerp periodiek voor Hallo doel van Hallo voorbeeld hier gewoon verzonden.</span><span class="sxs-lookup"><span data-stu-id="2f66b-155">Here we are simply sending a set of random messages toohello topic periodically for hello purpose of hello sample.</span></span> <span data-ttu-id="2f66b-156">Normaal gesproken zal er een back endsysteem dat berichten verzenden zal wanneer een gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="2f66b-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds toohello topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched tooa different team."
            };
   
            while (true)
            {
                Random rnd = new Random();
                string employeeId = rnd.Next(10000, 99999).ToString();
                string notification = String.Format(messages[rnd.Next(0,messages.Length)], employeeId);
   
                // Send Notification
                BrokeredMessage message = new BrokeredMessage(notification);
                client.Send(message);
   
                Console.WriteLine("{0} Message sent - '{1}'", DateTime.Now, notification);
   
                System.Threading.Thread.Sleep(new TimeSpan(0, 0, 10));
            }
        }
2. <span data-ttu-id="2f66b-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="2f66b-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="2f66b-158">a.</span><span class="sxs-lookup"><span data-stu-id="2f66b-158">a.</span></span> <span data-ttu-id="2f66b-159">Dit project gebruikt Hallo *WindowsAzure.ServiceBus* en *Microsoft.Web.WebJobs.Publish* Nuget-pakketten en is gebaseerd op [Service Bus Pub subitems programmering].</span><span class="sxs-lookup"><span data-stu-id="2f66b-159">This project uses hello *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="2f66b-160">b.</span><span class="sxs-lookup"><span data-stu-id="2f66b-160">b.</span></span> <span data-ttu-id="2f66b-161">Dit is een andere C#-consoletoepassing die wordt uitgevoerd als een [Azure webtaak] omdat het toorun continu heeft toolisten voor berichten van Hallo LoB/back-end-systemen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-161">This is another C# console app which we will run as an [Azure WebJob] since it has toorun continuously toolisten for messages from hello LoB/backend systems.</span></span> <span data-ttu-id="2f66b-162">Dit zal onderdeel zijn van uw mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="2f66b-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="2f66b-163">c.</span><span class="sxs-lookup"><span data-stu-id="2f66b-163">c.</span></span> <span data-ttu-id="2f66b-164">`CreateSubscription`is gebruikte toocreate een Service Bus-abonnement voor Hallo onderwerp Hallo back-end-systeem zal waar berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="2f66b-164">`CreateSubscription` is used toocreate a Service Bus subscription for hello topic where hello backend system will send messages.</span></span> <span data-ttu-id="2f66b-165">Afhankelijk van het bedrijfsscenario hello maakt dit onderdeel u een of meer abonnementen toocorresponding onderwerpen (bv. Sommige kan worden ontvangen van berichten van HR-systeem, sommige vanuit Financiën system, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="2f66b-165">Depending on hello business scenario, this component will create one or more subscriptions toocorresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create hello subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="2f66b-166">d.</span><span class="sxs-lookup"><span data-stu-id="2f66b-166">d.</span></span> <span data-ttu-id="2f66b-167">ReceiveMessageAndSendNotification gebruikte tooread Hallo-bericht van Hallo onderwerp met behulp van het abonnement is en als Hallo lezen slaagt vervolgens stellen van een mobiele melding (in de voorbeeldscenario een systeemeigen pop-upmelding voor Windows hello) toobe verzonden toohello een toepassing met Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="2f66b-167">ReceiveMessageAndSendNotification is used tooread hello message from hello topic using its subscription and if hello read is successful then craft a notification (in hello sample scenario a Windows native toast notification) toobe sent toohello mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize hello Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from hello subscription
            while (true)
            {
                BrokeredMessage message = Client.Receive();
                var toastMessage = @"<toast><visual><binding template=""ToastText01""><text id=""1"">{messagepayload}</text></binding></visual></toast>";
   
                if (message != null)
                {
                    try
                    {
                        Console.WriteLine(message.MessageId);
                        Console.WriteLine(message.SequenceNumber);
                        string messageBody = message.GetBody<string>();
                        Console.WriteLine("Body: " + messageBody + "\n");
   
                        toastMessage = toastMessage.Replace("{messagepayload}", messageBody);
                        SendNotificationAsync(toastMessage);
   
                        // Remove message from subscription
                        message.Complete();
                    }
                    catch (Exception)
                    {
                        // Indicate a problem, unlock message in subscription
                        message.Abandon();
                    }
                }
            }
        }
        static async void SendNotificationAsync(string message)
        {
            await hub.SendWindowsNativeNotificationAsync(message);
        }
   
    <span data-ttu-id="2f66b-168">e.</span><span class="sxs-lookup"><span data-stu-id="2f66b-168">e.</span></span> <span data-ttu-id="2f66b-169">Voor het publiceren van dit als een **webtaak**, klik met de rechtermuisknop op het Hallo-oplossing in Visual Studio en selecteer **publiceren als webtaak**</span><span class="sxs-lookup"><span data-stu-id="2f66b-169">For publishing this as a **WebJob**, right click on hello solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="2f66b-170">f.</span><span class="sxs-lookup"><span data-stu-id="2f66b-170">f.</span></span> <span data-ttu-id="2f66b-171">Uw publicatieprofiel selecteren en maken van een nieuwe Azure-WebSite als deze niet al host die deze webtaak en zodra er Hallo WebSite vervolgens **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="2f66b-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have hello WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="2f66b-172">g.</span><span class="sxs-lookup"><span data-stu-id="2f66b-172">g.</span></span> <span data-ttu-id="2f66b-173">Taak toobe 'Continu uitvoeren' hello zodanig configureren dat wanneer u zich toohello aanmeldt [klassieke Azure-Portal] u ziet er ongeveer zo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="2f66b-173">Configure hello job toobe "Run Continuously" so that when you log in toohello [Azure Classic Portal] you should see something like hello following:</span></span>
   
    ![][4]
3. <span data-ttu-id="2f66b-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="2f66b-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="2f66b-175">a.</span><span class="sxs-lookup"><span data-stu-id="2f66b-175">a.</span></span> <span data-ttu-id="2f66b-176">Dit is een Windows Store-toepassing die wordt ontvangen pop-upmeldingen uit Hallo webtaak wordt uitgevoerd als onderdeel van uw mobiele back-end en weer te geven.</span><span class="sxs-lookup"><span data-stu-id="2f66b-176">This is a Windows Store application which will receive toast notifications from hello WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="2f66b-177">Dit is gebaseerd op [Notification Hubs - universele Windows-zelfstudie].</span><span class="sxs-lookup"><span data-stu-id="2f66b-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="2f66b-178">b.</span><span class="sxs-lookup"><span data-stu-id="2f66b-178">b.</span></span> <span data-ttu-id="2f66b-179">Zorg ervoor dat uw toepassing ingeschakelde tooreceive pop-upmeldingen.</span><span class="sxs-lookup"><span data-stu-id="2f66b-179">Ensure that your application is enabled tooreceive toast notifications.</span></span>
   
    <span data-ttu-id="2f66b-180">c.</span><span class="sxs-lookup"><span data-stu-id="2f66b-180">c.</span></span> <span data-ttu-id="2f66b-181">Zorg ervoor dat Hallo registratiecode Notification Hubs te volgen op Hallo starten van de App wordt aangeroepen (na het vervangen van Hallo *HubName* en *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="2f66b-181">Ensure that hello following Notification Hubs registration code is being called at hello App start up (after replacing hello *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="2f66b-182">Voorbeeld uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="2f66b-182">Running sample:</span></span>
1. <span data-ttu-id="2f66b-183">Zorg dat uw webtaak correct wordt uitgevoerd en gepland te 'uitvoeren continu'.</span><span class="sxs-lookup"><span data-stu-id="2f66b-183">Ensure that your WebJob is running successfully and scheduled too"Run Continuously".</span></span>
2. <span data-ttu-id="2f66b-184">Voer Hallo **EnterprisePushMobileApp** die Hallo Windows Store-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2f66b-184">Run hello **EnterprisePushMobileApp** which will start hello Windows Store app.</span></span>
3. <span data-ttu-id="2f66b-185">Voer Hallo **EnterprisePushBackendSystem** consoletoepassing die simuleert Hallo LoB back-end en wordt gestart met het verzenden van berichten en ziet u pop-upmeldingen Hallo volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="2f66b-185">Run hello **EnterprisePushBackendSystem** console application which will simulate hello LoB backend and will start sending messages and you should see toast notifications appearing like hello following:</span></span>
   
    ![][5]
4. <span data-ttu-id="2f66b-186">Hallo-berichten zijn tooService Bus-onderwerpen die werd bewaakt door Service Bus-abonnementen in uw Web-taak oorspronkelijk is verzonden.</span><span class="sxs-lookup"><span data-stu-id="2f66b-186">hello messages were originally sent tooService Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="2f66b-187">Wanneer een bericht is ontvangen, wordt een melding is gemaakt, en toohello mobiele app verzonden.</span><span class="sxs-lookup"><span data-stu-id="2f66b-187">Once a message was received, a notification was created and sent toohello mobile app.</span></span> <span data-ttu-id="2f66b-188">U kunt zoeken via Hallo webtaak tooconfirm Hallo verwerken Logboeken wanneer u toohello logboeken koppelen gaat in [klassieke Azure-Portal] voor uw Web-taak:</span><span class="sxs-lookup"><span data-stu-id="2f66b-188">You can look through hello WebJob logs tooconfirm hello processing when you go toohello Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
[Notification Hub voorbeelden]: https://github.com/Azure/azure-notificationhubs-samples
[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/
[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/
[Service Bus Pub subitems programmering]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/
[Azure webtaak]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/
[Notification Hubs - universele Windows-zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/
[klassieke Azure-Portal]: https://manage.windowsazure.com/

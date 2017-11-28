---
title: Notification Hubs - Push ondernemingsstructuur
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
ms.openlocfilehash: ae7c1c9644ecfe7fe4ad6e332cc0683a3b5df22f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-push-architectural-guidance"></a><span data-ttu-id="7ad3e-103">Hulp voor architectuur via pushmeldingen van het bedrijf</span><span class="sxs-lookup"><span data-stu-id="7ad3e-103">Enterprise push architectural guidance</span></span>
<span data-ttu-id="7ad3e-104">Ondernemingen zijn tegenwoordig geleidelijk verplaatsen naar het maken van mobiele toepassingen voor hun eindgebruikers (extern) of voor de werknemers (intern).</span><span class="sxs-lookup"><span data-stu-id="7ad3e-104">Enterprises today are gradually moving towards creating mobile applications for either their end users (external) or for the employees (internal).</span></span> <span data-ttu-id="7ad3e-105">Ze hebben bestaande back-endsystemen mainframes of sommige LoB-toepassingen die moeten worden geïntegreerd in de architectuur van de mobiele toepassing.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-105">They have existing backend systems in place be it mainframes or some LoB applications which must be integrated into the mobile application architecture.</span></span> <span data-ttu-id="7ad3e-106">Deze handleiding wordt hebben over de beste manier om u te doen van deze integratie mogelijke oplossing aanbevelen voor het algemene scenario's.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-106">This guide will talk about how best to do this integration recommending possible solution to common scenarios.</span></span>

<span data-ttu-id="7ad3e-107">Een frequente vereiste is voor het verzenden van pushmeldingen aan de gebruikers via hun mobiele toepassing als een gebeurtenis van belang zijn in de back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-107">A frequent requirement is for sending push notification to the users through their mobile application when an event of interest occurs in the backend systems.</span></span> <span data-ttu-id="7ad3e-108">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="7ad3e-108">E.g.</span></span> <span data-ttu-id="7ad3e-109">een klant bank die de bank-app voor bankieren op haar iPhone wil worden gewaarschuwd wanneer er een incasso wordt gedaan boven een bepaald bedrag van haar account of een intranet-scenario waarin een medewerker van de afdeling Financiën die een budget goedkeuring app op zijn Windows Phone wil worden gewaarschuwd wanneer hij een goedkeuringsaanvraag opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-109">a bank customer who has the bank's banking app on her iPhone wants to be notified when a debit is made above a certain amount from her account or an intranet scenario where an employee from finance department who has a budget approval app on his Windows Phone wants to be notified when he gets an approval request.</span></span>

<span data-ttu-id="7ad3e-110">De bank- of goedkeuring verwerking is het waarschijnlijk worden uitgevoerd in sommige back endsysteem dat een push naar de gebruiker moet starten.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-110">The bank account or approval processing is likely to be done in some backend system which must initiate a push to the user.</span></span> <span data-ttu-id="7ad3e-111">Er zijn meerdere dergelijke back voor endsystemen die u moeten alle dezelfde soort logica voor het implementeren van push wanneer een gebeurtenis wordt geactiveerd een melding maken.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-111">There may be multiple such backend systems which must all build the same kind of logic to implement push when an event triggers a notification.</span></span> <span data-ttu-id="7ad3e-112">De complexiteit hier ligt in het integreren van verschillende back endsystemen samen met een enkele push-systeem waar de eindgebruikers mogelijk andere meldingen bent geabonneerd en er kan zelfs meerdere mobiele toepassingen bijvoorbeeld in het geval van mobiele apps intranet waar een mobiele toepassing kan meldingen wilt ontvangen van meerdere dergelijke back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-112">The complexity here lies in integrating several backend systems together with a single push system where the end users may have subscribed to different notifications and there may even be multiple mobile applications e.g. in the case of intranet mobile apps where one mobile application may want to receive notifications from multiple such backend systems.</span></span> <span data-ttu-id="7ad3e-113">De back endsystemen niet kent of moet weten van push-semantiek/technologie zodat een gangbare oplossing hier is normaal gesproken in te voeren van een onderdeel dat de back endsystemen voor gebeurtenissen die van belang worden opgevraagd en is verantwoordelijk voor de pushberichten verzenden naar de client.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-113">The backend systems do not know or need to know of push semantics/technology so a common solution here traditionally has been to introduce a component which polls the backend systems for any events of interest and is responsible for sending the push messages to the client.</span></span>
<span data-ttu-id="7ad3e-114">Er wordt hier hebben over een nog beter oplossing met behulp van Azure Service Bus - onderwerp/abonnement model waarmee de complexiteit tijdens het maken van de oplossing schaalbaar wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-114">Here we will talk about an even better solution using Azure Service Bus - Topic/Subscription model which will reduce the complexity while making the solution scalable.</span></span>

<span data-ttu-id="7ad3e-115">Hier volgt de algemene architectuur van de oplossing (gegeneraliseerde met meerdere mobiele apps maar evenveel van toepassing wanneer er slechts één van de mobiele app)</span><span class="sxs-lookup"><span data-stu-id="7ad3e-115">Here is the general architecture of the solution (generalized with multiple mobile apps but equally applicable when there is only one mobile app)</span></span>

## <a name="architecture"></a><span data-ttu-id="7ad3e-116">Architectuur</span><span class="sxs-lookup"><span data-stu-id="7ad3e-116">Architecture</span></span>
![][1]

<span data-ttu-id="7ad3e-117">De sleutel in deze Architectuurdiagram is Azure Service Bus waarmee een onderwerpen/de abonnementen programmeermodel (meer informatie over op het [Service Bus Pub subitems programmering]).</span><span class="sxs-lookup"><span data-stu-id="7ad3e-117">The key piece in this architectural diagram is Azure Service Bus which provides a topics/subscriptions programming model (more on it at [Service Bus Pub/Sub programming]).</span></span> <span data-ttu-id="7ad3e-118">De ontvanger, die in dit geval de mobiele back-end wordt (meestal [Azure Mobile Service], gang een push naar de mobiele apps) niet ontvangen berichten rechtstreeks vanuit de back endsystemen, maar in plaats daarvan hebben we een tussenliggende abstractielaag geleverd door [Azure Service Bus] waardoor mobiele back-end om berichten te ontvangen van een of meer back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-118">The receiver, which in this case, is the Mobile backend (typically [Azure Mobile Service], which will initiate a push to the mobile apps) does not receive messages directly from the backend systems but instead we have an intermediate abstraction layer provided by [Azure Service Bus] which enables mobile backend to receive messages from one or more backend systems.</span></span> <span data-ttu-id="7ad3e-119">Een Service Bus-onderwerp moet worden gemaakt voor elk van de back-endsystemen bijvoorbeeld Account HR, financiële die eigenlijk 'onderwerpen' van belang dat berichten worden verzonden als de pushmelding wordt geïnitieerd.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-119">A Service Bus Topic needs to be created for each of the backend systems e.g. Account, HR, Finance which are basically "topics" of interest which will initiate messages to be sent as push notification.</span></span> <span data-ttu-id="7ad3e-120">De back endsystemen zal berichten verzenden naar deze onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-120">The backend systems will send messages to these topics.</span></span> <span data-ttu-id="7ad3e-121">Een back-end van Mobile kunnen zich abonneren op een of meer van deze onderwerpen door het maken van een Service Bus-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-121">A Mobile Backend can subscribe to one or more such topics by creating a Service Bus subscription.</span></span> <span data-ttu-id="7ad3e-122">Dit recht geven de mobiele back-end een melding te ontvangen van de bijbehorende back endsysteem.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-122">This will entitle the mobile backend to receive a notification from the corresponding backend system.</span></span> <span data-ttu-id="7ad3e-123">Back-end voor mobiele blijft om te luisteren naar berichten op hun abonnementen en zodra er een bericht binnenkomt, schakelt terug en verzendt het als melding met de notification hub.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-123">Mobile backend continues to listen for messages on their subscriptions and as soon as a message arrives, it turns back and sends it as notification to its notification hub.</span></span> <span data-ttu-id="7ad3e-124">Notification hubs uiteindelijk bezorgt het bericht vervolgens naar de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-124">Notification hubs then eventually delivers the message to the mobile app.</span></span> <span data-ttu-id="7ad3e-125">Om samen te vatten de hoofdonderdelen, hebben we dus:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-125">So to summarize the key components, we have:</span></span>

1. <span data-ttu-id="7ad3e-126">Back-end-systemen (LoB/oudere systemen)</span><span class="sxs-lookup"><span data-stu-id="7ad3e-126">Backend systems (LoB/Legacy systems)</span></span>
   * <span data-ttu-id="7ad3e-127">Service Bus-onderwerp maakt</span><span class="sxs-lookup"><span data-stu-id="7ad3e-127">Creates Service Bus Topic</span></span>
   * <span data-ttu-id="7ad3e-128">Bericht</span><span class="sxs-lookup"><span data-stu-id="7ad3e-128">Sends Message</span></span>
2. <span data-ttu-id="7ad3e-129">Mobiele back-end</span><span class="sxs-lookup"><span data-stu-id="7ad3e-129">Mobile backend</span></span>
   * <span data-ttu-id="7ad3e-130">Service-abonnement wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="7ad3e-130">Creates Service Subscription</span></span>
   * <span data-ttu-id="7ad3e-131">Ontvangen van bericht (van de back-end-systeem)</span><span class="sxs-lookup"><span data-stu-id="7ad3e-131">Receives Message (from Backend system)</span></span>
   * <span data-ttu-id="7ad3e-132">Wordt een melding verzonden naar clients (via Azure Notification Hub)</span><span class="sxs-lookup"><span data-stu-id="7ad3e-132">Sends notification to clients (via Azure Notification Hub)</span></span>
3. <span data-ttu-id="7ad3e-133">Mobile Application</span><span class="sxs-lookup"><span data-stu-id="7ad3e-133">Mobile Application</span></span>
   * <span data-ttu-id="7ad3e-134">Ontvangt en meldingen weergeven</span><span class="sxs-lookup"><span data-stu-id="7ad3e-134">Receives and display notification</span></span>

### <a name="benefits"></a><span data-ttu-id="7ad3e-135">Voordelen:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-135">Benefits:</span></span>
1. <span data-ttu-id="7ad3e-136">Het ontkoppelen tussen de ontvanger (mobiele app/service via Notification Hub) en de afzender (back endsystemen), kunt aanvullende back endsystemen worden geïntegreerd met minimale wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-136">The decoupling between the receiver (mobile app/service via Notification Hub) and sender (backend systems) enables additional backend systems being integrated with minimal change.</span></span>
2. <span data-ttu-id="7ad3e-137">Hierdoor wordt het scenario met meerdere mobiele apps kunnen worden ontvangen van gebeurtenissen van een of meer back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-137">This also makes the scenario of multiple mobile apps being able to receive events from one or more backend systems.</span></span>  

## <a name="sample"></a><span data-ttu-id="7ad3e-138">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-138">Sample:</span></span>
### <a name="prerequisites"></a><span data-ttu-id="7ad3e-139">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ad3e-139">Prerequisites</span></span>
<span data-ttu-id="7ad3e-140">U moet de volgende zelfstudies om vertrouwd met de concepten, evenals het maken van algemene & configuratiestappen te voltooien:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-140">You should complete the following tutorials to familiarize with the concepts as well as common creation & configuration steps:</span></span>

1. <span data-ttu-id="7ad3e-141">[Service Bus Pub subitems programmering] -Hier wordt uitgelegd hoe de details van het werken met Service Bus onderwerpen/abonnementen, het maken van een naamruimte onderwerpen/abonnementen bevatten, hoe u berichten ontvangen van deze & verzenden.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-141">[Service Bus Pub/Sub programming] - This explains the details of working with Service Bus Topics/Subscriptions, how to create a namespace to contain topics/subscriptions, how to send & receive messages from them.</span></span>
2. <span data-ttu-id="7ad3e-142">[Notification Hubs - universele Windows-zelfstudie] -procedure voor het instellen van een Windows Store-app en Notification Hubs gebruiken om te registreren en vervolgens meldingen ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-142">[Notification Hubs - Windows Universal tutorial] - This explains how to set up a Windows Store app and use Notification Hubs to register and then receive notifications.</span></span>

### <a name="sample-code"></a><span data-ttu-id="7ad3e-143">Voorbeeldcode</span><span class="sxs-lookup"><span data-stu-id="7ad3e-143">Sample code</span></span>
<span data-ttu-id="7ad3e-144">De code voor het volledige voorbeeld is beschikbaar op [Notification Hub voorbeelden].</span><span class="sxs-lookup"><span data-stu-id="7ad3e-144">The full sample code is available at [Notification Hub Samples].</span></span> <span data-ttu-id="7ad3e-145">Deze is opgesplitst in drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-145">It is split into three components:</span></span>

1. <span data-ttu-id="7ad3e-146">**EnterprisePushBackendSystem**</span><span class="sxs-lookup"><span data-stu-id="7ad3e-146">**EnterprisePushBackendSystem**</span></span>
   
    <span data-ttu-id="7ad3e-147">a.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-147">a.</span></span> <span data-ttu-id="7ad3e-148">Dit project gebruikt de *WindowsAzure.ServiceBus* Nuget-pakket en is gebaseerd op [Service Bus Pub subitems programmering].</span><span class="sxs-lookup"><span data-stu-id="7ad3e-148">This project uses the *WindowsAzure.ServiceBus* Nuget package and is  based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="7ad3e-149">b.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-149">b.</span></span> <span data-ttu-id="7ad3e-150">Dit is een eenvoudige C#-consoletoepassing te simuleren van een LoB-systeem waarvan het bericht moet worden geleverd aan de mobiele app initieert.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-150">This is a simple C# console app to simulate an LoB system which initiates the message to be delivered to the mobile app.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    <span data-ttu-id="7ad3e-151">c.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-151">c.</span></span> <span data-ttu-id="7ad3e-152">`CreateTopic`wordt gebruikt voor het maken van de Service Bus-onderwerp waarin berichten worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-152">`CreateTopic` is used to create the Service Bus topic where we will send messages.</span></span>
   
        public static void CreateTopic(string connectionString)
        {
            // Create the topic if it does not exist already
   
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.TopicExists(sampleTopic))
            {
                namespaceManager.CreateTopic(sampleTopic);
            }
        }
   
    <span data-ttu-id="7ad3e-153">d.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-153">d.</span></span> <span data-ttu-id="7ad3e-154">`SendMessage`wordt gebruikt om de berichten verzenden naar deze Service Bus-onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-154">`SendMessage` is used to send the messages to this Service Bus Topic.</span></span> <span data-ttu-id="7ad3e-155">We zijn een reeks willekeurige berichten hier alleen het verzenden naar het onderwerp periodiek omwille van de steekproef.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-155">Here we are simply sending a set of random messages to the topic periodically for the purpose of the sample.</span></span> <span data-ttu-id="7ad3e-156">Normaal gesproken zal er een back endsysteem dat berichten verzenden zal wanneer een gebeurtenis plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-156">Normally there will be a backend system which will send messages when an event occurs.</span></span>
   
        public static void SendMessage(string connectionString)
        {
            TopicClient client =
                TopicClient.CreateFromConnectionString(connectionString, sampleTopic);
   
            // Sends random messages every 10 seconds to the topic
            string[] messages =
            {
                "Employee Id '{0}' has joined.",
                "Employee Id '{0}' has left.",
                "Employee Id '{0}' has switched to a different team."
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
2. <span data-ttu-id="7ad3e-157">**ReceiveAndSendNotification**</span><span class="sxs-lookup"><span data-stu-id="7ad3e-157">**ReceiveAndSendNotification**</span></span>
   
    <span data-ttu-id="7ad3e-158">a.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-158">a.</span></span> <span data-ttu-id="7ad3e-159">Dit project gebruikt de *WindowsAzure.ServiceBus* en *Microsoft.Web.WebJobs.Publish* Nuget-pakketten en is gebaseerd op [Service Bus Pub subitems programmering].</span><span class="sxs-lookup"><span data-stu-id="7ad3e-159">This project uses the *WindowsAzure.ServiceBus* and *Microsoft.Web.WebJobs.Publish* Nuget packages and is based on [Service Bus Pub/Sub programming].</span></span>
   
    <span data-ttu-id="7ad3e-160">b.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-160">b.</span></span> <span data-ttu-id="7ad3e-161">Dit is een andere C#-consoletoepassing die wordt uitgevoerd als een [Azure webtaak] omdat er continu uitvoeren om te luisteren naar berichten van de LoB-/ back-end-systemen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-161">This is another C# console app which we will run as an [Azure WebJob] since it has to run continuously to listen for messages from the LoB/backend systems.</span></span> <span data-ttu-id="7ad3e-162">Dit zal onderdeel zijn van uw mobiele back-end.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-162">This will be part of your Mobile backend.</span></span>
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create the subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    <span data-ttu-id="7ad3e-163">c.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-163">c.</span></span> <span data-ttu-id="7ad3e-164">`CreateSubscription`wordt gebruikt voor het maken van een Service Bus-abonnement voor het onderwerp waarin de back endsysteem verzenden.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-164">`CreateSubscription` is used to create a Service Bus subscription for the topic where the backend system will send messages.</span></span> <span data-ttu-id="7ad3e-165">Dit onderdeel maakt, afhankelijk van het bedrijfsscenario een of meer abonnementen op de bijbehorende onderwerpen (bv. Sommige kan worden ontvangen van berichten van HR-systeem, sommige vanuit Financiën system, enzovoort)</span><span class="sxs-lookup"><span data-stu-id="7ad3e-165">Depending on the business scenario, this component will create one or more subscriptions to corresponding topics (e.g. some may be receiving messages from HR system, some from Finance system, and so on)</span></span>
   
        static void CreateSubscription(string connectionString)
        {
            // Create the subscription if it does not exist already
            var namespaceManager =
                NamespaceManager.CreateFromConnectionString(connectionString);
   
            if (!namespaceManager.SubscriptionExists(sampleTopic, sampleSubscription))
            {
                namespaceManager.CreateSubscription(sampleTopic, sampleSubscription);
            }
        }
   
    <span data-ttu-id="7ad3e-166">d.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-166">d.</span></span> <span data-ttu-id="7ad3e-167">ReceiveMessageAndSendNotification wordt gebruikt voor het lezen van het bericht van het onderwerp met behulp van het abonnement en als het lezen slaagt vervolgens een melding (in het voorbeeldscenario voor een Windows-systeemeigen pop-upmelding) stellen om te worden verzonden naar de mobiele toepassingen met Azure Notification Hubs.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-167">ReceiveMessageAndSendNotification is used to read the message from the topic using its subscription and if the read is successful then craft a notification (in the sample scenario a Windows native toast notification) to be sent to the mobile application using Azure Notification Hubs.</span></span>
   
        static void ReceiveMessageAndSendNotification(string connectionString)
        {
            // Initialize the Notification Hub
            string hubConnectionString = CloudConfigurationManager.GetSetting
                    ("Microsoft.NotificationHub.ConnectionString");
            hub = NotificationHubClient.CreateClientFromConnectionString
                    (hubConnectionString, "enterprisepushservicehub");
   
            SubscriptionClient Client =
                SubscriptionClient.CreateFromConnectionString
                        (connectionString, sampleTopic, sampleSubscription);
   
            Client.Receive();
   
            // Continuously process messages received from the subscription
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
   
    <span data-ttu-id="7ad3e-168">e.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-168">e.</span></span> <span data-ttu-id="7ad3e-169">Voor het publiceren van dit als een **webtaak**, klik met de rechtermuisknop op de oplossing in Visual Studio en selecteer **publiceren als webtaak**</span><span class="sxs-lookup"><span data-stu-id="7ad3e-169">For publishing this as a **WebJob**, right click on the solution in Visual Studio and select **Publish as WebJob**</span></span>
   
    ![][2]
   
    <span data-ttu-id="7ad3e-170">f.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-170">f.</span></span> <span data-ttu-id="7ad3e-171">Selecteer uw publicatieprofiel en als deze niet al host die deze webtaak en zodra u de WebSite klikt u vervolgens een nieuwe Azure-WebSite maken **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-171">Select your publishing profile and create a new Azure WebSite if it doesnt exist already which will host this WebJob and once you have the WebSite then **Publish**.</span></span>
   
    ![][3]
   
    <span data-ttu-id="7ad3e-172">g.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-172">g.</span></span> <span data-ttu-id="7ad3e-173">Configureren van de taak voor het 'Continu uitvoeren' zo dat wanneer u zich aanmelden bij de [klassieke Azure-Portal] ziet er ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-173">Configure the job to be "Run Continuously" so that when you log in to the [Azure Classic Portal] you should see something like the following:</span></span>
   
    ![][4]
3. <span data-ttu-id="7ad3e-174">**EnterprisePushMobileApp**</span><span class="sxs-lookup"><span data-stu-id="7ad3e-174">**EnterprisePushMobileApp**</span></span>
   
    <span data-ttu-id="7ad3e-175">a.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-175">a.</span></span> <span data-ttu-id="7ad3e-176">Dit is een Windows Store-toepassing die wordt ontvangen pop-upmeldingen uit de webtaak uitgevoerd als onderdeel van uw mobiele back-end en weer te geven.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-176">This is a Windows Store application which will receive toast notifications from the WebJob running as part of your Mobile backend and display it.</span></span> <span data-ttu-id="7ad3e-177">Dit is gebaseerd op [Notification Hubs - universele Windows-zelfstudie].</span><span class="sxs-lookup"><span data-stu-id="7ad3e-177">This is based on [Notification Hubs - Windows Universal tutorial].</span></span>  
   
    <span data-ttu-id="7ad3e-178">b.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-178">b.</span></span> <span data-ttu-id="7ad3e-179">Zorg ervoor dat uw toepassing is ingeschakeld voor het pop-upmeldingen te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-179">Ensure that your application is enabled to receive toast notifications.</span></span>
   
    <span data-ttu-id="7ad3e-180">c.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-180">c.</span></span> <span data-ttu-id="7ad3e-181">Zorg ervoor dat de volgende Notification Hubs registratiecode wordt aangeroepen op de App gestart (na het vervangen van de *HubName* en *DefaultListenSharedAccessSignature*:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-181">Ensure that the following Notification Hubs registration code is being called at the App start up (after replacing the *HubName* and *DefaultListenSharedAccessSignature*:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("[HubName]", "[DefaultListenSharedAccessSignature]");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

### <a name="running-sample"></a><span data-ttu-id="7ad3e-182">Voorbeeld uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-182">Running sample:</span></span>
1. <span data-ttu-id="7ad3e-183">Zorg ervoor dat uw webtaak correct wordt uitgevoerd en wordt 'Continu uitvoeren'.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-183">Ensure that your WebJob is running successfully and scheduled to "Run Continuously".</span></span>
2. <span data-ttu-id="7ad3e-184">Voer de **EnterprisePushMobileApp** die de Windows Store-app wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-184">Run the **EnterprisePushMobileApp** which will start the Windows Store app.</span></span>
3. <span data-ttu-id="7ad3e-185">Voer de **EnterprisePushBackendSystem** consoletoepassing die de LoB-back-end simuleert en wordt gestart met het verzenden van berichten en ziet u pop-upmeldingen verschijnen als volgt:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-185">Run the **EnterprisePushBackendSystem** console application which will simulate the LoB backend and will start sending messages and you should see toast notifications appearing like the following:</span></span>
   
    ![][5]
4. <span data-ttu-id="7ad3e-186">De berichten werden oorspronkelijk is verzonden naar Service Bus-onderwerpen die werd bewaakt door Service Bus-abonnementen in uw Web-taak.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-186">The messages were originally sent to Service Bus topics which was being monitored by Service Bus subscriptions in your Web Job.</span></span> <span data-ttu-id="7ad3e-187">Wanneer een bericht is ontvangen, is een melding gemaakt en verzonden naar de mobiele app.</span><span class="sxs-lookup"><span data-stu-id="7ad3e-187">Once a message was received, a notification was created and sent to the mobile app.</span></span> <span data-ttu-id="7ad3e-188">U kunt zoeken via de webtaak Logboeken om te bevestigen dat de verwerking wanneer u gaat de koppeling om de logboeken in [klassieke Azure-Portal] voor uw Web-taak:</span><span class="sxs-lookup"><span data-stu-id="7ad3e-188">You can look through the WebJob logs to confirm the processing when you go to the Logs link in [Azure Classic Portal] for your Web Job:</span></span>
   
    ![][6]

<!-- Images -->
[1]: ./media/notification-hubs-enterprise-push-architecture/architecture.png
[2]: ./media/notification-hubs-enterprise-push-architecture/WebJobsContextMenu.png
[3]: ./media/notification-hubs-enterprise-push-architecture/PublishAsWebJob.png
[4]: ./media/notification-hubs-enterprise-push-architecture/WebJob.png
[5]: ./media/notification-hubs-enterprise-push-architecture/Notifications.png
[6]: ./media/notification-hubs-enterprise-push-architecture/WebJobsLog.png

<!-- Links -->
<span data-ttu-id="7ad3e-189">[Notification Hub voorbeelden]: https://github.com/Azure/azure-notificationhubs-samples</span><span class="sxs-lookup"><span data-stu-id="7ad3e-189">[Notification Hub Samples]: https://github.com/Azure/azure-notificationhubs-samples</span></span>
<span data-ttu-id="7ad3e-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span><span class="sxs-lookup"><span data-stu-id="7ad3e-190">[Azure Mobile Service]: http://azure.microsoft.com/documentation/services/mobile-services/</span></span>
<span data-ttu-id="7ad3e-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span><span class="sxs-lookup"><span data-stu-id="7ad3e-191">[Azure Service Bus]: http://azure.microsoft.com/documentation/articles/fundamentals-service-bus-hybrid-solutions/</span></span>
<span data-ttu-id="7ad3e-192">[Service Bus Pub subitems programmering]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span><span class="sxs-lookup"><span data-stu-id="7ad3e-192">[Service Bus Pub/Sub programming]: http://azure.microsoft.com/documentation/articles/service-bus-dotnet-how-to-use-topics-subscriptions/</span></span>
<span data-ttu-id="7ad3e-193">[Azure webtaak]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span><span class="sxs-lookup"><span data-stu-id="7ad3e-193">[Azure WebJob]: http://azure.microsoft.com/documentation/articles/web-sites-create-web-jobs/</span></span>
<span data-ttu-id="7ad3e-194">[Notification Hubs - universele Windows-zelfstudie]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span><span class="sxs-lookup"><span data-stu-id="7ad3e-194">[Notification Hubs - Windows Universal tutorial]: http://azure.microsoft.com/documentation/articles/notification-hubs-windows-store-dotnet-get-started/</span></span>
<span data-ttu-id="7ad3e-195">[klassieke Azure-Portal]: https://manage.windowsazure.com/</span><span class="sxs-lookup"><span data-stu-id="7ad3e-195">[Azure Classic Portal]: https://manage.windowsazure.com/</span></span>

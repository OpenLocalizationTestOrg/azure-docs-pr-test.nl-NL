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
# <a name="enterprise-push-architectural-guidance"></a>Hulp voor architectuur via pushmeldingen van het bedrijf
Ondernemingen zijn tegenwoordig geleidelijk verplaatsen naar het maken van mobiele toepassingen voor hun eindgebruikers (extern) of voor Hallo werknemers (intern). Ze hebben bestaande back-endsystemen worden deze mainframes of sommige LoB-toepassingen die moeten worden geïntegreerd in de architectuur van de mobiele toepassing hello. Deze handleiding wordt hebben over de beste manier toodo deze integratie mogelijke oplossing aanbevelen toocommon scenario's.

Een frequente vereiste is voor het verzenden van push notification toohello gebruikers via hun mobiele toepassing bij een gebeurtenis van belang zijn in Hallo back-end-systemen. Bijvoorbeeld een klant bank die van de bank Hallo-app voor bankieren op haar iPhone wil toobe gewaarschuwd wanneer er een incasso boven een bepaald bedrag van haar account of een intranet-scenario waarin een medewerker van de afdeling Financiën die een budget goedkeuring app op zijn Windows Phone toobe wil wordt gedaan een melding wanneer hij een goedkeuringsaanvraag opgehaald.

bank- of goedkeuring verwerking Hallo is waarschijnlijk toobe doet u in sommige back endsysteem dat een gebruiker van de toohello push moet starten. Mogelijk zijn er meerdere dergelijke back-end voor systemen die u moeten alle bouwen Hallo dezelfde soort logica tooimplement push wanneer een gebeurtenis wordt een melding geactiveerd. Hallo complexiteit hier ligt in verschillende back endsystemen samen met een één push-systeem waar Hallo eindgebruikers mogelijk toodifferent meldingen bent geabonneerd en er kan zelfs meerdere mobiele toepassingen bijvoorbeeld in geval van Hallo van mobiele apps intranet worden integratie een mobiele toepassing wil waar tooreceive meldingen van meerdere dergelijke back endsystemen. Hallo back-endsystemen niet kent of tooknow van push-semantiek/technologie moet dus een gangbare oplossing hier is normaal een onderdeel dat opgevraagd Hallo back-end-systemen voor gebeurtenissen die van belang en is verantwoordelijk gesproken voor het verzenden van pushberichten hello toointroduce toohello-client.
Er wordt hier hebben over een nog beter oplossing met behulp van Azure Service Bus - onderwerp/abonnement model waarmee Hallo complexiteit tijdens het maken van Hallo oplossing schaalbaar wordt beperkt.

Hier volgt Hallo algemene architectuur van Hallo-oplossing (gegeneraliseerde met meerdere mobiele apps maar evenveel van toepassing wanneer er slechts één van de mobiele app)

## <a name="architecture"></a>Architectuur
![][1]

Hallo belangrijk onderdeel in dit diagram architectuur is Azure Service Bus waarmee een onderwerpen/de abonnementen programmeermodel (meer informatie over op het [Service Bus Pub subitems programmering]). Hallo-ontvanger die in dit geval Hallo mobiele back-end (meestal [Azure Mobile Service], gang een mobiele apps voor push-toohello) niet ontvangen berichten rechtstreeks vanuit de back-endsystemen hello, maar in plaats daarvan hebben we een tussenliggende abstractielaag geleverd door [Azure Service Bus] waardoor mobiele back-end tooreceive berichten van een of meer back endsystemen. Een Service Bus-onderwerp moet toobe gemaakt voor elk Hallo back-endsystemen bijvoorbeeld Account HR, financiële die eigenlijk 'onderwerpen' van belang dat berichten toobe als push-bericht verzonden wordt geïnitieerd. Hallo back-endsystemen zal berichten verzenden toothese onderwerpen. Een back-end van Mobile kunnen zich abonneren tooone of meer van deze onderwerpen door het maken van een Service Bus-abonnement. Dit recht Hallo mobiele back-end tooreceive een melding van de bijbehorende back-end-systeem Hallo geven. Back-end voor mobiele blijft toolisten voor berichten die op hun abonnementen en zodra er een bericht binnenkomt, schakelt terug en verzendt het als melding tooits notification hub. Notification hubs biedt vervolgens uiteindelijk Hallo-bericht toohello mobiele app. Dus toosummarize Hallo hoofdonderdelen, hebben we:

1. Back-end-systemen (LoB/oudere systemen)
   * Service Bus-onderwerp maakt
   * Bericht
2. Mobiele back-end
   * Service-abonnement wordt gemaakt
   * Ontvangen van bericht (van de back-end-systeem)
   * Verzendt melding tooclients (via Azure Notification Hub)
3. Mobile Application
   * Ontvangt en meldingen weergeven

### <a name="benefits"></a>Voordelen:
1. Hallo ontkoppeling Hallo ontvanger (mobiele app/service via Notification Hub) en de afzender (back endsystemen), kunt aanvullende back endsystemen worden geïntegreerd met minimale wijzigen.
2. Hierdoor wordt ook Hallo scenario met meerdere mobiele apps kunnen tooreceive gebeurtenissen van een of meer back endsystemen worden.  

## <a name="sample"></a>Voorbeeld:
### <a name="prerequisites"></a>Vereisten
U moet voltooien Hallo zelfstudies toofamiliarize met Hallo concepten, evenals algemene stappen voor het maken van & configuratie te volgen:

1. [Service Bus Pub subitems programmering] -Hier wordt uitgelegd hoe Hallo details van het werken met abonnementen/Service Bus onderwerpen, hoe toocreate een naamruimte toocontain onderwerpen/abonnementen, hoe toosend & berichten ontvangen van deze.
2. [Notification Hubs - universele Windows-zelfstudie] -dit wordt uitgelegd hoe tooset-up maken van een Windows Store-app Notification Hubs tooregister en gebruik vervolgens meldingen ontvangen.

### <a name="sample-code"></a>Voorbeeldcode
Hallo-code voor het volledige voorbeeld is beschikbaar op [Notification Hub voorbeelden]. Deze is opgesplitst in drie onderdelen:

1. **EnterprisePushBackendSystem**
   
    a. Dit project gebruikt Hallo *WindowsAzure.ServiceBus* Nuget-pakket en is gebaseerd op [Service Bus Pub subitems programmering].
   
    b. Dit is een eenvoudige C#-console-app toosimulate een LoB-systeem waarmee wordt geïnitieerd Hallo-bericht toobe bezorgd toohello mobiele app.
   
        static void Main(string[] args)
        {
            string connectionString =
                CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello topic where we will send notifications
            CreateTopic(connectionString);
   
            // Send message
            SendMessage(connectionString);
        }
   
    c. `CreateTopic`gebruikte toocreate Hallo Service Bus-onderwerp is waarin berichten worden verzonden.
   
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
   
    d. `SendMessage`gebruikte toosend Hallo berichten toothis Service Bus-onderwerp is. We zijn een set van willekeurige berichten toohello onderwerp periodiek voor Hallo doel van Hallo voorbeeld hier gewoon verzonden. Normaal gesproken zal er een back endsysteem dat berichten verzenden zal wanneer een gebeurtenis plaatsvindt.
   
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
2. **ReceiveAndSendNotification**
   
    a. Dit project gebruikt Hallo *WindowsAzure.ServiceBus* en *Microsoft.Web.WebJobs.Publish* Nuget-pakketten en is gebaseerd op [Service Bus Pub subitems programmering].
   
    b. Dit is een andere C#-consoletoepassing die wordt uitgevoerd als een [Azure webtaak] omdat het toorun continu heeft toolisten voor berichten van Hallo LoB/back-end-systemen. Dit zal onderdeel zijn van uw mobiele back-end.
   
        static void Main(string[] args)
        {
            string connectionString =
                     CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");
   
            // Create hello subscription which will receive messages
            CreateSubscription(connectionString);
   
            // Receive message
            ReceiveMessageAndSendNotification(connectionString);
        }
   
    c. `CreateSubscription`is gebruikte toocreate een Service Bus-abonnement voor Hallo onderwerp Hallo back-end-systeem zal waar berichten verzenden. Afhankelijk van het bedrijfsscenario hello maakt dit onderdeel u een of meer abonnementen toocorresponding onderwerpen (bv. Sommige kan worden ontvangen van berichten van HR-systeem, sommige vanuit Financiën system, enzovoort)
   
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
   
    d. ReceiveMessageAndSendNotification gebruikte tooread Hallo-bericht van Hallo onderwerp met behulp van het abonnement is en als Hallo lezen slaagt vervolgens stellen van een mobiele melding (in de voorbeeldscenario een systeemeigen pop-upmelding voor Windows hello) toobe verzonden toohello een toepassing met Azure Notification Hubs.
   
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
   
    e. Voor het publiceren van dit als een **webtaak**, klik met de rechtermuisknop op het Hallo-oplossing in Visual Studio en selecteer **publiceren als webtaak**
   
    ![][2]
   
    f. Uw publicatieprofiel selecteren en maken van een nieuwe Azure-WebSite als deze niet al host die deze webtaak en zodra er Hallo WebSite vervolgens **publiceren**.
   
    ![][3]
   
    g. Taak toobe 'Continu uitvoeren' hello zodanig configureren dat wanneer u zich toohello aanmeldt [klassieke Azure-Portal] u ziet er ongeveer zo Hallo volgende:
   
    ![][4]
3. **EnterprisePushMobileApp**
   
    a. Dit is een Windows Store-toepassing die wordt ontvangen pop-upmeldingen uit Hallo webtaak wordt uitgevoerd als onderdeel van uw mobiele back-end en weer te geven. Dit is gebaseerd op [Notification Hubs - universele Windows-zelfstudie].  
   
    b. Zorg ervoor dat uw toepassing ingeschakelde tooreceive pop-upmeldingen.
   
    c. Zorg ervoor dat Hallo registratiecode Notification Hubs te volgen op Hallo starten van de App wordt aangeroepen (na het vervangen van Hallo *HubName* en *DefaultListenSharedAccessSignature*:
   
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

### <a name="running-sample"></a>Voorbeeld uitgevoerd:
1. Zorg dat uw webtaak correct wordt uitgevoerd en gepland te 'uitvoeren continu'.
2. Voer Hallo **EnterprisePushMobileApp** die Hallo Windows Store-app wordt gestart.
3. Voer Hallo **EnterprisePushBackendSystem** consoletoepassing die simuleert Hallo LoB back-end en wordt gestart met het verzenden van berichten en ziet u pop-upmeldingen Hallo volgende weergegeven:
   
    ![][5]
4. Hallo-berichten zijn tooService Bus-onderwerpen die werd bewaakt door Service Bus-abonnementen in uw Web-taak oorspronkelijk is verzonden. Wanneer een bericht is ontvangen, wordt een melding is gemaakt, en toohello mobiele app verzonden. U kunt zoeken via Hallo webtaak tooconfirm Hallo verwerken Logboeken wanneer u toohello logboeken koppelen gaat in [klassieke Azure-Portal] voor uw Web-taak:
   
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

---
title: aaaGet de slag met Azure Service Bus-onderwerpen en abonnementen | Microsoft Docs
description: Een C#-consoletoepassing schrijven die Service Bus Messaging-onderwerpen en -abonnementen gebruikt.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Aan de slag met Service Bus-onderwerpen

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>Wat wordt bereikt

Deze zelfstudie behandelt Hallo stappen te volgen:

1. Maken van een Service Bus-naamruimte met behulp van hello Azure-portal.
2. Maken van een Service Bus-onderwerp met hello Azure-portal.
3. Maken van een Service Bus abonnement toothat onderwerp, met behulp van hello Azure-portal.
4. Schrijven van een toepassing console toosend een bericht toohello onderwerp.
5. Een toepassing console tooreceive bericht uit Hallo abonnement schrijven.

## <a name="prerequisites"></a>Vereisten

1. [Visual Studio 2015 of hoger](http://www.visualstudio.com). Hallo-voorbeelden in deze zelfstudie gebruikt Visual Studio 2017.
2. Een Azure-abonnement.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Maken van een naamruimte met behulp van hello Azure-portal

Als u al een Service Bus-berichtenservice naamruimte hebt gemaakt, gaan toohello [maken van een onderwerp hello Azure-portal met](#2-create-a-topic-using-the-azure-portal) sectie.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Maken van een onderwerp met hello Azure-portal

1. Meld u aan toohello [Azure-portal][azure-portal].
2. Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **Service Bus** (als er geen **Service Bus**, klikt u op **meer services**).
3. Klik op Hallo naamruimte waarin u toocreate Hallo onderwerp wilt. overzichtsblade Hallo-naamruimte wordt weergegeven:
   
    ![Een onderwerp maken][createtopic1]
4. In Hallo **Service Bus-naamruimte** blade, klikt u op **onderwerpen**, klikt u vervolgens op **toevoegen onderwerp**.
   
    ![Onderwerpen selecteren][createtopic2]
5. Voer een naam voor onderwerp Hallo en schakelt u Hallo **inschakelen partitioneren** optie. Laat Hallo andere opties met hun standaardwaarden.
   
    ![Selecteer Nieuw][createtopic3]
6. Hallo onderaan de blade hello, klikt u op **maken**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Maken van een abonnement toohello onderwerp

1. Hallo portal resources deelvenster Hallo-naamruimte die u in stap 1 hebt gemaakt, klik op de naam van Hallo onderwerp die u in stap 2 hebt gemaakt.
2. Een top Hallo Hallo overzicht deelvenster, klikt u op Hallo plus naast te ondertekenen**abonnement** tooadd een abonnement toothis onderwerp.

    ![Abonnement maken][createtopic4]

3. Voer een naam voor het Hallo-abonnement. Laat Hallo andere opties met hun standaardwaarden.

## <a name="4-send-messages-toohello-topic"></a>4. Verzenden van berichten toohello onderwerp

toosend berichten toohello onderwerp schrijven we een C#-consoletoepassing met Visual Studio.

### <a name="create-a-console-application"></a>Een consoletoepassing maken

Start Visual Studio en maak een nieuwe **consoletoepassing (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Hallo Service Bus NuGet-pakket toevoegen

1. Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.
2. Klik op Hallo **Bladeren** tabblad, zoeken naar **Microsoft Azure Service Bus**, en selecteer vervolgens Hallo **WindowsAzure.ServiceBus** item. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.
   
    ![Een NuGet-pakket selecteren][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Sommige toosend code schrijven een bericht toohello onderwerp

1. Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Hallo na code toohello toevoegen `Main` methode. Set Hallo `connectionString` variabele toohello verbinding tekenreeks die u hebt verkregen tijdens het Hallo-naamruimte maken en stel `topicName` toohello-naam die u hebt gebruikt bij het maken van Hallo onderwerp.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Zo zou het bestand Program.cs er moeten uitzien.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Hallo-programma uitvoeren en controleren van hello Azure-portal: klik op Hallo-naam van uw onderwerp in de naamruimte Hallo **overzicht** blade. Hallo onderwerp **Essentials** blade wordt weergegeven. In het Hallo-abonnementen die worden vermeld in de buurt Hallo onder aan de blade Hallo, ziet u dat Hallo **aantal berichten** waarde voor elk abonnement nu 1 worden. Wanneer u de afzender-toepassing hello worden uitgevoerd zonder het Hallo-berichten worden opgehaald (zoals beschreven in de volgende sectie Hallo), wordt deze waarde met 1 verhoogd. Let ook op de huidige grootte van die Hallo Hallo onderwerp stappen Hallo **huidige** waarde op Hallo **Essentials** blade telkens Hallo-app wordt een bericht toohello onderwerp/abonnement toegevoegd.
   
      ![Berichtgrootte][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Berichten ontvangen uit het Hallo-abonnement

1. tooreceive Hallo-bericht of berichten die u zojuist hebt verzonden, een nieuwe consoletoepassing maken en toevoegen van een verwijzing toohello Service Bus NuGet-pakket, vergelijkbare toohello vorige afzender-toepassing.
2. Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Hallo na code toohello toevoegen `Main` methode. Set Hallo `connectionString` variabele toohello connection string u bij het maken van de naamruimte Hallo verkregen en stel `topicName` toohello-naam die u hebt gebruikt bij het maken van Hallo onderwerp.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Zo zou het bestand Program.cs er moeten uitzien:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Hallo-programma uitvoeren, en Hallo portal opnieuw controleren. U ziet dat Hallo **aantal berichten** en **huidige** waarden zijn nu 0.
   
    ![Lengte van het onderwerp][topic-message-receive]

Gefeliciteerd. U hebt nu een onderwerp en een abonnement gemaakt, een bericht verzonden en dat bericht ontvangen.

## <a name="next-steps"></a>Volgende stappen

Bekijk onze [GitHub-opslagplaats met voorbeelden](https://github.com/Azure/azure-service-bus/tree/master/samples) die illustratie van Hallo meer geavanceerde functies van Service Bus-berichtenservice.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com

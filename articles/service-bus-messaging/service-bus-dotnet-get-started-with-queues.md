---
title: aaaGet de slag met Azure Service Bus-wachtrijen | Microsoft Docs
description: Een C#-consoletoepassing schrijven voor Service Bus Messaging-wachtrijen.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Aan de slag met Service Bus-wachtrijen
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>Wat wordt bereikt
Deze zelfstudie behandelt Hallo stappen te volgen:

1. Maken van een Service Bus-naamruimte met behulp van hello Azure-portal.
2. Maken van een Service Bus-wachtrij met hello Azure-portal.
3. Een toepassing console toosend een bericht geschreven.
4. Een console toepassing tooreceive Hallo verzonden berichten in de vorige stap Hallo schrijven.

## <a name="prerequisites"></a>Vereisten
1. [Visual Studio 2015 of hoger](http://www.visualstudio.com). Hallo-voorbeelden in deze zelfstudie gebruikt Visual Studio 2017.
2. Een Azure-abonnement.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Maken van een naamruimte met behulp van hello Azure-portal
Als u al een Service Bus-berichtenservice naamruimte hebt gemaakt, gaan toohello [maken van een wachtrij met hello Azure-portal](#2-create-a-queue-using-the-azure-portal) sectie.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Maken van een wachtrij met hello Azure-portal
Als u een Service Bus-wachtrij al hebt gemaakt, gaan toohello [verzendwachtrij berichten toohello](#3-send-messages-to-the-queue) sectie.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Berichten toohello wachtrij verzenden
toosend berichten toohello wachtrij schrijven we een C#-consoletoepassing met Visual Studio.

### <a name="create-a-console-application"></a>Een consoletoepassing maken

Start Visual Studio en maak een nieuwe **consoletoepassing (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Hallo Service Bus NuGet-pakket toevoegen
1. Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.
2. Klik op Hallo **Bladeren** tabblad, zoeken naar **Microsoft Azure Service Bus**, en selecteer vervolgens Hallo **WindowsAzure.ServiceBus** item. Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.
   
    ![Een NuGet-pakket selecteren][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Sommige toosend code een toohello berichtenwachtrij schrijven
1. Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Hallo na code toohello toevoegen `Main` methode. Set Hallo `connectionString` variabele toohello verbinding tekenreeks die u hebt verkregen tijdens het Hallo-naamruimte maken en stel `queueName` toohello wachtrijnaam die u hebt gebruikt bij het maken van Hallo wachtrij.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

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

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Hallo-programma uitvoeren en controleren van hello Azure-portal: klik op Hallo-naam van uw wachtrij in de naamruimte Hallo **overzicht** blade. Hallo wachtrij **Essentials** blade wordt weergegeven. U ziet dat Hallo **bericht-aantal actieve** waarde moet 1 nu. Telkens wanneer die u de afzender-toepassing hello uitvoert zonder het Hallo-berichten bij het ophalen van deze waarde met 1 wordt verhoogd. Opmerking dat Hallo huidige grootte van de wachtrij Hallo stappen, elke keer Hallo-app wordt ook een berichtenwachtrij toohello toegevoegd.
   
      ![Berichtgrootte][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Berichten ontvangen uit de wachtrij Hallo

1. tooreceive hello berichten die u zojuist hebt verzonden, een nieuwe consoletoepassing maken en toevoegen van een verwijzing toohello Service Bus NuGet-pakket, vergelijkbare toohello vorige afzender-toepassing.
2. Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Hallo na code toohello toevoegen `Main` methode. Set Hallo `connectionString` variabele toohello verbindingsreeks die is verkregen tijdens het Hallo-naamruimte maken en stellen `queueName` toohello wachtrijnaam die u hebt gebruikt bij het maken van Hallo wachtrij.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
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
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
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
4. Hallo-programma uitvoeren, en Hallo portal opnieuw controleren. U ziet dat Hallo **bericht-aantal actieve** en **huidige** waarden zijn nu 0.
   
    ![Wachtrijlengte][queue-message-receive]

Gefeliciteerd. U hebt nu een wachtrij gemaakt, een bericht verzonden en een bericht ontvangen.

## <a name="next-steps"></a>Volgende stappen

Bekijk onze [GitHub-opslagplaats met voorbeelden](https://github.com/Azure/azure-service-bus/tree/master/samples) die illustratie van Hallo meer geavanceerde functies van Service Bus-berichtenservice.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples

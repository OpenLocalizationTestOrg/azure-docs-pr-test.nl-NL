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
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="dbb16-103">Aan de slag met Service Bus-wachtrijen</span><span class="sxs-lookup"><span data-stu-id="dbb16-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="dbb16-104">Wat wordt bereikt</span><span class="sxs-lookup"><span data-stu-id="dbb16-104">What will be accomplished</span></span>
<span data-ttu-id="dbb16-105">Deze zelfstudie behandelt Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="dbb16-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="dbb16-106">Maken van een Service Bus-naamruimte met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dbb16-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="dbb16-107">Maken van een Service Bus-wachtrij met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="dbb16-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="dbb16-108">Een toepassing console toosend een bericht geschreven.</span><span class="sxs-lookup"><span data-stu-id="dbb16-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="dbb16-109">Een console toepassing tooreceive Hallo verzonden berichten in de vorige stap Hallo schrijven.</span><span class="sxs-lookup"><span data-stu-id="dbb16-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbb16-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="dbb16-110">Prerequisites</span></span>
1. <span data-ttu-id="dbb16-111">[Visual Studio 2015 of hoger](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="dbb16-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="dbb16-112">Hallo-voorbeelden in deze zelfstudie gebruikt Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dbb16-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="dbb16-113">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="dbb16-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="dbb16-114">1. Maken van een naamruimte met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="dbb16-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="dbb16-115">Als u al een Service Bus-berichtenservice naamruimte hebt gemaakt, gaan toohello [maken van een wachtrij met hello Azure-portal](#2-create-a-queue-using-the-azure-portal) sectie.</span><span class="sxs-lookup"><span data-stu-id="dbb16-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="dbb16-116">2. Maken van een wachtrij met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="dbb16-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="dbb16-117">Als u een Service Bus-wachtrij al hebt gemaakt, gaan toohello [verzendwachtrij berichten toohello](#3-send-messages-to-the-queue) sectie.</span><span class="sxs-lookup"><span data-stu-id="dbb16-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="dbb16-118">3. Berichten toohello wachtrij verzenden</span><span class="sxs-lookup"><span data-stu-id="dbb16-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="dbb16-119">toosend berichten toohello wachtrij schrijven we een C#-consoletoepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dbb16-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="dbb16-120">Een consoletoepassing maken</span><span class="sxs-lookup"><span data-stu-id="dbb16-120">Create a console application</span></span>

<span data-ttu-id="dbb16-121">Start Visual Studio en maak een nieuwe **consoletoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="dbb16-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="dbb16-122">Hallo Service Bus NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="dbb16-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="dbb16-123">Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="dbb16-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="dbb16-124">Klik op Hallo **Bladeren** tabblad, zoeken naar **Microsoft Azure Service Bus**, en selecteer vervolgens Hallo **WindowsAzure.ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="dbb16-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="dbb16-125">Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="dbb16-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Een NuGet-pakket selecteren][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="dbb16-127">Sommige toosend code een toohello berichtenwachtrij schrijven</span><span class="sxs-lookup"><span data-stu-id="dbb16-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="dbb16-128">Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbb16-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="dbb16-129">Hallo na code toohello toevoegen `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="dbb16-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="dbb16-130">Set Hallo `connectionString` variabele toohello verbinding tekenreeks die u hebt verkregen tijdens het Hallo-naamruimte maken en stel `queueName` toohello wachtrijnaam die u hebt gebruikt bij het maken van Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="dbb16-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="dbb16-131">Zo zou het bestand Program.cs er moeten uitzien.</span><span class="sxs-lookup"><span data-stu-id="dbb16-131">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="dbb16-132">Hallo-programma uitvoeren en controleren van hello Azure-portal: klik op Hallo-naam van uw wachtrij in de naamruimte Hallo **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="dbb16-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="dbb16-133">Hallo wachtrij **Essentials** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="dbb16-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="dbb16-134">U ziet dat Hallo **bericht-aantal actieve** waarde moet 1 nu.</span><span class="sxs-lookup"><span data-stu-id="dbb16-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="dbb16-135">Telkens wanneer die u de afzender-toepassing hello uitvoert zonder het Hallo-berichten bij het ophalen van deze waarde met 1 wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="dbb16-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="dbb16-136">Opmerking dat Hallo huidige grootte van de wachtrij Hallo stappen, elke keer Hallo-app wordt ook een berichtenwachtrij toohello toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="dbb16-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![Berichtgrootte][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="dbb16-138">4. Berichten ontvangen uit de wachtrij Hallo</span><span class="sxs-lookup"><span data-stu-id="dbb16-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="dbb16-139">tooreceive hello berichten die u zojuist hebt verzonden, een nieuwe consoletoepassing maken en toevoegen van een verwijzing toohello Service Bus NuGet-pakket, vergelijkbare toohello vorige afzender-toepassing.</span><span class="sxs-lookup"><span data-stu-id="dbb16-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="dbb16-140">Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="dbb16-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="dbb16-141">Hallo na code toohello toevoegen `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="dbb16-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="dbb16-142">Set Hallo `connectionString` variabele toohello verbindingsreeks die is verkregen tijdens het Hallo-naamruimte maken en stellen `queueName` toohello wachtrijnaam die u hebt gebruikt bij het maken van Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="dbb16-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
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
   
    <span data-ttu-id="dbb16-143">Zo zou het bestand Program.cs er moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="dbb16-143">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="dbb16-144">Hallo-programma uitvoeren, en Hallo portal opnieuw controleren.</span><span class="sxs-lookup"><span data-stu-id="dbb16-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="dbb16-145">U ziet dat Hallo **bericht-aantal actieve** en **huidige** waarden zijn nu 0.</span><span class="sxs-lookup"><span data-stu-id="dbb16-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Wachtrijlengte][queue-message-receive]

<span data-ttu-id="dbb16-147">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="dbb16-147">Congratulations!</span></span> <span data-ttu-id="dbb16-148">U hebt nu een wachtrij gemaakt, een bericht verzonden en een bericht ontvangen.</span><span class="sxs-lookup"><span data-stu-id="dbb16-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dbb16-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dbb16-149">Next steps</span></span>

<span data-ttu-id="dbb16-150">Bekijk onze [GitHub-opslagplaats met voorbeelden](https://github.com/Azure/azure-service-bus/tree/master/samples) die illustratie van Hallo meer geavanceerde functies van Service Bus-berichtenservice.</span><span class="sxs-lookup"><span data-stu-id="dbb16-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples

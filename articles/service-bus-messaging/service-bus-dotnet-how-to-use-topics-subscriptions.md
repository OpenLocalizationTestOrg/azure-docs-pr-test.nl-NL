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
# <a name="get-started-with-service-bus-topics"></a><span data-ttu-id="e6ad8-103">Aan de slag met Service Bus-onderwerpen</span><span class="sxs-lookup"><span data-stu-id="e6ad8-103">Get started with Service Bus topics</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="e6ad8-104">Wat wordt bereikt</span><span class="sxs-lookup"><span data-stu-id="e6ad8-104">What will be accomplished</span></span>

<span data-ttu-id="e6ad8-105">Deze zelfstudie behandelt Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e6ad8-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="e6ad8-106">Maken van een Service Bus-naamruimte met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="e6ad8-107">Maken van een Service Bus-onderwerp met hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-107">Create a Service Bus topic, using hello Azure portal.</span></span>
3. <span data-ttu-id="e6ad8-108">Maken van een Service Bus abonnement toothat onderwerp, met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-108">Create a Service Bus subscription toothat topic, using hello Azure portal.</span></span>
4. <span data-ttu-id="e6ad8-109">Schrijven van een toepassing console toosend een bericht toohello onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-109">Write a console application toosend a message toohello topic.</span></span>
5. <span data-ttu-id="e6ad8-110">Een toepassing console tooreceive bericht uit Hallo abonnement schrijven.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-110">Write a console application tooreceive that message from hello subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6ad8-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e6ad8-111">Prerequisites</span></span>

1. <span data-ttu-id="e6ad8-112">[Visual Studio 2015 of hoger](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="e6ad8-112">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="e6ad8-113">Hallo-voorbeelden in deze zelfstudie gebruikt Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-113">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="e6ad8-114">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="e6ad8-115">1. Maken van een naamruimte met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e6ad8-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="e6ad8-116">Als u al een Service Bus-berichtenservice naamruimte hebt gemaakt, gaan toohello [maken van een onderwerp hello Azure-portal met](#2-create-a-topic-using-the-azure-portal) sectie.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-116">If you have already created a Service Bus Messaging namespace, jump toohello [Create a topic using hello Azure portal](#2-create-a-topic-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a><span data-ttu-id="e6ad8-117">2. Maken van een onderwerp met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="e6ad8-117">2. Create a topic using hello Azure portal</span></span>

1. <span data-ttu-id="e6ad8-118">Meld u aan toohello [Azure-portal][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="e6ad8-118">Log on toohello [Azure portal][azure-portal].</span></span>
2. <span data-ttu-id="e6ad8-119">Klik in het Hallo navigatiedeelvenster links van de portal Hallo op **Service Bus** (als er geen **Service Bus**, klikt u op **meer services**).</span><span class="sxs-lookup"><span data-stu-id="e6ad8-119">In hello left navigation pane of hello portal, click **Service Bus** (if you don't see **Service Bus**, click **More services**).</span></span>
3. <span data-ttu-id="e6ad8-120">Klik op Hallo naamruimte waarin u toocreate Hallo onderwerp wilt.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-120">Click hello namespace in which you would like toocreate hello topic.</span></span> <span data-ttu-id="e6ad8-121">overzichtsblade Hallo-naamruimte wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e6ad8-121">hello namespace overview blade appears:</span></span>
   
    ![Een onderwerp maken][createtopic1]
4. <span data-ttu-id="e6ad8-123">In Hallo **Service Bus-naamruimte** blade, klikt u op **onderwerpen**, klikt u vervolgens op **toevoegen onderwerp**.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-123">In hello **Service Bus namespace** blade, click **Topics**, then click **Add topic**.</span></span>
   
    ![Onderwerpen selecteren][createtopic2]
5. <span data-ttu-id="e6ad8-125">Voer een naam voor onderwerp Hallo en schakelt u Hallo **inschakelen partitioneren** optie.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-125">Enter a name for hello topic, and uncheck hello **Enable partitioning** option.</span></span> <span data-ttu-id="e6ad8-126">Laat Hallo andere opties met hun standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-126">Leave hello other options with their default values.</span></span>
   
    ![Selecteer Nieuw][createtopic3]
6. <span data-ttu-id="e6ad8-128">Hallo onderaan de blade hello, klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-128">At hello bottom of hello blade, click **Create**.</span></span>

## <a name="3-create-a-subscription-toohello-topic"></a><span data-ttu-id="e6ad8-129">3. Maken van een abonnement toohello onderwerp</span><span class="sxs-lookup"><span data-stu-id="e6ad8-129">3. Create a subscription toohello topic</span></span>

1. <span data-ttu-id="e6ad8-130">Hallo portal resources deelvenster Hallo-naamruimte die u in stap 1 hebt gemaakt, klik op de naam van Hallo onderwerp die u in stap 2 hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-130">In hello portal resources pane, click hello namespace you created in step 1, then click name of hello topic you created in step 2.</span></span>
2. <span data-ttu-id="e6ad8-131">Een top Hallo Hallo overzicht deelvenster, klikt u op Hallo plus naast te ondertekenen**abonnement** tooadd een abonnement toothis onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-131">A hello top of hello overview pane, click hello plus sign next too**Subscription** tooadd a subscription toothis topic.</span></span>

    ![Abonnement maken][createtopic4]

3. <span data-ttu-id="e6ad8-133">Voer een naam voor het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-133">Enter a name for hello subscription.</span></span> <span data-ttu-id="e6ad8-134">Laat Hallo andere opties met hun standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-134">Leave hello other options with their default values.</span></span>

## <a name="4-send-messages-toohello-topic"></a><span data-ttu-id="e6ad8-135">4. Verzenden van berichten toohello onderwerp</span><span class="sxs-lookup"><span data-stu-id="e6ad8-135">4. Send messages toohello topic</span></span>

<span data-ttu-id="e6ad8-136">toosend berichten toohello onderwerp schrijven we een C#-consoletoepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-136">toosend messages toohello topic, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="e6ad8-137">Een consoletoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e6ad8-137">Create a console application</span></span>

<span data-ttu-id="e6ad8-138">Start Visual Studio en maak een nieuwe **consoletoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-138">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="e6ad8-139">Hallo Service Bus NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="e6ad8-139">Add hello Service Bus NuGet package</span></span>

1. <span data-ttu-id="e6ad8-140">Met de rechtermuisknop op Hallo van een nieuw gemaakt project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-140">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="e6ad8-141">Klik op Hallo **Bladeren** tabblad, zoeken naar **Microsoft Azure Service Bus**, en selecteer vervolgens Hallo **WindowsAzure.ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-141">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="e6ad8-142">Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens dit dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-142">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Een NuGet-pakket selecteren][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a><span data-ttu-id="e6ad8-144">Sommige toosend code schrijven een bericht toohello onderwerp</span><span class="sxs-lookup"><span data-stu-id="e6ad8-144">Write some code toosend a message toohello topic</span></span>

1. <span data-ttu-id="e6ad8-145">Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-145">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="e6ad8-146">Hallo na code toohello toevoegen `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-146">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="e6ad8-147">Set Hallo `connectionString` variabele toohello verbinding tekenreeks die u hebt verkregen tijdens het Hallo-naamruimte maken en stel `topicName` toohello-naam die u hebt gebruikt bij het maken van Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-147">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="e6ad8-148">Zo zou het bestand Program.cs er moeten uitzien.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-148">Here is what your Program.cs file should look like.</span></span>
   
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
3. <span data-ttu-id="e6ad8-149">Hallo-programma uitvoeren en controleren van hello Azure-portal: klik op Hallo-naam van uw onderwerp in de naamruimte Hallo **overzicht** blade.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-149">Run hello program, and check hello Azure portal: click hello name of your topic in hello namespace **Overview** blade.</span></span> <span data-ttu-id="e6ad8-150">Hallo onderwerp **Essentials** blade wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-150">hello topic **Essentials** blade is displayed.</span></span> <span data-ttu-id="e6ad8-151">In het Hallo-abonnementen die worden vermeld in de buurt Hallo onder aan de blade Hallo, ziet u dat Hallo **aantal berichten** waarde voor elk abonnement nu 1 worden.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-151">In hello subscription(s) listed near hello bottom of hello blade, notice that hello **Message Count** value for each subscription should now be 1.</span></span> <span data-ttu-id="e6ad8-152">Wanneer u de afzender-toepassing hello worden uitgevoerd zonder het Hallo-berichten worden opgehaald (zoals beschreven in de volgende sectie Hallo), wordt deze waarde met 1 verhoogd.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-152">Each time you run hello sender application without retrieving hello messages (as described in hello next section), this value increases by 1.</span></span> <span data-ttu-id="e6ad8-153">Let ook op de huidige grootte van die Hallo Hallo onderwerp stappen Hallo **huidige** waarde op Hallo **Essentials** blade telkens Hallo-app wordt een bericht toohello onderwerp/abonnement toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-153">Also note that hello current size of hello topic increments hello **Current** value on hello **Essentials** blade each time hello app adds a message toohello topic/subscription.</span></span>
   
      ![Berichtgrootte][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a><span data-ttu-id="e6ad8-155">5. Berichten ontvangen uit het Hallo-abonnement</span><span class="sxs-lookup"><span data-stu-id="e6ad8-155">5. Receive messages from hello subscription</span></span>

1. <span data-ttu-id="e6ad8-156">tooreceive Hallo-bericht of berichten die u zojuist hebt verzonden, een nieuwe consoletoepassing maken en toevoegen van een verwijzing toohello Service Bus NuGet-pakket, vergelijkbare toohello vorige afzender-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-156">tooreceive hello message or messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="e6ad8-157">Voeg de volgende Hallo `using` instructie toohello boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-157">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="e6ad8-158">Hallo na code toohello toevoegen `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-158">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="e6ad8-159">Set Hallo `connectionString` variabele toohello connection string u bij het maken van de naamruimte Hallo verkregen en stel `topicName` toohello-naam die u hebt gebruikt bij het maken van Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-159">Set hello `connectionString` variable toohello connection string you obtained when creating hello namespace, and set `topicName` toohello name that you used when creating hello topic.</span></span>
   
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
   
    <span data-ttu-id="e6ad8-160">Zo zou het bestand Program.cs er moeten uitzien:</span><span class="sxs-lookup"><span data-stu-id="e6ad8-160">Here is what your Program.cs file should look like:</span></span>
   
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
4. <span data-ttu-id="e6ad8-161">Hallo-programma uitvoeren, en Hallo portal opnieuw controleren.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-161">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="e6ad8-162">U ziet dat Hallo **aantal berichten** en **huidige** waarden zijn nu 0.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-162">Notice that hello **Message Count** and **Current** values are now 0.</span></span>
   
    ![Lengte van het onderwerp][topic-message-receive]

<span data-ttu-id="e6ad8-164">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-164">Congratulations!</span></span> <span data-ttu-id="e6ad8-165">U hebt nu een onderwerp en een abonnement gemaakt, een bericht verzonden en dat bericht ontvangen.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-165">You have now created a topic and subscription, sent a message, and received that message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6ad8-166">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e6ad8-166">Next steps</span></span>

<span data-ttu-id="e6ad8-167">Bekijk onze [GitHub-opslagplaats met voorbeelden](https://github.com/Azure/azure-service-bus/tree/master/samples) die illustratie van Hallo meer geavanceerde functies van Service Bus-berichtenservice.</span><span class="sxs-lookup"><span data-stu-id="e6ad8-167">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

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

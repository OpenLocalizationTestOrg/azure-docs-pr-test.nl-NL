---
title: Gebeurtenissen verzenden naar Azure Event Hubs met behulp van .NET Framework | Microsoft Docs
description: Ga aan de slag met het verzenden van gebeurtenissen naar Event Hubs met .NET Framework
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: 4eb0e7bcc14722010121c2a5945509d6ed736f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="43e43-103">Gebeurtenissen verzenden naar Azure Event Hubs met behulp van .NET Framework</span><span class="sxs-lookup"><span data-stu-id="43e43-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="43e43-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="43e43-104">Introduction</span></span>

<span data-ttu-id="43e43-105">Event Hubs is een service die grote hoeveelheden gebeurtenisgegevens (telemetrie) van verbonden apparaten en toepassingen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="43e43-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="43e43-106">Nadat u gegevens in Event Hubs hebt verzameld, kunt u de gegevens opslaan met behulp van een opslagcluster of transformeren met een provider van realtime-analyses.</span><span class="sxs-lookup"><span data-stu-id="43e43-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="43e43-107">Deze functie voor grootschalige gebeurtenisverzameling en -verwerking is een belangrijk onderdeel van de architectuur van moderne toepassingen, met inbegrip van het Internet der dingen (IoT).</span><span class="sxs-lookup"><span data-stu-id="43e43-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="43e43-108">In deze zelfstudie kunt u zien hoe u [Azure Portal](https://portal.azure.com) gebruikt om een Event Hub te maken.</span><span class="sxs-lookup"><span data-stu-id="43e43-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="43e43-109">U leert ook hoe u gebeurtenissen met .NET Framework naar een Event Hub verzendt via een in C# geschreven consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="43e43-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="43e43-110">Zie het artikel [Gebeurtenissen ontvangen met .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) of klik op de juiste taal voor ontvangst in de tabel links om gebeurtenissen te ontvangen via .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="43e43-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="43e43-111">Voor het voltooien van deze zelfstudie moet aan de volgende vereisten worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="43e43-111">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="43e43-112">[Microsoft Visual Studio 2015 of hoger](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="43e43-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="43e43-113">In de schermafbeeldingen in deze zelfstudie wordt Visual Studio 2017 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="43e43-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="43e43-114">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="43e43-114">An active Azure account.</span></span> <span data-ttu-id="43e43-115">Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="43e43-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="43e43-116">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="43e43-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="43e43-117">Een Event Hubs-naamruimte en een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="43e43-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="43e43-118">In de eerste stap gebruikt u [Azure Portal](https://portal.azure.com) om een naamruimte van het type Event Hubs te maken en de beheerreferenties te verkrijgen die de toepassing nodig heeft om met de Event Hub te communiceren.</span><span class="sxs-lookup"><span data-stu-id="43e43-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="43e43-119">Volg de procedure in [dit artikel](event-hubs-create.md) om een naamruimte en Event Hub te maken en ga daarna verder met de volgende stappen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="43e43-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="43e43-120">Een consoletoepassing voor afzenders maken</span><span class="sxs-lookup"><span data-stu-id="43e43-120">Create a sender console application</span></span>

<span data-ttu-id="43e43-121">In deze sectie schrijft u een Windows-consoletoepassing die gebeurtenissen naar uw Event Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="43e43-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="43e43-122">Maak in Visual Studio een nieuw Visual C# bureaublad-app-project met behulp van de projectsjabloon**Consoletoepassing**.</span><span class="sxs-lookup"><span data-stu-id="43e43-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="43e43-123">Noem het project **Afzender**.</span><span class="sxs-lookup"><span data-stu-id="43e43-123">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="43e43-124">Klik in Solution Explorer met de rechtermuisknop op het project **Afzender** en klik op **NuGet-pakketten beheren voor oplossing**.</span><span class="sxs-lookup"><span data-stu-id="43e43-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="43e43-125">Klik op het tabblad **Bladeren** en zoek vervolgens naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="43e43-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="43e43-126">Klik op **Installeren** en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="43e43-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="43e43-127">Er wordt door Visual Studio een verwijzing naar het [ NuGet-pakket Azure Service Bus-bibliotheek](https://www.nuget.org/packages/WindowsAzure.ServiceBus) gedownload, geïnstalleerd en toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="43e43-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="43e43-128">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="43e43-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="43e43-129">Voeg de volgende velden toe aan de klasse **Program**, waarbij u de waarden van de tijdelijke aanduiding vervangt door de naam van de Event Hub die u in de vorige sectie hebt gemaakt, en de verbindingsreeks op naamruimteniveau die u eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="43e43-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="43e43-130">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="43e43-130">Add the following method to the **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="43e43-131">Met deze methode worden er continu gebeurtenissen naar uw Event Hub verzonden, met een vertraging van 200 ms.</span><span class="sxs-lookup"><span data-stu-id="43e43-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="43e43-132">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="43e43-132">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="43e43-133">Voer het programma uit en controleer of er geen fouten zijn.</span><span class="sxs-lookup"><span data-stu-id="43e43-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="43e43-134">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="43e43-134">Congratulations!</span></span> <span data-ttu-id="43e43-135">U hebt nu berichten verzonden naar een Event Hub.</span><span class="sxs-lookup"><span data-stu-id="43e43-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="43e43-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="43e43-136">Next steps</span></span>
<span data-ttu-id="43e43-137">Nu u een werkende toepassing hebt gebouwd die een Event Hub maakt en gegevens verzendt, kunt u naar de volgende scenario's gaan:</span><span class="sxs-lookup"><span data-stu-id="43e43-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="43e43-138">Gebeurtenissen ontvangen met de gebeurtenisprocessorhost</span><span class="sxs-lookup"><span data-stu-id="43e43-138">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="43e43-139">Documentatie over de gebeurtenisprocessorhost</span><span class="sxs-lookup"><span data-stu-id="43e43-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="43e43-140">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="43e43-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png


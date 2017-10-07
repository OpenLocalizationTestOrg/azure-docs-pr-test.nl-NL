---
title: .NET Framework aaaSend gebeurtenissen tooAzure Event Hubs met behulp van Hallo | Microsoft Docs
description: Aan de slag tooEvent Hubs Hallo .NET Framework met het verzenden van gebeurtenissen
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="1c9eb-103">Verzenden van gebeurtenissen tooAzure Event Hubs met behulp van Hallo .NET Framework</span><span class="sxs-lookup"><span data-stu-id="1c9eb-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="1c9eb-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="1c9eb-104">Introduction</span></span>

<span data-ttu-id="1c9eb-105">Event Hubs is een service die grote hoeveelheden gebeurtenisgegevens (telemetrie) van verbonden apparaten en toepassingen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="1c9eb-106">Nadat u gegevens in Event Hubs hebt verzameld, kunt u Hallo gegevensopslag met behulp van een opslagcluster of transformeren met een realtime analytics-provider.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="1c9eb-107">Deze gebeurtenis grootschalige verzamelen en verwerken mogelijkheid is een belangrijk onderdeel van moderne toepassingsarchitecturen inclusief Hallo Internet der dingen (IoT).</span><span class="sxs-lookup"><span data-stu-id="1c9eb-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="1c9eb-108">Deze zelfstudie laat zien hoe toouse hello [Azure-portal](https://portal.azure.com) toocreate een event hub.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="1c9eb-109">U ziet ook hoe toosend gebeurtenissen tooan event hub met een consoletoepassing die is geschreven in C# met behulp van .NET Framework Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="1c9eb-110">tooreceive gebeurtenissen met Hallo .NET Framework, Zie Hallo [ontvangen van gebeurtenissen met behulp van .NET Framework Hallo](event-hubs-dotnet-framework-getstarted-receive-eph.md) artikel, of klik op de juiste Hallo ontvangende taal in Hallo links inhoudsopgave.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="1c9eb-111">toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="1c9eb-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="1c9eb-112">[Microsoft Visual Studio 2015 of hoger](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1c9eb-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="1c9eb-113">Hallo schermopnamen in deze zelfstudie gebruiken Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="1c9eb-114">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-114">An active Azure account.</span></span> <span data-ttu-id="1c9eb-115">Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="1c9eb-116">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="1c9eb-117">Een Event Hubs-naamruimte en een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="1c9eb-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="1c9eb-118">de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte van Event Hubs typt en beheerreferenties Hallo uw toepassing moet toocommunicate met Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="1c9eb-119">toocreate een naamruimte en event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), gaat u verder met de Hallo stappen in deze zelfstudie te volgen.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="1c9eb-120">Een consoletoepassing voor afzenders maken</span><span class="sxs-lookup"><span data-stu-id="1c9eb-120">Create a sender console application</span></span>

<span data-ttu-id="1c9eb-121">In deze sectie schrijft u een Windows-consoletoepassing die gebeurtenissen tooyour event hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="1c9eb-122">Maak in Visual Studio een nieuw Visual C# bureaublad-App-project met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="1c9eb-123">Naam Hallo project **afzender**.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="1c9eb-124">Klik in Solution Explorer met de rechtermuisknop op Hallo **afzender** project en klik vervolgens op **NuGet-pakketten beheren voor oplossing**.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="1c9eb-125">Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="1c9eb-126">Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="1c9eb-127">Visual Studio downloadt, installeert en voegt u een verwijzing toohello [bibliotheek NuGet-pakket Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="1c9eb-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="1c9eb-128">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="1c9eb-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="1c9eb-129">Hallo na toohello velden toevoegen **programma** klasse, vervangen door waarden van de tijdelijke aanduiding Hallo Hallo-naam van Hallo event hub die u hebt gemaakt in de vorige sectie Hallo en Hallo naamruimteniveau verbindingsreeks u eerder hebt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="1c9eb-130">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="1c9eb-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="1c9eb-131">Deze methode verzendt continu gebeurtenissen tooyour event hub, met een vertraging van 200 ms.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="1c9eb-132">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="1c9eb-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="1c9eb-133">Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="1c9eb-134">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-134">Congratulations!</span></span> <span data-ttu-id="1c9eb-135">U hebt nu verzonden berichten tooan event hub.</span><span class="sxs-lookup"><span data-stu-id="1c9eb-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1c9eb-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1c9eb-136">Next steps</span></span>
<span data-ttu-id="1c9eb-137">Nu dat u een werkende toepassing die een event hub maakt en verzendt gegevens hebt gemaakt, kunt u op toohello volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="1c9eb-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="1c9eb-138">Hallo Event Processor Host met gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="1c9eb-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="1c9eb-139">Documentatie over de gebeurtenisprocessorhost</span><span class="sxs-lookup"><span data-stu-id="1c9eb-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="1c9eb-140">Event Hubs-overzicht</span><span class="sxs-lookup"><span data-stu-id="1c9eb-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png


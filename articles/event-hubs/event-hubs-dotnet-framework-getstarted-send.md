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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Verzenden van gebeurtenissen tooAzure Event Hubs met behulp van Hallo .NET Framework

## <a name="introduction"></a>Inleiding

Event Hubs is een service die grote hoeveelheden gebeurtenisgegevens (telemetrie) van verbonden apparaten en toepassingen verwerkt. Nadat u gegevens in Event Hubs hebt verzameld, kunt u Hallo gegevensopslag met behulp van een opslagcluster of transformeren met een realtime analytics-provider. Deze gebeurtenis grootschalige verzamelen en verwerken mogelijkheid is een belangrijk onderdeel van moderne toepassingsarchitecturen inclusief Hallo Internet der dingen (IoT).

Deze zelfstudie laat zien hoe toouse hello [Azure-portal](https://portal.azure.com) toocreate een event hub. U ziet ook hoe toosend gebeurtenissen tooan event hub met een consoletoepassing die is geschreven in C# met behulp van .NET Framework Hallo. tooreceive gebeurtenissen met Hallo .NET Framework, Zie Hallo [ontvangen van gebeurtenissen met behulp van .NET Framework Hallo](event-hubs-dotnet-framework-getstarted-receive-eph.md) artikel, of klik op de juiste Hallo ontvangende taal in Hallo links inhoudsopgave.

toocomplete in deze zelfstudie, moet u Hallo volgende vereisten:

* [Microsoft Visual Studio 2015 of hoger](http://visualstudio.com). Hallo schermopnamen in deze zelfstudie gebruiken Visual Studio 2017.
* Een actief Azure-account. Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Een Event Hubs-naamruimte en een Event Hub maken

de eerste stap Hallo is toouse hello [Azure-portal](https://portal.azure.com) toocreate een naamruimte van Event Hubs typt en beheerreferenties Hallo uw toepassing moet toocommunicate met Hallo event hub. toocreate een naamruimte en event hub, volgt u de procedure Hallo in [in dit artikel](event-hubs-create.md), gaat u verder met de Hallo stappen in deze zelfstudie te volgen.

## <a name="create-a-sender-console-application"></a>Een consoletoepassing voor afzenders maken

In deze sectie schrijft u een Windows-consoletoepassing die gebeurtenissen tooyour event hub verzendt.

1. Maak in Visual Studio een nieuw Visual C# bureaublad-App-project met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **afzender**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. Klik in Solution Explorer met de rechtermuisknop op Hallo **afzender** project en klik vervolgens op **NuGet-pakketten beheren voor oplossing**. 
3. Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`. Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Visual Studio downloadt, installeert en voegt u een verwijzing toohello [bibliotheek NuGet-pakket Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Hallo na toohello velden toevoegen **programma** klasse, vervangen door waarden van de tijdelijke aanduiding Hallo Hallo-naam van Hallo event hub die u hebt gemaakt in de vorige sectie Hallo en Hallo naamruimteniveau verbindingsreeks u eerder hebt opgeslagen.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Hallo na methode toohello toevoegen **programma** klasse:
   
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
   
  Deze methode verzendt continu gebeurtenissen tooyour event hub, met een vertraging van 200 ms.
7. Voeg regels toohello na Hallo **Main** methode:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Hallo-programma uitvoeren en zorg ervoor dat er geen fouten.
  
Gefeliciteerd. U hebt nu verzonden berichten tooan event hub.

## <a name="next-steps"></a>Volgende stappen
Nu dat u een werkende toepassing die een event hub maakt en verzendt gegevens hebt gemaakt, kunt u op toohello volgen scenario's:

* [Hallo Event Processor Host met gebeurtenissen ontvangen](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Documentatie over de gebeurtenisprocessorhost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Event Hubs-overzicht](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png


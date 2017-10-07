---
title: aaa.NET toepassing met meerdere lagen Azure Service Bus | Microsoft Docs
description: Een .NET-zelfstudie waarmee u een app in Azure die gebruikmaakt van Service Bus-wachtrijen toocommunicate tussen lagen met meerdere lagen ontwikkelen.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a>.NET-toepassing met meerdere lagen die Azure Service Bus-wachtrijen gebruikt
## <a name="introduction"></a>Inleiding
Ontwikkelen voor Microsoft Azure is eenvoudig met Visual Studio en Hallo gratis Azure SDK voor .NET. Deze zelfstudie wordt u begeleid Hallo stappen toocreate een toepassing die gebruikmaakt van meerdere Azure-resources in uw lokale omgeving.

U leert Hallo volgende:

* Hoe tooenable uw computer voor het ontwikkelen van Azure met één downloaden en installeren.
* Hoe toouse Visual Studio toodevelop voor Azure.
* Hoe een toepassing met meerdere lagen in Azure met behulp van web-en werkrollen toocreate.
* Hoe toocommunicate tussen lagen met Service Bus-wachtrijen.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

In deze zelfstudie hebt u bouwen en uitvoeren van toepassing met meerdere lagen Hallo in een Azure-cloudservice. Hallo-front-end is een ASP.NET MVC-Webrol en Hallo back-end een werkrol die gebruikmaakt van een Service Bus-wachtrij is. U kunt maken Hallo dezelfde toepassing met meerdere lagen Hallo front-end als een webproject dat geïmplementeerde tooan Azure-website in plaats van een cloudservice. U kunt ook proberen Hallo [.NET on-premises/hybride cloud-toepassing](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) zelfstudie.

Hallo volgende schermafbeelding ziet u de toepassing hello voltooid.

![][0]

## <a name="scenario-overview-inter-role-communication"></a>Scenario-overzicht: communicatie tussen rollen
een order voor het verwerken van Hallo front-end UI-onderdeel, uitgevoerd in de Webrol hello, toosubmit moet communiceren met de Hallo middelste laag logica uitgevoerd in de werkrol Hallo. In dit voorbeeld wordt Service Bus-berichtenservice voor communicatie tussen lagen Hallo Hallo.

Met Service Bus, uitwisseling van berichten tussen Hallo web en de middelste laag worden de twee onderdelen losgekoppeld. Daarentegen toodirect messaging (dat wil zeggen, TCP of HTTP), Hallo weblaag toohello middelste laag niet rechtstreeks; verbinding in plaats daarvan stuurt het werkeenheden, als berichten, naar Service Bus die betrouwbaar behoudt deze totdat de middelste laag Hallo tooconsume gereed is en deze te verwerken.

Service Bus biedt twee entiteiten toosupport brokered messaging: wachtrijen en onderwerpen. Met wachtrijen wordt verzonden elk bericht toohello wachtrij wordt gebruikt door een enkele ontvanger. Onderwerpen ondersteunen Hallo publiceren/abonneren patroon waarin elk gepubliceerde bericht beschikbaar tooa abonnement geregistreerd bij Hallo onderwerp is gemaakt. Elk abonnement onderhoudt logisch gezien zijn eigen wachtrij met berichten. Abonnementen kunnen ook worden geconfigureerd met filterregels die Hallo set berichten doorgegeven aan Hallo abonnement wachtrij toothose die overeenkomen met Hallo filter beperken. Hallo wordt volgende voorbeeld Service Bus-wachtrijen.

![][1]

Dit communicatiemechanisme heeft verschillende voordelen ten opzichte van Direct Messaging:

* **Tijdelijke ontkoppeling.** Met de Hallo asynchrone berichtenpatroon producenten en consumenten hoeven niet te worden online op Hallo hetzelfde moment. Service Bus slaat berichten veilig op totdat Hallo verbruikende partij gereed is om ze te ontvangen. Hierdoor Hallo onderdelen van Hallo gedistribueerde toepassing toobe losgekoppeld-hetzij vrijwillig, bijvoorbeeld voor onderhoud, hetzij vanwege het vastlopen van tooa onderdeel zonder enige impact op het systeem als geheel. Bovendien hoeft Hallo verbruikt toepassing alleen online toocome bepaalde tijdstippen gedurende Hallo dag.
* **Herverdeling van taken.** In veel toepassingen varieert de systeembelasting gedurende een periode, terwijl Hallo benodigde verwerkingstijd voor elke werkeenheid doorgaans constant blijft. Tussen bericht producenten en consumenten met een wachtrij betekent dat Hallo verbruikt toobe behoeften alleen van toepassing (Hallo worker) ingericht tooaccommodate gemiddelde belasting in plaats van piekbelasting. Hallo diepte van Hallo wachtrij neemt toe of af als de inkomende belasting Hallo varieert. Dit bespaart rechtstreeks geld in termen van Hallo hoeveelheid infrastructuur vereist tooservice Hallo toepassing werklast.
* **Taakverdeling.** Naarmate het verkeer toeneemt, kan meer werkprocessen kunnen tooread uit de wachtrij Hallo worden toegevoegd. Elk bericht wordt verwerkt door slechts één van de werkprocessen Hallo. Bovendien deze pull-gebaseerde taakverdeling optimaal gebruik van de werkmachines Hallo zelfs als kan de werkmachines verschilt verwerkingskracht, zoals ze op eigen maximale snelheid berichten ophalen. Dit patroon wordt vaak aangeduid als Hallo *concurrerend consumenten* patroon.
  
  ![][2]

Hallo volgende secties worden besproken Hallo-code waarmee deze architectuur.

## <a name="set-up-hello-development-environment"></a>Hallo-ontwikkelomgeving instellen
Voordat u kunt Azure-toepassingen te ontwikkelen, Hallo-hulpprogramma's ophalen en instellen van uw ontwikkelomgeving.

1. Installeer hello Azure SDK voor .NET via Hallo SDK [pagina downloads](https://azure.microsoft.com/downloads/).
2. In Hallo **.NET** kolom, klikt u op Hallo-versie van [Visual Studio](http://www.visualstudio.com) u gebruikt. Hallo stappen in deze zelfstudie Gebruik Visual Studio 2015, maar ze werken ook met Visual Studio 2017.
3. Wanneer u daarom wordt gevraagd toorun of Hallo installatieprogramma opslaat, klikt u op **uitvoeren**.
4. In Hallo **Web Platform Installer**, klikt u op **installeren** te gaan met Hallo-installatie.
5. Zodra Hallo-installatie voltooid is, hebt u alles wat u nodig toostart toodevelop Hallo app. Hallo SDK bevat hulpprogramma's waarmee u eenvoudig Azure toepassingen ontwikkelen in Visual Studio.

## <a name="create-a-namespace"></a>Een naamruimte maken
de volgende stap Hallo toocreate is een Servicenaamruimte en ophalen van een Shared Access Signature (SAS)-sleutel. Een naamruimte biedt een toepassingsbegrenzing voor elke toepassing die toegankelijk is via Service Bus. Een SAS-sleutel wordt gegenereerd door Hallo systeem wanneer een naamruimte is gemaakt. Hallo combinatie van naamruimte en SAS-sleutel biedt Hallo referenties voor Service Bus tooauthenticate toegang tooan toepassing.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a>Een webrol maken
In deze sectie bouwt u Hallo-front-end van uw toepassing. U maakt eerst Hallo-pagina's die uw toepassing worden weergegeven.
Voeg daarna code items tooa Service Bus-wachtrij verzendt en geeft statusinformatie weer over Hallo wachtrij.

### <a name="create-hello-project"></a>Hallo-project maken
1. Visual Studio met administratorbevoegdheden starten: klik met de rechtermuisknop Hallo **Visual Studio** programmapictogram en klik vervolgens op **als administrator uitvoeren**. Hello Azure-rekenemulator, die verderop in dit artikel wordt besproken vereist dat Visual Studio met administratorbevoegdheden worden gestart.
   
   In Visual Studio op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
2. Klik vanuit **Geïnstalleerde sjablonen** onder **Visual C#** op **Cloud** en klik vervolgens op **Azure Cloud Service**. Naam Hallo project **MultiTierApp**. Klik vervolgens op **OK**.
   
   ![][9]
3. Dubbelklik vanuit **.NET Framework 4.5**-rollen op **ASP.NET-webrol**.
   
   ![][10]
4. Beweeg de muisaanwijzer over **WebRole1** onder **Azure Cloud Service-oplossing**, klik op het potloodpictogram Hallo en wijzig de naam van de Webrol hello te**FrontendWebRole**. Klik vervolgens op **OK**. (Zorg ervoor dat u 'Frontend' invoert met een kleine letter 'e', dus niet 'FrontEnd'.)
   
   ![][11]
5. Van Hallo **nieuw ASP.NET-Project** dialoogvenster in Hallo **Selecteer een sjabloon** lijst, klikt u op **MVC**.
   
   ![][12]
6. Nog steeds in Hallo **nieuw ASP.NET-Project** dialoogvenster vak, klikt u op Hallo **verificatie wijzigen** knop. In Hallo **verificatie wijzigen** in het dialoogvenster, klikt u op **geen verificatie**, en klik vervolgens op **OK**. In deze zelfstudie implementeert u een app waarvoor geen gebruikersaanmelding nodig is.
   
    ![][16]
7. Terug in Hallo **nieuw ASP.NET-Project** in het dialoogvenster, klikt u op **OK** toocreate Hallo project.
8. In **Solution Explorer**, in Hallo **FrontendWebRole** project, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **NuGet-pakketten beheren**.
9. Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`. Selecteer Hallo **WindowsAzure.ServiceBus** van het pakket, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.
   
   ![][13]
   
   Houd er rekening mee dat Hallo vereiste clientassembly nu wordt verwezen en enkele nieuwe codebestanden toegevoegd.
10. Klik in **Solution Explorer** met de rechtermuisknop op **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**. In Hallo **naam** vak, Hallo typenaam **OnlineOrder.cs**. Klik vervolgens op **Toevoegen**.

### <a name="write-hello-code-for-your-web-role"></a>Hallo-code voor de Webrol schrijven
In deze sectie maakt u Hallo verschillende pagina's die uw toepassing worden weergegeven.

1. Vervang de bestaande naamruimtedefinitie Hello na de code in Hallo OnlineOrder.cs bestand in Visual Studio:
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. Dubbelklik in **Solution Explorer** op **Controllers\HomeController.cs**. Voeg de volgende Hallo **met** instructies Hallo Hallo bovenaan in het bestand tooinclude Hallo naamruimten voor het model dat u zojuist hebt gemaakt, maar ook voor Service Bus.
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. Ook in Hallo HomeController.cs bestand in Visual Studio vervangt u de bestaande naamruimtedefinitie Hello code te volgen. Deze code bevat methoden voor het indienen van items toohello wachtrij Hallo afhandelen.
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. Van Hallo **bouwen** menu, klikt u op **Build Solution** tootest Hallo juistheid van uw werk tot nu toe.
5. Maak nu de weergave Hallo voor Hallo `Submit()` methode die u eerder hebt gemaakt. Met de rechtermuisknop op Hallo `Submit()` methode (Hallo overbelasting van de `Submit()` die geen parameters zijn vereist), en kies vervolgens **weergave toevoegen**.
   
   ![][14]
6. Er verschijnt een dialoogvenster voor het maken van Hallo weergeven. In Hallo **sjabloon** Kies **maken**. In Hallo **Modelklasse** lijst, klikt u op Hallo **OnlineOrder** klasse.
   
   ![][15]
7. Klik op **Add**.
8. Wijzig nu de naam van uw toepassing hello weergegeven. In **Solution Explorer**, dubbelklikt u op de **Views\Shared\\_Layout.cshtml** tooopen bestand in Visual Studio-editor Hallo.
9. Vervang alle instanties van **Mijn ASP.NET-toepassing** door **Producten van LITWARE**.
10. Hallo verwijderen **Start**, **over**, en **Contact** koppelingen. Verwijder Hallo gemarkeerde code:
    
    ![][28]
11. Ten slotte wijzigen Hallo verzending pagina tooinclude enige informatie over Hallo wachtrij. In **Solution Explorer**, dubbelklikt u op de **Views\Home\Submit.cshtml** tooopen bestand in Visual Studio-editor Hallo. Hallo volgt regel na toevoegen `<h2>Submit</h2>`. Op dit moment Hallo `ViewBag.MessageCount` is leeg. U vult dit later in.
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. U hebt nu de gebruikersinterface geïmplementeerd. U kunt ook op **F5** toorun uw toepassing en Bevestig dat het lijkt erop zoals verwacht.
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a>Hallo-code voor het indienen van items tooa Service Bus-wachtrij schrijven
Voeg nu code voor het indienen van items tooa wachtrij. U maakt eerst een klasse die de verbindingsgegevens van de Service Bus-wachtrij bevat. Vervolgens initialiseert u de verbinding vanuit Global.aspx.cs. Tot slot werkt Hallo verzendcode die u eerder in HomeController.cs tooactually indienen items tooa Service Bus-wachtrij gemaakt.

1. In **Solution Explorer**, met de rechtermuisknop op **FrontendWebRole** (Klik met de rechtermuisknop Hallo project, niet Hallo rol). Klik op **Toevoegen** en klik vervolgens op **Klasse**.
2. Naam Hallo klasse **QueueConnector.cs**. Klik op **toevoegen** toocreate Hallo-klasse.
3. Voeg nu code die de verbindingsgegevens Hallo ingekapseld en Hallo verbinding tooa Service Bus-wachtrij wordt geïnitialiseerd. Vervang Hallo volledige inhoud van QueueConnector.cs door Hallo volgende code en voer waarden in voor `your Service Bus namespace` (uw naamruimtenaam) en `yourKey`, namelijk Hallo **primaire sleutel** u eerder hebt verkregen via hello Azure Portal.
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. Controleer nu of uw methode voor **Initialiseren** wordt aangeroepen. Dubbelklik in **Solution Explorer** op **Global.asax\Global.asax.cs**.
5. Toevoegen van de volgende regel code achter Hallo HALLO hallo **Application_Start** methode.
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. Werk tot slot de Webcode die u eerder hebt gemaakt, als u items toohello wachtrij Hallo. Dubbelklik in **Solution Explorer** op **Controllers\HomeController.cs**.
7. Update Hallo `Submit()` methode (Hallo overbelasting waarvoor geen parameters zijn vereist) als volgt het Hallo-bericht tooget tellen voor Hallo wachtrij.
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. Update Hallo `Submit(OnlineOrder order)` methode (Hallo overbelasting waarvoor één parameter) als volgt toosubmit informatie toohello wachtrij rangschikken.
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. U kunt nu de toepassing hello opnieuw uitvoeren. Telkens wanneer die u een order verzendt aantal Hallo-berichten neemt toe.
   
   ![][18]

## <a name="create-hello-worker-role"></a>Hallo-werkrol maken
U maakt nu de werkrol Hallo waarmee Hallo volgorde van voorbeelden worden verwerkt. In dit voorbeeld wordt Hallo **Werkrol met Service Bus-wachtrij** Visual Studio-projectsjabloon. U hebt al Hallo vereist referenties verkregen via Hallo-portal.

1. Zorg ervoor dat u Visual Studio tooyour Azure-account hebt gekoppeld.
2. In Visual Studio in **Solution Explorer** met de rechtermuisknop op de **rollen** map onder Hallo **MultiTierApp** project.
3. Klik op **Toevoegen** en klik vervolgens op **Nieuw werkrolproject**. Hallo **nieuw Rolproject toevoegen** dialoogvenster wordt weergegeven.
   
   ![][26]
4. In Hallo **nieuw Rolproject toevoegen** in het dialoogvenster, klikt u op **Werkrol met Service Bus-wachtrij**.
   
   ![][23]
5. In Hallo **naam** vak, naam Hallo project **OrderProcessingRole**. Klik vervolgens op **Toevoegen**.
6. Hallo-verbindingsreeks die u hebt verkregen in stap 9 van Hallo 'Een Servicebus-naamruimte maken' sectie toohello Klembord kopiëren.
7. In **Solution Explorer**, klik met de rechtermuisknop Hallo **OrderProcessingRole** u in stap 5 hebt gemaakt (Zorg ervoor dat u met de rechtermuisknop op **OrderProcessingRole** onder **Rollen**, en niet Hallo klasse). Klik vervolgens op **Eigenschappen**.
8. Op Hallo **instellingen** tabblad Hallo **eigenschappen** in het dialoogvenster, klikt u in Hallo **waarde** vak voor **Microsoft.ServiceBus.ConnectionString**, en plak vervolgens Hallo-eindpuntwaarde die u in stap 6 hebt gekopieerd.
   
   ![][25]
9. Maak een **OnlineOrder** toorepresent Hallo orders klasse tijdens het verwerken van Hallo wachtrij. U kunt een klasse die u al hebt gemaakt opnieuw gebruiken. In **Solution Explorer**, klik met de rechtermuisknop Hallo **OrderProcessingRole** klasse (Klik met de rechtermuisknop Hallo klassepictogram, niet Hallo rol). Klik op **Toevoegen** en vervolgens op **Bestaand item**.
10. Blader toohello submap voor **FrontendWebRole\Models**, en dubbelklik vervolgens op **OnlineOrder.cs** tooadd het toothis project.
11. In **WorkerRole.cs**, wijzig de waarde Hallo Hallo **wachtrijnaam** variabele van `"ProcessingQueue"` te`"OrdersQueue"` zoals weergegeven in de volgende code Hallo.
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. Voeg de volgende Hallo gebruiksinstructie Hallo boven aan het Hallo-WorkerRole.cs-bestand.
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. In Hallo `Run()` functie binnen Hallo `OnMessage()` aanroepen, vervang de inhoud Hallo Hallo `try` component Hello code te volgen.
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. U kunt de toepassing hello hebt voltooid. U kunt de volledige toepassing hello testen door met de rechtermuisknop op Hallo MultiTierApp-project in Solution Explorer selecteren **instellen als opstartproject**, en klik vervolgens op F5 te drukken. Houd er rekening mee dat het aantal berichten niet toeneemt, omdat het Hallo-werkrol items uit de wachtrij hello, verwerkt en als voltooid markeert. U ziet Hallo trace-uitvoer van uw werkrol door hello Azure Compute-Emulator gebruikersinterface weer te geven. U kunt dit doen met de rechtermuisknop op Hallo emulatorpictogram in systeemvak Hallo van de taakbalk en selecteer **weergeven Compute-Emulator UI**.
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Service Bus Zie Hallo resources te volgen:  

* [Documentatie voor Azure Service Bus][sbdocs]  
* [Service Bus-servicepagina][sbacom]  
* [Hoe tooUse Service Bus-wachtrijen][sbacomqhowto]  

toolearn meer informatie over scenario's met meerdere lagen, Zie:  

* [.NET-toepassing met meerdere lagen met Table Storage, Queue Storage en Blob Storage][mutitierstorage]  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36

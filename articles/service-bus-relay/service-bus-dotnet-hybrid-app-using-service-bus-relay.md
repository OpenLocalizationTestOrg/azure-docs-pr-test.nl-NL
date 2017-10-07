---
title: aaaAzure WCF Relay hybride-toepassing voor on-premises/cloudtoepassing (.NET) | Microsoft Docs
description: Meer informatie over hoe toocreate een .NET on-premises/cloudtoepassing met Azure WCF Relay hybride-toepassing.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9ed02f7c-ebfb-4f39-9c97-b7dc15bcb4c1
ms.service: service-bus-relay
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: sethm
ms.openlocfilehash: aab8b1dbdc85c4edf7b0ccef0921b69524b2d306
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a>Hybride .NET on-premises/cloudtoepassing met Azure WCF Relay
## <a name="introduction"></a>Inleiding

Dit artikel laat zien hoe toobuild een hybride cloud-toepassing met Microsoft Azure en Visual Studio. Hallo-zelfstudie wordt ervan uitgegaan dat u hebt geen ervaring met Azure. In minder dan 30 minuten hebt u een toepassing die meerdere Azure-resources maakt het gebruik van en uitgevoerd in de cloud Hallo.

U leert:

* Hoe toocreate of een bestaande webservice voor verbruik door een weboplossing aanpassen.
* Hoe toouse hello Azure WCF Relay-service tooshare gegevens tussen een Azure-toepassing en een webservice die elders wordt gehost.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a>Hoe Azure hulp biedt bij hybride oplossingen

Bedrijfsoplossingen bestaan meestal uit een combinatie van aangepaste code geschreven tootackle nieuwe en unieke zakelijke vereisten en bestaande functionaliteit van oplossingen en systemen die al aanwezig zijn.

Oplossingsarchitecten begint toouse Hallo cloud om gemakkelijk aan schaalvereisten te voldoen en operationele kosten te verlagen. Hierbij vinden ze dat bestaande serviceassets die ze graag tooleverage als bouwstenen voor hun oplossingen in de bedrijfsfirewall Hallo en niet gemakkelijk zijn bereikbaar zijn voor Hallo cloudoplossing. Veel interne services zijn niet gemaakt of gehost op een manier die ze eenvoudig kunnen worden blootgesteld aan de rand van Hallo bedrijfsnetwerk.

[Azure Relay](https://azure.microsoft.com/services/service-bus/) is ontworpen voor Hallo gebruikstoepassing waarbij bestaande webservices van Windows Communication Foundation (WCF) en zodat deze veilig toegankelijk toosolutions die zich buiten de bedrijfsperimeter Hallo zonder services Tussenkomende wijzigingen toohello bedrijfsnetwerkinfrastructuur. Dergelijke relay-services worden nog steeds gehost binnen hun bestaande omgeving, maar ze dragen het luisteren naar binnenkomende sessies en aanvragen toohello cloud-gebaseerde relay-service. Ook beveiligt Azure Relay deze services tegen onbevoegde toegang door [SAS (Shared Access Signature)](../service-bus-messaging/service-bus-sas.md)-verificatie te gebruiken.

## <a name="solution-scenario"></a>Oplossingsscenario
In deze zelfstudie maakt u een ASP.NET-website waarmee u een lijst met producten op Hallo inventaris productpagina toosee.

![][0]

Hallo-zelfstudie wordt ervan uitgegaan dat u productgegevens in een bestaande on-premises systeem hebt en maakt gebruik van Azure Relay tooreach dat systeem. Dit wordt gesimuleerd door een webservice die in een eenvoudige consoletoepassing wordt uitgevoerd en wordt ondersteund door een set producten in het geheugen. U kunt toorun deze consoletoepassing op uw eigen computer en Hallo Webrol in Azure implementeert. Doet, ziet u hoe Hallo Webrol uitgevoerd in de Azure-datacenter Hallo inderdaad wordt gebeld op uw computer, ondanks dat de computer bijna zeker achter ten minste één firewall en een network address translation (NAT) laag blijven staan.

## <a name="set-up-hello-development-environment"></a>Hallo-ontwikkelomgeving instellen

Voordat u kunt Azure-toepassingen te ontwikkelen, Hallo-hulpprogramma's downloaden en uw ontwikkelomgeving instellen:

1. Installeer hello Azure SDK voor .NET via Hallo SDK [pagina downloads](https://azure.microsoft.com/downloads/).
2. In Hallo **.NET** kolom, klikt u op Hallo-versie van [Visual Studio](http://www.visualstudio.com) u gebruikt. Hallo stappen in deze zelfstudie Gebruik Visual Studio 2015, maar ze werken ook met Visual Studio 2017.
3. Wanneer u daarom wordt gevraagd toorun of Hallo installatieprogramma opslaat, klikt u op **uitvoeren**.
4. In Hallo **Web Platform Installer**, klikt u op **installeren** te gaan met Hallo-installatie.
5. Zodra Hallo-installatie voltooid is, hebt u alles wat u nodig toostart toodevelop Hallo app. Hallo SDK bevat hulpprogramma's waarmee u eenvoudig Azure toepassingen ontwikkelen in Visual Studio.

## <a name="create-a-namespace"></a>Een naamruimte maken

met behulp van toobegin Hallo relay-functies in Azure, moet u eerst een Servicenaamruimte maken. Een naamruimte biedt een scoping container voor het verwerken van Azure-resources in uw toepassing. Ga als volgt Hallo [hier instructies](relay-create-namespace-portal.md) toocreate een Relay-naamruimte.

## <a name="create-an-on-premises-server"></a>Een on-premises server maken

U bouwt eerst een on-premises (model)systeem voor de productcatalogus op. Dit is redelijk eenvoudig; u kunt dit zien als het representeren van een werkelijk on-premises productcatalogussysteem met een volledige serviceoppervlak dat we toointegrate proberen.

Dit project is een Visual Studio-consoletoepassing en gebruikt Hallo [Azure Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Hallo Service Bus-bibliotheken en configuratie-instellingen.

### <a name="create-hello-project"></a>Hallo-project maken

1. Start Microsoft Visual Studio met administratorbevoegdheden. toodo dus programmapictogram Hallo-Visual Studio met de rechtermuisknop op en klik vervolgens op **als administrator uitvoeren**.
2. In Visual Studio op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
3. Klik bij **Geïnstalleerde sjablonen**, onder **Visual C#**, op **Consoletoepassing (.NET Framework)**. In Hallo **naam** vak, Hallo typenaam **ProductsServer**:

   ![][11]
4. Klik op **OK** toocreate hello **ProductsServer** project.
5. Als u Hallo NuGet package manager voor Visual Studio al hebt geïnstalleerd, moet u de volgende stap toohello overslaan. Anders gaat u naar [NuGet][NuGet] en klikt u op [NuGet installeren](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c). Ga als volgt Hallo prompts tooinstall hello NuGet-Pakketbeheer en Visual Studio opnieuw te starten.
6. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsServer** project en klik vervolgens op **NuGet-pakketten beheren**.
7. Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`. Selecteer Hallo **WindowsAzure.ServiceBus** pakket.
8. Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.

   ![][13]

   Houd er rekening mee dat Hallo vereiste clientassembly nu wordt verwezen.
8. Voeg een nieuwe klasse voor uw productcontract toe. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsServer** project en klik op **toevoegen**, en klik vervolgens op **klasse**.
9. In Hallo **naam** vak, Hallo typenaam **ProductsContract.cs**. Klik vervolgens op **Toevoegen**.
10. In **ProductsContract.cs**, vervang de naamruimtedefinitie Hallo door Hallo volgende code waarmee Hallo contract voor Hallo-service wordt gedefinieerd.

    ```csharp
    namespace ProductsServer
    {
        using System.Collections.Generic;
        using System.Runtime.Serialization;
        using System.ServiceModel;

        // Define hello data contract for hello service
        [DataContract]
        // Declare hello serializable properties.
        public class ProductData
        {
            [DataMember]
            public string Id { get; set; }
            [DataMember]
            public string Name { get; set; }
            [DataMember]
            public string Quantity { get; set; }
        }

        // Define hello service contract.
        [ServiceContract]
        interface IProducts
        {
            [OperationContract]
            IList<ProductData> GetProducts();

        }

        interface IProductsChannel : IProducts, IClientChannel
        {
        }
    }
    ```
11. Vervang in Program.cs de naamruimtedefinitie Hallo met de volgende code, die wordt toegevoegd Hallo-Profielservice en Hallo host voor deze Hallo.

    ```csharp
    namespace ProductsServer
    {
        using System;
        using System.Linq;
        using System.Collections.Generic;
        using System.ServiceModel;

        // Implement hello IProducts interface.
        class ProductsService : IProducts
        {

            // Populate array of products for display on website
            ProductData[] products =
                new []
                    {
                        new ProductData{ Id = "1", Name = "Rock",
                                         Quantity = "1"},
                        new ProductData{ Id = "2", Name = "Paper",
                                         Quantity = "3"},
                        new ProductData{ Id = "3", Name = "Scissors",
                                         Quantity = "5"},
                        new ProductData{ Id = "4", Name = "Well",
                                         Quantity = "2500"},
                    };

            // Display a message in hello service console application
            // when hello list of products is retrieved.
            public IList<ProductData> GetProducts()
            {
                Console.WriteLine("GetProducts called.");
                return products;
            }

        }

        class Program
        {
            // Define hello Main() function in hello service application.
            static void Main(string[] args)
            {
                var sh = new ServiceHost(typeof(ProductsService));
                sh.Open();

                Console.WriteLine("Press ENTER tooclose");
                Console.ReadLine();

                sh.Close();
            }
        }
    }
    ```
12. Dubbelklik in Solution Explorer op Hallo **App.config** bestand tooopen in Hallo Visual Studio-editor. Hallo Hallo onderaan in `<system.ServiceModel>` element (maar nog steeds binnen `<system.ServiceModel>`), Hallo volgende XML-code toevoegen. Ervoor tooreplace worden *yourServiceNamespace* met de naam van uw naamruimte Hallo en *yourKey* met SAS-sleutel Hallo u eerder hebt opgehaald via de portal Hallo:

    ```xml
    <system.serviceModel>
    ...
      <services>
         <service name="ProductsServer.ProductsService">
           <endpoint address="sb://yourServiceNamespace.servicebus.windows.net/products" binding="netTcpRelayBinding" contract="ProductsServer.IProducts" behaviorConfiguration="products"/>
         </service>
      </services>
      <behaviors>
         <endpointBehaviors>
           <behavior name="products">
             <transportClientEndpointBehavior>
                <tokenProvider>
                   <sharedAccessSignature keyName="RootManageSharedAccessKey" key="yourKey" />
                </tokenProvider>
             </transportClientEndpointBehavior>
           </behavior>
         </endpointBehaviors>
      </behaviors>
    </system.serviceModel>
    ```
13. Nog steeds in App.config in Hallo `<appSettings>` vervangen Hallo gegevensbronwaarde met verbindingsreeks die u eerder hebt verkregen via de portal Hallo Hallo-element.

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. Druk op **Ctrl + Shift + B** of van Hallo **bouwen** menu, klikt u op **Build Solution** toobuild toepassing hello en controleer Hallo juistheid van uw werk tot nu toe.

## <a name="create-an-aspnet-application"></a>Een ASP.NET-toepassing maken

In deze sectie bouwt u een eenvoudige ASP.NET-toepassing op waarmee gegevens worden weergegeven die u uit uw productservice hebt opgehaald.

### <a name="create-hello-project"></a>Hallo-project maken

1. Zorg ervoor dat Visual Studio met administratorbevoegdheden wordt uitgevoerd.
2. In Visual Studio op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.
3. Klik bij **Geïnstalleerde sjablonen**, onder **Visual C#**, op **ASP.NET-webtoepassing (.NET Framework)**. Naam Hallo project **ProductsPortal**. Klik vervolgens op **OK**.

   ![][15]

4. Van Hallo **ASP.NET sjablonen** lijst in Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **MVC**.

   ![][16]

6. Klik op Hallo **verificatie wijzigen** knop. In Hallo **verificatie wijzigen** dialoogvenster vak, zorg ervoor dat **geen verificatie** is geselecteerd en klik vervolgens op **OK**. In deze zelfstudie implementeert u een app waarvoor geen gebruikersaanmelding nodig is.

    ![][18]

7. Terug in Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **OK** toocreate Hallo MVC-app.
8. U moet nu Azure-resources configureren voor een nieuwe web-app. Volg de stappen Hallo in Hallo [tooAzure sectie van dit artikel publiceren](../app-service-web/app-service-web-get-started-dotnet.md). Vervolgens toothis zelfstudie retourneren en de volgende stap toohello gaan.
10. Klik in Solution Explorer met de rechtermuisknop op **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**. In Hallo **naam** vak, Hallo typenaam **Product.cs**. Klik vervolgens op **Toevoegen**.

    ![][17]

### <a name="modify-hello-web-application"></a>Hallo-webtoepassing wijzigen

1. In Hallo Product.cs bestand in Visual Studio vervangt u de bestaande naamruimtedefinitie Hallo Hello code te volgen.

   ```csharp
    // Declare properties for hello products inventory.
    namespace ProductsWeb.Models
    {
       public class Product
       {
           public string Id { get; set; }
           public string Name { get; set; }
           public string Quantity { get; set; }
       }
    }
    ```
2. Vouw in Solution Explorer Hallo **domeincontrollers** map, dubbelklikt u vervolgens op Hallo **HomeController.cs** tooopen bestand in Visual Studio.
3. In **HomeController.cs**, de bestaande naamruimtedefinitie Hallo vervangen door Hallo code te volgen.

    ```csharp
    namespace ProductsWeb.Controllers
    {
        using System.Collections.Generic;
        using System.Web.Mvc;
        using Models;

        public class HomeController : Controller
        {
            // Return a view of hello products inventory.
            public ActionResult Index(string Identifier, string ProductName)
            {
                var products = new List<Product>
                    {new Product {Id = Identifier, Name = ProductName}};
                return View(products);
            }
         }
    }
    ```
4. Vouw in Solution Explorer de map Views\Shared Hallo uit en dubbelklik vervolgens **_Layout.cshtml** tooopen in Hallo Visual Studio-editor.
5. Wijzig alle instanties van **mijn ASP.NET-toepassing** te**producten van LITWARE**.
6. Hallo verwijderen **Start**, **over**, en **Contact** koppelingen. Verwijder in Hallo voorbeeld te volgen, Hallo gemarkeerd code.

    ![][41]

7. Vouw in Solution Explorer de map Views\Home Hallo uit en dubbelklik vervolgens **Index.cshtml** tooopen in Hallo Visual Studio-editor. Vervang de volledige inhoud van de Hallo van Hallo-bestand met de volgende code Hallo.

   ```html
   @model IEnumerable<ProductsWeb.Models.Product>

   @{
            ViewBag.Title = "Index";
   }

   <h2>Prod Inventory</h2>

   <table>
             <tr>
                 <th>
                     @Html.DisplayNameFor(model => model.Name)
                 </th>
                 <th></th>
                 <th>
                     @Html.DisplayNameFor(model => model.Quantity)
                 </th>
             </tr>

   @foreach (var item in Model) {
             <tr>
                 <td>
                     @Html.DisplayFor(modelItem => item.Name)
                 </td>
                 <td>
                     @Html.DisplayFor(modelItem => item.Quantity)
                 </td>
             </tr>
   }

   </table>
   ```
8. tooverify hello juistheid van uw werk tot nu toe, drukt u op **Ctrl + Shift + B** toobuild Hallo project.

### <a name="run-hello-app-locally"></a>Hallo-app lokaal uitvoeren

Hallo toepassing tooverify die hierbij worden uitgevoerd.

1. Zorg ervoor dat **ProductsPortal** Hallo actieve project is. Hallo projectnaam in Solution Explorer met de rechtermuisknop en selecteer **instellen als opstartproject**.
2. Druk in Visual Studio op **F5**.
3. Uw toepassing moet dan in een browser worden weergegeven.

   ![][21]

## <a name="put-hello-pieces-together"></a>Hallo softwareonderdelen samenstellen

de volgende stap Hallo is toohook Hallo lokale producten server Hello ASP.NET-toepassing.

1. Als deze nog niet is geopend in Visual Studio opnieuw openen Hallo **ProductsPortal** project dat u hebt gemaakt in Hallo [maken van een ASP.NET-toepassing](#create-an-aspnet-application) sectie.
2. Vergelijkbare toohello stap in de sectie 'Een On-Premises Server maken' hello toevoegen toohello projectverwijzingen voor Hallo NuGet-pakket. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** project en klik vervolgens op **NuGet-pakketten beheren**.
3. Zoek naar 'Service Bus' en selecteer Hallo **WindowsAzure.ServiceBus** item. Vervolgens Hallo installatie voltooien en sluit het dialoogvenster.
4. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** project en klik vervolgens op **toevoegen**, klikt u vervolgens **bestaand Item**.
5. Navigeer toohello **ProductsContract.cs** bestand van Hallo **ProductsServer** console-project. Klik op toohighlight ProductsContract.cs. Klik op Hallo pijl-omlaag naast te**toevoegen**, klikt u vervolgens op **toevoegen als koppeling**.

   ![][24]

6. Open nu Hallo **HomeController.cs** -bestand in Visual Studio-editor Hallo en vervang de naamruimtedefinitie Hallo door Hallo code te volgen. Ervoor tooreplace worden *yourServiceNamespace* met Hallo-naam van uw Servicenaamruimte en *yourKey* met SAS-sleutel. Hiermee schakelt u Hallo toocall Hallo lokale clientservice, Hallo resultaat van Hallo aanroep retourneren.

   ```csharp
   namespace ProductsWeb.Controllers
   {
       using System.Linq;
       using System.ServiceModel;
       using System.Web.Mvc;
       using Microsoft.ServiceBus;
       using Models;
       using ProductsServer;

       public class HomeController : Controller
       {
           // Declare hello channel factory.
           static ChannelFactory<IProductsChannel> channelFactory;

           static HomeController()
           {
               // Create shared access signature token credentials for authentication.
               channelFactory = new ChannelFactory<IProductsChannel>(new NetTcpRelayBinding(),
                   "sb://yourServiceNamespace.servicebus.windows.net/products");
               channelFactory.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior {
                   TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                       "RootManageSharedAccessKey", "yourKey") });
           }

           public ActionResult Index()
           {
               using (IProductsChannel channel = channelFactory.CreateChannel())
               {
                   // Return a view of hello products inventory.
                   return this.View(from prod in channel.GetProducts()
                                    select
                                        new Product { Id = prod.Id, Name = prod.Name,
                                            Quantity = prod.Quantity });
               }
           }
       }
   }
   ```
7. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** oplossing (Zorg ervoor dat tooright en klik op Hallo oplossing, niet Hallo project). Klik op **Toevoegen** en vervolgens op **Bestaand project**.
8. Navigeer toohello **ProductsServer** project en dubbelklik op Hallo **ProductsServer.csproj** oplossing bestand tooadd deze.
9. **ProductsServer** in volgorde toodisplay Hallo gegevens moet worden uitgevoerd op **ProductsPortal**. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** oplossing en op **eigenschappen**. Hallo **eigenschappenvensters** in het dialoogvenster wordt weergegeven.
10. Klik op Hallo linkerkant, **opstartproject**. Klik op aan de rechterkant hello, **meerdere opstartprojecten**. Zorg ervoor dat **ProductsServer** en **ProductsPortal** worden weergegeven in de juiste volgorde, waarbij **Start** ingesteld als Hallo-actie voor beide.

      ![][25]

11. Nog steeds in Hallo **eigenschappen** in het dialoogvenster, klikt u op **Projectafhankelijkheden** op Hallo linkerkant.
12. In Hallo **projecten** lijst, klikt u op **ProductsServer**. Zorg ervoor dat **ProductsPortal** niet is geselecteerd.
13. In Hallo **projecten** lijst, klikt u op **ProductsPortal**. Zorg ervoor dat **ProductsServer** is geselecteerd.

    ![][26]

14. Klik op **OK** in Hallo **eigenschappenvensters** in het dialoogvenster.

## <a name="run-hello-project-locally"></a>Hallo-project lokaal uitvoeren

tootest hello toepassing lokaal door in Visual Studio druk op **F5**. Hallo on-premises-server (**ProductsServer**) moet eerst worden gestart en vervolgens Hallo **ProductsPortal** toepassing worden gestart in een browservenster. Deze tijd ziet u dat Hallo-productinventaris bevat gegevens die uit Hallo product service on-premises systeem opgehaald.

![][10]

Druk op **vernieuwen** op Hallo **ProductsPortal** pagina. Elke keer dat u Hallo pagina vernieuwt, ziet u Hallo server app een bericht weergegeven wanneer `GetProducts()` van **ProductsServer** wordt aangeroepen.

Sluit beide toepassingen voordat u doorgaat toohello volgende stap.

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a>Hallo ProductsPortal project tooan Azure-web-app implementeren

de volgende stap Hallo is toorepublish hello Azure-Web-app **ProductsPortal** frontend. Hallo te volgen:

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** project en klik op **publiceren**. Klik vervolgens op **publiceren** op Hallo **publiceren** pagina.

  > [!NOTE]
  > Wordt er een foutbericht weergegeven in het browservenster Hallo wanneer hello **ProductsPortal** -webproject automatisch wordt gestart na het Hallo-implementatie. Dit is normaal en doet zich voor omdat Hallo **ProductsServer** toepassing nog niet wordt uitgevoerd.
>
>

2. URL van de kopie Hallo Hallo geïmplementeerd web-app naar wens Hallo-URL in de volgende stap Hallo. U kunt ook deze URL ophalen via hello Azure App Service-activiteit venster in Visual Studio:

  ![][9]

3. Sluit Hallo browser venster toostop Hallo toepassing uitvoert.

### <a name="set-productsportal-as-web-app"></a>ProductsPortal instellen als web-app

Voordat u actieve Hallo-toepassing in de cloud hello, moet u ervoor zorgen dat **ProductsPortal** vanuit Visual Studio als een web-app wordt uitgevoerd.

1. In Visual Studio met de rechtermuisknop op Hallo **ProductsPortal** project en klik vervolgens op **eigenschappen**.
2. Klik in de linkerkolom hello, **Web**.
3. In Hallo **actie starten** sectie, klikt u op Hallo **Start-URL** knop, en in het tekstvak Hallo Hallo URL voor uw eerder geïmplementeerde web-app bijvoorbeeld `http://productsportal1234567890.azurewebsites.net/`.

    ![][27]

4. Van Hallo **bestand** menu in Visual Studio, klikt u op **Alles opslaan**.
5. In menu van Hallo bouwen in Visual Studio, klikt u op **oplossing opnieuw opbouwen**.

## <a name="run-hello-application"></a>Hallo-toepassing uitvoeren

1. Druk op F5 toobuild en Voer Hallo-toepassing. Hallo on-premises-server (Hallo **ProductsServer** consoletoepassing) moet eerst worden gestart en vervolgens Hallo **ProductsPortal** toepassing worden gestart in een browservenster wordt weergegeven in het volgende scherm Hallo opgenomen. U ziet opnieuw die productinventaris Hallo ziet u de gegevens uit de Hallo product service on-premises systeem en geeft die gegevens op Hallo web-app. Controleer Hallo URL toomake ervoor dat **ProductsPortal** wordt uitgevoerd in de cloud hello, als een Azure-web-app.

   ![][1]

   > [!IMPORTANT]
   > Hallo **ProductsServer** consoletoepassing moet worden uitgevoerd en kunnen tooserve Hallo gegevens toohello **ProductsPortal** toepassing. Als Hallo browser is een fout weergegeven, wacht u enkele seconden voor **ProductsServer** tooload en weergave hello te volgen. Druk op **vernieuwen** in Hallo browser.
   >
   >

   ![][37]
2. Terug in de browser hello, drukt u op **vernieuwen** op Hallo **ProductsPortal** pagina. Elke keer dat u Hallo pagina vernieuwt, ziet u Hallo server app een bericht weergegeven wanneer `GetProducts()` van **ProductsServer** wordt aangeroepen.

    ![][38]

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over Azure-Relay, Zie Hallo resources te volgen:  

* [Wat is Azure Relay?](relay-what-is-it.md)  
* [Hoe Relay-toouse](service-bus-dotnet-how-to-use-relay.md)  

[0]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hybrid.png
[1]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[NuGet]: http://nuget.org

[11]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-con-1.png
[13]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-13.png
[15]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-2.png
[16]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-4.png
[17]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-7.png
[18]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-5.png
[9]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-9.png
[10]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App3.png

[21]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App1.png
[24]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-12.png
[25]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-13.png
[26]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-14.png
[27]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-web-8.png

[36]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/App2.png
[37]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service1.png
[38]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/hy-service2.png
[41]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-multi-tier-40.png
[43]: ./media/service-bus-dotnet-hybrid-app-using-service-bus-relay/getting-started-hybrid-43.png

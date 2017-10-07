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
# <a name="net-on-premisescloud-hybrid-application-using-azure-wcf-relay"></a><span data-ttu-id="f9f34-103">Hybride .NET on-premises/cloudtoepassing met Azure WCF Relay</span><span class="sxs-lookup"><span data-stu-id="f9f34-103">.NET on-premises/cloud hybrid application using Azure WCF Relay</span></span>
## <a name="introduction"></a><span data-ttu-id="f9f34-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="f9f34-104">Introduction</span></span>

<span data-ttu-id="f9f34-105">Dit artikel laat zien hoe toobuild een hybride cloud-toepassing met Microsoft Azure en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9f34-105">This article shows how toobuild a hybrid cloud application with Microsoft Azure and Visual Studio.</span></span> <span data-ttu-id="f9f34-106">Hallo-zelfstudie wordt ervan uitgegaan dat u hebt geen ervaring met Azure.</span><span class="sxs-lookup"><span data-stu-id="f9f34-106">hello tutorial assumes you have no prior experience using Azure.</span></span> <span data-ttu-id="f9f34-107">In minder dan 30 minuten hebt u een toepassing die meerdere Azure-resources maakt het gebruik van en uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9f34-107">In less than 30 minutes, you will have an application that uses multiple Azure resources up and running in hello cloud.</span></span>

<span data-ttu-id="f9f34-108">U leert:</span><span class="sxs-lookup"><span data-stu-id="f9f34-108">You will learn:</span></span>

* <span data-ttu-id="f9f34-109">Hoe toocreate of een bestaande webservice voor verbruik door een weboplossing aanpassen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-109">How toocreate or adapt an existing web service for consumption by a web solution.</span></span>
* <span data-ttu-id="f9f34-110">Hoe toouse hello Azure WCF Relay-service tooshare gegevens tussen een Azure-toepassing en een webservice die elders wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="f9f34-110">How toouse hello Azure WCF Relay service tooshare data between an Azure application and a web service hosted elsewhere.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="how-azure-relay-helps-with-hybrid-solutions"></a><span data-ttu-id="f9f34-111">Hoe Azure hulp biedt bij hybride oplossingen</span><span class="sxs-lookup"><span data-stu-id="f9f34-111">How Azure Relay helps with hybrid solutions</span></span>

<span data-ttu-id="f9f34-112">Bedrijfsoplossingen bestaan meestal uit een combinatie van aangepaste code geschreven tootackle nieuwe en unieke zakelijke vereisten en bestaande functionaliteit van oplossingen en systemen die al aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="f9f34-112">Business solutions are typically composed of a combination of custom code written tootackle new and unique business requirements and existing functionality provided by solutions and systems that are already in place.</span></span>

<span data-ttu-id="f9f34-113">Oplossingsarchitecten begint toouse Hallo cloud om gemakkelijk aan schaalvereisten te voldoen en operationele kosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-113">Solution architects are starting toouse hello cloud for easier handling of scale requirements and lower operational costs.</span></span> <span data-ttu-id="f9f34-114">Hierbij vinden ze dat bestaande serviceassets die ze graag tooleverage als bouwstenen voor hun oplossingen in de bedrijfsfirewall Hallo en niet gemakkelijk zijn bereikbaar zijn voor Hallo cloudoplossing.</span><span class="sxs-lookup"><span data-stu-id="f9f34-114">In doing so, they find that existing service assets they'd like tooleverage as building blocks for their solutions are inside hello corporate firewall and out of easy reach for access by hello cloud solution.</span></span> <span data-ttu-id="f9f34-115">Veel interne services zijn niet gemaakt of gehost op een manier die ze eenvoudig kunnen worden blootgesteld aan de rand van Hallo bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="f9f34-115">Many internal services are not built or hosted in a way that they can be easily exposed at hello corporate network edge.</span></span>

<span data-ttu-id="f9f34-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is ontworpen voor Hallo gebruikstoepassing waarbij bestaande webservices van Windows Communication Foundation (WCF) en zodat deze veilig toegankelijk toosolutions die zich buiten de bedrijfsperimeter Hallo zonder services Tussenkomende wijzigingen toohello bedrijfsnetwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="f9f34-116">[Azure Relay](https://azure.microsoft.com/services/service-bus/) is designed for hello use-case of taking existing Windows Communication Foundation (WCF) web services and making those services securely accessible toosolutions that reside outside hello corporate perimeter without requiring intrusive changes toohello corporate network infrastructure.</span></span> <span data-ttu-id="f9f34-117">Dergelijke relay-services worden nog steeds gehost binnen hun bestaande omgeving, maar ze dragen het luisteren naar binnenkomende sessies en aanvragen toohello cloud-gebaseerde relay-service.</span><span class="sxs-lookup"><span data-stu-id="f9f34-117">Such relay services are still hosted inside their existing environment, but they delegate listening for incoming sessions and requests toohello cloud-hosted relay service.</span></span> <span data-ttu-id="f9f34-118">Ook beveiligt Azure Relay deze services tegen onbevoegde toegang door [SAS (Shared Access Signature)](../service-bus-messaging/service-bus-sas.md)-verificatie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f9f34-118">Azure Relay also protects those services from unauthorized access by using [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) authentication.</span></span>

## <a name="solution-scenario"></a><span data-ttu-id="f9f34-119">Oplossingsscenario</span><span class="sxs-lookup"><span data-stu-id="f9f34-119">Solution scenario</span></span>
<span data-ttu-id="f9f34-120">In deze zelfstudie maakt u een ASP.NET-website waarmee u een lijst met producten op Hallo inventaris productpagina toosee.</span><span class="sxs-lookup"><span data-stu-id="f9f34-120">In this tutorial, you will create an ASP.NET website that enables you toosee a list of products on hello product inventory page.</span></span>

![][0]

<span data-ttu-id="f9f34-121">Hallo-zelfstudie wordt ervan uitgegaan dat u productgegevens in een bestaande on-premises systeem hebt en maakt gebruik van Azure Relay tooreach dat systeem.</span><span class="sxs-lookup"><span data-stu-id="f9f34-121">hello tutorial assumes that you have product information in an existing on-premises system, and uses Azure Relay tooreach into that system.</span></span> <span data-ttu-id="f9f34-122">Dit wordt gesimuleerd door een webservice die in een eenvoudige consoletoepassing wordt uitgevoerd en wordt ondersteund door een set producten in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-122">This is simulated by a web service that runs in a simple console application and is backed by an in-memory set of products.</span></span> <span data-ttu-id="f9f34-123">U kunt toorun deze consoletoepassing op uw eigen computer en Hallo Webrol in Azure implementeert.</span><span class="sxs-lookup"><span data-stu-id="f9f34-123">You will be able toorun this console application on your own computer and deploy hello web role into Azure.</span></span> <span data-ttu-id="f9f34-124">Doet, ziet u hoe Hallo Webrol uitgevoerd in de Azure-datacenter Hallo inderdaad wordt gebeld op uw computer, ondanks dat de computer bijna zeker achter ten minste één firewall en een network address translation (NAT) laag blijven staan.</span><span class="sxs-lookup"><span data-stu-id="f9f34-124">By doing so, you will see how hello web role running in hello Azure datacenter will indeed call into your computer, even though your computer will almost certainly reside behind at least one firewall and a network address translation (NAT) layer.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="f9f34-125">Hallo-ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="f9f34-125">Set up hello development environment</span></span>

<span data-ttu-id="f9f34-126">Voordat u kunt Azure-toepassingen te ontwikkelen, Hallo-hulpprogramma's downloaden en uw ontwikkelomgeving instellen:</span><span class="sxs-lookup"><span data-stu-id="f9f34-126">Before you can begin developing Azure applications, download hello tools and set up your development environment:</span></span>

1. <span data-ttu-id="f9f34-127">Installeer hello Azure SDK voor .NET via Hallo SDK [pagina downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="f9f34-127">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="f9f34-128">In Hallo **.NET** kolom, klikt u op Hallo-versie van [Visual Studio](http://www.visualstudio.com) u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f9f34-128">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="f9f34-129">Hallo stappen in deze zelfstudie Gebruik Visual Studio 2015, maar ze werken ook met Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f9f34-129">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="f9f34-130">Wanneer u daarom wordt gevraagd toorun of Hallo installatieprogramma opslaat, klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-130">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="f9f34-131">In Hallo **Web Platform Installer**, klikt u op **installeren** te gaan met Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="f9f34-131">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="f9f34-132">Zodra Hallo-installatie voltooid is, hebt u alles wat u nodig toostart toodevelop Hallo app.</span><span class="sxs-lookup"><span data-stu-id="f9f34-132">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="f9f34-133">Hallo SDK bevat hulpprogramma's waarmee u eenvoudig Azure toepassingen ontwikkelen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9f34-133">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="f9f34-134">Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="f9f34-134">Create a namespace</span></span>

<span data-ttu-id="f9f34-135">met behulp van toobegin Hallo relay-functies in Azure, moet u eerst een Servicenaamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="f9f34-135">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="f9f34-136">Een naamruimte biedt een scoping container voor het verwerken van Azure-resources in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="f9f34-136">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="f9f34-137">Ga als volgt Hallo [hier instructies](relay-create-namespace-portal.md) toocreate een Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="f9f34-137">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="create-an-on-premises-server"></a><span data-ttu-id="f9f34-138">Een on-premises server maken</span><span class="sxs-lookup"><span data-stu-id="f9f34-138">Create an on-premises server</span></span>

<span data-ttu-id="f9f34-139">U bouwt eerst een on-premises (model)systeem voor de productcatalogus op.</span><span class="sxs-lookup"><span data-stu-id="f9f34-139">First, you will build a (mock) on-premises product catalog system.</span></span> <span data-ttu-id="f9f34-140">Dit is redelijk eenvoudig; u kunt dit zien als het representeren van een werkelijk on-premises productcatalogussysteem met een volledige serviceoppervlak dat we toointegrate proberen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-140">It will be fairly simple; you can see this as representing an actual on-premises product catalog system with a complete service surface that we're trying toointegrate.</span></span>

<span data-ttu-id="f9f34-141">Dit project is een Visual Studio-consoletoepassing en gebruikt Hallo [Azure Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude Hallo Service Bus-bibliotheken en configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-141">This project is a Visual Studio console application, and uses hello [Azure Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus/) tooinclude hello Service Bus libraries and configuration settings.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="f9f34-142">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="f9f34-142">Create hello project</span></span>

1. <span data-ttu-id="f9f34-143">Start Microsoft Visual Studio met administratorbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="f9f34-143">Using administrator privileges, start Microsoft Visual Studio.</span></span> <span data-ttu-id="f9f34-144">toodo dus programmapictogram Hallo-Visual Studio met de rechtermuisknop op en klik vervolgens op **als administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-144">toodo so, right-click hello Visual Studio program icon, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="f9f34-145">In Visual Studio op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-145">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="f9f34-146">Klik bij **Geïnstalleerde sjablonen**, onder **Visual C#**, op **Consoletoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-146">From **Installed Templates**, under **Visual C#**, click **Console App (.NET Framework)**.</span></span> <span data-ttu-id="f9f34-147">In Hallo **naam** vak, Hallo typenaam **ProductsServer**:</span><span class="sxs-lookup"><span data-stu-id="f9f34-147">In hello **Name** box, type hello name **ProductsServer**:</span></span>

   ![][11]
4. <span data-ttu-id="f9f34-148">Klik op **OK** toocreate hello **ProductsServer** project.</span><span class="sxs-lookup"><span data-stu-id="f9f34-148">Click **OK** toocreate hello **ProductsServer** project.</span></span>
5. <span data-ttu-id="f9f34-149">Als u Hallo NuGet package manager voor Visual Studio al hebt geïnstalleerd, moet u de volgende stap toohello overslaan.</span><span class="sxs-lookup"><span data-stu-id="f9f34-149">If you have already installed hello NuGet package manager for Visual Studio, skip toohello next step.</span></span> <span data-ttu-id="f9f34-150">Anders gaat u naar [NuGet][NuGet] en klikt u op [NuGet installeren](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span><span class="sxs-lookup"><span data-stu-id="f9f34-150">Otherwise, visit [NuGet][NuGet] and click [Install NuGet](http://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c).</span></span> <span data-ttu-id="f9f34-151">Ga als volgt Hallo prompts tooinstall hello NuGet-Pakketbeheer en Visual Studio opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="f9f34-151">Follow hello prompts tooinstall hello NuGet package manager, then re-start Visual Studio.</span></span>
6. <span data-ttu-id="f9f34-152">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsServer** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-152">In Solution Explorer, right-click hello **ProductsServer** project, then click **Manage NuGet Packages**.</span></span>
7. <span data-ttu-id="f9f34-153">Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="f9f34-153">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="f9f34-154">Selecteer Hallo **WindowsAzure.ServiceBus** pakket.</span><span class="sxs-lookup"><span data-stu-id="f9f34-154">Select hello **WindowsAzure.ServiceBus** package.</span></span>
8. <span data-ttu-id="f9f34-155">Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9f34-155">Click **Install**, and accept hello terms of use.</span></span>

   ![][13]

   <span data-ttu-id="f9f34-156">Houd er rekening mee dat Hallo vereiste clientassembly nu wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-156">Note that hello required client assemblies are now referenced.</span></span>
8. <span data-ttu-id="f9f34-157">Voeg een nieuwe klasse voor uw productcontract toe.</span><span class="sxs-lookup"><span data-stu-id="f9f34-157">Add a new class for your product contract.</span></span> <span data-ttu-id="f9f34-158">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsServer** project en klik op **toevoegen**, en klik vervolgens op **klasse**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-158">In Solution Explorer, right-click hello **ProductsServer** project and click **Add**, and then click **Class**.</span></span>
9. <span data-ttu-id="f9f34-159">In Hallo **naam** vak, Hallo typenaam **ProductsContract.cs**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-159">In hello **Name** box, type hello name **ProductsContract.cs**.</span></span> <span data-ttu-id="f9f34-160">Klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-160">Then click **Add**.</span></span>
10. <span data-ttu-id="f9f34-161">In **ProductsContract.cs**, vervang de naamruimtedefinitie Hallo door Hallo volgende code waarmee Hallo contract voor Hallo-service wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-161">In **ProductsContract.cs**, replace hello namespace definition with hello following code, which defines hello contract for hello service.</span></span>

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
11. <span data-ttu-id="f9f34-162">Vervang in Program.cs de naamruimtedefinitie Hallo met de volgende code, die wordt toegevoegd Hallo-Profielservice en Hallo host voor deze Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9f34-162">In Program.cs, replace hello namespace definition with hello following code, which adds hello profile service and hello host for it.</span></span>

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
12. <span data-ttu-id="f9f34-163">Dubbelklik in Solution Explorer op Hallo **App.config** bestand tooopen in Hallo Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="f9f34-163">In Solution Explorer, double-click hello **App.config** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="f9f34-164">Hallo Hallo onderaan in `<system.ServiceModel>` element (maar nog steeds binnen `<system.ServiceModel>`), Hallo volgende XML-code toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-164">At hello bottom of hello `<system.ServiceModel>` element (but still within `<system.ServiceModel>`), add hello following XML code.</span></span> <span data-ttu-id="f9f34-165">Ervoor tooreplace worden *yourServiceNamespace* met de naam van uw naamruimte Hallo en *yourKey* met SAS-sleutel Hallo u eerder hebt opgehaald via de portal Hallo:</span><span class="sxs-lookup"><span data-stu-id="f9f34-165">Be sure tooreplace *yourServiceNamespace* with hello name of your namespace, and *yourKey* with hello SAS key you retrieved earlier from hello portal:</span></span>

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
13. <span data-ttu-id="f9f34-166">Nog steeds in App.config in Hallo `<appSettings>` vervangen Hallo gegevensbronwaarde met verbindingsreeks die u eerder hebt verkregen via de portal Hallo Hallo-element.</span><span class="sxs-lookup"><span data-stu-id="f9f34-166">Still in App.config, in hello `<appSettings>` element, replace hello connection string value with hello connection string you previously obtained from hello portal.</span></span>

    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=yourKey"/>
    </appSettings>
    ```
14. <span data-ttu-id="f9f34-167">Druk op **Ctrl + Shift + B** of van Hallo **bouwen** menu, klikt u op **Build Solution** toobuild toepassing hello en controleer Hallo juistheid van uw werk tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="f9f34-167">Press **Ctrl+Shift+B** or from hello **Build** menu, click **Build Solution** toobuild hello application and verify hello accuracy of your work so far.</span></span>

## <a name="create-an-aspnet-application"></a><span data-ttu-id="f9f34-168">Een ASP.NET-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f9f34-168">Create an ASP.NET application</span></span>

<span data-ttu-id="f9f34-169">In deze sectie bouwt u een eenvoudige ASP.NET-toepassing op waarmee gegevens worden weergegeven die u uit uw productservice hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f9f34-169">In this section you will build a simple ASP.NET application that displays data retrieved from your product service.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="f9f34-170">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="f9f34-170">Create hello project</span></span>

1. <span data-ttu-id="f9f34-171">Zorg ervoor dat Visual Studio met administratorbevoegdheden wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-171">Ensure that Visual Studio is running with administrator privileges.</span></span>
2. <span data-ttu-id="f9f34-172">In Visual Studio op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-172">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="f9f34-173">Klik bij **Geïnstalleerde sjablonen**, onder **Visual C#**, op **ASP.NET-webtoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-173">From **Installed Templates**, under **Visual C#**, click **ASP.NET Web Application (.NET Framework)**.</span></span> <span data-ttu-id="f9f34-174">Naam Hallo project **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-174">Name hello project **ProductsPortal**.</span></span> <span data-ttu-id="f9f34-175">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-175">Then click **OK**.</span></span>

   ![][15]

4. <span data-ttu-id="f9f34-176">Van Hallo **ASP.NET sjablonen** lijst in Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **MVC**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-176">From hello **ASP.NET Templates** list in hello **New ASP.NET Web Application** dialog, click **MVC**.</span></span>

   ![][16]

6. <span data-ttu-id="f9f34-177">Klik op Hallo **verificatie wijzigen** knop.</span><span class="sxs-lookup"><span data-stu-id="f9f34-177">Click hello **Change Authentication** button.</span></span> <span data-ttu-id="f9f34-178">In Hallo **verificatie wijzigen** dialoogvenster vak, zorg ervoor dat **geen verificatie** is geselecteerd en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-178">In hello **Change Authentication** dialog box, ensure that **No Authentication** is selected, and then click **OK**.</span></span> <span data-ttu-id="f9f34-179">In deze zelfstudie implementeert u een app waarvoor geen gebruikersaanmelding nodig is.</span><span class="sxs-lookup"><span data-stu-id="f9f34-179">For this tutorial, you're deploying an app that does not need a user login.</span></span>

    ![][18]

7. <span data-ttu-id="f9f34-180">Terug in Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **OK** toocreate Hallo MVC-app.</span><span class="sxs-lookup"><span data-stu-id="f9f34-180">Back in hello **New ASP.NET Web Application** dialog, click **OK** toocreate hello MVC app.</span></span>
8. <span data-ttu-id="f9f34-181">U moet nu Azure-resources configureren voor een nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="f9f34-181">Now you must configure Azure resources for a new web app.</span></span> <span data-ttu-id="f9f34-182">Volg de stappen Hallo in Hallo [tooAzure sectie van dit artikel publiceren](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f9f34-182">Follow hello steps in hello [Publish tooAzure section of this article](../app-service-web/app-service-web-get-started-dotnet.md).</span></span> <span data-ttu-id="f9f34-183">Vervolgens toothis zelfstudie retourneren en de volgende stap toohello gaan.</span><span class="sxs-lookup"><span data-stu-id="f9f34-183">Then, return toothis tutorial and proceed toohello next step.</span></span>
10. <span data-ttu-id="f9f34-184">Klik in Solution Explorer met de rechtermuisknop op **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-184">In Solution Explorer, right-click **Models** and then click **Add**, then click **Class**.</span></span> <span data-ttu-id="f9f34-185">In Hallo **naam** vak, Hallo typenaam **Product.cs**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-185">In hello **Name** box, type hello name **Product.cs**.</span></span> <span data-ttu-id="f9f34-186">Klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-186">Then click **Add**.</span></span>

    ![][17]

### <a name="modify-hello-web-application"></a><span data-ttu-id="f9f34-187">Hallo-webtoepassing wijzigen</span><span class="sxs-lookup"><span data-stu-id="f9f34-187">Modify hello web application</span></span>

1. <span data-ttu-id="f9f34-188">In Hallo Product.cs bestand in Visual Studio vervangt u de bestaande naamruimtedefinitie Hallo Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-188">In hello Product.cs file in Visual Studio, replace hello existing namespace definition with hello following code.</span></span>

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
2. <span data-ttu-id="f9f34-189">Vouw in Solution Explorer Hallo **domeincontrollers** map, dubbelklikt u vervolgens op Hallo **HomeController.cs** tooopen bestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f9f34-189">In Solution Explorer, expand hello **Controllers** folder, then double-click hello **HomeController.cs** file tooopen it in Visual Studio.</span></span>
3. <span data-ttu-id="f9f34-190">In **HomeController.cs**, de bestaande naamruimtedefinitie Hallo vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-190">In **HomeController.cs**, replace hello existing namespace definition with hello following code.</span></span>

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
4. <span data-ttu-id="f9f34-191">Vouw in Solution Explorer de map Views\Shared Hallo uit en dubbelklik vervolgens **_Layout.cshtml** tooopen in Hallo Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="f9f34-191">In Solution Explorer, expand hello Views\Shared folder, then double-click **_Layout.cshtml** tooopen it in hello Visual Studio editor.</span></span>
5. <span data-ttu-id="f9f34-192">Wijzig alle instanties van **mijn ASP.NET-toepassing** te**producten van LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-192">Change all occurrences of **My ASP.NET Application** too**LITWARE's Products**.</span></span>
6. <span data-ttu-id="f9f34-193">Hallo verwijderen **Start**, **over**, en **Contact** koppelingen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-193">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="f9f34-194">Verwijder in Hallo voorbeeld te volgen, Hallo gemarkeerd code.</span><span class="sxs-lookup"><span data-stu-id="f9f34-194">In hello following example, delete hello highlighted code.</span></span>

    ![][41]

7. <span data-ttu-id="f9f34-195">Vouw in Solution Explorer de map Views\Home Hallo uit en dubbelklik vervolgens **Index.cshtml** tooopen in Hallo Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="f9f34-195">In Solution Explorer, expand hello Views\Home folder, then double-click **Index.cshtml** tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="f9f34-196">Vervang de volledige inhoud van de Hallo van Hallo-bestand met de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9f34-196">Replace hello entire contents of hello file with hello following code.</span></span>

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
8. <span data-ttu-id="f9f34-197">tooverify hello juistheid van uw werk tot nu toe, drukt u op **Ctrl + Shift + B** toobuild Hallo project.</span><span class="sxs-lookup"><span data-stu-id="f9f34-197">tooverify hello accuracy of your work so far, you can press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="run-hello-app-locally"></a><span data-ttu-id="f9f34-198">Hallo-app lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f9f34-198">Run hello app locally</span></span>

<span data-ttu-id="f9f34-199">Hallo toepassing tooverify die hierbij worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-199">Run hello application tooverify that it works.</span></span>

1. <span data-ttu-id="f9f34-200">Zorg ervoor dat **ProductsPortal** Hallo actieve project is.</span><span class="sxs-lookup"><span data-stu-id="f9f34-200">Ensure that **ProductsPortal** is hello active project.</span></span> <span data-ttu-id="f9f34-201">Hallo projectnaam in Solution Explorer met de rechtermuisknop en selecteer **instellen als opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-201">Right-click hello project name in Solution Explorer and select **Set As Startup Project**.</span></span>
2. <span data-ttu-id="f9f34-202">Druk in Visual Studio op **F5**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-202">In Visual Studio, press **F5**.</span></span>
3. <span data-ttu-id="f9f34-203">Uw toepassing moet dan in een browser worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f9f34-203">Your application should appear, running in a browser.</span></span>

   ![][21]

## <a name="put-hello-pieces-together"></a><span data-ttu-id="f9f34-204">Hallo softwareonderdelen samenstellen</span><span class="sxs-lookup"><span data-stu-id="f9f34-204">Put hello pieces together</span></span>

<span data-ttu-id="f9f34-205">de volgende stap Hallo is toohook Hallo lokale producten server Hello ASP.NET-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f9f34-205">hello next step is toohook up hello on-premises products server with hello ASP.NET application.</span></span>

1. <span data-ttu-id="f9f34-206">Als deze nog niet is geopend in Visual Studio opnieuw openen Hallo **ProductsPortal** project dat u hebt gemaakt in Hallo [maken van een ASP.NET-toepassing](#create-an-aspnet-application) sectie.</span><span class="sxs-lookup"><span data-stu-id="f9f34-206">If it is not already open, in Visual Studio re-open hello **ProductsPortal** project you created in hello [Create an ASP.NET application](#create-an-aspnet-application) section.</span></span>
2. <span data-ttu-id="f9f34-207">Vergelijkbare toohello stap in de sectie 'Een On-Premises Server maken' hello toevoegen toohello projectverwijzingen voor Hallo NuGet-pakket.</span><span class="sxs-lookup"><span data-stu-id="f9f34-207">Similar toohello step in hello "Create an On-Premises Server" section, add hello NuGet package toohello project references.</span></span> <span data-ttu-id="f9f34-208">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-208">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="f9f34-209">Zoek naar 'Service Bus' en selecteer Hallo **WindowsAzure.ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="f9f34-209">Search for "Service Bus" and select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="f9f34-210">Vervolgens Hallo installatie voltooien en sluit het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9f34-210">Then complete hello installation and close this dialog box.</span></span>
4. <span data-ttu-id="f9f34-211">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** project en klik vervolgens op **toevoegen**, klikt u vervolgens **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-211">In Solution Explorer, right-click hello **ProductsPortal** project, then click **Add**, then **Existing Item**.</span></span>
5. <span data-ttu-id="f9f34-212">Navigeer toohello **ProductsContract.cs** bestand van Hallo **ProductsServer** console-project.</span><span class="sxs-lookup"><span data-stu-id="f9f34-212">Navigate toohello **ProductsContract.cs** file from hello **ProductsServer** console project.</span></span> <span data-ttu-id="f9f34-213">Klik op toohighlight ProductsContract.cs.</span><span class="sxs-lookup"><span data-stu-id="f9f34-213">Click toohighlight ProductsContract.cs.</span></span> <span data-ttu-id="f9f34-214">Klik op Hallo pijl-omlaag naast te**toevoegen**, klikt u vervolgens op **toevoegen als koppeling**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-214">Click hello down arrow next too**Add**, then click **Add as Link**.</span></span>

   ![][24]

6. <span data-ttu-id="f9f34-215">Open nu Hallo **HomeController.cs** -bestand in Visual Studio-editor Hallo en vervang de naamruimtedefinitie Hallo door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-215">Now open hello **HomeController.cs** file in hello Visual Studio editor and replace hello namespace definition with hello following code.</span></span> <span data-ttu-id="f9f34-216">Ervoor tooreplace worden *yourServiceNamespace* met Hallo-naam van uw Servicenaamruimte en *yourKey* met SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="f9f34-216">Be sure tooreplace *yourServiceNamespace* with hello name of your service namespace, and *yourKey* with your SAS key.</span></span> <span data-ttu-id="f9f34-217">Hiermee schakelt u Hallo toocall Hallo lokale clientservice, Hallo resultaat van Hallo aanroep retourneren.</span><span class="sxs-lookup"><span data-stu-id="f9f34-217">This will enable hello client toocall hello on-premises service, returning hello result of hello call.</span></span>

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
7. <span data-ttu-id="f9f34-218">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** oplossing (Zorg ervoor dat tooright en klik op Hallo oplossing, niet Hallo project).</span><span class="sxs-lookup"><span data-stu-id="f9f34-218">In Solution Explorer, right-click hello **ProductsPortal** solution (make sure tooright-click hello solution, not hello project).</span></span> <span data-ttu-id="f9f34-219">Klik op **Toevoegen** en vervolgens op **Bestaand project**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-219">Click **Add**, then click **Existing Project**.</span></span>
8. <span data-ttu-id="f9f34-220">Navigeer toohello **ProductsServer** project en dubbelklik op Hallo **ProductsServer.csproj** oplossing bestand tooadd deze.</span><span class="sxs-lookup"><span data-stu-id="f9f34-220">Navigate toohello **ProductsServer** project, then double-click hello **ProductsServer.csproj** solution file tooadd it.</span></span>
9. <span data-ttu-id="f9f34-221">**ProductsServer** in volgorde toodisplay Hallo gegevens moet worden uitgevoerd op **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-221">**ProductsServer** must be running in order toodisplay hello data on **ProductsPortal**.</span></span> <span data-ttu-id="f9f34-222">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** oplossing en op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-222">In Solution Explorer, right-click hello **ProductsPortal** solution and click **Properties**.</span></span> <span data-ttu-id="f9f34-223">Hallo **eigenschappenvensters** in het dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f9f34-223">hello **Property Pages** dialog box is displayed.</span></span>
10. <span data-ttu-id="f9f34-224">Klik op Hallo linkerkant, **opstartproject**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-224">On hello left side, click **Startup Project**.</span></span> <span data-ttu-id="f9f34-225">Klik op aan de rechterkant hello, **meerdere opstartprojecten**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-225">On hello right side, click **Multiple startup projects**.</span></span> <span data-ttu-id="f9f34-226">Zorg ervoor dat **ProductsServer** en **ProductsPortal** worden weergegeven in de juiste volgorde, waarbij **Start** ingesteld als Hallo-actie voor beide.</span><span class="sxs-lookup"><span data-stu-id="f9f34-226">Ensure that **ProductsServer** and **ProductsPortal** appear, in that order, with **Start** set as hello action for both.</span></span>

      ![][25]

11. <span data-ttu-id="f9f34-227">Nog steeds in Hallo **eigenschappen** in het dialoogvenster, klikt u op **Projectafhankelijkheden** op Hallo linkerkant.</span><span class="sxs-lookup"><span data-stu-id="f9f34-227">Still in hello **Properties** dialog box, click **Project Dependencies** on hello left side.</span></span>
12. <span data-ttu-id="f9f34-228">In Hallo **projecten** lijst, klikt u op **ProductsServer**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-228">In hello **Projects** list, click **ProductsServer**.</span></span> <span data-ttu-id="f9f34-229">Zorg ervoor dat **ProductsPortal** niet is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-229">Ensure that **ProductsPortal** is not selected.</span></span>
13. <span data-ttu-id="f9f34-230">In Hallo **projecten** lijst, klikt u op **ProductsPortal**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-230">In hello **Projects** list, click **ProductsPortal**.</span></span> <span data-ttu-id="f9f34-231">Zorg ervoor dat **ProductsServer** is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-231">Ensure that **ProductsServer** is selected.</span></span>

    ![][26]

14. <span data-ttu-id="f9f34-232">Klik op **OK** in Hallo **eigenschappenvensters** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="f9f34-232">Click **OK** in hello **Property Pages** dialog box.</span></span>

## <a name="run-hello-project-locally"></a><span data-ttu-id="f9f34-233">Hallo-project lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f9f34-233">Run hello project locally</span></span>

<span data-ttu-id="f9f34-234">tootest hello toepassing lokaal door in Visual Studio druk op **F5**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-234">tootest hello application locally, in Visual Studio press **F5**.</span></span> <span data-ttu-id="f9f34-235">Hallo on-premises-server (**ProductsServer**) moet eerst worden gestart en vervolgens Hallo **ProductsPortal** toepassing worden gestart in een browservenster.</span><span class="sxs-lookup"><span data-stu-id="f9f34-235">hello on-premises server (**ProductsServer**) should start first, then hello **ProductsPortal** application should start in a browser window.</span></span> <span data-ttu-id="f9f34-236">Deze tijd ziet u dat Hallo-productinventaris bevat gegevens die uit Hallo product service on-premises systeem opgehaald.</span><span class="sxs-lookup"><span data-stu-id="f9f34-236">This time, you will see that hello product inventory lists data retrieved from hello product service on-premises system.</span></span>

![][10]

<span data-ttu-id="f9f34-237">Druk op **vernieuwen** op Hallo **ProductsPortal** pagina.</span><span class="sxs-lookup"><span data-stu-id="f9f34-237">Press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="f9f34-238">Elke keer dat u Hallo pagina vernieuwt, ziet u Hallo server app een bericht weergegeven wanneer `GetProducts()` van **ProductsServer** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-238">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

<span data-ttu-id="f9f34-239">Sluit beide toepassingen voordat u doorgaat toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="f9f34-239">Close both applications before proceeding toohello next step.</span></span>

## <a name="deploy-hello-productsportal-project-tooan-azure-web-app"></a><span data-ttu-id="f9f34-240">Hallo ProductsPortal project tooan Azure-web-app implementeren</span><span class="sxs-lookup"><span data-stu-id="f9f34-240">Deploy hello ProductsPortal project tooan Azure web app</span></span>

<span data-ttu-id="f9f34-241">de volgende stap Hallo is toorepublish hello Azure-Web-app **ProductsPortal** frontend.</span><span class="sxs-lookup"><span data-stu-id="f9f34-241">hello next step is toorepublish hello Azure Web app **ProductsPortal** frontend.</span></span> <span data-ttu-id="f9f34-242">Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="f9f34-242">Do hello following:</span></span>

1. <span data-ttu-id="f9f34-243">Klik in Solution Explorer met de rechtermuisknop op Hallo **ProductsPortal** project en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-243">In Solution Explorer, right-click hello **ProductsPortal** project, and click **Publish**.</span></span> <span data-ttu-id="f9f34-244">Klik vervolgens op **publiceren** op Hallo **publiceren** pagina.</span><span class="sxs-lookup"><span data-stu-id="f9f34-244">Then, click **Publish** on hello **Publish** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="f9f34-245">Wordt er een foutbericht weergegeven in het browservenster Hallo wanneer hello **ProductsPortal** -webproject automatisch wordt gestart na het Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="f9f34-245">You may see an error message in hello browser window when hello **ProductsPortal** web project is automatically launched after hello deployment.</span></span> <span data-ttu-id="f9f34-246">Dit is normaal en doet zich voor omdat Hallo **ProductsServer** toepassing nog niet wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-246">This is expected, and occurs because hello **ProductsServer** application isn't running yet.</span></span>
>
>

2. <span data-ttu-id="f9f34-247">URL van de kopie Hallo Hallo geïmplementeerd web-app naar wens Hallo-URL in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="f9f34-247">Copy hello URL of hello deployed web app, as you will need hello URL in hello next step.</span></span> <span data-ttu-id="f9f34-248">U kunt ook deze URL ophalen via hello Azure App Service-activiteit venster in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="f9f34-248">You can also obtain this URL from hello Azure App Service Activity window in Visual Studio:</span></span>

  ![][9]

3. <span data-ttu-id="f9f34-249">Sluit Hallo browser venster toostop Hallo toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f9f34-249">Close hello browser window toostop hello running application.</span></span>

### <a name="set-productsportal-as-web-app"></a><span data-ttu-id="f9f34-250">ProductsPortal instellen als web-app</span><span class="sxs-lookup"><span data-stu-id="f9f34-250">Set ProductsPortal as web app</span></span>

<span data-ttu-id="f9f34-251">Voordat u actieve Hallo-toepassing in de cloud hello, moet u ervoor zorgen dat **ProductsPortal** vanuit Visual Studio als een web-app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f9f34-251">Before running hello application in hello cloud, you must ensure that **ProductsPortal** is launched from within Visual Studio as a web app.</span></span>

1. <span data-ttu-id="f9f34-252">In Visual Studio met de rechtermuisknop op Hallo **ProductsPortal** project en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-252">In Visual Studio, right-click hello **ProductsPortal** project and then click **Properties**.</span></span>
2. <span data-ttu-id="f9f34-253">Klik in de linkerkolom hello, **Web**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-253">In hello left-hand column, click **Web**.</span></span>
3. <span data-ttu-id="f9f34-254">In Hallo **actie starten** sectie, klikt u op Hallo **Start-URL** knop, en in het tekstvak Hallo Hallo URL voor uw eerder geïmplementeerde web-app bijvoorbeeld `http://productsportal1234567890.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="f9f34-254">In hello **Start Action** section, click hello **Start URL** button, and in hello text box enter hello URL for your previously deployed web app; for example, `http://productsportal1234567890.azurewebsites.net/`.</span></span>

    ![][27]

4. <span data-ttu-id="f9f34-255">Van Hallo **bestand** menu in Visual Studio, klikt u op **Alles opslaan**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-255">From hello **File** menu in Visual Studio, click **Save All**.</span></span>
5. <span data-ttu-id="f9f34-256">In menu van Hallo bouwen in Visual Studio, klikt u op **oplossing opnieuw opbouwen**.</span><span class="sxs-lookup"><span data-stu-id="f9f34-256">From hello Build menu in Visual Studio, click **Rebuild Solution**.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="f9f34-257">Hallo-toepassing uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f9f34-257">Run hello application</span></span>

1. <span data-ttu-id="f9f34-258">Druk op F5 toobuild en Voer Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f9f34-258">Press F5 toobuild and run hello application.</span></span> <span data-ttu-id="f9f34-259">Hallo on-premises-server (Hallo **ProductsServer** consoletoepassing) moet eerst worden gestart en vervolgens Hallo **ProductsPortal** toepassing worden gestart in een browservenster wordt weergegeven in het volgende scherm Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-259">hello on-premises server (hello **ProductsServer** console application) should start first, then hello **ProductsPortal** application should start in a browser window, as shown in hello following screen shot.</span></span> <span data-ttu-id="f9f34-260">U ziet opnieuw die productinventaris Hallo ziet u de gegevens uit de Hallo product service on-premises systeem en geeft die gegevens op Hallo web-app.</span><span class="sxs-lookup"><span data-stu-id="f9f34-260">Notice again that hello product inventory lists data retrieved from hello product service on-premises system, and displays that data in hello web app.</span></span> <span data-ttu-id="f9f34-261">Controleer Hallo URL toomake ervoor dat **ProductsPortal** wordt uitgevoerd in de cloud hello, als een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="f9f34-261">Check hello URL toomake sure that **ProductsPortal** is running in hello cloud, as an Azure web app.</span></span>

   ![][1]

   > [!IMPORTANT]
   > <span data-ttu-id="f9f34-262">Hallo **ProductsServer** consoletoepassing moet worden uitgevoerd en kunnen tooserve Hallo gegevens toohello **ProductsPortal** toepassing.</span><span class="sxs-lookup"><span data-stu-id="f9f34-262">hello **ProductsServer** console application must be running and able tooserve hello data toohello **ProductsPortal** application.</span></span> <span data-ttu-id="f9f34-263">Als Hallo browser is een fout weergegeven, wacht u enkele seconden voor **ProductsServer** tooload en weergave hello te volgen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-263">If hello browser displays an error, wait a few more seconds for **ProductsServer** tooload and display hello following message.</span></span> <span data-ttu-id="f9f34-264">Druk op **vernieuwen** in Hallo browser.</span><span class="sxs-lookup"><span data-stu-id="f9f34-264">Then press **Refresh** in hello browser.</span></span>
   >
   >

   ![][37]
2. <span data-ttu-id="f9f34-265">Terug in de browser hello, drukt u op **vernieuwen** op Hallo **ProductsPortal** pagina.</span><span class="sxs-lookup"><span data-stu-id="f9f34-265">Back in hello browser, press **Refresh** on hello **ProductsPortal** page.</span></span> <span data-ttu-id="f9f34-266">Elke keer dat u Hallo pagina vernieuwt, ziet u Hallo server app een bericht weergegeven wanneer `GetProducts()` van **ProductsServer** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f9f34-266">Each time you refresh hello page, you'll see hello server app display a message when `GetProducts()` from **ProductsServer** is called.</span></span>

    ![][38]

## <a name="next-steps"></a><span data-ttu-id="f9f34-267">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f9f34-267">Next steps</span></span>

<span data-ttu-id="f9f34-268">toolearn meer informatie over Azure-Relay, Zie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f9f34-268">toolearn more about Azure Relay, see hello following resources:</span></span>  

* [<span data-ttu-id="f9f34-269">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="f9f34-269">What is Azure Relay?</span></span>](relay-what-is-it.md)  
* [<span data-ttu-id="f9f34-270">Hoe Relay-toouse</span><span class="sxs-lookup"><span data-stu-id="f9f34-270">How toouse Relay</span></span>](service-bus-dotnet-how-to-use-relay.md)  

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

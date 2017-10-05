---
title: Aan de slag met Azure Relay WCF doorstuurt in .NET | Microsoft Docs
description: Informatie over hoe u met Azure Relay WCF relays verbinding maken met twee toepassingen die worden gehost op verschillende locaties.
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 5493281a-c2e5-49f2-87ee-9d3ffb782c75
ms.service: service-bus-relay
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: sethm
ms.openlocfilehash: 1af1ac78398d65e6a87f0d24d6198f3dfbc82ffd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="b7571-103">Het gebruik van Azure Relay WCF doorstuurt met .NET</span><span class="sxs-lookup"><span data-stu-id="b7571-103">How to use Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="b7571-104">In dit artikel wordt beschreven hoe u de Azure-Relay-service.</span><span class="sxs-lookup"><span data-stu-id="b7571-104">This article describes how to use the Azure Relay service.</span></span> <span data-ttu-id="b7571-105">De voorbeelden zijn geschreven in C# en maken gebruik van de WCF-API (Windows Communication Foundation) met extensies die deel uitmaken van de Service Bus-assembly.</span><span class="sxs-lookup"><span data-stu-id="b7571-105">The samples are written in C# and use the Windows Communication Foundation (WCF) API with extensions contained in the Service Bus assembly.</span></span> <span data-ttu-id="b7571-106">Zie voor meer informatie over Azure relay, de [Azure Relay overzicht](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="b7571-106">For more information about Azure relay, see the [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="b7571-107">Wat is de Relay WCF?</span><span class="sxs-lookup"><span data-stu-id="b7571-107">What is WCF Relay?</span></span>

<span data-ttu-id="b7571-108">De Azure [ *WCF Relay* ](relay-what-is-it.md) service kunt u hybride toepassingen opbouwen die worden uitgevoerd in een Azure-datacenter en uw eigen on-premises bedrijfsomgeving.</span><span class="sxs-lookup"><span data-stu-id="b7571-108">The Azure [*WCF Relay*](relay-what-is-it.md) service enables you to build hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="b7571-109">De relay-service dit is mogelijk doordat u veilig kunt blootstellen Windows Communication Foundation (WCF)-services die zich in een bedrijfsnetwerk naar de openbare cloud bevinden zonder dat een firewallverbinding openen of een vereiste hoog wijzigingen in de infrastructuur van een bedrijfsnetwerk.</span><span class="sxs-lookup"><span data-stu-id="b7571-109">The relay service facilitates this by enabling you to securely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network to the public cloud, without having to open a firewall connection, or requiring intrusive changes to a corporate network infrastructure.</span></span>

![WCF Relay-concepten](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="b7571-111">Azure Relay kunt u de WCF-hostservices in uw bestaande bedrijfsomgeving.</span><span class="sxs-lookup"><span data-stu-id="b7571-111">Azure Relay enables you to host WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="b7571-112">U kunt overdragen luisteren naar binnenkomende sessies en aanvragen voor deze WCF-services naar de relay-service actief is in Azure.</span><span class="sxs-lookup"><span data-stu-id="b7571-112">You can then delegate listening for incoming sessions and requests to these WCF services to the relay service running within Azure.</span></span> <span data-ttu-id="b7571-113">Hierdoor kunt u deze services beschikbaar stellen voor toepassingscode die wordt uitgevoerd in Azure of voor mobiele werknemers of extranetpartneromgevingen.</span><span class="sxs-lookup"><span data-stu-id="b7571-113">This enables you to expose these services to application code running in Azure, or to mobile workers or extranet partner environments.</span></span> <span data-ttu-id="b7571-114">Relay kunt u veilig bepalen wie toegang deze services heel nauwkeurig tot.</span><span class="sxs-lookup"><span data-stu-id="b7571-114">Relay enables you to securely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="b7571-115">Service Bus biedt een krachtige en veilige manier om toepassingsfuncties en -gegevens van uw bestaande bedrijfsoplossingen beschikbaar te maken en hiervan te profiteren vanuit de cloud.</span><span class="sxs-lookup"><span data-stu-id="b7571-115">It provides a powerful and secure way to expose application functionality and data from your existing enterprise solutions and take advantage of it from the cloud.</span></span>

<span data-ttu-id="b7571-116">In dit artikel wordt beschreven hoe Azure Relay gebruiken voor het maken van een WCF-webservice weergegeven met behulp van een TCP-kanaal binding, waarmee een beveiligde communicatie tussen twee partijen wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b7571-116">This article discusses how to use Azure Relay to create a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-the-service-bus-nuget-package"></a><span data-ttu-id="b7571-117">Het Service Bus NuGet-pakket ophalen</span><span class="sxs-lookup"><span data-stu-id="b7571-117">Get the Service Bus NuGet package</span></span>
<span data-ttu-id="b7571-118">Het [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is de eenvoudigste manier om de Service Bus-API op te halen en om de toepassing te configureren met alle Service Bus-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="b7571-118">The [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is the easiest way to get the Service Bus API and to configure your application with all of the Service Bus dependencies.</span></span> <span data-ttu-id="b7571-119">Ga als volgt te werk om het NuGet-pakket in uw project te installeren:</span><span class="sxs-lookup"><span data-stu-id="b7571-119">To install the NuGet package in your project, do the following:</span></span>

1. <span data-ttu-id="b7571-120">Klik in Solution Explorer met de rechtermuisknop op **Verwijzingen** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="b7571-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="b7571-121">Zoek ‘Service Bus’ en selecteer het item **Microsoft Azure Service Bus**.</span><span class="sxs-lookup"><span data-stu-id="b7571-121">Search for "Service Bus" and select the **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="b7571-122">Klik op **Installeren** om de installatie te voltooien en sluit het volgende dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="b7571-122">Click **Install** to complete the installation, then close the following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="b7571-123">Weergeven en gebruiken van een SOAP-webservice met TCP</span><span class="sxs-lookup"><span data-stu-id="b7571-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="b7571-124">Als u een bestaande WCF SOAP-webservice voor extern verbruik beschikbaar wilt maken, moet u wijzigingen aanbrengen aan de servicebindingen en -adressen.</span><span class="sxs-lookup"><span data-stu-id="b7571-124">To expose an existing WCF SOAP web service for external consumption, you must make changes to the service bindings and addresses.</span></span> <span data-ttu-id="b7571-125">Hiervoor zijn mogelijk wijzigingen aan uw configuratiebestand of codewijzigingen nodig, afhankelijk van hoe u de WCF-services hebt ingesteld en geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="b7571-125">This may require changes to your configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="b7571-126">Houd er rekening mee dat WCF u meerdere netwerkeindpunten via dezelfde service hebben kunt, zodat u de bestaande interne eindpunten behouden kunt bij het toevoegen van de relay-eindpunten voor externe toegang op hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="b7571-126">Note that WCF allows you to have multiple network endpoints over the same service, so you can retain the existing internal endpoints while adding relay endpoints for external access at the same time.</span></span>

<span data-ttu-id="b7571-127">In deze taak bouwen van een eenvoudige WCF-service en een relay-listener aan toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="b7571-127">In this task, you build a simple WCF service and add a relay listener to it.</span></span> <span data-ttu-id="b7571-128">Bij deze oefening wordt ervan uitgegaan dat u enigszins bekend bent met Visual Studio. Daarom wordt het maken van een project niet in detail behandeld.</span><span class="sxs-lookup"><span data-stu-id="b7571-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all the details of creating a project.</span></span> <span data-ttu-id="b7571-129">In plaats daarvan ligt de nadruk op de code.</span><span class="sxs-lookup"><span data-stu-id="b7571-129">Instead, it focuses on the code.</span></span>

<span data-ttu-id="b7571-130">Voordat u met deze stappen begint, voert u de volgende procedure uit om uw omgeving in te stellen:</span><span class="sxs-lookup"><span data-stu-id="b7571-130">Before starting these steps, complete the following procedure to set up your environment:</span></span>

1. <span data-ttu-id="b7571-131">Maak in Visual Studio een consoletoepassing die twee projecten, Client en Service, binnen de oplossing bevat.</span><span class="sxs-lookup"><span data-stu-id="b7571-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within the solution.</span></span>
2. <span data-ttu-id="b7571-132">De Service Bus NuGet-pakket aan beide projecten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b7571-132">Add the Service Bus NuGet package to both projects.</span></span> <span data-ttu-id="b7571-133">Met dit pakket voegt u alle benodigde assemblyverwijzingen aan uw projecten toe.</span><span class="sxs-lookup"><span data-stu-id="b7571-133">This package adds all the necessary assembly references to your projects.</span></span>

### <a name="how-to-create-the-service"></a><span data-ttu-id="b7571-134">De service maken</span><span class="sxs-lookup"><span data-stu-id="b7571-134">How to create the service</span></span>
<span data-ttu-id="b7571-135">Maak eerst de service zelf.</span><span class="sxs-lookup"><span data-stu-id="b7571-135">First, create the service itself.</span></span> <span data-ttu-id="b7571-136">Een WCF-service bestaat uit ten minste drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="b7571-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="b7571-137">Definitie van een contract waarmee wordt beschreven welke berichten worden uitgewisseld en welke bewerkingen moeten worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="b7571-137">Definition of a contract that describes what messages are exchanged and what operations are to be invoked.</span></span>
* <span data-ttu-id="b7571-138">Implementatie van deze overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="b7571-138">Implementation of that contract.</span></span>
* <span data-ttu-id="b7571-139">Host voor de WCF-service waarop een aantal eindpunten beschikbaar wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7571-139">Host that hosts the WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="b7571-140">De codevoorbeelden in deze sectie hebben betrekking op elk van deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="b7571-140">The code examples in this section address each of these components.</span></span>

<span data-ttu-id="b7571-141">Met het contract wordt één bewerking, `AddNumbers`, gedefinieerd waarmee twee getallen worden opgeteld en het resultaat wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b7571-141">The contract defines a single operation, `AddNumbers`, that adds two numbers and returns the result.</span></span> <span data-ttu-id="b7571-142">De client kan met de `IProblemSolverChannel`-interface eenvoudig de levensduur van de proxy beheren.</span><span class="sxs-lookup"><span data-stu-id="b7571-142">The `IProblemSolverChannel` interface enables the client to more easily manage the proxy lifetime.</span></span> <span data-ttu-id="b7571-143">Het wordt aanbevolen een dergelijke interface te maken.</span><span class="sxs-lookup"><span data-stu-id="b7571-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="b7571-144">U kunt deze contractdefinitie het beste in een afzonderlijk bestand plaatsen zodat u naar dat bestand kunt verwijzen vanuit zowel het project Client als het project Service, maar u kunt de code ook naar beide projecten kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b7571-144">It's a good idea to put this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy the code into both projects.</span></span>

```csharp
using System.ServiceModel;

[ServiceContract(Namespace = "urn:ps")]
interface IProblemSolver
{
    [OperationContract]
    int AddNumbers(int a, int b);
}

interface IProblemSolverChannel : IProblemSolver, IClientChannel {}
```

<span data-ttu-id="b7571-145">Met het contract is de implementatie als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="b7571-145">With the contract in place, the implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="b7571-146">Een servicehost via een programma configureren</span><span class="sxs-lookup"><span data-stu-id="b7571-146">Configure a service host programmatically</span></span>
<span data-ttu-id="b7571-147">Met het geïmplementeerde contract kunt u nu de service hosten.</span><span class="sxs-lookup"><span data-stu-id="b7571-147">With the contract and implementation in place, you can now host the service.</span></span> <span data-ttu-id="b7571-148">Hosting vindt plaats in een [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx)-object waarmee exemplaren van de service worden beheerd en dat als host fungeert voor de eindpunten die naar berichten luisteren.</span><span class="sxs-lookup"><span data-stu-id="b7571-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of the service and hosts the endpoints that listen for messages.</span></span> <span data-ttu-id="b7571-149">De volgende code configureert de service met zowel een regulier lokaal eindpunt als een relay-eindpunt ter illustratie van de weergave, naast elkaar van interne en externe eindpunten.</span><span class="sxs-lookup"><span data-stu-id="b7571-149">The following code configures the service with both a regular local endpoint and a relay endpoint to illustrate the appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="b7571-150">Vervang de tekenreeks *namespace* door de naamruimtenaam en *yourKey* door de SAS-sleutel die u in de vorige instellingsstap hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="b7571-150">Replace the string *namespace* with your namespace name and *yourKey* with the SAS key that you obtained in the previous setup step.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));

sh.AddServiceEndpoint(
   typeof (IProblemSolver), new NetTcpBinding(),
   "net.tcp://localhost:9358/solver");

sh.AddServiceEndpoint(
   typeof(IProblemSolver), new NetTcpRelayBinding(),
   ServiceBusEnvironment.CreateServiceUri("sb", "namespace", "solver"))
    .Behaviors.Add(new TransportClientEndpointBehavior {
          TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", "<yourKey>")});

sh.Open();

Console.WriteLine("Press ENTER to close");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="b7571-151">In het voorbeeld maakt u twee eindpunten die deel uitmaken van dezelfde contractimplementatie.</span><span class="sxs-lookup"><span data-stu-id="b7571-151">In the example, you create two endpoints that are on the same contract implementation.</span></span> <span data-ttu-id="b7571-152">Een lokale is en een eindpunt is geprojecteerd via Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="b7571-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="b7571-153">De belangrijkste verschillen tussen deze twee zijn de bindingen; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) voor het lokale eindpunt en [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) voor de relay-eindpunt en de adressen.</span><span class="sxs-lookup"><span data-stu-id="b7571-153">The key differences between them are the bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for the local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for the relay endpoint and the addresses.</span></span> <span data-ttu-id="b7571-154">Het lokale eindpunt heeft een lokaal netwerkadres met een afzonderlijke poort.</span><span class="sxs-lookup"><span data-stu-id="b7571-154">The local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="b7571-155">De relay-eindpunt heeft een eindpuntadres dat bestaat uit de tekenreeks `sb`, uw naamruimtenaam en het pad 'Solver '.'</span><span class="sxs-lookup"><span data-stu-id="b7571-155">The relay endpoint has an endpoint address composed of the string `sb`, your namespace name, and the path "solver."</span></span> <span data-ttu-id="b7571-156">Dit resulteert in de URI `sb://[serviceNamespace].servicebus.windows.net/solver`, het identificeren van het service-eindpunt als een Service Bus (relais) TCP-eindpunt met een volledig gekwalificeerde externe DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="b7571-156">This results in the URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying the service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="b7571-157">Als u de code in de `Main`-functie van de **Service**-toepassing plaatst en de tijdelijke aanduidingen vervangt, hebt u een functionele service.</span><span class="sxs-lookup"><span data-stu-id="b7571-157">If you place the code replacing the placeholders into the `Main` function of the **Service** application, you will have a functional service.</span></span> <span data-ttu-id="b7571-158">Als u wilt dat uw service uitsluitend op de relay luisteren, verwijdert u de declaratie van het lokale eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b7571-158">If you want your service to listen exclusively on the relay, remove the local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-the-appconfig-file"></a><span data-ttu-id="b7571-159">Een servicehost configureren in het bestand App.config</span><span class="sxs-lookup"><span data-stu-id="b7571-159">Configure a service host in the App.config file</span></span>
<span data-ttu-id="b7571-160">U kunt de host ook configureren met het bestand App.config.</span><span class="sxs-lookup"><span data-stu-id="b7571-160">You can also configure the host using the App.config file.</span></span> <span data-ttu-id="b7571-161">De servicehostingcode in dit geval wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b7571-161">The service hosting code in this case appears in the next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER to close");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="b7571-162">De eindpuntdefinities worden verplaatst naar het bestand App.config.</span><span class="sxs-lookup"><span data-stu-id="b7571-162">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="b7571-163">Het NuGet-pakket heeft al een reeks definities aan het App.config-bestand, dat de vereiste configuratie-extensies voor Azure Relay zijn toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b7571-163">The NuGet package has already added a range of definitions to the App.config file, which are the required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="b7571-164">Het volgende voorbeeld, dat het exacte equivalent van de vorige code is, moet direct onder het **system.serviceModel**-element worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b7571-164">The following example, which is the exact equivalent of the previous code, should appear directly beneath the **system.serviceModel** element.</span></span> <span data-ttu-id="b7571-165">In dit voorbeeld wordt ervan uitgegaan dat uw project C#-naamruimte de naam **Service** heeft.</span><span class="sxs-lookup"><span data-stu-id="b7571-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="b7571-166">Vervang de tijdelijke aanduidingen door de naam van de relay-naamruimte en SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="b7571-166">Replace the placeholders with your relay namespace name and SAS key.</span></span>

```xml
<services>
    <service name="Service.ProblemSolver">
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpBinding"
                  address="net.tcp://localhost:9358/solver"/>
        <endpoint contract="Service.IProblemSolver"
                  binding="netTcpRelayBinding"
                  address="sb://<namespaceName>.servicebus.windows.net/solver"
                  behaviorConfiguration="sbTokenProvider"/>
    </service>
</services>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

<span data-ttu-id="b7571-167">Nadat u deze wijzigingen hebt aangebracht, start de service als voorheen maar met twee live eindpunten: een lokaal eindpunt en een eindpunt waarmee in de cloud wordt geluisterd.</span><span class="sxs-lookup"><span data-stu-id="b7571-167">After you make these changes, the service starts as it did before, but with two live endpoints: one local and one listening in the cloud.</span></span>

### <a name="create-the-client"></a><span data-ttu-id="b7571-168">De client maken</span><span class="sxs-lookup"><span data-stu-id="b7571-168">Create the client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="b7571-169">Een client via een programma configureren</span><span class="sxs-lookup"><span data-stu-id="b7571-169">Configure a client programmatically</span></span>
<span data-ttu-id="b7571-170">U kunt voor het verbruik van de service een WCF-client maken met een [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx)-object.</span><span class="sxs-lookup"><span data-stu-id="b7571-170">To consume the service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="b7571-171">Service Bus maakt gebruik van een beveiligingsmodel op basis van tokens dat wordt geïmplementeerd met SAS.</span><span class="sxs-lookup"><span data-stu-id="b7571-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="b7571-172">De klasse [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) vertegenwoordigt een beveiligingstokenprovider met ingebouwde factorymethoden waarmee een aantal bekende tokenproviders wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b7571-172">The [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="b7571-173">In het volgende voorbeeld wordt de methode [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) gebruikt voor het verwerken van het ophalen van het juiste SAS-token.</span><span class="sxs-lookup"><span data-stu-id="b7571-173">The following example uses the [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method to handle the acquisition of the appropriate SAS token.</span></span> <span data-ttu-id="b7571-174">De naam en de sleutel zijn verkregen via de portal, zoals beschreven in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="b7571-174">The name and key are those obtained from the portal as described in the previous section.</span></span>

<span data-ttu-id="b7571-175">Verwijs eerst naar de `IProblemSolver`-contractcode van de service in uw clientproject of kopieer deze.</span><span class="sxs-lookup"><span data-stu-id="b7571-175">First, reference or copy the `IProblemSolver` contract code from the service into your client project.</span></span>

<span data-ttu-id="b7571-176">Vervang vervolgens de code in de `Main` methode van de client, Vervang ook de tijdelijke aanduiding voor tekst met de relay-naamruimte en SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="b7571-176">Then, replace the code in the `Main` method of the client, again replacing the placeholder text with your relay namespace and SAS key.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>(
    new NetTcpRelayBinding(),
    new EndpointAddress(ServiceBusEnvironment.CreateServiceUri("sb", "<namespaceName>", "solver")));

cf.Endpoint.Behaviors.Add(new TransportClientEndpointBehavior
            { TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey","<yourKey>") });

using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="b7571-177">U kunt de client en de service nu opbouwen en uitvoeren (voer de service eerst uit). De client roept de service aan en drukt **9** af.</span><span class="sxs-lookup"><span data-stu-id="b7571-177">You can now build the client and the service, run them (run the service first), and the client calls the service and prints **9**.</span></span> <span data-ttu-id="b7571-178">U kunt de client en server op verschillende computers uitvoeren, zelfs in netwerken. De communicatie zal dan nog steeds goed verlopen.</span><span class="sxs-lookup"><span data-stu-id="b7571-178">You can run the client and server on different machines, even across networks, and the communication will still work.</span></span> <span data-ttu-id="b7571-179">De clientcode kan in de cloud of lokaal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b7571-179">The client code can also run in the cloud or locally.</span></span>

#### <a name="configure-a-client-in-the-appconfig-file"></a><span data-ttu-id="b7571-180">Een client configureren in het bestand App.config</span><span class="sxs-lookup"><span data-stu-id="b7571-180">Configure a client in the App.config file</span></span>
<span data-ttu-id="b7571-181">De volgende code laat zien hoe u de client met het bestand App.config configureert.</span><span class="sxs-lookup"><span data-stu-id="b7571-181">The following code shows how to configure the client using the App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="b7571-182">De eindpuntdefinities worden verplaatst naar het bestand App.config.</span><span class="sxs-lookup"><span data-stu-id="b7571-182">The endpoint definitions move into the App.config file.</span></span> <span data-ttu-id="b7571-183">Het volgende voorbeeld hetzelfde als de code eerder is vermeld is, moet worden weergegeven direct onder de `<system.serviceModel>` element.</span><span class="sxs-lookup"><span data-stu-id="b7571-183">The following example, which is the same as the code listed previously, should appear directly beneath the `<system.serviceModel>` element.</span></span> <span data-ttu-id="b7571-184">Hier, als voorheen, moet u vervangen de tijdelijke aanduidingen door uw relay-naamruimte en SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="b7571-184">Here, as before, you must replace the placeholders with your relay namespace and SAS key.</span></span>

```xml
<client>
    <endpoint name="solver" contract="Service.IProblemSolver"
              binding="netTcpRelayBinding"
              address="sb://<namespaceName>.servicebus.windows.net/solver"
              behaviorConfiguration="sbTokenProvider"/>
</client>
<behaviors>
    <endpointBehaviors>
        <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
                <tokenProvider>
                    <sharedAccessSignature keyName="RootManageSharedAccessKey" key="<yourKey>" />
                </tokenProvider>
            </transportClientEndpointBehavior>
        </behavior>
    </endpointBehaviors>
</behaviors>
```

## <a name="next-steps"></a><span data-ttu-id="b7571-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b7571-185">Next steps</span></span>
<span data-ttu-id="b7571-186">Nu u de basisprincipes van Azure Relay hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b7571-186">Now that you've learned the basics of Azure Relay, follow these links to learn more.</span></span>

* [<span data-ttu-id="b7571-187">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="b7571-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="b7571-188">Overzicht van Azure Service Bus-architectuur</span><span class="sxs-lookup"><span data-stu-id="b7571-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="b7571-189">Download Service Bus-voorbeelden van [Azure-voorbeelden] [ Azure samples] of Raadpleeg de [overzicht van Service Bus-voorbeelden][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="b7571-189">Download Service Bus samples from [Azure samples][Azure samples] or see the [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md

---
title: aaaGet de slag met Azure Relay WCF-relays in .NET | Microsoft Docs
description: Meer informatie over hoe Azure Relay WCF toouse tooconnect twee toepassingen die worden gehost op verschillende locaties doorstuurt.
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
ms.openlocfilehash: a652617fc2e9b7c8d62d39fa914f77df6e3a1771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-relay-wcf-relays-with-net"></a><span data-ttu-id="e3955-103">Hoe toouse Azure Relay WCF doorstuurt met .NET</span><span class="sxs-lookup"><span data-stu-id="e3955-103">How toouse Azure Relay WCF relays with .NET</span></span>
<span data-ttu-id="e3955-104">Dit artikel wordt beschreven hoe toouse hello Azure Relay-service.</span><span class="sxs-lookup"><span data-stu-id="e3955-104">This article describes how toouse hello Azure Relay service.</span></span> <span data-ttu-id="e3955-105">Hallo-voorbeelden zijn geschreven in C# en gebruiken van Hallo Windows Communication Foundation (WCF) API met extensies die deel uitmaken Hallo Service Bus-assembly.</span><span class="sxs-lookup"><span data-stu-id="e3955-105">hello samples are written in C# and use hello Windows Communication Foundation (WCF) API with extensions contained in hello Service Bus assembly.</span></span> <span data-ttu-id="e3955-106">Zie voor meer informatie over Azure relay Hallo [Azure Relay overzicht](relay-what-is-it.md).</span><span class="sxs-lookup"><span data-stu-id="e3955-106">For more information about Azure relay, see hello [Azure Relay overview](relay-what-is-it.md).</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="what-is-wcf-relay"></a><span data-ttu-id="e3955-107">Wat is de Relay WCF?</span><span class="sxs-lookup"><span data-stu-id="e3955-107">What is WCF Relay?</span></span>

<span data-ttu-id="e3955-108">Hello Azure [ *WCF Relay* ](relay-what-is-it.md) service kunt u toobuild hybride toepassingen die worden uitgevoerd in een Azure-datacenter en uw eigen on-premises bedrijfsomgeving.</span><span class="sxs-lookup"><span data-stu-id="e3955-108">hello Azure [*WCF Relay*](relay-what-is-it.md) service enables you toobuild hybrid applications that run in both an Azure datacenter and your own on-premises enterprise environment.</span></span> <span data-ttu-id="e3955-109">Hallo relay-service dit is mogelijk doordat u toosecurely Windows Communication Foundation (WCF)-services die zich bevinden in een zakelijke enterprise netwerk toohello openbare cloud, zonder dat een firewallverbinding hoeft tooopen of een vereiste weergeven Tussenkomende wijzigingen tooa bedrijfsnetwerkinfrastructuur.</span><span class="sxs-lookup"><span data-stu-id="e3955-109">hello relay service facilitates this by enabling you toosecurely expose Windows Communication Foundation (WCF) services that reside within a corporate enterprise network toohello public cloud, without having tooopen a firewall connection, or requiring intrusive changes tooa corporate network infrastructure.</span></span>

![WCF Relay-concepten](./media/service-bus-dotnet-how-to-use-relay/sb-relay-01.png)

<span data-ttu-id="e3955-111">Azure Relay kunt u toohost WCF-services in uw bestaande bedrijfsomgeving.</span><span class="sxs-lookup"><span data-stu-id="e3955-111">Azure Relay enables you toohost WCF services within your existing enterprise environment.</span></span> <span data-ttu-id="e3955-112">U kunt vervolgens delegeren luisteren naar binnenkomende sessies en aanvragen toothese WCF services toohello relay-service actief is in Azure.</span><span class="sxs-lookup"><span data-stu-id="e3955-112">You can then delegate listening for incoming sessions and requests toothese WCF services toohello relay service running within Azure.</span></span> <span data-ttu-id="e3955-113">Hierdoor kunt u tooexpose deze services tooapplication code die wordt uitgevoerd in Azure, of toomobile werknemers of extranetpartneromgevingen.</span><span class="sxs-lookup"><span data-stu-id="e3955-113">This enables you tooexpose these services tooapplication code running in Azure, or toomobile workers or extranet partner environments.</span></span> <span data-ttu-id="e3955-114">Relay kunt u toosecurely bepalen wie toegang deze services heel nauwkeurig tot.</span><span class="sxs-lookup"><span data-stu-id="e3955-114">Relay enables you toosecurely control who can access these services at a fine-grained level.</span></span> <span data-ttu-id="e3955-115">Het biedt een krachtige en veilige manier tooexpose functies en gegevens van uw bestaande bedrijfsoplossingen en profiteren van deze vanuit Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="e3955-115">It provides a powerful and secure way tooexpose application functionality and data from your existing enterprise solutions and take advantage of it from hello cloud.</span></span>

<span data-ttu-id="e3955-116">Dit artikel wordt beschreven hoe toouse Azure Relay toocreate een WCF-webservice weergegeven met behulp van een TCP-kanaalbinding waarmee een beveiligde communicatie tussen twee partijen wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e3955-116">This article discusses how toouse Azure Relay toocreate a WCF web service, exposed using a TCP channel binding, that implements a secure conversation between two parties.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="get-hello-service-bus-nuget-package"></a><span data-ttu-id="e3955-117">Hallo Service Bus NuGet-pakket</span><span class="sxs-lookup"><span data-stu-id="e3955-117">Get hello Service Bus NuGet package</span></span>
<span data-ttu-id="e3955-118">Hallo [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is Hallo gemakkelijkste manier tooget Hallo Service Bus-API en tooconfigure uw toepassing met alle Hallo Service Bus-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e3955-118">hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is hello easiest way tooget hello Service Bus API and tooconfigure your application with all of hello Service Bus dependencies.</span></span> <span data-ttu-id="e3955-119">tooinstall hello NuGet-pakket in uw project Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3955-119">tooinstall hello NuGet package in your project, do hello following:</span></span>

1. <span data-ttu-id="e3955-120">Klik in Solution Explorer met de rechtermuisknop op **Verwijzingen** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="e3955-120">In Solution Explorer, right-click **References**, then click **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="e3955-121">Zoek naar 'Service Bus' en selecteer Hallo **Microsoft Azure Service Bus** item.</span><span class="sxs-lookup"><span data-stu-id="e3955-121">Search for "Service Bus" and select hello **Microsoft Azure Service Bus** item.</span></span> <span data-ttu-id="e3955-122">Klik op **installeren** toocomplete Hallo installatie en sluit vervolgens Hallo in het dialoogvenster te volgen:</span><span class="sxs-lookup"><span data-stu-id="e3955-122">Click **Install** toocomplete hello installation, then close hello following dialog box:</span></span>
   
   ![](./media/service-bus-dotnet-how-to-use-relay/getting-started-multi-tier-13.png)

## <a name="expose-and-consume-a-soap-web-service-with-tcp"></a><span data-ttu-id="e3955-123">Weergeven en gebruiken van een SOAP-webservice met TCP</span><span class="sxs-lookup"><span data-stu-id="e3955-123">Expose and consume a SOAP web service with TCP</span></span>
<span data-ttu-id="e3955-124">een bestaande WCF SOAP-webservice voor extern verbruik tooexpose, moet u wijzigingen toohello servicebindingen en -adressen.</span><span class="sxs-lookup"><span data-stu-id="e3955-124">tooexpose an existing WCF SOAP web service for external consumption, you must make changes toohello service bindings and addresses.</span></span> <span data-ttu-id="e3955-125">Hiervoor wijzigingen tooyour configuratiebestand of codewijzigingen nodig codewijzigingen, afhankelijk van hoe u hebt ingesteld en de WCF-services zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e3955-125">This may require changes tooyour configuration file or it could require code changes, depending on how you have set up and configured your WCF services.</span></span> <span data-ttu-id="e3955-126">Houd er rekening mee dat WCF u toohave kunt meerdere netwerkeindpunten via dezelfde service Hallo, zodat u kunt behouden Hallo bestaande interne eindpunten tijdens het toevoegen van de relay-eindpunten voor externe toegang op Hallo dezelfde tijd.</span><span class="sxs-lookup"><span data-stu-id="e3955-126">Note that WCF allows you toohave multiple network endpoints over hello same service, so you can retain hello existing internal endpoints while adding relay endpoints for external access at hello same time.</span></span>

<span data-ttu-id="e3955-127">In deze taak bouwen van een eenvoudige WCF-service en een relay-listener tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e3955-127">In this task, you build a simple WCF service and add a relay listener tooit.</span></span> <span data-ttu-id="e3955-128">In deze oefening wordt ervan uitgegaan dat enigszins bekend bent met Visual Studio en daarom komt niet in detail behandeld alle Hallo details van een project maken.</span><span class="sxs-lookup"><span data-stu-id="e3955-128">This exercise assumes some familiarity with Visual Studio, and therefore does not walk through all hello details of creating a project.</span></span> <span data-ttu-id="e3955-129">In plaats daarvan ligt de nadruk op Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="e3955-129">Instead, it focuses on hello code.</span></span>

<span data-ttu-id="e3955-130">Voordat u deze stappen begint, voert u hello te volgen procedure tooset van uw omgeving:</span><span class="sxs-lookup"><span data-stu-id="e3955-130">Before starting these steps, complete hello following procedure tooset up your environment:</span></span>

1. <span data-ttu-id="e3955-131">Maak in Visual Studio een consoletoepassing die twee projecten 'Client' en 'Service' binnen de oplossing Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="e3955-131">Within Visual Studio, create a console application that contains two projects, "Client" and "Service", within hello solution.</span></span>
2. <span data-ttu-id="e3955-132">Hallo Service Bus NuGet-pakket tooboth projecten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e3955-132">Add hello Service Bus NuGet package tooboth projects.</span></span> <span data-ttu-id="e3955-133">Dit pakket voegt alle Hallo vereiste assembly-verwijzingen tooyour projecten.</span><span class="sxs-lookup"><span data-stu-id="e3955-133">This package adds all hello necessary assembly references tooyour projects.</span></span>

### <a name="how-toocreate-hello-service"></a><span data-ttu-id="e3955-134">Hoe toocreate Hallo service</span><span class="sxs-lookup"><span data-stu-id="e3955-134">How toocreate hello service</span></span>
<span data-ttu-id="e3955-135">Maak eerst Hallo-service zelf.</span><span class="sxs-lookup"><span data-stu-id="e3955-135">First, create hello service itself.</span></span> <span data-ttu-id="e3955-136">Een WCF-service bestaat uit ten minste drie onderdelen:</span><span class="sxs-lookup"><span data-stu-id="e3955-136">Any WCF service consists of at least three distinct parts:</span></span>

* <span data-ttu-id="e3955-137">De definitie van een contract waarmee wordt beschreven welke berichten worden uitgewisseld en welke bewerkingen zijn toobe aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="e3955-137">Definition of a contract that describes what messages are exchanged and what operations are toobe invoked.</span></span>
* <span data-ttu-id="e3955-138">Implementatie van deze overeenkomst.</span><span class="sxs-lookup"><span data-stu-id="e3955-138">Implementation of that contract.</span></span>
* <span data-ttu-id="e3955-139">Host die als host fungeert voor Hallo WCF-service en beschrijft de verschillende eindpunten.</span><span class="sxs-lookup"><span data-stu-id="e3955-139">Host that hosts hello WCF service and exposes several endpoints.</span></span>

<span data-ttu-id="e3955-140">Hallo-codevoorbeelden in deze sectie hebben betrekking op elk van deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="e3955-140">hello code examples in this section address each of these components.</span></span>

<span data-ttu-id="e3955-141">Hallo-contract wordt één bewerking gedefinieerd `AddNumbers`, die twee getallen worden opgeteld en Hallo resultaat retourneert.</span><span class="sxs-lookup"><span data-stu-id="e3955-141">hello contract defines a single operation, `AddNumbers`, that adds two numbers and returns hello result.</span></span> <span data-ttu-id="e3955-142">Hallo `IProblemSolverChannel` interface schakelt Hallo client toomore eenvoudig hello proxy levensduur beheren.</span><span class="sxs-lookup"><span data-stu-id="e3955-142">hello `IProblemSolverChannel` interface enables hello client toomore easily manage hello proxy lifetime.</span></span> <span data-ttu-id="e3955-143">Het wordt aanbevolen een dergelijke interface te maken.</span><span class="sxs-lookup"><span data-stu-id="e3955-143">Creating such an interface is considered a best practice.</span></span> <span data-ttu-id="e3955-144">Het is een goed idee tooput dit contract definitie in een afzonderlijk bestand, zodat u kunt verwijzen naar dit bestand uit uw 'Client' en de 'Service'-projecten, maar u kunt ook Hallo code naar beide projecten kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e3955-144">It's a good idea tooput this contract definition into a separate file so that you can reference that file from both your "Client" and "Service" projects, but you can also copy hello code into both projects.</span></span>

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

<span data-ttu-id="e3955-145">Met Hallo contract aanwezig is Hallo-implementatie als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="e3955-145">With hello contract in place, hello implementation is as follows:</span></span>

```csharp
class ProblemSolver : IProblemSolver
{
    public int AddNumbers(int a, int b)
    {
        return a + b;
    }
}
```

### <a name="configure-a-service-host-programmatically"></a><span data-ttu-id="e3955-146">Een servicehost via een programma configureren</span><span class="sxs-lookup"><span data-stu-id="e3955-146">Configure a service host programmatically</span></span>
<span data-ttu-id="e3955-147">U kunt nu Hallo service hosten met Hallo contract en implementatie in plaats.</span><span class="sxs-lookup"><span data-stu-id="e3955-147">With hello contract and implementation in place, you can now host hello service.</span></span> <span data-ttu-id="e3955-148">Hosting vindt plaats in een [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, die zorgt voor het beheren van exemplaren van Hallo-service en hosts Hallo eindpunten die naar berichten luisteren.</span><span class="sxs-lookup"><span data-stu-id="e3955-148">Hosting occurs inside a [System.ServiceModel.ServiceHost](https://msdn.microsoft.com/library/system.servicemodel.servicehost.aspx) object, which takes care of managing instances of hello service and hosts hello endpoints that listen for messages.</span></span> <span data-ttu-id="e3955-149">Hallo volgende code wordt geconfigureerd voor Hallo met zowel een regulier lokaal eindpunt als een relay eindpunt tooillustrate Hallo uiterlijk, naast elkaar van interne en externe eindpunten.</span><span class="sxs-lookup"><span data-stu-id="e3955-149">hello following code configures hello service with both a regular local endpoint and a relay endpoint tooillustrate hello appearance, side by side, of internal and external endpoints.</span></span> <span data-ttu-id="e3955-150">Vervang de tekenreeks Hallo *naamruimte* met de naamruimtenaam van uw en *yourKey* met Hallo SAS-sleutel die u hebt verkregen in de vorige instellingsstap Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3955-150">Replace hello string *namespace* with your namespace name and *yourKey* with hello SAS key that you obtained in hello previous setup step.</span></span>

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

Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();

sh.Close();
```

<span data-ttu-id="e3955-151">In voorbeeld hello, maakt u twee eindpunten die op Hallo dezelfde implementatie contract.</span><span class="sxs-lookup"><span data-stu-id="e3955-151">In hello example, you create two endpoints that are on hello same contract implementation.</span></span> <span data-ttu-id="e3955-152">Een lokale is en een eindpunt is geprojecteerd via Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="e3955-152">One is local and one is projected through Azure Relay.</span></span> <span data-ttu-id="e3955-153">Hallo belangrijke verschillen tussen deze twee zijn Hallo bindingen; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) voor Hallo lokale en [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) voor Hallo relay eindpunt en hello-mailadressen.</span><span class="sxs-lookup"><span data-stu-id="e3955-153">hello key differences between them are hello bindings; [NetTcpBinding](https://msdn.microsoft.com/library/system.servicemodel.nettcpbinding.aspx) for hello local one and [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding#microsoft_servicebus_nettcprelaybinding) for hello relay endpoint and hello addresses.</span></span> <span data-ttu-id="e3955-154">Hallo lokale eindpunt heeft een lokaal netwerkadres met een afzonderlijke poort.</span><span class="sxs-lookup"><span data-stu-id="e3955-154">hello local endpoint has a local network address with a distinct port.</span></span> <span data-ttu-id="e3955-155">Hallo relay-eindpunt heeft een eindpuntadres samengesteld van Hallo tekenreeks `sb`, uw naamruimtenaam en Hallo pad 'Solver '.'</span><span class="sxs-lookup"><span data-stu-id="e3955-155">hello relay endpoint has an endpoint address composed of hello string `sb`, your namespace name, and hello path "solver."</span></span> <span data-ttu-id="e3955-156">Dit resulteert in Hallo URI `sb://[serviceNamespace].servicebus.windows.net/solver`, service-eindpunt Hallo identificeren als een Service Bus (relais) TCP-eindpunt met een volledig gekwalificeerde externe DNS-naam.</span><span class="sxs-lookup"><span data-stu-id="e3955-156">This results in hello URI `sb://[serviceNamespace].servicebus.windows.net/solver`, identifying hello service endpoint as a Service Bus (relay) TCP endpoint with a fully qualified external DNS name.</span></span> <span data-ttu-id="e3955-157">Als u Hallo code Hallo tijdelijke aanduidingen vervangt in Hallo plaatsen `Main` functie Hallo **Service** toepassing, hebt u een functionele service.</span><span class="sxs-lookup"><span data-stu-id="e3955-157">If you place hello code replacing hello placeholders into hello `Main` function of hello **Service** application, you will have a functional service.</span></span> <span data-ttu-id="e3955-158">Als u wilt dat uw toolisten service uitsluitend op Hallo relay, verwijdert u Hallo lokaal eindpunt declaratie.</span><span class="sxs-lookup"><span data-stu-id="e3955-158">If you want your service toolisten exclusively on hello relay, remove hello local endpoint declaration.</span></span>

### <a name="configure-a-service-host-in-hello-appconfig-file"></a><span data-ttu-id="e3955-159">Een ServiceHost configureren in Hallo App.config-bestand</span><span class="sxs-lookup"><span data-stu-id="e3955-159">Configure a service host in hello App.config file</span></span>
<span data-ttu-id="e3955-160">U kunt ook configureren Hallo-host met behulp van Hallo App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="e3955-160">You can also configure hello host using hello App.config file.</span></span> <span data-ttu-id="e3955-161">Hallo servicehostingcode in dit geval wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3955-161">hello service hosting code in this case appears in hello next example.</span></span>

```csharp
ServiceHost sh = new ServiceHost(typeof(ProblemSolver));
sh.Open();
Console.WriteLine("Press ENTER tooclose");
Console.ReadLine();
sh.Close();
```

<span data-ttu-id="e3955-162">Hallo-eindpuntdefinities worden verplaatst naar Hallo App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="e3955-162">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="e3955-163">Hallo NuGet-pakket is al een reeks definities toohello App.config-bestand toegevoegd die zijn vereist Hallo configuratie-extensies voor Azure Relay.</span><span class="sxs-lookup"><span data-stu-id="e3955-163">hello NuGet package has already added a range of definitions toohello App.config file, which are hello required configuration extensions for Azure Relay.</span></span> <span data-ttu-id="e3955-164">Hallo volgende voorbeeld met Hallo exacte equivalent van de vorige code Hallo moet worden weergegeven direct onder Hallo **system.serviceModel** element.</span><span class="sxs-lookup"><span data-stu-id="e3955-164">hello following example, which is hello exact equivalent of hello previous code, should appear directly beneath hello **system.serviceModel** element.</span></span> <span data-ttu-id="e3955-165">In dit voorbeeld wordt ervan uitgegaan dat uw project C#-naamruimte de naam **Service** heeft.</span><span class="sxs-lookup"><span data-stu-id="e3955-165">This code example assumes that your project C# namespace is named **Service**.</span></span>
<span data-ttu-id="e3955-166">Vervang de tijdelijke aanduidingen Hallo met de naam van de relay-naamruimte en SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="e3955-166">Replace hello placeholders with your relay namespace name and SAS key.</span></span>

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

<span data-ttu-id="e3955-167">Nadat u deze wijzigingen aanbrengt, Hallo-service wordt gestart als voorheen maar met twee live eindpunten: een lokaal en één luisteren in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="e3955-167">After you make these changes, hello service starts as it did before, but with two live endpoints: one local and one listening in hello cloud.</span></span>

### <a name="create-hello-client"></a><span data-ttu-id="e3955-168">Hallo-client maken</span><span class="sxs-lookup"><span data-stu-id="e3955-168">Create hello client</span></span>
#### <a name="configure-a-client-programmatically"></a><span data-ttu-id="e3955-169">Een client via een programma configureren</span><span class="sxs-lookup"><span data-stu-id="e3955-169">Configure a client programmatically</span></span>
<span data-ttu-id="e3955-170">tooconsume Hallo-service, kunt u een WCF-client met samenstellen een [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span><span class="sxs-lookup"><span data-stu-id="e3955-170">tooconsume hello service, you can construct a WCF client using a [ChannelFactory](https://msdn.microsoft.com/library/system.servicemodel.channelfactory.aspx) object.</span></span> <span data-ttu-id="e3955-171">Service Bus maakt gebruik van een beveiligingsmodel op basis van tokens dat wordt geïmplementeerd met SAS.</span><span class="sxs-lookup"><span data-stu-id="e3955-171">Service Bus uses a token-based security model implemented using SAS.</span></span> <span data-ttu-id="e3955-172">Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) klasse vertegenwoordigt een beveiligingstokenprovider met ingebouwde factorymethoden waarmee een aantal bekende token providers retourneren.</span><span class="sxs-lookup"><span data-stu-id="e3955-172">hello [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) class represents a security token provider with built-in factory methods that return some well-known token providers.</span></span> <span data-ttu-id="e3955-173">Hallo volgende voorbeeld wordt Hallo [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) methode toohandle Hallo verkrijging van Hallo juiste SAS-token.</span><span class="sxs-lookup"><span data-stu-id="e3955-173">hello following example uses hello [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) method toohandle hello acquisition of hello appropriate SAS token.</span></span> <span data-ttu-id="e3955-174">Hallo-naam en sleutel zijn verkregen via Hallo beheerportal, zoals beschreven in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e3955-174">hello name and key are those obtained from hello portal as described in hello previous section.</span></span>

<span data-ttu-id="e3955-175">Eerste, verwijzing of copy Hallo `IProblemSolver` Contractcode van Hallo-service in uw clientproject.</span><span class="sxs-lookup"><span data-stu-id="e3955-175">First, reference or copy hello `IProblemSolver` contract code from hello service into your client project.</span></span>

<span data-ttu-id="e3955-176">Vervang vervolgens Hallo-code in Hallo `Main` methode voor het Hallo-client opnieuw Hallo tijdelijke aanduiding voor tekst vervangen door uw relay-naamruimte en SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="e3955-176">Then, replace hello code in hello `Main` method of hello client, again replacing hello placeholder text with your relay namespace and SAS key.</span></span>

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

<span data-ttu-id="e3955-177">U kunt nu opbouwen Hallo-client en Hallo-service, ze uit te voeren (Hallo service eerst uitvoeren), Hallo client roept Hallo-service en wordt afgedrukt **9**.</span><span class="sxs-lookup"><span data-stu-id="e3955-177">You can now build hello client and hello service, run them (run hello service first), and hello client calls hello service and prints **9**.</span></span> <span data-ttu-id="e3955-178">U kunt Hallo-client en server op verschillende computers uitvoeren zelfs in netwerken en Hallo communicatie nog steeds werken.</span><span class="sxs-lookup"><span data-stu-id="e3955-178">You can run hello client and server on different machines, even across networks, and hello communication will still work.</span></span> <span data-ttu-id="e3955-179">Hallo-clientcode kunt ook in Hallo cloud of lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e3955-179">hello client code can also run in hello cloud or locally.</span></span>

#### <a name="configure-a-client-in-hello-appconfig-file"></a><span data-ttu-id="e3955-180">Een client in Hallo App.config-bestand configureren</span><span class="sxs-lookup"><span data-stu-id="e3955-180">Configure a client in hello App.config file</span></span>
<span data-ttu-id="e3955-181">Hallo volgende code toont hoe tooconfigure Hallo client met Hallo App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="e3955-181">hello following code shows how tooconfigure hello client using hello App.config file.</span></span>

```csharp
var cf = new ChannelFactory<IProblemSolverChannel>("solver");
using (var ch = cf.CreateChannel())
{
    Console.WriteLine(ch.AddNumbers(4, 5));
}
```

<span data-ttu-id="e3955-182">Hallo-eindpuntdefinities worden verplaatst naar Hallo App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="e3955-182">hello endpoint definitions move into hello App.config file.</span></span> <span data-ttu-id="e3955-183">Hallo volgende voorbeeld is hetzelfde als Hallo code eerder is vermeld, hello, ziet er direct onder Hallo `<system.serviceModel>` element.</span><span class="sxs-lookup"><span data-stu-id="e3955-183">hello following example, which is hello same as hello code listed previously, should appear directly beneath hello `<system.serviceModel>` element.</span></span> <span data-ttu-id="e3955-184">Hier, als voorheen, moet u vervangen Hallo tijdelijke aanduidingen door uw relay-naamruimte en SAS-sleutel.</span><span class="sxs-lookup"><span data-stu-id="e3955-184">Here, as before, you must replace hello placeholders with your relay namespace and SAS key.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e3955-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3955-185">Next steps</span></span>
<span data-ttu-id="e3955-186">Nu u de basisbeginselen van Azure Relay Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="e3955-186">Now that you've learned hello basics of Azure Relay, follow these links toolearn more.</span></span>

* [<span data-ttu-id="e3955-187">Wat is Azure Relay?</span><span class="sxs-lookup"><span data-stu-id="e3955-187">What is Azure Relay?</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="e3955-188">Overzicht van Azure Service Bus-architectuur</span><span class="sxs-lookup"><span data-stu-id="e3955-188">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* <span data-ttu-id="e3955-189">Download Service Bus-voorbeelden van [Azure-voorbeelden] [ Azure samples] of Raadpleeg Hallo [overzicht van Service Bus-voorbeelden][overview of Service Bus samples].</span><span class="sxs-lookup"><span data-stu-id="e3955-189">Download Service Bus samples from [Azure samples][Azure samples] or see hello [overview of Service Bus samples][overview of Service Bus samples].</span></span>

[Shared Access Signature Authentication with Service Bus]: ../service-bus-messaging/service-bus-shared-access-signature-authentication.md
[Azure samples]: https://code.msdn.microsoft.com/site/search?query=service%20bus&f%5B0%5D.Value=service%20bus&f%5B0%5D.Type=SearchText&ac=2
[overview of Service Bus samples]: ../service-bus-messaging/service-bus-samples.md

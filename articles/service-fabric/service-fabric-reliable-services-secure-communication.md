---
title: veilige communicatie voor services in Azure Service Fabric aaaHelp | Microsoft Docs
description: Overzicht van hoe toohelp beveiligde communicatie voor betrouwbare services die worden uitgevoerd in een Azure Service Fabric-cluster.
services: service-fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: vturecek
ms.assetid: fc129c1a-fbe4-4339-83ae-0e69a41654e0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 15201eb503322b17db329b319f1f42860b0f0c6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="eb4cd-103">Veilige communicatie van de Help voor services in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="eb4cd-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="eb4cd-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="eb4cd-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="eb4cd-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="eb4cd-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

<span data-ttu-id="eb4cd-106">Beveiliging is een van de belangrijkste aspecten Hallo van communicatie.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-106">Security is one of hello most important aspects of communication.</span></span> <span data-ttu-id="eb4cd-107">toepassingsframework voor Hallo Reliable Services biedt enkele vooraf gedefinieerde communicatie stacks en hulpprogramma's waarmee u tooimprove beveiliging kunt.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-107">hello Reliable Services application framework provides a few prebuilt communication stacks and tools that you can use tooimprove security.</span></span> <span data-ttu-id="eb4cd-108">In dit artikel wordt gesproken over hoe tooimprove beveiliging wanneer u remoting service en het Hallo communicatiestack Windows Communication Foundation (WCF).</span><span class="sxs-lookup"><span data-stu-id="eb4cd-108">This article talks about how tooimprove security when you're using service remoting and hello Windows Communication Foundation (WCF) communication stack.</span></span>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="eb4cd-109">Beveiligen van een service als u service voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="eb4cd-109">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="eb4cd-110">We gebruiken een bestaande [voorbeeld](service-fabric-reliable-services-communication-remoting.md) waarin wordt uitgelegd hoe tooset van externe toegang tot betrouwbare services.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-110">We are using an existing [example](service-fabric-reliable-services-communication-remoting.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="eb4cd-111">toohelp beveiligen van een service als u service voor externe toegang, wordt als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-111">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="eb4cd-112">Maken van een interface `IHelloWorldStateful`, die definieert Hallo-methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-112">Create an interface, `IHelloWorldStateful`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="eb4cd-113">Uw service maakt gebruik van `FabricTransportServiceRemotingListener`, die is gedeclareerd in Hallo `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` naamruimte.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-113">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `Microsoft.ServiceFabric.Services.Remoting.FabricTransport.Runtime` namespace.</span></span> <span data-ttu-id="eb4cd-114">Dit is een `ICommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-114">This is an `ICommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```csharp
    public interface IHelloWorldStateful : IService
    {
        Task<string> GetHelloWorld();
    }

    internal class HelloWorldStateful : StatefulService, IHelloWorldStateful
    {
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]{
                    new ServiceReplicaListener(
                        (context) => new FabricTransportServiceRemotingListener(context,this))};
        }

        public Task<string> GetHelloWorld()
        {
            return Task.FromResult("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="eb4cd-115">Instellingen voor listener en beveiligingsreferenties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-115">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="eb4cd-116">Zorg ervoor dat Hallo-certificaat dat u wilt dat toouse toohelp beveiligde die uw servicecommunicatie is geïnstalleerd op alle Hallo-knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-116">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="eb4cd-117">Er zijn twee manieren waarop u instellingen voor listener en beveiligingsreferenties kunt opgeven:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-117">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="eb4cd-118">Ze rechtstreeks op Hallo servicecode bieden:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-118">Provide them directly in hello service code:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           FabricTransportRemotingListenerSettings  listenerSettings = new FabricTransportRemotingListenerSettings
           {
               MaxMessageSize = 10000000,
               SecurityCredentials = GetSecurityCredentials()
           };
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(context,this,listenerSettings))
           };
       }

       private static SecurityCredentials GetSecurityCredentials()
       {
           // Provide certificate details.
           var x509Credentials = new X509Credentials
           {
               FindType = X509FindType.FindByThumbprint,
               FindValue = "4FEF3950642138446CC364A396E1E881DB76B48C",
               StoreLocation = StoreLocation.LocalMachine,
               StoreName = "My",
               ProtectionLevel = ProtectionLevel.EncryptAndSign
           };
           x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
           x509Credentials.RemoteCertThumbprints.Add("9FEF3950642138446CC364A396E1E881DB76B483");
           return x509Credentials;
       }
       ```
   2. <span data-ttu-id="eb4cd-119">Ze bieden met behulp van een [configuratiepakket](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="eb4cd-119">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="eb4cd-120">Voeg een `TransportSettings` sectie in Hallo settings.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-120">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <Section Name="HelloWorldStatefulTransportSettings">
           <Parameter Name="MaxMessageSize" Value="10000000" />
           <Parameter Name="SecurityCredentialsType" Value="X509" />
           <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
           <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
           <Parameter Name="CertificateRemoteThumbprints" Value="9FEF3950642138446CC364A396E1E881DB76B483" />
           <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
           <Parameter Name="CertificateStoreName" Value="My" />
           <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
           <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
       </Section>
       ```

       <span data-ttu-id="eb4cd-121">In dit geval Hallo `CreateServiceReplicaListeners` methode ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-121">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

       ```csharp
       protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
       {
           return new[]
           {
               new ServiceReplicaListener(
                   (context) => new FabricTransportServiceRemotingListener(
                       context,this,FabricTransportRemotingListenerSettings .LoadFrom("HelloWorldStatefulTransportSettings")))
           };
       }
       ```

        <span data-ttu-id="eb4cd-122">Als u een `TransportSettings` hello settings.xml bestand, met `FabricTransportRemotingListenerSettings ` alle Hallo-instellingen in deze sectie standaard wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-122">If you add a `TransportSettings` section in hello settings.xml file , `FabricTransportRemotingListenerSettings ` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section .-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="eb4cd-123">In dit geval Hallo `CreateServiceReplicaListeners` methode ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-123">In this case, hello `CreateServiceReplicaListeners` method will look like this:</span></span>

        ```csharp
        protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
        {
            return new[]
            {
                return new[]{
                        new ServiceReplicaListener(
                            (context) => new FabricTransportServiceRemotingListener(context,this))};
            };
        }
        ```
3. <span data-ttu-id="eb4cd-124">Wanneer u methoden aanroepen op een beveiligde service via Hallo remoting stack, in plaats van Hallo `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` klasse toocreate geen proxy-service, gebruik `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-124">When you call methods on a secured service by using hello remoting stack, instead of using hello `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxy` class toocreate a service proxy, use `Microsoft.ServiceFabric.Services.Remoting.Client.ServiceProxyFactory`.</span></span> <span data-ttu-id="eb4cd-125">Doorgeven `FabricTransportRemotingSettings`, die bevat `SecurityCredentials`.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-125">Pass in `FabricTransportRemotingSettings`, which contains `SecurityCredentials`.</span></span>

    ```csharp

    var x509Credentials = new X509Credentials
    {
        FindType = X509FindType.FindByThumbprint,
        FindValue = "9FEF3950642138446CC364A396E1E881DB76B483",
        StoreLocation = StoreLocation.LocalMachine,
        StoreName = "My",
        ProtectionLevel = ProtectionLevel.EncryptAndSign
    };
    x509Credentials.RemoteCommonNames.Add("ServiceFabric-Test-Cert");
    x509Credentials.RemoteCertThumbprints.Add("4FEF3950642138446CC364A396E1E881DB76B48C");

    FabricTransportRemotingSettings transportSettings = new FabricTransportRemotingSettings
    {
        SecurityCredentials = x509Credentials,
    };

    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(transportSettings));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="eb4cd-126">Als de clientcode Hallo als onderdeel van een service wordt uitgevoerd, kunt u laden `FabricTransportRemotingSettings` uit Hallo settings.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-126">If hello client code is running as part of a service, you can load `FabricTransportRemotingSettings` from hello settings.xml file.</span></span> <span data-ttu-id="eb4cd-127">Maak een HelloWorldClientTransportSettings-sectie die vergelijkbaar toohello servicecode, zoals eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-127">Create a HelloWorldClientTransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="eb4cd-128">Controleer Hallo wijzigingen toohello clientcode te volgen:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-128">Make hello following changes toohello client code:</span></span>

    ```csharp
    ServiceProxyFactory serviceProxyFactory = new ServiceProxyFactory(
        (c) => new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.LoadFrom("HelloWorldClientTransportSettings")));

    IHelloWorldStateful client = serviceProxyFactory.CreateServiceProxy<IHelloWorldStateful>(
        new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

    <span data-ttu-id="eb4cd-129">Als het Hallo-client wordt niet uitgevoerd als onderdeel van een service, kunt u een bestand client_name.settings.xml in Hallo dezelfde locatie Hallo client_name.exe.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-129">If hello client is not running as part of a service, you can create a client_name.settings.xml file in hello same location where hello client_name.exe is.</span></span> <span data-ttu-id="eb4cd-130">Maak vervolgens een TransportSettings-sectie in dat bestand.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-130">Then create a TransportSettings section in that file.</span></span>

    <span data-ttu-id="eb4cd-131">Vergelijkbare toohello service, als u een `TransportSettings` sectie in client-settings.xml/client_name.settings.xml `FabricTransportRemotingSettings` alle Hallo-instellingen in deze sectie standaard laadt.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-131">Similar toohello service, if you add a `TransportSettings` section in client settings.xml/client_name.settings.xml, `FabricTransportRemotingSettings` loads all hello settings from this section by default.</span></span>

    <span data-ttu-id="eb4cd-132">In dat geval wordt hello eerdere code nog verder vereenvoudigd:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-132">In that case, hello earlier code is even further simplified:</span></span>  

    ```csharp

    IHelloWorldStateful client = ServiceProxy.Create<IHelloWorldStateful>(
                 new Uri("fabric:/MyApplication/MyHelloWorldService"));

    string message = await client.GetHelloWorld();

    ```

## <a name="help-secure-a-service-when-youre-using-a-wcf-based-communication-stack"></a><span data-ttu-id="eb4cd-133">Beveiligen van een service wanneer u een WCF-communicatie-stack</span><span class="sxs-lookup"><span data-stu-id="eb4cd-133">Help secure a service when you're using a WCF-based communication stack</span></span>
<span data-ttu-id="eb4cd-134">We gebruiken een bestaande [voorbeeld](service-fabric-reliable-services-communication-wcf.md) waarin wordt uitgelegd hoe tooset van een WCF-communicatie stapelen voor betrouwbare services.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-134">We are using an existing [example](service-fabric-reliable-services-communication-wcf.md) that explains how tooset up a WCF-based communication stack for reliable services.</span></span> <span data-ttu-id="eb4cd-135">toohelp beveiligen van een service wanneer u een stack WCF-communicatie gebruikt, wordt als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-135">toohelp secure a service when you're using a WCF-based communication stack, follow these steps:</span></span>

1. <span data-ttu-id="eb4cd-136">Hallo-service, moet u toohelp beveiligde Hallo WCF communicatie listener (`WcfCommunicationListener`) die u maakt.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-136">For hello service, you need toohelp secure hello WCF communication listener (`WcfCommunicationListener`) that you create.</span></span> <span data-ttu-id="eb4cd-137">toodo dit Hallo wijzigen `CreateServiceReplicaListeners` methode.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-137">toodo this, modify hello `CreateServiceReplicaListeners` method.</span></span>

    ```csharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        return new[]
        {
            new ServiceReplicaListener(
                this.CreateWcfCommunicationListener)
        };
    }

    private WcfCommunicationListener<ICalculator> CreateWcfCommunicationListener(StatefulServiceContext context)
    {
       var wcfCommunicationListener = new WcfCommunicationListener<ICalculator>(
            serviceContext:context,
            wcfServiceObject:this,
            // For this example, we will be using NetTcpBinding.
            listenerBinding: GetNetTcpBinding(),
            endpointResourceName:"WcfServiceEndpoint");

        // Add certificate details in hello ServiceHost credentials.
        wcfCommunicationListener.ServiceHost.Credentials.ServiceCertificate.SetCertificate(
            StoreLocation.LocalMachine,
            StoreName.My,
            X509FindType.FindByThumbprint,
            "9DC906B169DC4FAFFD1697AC781E806790749D2F");
        return wcfCommunicationListener;
    }

    private static NetTcpBinding GetNetTcpBinding()
    {
        NetTcpBinding b = new NetTcpBinding(SecurityMode.TransportWithMessageCredential);
        b.Security.Message.ClientCredentialType = MessageCredentialType.Certificate;
        return b;
    }
    ```
2. <span data-ttu-id="eb4cd-138">Hallo-client Hallo `WcfCommunicationClient` klasse die is gemaakt in Hallo vorige [voorbeeld](service-fabric-reliable-services-communication-wcf.md) blijft ongewijzigd.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-138">In hello client, hello `WcfCommunicationClient` class that was created in hello previous [example](service-fabric-reliable-services-communication-wcf.md) remains unchanged.</span></span> <span data-ttu-id="eb4cd-139">Maar u moet toooverride hello `CreateClientAsync` methode van `WcfCommunicationClientFactory`:</span><span class="sxs-lookup"><span data-stu-id="eb4cd-139">But you need toooverride hello `CreateClientAsync` method of `WcfCommunicationClientFactory`:</span></span>

    ```csharp
    public class SecureWcfCommunicationClientFactory<TServiceContract> : WcfCommunicationClientFactory<TServiceContract> where TServiceContract : class
    {
        private readonly Binding clientBinding;
        private readonly object callbackObject;
        public SecureWcfCommunicationClientFactory(
            Binding clientBinding,
            IEnumerable<IExceptionHandler> exceptionHandlers = null,
            IServicePartitionResolver servicePartitionResolver = null,
            string traceId = null,
            object callback = null)
            : base(clientBinding, exceptionHandlers, servicePartitionResolver,traceId,callback)
        {
            this.clientBinding = clientBinding;
            this.callbackObject = callback;
        }

        protected override Task<WcfCommunicationClient<TServiceContract>> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
        {
            var endpointAddress = new EndpointAddress(new Uri(endpoint));
            ChannelFactory<TServiceContract> channelFactory;
            if (this.callbackObject != null)
            {
                channelFactory = new DuplexChannelFactory<TServiceContract>(
                this.callbackObject,
                this.clientBinding,
                endpointAddress);
            }
            else
            {
                channelFactory = new ChannelFactory<TServiceContract>(this.clientBinding, endpointAddress);
            }
            // Add certificate details toohello ChannelFactory credentials.
            // These credentials will be used by hello clients created by
            // SecureWcfCommunicationClientFactory.  
            channelFactory.Credentials.ClientCertificate.SetCertificate(
                StoreLocation.LocalMachine,
                StoreName.My,
                X509FindType.FindByThumbprint,
                "9DC906B169DC4FAFFD1697AC781E806790749D2F");
            var channel = channelFactory.CreateChannel();
            var clientChannel = ((IClientChannel)channel);
            clientChannel.OperationTimeout = this.clientBinding.ReceiveTimeout;
            return Task.FromResult(this.CreateWcfCommunicationClient(channel));
        }
    }
    ```

    <span data-ttu-id="eb4cd-140">Gebruik `SecureWcfCommunicationClientFactory` toocreate een WCF-client voor communicatie (`WcfCommunicationClient`).</span><span class="sxs-lookup"><span data-stu-id="eb4cd-140">Use `SecureWcfCommunicationClientFactory` toocreate a WCF communication client (`WcfCommunicationClient`).</span></span> <span data-ttu-id="eb4cd-141">Hallo client tooinvoke servicemethoden te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb4cd-141">Use hello client tooinvoke service methods.</span></span>

    ```csharp
    IServicePartitionResolver partitionResolver = ServicePartitionResolver.GetDefault();

    var wcfClientFactory = new SecureWcfCommunicationClientFactory<ICalculator>(clientBinding: GetNetTcpBinding(), servicePartitionResolver: partitionResolver);

    var calculatorServiceCommunicationClient =  new WcfCommunicationClient(
        wcfClientFactory,
        ServiceUri,
        ServicePartitionKey.Singleton);

    var result = calculatorServiceCommunicationClient.InvokeWithRetryAsync(
        client => client.Channel.Add(2, 3)).Result;
    ```

## <a name="next-steps"></a><span data-ttu-id="eb4cd-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eb4cd-142">Next steps</span></span>
* [<span data-ttu-id="eb4cd-143">Web-API met OWIN in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="eb4cd-143">Web API with OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)

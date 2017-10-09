---
title: veilige communicatie voor services in Azure Service Fabric aaaHelp | Microsoft Docs
description: Overzicht van hoe toohelp beveiligde communicatie voor betrouwbare services die worden uitgevoerd in een Azure Service Fabric-cluster.
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 14db54d50c35478c1f2c156de0dba36f1427c8cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a><span data-ttu-id="57b0a-103">Veilige communicatie van de Help voor services in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="57b0a-103">Help secure communication for services in Azure Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="57b0a-104">C# op Windows</span><span class="sxs-lookup"><span data-stu-id="57b0a-104">C# on Windows</span></span>](service-fabric-reliable-services-secure-communication.md)
> * [<span data-ttu-id="57b0a-105">Java op Linux</span><span class="sxs-lookup"><span data-stu-id="57b0a-105">Java on Linux</span></span>](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a><span data-ttu-id="57b0a-106">Beveiligen van een service als u service voor externe toegang</span><span class="sxs-lookup"><span data-stu-id="57b0a-106">Help secure a service when you're using service remoting</span></span>
<span data-ttu-id="57b0a-107">We gebruiken hiervoor een bestaande [voorbeeld](service-fabric-reliable-services-communication-remoting-java.md) waarin wordt uitgelegd hoe tooset van externe toegang tot betrouwbare services.</span><span class="sxs-lookup"><span data-stu-id="57b0a-107">We'll be using an existing [example](service-fabric-reliable-services-communication-remoting-java.md) that explains how tooset up remoting for reliable services.</span></span> <span data-ttu-id="57b0a-108">toohelp beveiligen van een service als u service voor externe toegang, wordt als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="57b0a-108">toohelp secure a service when you're using service remoting, follow these steps:</span></span>

1. <span data-ttu-id="57b0a-109">Maken van een interface `HelloWorldStateless`, die definieert Hallo-methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service.</span><span class="sxs-lookup"><span data-stu-id="57b0a-109">Create an interface, `HelloWorldStateless`, that defines hello methods that will be available for a remote procedure call on your service.</span></span> <span data-ttu-id="57b0a-110">Uw service maakt gebruik van `FabricTransportServiceRemotingListener`, die is gedeclareerd in Hallo `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pakket.</span><span class="sxs-lookup"><span data-stu-id="57b0a-110">Your service will use `FabricTransportServiceRemotingListener`, which is declared in hello `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` package.</span></span> <span data-ttu-id="57b0a-111">Dit is een `CommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.</span><span class="sxs-lookup"><span data-stu-id="57b0a-111">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span>

    ```java
    public interface HelloWorldStateless extends Service {
        CompletableFuture<String> getHelloWorld();
    }

    class HelloWorldStatelessImpl extends StatelessService implements HelloWorldStateless {
        @Override
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
        return listeners;
        }

        public CompletableFuture<String> getHelloWorld() {
            return CompletableFuture.completedFuture("Hello World!");
        }
    }
    ```
2. <span data-ttu-id="57b0a-112">Instellingen voor listener en beveiligingsreferenties toevoegen.</span><span class="sxs-lookup"><span data-stu-id="57b0a-112">Add listener settings and security credentials.</span></span>

    <span data-ttu-id="57b0a-113">Zorg ervoor dat Hallo-certificaat dat u wilt dat toouse toohelp beveiligde die uw servicecommunicatie is geïnstalleerd op alle Hallo-knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="57b0a-113">Make sure that hello certificate that you want toouse toohelp secure your service communication is installed on all hello nodes in hello cluster.</span></span> <span data-ttu-id="57b0a-114">Er zijn twee manieren waarop u instellingen voor listener en beveiligingsreferenties kunt opgeven:</span><span class="sxs-lookup"><span data-stu-id="57b0a-114">There are two ways that you can provide listener settings and security credentials:</span></span>

   1. <span data-ttu-id="57b0a-115">Ze bieden met behulp van een [configuratiepakket](service-fabric-application-model.md):</span><span class="sxs-lookup"><span data-stu-id="57b0a-115">Provide them by using a [config package](service-fabric-application-model.md):</span></span>

       <span data-ttu-id="57b0a-116">Voeg een `TransportSettings` sectie in Hallo settings.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="57b0a-116">Add a `TransportSettings` section in hello settings.xml file.</span></span>

       ```xml
       <!--Section name should always end with "TransportSettings".-->
       <!--Here we are using a prefix "HelloWorldStateless".-->
        <Section Name="HelloWorldStatelessTransportSettings">
            <Parameter Name="MaxMessageSize" Value="10000000" />
            <Parameter Name="SecurityCredentialsType" Value="X509_2" />
            <Parameter Name="CertificatePath" Value="/path/to/cert/BD1C71E248B8C6834C151174DECDBDC02DE1D954.crt" />
            <Parameter Name="CertificateProtectionLevel" Value="EncryptandSign" />
            <Parameter Name="CertificateRemoteThumbprints" Value="BD1C71E248B8C6834C151174DECDBDC02DE1D954" />
        </Section>

       ```

       <span data-ttu-id="57b0a-117">In dit geval Hallo `createServiceInstanceListeners` methode ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="57b0a-117">In this case, hello `createServiceInstanceListeners` method will look like this:</span></span>

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        <span data-ttu-id="57b0a-118">Als u een `TransportSettings` hello settings.xml bestand zonder voorvoegsel, met `FabricTransportListenerSettings` alle Hallo-instellingen in deze sectie standaard wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="57b0a-118">If you add a `TransportSettings` section in hello settings.xml file without any prefix, `FabricTransportListenerSettings` will load all hello settings from this section by default.</span></span>

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        <span data-ttu-id="57b0a-119">In dit geval Hallo `CreateServiceInstanceListeners` methode ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="57b0a-119">In this case, hello `CreateServiceInstanceListeners` method will look like this:</span></span>

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. <span data-ttu-id="57b0a-120">Wanneer u methoden aanroepen op een beveiligde service via Hallo remoting stack, in plaats van Hallo `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasse toocreate geen proxy-service, gebruik `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="57b0a-120">When you call methods on a secured service by using hello remoting stack, instead of using hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class toocreate a service proxy, use `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.</span></span>

    <span data-ttu-id="57b0a-121">Als de clientcode Hallo als onderdeel van een service wordt uitgevoerd, kunt u laden `FabricTransportSettings` uit Hallo settings.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="57b0a-121">If hello client code is running as part of a service, you can load `FabricTransportSettings` from hello settings.xml file.</span></span> <span data-ttu-id="57b0a-122">Maak een TransportSettings-sectie die vergelijkbaar toohello servicecode, zoals eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="57b0a-122">Create a TransportSettings section that is similar toohello service code, as shown earlier.</span></span> <span data-ttu-id="57b0a-123">Controleer Hallo wijzigingen toohello clientcode te volgen:</span><span class="sxs-lookup"><span data-stu-id="57b0a-123">Make hello following changes toohello client code:</span></span>

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```

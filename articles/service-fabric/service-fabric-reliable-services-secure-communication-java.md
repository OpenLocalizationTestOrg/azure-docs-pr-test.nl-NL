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
# <a name="help-secure-communication-for-services-in-azure-service-fabric"></a>Veilige communicatie van de Help voor services in Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# op Windows](service-fabric-reliable-services-secure-communication.md)
> * [Java op Linux](service-fabric-reliable-services-secure-communication-java.md)
>
>

## <a name="help-secure-a-service-when-youre-using-service-remoting"></a>Beveiligen van een service als u service voor externe toegang
We gebruiken hiervoor een bestaande [voorbeeld](service-fabric-reliable-services-communication-remoting-java.md) waarin wordt uitgelegd hoe tooset van externe toegang tot betrouwbare services. toohelp beveiligen van een service als u service voor externe toegang, wordt als volgt te werk:

1. Maken van een interface `HelloWorldStateless`, die definieert Hallo-methoden die beschikbaar zijn voor een externe procedureaanroep voor uw service. Uw service maakt gebruik van `FabricTransportServiceRemotingListener`, die is gedeclareerd in Hallo `microsoft.serviceFabric.services.remoting.fabricTransport.runtime` pakket. Dit is een `CommunicationListener` -implementatie mogelijkheden voor externe toegang biedt.

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
2. Instellingen voor listener en beveiligingsreferenties toevoegen.

    Zorg ervoor dat Hallo-certificaat dat u wilt dat toouse toohelp beveiligde die uw servicecommunicatie is geïnstalleerd op alle Hallo-knooppunten in het Hallo-cluster. Er zijn twee manieren waarop u instellingen voor listener en beveiligingsreferenties kunt opgeven:

   1. Ze bieden met behulp van een [configuratiepakket](service-fabric-application-model.md):

       Voeg een `TransportSettings` sectie in Hallo settings.xml bestand.

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

       In dit geval Hallo `createServiceInstanceListeners` methode ziet er als volgt:

       ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this, FabricTransportRemotingListenerSettings.loadFrom(HelloWorldStatelessTransportSettings));
            }));
            return listeners;
        }
       ```

        Als u een `TransportSettings` hello settings.xml bestand zonder voorvoegsel, met `FabricTransportListenerSettings` alle Hallo-instellingen in deze sectie standaard wordt geladen.

        ```xml
        <!--"TransportSettings" section without any prefix.-->
        <Section Name="TransportSettings">
            ...
        </Section>
        ```
        In dit geval Hallo `CreateServiceInstanceListeners` methode ziet er als volgt:

        ```java
        protected List<ServiceInstanceListener> createServiceInstanceListeners() {
            ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
            listeners.add(new ServiceInstanceListener((context) -> {
                return new FabricTransportServiceRemotingListener(context,this);
            }));
            return listeners;
        }
       ```
3. Wanneer u methoden aanroepen op een beveiligde service via Hallo remoting stack, in plaats van Hallo `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` klasse toocreate geen proxy-service, gebruik `microsoft.serviceFabric.services.remoting.client.FabricServiceProxyFactory`.

    Als de clientcode Hallo als onderdeel van een service wordt uitgevoerd, kunt u laden `FabricTransportSettings` uit Hallo settings.xml-bestand. Maak een TransportSettings-sectie die vergelijkbaar toohello servicecode, zoals eerder besproken. Controleer Hallo wijzigingen toohello clientcode te volgen:

    ```java

    FabricServiceProxyFactory serviceProxyFactory = new FabricServiceProxyFactory(c -> {
            return new FabricTransportServiceRemotingClientFactory(FabricTransportRemotingSettings.loadFrom("TransportPrefixTransportSettings"), null, null, null, null);
        }, null)

    HelloWorldStateless client = serviceProxyFactory.createServiceProxy(HelloWorldStateless.class,
        new URI("fabric:/MyApplication/MyHelloWorldService"));

    CompletableFuture<String> message = client.getHelloWorld();

    ```

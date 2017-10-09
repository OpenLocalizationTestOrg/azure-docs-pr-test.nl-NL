---
title: aaaAzure Service Bus WCF Relay-zelfstudie | Microsoft Docs
description: U een Service Bus-clienttoepassing en met Relay WCF-service.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 53dfd236-97f1-4778-b376-be91aa14b842
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: sethm
ms.openlocfilehash: 78cd52ef51e9fcfcda2f13ec54bde3af50d76476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-tutorial"></a><span data-ttu-id="848e8-103">Azure Relay WCF-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="848e8-103">Azure WCF Relay tutorial</span></span>

<span data-ttu-id="848e8-104">Deze zelfstudie wordt beschreven hoe toobuild een eenvoudige WCF Relay-clienttoepassing en met Azure Relay-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-104">This tutorial describes how toobuild a simple WCF Relay client application and service using Azure Relay.</span></span> <span data-ttu-id="848e8-105">Voor een vergelijkbare zelfstudie waarin [Service Bus-berichtenservice](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), Zie [aan de slag met Service Bus-wachtrijen](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="848e8-105">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="848e8-106">Het uitvoeren van deze zelfstudie hebt u een goed begrip van Hallo stappen vereist toocreate een Relay WCF-client en service-toepassing zijn.</span><span class="sxs-lookup"><span data-stu-id="848e8-106">Working through this tutorial gives you an understanding of hello steps that are required toocreate a WCF Relay client and service application.</span></span> <span data-ttu-id="848e8-107">Als de oorspronkelijke WCF is is een service een middel met een of meer eindpunten, die allemaal een of meer servicebewerkingen.</span><span class="sxs-lookup"><span data-stu-id="848e8-107">Like their original WCF counterparts, a service is a construct that exposes one or more endpoints, each of which exposes one or more service operations.</span></span> <span data-ttu-id="848e8-108">Hallo-eindpunt van een service geeft een adres waar de Hallo-service kan worden gevonden, een binding met Hallo-informatie die een client moet communiceren met de Hallo-service en een contract waarin staat Hallo functionaliteit van Hallo service tooits clients.</span><span class="sxs-lookup"><span data-stu-id="848e8-108">hello endpoint of a service specifies an address where hello service can be found, a binding that contains hello information that a client must communicate with hello service, and a contract that defines hello functionality provided by hello service tooits clients.</span></span> <span data-ttu-id="848e8-109">Hallo belangrijkste verschil tussen de WCF- en WCF Relay is dat Hallo-eindpunt wordt weergegeven in de cloud Hallo in plaats van lokaal op uw computer.</span><span class="sxs-lookup"><span data-stu-id="848e8-109">hello main difference between WCF and WCF Relay is that hello endpoint is exposed in hello cloud instead of locally on your computer.</span></span>

<span data-ttu-id="848e8-110">Als u Hallo volgorde van onderwerpen in deze zelfstudie doorloopt, hebt u een actieve service en een client die Hallo bewerkingen van Hallo service kan worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="848e8-110">After you work through hello sequence of topics in this tutorial, you will have a running service, and a client that can invoke hello operations of hello service.</span></span> <span data-ttu-id="848e8-111">Hallo eerste onderwerp wordt beschreven hoe tooset van een account.</span><span class="sxs-lookup"><span data-stu-id="848e8-111">hello first topic describes how tooset up an account.</span></span> <span data-ttu-id="848e8-112">Hallo volgende stappen wordt beschreven hoe toodefine een service die gebruikmaakt van een contract, hoe tooimplement Hallo service en hoe tooconfigure Hallo-service in code.</span><span class="sxs-lookup"><span data-stu-id="848e8-112">hello next steps describe how toodefine a service that uses a contract, how tooimplement hello service, and how tooconfigure hello service in code.</span></span> <span data-ttu-id="848e8-113">Er wordt ook beschreven hoe toohost en Voer Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-113">They also describe how toohost and run hello service.</span></span> <span data-ttu-id="848e8-114">Hallo service die is gemaakt is host zichzelf en Hallo-client en service uitgevoerd op Hallo dezelfde computer.</span><span class="sxs-lookup"><span data-stu-id="848e8-114">hello service that is created is self-hosted and hello client and service run on hello same computer.</span></span> <span data-ttu-id="848e8-115">U kunt Hallo service configureren met behulp van code of een configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="848e8-115">You can configure hello service by using either code or a configuration file.</span></span>

<span data-ttu-id="848e8-116">Hallo van de laatste drie stappen wordt beschreven hoe toocreate een clienttoepassing Hallo clienttoepassing, configureren en maken en gebruiken van een client die toegang de functionaliteit van de host Hallo Hallo tot.</span><span class="sxs-lookup"><span data-stu-id="848e8-116">hello final three steps describe how toocreate a client application, configure hello client application, and create and use a client that can access hello functionality of hello host.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="848e8-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="848e8-117">Prerequisites</span></span>

<span data-ttu-id="848e8-118">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="848e8-118">toocomplete this tutorial, you'll need hello following:</span></span>

* <span data-ttu-id="848e8-119">[Microsoft Visual Studio 2015 of hoger](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="848e8-119">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="848e8-120">Deze zelfstudie wordt Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="848e8-120">This tutorial uses Visual Studio 2017.</span></span>
* <span data-ttu-id="848e8-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="848e8-121">An active Azure account.</span></span> <span data-ttu-id="848e8-122">Als u geen Azure-account hebt, kunt u binnen een paar minuten een gratis account maken.</span><span class="sxs-lookup"><span data-stu-id="848e8-122">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="848e8-123">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/free/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="848e8-123">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="848e8-124">Een servicenaamruimte maken</span><span class="sxs-lookup"><span data-stu-id="848e8-124">Create a service namespace</span></span>

<span data-ttu-id="848e8-125">de eerste stap Hallo is toocreate een naamruimte en tooobtain een [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) sleutel.</span><span class="sxs-lookup"><span data-stu-id="848e8-125">hello first step is toocreate a namespace, and tooobtain a [Shared Access Signature (SAS)](../service-bus-messaging/service-bus-sas.md) key.</span></span> <span data-ttu-id="848e8-126">Een naamruimte biedt een toepassingsbegrenzing voor elke toepassing die toegankelijk is via Hallo relay-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-126">A namespace provides an application boundary for each application exposed through hello relay service.</span></span> <span data-ttu-id="848e8-127">Een SAS-sleutel wordt automatisch gegenereerd door Hallo systeem wanneer een Servicenaamruimte wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="848e8-127">A SAS key is automatically generated by hello system when a service namespace is created.</span></span> <span data-ttu-id="848e8-128">Hallo combinatie van Servicenaamruimte en SAS-sleutel biedt Hallo referenties voor Azure tooauthenticate toegang tooan toepassing.</span><span class="sxs-lookup"><span data-stu-id="848e8-128">hello combination of service namespace and SAS key provides hello credentials for Azure tooauthenticate access tooan application.</span></span> <span data-ttu-id="848e8-129">Ga als volgt Hallo [hier instructies](relay-create-namespace-portal.md) toocreate een Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="848e8-129">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="define-a-wcf-service-contract"></a><span data-ttu-id="848e8-130">Een WCF-servicecontract definiëren</span><span class="sxs-lookup"><span data-stu-id="848e8-130">Define a WCF service contract</span></span>

<span data-ttu-id="848e8-131">Hallo-servicecontract geeft aan welke bewerkingen (Hallo webserviceterminologie voor methoden of functies) Hallo ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="848e8-131">hello service contract specifies what operations (hello web service terminology for methods or functions) hello service supports.</span></span> <span data-ttu-id="848e8-132">Contracten worden gemaakt door een C++-, C#- of Visual Basic-interface te definiëren.</span><span class="sxs-lookup"><span data-stu-id="848e8-132">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="848e8-133">Elke methode in Hallo interface komt tooa specifieke servicebewerking overeen.</span><span class="sxs-lookup"><span data-stu-id="848e8-133">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="848e8-134">Elke interface moet hebben Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) kenmerk tooit toegepast, en elke bewerking moet Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) tooit kenmerk dat wordt toegepast.</span><span class="sxs-lookup"><span data-stu-id="848e8-134">Each interface must have hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute applied tooit, and each operation must have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute applied tooit.</span></span> <span data-ttu-id="848e8-135">Als een methode in een interface met Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) kenmerk heeft geen Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) kenmerk toe, die methode niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="848e8-135">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute, that method is not exposed.</span></span> <span data-ttu-id="848e8-136">Hallo-code voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="848e8-136">hello code for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="848e8-137">Zie voor meer informatie over contracten en services, [Services ontwerpen en implementeren](https://msdn.microsoft.com/library/ms729746.aspx) in Hallo WCF-documentatie.</span><span class="sxs-lookup"><span data-stu-id="848e8-137">For a larger discussion of contracts and services, see [Designing and Implementing Services](https://msdn.microsoft.com/library/ms729746.aspx) in hello WCF documentation.</span></span>

### <a name="create-a-relay-contract-with-an-interface"></a><span data-ttu-id="848e8-138">Een relay-contract met een interface maken</span><span class="sxs-lookup"><span data-stu-id="848e8-138">Create a relay contract with an interface</span></span>

1. <span data-ttu-id="848e8-139">Open Visual Studio als beheerder door met de rechtermuisknop op Hallo programma in Hallo **Start** menu en selecteer **als administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="848e8-139">Open Visual Studio as an administrator by right-clicking hello program in hello **Start** menu and selecting **Run as administrator**.</span></span>
2. <span data-ttu-id="848e8-140">Maak een nieuw consoletoepassingsproject aan.</span><span class="sxs-lookup"><span data-stu-id="848e8-140">Create a new console application project.</span></span> <span data-ttu-id="848e8-141">Klik op Hallo **bestand** menu en selecteer **nieuw**, klikt u vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="848e8-141">Click hello **File** menu and select **New**, then click **Project**.</span></span> <span data-ttu-id="848e8-142">In Hallo **nieuw Project** dialoogvenster, klikt u op **Visual C#** (als **Visual C#** niet wordt weergegeven, kijkt u onder **andere talen**).</span><span class="sxs-lookup"><span data-stu-id="848e8-142">In hello **New Project** dialog, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**).</span></span> <span data-ttu-id="848e8-143">Klik op Hallo **Console-App (.NET Framework)** -sjabloon en noem deze **EchoService**.</span><span class="sxs-lookup"><span data-stu-id="848e8-143">Click hello **Console App (.NET Framework)** template, and name it **EchoService**.</span></span> <span data-ttu-id="848e8-144">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="848e8-144">Click **OK** toocreate hello project.</span></span>

    ![][2]

3. <span data-ttu-id="848e8-145">Hallo Service Bus NuGet-pakketten installeren.</span><span class="sxs-lookup"><span data-stu-id="848e8-145">Install hello Service Bus NuGet package.</span></span> <span data-ttu-id="848e8-146">Dit pakket wordt automatisch toegevoegd verwijzingen toohello Service Bus-bibliotheken, evenals Hallo WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="848e8-146">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="848e8-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is Hallo-naamruimte die u tooprogrammatically toegang Hallo basisfuncties van WCF.</span><span class="sxs-lookup"><span data-stu-id="848e8-147">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables you tooprogrammatically access hello basic features of WCF.</span></span> <span data-ttu-id="848e8-148">Service Bus maakt gebruik van veel van Hallo-objecten en kenmerken van WCF toodefine servicecontracten.</span><span class="sxs-lookup"><span data-stu-id="848e8-148">Service Bus uses many of hello objects and attributes of WCF toodefine service contracts.</span></span>

    <span data-ttu-id="848e8-149">Klik in Solution Explorer met de rechtermuisknop op het Hallo-project en klik vervolgens op **NuGet-pakketten beheren...** . Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="848e8-149">In Solution Explorer, right-click hello project, and then click **Manage NuGet Packages...**. Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="848e8-150">Zorg ervoor dat projectnaam Hallo is geselecteerd in Hallo **versie (s)** vak.</span><span class="sxs-lookup"><span data-stu-id="848e8-150">Ensure that hello project name is selected in hello **Version(s)** box.</span></span> <span data-ttu-id="848e8-151">Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-151">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
4. <span data-ttu-id="848e8-152">Dubbelklik in Solution Explorer op Hallo Program.cs-bestand tooopen deze in de editor Hallo als deze nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="848e8-152">In Solution Explorer, double-click hello Program.cs file tooopen it in hello editor, if it is not already open.</span></span>
5. <span data-ttu-id="848e8-153">Voeg de volgende Hallo using-instructies Hallo boven aan het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="848e8-153">Add hello following using statements at hello top of hello file:</span></span>

    ```csharp
    using System.ServiceModel;
    using Microsoft.ServiceBus;
    ```
6. <span data-ttu-id="848e8-154">Wijziging Hallo naamruimtenaam van de standaardnaam van **EchoService** te**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="848e8-154">Change hello namespace name from its default name of **EchoService** too**Microsoft.ServiceBus.Samples**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="848e8-155">Deze zelfstudie wordt gebruikgemaakt van Hallo C#-naamruimte **Microsoft.ServiceBus.Samples**, namelijk Hallo-naamruimte van contract gebaseerde Hallo beheerde type dat wordt gebruikt in het Hallo-configuratiebestand in Hallo [configureren Hallo WCF-client](#configure-the-wcf-client) stap.</span><span class="sxs-lookup"><span data-stu-id="848e8-155">This tutorial uses hello C# namespace **Microsoft.ServiceBus.Samples**, which is hello namespace of hello contract-based managed type that is used in hello configuration file in hello [Configure hello WCF client](#configure-the-wcf-client) step.</span></span> <span data-ttu-id="848e8-156">U kunt elke gewenste naamruimte bij het maken van dit voorbeeld; opgeven Hallo-zelfstudie werkt echter niet tenzij u vervolgens Hallo naamruimten van Hallo contract en de service, in het configuratiebestand van de toepassing hello aanpassen.</span><span class="sxs-lookup"><span data-stu-id="848e8-156">You can specify any namespace you want when you build this sample; however, hello tutorial will not work unless you then modify hello namespaces of hello contract and service accordingly, in hello application configuration file.</span></span> <span data-ttu-id="848e8-157">Hallo naamruimte die is opgegeven in het App.config-bestand moet Hallo Hallo dezelfde als Hallo naamruimte die is opgegeven in de C#-bestanden.</span><span class="sxs-lookup"><span data-stu-id="848e8-157">hello namespace specified in hello App.config file must be hello same as hello namespace specified in your C# files.</span></span>
   >
   >
7. <span data-ttu-id="848e8-158">Direct na Hallo `Microsoft.ServiceBus.Samples` naamruimtedeclaratie, maar in Hallo naamruimte, definieert u een nieuwe interface met de naam `IEchoContract` en toepassing hello `ServiceContractAttribute` kenmerk toohello interface met een naamruimtewaarde van `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="848e8-158">Directly after hello `Microsoft.ServiceBus.Samples` namespace declaration, but within hello namespace, define a new interface named `IEchoContract` and apply hello `ServiceContractAttribute` attribute toohello interface with a namespace value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="848e8-159">Hallo naamruimtewaarde verschilt van Hallo-naamruimte die u gebruiken voor de hele Hallo bereik van uw code.</span><span class="sxs-lookup"><span data-stu-id="848e8-159">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="848e8-160">In plaats daarvan Hallo naamruimtewaarde gebruikt als een unieke id voor dit contract.</span><span class="sxs-lookup"><span data-stu-id="848e8-160">Instead, hello namespace value is used as a unique identifier for this contract.</span></span> <span data-ttu-id="848e8-161">Het expliciet opgeven van Hallo-naamruimte voorkomt u dat standaardnaamruimtewaarde hello toohello contractnaam wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="848e8-161">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span> <span data-ttu-id="848e8-162">Plak de code te volgen na de naamruimtedeclaratie Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="848e8-162">Paste hello following code after hello namespace declaration:</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="848e8-163">Hallo naamruimte van het servicecontract bevat meestal een schematische naam die versie-informatie bevat.</span><span class="sxs-lookup"><span data-stu-id="848e8-163">Typically, hello service contract namespace contains a naming scheme that includes version information.</span></span> <span data-ttu-id="848e8-164">Inclusief versiegegevens in de naamruimte van het servicecontract hello, kunnen services tooisolate grote wijzigingen door te definiëren van een nieuw servicecontract met een nieuwe naamruimte en het beschikbaar te maken op een nieuw eindpunt.</span><span class="sxs-lookup"><span data-stu-id="848e8-164">Including version information in hello service contract namespace enables services tooisolate major changes by defining a new service contract with a new namespace and exposing it on a new endpoint.</span></span> <span data-ttu-id="848e8-165">Op deze manier kunnen clients zonder toobe bijgewerkt toouse Hallo oude servicecontract blijven.</span><span class="sxs-lookup"><span data-stu-id="848e8-165">In this manner, clients can continue toouse hello old service contract without having toobe updated.</span></span> <span data-ttu-id="848e8-166">De versie-informatie kan bestaan uit een datum of een buildnummer.</span><span class="sxs-lookup"><span data-stu-id="848e8-166">Version information can consist of a date or a build number.</span></span> <span data-ttu-id="848e8-167">Zie [Serviceversiebeheer](http://go.microsoft.com/fwlink/?LinkID=180498) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="848e8-167">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="848e8-168">Naamgeving van schema van de servicecontractnaamruimte Hallo Hallo bevat oog op Hallo van deze zelfstudie wordt geen versie-informatie.</span><span class="sxs-lookup"><span data-stu-id="848e8-168">For hello purposes of this tutorial, hello naming scheme of hello service contract namespace does not contain version information.</span></span>
   >
   >
8. <span data-ttu-id="848e8-169">Binnen Hallo `IEchoContract` interface, declareert u een methode voor het Hallo één bewerking Hallo `IEchoContract` contract zichtbaar gemaakt in Hallo interface en toepassing hello `OperationContractAttribute` kenmerk toohello methode die u wilt dat tooexpose als onderdeel van openbare WCF Relay Hallo contract, als volgt:</span><span class="sxs-lookup"><span data-stu-id="848e8-169">Within hello `IEchoContract` interface, declare a method for hello single operation hello `IEchoContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public WCF Relay contract, as follows:</span></span>

    ```csharp
    [OperationContract]
    string Echo(string text);
    ```
9. <span data-ttu-id="848e8-170">Direct na Hallo `IEchoContract` interface definition, declareert u een kanaal dat eigenschappen van overneemt `IEchoContract` en ook toohello `IClientChannel` interface, zoals hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="848e8-170">Directly after hello `IEchoContract` interface definition, declare a channel that inherits from both `IEchoContract` and also toohello `IClientChannel` interface, as shown here:</span></span>

    ```csharp
    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```

    <span data-ttu-id="848e8-171">Een kanaal is Hallo WCF-object waarmee Hallo host en de client informatie tooeach andere doorgeven.</span><span class="sxs-lookup"><span data-stu-id="848e8-171">A channel is hello WCF object through which hello host and client pass information tooeach other.</span></span> <span data-ttu-id="848e8-172">Later schrijft u code tegen Hallo kanaal tooecho informatie tussen de twee toepassingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-172">Later, you will write code against hello channel tooecho information between hello two applications.</span></span>
10. <span data-ttu-id="848e8-173">Van Hallo **bouwen** menu, klikt u op **Build Solution** of druk op **Ctrl + Shift + B** tooconfirm Hallo juistheid van uw werk tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="848e8-173">From hello **Build** menu, click **Build Solution** or press **Ctrl+Shift+B** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="848e8-174">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="848e8-174">Example</span></span>

<span data-ttu-id="848e8-175">Hallo volgende code toont een eenvoudige interface die een Relay WCF-contract wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="848e8-175">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="848e8-176">Nu dat hello interface is gemaakt, kunt u Hallo-interface implementeren.</span><span class="sxs-lookup"><span data-stu-id="848e8-176">Now that hello interface is created, you can implement hello interface.</span></span>

## <a name="implement-hello-wcf-contract"></a><span data-ttu-id="848e8-177">Hallo WCF-contract implementeren</span><span class="sxs-lookup"><span data-stu-id="848e8-177">Implement hello WCF contract</span></span>

<span data-ttu-id="848e8-178">Maken van een Azure relay, moet eerst de Hallo-contract wordt gedefinieerd door middel van een interface te maken.</span><span class="sxs-lookup"><span data-stu-id="848e8-178">Creating an Azure relay requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="848e8-179">Zie voor meer informatie over het maken van de interface Hallo Hallo vorige stap.</span><span class="sxs-lookup"><span data-stu-id="848e8-179">For more information about creating hello interface, see hello previous step.</span></span> <span data-ttu-id="848e8-180">de volgende stap Hallo is tooimplement Hallo-interface.</span><span class="sxs-lookup"><span data-stu-id="848e8-180">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="848e8-181">Dit omvat het maken van een klasse met de naam `EchoService` die gebruiker gedefinieerde Hallo implementeert `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="848e8-181">This involves creating a class named `EchoService` that implements hello user-defined `IEchoContract` interface.</span></span> <span data-ttu-id="848e8-182">Nadat u Hallo-interface implementeert, configureert u Hallo-interface met een App.config-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="848e8-182">After you implement hello interface, you then configure hello interface using an App.config configuration file.</span></span> <span data-ttu-id="848e8-183">Hallo-configuratiebestand bevat de benodigde gegevens voor het Hallo-toepassing, zoals het Hallo-naam van Hallo-service, Hallo-naam van het Hallo-contract en Hallo type protocol dat wordt gebruikt toocommunicate met Hallo relay-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-183">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="848e8-184">Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="848e8-184">hello code used for these tasks is provided in hello example following hello procedure.</span></span> <span data-ttu-id="848e8-185">Raadpleeg voor algemene informatie over hoe een service tooimplement contract [servicecontracten implementeren](https://msdn.microsoft.com/library/ms733764.aspx) in Hallo WCF-documentatie.</span><span class="sxs-lookup"><span data-stu-id="848e8-185">For a more general discussion about how tooimplement a service contract, see [Implementing Service Contracts](https://msdn.microsoft.com/library/ms733764.aspx) in hello WCF documentation.</span></span>

1. <span data-ttu-id="848e8-186">Maak een nieuwe klasse met de naam `EchoService` direct na de definitie van Hallo Hallo `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="848e8-186">Create a new class named `EchoService` directly after hello definition of hello `IEchoContract` interface.</span></span> <span data-ttu-id="848e8-187">Hallo `EchoService` klasse implementeert Hallo `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="848e8-187">hello `EchoService` class implements hello `IEchoContract` interface.</span></span>

    ```csharp
    class EchoService : IEchoContract
    {
    }
    ```

    <span data-ttu-id="848e8-188">Vergelijkbare tooother interface-implementaties, kunt u Hallo definitie implementeren in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="848e8-188">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="848e8-189">Echter Hallo-implementatie voor deze zelfstudie bevindt zich in hetzelfde bestand als de interfacedefinitie Hallo en Hallo Hallo `Main` methode.</span><span class="sxs-lookup"><span data-stu-id="848e8-189">However, for this tutorial, hello implementation is located in hello same file as hello interface definition and hello `Main` method.</span></span>
2. <span data-ttu-id="848e8-190">Toepassing hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) toohello kenmerk `IEchoContract` interface.</span><span class="sxs-lookup"><span data-stu-id="848e8-190">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello `IEchoContract` interface.</span></span> <span data-ttu-id="848e8-191">Hallo-kenmerk geeft Hallo servicenaam en naamruimte.</span><span class="sxs-lookup"><span data-stu-id="848e8-191">hello attribute specifies hello service name and namespace.</span></span> <span data-ttu-id="848e8-192">Hierna moet u Hallo `EchoService` klasse als volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="848e8-192">After doing so, hello `EchoService` class appears as follows:</span></span>

    ```csharp
    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
    }
    ```
3. <span data-ttu-id="848e8-193">Implementeer Hallo `Echo` methode die is gedefinieerd in Hallo `IEchoContract` interface in Hallo `EchoService` klasse.</span><span class="sxs-lookup"><span data-stu-id="848e8-193">Implement hello `Echo` method defined in hello `IEchoContract` interface in hello `EchoService` class.</span></span>

    ```csharp
    public string Echo(string text)
    {
        Console.WriteLine("Echoing: {0}", text);
        return text;
    }
    ```
4. <span data-ttu-id="848e8-194">Klik op **bouwen**, klikt u vervolgens op **Build Solution** tooconfirm Hallo juistheid van uw werk.</span><span class="sxs-lookup"><span data-stu-id="848e8-194">Click **Build**, then click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="define-hello-configuration-for-hello-service-host"></a><span data-ttu-id="848e8-195">Hallo-configuratie voor Hallo ServiceHost definiëren</span><span class="sxs-lookup"><span data-stu-id="848e8-195">Define hello configuration for hello service host</span></span>

1. <span data-ttu-id="848e8-196">Hallo-configuratiebestand is heel vergelijkbaar tooa WCF-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="848e8-196">hello configuration file is very similar tooa WCF configuration file.</span></span> <span data-ttu-id="848e8-197">Het Hallo-servicenaam, eindpunt (dat wil zeggen, Hallo locatie die Azure Relay beschikbaar voor clients en hosts toocommunicate met elkaar maakt) bevat en Hallo binding (Hallo type protocol dat wordt gebruikt toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="848e8-197">It includes hello service name, endpoint (that is, hello location that Azure Relay exposes for clients and hosts toocommunicate with each other), and hello binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="848e8-198">Hallo belangrijkste verschil is dat deze geconfigureerde service-eindpunt tooa verwijst [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding die geen deel van Hallo .NET Framework uitmaakt.</span><span class="sxs-lookup"><span data-stu-id="848e8-198">hello main difference is that this configured service endpoint refers tooa [NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) binding, which is not part of hello .NET Framework.</span></span> <span data-ttu-id="848e8-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is een Hallo bindingen die is gedefinieerd door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-199">[NetTcpRelayBinding](/dotnet/api/microsoft.servicebus.nettcprelaybinding) is one of hello bindings defined by hello service.</span></span>
2. <span data-ttu-id="848e8-200">In **Solution Explorer**, dubbelklikt u op Hallo App.config-bestand tooopen in Hallo Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="848e8-200">In **Solution Explorer**, double-click hello App.config file tooopen it in hello Visual Studio editor.</span></span>
3. <span data-ttu-id="848e8-201">In Hallo `<appSettings>` element Hallo tijdelijke aanduidingen vervangen door Hallo-naam van uw Servicenaamruimte en SAS-sleutel die u in een eerdere stap hebt gekopieerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-201">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
4. <span data-ttu-id="848e8-202">Binnen Hallo `<system.serviceModel>` tags, Voeg een `<services>` element.</span><span class="sxs-lookup"><span data-stu-id="848e8-202">Within hello `<system.serviceModel>` tags, add a `<services>` element.</span></span> <span data-ttu-id="848e8-203">U kunt meerdere relay-toepassingen definiëren in een enkel configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="848e8-203">You can define multiple relay applications in a single configuration file.</span></span> <span data-ttu-id="848e8-204">In deze zelfstudie wordt er echter maar één gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="848e8-204">However, this tutorial defines only one.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <services>

        </services>
      </system.serviceModel>
    </configuration>
    ```
5. <span data-ttu-id="848e8-205">Binnen Hallo `<services>` element, Voeg een `<service>` toodefine Hallo elementnaam Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-205">Within hello `<services>` element, add a `<service>` element toodefine hello name of hello service.</span></span>

    ```xml
    <service name="Microsoft.ServiceBus.Samples.EchoService">
    </service>
    ```
6. <span data-ttu-id="848e8-206">Binnen Hallo `<service>` element Hallo-locatie van het contract Hallo-eindpunt te definiëren en ook Hallo type van de binding voor het Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="848e8-206">Within hello `<service>` element, define hello location of hello endpoint contract, and also hello type of binding for hello endpoint.</span></span>

    ```xml
    <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="848e8-207">Hallo-eindpunt definieert waar Hallo client zoekt naar de hosttoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-207">hello endpoint defines where hello client will look for hello host application.</span></span> <span data-ttu-id="848e8-208">Later, Hallo zelfstudie maakt gebruik van deze stap toocreate een URI die volledig Hallo host via Azure Relay beschrijft.</span><span class="sxs-lookup"><span data-stu-id="848e8-208">Later, hello tutorial uses this step toocreate a URI that fully exposes hello host through Azure Relay.</span></span> <span data-ttu-id="848e8-209">Hallo binding weet u dat we TCP gebruiken zoals Hallo protocol toocommunicate met Hallo relay-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-209">hello binding declares that we are using TCP as hello protocol toocommunicate with hello relay service.</span></span>
7. <span data-ttu-id="848e8-210">Van Hallo **bouwen** menu, klikt u op **Build Solution** tooconfirm Hallo juistheid van uw werk.</span><span class="sxs-lookup"><span data-stu-id="848e8-210">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work.</span></span>

### <a name="example"></a><span data-ttu-id="848e8-211">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="848e8-211">Example</span></span>

<span data-ttu-id="848e8-212">Hallo toont volgende code Hallo-implementatie van het servicecontract Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-212">hello following code shows hello implementation of hello service contract.</span></span>

```csharp
[ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]

    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }
```

<span data-ttu-id="848e8-213">Hallo toont volgende code basisindeling van Hallo App.config-bestand die is gekoppeld aan de ServiceHost Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-213">hello following code shows hello basic format of hello App.config file associated with hello service host.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <services>
      <service name="Microsoft.ServiceBus.Samples.EchoService">
        <endpoint contract="Microsoft.ServiceBus.Samples.IEchoContract" binding="netTcpRelayBinding" />
      </service>
    </services>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="host-and-run-a-basic-web-service-tooregister-with-hello-relay-service"></a><span data-ttu-id="848e8-214">Hosten en uitvoeren van een eenvoudige web service tooregister met Hallo relay-service</span><span class="sxs-lookup"><span data-stu-id="848e8-214">Host and run a basic web service tooregister with hello relay service</span></span>

<span data-ttu-id="848e8-215">Deze stap wordt beschreven hoe toorun een Azure Relay-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-215">This step describes how toorun an Azure Relay service.</span></span>

### <a name="create-hello-relay-credentials"></a><span data-ttu-id="848e8-216">Hallo relay referenties maken</span><span class="sxs-lookup"><span data-stu-id="848e8-216">Create hello relay credentials</span></span>

1. <span data-ttu-id="848e8-217">In `Main()`, maakt u twee variabelen in welke toostore Hallo-naamruimte en SAS-sleutel die worden gelezen vanuit het consolevenster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-217">In `Main()`, create two variables in which toostore hello namespace and hello SAS key that are read from hello console window.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS key: ");
    string sasKey = Console.ReadLine();
    ```

    <span data-ttu-id="848e8-218">Hallo SAS-sleutel zijn gebruikte hoger tooaccess uw project.</span><span class="sxs-lookup"><span data-stu-id="848e8-218">hello SAS key will be used later tooaccess your project.</span></span> <span data-ttu-id="848e8-219">Hallo-naamruimte is doorgegeven als parameter te`CreateServiceUri` toocreate een service-URI.</span><span class="sxs-lookup"><span data-stu-id="848e8-219">hello namespace is passed as a parameter too`CreateServiceUri` toocreate a service URI.</span></span>
2. <span data-ttu-id="848e8-220">Met behulp van een [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, dat u gebruikmaakt van een SAS-sleutel als referentietype Hallo declareren.</span><span class="sxs-lookup"><span data-stu-id="848e8-220">Using a [TransportClientEndpointBehavior](/dotnet/api/microsoft.servicebus.transportclientendpointbehavior) object, declare that you will be using a SAS key as hello credential type.</span></span> <span data-ttu-id="848e8-221">Hallo volgende code direct na Hallo-code toegevoegd in de laatste stap Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="848e8-221">Add hello following code directly after hello code added in hello last step.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```

### <a name="create-a-base-address-for-hello-service"></a><span data-ttu-id="848e8-222">Een basisadres voor Hallo service maken</span><span class="sxs-lookup"><span data-stu-id="848e8-222">Create a base address for hello service</span></span>

<span data-ttu-id="848e8-223">Nadat u hebt toegevoegd in de laatste stap Hallo Hallo code maakt een `Uri` exemplaar voor het basisadres Hallo van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-223">After hello code you added in hello last step, create a `Uri` instance for hello base address of hello service.</span></span> <span data-ttu-id="848e8-224">Deze URI bevat Hallo Service Bus-schema, Hallo-naamruimte en het pad Hallo van Hallo service-interface.</span><span class="sxs-lookup"><span data-stu-id="848e8-224">This URI specifies hello Service Bus scheme, hello namespace, and hello path of hello service interface.</span></span>

```csharp
Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
```

<span data-ttu-id="848e8-225">'sb' is een afkorting van Hallo Service Bus-schema en geeft aan dat we TCP als protocol hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="848e8-225">"sb" is an abbreviation for hello Service Bus scheme, and indicates that we are using TCP as hello protocol.</span></span> <span data-ttu-id="848e8-226">Dit is ook eerder aangegeven in het configuratiebestand hello, wanneer [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) als Hallo-binding is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="848e8-226">This was also previously indicated in hello configuration file, when [NetTcpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.nettcprelaybinding.aspx) was specified as hello binding.</span></span>

<span data-ttu-id="848e8-227">Voor deze zelfstudie Hallo-URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span><span class="sxs-lookup"><span data-stu-id="848e8-227">For this tutorial, hello URI is `sb://putServiceNamespaceHere.windows.net/EchoService`.</span></span>

### <a name="create-and-configure-hello-service-host"></a><span data-ttu-id="848e8-228">Maken en configureren van ServiceHost Hallo</span><span class="sxs-lookup"><span data-stu-id="848e8-228">Create and configure hello service host</span></span>

1. <span data-ttu-id="848e8-229">Stel de connectiviteitsmodus Hallo in te`AutoDetect`.</span><span class="sxs-lookup"><span data-stu-id="848e8-229">Set hello connectivity mode too`AutoDetect`.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```

    <span data-ttu-id="848e8-230">Hallo connectiviteitsmodus beschrijft Hallo protocol Hallo-service gebruikt toocommunicate met Hallo relay-service; via HTTP of TCP.</span><span class="sxs-lookup"><span data-stu-id="848e8-230">hello connectivity mode describes hello protocol hello service uses toocommunicate with hello relay service; either HTTP or TCP.</span></span> <span data-ttu-id="848e8-231">Met behulp van de standaardinstelling Hallo `AutoDetect`, Hallo-service probeert tooconnect tooAzure Relay via TCP als deze beschikbaar is en HTTP als TCP niet beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="848e8-231">Using hello default setting `AutoDetect`, hello service attempts tooconnect tooAzure Relay over TCP if it is available, and HTTP if TCP is not available.</span></span> <span data-ttu-id="848e8-232">Dit wijkt af van de protocolservice Hallo Hallo opmerking opgeeft voor clientcommunicatie.</span><span class="sxs-lookup"><span data-stu-id="848e8-232">Note that this differs from hello protocol hello service specifies for client communication.</span></span> <span data-ttu-id="848e8-233">Dat protocol wordt bepaald door het Hallo-binding die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="848e8-233">That protocol is determined by hello binding used.</span></span> <span data-ttu-id="848e8-234">Bijvoorbeeld, een service kunt Hallo [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding die aangeeft dat het eindpunt met clients via HTTP communiceert.</span><span class="sxs-lookup"><span data-stu-id="848e8-234">For example, a service can use hello [BasicHttpRelayBinding](https://msdn.microsoft.com/library/microsoft.servicebus.basichttprelaybinding.aspx) binding, which specifies that its endpoint communicates with clients over HTTP.</span></span> <span data-ttu-id="848e8-235">Die dezelfde service kan opgeeft **ConnectivityMode.AutoDetect** zodat Hallo service met Azure Relay via TCP communiceert.</span><span class="sxs-lookup"><span data-stu-id="848e8-235">That same service could specify **ConnectivityMode.AutoDetect** so that hello service communicates with Azure Relay over TCP.</span></span>
2. <span data-ttu-id="848e8-236">Hallo ServiceHost, met behulp van Hallo die URI eerder hebt gemaakt in deze sectie maken.</span><span class="sxs-lookup"><span data-stu-id="848e8-236">Create hello service host, using hello URI created earlier in this section.</span></span>

    ```csharp
    ServiceHost host = new ServiceHost(typeof(EchoService), address);
    ```

    <span data-ttu-id="848e8-237">Hallo ServiceHost is Hallo WCF-object dat Hallo-service instantieert.</span><span class="sxs-lookup"><span data-stu-id="848e8-237">hello service host is hello WCF object that instantiates hello service.</span></span> <span data-ttu-id="848e8-238">Hier kunt u geeft hieraan Hallo type service dat u wilt dat toocreate (een `EchoService` type), en ook toohello adres waarmee u wilt dat tooexpose Hallo service.</span><span class="sxs-lookup"><span data-stu-id="848e8-238">Here, you pass it hello type of service you want toocreate (an `EchoService` type), and also toohello address at which you want tooexpose hello service.</span></span>
3. <span data-ttu-id="848e8-239">Toevoegen aan de bovenkant van de Hallo van het bestand Program.cs hello, verwijzingen te[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) en [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span><span class="sxs-lookup"><span data-stu-id="848e8-239">At hello top of hello Program.cs file, add references too[System.ServiceModel.Description](https://msdn.microsoft.com/library/system.servicemodel.description.aspx) and [Microsoft.ServiceBus.Description](/dotnet/api/microsoft.servicebus.description).</span></span>

    ```csharp
    using System.ServiceModel.Description;
    using Microsoft.ServiceBus.Description;
    ```
4. <span data-ttu-id="848e8-240">Terug in de `Main()`, Hallo eindpunt tooenable openbare toegang configureren.</span><span class="sxs-lookup"><span data-stu-id="848e8-240">Back in `Main()`, configure hello endpoint tooenable public access.</span></span>

    ```csharp
    IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);
    ```

    <span data-ttu-id="848e8-241">Deze stap informeert Hallo relay-service dat uw toepassing openbaar vinden is te door Hallo ATOM-feed voor uw project in.</span><span class="sxs-lookup"><span data-stu-id="848e8-241">This step informs hello relay service that your application can be found publicly by examining hello ATOM feed for your project.</span></span> <span data-ttu-id="848e8-242">Als u instelt **DiscoveryType** te**persoonlijke**, een client zou kunnen tooaccess Hallo service nog steeds zijn.</span><span class="sxs-lookup"><span data-stu-id="848e8-242">If you set **DiscoveryType** too**private**, a client would still be able tooaccess hello service.</span></span> <span data-ttu-id="848e8-243">Hallo service zou niet weergegeven bij het zoeken Hallo Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="848e8-243">However, hello service would not appear when it searches hello Relay namespace.</span></span> <span data-ttu-id="848e8-244">In plaats daarvan heeft Hallo-client tooknow hello eindpuntpad tevoren.</span><span class="sxs-lookup"><span data-stu-id="848e8-244">Instead, hello client would have tooknow hello endpoint path beforehand.</span></span>
5. <span data-ttu-id="848e8-245">Toepassing hello service referenties toohello service-eindpunten gedefinieerd in Hallo App.config-bestand:</span><span class="sxs-lookup"><span data-stu-id="848e8-245">Apply hello service credentials toohello service endpoints defined in hello App.config file:</span></span>

    ```csharp
    foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
    {
        endpoint.Behaviors.Add(serviceRegistrySettings);
        endpoint.Behaviors.Add(sasCredential);
    }
    ```

    <span data-ttu-id="848e8-246">Zoals vermeld in de vorige stap hello, kan u hebt gedeclareerd meerdere services en eindpunten in het Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="848e8-246">As stated in hello previous step, you could have declared multiple services and endpoints in hello configuration file.</span></span> <span data-ttu-id="848e8-247">Als u had deze code zou passeren Hallo-configuratiebestand en de zoekcriteria voor elk eindpunt toowhich uw referenties kunnen worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="848e8-247">If you had, this code would traverse hello configuration file and search for every endpoint toowhich it should apply your credentials.</span></span> <span data-ttu-id="848e8-248">Voor deze zelfstudie heeft Hallo configuratiebestand echter slechts één eindpunt.</span><span class="sxs-lookup"><span data-stu-id="848e8-248">However, for this tutorial, hello configuration file has only one endpoint.</span></span>

### <a name="open-hello-service-host"></a><span data-ttu-id="848e8-249">De ServiceHost openen Hallo</span><span class="sxs-lookup"><span data-stu-id="848e8-249">Open hello service host</span></span>

1. <span data-ttu-id="848e8-250">Hallo-service openen.</span><span class="sxs-lookup"><span data-stu-id="848e8-250">Open hello service.</span></span>

    ```csharp
    host.Open();
    ```
2. <span data-ttu-id="848e8-251">Kennis Hallo-gebruiker die het Hallo-service wordt uitgevoerd en wordt uitgelegd hoe tooshut Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-251">Inform hello user that hello service is running, and explain how tooshut down hello service.</span></span>

    ```csharp
    Console.WriteLine("Service address: " + address);
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="848e8-252">Wanneer u klaar bent, sluit u Hallo ServiceHost.</span><span class="sxs-lookup"><span data-stu-id="848e8-252">When finished, close hello service host.</span></span>

    ```csharp
    host.Close();
    ```
4. <span data-ttu-id="848e8-253">Druk op **Ctrl + Shift + B** toobuild Hallo project.</span><span class="sxs-lookup"><span data-stu-id="848e8-253">Press **Ctrl+Shift+B** toobuild hello project.</span></span>

### <a name="example"></a><span data-ttu-id="848e8-254">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="848e8-254">Example</span></span>

<span data-ttu-id="848e8-255">Uw servicecode voltooide ziet er als volgt.</span><span class="sxs-lookup"><span data-stu-id="848e8-255">Your completed service code should appear as follows.</span></span> <span data-ttu-id="848e8-256">Hallo-code bevat Hallo servicecontract en de implementatie uit de vorige stappen in de zelfstudie Hallo en hosts Hallo service in een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="848e8-256">hello code includes hello service contract and implementation from previous steps in hello tutorial, and hosts hello service in a console application.</span></span>

```csharp
using System;
using System.ServiceModel;
using System.ServiceModel.Description;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Description;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { };

    [ServiceBehavior(Name = "EchoService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class EchoService : IEchoContract
    {
        public string Echo(string text)
        {
            Console.WriteLine("Echoing: {0}", text);
            return text;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {

            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;         

            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS key: ");
            string sasKey = Console.ReadLine();

           // Create hello credentials object for hello endpoint.
            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            // Create hello service URI based on hello service namespace.
            Uri address = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            // Create hello service host reading hello configuration.
            ServiceHost host = new ServiceHost(typeof(EchoService), address);

            // Create hello ServiceRegistrySettings behavior for hello endpoint.
            IEndpointBehavior serviceRegistrySettings = new ServiceRegistrySettings(DiscoveryType.Public);

            // Add hello Relay credentials tooall endpoints specified in configuration.
            foreach (ServiceEndpoint endpoint in host.Description.Endpoints)
            {
                endpoint.Behaviors.Add(serviceRegistrySettings);
                endpoint.Behaviors.Add(sasCredential);
            }

            // Open hello service.
            host.Open();

            Console.WriteLine("Service address: " + address);
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            // Close hello service.
            host.Close();
        }
    }
}
```

## <a name="create-a-wcf-client-for-hello-service-contract"></a><span data-ttu-id="848e8-257">Maak een WCF-client voor servicecontract Hallo</span><span class="sxs-lookup"><span data-stu-id="848e8-257">Create a WCF client for hello service contract</span></span>

<span data-ttu-id="848e8-258">de volgende stap Hallo toocreate een clienttoepassing en definiëren Hallo servicecontract u in latere stappen gaat implementeren.</span><span class="sxs-lookup"><span data-stu-id="848e8-258">hello next step is toocreate a client application and define hello service contract you will implement in later steps.</span></span> <span data-ttu-id="848e8-259">Veel van deze stappen lijken op Hallo stappen gebruikt een service toocreate: een contract, bewerkt een App.config-bestand, met behulp van referenties tooconnect toohello relay-service, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="848e8-259">Note that many of these steps resemble hello steps used toocreate a service: defining a contract, editing an App.config file, using credentials tooconnect toohello relay service, and so on.</span></span> <span data-ttu-id="848e8-260">Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="848e8-260">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="848e8-261">Maak een nieuw project in de huidige Visual Studio-oplossing Hallo voor Hallo client door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="848e8-261">Create a new project in hello current Visual Studio solution for hello client by doing hello following:</span></span>

   1. <span data-ttu-id="848e8-262">Klik in Solution Explorer in Hallo oplossing die Hallo service bevat, met de rechtermuisknop op Hallo huidige oplossing (niet Hallo project) en klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="848e8-262">In Solution Explorer, in hello same solution that contains hello service, right-click hello current solution (not hello project), and click **Add**.</span></span> <span data-ttu-id="848e8-263">Klik vervolgens op **Nieuw project**.</span><span class="sxs-lookup"><span data-stu-id="848e8-263">Then click **New Project**.</span></span>
   2. <span data-ttu-id="848e8-264">In Hallo **Add New Project** in het dialoogvenster, klikt u op **Visual C#** (als **Visual C#** niet wordt weergegeven, kijkt u onder **andere talen**), selecteer Hallo **Console-App (.NET Framework)** -sjabloon en noem deze **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="848e8-264">In hello **Add New Project** dialog box, click **Visual C#** (if **Visual C#** does not appear, look under **Other Languages**), select hello **Console App (.NET Framework)** template, and name it **EchoClient**.</span></span>
   3. <span data-ttu-id="848e8-265">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="848e8-265">Click **OK**.</span></span>
      <br />
2. <span data-ttu-id="848e8-266">Dubbelklik in Solution Explorer op Hallo het bestand Program.cs in Hallo **EchoClient** project tooopen deze in de editor Hallo als deze nog niet is geopend.</span><span class="sxs-lookup"><span data-stu-id="848e8-266">In Solution Explorer, double-click hello Program.cs file in hello **EchoClient** project tooopen it in hello editor, if it is not already open.</span></span>
3. <span data-ttu-id="848e8-267">Wijziging Hallo naamruimtenaam van de standaardnaam van `EchoClient` te`Microsoft.ServiceBus.Samples`.</span><span class="sxs-lookup"><span data-stu-id="848e8-267">Change hello namespace name from its default name of `EchoClient` too`Microsoft.ServiceBus.Samples`.</span></span>
4. <span data-ttu-id="848e8-268">Hallo installeren [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus): Klik in Solution Explorer met de rechtermuisknop op Hallo **EchoClient** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="848e8-268">Install hello [Service Bus NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus): in Solution Explorer, right-click hello **EchoClient** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="848e8-269">Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="848e8-269">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="848e8-270">Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-270">Click **Install**, and accept hello terms of use.</span></span>

    ![][3]
5. <span data-ttu-id="848e8-271">Voeg een `using` -instructie voor Hallo [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) naamruimte in het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-271">Add a `using` statement for hello [System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) namespace in hello Program.cs file.</span></span>

    ```csharp
    using System.ServiceModel;
    ```
6. <span data-ttu-id="848e8-272">Hallo definitie toohello servicecontractnaamruimte, zoals wordt weergegeven in het volgende voorbeeld Hallo toevoegen</span><span class="sxs-lookup"><span data-stu-id="848e8-272">Add hello service contract definition toohello namespace, as shown in hello following example.</span></span> <span data-ttu-id="848e8-273">Houd er rekening mee dat deze definitie identiek toohello definitie gebruikt in Hallo is **Service** project.</span><span class="sxs-lookup"><span data-stu-id="848e8-273">Note that this definition is identical toohello definition used in hello **Service** project.</span></span> <span data-ttu-id="848e8-274">U moet deze code toevoegen boven Hallo Hallo `Microsoft.ServiceBus.Samples` naamruimte.</span><span class="sxs-lookup"><span data-stu-id="848e8-274">You should add this code at hello top of hello `Microsoft.ServiceBus.Samples` namespace.</span></span>

    ```csharp
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }
    ```
7. <span data-ttu-id="848e8-275">Druk op **Ctrl + Shift + B** toobuild Hallo-client.</span><span class="sxs-lookup"><span data-stu-id="848e8-275">Press **Ctrl+Shift+B** toobuild hello client.</span></span>

### <a name="example"></a><span data-ttu-id="848e8-276">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="848e8-276">Example</span></span>

<span data-ttu-id="848e8-277">Hallo volgende code toont Hallo huidige status van het bestand Program.cs Hallo in Hallo **EchoClient** project.</span><span class="sxs-lookup"><span data-stu-id="848e8-277">hello following code shows hello current status of hello Program.cs file in hello **EchoClient** project.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        string Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }


    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="configure-hello-wcf-client"></a><span data-ttu-id="848e8-278">Hallo WCF-client configureren</span><span class="sxs-lookup"><span data-stu-id="848e8-278">Configure hello WCF client</span></span>

<span data-ttu-id="848e8-279">In deze stap maakt u een App.config-bestand voor een eenvoudige clienttoepassing die toegang heeft tot Hallo service eerder hebt gemaakt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="848e8-279">In this step, you create an App.config file for a basic client application that accesses hello service created previously in this tutorial.</span></span> <span data-ttu-id="848e8-280">Dit App.config-bestand definieert Hallo contract, binding en de naam van het Hallo-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="848e8-280">This App.config file defines hello contract, binding, and name of hello endpoint.</span></span> <span data-ttu-id="848e8-281">Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="848e8-281">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

1. <span data-ttu-id="848e8-282">Klik in Solution Explorer in Hallo **EchoClient** project, dubbelklikt u op **App.config** tooopen Hallo-bestand in Visual Studio-editor Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-282">In Solution Explorer, in hello **EchoClient** project, double-click **App.config** tooopen hello file in hello Visual Studio editor.</span></span>
2. <span data-ttu-id="848e8-283">In Hallo `<appSettings>` element Hallo tijdelijke aanduidingen vervangen door Hallo-naam van uw Servicenaamruimte en SAS-sleutel die u in een eerdere stap hebt gekopieerd Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-283">In hello `<appSettings>` element, replace hello placeholders with hello name of your service namespace, and hello SAS key that you copied in an earlier step.</span></span>
3. <span data-ttu-id="848e8-284">Binnen het element system.serviceModel Hallo toevoegen een `<client>` element.</span><span class="sxs-lookup"><span data-stu-id="848e8-284">Within hello system.serviceModel element, add a `<client>` element.</span></span>

    ```xml
    <?xmlversion="1.0"encoding="utf-8"?>
    <configuration>
      <system.serviceModel>
        <client>
        </client>
      </system.serviceModel>
    </configuration>
    ```

    <span data-ttu-id="848e8-285">Tijdens deze stap wordt aangegeven dat u een clienttoepassing van het type WCF maakt.</span><span class="sxs-lookup"><span data-stu-id="848e8-285">This step declares that you are defining a WCF-style client application.</span></span>
4. <span data-ttu-id="848e8-286">Binnen Hallo `client` element Hallo-naam, contract en bindingstype voor Hallo eindpunt definiëren.</span><span class="sxs-lookup"><span data-stu-id="848e8-286">Within hello `client` element, define hello name, contract, and binding type for hello endpoint.</span></span>

    ```xml
    <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IEchoContract"
                    binding="netTcpRelayBinding"/>
    ```

    <span data-ttu-id="848e8-287">Deze stap definieert Hallo-naam van eindpunt hello, Hallo contract gedefinieerd in het Hallo-service en Hallo feit die Hallo clienttoepassing TCP toocommunicate met Azure Relay gebruikt.</span><span class="sxs-lookup"><span data-stu-id="848e8-287">This step defines hello name of hello endpoint, hello contract defined in hello service, and hello fact that hello client application uses TCP toocommunicate with Azure Relay.</span></span> <span data-ttu-id="848e8-288">Hallo eindpuntnaam wordt gebruikt in Hallo volgende stap toolink deze eindpuntconfiguratie met Hallo service-URI.</span><span class="sxs-lookup"><span data-stu-id="848e8-288">hello endpoint name is used in hello next step toolink this endpoint configuration with hello service URI.</span></span>
5. <span data-ttu-id="848e8-289">Klik op **bestand**, klikt u vervolgens op **Alles opslaan**.</span><span class="sxs-lookup"><span data-stu-id="848e8-289">Click **File**, then click **Save All**.</span></span>

## <a name="example"></a><span data-ttu-id="848e8-290">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="848e8-290">Example</span></span>

<span data-ttu-id="848e8-291">Hallo toont volgende code Hallo App.config-bestand voor Hallo Echo-client.</span><span class="sxs-lookup"><span data-stu-id="848e8-291">hello following code shows hello App.config file for hello Echo client.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <client>
      <endpoint name="RelayEndpoint"
                      contract="Microsoft.ServiceBus.Samples.IEchoContract"
                      binding="netTcpRelayBinding"/>
    </client>
    <extensions>
      <bindingExtensions>
        <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
      </bindingExtensions>
    </extensions>
  </system.serviceModel>
</configuration>
```

## <a name="implement-hello-wcf-client"></a><span data-ttu-id="848e8-292">Hallo WCF-client implementeren</span><span class="sxs-lookup"><span data-stu-id="848e8-292">Implement hello WCF client</span></span>
<span data-ttu-id="848e8-293">In deze stap maakt implementeren u een eenvoudige clienttoepassing die u eerder hebt gemaakt in deze zelfstudie Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-293">In this step, you implement a basic client application that accesses hello service you created previously in this tutorial.</span></span> <span data-ttu-id="848e8-294">Vergelijkbare toohello service, Hallo client voeren veel van Hallo dezelfde bewerkingen tooaccess Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="848e8-294">Similar toohello service, hello client performs many of hello same operations tooaccess Azure Relay:</span></span>

1. <span data-ttu-id="848e8-295">Sets Hallo connectiviteitsmodus.</span><span class="sxs-lookup"><span data-stu-id="848e8-295">Sets hello connectivity mode.</span></span>
2. <span data-ttu-id="848e8-296">Hallo URI die u Hallo host-service zoekt maakt.</span><span class="sxs-lookup"><span data-stu-id="848e8-296">Creates hello URI that locates hello host service.</span></span>
3. <span data-ttu-id="848e8-297">Hallo beveiligingsreferenties definieert.</span><span class="sxs-lookup"><span data-stu-id="848e8-297">Defines hello security credentials.</span></span>
4. <span data-ttu-id="848e8-298">Van toepassing hello referenties toohello verbinding.</span><span class="sxs-lookup"><span data-stu-id="848e8-298">Applies hello credentials toohello connection.</span></span>
5. <span data-ttu-id="848e8-299">Hallo-verbinding wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="848e8-299">Opens hello connection.</span></span>
6. <span data-ttu-id="848e8-300">Hallo toepassingsspecifieke taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="848e8-300">Performs hello application-specific tasks.</span></span>
7. <span data-ttu-id="848e8-301">Hallo-verbinding gesloten.</span><span class="sxs-lookup"><span data-stu-id="848e8-301">Closes hello connection.</span></span>

<span data-ttu-id="848e8-302">Een van de belangrijkste verschillen Hallo is echter dat Hallo-clienttoepassing gebruikmaakt van een kanaal tooconnect toohello relay-service dat het Hallo-service gebruikt een gesprek te**ServiceHost**.</span><span class="sxs-lookup"><span data-stu-id="848e8-302">However, one of hello main differences is that hello client application uses a channel tooconnect toohello relay service, whereas hello service uses a call too**ServiceHost**.</span></span> <span data-ttu-id="848e8-303">Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="848e8-303">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

### <a name="implement-a-client-application"></a><span data-ttu-id="848e8-304">Een clienttoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="848e8-304">Implement a client application</span></span>
1. <span data-ttu-id="848e8-305">Stel de connectiviteitsmodus Hallo in te**AutoDetect**.</span><span class="sxs-lookup"><span data-stu-id="848e8-305">Set hello connectivity mode too**AutoDetect**.</span></span> <span data-ttu-id="848e8-306">Toevoegen van de volgende code in Hallo Hallo `Main()` methode Hallo **EchoClient** toepassing.</span><span class="sxs-lookup"><span data-stu-id="848e8-306">Add hello following code inside hello `Main()` method of hello **EchoClient** application.</span></span>

    ```csharp
    ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;
    ```
2. <span data-ttu-id="848e8-307">Variabelen toohold Hallo waarden opgeven voor het Hallo-Servicenaamruimte en SAS-sleutel die in de console Hallo worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="848e8-307">Define variables toohold hello values for hello service namespace, and SAS key that are read from hello console.</span></span>

    ```csharp
    Console.Write("Your Service Namespace: ");
    string serviceNamespace = Console.ReadLine();
    Console.Write("Your SAS Key: ");
    string sasKey = Console.ReadLine();
    ```
3. <span data-ttu-id="848e8-308">Hallo URI die Hallo-locatie van Hallo host in uw Relay-project definieert maken.</span><span class="sxs-lookup"><span data-stu-id="848e8-308">Create hello URI that defines hello location of hello host in your Relay project.</span></span>

    ```csharp
    Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");
    ```
4. <span data-ttu-id="848e8-309">Hallo-referentieobject voor het eindpunt van uw Servicenaamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="848e8-309">Create hello credential object for your service namespace endpoint.</span></span>

    ```csharp
    TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
    sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);
    ```
5. <span data-ttu-id="848e8-310">Maak Hallo kanaal-factory waarin wordt beschreven in de bestand App.config Hallo Hallo-configuratie wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="848e8-310">Create hello channel factory that loads hello configuration described in hello App.config file.</span></span>

    ```csharp
    ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));
    ```

    <span data-ttu-id="848e8-311">Een kanaalfactory is een WCF-object dat wordt gemaakt van een kanaal dat Hallo-service en clienttoepassingen communiceren.</span><span class="sxs-lookup"><span data-stu-id="848e8-311">A channel factory is a WCF object that creates a channel through which hello service and client applications communicate.</span></span>
6. <span data-ttu-id="848e8-312">Hallo-referenties zijn van toepassing.</span><span class="sxs-lookup"><span data-stu-id="848e8-312">Apply hello credentials.</span></span>

    ```csharp
    channelFactory.Endpoint.Behaviors.Add(sasCredential);
    ```
7. <span data-ttu-id="848e8-313">Maak en open Hallo kanaal toohello-service.</span><span class="sxs-lookup"><span data-stu-id="848e8-313">Create and open hello channel toohello service.</span></span>

    ```csharp
    IEchoChannel channel = channelFactory.CreateChannel();
    channel.Open();
    ```
8. <span data-ttu-id="848e8-314">Schrijf Hallo algemene gebruikersinterface en functionaliteit voor Hallo echo.</span><span class="sxs-lookup"><span data-stu-id="848e8-314">Write hello basic user interface and functionality for hello echo.</span></span>

    ```csharp
    Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
    string input = Console.ReadLine();
    while (input != String.Empty)
    {
        try
        {
            Console.WriteLine("Server echoed: {0}", channel.Echo(input));
        }
        catch (Exception e)
        {
            Console.WriteLine("Error: " + e.Message);
        }
        input = Console.ReadLine();
    }
    ```

    <span data-ttu-id="848e8-315">Houd er rekening mee dat Hallo code Hallo exemplaar van Hallo kanaalobject als proxy voor Hallo-service gebruikt.</span><span class="sxs-lookup"><span data-stu-id="848e8-315">Note that hello code uses hello instance of hello channel object as a proxy for hello service.</span></span>
9. <span data-ttu-id="848e8-316">Sluit Hallo kanaal en sluit Hallo factory.</span><span class="sxs-lookup"><span data-stu-id="848e8-316">Close hello channel, and close hello factory.</span></span>

    ```csharp
    channel.Close();
    channelFactory.Close();
    ```

## <a name="example"></a><span data-ttu-id="848e8-317">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="848e8-317">Example</span></span>

<span data-ttu-id="848e8-318">De volledige code ziet er als volgt die weergeeft hoe toocreate een clienttoepassing, hoe toocall Hallo bewerkingen van het Hallo-service en hoe tooclose client Hallo na Hallo bewerking aanroepen is voltooid.</span><span class="sxs-lookup"><span data-stu-id="848e8-318">Your completed code should appear as follows, showing how toocreate a client application, how toocall hello operations of hello service, and how tooclose hello client after hello operation call is finished.</span></span>

```csharp
using System;
using Microsoft.ServiceBus;
using System.ServiceModel;

namespace Microsoft.ServiceBus.Samples
{
    [ServiceContract(Name = "IEchoContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IEchoContract
    {
        [OperationContract]
        String Echo(string text);
    }

    public interface IEchoChannel : IEchoContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
            ServiceBusEnvironment.SystemConnectivity.Mode = ConnectivityMode.AutoDetect;


            Console.Write("Your Service Namespace: ");
            string serviceNamespace = Console.ReadLine();
            Console.Write("Your SAS Key: ");
            string sasKey = Console.ReadLine();



            Uri serviceUri = ServiceBusEnvironment.CreateServiceUri("sb", serviceNamespace, "EchoService");

            TransportClientEndpointBehavior sasCredential = new TransportClientEndpointBehavior();
            sasCredential.TokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider("RootManageSharedAccessKey", sasKey);

            ChannelFactory<IEchoChannel> channelFactory = new ChannelFactory<IEchoChannel>("RelayEndpoint", new EndpointAddress(serviceUri));

            channelFactory.Endpoint.Behaviors.Add(sasCredential);

            IEchoChannel channel = channelFactory.CreateChannel();
            channel.Open();

            Console.WriteLine("Enter text tooecho (or [Enter] tooexit):");
            string input = Console.ReadLine();
            while (input != String.Empty)
            {
                try
                {
                    Console.WriteLine("Server echoed: {0}", channel.Echo(input));
                }
                catch (Exception e)
                {
                    Console.WriteLine("Error: " + e.Message);
                }
                input = Console.ReadLine();
            }

            channel.Close();
            channelFactory.Close();

        }
    }
}
```

## <a name="run-hello-applications"></a><span data-ttu-id="848e8-319">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="848e8-319">Run hello applications</span></span>

1. <span data-ttu-id="848e8-320">Druk op **Ctrl + Shift + B** toobuild Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="848e8-320">Press **Ctrl+Shift+B** toobuild hello solution.</span></span> <span data-ttu-id="848e8-321">Dit bouwt zowel het clientproject hello en Hallo-serviceproject dat u hebt gemaakt in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-321">This builds both hello client project and hello service project that you created in hello previous steps.</span></span>
2. <span data-ttu-id="848e8-322">Voordat u actieve Hallo clienttoepassing, moet u ervoor zorgen dat Hallo-servicetoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="848e8-322">Before running hello client application, you must make sure that hello service application is running.</span></span> <span data-ttu-id="848e8-323">Klik in Solution Explorer in Visual Studio met de rechtermuisknop op Hallo **EchoService** oplossing, klikt u vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="848e8-323">In Solution Explorer in Visual Studio, right-click hello **EchoService** solution, then click **Properties**.</span></span>
3. <span data-ttu-id="848e8-324">Klik in het Hallo-oplossing het dialoogvenster Eigenschappen op **opstartproject**, klikt u vervolgens op Hallo **meerdere opstartprojecten** knop.</span><span class="sxs-lookup"><span data-stu-id="848e8-324">In hello solution properties dialog box, click **Startup Project**, then click hello **Multiple startup projects** button.</span></span> <span data-ttu-id="848e8-325">Zorg ervoor dat **EchoService** verschijnt eerst in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-325">Make sure **EchoService** appears first in hello list.</span></span>
4. <span data-ttu-id="848e8-326">Set Hallo **actie** in voor beide Hallo **EchoService** en **EchoClient** projecten te**Start**.</span><span class="sxs-lookup"><span data-stu-id="848e8-326">Set hello **Action** box for both hello **EchoService** and **EchoClient** projects too**Start**.</span></span>

    ![][5]
5. <span data-ttu-id="848e8-327">Klik op **Projectafhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="848e8-327">Click **Project Dependencies**.</span></span> <span data-ttu-id="848e8-328">In Hallo **projecten** de optie **EchoClient**.</span><span class="sxs-lookup"><span data-stu-id="848e8-328">In hello **Projects** box, select **EchoClient**.</span></span> <span data-ttu-id="848e8-329">In Hallo **is afhankelijk van** zorg **EchoService** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="848e8-329">In hello **Depends on** box, make sure **EchoService** is checked.</span></span>

    ![][6]
6. <span data-ttu-id="848e8-330">Klik op **OK** toodismiss hello **eigenschappen** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="848e8-330">Click **OK** toodismiss hello **Properties** dialog.</span></span>
7. <span data-ttu-id="848e8-331">Druk op **F5** toorun beide projecten.</span><span class="sxs-lookup"><span data-stu-id="848e8-331">Press **F5** toorun both projects.</span></span>
8. <span data-ttu-id="848e8-332">Beide consolevensters openen en u vragen om Hallo naamruimtenaam.</span><span class="sxs-lookup"><span data-stu-id="848e8-332">Both console windows open and prompt you for hello namespace name.</span></span> <span data-ttu-id="848e8-333">Hallo service moet eerst uitvoeren, dus in Hallo **EchoService** consolevenster, voert Hallo-naamruimte in en druk vervolgens op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="848e8-333">hello service must run first, so in hello **EchoService** console window, enter hello namespace and then press **Enter**.</span></span>
9. <span data-ttu-id="848e8-334">U wordt vervolgens nogmaals om uw SAS-sleutel gevraagd.</span><span class="sxs-lookup"><span data-stu-id="848e8-334">Next, you are prompted for your SAS key.</span></span> <span data-ttu-id="848e8-335">Voer Hallo SAS-sleutel in en druk op ENTER.</span><span class="sxs-lookup"><span data-stu-id="848e8-335">Enter hello SAS key and press ENTER.</span></span>

    <span data-ttu-id="848e8-336">Hier volgt een voorbeeld van uitvoer van Hallo-consolevenster.</span><span class="sxs-lookup"><span data-stu-id="848e8-336">Here is example output from hello console window.</span></span> <span data-ttu-id="848e8-337">Houd er rekening mee dat Hallo waarden die hier zijn bijvoorbeeld alleen bedoeld.</span><span class="sxs-lookup"><span data-stu-id="848e8-337">Note that hello values provided here are for example purposes only.</span></span>

    <span data-ttu-id="848e8-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span><span class="sxs-lookup"><span data-stu-id="848e8-338">`Your Service Namespace: myNamespace` `Your SAS Key: <SAS key value>`</span></span>

    <span data-ttu-id="848e8-339">Hallo-servicetoepassing geeft toohello venster Hallo adres van de console waarop luistert, zoals in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="848e8-339">hello service application prints toohello console window hello address on which it's listening, as seen in hello following example.</span></span>

    <span data-ttu-id="848e8-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span><span class="sxs-lookup"><span data-stu-id="848e8-340">`Service address: sb://mynamespace.servicebus.windows.net/EchoService/` `Press [Enter] tooexit`</span></span>
10. <span data-ttu-id="848e8-341">In Hallo **EchoClient** consolevenster, voert u dezelfde informatie die u eerder hebt opgegeven voor de servicetoepassing Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-341">In hello **EchoClient** console window, enter hello same information that you entered previously for hello service application.</span></span> <span data-ttu-id="848e8-342">Ga als volgt Hallo vorige stappen tooenter Hallo dezelfde Servicenaamruimte en SAS waarden voor de clienttoepassing Hallo sleutel.</span><span class="sxs-lookup"><span data-stu-id="848e8-342">Follow hello previous steps tooenter hello same service namespace and SAS key values for hello client application.</span></span>
11. <span data-ttu-id="848e8-343">Na het invoeren van deze waarden Hallo client Hiermee opent u een kanaal toohello-service en de prompts tooenter u wat tekst, zoals in de volgende console-Uitvoervoorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-343">After entering these values, hello client opens a channel toohello service and prompts you tooenter some text as seen in hello following console output example.</span></span>

    `Enter text tooecho (or [Enter] tooexit):`

    <span data-ttu-id="848e8-344">Voer enkele tekst toosend toohello-servicetoepassing en druk op Enter.</span><span class="sxs-lookup"><span data-stu-id="848e8-344">Enter some text toosend toohello service application and press Enter.</span></span> <span data-ttu-id="848e8-345">Deze tekst toohello service via Hallo Echo-servicebewerking is verzonden en wordt weergegeven in het serviceconsolevenster zoals in de volgende voorbeelduitvoer Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="848e8-345">This text is sent toohello service through hello Echo service operation and appears in hello service console window as in hello following example output.</span></span>

    `Echoing: My sample text`

    <span data-ttu-id="848e8-346">Hallo-clienttoepassing ontvangt de retourwaarde Hallo Hallo `Echo` bewerking, waarmee de oorspronkelijke tekst hello en verwerkt deze tooits consolevenster.</span><span class="sxs-lookup"><span data-stu-id="848e8-346">hello client application receives hello return value of hello `Echo` operation, which is hello original text, and prints it tooits console window.</span></span> <span data-ttu-id="848e8-347">Hallo volgt voorbeelduitvoer van Hallo clientconsolevenster.</span><span class="sxs-lookup"><span data-stu-id="848e8-347">hello following is example output from hello client console window.</span></span>

    `Server echoed: My sample text`
12. <span data-ttu-id="848e8-348">U kunt doorgaan met het verzenden van berichten van Hallo client toohello-service op deze manier.</span><span class="sxs-lookup"><span data-stu-id="848e8-348">You can continue sending text messages from hello client toohello service in this manner.</span></span> <span data-ttu-id="848e8-349">Wanneer u klaar bent, drukt u op Enter in Hallo client en service-console windows tooend beide toepassingen.</span><span class="sxs-lookup"><span data-stu-id="848e8-349">When you are finished, press Enter in hello client and service console windows tooend both applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="848e8-350">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="848e8-350">Next steps</span></span>

<span data-ttu-id="848e8-351">Deze zelfstudie hebt u geleerd hoe Hallo mogelijkheden van Service Bus Relay WCF toobuild een Azure-Relay-clienttoepassing en het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="848e8-351">This tutorial showed how toobuild an Azure Relay client application and service using hello WCF Relay capabilities of Service Bus.</span></span> <span data-ttu-id="848e8-352">Voor een vergelijkbare zelfstudie waarin [Service Bus-berichtenservice](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), Zie [aan de slag met Service Bus-wachtrijen](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="848e8-352">For a similar tutorial that uses [Service Bus Messaging](../service-bus-messaging/service-bus-messaging-overview.md#brokered-messaging), see [Get started with Service Bus queues](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md).</span></span>

<span data-ttu-id="848e8-353">toolearn meer informatie over Azure-Relay, Zie Hallo volgende onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="848e8-353">toolearn more about Azure Relay, see hello following topics.</span></span>

* [<span data-ttu-id="848e8-354">Overzicht van Azure Service Bus-architectuur</span><span class="sxs-lookup"><span data-stu-id="848e8-354">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md#relays)
* [<span data-ttu-id="848e8-355">Overzicht van Azure Relay</span><span class="sxs-lookup"><span data-stu-id="848e8-355">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="848e8-356">Hoe toouse Hallo WCF relay-service met .NET</span><span class="sxs-lookup"><span data-stu-id="848e8-356">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure classic portal]: http://manage.windowsazure.com

[2]: ./media/service-bus-relay-tutorial/create-console-app.png
[3]: ./media/service-bus-relay-tutorial/install-nuget.png
[5]: ./media/service-bus-relay-tutorial/set-projects.png
[6]: ./media/service-bus-relay-tutorial/set-depend.png

---
title: aaaService Bus REST-zelfstudie met Azure Relay | Microsoft Docs
description: Bouw een eenvoudige Azure Service Bus relay-hosttoepassing een REST gebaseerde interface.
services: service-bus-relay
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1312b2db-94c4-4a48-b815-c5deb5b77a6a
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/17/2017
ms.author: sethm
ms.openlocfilehash: b68650993a0390e7cef891ccb4236095cd86d4c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="154b1-103">Azure WCF Relay REST-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="154b1-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="154b1-104">Deze zelfstudie wordt beschreven hoe de toepassing die een REST gebaseerde interface voor het hosten van toobuild een eenvoudige Azure-Relay.</span><span class="sxs-lookup"><span data-stu-id="154b1-104">This tutorial describes how toobuild a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="154b1-105">REST kan een webclient, zoals een webbrowser, tooaccess Hallo Service Bus-API's via HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="154b1-105">REST enables a web client, such as a web browser, tooaccess hello Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="154b1-106">Hallo-zelfstudie wordt gebruikgemaakt van Hallo Windows Communication Foundation (WCF) REST programming model tooconstruct een REST-service op de Service Bus.</span><span class="sxs-lookup"><span data-stu-id="154b1-106">hello tutorial uses hello Windows Communication Foundation (WCF) REST programming model tooconstruct a REST service on Service Bus.</span></span> <span data-ttu-id="154b1-107">Zie voor meer informatie [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) en [Services ontwerpen en implementeren](/dotnet/framework/wcf/designing-and-implementing-services) in Hallo WCF-documentatie.</span><span class="sxs-lookup"><span data-stu-id="154b1-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in hello WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="154b1-108">Stap 1: Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="154b1-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="154b1-109">met behulp van toobegin Hallo relay-functies in Azure, moet u eerst een Servicenaamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="154b1-109">toobegin using hello relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="154b1-110">Een naamruimte biedt een scoping container voor het verwerken van Azure-resources in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="154b1-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="154b1-111">Ga als volgt Hallo [hier instructies](relay-create-namespace-portal.md) toocreate een Relay-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="154b1-111">Follow hello [instructions here](relay-create-namespace-portal.md) toocreate a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-toouse-with-azure-relay"></a><span data-ttu-id="154b1-112">Stap 2: Een toouse REST gebaseerd WCF-servicecontract met Azure Relay definiëren</span><span class="sxs-lookup"><span data-stu-id="154b1-112">Step 2: Define a REST-based WCF service contract toouse with Azure Relay</span></span>

<span data-ttu-id="154b1-113">Wanneer u een service WCF REST-stijl maakt, moet u Hallo contract definiëren.</span><span class="sxs-lookup"><span data-stu-id="154b1-113">When you create a WCF REST-style service, you must define hello contract.</span></span> <span data-ttu-id="154b1-114">Hallo contract geeft aan welke bewerkingen Hallo host ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="154b1-114">hello contract specifies what operations hello host supports.</span></span> <span data-ttu-id="154b1-115">Een servicebewerking kan worden beschouwd als een webservicemethode.</span><span class="sxs-lookup"><span data-stu-id="154b1-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="154b1-116">Contracten worden gemaakt door een C++-, C#- of Visual Basic-interface te definiëren.</span><span class="sxs-lookup"><span data-stu-id="154b1-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="154b1-117">Elke methode in Hallo interface komt tooa specifieke servicebewerking overeen.</span><span class="sxs-lookup"><span data-stu-id="154b1-117">Each method in hello interface corresponds tooa specific service operation.</span></span> <span data-ttu-id="154b1-118">Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) -kenmerk moet worden toegepast tooeach interface en Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) kenmerk moet toegepaste tooeach bewerking.</span><span class="sxs-lookup"><span data-stu-id="154b1-118">hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied tooeach interface, and hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied tooeach operation.</span></span> <span data-ttu-id="154b1-119">Als een methode in een interface met Hallo [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) heeft geen Hallo [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), die methode niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="154b1-119">If a method in an interface that has hello [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have hello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="154b1-120">Hallo-code die wordt gebruikt voor deze taken wordt weergegeven in het Hallo-voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="154b1-120">hello code used for these tasks is shown in hello example following hello procedure.</span></span>

<span data-ttu-id="154b1-121">Hallo belangrijkste verschil tussen een WCF-contract en een REST-stijlcontract is Hallo toevoeging van een eigenschap toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="154b1-121">hello primary difference between a WCF contract and a REST-style contract is hello addition of a property toohello [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="154b1-122">Deze eigenschap kunt u een methode in uw interfacemethode tooa op Hallo toomap andere kant van het Hallo-interface.</span><span class="sxs-lookup"><span data-stu-id="154b1-122">This property enables you toomap a method in your interface tooa method on hello other side of hello interface.</span></span> <span data-ttu-id="154b1-123">We gebruiken in dit geval [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink een tooHTTP methode GET.</span><span class="sxs-lookup"><span data-stu-id="154b1-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) toolink a method tooHTTP GET.</span></span> <span data-ttu-id="154b1-124">Hierdoor kan Service Bus tooaccurately ophalen en interpreteren opdrachten toohello interface verzonden.</span><span class="sxs-lookup"><span data-stu-id="154b1-124">This allows Service Bus tooaccurately retrieve and interpret commands sent toohello interface.</span></span>

### <a name="toocreate-a-contract-with-an-interface"></a><span data-ttu-id="154b1-125">toocreate een contract met een interface</span><span class="sxs-lookup"><span data-stu-id="154b1-125">toocreate a contract with an interface</span></span>

1. <span data-ttu-id="154b1-126">Open Visual Studio als beheerder: klik met de rechtermuisknop Hallo programma in Hallo **Start** menu en klik vervolgens op **als administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="154b1-126">Open Visual Studio as an administrator: right-click hello program in hello **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="154b1-127">Maak een nieuw consoletoepassingsproject aan.</span><span class="sxs-lookup"><span data-stu-id="154b1-127">Create a new console application project.</span></span> <span data-ttu-id="154b1-128">Klik op Hallo **bestand** menu en selecteer **nieuw**, selecteer daarna **Project**.</span><span class="sxs-lookup"><span data-stu-id="154b1-128">Click hello **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="154b1-129">In Hallo **nieuw Project** in het dialoogvenster klikt u op **Visual C#**, selecteer Hallo **consoletoepassing** -sjabloon en noem deze **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="154b1-129">In hello **New Project** dialog box, click **Visual C#**, select hello **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="154b1-130">Standaard-Hallo **locatie**.</span><span class="sxs-lookup"><span data-stu-id="154b1-130">Use hello default **Location**.</span></span> <span data-ttu-id="154b1-131">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="154b1-131">Click **OK** toocreate hello project.</span></span>
3. <span data-ttu-id="154b1-132">Voor een C#-project maakt Visual Studio een `Program.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="154b1-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="154b1-133">Deze klasse bevat een lege `Main()` methode, vereist voor een console application project toobuild correct.</span><span class="sxs-lookup"><span data-stu-id="154b1-133">This class contains an empty `Main()` method, required for a console application project toobuild correctly.</span></span>
4. <span data-ttu-id="154b1-134">Voeg verwijzingen tooService Bus en **System.ServiceModel.dll** toohello project door Hallo Service Bus NuGet-pakket installeert.</span><span class="sxs-lookup"><span data-stu-id="154b1-134">Add references tooService Bus and **System.ServiceModel.dll** toohello project by installing hello Service Bus NuGet package.</span></span> <span data-ttu-id="154b1-135">Dit pakket wordt automatisch toegevoegd verwijzingen toohello Service Bus-bibliotheken, evenals Hallo WCF **System.ServiceModel**.</span><span class="sxs-lookup"><span data-stu-id="154b1-135">This package automatically adds references toohello Service Bus libraries, as well as hello WCF **System.ServiceModel**.</span></span> <span data-ttu-id="154b1-136">Klik in Solution Explorer met de rechtermuisknop op Hallo **ImageListener** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="154b1-136">In Solution Explorer, right-click hello **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="154b1-137">Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="154b1-137">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="154b1-138">Klik op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="154b1-138">Click **Install**, and accept hello terms of use.</span></span>
5. <span data-ttu-id="154b1-139">U moet expliciet een verwijzing te toevoegen**System.ServiceModel.Web.dll** toohello project:</span><span class="sxs-lookup"><span data-stu-id="154b1-139">You must explicitly add a reference too**System.ServiceModel.Web.dll** toohello project:</span></span>
   
    <span data-ttu-id="154b1-140">a.</span><span class="sxs-lookup"><span data-stu-id="154b1-140">a.</span></span> <span data-ttu-id="154b1-141">Klik in Solution Explorer met de rechtermuisknop op Hallo **verwijzingen** map onder Hallo projectmap en klik vervolgens op **verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="154b1-141">In Solution Explorer, right-click hello **References** folder under hello project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="154b1-142">b.</span><span class="sxs-lookup"><span data-stu-id="154b1-142">b.</span></span> <span data-ttu-id="154b1-143">In Hallo **verwijzing toevoegen** dialoogvenster vak, klikt u op Hallo **Framework** tabblad aan de linkerkant hello en in Hallo **Search** in het vak **System.ServiceModel.Web** .</span><span class="sxs-lookup"><span data-stu-id="154b1-143">In hello **Add Reference** dialog box, click hello **Framework** tab on hello left-hand side and in hello **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="154b1-144">Selecteer Hallo **System.ServiceModel.Web** selectievakje en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="154b1-144">Select hello **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="154b1-145">Voeg de volgende Hallo `using` instructies Hallo boven aan het bestand Program.cs Hallo.</span><span class="sxs-lookup"><span data-stu-id="154b1-145">Add hello following `using` statements at hello top of hello Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="154b1-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is Hallo-naamruimte die programmatisch toegang toobasic onderdelen van WCF.</span><span class="sxs-lookup"><span data-stu-id="154b1-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is hello namespace that enables programmatic access toobasic features of WCF.</span></span> <span data-ttu-id="154b1-147">Relay WCF maakt gebruik van veel van Hallo-objecten en kenmerken van WCF toodefine servicecontracten.</span><span class="sxs-lookup"><span data-stu-id="154b1-147">WCF Relay uses many of hello objects and attributes of WCF toodefine service contracts.</span></span> <span data-ttu-id="154b1-148">U gebruikt deze naamruimte in de meeste van de relay-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="154b1-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="154b1-149">Op deze manier [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helpt bij het Hallo-kanaal is Hallo-object waarmee u contact met de Azure-Relay en Hallo clientwebbrowser opnemen definiëren.</span><span class="sxs-lookup"><span data-stu-id="154b1-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define hello channel, which is hello object through which you communicate with Azure Relay and hello client web browser.</span></span> <span data-ttu-id="154b1-150">Ten slotte [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) bevat Hallo typen waarmee u toocreate webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="154b1-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains hello types that enable you toocreate web-based applications.</span></span>
7. <span data-ttu-id="154b1-151">Wijzig de naam van Hallo `ImageListener` naamruimte te**Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="154b1-151">Rename hello `ImageListener` namespace too**Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="154b1-152">Direct na de Hallo na accolades openen van de naamruimtedeclaratie hello, definiëren een nieuwe interface met de naam **IImageContract** en toepassing hello **ServiceContractAttribute** kenmerk toohello interface met een waarde van `http://samples.microsoft.com/ServiceModel/Relay/`.</span><span class="sxs-lookup"><span data-stu-id="154b1-152">Directly after hello opening curly brace of hello namespace declaration, define a new interface named **IImageContract** and apply hello **ServiceContractAttribute** attribute toohello interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="154b1-153">Hallo naamruimtewaarde verschilt van Hallo-naamruimte die u gebruiken voor de hele Hallo bereik van uw code.</span><span class="sxs-lookup"><span data-stu-id="154b1-153">hello namespace value differs from hello namespace that you use throughout hello scope of your code.</span></span> <span data-ttu-id="154b1-154">Hallo naamruimtewaarde wordt gebruikt als een unieke id voor dit contract en moet versie-informatie.</span><span class="sxs-lookup"><span data-stu-id="154b1-154">hello namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="154b1-155">Zie [Serviceversiebeheer](http://go.microsoft.com/fwlink/?LinkID=180498) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="154b1-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="154b1-156">Het expliciet opgeven van Hallo-naamruimte voorkomt u dat standaardnaamruimtewaarde hello toohello contractnaam wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="154b1-156">Specifying hello namespace explicitly prevents hello default namespace value from being added toohello contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="154b1-157">Binnen Hallo `IImageContract` interface, declareert u een methode voor het Hallo één bewerking Hallo `IImageContract` contract zichtbaar gemaakt in Hallo interface en toepassing hello `OperationContractAttribute` toohello methode waarmee u tooexpose als onderdeel van Hallo openbare Service Bus-kenmerk contract.</span><span class="sxs-lookup"><span data-stu-id="154b1-157">Within hello `IImageContract` interface, declare a method for hello single operation hello `IImageContract` contract exposes in hello interface and apply hello `OperationContractAttribute` attribute toohello method that you want tooexpose as part of hello public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="154b1-158">In Hallo **OperationContract** kenmerk, het toevoegen van Hallo **WebGet** waarde.</span><span class="sxs-lookup"><span data-stu-id="154b1-158">In hello **OperationContract** attribute, add hello **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="154b1-159">Dit doet, kunnen Hallo relay-service tooroute HTTP GET-te aanvragen`GetImage`, en tootranslate Hallo retourwaarden van `GetImage` in een HTTP GETRESPONSE-antwoord.</span><span class="sxs-lookup"><span data-stu-id="154b1-159">Doing so enables hello relay service tooroute HTTP GET requests too`GetImage`, and tootranslate hello return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="154b1-160">Later in Hallo zelfstudie gebruikt u een web browser tooaccess deze methode als toodisplay Hallo installatiekopie in de browser Hallo.</span><span class="sxs-lookup"><span data-stu-id="154b1-160">Later in hello tutorial, you will use a web browser tooaccess this method, and toodisplay hello image in hello browser.</span></span>
11. <span data-ttu-id="154b1-161">Direct na Hallo `IImageContract` definitie een kanaal dat eigenschappen van beide Hallo overneemt declareren `IImageContract` en `IClientChannel` interfaces.</span><span class="sxs-lookup"><span data-stu-id="154b1-161">Directly after hello `IImageContract` definition, declare a channel that inherits from both hello `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="154b1-162">Een kanaal is Hallo WCF-object waarmee Hallo-service en de client informatie tooeach andere doorgeven.</span><span class="sxs-lookup"><span data-stu-id="154b1-162">A channel is hello WCF object through which hello service and client pass information tooeach other.</span></span> <span data-ttu-id="154b1-163">Later, maakt u Hallo channel in uw hosttoepassing.</span><span class="sxs-lookup"><span data-stu-id="154b1-163">Later, you will create hello channel in your host application.</span></span> <span data-ttu-id="154b1-164">Azure Relay gebruikt dit kanaal toopass Hallo HTTP GET-aanvragen van Hallo browser tooyour **GetImage** implementatie.</span><span class="sxs-lookup"><span data-stu-id="154b1-164">Azure Relay then uses this channel toopass hello HTTP GET requests from hello browser tooyour **GetImage** implementation.</span></span> <span data-ttu-id="154b1-165">Hallo relay gebruikt ook Hallo kanaal tootake hello **GetImage** waarde retourneren en zet deze om naar een HTTP GETRESPONSE voor de clientbrowser Hallo.</span><span class="sxs-lookup"><span data-stu-id="154b1-165">hello relay also uses hello channel tootake hello **GetImage** return value and translate it into an HTTP GETRESPONSE for hello client browser.</span></span>
12. <span data-ttu-id="154b1-166">Van Hallo **bouwen** menu, klikt u op **Build Solution** tooconfirm Hallo juistheid van uw werk tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="154b1-166">From hello **Build** menu, click **Build Solution** tooconfirm hello accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="154b1-167">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="154b1-167">Example</span></span>
<span data-ttu-id="154b1-168">Hallo volgende code toont een eenvoudige interface die een Relay WCF-contract wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="154b1-168">hello following code shows a basic interface that defines a WCF Relay contract.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "IImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

## <a name="step-3-implement-a-rest-based-wcf-service-contract-toouse-service-bus"></a><span data-ttu-id="154b1-169">Stap 3: Een REST gebaseerd WCF-servicecontract toouse Service Bus implementeren</span><span class="sxs-lookup"><span data-stu-id="154b1-169">Step 3: Implement a REST-based WCF service contract toouse Service Bus</span></span>
<span data-ttu-id="154b1-170">Maken van een REST-stijl WCF Relay-service, moet eerst de Hallo-contract wordt gedefinieerd door middel van een interface te maken.</span><span class="sxs-lookup"><span data-stu-id="154b1-170">Creating a REST-style WCF Relay service requires that you first create hello contract, which is defined by using an interface.</span></span> <span data-ttu-id="154b1-171">de volgende stap Hallo is tooimplement Hallo-interface.</span><span class="sxs-lookup"><span data-stu-id="154b1-171">hello next step is tooimplement hello interface.</span></span> <span data-ttu-id="154b1-172">Dit omvat het maken van een klasse met de naam **ImageService** die gebruiker gedefinieerde Hallo implementeert **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="154b1-172">This involves creating a class named **ImageService** that implements hello user-defined **IImageContract** interface.</span></span> <span data-ttu-id="154b1-173">Nadat u Hallo contract implementeert, configureert u Hallo-interface met een App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="154b1-173">After you implement hello contract, you then configure hello interface using an App.config file.</span></span> <span data-ttu-id="154b1-174">Hallo-configuratiebestand bevat de benodigde gegevens voor het Hallo-toepassing, zoals het Hallo-naam van Hallo-service, Hallo-naam van het Hallo-contract en Hallo type protocol dat wordt gebruikt toocommunicate met Hallo relay-service.</span><span class="sxs-lookup"><span data-stu-id="154b1-174">hello configuration file contains necessary information for hello application, such as hello name of hello service, hello name of hello contract, and hello type of protocol that is used toocommunicate with hello relay service.</span></span> <span data-ttu-id="154b1-175">Hallo-code die wordt gebruikt voor deze taken wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="154b1-175">hello code used for these tasks is provided in hello example following hello procedure.</span></span>

<span data-ttu-id="154b1-176">Als met de vorige stappen hello, er is weinig verschil tussen het implementeren van een REST-stijlcontract en een Relay WCF-contract.</span><span class="sxs-lookup"><span data-stu-id="154b1-176">As with hello previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="tooimplement-a-rest-style-service-bus-contract"></a><span data-ttu-id="154b1-177">Service Bus-contract tooimplement een REST-stijl</span><span class="sxs-lookup"><span data-stu-id="154b1-177">tooimplement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="154b1-178">Maak een nieuwe klasse met de naam **ImageService** direct na de definitie van Hallo Hallo **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="154b1-178">Create a new class named **ImageService** directly after hello definition of hello **IImageContract** interface.</span></span> <span data-ttu-id="154b1-179">Hallo **ImageService** klasse implementeert Hallo **IImageContract** interface.</span><span class="sxs-lookup"><span data-stu-id="154b1-179">hello **ImageService** class implements hello **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="154b1-180">Vergelijkbare tooother interface-implementaties, kunt u Hallo definitie implementeren in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="154b1-180">Similar tooother interface implementations, you can implement hello definition in a different file.</span></span> <span data-ttu-id="154b1-181">Voor deze zelfstudie Hallo-implementatie wordt weergegeven in hetzelfde bestand als de interfacedefinitie Hallo Hallo en `Main()` methode.</span><span class="sxs-lookup"><span data-stu-id="154b1-181">However, for this tutorial, hello implementation appears in hello same file as hello interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="154b1-182">Toepassing hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) kenmerk toohello **IImageService** klasse tooindicate die klasse Hallo is een implementatie van een WCF-contract.</span><span class="sxs-lookup"><span data-stu-id="154b1-182">Apply hello [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute toohello **IImageService** class tooindicate that hello class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="154b1-183">Zoals eerder is vermeld, is deze naamruimte geen traditionele naamruimte,</span><span class="sxs-lookup"><span data-stu-id="154b1-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="154b1-184">In plaats daarvan uitmaakt het deel van Hallo WCF-architectuur waarmee Hallo contract identificeert.</span><span class="sxs-lookup"><span data-stu-id="154b1-184">Instead, it is part of hello WCF architecture that identifies hello contract.</span></span> <span data-ttu-id="154b1-185">Zie voor meer informatie, Hallo [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) onderwerp in Hallo WCF-documentatie.</span><span class="sxs-lookup"><span data-stu-id="154b1-185">For more information, see hello [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in hello WCF documentation.</span></span>
3. <span data-ttu-id="154b1-186">Voeg een jpg-installatiekopie tooyour-project.</span><span class="sxs-lookup"><span data-stu-id="154b1-186">Add a .jpg image tooyour project.</span></span>  
   
    <span data-ttu-id="154b1-187">Dit is een afbeelding die Hallo-service wordt weergegeven in Hallo ontvangen van de browser.</span><span class="sxs-lookup"><span data-stu-id="154b1-187">This is a picture that hello service displays in hello receiving browser.</span></span> <span data-ttu-id="154b1-188">Klik met de rechtermuisknop op het project en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="154b1-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="154b1-189">Klik vervolgens op **Bestaand item**.</span><span class="sxs-lookup"><span data-stu-id="154b1-189">Then click **Existing Item**.</span></span> <span data-ttu-id="154b1-190">Gebruik Hallo **Add Existing Item** dialoogvenster vak toobrowse tooan geschikt jpg en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="154b1-190">Use hello **Add Existing Item** dialog box toobrowse tooan appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="154b1-191">Wanneer u Hallo bestand toevoegt, zorg ervoor dat **alle bestanden** is geselecteerd in de volgende toohello van Hallo vervolgkeuzelijst **bestandsnaam:** veld.</span><span class="sxs-lookup"><span data-stu-id="154b1-191">When adding hello file, make sure that **All Files** is selected in hello drop-down list next toohello **File name:** field.</span></span> <span data-ttu-id="154b1-192">Hallo rest van deze handleiding wordt ervan uitgegaan dat Hallo naam van Hallo afbeelding 'image.jpg' is.</span><span class="sxs-lookup"><span data-stu-id="154b1-192">hello rest of this tutorial assumes that hello name of hello image is "image.jpg".</span></span> <span data-ttu-id="154b1-193">Als u een ander bestand hebt, wordt toorename Hallo afbeelding, of wijzig uw toocompensate code.</span><span class="sxs-lookup"><span data-stu-id="154b1-193">If you have a different file, you will have toorename hello image, or change your code toocompensate.</span></span>
4. <span data-ttu-id="154b1-194">er zeker die Hallo waarop service wordt uitgevoerd in Hallo installatiekopiebestand kan vinden toomake **Solution Explorer** met de rechtermuisknop op het Hallo-afbeeldingsbestand en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="154b1-194">toomake sure that hello running service can find hello image file, in **Solution Explorer** right-click hello image file, then click **Properties**.</span></span> <span data-ttu-id="154b1-195">In Hallo **eigenschappen** deelvenster ingesteld **tooOutput Directory kopiëren** te**kopiëren indien nieuwer**.</span><span class="sxs-lookup"><span data-stu-id="154b1-195">In hello **Properties** pane, set **Copy tooOutput Directory** too**Copy if newer**.</span></span>
5. <span data-ttu-id="154b1-196">Voeg een verwijzing toohello **System.Drawing.dll** assembly toohello project en ook toevoegen Hallo volgende gekoppelde `using` instructies.</span><span class="sxs-lookup"><span data-stu-id="154b1-196">Add a reference toohello **System.Drawing.dll** assembly toohello project, and also add hello following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="154b1-197">In Hallo **ImageService** klasse, het toevoegen van Hallo volgende constructor dat geladen bitmap Hallo en toosend bereidt het toohello clientbrowser.</span><span class="sxs-lookup"><span data-stu-id="154b1-197">In hello **ImageService** class, add hello following constructor that loads hello bitmap and prepares toosend it toohello client browser.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";
   
        Image bitmap;
   
        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }
    }
    ```
7. <span data-ttu-id="154b1-198">Direct na de vorige code hello, voeg de volgende Hallo **GetImage** methode in Hallo **ImageService** klasse tooreturn een HTTP-bericht dat de installatiekopie Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="154b1-198">Directly after hello previous code, add hello following **GetImage** method in hello **ImageService** class tooreturn an HTTP message that contains hello image.</span></span>
   
    ```csharp
    public Stream GetImage()
    {
        MemoryStream stream = new MemoryStream();
        this.bitmap.Save(stream, ImageFormat.Jpeg);
   
        stream.Position = 0;
        WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";
   
        return stream;
    }
    ```
   
    <span data-ttu-id="154b1-199">Maakt gebruik van deze implementatie **MemoryStream** tooretrieve Hallo installatiekopie en voorbereiden voor streaming toohello browser.</span><span class="sxs-lookup"><span data-stu-id="154b1-199">This implementation uses **MemoryStream** tooretrieve hello image and prepare it for streaming toohello browser.</span></span> <span data-ttu-id="154b1-200">Het Hallo stroompositie bij nul wordt gestart, declareert Hallo stroominhoud als jpeg en streams Hallo informatie.</span><span class="sxs-lookup"><span data-stu-id="154b1-200">It starts hello stream position at zero, declares hello stream content as a jpeg, and streams hello information.</span></span>
8. <span data-ttu-id="154b1-201">Van Hallo **bouwen** menu, klikt u op **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="154b1-201">From hello **Build** menu, click **Build Solution**.</span></span>

### <a name="toodefine-hello-configuration-for-running-hello-web-service-on-service-bus"></a><span data-ttu-id="154b1-202">toodefine hello configuratie voor het uitvoeren van Hallo-webservice in Service Bus</span><span class="sxs-lookup"><span data-stu-id="154b1-202">toodefine hello configuration for running hello web service on Service Bus</span></span>
1. <span data-ttu-id="154b1-203">In **Solution Explorer**, dubbelklikt u op **App.config** tooopen in Hallo Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="154b1-203">In **Solution Explorer**, double-click **App.config** tooopen it in hello Visual Studio editor.</span></span>
   
    <span data-ttu-id="154b1-204">Hallo **App.config** -bestand bevat de servicenaam hello, eindpunt (dat wil zeggen, Hallo locatie Azure Relay voor clients en hosts toocommunicate met elkaar biedt) en binding (Hallo type protocol dat wordt gebruikt toocommunicate).</span><span class="sxs-lookup"><span data-stu-id="154b1-204">hello **App.config** file includes hello service name, endpoint (that is, hello location Azure Relay exposes for clients and hosts toocommunicate with each other), and binding (hello type of protocol that is used toocommunicate).</span></span> <span data-ttu-id="154b1-205">Hallo hier het belangrijkste verschil is dat Hallo geconfigureerd service-eindpunt verwijst tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span><span class="sxs-lookup"><span data-stu-id="154b1-205">hello main difference here is that hello configured service endpoint refers tooa [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="154b1-206">Hallo `<system.serviceModel>` XML-element is een WCF-element dat een of meer services definieert.</span><span class="sxs-lookup"><span data-stu-id="154b1-206">hello `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="154b1-207">Hier is het gebruikte toodefine Hallo servicenaam en -eindpunt.</span><span class="sxs-lookup"><span data-stu-id="154b1-207">Here, it is used toodefine hello service name and endpoint.</span></span> <span data-ttu-id="154b1-208">Hallo Hallo onderaan in `<system.serviceModel>` element (maar nog steeds binnen `<system.serviceModel>`), Voeg een `<bindings>` -element waarvoor Hallo inhoud na.</span><span class="sxs-lookup"><span data-stu-id="154b1-208">At hello bottom of hello `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has hello following content.</span></span> <span data-ttu-id="154b1-209">Hiermee definieert u Hallo bindingen in de toepassing hello gebruikt.</span><span class="sxs-lookup"><span data-stu-id="154b1-209">This defines hello bindings used in hello application.</span></span> <span data-ttu-id="154b1-210">U kunt meerdere bindingen definiëren, maar in deze zelfstudie definieert u er slechts één.</span><span class="sxs-lookup"><span data-stu-id="154b1-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
    ```xml
    <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
            <binding name="default">
                <security relayClientAuthenticationType="None" />
            </binding>
        </webHttpRelayBinding>
    </bindings>
    ```
   
    <span data-ttu-id="154b1-211">Hallo vorige code definieert een Relay WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding met **relayClientAuthenticationType** instellen te**geen**.</span><span class="sxs-lookup"><span data-stu-id="154b1-211">hello previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set too**None**.</span></span> <span data-ttu-id="154b1-212">Met deze instelling geeft u aan dat voor een eindpunt dat deze binding gebruikt, geen clientreferentie is vereist.</span><span class="sxs-lookup"><span data-stu-id="154b1-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="154b1-213">Na het Hallo `<bindings>` element, Voeg een `<services>` element.</span><span class="sxs-lookup"><span data-stu-id="154b1-213">After hello `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="154b1-214">Soortgelijke toohello bindingen kunt u meerdere services definiëren in een enkel configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="154b1-214">Similar toohello bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="154b1-215">In deze zelfstudie definieert u slechts een service.</span><span class="sxs-lookup"><span data-stu-id="154b1-215">However, for this tutorial, you define only one.</span></span>
   
    ```xml
    <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
            <endpoint name="RelayEndpoint"
                    contract="Microsoft.ServiceBus.Samples.IImageContract"
                    binding="webHttpRelayBinding"
                    bindingConfiguration="default"
                    behaviorConfiguration="sbTokenProvider"
                    address="" />
        </service>
    </services>
    ```
   
    <span data-ttu-id="154b1-216">Deze stap configureert u een service die gebruikmaakt van standaard Hallo eerder gedefinieerd **webHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="154b1-216">This step configures a service that uses hello previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="154b1-217">Gebruikt ook Hallo standaard **sbTokenProvider**, die is gedefinieerd in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="154b1-217">It also uses hello default **sbTokenProvider**, which is defined in hello next step.</span></span>
4. <span data-ttu-id="154b1-218">Na Hallo `<services>` element, maakt een `<behaviors>` element met Hallo inhoud te volgen, Vervang 'sas_key ' vervangen door Hallo *Shared Access Signature* (SAS)-sleutel die u eerder hebt verkregen via Hallo [Azure-portal ][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="154b1-218">After hello `<services>` element, create a `<behaviors>` element with hello following content, replacing "SAS_KEY" with hello *Shared Access Signature* (SAS) key you previously obtained from hello [Azure portal][Azure portal].</span></span>
   
    ```xml
    <behaviors>
        <endpointBehaviors>
            <behavior name="sbTokenProvider">
                <transportClientEndpointBehavior>
                    <tokenProvider>
                        <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
                    </tokenProvider>
                </transportClientEndpointBehavior>
            </behavior>
            </endpointBehaviors>
            <serviceBehaviors>
                <behavior name="default">
                    <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
                </behavior>
            </serviceBehaviors>
    </behaviors>
    ```
5. <span data-ttu-id="154b1-219">Nog steeds in App.config in Hallo `<appSettings>` vervangen Hallo gehele gegevensbronwaarde met verbindingsreeks die u eerder hebt verkregen via de portal Hallo Hallo-element.</span><span class="sxs-lookup"><span data-stu-id="154b1-219">Still in App.config, in hello `<appSettings>` element, replace hello entire connection string value with hello connection string you previously obtained from hello portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="154b1-220">Van Hallo **bouwen** menu, klikt u op **Build Solution** toobuild Hallo hele oplossing.</span><span class="sxs-lookup"><span data-stu-id="154b1-220">From hello **Build** menu, click **Build Solution** toobuild hello entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="154b1-221">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="154b1-221">Example</span></span>
<span data-ttu-id="154b1-222">Hallo volgende code toont Hallo contract en de service-implementatie voor een op REST gebaseerde service die wordt uitgevoerd op de Service Bus met Hallo **WebHttpRelayBinding** binding.</span><span class="sxs-lookup"><span data-stu-id="154b1-222">hello following code shows hello contract and service implementation for a REST-based service that is running on  Service Bus using hello **WebHttpRelayBinding** binding.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{


    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```

<span data-ttu-id="154b1-223">Hallo ziet volgende voorbeeld Hallo App.config-bestand dat is gekoppeld met Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="154b1-223">hello following example shows hello App.config file associated with hello service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove hello ones they don't need. -->
            <behaviorExtensions>
                <add name="connectionStatusBehavior"
                    type="Microsoft.ServiceBus.Configuration.ConnectionStatusElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="transportClientEndpointBehavior"
                    type="Microsoft.ServiceBus.Configuration.TransportClientEndpointBehaviorElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="serviceRegistrySettings"
                    type="Microsoft.ServiceBus.Configuration.ServiceRegistrySettingsElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </behaviorExtensions>
            <bindingElementExtensions>
                <add name="netMessagingTransport"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingTransportExtensionElement, Microsoft.ServiceBus,  Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="tcpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.TcpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="httpsRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.HttpsRelayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="onewayRelayTransport"
                    type="Microsoft.ServiceBus.Configuration.RelayedOnewayTransportElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingElementExtensions>
            <bindingExtensions>
                <add name="basicHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.BasicHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="webHttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WebHttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="ws2007HttpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.WS2007HttpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netTcpRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetTcpRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netOnewayRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetOnewayRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netEventRelayBinding"
                    type="Microsoft.ServiceBus.Configuration.NetEventRelayBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
                <add name="netMessagingBinding"
                    type="Microsoft.ServiceBus.Messaging.Configuration.NetMessagingBindingCollectionElement, Microsoft.ServiceBus, Culture=neutral, PublicKeyToken=31bf3856ad364e35"/>
            </bindingExtensions>
        </extensions>
      <bindings>
        <!-- Application Binding -->
        <webHttpRelayBinding>
          <binding name="default">
            <security relayClientAuthenticationType="None" />
          </binding>
        </webHttpRelayBinding>
      </bindings>
      <services>
        <!-- Application Service -->
        <service name="Microsoft.ServiceBus.Samples.ImageService"
             behaviorConfiguration="default">
          <endpoint name="RelayEndpoint"
                  contract="Microsoft.ServiceBus.Samples.IImageContract"
                  binding="webHttpRelayBinding"
                  bindingConfiguration="default"
                  behaviorConfiguration="sbTokenProvider"
                  address="" />
        </service>
      </services>
      <behaviors>
        <endpointBehaviors>
          <behavior name="sbTokenProvider">
            <transportClientEndpointBehavior>
              <tokenProvider>
                <sharedAccessSignature keyName="RootManageSharedAccessKey" key="YOUR_SAS_KEY" />
              </tokenProvider>
            </transportClientEndpointBehavior>
          </behavior>
        </endpointBehaviors>
        <serviceBehaviors>
          <behavior name="default">
            <serviceDebug httpHelpPageEnabled="false" httpsHelpPageEnabled="false" />
          </behavior>
        </serviceBehaviors>
      </behaviors>
    </system.serviceModel>
    <appSettings>
        <!-- Service Bus specific app setings for messaging connections -->
        <add key="Microsoft.ServiceBus.ConnectionString"
            value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey="YOUR_SAS_KEY"/>
    </appSettings>
</configuration>
```

## <a name="step-4-host-hello-rest-based-wcf-service-toouse-azure-relay"></a><span data-ttu-id="154b1-224">Stap 4: Host Hallo REST gebaseerd WCF-service toouse Relay in Azure</span><span class="sxs-lookup"><span data-stu-id="154b1-224">Step 4: Host hello REST-based WCF service toouse Azure Relay</span></span>
<span data-ttu-id="154b1-225">Deze stap wordt beschreven hoe toorun een web service met een consoletoepassing met WCF Relay.</span><span class="sxs-lookup"><span data-stu-id="154b1-225">This step describes how toorun a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="154b1-226">Een volledig overzicht van Hallo code die is geschreven in deze stap wordt vermeld in Hallo voorbeeld Hallo procedure te volgen.</span><span class="sxs-lookup"><span data-stu-id="154b1-226">A complete listing of hello code written in this step is provided in hello example following hello procedure.</span></span>

### <a name="toocreate-a-base-address-for-hello-service"></a><span data-ttu-id="154b1-227">een basisadres voor Hallo service toocreate</span><span class="sxs-lookup"><span data-stu-id="154b1-227">toocreate a base address for hello service</span></span>
1. <span data-ttu-id="154b1-228">In Hallo `Main()` declaratie van de functie, maakt u een variabele toostore Hallo-naamruimte van uw project.</span><span class="sxs-lookup"><span data-stu-id="154b1-228">In hello `Main()` function declaration, create a variable toostore hello namespace of your project.</span></span> <span data-ttu-id="154b1-229">Zorg ervoor dat tooreplace `yourNamespace` met Hallo-naam van Hallo Relay naamruimte die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="154b1-229">Make sure tooreplace `yourNamespace` with hello name of hello Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="154b1-230">Service Bus maakt gebruik van Hallo-naam van uw naamruimte toocreate een unieke URI.</span><span class="sxs-lookup"><span data-stu-id="154b1-230">Service Bus uses hello name of your namespace toocreate a unique URI.</span></span>
2. <span data-ttu-id="154b1-231">Maak een `Uri` exemplaar voor het basisadres Hallo van Hallo-service die is gebaseerd op Hallo-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="154b1-231">Create a `Uri` instance for hello base address of hello service that is based on hello namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="toocreate-and-configure-hello-web-service-host"></a><span data-ttu-id="154b1-232">toocreate en Hallo WebServiceHost configureren</span><span class="sxs-lookup"><span data-stu-id="154b1-232">toocreate and configure hello web service host</span></span>
* <span data-ttu-id="154b1-233">Hallo web ServiceHost, met behulp van de URI-adres Hallo eerder hebt gemaakt in deze sectie maken.</span><span class="sxs-lookup"><span data-stu-id="154b1-233">Create hello web service host, using hello URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="154b1-234">Hallo ServiceHost is Hallo WCF-object dat Hallo-hosttoepassing instantieert.</span><span class="sxs-lookup"><span data-stu-id="154b1-234">hello service host is hello WCF object that instantiates hello host application.</span></span> <span data-ttu-id="154b1-235">In dit voorbeeld wordt doorgegeven Hallo type host dat u wilt dat toocreate (een **ImageService**), en ook Hallo-mailadres waarmee u tooexpose Hallo-hosttoepassing.</span><span class="sxs-lookup"><span data-stu-id="154b1-235">This example passes it hello type of host you want toocreate (an **ImageService**), and also hello address at which you want tooexpose hello host application.</span></span>

### <a name="toorun-hello-web-service-host"></a><span data-ttu-id="154b1-236">toorun hello WebServiceHost</span><span class="sxs-lookup"><span data-stu-id="154b1-236">toorun hello web service host</span></span>
1. <span data-ttu-id="154b1-237">Hallo-service openen.</span><span class="sxs-lookup"><span data-stu-id="154b1-237">Open hello service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="154b1-238">Hallo-service wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="154b1-238">hello service is now running.</span></span>
2. <span data-ttu-id="154b1-239">Een bericht waarin staat dat Hallo-service wordt uitgevoerd en hoe toostop Hallo service weergegeven.</span><span class="sxs-lookup"><span data-stu-id="154b1-239">Display a message indicating that hello service is running, and how toostop hello service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] tooexit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="154b1-240">Wanneer u klaar bent, sluit u Hallo ServiceHost.</span><span class="sxs-lookup"><span data-stu-id="154b1-240">When finished, close hello service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="154b1-241">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="154b1-241">Example</span></span>
<span data-ttu-id="154b1-242">Hallo volgende voorbeeld bevat Hallo servicecontract en de implementatie uit de vorige stappen in Hallo zelfstudie en hosts Hallo service in een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="154b1-242">hello following example includes hello service contract and implementation from previous steps in hello tutorial and hosts hello service in a console application.</span></span> <span data-ttu-id="154b1-243">Compileren Hallo na de code in een uitvoerbaar bestand met de naam ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="154b1-243">Compile hello following code into an executable named ImageListener.exe.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.ServiceModel;
using System.ServiceModel.Channels;
using System.ServiceModel.Web;
using System.IO;
using System.Drawing;
using System.Drawing.Imaging;
using Microsoft.ServiceBus;
using Microsoft.ServiceBus.Web;

namespace Microsoft.ServiceBus.Samples
{

    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }

    public interface IImageChannel : IImageContract, IClientChannel { }

    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
        const string imageFileName = "image.jpg";

        Image bitmap;

        public ImageService()
        {
            this.bitmap = Image.FromFile(imageFileName);
        }

        public Stream GetImage()
        {
            MemoryStream stream = new MemoryStream();
            this.bitmap.Save(stream, ImageFormat.Jpeg);

            stream.Position = 0;
            WebOperationContext.Current.OutgoingResponse.ContentType = "image/jpeg";

            return stream;
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string serviceNamespace = "InsertServiceNamespaceHere";
            Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");

            WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
            host.Open();

            Console.WriteLine("Copy hello following address into a browser toosee hello image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] tooexit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-hello-code"></a><span data-ttu-id="154b1-244">Hallo code compileren</span><span class="sxs-lookup"><span data-stu-id="154b1-244">Compiling hello code</span></span>
<span data-ttu-id="154b1-245">Na het Hallo-oplossing bouwen, Hallo na toorun Hallo toepassing:</span><span class="sxs-lookup"><span data-stu-id="154b1-245">After building hello solution, do hello following toorun hello application:</span></span>

1. <span data-ttu-id="154b1-246">Druk op **F5**, of blader toohello uitvoerbaar bestandslocatie (ImageListener\bin\Debug\ImageListener.exe) toorun Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="154b1-246">Press **F5**, or browse toohello executable file location (ImageListener\bin\Debug\ImageListener.exe), toorun hello service.</span></span> <span data-ttu-id="154b1-247">Houd Hallo app wordt uitgevoerd, wordt dit tooperform Hallo volgende stap is vereist.</span><span class="sxs-lookup"><span data-stu-id="154b1-247">Keep hello app running, as it's required tooperform hello next step.</span></span>
2. <span data-ttu-id="154b1-248">Kopieer en plak Hallo-adres van de opdrachtprompt Hallo in een browser toosee Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="154b1-248">Copy and paste hello address from hello command prompt into a browser toosee hello image.</span></span>
3. <span data-ttu-id="154b1-249">Wanneer u klaar bent, drukt u op **Enter** in Hallo opdrachtprompt venster tooclose Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="154b1-249">When you are finished, press **Enter** in hello command prompt window tooclose hello app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="154b1-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="154b1-250">Next steps</span></span>
<span data-ttu-id="154b1-251">Nu u een toepassing die gebruikmaakt van Hallo Service Bus relay-service hebt gemaakt, gaat u naar Hallo toolearn meer artikelen over Azure Relay te volgen:</span><span class="sxs-lookup"><span data-stu-id="154b1-251">Now that you've built an application that uses hello Service Bus relay service, see hello following articles toolearn more about Azure Relay:</span></span>

* [<span data-ttu-id="154b1-252">Overzicht van Azure Service Bus-architectuur</span><span class="sxs-lookup"><span data-stu-id="154b1-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="154b1-253">Overzicht van Azure Relay</span><span class="sxs-lookup"><span data-stu-id="154b1-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="154b1-254">Hoe toouse Hallo WCF relay-service met .NET</span><span class="sxs-lookup"><span data-stu-id="154b1-254">How toouse hello WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com

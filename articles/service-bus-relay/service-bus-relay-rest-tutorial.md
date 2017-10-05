---
title: Zelfstudie Service Bus REST met Azure Relay | Microsoft Docs
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
ms.openlocfilehash: 0db9dbd2d2743907e3f0b259228201d4f5d0c3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-wcf-relay-rest-tutorial"></a><span data-ttu-id="bfaf7-103">Azure WCF Relay REST-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="bfaf7-103">Azure WCF Relay REST tutorial</span></span>

<span data-ttu-id="bfaf7-104">Deze zelfstudie wordt beschreven hoe u een eenvoudige Azure Relay-hosttoepassing een REST gebaseerde interface.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-104">This tutorial describes how to build a simple Azure Relay host application that exposes a REST-based interface.</span></span> <span data-ttu-id="bfaf7-105">Met REST kan een webclient, zoals een webbrowser, toegang krijgen tot de Service Bus-API's via HTTP-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-105">REST enables a web client, such as a web browser, to access the Service Bus APIs through HTTP requests.</span></span>

<span data-ttu-id="bfaf7-106">De Windows Communication Foundation (WCF) REST-programmeermodel gebruikt voor het maken van een REST-service op de Service Bus maakt gebruik van de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-106">The tutorial uses the Windows Communication Foundation (WCF) REST programming model to construct a REST service on Service Bus.</span></span> <span data-ttu-id="bfaf7-107">Zie [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) (WCF REST-programmeermodel) en [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) (Services ontwerpen en implementeren) in de WCF-documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-107">For more information, see [WCF REST Programming Model](/dotnet/framework/wcf/feature-details/wcf-web-http-programming-model) and [Designing and Implementing Services](/dotnet/framework/wcf/designing-and-implementing-services) in the WCF documentation.</span></span>

## <a name="step-1-create-a-namespace"></a><span data-ttu-id="bfaf7-108">Stap 1: Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="bfaf7-108">Step 1: Create a namespace</span></span>

<span data-ttu-id="bfaf7-109">Als u de relayfuncties in Azure wilt gebruiken, moet u eerst een servicenaamruimte maken.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-109">To begin using the relay features in Azure, you must first create a service namespace.</span></span> <span data-ttu-id="bfaf7-110">Een naamruimte biedt een scoping container voor het verwerken van Azure-resources in uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-110">A namespace provides a scoping container for addressing Azure resources within your application.</span></span> <span data-ttu-id="bfaf7-111">Volg [deze instructies](relay-create-namespace-portal.md) om een Relay-naamruimte te maken.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-111">Follow the [instructions here](relay-create-namespace-portal.md) to create a Relay namespace.</span></span>

## <a name="step-2-define-a-rest-based-wcf-service-contract-to-use-with-azure-relay"></a><span data-ttu-id="bfaf7-112">Stap 2: Een REST gebaseerd WCF-servicecontract voor gebruik met Azure Relay definiëren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-112">Step 2: Define a REST-based WCF service contract to use with Azure Relay</span></span>

<span data-ttu-id="bfaf7-113">Wanneer u een service WCF REST-stijl maakt, moet u het contract definiëren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-113">When you create a WCF REST-style service, you must define the contract.</span></span> <span data-ttu-id="bfaf7-114">Het contract geeft aan welke bewerkingen door de host worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-114">The contract specifies what operations the host supports.</span></span> <span data-ttu-id="bfaf7-115">Een servicebewerking kan worden beschouwd als een webservicemethode.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-115">A service operation can be thought of as a web service method.</span></span> <span data-ttu-id="bfaf7-116">Contracten worden gemaakt door een C++-, C#- of Visual Basic-interface te definiëren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-116">Contracts are created by defining a C++, C#, or Visual Basic interface.</span></span> <span data-ttu-id="bfaf7-117">Elke methode in de interface komt overeen met een specifieke servicebewerking.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-117">Each method in the interface corresponds to a specific service operation.</span></span> <span data-ttu-id="bfaf7-118">Op elke interface moet het kenmerk [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) worden toegepast en op elke bewerking moet het kenmerk [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-118">The [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) attribute must be applied to each interface, and the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx) attribute must be applied to each operation.</span></span> <span data-ttu-id="bfaf7-119">Als een methode in een interface met het kenmerk [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) niet beschikt over het kenmerk [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), wordt die methode niet weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-119">If a method in an interface that has the [ServiceContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicecontractattribute.aspx) does not have the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx), that method is not exposed.</span></span> <span data-ttu-id="bfaf7-120">In het voorbeeld na de procedure wordt de code weergegeven die voor deze taken wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-120">The code used for these tasks is shown in the example following the procedure.</span></span>

<span data-ttu-id="bfaf7-121">Het belangrijkste verschil tussen een WCF-contract en een REST-stijlcontract is de toevoeging van een eigenschap aan de [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span><span class="sxs-lookup"><span data-stu-id="bfaf7-121">The primary difference between a WCF contract and a REST-style contract is the addition of a property to the [OperationContractAttribute](https://msdn.microsoft.com/library/system.servicemodel.operationcontractattribute.aspx): [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx).</span></span> <span data-ttu-id="bfaf7-122">Met deze eigenschap kunt u een methode in uw interface toewijzen aan een methode aan de andere kant van de interface.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-122">This property enables you to map a method in your interface to a method on the other side of the interface.</span></span> <span data-ttu-id="bfaf7-123">In dit geval wordt [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) gebruikt om een methode te koppelen aan HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-123">In this case, we will use [WebGetAttribute](https://msdn.microsoft.com/library/system.servicemodel.web.webgetattribute.aspx) to link a method to HTTP GET.</span></span> <span data-ttu-id="bfaf7-124">Hierdoor kan Service Bus opdrachten die naar de interface worden verzonden, correct ophalen en interpreteren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-124">This allows Service Bus to accurately retrieve and interpret commands sent to the interface.</span></span>

### <a name="to-create-a-contract-with-an-interface"></a><span data-ttu-id="bfaf7-125">Een contract met een interface maken</span><span class="sxs-lookup"><span data-stu-id="bfaf7-125">To create a contract with an interface</span></span>

1. <span data-ttu-id="bfaf7-126">Open Visual Studio als beheerder: klik met de rechtermuisknop op het programma in het menu **Start** en klik vervolgens op **Als administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-126">Open Visual Studio as an administrator: right-click the program in the **Start** menu, and then click **Run as administrator**.</span></span>
2. <span data-ttu-id="bfaf7-127">Maak een nieuw consoletoepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-127">Create a new console application project.</span></span> <span data-ttu-id="bfaf7-128">Klik op het menu **Bestand**, selecteer **Nieuw** en selecteer vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-128">Click the **File** menu and select **New**, then select **Project**.</span></span> <span data-ttu-id="bfaf7-129">Klik in het dialoogvenster **Nieuw project** op **Visual C#**, selecteer de sjabloon **Consoletoepassing** en geef deze de naam **ImageListener**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-129">In the **New Project** dialog box, click **Visual C#**, select the **Console Application** template, and name it **ImageListener**.</span></span> <span data-ttu-id="bfaf7-130">Gebruik de standaardwaarde voor **Locatie**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-130">Use the default **Location**.</span></span> <span data-ttu-id="bfaf7-131">Klik op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-131">Click **OK** to create the project.</span></span>
3. <span data-ttu-id="bfaf7-132">Voor een C#-project maakt Visual Studio een `Program.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-132">For a C# project, Visual Studio creates a `Program.cs` file.</span></span> <span data-ttu-id="bfaf7-133">Deze klasse bevat een lege `Main()`-methode, vereist voor de juiste opbouw van een consoletoepassingsproject.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-133">This class contains an empty `Main()` method, required for a console application project to build correctly.</span></span>
4. <span data-ttu-id="bfaf7-134">Voeg verwijzingen naar Service Bus en **System.ServiceModel.dll** aan het project toe door het Service Bus NuGet-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-134">Add references to Service Bus and **System.ServiceModel.dll** to the project by installing the Service Bus NuGet package.</span></span> <span data-ttu-id="bfaf7-135">Met dit pakket worden automatisch verwijzingen naar de Service Bus-bibliotheken en naar het **System.ServiceModel** van WCF toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-135">This package automatically adds references to the Service Bus libraries, as well as the WCF **System.ServiceModel**.</span></span> <span data-ttu-id="bfaf7-136">Klik in Solution Explorer met de rechtermuisknop op het project **ImageListener** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-136">In Solution Explorer, right-click the **ImageListener** project, and then click **Manage NuGet Packages**.</span></span> <span data-ttu-id="bfaf7-137">Klik op het tabblad **Bladeren** en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-137">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="bfaf7-138">Klik op **Installeren** en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-138">Click **Install**, and accept the terms of use.</span></span>
5. <span data-ttu-id="bfaf7-139">U moet expliciet een verwijzing naar **System.ServiceModel.Web.dll** toevoegen aan het project:</span><span class="sxs-lookup"><span data-stu-id="bfaf7-139">You must explicitly add a reference to **System.ServiceModel.Web.dll** to the project:</span></span>
   
    <span data-ttu-id="bfaf7-140">a.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-140">a.</span></span> <span data-ttu-id="bfaf7-141">Klik in Solution Explorer met de rechtermuisknop op de map **Verwijzingen** in de projectmap en klik vervolgens op **Verwijzing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-141">In Solution Explorer, right-click the **References** folder under the project folder and then click **Add Reference**.</span></span>
   
    <span data-ttu-id="bfaf7-142">b.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-142">b.</span></span> <span data-ttu-id="bfaf7-143">Klik in het dialoogvenster **Verwijzing toevoegen** op het tabblad **Framework** aan de linkerkant en typ **System.ServiceModel.Web** in het vak **Zoeken**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-143">In the **Add Reference** dialog box, click the **Framework** tab on the left-hand side and in the **Search** box, type **System.ServiceModel.Web**.</span></span> <span data-ttu-id="bfaf7-144">Schakel het selectievakje **System.ServiceModel.Web** in en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-144">Select the **System.ServiceModel.Web** check box, then click **OK**.</span></span>
6. <span data-ttu-id="bfaf7-145">Voeg aan het begin van het bestand Program.cs de volgende `using`-instructies toe:</span><span class="sxs-lookup"><span data-stu-id="bfaf7-145">Add the following `using` statements at the top of the Program.cs file.</span></span>
   
    ```csharp
    using System.ServiceModel;
    using System.ServiceModel.Channels;
    using System.ServiceModel.Web;
    using System.IO;
    ```
   
    <span data-ttu-id="bfaf7-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is de naamruimte die programmatisch toegang biedt tot de basisfuncties van WCF.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-146">[System.ServiceModel](https://msdn.microsoft.com/library/system.servicemodel.aspx) is the namespace that enables programmatic access to basic features of WCF.</span></span> <span data-ttu-id="bfaf7-147">Relay WCF maakt gebruik van veel van de objecten en kenmerken van WCF om servicecontracten te definiëren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-147">WCF Relay uses many of the objects and attributes of WCF to define service contracts.</span></span> <span data-ttu-id="bfaf7-148">U gebruikt deze naamruimte in de meeste van de relay-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-148">You will use this namespace in most of your relay applications.</span></span> <span data-ttu-id="bfaf7-149">Op deze manier [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helpt bij het definiëren het kanaal, dit is het object waarmee u met Azure Relay en de clientwebbrowser communiceren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-149">Similarly, [System.ServiceModel.Channels](https://msdn.microsoft.com/library/system.servicemodel.channels.aspx) helps define the channel, which is the object through which you communicate with Azure Relay and the client web browser.</span></span> <span data-ttu-id="bfaf7-150">Tot slot bevat [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) de typen waarmee u webtoepassingen kunt maken.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-150">Finally, [System.ServiceModel.Web](https://msdn.microsoft.com/library/system.servicemodel.web.aspx) contains the types that enable you to create web-based applications.</span></span>
7. <span data-ttu-id="bfaf7-151">Wijzig de naam van de naamruimte `ImageListener` in **Microsoft.ServiceBus.Samples**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-151">Rename the `ImageListener` namespace to **Microsoft.ServiceBus.Samples**.</span></span>
   
    ```csharp
    namespace Microsoft.ServiceBus.Samples
    {
        ...
    ```
8. <span data-ttu-id="bfaf7-152">Definieer meteen na de openingsaccolade van de naamruimtedeclaratie een nieuwe interface met de naam **IImageContract** en pas het kenmerk **ServiceContractAttribute** met de waarde `http://samples.microsoft.com/ServiceModel/Relay/` toe op de interface.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-152">Directly after the opening curly brace of the namespace declaration, define a new interface named **IImageContract** and apply the **ServiceContractAttribute** attribute to the interface with a value of `http://samples.microsoft.com/ServiceModel/Relay/`.</span></span> <span data-ttu-id="bfaf7-153">De naamruimtewaarde verschilt van de naamruimte die u in uw code gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-153">The namespace value differs from the namespace that you use throughout the scope of your code.</span></span> <span data-ttu-id="bfaf7-154">De naamruimtewaarde wordt gebruikt als een unieke id voor dit contract en moet versie-informatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-154">The namespace value is used as a unique identifier for this contract, and should have version information.</span></span> <span data-ttu-id="bfaf7-155">Zie [Serviceversiebeheer](http://go.microsoft.com/fwlink/?LinkID=180498) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-155">For more information, see [Service Versioning](http://go.microsoft.com/fwlink/?LinkID=180498).</span></span> <span data-ttu-id="bfaf7-156">Door de naamruimte expliciet op te geven, wordt voorkomen dat de standaardnaamruimtewaarde wordt toegevoegd aan de naam van het contract.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-156">Specifying the namespace explicitly prevents the default namespace value from being added to the contract name.</span></span>
   
    ```csharp
    [ServiceContract(Name = "ImageContract", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/RESTTutorial1")]
    public interface IImageContract
    {
    }
    ```
9. <span data-ttu-id="bfaf7-157">Declareer in de `IImageContract`-interface een methode voor de enkelvoudige bewerking die door het `IImageContract`-contract wordt weergegeven in de interface en pas het kenmerk `OperationContractAttribute` toe op de methode die u wilt weergeven als onderdeel van het openbare Service Bus-contract.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-157">Within the `IImageContract` interface, declare a method for the single operation the `IImageContract` contract exposes in the interface and apply the `OperationContractAttribute` attribute to the method that you want to expose as part of the public Service Bus contract.</span></span>
   
    ```csharp
    public interface IImageContract
    {
        [OperationContract]
        Stream GetImage();
    }
    ```
10. <span data-ttu-id="bfaf7-158">Voeg de waarde **WebGet** toe aan het kenmerk **OperationContract**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-158">In the **OperationContract** attribute, add the **WebGet** value.</span></span>
    
    ```csharp
    public interface IImageContract
    {
        [OperationContract, WebGet]
        Stream GetImage();
    }
    ```
    
    <span data-ttu-id="bfaf7-159">In dat geval schakelt de relay-service op route HTTP GET aanvragen om te doen `GetImage`, en de retourwaarden van vertalen `GetImage` in een HTTP GETRESPONSE-antwoord.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-159">Doing so enables the relay service to route HTTP GET requests to `GetImage`, and to translate the return values of `GetImage` into an HTTP GETRESPONSE reply.</span></span> <span data-ttu-id="bfaf7-160">Verderop in de zelfstudie gebruikt u een webbrowser om toegang te krijgen tot deze methode en de installatiekopie weer te geven in de browser.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-160">Later in the tutorial, you will use a web browser to access this method, and to display the image in the browser.</span></span>
11. <span data-ttu-id="bfaf7-161">Declareer direct na de `IImageContract`-definitie een kanaal dat de eigenschappen overneemt van de `IImageContract`- en `IClientChannel`-interface.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-161">Directly after the `IImageContract` definition, declare a channel that inherits from both the `IImageContract` and `IClientChannel` interfaces.</span></span>
    
    ```csharp
    public interface IImageChannel : IImageContract, IClientChannel { }
    ```
    
    <span data-ttu-id="bfaf7-162">Een kanaal is het WCF-object waarmee de service en de client informatie aan elkaar doorgeven.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-162">A channel is the WCF object through which the service and client pass information to each other.</span></span> <span data-ttu-id="bfaf7-163">U maakt het kanaal later in uw hosttoepassing.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-163">Later, you will create the channel in your host application.</span></span> <span data-ttu-id="bfaf7-164">Azure Relay gebruikt dit kanaal om door te geven van de HTTP GET-aanvragen van de browser uw **GetImage** implementatie.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-164">Azure Relay then uses this channel to pass the HTTP GET requests from the browser to your **GetImage** implementation.</span></span> <span data-ttu-id="bfaf7-165">De relay gebruikt dit kanaal ook te laten de **GetImage** waarde retourneren en zet deze om naar een HTTP GETRESPONSE voor de clientbrowser.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-165">The relay also uses the channel to take the **GetImage** return value and translate it into an HTTP GETRESPONSE for the client browser.</span></span>
12. <span data-ttu-id="bfaf7-166">Klik in het menu **Bouwen** op **Oplossing opbouwen** om de juistheid van uw werk tot nu toe te controleren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-166">From the **Build** menu, click **Build Solution** to confirm the accuracy of your work so far.</span></span>

### <a name="example"></a><span data-ttu-id="bfaf7-167">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bfaf7-167">Example</span></span>
<span data-ttu-id="bfaf7-168">De volgende code toont een eenvoudige interface die een Relay WCF-contract wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-168">The following code shows a basic interface that defines a WCF Relay contract.</span></span>

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

## <a name="step-3-implement-a-rest-based-wcf-service-contract-to-use-service-bus"></a><span data-ttu-id="bfaf7-169">Stap 3: een op REST gebaseerd WCF-servicecontract voor gebruik met Service Bus implementeren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-169">Step 3: Implement a REST-based WCF service contract to use Service Bus</span></span>
<span data-ttu-id="bfaf7-170">Maken van een REST-stijl WCF Relay-service, moet u eerst het contract, die is gedefinieerd met behulp van een interface maken.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-170">Creating a REST-style WCF Relay service requires that you first create the contract, which is defined by using an interface.</span></span> <span data-ttu-id="bfaf7-171">De volgende stap is het implementeren van de interface.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-171">The next step is to implement the interface.</span></span> <span data-ttu-id="bfaf7-172">Hiervoor moet u een klasse met de naam **ImageService** maken die de door de gebruiker gedefinieerde **IImageContract**-interface implementeert.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-172">This involves creating a class named **ImageService** that implements the user-defined **IImageContract** interface.</span></span> <span data-ttu-id="bfaf7-173">Nadat het contract is geïmplementeerd, configureert u de interface met een App.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-173">After you implement the contract, you then configure the interface using an App.config file.</span></span> <span data-ttu-id="bfaf7-174">Het configuratiebestand bevat de benodigde informatie voor de toepassing, zoals de naam van de service, de naam van het contract en het type protocol dat wordt gebruikt om te communiceren met de relay-service.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-174">The configuration file contains necessary information for the application, such as the name of the service, the name of the contract, and the type of protocol that is used to communicate with the relay service.</span></span> <span data-ttu-id="bfaf7-175">In het voorbeeld na de procedure wordt de code weergegeven die voor deze taken wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-175">The code used for these tasks is provided in the example following the procedure.</span></span>

<span data-ttu-id="bfaf7-176">Net als bij de vorige stappen, is er weinig verschil tussen het implementeren van een REST-stijlcontract en een Relay WCF-contract.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-176">As with the previous steps, there is very little difference between implementing a REST-style contract and a WCF Relay contract.</span></span>

### <a name="to-implement-a-rest-style-service-bus-contract"></a><span data-ttu-id="bfaf7-177">Een Service Bus-contract in REST-stijl implementeren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-177">To implement a REST-style Service Bus contract</span></span>
1. <span data-ttu-id="bfaf7-178">Maak een nieuwe klasse met de naam **ImageService** direct na de definitie van de **IImageContract**-interface.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-178">Create a new class named **ImageService** directly after the definition of the **IImageContract** interface.</span></span> <span data-ttu-id="bfaf7-179">Met de klasse **ImageService** wordt de **IImageContract**-interface geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-179">The **ImageService** class implements the **IImageContract** interface.</span></span>
   
    ```csharp
    class ImageService : IImageContract
    {
    }
    ```
    <span data-ttu-id="bfaf7-180">Net als bij andere interface-implementaties kunt u de definitie implementeren in een ander bestand.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-180">Similar to other interface implementations, you can implement the definition in a different file.</span></span> <span data-ttu-id="bfaf7-181">In deze zelfstudie wordt de implementatie echter weergegeven in hetzelfde bestand als de interfacedefinitie en de `Main()`-methode.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-181">However, for this tutorial, the implementation appears in the same file as the interface definition and `Main()` method.</span></span>
2. <span data-ttu-id="bfaf7-182">Pas het kenmerk [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) op de klasse **IImageService** toe om aan te geven dat de klasse een implementatie is van een WCF-contract.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-182">Apply the [ServiceBehaviorAttribute](https://msdn.microsoft.com/library/system.servicemodel.servicebehaviorattribute.aspx) attribute to the **IImageService** class to indicate that the class is an implementation of a WCF contract.</span></span>
   
    ```csharp
    [ServiceBehavior(Name = "ImageService", Namespace = "http://samples.microsoft.com/ServiceModel/Relay/")]
    class ImageService : IImageContract
    {
    }
    ```
   
    <span data-ttu-id="bfaf7-183">Zoals eerder is vermeld, is deze naamruimte geen traditionele naamruimte,</span><span class="sxs-lookup"><span data-stu-id="bfaf7-183">As mentioned previously, this namespace is not a traditional namespace.</span></span> <span data-ttu-id="bfaf7-184">maar maakt deze deel uit van de WCF-architectuur waarmee het contract wordt geïdentificeerd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-184">Instead, it is part of the WCF architecture that identifies the contract.</span></span> <span data-ttu-id="bfaf7-185">Zie het onderwerp [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) (Gegevenscontractnamen) in de WCF-documentatie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-185">For more information, see the [Data Contract Names](https://msdn.microsoft.com/library/ms731045.aspx) topic in the WCF documentation.</span></span>
3. <span data-ttu-id="bfaf7-186">Voeg een JPG-afbeelding toe aan uw project.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-186">Add a .jpg image to your project.</span></span>  
   
    <span data-ttu-id="bfaf7-187">Dit is een afbeelding die de service in de ontvangende browser weergeeft.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-187">This is a picture that the service displays in the receiving browser.</span></span> <span data-ttu-id="bfaf7-188">Klik met de rechtermuisknop op het project en klik op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-188">Right-click your project, then click **Add**.</span></span> <span data-ttu-id="bfaf7-189">Klik vervolgens op **Bestaand item**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-189">Then click **Existing Item**.</span></span> <span data-ttu-id="bfaf7-190">Gebruik het dialoogvenster **Bestaand item toevoegen** om te bladeren naar een geschikt JPG-bestand en klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-190">Use the **Add Existing Item** dialog box to browse to an appropriate .jpg, and then click **Add**.</span></span>
   
    <span data-ttu-id="bfaf7-191">Als u het bestand toevoegt, moet u ervoor zorgen dat **Alle bestanden** is geselecteerd in de vervolgkeuzelijst naast het veld **Bestandsnaam:**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-191">When adding the file, make sure that **All Files** is selected in the drop-down list next to the **File name:** field.</span></span> <span data-ttu-id="bfaf7-192">In de rest van deze zelfstudie wordt ervan uitgegaan dat de naam van de afbeelding 'image.jpg' is.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-192">The rest of this tutorial assumes that the name of the image is "image.jpg".</span></span> <span data-ttu-id="bfaf7-193">Als u een ander bestand gebruikt, moet u de naam van de afbeelding wijzigen of moet u uw code wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-193">If you have a different file, you will have to rename the image, or change your code to compensate.</span></span>
4. <span data-ttu-id="bfaf7-194">Klik in **Solution Explorer** met de rechtermuisknop op het afbeeldingsbestand en klik op **Eigenschappen** om te controleren of de service die wordt uitgevoerd het affbeeldingsbestand kan vinden.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-194">To make sure that the running service can find the image file, in **Solution Explorer** right-click the image file, then click **Properties**.</span></span> <span data-ttu-id="bfaf7-195">Stel **Naar uitvoermap kopiëren** in het deelvenster **Eigenschappen** in op **Kopiëren indien nieuwer**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-195">In the **Properties** pane, set **Copy to Output Directory** to **Copy if newer**.</span></span>
5. <span data-ttu-id="bfaf7-196">Voeg een verwijzing naar de **System.Drawing.dll**-assembly toe aan het project en voeg tevens de volgende gekoppelde `using`-instructies toe.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-196">Add a reference to the **System.Drawing.dll** assembly to the project, and also add the following associated `using` statements.</span></span>  
   
    ```csharp
    using System.Drawing;
    using System.Drawing.Imaging;
    using Microsoft.ServiceBus;
    using Microsoft.ServiceBus.Web;
    ```
6. <span data-ttu-id="bfaf7-197">Voeg in de klasse **ImageService** de volgende constructor toe waarmee de bitmap wordt geladen en voorbereid op verzending naar de clientbrowser.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-197">In the **ImageService** class, add the following constructor that loads the bitmap and prepares to send it to the client browser.</span></span>
   
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
7. <span data-ttu-id="bfaf7-198">Voeg direct na de vorige code de volgende **GetImage**-methode toe aan de klasse **ImageService** om een HTTP-bericht met de afbeelding te retourneren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-198">Directly after the previous code, add the following **GetImage** method in the **ImageService** class to return an HTTP message that contains the image.</span></span>
   
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
   
    <span data-ttu-id="bfaf7-199">Deze implementatie maakt gebruik van **MemoryStream** om de afbeelding op te halen en deze voor te bereiden op streaming naar de browser.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-199">This implementation uses **MemoryStream** to retrieve the image and prepare it for streaming to the browser.</span></span> <span data-ttu-id="bfaf7-200">De streampositie start bij nul, de stream wordt gedeclareerd als JPEG en de gegevens worden gestreamd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-200">It starts the stream position at zero, declares the stream content as a jpeg, and streams the information.</span></span>
8. <span data-ttu-id="bfaf7-201">Klik in het menu **Bouwen** op **Oplossing opbouwen**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-201">From the **Build** menu, click **Build Solution**.</span></span>

### <a name="to-define-the-configuration-for-running-the-web-service-on-service-bus"></a><span data-ttu-id="bfaf7-202">De configuratie voor het uitvoeren van de webservice in Service Bus definiëren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-202">To define the configuration for running the web service on Service Bus</span></span>
1. <span data-ttu-id="bfaf7-203">Dubbelklik in **Solution Explorer** op het bestand **App.config** om dit te openen in de Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-203">In **Solution Explorer**, double-click **App.config** to open it in the Visual Studio editor.</span></span>
   
    <span data-ttu-id="bfaf7-204">De **App.config** bestand bevat de servicenaam, het eindpunt (dat wil zeggen, de locatie die Azure Relay biedt voor clients en hosts om te communiceren met elkaar) en de binding (het type protocol dat wordt gebruikt voor communicatie).</span><span class="sxs-lookup"><span data-stu-id="bfaf7-204">The **App.config** file includes the service name, endpoint (that is, the location Azure Relay exposes for clients and hosts to communicate with each other), and binding (the type of protocol that is used to communicate).</span></span> <span data-ttu-id="bfaf7-205">Hier het belangrijkste verschil is dat het geconfigureerde service-eindpunt naar verwijst een [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-205">The main difference here is that the configured service endpoint refers to a [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding.</span></span>
2. <span data-ttu-id="bfaf7-206">Het `<system.serviceModel>` XML-element is een WCF-element waarmee een of meer services worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-206">The `<system.serviceModel>` XML element is a WCF element that defines one or more services.</span></span> <span data-ttu-id="bfaf7-207">Hier wordt het gebruikt om de servicenaam en het eindpunt te definiëren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-207">Here, it is used to define the service name and endpoint.</span></span> <span data-ttu-id="bfaf7-208">Voeg onder aan het `<system.serviceModel>`-element (maar nog wel binnen `<system.serviceModel>`) een `<bindings>`-element toe met de volgende inhoud.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-208">At the bottom of the `<system.serviceModel>` element (but still within `<system.serviceModel>`), add a `<bindings>` element that has the following content.</span></span> <span data-ttu-id="bfaf7-209">Hiermee definieert u de bindingen die in de toepassing worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-209">This defines the bindings used in the application.</span></span> <span data-ttu-id="bfaf7-210">U kunt meerdere bindingen definiëren, maar in deze zelfstudie definieert u er slechts één.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-210">You can define multiple bindings, but for this tutorial you are defining only one.</span></span>
   
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
   
    <span data-ttu-id="bfaf7-211">De vorige code definieert een Relay WCF [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding met **relayClientAuthenticationType** ingesteld op **geen**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-211">The previous code defines a WCF Relay [WebHttpRelayBinding](/dotnet/api/microsoft.servicebus.webhttprelaybinding) binding with **relayClientAuthenticationType** set to **None**.</span></span> <span data-ttu-id="bfaf7-212">Met deze instelling geeft u aan dat voor een eindpunt dat deze binding gebruikt, geen clientreferentie is vereist.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-212">This setting indicates that an endpoint using this binding does not require a client credential.</span></span>
3. <span data-ttu-id="bfaf7-213">Na het `<bindings>`-element voegt u een `<services>`-element toe.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-213">After the `<bindings>` element, add a `<services>` element.</span></span> <span data-ttu-id="bfaf7-214">Net zoals bij bindingen kunt u meerdere services definiëren in een enkel configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-214">Similar to the bindings, you can define multiple services in a single configuration file.</span></span> <span data-ttu-id="bfaf7-215">In deze zelfstudie definieert u slechts een service.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-215">However, for this tutorial, you define only one.</span></span>
   
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
   
    <span data-ttu-id="bfaf7-216">In deze stap configureert u een service die de vooraf gedefinieerde **webHttpRelayBinding**-binding gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-216">This step configures a service that uses the previously defined default **webHttpRelayBinding**.</span></span> <span data-ttu-id="bfaf7-217">Deze service gebruikt ook de standaard **sbTokenProvider**, die in de volgende stap wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-217">It also uses the default **sbTokenProvider**, which is defined in the next step.</span></span>
4. <span data-ttu-id="bfaf7-218">Na de `<services>` element, maakt een `<behaviors>` element met de volgende inhoud en vervang 'sas_key ' vervangen door de *Shared Access Signature* sleutel (SAS) u eerder hebt verkregen via de [Azure-portal] [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="bfaf7-218">After the `<services>` element, create a `<behaviors>` element with the following content, replacing "SAS_KEY" with the *Shared Access Signature* (SAS) key you previously obtained from the [Azure portal][Azure portal].</span></span>
   
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
5. <span data-ttu-id="bfaf7-219">Terwijl App.config actief is, vervangt u in het `<appSettings>`-element de hele verbindingsreekswaarde door de verbindingsreeks die u eerder hebt verkregen via de portal.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-219">Still in App.config, in the `<appSettings>` element, replace the entire connection string value with the connection string you previously obtained from the portal.</span></span> 
   
    ```xml
    <appSettings>
       <!-- Service Bus specific app settings for messaging connections -->
       <add key="Microsoft.ServiceBus.ConnectionString"
           value="Endpoint=sb://yourNamespace.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=YOUR_SAS_KEY"/>
    </appSettings>
    ```
6. <span data-ttu-id="bfaf7-220">Klik in het menu **Bouwen** op **Oplossing opbouwen** om de volledige oplossing op te bouwen.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-220">From the **Build** menu, click **Build Solution** to build the entire solution.</span></span>

### <a name="example"></a><span data-ttu-id="bfaf7-221">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bfaf7-221">Example</span></span>
<span data-ttu-id="bfaf7-222">De volgende code toont het contract en de service-implementatie voor een op REST gebaseerde service die in Service Bus wordt uitgevoerd met de binding **WebHttpRelayBinding**.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-222">The following code shows the contract and service implementation for a REST-based service that is running on  Service Bus using the **WebHttpRelayBinding** binding.</span></span>

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

<span data-ttu-id="bfaf7-223">In het volgende voorbeeld wordt het aan de service gekoppelde bestand App.config weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-223">The following example shows the App.config file associated with the service.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2"/>
    </startup>
    <system.serviceModel>
        <extensions>
            <!-- In this extension section we are introducing all known service bus extensions. User can remove the ones they don't need. -->
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

## <a name="step-4-host-the-rest-based-wcf-service-to-use-azure-relay"></a><span data-ttu-id="bfaf7-224">Stap 4: De REST gebaseerd WCF-service voor het gebruik van Azure Relay hosten</span><span class="sxs-lookup"><span data-stu-id="bfaf7-224">Step 4: Host the REST-based WCF service to use Azure Relay</span></span>
<span data-ttu-id="bfaf7-225">Deze stap wordt beschreven hoe een webservice met een consoletoepassing met WCF Relay uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-225">This step describes how to run a web service using a console application with WCF Relay.</span></span> <span data-ttu-id="bfaf7-226">Een volledig overzicht van de code die in deze stap wordt geschreven, vindt u in het voorbeeld na de procedure.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-226">A complete listing of the code written in this step is provided in the example following the procedure.</span></span>

### <a name="to-create-a-base-address-for-the-service"></a><span data-ttu-id="bfaf7-227">Een basisadres voor de service maken</span><span class="sxs-lookup"><span data-stu-id="bfaf7-227">To create a base address for the service</span></span>
1. <span data-ttu-id="bfaf7-228">In de `Main()` declaratie van de functie, maakt u een variabele voor het opslaan van de naamruimte van uw project.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-228">In the `Main()` function declaration, create a variable to store the namespace of your project.</span></span> <span data-ttu-id="bfaf7-229">Zorg ervoor dat u `yourNamespace` met de naam van de Relay-naamruimte die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-229">Make sure to replace `yourNamespace` with the name of the Relay namespace you created previously.</span></span>
   
    ```csharp
    string serviceNamespace = "yourNamespace";
    ```
    <span data-ttu-id="bfaf7-230">Service Bus gebruikt de naam van uw naamruimte om een unieke URI te maken.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-230">Service Bus uses the name of your namespace to create a unique URI.</span></span>
2. <span data-ttu-id="bfaf7-231">Maak een `Uri`-exemplaar voor het basisadres van de service die is gebaseerd op de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-231">Create a `Uri` instance for the base address of the service that is based on the namespace.</span></span>
   
    ```csharp
    Uri address = ServiceBusEnvironment.CreateServiceUri("https", serviceNamespace, "Image");
    ```

### <a name="to-create-and-configure-the-web-service-host"></a><span data-ttu-id="bfaf7-232">De webservicehost maken en configureren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-232">To create and configure the web service host</span></span>
* <span data-ttu-id="bfaf7-233">Maak de webservicehost met het URI-adres dat u eerder in dit gedeelte hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-233">Create the web service host, using the URI address created earlier in this section.</span></span>
  
    ```csharp
    WebServiceHost host = new WebServiceHost(typeof(ImageService), address);
    ```
    <span data-ttu-id="bfaf7-234">De servicehost is het WCF-object waarmee de hosttoepassing wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-234">The service host is the WCF object that instantiates the host application.</span></span> <span data-ttu-id="bfaf7-235">In dit voorbeeld wordt het type host dat u wilt maken (een **ImageService**), doorgegeven en ook het adres waarop u de hosttoepassing wilt weergeven.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-235">This example passes it the type of host you want to create (an **ImageService**), and also the address at which you want to expose the host application.</span></span>

### <a name="to-run-the-web-service-host"></a><span data-ttu-id="bfaf7-236">De webservicehost uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-236">To run the web service host</span></span>
1. <span data-ttu-id="bfaf7-237">Open de service.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-237">Open the service.</span></span>
   
    ```csharp
    host.Open();
    ```
    <span data-ttu-id="bfaf7-238">De service wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-238">The service is now running.</span></span>
2. <span data-ttu-id="bfaf7-239">Geef een bericht weer waarin wordt aangegeven dat de service wordt uitgevoerd en hoe deze kan worden gestopt.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-239">Display a message indicating that the service is running, and how to stop the service.</span></span>
   
    ```csharp
    Console.WriteLine("Copy the following address into a browser to see the image: ");
    Console.WriteLine(address + "GetImage");
    Console.WriteLine();
    Console.WriteLine("Press [Enter] to exit");
    Console.ReadLine();
    ```
3. <span data-ttu-id="bfaf7-240">Sluit de servicehost wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-240">When finished, close the service host.</span></span>
   
    ```csharp
    host.Close();
    ```

## <a name="example"></a><span data-ttu-id="bfaf7-241">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bfaf7-241">Example</span></span>
<span data-ttu-id="bfaf7-242">Het volgende voorbeeld bevat het servicecontract en de implementatie uit de vorige stappen in de zelfstudie. Hierin wordt de service gehost in een consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-242">The following example includes the service contract and implementation from previous steps in the tutorial and hosts the service in a console application.</span></span> <span data-ttu-id="bfaf7-243">Compileer de volgende code in een uitvoerbaar bestand met de naam ImageListener.exe.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-243">Compile the following code into an executable named ImageListener.exe.</span></span>

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

            Console.WriteLine("Copy the following address into a browser to see the image: ");
            Console.WriteLine(address + "GetImage");
            Console.WriteLine();
            Console.WriteLine("Press [Enter] to exit");
            Console.ReadLine();

            host.Close();
        }
    }
}
```

### <a name="compiling-the-code"></a><span data-ttu-id="bfaf7-244">De code compileren</span><span class="sxs-lookup"><span data-stu-id="bfaf7-244">Compiling the code</span></span>
<span data-ttu-id="bfaf7-245">Nadat u de oplossing hebt opgebouwd, gaat u als volgt te werk om de toepassing uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="bfaf7-245">After building the solution, do the following to run the application:</span></span>

1. <span data-ttu-id="bfaf7-246">Druk op **F5** of blader naar de locatie van het uitvoerbare bestand (ImageListener\bin\Debug\ImageListener.exe) om de service uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-246">Press **F5**, or browse to the executable file location (ImageListener\bin\Debug\ImageListener.exe), to run the service.</span></span> <span data-ttu-id="bfaf7-247">Zorg ervoor dat de app actief blijft. Dit is vereist voor het uitvoeren van de volgende stap.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-247">Keep the app running, as it's required to perform the next step.</span></span>
2. <span data-ttu-id="bfaf7-248">Kopieer en plak het adres van de opdrachtprompt in een browser om de afbeelding te zien.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-248">Copy and paste the address from the command prompt into a browser to see the image.</span></span>
3. <span data-ttu-id="bfaf7-249">Druk op **Enter** in het opdrachtpromptvenster om de app te sluiten wanneer u klaar bent.</span><span class="sxs-lookup"><span data-stu-id="bfaf7-249">When you are finished, press **Enter** in the command prompt window to close the app.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bfaf7-250">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bfaf7-250">Next steps</span></span>
<span data-ttu-id="bfaf7-251">Nu u een toepassing die gebruikmaakt van de Service Bus relay-service hebt gemaakt, gaat u naar de volgende artikelen voor meer informatie over Azure Relay:</span><span class="sxs-lookup"><span data-stu-id="bfaf7-251">Now that you've built an application that uses the Service Bus relay service, see the following articles to learn more about Azure Relay:</span></span>

* [<span data-ttu-id="bfaf7-252">Overzicht van Azure Service Bus-architectuur</span><span class="sxs-lookup"><span data-stu-id="bfaf7-252">Azure Service Bus architectural overview</span></span>](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md)
* [<span data-ttu-id="bfaf7-253">Overzicht van Azure Relay</span><span class="sxs-lookup"><span data-stu-id="bfaf7-253">Azure Relay overview</span></span>](relay-what-is-it.md)
* [<span data-ttu-id="bfaf7-254">De relay WCF-service gebruiken met .NET</span><span class="sxs-lookup"><span data-stu-id="bfaf7-254">How to use the WCF relay service with .NET</span></span>](relay-wcf-dotnet-get-started.md)

[Azure portal]: https://portal.azure.com

---
title: .NET-toepassing met meerdere lagen die Azure Service Bus gebruikt | Microsoft Docs
description: Een .NET-zelfstudie waarmee u in Azure een app met meerdere lagen kunt ontwikkelen die Service Bus-wachtrijen gebruikt voor communicatie tussen lagen.
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 1b8608ca-aa5a-4700-b400-54d65b02615c
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: get-started-article
ms.date: 04/11/2017
ms.author: sethm
ms.openlocfilehash: 8b502f5ac5d89801d390a872e7a8b06e094ecbba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="3c9fe-103">.NET-toepassing met meerdere lagen die Azure Service Bus-wachtrijen gebruikt</span><span class="sxs-lookup"><span data-stu-id="3c9fe-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="3c9fe-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="3c9fe-104">Introduction</span></span>
<span data-ttu-id="3c9fe-105">Ontwikkelen voor Microsoft Azure is eenvoudig met Visual Studio en de gratis Azure SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-105">Developing for Microsoft Azure is easy using Visual Studio and the free Azure SDK for .NET.</span></span> <span data-ttu-id="3c9fe-106">In deze zelfstudie doorloopt u de stappen voor het maken van een toepassing die meerdere Azure-resources in uw lokale omgeving gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-106">This tutorial walks you through the steps to create an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="3c9fe-107">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="3c9fe-107">You will learn the following:</span></span>

* <span data-ttu-id="3c9fe-108">De computer met een enkele download en installatie instellen voor het ontwikkelen voor Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-108">How to enable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="3c9fe-109">Visual Studio gebruiken om te ontwikkelen voor Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-109">How to use Visual Studio to develop for Azure.</span></span>
* <span data-ttu-id="3c9fe-110">Een toepassing met meerdere lagen maken in Azure met de web- en werkrollen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-110">How to create a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="3c9fe-111">Communiceren tussen lagen met Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-111">How to communicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="3c9fe-112">In deze zelfstudie zult u de toepassing met meerdere lagen ontwikkelen en uitvoeren in een cloudservice van Azure.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-112">In this tutorial you'll build and run the multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="3c9fe-113">De front-end is een ASP.NET MVC-webrol en de back-end is een werkrol die gebruikmaakt van een Service Bus-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-113">The front end is an ASP.NET MVC web role and the back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="3c9fe-114">U kunt dezelfde toepassing met meerdere lagen maken met de front-end als een webproject dat wordt geïmplementeerd op een Azure-website in plaats van een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-114">You can create the same multi-tier application with the front end as a web project, that is deployed to an Azure website instead of a cloud service.</span></span> <span data-ttu-id="3c9fe-115">U kunt ook de zelfstudie [.NET on-premises/hybride cloud-toepassing](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-115">You can also try out the [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="3c9fe-116">In de volgende schermafbeelding wordt de voltooide toepassing weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-116">The following screen shot shows the completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="3c9fe-117">Scenario-overzicht: communicatie tussen rollen</span><span class="sxs-lookup"><span data-stu-id="3c9fe-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="3c9fe-118">Als u een order wilt indienen voor verwerking, moet het front-end UI-onderdeel, dat wordt uitgevoerd in de webrol, communiceren met de logica van de middelste laag, die wordt uitgevoerd in de werkrol.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-118">To submit an order for processing, the front-end UI component, running in the web role, must interact with the middle tier logic running in the worker role.</span></span> <span data-ttu-id="3c9fe-119">In dit voorbeeld wordt Service Bus Messaging gebruikt voor communicatie tussen de lagen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-119">This example uses Service Bus messaging for the communication between the tiers.</span></span>

<span data-ttu-id="3c9fe-120">Met behulp van Service Bus Messaging tussen de weblaag en de middelste laag worden de twee onderdelen losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-120">Using Service Bus messaging between the web and middle tiers decouples the two components.</span></span> <span data-ttu-id="3c9fe-121">In tegenstelling tot Direct Messaging (dat wil zeggen, TCP of HTTP) hoeft de weblaag niet rechtstreeks verbinding te maken met de middelste laag. In plaats daarvan worden werkeenheden, als berichten, naar Service Bus gepusht. Daar worden ze veilig bewaard totdat de middelste laag gereed is om ze te ontvangen en te verwerken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-121">In contrast to direct messaging (that is, TCP or HTTP), the web tier does not connect to the middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until the middle tier is ready to consume and process them.</span></span>

<span data-ttu-id="3c9fe-122">Service Bus biedt twee entiteiten ter ondersteuning van Brokered Messaging: wachtrijen en onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-122">Service Bus provides two entities to support brokered messaging: queues and topics.</span></span> <span data-ttu-id="3c9fe-123">Met wachtrijen wordt elk bericht dat naar de wachtrij wordt verzonden, verbruikt door een enkele ontvanger.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-123">With queues, each message sent to the queue is consumed by a single receiver.</span></span> <span data-ttu-id="3c9fe-124">Onderwerpen ondersteunen het patroon voor publiceren/abonneren waarin elk gepubliceerde bericht beschikbaar wordt gesteld aan een abonnement dat bij het onderwerp is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-124">Topics support the publish/subscribe pattern in which each published message is made available to a subscription registered with the topic.</span></span> <span data-ttu-id="3c9fe-125">Elk abonnement onderhoudt logisch gezien zijn eigen wachtrij met berichten.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="3c9fe-126">Abonnementen kunnen ook worden geconfigureerd met filterregels die de set berichten die wordt doorgegeven aan de abonnementenwachtrij beperken tot berichten die overeenkomen met het filter.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-126">Subscriptions can also be configured with filter rules that restrict the set of messages passed to the subscription queue to those that match the filter.</span></span> <span data-ttu-id="3c9fe-127">In het volgende voorbeeld wordt gebruikgemaakt van Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-127">The following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="3c9fe-128">Dit communicatiemechanisme heeft verschillende voordelen ten opzichte van Direct Messaging:</span><span class="sxs-lookup"><span data-stu-id="3c9fe-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="3c9fe-129">**Tijdelijke ontkoppeling.**</span><span class="sxs-lookup"><span data-stu-id="3c9fe-129">**Temporal decoupling.**</span></span> <span data-ttu-id="3c9fe-130">Met het asynchrone berichtenpatroon hoeven producenten en consumenten niet op hetzelfde moment online te zijn.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-130">With the asynchronous messaging pattern, producers and consumers need not be online at the same time.</span></span> <span data-ttu-id="3c9fe-131">Service Bus slaat de berichten veilig op totdat de verbruikende partij gereed is om de berichten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-131">Service Bus reliably stores messages until the consuming party is ready to receive them.</span></span> <span data-ttu-id="3c9fe-132">Hierdoor kunnen de onderdelen van de gedistribueerde toepassing worden losgekoppeld - hetzij vrijwillig, bijvoorbeeld voor onderhoud, hetzij vanwege het vastlopen van een onderdeel - zonder dat dit van invloed is op het systeem als geheel.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-132">This enables the components of the distributed application to be disconnected, either voluntarily, for example, for maintenance, or due to a component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="3c9fe-133">Bovendien hoeft de betreffende toepassing mogelijk alleen online te komen op bepaalde tijdstippen gedurende de dag.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-133">Furthermore, the consuming application might only need to come online during certain times of the day.</span></span>
* <span data-ttu-id="3c9fe-134">**Herverdeling van taken.**</span><span class="sxs-lookup"><span data-stu-id="3c9fe-134">**Load leveling.**</span></span> <span data-ttu-id="3c9fe-135">In veel toepassingen varieert de systeembelasting gedurende de tijd, terwijl de benodigde verwerkingstijd voor elke werkeenheid doorgaans constant blijft.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-135">In many applications, system load varies over time, while the processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="3c9fe-136">Door een wachtrij tussen producenten en consumenten van berichten te plaatsen, hoeft de verbruikende toepassing (de werkrol) alleen te worden ingericht voor het opvangen van een gemiddelde belasting in plaats van een piekbelasting.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-136">Intermediating message producers and consumers with a queue means that the consuming application (the worker) only needs to be provisioned to accommodate average load rather than peak load.</span></span> <span data-ttu-id="3c9fe-137">De lengte van de wachtrij neemt toe of af, al naargelang het binnenkomende verkeer.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-137">The depth of the queue grows and contracts as the incoming load varies.</span></span> <span data-ttu-id="3c9fe-138">Dit betekent een rechtstreekse besparing op de kosten voor de benodigde infrastructuur om de toepassingsbelasting te verwerken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-138">This directly saves money in terms of the amount of infrastructure required to service the application load.</span></span>
* <span data-ttu-id="3c9fe-139">**Taakverdeling.**</span><span class="sxs-lookup"><span data-stu-id="3c9fe-139">**Load balancing.**</span></span> <span data-ttu-id="3c9fe-140">Naarmate het verkeer toeneemt, kunnen meer werkprocessen worden toegevoegd om uit de wachtrij te lezen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-140">As load increases, more worker processes can be added to read from the queue.</span></span> <span data-ttu-id="3c9fe-141">Elk bericht worden door slechts één van de werkprocessen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-141">Each message is processed by only one of the worker processes.</span></span> <span data-ttu-id="3c9fe-142">Bovendien biedt deze pull-gebaseerde taakverdeling optimaal gebruik van de werkmachines, zelfs als de verwerkingskracht van de werkmachines verschilt en ze op eigen maximale snelheid berichten ophalen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-142">Furthermore, this pull-based load balancing enables optimal use of the worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="3c9fe-143">Dit patroon wordt vaak aangeduid als het *concurrerend consumenten*-patroon.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-143">This pattern is often termed the *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="3c9fe-144">In de volgende gedeelten wordt de code besproken waarmee deze architectuur wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-144">The following sections discuss the code that implements this architecture.</span></span>

## <a name="set-up-the-development-environment"></a><span data-ttu-id="3c9fe-145">De ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="3c9fe-145">Set up the development environment</span></span>
<span data-ttu-id="3c9fe-146">Voordat u Azure-toepassingen kunt ontwikkelen, moet u de hulpprogramma's ophalen en uw ontwikkelomgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-146">Before you can begin developing Azure applications, get the tools and set up your development environment.</span></span>

1. <span data-ttu-id="3c9fe-147">Installeer de Azure-SDK voor .NET via de [pagina met downloads](https://azure.microsoft.com/downloads/) voor SDK.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-147">Install the Azure SDK for .NET from the SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="3c9fe-148">Klik in de kolom **.NET** op de versie van [Visual Studio](http://www.visualstudio.com) die u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-148">In the **.NET** column, click the version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="3c9fe-149">In de stappen in deze zelfstudie wordt Visual Studio 2015 gebruikt, maar ze werken ook met Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-149">The steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="3c9fe-150">Klik op **Uitvoeren** wanneer u wordt gevraagd of u het installatieprogramma wilt uitvoeren of opslaan.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-150">When prompted to run or save the installer, click **Run**.</span></span>
4. <span data-ttu-id="3c9fe-151">Klik in het **webplatforminstallatieprogramma** op **Installeren** om door te gaan met de installatie.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-151">In the **Web Platform Installer**, click **Install** and proceed with the installation.</span></span>
5. <span data-ttu-id="3c9fe-152">Nadat de installatie is voltooid, hebt u alles wat u nodig hebt om te starten met het ontwikkelen van de app.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-152">Once the installation is complete, you will have everything necessary to start to develop the app.</span></span> <span data-ttu-id="3c9fe-153">De SDK bevat hulpprogramma's waarmee u eenvoudig Azure-toepassingen kunt ontwikkelen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-153">The SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="3c9fe-154">Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="3c9fe-154">Create a namespace</span></span>
<span data-ttu-id="3c9fe-155">De volgende stap is het maken van een servicenaamruimte en ophalen van een SAS-sleutel (Shared Access Signature).</span><span class="sxs-lookup"><span data-stu-id="3c9fe-155">The next step is to create a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="3c9fe-156">Een naamruimte biedt een toepassingsbegrenzing voor elke toepassing die toegankelijk is via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="3c9fe-157">Er wordt automatisch een SAS-sleutel gegenereerd wanneer er een naamruimte wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-157">A SAS key is generated by the system when a namespace is created.</span></span> <span data-ttu-id="3c9fe-158">De combinatie van naamruimte en SAS-sleutel biedt Service Bus de benodigde referenties voor het verifiëren van toegang tot een toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-158">The combination of namespace and SAS key provides the credentials for Service Bus to authenticate access to an application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="3c9fe-159">Een webrol maken</span><span class="sxs-lookup"><span data-stu-id="3c9fe-159">Create a web role</span></span>
<span data-ttu-id="3c9fe-160">In dit gedeelte maakt u de front-end van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-160">In this section, you build the front end of your application.</span></span> <span data-ttu-id="3c9fe-161">U maakt eerst de pagina's die door uw toepassing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-161">First, you create the pages that your application displays.</span></span>
<span data-ttu-id="3c9fe-162">Vervolgens voegt u code toe waarmee items worden verzonden naar een Service Bus-wachtrij en waarmee statusinformatie over de wachtrij wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-162">After that, add code that submits items to a Service Bus queue and displays status information about the queue.</span></span>

### <a name="create-the-project"></a><span data-ttu-id="3c9fe-163">Het project maken</span><span class="sxs-lookup"><span data-stu-id="3c9fe-163">Create the project</span></span>
1. <span data-ttu-id="3c9fe-164">Visual Studio starten met administratorbevoegdheden: klik met de rechtermuisknop op het programmapictogram **Visual Studio** en klik vervolgens op **Als administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-164">Using administrator privileges, start Visual Studio: right-click the **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="3c9fe-165">Voor de Azure-rekenemulator, die verderop in dit artikel wordt besproken, is vereist dat Visual Studio wordt gestart met administratorbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-165">The Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="3c9fe-166">Klik in het menu **Bestand** van Visual Studio op **Nieuw** en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-166">In Visual Studio, on the **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="3c9fe-167">Klik vanuit **Geïnstalleerde sjablonen** onder **Visual C#** op **Cloud** en klik vervolgens op **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="3c9fe-168">Geef het project de naam **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-168">Name the project **MultiTierApp**.</span></span> <span data-ttu-id="3c9fe-169">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="3c9fe-170">Dubbelklik vanuit **.NET Framework 4.5**-rollen op **ASP.NET-webrol**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="3c9fe-171">Beweeg de muisaanwijzer over **WebRole1** onder **Azure Cloud Service-oplossing**, klik op het potloodpictogram en wijzig de naam van de webrol in **FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click the pencil icon, and rename the web role to **FrontendWebRole**.</span></span> <span data-ttu-id="3c9fe-172">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-172">Then click **OK**.</span></span> <span data-ttu-id="3c9fe-173">(Zorg ervoor dat u 'Frontend' invoert met een kleine letter 'e', dus niet 'FrontEnd'.)</span><span class="sxs-lookup"><span data-stu-id="3c9fe-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="3c9fe-174">Klik in het dialoogvenster **Nieuw ASP.NET-project** in de lijst **Een sjabloon selecteren** op **MVC**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-174">From the **New ASP.NET Project** dialog box, in the **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="3c9fe-175">Klik nog steeds vanuit het dialoogvenster **Nieuw ASP.NET-project** op de knop **Verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-175">Still in the **New ASP.NET Project** dialog box, click the **Change Authentication** button.</span></span> <span data-ttu-id="3c9fe-176">Klik in het dialoogvenster **Verificatie wijzigen** op **Geen verificatie** en vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-176">In the **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="3c9fe-177">In deze zelfstudie implementeert u een app waarvoor geen gebruikersaanmelding nodig is.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="3c9fe-178">Ga terug naar het dialoogvenster **Nieuw ASP.NET-project** en klik op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-178">Back in the **New ASP.NET Project** dialog box, click **OK** to create the project.</span></span>
8. <span data-ttu-id="3c9fe-179">Klik in **Solution Explorer** in het project **FrontendWebRole** met de rechtermuisknop op **Verwijzingen** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-179">In **Solution Explorer**, in the **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="3c9fe-180">Klik op het tabblad **Bladeren** en zoek vervolgens naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-180">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="3c9fe-181">Selecteer het **WindowsAzure.ServiceBus**-pakket, klik op **Installeren** en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-181">Select the **WindowsAzure.ServiceBus** package, click **Install**, and accept the terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="3c9fe-182">Na de installatie wordt verwezen naar de vereiste clientassembly's en zijn enkele nieuwe codebestanden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-182">Note that the required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="3c9fe-183">Klik in **Solution Explorer** met de rechtermuisknop op **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="3c9fe-184">Typ in het vak **Naam** de naam **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-184">In the **Name** box, type the name **OnlineOrder.cs**.</span></span> <span data-ttu-id="3c9fe-185">Klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-185">Then click **Add**.</span></span>

### <a name="write-the-code-for-your-web-role"></a><span data-ttu-id="3c9fe-186">De code voor de webrol schrijven</span><span class="sxs-lookup"><span data-stu-id="3c9fe-186">Write the code for your web role</span></span>
<span data-ttu-id="3c9fe-187">In dit gedeelte maakt u de verschillende pagina's die door uw toepassing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-187">In this section, you create the various pages that your application displays.</span></span>

1. <span data-ttu-id="3c9fe-188">In het bestand OnlineOrder.cs in Visual Studio vervangt u de bestaande naamruimtedefinitie door de volgende code:</span><span class="sxs-lookup"><span data-stu-id="3c9fe-188">In the OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with the following code:</span></span>
   
   ```csharp
   namespace FrontendWebRole.Models
   {
       public class OnlineOrder
       {
           public string Customer { get; set; }
           public string Product { get; set; }
       }
   }
   ```
2. <span data-ttu-id="3c9fe-189">Dubbelklik in **Solution Explorer** op **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="3c9fe-190">Voeg de volgende **using**-instructies aan het begin van het bestand toe om de naamruimten op te nemen voor het model dat u zojuist hebt gemaakt, maar ook voor Service Bus.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-190">Add the following **using** statements at the top of the file to include the namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="3c9fe-191">In het bestand HomeController.cs in Visual Studio vervangt u bovendien de bestaande naamruimtedefinitie door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-191">Also in the HomeController.cs file in Visual Studio, replace the existing namespace definition with the following code.</span></span> <span data-ttu-id="3c9fe-192">Deze code bevat methoden voor het afhandelen van de verzending van items naar de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-192">This code contains methods for handling the submission of items to the queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect to Submit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for the submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from the submission
           // form.
           [HttpPost]
           // Attribute to help prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting to queue here.
   
                   return RedirectToAction("Submit");
               }
               else
               {
                   return View(order);
               }
           }
       }
   }
   ```
4. <span data-ttu-id="3c9fe-193">Klik in het menu **Bouwen** op **Oplossing opbouwen** om de juistheid van uw werk tot nu toe te controleren.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-193">From the **Build** menu, click **Build Solution** to test the accuracy of your work so far.</span></span>
5. <span data-ttu-id="3c9fe-194">Maak nu de weergave voor de methode voor `Submit()` die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-194">Now, create the view for the `Submit()` method you created earlier.</span></span> <span data-ttu-id="3c9fe-195">Klik met de rechtermuisknop in de methode voor `Submit()` (de overbelasting van `Submit()` waarvoor geen parameters zijn vereist) en kies vervolgens **Weergave toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-195">Right-click within the `Submit()` method (the overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="3c9fe-196">Een dialoogvenster voor het maken van de weergave wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-196">A dialog box appears for creating the view.</span></span> <span data-ttu-id="3c9fe-197">Kies **Maken** in de lijst **Sjabloon**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-197">In the **Template** list, choose **Create**.</span></span> <span data-ttu-id="3c9fe-198">Klik in de lijst **Modelklasse** op de klasse **OnlineOrder**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-198">In the **Model class** list, click the **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="3c9fe-199">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-199">Click **Add**.</span></span>
8. <span data-ttu-id="3c9fe-200">Wijzig nu de weergegeven naam van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-200">Now, change the displayed name of your application.</span></span> <span data-ttu-id="3c9fe-201">Dubbelklik in **Solution Explorer** op het bestand **Views\Shared\\_Layout.cshtml** om dit te openen in de Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file to open it in the Visual Studio editor.</span></span>
9. <span data-ttu-id="3c9fe-202">Vervang alle instanties van **Mijn ASP.NET-toepassing** door **Producten van LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="3c9fe-203">Verwijder de koppelingen **Start**, **Info** en **Contact**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-203">Remove the **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="3c9fe-204">Verwijder de gemarkeerde code:</span><span class="sxs-lookup"><span data-stu-id="3c9fe-204">Delete the highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="3c9fe-205">Wijzig tot slot de verzendpagina om enige informatie over de wachtrij op te nemen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-205">Finally, modify the submission page to include some information about the queue.</span></span> <span data-ttu-id="3c9fe-206">Dubbelklik in **Solution Explorer** op het bestand **Views\Home\Submit.cshtml** om dit te openen in de Visual Studio-editor.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file to open it in the Visual Studio editor.</span></span> <span data-ttu-id="3c9fe-207">Voeg de volgende regel toe na `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-207">Add the following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="3c9fe-208">Op dit moment is `ViewBag.MessageCount` leeg.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-208">For now, the `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="3c9fe-209">U vult dit later in.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting to be processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="3c9fe-210">U hebt nu de gebruikersinterface geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-210">You now have implemented your UI.</span></span> <span data-ttu-id="3c9fe-211">Druk op **F5** om uw toepassing uit te voeren en te controleren of deze voldoet aan uw verwachting.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-211">You can press **F5** to run your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-the-code-for-submitting-items-to-a-service-bus-queue"></a><span data-ttu-id="3c9fe-212">De code schrijven voor het indienen van items aan een Service Bus-wachtrij</span><span class="sxs-lookup"><span data-stu-id="3c9fe-212">Write the code for submitting items to a Service Bus queue</span></span>
<span data-ttu-id="3c9fe-213">Voeg nu code toe voor het indienen van items aan een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-213">Now, add code for submitting items to a queue.</span></span> <span data-ttu-id="3c9fe-214">U maakt eerst een klasse die de verbindingsgegevens van de Service Bus-wachtrij bevat.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="3c9fe-215">Vervolgens initialiseert u de verbinding vanuit Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="3c9fe-216">Tot slot werkt u de verzendcode bij die u eerder hebt gemaakt in HomeController.cs, zodat items daadwerkelijk naar een Service Bus-wachtrij worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-216">Finally, update the submission code you created earlier in HomeController.cs to actually submit items to a Service Bus queue.</span></span>

1. <span data-ttu-id="3c9fe-217">Klik in **Solution Explorer** met de rechtermuisknop op **FrontendWebRole** (klik met de rechtermuisknop op het project, niet op de rol).</span><span class="sxs-lookup"><span data-stu-id="3c9fe-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click the project, not the role).</span></span> <span data-ttu-id="3c9fe-218">Klik op **Toevoegen** en klik vervolgens op **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="3c9fe-219">Geef de klasse de naam **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-219">Name the class **QueueConnector.cs**.</span></span> <span data-ttu-id="3c9fe-220">Klik op **Toevoegen** om de klasse te maken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-220">Click **Add** to create the class.</span></span>
3. <span data-ttu-id="3c9fe-221">Voeg nu code toe waarin de verbindingsgegevens zijn opgenomen en waarmee de verbinding met een Service Bus-wachtrij wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-221">Now, add code that encapsulates the connection information and initializes the connection to a Service Bus queue.</span></span> <span data-ttu-id="3c9fe-222">Vervang de volledige inhoud van QueueConnector.cs door de volgende code en voer waarden in voor `your Service Bus namespace` (de naam van uw naamruimte) en `yourKey`. Dit is de **primaire sleutel** die u eerder van Azure Portal hebt gekregen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-222">Replace the entire contents of QueueConnector.cs with the following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is the **primary key** you previously obtained from the Azure portal.</span></span>
   
   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Web;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   
   namespace FrontendWebRole
   {
       public static class QueueConnector
       {
           // Thread-safe. Recommended that you cache rather than recreating it
           // on every request.
           public static QueueClient OrdersQueueClient;
   
           // Obtain these values from the portal.
           public const string Namespace = "your Service Bus namespace";
   
           // The name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create the namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http to be friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create the namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create the queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client to the queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="3c9fe-223">Controleer nu of uw methode voor **Initialiseren** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="3c9fe-224">Dubbelklik in **Solution Explorer** op **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="3c9fe-225">Voeg de volgende coderegel toe aan het einde van de methode **Application_Start**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-225">Add the following line of code at the end of the **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="3c9fe-226">Werk tot slot de webcode die u eerder hebt gemaakt, bij om items naar de wachtrij te verzenden.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-226">Finally, update the web code you created earlier, to submit items to the queue.</span></span> <span data-ttu-id="3c9fe-227">Dubbelklik in **Solution Explorer** op **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="3c9fe-228">Werk de methode `Submit()` (de overbelasting waarvoor geen parameters zijn vereist) als volgt bij om het aantal berichten voor de wachtrij te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-228">Update the `Submit()` method (the overload that takes no parameters) as follows to get the message count for the queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you to perform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get the queue, and obtain the message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="3c9fe-229">Werk de methode `Submit(OnlineOrder order)` (de overbelasting waarvoor één parameter moet worden gebruikt) als volgt bij om ordergegevens naar de wachtrij te verzenden.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-229">Update the `Submit(OnlineOrder order)` method (the overload that takes one parameter) as follows to submit order information to the queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from the order.
           var message = new BrokeredMessage(order);
   
           // Submit the order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="3c9fe-230">U kunt nu de toepassing opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-230">You can now run the application again.</span></span> <span data-ttu-id="3c9fe-231">Het aantal berichten neemt toe elke keer wanneer u een order verzendt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-231">Each time you submit an order, the message count increases.</span></span>
   
   ![][18]

## <a name="create-the-worker-role"></a><span data-ttu-id="3c9fe-232">De werkrol maken</span><span class="sxs-lookup"><span data-stu-id="3c9fe-232">Create the worker role</span></span>
<span data-ttu-id="3c9fe-233">U maakt nu de werkrol die de orderverzendingen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-233">You will now create the worker role that processes the order submissions.</span></span> <span data-ttu-id="3c9fe-234">In dit voorbeeld wordt de Visual Studio-projectsjabloon **Werkrol met Service Bus-wachtrij** gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-234">This example uses the **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="3c9fe-235">U hebt al de vereiste referenties ontvangen van de portal.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-235">You already obtained the required credentials from the portal.</span></span>

1. <span data-ttu-id="3c9fe-236">Zorg ervoor dat u Visual Studio aan uw Azure-account hebt gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-236">Make sure you have connected Visual Studio to your Azure account.</span></span>
2. <span data-ttu-id="3c9fe-237">Klik in Visual Studio in **Solution Explorer** met de rechtermuisknop op de map **Rollen** onder het **MultiTierApp**-project.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under the **MultiTierApp** project.</span></span>
3. <span data-ttu-id="3c9fe-238">Klik op **Toevoegen** en klik vervolgens op **Nieuw werkrolproject**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="3c9fe-239">Het dialoogvenster **Nieuw rolproject toevoegen** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-239">The **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="3c9fe-240">Klik in het dialoogvenster **Nieuw rolproject toevoegen** op **Werkrol met Service Bus-wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-240">In the **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="3c9fe-241">Voer in het vak **Naam** de naam **OrderProcessingRole** voor het project in.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-241">In the **Name** box, name the project **OrderProcessingRole**.</span></span> <span data-ttu-id="3c9fe-242">Klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-242">Then click **Add**.</span></span>
6. <span data-ttu-id="3c9fe-243">Kopieer de verbindingsreeks die u hebt verkregen in stap 9 van het gedeelte 'Een Service Bus-naamruimte maken' naar het klembord.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-243">Copy the connection string that you obtained in step 9 of the "Create a Service Bus namespace" section to the clipboard.</span></span>
7. <span data-ttu-id="3c9fe-244">Klik in **Solution Explorer** met de rechtermuisknop op de **OrderProcessingRole** die u in stap 5 hebt gemaakt (klik met de rechtermuisknop op **OrderProcessingRole** onder **Rollen** en niet onder de klasse).</span><span class="sxs-lookup"><span data-stu-id="3c9fe-244">In **Solution Explorer**, right-click the **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not the class).</span></span> <span data-ttu-id="3c9fe-245">Klik vervolgens op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="3c9fe-246">Klik op het tabblad **Instellingen** van het dialoogvenster **Eigenschappen** in het vak **Waarde** voor **Microsoft.ServiceBus.ConnectionString**. Plak vervolgens de eindpuntwaarde die u in stap 6 hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-246">On the **Settings** tab of the **Properties** dialog box, click inside the **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste the endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="3c9fe-247">Maak een klasse **OnlineOrder** die de orders vertegenwoordigt tijdens het verwerken van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-247">Create an **OnlineOrder** class to represent the orders as you process them from the queue.</span></span> <span data-ttu-id="3c9fe-248">U kunt een klasse die u al hebt gemaakt opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="3c9fe-249">Klik in **Solution Explorer** met de rechtermuisknop op de klasse **OrderProcessingRole** (klik met de rechtermuisknop op het klassepictogram en niet op de rol).</span><span class="sxs-lookup"><span data-stu-id="3c9fe-249">In **Solution Explorer**, right-click the **OrderProcessingRole** class (right-click the class icon, not the role).</span></span> <span data-ttu-id="3c9fe-250">Klik op **Toevoegen** en vervolgens op **Bestaand item**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="3c9fe-251">Blader naar de submap voor **FrontendWebRole\Models** en dubbelklik vervolgens op **OnlineOrder.cs** om het bestand toe te voegen aan dit project.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-251">Browse to the subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** to add it to this project.</span></span>
11. <span data-ttu-id="3c9fe-252">Wijzig in **WorkerRole.cs** de waarde van de variabele **QueueName** van `"ProcessingQueue"` in `"OrdersQueue"`, zoals weergegeven in de volgende code.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-252">In **WorkerRole.cs**, change the value of the **QueueName** variable from `"ProcessingQueue"` to `"OrdersQueue"` as shown in the following code.</span></span>
    
    ```csharp
    // The name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="3c9fe-253">Voeg de volgende instructie toe aan het begin van het bestand WorkerRole.cs.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-253">Add the following using statement at the top of the WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="3c9fe-254">In de functie `Run()` binnen de aanroep `OnMessage()` vervangt u de inhoud van de `try`-component door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-254">In the `Run()` function, inside the `OnMessage()` call, replace the contents of the `try` clause with the following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View the message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="3c9fe-255">U hebt de toepassing nu voltooid.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-255">You have completed the application.</span></span> <span data-ttu-id="3c9fe-256">U kunt de volledige toepassing testen door met de rechtermuisknop te klikken op het MultiTierApp-project in Solution Explorer, **Instellen als opstartproject** te selecteren en vervolgens op F5 te drukken.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-256">You can test the full application by right-clicking the MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="3c9fe-257">Houd er rekening mee dat het aantal berichten niet toeneemt, omdat de werkrol items uit de wachtrij verwerkt en als voltooid markeert.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-257">Note that the message count does not increment, because the worker role processes items from the queue and marks them as complete.</span></span> <span data-ttu-id="3c9fe-258">U ziet de trace-uitvoer van uw werkrol door de gebruikersinterface van de Azure-rekenemulator weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-258">You can see the trace output of your worker role by viewing the Azure Compute Emulator UI.</span></span> <span data-ttu-id="3c9fe-259">Klik hiervoor met de rechtermuisknop op het emulatorpictogram in het systeemvak van de taakbalk en selecteer **Gebruikersinterface van de rekenemulator weergeven**.</span><span class="sxs-lookup"><span data-stu-id="3c9fe-259">You can do this by right-clicking the emulator icon in the notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="3c9fe-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c9fe-260">Next steps</span></span>
<span data-ttu-id="3c9fe-261">Zie de volgende resources voor meer informatie over Service Bus:</span><span class="sxs-lookup"><span data-stu-id="3c9fe-261">To learn more about Service Bus, see the following resources:</span></span>  

* <span data-ttu-id="3c9fe-262">[Documentatie voor Azure Service Bus][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="3c9fe-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="3c9fe-263">[Service Bus-servicepagina][sbacom]</span><span class="sxs-lookup"><span data-stu-id="3c9fe-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="3c9fe-264">[Service Bus-wachtrijen gebruiken][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="3c9fe-264">[How to Use Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="3c9fe-265">Zie voor meer informatie over scenario's voor meerdere lagen:</span><span class="sxs-lookup"><span data-stu-id="3c9fe-265">To learn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="3c9fe-266">[.NET-toepassing met meerdere lagen met Table Storage, Queue Storage en Blob Storage][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="3c9fe-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

[0]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[1]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-100.png
[2]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-101.png
[9]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-10.png
[10]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-11.png
[11]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-02.png
[12]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-12.png
[13]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-13.png
[14]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-33.png
[15]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-34.png
[16]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-14.png
[17]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app.png
[18]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-app2.png

[19]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-38.png
[20]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-39.png
[23]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRole1.png
[25]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBWorkerRoleProperties.png
[26]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/SBNewWorkerRole.png
[28]: ./media/service-bus-dotnet-multi-tier-app-using-service-bus-queues/getting-started-multi-tier-40.png

[sbdocs]: /azure/service-bus-messaging/  
[sbacom]: https://azure.microsoft.com/services/service-bus/  
[sbacomqhowto]: service-bus-dotnet-get-started-with-queues.md  
[mutitierstorage]: https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36

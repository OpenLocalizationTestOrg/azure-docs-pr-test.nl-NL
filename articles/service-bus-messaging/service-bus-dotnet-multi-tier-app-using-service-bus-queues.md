---
title: aaa.NET toepassing met meerdere lagen Azure Service Bus | Microsoft Docs
description: Een .NET-zelfstudie waarmee u een app in Azure die gebruikmaakt van Service Bus-wachtrijen toocommunicate tussen lagen met meerdere lagen ontwikkelen.
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
ms.openlocfilehash: 485910ff1d3b8b0a709ee14ede32e57cf873829a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="net-multi-tier-application-using-azure-service-bus-queues"></a><span data-ttu-id="ef29a-103">.NET-toepassing met meerdere lagen die Azure Service Bus-wachtrijen gebruikt</span><span class="sxs-lookup"><span data-stu-id="ef29a-103">.NET multi-tier application using Azure Service Bus queues</span></span>
## <a name="introduction"></a><span data-ttu-id="ef29a-104">Inleiding</span><span class="sxs-lookup"><span data-stu-id="ef29a-104">Introduction</span></span>
<span data-ttu-id="ef29a-105">Ontwikkelen voor Microsoft Azure is eenvoudig met Visual Studio en Hallo gratis Azure SDK voor .NET.</span><span class="sxs-lookup"><span data-stu-id="ef29a-105">Developing for Microsoft Azure is easy using Visual Studio and hello free Azure SDK for .NET.</span></span> <span data-ttu-id="ef29a-106">Deze zelfstudie wordt u begeleid Hallo stappen toocreate een toepassing die gebruikmaakt van meerdere Azure-resources in uw lokale omgeving.</span><span class="sxs-lookup"><span data-stu-id="ef29a-106">This tutorial walks you through hello steps toocreate an application that uses multiple Azure resources running in your local environment.</span></span>

<span data-ttu-id="ef29a-107">U leert Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ef29a-107">You will learn hello following:</span></span>

* <span data-ttu-id="ef29a-108">Hoe tooenable uw computer voor het ontwikkelen van Azure met één downloaden en installeren.</span><span class="sxs-lookup"><span data-stu-id="ef29a-108">How tooenable your computer for Azure development with a single download and install.</span></span>
* <span data-ttu-id="ef29a-109">Hoe toouse Visual Studio toodevelop voor Azure.</span><span class="sxs-lookup"><span data-stu-id="ef29a-109">How toouse Visual Studio toodevelop for Azure.</span></span>
* <span data-ttu-id="ef29a-110">Hoe een toepassing met meerdere lagen in Azure met behulp van web-en werkrollen toocreate.</span><span class="sxs-lookup"><span data-stu-id="ef29a-110">How toocreate a multi-tier application in Azure using web and worker roles.</span></span>
* <span data-ttu-id="ef29a-111">Hoe toocommunicate tussen lagen met Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-111">How toocommunicate between tiers using Service Bus queues.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

<span data-ttu-id="ef29a-112">In deze zelfstudie hebt u bouwen en uitvoeren van toepassing met meerdere lagen Hallo in een Azure-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="ef29a-112">In this tutorial you'll build and run hello multi-tier application in an Azure cloud service.</span></span> <span data-ttu-id="ef29a-113">Hallo-front-end is een ASP.NET MVC-Webrol en Hallo back-end een werkrol die gebruikmaakt van een Service Bus-wachtrij is.</span><span class="sxs-lookup"><span data-stu-id="ef29a-113">hello front end is an ASP.NET MVC web role and hello back end is a worker-role that uses a Service Bus queue.</span></span> <span data-ttu-id="ef29a-114">U kunt maken Hallo dezelfde toepassing met meerdere lagen Hallo front-end als een webproject dat geïmplementeerde tooan Azure-website in plaats van een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="ef29a-114">You can create hello same multi-tier application with hello front end as a web project, that is deployed tooan Azure website instead of a cloud service.</span></span> <span data-ttu-id="ef29a-115">U kunt ook proberen Hallo [.NET on-premises/hybride cloud-toepassing](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ef29a-115">You can also try out hello [.NET on-premises/cloud hybrid application](../service-bus-relay/service-bus-dotnet-hybrid-app-using-service-bus-relay.md) tutorial.</span></span>

<span data-ttu-id="ef29a-116">Hallo volgende schermafbeelding ziet u de toepassing hello voltooid.</span><span class="sxs-lookup"><span data-stu-id="ef29a-116">hello following screen shot shows hello completed application.</span></span>

![][0]

## <a name="scenario-overview-inter-role-communication"></a><span data-ttu-id="ef29a-117">Scenario-overzicht: communicatie tussen rollen</span><span class="sxs-lookup"><span data-stu-id="ef29a-117">Scenario overview: inter-role communication</span></span>
<span data-ttu-id="ef29a-118">een order voor het verwerken van Hallo front-end UI-onderdeel, uitgevoerd in de Webrol hello, toosubmit moet communiceren met de Hallo middelste laag logica uitgevoerd in de werkrol Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-118">toosubmit an order for processing, hello front-end UI component, running in hello web role, must interact with hello middle tier logic running in hello worker role.</span></span> <span data-ttu-id="ef29a-119">In dit voorbeeld wordt Service Bus-berichtenservice voor communicatie tussen lagen Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-119">This example uses Service Bus messaging for hello communication between hello tiers.</span></span>

<span data-ttu-id="ef29a-120">Met Service Bus, uitwisseling van berichten tussen Hallo web en de middelste laag worden de twee onderdelen losgekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ef29a-120">Using Service Bus messaging between hello web and middle tiers decouples the two components.</span></span> <span data-ttu-id="ef29a-121">Daarentegen toodirect messaging (dat wil zeggen, TCP of HTTP), Hallo weblaag toohello middelste laag niet rechtstreeks; verbinding in plaats daarvan stuurt het werkeenheden, als berichten, naar Service Bus die betrouwbaar behoudt deze totdat de middelste laag Hallo tooconsume gereed is en deze te verwerken.</span><span class="sxs-lookup"><span data-stu-id="ef29a-121">In contrast toodirect messaging (that is, TCP or HTTP), hello web tier does not connect toohello middle tier directly; instead it pushes units of work, as messages, into Service Bus, which reliably retains them until hello middle tier is ready tooconsume and process them.</span></span>

<span data-ttu-id="ef29a-122">Service Bus biedt twee entiteiten toosupport brokered messaging: wachtrijen en onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-122">Service Bus provides two entities toosupport brokered messaging: queues and topics.</span></span> <span data-ttu-id="ef29a-123">Met wachtrijen wordt verzonden elk bericht toohello wachtrij wordt gebruikt door een enkele ontvanger.</span><span class="sxs-lookup"><span data-stu-id="ef29a-123">With queues, each message sent toohello queue is consumed by a single receiver.</span></span> <span data-ttu-id="ef29a-124">Onderwerpen ondersteunen Hallo publiceren/abonneren patroon waarin elk gepubliceerde bericht beschikbaar tooa abonnement geregistreerd bij Hallo onderwerp is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef29a-124">Topics support hello publish/subscribe pattern in which each published message is made available tooa subscription registered with hello topic.</span></span> <span data-ttu-id="ef29a-125">Elk abonnement onderhoudt logisch gezien zijn eigen wachtrij met berichten.</span><span class="sxs-lookup"><span data-stu-id="ef29a-125">Each subscription logically maintains its own queue of messages.</span></span> <span data-ttu-id="ef29a-126">Abonnementen kunnen ook worden geconfigureerd met filterregels die Hallo set berichten doorgegeven aan Hallo abonnement wachtrij toothose die overeenkomen met Hallo filter beperken.</span><span class="sxs-lookup"><span data-stu-id="ef29a-126">Subscriptions can also be configured with filter rules that restrict hello set of messages passed to hello subscription queue toothose that match hello filter.</span></span> <span data-ttu-id="ef29a-127">Hallo wordt volgende voorbeeld Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-127">hello following example uses Service Bus queues.</span></span>

![][1]

<span data-ttu-id="ef29a-128">Dit communicatiemechanisme heeft verschillende voordelen ten opzichte van Direct Messaging:</span><span class="sxs-lookup"><span data-stu-id="ef29a-128">This communication mechanism has several advantages over direct messaging:</span></span>

* <span data-ttu-id="ef29a-129">**Tijdelijke ontkoppeling.**</span><span class="sxs-lookup"><span data-stu-id="ef29a-129">**Temporal decoupling.**</span></span> <span data-ttu-id="ef29a-130">Met de Hallo asynchrone berichtenpatroon producenten en consumenten hoeven niet te worden online op Hallo hetzelfde moment.</span><span class="sxs-lookup"><span data-stu-id="ef29a-130">With hello asynchronous messaging pattern, producers and consumers need not be online at hello same time.</span></span> <span data-ttu-id="ef29a-131">Service Bus slaat berichten veilig op totdat Hallo verbruikende partij gereed is om ze te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-131">Service Bus reliably stores messages until hello consuming party is ready to receive them.</span></span> <span data-ttu-id="ef29a-132">Hierdoor Hallo onderdelen van Hallo gedistribueerde toepassing toobe losgekoppeld-hetzij vrijwillig, bijvoorbeeld voor onderhoud, hetzij vanwege het vastlopen van tooa onderdeel zonder enige impact op het systeem als geheel.</span><span class="sxs-lookup"><span data-stu-id="ef29a-132">This enables hello components of hello distributed application toobe disconnected, either voluntarily, for example, for maintenance, or due tooa component crash, without impacting the system as a whole.</span></span> <span data-ttu-id="ef29a-133">Bovendien hoeft Hallo verbruikt toepassing alleen online toocome bepaalde tijdstippen gedurende Hallo dag.</span><span class="sxs-lookup"><span data-stu-id="ef29a-133">Furthermore, hello consuming application might only need toocome online during certain times of hello day.</span></span>
* <span data-ttu-id="ef29a-134">**Herverdeling van taken.**</span><span class="sxs-lookup"><span data-stu-id="ef29a-134">**Load leveling.**</span></span> <span data-ttu-id="ef29a-135">In veel toepassingen varieert de systeembelasting gedurende een periode, terwijl Hallo benodigde verwerkingstijd voor elke werkeenheid doorgaans constant blijft.</span><span class="sxs-lookup"><span data-stu-id="ef29a-135">In many applications, system load varies over time, while hello processing time required for each unit of work is typically constant.</span></span> <span data-ttu-id="ef29a-136">Tussen bericht producenten en consumenten met een wachtrij betekent dat Hallo verbruikt toobe behoeften alleen van toepassing (Hallo worker) ingericht tooaccommodate gemiddelde belasting in plaats van piekbelasting.</span><span class="sxs-lookup"><span data-stu-id="ef29a-136">Intermediating message producers and consumers with a queue means that hello consuming application (hello worker) only needs toobe provisioned tooaccommodate average load rather than peak load.</span></span> <span data-ttu-id="ef29a-137">Hallo diepte van Hallo wachtrij neemt toe of af als de inkomende belasting Hallo varieert.</span><span class="sxs-lookup"><span data-stu-id="ef29a-137">hello depth of hello queue grows and contracts as hello incoming load varies.</span></span> <span data-ttu-id="ef29a-138">Dit bespaart rechtstreeks geld in termen van Hallo hoeveelheid infrastructuur vereist tooservice Hallo toepassing werklast.</span><span class="sxs-lookup"><span data-stu-id="ef29a-138">This directly saves money in terms of hello amount of infrastructure required tooservice hello application load.</span></span>
* <span data-ttu-id="ef29a-139">**Taakverdeling.**</span><span class="sxs-lookup"><span data-stu-id="ef29a-139">**Load balancing.**</span></span> <span data-ttu-id="ef29a-140">Naarmate het verkeer toeneemt, kan meer werkprocessen kunnen tooread uit de wachtrij Hallo worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ef29a-140">As load increases, more worker processes can be added tooread from hello queue.</span></span> <span data-ttu-id="ef29a-141">Elk bericht wordt verwerkt door slechts één van de werkprocessen Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-141">Each message is processed by only one of hello worker processes.</span></span> <span data-ttu-id="ef29a-142">Bovendien deze pull-gebaseerde taakverdeling optimaal gebruik van de werkmachines Hallo zelfs als kan de werkmachines verschilt verwerkingskracht, zoals ze op eigen maximale snelheid berichten ophalen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-142">Furthermore, this pull-based load balancing enables optimal use of hello worker machines even if the worker machines differ in terms of processing power, as they will pull messages at their own maximum rate.</span></span> <span data-ttu-id="ef29a-143">Dit patroon wordt vaak aangeduid als Hallo *concurrerend consumenten* patroon.</span><span class="sxs-lookup"><span data-stu-id="ef29a-143">This pattern is often termed hello *competing consumer* pattern.</span></span>
  
  ![][2]

<span data-ttu-id="ef29a-144">Hallo volgende secties worden besproken Hallo-code waarmee deze architectuur.</span><span class="sxs-lookup"><span data-stu-id="ef29a-144">hello following sections discuss hello code that implements this architecture.</span></span>

## <a name="set-up-hello-development-environment"></a><span data-ttu-id="ef29a-145">Hallo-ontwikkelomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="ef29a-145">Set up hello development environment</span></span>
<span data-ttu-id="ef29a-146">Voordat u kunt Azure-toepassingen te ontwikkelen, Hallo-hulpprogramma's ophalen en instellen van uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="ef29a-146">Before you can begin developing Azure applications, get hello tools and set up your development environment.</span></span>

1. <span data-ttu-id="ef29a-147">Installeer hello Azure SDK voor .NET via Hallo SDK [pagina downloads](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ef29a-147">Install hello Azure SDK for .NET from hello SDK [downloads page](https://azure.microsoft.com/downloads/).</span></span>
2. <span data-ttu-id="ef29a-148">In Hallo **.NET** kolom, klikt u op Hallo-versie van [Visual Studio](http://www.visualstudio.com) u gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ef29a-148">In hello **.NET** column, click hello version of [Visual Studio](http://www.visualstudio.com) you are using.</span></span> <span data-ttu-id="ef29a-149">Hallo stappen in deze zelfstudie Gebruik Visual Studio 2015, maar ze werken ook met Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ef29a-149">hello steps in this tutorial use Visual Studio 2015, but they also work with Visual Studio 2017.</span></span>
3. <span data-ttu-id="ef29a-150">Wanneer u daarom wordt gevraagd toorun of Hallo installatieprogramma opslaat, klikt u op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-150">When prompted toorun or save hello installer, click **Run**.</span></span>
4. <span data-ttu-id="ef29a-151">In Hallo **Web Platform Installer**, klikt u op **installeren** te gaan met Hallo-installatie.</span><span class="sxs-lookup"><span data-stu-id="ef29a-151">In hello **Web Platform Installer**, click **Install** and proceed with hello installation.</span></span>
5. <span data-ttu-id="ef29a-152">Zodra Hallo-installatie voltooid is, hebt u alles wat u nodig toostart toodevelop Hallo app.</span><span class="sxs-lookup"><span data-stu-id="ef29a-152">Once hello installation is complete, you will have everything necessary toostart toodevelop hello app.</span></span> <span data-ttu-id="ef29a-153">Hallo SDK bevat hulpprogramma's waarmee u eenvoudig Azure toepassingen ontwikkelen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ef29a-153">hello SDK includes tools that let you easily develop Azure applications in Visual Studio.</span></span>

## <a name="create-a-namespace"></a><span data-ttu-id="ef29a-154">Een naamruimte maken</span><span class="sxs-lookup"><span data-stu-id="ef29a-154">Create a namespace</span></span>
<span data-ttu-id="ef29a-155">de volgende stap Hallo toocreate is een Servicenaamruimte en ophalen van een Shared Access Signature (SAS)-sleutel.</span><span class="sxs-lookup"><span data-stu-id="ef29a-155">hello next step is toocreate a service namespace, and obtain a Shared Access Signature (SAS) key.</span></span> <span data-ttu-id="ef29a-156">Een naamruimte biedt een toepassingsbegrenzing voor elke toepassing die toegankelijk is via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ef29a-156">A namespace provides an application boundary for each application exposed through Service Bus.</span></span> <span data-ttu-id="ef29a-157">Een SAS-sleutel wordt gegenereerd door Hallo systeem wanneer een naamruimte is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef29a-157">A SAS key is generated by hello system when a namespace is created.</span></span> <span data-ttu-id="ef29a-158">Hallo combinatie van naamruimte en SAS-sleutel biedt Hallo referenties voor Service Bus tooauthenticate toegang tooan toepassing.</span><span class="sxs-lookup"><span data-stu-id="ef29a-158">hello combination of namespace and SAS key provides hello credentials for Service Bus tooauthenticate access tooan application.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-web-role"></a><span data-ttu-id="ef29a-159">Een webrol maken</span><span class="sxs-lookup"><span data-stu-id="ef29a-159">Create a web role</span></span>
<span data-ttu-id="ef29a-160">In deze sectie bouwt u Hallo-front-end van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="ef29a-160">In this section, you build hello front end of your application.</span></span> <span data-ttu-id="ef29a-161">U maakt eerst Hallo-pagina's die uw toepassing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef29a-161">First, you create hello pages that your application displays.</span></span>
<span data-ttu-id="ef29a-162">Voeg daarna code items tooa Service Bus-wachtrij verzendt en geeft statusinformatie weer over Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ef29a-162">After that, add code that submits items tooa Service Bus queue and displays status information about hello queue.</span></span>

### <a name="create-hello-project"></a><span data-ttu-id="ef29a-163">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="ef29a-163">Create hello project</span></span>
1. <span data-ttu-id="ef29a-164">Visual Studio met administratorbevoegdheden starten: klik met de rechtermuisknop Hallo **Visual Studio** programmapictogram en klik vervolgens op **als administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-164">Using administrator privileges, start Visual Studio: right-click hello **Visual Studio** program icon, and then click **Run as administrator**.</span></span> <span data-ttu-id="ef29a-165">Hello Azure-rekenemulator, die verderop in dit artikel wordt besproken vereist dat Visual Studio met administratorbevoegdheden worden gestart.</span><span class="sxs-lookup"><span data-stu-id="ef29a-165">hello Azure compute emulator, discussed later in this article, requires that Visual Studio be started with administrator privileges.</span></span>
   
   <span data-ttu-id="ef29a-166">In Visual Studio op Hallo **bestand** menu, klikt u op **nieuw**, en klik vervolgens op **Project**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-166">In Visual Studio, on hello **File** menu, click **New**, and then click **Project**.</span></span>
2. <span data-ttu-id="ef29a-167">Klik vanuit **Geïnstalleerde sjablonen** onder **Visual C#** op **Cloud** en klik vervolgens op **Azure Cloud Service**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-167">From **Installed Templates**, under **Visual C#**, click **Cloud** and then click **Azure Cloud Service**.</span></span> <span data-ttu-id="ef29a-168">Naam Hallo project **MultiTierApp**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-168">Name hello project **MultiTierApp**.</span></span> <span data-ttu-id="ef29a-169">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-169">Then click **OK**.</span></span>
   
   ![][9]
3. <span data-ttu-id="ef29a-170">Dubbelklik vanuit **.NET Framework 4.5**-rollen op **ASP.NET-webrol**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-170">From **.NET Framework 4.5** roles, double-click **ASP.NET Web Role**.</span></span>
   
   ![][10]
4. <span data-ttu-id="ef29a-171">Beweeg de muisaanwijzer over **WebRole1** onder **Azure Cloud Service-oplossing**, klik op het potloodpictogram Hallo en wijzig de naam van de Webrol hello te**FrontendWebRole**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-171">Hover over **WebRole1** under **Azure Cloud Service solution**, click hello pencil icon, and rename hello web role too**FrontendWebRole**.</span></span> <span data-ttu-id="ef29a-172">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-172">Then click **OK**.</span></span> <span data-ttu-id="ef29a-173">(Zorg ervoor dat u 'Frontend' invoert met een kleine letter 'e', dus niet 'FrontEnd'.)</span><span class="sxs-lookup"><span data-stu-id="ef29a-173">(Make sure you enter "Frontend" with a lower-case 'e,' not "FrontEnd".)</span></span>
   
   ![][11]
5. <span data-ttu-id="ef29a-174">Van Hallo **nieuw ASP.NET-Project** dialoogvenster in Hallo **Selecteer een sjabloon** lijst, klikt u op **MVC**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-174">From hello **New ASP.NET Project** dialog box, in hello **Select a template** list, click **MVC**.</span></span>
   
   ![][12]
6. <span data-ttu-id="ef29a-175">Nog steeds in Hallo **nieuw ASP.NET-Project** dialoogvenster vak, klikt u op Hallo **verificatie wijzigen** knop.</span><span class="sxs-lookup"><span data-stu-id="ef29a-175">Still in hello **New ASP.NET Project** dialog box, click hello **Change Authentication** button.</span></span> <span data-ttu-id="ef29a-176">In Hallo **verificatie wijzigen** in het dialoogvenster, klikt u op **geen verificatie**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-176">In hello **Change Authentication** dialog box, click **No Authentication**, and then click **OK**.</span></span> <span data-ttu-id="ef29a-177">In deze zelfstudie implementeert u een app waarvoor geen gebruikersaanmelding nodig is.</span><span class="sxs-lookup"><span data-stu-id="ef29a-177">For this tutorial, you're deploying an app that doesn't need a user login.</span></span>
   
    ![][16]
7. <span data-ttu-id="ef29a-178">Terug in Hallo **nieuw ASP.NET-Project** in het dialoogvenster, klikt u op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="ef29a-178">Back in hello **New ASP.NET Project** dialog box, click **OK** toocreate hello project.</span></span>
8. <span data-ttu-id="ef29a-179">In **Solution Explorer**, in Hallo **FrontendWebRole** project, met de rechtermuisknop op **verwijzingen**, klikt u vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-179">In **Solution Explorer**, in hello **FrontendWebRole** project, right-click **References**, then click **Manage NuGet Packages**.</span></span>
9. <span data-ttu-id="ef29a-180">Klik op Hallo **Bladeren** tabblad en zoek naar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="ef29a-180">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="ef29a-181">Selecteer Hallo **WindowsAzure.ServiceBus** van het pakket, klikt u op **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-181">Select hello **WindowsAzure.ServiceBus** package, click **Install**, and accept hello terms of use.</span></span>
   
   ![][13]
   
   <span data-ttu-id="ef29a-182">Houd er rekening mee dat Hallo vereiste clientassembly nu wordt verwezen en enkele nieuwe codebestanden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ef29a-182">Note that hello required client assemblies are now referenced and some new code files have been added.</span></span>
10. <span data-ttu-id="ef29a-183">Klik in **Solution Explorer** met de rechtermuisknop op **Modellen** en klik achtereenvolgens op **Toevoegen** en **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-183">In **Solution Explorer**, right-click **Models** and click **Add**, then click **Class**.</span></span> <span data-ttu-id="ef29a-184">In Hallo **naam** vak, Hallo typenaam **OnlineOrder.cs**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-184">In hello **Name** box, type hello name **OnlineOrder.cs**.</span></span> <span data-ttu-id="ef29a-185">Klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-185">Then click **Add**.</span></span>

### <a name="write-hello-code-for-your-web-role"></a><span data-ttu-id="ef29a-186">Hallo-code voor de Webrol schrijven</span><span class="sxs-lookup"><span data-stu-id="ef29a-186">Write hello code for your web role</span></span>
<span data-ttu-id="ef29a-187">In deze sectie maakt u Hallo verschillende pagina's die uw toepassing worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef29a-187">In this section, you create hello various pages that your application displays.</span></span>

1. <span data-ttu-id="ef29a-188">Vervang de bestaande naamruimtedefinitie Hello na de code in Hallo OnlineOrder.cs bestand in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ef29a-188">In hello OnlineOrder.cs file in Visual Studio, replace the existing namespace definition with hello following code:</span></span>
   
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
2. <span data-ttu-id="ef29a-189">Dubbelklik in **Solution Explorer** op **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-189">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span> <span data-ttu-id="ef29a-190">Voeg de volgende Hallo **met** instructies Hallo Hallo bovenaan in het bestand tooinclude Hallo naamruimten voor het model dat u zojuist hebt gemaakt, maar ook voor Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ef29a-190">Add hello following **using** statements at hello top of hello file tooinclude hello namespaces for the model you just created, as well as Service Bus.</span></span>
   
   ```csharp
   using FrontendWebRole.Models;
   using Microsoft.ServiceBus.Messaging;
   using Microsoft.ServiceBus;
   ```
3. <span data-ttu-id="ef29a-191">Ook in Hallo HomeController.cs bestand in Visual Studio vervangt u de bestaande naamruimtedefinitie Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-191">Also in hello HomeController.cs file in Visual Studio, replace the existing namespace definition with hello following code.</span></span> <span data-ttu-id="ef29a-192">Deze code bevat methoden voor het indienen van items toohello wachtrij Hallo afhandelen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-192">This code contains methods for handling hello submission of items toohello queue.</span></span>
   
   ```csharp
   namespace FrontendWebRole.Controllers
   {
       public class HomeController : Controller
       {
           public ActionResult Index()
           {
               // Simply redirect tooSubmit, since Submit will serve as the
               // front page of this application.
               return RedirectToAction("Submit");
           }
   
           public ActionResult About()
           {
               return View();
           }
   
           // GET: /Home/Submit.
           // Controller method for a view you will create for hello submission
           // form.
           public ActionResult Submit()
           {
               // Will put code for displaying queue message count here.
   
               return View();
           }
   
           // POST: /Home/Submit.
           // Controller method for handling submissions from hello submission
           // form.
           [HttpPost]
           // Attribute toohelp prevent cross-site scripting attacks and
           // cross-site request forgery.  
           [ValidateAntiForgeryToken]
           public ActionResult Submit(OnlineOrder order)
           {
               if (ModelState.IsValid)
               {
                   // Will put code for submitting tooqueue here.
   
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
4. <span data-ttu-id="ef29a-193">Van Hallo **bouwen** menu, klikt u op **Build Solution** tootest Hallo juistheid van uw werk tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="ef29a-193">From hello **Build** menu, click **Build Solution** tootest hello accuracy of your work so far.</span></span>
5. <span data-ttu-id="ef29a-194">Maak nu de weergave Hallo voor Hallo `Submit()` methode die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef29a-194">Now, create hello view for hello `Submit()` method you created earlier.</span></span> <span data-ttu-id="ef29a-195">Met de rechtermuisknop op Hallo `Submit()` methode (Hallo overbelasting van de `Submit()` die geen parameters zijn vereist), en kies vervolgens **weergave toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-195">Right-click within hello `Submit()` method (hello overload of `Submit()` that takes no parameters), and then choose **Add View**.</span></span>
   
   ![][14]
6. <span data-ttu-id="ef29a-196">Er verschijnt een dialoogvenster voor het maken van Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="ef29a-196">A dialog box appears for creating hello view.</span></span> <span data-ttu-id="ef29a-197">In Hallo **sjabloon** Kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-197">In hello **Template** list, choose **Create**.</span></span> <span data-ttu-id="ef29a-198">In Hallo **Modelklasse** lijst, klikt u op Hallo **OnlineOrder** klasse.</span><span class="sxs-lookup"><span data-stu-id="ef29a-198">In hello **Model class** list, click hello **OnlineOrder** class.</span></span>
   
   ![][15]
7. <span data-ttu-id="ef29a-199">Klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-199">Click **Add**.</span></span>
8. <span data-ttu-id="ef29a-200">Wijzig nu de naam van uw toepassing hello weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef29a-200">Now, change hello displayed name of your application.</span></span> <span data-ttu-id="ef29a-201">In **Solution Explorer**, dubbelklikt u op de **Views\Shared\\_Layout.cshtml** tooopen bestand in Visual Studio-editor Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-201">In **Solution Explorer**, double-click the **Views\Shared\\_Layout.cshtml** file tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="ef29a-202">Vervang alle instanties van **Mijn ASP.NET-toepassing** door **Producten van LITWARE**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-202">Replace all occurrences of **My ASP.NET Application** with **LITWARE'S Products**.</span></span>
10. <span data-ttu-id="ef29a-203">Hallo verwijderen **Start**, **over**, en **Contact** koppelingen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-203">Remove hello **Home**, **About**, and **Contact** links.</span></span> <span data-ttu-id="ef29a-204">Verwijder Hallo gemarkeerde code:</span><span class="sxs-lookup"><span data-stu-id="ef29a-204">Delete hello highlighted code:</span></span>
    
    ![][28]
11. <span data-ttu-id="ef29a-205">Ten slotte wijzigen Hallo verzending pagina tooinclude enige informatie over Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ef29a-205">Finally, modify hello submission page tooinclude some information about hello queue.</span></span> <span data-ttu-id="ef29a-206">In **Solution Explorer**, dubbelklikt u op de **Views\Home\Submit.cshtml** tooopen bestand in Visual Studio-editor Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-206">In **Solution Explorer**, double-click the **Views\Home\Submit.cshtml** file tooopen it in hello Visual Studio editor.</span></span> <span data-ttu-id="ef29a-207">Hallo volgt regel na toevoegen `<h2>Submit</h2>`.</span><span class="sxs-lookup"><span data-stu-id="ef29a-207">Add hello following line after `<h2>Submit</h2>`.</span></span> <span data-ttu-id="ef29a-208">Op dit moment Hallo `ViewBag.MessageCount` is leeg.</span><span class="sxs-lookup"><span data-stu-id="ef29a-208">For now, hello `ViewBag.MessageCount` is empty.</span></span> <span data-ttu-id="ef29a-209">U vult dit later in.</span><span class="sxs-lookup"><span data-stu-id="ef29a-209">You will populate it later.</span></span>
    
    ```html
    <p>Current number of orders in queue waiting toobe processed: @ViewBag.MessageCount</p>
    ```
12. <span data-ttu-id="ef29a-210">U hebt nu de gebruikersinterface geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ef29a-210">You now have implemented your UI.</span></span> <span data-ttu-id="ef29a-211">U kunt ook op **F5** toorun uw toepassing en Bevestig dat het lijkt erop zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="ef29a-211">You can press **F5** toorun your application and confirm that it looks as expected.</span></span>
    
    ![][17]

### <a name="write-hello-code-for-submitting-items-tooa-service-bus-queue"></a><span data-ttu-id="ef29a-212">Hallo-code voor het indienen van items tooa Service Bus-wachtrij schrijven</span><span class="sxs-lookup"><span data-stu-id="ef29a-212">Write hello code for submitting items tooa Service Bus queue</span></span>
<span data-ttu-id="ef29a-213">Voeg nu code voor het indienen van items tooa wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ef29a-213">Now, add code for submitting items tooa queue.</span></span> <span data-ttu-id="ef29a-214">U maakt eerst een klasse die de verbindingsgegevens van de Service Bus-wachtrij bevat.</span><span class="sxs-lookup"><span data-stu-id="ef29a-214">First, you create a class that contains your Service Bus queue connection information.</span></span> <span data-ttu-id="ef29a-215">Vervolgens initialiseert u de verbinding vanuit Global.aspx.cs.</span><span class="sxs-lookup"><span data-stu-id="ef29a-215">Then, initialize your connection from Global.aspx.cs.</span></span> <span data-ttu-id="ef29a-216">Tot slot werkt Hallo verzendcode die u eerder in HomeController.cs tooactually indienen items tooa Service Bus-wachtrij gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef29a-216">Finally, update hello submission code you created earlier in HomeController.cs tooactually submit items tooa Service Bus queue.</span></span>

1. <span data-ttu-id="ef29a-217">In **Solution Explorer**, met de rechtermuisknop op **FrontendWebRole** (Klik met de rechtermuisknop Hallo project, niet Hallo rol).</span><span class="sxs-lookup"><span data-stu-id="ef29a-217">In **Solution Explorer**, right-click **FrontendWebRole** (right-click hello project, not hello role).</span></span> <span data-ttu-id="ef29a-218">Klik op **Toevoegen** en klik vervolgens op **Klasse**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-218">Click **Add**, and then click **Class**.</span></span>
2. <span data-ttu-id="ef29a-219">Naam Hallo klasse **QueueConnector.cs**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-219">Name hello class **QueueConnector.cs**.</span></span> <span data-ttu-id="ef29a-220">Klik op **toevoegen** toocreate Hallo-klasse.</span><span class="sxs-lookup"><span data-stu-id="ef29a-220">Click **Add** toocreate hello class.</span></span>
3. <span data-ttu-id="ef29a-221">Voeg nu code die de verbindingsgegevens Hallo ingekapseld en Hallo verbinding tooa Service Bus-wachtrij wordt geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="ef29a-221">Now, add code that encapsulates hello connection information and initializes hello connection tooa Service Bus queue.</span></span> <span data-ttu-id="ef29a-222">Vervang Hallo volledige inhoud van QueueConnector.cs door Hallo volgende code en voer waarden in voor `your Service Bus namespace` (uw naamruimtenaam) en `yourKey`, namelijk Hallo **primaire sleutel** u eerder hebt verkregen via hello Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="ef29a-222">Replace hello entire contents of QueueConnector.cs with hello following code, and enter values for `your Service Bus namespace` (your namespace name) and `yourKey`, which is hello **primary key** you previously obtained from hello Azure portal.</span></span>
   
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
   
           // Obtain these values from hello portal.
           public const string Namespace = "your Service Bus namespace";
   
           // hello name of your queue.
           public const string QueueName = "OrdersQueue";
   
           public static NamespaceManager CreateNamespaceManager()
           {
               // Create hello namespace manager which gives you access to
               // management operations.
               var uri = ServiceBusEnvironment.CreateServiceUri(
                   "sb", Namespace, String.Empty);
               var tP = TokenProvider.CreateSharedAccessSignatureTokenProvider(
                   "RootManageSharedAccessKey", "yourKey");
               return new NamespaceManager(uri, tP);
           }
   
           public static void Initialize()
           {
               // Using Http toobe friendly with outbound firewalls.
               ServiceBusEnvironment.SystemConnectivity.Mode =
                   ConnectivityMode.Http;
   
               // Create hello namespace manager which gives you access to
               // management operations.
               var namespaceManager = CreateNamespaceManager();
   
               // Create hello queue if it does not exist already.
               if (!namespaceManager.QueueExists(QueueName))
               {
                   namespaceManager.CreateQueue(QueueName);
               }
   
               // Get a client toohello queue.
               var messagingFactory = MessagingFactory.Create(
                   namespaceManager.Address,
                   namespaceManager.Settings.TokenProvider);
               OrdersQueueClient = messagingFactory.CreateQueueClient(
                   "OrdersQueue");
           }
       }
   }
   ```
4. <span data-ttu-id="ef29a-223">Controleer nu of uw methode voor **Initialiseren** wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-223">Now, ensure that your **Initialize** method gets called.</span></span> <span data-ttu-id="ef29a-224">Dubbelklik in **Solution Explorer** op **Global.asax\Global.asax.cs**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-224">In **Solution Explorer**, double-click **Global.asax\Global.asax.cs**.</span></span>
5. <span data-ttu-id="ef29a-225">Toevoegen van de volgende regel code achter Hallo HALLO hallo **Application_Start** methode.</span><span class="sxs-lookup"><span data-stu-id="ef29a-225">Add hello following line of code at hello end of hello **Application_Start** method.</span></span>
   
   ```csharp
   FrontendWebRole.QueueConnector.Initialize();
   ```
6. <span data-ttu-id="ef29a-226">Werk tot slot de Webcode die u eerder hebt gemaakt, als u items toohello wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-226">Finally, update hello web code you created earlier, to submit items toohello queue.</span></span> <span data-ttu-id="ef29a-227">Dubbelklik in **Solution Explorer** op **Controllers\HomeController.cs**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-227">In **Solution Explorer**, double-click **Controllers\HomeController.cs**.</span></span>
7. <span data-ttu-id="ef29a-228">Update Hallo `Submit()` methode (Hallo overbelasting waarvoor geen parameters zijn vereist) als volgt het Hallo-bericht tooget tellen voor Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ef29a-228">Update hello `Submit()` method (hello overload that takes no parameters) as follows tooget hello message count for hello queue.</span></span>
   
   ```csharp
   public ActionResult Submit()
   {
       // Get a NamespaceManager which allows you tooperform management and
       // diagnostic operations on your Service Bus queues.
       var namespaceManager = QueueConnector.CreateNamespaceManager();
   
       // Get hello queue, and obtain hello message count.
       var queue = namespaceManager.GetQueue(QueueConnector.QueueName);
       ViewBag.MessageCount = queue.MessageCount;
   
       return View();
   }
   ```
8. <span data-ttu-id="ef29a-229">Update Hallo `Submit(OnlineOrder order)` methode (Hallo overbelasting waarvoor één parameter) als volgt toosubmit informatie toohello wachtrij rangschikken.</span><span class="sxs-lookup"><span data-stu-id="ef29a-229">Update hello `Submit(OnlineOrder order)` method (hello overload that takes one parameter) as follows toosubmit order information toohello queue.</span></span>
   
   ```csharp
   public ActionResult Submit(OnlineOrder order)
   {
       if (ModelState.IsValid)
       {
           // Create a message from hello order.
           var message = new BrokeredMessage(order);
   
           // Submit hello order.
           QueueConnector.OrdersQueueClient.Send(message);
           return RedirectToAction("Submit");
       }
       else
       {
           return View(order);
       }
   }
   ```
9. <span data-ttu-id="ef29a-230">U kunt nu de toepassing hello opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ef29a-230">You can now run hello application again.</span></span> <span data-ttu-id="ef29a-231">Telkens wanneer die u een order verzendt aantal Hallo-berichten neemt toe.</span><span class="sxs-lookup"><span data-stu-id="ef29a-231">Each time you submit an order, hello message count increases.</span></span>
   
   ![][18]

## <a name="create-hello-worker-role"></a><span data-ttu-id="ef29a-232">Hallo-werkrol maken</span><span class="sxs-lookup"><span data-stu-id="ef29a-232">Create hello worker role</span></span>
<span data-ttu-id="ef29a-233">U maakt nu de werkrol Hallo waarmee Hallo volgorde van voorbeelden worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ef29a-233">You will now create hello worker role that processes hello order submissions.</span></span> <span data-ttu-id="ef29a-234">In dit voorbeeld wordt Hallo **Werkrol met Service Bus-wachtrij** Visual Studio-projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="ef29a-234">This example uses hello **Worker Role with Service Bus Queue** Visual Studio project template.</span></span> <span data-ttu-id="ef29a-235">U hebt al Hallo vereist referenties verkregen via Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ef29a-235">You already obtained hello required credentials from hello portal.</span></span>

1. <span data-ttu-id="ef29a-236">Zorg ervoor dat u Visual Studio tooyour Azure-account hebt gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ef29a-236">Make sure you have connected Visual Studio tooyour Azure account.</span></span>
2. <span data-ttu-id="ef29a-237">In Visual Studio in **Solution Explorer** met de rechtermuisknop op de **rollen** map onder Hallo **MultiTierApp** project.</span><span class="sxs-lookup"><span data-stu-id="ef29a-237">In Visual Studio, in **Solution Explorer** right-click the **Roles** folder under hello **MultiTierApp** project.</span></span>
3. <span data-ttu-id="ef29a-238">Klik op **Toevoegen** en klik vervolgens op **Nieuw werkrolproject**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-238">Click **Add**, and then click **New Worker Role Project**.</span></span> <span data-ttu-id="ef29a-239">Hallo **nieuw Rolproject toevoegen** dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ef29a-239">hello **Add New Role Project** dialog box appears.</span></span>
   
   ![][26]
4. <span data-ttu-id="ef29a-240">In Hallo **nieuw Rolproject toevoegen** in het dialoogvenster, klikt u op **Werkrol met Service Bus-wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-240">In hello **Add New Role Project** dialog box, click **Worker Role with Service Bus Queue**.</span></span>
   
   ![][23]
5. <span data-ttu-id="ef29a-241">In Hallo **naam** vak, naam Hallo project **OrderProcessingRole**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-241">In hello **Name** box, name hello project **OrderProcessingRole**.</span></span> <span data-ttu-id="ef29a-242">Klik vervolgens op **Toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-242">Then click **Add**.</span></span>
6. <span data-ttu-id="ef29a-243">Hallo-verbindingsreeks die u hebt verkregen in stap 9 van Hallo 'Een Servicebus-naamruimte maken' sectie toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ef29a-243">Copy hello connection string that you obtained in step 9 of hello "Create a Service Bus namespace" section toohello clipboard.</span></span>
7. <span data-ttu-id="ef29a-244">In **Solution Explorer**, klik met de rechtermuisknop Hallo **OrderProcessingRole** u in stap 5 hebt gemaakt (Zorg ervoor dat u met de rechtermuisknop op **OrderProcessingRole** onder **Rollen**, en niet Hallo klasse).</span><span class="sxs-lookup"><span data-stu-id="ef29a-244">In **Solution Explorer**, right-click hello **OrderProcessingRole** you created in step 5 (make sure that you right-click **OrderProcessingRole** under **Roles**, and not hello class).</span></span> <span data-ttu-id="ef29a-245">Klik vervolgens op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-245">Then click **Properties**.</span></span>
8. <span data-ttu-id="ef29a-246">Op Hallo **instellingen** tabblad Hallo **eigenschappen** in het dialoogvenster, klikt u in Hallo **waarde** vak voor **Microsoft.ServiceBus.ConnectionString**, en plak vervolgens Hallo-eindpuntwaarde die u in stap 6 hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="ef29a-246">On hello **Settings** tab of hello **Properties** dialog box, click inside hello **Value** box for **Microsoft.ServiceBus.ConnectionString**, and then paste hello endpoint value you copied in step 6.</span></span>
   
   ![][25]
9. <span data-ttu-id="ef29a-247">Maak een **OnlineOrder** toorepresent Hallo orders klasse tijdens het verwerken van Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ef29a-247">Create an **OnlineOrder** class toorepresent hello orders as you process them from hello queue.</span></span> <span data-ttu-id="ef29a-248">U kunt een klasse die u al hebt gemaakt opnieuw gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ef29a-248">You can reuse a class you have already created.</span></span> <span data-ttu-id="ef29a-249">In **Solution Explorer**, klik met de rechtermuisknop Hallo **OrderProcessingRole** klasse (Klik met de rechtermuisknop Hallo klassepictogram, niet Hallo rol).</span><span class="sxs-lookup"><span data-stu-id="ef29a-249">In **Solution Explorer**, right-click hello **OrderProcessingRole** class (right-click hello class icon, not hello role).</span></span> <span data-ttu-id="ef29a-250">Klik op **Toevoegen** en vervolgens op **Bestaand item**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-250">Click **Add**, then click **Existing Item**.</span></span>
10. <span data-ttu-id="ef29a-251">Blader toohello submap voor **FrontendWebRole\Models**, en dubbelklik vervolgens op **OnlineOrder.cs** tooadd het toothis project.</span><span class="sxs-lookup"><span data-stu-id="ef29a-251">Browse toohello subfolder for **FrontendWebRole\Models**, and then double-click **OnlineOrder.cs** tooadd it toothis project.</span></span>
11. <span data-ttu-id="ef29a-252">In **WorkerRole.cs**, wijzig de waarde Hallo Hallo **wachtrijnaam** variabele van `"ProcessingQueue"` te`"OrdersQueue"` zoals weergegeven in de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="ef29a-252">In **WorkerRole.cs**, change hello value of hello **QueueName** variable from `"ProcessingQueue"` too`"OrdersQueue"` as shown in hello following code.</span></span>
    
    ```csharp
    // hello name of your queue.
    const string QueueName = "OrdersQueue";
    ```
12. <span data-ttu-id="ef29a-253">Voeg de volgende Hallo gebruiksinstructie Hallo boven aan het Hallo-WorkerRole.cs-bestand.</span><span class="sxs-lookup"><span data-stu-id="ef29a-253">Add hello following using statement at hello top of hello WorkerRole.cs file.</span></span>
    
    ```csharp
    using FrontendWebRole.Models;
    ```
13. <span data-ttu-id="ef29a-254">In Hallo `Run()` functie binnen Hallo `OnMessage()` aanroepen, vervang de inhoud Hallo Hallo `try` component Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="ef29a-254">In hello `Run()` function, inside hello `OnMessage()` call, replace hello contents of hello `try` clause with hello following code.</span></span>
    
    ```csharp
    Trace.WriteLine("Processing", receivedMessage.SequenceNumber.ToString());
    // View hello message as an OnlineOrder.
    OnlineOrder order = receivedMessage.GetBody<OnlineOrder>();
    Trace.WriteLine(order.Customer + ": " + order.Product, "ProcessingMessage");
    receivedMessage.Complete();
    ```
14. <span data-ttu-id="ef29a-255">U kunt de toepassing hello hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="ef29a-255">You have completed hello application.</span></span> <span data-ttu-id="ef29a-256">U kunt de volledige toepassing hello testen door met de rechtermuisknop op Hallo MultiTierApp-project in Solution Explorer selecteren **instellen als opstartproject**, en klik vervolgens op F5 te drukken.</span><span class="sxs-lookup"><span data-stu-id="ef29a-256">You can test hello full application by right-clicking hello MultiTierApp project in Solution Explorer, selecting **Set as Startup Project**, and then pressing F5.</span></span> <span data-ttu-id="ef29a-257">Houd er rekening mee dat het aantal berichten niet toeneemt, omdat het Hallo-werkrol items uit de wachtrij hello, verwerkt en als voltooid markeert.</span><span class="sxs-lookup"><span data-stu-id="ef29a-257">Note that the message count does not increment, because hello worker role processes items from hello queue and marks them as complete.</span></span> <span data-ttu-id="ef29a-258">U ziet Hallo trace-uitvoer van uw werkrol door hello Azure Compute-Emulator gebruikersinterface weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ef29a-258">You can see hello trace output of your worker role by viewing hello Azure Compute Emulator UI.</span></span> <span data-ttu-id="ef29a-259">U kunt dit doen met de rechtermuisknop op Hallo emulatorpictogram in systeemvak Hallo van de taakbalk en selecteer **weergeven Compute-Emulator UI**.</span><span class="sxs-lookup"><span data-stu-id="ef29a-259">You can do this by right-clicking hello emulator icon in hello notification area of your taskbar and selecting **Show Compute Emulator UI**.</span></span>
    
    ![][19]
    
    ![][20]

## <a name="next-steps"></a><span data-ttu-id="ef29a-260">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ef29a-260">Next steps</span></span>
<span data-ttu-id="ef29a-261">toolearn meer informatie over Service Bus Zie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="ef29a-261">toolearn more about Service Bus, see hello following resources:</span></span>  

* <span data-ttu-id="ef29a-262">[Documentatie voor Azure Service Bus][sbdocs]</span><span class="sxs-lookup"><span data-stu-id="ef29a-262">[Azure Service Bus documentation][sbdocs]</span></span>  
* <span data-ttu-id="ef29a-263">[Service Bus-servicepagina][sbacom]</span><span class="sxs-lookup"><span data-stu-id="ef29a-263">[Service Bus service page][sbacom]</span></span>  
* <span data-ttu-id="ef29a-264">[Hoe tooUse Service Bus-wachtrijen][sbacomqhowto]</span><span class="sxs-lookup"><span data-stu-id="ef29a-264">[How tooUse Service Bus Queues][sbacomqhowto]</span></span>  

<span data-ttu-id="ef29a-265">toolearn meer informatie over scenario's met meerdere lagen, Zie:</span><span class="sxs-lookup"><span data-stu-id="ef29a-265">toolearn more about multi-tier scenarios, see:</span></span>  

* <span data-ttu-id="ef29a-266">[.NET-toepassing met meerdere lagen met Table Storage, Queue Storage en Blob Storage][mutitierstorage]</span><span class="sxs-lookup"><span data-stu-id="ef29a-266">[.NET Multi-Tier Application Using Storage Tables, Queues, and Blobs][mutitierstorage]</span></span>  

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

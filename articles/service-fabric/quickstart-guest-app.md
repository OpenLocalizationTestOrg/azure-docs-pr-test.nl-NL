---
title: aaaQuickly een bestaande app tooan Azure Service Fabric-cluster implementeren
description: Een Azure Service Fabric-cluster toohost een bestaande Node.js-toepassing met Visual Studio gebruiken.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a><span data-ttu-id="c3a3b-103">Een Node.js-toepassing hosten in Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c3a3b-103">Host a Node.js application on Azure Service Fabric</span></span>

<span data-ttu-id="c3a3b-104">Deze snelstartgids kunt u een bestaande toepassing (Node.js in dit voorbeeld) tooa Service Fabric-cluster implementeren uitgevoerd op Azure.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-104">This quickstart helps you deploy an existing application (Node.js in this example) tooa Service Fabric cluster running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3a3b-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c3a3b-105">Prerequisites</span></span>

<span data-ttu-id="c3a3b-106">Voordat u begint, zorgt u ervoor dat u [uw ontwikkelingsomgeving hebt ingesteld](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3a3b-106">Before you get started, make sure that you have [set up your development environment](service-fabric-get-started.md).</span></span> <span data-ttu-id="c3a3b-107">Dit omvat Hallo Service Fabric SDK en Visual Studio 2017 of 2015 installeren.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-107">Which includes installing hello Service Fabric SDK and Visual Studio 2017 or 2015.</span></span>

<span data-ttu-id="c3a3b-108">U moet ook een bestaande Node.js-toepassing toohave voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-108">You also need toohave an existing Node.js application for deployment.</span></span> <span data-ttu-id="c3a3b-109">Deze snelstartgids maakt gebruik van een eenvoudige Node.js-website die [hier][download-sample] kan worden gedownload.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-109">This quickstart uses a simple Node.js website that can be downloaded [here][download-sample].</span></span> <span data-ttu-id="c3a3b-110">Dit bestand tooyour uitpakken `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` map nadat u in de volgende stap Hallo Hallo-project maakt.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-110">Extract this file tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` folder after you create hello project in hello next step.</span></span>

<span data-ttu-id="c3a3b-111">Als u nog geen abonnement op Azure hebt, maak dan een [gratis account][create-account] aan.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-111">If you don't have an Azure subscription, create a [free account][create-account].</span></span>

## <a name="create-hello-service"></a><span data-ttu-id="c3a3b-112">Hallo-service maken</span><span class="sxs-lookup"><span data-stu-id="c3a3b-112">Create hello service</span></span>

<span data-ttu-id="c3a3b-113">Start Visual Studio als **beheerder**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-113">Launch Visual Studio as an **administrator**.</span></span>

<span data-ttu-id="c3a3b-114">Maak een project met `CTRL`+`SHIFT`+`N`</span><span class="sxs-lookup"><span data-stu-id="c3a3b-114">Create a project with `CTRL`+`SHIFT`+`N`</span></span>

<span data-ttu-id="c3a3b-115">In Hallo **nieuw Project** dialoogvenster kiezen **Cloud > Service Fabric-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-115">In hello **New Project** dialog, choose **Cloud > Service Fabric Application**.</span></span>

<span data-ttu-id="c3a3b-116">Naam van de toepassing hello **MyGuestApp** en druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-116">Name hello application **MyGuestApp** and press **OK**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c3a3b-117">Node.js kunnen eenvoudig 260 tekens voor paden met windows hello worden verbroken.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-117">Node.js can easily break hello 260 character limit for paths that windows has.</span></span> <span data-ttu-id="c3a3b-118">Een korte pad gebruiken voor het Hallo-project zelf zoals **c:\code\svc1**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-118">Use a short path for hello project itself such as **c:\code\svc1**.</span></span>
   
![Dialoogvenster voor nieuw project in Visual Studio][new-project]

<span data-ttu-id="c3a3b-120">U kunt elk type Service Fabric-service van het volgende dialoogvenster Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-120">You can create any type of Service Fabric service from hello next dialog.</span></span> <span data-ttu-id="c3a3b-121">Kies voor deze snelstartgids **Door gast uitvoerbaar bestand**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-121">For this quickstart, choose **Guest Executable**.</span></span>

<span data-ttu-id="c3a3b-122">Service voor Hallo **MyGuestService** en Hallo opties instellen op de juiste toohello Hallo de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="c3a3b-122">Name hello service **MyGuestService** and set hello options on hello right toohello following values:</span></span>

| <span data-ttu-id="c3a3b-123">Instelling</span><span class="sxs-lookup"><span data-stu-id="c3a3b-123">Setting</span></span>                   | <span data-ttu-id="c3a3b-124">Waarde</span><span class="sxs-lookup"><span data-stu-id="c3a3b-124">Value</span></span> |
| ------------------------- | ------ |
| <span data-ttu-id="c3a3b-125">Map met codepakket</span><span class="sxs-lookup"><span data-stu-id="c3a3b-125">Code Package Folder</span></span>       | <span data-ttu-id="c3a3b-126">_&lt;Hallo-map met uw Node.js-app&gt;_</span><span class="sxs-lookup"><span data-stu-id="c3a3b-126">_&lt;hello folder with your Node.js app&gt;_</span></span> |
| <span data-ttu-id="c3a3b-127">Gedrag codepakket</span><span class="sxs-lookup"><span data-stu-id="c3a3b-127">Code Package Behavior</span></span>     | <span data-ttu-id="c3a3b-128">Kopieer de map inhoud tooproject</span><span class="sxs-lookup"><span data-stu-id="c3a3b-128">Copy folder contents tooproject</span></span> |
| <span data-ttu-id="c3a3b-129">Programma</span><span class="sxs-lookup"><span data-stu-id="c3a3b-129">Program</span></span>                   | <span data-ttu-id="c3a3b-130">node.exe</span><span class="sxs-lookup"><span data-stu-id="c3a3b-130">node.exe</span></span> |
| <span data-ttu-id="c3a3b-131">Argumenten</span><span class="sxs-lookup"><span data-stu-id="c3a3b-131">Arguments</span></span>                 | <span data-ttu-id="c3a3b-132">server.js</span><span class="sxs-lookup"><span data-stu-id="c3a3b-132">server.js</span></span> |
| <span data-ttu-id="c3a3b-133">Werkmap</span><span class="sxs-lookup"><span data-stu-id="c3a3b-133">Working Folder</span></span>            | <span data-ttu-id="c3a3b-134">CodePackage</span><span class="sxs-lookup"><span data-stu-id="c3a3b-134">CodePackage</span></span> |

<span data-ttu-id="c3a3b-135">Druk op **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-135">Press **OK**.</span></span>

![Dialoogvenster voor nieuwe service in Visual Studio][new-service]

<span data-ttu-id="c3a3b-137">Visual Studio maakt het toepassingsproject Hallo en Hallo actor-serviceproject en geeft deze weer in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-137">Visual Studio creates hello application project and hello actor service project and displays them in Solution Explorer.</span></span>

<span data-ttu-id="c3a3b-138">Hallo-toepassingsproject (**MyGuestApp**) bevat geen code rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-138">hello application project (**MyGuestApp**) does not contain any code directly.</span></span> <span data-ttu-id="c3a3b-139">Het verwijst naar een reeks serviceprojecten.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-139">Instead, it references a set of service projects.</span></span> <span data-ttu-id="c3a3b-140">Daarnaast bevat het project drie andere typen inhoud:</span><span class="sxs-lookup"><span data-stu-id="c3a3b-140">In addition, it contains three other types of content:</span></span>

* <span data-ttu-id="c3a3b-141">**Profielen publiceren**</span><span class="sxs-lookup"><span data-stu-id="c3a3b-141">**Publish profiles**</span></span>  
<span data-ttu-id="c3a3b-142">Hulpprogrammavoorkeuren voor verschillende omgevingen.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-142">Tooling preferences for different environments.</span></span>

* <span data-ttu-id="c3a3b-143">**Scripts**</span><span class="sxs-lookup"><span data-stu-id="c3a3b-143">**Scripts**</span></span>  
<span data-ttu-id="c3a3b-144">PowerShell-script voor het implementeren/bijwerken van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-144">PowerShell script for deploying/upgrading your application.</span></span>

* <span data-ttu-id="c3a3b-145">**Toepassingsdefinitie**</span><span class="sxs-lookup"><span data-stu-id="c3a3b-145">**Application definition**</span></span>  
<span data-ttu-id="c3a3b-146">Hallo-toepassingsmanifest onder omvat *ApplicationPackageRoot*.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-146">Includes hello application manifest under *ApplicationPackageRoot*.</span></span> <span data-ttu-id="c3a3b-147">Bijbehorende parameter voor toepassingsbestanden onder zijn *ApplicationParameters*, die toepassing hello definiëren en kunt u tooconfigure specifiek voor een bepaalde omgeving.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-147">Associated application parameter files are under *ApplicationParameters*, which define hello application and allow you tooconfigure it specifically for a given environment.</span></span>
    
<span data-ttu-id="c3a3b-148">Zie voor een overzicht van Hallo inhoud van het serviceproject Hallo [aan de slag met Reliable Services](service-fabric-reliable-services-quick-start.md).</span><span class="sxs-lookup"><span data-stu-id="c3a3b-148">For an overview of hello contents of hello service project, see [Getting started with Reliable Services](service-fabric-reliable-services-quick-start.md).</span></span>

## <a name="set-up-networking"></a><span data-ttu-id="c3a3b-149">Netwerkservice instellen</span><span class="sxs-lookup"><span data-stu-id="c3a3b-149">Set up networking</span></span>

<span data-ttu-id="c3a3b-150">Hallo-voorbeeld we implementeert Node.js-app gebruikt poort **80** en moeten tootell Service Fabric die we nodig hebben die poort weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-150">hello example Node.js app we're deploying uses port **80** and we need tootell Service Fabric that we need that port exposed.</span></span>

<span data-ttu-id="c3a3b-151">Open Hallo **ServiceManifest.xml** bestand in Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-151">Open hello **ServiceManifest.xml** file in hello project.</span></span> <span data-ttu-id="c3a3b-152">Aan de onderkant van de Hallo van Hallo manifest, er is een `<Resources> \ <Endpoints>` met een vermelding is al gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-152">At hello bottom of hello manifest, there is a `<Resources> \ <Endpoints>` with an entry already defined.</span></span> <span data-ttu-id="c3a3b-153">Wijzigen van deze vermelding tooadd `Port`, `Protocol`, en `Type`.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-153">Modify that entry tooadd `Port`, `Protocol`, and `Type`.</span></span> 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a><span data-ttu-id="c3a3b-154">TooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="c3a3b-154">Deploy tooAzure</span></span>

<span data-ttu-id="c3a3b-155">Als u op **F5** en Hallo-project uitvoeren, is het lokale cluster geïmplementeerde toohello.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-155">If you press **F5** and run hello project, it is deployed toohello local cluster.</span></span> <span data-ttu-id="c3a3b-156">We gaan echter tooAzure in plaats daarvan implementeren.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-156">However, let's deploy tooAzure instead.</span></span>

<span data-ttu-id="c3a3b-157">Met de rechtermuisknop op het Hallo-project en kies **publiceren...**  waarmee u een dialoogvenster toopublish tooAzure opent.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-157">Right-click on hello project and choose **Publish...** which opens a dialog toopublish tooAzure.</span></span>

![Dialoogvenster tooazure voor een service fabric-service publiceren][publish]

<span data-ttu-id="c3a3b-159">Selecteer Hallo **PublishProfiles\Cloud.xml** profiel als doel.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-159">Select hello **PublishProfiles\Cloud.xml** target profile.</span></span>

<span data-ttu-id="c3a3b-160">Als u niet eerder hebt, kiest u een Azure-account toodeploy naar.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-160">If you haven't previously, choose an Azure account toodeploy to.</span></span> <span data-ttu-id="c3a3b-161">Als u er nog geen hebt, [meldt u zich er voor een aan][create-account].</span><span class="sxs-lookup"><span data-stu-id="c3a3b-161">If you don't have one yet, [sign-up for one][create-account].</span></span>

<span data-ttu-id="c3a3b-162">Onder **verbindingseindpunt**, selecteer Hallo toodeploy voor Service Fabric-cluster aan.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-162">Under **Connection Endpoint**, select hello Service Fabric cluster toodeploy to.</span></span> <span data-ttu-id="c3a3b-163">Als u geen abonnement hebt, selecteert u  **&lt;nieuw Cluster maken... &gt;**  die web browser venster toohello Azure-portal wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-163">If you do not have one, select **&lt;Create New Cluster...&gt;** which opens up web browser window toohello Azure portal.</span></span> <span data-ttu-id="c3a3b-164">Zie voor meer informatie [maken van een cluster in Hallo portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c3a3b-164">For more information, see [create a cluster in hello portal](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal).</span></span> 

<span data-ttu-id="c3a3b-165">Wanneer u Hallo Service Fabric-cluster maakt, moet u ervoor dat tooset hello **aangepaste eindpunten** instellen te**80**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-165">When you create hello Service Fabric cluster, make sure tooset hello **Custom endpoints** setting too**80**.</span></span>

![Service Fabric-knooppuntconfiguratie met aangepast eindpunt][custom-endpoint]

<span data-ttu-id="c3a3b-167">Maken van een nieuwe Service Fabric-cluster duurt enige tijd toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-167">Creating a new Service Fabric cluster takes some time toocomplete.</span></span> <span data-ttu-id="c3a3b-168">Nadat deze is gemaakt, gaat u terug toohello dialoogvenster publiceren en selecteer  **&lt;vernieuwen&gt;**.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-168">Once it has been created, go back toohello publish dialog and select **&lt;Refresh&gt;**.</span></span> <span data-ttu-id="c3a3b-169">het nieuwe cluster Hello wordt vermeld in de vervolgkeuzelijst Hallo; Selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-169">hello new cluster is listed in hello drop-down box; select it.</span></span>

<span data-ttu-id="c3a3b-170">Druk op **publiceren** en wachten op Hallo implementatie toofinish.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-170">Press **Publish** and wait for hello deployment toofinish.</span></span>

<span data-ttu-id="c3a3b-171">Dit kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-171">This may take a few minutes.</span></span> <span data-ttu-id="c3a3b-172">Nadat deze is voltooid, wordt het duurt enkele minuten voor Hallo toepassing toobe volledig beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-172">After it completes, it may take a few more minutes for hello application toobe fully available.</span></span>

## <a name="test-hello-website"></a><span data-ttu-id="c3a3b-173">Test Hallo website</span><span class="sxs-lookup"><span data-stu-id="c3a3b-173">Test hello website</span></span>

<span data-ttu-id="c3a3b-174">Test uw service na publicatie in een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-174">After your service has been published, test it in a web browser.</span></span> 

<span data-ttu-id="c3a3b-175">Eerst openen hello Azure-portal en zoek de Service Fabric-service.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-175">First, open hello Azure portal and find your Service Fabric service.</span></span>

<span data-ttu-id="c3a3b-176">Ga naar de blade overzicht Hallo van Hallo-serviceadres.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-176">Check hello overview blade of hello service address.</span></span> <span data-ttu-id="c3a3b-177">Hallo-domeinnaam voor gebruik van Hallo _verbindingseindpunt Client_ eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-177">Use hello domain name from hello _Client connection endpoint_ property.</span></span> <span data-ttu-id="c3a3b-178">Bijvoorbeeld `http://mysvcfab1.westus2.cloudapp.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-178">For example, `http://mysvcfab1.westus2.cloudapp.azure.com`.</span></span>

![Service fabric-overzichtsblade op Hallo Azure-portal][overview]

<span data-ttu-id="c3a3b-180">Navigeer toothis adres waar u Hallo ziet `HELLO WORLD` antwoord.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-180">Navigate toothis address where you will see hello `HELLO WORLD` response.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="c3a3b-181">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="c3a3b-181">Delete hello cluster</span></span>

<span data-ttu-id="c3a3b-182">Vergeet niet alle Hallo-resources die u hebt gemaakt voor deze snelstartgids, als u in rekening voor die resources gebracht toodelete.</span><span class="sxs-lookup"><span data-stu-id="c3a3b-182">Do not forget toodelete all of hello resources you've created for this quickstart, as you are charged for those resources.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3a3b-183">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3a3b-183">Next steps</span></span>
<span data-ttu-id="c3a3b-184">Lees meer over [door gast uitvoerbare bestanden](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="c3a3b-184">Read more about [guest executables](service-fabric-deploy-existing-app.md).</span></span>

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F
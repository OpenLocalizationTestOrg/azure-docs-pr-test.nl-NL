---
title: aaaGet slag met Azure Search in Java | Microsoft Docs
description: Hoe zoeken toobuild een gehoste cloud toepassing in Azure met behulp van Java als uw programmeertaal.
services: search
documentationcenter: 
author: EvanBoyle
manager: pablocas
editor: v-lincan
ms.assetid: 8b4df3c9-3ae5-4e3a-b4bb-74b516a91c8e
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 07/14/2016
ms.author: evboyle
ms.openlocfilehash: 5476a2103f3b60fe6ec78ff3d3fdba9fcff55c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-search-in-java"></a><span data-ttu-id="7d85f-103">Aan de slag met Azure Search in Java</span><span class="sxs-lookup"><span data-stu-id="7d85f-103">Get started with Azure Search in Java</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7d85f-104">Portal</span><span class="sxs-lookup"><span data-stu-id="7d85f-104">Portal</span></span>](search-get-started-portal.md)
> * [<span data-ttu-id="7d85f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7d85f-105">.NET</span></span>](search-howto-dotnet-sdk.md)
> 
> 

<span data-ttu-id="7d85f-106">Meer informatie over hoe toobuild een aangepaste Java-toepassing die gebruikmaakt van Azure Search voor de zoekfunctie zoeken.</span><span class="sxs-lookup"><span data-stu-id="7d85f-106">Learn how toobuild a custom Java search application that uses Azure Search for its search experience.</span></span> <span data-ttu-id="7d85f-107">Deze zelfstudie wordt gebruikgemaakt van Hallo [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct Hallo objecten en bewerkingen in deze oefening.</span><span class="sxs-lookup"><span data-stu-id="7d85f-107">This tutorial uses hello [Azure Search Service REST API](https://msdn.microsoft.com/library/dn798935.aspx) tooconstruct hello objects and operations used in this exercise.</span></span>

<span data-ttu-id="7d85f-108">toorun dit voorbeeld hebt u een Azure Search-service, u voor Hallo aanmelden kunt [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d85f-108">toorun this sample, you must have an Azure Search service, which you can sign up for in hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="7d85f-109">Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="7d85f-109">See [Create an Azure Search service in hello portal](search-create-service-portal.md) for step-by-step instructions.</span></span>

<span data-ttu-id="7d85f-110">We Hallo na software toobuild gebruikt en testen van dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7d85f-110">We used hello following software toobuild and test this sample:</span></span>

* <span data-ttu-id="7d85f-111">[Eclipse IDE voor Java EE-ontwikkelaars](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span><span class="sxs-lookup"><span data-stu-id="7d85f-111">[Eclipse IDE for Java EE Developers](https://eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/lunar).</span></span> <span data-ttu-id="7d85f-112">Worden ervoor toodownload Hallo EE-versie.</span><span class="sxs-lookup"><span data-stu-id="7d85f-112">Be sure toodownload hello EE version.</span></span> <span data-ttu-id="7d85f-113">Een van de verificatiestappen Hallo vereist een functie die alleen in deze versie is gevonden.</span><span class="sxs-lookup"><span data-stu-id="7d85f-113">One of hello verification steps requires a feature that is found only in this edition.</span></span>
* [<span data-ttu-id="7d85f-114">JDK 8u40</span><span class="sxs-lookup"><span data-stu-id="7d85f-114">JDK 8u40</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
* [<span data-ttu-id="7d85f-115">Apache Tomcat 8.0</span><span class="sxs-lookup"><span data-stu-id="7d85f-115">Apache Tomcat 8.0</span></span>](http://tomcat.apache.org/download-80.cgi)

## <a name="about-hello-data"></a><span data-ttu-id="7d85f-116">Over Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="7d85f-116">About hello data</span></span>
<span data-ttu-id="7d85f-117">Deze voorbeeldtoepassing gebruikt gegevens uit Hallo [Verenigde Staten Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), gefilterd op Hallo staat Rhode Island tooreduce Hallo gegevensset grootte.</span><span class="sxs-lookup"><span data-stu-id="7d85f-117">This sample application uses data from hello [United States Geological Services (USGS)](http://geonames.usgs.gov/domestic/download_data.htm), filtered on hello state of Rhode Island tooreduce hello dataset size.</span></span> <span data-ttu-id="7d85f-118">We gebruiken deze gegevens toobuild een zoektoepassing die kenmerkende gebouwen zoals ziekenhuizen en scholen, evenals geologische kenmerken, zoals stromen, meren en toppen retourneert.</span><span class="sxs-lookup"><span data-stu-id="7d85f-118">We'll use this data toobuild a search application that returns landmark buildings such as hospitals and schools, as well as geological features like streams, lakes, and summits.</span></span>

<span data-ttu-id="7d85f-119">In deze toepassing hello **SearchServlet.java** programma bouwt en belastingen Hallo index met behulp van een [indexeerfunctie](https://msdn.microsoft.com/library/azure/dn798918.aspx) constructie, bij het ophalen van Hallo gefilterde USGS-gegevensset uit een openbare Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7d85f-119">In this application, hello **SearchServlet.java** program builds and loads hello index using an [Indexer](https://msdn.microsoft.com/library/azure/dn798918.aspx) construct, retrieving hello filtered USGS dataset from a public Azure SQL Database.</span></span> <span data-ttu-id="7d85f-120">Vooraf gedefinieerde referenties en informatie toohello Onlinegegevens verbindingsbron vindt u in Hallo programmacode.</span><span class="sxs-lookup"><span data-stu-id="7d85f-120">Predefined credentials and connection  information toohello online data source are provided in hello program code.</span></span> <span data-ttu-id="7d85f-121">Voor de toegang tot de gegevens hoeft u verder niets te configureren.</span><span class="sxs-lookup"><span data-stu-id="7d85f-121">In terms of data access, no further configuration is necessary.</span></span>

> [!NOTE]
> <span data-ttu-id="7d85f-122">We een filter toegepast op deze gegevensset toostay onder Hallo 10.000 Documentlimiet Hallo gratis prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="7d85f-122">We applied a filter on this dataset toostay under hello 10,000 document limit of hello free pricing tier.</span></span> <span data-ttu-id="7d85f-123">Als u de standaardcategorie Hallo gebruikt, deze limiet niet van toepassing en kunt u deze code toouse een grotere gegevensset wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7d85f-123">If you use hello standard tier, this limit does not apply, and you can modify this code toouse a bigger dataset.</span></span> <span data-ttu-id="7d85f-124">Zie [Limieten en beperkingen](search-limits-quotas-capacity.md) voor meer informatie over de capaciteit voor elke prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="7d85f-124">For details about capacity for each pricing tier, see [Limits and constraints](search-limits-quotas-capacity.md).</span></span>
> 
> 

## <a name="about-hello-program-files"></a><span data-ttu-id="7d85f-125">Over het Hallo-programmabestanden</span><span class="sxs-lookup"><span data-stu-id="7d85f-125">About hello program files</span></span>
<span data-ttu-id="7d85f-126">Hallo hieronder wordt beschreven Hallo-bestanden die betrokken toothis voorbeeld zijn.</span><span class="sxs-lookup"><span data-stu-id="7d85f-126">hello following list describes hello files that are relevant toothis sample.</span></span>

* <span data-ttu-id="7d85f-127">Search.JSP: Levert Hallo-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="7d85f-127">Search.jsp: Provides hello user interface</span></span>
* <span data-ttu-id="7d85f-128">SearchServlet.java: Biedt methoden (vergelijkbaar tooa controller in MVC)</span><span class="sxs-lookup"><span data-stu-id="7d85f-128">SearchServlet.java: Provides methods (similar tooa controller in MVC)</span></span>
* <span data-ttu-id="7d85f-129">SearchServiceClient.java: verwerkt de HTTP-aanvragen</span><span class="sxs-lookup"><span data-stu-id="7d85f-129">SearchServiceClient.java: Handles HTTP requests</span></span>
* <span data-ttu-id="7d85f-130">SearchServiceHelper.java: een helperklasse die statische methoden biedt</span><span class="sxs-lookup"><span data-stu-id="7d85f-130">SearchServiceHelper.java: A helper class that provides static methods</span></span>
* <span data-ttu-id="7d85f-131">Document.Java: Levert het gegevensmodel Hallo</span><span class="sxs-lookup"><span data-stu-id="7d85f-131">Document.java: Provides hello data model</span></span>
* <span data-ttu-id="7d85f-132">Config.Properties: stelt Hallo Search-service-URL en api-sleutel</span><span class="sxs-lookup"><span data-stu-id="7d85f-132">config.properties: Sets hello Search service URL and api-key</span></span>
* <span data-ttu-id="7d85f-133">Pom.XML: een Maven-afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="7d85f-133">Pom.xml: A Maven dependency</span></span>

<a id="sub-2"></a>

## <a name="find-hello-service-name-and-api-key-of-your-azure-search-service"></a><span data-ttu-id="7d85f-134">Hallo-servicenaam en api-sleutel van uw Azure Search-service zoeken</span><span class="sxs-lookup"><span data-stu-id="7d85f-134">Find hello service name and api-key of your Azure Search service</span></span>
<span data-ttu-id="7d85f-135">Alle REST-API-aanroepen in Azure Search is vereist dat u Hallo service-URL en api-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="7d85f-135">All REST API calls into Azure Search require that you provide hello service URL and an api-key.</span></span> 

1. <span data-ttu-id="7d85f-136">Meld u aan toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7d85f-136">Sign in toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7d85f-137">Klik in de snelbalk hello **zoekservice** toolist alle hello Azure Search-services worden ingericht voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7d85f-137">In hello jump bar, click **Search service** toolist all of hello Azure Search services provisioned for your subscription.</span></span>
3. <span data-ttu-id="7d85f-138">Selecteer de gewenste toouse Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7d85f-138">Select hello service you want toouse.</span></span>
4. <span data-ttu-id="7d85f-139">Op Hallo servicedashboard ziet u tegels weergegeven voor essentiële informatie evenals sleutelpictogram voor toegang tot de beheersleutels Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d85f-139">On hello service dashboard, you'll see tiles for essential information as well as hello key icon for accessing hello admin keys.</span></span>
   
      ![][3]
5. <span data-ttu-id="7d85f-140">Kopieer Hallo service-URL en een beheersleutel.</span><span class="sxs-lookup"><span data-stu-id="7d85f-140">Copy hello service URL and an admin key.</span></span> <span data-ttu-id="7d85f-141">Moet u ze later, wanneer u ze toohello toevoegt **config.properties** bestand.</span><span class="sxs-lookup"><span data-stu-id="7d85f-141">You will need them later, when you add them toohello **config.properties** file.</span></span>

## <a name="download-hello-sample-files"></a><span data-ttu-id="7d85f-142">Hallo voorbeeldbestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="7d85f-142">Download hello sample files</span></span>
1. <span data-ttu-id="7d85f-143">Ga te[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d85f-143">Go too[AzureSearchJavaDemo](https://github.com/AzureSearch/AzureSearchJavaIndexerDemo) on GitHub.</span></span>
2. <span data-ttu-id="7d85f-144">Klik op **ZIP downloaden**, Hallo ZIP-bestand toodisk opslaan en pak vervolgens alle Hallo bestanden bevat.</span><span class="sxs-lookup"><span data-stu-id="7d85f-144">Click **Download ZIP**, save hello .zip file toodisk, and then extract all hello files it contains.</span></span> <span data-ttu-id="7d85f-145">Houd rekening met het uitpakken van Hallo-bestanden in uw werkruimte Java toomake eenvoudiger toofind Hallo project later.</span><span class="sxs-lookup"><span data-stu-id="7d85f-145">Consider extracting hello files into your Java workspace toomake it easier toofind hello project later.</span></span>
3. <span data-ttu-id="7d85f-146">Hallo voorbeeldbestanden zijn alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="7d85f-146">hello sample files are read-only.</span></span> <span data-ttu-id="7d85f-147">Met de rechtermuisknop op mapeigenschappen en wissen Hallo-kenmerk voor alleen-lezen.</span><span class="sxs-lookup"><span data-stu-id="7d85f-147">Right-click folder properties and clear hello read-only attribute.</span></span>

<span data-ttu-id="7d85f-148">Alle volgende bestandswijzigingen en uitvoerinstructies worden uitgevoerd voor de bestanden in deze map.</span><span class="sxs-lookup"><span data-stu-id="7d85f-148">All subsequent file modifications and run statements will be made against files in this folder.</span></span>  

## <a name="import-project"></a><span data-ttu-id="7d85f-149">Project importeren</span><span class="sxs-lookup"><span data-stu-id="7d85f-149">Import project</span></span>
1. <span data-ttu-id="7d85f-150">Klik in Eclipse achtereenvolgens op **File** >  (Bestand)**Import** (Importeren) > **General** (Algemeen) > **Existing Projects into Workspace** (Bestaand project naar werkruimte).</span><span class="sxs-lookup"><span data-stu-id="7d85f-150">In Eclipse, choose **File** > **Import** > **General** > **Existing Projects into Workspace**.</span></span>
   
    ![][4]
2. <span data-ttu-id="7d85f-151">In **Selecteer hoofdmap**, toohello map met de voorbeeldbestanden bladeren.</span><span class="sxs-lookup"><span data-stu-id="7d85f-151">In **Select root directory**, browse toohello folder containing sample files.</span></span> <span data-ttu-id="7d85f-152">Selecteer Hallo-map met de map .project Hallo.</span><span class="sxs-lookup"><span data-stu-id="7d85f-152">Select hello folder that contains hello .project folder.</span></span> <span data-ttu-id="7d85f-153">Hallo-project moet worden weergegeven in Hallo **projecten** lijst als een geselecteerd item.</span><span class="sxs-lookup"><span data-stu-id="7d85f-153">hello project should appear in hello **Projects** list as a selected item.</span></span>
   
    ![][12]
3. <span data-ttu-id="7d85f-154">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-154">Click **Finish**.</span></span>
4. <span data-ttu-id="7d85f-155">Gebruik **Projectverkenner** tooview en bewerk Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="7d85f-155">Use **Project Explorer** tooview and edit hello files.</span></span> <span data-ttu-id="7d85f-156">Als deze nog niet is geopend, klikt u op **venster** > **weergave tonen** > **Projectverkenner** of gebruik Hallo snelkoppeling tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="7d85f-156">If it's not already open, click **Window** > **Show View** > **Project Explorer** or use hello shortcut tooopen it.</span></span>

## <a name="configure-hello-service-url-and-api-key"></a><span data-ttu-id="7d85f-157">Hallo-service-URL en api-sleutel configureren</span><span class="sxs-lookup"><span data-stu-id="7d85f-157">Configure hello service URL and api-key</span></span>
1. <span data-ttu-id="7d85f-158">In **Projectverkenner**, dubbelklikt u op **config.properties** tooedit Hallo configuratie-instellingen met de Hallo-servernaam en api-sleutel.</span><span class="sxs-lookup"><span data-stu-id="7d85f-158">In **Project Explorer**, double-click **config.properties** tooedit hello configuration settings containing hello server name and api-key.</span></span>
2. <span data-ttu-id="7d85f-159">Raadpleeg toohello eerdere stappen in dit artikel, waarin u Hallo service-URL en api-sleutel in Hallo gevonden [Azure Portal](https://portal.azure.com), tooget Hallo waarden die u nu moet opgeven in **config.properties**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-159">Refer toohello steps earlier in this article, where you found hello service URL and api-key in hello [Azure Portal](https://portal.azure.com), tooget hello values you will now enter into **config.properties**.</span></span>
3. <span data-ttu-id="7d85f-160">In **config.properties**, vervangen door 'Api Key' hello api-sleutel voor uw service.</span><span class="sxs-lookup"><span data-stu-id="7d85f-160">In **config.properties**, replace "Api Key" with hello api-key for your service.</span></span> <span data-ttu-id="7d85f-161">Vervolgens servicenaam (Hallo eerste onderdeel van Hallo URL http://servicename.search.windows.net) vervangen door 'service name' in hello hetzelfde bestand.</span><span class="sxs-lookup"><span data-stu-id="7d85f-161">Next, service name (hello first component of hello URL http://servicename.search.windows.net) replaces "service name" in hello same file.</span></span>
   
    ![][5]

## <a name="configure-hello-project-build-and-runtime-environments"></a><span data-ttu-id="7d85f-162">Hallo-project, build en runtime-omgeving configureren</span><span class="sxs-lookup"><span data-stu-id="7d85f-162">Configure hello project, build and runtime environments</span></span>
1. <span data-ttu-id="7d85f-163">In Eclipse in Projectverkenner met de rechtermuisknop op Hallo project > **eigenschappen** > **Project-facetten**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-163">In Eclipse, in Project Explorer, right-click hello project > **Properties** > **Project Facets**.</span></span>
2. <span data-ttu-id="7d85f-164">Selecteer **Dynamic Web Module** (Dynamische webmodule), **Java** en **JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-164">Select **Dynamic Web Module**, **Java**, and **JavaScript**.</span></span>
   
    ![][6]
3. <span data-ttu-id="7d85f-165">Klik op **Apply** (Toepassen).</span><span class="sxs-lookup"><span data-stu-id="7d85f-165">Click **Apply**.</span></span>
4. <span data-ttu-id="7d85f-166">Selecteer **Window** (Venster) > **Preferences** (Voorkeuren) > **Server** > **Runtime Environments** (Runtime-omgevingen) > **Add..** (Toevoegen).</span><span class="sxs-lookup"><span data-stu-id="7d85f-166">Select **Window** > **Preferences** > **Server** > **Runtime Environments** > **Add..**.</span></span>
5. <span data-ttu-id="7d85f-167">Vouw Apache uit en selecteer Hallo-versie van Hallo Apache Tomcat-server die u eerder hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d85f-167">Expand Apache and select hello version of hello Apache Tomcat server you previously installed.</span></span> <span data-ttu-id="7d85f-168">Op ons systeem hebben we versie 8 geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d85f-168">On our system, we installed version 8.</span></span>
   
    ![][7]
6. <span data-ttu-id="7d85f-169">Geef op de volgende pagina Hallo Hallo Tomcat-installatiedirectory.</span><span class="sxs-lookup"><span data-stu-id="7d85f-169">On hello next page, specify hello Tomcat installation directory.</span></span> <span data-ttu-id="7d85f-170">Op een Windows-computer is dit waarschijnlijk C:\Program Files\Apache Software Foundation\Tomcat *versie*.</span><span class="sxs-lookup"><span data-stu-id="7d85f-170">On a Windows computer, this will most likely be C:\Program Files\Apache Software Foundation\Tomcat *version*.</span></span>
7. <span data-ttu-id="7d85f-171">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-171">Click **Finish**.</span></span>
8. <span data-ttu-id="7d85f-172">Selecteer **Window** (Venster) > **Preferences** (Voorkeuren) > **Java** > **Installed JREs**(Geïnstalleerde JRE's) > **Add** (Toevoegen).</span><span class="sxs-lookup"><span data-stu-id="7d85f-172">Select **Window** > **Preferences** > **Java** > **Installed JREs** > **Add**.</span></span>
9. <span data-ttu-id="7d85f-173">Selecteer in het venster **Add JRE** (JRE toevoegen) de optie **Standard VM** (Standaard-VM).</span><span class="sxs-lookup"><span data-stu-id="7d85f-173">In **Add JRE**, select **Standard VM**.</span></span>
10. <span data-ttu-id="7d85f-174">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-174">Click **Next**.</span></span>
11. <span data-ttu-id="7d85f-175">Klik in JRE Definition (JRE-definitie), in JRE home (JRE-startpagina), op **Directory**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-175">In JRE Definition, in JRE home, click **Directory**.</span></span>
12. <span data-ttu-id="7d85f-176">Navigeer te**Program Files** > **Java** en selecteer Hallo JDK die u eerder hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7d85f-176">Navigate too**Program Files** > **Java** and select hello JDK you previously installed.</span></span> <span data-ttu-id="7d85f-177">Het is belangrijk tooselect hello JDK als Hallo JRE.</span><span class="sxs-lookup"><span data-stu-id="7d85f-177">It's important tooselect hello JDK as hello JRE.</span></span>
13. <span data-ttu-id="7d85f-178">Kies in de geïnstalleerd JREs hello **JDK**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-178">In Installed JREs, choose hello **JDK**.</span></span> <span data-ttu-id="7d85f-179">Uw instellingen ziet vergelijkbare toohello volgende schermopname.</span><span class="sxs-lookup"><span data-stu-id="7d85f-179">Your settings should look similar toohello following screenshot.</span></span>
    
    ![][9]
14. <span data-ttu-id="7d85f-180">Selecteer desgewenst **venster** > **webbrowser** > **Internet Explorer** tooopen Hallo toepassing in een extern browservenster.</span><span class="sxs-lookup"><span data-stu-id="7d85f-180">Optionally, select **Window** > **Web Browser** > **Internet Explorer** tooopen hello application in an external browser window.</span></span> <span data-ttu-id="7d85f-181">Het gebruik van de externe browser biedt een betere gebruikservaring voor de webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="7d85f-181">Using an external browser gives you a better Web application experience.</span></span>
    
    ![][8]

<span data-ttu-id="7d85f-182">U hebt nu Hallo configuratietaken voltooid.</span><span class="sxs-lookup"><span data-stu-id="7d85f-182">You have now completed hello configuration tasks.</span></span> <span data-ttu-id="7d85f-183">U moet vervolgens bouwen en uitvoeren van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="7d85f-183">Next, you'll build and run hello project.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="7d85f-184">Hallo-project maken</span><span class="sxs-lookup"><span data-stu-id="7d85f-184">Build hello project</span></span>
1. <span data-ttu-id="7d85f-185">In Projectverkenner met de rechtermuisknop op de projectnaam Hallo en kies **uitvoeren als** > **Maven build...**  tooconfigure Hallo project.</span><span class="sxs-lookup"><span data-stu-id="7d85f-185">In Project Explorer, right-click hello project name and choose **Run As** > **Maven build...** tooconfigure hello project.</span></span>
   
    ![][10]
2. <span data-ttu-id="7d85f-186">Ga naar Edit Configuration (Configuratie bewerken), typ bij Goals (Doelen) 'clean install' en klik vervolgens op **Run** (Uitvoeren).</span><span class="sxs-lookup"><span data-stu-id="7d85f-186">In Edit Configuration, in Goals, type "clean install", and then click **Run**.</span></span>

<span data-ttu-id="7d85f-187">Statusberichten die zijn uitvoer toohello-consolevenster.</span><span class="sxs-lookup"><span data-stu-id="7d85f-187">Status messages are output toohello console window.</span></span> <span data-ttu-id="7d85f-188">U ziet BUILD SUCCESS die duiden Hallo project zonder fouten is gebouwd.</span><span class="sxs-lookup"><span data-stu-id="7d85f-188">You should see BUILD SUCCESS indicating hello project built without errors.</span></span>

## <a name="run-hello-app"></a><span data-ttu-id="7d85f-189">Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7d85f-189">Run hello app</span></span>
<span data-ttu-id="7d85f-190">In deze laatste stap wordt u Hallo toepassing uitvoert in een lokale server runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7d85f-190">In this last step, you will run hello application in a local server runtime environment.</span></span>

<span data-ttu-id="7d85f-191">Als u dit nog niet hebt nog geen serverruntime-omgeving in Eclipse opgegeven, moet u dat eerst toodo.</span><span class="sxs-lookup"><span data-stu-id="7d85f-191">If you haven't yet specified a server runtime environment in Eclipse, you'll need toodo that first.</span></span>

1. <span data-ttu-id="7d85f-192">Vouw in Projectverkenner **WebContent** uit.</span><span class="sxs-lookup"><span data-stu-id="7d85f-192">In Project Explorer, expand **WebContent**.</span></span>
2. <span data-ttu-id="7d85f-193">Klik met de rechtermuisknop op **Search.jsp** > **Run As** (Uitvoeren als) > **Run on Server** (Uitvoeren op server).</span><span class="sxs-lookup"><span data-stu-id="7d85f-193">Right-click **Search.jsp** > **Run As** > **Run on Server**.</span></span> <span data-ttu-id="7d85f-194">Selecteer Hallo Apache Tomcat-server en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-194">Select hello Apache Tomcat server, and then click **Run**.</span></span>

> [!TIP]
> <span data-ttu-id="7d85f-195">Als u een niet-standaard werkruimte toostore op uw project gebruikt, moet u toomodify **Run configuratie** toopoint toohello project locatie tooavoid een opstartfout voor de server.</span><span class="sxs-lookup"><span data-stu-id="7d85f-195">If you used a non-default workspace toostore your project, you'll need toomodify **Run Configuration** toopoint toohello project location tooavoid a server start-up error.</span></span> <span data-ttu-id="7d85f-196">Klik in Projectverkenner met de rechtermuisknop op **Search.jsp** > **Uitvoeren als** > **Configuratie uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-196">In Project Explorer, right-click **Search.jsp** > **Run As** > **Run Configurations**.</span></span> <span data-ttu-id="7d85f-197">Selecteer Hallo Apache Tomcat-server.</span><span class="sxs-lookup"><span data-stu-id="7d85f-197">Select hello Apache Tomcat server.</span></span> <span data-ttu-id="7d85f-198">Klik op **Argumenten**.</span><span class="sxs-lookup"><span data-stu-id="7d85f-198">Click **Arguments**.</span></span> <span data-ttu-id="7d85f-199">Klik op **werkruimte** of **bestandssysteem** tooset Hallo map met de Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="7d85f-199">Click **Workspace** or **File System** tooset hello folder containing hello project.</span></span>
> 
> 

<span data-ttu-id="7d85f-200">Wanneer u de toepassing hello uitvoert, ziet u een browservenster biedt een zoekvak waarin u termen.</span><span class="sxs-lookup"><span data-stu-id="7d85f-200">When you run hello application, you should see a browser window, providing a search box for entering terms.</span></span>

<span data-ttu-id="7d85f-201">Wacht ongeveer een minuut voordat u op **Search** toogive Hallo service tijd toocreate en load Hallo index.</span><span class="sxs-lookup"><span data-stu-id="7d85f-201">Wait about one minute before clicking **Search** toogive hello service time toocreate and load hello index.</span></span> <span data-ttu-id="7d85f-202">Als u een HTTP 404-fout krijgt, hoeft u alleen toowait iets langer voordat u opnieuw probeert.</span><span class="sxs-lookup"><span data-stu-id="7d85f-202">If you get an HTTP 404 error, you just need toowait a little bit longer before trying again.</span></span>

## <a name="search-on-usgs-data"></a><span data-ttu-id="7d85f-203">Zoeken in USGS-gegevens</span><span class="sxs-lookup"><span data-stu-id="7d85f-203">Search on USGS data</span></span>
<span data-ttu-id="7d85f-204">Hallo USGS-gegevensset bevat records die relevant toohello staat Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="7d85f-204">hello USGS data set includes records that are relevant toohello state of Rhode Island.</span></span> <span data-ttu-id="7d85f-205">Als u op **Search** op het zoekvak leeg is, ontvangt u een Hallo bovenste 50 vermeldingen, Hallo standaardinstelling.</span><span class="sxs-lookup"><span data-stu-id="7d85f-205">If you click **Search** on an empty search box, you will get hello top 50 entries, which is hello default.</span></span>

<span data-ttu-id="7d85f-206">Een zoekterm invoert, krijgt Hallo zoekmachine iets toogo op.</span><span class="sxs-lookup"><span data-stu-id="7d85f-206">Entering a search term will give hello search engine something toogo on.</span></span> <span data-ttu-id="7d85f-207">Voer een regionale naam in.</span><span class="sxs-lookup"><span data-stu-id="7d85f-207">Try entering a regional name.</span></span> <span data-ttu-id="7d85f-208">'Roger Williams' was Hallo eerste gouverneur van Rhode Island.</span><span class="sxs-lookup"><span data-stu-id="7d85f-208">"Roger Williams" was hello first governor of Rhode Island.</span></span> <span data-ttu-id="7d85f-209">Er zijn verschillende parken, gebouwen en scholen naar hem vernoemd.</span><span class="sxs-lookup"><span data-stu-id="7d85f-209">Numerous parks, buildings, and schools are named after him.</span></span>

![][11]

<span data-ttu-id="7d85f-210">U kunt ook de volgende termen proberen:</span><span class="sxs-lookup"><span data-stu-id="7d85f-210">You could also try any of these terms:</span></span>

* <span data-ttu-id="7d85f-211">Pawtucket</span><span class="sxs-lookup"><span data-stu-id="7d85f-211">Pawtucket</span></span>
* <span data-ttu-id="7d85f-212">Pembroke</span><span class="sxs-lookup"><span data-stu-id="7d85f-212">Pembroke</span></span>
* <span data-ttu-id="7d85f-213">goose +cape</span><span class="sxs-lookup"><span data-stu-id="7d85f-213">goose +cape</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d85f-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7d85f-214">Next steps</span></span>
<span data-ttu-id="7d85f-215">Dit is Hallo eerste Azure Search-zelfstudie op basis van Java en Hallo USGS-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="7d85f-215">This is hello first Azure Search tutorial based on Java and hello USGS dataset.</span></span> <span data-ttu-id="7d85f-216">Na verloop van tijd hebt we deze zelfstudie toodemonstrate aanvullende zoekfuncties kunt u toouse in uw aangepaste oplossingen uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="7d85f-216">Over time, we'll extend this tutorial toodemonstrate additional search features you might want toouse in your custom solutions.</span></span>

<span data-ttu-id="7d85f-217">Als u al enige ervaring in Azure Search hebt, kunt u dit voorbeeld als Springplank voor verdere experimenten, om Hallo [zoekpagina](search-pagination-page-layout.md), of implementeren van een [facetnavigatie](search-faceted-navigation.md).</span><span class="sxs-lookup"><span data-stu-id="7d85f-217">If you already have some background in Azure Search, you can use this sample as a springboard for further experimentation, perhaps augmenting hello [search page](search-pagination-page-layout.md), or implementing [faceted navigation](search-faceted-navigation.md).</span></span> <span data-ttu-id="7d85f-218">U kunt ook op Hallo pagina met zoekresultaten verbeteren door tellers toe te voegen document in batch zodat gebruikers kunnen via Hallo resultaten.</span><span class="sxs-lookup"><span data-stu-id="7d85f-218">You can also improve upon hello search results page by adding counts and batching documents so that users can page through hello results.</span></span>

<span data-ttu-id="7d85f-219">Nieuwe tooAzure zoeken?</span><span class="sxs-lookup"><span data-stu-id="7d85f-219">New tooAzure Search?</span></span> <span data-ttu-id="7d85f-220">Het is raadzaam om bij andere zelfstudies toodevelop een goed begrip van kunt maken.</span><span class="sxs-lookup"><span data-stu-id="7d85f-220">We recommend trying other tutorials toodevelop an understanding of what you can create.</span></span> <span data-ttu-id="7d85f-221">Ga naar onze [documentatiepagina](https://azure.microsoft.com/documentation/services/search/) toofind meer bronnen.</span><span class="sxs-lookup"><span data-stu-id="7d85f-221">Visit our [documentation page](https://azure.microsoft.com/documentation/services/search/) toofind more resources.</span></span> <span data-ttu-id="7d85f-222">U kunt ook weergeven Hallo koppelingen in onze [Video's en zelfstudies lijst](search-video-demo-tutorial-list.md) tooaccess meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7d85f-222">You can also view hello links in our [Video and Tutorial list](search-video-demo-tutorial-list.md) tooaccess more information.</span></span>

<!--Image references-->
[1]: ./media/search-get-started-java/create-search-portal-1.PNG
[2]: ./media/search-get-started-java/create-search-portal-21.PNG
[3]: ./media/search-get-started-java/create-search-portal-31.PNG
[4]: ./media/search-get-started-java/AzSearch-Java-Import1.PNG
[5]: ./media/search-get-started-java/AzSearch-Java-config1.PNG
[6]: ./media/search-get-started-java/AzSearch-Java-ProjectFacets1.PNG
[7]: ./media/search-get-started-java/AzSearch-Java-runtime1.PNG
[8]: ./media/search-get-started-java/AzSearch-Java-Browser1.PNG
[9]: ./media/search-get-started-java/AzSearch-Java-JREPref1.PNG
[10]: ./media/search-get-started-java/AzSearch-Java-BuildProject1.PNG
[11]: ./media/search-get-started-java/rogerwilliamsschool1.PNG
[12]: ./media/search-get-started-java/AzSearch-Java-SelectProject.png

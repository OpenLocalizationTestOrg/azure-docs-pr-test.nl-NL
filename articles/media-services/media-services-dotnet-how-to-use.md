---
title: aaaHow tooSet Computer voor het ontwikkelen van Media Services met .NET
description: Meer informatie over het Hallo-vereisten voor Media Services met Hallo Media Services SDK voor .NET. Ook meer te weten hoe toocreate een Visual Studio-app.
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/23/2017
ms.author: juliako
ms.openlocfilehash: a5a2af3211d8156fd7dea99831fb769df4130d41
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="80f26-104">Het ontwikkelen van Media Services met .NET</span><span class="sxs-lookup"><span data-stu-id="80f26-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="80f26-105">Dit onderwerp wordt beschreven hoe toostart ontwikkelen Media Services-toepassingen met behulp van .NET.</span><span class="sxs-lookup"><span data-stu-id="80f26-105">This topic discusses how toostart developing Media Services applications using .NET.</span></span>

<span data-ttu-id="80f26-106">Hallo **Azure Media Services .NET SDK** bibliotheek kunt u tooprogram op basis van Media Services met .NET.</span><span class="sxs-lookup"><span data-stu-id="80f26-106">hello **Azure Media Services .NET SDK** library enables you tooprogram against Media Services using .NET.</span></span> <span data-ttu-id="80f26-107">deze zelfs eenvoudiger toodevelop met .NET, hello toomake **Azure Media Services .NET SDK Extensions** bibliotheek is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="80f26-107">toomake it even easier toodevelop with .NET, hello **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="80f26-108">Deze bibliotheek bevat een set uitbreidingsmethoden en Help-functies die uw .NET-code vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="80f26-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="80f26-109">Beide bibliotheken zijn beschikbaar via **NuGet** en **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="80f26-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80f26-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="80f26-110">Prerequisites</span></span>
* <span data-ttu-id="80f26-111">Een Media Services-account in een nieuw of bestaand Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="80f26-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="80f26-112">Zie onderwerp Hallo [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="80f26-112">See hello topic [How tooCreate a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="80f26-113">Besturingssystemen: Windows 10, Windows 7, Windows 2008 R2 of Windows 8.</span><span class="sxs-lookup"><span data-stu-id="80f26-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="80f26-114">.NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="80f26-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="80f26-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="80f26-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="80f26-116">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="80f26-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="80f26-117">Deze sectie leest u hoe een project in Visual Studio toocreate en instellen voor het ontwikkelen van Media Services.</span><span class="sxs-lookup"><span data-stu-id="80f26-117">This section shows you how toocreate a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="80f26-118">In dit geval Hallo project is een Windows C#-consoletoepassing, maar hello dezelfde instellingsstappen hier weergegeven tooother typen toepassen van de projecten die u voor Media Services-toepassingen (bijvoorbeeld een Windows Forms-toepassing of een ASP.NET-webtoepassing maken kunt).</span><span class="sxs-lookup"><span data-stu-id="80f26-118">In this case, hello project is a C# Windows console application, but hello same setup steps shown here apply tooother types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="80f26-119">Deze sectie wordt beschreven hoe toouse **NuGet** tooadd Media Services .NET SDK extensions en andere afhankelijke bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="80f26-119">This section shows how toouse **NuGet** tooadd Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="80f26-120">U kunt ook de meest recente Media Services .NET SDK bits Hallo ophalen vanuit GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) of [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), Hallo oplossing bouwen en Hallo verwijzingen toohello clientproject toevoegen.</span><span class="sxs-lookup"><span data-stu-id="80f26-120">Alternatively, you can get hello latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build hello solution, and add hello references toohello client project.</span></span> <span data-ttu-id="80f26-121">Alle benodigde Hallo-afhankelijkheden ophalen gedownload en uitgepakt automatisch.</span><span class="sxs-lookup"><span data-stu-id="80f26-121">All hello necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="80f26-122">Maak in Visual Studio een nieuwe C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="80f26-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="80f26-123">Voer Hallo **naam**, **locatie**, en **oplossingsnaam**, en klik op OK.</span><span class="sxs-lookup"><span data-stu-id="80f26-123">Enter hello **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="80f26-124">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="80f26-124">Build hello solution.</span></span>
3. <span data-ttu-id="80f26-125">Gebruik **NuGet** tooinstall en voeg **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="80f26-125">Use **NuGet** tooinstall and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="80f26-126">Als u dit pakket installeert, wordt ook de **Media Services .NET SDK** geïnstalleerd en worden alle andere vereiste afhankelijkheden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="80f26-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="80f26-127">Zorg ervoor dat u de nieuwste versie Hallo van NuGet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="80f26-127">Ensure that you have hello newest version of NuGet installed.</span></span> <span data-ttu-id="80f26-128">Zie voor meer informatie en installatie-instructies, [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="80f26-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="80f26-129">Klik in Solution Explorer met de rechtermuisknop op Hallo van Hallo-project en kies beheren NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="80f26-129">In Solution Explorer, right-click hello name of hello project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="80f26-130">Hallo NuGet-pakketten beheren dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80f26-130">hello Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="80f26-131">In Hallo Online galerie, zoeken naar Azure MediaServices Extensions Azure Media Services .NET SDK Extensions kiezen en klik op de knop installeren Hallo.</span><span class="sxs-lookup"><span data-stu-id="80f26-131">In hello Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click hello Install button.</span></span>
   
    <span data-ttu-id="80f26-132">Hallo-project is gewijzigd en verwijst naar toohello Media Services .NET SDK Extensions, Media Services .NET SDK en andere afhankelijke assembly's worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="80f26-132">hello project is modified and references toohello Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="80f26-133">een ontwikkelingsomgeving schonere toopromote Overweeg NuGet-pakket herstellen inschakelen.</span><span class="sxs-lookup"><span data-stu-id="80f26-133">toopromote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="80f26-134">Zie voor meer informatie [NuGet-pakket herstellen '](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="80f26-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="80f26-135">Voeg een verwijzing te**System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="80f26-135">Add a reference too**System.Configuration** assembly.</span></span> <span data-ttu-id="80f26-136">Deze assembly bevat Hallo System.Configuration. **ConfigurationManager** gebruikte tooaccess configuratiebestanden (bijvoorbeeld App.config) van die klasse.</span><span class="sxs-lookup"><span data-stu-id="80f26-136">This assembly contains hello System.Configuration.**ConfigurationManager** class that is used tooaccess configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="80f26-137">tooadd verwijzingen met dialoogvenster Hallo verwijzingen beheren, met de rechtermuisknop op Hallo projectnaam in Solution Explorer Hallo.</span><span class="sxs-lookup"><span data-stu-id="80f26-137">tooadd references using hello Manage References dialog, right-click hello project name in hello Solution Explorer.</span></span> <span data-ttu-id="80f26-138">Selecteer toevoegen en verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="80f26-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="80f26-139">Hallo beheren verwijst naar het dialoogvenster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="80f26-139">hello Manage References dialog appears.</span></span>
8. <span data-ttu-id="80f26-140">Onder de .NET framework-assembly's vinden en selecteer Hallo System.Configuration-assembly en druk op OK.</span><span class="sxs-lookup"><span data-stu-id="80f26-140">Under .NET framework assemblies, find and select hello System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="80f26-141">Open Hallo App.config-bestand en voeg een *appSettings* sectie toohello bestand.</span><span class="sxs-lookup"><span data-stu-id="80f26-141">Open hello App.config file and add an *appSettings* section toohello file.</span></span>     
   
    <span data-ttu-id="80f26-142">Stel Hallo-waarden die vereist tooconnect toohello Media Services-API zijn.</span><span class="sxs-lookup"><span data-stu-id="80f26-142">Set hello values that are needed tooconnect toohello Media Services API.</span></span> <span data-ttu-id="80f26-143">Zie voor meer informatie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="80f26-143">For more information, see [Access hello Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="80f26-144">Als u [gebruikersverificatie](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) uw configuratiebestand wordt waarschijnlijk waarden voor uw Azure AD-tenant-domein en Hallo AMS REST API-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="80f26-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and hello AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="80f26-145">De meeste codevoorbeelden in hello Azure Media Services-documentatie instellen, gebruikt u een gebruiker (interactief) soort verificatie tooconnect toohello AMS API.</span><span class="sxs-lookup"><span data-stu-id="80f26-145">Most code samples in hello Azure Media Services documentation set, use a user (interactive) type of authentication tooconnect toohello AMS API.</span></span> <span data-ttu-id="80f26-146">Deze verificatiemethode werkt goed voor beheer- of systeemeigen apps bewaking: mobiele apps, Windows-apps en toepassingen van de Console.</span><span class="sxs-lookup"><span data-stu-id="80f26-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="80f26-147">Deze verificatiemethode is niet geschikt voor de server, webservices of type API's van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="80f26-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="80f26-148">Zie voor meer informatie [toegang Hallo AMS API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="80f26-148">For more information, see [Access hello AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="80f26-149">Overschrijf Hallo bestaande **met** instructies aan Hallo begin van Hallo bestand Program.cs Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="80f26-149">Overwrite hello existing **using** statements at hello beginning of hello Program.cs file with hello following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="80f26-150">U bent nu klaar toostart ontwikkelen van een Media Services-toepassing.</span><span class="sxs-lookup"><span data-stu-id="80f26-150">At this point, you are ready toostart developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="80f26-151">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="80f26-151">Example</span></span>

<span data-ttu-id="80f26-152">Hier volgt een voorbeeld van een kleine die is verbonden toohello AMS API en een lijst met alle beschikbare Media-Processors.</span><span class="sxs-lookup"><span data-stu-id="80f26-152">Here is a small example that connects toohello AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from hello App.config file.
        private static readonly string _AADTenantDomain =
            ConfigurationManager.AppSettings["AADTenantDomain"];
        private static readonly string _RESTAPIEndpoint =
            ConfigurationManager.AppSettings["MediaServiceRESTAPIEndpoint"];
    
        private static CloudMediaContext _context = null;
        static void Main(string[] args)
        {
            var tokenCredentials = new AzureAdTokenCredentials(_AADTenantDomain, AzureEnvironments.AzureCloudEnvironment);
            var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
            _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
    
            // List all available Media Processors
            foreach (var mp in _context.MediaProcessors)
            {
                Console.WriteLine(mp.Name);
            }
    
        }

##<a name="next-steps"></a><span data-ttu-id="80f26-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="80f26-153">Next steps</span></span>

<span data-ttu-id="80f26-154">Nu [toohello AMS API kunt u](media-services-use-aad-auth-to-access-ams-api.md) en start [ontwikkelen](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="80f26-154">Now [you can connect toohello AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="80f26-155">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="80f26-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="80f26-156">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="80f26-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


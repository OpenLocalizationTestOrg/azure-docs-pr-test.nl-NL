---
title: Computer instellen voor het ontwikkelen van Media Services met .NET
description: Meer informatie over de vereisten voor Media Services met behulp van de Media Services SDK voor .NET. Ook informatie over het maken van een Visual Studio-app.
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
ms.openlocfilehash: 15828bc74937a036871b26493498232ec7cf6f06
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="e603f-104">Het ontwikkelen van Media Services met .NET</span><span class="sxs-lookup"><span data-stu-id="e603f-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="e603f-105">In dit onderwerp wordt beschreven hoe beginnen met het ontwikkelen van Media Services-toepassingen met behulp van .NET.</span><span class="sxs-lookup"><span data-stu-id="e603f-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="e603f-106">De **Azure Media Services .NET SDK** bibliotheek kunt u voor het programmeren in Media Services met .NET.</span><span class="sxs-lookup"><span data-stu-id="e603f-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="e603f-107">Zelfs gemakkelijker te ontwikkelen met .NET, de **Azure Media Services .NET SDK Extensions** bibliotheek is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e603f-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="e603f-108">Deze bibliotheek bevat een set uitbreidingsmethoden en Help-functies die uw .NET-code vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="e603f-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="e603f-109">Beide bibliotheken zijn beschikbaar via **NuGet** en **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="e603f-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e603f-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e603f-110">Prerequisites</span></span>
* <span data-ttu-id="e603f-111">Een Media Services-account in een nieuw of bestaand Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e603f-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="e603f-112">Zie het onderwerp [Een Media Services-account maken](media-services-portal-create-account.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e603f-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="e603f-113">Besturingssystemen: Windows 10, Windows 7, Windows 2008 R2 of Windows 8.</span><span class="sxs-lookup"><span data-stu-id="e603f-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="e603f-114">.NET framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e603f-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="e603f-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e603f-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="e603f-116">Maak en configureer een Visual Studio-project.</span><span class="sxs-lookup"><span data-stu-id="e603f-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="e603f-117">Deze sectie wordt beschreven hoe u een project in Visual Studio maken en instellen voor het ontwikkelen van Media Services.</span><span class="sxs-lookup"><span data-stu-id="e603f-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="e603f-118">In dit geval wordt het project is een Windows C#-consoletoepassing, maar dezelfde installatiestappen hier weergegeven gelden voor andere soorten projecten die u voor Media Services-toepassingen (bijvoorbeeld een Windows Forms-toepassing of een ASP.NET-webtoepassing maken kunt).</span><span class="sxs-lookup"><span data-stu-id="e603f-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="e603f-119">Deze sectie wordt beschreven hoe u **NuGet** Media Services .NET SDK extensions en andere afhankelijke bibliotheken toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="e603f-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="e603f-120">U kunt ook de meest recente Media Services .NET SDK bits ophalen vanuit GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) of [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), de oplossing bouwen en de verwijzingen naar de client-project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="e603f-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="e603f-121">De vereiste afhankelijkheden ophalen gedownload en uitgepakt automatisch.</span><span class="sxs-lookup"><span data-stu-id="e603f-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="e603f-122">Maak in Visual Studio een nieuwe C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="e603f-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="e603f-123">Voer de **naam**, **locatie**, en **oplossingsnaam**, en klik op OK.</span><span class="sxs-lookup"><span data-stu-id="e603f-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="e603f-124">De oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="e603f-124">Build the solution.</span></span>
3. <span data-ttu-id="e603f-125">Gebruik **NuGet** installeren en toevoegen **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="e603f-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="e603f-126">Als u dit pakket installeert, wordt ook de **Media Services .NET SDK** geïnstalleerd en worden alle andere vereiste afhankelijkheden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e603f-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="e603f-127">Zorg ervoor dat u de nieuwste versie van NuGet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="e603f-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="e603f-128">Zie voor meer informatie en installatie-instructies, [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="e603f-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="e603f-129">Klik in Solution Explorer met de rechtermuisknop op de naam van het project en kies beheren NuGet-pakketten.</span><span class="sxs-lookup"><span data-stu-id="e603f-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="e603f-130">Het dialoogvenster NuGet-pakketten beheren wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e603f-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="e603f-131">In de galerie met Online zoeken naar Azure MediaServices Extensions, kiest u Azure Media Services .NET SDK Extensions en klik vervolgens op de knop installeren.</span><span class="sxs-lookup"><span data-stu-id="e603f-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="e603f-132">Het project is gewijzigd en verwijzingen naar de Media Services .NET SDK Extensions, Media Services .NET SDK en andere afhankelijke assembly's worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e603f-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="e603f-133">Als u een schonere ontwikkelomgeving verhogen, kunt u inschakelen NuGet-pakket herstellen.</span><span class="sxs-lookup"><span data-stu-id="e603f-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="e603f-134">Zie voor meer informatie [NuGet-pakket herstellen '](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="e603f-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="e603f-135">Voeg een verwijzing naar **System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="e603f-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="e603f-136">Deze assembly bevat de System.Configuration. **ConfigurationManager** klasse die wordt gebruikt voor toegang tot de configuratiebestanden (bijvoorbeeld App.config).</span><span class="sxs-lookup"><span data-stu-id="e603f-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="e603f-137">Om verwijzingen te voegen met het dialoogvenster referenties beheren, met de rechtermuisknop op de projectnaam in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="e603f-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="e603f-138">Selecteer toevoegen en verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="e603f-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="e603f-139">Het dialoogvenster referenties beheren wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e603f-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="e603f-140">Onder de .NET framework-assembly's vinden en selecteer de System.Configuration-assembly en druk op OK.</span><span class="sxs-lookup"><span data-stu-id="e603f-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="e603f-141">Open het bestand App.config en voeg een *appSettings* sectie naar het bestand.</span><span class="sxs-lookup"><span data-stu-id="e603f-141">Open the App.config file and add an *appSettings* section to the file.</span></span>     
   
    <span data-ttu-id="e603f-142">Stel de waarden die nodig zijn voor het verbinding maken met het Media Services-API.</span><span class="sxs-lookup"><span data-stu-id="e603f-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="e603f-143">Zie voor meer informatie [toegang tot de API van Azure Media Services met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e603f-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="e603f-144">Als u [gebruikersverificatie](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) uw configuratiebestand hebt waarschijnlijk waarden voor uw Azure AD-tenant-domein en de AMS REST API-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="e603f-144">If you are using [user authentication](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) your config file will probably have values for your Azure AD tenant domain and the AMS REST API endpoint.</span></span>
    
    >[!Important]
    ><span data-ttu-id="e603f-145">De meeste codevoorbeelden in de documentatie van Azure Media Services instellen, gebruikt u een gebruiker (interactief) type verificatie verbinding maken met de AMS-API.</span><span class="sxs-lookup"><span data-stu-id="e603f-145">Most code samples in the Azure Media Services documentation set, use a user (interactive) type of authentication to connect to the AMS API.</span></span> <span data-ttu-id="e603f-146">Deze verificatiemethode werkt goed voor beheer- of systeemeigen apps bewaking: mobiele apps, Windows-apps en toepassingen van de Console.</span><span class="sxs-lookup"><span data-stu-id="e603f-146">This authentication method will work well for management or monitoring native apps: mobile apps, Windows apps, and Console applications.</span></span> <span data-ttu-id="e603f-147">Deze verificatiemethode is niet geschikt voor de server, webservices of type API's van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e603f-147">This authentication method is not suitable for server, web services, APIs type of applications.</span></span>  <span data-ttu-id="e603f-148">Zie voor meer informatie [toegang tot de AMS-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="e603f-148">For more information, see [Access the AMS API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. <span data-ttu-id="e603f-149">Overschrijf de bestaande instructies aan het begin van het bestand Program.cs **met** de volgende code.</span><span class="sxs-lookup"><span data-stu-id="e603f-149">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

<span data-ttu-id="e603f-150">U bent nu klaar om te beginnen met het ontwikkelen van een Media Services-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e603f-150">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="e603f-151">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e603f-151">Example</span></span>

<span data-ttu-id="e603f-152">Hier volgt een voorbeeld van een kleine die verbinding maakt met de AMS-API en een lijst met alle beschikbare Media-Processors.</span><span class="sxs-lookup"><span data-stu-id="e603f-152">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>
    
    class Program
    {
        // Read values from the App.config file.
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

##<a name="next-steps"></a><span data-ttu-id="e603f-153">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e603f-153">Next steps</span></span>

<span data-ttu-id="e603f-154">Nu [u kunt verbinding maken met de AMS API](media-services-use-aad-auth-to-access-ams-api.md) en start [ontwikkelen](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e603f-154">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="e603f-155">Media Services-leertrajecten</span><span class="sxs-lookup"><span data-stu-id="e603f-155">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="e603f-156">Feedback geven</span><span class="sxs-lookup"><span data-stu-id="e603f-156">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


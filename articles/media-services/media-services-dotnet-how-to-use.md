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
# <a name="media-services-development-with-net"></a>Het ontwikkelen van Media Services met .NET
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

Dit onderwerp wordt beschreven hoe toostart ontwikkelen Media Services-toepassingen met behulp van .NET.

Hallo **Azure Media Services .NET SDK** bibliotheek kunt u tooprogram op basis van Media Services met .NET. deze zelfs eenvoudiger toodevelop met .NET, hello toomake **Azure Media Services .NET SDK Extensions** bibliotheek is opgegeven. Deze bibliotheek bevat een set uitbreidingsmethoden en Help-functies die uw .NET-code vereenvoudigen. Beide bibliotheken zijn beschikbaar via **NuGet** en **GitHub**.

## <a name="prerequisites"></a>Vereisten
* Een Media Services-account in een nieuw of bestaand Azure-abonnement. Zie onderwerp Hallo [hoe tooCreate een Media Services-Account](media-services-portal-create-account.md).
* Besturingssystemen: Windows 10, Windows 7, Windows 2008 R2 of Windows 8.
* .NET framework 4.5.
* Visual Studio.

## <a name="create-and-configure-a-visual-studio-project"></a>Maak en configureer een Visual Studio-project.
Deze sectie leest u hoe een project in Visual Studio toocreate en instellen voor het ontwikkelen van Media Services.  In dit geval Hallo project is een Windows C#-consoletoepassing, maar hello dezelfde instellingsstappen hier weergegeven tooother typen toepassen van de projecten die u voor Media Services-toepassingen (bijvoorbeeld een Windows Forms-toepassing of een ASP.NET-webtoepassing maken kunt).

Deze sectie wordt beschreven hoe toouse **NuGet** tooadd Media Services .NET SDK extensions en andere afhankelijke bibliotheken.

U kunt ook de meest recente Media Services .NET SDK bits Hallo ophalen vanuit GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) of [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), Hallo oplossing bouwen en Hallo verwijzingen toohello clientproject toevoegen. Alle benodigde Hallo-afhankelijkheden ophalen gedownload en uitgepakt automatisch.

1. Maak in Visual Studio een nieuwe C#-consoletoepassing. Voer Hallo **naam**, **locatie**, en **oplossingsnaam**, en klik op OK.
2. Hallo-oplossing bouwen.
3. Gebruik **NuGet** tooinstall en voeg **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**). Als u dit pakket installeert, wordt ook de **Media Services .NET SDK** geïnstalleerd en worden alle andere vereiste afhankelijkheden toegevoegd.
   
    Zorg ervoor dat u de nieuwste versie Hallo van NuGet geïnstalleerd. Zie voor meer informatie en installatie-instructies, [NuGet](http://nuget.codeplex.com/).
4. Klik in Solution Explorer met de rechtermuisknop op Hallo van Hallo-project en kies beheren NuGet-pakketten.
   
    Hallo NuGet-pakketten beheren dialoogvenster wordt weergegeven.
5. In Hallo Online galerie, zoeken naar Azure MediaServices Extensions Azure Media Services .NET SDK Extensions kiezen en klik op de knop installeren Hallo.
   
    Hallo-project is gewijzigd en verwijst naar toohello Media Services .NET SDK Extensions, Media Services .NET SDK en andere afhankelijke assembly's worden toegevoegd.
6. een ontwikkelingsomgeving schonere toopromote Overweeg NuGet-pakket herstellen inschakelen. Zie voor meer informatie [NuGet-pakket herstellen '](http://docs.nuget.org/consume/package-restore).
7. Voeg een verwijzing te**System.Configuration** assembly. Deze assembly bevat Hallo System.Configuration. **ConfigurationManager** gebruikte tooaccess configuratiebestanden (bijvoorbeeld App.config) van die klasse.
   
    tooadd verwijzingen met dialoogvenster Hallo verwijzingen beheren, met de rechtermuisknop op Hallo projectnaam in Solution Explorer Hallo. Selecteer toevoegen en verwijzingen.
   
    Hallo beheren verwijst naar het dialoogvenster wordt weergegeven.
8. Onder de .NET framework-assembly's vinden en selecteer Hallo System.Configuration-assembly en druk op OK.
9. Open Hallo App.config-bestand en voeg een *appSettings* sectie toohello bestand.     
   
    Stel Hallo-waarden die vereist tooconnect toohello Media Services-API zijn. Zie voor meer informatie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md). 

    Als u [gebruikersverificatie](media-services-use-aad-auth-to-access-ams-api.md#types-of-authentication) uw configuratiebestand wordt waarschijnlijk waarden voor uw Azure AD-tenant-domein en Hallo AMS REST API-eindpunt.
    
    >[!Important]
    >De meeste codevoorbeelden in hello Azure Media Services-documentatie instellen, gebruikt u een gebruiker (interactief) soort verificatie tooconnect toohello AMS API. Deze verificatiemethode werkt goed voor beheer- of systeemeigen apps bewaking: mobiele apps, Windows-apps en toepassingen van de Console. Deze verificatiemethode is niet geschikt voor de server, webservices of type API's van toepassingen.  Zie voor meer informatie [toegang Hallo AMS API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).

        <configuration>
        ...
            <appSettings>
              <add key="AADTenantDomain" value="YourAADTenantDomain" />
              <add key="MediaServiceRESTAPIEndpoint" value="YourRESTAPIEndpoint" />
            </appSettings>

        </configuration>

10. Overschrijf Hallo bestaande **met** instructies aan Hallo begin van Hallo bestand Program.cs Hallo code te volgen.
           
        using System;
        using System.Configuration;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;
        using System.Threading;
        using System.Collections.Generic;
        using System.Linq;

U bent nu klaar toostart ontwikkelen van een Media Services-toepassing.    

## <a name="example"></a>Voorbeeld

Hier volgt een voorbeeld van een kleine die is verbonden toohello AMS API en een lijst met alle beschikbare Media-Processors.
    
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

##<a name="next-steps"></a>Volgende stappen

Nu [toohello AMS API kunt u](media-services-use-aad-auth-to-access-ams-api.md) en start [ontwikkelen](media-services-dotnet-get-started.md).


## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


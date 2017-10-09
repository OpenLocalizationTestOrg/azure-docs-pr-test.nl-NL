---
title: aaaUsing .NET SDK tooaccess Azure Mobile Engagement Service API 's
description: Hierin wordt beschreven hoe toouse Hallo Mobile Engagement .NET SDK tooaccess Azure Mobile Engagement Service API 's
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: c07728aa-43f2-4238-8b4a-c9eddf9d838b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 812be6f507b29f7b2de6454e06face8082c2d161
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a>Met behulp van de .NET SDK tooaccess Azure Mobile Engagement Service API 's
Azure Mobile Engagement beschikt over een set API's voor u toomanage apparaten campagnes Reach/te pushen toointeract enz. met deze API's, wij bieden u ook een [Swagger-bestand](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) die u met gebruiken kunt hulpprogramma's voor toogenerate-SDK's voor de gewenste taal. Aangeraden wordt Hallo [AutoRest](https://github.com/Azure/AutoRest) hulpprogramma toogenerate uw SDK uit onze Swagger-bestand.

> [!NOTE]
> Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten. Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.

We hebben een .NET SDK gemaakt op een vergelijkbare manier waarmee u kunt toointeract met deze API's met behulp van een C#-wrapper en u hebt geen toodo Hallo verificatie token onderhandeling en uzelf te vernieuwen.  

Dit voorbeeld doorloopt NTDS Hallo reeks stappen toofollow toouse Hallo .NET SDK:

1. Ten eerste moet u toosetup Hallo verificatie voor uw API's met behulp van Azure Active Directory Hallo zoals beschreven [hier](mobile-engagement-api-authentication.md#authentication). Hallo na deze stappen u moet beschikken over een geldige **SubscriptionId**, **TenantId**, **ApplicationId** en **geheim**. 
2. We gebruiken een eenvoudige Windows-Console-app toodemonstrate werken met .NET SDK Hallo met Hallo scenario voor het maken van een campagne aankondiging. Dus opent u Visual Studio en maak een **consoletoepassing**.   
3. Vervolgens dient u toodownload Hallo .NET SDK die beschikbaar is als **Management-bibliotheek van Microsoft Azure Engagement** in Nuget-galerie Hallo [hier](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).
   Als u Hallo Nuget vanuit Visual Studio installeert, moet u dat u ingeschakeld Hallo hebt tooensure **Include prerelease** optie bij het zoeken naar Hallo pakket:
   
    ![][1]
4. In Hallo `Program.cs` bestand, het toevoegen van Hallo volgende naamruimten:
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. Vervolgens moet u toodefine Hallo volgende constanten die zullen worden gebruikt voor verificatie en interactie met Hallo Mobile Engagement-App die u in Hallo aankondiging campagne maakt:
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is hello Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using hello one as specified in hello Azure portal (NOT hello App Name)
        const string APP_RESOURCE_NAME = "";
6. Hallo definiëren `EngagementManagementClient` variabele die we gebruiken toocall Hallo Mobile Engagement SDK methoden:
   
        static EngagementManagementClient engagementClient; 
7. Hallo na tooyour toevoegen `Main` methode:
   
        try
            {
                // Initialize hello Engagement SDK toocall out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. Na de methode op die zorgt voor het initialiseren van Hallo Hallo definiëren `EngagementManagementClient` door eerst te verifiëren en zichzelf vervolgens te koppelen met Hallo Mobile Engagement-App waarin u toocreate Hallo aankondiging campagne plannen:
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is hello Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create hello campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > U moet toouse hello **App resourcenaam** zoals gedefinieerd in hello Azure-beheerportal voor Hallo AppName parameter. 
   > 
   > 
9. Ten slotte definiëren Hallo CreateCampaign methode op die zorgt voor het eerder is geïnitialiseerd Hallo EngagementClient toocreate een eenvoudige **op elk gewenst moment** & **melding alleen-lezen** campagne met een titel en het bericht: 
   
        private async static Task CreateCampaign()
        {
            //  Refer toohello Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all hello non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing hello app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer toohello Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. Voer Hallo console-app en u wordt ziet Hallo Hallo campagne gemaakt:
    
    **Campagne-Id '159' is gemaakt en de status 'Concept'**

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png

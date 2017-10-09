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
# <a name="using-net-sdk-tooaccess-azure-mobile-engagement-service-apis"></a><span data-ttu-id="4c0da-103">Met behulp van de .NET SDK tooaccess Azure Mobile Engagement Service API 's</span><span class="sxs-lookup"><span data-stu-id="4c0da-103">Using .NET SDK tooaccess Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="4c0da-104">Azure Mobile Engagement beschikt over een set API's voor u toomanage apparaten campagnes Reach/te pushen toointeract enz. met deze API's, wij bieden u ook een [Swagger-bestand](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) die u met gebruiken kunt hulpprogramma's voor toogenerate-SDK's voor de gewenste taal.</span><span class="sxs-lookup"><span data-stu-id="4c0da-104">Azure Mobile Engagement exposes a set of APIs for you toomanage Devices, Reach/Push campaigns etc. toointeract with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools toogenerate SDKs for your preferred language.</span></span> <span data-ttu-id="4c0da-105">Aangeraden wordt Hallo [AutoRest](https://github.com/Azure/AutoRest) hulpprogramma toogenerate uw SDK uit onze Swagger-bestand.</span><span class="sxs-lookup"><span data-stu-id="4c0da-105">We recommend using hello [AutoRest](https://github.com/Azure/AutoRest) tool toogenerate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="4c0da-106">Hallo Azure Mobile Engagement service buiten gebruik gesteld maart 2018 en is momenteel alleen beschikbaar tooexisting klanten.</span><span class="sxs-lookup"><span data-stu-id="4c0da-106">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="4c0da-107">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4c0da-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="4c0da-108">We hebben een .NET SDK gemaakt op een vergelijkbare manier waarmee u kunt toointeract met deze API's met behulp van een C#-wrapper en u hebt geen toodo Hallo verificatie token onderhandeling en uzelf te vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="4c0da-108">We have created a .NET SDK in a similar manner which allows you toointeract with these APIs using a C# wrapper and you don't have toodo hello authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="4c0da-109">Dit voorbeeld doorloopt NTDS Hallo reeks stappen toofollow toouse Hallo .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="4c0da-109">This sample goes through hello set of steps toofollow toouse hello .NET SDK:</span></span>

1. <span data-ttu-id="4c0da-110">Ten eerste moet u toosetup Hallo verificatie voor uw API's met behulp van Azure Active Directory Hallo zoals beschreven [hier](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="4c0da-110">First of all, you need toosetup hello authentication for your APIs using hello Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="4c0da-111">Hallo na deze stappen u moet beschikken over een geldige **SubscriptionId**, **TenantId**, **ApplicationId** en **geheim**.</span><span class="sxs-lookup"><span data-stu-id="4c0da-111">At hello end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="4c0da-112">We gebruiken een eenvoudige Windows-Console-app toodemonstrate werken met .NET SDK Hallo met Hallo scenario voor het maken van een campagne aankondiging.</span><span class="sxs-lookup"><span data-stu-id="4c0da-112">We will use a simple Windows Console app toodemonstrate working with hello .NET SDK with hello scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="4c0da-113">Dus opent u Visual Studio en maak een **consoletoepassing**.</span><span class="sxs-lookup"><span data-stu-id="4c0da-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="4c0da-114">Vervolgens dient u toodownload Hallo .NET SDK die beschikbaar is als **Management-bibliotheek van Microsoft Azure Engagement** in Nuget-galerie Hallo [hier](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="4c0da-114">Next you need toodownload hello .NET SDK which is available as **Microsoft Azure Engagement Management Library** in hello Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="4c0da-115">Als u Hallo Nuget vanuit Visual Studio installeert, moet u dat u ingeschakeld Hallo hebt tooensure **Include prerelease** optie bij het zoeken naar Hallo pakket:</span><span class="sxs-lookup"><span data-stu-id="4c0da-115">If you are installing hello Nuget from Visual Studio, you need tooensure that you have check marked hello **Include prerelease** option while searching for hello package:</span></span>
   
    ![][1]
4. <span data-ttu-id="4c0da-116">In Hallo `Program.cs` bestand, het toevoegen van Hallo volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="4c0da-116">In hello `Program.cs` file, add hello following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="4c0da-117">Vervolgens moet u toodefine Hallo volgende constanten die zullen worden gebruikt voor verificatie en interactie met Hallo Mobile Engagement-App die u in Hallo aankondiging campagne maakt:</span><span class="sxs-lookup"><span data-stu-id="4c0da-117">Next you need toodefine hello following constants that we will use for authentication and interacting with hello Mobile Engagement App in which you are creating hello Announcement campaign:</span></span>
   
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
6. <span data-ttu-id="4c0da-118">Hallo definiëren `EngagementManagementClient` variabele die we gebruiken toocall Hallo Mobile Engagement SDK methoden:</span><span class="sxs-lookup"><span data-stu-id="4c0da-118">Define hello `EngagementManagementClient` variable which we will use toocall hello Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="4c0da-119">Hallo na tooyour toevoegen `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="4c0da-119">Add hello following tooyour `Main` method:</span></span>
   
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
8. <span data-ttu-id="4c0da-120">Na de methode op die zorgt voor het initialiseren van Hallo Hallo definiëren `EngagementManagementClient` door eerst te verifiëren en zichzelf vervolgens te koppelen met Hallo Mobile Engagement-App waarin u toocreate Hallo aankondiging campagne plannen:</span><span class="sxs-lookup"><span data-stu-id="4c0da-120">Define hello following method which takes care of initializing hello `EngagementManagementClient` by first authenticating and then associating itself with hello Mobile Engagement App in which you plan toocreate hello Announcement campaign:</span></span>
   
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
   > <span data-ttu-id="4c0da-121">U moet toouse hello **App resourcenaam** zoals gedefinieerd in hello Azure-beheerportal voor Hallo AppName parameter.</span><span class="sxs-lookup"><span data-stu-id="4c0da-121">Note that you need toouse hello **App Resource Name** as defined in hello Azure management portal for hello AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="4c0da-122">Ten slotte definiëren Hallo CreateCampaign methode op die zorgt voor het eerder is geïnitialiseerd Hallo EngagementClient toocreate een eenvoudige **op elk gewenst moment** & **melding alleen-lezen** campagne met een titel en het bericht:</span><span class="sxs-lookup"><span data-stu-id="4c0da-122">Lastly, define hello CreateCampaign method which will take care of using hello previously initialized EngagementClient toocreate a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
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
10. <span data-ttu-id="4c0da-123">Voer Hallo console-app en u wordt ziet Hallo Hallo campagne gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4c0da-123">Run hello console app and you will see hello following on successful creation of hello campaign:</span></span>
    
    <span data-ttu-id="4c0da-124">**Campagne-Id '159' is gemaakt en de status 'Concept'**</span><span class="sxs-lookup"><span data-stu-id="4c0da-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png

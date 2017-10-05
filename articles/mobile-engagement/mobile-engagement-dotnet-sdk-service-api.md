---
title: Met behulp van .NET SDK voor toegang tot Azure Mobile Engagement Service API 's
description: Hierin wordt beschreven hoe u de Mobile Engagement .NET SDK gebruiken voor toegang tot Azure Mobile Engagement Service API 's
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
ms.openlocfilehash: 6a497189268c5a1b7e269cc57904ebc77c1906fd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="using-net-sdk-to-access-azure-mobile-engagement-service-apis"></a><span data-ttu-id="2004c-103">Met behulp van .NET SDK voor toegang tot Azure Mobile Engagement Service API 's</span><span class="sxs-lookup"><span data-stu-id="2004c-103">Using .NET SDK to access Azure Mobile Engagement Service APIs</span></span>
<span data-ttu-id="2004c-104">Beschrijft een reeks API's voor het beheer van apparaten, de Azure Mobile Engagement/te pushen Reach-campagnes enzovoort. Om te kunnen communiceren met deze API's, wij bieden u ook een [Swagger-bestand](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) waarmee u met hulpprogramma's kunt voor het genereren van SDK's voor uw voorkeurstaal.</span><span class="sxs-lookup"><span data-stu-id="2004c-104">Azure Mobile Engagement exposes a set of APIs for you to manage Devices, Reach/Push campaigns etc. To interact with these APIs, we also provide you a [Swagger file](https://github.com/Azure/azure-rest-api-specs/blob/master/arm-mobileengagement/2014-12-01/swagger/mobile-engagement.json) that you can use with tools to generate SDKs for your preferred language.</span></span> <span data-ttu-id="2004c-105">Wordt u aangeraden de [AutoRest](https://github.com/Azure/AutoRest) hulpprogramma voor het genereren van de SDK van onze Swagger-bestand.</span><span class="sxs-lookup"><span data-stu-id="2004c-105">We recommend using the [AutoRest](https://github.com/Azure/AutoRest) tool to generate your SDK from our Swagger file.</span></span>

> [!NOTE]
> <span data-ttu-id="2004c-106">De Azure Mobile Engagement-service wordt in maart 2018 beëindigd en is momenteel alleen beschikbaar voor bestaande klanten.</span><span class="sxs-lookup"><span data-stu-id="2004c-106">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="2004c-107">Zie [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2004c-107">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="2004c-108">We hebben een .NET-SDK op een vergelijkbare manier waarmee u communiceren met deze API's met behulp van een C#-wrapper gemaakt en u hoeft te doen de token verificatie-onderhandeling en vernieuw zelf.</span><span class="sxs-lookup"><span data-stu-id="2004c-108">We have created a .NET SDK in a similar manner which allows you to interact with these APIs using a C# wrapper and you don't have to do the authentication token negotiation and refresh yourself.</span></span>  

<span data-ttu-id="2004c-109">Dit voorbeeld wordt de reeks stappen te volgen voor het gebruik van de .NET SDK:</span><span class="sxs-lookup"><span data-stu-id="2004c-109">This sample goes through the set of steps to follow to use the .NET SDK:</span></span>

1. <span data-ttu-id="2004c-110">U moet eerst, om de verificatie voor uw API's met behulp van de Azure Active Directory zoals beschreven in te stellen [hier](mobile-engagement-api-authentication.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="2004c-110">First of all, you need to setup the authentication for your APIs using the Azure Active Directory as described [here](mobile-engagement-api-authentication.md#authentication).</span></span> <span data-ttu-id="2004c-111">Aan het einde van de volgende stappen u moet beschikken over een geldige **SubscriptionId**, **TenantId**, **ApplicationId** en **geheim**.</span><span class="sxs-lookup"><span data-stu-id="2004c-111">At the end of these steps, you should have a valid **SubscriptionId**, **TenantId**, **ApplicationId** and **Secret**.</span></span> 
2. <span data-ttu-id="2004c-112">We een eenvoudige app voor Windows-Console gebruiken om te werken met de .NET SDK met het scenario voor het maken van een campagne aankondiging demonstreren.</span><span class="sxs-lookup"><span data-stu-id="2004c-112">We will use a simple Windows Console app to demonstrate working with the .NET SDK with the scenario of creating an Announcement campaign.</span></span> <span data-ttu-id="2004c-113">Dus opent u Visual Studio en maak een **consoletoepassing**.</span><span class="sxs-lookup"><span data-stu-id="2004c-113">So open up Visual Studio and create a **Console Application**.</span></span>   
3. <span data-ttu-id="2004c-114">Vervolgens moet u de .NET SDK die beschikbaar als is download **Management-bibliotheek van Microsoft Azure Engagement** in de Nuget-galerie [hier](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span><span class="sxs-lookup"><span data-stu-id="2004c-114">Next you need to download the .NET SDK which is available as **Microsoft Azure Engagement Management Library** in the Nuget gallery [here](https://www.nuget.org/packages/Microsoft.Azure.Management.Engagement/).</span></span>
   <span data-ttu-id="2004c-115">Als u het Nuget vanuit Visual Studio installeert, moet u ervoor zorgen dat u ingeschakeld hebt de **Include prerelease** optie bij het zoeken naar het pakket:</span><span class="sxs-lookup"><span data-stu-id="2004c-115">If you are installing the Nuget from Visual Studio, you need to ensure that you have check marked the **Include prerelease** option while searching for the package:</span></span>
   
    ![][1]
4. <span data-ttu-id="2004c-116">In de `Program.cs` bestand, het toevoegen van de volgende naamruimten:</span><span class="sxs-lookup"><span data-stu-id="2004c-116">In the `Program.cs` file, add the following namespaces:</span></span>
   
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.Engagement;
        using Microsoft.Azure.Management.Engagement.Models;
5. <span data-ttu-id="2004c-117">Vervolgens moet u de volgende constanten die we gebruiken voor verificatie en interactie met de Mobile Engagement-App die u in de campagne aankondiging maakt definiëren:</span><span class="sxs-lookup"><span data-stu-id="2004c-117">Next you need to define the following constants that we will use for authentication and interacting with the Mobile Engagement App in which you are creating the Announcement campaign:</span></span>
   
        // For authentication
        const string TENANT_ID = "<Your TenantId>";
        const string CLIENT_ID = "<Your Application Id>";
        const string CLIENT_SECRET = "<Your Secret>";
        const string SUBSCRIPTION_ID = "<Your Subscription Id>";
   
        // This is the Azure Resource group concept for grouping together resources 
        //  see here: https://azure.microsoft.com/en-us/documentation/articles/resource-group-portal/
        const string RESOURCE_GROUP = "";
   
        // For Mobile Engagement operations
        // App Collection Name 
        const string APP_COLLECTION_NAME = "";
        // Application Resource Name - make sure you are using the one as specified in the Azure portal (NOT the App Name)
        const string APP_RESOURCE_NAME = "";
6. <span data-ttu-id="2004c-118">Definieer de `EngagementManagementClient` variabele die wordt gebruikt om de Mobile Engagement SDK-methoden aanroept:</span><span class="sxs-lookup"><span data-stu-id="2004c-118">Define the `EngagementManagementClient` variable which we will use to call the Mobile Engagement SDK methods:</span></span>
   
        static EngagementManagementClient engagementClient; 
7. <span data-ttu-id="2004c-119">Het volgende toevoegen aan uw `Main` methode:</span><span class="sxs-lookup"><span data-stu-id="2004c-119">Add the following to your `Main` method:</span></span>
   
        try
            {
                // Initialize the Engagement SDK to call out APIs. 
                InitEngagementClient().Wait();
   
                // Create a Reach campaign
                CreateCampaign().Wait();
            }
            catch (Exception ex)
            {
                Console.WriteLine(ex.InnerException.Message);
                throw ex;
            }
8. <span data-ttu-id="2004c-120">Definieer de volgende methode op die voor het initialiseren van zorgt de `EngagementManagementClient` door eerst te verifiëren en zichzelf vervolgens te koppelen met de Mobile Engagement-App waarin u van plan bent om de campagne aankondiging te maken:</span><span class="sxs-lookup"><span data-stu-id="2004c-120">Define the following method which takes care of initializing the `EngagementManagementClient` by first authenticating and then associating itself with the Mobile Engagement App in which you plan to create the Announcement campaign:</span></span>
   
        private static async Task InitEngagementClient()
        {
            var credentials = await ApplicationTokenProvider.LoginSilentAsync(TENANT_ID, CLIENT_ID, CLIENT_SECRET);
            engagementClient = new EngagementManagementClient(credentials) { SubscriptionId = SUBSCRIPTION_ID };
   
            // This is the Azure concept of ResourceGroup
            engagementClient.ResourceGroupName = RESOURCE_GROUP;
   
            // This is your Mobile Engagement App Collection & App Resource Name in which you create the campaign
            engagementClient.AppCollection = APP_COLLECTION_NAME;
            engagementClient.AppName = APP_RESOURCE_NAME;
        }
   
   > [!IMPORTANT]
   > <span data-ttu-id="2004c-121">Merk op dat u wilt gebruiken, de **App resourcenaam** zoals gedefinieerd in de Azure-beheerportal voor de parameter AppName.</span><span class="sxs-lookup"><span data-stu-id="2004c-121">Note that you need to use the **App Resource Name** as defined in the Azure management portal for the AppName parameter.</span></span> 
   > 
   > 
9. <span data-ttu-id="2004c-122">Ten slotte definiëren de CreateCampaign-methode op die zorgt voor een eenvoudige maken met de eerder geïnitialiseerd EngagementClient **op elk gewenst moment** & **melding alleen-lezen** campagne met een titel en het bericht:</span><span class="sxs-lookup"><span data-stu-id="2004c-122">Lastly, define the CreateCampaign method which will take care of using the previously initialized EngagementClient to create a simple **AnyTime** & **Notification-only** campaign with a title and message:</span></span> 
   
        private async static Task CreateCampaign()
        {
            //  Refer to the Announcement Campaign format from here - 
            //      https://msdn.microsoft.com/en-us/library/azure/mt683751.aspx
            // Make sure you are passing all the non-optional parameters
            Campaign parameters = new Campaign(
                name:"WelcomeCampaign",
                notificationTitle: "Welcome", 
                notificationMessage: "Thank you for installing the app!",
                type:"only_notif",
                deliveryTime:"any"
                );
   
            // Refer to the Campaign Kinds from here - https://msdn.microsoft.com/en-us/library/azure/mt683742.aspx
            CampaignStateResult result = 
                await engagementClient.Campaigns.CreateAsync(CampaignKinds.Announcements, parameters);
            Console.WriteLine("Campaign Id '{0}' was created successfully and it is in '{1}' state", result.Id, result.State);
        }
10. <span data-ttu-id="2004c-123">Voer de console-app en u ziet het volgende op de campagne gemaakt:</span><span class="sxs-lookup"><span data-stu-id="2004c-123">Run the console app and you will see the following on successful creation of the campaign:</span></span>
    
    <span data-ttu-id="2004c-124">**Campagne-Id '159' is gemaakt en de status 'Concept'**</span><span class="sxs-lookup"><span data-stu-id="2004c-124">**Campaign Id '159' was created successfully and it is in 'draft' state**</span></span>

<!-- Images. -->

[1]: ./media/mobile-engagement-dotnet-sdk-service-api/include-prerelease.png

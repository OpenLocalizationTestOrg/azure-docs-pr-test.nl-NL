---
title: Azure Mobile Engagement - back-end-integratie
description: Verbinding maken met Azure Mobile Engagement met een SharePoint-back-end campagnes maken van SharePoint
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 06297b43-579f-46e6-8a58-961a68f9aa09
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: d49f1094f4c3f170f3618f3e19e42266f9ae8858
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="f30f3-103">Azure Mobile Engagement - API-integratie</span><span class="sxs-lookup"><span data-stu-id="f30f3-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="f30f3-104">In een geautomatiseerde marketing-systeem, maken en activeren van de marketingcampagnes ook automatisch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f30f3-104">In an automated marketing system, creating and activating the marketing campaigns also occur automatically.</span></span> <span data-ttu-id="f30f3-105">Voor dit doel - Azure Mobile Engagement kunt maken van dergelijke geautomatiseerde marketingcampagnes ook met behulp van API's.</span><span class="sxs-lookup"><span data-stu-id="f30f3-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="f30f3-106">Klanten gebruiken doorgaans de Mobile Engagement-front-end interface aankondigingen/polls enzovoort als onderdeel van hun marketingcampagnes maken.</span><span class="sxs-lookup"><span data-stu-id="f30f3-106">Typically customers use the Mobile Engagement front end interface to create announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="f30f3-107">Maar zodra de marketingcampagnes volwassen, hoeft een gebruikmaken van de gegevens in de back endsystemen (zoals een CRM-systeem of CMS-systeem zoals SharePoint) moet worden vergrendeld zodat een volledig geautomatiseerde pijplijn kan worden gemaakt die campagnes maakt in Mobile Engagement dynamisch op basis van de gegevens die van de back endsystemen.</span><span class="sxs-lookup"><span data-stu-id="f30f3-107">However as the marketing campaigns become mature, there is a need to leverage the data locked in the backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on the data flowing in from the backend systems.</span></span> 

![][5]

<span data-ttu-id="f30f3-108">Deze zelfstudie doorloopt van een scenario waarbij een SharePoint-bedrijven gebruiker vult een SharePoint-lijst met marketing gegevens en een geautomatiseerd proces items uit de lijst wordt opgehaald en verbinding maakt met de Mobile Engagement-systeem met de beschikbare REST-API's voor het maken van een campagne van de SharePoint-gegevens.</span><span class="sxs-lookup"><span data-stu-id="f30f3-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from the list and connects with the Mobile Engagement system using the available REST APIs to create a marketing campaign from the SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f30f3-109">In het algemeen kunt u dit voorbeeld als uitgangspunt voor informatie over het aanroepen van Mobile Engagement REST API, zoals het details van de twee belangrijke aspecten van het aanroepen van de API - verificatie en doorgegeven parameters.</span><span class="sxs-lookup"><span data-stu-id="f30f3-109">In general, you can use this sample as a starting point for understanding how to call any Mobile Engagement REST API as it details the two key aspects of calling the APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="f30f3-110">Integratie met SharePoint</span><span class="sxs-lookup"><span data-stu-id="f30f3-110">SharePoint integration</span></span>
1. <span data-ttu-id="f30f3-111">Hier ziet u hoe de SharePoint-voorbeeldlijst eruit ziet.</span><span class="sxs-lookup"><span data-stu-id="f30f3-111">Here is what the sample SharePoint list looks like.</span></span> <span data-ttu-id="f30f3-112">**Titel**, **categorie**, **NotificationTitle**, **bericht** en **URL** worden gebruikt voor het maken van de aankondiging.</span><span class="sxs-lookup"><span data-stu-id="f30f3-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating the announcement.</span></span> <span data-ttu-id="f30f3-113">Er is een kolom met de naam **IsProcessed** die wordt gebruikt door het proces van het automation voorbeeld in de vorm van een consoleprogramma.</span><span class="sxs-lookup"><span data-stu-id="f30f3-113">There is a column called **IsProcessed** which is used by the sample automation process in the form of a console program.</span></span> <span data-ttu-id="f30f3-114">U kunt deze console programma als een webtaak Azure zodat u kunt plannen dat het uitvoeren of u kunt de SharePoint-werkstroom programma maken en de aankondiging activeren wanneer een item wordt ingevoegd in de SharePoint-lijst rechtstreeks gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f30f3-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use the SharePoint workflow to program creating and activating the announcement when an item is inserted into the SharePoint list.</span></span> <span data-ttu-id="f30f3-115">In dit voorbeeld gebruiken we de consoleprogramma gaat door de items in de SharePoint-lijst en de aankondiging te maken in Azure Mobile Engagement voor elk van deze en ten slotte markeert vervolgens de **IsProcessed** vlag waar op geslaagde aankondiging maken.</span><span class="sxs-lookup"><span data-stu-id="f30f3-115">In this sample we use the console program which goes through the items in the SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks the **IsProcessed** flag to be true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="f30f3-116">We gebruiken de code van de steekproef *externe verificatie in SharePoint Online met behulp van de Client-objectmodel* [hier](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) voor verificatie met de SharePoint-lijst.</span><span class="sxs-lookup"><span data-stu-id="f30f3-116">We are using the code from the sample *Remote Authentication in SharePoint Online Using the Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) to authenticate with the SharePoint list.</span></span>
3. <span data-ttu-id="f30f3-117">Eenmaal is geverifieerd, wordt de items in de lijst om erachter te komen de zojuist gemaakte items doorlopen (die zullen hebben **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="f30f3-117">Once authenticated, we loop through the list items to find out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
         static async void CreateCampaignFromSharepoint()
        {
            using (ClientContext clientContext = ClaimClientContext.GetAuthenticatedContext(targetSharepointSite))
            {
                // Using https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c for authentication     
                Web site = clientContext.Web;
                List list = site.Lists.GetByTitle("VideoContent");
                CamlQuery query = new CamlQuery();
                query.ViewXml = "<View/>";
                ListItemCollection items = list.GetItems(query);
   
                // Load the SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through the list to go through all the items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request to create AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this to true
                            item["IsProcessed"] = "Yes";
   
                            // Now try to activate the campaign also
                            await ActivateAzMECampaign(campaignId);
                        }
                        else
                        {
                            item["IsProcessed"] = "Error";
                        }
                        item.Update();
                    }
                clientContext.ExecuteQuery();
            }
        }

## <a name="mobile-engagement-integration"></a><span data-ttu-id="f30f3-118">Mobile Engagement-integratie</span><span class="sxs-lookup"><span data-stu-id="f30f3-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="f30f3-119">Zodra er een item dat worden verwerkt moet - gevonden we gegevens nodig voor het maken van een aankondiging van het item in de lijst en de aanroep ophalen `CreateAzMECampaign` om deze te maken en vervolgens `ActivateAzMECampaign` om deze te activeren.</span><span class="sxs-lookup"><span data-stu-id="f30f3-119">Once we find an item which requires processing - we extract the information required to create an announcement from the list item and call `CreateAzMECampaign` to create it and subsequently `ActivateAzMECampaign` to activate it.</span></span> <span data-ttu-id="f30f3-120">Dit zijn in wezen REST-API aanroepen aanroepen van de back-end van Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f30f3-120">These are essentially REST API calls calling to the Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="f30f3-121">De Mobile Engagement REST-API's vereisen een **Basic auth schema autorisatie HTTP-header** die bestaat uit de `ApplicationId` en de `ApiKey` die u krijgen via de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f30f3-121">The Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of the `ApplicationId` and the `ApiKey` which you get from the Azure portal.</span></span> <span data-ttu-id="f30f3-122">Zorg ervoor dat u van de sleutel van gebruikmaakt de **api-sleutels** sectie en *niet* van de **sdk sleutels** sectie.</span><span class="sxs-lookup"><span data-stu-id="f30f3-122">Make sure that you are using the Key from the **api keys** section and *not* from the **sdk keys** section.</span></span> 
   
   ![][2]
   
       static string CreateAuthZHeader()
       {
           string BasicAuthzHeaderString = "Basic " + EncodeTo64(ApplicationId + ":" + ApiKey);
           return BasicAuthzHeaderString;
       }
   
       static public string EncodeTo64(string toEncode)
       {
           byte[] toEncodeAsBytes = System.Text.ASCIIEncoding.ASCII.GetBytes(toEncode);
           string returnValue = System.Convert.ToBase64String(toEncodeAsBytes);
           return returnValue;
       }  
3. <span data-ttu-id="f30f3-123">Voor het maken van de aankondiging type campagne - verwijzen naar de [documentatie](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="f30f3-123">For creating the announcement type campaign - refer to the [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="f30f3-124">U moet ervoor zorgen dat u de campagne opgeeft `kind` als *aankondiging* en de [nettolading](https://msdn.microsoft.com/library/azure/mt683751.aspx) en door te geven als FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="f30f3-124">You need to make sure that you are specifying the campaign `kind` as *announcement* and the [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create the payload to send the content
                // Reference -> https://msdn.microsoft.com/library/dn913749.aspx
                string data =
                    @"{""name"":""" + campaignName + @"""," + 
                    @"""type"":""only_notif""," + 
                    @"""deliveryTime"":""any"","" + 
                    @""notificationTitle"":""" + notificationTitle + 
                    @""",""notificationMessage"":""" + notificationMessage + 
                    @""",""actionUrl"":""" + actionURL + @"""}";
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("data", data),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is the campaign id
                    campaignId = Convert.ToInt32(responseString);
                    Console.WriteLine("Campaign successfully created with id {0}", campaignId);
                }
                else
                {
                    Console.WriteLine("Campaign creation failed with error - '{0}'", responseString);
                }
                return campaignId;
            }
        }
4. <span data-ttu-id="f30f3-125">Nadat u de aankondiging gemaakt hebt, ziet u ongeveer als volgt op de Mobile Engagement-portal (Houd er rekening mee dat de status concept en geactiveerd = = N.V.T.)</span><span class="sxs-lookup"><span data-stu-id="f30f3-125">Once you have the announcement created, you will see something like the following on the Mobile Engagement portal (note that the State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="f30f3-126">`CreateAzMECampaign`maakt een campagne aankondiging en retourneert de Id naar de aanroeper.</span><span class="sxs-lookup"><span data-stu-id="f30f3-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id to the caller.</span></span> <span data-ttu-id="f30f3-127">`ActivateAzMECampaign`deze Id is vereist als de parameter om de campagne te activeren.</span><span class="sxs-lookup"><span data-stu-id="f30f3-127">`ActivateAzMECampaign` requires this Id as the parameter to activate the campaign.</span></span> 
   
        static async Task<bool> ActivateAzMECampaign(int campaignId)
        {
            string activateUriFragment = "/reach/1/activate";
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                var content = new FormUrlEncodedContent(new[] 
                {
                    new KeyValuePair<string, string>("kind", "announcement"),
                    new KeyValuePair<string, string>("id", campaignId.ToString()),
                });
   
                // Send the POST request
                var response = await client.PostAsync(url + activateUriFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                if (response.StatusCode.ToString() == "OK")
                {
                    Console.WriteLine("Campaign successfully activated");
                    return true;
                }
                else
                {
                    Console.WriteLine("Campaign activation failed with error - '{0}'", responseString);
                    return false;
                }
            }
        }
6. <span data-ttu-id="f30f3-128">Zodra u de aankondiging geactiveerd hebt, worden er ongeveer als volgt op de Mobile Engagement-portal:</span><span class="sxs-lookup"><span data-stu-id="f30f3-128">Once you have the announcement activated, you will see something like the following on the Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="f30f3-129">Zodra de campagne wordt geactiveerd, gaat alle apparaten die voldoen aan de criteria voor de campagne meldingen te zien.</span><span class="sxs-lookup"><span data-stu-id="f30f3-129">As soon as the campaign gets activated, any devices which satisfy the criterion on the campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="f30f3-130">U ziet ook dat het item in de lijst gemarkeerd met IsProcessed = false is ingesteld op waar zodra de aankondiging campagne is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f30f3-130">You will also notice that the list item marked with IsProcessed = false has been set to True once the announcement campaign is created.</span></span>  

<span data-ttu-id="f30f3-131">Dit voorbeeld gemaakt een eenvoudige aankondiging campagne voornamelijk de vereiste eigenschappen opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f30f3-131">This sample created a simple announcement campaign specifying mostly the required properties.</span></span> <span data-ttu-id="f30f3-132">U kunt dit aanpassen als u vanuit de portal kunt met behulp van de informatie [hier](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="f30f3-132">You can customize this as much as you can from the portal by using the information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png




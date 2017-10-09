---
title: aaaAzure Mobile Engagement - back-end-integratie
description: Verbinding maken met Azure Mobile Engagement met een SharePoint-campagnes back-end toocreate van SharePoint
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
ms.openlocfilehash: 89e1ef57db607d63c326a760b20260ad439f08b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement---api-integration"></a><span data-ttu-id="f295b-103">Azure Mobile Engagement - API-integratie</span><span class="sxs-lookup"><span data-stu-id="f295b-103">Azure Mobile Engagement - API integration</span></span>
<span data-ttu-id="f295b-104">In een geautomatiseerde marketing-systeem, maken en activeren Hallo marketingcampagnes ook automatisch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f295b-104">In an automated marketing system, creating and activating hello marketing campaigns also occur automatically.</span></span> <span data-ttu-id="f295b-105">Voor dit doel - Azure Mobile Engagement kunt maken van dergelijke geautomatiseerde marketingcampagnes ook met behulp van API's.</span><span class="sxs-lookup"><span data-stu-id="f295b-105">For this purpose - Azure Mobile Engagement enables creating such automated marketing campaigns using APIs as well.</span></span> 

<span data-ttu-id="f295b-106">Klanten wordt doorgaans Hallo Mobile Engagement-front-end interface toocreate aankondigingen/polls enzovoort gebruiken als onderdeel van hun marketingcampagnes.</span><span class="sxs-lookup"><span data-stu-id="f295b-106">Typically customers use hello Mobile Engagement front end interface toocreate announcements/polls etc as part of their marketing campaigns.</span></span> <span data-ttu-id="f295b-107">Maar als Hallo marketingcampagnes volwassen geworden, u een hoeft tooleverage Hallo gegevens vergrendeld in Hallo back-end-systemen (zoals een CRM-systeem of CMS-systeem zoals SharePoint) zodat een volledig geautomatiseerde pijplijn kan worden gemaakt die campagnes maakt in Mobile Engagement dynamisch op basis van Hallo-gegevens die vanuit Hallo back-end-systemen.</span><span class="sxs-lookup"><span data-stu-id="f295b-107">However as hello marketing campaigns become mature, there is a need tooleverage hello data locked in hello backend systems (like any CRM system or CMS system like SharePoint) so that a fully automated pipeline can be created which creates campaigns in Mobile Engagement dynamically based on hello data flowing in from hello backend systems.</span></span> 

![][5]

<span data-ttu-id="f295b-108">Deze zelfstudie gaan via een scenario waarbij een SharePoint-business-gebruiker een SharePoint-lijst met marketinggegevens gevuld en een geautomatiseerd proces items uit de lijst hello wordt opgehaald en verbinding maakt met het gebruik van Hallo Mobile Engagement system Hallo beschikbare REST-API 's toocreate een campagne Hallo SharePoint-gegevens.</span><span class="sxs-lookup"><span data-stu-id="f295b-108">This tutorial goes through such a scenario where a SharePoint business user populates a SharePoint list with marketing data and an automated process picks up items from hello list and connects with hello Mobile Engagement system using hello available REST APIs toocreate a marketing campaign from hello SharePoint data.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f295b-109">In het algemeen kunt u dit voorbeeld gebruiken als uitgangspunt om te begrijpen hoe toocall Mobile Engagement REST API's zoals deze details Hallo twee belangrijke aspecten van het aanroepen van Hallo-API's - verificatie en doorgegeven parameters.</span><span class="sxs-lookup"><span data-stu-id="f295b-109">In general, you can use this sample as a starting point for understanding how toocall any Mobile Engagement REST API as it details hello two key aspects of calling hello APIs - authenticating and passing parameters.</span></span> 
> 
> 

## <a name="sharepoint-integration"></a><span data-ttu-id="f295b-110">Integratie met SharePoint</span><span class="sxs-lookup"><span data-stu-id="f295b-110">SharePoint integration</span></span>
1. <span data-ttu-id="f295b-111">Hier volgt welke Hallo voorbeeld SharePoint-lijst ziet.</span><span class="sxs-lookup"><span data-stu-id="f295b-111">Here is what hello sample SharePoint list looks like.</span></span> <span data-ttu-id="f295b-112">**Titel**, **categorie**, **NotificationTitle**, **bericht** en **URL** worden gebruikt voor het maken van Hallo-aankondiging.</span><span class="sxs-lookup"><span data-stu-id="f295b-112">**Title**, **Category**, **NotificationTitle**, **Message** and **URL** are used for creating hello announcement.</span></span> <span data-ttu-id="f295b-113">Er is een kolom met de naam **IsProcessed** die wordt gebruikt door Hallo voorbeeld automatiseringsproces Hallo vorm van een consoleprogramma.</span><span class="sxs-lookup"><span data-stu-id="f295b-113">There is a column called **IsProcessed** which is used by hello sample automation process in hello form of a console program.</span></span> <span data-ttu-id="f295b-114">U kunt dit consoleprogramma ofwel uitvoeren als een webtaak Azure zodat u deze plannen kunt of u rechtstreeks kunt Hallo SharePoint werkstroom tooprogram maken en activeren Hallo aankondiging wanneer een item in de SharePoint-lijst hello wordt ingevoerd.</span><span class="sxs-lookup"><span data-stu-id="f295b-114">You can either run this console program as an Azure WebJob so that you can schedule it or you can directly use hello SharePoint workflow tooprogram creating and activating hello announcement when an item is inserted into hello SharePoint list.</span></span> <span data-ttu-id="f295b-115">In dit voorbeeld gebruiken we Hallo consoleprogramma gaat door Hallo items in Hallo SharePoint-lijst en de aankondiging te maken in Azure Mobile Engagement voor elk van deze en ten slotte markeert vervolgens Hallo **IsProcessed** vlag toobe ' True ' op geslaagde aankondiging maken.</span><span class="sxs-lookup"><span data-stu-id="f295b-115">In this sample we use hello console program which goes through hello items in hello SharePoint list and create announcement in Azure Mobile Engagement for each of them and then finally marks hello **IsProcessed** flag toobe true on successful announcement creation.</span></span>
   
    ![][1]
2. <span data-ttu-id="f295b-116">We gebruiken Hallo-code van Hallo voorbeeld *externe verificatie in SharePoint Online met behulp van Hallo van Client-objectmodel* [hier](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate met Hallo SharePoint-lijst.</span><span class="sxs-lookup"><span data-stu-id="f295b-116">We are using hello code from hello sample *Remote Authentication in SharePoint Online Using hello Client Object Model* [here](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate with hello SharePoint list.</span></span>
3. <span data-ttu-id="f295b-117">Eenmaal is geverifieerd, we doorlopen Hallo lijst items toofind alle gemaakte items (die zullen hebben **IsProcessed** = false).</span><span class="sxs-lookup"><span data-stu-id="f295b-117">Once authenticated, we loop through hello list items toofind out any newly created items (which will have **IsProcessed** = false).</span></span> 
   
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
   
                // Load hello SharePoint list
                clientContext.Load(list);
                clientContext.Load(items);
                clientContext.ExecuteQuery();
   
                // Loop through hello list toogo through all hello items which are newly added
                foreach (ListItem item in items)
                    if (item["IsProcessed"].ToString() != "Yes")
                    {
                        string name = item["Title"].ToString();
                        string notificationTitle = item["NotificationTitle"].ToString();
                        string notificationMessage = item["Message"].ToString();
                        string category = item["Category"].ToString();
                        string actionURL = ((FieldUrlValue)item["URL"]).Url;
   
                        // Send an HTTP request toocreate AzME campaign
                        int campaignId = CreateAzMECampaign
                            (name, notificationTitle, notificationMessage, category, actionURL).Result;
   
                        if (campaignId != -1)
                        {
                            // If creating campaign is successful then set this tootrue
                            item["IsProcessed"] = "Yes";
   
                            // Now try tooactivate hello campaign also
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

## <a name="mobile-engagement-integration"></a><span data-ttu-id="f295b-118">Mobile Engagement-integratie</span><span class="sxs-lookup"><span data-stu-id="f295b-118">Mobile Engagement integration</span></span>
1. <span data-ttu-id="f295b-119">Zodra er een item dat worden verwerkt moet vinden: we vereiste informatie op Hallo extraheren toocreate een aankondiging van Hallo lijstitem en roep `CreateAzMECampaign` toocreate deze en vervolgens `ActivateAzMECampaign` tooactivate deze.</span><span class="sxs-lookup"><span data-stu-id="f295b-119">Once we find an item which requires processing - we extract hello information required toocreate an announcement from hello list item and call `CreateAzMECampaign` toocreate it and subsequently `ActivateAzMECampaign` tooactivate it.</span></span> <span data-ttu-id="f295b-120">Dit zijn in wezen REST-API aanroepen voor het aanroepen van back-end van toohello Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="f295b-120">These are essentially REST API calls calling toohello Mobile Engagement backend.</span></span> 
2. <span data-ttu-id="f295b-121">Hallo Mobile Engagement REST-API's vereisen een **Basic auth schema autorisatie HTTP-header** die bestaat uit Hallo `ApplicationId` en Hallo `ApiKey` die u krijgt van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f295b-121">hello Mobile Engagement REST APIs require a **Basic auth scheme authorization HTTP header** which is composed of hello `ApplicationId` and hello `ApiKey` which you get from hello Azure portal.</span></span> <span data-ttu-id="f295b-122">Zorg ervoor dat u van Hallo sleutel uit Hallo gebruikmaakt **api-sleutels** sectie en *niet* van Hallo **sdk sleutels** sectie.</span><span class="sxs-lookup"><span data-stu-id="f295b-122">Make sure that you are using hello Key from hello **api keys** section and *not* from hello **sdk keys** section.</span></span> 
   
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
3. <span data-ttu-id="f295b-123">Voor het maken van Hallo aankondiging type campagne - Raadpleeg toohello [documentatie](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span><span class="sxs-lookup"><span data-stu-id="f295b-123">For creating hello announcement type campaign - refer toohello [documentation](https://msdn.microsoft.com/library/azure/mt683750.aspx).</span></span> <span data-ttu-id="f295b-124">Moet u ervoor dat u Hallo campagne opgeeft toomake `kind` als *aankondiging* en Hallo [nettolading](https://msdn.microsoft.com/library/azure/mt683751.aspx) en door te geven als FormUrlEncodedContent.</span><span class="sxs-lookup"><span data-stu-id="f295b-124">You need toomake sure that you are specifying hello campaign `kind` as *announcement* and hello [payload](https://msdn.microsoft.com/library/azure/mt683751.aspx) and passing it as FormUrlEncodedContent.</span></span> 
   
        static async Task<int> CreateAzMECampaign(string campaignName, string notificationTitle, 
            string notificationMessage, string notificationCategory, string actionURL)
        {
            string createURIFragment = "/reach/1/create";
   
            using (var client = new HttpClient())
            {
                // Add Authorization Header
                client.DefaultRequestHeaders.TryAddWithoutValidation("Authorization", CreateAuthZHeader());
   
                // Create hello payload toosend hello content
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
   
                // Send hello POST request
                var response = await client.PostAsync(url + createURIFragment, content);
                var responseString = response.Content.ReadAsStringAsync().Result;
                int campaignId = -1;
                if (response.StatusCode.ToString() == "OK")
                {
                    // This is hello campaign id
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
4. <span data-ttu-id="f295b-125">Nadat u gemaakt Hallo-aankondiging hebt, ziet u dat lijkt op Hallo op Hallo Mobile Engagement-portal (Houd er rekening mee dat Hallo status = concept en geactiveerd = N.V.T.)</span><span class="sxs-lookup"><span data-stu-id="f295b-125">Once you have hello announcement created, you will see something like hello following on hello Mobile Engagement portal (note that hello State=Draft and Activated = N/A)</span></span>
   
    ![][3]
5. <span data-ttu-id="f295b-126">`CreateAzMECampaign`maakt een campagne aankondiging en retourneert de Id toohello aanroeper.</span><span class="sxs-lookup"><span data-stu-id="f295b-126">`CreateAzMECampaign` creates an announcement campaign and returns its Id toohello caller.</span></span> <span data-ttu-id="f295b-127">`ActivateAzMECampaign`deze Id is vereist als Hallo parameter tooactivate Hallo campagne.</span><span class="sxs-lookup"><span data-stu-id="f295b-127">`ActivateAzMECampaign` requires this Id as hello parameter tooactivate hello campaign.</span></span> 
   
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
   
                // Send hello POST request
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
6. <span data-ttu-id="f295b-128">Zodra u Hallo aankondiging geactiveerd hebt, ziet u dat lijkt op de volgende Hallo op Hallo Mobile Engagement-portal:</span><span class="sxs-lookup"><span data-stu-id="f295b-128">Once you have hello announcement activated, you will see something like hello following on hello Mobile Engagement portal:</span></span>
   
    ![][4]
7. <span data-ttu-id="f295b-129">Zodra de campagne Hallo wordt geactiveerd, gaat alle apparaten die voldoen aan Hallo criterium op Hallo campagne meldingen te zien.</span><span class="sxs-lookup"><span data-stu-id="f295b-129">As soon as hello campaign gets activated, any devices which satisfy hello criterion on hello campaign will start seeing notifications.</span></span> 
8. <span data-ttu-id="f295b-130">U ziet ook dat lijstitem Hallo gemarkeerd met IsProcessed = false is ingesteld tooTrue zodra Hallo aankondiging campagne is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f295b-130">You will also notice that hello list item marked with IsProcessed = false has been set tooTrue once hello announcement campaign is created.</span></span>  

<span data-ttu-id="f295b-131">Dit voorbeeld gemaakt een eenvoudige aankondiging campagne voornamelijk Hallo vereist eigenschappen opgeven.</span><span class="sxs-lookup"><span data-stu-id="f295b-131">This sample created a simple announcement campaign specifying mostly hello required properties.</span></span> <span data-ttu-id="f295b-132">U kunt dit aanpassen zoveel u vanuit de portal Hallo kunt met behulp van Hallo informatie [hier](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span><span class="sxs-lookup"><span data-stu-id="f295b-132">You can customize this as much as you can from hello portal by using hello information [here](https://msdn.microsoft.com/library/azure/mt683751.aspx).</span></span> 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png




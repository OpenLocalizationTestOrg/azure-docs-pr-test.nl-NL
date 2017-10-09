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
# <a name="azure-mobile-engagement---api-integration"></a>Azure Mobile Engagement - API-integratie
In een geautomatiseerde marketing-systeem, maken en activeren Hallo marketingcampagnes ook automatisch uitgevoerd. Voor dit doel - Azure Mobile Engagement kunt maken van dergelijke geautomatiseerde marketingcampagnes ook met behulp van API's. 

Klanten wordt doorgaans Hallo Mobile Engagement-front-end interface toocreate aankondigingen/polls enzovoort gebruiken als onderdeel van hun marketingcampagnes. Maar als Hallo marketingcampagnes volwassen geworden, u een hoeft tooleverage Hallo gegevens vergrendeld in Hallo back-end-systemen (zoals een CRM-systeem of CMS-systeem zoals SharePoint) zodat een volledig geautomatiseerde pijplijn kan worden gemaakt die campagnes maakt in Mobile Engagement dynamisch op basis van Hallo-gegevens die vanuit Hallo back-end-systemen. 

![][5]

Deze zelfstudie gaan via een scenario waarbij een SharePoint-business-gebruiker een SharePoint-lijst met marketinggegevens gevuld en een geautomatiseerd proces items uit de lijst hello wordt opgehaald en verbinding maakt met het gebruik van Hallo Mobile Engagement system Hallo beschikbare REST-API 's toocreate een campagne Hallo SharePoint-gegevens. 

> [!IMPORTANT]
> In het algemeen kunt u dit voorbeeld gebruiken als uitgangspunt om te begrijpen hoe toocall Mobile Engagement REST API's zoals deze details Hallo twee belangrijke aspecten van het aanroepen van Hallo-API's - verificatie en doorgegeven parameters. 
> 
> 

## <a name="sharepoint-integration"></a>Integratie met SharePoint
1. Hier volgt welke Hallo voorbeeld SharePoint-lijst ziet. **Titel**, **categorie**, **NotificationTitle**, **bericht** en **URL** worden gebruikt voor het maken van Hallo-aankondiging. Er is een kolom met de naam **IsProcessed** die wordt gebruikt door Hallo voorbeeld automatiseringsproces Hallo vorm van een consoleprogramma. U kunt dit consoleprogramma ofwel uitvoeren als een webtaak Azure zodat u deze plannen kunt of u rechtstreeks kunt Hallo SharePoint werkstroom tooprogram maken en activeren Hallo aankondiging wanneer een item in de SharePoint-lijst hello wordt ingevoerd. In dit voorbeeld gebruiken we Hallo consoleprogramma gaat door Hallo items in Hallo SharePoint-lijst en de aankondiging te maken in Azure Mobile Engagement voor elk van deze en ten slotte markeert vervolgens Hallo **IsProcessed** vlag toobe ' True ' op geslaagde aankondiging maken.
   
    ![][1]
2. We gebruiken Hallo-code van Hallo voorbeeld *externe verificatie in SharePoint Online met behulp van Hallo van Client-objectmodel* [hier](https://code.msdn.microsoft.com/Remote-Authentication-in-b7b6f43c) tooauthenticate met Hallo SharePoint-lijst.
3. Eenmaal is geverifieerd, we doorlopen Hallo lijst items toofind alle gemaakte items (die zullen hebben **IsProcessed** = false). 
   
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

## <a name="mobile-engagement-integration"></a>Mobile Engagement-integratie
1. Zodra er een item dat worden verwerkt moet vinden: we vereiste informatie op Hallo extraheren toocreate een aankondiging van Hallo lijstitem en roep `CreateAzMECampaign` toocreate deze en vervolgens `ActivateAzMECampaign` tooactivate deze. Dit zijn in wezen REST-API aanroepen voor het aanroepen van back-end van toohello Mobile Engagement. 
2. Hallo Mobile Engagement REST-API's vereisen een **Basic auth schema autorisatie HTTP-header** die bestaat uit Hallo `ApplicationId` en Hallo `ApiKey` die u krijgt van hello Azure-portal. Zorg ervoor dat u van Hallo sleutel uit Hallo gebruikmaakt **api-sleutels** sectie en *niet* van Hallo **sdk sleutels** sectie. 
   
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
3. Voor het maken van Hallo aankondiging type campagne - Raadpleeg toohello [documentatie](https://msdn.microsoft.com/library/azure/mt683750.aspx). Moet u ervoor dat u Hallo campagne opgeeft toomake `kind` als *aankondiging* en Hallo [nettolading](https://msdn.microsoft.com/library/azure/mt683751.aspx) en door te geven als FormUrlEncodedContent. 
   
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
4. Nadat u gemaakt Hallo-aankondiging hebt, ziet u dat lijkt op Hallo op Hallo Mobile Engagement-portal (Houd er rekening mee dat Hallo status = concept en geactiveerd = N.V.T.)
   
    ![][3]
5. `CreateAzMECampaign`maakt een campagne aankondiging en retourneert de Id toohello aanroeper. `ActivateAzMECampaign`deze Id is vereist als Hallo parameter tooactivate Hallo campagne. 
   
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
6. Zodra u Hallo aankondiging geactiveerd hebt, ziet u dat lijkt op de volgende Hallo op Hallo Mobile Engagement-portal:
   
    ![][4]
7. Zodra de campagne Hallo wordt geactiveerd, gaat alle apparaten die voldoen aan Hallo criterium op Hallo campagne meldingen te zien. 
8. U ziet ook dat lijstitem Hallo gemarkeerd met IsProcessed = false is ingesteld tooTrue zodra Hallo aankondiging campagne is gemaakt.  

Dit voorbeeld gemaakt een eenvoudige aankondiging campagne voornamelijk Hallo vereist eigenschappen opgeven. U kunt dit aanpassen zoveel u vanuit de portal Hallo kunt met behulp van Hallo informatie [hier](https://msdn.microsoft.com/library/azure/mt683751.aspx). 

<!-- Images. -->
[1]: ./media/mobile-engagement-sample-backend-integration-sharepoint/sharepointlist.png
[2]: ./media/mobile-engagement-sample-backend-integration-sharepoint/properties.png
[3]: ./media/mobile-engagement-sample-backend-integration-sharepoint/new-announcement.png
[4]: ./media/mobile-engagement-sample-backend-integration-sharepoint/activate-announcement.png
[5]: ./media/mobile-engagement-sample-backend-integration-sharepoint/diagram.png




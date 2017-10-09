---
title: aaaAuthenticate met Mobile Engagement REST-API's - handmatige installatie
description: Hierin wordt beschreven hoe toomanually instellen voor verificatie voor Mobile Engagement REST-API 's
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a><span data-ttu-id="1f035-103">Verificatie met de Mobile Engagement REST-API's - handmatige installatie</span><span class="sxs-lookup"><span data-stu-id="1f035-103">Authenticate with Mobile Engagement REST APIs - manual setup</span></span>
<span data-ttu-id="1f035-104">Dit is een bijlage documentatie te[verifiëren met Mobile Engagement REST-API's](mobile-engagement-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1f035-104">This is an appendix documentation too[Authenticate with Mobile Engagement REST APIs](mobile-engagement-api-authentication.md).</span></span> <span data-ttu-id="1f035-105">Zorg ervoor dat u het eerste tooget Hallo context lezen.</span><span class="sxs-lookup"><span data-stu-id="1f035-105">Make sure you read it first tooget hello context.</span></span> <span data-ttu-id="1f035-106">Hier wordt een andere manier toodo Hallo eenmalige instelling voor het instellen van de verificatie van uw beschreven voor Hallo met behulp van Mobile Engagement REST-API's hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="1f035-106">This describes an alternate way toodo hello One-time setup for setting up your authentication for hello Mobile Engagement REST APIs using hello Azure Portal.</span></span> 

> [!NOTE]
> <span data-ttu-id="1f035-107">Hallo-instructies die hieronder zijn gebaseerd op deze [Active Directory-handleiding](../azure-resource-manager/resource-group-create-service-principal-portal.md) en aangepast voor wat vereist voor verificatie voor Mobile Engagement-API's is.</span><span class="sxs-lookup"><span data-stu-id="1f035-107">hello instructions below are based on this [Active Directory guide](../azure-resource-manager/resource-group-create-service-principal-portal.md) and customized for what is required for authentication for Mobile Engagement APIs.</span></span> <span data-ttu-id="1f035-108">Raadpleeg tooit dus als u wilt dat toounderstand Hallo stappen hieronder in detail besproken.</span><span class="sxs-lookup"><span data-stu-id="1f035-108">So refer tooit if you want toounderstand hello steps below in detail.</span></span> 
> 
> 

1. <span data-ttu-id="1f035-109">Aanmelding tooyour Azure-Account via Hallo [klassieke portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="1f035-109">Login tooyour Azure Account through hello [classic portal](https://manage.windowsazure.com/).</span></span>
2. <span data-ttu-id="1f035-110">Selecteer **Active Directory** in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f035-110">Select **Active Directory** from hello left pane.</span></span>
   
     ![Selecteer Active Directory][1]
3. <span data-ttu-id="1f035-112">Kies Hallo **Active standaarddirectory** in uw Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1f035-112">Choose hello **Default Active Directory** in your Azure portal.</span></span> 
   
     ![map te kiezen][2]
   
   > [!IMPORTANT]
   > <span data-ttu-id="1f035-114">Deze methode werkt alleen als u in Hallo standaard Active Directory van uw account werkt en niet werken als u dit doen in een Active Directory die u hebt gemaakt in uw account.</span><span class="sxs-lookup"><span data-stu-id="1f035-114">This approach works only when you are working in hello default Active Directory of your account and will not work if you are doing this in an Active Directory that you have created in your account.</span></span> 
   > 
   > 
4. <span data-ttu-id="1f035-115">tooview hello toepassingen in uw directory, klikt u op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="1f035-115">tooview hello applications in your directory, click on **Applications**.</span></span>
   
     ![toepassingen weergeven][3]
5. <span data-ttu-id="1f035-117">Klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="1f035-117">Click on **ADD**.</span></span> 
   
     ![Toepassing toevoegen][4]
6. <span data-ttu-id="1f035-119">Klik op **mijn organisatie ontwikkelt toepassing toevoegen**</span><span class="sxs-lookup"><span data-stu-id="1f035-119">Click on **Add an application my organization is developing**</span></span>
   
     ![nieuwe toepassing][5]
7. <span data-ttu-id="1f035-121">Vul in de naam van de toepassing hello en selecteer Hallo type toepassing als **WEBTOEPASSING en/of WEB-API** en klik op de volgende knop Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f035-121">Fill in name of hello application and select hello type of application as **WEB APPLICATION AND/OR WEB API** and click hello next button.</span></span>
   
     ![de naam van toepassing][6]
8. <span data-ttu-id="1f035-123">U kunt opgeven dat alle dummy-URL's voor **AANMELDINGS-URL** en **APP ID URI**.</span><span class="sxs-lookup"><span data-stu-id="1f035-123">You can provide any dummy URLs for **SIGN-ON URL** and **APP ID URI**.</span></span> <span data-ttu-id="1f035-124">Ze worden niet gebruikt voor ons scenario en URL's Hallo zelf worden niet gevalideerd.</span><span class="sxs-lookup"><span data-stu-id="1f035-124">They are not used for our scenario and hello URLs themselves are not validated.</span></span>  
   
     ![Toepassingseigenschappen][7]
9. <span data-ttu-id="1f035-126">Aan het einde van de Hallo hiervan hebt u een AAD-app met Hallo naam die u eerder Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="1f035-126">At hello end of this, you will have an AAD app with hello name you provided previously like hello following.</span></span> <span data-ttu-id="1f035-127">Dit is uw **AD\_APP\_naam** en noteer deze.</span><span class="sxs-lookup"><span data-stu-id="1f035-127">This is your **AD\_APP\_NAME** and make a note of it.</span></span>  
   
     ![App-naam][8]
10. <span data-ttu-id="1f035-129">Klik op de naam van de app Hallo en klik op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="1f035-129">Click on hello app name and click on **Configure**.</span></span>
    
      ![App configureren][9]
11. <span data-ttu-id="1f035-131">Maak een notitie van Hallo CLIENT-ID die wordt gebruikt als **CLIENT\_ID** voor uw API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1f035-131">Make a note of hello CLIENT ID that will be used as **CLIENT\_ID** for your API calls.</span></span> 
    
     ![App configureren][10]
12. <span data-ttu-id="1f035-133">Schuif omlaag toohello **sleutels** gedeelte en een sleutel met bij voorkeur 2 jaar (verlopen) duur toevoegen en klik op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="1f035-133">Scroll down toohello **Keys** section and add a key with preferably 2 years (expiry) duration and click **Save**.</span></span> 
    
     ![App configureren][11]
13. <span data-ttu-id="1f035-135">Kopieer onmiddellijk Hallo-waarde die wordt weergegeven voor de sleutel Hallo omdat deze nu alleen weergegeven wordt en niet opgeslagen wordt zodat u niet steeds opnieuw weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f035-135">Immediately copy hello value which is shown for hello key as it is only shown now and is not stored so will not be displayed ever again.</span></span> <span data-ttu-id="1f035-136">Als u deze verliest vervolgens hebt u toogenerate een nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="1f035-136">If you lose it then you will have toogenerate a new key.</span></span> <span data-ttu-id="1f035-137">Dit is Hallo **CLIENT_SECRET** voor uw API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1f035-137">This will be hello **CLIENT_SECRET** for your API calls.</span></span> 
    
     ![App configureren][12]
    
    > [!IMPORTANT]
    > <span data-ttu-id="1f035-139">Deze sleutel verlopen op Hallo einde van Hallo duur die u hebt opgegeven in dat geval Zorg ervoor dat toorenew wanneer Hallo nadert anders uw API-verificatie niet meer werkt.</span><span class="sxs-lookup"><span data-stu-id="1f035-139">This key will expire at hello end of hello duration that you specified so make sure toorenew it when hello time comes otherwise your API authentication will not work anymore.</span></span> <span data-ttu-id="1f035-140">U kunt ook verwijderen en opnieuw maken van deze sleutel als u denkt dat deze is geschonden.</span><span class="sxs-lookup"><span data-stu-id="1f035-140">You can also delete and recreate this key if you think that it has been compromised.</span></span>
    > 
    > 
14. <span data-ttu-id="1f035-141">Klik op **EINDPUNTEN weergeven** knop nu Hallo die geopend **App eindpunten** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="1f035-141">Click on **VIEW ENDPOINTS** button now which will open up hello **App Endpoints** dialog box.</span></span> 
    
    ![][13]
15. <span data-ttu-id="1f035-142">Hallo App eindpunten in het dialoogvenster kopiëren Hallo **OAUTH 2.0-TOKENEINDPUNT**.</span><span class="sxs-lookup"><span data-stu-id="1f035-142">From hello App Endpoints dialog box, copy hello **OAUTH 2.0 TOKEN ENDPOINT**.</span></span> 
    
    ![][14]
16. <span data-ttu-id="1f035-143">Dit eindpunt worden weergegeven in Hallo formulier te volgen waarbij Hallo GUID in Hallo-URL is uw **TENANT_ID** dus maak een notitie van deze:</span><span class="sxs-lookup"><span data-stu-id="1f035-143">This endpoint will be in hello following form where hello GUID in hello URL is your **TENANT_ID** so make a note of it:</span></span> 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. <span data-ttu-id="1f035-144">Er wordt nu tooconfigure Hallo machtigingen voor deze app worden voortgezet.</span><span class="sxs-lookup"><span data-stu-id="1f035-144">Now we will proceed tooconfigure hello permissions on this app.</span></span> <span data-ttu-id="1f035-145">Hiervoor hebt u tooopen up Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1f035-145">For this you will have tooopen up hello [Azure portal](https://portal.azure.com).</span></span> 
18. <span data-ttu-id="1f035-146">Klik op **resourcegroepen** en Hallo zoeken **Mobile Engagement** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="1f035-146">Click on **Resource Groups** and find hello **Mobile Engagement** resource group.</span></span>  
    
    ![][15]
19. <span data-ttu-id="1f035-147">Klik op Hallo **Mobile Engagement** resource groeperen en navigeer toohello **instellingen** blade hier.</span><span class="sxs-lookup"><span data-stu-id="1f035-147">Click hello **Mobile Engagement** resource group and navigate toohello **Settings** blade here.</span></span> 
    
    ![][16]
20. <span data-ttu-id="1f035-148">Klik op **gebruikers** in Hallo blade instellingen en klik vervolgens op **toevoegen** tooadd een gebruiker.</span><span class="sxs-lookup"><span data-stu-id="1f035-148">Click on **Users** in hello Settings blade and then click on **Add** tooadd a user.</span></span> 
    
    ![][17]
21. <span data-ttu-id="1f035-149">Klik op **een rol selecteren**</span><span class="sxs-lookup"><span data-stu-id="1f035-149">Click on **Select a role**</span></span>
    
    ![][18]
22. <span data-ttu-id="1f035-150">Klik op **eigenaar**</span><span class="sxs-lookup"><span data-stu-id="1f035-150">Click on **Owner**</span></span>
    
    ![][19]
23. <span data-ttu-id="1f035-151">Zoeken naar de naam van uw toepassing hello **AD\_APP\_naam** in het zoekvak Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f035-151">Search for hello name of your application **AD\_APP\_NAME** in hello Search box.</span></span> <span data-ttu-id="1f035-152">U ziet dit hier standaard.</span><span class="sxs-lookup"><span data-stu-id="1f035-152">You will not see this by default here.</span></span> <span data-ttu-id="1f035-153">Als u deze hebt gevonden, selecteert u deze en klik op **Selecteer** Hallo Hallo blade onderaan in.</span><span class="sxs-lookup"><span data-stu-id="1f035-153">Once you find it, select it and click on **Select** at hello bottom of hello blade.</span></span> 
    
    ![][20]
24. <span data-ttu-id="1f035-154">Op Hallo **toegang toevoegen** blade, deze wordt weergegeven als **1 gebruiker, 0 groepen**.</span><span class="sxs-lookup"><span data-stu-id="1f035-154">On hello **Add Access** blade, it will show up as **1 user, 0 groups**.</span></span> <span data-ttu-id="1f035-155">Klik op **OK** op deze blade tooconfirm Hallo wijziging.</span><span class="sxs-lookup"><span data-stu-id="1f035-155">Click **OK** on this blade tooconfirm hello change.</span></span> 
    
    ![][21]

<span data-ttu-id="1f035-156">U hebt nu Hallo vereist AAD-configuratie voltooid en u alle set toocall Hallo API's.</span><span class="sxs-lookup"><span data-stu-id="1f035-156">You have now completed hello required AAD configuration and you are all set toocall hello APIs.</span></span> 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png




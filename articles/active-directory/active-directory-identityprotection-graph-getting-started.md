---
title: 'Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph | Microsoft Docs'
description: Biedt een inleiding tot Microsoft Graph query voor een lijst met risico's en bijbehorende gegevens van Azure Active Directory.
services: active-directory
keywords: beveiliging voor Azure active directory-identiteit, risicogebeurtenis, beveiligingsprobleem, beveiligingsbeleid, Microsoft Graph
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: fa109ba7-a914-437b-821d-2bd98e681386
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 9b01ff86da6a1fd4a439a6ba59ea15ed6480cdad
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="52d89-104">Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="52d89-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="52d89-105">Microsoft Graph is de Microsoft unified API-eindpunt en het hart van [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) API's.</span><span class="sxs-lookup"><span data-stu-id="52d89-105">Microsoft Graph is the Microsoft unified API endpoint and the home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="52d89-106">De eerste API **identityRiskEvents**, kunt u Microsoft Graph opvragen voor een lijst met [bestaat de kans dat gebeurtenissen](active-directory-identityprotection-risk-events-types.md) en informatie die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="52d89-106">The first API, **identityRiskEvents**, allows you to query Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="52d89-107">In dit artikel helpt u op weg met het opvragen van deze API.</span><span class="sxs-lookup"><span data-stu-id="52d89-107">This article gets you started querying this API.</span></span> <span data-ttu-id="52d89-108">Zie voor een gedetailleerde inleiding, volledige documentatie en toegang tot de grafiek Explorer, de [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="52d89-108">For an in-depth introduction, full documentation, and access to the Graph Explorer, see the [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="52d89-109">Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="52d89-109">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="52d89-110">Er zijn drie stappen voor het openen van Identity Protection gegevens via Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="52d89-110">There are three steps to accessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="52d89-111">Toevoegen van een toepassing met een clientgeheim.</span><span class="sxs-lookup"><span data-stu-id="52d89-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="52d89-112">Gebruik dit geheim en enkele andere stukjes informatie om Microsoft Graph, waarbij er geen verificatietoken te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="52d89-112">Use this secret and a few other pieces of information to authenticate to Microsoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="52d89-113">Gebruik dit token aanvragen in de API-eindpunt aanbrengen en terughalen van gegevens voor de beveiliging van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="52d89-113">Use this token to make requests to the API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="52d89-114">Voordat u begint, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="52d89-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="52d89-115">Beheerdersrechten voor de toepassing in Azure AD maken</span><span class="sxs-lookup"><span data-stu-id="52d89-115">Administrator privileges to create the application in Azure AD</span></span>
* <span data-ttu-id="52d89-116">De naam van uw tenant-domein (bijvoorbeeld: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="52d89-116">The name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="52d89-117">Een toepassing met een clientgeheim toevoegen</span><span class="sxs-lookup"><span data-stu-id="52d89-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="52d89-118">[Meld u aan](https://manage.windowsazure.com) bij de klassieke Azure portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="52d89-118">[Sign in](https://manage.windowsazure.com) to your Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="52d89-119">Klik op in het navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="52d89-119">On on the left navigation pane, click **Active Directory**.</span></span> 
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="52d89-121">Van de **Directory** , selecteert u de map waarvoor u wilt inschakelen van Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="52d89-121">From the **Directory** list, select the directory for which you want to enable directory integration.</span></span>
4. <span data-ttu-id="52d89-122">Klik in het menu bovenaan op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="52d89-122">In the menu on the top, click **Applications**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="52d89-124">Klik op **toevoegen** aan de onderkant van de pagina.</span><span class="sxs-lookup"><span data-stu-id="52d89-124">Click **Add** at the bottom of the page.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="52d89-126">Op de **wat wilt u doen** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52d89-126">On the **What do you want to do** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="52d89-128">Op de **Vertel ons over uw toepassing** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="52d89-128">On the **Tell us about your application** dialog, perform the following steps:</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="52d89-130">a.</span><span class="sxs-lookup"><span data-stu-id="52d89-130">a.</span></span> <span data-ttu-id="52d89-131">In de **naam** textbox, typ een naam voor uw toepassing (bijvoorbeeld: AADIP risico gebeurtenis API toepassing).</span><span class="sxs-lookup"><span data-stu-id="52d89-131">In the **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="52d89-132">b.</span><span class="sxs-lookup"><span data-stu-id="52d89-132">b.</span></span> <span data-ttu-id="52d89-133">Als **Type**, selecteer **webtoepassing en / of Web-API**.</span><span class="sxs-lookup"><span data-stu-id="52d89-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="52d89-134">c.</span><span class="sxs-lookup"><span data-stu-id="52d89-134">c.</span></span> <span data-ttu-id="52d89-135">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="52d89-135">Click **Next**.</span></span>
8. <span data-ttu-id="52d89-136">Op de **App-eigenschappen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="52d89-136">On the **App properties** dialog, perform the following steps:</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="52d89-138">a.</span><span class="sxs-lookup"><span data-stu-id="52d89-138">a.</span></span> <span data-ttu-id="52d89-139">In de **aanmeldings-URL** textbox type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="52d89-139">In the **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="52d89-140">b.</span><span class="sxs-lookup"><span data-stu-id="52d89-140">b.</span></span> <span data-ttu-id="52d89-141">In de **App ID URI** textbox type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="52d89-141">In the **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="52d89-142">c.</span><span class="sxs-lookup"><span data-stu-id="52d89-142">c.</span></span> <span data-ttu-id="52d89-143">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="52d89-143">Click **Complete**.</span></span>

<span data-ttu-id="52d89-144">U kunt nu uw toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="52d89-144">Your can now configure your application.</span></span>

![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-to-use-the-api"></a><span data-ttu-id="52d89-146">Uw toepassing toestemming de API gebruiken</span><span class="sxs-lookup"><span data-stu-id="52d89-146">Grant your application permission to use the API</span></span>
1. <span data-ttu-id="52d89-147">Klik op de pagina van uw toepassing in het menu aan de bovenkant op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="52d89-147">On your application's page, in the menu on the top, click **Configure**.</span></span> 
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="52d89-149">In de **machtigingen voor andere toepassingen** sectie, klikt u op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="52d89-149">In the **permissions to other applications** section, click **Add application**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="52d89-151">Op de **machtigingen voor andere toepassingen** dialoogvenster de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="52d89-151">On the **permissions to other applications** dialog, perform the following steps:</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="52d89-153">a.</span><span class="sxs-lookup"><span data-stu-id="52d89-153">a.</span></span> <span data-ttu-id="52d89-154">Selecteer **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="52d89-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="52d89-155">b.</span><span class="sxs-lookup"><span data-stu-id="52d89-155">b.</span></span> <span data-ttu-id="52d89-156">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="52d89-156">Click **Complete**.</span></span>
4. <span data-ttu-id="52d89-157">Klik op **Toepassingsmachtigingen: 0**, en selecteer vervolgens **lezen van alle gegevens van identiteit risico gebeurtenis**.</span><span class="sxs-lookup"><span data-stu-id="52d89-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="52d89-159">Klik op **Opslaan** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="52d89-159">Click **Save** at the bottom of the page.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="52d89-161">Een toegangssleutel opvragen</span><span class="sxs-lookup"><span data-stu-id="52d89-161">Get an access key</span></span>
1. <span data-ttu-id="52d89-162">Klik op de pagina van uw toepassing in de **sleutels** sectie, selecteert u 1 jaar als duur.</span><span class="sxs-lookup"><span data-stu-id="52d89-162">On your application's page, in the **keys** section, select 1 year as duration.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="52d89-164">Klik op **Opslaan** onder aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="52d89-164">Click **Save** at the bottom of the page.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="52d89-166">Kopieer de waarde van de zojuist gemaakte sleutel in de sectie sleutels en plak deze in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="52d89-166">in the keys section, copy the value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="52d89-168">Als u deze sleutel kwijtraakt, wordt u terug naar deze sectie en maak een nieuwe sleutel hebben.</span><span class="sxs-lookup"><span data-stu-id="52d89-168">If you lose this key, you will have to return to this section and create a new key.</span></span> <span data-ttu-id="52d89-169">Een geheim voor deze sleutel behouden: iedereen die deze heeft toegang tot uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="52d89-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="52d89-170">In de **eigenschappen** sectie, Kopieer de **Client-ID**, en plak deze in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="52d89-170">In the **properties** section, copy the **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-to-microsoft-graph-and-query-the-identity-risk-events-api"></a><span data-ttu-id="52d89-171">Verifiëren naar Microsoft Graph en de identiteit risico gebeurtenissen API query</span><span class="sxs-lookup"><span data-stu-id="52d89-171">Authenticate to Microsoft Graph and query the Identity Risk Events API</span></span>
<span data-ttu-id="52d89-172">Op dit moment dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="52d89-172">At this point, you should have:</span></span>

* <span data-ttu-id="52d89-173">De client-ID die u hierboven hebt gekopieerd</span><span class="sxs-lookup"><span data-stu-id="52d89-173">The client ID you copied above</span></span>
* <span data-ttu-id="52d89-174">De sleutel die u hierboven hebt gekopieerd</span><span class="sxs-lookup"><span data-stu-id="52d89-174">The key you copied above</span></span>
* <span data-ttu-id="52d89-175">De naam van uw tenant-domein</span><span class="sxs-lookup"><span data-stu-id="52d89-175">The name of your tenant's domain</span></span>

<span data-ttu-id="52d89-176">Om te verifiëren, verzendt u een post-aanvraag voor `https://login.microsoft.com` met de volgende parameters in de hoofdtekst:</span><span class="sxs-lookup"><span data-stu-id="52d89-176">To authenticate, send a post request to `https://login.microsoft.com` with the following parameters in the body:</span></span>

* <span data-ttu-id="52d89-177">grant_type: '**client_credentials**'</span><span class="sxs-lookup"><span data-stu-id="52d89-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="52d89-178">resource: '**https://graph.microsoft.com**'</span><span class="sxs-lookup"><span data-stu-id="52d89-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="52d89-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="52d89-179">client_id: <your client ID></span></span>
* <span data-ttu-id="52d89-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="52d89-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="52d89-181">U moet waarden opgeven voor de **client_id** en de **client_secret** parameter.</span><span class="sxs-lookup"><span data-stu-id="52d89-181">You need to provide values for the **client_id** and the **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="52d89-182">Als dit lukt, retourneert deze geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="52d89-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="52d89-183">Voor het aanroepen van de API maakt u een header met de volgende parameter:</span><span class="sxs-lookup"><span data-stu-id="52d89-183">To call the API, create a header with the following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="52d89-184">Bij de verificatie, vindt u het type token en het toegangstoken in het resulterende token.</span><span class="sxs-lookup"><span data-stu-id="52d89-184">When authenticating, you can find the token type and access token in the returned token.</span></span>

<span data-ttu-id="52d89-185">Deze header als een aanvraag verzenden naar de volgende API-URL:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="52d89-185">Send this header as a request to the following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="52d89-186">Het antwoord, is als dit lukt, een verzameling van identiteit risico's en bijbehorende gegevens in de OData-JSON-indeling, die kan worden geparseerd en verwerkt als naar eigen inzicht.</span><span class="sxs-lookup"><span data-stu-id="52d89-186">The response, if successful, is a collection of identity risk events and associated data in the OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="52d89-187">Hier volgt een voorbeeld van code voor verificatie en het aanroepen van de API met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="52d89-187">Here’s sample code for authenticating and calling the API using Powershell.</span></span>  
<span data-ttu-id="52d89-188">Alleen toe te voegen uw client-ID sleutel en tenant-domein.</span><span class="sxs-lookup"><span data-stu-id="52d89-188">Just add your client ID, key, and tenant domain.</span></span>

    $ClientID       = "<your client ID here>"        # Should be a ~36 hex character string; insert your info here
    $ClientSecret   = "<your client secret here>"    # Should be a ~44 character string; insert your info here
    $tenantdomain   = "<your tenant domain here>"    # For example, contoso.onmicrosoft.com

    $loginURL       = "https://login.microsoft.com"
    $resource       = "https://graph.microsoft.com"

    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    Write-Output $oauth

    if ($oauth.access_token -ne $null) {
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

        $url = "https://graph.microsoft.com/beta/identityRiskEvents"
        Write-Output $url

        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)

        foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
            Write-Output $event
        }

    } else {
        Write-Host "ERROR: No Access Token"
    } 


## <a name="next-steps"></a><span data-ttu-id="52d89-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="52d89-189">Next steps</span></span>
<span data-ttu-id="52d89-190">Gefeliciteerd, u uw eerste aanroep naar Microsoft Graph zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="52d89-190">Congratulations, you just made your first call to Microsoft Graph!</span></span>  
<span data-ttu-id="52d89-191">U kunt nu query identiteit risico's en de gegevens echter naar eigen inzicht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="52d89-191">Now you can query identity risk events and use the data however you see fit.</span></span>

<span data-ttu-id="52d89-192">Bekijk voor meer informatie over Microsoft Graph en het ontwikkelen van toepassingen met behulp van de Graph API de [documentatie](https://graph.microsoft.io/docs) en nog veel meer op de [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="52d89-192">To learn more about Microsoft Graph and how to build applications using the Graph API, check out the [documentation](https://graph.microsoft.io/docs) and much more on the [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="52d89-193">Zorg er ook bladwijzer voor de [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) pagina met een lijst met alle van de identiteit beveiliging beschikbare API's in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="52d89-193">Also, make sure to bookmark the [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of the Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="52d89-194">Als er nieuwe manieren om te werken met Identity Protection via API toevoegt, ziet u ze op die pagina.</span><span class="sxs-lookup"><span data-stu-id="52d89-194">As we add new ways to work with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="52d89-195">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="52d89-195">Additional resources</span></span>
* [<span data-ttu-id="52d89-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="52d89-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="52d89-197">Typen risicogebeurtenissen die worden gedetecteerd door Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="52d89-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="52d89-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="52d89-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="52d89-199">Overzicht van Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="52d89-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="52d89-200">Azure AD Identity Protection Service hoofdmap</span><span class="sxs-lookup"><span data-stu-id="52d89-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)


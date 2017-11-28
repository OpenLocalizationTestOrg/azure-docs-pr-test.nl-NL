---
title: 'aaaGet de slag met Azure Active Directory: Identity Protection en Microsoft Graph | Microsoft Docs'
description: Biedt een inleiding tooquery Microsoft Graph voor een lijst met risico's en bijbehorende gegevens van Azure Active Directory.
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
ms.openlocfilehash: 75b8b7629a0120d8101f6fde0d9163122503d276
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a><span data-ttu-id="921c3-104">Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="921c3-104">Get started with Azure Active Directory Identity Protection and Microsoft Graph</span></span>
<span data-ttu-id="921c3-105">Microsoft Graph is Hallo Microsoft unified API-eindpunt en thuis Hallo van [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) API's.</span><span class="sxs-lookup"><span data-stu-id="921c3-105">Microsoft Graph is hello Microsoft unified API endpoint and hello home of [Azure Active Directory Identity Protection](active-directory-identityprotection.md) APIs.</span></span> <span data-ttu-id="921c3-106">eerste Hallo-API, **identityRiskEvents**, kunt u Microsoft Graph tooquery voor een lijst van [bestaat de kans dat gebeurtenissen](active-directory-identityprotection-risk-events-types.md) en informatie die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="921c3-106">hello first API, **identityRiskEvents**, allows you tooquery Microsoft Graph for a list of [risk events](active-directory-identityprotection-risk-events-types.md) and associated information.</span></span> <span data-ttu-id="921c3-107">In dit artikel helpt u op weg met het opvragen van deze API.</span><span class="sxs-lookup"><span data-stu-id="921c3-107">This article gets you started querying this API.</span></span> <span data-ttu-id="921c3-108">Zie voor een gedetailleerde inleiding, de volledige documentatie en de toegang toohello grafiek Explorer Hallo [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="921c3-108">For an in-depth introduction, full documentation, and access toohello Graph Explorer, see hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="921c3-109">Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="921c3-109">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span>

<span data-ttu-id="921c3-110">Er zijn drie stappen tooaccessing Identity Protection gegevens via Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="921c3-110">There are three steps tooaccessing Identity Protection data through Microsoft Graph:</span></span>

1. <span data-ttu-id="921c3-111">Toevoegen van een toepassing met een clientgeheim.</span><span class="sxs-lookup"><span data-stu-id="921c3-111">Add an application with a client secret.</span></span> 
2. <span data-ttu-id="921c3-112">Gebruik dit geheim en enkele andere stukjes informatie tooauthenticate tooMicrosoft grafiek, waarbij er geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="921c3-112">Use this secret and a few other pieces of information tooauthenticate tooMicrosoft Graph, where you receive an authentication token.</span></span> 
3. <span data-ttu-id="921c3-113">Gebruik dit token toomake aanvragen toohello API-eindpunt en terughalen van gegevens voor de beveiliging van de identiteit.</span><span class="sxs-lookup"><span data-stu-id="921c3-113">Use this token toomake requests toohello API endpoint and get Identity Protection data back.</span></span>

<span data-ttu-id="921c3-114">Voordat u begint, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="921c3-114">Before you get started, you’ll need:</span></span>

* <span data-ttu-id="921c3-115">Administrator-bevoegdheden toocreate Hallo toepassing in Azure AD</span><span class="sxs-lookup"><span data-stu-id="921c3-115">Administrator privileges toocreate hello application in Azure AD</span></span>
* <span data-ttu-id="921c3-116">Hallo-naam van uw tenant-domein (bijvoorbeeld: contoso.onmicrosoft.com)</span><span class="sxs-lookup"><span data-stu-id="921c3-116">hello name of your tenant's domain (for example, contoso.onmicrosoft.com)</span></span>

## <a name="add-an-application-with-a-client-secret"></a><span data-ttu-id="921c3-117">Een toepassing met een clientgeheim toevoegen</span><span class="sxs-lookup"><span data-stu-id="921c3-117">Add an application with a client secret</span></span>
1. <span data-ttu-id="921c3-118">[Meld u aan](https://manage.windowsazure.com) tooyour klassieke Azure-portal als beheerder.</span><span class="sxs-lookup"><span data-stu-id="921c3-118">[Sign in](https://manage.windowsazure.com) tooyour Azure classic portal as an administrator.</span></span> 
2. <span data-ttu-id="921c3-119">Klik op op Hallo navigatiedeelvenster links op **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="921c3-119">On on hello left navigation pane, click **Active Directory**.</span></span> 
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. <span data-ttu-id="921c3-121">Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.</span><span class="sxs-lookup"><span data-stu-id="921c3-121">From hello **Directory** list, select hello directory for which you want tooenable directory integration.</span></span>
4. <span data-ttu-id="921c3-122">Klik in het menu bovenaan Hallo Hallo **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="921c3-122">In hello menu on hello top, click **Applications**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. <span data-ttu-id="921c3-124">Klik op **toevoegen** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="921c3-124">Click **Add** at hello bottom of hello page.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. <span data-ttu-id="921c3-126">Op Hallo **wat wilt u wilt dat toodo** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="921c3-126">On hello **What do you want toodo** dialog, click **Add an application my organization is developing**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. <span data-ttu-id="921c3-128">Op Hallo **Vertel ons over uw toepassing** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="921c3-128">On hello **Tell us about your application** dialog, perform hello following steps:</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    <span data-ttu-id="921c3-130">a.</span><span class="sxs-lookup"><span data-stu-id="921c3-130">a.</span></span> <span data-ttu-id="921c3-131">In Hallo **naam** textbox, typ een naam voor uw toepassing (bijvoorbeeld: AADIP risico gebeurtenis API toepassing).</span><span class="sxs-lookup"><span data-stu-id="921c3-131">In hello **Name** textbox, type a name for your application (e.g.: AADIP Risk Event API Application).</span></span>
   
    <span data-ttu-id="921c3-132">b.</span><span class="sxs-lookup"><span data-stu-id="921c3-132">b.</span></span> <span data-ttu-id="921c3-133">Als **Type**, selecteer **webtoepassing en / of Web-API**.</span><span class="sxs-lookup"><span data-stu-id="921c3-133">As **Type**, select **Web Application And / Or Web API**.</span></span>
   
    <span data-ttu-id="921c3-134">c.</span><span class="sxs-lookup"><span data-stu-id="921c3-134">c.</span></span> <span data-ttu-id="921c3-135">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="921c3-135">Click **Next**.</span></span>
8. <span data-ttu-id="921c3-136">Op Hallo **App-eigenschappen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="921c3-136">On hello **App properties** dialog, perform hello following steps:</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    <span data-ttu-id="921c3-138">a.</span><span class="sxs-lookup"><span data-stu-id="921c3-138">a.</span></span> <span data-ttu-id="921c3-139">In Hallo **aanmeldings-URL** textbox type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="921c3-139">In hello **Sign-On URL** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="921c3-140">b.</span><span class="sxs-lookup"><span data-stu-id="921c3-140">b.</span></span> <span data-ttu-id="921c3-141">In Hallo **App ID URI** textbox type `http://localhost`.</span><span class="sxs-lookup"><span data-stu-id="921c3-141">In hello **App ID URI** textbox, type `http://localhost`.</span></span>
   
    <span data-ttu-id="921c3-142">c.</span><span class="sxs-lookup"><span data-stu-id="921c3-142">c.</span></span> <span data-ttu-id="921c3-143">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="921c3-143">Click **Complete**.</span></span>

<span data-ttu-id="921c3-144">U kunt nu uw toepassing configureren.</span><span class="sxs-lookup"><span data-stu-id="921c3-144">Your can now configure your application.</span></span>

![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a><span data-ttu-id="921c3-146">Uw toepassing machtiging toouse Hallo API verlenen</span><span class="sxs-lookup"><span data-stu-id="921c3-146">Grant your application permission toouse hello API</span></span>
1. <span data-ttu-id="921c3-147">Klik op de pagina van uw toepassing in het menu bovenaan Hallo Hallo op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="921c3-147">On your application's page, in hello menu on hello top, click **Configure**.</span></span> 
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. <span data-ttu-id="921c3-149">In Hallo **machtigingen tooother toepassingen** sectie, klikt u op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="921c3-149">In hello **permissions tooother applications** section, click **Add application**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. <span data-ttu-id="921c3-151">Op Hallo **machtigingen tooother toepassingen** dialoogvenster Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="921c3-151">On hello **permissions tooother applications** dialog, perform hello following steps:</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    <span data-ttu-id="921c3-153">a.</span><span class="sxs-lookup"><span data-stu-id="921c3-153">a.</span></span> <span data-ttu-id="921c3-154">Selecteer **Microsoft Graph**.</span><span class="sxs-lookup"><span data-stu-id="921c3-154">Select **Microsoft Graph**.</span></span>
   
    <span data-ttu-id="921c3-155">b.</span><span class="sxs-lookup"><span data-stu-id="921c3-155">b.</span></span> <span data-ttu-id="921c3-156">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="921c3-156">Click **Complete**.</span></span>
4. <span data-ttu-id="921c3-157">Klik op **Toepassingsmachtigingen: 0**, en selecteer vervolgens **lezen van alle gegevens van identiteit risico gebeurtenis**.</span><span class="sxs-lookup"><span data-stu-id="921c3-157">Click **Application Permissions: 0**, and then select **Read all identity risk event information**.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. <span data-ttu-id="921c3-159">Klik op **opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="921c3-159">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a><span data-ttu-id="921c3-161">Een toegangssleutel opvragen</span><span class="sxs-lookup"><span data-stu-id="921c3-161">Get an access key</span></span>
1. <span data-ttu-id="921c3-162">Op de pagina van uw toepassing, in Hallo **sleutels** sectie, selecteert u 1 jaar als duur.</span><span class="sxs-lookup"><span data-stu-id="921c3-162">On your application's page, in hello **keys** section, select 1 year as duration.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. <span data-ttu-id="921c3-164">Klik op **opslaan** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="921c3-164">Click **Save** at hello bottom of hello page.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. <span data-ttu-id="921c3-166">Hallo-waarde van de zojuist gemaakte sleutel kopiëren in Hallo sleutels sectie en plak deze in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="921c3-166">in hello keys section, copy hello value of your newly created key, and then paste it into a safe location.</span></span>
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > <span data-ttu-id="921c3-168">Als u deze sleutel kwijtraakt, wordt u tooreturn toothis sectie en maak een nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="921c3-168">If you lose this key, you will have tooreturn toothis section and create a new key.</span></span> <span data-ttu-id="921c3-169">Een geheim voor deze sleutel behouden: iedereen die deze heeft toegang tot uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="921c3-169">Keep this key a secret: anyone who has it can access your data.</span></span>
   > 
   > 
4. <span data-ttu-id="921c3-170">In Hallo **eigenschappen** sectie, kopie Hallo **Client-ID**, en plak deze in een veilige locatie.</span><span class="sxs-lookup"><span data-stu-id="921c3-170">In hello **properties** section, copy hello **Client ID**, and then paste it into a safe location.</span></span> 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a><span data-ttu-id="921c3-171">TooMicrosoft grafiek en query Hallo identiteit risico gebeurtenissen API verifiëren</span><span class="sxs-lookup"><span data-stu-id="921c3-171">Authenticate tooMicrosoft Graph and query hello Identity Risk Events API</span></span>
<span data-ttu-id="921c3-172">Op dit moment dat u hebt:</span><span class="sxs-lookup"><span data-stu-id="921c3-172">At this point, you should have:</span></span>

* <span data-ttu-id="921c3-173">Hallo client-ID u hierboven hebt gekopieerd</span><span class="sxs-lookup"><span data-stu-id="921c3-173">hello client ID you copied above</span></span>
* <span data-ttu-id="921c3-174">Hallo-sleutel die u hierboven hebt gekopieerd</span><span class="sxs-lookup"><span data-stu-id="921c3-174">hello key you copied above</span></span>
* <span data-ttu-id="921c3-175">Hallo-naam van uw tenant-domein</span><span class="sxs-lookup"><span data-stu-id="921c3-175">hello name of your tenant's domain</span></span>

<span data-ttu-id="921c3-176">tooauthenticate, verzenden een post-aanvragen te`https://login.microsoft.com` Hello parameters in de hoofdtekst van het Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="921c3-176">tooauthenticate, send a post request too`https://login.microsoft.com` with hello following parameters in hello body:</span></span>

* <span data-ttu-id="921c3-177">grant_type: '**client_credentials**'</span><span class="sxs-lookup"><span data-stu-id="921c3-177">grant_type: “**client_credentials**”</span></span>
* <span data-ttu-id="921c3-178">resource: '**https://graph.microsoft.com**'</span><span class="sxs-lookup"><span data-stu-id="921c3-178">resource: “**https://graph.microsoft.com**”</span></span>
* <span data-ttu-id="921c3-179">client_id:<your client ID></span><span class="sxs-lookup"><span data-stu-id="921c3-179">client_id: <your client ID></span></span>
* <span data-ttu-id="921c3-180">client_secret:<your key></span><span class="sxs-lookup"><span data-stu-id="921c3-180">client_secret: <your key></span></span>

> [!NOTE]
> <span data-ttu-id="921c3-181">Hebt u tooprovide waarden voor Hallo **client_id** en Hallo **client_secret** parameter.</span><span class="sxs-lookup"><span data-stu-id="921c3-181">You need tooprovide values for hello **client_id** and hello **client_secret** parameter.</span></span>
> 
> 

<span data-ttu-id="921c3-182">Als dit lukt, retourneert deze geen verificatietoken.</span><span class="sxs-lookup"><span data-stu-id="921c3-182">If successful, this returns an authentication token.</span></span>  
<span data-ttu-id="921c3-183">een header toocall Hallo-API maken met de volgende parameter Hallo:</span><span class="sxs-lookup"><span data-stu-id="921c3-183">toocall hello API, create a header with hello following parameter:</span></span>

    `Authorization`=”<token_type> <access_token>"


<span data-ttu-id="921c3-184">Bij de verificatie, vindt u Hallo tokentype en toegangstoken in Hallo heeft een token geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="921c3-184">When authenticating, you can find hello token type and access token in hello returned token.</span></span>

<span data-ttu-id="921c3-185">Deze header verzenden als een aanvraag toohello URL van de API te volgen:`https://graph.microsoft.com/beta/identityRiskEvents`</span><span class="sxs-lookup"><span data-stu-id="921c3-185">Send this header as a request toohello following API URL: `https://graph.microsoft.com/beta/identityRiskEvents`</span></span>

<span data-ttu-id="921c3-186">Hallo-antwoord als dit lukt, is een verzameling van identiteit risicogebeurtenissen en gegevens in Hallo OData-JSON-indeling, die kan worden geparseerd en verwerkt als naar eigen inzicht die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="921c3-186">hello response, if successful, is a collection of identity risk events and associated data in hello OData JSON format, which can be parsed and handled as see fit.</span></span>

<span data-ttu-id="921c3-187">Hier volgt een voorbeeld van code voor verificatie en het aanroepen van Hallo-API met behulp van Powershell.</span><span class="sxs-lookup"><span data-stu-id="921c3-187">Here’s sample code for authenticating and calling hello API using Powershell.</span></span>  
<span data-ttu-id="921c3-188">Alleen toe te voegen uw client-ID sleutel en tenant-domein.</span><span class="sxs-lookup"><span data-stu-id="921c3-188">Just add your client ID, key, and tenant domain.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="921c3-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="921c3-189">Next steps</span></span>
<span data-ttu-id="921c3-190">Gefeliciteerd, u uw eerste aanroep tooMicrosoft grafiek zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="921c3-190">Congratulations, you just made your first call tooMicrosoft Graph!</span></span>  
<span data-ttu-id="921c3-191">U kunt nu query identiteit risico's en Hallo gegevens gebruiken, maar naar eigen inzicht.</span><span class="sxs-lookup"><span data-stu-id="921c3-191">Now you can query identity risk events and use hello data however you see fit.</span></span>

<span data-ttu-id="921c3-192">toolearn meer informatie over Microsoft Graph en hoe toobuild toepassingen die gebruikmaken van Graph API Hallo uitchecken Hallo [documentatie](https://graph.microsoft.io/docs) en nog veel meer op Hallo [Microsoft Graph site](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="921c3-192">toolearn more about Microsoft Graph and how toobuild applications using hello Graph API, check out hello [documentation](https://graph.microsoft.io/docs) and much more on hello [Microsoft Graph site](https://graph.microsoft.io/).</span></span> <span data-ttu-id="921c3-193">Zorg ervoor dat toobookmark Hallo ook [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) pagina met een lijst met alle Hallo Identity Protection API's beschikbaar zijn in de grafiek.</span><span class="sxs-lookup"><span data-stu-id="921c3-193">Also, make sure toobookmark hello [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) page that lists all of hello Identity Protection APIs available in Graph.</span></span> <span data-ttu-id="921c3-194">Als er nieuwe manieren toowork met Identity Protection via API toevoegt, ziet u ze op die pagina.</span><span class="sxs-lookup"><span data-stu-id="921c3-194">As we add new ways toowork with Identity Protection via API, you’ll see them on that page.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="921c3-195">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="921c3-195">Additional resources</span></span>
* [<span data-ttu-id="921c3-196">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="921c3-196">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
* [<span data-ttu-id="921c3-197">Typen risicogebeurtenissen die worden gedetecteerd door Azure Active Directory: Identity Protection</span><span class="sxs-lookup"><span data-stu-id="921c3-197">Types of risk events detected by Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection-risk-events-types.md)
* [<span data-ttu-id="921c3-198">Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="921c3-198">Microsoft Graph</span></span>](https://graph.microsoft.io/)
* [<span data-ttu-id="921c3-199">Overzicht van Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="921c3-199">Overview of Microsoft Graph</span></span>](https://graph.microsoft.io/docs)
* [<span data-ttu-id="921c3-200">Azure AD Identity Protection Service hoofdmap</span><span class="sxs-lookup"><span data-stu-id="921c3-200">Azure AD Identity Protection Service Root</span></span>](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)


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
# <a name="get-started-with-azure-active-directory-identity-protection-and-microsoft-graph"></a>Aan de slag met Azure Active Directory: Identity Protection en Microsoft Graph
Microsoft Graph is Hallo Microsoft unified API-eindpunt en thuis Hallo van [Azure Active Directory: Identity Protection](active-directory-identityprotection.md) API's. eerste Hallo-API, **identityRiskEvents**, kunt u Microsoft Graph tooquery voor een lijst van [bestaat de kans dat gebeurtenissen](active-directory-identityprotection-risk-events-types.md) en informatie die is gekoppeld. In dit artikel helpt u op weg met het opvragen van deze API. Zie voor een gedetailleerde inleiding, de volledige documentatie en de toegang toohello grafiek Explorer Hallo [Microsoft Graph site](https://graph.microsoft.io/).

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.

Er zijn drie stappen tooaccessing Identity Protection gegevens via Microsoft Graph:

1. Toevoegen van een toepassing met een clientgeheim. 
2. Gebruik dit geheim en enkele andere stukjes informatie tooauthenticate tooMicrosoft grafiek, waarbij er geen verificatietoken. 
3. Gebruik dit token toomake aanvragen toohello API-eindpunt en terughalen van gegevens voor de beveiliging van de identiteit.

Voordat u begint, hebt u nodig:

* Administrator-bevoegdheden toocreate Hallo toepassing in Azure AD
* Hallo-naam van uw tenant-domein (bijvoorbeeld: contoso.onmicrosoft.com)

## <a name="add-an-application-with-a-client-secret"></a>Een toepassing met een clientgeheim toevoegen
1. [Meld u aan](https://manage.windowsazure.com) tooyour klassieke Azure-portal als beheerder. 
2. Klik op op Hallo navigatiedeelvenster links op **Active Directory**. 
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_01.png)
3. Van Hallo **Directory** lijst, selecteer Hallo map waarvoor u tooenable Active directory-integratie.
4. Klik in het menu bovenaan Hallo Hallo **toepassingen**.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_02.png)
5. Klik op **toevoegen** Hallo Hallo pagina onderaan in.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_03.png)
6. Op Hallo **wat wilt u wilt dat toodo** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_04.png)
7. Op Hallo **Vertel ons over uw toepassing** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_05.png)
   
    a. In Hallo **naam** textbox, typ een naam voor uw toepassing (bijvoorbeeld: AADIP risico gebeurtenis API toepassing).
   
    b. Als **Type**, selecteer **webtoepassing en / of Web-API**.
   
    c. Klik op **Volgende**.
8. Op Hallo **App-eigenschappen** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_06.png)
   
    a. In Hallo **aanmeldings-URL** textbox type `http://localhost`.
   
    b. In Hallo **App ID URI** textbox type `http://localhost`.
   
    c. Klik op **Voltooien**.

U kunt nu uw toepassing configureren.

![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_07.png)

## <a name="grant-your-application-permission-toouse-hello-api"></a>Uw toepassing machtiging toouse Hallo API verlenen
1. Klik op de pagina van uw toepassing in het menu bovenaan Hallo Hallo op **configureren**. 
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_08.png)
2. In Hallo **machtigingen tooother toepassingen** sectie, klikt u op **toepassing toevoegen**.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_09.png)
3. Op Hallo **machtigingen tooother toepassingen** dialoogvenster Hallo volgende stappen uit te voeren:
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_10.png)
   
    a. Selecteer **Microsoft Graph**.
   
    b. Klik op **Voltooien**.
4. Klik op **Toepassingsmachtigingen: 0**, en selecteer vervolgens **lezen van alle gegevens van identiteit risico gebeurtenis**.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_11.png)
5. Klik op **opslaan** Hallo Hallo pagina onderaan in.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)

## <a name="get-an-access-key"></a>Een toegangssleutel opvragen
1. Op de pagina van uw toepassing, in Hallo **sleutels** sectie, selecteert u 1 jaar als duur.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_13.png)
2. Klik op **opslaan** Hallo Hallo pagina onderaan in.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_12.png)
3. Hallo-waarde van de zojuist gemaakte sleutel kopiëren in Hallo sleutels sectie en plak deze in een veilige locatie.
   
    ![Maken van een toepassing](./media/active-directory-identityprotection-graph-getting-started/tutorial_general_14.png)
   
   > [!NOTE]
   > Als u deze sleutel kwijtraakt, wordt u tooreturn toothis sectie en maak een nieuwe sleutel. Een geheim voor deze sleutel behouden: iedereen die deze heeft toegang tot uw gegevens.
   > 
   > 
4. In Hallo **eigenschappen** sectie, kopie Hallo **Client-ID**, en plak deze in een veilige locatie. 

## <a name="authenticate-toomicrosoft-graph-and-query-hello-identity-risk-events-api"></a>TooMicrosoft grafiek en query Hallo identiteit risico gebeurtenissen API verifiëren
Op dit moment dat u hebt:

* Hallo client-ID u hierboven hebt gekopieerd
* Hallo-sleutel die u hierboven hebt gekopieerd
* Hallo-naam van uw tenant-domein

tooauthenticate, verzenden een post-aanvragen te`https://login.microsoft.com` Hello parameters in de hoofdtekst van het Hallo te volgen:

* grant_type: '**client_credentials**'
* resource: '**https://graph.microsoft.com**'
* client_id:<your client ID>
* client_secret:<your key>

> [!NOTE]
> Hebt u tooprovide waarden voor Hallo **client_id** en Hallo **client_secret** parameter.
> 
> 

Als dit lukt, retourneert deze geen verificatietoken.  
een header toocall Hallo-API maken met de volgende parameter Hallo:

    `Authorization`=”<token_type> <access_token>"


Bij de verificatie, vindt u Hallo tokentype en toegangstoken in Hallo heeft een token geretourneerd.

Deze header verzenden als een aanvraag toohello URL van de API te volgen:`https://graph.microsoft.com/beta/identityRiskEvents`

Hallo-antwoord als dit lukt, is een verzameling van identiteit risicogebeurtenissen en gegevens in Hallo OData-JSON-indeling, die kan worden geparseerd en verwerkt als naar eigen inzicht die zijn gekoppeld.

Hier volgt een voorbeeld van code voor verificatie en het aanroepen van Hallo-API met behulp van Powershell.  
Alleen toe te voegen uw client-ID sleutel en tenant-domein.

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


## <a name="next-steps"></a>Volgende stappen
Gefeliciteerd, u uw eerste aanroep tooMicrosoft grafiek zojuist hebt gemaakt.  
U kunt nu query identiteit risico's en Hallo gegevens gebruiken, maar naar eigen inzicht.

toolearn meer informatie over Microsoft Graph en hoe toobuild toepassingen die gebruikmaken van Graph API Hallo uitchecken Hallo [documentatie](https://graph.microsoft.io/docs) en nog veel meer op Hallo [Microsoft Graph site](https://graph.microsoft.io/). Zorg ervoor dat toobookmark Hallo ook [Azure AD Identity Protection API](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root) pagina met een lijst met alle Hallo Identity Protection API's beschikbaar zijn in de grafiek. Als er nieuwe manieren toowork met Identity Protection via API toevoegt, ziet u ze op die pagina.

## <a name="additional-resources"></a>Aanvullende bronnen
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)
* [Typen risicogebeurtenissen die worden gedetecteerd door Azure Active Directory: Identity Protection](active-directory-identityprotection-risk-events-types.md)
* [Microsoft Graph](https://graph.microsoft.io/)
* [Overzicht van Microsoft Graph](https://graph.microsoft.io/docs)
* [Azure AD Identity Protection Service hoofdmap](https://graph.microsoft.io/docs/api-reference/beta/resources/identityprotection_root)


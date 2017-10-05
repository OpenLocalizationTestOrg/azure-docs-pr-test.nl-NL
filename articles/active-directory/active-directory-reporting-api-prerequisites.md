---
title: Vereisten voor toegang tot de Azure AD rapportage-API. | Microsoft Docs
description: Meer informatie over de vereisten voor toegang tot de Azure AD rapportage-API
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: 6e409fc56b77f37dac7f37382e664c577666ad4d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="prerequisites-to-access-the-azure-ad-reporting-api"></a>Vereisten voor toegang tot de Azure AD rapportage-API
De [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) u programmatische toegang bieden tot de gegevens via een set op basis van REST-API's. U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.

De rapportage-API maakt gebruikt [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) toegang verlenen aan de web-API's. 

Als u met het voorbereiden van uw toegang tot de rapportage-API, moet u het volgende doen:

1. Een toepassing in uw Azure AD-tenant maken 
2. Verleen de juiste toepassing worden machtigingen voor toegang tot de Azure AD-gegevens
3. Verzamelen van configuratie-instellingen van uw directory

Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Een Azure AD-toepassing maken
Voor het configureren van uw directory voor toegang tot de Azure AD rapportage-API, moet u zich aanmeldt bij de klassieke Azure portal met een administrator-account voor Azure-abonnement is ook lid zijn van de rol globale beheerder directory in uw Azure AD-tenant.

> [!IMPORTANT]
> Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat de toepassing-ID/geheim referenties veilig te houden.
> 
> 

1. In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van de **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan op **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Klik op de balk onderaan **toevoegen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Op de **wat wilt u doen?** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**. 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Op de **Vertel ons over uw toepassing** dialoogvenster de volgende stappen uitvoeren: 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. In de **naam** textbox, typ een naam (bijvoorbeeld: de toepassing van rapportage-API).
   
    b. Selecteer **webtoepassing en/of web-API**.
   
    c. Klik op **Volgende**.
7. Op de **App-eigenschappen** dialoogvenster de volgende stappen uitvoeren: 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. In de **aanmeldings-URL** textbox type `https://localhost`.
   
    b. In de **App ID URI** textbox type ```https://localhost/ReportingApiApp```.
   
    c. Klik op **Voltooien**.

## <a name="grant-your-application-permission-to-use-the-api"></a>Uw toepassing toestemming de API gebruiken
1. In de [klassieke Azure-portal](https://manage.windowsazure.com/), klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van de **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan op **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png)
4. Selecteer uw nieuwe toepassing in de lijst met toepassingen.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. Klik in het menu bovenaan op **configureren**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. In de **machtigingen voor andere toepassingen** sectie voor de **Azure Active Directory** resource, klikt u op de **Toepassingsmachtigingen** vervolgkeuzelijst en selecteer vervolgens **mapgegevens lezen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/09.png)
7. Klik op de balk onderaan **opslaan**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Verzamelen van configuratie-instellingen van uw directory
Deze sectie wordt beschreven hoe u de volgende instellingen van uw directory ophalen:

* Domeinnaam
* Client-ID
* Clientgeheim

U moet deze waarden bij het configureren van de rapportage-API aanroepen. 

### <a name="get-your-domain-name"></a>Uw domeinnaam ophalen
1. In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van de **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan op **domeinen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/11.png) 
4. In de **domeinnaam** kolom, kopieert u de domeinnaam van uw.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-the-applications-client-id"></a>Client-ID van de toepassing ophalen
1. In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van de **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan op **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Selecteer uw nieuwe toepassing in de lijst met toepassingen.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. Klik in het menu bovenaan op **configureren**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. Kopieer uw **Client-ID**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-the-applications-client-secret"></a>Clientgeheim van de toepassing ophalen
Als u uw toepassing clientgeheim, moet u een nieuwe sleutel maken en opslaan van de waarde bij het opslaan van de nieuwe sleutel, omdat het is niet mogelijk is deze waarde later meer ophalen.

1. In de [klassieke Azure-portal](https://manage.windowsazure.com), klik op het navigatiedeelvenster links **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van de **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan op **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Selecteer uw nieuwe toepassing in de lijst met toepassingen.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. Klik in het menu bovenaan op **configureren**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. In de **sleutels** sectie, voert u de volgende stappen uit: 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. In de duur van de lijst, selecteert u een duur
   
    b. Klik op de balk onderaan **opslaan**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Kopieer de waarde van de sleutel.

## <a name="next-steps"></a>Volgende stappen
* Wilt u de toegang tot de gegevens van de Azure AD rapportage-API op een programmatische manier? Bekijk [aan de slag met Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).
* Als u meer informatie over Azure Active Directory-rapportage wilt, raadpleegt u de [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).  


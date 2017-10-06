---
title: aaaPrerequisites tooaccess hello Azure AD rapportage-API. | Microsoft Docs
description: Meer informatie over Hallo vereisten tooaccess hello Azure AD reporting API
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
ms.openlocfilehash: e9d7ceaedb07d18fbd75b70d68b5cfbebc756c36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Vereisten tooaccess hello Azure AD rapportage-API
Hallo [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) voorzien van toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's. U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.

rapportage-API maakt gebruikt Hallo [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toegang toohello web-API's. 

tooprepare uw toegang toohello rapportage-API, moet u:

1. Een toepassing in uw Azure AD-tenant maken 
2. Verleen Hallo toepassing gemachtigd tooaccess hello Azure AD-gegevens
3. Verzamelen van configuratie-instellingen van uw directory

Voor vragen, problemen of feedback, neem contact op met [AAD rapportage Help](mailto:aadreportinghelp@microsoft.com).

## <a name="create-an-azure-ad-application"></a>Een Azure AD-toepassing maken
tooconfigure uw directory tooaccess hello Azure AD reporting API, moet u zich aanmeldt toohello klassieke Azure-portal met een administrator-account voor Azure-abonnement is ook lid zijn van de rol van algemeen beheerder directory Hallo in uw Azure AD-tenant.

> [!IMPORTANT]
> Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat tookeep Hallo van de toepassing-ID/geheim referenties veilig.
> 
> 

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van Hallo **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan Hallo Hallo **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Klik op de balk onderaan hello, **toevoegen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/03.png) 
5. Op Hallo **wat wilt u wilt dat toodo?** dialoogvenster, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**. 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/04.png) 
6. Op Hallo **Vertel ons over uw toepassing** dialoogvenster Hallo volgende stappen uit te voeren: 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/05.png) 
   
    a. In Hallo **naam** textbox, typ een naam (bijvoorbeeld: de toepassing van rapportage-API).
   
    b. Selecteer **webtoepassing en/of web-API**.
   
    c. Klik op **Volgende**.
7. Op Hallo **App-eigenschappen** dialoogvenster Hallo volgende stappen uit te voeren: 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/06.png) 
   
    a. In Hallo **aanmeldings-URL** textbox type `https://localhost`.
   
    b. In Hallo **App ID URI** textbox type ```https://localhost/ReportingApiApp```.
   
    c. Klik op **Voltooien**.

## <a name="grant-your-application-permission-toouse-hello-api"></a>Uw toepassing machtiging toouse Hallo API verlenen
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com/), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van Hallo **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan Hallo Hallo **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png)
4. Selecteer in de lijst met toepassingen van Hallo, uw nieuwe toepassing.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. Klik in het menu bovenaan Hallo Hallo **configureren**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. In Hallo **machtigingen tooother toepassingen** sectie voor Hallo **Azure Active Directory** resource, klikt u op Hallo **Toepassingsmachtigingen** vervolgkeuzelijst, en vervolgens Selecteer **mapgegevens lezen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/09.png)
7. Klik op de balk onderaan hello, **opslaan**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)

## <a name="gather-configuration-settings-from-your-directory"></a>Verzamelen van configuratie-instellingen van uw directory
Deze sectie leest u hoe tooget Hallo instellingen van uw directory te volgen:

* Domeinnaam
* Client-ID
* Clientgeheim

U moet deze waarden bij het configureren van rapportage toohello-API aanroepen. 

### <a name="get-your-domain-name"></a>Uw domeinnaam ophalen
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van Hallo **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan Hallo Hallo **domeinen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/11.png) 
4. In Hallo **domeinnaam** kolom, kopieert u de domeinnaam van uw.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/12.png) 

### <a name="get-hello-applications-client-id"></a>Haal client-ID van de toepassing hello
1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van Hallo **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan Hallo Hallo **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Selecteer in de lijst met toepassingen van Hallo, uw nieuwe toepassing.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. Klik in het menu bovenaan Hallo Hallo **configureren**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. Kopieer uw **Client-ID**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/13.png)

### <a name="get-hello-applications-client-secret"></a>Van de toepassing hello clientgeheim ophalen
tooget van uw toepassing client geheime, u moet een nieuwe sleutel toocreate en sla de waarde bij het opslaan van de nieuwe sleutel Hallo omdat het niet mogelijk tooretrieve deze waarde later niet meer.

1. In Hallo [klassieke Azure-portal](https://manage.windowsazure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/01.png) 
2. Van Hallo **active directory** Selecteer uw directory.
3. Klik in het menu bovenaan Hallo Hallo **toepassingen**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/02.png) 
4. Selecteer in de lijst met toepassingen van Hallo, uw nieuwe toepassing.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/07.png)
5. Klik in het menu bovenaan Hallo Hallo **configureren**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/08.png)
6. In Hallo **sleutels** sectie, voert u Hallo stappen te volgen: 
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/14.png)
   
    a. Selecteer een duur in Hallo duur van de lijst.
   
    b. Klik op de balk onderaan hello, **opslaan**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites/10.png)
   
    c. Hallo-sleutelwaarde kopiëren.

## <a name="next-steps"></a>Volgende stappen
* Zou u zoals tooaccess gegevens van Azure AD Hallo Hallo rapportage-API op een programmatische manier? Bekijk [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).
* Als u toofind voor meer informatie over Azure Active Directory-rapportage wilt, Zie Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).  


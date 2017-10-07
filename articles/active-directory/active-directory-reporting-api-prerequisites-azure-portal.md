---
title: aaaPrerequisites tooaccess hello Azure AD reporting API | Microsoft Docs
description: Meer informatie over Hallo vereisten tooaccess hello Azure AD reporting API
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ada19f69-665c-452a-8452-701029bf4252
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: ec28a7530f341dda31268a978754b615c727d66f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="prerequisites-tooaccess-hello-azure-ad-reporting-api"></a>Vereisten tooaccess hello Azure AD rapportage-API

Hallo [Azure AD rapportage-API's](https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-reports-and-events-preview) voorzien van toegang op programmeerniveau toohello gegevens via een set op basis van REST-API's. U kunt deze API's vanuit een groot aantal computertalen en hulpprogramma's aanroepen.

rapportage-API maakt gebruikt Hallo [OAuth](https://msdn.microsoft.com/library/azure/dn645545.aspx) tooauthorize toegang toohello web-API's. 

tooget toohello reporting gegevens benaderen via Hallo API, moet u toohave een van de volgende rollen toegewezen Hallo:

- Beveiliging lezer
- De beheerder beveiliging
- Globale beheerder


tooprepare uw toegang toohello rapportage-API, moet u:

1. Een toepassing registreren 
2. Machtigingen toekennen 
3. Verzamelen van configuratie-instellingen 

Voor vragen, problemen of feedback, neemt u [een ondersteuningsticket bestand](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-troubleshooting-support-howto).

## <a name="register-an-azure-active-directory-application"></a>Een Azure Active Directory-toepassing registreren

U moet tooregister een app, zelfs als u Hallo rapportage-API met een script opent. Hiermee krijgt u een **toepassings-ID**, die is vereist voor een aanroep van de autorisatie en kunnen uw code tooreceive-tokens.

tooconfigure uw directory tooaccess hello Azure AD reporting API, moet u zich aanmeldt toohello Azure-portal met een Azure-beheerdersaccount die ook lid zijn van Hallo **hoofdbeheerder** directory-rol in uw Azure AD-tenant .

> [!IMPORTANT]
> Toepassingen die worden uitgevoerd onder-referenties met bevoegdheden als volgt 'admin' kunnen zeer krachtig zijn, dus zorg ervoor dat tookeep Hallo van de toepassing-ID/geheim referenties veilig.
> 


**tooregister een Azure Active Directory-toepassing:**

1. In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Op Hallo **Azure Active Directory** blade, klikt u op **App registraties**.

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/02.png) 

3. Op Hallo **App registraties** blade in de werkbalk Hallo op Hallo boven, klikt u op **registratie van de nieuwe toepassing**.

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/03.png)

4. Op Hallo **maken** blade Hallo volgende stappen uit te voeren:

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/04.png)

    a. In Hallo **naam** textbox type `Reporting API application`.

    b. Als **toepassingstype**, selecteer **Web-app / API**.

    c. In Hallo **aanmeldings-URL** textbox type `https://localhost`.

    d. Klik op **Create**. 


## <a name="grant-permissions"></a>Machtigingen toekennen 

Hallo-doel van deze stap is toogrant uw toepassing **mapgegevens lezen** machtigingen toohello **Windows Azure Active Directory** API.

![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/16.png)
 

**toogrant uw toepassing machtiging toouse Hallo API:**

1. Op Hallo **App registraties** blade in de lijst met apps van hello, klikt u op **rapportage-API-toepassing**.

2. Op Hallo **rapportage-API-toepassing** blade in de werkbalk Hallo op Hallo boven, klikt u op **instellingen**. 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

3. Op Hallo **instellingen** blade, klikt u op **vereist machtigingen**. 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/06.png)

4. Op Hallo **vereist machtigingen** blade in Hallo **API** lijst, klikt u op **Windows Azure Active Directory**. 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/07.png)

5. Op Hallo **toegang inschakelen** blade Selecteer **mapgegevens lezen**. 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/08.png)

6. Klik in de werkbalk bovenaan Hallo Hallo op **opslaan**.

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/15.png)

## <a name="gather-configuration-settings"></a>Verzamelen van configuratie-instellingen 
Deze sectie leest u hoe tooget Hallo instellingen van uw directory te volgen:

* Domeinnaam
* Client-ID
* Clientgeheim

U moet deze waarden bij het configureren van rapportage toohello-API aanroepen. 

### <a name="get-your-domain-name"></a>Uw domeinnaam ophalen

**tooget uw domeinnaam:**

1. In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Op Hallo **Azure Active Directory** blade, klikt u op **domeinnamen**.

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/09.png) 

3. Uw domeinnaam van de lijst met domeinen Hallo kopiëren.


### <a name="get-your-applications-client-id"></a>Haal client-ID van uw toepassing

**tooget van uw toepassing de client-ID:**

1. In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Op Hallo **App registraties** blade in de lijst met apps van hello, klikt u op **rapportage-API-toepassing**.

3. Op Hallo **rapportage-API-toepassing** blade op Hallo **toepassings-ID**, klikt u op **klikt u op toocopy**.

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/11.png) 



### <a name="get-your-applications-client-secret"></a>Uw toepassing clientgeheim ophalen
tooget van uw toepassing client geheime, u moet een nieuwe sleutel toocreate en sla de waarde bij het opslaan van de nieuwe sleutel Hallo omdat het niet mogelijk tooretrieve deze waarde later niet meer.

**tooget clientgeheim van uw toepassing:**

1. In Hallo [Azure-portal](https://portal.azure.com), op Hallo navigatiedeelvenster links, klikt u op **Active Directory**.
   
    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/01.png) 

2. Op Hallo **App registraties** blade in de lijst met apps van hello, klikt u op **rapportage-API-toepassing**.


3. Op Hallo **rapportage-API-toepassing** blade in de werkbalk Hallo op Hallo boven, klikt u op **instellingen**. 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/05.png)

4. Op Hallo **instellingen** blade in Hallo **APIR toegang** sectie, klikt u op **sleutels**. 

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/12.png)


5. Op Hallo **sleutels** blade Hallo volgende stappen uit te voeren:

    ![Toepassing registreren](./media/active-directory-reporting-api-prerequisites-azure-portal/14.png)

    a. In Hallo **beschrijving** textbox type `Reporting API`.

    b. Als **verloopt**, selecteer **In 2 jaar**.

    c. Klik op **Opslaan**.

    d. Hallo-sleutelwaarde kopiëren.


## <a name="next-steps"></a>Volgende stappen
* Zou u zoals tooaccess gegevens van Azure AD Hallo Hallo rapportage-API op een programmatische manier? Bekijk [aan de slag met Azure Active Directory Reporting API Hallo](active-directory-reporting-api-getting-started.md).
* Als u toofind voor meer informatie over Azure Active Directory-rapportage wilt, Zie Hallo [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).  


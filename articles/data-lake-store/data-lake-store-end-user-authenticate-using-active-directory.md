---
title: 'Verificatie van de eindgebruiker: Data Lake Store met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooachieve eindgebruiker verificatie met Data Lake Store met Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: fd58f4f2d8fc915b8bc51d9e5b040d2cee34047e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Verificatie van de eindgebruiker met Data Lake Store met Azure Active Directory
> [!div class="op_single_selector"]
> * [Verificatie van service-tot-service](data-lake-store-authenticate-using-active-directory.md)
> * [Verificatie van de eindgebruiker](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie. Vóór het ontwerpen van een toepassing die met Azure Data Lake Store of Azure Data Lake Analytics werkt, moet u eerst beslissen hoe u tooauthenticate wilt dat uw toepassing met Azure Active Directory (Azure AD). Hallo twee belangrijkste opties zijn beschikbaar:

* Verificatie van de eindgebruiker (in dit artikel)
* Verificatie van service-tot-service

Deze beide opties leiden in uw toepassing wordt geleverd met een OAuth 2.0-token, dat gekoppelde tooeach verzoek tooAzure Data Lake Store of Azure Data Lake Analytics opgehaald.

Dit artikel vertelt over het maken van een **systeemeigen Azure AD-toepassing voor verificatie van de eindgebruiker**. Zie voor instructies voor de configuratie van Azure AD-toepassing voor verificatie van de service to service [authentication Service-naar-service met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* Uw abonnement-ID. U kunt het ophalen van hello Azure-Portal. Het is bijvoorbeeld beschikbaar vanuit de blade Hallo Data Lake Store-account.
  
    ![Abonnement-ID ophalen](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* De naam van uw Azure AD-domein. U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-Portal. Van Hallo onderstaande schermafbeelding Hallo domeinnaam is **contoso.onmicrosoft.com**, en Hallo GUID tussen vierkante haken is Hallo tenant-ID. 
  
    ![Ophalen van AAD-domein](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Verificatie van de eindgebruiker
Dit is Hallo benadering wordt aanbevolen als u wilt dat een eindgebruiker toolog in tooyour toepassing via Azure AD. Uw toepassing worden kunnen tooaccess Azure-resources met Hallo hetzelfde niveau van toegang als Hallo eindgebruikers die in het logboek geregistreerd. De eindgebruiker moet tooprovide hun referenties periodiek in volgorde voor uw toepassing toomaintain toegang.

Hallo-resultaat van het Hallo eindgebruiker zich aanmeldt met is dat uw toepassing een toegangstoken en een vernieuwingstoken wordt gegeven. Hallo toegangstoken opgehaald gekoppelde tooeach verzoek tooData Lake Store of Data Lake Analytics en het één uur standaard geldig is. Hallo-vernieuwingstoken mag gebruikte tooobtain en een nieuw toegangstoken is geldig voor up tootwo weken standaard als u regelmatig gebruikt. U kunt twee verschillende benaderingen voor eindgebruikers aanmelden.

### <a name="using-hello-oauth-20-pop-up"></a>Met behulp van OAuth 2.0 Hallo pop-upvenster
Uw toepassing kan resulteren in een OAuth 2.0 autorisatie pop-upvenster in welke Hallo eindgebruikers hun referenties kan opgeven. Dit pop-upvenster werkt ook met hello Azure AD tweeledige verificatie (2FA) proces, indien nodig. 

> [!NOTE]
> Deze methode is nog niet ondersteund in hello Azure AD Authentication Library (ADAL) voor Python of Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Rechtstreeks doorgeven in de referenties van gebruiker
Uw toepassing kan de gebruiker referenties tooAzure AD rechtstreeks bieden. Deze methode werkt alleen met een gebruikersaccount voor de organisatie-ID; het is niet compatibel met persoonlijke / 'live-ID' gebruikersaccounts, met inbegrip van die eindigt op @outlook.com of @live.com. Deze methode is bovendien niet compatibel zijn met een gebruikersaccount waarvoor Azure AD tweeledige verificatie (2FA)).

### <a name="what-do-i-need-toouse-this-approach"></a>Wat kan ik deze benadering toouse nodig?
* Azure AD-domeinnaam. Dit al wordt vermeld in de vereiste Hallo van dit artikel.
* Azure AD **systeemeigen toepassing**
* Toepassings-ID voor de systeemeigen toepassing hello Azure AD
* Omleidings-URI voor Hallo systeemeigen Azure AD-toepassing
* Gedelegeerde machtigingen instellen


## <a name="step-1-create-an-active-directory-native-application"></a>Stap 1: Een systeemeigen Active Directory-toepassing maken

Maak en configureer een systeemeigen Azure AD-toepassing voor de eindgebruiker verificatie met Azure Data Lake Store met Azure Active Directory. Zie voor instructies [maken van een Azure AD-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Zorg ervoor dat u selecteert bij het Hallo-instructies op Hallo hierboven koppeling te volgen, **systeemeigen** voor toepassingstype, zoals wordt weergegeven in onderstaande schermafbeelding voor Hallo.

![Web-app maken](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "systeemeigen app maken")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Stap 2: Ophalen van toepassings-id en omleidings-URI

Zie [Hallo toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) tooretrieve Hallo toepassings-id (ook Hallo client-ID in de klassieke Azure-portal Hallo genoemd) van systeemeigen hello Azure AD-toepassing.

tooretrieve Hallo omleidings-URI, volgt u onderstaande stappen voor Hallo.

1. Selecteer in Azure Portal Hallo, **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op systeemeigen hello Azure AD-toepassing die u zojuist hebt gemaakt.

2. Van Hallo **instellingen** blade voor de toepassing hello, klikt u op **omleidings-URI's**.

    ![Get omleidings-URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Kopieer Hallo waarde weergegeven.


## <a name="step-3-set-permissions"></a>Stap 3: Machtigingen voor het instellen

1. Selecteer in Azure Portal Hallo, **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op systeemeigen hello Azure AD-toepassing die u zojuist hebt gemaakt.

2. Van Hallo **instellingen** blade voor de toepassing hello, klikt u op **vereist machtigingen**, en klik vervolgens op **toevoegen**.

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. In Hallo **API-toegang toevoegen** blade, klikt u op **selecteert u een API**, klikt u op **Azure Data Lake**, en klik vervolgens op **Selecteer**.

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  In Hallo **API-toegang toevoegen** blade, klikt u op **machtigingen selecteren**, selecteer het selectievakje toogive Hallo **volledige toegang tot tooData Lake Store**, en klik vervolgens op **selecteren** .

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Klik op **Gereed**.

5. Herhaal Hallo laatste twee stappen toogrant machtigingen voor **Windows Azure Service Management API** ook.
   
## <a name="next-steps"></a>Volgende stappen
In dit artikel een systeemeigen Azure AD-toepassing hebt gemaakt en die worden verzameld door Hallo-informatie die u nodig hebt in uw clienttoepassingen te ontwerpen met behulp van de SDK voor .NET, Java SDK, REST-API, enzovoort. Nu kunt u verder toohello artikelen die praten over hoe toouse hello Azure AD web application toofirst verifiëren met Data Lake Store en andere bewerkingen uit te voeren op Hallo store te volgen.

* [Aan de slag met Azure Data Lake Store met .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Aan de slag met Azure Data Lake Store met Java SDK](data-lake-store-get-started-java-sdk.md)
* [Aan de slag met Azure Data Lake Store met REST-API](data-lake-store-get-started-rest-api.md)


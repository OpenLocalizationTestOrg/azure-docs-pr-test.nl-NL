---
title: 'Verificatie van de eindgebruiker: Data Lake Store met Azure Active Directory | Microsoft Docs'
description: Meer informatie over het bereiken van de eindgebruiker verificatie met Data Lake Store met Azure Active Directory
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
ms.openlocfilehash: c20f5c39b00992d801909c8e5de292f3c2f12673
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a>Verificatie van de eindgebruiker met Data Lake Store met Azure Active Directory
> [!div class="op_single_selector"]
> * [Verificatie van service-tot-service](data-lake-store-authenticate-using-active-directory.md)
> * [Verificatie van de eindgebruiker](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie. Vóór het ontwerpen van een toepassing die met Azure Data Lake Store of Azure Data Lake Analytics werkt, moet u eerst beslissen hoe u wilt verifiëren van uw toepassing met Azure Active Directory (Azure AD). De twee belangrijkste opties zijn beschikbaar:

* Verificatie van de eindgebruiker (in dit artikel)
* Verificatie van service-tot-service

Deze beide opties leiden in uw toepassing wordt geleverd met een OAuth 2.0-token, dat wordt gekoppeld aan elke aanvraag die zijn aangebracht in Azure Data Lake Store of Azure Data Lake Analytics.

Dit artikel vertelt over het maken van een **systeemeigen Azure AD-toepassing voor verificatie van de eindgebruiker**. Zie voor instructies voor de configuratie van Azure AD-toepassing voor verificatie van de service to service [authentication Service-naar-service met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

* Uw abonnement-ID. U kunt deze ophalen vanuit de Azure Portal. Het is bijvoorbeeld beschikbaar op de blade Data Lake Store-account.
  
    ![Abonnement-ID ophalen](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* De naam van uw Azure AD-domein. U kunt deze ophalen door de muis in de rechterbovenhoek van de Azure-Portal. Uit de onderstaande schermafbeelding de domeinnaam is **contoso.onmicrosoft.com**, en de GUID tussen vierkante haken is de tenant-ID. 
  
    ![Ophalen van AAD-domein](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a>Verificatie van de eindgebruiker
Dit is de aanbevolen aanpak als u wilt dat een eindgebruiker zich aanmelden bij uw toepassing via Azure AD. Uw toepassing zich voor toegang tot Azure-resources met hetzelfde niveau van toegang als de eindgebruiker die in het logboek geregistreerd. U moet uw eindgebruikers hun referenties periodiek in volgorde voor uw toepassing toegankelijk.

Het resultaat van de eindgebruiker zich aanmeldt met is dat uw toepassing een toegangstoken en een vernieuwingstoken wordt gegeven. Het toegangstoken opgehaald gekoppeld aan elke aanvraag die wijzigingen in Data Lake Store of de Data Lake Analytics en het één uur standaard geldig is. Het vernieuwingstoken dat kan worden gebruikt voor het verkrijgen van een nieuw toegangstoken en is geldig voor maximaal twee weken standaard als u regelmatig gebruikt. U kunt twee verschillende benaderingen voor eindgebruikers aanmelden.

### <a name="using-the-oauth-20-pop-up"></a>Met behulp van het pop-upvenster OAuth 2.0
Uw toepassing kan resulteren in een OAuth 2.0 autorisatie pop-upvenster waarin de eindgebruiker hun referenties kan opgeven. Dit pop-upvenster werkt ook met het proces van Azure AD tweeledige verificatie (2FA), indien nodig. 

> [!NOTE]
> Nog wordt niet in de Azure AD Authentication Library (ADAL) voor Python of Java ondersteund door deze methode.
> 
> 

### <a name="directly-passing-in-user-credentials"></a>Rechtstreeks doorgeven in de referenties van gebruiker
Uw toepassing krijgt u de referenties van gebruiker rechtstreeks naar Azure AD. Deze methode werkt alleen met een gebruikersaccount voor de organisatie-ID; het is niet compatibel met persoonlijke / 'live-ID' gebruikersaccounts, met inbegrip van die eindigt op @outlook.com of @live.com. Deze methode is bovendien niet compatibel zijn met een gebruikersaccount waarvoor Azure AD tweeledige verificatie (2FA)).

### <a name="what-do-i-need-to-use-this-approach"></a>Wat moet ik gebruik deze benadering?
* Azure AD-domeinnaam. Dit staat al in de vereisten van dit artikel.
* Azure AD **systeemeigen toepassing**
* Toepassings-ID voor de systeemeigen Azure AD-toepassing
* Omleidings-URI voor de systeemeigen Azure AD-toepassing
* Gedelegeerde machtigingen instellen


## <a name="step-1-create-an-active-directory-native-application"></a>Stap 1: Een systeemeigen Active Directory-toepassing maken

Maak en configureer een systeemeigen Azure AD-toepassing voor de eindgebruiker verificatie met Azure Data Lake Store met Azure Active Directory. Zie voor instructies [maken van een Azure AD-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Zorg ervoor dat u selecteert bij de instructies in de bovenstaande koppeling te volgen, **systeemeigen** voor toepassingstype, zoals wordt weergegeven in de onderstaande schermafbeelding.

![Web-app maken](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "systeemeigen app maken")

## <a name="step-2-get-application-id-and-redirect-uri"></a>Stap 2: Ophalen van toepassings-id en omleidings-URI

Zie [de toepassings-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) voor het ophalen van de toepassings-id (oftewel de client-ID in de klassieke Azure portal) van de systeemeigen Azure AD-toepassing.

Volg de onderstaande stappen voor het ophalen van de omleidings-URI.

1. Selecteer in de Azure-Portal **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op de systeemeigen Azure AD-toepassing die u zojuist hebt gemaakt.

2. Van de **instellingen** blade voor de toepassing, klikt u op **omleidings-URI's**.

    ![Get omleidings-URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. Kopieer de weergegeven waarde.


## <a name="step-3-set-permissions"></a>Stap 3: Machtigingen voor het instellen

1. Selecteer in de Azure-Portal **Azure Active Directory**, klikt u op **App registraties**, en zoeken en klikt u op de systeemeigen Azure AD-toepassing die u zojuist hebt gemaakt.

2. Van de **instellingen** blade voor de toepassing, klikt u op **vereist machtigingen**, en klik vervolgens op **toevoegen**.

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. In de **API-toegang toevoegen** blade, klikt u op **selecteert u een API**, klikt u op **Azure Data Lake**, en klik vervolgens op **Selecteer**.

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  In de **API-toegang toevoegen** blade, klikt u op **machtigingen selecteren**, schakel het selectievakje in zodat **volledige toegang tot Data Lake Store**, en klik vervolgens op **selecteren**.

    ![client-id](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    Klik op **Gereed**.

5. Herhaal de laatste twee stappen voor het verlenen van machtigingen voor **Windows Azure Service Management API** ook.
   
## <a name="next-steps"></a>Volgende stappen
In dit artikel een systeemeigen Azure AD-toepassing hebt gemaakt en die worden verzameld door de informatie die u nodig hebt in uw clienttoepassingen te ontwerpen met behulp van de SDK voor .NET, Java SDK, REST-API, enzovoort. U kunt nu doorgaan met de volgende artikelen die communiceren over het gebruik van de Azure AD-webtoepassing eerst worden geverifieerd met Data Lake Store en andere bewerkingen uit te voeren in de store.

* [Aan de slag met Azure Data Lake Store met .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Aan de slag met Azure Data Lake Store met Java SDK](data-lake-store-get-started-java-sdk.md)
* [Aan de slag met Azure Data Lake Store met REST-API](data-lake-store-get-started-rest-api.md)


---
title: 'Verificatie van de service-naar-service: Data Lake Store met Azure Active Directory | Microsoft Docs'
description: Meer informatie over hoe tooachieve service to service-verificatie met Data Lake Store met Azure Active Directory
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 2e56237a75f020067b3248a1e1cfaf3c8df1371c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Verificatie met Data Lake Store met Azure Active Directory-Services
> [!div class="op_single_selector"]
> * [Verificatie van service-tot-service](data-lake-store-authenticate-using-active-directory.md)
> * [Verificatie van de eindgebruiker](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie. Vóór het ontwerpen van een toepassing die met Azure Data Lake Store of Azure Data Lake Analytics werkt, moet u eerst beslissen hoe u tooauthenticate wilt dat uw toepassing met Azure Active Directory (Azure AD). Hallo twee belangrijkste opties zijn beschikbaar:

* Verificatie van de eindgebruiker 
* Verificatie van de service-naar-service (in dit artikel) 

Deze beide opties leiden in uw toepassing wordt geleverd met een OAuth 2.0-token, dat gekoppelde tooeach verzoek tooAzure Data Lake Store of Azure Data Lake Analytics opgehaald.

Dit artikel vertelt over het maken van een **Azure AD-webtoepassing voor verificatie van de service to service**. Zie voor instructies voor de configuratie van Azure AD-toepassing voor verificatie van de eindgebruiker [eindgebruiker verificatie met Data Lake Store met Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Stap 1: Maak een Active Directory-webtoepassing

Maken en configureren van een Azure AD-webtoepassing voor service to service-verificatie met Azure Data Lake Store met Azure Active Directory. Zie voor instructies [maken van een Azure AD-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Zorg ervoor dat u selecteert bij het Hallo-instructies op Hallo hierboven koppeling te volgen, **Web-App / API** voor toepassingstype, zoals wordt weergegeven in onderstaande schermafbeelding voor Hallo.

![Web-app maken](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "web-app maken")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Stap 2: Toepassings-id en verificatiesleutel tenant-id ophalen
Wanneer u programmatisch zich aanmeldt, moet u Hallo-id voor uw toepassing. Als de toepassing hello wordt uitgevoerd onder zijn eigen referenties, moet u ook een verificatiesleutel.

* Zie voor instructies over hoe tooretrieve Hallo toepassings-ID en -verificatie (ook wel Hallo clientgeheim) sleutel voor uw toepassing, [Get-ID en verificatie Toepassingssleutel](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Zie voor instructies over hoe tooretrieve Hallo tenant-ID, [tenant-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-hello-azure-ad-application-toohello-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Stap 3: Hello Azure AD-toepassing toohello Azure Data Lake Store-accountbestand of map (alleen voor verificatie van de service-naar-service) toewijzen
1. Meld u aan bij de nieuwe toohello [Azure-portal](https://portal.azure.com) en open hello Azure Data Lake Store-account dat u wilt dat tooassociate Hello Azure Active Directory-toepassing die u eerder hebt gemaakt.
2. Klik op de blade van het Data Lake Store-account op **Gegevensverkenner**.
   
    ![Mappen maken in Data Lake Store-account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "mappen maken in Data Lake-account")
3. In Hallo **Data Explorer** blade, klikt u op het Hallo-bestand of map waarvoor u wilt dat tooprovide toegang toohello Azure AD-toepassing en klik vervolgens op **toegang**. tooconfigure access tooa-bestand, klikt u op **toegang** van Hallo **bestandsvoorbeeld** blade.
   
    ![ACL's ingesteld op Data Lake-bestandssysteem](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "ACL's ingesteld op Data Lake-bestandssysteem")
4. Hallo **toegang** blade bevat standaard toegang Hallo en aangepaste toegang toohello hoofdmap al toegewezen. Klik op Hallo **toevoegen** pictogram tooadd aangepast-niveau ACL's.
   
    ![Standaard- en aangepaste toegang lijst](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "lijst standaard en aangepaste toegang")
5. Klik op Hallo **toevoegen** pictogram tooopen hello **aangepaste toegang toevoegen** blade. Klik op deze blade **gebruiker of groep selecteren**, en klik vervolgens in **gebruiker of groep selecteren** blade, zoekt u hello Azure Active Directory-toepassing u eerder hebt gemaakt. Als u een groot aantal groepen toosearch van hebt, gebruik Hallo bovenste toofilter op Hallo groepsnaam Hallo tekstvak. Klik op groep Hallo u tooadd wilt en klik vervolgens op **Selecteer**.
   
    ![Een groep toevoegen](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "een groep toevoegen")
6. Klik op **Selecteer machtigingen**, selecteer Hallo machtigingen en of u wilt dat tooassign Hallo machtigingen standaard ACL, toegang krijgen tot ACL of beide. Klik op **OK**.
   
    ![Wijs machtigingen toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "toogroup machtigingen toewijzen")
   
    Zie voor meer informatie over de machtigingen in Data Lake Store en/toegang ACL's, [toegangsbeheer in Data Lake Store](data-lake-store-access-control.md).
7. In Hallo **aangepaste toegang toevoegen** blade, klikt u op **OK**. Hallo toegevoegde groep met machtigingen Hallo die zijn gekoppeld, wordt nu weergegeven in Hallo **toegang** blade.
   
    ![Wijs machtigingen toogroup](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "toogroup machtigingen toewijzen")

## <a name="step-4-get-hello-oauth-20-token-endpoint-only-for-java-based-applications"></a>Stap 4: Hallo OAuth 2.0-tokeneindpunt ophalen (alleen voor Java-toepassingen)

1. Meld u aan bij de nieuwe toohello [Azure-portal](https://portal.azure.com) en klikt u op Active Directory in het linkerdeelvenster Hallo.

2. Klik in het linkerdeelvenster hello, **App registraties**.

3. Vanaf de bovenkant van de Hallo van tabblad App-registraties hello, klikt u op **eindpunten**.

    ![OAuth-token eindpunt](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "token OAuth-eindpunt")

4. Kopieer uit Hallo lijst met eindpunten, Hallo OAuth 2.0-tokeneindpunt.

    ![OAuth-token eindpunt](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "token OAuth-eindpunt")   

## <a name="next-steps"></a>Volgende stappen
In dit artikel gemaakt van een Azure AD-webtoepassing en verzameld Hallo-informatie die u nodig hebt in uw clienttoepassingen te ontwerpen met behulp van de SDK voor .NET, Java SDK, enzovoort. Nu kunt u verder toohello artikelen die praten over hoe toouse hello Azure AD web application toofirst verifiëren met Data Lake Store en andere bewerkingen uit te voeren op Hallo store te volgen.

* [Aan de slag met Azure Data Lake Store met .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Aan de slag met Azure Data Lake Store met Java SDK](data-lake-store-get-started-java-sdk.md)

In dit artikel doorlopen u Hallo basisstappen benodigde tooget een gebruiker principal up en wordt uitgevoerd voor uw toepassing. U kunt raadplegen Hallo artikelen tooget overige informatie op te volgen:
* [Gebruik PowerShell toocreate service-principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Verificatie via certificaat gebruiken voor verificatie van de service-principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Andere methoden tooauthenticate tooAzure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)



---
title: 'Verificatie van de service-naar-service: Data Lake Store met Azure Active Directory | Microsoft Docs'
description: Meer informatie over het bereiken van de service to service-verificatie met Data Lake Store met Azure Active Directory
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
ms.openlocfilehash: 27ec0a4f48115d44da98dd048868b044aedf173c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a>Verificatie met Data Lake Store met Azure Active Directory-Services
> [!div class="op_single_selector"]
> * [Verificatie van service-tot-service](data-lake-store-authenticate-using-active-directory.md)
> * [Verificatie van de eindgebruiker](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

Azure Data Lake Store maakt gebruik van Azure Active Directory voor verificatie. Vóór het ontwerpen van een toepassing die met Azure Data Lake Store of Azure Data Lake Analytics werkt, moet u eerst beslissen hoe u wilt verifiëren van uw toepassing met Azure Active Directory (Azure AD). De twee belangrijkste opties zijn beschikbaar:

* Verificatie van de eindgebruiker 
* Verificatie van de service-naar-service (in dit artikel) 

Deze beide opties leiden in uw toepassing wordt geleverd met een OAuth 2.0-token, dat wordt gekoppeld aan elke aanvraag die zijn aangebracht in Azure Data Lake Store of Azure Data Lake Analytics.

Dit artikel vertelt over het maken van een **Azure AD-webtoepassing voor verificatie van de service to service**. Zie voor instructies voor de configuratie van Azure AD-toepassing voor verificatie van de eindgebruiker [eindgebruiker verificatie met Data Lake Store met Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

## <a name="prerequisites"></a>Vereisten
* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="step-1-create-an-active-directory-web-application"></a>Stap 1: Maak een Active Directory-webtoepassing

Maken en configureren van een Azure AD-webtoepassing voor service to service-verificatie met Azure Data Lake Store met Azure Active Directory. Zie voor instructies [maken van een Azure AD-toepassing](../azure-resource-manager/resource-group-create-service-principal-portal.md).

Zorg ervoor dat u selecteert bij de instructies in de bovenstaande koppeling te volgen, **Web-App / API** voor toepassingstype, zoals wordt weergegeven in de onderstaande schermafbeelding.

![Web-app maken](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "web-app maken")

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a>Stap 2: Toepassings-id en verificatiesleutel tenant-id ophalen
Wanneer u programmatisch zich aanmeldt, moet u de id voor uw toepassing. Als de toepassing wordt uitgevoerd onder zijn eigen referenties, moet u ook een verificatiesleutel.

* Zie voor instructies over het ophalen van de toepassing-ID en -verificatie-sleutel (ook wel het clientgeheim) voor uw toepassing [Get-ID en verificatie Toepassingssleutel](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).

* Zie voor instructies over het ophalen van de tenant-ID [tenant-ID ophalen](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).

## <a name="step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a>Stap 3: De Azure AD toepassing toewijzen aan het Azure Data Lake Store-accountbestand of map (alleen voor verificatie van de service-naar-service)
1. Meld u bij de nieuwe [Azure-portal](https://portal.azure.com) en opent u het Azure Data Lake Store-account dat u wilt koppelen aan de Azure Active Directory-toepassing die u eerder hebt gemaakt.
2. Klik op de blade van het Data Lake Store-account op **Gegevensverkenner**.
   
    ![Mappen maken in Data Lake Store-account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "mappen maken in Data Lake-account")
3. In de **Data Explorer** blade, klikt u op het bestand of map waarvoor u wilt toegang bieden tot de Azure AD-toepassing en klik vervolgens op **toegang**. Voor het configureren van toegang tot een bestand, klikt u op **toegang** van de **bestandsvoorbeeld** blade.
   
    ![ACL's ingesteld op Data Lake-bestandssysteem](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "ACL's ingesteld op Data Lake-bestandssysteem")
4. De **toegang** blade bevat de standaard toegang en aangepaste toegang is al toegewezen aan de hoofdmap. Klik op de **toevoegen** pictogram Aangepast niveau ACL's toevoegen.
   
    ![Standaard- en aangepaste toegang lijst](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "lijst standaard en aangepaste toegang")
5. Klik op de **toevoegen** pictogram openen de **aangepaste toegang toevoegen** blade. Klik op deze blade **gebruiker of groep selecteren**, en klik vervolgens in **gebruiker of groep selecteren** blade, zoekt u de Azure Active Directory-toepassing die u eerder hebt gemaakt. Als u een groot aantal groepen om te zoeken vanaf hebt, gebruikt u in het tekstvak boven kunt u filteren op naam van de groep. Klik op de groep die u wilt toevoegen en klik vervolgens op **Selecteer**.
   
    ![Een groep toevoegen](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "een groep toevoegen")
6. Klik op **Selecteer machtigingen**, selecteer de machtigingen en of u de machtigingen toewijzen als een standaard ACL wilt, toegang krijgen tot ACL of beide. Klik op **OK**.
   
    ![Machtigingen toewijzen aan de groep](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "machtigingen toewijzen aan de groep")
   
    Zie voor meer informatie over de machtigingen in Data Lake Store en/toegang ACL's, [toegangsbeheer in Data Lake Store](data-lake-store-access-control.md).
7. In de **aangepaste toegang toevoegen** blade, klikt u op **OK**. De toegevoegde groep met de bijbehorende machtigingen wordt nu weergegeven in de **toegang** blade.
   
    ![Machtigingen toewijzen aan de groep](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "machtigingen toewijzen aan de groep")

## <a name="step-4-get-the-oauth-20-token-endpoint-only-for-java-based-applications"></a>Stap 4: Het eindpunt van het OAuth 2.0-token ophalen (alleen voor Java-toepassingen)

1. Meld u bij de nieuwe [Azure-portal](https://portal.azure.com) en klikt u op Active Directory in het linkerdeelvenster.

2. Klik in het linkerdeelvenster op **App registraties**.

3. Klik vanaf de bovenkant van het tabblad App-registraties **eindpunten**.

    ![OAuth-token eindpunt](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "token OAuth-eindpunt")

4. Kopieer het OAuth 2.0-tokeneindpunt uit de lijst met eindpunten.

    ![OAuth-token eindpunt](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "token OAuth-eindpunt")   

## <a name="next-steps"></a>Volgende stappen
In dit artikel gemaakt van een Azure AD-webtoepassing en verzameld van de informatie die u nodig hebt in uw clienttoepassingen te ontwerpen met behulp van de SDK voor .NET, Java SDK, enzovoort. U kunt nu doorgaan met de volgende artikelen die communiceren over het gebruik van de Azure AD-webtoepassing eerst worden geverifieerd met Data Lake Store en andere bewerkingen uit te voeren in de store.

* [Aan de slag met Azure Data Lake Store met .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Aan de slag met Azure Data Lake Store met Java SDK](data-lake-store-get-started-java-sdk.md)

In dit artikel gelopen u door de basisstappen die u nodig hebt voor een gebruiker principal up en wordt uitgevoerd voor uw toepassing. U kunt de volgende artikelen voor meer informatie bekijken:
* [PowerShell gebruiken voor het service-principal maken](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [Verificatie via certificaat gebruiken voor verificatie van de service-principal](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [Andere methoden om te verifiëren met Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)



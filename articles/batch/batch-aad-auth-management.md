---
title: aaaUse Azure Active Directory tooauthenticate Batch beheeroplossingen | Microsoft Docs
description: "Toepassingen die zijn gebouwd met Azure resourcemanager en Hallo Batch-resourceprovider zich verifiëren met Azure AD."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: tamram
ms.openlocfilehash: 192aa9f8d7cbfc0282a4a0c33ab1659f1f351525
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a>Verificatie van oplossingen voor het beheer van de Batch met Active Directory

Toepassingen die hello Azure Batch Management-service aanroepen verifiëren met [Azure Active Directory] [ aad_about] (Azure AD). Azure AD is Microsoft multitenant-cloudgebaseerde adreslijst en identity management-service. Azure zelf gebruikt Azure AD voor de verificatie van Hallo van zijn klanten, servicebeheerders en organisatie-gebruikers.

Hallo Batch Management .NET-bibliotheek wordt typen voor het werken met de Batch-accounts, toegangscodes, toepassingen en toepassingspakketten. Hallo Batch Management .NET-bibliotheek is een Azure-resource provider-client en wordt gebruikt in combinatie met [Azure Resource Manager] [ resman_overview] toomanage deze resources via een programma. Azure AD is vereist tooauthenticate aanvragen via een Azure-resource provider client, waaronder Hallo Batch Management .NET-bibliotheek, en via [Azure Resource Manager][resman_overview].

In dit artikel wordt besproken voor het gebruik van Azure AD-tooauthenticate uit toepassingen die gebruikmaken van Hallo Batch Management .NET-bibliotheek. Laten we zien hoe toouse Azure AD-tooauthenticate de abonnementsbeheerder van een of CO-beheerder, met behulp van verificatie geïntegreerde. We gebruiken Hallo [AccountManagment] [ acct_mgmt_sample] voorbeeldproject, beschikbaar op GitHub, toowalk via met behulp van Azure AD met Hallo Batch Management .NET-bibliotheek.

toolearn meer over het gebruik van Hallo Batch Management .NET-bibliotheek en voorbeeld van de AccountManagement hello, Zie [beheren Batch-accounts en quota's met Hallo Batch Management-clientbibliotheek voor .NET](batch-management-dotnet.md).

## <a name="register-your-application-with-azure-ad"></a>Uw toepassing registreren met Azure AD

Hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) biedt een programmeerinterface tooAzure AD voor gebruik binnen uw toepassingen. toocall ADAL van uw toepassing, moet u uw toepassing registreren in een Azure AD-tenant. Wanneer u uw toepassing registreert, kunt u Azure AD met informatie geven over uw toepassing, met inbegrip van een naam voor het binnen hello Azure AD-tenant. Vervolgens Azure AD levert een toepassings-ID dat u tooassociate uw toepassing met Azure AD tijdens runtime. toolearn meer informatie over het Hallo-toepassings-ID, Zie [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister hello AccountManagement voorbeeldtoepassing Hallo stappen in Hallo [een toepassing toe te voegen](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) in sectie [toepassingen integreren met Azure Active Directory] [ aad_integrate]. Geef **systeemeigen clienttoepassing** voor Hallo-type van de toepassing. Hallo bedrijfstak standaard OAuth 2.0-URI voor Hallo **omleidings-URI** is `urn:ietf:wg:oauth:2.0:oob`. U kunt echter geldige URI opgeven (zoals `http://myaccountmanagementsample`) voor Hallo **omleidings-URI**, zoals niet toobe een echte eindpunt hoeft:

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

Nadat u het registratieproces Hallo hebt voltooid, u ziet dat Hallo toepassings-ID en Hallo object (service-principal)-ID van uw toepassing.  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-hello-azure-resource-manager-api-access-tooyour-application"></a>Hello Azure Resource Manager-API toegang tooyour toepassing verlenen

Vervolgens moet u toodelegate toegang tooyour toepassing toohello Azure Resource Manager-API. Hello Azure AD-id voor Hallo Resource Manager-API is **Windows Azure Service Management API**.

Volg deze stappen in hello Azure-portal:

1. Kies in Hallo links navigatievenster van hello Azure-portal, **meer Services**, klikt u op **App registraties**, en klik op **toevoegen**.
2. Hallo-naam van uw toepassing in de lijst Hallo van app-registraties zoeken:

    ![Zoeken naar de toepassingsnaam van uw](./media/batch-aad-auth-management/search-app-registration.png)

3. Weergave Hallo **instellingen** blade. In Hallo **API-toegang** sectie **vereist machtigingen**.
4. Klik op **toevoegen** tooadd een nieuwe vereiste machtiging. 
5. Typ in stap 1, **Windows Azure Service Management API**, selecteer die API van Hallo lijst met resultaten en klikt u op Hallo **Selecteer** knop.
6. In stap 2, selecteer Hallo selectievakje in naast te**klassieke implementatiemodel van Azure toegang als gebruikers organisatie**, en klik op Hallo **Selecteer** knop.
7. Klik op Hallo **gedaan** knop.

Hallo **Required Permissions** blade nu toont dat machtigingen tooyour toepassing tooboth worden toegekend Hallo ADAL en Resource Manager-API's. Machtigingen worden verleend tooADAL standaard wanneer u uw app eerst bij Azure AD registreren.

![Delegeren van machtigingen toohello Azure Resource Manager-API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a>Azure AD-eindpunten

tooauthenticate uw Batch-Management-oplossingen in Azure AD, moet u twee bekende eindpunten.

- Hallo **algemene Azure AD-eindpunt** biedt een algemene referentie interface verzamelen als een specifieke tenant niet is opgegeven, net als bij Hallo geïntegreerde verificatie:

    `https://login.microsoftonline.com/common`

- Hallo **Azure Resource Manager-eindpunt** gebruikte tooacquire is een token voor het verifiëren van aanvragen toohello Batch management-service:

    `https://management.core.windows.net/`

Hallo AccountManagement voorbeeldtoepassing definieert constanten voor deze eindpunten. Laat deze constanten ongewijzigd:

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a>Verwijst naar de toepassings-ID 

Uw clienttoepassing gebruikmaakt van Hallo toepassing-ID (ook waarnaar wordt verwezen tooas Hallo client-ID) tooaccess Azure AD tijdens runtime. Nadat u uw toepassing in hello Azure-portal hebt geregistreerd, worden uw code toouse Hallo toepassings-ID opgegeven door Azure AD voor de geregistreerde toepassing bijgewerkt. In Hallo AccountManagement voorbeeldtoepassing, kopieert u de toepassings-ID van hello Azure portal toohello juiste constante:

```csharp
// Specify hello unique identifier (hello "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access hello Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
Hallo omleidings-URI die u hebt opgegeven tijdens het registratieproces Hallo ook kopiëren. Hallo redirect die URI in uw code opgegeven moet overeenkomen met de Hallo omleidings-URI die u hebt opgegeven bij de registratie van de toepassing hello.

```csharp
// hello URI toowhich Azure AD will redirect in response tooan OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need toobe a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a>Een Azure AD-verificatietoken ophalen

Nadat u Hallo AccountManagement voorbeeld in hello Azure AD-tenant registreren en voorbeeldcode Hallo met de waarden bijwerken, is een voorbeeld van Hallo gereed tooauthenticate gebruikmaken van Azure AD. Wanneer u Hallo voorbeeld uitvoert, probeert Hallo ADAL tooacquire geen verificatietoken. Bij deze stap wordt u gevraagd uw referenties Microsoft: 

```csharp
// Obtain an access token using hello "common" AAD resource. This allows hello application
// tooquery AAD for information that lies outside hello application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

Nadat u uw referenties opgeeft, kan de voorbeeldtoepassing Hallo tooissue geverifieerde aanvragen toohello Batch management-service kunt doorgaan. 

## <a name="next-steps"></a>Volgende stappen

Voor meer informatie over het uitvoeren van Hallo [AccountManagement voorbeeldtoepassing][acct_mgmt_sample], Zie [beheren Batch-accounts en quota's met Hallo Batch Management-clientbibliotheek voor .NET](batch-management-dotnet.md).

toolearn meer informatie over Azure AD, Zie Hallo [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/). Gedetailleerde voorbeelden ziet u hoe toouse ADAL zijn beschikbaar in Hallo [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliotheek.

Zie tooauthenticate Batch-service-toepassingen die gebruikmaken van Azure AD [oplossingen van de service Batch verifiëren met Active Directory](batch-aad-auth.md). 


[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md

---
title: oplossingen voor aaaUse Azure Active Directory tooauthenticate Azure Batch-service | Microsoft Docs
description: Batch ondersteunt Azure AD voor de verificatie van Hallo Batch-service.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/20/2017
ms.author: tamram
ms.openlocfilehash: 6c825c30f1c80bb059a797a2e78367e599acd109
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-batch-service-solutions-with-active-directory"></a>Verificatie van oplossingen voor Batch-service met Active Directory

Azure Batch biedt ondersteuning voor verificatie met [Azure Active Directory] [ aad_about] (Azure AD). Azure AD is Microsoft multitenant-cloudgebaseerde adreslijst en identity management-service. Azure zelf tooauthenticate Azure AD gebruikt, zijn klanten, servicebeheerders en organisatie-gebruikers.

Als u Azure AD-verificatie met Azure Batch, kunt u verifiëren op twee manieren:

- Met behulp van **geïntegreerde verificatie** tooauthenticate een gebruiker die de interactie met Hallo-toepassing. Een toepassing met geïntegreerde verificatie worden verzameld van de referenties van een gebruiker en gebruikt deze referenties tooauthenticate toegang tooBatch resources.
- Met behulp van een **service-principal** tooauthenticate een toepassing zonder toezicht. Een service-principal definieert Hallo beleid en machtigingen voor een toepassing in volgorde toorepresent Hallo toepassing bij het openen van bronnen tijdens runtime.

toolearn meer informatie over Azure AD, Zie Hallo [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/).

## <a name="authentication-and-pool-allocation-mode"></a>Verificatie- en groep toewijzing-modus

Wanneer u een Batch-account maakt, kunt u opgeven waar de groepen die zijn gemaakt voor dat account moeten worden toegewezen. U kunt groepen tooallocate in Hallo standaard Batch-service-abonnement of in een gebruikerabonnement. Uw keuze is van invloed op hoe u toegang tooresources in het account verifiëren.

- **Batch-service-abonnement**. Batch-pools worden standaard toegewezen in een Batch-service-abonnement. Als u deze optie kiest, kunt u verifiëren toegang tooresources in het account met [gedeelde sleutel](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) of met Azure AD.
- **Gebruikerabonnement.** U kunt tooallocate Batch-pools in een gebruikerabonnement die u opgeeft. Als u deze optie kiest, moet u verifiëren met Azure AD.

## <a name="endpoints-for-authentication"></a>Eindpunten voor verificatie

tooauthenticate Batch-toepassingen met Azure AD, moet u tooinclude sommige bekende eindpunten in uw code.

### <a name="azure-ad-endpoint"></a>Azure AD-eindpunt

Hallo base Azure AD authority-eindpunt is:

`https://login.microsoftonline.com/`

tooauthenticate met Azure AD, u dit eindpunt samen met de Hallo tenant-ID (directory-ID). Hallo tenant-ID identificeert hello Azure AD-tenant toouse voor verificatie. tooretrieve Hallo tenant-ID, Hallo stappen die worden beschreven in [hello tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

`https://login.microsoftonline.com/<tenant-id>`

> [!NOTE] 
> Hallo tenantspecifieke eindpunt is vereist wanneer u verifiëren met behulp van een service-principal. 
> 
> Hallo tenantspecifieke eindpunt is optioneel wanneer u verifiëren met behulp van geïntegreerde verificatie, maar aanbevolen. U kunt echter ook algemene hello Azure AD-eindpunt gebruiken. Hallo gemeenschappelijk eindpunt biedt een algemene referentie interface verzamelen als een specifieke tenant is niet opgegeven. algemene Hallo-eindpunt is `https://login.microsoftonline.com/common`.
>
>

Zie voor meer informatie over Azure AD-eindpunten [verificatie scenario's voor Azure AD][aad_auth_scenarios].

### <a name="batch-resource-endpoint"></a>Eindpunt voor batch-resource

Gebruik Hallo **endpoint van Azure Batch-resource** tooacquire een token voor het verifiëren van aanvragen toohello Batch-service:

`https://batch.core.windows.net/`

## <a name="register-your-application-with-a-tenant"></a>Uw toepassing registreren met een tenant

eerste stap bij het gebruik van Azure AD tooauthenticate Hello wordt uw toepassing registreren in een Azure AD-tenant. Registreren van uw toepassing kunt u toocall hello Azure [Active Directory Authentication Library] [ aad_adal] (ADAL) vanuit uw code. Hallo ADAL biedt een API voor de verificatie met Azure AD van uw toepassing. Registreren van uw toepassing is vereist, of u van plan toouse geïntegreerde verificatie of een service-principal bent.

Wanneer u uw toepassing registreert, kunt u informatie opgeven over uw toepassing tooAzure AD. Vervolgens Azure AD levert een toepassings-ID dat u tooassociate uw toepassing met Azure AD tijdens runtime. toolearn meer informatie over het Hallo-toepassings-ID, Zie [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).

tooregister uw Batch-toepassing hello Volg de stappen in Hallo [een toepassing toe te voegen](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) in sectie [toepassingen integreren met Azure Active Directory][aad_integrate]. Als u uw toepassing als een systeemeigen toepassing registreren, kunt u een geldige URI voor Hallo **omleidings-URI**. Hoeft niet toobe een echte-eindpunt.

Nadat u uw toepassing hebt geregistreerd, ziet u Hallo toepassings-ID:

![De Batch-toepassing registreren met Azure AD](./media/batch-aad-auth/app-registration-data-plane.png)

Zie voor meer informatie over het registreren van een toepassing met Azure AD [verificatie scenario's voor Azure AD](../active-directory/develop/active-directory-authentication-scenarios.md).

## <a name="get-hello-tenant-id-for-your-active-directory"></a>Hallo tenant-ID niet ophalen voor uw Active Directory

Hallo tenant-ID identificeert hello Azure AD-tenant waarmee verificatie services tooyour-toepassing. tooget Hallo tenant-ID, als volgt te werk:

1. Selecteer in hello Azure-portal, de Active Directory.
2. Klik op **Eigenschappen**.
3. Kopieer Hallo GUID-waarde opgegeven voor Hallo directory-ID. Deze waarde is een afkorting Hallo tenant-ID.

![Kopieer Hallo map-ID](./media/batch-aad-auth/aad-directory-id.png)


## <a name="use-integrated-authentication"></a>Gebruik van geïntegreerde verificatie

tooauthenticate met geïntegreerde verificatie, moet u toogrant na uw toepassing machtigingen tooconnect toohello API van Batch-service. Deze stap kunt uw toepassing tooauthenticate aanroepen toohello Batch-service API met Azure AD.

Zodra u hebt [geregistreerd van uw toepassing](#register-your-application-with-an-azure-ad-tenant), als volgt te werk in hello Azure portal toogrant deze toegang hebben tot toohello Batch-service:

1. Kies in Hallo links navigatievenster van hello Azure-portal, **meer Services**, klikt u op **App registraties**.
2. Hallo-naam van uw toepassing in de lijst Hallo van app-registraties zoeken:

    ![Zoeken naar de toepassingsnaam van uw](./media/batch-aad-auth/search-app-registration.png)

3. Open Hallo **instellingen** blade voor uw toepassing. In Hallo **API-toegang** sectie **vereist machtigingen**.
4. In Hallo **vereist machtigingen** blade, klikt u op Hallo **toevoegen** knop.
5. In stap 1, zoekt u Hallo Batch-API. Zoeken naar elk van deze tekenreeksen totdat u Hallo-API:
    1. **MicrosoftAzureBatch**.
    2. **Microsoft Azure Batch**. Nieuwere Azure AD-tenants kunnen deze naam gebruiken.
    3. **ddbf3205-c6bd-46ae-8127-60eb93363864** Hallo-id voor Hallo Batch-API. 
6. Als u Hallo Batch-API hebt gevonden, te selecteren en op Hallo **Selecteer** knop.
6. In stap 2, selecteer Hallo selectievakje in naast te**Access Azure Batch-Service** en klik op Hallo **Selecteer** knop.
7. Klik op Hallo **gedaan** knop.

Hallo **Required Permissions** blade nu blijkt dat uw Azure AD-toepassing heeft toegang tooboth ADAL tot en Hallo API van Batch-service. Machtigingen worden verleend tooADAL automatisch wanneer u uw app eerst bij Azure AD registreren.

![Machtigingen verlenen API](./media/batch-aad-auth/required-permissions-data-plane.png)

## <a name="use-a-service-principal"></a>Gebruik van een service-principal 

een toepassing die wordt uitgevoerd zonder toezicht tooauthenticate, dat u een service-principal gebruiken. Nadat u uw toepassing hebt geregistreerd, als volgt in hello Azure portal tooconfigure een service-principal:

1. Vraagt u een geheime sleutel voor uw toepassing.
2. Een toepassing RBAC-rol tooyour toewijzen.

### <a name="request-a-secret-key-for-your-application"></a>Vraagt u een geheime sleutel voor uw toepassing

Als uw toepassing wordt geverifieerd met een service-principal, verzendt de zowel Hallo toepassings-ID en een geheime sleutel tooAzure AD. U moet toocreate en geheime sleutel toouse Hallo kopiëren vanuit uw code.

Volg deze stappen in hello Azure-portal:

1. Kies in Hallo links navigatievenster van hello Azure-portal, **meer Services**, klikt u op **App registraties**.
2. Zoeken naar Hallo-naam van uw toepassing in de lijst Hallo van app-registraties.
3. Weergave Hallo **instellingen** blade. In Hallo **API-toegang** sectie **sleutels**.
4. toocreate een sleutel is, voer een beschrijving voor Hallo-sleutel. Selecteer vervolgens een duur voor de sleutel Hallo van één of twee jaar. 
5. Klik op Hallo **opslaan** knop toocreate en Hallo sleutel weer te geven. Gekopieerd Hallo sleutelwaarde tooa veilige plaats, zoals tooaccess kunnen niet worden het opnieuw nadat u laat Hallo-blade. 

    ![Maken van een geheime sleutel](./media/batch-aad-auth/secret-key.png)

### <a name="assign-an-rbac-role-tooyour-application"></a>Een toepassing RBAC-rol tooyour toewijzen

tooauthenticate met een service-principal moet u een toepassing RBAC-rol tooyour tooassign. Volg deze stappen:

1. Navigeer in hello Azure-portal, toohello Batch-account wordt gebruikt door uw toepassing.
2. In Hallo **instellingen** blade voor Hallo Batch-account, selecteer **Access Control (IAM)**.
3. Klik op Hallo **toevoegen** knop. 
4. Van Hallo **rol** vervolgkeuzelijst, kiest u beide Hallo _Inzender_ of _lezer_ rol voor uw toepassing. Zie voor meer informatie over deze rollen [aan de slag met toegangsbeheer op basis van rollen in Azure-portal Hallo](../active-directory/role-based-access-control-what-is.md).  
5. In Hallo **Selecteer** Hallo- naam van uw toepassing. Selecteer uw toepassing uit Hallo lijst en klikt u op **opslaan**.

Uw toepassing wordt nu weergegeven in de instellingen voor toegangsbeheer met een RBAC-rol die is toegewezen. 

![Een toepassing RBAC-rol tooyour toewijzen](./media/batch-aad-auth/app-rbac-role.png)

### <a name="get-hello-tenant-id-for-your-azure-active-directory"></a>Hallo tenant-ID niet ophalen voor uw Azure Active Directory

Hallo tenant-ID identificeert hello Azure AD-tenant waarmee verificatie services tooyour-toepassing. tooget Hallo tenant-ID, als volgt te werk:

1. Selecteer in hello Azure-portal, de Active Directory.
2. Klik op **Eigenschappen**.
3. Kopieer Hallo GUID-waarde opgegeven voor Hallo directory-ID. Deze waarde is een afkorting Hallo tenant-ID.

![Kopieer Hallo map-ID](./media/batch-aad-auth/aad-directory-id.png)


## <a name="code-examples"></a>Codevoorbeelden

Hallo-codevoorbeelden in deze sectie hoe tooauthenticate met Azure AD via verificatie geïntegreerde, en met een service-principal weergeven. Deze codevoorbeelden .NET gebruiken, maar Hallo concepten zijn vergelijkbaar voor andere talen.

> [!NOTE]
> Een Azure AD authentication-token verloopt na één uur. Wanneer u een lange levensduur **BatchClient** object, het is raadzaam dat u een token ophalen van ADAL op elke aanvraag tooensure hebt u altijd een geldig token. 
>
>
> tooachieve dit in .NET schrijven van een methode dat haalt Hallo-token van Azure AD en doorgeven die methode tooa **BatchTokenCredentials** object als een gemachtigde. Hallo gemachtigdenmethode is aangeroepen voor elke aanvraag toohello Batch-service tooensure die wordt geleverd met een geldig token. Standaard ADAL in de cache opgeslagen tokens, zodat een nieuw token is opgehaald uit Azure AD alleen indien nodig. Zie voor meer informatie over tokens in Azure AD [verificatie scenario's voor Azure AD][aad_auth_scenarios].
>
>

### <a name="code-example-using-azure-ad-integrated-authentication-with-batch-net"></a>Voorbeeld: met behulp van Azure AD geïntegreerde verificatie met Batch .NET

tooauthenticate met geïntegreerde verificatie in Batch .NET verwijzing Hallo [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pakket en Hallo [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakket.

Neem de volgende Hallo `using` instructies in uw code:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Verwijzing hello Azure AD-eindpunt in uw code, met inbegrip van Hallo tenant-ID. tooretrieve Hallo tenant-ID, Hallo stappen die worden beschreven in [hello tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Verwijzen naar Hallo Batch service-eindpunt voor resource:

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Verwijzen naar uw Batch-account:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Hallo toepassings-ID (client-ID) voor uw toepassing opgeven. Hallo toepassings-ID is beschikbaar via de registratie van uw app in hello Azure-portal:

```csharp
private const string ClientId = "<application-id>";
```

Hallo omleidings-URI die u hebt opgegeven tijdens het registratieproces Hallo ook kopiëren. Hallo redirect die URI in uw code opgegeven moet overeenkomen met de Hallo omleidings-URI die u hebt opgegeven bij de registratie van de toepassing hello:

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

Verificatietoken voor een retouraanroep methode tooacquire Hallo schrijven van Azure AD. Hallo **GetAuthenticationTokenAsync** een gebruiker die de interactie met de toepassing hello-aanroepen ADAL tooauthenticate retouraanroepmethode hier weergegeven. Hallo **AcquireTokenAsync** methode opgegeven door ADAL Hallo wordt u gevraagd de gebruiker om hun referenties en het Hallo-toepassing wordt voortgezet eenmaal Hallo gebruiker biedt deze (tenzij deze al in de cache referenties opgeslagen is):

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire hello authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

Samen een **BatchTokenCredentials** object waarvoor Hallo gemachtigde als parameter. Gebruik deze referenties tooopen een **BatchClient** object. U kunt die **BatchClient** object voor verdere bewerkingen tegen Hallo Batch-service:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

### <a name="code-example-using-an-azure-ad-service-principal-with-batch-net"></a>Voorbeeld: met behulp van een Azure AD-service-principal met Batch .NET

tooauthenticate met een service-principal in Batch .NET verwijzing Hallo [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) pakket en Hallo [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) pakket.

Neem de volgende Hallo `using` instructies in uw code:

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Verwijzing hello Azure AD-eindpunt in uw code, met inbegrip van Hallo tenant-ID. Wanneer u een service-principal gebruikt, moet u een eindpunt tenantspecifieke opgeven. tooretrieve Hallo tenant-ID, Hallo stappen die worden beschreven in [hello tenant-ID niet ophalen voor uw Azure Active Directory](#get-the-tenant-id-for-your-active-directory):

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/<tenant-id>";
```

Verwijzen naar Hallo Batch service-eindpunt voor resource:  

```csharp
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

Verwijzen naar uw Batch-account:

```csharp
private const string BatchAccountUrl = "https://myaccount.mylocation.batch.azure.com";
```

Hallo toepassings-ID (client-ID) voor uw toepassing opgeven. Hallo toepassings-ID is beschikbaar via de registratie van uw app in hello Azure-portal:

```csharp
private const string ClientId = "<application-id>";
```

Geef Hallo geheime sleutel die u hebt gekopieerd uit hello Azure-portal:

```csharp
private const string ClientKey = "<secret-key>";
```

Verificatietoken voor een retouraanroep methode tooacquire Hallo schrijven van Azure AD. Hallo **GetAuthenticationTokenAsync** retouraanroepmethode aanroepen ADAL voor verificatie zonder toezicht hier weergegeven:

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
    AuthenticationResult authResult = await authContext.AcquireTokenAsync(BatchResourceUri, new ClientCredential(ClientId, ClientKey));

    return authResult.AccessToken;
}
```

Samen een **BatchTokenCredentials** object waarvoor Hallo gemachtigde als parameter. Gebruik deze referenties tooopen een **BatchClient** object. Vervolgens kunt u die **BatchClient** object voor verdere bewerkingen tegen Hallo Batch-service:

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountUrl, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

## <a name="next-steps"></a>Volgende stappen

toolearn meer informatie over Azure AD, Zie Hallo [Azure Active Directory-documentatie](https://docs.microsoft.com/azure/active-directory/). Gedetailleerde voorbeelden ziet u hoe toouse ADAL zijn beschikbaar in Hallo [Azure codevoorbeelden](https://azure.microsoft.com/resources/samples/?service=active-directory) bibliotheek.

Zie toolearn meer informatie over service-principals [toepassing en service-principal objecten in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md). een service principal met toocreate hello Azure portal, Zie [portal toocreate Active Directory-toepassing en service-principal die toegang bronnen tot gebruiken](../resource-group-create-service-principal-portal.md). U kunt ook een service-principal maken met PowerShell of Azure CLI. 

Zie tooauthenticate Batch Management toepassingen die gebruikmaken van Azure AD [oplossingen voor het beheer van Batch verifiëren met Active Directory](batch-aad-auth-management.md). 

[aad_about]: ../active-directory/active-directory-whatis.md "Wat is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Verificatie-scenario's voor Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Toepassingen integreren met Azure Active Directory"
[azure_portal]: http://portal.azure.com

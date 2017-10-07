---
title: aaaCreate identiteit voor Azure-app met Azure CLI | Microsoft Docs
description: Hierin wordt beschreven hoe toouse Azure CLI toocreate een Azure Active Directory-toepassing en service-principal en verleen deze toegang hebben tot tooresources via op rollen gebaseerde toegang beheren. Er wordt weergegeven hoe tooauthenticate toepassing met een wachtwoord of certificaat.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Een service principal tooaccess-resources voor Azure CLI toocreate gebruiken

Wanneer u een app of een script dat tooaccess resources moet hebt, kunt u een identiteit voor het Hallo-app instellen en Hallo-app met een eigen referenties verifiëren. Deze identiteit staat bekend als een service-principal. Deze aanpak kunt u:

* Wijs machtigingen toe toohello app identiteit die anders zijn dan uw eigen machtigingen. Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.
* Een certificaat voor verificatie gebruiken bij het uitvoeren van een onbewaakt script.

Dit artikel ziet u hoe toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset van een toepassing toorun onder een eigen referenties en identiteit. Installeer de nieuwste versie Hallo van [Azure CLI 1.0](../cli-install-nodejs.md) toomake ervoor dat uw omgeving overeenkomt met de Hallo voorbeelden in dit artikel.

## <a name="required-permissions"></a>Vereiste machtigingen
toocomplete in dit onderwerp, moet u voldoende machtigingen in uw Azure Active Directory en uw Azure-abonnement hebben. In het bijzonder moeten kunnen toocreate een app in Azure Active Directory hello, en Hallo service principal tooa rol toe te wijzen. 

Hallo gemakkelijkste manier toocheck of uw account de juiste machtigingen heeft, is via Hallo-portal. Zie [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions) (Vereiste machtigingen controleren in de portal).

Nu gaan tooa sectie voor [wachtwoord](#create-service-principal-with-password) of [certificaat](#create-service-principal-with-certificate) verificatie.

## <a name="create-service-principal-with-password"></a>Service-principal maken met wachtwoord
In deze sectie uitvoeren Hallo stappen toocreate Hallo AD-toepassing met een wachtwoord en Hallo lezer rol toohello service-principal toewijzen.

1. Meld u aan tooyour-account.
   
   ```azurecli
   azure login
   ```
2. toocreate een identiteit app bieden Hallo-naam van Hallo-app en een wachtwoord, zoals wordt weergegeven in de volgende opdracht Hallo:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   Hallo nieuwe service-principal wordt geretourneerd. Hallo Object-Id is vereist bij het verlenen van machtigingen. Hallo-guid worden weergegeven met de Service Principal Names Hallo is nodig wanneer u zich aanmeldt. Deze guid is Hallo dezelfde waarde als Hallo app-id. Deze waarde is Hallo voorbeeldtoepassingen waarnaar wordt verwezen tooas Hallo `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Machtigingen Hallo service principal op uw abonnement. In dit voorbeeld moet u Hallo service principal toohello lezer functie, die machtiging tooread alle resources in het Hallo-abonnement verleent toevoegen. Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md). Hallo object-id-parameter, bieden Hallo Object-Id die u hebt gebruikt bij het maken van de toepassing hello. Voordat u deze opdracht uitvoert, moet u even totdat Hallo nieuwe service principal toopropagate in Azure Active Directory toestaan. Wanneer u deze opdrachten handmatig uitvoert, is meestal voldoende tijd verstreken tussen taken. In een script, moet u een stap toosleep tussen opdrachten Hallo toevoegen (zoals `sleep 15`). Als er dat een fout vermelden Hallo principal bestaat niet in de directory hello, moet u de opdracht Hallo opnieuw uitvoeren.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
Dat is alles. Uw AD-toepassing en service-principal worden ingesteld. de volgende sectie Hallo ziet u hoe toolog met Hallo referenties via Azure CLI. Als u wilt dat toouse Hallo referentie in uw toepassing code, hoeft u geen toocontinue met dit onderwerp. U kunt gaan toohello [voorbeeldtoepassingen](#sample-applications) voor voorbeelden van aangemeld met uw toepassings-id en wachtwoord. 

### <a name="provide-credentials-through-azure-cli"></a>Geef referenties op via Azure CLI
Nu moet u toolog in als Hallo toepassing tooperform bewerkingen.

1. Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app. Een tenant is een exemplaar van Azure Active Directory. tooretrieve hello tenant-id voor uw huidige geverifieerde abonnement, gebruiken:
   
   ```azurecli
   azure account show
   ```
   
   Die wordt geretourneerd:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Als u tooget hello tenant-id van een ander abonnement moet, gebruikt u Hallo volgende opdracht:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Als u tooretrieve Hallo client-id toouse voor logboekregistratie in nodig hebt, gebruikt:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     Hallo waarde toouse voor aanmelden is vermeld in de SPN-namen Hallo Hallo-guid.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Aanmelden als service-principal Hallo.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    U wordt gevraagd om Hallo wachtwoord. U hebt opgegeven bij het maken van de toepassing hello AD Hallo-wachtwoord opgeven.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

U bent nu geautoriseerd als Hallo service-principal voor Hallo service-principal die u hebt gemaakt.

U kunt ook de REST-bewerkingen van het Hallo opdrachtregel toolog in aanroepen. U kunt van antwoord Hallo-verificatie, Hallo toegangstoken voor gebruik met andere bewerkingen ophalen. Zie voor een voorbeeld van het toegangstoken Hallo ophalen door aan te roepen REST-bewerkingen [genereren van een Token toegang](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Service-principal maken met certificaat
In deze sectie kunt u Hallo stappen uitvoeren:

* Een zelfondertekend certificaat maken
* Hallo AD-toepassing maken met het Hallo-certificaat en Hallo service-principal
* Hallo lezer rol toohello service-principal toewijzen

toocomplete deze stappen, hebt u [OpenSSL](http://www.openssl.org/) geïnstalleerd.

1. Een zelfondertekend certificaat maken.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Hallo vóór stap gemaakt twee bestanden - privkey.pem en cert.pem. Hallo openbare en persoonlijke sleutels worden gecombineerd tot één bestand.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Open Hallo **examplecert.pem** bestand en zoek naar zeer lange reeks tekens tussen Hallo **---BEGIN CERTIFICATE---** en **---EINDCERTIFICAAT---**. Hallo certificaatgegevens kopiëren. U kunt deze gegevens als een parameter doorgeven bij het Hallo-service-principal maken.

4. Meld u aan tooyour-account.

   ```azurecli
   azure login
   ```
5. toocreate hello service-principal bieden Hallo-naam van het Hallo-app en de certificaatgegevens van Hallo, zoals wordt weergegeven in de volgende opdracht Hallo:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   Hallo nieuwe service-principal wordt geretourneerd. Hallo Object-Id is vereist bij het verlenen van machtigingen. Hallo-guid worden weergegeven met de Service Principal Names Hallo is nodig wanneer u zich aanmeldt. Deze guid is Hallo dezelfde waarde als Hallo app-id. Deze waarde is Hallo voorbeeldtoepassingen waarnaar wordt verwezen tooas Hallo Client-ID. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Machtigingen Hallo service principal op uw abonnement. In dit voorbeeld moet u Hallo service principal toohello lezer functie, die machtiging tooread alle resources in het Hallo-abonnement verleent toevoegen. Zie voor andere rollen, [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md). Hallo object-id-parameter, bieden Hallo Object-Id die u hebt gebruikt bij het maken van de toepassing hello. Voordat u deze opdracht uitvoert, moet u even totdat Hallo nieuwe service principal toopropagate in Azure Active Directory toestaan. Wanneer u deze opdrachten handmatig uitvoert, is meestal voldoende tijd verstreken tussen taken. In een script, moet u een stap toosleep tussen opdrachten Hallo toevoegen (zoals `sleep 15`). Als er dat een fout vermelden Hallo principal bestaat niet in de directory hello, moet u de opdracht Hallo opnieuw uitvoeren.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Geef het certificaat via automatische Azure CLI-script
Nu moet u toolog in als Hallo toepassing tooperform bewerkingen.

1. Wanneer u zich aanmeldt als een service-principal, moet u tooprovide hello tenant-id van Hallo directory voor uw AD-app. Een tenant is een exemplaar van Azure Active Directory. tooretrieve hello tenant-id voor uw huidige geverifieerde abonnement, gebruiken:
   
   ```azurecli
   azure account show
   ```
   
   Die wordt geretourneerd:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Als u tooget hello tenant-id van een ander abonnement moet, gebruikt u Hallo volgende opdracht:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve Hallo certificaatvingerafdruk en verwijder overbodige tekens, gebruiken:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   Die een vingerafdrukwaarde retourneert vergelijkbaar met:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Als u tooretrieve Hallo client-id toouse voor logboekregistratie in nodig hebt, gebruikt:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   Hallo waarde toouse voor aanmelden is vermeld in de SPN-namen Hallo Hallo-guid.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Aanmelden als service-principal Hallo.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

U bent nu geautoriseerd als Hallo service-principal voor hello Azure Active Directory-toepassing die u hebt gemaakt.

## <a name="change-credentials"></a>Referenties wijzigen

toochange hello referenties voor een AD-app, hetzij vanwege een beveiligingsinbreuk of een vervaldatum referentie gebruiken `azure ad app set`.

een wachtwoord, toochange gebruiken:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

de waarde van een certificaat toochange gebruiken:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Fouten opsporen

Hallo volgende fouten bij het maken van een service-principal kunnen optreden:

* **'Authentication_Unauthorized'** of **'geen abonnement gevonden in de context van Hallo'.** -U hebt deze fout te zien wanneer uw account geen Hallo [vereist machtigingen](#required-permissions) op Hallo Azure Active Directory tooregister een app. Normaal gesproken u deze fout te zien wanneer alleen admin gebruikers in uw Azure Active Directory apps registreren kunnen en uw account niet een beheerder is. Vraag uw beheerder tooeither tooan beheerdersrol of tooenable gebruikers tooregister apps toewijzen.

* Uw account **"heeft geen autorisatie tooperform actie 'Microsoft.Authorization/roleAssignments/write' bereik/subscriptions / {guid}."**  -Deze fout te zien wanneer uw account geen voldoende machtigingen tooassign tooan identiteit van een rol. Vraag uw beheerder abonnement tooadd u tooUser toegang beheerdersrol.

## <a name="sample-applications"></a>Voorbeeldtoepassingen
Zie voor informatie over logboekregistratie in als de toepassing hello via verschillende platforms:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Volgende stappen
* Zie voor gedetailleerde stappen voor het integreren van een toepassing in Azure voor het beheren van resources [Developer's guide tooauthorization Hello Azure Resource Manager-API](resource-manager-api-authentication.md).
* tooget meer informatie over het gebruik van certificaten en Azure CLI, Zie [certificaat gebaseerde verificatie met Azure Service-Principals vanaf de opdrachtregel Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd toousers [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).

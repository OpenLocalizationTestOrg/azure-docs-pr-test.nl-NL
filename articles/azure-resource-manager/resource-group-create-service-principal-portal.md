---
title: aaaCreate identiteit voor Azure portal-app | Microsoft Docs
description: Hierin wordt beschreven hoe toocreate een nieuwe Azure Active Directory-toepassing en service-principal die kan worden gebruikt met Hallo rollen gebaseerd toegangsbeheer in Azure Resource Manager toomanage toegang tooresources tot.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 7068617b-ac5e-47b3-a1de-a18c918297b6
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 9624715ac612f42df6f9e9e67b8233bd4b914174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-portal-toocreate-an-azure-active-directory-application-and-service-principal-that-can-access-resources"></a>Gebruik van toocreate portal een Azure Active Directory-toepassing en service-principal die toegang bronnen tot

Wanneer u een toepassing die moet tooaccess of wijzigen van resources hebt, moet u een Azure Active Directory (AD)-toepassing instellen en Hallo vereist machtigingen tooit toewijzen. Deze aanpak is beter toorunning Hallo app met uw eigen referenties, omdat:

* U kunt machtigingen toohello app identiteit die anders zijn dan uw eigen machtigingen toewijzen. Deze machtigingen zijn normaal gesproken beperkt tooexactly welke app Hallo moet toodo.
* U hebt geen toochange Hallo app referenties als uw verantwoordelijkheden wijzigen. 
* U kunt een tooautomate certificaatverificatie gebruiken bij het uitvoeren van een onbewaakt script.

Dit onderwerp leest u hoe tooperform die stapsgewijs Hallo-portal. Het is gericht op een één-tenant-toepassing waarbij de toepassing hello beoogde toorun binnen één organisatie is. Doorgaans gebruikt toepassingen voor één tenant voor line-of-business-toepassingen die worden uitgevoerd binnen uw organisatie.
 
## <a name="required-permissions"></a>Vereiste machtigingen
toocomplete in dit onderwerp, moet u voldoende machtigingen tooregister een toepassing hebt met uw Azure AD-tenant en de toepassingsrol tooa Hallo toewijzen in uw Azure-abonnement. Zorg ervoor dat u deze stappen tooperform van Hallo juiste machtigingen hebt.

### <a name="check-azure-active-directory-permissions"></a>Controleer de machtigingen voor Azure Active Directory
1. Meld u bij tooyour Azure-Account via Hallo [Azure-portal](https://portal.azure.com).
2. Selecteer **Azure Active Directory**.

     ![Selecteer azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)
3. Selecteer in Azure Active Directory, **gebruikersinstellingen**.

     ![gebruikersinstellingen voor de selecteren](./media/resource-group-create-service-principal-portal/select-user-settings.png)
4. Controleer de Hallo **App registraties** instelling. Als instellen te**Ja**, niet-beheerders kunnen zich registreren AD-apps. Deze instelling betekent dat elke gebruiker in Azure AD-tenant Hallo een app kunt registreren. U kunt verdergaan te[controleren Azure-abonnement machtigingen](#check-azure-subscription-permissions).

     ![app-registraties weergeven](./media/resource-group-create-service-principal-portal/view-app-registrations.png)
5. Als Hallo app registraties instellen te is ingesteld**Nee**, alleen de beheerder gebruikers apps kunnen registreren. U moet toocheck of uw account een beheerder voor hello Azure AD-tenant is. Selecteer **overzicht** en **een gebruiker zoeken** van snelle taken.

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/find-user.png)
6. Zoek uw account en selecteren wanneer u deze vinden.

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/show-user.png)
7. Selecteer voor uw account **functie Directory**. 

     ![Directory-rol](./media/resource-group-create-service-principal-portal/select-directory-role.png)
8. De functie toegewezen directory weergeven in Azure AD. Als uw account toohello gebruikersrol is toegewezen, maar hello app registratie-instelling (Hallo vorige stappen) beperkt tooadmin gebruikers is, vraag uw beheerder tooeither tooan beheerdersrol of tooenable gebruikers tooregister apps toewijzen.

     ![de rol weergeven](./media/resource-group-create-service-principal-portal/view-role.png)

### <a name="check-azure-subscription-permissions"></a>Controleer de machtigingen van de Azure-abonnement
In uw Azure-abonnement, uw account moet hebben `Microsoft.Authorization/*/Write` toegang tot een rol AD app tooa tooassign. Deze actie wordt verleend via Hallo [eigenaar](../active-directory/role-based-access-built-in-roles.md#owner) rol of [beheerder voor gebruikerstoegang](../active-directory/role-based-access-built-in-roles.md#user-access-administrator) rol. Als uw account is toegewezen toohello **Inzender** rol, u hebt niet de juiste machtiging. U ontvangt een fout opgetreden tijdens een poging de functie tooassign Hallo service-principal tooa. 

toocheck machtigingen voor uw abonnement:

1. Als u niet al op uw Azure AD-account van de vorige stappen hello, selecteer **Azure Active Directory** in het linkerdeelvenster Hallo.

2. Uw Azure AD-account vinden. Selecteer **overzicht** en **een gebruiker zoeken** van snelle taken.

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/find-user.png)
2. Zoek uw account en selecteren wanneer u deze vinden.

     ![gebruiker zoeken](./media/resource-group-create-service-principal-portal/show-user.png) 
     
3. Selecteer **Azure-resources**.

     ![Selecteer resources](./media/resource-group-create-service-principal-portal/select-azure-resources.png) 
3. De toegewezen rollen weergeven en bepalen of u onvoldoende machtigingen tooassign een AD-app tooa rol hebt. Als dit niet het geval is, vraagt u uw abonnement beheerder tooadd u tooUser toegang beheerdersrol. Hallo installatiekopie te volgen, is Hallo gebruiker toegewezen toohello rol van eigenaar voor twee abonnementen, wat betekent dat die de gebruiker heeft onvoldoende machtigingen. 

     ![machtigingen weergeven](./media/resource-group-create-service-principal-portal/view-assigned-roles.png)

## <a name="create-an-azure-active-directory-application"></a>Een Azure Active Directory-toepassing maken
1. Meld u bij tooyour Azure-Account via Hallo [Azure-portal](https://portal.azure.com).
2. Selecteer **Azure Active Directory**.

     ![Selecteer azure active directory](./media/resource-group-create-service-principal-portal/select-active-directory.png)

4. Selecteer **App registraties**.   

     ![Selecteer de app-registraties](./media/resource-group-create-service-principal-portal/select-app-registrations.png)
5. Selecteer **Toevoegen**.

     ![app toevoegen](./media/resource-group-create-service-principal-portal/select-add-app.png)

6. Geef een naam en de URL voor de toepassing hello. Selecteer een **Web-app / API** of **systeemeigen** Hallo type toepassing dat u wilt toocreate. Na het Hallo-waarden instellen, selecteer **maken**.

     ![de naam van toepassing](./media/resource-group-create-service-principal-portal/create-app.png)

U kunt uw toepassing hebt gemaakt.

## <a name="get-application-id-and-authentication-key"></a>Ophalen van de sleutel-ID en verificatie van toepassing
Wanneer u programmatisch zich aanmeldt, moet u Hallo-ID voor uw toepassing en een verificatiesleutel. tooget deze waarden, gebruik Hallo stappen te volgen:

1. Van **App registraties** in Azure Active Directory, selecteer uw toepassing.

     ![toepassing selecteren](./media/resource-group-create-service-principal-portal/select-app.png)
2. Kopiëren Hallo **toepassings-ID** en op te slaan in uw toepassingscode. toepassingen in Hallo Hallo [voorbeeldtoepassingen](#sample-applications) sectie toothis-waarde als de client-id Hallo verwijzen.

     ![client-id](./media/resource-group-create-service-principal-portal/copy-app-id.png)
3. Selecteer een verificatiesleutel toogenerate **sleutels**.

     ![Selecteer sleutels](./media/resource-group-create-service-principal-portal/select-keys.png)
4. Geef een beschrijving van het Hallo-sleutel en een duur voor het Hallo-sleutel. Wanneer u klaar bent, selecteer **opslaan**.

     ![sleutel opslaan](./media/resource-group-create-service-principal-portal/save-key.png)

     Na het opslaan van sleutel Hallo wordt Hallo-waarde van Hallo-sleutel weergegeven. Deze waarde niet kopiëren omdat u niet kunnen tooretrieve Hallo sleutel later bent. U geeft sleutelwaarde Hallo Hallo toepassing ID toolog in als de toepassing hello. Opslaan Hallo sleutelwaarde waar uw toepassing deze kan worden opgehaald.

     ![sleutel wordt opgeslagen](./media/resource-group-create-service-principal-portal/copy-key.png)

## <a name="get-tenant-id"></a>Tenant-ID ophalen
Wanneer u programmatisch zich aanmeldt, moet u toopass hello tenant-ID bij uw verificatieaanvraag. 

1. tooget hello tenant-ID, selecteer **eigenschappen** voor uw Azure AD-tenant. 

     ![Azure AD-eigenschappen selecteren](./media/resource-group-create-service-principal-portal/select-ad-properties.png)

2. Kopiëren Hallo **map-ID**. Deze waarde is uw tenant-ID.

     ![tenant-id](./media/resource-group-create-service-principal-portal/copy-directory-id.png)

## <a name="assign-application-toorole"></a>Toepassing toorole toewijzen
tooaccess resources in uw abonnement, moet u de toepassingsrol tooa Hallo toewijzen. Bepaal welke rol Hallo juiste machtigingen voor de toepassing hello vertegenwoordigt. toolearn over de beschikbare functies hello, Zie [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md).

U kunt Hallo bereik instellen op Hallo niveau van het Hallo-abonnement, resourcegroep of resource. Machtigingen zijn overgenomen toolower niveaus van het bereik. Bijvoorbeeld, vindt het toevoegen van dat een toepassing toohello lezersrol voor een resourcegroep betekent dat Hallo-resourcegroep en alle resources die deze bevat.

1. Toohello niveau van scope tooassign Hallo toepassing om te gewenst gaan. Bijvoorbeeld tooassign een rol op Hallo abonnementsbereik, selecteert u **abonnementen**. U kunt in plaats daarvan een resourcegroep of resource selecteren.

     ![Abonnement selecteren](./media/resource-group-create-service-principal-portal/select-subscription.png)

2. Hallo bepaald abonnement (resourcegroep of resource) tooassign Hallo toepassing te selecteren.

     ![Selecteer het abonnement voor de toewijzing](./media/resource-group-create-service-principal-portal/select-one-subscription.png)

3. Selecteer **toegangsbeheer (IAM)**.

     ![Selecteer toegang](./media/resource-group-create-service-principal-portal/select-access-control.png)

4. Selecteer **Toevoegen**.

     ![Selecteer toevoegen](./media/resource-group-create-service-principal-portal/select-add.png)
6. Selecteer desgewenst tooassign toohello toepassing hello-rol. Hallo volgende afbeelding toont Hallo **lezer** rol.

     ![rol selecteren](./media/resource-group-create-service-principal-portal/select-role.png)

8. Zoeken naar uw toepassing en selecteer deze.

     ![Zoek app](./media/resource-group-create-service-principal-portal/search-app.png)
9. Selecteer **OK** toofinish Hallo rol toewijst. Ziet u uw toepassing in de lijst Hallo tooa rol voor deze scope toegewezen aan gebruikers.

## <a name="log-in-as-hello-application"></a>Meld u aan als de toepassing hello

Uw toepassing is nu ingesteld in Azure Active Directory. U hebt een ID en sleutel toouse voor aanmelden als Hallo-toepassing. de toepassing Hello is tooa-rol die bepaalde acties die kan uitvoeren, krijgt het toegewezen. Zie voor informatie over logboekregistratie in als de toepassing hello via verschillende platforms:

* [PowerShell](resource-group-authenticate-service-principal.md#provide-credentials-through-powershell)
* [Azure CLI](resource-group-authenticate-service-principal-cli.md#provide-credentials-through-azure-cli)
* [REST](/rest/api/#create-the-request)
* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)


## <a name="next-steps"></a>Volgende stappen
* Zie tooset van een toepassing met meerdere tenants [Developer's guide tooauthorization Hello Azure Resource Manager-API](resource-manager-api-authentication.md).
* toolearn over het opgeven van beveiligingsbeleid, Zie [toegangsbeheer op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md).  
* Zie voor een lijst met beschikbare acties die kunnen worden verleend of geweigerd toousers [Resourceprovider van Azure Resource Manager operations](../active-directory/role-based-access-control-resource-provider-operations.md).

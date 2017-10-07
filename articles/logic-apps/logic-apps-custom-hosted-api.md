---
title: "aaaDeploy, aanroepen en verifiëren van web-API's & REST-API's voor Azure Logic Apps | Microsoft Docs"
description: "Implementeren, te verifiëren en web-API's & REST-API's aanroepen in werkstromen voor systeemintegraties met Azure Logic Apps"
keywords: "Web-API's, REST-API's, connectors, werkstromen, systeemintegraties, verifiëren"
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a>Implementeren en verifiëren van aangepaste API's als connectors voor logic apps aanroepen

Nadat u [maken van aangepaste API's](./logic-apps-create-api-app.md) die acties of triggers toouse in logic apps werkstromen bieden, moet u uw API's implementeren voordat u ze kunt aanroepen. En hoewel voor de beste ervaring hello, u API vanuit een logische app aanroepen kunt, toe te voegen [Swagger-metagegevens](http://swagger.io/specification/) die uw API bewerkingen en parameters beschrijft. Dit bestand Swagger helpt uw API werken beter en eenvoudiger te integreren met logische apps.

U kunt uw API's als implementeren [web-apps](../app-service-web/app-service-web-overview.md), maar overweeg het implementeren van uw API's als [API-apps](../app-service-api/app-service-api-apps-why-best-platform.md), zodat u uw taak gemakkelijker wanneer ontwikkelen, hosten en API's in Hallo cloud en on-premises gebruiken. Er geen toochange code in de API's, u hoeft de code tooan API-app te implementeren. U kunt uw API's hosten op [Azure App Service](../app-service/app-service-value-prop-what-is.md), een platform-as-a-service (PaaS) die het beste eenvoudigste en meest schaalbare manieren Hallo biedt voor het hosten van de API.

tooauthenticate aanroepen vanuit logic apps tooyour API's, u kunt instellen Azure Active Directory in hello Azure-portal dus u geen tooupdate uw code hebt. Of u kunt vereisen en afdwingen van verificatie via de API-code.

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a>Uw API als een web-app of API-app implementeren

Voordat u uw aangepaste API vanuit een logische app aanroepen kunt, implementeert u uw API als een web-app of API-app tooAzure App Service. Ook toomake uw Swagger document gelezen door Hallo Logic App-ontwerper, Hallo API-definitie-eigenschappen instellen en inschakelen [cross-origin-resource delen (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) voor uw web-app of API-app.

1. In hello Azure-portal, selecteer uw web-app of API-app.

2. Hallo-blade die wordt geopend, klikt u onder **API**, kies **API-definitie**. Set Hallo **locatie voor API-definitie** toohello-URL voor uw swagger.json-bestand.

   Normaal gesproken Hallo-URL wordt weergegeven in deze indeling:`https://{name}.azurewebsites.net/swagger/docs/v1)`

   ![Koppeling tooSwagger-bestand voor uw aangepaste API gebruiken](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. Onder **API**, kies **CORS**. Hallo CORS beleid instellen voor **toegestane oorsprongen** te**'*'** (alle toestaan).

   Deze instelling kan aanvragen van Logic App-ontwerper.

   ![Toestaan van aanvragen van Logic App-ontwerper tooyour aangepaste API](media/logic-apps-custom-hosted-api/custom-api-cors.png)

Zie voor meer informatie in deze artikelen:

* [Swagger-metagegevens voor ASP.NET web-API's toevoegen](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [ASP.NET web API's tooAzure App Service implementeren](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a>Uw aangepaste API aanroepen vanuit logic app-werkstromen

Na het instellen van eigenschappen van Hallo API-definitie en CORS, moeten triggers en acties van uw aangepaste API beschikbaar worden voor tooinclude in uw logische app-werkstroom. 

*  tooview hello websites die Swagger URL's hebben, kunt u uw abonnement websites in Hallo Logic Apps Designer bladeren.

*  de beschikbare acties tooview en invoer door aan te wijzen op een Swagger-document gebruiken Hallo [HTTP + Swagger actie](../connectors/connectors-native-http-swagger.md).

*  toocall API, met inbegrip van API's die niet hebt of blootstellen van een Swagger-document, kunt u altijd een aanvraag maken met de Hallo [HTTP-actie](../connectors/connectors-native-http.md).

## <a name="authenticate-calls-tooyour-custom-api"></a>Aangepaste tooyour-API aanroepen verifiëren

U kunt beveiligen aanroepen tooyour aangepaste API op de volgende manieren:

* [Er is geen codewijzigingen](#no-code): uw API beveiligen met [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) via hello Azure-portal, zodat u niet hebt tooupdate uw code of implementeren van uw API.

  > [!NOTE]
  > Standaard bieden niet hello Azure AD authentication die u in Azure-portal Hallo inschakelen fijnmazig autorisatie. Deze verificatie wordt bijvoorbeeld uw API-toojust vergrendeld een specifieke tenant, niet tooa specifieke gebruiker of app. 

* [Werk uw API-code](#update-code): uw API beveiligen door af te dwingen [certificaatverificatie](#certificate), [basisverificatie](#basic), of [Azure AD authentication](#azure-ad-code) via code.

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a>Aanroepen tooyour API verifiëren zonder code te wijzigen

Hier volgt de algemene stappen Hallo voor deze methode:

1. Maak twee [Azure Active Directory (Azure AD) toepassing identiteiten](../app-service-api/app-service-api-dotnet-service-principal-auth.md): één voor uw logische app en één voor uw web-app (of API-app).

2. tooauthenticate aanroepen tooyour API, Hallo referenties (client-ID en geheim) gebruikt voor Hallo [service-principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) die gekoppeld is aan hello Azure AD-toepassingsidentiteit voor uw logische app.

3. Hallo toepassing id's in de definitie van de logische app opnemen.

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a>Deel 1: Een Azure AD-toepassings-id voor uw logische app maken

Uw logische app maakt gebruik van deze Azure AD-toepassing identiteit tooauthenticate met Azure AD. U hoeft alleen tooset van deze identiteit voor uw directory. U kunt bijvoorbeeld toouse Hallo dezelfde identiteit voor alle logic apps, zelfs als u de unieke id's voor elke logische app kunt maken. U kunt deze identiteiten in hello Azure-portal instellen [klassieke Azure-portal](#app-identity-logic-classic), of gebruik [PowerShell](#powershell).

**Hallo toepassings-id voor uw logische app maken in hello Azure-portal**

1. In Hallo [Azure-portal](https://portal.azure.com "https://portal.azure.com"), kies **Azure Active Directory**. 

2. Bevestig dat u bent klaar Hallo dezelfde directory als uw web-app of API-app.

   > [!TIP]
   > tooswitch mappen, klikt u op uw profiel en selecteer een andere map. Of kies **overzicht** > **Switch directory**.

3. Hallo directory menu onder **beheren**, kies **App registraties** > **registratie van de nieuwe toepassing**.

   > [!TIP]
   > Standaard worden alle app-registraties Hallo app registraties lijst weergegeven in uw directory. selecteert u alleen uw app registraties, volgende toohello zoekvak tooview **mijn apps**. 

   ![Maken van nieuwe app-registratie](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. Geef een naam op voor de toepassingsidentiteit van uw, laat u **toepassingstype** instellen te**Web-app / API**, bieden een unieke tekenreeks die is opgemaakt als een domein voor **aanmeldings-URL**, en kies  **Maak**.

   ![Geef de naam van en aanmelding URL voor toepassings-id](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   Hallo toepassings-id die u hebt gemaakt voor uw logische app wordt nu weergegeven in Hallo app registraties lijst.

   ![Toepassings-id voor uw logische app](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. Selecteer de nieuwe toepassingsidentiteit in Hallo app registraties lijst. Kopiëren en opslaan van Hallo **toepassings-ID** toouse zoals Hallo 'client-ID' voor uw logische app in deel 3.

   ![Kopiëren en opslaan van toepassings-ID voor de logische app](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. Als de identity-instellingen van de toepassing niet weergegeven worden, kiest u **instellingen** of **alle instellingen**.

7. Onder **API-toegang**, kies **sleutels**. Onder **beschrijving**, Geef een naam voor uw sleutel. Onder **verloopt**, selecteert u een duur voor uw sleutel.

   Hallo-sleutel die u maakt, fungeert als Hallo toepassings-id van 'geheime' of het wachtwoord voor uw logische app.

   ![Sleutel voor de id van logische app maken](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. Kies op de werkbalk Hallo **opslaan**. Onder **waarde**, uw sleutel wordt nu weergegeven. 
**Zorg ervoor dat toocopy en opslaan van uw sleutel** voor later gebruik omdat Hallo-sleutel wordt verborgen wanneer u laat Hallo sleutel blade.

   Wanneer u uw logische app in deel 3 configureert, geeft u deze sleutel als Hallo 'geheime' of het wachtwoord.

   ![Kopieer en sleutel opslaan voor later](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

**Hallo toepassings-id voor uw logische app maken in Hallo klassieke Azure-portal**

1. In de klassieke Azure-portal Hallo, kiest u [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2. Selecteer Hallo dezelfde map die u voor uw web-app of API-app gebruikt.

3. Op Hallo **toepassingen** Kies **toevoegen** Hallo Hallo pagina onderaan in.

4. Geef een naam op voor de toepassingsidentiteit van uw en kies **volgende** (pijl naar rechts).

5. Onder **App-eigenschappen**, Geef een unieke tekenreeks die is opgemaakt als een domein voor **aanmeldings-URL** en **App ID URI**, en kies **Complete** (vinkje).

6. Op Hallo **configureren** tabblad, kopiëren en opslaan van Hallo **Client-ID** voor uw logische app toouse in deel 3.

7. Onder **sleutels**Open Hallo **Selecteer duur** lijst. Selecteer een duur voor de sleutel.

   Hallo-sleutel die u maakt, fungeert als Hallo toepassings-id van 'geheime' of het wachtwoord voor uw logische app.

8. Aan de onderkant van de Hallo van Hallo pagina, kies **opslaan**. Mogelijk hebt u toowait een paar seconden.

9. Onder **sleutels**, zorg ervoor dat toocopy en slaat u Hallo-sleutel die wordt nu weergegeven. 

   Wanneer u uw logische app in deel 3 configureert, geeft u deze sleutel als Hallo 'geheime' of het wachtwoord.

Voor meer informatie meer informatie over hoe te [configureren van uw App Service-toepassing toouse Azure Active Directory-aanmelding](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).

<a name="powershell"></a>

**Hallo toepassings-id voor uw logische app maken in PowerShell**

U kunt deze taak via Azure Resource Manager met PowerShell uitvoeren. Voer deze opdrachten uit in PowerShell:

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. Zorg ervoor dat toocopy hello **Tenant-ID** (GUID voor uw Azure AD-tenant), Hallo **toepassings-ID**, en het Hallo-wachtwoord die u hebt gebruikt.

Voor meer informatie meer informatie over hoe te [een service-principal maken met PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a>Deel 2: Een Azure AD-toepassings-id voor uw web-app of API-app maken

Als uw web-app of API-app al is geïmplementeerd, kunt u verificatie inschakelen en Hallo toepassings-id maken in hello Azure-portal. Anders kunt u [authentication inschakelen wanneer u met een Azure Resource Manager-sjabloon implementeert](#authen-deploy). 

**Hallo toepassings-id maken en verificatie in hello Azure-portal voor geïmplementeerde apps inschakelen**

1. In Hallo [Azure-portal](https://portal.azure.com "https://portal.azure.com"), zoeken en selecteert u uw web-app of API-app. 

2. Onder **instellingen**, kies **verificatie/autorisatie**. Onder **verificatie van App Service**, schakelt u verificatie **op**. Onder **verificatieproviders**, kies **Azure Active Directory**.

   ![Authentication inschakelen](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. Maak nu een toepassings-id voor uw web-app of API-app zoals hier wordt weergegeven. Op Hallo **Azure Active Directory-instellingen** blade ingesteld **beheermodus** te**Express**. Kies **nieuwe AD-App maken**. Geef een naam op voor de toepassingsidentiteit van uw en kies **OK**. 

   ![Toepassings-id voor uw web-app of API-app maken](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. Op Hallo **verificatie / autorisatie-blade**, kies **opslaan**.

U moet nu Hallo client-ID vinden en tenant-ID voor Hallo toepassings-id die is gekoppeld aan uw web-app of API-app. U gebruikt deze id in deel 3. Dus doorgaan met deze stappen voor hello Azure-portal of [klassieke Azure-portal](#find-id-classic).

**Toepassings-id client-ID vinden en tenant-ID voor uw web-app of API-app in hello Azure-portal**

1. Onder **verificatieproviders**, kies **Azure Active Directory**. 

   !['Azure Active Directory' kiezen](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. Op Hallo **Azure Active Directory-instellingen** blade ingesteld **beheermodus** te**Geavanceerd**.

3. Kopiëren Hallo **Client-ID**, en sla deze GUID voor gebruik in deel 3.

   > [!TIP] 
   > Als **Client-ID** en **Url-verlener** niet worden weergegeven, vernieuw hello Azure-portal en Herhaal stap 1.

4. Onder **Url-verlener**, kopiëren en opslaan net hello GUID voor deel 3. U kunt ook deze GUID gebruiken in uw web-app of sjabloon API-app-implementatie, indien nodig.

   Deze GUID is van de tenant van uw specifieke GUID ('tenant-ID') en moet worden weergegeven in deze URL:`https://sts.windows.net/{GUID}`

5. Sluit zonder de wijzigingen worden opgeslagen, Hallo **Azure Active Directory-instellingen** blade.

<a name="find-id-classic"></a>

**Toepassings-id client-ID vinden en tenant-ID voor uw web-app of API-app in de klassieke Azure-portal Hallo**

1. In de klassieke Azure-portal Hallo, kiest u [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).

2.  Hallo directory selecteren die u voor uw web-app of API-app gebruikt.

3. In Hallo **Search** , zoeken en kiest u Hallo toepassings-id voor uw web-app of API-app.

4. Op Hallo **configureren** tabblad, kopie Hallo **Client-ID**, en sla deze GUID voor gebruik in deel 3.

5. Nadat u Hallo client-ID aan de onderkant Hallo Hallo **configureren** Kies **eindpunten weergeven**.

6. Kopieer de URL Hallo voor **Document met federatieve metagegevens**, en blader toothat URL.

7. Zoeken in het document metagegevens Hallo dat wordt geopend, Hallo hoofdmap **EntityDescriptor ID** -element, wat is een **id van de entiteit** kenmerk in dit formulier:`https://sts.windows.net/{GUID}` 

      Hallo GUID in dit kenmerk is van de tenant van uw specifieke GUID (tenant-ID).

8. Hallo tenant-ID kopiëren en opslaan van die ID voor gebruik in deel 3 en toouse in uw web-app of sjabloon API-app-implementatie, indien nodig.

Zie de volgende onderwerpen voor meer informatie:

* [Gebruikersverificatie voor API-apps in Azure App Service](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [Verificatie en autorisatie in Azure App Service](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

**Verificatie inschakelen wanneer u met een Azure Resource Manager-sjabloon implementeren**

U moet nog steeds een Azure AD-toepassings-id voor uw web-app of API-app die verschilt Hallo app identiteit maken voor uw logische app. Deel 2 stappen toocreate Hallo toepassingsidentiteit, volg Hallo vorige voor hello Azure-portal. U kunt ook Hallo stappen in deel 1 maar zorg ervoor dat toouse uw web-app of API-app werkelijke `https://{URL}` voor **aanmeldings-URL** en **App ID URI**. Van deze stappen hebt u toosave zowel Hallo-client-ID en tenant-ID voor gebruik in uw app implementatiesjabloon en ook voor deel 3.

> [!NOTE]
> Wanneer u hello Azure AD-toepassings-id voor uw web-app of API-app maakt, moet u hello Azure-portal of klassieke Azure-portal, in plaats van PowerShell. Hallo PowerShell-cmdlet niet Hallo vereist machtigingen instellen toosign gebruikers in een website.

Nadat u Hallo client-ID en tenant-ID hebt ontvangen, moet u deze id opnemen als een subresource van uw web-app of API-app in de implementatiesjabloon voor:

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

tooautomatically een leeg web-app en een logische app samen met Azure Active Directory-verificatie implementeren [Hallo volledige sjabloon weergeven hier](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), of klik op **tooAzure implementeren** hier:

[![TooAzure implementeren](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a>Deel 3: Hallo autorisatie-sectie in uw logische app vullen

Hallo vorige sjabloon is al in deze sectie autorisatie is ingesteld, maar als u rechtstreeks Hallo logische app maakt, moet u Hallo volledige autorisatie sectie opnemen.

Open de definitie van de logische app in de codeweergave Ga toohello **HTTP** sectie actie, zoeken Hallo **autorisatie** sectie en deze regel:

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| Element | Beschrijving |
| ------- | ----------- |
| Tenant |Hallo GUID voor hello Azure AD-tenant |
| doelgroep |Vereist. Hallo GUID voor Hallo doelresource dat u wilt dat tooaccess - Hallo client-ID van Hallo toepassings-id voor uw web-app of API-app |
| clientId |Hallo GUID voor Hallo client access - client-ID Hallo van Hallo toepassings-id voor uw logische app aanvragen |
| Geheim |Vereist. Hallo sleutel of het wachtwoord van Hallo toepassings-id voor Hallo-client die Hallo toegangstoken aanvraagt |
| type |Hallo verificatietype. Hallo-waarde voor ActiveDirectoryOAuth verificatie, heeft `ActiveDirectoryOAuth`. |

Bijvoorbeeld:

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a>Beveiligde API-aanroepen via code

<a name="certificate"></a>

#### <a name="certificate-authentication"></a>Verificatie via certificaat

toovalidate hello binnenkomende aanvragen van uw logische app tooyour WebApp of API-app, kunt u clientcertificaten. tooset om uw code meer [hoe tooconfigure TLS wederzijdse verificatie](../app-service-web/app-service-web-configure-tls-mutual-auth.md).

In Hallo **autorisatie** sectie, voeg deze regel: 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| Element | Beschrijving |
| ------- | ----------- |
| type |Vereist. Hallo verificatietype. Voor SSL-clientcertificaten moet Hallo waarde `ClientCertificate`. |
| wachtwoord |Vereist. Hallo-wachtwoord voor toegang tot het clientcertificaat hello (PFX-bestand) |
| PFX |Vereist. Base64-gecodeerde inhoud van het clientcertificaat hello (PFX-bestand) |

<a name="basic"></a>

#### <a name="basic-authentication"></a>Basisverificatie

inkomende aanvragen toovalidate van uw logische app tooyour WebApp of API-app, kunt u basisverificatie, zoals een gebruikersnaam en wachtwoord. Basisverificatie is een algemene patroon en kunt u deze verificatie in een toobuild taal wordt gebruikt voor uw web-app of API-app.

In Hallo **autorisatie** sectie, voeg deze regel:

`{"type": "basic", "username": "username", "password": "password"}`.

| Element | Beschrijving |
| --- | --- |
| type |Vereist. Hallo verificatietype. Voor basisverificatie, moet Hallo waarde `Basic`. |
| gebruikersnaam |Vereist. Hallo-gebruikersnaam voor verificatie |
| wachtwoord |Vereist. Hallo-wachtwoord voor verificatie |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a>Azure Active Directory-verificatie via code

Standaard bieden niet hello Azure AD authentication die u in Azure-portal Hallo inschakelen fijnmazig autorisatie. Deze verificatie wordt bijvoorbeeld uw API-toojust vergrendeld een specifieke tenant, niet tooa specifieke gebruiker of app. 

toorestrict API toegang tooyour logische app via programmacode, pak Hallo-header die heeft Hallo JSON web token (JWT). Controleer Hallo aanroeper ID en aanvragen die niet overeenkomen met weigeren.

Doorgaat, tooimplement deze verificatie volledig in uw eigen code en geen gebruik hello Azure-portal, informatie over hoe te [verificatie met de lokale Active Directory in uw app in Azure](../app-service-web/web-sites-authentication-authorization.md).

een toepassings-id voor uw logische app toocreate en die identiteit toocall uw API gebruiken, moet u de vorige stappen Hallo volgen.

## <a name="next-steps"></a>Volgende stappen

* [Logica van app-prestaties met diagnostische logboeken en waarschuwingen controleren](logic-apps-monitor-your-logic-apps.md)
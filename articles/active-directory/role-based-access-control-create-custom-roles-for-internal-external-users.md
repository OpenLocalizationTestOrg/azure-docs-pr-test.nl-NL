---
title: aaaCreate aangepaste op rollen gebaseerde toegangsbeheer rollen en toe te wijzen toointernal en externe gebruikers in Azure | Microsoft Docs
description: Aangepaste RBAC-rollen gemaakt met behulp van PowerShell en CLI voor interne en externe gebruikers toewijzen
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a>Inleiding op rollen gebaseerd toegangsbeheer

Toegangsbeheer op basis van rollen is een Azure portal alleen functie zodat Hallo eigenaren van een abonnement tooassign gedetailleerde rollen tooother gebruikers die een specifieke bron scopes in hun omgeving kunnen beheren.

RBAC kan beter beveiligingsbeheer voor grote organisaties en voor midden-en kleinbedrijf werkt met externe deelnemers, leveranciers of freelancers die moeten toegang hebben tot bronnen in uw omgeving, maar niet noodzakelijkerwijs toohello gehele infrastructuur of een willekeurige toospecific Facturering-gerelateerde scopes. RBAC kan Hallo flexibiliteit van die eigenaar is van een Azure-abonnement beheerd door Hallo administrator-account (service-beheerdersrol op abonnementsniveau) en hebben meerdere gebruikers uitgenodigd toowork onder Hallo hetzelfde abonnement maar zonder een administratieve rechten voor. Hallo RBAC functie bewijst toobe een tijd- en efficiënte optie voor het gebruik van Azure in verschillende scenario's van een management en facturering perspectief.

## <a name="prerequisites"></a>Vereisten
Het gebruik van RBAC in hello Azure-omgeving vereist:

* Een zelfstandige met Azure-abonnement toohello gebruiker toegewezen als eigenaar (abonnement rol)
* Rol van eigenaar Hallo Hallo Azure-abonnement hebt
* Hebt u toegang toohello [Azure-portal](https://portal.azure.com)
* Zorg ervoor dat toohave hello Resourceproviders te volgen die zijn geregistreerd voor Hallo gebruikerabonnement: **Microsoft.Authorization**. Zie voor meer informatie over hoe tooregister resourceproviders hello, [Resource Manager-providers, regio's, API-versies en schema's](/azure-resource-manager/resource-manager-supported-services.md).

> [!NOTE]
> Abonnementen voor Office 365 of Azure Active Directory-licenties (bijvoorbeeld: toegang tot Active Directory tooAzure) vanaf Hallo O365 portal niet kwaliteit voor met RBAC wordt ingericht.

## <a name="how-can-rbac-be-used"></a>Hoe RBAC kan worden gebruikt
RBAC kan worden toegepast op drie verschillende bereiken in Azure. Van Hallo hoogste bereik toohello laagste één zijn ze als volgt:

* Abonnement (hoogste)
* Resourcegroep
* Resource-bereik (Hallo laagste toegangsniveau gerichte machtigingen tooan afzonderlijke Azure-resource bereik aanbieden)

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a>RBAC-rollen op Hallo abonnementsbereik toewijzen
Er zijn twee algemene voorbeelden wanneer RBAC is gebruikt (maar niet tot beperkt):

* Externe gebruikers van Hallo organisaties (die geen deel uit van Azure Active Directory-tenant Hallo beheerder van de gebruiker) met uitgenodigd toomanage bepaalde resources of de hele abonnement Hallo
* Werken met gebruikers binnen het Hallo-organisatie (ze zijn onderdeel van een van de gebruiker hello Azure Active Directory-tenant), maar deel uitmaken van verschillende teams of groepen die gedetailleerde toegang moeten beide toohello hele abonnement of toocertain resourcegroepen of de resource-bereiken in Hallo omgeving

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a>Toegang verlenen op het abonnementsniveau van een voor een gebruiker buiten Azure Active Directory
RBAC-rollen kunnen alleen worden toegekend **eigenaars** van Hallo abonnement daarom Hallo beheerder moet zijn aangemeld met een gebruikersnaam die deze rol is een vooraf toegewezen of hello Azure-abonnement is gemaakt.

Van hello Azure-portal, na het aanmelden als beheerder, selecteer 'Abonnementen' en gekozen Hallo gewenste een.
![abonnementsblade in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) standaard als gebruiker met beheerdersrechten Hallo hello Azure-abonnement heeft aangeschaft Hallo gebruiker wordt weergegeven als **accountbeheerder**, deze wordt Hallo abonnement rol. Zie voor meer informatie over hello Azure-abonnement rollen [toevoegen of wijzigen Azure-beheerdersrollen die Hallo abonnement of services beheren](/billing/billing-add-change-azure-subscription-administrator.md).

In dit voorbeeld Hallo gebruiker "alflanigan@outlook.com' hello is **eigenaar** Hallo 'Gratis' abonnement in Hallo AAD-tenant 'tenant Azure Default'. Omdat deze gebruiker Hallo maker van hello Azure-abonnement met Hallo initiële Microsoft-Account 'Outlook' (Microsoft-Account = Outlook, etc. Live) Hallo standaarddomeinnaam voor andere gebruikers die zijn toegevoegd aan deze tenant zijn **'@alflaniganuoutlook.onmicrosoft.com'**. Standaard Hallo syntaxis van het nieuwe domein hello wordt gevormd door het samenstellen van Hallo gebruikersnaam en domein op naam van Hallo-gebruiker die Hallo-tenant en toe te voegen Hallo extensie gemaakt **'. onmicrosoft.com '**.
Bovendien gebruikers kunnen aanmelden met een aangepaste domeinnaam in Hallo tenant na het toevoegen en verifiëren van deze voor de nieuwe tenant Hallo. Voor meer informatie over hoe tooverify een aangepaste domeinnaam in Azure Active Directory-tenant, Zie [toevoegen van een aangepast domein naam tooyour map](/active-directory/active-directory-add-domain).

In dit voorbeeld bevat Hallo ' standaard Azure ' tenantmap alleen gebruikers met de domeinnaam Hallo '@alflanigan.onmicrosoft.com'.

Na het selecteren van abonnement Hallo Hallo beheerder gebruiker klikt op **Access Control (IAM)** en vervolgens **een nieuwe rol toevoegen**.





![onderdeel voor toegangsbeheer IAM-functie in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![nieuwe gebruiker toevoegen in het onderdeel voor toegangsbeheer IAM-functie in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

de volgende stap Hallo is tooselect Hallo rol toobe toegewezen en Hallo gebruiker wie Hallo RBAC-rol wordt toegewezen aan. In Hallo **rol** dropdown menu Hallo beheerder gebruiker ziet alleen Hallo ingebouwde RBAC functies die beschikbaar in Azure zijn. Zie voor meer uitleg van elke rol en hun toewijsbare bereiken gedetailleerde, [ingebouwde functies voor op rollen gebaseerd toegangsbeheer](/active-directory/role-based-access-built-in-roles.md).

Hallo beheerder gebruiker moet vervolgens tooadd Hallo e-mailadres van de externe gebruiker Hallo. Hallo verwacht gedrag is voor Hallo externe gebruiker toonot worden weergegeven in Hallo bestaande tenant. Nadat de externe gebruiker Hallo heeft uitgenodigd, hij zijn zichtbaar onder **abonnementen > Access Control (IAM)** met alle Hallo actieve gebruikers dat momenteel een RBAC-rol op Hallo abonnementsbereik zijn toegewezen.





![machtigingen toonew RBAC-rol toevoegen](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![lijst met RBAC-rollen op abonnementsniveau](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

Hallo-gebruiker 'chessercarlton@gmail.com' uitgenodigde toobe is een **eigenaar** voor Hallo ' gratis ' proefabonnement. Na het verzenden van een uitnodiging voor Hallo ontvangen Hallo externe gebruiker een e-mailbevestiging met een activeringskoppeling.
![e-uitnodiging voor RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)

Alleen externe toohello organisatie, heeft Hallo nieuwe gebruiker geen bestaande kenmerken in Hallo 'tenant Azure Default' directory. Ze worden gemaakt nadat de externe gebruiker Hallo heeft toestemming toobe vastgelegd in Hallo directory, die is gekoppeld aan Hallo-abonnement dat hij een rol is toegewezen.





![e-mailbericht uitnodiging voor RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

ziet u de externe gebruiker Hallo in hello Azure Active Directory-tenant op als de externe gebruiker en deze kan worden bekeken in hello Azure-portal en in de klassieke portal Hallo.





![gebruikers blade azure active directory Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![gebruikers blade azure active directory klassieke Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

In Hallo **gebruikers** weergave in beide portals Hallo externe gebruikers kan worden herkend door:

* Hallo ander Pictogramtype in hello Azure-portal
* Hallo verschillende punt in de klassieke portal Hallo bron

Echter, verlenen **eigenaar** of **Inzender** toegang tooan externe gebruiker op Hallo **abonnement** bereik, staat niet toe dat Hallo toegang toohello-beheerder de map van gebruiker, tenzij Hallo **globale beheerder** is toegestaan. In de eigenschappen van de gebruiker hello, Hallo **gebruikerstype** die heeft twee algemene parameters, **lid** en **Gast** kunnen worden geïdentificeerd. Een lid is van een gebruiker die is geregistreerd in de map Hallo terwijl een gast een map van de gebruiker verzocht toohello van een externe bron is. Zie voor meer informatie [hoe Azure Active Directory-beheerders Voeg B2B-samenwerking gebruikers](/active-directory/active-directory-b2b-admin-add-users).

> [!NOTE]
> Zorg ervoor dat de externe gebruiker Hallo na het invoeren van Hallo-referenties in portal Hallo, de juiste map Hallo toosign bij selecteert. Hallo kan dezelfde gebruiker toegang toomultiple mappen hebt en kunt selecteert u een van deze door te klikken op Hallo gebruikersnaam in Hallo rechterbovenhoek in hello Azure-portal en kies vervolgens de overeenkomstige map Hallo uit de vervolgkeuzelijst Hallo.

Terwijl een gast in Hallo directory, Hallo externe gebruiker alle resources voor hello Azure-abonnement kunt beheren, maar geen toegang tot Hallo-directory.





![toegang tot Azure active directory-portal beperkte tooazure](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

Azure Active Directory en een Azure-abonnement niet hebben een relatie van de onderliggende structuur met bovenliggende net als andere Azure-resources (bijvoorbeeld: virtuele machines, virtuele netwerken, web-apps, opslag, enzovoort) met een Azure-abonnement hebt. Alle Hallo laatstgenoemde is gemaakt, beheerd en onder een Azure-abonnement in rekening gebracht terwijl een Azure-abonnement gebruikte toomanage Hallo toegang tooan Azure-map is. Zie voor meer informatie [hoe een Azure-abonnement is gerelateerd tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).

Uit alle Hallo ingebouwde RBAC rollen, **eigenaar** en **Inzender** bieden volledige beheertoegang tooall bronnen Hallo-omgeving, Hallo verschil wordt die een medewerker kan niet worden gemaakt en nieuwe verwijderen RBAC-rollen. Hallo andere ingebouwde rollen, zoals **Virtual Machine Contributor** bieden volledige beheertoegang alleen toohello resources aangegeven door de naam hello, ongeacht Hallo **resourcegroep** ze worden gemaakt in.

Toewijzen Hallo ingebouwde RBAC-rol van **Virtual Machine Contributor** op abonnementsniveau, betekent dat Hallo toegewezen Hallo gebruikersrol:

* Alle virtuele machines ongeacht hun implementatie van de datum en het Hallo resource-groepen kunt weergeven die ze deel van uitmaken
* Heeft volledige toegang toohello virtuele beheermachines in Hallo-abonnement
* Andere brontypen weergeven in Hallo abonnement niet
* Kan niet worden uitgevoerd vanuit het oogpunt van facturering van wijzigingen

> [!NOTE]
> RBAC wordt een enige functie van Azure portal, verlenen geen toegang toohello klassieke portal.

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a>Een ingebouwde RBAC-rol tooan externe gebruiker toewijzen
Hallo externe gebruiker voor een ander scenario in deze test 'alflanigan@gmail.com' wordt toegevoegd als een **Virtual Machine Contributor**.




![virtuele machine ingebouwde rol van Inzender](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

Hallo normaal gedrag voor deze externe gebruiker met deze ingebouwde functie toosee is en alleen virtuele machines en hun aangrenzende Resource Manager alleen bronnen nodig zijn tijdens de implementatie beheren. Door het ontwerp van deze rollen beperkt bieden toegang alleen tootheir corresponderende resources in hello Azure-portal hebt gemaakt, ongeacht sommige kan nog steeds worden geïmplementeerd in Hallo klassieke portal ook (bijvoorbeeld: virtuele machines).





![overzicht van virtuele machines Inzender rol in azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a>Ken toegang tot op het abonnementsniveau van een voor een gebruiker in Hallo dezelfde directory
Processtroom Hallo is identiek tooadding een externe gebruiker zowel in Hallo beheerder perspectief verlenen Hallo RBAC-rol, evenals Hallo gebruiker toohello-toegangsfunctie wordt verleend. Hallo verschil is hier is dat die Hallo uitgenodigd gebruiker ontvangt geen uitnodigingen voor een e-mailadres als alle Hallo resource scopes binnen Hallo abonnement beschikbaar in Hallo dashboard zijn na het aanmelden.

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a>RBAC-rollen op Hallo resource groepsbereik toewijzen
Toewijzen van een RBAC-rol op een **resourcegroep** scope heeft een identieke proces voor het toewijzen van Hallo-rol op Hallo abonnementsniveau, voor beide typen gebruikers - externe of interne (onderdeel van Hallo dezelfde directory). Hallo gebruikers die zijn toegewezen Hallo RBAC-rol is toosee in hun omgeving alleen Hallo resourcegroep ze zijn toegewezen toegang van Hallo **resourcegroepen** pictogram in hello Azure-portal.

## <a name="assign-rbac-roles-at-hello-resource-scope"></a>RBAC-rollen op Hallo resource bereik toewijzen
Toewijzen van een RBAC-rol op een scope resource in Azure heeft een identieke proces voor het toewijzen van Hallo-rol op Hallo abonnementsniveau of op niveau van de resourcegroep hello, volgende Hallo dezelfde werkstroom voor beide scenario's. Hallo-gebruikers die zijn toegewezen Hallo RBAC-rol Zie opnieuw kunnen alleen Hallo items dat ze zijn toegewezen toegang op beide in hello **alle Resources** tabblad of rechtstreeks in het dashboard.

Een belangrijk aspect voor RBAC zowel op resource groepsbereik of bereik van de resource is voor Hallo gebruikers toomake zeker toosign in toohello correcte directory.





![Directory-aanmelding in Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a>RBAC-rollen voor een Azure Active Directory-groep toewijzen
Alle Hallo-scenario's met RBAC op drie verschillende bereiken Hallo in Azure-aanbieding Hallo bevoegdheid beheren, implementeren en beheren van verschillende bronnen als een toegewezen gebruiker zonder Hallo moeten van het beheer van een persoonlijke abonnement. Ongeacht Hallo RBAC-rol is toegewezen voor een abonnement, resourcegroep of resource-scope, zijn onder Hallo één Azure-abonnement waarbij Hallo gebruikers toegang tot hebben alle Hallo resources verder gemaakt door Hallo toegewezen gebruikers kosten in rekening gebracht. Op deze manier hello gebruikers die beschikken over beheerdersrechten voor die volledige Azure-abonnement facturering heeft een volledig overzicht van Hallo verbruik, ongeacht wie Hallo resources wordt beheerd.

Voor grotere organisaties RBAC-rollen kunnen worden toegepast in Hallo dezelfde manier voor Azure Active Directory-groepen overweegt Hallo perspectief die Hallo beheerder gebruiker toogrant Hallo gedetailleerde toegang wil voor teams of volledige afdelingen, niet afzonderlijk voor elke gebruiker, dus kijken we naar deze als een zeer tijd- en efficiënte optie. tooillustrate in dit voorbeeld, Hallo **Inzender** rol is toegevoegd tooone van Hallo groepen in op abonnementsniveau Hallo Hallo-tenant.





![RBAC-rol voor AAD-groepen toevoegen](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

Deze groepen zijn beveiligingsgroepen die zijn ingericht en beheerd alleen binnen Azure Active Directory.

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a>Maak een aangepaste RBAC-rol tooopen ondersteuning aanvragen met behulp van PowerShell
Hallo ingebouwde RBAC-rollen die beschikbaar in Azure zijn ervoor zorgen dat bepaalde machtigingsniveaus op basis van beschikbare resources in de omgeving Hallo Hallo. Als geen van deze rollen Hallo beheerder gebruiker behoeften, is er echter Hallo optie toolimit toegang nog meer door aangepaste RBAC-rollen te maken.

Voor het maken van aangepaste RBAC-rollen moet een ingebouwde rol tootake, bewerken en vervolgens importeren in Hallo-omgeving. Hallo downloaden en het uploaden van Hallo rol worden beheerd met PowerShell of CLI.

Het is belangrijk toounderstand Hallo vereisten voor het maken van een aangepaste rol die u kunnen gedetailleerde toegang verlenen op abonnementsniveau Hallo en ook de mogelijkheid Hallo uitgenodigd gebruiker Hallo flexibiliteit ondersteuningsaanvragen te openen.

Voor dit voorbeeld Hallo ingebouwde rol **lezer** waarmee gebruikers toegang tooview Hallo-resource alle scopes maar niet tooedit ze of nieuwe maken is aangepast tooallow Hallo Hallo optie ondersteuningsaanvragen te openen.

eerste actie van het exporteren van Hallo Hallo **lezer** rol behoeften toobe voltooid in PowerShell met verhoogde machtigingen worden uitgevoerd als administrator.

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![Schermopname van PowerShell voor de rol Lezer RBAC](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

Vervolgens moet u tooextract Hallo JSON-sjabloon van Hallo-rol.





![JSON-sjabloon voor aangepaste lezer RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

Een typische RBAC-rol bestaat uit drie gedeelten **acties**, **NotActions** en **AssignableScopes**.

In Hallo **actie** sectie staan alle Hallo toegestane bewerkingen voor deze rol. Het is belangrijk toounderstand dat elke actie van een resourceprovider is toegewezen. In dit geval voor het maken van ondersteuning tickets Hallo **Microsoft.Support** resourceprovider moet worden weergegeven.

toobe kunnen toosee alle Hallo resourceproviders beschikbaar is en geregistreerd in uw abonnement, kunt u PowerShell.
```
Get-AzureRMResourceProvider

```
Bovendien kunt u controleren voor Hallo alle Hallo beschikbaar PowerShell-cmdlets toomanage hello resourceproviders.
    ![Schermopname van PowerShell voor provider bronbeheer](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)

alle acties voor een bepaalde RBAC-rol, resource providers worden vermeld in de sectie Hallo Hallo toorestrict **NotActions**.
Laatste, is het verplichte dat die Hallo RBAC-rol bevat Hallo expliciete abonnement-id's waar het wordt gebruikt. Hallo abonnement-id's vermeld onder Hallo **AssignableScopes**, anders u pas weer toegestaan tooimport Hallo rol in uw abonnement.

Na het maken en aanpassen van Hallo RBAC-rol, moet deze toobe geïmporteerde back Hallo-omgeving.

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

In dit voorbeeld is aangepaste naam voor deze rol RBAC Hallo 'Lezer ondersteuning tickets toegangsniveau' hello gebruiker tooview alles zodat in Hallo-abonnement en ook tooopen ondersteuningsaanvragen.

> [!NOTE]
> Hallo slechts twee ingebouwde RBAC-rollen zodat Hallo actie van het openen van ondersteuningsaanvragen zijn **eigenaar** en **Inzender**. Voor een gebruiker toobe kunnen tooopen ondersteuningsaanvragen, moet hij worden toegewezen een RBAC-rol alleen op Hallo abonnementsbereik, omdat alle ondersteuningsaanvragen zijn gemaakt op basis van een Azure-abonnement.

Deze nieuwe aangepaste rol is toegewezen tooan gebruiker Hallo dezelfde directory.





![schermopname van aangepaste RBAC-rol in Hallo geïmporteerd met Azure-portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![schermopname van het toewijzen van aangepaste geïmporteerde RBAC-rol toouser in Hallo dezelfde directory](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![schermopname van machtigingen voor aangepaste geïmporteerde RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

Hallo-voorbeeld is meer gedetailleerde tooemphasize Hallo limieten van deze aangepaste RBAC-rol als volgt:
* Nieuwe ondersteuningsaanvragen kunt maken
* Nieuwe scopes van de resource kan niet worden gemaakt (bijvoorbeeld: virtuele machine)
* Kan de nieuwe resourcegroepen niet maken.





![schermopname van aangepaste RBAC-rol ondersteuningsaanvragen maken](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![schermopname van aangepaste RBAC-rol kan niet toocreate virtuele machines](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![schermopname van aangepaste RBAC-rol kan niet toocreate nieuwe RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a>Maak een aangepaste RBAC-rol tooopen ondersteuning-aanvragen via de Azure CLI
Uitgevoerd op een Mac en zonder toegang tooPowerShell, is Azure CLI Hallo manier toogo.

Hallo stappen toocreate een aangepaste beveiligingsrol zijn Hallo dezelfde zijn, met de enige uitzondering Hallo dat met CLI Hallo-rol kan niet worden gedownload in een JSON-sjabloon, maar kan worden bekeken in Hallo CLI.

Voor dit voorbeeld ik hebt gekozen, is een ingebouwde rol Hallo van **back-up lezer**.

```

azure role show "backup reader" --json

```





![Schermafbeelding van de rol van back-lezer CLI weergeven](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

Hallo-rol in Visual Studio na het kopiëren van Hallo eigenschappen in een JSON-sjabloon bewerkt, Hallo **Microsoft.Support** resourceprovider is toegevoegd aan Hallo **acties** secties zodat deze gebruiker kunt openen ondersteuningsaanvragen terwijl u een lezer voor de back-upkluizen hello toobe. Opnieuw verdient het benodigde tooadd Hallo abonnements-ID waar deze rol wordt gebruikt in Hallo **AssignableScopes** sectie.

```

azure role create --inputfile <path>

```





![CLI-schermopname van het importeren van aangepaste RBAC-rol](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

de nieuwe rol Hallo is nu beschikbaar in hello Azure-portal en Hallo toewijzing proces is dezelfde als in de eerdere voorbeelden Hallo Hallo.





![Azure portal schermafbeelding van aangepaste RBAC-rol gemaakt met behulp van de CLI 1.0](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

Op Hallo is de meest recente Build 2017 hello Azure Cloud Shell algemeen beschikbaar. Azure Cloud-Shell is een aanvulling tooIDE en hello Azure-Portal. Met deze service krijgt u een browser gebaseerde shell die is geverifieerd en wordt gehost in Azure en u kunt deze gebruiken in plaats van de CLI op uw computer geïnstalleerd.





![Azure-Cloud-Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)

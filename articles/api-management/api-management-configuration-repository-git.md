---
title: aaaConfigure uw API Management-service met Git - Azure | Microsoft Docs
description: Meer informatie over hoe toosave en configureren van de configuratie van uw API Management-service met Git.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: mattfarm
ms.assetid: 364cd53e-88fb-4301-a093-f132fa1f88f5
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: ef7d4c18f2ea3f5c9b86403349a83aef240f979b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosave-and-configure-your-api-management-service-configuration-using-git"></a>Hoe toosave en configureren van de configuratie van uw API Management-service met Git
> 
> 

Elk exemplaar van API Management-service houdt een configuratiedatabase die informatie over het Hallo-configuratie en metagegevens voor Hallo service-exemplaar bevat. Wijzigingen kunnen toohello service-exemplaar worden gemaakt door een instelling in de publicatieportal hello te wijzigen, gebruikt een PowerShell-cmdlet of REST API-aanroep. Bovendien toothese methoden, kunt u ook beheren de serviceconfiguratie-exemplaar met behulp van Git, service management-scenario's zoals inschakelen:

* Configuratie versioning - downloaden en opslaan van verschillende versies van de serviceconfiguratie
* Bulksgewijs configuratiewijzigingen - toomultiple delen van de serviceconfiguratie wijzigingen aanbrengen in uw lokale opslagplaats en Hallo wijzigingen back toohello server integreren met een enkele bewerking
* Vertrouwde Git toolchain en workflow - Hallo Git tooling en werkstromen die u al bekend met bent gebruiken

Hallo volgende diagram geeft een overzicht van Hallo verschillende manieren tooconfigure uw API Management-service-exemplaar.

![GIT configureren][api-management-git-configure]

Wanneer u wijzigingen tooyour-service met behulp van de publicatieportal hello, PowerShell-cmdlets of Hallo REST-API aanbrengt, beheert u uw service-configuratiedatabase Hallo `https://{name}.management.azure-api.net` eindpunt, zoals wordt weergegeven aan de rechterkant Hallo van Hallo-diagram. Hallo links van Hallo diagram ziet u hoe u de configuratie van uw service met Git kunt beheren en Git-opslagplaats voor uw service zich bevindt op `https://{name}.scm.azure-api.net`.

Hallo stappen geven een overzicht van het beheer van uw API Management-service-exemplaar met Git.

1. Toegang tot de configuratie van Git in uw service
2. Opslaan van uw service configuration database tooyour Git-opslagplaats
3. Hallo Git-opslagplaats tooyour lokale machine worden gekloond
4. Ophalen van de meest recente opslagplaats Hallo omlaag tooyour lokale computer en doorvoeren en push wijzigingen back tooyour opslagplaats
5. Hallo wijzigingen uit de opslagplaats naar uw database van de configuration-service implementeren

Dit artikel wordt beschreven hoe tooenable en gebruik Git toomanage de serviceconfiguratie bevat naslaginformatie voor Hallo bestanden en mappen in Hallo Git-opslagplaats.

## <a name="access-git-configuration-in-your-service"></a>Toegang tot de configuratie van Git in uw service
U kunt snel Hallo status van de Git-configuratie door bekijkt hello Git-pictogram in de Hallo rechterbovenhoek van de publicatieportal Hallo weergeven. In dit voorbeeld status het Hallo-bericht geeft aan dat er niet-opgeslagen wijzigingen toohello opslagplaats. Dit komt doordat de configuratiedatabase van Hallo API Management-service is nog niet zijn opgeslagen toohello opslagplaats.

![GIT-status][api-management-git-icon-enable]

tooview en de Git-configuratie-instellingen configureren, u kunt Hallo Git pictogram klikt u op of klik op Hallo **beveiliging** menu en navigeer toohello **configuratie opslagplaats** tabblad.

![GIT inschakelen][api-management-enable-git]

> [!IMPORTANT]
> Geen geheimen die niet zijn gedefinieerd zoals eigenschappen worden opgeslagen in de opslagplaats hello en in de geschiedenis totdat u blijft uitschakelen en opnieuw inschakelen Git. Eigenschappen van een veilige plaats toomanage bieden constante string-waarden, inclusief geheimen, voor alle configuratie-API en beleidsregels, dus u geen toostore hebt ze rechtstreeks in uw beleidsverklaringen. Zie voor meer informatie [hoe toouse eigenschappen in Azure API Management-beleidsregels](api-management-howto-properties.md).
> 
> 

Zie voor meer informatie over het inschakelen of uitschakelen via Hallo REST-API toegang tot een Git [in- of uitschakelen via Hallo REST-API toegang tot een Git](https://msdn.microsoft.com/library/dn781420.aspx#EnableGit).

## <a name="toosave-hello-service-configuration-toohello-git-repository"></a>toosave hello service configuration toohello Git-opslagplaats
eerste stap van de Hallo voorafgaand aan het kopiëren van de opslagplaats Hallo is toosave Hallo huidige status van Hallo service configuration toohello opslagplaats. Klik op **opslaan configuratie toorepository**.

![Configuratie op te slaan][api-management-save-configuration]

Breng de gewenste wijzigingen op Hallo bevestigingsscherm en klik op **Ok** toosave.

![Configuratie op te slaan][api-management-save-configuration-confirm]

Na enkele ogenblikken Hallo-configuratie is opgeslagen en Hallo configuratiestatus van Hallo opslagplaats wordt weergegeven, inclusief Hallo datum en tijd van laatste configuratiewijziging Hallo en Hallo laatste synchronisatie tussen Hallo-serviceconfiguratie en Hallo opslagplaats.

![Configuratiestatus][api-management-configuration-status]

Zodra Hallo-configuratie is opgeslagen toohello opslagplaats, kunnen worden gekloond.

Zie voor informatie over het uitvoeren van deze bewerking met Hallo REST-API, [doorvoeren configuratie momentopname over met Hallo REST-API](https://msdn.microsoft.com/library/dn781420.aspx#CommitSnapshot).

## <a name="tooclone-hello-repository-tooyour-local-machine"></a>tooclone hello opslagplaats tooyour lokale computer
tooclone een opslagplaats, moet u Hallo URL tooyour opslagplaats, een gebruikersnaam en een wachtwoord. Hallo gebruikersnaam en -URL worden weergegeven aan de bovenkant Hallo Hallo **configuratie opslagplaats** tabblad.

![GIT kloon][api-management-configuration-git-clone]

Hallo-wachtwoord wordt gegenereerd aan de onderkant Hallo Hallo **configuratie opslagplaats** tabblad.

![Wachtwoord genereren][api-management-generate-password]

toogenerate een wachtwoord, eerst voor zorgen dat Hallo **verstrijken** toohello gewenst datum en tijd instellen en klik vervolgens op **Token genereren**.

![Wachtwoord][api-management-password]

> [!IMPORTANT]
> Noteer dit wachtwoord. Als u deze pagina Hallo-wachtwoord niet opnieuw weergegeven.
> 
> 

Hallo volgen voorbeelden gebruik Git Bash Hallo hulpprogramma van [Git voor Windows](http://www.git-scm.com/downloads) , maar u kunt een Git-hulpmiddel dat u bekend met bent.

Open uw Git-hulpprogramma in de gewenste map Hallo en Hallo opdracht tooclone Hallo git-opslagplaats tooyour lokale computer te volgen, geleverd door de publicatieportal Hallo Hallo-opdracht uitvoeren.

```
git clone https://bugbashdev4.scm.azure-api.net/
```

Geef Hallo-gebruikersnaam en wachtwoord wanneer u wordt gevraagd.

Als u eventuele fouten ontvangt, probeert u het wijzigen van uw `git clone` opdracht tooinclude Hallo-gebruikersnaam en wachtwoord, zoals wordt weergegeven in Hallo voorbeeld te volgen.

```
git clone https://username:password@bugbashdev4.scm.azure-api.net/
```

Als dit een fout biedt, probeert u URL-codering Hallo wachtwoord gedeelte van Hallo-opdracht. Een snelle manier toodo dit tooopen Visual Studio, en geef Hallo de volgende opdracht in Hallo **venster direct**. Hallo tooopen **venster direct**, opent u een oplossing of project in Visual Studio (of maak een nieuwe lege console-toepassing), en kies **Windows**, **Immediate** uit Hallo **Debug** menu.

```
?System.NetWebUtility.UrlEncode("password from publisher portal")
```

Hallo gecodeerd wachtwoord samen met uw naam en opslagplaats locatie tooconstruct Hallo git opdracht user gebruiken.

```
git clone https://username:url encoded password@bugbashdev4.scm.azure-api.net/
```

Zodra het Hallo-opslagplaats is gekloond kunt u deze kunt bekijken en bewerken in het lokale bestandssysteem. Zie voor meer informatie [structuur verwijzing van lokale Git-opslagplaats, bestanden en mappen](#file-and-folder-structure-reference-of-local-git-repository).

## <a name="tooupdate-your-local-repository-with-hello-most-current-service-instance-configuration"></a>tooupdate uw lokale opslagplaats met de meest recente configuratie van service-exemplaar Hallo
Als u wijzigingen tooyour API Management service-exemplaar in de publicatieportal Hallo of met behulp van Hallo REST-API maakt, moet u deze wijzigingen toohello opslagplaats opslaan voordat u uw lokale opslagplaats met de meest recente wijzigingen Hallo bijwerken kunt. toodo, klikt u op **opslaan configuratie toorepository** op Hallo **configuratie opslagplaats** tabblad in de publicatieportal hello en vervolgens uitgeeft Hallo volgende opdracht in uw lokale opslagplaats.

```
git pull
```

Voordat u `git pull` Zorg ervoor dat u in de map Hallo voor uw lokale opslagplaats. Als u hebt zojuist Hallo `git clone` opdracht, en vervolgens u Hallo directory tooyour opslagplaats wijzigen moet door het uitvoeren van een opdracht zoals Hallo volgende.

```
cd bugbashdev4.scm.azure-api.net/
```

## <a name="toopush-changes-from-your-local-repo-toohello-server-repo"></a>toopush wijzigingen uit uw lokale opslagplaats toohello server opslagplaats
toopush van uw opslagplaats lokale opslagplaats toohello server verandert, moet u uw wijzigingen en push ze toohello server-opslagplaats. toocommit uw wijzigingen open uw Git-opdrachthulpprogramma switch toohello directory van uw lokale opslagplaats en probleem Hallo opdrachten te volgen.

```
git add --all
git commit -m "Description of your changes"
```

alle Hallo toohello server is, voert doorvoeren toopush Hallo na de opdracht.

```
git push
```

## <a name="toodeploy-any-service-configuration-changes-toohello-api-management-service-instance"></a>toodeploy eventuele configuratie wijzigingen toohello API Management service-instantie
Wanneer uw lokale wijzigingen doorgevoerd en pushed toohello server-opslagplaats zijn, kunt u ze tooyour API Management service-exemplaar implementeert.

![Implementeren][api-management-configuration-deploy]

Zie voor informatie over het uitvoeren van deze bewerking met Hallo REST-API, [Git implementeren wijzigingen tooconfiguration-database met de Hallo REST-API](https://docs.microsoft.com/en-us/rest/api/apimanagement/tenantconfiguration).

## <a name="file-and-folder-structure-reference-of-local-git-repository"></a>Verwijzing in de bestanden en mappen de structuur van de lokale Git-opslagplaats
Hallo bevatten bestanden en mappen in de lokale git-opslagplaats Hallo Hallo configuratie-informatie over Hallo service-exemplaar.

| Item | Beschrijving |
| --- | --- |
| Hoofdmap voor de api-management |Op het hoogste niveau van de configuratie voor service-exemplaar Hallo bevat |
| map van de API 's |Hallo-configuratie voor Hallo API's bevat in Hallo service-exemplaar |
| map groepen |Hallo-configuratie voor Hallo groepen bevat in Hallo service-exemplaar |
| map beleid |Bevat Hallo-beleidsregels in Hallo service-exemplaar |
| portalStyles map |Hallo-configuratie voor Hallo developer portal aanpassingen bevat in Hallo service-exemplaar |
| map Products |Hallo-configuratie voor Hallo producten bevat in Hallo service-exemplaar |
| sjablonenmap |Bevat de Hallo-configuratie voor e-mailsjablonen Hallo in Hallo service-exemplaar |

Elke map kan een of meer bestanden bevatten en in sommige gevallen een of meer mappen, bijvoorbeeld een map voor elke API, product of groep. Hallo-bestanden in elke map zijn specifiek voor Hallo entiteitstype beschreven door Hallo mapnaam.

| Bestandstype | Doel |
| --- | --- |
| JSON |Configuratie-informatie over Hallo respectieve entiteit |
| HTML |Beschrijvingen over Hallo entiteit, vaak worden weergegeven in het Hallo-portal voor ontwikkelaars |
| xml |Beleidsinstructies |
| CSS |Opmaakmodellen voor developer portal aanpassen |

Deze bestanden kunnen worden gemaakt, verwijderd, bewerkt en beheerd op het lokale bestandssysteem en Hallo wijzigingen geïmplementeerd back toohello uw API Management-service-exemplaar.

> [!NOTE]
> Hallo volgende entiteiten zijn niet opgenomen in de Git-opslagplaats Hallo en kunnen niet worden geconfigureerd met Git.
> 
> * Gebruikers
> * Abonnementen
> * Eigenschappen
> * Developer portal entiteiten dan stijlen
> 
> 

### <a name="root-api-management-folder"></a>Hoofdmap voor de api-management
Hallo-hoofdmap `api-management` map bevat een `configuration.json` -bestand dat op het hoogste niveau van de informatie over service-exemplaar in de volgende indeling Hallo Hallo bevat.

```json
{
  "settings": {
    "RegistrationEnabled": "True",
    "UserRegistrationTerms": null,
    "UserRegistrationTermsEnabled": "False",
    "UserRegistrationTermsConsentRequired": "False",
    "DelegationEnabled": "False",
    "DelegationUrl": "",
    "DelegatedSubscriptionEnabled": "False",
    "DelegationValidationKey": ""
  },
  "$ref-policy": "api-management/policies/global.xml"
}
```

instellingen van de eerste vier Hallo (`RegistrationEnabled`, `UserRegistrationTerms`, `UserRegistrationTermsEnabled`, en `UserRegistrationTermsConsentRequired`) toewijzen toohello volgende instellingen op Hallo **identiteiten** tabblad in Hallo **beveiliging** sectie.

| Identiteit | Te worden toegewezen|
| --- | --- |
| RegistrationEnabled |**Omleidingspagina anonieme gebruikers toosign in** selectievakje |
| UserRegistrationTerms |**Gebruiksvoorwaarden op aanmelding gebruiker** tekstvak |
| UserRegistrationTermsEnabled |**Gebruiksvoorwaarden weergeven op de aanmeldingspagina** selectievakje |
| UserRegistrationTermsConsentRequired |**Toestemming vereist** selectievakje |

![Instellingen van identiteit][api-management-identity-settings]

instellingen van de volgende vier Hallo (`DelegationEnabled`, `DelegationUrl`, `DelegatedSubscriptionEnabled`, en `DelegationValidationKey`) toewijzen toohello volgende instellingen op Hallo **delegering** tabblad in Hallo **beveiliging** sectie.

| Delegatie-instelling | Te worden toegewezen|
| --- | --- |
| DelegationEnabled |**Gemachtigde aanmelden & registratie** selectievakje |
| DelegationUrl |**De eindpunt-URL voor overdracht** tekstvak |
| DelegatedSubscriptionEnabled |**Product abonnement delegeren** selectievakje |
| DelegationValidationKey |**Validatiesleutel delegeren** tekstvak |

![Delegatie-instellingen][api-management-delegation-settings]

laatste instelling Hallo `$ref-policy`, toohello algemene instructies beleidsbestand voor Hallo service-exemplaar wordt toegewezen.

### <a name="apis-folder"></a>map van de API 's
Hallo `apis` een map bevat voor elke API in Hallo service-exemplaar waarin de volgende items Hallo.

* `apis\<api name>\configuration.json`-Dit is Hallo-configuratie voor Hallo API en bevat informatie over Hallo back-end voor service-URL en Hallo-bewerkingen. Dit Hallo is dezelfde informatie die wordt geretourneerd als u toocall [ophalen van een specifieke API](https://msdn.microsoft.com/library/azure/dn781423.aspx#GetAPI) met `export=true` in `application/json` indeling.
* `apis\<api name>\api.description.html`-Dit Hallo beschrijving van Hallo API is en overeenkomt met toohello `description` eigenschap Hallo [API entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#EntityProperties).
* `apis\<api name>\operations\`-Deze map bevat `<operation name>.description.html` bestanden die zijn toegewezen toohello bewerkingen in Hallo API. Elk bestand bevat Hallo beschrijving van één bewerking in Hallo API waarmee toohello toegewezen `description` eigenschap Hallo [bewerking entiteit](https://msdn.microsoft.com/library/azure/dn781423.aspx#OperationProperties) in Hallo REST-API.

### <a name="groups-folder"></a>map groepen
Hallo `groups` een map voor elke groep die is gedefinieerd in Hallo service-exemplaar bevat.

* `groups\<group name>\configuration.json`-Dit is de configuratie Hallo voor Hallo-groep. Dit Hallo is dezelfde informatie die wordt geretourneerd als u toocall hello [ophalen van een specifieke groep](https://msdn.microsoft.com/library/azure/dn776329.aspx#GetGroup) bewerking.
* `groups\<group name>\description.html`-Dit Hallo beschrijving van Hallo-groep is en overeenkomt met toohello `description` eigenschap Hallo [groep entiteit](https://msdn.microsoft.com/library/azure/dn776329.aspx#EntityProperties).

### <a name="policies-folder"></a>map beleid
Hallo `policies` map Hallo beleidsverklaringen voor uw service-exemplaar bevat.

* `policies\global.xml`-beleid is gedefinieerd op globaal bereik voor uw service-exemplaar bevat.
* `policies\apis\<api name>\`-Als er beleid is gedefinieerd op API-scope, zijn opgenomen in deze map.
* `policies\apis\<api name>\<operation name>\`map - als er beleid is gedefinieerd op bewerkingsbereik, zijn opgenomen in deze map in `<operation name>.xml` bestanden die zijn toegewezen toohello beleidsverklaringen voor elke bewerking.
* `policies\products\`-Als er beleid is gedefinieerd op de product-scope, zijn opgenomen in deze map bevat `<product name>.xml` bestanden die zijn toegewezen toohello beleidsverklaringen voor elk product.

### <a name="portalstyles-folder"></a>portalStyles map
Hallo `portalStyles` map bevat configuratie- en opmaakmodellen developer portal aanpassingen voor Hallo service-exemplaar.

* `portalStyles\configuration.json`-Hallo namen bevat van StyleSheets Hallo gebruikt door het Hallo-portal voor ontwikkelaars
* `portalStyles\<style name>.css`-elke `<style name>.css` bestand bevat stijlen voor Hallo developer-portal (`Preview.css` en `Production.css` standaard).

### <a name="products-folder"></a>map Products
Hallo `products` een map voor elk product dat is gedefinieerd in Hallo service-exemplaar bevat.

* `products\<product name>\configuration.json`-Dit is Hallo-configuratie voor het Hallo-product. Dit Hallo is dezelfde informatie die wordt geretourneerd als u toocall hello [ophalen van een specifiek product](https://msdn.microsoft.com/library/azure/dn776336.aspx#GetProduct) bewerking.
* `products\<product name>\product.description.html`-Dit Hallo beschrijving van Hallo product is en overeenkomt met toohello `description` eigenschap Hallo [product entiteit](https://msdn.microsoft.com/library/azure/dn776336.aspx#Product) in Hallo REST-API.

### <a name="templates"></a>sjablonen
Hallo `templates` map bevat de configuratie voor Hallo [e-mailsjablonen](api-management-howto-configure-notifications.md) van Hallo service-exemplaar.

* `<template name>\configuration.json`-Dit is de configuratie Hallo voor Hallo e-mailsjabloon.
* `<template name>\body.html`-Dit is de hoofdtekst Hallo van Hallo e-mailsjabloon.

## <a name="next-steps"></a>Volgende stappen
Voor informatie over andere manieren toomanage uw service-exemplaar, Zie:

* Uw service-exemplaar met behulp van PowerShell-cmdlets volgen Hallo beheren
  * [Naslaginformatie over PowerShell-cmdlets voor service-implementatie](https://msdn.microsoft.com/library/azure/mt619282.aspx)
  * [Service management PowerShell-cmdlet-verwijzing](https://msdn.microsoft.com/library/azure/mt613507.aspx)
* Uw service-exemplaar in de publicatieportal Hallo beheren
  * [Uw eerste API beheren](api-management-get-started.md)
* Beheren van uw service-exemplaar met behulp van Hallo REST-API
  * [Naslaginformatie over API Management REST API](https://msdn.microsoft.com/library/azure/dn776326.aspx)

## <a name="watch-a-video-overview"></a>Bekijk een video-overzicht
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Configuration-over-Git/player]
> 
> 

[api-management-enable-git]: ./media/api-management-configuration-repository-git/api-management-enable-git.png
[api-management-git-enabled]: ./media/api-management-configuration-repository-git/api-management-git-enabled.png
[api-management-save-configuration]: ./media/api-management-configuration-repository-git/api-management-save-configuration.png
[api-management-save-configuration-confirm]: ./media/api-management-configuration-repository-git/api-management-save-configuration-confirm.png
[api-management-configuration-status]: ./media/api-management-configuration-repository-git/api-management-configuration-status.png
[api-management-configuration-git-clone]: ./media/api-management-configuration-repository-git/api-management-configuration-git-clone.png
[api-management-generate-password]: ./media/api-management-configuration-repository-git/api-management-generate-password.png
[api-management-password]: ./media/api-management-configuration-repository-git/api-management-password.png
[api-management-git-configure]: ./media/api-management-configuration-repository-git/api-management-git-configure.png
[api-management-configuration-deploy]: ./media/api-management-configuration-repository-git/api-management-configuration-deploy.png
[api-management-identity-settings]: ./media/api-management-configuration-repository-git/api-management-identity-settings.png
[api-management-delegation-settings]: ./media/api-management-configuration-repository-git/api-management-delegation-settings.png
[api-management-git-icon-enable]: ./media/api-management-configuration-repository-git/api-management-git-icon-enable.png





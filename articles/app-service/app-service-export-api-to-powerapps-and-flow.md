---
title: aaaExporting een tooPowerApps Azure gehoste API en Microsoft-Flow | Microsoft Docs
description: Overzicht van hoe tooexpose een API in App Service-tooPowerApps en Microsoft-Flow gehost
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/20/2017
ms.author: mahender
ms.openlocfilehash: 285b6efa3af5b0feac1ee2f617c0dc56dc3fd198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-an-azure-hosted-api-toopowerapps-and-microsoft-flow"></a>Exporteren van een Azure gehoste API tooPowerApps en Microsoft-Flow

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Maken van aangepaste connectors voor PowerApps en Microsoft-Flow

[PowerApps](https://powerapps.com) is een service voor het bouwen en met behulp van aangepaste zakelijke apps die verbinding maken met tooyour gegevens en alle platforms. [Microsoft-Flow](https://flow.microsoft.com) maakt het eenvoudig tooautomate werkstromen en bedrijfsprocessen tussen uw favoriete apps en services. Zowel PowerApps als Microsoft Flow worden geleverd met een groot aantal ingebouwde verbindingslijnen toodata bronnen zoals Office 365, Dynamics 365 en Salesforce. Gebruikers moeten echter ook toobe kunnen tooleverage gegevensbronnen en API's die zijn gebouwd door hun organisatie.

Op deze manier ontwikkelaars gewenste tooexpose hun API's meer grotendeels binnen Hallo organisatie wil toomake hun beschikbaar tooPowerApps API's en Microsoft-Flow-gebruikers. In dit onderwerp leert u hoe een API tooexpose gebouwd met Azure App Service- of Azure Functions tooPowerApps en Microsoft-Flow. [Azure App Service](https://azure.microsoft.com/services/app-service/) is een platform as a service-oplossing waarmee ontwikkelaars tooquickly en eenvoudig build bedrijfsniveau web-, mobiele en API-toepassingen. [Azure Functions](https://azure.microsoft.com/services/functions/) is een op basis van gebeurtenissen zonder server compute-oplossing waarmee u tooquickly auteur code die tooother onderdelen van uw systeem en schalen op basis van vraag reageren kan.

toolearn meer informatie over deze services, Zie:
- [PowerApps begeleide Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Microsoft-stroom begeleide Learning](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Wat is App Service?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Wat is Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Delen van een API-definitie

API's worden vaak beschreven met behulp van een [OpenAPI document](https://www.openapis.org/) (ook tooas een document 'Swagger' genoemd). Dit document bevat alle informatie over welke bewerkingen beschikbaar zijn en hoe Hallo gegevens moeten worden gestructureerd Hallo. PowerApps en Microsoft-Flow kunnen aangepaste connectors voor elk OpenAPI 2.0-document maken. Zodra een aangepaste connector is gemaakt, kan worden gebruikt in exact Hallo dezelfde manier als een van de ingebouwde verbindingslijnen Hallo en snel kunnen worden geïntegreerd in een toepassing.

Azure App Service en Azure Functions hebben [ingebouwde ondersteuning](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) voor maken en beheren van een document OpenAPI die als host fungeert. Volgorde toocreate een aangepaste connector voor een web, mobiel, API of functie-app moet PowerApps en stroom toobe krijgt een kopie van het Hallo-definitie.

> [!NOTE]
> Omdat een kopie van de API-definitie Hallo wordt gebruikt, informatie PowerApps en Microsoft-Flow geen onmiddellijk over updates of recente wijzigingen toohello toepassing. Als u een nieuwe versie van Hallo API beschikbaar wordt gesteld, moeten deze stappen voor de nieuwe versie Hallo worden herhaald. 

Ga als volgt tooprovide PowerApps en Microsoft-Flow met Hallo gehoste API-definitie voor uw app:

1. Open Hallo [Azure Portal](https://portal.azure.com) en navigeer tooyour App Service- of Azure Functions-toepassing.

    Als u Azure App Service gebruikt, selecteert u **API-definitie** uit de lijst Hallo-instellingen. 
    
    Als u Azure Functions, selecteert u de functie-app en kies vervolgens **platformfuncties**, en vervolgens **API-definitie**. U kunt ook tooopen Hallo **API-definitie (preview)** tabblad, in plaats daarvan.

2. Als een API-definitie is opgegeven, ziet u een **exporteren tooPowerApps + Microsoft Flow** knop. Klik op deze knop toobegin Hallo-exportproces.

3. Selecteer Hallo **exportmodus**. Hiermee bepaalt u Hallo-stappen die u moet toofollow toocreate een connector. App Service biedt twee opties voor het leveren van PowerApps en Microsoft-Flow met uw API-definitie:

    **Express** kunt u aangepaste connector Hallo van binnen hello Azure-portal. Het vereist dat Hallo huidige aangemelde gebruiker heeft toestemming toocreate connectors in de doelomgeving Hallo. Dit is Hallo aanbevolen benadering als aan deze eis kan worden voldaan. Als u deze modus gebruikt, voert u de Hallo [export Express](#express) onderstaande instructies.

    **Handmatige** kunt u een kopie van Hallo API afgebakend die kan worden geïmporteerd met Hallo PowerApps of Microsoft Flow portals exporteren. Dit is Hallo aanbevolen benadering als hello Azure en gebruiker Hallo-gebruiker met machtigingen toocreate connectors verschillende personen zijn of als het Hallo-connector moet toobe gemaakt in een andere tenant. Als u deze modus gebruikt, voert u de Hallo [handmatig exporteren en importeren](#manual) onderstaande instructies.

<a name="express"></a>
## <a name="express-export"></a>Snelle exporteren

In deze sectie maakt u een nieuwe aangepaste connector uit binnen hello Azure-portal. U moet zijn aangemeld in Hallo tenant toowhich gewenste tooexport en u moet machtigingen toocreate een aangepaste connector hebben in de doelomgeving Hallo.

1. Hallo-omgeving waarin u toocreate Hallo connector wilt selecteren. Geef een naam op voor uw aangepaste connector.

2. Als uw API-definitie definities beveiliging bevat, wordt deze in stap &#2; genoemd. Indien nodig, Hallo beveiliging bieden configuratiedetails nodig toogrant gebruikers toegang tot tooyour API. Zie voor meer informatie [verificatie](#auth) hieronder. 

3. Klik op **OK** toocreate uw aangepaste connector.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Handmatige exporteren en importeren

In de volgorde toocreate een aangepaste connector voor een web, mobiel, API of functie-app, twee stappen nodig:

1. [Hallo-API-definitie bij het ophalen van App Service- of Azure Functions](#export)
2. [Hallo-API-definitie te importeren in PowerApps en Microsoft-Flow](#import)

Het is mogelijk dat deze twee stappen toobe uitgevoerd door afzonderlijke personen binnen een organisatie, moet als een opgegeven gebruiker geen machtiging tooperform beide acties. In dit geval moet een ontwikkelaar die Inzender toegang toohello App Service- of Azure Functions-toepassing met tooobtain Hallo API-definitie (een enkele JSON-bestand) of een koppeling tooit. Ze moeten tooprovide vervolgens die definitie tooa PowerApps of Microsoft-Flow-eigenaar. Die eigenaar kunt Hallo metagegevens toocreate Hallo aangepaste connector gebruiken.

<a name="export"></a>
### <a name="retrieving-hello-api-definition-from-app-service-or-azure-functions"></a>Hallo-API-definitie bij het ophalen van App Service- of Azure Functions

In deze sectie exporteert u Hallo API-definitie voor uw App Service API toobe later in Hallo PowerApps of Microsoft Flow portal gebruikt.

1. U kunt tooeither **Hallo API-definitie downloaden** of **een koppeling**. Afhankelijk van wat u kiest, Hallo resultaat in de volgende sectie Hallo worden verstrekt. Selecteer een van deze opties en volg Hallo-instructies.
 
2. Als uw API-definitie definities beveiliging bevat, wordt deze in stap &#2; genoemd. Tijdens het importeren, PowerApps en Microsoft Flow detecteert deze en voor informatie over beveiliging, wordt gevraagd. Hallo referenties gerelateerde tooeach definitie voor gebruik in de volgende sectie Hallo verzamelen. Zie voor meer informatie [verificatie](#auth) hieronder. 

<a name="import"></a>
### <a name="importing-hello-api-definition-into-powerapps-and-microsoft-flow"></a>Hallo-API-definitie te importeren in PowerApps en Microsoft-Flow

In deze sectie maakt u een aangepaste connector in PowerApps en Microsoft-Flow met Hallo API-definitie eerder hebt verkregen. Aangepaste connectors worden gedeeld tussen Hallo twee services, dus u slechts eenmaal tooimport Hallo-definitie hoeft. Zie voor meer informatie over aangepaste connectors [registreren en gebruiken van aangepaste connectors in PowerApps] en [registreren en gebruiken van aangepaste connectors in Microsoft Flow].

1. Open Hallo [Powerapps webportal](https://web.powerapps.com) of Hallo [Microsoft Flow webportal](https://flow.microsoft.com/), en meld u aan. 

2. Klik op Hallo **instellingen** knop (pictogram Hallo tandwielpictogram) in de rechterbovenhoek Hallo van Hallo pagina en selecteer **aangepaste connectors**. 

3. Klik op **maken van aangepaste connector**.

4. Op Hallo **algemene** tabblad, Geef een naam voor uw API en vervolgens uploaden Hallo OpenAPI definitie of plak in Hallo metagegevens-URL. Klik op **gaan**.

4. Op Hallo **beveiliging** tabblad als u details over vraag tooprovide certificaatverificatie, Voer Hallo-waarden in de vorige sectie Hallo verkregen. Als dat niet het geval is, gaan toohello volgende stap.

5. Op Hallo **definities** tabblad alle Hallo bewerkingen die zijn gedefinieerd in uw bestand OpenAPI worden automatisch ingevuld. Als alle vereiste bewerkingen zijn gedefinieerd, kunt u de volgende stap toohello gaan. Zo niet, u kunt toevoegen en bewerkingen hier wijzigen.

6. Klik op **-connector maken**. Als u wilt dat tootest API-aanroepen, gaat u toohello volgende stap.

7. Op Hallo **Test** tabblad, geen verbinding maken, selecteert u een tootest bewerking en alle gegevens die nodig is voor de bewerking Hallo invoeren.

8. Klik op **testen bewerking**.


<a name="auth"></a>
## <a name="authentication"></a>Authentication

PowerApps en Microsoft-Flow ondersteuning systeemeigen voor een verzameling van id-providers die gebruikt toolog in gebruikers van uw aangepaste connector worden kunnen. Als uw API is verificatie vereist, zorg ervoor dat deze wordt vastgelegd als een _beveiliging definitie_ in uw document OpenAPI. Tijdens het exporteren moet u tooprovide configuratiewaarden die een Microsoft-Flow tooperform aanmelding acties voor PowerApps toestaan.

Deze sectie bevat informatie over Hallo verificatietypen die worden ondersteund door snelle Hallo-stroom: API-sleutel, Azure Active Directory en algemene OAuth 2.0. Zie voor een volledige lijst met providers en Hallo-referenties voor elk is vereist, [registreren en gebruiken van aangepaste connectors in PowerApps] en [registreren en gebruiken van aangepaste connectors in Microsoft Flow].

### <a name="api-key"></a>API-sleutel
Wanneer dit beveiligingsschema wordt gebruikt, worden Hallo gebruikers van de connector vraag tooprovide Hallo sleutel wanneer ze een verbinding maakt. U kunt opgeven dat een API sleutelnaam toohelp die ze weten welke sleutel nodig. Voor Azure Functions wordt dit doorgaans een Hallo-hostsleutels die betrekking hebben op de verschillende functies binnen Hallo functie-app.

### <a name="azure-active-directory"></a>Azure Active Directory
Bij het configureren van een aangepaste connector die AAD aanmelding vereist twee AAD-toepassing registraties zijn vereist: één toomodel Hallo back-end-API en één toomodel Hallo-connector in PowerApps en stroom.

Uw API moet geconfigureerde toowork met Hallo eerste registratie en dit wordt al worden afgehandeld als u Hallo gebruikt [App Service-verificatie/autorisatie](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) functie.

Hebt u toomanually Hallo tweede registratie voor Hallo-connector maken met behulp van Hallo stappen behandeld in [een AAD-toepassing toe te voegen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). Hallo registratie moet toohave gedelegeerde toegang tooyour API en antwoord-URL van de `https://msmanaged-na.consent.azure-apim.net/redirect`. Zie [in dit voorbeeld](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) vervangen door uw API voor hello Azure Resource Manager voor meer informatie.

Hallo volgende configuratiewaarden die zijn vereist:
- **Client-ID** -Hallo van client-ID van de registratie van de AAD-connector
- **Clientgeheim** -clientgeheim Hallo van de registratie van de AAD-connector
- **Aanmeldings-URL** - hello basis-URL voor AAD. In de openbare Azure, dit wordt doorgaans `https://login.windows.net`.
- **Tenant-ID** -ID van Hallo tenant toobe gebruikt voor aanmelding Hallo Hallo. Dit moet 'algemene' of Hallo-ID van het Hallo-tenant in welke Hallo connector wordt gemaakt.
- **Bron-URL** -Hallo bron-URL van uw API-back-end AAD-registratie

> [!IMPORTANT]
> Als een andere persoon Hallo API-definitie in PowerApps en Microsoft-Flow als onderdeel van de handmatige stroom hello importeren wilt, moet u tooprovide ze met het client-ID en client geheim Hallo **van registratie van de connector Hallo**, evenals Als de bron-URL Hallo van uw API. Zorg ervoor dat deze geheime gegevens veilig worden beheerd. **De beveiligingsreferenties Hallo Hallo API zelf niet delen.**

### <a name="generic-oauth-20"></a>Algemene OAuth 2.0
Hallo algemene OAuth 2.0-ondersteuning kunt u toointegrate met elke OAuth 2.0-provider. Hiermee kunt u toobring in een aangepaste provider die niet systeemeigen worden ondersteund.

Hallo volgende configuratiewaarden die zijn vereist:
- **Client-ID** -Hallo OAuth 2.0-client-ID
- **Clientgeheim** -geheim Hallo OAuth 2.0-client
- **Autorisatie-URL** -Hallo OAuth 2.0-autorisatie-URL
- **URL token** -Hallo token OAuth 2.0-URL
- **Vernieuwen van de URL** -URL voor OAuth 2.0-vernieuwen Hallo



[registreren en gebruiken van aangepaste connectors in PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[registreren en gebruiken van aangepaste connectors in Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/

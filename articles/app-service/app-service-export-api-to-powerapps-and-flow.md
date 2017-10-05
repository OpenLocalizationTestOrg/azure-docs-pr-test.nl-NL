---
title: Een Azure gehoste API exporteren naar PowerApps en Microsoft-stroom | Microsoft Docs
description: Overzicht van het blootstellen van een gehoste API in App Service PowerApps en Microsoft-Flow
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
ms.openlocfilehash: 0d166a2e5b60c3b9f911f9fc3ad49ad7f252abb4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="exporting-an-azure-hosted-api-to-powerapps-and-microsoft-flow"></a>Een Azure gehoste API exporteren naar PowerApps en Microsoft-stroom

## <a name="creating-custom-connectors-for-powerapps-and-microsoft-flow"></a>Maken van aangepaste connectors voor PowerApps en Microsoft-Flow

[PowerApps](https://powerapps.com) is een service voor het bouwen en met behulp van aangepaste zakelijke apps die verbinding maken met uw gegevens en alle platforms. [Microsoft-Flow](https://flow.microsoft.com) kunt u gemakkelijk om werkstromen en bedrijfsprocessen tussen uw favoriete apps en services te automatiseren. Zowel PowerApps als Microsoft Flow worden geleverd met diverse ingebouwde connectors met gegevensbronnen, zoals Office 365, Dynamics 365 en Salesforce. Gebruikers moeten echter ook kunnen gebruikmaken van gegevensbronnen en API's die zijn gebouwd door hun organisatie.

Ontwikkelaars die u beschikbaar wilt maken van hun API's grotere schaal binnen de organisatie wilt op dezelfde manier hun API's beschikbaar stellen aan PowerApps en Microsoft-Flow-gebruikers. In dit onderwerp wordt beschreven hoe u een API die is gebouwd met Azure App Service- of Azure Functions PowerApps en Microsoft-Flow blootstellen. [Azure App Service](https://azure.microsoft.com/services/app-service/) is een platform as a service-oplossing waarmee ontwikkelaars snel en eenvoudig ontwikkelen bedrijfsniveau web, mobiel en API-toepassingen. [Azure Functions](https://azure.microsoft.com/services/functions/) is een op basis van gebeurtenissen zonder server compute-oplossing waarmee u snel auteur-code die op andere onderdelen van uw systeem en schalen op basis van vraag reageren kan.

Zie voor meer informatie over deze services:
- [PowerApps begeleide Learning](https://powerapps.microsoft.com/guided-learning/learning-introducing-powerapps/) 
- [Microsoft-stroom begeleide Learning](https://flow.microsoft.com/guided-learning/learning-introducing-flow/)
- [Wat is App Service?](https://docs.microsoft.com/azure/app-service/app-service-value-prop-what-is)
- [Wat is Azure Functions](https://docs.microsoft.com/azure/azure-functions/functions-overview)

## <a name="sharing-an-api-definition"></a>Delen van een API-definitie

API's worden vaak beschreven met behulp van een [OpenAPI document](https://www.openapis.org/) (ook wel aangeduid als een document 'Swagger'). Dit document bevat alle informatie over welke bewerkingen beschikbaar zijn en hoe de gegevens moeten worden gestructureerd. PowerApps en Microsoft-Flow kunnen aangepaste connectors voor elk OpenAPI 2.0-document maken. Zodra een aangepaste connector is gemaakt, kunnen worden gebruikt op dezelfde manier als een van de ingebouwde connectors en snel kunnen worden geïntegreerd in een toepassing.

Azure App Service en Azure Functions hebben [ingebouwde ondersteuning](https://docs.microsoft.com/azure/app-service-api/app-service-api-metadata) voor maken en beheren van een document OpenAPI die als host fungeert. Een aangepaste connector voor een web, mobiel, API of functie-app maakt, moet PowerApps en stroom om een kopie van de definitie worden gegeven.

> [!NOTE]
> Omdat een kopie van de API-definitie wordt gebruikt, informatie PowerApps en Microsoft-Flow geen onmiddellijk over updates of grote wijzigingen aan de toepassing. Als u een nieuwe versie van de API beschikbaar wordt gesteld, moeten deze stappen voor de nieuwe versie worden herhaald. 

Om PowerApps en Microsoft-Flow met de gehoste API-definitie voor uw app, de volgende stappen uit:

1. Open de [Azure Portal](https://portal.azure.com) en navigeer naar uw App Service- of Azure Functions-toepassing.

    Als u Azure App Service gebruikt, selecteert u **API-definitie** uit de lijst met instellingen. 
    
    Als u Azure Functions, selecteert u de functie-app en kies vervolgens **platformfuncties**, en vervolgens **API-definitie**. U kunt er ook voor kiezen om te openen de **API-definitie (preview)** tabblad, in plaats daarvan.

2. Als een API-definitie is opgegeven, ziet u een **exporteren naar PowerApps + Microsoft Flow** knop. Klik op deze knop om te beginnen met de export.

3. Selecteer de **exportmodus**. Hiermee bepaalt u de stappen die u moet volgen om u te maken van een connector. App Service biedt twee opties voor het leveren van PowerApps en Microsoft-Flow met uw API-definitie:

    **Express** kunt u de aangepaste connector uit binnen de Azure portal maken. Vereist dat de huidige aangemelde gebruiker toegangsrechten heeft voor connectors maken in de doelomgeving. Dit is de aanbevolen aanpak als aan deze eis kan worden voldaan. Als u deze modus gebruikt, volgt u de [export Express](#express) onderstaande instructies.

    **Handmatige** kunt u een kopie van de API-definitie die kan worden geïmporteerd met behulp van de portals PowerApps of Microsoft Flow exporteren. Dit is de aanbevolen aanpak als de Azure-gebruiker en de gebruiker met machtigingen voor het maken van connectors verschillende personen of als de connector moet worden gemaakt in een andere tenant. Als u deze modus gebruikt, volgt u de [handmatig exporteren en importeren](#manual) onderstaande instructies.

<a name="express"></a>
## <a name="express-export"></a>Snelle exporteren

In deze sectie maakt u een nieuwe aangepaste connector uit binnen de Azure-portal. U moet worden aangemeld bij de tenant waarnaar u wilt exporteren en u gemachtigd bent om een aangepaste connector maken in de doelomgeving.

1. Selecteer de omgeving waarin u wilt maken van de connector. Geef een naam op voor uw aangepaste connector.

2. Als uw API-definitie definities beveiliging bevat, wordt deze in stap &#2; genoemd. Als vereist, geeft u de configuratiegegevens van de beveiliging die nodig zijn voor gebruikers toegang verlenen tot uw API. Zie voor meer informatie [verificatie](#auth) hieronder. 

3. Klik op **OK** om uw aangepaste connector te maken.


<a name="manual"></a>
## <a name="manual-export-and-import"></a>Handmatige exporteren en importeren

Om een aangepaste connector voor een web, mobiel, API of functie-app maakt, worden twee stappen vereist:

1. [Bij het ophalen van de API-definitie van App Service- of Azure Functions](#export)
2. [Importeren van de API-definitie in PowerApps en Microsoft-Flow](#import)

Het is mogelijk dat deze twee stappen worden uitgevoerd door afzonderlijke personen binnen een organisatie, moeten zoals een opgegeven gebruiker geen machtiging voor beide acties uitvoeren. In dit geval moet een ontwikkelaar die Inzender toegang tot de App Service- of Azure Functions-toepassing heeft de API-definitie (een enkele JSON-bestand) of een koppeling naar deze verkrijgen. Vervolgens moet ze die definitie voor de eigenaar van een PowerApps of Microsoft Flow opgeven. Die eigenaar kunt de metagegevens voor het maken van de aangepaste connector gebruiken.

<a name="export"></a>
### <a name="retrieving-the-api-definition-from-app-service-or-azure-functions"></a>Bij het ophalen van de API-definitie van App Service- of Azure Functions

In deze sectie exporteert u de API-definitie voor uw App Service API later in de portal PowerApps of Microsoft Flow moet worden gebruikt.

1. U kunt een **downloaden van de API-definitie** of **een koppeling**. Afhankelijk van wat u kiest, het resultaat in de volgende sectie worden verstrekt. Selecteer een van deze opties en volg de instructies.
 
2. Als uw API-definitie definities beveiliging bevat, wordt deze in stap &#2; genoemd. Tijdens het importeren, PowerApps en Microsoft Flow detecteert deze en voor informatie over beveiliging, wordt gevraagd. Verzamel de referenties die zijn gerelateerd aan elke definitie voor gebruik in de volgende sectie. Zie voor meer informatie [verificatie](#auth) hieronder. 

<a name="import"></a>
### <a name="importing-the-api-definition-into-powerapps-and-microsoft-flow"></a>Importeren van de API-definitie in PowerApps en Microsoft-Flow

In deze sectie maakt u een aangepaste connector in PowerApps en Microsoft-Flow met behulp van de API-definitie eerder hebt verkregen. Aangepaste connectors worden gedeeld tussen de twee services, dus u moet slechts één keer in de definitie voor het importeren. Zie voor meer informatie over aangepaste connectors [registreren en gebruiken van aangepaste connectors in PowerApps] en [registreren en gebruiken van aangepaste connectors in Microsoft Flow].

1. Open de [Powerapps webportal](https://web.powerapps.com) of de [Microsoft Flow webportal](https://flow.microsoft.com/), en meld u aan. 

2. Klik op de **instellingen** (het pictogram tandwielpictogram) op de rechterbovenhoek van de pagina en selecteer knop **aangepaste connectors**. 

3. Klik op **maken van aangepaste connector**.

4. Op de **algemene** tabblad, Geef een naam voor uw API en vervolgens de definitie OpenAPI uploaden of plak in de metagegevens-URL. Klik op **gaan**.

4. Op de **beveiliging** tabblad als u wordt gevraagd om te voorzien van verificatiegegevens, voer de waarden in de vorige sectie hebt verkregen. Als dat niet het geval is, gaat u verder met de volgende stap.

5. Op de **definities** tabblad alle bewerkingen die zijn gedefinieerd in uw bestand OpenAPI worden automatisch ingevuld. Als alle vereiste bewerkingen zijn gedefinieerd, kunt u gaan met de volgende stap. Zo niet, u kunt toevoegen en bewerkingen hier wijzigen.

6. Klik op **-connector maken**. Als u testen API-aanroepen wilt, gaat u naar de volgende stap.

7. Op de **testen** tabblad, geen verbinding maken, selecteer een bewerking voor het testen en voer alle gegevens die nodig is voor de bewerking.

8. Klik op **testen bewerking**.


<a name="auth"></a>
## <a name="authentication"></a>Authentication

PowerApps en Microsoft-Flow ondersteuning systeemeigen voor een verzameling van id-providers die kunnen worden gebruikt om aan te melden gebruikers van uw aangepaste connector. Als uw API is verificatie vereist, zorg ervoor dat deze wordt vastgelegd als een _beveiliging definitie_ in uw document OpenAPI. Tijdens het exporteren moet u bieden configuratiewaarden waarmee PowerApps een Microsoft-Flow aanmelding acties uit te voeren.

Deze sectie bevat informatie over de verificatietypen die worden ondersteund door de express-stroom: API-sleutel, Azure Active Directory en algemene OAuth 2.0. Zie voor een volledige lijst met providers en de referenties voor elk is vereist, [registreren en gebruiken van aangepaste connectors in PowerApps] en [registreren en gebruiken van aangepaste connectors in Microsoft Flow].

### <a name="api-key"></a>API-sleutel
Wanneer dit beveiligingsschema wordt gebruikt, worden de gebruikers van de connector wordt gevraagd naar de sleutel opgeven wanneer ze een verbinding maakt. U kunt de naam om te weten welke sleutel is vereist in een API-sleutel opgeven. Voor Azure Functions wordt dit doorgaans een van de sleutels van de host die betrekking hebben op de verschillende functies in de functie-app.

### <a name="azure-active-directory"></a>Azure Active Directory
Bij het configureren van een aangepaste connector die AAD aanmelding vereist twee AAD-toepassing registraties zijn vereist: één voor het modelleren van de back-end API en één als model voor de connector in PowerApps en stroom.

Uw API moet worden geconfigureerd om te werken met de eerste registratie en dit wordt al worden afgehandeld als u gebruikt de [App Service-verificatie/autorisatie](https://docs.microsoft.com/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication) functie.

U moet handmatig de registratie van de tweede voor de connector te maken met de stappen behandeld in [een AAD-toepassing toe te voegen](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-an-application). De registratie moet hebben toegang tot uw API en antwoord-URL van de gedelegeerde `https://msmanaged-na.consent.azure-apim.net/redirect`. Zie [in dit voorbeeld](
https://powerapps.microsoft.com/tutorials/customapi-azure-resource-manager-tutorial/) vervangen voor meer details over uw API voor de Azure Resource Manager.

De volgende configuratiewaarden zijn vereist:
- **Client-ID** -de client-ID van de registratie van de AAD-connector
- **Clientgeheim** -het clientgeheim van de registratie van de AAD-connector
- **Aanmeldings-URL** -de basis-URL voor AAD. In de openbare Azure, dit wordt doorgaans `https://login.windows.net`.
- **Tenant-ID** -de ID van de tenant moet worden gebruikt voor de aanmelding. Dit moet 'algemene' of de ID van de tenant waarin de connector wordt gemaakt.
- **Bron-URL** -de bron-URL van uw API-back-end AAD-registratie

> [!IMPORTANT]
> Als een andere persoon de API-definitie in PowerApps en Microsoft-Flow als onderdeel van de handmatige stroom importeren wilt, moet u hen voorzien van de client-ID en clientgeheim **van de registratie van de connector**, evenals de bron-URL van uw API. Zorg ervoor dat deze geheime gegevens veilig worden beheerd. **De beveiligingsreferenties van de API zelf niet delen.**

### <a name="generic-oauth-20"></a>Algemene OAuth 2.0
De algemene OAuth 2.0-ondersteuning kunt u integreren met elke OAuth 2.0-provider. Hiermee kunt u op te zetten in een aangepaste provider die niet systeemeigen worden ondersteund.

De volgende configuratiewaarden zijn vereist:
- **Client-ID** -de OAuth 2.0-client-ID
- **Clientgeheim** -het clientgeheim OAuth 2.0
- **Autorisatie-URL** -OAuth 2.0-autorisatie-URL
- **URL token** -de URL van OAuth 2.0-token
- **Vernieuwen van de URL** -URL van de OAuth 2.0-vernieuwen



[registreren en gebruiken van aangepaste connectors in PowerApps]: https://powerapps.microsoft.com/tutorials/register-custom-api/
[registreren en gebruiken van aangepaste connectors in Microsoft Flow]: https://flow.microsoft.com/documentation/register-custom-api/

---
ms.assetid: 
title: aaaAzure Sleutelkluis voorlopig verwijderen | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/10/2017
ms.openlocfilehash: 1b402c58db6f25ae4ae5e2720786fa81eb0e839a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-soft-delete-overview"></a>Overzicht van Azure Sleutelkluis voorlopig verwijderen

Functie van de voorlopig verwijderen van de Sleutelkluis kunt Hallo verwijderd kluizen en bekende als voorlopig verwijderd kluis objecten herstellen. We houden in het bijzonder Hallo volgen scenario's:

- Ondersteuning voor herstelbare verwijdering van een sleutelkluis
- Ondersteuning voor herstelbare verwijderen van sleutelkluis-objecten (ex. sleutels, geheimen, certificaten)

## <a name="supporting-interfaces"></a>Interfaces ondersteunen

Hallo soft-delete-functie is in eerste instantie beschikbaar via Hallo REST, .NET / C# en PowerShell-interfaces. Raadpleeg toohello verwijzingen van deze voor meer informatie [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).

## <a name="scenarios"></a>Scenario's

Azure sleutel kluizen worden bijgehouden resources, beheerd door Azure Resource Manager. Azure Resource Manager bevat ook een goed gedefinieerde gedrag voor verwijdering, die vereist dat een geslaagde verwijderbewerking moet resulteren in die resource niet meer wordt toegankelijk. Hallo voorlopig verwijderen functie adressen Hallo herstel van Hallo verwijderd object, of Hallo verwijdering per ongeluk of opzettelijk was.

1. In een typisch scenario hello, een gebruiker mogelijk per ongeluk verwijderd een sleutelkluis of een sleutelkluis-object. Als die sleutelkluis of key object toobe herstelbare zijn voor een vooraf bepaalde periode Vault, mag de Hallo gebruiker Hallo verwijderen ongedaan maken en hun gegevens herstellen.

2. In een ander scenario kan een kwaadwillende gebruiker toodelete proberen een sleutelkluis of een object van de sleutelkluis, zoals een sleutel in een kluis, toocause een onderbreking van de business. Hallo verwijderen van de sleutelkluis Hallo of sleutelkluis object scheiden van feitelijke verwijdering Hallo Hallo onderliggende gegevens kan worden gebruikt als veiligheidsmaatregel door, bijvoorbeeld rol beperken van machtigingen voor gegevens verwijdering tooa verschillen, vertrouwd. Deze benadering vergt effectief quorum voor een bewerking die anders in een onmiddellijke gegevensverlies resulteert mogelijk.

### <a name="soft-delete-behavior"></a>Gedrag voor voorlopig verwijderen

Met deze functie Hallo DELETE-bewerking op een sleutelkluis of sleutelkluis-object is een soft-verwijderen, effectief Hallo resources houden voor een bepaalde bewaartermijn, terwijl waardoor Hallo lijkt dat Hallo-object is verwijderd. verder Hallo-service biedt een mechanisme voor het herstellen van Hallo verwijderd object, in wezen Hallo verwijdering ongedaan te maken. 

Voorlopig verwijderen is een optionele Sleutelkluis gedrag en is **niet standaard ingeschakeld** in deze release. Zie voor meer informatie over het inschakelen van voorlopig verwijderen voor uw sleutelkluis, specifieke hulp in Hallo-documentatie voor interface van uw keuze Hallo Hallo [Key Vault Reference](https://docs.microsoft.com/azure/key-vault/).

### <a name="key-vault-recovery"></a>Sleutelkluis-herstel

Bij het verwijderen van een sleutelkluis maakt Hallo-service een proxy-resource onder Hallo-abonnement toe te voegen voldoende metagegevens voor herstel. Hallo proxy bron is een opgeslagen object beschikbaar in Hallo dezelfde locatie als de sleutelkluis Hallo verwijderd. 

### <a name="key-vault-object-recovery"></a>Sleutelkluis objectherstel

Bij het verwijderen van een object van de sleutelkluis, zoals een sleutel plaatst Hallo service Hallo-object in een verwijderde staat bevindt, waardoor deze niet toegankelijk tooany bewerkingen voor het ophalen. In deze status kan Hallo sleutelkluis-object alleen worden weergegeven, herstelde of geforceerd/permanent verwijderd. 

Op Hallo dezelfde tijd en de belangrijkste kluis wordt gepland Hallo verwijdering van de onderliggende gegevens van de bijbehorende toohello verwijderd Hallo sleutelkluis of sleutelkluis-object voor uitvoering na een vooraf vastgestelde retentie-interval. Hallo DNS-record betreffende toohello kluis wordt ook bewaard gedurende Hallo Hallo retentie-interval.

### <a name="soft-delete-retention-period"></a>Bewaarperiode voor voorlopig verwijderen

Voorlopig verwijderde bronnen worden bewaard gedurende een bepaalde tijd, 90 dagen. Tijdens het Hallo voorlopig verwijderen retentie-interval, Hallo volgende van toepassing:

- U kunt alle sleutelkluizen hello en sleutelkluis-objecten in Hallo voorlopig verwijderen voor uw abonnement, evenals de verwijdering en herstel informatie over deze aanbieden.
    - Alleen gebruikers met speciale machtigingen kunnen verwijderde kluizen aanbieden. U kunt het beste onze gebruikers een aangepaste beveiligingsrol maken met deze speciale machtigingen voor de verwerking van verwijderde kluizen.
- Een sleutelkluis met dezelfde naam kan niet worden gemaakt in Hallo Hallo dezelfde locatie; : een sleutelkluis-object kan niet worden gemaakt in een kluis gegeven als dat sleutelkluis een object met Hallo bevat dezelfde naam en deze bevindt zich in een verwijderde staat bevindt 
- Alleen een specifiek bevoegde gebruiker mogelijk een sleutelkluis of sleutelkluis object hersteld door een opdracht herstellen op Hallo bijbehorende proxy resource.
    - Hallo-gebruiker lid is van de aangepaste rol Hallo, die Hallo bevoegdheid toocreate een sleutelkluis onder de resourcegroep Hallo heeft kunt Hallo kluis herstellen.
- Alleen een specifiek bevoegde gebruiker mogelijk een sleutelkluis of sleutelkluis-object door uitgifte van een verwijderopdracht in het bijbehorende proxy resource Hallo geforceerd verwijderen.

Tenzij een sleutelkluis of sleutelkluis-object is hersteld, op Hallo voert einde van Hallo retentie-interval Hallo service een opschonen van de sleutelkluis Hallo voorlopig verwijderde of sleutelkluis-object en de inhoud ervan. Verwijderen van de resource kan niet opnieuw worden gepland.

### <a name="permitted-purge"></a>Toegestane opschonen

Permanent verwijderen, verwijderen, wordt een sleutelkluis is mogelijk via een POST-bewerking op Hallo proxy resource en speciale bevoegdheden vereist. In het algemeen worden alleen de eigenaar van Hallo-abonnement kunnen toopurge een sleutelkluis. Hallo POST-bewerking triggers Hallo onmiddellijk en onherstelbare verwijdering van deze kluis. 

Een toothis uitzondering is het Hallo geval hello Azure-abonnement is gemarkeerd als *niet kan*. In dit geval alleen Hallo service voert de werkelijke verwijdering Hallo en als een geplande proces gebeurt. 




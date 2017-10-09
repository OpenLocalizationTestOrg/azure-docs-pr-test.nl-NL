---
ms.assetid: 
title: aaaAzure Sleutelkluis beveiligingswerelden | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 07/03/2017
ms.openlocfilehash: 1995119c9e9886829d6c50af921f275d10e382f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-security-worlds-and-geographic-boundaries"></a>Beveiligingswerelden voor Azure Sleutelkluis en de geografische grenzen

Azure Sleutelkluis is een multitenant-service en een pool van Hardware Security Modules (HSM's) in elke Azure-locatie gebruikt. 

Alle HSM's op Azure locaties in Hallo Hallo dezelfde geografische regio delen dezelfde grens van cryptografische (Beveiligingswereld Thales). Bijvoorbeeld, Hallo VS-Oost en West, VS delen dezelfde beveiligingswereld omdat ze toohello VS geografische locatie horen. Op deze manier alle Azure locaties in Japan share Hallo dezelfde beveiligingswereld en alle Azure locaties in Australië, India, enzovoort. 

## <a name="backup-and-restore-behavior"></a>Gedrag van back-up en herstel

Een back-up van een sleutel van een sleutelkluis in een Azure-locatie kan worden hersteld tooa sleutelkluis in een andere Azure-locatie, mits beide volgende voorwaarden voldaan wordt:

- Beide hello Azure locaties behoren toohello dezelfde geografische locatie
- Beide Hallo sleutelkluizen toohello deel uitmaken van hetzelfde Azure-abonnement

Een back-up door een bepaald abonnement van een sleutel in een sleutelkluis in India West, kan bijvoorbeeld alleen worden teruggezet tooanother sleutelkluis in Hallo hetzelfde abonnement en dezelfde geografische locatie; India West, India centraal of Zuid, India.

## <a name="regions-and-products"></a>Regio's en -producten

- [Azure-regio's](https://azure.microsoft.com/regions/)
- [Microsoft-producten per regio](https://azure.microsoft.com/regions/services/)

Regio's zijn toegewezen toosecurity werelden, weergegeven als primaire koppen in Hallo tabellen:

In Hallo producten per regio artikel, bijvoorbeeld Hallo **Americas** tabblad bevat Oost US, VS-midden, VS-WEST alle toewijzing toohello Americas regio. 

>[!NOTE]
>Een uitzondering is dat ons DOD Oost en ons DOD centrale hun eigen beveiligingswerelden hebben. 

Op deze manier op Hallo **Europa** tabblad Noord-Europa en WEST-Europa beide toohello Europa regio toegewezen. Hallo geldt ook op Hallo **Azië** tabblad.




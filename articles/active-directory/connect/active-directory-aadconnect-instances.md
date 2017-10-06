---
title: 'Azure AD Connect: Service-exemplaren synchroniseren | Microsoft Docs'
description: Deze pagina worden speciale overwegingen voor exemplaren van Azure AD.
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: f340ea11-8ff5-4ae6-b09d-e939c76355a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 2a0d8a599cf84cd6530bdbb24951156510d2cf3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-special-considerations-for-instances"></a>Azure AD Connect: Speciale overwegingen voor exemplaren
Azure AD Connect wordt meestal gebruikt met hello world wide exemplaar van Azure AD en Office 365. Maar er zijn ook andere exemplaren en deze hebben verschillende vereisten voor de URL's en andere speciale overwegingen.

## <a name="microsoft-cloud-germany"></a>Microsoft Cloud Duitsland
Hallo [Microsoft Cloud Duitsland](http://www.microsoft.de/cloud-deutschland) is een soevereine cloud beheerd door een beheerder Duitse gegevens.

| URL's tooopen in proxyserver |
| --- |
| \*. microsoftonline.de |
| \*.windows.net |
| + Intrekkingslijsten voor certificaten |

Wanneer u zich aanmeldt tooyour Azure AD-tenant, moet u een account in Hallo onmicrosoft.de domein gebruiken.

Functies die momenteel niet aanwezig in Hallo Microsoft Cloud Duitsland:

* **Azure AD Connect Health** is niet beschikbaar.
* **Automatische updates** is niet beschikbaar.
* **Wachtwoord terugschrijven** is beschikbaar voor het voorbeeld met Azure AD Connect versie 1.1.570.0 en na.
* Andere Azure AD Premium-services zijn niet beschikbaar.

## <a name="microsoft-azure-government-cloud"></a>Microsoft Azure Government cloud
Hallo [Microsoft Azure Government cloud](https://azure.microsoft.com/features/gov/) is een cloudservice voor de overheid.

Deze cloud werd ondersteund door eerdere releases van DirSync. Vanaf build 1.1.180 van Azure AD Connect wordt Hallo volgende generatie Hallo cloud ondersteund. Deze generatie alleen VS gebaseerde eindpunten gebruikt en een andere lijst met URL's tooopen hebben in uw proxy-server.

| URL's tooopen in proxyserver |
| --- |
| \*.microsoftonline.com |
| \*. microsoftonline.us |
| \*. gov.us.microsoftonline.com |
| + Intrekkingslijsten voor certificaten |

Kan geen Azure AD Connect tooautomatically detecteren dat uw Azure AD-tenant bevindt zich in de cloud van de overheid Hallo. In plaats daarvan moet u tootake Hallo van de volgende activiteiten wanneer u Azure AD Connect installeert.

1. Hello Azure AD Connect-installatie start.
2. Wanneer er Hallo van de eerste pagina waar u gewoonlijk tooaccept Hallo overeenkomst, niet worden voortgezet, maar laat Hallo-installatiewizard uitgevoerd.
3. Start regedit en wijzigt u de registersleutel Hallo `HKLM\SOFTWARE\Microsoft\Azure AD Connect\AzureInstance` toohello waarde `2`.
4. Ga terug toohello Azure AD Connect-installatiewizard, Hallo overeenkomst te accepteren en doorgaan. Zorg ervoor dat toouse Hallo tijdens de installatie van **aangepaste configuratie** installatie pad (en niet de Express-installatie). Ga vervolgens door gewoon Hallo-installatie.

Functies die momenteel niet aanwezig in Hallo Microsoft Azure Government cloud:

* **Azure AD Connect Health** is niet beschikbaar.
* **Automatische updates** is niet beschikbaar.
* **Wachtwoord terugschrijven** is beschikbaar voor het voorbeeld met Azure AD Connect versie 1.1.570.0 en na.
* Andere Azure AD Premium-services zijn niet beschikbaar.

## <a name="next-steps"></a>Volgende stappen
Lees meer over het [integreren van uw on-premises identiteiten met Azure Active Directory](active-directory-aadconnect.md).

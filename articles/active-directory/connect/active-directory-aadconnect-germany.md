---
title: aaaAzure AD Connect in de Microsoft Cloud Duitsland
description: "Azure AD Connect integreert uw on-premises directory's met Azure Active Directory. Hiermee kunt u een algemene identiteit voor Office 365, Azure en SaaS toepassingen die zijn geïntegreerd met Azure AD tooprovide."
keywords: Inleiding tooAzure AD Connect, overzicht van Azure AD Connect, wat is Azure AD Connect, active directory, Duitsland, zwart Forest installeren
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 2bcb0caf-5d97-46cb-8c32-bda66cc22dad
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: f32194fa6c365614f68e5d1ddcf0dac44d223292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-in-microsoft-cloud-germany---public-preview"></a>Azure AD Connect in Microsoft Cloud Duitsland - Openbare preview
## <a name="introduction"></a>Inleiding
Azure AD Connect voorziet in synchronisatie tussen uw on-premises Active Directory en Azure Active Directory.
Op dit moment veel Hallo scenario's in [Microsoft Cloud Duitsland](https://www.microsoft.com/de-de/cloud/deutschland/default.aspx) door Hallo operator moet worden uitgevoerd. Wanneer u Microsoft Cloud Duitsland gebruikt, moet u zich bewust zijn van de volgende Hallo:

* Hallo die volgende URL's moeten worden geopend op een proxyserver voor synchronisatie toooccur is:
  
  * *.microsoftonline.de
  * *.windows.net
  * * Certificaatintrekkingslijsten
* Wanneer u Azure AD-directory tooyour aanmelden, moet u een account in Hallo onmicrosoft.de domein.
* Hallo volgende kenmerken zijn niet beschikbaar:
  * Azure AD Connect Health (Engelstalig)
  * Automatische updates
 
## <a name="download"></a>Downloaden
U kunt Azure AD Connect downloaden van Azure AD Connect-blade Hallo binnen Hallo-portal.  Gebruik onderstaande toolocate hello Azure AD Connect-blade Hallo-instructies.

### <a name="hello-azure-ad-connect-blade"></a>Hello Azure AD Connect-Blade
Wanneer u bent aangemeld in toohello Azure-portal, Hallo te volgen:

1. Ga tooBrowse
2. Selecteer Azure Active Directory
3. Selecteer vervolgens Azure AD Connect

Hier ziet u de volgende Hallo:

![De Azure AD Connect-blade](media/active-directory-aadconnect-germany/germany1.png)

Hello volgende tabel worden weergegeven in de blade Hallo Hallo-functies.

| Titel | Beschrijving |
| --- | --- |
| SYNCHRONISATIESTATUS |Hier ziet u of synchronisatie is in- of uitgeschakeld. |
| LAATSTE SYNCHRONISATIE |Hallo laatste keer dat een geslaagde synchronisatie is voltooid. |
| FEDERATIEVE DOMEINEN |Toont Hallo aantal federatieve domeinen die momenteel zijn geconfigureerd. |

## <a name="installation"></a>Installeren
Azure AD Connect tooinstall, kunt u documentatie Hallo [hier](active-directory-aadconnect.md#install-azure-ad-connect).

## <a name="advanced-features-and-additional-information"></a>Geavanceerde functies en aanvullende informatie
Zie [Uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md) voor meer informatie en tips over aangepaste instellingen en geavanceerde configuraties.  Deze pagina bevat informatie en koppelingen tooadditional richtlijnen.


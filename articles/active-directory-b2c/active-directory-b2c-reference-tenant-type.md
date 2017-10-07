---
title: 'Azure Active Directory B2C: Regio beschikbaarheid & gegevens hand vestigingsplaats | Microsoft Docs'
description: Een onderwerp op Hallo soorten tenants van Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: gsacavdm
manager: krassk
editor: bryanla
ms.assetid: 8a0644da-b825-4edc-8ce9-541c3c976afb
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: gsacavdm
ms.openlocfilehash: d382921fe9d62183b6d52c47d62f952dabd116c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-region-availability--data-residency"></a>Azure Active Directory B2C: Regio beschikbaarheid & gegevens hand vestigingsplaats
Beschikbaarheid in regio's en de hand van gegevens vestigingsplaats zijn twee heel andere concepten die anders tooAzure AD B2C van de rest Hallo van Azure toepassen. In dit artikel wordt Hallo verschillen tussen deze twee concepten uitgelegd en vergelijken hoe ze tooAzure ten opzichte van Azure AD B2C van toepassing.

## <a name="summary"></a>Samenvatting
Azure AD B2C wordt **algemeen beschikbaar wereldwijd** met de optie Hallo **hand vestigingsplaats gegevens in de Verenigde Staten of Europa**.

## <a name="concepts"></a>Concepten
* **Beschikbaarheid in regio's** toowhere verwijst een service is beschikbaar voor gebruik.
* **De hand van gegevens vestigingsplaats** verwijst toowhere gebruiker gegevens worden opgeslagen.

## <a name="region-availability"></a>Beschikbaarheid in regio’s
Azure AD B2C is wereldwijd beschikbaar via hello Azure openbare cloud. 

Dit verschilt van Hallo model meeste andere Azure-services volgen die Combineer beschikbaarheid aan de hand van gegevens vestigingsplaats. Ziet u voorbeelden van deze in beide Azure [beschikbare producten door regio](https://azure.microsoft.com/regions/services/) pagina en Hallo [Active Directory B2C prijscategorie Rekenmachine](https://azure.microsoft.com/pricing/details/active-directory-b2c/).

## <a name="data-residency"></a>Gegevensresidentie
Azure AD B2C slaat gebruikersgegevens in de Verenigde Staten of Europa.

De hand van gegevens vestigingsplaats wordt bepaald op basis van welke land/regio is geselecteerd als [maken van een Azure AD B2C-tenant](active-directory-b2c-get-started.md).

![Schermopname van een tenant preview](./media/active-directory-b2c-reference-tenant-type/data-residency-b2c-tenant.png)

Gegevens zich in de Verenigde Staten Hallo voor Hallo landen/regio's te volgen:

> Verenigde Staten, Canada, Costa Rica, Dominicaanse Republiek, El Salvador, Guatemala, Mexico, Panama, Portorico en Trinidad en Tobago

Gegevens zich bevindt in Europa voor Hallo landen/regio's te volgen:

> Algerije, Oostenrijk, Azerbeidzjan, Bahrein, Belarus, België, Bulgarije, Kroatië, Cyprus, Tsjechië, Denemarken, Egypte, Estland, Finland, Frankrijk, Duitsland, Griekenland, Hongarije, IJsland, Ierland, Israël, Italië, Jordanië, Kazachstan, Kenia, Koeweit, Letland, Libanon, Liechtenstein, NNNNNN, Luxemburg, Macedonië Macedonisch, Malta, Montenegro, Marokko, Nederland, Nigeria, Noorwegen, Oman, Pakistan, Polen, Portugal, Qatar, Roemenië, Rusland, Saudi-Arabië, Servië, Slowakije, Slovenië, Zuid-Afrika, Spanje, Zweden, Zwitserland, Tunesië, Turkije, Oekraïne, VAE en Verenigd Koninkrijk.

resterende Hallo-landen/regio's zijn in Hallo proces toohello lijst wordt toegevoegd.  Op dit moment kunt u Azure AD B2C door het verzamelen van Hallo landen/regio's hierboven.

> Afghanistan, Argentinië, Australië, Brazilië, onderliggende, Colombia, Ecuador, Hongkong SAR, India, Indonesië, Irak, Japan, Korea, Maleisië, Nieuw-Zeeland, Paraguay, Peru, Filipijnen, Singapore, Sri Lanka, Taiwan, Thailand, Uruguay en Venezuela.

## <a name="preview-tenant"></a>Preview-tenant
Als u een B2C-tenant had gemaakt in Azure AD B2C preview-periode, is het waarschijnlijk dat uw **Tenant-type** zegt **Preview tenant**. Als dit Hallo geval is, moet u uw tenant alleen voor ontwikkelings- en testdoeleinden en niet voor productie-apps gebruiken.

> [!IMPORTANT]
> Er is geen migratiepad van een preview B2C-tenant tooa productie scale B2C-tenant. Let op: Er zijn bekende problemen bij het verwijderen van een preview B2C-tenant en maak opnieuw een productie-scale B2C-tenant met Hallo dezelfde domeinnaam. U hebt een productie-scale B2C-tenant met een andere domeinnaam toocreate.


![Schermopname van een tenant preview](./media/active-directory-b2c-reference-tenant-type/preview-b2c-tenant.png)

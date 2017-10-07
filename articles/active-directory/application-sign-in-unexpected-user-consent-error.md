---
title: AAA onverwachte fout bij het uitvoeren van toestemming tooan toepassing | Microsoft Docs
description: Fouten die zich kunnen voordoen tijdens Hallo van ermee akkoord dat tooan toepassings- en wat u kunt doen over te komen aan bod
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: dfee35f3a10e3cc4313109cedd972499452320f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="unexpected-error-when-performing-consent-tooan-application"></a>Onverwachte fout bij het uitvoeren van toestemming tooan toepassing

Dit artikel bevat fouten die zich tijdens Hallo van ermee akkoord dat tooan toepassing voordoen kunnen. Als u problemen met onverwachte toestemming wordt gevraagd dat niet eventuele foutberichten bevatten, Zie [verificatie scenario's voor Azure AD](https://docs.microsoft.com/azure/active-directory/develop/active-directory-authentication-scenarios).

Veel toepassingen die zijn geïntegreerd met Azure Active Directory vereisen machtigingen tooaccess andere bronnen in de volgorde toofunction. Wanneer u deze resources zijn ook worden geïntegreerd met Azure Active Directory, toestemming machtigingen tooaccess ze vaak wordt aangevraagd met behulp van algemene Hallo framework. 

Dit resulteert in een instemmingsprompt wordt weergegeven, die doorgaans Hallo eerst een toepassing wordt gebruikt, maar kan ook optreden op een later gebruik van de toepassing hello plaatsvindt.

Bepaalde voorwaarden worden voldaan voor een gebruiker tooconsent toohello machtigingen vereist zijn voor een toepassing. Als u deze voorwaarden niet wordt voldaan, kunnen er diverse fouten optreden. Deze omvatten:

## <a name="requesting-not-authorized-permissions-error"></a>Niet-geautoriseerde Machtigingsfout aanvragen
* **AADSTS90093:** &lt;clientAppDisplayName&gt; vraagt een of meer machtigingen die u niet bent gemachtigd toogrant. Neem contact op met een beheerder, die kan toothis toepassing namens jou toestemming.

Deze fout treedt op wanneer een gebruiker die geen beheerder van een bedrijf probeert een toepassing die de machtigingen die alleen een beheerder kan verlenen aanvraagt toouse. Deze fout kan worden opgelost door een beheerder het verlenen van toegang toohello toepassing namens hun organisatie.

## <a name="policy-prevents-granting-permissions-error"></a>Beleid voorkomt dat machtigingen verlenen fout
* **AADSTS90093:** beheerder van &lt;tenantDisplayName&gt; heeft een beleid dat u niet verlenen ingesteld &lt;naam van de app&gt; Hallo machtigingen het vraagt. Neem contact op met de beheerder van &lt;tenantDisplayName&gt;, wie machtigingen toothis app namens jou kunnen verlenen.

Deze fout treedt op wanneer de beheerder uitgeschakeld Hallo mogelijkheid voor gebruikers tooconsent tooapplications wordt, en vervolgens een gebruiker die geen beheerder probeert een toepassing die toestemming nodig om toouse. Deze fout kan worden opgelost door een beheerder het verlenen van toegang toohello toepassing namens hun organisatie.

## <a name="intermittent-problem-error"></a>Onregelmatige probleem fout
* **AADSTS90090:** het lijkt erop dat we een onregelmatig probleem recording Hallo machtigingen die u hebt geprobeerd toogrant te aangetroffen&lt;clientAppDisplayName&gt;. Probeer het later opnieuw.

Deze fout geeft aan dat er een probleem onregelmatige service aan de clientzijde is opgetreden. Deze kan worden opgelost door tooconsent toohello toepassing opnieuw probeert.

## <a name="resource-not-available-error"></a>Resource niet beschikbaar-fout
* **AADSTS65005:** Hallo app &lt;clientAppDisplayName&gt; aangevraagd machtigingen tooaccess een resource &lt;resourceAppDisplayName&gt; die is niet beschikbaar. 

Neem contact op met de ontwikkelaar van de toepassing hello.

##  <a name="resource-not-available-in-tenant-error"></a>De resource is niet beschikbaar in de tenant-fout
* **AADSTS65005:** &lt;clientAppDisplayName&gt; vraagt toegang tooa resource &lt;resourceAppDisplayName&gt; die is niet beschikbaar in uw organisatie &lt; tenantDisplayName&gt;. 

Zorg ervoor dat deze resource beschikbaar is of neem contact op met de beheerder van &lt;tenantDisplayName&gt;.

## <a name="permissions-mismatch-error"></a>Fout met niet overeenkomende machtigingen
* **AADSTS65005:** Hallo app aangevraagd toestemming tooaccess resource &lt;resourceAppDisplayName&gt;. Deze aanvraag is mislukt omdat deze komt niet overeen met het hoe Hallo app is vooraf geconfigureerd tijdens de registratie van de app. Neem contact op met Hallo app vendor.* *

Deze alle fouten optreden wanneer de toepassing hello een gebruiker probeert tooconsent toois aanvragen machtigingen tooaccess een resource-toepassing die niet is gevonden in de map van de organisatie van de Hallo (tenant). Dit kan verschillende redenen optreden:

-   toepassingsontwikkelaar Hallo-client heeft de toepassing niet goed geconfigureerd, waardoor toorequest toegang tooan ongeldige resource. In dit geval moet Hallo toepassingsontwikkelaar bijwerken Hallo configuratie van Hallo client toepassing tooresolve dit probleem.

-   Een Service-Principal voor de doeltoepassing resource Hallo bestaat niet in de organisatie hello, of voorkomen in het verleden Hallo maar is verwijderd. tooresolve dit probleem, een Service-Principal voor Hallo resource toepassing moet worden ingericht in Hallo organisatie zodat het Hallo-clienttoepassing tooit machtigingen kan aanvragen. Dit kan gebeuren in een aantal manieren, afhankelijk van Hallo type toepassing, met inbegrip van:

    -   Ophalen van een abonnement voor de resource-toepassing hello (Microsoft gepubliceerde toepassingen)

    -   Ermee akkoord dat toohello resource toepassing

    -   Machtigingen Hallo toepassing via hello Azure Portal

    -   Hallo-toepassing toe te voegen uit hello Azure AD-Toepassingsgalerie

## <a name="next-steps"></a>Volgende stappen 

[Apps, machtigingen en toestemming in Azure Active Directory (v1-eindpunt)](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent)<br>

[Scopes, machtigingen en toestemming in hello Azure Active Directory (v2.0-eindpunt)](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)



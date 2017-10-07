---
title: aaaApplication pagina niet correct weergegeven voor een toepassing toepassingsproxy | Microsoft Docs
description: "Hulp bij het Hallo-pagina is niet correct weergegeven in een toepassing Proxy-toepassing hebt geïntegreerd met Azure AD"
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
ms.openlocfilehash: f4abaa4e94c512868f2085affe59cac443784a56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="application-page-does-not-display-correctly-for-an-application-proxy-application"></a>Toepassingspagina weergegeven niet correct voor een toepassing toepassingsproxy

In dit artikel kunt u tootroubleshoot problemen met Azure Active Directory-toepassingsproxy toepassingen wanneer u toohello pagina navigeert, maar er op de pagina Hallo ziet er niet juist.

## <a name="overview"></a>Overzicht
Wanneer u een toepassingsproxy-app publiceert, zijn alleen pagina's in uw hoofdmap toegankelijk wanneer toegang tot de toepassing hello. Als het Hallo-pagina is niet correct weergegeven, ontbreekt Hallo hoofdmap interne URL die wordt gebruikt voor de toepassing hello enkele informatiebronnen die pagina. tooresolve, zorg ervoor dat u hebt gepubliceerd *alle* Hallo resources voor Hallo pagina als onderdeel van uw toepassing.

U kunt controleren of dit Hallo probleem is door het openen van het beheer van uw netwerk (zoals Fiddler of F12 extra in Internet Explorer/Edge), Hallo pagina te laden en zoekt u 404-fouten. Die Hallo-pagina's die momenteel is niet gevonden en moeten nog steeds gepubliceerd toobe aangeeft.

Als een voorbeeld van deze aanvraag, wordt ervan uitgegaan hebt u een toepassing kosten op basis van een interne URL van gepubliceerd <http://myapps/expenses>, maar Hallo app gebruikmaakt van Hallo opmaakmodel <http://myapps/style.css>. Hallo opmaakmodel is in dit geval niet gepubliceerd in uw toepassing, zodat u een 404-fout bij poging tooload style.css laden Hallo uitgaven app genereert. In dit voorbeeld zou Hallo probleem worden opgelost door het publiceren van de toepassing hello met een interne URL <http://myapp/> in plaats daarvan.

## <a name="problems-with-publishing-as-one-application"></a>Problemen met de publicatie als één toepassing

Als het niet mogelijk toopublish alle resources binnen dezelfde toepassing hello, u moet toopublish meerdere toepassingen en koppelingen tussen deze twee inschakelen.

toodo geval is, wordt u aangeraden Hallo [aangepaste domeinen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) oplossing. Deze oplossing vereist echter dat u Hallo-certificaat voor uw domein bezit en uw toepassingen volledig gekwalificeerde domeinnamen (FQDN's) gebruiken. Zie voor andere opties Hallo [verbroken koppelingen documentatie oplossen](https://microsoft-my.sharepoint.com/personal/harshja_microsoft_com/_layouts/15/guestaccess.aspx?guestaccesstoken=IxuG3mFVbnPWI3Yn4Qi7wCNi8VIfHS5mwPt5quh8DMw%3d&docid=2_14558cd6ddea34c1c9887dc640feb5831&rev=1).

## <a name="next-steps"></a>Volgende stappen
[Toepassingen publiceren met Azure AD-toepassingsproxy](application-proxy-publish-azure-portal.md)

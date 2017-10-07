---
title: aaaLinks op Hallo pagina werken niet voor een toepassing toepassingsproxy | Microsoft Docs
description: "Hoe tootroubleshoot problemen met een verbroken koppelingen op hebt geïntegreerd met Azure AD-toepassingsproxy-toepassingen"
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
ms.openlocfilehash: 77c1e22d27c7a6436d8e57e105037c2328180481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="links-on-hello-page-dont-work-for-an-application-proxy-application"></a>Koppelingen op de pagina Hallo werken niet voor een toepassing toepassingsproxy

In dit artikel kunt u tootroubleshoot waarom koppelingen op uw toepassing met Azure Active Directory-toepassingsproxy niet goed werken.

## <a name="overview"></a>Overzicht 
Hallo alleen koppelingen dat werk standaard in de toepassing hello koppelingen toodestinations opgenomen in Hallo zijn gepubliceerd na het publiceren van een app-toepassingsproxy basis-URL. Hallo koppelingen binnen Hallo toepassingen worden niet werkt, Hallo interne URL voor de toepassing hello omvatten waarschijnlijk niet alle Hallo bestemmingen van koppelingen binnen Hallo-toepassing.

**Waarom komt dat?** Wanneer u op een koppeling in een toepassing, Hallo toepassingsproxy pogingen tooresolve Hallo URL als een interne URL binnen dezelfde toepassing, of als een extern beschikbare URL. Als Hallo koppeling verwijst tooan interne URL die zich niet binnen dezelfde Hallo toepassing, is deze niet behoren tooeither van deze buckets en resulteert in een fout niet gevonden.

## <a name="ways-you-can-resolve-broken-links"></a>Manieren waarop die u het kunt oplossen verbroken koppelingen

Er zijn drie manieren tooresolve dit probleem. Hallo die hieronder zijn vermeld in toenemende complexiteit.

1.  Zorg ervoor dat de interne URL Hallo een toegangspunt met alle relevante Hallo-koppelingen voor de toepassing hello. Hierdoor kunnen alle koppelingen toobe opgelost als inhoud publicatie binnen Hallo van dezelfde toepassing.

    Als u interne URL Hallo wijzigt maar niet wilt dat toochange Hallo landingspagina voor gebruikers, worden de interne URL wijziging Hallo startpagina URL toohello eerder gepubliceerd. Dit kan worden gedaan door te gaan 'Azure Active Directory' -&gt; registraties van App -&gt; Selecteer toepassing hello -&gt; eigenschappen. Op dit tabblad Eigenschappen ziet u Hallo veld "startpagina URL' kan worden aangepast toobe Hallo gewenst startpagina.

2.  Als uw toepassingen volledig gekwalificeerde domeinnamen (FQDN's), gebruik [aangepaste domeinen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) toopublish uw toepassingen. Deze functie kunt Hallo dezelfde URL toobe zowel intern gebruikt en extern.

    Deze optie zorgt ervoor dat koppelingen in uw toepassing hello extern toegankelijk is via toepassingsproxy omdat Hallo koppelingen in de URL's van toointernal Hallo ook extern worden herkend. Alle koppelingen moet nog steeds toobelong tooa gepubliceerde toepassing. Met deze optie Hallo koppelingen niet hoeft echter toobelong toohello dezelfde toepassing en toomultiple toepassingen kunnen behoren.

3.  Als geen van beide opties mogelijk, voeg Hallo preview voor een nieuwe functie die URL-omzetting/herschrijven. Met deze optie interne URL's of koppelingen die aanwezig zijn in de hoofdtekst HTML Hallo van uw toepassingen worden vertaald, of 'toegewezen', toohello externe URL's voor App-Proxy gepubliceerd. Dit werkt alleen voor de koppelingen in Hallo HTML-indeling of CSS en dit niet helpt, als de koppeling wordt gegenereerd via JS. 

Als gevolg hiervan ten zeerste aangeraden Hallo [aangepaste domeinen](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains) oplossing indien mogelijk. Als u dat toojoin Hallo preview wilt, e- < aadapfeedback@microsoft.com > met Hallo applicationId(s).

## <a name="next-steps"></a>Volgende stappen
[Werken met bestaande lokale proxyservers](application-proxy-working-with-proxy-servers.md)


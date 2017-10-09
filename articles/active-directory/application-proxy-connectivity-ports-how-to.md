---
title: aaaHow tooopen Hallo firewallpoorten die nodig zijn voor een toepassing toepassingsproxy | Microsoft Docs
description: Ontdek welke poorten tooopen voor hello Azure AD-toepassingsproxy toowork correct
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
ms.openlocfilehash: cdc7badb7c15591689a3bfd6bb26da182b00fb3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooopen-hello-firewall-ports-required-for-an-application-proxy-application"></a>Hoe tooopen firewallpoorten die nodig zijn voor een toepassing toepassingsproxy Hallo

een volledige lijst met poorten Hallo vereist en de Hallo-functie van elke poort toosee Zie Hallo vereisten sectie Hallo [toepassingsproxy documentatie](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-enable). Houd er rekening mee dat toepassingsproxy alleen uitgaande poorten gebruikt.

U kunt ook controleren of u beschikt over alle vereiste Hallo poorten openen door Hallo openen [Connectorhulpprogramma poorten Test](https://aadap-portcheck.connectorporttest.msappproxy.net/) vanuit uw on-premises netwerk. Meer een groen vinkje betekent groter tolerantie. 

## <a name="app-proxy-regions"></a>Toepassingsproxy van regio 's

We werken op een manier die u weet welke van deze gebieden toolet toobe groen voor u moet. Zorg dat ze allemaal zijn op dit moment. VS-midden is ook vereist, ongeacht welke regio in.

toomake ervoor Hallo hulpprogramma biedt u de juiste resultaten Hallo moet:

-   Hallo-hulpprogramma op een browser openen vanuit Hallo server waar u Hallo Connector hebt geïnstalleerd.

-   Zorg ervoor dat alle proxy's en firewalls toepasselijk tooyour Connector zijn ook toothis pagina toegepast. Dit kan worden gedaan in Internet Explorer door te gaan**instellingen**  - &gt; **Internetopties**  - &gt; **verbindingen**  - &gt; **Lan-instellingen**. Op deze pagina ziet u Hallo veld 'Gebruik een Proxy-Server voor uw LAN'. Schakel dit selectievakje in en Hallo proxyadres in Hallo 'Adres' veld geplaatst.

## <a name="next-steps"></a>Volgende stappen
[Azure AD-toepassingsproxy connectors begrijpen](application-proxy-understand-connectors.md)

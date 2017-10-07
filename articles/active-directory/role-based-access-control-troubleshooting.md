---
title: aaaTroubleshoot Azure RBAC | Microsoft Docs
description: Hulp bij problemen of vragen hebt over op rollen gebaseerd toegangsbeheer resources.
services: azure-portal
documentationcenter: na
author: andredm7
manager: femila
ms.assetid: df42cca2-02d6-4f3c-9d56-260e1eb7dc44
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: andredm
ms.reviewer: rqureshi
ms.openlocfilehash: 15feced32d8459d90c4c246d335932f90e1fc91f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="role-based-access-control-troubleshooting"></a>Probleemoplossing voor toegangsbeheer op basis van rollen

In dit artikel document antwoorden op veelgestelde vragen over Hallo specifieke toegangsrechten die zijn verleend aan rollen, zodat u welke tooexpect weet wanneer met behulp van rollen in Azure-portal Hallo Hallo en toegangsproblemen kunnen oplossen. Deze drie rollen hebben betrekking op alle brontypen:

* Eigenaar  
* Inzender  
* Lezer  

Eigenaars en medewerkers hebt volledige toegang toohello management ervaring, maar een medewerker kan niet geven toegang tooother gebruikers of groepen. Dingen krijgt u iets interessanter met de rol Lezer hello, zodat die waar we je besteed voldoende tijd is. Zie Hallo [toegangsbeheer op basis van rollen get-started artikel](role-based-access-control-configure.md) voor meer informatie over hoe toogrant toegang tot.

## <a name="app-service-workloads"></a>App service-werkbelastingen
### <a name="write-access-capabilities"></a>Toegang voor schrijven-mogelijkheden
Als u een gebruiker alleen-lezentoegang tooa één web-app toewijst, worden sommige functies zijn uitgeschakeld dat u niet verwacht. Hallo na beheermogelijkheden vereisen **schrijven** toegang tot tooa web-app (Inzender of eigenaar) en niet beschikbaar in een scenario met alleen-lezen.

* Opdrachten (zoals starten, stoppen, enz.)
* Wijzigen van de instellingen, zoals algemene configuratie, schaalinstellingen, back-upinstellingen en controle-instellingen
* Toegang tot publishing referenties en andere geheime informatie zoals het app-instellingen en verbindingsreeksen
* Streaminglogboeken
* Configuratie van diagnostische logboeken
* Console (opdrachtprompt)
* Actieve en recente implementaties (voor lokale git-continue implementatie)
* Geschatte besteden
* Webtests
* Virtueel netwerk (alleen zichtbaar tooa lezer als eerder een virtueel netwerk is geconfigureerd door een gebruiker met toegang voor schrijven).

Als u geen toegang deze tegels tot, moet u op tooask uw beheerder voor Inzender toegang toohello web-app.

### <a name="dealing-with-related-resources"></a>Omgaan met verwante bronnen
Web-apps zijn door Hallo aanwezigheid van een paar verschillende bronnen die wisselwerking ingewikkeld. Hier volgt een typisch resourcegroep met een paar websites:

![Web-app-resourcegroep](./media/role-based-access-control-troubleshooting/website-resource-model.png)

Als gevolg hiervan, als u iemand toegang toojust Hallo web-app verleent, dat veel Hallo-functionaliteit op de websiteblade Hallo in hello Azure-portal is uitgeschakeld.

Deze items vereisen **schrijven** toegang tot toohello **App Service-abonnement** die overeenkomt met tooyour website:  

* Weergave Hallo web-app de prijscategorie (vrije of standaard)  
* Configuratie van de schaal (aantal exemplaren, de grootte van virtuele machine, de instellingen voor automatisch schalen)  
* Quota (opslag, bandbreedte, CPU)  

Deze items vereisen **schrijven** toegang toohello hele **resourcegroep** die uw website bevat:  

* SSL-certificaten en bindingen (SSL-certificaten kunnen worden gedeeld tussen sites in Hallo dezelfde resourcegroep en de geografische locatie)  
* Regels voor waarschuwingen  
* instellingen voor automatisch schalen  
* Application insights-onderdelen  
* Webtests  

## <a name="virtual-machine-workloads"></a>Virtual machine-werkbelasting
Veel zoals met web-apps, sommige functies op Hallo virtuele machineblade vereisen schrijftoegang toohello virtuele machine of tooother resources in Hallo-resourcegroep.

Virtuele machines zijn verwante tooDomain namen, virtuele netwerken, opslagaccounts en regels voor waarschuwingen.

Deze items vereisen **schrijven** toegang tot toohello **virtuele machine**:

* Eindpunten  
* IP-adressen  
* Disks  
* Extensies  

Hiervoor is vereist **schrijven** toegang tooboth hello **virtuele machine**, en Hallo **resourcegroep** (samen met de domeinnaam Hallo) dat deze zich in:  

* Beschikbaarheidsset  
* Laden van de set met gelijke taakverdeling  
* Regels voor waarschuwingen  

Als u geen toegang deze tegels tot, vraag uw beheerder voor Inzender toegang toohello resourcegroep.

## <a name="see-more"></a>Meer informatie
* [Op rollen gebaseerd toegangsbeheer](role-based-access-control-configure.md): aan de slag met RBAC in hello Azure-portal.
* [Ingebouwde rollen](role-based-access-built-in-roles.md): meer informatie over het Hallo-functies die standaard in RBAC.
* [Aangepaste rollen in Azure RBAC](role-based-access-control-custom-roles.md): meer informatie over hoe toocreate aangepaste rollen toofit uw toegang moet.
* [Maken van een geschiedenisrapport voor gewijzigde van toegang](role-based-access-control-access-change-history-report.md): bijhouden van wijzigen van roltoewijzingen in RBAC.


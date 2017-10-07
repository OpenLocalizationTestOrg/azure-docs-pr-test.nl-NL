---
title: aaaProtecting uw toepassingen in Azure Security Center | Microsoft Docs
description: Dit document gaat in Azure Security Center aanbevelingen die u helpen bij uw Azure-toepassingen beveiligen en blijven in overeenstemming met het beveiligingsbeleid.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: b5fc7a9e-24b1-415f-b3b5-62a53f5dd424
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/01/2016
ms.author: terrylan
ms.openlocfilehash: da5e02cc2bad55c64e4da14e4e10efd6ddeab39e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="protecting-your-applications-in-azure-security-center"></a>Beveiligen van uw toepassingen in Azure Security Center
Azure Security Center analyseert de beveiligingsstatus Hallo van uw Azure-resources. Wanneer het Beveiligingscentrum identificeert mogelijke beveiligingsproblemen, maakt deze aanbevelingen die u helpt bij Hallo Hallo nodig-besturingselementen configureren.  Aanbevelingen tooAzure brontypen die van toepassing: virtuele machines (VM's), netwerken, SQL en toepassingen.

In dit artikel biedt de aanbevelingen die van toepassing zijn tooapplications.  Toepassing aanbevelingen center om de implementatie van web application firewall.  Gebruik Hallo onderstaande tabel als een verwijzing toohelp erkent u Hallo beschikbare toepassingsaanvragen aanbevelingen en elke eigenschap als u deze toe te passen.

## <a name="available-application-recommendations"></a>Beschikbare toepassingsaanvragen aanbevelingen
| Aanbeveling | Beschrijving |
| --- | --- |
| [Een firewall voor webtoepassingen toevoegen](security-center-add-web-application-firewall.md) |Raadt aan dat u een web application firewall (WAF) voor web-eindpunten implementeert. Een WAF aanbeveling wordt voor een openbare internetgerichte IP (exemplaar niveau IP- of Load Balanced IP) met een gekoppelde netwerkbeveiligingsgroep met poorten voor inkomend web openen (80,443) weergegeven.</br></br>Security Center raadt aan dat u een WAF toohelp inrichten bescherming tegen aanvallen die gericht is op uw webtoepassingen op virtuele machines en op App Service-omgeving. Een as-omgeving (App Service omgeving) is een [Premium](https://azure.microsoft.com/pricing/details/app-service/) service-plan optie van Azure App Service die een volledig geïsoleerde en toegewezen omgeving biedt voor het veilig uitvoeren van Azure App Service-apps. toolearn meer informatie over het as-omgeving, Zie Hallo [documentatie van App Service-omgeving](../app-service/app-service-app-service-environments-readme.md).</br></br>U kunt meerdere webtoepassingen in Security Center beveiligen door deze toepassingen tooyour bestaande WAF implementaties toe te voegen. |
| [Toepassingsbeveiliging voltooien](security-center-add-web-application-firewall.md#finalize-application-protection) |toocomplete hello configuratie van een WAF, verkeer moet omgeleide toohello WAF toestel. Na deze aanbeveling is Hallo benodigde installatiebestanden wijzigingen voltooid. |

## <a name="see-also"></a>Zie ook
toolearn meer informatie over de aanbevelingen die van toepassing zijn tooother Azure brontypen, Zie de volgende Hallo:

* [Beveiligen van uw virtuele machines in Azure Security Center](security-center-virtual-machine-recommendations.md)
* [Beveiligen van uw netwerk in Azure Security Center](security-center-network-recommendations.md)
* [Beveiligen van uw Azure SQL-service in Azure Security Center](security-center-sql-service-recommendations.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.

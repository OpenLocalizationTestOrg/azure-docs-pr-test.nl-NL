---
title: aaaIntegrate logboeken van de Azure-resources in uw SIEM-systemen | Microsoft Docs
description: Meer informatie over de integratie van Azure-logboekanalyse, de belangrijkste mogelijkheden en hoe het werkt.
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Inleiding tooMicrosoft Azure-logboekanalyse-integratie
Meer informatie over de integratie van Azure-logboekanalyse, de belangrijkste mogelijkheden en hoe het werkt.

## <a name="overview"></a>Overzicht

Azure-logboekanalyse-integratie is een gratis oplossing waarmee u toointegrate onbewerkte logboeken van uw Azure-resources in tooyour on-premises Security Information en Event Management SIEM ()-systemen.

Integratie van Azure-logboekanalyse verzamelt Windows-gebeurtenissen van Windows-Logboeken, [Azure activiteitenlogboeken](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Azure Security Center waarschuwingen](../security-center/security-center-intro.md), en [Azure diagnostische logboeken](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) van Azure-resources. Deze integratie helpt uw SIEM-oplossing een uniforme dashboard bieden voor alle activa, on-premises of in de cloud hello, zodat u samenvoegen kunt, correleren, analyseren en waarschuwen voor beveiligingsgebeurtenissen.

>[!NOTE]
Op dit moment zijn alleen ondersteund Hallo clouds commerciële Azure en Azure Government. Andere clouds worden niet ondersteund.

![Azure-logboekintegratie][1]

## <a name="what-logs-can-i-integrate"></a>Welke logboeken kan ik worden geïntegreerd?
Azure produceert uitgebreide logboekregistratie in voor elke Azure-service. Deze logboeken vertegenwoordigen drie verschillende typen logboeken:

* **Besturingselement/management-logboeken** bieden inzicht in Hallo [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) maken, bijwerken en DELETE-bewerkingen. Azure activiteitenlogboeken is een voorbeeld van dit type van het logboek.
* **Gegevens vlak logboeken** bieden inzicht in deze gebeurtenis treedt op als onderdeel van het gebruik van een Azure-resource Hallo Hallo-gebeurtenissen. Een voorbeeld van dit type van het logboek is Hallo Windows logboeken van **System**, **beveiliging**, en **toepassing** kanalen in een virtuele Windows-computer. Een ander voorbeeld is Diagnostics Logging geconfigureerd via de Azure-Monitor
* **Verwerkte gebeurtenissen** bieden geanalyseerde gebeurtenis- en waarschuwingsgegevens namens jou worden verwerkt. Een voorbeeld van dit type gebeurtenis is Azure Security Center Alerts, waarin het Azure Beveiligingscentrum heeft verwerkt en uw abonnement tooprovide waarschuwingen relevante tooyour huidige beveiligingspostuur geanalyseerd.

Integratie van Azure Log ondersteunt ArcSight, QRadar en Splunk. In alle gevallen Neem contact op met uw SIEM leverancier tooassess of ze een eigen connector hebben. In sommige gevallen moet u niet toouse Azure Log integratie wanneer systeemeigen connectors beschikbaar zijn. Voor meer informatie over ondersteunde logboek typen gaat u naar Hallo Veelgestelde vragen over.

>[!NOTE]
Azure Log-integratie is een gratis oplossing, maar er zijn Azure opslagkosten die voortvloeien uit Hallo logboek-bestandsopslag voor informatie.

Hulp is beschikbaar via Hallo [Azure Log integratie MSDN-Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Hallo-forum biedt Hallo AzLog community Hallo mogelijkheid toosupport elkaar vragen, antwoorden, tips en trucs over hoe tooget meest Hallo buiten Azure Log-integratie. Bovendien hello Azure Log integratie-team dit forum wordt bewaakt en wanneer we kunt.

U kunt ook openen een [ondersteuningsaanvraag](../azure-supportability/how-to-create-azure-support-request.md). toodo deze, selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.

## <a name="next-steps"></a>Volgende stappen
In dit document, kunt u geïntroduceerd tooAzure logboek integratie was. meer informatie over Azure-integratie en Hallo verschillende typen logboeken die worden ondersteund, meld toolearn Hallo ziet:

* [Microsoft Azure Log integratie](https://www.microsoft.com/download/details.aspx?id=53324) : Download Center voor meer informatie over de systeemvereisten en instructies op Azure-logboekanalyse-integratie installeren.
* [Aan de slag met Azure-logboekanalyse integratie](security-azure-log-integration-get-started.md) - in deze zelfstudie doorloopt u de installatie van de integratie van Azure-logboekanalyse en logboeken vanuit Azure af opslag, Azure activiteitenlogboeken, integratie van Azure Security Center-waarschuwingen en Azure Active Directory controlelogboeken.
* [Partner configuratiestappen](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – dit blogbericht leest u hoe tooconfigure Azure integratie toowork Meld met partneroplossingen Splunk, HP ArcSight en IBM QRadar. Deze blog vertegenwoordigt onze huidige positie voor het configureren van de partneroplossingen Hallo. In alle gevallen Raadpleeg de documentatie van de oplossing toopartner eerst.
* [Activiteit en ASC waarschuwingen via syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – dit blogbericht bevat stappen die Hallo toosend activiteit en Azure Security Center waarschuwingen via syslog tooQRadar
* [Azure-logboekanalyse integratie Veelgestelde vragen (FAQ)](security-azure-log-integration-faq.md) -deze Veelgestelde vragen over de antwoorden op vragen over Azure-logboekanalyse-integratie.
* [Waarschuwingen met Azure Security Center integreren Meld integratie](../security-center/security-center-integrating-alerts-with-log-integration.md) : dit document leest u hoe toosync Azure Security Center waarschuwingen met Azure Log-integratie.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png

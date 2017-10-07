---
title: Meld u integratie aaaIntegrating Azure Security Center waarschuwingen met Azure | Microsoft Docs
description: In dit artikel helpt u aan de slag met Security Center waarschuwingen integreren met Azure-logboekanalyse-integratie.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: d2d088d3-d38d-47ff-a062-c78e0fd59226
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: terrylan
ms.openlocfilehash: 2649036ee990bf0f48fa0cb35c7495ac932c29ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-azure-security-center-alerts-with-azure-log-integration"></a>Waarschuwingen van Azure Security Center integreren met Azure-logboekanalyse-integratie
Veel beveiligingsbewerkingen en respons op incidenten teams afhankelijk van een oplossing Security Information en Event Management (SIEM) als Hallo startpunt voor gesorteerd en beveiligingswaarschuwingen onderzoeken. U kunt waarschuwingen van Azure Security Center met uw SIEM-oplossing integreren met Azure Log-integratie.

Azure-logboekanalyse-integratie ondersteunt momenteel HP ArcSight Splunk en IBM QRadar.

## <a name="what-logs-can-i-integrate"></a>Welke logboeken kan ik worden geïntegreerd?
Azure produceert uitgebreide logboekregistratie in voor elke service. Deze logboeken zijn aangemerkt als:

* **Besturingselement/Management-logboeken** die geven inzicht in hello Azure Resource Manager maken, bijwerken en DELETE-bewerkingen. Deze controlevlak-gebeurtenissen worden in hello Azure activiteitenlogboeken opgehaald
* **Gegevenslogboeken vlak** die geven inzicht in Hallo gebeurtenissen treedt op wanneer met behulp van een Azure-resource. Een voorbeeld is Hallo Windows-gebeurtenislogboek, waar u de gebeurtenis beveiligingsgegevens van beveiligingskanaal Hallo Event Viewer kunt krijgen. Data vlak-gebeurtenissen (die worden gegenereerd door een virtuele machine of een Azure-service) worden opgehaald door Azure diagnostische logboeken.

Azure-logboekanalyse-integratie ondersteunt momenteel Hallo integratie van:

* Azure VM-Logboeken
* Azure controlelogboeken
* Azure Security Center-waarschuwingen

## <a name="install-azure-log-integration"></a>Azure-logboekanalyse-integratie installeren
Download [integratie van Azure-logboekanalyse](https://www.microsoft.com/download/details.aspx?id=53324).

Hello Azure-logboekanalyse integration-service verzamelt telemetriegegevens van Hallo-machine waarop deze is geïnstalleerd.  Verzamelde telemetriegegevens is:

* Uitzonderingen die tijdens het uitvoeren van de integratie van Azure-logboekanalyse optreden
* Metrische gegevens over Hallo aantal query's en gebeurtenissen die zijn verwerkt
* Statistieken over welke Azlog.exe opdrachtregelopties worden gebruikt

> [!NOTE]
> U kunt verzamelen van telemetriegegevens uitschakelen door deze optie uitschakelt.
>
>

## <a name="integrate-azure-audit-logs-and-security-center-alerts"></a>Integratie van Azure controlelogboeken en Security Center-waarschuwingen
1. Opdrachtprompt openen Hallo en **cd** in **c:\Program Files\Microsoft Azure Log integratie**.
2. Voer Hallo **azlog createazureid** opdracht toocreate een [Azure Active Directory Service-Principal](../active-directory/active-directory-application-objects.md) in Azure Active Directory (AD) Hallo Hallo tenants die als host fungeren Azure-abonnementen.

    U wordt gevraagd naar uw Azure-aanmelding.

   > [!NOTE]
   > U moet Hallo abonnement eigenaar of Medebeheerder van het Hallo-abonnement.
   >
   >

    TooAzure verificatie wordt gedaan door Azure AD.  Maken van een service-principal voor Azure-logboekanalyse integratie maakt hello Azure AD identity die toegang tooread van Azure-abonnementen krijgt.
3. Voer Hallo **azlog autoriseren <SubscriptionID>**  opdracht tooassign lezerstoegang op Hallo abonnement toohello service-principal gemaakt in stap 2. Als u geen opgeeft een **SubscriptionID**, dan Hallo service-principal is toegewezen Hallo lezer rol tooall abonnementen toowhich hebt u toegang hebt.

   > [!NOTE]
   > Mogelijk ziet u waarschuwingen als u Hallo uitvoeren **autoriseren** opdracht onmiddellijk na Hallo **createazureid** opdracht. Er is enige vertraging worden bijgewerkt tussen wanneer hello Azure AD-account wordt gemaakt en wanneer Hallo-account is beschikbaar voor gebruik. Als u ongeveer tien seconden wacht na het uitvoeren van Hallo **createazureid** opdracht toorun hello **autoriseren** uitvoert, en u moet deze waarschuwingen niet zien.
   >
   >
4. Controleer zijn er Hallo mappen tooconfirm die Hallo Audit log JSON-bestanden te volgen:

   * **c:\Users\azlog\AzureResourceManagerJson**
   * **c:\Users\azlog\AzureResourceManagerJsonLD**
5. Hallo mappen tooconfirm die Security Center waarschuwingen aanwezig zijn in deze volgende controleren:

   * **c:\Users\azlog\ AzureSecurityCenterJson**
   * **c:\Users\azlog\AzureSecurityCenterJsonLD**
6. Hallo SIEM doorstuurserver connector toohello juiste bestandsmap configureren. Hallo procedure variëren, afhankelijk van Hallo SIEM die u gebruikt.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Azure activiteitenlogboeken en eigenschapdefinities, Zie:

* [Bewerkingen controleren met Resource Manager](../azure-resource-manager/resource-group-audit.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) : meer informatie hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) : Hallo nieuwste Azure-beveiliging nieuws en informatie.

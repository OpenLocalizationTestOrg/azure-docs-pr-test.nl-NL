---
title: aaaAzure logboek integratie met security center | Microsoft Docs
description: Meer informatie over hoe tooget Azure Security center-waarschuwingen die werken met logboek-integratie
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 03/22/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: bcc208d071ec03738215f2aee3b71c7b10927904
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-your-security-center-alerts-in-azure-log-integration"></a>Hoe tooget uw Security Center waarschuwingen in Azure-logboekanalyse-integratie
Dit artikel bevat Hallo stappen vereist tooenable hello Azure Log integratie service toopull beveiligingswaarschuwing informatie die wordt gegenereerd door Azure Security Center. U moet hebt voltooid Hallo stappen in Hallo [aan de slag](security-azure-log-integration-get-started.md) artikel voordat u Hallo stappen in dit artikel uitvoert.

## <a name="detailed-steps"></a>Gedetailleerde stappen
Hallo volgende stappen maakt Hallo vereist Azure Active Directory Service-Principal en toewijzen Hallo Service Principle leesmachtigingen toohello abonnement:
1. Hallo-opdrachtprompt openen en te navigeren**c:\Program Files\Microsoft Azure Log-integratie**
2. Hallo-opdracht uitvoeren``azlog createazureid``

    Met deze opdracht wordt u gevraagd om uw Azure-aanmelding. Hallo opdracht maakt u vervolgens een [Azure Active Directory Service-Principal](../active-directory/develop/active-directory-application-objects.md) in hello Azure AD-Tenants die als host fungeren hello Azure-abonnementen een beheerder, CO-beheerder of een eigenaar in welke Hallo aangemelde gebruiker is. Hallo-opdracht mislukt als Hallo aangemelde gebruiker een gastgebruiker in hello Azure AD-Tenant. TooAzure verificatie wordt gedaan via Azure Active Directory (AD). Maken van een service-principal voor Azlog integratie maakt hello Azure AD identity die toegang tooread wordt gegeven van de Azure-abonnementen.

2. Vervolgens voert u een opdracht die wordt toegewezen lezerstoegang op Hallo abonnement toohello service-principal gemaakt in stap 2. Als u niet een abonnements-id opgeeft, wordt Hallo opdracht tooassign Hallo service principal lezer rol tooall abonnementen toowhich u toegang hebben geprobeerd. </br></br>
``azlog authorize <SubscriptionID>`` </br> bijvoorbeeld </br>
``azlog authorize 0ee55555-0bc4-4a32-a4e8-c29980000000``

    >[!NOTE]
    Mogelijk ziet u waarschuwingen als u Hallo uitvoeren opdracht onmiddellijk na Hallo createazureid opdracht autoriseren. Er is enige vertraging worden bijgewerkt tussen wanneer hello Azure AD-account wordt gemaakt en wanneer Hallo-account is beschikbaar voor gebruik. Als u over wacht 60 seconden na het uitvoeren van Hallo createazureid opdracht toorun Hallo opdracht toestaan en klik vervolgens niet ziet u deze waarschuwingen.

4. Controleer zijn er Hallo mappen tooconfirm die Hallo Audit log JSON-bestanden te volgen:
 * **c:\Users\azlog\AzureResourceManagerJson**
 * **c:\Users\azlog\AzureResourceManagerJsonLD** </br></br>
5. Hallo mappen tooconfirm die Security Center waarschuwingen aanwezig zijn in deze volgende controleren:</br></br>
 * **c:\Users\azlog\AzureSecurityCenterJson**
 * **c:\Users\azlog\AzureSecurityCenterJsonLD** </br></br>

Als u problemen ondervindt tijdens het Hallo-installatie en configuratie, opent u een [ondersteuningsaanvraag](/azure-supportability/how-to-create-azure-support-request.md), selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over de integratie van Azure Log, Zie Hallo documenten te volgen:

* [Microsoft Azure Log-integratie voor Azure logboeken](https://www.microsoft.com/download/details.aspx?id=53324) : Download Center voor meer informatie over de systeemvereisten en instructies op Azure-logboekanalyse-integratie installeren.
* [Inleiding tooAzure logboek integratie](security-azure-log-integration-overview.md) : dit document vindt u tooAzure logboek integratie, de belangrijkste mogelijkheden en hoe het werkt.
* [Partner configuratiestappen](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – dit blogbericht leest u hoe tooconfigure Azure integratie toowork Meld met partneroplossingen Splunk, HP ArcSight en IBM QRadar.
* [Azure-logboekanalyse integratie Veelgestelde vragen (FAQ)](security-azure-log-integration-faq.md) -deze Veelgestelde vragen over de antwoorden op vragen over Azure-logboekanalyse-integratie.
* [Waarschuwingen met Azure Security Center integreren Meld integratie](../security-center/security-center-integrating-alerts-with-log-integration.md) : dit document leest u hoe toosync Security Center waarschuwingen, samen met de virtuele machine beveiligingsgebeurtenissen die zijn verzameld door Azure Diagnostics- en Azure controlelogboeken met uw logboekanalyse of SIEM-oplossing.
* [Nieuwe functies voor Azure diagnoses en Azure controlelogboeken](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/) : vindt u in dit blogbericht tooAzure controlelogboeken en andere functies waarmee u inzicht in Hallo bewerkingen van uw Azure-resources.

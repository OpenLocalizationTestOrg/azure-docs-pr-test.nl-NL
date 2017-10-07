---
title: aaaAzure logboek integratie met Azure Active Directory-controlelogboeken | Microsoft Docs
description: Meer informatie over hoe tooinstall hello Azure Log Integration-service en de logboeken van Azure controlelogboeken integreren
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
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a>Integratie van Azure Active Directory-auditlogboeken

Controlegebeurtenissen van Azure Active Directory (Azure AD) kunnen u bepalen bevoorrechte acties die is opgetreden in Azure Active Directory. U kunt zien Hallo typen gebeurtenissen die u bijhouden aan de hand van kunt [Azure Active Directory-controlerapportgebeurtenissen](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).

> [!NOTE]
> Voordat u de stappen in dit artikel hello, moet u Hallo doornemen [aan de slag](security-azure-log-integration-get-started.md) en voltooi er Hallo stappen.

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a>Controlelogboeken stappen toointegrate Azure Active directory

1. Open Hallo-opdrachtprompt en voer deze opdracht uit:

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. Voer deze opdracht uit: 
 
   ``azlog createazureid``

   Met deze opdracht wordt u gevraagd om uw Azure-aanmelding. Hallo opdracht maakt u een Azure Active Directory service-principal in hello Azure AD-tenants die als host fungeren hello Azure-abonnementen in welke Hallo aangemelde gebruiker een beheerder, CO-beheerder of een eigenaar is. Hallo-opdracht mislukt als Hallo aangemelde gebruiker een gastgebruiker in hello Azure AD-tenant. TooAzure verificatie wordt gedaan door Azure AD. Maken van een service-principal voor Azure Log integratie maakt hello Azure AD identity die toegang tooread van Azure-abonnementen krijgt.

3. Voer Hallo opdracht tooprovide na uw tenant-ID. U moet lid van Hallo tenant admin rol toorun Hallo opdracht toobe.

   ``Azlog.exe authorizedirectoryreader tenantId``

   Voorbeeld:

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. Controleer Hallo na mappen tooconfirm die hello Azure Active Directory-audit log JSON-bestanden in deze zijn gemaakt:

   * **C:\Users\azlog\AzureActiveDirectoryJson**
   * **C:\Users\azlog\AzureActiveDirectoryJsonLD**

Hallo toont volgende video Hallo stappen die in dit artikel:

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> Neem contact op met de leverancier van uw SIEM voor specifieke instructies voor het Hallo-informatie te brengen in Hallo JSON-bestanden in uw security information en event management (SIEM)-systeem.

Hulp is beschikbaar via Hallo [Azure Log integratie MSDN-Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Dit forum kunt mensen in hello Azure Log integratie community toosupport elkaar met vragen, antwoorden, tips en slagen. Bovendien hello Azure Log integratie team dit forum wordt bewaakt en helpt wanneer dat mogelijk is.

U kunt ook openen een [ondersteuningsaanvraag](../azure-supportability/how-to-create-azure-support-request.md). Selecteer **logboek integratie** als Hallo service waarvoor u ondersteuning aanvraagt.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over de integratie van Azure Log, Zie:

* [Microsoft Azure Log-integratie voor Azure logboeken](https://www.microsoft.com/download/details.aspx?id=53324): deze Download Center-pagina geeft details, systeemvereisten en installatie-instructies voor de integratie van Azure-logboek.
* [Inleiding tooAzure logboek integratie](security-azure-log-integration-overview.md): in dit artikel vindt u tooAzure logboek integratie, de belangrijkste mogelijkheden en hoe het werkt.
* [Partner configuratiestappen](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): dit blogbericht leest u hoe tooconfigure Azure Log integratie toowork met partneroplossingen Splunk, HP ArcSight en IBM QRadar.
* [Veelgestelde vragen over de Azure Log integratie](security-azure-log-integration-faq.md): in dit artikel antwoorden op vragen over Azure Log-integratie.
* [Security Center waarschuwingen integreren met Azure Log integratie](../security-center/security-center-integrating-alerts-with-log-integration.md): dit artikel laat zien hoe toosync Security Center waarschuwingen, samen met de virtuele machine beveiligingsgebeurtenissen die is verzameld door Azure diagnoses en Azure controlelogboeken met uw logboekanalyse of SIEM-oplossing.
* [Nieuwe functies voor Azure Diagnostics- en Azure controlelogboeken](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): vindt u in dit blogbericht tooAzure controlelogboeken en andere functies waarmee u inzicht in Hallo bewerkingen van uw Azure-resources.

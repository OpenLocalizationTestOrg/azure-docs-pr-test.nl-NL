---
title: aaaAzure service Security Center en Azure SQL Database | Microsoft Docs
description: Dit artikel laat zien hoe Security Center kan u helpen uw database in Azure SQL Database beveiligen.
services: sql-database
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: f109adfd-daed-4257-9692-2042a1399480
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: 173590500f0ce64140f214ada24b9692e01dbd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-and-azure-sql-database-service"></a>Azure Security Center en Azure SQL Database-service
[Azure Security Center](https://azure.microsoft.com/documentation/services/security-center/) helpt u bij het detecteren, voorkomen van en reageren toothreats. Het biedt geïntegreerde beveiligingsbewaking en beleidsbeheer voor uw Azure-abonnementen, helpt bedreigingen te detecteren die anders onopgemerkt zouden blijven, en werkt met een uitgebreid ecosysteem van beveiligingsoplossingen.

Dit artikel laat zien hoe Security Center kan u helpen uw database in Azure SQL Database beveiligen.

## <a name="why-use-security-center"></a>Waarom Security Center gebruiken?
Security Center helpt u gegevens in SQL-Database beveiligt door te geven inzicht in Hallo beveiliging van uw servers en databases. U kunt met Security Center:

* Beleid voor versleuteling van de SQL-Database en controle definiëren.
* Hallo beveiliging van SQL Database-resources bewaken voor al uw abonnementen.
* Snel identificeren en te verhelpen beveiligingsproblemen.
* Waarschuwingen van integreren [Azure SQL Database met detectie van dreigingen](../sql-database/sql-database-threat-detection.md).

Bovendien toohelping de bronnen van uw SQL-Database beveiligen, Security Center biedt ook beveiligingsbewaking en beheer voor virtuele machines in Azure, Cloud Services, App-Services, virtuele netwerken en meer. Meer informatie over Security Center [hier](security-center-intro.md).

## <a name="prerequisites"></a>Vereisten
tooget gestart met Security Center, moet u een abonnement tooMicrosoft Azure hebben. Hallo gratis laag van het Beveiligingscentrum is met uw abonnement ingeschakeld. Zie voor meer informatie over de vrije en de standaard lagen van Security Center [Security Center prijzen](https://azure.microsoft.com/pricing/details/security-center/).

Security Center biedt ondersteuning voor toegang op basis van rollen. toolearn meer informatie over op rollen gebaseerde toegangsbeheer (RBAC) in Azure, Zie [toegangsbeheer op basis van een functie van Azure Active Directory](../active-directory/role-based-access-control-configure.md). Hallo Security Center FAQ biedt informatie over [hoe machtigingen worden verwerkt in Security Center](security-center-faq.md#permissions).

## <a name="access-security-center"></a>Security Center openen
Security Center is toegankelijk vanuit Hallo [Azure-portal](https://azure.microsoft.com/features/azure-portal/). [Meld u aan de portal toohello](https://portal.azure.com/) en selecteer Hallo **Security Center-optie**.

![Security Center-optie][1]

Hallo **Security Center** blade wordt geopend.
![Blade Security Center][2]

## <a name="set-security-policy"></a>Beveiligingsbeleid instellen
Een beveiligingsbeleid bepaalt Hallo set besturingselementen die worden aanbevolen voor resources binnen de opgegeven abonnement of resourcegroep groep Hallo. In Security Center definieert u beleid voor uw abonnementen of de resourcegroepen op basis van tooyour en van het bedrijf beveiligingsbehoeften Hallo type toepassingen of de vertrouwelijkheid van gegevens in elk abonnement Hallo.

Aanbevelingen voor SQL-controle en transparent data encryption voor SQL (TDE), kunt u een beleid tooshow instellen.

* Wanneer u inschakelt **SQL controle en detectie van bedreigingen**, Security Center raadt aan dat de controle van toegang tooAzure Database wordt ingeschakeld voor naleving, geavanceerde detectie en onderzoek doeleinden.
* Wanneer u inschakelt **transparent data encryption voor SQL**, Security Center raadt aan dat versleuteling in rust zijn ingeschakeld voor uw Azure SQL Database, gekoppelde back-ups en transactielogboekbestanden.

tooset een beveiligingsbeleid Selecteer Hallo **beleid** tegel op de blade Security Center Hallo. Op Hallo **beveiligingsbeleid** blade, selecteer Hallo abonnement waarop tooenable Hallo beveiligingsbeleid. Selecteer **preventiebeleid** en schakel **op** Hallo beveiligingsaanbevelingen voor de gewenste toouse voor dit abonnement.
![Beveiligingsbeleid][3]

toolearn meer, Zie [instellen van beveiligingsbeleid](security-center-policies.md).

## <a name="manage-security-recommendation"></a>Beveiligingsaanbeveling beheren
Security Center analyseert periodiek Hallo beveiligingsstatus van uw Azure-resources. Wanneer met Security Center potentiële beveiligingsproblemen worden geïdentificeerd, worden er aanbevelingen gedaan. Hallo aanbevelingen helpt u bij Hallo Hallo nodig-besturingselementen configureren.

Nadat u een beveiligingsbeleid instellen, analyseert Security Center Hallo beveiligingsstatus van uw resources tooidentify potentiële beveiligingslekken naar voren. Hallo aanbevelingen worden weergegeven in een tabel waarin elke regel staat voor een bepaalde aanbeveling. Gebruik Hallo volgende tabel als een verwijzing toohelp dat u Hallo beschikbaar aanbevelingen voor Azure SQL Database en welke elke aanbeveling heeft begrijpt als u deze toe te passen. Een aanbeveling te selecteren, gaat u tooan artikel waarin wordt uitgelegd hoe tooimplement Hallo aanbeveling in Security Center.

| Aanbeveling | Beschrijving |
| --- | --- |
| [Inschakelen van controle en detectie van bedreigingen op SQL-servers](security-center-enable-auditing-on-sql-servers.md) |Raadt aan dat u de controle en detectie van bedreigingen voor SQL Database-servers inschakelen. (Alleen voor SQL Database-service. Bevat geen Microsoft SQL Server op uw virtuele machines.) |
| [Inschakelen van controle en detectie van bedreigingen op SQL-databases](security-center-enable-auditing-on-sql-databases.md) |Raadt aan dat u de controle en detectie van bedreigingen voor databases in SQL-Database inschakelen. (Alleen voor SQL Database-service. Bevat geen Microsoft SQL Server op uw virtuele machines.) |
| [Transparante gegevensversleuteling inschakelen](security-center-enable-transparent-data-encryption.md) |Raadt aan om versleuteling voor SQL-databases in te schakelen. (Alleen SQL-Database-service). |

aanbevelingen voor uw Azure-resources, selecteer Hallo toosee **aanbevelingen** tegel op de blade Security Center Hallo. Op Hallo **aanbevelingen** blade, selecteert u de details van een aanbeveling toosee. In dit voorbeeld gaan we selecteren **controle inschakelen en detectie van bedreigingen op SQL-servers**.

![Aanbevelingen][4]

Zoals weergegeven onder Security Center bevat Hallo van SQL-servers waarop de controle en detectie van bedreigingen niet zijn ingeschakeld. Nadat u controle, kunt u de detectie van dreigingen instellingen configureren en e-instellingen tooreceive beveiligingswaarschuwingen. Detectie van dreigingen waarschuwt u wanneer deze worden afwijkende databaseactiviteiten die wijzen op mogelijke bedreigingen toohello database met gedetecteerd. Hallo waarschuwingen worden weergegeven in Hallo Security Center-dashboard.
![Controle en detectie van bedreigingen][5]

Hallo stappen in [SQL-Database de detectie van dreigingen in hello Azure-portal](../sql-database/sql-database-threat-detection-portal.md) tooturn op en configureren van detectie van dreigingen en tooconfigure Hallo lijst met e-mailberichten die beveiligingswaarschuwingen bij vreemde activiteiten worden ontvangen.

toolearn meer informatie over aanbevelingen, Zie [aanbevelingen voor beveiliging beheren](security-center-recommendations.md).

## <a name="monitor-security-health"></a>Beveiligingsstatus controleren
Nadat u hebt ingeschakeld [beveiligingsbeleid](security-center-policies.md) voor resources van een abonnement, analyseert Security Center Hallo beveiliging van uw resources tooidentify potentiële beveiligingslekken naar voren.  U kunt Hallo beveiligingsstatus van uw resources weergeven in Hallo **resourcebeveiligingsstatus** tegel. Wanneer u klikt op **gegevens** in Hallo **resourcebeveiligingsstatus** tegel, hello **gegevensbronnen** er wordt een blade geopend met aanbevelingen voor problemen zoals controle en transparent SQL versleuteling van gegevens is niet ingeschakeld. Het bevat ook aanbevelingen voor de algemene status Hallo van Hallo-database.
![Beveiligingsstatus van de resource][6]

toolearn meer, Zie [Security health monitoring](security-center-monitoring.md).

## <a name="manage-and-respond-toosecurity-alerts"></a>Beheren en hierop reageren toosecurity waarschuwingen
Security Center automatisch verzamelt, analyseert en integreert logboekgegevens van [Azure SQL-Bedreigingsdetectie](../sql-database/sql-database-threat-detection.md), als goed als andere Azure-resources, toodetect Werkelijke dreigingen en fout-positieven te reduceren. Een lijst met beveiligingswaarschuwingen in Security Center wordt weergegeven, samen met de Hallo informatie die u nodig tooquickly onderzoeken Hallo probleem en aanbevelingen voor hoe tooremediate een aanval.

toosee waarschuwingen, selecteer Hallo **beveiligingswaarschuwingen** tegel op de blade Security Center Hallo. Op Hallo **beveiligingswaarschuwingen** blade, selecteer een waarschuwing toolearn meer informatie over het Hallo-gebeurtenissen die Hallo waarschuwing en welke geactiveerd als de toepassing, stappen u moet tootake tooremediate een aanval. In dit voorbeeld gaan we selecteren **potentiële SQL-injectie**.
![Beveiligingswaarschuwingen][7]

Zoals hieronder wordt weergegeven, Security Center biedt aanvullende informatie inzicht in wat waarschuwing geactiveerd Hallo Hallo biedt doelresource, wanneer van toepassing hello bron-IP-adres en aanbevelingen over het tooremediate.
![Mogelijke SQL-injectie][8]

toolearn meer, Zie [waarschuwingen voor het beheer van is en reageert toosecurity](security-center-managing-and-responding-alerts.md).

## <a name="next-steps"></a>Volgende stappen
* [Security Center FAQ](security-center-faq.md) : Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Security Center plannen en de operations guide](security-center-planning-and-operations-guide.md) : een reeks stappen en taken toooptimize uw gebruik van het Beveiligingscentrum op basis van de beveiligingsvereisten en het cloudbeheermodel van uw organisatie.
* [Security Center-gegevensbeveiliging](security-center-data-security.md) : meer informatie over hoe Security Center verzamelt en gegevens over uw Azure-resources, met inbegrip van configuratie-informatie, metagegevens, gebeurtenislogboeken, crashdumpbestanden en meer verwerkt.
* [Afhandeling van beveiligingsincidenten](security-center-incident.md) -informatie over hoe toouse Hallo beveiliging mogelijkheden in Security Center tooassist waarschuwen u in het afhandelen van beveiligingsincidenten.

<!--Image references-->
[1]: ./media/security-center-sql-database/security-center.png
[2]: ./media/security-center-sql-database/security-center-blade.png
[3]: ./media/security-center-sql-database/security-policy.png
[4]: ./media/security-center-sql-database/recommendation.png
[5]: ./media/security-center-sql-database/turn-on-auditing.png
[6]: ./media/security-center-sql-database/monitor-health.png
[7]: ./media/security-center-sql-database/alert.png
[8]: ./media/security-center-sql-database/sql-injection.png

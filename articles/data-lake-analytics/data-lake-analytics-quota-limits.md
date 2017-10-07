---
title: aaaAzure quotalimieten voor Data Lake Analytics | Microsoft Docs
description: Meer informatie over hoe tooadjust en verhoging van het quotum beperkt in Azure Data Lake Analytics (ADLA)-accounts.
services: data-lake-analytics
keywords: Azure Data Lake Analytics
documentationcenter: 
author: omidm1
editor: omidm1
ms.assetid: 49416f38-fcc7-476f-a55e-d67f3f9c1d34
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: omidm
ms.openlocfilehash: 875c4d00e0c57414031e50754495c02162bdca48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-lake-analytics-quota-limits"></a>De quotalimieten voor Azure Data Lake Analytics

Meer informatie over hoe tooadjust en verhoging van het quotum beperkt in Azure Data Lake Analytics (ADLA)-accounts. Deze limieten weten, kunt u meer inzicht in uw U-SQL-taak gedrag. Alle quotalimieten zijn zachte, zodat u maximaal Hallo-limieten verhogen kunt door toous bereikt.

## <a name="azure-subscriptions-limits"></a>Limieten voor Azure-abonnementen

**Maximum aantal ADLA accounts per abonnement:** 5

 Dit is Hallo kunt u het maximum aantal ADLA accounts die u per abonnement maken kunt. Als u een zesde toocreate ADLA account probeert, krijgt u een foutbericht 'U bereikt Hallo kunt u het maximum aantal Data Lake Analytics-accounts toegestaan (5) in regio onder de abonnementsnaam van het '. In dit geval Verwijder ongebruikte ADLA accounts of bereiken door toous [een ondersteuningsticket openen](#increase-maximum-quota-limits).

## <a name="adla-account-limits"></a>Limieten van ADLA

**Maximum aantal eenheden Analytics (AUs) per account:** 250

Dit is Hallo kunt u het maximum aantal AUs die tegelijkertijd kunnen worden uitgevoerd in uw account. Als de totale AUs uitvoeren voor alle taken deze limiet overschrijdt, nieuwere taken in de wachtrij automatisch. Bijvoorbeeld:

* Als u slechts één taak hebt uitgevoerd met 250 AUs, wanneer u een tweede indient taak deze in de taakwachtrij Hallo wacht totdat de eerste taak Hallo is voltooid.
* Als u hebt al vijf taken worden uitgevoerd en elk van 50 gebruikmaakt AUs, wanneer u een zesde taak die 20 moet stuurt deze in de taakwachtrij Hallo wacht totdat er 20 AUs AUs beschikbaar.

**Maximum aantal gelijktijdige U-SQL-taken per account:** 20

Dit is Hallo kunt u het maximum aantal taken dat gelijktijdig kan worden uitgevoerd in uw account. Boven deze waarde nieuwere taken in de wachtrij automatisch.

## <a name="adjust-adla-quota-limits-per-account"></a>De quotalimieten ADLA per account aanpassen

1. Meld u aan bij toohello [Azure-portal](https://portal.azure.com).
2. Kies een bestaand ADLA-account.
3. Klik op **Eigenschappen**.
4. Aanpassen **parallelle uitvoering** en **gelijktijdige taken** toosuit uw behoeften.

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-properties.png)

## <a name="increase-maximum-quota-limits"></a>Maximumquotum limieten verhogen

1. Open een ondersteuningsaanvraag in Azure-Portal.

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-help-support.png)

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request.png)
2. Selecteer Hallo probleem type **quotum**.
3. Selecteer uw **abonnement** (Zorg ervoor dat het is niet een ' ' proefabonnement).
4. Selecteer quotatype **Data Lake Analytics**.

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-basics.png)

5. Hallo probleem blade uitgelegd uw limiet aangevraagde verhoging met **Details** van waarom u deze extra capaciteit nodig hebt.

    ![Azure Data Lake Analytics-portalblade](./media/data-lake-analytics-quota-limits/data-lake-analytics-quota-support-request-details.png)

6. Uw contactgegevens controleren en u Hallo ondersteuningsaanvraag wilt indienen.

Microsoft uw aanvraag beoordeelt en probeert tooaccommodate zo snel mogelijk de behoeften van uw bedrijf.

## <a name="next-steps"></a>Volgende stappen

* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Azure Data Lake Analytics beheren met Azure PowerShell](data-lake-analytics-manage-use-powershell.md)
* [Azure Data Lake Analytics-taken bewaken en problemen oplossen met Azure Portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

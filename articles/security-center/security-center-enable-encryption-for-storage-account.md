---
title: aaaEnable versleuteling voor storage-account in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbevelingen ** versleuteling voor Azure Storage Account ** inschakelen.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>Schakel versleuteling voor Azure storage-account in Azure Security Center
Azure Security Center kunt u het beste inschakelen Azure Storage-Service: versleuteling voor gegevens in rust.

Versleuteling voor opslag-Service (SSE) werkt door Hallo gegevens te coderen wanneer deze wordt tooAzure opslag geschreven en ontsleutelen van gegevens Hallo voordat ophalen.  SSE is momenteel alleen beschikbaar voor hello Azure Blob-service en kan worden gebruikt voor blok-blobs, pagina-blobs en toevoeg-blobs.  toolearn meer, Zie [Service versleuteling van opslag voor gegevens in rust](../storage/common/storage-service-encryption.md).


> [!Note]
> Nadat de codering is ingeschakeld, worden alleen nieuwe gegevens worden versleuteld. Alle bestaande blobs in uw opslagaccount blijven onversleuteld. tooencrypt bestaande blobs, Zie Hallo [opslag Service versleuteling Veelgestelde vragen over](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).
>
>

Versleuteling van de opslagruimte wordt alleen ondersteund op Resource Manager storage-accounts. Klassieke opslagaccounts worden momenteel niet ondersteund. Zie toounderstand Hallo klassieke en het Resource Manager-implementatiemodel, [Azure-implementatiemodellen](../azure-classic-rm.md).

> [!NOTE]
> Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.  Dit document is niet een stapsgewijze handleiding.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **Schakel versleuteling voor Azure Storage-Account**.
   ![Versleuteling inschakelen voor opslagaccount][1]
2. Hallo **inschakelen van versleuteling van opslag** blade wordt geopend. Deze blade bevat hello Azure storage-accounts waar versleuteling van opslag is uitgeschakeld. In dit voorbeeld gaan we selecteren **storageacct1**.
   ![Versleuteling van opslag inschakelen][2]
3. Hallo **versleuteling** blade voor **storageacct1** wordt geopend. Selecteer **ingeschakeld**.
   ![Codering-blade][3]
4. Selecteer **Opslaan**.

U hebt nu de versleuteling van opslag voor ingeschakeld **storageacct1**.


## <a name="see-also"></a>Zie ook
Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'Enable codering voor Azure Storage-Account." toolearn meer informatie over Azure Storage-Service: versleuteling, Zie de volgende Hallo:

* [Azure Storage-Service: versleuteling voor gegevens in rust](../storage/common/storage-service-encryption.md)

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png

---
title: aaaService quota en limieten voor Azure Batch | Microsoft Docs
description: Meer informatie over Azure Batch standaardquota, limieten valt en -beperkingen en hoe toorequest quotum verhoogt
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 28998df4-8693-431d-b6ad-974c2f8db5fb
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6035d1c7618cfe97ebca3780e02a4ee34f54e534
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="batch-service-quotas-and-limits"></a>Quota en limieten voor Batch-service

Als met andere Azure-services, er zijn limieten op bepaalde resources die zijn gekoppeld aan Hallo Batch-service. Veel van deze limieten zijn standaardquota toegepast door Azure op Hallo abonnement of account niveau. In dit artikel worden de standaardinstellingen en hoe u kunt aanvragen quotum verhoogt.

Houd rekening met deze quota bij het ontwerpen en schalen van de Batch-workloads. Bijvoorbeeld, als uw pool is niet Hallo doelaantal rekenknooppunten die u hebt opgegeven wordt bereikt, u mogelijk hebt bereikt Hallo core quotumlimiet voor uw Batch-account of een regionale VM kernen quotum voor uw abonnement.

U kunt meerdere Batch-workloads in één Batch-account worden uitgevoerd of uw workloads verdelen over Batch-accounts die zich in Hallo hetzelfde abonnement behoren, maar in verschillende Azure-regio's.

Als u van plan toorun productie-workloads in Batch bent, moet u mogelijk tooincrease een of meer van de quota Hallo hierboven Hallo standaard. Als u wilt dat een quotum tooraise, opent u een online [klant ondersteuningsaanvraag](#increase-a-quota) zonder kosten.

> [!NOTE]
> Een quotum is een tegoed limiet, geen garantie capaciteit. Als u grootschalige capaciteitsbehoeften hebt, neem contact op met de ondersteuning van Azure.
> 
> 

## <a name="resource-quotas"></a>Resourcequota
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a>Quota's in de gebruikersmodus-abonnement

Voor een Batch-account met de groep toewijzing modus ingesteld te**gebruikerabonnement**, Batch-VM's en andere resources, zoals de storage-accounts, rechtstreeks in uw abonnement worden gemaakt wanneer een groep is gemaakt. Hello Azure Batch kernen quotum tooan account gemaakt in deze modus niet van toepassing. In plaats daarvan worden Hallo quota's in uw abonnement voor de regionale compute kernen en andere bronnen toegepast. Meer informatie over deze quota in [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).

Bij het plannen van Resourcegebruik voor een account dat is gemaakt in de gebruikersmodus abonnement Opmerking Hallo volgende Batch-resources (in aanvulling toocompute kernen) vereist zijn voor elke 40 virtuele Linux-machines of 20 VM's van Windows:

| Resource | Quota | Provider |
| --- | ---| --- |
| Een opslagaccount | Opslagaccounts | Microsoft.Storage |
| Een openbaar IP-adres | Openbare IP-adressen | Microsoft.Network | 
| Een virtueel netwerk | Virtuele netwerken | Microsoft.Network | 
| Een netwerkbeveiligingsgroep toevoegen | Netwerkbeveiligingsgroepen | Microsoft.Network | 
| Een virtuele-machineschaalset | Schaalsets voor virtuele machines | Microsoft.Compute | 
| Één load balancer | Taakverdelers | Microsoft.Network | 

Hallo kernen quotum op een regionaal niveau of per VM-serie moet set volgens toohello VM-grootte vereist is voor uw Batch-pool of groepen:

| Quota | Provider |
| --- | ---- |
| Totaal aantal regionale kernen | Microsoft.Compute |
| … Familie kernen | Microsoft.Compute |



## <a name="other-limits"></a>Andere limieten
| **Resource** | **Maximumaantal** |
| --- | --- |
| [Gelijktijdige taken](batch-parallel-node-tasks.md) per rekenknooppunt |4 x aantal kernen voor knooppunt |
| [Toepassingen](batch-application-packages.md) per Batch-account |20 |
| Toepassingspakketten per toepassing |40 |
| Grootte van de toepassing-pakket (elk) |Ongeveer 195GB<sup>1</sup> |
| Maximale startgrootte van taak | 32768 tekens<sup>2</sup> |

<sup>1</sup> azure Storage-limiet voor maximale blob blokgrootte<br />
<sup>2</sup> bevat bronbestanden en omgevingsvariabelen

## <a name="view-batch-quotas"></a>Batch-quota's weergeven
Uw Batch-account quota's weergeven in Hallo [Azure-portal][portal].

1. Selecteer **Batch-accounts** in Hallo-portal, selecteer vervolgens Hallo u geïnteresseerd bent in Batch-account.
2. Selecteer **eigenschappen** op Hallo Batch-account van menu blade.
3. Hallo eigenschappenblade geeft Hallo **quota** momenteel toegepast toohello Batch-account
   
    ![Quota voor batch-account][account_quotas]

Voor een Batch-account gemaakt in de gebruikersmodus abonnement gerelateerd weergave Hallo abonnement quota's in hello Azure-Portal.

1. Selecteer **abonnementen**, en u voor de Batch-account Hallo gebruikt Hallo-abonnement te selecteren.

2. Op Hallo **abonnement** blade Selecteer **gebruik + quota**.



## <a name="increase-a-quota"></a>Een quotum verhogen
Volg deze stappen toorequest een quotum verhogen voor uw Batch-account of voor uw abonnement met Hallo [Azure-portal][portal]. Hallo type verhoging van het quotum is afhankelijk van Hallo groep toewijzing modus van uw Batch-account.

### <a name="increase-a-batch-cores-quota"></a>Een Batch kernen quotum verhogen 

Als uw Batch-account is gemaakt in **Batch-service** modus, volg deze stappen toorequest een verhoging van Batch kernen quotum:

1. Selecteer Hallo **Help + ondersteuning** tegel op uw portal-dashboard of Hallo vraagteken (**?**) in Hallo rechterbovenhoek van Hallo-portal.
2. Selecteer **nieuw ondersteuningsverzoek** > **basisbeginselen**.
3. Op Hallo **basisbeginselen** blade:
   
    a. **Type probleem** > **quotum**
   
    b. Selecteer uw abonnement.
   
    c. **Quotumtype** > **Batch**
   
    d. **Ondersteuningsplan** > **quotum support - opgenomen**
   
    Klik op **Volgende**.
4. Op Hallo **probleem** blade:
   
    a. Selecteer een **ernst** volgens tooyour [bedrijfsimpact][support_sev].
   
    b. In **Details**, elke gewenste toochange Hallo Batch-accountnaam en de nieuwe limiet Hallo quota opgeven.
   
    Klik op **Volgende**.
5. Op Hallo **contactgegevens** blade:
   
    a. Selecteer een **voorkeur contactmethode**.
   
    b. Verifiëren en voer de contactgegevens Hallo vereist.
   
    Klik op **maken** toosubmit Hallo ondersteuning aan te vragen.

Nadat u uw ondersteuningsaanvraag hebt ingediend, ondersteuning van Azure contact met u op. Hallo aanvraag voltooien kan maximaal duren too2 werkdagen.

### <a name="increase-a-subscription-cores-quota"></a>Een abonnement kernen quotum verhogen

Als uw Batch-account is gemaakt in **gebruikerabonnement** modus en u moet extra regionale of VM-familie kernen, de aanvraag een quotum verhogen in uw abonnement. Zie voor stappen [kerngeheugenquotum voor Resource Manager verhogen aanvragen](../azure-supportability/resource-manager-core-quotas-request.md).



## <a name="related-topics"></a>Verwante onderwerpen
* [Een Azure Batch-account maken met hello Azure-portal](batch-account-create-portal.md)
* [Overzicht van Azure Batch-functies](batch-api-basics.md)
* [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG

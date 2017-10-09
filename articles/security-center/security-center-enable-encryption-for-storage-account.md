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
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="c17fc-103">Schakel versleuteling voor Azure storage-account in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="c17fc-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="c17fc-104">Azure Security Center kunt u het beste inschakelen Azure Storage-Service: versleuteling voor gegevens in rust.</span><span class="sxs-lookup"><span data-stu-id="c17fc-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="c17fc-105">Versleuteling voor opslag-Service (SSE) werkt door Hallo gegevens te coderen wanneer deze wordt tooAzure opslag geschreven en ontsleutelen van gegevens Hallo voordat ophalen.</span><span class="sxs-lookup"><span data-stu-id="c17fc-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="c17fc-106">SSE is momenteel alleen beschikbaar voor hello Azure Blob-service en kan worden gebruikt voor blok-blobs, pagina-blobs en toevoeg-blobs.</span><span class="sxs-lookup"><span data-stu-id="c17fc-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="c17fc-107">toolearn meer, Zie [Service versleuteling van opslag voor gegevens in rust](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="c17fc-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="c17fc-108">Nadat de codering is ingeschakeld, worden alleen nieuwe gegevens worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="c17fc-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="c17fc-109">Alle bestaande blobs in uw opslagaccount blijven onversleuteld.</span><span class="sxs-lookup"><span data-stu-id="c17fc-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="c17fc-110">tooencrypt bestaande blobs, Zie Hallo [opslag Service versleuteling Veelgestelde vragen over](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="c17fc-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="c17fc-111">Versleuteling van de opslagruimte wordt alleen ondersteund op Resource Manager storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="c17fc-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="c17fc-112">Klassieke opslagaccounts worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c17fc-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="c17fc-113">Zie toounderstand Hallo klassieke en het Resource Manager-implementatiemodel, [Azure-implementatiemodellen](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="c17fc-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c17fc-114">Dit document bevat Hallo service met behulp van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="c17fc-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="c17fc-115">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="c17fc-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="c17fc-116">Hallo aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="c17fc-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="c17fc-117">In Hallo **aanbevelingen** blade Selecteer **Schakel versleuteling voor Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="c17fc-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="c17fc-118">![Versleuteling inschakelen voor opslagaccount][1]</span><span class="sxs-lookup"><span data-stu-id="c17fc-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="c17fc-119">Hallo **inschakelen van versleuteling van opslag** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c17fc-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="c17fc-120">Deze blade bevat hello Azure storage-accounts waar versleuteling van opslag is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="c17fc-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="c17fc-121">In dit voorbeeld gaan we selecteren **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="c17fc-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="c17fc-122">![Versleuteling van opslag inschakelen][2]</span><span class="sxs-lookup"><span data-stu-id="c17fc-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="c17fc-123">Hallo **versleuteling** blade voor **storageacct1** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="c17fc-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="c17fc-124">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="c17fc-124">Select **Enabled**.</span></span>
   <span data-ttu-id="c17fc-125">![Codering-blade][3]</span><span class="sxs-lookup"><span data-stu-id="c17fc-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="c17fc-126">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="c17fc-126">Select **Save**.</span></span>

<span data-ttu-id="c17fc-127">U hebt nu de versleuteling van opslag voor ingeschakeld **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="c17fc-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="c17fc-128">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c17fc-128">See also</span></span>
<span data-ttu-id="c17fc-129">Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'Enable codering voor Azure Storage-Account."</span><span class="sxs-lookup"><span data-stu-id="c17fc-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="c17fc-130">toolearn meer informatie over Azure Storage-Service: versleuteling, Zie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="c17fc-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="c17fc-131">Azure Storage-Service: versleuteling voor gegevens in rust</span><span class="sxs-lookup"><span data-stu-id="c17fc-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="c17fc-132">toolearn meer informatie over Security Center Hallo ziet:</span><span class="sxs-lookup"><span data-stu-id="c17fc-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="c17fc-133">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over hoe tooconfigure beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen.</span><span class="sxs-lookup"><span data-stu-id="c17fc-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="c17fc-134">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over hoe toomonitor Hallo status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="c17fc-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="c17fc-135">[Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="c17fc-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="c17fc-136">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="c17fc-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="c17fc-137">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c17fc-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="c17fc-138">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="c17fc-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png

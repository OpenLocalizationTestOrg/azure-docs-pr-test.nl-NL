---
title: Schakel versleuteling voor storage-account in Azure Security Center | Microsoft Docs
description: Dit document ziet u hoe de Azure Security Center aanbevelingen implementeren ** versleuteling voor Azure Storage Account ** inschakelen.
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
ms.openlocfilehash: b7b2e8a12cbab68da9c8fcc348e8e3c543607007
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="476d2-103">Schakel versleuteling voor Azure storage-account in Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="476d2-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="476d2-104">Azure Security Center kunt u het beste inschakelen Azure Storage-Service: versleuteling voor gegevens in rust.</span><span class="sxs-lookup"><span data-stu-id="476d2-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="476d2-105">Versleuteling voor opslag-Service (SSE) werkt door de gegevens te coderen wanneer deze is geschreven naar Azure storage en ontsleutelen van de gegevens voordat ophalen.</span><span class="sxs-lookup"><span data-stu-id="476d2-105">Storage Service Encryption (SSE) works by encrypting the data when it is written to Azure storage and decrypting the data before retrieval.</span></span>  <span data-ttu-id="476d2-106">SSE is momenteel alleen beschikbaar voor de Azure Blob-service en kan worden gebruikt voor blok-blobs, pagina-blobs en toevoeg-blobs.</span><span class="sxs-lookup"><span data-stu-id="476d2-106">SSE is currently available only for the Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="476d2-107">Zie voor meer informatie, [Service versleuteling van opslag voor gegevens in rust](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="476d2-107">To learn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="476d2-108">Nadat de codering is ingeschakeld, worden alleen nieuwe gegevens worden versleuteld.</span><span class="sxs-lookup"><span data-stu-id="476d2-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="476d2-109">Alle bestaande blobs in uw opslagaccount blijven onversleuteld.</span><span class="sxs-lookup"><span data-stu-id="476d2-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="476d2-110">Voor het versleutelen van bestaande blobs, Zie de [opslag Service versleuteling Veelgestelde vragen over](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="476d2-110">To encrypt existing blobs, see the [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="476d2-111">Versleuteling van de opslagruimte wordt alleen ondersteund op Resource Manager storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="476d2-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="476d2-112">Klassieke opslagaccounts worden momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="476d2-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="476d2-113">Zie inzicht in het klassieke en het Resource Manager-implementatiemodel [Azure-implementatiemodellen](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="476d2-113">To understand the classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="476d2-114">In dit document wordt de service geïntroduceerd aan de hand van een voorbeeldimplementatie.</span><span class="sxs-lookup"><span data-stu-id="476d2-114">This document introduces the service by using an example deployment.</span></span>  <span data-ttu-id="476d2-115">Dit document is niet een stapsgewijze handleiding.</span><span class="sxs-lookup"><span data-stu-id="476d2-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-the-recommendation"></a><span data-ttu-id="476d2-116">De aanbeveling implementeren</span><span class="sxs-lookup"><span data-stu-id="476d2-116">Implement the recommendation</span></span>
1. <span data-ttu-id="476d2-117">In de **aanbevelingen** blade Selecteer **Schakel versleuteling voor Azure Storage-Account**.</span><span class="sxs-lookup"><span data-stu-id="476d2-117">In the **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="476d2-118">![Versleuteling inschakelen voor opslagaccount][1]</span><span class="sxs-lookup"><span data-stu-id="476d2-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="476d2-119">De **inschakelen van versleuteling van opslag** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="476d2-119">The **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="476d2-120">Deze blade bevat de Azure storage-accounts waar versleuteling van opslag is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="476d2-120">This blade lists the Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="476d2-121">In dit voorbeeld gaan we selecteren **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="476d2-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="476d2-122">![Versleuteling van opslag inschakelen][2]</span><span class="sxs-lookup"><span data-stu-id="476d2-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="476d2-123">De **versleuteling** blade voor **storageacct1** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="476d2-123">The **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="476d2-124">Selecteer **ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="476d2-124">Select **Enabled**.</span></span>
   <span data-ttu-id="476d2-125">![Codering-blade][3]</span><span class="sxs-lookup"><span data-stu-id="476d2-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="476d2-126">Selecteer **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="476d2-126">Select **Save**.</span></span>

<span data-ttu-id="476d2-127">U hebt nu de versleuteling van opslag voor ingeschakeld **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="476d2-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="476d2-128">Zie ook</span><span class="sxs-lookup"><span data-stu-id="476d2-128">See also</span></span>
<span data-ttu-id="476d2-129">Dit document hebt u geleerd hoe u de aanbeveling Security Center implementeert "Schakel versleuteling voor Azure Storage-Account."</span><span class="sxs-lookup"><span data-stu-id="476d2-129">This document showed you how to implement the Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="476d2-130">Voor meer informatie over Azure Storage-Service: versleuteling, Zie de volgende:</span><span class="sxs-lookup"><span data-stu-id="476d2-130">To learn more about Azure Storage Service Encryption, see the following:</span></span>

* [<span data-ttu-id="476d2-131">Azure Storage-Service: versleuteling voor gegevens in rust</span><span class="sxs-lookup"><span data-stu-id="476d2-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="476d2-132">Zie de volgende onderwerpen voor meer informatie over het Beveiligingscentrum:</span><span class="sxs-lookup"><span data-stu-id="476d2-132">To learn more about Security Center, see the following:</span></span>

* <span data-ttu-id="476d2-133">[Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) -informatie over het beveiligingsbeleid voor uw Azure-abonnementen en resourcegroepen configureren.</span><span class="sxs-lookup"><span data-stu-id="476d2-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how to configure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="476d2-134">[Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) -informatie over het bewaken van de status van uw Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="476d2-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how to monitor the health of your Azure resources.</span></span>
* <span data-ttu-id="476d2-135">[Het beheren van en reageren op beveiligingswaarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) -informatie over het beheren van en reageren op beveiligingswaarschuwingen.</span><span class="sxs-lookup"><span data-stu-id="476d2-135">[Managing and responding to security alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how to manage and respond to security alerts.</span></span>
* <span data-ttu-id="476d2-136">[Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) -Leer hoe aanbevelingen u uw Azure-resources te beveiligen.</span><span class="sxs-lookup"><span data-stu-id="476d2-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="476d2-137">[Veelgestelde vragen over Azure Security Center](security-center-faq.md) -Raadpleeg Veelgestelde vragen over het gebruik van de service.</span><span class="sxs-lookup"><span data-stu-id="476d2-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using the service.</span></span>
* <span data-ttu-id="476d2-138">[Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) -Lees blogberichten over Azure-beveiliging en naleving.</span><span class="sxs-lookup"><span data-stu-id="476d2-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png

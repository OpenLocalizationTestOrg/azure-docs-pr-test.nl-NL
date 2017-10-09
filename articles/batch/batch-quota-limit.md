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
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="14f5e-103">Quota en limieten voor Batch-service</span><span class="sxs-lookup"><span data-stu-id="14f5e-103">Batch service quotas and limits</span></span>

<span data-ttu-id="14f5e-104">Als met andere Azure-services, er zijn limieten op bepaalde resources die zijn gekoppeld aan Hallo Batch-service.</span><span class="sxs-lookup"><span data-stu-id="14f5e-104">As with other Azure services, there are limits on certain resources associated with hello Batch service.</span></span> <span data-ttu-id="14f5e-105">Veel van deze limieten zijn standaardquota toegepast door Azure op Hallo abonnement of account niveau.</span><span class="sxs-lookup"><span data-stu-id="14f5e-105">Many of these limits are default quotas applied by Azure at hello subscription or account level.</span></span> <span data-ttu-id="14f5e-106">In dit artikel worden de standaardinstellingen en hoe u kunt aanvragen quotum verhoogt.</span><span class="sxs-lookup"><span data-stu-id="14f5e-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="14f5e-107">Houd rekening met deze quota bij het ontwerpen en schalen van de Batch-workloads.</span><span class="sxs-lookup"><span data-stu-id="14f5e-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="14f5e-108">Bijvoorbeeld, als uw pool is niet Hallo doelaantal rekenknooppunten die u hebt opgegeven wordt bereikt, u mogelijk hebt bereikt Hallo core quotumlimiet voor uw Batch-account of een regionale VM kernen quotum voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="14f5e-108">For example, if your pool isn't reaching hello target number of compute nodes you've specified, you might have reached hello core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="14f5e-109">U kunt meerdere Batch-workloads in één Batch-account worden uitgevoerd of uw workloads verdelen over Batch-accounts die zich in Hallo hetzelfde abonnement behoren, maar in verschillende Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="14f5e-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in hello same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="14f5e-110">Als u van plan toorun productie-workloads in Batch bent, moet u mogelijk tooincrease een of meer van de quota Hallo hierboven Hallo standaard.</span><span class="sxs-lookup"><span data-stu-id="14f5e-110">If you plan toorun production workloads in Batch, you may need tooincrease one or more of hello quotas above hello default.</span></span> <span data-ttu-id="14f5e-111">Als u wilt dat een quotum tooraise, opent u een online [klant ondersteuningsaanvraag](#increase-a-quota) zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="14f5e-111">If you want tooraise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="14f5e-112">Een quotum is een tegoed limiet, geen garantie capaciteit.</span><span class="sxs-lookup"><span data-stu-id="14f5e-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="14f5e-113">Als u grootschalige capaciteitsbehoeften hebt, neem contact op met de ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="14f5e-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="14f5e-114">Resourcequota</span><span class="sxs-lookup"><span data-stu-id="14f5e-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="14f5e-115">Quota's in de gebruikersmodus-abonnement</span><span class="sxs-lookup"><span data-stu-id="14f5e-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="14f5e-116">Voor een Batch-account met de groep toewijzing modus ingesteld te**gebruikerabonnement**, Batch-VM's en andere resources, zoals de storage-accounts, rechtstreeks in uw abonnement worden gemaakt wanneer een groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="14f5e-116">For a Batch account with pool allocation mode set too**user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="14f5e-117">Hello Azure Batch kernen quotum tooan account gemaakt in deze modus niet van toepassing.</span><span class="sxs-lookup"><span data-stu-id="14f5e-117">hello Azure Batch cores quota does not apply tooan account created in this mode.</span></span> <span data-ttu-id="14f5e-118">In plaats daarvan worden Hallo quota's in uw abonnement voor de regionale compute kernen en andere bronnen toegepast.</span><span class="sxs-lookup"><span data-stu-id="14f5e-118">Instead, hello quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="14f5e-119">Meer informatie over deze quota in [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="14f5e-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="14f5e-120">Bij het plannen van Resourcegebruik voor een account dat is gemaakt in de gebruikersmodus abonnement Opmerking Hallo volgende Batch-resources (in aanvulling toocompute kernen) vereist zijn voor elke 40 virtuele Linux-machines of 20 VM's van Windows:</span><span class="sxs-lookup"><span data-stu-id="14f5e-120">When planning resource usage for an account created in user subscription mode, note hello following Batch resources (in addition toocompute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="14f5e-121">Resource</span><span class="sxs-lookup"><span data-stu-id="14f5e-121">Resource</span></span> | <span data-ttu-id="14f5e-122">Quota</span><span class="sxs-lookup"><span data-stu-id="14f5e-122">Quota</span></span> | <span data-ttu-id="14f5e-123">Provider</span><span class="sxs-lookup"><span data-stu-id="14f5e-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="14f5e-124">Een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="14f5e-124">One storage account</span></span> | <span data-ttu-id="14f5e-125">Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="14f5e-125">Storage Accounts</span></span> | <span data-ttu-id="14f5e-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="14f5e-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="14f5e-127">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="14f5e-127">One public IP address</span></span> | <span data-ttu-id="14f5e-128">Openbare IP-adressen</span><span class="sxs-lookup"><span data-stu-id="14f5e-128">Public IP Addresses</span></span> | <span data-ttu-id="14f5e-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="14f5e-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="14f5e-130">Een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="14f5e-130">One virtual network</span></span> | <span data-ttu-id="14f5e-131">Virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="14f5e-131">Virtual Networks</span></span> | <span data-ttu-id="14f5e-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="14f5e-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="14f5e-133">Een netwerkbeveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="14f5e-133">One network security group</span></span> | <span data-ttu-id="14f5e-134">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="14f5e-134">Network Security Groups</span></span> | <span data-ttu-id="14f5e-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="14f5e-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="14f5e-136">Een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="14f5e-136">One virtual machine scale set</span></span> | <span data-ttu-id="14f5e-137">Schaalsets voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="14f5e-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="14f5e-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="14f5e-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="14f5e-139">Één load balancer</span><span class="sxs-lookup"><span data-stu-id="14f5e-139">One load balancer</span></span> | <span data-ttu-id="14f5e-140">Taakverdelers</span><span class="sxs-lookup"><span data-stu-id="14f5e-140">Load Balancers</span></span> | <span data-ttu-id="14f5e-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="14f5e-141">Microsoft.Network</span></span> | 

<span data-ttu-id="14f5e-142">Hallo kernen quotum op een regionaal niveau of per VM-serie moet set volgens toohello VM-grootte vereist is voor uw Batch-pool of groepen:</span><span class="sxs-lookup"><span data-stu-id="14f5e-142">hello cores quota at a regional level or per VM family should be set according toohello VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="14f5e-143">Quota</span><span class="sxs-lookup"><span data-stu-id="14f5e-143">Quota</span></span> | <span data-ttu-id="14f5e-144">Provider</span><span class="sxs-lookup"><span data-stu-id="14f5e-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="14f5e-145">Totaal aantal regionale kernen</span><span class="sxs-lookup"><span data-stu-id="14f5e-145">Total Regional Cores</span></span> | <span data-ttu-id="14f5e-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="14f5e-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="14f5e-147">…</span><span class="sxs-lookup"><span data-stu-id="14f5e-147">…</span></span> <span data-ttu-id="14f5e-148">Familie kernen</span><span class="sxs-lookup"><span data-stu-id="14f5e-148">Family Cores</span></span> | <span data-ttu-id="14f5e-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="14f5e-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="14f5e-150">Andere limieten</span><span class="sxs-lookup"><span data-stu-id="14f5e-150">Other limits</span></span>
| <span data-ttu-id="14f5e-151">**Resource**</span><span class="sxs-lookup"><span data-stu-id="14f5e-151">**Resource**</span></span> | <span data-ttu-id="14f5e-152">**Maximumaantal**</span><span class="sxs-lookup"><span data-stu-id="14f5e-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="14f5e-153">[Gelijktijdige taken](batch-parallel-node-tasks.md) per rekenknooppunt</span><span class="sxs-lookup"><span data-stu-id="14f5e-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="14f5e-154">4 x aantal kernen voor knooppunt</span><span class="sxs-lookup"><span data-stu-id="14f5e-154">4 x number of node cores</span></span> |
| <span data-ttu-id="14f5e-155">[Toepassingen](batch-application-packages.md) per Batch-account</span><span class="sxs-lookup"><span data-stu-id="14f5e-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="14f5e-156">20</span><span class="sxs-lookup"><span data-stu-id="14f5e-156">20</span></span> |
| <span data-ttu-id="14f5e-157">Toepassingspakketten per toepassing</span><span class="sxs-lookup"><span data-stu-id="14f5e-157">Application packages per application</span></span> |<span data-ttu-id="14f5e-158">40</span><span class="sxs-lookup"><span data-stu-id="14f5e-158">40</span></span> |
| <span data-ttu-id="14f5e-159">Grootte van de toepassing-pakket (elk)</span><span class="sxs-lookup"><span data-stu-id="14f5e-159">Application package size (each)</span></span> |<span data-ttu-id="14f5e-160">Ongeveer 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="14f5e-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="14f5e-161">Maximale startgrootte van taak</span><span class="sxs-lookup"><span data-stu-id="14f5e-161">Maximum start task size</span></span> | <span data-ttu-id="14f5e-162">32768 tekens<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="14f5e-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="14f5e-163"><sup>1</sup> azure Storage-limiet voor maximale blob blokgrootte</span><span class="sxs-lookup"><span data-stu-id="14f5e-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="14f5e-164">
<sup>2</sup> bevat bronbestanden en omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="14f5e-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="14f5e-165">Batch-quota's weergeven</span><span class="sxs-lookup"><span data-stu-id="14f5e-165">View Batch quotas</span></span>
<span data-ttu-id="14f5e-166">Uw Batch-account quota's weergeven in Hallo [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="14f5e-166">View your Batch account quotas in hello [Azure portal][portal].</span></span>

1. <span data-ttu-id="14f5e-167">Selecteer **Batch-accounts** in Hallo-portal, selecteer vervolgens Hallo u geïnteresseerd bent in Batch-account.</span><span class="sxs-lookup"><span data-stu-id="14f5e-167">Select **Batch accounts** in hello portal, then select hello Batch account you're interested in.</span></span>
2. <span data-ttu-id="14f5e-168">Selecteer **eigenschappen** op Hallo Batch-account van menu blade.</span><span class="sxs-lookup"><span data-stu-id="14f5e-168">Select **Properties** on hello Batch account's menu blade.</span></span>
3. <span data-ttu-id="14f5e-169">Hallo eigenschappenblade geeft Hallo **quota** momenteel toegepast toohello Batch-account</span><span class="sxs-lookup"><span data-stu-id="14f5e-169">hello Properties blade displays hello **quotas** currently applied toohello Batch account</span></span>
   
    ![Quota voor batch-account][account_quotas]

<span data-ttu-id="14f5e-171">Voor een Batch-account gemaakt in de gebruikersmodus abonnement gerelateerd weergave Hallo abonnement quota's in hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="14f5e-171">For a Batch account created in user subscription mode, view hello related subscription quotas in hello Azure Portal.</span></span>

1. <span data-ttu-id="14f5e-172">Selecteer **abonnementen**, en u voor de Batch-account Hallo gebruikt Hallo-abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="14f5e-172">Select **Subscriptions**, and select hello subscription you are using for hello Batch account.</span></span>

2. <span data-ttu-id="14f5e-173">Op Hallo **abonnement** blade Selecteer **gebruik + quota**.</span><span class="sxs-lookup"><span data-stu-id="14f5e-173">On hello **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="14f5e-174">Een quotum verhogen</span><span class="sxs-lookup"><span data-stu-id="14f5e-174">Increase a quota</span></span>
<span data-ttu-id="14f5e-175">Volg deze stappen toorequest een quotum verhogen voor uw Batch-account of voor uw abonnement met Hallo [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="14f5e-175">Follow these steps toorequest a quota increase for your Batch account or your subscription using hello [Azure portal][portal].</span></span> <span data-ttu-id="14f5e-176">Hallo type verhoging van het quotum is afhankelijk van Hallo groep toewijzing modus van uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="14f5e-176">hello type of quota increase depends on hello pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="14f5e-177">Een Batch kernen quotum verhogen</span><span class="sxs-lookup"><span data-stu-id="14f5e-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="14f5e-178">Als uw Batch-account is gemaakt in **Batch-service** modus, volg deze stappen toorequest een verhoging van Batch kernen quotum:</span><span class="sxs-lookup"><span data-stu-id="14f5e-178">If your Batch account was created in **Batch service** mode, follow these steps toorequest a Batch cores quota increase:</span></span>

1. <span data-ttu-id="14f5e-179">Selecteer Hallo **Help + ondersteuning** tegel op uw portal-dashboard of Hallo vraagteken (**?**) in Hallo rechterbovenhoek van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="14f5e-179">Select hello **Help + support** tile on your portal dashboard, or hello question mark (**?**) in hello upper-right corner of hello portal.</span></span>
2. <span data-ttu-id="14f5e-180">Selecteer **nieuw ondersteuningsverzoek** > **basisbeginselen**.</span><span class="sxs-lookup"><span data-stu-id="14f5e-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="14f5e-181">Op Hallo **basisbeginselen** blade:</span><span class="sxs-lookup"><span data-stu-id="14f5e-181">On hello **Basics** blade:</span></span>
   
    <span data-ttu-id="14f5e-182">a.</span><span class="sxs-lookup"><span data-stu-id="14f5e-182">a.</span></span> <span data-ttu-id="14f5e-183">**Type probleem** > **quotum**</span><span class="sxs-lookup"><span data-stu-id="14f5e-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="14f5e-184">b.</span><span class="sxs-lookup"><span data-stu-id="14f5e-184">b.</span></span> <span data-ttu-id="14f5e-185">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="14f5e-185">Select your subscription.</span></span>
   
    <span data-ttu-id="14f5e-186">c.</span><span class="sxs-lookup"><span data-stu-id="14f5e-186">c.</span></span> <span data-ttu-id="14f5e-187">**Quotumtype** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="14f5e-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="14f5e-188">d.</span><span class="sxs-lookup"><span data-stu-id="14f5e-188">d.</span></span> <span data-ttu-id="14f5e-189">**Ondersteuningsplan** > **quotum support - opgenomen**</span><span class="sxs-lookup"><span data-stu-id="14f5e-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="14f5e-190">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="14f5e-190">Click **Next**.</span></span>
4. <span data-ttu-id="14f5e-191">Op Hallo **probleem** blade:</span><span class="sxs-lookup"><span data-stu-id="14f5e-191">On hello **Problem** blade:</span></span>
   
    <span data-ttu-id="14f5e-192">a.</span><span class="sxs-lookup"><span data-stu-id="14f5e-192">a.</span></span> <span data-ttu-id="14f5e-193">Selecteer een **ernst** volgens tooyour [bedrijfsimpact][support_sev].</span><span class="sxs-lookup"><span data-stu-id="14f5e-193">Select a **Severity** according tooyour [business impact][support_sev].</span></span>
   
    <span data-ttu-id="14f5e-194">b.</span><span class="sxs-lookup"><span data-stu-id="14f5e-194">b.</span></span> <span data-ttu-id="14f5e-195">In **Details**, elke gewenste toochange Hallo Batch-accountnaam en de nieuwe limiet Hallo quota opgeven.</span><span class="sxs-lookup"><span data-stu-id="14f5e-195">In **Details**, specify each quota you want toochange, hello Batch account name, and hello new limit.</span></span>
   
    <span data-ttu-id="14f5e-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="14f5e-196">Click **Next**.</span></span>
5. <span data-ttu-id="14f5e-197">Op Hallo **contactgegevens** blade:</span><span class="sxs-lookup"><span data-stu-id="14f5e-197">On hello **Contact information** blade:</span></span>
   
    <span data-ttu-id="14f5e-198">a.</span><span class="sxs-lookup"><span data-stu-id="14f5e-198">a.</span></span> <span data-ttu-id="14f5e-199">Selecteer een **voorkeur contactmethode**.</span><span class="sxs-lookup"><span data-stu-id="14f5e-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="14f5e-200">b.</span><span class="sxs-lookup"><span data-stu-id="14f5e-200">b.</span></span> <span data-ttu-id="14f5e-201">Verifiëren en voer de contactgegevens Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="14f5e-201">Verify and enter hello required contact details.</span></span>
   
    <span data-ttu-id="14f5e-202">Klik op **maken** toosubmit Hallo ondersteuning aan te vragen.</span><span class="sxs-lookup"><span data-stu-id="14f5e-202">Click **Create** toosubmit hello support request.</span></span>

<span data-ttu-id="14f5e-203">Nadat u uw ondersteuningsaanvraag hebt ingediend, ondersteuning van Azure contact met u op.</span><span class="sxs-lookup"><span data-stu-id="14f5e-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="14f5e-204">Hallo aanvraag voltooien kan maximaal duren too2 werkdagen.</span><span class="sxs-lookup"><span data-stu-id="14f5e-204">Note that completing hello request can take up too2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="14f5e-205">Een abonnement kernen quotum verhogen</span><span class="sxs-lookup"><span data-stu-id="14f5e-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="14f5e-206">Als uw Batch-account is gemaakt in **gebruikerabonnement** modus en u moet extra regionale of VM-familie kernen, de aanvraag een quotum verhogen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="14f5e-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="14f5e-207">Zie voor stappen [kerngeheugenquotum voor Resource Manager verhogen aanvragen](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="14f5e-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="14f5e-208">Verwante onderwerpen</span><span class="sxs-lookup"><span data-stu-id="14f5e-208">Related topics</span></span>
* [<span data-ttu-id="14f5e-209">Een Azure Batch-account maken met hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="14f5e-209">Create an Azure Batch account using hello Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="14f5e-210">Overzicht van Azure Batch-functies</span><span class="sxs-lookup"><span data-stu-id="14f5e-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="14f5e-211">Azure-abonnement en Servicelimieten, quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="14f5e-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG

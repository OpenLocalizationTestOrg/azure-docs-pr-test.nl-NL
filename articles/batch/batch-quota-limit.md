---
title: Quota en limieten voor Azure Batch service | Microsoft Docs
description: Meer informatie over Azure Batch standaardquota, limieten en beperkingen en verhoogt het quotum aanvragen
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
ms.openlocfilehash: f3f69ed8d3a985afe07e648e7512a88b25278ced
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="batch-service-quotas-and-limits"></a><span data-ttu-id="7477c-103">Quota en limieten voor Batch-service</span><span class="sxs-lookup"><span data-stu-id="7477c-103">Batch service quotas and limits</span></span>

<span data-ttu-id="7477c-104">Zoals met andere Azure-services, moet u er limieten op bepaalde resources die zijn gekoppeld aan de Batch-service zijn.</span><span class="sxs-lookup"><span data-stu-id="7477c-104">As with other Azure services, there are limits on certain resources associated with the Batch service.</span></span> <span data-ttu-id="7477c-105">Veel van deze limieten zijn standaardquota door Azure wordt toegepast op het niveau van de account of het abonnement.</span><span class="sxs-lookup"><span data-stu-id="7477c-105">Many of these limits are default quotas applied by Azure at the subscription or account level.</span></span> <span data-ttu-id="7477c-106">In dit artikel worden de standaardinstellingen en hoe u kunt aanvragen quotum verhoogt.</span><span class="sxs-lookup"><span data-stu-id="7477c-106">This article discusses those defaults, and how you can request quota increases.</span></span>

<span data-ttu-id="7477c-107">Houd rekening met deze quota bij het ontwerpen en schalen van de Batch-workloads.</span><span class="sxs-lookup"><span data-stu-id="7477c-107">Keep these quotas in mind as you are designing and scaling up your Batch workloads.</span></span> <span data-ttu-id="7477c-108">Bijvoorbeeld, als uw pool is niet het is het doelaantal van rekenknooppunten die u hebt opgegeven bereikt, u mogelijk hebt bereikt de quotalimiet core voor uw Batch-account of een regionale VM kernen quotum voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7477c-108">For example, if your pool isn't reaching the target number of compute nodes you've specified, you might have reached the core quota limit for your Batch account, or a regional VM cores quota for your subscription.</span></span>

<span data-ttu-id="7477c-109">U kunt in één Batch-account meerdere Batch-workloads uitvoeren of uw workloads verdelen over Batch-accounts in hetzelfde abonnement maar in verschillende Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="7477c-109">You can run multiple Batch workloads in a single Batch account, or distribute your workloads among Batch accounts that are in the same subscription, but in different Azure regions.</span></span>

<span data-ttu-id="7477c-110">Als u van plan bent te productieworkloads in Batch uitvoeren, moet u wellicht een of meer van de quota boven de standaardwaarde verhogen.</span><span class="sxs-lookup"><span data-stu-id="7477c-110">If you plan to run production workloads in Batch, you may need to increase one or more of the quotas above the default.</span></span> <span data-ttu-id="7477c-111">Als u een quotum te verhogen wilt, opent u een online [klant ondersteuningsaanvraag](#increase-a-quota) zonder kosten.</span><span class="sxs-lookup"><span data-stu-id="7477c-111">If you want to raise a quota, you can open an online [customer support request](#increase-a-quota) at no charge.</span></span>

> [!NOTE]
> <span data-ttu-id="7477c-112">Een quotum is een tegoed limiet, geen garantie capaciteit.</span><span class="sxs-lookup"><span data-stu-id="7477c-112">A quota is a credit limit, not a capacity guarantee.</span></span> <span data-ttu-id="7477c-113">Als u grootschalige capaciteitsbehoeften hebt, neem contact op met de ondersteuning van Azure.</span><span class="sxs-lookup"><span data-stu-id="7477c-113">If you have large-scale capacity needs, please contact Azure support.</span></span>
> 
> 

## <a name="resource-quotas"></a><span data-ttu-id="7477c-114">Resourcequota</span><span class="sxs-lookup"><span data-stu-id="7477c-114">Resource quotas</span></span>
[!INCLUDE [azure-batch-limits](../../includes/azure-batch-limits.md)]

## <a name="quotas-in-user-subscription-mode"></a><span data-ttu-id="7477c-115">Quota's in de gebruikersmodus-abonnement</span><span class="sxs-lookup"><span data-stu-id="7477c-115">Quotas in user subscription mode</span></span>

<span data-ttu-id="7477c-116">Voor een Batch-account met de groep toewijzing modus is ingesteld op **gebruikerabonnement**, Batch-VM's en andere resources, zoals de storage-accounts, rechtstreeks in uw abonnement worden gemaakt wanneer een groep is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7477c-116">For a Batch account with pool allocation mode set to **user subscription**, Batch VMs and other resources, such as storage accounts, are created directly in your subscription when a pool is created.</span></span> <span data-ttu-id="7477c-117">Het quotum van Azure Batch kernen geldt niet voor een account dat is gemaakt in deze modus.</span><span class="sxs-lookup"><span data-stu-id="7477c-117">The Azure Batch cores quota does not apply to an account created in this mode.</span></span> <span data-ttu-id="7477c-118">In plaats daarvan de quota's in uw abonnement voor de regionale compute kernen en andere resources zijn toegepast.</span><span class="sxs-lookup"><span data-stu-id="7477c-118">Instead, the quotas in your subscription for regional compute cores and other resources are applied.</span></span> <span data-ttu-id="7477c-119">Meer informatie over deze quota in [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="7477c-119">Learn more about these quotas in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="7477c-120">Houd rekening met dat de volgende Batch-resources (in aanvulling op compute kernen) zijn vereist voor elke 40 virtuele Linux-machines of 20 VM's van Windows bij het plannen van Resourcegebruik voor een account dat is gemaakt in de gebruikersmodus abonnement:</span><span class="sxs-lookup"><span data-stu-id="7477c-120">When planning resource usage for an account created in user subscription mode, note the following Batch resources (in addition to compute cores) are required for every 40 Linux VMs, or 20 Windows VMs:</span></span>

| <span data-ttu-id="7477c-121">Resource</span><span class="sxs-lookup"><span data-stu-id="7477c-121">Resource</span></span> | <span data-ttu-id="7477c-122">Quota</span><span class="sxs-lookup"><span data-stu-id="7477c-122">Quota</span></span> | <span data-ttu-id="7477c-123">Provider</span><span class="sxs-lookup"><span data-stu-id="7477c-123">Provider</span></span> |
| --- | ---| --- |
| <span data-ttu-id="7477c-124">Een opslagaccount</span><span class="sxs-lookup"><span data-stu-id="7477c-124">One storage account</span></span> | <span data-ttu-id="7477c-125">Opslagaccounts</span><span class="sxs-lookup"><span data-stu-id="7477c-125">Storage Accounts</span></span> | <span data-ttu-id="7477c-126">Microsoft.Storage</span><span class="sxs-lookup"><span data-stu-id="7477c-126">Microsoft.Storage</span></span> |
| <span data-ttu-id="7477c-127">Een openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="7477c-127">One public IP address</span></span> | <span data-ttu-id="7477c-128">Openbare IP-adressen</span><span class="sxs-lookup"><span data-stu-id="7477c-128">Public IP Addresses</span></span> | <span data-ttu-id="7477c-129">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7477c-129">Microsoft.Network</span></span> | 
| <span data-ttu-id="7477c-130">Een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="7477c-130">One virtual network</span></span> | <span data-ttu-id="7477c-131">Virtuele netwerken</span><span class="sxs-lookup"><span data-stu-id="7477c-131">Virtual Networks</span></span> | <span data-ttu-id="7477c-132">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7477c-132">Microsoft.Network</span></span> | 
| <span data-ttu-id="7477c-133">Een netwerkbeveiligingsgroep toevoegen</span><span class="sxs-lookup"><span data-stu-id="7477c-133">One network security group</span></span> | <span data-ttu-id="7477c-134">Netwerkbeveiligingsgroepen</span><span class="sxs-lookup"><span data-stu-id="7477c-134">Network Security Groups</span></span> | <span data-ttu-id="7477c-135">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7477c-135">Microsoft.Network</span></span> | 
| <span data-ttu-id="7477c-136">Een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="7477c-136">One virtual machine scale set</span></span> | <span data-ttu-id="7477c-137">Schaalsets voor virtuele machines</span><span class="sxs-lookup"><span data-stu-id="7477c-137">Virtual Machine Scale Sets</span></span> | <span data-ttu-id="7477c-138">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7477c-138">Microsoft.Compute</span></span> | 
| <span data-ttu-id="7477c-139">Één load balancer</span><span class="sxs-lookup"><span data-stu-id="7477c-139">One load balancer</span></span> | <span data-ttu-id="7477c-140">Taakverdelers</span><span class="sxs-lookup"><span data-stu-id="7477c-140">Load Balancers</span></span> | <span data-ttu-id="7477c-141">Microsoft.Network</span><span class="sxs-lookup"><span data-stu-id="7477c-141">Microsoft.Network</span></span> | 

<span data-ttu-id="7477c-142">Het quotum voor kernen op een regionaal niveau of per VM-familie moet worden ingesteld volgens de VM-grootte die vereist zijn voor uw Batch-pool of groepen:</span><span class="sxs-lookup"><span data-stu-id="7477c-142">The cores quota at a regional level or per VM family should be set according to the VM size required for your Batch pool or pools:</span></span>

| <span data-ttu-id="7477c-143">Quota</span><span class="sxs-lookup"><span data-stu-id="7477c-143">Quota</span></span> | <span data-ttu-id="7477c-144">Provider</span><span class="sxs-lookup"><span data-stu-id="7477c-144">Provider</span></span> |
| --- | ---- |
| <span data-ttu-id="7477c-145">Totaal aantal regionale kernen</span><span class="sxs-lookup"><span data-stu-id="7477c-145">Total Regional Cores</span></span> | <span data-ttu-id="7477c-146">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7477c-146">Microsoft.Compute</span></span> |
| <span data-ttu-id="7477c-147">…</span><span class="sxs-lookup"><span data-stu-id="7477c-147">…</span></span> <span data-ttu-id="7477c-148">Familie kernen</span><span class="sxs-lookup"><span data-stu-id="7477c-148">Family Cores</span></span> | <span data-ttu-id="7477c-149">Microsoft.Compute</span><span class="sxs-lookup"><span data-stu-id="7477c-149">Microsoft.Compute</span></span> |



## <a name="other-limits"></a><span data-ttu-id="7477c-150">Andere limieten</span><span class="sxs-lookup"><span data-stu-id="7477c-150">Other limits</span></span>
| <span data-ttu-id="7477c-151">**Resource**</span><span class="sxs-lookup"><span data-stu-id="7477c-151">**Resource**</span></span> | <span data-ttu-id="7477c-152">**Maximumaantal**</span><span class="sxs-lookup"><span data-stu-id="7477c-152">**Maximum Limit**</span></span> |
| --- | --- |
| <span data-ttu-id="7477c-153">[Gelijktijdige taken](batch-parallel-node-tasks.md) per rekenknooppunt</span><span class="sxs-lookup"><span data-stu-id="7477c-153">[Concurrent tasks](batch-parallel-node-tasks.md) per compute node</span></span> |<span data-ttu-id="7477c-154">4 x aantal kernen voor knooppunt</span><span class="sxs-lookup"><span data-stu-id="7477c-154">4 x number of node cores</span></span> |
| <span data-ttu-id="7477c-155">[Toepassingen](batch-application-packages.md) per Batch-account</span><span class="sxs-lookup"><span data-stu-id="7477c-155">[Applications](batch-application-packages.md) per Batch account</span></span> |<span data-ttu-id="7477c-156">20</span><span class="sxs-lookup"><span data-stu-id="7477c-156">20</span></span> |
| <span data-ttu-id="7477c-157">Toepassingspakketten per toepassing</span><span class="sxs-lookup"><span data-stu-id="7477c-157">Application packages per application</span></span> |<span data-ttu-id="7477c-158">40</span><span class="sxs-lookup"><span data-stu-id="7477c-158">40</span></span> |
| <span data-ttu-id="7477c-159">Grootte van de toepassing-pakket (elk)</span><span class="sxs-lookup"><span data-stu-id="7477c-159">Application package size (each)</span></span> |<span data-ttu-id="7477c-160">Ongeveer 195GB<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="7477c-160">Approx. 195GB<sup>1</sup></span></span> |
| <span data-ttu-id="7477c-161">Maximale startgrootte van taak</span><span class="sxs-lookup"><span data-stu-id="7477c-161">Maximum start task size</span></span> | <span data-ttu-id="7477c-162">32768 tekens<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="7477c-162">32768 characters<sup>2</sup></span></span> |

<span data-ttu-id="7477c-163"><sup>1</sup> azure Storage-limiet voor maximale blob blokgrootte</span><span class="sxs-lookup"><span data-stu-id="7477c-163"><sup>1</sup> Azure Storage limit for maximum block blob size</span></span><br /><span data-ttu-id="7477c-164">
<sup>2</sup> bevat bronbestanden en omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="7477c-164">
<sup>2</sup> Includes resource files and environment variables</span></span>

## <a name="view-batch-quotas"></a><span data-ttu-id="7477c-165">Batch-quota's weergeven</span><span class="sxs-lookup"><span data-stu-id="7477c-165">View Batch quotas</span></span>
<span data-ttu-id="7477c-166">Weergeven van uw Batch-account quota's in de [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="7477c-166">View your Batch account quotas in the [Azure portal][portal].</span></span>

1. <span data-ttu-id="7477c-167">Selecteer **Batch-accounts** in de portal, selecteer vervolgens het Batch-account dat u geïnteresseerd bent in.</span><span class="sxs-lookup"><span data-stu-id="7477c-167">Select **Batch accounts** in the portal, then select the Batch account you're interested in.</span></span>
2. <span data-ttu-id="7477c-168">Selecteer **eigenschappen** op het Batch-account menu blade.</span><span class="sxs-lookup"><span data-stu-id="7477c-168">Select **Properties** on the Batch account's menu blade.</span></span>
3. <span data-ttu-id="7477c-169">De eigenschappenblade geeft de **quota** momenteel wordt toegepast op het Batch-account</span><span class="sxs-lookup"><span data-stu-id="7477c-169">The Properties blade displays the **quotas** currently applied to the Batch account</span></span>
   
    ![Quota voor batch-account][account_quotas]

<span data-ttu-id="7477c-171">Weergeven voor een Batch-account is gemaakt in de gebruikersmodus abonnement, de verwante abonnement quota in de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="7477c-171">For a Batch account created in user subscription mode, view the related subscription quotas in the Azure Portal.</span></span>

1. <span data-ttu-id="7477c-172">Selecteer **abonnementen**, en selecteer het abonnement dat u voor het Batch-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7477c-172">Select **Subscriptions**, and select the subscription you are using for the Batch account.</span></span>

2. <span data-ttu-id="7477c-173">Op de **abonnement** blade Selecteer **gebruik + quota**.</span><span class="sxs-lookup"><span data-stu-id="7477c-173">On the **Subscription** blade, select **Usage + quotas**.</span></span>



## <a name="increase-a-quota"></a><span data-ttu-id="7477c-174">Een quotum verhogen</span><span class="sxs-lookup"><span data-stu-id="7477c-174">Increase a quota</span></span>
<span data-ttu-id="7477c-175">Volg deze stappen om aan te vragen een quotum voor uw Batch-account of uw abonnement met verhogen de [Azure-portal][portal].</span><span class="sxs-lookup"><span data-stu-id="7477c-175">Follow these steps to request a quota increase for your Batch account or your subscription using the [Azure portal][portal].</span></span> <span data-ttu-id="7477c-176">Het type van de verhoging van het quotum is afhankelijk van de modus van de toewijzing van toepassingen van uw Batch-account.</span><span class="sxs-lookup"><span data-stu-id="7477c-176">The type of quota increase depends on the pool allocation mode of your Batch account.</span></span>

### <a name="increase-a-batch-cores-quota"></a><span data-ttu-id="7477c-177">Een Batch kernen quotum verhogen</span><span class="sxs-lookup"><span data-stu-id="7477c-177">Increase a Batch cores quota</span></span> 

<span data-ttu-id="7477c-178">Als uw Batch-account is gemaakt in **Batch-service** modus, voert u deze stappen om aan te vragen van een Batch kernen quotum verhogen:</span><span class="sxs-lookup"><span data-stu-id="7477c-178">If your Batch account was created in **Batch service** mode, follow these steps to request a Batch cores quota increase:</span></span>

1. <span data-ttu-id="7477c-179">Selecteer de **Help + ondersteuning** tegel op uw portal-dashboard of een vraagteken (**?**) in de rechterbovenhoek van de portal.</span><span class="sxs-lookup"><span data-stu-id="7477c-179">Select the **Help + support** tile on your portal dashboard, or the question mark (**?**) in the upper-right corner of the portal.</span></span>
2. <span data-ttu-id="7477c-180">Selecteer **nieuw ondersteuningsverzoek** > **basisbeginselen**.</span><span class="sxs-lookup"><span data-stu-id="7477c-180">Select **New support request** > **Basics**.</span></span>
3. <span data-ttu-id="7477c-181">Op de **basisbeginselen** blade:</span><span class="sxs-lookup"><span data-stu-id="7477c-181">On the **Basics** blade:</span></span>
   
    <span data-ttu-id="7477c-182">a.</span><span class="sxs-lookup"><span data-stu-id="7477c-182">a.</span></span> <span data-ttu-id="7477c-183">**Type probleem** > **quotum**</span><span class="sxs-lookup"><span data-stu-id="7477c-183">**Issue Type** > **Quota**</span></span>
   
    <span data-ttu-id="7477c-184">b.</span><span class="sxs-lookup"><span data-stu-id="7477c-184">b.</span></span> <span data-ttu-id="7477c-185">Selecteer uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7477c-185">Select your subscription.</span></span>
   
    <span data-ttu-id="7477c-186">c.</span><span class="sxs-lookup"><span data-stu-id="7477c-186">c.</span></span> <span data-ttu-id="7477c-187">**Quotumtype** > **Batch**</span><span class="sxs-lookup"><span data-stu-id="7477c-187">**Quota type** > **Batch**</span></span>
   
    <span data-ttu-id="7477c-188">d.</span><span class="sxs-lookup"><span data-stu-id="7477c-188">d.</span></span> <span data-ttu-id="7477c-189">**Ondersteuningsplan** > **quotum support - opgenomen**</span><span class="sxs-lookup"><span data-stu-id="7477c-189">**Support plan** > **Quota support - Included**</span></span>
   
    <span data-ttu-id="7477c-190">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7477c-190">Click **Next**.</span></span>
4. <span data-ttu-id="7477c-191">Op de **probleem** blade:</span><span class="sxs-lookup"><span data-stu-id="7477c-191">On the **Problem** blade:</span></span>
   
    <span data-ttu-id="7477c-192">a.</span><span class="sxs-lookup"><span data-stu-id="7477c-192">a.</span></span> <span data-ttu-id="7477c-193">Selecteer een **ernst** volgens uw [bedrijfsimpact][support_sev].</span><span class="sxs-lookup"><span data-stu-id="7477c-193">Select a **Severity** according to your [business impact][support_sev].</span></span>
   
    <span data-ttu-id="7477c-194">b.</span><span class="sxs-lookup"><span data-stu-id="7477c-194">b.</span></span> <span data-ttu-id="7477c-195">In **Details**, geef elke quota die u wilt wijzigen, de Batch-accountnaam en de nieuwe limiet.</span><span class="sxs-lookup"><span data-stu-id="7477c-195">In **Details**, specify each quota you want to change, the Batch account name, and the new limit.</span></span>
   
    <span data-ttu-id="7477c-196">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7477c-196">Click **Next**.</span></span>
5. <span data-ttu-id="7477c-197">Op de **contactgegevens** blade:</span><span class="sxs-lookup"><span data-stu-id="7477c-197">On the **Contact information** blade:</span></span>
   
    <span data-ttu-id="7477c-198">a.</span><span class="sxs-lookup"><span data-stu-id="7477c-198">a.</span></span> <span data-ttu-id="7477c-199">Selecteer een **voorkeur contactmethode**.</span><span class="sxs-lookup"><span data-stu-id="7477c-199">Select a **Preferred contact method**.</span></span>
   
    <span data-ttu-id="7477c-200">b.</span><span class="sxs-lookup"><span data-stu-id="7477c-200">b.</span></span> <span data-ttu-id="7477c-201">Controleer en voer de vereiste contact op met details.</span><span class="sxs-lookup"><span data-stu-id="7477c-201">Verify and enter the required contact details.</span></span>
   
    <span data-ttu-id="7477c-202">Klik op **Maken** om het ondersteuningsverzoek in te dienen.</span><span class="sxs-lookup"><span data-stu-id="7477c-202">Click **Create** to submit the support request.</span></span>

<span data-ttu-id="7477c-203">Nadat u uw ondersteuningsaanvraag hebt ingediend, ondersteuning van Azure contact met u op.</span><span class="sxs-lookup"><span data-stu-id="7477c-203">Once you've submitted your support request, Azure support will contact you.</span></span> <span data-ttu-id="7477c-204">Let op het voltooien van de aanvraag kan maximaal 2 werkdagen duren.</span><span class="sxs-lookup"><span data-stu-id="7477c-204">Note that completing the request can take up to 2 business days.</span></span>

### <a name="increase-a-subscription-cores-quota"></a><span data-ttu-id="7477c-205">Een abonnement kernen quotum verhogen</span><span class="sxs-lookup"><span data-stu-id="7477c-205">Increase a subscription cores quota</span></span>

<span data-ttu-id="7477c-206">Als uw Batch-account is gemaakt in **gebruikerabonnement** modus en u moet extra regionale of VM-familie kernen, de aanvraag een quotum verhogen in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="7477c-206">If your Batch account was created in **user subscription** mode and you need additional regional or VM family cores, request a quota increase in your subscription.</span></span> <span data-ttu-id="7477c-207">Zie voor stappen [kerngeheugenquotum voor Resource Manager verhogen aanvragen](../azure-supportability/resource-manager-core-quotas-request.md).</span><span class="sxs-lookup"><span data-stu-id="7477c-207">For steps, see [Resource Manager core quota increase requests](../azure-supportability/resource-manager-core-quotas-request.md).</span></span>



## <a name="related-topics"></a><span data-ttu-id="7477c-208">Verwante onderwerpen</span><span class="sxs-lookup"><span data-stu-id="7477c-208">Related topics</span></span>
* [<span data-ttu-id="7477c-209">Een Azure Batch-account maken met de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="7477c-209">Create an Azure Batch account using the Azure portal</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="7477c-210">Overzicht van Azure Batch-functies</span><span class="sxs-lookup"><span data-stu-id="7477c-210">Azure Batch feature overview</span></span>](batch-api-basics.md)
* [<span data-ttu-id="7477c-211">Azure-abonnement en Servicelimieten, quota's en beperkingen</span><span class="sxs-lookup"><span data-stu-id="7477c-211">Azure subscription and service limits, quotas, and constraints</span></span>](../azure-subscription-service-limits.md)

[portal]: https://portal.azure.com
[portal_classic_increase]: https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/
[support_sev]: http://aka.ms/supportseverity

[account_quotas]: ./media/batch-quota-limit/accountquota_portal.PNG

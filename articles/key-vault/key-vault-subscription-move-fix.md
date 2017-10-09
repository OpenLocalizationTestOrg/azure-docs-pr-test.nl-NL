---
title: aaaChange hello sleutelkluis tenant-ID nadat een abonnement hebt verplaatst | Microsoft Docs
description: Meer informatie over hoe tooswitch hello tenant-ID voor een sleutelkluis nadat een abonnement is verplaatst tooa andere tenant
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="112c4-103">De tenant-ID van de Key Vault wijzigen na een verplaatsing van een abonnement</span><span class="sxs-lookup"><span data-stu-id="112c4-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="112c4-104">V: Mijn abonnement is verplaatst van de tenant A tootenant B. Hoe ik Hallo tenant-ID voor mijn bestaande sleutelkluis wijzigen en juiste ACL's ingesteld voor principals in B-tenant?</span><span class="sxs-lookup"><span data-stu-id="112c4-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="112c4-105">Wanneer u een nieuwe sleutelkluis in een abonnement maakt, is het automatisch gebonden toohello standaard Azure Active Directory-tenant-ID voor dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="112c4-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="112c4-106">Alle toegang beleid vermeldingen zijn ook gebonden toothis tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="112c4-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="112c4-107">Wanneer u uw Azure-abonnement hebt verplaatst van tenant een tootenant B, uw bestaande sleutel kluizen zijn niet toegankelijk door Hallo-principals (gebruikers en toepassingen) in de tenant B. toofix dit probleem, moet u:</span><span class="sxs-lookup"><span data-stu-id="112c4-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="112c4-108">Hallo tenant-ID die is gekoppeld aan alle bestaande sleutelkluizen in dit abonnement tootenant B. wijzigen</span><span class="sxs-lookup"><span data-stu-id="112c4-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="112c4-109">Alle bestaande vermeldingen van het toegangsbeleid te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="112c4-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="112c4-110">Nieuwe vermeldingen van het toegangsbeleid toe te voegen die zijn gekoppeld aan tenant B.</span><span class="sxs-lookup"><span data-stu-id="112c4-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="112c4-111">Bijvoorbeeld, als er sleutelkluis 'myvault' in een abonnement dat is verplaatst van de tenant A tootenant B, hier van hoe toochange hello tenant-ID voor deze sleutelkluis en verwijderen van toegangsbeleid oude.</span><span class="sxs-lookup"><span data-stu-id="112c4-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="112c4-112">Omdat deze kluis in een tenant voordat Hallo verplaatsen is, de oorspronkelijke waarde van Hallo **$vault. Properties.TenantId** tenant A, wordt tijdens **(Get-AzureRmContext). Tenant.TenantId** is tenant B.</span><span class="sxs-lookup"><span data-stu-id="112c4-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="112c4-113">Nu dat uw kluis gekoppeld aan de juiste tenant-ID Hallo is en oude toegang beleid vermeldingen worden verwijderd, stelt u nieuwe toegang beleid vermeldingen met [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="112c4-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="112c4-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="112c4-114">Next steps</span></span>
<span data-ttu-id="112c4-115">Als u vragen over Azure Sleutelkluis hebt, gaat u naar Hallo [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="112c4-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>


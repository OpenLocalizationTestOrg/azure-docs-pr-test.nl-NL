---
title: De tenant-ID van de Key Vault wijzigen na een verplaatsing van een abonnement | Microsoft Docs
description: Meer informatie over het overschakelen op een ander tenant-ID voor een Key Vault nadat een abonnement is verplaatst naar een andere tenant
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
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="d0dc3-103">De tenant-ID van de Key Vault wijzigen na een verplaatsing van een abonnement</span><span class="sxs-lookup"><span data-stu-id="d0dc3-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="d0dc3-104">V: Mijn abonnement is van tenant A verplaatst naar tenant B. Hoe wijzig ik de tenant-ID voor mijn bestaande Key Vault en stel ik de juiste ACL's in voor principals in tenant B?</span><span class="sxs-lookup"><span data-stu-id="d0dc3-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="d0dc3-105">Wanneer u een nieuwe Key Vault maakt in een abonnement, is het automatisch gekoppeld aan de tenant-ID van Azure Active Directory voor dit abonnement.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="d0dc3-106">Alle vermeldingen van het toegangsbeleid zijn ook gekoppeld aan deze tenant-ID.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="d0dc3-107">Wanneer u uw Azure-abonnement van tenant A naar tenant B verplaatst, hebben de principals (gebruikers en toepassingen) geen toegang tot de bestaande Key Vaults in tenant B. U kunt dit probleem oplossen door:</span><span class="sxs-lookup"><span data-stu-id="d0dc3-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="d0dc3-108">De tenant-ID die is gekoppeld aan alle bestaande Key Vaults in dit abonnement te wijzigen in tenant B.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="d0dc3-109">Alle bestaande vermeldingen van het toegangsbeleid te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="d0dc3-110">Nieuwe vermeldingen van het toegangsbeleid toe te voegen die zijn gekoppeld aan tenant B.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="d0dc3-111">Als u bijvoorbeeld Kay Vault 'mijnvault' hebt in een abonnement dat is verplaatst van tenant A naar B, kunt u de tenant-ID voor deze Key Vault als volgt wijzigen en het oude toegangsbeleid verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="d0dc3-112">Omdat deze Vault zich in tenant A bevond voor de wijziging, is de oorspronkelijke waarde van **$vault. Properties.TenantId** tenant A en is **(Get-AzureRmContext). Tenant.TenantId** tenant B.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="d0dc3-113">Nu uw Vault is gekoppeld aan de juiste tenant-ID en de oude vermeldingen van het toegangsbeleid zijn verwijderd, kunt u nieuwe vermeldingen van het toegangsbeleid instellen met [Set AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0dc3-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d0dc3-114">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d0dc3-114">Next steps</span></span>
<span data-ttu-id="d0dc3-115">Ga naar de [forums van Azure Key Vault](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault) als u vragen hebt over Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="d0dc3-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>


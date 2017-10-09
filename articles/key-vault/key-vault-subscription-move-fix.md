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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>De tenant-ID van de Key Vault wijzigen na een verplaatsing van een abonnement
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>V: Mijn abonnement is verplaatst van de tenant A tootenant B. Hoe ik Hallo tenant-ID voor mijn bestaande sleutelkluis wijzigen en juiste ACL's ingesteld voor principals in B-tenant?
Wanneer u een nieuwe sleutelkluis in een abonnement maakt, is het automatisch gebonden toohello standaard Azure Active Directory-tenant-ID voor dat abonnement. Alle toegang beleid vermeldingen zijn ook gebonden toothis tenant-ID. Wanneer u uw Azure-abonnement hebt verplaatst van tenant een tootenant B, uw bestaande sleutel kluizen zijn niet toegankelijk door Hallo-principals (gebruikers en toepassingen) in de tenant B. toofix dit probleem, moet u:

* Hallo tenant-ID die is gekoppeld aan alle bestaande sleutelkluizen in dit abonnement tootenant B. wijzigen
* Alle bestaande vermeldingen van het toegangsbeleid te verwijderen.
* Nieuwe vermeldingen van het toegangsbeleid toe te voegen die zijn gekoppeld aan tenant B.

Bijvoorbeeld, als er sleutelkluis 'myvault' in een abonnement dat is verplaatst van de tenant A tootenant B, hier van hoe toochange hello tenant-ID voor deze sleutelkluis en verwijderen van toegangsbeleid oude.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Omdat deze kluis in een tenant voordat Hallo verplaatsen is, de oorspronkelijke waarde van Hallo **$vault. Properties.TenantId** tenant A, wordt tijdens **(Get-AzureRmContext). Tenant.TenantId** is tenant B.

Nu dat uw kluis gekoppeld aan de juiste tenant-ID Hallo is en oude toegang beleid vermeldingen worden verwijderd, stelt u nieuwe toegang beleid vermeldingen met [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Volgende stappen
Als u vragen over Azure Sleutelkluis hebt, gaat u naar Hallo [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).


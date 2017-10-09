---
title: aaaGrant machtiging toomany toepassingen tooaccess een Azure sleutelkluis | Microsoft Docs
description: Meer informatie over hoe toogrant machtiging toomany toepassingen tooaccess een sleutel-kluis
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Een sleutelkluis voor machtiging toomany toepassingen tooaccess verlenen

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>V: ik heb meerdere (meer dan 16) toepassingen die tooaccess een sleutelkluis moeten. Omdat Sleutelkluis mag uit maximaal 16 vermeldingen voor toegangsbeheer, hoe kan ik bereikt die?

Beleid voor toegangsbeheer Sleutelkluis biedt alleen ondersteuning voor 16 vermeldingen. U kunt echter een Azure Active Directory-beveiligingsgroep maken. Voeg alle Hallo service-principals toothis beveiligingsgroep die is gekoppeld en Verleen toegang toothis beveiliging groep tooKey kluis.

Hier volgen Hallo-vereisten:
* [Installeer Azure Active Directory V2 PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Installeer Azure PowerShell](/powershell/azure/overview).
* toorun hello volgende opdrachten, moet u machtigingen toocreate/bewerken groepen in hello Azure Active Directory-tenant. Als u geen machtigingen hebt, moet u mogelijk toocontact uw Azure Active Directory-beheerder.

Voer nu Hallo volgende opdrachten in PowerShell.

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

Als u een andere set machtigingen tooa groep van toepassingen toogrant moet, maakt u een afzonderlijke Azure Active Directory-beveiligingsgroep voor dergelijke toepassingen.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over het te[beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).

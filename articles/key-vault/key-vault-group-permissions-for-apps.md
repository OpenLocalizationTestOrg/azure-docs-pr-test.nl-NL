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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="aee81-103">Een sleutelkluis voor machtiging toomany toepassingen tooaccess verlenen</span><span class="sxs-lookup"><span data-stu-id="aee81-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="aee81-104">V: ik heb meerdere (meer dan 16) toepassingen die tooaccess een sleutelkluis moeten.</span><span class="sxs-lookup"><span data-stu-id="aee81-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="aee81-105">Omdat Sleutelkluis mag uit maximaal 16 vermeldingen voor toegangsbeheer, hoe kan ik bereikt die?</span><span class="sxs-lookup"><span data-stu-id="aee81-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="aee81-106">Beleid voor toegangsbeheer Sleutelkluis biedt alleen ondersteuning voor 16 vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="aee81-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="aee81-107">U kunt echter een Azure Active Directory-beveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="aee81-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="aee81-108">Voeg alle Hallo service-principals toothis beveiligingsgroep die is gekoppeld en Verleen toegang toothis beveiliging groep tooKey kluis.</span><span class="sxs-lookup"><span data-stu-id="aee81-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="aee81-109">Hier volgen Hallo-vereisten:</span><span class="sxs-lookup"><span data-stu-id="aee81-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="aee81-110">[Installeer Azure Active Directory V2 PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="aee81-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="aee81-111">[Installeer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aee81-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="aee81-112">toorun hello volgende opdrachten, moet u machtigingen toocreate/bewerken groepen in hello Azure Active Directory-tenant.</span><span class="sxs-lookup"><span data-stu-id="aee81-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="aee81-113">Als u geen machtigingen hebt, moet u mogelijk toocontact uw Azure Active Directory-beheerder.</span><span class="sxs-lookup"><span data-stu-id="aee81-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="aee81-114">Voer nu Hallo volgende opdrachten in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aee81-114">Now run hello following commands in PowerShell.</span></span>

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

<span data-ttu-id="aee81-115">Als u een andere set machtigingen tooa groep van toepassingen toogrant moet, maakt u een afzonderlijke Azure Active Directory-beveiligingsgroep voor dergelijke toepassingen.</span><span class="sxs-lookup"><span data-stu-id="aee81-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aee81-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aee81-116">Next steps</span></span>

<span data-ttu-id="aee81-117">Meer informatie over het te[beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="aee81-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

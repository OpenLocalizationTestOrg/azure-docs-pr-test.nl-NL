---
title: Machtiging verlenen om te veel toepassingen voor toegang tot een Azure sleutelkluis | Microsoft Docs
description: Meer informatie over het machtiging verlenen om te veel toepassingen voor toegang tot een sleutelkluis
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
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="2a8d3-103">Machtiging verlenen om te veel toepassingen voor toegang tot een sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="2a8d3-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="2a8d3-104">V: ik heb meerdere (meer dan 16) toepassingen die toegang moeten krijgen tot een sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="2a8d3-105">Omdat Sleutelkluis mag uit maximaal 16 vermeldingen voor toegangsbeheer, hoe kan ik bereikt die?</span><span class="sxs-lookup"><span data-stu-id="2a8d3-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="2a8d3-106">Beleid voor toegangsbeheer Sleutelkluis biedt alleen ondersteuning voor 16 vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="2a8d3-107">U kunt echter een Azure Active Directory-beveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="2a8d3-108">Alle gekoppelde service-principals toevoegen aan deze beveiligingsgroep en vervolgens toegang verlenen aan deze beveiligingsgroep voor Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="2a8d3-109">Hier volgen de vereisten:</span><span class="sxs-lookup"><span data-stu-id="2a8d3-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="2a8d3-110">[Installeer Azure Active Directory V2 PowerShell-module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="2a8d3-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="2a8d3-111">[Installeer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2a8d3-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="2a8d3-112">Als u wilt de volgende opdrachten uitvoeren, moet u machtigingen voor groepen in de Azure Active Directory-tenant maken/bewerken.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="2a8d3-113">Als u geen machtigingen hebt, moet u mogelijk contact opnemen met uw Azure Active Directory-beheerder.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="2a8d3-114">Voer nu de volgende opdrachten in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="2a8d3-115">Als u een andere set machtigingen aan een groep van toepassingen te verlenen moet, maakt u een afzonderlijke Azure Active Directory-beveiligingsgroep voor dergelijke toepassingen.</span><span class="sxs-lookup"><span data-stu-id="2a8d3-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2a8d3-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2a8d3-116">Next steps</span></span>

<span data-ttu-id="2a8d3-117">Meer informatie over het [beveiligen van uw sleutelkluis](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="2a8d3-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>

---
title: aaaUse PowerShell toocreate een Azure AD app tooaccess hello Azure Media Services-API | Microsoft Docs
description: Meer informatie over hoe toouse PowerShell toocreate een app met Azure Active Directory (Azure AD) en stel tooaccess hello Azure Media Services-API.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 1a8b4a53ad10b559f6ee4242b95c5bd15ee8e903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a>Gebruik PowerShell toocreate een Azure AD app toouse Hello Azure Media Services-API

Meer informatie over hoe een PowerShell toouse toocreate script een Azure Active Directory (Azure AD)-toepassing en service-principal tooaccess Azure Media Services-bronnen.  

## <a name="prerequisites"></a>Vereisten

- Een Azure-account. Als u geen account hebt, beginnen met een [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/). 
- Een Media Services-account. Zie voor meer informatie [een Azure Media Services-account maken in Azure-portal Hallo](media-services-portal-create-account.md).
- Azure PowerShell-versie 0.8.8 of een latere versie. Zie voor meer informatie [hoe toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
- Azure Resource Manager-cmdlets.  

## <a name="create-an-azure-ad-app-by-using-powershell"></a>Een Azure AD-app maken met behulp van PowerShell  

```powershell
Login-AzureRmAccount
Import-Module AzureRM.Resources
Set-AzureRmContext -SubscriptionId $SubscriptionId
$ServicePrincipal = New-AzureRMADServicePrincipal -DisplayName $ApplicationDisplayName -Password $Password

Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id 
$NewRole = $null
$Scope = "/subscriptions/your subscription id/resourceGroups/userresourcegroup/providers/microsoft.media/mediaservices/your media account"

$Retries = 0;While ($NewRole -eq $null -and $Retries -le 6)
{
    # Sleep here for a few seconds tooallow hello service principal application toobecome active (usually, it will take only a couple of seconds)
    Sleep 15
    New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $ServicePrincipal.ApplicationId -Scope $Scope | Write-Verbose -ErrorAction SilentlyContinue
    $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $ServicePrincipal.ApplicationId -ErrorAction SilentlyContinue
    $Retries++;
}
```

Zie voor meer informatie Hallo artikelen te volgen:

- [Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [Toegangsbeheer op basis van rollen beheren met behulp van Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
- [Hoe toomanually daemon apps configureren met behulp van certificaten](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a>Volgende stappen

Aan de slag met [tooyour account uploaden van bestanden](media-services-portal-upload-files.md).

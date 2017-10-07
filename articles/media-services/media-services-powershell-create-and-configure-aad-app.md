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
# <a name="use-powershell-toocreate-an-azure-ad-app-toouse-with-hello-azure-media-services-api"></a><span data-ttu-id="4b5a7-103">Gebruik PowerShell toocreate een Azure AD app toouse Hello Azure Media Services-API</span><span class="sxs-lookup"><span data-stu-id="4b5a7-103">Use PowerShell toocreate an Azure AD app toouse with hello Azure Media Services API</span></span>

<span data-ttu-id="4b5a7-104">Meer informatie over hoe een PowerShell toouse toocreate script een Azure Active Directory (Azure AD)-toepassing en service-principal tooaccess Azure Media Services-bronnen.</span><span class="sxs-lookup"><span data-stu-id="4b5a7-104">Learn how toouse a PowerShell script toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="4b5a7-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4b5a7-105">Prerequisites</span></span>

- <span data-ttu-id="4b5a7-106">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="4b5a7-106">An Azure account.</span></span> <span data-ttu-id="4b5a7-107">Als u geen account hebt, beginnen met een [gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4b5a7-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="4b5a7-108">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="4b5a7-108">A Media Services account.</span></span> <span data-ttu-id="4b5a7-109">Zie voor meer informatie [een Azure Media Services-account maken in Azure-portal Hallo](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="4b5a7-109">For more information, see [Create an Azure Media Services account in hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="4b5a7-110">Azure PowerShell-versie 0.8.8 of een latere versie.</span><span class="sxs-lookup"><span data-stu-id="4b5a7-110">Azure PowerShell version 0.8.8 or a later version.</span></span> <span data-ttu-id="4b5a7-111">Zie voor meer informatie [hoe toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b5a7-111">For more information, see [How toouse Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span></span>
- <span data-ttu-id="4b5a7-112">Azure Resource Manager-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="4b5a7-112">Azure Resource Manager cmdlets.</span></span>  

## <a name="create-an-azure-ad-app-by-using-powershell"></a><span data-ttu-id="4b5a7-113">Een Azure AD-app maken met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b5a7-113">Create an Azure AD app by using PowerShell</span></span>  

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

<span data-ttu-id="4b5a7-114">Zie voor meer informatie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b5a7-114">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="4b5a7-115">Een service principal tooaccess-resources voor Azure PowerShell toocreate gebruiken</span><span class="sxs-lookup"><span data-stu-id="4b5a7-115">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](../azure-resource-manager/resource-group-authenticate-service-principal.md)
- [<span data-ttu-id="4b5a7-116">Toegangsbeheer op basis van rollen beheren met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b5a7-116">Manage Role-Based Access Control by using Azure PowerShell</span></span>](../active-directory/role-based-access-control-manage-access-powershell.md)
- [<span data-ttu-id="4b5a7-117">Hoe toomanually daemon apps configureren met behulp van certificaten</span><span class="sxs-lookup"><span data-stu-id="4b5a7-117">How toomanually configure daemon apps by using certificates</span></span>](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md#add-the-certificate-as-a-key-for-the-todolistdaemonwithcert-application-in-azure-ad)

## <a name="next-steps"></a><span data-ttu-id="4b5a7-118">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4b5a7-118">Next steps</span></span>

<span data-ttu-id="4b5a7-119">Aan de slag met [tooyour account uploaden van bestanden](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="4b5a7-119">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>

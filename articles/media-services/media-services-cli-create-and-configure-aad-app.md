---
title: aaaUse CLI 2.0 toocreate een Azure AD-app en configureer deze tooaccess Azure Media Services-API | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe toouse CLI 2.0 toocreate een Azure AD-app en configureer deze tooaccess Azure Media Services-API.
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
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="957f6-103">Gebruik CLI 2.0 toocreate een AAD-app en configureer deze tooaccess Azure Media Services-API</span><span class="sxs-lookup"><span data-stu-id="957f6-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="957f6-104">Dit onderwerp leest u hoe toouse CLI 2.0 toocreate een Azure Active Directory (Azure AD)-toepassing en service-principal tooaccess Azure Media Services-bronnen.</span><span class="sxs-lookup"><span data-stu-id="957f6-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="957f6-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="957f6-105">Prerequisites</span></span>

- <span data-ttu-id="957f6-106">Een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="957f6-106">An Azure account.</span></span> <span data-ttu-id="957f6-107">Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="957f6-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="957f6-108">Een Media Services-account.</span><span class="sxs-lookup"><span data-stu-id="957f6-108">A Media Services account.</span></span> <span data-ttu-id="957f6-109">Zie voor meer informatie [een Azure Media Services-account maken met Azure-portal Hallo](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="957f6-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="957f6-110">Hello Azure Cloud Shell gebruiken</span><span class="sxs-lookup"><span data-stu-id="957f6-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="957f6-111">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="957f6-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="957f6-112">Start Hallo Cloud-Shell uit Hallo bovenste navigatievenster van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="957f6-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="957f6-114">Zie voor meer informatie [overzicht van Azure Cloud Shell](../cloud-shell/overview.md).</span><span class="sxs-lookup"><span data-stu-id="957f6-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="957f6-115">Een Azure AD-app maken en configureren van account voor toegang tot toohello media met CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="957f6-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="957f6-116">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="957f6-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="957f6-117">In dit voorbeeld Hallo **bereik** is volledig bronpad Hallo voor Hallo media services-account.</span><span class="sxs-lookup"><span data-stu-id="957f6-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="957f6-118">Hallo echter **bereik** kan zijn op elk niveau.</span><span class="sxs-lookup"><span data-stu-id="957f6-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="957f6-119">Bijvoorbeeld, wordt een van de volgende niveaus Hallo:</span><span class="sxs-lookup"><span data-stu-id="957f6-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="957f6-120">Hallo **abonnement** niveau.</span><span class="sxs-lookup"><span data-stu-id="957f6-120">hello **subscription** level.</span></span>
* <span data-ttu-id="957f6-121">Hallo **resourcegroep** niveau.</span><span class="sxs-lookup"><span data-stu-id="957f6-121">hello **resource group** level.</span></span>
* <span data-ttu-id="957f6-122">Hallo **resource** niveau (bijvoorbeeld een account Media).</span><span class="sxs-lookup"><span data-stu-id="957f6-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="957f6-123">Zie voor meer informatie [een Azure-service-principal maken met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span><span class="sxs-lookup"><span data-stu-id="957f6-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="957f6-124">Zie ook [Manage Role-Based toegangsbeheer Hello Azure-opdrachtregelinterface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="957f6-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="957f6-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="957f6-125">Next steps</span></span>

<span data-ttu-id="957f6-126">Aan de slag met [tooyour account uploaden van bestanden](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="957f6-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>

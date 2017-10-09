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
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a>Gebruik CLI 2.0 toocreate een AAD-app en configureer deze tooaccess Azure Media Services-API

Dit onderwerp leest u hoe toouse CLI 2.0 toocreate een Azure Active Directory (Azure AD)-toepassing en service-principal tooaccess Azure Media Services-bronnen. 

## <a name="prerequisites"></a>Vereisten

- Een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
- Een Media Services-account. Zie voor meer informatie [een Azure Media Services-account maken met Azure-portal Hallo](media-services-portal-create-account.md).

## <a name="use-hello-azure-cloud-shell"></a>Hello Azure Cloud Shell gebruiken

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Start Hallo Cloud-Shell uit Hallo bovenste navigatievenster van Hallo-portal.

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

Zie voor meer informatie [overzicht van Azure Cloud Shell](../cloud-shell/overview.md).

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a>Een Azure AD-app maken en configureren van account voor toegang tot toohello media met CLI 2.0
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

Bijvoorbeeld:

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

In dit voorbeeld Hallo **bereik** is volledig bronpad Hallo voor Hallo media services-account. Hallo echter **bereik** kan zijn op elk niveau.

Bijvoorbeeld, wordt een van de volgende niveaus Hallo:
 
* Hallo **abonnement** niveau.
* Hallo **resourcegroep** niveau.
* Hallo **resource** niveau (bijvoorbeeld een account Media).

Zie voor meer informatie [een Azure-service-principal maken met Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)

Zie ook [Manage Role-Based toegangsbeheer Hello Azure-opdrachtregelinterface](../active-directory/role-based-access-control-manage-access-azure-cli.md). 

## <a name="next-steps"></a>Volgende stappen

Aan de slag met [tooyour account uploaden van bestanden](media-services-portal-upload-files.md).

---
title: een Azure Media Services-account met hello Azure-portal aaaCreate | Microsoft Docs
description: Deze zelfstudie wordt u begeleid Hallo stappen voor het maken van een Azure Media Services-account met hello Azure-portal.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: c551e158-aad6-47b4-931e-b46260b3ee4c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: juliako
ms.openlocfilehash: fdad93d5d470fc08380670ec0f6c2d33468b1492
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-media-services-account-using-hello-azure-portal"></a>Een Azure Media Services-account maken met hello Azure-portal
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-create-account.md)
> * [PowerShell](media-services-manage-with-powershell.md)
> * [REST](https://docs.microsoft.com/rest/api/media/mediaservice)
> 
> [!NOTE]
> toocomplete in deze zelfstudie, moet u een Azure-account. Zie [Gratis proefversie van Azure](https://azure.microsoft.com/pricing/free-trial/) voor meer informatie. 
> 
> 

Hello Azure-portal biedt een manier tooquickly account maken voor een Azure Media Services (AMS). U kunt uw account tooaccess Media Services die u toostore inschakelen, versleutelen, coderen, beheren en streamen van mediainhoud in Azure. Tijdens Hallo maken van een Media Services-account, u ook een gekoppeld opslagaccount maken (of gebruik een bestaande) in Hallo dezelfde geografische regio als Hallo Media Services-account.

Dit artikel worden enkele algemene concepten uitgelegd en ziet u hoe u een Media Services toocreate administratief Hello Azure-portal.

## <a name="concepts"></a>Concepten
Voor toegang tot Media Services zijn twee gekoppelde accounts vereist: 

* Een Media Services-account. Uw account biedt u toegang tot tooa set van cloud-gebaseerde Media Services die beschikbaar zijn in Azure. Er wordt geen echte media-inhoud opgeslagen in een Media Services-account. In plaats daarvan worden metagegevens over Hallo media-inhoud en taken voor de verwerking media opgeslagen in uw account. Tijdens het Hallo die u Hallo-account maakt, moet u een beschikbare Media Services-regio selecteren. Hallo regio die u selecteert, is een datacenter waarin Hallo media en metagegevensrecords voor uw account wordt opgeslagen.
  
* Een Azure Storage-account. Storage-accounts moeten zich bevinden in Hallo dezelfde geografische regio als Hallo Media Services-account. Wanneer u een Media Services-account maakt, kunt u kiezen een bestaand opslagaccount in Hallo dezelfde regio, of u een nieuw opslagaccount in Hallo kunt maken dezelfde regio. Als u een Media Services-account verwijdert, worden de Hallo blobs in uw gerelateerde opslagaccount niet verwijderd.

> [!NOTE]
> Zie [Scenarios and availability of Media Services features across datacenters](scenarios-and-availability.md#availability) (Scenario's en beschikbaarheid van Media Services-functies via datacenters) voor meer informatie over de beschikbaarheid van Azure Media Services-functies in verschillende regio's.

## <a name="create-an-ams-account"></a>Een AMS-account maken
Hallo stappen in deze sectie tonen hoe toocreate een AMS-account.

1. Aanmelden op Hallo [Azure-portal](https://portal.azure.com/).
2. Klik op **+Nieuw** > **Web en mobiel** > **Media Services**.
   
    ![Media Services-account maken](./media/media-services-create-account/media-services-new1.png)
3. Voer bij **MEDIA SERVICES-ACCOUNT MAKEN** de vereiste waarden in.
   
    ![Media Services-account maken](./media/media-services-create-account/media-services-new3.png)
   
   1. In **accountnaam**, voer de naam Hallo van Hallo nieuwe AMS-account. De naam van een Media Services-account is alle kleine letters of cijfers zonder spaties en 3 too24 tekens lang is.
   2. Selecteer in abonnement tussen Hallo verschillende Azure-abonnementen waartoe u toegang hebt.
   3. In **resourcegroep**, selecteer Hallo nieuwe of bestaande resourcegroep.  Een resourcegroep is een verzameling resources met dezelfde levenscyclus, dezelfde machtigingen en hetzelfde beleid. Klik [hier](../azure-resource-manager/resource-group-overview.md#resource-groups) voor meer informatie.
   4. In **locatie**, selecteer Hallo geografische regio die wordt gebruikt toostore Hallo media en metagegevensrecords voor uw Media Services-account. Dit gebied wordt gebruikt tooprocess en media streamen. Alleen Hallo beschikbare Media Services-regio's worden weergegeven in Hallo vervolgkeuzelijst. 
   5. In **Opslagaccount**, selecteert u een storage account tooprovide blob storage van Hallo media-inhoud vanaf uw Media Services-account. U kunt een bestaand opslagaccount selecteren in Hallo dezelfde geografische regio als uw Media Services-account, of u kunt een opslagaccount maken. Een nieuw opslagaccount gemaakt in Hallo dezelfde regio. Hallo-regels voor het opslagaccount namen zijn Hallo dezelfde als voor Media Services-accounts.
      
       Klik [hier](../storage/common/storage-introduction.md) voor meer informatie over opslag.
   6. Selecteer **pincode toodashboard** toosee Hallo voortgang van de implementatie van Hallo-account.
4. Klik op **maken** onderin Hallo Hallo vorm.
   
    Zodra het Hallo-account is gemaakt, geladen overzichtspagina. In Hallo streaming-eindpunt tabel Hallo account heeft een standaard streaming-eindpunt in Hallo **gestopt** status. 

    >[!NOTE]
    >Wanneer uw AMS-account wordt gemaakt een **standaard** tooyour account streaming-eindpunt is toegevoegd in Hallo **gestopt** status. uw inhoud en los het voordeel van dynamische pakketten en dynamische versleuteling streaming toostart Hallo streaming-eindpunt van waaruit u wilt toostream inhoud heeft toobe in Hallo **met** status. 
   
## <a name="toomanage-your-ams-account"></a>toomanage uw AMS-account

toomanage uw AMS-account (bijvoorbeeld verbinding maken via een programma met toohello AMS API, video's uploaden, assets coderen, configureren van beveiliging van inhoud, voortgang taak) Selecteer **instellingen** op Hallo linkerkant van Hallo-portal. Van Hallo **instellingen**, navigeer tooone Hallo beschikbaar bladen (bijvoorbeeld: **API-toegang**, **activa**, **taken**, **Content protection**).


## <a name="next-steps"></a>Volgende stappen

U kunt nu bestanden uploaden naar uw AMS-account. Zie [Bestanden uploaden](media-services-portal-upload-files.md) voor meer informatie.

Als u van plan tooaccess AMS API programmatisch bent, Zie [toegang hello Azure Media Services-API met Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]


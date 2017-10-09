---
title: aaaHow toomigrate tooschema versie 2015-08-01-preview-logic apps | Microsoft Docs
description: U kunt de nieuwste schemaversie van logic apps toohello eenvoudig migreren. Volg deze stappen.
services: logic-apps
documentationcenter: 
author: MSFTMAN
manager: erikre
editor: 
tags: connectors
ms.assetid: 3e177e49-fd69-43e9-9b9b-218abb250c31
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2016
ms.author: deonhe
ms.openlocfilehash: c7b42aaec547eddd28b0c649a3c0625047f9f805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-logic-apps-tooschema-version-2015-08-01-preview"></a><span data-ttu-id="98bdc-104">Hoe toomigrate logic apps tooschema versie 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="98bdc-104">How toomigrate logic apps tooschema version 2015-08-01-preview</span></span>
<span data-ttu-id="98bdc-105">toomove uw bestaande logic apps toohello nieuwe schema, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="98bdc-105">toomove your existing logic apps toohello new schema, do hello following:</span></span>  

1. <span data-ttu-id="98bdc-106">Open uw logische app in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="98bdc-106">Open your logic app in hello Azure portal</span></span>  
2. <span data-ttu-id="98bdc-107">Klik op Schema bijwerken:</span><span class="sxs-lookup"><span data-stu-id="98bdc-107">Click Update Schema:</span></span>
   
   <span data-ttu-id="98bdc-108">![API-pictogram][step1] </span><span class="sxs-lookup"><span data-stu-id="98bdc-108">![API Icon][step1] </span></span>  
   <span data-ttu-id="98bdc-109">Hallo Schema bijwerken pagina weergegeven en bevat een koppeling tooa document dat gedetailleerde informatie over verbeteringen in het nieuwe schema Hallo Hallo: ![API-pictogram][step2]</span><span class="sxs-lookup"><span data-stu-id="98bdc-109">hello Update Schema page displays and provides a link tooa document that provide details on hello improvements in hello new schema: ![API Icon][step2]</span></span>

> [!NOTE]
> <span data-ttu-id="98bdc-110">Wanneer u selecteert **Schema bijwerken**, automatisch Hallo migratiestappen uitgevoerd en krijgt u Hallo code-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="98bdc-110">When you select **Update Schema**, we automatically run hello migration steps and provide hello code output for you.</span></span> <span data-ttu-id="98bdc-111">U kunt deze tooupdate echter uw definitie gebruiken, zorg ervoor dat u goed codering Volg zoals die zijn beschreven in Hallo **Best practices** hieronder.</span><span class="sxs-lookup"><span data-stu-id="98bdc-111">You can use this tooupdate your definition, however, ensure you follow good coding practices such as those outlined in hello **Best practices** section below.</span></span>
> 
> 

## <a name="best-practices-when-migrating-your-logic-apps-toohello-latest-schema-version"></a><span data-ttu-id="98bdc-112">Aanbevolen procedures bij het migreren van de nieuwste schemaversie van Logic apps toohello:</span><span class="sxs-lookup"><span data-stu-id="98bdc-112">Best practices when migrating your Logic apps toohello latest schema version:</span></span>
* <span data-ttu-id="98bdc-113">Kopiëren Hallo gemigreerd script tooa nieuwe Logic App - niet overschrijven Hallo oude pas nadat u hebt uw gemigreerde app testen en bevestigd hello voltooid werkt zoals verwacht.</span><span class="sxs-lookup"><span data-stu-id="98bdc-113">Copy hello migrated script tooa new Logic App - don't overwrite hello old one until you've completed your testing and confirmed hello migrated app works as expected.</span></span>
* <span data-ttu-id="98bdc-114">Uw logische app testen **voordat** u deze in productie neemt</span><span class="sxs-lookup"><span data-stu-id="98bdc-114">Test your Logic app **before** putting in production</span></span>
* <span data-ttu-id="98bdc-115">Nadat de migratie is voltooid, start u het bijwerken van uw logische apps toouse hello [beheerde API's](apis-list.md) waar mogelijk.</span><span class="sxs-lookup"><span data-stu-id="98bdc-115">After migration completes, start updating your Logic apps toouse hello [managed APIs](apis-list.md) where possible.</span></span> <span data-ttu-id="98bdc-116">U kunt bijvoorbeeld starten met het gebruik van de Dropbox v2-versie overal waar u DropBox v1 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="98bdc-116">For example, you can start using Dropbox v2, whereever you are using DropBox v1.</span></span>

## <a name="whats-next"></a><span data-ttu-id="98bdc-117">Volgend onderwerp</span><span class="sxs-lookup"><span data-stu-id="98bdc-117">What's next</span></span>
* [<span data-ttu-id="98bdc-118">Meer informatie over hoe toomanually uw logische apps migreren</span><span class="sxs-lookup"><span data-stu-id="98bdc-118">Learn how toomanually migrate your Logic apps</span></span>](../logic-apps/logic-apps-schema-2015-08-01.md)

<!--Icon references-->
[step1]: ./media/connectors-schema-migration/migrateschema1.png
[step2]: ./media/connectors-schema-migration/migrateschema2.png







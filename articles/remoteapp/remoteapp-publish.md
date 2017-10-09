---
title: aaaPublish een app in Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe toopublish toepassingen en bronnen in Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c7e1a2cd-8e1f-4a33-bd43-8032ec9ac952
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: d7d92187e9ed999ac79554c9bb61f56a8eceeb31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toopublish-an-app-in-remoteapp"></a><span data-ttu-id="81b3f-103">Hoe toopublish een app in RemoteApp</span><span class="sxs-lookup"><span data-stu-id="81b3f-103">How toopublish an app in RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="81b3f-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="81b3f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="81b3f-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="81b3f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="81b3f-106">Nadat u uw RemoteApp-collectie maken, moet u toopublish Hallo apps of resources wilt u toomake beschikbaar voor uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="81b3f-106">After you create your RemoteApp collection, you need toopublish hello apps or resources that you want toomake available for your users.</span></span> <span data-ttu-id="81b3f-107">Hallo sjablooninstallatiekopieën voorzien van uw abonnement alleen enkele apps hebben standaard - uitgegeven tooshare Hallo andere apps, moet u toopublish ze.</span><span class="sxs-lookup"><span data-stu-id="81b3f-107">hello template images provided with your subscription only have a few apps published by default - tooshare hello other apps, you need toopublish them.</span></span>

> [!NOTE]
> <span data-ttu-id="81b3f-108">Moet u een app tooupdate?</span><span class="sxs-lookup"><span data-stu-id="81b3f-108">Do you need tooupdate an app?</span></span> <span data-ttu-id="81b3f-109">U moet te[update Hallo installatiekopie](remoteapp-update.md) eerste.</span><span class="sxs-lookup"><span data-stu-id="81b3f-109">You'll need too[update hello image](remoteapp-update.md) first.</span></span>
> 
> 

<span data-ttu-id="81b3f-110">Op Hallo **Publishing** in Hallo-portal en klik op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="81b3f-110">On hello **Publishing** tab in hello portal, click **Publish**.</span></span> <span data-ttu-id="81b3f-111">Kunt u een app toevoegen van uw sjablooninstallatiekopie **Start** menu of geef Hallo pad toowhere Hallo app op Hallo-sjablooninstallatiekopie is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="81b3f-111">You can either add an app from your template image's **Start** menu or provide hello path toowhere hello app is installed on hello template image.</span></span> <span data-ttu-id="81b3f-112">Als u tooadd uit Hallo **Start** menu Hallo app toopublish in Hallo lijst kiezen.</span><span class="sxs-lookup"><span data-stu-id="81b3f-112">If you choose tooadd from hello **Start** menu, choose hello app toopublish from hello list.</span></span> <span data-ttu-id="81b3f-113">Als u tooprovide Hallo pad toohello app kiest, voer een naam voor het Hallo-app en Hallo pad toohello app.</span><span class="sxs-lookup"><span data-stu-id="81b3f-113">If you choose tooprovide hello path toohello app, enter a name for hello app and hello path toohello app.</span></span> <span data-ttu-id="81b3f-114">Variabelen in Hallo pad - bijvoorbeeld '% systemdrive %' gebruiken in plaats van ' c:\".</span><span class="sxs-lookup"><span data-stu-id="81b3f-114">Use variables in hello path - for example, "%systemdrive%" instead of "c:\".</span></span>

> [!NOTE]
> <span data-ttu-id="81b3f-115">Als u uw app uit Hallo tooadd wilt **Start** menu, moet u toohave *toegevoegd die app-toohello **Start** menu op uw sjablooninstallatiekopie.*</span><span class="sxs-lookup"><span data-stu-id="81b3f-115">If you want tooadd your app from hello **Start** menu, you need toohave *added that app toohello **Start** menu on your template image.*</span></span> <span data-ttu-id="81b3f-116">Anders RemoteApp alleen zien wat *is* op Hallo **Start** menu en u wordt verwarren.</span><span class="sxs-lookup"><span data-stu-id="81b3f-116">Otherwise, RemoteApp will only see what *is* on hello **Start** menu, and you will be confused.</span></span> 
> 
> <span data-ttu-id="81b3f-117">toomake ervoor dat uw app wordt in Hallo **Start** menu, plaatst u het snelkoppelingsbestand - **lnk** - Hallo %systemdrive%\ProgramData\Microsoft\Windows\Start Start\Programma 's map.</span><span class="sxs-lookup"><span data-stu-id="81b3f-117">toomake sure your app is in hello **Start** menu, place a shortcut file - **.lnk** - inside hello %systemdrive%\ProgramData\Microsoft\Windows\Start Menu\Programs folder.</span></span>
> 
> <span data-ttu-id="81b3f-118">Als u bent tooadd Hallo app toohello vergeten **Start** menu tijdens het maken van Hallo-sjabloon, kies tooadd Hallo pad toohello app.</span><span class="sxs-lookup"><span data-stu-id="81b3f-118">If you forgot tooadd hello app toohello **Start** menu when you created hello template, choose tooadd hello path toohello app.</span></span> <span data-ttu-id="81b3f-119">(Of maak deze opnieuw uw sjablooninstallatiekopie, maar dat is erg iets meer werk.)</span><span class="sxs-lookup"><span data-stu-id="81b3f-119">(Or recreate your template image, but that's quite a bit more work.)</span></span>
> 
> 


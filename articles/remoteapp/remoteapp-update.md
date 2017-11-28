---
title: aaaUpdate uw Azure RemoteApp-collectie | Microsoft Docs
description: Meer informatie over hoe tooupdate uw Azure RemoteApp-verzameling
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
editor: 
ms.assetid: e553d432-e581-48fe-b996-c432357eb64a
ms.service: remoteapp
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 849d7abfdfad4dbe6a235d2a28c71f7943eb812c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-a-collection-in-azure-remoteapp"></a><span data-ttu-id="4715f-103">Bijwerken van een verzameling in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="4715f-103">Update a collection in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4715f-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="4715f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="4715f-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4715f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="4715f-106">Er wordt een tijdje onvermijdelijk, wanneer u tooupdate Hallo apps of de afbeelding in uw Azure RemoteApp-verzameling moet worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="4715f-106">There will come a time, inevitably, when you need tooupdate hello apps or image in your Azure RemoteApp collection.</span></span> <span data-ttu-id="4715f-107">Als u een van Hallo installatiekopieën die zijn opgenomen in uw abonnement Azure RemoteApp in een cloud- of hybride verzameling, worden alle updates worden verwerkt door Azure RemoteApp zelf, zodat u gemakkelijk kunt plaatst.</span><span class="sxs-lookup"><span data-stu-id="4715f-107">If you are using one of hello images included with your Azure RemoteApp subscription, in either a cloud or hybrid collection, any and all updates are handled by Azure RemoteApp itself, so you can rest easy.</span></span>

<span data-ttu-id="4715f-108">Echter als u een aangepaste installatiekopie (dat u hebt ontwikkeld vanaf het begin of dat u hebt gemaakt door het wijzigen van een van onze installatiekopieën) gebruikt, bent u verantwoordelijk onderhouden Hallo installatiekopie en apps.</span><span class="sxs-lookup"><span data-stu-id="4715f-108">However, if you are using a custom image (either that you built from scratch or that you created by modifying one of our images), you are in charge of maintaining hello image and apps.</span></span> <span data-ttu-id="4715f-109">Als u uw installatiekopie of Hallo Apps erin tooupdate nodig, moet u op toocreate een nieuwe, bijgewerkte versie van de installatiekopie van het Hallo en vervangen Hallo bestaande installatiekopie in de verzameling met deze nieuwe, bijgewerkte installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="4715f-109">If you need tooupdate your image or any of hello apps inside it, you need toocreate a new, updated version of hello image, and then replace hello existing image in your collection with this new updated image.</span></span>

<span data-ttu-id="4715f-110">Ja, hoe moet u doen over het bijwerken van uw verzameling?</span><span class="sxs-lookup"><span data-stu-id="4715f-110">So, how do you go about updating your collection?</span></span> <span data-ttu-id="4715f-111">Het is zeer eenvoudig:</span><span class="sxs-lookup"><span data-stu-id="4715f-111">It's fairly straightforward:</span></span>

1. <span data-ttu-id="4715f-112">Hallo-installatiekopie die u hebt gebruikt in uw verzameling bijwerken.</span><span class="sxs-lookup"><span data-stu-id="4715f-112">Update hello image that you used in your collection.</span></span> <span data-ttu-id="4715f-113">Alle patches of de vereiste updates toepassen en sla deze op een nieuwe naam.</span><span class="sxs-lookup"><span data-stu-id="4715f-113">Apply any patches or updates needed, and then save it with a new name.</span></span>
2. <span data-ttu-id="4715f-114">[Uploaden](remoteapp-uploadimage.md) of [importeren](remoteapp-image-on-azurevm.md) die tooRemoteApp installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="4715f-114">[Upload](remoteapp-uploadimage.md) or [import](remoteapp-image-on-azurevm.md) that image tooRemoteApp.</span></span>
3. <span data-ttu-id="4715f-115">Klik nu op Hallo verzameling pagina op **Update**.</span><span class="sxs-lookup"><span data-stu-id="4715f-115">Now, on hello collection page, click **Update**.</span></span>
4. <span data-ttu-id="4715f-116">De nieuwe installatiekopie Hallo kiezen uit Hallo **Sjablooninstallatiekopie** lijst.</span><span class="sxs-lookup"><span data-stu-id="4715f-116">Choose hello new image from hello **Template Image** list.</span></span>
5. <span data-ttu-id="4715f-117">Hier volgt de moeilijkste Hallo - moet u toodecide hoe toodeal met alle gebruikers die momenteel van een app in de verzameling Hallo gebruikmaken.</span><span class="sxs-lookup"><span data-stu-id="4715f-117">Here's hello tricky part - you need toodecide how toodeal with any users that are currently using an app in hello collection.</span></span> <span data-ttu-id="4715f-118">Hebt u Hallo keuzes te volgen:</span><span class="sxs-lookup"><span data-stu-id="4715f-118">You have hello following choices:</span></span>
   
   * <span data-ttu-id="4715f-119">**Geef gebruikers 60 minuten na de update Hallo**.</span><span class="sxs-lookup"><span data-stu-id="4715f-119">**Give users 60 minutes after hello update**.</span></span> <span data-ttu-id="4715f-120">Zodra het Hallo-update is voltooid, wordt Azure RemoteApp een bericht tooany actieve gebruikers om door te geven toosave logboek en hun werk uit en weer aanmelden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4715f-120">As soon as hello update is finished, Azure RemoteApp will display a message tooany active users telling them toosave their work and log off and log back in.</span></span> <span data-ttu-id="4715f-121">Na 60 minuten duurt, wordt alle actieve gebruikers dat u niet afgemeld bent automatisch afgemeld.</span><span class="sxs-lookup"><span data-stu-id="4715f-121">After 60 minutes, any active users who have not logged off will be automatically logged off.</span></span> <span data-ttu-id="4715f-122">Gebruikers kunnen direct aanmelden terug.</span><span class="sxs-lookup"><span data-stu-id="4715f-122">Users can immediately log back on.</span></span>
   * <span data-ttu-id="4715f-123">**Gebruikers direct Afmelden**.</span><span class="sxs-lookup"><span data-stu-id="4715f-123">**Sign users out immediately**.</span></span> <span data-ttu-id="4715f-124">Zodra het Hallo-update is voltooid, zich afmelden bij alle gebruikers automatisch zonder waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="4715f-124">As soon as hello update is finished, log off all users automatically without any warning.</span></span> <span data-ttu-id="4715f-125">Als u deze optie kiest, kunnen gebruikers gegevens verliezen.</span><span class="sxs-lookup"><span data-stu-id="4715f-125">If you choose this option, users might lose data.</span></span> <span data-ttu-id="4715f-126">Ze kunnen echter toohello app onmiddellijk opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4715f-126">However, they can reconnect toohello app immediately.</span></span>
6. <span data-ttu-id="4715f-127">Klik op Hallo vinkje toostart Hallo bijwerken.</span><span class="sxs-lookup"><span data-stu-id="4715f-127">Click hello check mark toostart hello update.</span></span>


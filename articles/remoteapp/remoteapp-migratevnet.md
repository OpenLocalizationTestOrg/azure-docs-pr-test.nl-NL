---
title: aaaHow toomigrate van een RemoteApp VNET tooan Azure VNET | Microsoft Docs
description: Meer informatie over hoe toomigrate van een RemoteApp VNET tooan Azure VNET
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: baea5d29-353b-48f8-b47f-806f2163e067
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: c0f8617556c6f1e33eca8322febf67ff33937ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomigrate-a-hybrid-collection-from-a-remoteapp-vnet-tooan-azure-vnet"></a><span data-ttu-id="f7439-103">Hoe toomigrate een hybride verzameling van een RemoteApp VNET tooan Azure VNET</span><span class="sxs-lookup"><span data-stu-id="f7439-103">How toomigrate a hybrid collection from a RemoteApp VNET tooan Azure VNET</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f7439-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="f7439-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="f7439-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f7439-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="f7439-106">Goed nieuws!</span><span class="sxs-lookup"><span data-stu-id="f7439-106">Good news!</span></span> <span data-ttu-id="f7439-107">We hebben u ingeschakeld toodeploy hybride RemoteApp-collecties rechtstreeks in uw bestaande virtuele Azure-netwerken (vnet's) in plaats van RemoteApp-specifieke VNETs maken.</span><span class="sxs-lookup"><span data-stu-id="f7439-107">We have enabled you toodeploy hybrid RemoteApp collections directly into your existing Azure virtual networks (VNETs) instead of creating RemoteApp-specific VNETs.</span></span> <span data-ttu-id="f7439-108">Hiermee kunt u profiteren van Hallo nieuwste VNET-functies (zoals ExpressRoute) en geef uw tooother hybride verzamelingen netwerk met directe toegang tot Azure-services en virtuele machines geïmplementeerd toothat VNET.</span><span class="sxs-lookup"><span data-stu-id="f7439-108">This lets you take advantage of hello latest VNET features (like ExpressRoute) and give your hybrid collections direct network access tooother Azure services and virtual machines deployed toothat VNET.</span></span>  <span data-ttu-id="f7439-109">(Hiermee haalt u betere prestaties en eenvoudiger instellen dan VNET-naar-VNET-configuraties).</span><span class="sxs-lookup"><span data-stu-id="f7439-109">(This gets you better performance and easier setup than VNET-to-VNET configurations).</span></span>

<span data-ttu-id="f7439-110">Stel dat u hebt al een hybride RemoteApp-collectie aangeroepen gemaakt *OriginalCollection* aangeroepen met een RemoteApp-VNET *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f7439-110">Let’s say that you’ve already created a hybrid RemoteApp collection called *OriginalCollection* with a RemoteApp VNET called *RemoteAppVNET*.</span></span> <span data-ttu-id="f7439-111">Hier volgen Hallo stappen toomigrate deze nieuwe Azure VNET aangeroepen tooa *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="f7439-111">Here are hello steps toomigrate it tooa new Azure VNET called *AzureVNET*.</span></span>

1. <span data-ttu-id="f7439-112">Op Hallo **netwerken** tabblad in Hallo [beheerportal](http://manage.windowsazure.com/), maak een VNET aangeroepen *AzureVNET*met dezelfde locatie, DNS-configuratie en adresruimte (voor ten minste één Hallo Hallo *AzureVNET* subnetten) als u hebt gebruikt voor *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f7439-112">On hello **Networks** tab in hello [management portal](http://manage.windowsazure.com/), create a VNET called *AzureVNET*, using hello same location, DNS configuration, and address space (for at least one of hello *AzureVNET* subnets) as you used for *RemoteAppVNET*.</span></span>
2. <span data-ttu-id="f7439-113">Configureer *AzureVNET* tooeither hosten of network connectivity toohello Active Directory-implementatie hebt die *OriginalCollection* domein lid is.</span><span class="sxs-lookup"><span data-stu-id="f7439-113">Configure *AzureVNET* tooeither host or have network connectivity toohello Active Directory deployment that *OriginalCollection* is domain joined to.</span></span>
3. <span data-ttu-id="f7439-114">Op Hallo **instellen om RemoteApps** tabblad, maakt u een nieuwe RemoteApp-collectie aangeroepen *nieuwe verzameling*.</span><span class="sxs-lookup"><span data-stu-id="f7439-114">On hello **RemoteApps** tab, create a new RemoteApp collection called *New Collection*.</span></span> <span data-ttu-id="f7439-115">(Gebruik Hallo **maken met VNET** optie niet **snelle invoer**.)</span><span class="sxs-lookup"><span data-stu-id="f7439-115">(Use hello **Create with VNET** option, not **Quick Create**.)</span></span>
4. <span data-ttu-id="f7439-116">Configureer *NewCollection* toobe geïmplementeerd tooa subnet in *AzureVNET*.</span><span class="sxs-lookup"><span data-stu-id="f7439-116">Configure *NewCollection* toobe deployed tooa subnet in *AzureVNET*.</span></span>
5. <span data-ttu-id="f7439-117">Configureer *NewCollection* toouse Hallo dezelfde installatiekopie en de gegevens voor domeindeelname als u hebt gebruikt voor *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="f7439-117">Configure *NewCollection* toouse hello same image and domain join information as you used for *OriginalCollection*.</span></span>
6. <span data-ttu-id="f7439-118">Na enkele uren *NewCollection* wordt weergegeven in de verzamelingenlijst met een actieve status heeft.</span><span class="sxs-lookup"><span data-stu-id="f7439-118">After a few hours, *NewCollection* will show up in your collection list with an Active state.</span></span>

<span data-ttu-id="f7439-119">Nu, als u geen toomigrate gebruikersgegevens uit Hallo oorspronkelijke verzameling toohello nieuwe verzameling, doen deze stappen:</span><span class="sxs-lookup"><span data-stu-id="f7439-119">Now, if you DON’T need toomigrate any user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="f7439-120">Verwijder *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="f7439-120">Delete *OriginalCollection*.</span></span>
2. <span data-ttu-id="f7439-121">Verwijder *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f7439-121">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="f7439-122">En u klaar bent!</span><span class="sxs-lookup"><span data-stu-id="f7439-122">And, you’re done!</span></span>

<span data-ttu-id="f7439-123">U kunt ook als u de gebruikersinformatie toomigrate uit Hallo oorspronkelijke verzameling toohello nieuwe verzameling hoeft, gaat u deze stappen naast:</span><span class="sxs-lookup"><span data-stu-id="f7439-123">Alternately, if you DO need toomigrate user information from hello original collection toohello new collection, do these steps next:</span></span>

1. <span data-ttu-id="f7439-124">E-mailbericht te verzenden[ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) met uw Azure-abonnement-ID, naam van uw oorspronkelijke verzameling en Hallo-naam van de nieuwe verzameling Hallo en vraag deze toomigrate uw gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="f7439-124">Send an email too[remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20user%20information%20migration) with your Azure subscription ID, hello name of your original collection, and hello name of your new collection, and ask them toomigrate your user information.</span></span>
2. <span data-ttu-id="f7439-125">Binnen 2 dagen worden Hallo RemoteApp-team Hallo toegang gebruikerslijst alle gebruikersdocumenten en gebruikersinstellingen verplaatst van Hallo oorspronkelijke verzameling toohello nieuwe verzameling.</span><span class="sxs-lookup"><span data-stu-id="f7439-125">Within 2 business days hello RemoteApp team will move hello user access list and all user documents and user settings from hello original collection toohello new collection.</span></span>
3. <span data-ttu-id="f7439-126">Verwijder *OriginalCollection*.</span><span class="sxs-lookup"><span data-stu-id="f7439-126">Delete *OriginalCollection*.</span></span>
4. <span data-ttu-id="f7439-127">Verwijder *RemoteAppVNET*.</span><span class="sxs-lookup"><span data-stu-id="f7439-127">Delete *RemoteAppVNET*.</span></span>

<span data-ttu-id="f7439-128">En u bent nu klaar!</span><span class="sxs-lookup"><span data-stu-id="f7439-128">And now, you’re done!</span></span>

<span data-ttu-id="f7439-129">Als u vragen hebt of speciale hulp nodig hebt, kunt u een e-mail [ remoteappforum@microsoft.com ](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span><span class="sxs-lookup"><span data-stu-id="f7439-129">If you have any questions or need special assistance, please email [remoteappforum@microsoft.com](mailto:remoteappforum@microsoft.com?subject=Azure%20RemoteApp%20VNET%20migration%20help).</span></span>


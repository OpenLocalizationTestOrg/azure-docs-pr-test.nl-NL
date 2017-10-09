---
title: aaaUpload een aangepaste installatiekopie voor Azure RemoteApp | Microsoft Docs
description: Meer informatie over hoe tooupload een aangepaste installatiekopie voor Azure RemoteApp
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a><span data-ttu-id="9f4da-103">Een aangepaste installatiekopie uploaden voor Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="9f4da-103">Upload a custom image for Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="9f4da-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="9f4da-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="9f4da-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9f4da-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="9f4da-106">Nu u de installatiekopie van uw aangepaste sjabloon hebt gemaakt of met wijzigingen bijgewerkt, moet u tooupload die afbeeldingsbibliotheek tooyour Azure RemoteApp-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="9f4da-106">Now that you have created your custom template image or have updated it with changes, you need tooupload that image tooyour Azure RemoteApp image library.</span></span> <span data-ttu-id="9f4da-107">Volg deze stappen.</span><span class="sxs-lookup"><span data-stu-id="9f4da-107">Use these steps.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="9f4da-108">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9f4da-108">Before you start</span></span>
1. <span data-ttu-id="9f4da-109">Controleer of de aangepaste installatiekopie voldoet aan Hallo [afbeeldingsvereisten](remoteapp-imagereqs.md) en [toepassingsvereisten](remoteapp-appreqs.md).</span><span class="sxs-lookup"><span data-stu-id="9f4da-109">Verify your custom image meets hello [image requirements](remoteapp-imagereqs.md) and [application requirements](remoteapp-appreqs.md).</span></span>
2. <span data-ttu-id="9f4da-110">Hallo installeren [Azure PowerShell-module](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9f4da-110">Install hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

## <a name="step-by-step-on-how-tooupload-custom-image"></a><span data-ttu-id="9f4da-111">Stap voor stap voor het aangepaste installatiekopie tooupload</span><span class="sxs-lookup"><span data-stu-id="9f4da-111">Step by step on how tooupload custom image</span></span>
1. <span data-ttu-id="9f4da-112">Open Azure Management Portal en navigeer van toohello RemoteApp-pagina.</span><span class="sxs-lookup"><span data-stu-id="9f4da-112">Open Azure Management Portal and navigate toohello RemoteApp page.</span></span>
2. <span data-ttu-id="9f4da-113">Op Hallo **sjablooninstallatiekopieën** tabblad **uploaden** Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="9f4da-113">On hello **Template images** tab, click **Upload** at hello bottom of hello page.</span></span>
3. <span data-ttu-id="9f4da-114">Geef een beschrijvende naam voor uw installatiekopie en Hallo opslagaccountlocatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="9f4da-114">Enter a friendly name for your image and specify hello storage account location.</span></span> <span data-ttu-id="9f4da-115">Zorg ervoor dat de locatie Hallo Hallo dezelfde locatie als uw RemoteApp-collectie of een locatie waar u toocreate een.</span><span class="sxs-lookup"><span data-stu-id="9f4da-115">Ensure hello location is hello same location as your RemoteApp collection or a location where you want toocreate one.</span></span>
4. <span data-ttu-id="9f4da-116">Wanneer u wordt gevraagd, downloaden Hallo script tooyour lokale PC.</span><span class="sxs-lookup"><span data-stu-id="9f4da-116">When prompted, download hello script tooyour local PC.</span></span>
5. <span data-ttu-id="9f4da-117">Hallo opdrachtparameters in Hallo tekst vak tooyour Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="9f4da-117">Copy hello command parameters in hello text box tooyour clipboard.</span></span>
6. <span data-ttu-id="9f4da-118">Open een Windows PowerShell-venster met verhoogde bevoegdheid.</span><span class="sxs-lookup"><span data-stu-id="9f4da-118">Open an elevated Windows PowerShell window.</span></span>
7. <span data-ttu-id="9f4da-119">Van Hallo met verhoogde bevoegdheden voor Windows PowerShell-venster Navigeren toohello dezelfde map waarin u Hallo script gedownload.</span><span class="sxs-lookup"><span data-stu-id="9f4da-119">From hello elevated Windows PowerShell window, navigate toohello same directory where you downloaded hello script.</span></span>
8. <span data-ttu-id="9f4da-120">Plakken Hallo gekopieerd opdracht en druk op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9f4da-120">Paste hello copied command and press **Enter**.</span></span>
   
   <span data-ttu-id="9f4da-121">Hallo uploadproces wordt gestart en duur afhankelijk zijn van veel factoren, waaronder uw netwerksnelheid en de grootte van afbeelding Hallo</span><span class="sxs-lookup"><span data-stu-id="9f4da-121">hello upload process will begin and duration may depend on many factors including your network speed and size of hello image</span></span>
9. <span data-ttu-id="9f4da-122">U kunt uw uploaden mislukt vanwege onderbreking op het netwerk of dingen die, altijd Hallo uploadproces die u begon te hervatten.</span><span class="sxs-lookup"><span data-stu-id="9f4da-122">If your upload does not succeed because of network interruption or things like that, you can always resume hello upload process you began.</span></span> <span data-ttu-id="9f4da-123">tooresume een upload Voer Hallo script opnieuw uit met dezelfde Hallo vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="9f4da-123">tooresume an upload, run hello script again using hello same command line.</span></span>

> [!WARNING]
> <span data-ttu-id="9f4da-124">Nooit Hallo uploaden script wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9f4da-124">Never modify hello upload script.</span></span> <span data-ttu-id="9f4da-125">Specifieke controles zijn geïmplementeerd tooensure die Hallo installatiekopie voldoet aan Hallo installatiekopie van de vereisten en toepassingsvereisten.</span><span class="sxs-lookup"><span data-stu-id="9f4da-125">Specific checks have been implemented tooensure that hello image meets hello image requirements and application requirements.</span></span>
> 
> 

## <a name="common-problems"></a><span data-ttu-id="9f4da-126">Algemene problemen</span><span class="sxs-lookup"><span data-stu-id="9f4da-126">Common problems</span></span>
* <span data-ttu-id="9f4da-127">Zorg ervoor dat u Windows PowerShell, niet Azure PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9f4da-127">Make sure you use Windows PowerShell, not Azure PowerShell.</span></span> <span data-ttu-id="9f4da-128">U moet tooinstall hello Azure PowerShell-module omdat bepaalde modules nodig zijn tijdens Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="9f4da-128">You need tooinstall hello Azure PowerShell module because certain modules are needed during hello upload process.</span></span>
* <span data-ttu-id="9f4da-129">Nooit alter Hallo script, validaties zijn er voor uw gemak.</span><span class="sxs-lookup"><span data-stu-id="9f4da-129">Never alter hello script, validations are there for your convenience.</span></span>
* <span data-ttu-id="9f4da-130">Als Hallo vhd-bestand is vergrendeld tijdens het uploaden, Hallo bestand kopiëren of verplaatsen nieuwe locatie en probeer het uploaden van tooa opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9f4da-130">If hello vhd file gets locked out during upload, copy hello file or move it tooa new location and attempt upload again.</span></span> <span data-ttu-id="9f4da-131">Er is mogelijk een Windows-proces dat voorkomt uploaden dat.</span><span class="sxs-lookup"><span data-stu-id="9f4da-131">There might be some Windows process that is preventing upload.</span></span>  


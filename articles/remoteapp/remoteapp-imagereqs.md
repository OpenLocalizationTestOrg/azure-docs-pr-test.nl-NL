---
title: vereisten voor RemoteApp-installatiekopie aaaAzure | Microsoft Docs
description: "Meer informatie over het Hallo-vereisten voor het maken van installatiekopieën toobe gebruikt met Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 7cbb90f4-6dc9-462c-a429-088cdb57414e
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 4e35203eb93a866d4e0bd591d42b34746c7ffa4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="a51c1-103">Vereisten voor Azure RemoteApp-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="a51c1-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="a51c1-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="a51c1-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="a51c1-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a51c1-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="a51c1-106">Azure RemoteApp gebruikt een installatiekopie van Windows Server 2012 R2 toohost alle Hallo-programma's die u wilt de tooshare met uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="a51c1-106">Azure RemoteApp uses a Windows Server 2012 R2 image toohost all hello programs that you want tooshare with your users.</span></span> <span data-ttu-id="a51c1-107">een aangepaste installatiekopie toocreate, u kunt beginnen met een bestaande installatiekopie of [Maak een nieuwe](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="a51c1-107">toocreate a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="a51c1-108">Wist u dat uw Azure RemoteApp-abonnement biedt die u toegang tot Windows Server 2012 R2-afbeelding tooa in de virtuele machine van Azure-galerie waarmee u toocreate uw eigen sjablooninstallatiekopie kunt Hallo?</span><span class="sxs-lookup"><span data-stu-id="a51c1-108">Did you know that your Azure RemoteApp subscription gives you access tooa Windows Server 2012 R2 image in hello Azure VM gallery that you can use toocreate your own template image?</span></span> <span data-ttu-id="a51c1-109">[Het uitchecken](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="a51c1-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="a51c1-110">Hallo-vereisten voor het Hallo-installatiekopie die kan worden geüpload voor gebruik met Azure RemoteApp zijn:</span><span class="sxs-lookup"><span data-stu-id="a51c1-110">hello requirements for hello image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="a51c1-111">Aangepaste toepassingen opslaan niet gegevens lokaal op Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a51c1-111">Custom applications don’t store data locally on hello image.</span></span> <span data-ttu-id="a51c1-112">Deze installatiekopieën staatloze zijn en mag alleen toepassingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="a51c1-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="a51c1-113">Hallo-afbeelding bevat geen gegevens die verbroken worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="a51c1-113">hello image does not contain data that can be lost.</span></span>
* <span data-ttu-id="a51c1-114">Afbeeldingsgrootte Hallo moet een veelvoud van MB.</span><span class="sxs-lookup"><span data-stu-id="a51c1-114">hello image size should be a multiple of MBs.</span></span> <span data-ttu-id="a51c1-115">Als u een installatiekopie die is geen exacte veelvoud tooupload probeert, mislukt de Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="a51c1-115">If you try tooupload an image that is not an exact multiple, hello upload will fail.</span></span>
* <span data-ttu-id="a51c1-116">Hallo afbeeldingsformaat moet 127 GB of kleiner.</span><span class="sxs-lookup"><span data-stu-id="a51c1-116">hello image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="a51c1-117">Dit moet een VHD-bestand (VHDX-bestanden worden momenteel niet ondersteund).</span><span class="sxs-lookup"><span data-stu-id="a51c1-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="a51c1-118">Hallo VHD mag geen virtuele machines van generatie 2.</span><span class="sxs-lookup"><span data-stu-id="a51c1-118">hello VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="a51c1-119">Hallo VHD kan een vaste grootte of dynamisch uitbreidbare zijn.</span><span class="sxs-lookup"><span data-stu-id="a51c1-119">hello VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="a51c1-120">Een dynamisch uitbreidbare VHD wordt aanbevolen omdat duurt het minder tijd tooupload tooAzure dan een vaste grootte VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="a51c1-120">A dynamically expanding VHD is recommended because it takes less time tooupload tooAzure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="a51c1-121">Hallo-schijf moet worden geïnitialiseerd met Hallo Master Boot Record (MBR) partitionering stijl.</span><span class="sxs-lookup"><span data-stu-id="a51c1-121">hello disk must be initialized using hello Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="a51c1-122">Hallo partitiestijl van GUID partition table (GPT) wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a51c1-122">hello GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="a51c1-123">Hallo VHD moet één installatie van Windows Server 2012 R2 bevatten.</span><span class="sxs-lookup"><span data-stu-id="a51c1-123">hello VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="a51c1-124">Meerdere volumes, maar slechts één met een installatie van Windows kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="a51c1-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="a51c1-125">Hallo Remote Desktop Session Host (RDSH)-functie en de functie Bureaubladervaring Hallo moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a51c1-125">hello Remote Desktop Session Host (RDSH) role and hello Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="a51c1-126">Hallo Remote Desktop Connection Broker-rol moet *niet* worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a51c1-126">hello Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="a51c1-127">Hallo Encrypting File System (EFS) moet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a51c1-127">hello Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="a51c1-128">Hallo-installatiekopie moet SYSPREPed met Hallo parameters **/oobe / generalize/shutdown** (gebruikt Hallo **/mode:vm** parameter).</span><span class="sxs-lookup"><span data-stu-id="a51c1-128">hello image must be SYSPREPed using hello parameters **/oobe /generalize /shutdown** (DO NOT use hello **/mode:vm** parameter).</span></span>
* <span data-ttu-id="a51c1-129">Uploaden van uw VHD van een keten van de momentopname wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a51c1-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="a51c1-130">Zie [maken van een installatiekopie van een Azure RemoteApp](remoteapp-imageoptions.md) voor meer informatie over het maken van installatiekopieën voor Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="a51c1-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>


---
title: Azure RemoteApp image-vereisten | Microsoft Docs
description: "Meer informatie over de vereisten voor het maken van installatiekopieën moet worden gebruikt met Azure RemoteApp"
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
ms.openlocfilehash: 75b0f8d6b25a80f11002b683152cfb294cbb68bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="requirements-for-azure-remoteapp-images"></a><span data-ttu-id="b3741-103">Vereisten voor Azure RemoteApp-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="b3741-103">Requirements for Azure RemoteApp images</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b3741-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="b3741-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b3741-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b3741-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b3741-106">Azure RemoteApp maakt gebruik van een Windows Server 2012 R2-afbeelding voor het hosten van alle programma's die u wilt delen met uw gebruikers.</span><span class="sxs-lookup"><span data-stu-id="b3741-106">Azure RemoteApp uses a Windows Server 2012 R2 image to host all the programs that you want to share with your users.</span></span> <span data-ttu-id="b3741-107">Voor het maken van een aangepaste installatiekopie die u kunt beginnen met een bestaande installatiekopie of [Maak een nieuwe](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="b3741-107">To create a custom image, you can start with an existing image or [create a new one](remoteapp-create-custom-image.md).</span></span>

> [!TIP]
> <span data-ttu-id="b3741-108">Wist u dat uw Azure RemoteApp-abonnement hebt dat u toegang tot een Windows Server 2012 R2-installatiekopie in de galerie van Azure VM die u gebruiken kunt om uw eigen sjablooninstallatiekopie te maken?</span><span class="sxs-lookup"><span data-stu-id="b3741-108">Did you know that your Azure RemoteApp subscription gives you access to a Windows Server 2012 R2 image in the Azure VM gallery that you can use to create your own template image?</span></span> <span data-ttu-id="b3741-109">[Het uitchecken](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="b3741-109">[Check it out](remoteapp-image-on-azurevm.md).</span></span>  
> 
> 

<span data-ttu-id="b3741-110">De vereisten voor de installatiekopie die kan worden geüpload voor gebruik met Azure RemoteApp zijn:</span><span class="sxs-lookup"><span data-stu-id="b3741-110">The requirements for the image that can be uploaded for use with Azure RemoteApp are:</span></span>

* <span data-ttu-id="b3741-111">Aangepaste toepassingen opslaan niet gegevens lokaal op de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b3741-111">Custom applications don’t store data locally on the image.</span></span> <span data-ttu-id="b3741-112">Deze installatiekopieën staatloze zijn en mag alleen toepassingen bevatten.</span><span class="sxs-lookup"><span data-stu-id="b3741-112">These images are stateless and should only contain applications.</span></span>
* <span data-ttu-id="b3741-113">De afbeelding bevat geen gegevens die verloren kunnen gaan.</span><span class="sxs-lookup"><span data-stu-id="b3741-113">The image does not contain data that can be lost.</span></span>
* <span data-ttu-id="b3741-114">Grootte van de afbeelding moet een veelvoud van MB.</span><span class="sxs-lookup"><span data-stu-id="b3741-114">The image size should be a multiple of MBs.</span></span> <span data-ttu-id="b3741-115">Als u probeert te uploaden van een installatiekopie die is geen exacte veelvoud, mislukt het uploaden.</span><span class="sxs-lookup"><span data-stu-id="b3741-115">If you try to upload an image that is not an exact multiple, the upload will fail.</span></span>
* <span data-ttu-id="b3741-116">Grootte van de installatiekopie moet 127 GB of kleiner.</span><span class="sxs-lookup"><span data-stu-id="b3741-116">The image size must be 127 GB or smaller.</span></span>
* <span data-ttu-id="b3741-117">Dit moet een VHD-bestand (VHDX-bestanden worden momenteel niet ondersteund).</span><span class="sxs-lookup"><span data-stu-id="b3741-117">It must be on a VHD file (VHDX files are not currently supported).</span></span>
* <span data-ttu-id="b3741-118">De VHD moet geen virtuele machines van generatie 2.</span><span class="sxs-lookup"><span data-stu-id="b3741-118">The VHD must not be a generation 2 virtual machine.</span></span>
* <span data-ttu-id="b3741-119">De VHD kan een vaste grootte of dynamisch uitbreidbare zijn.</span><span class="sxs-lookup"><span data-stu-id="b3741-119">The VHD can be either fixed-size or dynamically expanding.</span></span> <span data-ttu-id="b3741-120">Een dynamisch uitbreidbare VHD wordt aanbevolen omdat kost het minder tijd om te uploaden naar Azure dan een vaste grootte VHD-bestand.</span><span class="sxs-lookup"><span data-stu-id="b3741-120">A dynamically expanding VHD is recommended because it takes less time to upload to Azure than a fixed-size VHD file.</span></span>
* <span data-ttu-id="b3741-121">De schijf moet worden geïnitialiseerd met behulp van de Record MBR (Master Boot) stijl partitioneren.</span><span class="sxs-lookup"><span data-stu-id="b3741-121">The disk must be initialized using the Master Boot Record (MBR) partitioning style.</span></span> <span data-ttu-id="b3741-122">De partitiestijl GUID partition table (GPT) wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b3741-122">The GUID partition table (GPT) partition style is not supported.</span></span>
* <span data-ttu-id="b3741-123">De VHD moet één installatie van Windows Server 2012 R2 bevatten.</span><span class="sxs-lookup"><span data-stu-id="b3741-123">The VHD must contain a single installation of Windows Server 2012 R2.</span></span> <span data-ttu-id="b3741-124">Meerdere volumes, maar slechts één met een installatie van Windows kan bevatten.</span><span class="sxs-lookup"><span data-stu-id="b3741-124">It can contain multiple volumes, but only one that contains an installation of Windows.</span></span>
* <span data-ttu-id="b3741-125">De functie Remote Desktop Session Host (RDSH) en de functie Bureaubladervaring moeten worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b3741-125">The Remote Desktop Session Host (RDSH) role and the Desktop Experience feature must be installed.</span></span>
* <span data-ttu-id="b3741-126">De extern bureaublad Connection Broker-rol moet *niet* worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b3741-126">The Remote Desktop Connection Broker role must *not* be installed.</span></span>
* <span data-ttu-id="b3741-127">Het Encrypting File System (EFS) moet worden uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b3741-127">The Encrypting File System (EFS) must be disabled.</span></span>
* <span data-ttu-id="b3741-128">De afbeelding moet met de parameters SYSPREPed **/oobe / generalize/shutdown** (niet gebruik de **/mode:vm** parameter).</span><span class="sxs-lookup"><span data-stu-id="b3741-128">The image must be SYSPREPed using the parameters **/oobe /generalize /shutdown** (DO NOT use the **/mode:vm** parameter).</span></span>
* <span data-ttu-id="b3741-129">Uploaden van uw VHD van een keten van de momentopname wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b3741-129">Uploading your VHD from a snapshot chain is not supported.</span></span>

<span data-ttu-id="b3741-130">Zie [maken van een installatiekopie van een Azure RemoteApp](remoteapp-imageoptions.md) voor meer informatie over het maken van installatiekopieën voor Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b3741-130">See [Create an Azure RemoteApp image](remoteapp-imageoptions.md) for more information about creating images for Azure RemoteApp.</span></span>


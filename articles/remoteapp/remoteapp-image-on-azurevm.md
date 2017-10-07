---
title: een Azure RemoteApp-installatiekopie op basis van een Azure VM aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een afbeelding voor Azure RemoteApp door te beginnen met een virtuele machine van Azure.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: d41583ef-6cd8-4115-8dcb-b2cd5b3d301a
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 2d432bcb15be68a2946d91b5f36f41d980726338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-azure-remoteapp-image-based-on-an-azure-virtual-machine"></a><span data-ttu-id="dd2ff-103">Een Azure RemoteApp-installatiekopie op basis van een virtuele machine van Azure maken</span><span class="sxs-lookup"><span data-stu-id="dd2ff-103">Create a Azure RemoteApp image based on an Azure virtual machine</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dd2ff-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="dd2ff-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="dd2ff-106">U kunt Azure RemoteApp-installatiekopieën (die houdt Hallo-apps die u in uw verzameling deelt) maken van een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-106">You can create Azure RemoteApp images (which hold hello apps you share in your collection) from an Azure virtual machine.</span></span> <span data-ttu-id="dd2ff-107">Ook kunt u toouse de installatiekopie van een virtuele machine toegevoegd toohello Azure VM-installatiekopie galerie die voldoet aan alle vereisten van hello Azure RemoteApp-installatiekopie: u kunt die VM-installatiekopie gebruiken als een beginpunt voor uw eigen virtuele machine, als u wilt.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-107">You could also choose toouse a virtual machine image we added toohello Azure VM image gallery that meets all hello Azure RemoteApp image requirements - you can use that VM image as a starting point for your own VM, if you want.</span></span> <span data-ttu-id="dd2ff-108">Kijk voor Hallo 'Windows Server extern bureaublad-sessiehost'-installatiekopie in Hallo-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-108">Just look for hello "Windows Server Remote Desktop Session Host" image in hello library.</span></span>

<span data-ttu-id="dd2ff-109">Er zijn twee stappen toocreate uw eigen installatiekopie op basis van een Azure VM - Hallo installatiekopie maken en uploaden van hello Azure VM-bibliotheek tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-109">There are two steps toocreate your own image based on an Azure VM - create hello image and then upload it from hello Azure VM library tooAzure RemoteApp.</span></span>

## <a name="create-a-custom-image-based-on-an-azure-vm"></a><span data-ttu-id="dd2ff-110">Een aangepaste installatiekopie op basis van een virtuele machine in Azure maken</span><span class="sxs-lookup"><span data-stu-id="dd2ff-110">Create a custom image based on an Azure VM</span></span>
<span data-ttu-id="dd2ff-111">Gebruik deze stappen toocreate een installatiekopie op basis van een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-111">Use these steps toocreate an image based on an Azure VM.</span></span>

1. <span data-ttu-id="dd2ff-112">Maak een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-112">Create an Azure virtual machine.</span></span> <span data-ttu-id="dd2ff-113">U kunt Hallo 'Windows Server extern bureaublad-sessiehost' of 'Windows Server Remote Desktop Session Host met Microsoft Office 365 ProPlus' Hallo-installatiekopie vanuit galerie met virtuele machine van Azure installatiekopie hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-113">You can use hello "Windows Server Remote Desktop Session Host" or hello "Windows Server Remote Desktop Session Host with Microsoft Office 365 ProPlus" image from hello Azure virtual machine image gallery.</span></span> <span data-ttu-id="dd2ff-114">Deze installatiekopie voldoet aan de vereisten van de installatiekopie van het Azure RemoteApp sjabloon Hallo.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-114">This image meets all hello Azure RemoteApp template image requirements.</span></span>
   
    <span data-ttu-id="dd2ff-115">Zie voor meer informatie [maken van een virtuele machine met Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd2ff-115">For details, see [Create a VM running Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="dd2ff-116">Verbinding maken met toohello VM en installeren en configureren van Hallo-apps die u wilt dat tooshare via RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-116">Connect toohello VM and install and configure hello apps that you want tooshare through RemoteApp.</span></span> <span data-ttu-id="dd2ff-117">Zorg ervoor dat tooperform geen aanvullende Windows-configuraties die vereist zijn voor uw apps.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-117">Make sure tooperform any additional Windows configurations required by your apps.</span></span>
   
    <span data-ttu-id="dd2ff-118">Zie voor meer informatie [hoe tooLog op virtuele Machine Running Windows Server tooa](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dd2ff-118">For details, see [How tooLog on tooa Virtual Machine Running Windows Server](../virtual-machines/windows/classic/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>
3. <span data-ttu-id="dd2ff-119">Als u van een Windows Server Remote Desktop Session Host-installatiekopieën hello gebruikmaakt, is er een opgenomen validatiescript uw virtuele machine voldoet aan Hallo RemoteApp pre-reqs. zo dat</span><span class="sxs-lookup"><span data-stu-id="dd2ff-119">If you are using one of hello Windows Server Remote Desktop Session Host images, there is an included validation script that will ensure your VM meets hello RemoteApp pre-reqs.</span></span> <span data-ttu-id="dd2ff-120">toorun script, dubbelklikt u op **ValidateRemoteAppImage** op Hallo bureaublad.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-120">toorun script, double-click **ValidateRemoteAppImage** on hello desktop.</span></span> <span data-ttu-id="dd2ff-121">Zorg ervoor dat alle fouten gerapporteerd door Hallo script worden opgelost voordat u doorgaat toohello volgende stap.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-121">Ensure that all errors reported by hello script are fixed before proceeding toohello next step.</span></span>
4. <span data-ttu-id="dd2ff-122">SYSPREP generaliseren en Hallo installatiekopie vastleggen.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-122">SYSPREP generalize and capture hello image.</span></span> <span data-ttu-id="dd2ff-123">Zie [hoe tooCapture een tooUse virtuele Windows-computer als een sjabloon](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-123">See [How tooCapture a Windows Virtual Machine tooUse as a Template](../virtual-machines/windows/classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) for instructions.</span></span>

## <a name="import-hello-image-into-hello-azure-remoteapp-image-library"></a><span data-ttu-id="dd2ff-124">Hallo afbeelding importeren in Azure RemoteApp-afbeeldingsbibliotheek Hallo</span><span class="sxs-lookup"><span data-stu-id="dd2ff-124">Import hello image into hello Azure RemoteApp image library</span></span>
<span data-ttu-id="dd2ff-125">Gebruik deze stappen tooimport Hallo nieuwe installatiekopie in Azure RemoteApp:</span><span class="sxs-lookup"><span data-stu-id="dd2ff-125">Use these steps tooimport hello new image into Azure RemoteApp:</span></span>

1. <span data-ttu-id="dd2ff-126">In Hallo **Sjablooninstallatiekopieën** tabblad:</span><span class="sxs-lookup"><span data-stu-id="dd2ff-126">In hello **Template Images** tab:</span></span>
   
   * <span data-ttu-id="dd2ff-127">Als u geen bestaande afbeeldingen hebt, klikt u op **uploaden of de installatiekopie van een sjabloon importeren**.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-127">If you have no existing images, click **Upload or Import a Template Image**.</span></span>
   * <span data-ttu-id="dd2ff-128">Als u ten minste één installatiekopie al hebt, klikt u op  **+**  tooadd een nieuwe installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-128">If you have at least one image already, click **+** tooadd a new image.</span></span>
2. <span data-ttu-id="dd2ff-129">Selecteer **een afbeelding van uw virtuele Machines importeren** bibliotheek, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-129">Select **Import an image from your Virtual Machines** library, and then click **Next**.</span></span>
3. <span data-ttu-id="dd2ff-130">Op de volgende pagina hello, selecteert u de aangepaste installatiekopie in Hallo lijst en Bevestig dat u Hallo stappen die worden vermeld bij het maken van uw installatiekopie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-130">On hello next page, select your custom image from hello list and confirm that you followed hello steps listed when you created your image.</span></span> <span data-ttu-id="dd2ff-131">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-131">Click **Next**.</span></span>
4. <span data-ttu-id="dd2ff-132">Voer een naam voor de nieuwe RemoteApp-installatiekopie Hallo Hallo locatie kiezen, en klikt u op Hallo vinkje toostart Hallo-importproces.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-132">Enter a name for hello new RemoteApp image and pick hello location, then click hello checkmark toostart hello import process.</span></span>

> [!NOTE]
> <span data-ttu-id="dd2ff-133">U kunt afbeeldingen importeren uit een Azure-locatie wordt ondersteund door Azure Virtual Machines tooany Azure-locatie wordt ondersteund door Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-133">You can import images from any Azure location supported by Azure Virtual Machines tooany Azure location supported by Azure RemoteApp.</span></span> <span data-ttu-id="dd2ff-134">Afhankelijk van Hallo locaties kan Hallo importeren too25 minuten duren.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-134">Depending on hello locations hello import can take up too25 minutes.</span></span>
> 
> 

<span data-ttu-id="dd2ff-135">U bent er nu klaar toocreate uw nieuwe verzameling, ofwel een [cloud](remoteapp-create-cloud-deployment.md) verzameling of [hybride](remoteapp-create-hybrid-deployment.md), afhankelijk van uw behoeften.</span><span class="sxs-lookup"><span data-stu-id="dd2ff-135">Now you are ready toocreate your new collection, either a [cloud](remoteapp-create-cloud-deployment.md) collection or [hybrid](remoteapp-create-hybrid-deployment.md), depending on your needs.</span></span>


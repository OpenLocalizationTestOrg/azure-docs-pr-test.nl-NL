---
title: aaaCreate een installatiekopie van een Azure RemoteApp | Microsoft Docs
description: "Meer informatie over het Hallo-opties die beschikbaar zijn voor het maken van installatiekopieën voor Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: cb0f9424-6185-45a1-abe9-c23f1edf34f2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 54e63b6fa13addfcda96ce581910e1ac48d91e70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-remoteapp-image"></a><span data-ttu-id="1a872-103">Create an Azure RemoteApp image (Een installatiekopie maken voor Azure RemoteApp)</span><span class="sxs-lookup"><span data-stu-id="1a872-103">Create an Azure RemoteApp image</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1a872-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="1a872-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1a872-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1a872-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1a872-106">Azure RemoteApp maakt gebruik van installatiekopieën toohold Hallo apps die u met uw gebruikers deelt.</span><span class="sxs-lookup"><span data-stu-id="1a872-106">Azure RemoteApp uses images toohold hello apps that you share with your users.</span></span> <span data-ttu-id="1a872-107">(We nemen uw installatiekopie en virtuele machines toocreate - die het Hallo-gebruikers toegang wanneer ze zich aanmelden bij Azure RemoteApp.) toocreate een Azure RemoteApp-verzameling met uw keuze van toepassingen, of de cloud of hybride, begint u met een installatiekopie maken met deze toepassingen zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1a872-107">(We take your image and use it toocreate VMs - that's what hello users access when they sign into Azure RemoteApp.) toocreate an Azure RemoteApp collection with your choice of applications, whether it is cloud or hybrid, you  start by creating an image with those applications installed.</span></span> <span data-ttu-id="1a872-108">Vervolgens maakt u een verzameling die gebruikmaakt van de installatiekopie, gebruikers toohello verzameling toewijzen en publiceren van apps toothose gebruikers.</span><span class="sxs-lookup"><span data-stu-id="1a872-108">Then, create a collection that uses that image, assign users toohello collection, and publish apps toothose users.</span></span>

<span data-ttu-id="1a872-109">U hebt verschillende mogelijkheden voor het maken of met behulp van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="1a872-109">You have several options for creating or using images.</span></span> <span data-ttu-id="1a872-110">Hallo basic [vereiste](remoteapp-imagereqs.md) voor een installatiekopie is dat het uitvoeren van Windows Server 2012 R2 en Hallo Remote Desktop Session Host (RDSH)-rol is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1a872-110">hello basic [requirement](remoteapp-imagereqs.md) for an image is that it run Windows Server 2012 R2 and have hello Remote Desktop Session Host (RDSH) role installed.</span></span> <span data-ttu-id="1a872-111">Hoe u krijgt dat is waar dingen interessante krijgen.</span><span class="sxs-lookup"><span data-stu-id="1a872-111">How you get that is where things get interesting.</span></span>

<span data-ttu-id="1a872-112">Hebt u volgende opties wanneer deze wordt gezet tooimages Hallo:</span><span class="sxs-lookup"><span data-stu-id="1a872-112">You have hello following options when it comes tooimages:</span></span>

* <span data-ttu-id="1a872-113">U kunt importeren en gebruiken een [installatiekopie op basis van een virtuele machine van Azure](remoteapp-image-on-azurevm.md).</span><span class="sxs-lookup"><span data-stu-id="1a872-113">You can import and use an [image based on an Azure virtual machine](remoteapp-image-on-azurevm.md).</span></span> <span data-ttu-id="1a872-114">Dit is geschikt voor line-of-business-apps waarvoor u aangepaste instellingen.</span><span class="sxs-lookup"><span data-stu-id="1a872-114">This is good for line-of-business apps that require custom settings.</span></span> <span data-ttu-id="1a872-115">U kunt Hallo installatiekopie toowork voor Hallo app aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1a872-115">You can customize hello image toowork for hello app.</span></span>
* <span data-ttu-id="1a872-116">U kunt [maken en een aangepaste installatiekopie uploaden](remoteapp-create-custom-image.md).</span><span class="sxs-lookup"><span data-stu-id="1a872-116">You can [create and upload a custom image](remoteapp-create-custom-image.md).</span></span> <span data-ttu-id="1a872-117">Dit is geschikt als er al een afbeelding die u voor uw on-premises-implementatie voor extern bureaublad-Services gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1a872-117">This is good if you already have an image that you use for your on-premises Remote Desktop Services deployment.</span></span>
* <span data-ttu-id="1a872-118">U kunt een van de Hallo [sjablooninstallatiekopieën](remoteapp-images.md) opgenomen in uw RemoteApp-abonnement.</span><span class="sxs-lookup"><span data-stu-id="1a872-118">You can use one of hello [template images](remoteapp-images.md) included in your RemoteApp subscription.</span></span> <span data-ttu-id="1a872-119">Deze installatiekopieën worden gemaakt en onderhouden door Hallo RemoteApp-team en sommige standaard toepassingen (zoals Hallo Office suite) dat kunt u gebruikers van de beschikbare tooyour bevatten.</span><span class="sxs-lookup"><span data-stu-id="1a872-119">These images are created and maintained by hello RemoteApp team and contain some standard applications (like hello Office suite) that you can make available tooyour users.</span></span> <span data-ttu-id="1a872-120">Houd er rekening mee dat alleen Hallo Office 365 Pro Plus-installatiekopie kan worden gebruikt in een productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="1a872-120">Note that only hello Office 365 Pro Plus image can be used in a production setting.</span></span>

<span data-ttu-id="1a872-121">Ongeacht waar het verkrijgen van uw installatiekopie of hoe u dit hebt gemaakt, moet u zeker dat u begrijpt Hallo toomake [appvereisten](remoteapp-appreqs.md) tooensure die uw app goed in RemoteApp werkt.</span><span class="sxs-lookup"><span data-stu-id="1a872-121">Regardless of where you get your image or how you create it, you'll want toomake sure you understand hello [app requirements](remoteapp-appreqs.md) tooensure that your app works well in RemoteApp.</span></span> <span data-ttu-id="1a872-122">Vervolgens de volgende stap Hallo toocreate is een [cloud](remoteapp-create-cloud-deployment.md) of [hybride](remoteapp-create-hybrid-deployment.md) verzameling.</span><span class="sxs-lookup"><span data-stu-id="1a872-122">Then, hello next step is toocreate a [cloud](remoteapp-create-cloud-deployment.md) or [hybrid](remoteapp-create-hybrid-deployment.md) collection.</span></span>


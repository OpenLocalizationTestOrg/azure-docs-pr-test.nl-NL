---
title: Problemen met RemoteApp-collecties voor cloud - maken | Microsoft Docs
description: Meer informatie over het oplossen van fouten bij RemoteApp cloud verzameling maken
services: remoteapp
documentationcenter: 
author: vkbucha
manager: mbaldwin
ms.assetid: 95eb7797-7b5e-4781-ad23-f15dd85b213d
ms.service: remoteapp
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 304ba7c5057b27c459bccbb75d3a711567757675
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="8d42d-103">Verzamelingen van de cloud maken RemoteApp oplossen</span><span class="sxs-lookup"><span data-stu-id="8d42d-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="8d42d-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="8d42d-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="8d42d-105">Lees de [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8d42d-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="8d42d-106">Als u hebt met het maken van een cloudverzameling problemen, Raadpleeg de volgende informatie.</span><span class="sxs-lookup"><span data-stu-id="8d42d-106">If you are having problems creating a cloud collection, check out the following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="8d42d-107">Uw installatiekopie is ongeldig</span><span class="sxs-lookup"><span data-stu-id="8d42d-107">Your image is invalid</span></span>
<span data-ttu-id="8d42d-108">Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure voor het inrichten van uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon voldoet niet aan de [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="8d42d-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure to provision your collection, it means that your template image doesn't meet the [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="8d42d-109">Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer uw verzameling opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="8d42d-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try to create your collection again.</span></span>

## <a name="common-errors-seen-in-the-azure-management-portal"></a><span data-ttu-id="8d42d-110">Veelvoorkomende fouten in de Azure Management portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="8d42d-110">Common errors seen in the Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="8d42d-111">Verzamelingen vaak cloud is mislukt tijdens het maken van vanwege u gebruikmaakt van aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="8d42d-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="8d42d-112">Als u een van de bovenstaande fouten ziet en u een aangepaste installatiekopie gebruikt om de verzameling te maken, controleert u de volgende zaken:</span><span class="sxs-lookup"><span data-stu-id="8d42d-112">If you see one of the above errors and you are using a custom image to create the collection, please check the following things:</span></span>

* <span data-ttu-id="8d42d-113">Zorg ervoor dat de aangepaste installatiekopie die u hebt geüpload voldoet aan de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8d42d-113">Ensure that the custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="8d42d-114">Meestal is het algemene probleem dat de installatiekopie niet goed syspreped is.</span><span class="sxs-lookup"><span data-stu-id="8d42d-114">Most often the common problem is that the image was not properly syspreped.</span></span>  
* <span data-ttu-id="8d42d-115">Controleer of de installatiekopie kunt opstarten in Hyper-V of proberen te maken van een IAAS VM rechtstreeks in uw Azure-abonnement met behulp van de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8d42d-115">Verify the image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using the image.</span></span> <span data-ttu-id="8d42d-116">Als de virtuele machine niet kan worden opgestart en wordt niet gestart, klikt u vervolgens dit geeft meestal aan dat de aangepaste installatiekopie niet juist is voorbereid.</span><span class="sxs-lookup"><span data-stu-id="8d42d-116">If the VM fails to boot and not start, then this usually indicates that the custom image was not prepared correctly.</span></span>  <span data-ttu-id="8d42d-117">Controleer of de aangepaste installatiekopie is gemaakt met het volgende op de manier waarop de installatiekopie van een aangepaste sjabloon maken voor RemoteApp</span><span class="sxs-lookup"><span data-stu-id="8d42d-117">Verify the custom image was built following the How to create a custom template image for RemoteApp</span></span>

<span data-ttu-id="8d42d-118">Als u van een van de Microsoft-installatiekopieën die deel uitmaakt van uw abonnement gebruikmaakt, kunt u de verzameling opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="8d42d-118">If you are using one of the Microsoft images included with your subscription, try to create the collection again.</span></span> <span data-ttu-id="8d42d-119">Als het probleem zich blijft voordoen vervolgens Neem contact op met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="8d42d-119">If the issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="8d42d-120">Als u deze fout ziet dit betekent meestal dat die u naar een betaald account is bijgewerkt, maar u probeert een afbeelding van Microsoft die geldig alleen tijdens de proefmodus van de service te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8d42d-120">If you see this error this usually means that you been upgraded to a paid account but you are trying to use a Microsoft provided image that is valid only during the trial mode of the service.</span></span> <span data-ttu-id="8d42d-121">In dit geval probeert te maken van uw cloudverzameling opnieuw, maar zorg ervoor dat u de juiste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="8d42d-121">In this case, try to create your cloud collection again, but be sure to specify the correct image.</span></span>


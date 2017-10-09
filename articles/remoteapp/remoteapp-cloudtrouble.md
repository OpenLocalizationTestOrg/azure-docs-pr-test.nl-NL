---
title: 'aaaTroubleshoot RemoteApp cloudverzamelingen: maken | Microsoft Docs'
description: Meer informatie over hoe tootroubleshoot RemoteApp cloud fouten bij het maken van de verzameling
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
ms.openlocfilehash: 9484ecbdb048ede8df725215b313e049cc7648f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-remoteapp-cloud-collections"></a><span data-ttu-id="b508a-103">Verzamelingen van de cloud maken RemoteApp oplossen</span><span class="sxs-lookup"><span data-stu-id="b508a-103">Troubleshoot creating RemoteApp cloud collections</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b508a-104">Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld.</span><span class="sxs-lookup"><span data-stu-id="b508a-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b508a-105">Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b508a-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="b508a-106">Als u hebt met het maken van een cloudverzameling problemen, Raadpleeg Hallo informatie te volgen.</span><span class="sxs-lookup"><span data-stu-id="b508a-106">If you are having problems creating a cloud collection, check out hello following information.</span></span>

## <a name="your-image-is-invalid"></a><span data-ttu-id="b508a-107">Uw installatiekopie is ongeldig</span><span class="sxs-lookup"><span data-stu-id="b508a-107">Your image is invalid</span></span>
<span data-ttu-id="b508a-108">Als u een bericht zoals 'GoldImageInvalid' ziet wanneer u Azure tooprovision uw verzameling wacht, betekent dit dat de installatiekopie van uw sjabloon Hallo voldoet niet aan [installatiekopie vereisten gedefinieerd](remoteapp-imagereqs.md).</span><span class="sxs-lookup"><span data-stu-id="b508a-108">If you see a message like, "GoldImageInvalid" when you are waiting for Azure tooprovision your collection, it means that your template image doesn't meet hello [defined image requirements](remoteapp-imagereqs.md).</span></span> <span data-ttu-id="b508a-109">Ja, Ga lezen die [vereisten](remoteapp-imagereqs.md). Corrigeer de afbeelding, en probeer toocreate uw verzameling opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b508a-109">So, go read those [requirements](remoteapp-imagereqs.md), fix your image, and try toocreate your collection again.</span></span>

## <a name="common-errors-seen-in-hello-azure-management-portal"></a><span data-ttu-id="b508a-110">Veelvoorkomende fouten in hello Azure Management portal weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b508a-110">Common errors seen in hello Azure Management portal</span></span>
    DNS server could not be reached
    ProvisioningTimeout

<span data-ttu-id="b508a-111">Verzamelingen vaak cloud is mislukt tijdens het maken van vanwege u gebruikmaakt van aangepaste installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="b508a-111">Cloud collections often fail during creation because of you are using custom images.</span></span>  <span data-ttu-id="b508a-112">Als u een Hallo hierboven fouten ziet en u een aangepaste installatiekopie toocreate Hallo verzameling gebruikt, controleert u Hallo dingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b508a-112">If you see one of hello above errors and you are using a custom image toocreate hello collection, please check hello following things:</span></span>

* <span data-ttu-id="b508a-113">Zorg ervoor dat Hallo aangepaste installatiekopie die u hebt geüpload voldoet aan de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b508a-113">Ensure that hello custom image you uploaded meets image requirements.</span></span>
* <span data-ttu-id="b508a-114">Meest voorkomende Hallo probleem is dat die Hallo-installatiekopie is niet goed syspreped.</span><span class="sxs-lookup"><span data-stu-id="b508a-114">Most often hello common problem is that hello image was not properly syspreped.</span></span>  
* <span data-ttu-id="b508a-115">Controleer of Hallo installatiekopie kunt opstarten in Hyper-V of proberen te maken van een IAAS VM rechtstreeks in uw Azure-abonnement met Hallo-installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b508a-115">Verify hello image can boot within Hyper-V or try creating an IAAS VM directly in your Azure subscription using hello image.</span></span> <span data-ttu-id="b508a-116">Als Hallo VM tooboot en niet starten mislukt, klikt u vervolgens duidt dit meestal dat die Hallo aangepaste installatiekopie is niet correct voorbereid.</span><span class="sxs-lookup"><span data-stu-id="b508a-116">If hello VM fails tooboot and not start, then this usually indicates that hello custom image was not prepared correctly.</span></span>  <span data-ttu-id="b508a-117">Controleer of de aangepaste installatiekopie Hallo is opgebouwd na Hallo hoe toocreate een aangepaste sjablooninstallatiekopie voor RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b508a-117">Verify hello custom image was built following hello How toocreate a custom template image for RemoteApp</span></span>

<span data-ttu-id="b508a-118">Als u van een van Hallo Microsoft installatiekopieën zijn opgenomen in uw abonnement gebruikmaakt, probeert u opnieuw toocreate Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="b508a-118">If you are using one of hello Microsoft images included with your subscription, try toocreate hello collection again.</span></span> <span data-ttu-id="b508a-119">Als Hallo probleem zich blijft voordoen vervolgens Neem contact op met Microsoft ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="b508a-119">If hello issue persists then please contact Microsoft support.</span></span>

    PlatformImageTrialModeOnly

<span data-ttu-id="b508a-120">Als u deze fout ziet dit betekent meestal dat u bijgewerkt tooa betaald account en u probeert een installatiekopie van Microsoft die geldig is tijdens de proefmodus van Hallo service Hallo toouse.</span><span class="sxs-lookup"><span data-stu-id="b508a-120">If you see this error this usually means that you been upgraded tooa paid account but you are trying toouse a Microsoft provided image that is valid only during hello trial mode of hello service.</span></span> <span data-ttu-id="b508a-121">In dit geval probeert toocreate uw cloudverzameling opnieuw worden echter zeker toospecify Hallo juiste installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="b508a-121">In this case, try toocreate your cloud collection again, but be sure toospecify hello correct image.</span></span>


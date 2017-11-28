---
title: beperkingen van aaaAzure Cloud Shell (Preview) | Microsoft Docs
description: Overzicht van de beperkingen van Azure Cloud Shell
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="cbd9d-103">Beperkingen van de Azure-Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="cbd9d-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="cbd9d-104">Azure Cloud-Shell heeft Hallo bekende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="cbd9d-104">Azure Cloud Shell has hello following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="cbd9d-105">Systeemstatus en persistentie</span><span class="sxs-lookup"><span data-stu-id="cbd9d-105">System state and persistence</span></span>
<span data-ttu-id="cbd9d-106">Hallo-machine waarmee u uw Cloud-Shell-sessie is tijdelijk en deze wordt gerecycled nadat uw sessie is niet actief is gedurende 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-106">hello machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="cbd9d-107">Cloud-Shell vereist een bestandsshare toobe gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-107">Cloud Shell requires a file share toobe mounted.</span></span> <span data-ttu-id="cbd9d-108">Uw abonnement moet als gevolg hiervan kunnen tooset up opslag resources tooaccess Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-108">As a result, your subscription must be able tooset up storage resources tooaccess Cloud Shell.</span></span> <span data-ttu-id="cbd9d-109">Andere overwegingen zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="cbd9d-109">Other considerations include:</span></span>
* <span data-ttu-id="cbd9d-110">Met gekoppelde opslag, alleen de wijzigingen in uw `$Home` directory of `clouddrive` directory blijven bestaan.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="cbd9d-111">Bestandsshares worden gekoppeld, alleen vanuit uw [regio toegewezen](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="cbd9d-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="cbd9d-112">Azure Files ondersteunt alleen lokaal redundante opslag en geo-redundant storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="cbd9d-113">Gebruikersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="cbd9d-113">User permissions</span></span>
<span data-ttu-id="cbd9d-114">Machtigingen zijn ingesteld als gewone gebruikers zonder toegang tot sudo.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="cbd9d-115">Elke installatie buiten uw `$Home` directory niet bewaard.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="cbd9d-116">Hoewel bepaalde opdrachten binnen Hallo `clouddrive` map zoals `git clone`, beschikt niet over de juiste machtigingen, uw `$Home` directory is gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-116">Although certain commands within hello `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="cbd9d-117">Browserondersteuning</span><span class="sxs-lookup"><span data-stu-id="cbd9d-117">Browser support</span></span>
<span data-ttu-id="cbd9d-118">Cloud-Shell ondersteunt Hallo nieuwste versies van Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox en Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-118">Cloud Shell supports hello latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="cbd9d-119">Safari in privé-modus wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="cbd9d-120">Kopiëren en plakken</span><span class="sxs-lookup"><span data-stu-id="cbd9d-120">Copy and paste</span></span>
<span data-ttu-id="cbd9d-121">CTRL + C en Ctrl + V werken niet zoals kopiëren en plakken snelkoppelingen in de Cloud-Shell op Windows-machines, gebruikt u Ctrl + Insert en Shift + Insert toocopy- en respectievelijk plakken.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert toocopy and paste respectively.</span></span>

<span data-ttu-id="cbd9d-122">Klik met de rechtermuisknop kopiëren en plakken opties zijn ook beschikbaar, maar met de rechtermuisknop op de functie is onderwerp toobrowser-specifieke Klembord toegang.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-122">Right-click copy-and-paste options are also available, but right-click function is subject toobrowser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="cbd9d-123">.Bashrc bewerken</span><span class="sxs-lookup"><span data-stu-id="cbd9d-123">Editing .bashrc</span></span>
<span data-ttu-id="cbd9d-124">Waarschuwing nemen bij het bewerken van .bashrc, in dat geval kan leiden tot onverwachte fouten in de Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="cbd9d-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="cbd9d-125">.bash_history</span></span>
<span data-ttu-id="cbd9d-126">De geschiedenis van bash opdrachten mogelijk inconsistent vanwege Cloud Shell-sessie wordt onderbroken of gelijktijdige sessies.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="cbd9d-127">Limieten voor Resourcegebruik</span><span class="sxs-lookup"><span data-stu-id="cbd9d-127">Usage limits</span></span>
<span data-ttu-id="cbd9d-128">Cloud-Shell is bedoeld voor interactieve gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="cbd9d-129">Als gevolg hiervan zijn geen niet-interactieve sessies langlopende beëindigd zonder waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="cbd9d-130">Netwerkverbinding</span><span class="sxs-lookup"><span data-stu-id="cbd9d-130">Network connectivity</span></span>
<span data-ttu-id="cbd9d-131">Eventuele latentie in de Cloud-Shell onderwerp toolocal internetverbinding, Cloud Shell blijft tooattempt toocarry uit instructies die zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="cbd9d-131">Any latency in Cloud Shell is subject toolocal internet connectivity, Cloud Shell continues tooattempt toocarry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbd9d-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cbd9d-132">Next steps</span></span>
[<span data-ttu-id="cbd9d-133">Cloud-Shell Quick Start</span><span class="sxs-lookup"><span data-stu-id="cbd9d-133">Cloud Shell Quickstart</span></span>](quickstart.md)

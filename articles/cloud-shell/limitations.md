---
title: Beperkingen voor Azure Cloud-Shell (Preview) | Microsoft Docs
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
ms.openlocfilehash: e42841b126a9df9240bec3f489589d5ce4a6db80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="limitations-of-azure-cloud-shell"></a><span data-ttu-id="535a0-103">Beperkingen van de Azure-Cloud-Shell</span><span class="sxs-lookup"><span data-stu-id="535a0-103">Limitations of Azure Cloud Shell</span></span>
<span data-ttu-id="535a0-104">Azure Cloud-Shell heeft de volgende beperkingen:</span><span class="sxs-lookup"><span data-stu-id="535a0-104">Azure Cloud Shell has the following known limitations:</span></span>

## <a name="system-state-and-persistence"></a><span data-ttu-id="535a0-105">Systeemstatus en persistentie</span><span class="sxs-lookup"><span data-stu-id="535a0-105">System state and persistence</span></span>
<span data-ttu-id="535a0-106">De computer waarmee u uw Cloud-Shell-sessie is tijdelijk en deze wordt gerecycled nadat uw sessie is niet actief is gedurende 20 minuten.</span><span class="sxs-lookup"><span data-stu-id="535a0-106">The machine that provides your Cloud Shell session is temporary, and it is recycled after your session is inactive for 20 minutes.</span></span> <span data-ttu-id="535a0-107">Cloud-Shell vereist een bestandsshare te koppelen.</span><span class="sxs-lookup"><span data-stu-id="535a0-107">Cloud Shell requires a file share to be mounted.</span></span> <span data-ttu-id="535a0-108">Uw abonnement moet als gevolg hiervan kunnen storage-resources instellen voor toegang tot Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="535a0-108">As a result, your subscription must be able to set up storage resources to access Cloud Shell.</span></span> <span data-ttu-id="535a0-109">Andere overwegingen zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="535a0-109">Other considerations include:</span></span>
* <span data-ttu-id="535a0-110">Met gekoppelde opslag, alleen de wijzigingen in uw `$Home` directory of `clouddrive` directory blijven bestaan.</span><span class="sxs-lookup"><span data-stu-id="535a0-110">With mounted storage, only modifications within your `$Home` directory or `clouddrive` directory are persisted.</span></span>
* <span data-ttu-id="535a0-111">Bestandsshares worden gekoppeld, alleen vanuit uw [regio toegewezen](persisting-shell-storage.md#mount-a-new-clouddrive).</span><span class="sxs-lookup"><span data-stu-id="535a0-111">File shares can be mounted only from within your [assigned region](persisting-shell-storage.md#mount-a-new-clouddrive).</span></span>
* <span data-ttu-id="535a0-112">Azure Files ondersteunt alleen lokaal redundante opslag en geo-redundant storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="535a0-112">Azure Files supports only locally redundant storage and geo-redundant storage accounts.</span></span>

## <a name="user-permissions"></a><span data-ttu-id="535a0-113">Gebruikersmachtigingen</span><span class="sxs-lookup"><span data-stu-id="535a0-113">User permissions</span></span>
<span data-ttu-id="535a0-114">Machtigingen zijn ingesteld als gewone gebruikers zonder toegang tot sudo.</span><span class="sxs-lookup"><span data-stu-id="535a0-114">Permissions are set as regular users without sudo access.</span></span> <span data-ttu-id="535a0-115">Elke installatie buiten uw `$Home` directory niet bewaard.</span><span class="sxs-lookup"><span data-stu-id="535a0-115">Any installation outside your `$Home` directory will not persist.</span></span>
<span data-ttu-id="535a0-116">Hoewel bepaalde opdrachten binnen de `clouddrive` map zoals `git clone`, beschikt niet over de juiste machtigingen, uw `$Home` directory is gemachtigd.</span><span class="sxs-lookup"><span data-stu-id="535a0-116">Although certain commands within the `clouddrive` directory, such as `git clone`, do not have proper permissions, your `$Home` directory does have permissions.</span></span>

## <a name="browser-support"></a><span data-ttu-id="535a0-117">Browserondersteuning</span><span class="sxs-lookup"><span data-stu-id="535a0-117">Browser support</span></span>
<span data-ttu-id="535a0-118">Cloud-Shell biedt ondersteuning voor de nieuwste versies van Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox en Apple Safari.</span><span class="sxs-lookup"><span data-stu-id="535a0-118">Cloud Shell supports the latest versions of Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox, and Apple Safari.</span></span> <span data-ttu-id="535a0-119">Safari in privé-modus wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="535a0-119">Safari in private mode is not supported.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="535a0-120">Kopiëren en plakken</span><span class="sxs-lookup"><span data-stu-id="535a0-120">Copy and paste</span></span>
<span data-ttu-id="535a0-121">CTRL + C en Ctrl + V niet werken als kopiëren en plakken snelkoppelingen in de Cloud-Shell op Windows-machines, gebruik Ctrl + Insert en Shift + Insert kopiëren en plakken, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="535a0-121">Ctrl+C and Ctrl+V do not function as copy/paste shortcuts in Cloud Shell on Windows machines, use Ctrl+Insert and Shift+Insert to copy and paste respectively.</span></span>

<span data-ttu-id="535a0-122">Klik met de rechtermuisknop kopiëren en plakken opties zijn ook beschikbaar, maar met de rechtermuisknop op de functie is onderworpen aan de browser-specifieke Klembord toegang.</span><span class="sxs-lookup"><span data-stu-id="535a0-122">Right-click copy-and-paste options are also available, but right-click function is subject to browser-specific clipboard access.</span></span>

## <a name="editing-bashrc"></a><span data-ttu-id="535a0-123">.Bashrc bewerken</span><span class="sxs-lookup"><span data-stu-id="535a0-123">Editing .bashrc</span></span>
<span data-ttu-id="535a0-124">Waarschuwing nemen bij het bewerken van .bashrc, in dat geval kan leiden tot onverwachte fouten in de Cloud-Shell.</span><span class="sxs-lookup"><span data-stu-id="535a0-124">Take caution when editing .bashrc, doing so can cause unexpected errors in Cloud Shell.</span></span>

## <a name="bashhistory"></a><span data-ttu-id="535a0-125">.bash_history</span><span class="sxs-lookup"><span data-stu-id="535a0-125">.bash_history</span></span>
<span data-ttu-id="535a0-126">De geschiedenis van bash opdrachten mogelijk inconsistent vanwege Cloud Shell-sessie wordt onderbroken of gelijktijdige sessies.</span><span class="sxs-lookup"><span data-stu-id="535a0-126">Your history of bash commands may be inconsistent because of Cloud Shell session disruption or concurrent sessions.</span></span>

## <a name="usage-limits"></a><span data-ttu-id="535a0-127">Limieten voor Resourcegebruik</span><span class="sxs-lookup"><span data-stu-id="535a0-127">Usage limits</span></span>
<span data-ttu-id="535a0-128">Cloud-Shell is bedoeld voor interactieve gebruiksvoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="535a0-128">Cloud Shell is intended for interactive use cases.</span></span> <span data-ttu-id="535a0-129">Als gevolg hiervan zijn geen niet-interactieve sessies langlopende beëindigd zonder waarschuwing.</span><span class="sxs-lookup"><span data-stu-id="535a0-129">As a result, any long-running non-interactive sessions are ended without warning.</span></span>

## <a name="network-connectivity"></a><span data-ttu-id="535a0-130">Netwerkverbinding</span><span class="sxs-lookup"><span data-stu-id="535a0-130">Network connectivity</span></span>
<span data-ttu-id="535a0-131">Eventuele latentie in de Cloud-Shell is onderworpen aan de lokale verbinding met internet, Cloud Shell blijft proberen bij het uitvoeren van de instructies die zijn verzonden.</span><span class="sxs-lookup"><span data-stu-id="535a0-131">Any latency in Cloud Shell is subject to local internet connectivity, Cloud Shell continues to attempt to carry out any instructions sent.</span></span>

## <a name="next-steps"></a><span data-ttu-id="535a0-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="535a0-132">Next steps</span></span>
[<span data-ttu-id="535a0-133">Cloud-Shell Quick Start</span><span class="sxs-lookup"><span data-stu-id="535a0-133">Cloud Shell Quickstart</span></span>](quickstart.md)

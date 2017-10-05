---
title: Een Azure Linux VM-ID ophalen | Microsoft Docs
description: Hierin wordt beschreven hoe halen en gebruik van een Azure Linux VM unieke ID.
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 136c5d28-ff6b-4466-b27f-7a29785b5d27
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 01/23/2017
ms.author: kmouss
ms.openlocfilehash: 258ce425d5692730011cf2f4468dc0ba77f4cb79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="4f97b-103">Toegang tot en met behulp van de unieke ID van Azure VM</span><span class="sxs-lookup"><span data-stu-id="4f97b-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="4f97b-104">De unieke ID van de Azure VM is een id 128 bits gecodeerd en opgeslagen in alle Azure IaaS VM's SMBIOS en kan op dit moment worden gelezen met platform BIOS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="4f97b-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="4f97b-105">De unieke ID van de Azure VM is een alleen-lezen eigenschap.</span><span class="sxs-lookup"><span data-stu-id="4f97b-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="4f97b-106">Azure unieke ID van de VM niet veranderd bij opnieuw opstarten afsluiting van (hetzij geplande voor niet-geplande), starten/stoppen ongedaan toewijzen, service-herstel of terugzetten aanwezig.</span><span class="sxs-lookup"><span data-stu-id="4f97b-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="4f97b-107">Als de virtuele machine een momentopname is en voor het maken van een nieuw exemplaar gekopieerd, wordt echter nieuwe Azure VM-ID geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4f97b-107">However, if the VM is a snapshot and copied to create a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="4f97b-108">Als u oudere VMs gemaakt en uw virtuele machine automatisch ophalen van een Azure unieke id uitgevoerd sinds deze nieuwe functie kreeg uitgerold (18 September 2014), neem opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="4f97b-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM to automatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="4f97b-109">Toegang krijgen tot Azure unieke ID van VM uit vanuit de virtuele machine:</span><span class="sxs-lookup"><span data-stu-id="4f97b-109">To access Azure Unique VM ID from within the VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="4f97b-110">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="4f97b-110">Create a VM</span></span>
<span data-ttu-id="4f97b-111">Zie voor meer informatie [een virtuele Machine maken](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4f97b-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="4f97b-112">Verbinding maken met de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="4f97b-112">Connect to the VM</span></span>
<span data-ttu-id="4f97b-113">Zie voor meer informatie [SSH in Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="4f97b-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="4f97b-114">De unieke ID van de query VM</span><span class="sxs-lookup"><span data-stu-id="4f97b-114">Query VM Unique ID</span></span>
<span data-ttu-id="4f97b-115">Opdracht (voorbeeld wordt **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="4f97b-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="4f97b-116">Voorbeeld van de verwachte resultaten:</span><span class="sxs-lookup"><span data-stu-id="4f97b-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="4f97b-117">Als gevolg van Big Endian bit ordening, zijn werkelijke unieke ID van de VM in dit geval:</span><span class="sxs-lookup"><span data-stu-id="4f97b-117">Due to Big Endian bit ordering, the actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="4f97b-118">De unieke ID van de Azure VM kan worden gebruikt in verschillende scenario's of de virtuele machine wordt uitgevoerd op Azure of on-premises en kan helpen uw licentiegegevens, rapportage of algemene bijhouden-vereisten die u van uw Azure IaaS-implementaties misschien.</span><span class="sxs-lookup"><span data-stu-id="4f97b-118">Azure VM unique ID can be used in different scenarios whether the VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="4f97b-119">Kunnen het veel onafhankelijke softwareleveranciers bouwen van toepassingen en gecertificeerd door ze in Azure nodig te identificeren van een Azure VM gedurende de levenscyclus en zien of als de virtuele machine wordt uitgevoerd op Azure, on-Premises of op andere cloudproviders.</span><span class="sxs-lookup"><span data-stu-id="4f97b-119">Many independent software vendors building applications and certifying them on Azure may require to identify an Azure VM throughout its lifecycle and to tell if the VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="4f97b-120">Deze platform-id kan bijvoorbeeld helpen detecteren als de software correct is gelicentieerd of kunnen geen VM-gegevens naar de bron, zoals correleren om u te helpen bij het instellen van de juiste metrische gegevens voor de juiste platform en voor het bijhouden en deze metrische gegevens voor ander gebruik correleren.</span><span class="sxs-lookup"><span data-stu-id="4f97b-120">This platform identifier can for example help detect if the software is properly licensed or help to correlate any VM data to its source such as to assist on setting the right metrics for the right platform and to track and correlate these metrics amongst other uses.</span></span>


---
title: een Azure Linux VM-ID aaaGet | Microsoft Docs
description: Hierin wordt beschreven hoe tooget en gebruik een unieke Azure Linux VM-id.
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
ms.openlocfilehash: 4c8ddfc2e892824581e77649285ee8adbccd5def
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-and-using-azure-vm-unique-id"></a><span data-ttu-id="c5ad3-103">Toegang tot en met behulp van de unieke ID van Azure VM</span><span class="sxs-lookup"><span data-stu-id="c5ad3-103">Accessing and Using Azure VM Unique ID</span></span>
<span data-ttu-id="c5ad3-104">De unieke ID van de Azure VM is een id 128 bits gecodeerd en opgeslagen in alle Azure IaaS VM's SMBIOS en kan op dit moment worden gelezen met platform BIOS-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-104">Azure VM unique ID is a 128bits identifier encoded and stored in all Azure IaaS VM’s SMBIOS and can currently be read using platform BIOS commands.</span></span>

<span data-ttu-id="c5ad3-105">De unieke ID van de Azure VM is een alleen-lezen eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-105">Azure VM unique ID is a Read-only property.</span></span> <span data-ttu-id="c5ad3-106">Azure unieke ID van de VM niet veranderd bij opnieuw opstarten afsluiting van (hetzij geplande voor niet-geplande), starten/stoppen ongedaan toewijzen, service-herstel of terugzetten aanwezig.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-106">Azure Unique VM ID won’t change upon reboot shutdown (either planned for unplanned), Start/Stop de-allocate, service healing or restore in place.</span></span> <span data-ttu-id="c5ad3-107">Nieuwe Azure VM-ID wordt is geconfigureerd als Hallo VM een momentopname en gekopieerde toocreate een nieuw exemplaar is.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-107">However, if hello VM is a snapshot and copied toocreate a new instance, new Azure VM ID is configured.</span></span>

> [!NOTE]
> <span data-ttu-id="c5ad3-108">Als u oudere VM's die zijn gemaakt en uitgevoerd sinds deze nieuwe functie (18 September 2014), hebt u uitgerold Start uw tooautomatically VM ophalen Azure unieke ID.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-108">If you have older VMs created and running since this new feature got rolled out (September 18, 2014), please restart your VM tooautomatically get an Azure unique ID.</span></span>
> 
> 

<span data-ttu-id="c5ad3-109">tooaccess Azure unieke ID van VM uit binnen Hallo VM:</span><span class="sxs-lookup"><span data-stu-id="c5ad3-109">tooaccess Azure Unique VM ID from within hello VM:</span></span>

## <a name="create-a-vm"></a><span data-ttu-id="c5ad3-110">Een virtuele machine maken</span><span class="sxs-lookup"><span data-stu-id="c5ad3-110">Create a VM</span></span>
<span data-ttu-id="c5ad3-111">Zie voor meer informatie [een virtuele Machine maken](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c5ad3-111">For more information, see [Create a Virtual Machine](../windows/creation-choices.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="connect-toohello-vm"></a><span data-ttu-id="c5ad3-112">Verbinding maken met toohello VM</span><span class="sxs-lookup"><span data-stu-id="c5ad3-112">Connect toohello VM</span></span>
<span data-ttu-id="c5ad3-113">Zie voor meer informatie [SSH in Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="c5ad3-113">For more information, see [SSH from Linux](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

## <a name="query-vm-unique-id"></a><span data-ttu-id="c5ad3-114">De unieke ID van de query VM</span><span class="sxs-lookup"><span data-stu-id="c5ad3-114">Query VM Unique ID</span></span>
<span data-ttu-id="c5ad3-115">Opdracht (voorbeeld wordt **Ubuntu**):</span><span class="sxs-lookup"><span data-stu-id="c5ad3-115">Command (example uses **Ubuntu**):</span></span>

```bash
sudo dmidecode | grep UUID
```

<span data-ttu-id="c5ad3-116">Voorbeeld van de verwachte resultaten:</span><span class="sxs-lookup"><span data-stu-id="c5ad3-116">Example Expected Results:</span></span>

```bash
UUID: 090556DA-D4FA-764F-A9F1-63614EDA019A
```

<span data-ttu-id="c5ad3-117">Vervaldatum tooBig Endian bits ordening, zijn hello werkelijke unieke ID van de VM in dit geval:</span><span class="sxs-lookup"><span data-stu-id="c5ad3-117">Due tooBig Endian bit ordering, hello actual Unique VM ID in this case will be:</span></span>

```bash
DA 56 05 09 – FA D4 – 4f 76 - A9F1-63614EDA019A
```

<span data-ttu-id="c5ad3-118">De unieke ID van de Azure VM kan worden gebruikt in verschillende scenario's of Hallo VM wordt uitgevoerd op Azure of on-premises en kan helpen uw licentiegegevens, rapportage of algemene bijhouden-vereisten die u van uw Azure IaaS-implementaties misschien.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-118">Azure VM unique ID can be used in different scenarios whether hello VM is running on Azure or on-premises and can help your licensing, reporting or general tracking requirements you may have on your Azure IaaS deployments.</span></span> <span data-ttu-id="c5ad3-119">Veel onafhankelijke softwareleveranciers bouwen van toepassingen en gecertificeerd door ze in Azure moet mogelijk een Azure VM gedurende de levensduur en tootell tooidentify als Hallo VM wordt uitgevoerd op Azure, on-Premises of andere cloudproviders.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-119">Many independent software vendors building applications and certifying them on Azure may require tooidentify an Azure VM throughout its lifecycle and tootell if hello VM is running on Azure, on-Premises or on other cloud providers.</span></span> <span data-ttu-id="c5ad3-120">Deze platform-id kunt bijvoorbeeld detecteren als Hallo-software correct is gelicentieerd of help toocorrelate elke VM tooits gegevensbron zoals tooassist over het instellen van de metrische gegevens voor Hallo rechts voor de juiste platform Hallo en tootrack en deze metrische gegevens voor de correleren andere toepassingen.</span><span class="sxs-lookup"><span data-stu-id="c5ad3-120">This platform identifier can for example help detect if hello software is properly licensed or help toocorrelate any VM data tooits source such as tooassist on setting hello right metrics for hello right platform and tootrack and correlate these metrics amongst other uses.</span></span>


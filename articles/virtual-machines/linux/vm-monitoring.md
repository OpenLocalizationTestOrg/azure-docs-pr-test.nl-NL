---
title: aaaEnable- of uitschakelen van Azure VM-bewaking
description: Hierin wordt beschreven hoe tooEnable of Azure-VM Monitoring uitschakelen
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="5f7c3-103">Of schakel bewaking van de Azure VM</span><span class="sxs-lookup"><span data-stu-id="5f7c3-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="5f7c3-104">Deze sectie beschrijft hoe tooenable of schakel bewaking op virtuele machines in Azure wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="5f7c3-105">U kunt in- of uitschakelen bewaking met Hallo portal of Azure-opdrachtregelinterface voor Mac, Linux en Windows (hello Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="5f7c3-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f7c3-106">Dit document beschrijft versie 2.3 Hallo Linux diagnostische extensie, die is afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="5f7c3-107">Versie 2.3 worden tot en met 30 juni 2018 ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="5f7c3-108">Versie 3.0 Hallo diagnostische Linux-extensie kan in plaats daarvan worden ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="5f7c3-109">Zie voor meer informatie [Hallo documentatie](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="5f7c3-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="5f7c3-110">Inschakelen / uitschakelen bewaking via hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="5f7c3-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="5f7c3-111">U kunt inschakelen bewaking van uw virtuele machine van Azure, waardoor gegevens over uw exemplaar in perioden van 1 minuut.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="5f7c3-112">(wijzigingen van de opslag van toepassing).</span><span class="sxs-lookup"><span data-stu-id="5f7c3-112">(storage changes apply).</span></span> <span data-ttu-id="5f7c3-113">Gedetailleerde diagnostische gegevens is vervolgens beschikbaar voor Hallo VM in de portal grafieken Hallo of via Hallo API.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="5f7c3-114">Standaard kan Azure-portal bewaking op basis van een host voor een beperkte set van metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="5f7c3-115">U kunt inschakelen bewaking van metrische gegevens van binnen een virtuele machine tijdens het Hallo die VM wordt uitgevoerd of gestopt.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="5f7c3-116">Open hello Azure portal op [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5f7c3-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="5f7c3-117">Klik in het Hallo linkernavigatiebalk, virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="5f7c3-118">Selecteer een exemplaar uitgevoerd of gestopt op Hallo lijst met virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="5f7c3-119">Hallo 'Virtuele machine' blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="5f7c3-120">Klik op alle instellingen.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-120">Click All settings.</span></span>
* <span data-ttu-id="5f7c3-121">Klik op diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-121">Click Diagnostics.</span></span>
* <span data-ttu-id="5f7c3-122">Status tooOn wijzigen of uit.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-122">Change status tooOn or Off.</span></span> <span data-ttu-id="5f7c3-123">U kunt er ook voor kiezen in deze blade Hallo niveau bewaking details die u wilt tooenable voor uw virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Inschakelen / uitschakelen bewaking via hello Azure-portal.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="5f7c3-125">Inschakelen / uitschakelen bewaking met Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5f7c3-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="5f7c3-126">tooenable bewaking voor een virtuele machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="5f7c3-127">Maak een bestand (met de naam zoals PrivateConfig.json):</span><span class="sxs-lookup"><span data-stu-id="5f7c3-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="5f7c3-128">Hallo-uitbreiding via Azure CLI inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5f7c3-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="5f7c3-129">Zie voor meer informatie [de prestaties en diagnostische gegevens met behulp van Linux diagnostische extensie tooMonitor Linux VM's](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5f7c3-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png

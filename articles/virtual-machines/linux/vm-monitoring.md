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
# <a name="enable-or-disable-azure-vm-monitoring"></a>Of schakel bewaking van de Azure VM

Deze sectie beschrijft hoe tooenable of schakel bewaking op virtuele machines in Azure wordt uitgevoerd. U kunt in- of uitschakelen bewaking met Hallo portal of Azure-opdrachtregelinterface voor Mac, Linux en Windows (hello Azure CLI).

> [!IMPORTANT]
> Dit document beschrijft versie 2.3 Hallo Linux diagnostische extensie, die is afgeschaft. Versie 2.3 worden tot en met 30 juni 2018 ondersteund.
>
> Versie 3.0 Hallo diagnostische Linux-extensie kan in plaats daarvan worden ingeschakeld. Zie voor meer informatie [Hallo documentatie](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Inschakelen / uitschakelen bewaking via hello Azure-portal

U kunt inschakelen bewaking van uw virtuele machine van Azure, waardoor gegevens over uw exemplaar in perioden van 1 minuut. (wijzigingen van de opslag van toepassing). Gedetailleerde diagnostische gegevens is vervolgens beschikbaar voor Hallo VM in de portal grafieken Hallo of via Hallo API. Standaard kan Azure-portal bewaking op basis van een host voor een beperkte set van metrische gegevens. U kunt inschakelen bewaking van metrische gegevens van binnen een virtuele machine tijdens het Hallo die VM wordt uitgevoerd of gestopt.

* Open hello Azure portal op [https://portal.azure.com](https://portal.azure.com).
* Klik in het Hallo linkernavigatiebalk, virtuele machines.
* Selecteer een exemplaar uitgevoerd of gestopt op Hallo lijst met virtuele machines. Hallo 'Virtuele machine' blade wordt geopend.
* Klik op alle instellingen.
* Klik op diagnostische gegevens.
* Status tooOn wijzigen of uit. U kunt er ook voor kiezen in deze blade Hallo niveau bewaking details die u wilt tooenable voor uw virtuele machine.

![Inschakelen / uitschakelen bewaking via hello Azure-portal.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Inschakelen / uitschakelen bewaking met Azure CLI

tooenable bewaking voor een virtuele machine in Azure.

* Maak een bestand (met de naam zoals PrivateConfig.json):

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Hallo-uitbreiding via Azure CLI inschakelen.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Zie voor meer informatie [de prestaties en diagnostische gegevens met behulp van Linux diagnostische extensie tooMonitor Linux VM's](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png

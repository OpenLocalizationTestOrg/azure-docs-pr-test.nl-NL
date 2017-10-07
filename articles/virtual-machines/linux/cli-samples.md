---
title: Voorbeelden van de CLI aaaAzure | Microsoft Docs
description: Voorbeelden van Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Azure CLI-voorbeelden voor virtuele Linux-machines

Hallo bevat volgende tabel koppelingen toobash scripts gebouwd met behulp van hello Azure CLI.

| | |
|---|---|
|**Virtuele machines maken**||
| [Een virtuele machine maken](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Maakt een virtuele Linux-machine met een minimale configuratie. |
| [Een volledig geconfigureerde virtuele machine maken](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Een resourcegroep, virtuele machine en alle gerelateerde resources gemaakt.|
| [Maximaal beschikbare virtuele machines maken](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Maakt verschillende virtuele machines in een maximaal beschikbare en configuratie van taakverdeling. |
| [Een virtuele machine maken met Docker ingeschakeld](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | Een virtuele machine maakt, configureert deze virtuele machine als een Docker-host en een NGINX-container wordt uitgevoerd. |
| [Een virtuele machine maken en voer het script voor configuratie](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Een virtuele machine maakt en hello Azure aangepast Script extensie tooinstall NGINX gebruikt. |
| [Een virtuele machine maken met WordPress geïnstalleerd](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Een virtuele machine maakt en hello Azure aangepast Script extensie tooinstall WordPress gebruikt. |
| [Een virtuele machine maken van een beheerde OS-schijf](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | Maakt een virtuele machine door het koppelen van een bestaande schijf beheerd als besturingssysteemschijf. |
| [Een virtuele machine maken vanuit een momentopname](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Een virtuele machine maakt vanuit een momentopname eerst een beheerde schijven maken vanuit een momentopname en vervolgens Hallo nieuwe beheerde schijf als besturingssysteemschijf te koppelen. |
|**Opslag beheren**||
| [Beheerde schijf vanaf een VHD maken](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | Een beheerde schijf maakt vanaf een speciale VHD als een besturingssysteemschijf of van een gegevensschijf VHD-gegevens.  |
| [Een beheerde schijf maken vanuit een momentopname](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Maakt een beheerde schijf van een momentopname. |
| [Toosame beheerde schijf of een ander abonnement niet kopiëren](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Exemplaren beheerd schijf toosame of een ander abonnement maar Hallo in dezelfde regio bevinden als Hallo bovenliggende schijf worden beheerd. 
| [Een momentopname exporteren als VHD tooa storage-account](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | Exporteert een momentopname van een beheerde als VHD tooa storage-account in andere regio. |
| [Momentopname toosame of een ander abonnement kopiëren](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Kopieën momentopname toosame of ander abonnement maar in Hallo dezelfde regio bevinden als Hallo bovenliggende momentopname. |
|**Virtuele machines**||
| [Beveiligen van netwerkverkeer tussen virtuele machines](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Hiermee maakt twee virtuele machines, alle gerelateerde resources en een interne en externe netwerkbeveiligingsgroepen (NSG). |
|**Beveiligde virtuele machines**||
| [Versleutelen van een VM- en gegevensschijven](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Een Azure Sleutelkluis, de versleutelingssleutel en de service-principal gemaakt en vervolgens een virtuele machine versleutelt. |
|**Virtuele machines bewaken**||
| [Monitor voor een virtuele machine bij Operations Management Suite](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Een virtuele machine maakt, Hallo Operations Management Suite-agent geïnstalleerd en schrijft Hallo VM in een OMS-werkruimte.  |
|**Problemen met virtuele machines**||
| [Problemen met een besturingssysteemschijf virtuele machines](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Koppelt de besturingssysteemschijf Hallo van een virtuele machine als een gegevensschijf op een tweede virtuele machine. |
| | |

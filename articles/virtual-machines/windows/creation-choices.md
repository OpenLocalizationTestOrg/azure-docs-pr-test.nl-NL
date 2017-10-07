---
title: aaaDifferent manieren toocreate een Windows-VM in Azure | Microsoft Docs
description: Geeft een lijst Hallo verschillende manieren toocreate virtuele Windows-machine met Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 809ba8f4-b54e-43c5-bbe3-8e710c49971f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/02/2017
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2928d4daa9b44c4d3a5083092a82c9a7f7c69fae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-windows-virtual-machine"></a>Verschillende manieren toocreate virtuele Windows-machine

Azure biedt verschillende manieren toocreate een virtuele machine omdat de virtuele machines zijn geschikt voor verschillende gebruikers en doelstellingen. Dit betekent dat u toomake enkele mogelijkheden over Hallo virtuele machine moet en hoe toocreate deze. In dit artikel krijgt u een overzicht van deze keuzes en tooinstructions koppelingen.

## <a name="azure-portal"></a>Azure Portal
Met behulp van hello Azure-portal is een eenvoudige manier tootry uit een virtuele machine, vooral als u net met Azure begint. 

[Maak een virtuele machine met Windows met behulp van Hallo-portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="template"></a>Template
Virtuele machines vereisen een combinatie van resources (zoals een beschikbare sets en storage-accounts). In plaats van te implementeren en beheren van elke resource afzonderlijk, kunt u een Azure Resource Manager-sjabloon die u implementeert en richt alle Hallo resources in een enkele, gecoördineerde bewerking.

* [Een virtuele Windows-machine maken met een Resource Manager-sjabloon](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="azure-powershell"></a>Azure PowerShell
Als u liever in een opdrachtshell werkt, kunt u Azure PowerShell.

* [Een Windows-VM maken met behulp van PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="visual-studio"></a>Visual Studio
Gebruik Visual Studio toobuild, beheren, en implementeren van virtuele machines met hello Azure Tools voor Visual Studio en hello Azure SDK.

[Azure-hulpprogramma's voor Visual Studio](https://www.visualstudio.com/features/azure-tools-vs)


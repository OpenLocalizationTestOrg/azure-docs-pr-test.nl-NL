---
title: aaaAdd burst knooppunten tooan HPC Pack cluster | Microsoft Docs
description: Meer informatie over hoe een HPC Pack tooexpand-cluster in Azure op aanvraag door toe te voegen worker rolinstanties uitgevoerd in een cloudservice
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 24b79a8a-24ad-4002-ae76-75abc9b28c83
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 10/14/2016
ms.author: danlep
ms.openlocfilehash: 7ec40ffe76485742c9e458ec49e11805990974e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-on-demand-burst-nodes-tooan-hpc-pack-cluster-in-azure"></a>On-demand 'burst' knooppunten tooan HPC Pack-cluster toevoegen in Azure
Als u een [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure, kunt u een manier tooquickly scale Hallo cluster capaciteit omhoog of omlaag, zonder het onderhouden van een reeks vooraf rekenknooppunt virtuele machines geconfigureerde. Dit artikel ziet u hoe tooadd on demand 'burst' knooppunten (worker-rolexemplaren in een cloudservice wordt uitgevoerd) als compute resources tooa hoofdknooppunt in Azure. 

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

![Burst knooppunten][burst]

Hallo stappen in dit artikel kunt u snel Azure knooppunten toevoegen tooa cloud-gebaseerde HPC Pack hoofdknooppunt VM voor de implementatie van een test of bewijs van het concept. Hallo hoofdstappen Hallo zijn hetzelfde zijn als Hallo stappen te 'burst tooAzure' tooadd cloud compute capaciteit tooan on-premises HPC Pack-cluster. Zie voor een zelfstudie [instellen van een hybride rekencluster met Microsoft HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md). Zie voor gedetailleerde richtlijnen en overwegingen voor productie-implementaties, [tooAzure met Microsoft HPC Pack Burst](https://technet.microsoft.com/library/gg481749.aspx).

## <a name="prerequisites"></a>Vereisten
* **HPC Pack hoofdknooppunt geïmplementeerd in een Azure VM** -kunt u een zelfstandige hoofdknooppunt VM of een die deel uitmaakt van een groter cluster. een zelfstandige hoofdknooppunt toocreate Zie [implementeren van een HPC Pack hoofdknooppunt in een Azure VM](../../virtual-machines-windows-hpcpack-cluster-headnode.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Zie voor geautomatiseerde HPC Pack cluster implementatieopties [toocreate opties en beheren van een Windows HPC-cluster in Azure met Microsoft HPC Pack](../../virtual-machines-windows-hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
  
  > [!TIP]
  > Als u Hallo [HPC Pack IaaS-implementatiescript](hpcpack-cluster-powershell-script.md) toocreate Hallo-cluster in Azure, kunt u Azure burst knooppunten in uw automatische implementatie. Zie Hallo voorbeelden in dit artikel.
  > 
  > 
* **Azure-abonnement** -tooadd Azure knooppunten, kunt u Hallo hetzelfde abonnement dat u gebruikt toodeploy Hallo hoofdknooppunt VM, of een ander abonnement (of abonnementen).
* **Quotum voor kernen** -moet u mogelijk tooincrease Hallo quotum van kernen, met name als u verschillende Azure knooppunten met multicore grootten toodeploy kiezen. een quotum tooincrease [opent u een ondersteuningsaanvraag online klant](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) zonder kosten.

## <a name="step-1-create-a-cloud-service-and-a-storage-account-for-hello-azure-nodes"></a>Stap 1: Maak een cloudservice en een opslagaccount voor hello Azure knooppunten
Hallo klassieke Azure-portal of vergelijkbare's tooconfigure Hallo resources die nodig toodeploy na uw Azure knooppunten gebruiken:

* Een nieuwe Azure-cloud-service
* Een nieuwe Azure storage-account

> [!NOTE]
> Niet opnieuw gebruiken van een bestaande cloudservice in uw abonnement. 
> 
> 

**Overwegingen**

* Een afzonderlijke cloudservice voor elke Azure knooppuntsjabloon dat u van plan toocreate bent configureren. U kunt echter hetzelfde opslagaccount voor meerdere knooppunt sjablonen Hallo.
* Het is raadzaam dat u Hallo-cloudservice en storage-account voor de implementatie van Hallo Hallo in Hallo vinden dezelfde Azure-regio.

## <a name="step-2-configure-an-azure-management-certificate"></a>Stap 2: Een Azure-beheercertificaat configureren
tooadd Azure knooppunten zoals bronnen berekenen, moet u een beheercertificaat op Hallo hoofdknooppunt en uploaden een overeenkomende toohello Azure-abonnement gebruikt voor Hallo implementatie van het certificaat.

Voor dit scenario kunt u Hallo **standaard HPC Azure-Beheercertificaat** die HPC Pack automatisch geïnstalleerd en geconfigureerd op het hoofdknooppunt. Dit certificaat is handig voor het testen van de toepassing en bewijs van concept implementaties. toouse van dit certificaat, upload het bestand C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer van hoofdknooppunt Hallo VM toothe abonnement. tooupload hello certificaat in Hallo [klassieke Azure-portal](https://manage.windowsazure.com), klikt u op **instellingen** > **Beheercertificaten**.

Zie voor extra opties tooconfigure hello beheercertificaat [scenario's tooConfigure hello Azure-Beheercertificaat voor Azure Burst implementaties](http://technet.microsoft.com/library/gg481759.aspx).

## <a name="step-3-deploy-azure-nodes-toohello-cluster"></a>Stap 3: Azure knooppunten toohello cluster implementeren
Hallo stappen tooadd en start Azure knooppunten in dit scenario zijn dezelfde doorgaans Hallo als Hallo stappen met het hoofdknooppunt van een lokale. Zie voor meer informatie, Hallo uit te voeren in [tooDeploy Azure knooppunten met Microsoft HPC Pack stappen](https://technet.microsoft.com/library/gg481758.aspx):

* Een op Azure-knooppuntsjabloon maken
* Azure knooppunten toohello Windows HPC-cluster toevoegen
* Start (ingericht) hello Azure knooppunten

Nadat u toevoegen en knooppunten Hallo starten, zijn ze klaar voor je toouse toorun cluster taken.

Als u problemen ondervindt bij het implementeren van Azure knooppunten, Zie [oplossen implementaties van Azure knooppunten met Microsoft HPC Pack](http://technet.microsoft.com/library/jj159097.aspx).

## <a name="next-steps"></a>Volgende stappen
* een van rekenintensieve exemplaargrootte voor Hallo toouse burst knooppunten, Zie Hallo overwegingen in [hoge prestaties compute-VM-grootten](../sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
* Als u wilt automatisch vergroten of verkleinen Hallo computerbronnen volgens clusterbelasting hello Azure, Zie [automatisch vergroten of verkleinen van Azure-rekenresources in een cluster HPC Pack](hpcpack-cluster-node-autogrowshrink.md).

<!--Image references-->
[burst]: ./media/hpcpack-cluster-node-burst/burst.png

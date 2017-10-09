---
title: aaaMATLAB clusters op virtuele machines | Microsoft Docs
description: Gebruik Microsoft Azure virtuele machines toocreate MATLAB gedistribueerde Computing Server clusters toorun uw rekenintensieve parallelle MATLAB workloads
services: virtual-machines-windows
documentationcenter: 
author: mscurrell
manager: timlt
editor: 
ms.assetid: e9980ce9-124a-41f1-b9ec-f444c8ea5c72
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Windows
ms.workload: infrastructure-services
ms.date: 05/09/2016
ms.author: markscu
ms.openlocfilehash: 266749dbdcfefac42c94b74aa612bfee18075a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-matlab-distributed-computing-server-clusters-on-azure-vms"></a>Server voor MATLAB gedistribueerde Computing clusters maken op Azure Virtual machines
Gebruik Microsoft Azure virtual machines toocreate een of meer MATLAB gedistribueerde Computing serverclusters toorun uw rekenintensieve parallelle MATLAB werkbelastingen. Uw Server voor MATLAB gedistribueerde Computing-software installeren op een VM-toouse als een basisinstallatiekopie en een sjabloon voor de Azure quickstart of Azure PowerShell-script (beschikbaar op [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster)) toodeploy Hallo-cluster en dit beheren. Verbinding toohello cluster toorun uw werkbelastingen na de implementatie.

## <a name="about-matlab-and-matlab-distributed-computing-server"></a>Over MATLAB en MATLAB gedistribueerde Computing Server
Hallo [MATLAB](http://www.mathworks.com/products/matlab/) platform is geoptimaliseerd voor het oplossen van problemen met de technische en wetenschappelijke. MATLAB gebruikers met grootschalige simulaties en gegevensverwerkingstaken kunnen MathWorks parallel producten toospeed van hun rekenintensieve workloads computing door gebruik te maken van de rekenclusters en raster services gebruiken. [Parallelle berekeningen werkset](http://www.mathworks.com/products/parallel-computing/) kunnen gebruikers MATLAB parallelize toepassingen en te profiteren van multicore-processors, GPU's, en rekenclusters. [Server voor MATLAB gedistribueerde Computing](http://www.mathworks.com/products/distriben/) MATLAB gebruikers tooutilize kunnen veel computers in een rekencluster.

Met behulp van virtuele machines in Azure, kunt u Server voor MATLAB gedistribueerde Computing-clusters die alle Hallo dezelfde mechanismen beschikbaar toosubmit parallel werk als lokale clusters, zoals interactieve jobs, taken, onafhankelijke taken en communicatie van taken. Met behulp van Azure in combinatie met Hallo MATLAB platform heeft veel voordelen ten opzichte tooprovisioning en met behulp van traditionele on-premises hardware: een bereik van de VM-groottes, het maken van clusters op aanvraag zodat u alleen voor Hallo-rekenresources die u gebruikt betaalt, en Hallo mogelijkheid tootest modellen op schaal.  

## <a name="prerequisites"></a>Vereisten
* **Clientcomputer** -moet u een client voor Windows-computer toocommunicate met Azure en Hallo MATLAB gedistribueerde Computing Server-cluster na de implementatie.
* **Azure PowerShell** -Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) tooinstall op de clientcomputer.
* **Azure-abonnement** -als u geen een abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten. Voor grotere clusters kunt u een abonnement op gebruiksbasis of andere Aankoopopties.
* **Quotum voor kernen** -moet u mogelijk tooincrease Hallo core quotum toodeploy een grote cluster of meer dan één Server voor MATLAB gedistribueerde Computing-cluster. een quotum tooincrease [opent u een ondersteuningsaanvraag online klant](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) zonder kosten.
* **MATLAB, parallelle berekeningen werkset en MATLAB gedistribueerde Computing Server licenties** -Hallo scripts wordt ervan uitgegaan dat Hallo [MathWorks gehost Licentiebeheer](http://www.mathworks.com/products/parallel-computing/mathworks-hosted-license-manager/) wordt gebruikt voor alle licenties.  
* **Server voor MATLAB gedistribueerde Computing software** -wordt geïnstalleerd op een virtuele machine die wordt gebruikt als basisinstallatiekopie VM voor Hallo voor Hallo cluster virtuele machines.

## <a name="high-level-steps"></a>Hoog niveau stappen
toouse Azure virtuele machines voor uw MATLAB gedistribueerde Computing serverclusters hello volgende geavanceerde stappen zijn vereist. Gedetailleerde instructies vindt u in de documentatie van Hallo Hallo Quick Start-sjabloon en scripts die op [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster).

1. **Basis VM-installatiekopie maken**  

   * Download en installeer de Server voor MATLAB gedistribueerde Computing software op deze virtuele machine.

     > [!NOTE]
     > Dit proces kan enkele uren duren, maar u hebt alleen toodo deze zodra u voor elke versie van MATLAB gebruiken.   
     >
     >
2. **Een of meer clusters maken**  

   * Hallo opgegeven PowerShell-script gebruikt of Hallo Quick Start sjabloon toocreate een cluster met Hallo basisinstallatiekopie VM.   
   * Hallo-clusters met Hallo opgegeven PowerShell-script waarmee u toolist, onderbreken, hervatten en delete-clusters kunt beheren.

## <a name="cluster-configurations"></a>Configuraties van clusters
Op dit moment kunnen Hallo-script voor het maken van cluster en de sjabloon u een topologie met één Server voor MATLAB gedistribueerde Computing toocreate. Als u wilt maken van een of meer extra clusters, met elk cluster met een verschillend aantal worker virtuele machines, met behulp van andere VM-grootten, enzovoort.

### <a name="matlab-client-and-cluster-in-azure"></a>MATLAB client en de cluster in Azure
Hallo MATLAB client-knooppunt, MATLAB Taakplanner-knooppunt en MATLAB Computing Server voor gedistribueerde 'worker' knooppunten zijn alle geconfigureerd als Azure virtuele machines in een virtueel netwerk, zoals wordt weergegeven in de volgende Hallo afbeelding.


* Hallo toouse cluster, verbinding maken met extern bureaublad toohello client-knooppunt. Hallo clientknooppunt uitvoert Hallo MATLAB client.
* Hallo clientknooppunt heeft een bestandsshare die toegankelijk zijn voor alle werknemers.
* MathWorks gehost Licentiebeheer wordt gebruikt voor Hallo licentie controles voor alle MATLAB software.
* Standaard één Server voor MATLAB gedistribueerde Computing werknemer per core op Hallo worker virtuele machines is gemaakt, maar u kunt een willekeurig getal opgeven.

## <a name="use-an-azure-based-cluster"></a>Gebruik een Cluster op basis van Azure
Net als bij andere soorten MATLAB gedistribueerde Computing serverclusters, moet u toouse Hallo profiel Clusterbeheer in Hallo MATLAB client (op Hallo van client VM) toocreate een profiel van de cluster MATLAB Taakplanner.

![Profiel Clusterbeheer](./media/matlab-mdcs-cluster/cluster_profile_manager.png)

## <a name="next-steps"></a>Volgende stappen
* Voor gedetailleerde instructies toodeploy en MATLAB gedistribueerde Computing serverclusters beheren in Azure, Zie Hallo [GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/matlab-cluster) -opslagplaats met Hallo sjablonen en scripts.
* Ga toohello [MathWorks site](http://www.mathworks.com/) voor gedetailleerde documentatie voor MATLAB en MATLAB gedistribueerde Computing-Server.

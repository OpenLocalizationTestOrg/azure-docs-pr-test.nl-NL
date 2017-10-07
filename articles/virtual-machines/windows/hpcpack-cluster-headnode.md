---
title: een HPC Pack hoofdknooppunt in een Azure VM aaaCreate | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure portal en Hallo Resource Manager deployment model toocreate een Microsoft HPC Pack 2012 R2-hoofdknooppunt in een Azure VM.
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Hoofdknooppunt van een cluster HPC Pack Hallo in een Azure-VM met een Marketplace-installatiekopie maken
Gebruik een [installatiekopie van de virtuele machine Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) hello Azure Marketplace en hello Azure portal toocreate Hallo head knooppunt van een HPC-cluster. Deze HPC Pack VM-installatiekopie is gebaseerd op Windows Server 2012 R2 Datacenter met HPC Pack 2012 R2 Update 3 vooraf zijn geïnstalleerd. Gebruik deze hoofdknooppunt voor een bewijs van de implementatie van het concept van HPC Pack in Azure. U kunt vervolgens compute knooppunten toohello cluster toorun HPC-workloads toevoegen.

> [!TIP]
> een volledige HPC Pack 2012 R2-cluster in Azure met hoofdknooppunt Hallo en rekenknooppunten toodeploy, wordt aangeraden dat u een automatische methode. Opties zijn onder andere Hallo [HPC Pack IaaS-implementatiescript](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) en Resource Manager-sjablonen zoals Hallo [cluster HPC Pack voor Windows werkbelasting](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Resource Manager-sjablonen zijn ook beschikbaar voor [Microsoft HPC Pack 2016 clusters](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Aandachtspunten voor de planning
Zoals u in de volgende afbeelding Hallo, implementeert u Hallo HPC Pack hoofdknooppunt in Active Directory-domein in een Azure-netwerk.

![Hoofdknooppunt HPC Pack][headnode]

* **Active Directory-domein**: hello HPC Pack 2012 R2 hoofdknooppunt moet worden samengevoegd tooan Active Directory-domein in Azure voordat u Hallo HPC-services op Hallo VM starten. Zoals in dit artikel voor een bewijs van concept implementatie, kunt u Hallo VM die u maakt voordat Hallo HPC-services starten als een domeincontroller voor het hoofdknooppunt Hallo promoveren. Een andere optie is een afzonderlijke domeincontroller toodeploy en -forest in Azure toowhich u deelnemen aan Hallo hoofdknooppunt VM.

* **Implementatiemodel**: voor de meeste nieuwe implementaties, wordt aangeraden dat u Hallo Resource Manager-implementatiemodel. In dit artikel wordt ervan uitgegaan dat u dit implementatiemodel.

* **Virtuele Azure-netwerk**: wanneer u Hallo Resource Manager deployment model toodeploy Hallo hoofdknooppunt gebruikt, u opgeven of maken van een virtuele Azure-netwerk. U Hallo virtueel netwerk gebruiken als u toojoin Hallo hoofdknooppunt tooan bestaande Active Directory-domein nodig. U moet ook het rekenknooppunt hoger tooadd VMs toohello cluster.

## <a name="steps-toocreate-hello-head-node"></a>Stappen toocreate Hallo hoofdknooppunt
Hieronder vindt u stappen op hoog niveau toouse hello toocreate met Azure portal een Azure-VM voor HPC Pack Hallo-hoofdknooppunt met Hallo Resource Manager-implementatiemodel. 

1. Als u een nieuw Active Directory-forest in Azure met afzonderlijke domeincontroller VMs toocreate wilt, één optie toouse is een [Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Voor een eenvoudige bewijs van concept-implementatie heeft fijn tooomit deze stap en Hallo hoofdknooppunt VM zelf configureren als een domeincontroller. Deze optie wordt verderop in dit artikel beschreven.
2. Op Hallo [HPC Pack 2012 R2 op de pagina Windows Server 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) in hello Azure Marketplace, klikt u op **virtuele Machine maken**. 
3. In de portal Hallo op Hallo **HPC Pack 2012 R2 op Windows Server 2012 R2** pagina, selecteer Hallo **Resource Manager** implementatiemodel en klik vervolgens op **maken**.
   
    ![HPC Pack installatiekopie][marketplace]
4. Hallo portal tooconfigure Hallo instellingen gebruiken en Hallo VM maken. Als u nieuwe tooAzure, volg Hallo zelfstudie [virtuele Windows-machine maken in Azure-portal Hallo](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Voor een bewijs van concept implementatie kan meestal Hallo standaardwaarde accepteren of aanbevolen instellingen.
   
   > [!NOTE]
   > Als u toojoin Hallo hoofdknooppunt tooan bestaande Active Directory-domein in Azure wilt, zorg er dan voor dat u Hallo virtueel netwerk voor dat domein opgeeft bij het maken van Hallo VM.
   > 
   > 
5. Na het maken van VM Hallo Hallo VM wordt uitgevoerd, [toohello VM verbinding](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) door extern bureaublad. 
6. Aanmelden bij Hallo VM tooan Active Directory-domein-forest door een Hallo volgende opties te kiezen:
   
   * Als u Hallo VM in een Azure-netwerk met een bestaand domeinforest gemaakt, met elkaar verbinden Hallo VM toohello forest met standaardprogramma's voor Serverbeheer of Windows PowerShell. Start vervolgens opnieuw.
   * Als u Hallo VM gemaakt in een nieuw virtueel netwerk (zonder een bestaand domein-forest), moet u vervolgens Hallo VM als een domeincontroller promoveren. Gebruik standaard stappen tooinstall en Hallo Active Directory Domain Services-functie configureren op Hallo hoofdknooppunt. Zie voor gedetailleerde stappen [een nieuw Windows Server 2012 Active Directory-Forest installeren](https://technet.microsoft.com/library/jj574166.aspx).
7. Start na Hallo VM wordt uitgevoerd en gekoppelde tooan Active Directory-forest, Hallo HPC Pack services als volgt:
   
    a. Verbinding maken met hoofdknooppunt toohello VM die gebruikmaakt van een domeinaccount dat lid is van de lokale beheerdersgroep Hallo. Bijvoorbeeld, Hallo administratoraccount gebruikt die u instellen wanneer u Hallo hoofdknooppunt VM gemaakt.
   
    b. Voor een hoofdknooppunt standaardconfiguratie start Windows PowerShell als beheerder en typ de volgende Hallo:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Het kan enkele minuten duren voordat Hallo HPC Pack services toostart.
   
    Voor extra hoofdknooppunt configuratieopties, typt u `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Volgende stappen
* Nu kunt u werken met het hoofdknooppunt van het cluster HPC Pack Hallo. Bijvoorbeeld, start HPC Cluster Manager en volledige Hallo [implementatie takenlijst](https://technet.microsoft.com/library/jj884141.aspx).
* Als u wilt dat tooincrease Hallo cluster compute-capaciteit op aanvraag, voegt u [Azure burst knooppunten](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) in een cloudservice. 
* Probeer een werkbelasting test uitgevoerd op Hallo-cluster. Zie voor een voorbeeld Hallo HPC Pack [instructiehandleiding](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png

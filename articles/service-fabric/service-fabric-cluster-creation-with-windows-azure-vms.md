---
title: aaaCreate zelfstandige cluster met virtuele Azure-machines met Windows | Microsoft Docs
description: Meer informatie over hoe toocreate en beheren van een Azure Service Fabric-cluster op virtuele machines in Azure waarop Windows Server wordt uitgevoerd.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 7eeb40d2-fb22-4a77-80ca-f1b46b22edbc
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: ryanwi;chackdan
redirect_url: /azure/service-fabric/service-fabric-cluster-creation-via-arm
ms.openlocfilehash: 8900204fe69887a7a0ca54b06e0d32534421bcfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-three-node-standalone-service-fabric-cluster-with-azure-virtual-machines-running-windows-server"></a>Drie knooppunten zelfstandige Service Fabric-cluster maken met virtuele machines in Azure waarop Windows Server wordt uitgevoerd
Dit artikel wordt beschreven hoe toocreate een cluster op Windows gebaseerde virtuele Azure-machines (VM's) met behulp van Hallo van zelfstandige Service Fabric-installatieprogramma voor Windows Server. Hallo-scenario is een speciaal geval van [maken en beheren van een cluster met Windows Server](service-fabric-cluster-creation-for-windows-server.md) waar Hallo VM's zijn [Azure VM's met Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), maar u geen maakt [een Azure cloud-gebaseerde Service Fabric-cluster](service-fabric-cluster-creation-via-portal.md). Hallo verschil in de volgende dit patroon is dat Hallo zelfstandige Service Fabric-cluster gemaakt door de volgende stappen uit Hallo volledig wordt beheerd door u, terwijl hello Azure cloud-gebaseerde Service Fabric-clusters worden beheerd en bijgewerkt door Hallo Service Fabric resourceprovider.

## <a name="steps-toocreate-hello-standalone-cluster"></a>Stappen toocreate Hallo zelfstandige cluster
1. Meld u aan toohello Azure-portal en een nieuwe Windows Server 2012 R2 Datacenter of Windows Server 2016 Datacenter VM in een resourcegroep maken. Hallo-artikel lezen [maken van een virtuele machine van Windows in hello Azure-portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor meer informatie.
2. Toevoegen van een aantal meer virtuele machines toohello dezelfde resourcegroep. Zorg ervoor dat elk Hallo VMs heeft Hallo dezelfde beheerdersgebruikersnaam en hetzelfde wachtwoord tijdens het maken. Nadat deze is gemaakt ziet u alle drie virtuele machines in Hallo hetzelfde virtuele netwerk.
3. Verbinding maken tooeach Hallo VM's en Hallo uitschakelen met Windows Firewall met Hallo [Server Manager dashboard van de lokale Server](https://technet.microsoft.com/library/jj134147.aspx). Dit zorgt ervoor dat het Hallo-netwerkverkeer tussen Hallo-machines communiceren kan. Ophalen tijdens verbonden tooeach machine Hallo IP-adres door een opdrachtprompt openen en te typen `ipconfig`. U kunt ook ziet u Hallo IP-adres van elke computer op Hallo-portal door te selecteren Hallo virtueel netwerk resource voor de resourcegroep Hallo en Hallo netwerkinterfaces gemaakt voor elk van deze machines te controleren.
4. Verbind tooone Hallo VM's en test die u kunt pingen Hallo andere twee virtuele machines is.
5. Tooone Hallo virtuele machines verbinding en [downloaden Hallo zelfstandige Service Fabric-pakket voor Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) naar een nieuwe map op Hallo van de computer en pak Hallo-pakket.
6. Open Hallo *ClusterConfig.Unsecure.MultiMachine.json* -bestand in Kladblok en bewerken van elk knooppunt met Hallo drie IP-adressen van Hallo-machines. De clusternaam Hallo Hallo boven wijzigen en sla Hallo-bestand.  Een voorbeeld van een gedeeltelijke van het clustermanifest Hallo worden hieronder weergegeven.
   
    ```
    {
        "name": "SampleCluster",
        "clusterConfigurationVersion": "1.0.0",
        "apiVersion": "01-2017",
        "nodes": [
        {
            "nodeName": "standalonenode0",
            "iPAddress": "10.1.0.4",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD0"
        },
        {
            "nodeName": "standalonenode1",
            "iPAddress": "10.1.0.5",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc2/r0",
            "upgradeDomain": "UD1"
        },
        {
            "nodeName": "standalonenode2",
            "iPAddress": "10.1.0.6",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc3/r0",
            "upgradeDomain": "UD2"
        }
        ],
    ```
7. Als u van plan deze toobe een beveiligde cluster bent, moet u bepalen Hallo beveiligingsmaatregel u wilt toouse en volg de stappen Hallo op Hallo koppeling die is gekoppeld: [X509-certificaat](service-fabric-windows-cluster-x509-security.md) of [Windows-beveiliging](service-fabric-windows-cluster-windows-security.md). Als het Hallo-cluster met behulp van Windows-beveiliging instelt, moet u tooset van een domeincontroller toomanage Active Directory. Houd er rekening mee dat met een computer op een domeincontroller in een domein als een Service Fabric knooppunt wordt niet ondersteund.
8. Open een [PowerShell ISE-venster](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise). Navigeer toohello map waarin u Hallo gedownloade zelfstandige installer-pakket hebt uitgepakt en Hallo cluster configuratiebestand opgeslagen. Voer Hallo PowerShell-opdracht toodeploy Hallo cluster te volgen:
   
    ```
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.MultiMachine.json
    ```

Hallo script Hallo Service Fabric-cluster op afstand configureert en voortgang moet worden gerapporteerd als wordt via de implementatie.

9. Na ongeveer een minuut, u controleren kunt of Hallo cluster operationele is door verbinding te maken toohello Service Fabric Explorer met behulp van een van de machine Hallo IP-adressen, bijvoorbeeld met behulp van `http://10.1.0.5:19080/Explorer/index.html`. 

## <a name="next-steps"></a>Volgende stappen
* [Create standalone Service Fabric clusters on Windows Server or Linux (Zelfstandige Service Fabric-clusters maken in Windows Server of Linux)](service-fabric-deploy-anywhere.md)
* [Toevoegen of verwijderen van knooppunten tooa zelfstandige Service Fabric-cluster](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [Configuratie-instellingen voor zelfstandige Windows-cluster](service-fabric-cluster-manifest.md)
* [Beveiligen van een zelfstandige cluster op Windows met behulp van Windows-beveiliging](service-fabric-windows-cluster-windows-security.md)
* [Beveiligen van een zelfstandige cluster op Windows met behulp van X509 certificaten](service-fabric-windows-cluster-x509-security.md)


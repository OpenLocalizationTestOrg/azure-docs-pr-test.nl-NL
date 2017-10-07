---
title: aaaConnect tooa virtuele Machine van SQL Server op Azure (klassiek) | Microsoft Docs
description: Meer informatie over hoe tooconnect tooSQL Server uitgevoerd op een virtuele Machine in Azure. In dit onderwerp maakt gebruik van het klassieke implementatiemodel Hallo. Hallo scenario's verschillen afhankelijk van de netwerkconfiguratie Hallo en Hallo-locatie van Hallo-client.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: 416948af-454f-4cfe-8fd2-7cf971cbd3e9
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: jroth
experimental_id: d51f3cc6-753b-4e
ms.openlocfilehash: 4fff3936ad0bcfd3a56855a8436991e19b92522b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-classic-deployment"></a>Verbinding maken met tooa virtuele Machine van SQL Server op Azure (klassieke implementatie)
> [!div class="op_single_selector"]
> * [Resource Manager](../sql/virtual-machines-windows-sql-connect.md)
> * [Klassiek](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Overzicht
Dit onderwerp wordt beschreven hoe tooconnect tooyour SQL Server-instantie uitgevoerd op een virtuele machine van Azure. Dit omvat een aantal [algemene verbindingsproblemen scenario's](#connection-scenarios) en geeft vervolgens [gedetailleerde stappen voor het configureren van SQL-serververbindingen in een Azure VM](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Als u virtuele machines van Resource Manager gebruikt, raadpleegt u [verbinding maken met virtuele Machine van SQL Server op Azure Resource Manager met tooa](../sql/virtual-machines-windows-sql-connect.md).

## <a name="connection-scenarios"></a>Scenario 's
Hallo manier een client verbinding maakt tooSQL-Server op een virtuele Machine, is afhankelijk van Hallo locatie van het Hallo-client en Hallo machine/netwerkconfiguratie. Deze scenario's omvatten:

* [Verbinding maken met Server tooSQL Hallo moeten dezelfde cloudservice](#connect-to-sql-server-in-the-same-cloud-service)
* [TooSQL Server via Hallo verbinding maken met internet](#connect-to-sql-server-over-the-internet)
* [Verbinding maken met Server tooSQL in Hallo hetzelfde virtuele netwerk](#connect-to-sql-server-in-the-same-virtual-network)

> [!NOTE]
> Voordat u verbinding met een van deze methoden maakt, moet u Hallo volgen [stappen in dit artikel tooconfigure connectiviteit](#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).
> 
> 

### <a name="connect-toosql-server-in-hello-same-cloud-service"></a>Verbinding maken met Server tooSQL Hallo moeten dezelfde cloudservice
Meerdere virtuele machines kunnen worden gemaakt in Hallo dezelfde cloudservice. toounderstand deze virtuele machines scenario, Zie [hoe tooconnect virtuele machines met een virtueel netwerk of cloud service](../classic/connect-vms.md#connect-vms-in-a-standalone-cloud-service). Dit scenario is wanneer een client op een virtuele machine tooconnect tooSQL Server wordt uitgevoerd probeert op een andere virtuele machine in Hallo dezelfde cloudservice.

In dit scenario kunt u verbinding maken met behulp van Hallo VM **naam** (ook weergegeven als **computernaam** of **hostnaam** in Hallo-portal). Dit is Hallo-naam die u hebt opgegeven voor Hallo VM tijdens het maken van. Bijvoorbeeld, als u met de naam van de VM SQL **mysqlvm**, Hallo dezelfde cloudservice kan gebruiken een client VM Hallo connection string tooconnect te volgen:

    "Server=mysqlvm;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

### <a name="connect-toosql-server-over-hello-internet"></a>Verbinding maken met tooSQL Server via Internet Hallo
Als u tooconnect tooyour SQL Server database-engine van Hallo Internet wilt, moet u een virtuele machine-eindpunt voor binnenkomende TCP-communicatie. Deze stap configuratie van Azure zorgt ervoor dat de binnenkomende TCP-poort verkeer tooa TCP-poort die is toegankelijk toohello virtuele machine.

tooconnect via Hallo internet, moet u Hallo van de virtuele machine DNS-naam en het Hallo VM eindpunt poortnummer (geconfigureerd verderop in dit artikel). toofind hello DNS-naam, navigeer toohello Azure portal en selecteer **virtuele machines (klassiek)**. Selecteer vervolgens de virtuele machine. Hallo **DNS-naam** wordt weergegeven in Hallo **overzicht** sectie.

Neem bijvoorbeeld een klassieke virtuele machine met de naam **mysqlvm** met een DNS-naam van **mysqlvm7777.cloudapp.net** en een VM-eindpunt van **57500**. Ervan uitgaande dat verbinding juist is geconfigureerd, kan Hallo verbindingsreeks na gebruikte tooaccess Hallo virtuele machine vanaf elke locatie op worden Hallo internet:

    "Server=mycloudservice.cloudapp.net,57500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"

Hoewel dit wordt de connectiviteit mogelijk voor clients via internet Hallo, betekent dit niet dat iedereen tooyour SQL Server verbinding kan maken. Externe clients hebben toohello juiste gebruikersnaam en wachtwoord. Voor extra beveiliging, gebruik geen Hallo bekende poort 1433 voor het eindpunt van de openbare virtuele machine Hallo. En, indien mogelijk, overweegt u het toevoegen van een ACL op uw eindpunt toorestrict verkeer alleen toohello clients die u toestaan. Zie voor instructies over het gebruik van ACL's met eindpunten [beheren Hallo ACL op een eindpunt](../classic/setup-endpoints.md#manage-the-acl-on-an-endpoint).

> [!NOTE]
> Het is belangrijk wanneer u deze techniek toocommunicate met SQL Server gebruikt, Hallo alle uitgaande gegevens van Azure-datacenter toonote onderwerp toonormal [prijzen voor uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/).
> 
> 

### <a name="connect-toosql-server-in-hello-same-virtual-network"></a>Verbinding maken met Server tooSQL in Hallo hetzelfde virtuele netwerk
[Virtueel netwerk](../../../virtual-network/virtual-networks-overview.md) kunnen aanvullende scenario's. U kunt virtuele machines in hetzelfde virtuele netwerk, zelfs als deze virtuele machines bestaan in verschillende cloudservices Hallo verbinden. En met een [site-naar-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), kunt u een hybride-architectuur die virtuele machines met on-premises netwerken en machines verbindt.

Virtuele netwerken kunt u toojoin ook uw virtuele Azure-machines tooa-domein. Dit is Hallo alleen manier toouse Windows-verificatie tooSQL Server. Hallo vereisen andere scenario's SQL-verificatie met gebruikersnamen en wachtwoorden.

Als u tooconfigure een domeinomgeving en Windows-verificatie gaat, hoeft u geen toouse Hallo stappen in dit artikel tooconfigure Hallo openbaar eindpunt of Hallo SQL-verificatie en aanmeldingen. In dit scenario tooyour SQL Server-exemplaar verbinding kunt maken met de Hallo SQL Server VM-naam te geven in Hallo-verbindingsreeks. Hallo volgende voorbeeld wordt ervan uitgegaan dat Windows-verificatie ook is geconfigureerd en die gebruiker Hallo toohello SQL Server-exemplaar toegang heeft gekregen.

    "Server=mysqlvm;Integrated Security=true"

## <a name="steps-for-configuring-sql-server-connectivity-in-an-azure-vm"></a>Stappen voor het configureren van SQL-serververbindingen in een Azure VM
Hallo stappen laten zien hoe tooconnect toohello SQL Server-exemplaar via internet met behulp van SQL Server Management Studio (SSMS) Hallo. Echter, hello dezelfde stappen toepassen toomaking uw virtuele machine voor SQL Server toegankelijk is voor uw toepassingen, zowel on-premises uitgevoerd en in Azure.

Voordat u kunt verbinding maken met toohello exemplaar van SQL Server uit een andere virtuele machine of Hallo internet, moet u taken te volgen, zoals beschreven in de secties Hallo Hallo uitvoeren:

* [Een TCP-eindpunt voor Hallo virtuele machine maken](#create-a-tcp-endpoint-for-the-virtual-machine)
* [TCP-poorten openen in Hallo Windows firewall](#open-tcp-ports-in-the-windows-firewall-for-the-default-instance-of-the-database-engine)
* [Configureren van SQL Server-toolisten op Hallo TCP-protocol](#configure-sql-server-to-listen-on-the-tcp-protocol)
* [SQL Server configureren voor verificatie in gemengde modus](#configure-sql-server-for-mixed-mode-authentication)
* [SQL Server-verificatie-aanmeldingen maken](#create-sql-server-authentication-logins)
* [Hallo DNS-naam van de virtuele machine van Hallo bepalen](#determine-the-dns-name-of-the-virtual-machine)
* [Verbinding maken met Database-Engine toohello vanaf een andere computer](#connect-to-the-database-engine-from-another-computer)

Hallo verbindingspad wordt door Hallo volgende diagram samengevat:

![Verbinding maken met tooa SQL Server-virtuele machine](../../../../includes/media/virtual-machines-sql-server-connection-steps/SQLServerinVMConnectionMap.png)

[!INCLUDE [Connect tooSQL Server in a VM Classic TCP Endpoint](../../../../includes/virtual-machines-sql-server-connection-steps-classic-tcp-endpoint.md)]

[!INCLUDE [Connect tooSQL Server in a VM](../../../../includes/virtual-machines-sql-server-connection-steps.md)]

[!INCLUDE [Connect tooSQL Server in a VM Classic Steps](../../../../includes/virtual-machines-sql-server-connection-steps-classic.md)]

## <a name="next-steps"></a>Volgende stappen
Als u ook toouse AlwaysOn Availability Groups voor hoge beschikbaarheid en herstel na noodgevallen plant, kunt u overwegen een listener te implementeren. Database-clients verbinding maken toohello listener in plaats van rechtstreeks tooone van Hallo SQL Server-exemplaren. Hallo-listener routes clients toohello primaire replica in de beschikbaarheidsgroep Hallo. Zie voor meer informatie [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).

Het is belangrijk tooreview alle Hallo beveiliging aanbevolen procedures voor SQL Server op Azure een virtuele machine wordt uitgevoerd. Zie [Veiligheidsoverwegingen voor SQL Server in virtuele Azure-machines](../sql/virtual-machines-windows-sql-security.md) voor meer informatie.

[Hallo Leertraject verkennen](https://azure.microsoft.com/documentation/learning-paths/sql-azure-vm/) voor SQL Server op Azure virtuele machines. 

Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).


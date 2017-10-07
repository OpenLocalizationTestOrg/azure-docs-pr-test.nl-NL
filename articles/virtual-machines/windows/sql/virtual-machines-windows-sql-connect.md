---
title: aaaConnect tooa SQL Server-VM (Resource Manager) | Microsoft Docs
description: Meer informatie over hoe tooconnect tooSQL Server uitgevoerd op een virtuele Machine in Azure. In dit onderwerp maakt gebruik van het klassieke implementatiemodel Hallo. Hallo scenario's verschillen afhankelijk van de netwerkconfiguratie Hallo en Hallo-locatie van Hallo-client.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/14/2017
ms.author: jroth
ms.openlocfilehash: 7b127c14c37b9a72c19ed17f8b1dad61c7bc2d38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a>Verbinding maken met tooa virtuele Machine van SQL Server op Azure (Resource Manager)
> [!div class="op_single_selector"]
> * [Resource Manager](virtual-machines-windows-sql-connect.md)
> * [Klassiek](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a>Overzicht

Dit onderwerp wordt beschreven hoe tooconnect tooyour SQL Server-instantie uitgevoerd op een virtuele machine van Azure. Dit omvat een aantal [algemene verbindingsproblemen scenario's](#connection-scenarios) en geeft vervolgens [gedetailleerde stappen voor het configureren van SQL-serververbindingen in een Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

Als u liever een volledig overzicht van beide, inrichten en connectiviteit, Zie [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="connection-scenarios"></a>Scenario 's

Hallo manier een client verbinding maakt tooSQL-Server op een virtuele Machine, is afhankelijk van Hallo-locatie van het Hallo-client en de netwerkconfiguratie Hallo.

Als u een SQL Server VM in hello Azure-portal inricht, hebt u de optie Hallo van het type Hallo opgeven **SQL-connectiviteit**.

![Openbare SQL verbindingsoptie tijdens het inrichten](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

Uw opties voor connectiviteit zijn onder andere:

| Optie | Beschrijving |
|---|---|
| **Openbare** | TooSQL Server via Hallo verbinding maken met internet |
| **Persoonlijke** | Verbinding maken met Server tooSQL in Hallo hetzelfde virtuele netwerk |
| **Lokale** | Verbinding maken met tooSQL Server lokaal op Hallo dezelfde virtuele machine | 

Hallo volgende secties wordt uitgelegd Hallo **openbare** en **persoonlijke** opties in meer detail.

## <a name="connect-toosql-server-over-hello-internet"></a>Verbinding maken met tooSQL Server via Internet Hallo

Als u wilt dat tooconnect tooyour SQL Server database-engine van Hallo Internet, selecteert u **openbare** voor Hallo **SQL-connectiviteit** type in de portal Hallo tijdens het inrichten. Hallo-portal automatisch Hallo volgende stappen:

* Hallo TCP/IP-protocol ingeschakeld voor SQL Server.
* Hiermee configureert u een firewall regel tooopen Hallo SQL Server-TCP-poort (standaard 1433).
* Hiermee kunt SQL Server-verificatie vereist is voor openbare toegang.
* Netwerkbeveiligingsgroep hello configureert op Hallo VM tooall TCP-verkeer op Hallo van SQL Server-poort.

> [!IMPORTANT]
> installatiekopieën van virtuele machines Hallo voor SQL Server Developer Hallo en Express-edities niet automatisch ingeschakeld Hallo TCP/IP-protocol. Voor ontwikkelaars en Express-edities, moet u SQL Server Configuration Manager te gebruiken[handmatig inschakelen Hallo TCP/IP-protocol](#manualtcp) Hallo na het maken van VM.

Een client met toegang tot internet verbinding kunt maken voor toohello SQL Server-exemplaar met geven Hallo openbaar IP-adres van Hallo virtuele machine of een DNS-label toothat IP-adres toegewezen. Als Hallo SQL Server-poort 1433, hoeft u niet toospecify in Hallo-verbindingsreeks. Hallo verbindingsreeks na tooa SQL VM is verbonden met een DNS-label van `sqlvmlabel.eastus.cloudapp.azure.com` via SQL-verificatie (u kunt ook Hallo openbaar IP-adres).

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

Hoewel dit wordt de connectiviteit mogelijk voor clients via internet Hallo, betekent dit niet dat iedereen tooyour SQL Server verbinding kan maken. Externe clients hebben toohello juiste gebruikersnaam en wachtwoord. Voor extra beveiliging kunt u echter een bekende Hallo-poort 1433 voorkomen. Bijvoorbeeld, als u SQL Server-toolisten op poort 1500 en tot stand gebrachte correcte firewall en netwerkbeveiligingsgroepen hebt geconfigureerd, kan u door Hallo poort nummer toohello-servernaam toe te voegen. Hallo volgende voorbeeld wijzigt Hallo vorige door een aangepast poortnummer toe te voegen **1500**, toohello servernaam:

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> Als u SQL Server op een virtuele machine query's via internet, alle uitgaande gegevens Hallo van hello Azure datacenter onderwerp toonormal is [prijzen voor uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/).

## <a name="connect-toosql-server-within-a-virtual-network"></a>Verbinding maken met Server tooSQL binnen een virtueel netwerk

Wanneer u de optie **persoonlijke** voor Hallo **SQL-connectiviteit** type in Azure-portal Hallo configureert u de meeste Hallo dezelfde instellingen te**openbare**. Hallo een verschil is dat er geen netwerk beveiliging groep regel tooallow buiten-verkeer op Hallo SQL Server-poort (standaard 1433).

> [!IMPORTANT]
> installatiekopieën van virtuele machines Hallo voor SQL Server Developer Hallo en Express-edities niet automatisch ingeschakeld Hallo TCP/IP-protocol. Voor ontwikkelaars en Express-edities, moet u SQL Server Configuration Manager te gebruiken[handmatig inschakelen Hallo TCP/IP-protocol](#manualtcp) Hallo na het maken van VM.

Particuliere connectiviteit wordt vaak gebruikt in combinatie met [virtueel netwerk](../../../virtual-network/virtual-networks-overview.md), waardoor verschillende scenario's. U kunt virtuele machines in hetzelfde virtuele netwerk, zelfs als deze virtuele machines bestaan in verschillende resourcegroepen Hallo verbinden. En met een [site-naar-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), kunt u een hybride-architectuur die virtuele machines met on-premises netwerken en machines verbindt.

Virtuele netwerken maken voor toojoin u ook uw virtuele Azure-machines tooa-domein. Dit is Hallo alleen manier toouse Windows-verificatie tooSQL Server. Hallo vereisen andere scenario's SQL-verificatie met gebruikersnamen en wachtwoorden.

Ervan uitgaande dat u DNS in het virtuele netwerk hebt geconfigureerd, kunt u SQL Server-exemplaar tooyour door Hallo virtuele machine van SQL Server-computernaam opgeven in de verbindingsreeks Hallo. Hallo volgt ook wordt ervan uitgegaan dat Windows-verificatie ook is geconfigureerd en die gebruiker Hallo toohello SQL Server-exemplaar toegang heeft gekregen.

```
Server=mysqlvm;Integrated Security=true
```

## <a id="change"></a>SQL-connectiviteitsinstellingen wijzigen

U kunt de connectiviteitsinstellingen van het Hallo wijzigen voor uw virtuele machine van SQL Server in hello Azure-portal.

1. Selecteer in de Azure-portal hello, **virtuele Machines**.

2. Selecteer uw SQL Server VM.

3. Onder **instellingen**, klikt u op **SQL Server-configuratiebestand**.

4. Wijziging Hallo **niveau van de SQL-connectiviteit** tooyour vereist instellen. Desgewenst kunt u dit gebied toochange Hallo SQL Server-poort of Hallo SQL-verificatie-instellingen.

   ![Wijzigen van de SQL-connectiviteit](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. Wacht enkele minuten tot Hallo update toocomplete.

   ![Updatebericht SQL VM](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <a id="manualtcp"></a>TCP/IP inschakelen voor ontwikkelaars en Express-edities

Bij het wijzigen van SQL Server-verbindingsinstellingen wordt Azure niet automatisch ingeschakeld Hallo TCP/IP-protocol voor SQL Server-ontwikkelaars en Express-edities. Hallo hieronder wordt uitgelegd hoe toomanually TCP/IP inschakelen zodat u kunt op afstand verbinding maken via IP-adres.

Eerst toohello SQL Server-computer verbinding met extern bureaublad.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

Schakel vervolgens Hallo TCP/IP-protocol met **SQL Server Configuration Manager**.

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a>Verbinden met SSMS

Hallo volgende stappen laten zien hoe toocreate een optionele DNS-server Label voor de virtuele machine van Azure en maak verbinding met SQL Server Management Studio (SSMS).

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a>Volgende stappen

inrichting instructies toosee samen met deze stappen connectiviteit Zie [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).

Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).

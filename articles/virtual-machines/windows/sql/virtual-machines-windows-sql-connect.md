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
# <a name="connect-tooa-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="bc6d2-105">Verbinding maken met tooa virtuele Machine van SQL Server op Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="bc6d2-105">Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc6d2-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="bc6d2-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="bc6d2-107">Klassiek</span><span class="sxs-lookup"><span data-stu-id="bc6d2-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="bc6d2-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="bc6d2-108">Overview</span></span>

<span data-ttu-id="bc6d2-109">Dit onderwerp wordt beschreven hoe tooconnect tooyour SQL Server-instantie uitgevoerd op een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-109">This topic describes how tooconnect tooyour SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="bc6d2-110">Dit omvat een aantal [algemene verbindingsproblemen scenario's](#connection-scenarios) en geeft vervolgens [gedetailleerde stappen voor het configureren van SQL-serververbindingen in een Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="bc6d2-111">Als u liever een volledig overzicht van beide, inrichten en connectiviteit, Zie [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="bc6d2-112">Scenario 's</span><span class="sxs-lookup"><span data-stu-id="bc6d2-112">Connection scenarios</span></span>

<span data-ttu-id="bc6d2-113">Hallo manier een client verbinding maakt tooSQL-Server op een virtuele Machine, is afhankelijk van Hallo-locatie van het Hallo-client en de netwerkconfiguratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-113">hello way a client connects tooSQL Server running on a Virtual Machine differs depending on hello location of hello client and hello networking configuration.</span></span>

<span data-ttu-id="bc6d2-114">Als u een SQL Server VM in hello Azure-portal inricht, hebt u de optie Hallo van het type Hallo opgeven **SQL-connectiviteit**.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-114">If you provision a SQL Server VM in hello Azure portal, you have hello option of specifying hello type of **SQL connectivity**.</span></span>

![Openbare SQL verbindingsoptie tijdens het inrichten](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="bc6d2-116">Uw opties voor connectiviteit zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="bc6d2-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="bc6d2-117">Optie</span><span class="sxs-lookup"><span data-stu-id="bc6d2-117">Option</span></span> | <span data-ttu-id="bc6d2-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="bc6d2-118">Description</span></span> |
|---|---|
| <span data-ttu-id="bc6d2-119">**Openbare**</span><span class="sxs-lookup"><span data-stu-id="bc6d2-119">**Public**</span></span> | <span data-ttu-id="bc6d2-120">TooSQL Server via Hallo verbinding maken met internet</span><span class="sxs-lookup"><span data-stu-id="bc6d2-120">Connect tooSQL Server over hello internet</span></span> |
| <span data-ttu-id="bc6d2-121">**Persoonlijke**</span><span class="sxs-lookup"><span data-stu-id="bc6d2-121">**Private**</span></span> | <span data-ttu-id="bc6d2-122">Verbinding maken met Server tooSQL in Hallo hetzelfde virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="bc6d2-122">Connect tooSQL Server in hello same virtual network</span></span> |
| <span data-ttu-id="bc6d2-123">**Lokale**</span><span class="sxs-lookup"><span data-stu-id="bc6d2-123">**Local**</span></span> | <span data-ttu-id="bc6d2-124">Verbinding maken met tooSQL Server lokaal op Hallo dezelfde virtuele machine</span><span class="sxs-lookup"><span data-stu-id="bc6d2-124">Connect tooSQL Server locally on hello same virtual machine</span></span> | 

<span data-ttu-id="bc6d2-125">Hallo volgende secties wordt uitgelegd Hallo **openbare** en **persoonlijke** opties in meer detail.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-125">hello following sections explain hello **Public** and **Private** options in more detail.</span></span>

## <a name="connect-toosql-server-over-hello-internet"></a><span data-ttu-id="bc6d2-126">Verbinding maken met tooSQL Server via Internet Hallo</span><span class="sxs-lookup"><span data-stu-id="bc6d2-126">Connect tooSQL Server over hello Internet</span></span>

<span data-ttu-id="bc6d2-127">Als u wilt dat tooconnect tooyour SQL Server database-engine van Hallo Internet, selecteert u **openbare** voor Hallo **SQL-connectiviteit** type in de portal Hallo tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-127">If you want tooconnect tooyour SQL Server database engine from hello Internet, select **Public** for hello **SQL connectivity** type in hello portal during provisioning.</span></span> <span data-ttu-id="bc6d2-128">Hallo-portal automatisch Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="bc6d2-128">hello portal automatically does hello following steps:</span></span>

* <span data-ttu-id="bc6d2-129">Hallo TCP/IP-protocol ingeschakeld voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-129">Enables hello TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="bc6d2-130">Hiermee configureert u een firewall regel tooopen Hallo SQL Server-TCP-poort (standaard 1433).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-130">Configures a firewall rule tooopen hello SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="bc6d2-131">Hiermee kunt SQL Server-verificatie vereist is voor openbare toegang.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="bc6d2-132">Netwerkbeveiligingsgroep hello configureert op Hallo VM tooall TCP-verkeer op Hallo van SQL Server-poort.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-132">Configures hello network security group on hello VM tooall TCP traffic on hello SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc6d2-133">installatiekopieën van virtuele machines Hallo voor SQL Server Developer Hallo en Express-edities niet automatisch ingeschakeld Hallo TCP/IP-protocol.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-133">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="bc6d2-134">Voor ontwikkelaars en Express-edities, moet u SQL Server Configuration Manager te gebruiken[handmatig inschakelen Hallo TCP/IP-protocol](#manualtcp) Hallo na het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-134">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="bc6d2-135">Een client met toegang tot internet verbinding kunt maken voor toohello SQL Server-exemplaar met geven Hallo openbaar IP-adres van Hallo virtuele machine of een DNS-label toothat IP-adres toegewezen.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-135">Any client with internet access can connect toohello SQL Server instance by specifying either hello public IP address of hello virtual machine or any DNS label assigned toothat IP address.</span></span> <span data-ttu-id="bc6d2-136">Als Hallo SQL Server-poort 1433, hoeft u niet toospecify in Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-136">If hello SQL Server port is 1433, you do not need toospecify it in hello connection string.</span></span> <span data-ttu-id="bc6d2-137">Hallo verbindingsreeks na tooa SQL VM is verbonden met een DNS-label van `sqlvmlabel.eastus.cloudapp.azure.com` via SQL-verificatie (u kunt ook Hallo openbaar IP-adres).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-137">hello following connection string connects tooa SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use hello public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="bc6d2-138">Hoewel dit wordt de connectiviteit mogelijk voor clients via internet Hallo, betekent dit niet dat iedereen tooyour SQL Server verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-138">Although this enables connectivity for clients over hello internet, this does not imply that anyone can connect tooyour SQL Server.</span></span> <span data-ttu-id="bc6d2-139">Externe clients hebben toohello juiste gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-139">Outside clients have toohello correct username and password.</span></span> <span data-ttu-id="bc6d2-140">Voor extra beveiliging kunt u echter een bekende Hallo-poort 1433 voorkomen.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-140">However, for additional security, you can avoid hello well-known port 1433.</span></span> <span data-ttu-id="bc6d2-141">Bijvoorbeeld, als u SQL Server-toolisten op poort 1500 en tot stand gebrachte correcte firewall en netwerkbeveiligingsgroepen hebt geconfigureerd, kan u door Hallo poort nummer toohello-servernaam toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-141">For example, if you configured SQL Server toolisten on port 1500 and established proper firewall and network security group rules, you could connect by appending hello port number toohello Server name.</span></span> <span data-ttu-id="bc6d2-142">Hallo volgende voorbeeld wijzigt Hallo vorige door een aangepast poortnummer toe te voegen **1500**, toohello servernaam:</span><span class="sxs-lookup"><span data-stu-id="bc6d2-142">hello following example alters hello previous one by adding a custom port number, **1500**, toohello server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="bc6d2-143">Als u SQL Server op een virtuele machine query's via internet, alle uitgaande gegevens Hallo van hello Azure datacenter onderwerp toonormal is [prijzen voor uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-143">When you query SQL Server in a VM over hello internet, all outgoing data from hello Azure datacenter is subject toonormal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-toosql-server-within-a-virtual-network"></a><span data-ttu-id="bc6d2-144">Verbinding maken met Server tooSQL binnen een virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="bc6d2-144">Connect tooSQL Server within a virtual network</span></span>

<span data-ttu-id="bc6d2-145">Wanneer u de optie **persoonlijke** voor Hallo **SQL-connectiviteit** type in Azure-portal Hallo configureert u de meeste Hallo dezelfde instellingen te**openbare**.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-145">When you choose **Private** for hello **SQL connectivity** type in hello portal, Azure configures most of hello settings identical too**Public**.</span></span> <span data-ttu-id="bc6d2-146">Hallo een verschil is dat er geen netwerk beveiliging groep regel tooallow buiten-verkeer op Hallo SQL Server-poort (standaard 1433).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-146">hello one difference is that there is no network security group rule tooallow outside traffic on hello SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc6d2-147">installatiekopieën van virtuele machines Hallo voor SQL Server Developer Hallo en Express-edities niet automatisch ingeschakeld Hallo TCP/IP-protocol.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-147">hello virtual machine images for hello SQL Server Developer and Express editions do not automatically enable hello TCP/IP protocol.</span></span> <span data-ttu-id="bc6d2-148">Voor ontwikkelaars en Express-edities, moet u SQL Server Configuration Manager te gebruiken[handmatig inschakelen Hallo TCP/IP-protocol](#manualtcp) Hallo na het maken van VM.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-148">For Developer and Express editions, you must use SQL Server Configuration Manager too[manually enable hello TCP/IP protocol](#manualtcp) after creating hello VM.</span></span>

<span data-ttu-id="bc6d2-149">Particuliere connectiviteit wordt vaak gebruikt in combinatie met [virtueel netwerk](../../../virtual-network/virtual-networks-overview.md), waardoor verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="bc6d2-150">U kunt virtuele machines in hetzelfde virtuele netwerk, zelfs als deze virtuele machines bestaan in verschillende resourcegroepen Hallo verbinden.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-150">You can connect VMs in hello same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="bc6d2-151">En met een [site-naar-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), kunt u een hybride-architectuur die virtuele machines met on-premises netwerken en machines verbindt.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="bc6d2-152">Virtuele netwerken maken voor toojoin u ook uw virtuele Azure-machines tooa-domein.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-152">Virtual networks also enable     you toojoin your Azure VMs tooa domain.</span></span> <span data-ttu-id="bc6d2-153">Dit is Hallo alleen manier toouse Windows-verificatie tooSQL Server.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-153">This is hello only way toouse Windows Authentication tooSQL Server.</span></span> <span data-ttu-id="bc6d2-154">Hallo vereisen andere scenario's SQL-verificatie met gebruikersnamen en wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-154">hello other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="bc6d2-155">Ervan uitgaande dat u DNS in het virtuele netwerk hebt geconfigureerd, kunt u SQL Server-exemplaar tooyour door Hallo virtuele machine van SQL Server-computernaam opgeven in de verbindingsreeks Hallo.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-155">Assuming that you have configured DNS in your virtual network, you can connect tooyour SQL Server instance by specifying hello SQL Server VM computer name in hello connection string.</span></span> <span data-ttu-id="bc6d2-156">Hallo volgt ook wordt ervan uitgegaan dat Windows-verificatie ook is geconfigureerd en die gebruiker Hallo toohello SQL Server-exemplaar toegang heeft gekregen.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-156">hello following example also assumes that Windows Authentication has also been configured and that hello user has been granted access toohello SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="bc6d2-157"><a id="change"></a>SQL-connectiviteitsinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="bc6d2-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="bc6d2-158">U kunt de connectiviteitsinstellingen van het Hallo wijzigen voor uw virtuele machine van SQL Server in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-158">You can change hello connectivity settings for your SQL Server virtual machine in hello Azure portal.</span></span>

1. <span data-ttu-id="bc6d2-159">Selecteer in de Azure-portal hello, **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-159">In hello Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="bc6d2-160">Selecteer uw SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="bc6d2-161">Onder **instellingen**, klikt u op **SQL Server-configuratiebestand**.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="bc6d2-162">Wijziging Hallo **niveau van de SQL-connectiviteit** tooyour vereist instellen.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-162">Change hello **SQL connectivity level** tooyour required setting.</span></span> <span data-ttu-id="bc6d2-163">Desgewenst kunt u dit gebied toochange Hallo SQL Server-poort of Hallo SQL-verificatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-163">You can optionally use this area toochange hello SQL Server port or hello SQL Authentication settings.</span></span>

   ![Wijzigen van de SQL-connectiviteit](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="bc6d2-165">Wacht enkele minuten tot Hallo update toocomplete.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-165">Wait several minutes for hello update toocomplete.</span></span>

   ![Updatebericht SQL VM](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="bc6d2-167"><a id="manualtcp"></a>TCP/IP inschakelen voor ontwikkelaars en Express-edities</span><span class="sxs-lookup"><span data-stu-id="bc6d2-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="bc6d2-168">Bij het wijzigen van SQL Server-verbindingsinstellingen wordt Azure niet automatisch ingeschakeld Hallo TCP/IP-protocol voor SQL Server-ontwikkelaars en Express-edities.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-168">When changing SQL Server connectivity settings, Azure does not automatically enable hello TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="bc6d2-169">Hallo hieronder wordt uitgelegd hoe toomanually TCP/IP inschakelen zodat u kunt op afstand verbinding maken via IP-adres.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-169">hello steps below explain how toomanually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="bc6d2-170">Eerst toohello SQL Server-computer verbinding met extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-170">First, connect toohello SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="bc6d2-171">Schakel vervolgens Hallo TCP/IP-protocol met **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="bc6d2-171">Next, enable hello TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect tooSQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="bc6d2-172">Verbinden met SSMS</span><span class="sxs-lookup"><span data-stu-id="bc6d2-172">Connect with SSMS</span></span>

<span data-ttu-id="bc6d2-173">Hallo volgende stappen laten zien hoe toocreate een optionele DNS-server Label voor de virtuele machine van Azure en maak verbinding met SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-173">hello following steps show how toocreate an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect tooSQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="bc6d2-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc6d2-174">Next Steps</span></span>

<span data-ttu-id="bc6d2-175">inrichting instructies toosee samen met deze stappen connectiviteit Zie [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-175">toosee provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="bc6d2-176">Voor andere onderwerpen die betrekking toorunning SQL-Server in Azure VM's hebben, Zie [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc6d2-176">For other topics related toorunning SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>

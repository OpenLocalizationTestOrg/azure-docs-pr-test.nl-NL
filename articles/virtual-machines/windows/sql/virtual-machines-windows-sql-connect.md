---
title: Verbinding maken met een virtuele Machine van SQL Server (Resource Manager) | Microsoft Docs
description: Informatie over het verbinding maken met SQL Server wordt uitgevoerd op een virtuele Machine in Azure. In dit onderwerp maakt gebruik van het klassieke implementatiemodel. De scenario's, is afhankelijk van de netwerkconfiguratie en de locatie van de client.
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
ms.openlocfilehash: 67ba43f9456bbeffbf602067586143c4c68af672
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-to-a-sql-server-virtual-machine-on-azure-resource-manager"></a><span data-ttu-id="404eb-105">Verbinding maken met een virtuele SQL Server-machine op Azure (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="404eb-105">Connect to a SQL Server Virtual Machine on Azure (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="404eb-106">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="404eb-106">Resource Manager</span></span>](virtual-machines-windows-sql-connect.md)
> * [<span data-ttu-id="404eb-107">Klassiek</span><span class="sxs-lookup"><span data-stu-id="404eb-107">Classic</span></span>](../classic/sql-connect.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="404eb-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="404eb-108">Overview</span></span>

<span data-ttu-id="404eb-109">Dit onderwerp wordt beschreven hoe u verbinding maken met uw SQL Server-exemplaar dat is uitgevoerd op een virtuele machine van Azure.</span><span class="sxs-lookup"><span data-stu-id="404eb-109">This topic describes how to connect to your SQL Server instance running on an Azure virtual machine.</span></span> <span data-ttu-id="404eb-110">Dit omvat een aantal [algemene verbindingsproblemen scenario's](#connection-scenarios) en geeft vervolgens [gedetailleerde stappen voor het configureren van SQL-serververbindingen in een Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="404eb-110">It covers some [general connectivity scenarios](#connection-scenarios) and then provides [detailed steps for configuring SQL Server connectivity in an Azure VM](#steps-for-manually-configuring-sql-server-connectivity-in-an-azure-vm).</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="404eb-111">Als u liever een volledig overzicht van beide, inrichten en connectiviteit, Zie [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="404eb-111">If you would rather have a full walk-through of both provisioning and connectivity, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="connection-scenarios"></a><span data-ttu-id="404eb-112">Scenario 's</span><span class="sxs-lookup"><span data-stu-id="404eb-112">Connection scenarios</span></span>

<span data-ttu-id="404eb-113">De manier waarop die een client verbinding maakt met SQL Server op een virtuele Machine wordt uitgevoerd, is afhankelijk van de locatie van de client en de netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="404eb-113">The way a client connects to SQL Server running on a Virtual Machine differs depending on the location of the client and the networking configuration.</span></span>

<span data-ttu-id="404eb-114">Als u een virtuele SQL Server-machine in de Azure portal inricht, hebt u de optie voor het opgeven van het type **SQL-connectiviteit**.</span><span class="sxs-lookup"><span data-stu-id="404eb-114">If you provision a SQL Server VM in the Azure portal, you have the option of specifying the type of **SQL connectivity**.</span></span>

![Openbare SQL verbindingsoptie tijdens het inrichten](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity.png)

<span data-ttu-id="404eb-116">Uw opties voor connectiviteit zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="404eb-116">Your options for connectivity include:</span></span>

| <span data-ttu-id="404eb-117">Optie</span><span class="sxs-lookup"><span data-stu-id="404eb-117">Option</span></span> | <span data-ttu-id="404eb-118">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="404eb-118">Description</span></span> |
|---|---|
| <span data-ttu-id="404eb-119">**Openbare**</span><span class="sxs-lookup"><span data-stu-id="404eb-119">**Public**</span></span> | <span data-ttu-id="404eb-120">Via internet verbinding maken met SQL Server</span><span class="sxs-lookup"><span data-stu-id="404eb-120">Connect to SQL Server over the internet</span></span> |
| <span data-ttu-id="404eb-121">**Persoonlijke**</span><span class="sxs-lookup"><span data-stu-id="404eb-121">**Private**</span></span> | <span data-ttu-id="404eb-122">Verbinding maken met SQL Server in hetzelfde virtuele netwerk</span><span class="sxs-lookup"><span data-stu-id="404eb-122">Connect to SQL Server in the same virtual network</span></span> |
| <span data-ttu-id="404eb-123">**Lokale**</span><span class="sxs-lookup"><span data-stu-id="404eb-123">**Local**</span></span> | <span data-ttu-id="404eb-124">Verbinding maken met SQL Server lokaal op dezelfde virtuele machine</span><span class="sxs-lookup"><span data-stu-id="404eb-124">Connect to SQL Server locally on the same virtual machine</span></span> | 

<span data-ttu-id="404eb-125">De volgende secties worden de **openbare** en **persoonlijke** opties in meer detail.</span><span class="sxs-lookup"><span data-stu-id="404eb-125">The following sections explain the **Public** and **Private** options in more detail.</span></span>

## <a name="connect-to-sql-server-over-the-internet"></a><span data-ttu-id="404eb-126">Verbinding maken met SQL Server via Internet</span><span class="sxs-lookup"><span data-stu-id="404eb-126">Connect to SQL Server over the Internet</span></span>

<span data-ttu-id="404eb-127">Als u verbinding maken met uw SQL Server database-engine van het Internet wilt, selecteert u **openbare** voor de **SQL-connectiviteit** type in de portal tijdens het inrichten.</span><span class="sxs-lookup"><span data-stu-id="404eb-127">If you want to connect to your SQL Server database engine from the Internet, select **Public** for the **SQL connectivity** type in the portal during provisioning.</span></span> <span data-ttu-id="404eb-128">De portal wordt automatisch de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="404eb-128">The portal automatically does the following steps:</span></span>

* <span data-ttu-id="404eb-129">Hiermee kunt het TCP/IP-protocol voor SQL Server.</span><span class="sxs-lookup"><span data-stu-id="404eb-129">Enables the TCP/IP protocol for SQL Server.</span></span>
* <span data-ttu-id="404eb-130">Hiermee configureert u een firewallregel in voor het openen van de SQL Server-TCP-poort (standaard 1433).</span><span class="sxs-lookup"><span data-stu-id="404eb-130">Configures a firewall rule to open the SQL Server TCP port (default 1433).</span></span>
* <span data-ttu-id="404eb-131">Hiermee kunt SQL Server-verificatie vereist is voor openbare toegang.</span><span class="sxs-lookup"><span data-stu-id="404eb-131">Enables SQL Server Authentication, required for public access.</span></span>
* <span data-ttu-id="404eb-132">Hiermee configureert u de netwerkbeveiligingsgroep op de virtuele machine voor alle TCP-verkeer op de SQL Server-poort.</span><span class="sxs-lookup"><span data-stu-id="404eb-132">Configures the network security group on the VM to all TCP traffic on the SQL Server port.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="404eb-133">Installatiekopieën van virtuele machines voor de SQL Server-ontwikkelaars en Express-edities het TCP/IP-protocol niet automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="404eb-133">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="404eb-134">Voor ontwikkelaars en Express-edities, moet u SQL Server Configuration Manager te gebruiken [handmatig het TCP/IP-protocol inschakelen](#manualtcp) na het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="404eb-134">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="404eb-135">Een client met internettoegang kan verbinding maken met SQL Server-exemplaar door ofwel het openbare IP-adres van de virtuele machine of een DNS-label toegewezen aan dat IP-adres te geven.</span><span class="sxs-lookup"><span data-stu-id="404eb-135">Any client with internet access can connect to the SQL Server instance by specifying either the public IP address of the virtual machine or any DNS label assigned to that IP address.</span></span> <span data-ttu-id="404eb-136">Als de SQL Server-poort 1433, hoeft u niet opgeven in de verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="404eb-136">If the SQL Server port is 1433, you do not need to specify it in the connection string.</span></span> <span data-ttu-id="404eb-137">De volgende verbindingsreeks verbinding maakt met een SQL-VM met een DNS-label `sqlvmlabel.eastus.cloudapp.azure.com` via SQL-verificatie (u kunt ook het openbare IP-adres).</span><span class="sxs-lookup"><span data-stu-id="404eb-137">The following connection string connects to a SQL VM with a DNS label of `sqlvmlabel.eastus.cloudapp.azure.com` using SQL Authentication (you could also use the public IP address).</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com;Integrated Security=false;User ID=<login_name>;Password=<your_password>
```

<span data-ttu-id="404eb-138">Hoewel dit wordt de connectiviteit mogelijk voor clients via internet, betekent dit niet dat iedereen verbinding kan maken met uw SQL-Server.</span><span class="sxs-lookup"><span data-stu-id="404eb-138">Although this enables connectivity for clients over the internet, this does not imply that anyone can connect to your SQL Server.</span></span> <span data-ttu-id="404eb-139">Buiten hebben clients op de juiste gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="404eb-139">Outside clients have to the correct username and password.</span></span> <span data-ttu-id="404eb-140">Voor extra beveiliging kunt u echter de standaardpoort 1433 voorkomen.</span><span class="sxs-lookup"><span data-stu-id="404eb-140">However, for additional security, you can avoid the well-known port 1433.</span></span> <span data-ttu-id="404eb-141">Bijvoorbeeld, als u SQL Server om te luisteren op poort 1500 en tot stand gebrachte correcte firewall- en netwerkbeveiligingsgroepen hebt geconfigureerd, kan u door het poortnummer op de naam van de Server toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="404eb-141">For example, if you configured SQL Server to listen on port 1500 and established proper firewall and network security group rules, you could connect by appending the port number to the Server name.</span></span> <span data-ttu-id="404eb-142">Het volgende voorbeeld wijzigt u de vorige taak door een aangepast poortnummer toe te voegen **1500**, naar de server:</span><span class="sxs-lookup"><span data-stu-id="404eb-142">The following example alters the previous one by adding a custom port number, **1500**, to the server name:</span></span>

```
Server=sqlvmlabel.eastus.cloudapp.azure.com,1500;Integrated Security=false;User ID=<login_name>;Password=<your_password>"
```

> [!NOTE]
> <span data-ttu-id="404eb-143">Als u een query's van SQL Server op een virtuele machine via het internet, alle uitgaande gegevens van de Azure-datacenter is onderworpen aan normaal [prijzen voor uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/).</span><span class="sxs-lookup"><span data-stu-id="404eb-143">When you query SQL Server in a VM over the internet, all outgoing data from the Azure datacenter is subject to normal [pricing on outbound data transfers](https://azure.microsoft.com/pricing/details/data-transfers/).</span></span>

## <a name="connect-to-sql-server-within-a-virtual-network"></a><span data-ttu-id="404eb-144">Binnen een virtueel netwerk verbinding maken met SQL Server</span><span class="sxs-lookup"><span data-stu-id="404eb-144">Connect to SQL Server within a virtual network</span></span>

<span data-ttu-id="404eb-145">Wanneer u de optie **persoonlijke** voor de **SQL-connectiviteit** type in de Azure-portal configureert u de instellingen die identiek is aan de meeste **openbare**.</span><span class="sxs-lookup"><span data-stu-id="404eb-145">When you choose **Private** for the **SQL connectivity** type in the portal, Azure configures most of the settings identical to **Public**.</span></span> <span data-ttu-id="404eb-146">Een verschil is dat er geen groep van de netwerkbeveiligingsregel om toe te staan buiten verkeer op de SQL Server-poort (standaard 1433).</span><span class="sxs-lookup"><span data-stu-id="404eb-146">The one difference is that there is no network security group rule to allow outside traffic on the SQL Server port (default 1433).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="404eb-147">Installatiekopieën van virtuele machines voor de SQL Server-ontwikkelaars en Express-edities het TCP/IP-protocol niet automatisch ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="404eb-147">The virtual machine images for the SQL Server Developer and Express editions do not automatically enable the TCP/IP protocol.</span></span> <span data-ttu-id="404eb-148">Voor ontwikkelaars en Express-edities, moet u SQL Server Configuration Manager te gebruiken [handmatig het TCP/IP-protocol inschakelen](#manualtcp) na het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="404eb-148">For Developer and Express editions, you must use SQL Server Configuration Manager to [manually enable the TCP/IP protocol](#manualtcp) after creating the VM.</span></span>

<span data-ttu-id="404eb-149">Particuliere connectiviteit wordt vaak gebruikt in combinatie met [virtueel netwerk](../../../virtual-network/virtual-networks-overview.md), waardoor verschillende scenario's.</span><span class="sxs-lookup"><span data-stu-id="404eb-149">Private connectivity is often used in conjunction with [Virtual Network](../../../virtual-network/virtual-networks-overview.md), which enables several scenarios.</span></span> <span data-ttu-id="404eb-150">Zelfs als deze virtuele machines bestaan in verschillende resourcegroepen, kunt u virtuele machines in hetzelfde virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="404eb-150">You can connect VMs in the same virtual network, even if those VMs exist in different resource groups.</span></span> <span data-ttu-id="404eb-151">En met een [site-naar-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), kunt u een hybride-architectuur die virtuele machines met on-premises netwerken en machines verbindt.</span><span class="sxs-lookup"><span data-stu-id="404eb-151">And with a [site-to-site VPN](../../../vpn-gateway/vpn-gateway-site-to-site-create.md), you can create a hybrid architecture that connects VMs with on-premises networks and machines.</span></span>

<span data-ttu-id="404eb-152">Virtuele netwerken kunnen u uw Azure VM's toevoegen aan een domein.</span><span class="sxs-lookup"><span data-stu-id="404eb-152">Virtual networks also enable     you to join your Azure VMs to a domain.</span></span> <span data-ttu-id="404eb-153">Dit is de enige manier om Windows-verificatie met SQL Server gebruiken.</span><span class="sxs-lookup"><span data-stu-id="404eb-153">This is the only way to use Windows Authentication to SQL Server.</span></span> <span data-ttu-id="404eb-154">De andere scenario's vereisen SQL-verificatie met gebruikersnamen en wachtwoorden.</span><span class="sxs-lookup"><span data-stu-id="404eb-154">The other connection scenarios require SQL Authentication with user names and passwords.</span></span>

<span data-ttu-id="404eb-155">Ervan uitgaande dat u DNS in het virtuele netwerk hebt geconfigureerd, kunt u verbinding met uw exemplaar van SQL Server door op te geven van de naam van de virtuele machine van SQL Server-computer in de verbindingstekenreeks.</span><span class="sxs-lookup"><span data-stu-id="404eb-155">Assuming that you have configured DNS in your virtual network, you can connect to your SQL Server instance by specifying the SQL Server VM computer name in the connection string.</span></span> <span data-ttu-id="404eb-156">Het volgende voorbeeld wordt ervan uitgegaan dat ook Windows-verificatie is geconfigureerd en dat de gebruiker toegang tot de SQL Server-exemplaar gekregen heeft.</span><span class="sxs-lookup"><span data-stu-id="404eb-156">The following example also assumes that Windows Authentication has also been configured and that the user has been granted access to the SQL Server instance.</span></span>

```
Server=mysqlvm;Integrated Security=true
```

## <span data-ttu-id="404eb-157"><a id="change"></a>SQL-connectiviteitsinstellingen wijzigen</span><span class="sxs-lookup"><span data-stu-id="404eb-157"><a id="change"></a> Change SQL connectivity settings</span></span>

<span data-ttu-id="404eb-158">U kunt de connectiviteitsinstellingen wijzigen voor uw virtuele machine van SQL Server in de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="404eb-158">You can change the connectivity settings for your SQL Server virtual machine in the Azure portal.</span></span>

1. <span data-ttu-id="404eb-159">Selecteer in de Azure-portal **virtuele Machines**.</span><span class="sxs-lookup"><span data-stu-id="404eb-159">In the Azure portal, select **Virtual Machines**.</span></span>

2. <span data-ttu-id="404eb-160">Selecteer uw SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="404eb-160">Select your SQL Server VM.</span></span>

3. <span data-ttu-id="404eb-161">Onder **instellingen**, klikt u op **SQL Server-configuratiebestand**.</span><span class="sxs-lookup"><span data-stu-id="404eb-161">Under **Settings**, click **SQL Server configuration**.</span></span>

4. <span data-ttu-id="404eb-162">Wijzig de **niveau van de SQL-connectiviteit** naar de vereiste instelling.</span><span class="sxs-lookup"><span data-stu-id="404eb-162">Change the **SQL connectivity level** to your required setting.</span></span> <span data-ttu-id="404eb-163">Desgewenst kunt u dit gebied kunt u de SQL Server-poort of de SQL-verificatie-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="404eb-163">You can optionally use this area to change the SQL Server port or the SQL Authentication settings.</span></span>

   ![Wijzigen van de SQL-connectiviteit](./media/virtual-machines-windows-sql-connect/sql-vm-portal-connectivity-change.png)

5. <span data-ttu-id="404eb-165">Wacht enkele minuten voor de update te voltooien.</span><span class="sxs-lookup"><span data-stu-id="404eb-165">Wait several minutes for the update to complete.</span></span>

   ![Updatebericht SQL VM](./media/virtual-machines-windows-sql-connect/sql-vm-updating-notification.png)

## <span data-ttu-id="404eb-167"><a id="manualtcp"></a>TCP/IP inschakelen voor ontwikkelaars en Express-edities</span><span class="sxs-lookup"><span data-stu-id="404eb-167"><a id="manualtcp"></a> Enable TCP/IP for Developer and Express editions</span></span>

<span data-ttu-id="404eb-168">Bij het wijzigen van SQL Server-verbindingsinstellingen wordt Azure niet automatisch ingeschakeld het TCP/IP-protocol voor SQL Server-ontwikkelaars en Express-edities.</span><span class="sxs-lookup"><span data-stu-id="404eb-168">When changing SQL Server connectivity settings, Azure does not automatically enable the TCP/IP protocol for SQL Server Developer and Express editions.</span></span> <span data-ttu-id="404eb-169">In de onderstaande stappen wordt uitgelegd hoe u TCP/IP handmatig kunt inschakelen, zodat u op afstand via een IP-adres verbinding kunt maken.</span><span class="sxs-lookup"><span data-stu-id="404eb-169">The steps below explain how to manually enable TCP/IP so that you can connect remotely by IP address.</span></span>

<span data-ttu-id="404eb-170">Eerst verbinding met de SQL Server-machine via Extern bureaublad.</span><span class="sxs-lookup"><span data-stu-id="404eb-170">First, connect to the SQL Server machine with remote desktop.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-remote-desktop-connect.md)]

<span data-ttu-id="404eb-171">Schakel vervolgens het TCP/IP-protocol **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="404eb-171">Next, enable the TCP/IP protocol with **SQL Server Configuration Manager**.</span></span>

> [!INCLUDE [Connect to SQL Server VM with remote desktop](../../../../includes/virtual-machines-sql-server-connection-tcp-protocol.md)]

## <a name="connect-with-ssms"></a><span data-ttu-id="404eb-172">Verbinden met SSMS</span><span class="sxs-lookup"><span data-stu-id="404eb-172">Connect with SSMS</span></span>

<span data-ttu-id="404eb-173">De volgende stappen laten zien hoe een optionele DNS-Label maken voor uw virtuele machine van Azure en maak verbinding met SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="404eb-173">The following steps show how to create an optional DNS Label for your Azure VM and then connect with SQL Server Management Studio (SSMS).</span></span>

[!INCLUDE [Connect to SQL Server in a VM Resource Manager](../../../../includes/virtual-machines-sql-server-connection-steps-resource-manager.md)]

## <a name="next-steps"></a><span data-ttu-id="404eb-174">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="404eb-174">Next Steps</span></span>

<span data-ttu-id="404eb-175">Zie voor instructies samen met deze stappen connectiviteit inrichting [inrichten van een virtuele Machine van SQL Server op Azure](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="404eb-175">To see provisioning instructions along with these connectivity steps, see [Provisioning a SQL Server Virtual Machine on Azure](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

<span data-ttu-id="404eb-176">Zie voor andere onderwerpen die betrekking hebben op SQL Server wordt uitgevoerd in Azure VM's [SQL Server op Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="404eb-176">For other topics related to running SQL Server in Azure VMs, see [SQL Server on Azure Virtual Machines](virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
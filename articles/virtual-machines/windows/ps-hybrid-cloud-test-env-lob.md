---
title: testomgeving aaaLOB-toepassing | Microsoft Docs
description: Meer informatie over hoe een webgebaseerde toocreate line-of-business-toepassing in een hybride omgeving voor cloud IT pro of ontwikkeling testen.
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="82a26-103">Een webgebaseerde LOB-toepassing instellen in een hybride cloud voor testen</span><span class="sxs-lookup"><span data-stu-id="82a26-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="82a26-104">In dit onderwerp begeleidt u stapsgewijs hoe u een gesimuleerde hybride cloud-omgeving voor het testen van een web gebaseerde line-of-business (LOB)-toepassing die wordt gehost in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="82a26-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="82a26-105">Hier wordt de resulterende configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="82a26-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="82a26-106">Deze configuratie bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="82a26-106">This configuration consists of:</span></span>

* <span data-ttu-id="82a26-107">Een gesimuleerde on-premises netwerk wordt gehost in Azure (hello TestLab VNet).</span><span class="sxs-lookup"><span data-stu-id="82a26-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="82a26-108">Een cross-premises virtueel netwerk gehost in Azure (TestVNET).</span><span class="sxs-lookup"><span data-stu-id="82a26-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="82a26-109">Een VNet-naar-VNet-VPN-verbinding.</span><span class="sxs-lookup"><span data-stu-id="82a26-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="82a26-110">Een web gebaseerde LOB-server, SQL server en secundaire domeincontroller in het Hallo TestVNET virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="82a26-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="82a26-111">Deze configuratie biedt een basis- en algemene beginpunt van waaruit u kunt:</span><span class="sxs-lookup"><span data-stu-id="82a26-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="82a26-112">Ontwikkelen en testen van LOB-toepassingen die worden gehost op Internet Information Services (IIS) met een SQL Server 2014 back-end-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="82a26-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="82a26-113">Testen van deze gesimuleerde hybride cloud-gebaseerde IT workload.</span><span class="sxs-lookup"><span data-stu-id="82a26-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="82a26-114">Er zijn drie belangrijke fasen toosetting u deze testomgeving van hybride cloud:</span><span class="sxs-lookup"><span data-stu-id="82a26-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="82a26-115">Hallo gesimuleerde hybride cloudomgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="82a26-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="82a26-116">Configureer Hallo SQL-servercomputer (SQL1).</span><span class="sxs-lookup"><span data-stu-id="82a26-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="82a26-117">Hallo LOB-server (LOB1) configureren.</span><span class="sxs-lookup"><span data-stu-id="82a26-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="82a26-118">Deze werkbelasting vereist een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="82a26-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="82a26-119">Als u een MSDN- of Visual Studio-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="82a26-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="82a26-120">Zie voor een voorbeeld van een productie LOB-toepassing die wordt gehost in Azure, Hallo **Line-of-business-toepassingen** architectuur blauwdruk op [Microsoft Software architectuur's en blauwdrukken](http://msdn.microsoft.com/dn630664).</span><span class="sxs-lookup"><span data-stu-id="82a26-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="82a26-121">Fase 1: Hallo gesimuleerde hybride cloudomgeving instellen</span><span class="sxs-lookup"><span data-stu-id="82a26-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="82a26-122">Hallo maken [gesimuleerde hybride cloud-testomgeving](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82a26-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="82a26-123">Omdat deze testomgeving Hallo aanwezigheid van Hallo APP1-server op Hallo Corpnet-subnet niet vereist, kunt u deze afsluiten nu.</span><span class="sxs-lookup"><span data-stu-id="82a26-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="82a26-124">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="82a26-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="82a26-125">Fase 2: Configureer Hallo SQL-servercomputer (SQL1)</span><span class="sxs-lookup"><span data-stu-id="82a26-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="82a26-126">Start op Hallo Azure-portal, Hallo DC2 computer indien nodig.</span><span class="sxs-lookup"><span data-stu-id="82a26-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="82a26-127">Maak vervolgens een virtuele machine voor SQL1 met de volgende opdrachten bij een Azure PowerShell-opdrachtprompt op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="82a26-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="82a26-128">Eerdere toorunning deze opdrachten invullen Hallo waarden van variabelen en verwijder Hallo < en > tekens.</span><span class="sxs-lookup"><span data-stu-id="82a26-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="82a26-129">Gebruik hello Azure portal tooconnect tooSQL1 met lokale administrator-account Hallo van SQL1.</span><span class="sxs-lookup"><span data-stu-id="82a26-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="82a26-130">Vervolgens configureert Windows Firewall regels tooallow basisconnectiviteit testen en SQL Server-verkeer.</span><span class="sxs-lookup"><span data-stu-id="82a26-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="82a26-131">Voer deze opdrachten uit vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op SQL1.</span><span class="sxs-lookup"><span data-stu-id="82a26-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="82a26-132">Hallo ping-opdracht moet resulteren in vier geslaagde antwoorden van IP-adres 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="82a26-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="82a26-133">Vervolgens voegt u Hallo extra gegevensschijf op SQL1 als een nieuw volume met de stationsletter Hallo F:.</span><span class="sxs-lookup"><span data-stu-id="82a26-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="82a26-134">In Hallo linkerdeelvenster van Serverbeheer, klikt u op **File and Storage Services**, en klik vervolgens op **schijven**.</span><span class="sxs-lookup"><span data-stu-id="82a26-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="82a26-135">In het Hallo inhoudsdeelvenster Hallo **schijven** groep, klikt u op **schijf 2** (Hello **partitie** instellen te**onbekende**).</span><span class="sxs-lookup"><span data-stu-id="82a26-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="82a26-136">Klik op **taken**, en klik vervolgens op **NieuwVolume**.</span><span class="sxs-lookup"><span data-stu-id="82a26-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="82a26-137">Hallo voordat u een pagina van Wizard Nieuw Volume hello, klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="82a26-138">Klik op Hallo Selecteer Hallo-server en schijfpagina op **schijf 2**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="82a26-139">Wanneer u wordt gevraagd, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="82a26-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="82a26-140">Klik op Hallo Hallo grootte opgeven van Hallo volume pagina, **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="82a26-141">Klik op Hallo toewijzen tooa station stationsletter of map pagina op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="82a26-142">Klik op Hallo bestand selecteren pagina systeeminstellingen, **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="82a26-143">Klik op de pagina van het Hallo bevestigen selecties **maken**.</span><span class="sxs-lookup"><span data-stu-id="82a26-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="82a26-144">Wanneer voltooid, klikt u op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="82a26-144">When complete, click **Close**.</span></span>

<span data-ttu-id="82a26-145">Deze opdrachten uitvoeren op Hallo Windows PowerShell-opdrachtprompt op SQL1:</span><span class="sxs-lookup"><span data-stu-id="82a26-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="82a26-146">Voeg vervolgens SQL1 toohello CORP Windows Server Active Directory-domein met de volgende opdrachten bij de Windows PowerShell-prompt Hallo op SQL1.</span><span class="sxs-lookup"><span data-stu-id="82a26-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="82a26-147">Gebruik Hallo corp\gebruiker1 account wanneer u wordt gevraagd de domeinaccountreferenties toosupply voor Hallo **Add-Computer** opdracht.</span><span class="sxs-lookup"><span data-stu-id="82a26-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="82a26-148">Start opnieuw op en gebruik hello Azure portal tooconnect tooSQL1 *met lokale administrator-account van SQL1 hello*.</span><span class="sxs-lookup"><span data-stu-id="82a26-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="82a26-149">Configureer vervolgens SQL Server 2014 toouse Hallo F: station voor nieuwe databases en machtigingen van gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="82a26-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="82a26-150">Typ vanuit het startscherm Hallo **SQL Server Management**, en klik vervolgens op **SQL Server 2014 Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="82a26-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="82a26-151">In **verbinding tooServer**, klikt u op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="82a26-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="82a26-152">In het structuurvenster van de Hallo Object Explorer met de rechtermuisknop **SQL1**, en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="82a26-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="82a26-153">In Hallo **servereigenschappen** venster, klikt u op **Database-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="82a26-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="82a26-154">Zoek Hallo **Database standaardlocaties** en deze waarden instellen:</span><span class="sxs-lookup"><span data-stu-id="82a26-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="82a26-155">Voor **gegevens**, tekst hello pad **f:\Data**.</span><span class="sxs-lookup"><span data-stu-id="82a26-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="82a26-156">Voor **logboek**, tekst hello pad **f:\Log**.</span><span class="sxs-lookup"><span data-stu-id="82a26-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="82a26-157">Voor **back-up**, tekst hello pad **f:\Backup**.</span><span class="sxs-lookup"><span data-stu-id="82a26-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="82a26-158">Opmerking: Alleen nieuwe databases gebruiken deze locaties.</span><span class="sxs-lookup"><span data-stu-id="82a26-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="82a26-159">Klik op Hallo **OK** tooclose Hallo venster.</span><span class="sxs-lookup"><span data-stu-id="82a26-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="82a26-160">In Hallo **Objectverkenner** structuurvenster van de open **beveiliging**.</span><span class="sxs-lookup"><span data-stu-id="82a26-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="82a26-161">Met de rechtermuisknop op **aanmeldingen** en klik vervolgens op **New Login**.</span><span class="sxs-lookup"><span data-stu-id="82a26-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="82a26-162">In **aanmeldingsnaam**, type **corp\gebruiker1**.</span><span class="sxs-lookup"><span data-stu-id="82a26-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="82a26-163">Op Hallo **serverfuncties** pagina, klikt u op **sysadmin**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="82a26-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="82a26-164">Sluit Microsoft SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="82a26-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="82a26-165">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="82a26-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="82a26-166">Fase 3: Hallo LOB-server (LOB1) configureren</span><span class="sxs-lookup"><span data-stu-id="82a26-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="82a26-167">Maak eerst een virtuele machine voor LOB1 met de volgende opdrachten bij hello Azure PowerShell-opdrachtprompt op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="82a26-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="82a26-168">Gebruik vervolgens hello Azure portal tooconnect tooLOB1 met referenties van de lokale beheerdersaccount Hallo van LOB1 Hallo.</span><span class="sxs-lookup"><span data-stu-id="82a26-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="82a26-169">Configureer vervolgens een Windows Firewall tooallow verkeer van de regel voor het testen van verbinding.</span><span class="sxs-lookup"><span data-stu-id="82a26-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="82a26-170">Voer deze opdrachten uit vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op LOB1.</span><span class="sxs-lookup"><span data-stu-id="82a26-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="82a26-171">Hallo ping-opdracht moet resulteren in vier geslaagde antwoorden van IP-adres 192.168.0.4.</span><span class="sxs-lookup"><span data-stu-id="82a26-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="82a26-172">Voeg vervolgens LOB1 toohello CORP Active Directory-domein met de volgende opdrachten bij Hallo Windows PowerShell-prompt.</span><span class="sxs-lookup"><span data-stu-id="82a26-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="82a26-173">Gebruik Hallo corp\gebruiker1 account wanneer u wordt gevraagd de domeinaccountreferenties toosupply voor Hallo **Add-Computer** opdracht.</span><span class="sxs-lookup"><span data-stu-id="82a26-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="82a26-174">Start opnieuw op en hello Azure portal tooconnect tooLOB1 met Hallo corp\gebruiker1-account en wachtwoord te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="82a26-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="82a26-175">Vervolgens LOB1 voor IIS configureren en testen van de toegang van CLIENT1.</span><span class="sxs-lookup"><span data-stu-id="82a26-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="82a26-176">Klik in Serverbeheer **functies en onderdelen toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="82a26-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="82a26-177">Op Hallo **voordat u begint met** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="82a26-178">Op Hallo **installatietype selecteren** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="82a26-179">Op Hallo **Select doelserver** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="82a26-180">Op Hallo **serverfuncties** pagina, klikt u op **webserver (IIS)** in de lijst met Hallo **rollen**.</span><span class="sxs-lookup"><span data-stu-id="82a26-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="82a26-181">Wanneer u wordt gevraagd, klikt u op **onderdelen toevoegen**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="82a26-182">Op Hallo **functies selecteren** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="82a26-183">Op Hallo **webserver (IIS)** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="82a26-184">Op Hallo **Functieservices selecteren** pagina selecteren of schakel de selectievakjes Hallo voor Hallo-services die u nodig hebt voor het testen van uw LOB-toepassing en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="82a26-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="82a26-185">Op Hallo **installatieselecties bevestigen** pagina, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="82a26-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="82a26-186">Wacht totdat het Hallo-installatie van onderdelen is voltooid en klik vervolgens op **sluiten**.</span><span class="sxs-lookup"><span data-stu-id="82a26-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="82a26-187">Toohello CLIENT1-computer verbinding met de referenties van de account corp\gebruiker1 Hallo vanaf hello Azure-portal, en start Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="82a26-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="82a26-188">Typ in de adresbalk Hallo **http://lob1/** en druk op ENTER.</span><span class="sxs-lookup"><span data-stu-id="82a26-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="82a26-189">U ziet Hallo IIS 8 standaardwebpagina.</span><span class="sxs-lookup"><span data-stu-id="82a26-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="82a26-190">Dit is de huidige configuratie.</span><span class="sxs-lookup"><span data-stu-id="82a26-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="82a26-191">Deze omgeving is nu klaar voor toodeploy u uw webtoepassing op LOB1 en test functionaliteit van CLIENT1 op Hallo Corpnet-subnet.</span><span class="sxs-lookup"><span data-stu-id="82a26-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="82a26-192">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="82a26-192">Next step</span></span>
* <span data-ttu-id="82a26-193">Voeg een nieuwe virtuele machine met behulp van Hallo [Azure-portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="82a26-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


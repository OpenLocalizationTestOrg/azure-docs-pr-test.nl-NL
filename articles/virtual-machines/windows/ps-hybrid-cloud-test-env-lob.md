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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>Een webgebaseerde LOB-toepassing instellen in een hybride cloud voor testen
In dit onderwerp begeleidt u stapsgewijs hoe u een gesimuleerde hybride cloud-omgeving voor het testen van een web gebaseerde line-of-business (LOB)-toepassing die wordt gehost in Microsoft Azure. Hier wordt de resulterende configuratie Hallo.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Deze configuratie bestaat uit:

* Een gesimuleerde on-premises netwerk wordt gehost in Azure (hello TestLab VNet).
* Een cross-premises virtueel netwerk gehost in Azure (TestVNET).
* Een VNet-naar-VNet-VPN-verbinding.
* Een web gebaseerde LOB-server, SQL server en secundaire domeincontroller in het Hallo TestVNET virtuele netwerk.

Deze configuratie biedt een basis- en algemene beginpunt van waaruit u kunt:

* Ontwikkelen en testen van LOB-toepassingen die worden gehost op Internet Information Services (IIS) met een SQL Server 2014 back-end-database in Azure.
* Testen van deze gesimuleerde hybride cloud-gebaseerde IT workload.

Er zijn drie belangrijke fasen toosetting u deze testomgeving van hybride cloud:

1. Hallo gesimuleerde hybride cloudomgeving instellen.
2. Configureer Hallo SQL-servercomputer (SQL1).
3. Hallo LOB-server (LOB1) configureren.

Deze werkbelasting vereist een Azure-abonnement. Als u een MSDN- of Visual Studio-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).

Zie voor een voorbeeld van een productie LOB-toepassing die wordt gehost in Azure, Hallo **Line-of-business-toepassingen** architectuur blauwdruk op [Microsoft Software architectuur's en blauwdrukken](http://msdn.microsoft.com/dn630664).

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>Fase 1: Hallo gesimuleerde hybride cloudomgeving instellen
Hallo maken [gesimuleerde hybride cloud-testomgeving](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Omdat deze testomgeving Hallo aanwezigheid van Hallo APP1-server op Hallo Corpnet-subnet niet vereist, kunt u deze afsluiten nu.

Dit is de huidige configuratie.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>Fase 2: Configureer Hallo SQL-servercomputer (SQL1)
Start op Hallo Azure-portal, Hallo DC2 computer indien nodig.

Maak vervolgens een virtuele machine voor SQL1 met de volgende opdrachten bij een Azure PowerShell-opdrachtprompt op de lokale computer. Eerdere toorunning deze opdrachten invullen Hallo waarden van variabelen en verwijder Hallo < en > tekens.

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

Gebruik hello Azure portal tooconnect tooSQL1 met lokale administrator-account Hallo van SQL1.

Vervolgens configureert Windows Firewall regels tooallow basisconnectiviteit testen en SQL Server-verkeer. Voer deze opdrachten uit vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op SQL1.

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

Hallo ping-opdracht moet resulteren in vier geslaagde antwoorden van IP-adres 192.168.0.4.

Vervolgens voegt u Hallo extra gegevensschijf op SQL1 als een nieuw volume met de stationsletter Hallo F:.

1. In Hallo linkerdeelvenster van Serverbeheer, klikt u op **File and Storage Services**, en klik vervolgens op **schijven**.
2. In het Hallo inhoudsdeelvenster Hallo **schijven** groep, klikt u op **schijf 2** (Hello **partitie** instellen te**onbekende**).
3. Klik op **taken**, en klik vervolgens op **NieuwVolume**.
4. Hallo voordat u een pagina van Wizard Nieuw Volume hello, klik op **volgende**.
5. Klik op Hallo Selecteer Hallo-server en schijfpagina op **schijf 2**, en klik vervolgens op **volgende**. Wanneer u wordt gevraagd, klikt u op **OK**.
6. Klik op Hallo Hallo grootte opgeven van Hallo volume pagina, **volgende**.
7. Klik op Hallo toewijzen tooa station stationsletter of map pagina op **volgende**.
8. Klik op Hallo bestand selecteren pagina systeeminstellingen, **volgende**.
9. Klik op de pagina van het Hallo bevestigen selecties **maken**.
10. Wanneer voltooid, klikt u op **sluiten**.

Deze opdrachten uitvoeren op Hallo Windows PowerShell-opdrachtprompt op SQL1:

    md f:\Data
    md f:\Log
    md f:\Backup

Voeg vervolgens SQL1 toohello CORP Windows Server Active Directory-domein met de volgende opdrachten bij de Windows PowerShell-prompt Hallo op SQL1.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Gebruik Hallo corp\gebruiker1 account wanneer u wordt gevraagd de domeinaccountreferenties toosupply voor Hallo **Add-Computer** opdracht.

Start opnieuw op en gebruik hello Azure portal tooconnect tooSQL1 *met lokale administrator-account van SQL1 hello*.

Configureer vervolgens SQL Server 2014 toouse Hallo F: station voor nieuwe databases en machtigingen van gebruikersaccount.

1. Typ vanuit het startscherm Hallo **SQL Server Management**, en klik vervolgens op **SQL Server 2014 Management Studio**.
2. In **verbinding tooServer**, klikt u op **Connect**.
3. In het structuurvenster van de Hallo Object Explorer met de rechtermuisknop **SQL1**, en klik vervolgens op **eigenschappen**.
4. In Hallo **servereigenschappen** venster, klikt u op **Database-instellingen**.
5. Zoek Hallo **Database standaardlocaties** en deze waarden instellen: 
   * Voor **gegevens**, tekst hello pad **f:\Data**.
   * Voor **logboek**, tekst hello pad **f:\Log**.
   * Voor **back-up**, tekst hello pad **f:\Backup**.
   * Opmerking: Alleen nieuwe databases gebruiken deze locaties.
6. Klik op Hallo **OK** tooclose Hallo venster.
7. In Hallo **Objectverkenner** structuurvenster van de open **beveiliging**.
8. Met de rechtermuisknop op **aanmeldingen** en klik vervolgens op **New Login**.
9. In **aanmeldingsnaam**, type **corp\gebruiker1**.
10. Op Hallo **serverfuncties** pagina, klikt u op **sysadmin**, en klik vervolgens op **OK**.
11. Sluit Microsoft SQL Server Management Studio.

Dit is de huidige configuratie.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>Fase 3: Hallo LOB-server (LOB1) configureren
Maak eerst een virtuele machine voor LOB1 met de volgende opdrachten bij hello Azure PowerShell-opdrachtprompt op de lokale computer.

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

Gebruik vervolgens hello Azure portal tooconnect tooLOB1 met referenties van de lokale beheerdersaccount Hallo van LOB1 Hallo.

Configureer vervolgens een Windows Firewall tooallow verkeer van de regel voor het testen van verbinding. Voer deze opdrachten uit vanaf een beheerdersniveau Windows PowerShell-opdrachtprompt op LOB1.

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

Hallo ping-opdracht moet resulteren in vier geslaagde antwoorden van IP-adres 192.168.0.4.

Voeg vervolgens LOB1 toohello CORP Active Directory-domein met de volgende opdrachten bij Hallo Windows PowerShell-prompt.

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

Gebruik Hallo corp\gebruiker1 account wanneer u wordt gevraagd de domeinaccountreferenties toosupply voor Hallo **Add-Computer** opdracht.

Start opnieuw op en hello Azure portal tooconnect tooLOB1 met Hallo corp\gebruiker1-account en wachtwoord te gebruiken.

Vervolgens LOB1 voor IIS configureren en testen van de toegang van CLIENT1.

1. Klik in Serverbeheer **functies en onderdelen toevoegen**.
2. Op Hallo **voordat u begint met** pagina, klikt u op **volgende**.
3. Op Hallo **installatietype selecteren** pagina, klikt u op **volgende**.
4. Op Hallo **Select doelserver** pagina, klikt u op **volgende**.
5. Op Hallo **serverfuncties** pagina, klikt u op **webserver (IIS)** in de lijst met Hallo **rollen**.
6. Wanneer u wordt gevraagd, klikt u op **onderdelen toevoegen**, en klik vervolgens op **volgende**.
7. Op Hallo **functies selecteren** pagina, klikt u op **volgende**.
8. Op Hallo **webserver (IIS)** pagina, klikt u op **volgende**.
9. Op Hallo **Functieservices selecteren** pagina selecteren of schakel de selectievakjes Hallo voor Hallo-services die u nodig hebt voor het testen van uw LOB-toepassing en klik vervolgens op **volgende**.
10. Op Hallo **installatieselecties bevestigen** pagina, klikt u op **installeren**.
11. Wacht totdat het Hallo-installatie van onderdelen is voltooid en klik vervolgens op **sluiten**.
12. Toohello CLIENT1-computer verbinding met de referenties van de account corp\gebruiker1 Hallo vanaf hello Azure-portal, en start Internet Explorer.
13. Typ in de adresbalk Hallo **http://lob1/** en druk op ENTER. U ziet Hallo IIS 8 standaardwebpagina.

Dit is de huidige configuratie.

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

Deze omgeving is nu klaar voor toodeploy u uw webtoepassing op LOB1 en test functionaliteit van CLIENT1 op Hallo Corpnet-subnet.

## <a name="next-step"></a>Volgende stap
* Voeg een nieuwe virtuele machine met behulp van Hallo [Azure-portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


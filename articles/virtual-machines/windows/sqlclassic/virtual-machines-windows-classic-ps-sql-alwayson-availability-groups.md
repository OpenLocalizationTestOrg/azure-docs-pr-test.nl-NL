---
title: aaaConfigure hello AlwaysOn-beschikbaarheidsgroep op een virtuele machine in Azure met behulp van PowerShell | Microsoft Docs
description: Deze zelfstudie maakt gebruik van bronnen die zijn gemaakt met het klassieke implementatiemodel Hallo. U kunt PowerShell toocreate een AlwaysOn-beschikbaarheidsgroep gebruikt in Azure.
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>Hallo-AlwaysOn-beschikbaarheidsgroep configureren op een virtuele machine in Azure met PowerShell
> [!div class="op_single_selector"]
> * [Klassieke: UI](../classic/portal-sql-alwayson-availability-groups.md)
> * [Klassieke: PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

Voordat u begint, kunt u overwegen of u kunt deze taak in Azure resource manager-model voltooien. U wordt aangeraden Azure resource manager-model voor nieuwe implementaties. Zie [op virtuele machines in Azure SQL Server altijd op beschikbaarheidsgroepen](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md).

> [!IMPORTANT]
> U wordt aangeraden de meeste nieuwe implementaties Hallo Resource Manager-model gebruiken. Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.

Azure virtuele machines (VM's) kunt database beheerders toolower Hallo kosten van een SQL Server-systeem voor hoge beschikbaarheid. Deze zelfstudie leert u hoe tooimplement een beschikbaarheid van groep met behulp van SQL Server Always On end-to-end binnen een Azure-omgeving. Uw oplossing SQL Server Always On in Azure wordt aan het einde van de Hallo Hallo zelfstudie bestaan uit Hallo volgende elementen:

* Een virtueel netwerk met meerdere subnetten, met inbegrip van een front-end- en een back-end-subnet.
* Een domeincontroller met een Active Directory-domein.
* Twee SQL Server-VM's die geïmplementeerd toohello back-end-subnet en gekoppelde toohello Active Directory-domein zijn.
* Drie knooppunten Windows failovercluster met Hallo Knooppuntmeerderheid quorummodel.
* Een beschikbaarheidsgroep met twee replica's voor synchrone doorvoer van een beschikbaarheidsdatabase.

Dit scenario is een goede keuze voor de eenvoud op Azure, niet voor de kosteneffectiviteit of andere factoren. Bijvoorbeeld, kunt u met behulp van de domeincontroller Hallo als Hallo bestandssharewitness van quorum in een failovercluster met twee knooppunten Hallo aantal virtuele machines voor een groep twee replica beschikbaarheid toosave minimaliseren op rekenuren in Azure. Deze methode wordt Hallo-aantal VM's met één van Hallo hierboven configuratie verlaagd.

Deze zelfstudie is bedoeld tooshow u stappen die vereist tooset up Hallo zijn Hallo oplossing hierboven beschreven zonder bespreekt Hallo details van elke stap. Daarom stap in plaats van mits Hallo GUI-configuratiestappen, deze PowerShell-scripts tootake gebruikt u snel tot en met elke. Deze zelfstudie wordt ervan uitgegaan dat de volgende Hallo:

* U hebt al een Azure-account met Hallo virtuele machine abonnement.
* U hebt geïnstalleerd Hallo [Azure PowerShell-cmdlets](/powershell/azure/overview).
* U hebt al een goed begrip van AlwaysOn-beschikbaarheidsgroepen voor oplossingen on-premises. Zie voor meer informatie [altijd op beschikbaarheidsgroepen (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx).

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>Verbinding maken met tooyour Azure-abonnement en Hallo virtueel netwerk maken
1. In een PowerShell-venster op de lokale computer hello Azure-module importeren, Hallo publiceren instellingen bestand tooyour machine downloaden en verbinding maken met de PowerShell-sessie tooyour Azure-abonnement via Hallo gedownload publicatie-instellingen te importeren.

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    Hallo **Get-AzurePublishSettingsFile** opdracht genereert u een beheercertificaat met Azure automatisch en downloadt u tooyour machine. Een browser wordt automatisch geopend en u bent na vragen aan gebruiker tooenter Hallo Microsoft-accountreferenties voor uw Azure-abonnement. Hallo gedownload **.publishsettings** bestand bevat alle Hallo gegevens die u nodig toomanage uw Azure-abonnement. Na het opslaan van deze lokale map tooa importeren met Hallo **importeren AzurePublishSettingsFile** opdracht.

   > [!NOTE]
   > Hallo .publishsettings-bestand bevat uw referenties (ongecodeerde) die gebruikt tooadminister zijn uw Azure-abonnementen en services. Hallo aanbevolen beveiligingsprocedure voor dit bestand is toostore deze tijdelijk buiten uw adreslijsten bron (bijvoorbeeld in Hallo Libraries\Documents map), en vervolgens verwijdert nadat Hallo importeren is voltooid. Een kwaadwillende gebruiker die u toegang tot toohello .publishsettings-bestand krijgt kunt bewerken, maken en verwijderen van uw Azure-services.

2. Definieer een reeks variabelen die u toocreate uw cloud IT-infrastructuur gebruiken wilt.

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    Betalen aandacht toohello tooensure die uw opdrachten later slaagt te volgen:

   * Variabelen **$storageAccountName** en **$dcServiceName** moeten uniek zijn omdat ze gebruikt tooidentify uw cloud-opslagaccount en cloud-server, respectievelijk op Hallo Internet.
   * Hallo namen die u voor variabelen opgeeft **$affinityGroupName** en **$virtualNetworkName** zijn geconfigureerd in het configuratiebestand voor Hallo virtueel netwerk die u later gaat gebruiken.
   * **$sqlImageName** geeft de naam bijgewerkt Hallo van Hallo VM-installatiekopie waarin SQL Server 2012 Service Pack 1 Enterprise Edition.
   * Ter vereenvoudiging **Contoso! 000** is Hallo hetzelfde wachtwoord dat wordt gebruikt in de hele zelfstudie Hallo.

3. Maak een affiniteitsgroep.

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. Een virtueel netwerk maken door een configuratiebestand te importeren.

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    Hallo-configuratiebestand bevat Hallo XML-document te volgen. Kort samengevat: Hiermee wordt een virtueel netwerk met de naam **ContosoNET** in Hallo affiniteitsgroep aangeroepen **ContosoAG**. Het Hallo-adresruimte is **10.10.0.0/16** en heeft twee subnetten **10.10.1.0/24** en **10.10.2.0/24**, die zijn Hallo front-subnet en back-subnet, respectievelijk. Hallo front-subnet is waarin u de clienttoepassingen, zoals Microsoft SharePoint kunt plaatsen. Hallo back-subnet is plaats voegt u Hallo SQL Server-VM's. Als u Hallo wijzigt **$affinityGroupName** en **$virtualNetworkName** variabelen eerder, moet u ook wijzigen Hallo namen onderstaande overeenkomt.

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. Maak een opslagaccount die is gekoppeld aan een affiniteitsgroep Hallo gemaakt en stel dit in als de huidige opslagaccount Hallo in uw abonnement.

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. Hallo domeincontrollerserver maken in Hallo nieuwe cloud service- en beschikbaarheid.

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    Deze opdrachten piped Hallo volgende dingen:

   * **Nieuwe AzureVMConfig** maakt u een VM-configuratie.
   * **Voeg AzureProvisioningConfig** biedt Hallo parameters voor de configuratie van een zelfstandige Windows-server.
   * **Voeg AzureDataDisk** Hallo gegevensschijf die u gebruiken gaat voor het opslaan van Active Directory-gegevens met caching optie set tooNone hello wordt toegevoegd.
   * **Nieuwe AzureVM** maakt een nieuwe cloudservice en maakt u nieuwe virtuele machine van Azure in een nieuwe cloudservice Hallo Hallo.

7. Wachten op Hallo nieuwe VM toobe volledig is ingericht en Hallo extern bureaublad bestand tooyour-werkmap downloaden. Omdat hello nieuwe virtuele machine in Azure een tooprovision lang, Hallo `while` lus blijft toopoll Hallo van nieuwe virtuele machine totdat deze klaar voor gebruik.

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

Hallo domain controller-server is nu is ingericht. Vervolgens configureert u Hallo Active Directory-domein op deze domeincontrollerserver. Laat Hallo PowerShell-venster geopend op uw lokale computer. U gaat deze gebruiken opnieuw hoger toocreate Hallo twee SQL Server-VM's.

## <a name="configure-hello-domain-controller"></a>Hallo-domeincontroller configureren
1. Verbinding maken met toohello domeincontrollerserver beschadigt door Hallo extern bureaublad-bestand. Gebruik de gebruikersnaam AzureAdmin en het wachtwoord van beheerder Hallo-machine **Contoso! 000**, die u hebt opgegeven tijdens het maken van Hallo van nieuwe virtuele machine.
2. Open een PowerShell-venster in de beheerdersmodus.
3. Voer de volgende Hallo **DCPROMO. EXE** opdracht tooset up Hallo **corp.contoso.com** domein met de gegevensmappen Hallo op station M.

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Nadat het Hallo-opdracht is voltooid, wordt Hallo VM automatisch opnieuw opgestart.

4. Verbinding maken toohello domeincontrollerserver opnieuw beschadigt door Hallo extern bureaublad-bestand. Deze tijd, meld u aan als **CORP\Administrator**.
5. Open een PowerShell-venster in de beheerdersmodus en Hallo Active Directory PowerShell-module importeren met behulp van Hallo volgende opdracht:

        Import-Module ActiveDirectory

6. Voer Hallo opdrachten tooadd drie gebruikers toohello domein te volgen.

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install** gebruikte tooconfigure is alles verwante toohello SQL Server-service-exemplaren, Hallo failover-cluster en Hallo-beschikbaarheidsgroep. **CORP\SQLSvc1** en **CORP\SQLSvc2** worden gebruikt als Hallo SQL Server-serviceaccounts voor Hallo twee SQL Server-VM's.
7. Hallo volgende, voert deze opdrachten toogive **CORP\Install** Hallo machtigingen toocreate computerobjecten in Hallo-domein.

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    Hallo hierboven opgegeven GUID is Hallo GUID voor objecttype Hallo-computer. Hallo **CORP\Install** account moet Hallo **alle eigenschappen lezen** en **Computerobjecten maken** machtiging toocreate Hallo Active Direct objecten voor Hallo failover cluster. Hallo **alle eigenschappen lezen** machtiging is al toegewezen tooCORP\Install standaard, dus u toogrant hoeft het expliciet. Zie voor meer informatie over de machtigingen die zijn vereist toocreate Hallo failover-cluster, [stapsgewijze handleiding voor Failover-Cluster: Accounts configureren in Active Directory](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx).

    Nu dat u klaar bent met het configureren van Active Directory en gebruikersobjecten hello, hebt u twee SQL Server-virtuele machines maken en toothis domein kan toevoegen.

## <a name="create-hello-sql-server-vms"></a>Hallo SQL Server-VM's maken
1. Blijven toouse Hallo PowerShell-venster is geopend op uw lokale computer. Definieer Hallo aanvullende variabelen te volgen:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    IP-adres Hallo **10.10.0.4** is doorgaans toegewezen toohello eerste VM die u in Hallo maakt **10.10.0.0/16** subnet van uw virtuele Azure-netwerk. U moet controleren of het Hallo-adres van de domain controller-server door het uitvoeren van **IPCONFIG**.
2. Voer Hallo doorgesluisd opdrachten toocreate Hallo eerst na VM in het Hallo-failovercluster, met de naam **ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    Let op Hallo volgende met betrekking tot de bovenstaande Hallo-opdracht:

   * **Nieuwe AzureVMConfig** maakt u een VM-configuratie met de naam van de gewenste beschikbaarheidsset Hallo. Hallo latere virtuele machines wordt gemaakt met Hallo dezelfde beschikbaarheidsset zodat ze bent gekoppeld toohello dezelfde beschikbaarheidsset.
   * **Voeg AzureProvisioningConfig** joins Hallo VM toohello Active Directory-domein dat u hebt gemaakt.
   * **Set-AzureSubnet** plaatsen Hallo VM in Hallo back-subnet.
   * **Nieuwe AzureVM** maakt een nieuwe cloudservice en maakt u nieuwe virtuele machine van Azure in een nieuwe cloudservice Hallo Hallo. Hallo **DnsSettings** parameter die Hallo DNS-server geeft u voor het Hallo-servers in een nieuwe cloudservice Hallo Hallo IP-adres **10.10.0.4**. Dit is Hallo IP-adres van Hallo domeincontrollerserver. Deze parameter is vereist tooenable Hallo nieuwe virtuele machines in Hallo cloud service toojoin toohello Active Directory-domein is. Deze parameter niet opgeeft, moet u handmatig instellen Hallo IPv4-instellingen in uw VM toouse Hallo domain controller-server als het primaire DNS-server Hallo nadat Hallo VM is ingericht en meldt u zich Hallo VM toohello Active Directory-domein.
3. Voer Hallo na doorgesluisd opdrachten toocreate Hallo SQL Server-VM's met de naam **ContosoSQL1** en **ContosoSQL2**.

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    Let op Hallo volgende met betrekking tot de bovenstaande Hallo-opdrachten:

   * **Nieuwe AzureVMConfig** gebruikt dezelfde naam van de beschikbaarheidsset als domeincontrollerserver Hallo Hallo en maakt gebruik van SQL Server 2012 Service Pack 1 Enterprise Edition-installatiekopie in de galerie met virtuele machines Hallo Hallo. Hallo operationele systeem tooread-schijfcache alleen (geen schrijfcache) wordt ook ingesteld. U wordt aangeraden Hallo database bestanden tooa afzonderlijke gegevensschijf u koppelen toohello VM, en deze configureren met niet lezen of schrijfcache te migreren. De volgende beste Hallo is echter tooremove schrijfcache op Hallo besturingssysteemschijf omdat u niet verwijderen lezen cachegebruik op schijf Hallo-besturingssysteem.
   * **Voeg AzureProvisioningConfig** joins Hallo VM toohello Active Directory-domein dat u hebt gemaakt.
   * **Set-AzureSubnet** plaatsen Hallo VM in Hallo back-subnet.
   * **Voeg AzureEndpoint** toegang eindpunten toegevoegd zodat clienttoepassingen toegang deze services-exemplaren van SQL Server op Hallo Internet tot. Er zijn verschillende poorten opgegeven tooContosoSQL1 en ContosoSQL2.
   * **Nieuwe AzureVM** maakt nieuwe SQL Server VM Hallo in Hallo dezelfde cloudservice als ContosoQuorum. U moet Hallo VMs plaatsen in dezelfde cloudservice als u deze wilt toobe in Hallo Hallo dezelfde beschikbaarheidsset.
4. Wacht voor elke VM toobe volledig is ingericht en voor elke VM toodownload werkmap tooyour extern bureaublad-bestand. Hallo `for` lus Hallo doorlopen met drie nieuwe virtuele machines en voert Hallo-opdrachten binnen het hoogste niveau accolades Hallo voor elk van deze.

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    Hallo SQL Server-VM's nu zijn ingericht en wordt uitgevoerd, maar ze zijn geïnstalleerd met SQL Server met de standaardopties.

## <a name="initialize-hello-failover-cluster-vms"></a>Hallo failover-cluster virtuele machines te initialiseren
In deze sectie moet u toomodify Hallo drie servers die u in Hallo failover-cluster en Hallo SQL Server-installatie gebruiken gaat. Specifiek:

* Alle servers: U moet tooinstall hello **Failoverclustering** functie.
* Alle servers: U moet tooadd **CORP\Install** als Hallo machine **beheerder**.
* ContosoSQL1 en alleen ContosoSQL2: U moet tooadd **CORP\Install** als een **sysadmin** rol in de standaarddatabase Hallo.
* ContosoSQL1 en alleen ContosoSQL2: U moet tooadd **NT AUTHORITY\System** als iemand zich aanmeldt met Hallo volgende machtigingen:

  * Wijzigen van een beschikbaarheidsgroep
  * Verbinding maken met SQL
  * Status van de server weergeven
* ContosoSQL1 en ContosoSQL2 alleen: Hallo **TCP** protocol is al ingeschakeld op Hallo van SQL Server-VM. U moet echter nog steeds tooopen Hallo firewall voor externe toegang van SQL Server.

U bent nu klaar toostart. Beginnen met **ContosoQuorum**, volgt u onderstaande Hallo stappen:

1. Verbinding te maken met**ContosoQuorum** door Hallo extern bureaublad-bestanden. Gebruik Hallo machine beheerder gebruikersnaam **AzureAdmin** en het wachtwoord **Contoso! 000**, die u hebt opgegeven tijdens het maken van virtuele machines Hallo.
2. Controleer of dat Hallo computers hebt toegevoegd te**corp.contoso.com**.
3. Wachten op Hallo SQL Server-installatie toofinish actieve Hallo automatische initialisatietaken voordat u doorgaat.
4. Open een PowerShell-venster in de beheerdersmodus.
5. Hallo Windows Failover Clustering installeren.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Voeg **CORP\Install** als een lokale beheerder.

        net localgroup administrators "CORP\Install" /Add
7. Afmelden bij ContosoQuorum. U bent nu klaar met deze server.

        logoff.exe

Vervolgens initialiseren **ContosoSQL1** en **ContosoSQL2**. Volgende stappen uit hello, die identiek voor beide VM's van SQL Server zijn.

1. Verbinding met het maken van VM's toohello twee SQL Server door Hallo extern bureaublad-bestanden. Gebruik Hallo machine beheerder gebruikersnaam **AzureAdmin** en het wachtwoord **Contoso! 000**, die u hebt opgegeven tijdens het maken van virtuele machines Hallo.
2. Controleer of dat Hallo computers hebt toegevoegd te**corp.contoso.com**.
3. Wachten op Hallo SQL Server-installatie toofinish actieve Hallo automatische initialisatietaken voordat u doorgaat.
4. Open een PowerShell-venster in de beheerdersmodus.
5. Hallo Windows Failover Clustering installeren.

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. Voeg **CORP\Install** als een lokale beheerder.

        net localgroup administrators "CORP\Install" /Add
7. Hallo PowerShell-Provider voor SQL Server worden geïmporteerd.

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. Voeg **CORP\Install** als Hallo sysadmin-rol voor Hallo standaard SQL Server-exemplaar.

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. Voeg **NT AUTHORITY\System** als iemand zich aanmeldt met Hallo drie machtigingen die hierboven worden beschreven.

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. Hallo firewall voor externe toegang van SQL Server openen.

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. Afmelden bij beide virtuele machines.

         logoff.exe

Ten slotte, bent u klaar tooconfigure Hallo-beschikbaarheidsgroep. U Hallo PowerShell-Provider voor SQL Server tooperform werkt met alle Hallo **ContosoSQL1**.

## <a name="configure-hello-availability-group"></a>Hallo-beschikbaarheidsgroep configureren
1. Verbinding te maken met**ContosoSQL1** opnieuw door het Hallo-bestanden voor extern bureaublad. In plaats van via Hallo machineaccount aanmeldt, moet u zich aanmelden via **CORP\Install**.
2. Open een PowerShell-venster in de beheerdersmodus.
3. Definieer Hallo variabelen te volgen:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. Hallo PowerShell-Provider voor SQL Server worden geïmporteerd.

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. Hallo SQL Server-serviceaccount voor ContosoSQL1 tooCORP\SQLSvc1 wijzigen.

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. Hallo SQL Server-serviceaccount voor ContosoSQL2 tooCORP\SQLSvc2 wijzigen.

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. Download **CreateAzureFailoverCluster.ps1** van [failovercluster maken voor AlwaysOn-beschikbaarheidsgroepen in Azure VM](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a) toohello lokale werkmap. U gebruikt dit script toohelp maken van een functionele failover-cluster. Netwerk voor belangrijke informatie over hoe Windows Failover Clustering met hello Azure samenwerkt, Zie [hoge beschikbaarheid en herstel na noodgevallen voor SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).
8. Wijzig tooyour werkmap en Hallo failover-cluster maken met een script Hallo gedownload.

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. Schakel AlwaysOn-beschikbaarheidsgroepen voor Hallo standaard SQL Server-exemplaren op **ContosoSQL1** en **ContosoSQL2**.

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. Maak een back-map en machtigingen voor Hallo SQL Server-serviceaccounts. U gebruikt deze beschikbaarheidsdatabase directory tooprepare Hallo op Hallo secundaire replica.

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. Een database maakt op **ContosoSQL1** aangeroepen **MyDB1**, Neem zowel een volledige back-up als een logboekback-up en herstel deze op **ContosoSQL2** Hello **WITH NORECOVERY** optie.

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Hallo beschikbaarheid groep eindpunten maken op Hallo VM's van SQL Server en de juiste machtigingen Hallo op Hallo-eindpunten.

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. Hallo beschikbaarheidsreplica's maken.

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. Maak ten slotte Hallo beschikbaarheidsgroep en join Hallo secundaire replica toohello-beschikbaarheidsgroep.

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>Volgende stappen
U hebt nu geïmplementeerd SQL Server Always On door het maken van een beschikbaarheidsgroep in Azure. Zie een listener voor deze beschikbaarheidsgroep tooconfigure [een ILB-listener voor AlwaysOn-beschikbaarheidsgroepen configureren in Azure](../classic/ps-sql-int-listener.md).

Zie voor meer informatie over het gebruik van SQL Server in Azure, [SQL Server op virtuele machines in Azure](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

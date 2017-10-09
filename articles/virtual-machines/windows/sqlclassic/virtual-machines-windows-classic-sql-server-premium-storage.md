---
title: aaaUse Azure Premium-opslag met SQL Server | Microsoft Docs
description: Dit artikel maakt gebruik van resources die zijn gemaakt met het klassieke implementatiemodel Hallo en biedt richtlijnen over het gebruik van Azure Premium-opslag met SQL Server wordt uitgevoerd op Azure Virtual Machines.
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: jhubbard
editor: monicar
tags: azure-service-management
ms.assetid: 7ccf99d7-7cce-4e3d-bbab-21b751ab0e88
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/01/2017
ms.author: jroth
ms.openlocfilehash: 393ea2020b39ea686302ae632e1049935c24af00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-premium-storage-with-sql-server-on-virtual-machines"></a>Azure Premium Storage gebruiken met SQL Server op Virtual Machines
## <a name="overview"></a>Overzicht
[Azure Premium-opslag](../../../storage/common/storage-premium-storage.md) generatie van opslag die een lage latentie hoge doorvoersnelheid IO en is Hallo. Het meest geschikt is voor belangrijke IO intensieve werkbelastingen, zoals SQL Server op IaaS [virtuele Machines](https://azure.microsoft.com/services/virtual-machines/).

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Dit artikel bevat plannen en richtlijnen voor het migreren van een virtuele Machine met SQL Server-toouse Premium-opslag. Dit omvat de Azure-infrastructuur (netwerk-, opslag) en Gast Windows VM stappen. Hallo-voorbeeld in Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) ziet u de migratie van een volledige uitgebreide end tooend van hoe toomove grotere virtuele machines tootake profiteren van betere lokale SSD-opslag met PowerShell.

Het is belangrijk toounderstand Hallo end-to-end-proces met Azure Premium-opslag met SQL Server op IAAS VM's. Dit omvat:

* Identificatie van Hallo vereisten toouse Premium-opslag.
* Voorbeelden voor het implementeren van SQL Server op IaaS tooPremium opslag voor nieuwe implementaties.
* Voorbeelden van migreren bestaande implementaties, zowel zelfstandige servers en implementaties met behulp van SQL AlwaysOn-beschikbaarheidsgroepen.
* Mogelijke migratie nadert.
* Volledige end-to-end-voorbeeld Azure, Windows en SQL Server-stappen voor migratie van een bestaande implementatie altijd op Hallo wordt weergegeven.

Zie voor meer achtergrondinformatie op SQL Server in Azure Virtual Machines, [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

**Auteur:** Daniel Sol **technische controleurs:** Luis Jeroen Vargas haring, Sanjay Mishra, Pravin Mital, Schwertl Thomas, Gonzalo Ruiz.

## <a name="prerequisites-for-premium-storage"></a>Vereisten voor de Premium-opslag
Er zijn verschillende vereisten voor het gebruik van Premium-opslag.

### <a name="machine-size"></a>Grootte van de machine
Voor het gebruik van Premium-opslag moet u toouse DS reeks virtuele Machines (VM). Als u niet DS-serie machines in uw cloudservice voordat u gebruikt hebt, moet u Hallo bestaande VM verwijderen, Hallo gekoppelde schijven houden en vervolgens een nieuwe cloudservice maken voordat de virtuele machine als de grootte van de rol DS * Hallo opnieuw te maken. Zie voor meer informatie over grootten van virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="cloud-services"></a>Cloud services
U kunt alleen virtuele machines DS * met Premium-opslag gebruiken wanneer ze worden gemaakt in een nieuwe cloudservice. Als u SQL Server Always On in Azure, verwijzen Hallo altijd-Listener voor toohello Azure interne of externe Load Balancer-IP-adres dat is gekoppeld aan een cloudservice. In dit artikel is gericht op het toomigrate behoud van beschikbaarheid in dit scenario.

> [!NOTE]
> Een reeks DS * moet de Hallo eerste virtuele machine die is geïmplementeerd toohello nieuwe Cloudservice.
>
>

### <a name="regional-vnets"></a>Regionaal vnet 's
Voor virtuele machines DS * moet u Hallo virtuele netwerk (VNET) die als host fungeert voor uw virtuele machines van regionale toobe configureren. Deze 'breder' hello VNET tooallow Hallo grotere virtuele machines toobe ingericht in andere clusters is en communicatie tussen deze twee toestaan. In Hallo schermafbeelding te volgen, weergegeven hello gemarkeerde locatie regionaal vnet's, terwijl de eerste resultaat Hallo een 'smalle' VNET toont.

![RegionalVNET][1]

U kunt een Microsoft-ondersteuning ticket toomigrate tooa verhogen regionaal VNET, Microsoft wordt een wijziging aanbrengt toocomplete Hallo migratie tooregional VNETs, wijzig Hallo eigenschap AffinityGroup in Hallo-netwerkconfiguratie. Hallo netwerkconfiguratie in PowerShell eerst te exporteren en vervolgens vervangen Hallo **AffinityGroup** eigenschap in Hallo **VirtualNetworkSite** element met een **locatie** de eigenschap. Geef `Location = XXXX` waar `XXXX` is een Azure-regio. Hallo nieuwe configuratie importeren.

Bijvoorbeeld, overweegt Hallo VNET-configuratie te volgen:

    <VirtualNetworkSite name="danAzureSQLnet" AffinityGroup="AzureSQLNetwork">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

toomove deze tooa regionaal VNET in West-Europa wijzigen Hallo configuratie toohello te volgen:

    <VirtualNetworkSite name="danAzureSQLnet" Location="West Europe">
    <AddressSpace>
      <AddressPrefix>10.0.0.0/8</AddressPrefix>
      <AddressPrefix>172.16.0.0/12</AddressPrefix>
    </AddressSpace>
    <Subnets>
    ...
    </VirtualNetworkSite>

### <a name="storage-accounts"></a>Opslagaccounts
U moet toocreate een nieuw opslagaccount die is geconfigureerd voor Premium-opslag. Houd er rekening mee dat Hallo gebruik van Premium-opslag is ingesteld op Hallo storage-account, niet op afzonderlijke VHD's, maar bij gebruik van een DS * reeks VM u de VHD van Premium en Standard-opslag-accounts koppelen kunt. U kunt dit overwegen als u niet dat tooplace Hallo OS VHD op toohello Premium Storage-account wilt.

Hallo volgende **nieuw AzureStorageAccountPowerShell** opdracht 'Premium_LRS' Hello **Type** maakt een Premium-Opslagaccount:

    $newstorageaccountname = "danpremstor"
    New-AzureStorageAccount -StorageAccountName $newstorageaccountname -Location "West Europe" -Type "Premium_LRS"   

### <a name="vhds-cache-settings"></a>Cache-instellingen voor virtuele harde schijven
Hallo belangrijkste verschil tussen het maken van schijven die deel van een Premium Storage-account uitmaken is Hallo schijfcache-instelling. Voor SQL Server-gegevens volume het schijven wordt aanbevolen dat u '**Lees-Caching**'. Voor transactie logboekvolumes, Hallo schijfcache-instelling te moet worden ingesteld '**geen**'. Dit wijkt af van Hallo aanbevelingen voor Standard-opslagaccounts.

Eenmaal Hallo VHD's zijn gekoppeld, kan Hallo cache-instelling kan niet worden gewijzigd. U moet toodetach en koppelt u Hallo VHD opnieuw met een bijgewerkte cache-instelling.

### <a name="windows-storage-spaces"></a>Windows-opslagruimten
U kunt [Windows Storage Spaces](https://technet.microsoft.com/library/hh831739.aspx) zoals u deed met vorige Standard-opslag, Hierdoor kunt u een virtuele machine die wordt al gebruikt door opslagruimten toomigrate. Hallo-voorbeeld in [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) (stap 9 en voorwaarts) laat zien Hallo Powershell code tooextract en importeren van een virtuele machine met meerdere gekoppelde VHD's.

Opslaggroepen zijn gebruikt met standaard Azure storage-account tooenhance doorvoer en de latentie te verminderen. Wellicht waarde in nieuwe implementaties het testen van opslaggroepen met Premium-opslag, maar ze extra complexiteit met setup opslag toevoegen.

#### <a name="how-toofind-which-azure-virtual-disks-map-toostorage-pools"></a>Hoe toofind welke virtuele schijven van Azure toostorage groepen toewijzen
Als er verschillende cache-instelling aanbevelingen voor het gekoppelde VHD's zijn, besluiten u toocopy Hallo VHD's tooa Premium Storage-account. Echter, wanneer u koppelt u deze opnieuw toohello nieuwe DS reeks VM, moet u mogelijk tooalter Hallo cache-instellingen. Het is eenvoudiger tooapply Hallo die Premium-opslag instellingen voor de uitvoercache aanbevolen wanneer er een aparte virtuele harde schijven Hallo SQL-gegevens bestanden en logboek-bestanden (in plaats van voor een enkele VHD met zowel).

> [!NOTE]
> Als u SQL Server-gegevens en logboekbestanden bestanden op hetzelfde volume, Hallo caching optie die u kiest, is afhankelijk van Hallo i/o-toegangspatronen voor de werkbelasting van uw database Hallo hebt. Alleen testen kunt laten zien welke cache-instelling wordt aanbevolen voor dit scenario.
>
>

Als u gebruikmaakt van Windows Storage Spaces die bestaan uit meerdere VHD's moet u toolook op uw oorspronkelijke scripts tooidentify die gekoppeld VHD's zijn echter in welke specifieke groep, dus vervolgens kunt u instellen Hallo cache-instellingen dienovereenkomstig voor elke schijf.

Als u nog geen oorspronkelijke script beschikbaar tooshow u die VHD's zijn toegewezen toohello opslaggroep, kunt u Hallo stappen toodetermine Hallo schijfopslag/groep toewijzing te volgen.

Gebruik voor elke schijf Hallo stappen te volgen:

1. Haal de lijst met schijven gekoppeld tooVM Hello **Get-AzureVM** opdracht:

    Get-AzureVM - ServiceName <servicename> -naam <vmname> | Get-AzureDataDisk
2. Houd er rekening mee Hallo Diskname en LUN.

    ![DisknameAndLUN][2]
3. Extern bureaublad in Hallo VM. Ga te**Computerbeheer** | **Apparaatbeheer** | **schijfstations**. Bekijk Hallo eigenschappen van elke Hallo 'virtuele schijven Microsoft'

    ![VirtualDiskProperties][3]
4. Hier Hallo LUN-nummer is een referentienummer toohello LUN dat die u opgeeft bij het toevoegen van Hallo VHD toohello VM.
5. Ga voor Hallo Microsoft Virtual Disk toohello **Details** tabblad en klik vervolgens in Hallo **eigenschap** weergeven, gaat u te**stuurprogrammasleutel**. In Hallo **waarde**, opmerking Hallo **Offset**, namelijk 0002 in Hallo volgende schermopname. Hallo 0002 geeft Hallo PhysicalDisk2 die Hallo storage pool verwijzingen.

    ![VirtualDiskPropertyDetails][4]
6. Voor elke opslaggroep gekoppeld dump uit Hallo schijven:

    Get-StoragePool - FriendlyName AMS1pooldata | Get-PhysicalDisk

    ![GetStoragePool][5]

Nu kunt u gekoppelde deze informatie tooassociate VHD's tooPhysical schijven in opslaggroepen.

Zodra u de VHD's tooPhysical schijven in opslaggroepen vervolgens loskoppelen en kopieert u deze via tooa Premium Storage-account hebt gekoppeld, koppelt u ze met de juiste cache Hallo instellen. Zie Hallo voorbeeld in Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage), stappen 8 tot en met 12. Deze stappen laten zien hoe tooextract een VM gekoppeld VHD schijf configuratie tooa CSV-bestand kopiëren Hallo VHD's, Hallo schijf configuratie cache-instellingen wijzigen en ten slotte Hallo VM implementeren als een DS-serie VM alle Hello gekoppelde schijven.

### <a name="vm-storage-bandwidth-and-vhd-storage-throughput"></a>VM-opslag bandbreedte en opslagdoorvoer VHD
Hallo bedrag van de prestaties van de opslag, is afhankelijk van Hallo DS * VM-grootte opgegeven en Hallo grootten van de VHD. Hallo virtuele machines hebben verschillende rechten voor het aantal virtuele harde schijven die kunnen worden bijgevoegd en maximale bandbreedte wordt ondersteund (MB/s) Hallo Hallo. Zie voor Hallo specifieke bandbreedte cijfers [virtuele Machine en Cloud Service Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Verbeterde IOPS worden verkregen met grotere schijf. Dit moet u overwegen wanneer u over het migratiepad voor de nadenkt. Voor meer informatie [Zie Hallo tabel voor IOPS en schijftypen](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets).

Overweeg tot slot dat virtuele machines hebben verschillende maximale schijf-bandbreedten die wordt ondersteund voor alle schijven die zijn gekoppeld. U kunt Hallo maximale schijf-bandbreedte die beschikbaar is voor de grootte van die VM-rol kan verzadigen onder hoge belasting. Bijvoorbeeld wordt een Standard_DS14 ondersteuning voor maximaal too512MB/s; Daarom kan u Hallo schijf bandbreedte van Hallo VM verzadigen met drie P30 schijven. Maar in dit voorbeeld kan Hallo doorvoer limiet wordt overschreden, afhankelijk van Hallo combinatie van lees- en IOs.

## <a name="new-deployments"></a>Nieuwe implementaties
de volgende twee secties Hallo laten zien hoe u SQL Server-VM's tooPremium opslag kunt implementeren. Zoals al eerder vermeld, hoeft niet per se u tooplace hello besturingssysteemschijf naar Premium-opslag. U kunt toodo dit als u tooplace een intensieve i/o-werkbelastingen op Hallo OS VHD wilde weet.

Hallo eerste voorbeeld laat zien met behulp van de bestaande Azure-galerie met installatiekopieën. Hallo tweede voorbeeld laat zien hoe toouse een aangepaste VM-installatiekopie is die u in een bestaand standaard opslagaccount hebt.

> [!NOTE]
> Deze voorbeelden wordt ervan uitgegaan dat u al een regionaal VNET hebt gemaakt.
>
>

### <a name="create-a-new-vm-with-premium-storage-with-gallery-image"></a>Maak een nieuwe virtuele machine met Premium-opslag met afbeelding
Hallo voorbeeld hieronder ziet u hoe tooplace Hallo OS VHD naar premium-opslag en Premium-opslag-VHD's koppelen. U kunt echter ook Hallo besturingssysteemschijf plaatsen in een Standard-opslagaccount en koppel vervolgens de VHD's die zich in een Premium-opslagaccount bevinden. Beide scenario's worden uitgelegd.

    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Set up subscription
    Set-AzureSubscription -SubscriptionName $mysubscription
    Select-AzureSubscription -SubscriptionName $mysubscription -Current  

#### <a name="step-1-create-a-premium-storage-account"></a>Stap 1: Een Premium Storage-Account maken
    #Create Premium Storage account, note Type
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  


#### <a name="step-2-create-a-new-cloud-service"></a>Stap 2: Maak een nieuwe Cloudservice
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-reserve-a-cloud-service-vip-optional"></a>Stap 3: Gereserveerd VIP van de Cloud-Service (optioneel)
    #check exisitng reserved VIP
    Get-AzureReservedIP

    $reservedVIPName = “sqlcloudVIP”
    New-AzureReservedIP –ReservedIPName $reservedVIPName –Label $reservedVIPName –Location $location

#### <a name="step-4-create-a-vm-container"></a>Stap 4: Een VM-Container maken
    #Generate storage keys for later
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    ##Generate storage acc contexts
    $xioContext = New-AzureStorageContext –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary   

    #Create container
    $containerName = 'vhds'
    New-AzureStorageContainer -Name $containerName -Context $xioContext

#### <a name="step-5-placing-os-vhd-on-standard-or-premium-storage"></a>Stap 5: Brengen OS VHD Standard of Premium-opslag
    #NOTE: Set up subscription and default storage account which will be used tooplace hello OS VHD in

    #If you want tooplace hello OS VHD Premium Storage Account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $newxiostorageaccountname  

    #If you wanted tooplace hello OS VHD Standard Storage Account but attach Premium Storage VHDs then you would run this instead:
    $standardstorageaccountname = "danstdams"

    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount  $standardstorageaccountname

#### <a name="step-6-create-vm"></a>Stap 6: Een virtuele machine maken
    #Get list of available SQL Server Images from hello Azure Image Gallery.
    $galleryImage = Get-AzureVMImage | where-object {$_.ImageName -like "*SQL*2014*Enterprise*"}
    $image = $galleryImage.ImageName

    #Set up Machine Specific Information
    $vmName = "dsDan1"
    $vnet = "dansvnetwesteur"
    $subnet = "SQL"
    $ipaddr = "192.168.0.8"

    #Remember toochange tooDS series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "mycomplexpwd4*"

    #Create VM Config
    $vmConfigsl = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $image  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Add Data and Log Disks tooVM Config
    #Note hello size specified ‘-DiskSizeInGB 1023’, this will attach 2 x P30 Premium Storage Disk Type
    #Utilising hello Premium Storage enabled Storage account

    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-data1.vhd"
    $vmConfigsl | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "logDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-log1.vhd"

    #Create VM
    $vmConfigsl  | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)  

    #Add RDP Endpoint
    $EndpointNameRDPInt = "3389"
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Add-AzureEndpoint -Name "EndpointNameRDP" -Protocol "TCP" -PublicPort "53385" -LocalPort $EndpointNameRDPInt  | Update-AzureVM

    #Check VHD storage account, these should be in $newxiostorageaccountname
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName | Get-AzureDataDisk
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmName |Get-AzureOSDisk


### <a name="create-a-new-vm-toouse-premium-storage-with-a-custom-image"></a>Een nieuwe VM-toouse Premium-opslag met een aangepaste installatiekopie maken
Dit scenario laat zien waar u de bestaande aangepaste installatiekopieën die zich in een Standard-opslag-account bevinden hebt. Zoals vermeld als u wilt dat tooplace Hallo OS VHD op Premium-opslag moet u toocopy Hallo installatiekopie of aanwezig is op Hallo Standard-opslagaccount en dragen deze tooa Premium-opslag voordat deze kan worden gebruikt. Als u een installatiekopie van een lokale, kunt u ook deze toocopy methode gebruiken die rechtstreeks toohello Premium Storage-account.

#### <a name="step-1-create-storage-account"></a>Stap 1: De Storage-Account maken
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Standard Storage account
    $origstorageaccountname = "danstdams"

#### <a name="step-2-create-cloud-service"></a>Stap 2-Cloudservice maken
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location


#### <a name="step-3-use-existing-image"></a>Stap 3: Een bestaande installatiekopie gebruiken
U kunt een bestaande installatiekopie gebruiken. U kunt [nemen van een installatiekopie van een bestaande machine](../classic/capture-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json). Opmerking Hallo machine die u een installatiekopie heeft geen toobe DS * machine. Zodra u de installatiekopie van het Hallo hebt, Hallo volgen stappen tonen hoe toocopy het toohello Premium Storage-account met Hallo **Start AzureStorageBlobCopy** PowerShell-cmdlet.

    #Get storage account keys:
    #Standard Storage account
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    #Premium Storage account
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Set up contexts for hello storage accounts:
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $destContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

#### <a name="step-4-copy-blob-between-storage-accounts"></a>Stap 4: Kopieer Blob tussen Opslagaccounts
    #Get Image VHD
    $myImageVHD = "dansoldonorsql2k14-os-2015-04-15.vhd"
    $containerName = 'vhds'

    #Copy Blob between accounts
    $blob = Start-AzureStorageBlobCopy -SrcBlob $myImageVHD -SrcContainer $containerName `
    -DestContainer vhds -Destblob "prem-$myImageVHD" `
    -Context $origContext -DestContext $destContext  

#### <a name="step-5-regularly-check-copy-status"></a>Stap 5: Controleer regelmatig de status van het exemplaar:
    $blob | Get-AzureStorageBlobCopyState

#### <a name="step-6-add-image-disk-tooazure-disk-repository-in-subscription"></a>Stap 6: Installatiekopie tooAzure schijf opslagplaats in abonnement toevoegen
    $imageMediaLocation = $destContext.BlobEndPoint+"/"+$myImageVHD
    $newimageName = "prem"+"dansoldonorsql2k14"

    Add-AzureVMImage -ImageName $newimageName -MediaLocation $imageMediaLocation

> [!NOTE]
> Kan het gebeuren dat hoewel Hallo als geslaagd statusrapporten u kan nog steeds een schijffout lease. In dit geval wacht tien minuten.
>
>

#### <a name="step-7--build-hello-vm"></a>Stap 7: Hallo VM maken
U maakt hier Hallo VM van uw installatiekopie en twee Premium-opslag-VHD's koppelen:

    $newimageName = "prem"+"dansoldonorsql2k14"
    #Set up Machine Specific Information
    $vmName = "dansolchild"
    $vnet = "westeur"
    $subnet = "Clients"
    $ipaddr = "192.168.0.41"

    #This will need toobe a new cloud service
    $destcloudsvc = "danregsvcamsxio2"

    #Use tooDS Series VM
    $newInstanceSize = "Standard_DS1"

    #create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS3"

    #Machine User Credentials
    $userName = "myadmin"
    $pass = "theM)stC0mplexP@ssw0rd!”


    #Create VM Config
    $vmConfigsl2 = New-AzureVMConfig -Name $vmName -InstanceSize $newInstanceSize -ImageName $newimageName  -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` -AdminUserName $userName -Password $pass | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 0 -HostCaching "ReadOnly"  -DiskLabel "DataDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-Datadisk-1.vhd"
    $vmConfigsl2 | Add-AzureDataDisk -CreateNew -DiskSizeInGB 1023 -LUN 1 -HostCaching "None"  -DiskLabel "LogDisk1" -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vmName-logdisk-1.vhd"



    $vmConfigsl2 | New-AzureVM –ServiceName $destcloudsvc -VNetName $vnet

## <a name="existing-deployments-that-do-not-use-always-on-availability-groups"></a>Bestaande implementaties die altijd op beschikbaarheidsgroepen niet wordt gebruikt
> [!NOTE]
> Voor bestaande implementaties raadpleegt u eerst Hallo [vereisten](#prerequisites-for-premium-storage) sectie van dit onderwerp.
>
>

Er zijn verschillende overwegingen voor implementaties van SQL Server die niet altijd op beschikbaarheidsgroepen en programma's die u wilt gebruiken. Als u altijd op niet gebruikt en een bestaande zelfstandige SQL Server hebt, kunt u tooPremium opslag upgraden met behulp van een nieuw cloud service- en storage-account. Houd rekening met Hallo volgende opties:

* **Maak een nieuwe SQL Server VM**. U kunt een nieuwe versie van SQL Server VM die gebruikmaakt van een Premium-opslagaccount maken, zoals beschreven in nieuwe implementaties. Vervolgens back-up en herstel van SQL Server-configuratie- en databases. Hallo toepassing moet toobe bijgewerkt tooreference Hallo nieuwe SQL-Server als intern of extern wordt geopend. U moet toocopy alle objecten voor buiten-db' als u een gelijktijdige (SxS) SQL Server-migratie deed. Dit omvat objecten, zoals aanmeldingen, certificaten en gekoppelde servers.
* **Migreren van een bestaande SQL Server VM**. Hiervoor moet Hallo virtuele machine van SQL Server offline moet worden gezet en vervolgens overdragen tooa nieuwe cloudservice, waaronder kopiëren alle van de gekoppelde VHD's toohello Premium Storage-account. Wanneer Hallo VM online wordt gezet, wordt de toepassing hello verwijzen naar Hallo hostnaam als voordat. Let erop dat Hallo grootte van de bestaande schijf Hallo invloed is op Hallo prestatiekenmerken. Een schijf 400 GB opgehaald bijvoorbeeld tooa P20 afgerond. Als u weet dat u niet nodig hebt die schijfprestaties kan u Hallo virtuele machine als een reeks DS VM opnieuw te maken en koppelen van Premium Storage VHD's van Hallo grootte/prestaties specificatie die u nodig hebt. Vervolgens kan u loskoppelen en weer koppelt Hallo SQL DB-bestanden.

> [!NOTE]
> Wanneer welk type opslagschijf Premium kopiëren Hallo VHD schijven u rekening moet houden met een grootte van hello, afhankelijk van de grootte Hallo betekent dat ze vallen, dit schijf prestaties specificatie bepaalt. Azure worden afgerond up toohello dichtstbijzijnde schijf grootte, dus als er een schijf van 400 GB, dit wordt afgerond tooa P20. Afhankelijk van uw bestaande i/o-vereisten Hallo OS VHD moet u mogelijk niet toomigrate deze tooa Premium Storage-account.
>
>

Als uw SQL-Server extern wordt geopend, klikt u vervolgens Hallo cloud service VIP gewijzigd. U hebt tevens tooupdate eindpunten, ACL's en DNS-instellingen.

## <a name="existing-deployments-that-use-always-on-availability-groups"></a>Bestaande implementaties die gebruikmaken van altijd op beschikbaarheidsgroepen
> [!NOTE]
> Voor bestaande implementaties raadpleegt u eerst Hallo [vereisten](#prerequisites-for-premium-storage) sectie van dit onderwerp.
>
>

In eerste instantie in dit gedeelte kijken we altijd op de interactie met Azure-netwerken. Er wordt vervolgens migraties in scenario's tootwo opsplitsen: waar u enige uitvaltijd kan verdragen migraties en migraties waar u de minimale downtime moet bereiken.

Lokale SQL Server AlwaysOn-beschikbaarheidsgroepen gebruiken een Listener op lokale waarmee een virtuele DNS-naam samen met een IP-adres dat wordt gedeeld tussen een of meer SQL-Servers geregistreerd. Wanneer clients verbinding maken, worden ze via Hallo listener IP-toohello primaire SQL-Server gerouteerd. Dit is Hallo-server die eigenaar is van Hallo altijd op IP-resource op dat moment.

![DeploymentsUseAlways op][6]

U kunt slechts één IP-adres toegewezen tooa NIC op Hallo VM, daarom in volgorde van tooachieve Hallo dezelfde laag van abstractie als lokale, Hallo IP-adres dat is toegewezen toohello interne of externe Load Balancers (ILB/ELB) maakt gebruik van Azure hebben in Microsoft Azure. Hallo IP-resource die wordt gedeeld tussen servers Hallo toohello is ingesteld dezelfde IP als Hallo ILB-/ ELB. Dit is gepubliceerd in Hallo DNS en clientverkeer Hallo ILB-/ ELB toohello primaire SQL Server-replica is doorgegeven. Hallo ILB-/ ELB kent die SQL Server is de primaire omdat hierbij tests tooprobe Hallo altijd op IP-resource. In het vorige voorbeeld hello, deze tests op elk knooppunt dat een waarnaar wordt verwezen door Hallo ELB/ILB eindpunt, afhankelijk van wat reageert is Hallo primaire SQL-Server.

> [!NOTE]
> Hallo ILB en ELB zijn beide toegewezen tooa bepaald Azure-cloudservice, daarom cloudmigratie in Azure waarschijnlijk betekent dat dat Hallo die Load Balancer IP wordt gewijzigd.
>
>

### <a name="migrating-always-on-deployments-that-can-allow-some-downtime"></a>Migreren altijd op implementaties die enige downtime kunnen toestaan
Er zijn twee strategieën toomigrate altijd op implementaties die voor enige downtime toestaan:

1. **Meer secundaire replica's tooan bestaande altijd op de Cluster toevoegen**
2. **Migreren van tooa nieuwe altijd op Cluster**

#### <a name="1-add-more-secondary-replicas-tooan-existing-always-on-cluster"></a>1. Voeg meer secundaire replica's tooan bestaande altijd op Cluster
Een strategie tooadd meer secundaire databases toohello AlwaysOn-beschikbaarheidsgroep is. U moet tooadd deze in een nieuwe cloudservice en het bijwerken van Hallo listener Hallo nieuwe load balancer-IP-adres.

##### <a name="points-of-downtime"></a>De punten van downtime:
* Clustervalidatie van het.
* Always On failover testen voor de nieuwe secundaire replica's.

Als u Windows-opslaggroepen binnen Hallo VM voor een hogere i/o-doorvoer en vervolgens deze zal offline worden gehaald tijdens een volledige validatie van de Cluster. Hallo validatietest is vereist als u knooppunten toohello cluster toevoegen. Hallo duurt toorun Hallo test kan variëren, dus u dit in uw omgeving representatief test tooget bij benadering de tijd testen moet van hoe lang dit gaat duren.

U moet de tijd waarin u de handmatige failover kunt uitvoeren en chaos testen op Hallo zojuist toegevoegd knooppunten tooensure altijd op hoge beschikbaarheid functies zoals verwacht inrichten.

![DeploymentUseAlways On2][7]

> [!NOTE]
> Alle exemplaren van SQL Server waar de opslaggroepen hello worden gebruikt voordat hello validatie wordt uitgevoerd, moet worden gestopt.
>
> ##### <a name="high-level-steps"></a>Stappen op hoog niveau
>

1. Maak twee nieuwe SQL-Servers in de nieuwe cloudservice met gekoppelde Premium-opslag.
2. Kopiëren via volledige back-ups en herstellen met **NORECOVERY**.
3. Kopiëren via 'buiten user DB' afhankelijke objecten, zoals aanmeldingen enzovoort.
4. Maken van nieuwe een nieuwe interne Load Balancer (ILB) of gebruik een externe Load Balancer (ELB) en vervolgens Load Balanced eindpunten instellen op beide nieuwe knooppunten.

   > [!NOTE]
   > Controleer dat alle knooppunten hebben het juiste eindpuntconfiguratie Hallo voordat u doorgaat
   >
   >
5. Gebruiker/toepassing toegang toohello SQL Server stoppen (als u de opslaggroepen).
6. SQL Server-Engine-Services stoppen op alle knooppunten (als u de opslaggroepen).
7. Toevoegen van nieuwe knooppunten toocluster en volledige validatie uitvoeren.
8. Wanneer validatie voltooid is, start u alle SQL Server-Services.
9. Transactielogboeken back-up en herstel van gebruikersdatabases.
10. Nieuwe knooppunten toevoegen aan Hallo AlwaysOn-beschikbaarheidsgroep en replicatie in plaats **synchroon**.
11. Hallo IP toevoegen bron van het adres van Hallo nieuwe Cloud Service ILB-/ ELB via PowerShell voor altijd op op basis van Hallo multi-site voorbeeld in Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage). Stel in het Windows-clustering, Hallo **mogelijke eigenaars** Hallo **IP-adres** resource toohello nieuwe knooppunten oude. Zie 'IP-adres Resource toevoegen op hetzelfde Subnet' Hallo-sectie van Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
12. Failover tooone van Hallo nieuwe knooppunten.
13. Controleer Hallo nieuwe knooppunten automatisch Failoverpartners en testfailovers.
14. Oorspronkelijke knooppunten verwijderen uit de beschikbaarheidsgroep.

##### <a name="advantages"></a>Voordelen
* Nieuwe SQL-Servers kunnen worden getest (SQL Server en toepassing) voordat ze worden tooAlways toegevoegd op.
* U kunt Hallo VM-grootte wijzigen en aanpassen van Hallo tooyour exacte opslagvereisten. Echter, het normaal zou zijn nuttig tookeep alle Hallo SQL bestandspaden Hallo dezelfde.
* U kunt bepalen wanneer de overdracht Hallo van Hallo DB back-ups toohello secundaire replica's worden gestart. Dit wijkt af van het gebruik van Azure **Start AzureStorageBlobCopy** commandlet toocopy VHD's, omdat dit een asynchrone kopie.

##### <a name="disadvantages"></a>Nadelen
* Wanneer met behulp van Windows-opslaggroepen, is dit Cluster uitvaltijd tijdens Hallo volledige validatie van het Cluster voor Hallo nieuwe extra knooppunten.
* Afhankelijk van Hallo SQL Server-versie en Hallo bestaande aantal secundaire replica's, kunt u niet kunt tooadd worden meer secundaire replica's zonder te verwijderen van bestaande secundaire replica's.
* Kan er lang SQL gegevens overdrachtstijd tijdens het instellen van Hallo secundaire replica's zijn.
* Er is extra kosten tijdens de migratie terwijl u nieuwe machines parallelle uitvoering zijn.

#### <a name="2-migrate-tooa-new-always-on-cluster"></a>2. Migreren van tooa nieuwe altijd op Cluster
Een andere strategie is er toocreate een geheel nieuwe altijd op Cluster met nieuwe knooppunten in nieuwe cloudservice omleiding Hallo clients toouse deze.

##### <a name="points-of-downtime"></a>Punten van uitvaltijd
Er is uitvaltijd wanneer u toepassingen en gebruikers toohello nieuwe altijd-listener voor overdraagt. afhankelijk van Hallo downtime:

* Hallo tijd toorestore laatste transactie logboek back-ups toodatabases op nieuwe servers.
* Hallo tijd tooupdate client toepassingen toouse nieuwe altijd op listener.

##### <a name="advantages"></a>Voordelen
* U kunt Hallo werkelijke productieomgeving, SQL Server, testen en OS-build-wijzigingen.
* Hallo optie toocustomize Hallo opslag en toopotentially verkleinen van virtuele machine. Dit kan leiden tot kosten te beperken.
* Tijdens dit proces kunt u uw versie van SQL Server of een versie bijwerken. U kunt ook Hallo besturingssysteem bijwerken.
* Hallo die eerder altijd op Cluster als een doel effen terugdraaien fungeren kan.

##### <a name="disadvantages"></a>Nadelen
* U moet toochange Hallo DNS-naam van de listener Hallo als u wilt dat beide AlwaysOn-clusters die tegelijkertijd wordt uitgevoerd. Beheer overhead tijdens de migratie hello wordt toegevoegd als tekenreeksen van toepassingen voor client Hallo nieuwe Listener-naam moeten geven.
* U kunt een mechanisme voor synchronisatie tussen Hallo twee omgevingen tookeep als sluiten als mogelijke toominimize Hallo laatste synchronisatievereisten voor de migratie moet implementeren.
* Er is toegevoegd kosten tijdens de migratie terwijl u nieuwe Hallo-omgeving actief zijn.

### <a name="migrating-always-on-deployments-for-minimal-downtime"></a>Migreren altijd op implementaties voor minimale downtime
Er zijn twee strategieën voor het migreren altijd op implementaties voor minimale downtime:

1. **Gebruikmaken van een bestaande secundaire: één Site**
2. **Gebruikmaken van bestaande secundaire beschikbaarheidsreplica('s): meerdere locaties**

#### <a name="1-utilize-an-existing-secondary-single-site"></a>1. Gebruikmaken van een bestaande secundaire: één Site
Een strategie voor minimale downtime is tootake een bestaande secundaire cloud en van de huidige cloudservice Hallo verwijderen. Kopieer Hallo VHD's toohello nieuwe Premium Storage-account en Hallo VM in Hallo nieuwe cloudservice maken. Werk vervolgens Hallo-listener in clustering en failover.

##### <a name="points-of-downtime"></a>Punten van uitvaltijd
* Er is uitvaltijd wanneer u het laatste knooppunt Hallo met gelijke taakverdeling Hallo-eindpunt bijwerkt.
* Opnieuw verbinden met uw client mogelijk afhankelijk van de client en DNS-configuratie worden uitgesteld.
* Er is extra uitvaltijd als u ervoor tootake Hallo altijd op de Cluster groep offline tooswap Hallo IP-adressen kiest. U kunt dit vermijden met behulp van een afhankelijkheid of en mogelijke eigenaars voor Hallo bronnen IP-adres toegevoegd. Zie 'IP-adres Resource toevoegen op hetzelfde Subnet' Hallo-sectie van Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).

> [!NOTE]
> Wanneer u wilt dat Hallo toegevoegde knooppunt toopartake in als altijd op Failover-Partner, moet u tooadd een Azure-eindpunt met een verwijzing toohello Load Balanced ingesteld. Bij het uitvoeren van Hallo **toevoegen AzureEndpoint** opdracht toodo deze, huidige verbindingen tooremain openen, maar nieuwe verbindingen toohello-listener kan niet kunnen toobe tot stand gebracht totdat Hallo load balancer is bijgewerkt. In testen was dit waargenomen toolast 90-120seconds, dit moet worden getest.
>
>

##### <a name="advantages"></a>Voordelen
* Er zijn geen extra kosten die zijn gemaakt tijdens de migratie.
* Een-op-een migratie.
* Minder complexiteit.
* Verbeterde IOPS staat van Premium-opslag-SKU's. Als Hallo schijven is losgekoppeld van Hallo VM en gekopieerd toohello nieuwe cloudservice, een 3rd partij worden hulpprogramma gebruikte tooincrease Hallo VHD grootte, die hoger doorvoercapaciteit biedt. Zie voor het VHD-grootte verhogen, [forumdiscussie](https://social.msdn.microsoft.com/Forums/azure/4a9bcc9e-e5bf-4125-9994-7c154c9b0d52/resizing-azure-data-disk?forum=WAVirtualMachinesforWindows).

##### <a name="disadvantages"></a>Nadelen
* Er is een tijdelijk onderbroken HA en Noodherstel tijdens de migratie.
* Omdat dit een migratie 1:1, hebt u toouse een minimale VM-grootte die wordt ondersteuning voor het aantal virtuele harde schijven, zodat u mogelijk niet kunnen toodownsize uw virtuele machines.
* Dit scenario zou gebruiken hello Azure **Start AzureStorageBlobCopy** commandlet die asynchroon is. Er is geen SLA op voltooiing van de kopie. Hallo-tijd van Hallo kopieën varieert, terwijl dit afhankelijk van de wachttijd in wachtrij die het is ook afhankelijk van Hallo hoeveelheid gegevens tootransfer. Hallo kopie tijd toeneemt als Hallo overdracht gaat tooanother Azure-datacenter die ondersteuning biedt voor Premium-opslag in een andere regio. Als u zojuist 2 knooppunten hebt, kunt u overwegen een mogelijke risicobeperking geval Hallo kopie langer dan in de testfase duurt. Dit omvat bijvoorbeeld Hallo ideeën te volgen.
  * Een tijdelijk 3e SQL Server-knooppunt toevoegen voor HA vóór de migratie Hallo overeengekomen uitvaltijd.
  * Hallo migratie buiten Azure gepland onderhoud worden uitgevoerd.
  * Zorg ervoor dat u hebt uw clusterquorum correct geconfigureerd.  

##### <a name="high-level-steps"></a>Stappen op hoog niveau
Dit document niet illustratie van de voorbeeld van een volledige end-tooend echter Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage) vindt u gedetailleerde informatie die overgenomen tooperform worden kunnen dit.

![MinimalDowntime][8]

* Schijfconfiguratie verzamelen en verwijderen van het knooppunt hello (gekoppelde VHD's niet verwijderd).
* Premium-opslagaccount maken en kopieer van VHD's van Hallo Standard-opslagaccount
* Nieuwe cloudservice maken en implementeren van Hallo SQL2 VM in deze cloudservice. Hallo VM maken met behulp van Hallo gekopieerd oorspronkelijke besturingssysteem-VHD en koppelen van Hallo gekopieerd VHD's.
* Configureer ILB / ELB en het toevoegen van eindpunten.
* Update-Listener door:
  * Duurt Hallo altijd op de groep offline en bij te werken altijd op Listener met nieuwe ILB Hallo / ELB-IP-adressen.
  * Of Hallo IP-adres resource van nieuwe Cloud Service ILB-/ ELB via PowerShell in Windows-clustering toe te voegen. Vervolgens set Hallo mogelijke eigenaars van Hallo IP-adres resource toohello gemigreerd knooppunt SQL2, en dit als afhankelijkheid in Hallo netwerknaam of instellen. Zie 'IP-adres Resource toevoegen op hetzelfde Subnet' Hallo-sectie van Hallo [bijlage](#appendix-migrating-a-multisite-always-on-cluster-to-premium-storage).
* Controleer de DNS-configuratie/doorgiftetaak toohello clients.
* SQL1 VM gemigreerd en doorloop de stappen 2-4.
* Als u stappen 5ii, voegt u SQL1 als mogelijke eigenaar van Hallo bron van het IP-adres toegevoegd
* Testfailovers.

#### <a name="2-utilize-existing-secondary-replicas-multi-site"></a>2. Gebruikmaken van bestaande secundaire beschikbaarheidsreplica('s): meerdere locaties
Als u knooppunten in meer dan één Azure-datacenter (DC hebben) of als u een hybride omgeving hebt, kunt u een configuratie altijd op in deze omgeving toominimize uitvaltijd.

Hallo aanpak is toochange Hallo altijd op synchronisatie tooSynchronous voor Hallo on-premises of secundaire domeincontroller voor Azure en failover via toothat SQL Server. Kopieer Hallo VHD's tooa Premium Storage-account en Hallo-machine implementeren in een nieuwe cloudservice. Hallo-listener bijwerken en vervolgens een failback uit.

##### <a name="points-of-downtime"></a>Punten van uitvaltijd
Hallo uitvaltijd bestaat uit Hallo tijd toofailover toohello alternatieve DC en terug. Ook afhankelijk van de client en DNS-configuratie en de client opnieuw verbinden mag worden uitgesteld.
Houd rekening met Hallo voorbeeld van een hybride altijd op de configuratie te volgen:

![MultiSite1][9]

##### <a name="advantages"></a>Voordelen
* U kunt gebruikmaken van bestaande infrastructuur.
* Er Hallo optie toopre-upgrade hello Azure-opslag op Hallo DR Azure DC eerst.
* Hallo DC DR Azure-opslag opnieuw kan worden geconfigureerd.
* Er is een minimum van twee failovers tijdens de migratie, met uitzondering van testfailovers.
* U moet toomove SQL Server-gegevens met back-up en herstellen.

##### <a name="disadvantages"></a>Nadelen
* Afhankelijk van de client toegang tooSQL Server, kunnen er langere latentie als SQL Server wordt uitgevoerd in een alternatieve DC toohello toepassing.
* Hallo kopie tijd van VHD's tooPremium opslag kan lang zijn. Dit kan invloed hebben op uw beslissing op of tookeep Hallo knooppunt in het Hallo-beschikbaarheidsgroep. U kunt dit wanneer logboek intensieve belasting worden uitgevoerd tijdens de migratie Hallo niets te doen, omdat het primaire knooppunt Hallo tookeep Hallo van niet-gerepliceerde transacties in het transactielogboek. Daarom kan dit aanzienlijk groeien.
* Dit scenario zou gebruiken hello Azure **Start AzureStorageBlobCopy** commandlet die asynchroon is. Er is geen SLA op voltooiing. Hallo tijd Hallo kopieën varieert, terwijl dit afhankelijk van de wachttijd in wachtrij, het is ook afhankelijk van Hallo hoeveelheid gegevens tootransfer. Daarom alleen hebt u één knooppunt in uw datacenter 2e, u moet treffen risicobeperking geval Hallo kopie langer duurt dan in de testfase. Dit omvat bijvoorbeeld Hallo ideeën te volgen.
  * Een tijdelijke SQL-knooppunt 2e toevoegen voor HA vóór de migratie Hallo overeengekomen uitvaltijd.
  * Hallo migratie buiten Azure gepland onderhoud worden uitgevoerd.
  * Zorg ervoor dat u hebt uw clusterquorum correct geconfigureerd.

Dit scenario wordt ervan uitgegaan dat u de installatie hebt gedocumenteerd en weten hoe Hallo opslag is toegewezen in volgorde toomake wijzigingen voor optimale schijf cache-instellingen.

##### <a name="high-level-steps"></a>Stappen op hoog niveau
![Multisite2][10]

* Lokale Hallo / alternatieve Azure DC Hallo SQL Server de primaire en maken het Hallo andere automatische Failover Partner (AFP) maken.
* Verzamelen van gegevens over de schijfconfiguratie van SQL2 en verwijderen van het knooppunt hello (gekoppelde VHD's niet verwijderd).
* Premium-opslagaccount maken en kopieer VHD's van Hallo Standard-opslagaccount.
* Maak een nieuwe cloudservice en Hallo SQL2 VM maken met de opslag van premies schijven die zijn gekoppeld.
* Configureer ILB / ELB en het toevoegen van eindpunten.
* Update Hallo altijd op Listener met nieuwe ILB / ELB IP-adres en test failover.
* Controleer de Hallo DNS-configuratie.
* Hallo AFP tooSQL2, wijzigen en migreren van SQL1 en stappen 2 tot en met 5 doorlopen.
* Testfailovers.
* Ga terug tooSQL1 Hallo AFP en SQL2

## <a name="appendix-migrating-a-multisite-always-on-cluster-toopremium-storage"></a>Bijlage: Een implementatie voor meerdere locaties altijd op Cluster tooPremium opslag migreren
Hallo rest van dit onderwerp biedt een gedetailleerd voorbeeld van het converteren van een opslag voor meerdere locaties tooPremium altijd aan cluster. Hallo Listener worden geconverteerd van het gebruik van een externe load balancer (ELB) tooan interne load balancer (ILB).

### <a name="environment"></a>Omgeving
* Windows 2k 12 / SQL 2k 12
* Bestanden op SP 1 DB
* 2 x opslaggroepen per knooppunt

![Appendix1][11]

### <a name="vm"></a>VIRTUELE MACHINE:
In dit voorbeeld gaan we toodemonstrate verplaatsen van een ELB-tooILB. ELB is beschikbaar voordat ILB, zodat dit ziet u hoe tooswitch toothis tijdens de migratie Hallo.

![Appendix2][12]

### <a name="pre-steps-connect-toosubscription"></a>Pre-stappen: Verbinding maken met tooSubscription
    Add-AzureAccount

    #Set up subscription
    Get-AzureSubscription

#### <a name="step-1-create-new-storage-account-and-cloud-service"></a>Stap 1: Nieuw Opslagaccount maken en in de Cloud Service
    $mysubscription = "DansSubscription"
    $location = "West Europe"

    #Storage accounts
    #current storage account where hello vm toomigrate resides
    $origstorageaccountname = "danstdams"

    #Create Premium Storage account
    $newxiostorageaccountname = "danspremsams"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountname -Location $location -Type "Premium_LRS"  

    #Generate storage keys for later
    $originalstorage =  Get-AzureStorageKey -StorageAccountName $origstorageaccountname
    $xiostorage = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountname

    #Generate storage acc contexts
    $origContext = New-AzureStorageContext  –StorageAccountName $origstorageaccountname -StorageAccountKey $originalstorage.Primary
    $xioContext = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountname -StorageAccountKey $xiostorage.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $origstorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #CREATE NEW CLOUD SVC
    $vnet = "dansvnetwesteur"

    ##Existing cloud service
    $sourceSvc="dansolSrcAms"

    ##Create new cloud service
    $destcloudsvc = "danNewSvcAms"
    New-AzureService $destcloudsvc -Location $location

#### <a name="step-2-increase-hello-permitted-failures-on-resources-optional"></a>Stap 2: Toename Hallo fouten toegestaan op resources<Optional>
Bepaalde bronnen die deel uitmaken van AlwaysOn-beschikbaarheidsgroep tooyour er gelden beperkingen op hoeveel fouten die in een periode optreden, waarbij Hallo cluster-service het toorestart Hallo resourcegroep probeert. Het is raadzaam dat u deze verhogen, terwijl u via deze procedure worden roulatie van omdat als u niet handmatig failover en trigger failovers door het afsluiten van computers u sluiten toothis limiet kunt krijgen.

Deze zou worden voorzichtig toodouble Hallo fout vergoeding toodo dit in Failoverclusterbeheer, gaat u toohello-eigenschappen van Hallo altijd op resourcegroep:

![Appendix3][13]

Maximum aantal fouten too6 Hallo wijzigen.

#### <a name="step-3-addition-ip-address-resource-for-cluster-group-optional"></a>Stap 3: Aanvullende IP-adres resource voor de clustergroep<Optional>
Als u slechts één IP-adres voor de clustergroep Hallo dit uitgelijnde toohello cloud subnet is, houd er rekening mee, als u per ongeluk offline alle clusterknooppunten in Hallo cloud halen op dat netwerk vervolgens Hallo Cluster-IP-resource en de clusternetwerknaam niet zal kunnen toocome Online. In Hallo-gebeurtenis van dit wordt voorkomen dat tooother clusterbronnen updates.

#### <a name="step-4-dns-configuration"></a>Stap 4: DNS-configuratie
tooimplement een overgang is afhankelijk van hoe DNS wordt gebruikt en bijgewerkt.
Wanneer altijd op is geïnstalleerd, wordt er een resourcegroep van Windows-Cluster gemaakt als u Failoverclusterbeheer opent, ziet u dat ten minste drie middelen beschikken, Hallo twee die Hallo document verwijst tooare:

* Virtuele-netwerknaam (VNN) – Dit is Hallo DNS-naam die client toowhen productiviteitsniveau tooconnect tooSQL Servers via altijd op verbinding maken.
* Bron van het IP-adres – Dit IP-adres die zijn gekoppeld aan Hallo VNN Hallo is, kunt u meer dan één hebben en in een configuratie voor meerdere sites hebt u een IP-adres per site/subnet.

Wanneer verbindende tooSQL Hallo-stuurprogramma voor SQL Server Client-Server wordt Hallo DNS-records die zijn gekoppeld aan het Hallo-listener ophalen en probeer het tooconnect tooeach altijd aan dat IP-adres is gekoppeld, worden hieronder bespreken we een aantal factoren die van invloed kunnen zijn op dit.

Hallo aantal gelijktijdige DNS-records die gekoppeld aan de naam van de beschikbaarheidsgroeplistener Hallo zijn afhankelijk niet alleen Hallo aantal IP-adressen die zijn gekoppeld, maar Hallo ' RegisterAllIpProviders'setting in Failover Clustering voor Hallo altijd ON VNN resource.

Wanneer u altijd op in Azure implementeert er zijn verschillende stappen toocreate Hallo Listener en IP-adressen, hebt u toomanually Hallo 'RegisterAllIpProviders' too1 configureren, is dit verschillende tooan on-premises altijd op implementatie waarbij too1 is al ingesteld.

Als 'RegisterAllIpProviders' 0 is, klikt u vervolgens ziet alleen u een DNS-record in DNS die zijn gekoppeld aan Hallo Listener:

![Appendix4][14]

Als 'RegisterAllIpProviders' 1:

![Appendix5][15]

Hallo-code hieronder wordt dump uit Hallo VNN instellingen en voor u ingesteld, neem Opmerking voor Hallo wijzigen tootake effect moet u tootake hello VNN offline en weer online inschakelen, deze nemen Hallo Listener offline veroorzaakt client connectiviteit wordt onderbroken.

    ##Always On Listener Name
    $ListenerName = "Mylistener"
    ##Get AlwaysOn Network Name Settings
    Get-ClusterResource $ListenerName| Get-ClusterParameter
    ##Set RegisterAllProvidersIP
    Get-ClusterResource $ListenerName| Set-ClusterParameter RegisterAllProvidersIP  1

In een latere migratiestap van de moet u tooupdate Hallo altijd-listener voor met een bijgewerkte IP-adres dat verwijst naar een load balancer, dient hiervoor een IP-adres resource verwijderen en toevoegen. Na Hallo IP-update moet u tooensure Hallo nieuwe IP-adres is bijgewerkt in DNS-Zone en het Hallo-clients hun lokale DNS-cache bijwerken.

Als uw clients zich in een ander netwerksegment bevinden en verwijzen naar een andere DNS-server, moet u tooconsider wat gebeurt er over het overdragen van DNS-Zone tijdens de migratie Hallo Hallo toepassing bezorgd tijd zal worden beperkt door ten minste Hallo Zone Transfer tijd een nieuwe IP-adressen voor Hallo listener. Als u hier tijd-beperking, u moet worden behandeld en testen forceren van een incrementele zoneoverdracht met uw Windows-teams, en ook plaatsen Hallo DNS host record tooa verlagen tijd tooLive (TTL), zodat clients Hallo bijwerken. Zie voor meer informatie [incrementele zoneoverdrachten](https://technet.microsoft.com/library/cc958973.aspx) en [Start DnsServerZoneTransfer](https://technet.microsoft.com/library/jj649917.aspx).

Hallo standaard TTL-waarde van de DNS-Record die is gekoppeld aan het Hallo-Listener in altijd op in Azure is 1200 seconden. U kunt desgewenst tooreduce dit als u tijd beperking tijdens de migratie tooensure Hallo clients update hun DNS met Hallo bijgewerkt IP-adres voor Hallo listener. U kunt zien en Hallo-configuratie wijzigen door het dumpen van Hallo configuratie Hallo VNN:

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"
    #Look at HostRecordTTL
    Get-ClusterResource $ListenerName| Get-ClusterParameter

    #Set HostRecordTTL Examples
    Get-ClusterResource $ListenerName| Set-ClusterParameter -Name "HostRecordTTL" 120

Houd er rekening mee, Hallo lagere Hallo 'HostRecordTTL', een hogere mate van DNS-verkeer wordt uitgevoerd.

##### <a name="client-application-settings"></a>Instellingen voor client-toepassing
Als uw SQL-client toepassing ondersteunt Hallo .net 4.5 SQLClient, dan hebt u kunt gebruiken ' MULTISUBNETFAILOVER = TRUE' sleutelwoord, dit wordt aanbevolen toobe toegepast zoals maakt het mogelijk sneller verbinding tooSQL AlwaysOn-beschikbaarheidsgroep tijdens failover. Het inventariseren via alle IP-adressen die zijn gekoppeld aan Hallo altijd-listener voor parallel en een agressievere TCP opnieuw verbindingssnelheid tijdens een failover uitvoert.

Zie voor meer informatie over Hallo bovenstaande instellingen [MultiSubnetFailover sleutelwoord en functies die zijn gekoppeld](https://msdn.microsoft.com/library/hh213080.aspx#MultiSubnetFailover). Zie ook [SqlClient-ondersteuning voor hoge beschikbaarheid, herstel na noodgevallen](https://msdn.microsoft.com/library/hh205662\(v=vs.110\).aspx).

#### <a name="step-5-cluster-quorum-settings"></a>Stap 5: Instellingen van het clusterquorum
Als u toobe duurt uit ten minste één SQL-Server niet actief op een tijdstip gaat, moet u Hallo clusterquorum instelling wijzigen als u File Share Witness (FSW) met 2 knooppunten, moet u Hallo quorum tooallow Knooppuntmeerderheid instellen en gebruikmaken van dynamische stemmen, en dit tooallow voor een permanente tooremain van één knooppunt.

    Set-ClusterQuorum -NodeMajority  

Zie voor meer informatie over het beheren en configureren van het clusterquorum Hallo [configureren en beheren Hallo Quorum in een Windows Server 2012-failovercluster](https://technet.microsoft.com/library/jj612870.aspx).

#### <a name="step-6-extract-existing-endpoints-and-acls"></a>Stap 6: Extraheren bestaande eindpunten en ACL 's
    #GET Endpoint info
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureEndpoint
    #GET ACL Rules for Each EP, this example is for hello Always On Endpoint
    Get-AzureVM -ServiceName $destcloudsvc -Name $vmNameToMigrate | Get-AzureAclConfig -EndpointName "myAOEndPoint-LB"  

Sla deze tooa tekstbestand.

#### <a name="step-7-change-failover-partners-and-replication-modes"></a>Stap 7: Failoverpartners en replicatie-modi wijzigen
Als u meer dan 2 SQL-Servers hebt, u hoeft Hallo failover van een andere secundaire in een andere domeincontroller te wijzigen of on-premises too'Synchronous en kunt u een Partner voor automatische Failover (AFP), is dit zodat u HA onderhouden terwijl u wijzigingen doorvoert. U kunt dit doen via TSQL van echter SSMS wijzigen:

![Appendix6][16]

#### <a name="step-8-remove-secondary-vm-from-cloud-service"></a>Stap 8: Verwijder secundaire virtuele machine van de cloudservice
U rekening mee moet houden toomigrate een secundair knooppunt cloud als dit momenteel primaire is, moet u eerst een handmatige failover initiëren.

    $vmNameToMigrate="dansqlams2"

    #Check machine status
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Shutdown secondary VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM


    #Extract disk configuration

    ##Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk config, make sure below returns hello disks associated with hello VM
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machibe is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-9-change-disk-caching-settings-in-csv-file-and-save"></a>Stap 9: Instellingen in CSV-bestand van de schijfcache wijzigen en opslaan
Voor gegevensvolumes moeten deze tooREADONLY worden ingesteld.

Voor TLOG volumes moeten deze tooNONE worden ingesteld.

![Appendix7][17]

#### <a name="step-10-copy-vhds"></a>Stap 10: Kopie VHD 's
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContext

    ####DISK COPYING####
    #Get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname.blob.core.windows.net/vhds/$vhdname" `
    -SrcContext $origContext `
    -DestContainer $containerName `
    -DestBlob $vhdname `
    -DestContext $xioContext
       }



U kunt Hallo kopiestatus controleren van Hallo VHD's toohello Premium Storage-account:

    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContext
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix8][18]

Wacht totdat deze worden geregistreerd als geslaagd.

Voor informatie over afzonderlijke blobs:

    Get-AzureStorageBlobCopyState -Blob "blobname.vhd" -Container $containerName -Context $xioContext

#### <a name="step-11-register-os-disk"></a>Stap 11: Register OS-schijf
    #Change storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountname
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

#### <a name="step-12-import-secondary-into-new-cloud-service"></a>Stap 12: Secundaire importeren in de nieuwe cloudservice
Hallo-code hieronder ook gebruikt Hallo toegevoegd optie hier u kunt Hallo machine importeren en gebruiken van Hallo retainable VIP.

    #Build VM Config
    $ipaddr = "192.168.0.5"
    #Remember toochange tooXIO
    $newInstanceSize = "Standard_DS13"
    $subnet = "SQL"

    #Create new Avaiability Set
    $availabilitySet = "cloudmigAVAMS"

    #build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###Attaching disks tooa VM during a deploy tooa new cloud service and new storage account is different from just attaching VHDs toojust a redeploy in a new cloud service
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountname.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet ## Optional (-ReservedIPName $reservedVIPName)

#### <a name="step-13-create-ilb-on-new-cloud-svc-add-load-balanced-endpoints-and-acls"></a>Stap 13: Maak ILB op nieuwe Cloud Svc toevoegen van Load Balanced eindpunten en ACL's
    #Check for existing ILB
    GET-AzureInternalLoadBalancer -ServiceName $destcloudsvc

    $ilb="sqlIntIlbDest"
    $subnet = "SQL"
    $IP="192.168.0.25"
    Add-AzureInternalLoadBalancer -ServiceName $destcloudsvc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP

    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM

    #SET Azure ACLs or Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

    ####WAIT FOR FULL AlwaysOn RESYNCRONISATION!!!!!!!!!#####

#### <a name="step-14-update-always-on"></a>Stap 14: Altijd bijwerken op
    #Code toobe executed on a Cluster Node
    $ClusterNetworkNameAmsterdam = "Cluster Network 2" # hello azure cluster subnet network name
    $newCloudServiceIPAmsterdam = "192.168.0.25" # IP address of your cloud service

    $AGName = "myProductionAG"
    $ListenerName = "Mylistener"


    Add-ClusterResource "IP Address $newCloudServiceIPAmsterdam" -ResourceType "IP Address" -Group $AGName -ErrorAction Stop |  Set-ClusterParameter -Multiple @{"Address"="$newCloudServiceIPAmsterdam";"ProbePort"="59999";SubnetMask="255.255.255.255";"Network"=$ClusterNetworkNameAmsterdam;"OverrideAddressMatch"=1;"EnableDhcp"=0} -ErrorAction Stop

    #set dependancy and NETBIOS, then remove old IP address

    #set NETBIOS, then remove old IP address
    Get-ClusterGroup $AGName | Get-ClusterResource -Name "IP Address $newCloudServiceIPAmsterdam" | Set-ClusterParameter -Name EnableNetBIOS -Value 0

    #set dependency tooListener (OR Dependency) and delete previous IP Address resource that references:

    #Make sure no static records in DNS

![Appendix9][19]

Nu Hallo oude cloudservice IP-adres verwijderen.

![Appendix10][20]

#### <a name="step-15-dns-update-check"></a>Stap 15: DNS-updates controleren
U moet nu DNS-Servers in uw SQL Server client netwerken controleren en zorg ervoor dat het clustering Hallo heeft toegevoegd extra hostrecord voor Hallo IP-adres toegevoegd. Als deze DNS-servers niet hebt bijgewerkt, houd rekening met het forceren van een DNS-Zone-overdracht en controleer of hello clients in er subnet zijn kunnen tooresolve tooboth altijd op IP-adressen, dit is dus u hoeft geen toowait voor automatische DNS-replicatie.

#### <a name="step-16-reconfigure-always-on"></a>Stap 16: Configureer altijd opnieuw op
Op dit moment wachten op Hallo secundaire dat knooppunt die gemigreerde toofully is gesynchroniseerd met de Hallo lokale knooppunt- en switch toosynchronous bestandsreplicatie-knooppunt en kunnen Hallo AFP.  

#### <a name="step-17-migrate-second-node"></a>Stap 17: Tweede knooppunt migreren
    $vmNameToMigrate="dansqlams1"

    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

    #Get endpoint information
    $endpoint = Get-AzureVM -ServiceName $sourceSvc  -Name $vmNameToMigrate | Get-AzureEndpoint

    #Shutdown VM
    Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | stop-AzureVM

    #Get disk config

    #Building Existing Data Disk Configuration
    $file = "C:\Azure Storage Testing\mydiskconfig_$vmNameToMigrate.csv"
    $datadisks = @(Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureDataDisk )
    Add-Content $file “lun, vhdname, hostcaching, disklabel, diskName”
    foreach ($disk in $datadisks)
    {
      $vhdname = $disk.MediaLink.AbsolutePath -creplace  "/vhds/"
      $disk.Lun, , $disk.HostCaching, $vhdname, $disk.DiskLabel,$disks.DiskName
    # Write-Host "copying disk $disk"
    $adddisk = "{0},{1},{2},{3},{4}" -f $disk.Lun,$vhdname, $disk.HostCaching, $disk.DiskLabel, $disk.DiskName
    $adddisk | add-content -path $file
    }

    #Get OS Disk
    $osdisks = Get-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate | Get-AzureOSDisk ## | select -ExpandProperty MediaLink
    $osvhdname = $osdisks.MediaLink.AbsolutePath -creplace  "/vhds/"
    $osdisks.OS, $osdisks.HostCaching, $osvhdname, $osdisks.DiskLabel, $osdisks.DiskName
    $addosdisk = "{0},{1},{2},{3},{4}" -f $osdisks.OS,$osvhdname, $osdisks.HostCaching, $osdisks.Disklabel , $osdisks.DiskName
    $addosdisk | add-content -path $file

    #Import disk config
    $diskobjects  = Import-CSV $file

    #Check disk configuration
    $diskobjects

    #Identify OS Disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osdiskforbuild = $osdiskimport.diskName

    #Check machine is off
    Get-AzureVM -ServiceName $sourceSvc -Name  $vmNameToMigrate

    #Drop machine and rebuild toonew cls
    Remove-AzureVM -ServiceName $sourceSvc -Name $vmNameToMigrate

#### <a name="step-18-change-disk-caching-settings-in-csv-file-and-save"></a>Stap 18: Instellingen in CSV-bestand van de schijfcache wijzigen en opslaan
Voor gegevensvolumes moeten deze tooREADONLY worden ingesteld.

Voor TLOG volumes moeten deze tooNONE worden ingesteld.

![Appendix11][21]

#### <a name="step-19-create-new-independent-storage-account-for-secondary-node"></a>Stap 19: Maak een nieuwe onafhankelijke Storage-Account voor secundair knooppunt
    $newxiostorageaccountnamenode2 = "danspremsams2"
    New-AzureStorageAccount -StorageAccountName $newxiostorageaccountnamenode2 -Location $location -Type "Premium_LRS"  

    #Reset hello storage account src if node 1 in a different storage account
    $origstorageaccountname2nd = "danstdams2"

    #Generate storage keys for later
    $xiostoragenode2 = Get-AzureStorageKey -StorageAccountName $newxiostorageaccountnamenode2

    #Generate storage acc contexts
    $xioContextnode2 = New-AzureStorageContext  –StorageAccountName $newxiostorageaccountnamenode2 -StorageAccountKey $xiostoragenode2.Primary  

    #Set up subscription and default storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

#### <a name="step-20-copy-vhds"></a>Stap 20: Kopie VHD 's
    #Ensure you have created hello container for these:
    $containerName = 'vhds'

    #Create container
    New-AzureStorageContainer -Name $containerName -Context $xioContextnode2  

    ####DISK COPYING####
    ##get disks from csv, get settings for each VHDs and copy tooPremium Storage accoun
    ForEach ($disk in $diskobjects)
       {
       $lun = $disk.Lun
       $vhdname = $disk.vhdname
       $cacheoption = $disk.HostCaching
       $disklabel = $disk.DiskLabel
       $diskName = $disk.DiskName
       Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname has cache setting : $cacheoption"

       #Start async copy
       Start-AzureStorageBlobCopy -srcUri "https://$origstorageaccountname2nd.blob.core.windows.net/vhds/$vhdname" `
        -SrcContext $origContext `
        -DestContainer $containerName `
        -DestBlob $vhdname `
        -DestContext $xioContextnode2
       }

    #Check for copy progress

    #check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContext


U kunt Hallo VHD kopiestatus controleren voor alle virtuele harde schijven: ForEach ($disk in $diskobjects) {$lun = $disk. LUN $vhdname = $disk.vhdname $cacheoption = $disk. HostCaching $disklabel = $disk. Schijflabel $diskName = $disk. DiskName

       $copystate = Get-AzureStorageBlobCopyState -Blob $vhdname -Container $containerName -Context $xioContextnode2
    Write-Host "Copying Disk Lun $lun, Label : $disklabel, VHD : $vhdname, STATUS = " $copystate.Status
       }

![Appendix12][22]

Wacht totdat deze worden geregistreerd als geslaagd.

Voor informatie over afzonderlijke blobs:

    #Check induvidual blob status
    Get-AzureStorageBlobCopyState -Blob "danRegSvcAms-dansqlams1-2014-07-03.vhd" -Container $containerName -Context $xioContextnode2

#### <a name="step-21-register-os-disk"></a>Stap 21: Register OS-schijf
    #change storage account toohello new XIO storage account
    Set-AzureSubscription -SubscriptionName $mysubscription -CurrentStorageAccount $newxiostorageaccountnamenode2
    Select-AzureSubscription -SubscriptionName $mysubscription -Current

    #Register OS disk
    $osdiskimport = $diskobjects | where {$_.lun -eq "Windows"}
    $osvhd = $osdiskimport.vhdname
    $osdiskforbuild = $osdiskimport.diskName

    #Registering OS disk, but as XIO disk
    $xioDiskName = $osdiskforbuild + "xio"
    Add-AzureDisk -DiskName $xioDiskName -MediaLocation  "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$osvhd"  -Label "BootDisk" -OS "Windows"

    #Build VM Config
    $ipaddr = "192.168.0.4"
    $newInstanceSize = "Standard_DS13"

    #Join tooexisting Avaiability Set

    #Build machine config into object
    $vmConfig = New-AzureVMConfig -Name $vmNameToMigrate -InstanceSize $newInstanceSize -DiskName $xioDiskName -AvailabilitySetName $availabilitySet  ` | Add-AzureProvisioningConfig -Windows ` | Set-AzureSubnet -SubnetNames $subnet | Set-AzureStaticVNetIP -IPAddress $ipaddr

    #Reload disk config
    $diskobjects  = Import-CSV $file
    $datadiskimport = $diskobjects | where {$_.lun -ne "Windows"}

    ForEach ( $attachdatadisk in $datadiskimport)
       {
    $label = $attachdatadisk.disklabel
    $lunNo = $attachdatadisk.lun
    $hostcach = $attachdatadisk.hostcaching
    $datadiskforbuild = $attachdatadisk.diskName
    $vhdname = $attachdatadisk.vhdname

    ###This is different toojust a straight cloud service change
    #note if you do not have a disk label hello command below will fail, populate as required.
    $vmConfig | Add-AzureDataDisk -ImportFrom -MediaLocation "https://$newxiostorageaccountnamenode2.blob.core.windows.net/vhds/$vhdname" -LUN $lunNo -HostCaching $hostcach -DiskLabel $label

    }

    #Create VM
    $vmConfig  | New-AzureVM –ServiceName $destcloudsvc –Location $location -VNetName $vnet -Verbose

#### <a name="step-22-add-load-balanced-endpoints-and-acls"></a>Stap 22: Toevoegen Load Balanced eindpunten en ACL's
    #Endpoints
    $epname="sqlIntEP"
    $prot="tcp"
    $locport=1433
    $pubport=1433
    Get-AzureVM –ServiceName $destcloudsvc –Name $vmNameToMigrate  | Add-AzureEndpoint -Name $epname -Protocol $prot -LocalPort $locport -PublicPort $pubport -ProbePort 59999 -ProbeIntervalInSeconds 5 -ProbeTimeoutInSeconds 11  -ProbeProtocol "TCP" -InternalLoadBalancerName $ilb -LBSetName $ilb -DirectServerReturn $true | Update-AzureVM


    #STOP!!! CHECK in hello Azure portal or Machine Endpoints through PowerShell that these Endpoints are created!

    #SET ACLs or Azure Network Security Groups & Windows FWs

    #http://msdn.microsoft.com/library/azure/dn495192.aspx

#### <a name="step-23-test-failover"></a>Stap 23: De testfailover
U moet nu laten Hallo gemigreerde knooppunt worden gesynchroniseerd met de Hallo lokale altijd aan knooppunt, plaatst u het in toosynchronous replicatiemodus en wacht totdat deze is gesynchroniseerd. Vervolgens failover van het eerste knooppunt van on-premises toohello gemigreerd, namelijk Hallo AFP. Zodra die eerder heeft gewerkt, gemigreerd Hallo wijziging laatste knooppunt toohello AFP.

U moet testfailovers tussen alle knooppunten en hoewel chaos tests tooensure failovers zoals werken verwacht en in een tijdige manor uitvoeren.

#### <a name="step-24-put-back-cluster-quorum-settings--dns-ttl--failover-pntrs--sync-settings"></a>24 stap: Opnieuw clusterquoruminstellingen zetten / DNS TTL / Failover Pntrs / synchronisatie-instellingen
##### <a name="adding-ip-address-resource-on-same-subnet"></a>Toevoegen van de bron van het IP-adres op hetzelfde Subnet
Als u alleen 2 SQL-Servers en toomigrate wilt ze tooa nieuwe cloudservice, maar wilt tookeep op hetzelfde subnet hello, kunt u vermijden Hallo listener altijd offline toodelete Hallo oorspronkelijke op IP-adres en Hallo nieuwe IP-adres toevoegen. Als u Hallo VMs tooanother subnet hoeft u niet toodo dit migreert omdat er een extra clusternetwerk dat verwijst naar dat subnet.

Als u hebt gebracht Hallo secundaire gemigreerd en toegevoegd in het nieuwe IP-adres resource Hallo voor nieuwe cloudservice Hallo voordat failover Hallo bestaande primaire, moet u deze stappen binnen Hallo Failover-clusterbeheer nemen:

tooadd in IP-adres, Zie Hallo [bijlage](#appendix-migrating-a-multisite-alwayson-cluster-to-premium-storage), stap 14.

1. Voor Hallo huidige IP-adres resource wijzigen Hallo mogelijke eigenaar too'Existing primaire SQL-Server', in onderstaande 'dansqlams4' Hallo-voorbeeld:

    ![Appendix13][23]
2. Voor Hallo nieuwe IP-adres resource wijzigen Hallo mogelijke eigenaar too'Migrated secundaire SQL-Server', in onderstaande 'dansqlams5' Hallo-voorbeeld:

    ![Appendix14][24]
3. Wanneer deze optie is ingesteld, kunt u failover en wanneer het laatste knooppunt hello wordt gemigreerd Hallo mogelijke eigenaars worden bewerkt zodat dit knooppunt wordt toegevoegd als een mogelijke eigenaar:

    ![Appendix15][25]

## <a name="additional-resources"></a>Aanvullende bronnen
* [Azure Premium-opslag](../../../storage/common/storage-premium-storage.md)
* [Virtuele machines](https://azure.microsoft.com/services/virtual-machines/)
* [SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

<!-- IMAGES -->
[1]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/1_VNET_Portal.png
[2]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/2_Diskname_Lun.png
[3]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/3_Virtual_Disk_Properties.png
[4]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/4_Virtual_Disk_Properties_Details.png
[5]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/5_Get_Storage_Pool.png
[6]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/6_Deployments_Always_On.png
[7]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/7_Add_More_Secondaries.png
[8]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/8_Use_Existing_Secondary_Single_Site.png
[9]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site.png
[10]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/9_Use_Existing_Secondary_Multi_Site_b.png
[11]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_01.png
[12]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_02.png
[13]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_03.png
[14]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_04.png
[15]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_05.png
[16]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_06.png
[17]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_07.png
[18]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_08.png
[19]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_09.png
[20]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_10.png
[21]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_11.png
[22]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_12.png
[23]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_13.png
[24]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_14.png
[25]: ./media/virtual-machines-windows-classic-sql-server-premium-storage/10_Appendix_15.png

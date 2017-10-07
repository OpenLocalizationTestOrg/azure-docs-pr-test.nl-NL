---
title: aaaCreate een SQL Server-Machine in Azure PowerShell (klassiek) | Microsoft Docs
description: "Bevat de stappen en PowerShell-scripts voor het maken van een virtuele machine in Azure met SQL Server-installatiekopieën voor virtuele machine-galerie. In dit onderwerp maakt gebruik van de klassieke implementatiemodus Hallo."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>Een SQL Server-machine met Azure PowerShell (klassiek) inrichten

In dit artikel bevat stappen voor hoe toocreate een SQL Server virtuele machine in Azure met behulp van PowerShell-cmdlets Hallo.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../azure-resource-manager/resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.

Zie voor Hallo Resource Manager-versie van dit onderwerp [een met Azure PowerShell-Resource Manager van SQL Server-machine inrichten](../sql/virtual-machines-windows-ps-sql-create.md).

### <a name="install-and-configure-powershell"></a>PowerShell installeren en configureren:
1. Als u geen Azure-account hebt, gaat u naar [Azure, gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
2. [Download en installeer de nieuwste Azure PowerShell-opdrachten Hallo](/powershell/azure/overview).
3. Start Windows PowerShell en tooyour Azure-abonnement verbinden met de Hallo **Add-AzureAccount** opdracht.

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>Het doel-Azure-regio bepalen

Uw virtuele Machine van SQL Server zal worden gehost in een cloudservice die een specifieke Azure-regio. Hallo volgende stappen kunt u toodetermine uw regio, de storage-account en de cloudservice, die wordt gebruikt voor de rest van de zelfstudie Hallo Hallo.

1. Hallo datacenter dat u wilt dat toouse toohost uw SQL Server VM bepalen. Hallo volgende PowerShell-opdracht geeft een lijst van beschikbare regionamen.

   ```powershell
   (Get-AzureLocation).Name
   ```

2. Zodra u de gewenste locatie hebt geïdentificeerd, instellen van een variabele met de naam **$dcLocation** toothat regio. Bijvoorbeeld, Hallo opdracht sets Hallo regio te volgen 'VS-Oost':

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>Uw abonnement en storage-account instellen

1. Hello Azure-abonnement u voor de nieuwe virtuele machine Hallo gebruiken wilt bepalen.

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. Toewijzen van uw Azure-abonnement doel toohello **$subscr** variabele. Dit wordt ingesteld als uw huidige Azure-abonnement.

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. Vervolgens kunt u controleren op bestaande opslagaccounts. Hallo geeft volgende script alle opslagaccounts die zijn opgenomen in uw gekozen regio:

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > Als u een nieuw opslagaccount vereist, moet u eerst een opslagaccountnaam alle kleine maken met de opdracht zoals in het volgende voorbeeld Hallo Hallo nieuw AzureStorageAccount:`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. Hallo doel storage account name toohello toewijzen **$staccount**. Gebruik vervolgens **Set-AzureSubscription** tooset Hallo abonnement en de huidige opslagaccount.

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>Selecteer de installatiekopie van een SQL Server-virtuele machine

1. Ontdek Hallo lijst met beschikbare virtuele machines van SQL Server-installatiekopieën uit Hallo galerie. Deze installatiekopieën alle hebben een **ImageFamily** eigenschap die met 'SQL begint'. Hallo volgende query geeft Hallo installatiekopie familie beschikbaar tooyou die SQL Server vooraf geïnstalleerd hebben.

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. Wanneer u Hallo virtuele machine installatiekopie familie gevonden, kan dit worden veroorzaakt door meerdere gepubliceerde afbeeldingen in deze familie. Gebruik Hallo volgende script toofind Hallo nieuwste gepubliceerde naam virtuele machine-installatiekopie voor de geselecteerde installatiekopie-familie (zoals **RTM Enterprise van SQL Server 2016 op Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>Hallo virtuele machine maken

Maak ten slotte Hallo virtuele machine met PowerShell:

1. Maak een cloud service toohost Hallo nieuwe virtuele machine. Houd er rekening mee dat het is ook mogelijk toouse een bestaande cloudservice in plaats daarvan. Maak een nieuwe variabele **$svcname** met korte naam van de cloudservice Hallo Hallo.

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. Naam van de virtuele machine Hallo en een grootte opgeven. Zie voor meer informatie over de grootte van virtuele machines, [grootten van virtuele machines voor Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. Hallo lokale administrator-account en wachtwoord opgeven.

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. Hallo na script toocreate Hallo virtuele machine worden uitgevoerd.

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> Zie voor aanvullende uitleg en configuratieopties Hallo **bouwen van uw opdrachtset** in sectie [toocreate gebruik Azure PowerShell en vooraf configureren van virtuele Machines op basis van Windows](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

## <a name="example-powershell-script"></a>Voorbeeld van de PowerShell-script

Hallo volgende script toont een voorbeeld van een volledige-script maakt een **RTM Enterprise van SQL Server 2016 op Windows Server 2012 R2** virtuele machine. Als u dit script gebruikt, moet u de initiële Hallo-variabelen op basis van de vorige stappen in dit onderwerp Hallo aanpassen.

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>Verbinding maken met extern bureaublad

1. Hallo RDP-bestanden op Hallo van de huidige gebruiker document map toolaunch deze toocomplete-setup van virtuele machines maken:

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. Start in de map documenten van Hallo Hallo RDP-bestand. Verbinding maken met de Hallo beheerdersgebruikersnaam en wachtwoord die eerder is verkregen (bijvoorbeeld, als uw gebruikersnaam VMAdmin, '\VMAdmin' opgeven als de gebruiker Hallo en Hallo wachtwoord opgeven).

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Configuratie voltooid Hallo Hallo Machine van SQL Server voor externe toegang

Na aanmelding toohello machine via Extern bureaublad configureren van SQL Server op basis van de instructies in Hallo [stappen voor het configureren van SQL-serververbindingen in een Azure VM](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm).

## <a name="next-steps"></a>Volgende stappen

U vindt aanvullende instructies voor het inrichten van virtuele machines met PowerShell in Hallo [documentatie virtual machines](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

In veel gevallen is de volgende stap Hallo toomigrate uw databases toothis nieuwe virtuele machine voor SQL Server. Zie voor instructies voor het migreren van database [migreren van een Database tooSQL Server op een Azure VM](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json).

Als u ook geïnteresseerd bent in met behulp van hello Azure portal toocreate virtuele Machines van SQL, raadpleegt u [inrichten van een virtuele Machine van SQL Server op Azure](../sql/virtual-machines-windows-portal-sql-server-provision.md). Houd er rekening mee dat Hallo-zelfstudie dat helpt die u bij het Hallo-portal maakt virtuele machines met Hallo aanbevolen Resource Manager-model, in plaats van klassieke Hallo-model in dit onderwerp PowerShell gebruikt.

Bovendien toothese resources, wordt aangeraden te controleren [andere onderwerpen gerelateerde toorunning SQL Server in Azure Virtual Machines](../sql/virtual-machines-windows-sql-server-iaas-overview.md).

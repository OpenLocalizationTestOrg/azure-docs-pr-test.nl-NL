---
title: aaaMigrating VMs tooAzure Premium-opslag | Microsoft Docs
description: Migreer uw bestaande virtuele machines tooAzure Premium-opslag. Premium-opslag biedt ondersteuning voor schijven voor hoge prestaties, lage latentie voor I/O-intensieve werkbelastingen die worden uitgevoerd op Azure Virtual Machines.
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Migreren tooAzure Premium-opslag (niet-beheerde schijven)

> [!NOTE]
> Dit artikel wordt beschreven hoe een virtuele machine die gebruikmaakt van niet-beheerde standaardschijven tooa VM die gebruikmaakt van toomigrate zonder begeleiding premium-schijven. U wordt aangeraden dat u Azure beheerd schijven gebruikt voor nieuwe virtuele machines en dat u uw vorige niet-beheerde schijven toomanaged schijven converteren. Schijven ingang Hallo onderliggende storage-accounts zodat u niet te hoeft worden beheerd. Zie voor meer informatie onze [schijven overzicht beheerde](../../virtual-machines/windows/managed-disks-overview.md).
>

Azure Premium-opslag biedt ondersteuning voor hoge prestaties, lage latentie schijven voor virtuele machines met I/O-intensieve werkbelastingen. U kunt profiteren van Hallo snelheid en prestaties van deze schijven nemen door te migreren van uw toepassing VM schijven tooAzure Premium-opslag.

Hallo-doel van deze handleiding is toohelp nieuwe gebruikers van betere Azure Premium-opslag voorbereiden toomake een overgang van hun huidige systeem tooPremium opslag. Hallo handleiding biedt drie van de belangrijke onderdelen Hallo in dit proces:

* [Hallo migratie tooPremium opslag plannen](#plan-the-migration-to-premium-storage)
* [Voorbereiden en kopieer virtuele harde schijven (VHD's) tooPremium opslag](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Premium-opslag met van Azure virtuele Machine maken](#create-azure-virtual-machine-using-premium-storage)

U kunt virtuele machines migreren van andere platforms tooAzure Premium-opslag of bestaande Azure-virtuele machines migreren van standaardopslag tooPremium opslag. Deze handleiding worden de stappen beschreven voor beide twee scenario's. Hallo stappen opgegeven in de relevante sectie hello, afhankelijk van uw scenario.

> [!NOTE]
> U vindt een overzicht van functies en prijzen van Premium-opslag in Premium-opslag: [krachtige opslag voor Azure Virtual Machine-werkbelasting](storage-premium-storage.md). Het is raadzaam om een hoge IOPS tooAzure Premium-opslag voor de beste prestaties voor uw toepassing hello vereisen schijf voor de virtuele machine migreren. Als de schijf niet hoge IOPS vereist, kunt u kosten beperken door handhaven standaardopslag die schijfgegevens voor virtuele machine op de harde schijven (HDD's) in plaats van SSD's opslaat.
>

Voltooien van het migratieproces Hallo in zijn geheel moet mogelijk extra acties vóór en na Hallo stappen in deze handleiding. Voorbeelden zijn virtuele netwerken of eindpunten configureren of u wijzigingen aanbrengt code vanuit Hallo toepassing zelf, waarin u mogelijk de enige downtime in uw toepassing. Deze acties zijn unieke tooeach toepassing en u ze samen met de stappen in deze handleiding toomake Hallo volledige overgang tooPremium opslag zo weinig mogelijk Hallo moet voltooien.

## <a name="plan-the-migration-to-premium-storage"></a>Hallo migratie tooPremium opslag plannen
Deze sectie zorgt ervoor dat u gereed toofollow Hallo migratiestappen in dit artikel, en u bij toomake Hallo beste beslissing op schijf en VM-typen helpt.

### <a name="prerequisites"></a>Vereisten
* U moet een Azure-abonnement. Als u niet hebt, kunt u één maand [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/) abonnement of gaat u naar [prijzen van Azure](https://azure.microsoft.com/pricing/) voor meer opties.
* tooexecute PowerShell-cmdlets, moet u Hallo Microsoft Azure PowerShell-module. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) installeren voor Hallo installatiepunt en de installatie-instructies.
* Wanneer u van plan toouse Azure VM's uitgevoerd op de Premium-opslag bent, moet u toouse Hallo Premium-opslag kunnen virtuele machines. Standaard- en Premium-opslag-schijven kunt u met Premium-opslag kunnen virtuele machines. Premium-opslag-schijven zijn beschikbaar met meer VM-typen in toekomstige Hallo. Zie voor meer informatie over alle beschikbare virtuele machine van Azure schijftypen en groottes [grootten voor virtuele machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) en [grootten voor Cloudservices](../../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Overwegingen
Een virtuele machine van Azure ondersteunt meerdere schijven met Premium-opslag koppelen zodat uw toepassingen van too256 TB opslagruimte per virtuele machine kunnen hebben. Met de Premium-opslag, kunnen uw toepassingen 80.000 IOP's (i/o-bewerkingen per seconde) per VM en 2000 MB per tweede schijfdoorvoer per virtuele machine met zeer lage latentie voor leesbewerkingen bereiken. Hebt u opties in tal van virtuele machines en de schijven. Deze sectie is toohelp toofind een optie die het beste past bij uw workload.

#### <a name="vm-sizes"></a>Formaten van virtuele machines
Hello Azure VM-grootte specificaties worden vermeld in [grootten voor virtuele machines](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Bekijk de prestatiekenmerken Hallo van virtuele machines die geschikt is voor Premium-opslag en kies Hallo meest geschikte VM-grootte die het beste past bij uw werkbelasting. Zorg ervoor dat er voldoende bandbreedte beschikbaar op uw VM toodrive Hallo schijf verkeer is.

#### <a name="disk-sizes"></a>Schijfformaten
Er zijn vijf typen schijven die kunnen worden gebruikt met uw virtuele machine en elke principal heeft bepaalde IOPs en doorvoerlimieten limieten. In overweging nemen deze limieten wanneer Hallo schijftype kiezen voor uw virtuele machine op basis van Hallo behoeften van uw toepassing in termen van capaciteit, prestaties, schaalbaarheid en piek wordt geladen.

| Premium-schijven Type  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Schijfgrootte           | 128 GB| 512 GB| 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| IOP's per schijf       | 500   | 2300  | 5000           | 7500           | 7500           | 
| Doorvoer per schijf | 100 MB per seconde | 150 MB per seconde | 200 MB per seconde | 250 MB per seconde | 250 MB per seconde |

Bepalen of extra gegevensschijven nodig zijn voor uw virtuele machine zijn afhankelijk van uw workload. U kunt verschillende permanente gegevens schijven tooyour VM koppelen. Indien nodig, kunt u via Hallo schijven tooincrease Hallo capaciteit en prestaties van Hallo volume stripe. (Zie Wat is er schijf Striping [hier](storage-premium-storage-performance.md#disk-striping).) Als u Premium-opslag gegevensschijven met stripe [opslagruimten][4], moet u deze configureren met één kolom voor elke schijf die wordt gebruikt. Anders hello algehele prestaties van Hallo striped volume mogelijk lager is dan verwacht vanwege toouneven distributie van verkeer over Hallo-schijven. Voor Linux VM's kunt u Hallo *mdadm* hulpprogramma tooachieve Hallo dezelfde. Zie het artikel [Software-RAID configureren op Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) voor meer informatie.

#### <a name="storage-account-scalability-targets"></a>Schaalbaarheidsdoelen van Storage-account
Premium-opslagaccounts hebben Hallo na schaalbaarheidsdoelen in toevoeging toohello [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md). Als uw toepassingsvereisten Hallo schaalbaarheidsdoelen van een enkele opslagaccount overschrijdt, bouwen van uw toepassing toouse meerdere opslagaccounts en partitioneren van uw gegevens over de storage-accounts.

| Capaciteit van de totale Account | Totale bandbreedte voor een Account met lokaal redundante opslag |
|:--- |:--- |
| Schijf capaciteit: 35TB<br />Momentopname maken van capaciteit: 10 TB |Up too50 gigabits per seconde voor inkomend en uitgaand |

Hallo voor meer informatie over specificaties voor Premium-opslag, Bekijk [Scalability and Performance Targets wanneer u Premium-opslag](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Het beleid voor schijf
Beleid voor de schijfcache is standaard *alleen-lezen* voor alle gegevensschijven Premium, Hallo en *lezen-schrijven* voor Hallo Premium besturingssysteemschijf gekoppeld toohello VM. Deze configuratieinstelling wordt aanbevolen tooachieve Hallo optimale prestaties voor uw toepassing IOs. Voor schijven schrijven zware of alleen-schrijven gegevens (zoals SQL Server-logboekbestanden), uitschakelen schijfcache, zodat u kunt betere prestaties bereiken. Hallo-cache-instellingen voor bestaande gegevensschijven kunnen worden bijgewerkt met behulp van [Azure Portal](https://portal.azure.com) of Hallo *- HostCaching* parameter Hallo *Set AzureDataDisk* cmdlet.

#### <a name="location"></a>Locatie
Kies een locatie waar Azure Premium-opslag beschikbaar is. Zie [Azure-Services per regio](https://azure.microsoft.com/regions/#services) voor actuele informatie over beschikbare locaties. Virtuele machines zich bevinden in Hallo dezelfde regio als Hallo Storage-account dat winkels schijven Hallo voor Hallo VM u veel betere prestaties krijgt dan als ze zich in afzonderlijke regio's.

#### <a name="other-azure-vm-configuration-settings"></a>Andere Azure VM-configuratie-instellingen
Wanneer u een virtuele machine in Azure maakt, zult u gevraagd tooconfigure bepaalde instellingen voor virtuele machine. Denk eraan dat enkele instellingen vast voor Hallo levensduur van Hallo VM, terwijl u kunt wijzigen of anderen later toevoegen. Deze configuratie-instellingen voor virtuele machine van Azure controleren en zorg ervoor dat ze zijn geconfigureerd op de juiste wijze toomatch de vereisten van uw werkbelasting.

### <a name="optimization"></a>Optimalisatie
[Azure Premium-opslag: Ontwerpen voor hoge prestaties](storage-premium-storage-performance.md) biedt richtlijnen voor het bouwen van krachtige toepassingen met behulp van Azure Premium-opslag. Hallo richtlijnen gecombineerd met de prestaties van best practices van toepassing tootechnologies gebruikt door de toepassing, kunt u volgen.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Voorbereiden en virtuele harde schijven (VHD's) tooPremium opslag kopiëren
Hallo volgende sectie bevat richtlijnen voor het voorbereiden van VHD's van uw virtuele machine en VHD's tooAzure Storage kopiëren.

* [Scenario 1: 'Ik ben migreren van bestaande virtuele machines in Azure tooAzure Premium-opslag."](#scenario1)
* [Scenario 2: 'Ik ben migreren VM's van andere platforms tooAzure Premium-opslag."](#scenario2)

### <a name="prerequisites"></a>Vereisten
tooprepare hello VHD's voor migratie, hebt u nodig:

* Een Azure-abonnement, een opslagaccount en een container in dat storage account toowhich kunt u uw VHD. Houd er rekening mee dat Hallo doelopslagaccount kan bestaan uit een Standard of Premium-opslag-account, afhankelijk van uw behoeften.
* Een hulpprogramma toogeneralize hello VHD als u van plan toocreate meerdere VM-exemplaren van deze bent. Bijvoorbeeld: sysprep voor Windows of virt-sysprep voor Ubuntu.
* Een hulpprogramma tooupload Hallo VHD-bestand toohello Storage-account. Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) of gebruik een [Azure Opslagverkenner](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Deze handleiding beschrijft de VHD met Hallo AzCopy hulpprogramma kopieert.

> [!NOTE]
> Als u ervoor de optie synchrone kopiëren met AzCopy, voor optimale prestaties kiest Kopieer uw VHD door een van deze hulpprogramma's van een Azure-virtuele machine die zich in Hallo dezelfde regio als doelopslagaccount Hallo. Als u een VHD van een Azure-virtuele machine in een andere regio kopieert, kan de prestaties van uw trager worden.
>
> Voor het kopiëren een grote hoeveelheid gegevens over beperkte bandbreedte, kunt u overwegen [hello Azure Import/Export-service tootransfer gegevens tooBlob opslag met](../storage-import-export-service.md); Hiermee kunt u tootransfer uw gegevens door back-ups van harde schijf tooan Azure-schijven Datacenter. U kunt hello Azure Import/Export-toocopy gegevens tooa standaardopslag serviceaccount alleen gebruiken. Nadat Hallo gegevens uw account standard-opslag is, kunt u beide Hallo [kopie Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) of AzCopy tootransfer Hallo gegevens tooyour premium storage-account.
>
> Houd er rekening mee dat Microsoft Azure biedt alleen ondersteuning voor VHD-bestanden van vaste grootte. VHDX-bestanden of dynamische virtuele harde schijven worden niet ondersteund. Als u een dynamische VHD hebt, kunt u deze converteren toofixed grootte Hallo met [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet.
>
>

### <a name="scenario1"></a>Scenario 1: 'Ik ben migreren van bestaande virtuele machines in Azure tooAzure Premium-opslag."
Als u migreert Azure virtuele machines, stop Hallo VM, bestaande virtuele harde schijven per Hallo type VHD die u wilt voorbereiden en kopieert u Hallo VHD met AzCopy of PowerShell.

Hallo VM moet toobe volledig omlaag toomigrate een oude toestand. Er zijn een uitvaltijd totdat Hallo migratie is voltooid.

#### <a name="step-1-prepare-vhds-for-migration"></a>Step 1. VHD's voorbereiden voor migratie
Als u een bestaande virtuele Azure-machines tooPremium opslag migreert, is uw VHD mogelijk:

* De installatiekopie van een gegeneraliseerde besturingssysteem
* Een unieke besturingssysteemschijf
* Een gegevensschijf

Hieronder doorlopen we deze 3 scenario's voor het voorbereiden van uw VHD.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Gebruik een gegeneraliseerde besturingssysteem-VHD toocreate meerdere VM-exemplaren
Als u een VHD die gebruikt toocreate worden uploadt meerdere algemene Azure VM-instanties, moet u eerst de VHD met een hulpprogramma sysprep generalize. Dit geldt tooa VHD on-premises of in de cloud Hallo. Sysprep verwijdert alle systeemspecifieke gegevens uit Hallo VHD.

> [!IMPORTANT]
> Een momentopname of back-up van uw VM voordat deze het generaliseren. Sysprep uitgevoerd worden gestopt en VM-instantie Hallo ongedaan gemaakt. Volg de stappen hieronder toosysprep een Windows-besturingssysteem-VHD. Houd er rekening mee dat Hallo Sysprep opdracht uit te voeren u tooshut omlaag Hallo virtuele machine moet. Zie voor meer informatie over Sysprep [Sysprep overzicht](http://technet.microsoft.com/library/hh825209.aspx) of [technische documentatie van Sysprep](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Open een opdrachtpromptvenster als administrator.
2. Voer Hallo opdracht tooopen Sysprep te volgen:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Selecteer in het hulpprogramma voor systeemvoorbereiding Hallo, selecteer System Voer Out of Box Experience (OOBE), selecteer Hallo Generalize of u het selectievakje **afsluiten**, en klik vervolgens op **OK**, zoals wordt weergegeven in onderstaande Hallo-afbeelding. Sysprep wordt generalize Hallo-besturingssysteem en Hallo-systeem afsluiten.

    ![][1]

Voor een VM Ubuntu Hallo gebruik virt sysprep tooachieve dezelfde. Zie [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) voor meer informatie. Zie ook een aantal van de open source Hallo [inrichten van Linux-servers software](http://www.cyberciti.biz/tips/server-provisioning-software.html) voor andere Linux-besturingssystemen.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Gebruik een unieke besturingssysteem-VHD toocreate één VM-exemplaar
Als u een toepassing die wordt uitgevoerd op Hallo VM waarvoor Hallo machine specifieke gegevens hebt, niet generalize Hallo VHD. Een VHD niet gegeneraliseerd mag gebruikte toocreate een uniek exemplaar van de virtuele machine van Azure. Bijvoorbeeld, als u een domeincontroller op uw VHD hebt, maakt sysprep wordt uitgevoerd het niet effectief als een domeincontroller. Bekijk Hallo toepassingen die worden uitgevoerd op uw virtuele machine en Hallo gevolgen van het sysprep erop worden uitgevoerd voordat het generaliseren van Hallo VHD.

##### <a name="register-data-disk-vhd"></a>Gegevensschijf VHD registreren
Als u gegevensschijven in Azure toobe gemigreerd, moet u ervoor dat Hallo virtuele machines die gebruikmaken van deze schijven worden afgesloten gegevens maken.

Volg de stappen Hallo hieronder toocopy VHD tooAzure Premium-opslag en registreren als een ingerichte gegevensschijf.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Stap 2. Hallo-doel voor de VHD maken
Een opslagaccount voor het onderhouden van uw VHD's maken. Hallo volgende punten bij het plannen van waar u rekening houden toostore uw VHD's:

* Hallo-doel Premium storage-account.
* Hallo opslagaccountlocatie moet hetzelfde zijn als Premium-opslag kunnen Azure virtuele machines in de laatste fase hello wordt gemaakt. U kan kopiëren tooa nieuw opslagaccount of plan toouse Hallo hetzelfde opslagaccount op basis van uw behoeften.
* Kopieer en sla de opslagaccountsleutel van doelopslagaccount Hallo Hallo voor de volgende fase Hallo.

Voor gegevensschijven, kunt u tookeep sommige gegevensschijven in een standard-opslagaccount (bijvoorbeeld schijven die koelervoorbeeld opslag), maar wij raden u alle gegevens voor productie werkbelasting toouse premium-opslag te verplaatsen.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>Stap 3. Kopieer de VHD met AzCopy of PowerShell
U moet toofind uw containerpad en storage account key tooprocess een van deze twee opties. Container pad en de opslagruimte accountsleutel vindt u in **Azure Portal** > **opslag**. URL van de opslagcontainer Hallo worden zoals 'https://myaccount.blob.core.windows.net/mycontainer/'.

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Optie 1: Kopieer geen VHD met AzCopy (asynchrone kopiëren)
AzCopy gebruikt, kunt u eenvoudig uploaden Hallo VHD via Hallo Internet. Dit kan tijd duren, afhankelijk van de grootte van de Hallo Hallo VHD's. Houd er rekening mee toocheck Hallo inkomend en uitgaand opslagaccountlimieten wanneer u deze optie. Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie.

1. Download en installeer AzCopy vanaf hier: [meest recente versie van AzCopy](http://aka.ms/downloadazcopy)
2. Open Azure PowerShell en ga toohello-map waarin AzCopy is geïnstalleerd.
3. Gebruik Hallo volgende opdracht toocopy Hallo VHD-bestand van 'Bron' te 'Bestemming'.

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Voorbeeld:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Hier volgen beschrijvingen van Hallo parameters gebruikt in Hallo AzCopy-opdracht:

   * **/ Bron:  *&lt;bron&gt;:***  locatie van het Hallo-map of URL van de opslagcontainer waarin Hallo VHD.
   * **/ SourceKey:  *&lt;bron accountsleutel&gt;:***  opslagaccountsleutel van Hallo bron storage-account.
   * **/ Dest:  *&lt;bestemming&gt;:***  opslag container URL toocopy Hallo VHD.
   * **/ DestKey:  *&lt;dest accountsleutel&gt;:***  opslagaccountsleutel van Hallo doelopslagaccount.
   * **/ Patroon:  *&lt;bestandsnaam&gt;:***  het Hallo-bestandsnaam opgeven van Hallo VHD toocopy.

Hulpprogramma voor meer informatie over het gebruik van AzCopy, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Optie 2: Kopieer geen VHD met PowerShell (Synchronized kopiëren)
U kunt ook Hallo VHD-bestand met Hallo PowerShell-cmdlet Start-AzureStorageBlobCopy kopiëren. Hallo volgende opdracht op Azure PowerShell toocopy VHD gebruiken. Hallo-waarden in <> vervangen door een overeenkomende waarden uit de bron- en storage-account. toouse dit uitvoert, moet u een zogenaamd VHD's in uw doelopslagaccount hebben. Als het Hallo-container bestaat niet, maken voordat Hallo opdracht uit te voeren.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Voorbeeld:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Scenario 2: 'Ik ben migreren VM's van andere platforms tooAzure Premium-opslag."
Als u een VHD van niet - Azure-Cloud-opslag tooAzure migreert, moet u eerst Hallo VHD tooa lokale directory te exporteren. Hallo voltooid bronpad van de lokale map Hallo waar VHD wordt opgeslagen bij de hand hebben en met behulp van AzCopy tooupload het tooAzure opslag.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>Step 1. Exporteren van VHD tooa lokale directory
##### <a name="copy-a-vhd-from-aws"></a>Kopieer geen VHD van AWS
1. Als u van AWS gebruikmaakt, exporteert u Hallo EC2 exemplaar tooa VHD in een Amazon S3-bucket. Volg de stappen Hallo in Hallo Amazon-documentatie voor exporteren Amazon EC2 exemplaren tooinstall Hallo Amazon EC2 opdrachtregelinterface (CLI) hulpprogramma en Hallo-exemplaar-export-taak maken opdracht tooexport Hallo EC2 exemplaar tooa VHD-bestand uit te voeren. Ervoor toouse worden **VHD** voor Hallo schijf &#95; INSTALLATIEKOPIE &#95; INDELING variabele bij het uitvoeren van Hallo **-exemplaar-export-taak maken** opdracht. Hallo wordt geëxporteerde VHD-bestand opgeslagen in Hallo Amazon S3-bucket die u tijdens dat proces opgeeft.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Hallo VHD-bestand downloaden van Hallo S3-bucket. Selecteer Hallo VHD-bestand, klikt u vervolgens **acties** > **downloaden**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Kopieer geen VHD van andere niet-Azure-cloud
Als u een VHD van niet - Azure-Cloud-opslag tooAzure migreert, moet u eerst Hallo VHD tooa lokale directory te exporteren. Kopieer Hallo voltooid bronpad van de lokale map Hallo waar de VHD wordt opgeslagen.

##### <a name="copy-a-vhd-from-on-premises"></a>Kopieer geen VHD van on-premises
Als u een VHD van een on-premises omgeving migreert, moet u volledige bronpad Hallo waar de VHD wordt opgeslagen. Hallo bronpad kan een server of bestandsshare worden.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Stap 2. Hallo-doel voor de VHD maken
Een opslagaccount voor het onderhouden van uw VHD's maken. Hallo volgende punten bij het plannen van waar u rekening houden toostore uw VHD's:

* Hallo doel storage-account kan worden standaard of premium-opslag, afhankelijk van uw vereisten voor toepassingsimplementatie.
* Hallo storage accountregio moet hetzelfde zijn als Premium-opslag kunnen Azure virtuele machines in de laatste fase hello wordt gemaakt. U kan kopiëren tooa nieuw opslagaccount of plan toouse Hallo hetzelfde opslagaccount op basis van uw behoeften.
* Kopieer en sla de opslagaccountsleutel van doelopslagaccount Hallo Hallo voor de volgende fase Hallo.

Wij raden u alle gegevens voor productie werkbelasting toouse premium-opslag te verplaatsen.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>Stap 3. Hallo VHD tooAzure opslag uploaden
Nu dat u uw VHD in de lokale directory Hallo hebt, kunt u AzCopy of AzurePowerShell tooupload Hallo .vhd-bestand tooAzure opslag. Beide opties vindt u hier:

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Optie 1: Met behulp van Azure PowerShell Add-AzureVhd tooupload Hallo .vhd-bestand

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Een voorbeeld <Uri> mogelijk ***'https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd'***. Een voorbeeld <FileInfo> mogelijk ***'C:\path\to\upload.vhd'***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Optie 2: Met behulp van AzCopy tooupload Hallo .vhd-bestand
AzCopy gebruikt, kunt u eenvoudig uploaden Hallo VHD via Hallo Internet. Dit kan tijd duren, afhankelijk van de grootte van de Hallo Hallo VHD's. Houd er rekening mee toocheck Hallo inkomend en uitgaand opslagaccountlimieten wanneer u deze optie. Zie [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md) voor meer informatie.

1. Download en installeer AzCopy vanaf hier: [meest recente versie van AzCopy](http://aka.ms/downloadazcopy)
2. Open Azure PowerShell en ga toohello-map waarin AzCopy is geïnstalleerd.
3. Gebruik Hallo volgende opdracht toocopy Hallo VHD-bestand van 'Bron' te 'Bestemming'.

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Voorbeeld:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Hier volgen beschrijvingen van Hallo parameters gebruikt in Hallo AzCopy-opdracht:

   * **/ Bron:  *&lt;bron&gt;:***  locatie van het Hallo-map of URL van de opslagcontainer waarin Hallo VHD.
   * **/ SourceKey:  *&lt;bron accountsleutel&gt;:***  opslagaccountsleutel van Hallo bron storage-account.
   * **/ Dest:  *&lt;bestemming&gt;:***  opslag container URL toocopy Hallo VHD.
   * **/ DestKey:  *&lt;dest accountsleutel&gt;:***  opslagaccountsleutel van Hallo doelopslagaccount.
   * **/ BlobType: pagina:** geeft aan dat Hallo-doel is een pagina-blob.
   * **/ Patroon:  *&lt;bestandsnaam&gt;:***  het Hallo-bestandsnaam opgeven van Hallo VHD toocopy.

Hulpprogramma voor meer informatie over het gebruik van AzCopy, Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Andere opties voor het uploaden van een VHD
U kunt ook een VHD tooyour storage-account met behulp van een Hallo na betekent uploaden:

* [API voor Azure Storage kopiëren-Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Azure Storage Explorer uploaden van BLOB 's](https://azurestorageexplorer.codeplex.com/)
* [Opslag voor importeren/exporteren Service REST API-verwijzing](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> U kunt het beste Import/Export-Service gebruikt als de geschatte tijd uploaden is langer dan zeven dagen. U kunt [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate Hallo tijd van de grootte en de overdracht van gegevenseenheid.
>
> Import/Export kan worden gebruikt toocopy tooa standard-opslagaccount. U moet toocopy van standaardopslag toopremium storage-account met behulp van een hulpprogramma zoals AzCopy.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Azure virtuele machines met Premium-opslag maken
Nadat Hallo VHD geüpload of gekopieerde toohello gewenst storage-account is, Hallo-instructies in deze sectie tooregister Hallo VHD volgen als een installatiekopie van het besturingssysteem, of de besturingssysteemschijf afhankelijk van uw scenario en maak een VM-instantie uit. Hallo gegevensschijf VHD kan worden aangesloten toohello VM zodra deze is gemaakt.
Een migratie voorbeeldscript wordt verstrekt aan Hallo einde van deze sectie. Dit eenvoudige script komt niet overeen met alle scenario's. U moet mogelijk tooupdate Hallo script toomatch met uw specifieke scenario. Hieronder vindt u de toosee als dit script geldt tooyour scenario [A migratie voorbeeldscript](#a-sample-migration-script).

### <a name="checklist"></a>Controlelijst
1. Wacht totdat alle Hallo VHD schijven kopiëren is voltooid.
2. Zorg ervoor dat de dat Premium-opslag is beschikbaar in Hallo-regio die u naar migreert.
3. Bepaal Hallo nieuwe VM-reeks die u gaat gebruiken. Dit moet een compatibele Premium-opslag en Hallo grootte moet zijn afhankelijk van beschikbaarheid in regio Hallo Hallo en op basis van uw behoeften.
4. Bepaal Hallo exacte VM-grootte die u wilt gebruiken. VM-grootte moet toobe groot genoeg toosupport Hallo aantal gegevensschijven dat u hebt. Bijvoorbeeld Als u 4 gegevensschijven hebt, moet Hallo VM 2 of hoger kernen hebben. Houd ook rekening met verwerkingskracht, geheugen en netwerkbandbreedte moet.
5. Hallo doelregio een Premium-opslag-account maken. Dit is Hallo account u voor Hallo gebruiken wilt nieuwe virtuele machine.
6. Informatie over een Hallo huidige VM handige, inclusief Hallo-lijst van schijven en de bijbehorende VHD-blobs.

Bereid uw toepassing uitvaltijd. toodo een schone migratie, hebt u toostop Hallo verwerking in de huidige systeem Hallo. Alleen dan kunt u dit downloaden tooconsistent staat die u kunt migreren toohello nieuwe platform. Duur van uitvaltijd afhankelijk Hallo hoeveelheid gegevens in Hallo schijven toomigrate.

> [!NOTE]
> Als u een Azure Resource Manager VM vanaf een speciale VHD schijf maakt, Raadpleeg te[deze sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) voor de implementatie van Resource Manager-VM met bestaande schijf.
>
>

### <a name="register-your-vhd"></a>Registreren van uw VHD
een virtuele machine van het besturingssysteem-VHD- of tooattach een schijf gegevens tooa toocreate nieuwe virtuele machine, moet u eerst registreren ze. Voer onderstaande stappen, afhankelijk van uw VHD-scenario.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Besturingssysteem-VHD toocreate gegeneraliseerd meerdere exemplaren van de virtuele machine in Azure
Nadat gegeneraliseerde installatiekopie van het besturingssysteem VHD is geüpload toohello storage-account, registreert u dit als een **Azure VM-installatiekopie** zodat u een of meer VM-exemplaren van deze maken kunt. Hallo volgende PowerShell-cmdlets tooregister uw VHD als de installatiekopie van een Azure VM-OS gebruiken. Hallo volledige container URL waar de VHD is gekopieerd naar opgeven.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Kopieer en sla Hallo-naam van deze nieuwe Azure VM-installatiekopie. In Hallo bovenstaande voorbeeld is het *OSImageName*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Unieke besturingssysteem-VHD toocreate slechts één exemplaar van de virtuele machine in Azure
Na het Hallo unieke OS VHD geüploade toohello opslag is account, registreert u dit als een **Azure Besturingssysteemschijf** zodat u een VM-exemplaar van deze maken kunt. Gebruik deze PowerShell-cmdlets tooregister uw VHD als een Besturingssysteemschijf Azure. Hallo volledige container URL waar de VHD is gekopieerd naar opgeven.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Kopieer en Hallo-naam van deze nieuwe OS-schijf van Azure worden opgeslagen. In Hallo bovenstaande voorbeeld is het *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Gegevens schijf VHD toobe toonew Azure VM-exemplaren die zijn gekoppeld
Nadat hello gegevensschijf VHD is geüpload toostorage account, registreren als een Azure-gegevensschijf zodat deze aangesloten tooyour worden kan nieuwe DS-serie DSv2 reeks of GS-serie Azure VM-instantie.

Gebruik deze PowerShell-cmdlets tooregister uw VHD als een Azure-gegevensschijf. Hallo volledige container URL waar de VHD is gekopieerd naar opgeven.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Kopieer en Hallo-naam van deze nieuwe Azure-gegevensschijf worden opgeslagen. In Hallo bovenstaande voorbeeld is het *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Maak een geschikt VM voor Premium-opslag
Eenmaal Hallo installatiekopie van het besturingssysteem of besturingssysteemschijf zijn geregistreerd, maakt u een nieuwe Active Directory-serie, DSv2-serie- of GS-serie VM. U gaat gebruiken de besturingssysteemkopie Hallo of naam van een besturingssysteem schijf die u hebt geregistreerd. Selecteer Hallo VM in Hallo Premium Storage-laag. In onderstaand voorbeeld gebruiken we Hallo *Standard_DS2* VM-grootte.

> [!NOTE]
> Hallo schijf grootte toomake zeker van te zijn dat deze overeenkomt met de capaciteit en prestatie-eisen en hello Azure schijfgrootten beschikbaar bijwerken.
>
>

Volg Hallo stapsgewijze PowerShell-cmdlets hieronder toocreate Hallo nieuwe virtuele machine. Stel eerst Hallo algemene parameters:

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

Maak eerst een cloudservice waarin u uw nieuwe virtuele machines worden gehost.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

Maak vervolgens hello Azure VM-instantie van Hallo installatiekopie van het besturingssysteem of Besturingssysteemschijf die u hebt geregistreerd, afhankelijk van uw scenario.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Besturingssysteem-VHD toocreate gegeneraliseerd meerdere exemplaren van de virtuele machine in Azure
Hallo maken een of meer nieuwe DS reeks Azure VM-instanties met Hallo **installatiekopie van het besturingssysteem Azure** die u hebt geregistreerd. Geef de naam van deze installatiekopie van het besturingssysteem in Hallo VM-configuratie bij het maken van nieuwe virtuele machine, zoals hieronder wordt weergegeven.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Unieke besturingssysteem-VHD toocreate slechts één exemplaar van de virtuele machine in Azure
Maak een nieuw Azure VM exemplaar voor DS reeks met behulp van Hallo **Besturingssysteemschijf Azure** die u hebt geregistreerd. Geef de naam van deze Besturingssysteemschijf Hallo VM-configuratie bij het maken van nieuwe virtuele machine Hallo zoals hieronder wordt weergegeven.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Geef andere Azure VM-informatie, zoals een cloudservice, regio, storage-account, beschikbaarheidsset en het beleid. Houd er rekening mee dat Hallo VM-instantie geplaatst met bijbehorende besturingssysteem worden moet of gegevensschijven zodat Hallo geselecteerd cloud-service, regio en storage-account moet zich in dezelfde locatie als onderliggende VHD's van deze schijven Hallo Hallo.

### <a name="attach-data-disk"></a>Een gegevensschijf koppelen
Ten slotte, als u hebt geregistreerd gegevens schijf VHD's, koppelt u ze toohello nieuwe Premium-opslag kan virtuele machine van Azure.

Gebruikt u de volgende PowerShell-cmdlet tooattach gegevens schijf toohello nieuwe virtuele machine en Hallo cachebeleid opgeven. In het voorbeeld hieronder Hallo cachebeleid is ingesteld te*ReadOnly*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Mogelijk zijn er extra stappen nodig toosupport uw toepassing die niet worden gedekt door deze handleiding.
>
>

### <a name="checking-and-plan-backup"></a>Controleren en back-up plannen
Eenmaal Hallo nieuwe virtuele machine actief is en die wordt uitgevoerd, toegang met behulp van dezelfde gebruikersnaam en wachtwoord Hallo is als de oorspronkelijke VM Hallo en controleren of alles werkt zoals verwacht. Alle Hallo-instellingen, inclusief Hallo striped volumes, moeten aanwezig zijn in Hallo van nieuwe virtuele machine.

de laatste stap Hallo is tooplan back-up en onderhoud planning voor de nieuwe virtuele machine op basis van de behoeften van de toepassing hello Hallo.

### <a name="a-sample-migration-script"></a>Een voorbeeldscript voor migratie
Als u meerdere virtuele machines toomigrate hebt, wordt de automation via PowerShell-scripts nuttig zijn. Hier volgt een voorbeeld van een script waarmee Hallo migratie van een virtuele machine worden geautomatiseerd. Opmerking die onderstaand script is slechts een voorbeeld en er zijn enkele veronderstellingen over Hallo huidige VM-schijven. U moet mogelijk tooupdate Hallo script toomatch met uw specifieke scenario.

Hallo veronderstellingen zijn:

* Klassieke Azure-VM's die u maakt.
* Uw bron OS schijven en de gegevensschijven van de bron zich in hetzelfde opslagaccount en in dezelfde container. Als de OS-schijven en de gegevensschijven zich niet op dezelfde Hallo plaatst, kunt u AzCopy of Azure PowerShell toocopy VHD's via de storage-accounts en containers. Raadpleeg de vorige stap toohello: [kopie VHD met AzCopy of PowerShell](#copy-vhd-with-azcopy-or-powershell). Dit script toomeet bewerken uw scenario is een andere keuze, maar we raden via AzCopy of PowerShell nadat het is eenvoudiger en sneller.

Hieronder vindt u Hallo automatiseringsscript. Tekst vervangen door uw gegevens en Hallo script toomatch werk met uw specifieke scenario.

> [!NOTE]
> Met behulp van de bestaande script Hallo behoudt niet Hallo netwerkconfiguratie van de bron-VM. U moet toore-config Hallo netwerkinstellingen op de gemigreerde virtuele machines.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>Optimalisatie
Uw huidige configuratie van de virtuele machine kan worden aangepast specifiek toowork goed met standaardschijven. Bijvoorbeeld: tooincrease Hallo prestaties met behulp van veel schijven in striped volumes. Bijvoorbeeld, in plaats van 4 schijven afzonderlijk op Premium-opslag, mogelijk kunnen toooptimize Hallo kosten doordat één schijf. Optimalisaties zoals dit moet toobe verwerkt op basis van geval tot geval en aangepaste stappen na de migratie Hallo nodig. Merk ook op dit proces werkt niet goed voor databases en toepassingen die afhankelijk van Hallo schijfindeling gedefinieerd in het Hallo-installatieprogramma zijn.

##### <a name="preparation"></a>Voorbereiding
1. Volledige Hallo eenvoudige migratie, zoals beschreven in Hallo eerder gedeelte. Optimalisaties wordt uitgevoerd op Hallo nieuwe virtuele machine na migratie Hallo.
2. Definieer Hallo nieuwe schijfgrootten nodig voor de configuratie van Hallo geoptimaliseerd.
3. Toewijzing van Hallo huidige schijven/volumes toohello nieuwe schijf specificaties bepalen.

##### <a name="execution-steps"></a>De stappen worden uitgevoerd
1. Hallo nieuwe schijven met de juiste Hallo grootte op Hallo VM voor Premium-opslag beschikbaar maken.
2. Aanmelding toohello VM en Hallo gegevens kopiëren van Hallo huidige volume toohello nieuwe schijf die is toegewezen toothat volume. Doe dit voor alle Hallo huidige volumes die toomap tooa nieuwe schijf nodig.
3. Vervolgens wijzigen Hallo toepassing instellingen tooswitch toohello nieuwe schijven en Hallo oude volumes loskoppelen.

Voor het afstemmen Hallo-toepassing voor betere prestaties van de schijf, Raadpleeg te[toepassingsprestaties optimaliseren](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Migraties van toepassing
Databases en andere complexe toepassingen mogelijk speciale stappen zoals gedefinieerd door Hallo toepassingsprovider voor Hallo-migratie. Raadpleeg de documentatie van de toepassing toorespective. Bijvoorbeeld doorgaans databases kunnen worden gemigreerd door middel van de back-up en herstel.

## <a name="next-steps"></a>Volgende stappen
Zie Hallo resources voor specifieke scenario's voor het migreren van virtuele machines te volgen:

* [Azure virtuele Machines tussen Opslagaccounts migreren](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Maken en uploaden van een Windows Server-VHD tooAzure.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Maakt en uploadt u een virtuele harde schijf met Hallo Linux-besturingssysteem](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migreren van virtuele Machines van Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Zie ook Hallo resources toolearn meer informatie over Azure Storage en Azure Virtual Machines te volgen:

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Virtuele Machines in Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Premium Storage: opslag met hoge prestaties voor de werkbelasting van virtuele Azure-machines](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx

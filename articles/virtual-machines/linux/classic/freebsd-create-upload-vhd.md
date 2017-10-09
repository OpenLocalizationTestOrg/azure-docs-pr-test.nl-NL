---
title: aaaCreate en het uploaden van een FreeBSD VM image | Microsoft Docs
description: Informatie over toocreate en het uploaden van een virtuele harde schijf (VHD) die Hallo FreeBSD besturingssysteem toocreate Azure een virtuele machine bevat
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Maken en een tooAzure FreeBSD VHD uploaden
Dit artikel laat zien hoe Hallo besturingssysteem FreeBSD toocreate en het uploaden van een virtuele harde schijf (VHD) die bevat. Nadat u deze uploaden, kunt u deze kunt gebruiken als uw eigen toocreate installatiekopie van een virtuele machine (VM) in Azure.

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Zie voor meer informatie over het uploaden van een VHD met Resource Manager-model Hallo [hier](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Vereisten
In dit artikel wordt ervan uitgegaan dat u hebt Hallo volgende items:

* **Een Azure-abonnement**--als u geen account hebt, kunt u een in een paar minuten. Als u een MSDN-abonnement hebt, raadpleegt u [maandelijkse Azure-tegoed voor Visual Studio-abonnees](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). Anders wordt informatie over hoe te[maken van een gratis proefaccount](https://azure.microsoft.com/pricing/free-trial/).  
* **Azure PowerShell-hulpprogramma's**--hello Azure PowerShell-module moet worden geïnstalleerd en geconfigureerd toouse uw Azure-abonnement. toodownload Hallo-module, Zie [Azure downloadt](https://azure.microsoft.com/downloads/). Een zelfstudie waarin wordt beschreven hoe tooinstall en configureer Hallo-module is hier beschikbaar. Gebruik Hallo [Azure downloadt](https://azure.microsoft.com/downloads/) cmdlet tooupload Hallo VHD.
* **FreeBSD-besturingssysteem is geïnstalleerd in een .vhd-bestand**--er is een ondersteund besturingssysteem voor FreeBSD moet tooa virtuele hardeschijf geïnstalleerd. Meerdere hulpprogramma's bestaan toocreate VHD-bestanden. U kunt bijvoorbeeld een oplossing voor netwerkvirtualisatie gebruiken zoals Hyper-V toocreate Hallo .vhd-bestand en Hallo-besturingssysteem installeren. Voor instructies over hoe tooinstall en het gebruik van Hyper-V, Zie [Hyper-V installeren en een virtuele machine maken](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> Hallo nieuwere VHDX-indeling wordt niet ondersteund in Azure. U kunt converteren Hallo tooVHD schijfindeling met behulp van Hyper-V-beheer of cmdlet Hallo [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Er is bovendien een [zelfstudie in MSDN over het toouse FreeBSD met Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Deze taak omvat Hallo vijf stappen te volgen:

## <a name="step-1-prepare-hello-image-for-upload"></a>Stap 1: Voorbereiden Hallo installatiekopie uploaden
Voer op Hallo virtuele machine waar u Hallo FreeBSD besturingssysteem hebt geïnstalleerd, Hallo procedures te volgen:

1. Schakel DHCP in.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. SSH inschakelen.

    Zorg ervoor dat Hallo SSH-server is geïnstalleerd en geconfigureerd toostart tijdens het opstarten. Dit is standaard ingeschakeld na de installatie van FreeBSD schijf. 
3. Instellen van een seriële console.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Sudo installeren.

    Hallo root-account is uitgeschakeld in Azure. Dit betekent dat u tooutilize sudo uit een onbevoegde gebruiker toorun-opdrachten met verhoogde bevoegdheden nodig.

        # pkg install sudo
   
5. Vereisten voor Azure-Agent.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Azure-Agent installeren.

    Hallo meest recente versie van hello Azure-Agent altijd vindt u op [github](https://github.com/Azure/WALinuxAgent/releases). Hallo versie 2.0.10 + officieel ondersteunt FreeBSD 10 & 10.1 en Hallo versie 2.1.4 + (inclusief 2.2.x) officieel ondersteunt FreeBSD 10.2 en latere versies.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    Gebruik voor 2.0, gaan we 2.0.16 als een voorbeeld:

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    2.1, gaan we gebruik 2.1.4 als voor een voorbeeld:

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Nadat u Azure-Agent hebt geïnstalleerd, is het een goed idee tooverify dat deze wordt uitgevoerd:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Inrichting ervan ongedaan Hallo-systeem.

    Identiteitsgegevens Hallo system tooclean deze en maak deze geschikt is voor reprovisioning. Hallo volgende opdracht ook verwijderd Hallo laatste ingerichte gebruiker serviceaccount en Hallo die zijn gekoppeld:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    U kunt nu uw virtuele machine afsluiten.

## <a name="step-2-create-a-storage-account-in-azure"></a>Stap 2: Een opslagaccount maken in Azure
U moet een opslagaccount in Azure tooupload een .vhd-bestand, zodat deze gebruikt toocreate een virtuele machine worden kan. U kunt hello Azure classic portal toocreate storage-account gebruiken.

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer op de opdrachtbalk Hallo **nieuw**.
3. Selecteer **gegevensservices** > **opslag** > **snelle invoer**.

    ![Snel een opslagaccount maken](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Vul de velden Hallo als volgt in:

   * In Hallo **URL** veld, typt u een subdomein naam toouse in Hallo storage account-URL. Hallo-vermelding kan van 3 tot 24 cijfers en kleine letters bevatten. Deze naam wordt Hallo hostnaam binnen Hallo-URL die is gebruikt tooaddress Azure Blob storage, Azure Queue storage of Azure Table storage-resources voor Hallo-abonnement.
   * In Hallo **locatie/Affiniteitsgroep** vervolgkeuzelijst, kies Hallo **locatie of affiniteitsgroep** voor Hallo storage-account. Een affiniteitsgroep kunt u uw cloud-services en opslag in Hallo plaatst hetzelfde Datacenter.
   * In Hallo **replicatie** veld, besluiten of toouse **geografisch redundante** replicatie voor het Hallo-opslagaccount. Geo-replicatie is standaard ingeschakeld. Deze optie uw gegevens tooa secundaire locatie, er zijn geen kosten tooyou repliceert, zodat uw opslag wordt overgenomen toothat locatie als een storing optreedt op Hallo primaire locatie. Hallo secundaire locatie wordt automatisch toegewezen en kan niet worden gewijzigd. Als u meer controle over het Hallo-locatie van de cloud-gebaseerde opslag vervaldatum toolegal vereisten of organisatie beleid nodig hebt, kunt u geo-replicatie kunt uitschakelen. Echter wel rekening dat als u later geo-replicatie inschakelt, wordt u gefactureerd eenmalig kosten tooreplicate van gegevensoverdracht uw bestaande gegevens toohello secundaire locatie. Storage-services zonder geo-replicatie worden aangeboden met korting. Meer informatie over het beheren van geo-replicatie van opslagaccounts vindt u hier: [Azure Storage-replicatie](../../../storage/common/storage-redundancy.md).

     ![Voer de details van opslag](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Selecteer **Storage-Account maken**. Hallo account wordt nu weergegeven onder **opslag**.

    ![Storage-account is gemaakt](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Maak vervolgens een container voor uw geüploade VHD-bestanden. Selecteer de opslagaccountnaam hello, en selecteer vervolgens **Containers**.

    ![Details van de Storage-account](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Selecteer **maken van een Container**.

    ![Details van de Storage-account](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. In Hallo **naam** veld, typ een naam voor de container. Klik op Hallo **toegang** vervolgkeuzelijst, selecteer welk type toegangsbeleid dat u wilt.

    ![Containernaam](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > Standaard Hallo container privé is en alleen toegankelijk zijn voor de accounteigenaar Hallo. tooallow openbare leestoegang toohello blobs in de container hello, maar niet de eigenschappen van toohello-container en metagegevens gebruiken Hallo **openbare Blob** optie. tooallow volledige openbare leestoegang voor hello container en blobs, Hallo **openbare Container** optie.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Stap 3: Hallo verbinding tooAzure voorbereiden
Voordat u een .vhd-bestand uploadt kunt, moet u tooestablish een beveiligde verbinding tussen uw computer en uw Azure-abonnement. U kunt gebruiken hello Azure Active Directory (Azure AD)-methode of Hallo certificaat methode toodo deze.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Hello Azure AD-methode tooupload een .vhd-bestand gebruiken
1. Open hello Azure PowerShell-console.
2. Type Hallo volgende opdracht:  
    `Add-AzureAccount`

    Deze opdracht opent een aanmeldingspagina-venster waar u zich met uw werk- of schoolaccount aanmelden kunt.

    ![PowerShell-venster](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure worden geverifieerd en Hallo referentie-informatie wordt opgeslagen. Vervolgens wordt Hallo-venster gesloten.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Hallo certificaat methode tooupload een .vhd-bestand gebruiken
1. Open hello Azure PowerShell-console.
2. Type: `Get-AzurePublishSettingsFile`.
3. Een browservenster wordt geopend en vraagt u toodownload hello .publishsettings-bestand. Dit bestand bevat informatie en een certificaat voor uw Azure-abonnement.

    ![Browser-downloadpagina](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Hallo .publishsettings-bestand opslaan.
5. Type: `Import-AzurePublishSettingsFile <PathToFile>`, waarbij `<PathToFile>` Hallo volledig pad toohello .publishsettings-bestand is.

   Zie voor meer informatie [aan de slag met Azure-cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).

   Zie voor meer informatie over het installeren en configureren van PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Stap 4: Hallo .vhd-bestand uploaden
Wanneer u Hallo .vhd-bestand uploadt, kunt u deze overal opnemen in de Blob-opslag. Hieronder volgen enkele termen die u bij het Hallo-bestand te uploaden:

* **BlobStorageURL** Hallo-URL voor Hallo storage-account die u in stap 2 hebt gemaakt.
* **YourImagesFolder** Hallo-container in Blob-opslag is waar u toostore uw afbeeldingen.
* **VHDName** Hallo-label die wordt weergegeven in hello Azure classic portal tooidentify Hallo virtuele harde schijf.
* **PathToVHDFile** Hallo volledig pad en naam van Hallo .vhd-bestand.

U hebt gebruikt in de vorige stap Hallo hello Azure PowerShell-venster, typ:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Stap 5: Een virtuele machine maken met de Hallo geüploade .vhd-bestand
Nadat u Hallo .vhd-bestand uploadt, kunt u deze toevoegen als een lijst met afbeeldingen toohello van aangepaste installatiekopieën die zijn gekoppeld aan uw abonnement en een virtuele machine maken met deze aangepaste installatiekopie.

1. U hebt gebruikt in de vorige stap Hallo hello Azure PowerShell-venster, typ:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Linux gebruiken als Hallo BS-type. de huidige Azure PowerShell-versie Hallo accepteert alleen 'Linux' of 'Windows' als parameter.
   >
   >
2. Nadat u de vorige stappen hello, Hallo nieuwe installatiekopie wordt weergegeven wanneer u ervoor Hallo kiest **installatiekopieën** tabblad op Hallo klassieke Azure-portal.  

    ![Een afbeelding kiezen](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Een virtuele machine maken vanuit Hallo-galerie. Deze nieuwe installatiekopie is nu beschikbaar onder **Mijn afbeeldingen**.
4. Hallo nieuwe installatiekopie selecteren. Ga vervolgens door Hallo prompts tooset van een hostnaam, een wachtwoord, een SSH-sleutel, enzovoort.

    ![Aangepaste installatiekopie](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Nadat u het Hallo-inrichting hebt voltooid, ziet u uw FreeBSD VM worden uitgevoerd in Azure.

    ![Afbeelding van FreeBSD in azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)

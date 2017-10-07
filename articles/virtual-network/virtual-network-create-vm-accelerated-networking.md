---
title: een virtuele machine van Azure met versnelde toegang aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtuele machine met versnelde netwerken.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/10/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 241362891bfe083ab32c2f558be54f63f87c0693
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-accelerated-networking"></a>Een virtuele machine met versnelde toegang maken

In deze zelfstudie leert u hoe een Azure-virtuele Machine (VM) met versnelde toegang toocreate. Versnelde netwerken wordt GA voor Windows en een openbare Preview voor specifieke Linux-distributies. Versnelde netwerken kan één hoofdelement i/o-virtualisatie (SR-IOV) tooa VM, aanzienlijk verbeteren de prestaties van netwerken. Dit pad krachtige omzeilt Hallo host Hallo gegevenspad waardoor latentie en jitter CPU-gebruik, voor gebruik met Hallo zwaarste netwerkbelasting op ondersteunde VM-typen. Hallo volgende afbeelding toont communicatie tussen twee virtuele machines (VM) met en zonder versnelde netwerken:

![Vergelijking](./media/virtual-network-create-vm-accelerated-networking/image1.png)

Alle netwerkverkeer naar en vanuit Hallo VM moet zonder versnelde netwerken passeren Hallo host en Hallo virtuele switch. Hallo-switch biedt alle afdwingen van beleid, zoals zoals beveiligingsgroepen, het netwerk toegang tot toegangsbeheerlijsten-, isolatie- en andere gevirtualiseerd services toonetwork netwerkverkeer. meer informatie over virtuele switches, Hallo lezen toolearn [Hyper-V-netwerkvirtualisatie en virtuele switch](https://technet.microsoft.com/library/jj945275.aspx) artikel.

Met versnelde netwerken netwerkverkeer binnenkomt op Hallo van de virtuele machine netwerkinterface (NIC) en wordt vervolgens doorgestuurd toohello VM. Alle netwerkbeleid dat Hallo virtuele switch wordt toegepast zonder versnelde netwerken worden ge-offload en toegepast in hardware. Toepassen van beleid in hardware schakelt Hallo NIC tooforward netwerkverkeer rechtstreeks toohello VM, het omzeilen van Hallo-host en Hallo virtuele switch, terwijl alle Hallo beleid wordt toegepast in Hallo host.

Hallo voordelen van versnelde netwerken alleen van toepassing toohello VM die is ingeschakeld. Voor de beste resultaten hello, is het ideaal tooenable deze functie op ten minste twee virtuele machines verbonden toohello dezelfde Azure Virtual Network (VNet). Tijdens de communicatie tussen VNets of verbindende on-premises, heeft dit onderdeel minimale gevolgen toooverall latentie.

> [!WARNING]
> Deze Linux Public Preview mogelijk geen Hallo zijn van hetzelfde niveau van beschikbaarheid en betrouwbaarheid als functies beschreven die in het algemeen beschikbaarheid vrijgeven. Hallo-functie wordt niet ondersteund, kan hebben beperkte mogelijkheden en mogelijk niet beschikbaar in alle Azure-locaties. Meest recente meldingen Hallo niet op de beschikbaarheid en de status van deze functie, Controleer pagina hello Azure Virtual Network-updates.

## <a name="benefits"></a>Voordelen
* **Lagere latentie / hoger pakketten per seconde (pps):** verwijderen Hallo virtuele switch van Hallo gegevenspad verwijdert Hallo tijd te besteden aan de pakketten in Hallo host voor de verwerking van beleid en toeneemt Hallo aantal pakketten dat kan worden verwerkt binnen Hallo VM.
* **Minder jitter:** virtuele switch verwerking is afhankelijk van de vraag Hallo hoeveelheid beleid die behoeften toobe toegepast en Hallo werkbelasting Hallo CPU die Hallo verwerking doet. Offloading van Hallo beleid afdwingen toohello hardware verwijdert die variabiliteit door het leveren van pakketten direct toohello VM, Hallo host tooVM communicatie en alle software-interrupts en context verwijderd verandert.
* **CPU-gebruik verlaagd:** Bypassing Hallo virtuele switch op de host Hallo leidt tooless CPU-gebruik voor het verwerken van netwerkverkeer.

## <a name="Limitations"></a>Beperkingen
Hallo volgen beperkingen bestaan wanneer deze wordt met deze mogelijkheid:

* **Interface maken van een netwerk:** Accelerated netwerken kan alleen worden ingeschakeld voor een nieuwe NIC. Deze kan niet worden ingeschakeld voor een bestaande NIC.
* **Maken van VM:** een NIC met versnelde netwerken ingeschakeld kan slechts worden aangesloten tooa VM wanneer hello virtuele machine wordt gemaakt. Hallo NIC mag geen gekoppelde tooan bestaande virtuele machine.
* **Gebieden:** Windows virtuele machines met versnelde netwerken worden aangeboden in de meeste Azure-regio's. Virtuele Linux-machines met versnelde netwerken worden aangeboden in meerdere regio's. Deze mogelijkheid is beschikbaar in Hallo-regio's is uitgebreid. Zie de blog onder Azure virtuele netwerken Updates voor de meest recente informatie Hallo Hallo.   
* **Ondersteunde besturingssystemen:** Windows: Microsoft Windows Server 2012 R2 Datacenter- en Windows Server 2016. Linux: Ubuntu Server 16.04 TNS met kernel 4.4.0-77 of hoger, SLES 12 SP2, RHEL 7.3 en CentOS 7.3 (gepubliceerd door 'Rogue Wave Software').
* **VM-grootte:** algemeen en de grootte van de compute-geoptimaliseerde exemplaar met acht of meer cores. Zie voor meer informatie, Hallo [Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) en [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) VM-groottes artikelen. Hallo wordt set ondersteunde grootten voor VM-exemplaar uitgebreid in toekomstige Hallo.
* **Implementatie via Azure Resource Manager (ARM) alleen:** versnelde toegang is niet beschikbaar voor implementatie via ASM/RDFE.

Wijzigingen toothese beperkingen zijn aangekondigd door Hallo [virtuele netwerken van Azure updates](https://azure.microsoft.com/updates/accelerated-networking-in-preview) pagina.

## <a name="create-a-windows-vm"></a>Een Windows-VM maken
U kunt hello Azure-portal of Azure [PowerShell](#windows-powershell) toocreate Hallo VM.

### <a name="windows-portal"></a>Portal

1. Open in een internetbrowser hello Azure [portal](https://portal.azure.com) en meld u aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Klik in de portal Hallo op **+ nieuw** > **Compute** > **Windows Server 2016 Datacenter**. 
3. In Hallo **Windows Server 2016 Datacenter** blade die wordt weergegeven, laat de eigenschap *Resource Manager* geselecteerde onder **een implementatiemodel selecteren**, en klik op **maken** .
4. In Hallo **basisbeginselen** blade die wordt weergegeven, Voer Hallo waarden te volgen, laat Hallo resterende standaardopties of selecteren of uw eigen waarden en klikt u op Hallo **OK** knop:

    |Instelling|Waarde|
    |---|---|
    |Naam|MyVm|
    |Resourcegroep|Laat **nieuw** geselecteerd en voer *MyResourceGroup*|
    |Locatie|VS - west 2|

    Als u nieuwe tooAzure, meer informatie over [resourcegroepen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [abonnementen](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), en [locaties](https://azure.microsoft.com/regions) (tooas regio's zijn ook genoemd).
5. In Hallo **een grootte kiezen** blade die wordt weergegeven, invoeren *8* in Hallo **Minimum kernen** vak en klik vervolgens op **weergeven van alle**.
6. Klik op **DS4_V2 standaard**, of een ondersteunde VM, klikt u op Hallo **Selecteer** knop.
7. In Hallo **instellingen** blade die wordt weergegeven, laat u alle instellingen als-is, met uitzondering van Klik **ingeschakeld** onder **versnelde netwerken**, klikt u vervolgens op Hallo **OK** knop. **Opmerking:** als, in de vorige stappen hebt u waarden voor VM-grootte, besturingssysteem of locatie die niet zijn opgenomen in Hallo geselecteerd [beperkingen](#Limitations) sectie van dit artikel **Accelerated netwerken**niet zichtbaar is.
8. In Hallo **samenvatting** blade die wordt weergegeven, klikt u op Hallo **OK** knop. Azure begint Hallo VM maken. Maken van VM duurt een paar minuten.
9. tooinstall Hallo-netwerkstuurprogramma versnelde voor Windows, volledige Hallo stappen voor het Hallo [Windows configureren](#configure-windows) sectie van dit artikel.

### <a name="windows-powershell"></a>PowerShell
1. Installeer de nieuwste versie Hallo van hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, lezen Hallo [overzicht van Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.
2. Een PowerShell-sessie starten door te klikken op de knop Start van Windows hello typen **powershell**, vervolgens te klikken op **PowerShell** van Hallo zoekresultaten.
3. Voer in het PowerShell-venster Hallo `login-azurermaccount` opdracht toosign aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
4. In uw browser kopiëren Hallo script volgen:
    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Windows `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName MicrosoftWindowsServer `
      -Offer WindowsServer `
      -Skus 2016-Datacenter `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    #
    ```
5. Met de rechtermuisknop op toopaste Hallo script en beginnen met de uitvoering van deze in uw PowerShell-venster. U wordt gevraagd om een gebruikersnaam en wachtwoord. Deze referenties toolog in toohello VM gebruiken bij het verbinden van tooit in de volgende stap Hallo. Als Hallo script mislukt en u de waarden in de script Hallo gewijzigd voordat deze wordt uitgevoerd, bevestig Hallo-waarden die u voor VM-grootte, besturingssysteem gebruikt, en locatie staan in Hallo [beperkingen](#Limitations) sectie van dit artikel.
6. tooinstall Hallo-netwerkstuurprogramma versnelde voor Windows, volledige Hallo stappen voor het Hallo [Windows configureren](#configure-windows) sectie van dit artikel.

### <a name="configure-windows"></a>Windows configureren
Zodra u Hallo VM in Azure maakt, moet u Hallo versnelde-netwerkstuurprogramma installeren voor Windows. Voordat u Hallo stappen te volgen, moet u een virtuele Windows-machine gemaakt met versnelde netwerken met behulp van beide Hallo [portal](#windows-portal) of [PowerShell](#windows-powershell) stappen in dit artikel. 

1. Open in een internetbrowser hello Azure [portal](https://portal.azure.com) en meld u aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
2. In Hallo vak waarin tekst hello *zoeken bronnen* bovenaan Hallo hello Azure-portal, typ *MyVm*. Wanneer **MyVm** wordt weergegeven in zoekresultaten hello, klik erop.
3. In Hallo **MyVm** blade die wordt weergegeven, klikt u op Hallo **Connect** knop in Hallo linksboven Hallo-blade. **Opmerking:** als **maken** zichtbaar onder Hallo **Connect** knop Azure is nog niet voltooid Hallo VM maken. Klik op **Connect** pas nadat u niet meer zien **maken** onder Hallo **Connect** knop.
4. Uw browser toodownload Hallo toestaan **MyVm.rdp** bestand.  Nadat u hebt gedownload, klikt u op Hallo bestand tooopen deze. 
5. Klik op Hallo **Connect** knop in Hallo **verbinding met extern bureaublad** vak dat wordt weergegeven, meegedeeld dat Hallo uitgever van Hallo externe verbinding kan niet worden vastgesteld.
6. In Hallo **Windows-beveiliging** dat verschijnt, klikt u op **meer opties**, klikt u vervolgens op **gebruik een ander account**. Hallo-gebruikersnaam en wachtwoord die u hebt opgegeven in stap 4 invoeren, en klik vervolgens op Hallo **OK** knop.
7. Klik op Hallo **Ja** knop in Hallo verbinding met extern bureaublad-vak dat wordt weergegeven om u te informeren dat de identiteit van de externe computer Hallo Hallo kan niet worden geverifieerd.
8. Met de rechtermuisknop op de knop Start van Windows hello en klik op **Apparaatbeheer**. Vouw Hallo **netwerkadapters** knooppunt. Bevestig dat Hallo **Mellanox ConnectX 3 virtuele functie Ethernet-Adapter** wordt weergegeven, zoals wordt weergegeven in de volgende afbeelding Hallo:
   
    ![Apparaatbeheer](./media/virtual-network-create-vm-accelerated-networking/image2.png)

9. Versnelde netwerken is nu ingeschakeld voor uw virtuele machine.

## <a name="create-a-linux-vm"></a>Een Linux-VM maken
U kunt hello Azure-portal of Azure [PowerShell](#linux-powershell) toocreate een Ubuntu of SLES VM. Er is een andere werkstroom voor RHEL en CentOS virtuele machines.  Zie de onderstaande Hallo-instructies.

### <a name="linux-portal"></a>Portal
1. Registreren voor Hallo versnelde netwerken voor Linux-preview via stappen 1-5 Hallo [maken van een Linux-VM - PowerShell](#linux-powershell) sectie van dit artikel.  U registreren niet voor preview Hallo in Hallo-portal.
2. Volledige stappen 1-8 in Hallo [maken van een Windows-VM - portal](#windows-portal) sectie van dit artikel. Klik in stap 2 op **Ubuntu Server 16.04 LTS** in plaats van **Windows Server 2016 Datacenter**. Voor deze zelfstudie kiest toouse een wachtwoord, in plaats van een SSH-sleutel al is voor productie-implementaties, gebruikt u een. Als **versnelde netwerken** wordt niet weergegeven wanneer u bij het voltooien van stap 7 van Hallo [maken van een Windows-VM - portal](#windows-portal) sectie van dit artikel, is het waarschijnlijk voor een van de volgende redenen Hallo:
    - U nog niet zijn geregistreerd voor Hallo preview. Controleer of de status van uw registratie **geregistreerde**, zoals wordt beschreven in stap 4 van Hallo [maken van een Linux-VM - Powershell](#linux-powershell) sectie van dit artikel. **Opmerking:** als u hebt deelgenomen aan Hallo Accelerated netwerken voor VM's van Windows-preview (het niet langer nodig tooregister toouse versnelde netwerken voor Windows-VM's), u worden niet automatisch geregistreerd voor Hallo Accelerated voor netwerken Voorbeeld van de virtuele Linux-machines. U moet registreren voor Hallo Accelerated netwerken voor virtuele Linux-machines tooparticipate in dit voorbeeld.
    - U hebt geen geselecteerd voor een VM-grootte, besturingssysteem of locatie die worden vermeld in Hallo [beperkingen](#limitations) sectie van dit artikel.
3. tooinstall Hallo-netwerkstuurprogramma versnelde voor Linux, volledige Hallo stappen voor het Hallo [Linux configureren](#configure-linux) sectie van dit artikel.

### <a name="linux-powershell"></a>PowerShell

>[!WARNING]
>Als u virtuele Linux-machines met versnelde netwerken in een abonnement maken en vervolgens een virtuele machine van Windows met versnelde netwerken in Hallo toocreate probeert hetzelfde abonnement, het maken van de virtuele machine van Windows hello mislukken. Tijdens deze preview kunt u het beste Linux- en Windows-VM's te met versnelde netwerken in afzonderlijke abonnementen testen.
>

1. Installeer de nieuwste versie Hallo van hello Azure PowerShell [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) module. Als u nieuwe tooAzure PowerShell, lezen Hallo [overzicht van Azure PowerShell](/powershell/azure/get-started-azureps?toc=%2fazure%2fvirtual-network%2ftoc.json) artikel.
2. Een PowerShell-sessie starten door te klikken op de knop Start van Windows hello typen **powershell**, vervolgens te klikken op **PowerShell** van Hallo zoekresultaten.
3. Voer in het PowerShell-venster Hallo `login-azurermaccount` opdracht toosign aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Registreren voor Hallo versnelde netwerken voor Azure preview door Hallo volgende stappen uit te voeren:
    - E-mailbericht te verzenden[ axnpreview@microsoft.com ](mailto:axnpreview@microsoft.com?subject=Request%20to%20enable%20subscription%20%3csubscription%20id%3e) met uw Azure-abonnement-ID en het beoogde gebruik. Wacht totdat een e-mailbevestiging van Microsoft over uw abonnement wordt ingeschakeld.
    - Voer Hallo opdracht tooconfirm die u zijn geregistreerd voor het Hallo-voorbeeld te volgen:
    
        ```powershell
        Get-AzureRmProviderFeature -FeatureName AllowAcceleratedNetworkingForLinux -ProviderNamespace Microsoft.Network
        ```

        Ga niet verder met stap 5 tot en met **geregistreerde** wordt weergegeven in Hallo uitvoeren nadat u de vorige opdracht Hallo invoeren. De uitvoer moet eruitzien als Hallo volgende voordat u doorgaat met de uitvoer:
    
        ```powershell
        FeatureName                        ProviderName      RegistrationState
        -----------                        ------------      -----------------
        AllowAcceleratedNetworkingForLinux Microsoft.Network Registered
        ```
        
      >[!NOTE]
      >Als u hebt deelgenomen aan Hallo Accelerated netwerken voor VM's van Windows-preview (het niet langer nodig tooregister toouse versnelde netwerken voor Windows-VM's), u worden niet automatisch geregistreerd voor Hallo Accelerated netwerken voor virtuele Linux-machines preview. U moet registreren voor Hallo Accelerated netwerken voor virtuele Linux-machines tooparticipate in dit voorbeeld.
      >
5. Kopieer Hallo script vervangen door Ubuntu of SLES naar wens te volgen in uw browser.  Redhat en CentOS hebben weer een andere workflow onderstaande:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
      -Name $RgName `
      -Location $Location
    
    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
      -Name MySubnet `
      -AddressPrefix 10.0.0.0/24
    
    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName $RgName `
      -Location $Location `
      -Name MyVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet

    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
      -Name MyPublicIp `
      -ResourceGroupName $RgName `
      -Location $Location `
      -AllocationMethod Static

    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
      -Name MyNic `
      -ResourceGroupName $RgName `
      -Location $Location `
      -SubnetId $Vnet.Subnets[0].Id `
      -PublicIpAddressId $Pip.Id `
      -EnableAcceleratedNetworking
     
    # Create a new Storage account and define hello new VM’s OSDisk name and its URI
    # Must end with ".vhd" extension
    $OSDiskName = "MyOsDiskName.vhd"
    # Storage account name must be between 3 and 24 characters in length and use numbers and lower-case letters only.
    $OSDiskSAName = "thestorageaccountname"  
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $RgName -Name $OSDiskSAName -Type "Standard_GRS" -Location $Location
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName
 
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential

    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
      -VMName MyVM -VMSize Standard_DS4_v2 | `
      Set-AzureRmVMOperatingSystem `
      -Linux `
      -ComputerName myVM `
      -Credential $Cred | `
    Set-AzureRmVMSourceImage `
      -PublisherName Canonical `
      -Offer UbuntuServer `
      -Skus 16.04-LTS `
      -Version latest | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk -Name $OSDiskName `
      -VhdUri $OSDiskUri `
      -CreateOption FromImage 

    # Create hello virtual machine.    
    New-AzureRmVM `
      -ResourceGroupName $RgName `
      -Location $Location `
      -VM $VmConfig
    ```
    
6. Met de rechtermuisknop op toopaste Hallo script en beginnen met de uitvoering van deze in uw PowerShell-venster. U wordt gevraagd om een gebruikersnaam en wachtwoord. Deze referenties toolog in toohello VM gebruiken bij het verbinden van tooit in de volgende stap Hallo. Als het Hallo-script is mislukt, controleert u dat:
    - U bent geregistreerd voor Hallo preview, zoals beschreven in stap 4
    - Als u VM-grootte, besturingssysteemtype of locatie-waarden in Hallo script gewijzigd voordat deze wordt uitgevoerd, dat Hallo waarden staan in Hallo [beperkingen](#Limitations) sectie van dit artikel.
7. tooinstall Hallo-netwerkstuurprogramma versnelde voor Linux, volledige Hallo stappen voor het Hallo [Linux configureren](#configure-linux) sectie van dit artikel.

### <a name="configure-linux"></a>Configureren van Linux

Zodra u Hallo VM in Azure maakt, moet u Hallo versnelde-netwerkstuurprogramma voor Linux installeren. Voordat u Hallo stappen uitvoert, moet u een Linux-VM gemaakt met versnelde netwerken met behulp van beide Hallo [portal](#linux-portal) of [PowerShell](#linux-powershell) stappen in dit artikel. 

1. Open in een internetbrowser hello Azure [portal](https://portal.azure.com) en meld u aan met uw Azure [account](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Als u nog een account hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Hallo boven aan het portal toohello rechts Hallo Hallo *zoeken bronnen* balk, klikt u op Hallo **> _** pictogram toostart een cloud Bash-shell (Preview). Hallo Bash cloud shell deelvenster verschijnt onderin Hallo van Hallo-portal en na een paar seconden geeft een  **username@Azure:~ $** prompt. Hoewel u SSH toohello VM vanaf uw computer in plaats van door Hallo cloud shell kunt, Hallo-instructies in deze zelfstudie wordt ervan uitgegaan dat u Hallo cloud shell.
3. Bovenaan Hallo Hallo-portal, in Hallo vak die bevat tekst hello *zoeken bronnen*, type *MyVm*. Wanneer **MyVm** wordt weergegeven in zoekresultaten hello, klik erop.
4. In Hallo **MyVm** blade die wordt weergegeven, klikt u op Hallo **Connect** knop in Hallo linksboven Hallo-blade. **Opmerking:** als **maken** zichtbaar onder Hallo **Connect** knop Azure is nog niet voltooid Hallo VM maken. Klik op **Connect** pas nadat u niet meer zien **maken** onder Hallo **Connect** knop.
5. Azure opent u een melding tooenter hello `ssh adminuser@<ipaddress>`. Voer deze opdracht Hallo cloud shell (of kopiëren van Hallo vak die werden weergegeven in stap 4 en plak deze in de cloud-shell toohello), druk op Enter.
6. Voer **Ja** toohello vraag waarin u indien toocontinue verbinding maakt gewenst, druk op Enter.
7. U hebt ingevoerd bij het maken van VM Hallo Hallo-wachtwoord invoeren. Eenmaal aangemeld toohello VM, ziet u een adminuser@MyVm:~ $ prompt. U bent nu aangemeld toohello VM via Hallo cloud shell-sessie. **Opmerking:** Cloud shell sessies time-out na 10 minuten van inactiviteit.

Op dit moment afhankelijk Hallo instructies van Hallo-distributie die u gebruikt. 

#### <a name="ubuntusles"></a>Ubuntu/SLES

1. Voer bij Hallo-prompt `uname -r` en Bevestig Hallo-versie voor:

    * Ubuntu is '4.4.0-77-generic,' of hoger
    * SLES is '4.4.59-92.20-default' of hoger

2. Actieve Hallo-opdrachten die achter een band tussen Hallo standaard netwerken vNIC en Hallo versnelde netwerken vNIC maken. Netwerkverkeer gebruikt Hallo beter presteren versnelde netwerken vNIC, terwijl Hallo obligatie zorgt ervoor dat netwerkverkeer via de configuratiewijzigingen niet wordt onderbroken.
          
     ```bash
     wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/configure_hv_sriov.sh
     chmod +x ./configure_hv_sriov.sh
     sudo ./configure_hv_sriov.sh
     ```
3. Na het Hallo-script wordt uitgevoerd, hebben Hallo VM wordt opnieuw opgestart nadat een 60 seconden onderbreken.
4. Hallo VM opnieuw wordt opgestart, verbinding eenmaal tooit door stap 5-7 opnieuw uit te voeren.
5. Voer Hallo `ifconfig` opdracht in en Bevestig dat bond0 is actief en Hallo-interface wordt weergegeven als omhoog. 
 
 >[!NOTE]
      >Toepassingen die gebruikmaken van versnelde netwerken moeten communiceren via Hallo *bond0* interface niet *eth0*.  Hallo Interfacenaam overgaan voordat versnelde netwerken algemene beschikbaarheid bereikt.

#### <a name="rhelcentos"></a>RHEL/CentOS

Maken van een Red Hat Enterprise Linux of CentOS 7.3 VM, is enkele extra stappen tooload Hallo meest recente stuurprogramma's die nodig is voor SR-IOV en hello (VF stuurprogramma Virtual Function) voor de netwerkkaart Hallo vereist. Hallo bereidt eerste fase van de instructies Hallo een installatiekopie die gebruikt toomake worden kan een of meer virtuele machines die Hallo-stuurprogramma's die vooraf is geladen.

##### <a name="phase-one-prepare-a-red-hat-enterprise-linux-or-centos-73-base-image"></a>Stap 1: een Red Hat Enterprise Linux of CentOS 7.3 basisinstallatiekopie voorbereiden. 

1.  Inrichten van een niet - SRIOV CentOS 7.3 VM op Azure

2.  LIS 4.2.2 installeren:
    
    ```bash
    wget http://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
    tar -xvf lis-rpms-4.2.2-2.tar.gz
    cd LISISO && sudo ./install.sh
    ```

3.  De config-bestanden downloaden
    
    ```bash
    cd /etc/udev/rules.d/  
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/60-hyperv-vf-name.rules 
    cd /usr/sbin/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/hv_vf_name 
    sudo chmod +x hv_vf_name
    cd /etc/sysconfig/network-scripts/
    sudo wget https://raw.githubusercontent.com/LIS/lis-next/master/tools/sriov/ifcfg-vf1   
    ```

4.  Inrichting ervan ongedaan maakt deze VM

    ```bash
    sudo waagent -deprovision+user 
    ```

5.  Vanuit Azure-portal stop deze virtuele machine; en gaat u tooVM van '-schijven genoemd, vastleggen Hallo OSDisk van VHD-URI. Deze URI bevat Hallo basisinstallatiekopie van VHD-naam en de storage-account. 
 
##### <a name="phase-two-provision-new-vms-on-azure"></a>Fase twee: inrichten van nieuwe virtuele machines in Azure

1.  Nieuwe virtuele machines op basis van nieuw AzureRMVMConfig inrichten met behulp van Hallo basisinstallatiekopie VHD vastgelegd in stap 1, met AcceleratedNetworking ingeschakeld op Hallo vNIC:

    ```powershell
    $RgName="MyResourceGroup"
    $Location="westus2"
    
    # Create a resource group
    New-AzureRmResourceGroup `
     -Name $RgName `
     -Location $Location

    # Create a subnet
    $Subnet = New-AzureRmVirtualNetworkSubnetConfig `
     -Name MySubnet `
     -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $Vnet=New-AzureRmVirtualNetwork `
     -ResourceGroupName $RgName `
     -Location $Location `
     -Name MyVnet `
     -AddressPrefix 10.0.0.0/16 `
     -Subnet $Subnet
    
    # Create a public IP address
    $Pip = New-AzureRmPublicIpAddress `
     -Name MyPublicIp `
     -ResourceGroupName $RgName `
     -Location $Location `
     -AllocationMethod Static
    
    # Create a virtual network interface and associate hello public IP address tooit
    $Nic = New-AzureRmNetworkInterface `
     -Name MyNic `
     -ResourceGroupName $RgName `
     -Location $Location `
     -SubnetId $Vnet.Subnets[0].Id `
     -PublicIpAddressId $Pip.Id `
     -EnableAcceleratedNetworking
    
    # Specify hello base image's VHD URI (from phase one step 5). 
    # Note: hello storage account of this base image vhd should have "Storage service encryption" disabled
    # See more from here: https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption
    # This is just an example URI, you will need tooreplace this when running this script
    $sourceUri="https://myexamplesa.blob.core.windows.net/vhds/CentOS73-Base-Test120170629111341.vhd" 

    # Specify a URI for hello location from which hello new image binary large object (BLOB) is copied toostart hello virtual machine. 
    # Must end with ".vhd" extension
    $OsDiskName = "MyOsDiskName.vhd" 
    $destOsDiskUri = "https://myexamplesa.blob.core.windows.net/vhds/" + $OsDiskName
    
    # Define a credential object for hello VM. PowerShell prompts you for a username and password.
    $Cred = Get-Credential
    
    # Create a custom virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
     -VMName MyVM -VMSize Standard_DS4_v2 | `
    Set-AzureRmVMOperatingSystem `
     -Linux `
     -ComputerName myVM `
     -Credential $Cred | `
    Add-AzureRmVMNetworkInterface -Id $Nic.Id | `
    Set-AzureRmVMOSDisk `
     -Name $OsDiskName `
     -SourceImageUri $sourceUri `
     -VhdUri $destOsDiskUri `
     -CreateOption FromImage `
     -Linux
    
    # Create hello virtual machine.    
    New-AzureRmVM `
     -ResourceGroupName $RgName `
     -Location $Location `
     -VM $VmConfig
    ```

2.  Nadat de virtuele machines wordt opgestart, 'lspci' hello VF apparaat controleren en Hallo Mellanox invoer. Bijvoorbeeld, zien we dit item in Hallo lspci uitvoer:
    
    ```
    0001:00:02.0 Ethernet controller: Mellanox Technologies MT27500/MT27520 Family [ConnectX-3/ConnectX-3 Pro Virtual Function]
    ```
    
3.  Hallo binding script door uitvoeren:

    ```bash
    sudo bondvf.sh
    ```

4.  Start opnieuw op Hallo van nieuwe virtuele machines:

    ```bash
    sudo reboot
    ```

Hallo VM moet beginnen met bond0 geconfigureerd en Hallo versnelde netwerken pad ingeschakeld.  Voer `ifconfig` tooconfirm.

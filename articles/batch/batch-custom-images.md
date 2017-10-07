---
title: "aaaProvision Azure Batch pools van aangepaste installatiekopieën | Microsoft Docs"
description: "U kunt een Batch pool van een aangepaste installatiekopie tooprovision rekenknooppunten die Hallo software bevatten en gegevens die u nodig hebt voor uw toepassing maken. Aangepaste installatiekopieën zijn een efficiënte manier tooconfigure compute knooppunten toorun uw Batch-workloads."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/07/2017
ms.author: tamram
ms.openlocfilehash: 5cb698ee90f7d3ec9ffe69fa4dc602132c3f7569
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-custom-image-toocreate-a-pool-of-virtual-machines"></a>Gebruik een aangepaste installatiekopie toocreate een pool van virtuele machines

Wanneer u een pool van virtuele machines in Azure Batch maakt, geeft u een installatiekopie van virtuele machine (VM) waarmee Hallo-besturingssysteem voor elk rekenknooppunt in de groep Hallo. U kunt een pool van virtuele machines maken met behulp van een installatiekopie van een Azure Marketplace of door een aangepaste VHD-installatiekopie die u hebt voorbereid. Wanneer u een aangepaste installatiekopie opgeeft, hebt u controle over hoe Hallo-besturingssysteem is geconfigureerd op Hallo moment die elk rekenknooppunt is ingericht. Uw aangepaste installatiekopie kan ook toepassingen bevatten en verwijzen naar gegevens die beschikbaar op Hallo zijn rekenknooppunt zodra deze is ingericht.

Met een aangepaste installatiekopie kunt u bij het ophalen van uw pool, rekenknooppunten tijd besparen klaar toorun uw Batch-werkbelasting. Terwijl u kunt altijd een Azure Marketplace-installatiekopie gebruiken en software op elk rekenknooppunt installeren nadat deze zijn ingericht, is het mogelijk dat deze aanpak minder efficiënt dan met een aangepaste installatiekopie. 

Een aantal redenen toouse omvatten een aangepaste installatiekopie die is geconfigureerd voor uw scenario hoeven:

- **Hallo-besturingssysteem (OS) configureren** geen speciale configuratie van het besturingssysteem Hallo kan worden uitgevoerd op Hallo aangepaste installatiekopie. 
- **Grote toepassingen installeren.** Toepassingen installeren op een aangepaste installatiekopie is efficiënter dan installeren op elk rekenknooppunt nadat deze is ingericht.
- **Kopiëren van grote hoeveelheden gegevens.** Als Hallo gegevens gekopieerde toohello aangepaste installatiekopie, moet deze alleen toobe slechts één keer gekopieerd in plaats van tooeach rekenknooppunt, tijd en bandbreedte besparen.
- **Start opnieuw op tijdens het installatieproces Hallo Hallo VM.** Opnieuw opstarten Hallo VM kan een tijdrovend proces zijn, met name als u een aantal rekenknooppunten.

## <a name="prerequisites"></a>Vereisten

- **Een Batch-account is gemaakt met de Hallo gebruikerabonnement groep toewijzing modus.** toouse een aangepaste installatiekopie tooprovision virtuele Machine-adresgroepen maken uw Batch-account met Hallo gebruikerabonnement [groep toewijzing modus](batch-api-basics.md#pool-allocation-mode). Met deze modus worden toegewezen aan Batch-pools in Hallo abonnement waarin Hallo account zich bevindt. Zie Hallo [Account](batch-api-basics.md#account) in sectie [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md) voor informatie over het instellen van Hallo groep toewijzing modus bij het maken van een Batch-account.

- Een **Azure Storage-account.** toocreate een pool van virtuele machines met een aangepaste installatiekopie, moet u een standaard, algemene Azure Storage-account in Hallo hetzelfde abonnement en dezelfde regio. Als u een aangepaste installatiekopie van een virtuele machine in Azure maakt, wordt u Hallo toohello opslagaccount voor installatiekopieën waar besturingssysteemschijf Hallo van de virtuele machine zich bevindt en hoeft u geen toocreate een afzonderlijke opslagaccount kopiëren. 
    
## <a name="prepare-a-custom-image"></a>Een aangepaste installatiekopie voorbereiden

een aangepaste installatiekopie voor gebruik met Batch tooprepare, moet u een bestaande installatie van Linux of Windows generalize. De installatie van een besturingssysteem te generaliseren verwijdert systeemspecifieke gegevens. Hallo-resultaat is een installatiekopie die kan worden geïnstalleerd op andere computers of virtuele machines.  

> [!IMPORTANT]
> Batch ondersteunt momenteel geen gebruik van Azure tooprovision installatiekopieën van een groep beheerd. de aangepaste installatiekopie Hallo u tooprovision die een pool moet worden opgeslagen in Azure Storage. 
>
> Houd er rekening mee Hallo volgende punten bij het voorbereiden van uw aangepaste installatiekopie:
> - Zorg ervoor dat die Hallo OS basisinstallatiekopie gebruik van uw Batch-pools biedt tooprovision niet hebben geen vooraf geïnstalleerde Azure-extensies, zoals Hallo aangepast Script-extensie. Als Hallo afbeelding een vooraf geïnstalleerde uitbreiding bevat, ondervinden Azure problemen Hallo VM implementeren.
> - Zorg ervoor dat Hallo OS basisinstallatiekopie die maakt gebruik van tijdelijke standaardstation Hallo bieden zoals hello Batch knooppunt agent momenteel Hallo standaard tijdelijke station verwacht.
>
>

Als een aangepaste installatiekopie kunt u eventuele bestaande voorbereide installatiekopie van een Windows- of Linux. Bijvoorbeeld, als u wilt toouse een afbeelding voor lokaal, Hallo installatiekopie tooan Azure Storage-account in uploaden Hallo hetzelfde abonnement en dezelfde regio bevinden als uw Batch-account met [AzCopy](../storage/storage-use-azcopy.md) of een ander hulpprogramma voor het uploaden.

U kunt ook een aangepaste installatiekopie van een nieuwe of bestaande Azure-virtuele machine voorbereiden. Als u een nieuwe virtuele machine maakt, kunt u een Azure Marketplace-installatiekopie gebruikt als basisinstallatiekopie Hallo voor uw aangepaste installatiekopie en deze aanpassen. toocustomize hello basisinstallatiekopie, een virtuele machine in Azure maken en toevoegen van uw toepassingen of gegevens tooit. Vervolgens generalize Hallo VM tooserve als de aangepaste installatiekopie en sla het tooAzure opslag. 

een aangepaste installatiekopie van een virtuele machine van Azure tooprepare als volgt te werk:

1. Maak een **onbeheerde** Azure VM van de installatiekopie van een Azure Marketplace. Azure Marketplace afbeeldingen bevat voor zowel [Windows](../virtual-machines/windows/quick-create-portal.md) en [Linux](../virtual-machines/linux/quick-create-portal.md).
    
    Zorg ervoor dat u selecteert bij stap 3 van Hallo proces voor het maken van VM **Nee** voor **opslag: gebruik beheerd schijven** optie. Ook Noteer Hallo opslagaccountnaam voor de besturingssysteemschijf Hallo van de virtuele machine, omdat dit opslagaccount ook waar uw aangepaste installatiekopie wordt opgeslagen in Azure:

    ![Een niet-beheerde virtuele machine en de opmerking Hallo opslagaccountnaam maken](media/batch-custom-images/vm-create-storage.png)
 
2. Hallo-proces voor het maken van uw virtuele machine voltooien en wacht toobe toegewezen door Azure. Hier volgt een afbeelding die laat zien van een virtuele machine in Azure-portal op Hallo uitvoeringsstatus Hallo:

    ![Een virtuele machine maken vanuit een marketplace-installatiekopie](media/batch-custom-images/vm-status-running.png)

3. Zodra Hallo VM wordt uitgevoerd, verbinding maken met tooit via RDP (voor Windows) of SSH (voor Linux). Alle benodigde software installeren of kopiëren van de gewenste gegevens, en vervolgens generalize Hallo VM. Volg de stappen Hallo in [Generalize Hallo VM](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized.md#generalize-the-vm). 
   
4. Hallo stappen te volgen[tooAzure PowerShell aanmelden](../virtual-machines/windows/sa-copy-generalized.md#log-in-to-azure-powershell). Zie tooinstall Azure PowerShell [overzicht van Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.2.0). 

5. Vervolgens stappen hello te[Deallocate hello VM- en set Hallo status toogeneralized](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/sa-copy-generalized#deallocate-the-vm-and-set-the-state-to-generalized). 

    In hello Azure-portal, ziet u dat Hallo die VM toewijzing ongedaan wordt gemaakt:

    ![Zorg ervoor dat Hallo die VM toewijzing ongedaan wordt gemaakt](media/batch-custom-images/vm-status-deallocated.png)

6.  Maken en opslaan van Hallo VM image tooAzure opslag met behulp van Hallo [opslaan AzureRmVMImage](https://docs.microsoft.com/powershell/module/azurerm.compute/save-azurermvmimage) PowerShell-cmdlet. Ga als volgt Hallo-instructies die worden beschreven [Hallo-afbeelding maken](../virtual-machines/windows/sa-copy-generalized.md#create-the-image).
    
    Hallo VM-installatiekopie wordt opgeslagen toohello Azure Storage-account gemaakt wanneer Hallo VM is gemaakt, zoals u in stap 1 van deze procedure. Hallo opslaan AzureRmVMImage cmdlet slaat Hallo installatiekopie toohello **system** container in dit opslagaccount. Hallo `-DestinationContainername` parameter de namen van een virtuele map in Hallo **system** container. Hallo `-VHDNamePrefix` parameter geeft u een voorvoegsel voor Hallo blob-naam. Dit voorvoegsel wordt voorafgegaan toohello blob-naam met een afbreekstreepje. 

    Stel bijvoorbeeld dat u opslaan AzureRmVMImage aanroept met Hallo volgende parameters:  

        Save-AzureRmVMImage -ResourceGroupName sample-resource-group -Name vm-custom-image -DestinationContainerName batchimages -VHDNamePrefix custom -Path C:\Temp\Images\vm-custom-image.json

    Hallo resulterende installatiekopie wordt opgeslagen toohello locatie en de blobnaam hier weergegeven:

    ![Locatie van de VHD-opgeslagen in de systeemcontainer](media/batch-custom-images/vhd-in-vm-storage-account.png)

    > [!NOTE]
    > Een virtuele machine van Azure niet-beheerde maakt verschillende storage-accounts voor verschillende doeleinden. Als u hebt niet Noteer de naam van de Hallo van Hallo storage-container voor Hallo OS-schijf als hello VM is gemaakt, wordt de zoeken Hallo gekoppeld storage-account bevat Hallo **system** container. Navigeer door Hallo **system** container toofind Hallo aangepaste installatiekopie met Hallo-waarden die u hebt opgegeven voor Hallo **opslaan AzureRmVMImage** opdracht.

## <a name="create-a-pool-from-a-custom-image-in-hello-portal"></a>Een pool maken van een aangepaste installatiekopie in Hallo-portal

Als u uw aangepaste installatiekopie hebt opgeslagen en u weet dat de locatie, kunt u een Batch-pool maken vanuit die installatiekopie. Volg deze stappen toocreate een pool van hello Azure-portal:

1. Navigeer tooyour Batch-account in hello Azure-portal. Deze account moet rekening met Hallo aangepaste installatiekopie in Hallo hetzelfde abonnement en dezelfde regio als het Hallo-opslag. 
2. In Hallo **instellingen** -venster op Hallo links, selecteer Hallo **Pools** menu-item.
3. In Hallo **Pools** venster, selecteer Hallo **toevoegen** opdracht.
4. Op Hallo **van toepassingen toevoegen** Selecteer **aangepaste installatiekopie (Linux/Windows)** van Hallo **afbeeldingstype** vervolgkeuzelijst. Hallo-portal wordt weergegeven Hallo **aangepaste installatiekopie** objectkiezer. Navigeer toohello opslagaccount waarin de aangepaste installatiekopie zich bevindt en selecteer de gewenste VHD uit Hallo container Hallo. 
5. Selecteer Hallo juist **aanbieding-Publisher-Sku** voor uw aangepaste VHD.
6. Geef-instellingen, inclusief Hallo Hallo resterende vereist **knooppuntgrootte**, **gericht op specifieke knooppunten**, en **lage prioriteit knooppunten**, maar ook een optionele instellingen gewenst.

    Bijvoorbeeld: voor een aangepaste installatiekopie van de Microsoft Windows Server Datacenter 2016 Hallo **van toepassingen toevoegen** venster wordt weergegeven als volgt te werk:

    ![Toepassingen toevoegen van aangepaste Windows-installatiekopie](media/batch-custom-images/add-pool-custom-image.png)
  
toocheck of een bestaande pool is gebaseerd op een aangepaste installatiekopie bekijken Hallo **besturingssysteem** eigenschap in Hallo resource samenvatting sectie Hallo **groep** venster. Als Hallo toepassingen vanuit een aangepaste installatiekopie is gemaakt, wordt deze ingesteld te**aangepaste VM-installatiekopie**.

Alle aangepaste VHD's die zijn gekoppeld aan een groep worden weergegeven op van de pool Hallo **eigenschappen** venster.
 
## <a name="next-steps"></a>Volgende stappen

- Zie voor een gedetailleerd overzicht van Batch [ontwikkelen grootschalige parallelle compute-oplossingen met Batch](batch-api-basics.md).
- Zie voor meer informatie over het maken van een Batch-account [een Batch-account maken met Azure-portal Hallo](batch-account-create-portal.md).

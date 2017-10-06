---
title: aaaOverview van Azure Batch voor ontwikkelaars | Microsoft Docs
description: Meer informatie over Hallo functies van Hallo Batch-service en de API's vanuit het standpunt.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Grootschalige parallelle rekenoplossingen ontwikkelen met Batch

In dit overzicht van de kernonderdelen Hallo Hallo Azure Batch-service bespreken we Hallo primaire functies en bronnen waarmee ontwikkelaars van Batch toobuild grootschalige parallelle kunt compute-oplossingen.

Of u een gedistribueerde rekenkundige toepassing ontwikkelt of service die problemen direct [REST-API] [ batch_rest_api] aanroepen of u gebruikt een Hallo [Batch-SDK's](batch-apis-tools.md#azure-accounts-for-batch-development), gebruikt u veel Hallo bronnen en functies die in dit artikel wordt besproken.

> [!TIP]
> Zie voor een hoger niveau inleiding toohello Batch-service [basisbeginselen van Azure Batch](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Werkstroom van de Batch-service
Hallo is volgende werkstroom op hoog niveau doorgaans vrijwel alle toepassingen en services die gebruikmaken van Batch-service voor de verwerking van parallelle workloads Hallo:

1. Hallo uploaden **gegevensbestanden** dat u wilt dat tooprocess tooan [Azure Storage] [ azure_storage] account. Batch bevat ingebouwde ondersteuning voor toegang tot Azure Blob-opslag en uw taken kunnen deze bestanden te downloaden[rekenknooppunten](#compute-node) bij het Hallo-taken uitvoeren.
2. Hallo uploaden **toepassingsbestanden** die de taken worden uitgevoerd. Deze bestanden kunnen worden binaire bestanden of scripts en hun afhankelijkheden en worden uitgevoerd door Hallo taken in uw taken. Uw taken deze bestanden kunnen downloaden van uw opslagaccount of kunt u Hallo [toepassingspakketten](#application-packages) functie van Batch voor de implementatie en beheer van toepassingen.
3. Maak een [pool](#pool) van rekenknooppunten. Wanneer u een pool maakt, kunt u het aantal rekenknooppunten voor het Hallo-toepassingen, hun grootte en besturingssysteem Hallo Hallo opgeven. Wanneer elke taak in de taak wordt uitgevoerd, wordt het toegewezen tooexecute op een van de knooppunten Hallo in uw groep.
4. Maak een [job](#job). Een job beheert een verzameling van taken. U koppelt elke taak tooa specifieke toepassingen waar die taak taken worden uitgevoerd.
5. Voeg [taken](#task) toohello taak. Elke taak wordt uitgevoerd Hallo toepassing of het script dat u tooprocess Hallo-gegevensbestanden die het downloaden van uw opslagaccount hebt geüpload. Omdat elke taak is voltooid, kan deze de uitvoer tooAzure opslag uploaden.
6. Voortgang van de taak en uitvoer van de taak Hallo ophalen uit Azure Storage.

Hallo volgende secties bespreken deze en andere bronnen van Batch die uw gedistribueerde rekenkundige scenario inschakelen Hallo.

> [!NOTE]
> U moet een [Batch-account](#account) toouse Hallo Batch-service. Voor de meeste Batch-oplossingen wordt ook een [Azure-opslagaccount][azure_storage] gebruikt om bestanden op te slaan en op te halen. Batch ondersteunt momenteel alleen Hallo **algemeen** opslagaccounttype, zoals beschreven in stap 5 van [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Batch-serviceresources
Aantal Hallo na resources--accounts, compute knooppunten, pools, jobs en taken--vereist zijn voor alle oplossingen die gebruikmaken van Hallo Batch-service. Andere resources, zoals taakplanningen en toepassingspakketten, zijn nuttige, maar optionele functies.

* [Account](#account)
* [Rekenknooppunt](#compute-node)
* [Pool](#pool)
* [Job](#job)

  * [Jobplanningen](#scheduled-jobs)
* [Taak](#task)

  * [Begintaak](#start-task)
  * [Jobbeheertaak](#job-manager-task)
  * [Jobvoorbereidingstaken en jobvrijgevingstaken](#job-preparation-and-release-tasks)
  * [Taken met meerdere instanties (MPI)](#multi-instance-tasks)
  * [Taakafhankelijkheden](#task-dependencies)
* [Toepassingspakketten](#application-packages)

## <a name="account"></a>Account
Een Batch-account is een uniek geïdentificeerde entiteit in Hallo Batch-service. Alle verwerkingen zijn gekoppeld aan een Batch-account.

U kunt met behulp van hello Azure Batch-account maken [Azure-portal](batch-account-create-portal.md) of via een programma, zoals Hello [Batch Management .NET-bibliotheek](batch-management-dotnet.md). Wanneer het Hallo-account maakt, kunt u een Azure storage-account koppelen.

### <a name="pool-allocation-mode"></a>Pooltoewijzingsmodus

Wanneer u een Batch-account maakt, kunt u opgeven hoe [pools](#pool) rekenknooppunten worden toegewezen. U kunt tooallocate pools van rekenknooppunten in een abonnement beheerd door de Azure Batch of kunt u deze in uw eigen abonnement toewijzen. Hallo *groep toewijzing modus* eigenschap voor Hallo account bepaalt waar de groepen worden toegewezen. 

toodecide die groep toewijzing modus toouse, kunt u overwegen die beste past bij uw scenario:

* **Batch-Service**: Batch-Service is Hallo groep toewijzing standaardmodus, in welke groepen achter de schermen Hallo in beheerde Azure-abonnementen worden toegewezen. Houd er rekening mee deze sleutel verwijst over Hallo Batch-Service groep toewijzing modus:

    - Hallo Batch-Service groep toewijzing modus ondersteunt Cloudservice en de virtuele Machine van toepassingen.
    - Hallo Batch-Service groep toewijzing modus ondersteunt zowel gedeelde sleutelverificatie of [Azure Active Directory-verificatie](batch-aad-auth.md) (Azure AD). 
    - In toepassingen die zijn toegewezen met de Hallo Batch-Service groep toewijzing modus kunt u beide toegewezen of prioriteit Laag rekenknooppunten.
    - Gebruik geen Hallo Batch-Service groep toewijzing modus als u van plan bent toocreate virtuele machine van Azure groepen van aangepaste installatiekopieën voor virtuele machine, of als u van plan bent toouse een virtueel netwerk. Uw account in plaats daarvan met de Hallo gebruikerabonnement groep toewijzing modus gemaakt.
    - Virtuele Machine pools ingericht in een account dat is gemaakt met de Hallo Batch-Service groep toewijzing modus moeten worden gemaakt van [Azure Virtual Machines Marketplace] [ vm_marketplace] installatiekopieën.

* **Gebruikerabonnement**: met de Hallo gebruikerabonnement groep toewijzing modus Batch-pools zijn toegewezen in hello Azure-abonnement waarbij Hallo-account is gemaakt. Houd er rekening mee deze sleutel verwijst over Hallo gebruikerabonnement groep toewijzing modus:
     
    - Hallo gebruikerabonnement groep toewijzing modus ondersteunt alleen de groepen van de virtuele Machine. Cloud Services-pools worden niet ondersteund.
    - toocreate virtuele Machine groepen van aangepaste installatiekopieën van virtuele machine of toouse een virtueel netwerk met virtuele Machine van toepassingen, moet u Hallo gebruikerabonnement groep toewijzing modus.  
    - U moet gebruiken [Azure Active Directory-verificatie](batch-aad-auth.md) met toepassingen die zijn toegewezen in Hallo gebruikerabonnement. 
    - U moet een Azure sleutelkluis voor uw Batch-account instellen als Hallo groep toewijzing modus tooUser abonnement is ingesteld. 
    - In de opslaggroepen in een account dat is gemaakt met de Hallo gebruikerabonnement groep toewijzing modus kunt u alleen specifieke rekenknooppunten. Knooppunten met lage prioriteit worden niet ondersteund.
    - Virtuele Machine pools ingericht in een account met de Hallo gebruikerabonnement groep toewijzing modus kunnen worden gemaakt vanuit [Azure Virtual Machines Marketplace] [ vm_marketplace] afbeeldingen of van aangepaste installatiekopieën die u hebt bieden.

Hallo volgende tabel vergelijkt Hallo Batch-Service en de gebruikerabonnement groep toewijzing modi.

| **Pooltoewijzingsmodus**                 | **Batch-service**                                                                                       | **Gebruikersabonnement**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Pools worden toegewezen in**               | Een door Azure beheerd abonnement                                                                           | Hallo gebruikerabonnement in welke Hallo Batch-account is gemaakt                        |
| **Ondersteunde configuraties**             | <ul><li>Cloudserviceconfiguratie</li><li>Virtuele-machineconfiguratie (Linux en Windows)</li></ul> | <ul><li>Virtuele-machineconfiguratie (Linux en Windows)</li></ul>                |
| **Ondersteunde VM-installatiekopieën**                  | <ul><li>Azure Marketplace-installatiekopieën</li></ul>                                                              | <ul><li>Azure Marketplace-installatiekopieën</li><li>Aangepaste installatiekopieën</li></ul>                   |
| **Ondersteunde typen rekenknooppunten**         | <ul><li>Toegewezen knooppunten</li><li>Knooppunten met lage prioriteit</li></ul>                                            | <ul><li>Toegewezen knooppunten</li></ul>                                                  |
| **Ondersteunde verificatie**             | <ul><li>Gedeelde sleutel</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault vereist**             | Nee                                                                                                      | Ja                                                                                |
| **Kerngeheugenquotum**                           | Bepaald op basis van het Batch-kerngeheugenquotum                                                                          | Bepaald op basis van het kerngeheugenquotum van het abonnement                                              |
| **Azure Virtual Network-ondersteuning (VNet)** | Groepen die zijn gemaakt met de Hallo configuratie voor Cloud-Service                                                      | Groepen met virtuele-machineconfiguratie Hallo gemaakt                               |
| **Ondersteunde VNet-implementatiemodellen**      | VNets die zijn gemaakt met het klassieke implementatiemodel                                                             | Vnets die zijn gemaakt met het klassieke implementatiemodel Hallo of Azure Resource Manager |

## <a name="azure-storage-account"></a>Azure-opslagaccount

Bij de meeste Batch-oplossingen wordt gebruikgemaakt van Azure Storage om resourcebestanden en uitvoerbestanden op te slaan.  

Batch ondersteunt momenteel alleen Hallo algemeen opslagaccounttype, zoals beschreven in stap 5 van [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) in [over Azure storage-accounts](../storage/common/storage-create-storage-account.md). Uw Batch-taken (inclusief standaardtaken, begintaken, jobvoorbereidingstaken en jobvrijgevingstaken) moeten bronbestanden opgeven die zich bevinden in algemene opslagaccounts.


## <a name="compute-node"></a>Rekenknooppunt
Een rekenknooppunt is een Azure virtuele machine (VM) of een cloudservice-VM die is toegewezen tooprocessing een deel van uw toepassing werklast. Hallo-grootte van een knooppunt bepaalt Hallo aantal CPU-kernen, geheugencapaciteit en grootte van het lokale bestand die toohello knooppunt is toegewezen. U kunt groepen van Windows of Linux-knooppunten maken met behulp van Azure Cloud Services, installatiekopieën van Hallo [Azure Virtual Machines Marketplace][vm_marketplace], of aangepaste installatiekopieën die u opstelt. Zie de volgende Hallo [groep](#pool) sectie voor meer informatie over deze opties.

Knooppunten kunnen uitvoeren voor een uitvoerbaar bestand of script dat wordt ondersteund door Hallo besturingssysteemomgeving van Hallo-knooppunt. Dit omvat \*.exe \*.cmd, \*.bat en PowerShell-scripts voor Windows - en binaire bestanden, shell- en Python-scripts voor Linux.

Alle rekenknooppunten in Batch omvatten ook:

* Een standaard[mapstructuur](#files-and-directories) en daaraan gekoppelde [omgevingsvariabelen](#environment-settings-for-tasks) die beschikbaar zijn voor verwijzing door taken.
* **Firewall** instellingen die zijn geconfigureerd met toocontrol toegang.
* [Externe toegang](#connecting-to-compute-nodes) tooboth (Remote Desktop Protocol (RDP)) voor Windows en Linux (Secure Shell (SSH))-knooppunten.

## <a name="pool"></a>Pool
Een pool is een verzameling knooppunten waarop uw toepassing wordt uitgevoerd. Hallo-toepassingen kan worden gemaakt handmatig door u of automatisch door Hallo Batch-service wanneer u Hallo werk toobe gedaan opgeven. U kunt maken en beheren van een groep die voldoet aan de resourcevereisten Hallo van uw toepassing. Een groep kan alleen worden gebruikt door Hallo Batch-account waarin deze is gemaakt. Een Batch-account kan meer dan één pool hebben.

Azure Batch-pools bouwen op Hallo core Azure compute-platform. Ze bieden grootschalige toewijzing, installatie van toepassingen, gegevensdistributie, statuscontrole en flexibele aanpassing van het aantal rekenknooppunten binnen een pool hello ([schalen](#scaling-compute-resources)).

Elk knooppunt dat is toegevoegd aan de groep tooa is een unieke naam en IP-adres toegewezen. Wanneer een knooppunt uit een groep wordt verwijderd, gaan alle wijzigingen die zijn aangebracht toohello besturingssysteem of bestanden verloren en de naam en IP-adres worden vrijgegeven voor toekomstig gebruik. Wanneer een knooppunt een pool verlaat, is de levensduur ervan beëindigd.

Wanneer u een pool maakt, kunt u Hallo kenmerken te volgen. Sommige instellingen zijn, afhankelijk van Hallo groep toewijzing modus Hallo Batch [account](#account):

- Besturingssysteem en versie van rekenknooppunt
- Type rekenknooppunt en beoogd aantal knooppunten
- Grootte van rekenknooppunten Hallo
- Beleid voor vergroten/verkleinen
- Taakplanningsbeleid
- Communicatiestatus voor rekenknooppunten
- Begintaken voor rekenknooppunten
- Toepassingspakketten
- Netwerkconfiguratie

Elk van deze instellingen wordt nader beschreven in de volgende secties Hallo beschreven.

> [!IMPORTANT]
> Batch-accounts die zijn gemaakt met de Hallo Batch-Service groep toewijzing modus hebben een standaardquotum dat Hallo aantal kernen in een Batch-account beperkt. Hallo aantal kernen dat overeenkomt met het aantal rekenknooppunten toohello. U vindt Hallo standaardquota en instructies over het te[een quotum verhogen](batch-quota-limit.md#increase-a-quota) in [quota en limieten voor hello Azure Batch-service](batch-quota-limit.md). Als uw pool niet het doelaantal knooppunten oplevert is, mogelijk kerngeheugenquotum Hallo Hallo reden.
>
>Batch-accounts die zijn gemaakt met de Hallo gebruikerabonnement groep toewijzing modus naleven niet, quota's Hallo Batch-service. In plaats daarvan ze delen in Hallo kerngeheugenquotum voor Hallo opgegeven abonnement. Zie [Virtual Machines limits](../azure-subscription-service-limits.md#virtual-machines-limits) (Limieten voor Virtuele Machines) in [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md) (Azure-abonnement en servicelimieten, -quota en -beperkingen) voor meer informatie.
>
>

### <a name="compute-node-operating-system-and-version"></a>Besturingssysteem en versie van rekenknooppunt

Wanneer u een Batch-pool maakt, kunt u hello Azure Virtuele-machineconfiguratie en Hallo type besturingssysteem u toorun op elk rekenknooppunt in de groep hello wilt opgeven. Er zijn twee typen beschikbare configuraties in Batch Hallo:

- Hallo **Virtuele-machineconfiguratie**, waarmee die Hallo van toepassingen bestaat uit de virtuele machines in Azure. Deze virtuele machines kunnen worden gemaakt met Linux- of Windows-installatiekopieën. 

    Wanneer u een groep op basis van virtuele-machineconfiguratie Hallo maakt, moet u niet alleen Hallo grootte van Hallo knooppunten en Hallo bron van Hallo installatiekopieën gebruikt toocreate ze, maar ook Hallo **verwijzing naar afbeelding van virtuele machine** en Hallo Batch **knooppunt agent SKU** toobe op Hallo knooppunten geïnstalleerd. Zie [Linux-rekenknooppunten in Azure Batch-pools inrichten](batch-linux-nodes.md) voor meer informatie over het opgeven van deze pooleigenschappen.

- Hallo **Cloud Services-configuratie**, waarmee die Hallo van toepassingen bestaat uit Azure Cloud Services-knooppunten. Cloud Services verstrekt *alleen* Windows-rekenknooppunten.

    Beschikbare besturingssystemen voor de configuratie voor Cloud Services-toepassingen worden vermeld in Hallo [Azure Gast OS releases en SDK compatibiliteit matrix](../cloud-services/cloud-services-guestos-update-matrix.md). Wanneer u een groep met Cloud Services-knooppunten maakt, moet u toospecify hello knooppuntgrootte en de bijbehorende *OS-familie*. Cloudservices zijn geïmplementeerde tooAzure sneller dan voor virtuele machines waarop Windows wordt uitgevoerd. Als u pools met Windows-rekenknooppunten wilt, zult u merken dat Cloud Services prestatievoordelen biedt wat de implementatietijd betreft.

    * Hallo *OS-familie* bepaalt ook welke versies van .NET Hello besturingssysteem zijn geïnstalleerd.
    * Als bij werkrollen in Cloud Services, kunt u een *versie van het besturingssysteem* (Zie voor meer informatie over werkrollen Hallo [laten weten over cloudservices](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) sectie in Hallo [Cloudservices overzicht](../cloud-services/cloud-services-choose-me.md)).
    * Als bij werkrollen, het is raadzaam dat u opgeeft `*` voor Hallo *besturingssysteemversie* zodat Hallo knooppunten automatisch worden bijgewerkt en er geen werk vereist toocater toonewly uitgebracht versies is. Hallo primaire gebruiksvoorbeeld voor het selecteren van een specifieke versie van het besturingssysteem is tooensure toepassingscompatibiliteit, waardoor de compatibiliteit met eerdere versies testen toobe uitgevoerd alvorens deze Hallo versie toobe bijgewerkt. Na de validatie, Hallo *besturingssysteemversie* voor Hallo van toepassingen kan worden bijgewerkt en Hallo nieuwe OS-installatiekopie kan worden geïnstalleerd--actieve taken worden onderbroken en opnieuw.

Wanneer u een groep maakt, moet u tooselect Hallo juiste **nodeAgentSkuId**, afhankelijk van Hallo OS van Hallo basisinstallatiekopie van uw VHD. U kunt een toewijzing van beschikbare knooppunt agent SKU-id's tootheir verwijzingen van de installatiekopie van het besturingssysteem ophalen door de aanroepende Hallo [lijst ondersteund knooppunt Agent-SKU's](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) bewerking.

Zie Hallo [Account](#account) sectie voor informatie over het instellen van Hallo groep toewijzing modus bij het maken van een Batch-account.

#### <a name="custom-images-for-virtual-machine-pools"></a>Aangepaste installatiekopieën voor VM-pools

toouse een aangepaste installatiekopie tooprovision virtuele Machine-adresgroepen maken uw Batch-account met de Hallo gebruikerabonnement groep toewijzing modus. Met deze modus worden toegewezen aan Batch-pools in Hallo abonnement waarin Hallo account zich bevindt. Zie Hallo [Account](#account) sectie voor informatie over het instellen van Hallo groep toewijzing modus bij het maken van een Batch-account.

een aangepaste installatiekopie toouse, moet u tooprepare Hallo afbeelding door het generaliseren. Zie voor meer informatie over het voorbereiden van aangepaste Linux-installatiekopieën van virtuele Azure-machines [vastleggen van een Azure Linux VM toouse als sjabloon](../virtual-machines/linux/capture-image-nodejs.md). Zie [Aangepaste VM-installatiekopieën maken met Azure PowerShell](../virtual-machines/windows/tutorial-custom-images.md) voor meer informatie over het maken van aangepaste Windows-installatiekopieën op basis van Azure VM's. 

> [!IMPORTANT]
> Houd er rekening mee Hallo volgende bij het voorbereiden van uw aangepaste installatiekopie:
> - Zorg ervoor dat die Hallo OS basisinstallatiekopie gebruik van uw Batch-pools biedt tooprovision niet hebben geen vooraf geïnstalleerde Azure-extensies, zoals Hallo aangepast Script-extensie. Als Hallo afbeelding een vooraf geïnstalleerde uitbreiding bevat, ondervinden Azure problemen Hallo VM implementeren.
> - Zorg ervoor dat Hallo OS basisinstallatiekopie die maakt gebruik van tijdelijke standaardstation Hallo bieden zoals hello Batch knooppunt agent momenteel Hallo standaard tijdelijke station verwacht.
>
>

een virtuele-machineconfiguratie van toepassingen met een aangepaste installatiekopie toocreate, moet u een of meer standaard Azure Storage-accounts toostore uw aangepaste VHD-installatiekopieën. Aangepaste installatiekopieën worden opgeslagen als blobs. uw aangepaste installatiekopieën bij het maken van een groep tooreference opgeven Hallo URI's van Hallo aangepaste installatiekopie VHD-blobs Hallo [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) eigenschap Hallo [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) eigenschap.

Zorg ervoor dat uw storage-accounts voldoen aan de volgende criteria Hallo:   

- Hallo storage-accounts met Hallo aangepaste installatiekopie VHD-blobs moeten toobe in Hallo hetzelfde abonnement als Hallo Batch-account (abonnement Hallo gebruiker).
- Hallo opgegeven opslagaccounts toobe in Hallo moeten dezelfde regio bevinden als Hallo Batch-account.
- Op dit moment worden alleen algemene standaardopslagaccounts ondersteund. In toekomstige hello Azure Premium-opslag ondersteund.
- U kunt één opslagaccount opgeven met meerdere aangepaste VHD-blobs of meerdere opslagaccounts die elk één blob hebben. We raden u toouse meerdere opslagaccounts tooget een betere prestaties.
- Een unieke aangepaste installatiekopie VHD-blob kan ondersteunen too40 die Linux VM-exemplaren of 20 Windows VM-exemplaren. U moet toocreate kopieën van Hallo VHD-blob toocreate groepen met meer virtuele machines. Bijvoorbeeld: een pool met 200 VM's van Windows 10 unieke VHD-blobs opgegeven voor Hallo moet **osDisk** eigenschap.

toocreate een pool van een aangepaste installatiekopie met hello Azure-portal:

1. Navigeer tooyour Batch-account in hello Azure-portal.
2. Op Hallo **instellingen** blade, selecteer Hallo **Pools** menu-item.
3. Op Hallo **Pools** blade, selecteer Hallo **toevoegen** opdracht; Hallo **van toepassingen toevoegen** blade wordt weergegeven.
4. Selecteer **aangepaste installatiekopie (Linux/Windows)** van Hallo **afbeeldingstype** vervolgkeuzelijst. Hallo-portal wordt weergegeven Hallo **aangepaste installatiekopie** objectkiezer. Kies een of meer virtuele harde schijven van Hallo dezelfde container en klikt u op Hallo **Selecteer** knop. 
    Ondersteuning voor meerdere VHD's van verschillende opslagaccounts en verschillende containers wordt in toekomstige hello toegevoegd.
5. Selecteer Hallo juist **aanbieding-Publisher-Sku** voor uw aangepaste VHD's, selecteert u Hallo gewenst **opslaan in cache** modus en vul alle Hallo andere parameters voor het Hallo-groep.
6. Als een groep is gebaseerd op een aangepaste installatiekopie Zie Hallo toocheck **besturingssysteem** eigenschap in Hallo resource samenvatting sectie Hallo **groep** blade. Hallo-waarde van deze eigenschap moet **aangepaste VM-installatiekopie**.
7. Alle aangepaste VHD's die zijn gekoppeld aan een groep worden weergegeven op van de pool Hallo **eigenschappen** blade.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Type rekenknooppunt en beoogd aantal knooppunten

Wanneer u een pool maakt, kunt u opgeven welke rekenknooppunten u wilt en doelaantal Hallo voor elk. rekenknooppunten Hello twee typen zijn:

- **Toegewezen rekenknooppunten.** Toegewezen rekenknooppunten zijn gereserveerd voor uw workloads. Ze zijn duurder dan prioriteit Laag knooppunten, maar ze zijn gegarandeerd toonever afgebroken.

- **Rekenknooppunten met lage prioriteit.** Knooppunten met lage prioriteit te profiteren van de overtollige capaciteit in Azure toorun uw Batch-workloads. Knooppunten met lage prioriteit zijn minder duur per uur dan toegewezen knooppunten en maken workloads mogelijk met veel rekencapaciteit. Zie voor meer informatie [VM's met lage prioriteit gebruiken met Batch](batch-low-pri-vms.md).

    Rekenknooppunten met lage prioriteit kunnen worden verschoven wanneer Azure onvoldoende overtollige capaciteit heeft. Als een knooppunt wordt afgebroken tijdens het uitvoeren van taken, zijn Hallo taken opnieuw en voer het opnieuw nadat een rekenknooppunt weer beschikbaar. Prioriteit Laag knooppunten zijn een goede optie voor werkbelastingen waarbij Hallo taak voltooiingstijd is flexibel en Hallo werk verdeeld over veel knooppunten. Voordat u toouse prioriteit Laag knooppunten voor uw scenario besluit, zorg ervoor dat er geen werk vanwege verloren toopreemption worden de minimale en eenvoudig toorecreate.

    Prioriteit Laag rekenknooppunten zijn alleen beschikbaar voor Batch-accounts die zijn gemaakt met de Hallo groep toewijzing modus ingesteld te**Batch-Service**.

U kunt beide prioriteit Laag en speciale rekenknooppunten hebben in Hallo dezelfde groep. Elk type knooppunt &mdash; prioriteit Laag en speciale &mdash; heeft een eigen doel-instelling waarvoor u Hallo gewenst aantal knooppunten kunt opgeven. 
    
Hallo aantal rekenknooppunten is waarnaar wordt verwezen tooas een *doel* omdat, in sommige situaties uw pool kan niet worden bereikt Hallo gewenst aantal knooppunten. Bijvoorbeeld een groep kan niet worden bereikt Hallo doel als het Hallo bereikt [kerngeheugenquotum](batch-quota-limit.md) voor uw Batch-account eerst. Of Hallo van toepassingen mogelijk niet Hallo doel bereiken als u een automatische schaling hebt toegepast formule toohello van toepassingen die Hallo kunt u het maximum aantal knooppunten beperkt.

Zie [Batch-prijzen](https://azure.microsoft.com/pricing/details/batch/) voor informatie over prijzen voor rekenknooppunten met lage prioriteit en toegewezen rekenknooppunten.

### <a name="size-of-hello-compute-nodes"></a>Grootte van rekenknooppunten Hallo

De grootte van rekenknooppunten met **Cloud Services-configuratie** wordt vermeld in [Groottes voor Cloud Services](../cloud-services/cloud-services-sizes-specs.md). Batch ondersteunt Cloud Services van alle grootten met uitzondering van `ExtraSmall`, `STANDARD_A1_V2` en `STANDARD_A2_V2`.

De grootte van rekenknooppunten met **virtuele-machineconfiguratie** wordt vermeld in [Groottes voor virtuele machines in Azure](../virtual-machines/linux/sizes.md) (Linux) en [Groottes voor virtuele machines in Azure](../virtual-machines/windows/sizes.md) (Windows). Batch ondersteunt alle Azure VM-groottes met uitzondering van `STANDARD_A0` en die met Premium Storage (de serie `STANDARD_GS`, `STANDARD_DS` en `STANDARD_DSV2`).

Als u de grootte van een compute-knooppunt, overweeg Hallo kenmerken en vereisten van Hallo toepassingen, u op Hallo knooppunten voert. Aspecten zoals of Hallo toepassing meerdere threads en hoeveel geheugen deze gebruikt, kunt bepalen Hallo meest geschikte en voordeligste knooppuntgrootte. Is het typische tooselect de grootte van een knooppunt ervan uitgaande dat één taak tegelijk op een knooppunt wordt uitgevoerd. Het is echter mogelijk toohave meerdere taken (en daarom meerdere exemplaren van een toepassing) [parallel worden uitgevoerd](batch-parallel-node-tasks.md) op rekenknooppunten tijdens het uitvoeren van de taak. In dit geval is het algemene toochoose een groter knooppunt grootte tooaccommodate Hallo toegenomen vraag van de uitvoering van parallelle taken. Zie [Taak planningsbeleid](#task-scheduling-policy) voor meer informatie.

Alle knooppunten in een pool Hallo zijn Hallo dezelfde grootte. Als u van plan toorun toepassingen met verschillende systeemvereisten bent en/of workloadniveaus, raden wij aan dat u afzonderlijke pools.

### <a name="scaling-policy"></a>Beleid voor vergroten/verkleinen

Voor dynamische werkbelastingen kunt u schrijven en instellen dat een [formule voor automatisch schalen](#scaling-compute-resources) tooa van toepassingen. Hallo Batch-service wordt periodiek evalueert de formule en past u Hallo aantal knooppunten binnen Hallo-groep op basis van verschillende pool, Jobs en taakparameters die u kunt opgeven.

### <a name="task-scheduling-policy"></a>Taakplanningsbeleid

Hallo [maximum aantal taken per knooppunt](batch-parallel-node-tasks.md) configuratieoptie Hallo kunt u het maximum aantal taken dat parallel kan worden uitgevoerd op elk rekenknooppunt in Hallo pool bepaalt.

Hallo standaardconfiguratie bevat één taak tegelijk op een knooppunt wordt uitgevoerd, maar er zijn er twee of meer taken gelijktijdig uitgevoerd op een knooppunt zijn scenario's waarin het nuttig toohave. Zie Hallo [voorbeeldscenario](batch-parallel-node-tasks.md#example-scenario) in Hallo [knooppunt gelijktijdige taken](batch-parallel-node-tasks.md) artikel toosee hoe u van meerdere taken per knooppunt profiteren kunt.

U kunt ook opgeven een *opvultype* die bepaalt of Batch Hallo taken gelijkmatig verspreid over alle knooppunten in een pool of elk knooppunt met het maximum aantal taken Hallo packs alvorens taken tooanother knooppunt toe te wijzen.

### <a name="communication-status-for-compute-nodes"></a>Communicatiestatus voor rekenknooppunten

In de meeste gevallen taken onafhankelijk functioneren en hoeft niet toocommunicate met elkaar. Maar mogelijk hebt u ook toepassingen waarin taken moeten communiceren, bijvoorbeeld [MPI-scenario's](batch-mpi.md).

U kunt een pool tooallow **communicatie tussen knooppunten**, zodat de knooppunten in een pool tijdens runtime kunnen communiceren. Wanneer communicatie tussen knooppunten is ingeschakeld, kunnen knooppunten in de configuratie voor Cloud Services-pools met elkaar communiceren op poorten die groter zijn dan 1100. Voor virtuele-machineconfiguratiepools is verkeer op geen enkele poort beperkt.

Vergeet niet dat het inschakelen van communicatie tussen knooppunten ook heeft impact op Hallo plaatsing van Hallo knooppunten binnen clusters en Hallo kunt u het maximum aantal knooppunten in een pool vanwege beperkingen voor implementatie beperkt mogelijk. Als uw toepassing geen communicatie tussen knooppunten is vereist, Hallo Batch-service kan worden toegewezen een potentieel grote aantal knooppunten toohello toepassingen vanuit vele verschillende clusters en datacenters tooenable meer parallelle verwerkingskracht.

### <a name="start-tasks-for-compute-nodes"></a>Begintaken voor rekenknooppunten

Hallo optionele *begintaak* wordt op elk knooppunt worden uitgevoerd zoals u dat knooppunt aan Hallo-pool wordt toegevoegd en telkens wanneer een knooppunt opnieuw wordt opgestart of hersteld met een installatiekopie. Hallo begintaak is vooral nuttig voor het voorbereiden van rekenknooppunten voor uitvoering van taken, zoals het installeren van Hallo-toepassingen die de taken worden uitgevoerd op rekenknooppunten Hallo Hallo.

### <a name="application-packages"></a>Toepassingspakketten

U kunt opgeven [toepassingspakketten](#application-packages) toodeploy toohello rekenknooppunten in Hallo van toepassingen. Toepassingspakketten biedt vereenvoudigde implementatie en versiebeheer van Hallo-toepassingen die de taken worden uitgevoerd. Toepassingspakketten die u voor een groep van toepassingen opgeeft, worden geïnstalleerd op elk knooppunt dat lid wordt van de groep, en elke keer dat er een knooppunt opnieuw wordt opgestart of er een installatiekopie wordt hersteld.

> [!NOTE]
> Toepassingspakketten worden ondersteund in alle Batch-pools die na 5 juli 2017 zijn gemaakt. Ze worden ondersteund in de Batch-pools tussen 10 maart 2016 en 5 juli 2017 alleen gemaakt als Hallo-groep is gemaakt met behulp van de configuratie van een Service in de Cloud. Batch-pools gemaakt voorafgaande too10 maart 2016 bieden geen ondersteuning voor toepassingspakketten. Zie voor meer informatie over het gebruik van de toepassing toodeploy uw toepassingen tooyour Batch knooppunten pakketten, [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Netwerkconfiguratie

U kunt opgeven dat Hallo subnet van een Azure [virtueel netwerk (VNet)](../virtual-network/virtual-networks-overview.md) aan van welke groep Hallo compute knooppunten moeten worden gemaakt. Zie Hallo [groep netwerkconfiguratie](#pool-network-configuration) sectie voor meer informatie.


## <a name="job"></a>Job
Een job is een verzameling taken. Hiermee kunt beheren hoe een berekening wordt uitgevoerd door de taken op Hallo van rekenknooppunten in een pool.

* Hallo job bepaalt Hallo **groep** in welke Hallo werk toobe uitgevoerd wordt. U kunt voor elke job een nieuwe pool maken of één groep gebruiken voor een groot aantal jobs. U kunt een pool maken voor elke job die aan een jobplanning is gekoppeld, maar ook voor alle jobs die aan een jobplanning zijn gekoppeld.
* U kunt desgewenst een **jobprioriteit** opgeven. Wanneer een taak wordt verzonden met een hogere prioriteit dan de taken die momenteel uitgevoerd worden, worden Hallo taken voor Hallo hogere prioriteit job ingevoegd in de wachtrij Hallo tevoren taken voor Hallo lagere prioriteit taken. Taken met lagere prioriteit die al worden uitgevoerd, kunnen niet worden verschoven.
* U kunt taak **beperkingen** toospecify bepaalde limieten aan uw taken:

    U kunt instellen een **maximale kloktijd**, zodat als een taak wordt uitgevoerd langer dan Hallo maximale kloktijd die is opgegeven, Hallo taak en alle bijbehorende taken zijn beëindigd.

    Batch kan dit detecteren en vervolgens de mislukte taken opnieuw uitvoeren. U kunt opgeven dat Hallo **maximum aantal pogingen** als een beperking, met inbegrip van of de taak wordt *altijd* of *nooit* opnieuw geprobeerd. Een taak opnieuw wordt geprobeerd betekent die taak Hallo opnieuw toobe opnieuw uitvoeren.
* De clienttoepassing taken tooa taak kunt toevoegen, of kunt u een [jobbeheertaak](#job-manager-task). Een jobbeheertaak Hallo-informatie die nodig toocreate Hallo vereiste taken voor een taak bevat, met Hallo jobbeheertaak wordt uitgevoerd op een Hallo rekenknooppunten in Hallo van toepassingen. Hallo jobbeheertaak wordt verwerkt specifiek door Batch--het zich in de wachtrij als Hallo-taak wordt gemaakt en opnieuw wordt opgestart als deze uitvalt. Een jobbeheertaak is *vereist* voor taken die zijn gemaakt door een [taakschema](#scheduled-jobs) omdat het Hallo alleen manier toodefine Hallo taken voordat Hallo job wordt geïnstantieerd.
* Standaard blijven taken in de actieve status Hallo wanneer alle taken in Hallo job voltooid zijn. U kunt dit gedrag wijzigen zodat hello taak wordt automatisch beëindigd wanneer alle taken in Hallo job voltooid zijn. Set Hallo taak **onAllTasksComplete** eigenschap ([OnAllTasksComplete] [ net_onalltaskscomplete] in Batch .NET) te*terminatejob* tooautomatically Hallo taak beëindigen wanneer alle taken voltooid Hallo status heeft zijn.

    Houd er rekening mee dat Hallo Batch-service een taak met acht *geen* taken toohave alle taken worden voltooid. Daarom wordt deze optie meestal gebruikt met een [Jobbeheertaak](#job-manager-task). Als u wilt dat toouse automatische taak beëindiging zonder een job manager, moet u in eerste instantie van een nieuwe taak instellen **onAllTasksComplete** eigenschap te*noaction*, te stellen*terminatejob* alleen als u klaar bent met het toevoegen van taken toohello taak.

### <a name="job-priority"></a>Jobprioriteit
U kunt een prioriteit toojobs die u in Batch maakt toewijzen. Hallo Batch-service gebruikt Hallo prioriteitswaarde Hallo taak toodetermine Hallo volgorde van de jobplanning binnen een account (dit is geen toobe verward met een [geplande taak](#scheduled-jobs)). Hallo prioriteitswaarden variëren van-1000 too1000, met-1000 Hallo laagste prioriteit en 1000 Hallo hoogste. tooupdate hello prioriteit van een taak, aanroep Hallo [Hallo eigenschappen van een job bijwerken] [ rest_update_job] bewerking (Batch REST), of wijzig Hallo [CloudJob.Priority] [ net_cloudjob_priority] eigenschap (Batch .NET).

Binnen Hallo dezelfde account, hogere prioriteit taken planningsvoorrang op taken met lagere prioriteit. Een job met hogere prioriteit in het ene account heeft geen planningsvoorrang op een andere job met een lagere prioriteitswaarde in een ander account.

De jobplanning tussen pools verloopt onafhankelijk. Tussen verschillende pools is er geen garantie dat een job met hogere prioriteit eerst wordt gepland als de gekoppelde pool over te weinig niet-actieve knooppunten beschikt. In Hallo dezelfde groep taken Hello dezelfde prioriteit evenveel kans om gepland hebben.

### <a name="scheduled-jobs"></a>Geplande jobs
[Taak planningen] [ rest_job_schedules] kunt u toocreate terugkerende taken binnen Hallo Batch-service. Een jobplanning geeft aan wanneer toorun taken en bevat Hallo specificaties voor Hallo taken toobe uitvoeren. U Hallo duur van het schema Hallo--kunt opgeven hoe lang en wanneer Hallo planning--actief is en hoe vaak de taken worden gemaakt tijdens het Hallo geplande periode.

## <a name="task"></a>Taak
Een taak is een rekeneenheid die aan een job is gekoppeld. Deze wordt uitgevoerd op een knooppunt. Taken tooa knooppunt voor uitvoering zijn toegewezen, of tot een knooppunt beschikbaar in de wachtrij staan. Eenvoudig gesteld: een taak wordt uitgevoerd een of meer programma's of scripts op een compute knooppunt tooperform Hallo werk die u nodig hebt.

Wanneer u een taak maakt, kunt u het volgende opgeven:

* Hallo **opdrachtregel** voor Hallo-taak. Dit is Hallo-opdrachtregel die uw toepassing of het script op Hallo rekenknooppunt uitvoert.

    Het is belangrijk toonote die vanaf de opdrachtregel Hallo niet daadwerkelijk wordt uitgevoerd onder een shell. Daarom deze kan niet systeemeigen kan profiteren van shellfuncties zoals [omgevingsvariabele](#environment-settings-for-tasks) uitbreiding (dit omvat Hallo `PATH`). tootake profiteren van deze functies, u moet aanroepen Hallo-shell op de opdrachtregel Hallo--bijvoorbeeld beschadigt door `cmd.exe` op Windows-knooppunten of `/bin/sh` op Linux:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Als uw taken toorun moeten een toepassing of het script dat zich niet in het knooppunt Hallo `PATH` of verwijzen naar omgevingsvariabelen, roepen Hallo shell expliciet in Hallo taak vanaf de opdrachtregel.
* **Bronbestanden** die Hallo gegevens toobe verwerkt bevatten. Deze bestanden worden automatisch gekopieerd toohello knooppunt van Blob storage in een algemeen Azure Storage-account voordat de opdrachtregel van Hallo taak wordt uitgevoerd. Zie voor meer informatie, Hallo secties [begintaak](#start-task) en [bestanden en mappen](#files-and-directories).
* Hallo **omgevingsvariabelen** die worden vereist door uw toepassing. Zie voor meer informatie, Hallo [omgevingsinstellingen voor taken](#environment-settings-for-tasks) sectie.
* Hallo **beperkingen** onder welke Hallo taak moet worden uitgevoerd. Beperkingen zijn bijvoorbeeld Hallo maximumtijd die taak Hallo toorun, Hallo kunt u het maximum aantal keren dat een mislukte taak moet opnieuw worden geprobeerd, is toegestaan en Hallo maximum tijd die bestanden in de werkmap van de taak Hallo worden bewaard.
* **Toepassingspakketten** toodeploy toohello-rekenknooppunt op welke Hallo taak geplande toorun is. [Toepassingspakketten](#application-packages) bieden vereenvoudigde implementatie en versiebeheer van Hallo-toepassingen die de taken worden uitgevoerd. Taak niveau toepassingspakketten zijn vooral nuttig in de gedeelde groep omgevingen, waarbij verschillende taken worden uitgevoerd op één groep en het Hallo-groep is niet verwijderd wanneer een taak is voltooid. Als uw project minder taken dan knooppunten in de groep hello heeft, minimaliseren taak toepassingspakketten gegevensoverdracht sinds de toepassing is geïmplementeerd alleen toohello knooppunten die taken uitvoeren.

Bovendien tootasks u tooperform berekeningen definiëren op een knooppunt, Hallo volgende speciale taken worden ook geleverd door Hallo Batch-service:

* [Begintaak](#start-task)
* [Jobbeheertaak](#job-manager-task)
* [Jobvoorbereidingstaken en jobvrijgevingstaken](#job-preparation-and-release-tasks)
* [Taken met meerdere instanties (MPI)](#multi-instance-tasks)
* [Taakafhankelijkheden](#task-dependencies)

### <a name="start-task"></a>Begintaak
Door het koppelen van een **begintaak** aan een pool Hallo besturingsomgeving van de knooppunten ervan kan worden voorbereid. U kunt bijvoorbeeld bewerkingen zoals het installeren van Hallo-toepassingen die de taken worden uitgevoerd of het starten van achtergrondprocessen uitvoeren. Hallo begintaak wordt uitgevoerd telkens wanneer een knooppunt wordt gestart, voor zolang deze in de groep Hallo blijft--inclusief als Hallo-knooppunt wordt eerst toegevoegd toohello pool en wordt opnieuw opgestart of hersteld met een installatiekopie.

Een belangrijk voordeel van de begintaak Hallo is het kan alle Hallo-informatie die nodig zijn tooconfigure een rekenknooppunt bevatten en Hallo toepassingen installeren die vereist voor de uitvoering van de taak zijn. Daarom is het zo eenvoudig hello nieuw doelaantal knooppunten geven Hallo aantal knooppunten in een pool te verhogen. Hallo begintaak bevat Hallo Batch-service Hallo informatie die is vereist tooconfigure Hallo nieuwe knooppunten en ze gereed zijn voor het accepteren van taken.

Als met een Azure Batch-taak, kunt u een lijst met **bronbestanden** in [Azure Storage][azure_storage], Daarnaast tooa **opdrachtregel** toobe uitgevoerd. Hallo Batch-service eerst bestanden Hallo-toohello bronknooppunt opgehaald uit Azure Storage en Hallo vanaf de opdrachtregel wordt uitgevoerd. Voor een begintaak van toepassingen bevat Hallo bestandenlijst meestal Hallo taaktoepassing en de bijbehorende afhankelijkheden.

Hallo begintaak kan echter ook verwijzing gegevens toobe gebruikt door alle taken die worden uitgevoerd op het rekenknooppunt Hallo. Bijvoorbeeld, een begintaak opdrachtregel kan uitvoeren een `robocopy` bewerking toocopy toepassingsbestanden (die zijn opgegeven als bronbestanden en gedownload toohello knooppunt) van Hallo begintaak van [werkmap](#files-and-directories) toohello [gedeelde map](#files-and-directories), en voer vervolgens een MSI of `setup.exe`.

Het is doorgaans wenselijk Hallo Batch-service toowait voor Hallo start taak toocomplete voordat u overweegt Hallo knooppunt gereed toobe toegewezen taken, maar u kunt dit configureren.

Als een begintaak op een rekenknooppunt mislukt, klikt u vervolgens hello status van Hallo-knooppunt is bijgewerkte tooreflect Hallo fout en Hallo-knooppunt is niet toegewezen aan alle taken. Een begintaak kan mislukken als er is een probleem dat de resource-bestanden zijn gekopieerd uit de opslag, of als het Hallo-proces dat wordt uitgevoerd door de opdrachtregel ervan retourneert een afsluitcode die niet nul zijn.

Als u toevoegen of bijwerken van de begintaak Hallo voor een bestaande pool, moet u de rekenknooppunten voor Hallo taak toobe toegepast toohello beginknooppunten opnieuw worden opgestart.

>[!NOTE]
> Hallo totale grootte van een begintaak moet kleiner zijn dan of gelijk too32768 tekens, inclusief bronbestanden en omgevingsvariabelen. tooensure uw begintaak aan deze voorwaarde voldoet, kunt u een van twee methoden:
>
> 1. U kunt toepassing pakketten toodistribute toepassingen of gegevens in elk knooppunt in uw Batch-pool. Zie voor meer informatie over toepassingspakketten [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).
> 2. U kunt handmatig een ZIP-archief maken dat uw toepassingsbestanden bevat. Upload het ZIP-archief tooAzure opslag als een blob. Hallo ZIP-archief opgeven als een bronbestand voor de taak is gestart. Voordat u Hallo vanaf de opdrachtregel voor de taak is gestart uitvoert, pak Hallo-archief van Hallo vanaf de opdrachtregel. 
>
>    toounzip hello archiveren, kunt u Hallo archiveren hulpprogramma van uw keuze. U moet tooinclude Hallo hulpprogramma dat u toounzip Hallo archief als een bronbestand voor de begintaak Hallo gebruiken.
>
>

### <a name="job-manager-task"></a>Jobbeheertaak
Doorgaans gebruikt u een **jobbeheertaak** toocontrol en/of de monitor uitvoering--bijvoorbeeld toocreate taak en verzenden Hallo taken voor een job, bepalen van aanvullende taken toorun en bepalen wanneer werk is voltooid. Een jobbeheertaak is echter niet beperkt toothese activiteiten. Het is een volledig uitgewerkte taak die alle acties die vereist voor het Hallo-taak zijn kan uitvoeren. Een jobbeheertaak kan bijvoorbeeld een bestand downloaden dat is opgegeven als een parameter, Hallo inhoud van het bestand analyseren en aanvullende taken die op basis van die inhoud verzenden.

Een jobbeheertaak wordt vóór alle andere taken gestart. Het biedt Hallo volgende kenmerken:

* Het wordt automatisch verzonden als een taak door Hallo Batch-service wanneer Hallo-taak wordt gemaakt.
* Deze geplande tooexecute voordat Hallo andere taken in een job is.
* Het hieraan gekoppelde knooppunt is de laatste toobe Hallo verwijderd uit een pool wanneer Hallo-pool wordt verkleind.
* De beëindiging ervan kan worden gebonden toohello beëindiging van alle taken in Hallo-taak.
* Een jobbeheertaak krijgt de hoogste prioriteit Hallo zo nodig toobe opnieuw gestart. Als een niet-actief knooppunt niet beschikbaar is, Hallo Batch-service mogelijk beëindigen een Hallo andere taken worden uitgevoerd in Hallo groep toomake ruimte voor Hallo job manager taak toorun.
* Een jobbeheertaak in één taak heeft geen prioriteit via Hallo taken van andere jobs. Tussen jobs worden alleen prioriteiten op jobniveau in acht genomen.

### <a name="job-preparation-and-release-tasks"></a>Jobvoorbereidingstaken en jobvrijgevingstaken
Batch biedt jobvoorbereidingstaken om de job in te stellen voordat deze wordt uitgevoerd. Jobvrijgevingstaken zijn er voor onderhoud of opschoning nadat de job is uitgevoerd.

* **Jobvoorbereidingstaak**: een jobvoorbereidingstaak wordt uitgevoerd op alle rekenknooppunten die gepland toorun taken zijn, voordat een Hallo andere taken worden uitgevoerd. U kunt een voorbereiding taak toocopy taakgegevens die wordt gedeeld door alle taken, maar is de unieke toohello taak, bijvoorbeeld gebruiken.
* **Jobvrijgevingstaak**: wanneer een taak is voltooid, wordt een jobvrijgevingstaak uitgevoerd op elk knooppunt in Hallo pool dat ten minste één taak uitgevoerd. U kunt een taak release taak toodelete gegevens die door de jobvoorbereidingstaak Hallo worden gekopieerd of toocompress en uploaden diagnostische logboekgegevens bijvoorbeeld gebruiken.

Beide taken voorbereiden en release taken kunt u een opdrachtregel toorun toospecify wanneer het Hallo-taak wordt aangeroepen. Ze bieden functies zoals het downloaden van bestanden, uitvoering met verhoogde bevoegdheden, aangepaste omgevingsvariabelen, maximale uitvoeringsduur, aantal pogingen en bewaartijd voor bestanden.

Zie [Run job preparation and completion tasks on Azure Batch compute nodes](batch-job-prep-release.md) (Jobvoorbereidings- en jobvrijgevingstaken uitvoeren op Azure Batch-rekenknooppunten) voor meer informatie over jobvoorbereidings- en jobvrijgevingstaken.

### <a name="multi-instance-task"></a>Taak met meerdere instanties
Een [taak met meerdere instanties](batch-mpi.md) is een taak die is geconfigureerd toorun op meer dan één rekenknooppunt tegelijk. Taken met meerdere instanties, kunt u high-performance computing-scenario's waarvoor een groep rekenknooppunten die zijn toegewezen samen tooprocess één workload (zoals Message Passing Interface (MPI)).

Bekijk voor een gedetailleerde discussie over het uitvoeren van MPI-jobs in Batch met behulp van de Batch .NET-bibliotheek Hallo [gebruik meerdere exemplaren taken toorun Message Passing Interface (MPI) applications in Azure Batch](batch-mpi.md).

### <a name="task-dependencies"></a>Taakafhankelijkheden
[Taakafhankelijkheden](batch-task-dependencies.md), als Hallo naam al aangeeft, kunt u toospecify die een taak van Hallo voltooiing van andere taken voordat deze wordt uitgevoerd afhangt. Deze functie biedt ondersteuning voor situaties waarin een 'downstream' verbruik Hallo uitvoer van een 'upstream'-taak-- of wanneer een upstream-taak initialisaties uitvoert die is vereist voor een downstream-taak. toouse deze functie moet u eerst taakafhankelijkheden van inschakelen op uw Batch-job. Klik vervolgens voor elke taak die afhankelijk zijn van een andere (of vele andere), u Hallo-taken die u die taak afhankelijk opgeven.

Bij taakafhankelijkheden, kunt u scenario's zoals Hallo volgende configureren:

* *taakB* hangt af van *taakA* (*taakB* kan pas worden uitgevoerd nadat *taakA* is voltooid).
* *taakC* is afhankelijk van *taakA* én *taakB*.
* *taakD* is afhankelijk van een bereik van taken, zoals taken *1* t/m *10*, voordat deze wordt uitgevoerd.

Bekijk [taakafhankelijkheden in Azure Batch](batch-task-dependencies.md) en Hallo [taakafhankelijkheden] [ github_sample_taskdeps] codevoorbeeld in Hallo [azure-batch-samples] [ github_samples] GitHub-opslagplaats voor meer gedetailleerde informatie over deze functie.

## <a name="environment-settings-for-tasks"></a>Omgevingsinstellingen voor taken
Elke taak uitgevoerd door Hallo Batch-service heeft toegang tot tooenvironment variabelen die wordt ingesteld op rekenknooppunten. Dit omvat omgevingsvariabelen die zijn gedefinieerd door Hallo Batch-service ([service gedefinieerde][msdn_env_vars]) en de aangepaste variabelen die u voor uw taken kunt definiëren. Hallo-toepassingen en scripts die uw taken uitvoeren en hebt toegang toothese omgevingsvariabelen tijdens de uitvoering.

U kunt aangepaste omgevingsvariabelen instellen op Hallo taak niveau door in te vullen Hallo *omgevingsinstellingen* eigenschap voor deze entiteiten. Zie bijvoorbeeld Hallo [toevoegen van een taak tooa] [ rest_add_task] bewerking (Batch REST-API) of Hallo [CloudTask.EnvironmentSettings] [ net_cloudtask_env] en [ CloudJob.CommonEnvironmentSettings] [ net_job_env] eigenschappen in Batch .NET.

Uw clienttoepassing of service kunt verkrijgen van een taak omgevingsvariabelen, zowel service gedefinieerde en aangepaste, met Hallo [informatie ophalen over een taak] [ rest_get_task_info] bewerking (Batch REST) of door het openen van Hallo [CloudTask.EnvironmentSettings] [ net_cloudtask_env] eigenschap (Batch .NET). Processen die worden uitgevoerd op een rekenknooppunt toegang heeft tot deze en andere omgevingsvariabelen op Hallo knooppunt, bijvoorbeeld met behulp van Hallo bekend `%VARIABLE_NAME%` (Windows) of `$VARIABLE_NAME` (Linux)-syntaxis.

Een volledige lijst van alle gedefinieerde omgevingsvariabelen vindt u in [Compute node environment variables][msdn_env_vars] (Knooppuntomgevingsvariabelen berekenen).

## <a name="files-and-directories"></a>Bestanden en mappen
Elke taak heeft een *werkmap* waaronder nul of meer bestanden en mappen worden gemaakt. Deze werkmap kan worden gebruikt voor het opslaan van Hallo programma dat wordt uitgevoerd op Hallo taak Hallo-gegevens die erdoor worden verwerkt, en Hallo uitvoer van Hallo verwerking die wordt uitgevoerd. Alle bestanden en mappen van een taak zijn eigendom van Hallo taak gebruiker.

Hallo Batch-service geeft een deel van het bestandssysteem Hallo op een knooppunt als Hallo *hoofdmap*. Taken kunnen toegang krijgen tot hoofdmap Hallo Hallo verwijzende `AZ_BATCH_NODE_ROOT_DIR` omgevingsvariabele. Zie [Omgevingsinstellingen voor taken](#environment-settings-for-tasks) voor meer informatie over het gebruik van omgevingsvariabelen.

Hallo-hoofdmap bevat Hallo directory-structuur te volgen:

![Mapstructuur rekenknooppunt][1]

* **gedeelde**: deze map biedt lees-/ schrijftoegang te*alle* taken die worden uitgevoerd op een knooppunt. Elke taak die wordt uitgevoerd op Hallo knooppunt kunt maken, lezen, bijwerken en verwijderen van bestanden in deze map. Taken toegang tot deze map door te verwijzen naar Hallo `AZ_BATCH_NODE_SHARED_DIR` omgevingsvariabele.
* **startup**: deze map wordt door een begintaak gebruikt als werkmap. Alle Hallo-bestanden die gedownload toohello knooppunt Hallo begintaak zijn worden hier opgeslagen. Hallo begintaak kunt maken, lezen, bijwerken en verwijderen van bestanden in deze map. Taken toegang tot deze map door te verwijzen naar Hallo `AZ_BATCH_NODE_STARTUP_DIR` omgevingsvariabele.
* **Taken**: een map gemaakt voor elke taak die wordt uitgevoerd op Hallo-knooppunt. Deze is geopend door te verwijzen naar Hallo `AZ_BATCH_TASK_DIR` omgevingsvariabele.

    Binnen elk taakmap maakt Hallo Batch-service een werkmap (`wd`) waarvan het unieke pad wordt opgegeven door Hallo `AZ_BATCH_TASK_WORKING_DIR` omgevingsvariabele. Deze map biedt lees-/ schrijffout toegang toohello taak. Hallo-taak kunt maken, lezen, bijwerken en verwijderen van bestanden in deze map. Deze map blijft behouden op basis van Hallo *RetentionTime* beperking die is opgegeven voor het Hallo-taak.

    `stdout.txt`en `stderr.txt`: deze bestanden tijdens het uitvoeren van taak Hallo Hallo toohello taakmap geschreven.

> [!IMPORTANT]
> Wanneer een knooppunt wordt verwijderd uit groep hello, *alle* Hallo bestanden die zijn opgeslagen op Hallo knooppunt worden verwijderd.
>
>

## <a name="application-packages"></a>Toepassingspakketten
Hallo [toepassingspakketten](batch-application-packages.md) functie biedt eenvoudig beheren en implementeren van toepassingen toohello rekenknooppunten in uw pools. U kunt uploaden en beheren van meerdere versies van het Hallo-toepassingen worden uitgevoerd door uw taken, zoals de binaire bestanden en ondersteuningsbestanden. Vervolgens kunt u een automatisch implementeren of meer van deze toepassingen toohello rekenknooppunten in uw groep.

U kunt toepassingspakketten op Hallo van toepassingen en taak niveau opgeven. Wanneer u toepassingspakketten groep opgeeft, is toepassing hello geïmplementeerde tooevery knooppunt in Hallo pool. Wanneer u toepassingspakketten taak opgeeft, Hallo toepassing is geïmplementeerd alleen toonodes die gepland toorun ten minste één van Hallo projecttaken zijn, net vóór Hallo de opdrachtregel van de taak wordt uitgevoerd.

Batch-ingangen Hallo samenwerking met Azure Storage toostore uw toepassingspakketten en implementeer ze toocompute knooppunten, zodat uw code en de beheer-overhead kan worden vereenvoudigd.

toofind voor meer informatie over de functie Hallo, Bekijk [implementeren van toepassingen toocompute knooppunten met Batch-toepassingspakketten](batch-application-packages.md).

> [!NOTE]
> Als u toepassingen toepassing pakketten tooan toevoegt *bestaande* groep, moet u de rekenknooppunten opnieuw opstarten voor de toepassing hello-toobe geïmplementeerd toohello knooppunten pakketten.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Levensduur van pool en rekenknooppunt
Wanneer u uw Azure Batch-oplossing ontwerpt, hebt u toomake een ontwerpbeslissing over hoe en wanneer pools worden gemaakt en hoe lang rekenknooppunten in die pools beschikbaar blijven.

Op één end van Hallo spectrum, kunt u een groep maken voor elke taak die u verzendt en Hallo-groep verwijderen zodra de taken uitgevoerd zijn. Dit gebruik geoptimaliseerd omdat Hallo knooppunten alleen worden toegewezen wanneer nodig en als ze inactief zijn afgesloten. Hoewel dit betekent dat Hallo-taak moet wachten tot Hallo knooppunten toobe toegewezen, is het belangrijk toonote die taken zijn gepland voor uitvoering als knooppunten afzonderlijk beschikbaar zijn, toegewezen zijn, en Hallo is begintaak voltooid. Batch biedt *niet* wacht totdat alle knooppunten in een pool beschikbaar zijn alvorens taken toe te wijzen toohello knooppunten. Hiermee zorgt u voor maximaal gebruik van alle beschikbare knooppunten.

Op Hallo andere einde van het spectrum hello, als onmiddellijk starten van Jobs de hoogste prioriteit hello, u kunt een pool tevoren maken en de knooppunten ervan beschikbaar maken voordat jobs worden verzonden. In dit scenario taken onmiddellijk kunnen starten, maar knooppunten mogelijk inactief tijdens het wachten tot ze toobe toegewezen.

Een gecombineerde benadering wordt meestal gebruikt voor het verwerken van een variabele, maar continue workload. U kunt een pool dat meerdere taken om te worden verzonden, maar Hallo aantal knooppunten kunnen worden geschaald omhoog of omlaag toohello job workload volgens hebben (Zie [schaal rekenresources](#scaling-compute-resources) in Hallo volgende sectie). U kunt dit reactief doen, op basis van de huidige workload, of proactief als de workload kan worden voorspeld.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Configuratie van virtuele netwerken (VNet) en firewalls 

Wanneer u een pool van rekenknooppunten in Azure Batch inricht, kunt u Hallo pool koppelen aan een subnet van een Azure [virtueel netwerk (VNet)](../virtual-network/virtual-networks-overview.md). toolearn meer informatie over het maken van een VNet met subnetten, Zie [maken van een virtuele Azure-netwerk met subnetten](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Hallo VNet dat is gekoppeld aan een pool moet zijn:

   * In dezelfde Azure Hallo **regio** als hello Azure Batch-account.
   * Hallo in dezelfde **abonnement** als hello Azure Batch-account.

* Hallo type VNet ondersteund, is afhankelijk van hoe groepen worden toegewezen voor Hallo Batch-account:

    - Als Hallo groep toewijzing modus voor uw Batch-account tooBatch Service is ingesteld, wordt u een VNet-toopools alleen gemaakt met de Hallo kunt toewijzen **Cloud Services-configuratie**. Bovendien opgegeven Hallo dat vnet met het klassieke implementatiemodel Hallo moet worden gemaakt. VNets die zijn gemaakt met Azure Resource Manager-implementatiemodel Hallo worden niet ondersteund.
 
    - Als Hallo groep toewijzing modus voor uw Batch-account tooUser abonnement is ingesteld, wordt u een VNet-toopools alleen gemaakt met de Hallo kunt toewijzen **Virtuele-machineconfiguratie**. Groepen die zijn gemaakt met de Hallo **Cloud serviceconfiguratie** worden niet ondersteund. Hallo die gekoppeld VNet kan worden gemaakt met Azure Resource Manager-implementatiemodel Hallo of Hallo klassieke implementatiemodel.

    Zie voor een tabel samenvatten VNet ondersteuning volgens toopool toewijzing modus Hallo [groep toewijzing modus](#pool-allocation-mode) sectie.

* Als Hallo groep toewijzing modus voor uw Batch-account is tooBatch Service ingesteld, moet u opgeven machtigingen voor Batch-service-principal tooaccess Hallo Hallo VNet. Hallo VNet moet toewijzen Hallo [Classic Virtual Machine Contributor Role-Based toegangsbeheer (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) rol toohello Batch-service-principal. Als Hallo RBAC-rol niet is opgegeven opgegeven, retourneert Hallo Batch-service 400 (ongeldige aanvraag). tooadd hello rol in hello Azure-portal:

    1. Selecteer Hallo **VNet**, klikt u vervolgens **toegangsbeheer (IAM)** > **rollen** > **Virtual Machine Contributor**  >  **Toevoegen**.
    2. Op Hallo **machtigingen toevoegen** blade, selecteer Hallo **Virtual Machine Contributor** rol.
    3. Op Hallo **machtigingen toevoegen** blade, zoekt u Hallo Batch-API. Zoeken op zijn beurt voor elk van deze tekenreeksen totdat u Hallo-API:
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. Nieuwere Azure AD-tenants kunnen deze naam gebruiken.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** Hallo-id voor Hallo Batch-API. 
    3. Selecteer Hallo Batch-API service-principal. 
    4. Klik op **Opslaan**.

        ![Inzender VM-rol tooBatch service-principal toewijzen](./media/batch-api-basics/iam-add-role.png)


* Hallo opgegeven subnet moet er voldoende vrije **IP-adressen** tooaccommodate totaal aantal doelknooppunten Hallo; dat wil zeggen de som van Hallo Hallo `targetDedicatedNodes` en `targetLowPriorityNodes` eigenschappen van Hallo-groep. Hallo-subnet geen voldoende beschikbare IP-adressen, Hallo Batch-service gedeeltelijk Hallo-rekenknooppunten in Hallo pool toewijst als resulteert in een fout formaat.

* Hallo opgegeven subnet moet toestaan-communicatie van Hallo Batch-service toobe kunnen tooschedule taken op rekenknooppunten Hallo. Als de communicatie toohello rekenknooppunten is geweigerd door een **Netwerkbeveiligingsgroep (NSG)** hello VNet, gekoppeld en vervolgens Hallo Batch-service Hallo status van de rekenknooppunten Hallo te stelt**onbruikbaar**.

* Als Hallo opgegeven VNet is gekoppeld **Netwerkbeveiligingsgroepen (nsg's)** en/of een **firewall**, en vervolgens enkele gereserveerd voor het systeem-poorten moeten worden ingeschakeld om binnenkomende communicatie:

- Voor pools die zijn gemaakt met een virtuele-machineconfiguratie schakelt u poort 29876 en 29877 in, evenals poort 22 voor Linux en poort 3389 voor Windows. 
- Voor pools die zijn gemaakt met een cloudserviceconfiguratie schakelt u poort 10100, 20100 en 30100 in. 
- Uitgaande verbindingen tooAzure opslag op poort 443 inschakelen. Zorg er ook voor dat uw Azure Storage-eindpunt kan worden omgezet door alle aangepaste DNS-servers die u beschikbaar maakt voor uw VNet. In het bijzonder met URL Hallo `<account>.table.core.windows.net` moet worden omgezet.

    Hallo volgende tabel beschrijft Hallo binnenkomende poorten die u nodig hebt tooenable voor toepassingen die u hebt gemaakt met de configuratie van de virtuele machine Hallo:

    |    Doelpoort(en)    |    IP-adres van bron      |    Voegt Batch NSG's toe?    |    Vereist is voor VM toobe bruikbaar?    |    Actie van gebruiker   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Voor toepassingen die zijn gemaakt met de configuratie van de virtuele machine Hallo: 29876, 29877</li><li>Voor toepassingen die zijn gemaakt met Hallo cloud service-configuratie: 10100, 20100, 30100</li></ul>         |    Alleen IP-adressen van Batch-servicerollen |    Ja. Batch toevoegt nsg's op Hallo niveau van network interfaces (NIC) gekoppeld tooVMs. Deze NSG's staan alleen verkeer vanuit IP-adressen van Batch-servicerollen toe. Zelfs als u deze poorten voor de gehele web Hallo opent, wordt Hallo verkeer ophalen geblokkeerd op Hallo NIC. |    Ja  |  U hoeft niet toospecify een NSG omdat Batch kan alleen Batch IP-adressen. <br /><br /> Als u toch een NSG opgeeft, zorg dan dat deze poorten zijn geopend voor inkomend verkeer. <br /><br /> Als u opgeeft * als IP-adres van bron in uw NSG hello, Batch nog steeds nsg's toevoegen op Hallo niveau van tooVMs NIC die is gekoppeld. |
    |    3389, 22               |    Apparaten van gebruikers, die wordt gebruikt voor foutopsporing, zodat u op afstand toegang Hallo VM tot.    |    Nee                                    |    Nee                     |    Nsg's toevoegen als u wilt dat toopermit externe toegang (RDP/SSH) toohello VM.   |                 

    Hallo volgende tabel beschrijft Hallo uitgaande poort, moet u tooenable toopermit toegang tooAzure opslag:

    |    Uitgaande poort(en)    |    Doel    |    Voegt Batch NSG's toe?    |    Vereist is voor VM toobe bruikbaar?    |    Actie van gebruiker    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    Nee    |    Ja    |    Als u een nsg's toevoegt, zorg dat deze poort open toooutbound verkeer is.    |


## <a name="scaling-compute-resources"></a>Rekenresources vergroten/verkleinen
Met [automatische schaling](batch-automatic-scaling.md), kunt u Batch-service Hallo Hallo aantal rekenknooppunten in een pool op basis van toohello huidige workload en het Resourcegebruik gebruik van uw rekenscenario dynamisch wordt aangepast hebt. Hiermee kunt u toolower Hallo totale kosten van het uitvoeren van uw toepassing met behulp van alleen Hallo bronnen die u nodig en vrij te geven u niet nodig hebt.

U schakelt automatische vergroting/verkleining in door een [formule voor automatisch vergroten/verkleinen](batch-automatic-scaling.md#automatic-scaling-formulas) te schrijven en die formule te koppelen aan een pool. Hallo Batch-service gebruikt Hallo formule toodetermine hello doelaantal knooppunten in de groep Hallo voor Hallo volgende vergroten/verkleinen interval (een interval die u kunt configureren). U kunt Hallo automatisch vergroten/verkleinen instellingen voor een pool opgeven wanneer u deze maken of op een pool later inschakelen. U kunt ook bijwerken Hallo schalen op een pool schalen is ingeschakeld.

Als u bijvoorbeeld een bepaalde job moet dient u een zeer groot aantal taken toobe uitgevoerd. U kunt een vergroten/verkleinen formule toohello-groep die Hiermee past u het aantal knooppunten in Hallo pool op basis van Hallo Huidig aantal taken in de wachtrij en Hallo voltooiing frequentie van Hallo taken in Hallo job Hallo toewijzen. Hallo Batch-service periodiek evalueert Hallo formule en Hallo-groep, op basis van de werkbelasting en uw formule instellingen het formaat wordt aangepast. Hallo-service worden knooppunten toegevoegd, indien nodig wanneer er een groot aantal taken in de wachtrij en knooppunten verwijdert wanneer er geen taken in de wachtrij of wordt uitgevoerd zijn.

Een formule voor vergroten/verkleinen kan zijn gebaseerd op Hallo metrische gegevens te volgen:

* **Metrische gegevens voor tijd** zijn gebaseerd op statistieken verzameld om de vijf minuten in Hallo opgegeven aantal uren.
* **Metrische gegevens voor resources** zijn gebaseerd op CPU-gebruik, bandbreedtegebruik, geheugengebruik en het aantal knooppunten.
* **Metrische gegevens voor taken** zijn gebaseerd op de taakstatus, zoals *Actief* (in de wachtrij) *Wordt uitgevoerd* of *Voltooid*.

Wanneer automatisch vergroten / het aantal rekenknooppunten in een pool hello verkleinen, moet u overwegen hoe toohandle taken die worden uitgevoerd op moment van Hallo Hallo bewerking afnemen. tooaccommodate deze, Batch biedt een *knooppunt toewijzing is opgeheven optie* die u kunt opnemen in uw formules. U kunt bijvoorbeeld opgeven dat actieve taken worden onmiddellijk gestopt, onmiddellijk worden gestopt en vervolgens opnieuw voor uitvoering op een ander knooppunt of toofinish toegestaan voordat het Hallo-knooppunt wordt verwijderd uit groep Hallo.

Zie [Automatically scale compute nodes in an Azure Batch pool](batch-automatic-scaling.md) (Rekenknooppunten in een Azure Batch-pool automatisch vergroten/verkleinen) voor meer informatie over het automatisch vergroten/verkleinen van een toepassing.

> [!TIP]
> toomaximize compute Resourcegebruik, Hallo doelaantal knooppunten toozero ingesteld op Hallo einde van een taak, maar actieve taken toofinish toestaan.
>
>

## <a name="security-with-certificates"></a>Beveiliging met certificaten
U moet doorgaans toouse certificaten wanneer u versleutelen of ontsleutelen van gevoelige gegevens voor taken zoals het Hallo-sleutel voor een [Azure Storage-account][azure_storage]. toosupport, kunt u certificaten installeren op knooppunten. Versleutelde geheimen worden tootasks via opdrachtregelparameters doorgegeven of ingesloten in een van de Hallo taak resources en geïnstalleerd Hallo-certificaten kunnen worden gebruikt toodecrypt ze.

Gebruik van Hallo [certificaat toevoegen] [ rest_add_cert] bewerking (Batch REST) of [CertificateOperations.CreateCertificate] [ net_create_cert] methode (Batch .NET) tooadd een certificaat tooa Batch-account. U kunt vervolgens Hallo certificaat met een nieuwe of bestaande pool koppelen. Wanneer een certificaat gekoppeld aan een pool wordt, installeert Hallo Batch-service Hallo certificaat op elk knooppunt in de pool Hallo. Hallo Batch-service installeert de juiste certificaten Hallo wanneer Hallo-knooppunt wordt gestart, voordat er taken (inclusief Hallo begintaak en jobbeheertaak) wordt gestart.

Als u certificaten tooan toevoegt *bestaande* groep, moet u de rekenknooppunten opnieuw opstarten Hallo certificaten toobe toegepast toohello knooppunten.

## <a name="error-handling"></a>Foutafhandeling
Het wellicht noodzakelijk toohandle taak- en toepassingsfouten storingen in uw Batch-oplossing.

### <a name="task-failure-handling"></a>Afhandeling van taakfouten
Taakfouten kunnen worden onderverdeeld in deze categorieën:

* **Voorverwerkingsfouten**

    Als een taak toostart mislukt, is een fout vooraf verwerken voor Hallo taak ingesteld.  

    Voorverwerking van fouten kan optreden als de bronbestanden van de taak Hallo hebt verplaatst, Hallo Storage-account niet meer beschikbaar is of een ander probleem is opgetreden dat Hallo gekopieerd toohello knooppunt bestanden.

* **Fouten bij uploaden van bestand**

    Als het uploaden van bestanden die zijn opgegeven voor een taak voor een of andere reden mislukt, wordt een fout bij het uploaden is ingesteld voor Hallo-taak.

    Bestand uploaden fouten optreden kunnen als hello SAS opgegeven voor toegang tot Azure Storage is een ongeldige of biedt geen schrijfmachtigingen, als Hallo storage-account niet meer beschikbaar is, of als een ander probleem is opgetreden waardoor de Hallo geslaagde kopiëren van bestanden uit Hallo-knooppunt.    

* **Toepassingsfouten**

    Hallo-proces dat is opgegeven door de opdrachtregel van de taak Hallo kan ook mislukken. Hallo proces wordt geacht toohave is mislukt bij een andere waarde dan nul afsluitcode wordt geretourneerd door Hallo-proces dat wordt uitgevoerd door de taak hello (Zie *taak afsluitcodes* in de volgende sectie Hallo).

    Voor toepassingsfouten, kunt u Batch tooautomatically opnieuw Hallo taak tooa aantal keren opgegeven.

* **Beperkingsfouten**

    U kunt instellen dat een beperking die Hallo uitvoering van de maximale duur voor een job of taak hello aangeeft *maxWallClockTime*. Dit kan handig zijn voor taken die niet voldoen aan tooprogress wordt beëindigd.

    Wanneer de maximale tijdsduur Hallo is overschreden, Hallo-taak is gemarkeerd als *voltooid*, maar de afsluitcode hello te is ingesteld`0xC000013A` en Hallo *schedulingError* veld is gemarkeerd als `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Foutopsporing van toepassingsfouten
* `stderr` en `stdout`

    Tijdens het uitvoeren, kan een toepassing diagnostische uitvoer waarmee u tootroubleshoot problemen kunt opleveren. Zoals vermeld in Hallo eerder gedeelte [bestanden en mappen](#files-and-directories), Hallo Batch-service schrijft standaarduitvoer en de standaardfout uitvoer te`stdout.txt` en `stderr.txt` bestanden in de taakmap Hallo op Hallo rekenknooppunt. U kunt hello Azure-portal of een van de Hallo Batch-SDK's toodownload gebruiken deze bestanden. Bijvoorbeeld, kunt u deze en andere bestanden voor het oplossen van problemen met behulp van ophalen [ComputeNode.GetNodeFile] [ net_getfile_node] en [CloudTask.GetNodeFile] [ net_getfile_task] in Hallo Batch .NET-bibliotheek.

* **Taakafsluitcodes**

    Zoals eerder vermeld, wordt een taak wordt gemarkeerd als defect door Hallo Batch-service als het Hallo-proces dat wordt uitgevoerd door de taak Hallo retourneert een afsluitcode die niet nul. Wanneer een taak wordt uitgevoerd een proces, Batch van Hallo taak afsluiten code eigenschap met de Hallo gevuld *retourcode van Hallo proces*. Het is belangrijk toonote die de afsluitcode van een taak **niet** bepaald door Hallo Batch-service. De afsluitcode van een taak wordt bepaald door het Hallo-proces zelf of Hallo-besturingssysteem op welke Hallo-proces dat wordt uitgevoerd.

### <a name="accounting-for-task-failures-or-interruptions"></a>Verklaring voor mislukte taken of onderbrekingen van taken
Van tijd tot tijd kunnen taken mislukken of worden onderbroken. Hallo taaktoepassing zelf kan mislukken, Hallo knooppunt welke Hallo taak wordt uitgevoerd kan opnieuw worden opgestart of Hallo knooppunt kan worden verwijderd uit groep Hallo tijdens een bewerking formaat wijzigen als hello van groep opheffen van toewijzing van beleid set tooremove knooppunten onmiddellijk zonder te wachten taken toofinish. In alle gevallen kan Hallo taak worden automatisch opnieuw door de Batch voor uitvoering op een ander knooppunt.

Het is ook mogelijk dat een onregelmatig probleem toocause een taak toohang of tooexecute te lang duren. U kunt Hallo maximale uitvoering interval voor een taak instellen. Als hello maximale uitvoering-interval wordt overschreden, Hallo Batch-service-interrupts Hallo taaktoepassing.

### <a name="connecting-toocompute-nodes"></a>Verbinding maken met toocompute knooppunten
U kunt aanvullende opsporen en oplossen door het rekenknooppunt tooa extern aanmelden uitvoeren. U kunt hello Azure portal toodownload een Remote Desktop Protocol (RDP)-bestand gebruiken voor Windows-knooppunten en de verbindingsgegevens Secure Shell (SSH) voor Linux-knooppunten te verkrijgen. U kunt dit ook doen met behulp van Batch-API's--Hallo bijvoorbeeld met [Batch .NET] [ net_rdpfile] of [Batch Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> tooconnect tooa knooppunt via RDP of SSH, moet u eerst een gebruiker maken op Hallo-knooppunt. toodo, kunt u hello Azure-portal [toevoegen van een gebruiker account tooa knooppunt] [ rest_create_user] via Hallo Batch REST-API aanroepen Hallo [ComputeNode.CreateComputeNodeUser] [ net_create_user] methode in Batch .NET of aanroep Hallo [add_user] [ py_add_user] methode in Hallo Batch Python-module.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Problemen met problematische rekenknooppunten oplossen
In situaties waar aantal taken mislukken, onderzoeken uw Batch-clienttoepassing of service Hallo metagegevens van Hallo mislukt taken tooidentify een zich niet normaal gedraagt knooppunt. Elk knooppunt in een pool krijgt een unieke ID en Hallo knooppunt waarop een taak wordt uitgevoerd in de metagegevens van de taak Hallo is opgenomen. Als u eenmaal een probleemknooppunt hebt geïdentificeerd, kunt u verschillende acties uitvoeren:

* **Hallo knooppunt opnieuw opstarten** ([REST][rest_reboot] | [.NET][net_reboot])

    Opnieuw te starten Hallo knooppunt kunt soms latente problemen zoals vastgelopen of gecrashte processen wissen. Houd er rekening mee dat als uw pool een begintaak gebruikt of uw job een jobvoorbereidingstaak gebruikt, worden deze uitgevoerd wanneer Hallo knooppunt opnieuw wordt opgestart.
* **Hallo knooppunt installatiekopie** ([REST][rest_reimage] | [.NET][net_reimage])

    Dit wordt opnieuw geïnstalleerd besturingssysteem Hallo op Hallo-knooppunt. Net als bij het opstarten van een knooppunt, Begintaken en jobvoorbereidingstaken opnieuw worden uitgevoerd nadat Hallo-knooppunt is teruggezet.
* **Hallo knooppunt verwijderen uit groep Hallo** ([REST][rest_remove] | [.NET][net_remove])

    Soms is het nodig toocompletely verwijderen Hallo van het knooppunt uit Hallo-groep.
* **Taakplanning op Hallo knooppunt uitschakelen** ([REST][rest_offline] | [.NET][net_offline])

    Dit vindt effectief Hallo-knooppunt offline zodat er geen taken meer tooit zijn toegewezen, maar kunt Hallo knooppunt tooremain uitgevoerd en in Hallo van toepassingen. Hiermee kunt u verder onderzoek tooperform in Hallo oorzaak van Hallo fouten zonder verlies van gegevens Hallo mislukte taak en zonder Hallo knooppunt extra taakfouten veroorzaakt. Bijvoorbeeld, u kunt taakplanning uitschakelen op Hallo-knooppunt vervolgens [extern aanmelden](#connecting-to-compute-nodes) tooexamine Hallo de gebeurtenislogboeken van het knooppunt of andere probleemoplossing uitvoeren. Nadat u uw onderzoek hebt, kunt u vervolgens Hallo knooppunt weer online brengen doordat taakplanning ([REST][rest_online] | [.NET] [ net_online]), of voer een van de Hallo andere acties die eerder is besproken.

> [!IMPORTANT]
> Met elke actie die wordt beschreven in deze sectie--opnieuw opstarten, terugzetten van de installatiekopie, verwijderen en schakel taakplanning--u kunt toospecify hoe taken die momenteel worden uitgevoerd op Hallo knooppunt worden verwerkt wanneer u Hallo actie uitvoeren. Bijvoorbeeld, wanneer u taakplanning uitschakelen op een knooppunt met behulp van Hallo Batch .NET-clientbibliotheek kunt u een [DisableComputeNodeSchedulingOption] [ net_offline_option] enum-waarde toospecify of te**Beëindigen** taken uitvoeren, **Requeue** ze voor het plannen van op andere knooppunten of actieve taken toocomplete toe voordat u Hallo actie uitvoert (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Volgende stappen
* Meer informatie over Hallo [Batch-API's en hulpprogramma's](batch-apis-tools.md) beschikbaar voor het bouwen van Batch-oplossingen.
* Een Batch voorbeeldtoepassing stapsgewijze in doorlopen [aan de slag met hello Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md). Er is ook een [Python-versie](batch-python-tutorial.md) van Hallo-zelfstudie die wordt uitgevoerd een werklast op Linux-rekenknooppunten.
* Download en bouw Hallo [Batch Explorer] [ github_batchexplorer] voorbeeldproject voor gebruik bij het ontwikkelen van uw Batch-oplossingen. Hallo Batch Explorer gebruikt, kunt u de volgende Hallo en nog veel meer uitvoeren:

  * Pools, jobs en taken in uw Batch-account controleren en bewerken
  * `stdout.txt`, `stderr.txt` en andere bestanden van knooppunten downloaden
  * Gebruikers maken op knooppunten en RDP-bestanden downloaden voor externe aanmelding
* Meer informatie over hoe te[maken van groepen van Linux-rekenknooppunten](batch-linux-nodes.md).
* Ga naar Hallo [Azure Batch-forum] [ batch_forum] op MSDN. Hallo-forum is een goede plaats tooask vragen, ongeacht of u alleen leren of een expert in met behulp van Batch zijn.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

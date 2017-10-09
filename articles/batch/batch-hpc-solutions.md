---
title: aaaBatch en HPC-oplossingen in Hallo cloud - Azure | Microsoft Docs
description: Meer informatie over batchverwerkings- en High Performance Computing-scenario's (HPC en Big Compute) en oplossingsopties in Azure
services: batch, virtual-machines, cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: aab5401d-2baf-4cf2-bf20-ad224de33888
ms.service: batch
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c5a3c8859d1f95040bcdad15942a815d71eb4486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="batch-and-hpc-solutions-for-large-scale-computing-workloads"></a>Batch- en HPC-oplossingen voor grootschalige rekenworkloads

Azure biedt efficiënte, schaalbare cloudoplossingen voor batchverwerking en High Performance Computing (HPC), ook wel *Big Compute* genoemd. Hier vindt u informatie over Big Compute-workloads en Azure services toosupport ze, of rechtstreeks te gaan[Oplossingsscenario's](#scenarios) verderop in dit artikel. In dit artikel is hoofdzakelijk bestemd voor technische besluitvormers, IT-managers en onafhankelijke softwareleveranciers, maar andere IT-professionals en ontwikkelaars kunnen gebruiken it toofamiliarize zelf met deze oplossingen.

Organisaties kampen met grootschalige rekenproblemen: technische ontwerpen en analyses, opbouwen van afbeeldingen, complexe modellering, Monte Carlo-simulaties, berekeningen van financiële risico's enz. Azure helpt organisaties deze problemen oplossen met het Hallo-resources, schaal en planning die ze nodig hebben. Met Azure kunnen organisaties:

* Hybride oplossingen maken, een lokale HPC cluster toooffload piek werkbelastingen toohello cloud uitbreiden
* HPC-clusterhulpprogramma's en workloads volledig in Azure uitvoeren
* Gebruik van beheerde en schaalbare Azure-services, zoals [Batch](https://azure.microsoft.com/documentation/services/batch/) toorun rekenintensieve workloads zonder toodeploy compute-infrastructuur en beheren

Hoewel dit buiten Hallo bereik van dit artikel, biedt Azure ook ontwikkelaars en partners een volledige set mogelijkheden, architectuurkeuzen en development tools toobuild grootschalige, aangepaste Big Compute-werkstromen. En een groeiend ecosysteem voor partners klaar toohelp u uw Big Compute-workloads productief in hello Azure-cloud is.

## <a name="batch-and-hpc-applications"></a>Batch- en HPC-toepassingen
In tegenstelling tot webtoepassingen en veel Line-Of-Business-toepassingen, hebben batch- en HPC-toepassingen een gedefinieerd begin en einde en kunnen ze volgens een planning of op aanvraag worden uitgevoerd, urenlang of zelfs nog langer. Vallen de meeste in twee hoofdcategorieën: *intrinsiek parallel* (ook wel 'perfect parallel', omdat ze oplossen van problemen met het Hallo zich goed toorunning parallel op meerdere computers of processoren lenen) en *nauw gekoppeld*. Zie de volgende tabel voor meer informatie over deze toepassingstypen Hallo. Sommige Azure benaderingen voor oplossingen werken beter voor een type of andere Hallo.

> [!NOTE]
> In Batch- en HPC-oplossingen wordt een actief exemplaar van een toepassing doorgaans een *job* genoemd en kan elke job onderverdeeld worden in *taken*. En hello geclusterde rekenresources voor de toepassing hello worden vaak genoemd *rekenknooppunten*.
> 
> 

| Type | Kenmerken | Voorbeelden |
| --- | --- | --- |
| **Intrinsically parallel**<br/><br/>![Intrinsically parallel][parallel] |• Afzonderlijke computers voeren toepassingslogica onafhankelijk uit<br/><br/> • Toe te voegen computers kunt Hallo toepassing tooscale en daling rekentijd worden ingekort<br/><br/>• Toepassing bestaat uit afzonderlijke uitvoerbare bestanden of is onderverdeeld in een groep services die worden aangeroepen door een client (een Service Oriented Architecture (SOA), toepassing) |• Modellering van financiële risico’s<br/><br/>• Rendering van afbeeldingen en beeldverwerking<br/><br/>• Mediacodering en -transcodering<br/><br/>• Monte Carlo-simulaties<br/><br/>• Softwaretests |
| **Nauw gekoppeld**<br/><br/>![Nauw gekoppeld][coupled] |• Toepassing vereist compute knooppunten toointeract of exchange tussenliggende resultaten<br/><br/>• Compute knooppunten kunnen communiceren met Hallo Message Passing Interface (MPI), een gemeenschappelijk communicatieprotocol voor parallelle berekeningen<br/><br/>• Hallo toepassing is gevoelig toonetwork latentie en bandbreedte<br/><br/>• Toepassingsprestaties kunnen worden verbeterd door gebruik te maken van snelle netwerktechnologieën zoals InfiniBand en Remote Direct Memory Access (RDMA) |• Modellering van olie- en gasreservoirs<br/><br/>• Technische ontwerpen en analyses, zoals Computational Fluid Dynamics<br/><br/>• Fysieke simulaties zoals auto-ongevallen en nucleaire reacties<br/><br/>• Weersvoorspelling |

### <a name="considerations-for-running-batch-and-hpc-applications-in-hello-cloud"></a>Overwegingen voor het uitvoeren van batch- en HPC-toepassingen in de cloud Hallo
Veel toepassingen die ontworpen toorun in lokale HPC-clusters tooAzure of tooa hybride (cross-premises) omgeving zijn kunt u gemakkelijk migreren. Er kunnen wel enkele beperkingen of overwegingen zijn, zoals:

* **Beschikbaarheid van cloudresources** -afhankelijk van Hallo type cloudrekenresources dat u gebruikt, u mogelijk niet kunnen toorely op continue beschikbaarheid van computers terwijl een taak wordt uitgevoerd. Statusafhandeling en controleer wijzen zijn algemene technieken toohandle mogelijke tijdelijke fouten en meer nodig bij gebruik van cloud-bronnen.
* **Toegang tot gegevens** -voor technieken voor gegevenstoegang algemeen beschikbaar is in clusters van de onderneming, zoals NFS, speciale configuratie in de cloud Hallo mogelijk vereist. Of moet u mogelijk verschillende gegevens tooadopt praktijken en patronen voor Hallo cloud.
* **Gegevensverplaatsing** - voor toepassingen dat proces grote hoeveelheden gegevens, strategieën nodig toomove Hallo gegevens in de cloud-opslag- en toocompute bronnen zijn. Mogelijk hebt u ook snelle cross-premises netwerkmogelijkheden nodig, zoals die van [Azure ExpressRoute](https://azure.microsoft.com/services/expressroute/). Houd ook rekening met juridische, regelgevende of beleidsbeperkingen voor de opslag van en toegang tot die gegevens.
* **Licentieverlening** : Neem contact op met de leverancier Hallo van een commerciële toepassing voor licentieverlening of andere beperkingen voor het uitvoeren in de cloud Hallo. Niet alle leveranciers bieden licenties waarbij u betaalt naar gebruik. U mogelijk tooplan moet een licentieserver in de cloud Hallo voor uw oplossing of tooan lokale licentieserver verbinding.

### <a name="big-compute-or-big-data"></a>Big Compute of Big Data?
Hallo scheidingslijn tussen Big Compute- en Big Data-toepassingen is niet altijd duidelijk en sommige toepassingen mogelijk kenmerken van beide. Beide toepassingen maken gebruik van grootschalige berekeningen, die doorgaans op clusters of computers worden uitgevoerd. Maar Hallo oplossing benaderingen en ondersteunende hulpprogramma's kunnen verschillen.

• **Big Compute** doorgaans tooinvolve toepassingen die afhankelijk zijn van CPU-kracht en geheugen, zoals technische simulaties, modellering, van financiële risico en digitale rendering. Hallo-infrastructuur voor een Big Compute-oplossing mogelijk computers met gespecialiseerde multicore-processoren tooperform grote berekeningen en gespecialiseerde, snelle hardware tooconnect Hallo netwerkcomputers bevatten.

• **Big data**-toepassingen lossen problemen met gegevensanalyse op waarbij grote hoeveelheden gegevens betrokken zijn die niet door één computer of databasebeheersysteem kunnen worden beheerd. Dit zijn bijvoorbeeld grote volumes van weblogboeken of andere business intelligence-gegevens. BIG Data doorgaans toorely meer op schijfcapaciteit en i/o-prestaties dan op CPU-kracht. Er zijn ook speciale Big Data-hulpprogramma's zoals Apache Hadoop toomanage Hallo cluster en partitie Hallo-gegevens. (Zie [Hadoop](https://azure.microsoft.com/solutions/hadoop/) voor meer informatie over Azure HDInsight en andere Azure Hadoop-oplossingen.)

## <a name="compute-management-and-job-scheduling"></a>Berekeningsbeheer en jobplanning
Uitvoeren van Batch en HPC-toepassingen vaak bevat een *Clusterbeheer* en een *Taakplanner* toohelp geclusterde rekenresources te beheren en de groep toewijzen toohello toepassingen die Hallo taken worden uitgevoerd. Deze functies kunnen worden uitgevoerd door verschillende hulpprogramma's of door een geïntegreerd hulpprogramma of geïntegreerde service.

* **Clusterbeheer** - Staat in voor het inrichten, vrijgeven en beheren van rekenresources (of rekenknooppunten). Clusterbeheer kan de installatie van installatiekopieën van besturingssysteem automatiseren en toepassingen in rekenknooppunten, op basis van toodemands rekenresources geschaald uitbreiden en prestaties Hallo Hallo knooppunten controleren.
* **Taakplanner** -Hiermee geeft u op Hallo resources (zoals processoren of geheugen) een toepassing moet en hello condities wanneer deze wordt uitgevoerd. Een jobplanner houdt een wachtrij van taken en wijst bronnen toothem op basis van een toegewezen prioriteit of andere kenmerken.

Clustering en jobplanning hulpprogramma's voor Windows- en Linux-clusters kunnen worden gemigreerd en tooAzure. Zo biedt bijvoorbeeld [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029), de gratis rekenclusteroplossing van Microsoft voor HPC-workloads in Windows en Linux, verschillende opties voor het uitvoeren in Azure. U kunt Linux-clusters ook toorun open-source hulpprogramma's zoals Torque en SLURM maken. U kunt ook commerciële raster oplossingen tooAzure, zoals zetten [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/), [IBM Spectrum Symphony en Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/), en [Univa raster Engine](http://www.univa.com/products/grid-engine).

Zoals u in Hallo uit te voeren, kunt u ook te profiteren van Azure-services toomanage rekenresources en plannen van taken zonder (of als aanvulling op) traditionele hulpprogramma's.

## <a name="scenarios"></a>Scenario's
Hier volgen drie gangbare scenario's toorun Big Compute-workloads in Azure met behulp van bestaande HPC-clusteroplossingen, Azure-services of een combinatie van Hallo twee. Voor de keuze van elk scenario zijn belangrijke, maar mogelijk niet alle aandachtspunten vermeld. Meer vindt over Hallo beschikbare Azure-services die kunt u in uw oplossing u verderop in Hallo artikel.

| Scenario | Waarom voor dit scenario kiezen? |
| --- | --- | --- |
| **Een HPC-cluster tooAzure burst**<br/><br/>[![Clusteruitbreiding][burst_cluster]](./media/batch-hpc-solutions/burst_cluster.png) <br/><br/> Meer informatie:<br/>• [Burst tooAzure werkrolinstanties HPC Pack](https://technet.microsoft.com/library/gg481749.aspx)<br/><br/>• [Set up a hybrid compute cluster with HPC Pack](../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) (Een hybride rekencluster met HPC Pack instellen)<br/><br/>• [Burst tooAzure Batch met HPC Pack](https://technet.microsoft.com/library/mt612877.aspx)<br/><br/> |• Combineer uw [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) of een ander on-premises cluster met extra Azure-resources in een hybride oplossing.<br/><br/>• Breid uw Big Compute-workloads toorun op Platform als een Service (PaaS) VM-instanties (momenteel alleen Windows Server).<br/><br/>• Krijg toegang tot een on-premises licentieserver of gegevensopslag met behulp van een optioneel virtueel Azure-netwerk |
| **Een HPC-cluster volledig in Azure maken**<br/><br/>[![Cluster in IaaS][iaas_cluster]](./media/batch-hpc-solutions/iaas_cluster.png)<br/><br/>Meer informatie:<br/>• [HPC cluster solutions in Azure](big-compute-resources.md) (HPC-clusteroplossingen in Azure)<br/><br/> |• Implementeer uw toepassingen en clusterhulpprogramma's snel en consistent op standaard of aangepaste Infrastructure as a service (IaaS) virtuele machines met Windows of Linux.<br/><br/>• Voer diverse Big Compute-workloads met behulp van de oplossing van uw keuze voor jobplanning Hallo.<br/><br/>• Gebruik extra Azure-services met inbegrip van netwerken en opslag toocreate volledige cloudoplossingen. |
| **Een parallelle toepassing tooAzure uitbreiden**<br/><br/>[![Azure Batch][batch_proc]](./media/batch-hpc-solutions/batch_proc.png)<br/><br/>Meer informatie:<br/>• [Basics of Azure Batch](batch-technical-overview.md) (Basisbeginselen van Azure Batch)<br/><br/>• [Aan de slag met hello Azure Batch-bibliotheek voor .NET](batch-dotnet-get-started.md) |• Ontwikkel met [Azure Batch](https://azure.microsoft.com/documentation/services/batch/) tooscale uit diverse Big Compute werkbelastingen-toorun op groepen van Windows of Linux virtuele machines.<br/><br/>• Gebruik een Azure-platform service toomanage-implementatie en automatisch schalen van virtuele machines, jobplanning, herstel na noodgevallen, gegevensverplaatsing, Afhankelijkheidsbeheer en toepassingsimplementatie. |

## <a name="azure-services-for-big-compute"></a>Azure-services voor Big Compute
Is hier meer over Hallo compute, gegevens, netwerkvoorzieningen en verwante services die kunt u combineren voor Big Compute-oplossingen en werkstromen. Voor Zie voor meer informatie over Azure-services Azure-services Hallo [documentatie](https://azure.microsoft.com/documentation/). Hallo [scenario's](#scenarios) eerder in dit artikel tonen slechts enkele manieren om deze services te gebruiken.

> [!NOTE]
> Azure introduceert regelmatig nieuwe services die voor uw scenario nuttig kunnen zijn. Als u vragen hebt, neemt u contact op met een [Azure-partner](https://pinpoint.microsoft.com/en-US/search?keyword=azure) of stuurt u een e-mail naar *bigcompute@microsoft.com*.
> 
> 

### <a name="compute-services"></a>Compute services
Azure compute-services worden Hallo kern van een Big Compute-oplossing en Hallo andere compute services bieden voordelen voor verschillende scenario's. Op een basisniveau bieden deze services verschillende modi voor toepassingen toorun op op basis van een virtuele machine compute-exemplaren die Azure verstrekt met behulp van Windows Server Hyper-V-technologie. Op deze instanties kunnen standaard en aangepaste Linux- en Windows-besturingssystemen en hulpprogramma's worden uitgevoerd. Azure biedt u een keuze uit [instantiegrootten](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) met verschillende configuraties van CPU-kernen, geheugen, schijfcapaciteit en andere kenmerken. U kunt schalen Hallo exemplaren toothousands van kernen en daarna geschaald verkleinen wanneer u minder bronnen nodig afhankelijk van uw behoeften.

> [!NOTE]
> Profiteren van hello Azure [rekenintensieve exemplaren zoals Hallo H-serie](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooimprove Hallo prestaties en schaalbaarheid van HPC-workloads. Deze instanties ondersteunen ook parallelle MPI-toepassingen die een toepassingsnetwerk met een lage latentie en hoge doorvoer vereisen. Ook beschikbaar zijn [N-serie](../virtual-machines/windows/sizes-gpu.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) virtuele machines met NVIDIA GPU's tooexpand Hallo scala aan scenario's voor computer- en visualisatie in Azure.  
> 
> 

| Service | Beschrijving |
| --- | --- |
| **[Virtuele machines](https://azure.microsoft.com/documentation/services/virtual-machines/)**<br/><br/> |• Bieden Infrastructure as a Service (IaaS) voor berekeningen met behulp van Microsoft Hyper-V-technologie<br/><br/>• Kunt u tooflexibly inrichten en beheren van permanente cloudcomputers van standaard Windows Server- of Linux-installatiekopieën van Hallo [Azure Marketplace](https://azure.microsoft.com/marketplace/), of installatiekopieën en gegevensschijven die u opgeeft<br/><br/>• Kan worden geïmplementeerd en beheerd als [VM-Schaalsets](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/) toobuild grootschalige services vanaf identieke virtuele machines met automatisch schalen tooincrease of afname capaciteit automatisch<br/><br/>• On-premises uitgevoerd rekenclusterhulpprogramma's en toepassingen volledig uit in de cloud Hallo<br/><br/> |
| **[Cloudservices](https://azure.microsoft.com/documentation/services/cloud-services/)**<br/><br/> |• Kunnen Big Compute-toepassingen uitvoeren in werkrolinstanties (virtuele machines met een versie van Windows Server en die volledig door Azure worden beheerd)<br/><br/>• Maken schaalbare, betrouwbare toepassingen mogelijk met lage administratieve overhead, die worden uitgevoerd in een Platform as a service (PaaS)-model<br/><br/>• Vereisen mogelijk extra hulpprogramma's of ontwikkeling toointegrate met oplossingen voor on-premises HPC-cluster |
| **[Batch](https://azure.microsoft.com/documentation/services/batch/)**<br/><br/> |• Voert grootschalige parallelle workloads en batchworkloads uit in een volledig beheerde service<br/><br/>• Biedt jobplanning en automatisch schalen van een beheerde pool van virtuele machines<br/><br/>• Kunnen ontwikkelaars toepassingen toobuild en het uitvoeren als een service of cloud inschakelen voor bestaande toepassingen<br/> |

### <a name="storage-services"></a>Opslagservices
Een Big Compute-oplossing werkt doorgaans met een reeks invoergegevens en genereert gegevens voor de resultaten. Enkele van hello Azure storage-services die in Big Compute-oplossingen worden gebruikt:

* [Blob Storage, Table Storage en Queue Storage](https://azure.microsoft.com/documentation/services/storage/) - Beheer respectievelijk grote hoeveelheden ongestructureerde gegevens, NoSQL-gegevens en berichten voor werkstromen en communicatie. Bijvoorbeeld, u kunt blob storage gebruiken voor grote sets met technische gegevens, of voor Hallo invoer installatiekopieën of media die uw toepassing verwerkt. U kunt wachtrijen gebruiken voor asynchrone communicatie in een oplossing. Zie [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md).
* [Azure File storage](https://azure.microsoft.com/services/storage/files/) -Shares algemene bestanden en gegevens in Azure worden verkregen met Hallo standaard SMB-protocol, hetgeen nodig is voor sommige HPC-clusteroplossingen.
* [Data Lake Store](https://azure.microsoft.com/services/data-lake-store/) -biedt een grootschalig Apache Hadoop Distributed File System voor cloud hello, nuttig zijn voor batch, realtime en interactieve analyses.

### <a name="data-and-analysis-services"></a>Gegevens- en analyseservices
Bij sommige Big Compute-scenario's zijn grootschalige gegevensstromen betrokken of worden gegevens gegenereerd die verder moeten worden verwerkt of geanalyseerd. Azure biedt verschillende gegevens- en analyseservices, waaronder:

* [Data Factory](https://azure.microsoft.com/documentation/services/data-factory/) - Bouwt gegevensgestuurde werkstromen (pijplijnen) die gegevens uit on-premises gegevensopslag en cloud- en internetgegevensopslag samenvoegen, aggregeren en transformeren.
* [SQL-Database](https://azure.microsoft.com/documentation/services/sql-database/) -Hallo belangrijke functies van een relationeel Microsoft SQL Server-databasebeheersysteem in een beheerde service biedt.
* [HDInsight](https://azure.microsoft.com/documentation/services/hdinsight/) - implementeert en richt Windows Server of Linux-gebaseerde Apache Hadoop-clusters in Hallo toomanage cloud, analyseren en rapporteren van big data.
* [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/) - Helpt u bij het maken, testen, gebruiken en beheren van voorspellende analytische oplossingen in een volledig beheerde service.

### <a name="additional-services"></a>Extra services
Uw Big Compute-oplossing moet mogelijk andere Azure-services tooconnect tooresources lokale of in andere omgevingen. Voorbeelden zijn:

* [Virtueel netwerk](https://azure.microsoft.com/documentation/services/virtual-network/) -wordt gemaakt van een logisch geïsoleerde sectie in Azure tooconnect Azure-resources tooeach andere of tooyour on-premises Datacenter. Met een virtueel cross-premises netwerk hebben Big Compute-toepassingen toegang tot on-premises gegevens, Active Directory-services en licentieservers
* [ExpressRoute](https://azure.microsoft.com/documentation/services/expressroute/): hiermee maakt u een privéverbinding tussen Microsoft-datacenters en -infrastructuren on-premises of in een co-locatieomgeving. ExpressRoute biedt betere beveiliging, meer betrouwbaarheid, hogere snelheden en lagere latenties dan gewone verbindingen via Internet Hallo.
* [Service Bus](https://azure.microsoft.com/documentation/services/service-bus/) -biedt verschillende mechanismen voor toepassingen of ze in Azure, op een ander cloudplatform of in een datacenter bevinden zich toocommunicate of exchange-gegevens.

## <a name="next-steps"></a>Volgende stappen
* Zie [technische bronnen voor Batch- en HPC](big-compute-resources.md) toofind technische richtlijnen toobuild uw oplossing.
* Bespreek uw Azure-opties met partners, zoals Cycle Computing, Rescale en UberCloud.
* Lees meer over Big Compute-oplossingen voor Azure die worden geleverd door [Towers Watson](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222), [Altair](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/), [ANSYS](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/) en [d3VIEW](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088).
* Zie voor de meest recente aankondigingen Hallo Hallo [teamblog van Microsoft HPC en Batch](http://blogs.technet.com/b/windowshpc/) en Hallo [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).

<!--Image references-->
[parallel]: ./media/batch-hpc-solutions/parallel.png
[coupled]: ./media/batch-hpc-solutions/coupled.png
[iaas_cluster]: ./media/batch-hpc-solutions/iaas_cluster.png
[burst_cluster]: ./media/batch-hpc-solutions/burst_cluster.png
[batch_proc]: ./media/batch-hpc-solutions/batch_proc.png

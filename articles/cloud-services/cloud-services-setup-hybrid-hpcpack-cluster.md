---
title: aaaSet van een hybride HPC Pack-cluster in Azure | Microsoft Docs
description: Meer informatie over hoe Microsoft HPC Pack toouse en Azure tooset-up maken van een klein, hybride hoge prestaties computing (HPC)-cluster
services: cloud-services
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: hpc-pack
ms.assetid: 
ms.service: cloud-services
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: danlep
ms.openlocfilehash: 5ad30d78dcd0c6a95d2a61f25015232edab3563c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="7ad40-103">Een hybride high performance computing-cluster (HPC) met Microsoft HPC Pack en Azure rekenknooppunten op aanvraag instellen</span><span class="sxs-lookup"><span data-stu-id="7ad40-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="7ad40-104">Gebruik Microsoft HPC Pack 2012 R2 en Azure tooset van een klein, hybride high performance computing-cluster (HPC).</span><span class="sxs-lookup"><span data-stu-id="7ad40-104">Use Microsoft HPC Pack 2012 R2 and Azure tooset up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="7ad40-105">Hallo-cluster wordt weergegeven in dit artikel bestaat uit een lokale HPC Pack-hoofdknooppunt en enkele berekeningen knooppunten die u implementeert op aanvraag in een Azure-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7ad40-105">hello cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="7ad40-106">Vervolgens kunt u de compute-taken uitvoeren op Hallo hybride cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad40-106">You can then run compute jobs on hello hybrid cluster.</span></span>

![Hybride HPC-cluster][Overview] 

<span data-ttu-id="7ad40-108">Deze zelfstudie ziet u een benadering soms cluster 'burst toohello cloud,' toouse schaalbare, on-demand Azure-resources toorun compute-intensieve toepassingen genoemd.</span><span class="sxs-lookup"><span data-stu-id="7ad40-108">This tutorial shows one approach, sometimes called cluster "burst toohello cloud," toouse scalable, on-demand Azure resources toorun compute-intensive applications.</span></span>

<span data-ttu-id="7ad40-109">Deze zelfstudie wordt ervan uitgegaan dat geen ervaring met rekenclusters of HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="7ad40-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="7ad40-110">Het is beoogde alleen toohelp implementeren van een hybride rekencluster snel voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="7ad40-110">It is intended only toohelp you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="7ad40-111">Voor overwegingen en stappen toodeploy een hybride HPC Pack cluster op groter schaal in een productieomgeving of toouse HPC Pack 2016, Zie Hallo [gedetailleerde richtlijnen](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="7ad40-111">For considerations and steps toodeploy a hybrid HPC Pack cluster at greater scale in a production environment, or toouse HPC Pack 2016, see hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="7ad40-112">Voor andere scenario's met HPC Pack, met inbegrip van geautomatiseerde implementatie van het cluster in Azure virtuele machines, Zie [opties voor HPC-cluster met Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ad40-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7ad40-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7ad40-113">Prerequisites</span></span>
* <span data-ttu-id="7ad40-114">**Azure-abonnement** -als u geen Azure-abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="7ad40-115">**Een on-premises-computer met Windows Server 2012 R2 of Windows Server 2012** -deze computer gebruiken als het hoofdknooppunt Hallo van Hallo HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad40-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as hello head node of hello HPC cluster.</span></span> <span data-ttu-id="7ad40-116">Als u al Windows Server worden niet uitgevoerd, kunt u downloaden en installeren van een [evaluatieversie](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="7ad40-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="7ad40-117">Hallo-computer moet lid tooan Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="7ad40-117">hello computer must be joined tooan Active Directory domain.</span></span> <span data-ttu-id="7ad40-118">Voor testdoeleinden kunt u Hallo hoofdknooppunt computer configureren als een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="7ad40-118">For test purposes, you can configure hello head node computer as a domain controller.</span></span> <span data-ttu-id="7ad40-119">tooadd Hallo Active Directory Domain Services-serverfunctie en Hallo hoofdknooppunt computer als een domeincontroller te bevorderen, Zie Hallo-documentatie voor Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7ad40-119">tooadd hello Active Directory Domain Services server role and promote hello head node computer as a domain controller, see hello documentation for Windows Server.</span></span>
  * <span data-ttu-id="7ad40-120">toosupport HPC Pack Hallo-besturingssysteem moet worden geïnstalleerd in een van de volgende talen: Engels, Japans of Chinees (Vereenvoudigd).</span><span class="sxs-lookup"><span data-stu-id="7ad40-120">toosupport HPC Pack, hello operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="7ad40-121">Controleer of belangrijke en kritieke updates zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7ad40-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="7ad40-122">**HPC Pack 2012 R2** - [downloaden](http://go.microsoft.com/fwlink/p/?linkid=328024) Hallo-installatiepakket voor de meest recente versie Hallo gratis kosten en kopieer Hallo bestanden toohello hoofdknooppunt computer.</span><span class="sxs-lookup"><span data-stu-id="7ad40-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) hello installation package for hello latest version free of charge and copy hello files toohello head node computer.</span></span> <span data-ttu-id="7ad40-123">Kies installatiebestanden in Hallo dezelfde taal als de installatie van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7ad40-123">Choose installation files in hello same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="7ad40-124">Als u toouse HPC Pack 2016 in plaats van HPC Pack 2012 R2 wilt, is aanvullende configuratie nodig.</span><span class="sxs-lookup"><span data-stu-id="7ad40-124">If you want toouse HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="7ad40-125">Zie Hallo [gedetailleerde richtlijnen](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="7ad40-125">See hello [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="7ad40-126">**Domeinaccount** -dit account moet worden geconfigureerd met lokale beheermachtigingen op Hallo hoofdknooppunt tooinstall HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="7ad40-126">**Domain account** - This account must be configured with local Administrator permissions on hello head node tooinstall HPC Pack.</span></span>
* <span data-ttu-id="7ad40-127">**TCP-verbinding op poort 443** van Hallo hoofdknooppunt tooAzure.</span><span class="sxs-lookup"><span data-stu-id="7ad40-127">**TCP connectivity on port 443** from hello head node tooAzure.</span></span>

## <a name="install-hpc-pack-on-hello-head-node"></a><span data-ttu-id="7ad40-128">HPC Pack installeren op het hoofdknooppunt Hallo</span><span class="sxs-lookup"><span data-stu-id="7ad40-128">Install HPC Pack on hello head node</span></span>
<span data-ttu-id="7ad40-129">U eerst installeren Microsoft HPC Pack op uw lokale computer met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="7ad40-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="7ad40-130">Deze computer wordt Hallo hoofdknooppunt van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad40-130">This computer becomes hello head node of hello cluster.</span></span>

1. <span data-ttu-id="7ad40-131">Hoofdknooppunt toohello aanmelden met een domeinaccount met lokale beheerdersmachtigingen heeft.</span><span class="sxs-lookup"><span data-stu-id="7ad40-131">Log on toohello head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="7ad40-132">Start Hallo HPC Pack installatiewizard door het uitvoeren van Setup.exe uit Hallo HPC Pack-installatiebestanden.</span><span class="sxs-lookup"><span data-stu-id="7ad40-132">Start hello HPC Pack Installation Wizard by running Setup.exe from hello HPC Pack installation files.</span></span>

3. <span data-ttu-id="7ad40-133">Op Hallo **HPC Pack 2012 R2 installeren** scherm, klikt u op **nieuwe installatie of het toevoegen van nieuwe functies tooan bestaande installatie**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-133">On hello **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features tooan existing installation**.</span></span>

    ![HPC Pack 2012 Setup][install_hpc1]

4. <span data-ttu-id="7ad40-135">Op Hallo **Microsoft Software gebruikersovereenkomst pagina**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-135">On hello **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="7ad40-136">Op Hallo **Type installatie selecteren** pagina, klikt u op **een nieuw HPC-cluster maken door het maken van een hoofdknooppunt**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-136">On hello **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="7ad40-137">Hallo wizard voert verschillende voorafgaand aan installatie tests uit.</span><span class="sxs-lookup"><span data-stu-id="7ad40-137">hello wizard runs several pre-installation tests.</span></span> <span data-ttu-id="7ad40-138">Klik op **volgende** op Hallo **installatieregels** pagina als u alle tests zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="7ad40-138">Click **Next** on hello **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="7ad40-139">Anders Hallo informatie bekijken en breng eventueel benodigde wijzigingen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="7ad40-139">Otherwise, review hello information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="7ad40-140">Voer Hallo tests opnieuw, of als Hallo nodig start de installatiewizard opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7ad40-140">Then run hello tests again or if necessary start hello Installation Wizard again.</span></span>
7. <span data-ttu-id="7ad40-141">Op Hallo **HPC DB configuratie** pagina, controleert u of **hoofdknooppunt** is ingeschakeld voor alle HPC-databases en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-141">On hello **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB-configuratie][install_hpc4]

8. <span data-ttu-id="7ad40-143">Accepteer de standaardselecties op Hallo overige pagina's van de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ad40-143">Accept default selections on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="7ad40-144">Op Hallo **vereiste onderdelen installeren** pagina, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-144">On hello **Install Required Components** page, click **Install**.</span></span>
   
    ![Installeren][install_hpc6]

9. <span data-ttu-id="7ad40-146">Nadat het Hallo-installatie is voltooid, schakel het selectievakje **Start HPC Cluster Manager** en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-146">After hello installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="7ad40-147">(U start HPC Cluster Manager in een latere stap.)</span><span class="sxs-lookup"><span data-stu-id="7ad40-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Voltooien][install_hpc7]

## <a name="prepare-hello-azure-subscription"></a><span data-ttu-id="7ad40-149">Hello Azure-abonnement voorbereiden</span><span class="sxs-lookup"><span data-stu-id="7ad40-149">Prepare hello Azure subscription</span></span>
<span data-ttu-id="7ad40-150">Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com) met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7ad40-150">Perform hello following steps in hello [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="7ad40-151">Na het voltooien van deze stappen kunt u Azure knooppunten uit Hallo lokale hoofdknooppunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="7ad40-151">After completing these steps, you can deploy Azure nodes from hello on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="7ad40-152">Maak ook een notitie van uw Azure-abonnement-ID, die u later nodig.</span><span class="sxs-lookup"><span data-stu-id="7ad40-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="7ad40-153">Hallo-ID vinden in **abonnementen** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="7ad40-153">Find hello ID in **Subscriptions** in hello portal.</span></span>
  > 

### <a name="upload-hello-default-management-certificate"></a><span data-ttu-id="7ad40-154">Hallo standaard management-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="7ad40-154">Upload hello default management certificate</span></span>
<span data-ttu-id="7ad40-155">HPC Pack installeert een zelfondertekend certificaat op de hoofdknooppunt hello, Hallo standaard Microsoft HPC Azure Management certificaat genaamd, die u als een Azure-beheercertificaat uploaden kunt.</span><span class="sxs-lookup"><span data-stu-id="7ad40-155">HPC Pack installs a self-signed certificate on hello head node, called hello Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="7ad40-156">Dit certificaat is opgegeven voor het testen en bewijs van concept implementaties toosecure Hallo verbinding tussen Hallo hoofdknooppunt en Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad40-156">This certificate is provided for testing and proof-of-concept deployments toosecure hello connection between hello head node and Azure.</span></span>

1. <span data-ttu-id="7ad40-157">Aanmelden van Hallo hoofdknooppunt computer, toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7ad40-157">From hello head node computer, sign in toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7ad40-158">Klik op **abonnementen** > *your_subscription_name*.</span><span class="sxs-lookup"><span data-stu-id="7ad40-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="7ad40-159">Klik op **beheercertificaten** > **uploaden**.4.</span><span class="sxs-lookup"><span data-stu-id="7ad40-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="7ad40-160">Blader op Hallo hoofdknooppunt voor Hallo bestand C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="7ad40-160">Browse on hello head node for hello file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="7ad40-161">Klik vervolgens op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="7ad40-162">Hallo **standaard HPC Azure Management** certificaat wordt weergegeven in de lijst met beheercertificaten Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ad40-162">hello **Default HPC Azure Management** certificate appears in hello list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="7ad40-163">Een Azure-cloudservice maken</span><span class="sxs-lookup"><span data-stu-id="7ad40-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="7ad40-164">Voor de beste prestaties door Hallo-cloudservice en Hallo storage-account (in een later stadium) te maken in Hallo dezelfde geografische regio.</span><span class="sxs-lookup"><span data-stu-id="7ad40-164">For best performance, create hello cloud service and hello storage account (in a later step) in hello same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="7ad40-165">Klik in de portal Hallo op **Cloudservices (klassiek)** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-165">In hello portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="7ad40-166">Een DNS-naam voor de service hello, kiest u een resourcegroep en een locatie en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-166">Type a DNS name for hello service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="7ad40-167">Een Azure-opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="7ad40-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="7ad40-168">Klik in de portal Hallo op **opslagaccounts (klassiek)** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-168">In hello portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="7ad40-169">Typ een naam voor het Hallo-account en selecteer Hallo **klassieke** implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="7ad40-169">Type a name for hello account, and select hello **Classic** deployment model.</span></span>

3. <span data-ttu-id="7ad40-170">Kies een resourcegroep en een locatie en andere instellingen laten op standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="7ad40-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="7ad40-171">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-171">Then click **Create**.</span></span>

## <a name="configure-hello-head-node"></a><span data-ttu-id="7ad40-172">Hallo-hoofdknooppunt configureren</span><span class="sxs-lookup"><span data-stu-id="7ad40-172">Configure hello head node</span></span>
<span data-ttu-id="7ad40-173">toouse HPC Cluster Manager toodeploy Azure knooppunten en toosubmit taken, voert u eerst een aantal configuratiestappen vereist cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad40-173">toouse HPC Cluster Manager toodeploy Azure nodes and toosubmit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="7ad40-174">Start op het hoofdknooppunt Hallo HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="7ad40-174">On hello head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="7ad40-175">Als hello **hoofdknooppunt selecteren** dialoogvenster wordt weergegeven, klikt u op **lokale Computer**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-175">If hello **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="7ad40-176">Hallo **implementatie takenlijst** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7ad40-176">hello **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="7ad40-177">Onder **implementatietaken vereist**, klikt u op **configureren van uw netwerk**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Netwerk configureren][config_hpc2]

3. <span data-ttu-id="7ad40-179">Selecteer in de Wizard netwerkconfiguratie hello, **alle knooppunten alleen op een bedrijfsnetwerk** (topologie 5).</span><span class="sxs-lookup"><span data-stu-id="7ad40-179">In hello Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="7ad40-180">Deze netwerkconfiguratie is Hallo eenvoudigste voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="7ad40-180">This network configuration is hello simplest for demonstration purposes.</span></span>
   
    ![Topologie 5][config_hpc3]
   
4. <span data-ttu-id="7ad40-182">Klik op **volgende** tooaccept standaardwaarden op pagina's van de wizard Hallo resterende Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ad40-182">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="7ad40-183">Klik vervolgens op Hallo **revisie** tabblad **configureren** toocomplete Hallo-netwerkconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="7ad40-183">Then, on hello **Review** tab, click **Configure** toocomplete hello network configuration.</span></span>

5. <span data-ttu-id="7ad40-184">In Hallo **implementatie takenlijst**, klikt u op **referenties van de installatie**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-184">In hello **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="7ad40-185">In Hallo **Installatiereferenties** in het dialoogvenster Hallo typt u de referenties van Hallo-domeinaccount dat u tooinstall HPC Pack gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7ad40-185">In hello **Installation Credentials** dialog box, type hello credentials of hello domain account that you used tooinstall HPC Pack.</span></span> <span data-ttu-id="7ad40-186">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-186">Then click **OK**.</span></span> 
   
    ![Van Installatiereferenties][config_hpc6]
   
7. <span data-ttu-id="7ad40-188">In Hallo **implementatie takenlijst**, klikt u op **configureren Hallo naamgeving van nieuwe knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-188">In hello **Deployment To-do List**, click **Configure hello naming of new nodes**.</span></span>

8. <span data-ttu-id="7ad40-189">In Hallo **Geef knooppunt Naming reeks** dialoogvenster accepteer Hallo-standaard naamgevingscontext reeks en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-189">In hello **Specify Node Naming Series** dialog box, accept hello default naming series and click **OK**.</span></span> <span data-ttu-id="7ad40-190">Hoewel hello Azure knooppunten die u in deze zelfstudie toevoegen zijn benoemde automatisch deze stap hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="7ad40-190">Complete this step even though hello Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Naamgeving van knooppunt][config_hpc8]
   
9. <span data-ttu-id="7ad40-192">In Hallo **implementatie takenlijst**, klikt u op **maken van een knooppuntsjabloon**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-192">In hello **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="7ad40-193">Later in de zelfstudie hello gebruikt u Hallo sjabloon tooadd Azure knooppunten toohello knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-193">Later in hello tutorial, you use hello node template tooadd Azure nodes toohello cluster.</span></span>

10. <span data-ttu-id="7ad40-194">Hallo in Wizard-knooppunt sjabloon maken, Hallo volgende doen:</span><span class="sxs-lookup"><span data-stu-id="7ad40-194">In hello Create Node Template Wizard, do hello following:</span></span>
    
    <span data-ttu-id="7ad40-195">a.</span><span class="sxs-lookup"><span data-stu-id="7ad40-195">a.</span></span> <span data-ttu-id="7ad40-196">Op Hallo **knooppunttype sjabloon kiezen** pagina, klikt u op **Windows Azure-knooppuntsjabloon**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-196">On hello **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Knooppuntsjabloon][config_hpc10]
    
    <span data-ttu-id="7ad40-198">b.</span><span class="sxs-lookup"><span data-stu-id="7ad40-198">b.</span></span> <span data-ttu-id="7ad40-199">Klik op **volgende** tooaccept Hallo standaardnaam sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7ad40-199">Click **Next** tooaccept hello default template name.</span></span>
    
    <span data-ttu-id="7ad40-200">c.</span><span class="sxs-lookup"><span data-stu-id="7ad40-200">c.</span></span> <span data-ttu-id="7ad40-201">Op Hallo **abonnementsgegevens bieden** pagina, Voer uw Azure-abonnement-ID (beschikbaar in uw Azure-account-informatie).</span><span class="sxs-lookup"><span data-stu-id="7ad40-201">On hello **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="7ad40-202">Klik op **beheercertificaat**, zoeken naar **Microsoft HPC Azure Management Default.**</span><span class="sxs-lookup"><span data-stu-id="7ad40-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="7ad40-203">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-203">Then click **Next**.</span></span>
    
    ![Knooppuntsjabloon][config_hpc12]
    
    <span data-ttu-id="7ad40-205">d.</span><span class="sxs-lookup"><span data-stu-id="7ad40-205">d.</span></span> <span data-ttu-id="7ad40-206">Op Hallo **servicegegevens bieden** pagina, selecteer Hallo-cloudservice en Hallo storage-account dat u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7ad40-206">On hello **Provide Service Information** page, select hello cloud service and hello storage account that you created in a previous step.</span></span> <span data-ttu-id="7ad40-207">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-207">Then click **Next**.</span></span>
    
    ![Knooppuntsjabloon][config_hpc13]
    
    <span data-ttu-id="7ad40-209">e.</span><span class="sxs-lookup"><span data-stu-id="7ad40-209">e.</span></span> <span data-ttu-id="7ad40-210">Klik op **volgende** tooaccept standaardwaarden op pagina's van de wizard Hallo resterende Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ad40-210">Click **Next** tooaccept default values on hello remaining pages of hello wizard.</span></span> <span data-ttu-id="7ad40-211">Klik vervolgens op Hallo **revisie** tabblad **maken** toocreate Hallo knooppuntsjabloon.</span><span class="sxs-lookup"><span data-stu-id="7ad40-211">Then, on hello **Review** tab, click **Create** toocreate hello node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="7ad40-212">Standaard bevat hello Azure knooppuntsjabloon instellingen voor toostart (ingericht) en stop Hallo knooppunten handmatig met behulp van HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="7ad40-212">By default, hello Azure node template includes settings for you toostart (provision) and stop hello nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="7ad40-213">U kunt desgewenst een toostart planning configureren en Azure knooppunten automatisch Hallo stoppen.</span><span class="sxs-lookup"><span data-stu-id="7ad40-213">You can optionally configure a schedule toostart and stop hello Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-toohello-cluster"></a><span data-ttu-id="7ad40-214">Azure knooppunten toohello cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="7ad40-214">Add Azure nodes toohello cluster</span></span>
<span data-ttu-id="7ad40-215">Hallo sjabloon tooadd Azure knooppunten toohello knooppunten nu gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7ad40-215">Now use hello node template tooadd Azure nodes toohello cluster.</span></span> <span data-ttu-id="7ad40-216">Toe te voegen Hallo knooppunten toohello cluster hun configuratiegegevens worden opgeslagen zodat u starten kunt (ingericht) ze op elk gewenst moment in Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7ad40-216">Adding hello nodes toohello cluster stores their configuration information so that you can start (provision) them at any time in hello cloud service.</span></span> <span data-ttu-id="7ad40-217">Uw abonnement alleen opgehaald in rekening gebracht voor Azure knooppunten nadat Hallo exemplaren worden uitgevoerd in Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7ad40-217">Your subscription only gets charged for Azure nodes after hello instances are running in hello cloud service.</span></span>

<span data-ttu-id="7ad40-218">Volg deze stappen tooadd twee kleine knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-218">Follow these steps tooadd two Small nodes.</span></span>

1. <span data-ttu-id="7ad40-219">In HPC Cluster Manager, klikt u op **knooppunt Management** (aangeroepen **bronbeheer** in huidige versies van HPC Pack) > **knooppunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Knooppunt toevoegen][add_node1]

2. <span data-ttu-id="7ad40-221">Hallo in de Wizard knooppunt toevoegen op Hallo **implementatiemethode selecteren** pagina, klikt u op **toevoegen Windows Azure knooppunten**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-221">In hello Add Node Wizard, on hello **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Azure knooppunt toevoegen][add_node1_1]

3. <span data-ttu-id="7ad40-223">Op Hallo **nieuwe knooppunten opgeven** pagina, selecteer hello Azure knooppuntsjabloon die u eerder hebt gemaakt (standaard genoemd **AzureNode standaardsjabloon**).</span><span class="sxs-lookup"><span data-stu-id="7ad40-223">On hello **Specify New Nodes** page, select hello Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="7ad40-224">Geef vervolgens **2** knooppunten van de grootte van **kleine**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Knooppunten opgeven][add_node2]
   
4. <span data-ttu-id="7ad40-226">Op Hallo **voltooien Hallo Wizard knooppunt toevoegen** pagina, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-226">On hello **Completing hello Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="7ad40-227">Twee Azure knooppunten, met de naam **AzureCN 0001** en **AzureCN 0002**, worden nu weergegeven in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="7ad40-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="7ad40-228">Beide zijn in Hallo **niet geïmplementeerd** status.</span><span class="sxs-lookup"><span data-stu-id="7ad40-228">Both are in hello **Not-Deployed** state.</span></span>
   
    ![Toegevoegde knooppunten][add_node3]

## <a name="start-hello-azure-nodes"></a><span data-ttu-id="7ad40-230">Start hello Azure knooppunten</span><span class="sxs-lookup"><span data-stu-id="7ad40-230">Start hello Azure nodes</span></span>
<span data-ttu-id="7ad40-231">Als u wilt dat wordt toouse Hallo-clusterbronnen in Azure, gebruik HPC Cluster Manager toostart (ingericht) hello Azure knooppunten en ze online brengt.</span><span class="sxs-lookup"><span data-stu-id="7ad40-231">When you want toouse hello cluster resources in Azure, use HPC Cluster Manager toostart (provision) hello Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="7ad40-232">In HPC Cluster Manager, klikt u op **knooppunt Management** (aangeroepen **bronbeheer** in huidige versies van HPC Pack), en selecteer hello Azure knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select hello Azure nodes.</span></span>

2. <span data-ttu-id="7ad40-233">Klik op **Start**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Beginknooppunten][add_node4]
   
    <span data-ttu-id="7ad40-235">Hallo knooppunten overgang toohello **inrichten** status.</span><span class="sxs-lookup"><span data-stu-id="7ad40-235">hello nodes transition toohello **Provisioning** state.</span></span> <span data-ttu-id="7ad40-236">Weergave hello inrichting logboek tootrack Hallo inrichting uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7ad40-236">View hello provisioning log tootrack hello provisioning progress.</span></span>
   
    ![Inrichten knooppunten][add_node6]

3. <span data-ttu-id="7ad40-238">Na een paar minuten hello Azure knooppunten klaar bent met het inrichten en in Hallo **Offline** status.</span><span class="sxs-lookup"><span data-stu-id="7ad40-238">After a few minutes, hello Azure nodes finish provisioning and are in hello **Offline** state.</span></span> <span data-ttu-id="7ad40-239">In deze status is Hallo rolinstanties worden uitgevoerd, maar taken cluster nog niet accepteren.</span><span class="sxs-lookup"><span data-stu-id="7ad40-239">In this state, hello role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="7ad40-240">tooconfirm die Hallo rolinstanties in hello Azure-portal worden uitgevoerd, klikt u op **Cloudservices (klassiek)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="7ad40-240">tooconfirm that hello role instances are running, in hello Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="7ad40-241">U ziet twee **HpcWorkerRole** exemplaren (knooppunten) uitgevoerd in Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7ad40-241">You should see two **HpcWorkerRole** instances (nodes) running in hello service.</span></span> <span data-ttu-id="7ad40-242">HPC Pack implementeert ook automatisch twee **HpcProxy** (grootte normaal) toohandle communicatie tussen Hallo hoofdknooppunt en Azure-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="7ad40-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) toohandle communication between hello head node and Azure.</span></span>

   ![Exemplaren die worden uitgevoerd][view_instances1]

5. <span data-ttu-id="7ad40-244">toobring hello Azure knooppunten online toorun taken, selecteer Hallo knooppunten, klik met de rechtermuisknop en klik vervolgens op het cluster **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-244">toobring hello Azure nodes online toorun cluster jobs, select hello nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Offline knooppunten][add_node7]
   
    <span data-ttu-id="7ad40-246">HPC Cluster Manager geeft aan dat de knooppunten Hallo in Hallo **Online** status.</span><span class="sxs-lookup"><span data-stu-id="7ad40-246">HPC Cluster Manager indicates that hello nodes are in hello **Online** state.</span></span>

## <a name="run-a-command-across-hello-cluster"></a><span data-ttu-id="7ad40-247">Een opdracht over Hallo-cluster wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="7ad40-247">Run a command across hello cluster</span></span>
<span data-ttu-id="7ad40-248">toocheck hello installatie, gebruik Hallo HPC Pack **clusrun** opdracht toorun een opdracht of een toepassing op een of meer clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-248">toocheck hello installation, use hello HPC Pack **clusrun** command toorun a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="7ad40-249">Als een eenvoudig voorbeeld gebruiken **clusrun** tooget Hallo IP-adresconfiguratie van hello Azure knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-249">As a simple example, use **clusrun** tooget hello IP configuration of hello Azure nodes.</span></span>

1. <span data-ttu-id="7ad40-250">Op het hoofdknooppunt hello, open een opdrachtprompt als beheerder.</span><span class="sxs-lookup"><span data-stu-id="7ad40-250">On hello head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="7ad40-251">Type Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7ad40-251">Type hello following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="7ad40-252">Als u wordt gevraagd, voert u het wachtwoord van de cluster.</span><span class="sxs-lookup"><span data-stu-id="7ad40-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="7ad40-253">U ziet opdracht vergelijkbare toohello volgende uitvoer.</span><span class="sxs-lookup"><span data-stu-id="7ad40-253">You should see command output similar toohello following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="7ad40-255">Voer een test</span><span class="sxs-lookup"><span data-stu-id="7ad40-255">Run a test job</span></span>
<span data-ttu-id="7ad40-256">Nu een testtaak die wordt uitgevoerd op Hallo hybride cluster indienen.</span><span class="sxs-lookup"><span data-stu-id="7ad40-256">Now submit a test job that runs on hello hybrid cluster.</span></span> <span data-ttu-id="7ad40-257">In dit voorbeeld is een eenvoudige parametrische taak (een soort intrinsiek parallelle berekeningen).</span><span class="sxs-lookup"><span data-stu-id="7ad40-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="7ad40-258">In dit voorbeeld wordt uitgevoerd subtaken met Hallo voor het toevoegen van een geheel getal tooitself **/a ingesteld** opdracht.</span><span class="sxs-lookup"><span data-stu-id="7ad40-258">This example runs subtasks that add an integer tooitself by using hello **set /a** command.</span></span> <span data-ttu-id="7ad40-259">Alle Hallo knooppunten in cluster Hallo bijdragen toofinishing Hallo subtaken voor gehele getallen van 1 too100.</span><span class="sxs-lookup"><span data-stu-id="7ad40-259">All hello nodes in hello cluster contribute toofinishing hello subtasks for integers from 1 too100.</span></span>

1. <span data-ttu-id="7ad40-260">Klik in HPC Cluster Manager op **Jobbeheer** > **nieuwe parametrische Sweep taak**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nieuwe taak][test_job1]

2. <span data-ttu-id="7ad40-262">In Hallo **nieuwe parametrische Sweep taak** het dialoogvenster **opdrachtregel**, type `set /a *+*` (overschrijven Hallo standaardopdrachtregel die wordt weergegeven).</span><span class="sxs-lookup"><span data-stu-id="7ad40-262">In hello **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting hello default command line that appears).</span></span> <span data-ttu-id="7ad40-263">Laat de standaardwaarden voor Hallo resterende instellingen en klik vervolgens op **indienen** toosubmit Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="7ad40-263">Leave default values for hello remaining settings, and then click **Submit** toosubmit hello job.</span></span>
   
    ![Parametrische opschoning][param_sweep1]

3. <span data-ttu-id="7ad40-265">Wanneer het Hallo-taak is voltooid, dubbelklikt u op Hallo **mijn Sweep taak** taak.</span><span class="sxs-lookup"><span data-stu-id="7ad40-265">When hello job is finished, double-click hello **My Sweep Task** job.</span></span>

4. <span data-ttu-id="7ad40-266">Klik op **taken weergeven**, en klik vervolgens op een subtaak tooview Hallo berekend uitvoer van deze subtaak.</span><span class="sxs-lookup"><span data-stu-id="7ad40-266">Click **View Tasks**, and then click a subtask tooview hello calculated output of that subtask.</span></span>
   
    ![Resultaten van de taak][view_job361]

5. <span data-ttu-id="7ad40-268">toosee welk knooppunt Hallo berekening uitgevoerd voor deze subtaak, klikt u op **toegewezen knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-268">toosee which node performed hello calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="7ad40-269">(U mogelijk de naam van een ander knooppunt weergegeven voor uw cluster.)</span><span class="sxs-lookup"><span data-stu-id="7ad40-269">(Your cluster might show a different node name.)</span></span>
   
    ![Resultaten van de taak][view_job362]

## <a name="stop-hello-azure-nodes"></a><span data-ttu-id="7ad40-271">Stop hello Azure knooppunten</span><span class="sxs-lookup"><span data-stu-id="7ad40-271">Stop hello Azure nodes</span></span>
<span data-ttu-id="7ad40-272">Nadat u de cluster Hallo uitproberen, stop hello Azure knooppunten tooavoid onnodige kosten tooyour account.</span><span class="sxs-lookup"><span data-stu-id="7ad40-272">After you try out hello cluster, stop hello Azure nodes tooavoid unnecessary charges tooyour account.</span></span> <span data-ttu-id="7ad40-273">Deze stap Hallo cloudservice stopt en verwijdert hello Azure rolinstanties.</span><span class="sxs-lookup"><span data-stu-id="7ad40-273">This step stops hello cloud service and removes hello Azure role instances.</span></span>

1. <span data-ttu-id="7ad40-274">In HPC Cluster Manager in **knooppunt Management** (aangeroepen **bronbeheer** in eerdere versies van HPC Pack), selecteert u beide Azure knooppunten.</span><span class="sxs-lookup"><span data-stu-id="7ad40-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="7ad40-275">Klik vervolgens op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-275">Then, click **Stop**.</span></span>
   
    ![Knooppunten stoppen][stop_node1]

2. <span data-ttu-id="7ad40-277">In Hallo **stoppen Windows Azure knooppunten** in het dialoogvenster, klikt u op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-277">In hello **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="7ad40-278">Hallo knooppunten overgang toohello **stoppen** status.</span><span class="sxs-lookup"><span data-stu-id="7ad40-278">hello nodes transition toohello **Stopping** state.</span></span> <span data-ttu-id="7ad40-279">Na een paar minuten HPC Cluster Manager geeft aan dat de knooppunten Hallo **niet geïmplementeerd**.</span><span class="sxs-lookup"><span data-stu-id="7ad40-279">After a few minutes, HPC Cluster Manager shows that hello nodes are **Not-Deployed**.</span></span>
   
    ![Niet-geïmplementeerde knooppunten][stop_node4]

4. <span data-ttu-id="7ad40-281">tooconfirm die Hallo rolinstanties worden niet meer in Azure worden uitgevoerd in Azure portal op Hallo **Cloudservices (klassiek)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="7ad40-281">tooconfirm that hello role instances are no longer running in Azure, in hello Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="7ad40-282">Er zijn geen exemplaren worden geïmplementeerd in de productieomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="7ad40-282">No instances are deployed in hello production environment.</span></span> 
   
    <span data-ttu-id="7ad40-283">Deze zelfstudie Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7ad40-283">This completes hello tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ad40-284">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7ad40-284">Next steps</span></span>
* <span data-ttu-id="7ad40-285">Hallo-documentatie voor verkennen [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="7ad40-285">Explore hello documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="7ad40-286">Zie tooset van een hybride implementatie van het cluster op groter schaal HPC Pack [tooAzure Worker-Rolexemplaren met Microsoft HPC Pack Burst](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="7ad40-286">tooset up a hybrid HPC Pack cluster deployment at greater scale, see [Burst tooAzure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="7ad40-287">Voor andere manieren toocreate een HPC Pack-cluster in Azure, met inbegrip van met behulp van Azure Resource Manager-sjablonen, Zie [opties voor HPC-cluster met Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ad40-287">For other ways toocreate an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


[Overview]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/hybrid_cluster_overview.png
[install_hpc1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc1.png
[install_hpc4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc4.png
[install_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc6.png
[install_hpc7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc7.png
[install_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/install_hpc10.png
[config_hpc2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc2.png
[config_hpc3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc3.png
[config_hpc6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc6.png
[config_hpc8]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc8.png
[config_hpc10]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc10.png
[config_hpc12]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc12.png
[config_hpc13]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/config_hpc13.png
[add_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1.png
[add_node1_1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node1_1.png
[add_node2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node2.png
[add_node3]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node3.png
[add_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node4.png
[add_node6]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node6.png
[add_node7]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/add_node7.png
[view_instances1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances1.png
[clusrun1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/clusrun1.png
[test_job1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/test_job1.png
[param_sweep1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/param_sweep1.png
[view_job361]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job361.png
[view_job362]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_job362.png
[stop_node1]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node1.png
[stop_node4]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/stop_node4.png
[view_instances2]: ./media/cloud-services-setup-hybrid-hpcpack-cluster/view_instances2.png

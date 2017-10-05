---
title: Een hybride HPC Pack cluster in Azure instellen | Microsoft Docs
description: Informatie over het gebruik van Microsoft HPC Pack en Azure voor het instellen van een klein, hybride high performance computing-cluster (HPC)
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
ms.openlocfilehash: f6dc9657e64160be1e68a7356863b53131e9b3c3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-hybrid-high-performance-computing-hpc-cluster-with-microsoft-hpc-pack-and-on-demand-azure-compute-nodes"></a><span data-ttu-id="a5884-103">Een hybride high performance computing-cluster (HPC) met Microsoft HPC Pack en Azure rekenknooppunten op aanvraag instellen</span><span class="sxs-lookup"><span data-stu-id="a5884-103">Set up a hybrid high performance computing (HPC) cluster with Microsoft HPC Pack and on-demand Azure compute nodes</span></span>
<span data-ttu-id="a5884-104">Gebruik Microsoft HPC Pack 2012 R2 en Azure voor het instellen van een klein, hybride high performance computing-cluster (HPC).</span><span class="sxs-lookup"><span data-stu-id="a5884-104">Use Microsoft HPC Pack 2012 R2 and Azure to set up a small, hybrid high performance computing (HPC) cluster.</span></span> <span data-ttu-id="a5884-105">Het cluster weergegeven in dit artikel bestaat uit een lokale HPC Pack-hoofdknooppunt en sommige compute knooppunten die u implementeert op aanvraag in een Azure-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a5884-105">The cluster shown in this article consists of an on-premises HPC Pack head node and some compute nodes you deploy on-demand in an Azure cloud service.</span></span> <span data-ttu-id="a5884-106">Vervolgens kunt u op het cluster hybrid compute-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a5884-106">You can then run compute jobs on the hybrid cluster.</span></span>

![Hybride HPC-cluster][Overview] 

<span data-ttu-id="a5884-108">Deze zelfstudie ziet u een benadering wel cluster 'burst naar de cloud' schaalbare, bellen op Azure-resources gebruiken rekenintensieve toepassingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="a5884-108">This tutorial shows one approach, sometimes called cluster "burst to the cloud," to use scalable, on-demand Azure resources to run compute-intensive applications.</span></span>

<span data-ttu-id="a5884-109">Deze zelfstudie wordt ervan uitgegaan dat geen ervaring met rekenclusters of HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a5884-109">This tutorial assumes no prior experience with compute clusters or HPC Pack.</span></span> <span data-ttu-id="a5884-110">Het is bedoeld alleen bij het implementeren van een hybride rekencluster snel voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="a5884-110">It is intended only to help you deploy a hybrid compute cluster quickly for demonstration purposes.</span></span> <span data-ttu-id="a5884-111">Zie voor overwegingen en stappen voor het implementeren van een hybride HPC Pack cluster op groter schaal in een productieomgeving of HPC Pack 2016 gebruiken de [gedetailleerde richtlijnen](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a5884-111">For considerations and steps to deploy a hybrid HPC Pack cluster at greater scale in a production environment, or to use HPC Pack 2016, see the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span> <span data-ttu-id="a5884-112">Voor andere scenario's met HPC Pack, met inbegrip van geautomatiseerde implementatie van het cluster in Azure virtuele machines, Zie [opties voor HPC-cluster met Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5884-112">For other scenarios with HPC Pack, including automated cluster deployment in Azure virtual machines, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a5884-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a5884-113">Prerequisites</span></span>
* <span data-ttu-id="a5884-114">**Azure-abonnement** -als u geen Azure-abonnement hebt, kunt u een [gratis account](https://azure.microsoft.com/free/) binnen een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="a5884-114">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/free/) in just a couple of minutes.</span></span>
* <span data-ttu-id="a5884-115">**Een on-premises-computer met Windows Server 2012 R2 of Windows Server 2012** -deze computer gebruiken als het hoofdknooppunt van het HPC-cluster.</span><span class="sxs-lookup"><span data-stu-id="a5884-115">**An on-premises computer running Windows Server 2012 R2 or Windows Server 2012** - Use this computer as the head node of the HPC cluster.</span></span> <span data-ttu-id="a5884-116">Als u al Windows Server worden niet uitgevoerd, kunt u downloaden en installeren van een [evaluatieversie](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span><span class="sxs-lookup"><span data-stu-id="a5884-116">If you aren't already running Windows Server, you can download and install an [evaluation version](https://www.microsoft.com/evalcenter/evaluate-windows-server-2012-r2).</span></span>
  
  * <span data-ttu-id="a5884-117">De computer moet worden toegevoegd aan Active Directory-domein.</span><span class="sxs-lookup"><span data-stu-id="a5884-117">The computer must be joined to an Active Directory domain.</span></span> <span data-ttu-id="a5884-118">Voor testdoeleinden kunt u de computer hoofdknooppunt configureren als een domeincontroller.</span><span class="sxs-lookup"><span data-stu-id="a5884-118">For test purposes, you can configure the head node computer as a domain controller.</span></span> <span data-ttu-id="a5884-119">De Active Directory Domain Services-serverfunctie toevoegen en het niveau van het hoofdknooppunt computer als een domeincontroller, Zie de documentatie voor Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a5884-119">To add the Active Directory Domain Services server role and promote the head node computer as a domain controller, see the documentation for Windows Server.</span></span>
  * <span data-ttu-id="a5884-120">Ter ondersteuning van HPC Pack, het besturingssysteem moet worden geïnstalleerd in een van de volgende talen: Engels, Japans of Chinees (Vereenvoudigd).</span><span class="sxs-lookup"><span data-stu-id="a5884-120">To support HPC Pack, the operating system must be installed in one of these languages: English, Japanese, or Chinese (Simplified).</span></span>
  * <span data-ttu-id="a5884-121">Controleer of belangrijke en kritieke updates zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a5884-121">Verify that important and critical updates are installed.</span></span>
* <span data-ttu-id="a5884-122">**HPC Pack 2012 R2** - [downloaden](http://go.microsoft.com/fwlink/p/?linkid=328024) de installatie van het pakket voor de nieuwste versie kosteloos en kopieer de bestanden naar de computer van het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a5884-122">**HPC Pack 2012 R2** - [Download](http://go.microsoft.com/fwlink/p/?linkid=328024) the installation package for the latest version free of charge and copy the files to the head node computer.</span></span> <span data-ttu-id="a5884-123">Kies installatiebestanden in dezelfde taal als de installatie van Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a5884-123">Choose installation files in the same language as your installation of Windows Server.</span></span>

    >[!NOTE]
    > <span data-ttu-id="a5884-124">Als u wilt HPC Pack 2016 gebruiken in plaats van HPC Pack 2012 R2 is aanvullende configuratie nodig.</span><span class="sxs-lookup"><span data-stu-id="a5884-124">If you want to use HPC Pack 2016 instead of HPC Pack 2012 R2, additional configuration is needed.</span></span> <span data-ttu-id="a5884-125">Zie de [gedetailleerde richtlijnen](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a5884-125">See the [detailed guidance](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
    > 
* <span data-ttu-id="a5884-126">**Domeinaccount** -dit account moet worden geconfigureerd met lokale Administrator-machtigingen op het hoofdknooppunt HPC Pack te installeren.</span><span class="sxs-lookup"><span data-stu-id="a5884-126">**Domain account** - This account must be configured with local Administrator permissions on the head node to install HPC Pack.</span></span>
* <span data-ttu-id="a5884-127">**TCP-verbinding op poort 443** vanaf het hoofdknooppunt van naar Azure.</span><span class="sxs-lookup"><span data-stu-id="a5884-127">**TCP connectivity on port 443** from the head node to Azure.</span></span>

## <a name="install-hpc-pack-on-the-head-node"></a><span data-ttu-id="a5884-128">HPC Pack installeren op het hoofdknooppunt</span><span class="sxs-lookup"><span data-stu-id="a5884-128">Install HPC Pack on the head node</span></span>
<span data-ttu-id="a5884-129">U eerst installeren Microsoft HPC Pack op uw lokale computer met Windows Server.</span><span class="sxs-lookup"><span data-stu-id="a5884-129">You first install Microsoft HPC Pack on your on-premises computer running Windows Server.</span></span> <span data-ttu-id="a5884-130">Deze computer wordt het hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="a5884-130">This computer becomes the head node of the cluster.</span></span>

1. <span data-ttu-id="a5884-131">Meld u als een domeinaccount met lokale beheerdersmachtigingen heeft op met het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a5884-131">Log on to the head node by using a domain account that has local Administrator permissions.</span></span>

2. <span data-ttu-id="a5884-132">Start de installatiewizard van HPC Pack door het uitvoeren van Setup.exe uit de installatiebestanden HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a5884-132">Start the HPC Pack Installation Wizard by running Setup.exe from the HPC Pack installation files.</span></span>

3. <span data-ttu-id="a5884-133">Op de **HPC Pack 2012 R2 installeren** scherm, klikt u op **nieuwe installatie of het toevoegen van nieuwe functies aan een bestaande installatie**.</span><span class="sxs-lookup"><span data-stu-id="a5884-133">On the **HPC Pack 2012 R2 Setup** screen, click **New installation or add new features to an existing installation**.</span></span>

    ![HPC Pack 2012 Setup][install_hpc1]

4. <span data-ttu-id="a5884-135">Op de **Microsoft Software gebruikersovereenkomst pagina**, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-135">On the **Microsoft Software User Agreement page**, click **Next**.</span></span>

5. <span data-ttu-id="a5884-136">Op de **Type installatie selecteren** pagina, klikt u op **een nieuw HPC-cluster maken door het maken van een hoofdknooppunt**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-136">On the **Select Installation Type** page, click **Create a new HPC cluster by creating a head node**, and then click **Next**.</span></span>

6. <span data-ttu-id="a5884-137">De wizard wordt uitgevoerd voor verschillende voorafgaand aan installatie tests.</span><span class="sxs-lookup"><span data-stu-id="a5884-137">The wizard runs several pre-installation tests.</span></span> <span data-ttu-id="a5884-138">Klik op **volgende** op de **installatieregels** pagina als u alle tests zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="a5884-138">Click **Next** on the **Installation Rules** page if all tests pass.</span></span> <span data-ttu-id="a5884-139">Anders Bekijk de informatie en breng eventueel benodigde wijzigingen in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="a5884-139">Otherwise, review the information provided and make any necessary changes in your environment.</span></span> <span data-ttu-id="a5884-140">Voer de tests opnieuw, of indien nodig start u de installatiewizard opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a5884-140">Then run the tests again or if necessary start the Installation Wizard again.</span></span>
7. <span data-ttu-id="a5884-141">Op de **HPC DB configuratie** pagina, controleert u of **hoofdknooppunt** is ingeschakeld voor alle HPC-databases en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-141">On the **HPC DB Configuration** page, make sure **Head Node** is selected for all HPC databases, and then click **Next**.</span></span> 

    ![DB-configuratie][install_hpc4]

8. <span data-ttu-id="a5884-143">Accepteer de standaardselecties op de overige pagina's van de wizard.</span><span class="sxs-lookup"><span data-stu-id="a5884-143">Accept default selections on the remaining pages of the wizard.</span></span> <span data-ttu-id="a5884-144">Op de **vereiste onderdelen installeren** pagina, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="a5884-144">On the **Install Required Components** page, click **Install**.</span></span>
   
    ![Installeren][install_hpc6]

9. <span data-ttu-id="a5884-146">Nadat de installatie is voltooid, schakel het selectievakje **Start HPC Cluster Manager** en klik vervolgens op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="a5884-146">After the installation completes, uncheck **Start HPC Cluster Manager** and then click **Finish**.</span></span> <span data-ttu-id="a5884-147">(U start HPC Cluster Manager in een latere stap.)</span><span class="sxs-lookup"><span data-stu-id="a5884-147">(You start HPC Cluster Manager in a later step.)</span></span>
   
    ![Voltooien][install_hpc7]

## <a name="prepare-the-azure-subscription"></a><span data-ttu-id="a5884-149">Voorbereiden van het Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="a5884-149">Prepare the Azure subscription</span></span>
<span data-ttu-id="a5884-150">Voer de volgende stappen uit in de [Azure-portal](https://portal.azure.com) met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a5884-150">Perform the following steps in the [Azure portal](https://portal.azure.com) with your Azure subscription.</span></span> <span data-ttu-id="a5884-151">Na het voltooien van deze stappen kunt u Azure knooppunten van het hoofdknooppunt van het lokale implementeren.</span><span class="sxs-lookup"><span data-stu-id="a5884-151">After completing these steps, you can deploy Azure nodes from the on-premises head node.</span></span> 
  
  > [!NOTE]
  > <span data-ttu-id="a5884-152">Maak ook een notitie van uw Azure-abonnement-ID, die u later nodig.</span><span class="sxs-lookup"><span data-stu-id="a5884-152">Also make a note of your Azure subscription ID, which you need later.</span></span> <span data-ttu-id="a5884-153">De ID vinden in **abonnementen** in de portal.</span><span class="sxs-lookup"><span data-stu-id="a5884-153">Find the ID in **Subscriptions** in the portal.</span></span>
  > 

### <a name="upload-the-default-management-certificate"></a><span data-ttu-id="a5884-154">Het standaard management-certificaat uploaden</span><span class="sxs-lookup"><span data-stu-id="a5884-154">Upload the default management certificate</span></span>
<span data-ttu-id="a5884-155">HPC Pack installeert een zelfondertekend certificaat op het hoofdknooppunt, de standaard van Microsoft HPC Azure Management certificaat genaamd, die u als een Azure-beheercertificaat uploaden kunt.</span><span class="sxs-lookup"><span data-stu-id="a5884-155">HPC Pack installs a self-signed certificate on the head node, called the Default Microsoft HPC Azure Management certificate, that you can upload as an Azure management certificate.</span></span> <span data-ttu-id="a5884-156">Dit certificaat wordt aangeboden voor testen en bewijs van concept implementaties voor het beveiligen van de verbinding tussen het hoofdknooppunt en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5884-156">This certificate is provided for testing and proof-of-concept deployments to secure the connection between the head node and Azure.</span></span>

1. <span data-ttu-id="a5884-157">Vanaf het hoofdknooppunt computer, moet u zich aanmelden bij de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5884-157">From the head node computer, sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="a5884-158">Klik op **abonnementen** > *your_subscription_name*.</span><span class="sxs-lookup"><span data-stu-id="a5884-158">Click **Subscriptions** > *your_subscription_name*.</span></span>

3. <span data-ttu-id="a5884-159">Klik op **beheercertificaten** > **uploaden**.4.</span><span class="sxs-lookup"><span data-stu-id="a5884-159">Click **Management certificates** > **Upload**.4.</span></span> <span data-ttu-id="a5884-160">Blader op het hoofdknooppunt van het bestand C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span><span class="sxs-lookup"><span data-stu-id="a5884-160">Browse on the head node for the file C:\Program Files\Microsoft HPC Pack 2012\Bin\hpccert.cer.</span></span> <span data-ttu-id="a5884-161">Klik vervolgens op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="a5884-161">Then, click **Upload**.</span></span>

   
<span data-ttu-id="a5884-162">De **standaard HPC Azure Management** certificaat wordt weergegeven in de lijst met beheercertificaten.</span><span class="sxs-lookup"><span data-stu-id="a5884-162">The **Default HPC Azure Management** certificate appears in the list of management certificates.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="a5884-163">Een Azure-cloudservice maken</span><span class="sxs-lookup"><span data-stu-id="a5884-163">Create an Azure cloud service</span></span>
> [!NOTE]
> <span data-ttu-id="a5884-164">Maak de cloudservice en het opslagaccount (in een later stadium) in dezelfde geografische regio voor de beste prestaties.</span><span class="sxs-lookup"><span data-stu-id="a5884-164">For best performance, create the cloud service and the storage account (in a later step) in the same geographic region.</span></span>
> 
> 

1. <span data-ttu-id="a5884-165">Klik in de portal op **Cloudservices (klassiek)** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a5884-165">In the portal, click **Cloud services (classic)** > **+Add**.</span></span>

2.  <span data-ttu-id="a5884-166">Typ een DNS-naam voor de service, kiest u een resourcegroep en een locatie en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="a5884-166">Type a DNS name for the service, choose a resource group and a location, and then click **Create**.</span></span>


### <a name="create-an-azure-storage-account"></a><span data-ttu-id="a5884-167">Een Azure-opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="a5884-167">Create an Azure storage account</span></span>
1. <span data-ttu-id="a5884-168">Klik in de portal op **opslagaccounts (klassiek)** > **+ toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a5884-168">In the portal, click **Storage accounts (classic)** > **+Add**.</span></span>

2. <span data-ttu-id="a5884-169">Typ een naam voor het account en selecteer de **klassieke** implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a5884-169">Type a name for the account, and select the **Classic** deployment model.</span></span>

3. <span data-ttu-id="a5884-170">Kies een resourcegroep en een locatie en andere instellingen laten op standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="a5884-170">Choose a resource group and a location, and leave other settings at default values.</span></span> <span data-ttu-id="a5884-171">Klik vervolgens op **Maken**.</span><span class="sxs-lookup"><span data-stu-id="a5884-171">Then click **Create**.</span></span>

## <a name="configure-the-head-node"></a><span data-ttu-id="a5884-172">Het hoofdknooppunt configureren</span><span class="sxs-lookup"><span data-stu-id="a5884-172">Configure the head node</span></span>
<span data-ttu-id="a5884-173">Als u HPC Cluster Manager Azure knooppunten implementeren en om taken te verzenden, moet u eerst een aantal configuratiestappen vereist cluster uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a5884-173">To use HPC Cluster Manager to deploy Azure nodes and to submit jobs, first perform some required cluster configuration steps.</span></span>

1. <span data-ttu-id="a5884-174">Start op het hoofdknooppunt HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a5884-174">On the head node, start HPC Cluster Manager.</span></span> <span data-ttu-id="a5884-175">Als de **hoofdknooppunt selecteren** dialoogvenster wordt weergegeven, klikt u op **lokale Computer**.</span><span class="sxs-lookup"><span data-stu-id="a5884-175">If the **Select Head Node** dialog box appears, click **Local Computer**.</span></span> <span data-ttu-id="a5884-176">De **implementatie takenlijst** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a5884-176">The **Deployment To-do List** appears.</span></span>

2. <span data-ttu-id="a5884-177">Onder **implementatietaken vereist**, klikt u op **configureren van uw netwerk**.</span><span class="sxs-lookup"><span data-stu-id="a5884-177">Under **Required deployment tasks**, click **Configure your network**.</span></span>
   
    ![Netwerk configureren][config_hpc2]

3. <span data-ttu-id="a5884-179">Selecteer in de Wizard netwerkconfiguratie, **alle knooppunten alleen op een bedrijfsnetwerk** (topologie 5).</span><span class="sxs-lookup"><span data-stu-id="a5884-179">In the Network Configuration Wizard, select **All nodes only on an enterprise network** (Topology 5).</span></span> <span data-ttu-id="a5884-180">Deze netwerkconfiguratie is de eenvoudigste voor demonstratiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="a5884-180">This network configuration is the simplest for demonstration purposes.</span></span>
   
    ![Topologie 5][config_hpc3]
   
4. <span data-ttu-id="a5884-182">Klik op **volgende** standaardwaarden op de overige pagina's van de wizard accepteren.</span><span class="sxs-lookup"><span data-stu-id="a5884-182">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="a5884-183">Klik op de **revisie** tabblad **configureren** om de netwerkconfiguratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="a5884-183">Then, on the **Review** tab, click **Configure** to complete the network configuration.</span></span>

5. <span data-ttu-id="a5884-184">In de **implementatie takenlijst**, klikt u op **referenties van de installatie**.</span><span class="sxs-lookup"><span data-stu-id="a5884-184">In the **Deployment To-do List**, click **Provide installation credentials**.</span></span>

6. <span data-ttu-id="a5884-185">In de **Installatiereferenties** dialoogvenster typt u de referenties van het domeinaccount dat u gebruikt voor het installeren van HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a5884-185">In the **Installation Credentials** dialog box, type the credentials of the domain account that you used to install HPC Pack.</span></span> <span data-ttu-id="a5884-186">Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5884-186">Then click **OK**.</span></span> 
   
    ![Van Installatiereferenties][config_hpc6]
   
7. <span data-ttu-id="a5884-188">In de **implementatie takenlijst**, klikt u op **configureren de naamgeving van nieuwe knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="a5884-188">In the **Deployment To-do List**, click **Configure the naming of new nodes**.</span></span>

8. <span data-ttu-id="a5884-189">In de **Geef knooppunt Naming reeks** dialoogvenster vak, accepteer de standaardinstelling naamgeving van reeksen en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5884-189">In the **Specify Node Naming Series** dialog box, accept the default naming series and click **OK**.</span></span> <span data-ttu-id="a5884-190">Deze stap uitvoert, zelfs als de Azure knooppunten die u in deze zelfstudie toevoegen automatisch een naam zijn.</span><span class="sxs-lookup"><span data-stu-id="a5884-190">Complete this step even though the Azure nodes you add in this tutorial are named automatically.</span></span>
   
    ![Naamgeving van knooppunt][config_hpc8]
   
9. <span data-ttu-id="a5884-192">In de **implementatie takenlijst**, klikt u op **maken van een knooppuntsjabloon**.</span><span class="sxs-lookup"><span data-stu-id="a5884-192">In the **Deployment To-do List**, click **Create a node template**.</span></span> <span data-ttu-id="a5884-193">Verderop in de zelfstudie kunt u de knooppuntsjabloon Azure knooppunten toevoegen aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="a5884-193">Later in the tutorial, you use the node template to add Azure nodes to the cluster.</span></span>

10. <span data-ttu-id="a5884-194">Ga als volgt te werk in de Wizard knooppunt sjabloon maken:</span><span class="sxs-lookup"><span data-stu-id="a5884-194">In the Create Node Template Wizard, do the following:</span></span>
    
    <span data-ttu-id="a5884-195">a.</span><span class="sxs-lookup"><span data-stu-id="a5884-195">a.</span></span> <span data-ttu-id="a5884-196">Op de **knooppunttype sjabloon kiezen** pagina, klikt u op **Windows Azure-knooppuntsjabloon**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-196">On the **Choose Node Template Type** page, click **Windows Azure node template**, and then click **Next**.</span></span>
    
    ![Knooppuntsjabloon][config_hpc10]
    
    <span data-ttu-id="a5884-198">b.</span><span class="sxs-lookup"><span data-stu-id="a5884-198">b.</span></span> <span data-ttu-id="a5884-199">Klik op **volgende** naar accepteer de standaardnaam van de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="a5884-199">Click **Next** to accept the default template name.</span></span>
    
    <span data-ttu-id="a5884-200">c.</span><span class="sxs-lookup"><span data-stu-id="a5884-200">c.</span></span> <span data-ttu-id="a5884-201">Op de **abonnementsgegevens bieden** pagina, Voer uw Azure-abonnement-ID (beschikbaar in uw Azure-account-informatie).</span><span class="sxs-lookup"><span data-stu-id="a5884-201">On the **Provide Subscription Information** page, enter your Azure subscription ID (available in your Azure account information).</span></span> <span data-ttu-id="a5884-202">Klik op **beheercertificaat**, zoeken naar **Microsoft HPC Azure Management Default.**</span><span class="sxs-lookup"><span data-stu-id="a5884-202">Then, in **Management certificate**, browse for **Default Microsoft HPC Azure Management.**</span></span> <span data-ttu-id="a5884-203">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-203">Then click **Next**.</span></span>
    
    ![Knooppuntsjabloon][config_hpc12]
    
    <span data-ttu-id="a5884-205">d.</span><span class="sxs-lookup"><span data-stu-id="a5884-205">d.</span></span> <span data-ttu-id="a5884-206">Op de **servicegegevens bieden** pagina, selecteert u de cloudservice en het opslagaccount dat u in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a5884-206">On the **Provide Service Information** page, select the cloud service and the storage account that you created in a previous step.</span></span> <span data-ttu-id="a5884-207">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-207">Then click **Next**.</span></span>
    
    ![Knooppuntsjabloon][config_hpc13]
    
    <span data-ttu-id="a5884-209">e.</span><span class="sxs-lookup"><span data-stu-id="a5884-209">e.</span></span> <span data-ttu-id="a5884-210">Klik op **volgende** standaardwaarden op de overige pagina's van de wizard accepteren.</span><span class="sxs-lookup"><span data-stu-id="a5884-210">Click **Next** to accept default values on the remaining pages of the wizard.</span></span> <span data-ttu-id="a5884-211">Klik op de **revisie** tabblad **maken** de knooppuntsjabloon wilt maken.</span><span class="sxs-lookup"><span data-stu-id="a5884-211">Then, on the **Review** tab, click **Create** to create the node template.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="a5884-212">Standaard bevat de knooppuntsjabloon Azure instellingen voor u (ingericht) starten en stoppen van de knooppunten handmatig met behulp van HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a5884-212">By default, the Azure node template includes settings for you to start (provision) and stop the nodes manually, using HPC Cluster Manager.</span></span> <span data-ttu-id="a5884-213">U kunt desgewenst een schema te starten en stoppen van de Azure knooppunten automatisch configureren.</span><span class="sxs-lookup"><span data-stu-id="a5884-213">You can optionally configure a schedule to start and stop the Azure nodes automatically.</span></span>
    > 
    > 

## <a name="add-azure-nodes-to-the-cluster"></a><span data-ttu-id="a5884-214">Azure knooppunten toevoegen aan het cluster</span><span class="sxs-lookup"><span data-stu-id="a5884-214">Add Azure nodes to the cluster</span></span>
<span data-ttu-id="a5884-215">Nu de knooppuntsjabloon gebruiken Azure knooppunten toevoegen aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="a5884-215">Now use the node template to add Azure nodes to the cluster.</span></span> <span data-ttu-id="a5884-216">De knooppunten toevoegen aan het cluster hun configuratiegegevens worden opgeslagen zodat u starten kunt (ingericht) ze op elk gewenst moment in de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a5884-216">Adding the nodes to the cluster stores their configuration information so that you can start (provision) them at any time in the cloud service.</span></span> <span data-ttu-id="a5884-217">Uw abonnement alleen opgehaald in rekening gebracht voor Azure knooppunten nadat de exemplaren worden uitgevoerd in de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="a5884-217">Your subscription only gets charged for Azure nodes after the instances are running in the cloud service.</span></span>

<span data-ttu-id="a5884-218">Volg deze stappen als u twee kleine knooppunten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a5884-218">Follow these steps to add two Small nodes.</span></span>

1. <span data-ttu-id="a5884-219">In HPC Cluster Manager, klikt u op **knooppunt Management** (aangeroepen **bronbeheer** in huidige versies van HPC Pack) > **knooppunt toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="a5884-219">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack) > **Add Node**.</span></span>
   
    ![Knooppunt toevoegen][add_node1]

2. <span data-ttu-id="a5884-221">In de Wizard knooppunt toevoegen op de **implementatiemethode selecteren** pagina, klikt u op **toevoegen Windows Azure knooppunten**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-221">In the Add Node Wizard, on the **Select Deployment Method** page, click **Add Windows Azure nodes**, and then click **Next**.</span></span>
   
    ![Azure knooppunt toevoegen][add_node1_1]

3. <span data-ttu-id="a5884-223">Op de **nieuwe knooppunten opgeven** pagina, selecteer de knooppuntsjabloon die u eerder hebt gemaakt voor het Azure-(standaard genoemd **AzureNode standaardsjabloon**).</span><span class="sxs-lookup"><span data-stu-id="a5884-223">On the **Specify New Nodes** page, select the Azure node template you created previously (called by default **Default AzureNode Template**).</span></span> <span data-ttu-id="a5884-224">Geef vervolgens **2** knooppunten van de grootte van **kleine**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="a5884-224">Then specify **2** nodes of size **Small**, and then click **Next**.</span></span>
   
    ![Knooppunten opgeven][add_node2]
   
4. <span data-ttu-id="a5884-226">Op de **de wizard knooppunt toevoegen** pagina, klikt u op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="a5884-226">On the **Completing the Add Node Wizard** page, click **Finish**.</span></span>
    
     <span data-ttu-id="a5884-227">Twee Azure knooppunten, met de naam **AzureCN 0001** en **AzureCN 0002**, worden nu weergegeven in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a5884-227">Two Azure nodes, named **AzureCN-0001** and **AzureCN-0002**, now appear in HPC Cluster Manager.</span></span> <span data-ttu-id="a5884-228">Beide zijn de **niet geïmplementeerd** status.</span><span class="sxs-lookup"><span data-stu-id="a5884-228">Both are in the **Not-Deployed** state.</span></span>
   
    ![Toegevoegde knooppunten][add_node3]

## <a name="start-the-azure-nodes"></a><span data-ttu-id="a5884-230">Starten van de Azure knooppunten</span><span class="sxs-lookup"><span data-stu-id="a5884-230">Start the Azure nodes</span></span>
<span data-ttu-id="a5884-231">Als u de clusterbronnen in Azure gebruiken wilt, gebruikt u HPC Cluster Manager om te starten (ingericht) de Azure-knooppunten en ze online brengt.</span><span class="sxs-lookup"><span data-stu-id="a5884-231">When you want to use the cluster resources in Azure, use HPC Cluster Manager to start (provision) the Azure nodes and bring them online.</span></span>

1. <span data-ttu-id="a5884-232">In HPC Cluster Manager, klikt u op **knooppunt Management** (aangeroepen **bronbeheer** in huidige versies van HPC Pack), en selecteer de Azure knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a5884-232">In HPC Cluster Manager, click **Node Management** (called **Resource Management** in current versions of HPC Pack), and select the Azure nodes.</span></span>

2. <span data-ttu-id="a5884-233">Klik op **Start**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5884-233">Click **Start**, and then click **OK**.</span></span>
   
   ![Beginknooppunten][add_node4]
   
    <span data-ttu-id="a5884-235">De knooppunten worden overgezet naar de **inrichten** status.</span><span class="sxs-lookup"><span data-stu-id="a5884-235">The nodes transition to the **Provisioning** state.</span></span> <span data-ttu-id="a5884-236">Bekijk het logboek inrichting om de voortgang van de inrichting te volgen.</span><span class="sxs-lookup"><span data-stu-id="a5884-236">View the provisioning log to track the provisioning progress.</span></span>
   
    ![Inrichten knooppunten][add_node6]

3. <span data-ttu-id="a5884-238">Na een paar minuten Azure knooppunten inrichting en zich in de **Offline** status.</span><span class="sxs-lookup"><span data-stu-id="a5884-238">After a few minutes, the Azure nodes finish provisioning and are in the **Offline** state.</span></span> <span data-ttu-id="a5884-239">In deze toestand is, is de rolexemplaren worden uitgevoerd, maar taken cluster nog niet accepteren.</span><span class="sxs-lookup"><span data-stu-id="a5884-239">In this state, the role instances are running but cannot yet accept cluster jobs.</span></span>

4. <span data-ttu-id="a5884-240">Klik om te bevestigen dat de rolexemplaren worden uitgevoerd, klikt u in de Azure portal **Cloudservices (klassiek)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="a5884-240">To confirm that the role instances are running, in the Azure portal, click **Cloud Services (classic)** > *your_cloud_service_name*.</span></span>
   
   <span data-ttu-id="a5884-241">U ziet twee **HpcWorkerRole** exemplaren (knooppunten) uitgevoerd in de service.</span><span class="sxs-lookup"><span data-stu-id="a5884-241">You should see two **HpcWorkerRole** instances (nodes) running in the service.</span></span> <span data-ttu-id="a5884-242">HPC Pack implementeert ook automatisch twee **HpcProxy** exemplaren (grootte normaal) voor het afhandelen van communicatie tussen het hoofdknooppunt en Azure.</span><span class="sxs-lookup"><span data-stu-id="a5884-242">HPC Pack also automatically deploys two **HpcProxy** instances (size Medium) to handle communication between the head node and Azure.</span></span>

   ![Exemplaren die worden uitgevoerd][view_instances1]

5. <span data-ttu-id="a5884-244">Voor het maken van de Azure knooppunten online cluster taken uitvoeren, selecteert u de knooppunten, klik met de rechtermuisknop en klik vervolgens op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="a5884-244">To bring the Azure nodes online to run cluster jobs, select the nodes, right-click, and then click **Bring Online**.</span></span>
   
    ![Offline knooppunten][add_node7]
   
    <span data-ttu-id="a5884-246">HPC Cluster Manager geeft aan dat de knooppunten de **Online** status.</span><span class="sxs-lookup"><span data-stu-id="a5884-246">HPC Cluster Manager indicates that the nodes are in the **Online** state.</span></span>

## <a name="run-a-command-across-the-cluster"></a><span data-ttu-id="a5884-247">Een opdracht in het cluster wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="a5884-247">Run a command across the cluster</span></span>
<span data-ttu-id="a5884-248">Gebruiken om te controleren van de installatie, het HPC Pack **clusrun** opdracht voor het uitvoeren van een opdracht of een toepassing op een of meer clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="a5884-248">To check the installation, use the HPC Pack **clusrun** command to run a command or application on one or more cluster nodes.</span></span> <span data-ttu-id="a5884-249">Als een eenvoudig voorbeeld gebruiken **clusrun** ophalen van de IP-adresconfiguratie van de Azure knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a5884-249">As a simple example, use **clusrun** to get the IP configuration of the Azure nodes.</span></span>

1. <span data-ttu-id="a5884-250">Open een opdrachtprompt als beheerder op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a5884-250">On the head node, open a command prompt as an administrator.</span></span>

2. <span data-ttu-id="a5884-251">Typ de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a5884-251">Type the following command:</span></span>
   
    `clusrun /nodes:azurecn* ipconfig`

3. <span data-ttu-id="a5884-252">Als u wordt gevraagd, voert u het wachtwoord van de cluster.</span><span class="sxs-lookup"><span data-stu-id="a5884-252">If prompted, enter your cluster administrator password.</span></span> <span data-ttu-id="a5884-253">U ziet de uitvoer van de opdracht ziet er als volgt.</span><span class="sxs-lookup"><span data-stu-id="a5884-253">You should see command output similar to the following.</span></span>
   
    ![Clusrun][clusrun1]

## <a name="run-a-test-job"></a><span data-ttu-id="a5884-255">Voer een test</span><span class="sxs-lookup"><span data-stu-id="a5884-255">Run a test job</span></span>
<span data-ttu-id="a5884-256">Nu verzenden van een testtaak die wordt uitgevoerd op de hybride-cluster.</span><span class="sxs-lookup"><span data-stu-id="a5884-256">Now submit a test job that runs on the hybrid cluster.</span></span> <span data-ttu-id="a5884-257">In dit voorbeeld is een eenvoudige parametrische taak (een soort intrinsiek parallelle berekeningen).</span><span class="sxs-lookup"><span data-stu-id="a5884-257">This example is a simple parametric sweep job (a type of intrinsically parallel computation).</span></span> <span data-ttu-id="a5884-258">In dit voorbeeld wordt uitgevoerd subtaken die een geheel getal aan zichzelf met behulp van toevoegen de **/a ingesteld** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a5884-258">This example runs subtasks that add an integer to itself by using the **set /a** command.</span></span> <span data-ttu-id="a5884-259">Alle knooppunten in het cluster bijdragen aan de subtaken voor gehele getallen van 1 tot 100 is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a5884-259">All the nodes in the cluster contribute to finishing the subtasks for integers from 1 to 100.</span></span>

1. <span data-ttu-id="a5884-260">Klik in HPC Cluster Manager op **Jobbeheer** > **nieuwe parametrische Sweep taak**.</span><span class="sxs-lookup"><span data-stu-id="a5884-260">In HPC Cluster Manager, click **Job Management** > **New Parametric Sweep Job**.</span></span>
   
    ![Nieuwe taak][test_job1]

2. <span data-ttu-id="a5884-262">In de **nieuwe parametrische Sweep taak** het dialoogvenster **opdrachtregel**, type `set /a *+*` (overschrijven de standaard-opdrachtregel die wordt weergegeven).</span><span class="sxs-lookup"><span data-stu-id="a5884-262">In the **New Parametric Sweep Job** dialog box, in **Command line**, type `set /a *+*` (overwriting the default command line that appears).</span></span> <span data-ttu-id="a5884-263">Laat de standaardwaarden voor de overige instellingen en klik vervolgens op **indienen** voor het verzenden van de taak.</span><span class="sxs-lookup"><span data-stu-id="a5884-263">Leave default values for the remaining settings, and then click **Submit** to submit the job.</span></span>
   
    ![Parametrische opschoning][param_sweep1]

3. <span data-ttu-id="a5884-265">Wanneer de taak is voltooid, dubbelklikt u op de **mijn Sweep taak** taak.</span><span class="sxs-lookup"><span data-stu-id="a5884-265">When the job is finished, double-click the **My Sweep Task** job.</span></span>

4. <span data-ttu-id="a5884-266">Klik op **taken weergeven**, en klik vervolgens op een subtaak om de berekende uitvoer van deze subtaak weer te geven.</span><span class="sxs-lookup"><span data-stu-id="a5884-266">Click **View Tasks**, and then click a subtask to view the calculated output of that subtask.</span></span>
   
    ![Resultaten van de taak][view_job361]

5. <span data-ttu-id="a5884-268">Als u wilt zien welk knooppunt de berekening uitgevoerd voor deze subtaak, klikt u op **toegewezen knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="a5884-268">To see which node performed the calculation for that subtask, click **Allocated Nodes**.</span></span> <span data-ttu-id="a5884-269">(U mogelijk de naam van een ander knooppunt weergegeven voor uw cluster.)</span><span class="sxs-lookup"><span data-stu-id="a5884-269">(Your cluster might show a different node name.)</span></span>
   
    ![Resultaten van de taak][view_job362]

## <a name="stop-the-azure-nodes"></a><span data-ttu-id="a5884-271">De Azure knooppunten stoppen</span><span class="sxs-lookup"><span data-stu-id="a5884-271">Stop the Azure nodes</span></span>
<span data-ttu-id="a5884-272">Nadat u het cluster uitproberen, stopt u de Azure knooppunten om te voorkomen dat onnodige kosten voor je account.</span><span class="sxs-lookup"><span data-stu-id="a5884-272">After you try out the cluster, stop the Azure nodes to avoid unnecessary charges to your account.</span></span> <span data-ttu-id="a5884-273">Deze stap de cloudservice stopt en verwijdert u de Azure-rolexemplaren.</span><span class="sxs-lookup"><span data-stu-id="a5884-273">This step stops the cloud service and removes the Azure role instances.</span></span>

1. <span data-ttu-id="a5884-274">In HPC Cluster Manager in **knooppunt Management** (aangeroepen **bronbeheer** in eerdere versies van HPC Pack), selecteert u beide Azure knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a5884-274">In HPC Cluster Manager, in **Node Management** (called **Resource Management** in previous versions of HPC Pack), select both Azure nodes.</span></span> <span data-ttu-id="a5884-275">Klik vervolgens op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="a5884-275">Then, click **Stop**.</span></span>
   
    ![Knooppunten stoppen][stop_node1]

2. <span data-ttu-id="a5884-277">In de **stoppen Windows Azure knooppunten** in het dialoogvenster, klikt u op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="a5884-277">In the **Stop Windows Azure nodes** dialog box, click **Stop**.</span></span> 
   
3. <span data-ttu-id="a5884-278">De knooppunten worden overgezet naar de **stoppen** status.</span><span class="sxs-lookup"><span data-stu-id="a5884-278">The nodes transition to the **Stopping** state.</span></span> <span data-ttu-id="a5884-279">Na een paar minuten HPC Cluster Manager geeft aan dat de knooppunten **niet geïmplementeerd**.</span><span class="sxs-lookup"><span data-stu-id="a5884-279">After a few minutes, HPC Cluster Manager shows that the nodes are **Not-Deployed**.</span></span>
   
    ![Niet-geïmplementeerde knooppunten][stop_node4]

4. <span data-ttu-id="a5884-281">Om te bevestigen dat de rolinstanties niet langer zijn uitgevoerd in Azure, in de Azure-portal klikt u op **Cloudservices (klassiek)** > *your_cloud_service_name*.</span><span class="sxs-lookup"><span data-stu-id="a5884-281">To confirm that the role instances are no longer running in Azure, in the Azure portal, click **Cloud services (classic)** > *your_cloud_service_name*.</span></span> <span data-ttu-id="a5884-282">Er zijn geen exemplaren worden geïmplementeerd in de productieomgeving.</span><span class="sxs-lookup"><span data-stu-id="a5884-282">No instances are deployed in the production environment.</span></span> 
   
    <span data-ttu-id="a5884-283">Deze zelfstudie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a5884-283">This completes the tutorial.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5884-284">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5884-284">Next steps</span></span>
* <span data-ttu-id="a5884-285">Bekijk de documentatie voor [HPC Pack](https://technet.microsoft.com/library/cc514029).</span><span class="sxs-lookup"><span data-stu-id="a5884-285">Explore the documentation for [HPC Pack](https://technet.microsoft.com/library/cc514029).</span></span>
* <span data-ttu-id="a5884-286">Als u een hybride implementatie van het cluster op schaal groter HPC Pack instelt, Zie [Burst naar Azure Worker-Rolexemplaren met Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span><span class="sxs-lookup"><span data-stu-id="a5884-286">To set up a hybrid HPC Pack cluster deployment at greater scale, see [Burst to Azure Worker Role Instances with Microsoft HPC Pack](http://go.microsoft.com/fwlink/p/?LinkID=200493).</span></span>
* <span data-ttu-id="a5884-287">Voor andere manieren om te maken van een HPC Pack-cluster in Azure, met inbegrip van Azure Resource Manager-sjablonen, Zie [opties voor HPC-cluster met Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a5884-287">For other ways to create an HPC Pack cluster in Azure, including using Azure Resource Manager templates, see [HPC cluster options with Microsoft HPC Pack in Azure](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


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

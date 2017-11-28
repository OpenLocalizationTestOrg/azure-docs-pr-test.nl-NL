---
title: OpenFOAM HPC Pack uitvoeren op virtuele Linux-machines | Microsoft Docs
description: Een Microsoft HPC Pack cluster in Azure implementeren en uitvoeren van een taak OpenFOAM op meerdere rekenknooppunten van Linux via een netwerk RDMA.
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: c0bb1637-bb19-48f1-adaa-491808d3441f
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 07/22/2016
ms.author: danlep
ms.openlocfilehash: ef124a8983fa112d499252460bff9ed2fcccc02b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="3af23-103">OpenFoam uitvoeren met Microsoft HPC Pack op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="3af23-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="3af23-104">In dit artikel laat zien hoe OpenFoam uitvoeren in virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="3af23-104">This article shows you one way to run OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="3af23-105">Hier kunt u een cluster met Microsoft HPC Pack met Linux-rekenknooppunten in Azure en voer implementeert een [OpenFoam](http://openfoam.com/) taak met de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="3af23-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="3af23-106">Zodat de rekenknooppunten via het netwerk van Azure RDMA communiceren, kunt u RDMA-compatibele Azure VM's voor de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-106">You can use RDMA-capable Azure VMs for the compute nodes, so that the compute nodes communicate over the Azure RDMA network.</span></span> <span data-ttu-id="3af23-107">Andere opties OpenFoam uitvoeren in Azure, volledig geconfigureerde commerciële installatiekopieën beschikbaar zijn in de Marketplace, zoals de UberCloud [OpenFoam 2.3 op CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), en door te voeren op [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="3af23-107">Other options to run OpenFoam in Azure include fully configured commercial images available in the Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="3af23-108">OpenFOAM (voor veld bewerking openen en bewerken) is een open source computational fluid dynamics (CFD)-softwarepakket dat algemeen wordt gebruikt in de technische en wetenschappelijke in commerciële en academic organisaties.</span><span class="sxs-lookup"><span data-stu-id="3af23-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="3af23-109">Dit omvat de hulpprogramma's voor meshing, met name snappyHexMesh, een parallelized mesher voor complexe CAD-geometrie en voor vóór en na verwerking.</span><span class="sxs-lookup"><span data-stu-id="3af23-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="3af23-110">Bijna alle processen parallel uitgevoerd, zodat gebruikers kunnen profiteren van de computerhardware beschikken.</span><span class="sxs-lookup"><span data-stu-id="3af23-110">Almost all processes run in parallel, enabling users to take full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="3af23-111">Microsoft HPC Pack beschikt over functies voor het uitvoeren van grootschalige HPC en parallelle toepassingen, waaronder MPI-toepassingen op clusters van Microsoft Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="3af23-111">Microsoft HPC Pack provides features to run large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="3af23-112">HPC Pack ondersteunt ook actief Linux HPC-toepassingen op Linux VM's geïmplementeerd in een cluster HPC Pack rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="3af23-113">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor een inleiding tot het gebruik van Linux rekenknooppunten HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="3af23-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction to using Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="3af23-114">In dit artikel laat zien hoe een Linux MPI-werkbelasting met HPC Pack uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-114">This article illustrates how to run a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="3af23-115">Wordt ervan uitgegaan dat u enigszins bekend bent met Linux Systeembeheer en MPI belastingen uitgevoerd op Linux-clusters hebben.</span><span class="sxs-lookup"><span data-stu-id="3af23-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="3af23-116">Als u versies van MPI en OpenFOAM afwijken van de namen weergegeven in dit artikel gebruikt, moet u wellicht een aantal stappen installatie en configuratie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3af23-116">If you use versions of MPI and OpenFOAM different from the ones shown in this article, you might have to modify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="3af23-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3af23-117">Prerequisites</span></span>
* <span data-ttu-id="3af23-118">**HPC Pack cluster met RDMA-compatibele Linux-rekenknooppunten** : een cluster HPC Pack met een grootte A8, A9, H16r, implementeren of H16rm Linux-rekenknooppunten met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) of een [Azure PowerShell-script](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="3af23-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="3af23-119">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor de vereisten en stappen voor beide opties.</span><span class="sxs-lookup"><span data-stu-id="3af23-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for the prerequisites and steps for either option.</span></span> <span data-ttu-id="3af23-120">Als u de PowerShell-script-implementatie-optie kiest, raadpleegt u het voorbeeldconfiguratiebestand in de voorbeeldbestanden aan het einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3af23-120">If you choose the PowerShell script deployment option, see the sample configuration file in the sample files at the end of this article.</span></span> <span data-ttu-id="3af23-121">Deze configuratie gebruiken voor het implementeren van een HPC Pack op basis van een Azure-cluster die bestaan uit een grootte A8 Windows Server 2012 R2-hoofdknooppunt en 2 grootte A8 SUSE Linux Enterprise Server 12-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-121">Use this configuration to deploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="3af23-122">Vervang de juiste waarden voor uw abonnement en de service namen.</span><span class="sxs-lookup"><span data-stu-id="3af23-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="3af23-123">**Aanvullende zaken die u moet weten**</span><span class="sxs-lookup"><span data-stu-id="3af23-123">**Additional things to know**</span></span>
  
  * <span data-ttu-id="3af23-124">Zie voor Linux RDMA netwerken vereisten in Azure, [hoge prestaties compute-VM-grootten](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="3af23-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="3af23-125">Als u de optie voor de Powershell-script gebruikt, implementeert u alle Linux-rekenknooppunten in een cloudservice te gebruiken van de RDMA-netwerkverbinding.</span><span class="sxs-lookup"><span data-stu-id="3af23-125">If you use the Powershell script deployment option, deploy all the Linux compute nodes within one cloud service to use the RDMA network connection.</span></span>
  * <span data-ttu-id="3af23-126">Na implementatie van de Linux-knooppunten, verbinding maken via SSH eventuele extra beheertaken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-126">After deploying the Linux nodes, connect by SSH to perform any additional administrative tasks.</span></span> <span data-ttu-id="3af23-127">De details van de SSH-verbinding voor elke Linux-VM niet vinden in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3af23-127">Find the SSH connection details for each Linux VM in the Azure portal.</span></span>  
* <span data-ttu-id="3af23-128">**Intel MPI** - OpenFOAM uitvoeren op SLES 12 HPC-rekenknooppunten in Azure, moet u voor het installeren van de runtime Intel MPI-bibliotheek 5 van de [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="3af23-128">**Intel MPI** - To run OpenFOAM on SLES 12 HPC compute nodes in Azure, you need to install the Intel MPI Library 5 runtime from the [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="3af23-129">(Intel MPI 5 is voorgeïnstalleerd op op basis van CentOS HPC-installatiekopieën.)  Installeer Intel MPI op uw Linux-rekenknooppunten in een latere stap, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="3af23-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="3af23-130">Om voor te bereiden voor deze stap nadat u hebt geregistreerd met Intel, volgt u de koppeling in het bevestigingsbericht naar de gerelateerde webpagina.</span><span class="sxs-lookup"><span data-stu-id="3af23-130">To prepare for this step, after you register with Intel, follow the link in the confirmation email to the related web page.</span></span> <span data-ttu-id="3af23-131">Kopieer vervolgens de downloadkoppeling voor het bestand .tgz voor de juiste versie van Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="3af23-131">Then, copy the download link for the .tgz file for the appropriate version of Intel MPI.</span></span> <span data-ttu-id="3af23-132">In dit artikel is gebaseerd op Intel MPI versie 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="3af23-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="3af23-133">**OpenFOAM bron Pack** -Download de OpenFOAM bron Pack-software voor Linux van de [OpenFOAM Foundation-site](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="3af23-133">**OpenFOAM Source Pack** - Download the OpenFOAM Source Pack software for Linux from the [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="3af23-134">In dit artikel is gebaseerd op de bron-packversie 2.3.1-specificaties gedownload als OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="3af23-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="3af23-135">Volg de instructies verderop in dit artikel om te pakken en compileren OpenFOAM op de Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-135">Follow the instructions later in this article to unpack and compile OpenFOAM on the Linux compute nodes.</span></span>
* <span data-ttu-id="3af23-136">**EnSight** (optioneel): de resultaten van uw OpenFOAM simulatie, downloadt en installeert de [EnSight](https://www.ceisoftware.com/download/) visualisatie en analyse-programma.</span><span class="sxs-lookup"><span data-stu-id="3af23-136">**EnSight** (optional) - To see the results of your OpenFOAM simulation, download and install the [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="3af23-137">Licentie-en download zijn op de site EnSight.</span><span class="sxs-lookup"><span data-stu-id="3af23-137">Licensing and download information are at the EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="3af23-138">Wederzijdse vertrouwensrelatie tussen de rekenknooppunten instellen</span><span class="sxs-lookup"><span data-stu-id="3af23-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="3af23-139">Een taak cross-knooppunt wordt uitgevoerd op meerdere Linux-knooppunten vereist dat de knooppunten die elkaar vertrouwen (door **rsh** of **ssh**).</span><span class="sxs-lookup"><span data-stu-id="3af23-139">Running a cross-node job on multiple Linux nodes requires the nodes to trust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="3af23-140">Wanneer u het cluster HPC Pack met het script voor Microsoft HPC Pack IaaS-implementatie maakt, het script permanente wederzijds vertrouwen voor de administrator-account dat u opgeeft automatisch ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3af23-140">When you create the HPC Pack cluster with the Microsoft HPC Pack IaaS deployment script, the script automatically sets up permanent mutual trust for the administrator account you specify.</span></span> <span data-ttu-id="3af23-141">Voor gebruikers die geen beheerder u in domein van het cluster maakt, hebben om in te stellen van tijdelijke wederzijds vertrouwen tussen de knooppunten wanneer een taak wordt toegewezen aan hen en de relatie vernietigen nadat de taak voltooid is.</span><span class="sxs-lookup"><span data-stu-id="3af23-141">For non-administrator users you create in the cluster's domain, you have to set up temporary mutual trust among the nodes when a job is allocated to them, and destroy the relationship after the job is complete.</span></span> <span data-ttu-id="3af23-142">Als u wilt een vertrouwensrelatie voor elke gebruiker, bieden een RSA-sleutelpaar naar het cluster dat HPC Pack voor de vertrouwensrelatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3af23-142">To establish trust for each user, provide an RSA key pair to the cluster that HPC Pack uses for the trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="3af23-143">Een RSA-sleutelpaar niet genereren</span><span class="sxs-lookup"><span data-stu-id="3af23-143">Generate an RSA key pair</span></span>
<span data-ttu-id="3af23-144">Het is gemakkelijk voor het genereren van een RSA-sleutelpaar, die een openbare sleutel en een persoonlijke sleutel bevat door het uitvoeren van de Linux **ssh-keygen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="3af23-144">It's easy to generate an RSA key pair, which contains a public key and a private key, by running the Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="3af23-145">Meld u op een Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="3af23-145">Log on to a Linux computer.</span></span>
2. <span data-ttu-id="3af23-146">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="3af23-146">Run the following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="3af23-147">Druk op **Enter** de standaardinstellingen gebruiken totdat de opdracht is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3af23-147">Press **Enter** to use the default settings until the command is completed.</span></span> <span data-ttu-id="3af23-148">Voer een wachtwoordzin hier; niet Wanneer u daarom wordt gevraagd om een wachtwoord op te geven, drukt u op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3af23-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Een RSA-sleutelpaar niet genereren][keygen]
3. <span data-ttu-id="3af23-150">Map naar de map ~/.ssh wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3af23-150">Change directory to the ~/.ssh directory.</span></span> <span data-ttu-id="3af23-151">De persoonlijke sleutel wordt opgeslagen in id_rsa en de openbare sleutel in id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="3af23-151">The private key is stored in id_rsa and the public key in id_rsa.pub.</span></span>
   
   ![Persoonlijke en openbare sleutel][keys]

### <a name="add-the-key-pair-to-the-hpc-pack-cluster"></a><span data-ttu-id="3af23-153">Het sleutelpaar aan het cluster HPC Pack toevoegen</span><span class="sxs-lookup"><span data-stu-id="3af23-153">Add the key pair to the HPC Pack cluster</span></span>
1. <span data-ttu-id="3af23-154">Extern bureaublad verbinding maken met uw hoofdknooppunt met uw beheerdersaccount HPC Pack (het administrator-account u instellen wanneer u het script voor implementatie is uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="3af23-154">Make a Remote Desktop connection to your head node with your HPC Pack administrator account (the administrator account you set up when you ran the deployment script).</span></span>
2. <span data-ttu-id="3af23-155">Gebruik standaard Windows Server-procedures om een domeingebruikersaccount maken in Active Directory-domein van het cluster.</span><span class="sxs-lookup"><span data-stu-id="3af23-155">Use standard Windows Server procedures to create a domain user account in the cluster's Active Directory domain.</span></span> <span data-ttu-id="3af23-156">Bijvoorbeeld, gebruik het hulpprogramma Active Directory-gebruikers en Computers op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-156">For example, use the Active Directory User and Computers tool on the head node.</span></span> <span data-ttu-id="3af23-157">De voorbeelden in dit artikel wordt ervan uitgegaan dat u een domeingebruiker die met de naam hpclab\hpcuser maken.</span><span class="sxs-lookup"><span data-stu-id="3af23-157">The examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="3af23-158">Maak een bestand met de naam C:\cred.xml en kopieer de RSA-sleutelgegevens in de App.</span><span class="sxs-lookup"><span data-stu-id="3af23-158">Create a file named C:\cred.xml and copy the RSA key data into it.</span></span> <span data-ttu-id="3af23-159">Er is een voorbeeldbestand cred.xml aan het einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="3af23-159">A sample cred.xml file is at the end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy the contents of private key here</PrivateKey>
     <PublicKey>Copy the contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="3af23-160">Open een opdrachtprompt en voer de volgende opdracht om de gegevens van de referenties voor het account hpclab\hpcuser instellen.</span><span class="sxs-lookup"><span data-stu-id="3af23-160">Open a Command Prompt and enter the following command to set the credentials data for the hpclab\hpcuser account.</span></span> <span data-ttu-id="3af23-161">U gebruikt de **extendeddata** -parameter voor de naam van C:\cred.xml dat u hebt gemaakt voor de belangrijkste gegevens doorgeeft.</span><span class="sxs-lookup"><span data-stu-id="3af23-161">You use the **extendeddata** parameter to pass the name of C:\cred.xml file you created for the key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="3af23-162">Deze opdracht is voltooid zonder uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3af23-162">This command completes successfully without output.</span></span> <span data-ttu-id="3af23-163">Na het instellen van de referenties voor de gebruikersaccounts die u wilt uitvoeren van taken, sla het bestand cred.xml in een veilige locatie of verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="3af23-163">After setting the credentials for the user accounts you need to run jobs, store the cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="3af23-164">Als u de RSA-sleutelpaar gegenereerd op een van uw Linux-knooppunten, moet u de sleutels verwijderen nadat u klaar bent met het gebruik ervan.</span><span class="sxs-lookup"><span data-stu-id="3af23-164">If you generated the RSA key pair on one of your Linux nodes, remember to delete the keys after you finish using them.</span></span> <span data-ttu-id="3af23-165">HPC Pack vindt een bestaande id_rsa bestand of id_rsa.pub-bestand, dan wordt deze wederzijds vertrouwen niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="3af23-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3af23-166">Wordt niet aanbevolen als de Clusterbeheerder van een een Linux-taak wordt uitgevoerd op een gedeelde cluster, omdat een taak die is verzonden door een beheerder wordt uitgevoerd onder het hoofdaccount op de Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under the root account on the Linux nodes.</span></span> <span data-ttu-id="3af23-167">Een taak die is verzonden door een gebruiker die geen beheerder wordt echter uitgevoerd onder een lokale Linux-gebruikersaccount met dezelfde naam als de gebruiker van de taak.</span><span class="sxs-lookup"><span data-stu-id="3af23-167">However, a job submitted by a non-administrator user runs under a local Linux user account with the same name as the job user.</span></span> <span data-ttu-id="3af23-168">In dit geval stelt HPC Pack wederzijds vertrouwen voor deze gebruiker Linux op de knooppunten die zijn toegewezen aan de taak.</span><span class="sxs-lookup"><span data-stu-id="3af23-168">In this case, HPC Pack sets up mutual trust for this Linux user across the nodes allocated to the job.</span></span> <span data-ttu-id="3af23-169">U kunt de Linux-gebruiker handmatig op de Linux-knooppunten instellen voordat de taak wordt uitgevoerd of HPC Pack de gebruiker wordt automatisch gemaakt wanneer de taak wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="3af23-169">You can set up the Linux user manually on the Linux nodes before running the job, or HPC Pack creates the user automatically when the job is submitted.</span></span> <span data-ttu-id="3af23-170">Als HPC Pack de gebruiker maakt, verwijderd HPC Pack nadat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3af23-170">If HPC Pack creates the user, HPC Pack deletes it after the job completes.</span></span> <span data-ttu-id="3af23-171">Als u beveiligingsrisico's, verwijdert HPC Pack de sleutels na Taakvoltooiing van de.</span><span class="sxs-lookup"><span data-stu-id="3af23-171">To reduce security threats, HPC Pack removes the keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="3af23-172">Instellen van een bestandsshare voor Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="3af23-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="3af23-173">Nu ingesteld op een standaard SMB-share op een map op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-173">Now set up a standard SMB share on a folder on the head node.</span></span> <span data-ttu-id="3af23-174">Koppel de gedeelde map op de Linux-knooppunten zodat de Linux-knooppunten toegang tot toepassingsbestanden met een algemeen pad.</span><span class="sxs-lookup"><span data-stu-id="3af23-174">To allow the Linux nodes to access application files with a common path, mount the shared folder on the Linux nodes.</span></span> <span data-ttu-id="3af23-175">Als u wilt, kunt u een andere optie, zoals een Azure-bestanden share - aanbevolen voor veel scenario's- of een NFS-share voor bestandsdeling.</span><span class="sxs-lookup"><span data-stu-id="3af23-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="3af23-176">Zie het bestand delen van informatie en gedetailleerde stappen in [aan de slag met Linux-rekenknooppunten in een HPC Pack-Cluster in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3af23-176">See the file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="3af23-177">Maak een map op het hoofdknooppunt en voor iedereen delen door het instellen van machtigingen voor lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="3af23-177">Create a folder on the head node, and share it to Everyone by setting Read/Write privileges.</span></span> <span data-ttu-id="3af23-178">Bijvoorbeeld C:\OpenFOAM delen op het hoofdknooppunt als \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="3af23-178">For example, share C:\OpenFOAM on the head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="3af23-179">Hier *SUSE12RDMA HN* is de hostnaam van het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-179">Here, *SUSE12RDMA-HN* is the host name of the head node.</span></span>
2. <span data-ttu-id="3af23-180">Open een Windows PowerShell-venster en voer de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3af23-180">Open a Windows PowerShell window and run the following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="3af23-181">De eerste opdracht maakt een map met de naam /openfoam op alle knooppunten in de groep LinuxNodes.</span><span class="sxs-lookup"><span data-stu-id="3af23-181">The first command creates a folder named /openfoam on all nodes in the LinuxNodes group.</span></span> <span data-ttu-id="3af23-182">De tweede opdracht koppelt de //SUSE12RDMA-HN/OpenFOAM gedeelde map op de Linux-knooppunten met dir_mode en file_mode bits ingesteld op 777.</span><span class="sxs-lookup"><span data-stu-id="3af23-182">The second command mounts the shared folder //SUSE12RDMA-HN/OpenFOAM on the Linux nodes with dir_mode and file_mode bits set to 777.</span></span> <span data-ttu-id="3af23-183">De *gebruikersnaam* en *wachtwoord* in de opdracht moet de referenties van een gebruiker op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-183">The *username* and *password* in the command should be the credentials of a user on the head node.</span></span>

> [!NOTE]
> <span data-ttu-id="3af23-184">De '\\`' symbool in de tweede opdracht is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3af23-184">The “\\`” symbol in the second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="3af23-185">"\\`, ' betekent dat de","(kommateken) maakt deel uit van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3af23-185">“\\`,” means the “,” (comma character) is a part of the command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="3af23-186">MPI en OpenFOAM installeren</span><span class="sxs-lookup"><span data-stu-id="3af23-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="3af23-187">OpenFOAM als een MPI-taak op het netwerk RDMA, hebt u nodig voor het compileren van OpenFOAM met de Intel MPI-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="3af23-187">To run OpenFOAM as an MPI job on the RDMA network, you need to compile OpenFOAM with the Intel MPI libraries.</span></span> 

<span data-ttu-id="3af23-188">Voer eerst enkele **clusrun** opdrachten voor het installeren van Intel MPI-bibliotheken (indien nog niet is geïnstalleerd) en OpenFOAM op uw Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-188">First, run several **clusrun** commands to install Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="3af23-189">Het hoofdknooppunt share eerder geconfigureerd voor het delen van de van installatiebestanden tussen de Linux-knooppunten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3af23-189">Use the head node share configured previously to share the installation files among the Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3af23-190">Deze installatie en gecompileerd stappen zijn voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3af23-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="3af23-191">Moet u enige kennis van de Linux-systeembeheertaken om ervoor te zorgen dat afhankelijke compilers en bibliotheken correct zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3af23-191">You need some knowledge of Linux system administration to ensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="3af23-192">Mogelijk moet u bepaalde omgevingsvariabelen of andere instellingen voor uw versie van Intel MPI en OpenFOAM wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3af23-192">You might need to modify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="3af23-193">Zie voor meer informatie [Intel MPI-bibliotheek voor Linux-installatiehandleiding](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) en [OpenFOAM bron Pack installatie](http://openfoam.org/download/2-3-1-source/) voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="3af23-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="3af23-194">Intel MPI installeren</span><span class="sxs-lookup"><span data-stu-id="3af23-194">Install Intel MPI</span></span>
<span data-ttu-id="3af23-195">Sla het installatiepakket voor de gedownloade voor Intel MPI (l_mpi_p_5.0.3.048.tgz in dit voorbeeld) in C:\OpenFoam hoofdknooppunt van het zodat de Linux-knooppunten toegang dit bestand uit /openfoam tot.</span><span class="sxs-lookup"><span data-stu-id="3af23-195">Save the downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="3af23-196">Voer **clusrun** Intel MPI-bibliotheek te installeren op alle Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-196">Then run **clusrun** to install Intel MPI library on all the Linux nodes.</span></span>

1. <span data-ttu-id="3af23-197">De volgende opdrachten Kopieer het installatiepakket en pak het /opt/intel op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-197">The following commands copy the installation package and extract it to /opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="3af23-198">U kunt Intel MPI-bibliotheek achtergrond installeren met een silent.cfg-bestand.</span><span class="sxs-lookup"><span data-stu-id="3af23-198">To install Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="3af23-199">In de voorbeeldbestanden aan het einde van dit artikel vindt u een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3af23-199">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="3af23-200">Dit bestand in de gedeelde map /openfoam plaatsen.</span><span class="sxs-lookup"><span data-stu-id="3af23-200">Place this file in the shared folder /openfoam.</span></span> <span data-ttu-id="3af23-201">Zie voor meer informatie over het bestand silent.cfg [Intel MPI-bibliotheek voor de installatiehandleiding voor Linux - installatie op de achtergrond](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="3af23-201">For details about the silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="3af23-202">Zorg ervoor dat u uw silent.cfg bestand opslaan als een tekstbestand met Linux regeleinden heb (alleen LF, niet CR LF).</span><span class="sxs-lookup"><span data-stu-id="3af23-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="3af23-203">Deze stap zorgt ervoor dat deze goed op de Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-203">This step ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="3af23-204">Intel MPI-bibliotheek in stille modus installeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="3af23-205">MPI configureren</span><span class="sxs-lookup"><span data-stu-id="3af23-205">Configure MPI</span></span>
<span data-ttu-id="3af23-206">Voor het testen, moet u de volgende regels toevoegen aan de /etc/security/limits.conf op elk van de Linux-knooppunten:</span><span class="sxs-lookup"><span data-stu-id="3af23-206">For testing, you should add the following lines to the /etc/security/limits.conf on each of the Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="3af23-207">Na het bijwerken van het bestand limits.conf, start opnieuw op de Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-207">Restart the Linux nodes after you update the limits.conf file.</span></span> <span data-ttu-id="3af23-208">Bijvoorbeeld, gebruikt u de volgende **clusrun** opdracht:</span><span class="sxs-lookup"><span data-stu-id="3af23-208">For example, use the following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="3af23-209">Start opnieuw op en controleer of de gedeelde map is gekoppeld als /openfoam.</span><span class="sxs-lookup"><span data-stu-id="3af23-209">After restarting, ensure that the shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="3af23-210">Compileren en OpenFOAM installeren</span><span class="sxs-lookup"><span data-stu-id="3af23-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="3af23-211">Het installatiepakket voor de gedownloade voor OpenFOAM bron Pack (OpenFOAM-2.3.1.tgz in dit voorbeeld) naar C:\OpenFoam opslaan op het hoofdknooppunt zodat de Linux-knooppunten toegang dit bestand uit /openfoam tot.</span><span class="sxs-lookup"><span data-stu-id="3af23-211">Save the downloaded installation package for the OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) to C:\OpenFoam on the head node so that the Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="3af23-212">Voer **clusrun** opdrachten voor het compileren van OpenFOAM op alle Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-212">Then run **clusrun** commands to compile OpenFOAM on all the Linux nodes.</span></span>

1. <span data-ttu-id="3af23-213">Een map /opt/OpenFOAM op elk knooppunt Linux maken, de bronpakket kopiëren naar deze map en er extraheren.</span><span class="sxs-lookup"><span data-stu-id="3af23-213">Create a folder /opt/OpenFOAM on each Linux node, copy the source package to this folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="3af23-214">Voor het compileren van OpenFOAM met de Intel MPI-bibliotheek eerst enkele omgevingsvariabelen instellen voor Intel MPI- en OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="3af23-214">To compile OpenFOAM with the Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="3af23-215">Een bash-script settings.sh aangeroepen om in te stellen van de variabelen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3af23-215">Use a bash script called settings.sh to set the variables.</span></span> <span data-ttu-id="3af23-216">In de voorbeeldbestanden aan het einde van dit artikel vindt u een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3af23-216">You can find an example in the sample files at the end of this article.</span></span> <span data-ttu-id="3af23-217">Dit bestand (opgeslagen met regeleinden Linux) in de gedeelde map /openfoam plaatsen.</span><span class="sxs-lookup"><span data-stu-id="3af23-217">Place this file (saved with Linux line endings) in the shared folder /openfoam.</span></span> <span data-ttu-id="3af23-218">Dit bestand bevat ook de instellingen voor de MPI en OpenFOAM runtimes die u later gebruiken een OpenFOAM-taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-218">This file also contains settings for the MPI and OpenFOAM runtimes that you use later to run an OpenFOAM job.</span></span>
3. <span data-ttu-id="3af23-219">Afhankelijke pakketten nodig voor het compileren van OpenFOAM installeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-219">Install dependent packages needed to compile OpenFOAM.</span></span> <span data-ttu-id="3af23-220">Mogelijk moet u eerst het toevoegen van een opslagplaats, afhankelijk van uw Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="3af23-220">Depending on your Linux distribution, you might first need to add a repository.</span></span> <span data-ttu-id="3af23-221">Voer **clusrun** vergelijkbaar met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="3af23-221">Run **clusrun** commands similar to the following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="3af23-222">Indien nodig, SSH op elk knooppunt Linux uitvoeren van de opdrachten om te bevestigen dat ze naar behoren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3af23-222">If necessary, SSH to each Linux node to run the commands to confirm that they run properly.</span></span>
4. <span data-ttu-id="3af23-223">Voer de volgende opdracht voor het compileren van OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="3af23-223">Run the following command to compile OpenFOAM.</span></span> <span data-ttu-id="3af23-224">De compilatie-proces neemt enige tijd in beslag en genereert een grote hoeveelheid informatie naar de standaarduitvoer in het foutenlogboek, gebruikt u dus de **/ interleaved** optie om de uitvoer interleaved weer te geven.</span><span class="sxs-lookup"><span data-stu-id="3af23-224">The compilation process takes some time to complete and generates a large amount of log information to standard output, so use the **/interleaved** option to display the output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="3af23-225">De '\\`' symbool in de opdracht is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3af23-225">The “\\`” symbol in the command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="3af23-226">"\\`&" betekent de "&" deel uitmaakt van de opdracht.</span><span class="sxs-lookup"><span data-stu-id="3af23-226">“\\`&” means the “&” is a part of the command.</span></span>
   > 
   > 

## <a name="prepare-to-run-an-openfoam-job"></a><span data-ttu-id="3af23-227">Voorbereiden van een taak OpenFOAM uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3af23-227">Prepare to run an OpenFOAM job</span></span>
<span data-ttu-id="3af23-228">Nu voorbereidingen voor het uitvoeren van een MPI-taak sloshingTank3D, namelijk een van de voorbeelden OpenFoam aangeroepen in twee Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-228">Now get ready to run an MPI job called sloshingTank3D, which is one of the OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-the-runtime-environment"></a><span data-ttu-id="3af23-229">De runtime-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="3af23-229">Set up the runtime environment</span></span>
<span data-ttu-id="3af23-230">Als u de runtimeomgevingen voor MPI en OpenFOAM instelt op de Linux-knooppunten, voer de volgende opdracht in een Windows PowerShell-venster op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-230">To set up the runtime environments for MPI and OpenFOAM on the Linux nodes, run the following command in a Windows PowerShell window on the head node.</span></span> <span data-ttu-id="3af23-231">(Deze opdracht is alleen geldig voor SUSE Linux.)</span><span class="sxs-lookup"><span data-stu-id="3af23-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="3af23-232">Voorbeeldgegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="3af23-232">Prepare sample data</span></span>
<span data-ttu-id="3af23-233">Het hoofdknooppunt-share die u eerder hebt geconfigureerd voor het delen van bestanden tussen de Linux-knooppunten (gekoppeld als /openfoam) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3af23-233">Use the head node share you configured previously to share files among the Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="3af23-234">SSH op een van uw Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-234">SSH to one of your Linux compute nodes.</span></span>
2. <span data-ttu-id="3af23-235">Voer de volgende opdracht voor het instellen van de OpenFOAM runtime-omgeving, als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="3af23-235">Run the following command to set up the OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="3af23-236">Het voorbeeld sloshingTank3D kopiëren naar de gedeelde map en navigeer naar het.</span><span class="sxs-lookup"><span data-stu-id="3af23-236">Copy the sloshingTank3D sample to the shared folder and navigate to it.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="3af23-237">Wanneer u de standaardparameters van dit voorbeeld gebruikt, kan duren tien minuten worden uitgevoerd, zodat u wijzigen van sommige parameters wilt mogelijk zodat deze sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3af23-237">When you use the default parameters of this sample, it can take tens of minutes to run, so you might want to modify some parameters to make it run faster.</span></span> <span data-ttu-id="3af23-238">Een eenvoudige keuze is om de tijd stap variabelen deltaT en writeInterval in het systeem/controlDict-bestand te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3af23-238">One simple choice is to modify the time step variables deltaT and writeInterval in the system/controlDict file.</span></span> <span data-ttu-id="3af23-239">Dit bestand wordt alle ingevoerde gegevens met betrekking tot het beheren van tijd- en lezen en schrijven van oplossingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3af23-239">This file stores all input data relating to the control of time and reading and writing solution data.</span></span> <span data-ttu-id="3af23-240">U kunt bijvoorbeeld de waarde van deltaT van 0,05 op 0,5 en de waarde van writeInterval van 0,05 op 0,5 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3af23-240">For example, you could change the value of deltaT from 0.05 to 0.5 and the value of writeInterval from 0.05 to 0.5.</span></span>
   
   ![Wijzig de variabelen in stap][step_variables]
5. <span data-ttu-id="3af23-242">Geef de gewenste waarden voor de variabelen in het bestand system/decomposeParDict.</span><span class="sxs-lookup"><span data-stu-id="3af23-242">Specify desired values for the variables in the system/decomposeParDict file.</span></span> <span data-ttu-id="3af23-243">In dit voorbeeld maakt gebruik van twee Linux-knooppunten elke met 8 kernen, dus numberOfSubdomains ingesteld op 16 en n van hierarchicalCoeffs naar (1 1 16), wat betekent dat OpenFOAM parallel met 16 processen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3af23-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains to 16 and n of hierarchicalCoeffs to (1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="3af23-244">Zie voor meer informatie [OpenFOAM User Guide: 3,4 uitgevoerd toepassingen parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="3af23-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Processen afbreken][decompose]
6. <span data-ttu-id="3af23-246">Voer de volgende opdrachten uit de directory sloshingTank3D voorbereiden van de voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="3af23-246">Run the following commands from the sloshingTank3D directory to prepare the sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="3af23-247">U ziet het hoofdknooppunt van dat de bestanden met voorbeeldgegevens worden gekopieerd naar C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="3af23-247">On the head node, you should see the sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="3af23-248">(C:\OpenFoam is de gedeelde map op het hoofdknooppunt.)</span><span class="sxs-lookup"><span data-stu-id="3af23-248">(C:\OpenFoam is the shared folder on the head node.)</span></span>
   
   ![Gegevensbestanden worden opgeslagen in het hoofdknooppunt][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="3af23-250">Hostbestand voor mpirun</span><span class="sxs-lookup"><span data-stu-id="3af23-250">Host file for mpirun</span></span>
<span data-ttu-id="3af23-251">In deze stap maakt u een hostbestand (een lijst van rekenknooppunten) die de **mpirun** opdracht gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3af23-251">In this step, you create a host file (a list of compute nodes) which the **mpirun** command uses.</span></span>

1. <span data-ttu-id="3af23-252">Op een van de Linux-knooppunten, door een bestand met de naam hostfile onder /openfoam, zodat dit bestand kan worden bereikt op /openfoam/hostfile op alle knooppunten van Linux te maken.</span><span class="sxs-lookup"><span data-stu-id="3af23-252">On one of the Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="3af23-253">Schrijf uw Linux-knooppuntnamen in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="3af23-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="3af23-254">In dit voorbeeld wordt bevat het bestand de volgende namen:</span><span class="sxs-lookup"><span data-stu-id="3af23-254">In this example, the file contains the following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="3af23-255">U kunt dit bestand ook op C:\OpenFoam\hostfile maken op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3af23-255">You can also create this file at C:\OpenFoam\hostfile on the head node.</span></span> <span data-ttu-id="3af23-256">Als u deze optie kiest, opslaan als een tekstbestand met Linux regeleinden (alleen LF, niet CR LF).</span><span class="sxs-lookup"><span data-stu-id="3af23-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="3af23-257">Dit zorgt ervoor dat deze wordt uitgevoerd naar behoren op de Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-257">This ensures that it runs properly on the Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="3af23-258">**Wrapper voor Bash-scripts**</span><span class="sxs-lookup"><span data-stu-id="3af23-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="3af23-259">Als u veel Linux-knooppunten hebt en u wilt dat uw uit te voeren op slechts enkele van deze taak, is het niet een goed idee om een hostbestand vaste te gebruiken omdat u niet weet welke knooppunten wordt toegewezen aan uw project.</span><span class="sxs-lookup"><span data-stu-id="3af23-259">If you have many Linux nodes and you want your job to run on only some of them, it’s not a good idea to use a fixed host file, because you don’t know which nodes will be allocated to your job.</span></span> <span data-ttu-id="3af23-260">In dit geval een bash script wrapper voor schrijven **mpirun** bestand met de host om automatisch te maken.</span><span class="sxs-lookup"><span data-stu-id="3af23-260">In this case, write a bash script wrapper for **mpirun** to create the host file automatically.</span></span> <span data-ttu-id="3af23-261">U kunt een voorbeeld bash script wrapper aangeroepen hpcimpirun.sh aan het einde van dit artikel vinden en opslaan als /openfoam/hpcimpirun.sh.</span><span class="sxs-lookup"><span data-stu-id="3af23-261">You can find an example bash script wrapper called hpcimpirun.sh at the end of this article, and save it as /openfoam/hpcimpirun.sh.</span></span> <span data-ttu-id="3af23-262">Dit voorbeeldscript doet het volgende:</span><span class="sxs-lookup"><span data-stu-id="3af23-262">This example script does the following:</span></span>
   
   1. <span data-ttu-id="3af23-263">Stelt de omgevingsvariabelen voor **mpirun**, en sommige opdrachtparameters toevoegen voor het uitvoeren van de taak MPI via het netwerk RDMA.</span><span class="sxs-lookup"><span data-stu-id="3af23-263">Sets up the environment variables for **mpirun**, and some addition command parameters to run the MPI job through the RDMA network.</span></span> <span data-ttu-id="3af23-264">In dit geval wordt de volgende variabelen ingesteld:</span><span class="sxs-lookup"><span data-stu-id="3af23-264">In this case, it sets the following variables:</span></span>
      
      * <span data-ttu-id="3af23-265">I_MPI_FABRICS shm:dapl =</span><span class="sxs-lookup"><span data-stu-id="3af23-265">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="3af23-266">I_MPI_DAPL_PROVIDER weergeeft van een-v2-ib0 =</span><span class="sxs-lookup"><span data-stu-id="3af23-266">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="3af23-267">I_MPI_DYNAMIC_CONNECTION = 0</span><span class="sxs-lookup"><span data-stu-id="3af23-267">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="3af23-268">Maakt een hostbestand volgens de omgeving variabele $CCP_NODES_CORES die is ingesteld door het hoofdknooppunt HPC wanneer de taak wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="3af23-268">Creates a host file according to the environment variable $CCP_NODES_CORES, which is set by the HPC head node when the job is activated.</span></span>
      
      <span data-ttu-id="3af23-269">De indeling van $CCP_NODES_CORES volgt dit patroon:</span><span class="sxs-lookup"><span data-stu-id="3af23-269">The format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="3af23-270">waar</span><span class="sxs-lookup"><span data-stu-id="3af23-270">where</span></span>
      
      * <span data-ttu-id="3af23-271">`<Number of nodes>`-het aantal knooppunten dat is toegewezen aan deze taak.</span><span class="sxs-lookup"><span data-stu-id="3af23-271">`<Number of nodes>` - the number of nodes allocated to this job.</span></span>  
      * <span data-ttu-id="3af23-272">`<Name of node_n_...>`-de naam van elk knooppunt dat is toegewezen aan deze taak.</span><span class="sxs-lookup"><span data-stu-id="3af23-272">`<Name of node_n_...>` - the name of each node allocated to this job.</span></span>
      * <span data-ttu-id="3af23-273">`<Cores of node_n_...>`-het aantal kernen op het knooppunt dat is toegewezen aan deze taak.</span><span class="sxs-lookup"><span data-stu-id="3af23-273">`<Cores of node_n_...>` - the number of cores on the node allocated to this job.</span></span>
      
      <span data-ttu-id="3af23-274">Bijvoorbeeld, als de taak twee knooppunten om uit te voeren moet, is $CCP_NODES_CORES vergelijkbaar met</span><span class="sxs-lookup"><span data-stu-id="3af23-274">For example, if the job needs two nodes to run, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="3af23-275">Aanroepen van de **mpirun** opdracht en voegt u twee parameters toe aan de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="3af23-275">Calls the **mpirun** command and appends two parameters to the command line.</span></span>
      
      * <span data-ttu-id="3af23-276">`--hostfile <hostfilepath>: <hostfilepath>`-het pad van het script maakt bestand met de host</span><span class="sxs-lookup"><span data-stu-id="3af23-276">`--hostfile <hostfilepath>: <hostfilepath>` - the path of the host file the script creates</span></span>
      * <span data-ttu-id="3af23-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-een omgevingsvariabele ingesteld door het hoofdknooppunt HPC Pack, waarin het aantal totale kernen toegewezen aan deze taak worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3af23-277">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by the HPC Pack head node, which stores the number of total cores allocated to this job.</span></span> <span data-ttu-id="3af23-278">In dit geval geeft het aantal processen voor **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="3af23-278">In this case, it specifies the number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="3af23-279">Verzenden van een taak OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="3af23-279">Submit an OpenFOAM job</span></span>
<span data-ttu-id="3af23-280">U kunt nu een taak in HPC Cluster Manager verzenden.</span><span class="sxs-lookup"><span data-stu-id="3af23-280">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="3af23-281">U moet de hpcimpirun.sh script in de opdrachtregels voor enkele van de taken van de taak doorgeven.</span><span class="sxs-lookup"><span data-stu-id="3af23-281">You need to pass the script hpcimpirun.sh in the command lines for some of the job tasks.</span></span>

1. <span data-ttu-id="3af23-282">Verbinding maken met het hoofdknooppunt van het cluster en start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="3af23-282">Connect to your cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="3af23-283">**In de Resource Management**, zorg ervoor dat de Linux-rekenknooppunten in de **Online** status.</span><span class="sxs-lookup"><span data-stu-id="3af23-283">**In Resource Management**, ensure that the Linux compute nodes are in the **Online** state.</span></span> <span data-ttu-id="3af23-284">Als dat niet het geval is, selecteert u deze en klikt u op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="3af23-284">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="3af23-285">In **Jobbeheer**, klikt u op **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="3af23-285">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="3af23-286">Voer een naam voor de taak zoals *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="3af23-286">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Taakdetails][job_details]
5. <span data-ttu-id="3af23-288">In **taak resources**, kies het type resource als 'Knooppunt' en het Minimum ingesteld op 2.</span><span class="sxs-lookup"><span data-stu-id="3af23-288">In **Job resources**, choose the type of resource as “Node” and set the Minimum to 2.</span></span> <span data-ttu-id="3af23-289">Deze configuratie wordt de taak uitgevoerd op twee Linux-knooppunten, elk met acht kernen in dit voorbeeld heeft.</span><span class="sxs-lookup"><span data-stu-id="3af23-289">This configuration runs the job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Taak resources][job_resources]
6. <span data-ttu-id="3af23-291">Klik op **taken bewerken** in de navigatiebalk aan de linkerkant en klik vervolgens op **toevoegen** een taak toevoegen aan de taak.</span><span class="sxs-lookup"><span data-stu-id="3af23-291">Click **Edit Tasks** in the left navigation, and then click **Add** to add a task to the job.</span></span> <span data-ttu-id="3af23-292">Vier taken toevoegen aan de taak met de volgende regels en instellingen.</span><span class="sxs-lookup"><span data-stu-id="3af23-292">Add four tasks to the job with the following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3af23-293">Met `source /openfoam/settings.sh` stelt u de OpenFOAM en MPI-runtime-omgevingen, zodat elk van de volgende taken vóór de opdracht OpenFOAM aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="3af23-293">Running `source /openfoam/settings.sh` sets up the OpenFOAM and MPI runtime environments, so each of the following tasks calls it before the OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="3af23-294">**Taak 1**.</span><span class="sxs-lookup"><span data-stu-id="3af23-294">**Task 1**.</span></span> <span data-ttu-id="3af23-295">Voer **decomposePar** voor het genereren van de gegevensbestanden voor het werken met **interDyMFoam** parallel.</span><span class="sxs-lookup"><span data-stu-id="3af23-295">Run **decomposePar** to generate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="3af23-296">Eén knooppunt toewijzen aan de taak</span><span class="sxs-lookup"><span data-stu-id="3af23-296">Assign one node to the task</span></span>
     * <span data-ttu-id="3af23-297">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="3af23-297">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="3af23-298">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="3af23-298">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="3af23-299">Zie de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="3af23-299">See the following figure.</span></span> <span data-ttu-id="3af23-300">U configureren de resterende taken op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="3af23-300">You configure the remaining tasks similarly.</span></span>
     
     ![Taak 1-details][task_details1]
   * <span data-ttu-id="3af23-302">**Taak 2**.</span><span class="sxs-lookup"><span data-stu-id="3af23-302">**Task 2**.</span></span> <span data-ttu-id="3af23-303">Voer **interDyMFoam** parallel berekenen van de steekproef.</span><span class="sxs-lookup"><span data-stu-id="3af23-303">Run **interDyMFoam** in parallel to compute the sample.</span></span>
     
     * <span data-ttu-id="3af23-304">Twee knooppunten toewijzen aan de taak</span><span class="sxs-lookup"><span data-stu-id="3af23-304">Assign two nodes to the task</span></span>
     * <span data-ttu-id="3af23-305">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="3af23-305">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="3af23-306">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="3af23-306">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="3af23-307">**Taak 3**.</span><span class="sxs-lookup"><span data-stu-id="3af23-307">**Task 3**.</span></span> <span data-ttu-id="3af23-308">Voer **reconstructPar** de sets met mappen van de tijd van elke directory processor_N_ samenvoegen in één verzameling.</span><span class="sxs-lookup"><span data-stu-id="3af23-308">Run **reconstructPar** to merge the sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="3af23-309">Eén knooppunt toewijzen aan de taak</span><span class="sxs-lookup"><span data-stu-id="3af23-309">Assign one node to the task</span></span>
     * <span data-ttu-id="3af23-310">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="3af23-310">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="3af23-311">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="3af23-311">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="3af23-312">**Taak 4**.</span><span class="sxs-lookup"><span data-stu-id="3af23-312">**Task 4**.</span></span> <span data-ttu-id="3af23-313">Voer **foamToEnsight** parallel te converteren van het resultaat OpenFOAM bestanden naar EnSight formatteren en de bestanden EnSight plaatsen in een map met de naam Ensight in de map voor de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="3af23-313">Run **foamToEnsight** in parallel to convert the OpenFOAM result files into EnSight format and place the EnSight files in a directory named Ensight in the case directory.</span></span>
     
     * <span data-ttu-id="3af23-314">Twee knooppunten toewijzen aan de taak</span><span class="sxs-lookup"><span data-stu-id="3af23-314">Assign two nodes to the task</span></span>
     * <span data-ttu-id="3af23-315">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="3af23-315">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="3af23-316">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="3af23-316">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="3af23-317">Voeg de afhankelijkheden toe aan deze taken in oplopende taakvolgorde.</span><span class="sxs-lookup"><span data-stu-id="3af23-317">Add dependencies to these tasks in ascending task order.</span></span>
   
   ![Taakafhankelijkheden][task_dependencies]
8. <span data-ttu-id="3af23-319">Klik op **indienen** deze taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-319">Click **Submit** to run this job.</span></span>
   
   <span data-ttu-id="3af23-320">Standaard verzonden HPC Pack door de taak als uw huidige aangemelde gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="3af23-320">By default, HPC Pack submits the job as your current logged-on user account.</span></span> <span data-ttu-id="3af23-321">Nadat u op **indienen**, ziet u mogelijk een dialoogvenster waarin u de gebruikersnaam en wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="3af23-321">After you click **Submit**, you might see a dialog box prompting you to enter the user name and password.</span></span>
   
   ![Taak referenties][creds]
   
   <span data-ttu-id="3af23-323">Onder bepaalde omstandigheden onthoudt HPC Pack u de gebruikersgegevens invoeren voordat u dit dialoogvenster niet weergeven.</span><span class="sxs-lookup"><span data-stu-id="3af23-323">Under some conditions, HPC Pack remembers the user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="3af23-324">Voer de volgende opdracht achter de opdrachtprompt en verzend de taak zodat HPC Pack opnieuw weergeven.</span><span class="sxs-lookup"><span data-stu-id="3af23-324">To make HPC Pack show it again, enter the following command at a Command prompt and then submit the job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="3af23-325">De taak duurt van tien minuten tot enkele uren volgens de parameters die u hebt ingesteld voor het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3af23-325">The job takes from tens of minutes to several hours according to the parameters you have set for the sample.</span></span> <span data-ttu-id="3af23-326">In de heatmap ziet u de taak uitgevoerd op de Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="3af23-326">In the heat map, you see the job running on the Linux nodes.</span></span> 
   
   ![Heatmap][heat_map]
   
   <span data-ttu-id="3af23-328">Op elk knooppunt worden acht processen gestart.</span><span class="sxs-lookup"><span data-stu-id="3af23-328">On each node, eight processes are started.</span></span>
   
   ![Linux-processen][linux_processes]
10. <span data-ttu-id="3af23-330">Wanneer de taak is voltooid, moet u resultaten van de taak vinden in mappen onder C:\OpenFoam\sloshingTank3D en de logboekbestanden op C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="3af23-330">When the job finishes, find the job results in folders under C:\OpenFoam\sloshingTank3D, and the log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="3af23-331">De resultaten weergeven in EnSight</span><span class="sxs-lookup"><span data-stu-id="3af23-331">View results in EnSight</span></span>
<span data-ttu-id="3af23-332">Optioneel gebruik [EnSight](https://www.ceisoftware.com/) visualiseren en analyseren van de resultaten van de taak OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="3af23-332">Optionally use [EnSight](https://www.ceisoftware.com/) to visualize and analyze the results of the OpenFOAM job.</span></span> <span data-ttu-id="3af23-333">Zie voor meer informatie over visualisatie en animatie in EnSight, [video handleiding](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="3af23-333">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="3af23-334">Nadat u op het hoofdknooppunt EnSight hebt geïnstalleerd, start u deze.</span><span class="sxs-lookup"><span data-stu-id="3af23-334">After you install EnSight on the head node, start it.</span></span>
2. <span data-ttu-id="3af23-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="3af23-335">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="3af23-336">U ziet een vervangen in de viewer.</span><span class="sxs-lookup"><span data-stu-id="3af23-336">You see a tank in the viewer.</span></span>
   
   ![Vervangen in EnSight][tank]
3. <span data-ttu-id="3af23-338">Maak een **Isosurface** van **internalMesh**, en kies vervolgens de variabele **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="3af23-338">Create an **Isosurface** from **internalMesh**, and then choose the variable **alpha_water**.</span></span>
   
   ![Een isosurface maken][isosurface]
4. <span data-ttu-id="3af23-340">De kleur voor **Isosurface_part** in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3af23-340">Set the color for **Isosurface_part** created in the previous step.</span></span> <span data-ttu-id="3af23-341">Bijvoorbeeld: Stel deze in op water blauw.</span><span class="sxs-lookup"><span data-stu-id="3af23-341">For example, set it to water blue.</span></span>
   
   ![Isosurface kleur bewerken][isosurface_color]
5. <span data-ttu-id="3af23-343">Maak een **Iso-volume** van **wanden** door te selecteren **wanden** in de **delen** paneel en klik op de **Isosurfaces** knop op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="3af23-343">Create an **Iso-volume** from **walls** by selecting **walls** in the **Parts** panel and click the **Isosurfaces** button in the toolbar.</span></span>
6. <span data-ttu-id="3af23-344">Selecteer in het dialoogvenster **Type** als **Isovolume** en stelt het minimum van **Isovolume bereik** op 0,5.</span><span class="sxs-lookup"><span data-stu-id="3af23-344">In the dialog box, select **Type** as **Isovolume** and set the Min of **Isovolume range** to 0.5.</span></span> <span data-ttu-id="3af23-345">Klik op om de isovolume **maken met de geselecteerde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="3af23-345">To create the isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="3af23-346">De kleur voor **Iso_volume_part** in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3af23-346">Set the color for **Iso_volume_part** created in the previous step.</span></span> <span data-ttu-id="3af23-347">Bijvoorbeeld: Stel deze in op grondige water blauw.</span><span class="sxs-lookup"><span data-stu-id="3af23-347">For example, set it to deep water blue.</span></span>
8. <span data-ttu-id="3af23-348">De kleur voor **wanden**.</span><span class="sxs-lookup"><span data-stu-id="3af23-348">Set the color for **walls**.</span></span> <span data-ttu-id="3af23-349">Bijvoorbeeld, deze instellen op transparante wit.</span><span class="sxs-lookup"><span data-stu-id="3af23-349">For example, set it to transparent white.</span></span>
9. <span data-ttu-id="3af23-350">Klik nu op **afspelen** om de resultaten van de simulatie te bekijken.</span><span class="sxs-lookup"><span data-stu-id="3af23-350">Now click **Play** to see the results of the simulation.</span></span>
   
    ![Resultaat van de vervangen][tank_result]

## <a name="sample-files"></a><span data-ttu-id="3af23-352">Voorbeeldbestanden</span><span class="sxs-lookup"><span data-stu-id="3af23-352">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="3af23-353">Voorbeeld XML-configuratiebestand voor implementatie van het cluster door PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="3af23-353">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
 ```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>allvhdsje</StorageAccount>
  </Subscription>
  <Location>Japan East</Location>  
  <VNet>
    <VNetName>suse12rdmavnet</VNetName>
    <SubnetName>SUSE12RDMACluster</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>SUSE12RDMA-HN</VMName>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>SUSE12RDMA-LN%1%</VMNamePattern>
    <ServiceName>suse12rdma-je</ServiceName>
    <VMSize>A8</VMSize>
    <NodeCount>2</NodeCount>
      <ImageName>b4590d9e3ed742e4a1d46e5424aa335e__suse-sles-12-hpc-v20150708</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>
```

### <a name="sample-credxml-file"></a><span data-ttu-id="3af23-354">Voorbeeldbestand cred.xml</span><span class="sxs-lookup"><span data-stu-id="3af23-354">Sample cred.xml file</span></span>
```
<ExtendedData>
  <PrivateKey>-----BEGIN RSA PRIVATE KEY-----
MIIEpQIBAAKCAQEAxJKBABhnOsE9eneGHvsjdoXKooHUxpTHI1JVunAJkVmFy8JC
qFt1pV98QCtKEHTC6kQ7tj1UT2N6nx1EY9BBHpZacnXmknpKdX4Nu0cNlSphLpru
lscKPR3XVzkTwEF00OMiNJVknq8qXJF1T3lYx3rW5EnItn6C3nQm3gQPXP0ckYCF
Jdtu/6SSgzV9kaapctLGPNp1Vjf9KeDQMrJXsQNHxnQcfiICp21NiUCiXosDqJrR
AfzePdl0XwsNngouy8t0fPlNSngZvsx+kPGh/AKakKIYS0cO9W3FmdYNW8Xehzkc
VzrtJhU8x21hXGfSC7V0ZeD7dMeTL3tQCVxCmwIDAQABAoIBAQCve8Jh3Wc6koxZ
qh43xicwhdwSGyliZisoozYZDC/ebDb/Ydq0BYIPMiDwADVMX5AqJuPPmwyLGtm6
9hu5p46aycrQ5+QA299g6DlF+PZtNbowKuvX+rRvPxagrTmupkCswjglDUEYUHPW
05wQaNoSqtzwS9Y85M/b24FfLeyxK0n8zjKFErJaHdhVxI6cxw7RdVlSmM9UHmah
wTkW8HkblbOArilAHi6SlRTNZG4gTGeDzPb7fYZo3hzJyLbcaNfJscUuqnAJ+6pT
iY6NNp1E8PQgjvHe21yv3DRoVRM4egqQvNZgUbYAMUgr30T1UoxnUXwk2vqJMfg2
Nzw0ESGRAoGBAPkfXjjGfc4HryqPkdx0kjXs0bXC3js2g4IXItK9YUFeZzf+476y
OTMQg/8DUbqd5rLv7PITIAqpGs39pkfnyohPjOe2zZzeoyaXurYIPV98hhH880uH
ZUhOxJYnlqHGxGT7p2PmmnAlmY4TSJrp12VnuiQVVVsXWOGPqHx4S4f9AoGBAMn/
vuea7hsCgwIE25MJJ55FYCJodLkioQy6aGP4NgB89Azzg527WsQ6H5xhgVMKHWyu
Q1snp+q8LyzD0i1veEvWb8EYifsMyTIPXOUTwZgzaTTCeJNHdc4gw1U22vd7OBYy
nZCU7Tn8Pe6eIMNztnVduiv+2QHuiNPgN7M73/x3AoGBAOL0IcmFgy0EsR8MBq0Z
ge4gnniBXCYDptEINNBaeVStJUnNKzwab6PGwwm6w2VI3thbXbi3lbRAlMve7fKK
B2ghWNPsJOtppKbPCek2Hnt0HUwb7qX7Zlj2cX/99uvRAjChVsDbYA0VJAxcIwQG
TxXx5pFi4g0HexCa6LrkeKMdAoGAcvRIACX7OwPC6nM5QgQDt95jRzGKu5EpdcTf
g4TNtplliblLPYhRrzokoyoaHteyxxak3ktDFCLj9eW6xoCZRQ9Tqd/9JhGwrfxw
MS19DtCzHoNNewM/135tqyD8m7pTwM4tPQqDtmwGErWKj7BaNZARUlhFxwOoemsv
R6DbZyECgYEAhjL2N3Pc+WW+8x2bbIBN3rJcMjBBIivB62AwgYZnA2D5wk5o0DKD
eesGSKS5l22ZMXJNShgzPKmv3HpH22CSVpO0sNZ6R+iG8a3oq4QkU61MT1CfGoMI
a8lxTKnZCsRXU1HexqZs+DSc+30tz50bNqLdido/l5B4EJnQP03ciO0=
-----END RSA PRIVATE KEY-----</PrivateKey>
  <PublicKey>ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDEkoEAGGc6wT16d4Ye+yN2hcqigdTGlMcjUlW6cAmRWYXLwkKoW3WlX3xAK0oQdMLqRDu2PVRPY3qfHURj0EEellpydeaSekp1fg27Rw2VKmEumu6Wxwo9HddXORPAQXTQ4yI0lWSerypckXVPeVjHetbkSci2foLedCbeBA9c/RyRgIUl227/pJKDNX2Rpqly0sY82nVWN/0p4NAyslexA0fGdBx+IgKnbU2JQKJeiwOomtEB/N492XRfCw2eCi7Ly3R8+U1KeBm+zH6Q8aH8ApqQohhLRw71bcWZ1g1bxd6HORxXOu0mFTzHbWFcZ9ILtXRl4Pt0x5Mve1AJXEKb username@servername;</PublicKey>
</ExtendedData>
```
### <a name="sample-silentcfg-file-to-install-mpi"></a><span data-ttu-id="3af23-355">Voorbeeld van een bestand silent.cfg MPI installeren</span><span class="sxs-lookup"><span data-stu-id="3af23-355">Sample silent.cfg file to install MPI</span></span>
```
# Patterns used to check silent configuration file
#
# anythingpat - any string
# filepat     - the file location pattern (/file/location/to/license.lic)
# lspat       - the license server address pattern (0123@hostname)
# snpat       - the serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components to install, valid values are: {ALL, DEFAULTS, anythingpat}
COMPONENTS=DEFAULTS

# installation mode, valid values are: {install, modify, repair, uninstall}
PSET_MODE=install

# directory for non-RPM database, valid values are: {filepat}
#NONRPM_DB_DIR=filepat

# Serial number, valid values are: {snpat}
#ACTIVATION_SERIAL_NUMBER=snpat

# License file or license server, valid values are: {lspat, filepat}
#ACTIVATION_LICENSE_FILE=

# Activation type, valid values are: {exist_lic, license_server, license_file, trial_lic, serial_number}
ACTIVATION_TYPE=trial_lic

# Path to the cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes to enable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes to update ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="3af23-356">Voorbeeldscript settings.sh</span><span class="sxs-lookup"><span data-stu-id="3af23-356">Sample settings.sh script</span></span>
```
#!/bin/bash

# impi
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# openfoam
export FOAM_INST_DIR=/opt/OpenFOAM
source /opt/OpenFOAM/OpenFOAM-2.3.1/etc/bashrc
export WM_MPLIB=INTELMPI
```


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="3af23-357">Voorbeeldscript hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="3af23-357">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# The path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"

# Set mpirun runtime evironment
source /opt/intel/impi/5.0.3.048/bin64/mpivars.sh
export MPI_ROOT=$I_MPI_ROOT
export I_MPI_FABRICS=shm:dapl
export I_MPI_DAPL_PROVIDER=ofa-v2-ib0
export I_MPI_DYNAMIC_CONNECTION=0

# mpirun command
MPIRUN=mpirun
# Argument of "--hostfile"
NODELIST_OPT="--hostfile"
# Argument of "-np"
NUMPROCESS_OPT="-np"

# Get node information from ENVs
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # CCP_NODES_CORES is not found or is empty, just run the mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create the hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into the hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run the mpirun with hostfile arg
    ${MPIRUN} ${NUMPROCESS_OPT} ${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}

```





<!--Image references-->
[keygen]:media/hpcpack-cluster-openfoam/keygen.png
[keys]:media/hpcpack-cluster-openfoam/keys.png
[step_variables]:media/hpcpack-cluster-openfoam/step_variables.png
[data_files]:media/hpcpack-cluster-openfoam/data_files.png
[decompose]:media/hpcpack-cluster-openfoam/decompose.png
[job_details]:media/hpcpack-cluster-openfoam/job_details.png
[job_resources]:media/hpcpack-cluster-openfoam/job_resources.png
[task_details1]:media/hpcpack-cluster-openfoam/task_details1.png
[task_dependencies]:media/hpcpack-cluster-openfoam/task_dependencies.png
[creds]:media/hpcpack-cluster-openfoam/creds.png
[heat_map]:media/hpcpack-cluster-openfoam/heat_map.png
[tank]:media/hpcpack-cluster-openfoam/tank.png
[tank_result]:media/hpcpack-cluster-openfoam/tank_result.png
[isosurface]:media/hpcpack-cluster-openfoam/isosurface.png
[isosurface_color]:media/hpcpack-cluster-openfoam/isosurface_color.png
[linux_processes]:media/hpcpack-cluster-openfoam/linux_processes.png

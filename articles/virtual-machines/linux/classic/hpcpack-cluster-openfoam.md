---
title: aaaRun OpenFOAM HPC Pack op de virtuele Linux-machines | Microsoft Docs
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
ms.openlocfilehash: 1a51ffe6804abb5156f01d580c9b7a4a9649377a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-openfoam-with-microsoft-hpc-pack-on-a-linux-rdma-cluster-in-azure"></a><span data-ttu-id="a58a0-103">OpenFoam uitvoeren met Microsoft HPC Pack op een Linux RDMA-cluster in Azure</span><span class="sxs-lookup"><span data-stu-id="a58a0-103">Run OpenFoam with Microsoft HPC Pack on a Linux RDMA cluster in Azure</span></span>
<span data-ttu-id="a58a0-104">Dit artikel ziet u een eenrichtingssessie toorun OpenFoam in virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="a58a0-104">This article shows you one way toorun OpenFoam in Azure virtual machines.</span></span> <span data-ttu-id="a58a0-105">Hier kunt u een cluster met Microsoft HPC Pack met Linux-rekenknooppunten in Azure en voer implementeert een [OpenFoam](http://openfoam.com/) taak met de Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="a58a0-105">Here, you deploy a Microsoft HPC Pack cluster with Linux compute nodes on Azure and run an [OpenFoam](http://openfoam.com/) job with Intel MPI.</span></span> <span data-ttu-id="a58a0-106">Kunt u RDMA-compatibele Azure Virtual machines Hallo rekenknooppunten, zodat Hallo rekenknooppunten hello Azure RDMA netwerk communiceert.</span><span class="sxs-lookup"><span data-stu-id="a58a0-106">You can use RDMA-capable Azure VMs for hello compute nodes, so that hello compute nodes communicate over hello Azure RDMA network.</span></span> <span data-ttu-id="a58a0-107">Andere opties toorun OpenFoam in Azure omvatten volledig geconfigureerd commerciële installatiekopieën beschikbaar zijn in Hallo Marketplace, zoals de UberCloud [OpenFoam 2.3 op CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), en door te voeren op [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span><span class="sxs-lookup"><span data-stu-id="a58a0-107">Other options toorun OpenFoam in Azure include fully configured commercial images available in hello Marketplace, such as UberCloud's [OpenFoam 2.3 on CentOS 6](https://azure.microsoft.com/marketplace/partners/ubercloud/openfoam-v2dot3-centos-v6/), and by running on [Azure Batch](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/).</span></span> 

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="a58a0-108">OpenFOAM (voor veld bewerking openen en bewerken) is een open source computational fluid dynamics (CFD)-softwarepakket dat algemeen wordt gebruikt in de technische en wetenschappelijke in commerciële en academic organisaties.</span><span class="sxs-lookup"><span data-stu-id="a58a0-108">OpenFOAM (for Open Field Operation and Manipulation) is an open-source computational fluid dynamics (CFD) software package that is used widely in engineering and science, in both commercial and academic organizations.</span></span> <span data-ttu-id="a58a0-109">Dit omvat de hulpprogramma's voor meshing, met name snappyHexMesh, een parallelized mesher voor complexe CAD-geometrie en voor vóór en na verwerking.</span><span class="sxs-lookup"><span data-stu-id="a58a0-109">It includes tools for meshing, notably snappyHexMesh, a parallelized mesher for complex CAD geometries, and for pre- and post-processing.</span></span> <span data-ttu-id="a58a0-110">Bijna alle processen parallel uitgevoerd, waardoor gebruikers tootake volledig gebruikmaken van de hardware van de computer beschikken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-110">Almost all processes run in parallel, enabling users tootake full advantage of computer hardware at their disposal.</span></span>  

<span data-ttu-id="a58a0-111">Microsoft HPC Pack functies toorun biedt grootschalige HPC en parallelle toepassingen, waaronder MPI-toepassingen op clusters van Microsoft Azure virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="a58a0-111">Microsoft HPC Pack provides features toorun large-scale HPC and parallel applications, including MPI applications, on clusters of Microsoft Azure virtual machines.</span></span> <span data-ttu-id="a58a0-112">HPC Pack ondersteunt ook actief Linux HPC-toepassingen op Linux VM's geïmplementeerd in een cluster HPC Pack rekenknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-112">HPC Pack also supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="a58a0-113">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor een inleiding toousing Linux rekenknooppunten HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="a58a0-113">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction toousing Linux compute nodes with HPC Pack.</span></span>

> [!NOTE]
> <span data-ttu-id="a58a0-114">Dit artikel wordt beschreven hoe een Linux MPI-werkbelasting met HPC Pack toorun.</span><span class="sxs-lookup"><span data-stu-id="a58a0-114">This article illustrates how toorun a Linux MPI workload with HPC Pack.</span></span> <span data-ttu-id="a58a0-115">Wordt ervan uitgegaan dat u enigszins bekend bent met Linux Systeembeheer en MPI belastingen uitgevoerd op Linux-clusters hebben.</span><span class="sxs-lookup"><span data-stu-id="a58a0-115">It assumes you have some familiarity with Linux system administration and with running MPI workloads on Linux clusters.</span></span> <span data-ttu-id="a58a0-116">Als u versies van MPI en OpenFOAM verschilt Hallo voorbeelden in dit artikel gebruikt, wellicht u toomodify een aantal stappen installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="a58a0-116">If you use versions of MPI and OpenFOAM different from hello ones shown in this article, you might have toomodify some installation and configuration steps.</span></span> 
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a58a0-117">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a58a0-117">Prerequisites</span></span>
* <span data-ttu-id="a58a0-118">**HPC Pack cluster met RDMA-compatibele Linux-rekenknooppunten** : een cluster HPC Pack met een grootte A8, A9, H16r, implementeren of H16rm Linux-rekenknooppunten met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) of een [Azure PowerShell-script](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="a58a0-118">**HPC Pack cluster with RDMA-capable Linux compute nodes** - Deploy an HPC Pack cluster with size A8, A9, H16r, or H16rm Linux compute nodes using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="a58a0-119">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor Hallo vereisten en stappen voor beide opties.</span><span class="sxs-lookup"><span data-stu-id="a58a0-119">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="a58a0-120">Als u ervoor Hallo Implementatieoptie PowerShell-script kiest, ziet u Hallo voorbeeldconfiguratiebestand in Hallo voorbeeldbestanden aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a58a0-120">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="a58a0-121">Gebruik deze configuratie een op Azure gebaseerde toodeploy HPC Pack cluster die bestaan uit een grootte A8 Windows Server 2012 R2-hoofdknooppunt en 2 grootte A8 SUSE Linux Enterprise Server 12 rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-121">Use this configuration toodeploy an Azure-based HPC Pack cluster consisting of a size A8 Windows Server 2012 R2 head node and 2 size A8 SUSE Linux Enterprise Server 12 compute nodes.</span></span> <span data-ttu-id="a58a0-122">Vervang de juiste waarden voor uw abonnement en de service namen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-122">Substitute appropriate values for your subscription and service names.</span></span> 
  
  <span data-ttu-id="a58a0-123">**Extra zaken tooknow**</span><span class="sxs-lookup"><span data-stu-id="a58a0-123">**Additional things tooknow**</span></span>
  
  * <span data-ttu-id="a58a0-124">Zie voor Linux RDMA netwerken vereisten in Azure, [hoge prestaties compute-VM-grootten](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a58a0-124">For Linux RDMA networking prerequisites in Azure, see [High performance compute VM sizes](../../windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
  * <span data-ttu-id="a58a0-125">Als u Hallo Implementatieoptie Powershell-script gebruikt, moet u alle Hallo Linux-rekenknooppunten in een cloud service toouse hello RDMA-netwerkverbinding implementeren.</span><span class="sxs-lookup"><span data-stu-id="a58a0-125">If you use hello Powershell script deployment option, deploy all hello Linux compute nodes within one cloud service toouse hello RDMA network connection.</span></span>
  * <span data-ttu-id="a58a0-126">Na implementatie Hallo Linux-knooppunten, verbinding maken via SSH tooperform eventuele extra beheertaken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-126">After deploying hello Linux nodes, connect by SSH tooperform any additional administrative tasks.</span></span> <span data-ttu-id="a58a0-127">Hallo SSH Verbindingsdetails voor elke Linux-VM niet vinden in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a58a0-127">Find hello SSH connection details for each Linux VM in hello Azure portal.</span></span>  
* <span data-ttu-id="a58a0-128">**Intel MPI** -toorun OpenFOAM op SLES 12 HPC rekenknooppunten in Azure, moet u tooinstall Hallo Intel MPI-bibliotheek 5 runtime vanuit Hallo [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span><span class="sxs-lookup"><span data-stu-id="a58a0-128">**Intel MPI** - toorun OpenFOAM on SLES 12 HPC compute nodes in Azure, you need tooinstall hello Intel MPI Library 5 runtime from hello [Intel.com site](https://software.intel.com/en-us/intel-mpi-library/).</span></span> <span data-ttu-id="a58a0-129">(Intel MPI 5 is voorgeïnstalleerd op op basis van CentOS HPC-installatiekopieën.)  Installeer Intel MPI op uw Linux-rekenknooppunten in een latere stap, indien nodig.</span><span class="sxs-lookup"><span data-stu-id="a58a0-129">(Intel MPI 5 is preinstalled on CentOS-based HPC images.)  In a later step, if necessary, install Intel MPI on your Linux compute nodes.</span></span> <span data-ttu-id="a58a0-130">tooprepare voor deze stap nadat u hebt geregistreerd met Intel, volg Hallo koppeling op Hallo bevestiging e toohello gerelateerde webpagina.</span><span class="sxs-lookup"><span data-stu-id="a58a0-130">tooprepare for this step, after you register with Intel, follow hello link in hello confirmation email toohello related web page.</span></span> <span data-ttu-id="a58a0-131">Vervolgens kopiëren Hallo downloadkoppeling voor Hallo .tgz bestand voor de juiste versie van Intel MPI Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58a0-131">Then, copy hello download link for hello .tgz file for hello appropriate version of Intel MPI.</span></span> <span data-ttu-id="a58a0-132">In dit artikel is gebaseerd op Intel MPI versie 5.0.3.048.</span><span class="sxs-lookup"><span data-stu-id="a58a0-132">This article is based on Intel MPI version 5.0.3.048.</span></span>
* <span data-ttu-id="a58a0-133">**OpenFOAM bron Pack** -Hallo OpenFOAM bron Pack software voor Linux downloaden van Hallo [OpenFOAM Foundation-site](http://openfoam.org/download/2-3-1-source/).</span><span class="sxs-lookup"><span data-stu-id="a58a0-133">**OpenFOAM Source Pack** - Download hello OpenFOAM Source Pack software for Linux from hello [OpenFOAM Foundation site](http://openfoam.org/download/2-3-1-source/).</span></span> <span data-ttu-id="a58a0-134">In dit artikel is gebaseerd op de bron-packversie 2.3.1-specificaties gedownload als OpenFOAM 2.3.1.tgz.</span><span class="sxs-lookup"><span data-stu-id="a58a0-134">This article is based on Source Pack version 2.3.1, available for download as OpenFOAM-2.3.1.tgz.</span></span> <span data-ttu-id="a58a0-135">Volg de instructies Hallo verderop in dit artikel toounpack en OpenFOAM compileren op Hallo Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-135">Follow hello instructions later in this article toounpack and compile OpenFOAM on hello Linux compute nodes.</span></span>
* <span data-ttu-id="a58a0-136">**EnSight** (optioneel) - toosee Hallo resultaten van uw simulatie OpenFOAM downloaden en installeren van Hallo [EnSight](https://www.ceisoftware.com/download/) visualisatie en analyse-programma.</span><span class="sxs-lookup"><span data-stu-id="a58a0-136">**EnSight** (optional) - toosee hello results of your OpenFOAM simulation, download and install hello [EnSight](https://www.ceisoftware.com/download/) visualization and analysis program.</span></span> <span data-ttu-id="a58a0-137">Licentie-en downloaden op Hallo EnSight site zijn.</span><span class="sxs-lookup"><span data-stu-id="a58a0-137">Licensing and download information are at hello EnSight site.</span></span>

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="a58a0-138">Wederzijdse vertrouwensrelatie tussen de rekenknooppunten instellen</span><span class="sxs-lookup"><span data-stu-id="a58a0-138">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="a58a0-139">Een taak cross-knooppunt wordt uitgevoerd op meerdere Linux-knooppunten vereist Hallo knooppunten tootrust elkaar (door **rsh** of **ssh**).</span><span class="sxs-lookup"><span data-stu-id="a58a0-139">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="a58a0-140">Wanneer u Hallo HPC Pack cluster met Microsoft HPC Pack IaaS-implementatiescript hello maakt, Hallo script permanente wederzijds vertrouwen voor Hallo beheerdersaccount dat u opgeeft automatisch ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-140">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="a58a0-141">Voor gebruikers die geen beheerder u in Hallo clusterdomein maakt, hebt u tooset een tijdelijke wederzijdse vertrouwensrelatie tussen knooppunten Hallo wanneer een taak toothem is toegewezen en Hallo relatie vernietigen wanneer Hallo is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a58a0-141">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem, and destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="a58a0-142">tooestablish vertrouwen voor elke gebruiker een RSA-sleutelpaar toohello cluster HPC Pack gebruikt voor de vertrouwensrelatie Hallo bieden.</span><span class="sxs-lookup"><span data-stu-id="a58a0-142">tooestablish trust for each user, provide an RSA key pair toohello cluster that HPC Pack uses for hello trust relationship.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="a58a0-143">Een RSA-sleutelpaar niet genereren</span><span class="sxs-lookup"><span data-stu-id="a58a0-143">Generate an RSA key pair</span></span>
<span data-ttu-id="a58a0-144">Is het eenvoudig toogenerate een RSA-sleutelpaar, die een openbare sleutel en een persoonlijke sleutel bevat, door te voeren Hallo Linux **ssh-keygen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="a58a0-144">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="a58a0-145">Meld u aan tooa Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="a58a0-145">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="a58a0-146">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a58a0-146">Run hello following command:</span></span>
   
   ```
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="a58a0-147">Druk op **Enter** toouse Hallo standaardinstellingen totdat Hallo-opdracht is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a58a0-147">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="a58a0-148">Voer een wachtwoordzin hier; niet Wanneer u daarom wordt gevraagd om een wachtwoord op te geven, drukt u op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-148">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Een RSA-sleutelpaar niet genereren][keygen]
3. <span data-ttu-id="a58a0-150">Wijzig de directory toohello ~/.ssh directory.</span><span class="sxs-lookup"><span data-stu-id="a58a0-150">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="a58a0-151">Hallo persoonlijke sleutel wordt opgeslagen in id_rsa en Hallo openbare sleutel in id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="a58a0-151">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Persoonlijke en openbare sleutel][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="a58a0-153">Hallo sleutelpaar toohello HPC Pack cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="a58a0-153">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="a58a0-154">Maken van een extern bureaublad verbinding tooyour hoofdknooppunt met uw beheerdersaccount HPC Pack (Hallo administrator-account u instellen wanneer u het implementatiescript Hallo uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="a58a0-154">Make a Remote Desktop connection tooyour head node with your HPC Pack administrator account (hello administrator account you set up when you ran hello deployment script).</span></span>
2. <span data-ttu-id="a58a0-155">Gebruik standaard Windows Server procedures toocreate een domeingebruikersaccount in Active Directory-domein Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a58a0-155">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="a58a0-156">Bijvoorbeeld Hallo Active Directory-gebruikers en Computers hulpprogramma gebruiken op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-156">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="a58a0-157">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u een domeingebruiker die met de naam hpclab\hpcuser maken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-157">hello examples in this article assume you create a domain user named hpclab\hpcuser.</span></span>
3. <span data-ttu-id="a58a0-158">Maak een bestand met de naam C:\cred.xml en kopieer Hallo RSA belangrijke gegevens in de App.</span><span class="sxs-lookup"><span data-stu-id="a58a0-158">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="a58a0-159">Er is een voorbeeldbestand cred.xml op Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a58a0-159">A sample cred.xml file is at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
4. <span data-ttu-id="a58a0-160">Open een opdrachtprompt en Voer Hallo opdracht tooset Hallo-gegevens voor Hallo hpclab\hpcuser account referenties te volgen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-160">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="a58a0-161">Gebruik van Hallo **extendeddata** parameter toopass Hallo naam van C:\cred.xml u hebt gemaakt voor Hallo belangrijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="a58a0-161">You use hello **extendeddata** parameter toopass hello name of C:\cred.xml file you created for hello key data.</span></span>
   
   ```
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="a58a0-162">Deze opdracht is voltooid zonder uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a58a0-162">This command completes successfully without output.</span></span> <span data-ttu-id="a58a0-163">Na het instellen van referenties voor gebruikersaccounts Hallo moet u taken toorun Hallo Hallo cred.xml bestand opslaan op een veilige locatie of verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="a58a0-163">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
5. <span data-ttu-id="a58a0-164">Als u Hallo RSA-sleutelpaar gegenereerd op een van uw Linux-knooppunten, moet u toodelete Hallo sleutels als u klaar bent met het gebruik ervan.</span><span class="sxs-lookup"><span data-stu-id="a58a0-164">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="a58a0-165">HPC Pack vindt een bestaande id_rsa bestand of id_rsa.pub-bestand, dan wordt deze wederzijds vertrouwen niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-165">If HPC Pack finds an existing id_rsa file or id_rsa.pub file, it does not set up mutual trust.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a58a0-166">Wordt niet aanbevolen als de Clusterbeheerder van een een Linux-taak wordt uitgevoerd op een gedeelde cluster, omdat een taak die is verzonden door een beheerder wordt uitgevoerd onder het hoofdaccount Hallo op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-166">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="a58a0-167">Een taak die is verzonden door een gebruiker die geen beheerder wordt echter uitgevoerd onder een lokale Linux-gebruikersaccount met dezelfde naam als Hallo taak gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58a0-167">However, a job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="a58a0-168">In dit geval stelt HPC Pack wederzijds vertrouwen voor deze gebruiker Linux op Hallo knooppunten toohello taak toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-168">In this case, HPC Pack sets up mutual trust for this Linux user across hello nodes allocated toohello job.</span></span> <span data-ttu-id="a58a0-169">U kunt Hallo Linux gebruiker handmatig op de Linux-knooppunten Hallo instellen voordat u Hallo batchverwerking of HPC Pack Hallo gebruiker automatisch gemaakt wanneer Hallo job wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="a58a0-169">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="a58a0-170">Als HPC Pack Hallo gebruiker maakt, verwijderd HPC Pack nadat het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a58a0-170">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="a58a0-171">Hallo sleutels tooreduce beveiligingsrisico's, HPC Pack verwijdert na Taakvoltooiing van de.</span><span class="sxs-lookup"><span data-stu-id="a58a0-171">tooreduce security threats, HPC Pack removes hello keys after job completion.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="a58a0-172">Instellen van een bestandsshare voor Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="a58a0-172">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="a58a0-173">Nu een standaard SMB-share op een map op het hoofdknooppunt Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-173">Now set up a standard SMB share on a folder on hello head node.</span></span> <span data-ttu-id="a58a0-174">tooallow hello Linux knooppunten tooaccess toepassingsbestanden met een algemeen pad, koppelpunt Hallo gedeelde map op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-174">tooallow hello Linux nodes tooaccess application files with a common path, mount hello shared folder on hello Linux nodes.</span></span> <span data-ttu-id="a58a0-175">Als u wilt, kunt u een andere optie, zoals een Azure-bestanden share - aanbevolen voor veel scenario's- of een NFS-share voor bestandsdeling.</span><span class="sxs-lookup"><span data-stu-id="a58a0-175">If you want, you can use another file sharing option, such as an Azure Files share - recommended for many scenarios - or an NFS share.</span></span> <span data-ttu-id="a58a0-176">Zie Hallo-bestand delen van informatie en gedetailleerde stappen in [aan de slag met Linux-rekenknooppunten in een HPC Pack-Cluster in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="a58a0-176">See hello file sharing information and detailed steps in [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="a58a0-177">Maak een map op het hoofdknooppunt Hallo en tooEveryone delen door het instellen van machtigingen voor lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="a58a0-177">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="a58a0-178">Bijvoorbeeld C:\OpenFOAM delen op Hallo hoofdknooppunt als \\ \\SUSE12RDMA HN\OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="a58a0-178">For example, share C:\OpenFOAM on hello head node as \\\\SUSE12RDMA-HN\OpenFOAM.</span></span> <span data-ttu-id="a58a0-179">Hier *SUSE12RDMA HN* Hallo-hostnaam van Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-179">Here, *SUSE12RDMA-HN* is hello host name of hello head node.</span></span>
2. <span data-ttu-id="a58a0-180">Open een Windows PowerShell-venster en Voer Hallo volgende opdrachten uit:</span><span class="sxs-lookup"><span data-stu-id="a58a0-180">Open a Windows PowerShell window and run hello following commands:</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /openfoam
   
   clusrun /nodegroup:LinuxNodes mount -t cifs //SUSE12RDMA-HN/OpenFOAM /openfoam -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
   ```

<span data-ttu-id="a58a0-181">de eerste opdracht Hallo maakt een map met de naam /openfoam op alle knooppunten in Hallo LinuxNodes groep.</span><span class="sxs-lookup"><span data-stu-id="a58a0-181">hello first command creates a folder named /openfoam on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="a58a0-182">de tweede opdracht Hallo koppelt Hallo gedeelde map //SUSE12RDMA-HN/OpenFOAM op Hallo Linux-knooppunten met dir_mode en file_mode bits set too777.</span><span class="sxs-lookup"><span data-stu-id="a58a0-182">hello second command mounts hello shared folder //SUSE12RDMA-HN/OpenFOAM on hello Linux nodes with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="a58a0-183">Hallo *gebruikersnaam* en *wachtwoord* Hallo opdracht moet Hallo referenties van een gebruiker op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-183">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="a58a0-184">Hallo '\\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a58a0-184">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="a58a0-185">"\\`, 'betekent Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="a58a0-185">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="install-mpi-and-openfoam"></a><span data-ttu-id="a58a0-186">MPI en OpenFOAM installeren</span><span class="sxs-lookup"><span data-stu-id="a58a0-186">Install MPI and OpenFOAM</span></span>
<span data-ttu-id="a58a0-187">toorun OpenFOAM als een MPI-taak op Hallo RDMA netwerk, moet u toocompile OpenFOAM met Hallo Intel MPI-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-187">toorun OpenFOAM as an MPI job on hello RDMA network, you need toocompile OpenFOAM with hello Intel MPI libraries.</span></span> 

<span data-ttu-id="a58a0-188">Voer eerst enkele **clusrun** tooinstall Intel MPI-bibliotheken (indien nog niet is geïnstalleerd) en OpenFOAM opdrachten op uw Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-188">First, run several **clusrun** commands tooinstall Intel MPI libraries (if not already installed) and OpenFOAM on your Linux nodes.</span></span> <span data-ttu-id="a58a0-189">Gebruik Hallo hoofdknooppunt share geconfigureerde eerder tooshare Hallo installatiebestanden tussen Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-189">Use hello head node share configured previously tooshare hello installation files among hello Linux nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a58a0-190">Deze installatie en gecompileerd stappen zijn voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a58a0-190">These installation and compiling steps are examples.</span></span> <span data-ttu-id="a58a0-191">Moet u enige kennis van Linux-systeem beheer tooensure afhankelijke compilers en bibliotheken correct zijn geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-191">You need some knowledge of Linux system administration tooensure that dependent compilers and libraries are installed correctly.</span></span> <span data-ttu-id="a58a0-192">Mogelijk moet u toomodify bepaalde omgevingsvariabelen of andere instellingen voor uw versie van Intel MPI en OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="a58a0-192">You might need toomodify certain environment variables or other settings for your versions of Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="a58a0-193">Zie voor meer informatie [Intel MPI-bibliotheek voor Linux-installatiehandleiding](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) en [OpenFOAM bron Pack installatie](http://openfoam.org/download/2-3-1-source/) voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="a58a0-193">For details, see [Intel MPI Library for Linux Installation Guide](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html) and [OpenFOAM Source Pack Installation](http://openfoam.org/download/2-3-1-source/) for your environment.</span></span>
> 
> 

### <a name="install-intel-mpi"></a><span data-ttu-id="a58a0-194">Intel MPI installeren</span><span class="sxs-lookup"><span data-stu-id="a58a0-194">Install Intel MPI</span></span>
<span data-ttu-id="a58a0-195">Hallo gedownloade installatiepakket voor Intel MPI (l_mpi_p_5.0.3.048.tgz in dit voorbeeld) in C:\OpenFoam opslaan op Hallo hoofdknooppunt zodat Hallo Linux-knooppunten toegang dit bestand uit /openfoam tot.</span><span class="sxs-lookup"><span data-stu-id="a58a0-195">Save hello downloaded installation package for Intel MPI (l_mpi_p_5.0.3.048.tgz in this example) in C:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="a58a0-196">Voer **clusrun** tooinstall Intel MPI-bibliotheek op alle Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-196">Then run **clusrun** tooinstall Intel MPI library on all hello Linux nodes.</span></span>

1. <span data-ttu-id="a58a0-197">Hallo hieronder kopiëren Hallo installatiepakket voor de opdrachten en pakt te/opt/intel op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-197">hello following commands copy hello installation package and extract it too/opt/intel on each node.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/intel
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/l_mpi_p_5.0.3.048.tgz /opt/intel/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/intel/l_mpi_p_5.0.3.048.tgz -C /opt/intel/
   ```
2. <span data-ttu-id="a58a0-198">tooinstall Intel MPI-bibliotheek achtergrond, een silent.cfg-bestand gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-198">tooinstall Intel MPI Library silently, use a silent.cfg file.</span></span> <span data-ttu-id="a58a0-199">U kunt een voorbeeld vinden in Hallo voorbeeldbestanden aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a58a0-199">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="a58a0-200">Plaats dit bestand in Hallo gedeelde map /openfoam.</span><span class="sxs-lookup"><span data-stu-id="a58a0-200">Place this file in hello shared folder /openfoam.</span></span> <span data-ttu-id="a58a0-201">Zie voor meer informatie over Hallo silent.cfg bestand [Intel MPI-bibliotheek voor de installatiehandleiding voor Linux - installatie op de achtergrond](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span><span class="sxs-lookup"><span data-stu-id="a58a0-201">For details about hello silent.cfg file, see [Intel MPI Library for Linux Installation Guide - Silent Installation](http://registrationcenter-download.intel.com/akdlm/irc_nas/1718/INSTALL.html?lang=en&fileExt=.html#silentinstall).</span></span>
   
   > [!TIP]
   > <span data-ttu-id="a58a0-202">Zorg ervoor dat u uw silent.cfg bestand opslaan als een tekstbestand met Linux regeleinden heb (alleen LF, niet CR LF).</span><span class="sxs-lookup"><span data-stu-id="a58a0-202">Make sure that you save your silent.cfg file as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="a58a0-203">Deze stap zorgt ervoor dat deze goed op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-203">This step ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
3. <span data-ttu-id="a58a0-204">Intel MPI-bibliotheek in stille modus installeren.</span><span class="sxs-lookup"><span data-stu-id="a58a0-204">Install Intel MPI Library in silent mode.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes bash /opt/intel/l_mpi_p_5.0.3.048/install.sh --silent /openfoam/silent.cfg
   ```

### <a name="configure-mpi"></a><span data-ttu-id="a58a0-205">MPI configureren</span><span class="sxs-lookup"><span data-stu-id="a58a0-205">Configure MPI</span></span>
<span data-ttu-id="a58a0-206">Voor het testen, moet u de volgende regels toohello /etc/security/limits.conf op elke Linux-knooppunten Hallo Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a58a0-206">For testing, you should add hello following lines toohello /etc/security/limits.conf on each of hello Linux nodes:</span></span>

    clusrun /nodegroup:LinuxNodes echo "*               hard    memlock         unlimited" `>`> /etc/security/limits.conf
    clusrun /nodegroup:LinuxNodes echo "*               soft    memlock         unlimited" `>`> /etc/security/limits.conf


<span data-ttu-id="a58a0-207">Hallo Linux-knooppunten starten nadat u Hallo limits.conf bestand bijwerken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-207">Restart hello Linux nodes after you update hello limits.conf file.</span></span> <span data-ttu-id="a58a0-208">Bijvoorbeeld, gebruikt u Hallo volgende **clusrun** opdracht:</span><span class="sxs-lookup"><span data-stu-id="a58a0-208">For example, use hello following **clusrun** command:</span></span>

```
clusrun /nodegroup:LinuxNodes systemctl reboot
```

<span data-ttu-id="a58a0-209">Start opnieuw op en zorg ervoor dat die gedeelde map Hallo als /openfoam is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-209">After restarting, ensure that hello shared folder is mounted as /openfoam.</span></span>

### <a name="compile-and-install-openfoam"></a><span data-ttu-id="a58a0-210">Compileren en OpenFOAM installeren</span><span class="sxs-lookup"><span data-stu-id="a58a0-210">Compile and install OpenFOAM</span></span>
<span data-ttu-id="a58a0-211">Opslaan op het hoofdknooppunt Hallo Hallo gedownloade installatiepakket voor Hallo tooC:\OpenFoam OpenFOAM bron Pack (OpenFOAM-2.3.1.tgz in dit voorbeeld) zodat Hallo Linux-knooppunten toegang dit bestand uit /openfoam tot.</span><span class="sxs-lookup"><span data-stu-id="a58a0-211">Save hello downloaded installation package for hello OpenFOAM Source Pack (OpenFOAM-2.3.1.tgz in this example) tooC:\OpenFoam on hello head node so that hello Linux nodes can access this file from /openfoam.</span></span> <span data-ttu-id="a58a0-212">Voer **clusrun** opdrachten toocompile OpenFOAM op alle Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-212">Then run **clusrun** commands toocompile OpenFOAM on all hello Linux nodes.</span></span>

1. <span data-ttu-id="a58a0-213">Maak een map /opt/OpenFOAM op elk knooppunt Linux, kopie Hallo pakket toothis bronmap, en pak deze.</span><span class="sxs-lookup"><span data-stu-id="a58a0-213">Create a folder /opt/OpenFOAM on each Linux node, copy hello source package toothis folder, and extract it there.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes mkdir -p /opt/OpenFOAM
   
   clusrun /nodegroup:LinuxNodes cp /openfoam/OpenFOAM-2.3.1.tgz /opt/OpenFOAM/
   
   clusrun /nodegroup:LinuxNodes tar -xzf /opt/OpenFOAM/OpenFOAM-2.3.1.tgz -C /opt/OpenFOAM/
   ```
2. <span data-ttu-id="a58a0-214">toocompile OpenFOAM Hello Intel MPI-bibliotheek, Stel eerst enkele omgevingsvariabelen voor Intel MPI- en OpenFOAM.</span><span class="sxs-lookup"><span data-stu-id="a58a0-214">toocompile OpenFOAM with hello Intel MPI Library, first set up some environment variables for both Intel MPI and OpenFOAM.</span></span> <span data-ttu-id="a58a0-215">Een bash-script aangeroepen settings.sh tooset Hallo variabelen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-215">Use a bash script called settings.sh tooset hello variables.</span></span> <span data-ttu-id="a58a0-216">U kunt een voorbeeld vinden in Hallo voorbeeldbestanden aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a58a0-216">You can find an example in hello sample files at hello end of this article.</span></span> <span data-ttu-id="a58a0-217">Plaats dit bestand (opgeslagen met regeleinden Linux) in Hallo gedeelde map /openfoam.</span><span class="sxs-lookup"><span data-stu-id="a58a0-217">Place this file (saved with Linux line endings) in hello shared folder /openfoam.</span></span> <span data-ttu-id="a58a0-218">Dit bestand bevat ook de instellingen voor Hallo MPI en OpenFOAM runtimes hoger toorun een taak OpenFOAM te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-218">This file also contains settings for hello MPI and OpenFOAM runtimes that you use later toorun an OpenFOAM job.</span></span>
3. <span data-ttu-id="a58a0-219">Afhankelijke pakketten nodig toocompile OpenFOAM installeren.</span><span class="sxs-lookup"><span data-stu-id="a58a0-219">Install dependent packages needed toocompile OpenFOAM.</span></span> <span data-ttu-id="a58a0-220">Afhankelijk van uw Linux-distributie moet u mogelijk eerst tooadd een opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a58a0-220">Depending on your Linux distribution, you might first need tooadd a repository.</span></span> <span data-ttu-id="a58a0-221">Voer **clusrun** vergelijkbare toohello volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="a58a0-221">Run **clusrun** commands similar toohello following:</span></span>
   
    ```
    clusrun /nodegroup:LinuxNodes zypper ar http://download.opensuse.org/distribution/13.2/repo/oss/suse/ opensuse
   
    clusrun /nodegroup:LinuxNodes zypper -n --gpg-auto-import-keys install --repo opensuse --force-resolution -t pattern devel_C_C++
    ```
   
    <span data-ttu-id="a58a0-222">Indien nodig, opdrachten SSH tooeach Linux knooppunt toorun hello tooconfirm die ze naar behoren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-222">If necessary, SSH tooeach Linux node toorun hello commands tooconfirm that they run properly.</span></span>
4. <span data-ttu-id="a58a0-223">Hallo na de opdracht toocompile OpenFOAM worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-223">Run hello following command toocompile OpenFOAM.</span></span> <span data-ttu-id="a58a0-224">Hallo compilatie proces neemt enige tijd toocomplete en genereert een grote hoeveelheid logboekuitvoer informatie toostandard, gebruikt u dus Hallo **/ interleaved** toodisplay Hallo uitvoer interleaved optie.</span><span class="sxs-lookup"><span data-stu-id="a58a0-224">hello compilation process takes some time toocomplete and generates a large amount of log information toostandard output, so use hello **/interleaved** option toodisplay hello output interleaved.</span></span>
   
   ```
   clusrun /nodegroup:LinuxNodes /interleaved source /openfoam/settings.sh `&`& /opt/OpenFOAM/OpenFOAM-2.3.1/Allwmake
   ```
   
   > [!NOTE]
   > <span data-ttu-id="a58a0-225">Hallo '\\`' symbool in Hallo-opdracht is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a58a0-225">hello “\\`” symbol in hello command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="a58a0-226">"\\`&" betekent Hallo "&" deel uitmaakt van het Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="a58a0-226">“\\`&” means hello “&” is a part of hello command.</span></span>
   > 
   > 

## <a name="prepare-toorun-an-openfoam-job"></a><span data-ttu-id="a58a0-227">Een taak OpenFOAM voor toorun voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a58a0-227">Prepare toorun an OpenFOAM job</span></span>
<span data-ttu-id="a58a0-228">Nu get gereed toorun een MPI-taak aangeroepen sloshingTank3D, namelijk een Hallo OpenFoam steekproeven van op twee Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-228">Now get ready toorun an MPI job called sloshingTank3D, which is one of hello OpenFoam samples, on two Linux nodes.</span></span> 

### <a name="set-up-hello-runtime-environment"></a><span data-ttu-id="a58a0-229">Hallo-runtime-omgeving instellen</span><span class="sxs-lookup"><span data-stu-id="a58a0-229">Set up hello runtime environment</span></span>
<span data-ttu-id="a58a0-230">tooset hello runtime-omgevingen voor MPI en OpenFOAM op Hallo Linux-knooppunten, uitvoeren van de volgende opdracht in een Windows PowerShell-venster op het hoofdknooppunt Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58a0-230">tooset up hello runtime environments for MPI and OpenFOAM on hello Linux nodes, run hello following command in a Windows PowerShell window on hello head node.</span></span> <span data-ttu-id="a58a0-231">(Deze opdracht is alleen geldig voor SUSE Linux.)</span><span class="sxs-lookup"><span data-stu-id="a58a0-231">(This command is valid for SUSE Linux only.)</span></span>

```
clusrun /nodegroup:LinuxNodes cp /openfoam/settings.sh /etc/profile.d/
```

### <a name="prepare-sample-data"></a><span data-ttu-id="a58a0-232">Voorbeeldgegevens voorbereiden</span><span class="sxs-lookup"><span data-stu-id="a58a0-232">Prepare sample data</span></span>
<span data-ttu-id="a58a0-233">Gebruik Hallo hoofdknooppunt share u eerder hebt geconfigureerd tooshare bestanden tussen Hallo Linux-knooppunten (gekoppeld als /openfoam).</span><span class="sxs-lookup"><span data-stu-id="a58a0-233">Use hello head node share you configured previously tooshare files among hello Linux nodes (mounted as /openfoam).</span></span>

1. <span data-ttu-id="a58a0-234">SSH-tooone van uw Linux-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-234">SSH tooone of your Linux compute nodes.</span></span>
2. <span data-ttu-id="a58a0-235">Hallo na de opdracht tooset hello OpenFOAM runtime-omgeving worden uitgevoerd als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="a58a0-235">Run hello following command tooset up hello OpenFOAM runtime environment, if you haven’t already done this.</span></span>
   
   ```
   $ source /openfoam/settings.sh
   ```
3. <span data-ttu-id="a58a0-236">Hallo sloshingTank3D voorbeeld toohello gedeelde mappen kopiëren en navigeer tooit.</span><span class="sxs-lookup"><span data-stu-id="a58a0-236">Copy hello sloshingTank3D sample toohello shared folder and navigate tooit.</span></span>
   
   ```
   $ cp -r $FOAM_TUTORIALS/multiphase/interDyMFoam/ras/sloshingTank3D /openfoam/
   
   $ cd /openfoam/sloshingTank3D
   ```
4. <span data-ttu-id="a58a0-237">Wanneer u de standaardparameters Hallo van dit voorbeeld gebruikt, kan duren tien minuten toorun, zodat u toomodify kunt sommige parameters toomake het sneller worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-237">When you use hello default parameters of this sample, it can take tens of minutes toorun, so you might want toomodify some parameters toomake it run faster.</span></span> <span data-ttu-id="a58a0-238">Een eenvoudige keuze is toomodify Hallo tijd stap variabelen deltaT en writeInterval in Hallo system/controlDict-bestand.</span><span class="sxs-lookup"><span data-stu-id="a58a0-238">One simple choice is toomodify hello time step variables deltaT and writeInterval in hello system/controlDict file.</span></span> <span data-ttu-id="a58a0-239">Dit bestand wordt alle ingevoerde gegevens betreffende toohello besturingselement van het tijd- en lezen en schrijven van oplossingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="a58a0-239">This file stores all input data relating toohello control of time and reading and writing solution data.</span></span> <span data-ttu-id="a58a0-240">U kan bijvoorbeeld Hallo-waarde van deltaT van 0,05 too0.5 en Hallo-waarde van writeInterval van 0,05 too0.5 wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-240">For example, you could change hello value of deltaT from 0.05 too0.5 and hello value of writeInterval from 0.05 too0.5.</span></span>
   
   ![Wijzig de variabelen in stap][step_variables]
5. <span data-ttu-id="a58a0-242">Gewenste waarden voor Hallo variabelen in Hallo system/decomposeParDict bestand opgeven.</span><span class="sxs-lookup"><span data-stu-id="a58a0-242">Specify desired values for hello variables in hello system/decomposeParDict file.</span></span> <span data-ttu-id="a58a0-243">In dit voorbeeld worden twee Linux knooppunten, elk met 8 kernen, dus Stel numberOfSubdomains too16 en n van hierarchicalCoeffs too(1 1 16), wat betekent dat OpenFOAM parallel met 16 processen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-243">This example uses two Linux nodes each with 8 cores, so set numberOfSubdomains too16 and n of hierarchicalCoeffs too(1 1 16), which means run OpenFOAM in parallel with 16 processes.</span></span> <span data-ttu-id="a58a0-244">Zie voor meer informatie [OpenFOAM User Guide: 3,4 uitgevoerd toepassingen parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span><span class="sxs-lookup"><span data-stu-id="a58a0-244">For more information, see [OpenFOAM User Guide: 3.4 Running applications in parallel](http://cfd.direct/openfoam/user-guide/running-applications-parallel/#x12-820003.4).</span></span>
   
   ![Processen afbreken][decompose]
6. <span data-ttu-id="a58a0-246">Hallo volgende opdrachten uit Hallo sloshingTank3D directory tooprepare Hallo voorbeeldgegevens worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-246">Run hello following commands from hello sloshingTank3D directory tooprepare hello sample data.</span></span>
   
   ```
   $ . $WM_PROJECT_DIR/bin/tools/RunFunctions
   
   $ m4 constant/polyMesh/blockMeshDict.m4 > constant/polyMesh/blockMeshDict
   
   $ runApplication blockMesh
   
   $ cp 0/alpha.water.org 0/alpha.water
   
   $ runApplication setFields  
   ```
7. <span data-ttu-id="a58a0-247">Op het hoofdknooppunt hello ziet u bestanden met voorbeeldgegevens Hallo worden gekopieerd naar C:\OpenFoam\sloshingTank3D.</span><span class="sxs-lookup"><span data-stu-id="a58a0-247">On hello head node, you should see hello sample data files are copied into C:\OpenFoam\sloshingTank3D.</span></span> <span data-ttu-id="a58a0-248">(C:\OpenFoam is Hallo gedeelde map op het hoofdknooppunt Hallo.)</span><span class="sxs-lookup"><span data-stu-id="a58a0-248">(C:\OpenFoam is hello shared folder on hello head node.)</span></span>
   
   ![Gegevensbestanden op Hallo hoofdknooppunt][data_files]

### <a name="host-file-for-mpirun"></a><span data-ttu-id="a58a0-250">Hostbestand voor mpirun</span><span class="sxs-lookup"><span data-stu-id="a58a0-250">Host file for mpirun</span></span>
<span data-ttu-id="a58a0-251">In deze stap maakt u een hostbestand (een lijst van rekenknooppunten) welke Hallo **mpirun** opdracht gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-251">In this step, you create a host file (a list of compute nodes) which hello **mpirun** command uses.</span></span>

1. <span data-ttu-id="a58a0-252">Op een van de Linux-knooppunten hello, door een bestand met de naam hostfile onder /openfoam, zodat dit bestand kan worden bereikt op /openfoam/hostfile op alle knooppunten van Linux te maken.</span><span class="sxs-lookup"><span data-stu-id="a58a0-252">On one of hello Linux nodes, create a file named hostfile under /openfoam, so this file can be reached at /openfoam/hostfile on all Linux nodes.</span></span>
2. <span data-ttu-id="a58a0-253">Schrijf uw Linux-knooppuntnamen in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="a58a0-253">Write your Linux node names into this file.</span></span> <span data-ttu-id="a58a0-254">In dit voorbeeld bevat Hallo bestand Hallo namen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a58a0-254">In this example, hello file contains hello following names:</span></span>
   
   ```       
   SUSE12RDMA-LN1
   SUSE12RDMA-LN2
   ```
   
   > [!TIP]
   > <span data-ttu-id="a58a0-255">U kunt ook dit bestand maken op C:\OpenFoam\hostfile op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-255">You can also create this file at C:\OpenFoam\hostfile on hello head node.</span></span> <span data-ttu-id="a58a0-256">Als u deze optie kiest, opslaan als een tekstbestand met Linux regeleinden (alleen LF, niet CR LF).</span><span class="sxs-lookup"><span data-stu-id="a58a0-256">If you choose this option, save it as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="a58a0-257">Dit zorgt ervoor dat deze wordt uitgevoerd naar behoren op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-257">This ensures that it runs properly on hello Linux nodes.</span></span>
   > 
   > 
   
   <span data-ttu-id="a58a0-258">**Wrapper voor Bash-scripts**</span><span class="sxs-lookup"><span data-stu-id="a58a0-258">**Bash script wrapper**</span></span>
   
   <span data-ttu-id="a58a0-259">Als u veel Linux-knooppunten hebt en u wilt dat uw taak toorun op slechts een deel ervan, kan niet een goed idee toouse-bestand een vaste host, omdat u niet weet welke knooppunten tooyour taak worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-259">If you have many Linux nodes and you want your job toorun on only some of them, it’s not a good idea toouse a fixed host file, because you don’t know which nodes will be allocated tooyour job.</span></span> <span data-ttu-id="a58a0-260">In dit geval een bash script wrapper voor schrijven **mpirun** toocreate Hallo hostbestand automatisch.</span><span class="sxs-lookup"><span data-stu-id="a58a0-260">In this case, write a bash script wrapper for **mpirun** toocreate hello host file automatically.</span></span> <span data-ttu-id="a58a0-261">U kunt een voorbeeld bash script wrapper aangeroepen hpcimpirun.sh aan Hallo einde van dit artikel vinden en opslaan als /openfoam/hpcimpirun.sh. Dit voorbeeldscript Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="a58a0-261">You can find an example bash script wrapper called hpcimpirun.sh at hello end of this article, and save it as /openfoam/hpcimpirun.sh. This example script does hello following:</span></span>
   
   1. <span data-ttu-id="a58a0-262">Stelt de omgevingsvariabelen Hallo voor **mpirun**, en sommige toevoeging opdracht parameters toorun Hallo MPI-taak via Hallo RDMA-netwerk.</span><span class="sxs-lookup"><span data-stu-id="a58a0-262">Sets up hello environment variables for **mpirun**, and some addition command parameters toorun hello MPI job through hello RDMA network.</span></span> <span data-ttu-id="a58a0-263">In dit geval stelt het Hallo variabelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a58a0-263">In this case, it sets hello following variables:</span></span>
      
      * <span data-ttu-id="a58a0-264">I_MPI_FABRICS shm:dapl =</span><span class="sxs-lookup"><span data-stu-id="a58a0-264">I_MPI_FABRICS=shm:dapl</span></span>
      * <span data-ttu-id="a58a0-265">I_MPI_DAPL_PROVIDER weergeeft van een-v2-ib0 =</span><span class="sxs-lookup"><span data-stu-id="a58a0-265">I_MPI_DAPL_PROVIDER=ofa-v2-ib0</span></span>
      * <span data-ttu-id="a58a0-266">I_MPI_DYNAMIC_CONNECTION = 0</span><span class="sxs-lookup"><span data-stu-id="a58a0-266">I_MPI_DYNAMIC_CONNECTION=0</span></span>
   2. <span data-ttu-id="a58a0-267">Maakt een hostbestand toohello op basis van de variabele $ omgeving CCP_NODES_CORES die is ingesteld door Hallo HPC-hoofdknooppunt wanneer Hallo-taak wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-267">Creates a host file according toohello environment variable $CCP_NODES_CORES, which is set by hello HPC head node when hello job is activated.</span></span>
      
      <span data-ttu-id="a58a0-268">Hallo-indeling van $CCP_NODES_CORES volgt dit patroon:</span><span class="sxs-lookup"><span data-stu-id="a58a0-268">hello format of $CCP_NODES_CORES follows this pattern:</span></span>
      
      ```
      <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>...`
      ```
      
      <span data-ttu-id="a58a0-269">waar</span><span class="sxs-lookup"><span data-stu-id="a58a0-269">where</span></span>
      
      * <span data-ttu-id="a58a0-270">`<Number of nodes>`-het aantal knooppunten Hallo toothis taak toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-270">`<Number of nodes>` - hello number of nodes allocated toothis job.</span></span>  
      * <span data-ttu-id="a58a0-271">`<Name of node_n_...>`-Hallo-naam van elk knooppunt toegewezen toothis taak.</span><span class="sxs-lookup"><span data-stu-id="a58a0-271">`<Name of node_n_...>` - hello name of each node allocated toothis job.</span></span>
      * <span data-ttu-id="a58a0-272">`<Cores of node_n_...>`-het aantal kernen op Hallo knooppunt toegewezen toothis taak Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58a0-272">`<Cores of node_n_...>` - hello number of cores on hello node allocated toothis job.</span></span>
      
      <span data-ttu-id="a58a0-273">Bijvoorbeeld, als Hallo-taak twee knooppunten toorun moet, is $CCP_NODES_CORES vergelijkbaar met</span><span class="sxs-lookup"><span data-stu-id="a58a0-273">For example, if hello job needs two nodes toorun, $CCP_NODES_CORES is similar to</span></span>
      
      ```
      2 SUSE12RDMA-LN1 8 SUSE12RDMA-LN2 8
      ```
   3. <span data-ttu-id="a58a0-274">Aanroepen Hallo **mpirun** opdracht en voegt u twee parameters toohello vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="a58a0-274">Calls hello **mpirun** command and appends two parameters toohello command line.</span></span>
      
      * <span data-ttu-id="a58a0-275">`--hostfile <hostfilepath>: <hostfilepath>`-Hallo pad van Hallo host bestand Hallo script wordt gemaakt</span><span class="sxs-lookup"><span data-stu-id="a58a0-275">`--hostfile <hostfilepath>: <hostfilepath>` - hello path of hello host file hello script creates</span></span>
      * <span data-ttu-id="a58a0-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}`-een omgevingsvariabele ingesteld door Hallo HPC Pack hoofdknooppunt, die het aantal totale kernen Hallo opslaat toothis taak toegewezen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-276">`-np ${CCP_NUMCPUS}: ${CCP_NUMCPUS}` - an environment variable set by hello HPC Pack head node, which stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="a58a0-277">In dit geval geeft Hallo processen voor het aantal **mpirun**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-277">In this case, it specifies hello number of processes for **mpirun**.</span></span>

## <a name="submit-an-openfoam-job"></a><span data-ttu-id="a58a0-278">Verzenden van een taak OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="a58a0-278">Submit an OpenFOAM job</span></span>
<span data-ttu-id="a58a0-279">U kunt nu een taak in HPC Cluster Manager verzenden.</span><span class="sxs-lookup"><span data-stu-id="a58a0-279">Now you can submit a job in HPC Cluster Manager.</span></span> <span data-ttu-id="a58a0-280">U moet toopass Hallo script hpcimpirun.sh in Hallo opdrachtregels voor een aantal taken Hallo.</span><span class="sxs-lookup"><span data-stu-id="a58a0-280">You need toopass hello script hpcimpirun.sh in hello command lines for some of hello job tasks.</span></span>

1. <span data-ttu-id="a58a0-281">Verbinding maken met hoofdknooppunt tooyour-cluster en start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="a58a0-281">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="a58a0-282">**In de Resource Management**, moet u ervoor zorgen dat Hallo Linux-rekenknooppunten hello **Online** status.</span><span class="sxs-lookup"><span data-stu-id="a58a0-282">**In Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="a58a0-283">Als dat niet het geval is, selecteert u deze en klikt u op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-283">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="a58a0-284">In **Jobbeheer**, klikt u op **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-284">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="a58a0-285">Voer een naam voor de taak zoals *sloshingTank3D*.</span><span class="sxs-lookup"><span data-stu-id="a58a0-285">Enter a name for job such as *sloshingTank3D*.</span></span>
   
   ![Taakdetails][job_details]
5. <span data-ttu-id="a58a0-287">In **taak resources**, kies het type resource als 'Knooppunt' Hallo en Hallo Minimum too2 ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-287">In **Job resources**, choose hello type of resource as “Node” and set hello Minimum too2.</span></span> <span data-ttu-id="a58a0-288">Deze configuratie Hallo-taak op twee Linux-knooppunten, elk met acht kernen in dit voorbeeld heeft wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-288">This configuration runs hello job on two Linux nodes, each of which has eight cores in this example.</span></span>
   
   ![Taak resources][job_resources]
6. <span data-ttu-id="a58a0-290">Klik op **taken bewerken** in Hallo navigatiebalk aan de linkerkant en klik vervolgens op **toevoegen** tooadd een taak toohello taak.</span><span class="sxs-lookup"><span data-stu-id="a58a0-290">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span> <span data-ttu-id="a58a0-291">Vier taken toohello taak met de Hallo toevoegen na de opdracht regels en instellingen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-291">Add four tasks toohello job with hello following command lines and settings.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a58a0-292">Met `source /openfoam/settings.sh` stelt Hallo OpenFOAM en MPI-runtime-omgevingen, zodat elk van de taken te volgen Hallo voordat Hallo OpenFOAM opdracht aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-292">Running `source /openfoam/settings.sh` sets up hello OpenFOAM and MPI runtime environments, so each of hello following tasks calls it before hello OpenFOAM command.</span></span>
   > 
   > 
   
   * <span data-ttu-id="a58a0-293">**Taak 1**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-293">**Task 1**.</span></span> <span data-ttu-id="a58a0-294">Voer **decomposePar** toogenerate gegevensbestanden worden opgeslagen voor het werken met **interDyMFoam** parallel.</span><span class="sxs-lookup"><span data-stu-id="a58a0-294">Run **decomposePar** toogenerate data files for running **interDyMFoam** in parallel.</span></span>
     
     * <span data-ttu-id="a58a0-295">Een knooppunt toohello taak toewijzen</span><span class="sxs-lookup"><span data-stu-id="a58a0-295">Assign one node toohello task</span></span>
     * <span data-ttu-id="a58a0-296">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="a58a0-296">**Command line** - `source /openfoam/settings.sh && decomposePar -force > /openfoam/decomposePar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="a58a0-297">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="a58a0-297">**Working directory** - /openfoam/sloshingTank3D</span></span>
     
     <span data-ttu-id="a58a0-298">Zie Hallo volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="a58a0-298">See hello following figure.</span></span> <span data-ttu-id="a58a0-299">U configureren de resterende taken Hallo op dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="a58a0-299">You configure hello remaining tasks similarly.</span></span>
     
     ![Taak 1-details][task_details1]
   * <span data-ttu-id="a58a0-301">**Taak 2**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-301">**Task 2**.</span></span> <span data-ttu-id="a58a0-302">Voer **interDyMFoam** in parallelle toocompute Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-302">Run **interDyMFoam** in parallel toocompute hello sample.</span></span>
     
     * <span data-ttu-id="a58a0-303">Twee knooppunten toohello taak toewijzen</span><span class="sxs-lookup"><span data-stu-id="a58a0-303">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="a58a0-304">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="a58a0-304">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh interDyMFoam -parallel > /openfoam/interDyMFoam${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="a58a0-305">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="a58a0-305">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="a58a0-306">**Taak 3**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-306">**Task 3**.</span></span> <span data-ttu-id="a58a0-307">Voer **reconstructPar** toomerge Hallo wordt ingesteld met mappen van de tijd van elke map processor_N_ in één verzameling.</span><span class="sxs-lookup"><span data-stu-id="a58a0-307">Run **reconstructPar** toomerge hello sets of time directories from each processor_N_ directory into a single set.</span></span>
     
     * <span data-ttu-id="a58a0-308">Een knooppunt toohello taak toewijzen</span><span class="sxs-lookup"><span data-stu-id="a58a0-308">Assign one node toohello task</span></span>
     * <span data-ttu-id="a58a0-309">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="a58a0-309">**Command line** - `source /openfoam/settings.sh && reconstructPar > /openfoam/reconstructPar${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="a58a0-310">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="a58a0-310">**Working directory** - /openfoam/sloshingTank3D</span></span>
   * <span data-ttu-id="a58a0-311">**Taak 4**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-311">**Task 4**.</span></span> <span data-ttu-id="a58a0-312">Voer **foamToEnsight** in parallelle tooconvert hello OpenFOAM resultaat bestanden naar EnSight formatteren en Hallo EnSight bestanden in een map met de naam Ensight in case directory Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-312">Run **foamToEnsight** in parallel tooconvert hello OpenFOAM result files into EnSight format and place hello EnSight files in a directory named Ensight in hello case directory.</span></span>
     
     * <span data-ttu-id="a58a0-313">Twee knooppunten toohello taak toewijzen</span><span class="sxs-lookup"><span data-stu-id="a58a0-313">Assign two nodes toohello task</span></span>
     * <span data-ttu-id="a58a0-314">**Vanaf de opdrachtregel** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span><span class="sxs-lookup"><span data-stu-id="a58a0-314">**Command line** - `source /openfoam/settings.sh && /openfoam/hpcimpirun.sh foamToEnsight -parallel > /openfoam/foamToEnsight${CCP_JOBID}.log`</span></span>
     * <span data-ttu-id="a58a0-315">**Werkmap** -/ openfoam/sloshingTank3D</span><span class="sxs-lookup"><span data-stu-id="a58a0-315">**Working directory** - /openfoam/sloshingTank3D</span></span>
7. <span data-ttu-id="a58a0-316">Afhankelijkheden toothese taken in oplopende taakvolgorde toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a58a0-316">Add dependencies toothese tasks in ascending task order.</span></span>
   
   ![Taakafhankelijkheden][task_dependencies]
8. <span data-ttu-id="a58a0-318">Klik op **indienen** toorun deze taak.</span><span class="sxs-lookup"><span data-stu-id="a58a0-318">Click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="a58a0-319">Standaard verzendt HPC Pack Hallo taak als uw huidige aangemelde gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="a58a0-319">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="a58a0-320">Nadat u op **indienen**, ziet u mogelijk een dialoogvenster waarin u tooenter Hallo-gebruikersnaam en wachtwoord wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="a58a0-320">After you click **Submit**, you might see a dialog box prompting you tooenter hello user name and password.</span></span>
   
   ![Taak referenties][creds]
   
   <span data-ttu-id="a58a0-322">Onder bepaalde omstandigheden onthoudt HPC Pack Hallo gebruikersgegevens u invoer voordat en dit dialoogvenster niet weergeven.</span><span class="sxs-lookup"><span data-stu-id="a58a0-322">Under some conditions, HPC Pack remembers hello user information you input before and doesn’t show this dialog box.</span></span> <span data-ttu-id="a58a0-323">toomake HPC Pack opnieuw weergeven, voer de volgende opdracht achter de opdrachtprompt Hallo en vervolgens dient Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="a58a0-323">toomake HPC Pack show it again, enter hello following command at a Command prompt and then submit hello job.</span></span>
   
   ```
   hpccred delcreds
   ```
9. <span data-ttu-id="a58a0-324">Hallo taak neemt van tien minuten tooseveral uur volgens toohello parameters die u hebt ingesteld voor het Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a58a0-324">hello job takes from tens of minutes tooseveral hours according toohello parameters you have set for hello sample.</span></span> <span data-ttu-id="a58a0-325">U ziet in heatmap hello, Hallo-taak uitgevoerd op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="a58a0-325">In hello heat map, you see hello job running on hello Linux nodes.</span></span> 
   
   ![Heatmap][heat_map]
   
   <span data-ttu-id="a58a0-327">Op elk knooppunt worden acht processen gestart.</span><span class="sxs-lookup"><span data-stu-id="a58a0-327">On each node, eight processes are started.</span></span>
   
   ![Linux-processen][linux_processes]
10. <span data-ttu-id="a58a0-329">Wanneer het Hallo-taak is voltooid, kunt u de Hallo taak resultaten vinden in mappen onder C:\OpenFoam\sloshingTank3D en Hallo-logboekbestanden op C:\OpenFoam.</span><span class="sxs-lookup"><span data-stu-id="a58a0-329">When hello job finishes, find hello job results in folders under C:\OpenFoam\sloshingTank3D, and hello log files at C:\OpenFoam.</span></span>

## <a name="view-results-in-ensight"></a><span data-ttu-id="a58a0-330">De resultaten weergeven in EnSight</span><span class="sxs-lookup"><span data-stu-id="a58a0-330">View results in EnSight</span></span>
<span data-ttu-id="a58a0-331">Optioneel gebruik [EnSight](https://www.ceisoftware.com/) toovisualize en analyseer de resultaten Hallo van Hallo OpenFOAM taak.</span><span class="sxs-lookup"><span data-stu-id="a58a0-331">Optionally use [EnSight](https://www.ceisoftware.com/) toovisualize and analyze hello results of hello OpenFOAM job.</span></span> <span data-ttu-id="a58a0-332">Zie voor meer informatie over visualisatie en animatie in EnSight, [video handleiding](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span><span class="sxs-lookup"><span data-stu-id="a58a0-332">For more about visualization and animation in EnSight, see this [video guide](http://www.ceisoftware.com/wp-content/uploads/screencasts/vof_visualization/vof_visualization.html).</span></span>

1. <span data-ttu-id="a58a0-333">Nadat u op het hoofdknooppunt Hallo EnSight hebt geïnstalleerd, start u deze.</span><span class="sxs-lookup"><span data-stu-id="a58a0-333">After you install EnSight on hello head node, start it.</span></span>
2. <span data-ttu-id="a58a0-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span><span class="sxs-lookup"><span data-stu-id="a58a0-334">Open C:\OpenFoam\sloshingTank3D\EnSight\sloshingTank3D.case.</span></span>
   
   <span data-ttu-id="a58a0-335">U ziet een vervangen in Hallo-viewer.</span><span class="sxs-lookup"><span data-stu-id="a58a0-335">You see a tank in hello viewer.</span></span>
   
   ![Vervangen in EnSight][tank]
3. <span data-ttu-id="a58a0-337">Maak een **Isosurface** van **internalMesh**, en kies vervolgens Hallo variabele **alpha_water**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-337">Create an **Isosurface** from **internalMesh**, and then choose hello variable **alpha_water**.</span></span>
   
   ![Een isosurface maken][isosurface]
4. <span data-ttu-id="a58a0-339">Hallo voor kleur instellen **Isosurface_part** in de vorige stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-339">Set hello color for **Isosurface_part** created in hello previous step.</span></span> <span data-ttu-id="a58a0-340">Zo ingesteld dat deze toowater blauw.</span><span class="sxs-lookup"><span data-stu-id="a58a0-340">For example, set it toowater blue.</span></span>
   
   ![Isosurface kleur bewerken][isosurface_color]
5. <span data-ttu-id="a58a0-342">Maak een **Iso-volume** van **wanden** door te selecteren **wanden** in Hallo **delen** paneel en klik op Hallo **Isosurfaces**  knop op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="a58a0-342">Create an **Iso-volume** from **walls** by selecting **walls** in hello **Parts** panel and click hello **Isosurfaces** button in hello toolbar.</span></span>
6. <span data-ttu-id="a58a0-343">Selecteer in het dialoogvenster Hallo **Type** als **Isovolume** en stel Hallo Min van **Isovolume bereik** too0.5.</span><span class="sxs-lookup"><span data-stu-id="a58a0-343">In hello dialog box, select **Type** as **Isovolume** and set hello Min of **Isovolume range** too0.5.</span></span> <span data-ttu-id="a58a0-344">toocreate isovolume hello, klikt u op **maken met de geselecteerde onderdelen**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-344">toocreate hello isovolume, click **Create with selected parts**.</span></span>
7. <span data-ttu-id="a58a0-345">Hallo voor kleur instellen **Iso_volume_part** in de vorige stap Hallo gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a58a0-345">Set hello color for **Iso_volume_part** created in hello previous step.</span></span> <span data-ttu-id="a58a0-346">Zo ingesteld dat deze toodeep water blauw.</span><span class="sxs-lookup"><span data-stu-id="a58a0-346">For example, set it toodeep water blue.</span></span>
8. <span data-ttu-id="a58a0-347">Hallo voor kleur instellen **wanden**.</span><span class="sxs-lookup"><span data-stu-id="a58a0-347">Set hello color for **walls**.</span></span> <span data-ttu-id="a58a0-348">Zo ingesteld dat deze tootransparent wit.</span><span class="sxs-lookup"><span data-stu-id="a58a0-348">For example, set it tootransparent white.</span></span>
9. <span data-ttu-id="a58a0-349">Klik nu op **afspelen** toosee Hallo resultaten van Hallo simulatie.</span><span class="sxs-lookup"><span data-stu-id="a58a0-349">Now click **Play** toosee hello results of hello simulation.</span></span>
   
    ![Resultaat van de vervangen][tank_result]

## <a name="sample-files"></a><span data-ttu-id="a58a0-351">Voorbeeldbestanden</span><span class="sxs-lookup"><span data-stu-id="a58a0-351">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="a58a0-352">Voorbeeld XML-configuratiebestand voor implementatie van het cluster door PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="a58a0-352">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
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

### <a name="sample-credxml-file"></a><span data-ttu-id="a58a0-353">Voorbeeldbestand cred.xml</span><span class="sxs-lookup"><span data-stu-id="a58a0-353">Sample cred.xml file</span></span>
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
### <a name="sample-silentcfg-file-tooinstall-mpi"></a><span data-ttu-id="a58a0-354">Voorbeeld silent.cfg bestand tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="a58a0-354">Sample silent.cfg file tooinstall MPI</span></span>
```
# Patterns used toocheck silent configuration file
#
# anythingpat - any string
# filepat     - hello file location pattern (/file/location/to/license.lic)
# lspat       - hello license server address pattern (0123@hostname)
# snpat       - hello serial number pattern (ABCD-01234567)

# accept EULA, valid values are: {accept, decline}
ACCEPT_EULA=accept

# optional error behavior, valid values are: {yes, no}
CONTINUE_WITH_OPTIONAL_ERROR=yes

# install location, valid values are: {/opt/intel, filepat}
PSET_INSTALL_DIR=/opt/intel

# continue with overwrite of existing installation directory, valid values are: {yes, no}
CONTINUE_WITH_INSTALLDIR_OVERWRITE=yes

# list of components tooinstall, valid values are: {ALL, DEFAULTS, anythingpat}
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

# Path toohello cluster description file, valid values are: {filepat}
#CLUSTER_INSTALL_MACHINES_FILE=filepat

# Intel(R) Software Improvement Program opt-in, valid values are: {yes, no}
PHONEHOME_SEND_USAGE_DATA=no

# Perform validation of digital signatures of RPM files, valid values are: {yes, no}
SIGNING_ENABLED=yes

# Select yes tooenable mpi-selector integration, valid values are: {yes, no}
ENVIRONMENT_REG_MPI_ENV=no

# Select yes tooupdate ld.so.conf, valid values are: {yes, no}
ENVIRONMENT_LD_SO_CONF=no


```

### <a name="sample-settingssh-script"></a><span data-ttu-id="a58a0-355">Voorbeeldscript settings.sh</span><span class="sxs-lookup"><span data-stu-id="a58a0-355">Sample settings.sh script</span></span>
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


### <a name="sample-hpcimpirunsh-script"></a><span data-ttu-id="a58a0-356">Voorbeeldscript hpcimpirun.sh</span><span class="sxs-lookup"><span data-stu-id="a58a0-356">Sample hpcimpirun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
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
    # CCP_NODES_CORES is not found or is empty, just run hello mpirun without hostfile arg.
    ${MPIRUN} $*
else
    # Create hello hostfile file
    NODELIST_PATH=${SCRIPT_PATH}/hostfile_$$

    # Get every node name and write into hello hostfile file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "${NODESCORES[${I}]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello mpirun with hostfile arg
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

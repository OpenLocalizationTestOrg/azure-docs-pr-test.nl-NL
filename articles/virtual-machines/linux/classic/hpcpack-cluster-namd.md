---
title: aaaNAMD met Microsoft HPC Pack op de virtuele Linux-machines | Microsoft Docs
description: Een Microsoft HPC Pack cluster in Azure implementeren en uitvoeren van een simulatie NAMD met charmrun op meerdere rekenknooppunten voor Linux
services: virtual-machines-linux
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager,hpc-pack
ms.assetid: 76072c6b-ac35-4729-ba67-0d16f9443bd7
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: big-compute
ms.date: 10/13/2016
ms.author: danlep
ms.openlocfilehash: 90c722f66b494335a62c0613079366ae99002076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-namd-with-microsoft-hpc-pack-on-linux-compute-nodes-in-azure"></a><span data-ttu-id="6a643-103">NAMD uitvoeren met Microsoft HPC Pack op Linux-rekenknooppunten in Azure</span><span class="sxs-lookup"><span data-stu-id="6a643-103">Run NAMD with Microsoft HPC Pack on Linux compute nodes in Azure</span></span>
<span data-ttu-id="6a643-104">Dit artikel ziet u enkele toorun een werkbelasting Linux high performance computing (HPC) op virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="6a643-104">This article shows you one way toorun a Linux high-performance computing (HPC) workload on Azure virtual machines.</span></span> <span data-ttu-id="6a643-105">Hier kunt u instellen van een [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster in Azure met Linux-rekenknooppunten en voer een [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulatie toocalculate en visualiseren Hallo-structuur van een grote biomoleculaire-systeem.</span><span class="sxs-lookup"><span data-stu-id="6a643-105">Here, you set up a [Microsoft HPC Pack](https://technet.microsoft.com/library/cc514029) cluster on Azure with Linux compute nodes and run a [NAMD](http://www.ks.uiuc.edu/Research/namd/) simulation toocalculate and visualize hello structure of a large biomolecular system.</span></span>  

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

* <span data-ttu-id="6a643-106">**NAMD** (Nanoscale moleculaire Dynamics programma) is een parallelle moleculaire dynamics-pakket ontworpen voor high-performance simulatie van grote biomoleculaire systemen die up toomillions van atomen.</span><span class="sxs-lookup"><span data-stu-id="6a643-106">**NAMD** (for Nanoscale Molecular Dynamics program) is a parallel molecular dynamics package designed for high-performance simulation of large biomolecular systems containing up toomillions of atoms.</span></span> <span data-ttu-id="6a643-107">Voorbeelden van deze systemen zijn virussen, cel structuren en grote eiwitten.</span><span class="sxs-lookup"><span data-stu-id="6a643-107">Examples of these systems include viruses, cell structures, and large proteins.</span></span> <span data-ttu-id="6a643-108">NAMD schaalt toohundreds van kernen voor het typische simulaties en toomore dan 500.000 kernen voor het grootste simulaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="6a643-108">NAMD scales toohundreds of cores for typical simulations and toomore than 500,000 cores for hello largest simulations.</span></span>
* <span data-ttu-id="6a643-109">**Microsoft HPC Pack** functies toorun biedt grootschalige HPC en parallelle toepassingen in clusters van lokale computers of virtuele machines in Azure.</span><span class="sxs-lookup"><span data-stu-id="6a643-109">**Microsoft HPC Pack** provides features toorun large-scale HPC and parallel applications in clusters of on-premises computers or Azure virtual machines.</span></span> <span data-ttu-id="6a643-110">Oorspronkelijk is ontwikkeld als een oplossing voor Windows HPC-workloads, HPC Pack nu ondersteunt Linux HPC-toepassingen uitvoert op Linux compute knooppunt virtuele machines in een cluster HPC Pack geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="6a643-110">Originally developed as a solution for Windows HPC workloads, HPC Pack now supports running Linux HPC applications on Linux compute node VMs deployed in an HPC Pack cluster.</span></span> <span data-ttu-id="6a643-111">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor een inleiding.</span><span class="sxs-lookup"><span data-stu-id="6a643-111">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for an introduction.</span></span>

<span data-ttu-id="6a643-112">Voor andere opties toorun Linux HPC werkbelastingen in Azure, Zie [technische bronnen voor batchverwerking en high performance computing](../../../batch/batch-hpc-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="6a643-112">For other options toorun Linux HPC workloads in Azure, see [Technical resources for batch and high-performance computing](../../../batch/batch-hpc-solutions.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a643-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="6a643-113">Prerequisites</span></span>
* <span data-ttu-id="6a643-114">**HPC Pack cluster met Linux-rekenknooppunten** -implementeren van een cluster met HPC Pack met Linux-rekenknooppunten in Azure met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) of een [Azure PowerShell-script](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="6a643-114">**HPC Pack cluster with Linux compute nodes** - Deploy an HPC Pack cluster with Linux compute nodes on Azure using either an [Azure Resource Manager template](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterlinuxcn/) or an [Azure PowerShell script](hpcpack-cluster-powershell-script.md).</span></span> <span data-ttu-id="6a643-115">Zie [aan de slag met Linux-rekenknooppunten in een cluster HPC Pack Azure](hpcpack-cluster.md) voor Hallo vereisten en stappen voor beide opties.</span><span class="sxs-lookup"><span data-stu-id="6a643-115">See [Get started with Linux compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster.md) for hello prerequisites and steps for either option.</span></span> <span data-ttu-id="6a643-116">Als u ervoor Hallo Implementatieoptie PowerShell-script kiest, ziet u Hallo voorbeeldconfiguratiebestand in Hallo voorbeeldbestanden aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6a643-116">If you choose hello PowerShell script deployment option, see hello sample configuration file in hello sample files at hello end of this article.</span></span> <span data-ttu-id="6a643-117">Dit bestand configureert een HPC Pack op basis van een Azure-cluster die bestaan uit een Windows Server 2012 R2-hoofdknooppunt en vier grootte grote CentOS 6.6-rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="6a643-117">This file configures an Azure-based HPC Pack cluster consisting of a Windows Server 2012 R2 head node and four size Large CentOS 6.6 compute nodes.</span></span> <span data-ttu-id="6a643-118">Dit bestand aanpassen nodig zijn voor uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="6a643-118">Customize this file as needed for your environment.</span></span>
* <span data-ttu-id="6a643-119">**De software en zelfstudie bestanden NAMD** -NAMD downloaden van software voor Linux van Hallo [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registratie vereist).</span><span class="sxs-lookup"><span data-stu-id="6a643-119">**NAMD software and tutorial files** - Download NAMD software for Linux from hello [NAMD](http://www.ks.uiuc.edu/Research/namd/) site (registration required).</span></span> <span data-ttu-id="6a643-120">In dit artikel is gebaseerd op NAMD versie 2.10 en maakt gebruik van Hallo [Linux-x86_64 (64-bits Intel/AMD met Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archief.</span><span class="sxs-lookup"><span data-stu-id="6a643-120">This article is based on NAMD version 2.10, and uses hello [Linux-x86_64 (64-bit Intel/AMD with Ethernet)](http://www.ks.uiuc.edu/Development/Download/download.cgi?UserID=&AccessCode=&ArchiveID=1310) archive.</span></span> <span data-ttu-id="6a643-121">Ook downloaden Hallo [NAMD zelfstudie bestanden](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span><span class="sxs-lookup"><span data-stu-id="6a643-121">Also download hello [NAMD tutorial files](http://www.ks.uiuc.edu/Training/Tutorials/#namd).</span></span> <span data-ttu-id="6a643-122">Hallo downloads tar-bestanden zijn en moet u een Windows-hulpprogramma tooextract Hallo bestanden op Hallo cluster hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-122">hello downloads are .tar files, and you need a Windows tool tooextract hello files on hello cluster head node.</span></span> <span data-ttu-id="6a643-123">tooextract hello bestanden, volg de instructies Hallo verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6a643-123">tooextract hello files, follow hello instructions later in this article.</span></span> 
* <span data-ttu-id="6a643-124">**VMD** (optioneel) - toosee Hallo resultaten van de taak NAMD downloaden en installeren van Hallo moleculaire visualisatie programma [VMD](http://www.ks.uiuc.edu/Research/vmd/) op een computer van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="6a643-124">**VMD** (optional) - toosee hello results of your NAMD job, download and install hello molecular visualization program [VMD](http://www.ks.uiuc.edu/Research/vmd/) on a computer of your choice.</span></span> <span data-ttu-id="6a643-125">Er is een fout opgetreden in de huidige versie Hallo 1.9.2.</span><span class="sxs-lookup"><span data-stu-id="6a643-125">hello current version is 1.9.2.</span></span> <span data-ttu-id="6a643-126">Zie Hallo VMD downloaden site tooget gestart.</span><span class="sxs-lookup"><span data-stu-id="6a643-126">See hello VMD download site tooget started.</span></span>  

## <a name="set-up-mutual-trust-between-compute-nodes"></a><span data-ttu-id="6a643-127">Wederzijdse vertrouwensrelatie tussen de rekenknooppunten instellen</span><span class="sxs-lookup"><span data-stu-id="6a643-127">Set up mutual trust between compute nodes</span></span>
<span data-ttu-id="6a643-128">Een taak cross-knooppunt wordt uitgevoerd op meerdere Linux-knooppunten vereist Hallo knooppunten tootrust elkaar (door **rsh** of **ssh**).</span><span class="sxs-lookup"><span data-stu-id="6a643-128">Running a cross-node job on multiple Linux nodes requires hello nodes tootrust each other (by **rsh** or **ssh**).</span></span> <span data-ttu-id="6a643-129">Wanneer u Hallo HPC Pack cluster met Microsoft HPC Pack IaaS-implementatiescript hello maakt, Hallo script permanente wederzijds vertrouwen voor Hallo beheerdersaccount dat u opgeeft automatisch ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6a643-129">When you create hello HPC Pack cluster with hello Microsoft HPC Pack IaaS deployment script, hello script automatically sets up permanent mutual trust for hello administrator account you specify.</span></span> <span data-ttu-id="6a643-130">Voor gebruikers die geen beheerder u in Hallo clusterdomein maakt, hebt u tooset een tijdelijke wederzijdse vertrouwensrelatie tussen knooppunten Hallo wanneer een taak toothem is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6a643-130">For non-administrator users you create in hello cluster's domain, you have tooset up temporary mutual trust among hello nodes when a job is allocated toothem.</span></span> <span data-ttu-id="6a643-131">Vernietig vervolgens Hallo relatie wanneer Hallo voltooid is.</span><span class="sxs-lookup"><span data-stu-id="6a643-131">Then, destroy hello relationship after hello job is complete.</span></span> <span data-ttu-id="6a643-132">toodo voor elke gebruiker zodoende een RSA-sleutelpaar toohello cluster welke HPC Pack tooestablish Hallo vertrouwensrelatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="6a643-132">toodo this for each user, provide an RSA key pair toohello cluster which HPC Pack uses tooestablish hello trust relationship.</span></span> <span data-ttu-id="6a643-133">Instructies volgen.</span><span class="sxs-lookup"><span data-stu-id="6a643-133">Instructions follow.</span></span>

### <a name="generate-an-rsa-key-pair"></a><span data-ttu-id="6a643-134">Een RSA-sleutelpaar niet genereren</span><span class="sxs-lookup"><span data-stu-id="6a643-134">Generate an RSA key pair</span></span>
<span data-ttu-id="6a643-135">Is het eenvoudig toogenerate een RSA-sleutelpaar, die een openbare sleutel en een persoonlijke sleutel bevat, door te voeren Hallo Linux **ssh-keygen** opdracht.</span><span class="sxs-lookup"><span data-stu-id="6a643-135">It's easy toogenerate an RSA key pair, which contains a public key and a private key, by running hello Linux **ssh-keygen** command.</span></span>

1. <span data-ttu-id="6a643-136">Meld u aan tooa Linux-computer.</span><span class="sxs-lookup"><span data-stu-id="6a643-136">Log on tooa Linux computer.</span></span>
2. <span data-ttu-id="6a643-137">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="6a643-137">Run hello following command:</span></span>
   
   ```bash
   ssh-keygen -t rsa
   ```
   
   > [!NOTE]
   > <span data-ttu-id="6a643-138">Druk op **Enter** toouse Hallo standaardinstellingen totdat Hallo-opdracht is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6a643-138">Press **Enter** toouse hello default settings until hello command is completed.</span></span> <span data-ttu-id="6a643-139">Voer een wachtwoordzin hier; niet Wanneer u daarom wordt gevraagd om een wachtwoord op te geven, drukt u op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="6a643-139">Do not enter a passphrase here; when prompted for a password, just press **Enter**.</span></span>
   > 
   > 
   
   ![Een RSA-sleutelpaar niet genereren][keygen]
3. <span data-ttu-id="6a643-141">Wijzig de directory toohello ~/.ssh directory.</span><span class="sxs-lookup"><span data-stu-id="6a643-141">Change directory toohello ~/.ssh directory.</span></span> <span data-ttu-id="6a643-142">Hallo persoonlijke sleutel wordt opgeslagen in id_rsa en Hallo openbare sleutel in id_rsa.pub.</span><span class="sxs-lookup"><span data-stu-id="6a643-142">hello private key is stored in id_rsa and hello public key in id_rsa.pub.</span></span>
   
   ![Persoonlijke en openbare sleutel][keys]

### <a name="add-hello-key-pair-toohello-hpc-pack-cluster"></a><span data-ttu-id="6a643-144">Hallo sleutelpaar toohello HPC Pack cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="6a643-144">Add hello key pair toohello HPC Pack cluster</span></span>
1. <span data-ttu-id="6a643-145">[Verbinding maken met extern bureaublad](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello hoofdknooppunt VM gebruik Hallo domeinreferenties die u hebt opgegeven tijdens de implementatie Hallo-cluster (bijvoorbeeld hpc\clusteradmin).</span><span class="sxs-lookup"><span data-stu-id="6a643-145">[Connect by Remote Desktop](../../windows/connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toohello head node VM using hello domain credentials you provided when you deployed hello cluster (for example, hpc\clusteradmin).</span></span> <span data-ttu-id="6a643-146">U beheren Hallo cluster vanaf het hoofdknooppunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="6a643-146">You manage hello cluster from hello head node.</span></span>
2. <span data-ttu-id="6a643-147">Gebruik standaard Windows Server procedures toocreate een domeingebruikersaccount in Active Directory-domein Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6a643-147">Use standard Windows Server procedures toocreate a domain user account in hello cluster's Active Directory domain.</span></span> <span data-ttu-id="6a643-148">Bijvoorbeeld Hallo Active Directory-gebruikers en Computers hulpprogramma gebruiken op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-148">For example, use hello Active Directory User and Computers tool on hello head node.</span></span> <span data-ttu-id="6a643-149">Hallo-voorbeelden in dit artikel wordt ervan uitgegaan dat u een domeingebruiker die met de naam hpcuser in Hallo hpclab domein (hpclab\hpcuser) maken.</span><span class="sxs-lookup"><span data-stu-id="6a643-149">hello examples in this article assume you create a domain user named hpcuser in hello hpclab domain (hpclab\hpcuser).</span></span>
3. <span data-ttu-id="6a643-150">Hallo domein gebruiker toohello HPC Pack cluster toevoegen als een gebruiker van het cluster.</span><span class="sxs-lookup"><span data-stu-id="6a643-150">Add hello domain user toohello HPC Pack cluster as a cluster user.</span></span> <span data-ttu-id="6a643-151">Zie voor instructies [toevoegen of verwijderen cluster gebruikers](https://technet.microsoft.com/library/ff919330.aspx).</span><span class="sxs-lookup"><span data-stu-id="6a643-151">For instructions, see [Add or remove cluster users](https://technet.microsoft.com/library/ff919330.aspx).</span></span>
4. <span data-ttu-id="6a643-152">Maak een bestand met de naam C:\cred.xml en kopieer Hallo RSA belangrijke gegevens in de App.</span><span class="sxs-lookup"><span data-stu-id="6a643-152">Create a file named C:\cred.xml and copy hello RSA key data into it.</span></span> <span data-ttu-id="6a643-153">U kunt een voorbeeld vinden in Hallo voorbeeldbestanden aan Hallo einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6a643-153">You can find an example in hello sample files at hello end of this article.</span></span>
   
   ```
   <ExtendedData>
     <PrivateKey>Copy hello contents of private key here</PrivateKey>
     <PublicKey>Copy hello contents of public key here</PublicKey>
   </ExtendedData>
   ```
5. <span data-ttu-id="6a643-154">Open een opdrachtprompt en Voer Hallo opdracht tooset Hallo-gegevens voor Hallo hpclab\hpcuser account referenties te volgen.</span><span class="sxs-lookup"><span data-stu-id="6a643-154">Open a Command Prompt and enter hello following command tooset hello credentials data for hello hpclab\hpcuser account.</span></span> <span data-ttu-id="6a643-155">Gebruik van Hallo **extendeddata** parameter toopass Hallo naam van Hallo C:\cred.xml u hebt gemaakt voor Hallo belangrijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="6a643-155">You use hello **extendeddata** parameter toopass hello name of hello C:\cred.xml file you created for hello key data.</span></span>
   
   ```command
   hpccred setcreds /extendeddata:c:\cred.xml /user:hpclab\hpcuser /password:<UserPassword>
   ```
   
   <span data-ttu-id="6a643-156">Deze opdracht is voltooid zonder uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6a643-156">This command completes successfully without output.</span></span> <span data-ttu-id="6a643-157">Na het instellen van referenties voor gebruikersaccounts Hallo moet u taken toorun Hallo Hallo cred.xml bestand opslaan op een veilige locatie of verwijder deze.</span><span class="sxs-lookup"><span data-stu-id="6a643-157">After setting hello credentials for hello user accounts you need toorun jobs, store hello cred.xml file in a secure location, or delete it.</span></span>
6. <span data-ttu-id="6a643-158">Als u Hallo RSA-sleutelpaar gegenereerd op een van uw Linux-knooppunten, moet u toodelete Hallo sleutels als u klaar bent met het gebruik ervan.</span><span class="sxs-lookup"><span data-stu-id="6a643-158">If you generated hello RSA key pair on one of your Linux nodes, remember toodelete hello keys after you finish using them.</span></span> <span data-ttu-id="6a643-159">HPC Pack stelt geen wederzijdse vertrouwensrelatie Als het een bestaand id_rsa bestand of id_rsa.pub bestand gevonden.</span><span class="sxs-lookup"><span data-stu-id="6a643-159">HPC Pack does not set up mutual trust if it finds an existing id_rsa file or id_rsa.pub file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a643-160">Wordt niet aanbevolen als de Clusterbeheerder van een een Linux-taak wordt uitgevoerd op een gedeelde cluster, omdat een taak die is verzonden door een beheerder wordt uitgevoerd onder het hoofdaccount Hallo op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6a643-160">We don’t recommend running a Linux job as a cluster administrator on a shared cluster, because a job submitted by an administrator runs under hello root account on hello Linux nodes.</span></span> <span data-ttu-id="6a643-161">Een taak die is verzonden door een gebruiker die geen beheerder wordt uitgevoerd onder een lokale Linux-gebruikersaccount met dezelfde naam als Hallo taak gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="6a643-161">A job submitted by a non-administrator user runs under a local Linux user account with hello same name as hello job user.</span></span> <span data-ttu-id="6a643-162">In dit geval stelt HPC Pack wederzijds vertrouwen voor deze gebruiker Linux op alle Hallo knooppunten toohello taak toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6a643-162">In this case, HPC Pack sets up mutual trust for this Linux user across all hello nodes allocated toohello job.</span></span> <span data-ttu-id="6a643-163">U kunt Hallo Linux gebruiker handmatig op de Linux-knooppunten Hallo instellen voordat u Hallo batchverwerking of HPC Pack Hallo gebruiker automatisch gemaakt wanneer Hallo job wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="6a643-163">You can set up hello Linux user manually on hello Linux nodes before running hello job, or HPC Pack creates hello user automatically when hello job is submitted.</span></span> <span data-ttu-id="6a643-164">Als HPC Pack Hallo gebruiker maakt, verwijderd HPC Pack nadat het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="6a643-164">If HPC Pack creates hello user, HPC Pack deletes it after hello job completes.</span></span> <span data-ttu-id="6a643-165">tooreduce beveiligingsrisico, Hallo-codes worden verwijderd nadat het Hallo-taak is voltooid op Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6a643-165">tooreduce security threat, hello keys are removed after hello job completes on hello nodes.</span></span>
> 
> 

## <a name="set-up-a-file-share-for-linux-nodes"></a><span data-ttu-id="6a643-166">Instellen van een bestandsshare voor Linux-knooppunten</span><span class="sxs-lookup"><span data-stu-id="6a643-166">Set up a file share for Linux nodes</span></span>
<span data-ttu-id="6a643-167">Nu instellen van een SMB-bestandsshare en Hallo gedeelde map op alle Linux-knooppunten tooallow Hallo Linux knooppunten tooaccess NAMD bestanden met een algemeen pad koppelen.</span><span class="sxs-lookup"><span data-stu-id="6a643-167">Now set up an SMB file share, and mount hello shared folder on all Linux nodes tooallow hello Linux nodes tooaccess NAMD files with a common path.</span></span> <span data-ttu-id="6a643-168">Hieronder vindt u stappen toomount een gedeelde map op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-168">Following are steps toomount a shared folder on hello head node.</span></span> <span data-ttu-id="6a643-169">Een share wordt aanbevolen voor distributies zoals CentOS 6.6 die hello Azure File service momenteel niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="6a643-169">A share is recommended for distributions such as CentOS 6.6 that currently don’t support hello Azure File service.</span></span> <span data-ttu-id="6a643-170">Als uw Linux-knooppunten een Azure-bestandsshare ondersteunt, Zie [hoe toouse Azure File storage met Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6a643-170">If your Linux nodes support an Azure File share, see [How toouse Azure File storage with Linux](../../../storage/files/storage-how-to-use-files-linux.md).</span></span> <span data-ttu-id="6a643-171">Zie voor extra opties met HPC Pack delen van bestanden, [aan de slag met Linux-rekenknooppunten in een HPC Pack-Cluster in Azure](hpcpack-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="6a643-171">For additional file sharing options with HPC Pack, see [Get started with Linux compute nodes in an HPC Pack Cluster in Azure](hpcpack-cluster.md).</span></span>

1. <span data-ttu-id="6a643-172">Maak een map op het hoofdknooppunt Hallo en tooEveryone delen door het instellen van machtigingen voor lezen/schrijven.</span><span class="sxs-lookup"><span data-stu-id="6a643-172">Create a folder on hello head node, and share it tooEveryone by setting Read/Write privileges.</span></span> <span data-ttu-id="6a643-173">In dit voorbeeld \\ \\CentOS66HN\Namd heet Hallo Hallo map, waarbij CentOS66HN Hallo-hostnaam van Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-173">In this example, \\\\CentOS66HN\Namd is hello name of hello folder, where CentOS66HN is hello host name of hello head node.</span></span>
2. <span data-ttu-id="6a643-174">Maak een submap met de naam namd2 in Hallo gedeelde map.</span><span class="sxs-lookup"><span data-stu-id="6a643-174">Create a subfolder named namd2 in hello shared folder.</span></span> <span data-ttu-id="6a643-175">In namd2, maakt u een nieuwe submap met de naam namdsample.</span><span class="sxs-lookup"><span data-stu-id="6a643-175">In namd2, create another subfolder named namdsample.</span></span>
3. <span data-ttu-id="6a643-176">Hallo NAMD bestanden in de map Hallo uitpakken met behulp van een Windows-versie van **tar** of een ander Windows-hulpprogramma dat met TAR-archieven werkt.</span><span class="sxs-lookup"><span data-stu-id="6a643-176">Extract hello NAMD files in hello folder by using a Windows version of **tar** or another Windows utility that operates on .tar archives.</span></span> 
   
   * <span data-ttu-id="6a643-177">Hallo NAMD tar-archief te extraheren\\\\CentOS66HN\Namd\namd2.</span><span class="sxs-lookup"><span data-stu-id="6a643-177">Extract hello NAMD tar archive too\\\\CentOS66HN\Namd\namd2.</span></span>
   * <span data-ttu-id="6a643-178">Pak de zelfstudie bestanden Hallo onder \\ \\CentOS66HN\Namd\namd2\namdsample.</span><span class="sxs-lookup"><span data-stu-id="6a643-178">Extract hello tutorial files under \\\\CentOS66HN\Namd\namd2\namdsample.</span></span>
4. <span data-ttu-id="6a643-179">Open een Windows PowerShell-venster en Voer Hallo opdrachten toomount Hallo gedeelde map op Hallo Linux-knooppunten te volgen.</span><span class="sxs-lookup"><span data-stu-id="6a643-179">Open a Windows PowerShell window and run hello following commands toomount hello shared folder on hello Linux nodes.</span></span>
   
    ```command
    clusrun /nodegroup:LinuxNodes mkdir -p /namd2
   
    clusrun /nodegroup:LinuxNodes mount -t cifs //CentOS66HN/Namd/namd2 /namd2 -o vers=2.1`,username=<username>`,password='<password>'`,dir_mode=0777`,file_mode=0777
    ```

<span data-ttu-id="6a643-180">de eerste opdracht Hallo maakt een map met de naam /namd2 op alle knooppunten in Hallo LinuxNodes groep.</span><span class="sxs-lookup"><span data-stu-id="6a643-180">hello first command creates a folder named /namd2 on all nodes in hello LinuxNodes group.</span></span> <span data-ttu-id="6a643-181">de tweede opdracht Hallo koppelt Hallo gedeelde map //CentOS66HN/Namd/namd2 op Hallo-map met dir_mode en file_mode bits set too777.</span><span class="sxs-lookup"><span data-stu-id="6a643-181">hello second command mounts hello shared folder //CentOS66HN/Namd/namd2 onto hello folder with dir_mode and file_mode bits set too777.</span></span> <span data-ttu-id="6a643-182">Hallo *gebruikersnaam* en *wachtwoord* Hallo opdracht moet Hallo referenties van een gebruiker op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-182">hello *username* and *password* in hello command should be hello credentials of a user on hello head node.</span></span>

> [!NOTE]
> <span data-ttu-id="6a643-183">Hallo '\\`' symbool in de tweede opdracht Hallo is een escapeteken voor PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6a643-183">hello “\\`” symbol in hello second command is an escape symbol for PowerShell.</span></span> <span data-ttu-id="6a643-184">"\\`, 'betekent Hallo', ' (door komma's teken) maakt deel uit van Hallo-opdracht.</span><span class="sxs-lookup"><span data-stu-id="6a643-184">“\\`,” means hello “,” (comma character) is a part of hello command.</span></span>
> 
> 

## <a name="create-a-bash-script-toorun-a-namd-job"></a><span data-ttu-id="6a643-185">Een script Bash toorun NAMD taak maken</span><span class="sxs-lookup"><span data-stu-id="6a643-185">Create a Bash script toorun a NAMD job</span></span>
<span data-ttu-id="6a643-186">De taak NAMD moet een *nodelist* bestand voor **charmrun** toodetermine Hallo aantal knooppunten toouse bij het starten van NAMD processen.</span><span class="sxs-lookup"><span data-stu-id="6a643-186">Your NAMD job needs a *nodelist* file for **charmrun** toodetermine hello number of nodes toouse when starting NAMD processes.</span></span> <span data-ttu-id="6a643-187">U gebruikt een Bash-script die wordt uitgevoerd en genereert Hallo knooppuntenbestand **charmrun** met deze knooppuntenbestand.</span><span class="sxs-lookup"><span data-stu-id="6a643-187">You use a Bash script that generates hello nodelist file and runs **charmrun** with this nodelist file.</span></span> <span data-ttu-id="6a643-188">Vervolgens dient u een taak NAMD in HPC Cluster Manager waarmee dit script wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="6a643-188">You can then submit a NAMD job in HPC Cluster Manager that calls this script.</span></span>

<span data-ttu-id="6a643-189">Met een teksteditor van uw keuze, een Bash-script maken in Hallo /namd2 map met de Hallo NAMD-programmabestanden en noem deze hpccharmrun.sh. Voor een snel testen van het concept kopiëren Hallo hpccharmrun.sh voorbeeldscript gegeven aan het einde van dit artikel Hallo en ga te[verzenden van een taak NAMD](#submit-a-namd-job).</span><span class="sxs-lookup"><span data-stu-id="6a643-189">Using a text editor of your choice, create a Bash script in hello /namd2 folder containing hello NAMD program files and name it hpccharmrun.sh. For a quick proof of concept, copy hello example hpccharmrun.sh script provided at hello end of this article and go too[Submit a NAMD job](#submit-a-namd-job).</span></span>

> [!TIP]
> <span data-ttu-id="6a643-190">Sla het script als een tekstbestand met Linux regeleinden (alleen LF, niet CR LF).</span><span class="sxs-lookup"><span data-stu-id="6a643-190">Save your script as a text file with Linux line endings (LF only, not CR LF).</span></span> <span data-ttu-id="6a643-191">Dit zorgt ervoor dat deze wordt uitgevoerd naar behoren op Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6a643-191">This ensures that it runs properly on hello Linux nodes.</span></span>
> 
> 

<span data-ttu-id="6a643-192">Hieronder vindt u meer informatie over de werking van dit bash-script.</span><span class="sxs-lookup"><span data-stu-id="6a643-192">Following are details about what this bash script does.</span></span> 

1. <span data-ttu-id="6a643-193">Sommige variabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="6a643-193">Define some variables.</span></span>
   
   ```bash
   #!/bin/bash
   
   # hello path of this script
   SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
   # Charmrun command
   CHARMRUN=${SCRIPT_PATH}/charmrun
   # Argument of ++nodelist
   NODELIST_OPT="++nodelist"
   # Argument of ++p
   NUMPROCESS="+p"
   ```
2. <span data-ttu-id="6a643-194">Knooppunt-informatie ophalen uit het Hallo-omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="6a643-194">Get node information from hello environment variables.</span></span> <span data-ttu-id="6a643-195">$NODESCORES slaat een lijst met woorden van $CCP_NODES_CORES splitsen.</span><span class="sxs-lookup"><span data-stu-id="6a643-195">$NODESCORES stores a list of split words from $CCP_NODES_CORES.</span></span> <span data-ttu-id="6a643-196">$COUNT is Hallo grootte van $NODESCORES.</span><span class="sxs-lookup"><span data-stu-id="6a643-196">$COUNT is hello size of $NODESCORES.</span></span>
   
   ```
   # Get node information from hello environment variables
   NODESCORES=(${CCP_NODES_CORES})
   COUNT=${#NODESCORES[@]}
   ```    
   
   <span data-ttu-id="6a643-197">Hallo-indeling voor Hallo $CCP_NODES_CORES variabele is als volgt:</span><span class="sxs-lookup"><span data-stu-id="6a643-197">hello format for hello $CCP_NODES_CORES variable is as follows:</span></span>
   
   ```
   <Number of nodes> <Name of node1> <Cores of node1> <Name of node2> <Cores of node2>…
   ```
   
   <span data-ttu-id="6a643-198">Deze variabele bevat Hallo totaal aantal knooppunten, knooppuntnamen en het aantal kernen op elk knooppunt dat toohello taak is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="6a643-198">This variable lists hello total number of nodes, node names, and number of cores on each node that are allocated toohello job.</span></span> <span data-ttu-id="6a643-199">Bijvoorbeeld als Hallo-taak 10 kernen toorun moet, lijkt Hallo-waarde van $CCP_NODES_CORES op:</span><span class="sxs-lookup"><span data-stu-id="6a643-199">For example, if hello job needs 10 cores toorun, hello value of $CCP_NODES_CORES is similar to:</span></span>
   
   ```
   3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 2
   ```
3. <span data-ttu-id="6a643-200">Als Hallo $CCP_NODES_CORES variabele niet is ingesteld, start u **charmrun** rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="6a643-200">If hello $CCP_NODES_CORES variable is not set, start **charmrun** directly.</span></span> <span data-ttu-id="6a643-201">(Dit moet alleen worden uitgevoerd als u dit script rechtstreeks op uw Linux-knooppunten uitvoert.)</span><span class="sxs-lookup"><span data-stu-id="6a643-201">(This should only occur when you run this script directly on your Linux nodes.)</span></span>
   
   ```
   if [ ${COUNT} -eq 0 ]
   then
     # CCP_NODES is_CORES is not found or is empty, so just run charmrun without nodelist arg.
     #echo ${CHARMRUN} $*
     ${CHARMRUN} $*
   ```
4. <span data-ttu-id="6a643-202">Of maak een knooppuntenbestand voor **charmrun**.</span><span class="sxs-lookup"><span data-stu-id="6a643-202">Or create a nodelist file for **charmrun**.</span></span>
   
   ```
   else
     # Create hello nodelist file
     NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$
   
     # Write hello head line
     echo "group main" > ${NODELIST_PATH}
   
     # Get every node name and number of cores and write into hello nodelist file
     I=1
     while [ ${I} -lt ${COUNT} ]
     do
         echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
         let "I=${I}+2"
     done
   ```
5. <span data-ttu-id="6a643-203">Voer **charmrun** met knooppuntenbestand Hallo, krijgen de status van het resultaat, en verwijder knooppuntenbestand Hallo Hallo achter.</span><span class="sxs-lookup"><span data-stu-id="6a643-203">Run **charmrun** with hello nodelist file, get its return status, and remove hello nodelist file at hello end.</span></span>
   
   <span data-ttu-id="6a643-204">${CCP_NUMCPUS} is een andere omgevingsvariabele instellen door Hallo HPC Pack hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-204">${CCP_NUMCPUS} is another environment variable set by hello HPC Pack head node.</span></span> <span data-ttu-id="6a643-205">Hallo-nummer van de totale kernen toothis taak toegewezen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="6a643-205">It stores hello number of total cores allocated toothis job.</span></span> <span data-ttu-id="6a643-206">We gebruiken deze toospecify Hallo aantal processen voor charmrun.</span><span class="sxs-lookup"><span data-stu-id="6a643-206">We use it toospecify hello number of processes for charmrun.</span></span>
   
   ```
   # Run charmrun with nodelist arg
   #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
   
   RTNSTS=$?
   rm -f ${NODELIST_PATH}
   fi
   
   ```
6. <span data-ttu-id="6a643-207">Exit Hello **charmrun** status retourneren.</span><span class="sxs-lookup"><span data-stu-id="6a643-207">Exit with hello **charmrun** return status.</span></span>
   
   ```
   exit ${RTNSTS}
   ```

<span data-ttu-id="6a643-208">Hieronder vindt u Hallo-informatie in de knooppuntenbestand hello, welke Hallo script genereert:</span><span class="sxs-lookup"><span data-stu-id="6a643-208">Following is hello information in hello nodelist file, which hello script generates:</span></span>

```
group main
host <Name of node1> ++cpus <Cores of node1>
host <Name of node2> ++cpus <Cores of node2>
…
```

<span data-ttu-id="6a643-209">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="6a643-209">For example:</span></span>

```
group main
host CENTOS66LN-00 ++cpus 4
host CENTOS66LN-01 ++cpus 4
host CENTOS66LN-03 ++cpus 2
```

## <a name="submit-a-namd-job"></a><span data-ttu-id="6a643-210">Verzenden van een taak NAMD</span><span class="sxs-lookup"><span data-stu-id="6a643-210">Submit a NAMD job</span></span>
<span data-ttu-id="6a643-211">U bent nu klaar toosubmit een taak NAMD in HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="6a643-211">Now you are ready toosubmit a NAMD job in HPC Cluster Manager.</span></span>

1. <span data-ttu-id="6a643-212">Verbinding maken met hoofdknooppunt tooyour-cluster en start HPC Cluster Manager.</span><span class="sxs-lookup"><span data-stu-id="6a643-212">Connect tooyour cluster head node and start HPC Cluster Manager.</span></span>
2. <span data-ttu-id="6a643-213">In **bronbeheer**, moet u ervoor zorgen dat Hallo Linux-rekenknooppunten hello **Online** status.</span><span class="sxs-lookup"><span data-stu-id="6a643-213">In **Resource Management**, ensure that hello Linux compute nodes are in hello **Online** state.</span></span> <span data-ttu-id="6a643-214">Als dat niet het geval is, selecteert u deze en klikt u op **Online brengen**.</span><span class="sxs-lookup"><span data-stu-id="6a643-214">If they are not, select them and click **Bring Online**.</span></span>
3. <span data-ttu-id="6a643-215">In **Jobbeheer**, klikt u op **nieuwe taak**.</span><span class="sxs-lookup"><span data-stu-id="6a643-215">In **Job Management**, click **New Job**.</span></span>
4. <span data-ttu-id="6a643-216">Voer een naam voor de taak zoals *hpccharmrun*.</span><span class="sxs-lookup"><span data-stu-id="6a643-216">Enter a name for job such as *hpccharmrun*.</span></span>
   
   ![Nieuwe HPC-taak][namd_job]
5. <span data-ttu-id="6a643-218">Op Hallo **taakdetails** pagina onder **taak Resources**, selecteer Hallo type resource als **knooppunt** en set Hallo **Minimum** too3.</span><span class="sxs-lookup"><span data-stu-id="6a643-218">On hello **Job Details** page, under **Job Resources**, select hello type of resource as **Node** and set hello **Minimum** too3.</span></span> <span data-ttu-id="6a643-219">, we Hallo taak uitvoeren op drie Linux-knooppunten en elk knooppunt vier kernen heeft.</span><span class="sxs-lookup"><span data-stu-id="6a643-219">, we run hello job on three Linux nodes and each node has four cores.</span></span>
   
   ![Taak resources][job_resources]
6. <span data-ttu-id="6a643-221">Klik op **taken bewerken** in Hallo navigatiebalk aan de linkerkant en klik vervolgens op **toevoegen** tooadd een taak toohello taak.</span><span class="sxs-lookup"><span data-stu-id="6a643-221">Click **Edit Tasks** in hello left navigation, and then click **Add** tooadd a task toohello job.</span></span>    
7. <span data-ttu-id="6a643-222">Op Hallo **taakdetails en i/o-omleiding** pagina set Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="6a643-222">On hello **Task Details and I/O Redirection** page, set hello following values:</span></span>
   
   * <span data-ttu-id="6a643-223">**Opdrachtregel**-
     `/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span><span class="sxs-lookup"><span data-stu-id="6a643-223">**Command line** -
`/namd2/hpccharmrun.sh ++remote-shell ssh /namd2/namd2 /namd2/namdsample/1-2-sphere/ubq_ws_eq.conf > /namd2/namd2_hpccharmrun.log`</span></span>
     
     > [!TIP]
     > <span data-ttu-id="6a643-224">Hallo is voorgaande opdrachtregel één opdracht zonder regeleinden.</span><span class="sxs-lookup"><span data-stu-id="6a643-224">hello preceding command line is a single command without line breaks.</span></span> <span data-ttu-id="6a643-225">Loopt deze tooappear op meerdere regels onder **opdrachtregel**.</span><span class="sxs-lookup"><span data-stu-id="6a643-225">It wraps tooappear on several lines under **Command line**.</span></span>
     > 
     > 
   * <span data-ttu-id="6a643-226">**Werkmap** -/namd2</span><span class="sxs-lookup"><span data-stu-id="6a643-226">**Working directory** - /namd2</span></span>
   * <span data-ttu-id="6a643-227">**Minimale** - 3</span><span class="sxs-lookup"><span data-stu-id="6a643-227">**Minimum** - 3</span></span>
     
     ![Taakdetails][task_details]
     
     > [!NOTE]
     > <span data-ttu-id="6a643-229">Hallo-werkmap hier ingestelde omdat **charmrun** toonavigate toohello probeert dezelfde werkmap op elk knooppunt.</span><span class="sxs-lookup"><span data-stu-id="6a643-229">You set hello working directory here because **charmrun** tries toonavigate toohello same working directory on each node.</span></span> <span data-ttu-id="6a643-230">Als het Hallo-werkmap niet is ingesteld, begint HPC Pack Hallo-opdracht in een willekeurige naam map gemaakt op een Hallo Linux-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="6a643-230">If hello working directory isn't set, HPC Pack starts hello command in a randomly named folder created on one of hello Linux nodes.</span></span> <span data-ttu-id="6a643-231">Dit zorgt ervoor dat Hallo volgende fout op Hallo andere knooppunten: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid dit probleem op door een mappad die kan worden geopend door alle knooppunten als werkmap Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="6a643-231">This causes hello following error on hello other nodes: `/bin/bash: line 37: cd: /tmp/nodemanager_task_94_0.mFlQSN: No such file or directory.` tooavoid this problem, specify a folder path that can be accessed by all nodes as hello working directory.</span></span>
     > 
     > 
8. <span data-ttu-id="6a643-232">Klik op **OK** en klik vervolgens op **indienen** toorun deze taak.</span><span class="sxs-lookup"><span data-stu-id="6a643-232">Click **OK** and then click **Submit** toorun this job.</span></span>
   
   <span data-ttu-id="6a643-233">Standaard verzendt HPC Pack Hallo taak als uw huidige aangemelde gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="6a643-233">By default, HPC Pack submits hello job as your current logged-on user account.</span></span> <span data-ttu-id="6a643-234">Een dialoogvenster vragen u tooenter Hallo-gebruikersnaam en wachtwoord nadat u op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="6a643-234">A dialog box might prompt you tooenter hello user name and password after you click **Submit**.</span></span>
   
   ![Taak referenties][creds]
   
   <span data-ttu-id="6a643-236">Onder bepaalde omstandigheden onthoudt HPC Pack Hallo gebruikersgegevens u invoer voordat en dit dialoogvenster niet weergeven.</span><span class="sxs-lookup"><span data-stu-id="6a643-236">Under some conditions, HPC Pack remembers hello user information you input before and doesn't show this dialog box.</span></span> <span data-ttu-id="6a643-237">toomake HPC Pack opnieuw weergeven, voer de volgende opdracht achter de opdrachtprompt Hallo en vervolgens dient Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="6a643-237">toomake HPC Pack show it again, enter hello following command at a Command Prompt and then submit hello job.</span></span>
   
   ```command
   hpccred delcreds
   ```
9. <span data-ttu-id="6a643-238">Hallo taak duurt enkele minuten toofinish.</span><span class="sxs-lookup"><span data-stu-id="6a643-238">hello job takes several minutes toofinish.</span></span>
10. <span data-ttu-id="6a643-239">Hallo taaklogboek op vinden \\ <headnodeName>\Namd\namd2\namd2_hpccharmrun.log en Hallo uitvoerbestanden in \\ <headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span><span class="sxs-lookup"><span data-stu-id="6a643-239">Find hello job log at \\<headnodeName>\Namd\namd2\namd2_hpccharmrun.log and hello output files in \\<headnodeName>\Namd\namd2\namdsample\1-2-sphere\.</span></span>
11. <span data-ttu-id="6a643-240">Start VMD tooview eventueel de taak van de resultaten.</span><span class="sxs-lookup"><span data-stu-id="6a643-240">Optionally, start VMD tooview your job results.</span></span> <span data-ttu-id="6a643-241">Hallo-stappen voor het visualiseren van Hallo NAMD uitvoerbestanden (in dit geval een ubiquitin eiwit molecuul in een bol water) zijn buiten bereik Hallo van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="6a643-241">hello steps for visualizing hello NAMD output files (in this case, a ubiquitin protein molecule in a water sphere) are beyond hello scope of this article.</span></span> <span data-ttu-id="6a643-242">Zie [NAMD zelfstudie](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6a643-242">See [NAMD Tutorial](http://www.life.illinois.edu/emad/biop590c/namd-tutorial-unix-590C.pdf) for details.</span></span>
    
    ![Resultaten van de taak][vmd_view]

## <a name="sample-files"></a><span data-ttu-id="6a643-244">Voorbeeldbestanden</span><span class="sxs-lookup"><span data-stu-id="6a643-244">Sample files</span></span>
### <a name="sample-xml-configuration-file-for-cluster-deployment-by-powershell-script"></a><span data-ttu-id="6a643-245">Voorbeeld XML-configuratiebestand voor implementatie van het cluster door PowerShell-script</span><span class="sxs-lookup"><span data-stu-id="6a643-245">Sample XML configuration file for cluster deployment by PowerShell script</span></span>
```
<?xml version="1.0" encoding="utf-8" ?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>Subscription-1</SubscriptionName>
    <StorageAccount>mystorageaccount</StorageAccount>
  </Subscription>
      <Location>West US</Location>  
  <VNet>
    <VNetName>MyVNet</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>HeadNodeAsDC</DCOption>
    <DomainFQDN>hpclab.local</DomainFQDN>
  </Domain>
  <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>CentOS66HN</VMName>
    <ServiceName>MyHPCService</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI />
    <EnableWebPortal />
  </HeadNode>
  <LinuxComputeNodes>
    <VMNamePattern>CentOS66LN-%00%</VMNamePattern>
    <ServiceName>MyLnxCNService</ServiceName>
     <VMSize>Large</VMSize>
     <NodeCount>4</NodeCount>
    <ImageName>5112500ae3b842c8b9c604889f8753c3__OpenLogic-CentOS-66-20150325</ImageName>
  </LinuxComputeNodes>
</IaaSClusterConfig>    
```

### <a name="sample-credxml-file"></a><span data-ttu-id="6a643-246">Voorbeeldbestand cred.xml</span><span class="sxs-lookup"><span data-stu-id="6a643-246">Sample cred.xml file</span></span>
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

### <a name="sample-hpccharmrunsh-script"></a><span data-ttu-id="6a643-247">Voorbeeldscript hpccharmrun.sh</span><span class="sxs-lookup"><span data-stu-id="6a643-247">Sample hpccharmrun.sh script</span></span>
```
#!/bin/bash

# hello path of this script
SCRIPT_PATH="$( dirname "${BASH_SOURCE[0]}" )"
# Charmrun command
CHARMRUN=${SCRIPT_PATH}/charmrun
# Argument of ++nodelist
NODELIST_OPT="++nodelist"
# Argument of ++p
NUMPROCESS="+p"

# Get node information from ENVs
# CCP_NODES_CORES=3 CENTOS66LN-00 4 CENTOS66LN-01 4 CENTOS66LN-03 4
NODESCORES=(${CCP_NODES_CORES})
COUNT=${#NODESCORES[@]}

if [ ${COUNT} -eq 0 ]
then
    # If CCP_NODES_CORES is not found or is empty, just run hello charmrun without nodelist arg.
    #echo ${CHARMRUN} $*
    ${CHARMRUN} $*
else
    # Create hello nodelist file
    NODELIST_PATH=${SCRIPT_PATH}/nodelist_$$

    # Write hello head line
    echo "group main" > ${NODELIST_PATH}

    # Get every node name & cores and write into hello nodelist file
    I=1
    while [ ${I} -lt ${COUNT} ]
    do
        echo "host ${NODESCORES[${I}]} ++cpus ${NODESCORES[$(($I+1))]}" >> ${NODELIST_PATH}
        let "I=${I}+2"
    done

    # Run hello charmrun with nodelist arg
    #echo ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*
    ${CHARMRUN} ${NUMPROCESS}${CCP_NUMCPUS} ${NODELIST_OPT} ${NODELIST_PATH} $*

    RTNSTS=$?
    rm -f ${NODELIST_PATH}
fi

exit ${RTNSTS}
```

 

<!--Image references-->
[keygen]:media/hpcpack-cluster-namd/keygen.png
[keys]:media/hpcpack-cluster-namd/keys.png
[namd_job]:media/hpcpack-cluster-namd/namd_job.png
[job_resources]:media/hpcpack-cluster-namd/job_resources.png
[creds]:media/hpcpack-cluster-namd/creds.png
[task_details]:media/hpcpack-cluster-namd/task_details.png
[vmd_view]:media/hpcpack-cluster-namd/vmd_view.png

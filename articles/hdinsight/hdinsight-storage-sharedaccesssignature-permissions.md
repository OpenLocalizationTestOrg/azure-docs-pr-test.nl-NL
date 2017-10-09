---
title: aaaRestrict toegang met behulp van Shared Access Signatures - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Shared Access Signatures toorestrict HDInsight toegang krijgen tot toodata opgeslagen in Azure storage-blobs.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a><span data-ttu-id="d6719-103">Azure Storage Shared Access Signatures toorestrict toegang toodata in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="d6719-103">Use Azure Storage Shared Access Signatures toorestrict access toodata in HDInsight</span></span>

<span data-ttu-id="d6719-104">HDInsight heeft volledige toegang toodata in hello Azure Storage-accounts die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-104">HDInsight has full access toodata in hello Azure Storage accounts associated with hello cluster.</span></span> <span data-ttu-id="d6719-105">U kunt de handtekeningen voor gedeelde toegang op Hallo blob-container toorestrict toegang toohello gegevens.</span><span class="sxs-lookup"><span data-stu-id="d6719-105">You can use Shared Access Signatures on hello blob container toorestrict access toohello data.</span></span> <span data-ttu-id="d6719-106">Bijvoorbeeld: tooprovide alleen-lezentoegang toohello gegevens.</span><span class="sxs-lookup"><span data-stu-id="d6719-106">For example, tooprovide read-only access toohello data.</span></span> <span data-ttu-id="d6719-107">Shared Access Signatures (SAS) zijn een functie van Azure storage-accounts waarmee u toolimit toegang toodata.</span><span class="sxs-lookup"><span data-stu-id="d6719-107">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you toolimit access toodata.</span></span> <span data-ttu-id="d6719-108">Bijvoorbeeld, het bieden van alleen-lezentoegang toodata.</span><span class="sxs-lookup"><span data-stu-id="d6719-108">For example, providing read-only access toodata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6719-109">Voor een oplossing met behulp van Apache Zwerver, kunt u met HDInsight domein.</span><span class="sxs-lookup"><span data-stu-id="d6719-109">For a solution using Apache Ranger, consider using domain-joined HDInsight.</span></span> <span data-ttu-id="d6719-110">Zie voor meer informatie, Hallo [HDInsight domein configureren](hdinsight-domain-joined-configure.md) document.</span><span class="sxs-lookup"><span data-stu-id="d6719-110">For more information, see hello [Configure domain-joined HDInsight](hdinsight-domain-joined-configure.md) document.</span></span>

> [!WARNING]
> <span data-ttu-id="d6719-111">HDInsight moet hebben volledige toegang toohello standaard opslagruimte voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-111">HDInsight must have full access toohello default storage for hello cluster.</span></span>

## <a name="requirements"></a><span data-ttu-id="d6719-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d6719-112">Requirements</span></span>

* <span data-ttu-id="d6719-113">Een Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="d6719-113">An Azure subscription</span></span>
* <span data-ttu-id="d6719-114">C# of Python.</span><span class="sxs-lookup"><span data-stu-id="d6719-114">C# or Python.</span></span> <span data-ttu-id="d6719-115">C#-voorbeeldcode is opgegeven als een Visual Studio-oplossing.</span><span class="sxs-lookup"><span data-stu-id="d6719-115">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="d6719-116">Visual Studio moet versie 2013 of 2015 2017</span><span class="sxs-lookup"><span data-stu-id="d6719-116">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="d6719-117">Python moet 2.7 of hoger zijn</span><span class="sxs-lookup"><span data-stu-id="d6719-117">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="d6719-118">Een Linux gebaseerde HDInsight-cluster of [Azure PowerShell] [ powershell] -als u een bestaand cluster op basis van Linux hebt, kunt u Ambari tooadd een Shared Access Signature toohello-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-118">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari tooadd a Shared Access Signature toohello cluster.</span></span> <span data-ttu-id="d6719-119">Zo niet, kunt u gebruik van Azure PowerShell toocreate een cluster en het toevoegen van een Shared Access Signature tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-119">If not, you can use Azure PowerShell toocreate a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d6719-120">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d6719-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d6719-121">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d6719-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d6719-122">van de voorbeeldbestanden van Hallo [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="d6719-122">hello example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="d6719-123">Deze bibliotheek bevat de volgende items Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6719-123">This repository contains hello following items:</span></span>

  * <span data-ttu-id="d6719-124">Een Visual Studio-project dat een storage-container, opgeslagen beleid en SAS voor gebruik met HDInsight maken kunt</span><span class="sxs-lookup"><span data-stu-id="d6719-124">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="d6719-125">Een pythonscript die een storage-container, opgeslagen beleid en SAS voor gebruik met HDInsight maken kunt</span><span class="sxs-lookup"><span data-stu-id="d6719-125">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="d6719-126">Een PowerShell-script dat van een HDInsight maken kan-cluster en configureert u het toouse Hallo SAS.</span><span class="sxs-lookup"><span data-stu-id="d6719-126">A PowerShell script that can create a HDInsight cluster and configure it toouse hello SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="d6719-127">Handtekeningen voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="d6719-127">Shared Access Signatures</span></span>

<span data-ttu-id="d6719-128">Er zijn twee soorten handtekeningen voor gedeelde toegang:</span><span class="sxs-lookup"><span data-stu-id="d6719-128">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="d6719-129">Ad hoc: Hallo starttijd, verlooptijd en machtigingen voor Hallo SAS zijn opgegeven op Hallo SAS-URI.</span><span class="sxs-lookup"><span data-stu-id="d6719-129">Ad hoc: hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span>

* <span data-ttu-id="d6719-130">Opgeslagen toegangsbeleid: een opgeslagen-beleid is gedefinieerd in een resourcecontainer, zoals een blob-container.</span><span class="sxs-lookup"><span data-stu-id="d6719-130">Stored access policy: A stored access policy is defined on a resource container, such as a blob container.</span></span> <span data-ttu-id="d6719-131">Een beleid kan worden gebruikt toomanage beperkingen voor een of meer handtekeningen voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="d6719-131">A policy can be used toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="d6719-132">Wanneer u een SAS aan een opgeslagen toegangsbeleid koppelt, Hallo SAS neemt over Hallo beperkingen - Hallo starttijd, verlooptijd en machtigingen - zijn opgegeven voor toegangsbeleid Hallo opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d6719-132">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span>

<span data-ttu-id="d6719-133">Hallo verschil tussen twee Hallo formulieren is belangrijk voor één key '-scenario: intrekken.</span><span class="sxs-lookup"><span data-stu-id="d6719-133">hello difference between hello two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="d6719-134">Een SAS is een URL, zodat iedereen die Hallo SAS verkrijgt deze gebruiken kunt, ongeacht wie het aangevraagde toobegin met.</span><span class="sxs-lookup"><span data-stu-id="d6719-134">A SAS is a URL, so anyone who obtains hello SAS can use it, regardless of who requested it toobegin with.</span></span> <span data-ttu-id="d6719-135">Als een SAS openbaar wordt gepubliceerd, kan deze worden gebruikt door iedereen in Hallo wereld.</span><span class="sxs-lookup"><span data-stu-id="d6719-135">If a SAS is published publicly, it can be used by anyone in hello world.</span></span> <span data-ttu-id="d6719-136">Een SA's dat wordt gedistribueerd is geldig tot vier dingen gebeurt:</span><span class="sxs-lookup"><span data-stu-id="d6719-136">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="d6719-137">Hallo verlooptijd opgegeven op Hallo die SAS is bereikt.</span><span class="sxs-lookup"><span data-stu-id="d6719-137">hello expiry time specified on hello SAS is reached.</span></span>

2. <span data-ttu-id="d6719-138">Hallo verlooptijd opgegeven op Hallo opgeslagen toegangsbeleid waarnaar wordt verwezen door Hallo die SAS is bereikt.</span><span class="sxs-lookup"><span data-stu-id="d6719-138">hello expiry time specified on hello stored access policy referenced by hello SAS is reached.</span></span> <span data-ttu-id="d6719-139">Hallo volgende scenario's ervoor zorgen dat het verlooptijdstip Hallo toobe bereikt:</span><span class="sxs-lookup"><span data-stu-id="d6719-139">hello following scenarios cause hello expiry time toobe reached:</span></span>

    * <span data-ttu-id="d6719-140">Hallo tijdsinterval is verstreken.</span><span class="sxs-lookup"><span data-stu-id="d6719-140">hello time interval has elapsed.</span></span>
    * <span data-ttu-id="d6719-141">Hallo opgeslagen toegangsbeleid is gewijzigde toohave een verlooptijd in de afgelopen Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6719-141">hello stored access policy is modified toohave an expiry time in hello past.</span></span> <span data-ttu-id="d6719-142">Wijzigen van het verlooptijdstip Hallo is eenrichtingssessie toorevoke Hallo SAS.</span><span class="sxs-lookup"><span data-stu-id="d6719-142">Changing hello expiry time is one way toorevoke hello SAS.</span></span>

3. <span data-ttu-id="d6719-143">Hallo toegangsbeleid waarnaar wordt verwezen door Hallo die SAS wordt verwijderd, die een andere manier toorevoke Hallo SAS is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d6719-143">hello stored access policy referenced by hello SAS is deleted, which is another way toorevoke hello SAS.</span></span> <span data-ttu-id="d6719-144">Als u opnieuw maken Hallo opgeslagen-beleid met dezelfde naam, SAS-tokens voor Hallo Hallo vorige beleid zijn geldig (als Hallo verlooptijd op Hallo SAS is niet verstreken).</span><span class="sxs-lookup"><span data-stu-id="d6719-144">If you recreate hello stored access policy with hello same name, all  SAS tokens for hello previous policy are valid (if hello expiry time on hello SAS has not passed).</span></span> <span data-ttu-id="d6719-145">Als u van plan toorevoke Hallo SAS bent, zijn ervoor toouse een andere naam op als u het Hallo-beleid met een verlooptijd in toekomstige Hallo opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="d6719-145">If you intend toorevoke hello SAS, be sure toouse a different name if you recreate hello access policy with an expiry time in hello future.</span></span>

4. <span data-ttu-id="d6719-146">Hallo accountsleutel die gebruikt toocreate Hallo SAS is wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="d6719-146">hello account key that was used toocreate hello SAS is regenerated.</span></span> <span data-ttu-id="d6719-147">Opnieuw genereren Hallo-sleutel zorgt ervoor dat alle toepassingen die gebruikmaken van de vorige sleutel toofail verificatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6719-147">Regenerating hello key causes all applications that use hello previous key toofail authentication.</span></span> <span data-ttu-id="d6719-148">Werk alle onderdelen toohello nieuwe sleutel.</span><span class="sxs-lookup"><span data-stu-id="d6719-148">Update all components toohello new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d6719-149">Een shared access signature-URI is gekoppeld aan Hallo account key gebruikte toocreate Hallo handtekening en Hallo opgeslagen toegangsbeleid dat is gekoppeld (indien aanwezig).</span><span class="sxs-lookup"><span data-stu-id="d6719-149">A shared access signature URI is associated with hello account key used toocreate hello signature, and hello associated stored access policy (if any).</span></span> <span data-ttu-id="d6719-150">Als er geen opgeslagen toegangsbeleid is opgegeven, is hello alleen manier toorevoke een shared access signature toochange hello accountsleutel.</span><span class="sxs-lookup"><span data-stu-id="d6719-150">If no stored access policy is specified, hello only way toorevoke a shared access signature is toochange hello account key.</span></span>

<span data-ttu-id="d6719-151">Het is raadzaam om altijd opgeslagen toegangsbeleid te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6719-151">We recommend that you always use stored access policies.</span></span> <span data-ttu-id="d6719-152">Als u opgeslagen beleid, kunt u handtekeningen intrekken of vervaldatum Hallo uitbreiden naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="d6719-152">When using stored policies, you can either revoke signatures or extend hello expiry date as needed.</span></span> <span data-ttu-id="d6719-153">Hallo stappen in dit document wordt opgeslagen toegang beleid toogenerate SAS gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6719-153">hello steps in this document use stored access policies toogenerate SAS.</span></span>

<span data-ttu-id="d6719-154">Zie voor meer informatie over handtekeningen voor gedeelde toegang [Understanding Hallo SAS-model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="d6719-154">For more information on Shared Access Signatures, see [Understanding hello SAS model](../storage/common/storage-dotnet-shared-access-signature-part-1.md).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="d6719-155">Maak een opgeslagen beleid en de SAS met C\#</span><span class="sxs-lookup"><span data-stu-id="d6719-155">Create a stored policy and SAS using C\#</span></span>

1. <span data-ttu-id="d6719-156">Hallo-oplossing in Visual Studio openen.</span><span class="sxs-lookup"><span data-stu-id="d6719-156">Open hello solution in Visual Studio.</span></span>

2. <span data-ttu-id="d6719-157">Klik in Solution Explorer met de rechtermuisknop op Hallo **SASToken** project en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="d6719-157">In Solution Explorer, right-click on hello **SASToken** project and select **Properties**.</span></span>

3. <span data-ttu-id="d6719-158">Selecteer **instellingen** en waarden voor de volgende vermeldingen Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="d6719-158">Select **Settings** and add values for hello following entries:</span></span>

   * <span data-ttu-id="d6719-159">StorageConnectionString: Hallo verbinding tekenreeks voor Hallo storage-account dat u wilt dat toocreate een opgeslagen beleid en een SAS voor.</span><span class="sxs-lookup"><span data-stu-id="d6719-159">StorageConnectionString: hello connection string for hello storage account that you want toocreate a stored policy and SAS for.</span></span> <span data-ttu-id="d6719-160">Hallo-indeling moet `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` waar `myaccount` Hallo-naam van uw opslagaccount en `mykey` is Hallo-sleutel voor Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="d6719-160">hello format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is hello name of your storage account and `mykey` is hello key for hello storage account.</span></span>

   * <span data-ttu-id="d6719-161">ContainerName: Hallo-container in Hallo storage-account die u wilt dat de toegang tot toorestrict.</span><span class="sxs-lookup"><span data-stu-id="d6719-161">ContainerName: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="d6719-162">SASPolicyName: Hallo naam toouse voor Hallo opgeslagen beleid toocreate.</span><span class="sxs-lookup"><span data-stu-id="d6719-162">SASPolicyName: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="d6719-163">FileToUpload: Hallo pad tooa bestand dat is geüpload toohello container.</span><span class="sxs-lookup"><span data-stu-id="d6719-163">FileToUpload: hello path tooa file that is uploaded toohello container.</span></span>

4. <span data-ttu-id="d6719-164">Hallo-project uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d6719-164">Run hello project.</span></span> <span data-ttu-id="d6719-165">Informatie vergelijkbare toohello na de tekst wordt weergegeven zodra Hallo SAS is gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="d6719-165">Information similar toohello following text is displayed once hello SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="d6719-166">Hallo SAS-beleid token, opslagaccountnaam en containernaam opslaan.</span><span class="sxs-lookup"><span data-stu-id="d6719-166">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="d6719-167">Deze waarden worden gebruikt wanneer Hallo storage-account koppelen aan uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-167">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="d6719-168">Maak een opgeslagen beleid en de SAS met behulp van Python</span><span class="sxs-lookup"><span data-stu-id="d6719-168">Create a stored policy and SAS using Python</span></span>

1. <span data-ttu-id="d6719-169">Open Hallo SASToken.py bestand en wijzig Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="d6719-169">Open hello SASToken.py file and change hello following values:</span></span>

   * <span data-ttu-id="d6719-170">beleid\_naam: Hallo naam toouse voor Hallo beleid toocreate opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d6719-170">policy\_name: hello name toouse for hello stored policy toocreate.</span></span>

   * <span data-ttu-id="d6719-171">opslag\_account\_naam: Hallo-naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="d6719-171">storage\_account\_name: hello name of your storage account.</span></span>

   * <span data-ttu-id="d6719-172">opslag\_account\_sleutel: Hallo-sleutel voor Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="d6719-172">storage\_account\_key: hello key for hello storage account.</span></span>

   * <span data-ttu-id="d6719-173">opslag\_container\_naam: Hallo-container in Hallo storage-account die u wilt dat de toegang tot toorestrict.</span><span class="sxs-lookup"><span data-stu-id="d6719-173">storage\_container\_name: hello container in hello storage account that you want toorestrict access to.</span></span>

   * <span data-ttu-id="d6719-174">voorbeeld\_bestand\_pad: Hallo pad tooa-bestand dat is geüpload toohello container.</span><span class="sxs-lookup"><span data-stu-id="d6719-174">example\_file\_path: hello path tooa file that is uploaded toohello container.</span></span>

2. <span data-ttu-id="d6719-175">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d6719-175">Run hello script.</span></span> <span data-ttu-id="d6719-176">Hallo SAS-token vergelijkbare toohello tekst volgen wanneer Hallo-script is voltooid wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d6719-176">It displays hello SAS token similar toohello following text when hello script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="d6719-177">Hallo SAS-beleid token, opslagaccountnaam en containernaam opslaan.</span><span class="sxs-lookup"><span data-stu-id="d6719-177">Save hello SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="d6719-178">Deze waarden worden gebruikt wanneer Hallo storage-account koppelen aan uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-178">These values are used when associating hello storage account with your HDInsight cluster.</span></span>

## <a name="use-hello-sas-with-hdinsight"></a><span data-ttu-id="d6719-179">Hallo SAS gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6719-179">Use hello SAS with HDInsight</span></span>

<span data-ttu-id="d6719-180">Wanneer u een HDInsight-cluster maakt, moet u een primaire opslagaccount opgeven en kunt u eventueel extra opslagaccounts opgeven.</span><span class="sxs-lookup"><span data-stu-id="d6719-180">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="d6719-181">Beide methoden voor het toevoegen van opslag vereist volledige toegang toohello storage-accounts en containers die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6719-181">Both of these methods of adding storage require full access toohello storage accounts and containers that are used.</span></span>

<span data-ttu-id="d6719-182">toouse een Shared Access Signature toolimit toegang tooa container, Voeg een aangepaste vermelding toohello **core site** configuratie voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-182">toouse a Shared Access Signature toolimit access tooa container, add a custom entry toohello **core-site** configuration for hello cluster.</span></span>

* <span data-ttu-id="d6719-183">Voor **Windows gebaseerde** of **op basis van Linux** HDInsight-clusters, kunt u Hallo-vermelding toevoegen tijdens het maken van het cluster met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d6719-183">For **Windows-based** or **Linux-based** HDInsight clusters, you can add hello entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="d6719-184">Voor **op basis van Linux** HDInsight-clusters Hallo configuratie na het maken van het cluster met Ambari wijzigen.</span><span class="sxs-lookup"><span data-stu-id="d6719-184">For **Linux-based** HDInsight clusters, change hello configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-hello-sas"></a><span data-ttu-id="d6719-185">Maken van een cluster dat gebruik maakt van Hallo SAS</span><span class="sxs-lookup"><span data-stu-id="d6719-185">Create a cluster that uses hello SAS</span></span>

<span data-ttu-id="d6719-186">Een voorbeeld van het maken van een HDInsight-cluster dat gebruik Hallo SAS is opgenomen in Hallo `CreateCluster` map van Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d6719-186">An example of creating an HDInsight cluster that uses hello SAS is included in hello `CreateCluster` directory of hello repository.</span></span> <span data-ttu-id="d6719-187">toouse ervan gebruik Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="d6719-187">toouse it, use hello following steps:</span></span>

1. <span data-ttu-id="d6719-188">Open Hallo `CreateCluster\HDInsightSAS.ps1` bestand in een teksteditor en wijzig Hallo waarden aan begin van document Hallo Hallo te volgen.</span><span class="sxs-lookup"><span data-stu-id="d6719-188">Open hello `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify hello following values at hello beginning of hello document.</span></span>

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    <span data-ttu-id="d6719-189">Wijzig bijvoorbeeld `'mycluster'` toohello naam Hallo-cluster dat u wilt dat toocreate.</span><span class="sxs-lookup"><span data-stu-id="d6719-189">For example, change `'mycluster'` toohello name of hello cluster you want toocreate.</span></span> <span data-ttu-id="d6719-190">Hallo SAS waarden moeten overeenkomen met waarden uit de vorige stappen Hallo Hallo biedt bij het maken van een opslagaccount en SAS-token.</span><span class="sxs-lookup"><span data-stu-id="d6719-190">hello SAS values should match hello values from hello previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="d6719-191">Zodra u Hallo waarden hebt gewijzigd, moet u Hallo bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="d6719-191">Once you have changed hello values, save hello file.</span></span>

2. <span data-ttu-id="d6719-192">Open een nieuw Azure PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="d6719-192">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="d6719-193">Als u niet bekend met Azure PowerShell bent of niet hebt geïnstalleerd, raadpleegt u [installeren en configureren van Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="d6719-193">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>

1. <span data-ttu-id="d6719-194">Gebruik vanaf Hallo prompt Hallo opdracht tooauthenticate tooyour Azure-abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6719-194">From hello prompt, use hello following command tooauthenticate tooyour Azure subscription:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="d6719-195">Wanneer u wordt gevraagd, aanmelden met Hallo-account voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="d6719-195">When prompted, log in with hello account for your Azure subscription.</span></span>

    <span data-ttu-id="d6719-196">Als uw account gekoppeld aan meerdere Azure-abonnementen is, moet u mogelijk toouse `Select-AzureRmSubscription` tooselect Hallo abonnement u toouse wenst.</span><span class="sxs-lookup"><span data-stu-id="d6719-196">If your account is associated with multiple Azure subscriptions, you may need toouse `Select-AzureRmSubscription` tooselect hello subscription you wish toouse.</span></span>

4. <span data-ttu-id="d6719-197">Wijzig vanaf Hallo-prompt mappen toohello `CreateCluster` directory die Hallo HDInsightSAS.ps1 bestand bevat.</span><span class="sxs-lookup"><span data-stu-id="d6719-197">From hello prompt, change directories toohello `CreateCluster` directory that contains hello HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="d6719-198">Gebruik vervolgens de volgende opdrachtscript toorun Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="d6719-198">Then use hello following command toorun hello script</span></span>

    ```powershell
    .\HDInsightSAS.ps1
    ```

    <span data-ttu-id="d6719-199">Als het Hallo-script wordt uitgevoerd, geregistreerd in het logboek uitvoer toohello PowerShell-prompt als het Hallo-resource groep en storage-accounts maakt.</span><span class="sxs-lookup"><span data-stu-id="d6719-199">As hello script runs, it logs output toohello PowerShell prompt as it creates hello resource group and storage accounts.</span></span> <span data-ttu-id="d6719-200">U bent na vragen aan gebruiker tooenter Hallo HTTP gebruiker voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-200">You are prompted tooenter hello HTTP user for hello HDInsight cluster.</span></span> <span data-ttu-id="d6719-201">Dit account is gebruikte toosecure HTTP/s toegang toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-201">This account is used toosecure HTTP/s access toohello cluster.</span></span>

    <span data-ttu-id="d6719-202">Als u een cluster op basis van Linux maakt, wordt u gevraagd om een SSH-gebruikersnaam voor account en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d6719-202">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="d6719-203">Dit account is gebruikte tooremotely toohello cluster aanmelden.</span><span class="sxs-lookup"><span data-stu-id="d6719-203">This account is used tooremotely log in toohello cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d6719-204">Als u wordt gevraagd om Hallo HTTP/s of SSH-gebruikersnaam en wachtwoord, moet u een wachtwoord dat voldoet aan de volgende criteria Hallo opgeven:</span><span class="sxs-lookup"><span data-stu-id="d6719-204">When prompted for hello HTTP/s or SSH user name and password, you must provide a password that meets hello following criteria:</span></span>
   >
   > * <span data-ttu-id="d6719-205">Ten minste 10 tekens lang moet zijn</span><span class="sxs-lookup"><span data-stu-id="d6719-205">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="d6719-206">Moet ten minste één cijfer bevatten</span><span class="sxs-lookup"><span data-stu-id="d6719-206">Must contain at least one digit</span></span>
   > * <span data-ttu-id="d6719-207">Moet ten minste één niet-alfanumeriek teken bevatten</span><span class="sxs-lookup"><span data-stu-id="d6719-207">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="d6719-208">Moet ten minste één hoofdletter of kleine letter bevatten</span><span class="sxs-lookup"><span data-stu-id="d6719-208">Must contain at least one upper or lower case letter</span></span>

<span data-ttu-id="d6719-209">Het duurt lang voordat deze toocomplete script meestal ongeveer 15 minuten.</span><span class="sxs-lookup"><span data-stu-id="d6719-209">It takes a while for this script toocomplete, usually around 15 minutes.</span></span> <span data-ttu-id="d6719-210">Wanneer het Hallo-script is voltooid zonder fouten, is Hallo-cluster gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d6719-210">When hello script completes without any errors, hello cluster has been created.</span></span>

### <a name="use-hello-sas-with-an-existing-cluster"></a><span data-ttu-id="d6719-211">Hallo SAS gebruiken met een bestaand cluster</span><span class="sxs-lookup"><span data-stu-id="d6719-211">Use hello SAS with an existing cluster</span></span>

<span data-ttu-id="d6719-212">Als u een bestaand cluster op basis van Linux hebt, kunt u Hallo SAS toohello toevoegen **core site** configuratie met behulp van Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6719-212">If you have an existing Linux-based cluster, you can add hello SAS toohello **core-site** configuration by using hello following steps:</span></span>

1. <span data-ttu-id="d6719-213">Open Hallo Ambari-webgebruikersinterface voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="d6719-213">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="d6719-214">Hallo-adres voor deze pagina is https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="d6719-214">hello address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="d6719-215">Wanneer u wordt gevraagd, worden geverifieerd toohello cluster met behulp van de naam van de serverbeheerder hello (admin) en het wachtwoord die u hebt gebruikt toen Hallo cluster maken.</span><span class="sxs-lookup"><span data-stu-id="d6719-215">When prompted, authenticate toohello cluster using hello admin name (admin) and password you used when creating hello cluster.</span></span>

2. <span data-ttu-id="d6719-216">Selecteer in het Hallo-zijde van Hallo Ambari-webgebruikersinterface links, **HDFS** en selecteer vervolgens Hallo **Configs** tabblad in het midden van de pagina Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6719-216">From hello left side of hello Ambari web UI, select **HDFS** and then select hello **Configs** tab in hello middle of hello page.</span></span>

3. <span data-ttu-id="d6719-217">Selecteer Hallo **Geavanceerd** tabblad en schuif totdat u Hallo **aangepaste core-site** sectie.</span><span class="sxs-lookup"><span data-stu-id="d6719-217">Select hello **Advanced** tab, and then scroll until you find hello **Custom core-site** section.</span></span>

4. <span data-ttu-id="d6719-218">Vouw Hallo **aangepaste core-site** sectie vervolgens schuiven toohello einde en selecteer Hallo **eigenschap toevoegen...**  koppeling.</span><span class="sxs-lookup"><span data-stu-id="d6719-218">Expand hello **Custom core-site** section, then scroll toohello end and select hello **Add property...** link.</span></span> <span data-ttu-id="d6719-219">Gebruik Hallo volgende waarden voor Hallo **sleutel** en **waarde** velden:</span><span class="sxs-lookup"><span data-stu-id="d6719-219">Use hello following values for hello **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="d6719-220">**Sleutel**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="d6719-220">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="d6719-221">**Waarde**: Hallo SAS geretourneerd door Hallo C# of Python-toepassing die u eerder hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d6719-221">**Value**: hello SAS returned by hello C# or Python application you ran previously</span></span>

     <span data-ttu-id="d6719-222">Vervang **CONTAINERNAME** met Hallo containernaam die u gebruikt met Hallo C# of SAS-toepassing.</span><span class="sxs-lookup"><span data-stu-id="d6719-222">Replace **CONTAINERNAME** with hello container name you used with hello C# or SAS application.</span></span> <span data-ttu-id="d6719-223">Vervang **STORAGEACCOUNTNAME** met Hallo opslagaccountnaam die u hebt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d6719-223">Replace **STORAGEACCOUNTNAME** with hello storage account name you used.</span></span>

5. <span data-ttu-id="d6719-224">Klik op Hallo **toevoegen** knop toosave deze sleutel en waarde en klik op Hallo **opslaan** knop toosave Hallo configuratiewijzigingen.</span><span class="sxs-lookup"><span data-stu-id="d6719-224">Click hello **Add** button toosave this key and value, then click hello **Save** button toosave hello configuration changes.</span></span> <span data-ttu-id="d6719-225">Wanneer u wordt gevraagd, een beschrijving van Hallo wijzigen ('toe te voegen toegang tot de SAS-opslag' bijvoorbeeld) toevoegen en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="d6719-225">When prompted, add a description of hello change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="d6719-226">Klik op **OK** wanneer Hallo wijzigingen zijn voltooid.</span><span class="sxs-lookup"><span data-stu-id="d6719-226">Click **OK** when hello changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="d6719-227">U moet verschillende services opnieuw starten voordat Hallo wijziging van kracht.</span><span class="sxs-lookup"><span data-stu-id="d6719-227">You must restart several services before hello change takes effect.</span></span>

6. <span data-ttu-id="d6719-228">In Hallo Ambari-webgebruikersinterface, selecteer **HDFS** in Hallo-lijst op Hallo links en selecteer vervolgens **start opnieuw alle** van Hallo **serviceacties** vervolgkeuzelijst op de juiste Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6719-228">In hello Ambari web UI, select **HDFS** from hello list on hello left, and then select **Restart All** from hello **Service Actions** drop down list on hello right.</span></span> <span data-ttu-id="d6719-229">Wanneer u wordt gevraagd, selecteert u **onderhoudsmodus inschakelen** en vervolgens selecteert __Conform alle opnieuw starten '.</span><span class="sxs-lookup"><span data-stu-id="d6719-229">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="d6719-230">Herhaal dit proces voor MapReduce2 en YARN.</span><span class="sxs-lookup"><span data-stu-id="d6719-230">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="d6719-231">Zodra het Hallo-services opnieuw hebt opgestart, selecteren en uitschakelen van onderhoudsmodus van Hallo **serviceacties** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="d6719-231">Once hello services have restarted, select each one and disable maintenance mode from hello **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="d6719-232">Testen met beperkte toegang</span><span class="sxs-lookup"><span data-stu-id="d6719-232">Test restricted access</span></span>

<span data-ttu-id="d6719-233">tooverify die hebt u beperkte toegang, gebruik Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="d6719-233">tooverify that you have restricted access, use hello following methods:</span></span>

* <span data-ttu-id="d6719-234">Voor **Windows gebaseerde** HDInsight-clusters, extern bureaublad tooconnect toohello cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6719-234">For **Windows-based** HDInsight clusters, use Remote Desktop tooconnect toohello cluster.</span></span> <span data-ttu-id="d6719-235">Zie voor meer informatie [tooHDInsight met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="d6719-235">For more information, see [Connect tooHDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="d6719-236">Eenmaal zijn verbonden, gebruikt u Hallo **Hadoop opdrachtregelprogramma** pictogram op Hallo bureaublad tooopen vanaf de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="d6719-236">Once connected, use hello **Hadoop Command-Line** icon on hello desktop tooopen a command prompt.</span></span>

* <span data-ttu-id="d6719-237">Voor **op basis van Linux** SSH tooconnect toohello cluster voor HDInsight-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d6719-237">For **Linux-based** HDInsight clusters, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="d6719-238">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d6719-238">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="d6719-239">Eenmaal zijn verbonden toohello cluster, gebruikt u Hallo stappen tooverify kunt u alleen lezen en de lijst met items op Hallo SAS storage-account te volgen:</span><span class="sxs-lookup"><span data-stu-id="d6719-239">Once connected toohello cluster, use hello following steps tooverify that you can only read and list items on hello SAS storage account:</span></span>

1. <span data-ttu-id="d6719-240">toolist hello inhoud van de container hello, Hallo volgende opdracht uit Hallo prompt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d6719-240">toolist hello contents of hello container, use hello following command from hello prompt:</span></span> 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    <span data-ttu-id="d6719-241">Vervang **SASCONTAINER** met de naam van de Hallo van Hallo-container gemaakt voor Hallo SAS storage-account.</span><span class="sxs-lookup"><span data-stu-id="d6719-241">Replace **SASCONTAINER** with hello name of hello container created for hello SAS storage account.</span></span> <span data-ttu-id="d6719-242">Vervang **SASACCOUNTNAME** met de naam Hallo van Hallo storage-account gebruikt voor Hallo SAS.</span><span class="sxs-lookup"><span data-stu-id="d6719-242">Replace **SASACCOUNTNAME** with hello name of hello storage account used for hello SAS.</span></span>

    <span data-ttu-id="d6719-243">Hallo-lijst bevat Hallo bestand geüpload wanneer Hallo-container en SAS zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d6719-243">hello list includes hello file uploaded when hello container and SAS were created.</span></span>

2. <span data-ttu-id="d6719-244">Gebruik Hallo volgende opdracht tooverify dat u inhoud Hallo van Hallo-bestand kan lezen.</span><span class="sxs-lookup"><span data-stu-id="d6719-244">Use hello following command tooverify that you can read hello contents of hello file.</span></span> <span data-ttu-id="d6719-245">Vervang Hallo **SASCONTAINER** en **SASACCOUNTNAME** zoals in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="d6719-245">Replace hello **SASCONTAINER** and **SASACCOUNTNAME** as in hello previous step.</span></span> <span data-ttu-id="d6719-246">Vervang **FILENAME** met de naam van Hallo-bestand weergegeven in de vorige opdracht Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6719-246">Replace **FILENAME** with hello name of hello file displayed in hello previous command:</span></span>

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    <span data-ttu-id="d6719-247">Met deze opdracht worden Hallo inhoud van Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="d6719-247">This command lists hello contents of hello file.</span></span>

3. <span data-ttu-id="d6719-248">Hallo opdracht toodownload Hallo bestand toohello lokaal bestandssysteem volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d6719-248">Use hello following command toodownload hello file toohello local file system:</span></span>

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    <span data-ttu-id="d6719-249">Met deze opdracht downloads Hallo tooa lokale bestand met de naam **testbestand.txt**.</span><span class="sxs-lookup"><span data-stu-id="d6719-249">This command downloads hello file tooa local file named **testfile.txt**.</span></span>

4. <span data-ttu-id="d6719-250">Gebruik Hallo volgende opdracht tooupload Hallo lokaal bestand tooa nieuw bestand met de naam **testupload.txt** op Hallo SAS-opslag:</span><span class="sxs-lookup"><span data-stu-id="d6719-250">Use hello following command tooupload hello local file tooa new file named **testupload.txt** on hello SAS storage:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    <span data-ttu-id="d6719-251">U ontvangt een bericht vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d6719-251">You receive a message similar toohello following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="d6719-252">Deze fout treedt op omdat de opslaglocatie Hallo lezen + alleen lijst.</span><span class="sxs-lookup"><span data-stu-id="d6719-252">This error occurs because hello storage location is read+list only.</span></span> <span data-ttu-id="d6719-253">Gebruik Hallo volgende opdracht tooput Hallo gegevens op Hallo standaard opslag voor Hallo-cluster kunnen geschreven worden:</span><span class="sxs-lookup"><span data-stu-id="d6719-253">Use hello following command tooput hello data on hello default storage for hello cluster, which is writable:</span></span>

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    <span data-ttu-id="d6719-254">Deze tijd Hallo-bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d6719-254">This time, hello operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d6719-255">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d6719-255">Troubleshooting</span></span>

### <a name="a-task-was-canceled"></a><span data-ttu-id="d6719-256">Een taak is geannuleerd</span><span class="sxs-lookup"><span data-stu-id="d6719-256">A task was canceled</span></span>

<span data-ttu-id="d6719-257">**Symptomen**: bij het maken van een cluster met behulp van PowerShell-script hello, krijgt u Hallo volgende foutbericht weergegeven:</span><span class="sxs-lookup"><span data-stu-id="d6719-257">**Symptoms**: When creating a cluster using hello PowerShell script, you may receive hello following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="d6719-258">**Oorzaak**: deze fout kan optreden als u een wachtwoord voor Hallo beheerder/HTTP-gebruiker voor Hallo cluster of (voor op basis van Linux-clusters) Hallo SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="d6719-258">**Cause**: This error can occur if you use a password for hello admin/HTTP user for hello cluster, or (for Linux-based clusters) hello SSH user.</span></span>

<span data-ttu-id="d6719-259">**Resolutie**: geen wachtwoord gebruiken dat voldoet aan de volgende criteria Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6719-259">**Resolution**: Use a password that meets hello following criteria:</span></span>

* <span data-ttu-id="d6719-260">Ten minste 10 tekens lang moet zijn</span><span class="sxs-lookup"><span data-stu-id="d6719-260">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="d6719-261">Moet ten minste één cijfer bevatten</span><span class="sxs-lookup"><span data-stu-id="d6719-261">Must contain at least one digit</span></span>
* <span data-ttu-id="d6719-262">Moet ten minste één niet-alfanumeriek teken bevatten</span><span class="sxs-lookup"><span data-stu-id="d6719-262">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="d6719-263">Moet ten minste één hoofdletter of kleine letter bevatten</span><span class="sxs-lookup"><span data-stu-id="d6719-263">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6719-264">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6719-264">Next steps</span></span>

<span data-ttu-id="d6719-265">U hebt geleerd hoe tooadd opslag met beperkte toegang tooyour HDInsight-cluster, informatie over andere manieren toowork met gegevens op het cluster:</span><span class="sxs-lookup"><span data-stu-id="d6719-265">Now that you have learned how tooadd limited-access storage tooyour HDInsight cluster, learn other ways toowork with data on your cluster:</span></span>

* [<span data-ttu-id="d6719-266">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6719-266">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d6719-267">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6719-267">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d6719-268">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6719-268">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs

---
title: Met behulp van scriptacties - Azure HDInsight-clusters aanpassen | Microsoft Docs
description: Aangepaste onderdelen toevoegen op Linux gebaseerde HDInsight-clusters met behulp van scriptacties. Scriptacties zijn Bash-scripts die kunnen worden gebruikt voor het aanpassen van de configuratie van het cluster of Voeg extra services en hulpprogramma's zoals Hue, Solr of R.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48e85f53-87c1-474f-b767-ca772238cc13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 0c5d00b6cb9f68a1a0e474f81c969eb1b5654c67
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="9b3d3-104">Linux gebaseerde HDInsight-clusters met behulp van de scriptactie aanpassen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="9b3d3-105">HDInsight biedt een configuratieoptie aangeroepen **scriptactie** die aangepaste scripts die aanpassen van het cluster wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize the cluster.</span></span> <span data-ttu-id="9b3d3-106">Deze scripts worden gebruikt voor het installeren van extra onderdelen en configuratie-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-106">These scripts are used to install additional components and change configuration settings.</span></span> <span data-ttu-id="9b3d3-107">Scriptacties kunnen worden gebruikt tijdens of na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3d3-108">De mogelijkheid om met scriptacties op een cluster al actief is alleen beschikbaar voor Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-108">The ability to use script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="9b3d3-109">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9b3d3-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="9b3d3-111">Scriptacties kunnen ook worden gepubliceerd naar Azure Marketplace als een HDInsight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-111">Script actions can also be published to the Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="9b3d3-112">Sommige van de voorbeelden in dit document laten zien hoe u een HDInsight-toepassing met behulp van actie-scriptopdrachten van PowerShell en de .NET SDK kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-112">Some of the examples in this document show how you can install an HDInsight application using script action commands from PowerShell and the .NET SDK.</span></span> <span data-ttu-id="9b3d3-113">Zie voor meer informatie over HDInsight-toepassingen [publiceren HDInsight-toepassingen in Azure Marketplace](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-113">For more information on HDInsight applications, see [Publish HDInsight applications into the Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="9b3d3-114">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-114">Permissions</span></span>

<span data-ttu-id="9b3d3-115">Als u van een domein HDInsight-cluster gebruikmaakt, zijn er twee Ambari-machtigingen die vereist zijn bij het gebruik van scriptacties met het cluster:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with the cluster:</span></span>

* <span data-ttu-id="9b3d3-116">**AMBARI. Voer\_aangepaste\_opdracht**: de Ambari-beheerdersrol beschikt over deze machtiging standaard.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: The Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="9b3d3-117">**HET CLUSTER. Voer\_aangepaste\_opdracht**: zowel de HDInsight-Clusterbeheer en Ambari beheerder hebben deze machtiging standaard.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both the HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="9b3d3-118">Zie voor meer informatie over het werken met machtigingen met HDInsight domein [domein HDInsight-clusters beheren](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="9b3d3-119">Toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="9b3d3-119">Access control</span></span>

<span data-ttu-id="9b3d3-120">Als u niet de beheerder of de eigenaar van uw Azure-abonnement, uw account moet er ten minste **Inzender** toegang tot de resourcegroep die het HDInsight-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-120">If you are not the administrator/owner of your Azure subscription, your account must have at least **Contributor** access to the resource group that contains the HDInsight cluster.</span></span>

<span data-ttu-id="9b3d3-121">Bovendien, als u een HDInsight-cluster iemand met ten minste maakt **Inzender** toegang tot het Azure-abonnement moet hebben eerder geregistreerd de provider voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access to the Azure subscription must have previously registered the provider for HDInsight.</span></span> <span data-ttu-id="9b3d3-122">Registratie van een provider vindt plaats wanneer een gebruiker met toegang tot het abonnement op het niveau van Inzender, voor het eerst een resource maakt onder het abonnement.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-122">Provider registration happens when a user with Contributor access to the subscription creates a resource for the first time on the subscription.</span></span> <span data-ttu-id="9b3d3-123">Dit kan ook worden bereikt zonder dat er een resource wordt gemaakt door [een provider te registreren met behulp van REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="9b3d3-124">Zie de volgende documenten voor meer informatie over werken met toegangsbeheer:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-124">For more information on working with access management, see the following documents:</span></span>

* [<span data-ttu-id="9b3d3-125">Aan de slag met toegangsbeheer in Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9b3d3-125">Get started with access management in the Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="9b3d3-126">Roltoewijzingen gebruiken voor het beheer van de toegang tot de resources van uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="9b3d3-126">Use role assignments to manage access to your Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="9b3d3-127">Understanding scriptacties</span><span class="sxs-lookup"><span data-stu-id="9b3d3-127">Understanding Script Actions</span></span>

<span data-ttu-id="9b3d3-128">Een scriptactie is gewoon een Bash-script dat u een URI te bieden en parameters voor.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="9b3d3-129">Het script wordt uitgevoerd op knooppunten in het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-129">The script runs on nodes in the HDInsight cluster.</span></span> <span data-ttu-id="9b3d3-130">Hieronder vindt u kenmerken en functies van scriptacties.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-130">The following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="9b3d3-131">Moet worden opgeslagen op een URI die toegankelijk is vanaf het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-131">Must be stored on a URI that is accessible from the HDInsight cluster.</span></span> <span data-ttu-id="9b3d3-132">Hier volgen de mogelijke opslaglocaties:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-132">The following are possible storage locations:</span></span>

    * <span data-ttu-id="9b3d3-133">Een **Azure Data Lake Store** account die toegankelijk is voor het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-133">An **Azure Data Lake Store** account that is accessible by the HDInsight cluster.</span></span> <span data-ttu-id="9b3d3-134">Zie voor meer informatie over het gebruik van Azure Data Lake Store met HDInsight [een HDInsight-cluster maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="9b3d3-135">Wanneer u een script dat is opgeslagen in Data Lake Store, de indeling van de URI is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-135">When using a script stored in Data Lake Store, the URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="9b3d3-136">De service-principal die hdinsight gebruikt voor toegang tot Data Lake Store moet leestoegang hebben tot het script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-136">The service principal HDInsight uses to access Data Lake Store must have read access to the script.</span></span>

    * <span data-ttu-id="9b3d3-137">Een blob in een **Azure Storage-account** die beide het primaire of extra storage-account voor het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-137">A blob in an **Azure Storage account** that is either the primary or additional storage account for the HDInsight cluster.</span></span> <span data-ttu-id="9b3d3-138">HDInsight is toegang verleend tot beide typen opslagaccounts tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-138">HDInsight is granted access to both of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="9b3d3-139">Bestand met een openbare sharing-service zoals Azure Blob, GitHub, OneDrive, Dropbox, enz.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="9b3d3-140">Bijvoorbeeld URI's, Zie de [voorbeeldscripts script actie](#example-script-action-scripts) sectie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-140">For example URIs, see the [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="9b3d3-141">HDInsight biedt alleen ondersteuning voor __algemeen__ Azure Storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="9b3d3-142">Het momenteel geen ondersteunt de __Blob storage__ accounttype.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-142">It does not currently support the __Blob storage__ account type.</span></span>

* <span data-ttu-id="9b3d3-143">Kan worden beperkt tot **uitvoeren op alleen bepaalde knooppunttypen**voor voorbeeld hoofdknooppunten of worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-143">Can be restricted to **run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9b3d3-144">Wanneer gebruikt met HDInsight Premium, kunt u opgeven dat het script moet worden gebruikt op de edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-144">When used with HDInsight Premium, you can specify that the script should be used on the edge node.</span></span>

* <span data-ttu-id="9b3d3-145">Kan **persistent** of **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="9b3d3-146">**Persistent** scripts worden toegepast op de worker-knooppunten aan het cluster worden toegevoegd nadat het script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-146">**Persisted** scripts are applied to worker nodes added to the cluster after the script runs.</span></span> <span data-ttu-id="9b3d3-147">Bijvoorbeeld wanneer het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-147">For example, when scaling up the cluster.</span></span>

    <span data-ttu-id="9b3d3-148">Een persistent script mogelijk ook wijzigingen toepassen op een ander knooppunttype, zoals een hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-148">A persisted script might also apply changes to another node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9b3d3-149">Persistente scriptacties moeten een unieke naam hebben.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="9b3d3-150">**Ad hoc** scripts blijven niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="9b3d3-151">Ze worden niet toegepast op de worker-knooppunten aan het cluster worden toegevoegd nadat het script is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-151">They are not applied to worker nodes added to the cluster after the script has ran.</span></span> <span data-ttu-id="9b3d3-152">U kunt vervolgens promoveren van een ad-hoc script een persistent script of degraderen van een persistent script naar een ad-hoc-script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-152">You can subsequently promote an ad hoc script to a persisted script, or demote a persisted script to an ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9b3d3-153">Scriptacties gebruikt tijdens het maken van het cluster worden automatisch doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="9b3d3-154">Scripts die mislukken niet persistent hebt gemaakt, zelfs als u specifiek aangeeft dat ze moeten worden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="9b3d3-155">Kan accepteren **parameters** die door het script worden gebruikt tijdens de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-155">Can accept **parameters** that are used by the script during execution.</span></span>
* <span data-ttu-id="9b3d3-156">Voer met **root bevoegdheden** op de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-156">Run with **root level privileges** on the cluster nodes.</span></span>
* <span data-ttu-id="9b3d3-157">Kan worden gebruikt via de **Azure-portal**, **Azure PowerShell**, **Azure CLI**, of **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-157">Can be used through the **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="9b3d3-158">Het cluster houdt een geschiedenis van alle scripts die hebben is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-158">The cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="9b3d3-159">De geschiedenis is handig als u moet de ID van een script voor promotie of degradatie bewerkingen vinden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-159">The history is useful when you need to find the ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3d3-160">Er is geen automatische manier om de wijzigingen die door een scriptactie ongedaan te maken.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-160">There is no automatic way to undo the changes made by a script action.</span></span> <span data-ttu-id="9b3d3-161">Handmatig de wijzigingen ongedaan maken of een script dat wordt teruggedraaid ze bieden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-161">Either manually reverse the changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="9b3d3-162">Scriptactie in het proces voor het cluster maken</span><span class="sxs-lookup"><span data-stu-id="9b3d3-162">Script Action in the cluster creation process</span></span>

<span data-ttu-id="9b3d3-163">Scriptacties gebruikt tijdens het maken van het cluster zijn enigszins afwijken van het script acties worden uitgevoerd op een bestaand cluster:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="9b3d3-164">Het script is **automatisch persistente**.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-164">The script is **automatically persisted**.</span></span>
* <span data-ttu-id="9b3d3-165">Een **fout** in het script kan ertoe leiden dat het maakproces cluster mislukken.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-165">A **failure** in the script can cause the cluster creation process to fail.</span></span>

<span data-ttu-id="9b3d3-166">Het volgende diagram illustreert wanneer het Script wordt uitgevoerd tijdens het maken:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-166">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="9b3d3-167">![Aanpassing van HDInsight-cluster en fasen tijdens het maken van het cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="9b3d3-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="9b3d3-168">Het script wordt uitgevoerd terwijl HDInsight wordt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-168">The script runs while HDInsight is being configured.</span></span> <span data-ttu-id="9b3d3-169">In deze fase wordt het script wordt parallel uitgevoerd op de opgegeven knooppunten in het cluster en uitgevoerd met basis-bevoegdheden op de knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-169">At this stage, the script runs in parallel on all the specified nodes in the cluster, and runs with root privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="9b3d3-170">Omdat het script wordt uitgevoerd met het niveau bevoegdheid hoofdmap op de clusterknooppunten, kunt u bewerkingen zoals het stoppen en starten van services, met inbegrip van Hadoop-gerelateerde services kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-170">Because the script runs with root level privilege on the cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="9b3d3-171">Als u services stoppen, moet u ervoor zorgen dat de Ambari-service en andere Hadoop-gerelateerde services actief zijn voordat het script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-171">If you stop services, you must ensure that the Ambari service and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="9b3d3-172">Deze services zijn vereist om te bepalen is de status en de status van het cluster terwijl deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-172">These services are required to successfully determine the health and state of the cluster while it is being created.</span></span>


<span data-ttu-id="9b3d3-173">U kunt meerdere scriptacties tegelijk gebruiken tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="9b3d3-174">Deze scripts worden aangeroepen in de volgorde waarin ze zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-174">These scripts are invoked in the order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3d3-175">Scriptacties moeten binnen 60 minuten of time-out voltooien.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="9b3d3-176">Het script wordt uitgevoerd tijdens de clusterinrichting, samen met andere processen installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-176">During cluster provisioning, the script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="9b3d3-177">Concurrentie voor resources, zoals CPU-tijd of netwerk bandbreedte kan ertoe leiden dat het script duurt langer dan in uw ontwikkelomgeving te voltooien.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-177">Competition for resources such as CPU time or network bandwidth may cause the script to take longer to finish than it does in your development environment.</span></span>
>
> <span data-ttu-id="9b3d3-178">Als u wilt de tijd minimaliseren nodig die is om te voorkomen dat taken zoals het downloaden en toepassingen van bron compileren uit te voeren van het script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-178">To minimize the time it takes to run the script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="9b3d3-179">Toepassingen vooraf gecompileerd en het binaire bestand opslaan in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-179">Pre-compile applications and store the binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="9b3d3-180">Scriptactie op een actief cluster</span><span class="sxs-lookup"><span data-stu-id="9b3d3-180">Script action on a running cluster</span></span>

<span data-ttu-id="9b3d3-181">In tegenstelling tot script acties die worden gebruikt tijdens het maken van het cluster een fout in een script uitgevoerd op een al actief cluster tot niet automatisch het cluster te wijzigen in een mislukte status.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause the cluster to change to a failed state.</span></span> <span data-ttu-id="9b3d3-182">Zodra een script is voltooid, moet het cluster naar een status 'actief' retourneren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-182">Once a script completes, the cluster should return to a "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9b3d3-183">Zelfs als het cluster heeft een status 'actief', bevatten het mislukte script verbroken dingen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-183">Even if the cluster has a 'running' state, the failed script may have broken things.</span></span> <span data-ttu-id="9b3d3-184">Een script kan bijvoorbeeld bestanden die nodig zijn door het cluster te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-184">For example, a script could delete files needed by the cluster.</span></span>
>
> <span data-ttu-id="9b3d3-185">Scripts acties uitgevoerd met bevoegdheden van de hoofdmap, dus moet u ervoor zorgen dat u wat een script doet begrijpt voordat u deze toepast op uw cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it to your cluster.</span></span>

<span data-ttu-id="9b3d3-186">Bij het toepassen van een script naar een cluster wordt de clusterstatus verandert van **met** naar **geaccepteerde**, vervolgens **HDInsight configuratie**, en ten slotte terug naar **met** voor geslaagde scripts.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-186">When applying a script to a cluster, the cluster state changes to from **Running** to **Accepted**, then **HDInsight configuration**, and finally back to **Running** for successful scripts.</span></span> <span data-ttu-id="9b3d3-187">De scriptstatus wordt geregistreerd in de geschiedenis van de scriptactie en u kunt deze informatie gebruiken om te bepalen of het script is geslaagd of mislukt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-187">The script status is logged in the script action history, and you can use this information to determine whether the script succeeded or failed.</span></span> <span data-ttu-id="9b3d3-188">Bijvoorbeeld, de `Get-AzureRmHDInsightScriptActionHistory` PowerShell-cmdlet kan worden gebruikt om de status van een script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-188">For example, the `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used to view the status of a script.</span></span> <span data-ttu-id="9b3d3-189">Gegevens worden geretourneerd vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-189">It returns information similar to the following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="9b3d3-190">Als u kunt het wachtwoord van de cluster-gebruiker (admin) zijn gewijzigd nadat het cluster is gemaakt, mislukken script acties uitgevoerd op dit cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-190">If you have changed the cluster user (admin) password after the cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="9b3d3-191">Als u een persistente scriptacties die doel worker-knooppunten hebt, mislukken deze scripts wanneer u de schaal van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale the cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="9b3d3-192">Voorbeeld van de scriptactie scripts</span><span class="sxs-lookup"><span data-stu-id="9b3d3-192">Example Script Action scripts</span></span>

<span data-ttu-id="9b3d3-193">Script actie scripts kunnen worden gebruikt door de volgende hulpprogramma's:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-193">Script Action scripts can be used through the following utilities:</span></span>

* <span data-ttu-id="9b3d3-194">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="9b3d3-194">Azure portal</span></span>
* <span data-ttu-id="9b3d3-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b3d3-195">Azure PowerShell</span></span>
* <span data-ttu-id="9b3d3-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b3d3-196">Azure CLI</span></span>
* <span data-ttu-id="9b3d3-197">HDInsight .NET-SDK</span><span class="sxs-lookup"><span data-stu-id="9b3d3-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="9b3d3-198">HDInsight biedt scripts voor het installeren van de volgende onderdelen op HDInsight-clusters:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-198">HDInsight provides scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="9b3d3-199">Naam</span><span class="sxs-lookup"><span data-stu-id="9b3d3-199">Name</span></span> | <span data-ttu-id="9b3d3-200">Script</span><span class="sxs-lookup"><span data-stu-id="9b3d3-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="9b3d3-201">**Een Azure Storage-account toevoegen**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="9b3d3-202">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-account-v01.sh. Zie [extra opslag toevoegen aan een HDInsight-cluster](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage to an HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="9b3d3-203">**Hue installeren**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-203">**Install Hue**</span></span> |<span data-ttu-id="9b3d3-204">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/Install-HUE-uber-v02.sh. Zie [installeert en gebruikt Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="9b3d3-205">**Functie installeren**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-205">**Install Presto**</span></span> |<span data-ttu-id="9b3d3-206">https://RAW.githubusercontent.com/hdinsight/Presto-hdinsight/master/installpresto.sh. Zie [installeert en gebruikt de functie op HDInsight-clusters](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="9b3d3-207">**Solr installeren**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-207">**Install Solr**</span></span> |<span data-ttu-id="9b3d3-208">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.sh. Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="9b3d3-209">**Giraph installeren**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-209">**Install Giraph**</span></span> |<span data-ttu-id="9b3d3-210">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.sh. Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="9b3d3-211">**Vooraf laden Hive-bibliotheken**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="9b3d3-212">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Zie [toevoegen Hive-bibliotheken op HDInsight-clusters](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="9b3d3-213">**Mono installeren of bijwerken**</span><span class="sxs-lookup"><span data-stu-id="9b3d3-213">**Install or update Mono**</span></span> | <span data-ttu-id="9b3d3-214">https://hdiconfigactions.BLOB.Core.Windows.NET/Install-mono/Install-mono.Bash.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="9b3d3-215">Zie [installeren of update Mono op HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="9b3d3-216">Een actie Script gebruiken tijdens het maken van het cluster</span><span class="sxs-lookup"><span data-stu-id="9b3d3-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="9b3d3-217">Deze sectie vindt u voorbeelden van de verschillende manieren waarop die u scriptacties gebruiken kunt bij het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-217">This section provides examples on the different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-azure-portal"></a><span data-ttu-id="9b3d3-218">Een actie Script gebruiken tijdens het maken van de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9b3d3-218">Use a Script Action during cluster creation from the Azure portal</span></span>

1. <span data-ttu-id="9b3d3-219">Beginnen met het maken van een cluster, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="9b3d3-220">Stoppen wanneer u bereikt de __Cluster samenvatting__ sectie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-220">Stop when you reach the __Cluster summary__ section.</span></span>

2. <span data-ttu-id="9b3d3-221">Van de __Cluster samenvatting__ sectie, selecteer de __bewerken__ koppelen voor __geavanceerde instellingen__.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-221">From the __Cluster summary__ section, select the __edit__ link for __Advanced settings__.</span></span>

    ![Koppeling van de geavanceerde instellingen](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="9b3d3-223">Van de __geavanceerde instellingen__ sectie __acties Script__.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-223">From the __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="9b3d3-224">Van de __acties Script__ sectie __+ nieuw verzenden__</span><span class="sxs-lookup"><span data-stu-id="9b3d3-224">From the __Script actions__ section, select __+ Submit new__</span></span>

    ![Een nieuwe scriptactie verzenden](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="9b3d3-226">Gebruik de __selecteert u een script__ item naar een vooraf gemaakte script te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-226">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="9b3d3-227">Selecteer voor het gebruik van een aangepast script __aangepaste__ en geef vervolgens de __naam__ en __Bash script URI__ voor uw script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-227">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Een script in de vorm Selecteer script toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="9b3d3-229">De volgende tabel beschrijft de elementen in het formulier:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-229">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="9b3d3-230">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9b3d3-230">Property</span></span> | <span data-ttu-id="9b3d3-231">Waarde</span><span class="sxs-lookup"><span data-stu-id="9b3d3-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9b3d3-232">Selecteer een script</span><span class="sxs-lookup"><span data-stu-id="9b3d3-232">Select a script</span></span> | <span data-ttu-id="9b3d3-233">Selecteer voor het gebruik van uw eigen script __aangepaste__.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-233">To use your own script, select __Custom__.</span></span> <span data-ttu-id="9b3d3-234">Anders selecteert u een van de opgegeven scripts.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-234">Otherwise, select one of the provided scripts.</span></span> |
    | <span data-ttu-id="9b3d3-235">Naam</span><span class="sxs-lookup"><span data-stu-id="9b3d3-235">Name</span></span> |<span data-ttu-id="9b3d3-236">Geef een naam voor de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-236">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="9b3d3-237">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="9b3d3-237">Bash script URI</span></span> |<span data-ttu-id="9b3d3-238">Geef de URI moet het script dat wordt opgeroepen voor het aanpassen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-238">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="9b3d3-239">Worker-HEAD/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="9b3d3-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="9b3d3-240">Geef de knooppunten (**Head**, **Worker**, of **ZooKeeper**) op waarmee het script aanpassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-240">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="9b3d3-241">Parameters</span><span class="sxs-lookup"><span data-stu-id="9b3d3-241">Parameters</span></span> |<span data-ttu-id="9b3d3-242">Geef de parameters op, indien vereist door het script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-242">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="9b3d3-243">Gebruik de __deze scriptactie__ vermelding om ervoor te zorgen dat het script wordt toegepast tijdens het schalen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-243">Use the __Persist this script action__ entry to ensure that the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="9b3d3-244">Selecteer __maken__ om op te slaan van het script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-244">Select __Create__ to save the script.</span></span> <span data-ttu-id="9b3d3-245">Vervolgens kunt u __+ indienen nieuwe__ toevoegen van een ander script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-245">You can then use __+ Submit new__ to add another script.</span></span>

    ![Meerdere scriptacties](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="9b3d3-247">Wanneer u klaar bent met het toe te voegen scripts gebruiken de __Selecteer__ knop, en vervolgens de __volgende__ terug te keren naar de __Cluster samenvatting__ sectie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-247">When you are done adding scripts, use the __Select__ button, and then the __Next__ button to return to the __Cluster summary__ section.</span></span>

3. <span data-ttu-id="9b3d3-248">Voor het maken van het cluster selecteert __maken__ van de __Cluster samenvatting__ selectie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-248">To create the cluster, select __Create__ from the __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="9b3d3-249">Gebruik de actie van een Script van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="9b3d3-250">De voorbeelden in deze sectie laten zien hoe het gebruik van scriptacties met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-250">The examples in this section demonstrate how to use script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="9b3d3-251">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="9b3d3-251">Before you begin</span></span>

* <span data-ttu-id="9b3d3-252">Zie voor meer informatie over het configureren van een werkstation als HDInsight Powershell-cmdlets wilt uitvoeren, [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-252">For information about configuring a workstation to run HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="9b3d3-253">Zie voor instructies over het maken van sjablonen [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-253">For instructions on how to create templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="9b3d3-254">Als u niet eerder hebt gebruikt Azure PowerShell met Resource Manager, raadpleegt u [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="9b3d3-255">Maken van clusters met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="9b3d3-256">Kopieer de volgende sjabloon naar een locatie op uw computer.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-256">Copy the following template to a location on your computer.</span></span> <span data-ttu-id="9b3d3-257">Deze sjabloon wordt Giraph geïnstalleerd op de headnodes en worker-knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-257">This template installs Giraph on the headnodes and worker nodes in the cluster.</span></span> <span data-ttu-id="9b3d3-258">U kunt ook controleren of het JSON-sjabloon geldig is.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-258">You can also verify if the JSON template is valid.</span></span> <span data-ttu-id="9b3d3-259">Plak de inhoud in sjabloon [JSONLint](http://jsonlint.com/), een online JSON-validatiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

            {
            "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
            "contentVersion": "1.0.0.0",
            "parameters": {
                "clusterLocation": {
                    "type": "string",
                    "defaultValue": "West US",
                    "allowedValues": [ "West US" ]
                },
                "clusterName": {
                    "type": "string"
                },
                "clusterUserName": {
                    "type": "string",
                    "defaultValue": "admin"
                },
                "clusterUserPassword": {
                    "type": "securestring"
                },
                "sshUserName": {
                    "type": "string",
                    "defaultValue": "username"
                },
                "sshPassword": {
                    "type": "securestring"
                },
                "clusterStorageAccountName": {
                    "type": "string"
                },
                "clusterStorageAccountResourceGroup": {
                    "type": "string"
                },
                "clusterStorageType": {
                    "type": "string",
                    "defaultValue": "Standard_LRS",
                    "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS"
                    ]
                },
                "clusterStorageAccountContainer": {
                    "type": "string"
                },
                "clusterHeadNodeCount": {
                    "type": "int",
                    "defaultValue": 1
                },
                "clusterWorkerNodeCount": {
                    "type": "int",
                    "defaultValue": 2
                }
            },
            "variables": {
            },
            "resources": [
                {
                    "name": "[parameters('clusterStorageAccountName')]",
                    "type": "Microsoft.Storage/storageAccounts",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-05-01-preview",
                    "dependsOn": [ ],
                    "tags": { },
                    "properties": {
                        "accountType": "[parameters('clusterStorageType')]"
                    }
                },
                {
                    "name": "[parameters('clusterName')]",
                    "type": "Microsoft.HDInsight/clusters",
                    "location": "[parameters('clusterLocation')]",
                    "apiVersion": "2015-03-01-preview",
                    "dependsOn": [
                        "[concat('Microsoft.Storage/storageAccounts/', parameters('clusterStorageAccountName'))]"
                    ],
                    "tags": { },
                    "properties": {
                        "clusterVersion": "3.2",
                        "osType": "Linux",
                        "clusterDefinition": {
                            "kind": "hadoop",
                            "configurations": {
                                "gateway": {
                                    "restAuthCredential.isEnabled": true,
                                    "restAuthCredential.username": "[parameters('clusterUserName')]",
                                    "restAuthCredential.password": "[parameters('clusterUserPassword')]"
                                }
                            }
                        },
                        "storageProfile": {
                            "storageaccounts": [
                                {
                                    "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                                    "isDefault": true,
                                    "container": "[parameters('clusterStorageAccountContainer')]",
                                    "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), '2015-05-01-preview').key1]"
                                }
                            ]
                        },
                        "computeProfile": {
                            "roles": [
                                {
                                    "name": "headnode",
                                    "targetInstanceCount": "[parameters('clusterHeadNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installGiraph",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                },
                                {
                                    "name": "workernode",
                                    "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                                    "hardwareProfile": {
                                        "vmSize": "Large"
                                    },
                                    "osProfile": {
                                        "linuxOperatingSystemProfile": {
                                            "username": "[parameters('sshUserName')]",
                                            "password": "[parameters('sshPassword')]"
                                        }
                                    },
                                    "scriptActions": [
                                        {
                                            "name": "installR",
                                            "uri": "https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh",
                                            "parameters": ""
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                }
            ],
            "outputs": {
                "cluster":{
                    "type" : "object",
                    "value" : "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                }
            }
        }
2. <span data-ttu-id="9b3d3-260">Start Azure PowerShell en zich aanmelden bij uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-260">Start Azure PowerShell and Log in to your Azure account.</span></span> <span data-ttu-id="9b3d3-261">Na het opgeven van uw referenties, retourneert de opdracht informatie over uw account.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-261">After providing your credentials, the command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="9b3d3-262">Als u meerdere abonnementen hebt, geeft u de abonnements-ID die u wilt gebruiken voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-262">If you have multiple subscriptions, provide the subscription ID you wish to use for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="9b3d3-263">U kunt `Get-AzureRmSubscription` voor een lijst van alle abonnementen die zijn gekoppeld aan je account, waaronder de abonnements-ID voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-263">You can use `Get-AzureRmSubscription` to get a list of all subscriptions associated with your account, which includes the subscription ID for each one.</span></span>

4. <span data-ttu-id="9b3d3-264">Als u een bestaande resourcegroep niet hebt, kunt u een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="9b3d3-265">Geef de naam van de resourcegroep en de locatie die u nodig hebt voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-265">Provide the name of the resource group and location that you need for your solution.</span></span> <span data-ttu-id="9b3d3-266">Er wordt een samenvatting van de nieuwe resourcegroep geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-266">A summary of the new resource group is returned.</span></span>

        New-AzureRmResourceGroup -Name myresourcegroup -Location "West US"

        ResourceGroupName : myresourcegroup
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *
        ResourceId        : /subscriptions/######/resourceGroups/ExampleResourceGroup

5. <span data-ttu-id="9b3d3-267">Voor het maken van een implementatie voor de resourcegroep, voer de **New-AzureRmResourceGroupDeployment** opdracht en de vereiste parameters.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-267">To create a deployment for your resource group, run the **New-AzureRmResourceGroupDeployment** command and provide the necessary parameters.</span></span> <span data-ttu-id="9b3d3-268">De parameters omvatten de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-268">The parameters include the following data:</span></span>

    * <span data-ttu-id="9b3d3-269">Een naam voor uw implementatie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-269">A name for your deployment</span></span>
    * <span data-ttu-id="9b3d3-270">De naam van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="9b3d3-270">The name of your resource group</span></span>
    * <span data-ttu-id="9b3d3-271">Het pad of de URL van de sjabloon die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-271">The path or URL to the template you created.</span></span>

  <span data-ttu-id="9b3d3-272">Als de sjabloon parameters vereist, moet u ook deze parameters doorgeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="9b3d3-273">In dit geval is de actie van het script voor het installeren van R op het cluster geen parameters vereist.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-273">In this case, the script action to install R on the cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="9b3d3-274">U wordt gevraagd waarden opgeven voor de gedefinieerde parameters in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-274">You are prompted to provide values for the parameters defined in the template.</span></span>

1. <span data-ttu-id="9b3d3-275">Wanneer de resourcegroep is geïmplementeerd, wordt een overzicht van de implementatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-275">When the resource group has been deployed, a summary of the deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="9b3d3-276">Als uw implementatie mislukt, kunt u de volgende cmdlets voor informatie over de fouten.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-276">If your deployment fails, you can use the following cmdlets to get information about the failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="9b3d3-277">Een actie Script gebruiken tijdens het maken van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b3d3-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="9b3d3-278">In deze sectie gebruiken we de [toevoegen AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet aan te roepen scripts met behulp van de scriptactie voor het aanpassen van een cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-278">In this section, we use the [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet to invoke scripts by using Script Action to customize a cluster.</span></span> <span data-ttu-id="9b3d3-279">Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="9b3d3-280">Zie voor meer informatie over het configureren van een werkstation als HDInsight PowerShell-cmdlets wilt uitvoeren, [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-280">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="9b3d3-281">Het volgende script laat zien hoe een scriptactie toepassen bij het maken van een cluster met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-281">The following script demonstrates how to apply a script action when creating a cluster using PowerShell:</span></span>

<span data-ttu-id="9b3d3-282">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span><span class="sxs-lookup"><span data-stu-id="9b3d3-282">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]</span></span>

<span data-ttu-id="9b3d3-283">Het kan enkele minuten duren voordat het cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-283">It can take several minutes before the cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-the-hdinsight-net-sdk"></a><span data-ttu-id="9b3d3-284">Een actie Script gebruiken tijdens het maken van de HDInsight-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="9b3d3-284">Use a Script Action during cluster creation from the HDInsight .NET SDK</span></span>

<span data-ttu-id="9b3d3-285">De HDInsight-SDK voor .NET biedt clientbibliotheken waarmee eenvoudiger te laten werken met HDInsight vanuit een .NET-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-285">The HDInsight .NET SDK provides client libraries that makes it easier to work with HDInsight from a .NET application.</span></span> <span data-ttu-id="9b3d3-286">Zie voor een voorbeeld van code [maken Linux gebaseerde clusters in HDInsight met behulp van de .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-286">For a code sample, see [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-to-a-running-cluster"></a><span data-ttu-id="9b3d3-287">De actie Script toepassen op een actief cluster</span><span class="sxs-lookup"><span data-stu-id="9b3d3-287">Apply a Script Action to a running cluster</span></span>

<span data-ttu-id="9b3d3-288">Informatie over het toepassen van scriptacties met een actief cluster in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-288">In this section, learn how to apply script actions to a running cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-portal"></a><span data-ttu-id="9b3d3-289">Scriptactie toepassen op een cluster uitgevoerd vanuit de Azure-portal</span><span class="sxs-lookup"><span data-stu-id="9b3d3-289">Apply a Script Action to a running cluster from the Azure portal</span></span>

1. <span data-ttu-id="9b3d3-290">Van de [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-290">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="9b3d3-291">Selecteer in het overzicht van HDInsight-cluster, de **scriptacties** tegel.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-291">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="9b3d3-293">U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** in het gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-293">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

3. <span data-ttu-id="9b3d3-294">Selecteer in de bovenkant van de sectie scriptacties **indienen nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-294">From the top of the Script Actions section, select **Submit new**.</span></span>

    ![Een script toevoegen aan een actieve cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="9b3d3-296">Gebruik de __selecteert u een script__ item naar een vooraf gemaakte script te selecteren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-296">Use the __Select a script__ entry to select a pre-made script.</span></span> <span data-ttu-id="9b3d3-297">Selecteer voor het gebruik van een aangepast script __aangepaste__ en geef vervolgens de __naam__ en __Bash script URI__ voor uw script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-297">To use a custom script, select __Custom__ and then provide the __Name__ and __Bash script URI__ for your script.</span></span>

    ![Een script in de vorm Selecteer script toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="9b3d3-299">De volgende tabel beschrijft de elementen in het formulier:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-299">The following table describes the elements on the form:</span></span>

    | <span data-ttu-id="9b3d3-300">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9b3d3-300">Property</span></span> | <span data-ttu-id="9b3d3-301">Waarde</span><span class="sxs-lookup"><span data-stu-id="9b3d3-301">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="9b3d3-302">Selecteer een script</span><span class="sxs-lookup"><span data-stu-id="9b3d3-302">Select a script</span></span> | <span data-ttu-id="9b3d3-303">Selecteer voor het gebruik van uw eigen script __aangepaste__.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-303">To use your own script, select __custom__.</span></span> <span data-ttu-id="9b3d3-304">Anders selecteert u een geleverde script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-304">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="9b3d3-305">Naam</span><span class="sxs-lookup"><span data-stu-id="9b3d3-305">Name</span></span> |<span data-ttu-id="9b3d3-306">Geef een naam voor de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-306">Specify a name for the script action.</span></span> |
    | <span data-ttu-id="9b3d3-307">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="9b3d3-307">Bash script URI</span></span> |<span data-ttu-id="9b3d3-308">Geef de URI moet het script dat wordt opgeroepen voor het aanpassen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-308">Specify the URI to the script that is invoked to customize the cluster.</span></span> |
    | <span data-ttu-id="9b3d3-309">Worker-HEAD/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="9b3d3-309">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="9b3d3-310">Geef de knooppunten (**Head**, **Worker**, of **ZooKeeper**) op waarmee het script aanpassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-310">Specify the nodes (**Head**, **Worker**, or **ZooKeeper**) on which the customization script is run.</span></span> |
    | <span data-ttu-id="9b3d3-311">Parameters</span><span class="sxs-lookup"><span data-stu-id="9b3d3-311">Parameters</span></span> |<span data-ttu-id="9b3d3-312">Geef de parameters op, indien vereist door het script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-312">Specify the parameters, if required by the script.</span></span> |

    <span data-ttu-id="9b3d3-313">Gebruik de __deze scriptactie__ vermelding om ervoor te zorgen dat het script wordt toegepast tijdens het schalen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-313">Use the __Persist this script action__ entry to make sure the script is applied during scaling operations.</span></span>

5. <span data-ttu-id="9b3d3-314">Gebruik tot slot de **maken** knop om toe te passen van het script voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-314">Finally, use the **Create** button to apply the script to the cluster.</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-azure-powershell"></a><span data-ttu-id="9b3d3-315">Scriptactie toepassen op een actief cluster van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b3d3-315">Apply a Script Action to a running cluster from Azure PowerShell</span></span>

<span data-ttu-id="9b3d3-316">Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-316">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="9b3d3-317">Zie voor meer informatie over het configureren van een werkstation als HDInsight PowerShell-cmdlets wilt uitvoeren, [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-317">For information about configuring a workstation to run HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="9b3d3-318">Het volgende voorbeeld laat zien hoe een scriptactie toepassen op een actief cluster:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-318">The following example demonstrates how to apply a script action to a running cluster:</span></span>

<span data-ttu-id="9b3d3-319">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span><span class="sxs-lookup"><span data-stu-id="9b3d3-319">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]</span></span>

<span data-ttu-id="9b3d3-320">Nadat de bewerking is voltooid, wordt de informatie is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-320">Once the operation completes, you receive information similar to the following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-to-a-running-cluster-from-the-azure-cli"></a><span data-ttu-id="9b3d3-321">Scriptactie toepassen op een actief cluster van de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b3d3-321">Apply a Script Action to a running cluster from the Azure CLI</span></span>

<span data-ttu-id="9b3d3-322">Zorg ervoor dat u hebt geïnstalleerd en de Azure CLI geconfigureerd voordat u verdergaat.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-322">Before proceeding, make sure you have installed and configured the Azure CLI.</span></span> <span data-ttu-id="9b3d3-323">Zie voor meer informatie [Azure CLI installeren](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-323">For more information, see [Install the Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="9b3d3-324">Als u wilt overschakelen naar de modus Azure Resource Manager, gebruik de volgende opdracht bij de opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-324">To switch to Azure Resource Manager mode, use the following command at the command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="9b3d3-325">Gebruik de volgende om uw Azure-abonnement te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-325">Use the following to authenticate to your Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="9b3d3-326">Gebruik de volgende opdracht toe te passen van een scriptactie naar een actief cluster</span><span class="sxs-lookup"><span data-stu-id="9b3d3-326">Use the following command to apply a script action to a running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="9b3d3-327">Als u de parameters voor deze opdracht weglaat, wordt u gevraagd deze.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-327">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="9b3d3-328">Als het script dat u met opgeeft `-u` accepteert parameters, kunt u deze opgeven met behulp van de `-p` parameter.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-328">If the script you specify with `-u` accepts parameters, you can specify them using the `-p` parameter.</span></span>

    <span data-ttu-id="9b3d3-329">Geldige knooppunt-typen zijn `headnode`, `workernode`, en `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-329">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="9b3d3-330">Als het script moet worden toegepast op typen met meerdere knooppunten, geeft u de typen gescheiden door een ';'.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-330">If the script should be applied to multiple node types, specify the types separated by a ';'.</span></span> <span data-ttu-id="9b3d3-331">Bijvoorbeeld `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-331">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="9b3d3-332">Om te blijven behouden het script, voeg de `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-332">To persist the script, add the `--persistOnSuccess`.</span></span> <span data-ttu-id="9b3d3-333">U kunt ook het script later behouden met behulp van `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-333">You can also persist the script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="9b3d3-334">Zodra de taak is voltooid, wordt de uitvoer is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-334">Once the job completes, you receive output similar to the following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-to-a-running-cluster-using-rest-api"></a><span data-ttu-id="9b3d3-335">De actie Script toepassen op een actief cluster met behulp van REST-API</span><span class="sxs-lookup"><span data-stu-id="9b3d3-335">Apply a Script Action to a running cluster using REST API</span></span>

<span data-ttu-id="9b3d3-336">Zie [scriptacties uitvoeren op een actief cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-336">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-to-a-running-cluster-from-the-hdinsight-net-sdk"></a><span data-ttu-id="9b3d3-337">Scriptactie toepassen op een actief cluster van de HDInsight-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="9b3d3-337">Apply a Script Action to a running cluster from the HDInsight .NET SDK</span></span>

<span data-ttu-id="9b3d3-338">Zie voor een voorbeeld van het gebruik van de .NET SDK scripts toepassen op een cluster [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-338">For an example of using the .NET SDK to apply scripts to a cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="9b3d3-339">Geschiedenis weergeven en degraderen scriptacties promoveren</span><span class="sxs-lookup"><span data-stu-id="9b3d3-339">View history, promote, and demote Script Actions</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="9b3d3-340">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3d3-340">Using the Azure portal</span></span>

1. <span data-ttu-id="9b3d3-341">Van de [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-341">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="9b3d3-342">Selecteer in het overzicht van HDInsight-cluster, de **scriptacties** tegel.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-342">From the HDInsight cluster overview, select the **Script Actions** tile.</span></span>

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="9b3d3-344">U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** in het gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-344">You can also select **All settings** and then select **Script Actions** from the Settings section.</span></span>

4. <span data-ttu-id="9b3d3-345">Een geschiedenis van scripts voor dit cluster wordt weergegeven in de sectie scriptacties.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-345">A history of scripts for this cluster is displayed on the Script Actions section.</span></span> <span data-ttu-id="9b3d3-346">Deze informatie omvat een lijst met persistente scripts.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-346">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="9b3d3-347">In de onderstaande schermafbeelding ziet u dat de Solr script is uitgevoerd op dit cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-347">In the screenshot below, you can see that the Solr script has been ran on this cluster.</span></span> <span data-ttu-id="9b3d3-348">De permanente scripts niet wordt weergegeven in de schermafbeelding.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-348">The screenshot does not show any persisted scripts.</span></span>

    ![De sectie Acties script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="9b3d3-350">De sectie met eigenschappen voor dit script te selecteren van een script in de geschiedenis worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-350">Selecting a script from the history displays the Properties section for this script.</span></span> <span data-ttu-id="9b3d3-351">U kunt het script opnieuw uitvoeren of promoveer deze vanaf de bovenkant van het scherm.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-351">From the top of the screen, you can rerun the script or promote it.</span></span>

    ![Eigenschappen van de script-acties](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="9b3d3-353">U kunt ook de **...**  rechts van de vermeldingen in de sectie scriptacties acties uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-353">You can also use the **...** to the right of entries on the Script Actions section to perform actions.</span></span>

    ![Acties... script gebruik](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="9b3d3-355">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3d3-355">Using Azure PowerShell</span></span>

| <span data-ttu-id="9b3d3-356">Gebruik de volgende...</span><span class="sxs-lookup"><span data-stu-id="9b3d3-356">Use the following...</span></span> | <span data-ttu-id="9b3d3-357">Aan...</span><span class="sxs-lookup"><span data-stu-id="9b3d3-357">To ...</span></span> |
| --- | --- |
| <span data-ttu-id="9b3d3-358">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="9b3d3-358">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="9b3d3-359">Informatie over persistente scriptacties ophalen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-359">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="9b3d3-360">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="9b3d3-360">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="9b3d3-361">Een geschiedenis van scriptacties toegepast op het cluster of de details voor een specifiek script ophalen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-361">Retrieve a history of script actions applied to the cluster, or details for a specific script</span></span> |
| <span data-ttu-id="9b3d3-362">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="9b3d3-362">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="9b3d3-363">Bijdraagt aan een ad-hoc scriptactie naar een persistent script-actie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-363">Promotes an ad hoc script action to a persisted script action</span></span> |
| <span data-ttu-id="9b3d3-364">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="9b3d3-364">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="9b3d3-365">Selecteert, wordt een actie persistent script aan een ad-hoc actie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-365">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9b3d3-366">Met behulp van `Remove-AzureRmHDInsightPersistedScriptAction` die de acties die worden uitgevoerd door een script wordt niet ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-366">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo the actions performed by a script.</span></span> <span data-ttu-id="9b3d3-367">Deze cmdlet worden alleen de persistente vlag verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-367">This cmdlet only removes the persisted flag.</span></span>

<span data-ttu-id="9b3d3-368">Het volgende voorbeeldscript wordt gedemonstreerd met behulp van de cmdlets verhogen, en vervolgens degraderen van een script.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-368">The following example script demonstrates using the cmdlets to promote, then demote a script.</span></span>

<span data-ttu-id="9b3d3-369">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span><span class="sxs-lookup"><span data-stu-id="9b3d3-369">[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]</span></span>

### <a name="using-the-azure-cli"></a><span data-ttu-id="9b3d3-370">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="9b3d3-370">Using the Azure CLI</span></span>

| <span data-ttu-id="9b3d3-371">Gebruik de volgende...</span><span class="sxs-lookup"><span data-stu-id="9b3d3-371">Use the following...</span></span> | <span data-ttu-id="9b3d3-372">Aan...</span><span class="sxs-lookup"><span data-stu-id="9b3d3-372">To ...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="9b3d3-373">Een lijst met persistente scriptacties ophalen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-373">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="9b3d3-374">Ophalen van gegevens op een specifieke persistente scriptacties actie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-374">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="9b3d3-375">Ophalen van een geschiedenis van scriptacties toegepast op het cluster</span><span class="sxs-lookup"><span data-stu-id="9b3d3-375">Retrieve a history of script actions applied to the cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="9b3d3-376">Ophalen van informatie over een specifiek script-actie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-376">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="9b3d3-377">Bijdraagt aan een ad-hoc scriptactie naar een persistent script-actie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-377">Promotes an ad hoc script action to a persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="9b3d3-378">Selecteert, wordt een actie persistent script aan een ad-hoc actie</span><span class="sxs-lookup"><span data-stu-id="9b3d3-378">Demotes a persisted script action to an ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="9b3d3-379">Met behulp van `azure hdinsight script-action persisted delete` die de acties die worden uitgevoerd door een script wordt niet ongedaan gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-379">Using `azure hdinsight script-action persisted delete` does not undo the actions performed by a script.</span></span> <span data-ttu-id="9b3d3-380">Deze cmdlet worden alleen de persistente vlag verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-380">This cmdlet only removes the persisted flag.</span></span>

### <a name="using-the-hdinsight-net-sdk"></a><span data-ttu-id="9b3d3-381">Met behulp van de HDInsight-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="9b3d3-381">Using the HDInsight .NET SDK</span></span>

<span data-ttu-id="9b3d3-382">Voor een voorbeeld van het gebruik van de .NET SDK script geschiedenis ophalen uit een cluster promoten of degraderen van scripts, Zie [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-382">For an example of using the .NET SDK to retrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="9b3d3-383">In dit voorbeeld demonstreert ook hoe u een HDInsight-toepassing met de .NET SDK te installeren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-383">This example also demonstrates how to install an HDInsight application using the .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="9b3d3-384">Ondersteuning voor open-source software gebruikt op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="9b3d3-384">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="9b3d3-385">De Microsoft Azure HDInsight-service gebruikt een ecosysteem van open-source technologieën gevormd rond Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-385">The Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="9b3d3-386">Microsoft Azure biedt een algemeen niveau van ondersteuning voor de open source-technologieën.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-386">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="9b3d3-387">Zie voor meer informatie de **ondersteuning bereik** sectie van de [ondersteuning Veelgestelde vragen over Azure-website](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-387">For more information, see the **Support Scope** section of the [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="9b3d3-388">De HDInsight-service biedt een extra verificatieniveau van ondersteuning voor ingebouwde-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-388">The HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="9b3d3-389">Er zijn twee soorten open source-onderdelen die beschikbaar in de HDInsight-service zijn:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-389">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="9b3d3-390">**Ingebouwde onderdelen** -deze onderdelen vooraf zijn geïnstalleerd op HDInsight-clusters en geef de kernfunctionaliteit van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-390">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="9b3d3-391">Bijvoorbeeld: YARN ResourceManager, de Hive-query language (HiveQL) en de bibliotheek Mahout behoren tot deze categorie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-391">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="9b3d3-392">Een volledige lijst met clusteronderdelen is beschikbaar in [wat is er nieuw in de Hadoop-clusterversies geleverd door HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-392">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="9b3d3-393">**Aangepaste onderdelen** -u, als een gebruiker van het cluster kunt installeren of gebruiken in uw werkbelasting een onderdeel is beschikbaar in de community of door u gemaakte.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-393">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="9b3d3-394">Onderdelen van het HDInsight-cluster worden volledig ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-394">Components provided with the HDInsight cluster are fully supported.</span></span> <span data-ttu-id="9b3d3-395">Microsoft Support kunt opsporen en oplossen van problemen met betrekking tot deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-395">Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="9b3d3-396">Aangepaste onderdelen ontvangt binnen commercieel redelijke ondersteuning u helpen het probleem verder op te lossen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-396">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="9b3d3-397">Microsoft ondersteuning mogelijk het probleem op te lossen of ze gevraagd om te benaderen beschikbare kanalen voor de open-source technologieën waar grondige kennis van deze technologie kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-397">Microsoft support may be able to resolve the issue OR they may ask you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="9b3d3-398">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-398">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="9b3d3-399">De HDInsight-service biedt verschillende manieren om te gebruiken van aangepaste onderdelen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-399">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="9b3d3-400">Hetzelfde niveau van de ondersteuning van toepassing is, ongeacht hoe een onderdeel gebruikt of is geïnstalleerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-400">The same level of support applies, regardless of how a component is used or installed on the cluster.</span></span> <span data-ttu-id="9b3d3-401">De volgende lijst bevat de meest voorkomende manieren dat aangepaste onderdelen op HDInsight-clusters kunnen worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-401">The following list describes the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="9b3d3-402">Verzending van taak - Hadoop- of andere typen taken die worden uitgevoerd of het gebruik van aangepaste onderdelen kan worden verzonden naar het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-402">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>

2. <span data-ttu-id="9b3d3-403">Aanpassing van de cluster - tijdens het maken van het cluster, kunt u aanvullende instellingen en aangepaste onderdelen die zijn geïnstalleerd op de clusterknooppunten opgeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-403">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on the cluster nodes.</span></span>

3. <span data-ttu-id="9b3d3-404">Steekproeven - voor populaire aangepaste onderdelen, Microsoft en anderen kunnen voorbeelden van hoe deze onderdelen kunnen worden gebruikt op de HDInsight-clusters bieden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-404">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="9b3d3-405">Deze voorbeelden worden geleverd zonder ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-405">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9b3d3-406">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-406">Troubleshooting</span></span>

<span data-ttu-id="9b3d3-407">Ambari-webgebruikersinterface kunt u informatie die zijn vastgelegd door scriptacties weergeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-407">You can use Ambari web UI to view information logged by script actions.</span></span> <span data-ttu-id="9b3d3-408">Als het script is mislukt tijdens maken van het cluster, zijn de logboeken ook beschikbaar in het standaardopslagaccount die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-408">If the script fails during cluster creation, the logs are also available in the default storage account associated with the cluster.</span></span> <span data-ttu-id="9b3d3-409">Deze sectie bevat informatie over het ophalen van de logboeken met behulp van deze beide opties.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-409">This section provides information on how to retrieve the logs using both these options.</span></span>

### <a name="using-the-ambari-web-ui"></a><span data-ttu-id="9b3d3-410">Met behulp van de Ambari-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="9b3d3-410">Using the Ambari Web UI</span></span>

1. <span data-ttu-id="9b3d3-411">Ga naar https://CLUSTERNAME.azurehdinsight.net in uw browser.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-411">In your browser, navigate to https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="9b3d3-412">CLUSTERNAAM vervangen door de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-412">Replace CLUSTERNAME with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="9b3d3-413">Wanneer u wordt gevraagd, typt u de accountnaam van de beheerder (admin) en het wachtwoord voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-413">When prompted, enter the admin account name (admin) and password for the cluster.</span></span> <span data-ttu-id="9b3d3-414">U moet de beheerdersreferenties in een webformulier invoeren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-414">You may have to reenter the admin credentials in a web form.</span></span>

2. <span data-ttu-id="9b3d3-415">Selecteer in de balk aan de bovenkant van de pagina de **ops** vermelding.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-415">From the bar at the top of the page, select the **ops** entry.</span></span> <span data-ttu-id="9b3d3-416">Een lijst met huidige en vorige bewerkingen die worden uitgevoerd op het cluster door Ambari wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-416">A list of current and previous operations performed on the cluster through Ambari is displayed.</span></span>

    ![Ambari web UI-balk met ops geselecteerd](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="9b3d3-418">De items waarvoor vindt **uitvoeren\_customscriptaction** in de **Operations** kolom.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-418">Find the entries that have **run\_customscriptaction** in the **Operations** column.</span></span> <span data-ttu-id="9b3d3-419">Deze vermeldingen worden gemaakt wanneer de Script-bewerkingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-419">These entries are created when the Script Actions run.</span></span>

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="9b3d3-421">Als u wilt weergeven in de uitvoer STDOUT en STDERR, selecteer de vermelding run\customscriptaction en inzoomen via de koppelingen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-421">To view the STDOUT and STDERR output, select the run\customscriptaction entry and drill down through the links.</span></span> <span data-ttu-id="9b3d3-422">Deze uitvoer wordt gegenereerd wanneer het script wordt uitgevoerd, en mogelijk bevatten nuttige informatie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-422">This output is generated when the script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-the-default-storage-account"></a><span data-ttu-id="9b3d3-423">Toegang tot logboeken van het standaardopslagaccount</span><span class="sxs-lookup"><span data-stu-id="9b3d3-423">Access logs from the default storage account</span></span>

<span data-ttu-id="9b3d3-424">Als het maken van het cluster is mislukt vanwege een scriptfout actie, zijn de logboeken toegankelijk vanuit het opslagaccount van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-424">If the cluster creation fails due to a script action error, the logs can be accessed from the cluster storage account.</span></span>

* <span data-ttu-id="9b3d3-425">De logboeken van de opslag zijn beschikbaar op `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-425">The storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="9b3d3-427">De logboeken zijn in deze map afzonderlijk ingedeeld voor headnode, workernode en zookeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-427">Under this directory, the logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="9b3d3-428">Een aantal voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-428">Some examples are:</span></span>

    * <span data-ttu-id="9b3d3-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="9b3d3-429">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="9b3d3-430">**Werkrolknooppunt** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="9b3d3-430">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="9b3d3-431">**Zookeeper-knooppunt** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="9b3d3-431">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="9b3d3-432">Alle stdout en stderr van de bijbehorende host is geüpload naar het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-432">All stdout and stderr of the corresponding host is uploaded to the storage account.</span></span> <span data-ttu-id="9b3d3-433">Er is een **uitvoer -\*.txt** en **fouten -\*.txt** voor elke scriptactie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-433">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="9b3d3-434">De uitvoer-txt-bestand bevat informatie over de URI van het script dat is uitgevoerd op de host.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-434">The output-*.txt file contains information about the URI of the script that got run on the host.</span></span> <span data-ttu-id="9b3d3-435">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="9b3d3-435">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="9b3d3-436">Het is mogelijk dat u een script actie cluster herhaaldelijk met dezelfde naam maken.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-436">It's possible that you repeatedly create a script action cluster with the same name.</span></span> <span data-ttu-id="9b3d3-437">In dat geval kunt u de relevante logboekbestanden op basis van de naam van de datum-map onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-437">In such case, you can distinguish the relevant logs based on the DATE folder name.</span></span> <span data-ttu-id="9b3d3-438">Bijvoorbeeld, lijkt de mapstructuur voor een cluster (mijncluster) gemaakt op verschillende datums op de volgende logboekvermeldingen:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-438">For example, the folder structure for a cluster (mycluster) created on different dates appears similar to the following log entries:</span></span>

    <span data-ttu-id="9b3d3-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="9b3d3-439">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="9b3d3-440">Als u een script actie cluster met dezelfde naam op dezelfde dag maakt, kunt u het voorvoegsel uniek te identificeren van de relevante logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-440">If you create a script action cluster with the same name on the same day, you can use the unique prefix to identify the relevant log files.</span></span>

* <span data-ttu-id="9b3d3-441">Als u een cluster in de buurt van 12:00 AM (middernacht) maakt, is het mogelijk dat de logboekbestanden twee dagen overbruggen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-441">If you create a cluster near 12:00AM (midnight), it's possible that the log files span across two days.</span></span> <span data-ttu-id="9b3d3-442">In dergelijke gevallen ziet u twee andere datum mappen voor hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-442">In such cases, you see two different date folders for the same cluster.</span></span>

* <span data-ttu-id="9b3d3-443">Logboekbestanden uploaden naar de standaardcontainer kan maximaal 5 minuten, met name voor grote clusters duren.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-443">Uploading log files to the default container can take up to 5 mins, especially for large clusters.</span></span> <span data-ttu-id="9b3d3-444">Dus als u toegang wilt tot de logboeken, verwijdert niet onmiddellijk u het cluster als een scriptactie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-444">So, if you want to access the logs, you should not immediately delete the cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="9b3d3-445">Ambari watchdog</span><span class="sxs-lookup"><span data-stu-id="9b3d3-445">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="9b3d3-446">Wijzig het wachtwoord niet voor de Ambari-Watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-446">Do not change the password for the Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9b3d3-447">Wijzigen van het wachtwoord voor dit account, verbreekt de mogelijkheid nieuwe scriptacties uitvoeren op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-447">Changing the password for this account breaks the ability to run new script actions on the HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="9b3d3-448">Naam BlobService kan niet worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-448">Can't import name BlobService</span></span>

<span data-ttu-id="9b3d3-449">__Symptomen__: het script actie mislukt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-449">__Symptoms__: The script action fails.</span></span> <span data-ttu-id="9b3d3-450">Tekst die vergelijkbaar is met de volgende fout wordt weergegeven wanneer u de bewerking in Ambari weergeven:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-450">Text similar to the following error is displayed when you view the operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="9b3d3-451">__Oorzaak__: deze fout treedt op als u de Python Azure Storage client bijwerkt die is opgenomen in het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-451">__Cause__: This error occurs if you upgrade the Python Azure Storage client that is included with the HDInsight cluster.</span></span> <span data-ttu-id="9b3d3-452">HDInsight verwacht Azure Storage client 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-452">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="9b3d3-453">__Resolutie__: los deze fout, handmatig verbinding maken met elk cluster knooppunt gebruikt `ssh` en gebruik de volgende opdracht om opnieuw te installeren de juiste opslag clientversie:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-453">__Resolution__: To resolve this error, manually connect to each cluster node using `ssh` and use the following command to reinstall the correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="9b3d3-454">Zie voor informatie over de verbinding met het cluster met SSH, [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9b3d3-454">For information on connecting to the cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="9b3d3-455">Geschiedenis van niet wordt scripts die worden gebruikt tijdens het maken van het cluster weergegeven</span><span class="sxs-lookup"><span data-stu-id="9b3d3-455">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="9b3d3-456">Als uw cluster is gemaakt voordat 15 maart 2016, ziet u mogelijk niet een vermelding in de geschiedenis van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-456">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="9b3d3-457">Als u de grootte van het cluster na 15 maart 2016, de scripts die met behulp van tijdens het maken van het cluster weergegeven in de geschiedenis als ze worden toegepast op nieuwe knooppunten in het cluster als onderdeel van de bewerking formaat wijzigen.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-457">If you resize the cluster after March 15, 2016, the scripts using during cluster creation appear in history as they are applied to new nodes in the cluster as part of the resize operation.</span></span>

<span data-ttu-id="9b3d3-458">Er zijn twee uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-458">There are two exceptions:</span></span>

* <span data-ttu-id="9b3d3-459">Als uw cluster is gemaakt vóór 1 September 2015.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-459">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="9b3d3-460">Deze datum is wanneer scriptacties zijn geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-460">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="9b3d3-461">Een cluster is gemaakt voor deze datum kan niet hebben gebruikt scriptacties voor maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-461">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="9b3d3-462">Als u meerdere scriptacties tijdens het maken van het cluster gebruikt en dezelfde naam voor meerdere scripts of de dezelfde naam, dezelfde URI, maar verschillende parameters voor meerdere scripts gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-462">If you used multiple Script Actions during cluster creation, and used the same name for multiple scripts, or the same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="9b3d3-463">In deze gevallen is foutbericht het volgende:</span><span class="sxs-lookup"><span data-stu-id="9b3d3-463">In these cases, you receive the following error:</span></span>

    <span data-ttu-id="9b3d3-464">Op dit cluster vanwege conflicterende scriptnamen in bestaande scripts worden geen nieuwe script acties kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-464">No new script actions can be ran on this cluster due to conflicting script names in existing scripts.</span></span> <span data-ttu-id="9b3d3-465">Scriptnamen die zijn opgegeven bij het cluster moet maken allemaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-465">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="9b3d3-466">Bestaande scripts worden uitgevoerd op formaat.</span><span class="sxs-lookup"><span data-stu-id="9b3d3-466">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b3d3-467">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9b3d3-467">Next steps</span></span>

* [<span data-ttu-id="9b3d3-468">Scriptactie-scripts ontwikkelen voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="9b3d3-468">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="9b3d3-469">Installeren en gebruiken van Solr op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="9b3d3-469">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="9b3d3-470">Installeren en gebruiken van Giraph op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="9b3d3-470">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="9b3d3-471">Extra opslag toevoegen aan een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="9b3d3-471">Add additional storage to an HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

<span data-ttu-id="9b3d3-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"</span><span class="sxs-lookup"><span data-stu-id="9b3d3-472">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Stages during cluster creation"</span></span>

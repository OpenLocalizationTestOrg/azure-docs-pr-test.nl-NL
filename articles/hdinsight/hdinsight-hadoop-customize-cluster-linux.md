---
title: aaaCustomize HDInsight-clusters met behulp van scriptacties - Azure | Microsoft Docs
description: Aangepaste onderdelen die toolinux gebaseerde HDInsight-clusters met behulp van scriptacties toevoegen. Scriptacties zijn Bash-scripts die kunnen worden gebruikt toocustomize Hallo clusterconfiguratie of toevoegen van extra services en hulpprogramma's zoals Hue, Solr of R.
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
ms.openlocfilehash: ff22680a8a50b21985f6941f1edaf1dcf863d13f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="customize-linux-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="0a931-104">Linux gebaseerde HDInsight-clusters met behulp van de scriptactie aanpassen</span><span class="sxs-lookup"><span data-stu-id="0a931-104">Customize Linux-based HDInsight clusters using Script Action</span></span>

<span data-ttu-id="0a931-105">HDInsight biedt een configuratieoptie aangeroepen **scriptactie** die wordt aangeroepen met aangepaste scripts die Hallo cluster aanpassen.</span><span class="sxs-lookup"><span data-stu-id="0a931-105">HDInsight provides a configuration option called **Script Action** that invokes custom scripts that customize hello cluster.</span></span> <span data-ttu-id="0a931-106">Deze scripts zijn gebruikte tooinstall extra onderdelen en configuratie-instellingen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0a931-106">These scripts are used tooinstall additional components and change configuration settings.</span></span> <span data-ttu-id="0a931-107">Scriptacties kunnen worden gebruikt tijdens of na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-107">Script actions can be used during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a931-108">Hallo mogelijkheid toouse scriptacties op een cluster al actief is alleen beschikbaar voor Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="0a931-108">hello ability toouse script actions on an already running cluster is only available for Linux-based HDInsight clusters.</span></span>
>
> <span data-ttu-id="0a931-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="0a931-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0a931-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0a931-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="0a931-111">Scriptacties kunnen ook gepubliceerde toohello Azure Marketplace worden als een HDInsight-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0a931-111">Script actions can also be published toohello Azure Marketplace as an HDInsight application.</span></span> <span data-ttu-id="0a931-112">Aantal Hallo voorbeelden in dit document laten zien hoe u een HDInsight-toepassing met behulp van actie-scriptopdrachten van PowerShell en .NET SDK Hallo kunt installeren.</span><span class="sxs-lookup"><span data-stu-id="0a931-112">Some of hello examples in this document show how you can install an HDInsight application using script action commands from PowerShell and hello .NET SDK.</span></span> <span data-ttu-id="0a931-113">Zie voor meer informatie over HDInsight-toepassingen [publiceren HDInsight-toepassingen in Azure Marketplace Hallo](hdinsight-apps-publish-applications.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-113">For more information on HDInsight applications, see [Publish HDInsight applications into hello Azure Marketplace](hdinsight-apps-publish-applications.md).</span></span>

## <a name="permissions"></a><span data-ttu-id="0a931-114">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="0a931-114">Permissions</span></span>

<span data-ttu-id="0a931-115">Als u van een domein HDInsight-cluster gebruikmaakt, zijn er twee Ambari-machtigingen die vereist zijn wanneer met behulp van scriptacties met Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="0a931-115">If you are using a domain-joined HDInsight cluster, there are two Ambari permissions that are required when using script actions with hello cluster:</span></span>

* <span data-ttu-id="0a931-116">**AMBARI. Voer\_aangepaste\_opdracht**: Hallo Ambari beheerdersrol beschikt over deze machtiging standaard.</span><span class="sxs-lookup"><span data-stu-id="0a931-116">**AMBARI.RUN\_CUSTOM\_COMMAND**: hello Ambari Administrator role has this permission by default.</span></span>
* <span data-ttu-id="0a931-117">**HET CLUSTER. Voer\_aangepaste\_opdracht**: beide Hallo HDInsight Clusterbeheer en Ambari beheerder hebben deze machtiging standaard.</span><span class="sxs-lookup"><span data-stu-id="0a931-117">**CLUSTER.RUN\_CUSTOM\_COMMAND**: Both hello HDInsight Cluster Administrator and Ambari Administrator have this permission by default.</span></span>

<span data-ttu-id="0a931-118">Zie voor meer informatie over het werken met machtigingen met HDInsight domein [domein HDInsight-clusters beheren](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-118">For more information on working with permissions with domain-joined HDInsight, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="0a931-119">Toegangsbeheer</span><span class="sxs-lookup"><span data-stu-id="0a931-119">Access control</span></span>

<span data-ttu-id="0a931-120">Als u niet Hallo beheerder of eigenaar van uw Azure-abonnement, uw account moet er ten minste **Inzender** toegang toohello resourcegroep die Hallo HDInsight-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="0a931-120">If you are not hello administrator/owner of your Azure subscription, your account must have at least **Contributor** access toohello resource group that contains hello HDInsight cluster.</span></span>

<span data-ttu-id="0a931-121">Bovendien, als u een HDInsight-cluster iemand met ten minste maakt **Inzender** toegang toohello Azure-abonnement moet hebben eerder Hallo-provider geregistreerd voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a931-121">Additionally, if you are creating an HDInsight cluster, someone with at least **Contributor** access toohello Azure subscription must have previously registered hello provider for HDInsight.</span></span> <span data-ttu-id="0a931-122">Registratie van de provider wordt uitgevoerd wanneer een gebruiker met Inzender toegang toohello abonnement een resource voor Hallo eerst op Hallo-abonnement maakt.</span><span class="sxs-lookup"><span data-stu-id="0a931-122">Provider registration happens when a user with Contributor access toohello subscription creates a resource for hello first time on hello subscription.</span></span> <span data-ttu-id="0a931-123">Dit kan ook worden bereikt zonder dat er een resource wordt gemaakt door [een provider te registreren met behulp van REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a931-123">It can also be accomplished without creating a resource by [registering a provider using REST](https://msdn.microsoft.com/library/azure/dn790548.aspx).</span></span>

<span data-ttu-id="0a931-124">Zie voor meer informatie over het werken met toegangsbeheer Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a931-124">For more information on working with access management, see hello following documents:</span></span>

* [<span data-ttu-id="0a931-125">Aan de slag met toegangsbeheer in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0a931-125">Get started with access management in hello Azure portal</span></span>](../active-directory/role-based-access-control-what-is.md)
* [<span data-ttu-id="0a931-126">Rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken</span><span class="sxs-lookup"><span data-stu-id="0a931-126">Use role assignments toomanage access tooyour Azure subscription resources</span></span>](../active-directory/role-based-access-control-configure.md)

## <a name="understanding-script-actions"></a><span data-ttu-id="0a931-127">Understanding scriptacties</span><span class="sxs-lookup"><span data-stu-id="0a931-127">Understanding Script Actions</span></span>

<span data-ttu-id="0a931-128">Een scriptactie is gewoon een Bash-script dat u een URI te bieden en parameters voor.</span><span class="sxs-lookup"><span data-stu-id="0a931-128">A Script Action is simply a Bash script that you provide a URI to, and parameters for.</span></span> <span data-ttu-id="0a931-129">Hallo-script wordt uitgevoerd op knooppunten in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-129">hello script runs on nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="0a931-130">Hallo volgen kenmerken en functies van scriptacties.</span><span class="sxs-lookup"><span data-stu-id="0a931-130">hello following are characteristics and features of script actions.</span></span>

* <span data-ttu-id="0a931-131">Moet worden opgeslagen op een URI die toegankelijk is vanaf Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-131">Must be stored on a URI that is accessible from hello HDInsight cluster.</span></span> <span data-ttu-id="0a931-132">Hallo volgen mogelijke opslaglocaties:</span><span class="sxs-lookup"><span data-stu-id="0a931-132">hello following are possible storage locations:</span></span>

    * <span data-ttu-id="0a931-133">Een **Azure Data Lake Store** account die toegankelijk is voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-133">An **Azure Data Lake Store** account that is accessible by hello HDInsight cluster.</span></span> <span data-ttu-id="0a931-134">Zie voor meer informatie over het gebruik van Azure Data Lake Store met HDInsight [een HDInsight-cluster maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-134">For information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

        <span data-ttu-id="0a931-135">Wanneer u een script dat is opgeslagen in Data Lake Store, Hallo URI-indeling is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span><span class="sxs-lookup"><span data-stu-id="0a931-135">When using a script stored in Data Lake Store, hello URI format is `adl://DATALAKESTOREACCOUNTNAME.azuredatalakestore.net/path_to_file`.</span></span>

        > [!NOTE]
        > <span data-ttu-id="0a931-136">Hallo service principal HDInsight maakt gebruik van tooaccess Data Lake Store moet leestoegang toohello script hebben.</span><span class="sxs-lookup"><span data-stu-id="0a931-136">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

    * <span data-ttu-id="0a931-137">Een blob in een **Azure Storage-account** die beide accounts Hallo primaire of extra opslag voor Hallo HDInsight-cluster is.</span><span class="sxs-lookup"><span data-stu-id="0a931-137">A blob in an **Azure Storage account** that is either hello primary or additional storage account for hello HDInsight cluster.</span></span> <span data-ttu-id="0a931-138">HDInsight krijgt toegang tot tooboth van deze typen opslagaccounts tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-138">HDInsight is granted access tooboth of these types of storage accounts during cluster creation.</span></span>

    * <span data-ttu-id="0a931-139">Bestand met een openbare sharing-service zoals Azure Blob, GitHub, OneDrive, Dropbox, enz.</span><span class="sxs-lookup"><span data-stu-id="0a931-139">A public file sharing service such as Azure Blob, GitHub, OneDrive, Dropbox, etc.</span></span>

        <span data-ttu-id="0a931-140">Bijvoorbeeld URI's, Zie Hallo [voorbeeldscripts script actie](#example-script-action-scripts) sectie.</span><span class="sxs-lookup"><span data-stu-id="0a931-140">For example URIs, see hello [Example script action scripts](#example-script-action-scripts) section.</span></span>

        > [!WARNING]
        > <span data-ttu-id="0a931-141">HDInsight biedt alleen ondersteuning voor __algemeen__ Azure Storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="0a931-141">HDInsight only supports __General-purpose__ Azure Storage accounts.</span></span> <span data-ttu-id="0a931-142">Het ondersteunt momenteel geen Hallo __Blob storage__ accounttype.</span><span class="sxs-lookup"><span data-stu-id="0a931-142">It does not currently support hello __Blob storage__ account type.</span></span>

* <span data-ttu-id="0a931-143">Kan worden beperkt te**uitvoeren op alleen bepaalde knooppunttypen**voor voorbeeld hoofdknooppunten of worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="0a931-143">Can be restricted too**run on only certain node types**, for example head nodes or worker nodes.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0a931-144">Gebruikt in combinatie met HDInsight Premium, kunt u opgeven dat Hallo script op Hallo edge-knooppunt moet worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0a931-144">When used with HDInsight Premium, you can specify that hello script should be used on hello edge node.</span></span>

* <span data-ttu-id="0a931-145">Kan **persistent** of **ad hoc**.</span><span class="sxs-lookup"><span data-stu-id="0a931-145">Can be **persisted** or **ad hoc**.</span></span>

    <span data-ttu-id="0a931-146">**Persistent** scripts zijn toegepaste tooworker knooppunten toegevoegde toohello cluster na het Hallo-script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-146">**Persisted** scripts are applied tooworker nodes added toohello cluster after hello script runs.</span></span> <span data-ttu-id="0a931-147">Bijvoorbeeld tijdens het Hallo-cluster schalen.</span><span class="sxs-lookup"><span data-stu-id="0a931-147">For example, when scaling up hello cluster.</span></span>

    <span data-ttu-id="0a931-148">Een persistent script mogelijk ook van toepassing zijn wijzigingen tooanother knooppunttype, zoals een hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="0a931-148">A persisted script might also apply changes tooanother node type, such as a head node.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0a931-149">Persistente scriptacties moeten een unieke naam hebben.</span><span class="sxs-lookup"><span data-stu-id="0a931-149">Persisted script actions must have a unique name.</span></span>

    <span data-ttu-id="0a931-150">**Ad hoc** scripts blijven niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="0a931-150">**Ad hoc** scripts are not persisted.</span></span> <span data-ttu-id="0a931-151">Ze zijn niet toegepast tooworker knooppunten toegevoegde toohello cluster na het Hallo-script is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-151">They are not applied tooworker nodes added toohello cluster after hello script has ran.</span></span> <span data-ttu-id="0a931-152">U kunt vervolgens een ad-hoc script tooa promoveren persistent script of degraderen van een persistent script tooan ad-hoc-script.</span><span class="sxs-lookup"><span data-stu-id="0a931-152">You can subsequently promote an ad hoc script tooa persisted script, or demote a persisted script tooan ad hoc script.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0a931-153">Scriptacties gebruikt tijdens het maken van het cluster worden automatisch doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-153">Script actions used during cluster creation are automatically persisted.</span></span>
  >
  > <span data-ttu-id="0a931-154">Scripts die mislukken niet persistent hebt gemaakt, zelfs als u specifiek aangeeft dat ze moeten worden.</span><span class="sxs-lookup"><span data-stu-id="0a931-154">Scripts that fail are not persisted, even if you specifically indicate that they should be.</span></span>

* <span data-ttu-id="0a931-155">Kan accepteren **parameters** die worden gebruikt door Hallo script tijdens de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="0a931-155">Can accept **parameters** that are used by hello script during execution.</span></span>
* <span data-ttu-id="0a931-156">Voer met **root bevoegdheden** op Hallo clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="0a931-156">Run with **root level privileges** on hello cluster nodes.</span></span>
* <span data-ttu-id="0a931-157">Kan worden gebruikt via Hallo **Azure-portal**, **Azure PowerShell**, **Azure CLI**, of **HDInsight .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="0a931-157">Can be used through hello **Azure portal**, **Azure PowerShell**, **Azure CLI**, or **HDInsight .NET SDK**</span></span>

<span data-ttu-id="0a931-158">Hallo cluster houdt een geschiedenis van alle scripts die hebben is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-158">hello cluster keeps a history of all scripts that have been ran.</span></span> <span data-ttu-id="0a931-159">Hallo-geschiedenis is nuttig wanneer u toofind Hallo-ID van een script nodig hebt voor promotie of degradatie bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-159">hello history is useful when you need toofind hello ID of a script for promotion or demotion operations.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a931-160">Er is geen automatische manier tooundo Hallo wijzigingen die door een script in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="0a931-160">There is no automatic way tooundo hello changes made by a script action.</span></span> <span data-ttu-id="0a931-161">Hallo wijzigingen handmatig ongedaan te maken of een script dat wordt teruggedraaid ze bieden.</span><span class="sxs-lookup"><span data-stu-id="0a931-161">Either manually reverse hello changes or provide a script that reverses them.</span></span>


### <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="0a931-162">Scriptactie in het proces voor het Hallo-cluster maken</span><span class="sxs-lookup"><span data-stu-id="0a931-162">Script Action in hello cluster creation process</span></span>

<span data-ttu-id="0a931-163">Scriptacties gebruikt tijdens het maken van het cluster zijn enigszins afwijken van het script acties worden uitgevoerd op een bestaand cluster:</span><span class="sxs-lookup"><span data-stu-id="0a931-163">Script Actions used during cluster creation are slightly different from script actions ran on an existing cluster:</span></span>

* <span data-ttu-id="0a931-164">Hallo-script is **automatisch persistente**.</span><span class="sxs-lookup"><span data-stu-id="0a931-164">hello script is **automatically persisted**.</span></span>
* <span data-ttu-id="0a931-165">Een **fout** in Hallo script Hallo cluster maken van het proces toofail kan veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="0a931-165">A **failure** in hello script can cause hello cluster creation process toofail.</span></span>

<span data-ttu-id="0a931-166">Hallo volgende diagram wordt weergegeven wanneer het Script wordt uitgevoerd tijdens het maken van een Hallo:</span><span class="sxs-lookup"><span data-stu-id="0a931-166">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="0a931-167">![Aanpassing van HDInsight-cluster en fasen tijdens het maken van het cluster][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="0a931-167">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="0a931-168">Hallo-script wordt uitgevoerd terwijl HDInsight wordt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-168">hello script runs while HDInsight is being configured.</span></span> <span data-ttu-id="0a931-169">In deze fase Hallo Hallo script wordt parallel uitgevoerd in alle opgegeven knooppunten in cluster Hallo en wordt uitgevoerd met basis-bevoegdheden op Hallo knooppunten.</span><span class="sxs-lookup"><span data-stu-id="0a931-169">At this stage, hello script runs in parallel on all hello specified nodes in hello cluster, and runs with root privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="0a931-170">Omdat het Hallo-script wordt uitgevoerd met het niveau bevoegdheid hoofdmap op Hallo clusterknooppunten, kunt u bewerkingen zoals het stoppen en starten van services, met inbegrip van Hadoop-gerelateerde services uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="0a931-170">Because hello script runs with root level privilege on hello cluster nodes, you can perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="0a931-171">Als u services stoppen, moet u ervoor zorgen dat Hallo Ambari-service en andere Hadoop-gerelateerde services actief zijn voordat het Hallo-script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0a931-171">If you stop services, you must ensure that hello Ambari service and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="0a931-172">Deze services zijn vereist toosuccessfully bepalen Hallo gezondheid en status van de cluster Hallo terwijl deze wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a931-172">These services are required toosuccessfully determine hello health and state of hello cluster while it is being created.</span></span>


<span data-ttu-id="0a931-173">U kunt meerdere scriptacties tegelijk gebruiken tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-173">During cluster creation, you can use multiple script actions at once.</span></span> <span data-ttu-id="0a931-174">Deze scripts worden aangeroepen in Hallo volgorde waarin ze zijn opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0a931-174">These scripts are invoked in hello order in which they were specified.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a931-175">Scriptacties moeten binnen 60 minuten of time-out voltooien.</span><span class="sxs-lookup"><span data-stu-id="0a931-175">Script actions must complete within 60 minutes, or timeout.</span></span> <span data-ttu-id="0a931-176">Tijdens de clusterinrichting, voert Hallo script tegelijk met andere processen installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="0a931-176">During cluster provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="0a931-177">Concurrentie voor resources, zoals CPU-tijd of netwerk bandbreedte mogelijk Hallo script tootake langer toofinish dan in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="0a931-177">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>
>
> <span data-ttu-id="0a931-178">toominimize Hallo tijd het duurt toorun Hallo script, taken zoals het downloaden en toepassingen van bron compileren voorkomen.</span><span class="sxs-lookup"><span data-stu-id="0a931-178">toominimize hello time it takes toorun hello script, avoid tasks such as downloading and compiling applications from source.</span></span> <span data-ttu-id="0a931-179">Toepassingen vooraf gecompileerd en Hallo binair in Azure Storage opslaat.</span><span class="sxs-lookup"><span data-stu-id="0a931-179">Pre-compile applications and store hello binary in Azure Storage.</span></span>


### <a name="script-action-on-a-running-cluster"></a><span data-ttu-id="0a931-180">Scriptactie op een actief cluster</span><span class="sxs-lookup"><span data-stu-id="0a931-180">Script action on a running cluster</span></span>

<span data-ttu-id="0a931-181">In tegenstelling tot script acties die worden gebruikt tijdens het maken van het cluster een fout in een script uitgevoerd op een al actief cluster tot niet automatisch toochange Hallo-tooa mislukt clusterstatus.</span><span class="sxs-lookup"><span data-stu-id="0a931-181">Unlike script actions used during cluster creation, a failure in a script ran on an already running cluster does not automatically cause hello cluster toochange tooa failed state.</span></span> <span data-ttu-id="0a931-182">Zodra een script is voltooid, moet tooa status ' actief' hello cluster worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-182">Once a script completes, hello cluster should return tooa "running" state.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0a931-183">Zelfs als Hallo cluster heeft een status 'actief', bevatten hello mislukte script verbroken dingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-183">Even if hello cluster has a 'running' state, hello failed script may have broken things.</span></span> <span data-ttu-id="0a931-184">Een script kan bijvoorbeeld bestanden die nodig zijn door Hallo cluster verwijderen.</span><span class="sxs-lookup"><span data-stu-id="0a931-184">For example, a script could delete files needed by hello cluster.</span></span>
>
> <span data-ttu-id="0a931-185">Scripts acties uitgevoerd met bevoegdheden van de hoofdmap, dus moet u ervoor zorgen dat u wat een script doet begrijpt voordat u het cluster tooyour toepast.</span><span class="sxs-lookup"><span data-stu-id="0a931-185">Scripts actions run with root privileges, so you should make sure that you understand what a script does before applying it tooyour cluster.</span></span>

<span data-ttu-id="0a931-186">Bij het toepassen van een script tooa cluster Hallo clusterstatus toofrom wijzigingen **met** te**geaccepteerde**, klikt u vervolgens **HDInsight configuratie**, en ten slotte terug te**Met** voor geslaagde scripts.</span><span class="sxs-lookup"><span data-stu-id="0a931-186">When applying a script tooa cluster, hello cluster state changes toofrom **Running** too**Accepted**, then **HDInsight configuration**, and finally back too**Running** for successful scripts.</span></span> <span data-ttu-id="0a931-187">Hallo scriptstatus wordt geregistreerd in de geschiedenis van de scriptactie hello en u kunt deze informatie toodetermine of Hallo-script is geslaagd of mislukt.</span><span class="sxs-lookup"><span data-stu-id="0a931-187">hello script status is logged in hello script action history, and you can use this information toodetermine whether hello script succeeded or failed.</span></span> <span data-ttu-id="0a931-188">Bijvoorbeeld, Hallo `Get-AzureRmHDInsightScriptActionHistory` PowerShell-cmdlet kan worden gebruikt tooview Hallo status van een script.</span><span class="sxs-lookup"><span data-stu-id="0a931-188">For example, hello `Get-AzureRmHDInsightScriptActionHistory` PowerShell cmdlet can be used tooview hello status of a script.</span></span> <span data-ttu-id="0a931-189">Deze retourneert informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="0a931-189">It returns information similar toohello following text:</span></span>

    ScriptExecutionId : 635918532516474303
    StartTime         : 8/14/2017 7:40:55 PM
    EndTime           : 8/14/2017 7:41:05 PM
    Status            : Succeeded

> [!NOTE]
> <span data-ttu-id="0a931-190">Als u hebt Hallo cluster (admin) gebruikerswachtwoord gewijzigd nadat het Hallo-cluster is gemaakt, mislukken script acties uitgevoerd op dit cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-190">If you have changed hello cluster user (admin) password after hello cluster was created, script actions ran against this cluster may fail.</span></span> <span data-ttu-id="0a931-191">Als u een persistente scriptacties die doel worker-knooppunten hebt, mislukken deze scripts wanneer u Hallo-cluster schaalt.</span><span class="sxs-lookup"><span data-stu-id="0a931-191">If you have any persisted script actions that target worker nodes, these scripts may fail when you scale hello cluster.</span></span>

## <a name="example-script-action-scripts"></a><span data-ttu-id="0a931-192">Voorbeeld van de scriptactie scripts</span><span class="sxs-lookup"><span data-stu-id="0a931-192">Example Script Action scripts</span></span>

<span data-ttu-id="0a931-193">Script actie scripts kunnen worden gebruikt via Hallo hulpprogramma's te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a931-193">Script Action scripts can be used through hello following utilities:</span></span>

* <span data-ttu-id="0a931-194">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0a931-194">Azure portal</span></span>
* <span data-ttu-id="0a931-195">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a931-195">Azure PowerShell</span></span>
* <span data-ttu-id="0a931-196">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a931-196">Azure CLI</span></span>
* <span data-ttu-id="0a931-197">HDInsight .NET-SDK</span><span class="sxs-lookup"><span data-stu-id="0a931-197">HDInsight .NET SDK</span></span>

<span data-ttu-id="0a931-198">HDInsight biedt scripts tooinstall Hallo onderdelen op HDInsight-clusters te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a931-198">HDInsight provides scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="0a931-199">Naam</span><span class="sxs-lookup"><span data-stu-id="0a931-199">Name</span></span> | <span data-ttu-id="0a931-200">Script</span><span class="sxs-lookup"><span data-stu-id="0a931-200">Script</span></span> |
| --- | --- |
| <span data-ttu-id="0a931-201">**Een Azure Storage-account toevoegen**</span><span class="sxs-lookup"><span data-stu-id="0a931-201">**Add an Azure Storage account**</span></span> |<span data-ttu-id="0a931-202">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxaddstorageaccountv01/Add-Storage-account-v01.sh. Zie [toevoegen extra opslagruimte tooan HDInsight-cluster](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-202">https://hdiconfigactions.blob.core.windows.net/linuxaddstorageaccountv01/add-storage-account-v01.sh. See [Add additional storage tooan HDInsight cluster](hdinsight-hadoop-add-storage.md).</span></span> |
| <span data-ttu-id="0a931-203">**Hue installeren**</span><span class="sxs-lookup"><span data-stu-id="0a931-203">**Install Hue**</span></span> |<span data-ttu-id="0a931-204">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxhueconfigactionv02/Install-HUE-uber-v02.sh. Zie [installeert en gebruikt Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-204">https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh. See [Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> |
| <span data-ttu-id="0a931-205">**Functie installeren**</span><span class="sxs-lookup"><span data-stu-id="0a931-205">**Install Presto**</span></span> |<span data-ttu-id="0a931-206">https://RAW.githubusercontent.com/hdinsight/Presto-hdinsight/master/installpresto.sh. Zie [installeert en gebruikt de functie op HDInsight-clusters](hdinsight-hadoop-install-presto.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-206">https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh. See [Install and use Presto on HDInsight clusters](hdinsight-hadoop-install-presto.md).</span></span> |
| <span data-ttu-id="0a931-207">**Solr installeren**</span><span class="sxs-lookup"><span data-stu-id="0a931-207">**Install Solr**</span></span> |<span data-ttu-id="0a931-208">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsolrconfigactionv01/solr-Installer-v01.sh. Zie [installeert en gebruikt Solr op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-208">https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh. See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> |
| <span data-ttu-id="0a931-209">**Giraph installeren**</span><span class="sxs-lookup"><span data-stu-id="0a931-209">**Install Giraph**</span></span> |<span data-ttu-id="0a931-210">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxgiraphconfigactionv01/giraph-Installer-v01.sh. Zie [installeert en gebruikt Giraph op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-210">https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh. See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> |
| <span data-ttu-id="0a931-211">**Vooraf laden Hive-bibliotheken**</span><span class="sxs-lookup"><span data-stu-id="0a931-211">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="0a931-212">https://hdiconfigactions.BLOB.Core.Windows.NET/linuxsetupcustomhivelibsv01/Setup-customhivelibs-v01.sh. Zie [toevoegen Hive-bibliotheken op HDInsight-clusters](hdinsight-hadoop-add-hive-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-212">https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh. See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md).</span></span> |
| <span data-ttu-id="0a931-213">**Mono installeren of bijwerken**</span><span class="sxs-lookup"><span data-stu-id="0a931-213">**Install or update Mono**</span></span> | <span data-ttu-id="0a931-214">https://hdiconfigactions.BLOB.Core.Windows.NET/Install-mono/Install-mono.Bash.</span><span class="sxs-lookup"><span data-stu-id="0a931-214">https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash.</span></span> <span data-ttu-id="0a931-215">Zie [installeren of update Mono op HDInsight](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-215">See [Install or update Mono on HDInsight](hdinsight-hadoop-install-mono.md).</span></span> |

## <a name="use-a-script-action-during-cluster-creation"></a><span data-ttu-id="0a931-216">Een actie Script gebruiken tijdens het maken van het cluster</span><span class="sxs-lookup"><span data-stu-id="0a931-216">Use a Script Action during cluster creation</span></span>

<span data-ttu-id="0a931-217">Deze sectie bevat voorbeelden op Hallo van de verschillende manieren kunt met scriptacties bij het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-217">This section provides examples on hello different ways you can use script actions when creating an HDInsight cluster.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-azure-portal"></a><span data-ttu-id="0a931-218">Een actie Script gebruiken tijdens het maken van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0a931-218">Use a Script Action during cluster creation from hello Azure portal</span></span>

1. <span data-ttu-id="0a931-219">Beginnen met het maken van een cluster, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-219">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="0a931-220">Wanneer u Hallo bereiken stoppen __Cluster samenvatting__ sectie.</span><span class="sxs-lookup"><span data-stu-id="0a931-220">Stop when you reach hello __Cluster summary__ section.</span></span>

2. <span data-ttu-id="0a931-221">Van Hallo __Cluster samenvatting__ sectie, selecteer Hallo __bewerken__ koppelen voor __geavanceerde instellingen__.</span><span class="sxs-lookup"><span data-stu-id="0a931-221">From hello __Cluster summary__ section, select hello __edit__ link for __Advanced settings__.</span></span>

    ![Koppeling van de geavanceerde instellingen](./media/hdinsight-hadoop-customize-cluster-linux/advanced-settings-link.png)

3. <span data-ttu-id="0a931-223">Van Hallo __geavanceerde instellingen__ sectie __acties Script__.</span><span class="sxs-lookup"><span data-stu-id="0a931-223">From hello __Advanced settings__ section, select __Script actions__.</span></span> <span data-ttu-id="0a931-224">Van Hallo __acties Script__ sectie __+ nieuw verzenden__</span><span class="sxs-lookup"><span data-stu-id="0a931-224">From hello __Script actions__ section, select __+ Submit new__</span></span>

    ![Een nieuwe scriptactie verzenden](./media/hdinsight-hadoop-customize-cluster-linux/add-script-action.png)

4. <span data-ttu-id="0a931-226">Gebruik Hallo __selecteert u een script__ vermelding tooselect een vooraf gemaakte script.</span><span class="sxs-lookup"><span data-stu-id="0a931-226">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="0a931-227">selecteert u een aangepast script toouse __aangepaste__ en geef vervolgens Hallo __naam__ en __Bash script URI__ voor uw script.</span><span class="sxs-lookup"><span data-stu-id="0a931-227">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Een script in een select script Hallo toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="0a931-229">Hallo volgende tabel beschrijft Hallo elementen op Hallo formulier:</span><span class="sxs-lookup"><span data-stu-id="0a931-229">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="0a931-230">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0a931-230">Property</span></span> | <span data-ttu-id="0a931-231">Waarde</span><span class="sxs-lookup"><span data-stu-id="0a931-231">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0a931-232">Selecteer een script</span><span class="sxs-lookup"><span data-stu-id="0a931-232">Select a script</span></span> | <span data-ttu-id="0a931-233">toouse uw eigen script, selecteer __aangepaste__.</span><span class="sxs-lookup"><span data-stu-id="0a931-233">toouse your own script, select __Custom__.</span></span> <span data-ttu-id="0a931-234">Selecteer een van de Hallo is aangeleverd scripts.</span><span class="sxs-lookup"><span data-stu-id="0a931-234">Otherwise, select one of hello provided scripts.</span></span> |
    | <span data-ttu-id="0a931-235">Naam</span><span class="sxs-lookup"><span data-stu-id="0a931-235">Name</span></span> |<span data-ttu-id="0a931-236">Geef een naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a931-236">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="0a931-237">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="0a931-237">Bash script URI</span></span> |<span data-ttu-id="0a931-238">Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-238">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="0a931-239">Worker-HEAD/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="0a931-239">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="0a931-240">Hallo-knooppunten opgeven (**Head**, **Worker**, of **ZooKeeper**) op waarin aanpassing Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-240">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="0a931-241">Parameters</span><span class="sxs-lookup"><span data-stu-id="0a931-241">Parameters</span></span> |<span data-ttu-id="0a931-242">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="0a931-242">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="0a931-243">Gebruik Hallo __deze scriptactie__ vermelding tooensure die Hallo script wordt toegepast tijdens het schalen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-243">Use hello __Persist this script action__ entry tooensure that hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="0a931-244">Selecteer __maken__ toosave Hallo script.</span><span class="sxs-lookup"><span data-stu-id="0a931-244">Select __Create__ toosave hello script.</span></span> <span data-ttu-id="0a931-245">Vervolgens kunt u __+ indienen nieuwe__ tooadd een ander script.</span><span class="sxs-lookup"><span data-stu-id="0a931-245">You can then use __+ Submit new__ tooadd another script.</span></span>

    ![Meerdere scriptacties](./media/hdinsight-hadoop-customize-cluster-linux/multiple-scripts.png)

    <span data-ttu-id="0a931-247">Wanneer u klaar bent met het toe te voegen scripts gebruiken Hallo __Selecteer__ knop en vervolgens Hallo __volgende__ knop tooreturn toohello __Cluster samenvatting__ sectie.</span><span class="sxs-lookup"><span data-stu-id="0a931-247">When you are done adding scripts, use hello __Select__ button, and then hello __Next__ button tooreturn toohello __Cluster summary__ section.</span></span>

3. <span data-ttu-id="0a931-248">toocreate hello cluster, selecteer __maken__ van Hallo __Cluster samenvatting__ selectie.</span><span class="sxs-lookup"><span data-stu-id="0a931-248">toocreate hello cluster, select __Create__ from hello __Cluster summary__ selection.</span></span>

### <a name="use-a-script-action-from-azure-resource-manager-templates"></a><span data-ttu-id="0a931-249">Gebruik de actie van een Script van Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="0a931-249">Use a Script Action from Azure Resource Manager templates</span></span>

<span data-ttu-id="0a931-250">Hallo-voorbeelden in deze sectie laten zien hoe toouse script acties met Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="0a931-250">hello examples in this section demonstrate how toouse script actions with Azure Resource Manager templates.</span></span>

#### <a name="before-you-begin"></a><span data-ttu-id="0a931-251">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0a931-251">Before you begin</span></span>

* <span data-ttu-id="0a931-252">Zie voor meer informatie over het configureren van een werkstation toorun HDInsight Powershell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a931-252">For information about configuring a workstation toorun HDInsight Powershell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="0a931-253">Voor instructies over het toocreate sjablonen, Zie [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-253">For instructions on how toocreate templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="0a931-254">Als u niet eerder hebt gebruikt Azure PowerShell met Resource Manager, raadpleegt u [Azure PowerShell gebruiken met Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-254">If you have not previously used Azure PowerShell with Resource Manager, see [Using Azure PowerShell with Azure Resource Manager](../azure-resource-manager/powershell-azure-resource-manager.md).</span></span>

#### <a name="create-clusters-using-script-action"></a><span data-ttu-id="0a931-255">Maken van clusters met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="0a931-255">Create clusters using Script Action</span></span>

1. <span data-ttu-id="0a931-256">Hallo sjabloon tooa locatie volgen op uw computer kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0a931-256">Copy hello following template tooa location on your computer.</span></span> <span data-ttu-id="0a931-257">Deze sjabloon installeert Giraph op Hallo headnodes en worker-knooppunten in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-257">This template installs Giraph on hello headnodes and worker nodes in hello cluster.</span></span> <span data-ttu-id="0a931-258">U kunt ook controleren of de JSON-sjabloon Hallo geldig is.</span><span class="sxs-lookup"><span data-stu-id="0a931-258">You can also verify if hello JSON template is valid.</span></span> <span data-ttu-id="0a931-259">Plak de inhoud in sjabloon [JSONLint](http://jsonlint.com/), een online JSON-validatiehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="0a931-259">Paste your template content into [JSONLint](http://jsonlint.com/), an online JSON validation tool.</span></span>

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
2. <span data-ttu-id="0a931-260">Open Azure PowerShell en tooyour aanmelden met Azure-account.</span><span class="sxs-lookup"><span data-stu-id="0a931-260">Start Azure PowerShell and Log in tooyour Azure account.</span></span> <span data-ttu-id="0a931-261">Na het opgeven van referenties van uw retourneert Hallo opdracht informatie over uw account.</span><span class="sxs-lookup"><span data-stu-id="0a931-261">After providing your credentials, hello command returns information about your account.</span></span>

        Add-AzureRmAccount

        Id                             Type       ...
        --                             ----
        someone@example.com            User       ...
3. <span data-ttu-id="0a931-262">Als u meerdere abonnementen, bieden Hallo abonnements-ID hebt willen toouse voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="0a931-262">If you have multiple subscriptions, provide hello subscription ID you wish toouse for deployment.</span></span>

        Select-AzureRmSubscription -SubscriptionID <YourSubscriptionId>

    > [!NOTE]
    > <span data-ttu-id="0a931-263">U kunt `Get-AzureRmSubscription` tooget een lijst met alle abonnementen die zijn gekoppeld aan je account, waaronder Hallo abonnements-ID voor elk criterium.</span><span class="sxs-lookup"><span data-stu-id="0a931-263">You can use `Get-AzureRmSubscription` tooget a list of all subscriptions associated with your account, which includes hello subscription ID for each one.</span></span>

4. <span data-ttu-id="0a931-264">Als u een bestaande resourcegroep niet hebt, kunt u een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="0a931-264">If you do not have an existing resource group, create a resource group.</span></span> <span data-ttu-id="0a931-265">Geef de naam op Hallo van Hallo resourcegroep en locatie die u nodig hebt voor uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="0a931-265">Provide hello name of hello resource group and location that you need for your solution.</span></span> <span data-ttu-id="0a931-266">Een samenvatting van de nieuwe resourcegroep hello wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-266">A summary of hello new resource group is returned.</span></span>

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

5. <span data-ttu-id="0a931-267">toocreate een implementatie voor de resourcegroep, Voer Hallo **New-AzureRmResourceGroupDeployment** opdracht in en geef parameters op Hallo die nodig zijn.</span><span class="sxs-lookup"><span data-stu-id="0a931-267">toocreate a deployment for your resource group, run hello **New-AzureRmResourceGroupDeployment** command and provide hello necessary parameters.</span></span> <span data-ttu-id="0a931-268">Hallo-parameters zijn Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a931-268">hello parameters include hello following data:</span></span>

    * <span data-ttu-id="0a931-269">Een naam voor uw implementatie</span><span class="sxs-lookup"><span data-stu-id="0a931-269">A name for your deployment</span></span>
    * <span data-ttu-id="0a931-270">Hallo-naam van de resourcegroep</span><span class="sxs-lookup"><span data-stu-id="0a931-270">hello name of your resource group</span></span>
    * <span data-ttu-id="0a931-271">Hallo-pad of de URL toohello sjabloon die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a931-271">hello path or URL toohello template you created.</span></span>

  <span data-ttu-id="0a931-272">Als de sjabloon parameters vereist, moet u ook deze parameters doorgeven.</span><span class="sxs-lookup"><span data-stu-id="0a931-272">If your template requires any parameters, you must pass those parameters as well.</span></span> <span data-ttu-id="0a931-273">In dit geval is Hallo script actie tooinstall R op Hallo cluster geen parameters vereist.</span><span class="sxs-lookup"><span data-stu-id="0a931-273">In this case, hello script action tooinstall R on hello cluster does not require any parameters.</span></span>

        New-AzureRmResourceGroupDeployment -Name mydeployment -ResourceGroupName myresourcegroup -TemplateFile <PathOrLinkToTemplate>

    <span data-ttu-id="0a931-274">Bent u na vragen aan gebruiker tooprovide waarden voor Hallo-parameters in Hallo sjabloon worden gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-274">You are prompted tooprovide values for hello parameters defined in hello template.</span></span>

1. <span data-ttu-id="0a931-275">Wanneer het Hallo-resourcegroep is geïmplementeerd, wordt een overzicht van Hallo implementatie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a931-275">When hello resource group has been deployed, a summary of hello deployment is displayed.</span></span>

          DeploymentName    : mydeployment
          ResourceGroupName : myresourcegroup
          ProvisioningState : Succeeded
          Timestamp         : 8/14/2017 7:00:27 PM
          Mode              : Incremental
          ...

2. <span data-ttu-id="0a931-276">Als uw implementatie mislukt, kunt u de volgende cmdlets tooget informatie over mislukte Hallo Hallo kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0a931-276">If your deployment fails, you can use hello following cmdlets tooget information about hello failures.</span></span>

        Get-AzureRmResourceGroupDeployment -ResourceGroupName myresourcegroup -ProvisioningState Failed

### <a name="use-a-script-action-during-cluster-creation-from-azure-powershell"></a><span data-ttu-id="0a931-277">Een actie Script gebruiken tijdens het maken van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a931-277">Use a Script Action during cluster creation from Azure PowerShell</span></span>

<span data-ttu-id="0a931-278">In deze sectie gebruiken we Hallo [toevoegen AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts met behulp van de scriptactie toocustomize een cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-278">In this section, we use hello [Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) cmdlet tooinvoke scripts by using Script Action toocustomize a cluster.</span></span> <span data-ttu-id="0a931-279">Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a931-279">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="0a931-280">Zie voor meer informatie over het configureren van een werkstation toorun HDInsight PowerShell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a931-280">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="0a931-281">Hallo volgende script laat zien hoe tooapply een scriptactie bij het maken van een cluster met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="0a931-281">hello following script demonstrates how tooapply a script action when creating a cluster using PowerShell:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=5-90)]

<span data-ttu-id="0a931-282">Het kan enkele minuten duren voordat Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0a931-282">It can take several minutes before hello cluster is created.</span></span>

### <a name="use-a-script-action-during-cluster-creation-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="0a931-283">Een actie Script gebruiken tijdens het maken van Hallo HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0a931-283">Use a Script Action during cluster creation from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="0a931-284">Hallo HDInsight .NET SDK biedt clientbibliotheken die het eenvoudiger toowork met HDInsight vanuit een .NET-toepassing maakt.</span><span class="sxs-lookup"><span data-stu-id="0a931-284">hello HDInsight .NET SDK provides client libraries that makes it easier toowork with HDInsight from a .NET application.</span></span> <span data-ttu-id="0a931-285">Zie voor een voorbeeld van code [maken Linux gebaseerde clusters in HDInsight met behulp Hallo .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span><span class="sxs-lookup"><span data-stu-id="0a931-285">For a code sample, see [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action).</span></span>

## <a name="apply-a-script-action-tooa-running-cluster"></a><span data-ttu-id="0a931-286">Toepassen van een scriptactie tooa met cluster</span><span class="sxs-lookup"><span data-stu-id="0a931-286">Apply a Script Action tooa running cluster</span></span>

<span data-ttu-id="0a931-287">In deze sectie meer informatie over hoe tooapply acties tooa cluster met een script.</span><span class="sxs-lookup"><span data-stu-id="0a931-287">In this section, learn how tooapply script actions tooa running cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-portal"></a><span data-ttu-id="0a931-288">Toepassen van een scriptactie tooa cluster uitvoert vanuit hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0a931-288">Apply a Script Action tooa running cluster from hello Azure portal</span></span>

1. <span data-ttu-id="0a931-289">Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-289">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="0a931-290">Selecteer uit Hallo HDInsight-cluster overzicht Hallo **scriptacties** tegel.</span><span class="sxs-lookup"><span data-stu-id="0a931-290">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="0a931-292">U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** van Hallo gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-292">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

3. <span data-ttu-id="0a931-293">Vanaf de bovenkant van de Hallo Hallo scriptacties sectie, selecteer **indienen nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="0a931-293">From hello top of hello Script Actions section, select **Submit new**.</span></span>

    ![Toevoegen van een script tooa met cluster](./media/hdinsight-hadoop-customize-cluster-linux/add-script-running-cluster.png)

4. <span data-ttu-id="0a931-295">Gebruik Hallo __selecteert u een script__ vermelding tooselect een vooraf gemaakte script.</span><span class="sxs-lookup"><span data-stu-id="0a931-295">Use hello __Select a script__ entry tooselect a pre-made script.</span></span> <span data-ttu-id="0a931-296">selecteert u een aangepast script toouse __aangepaste__ en geef vervolgens Hallo __naam__ en __Bash script URI__ voor uw script.</span><span class="sxs-lookup"><span data-stu-id="0a931-296">toouse a custom script, select __Custom__ and then provide hello __Name__ and __Bash script URI__ for your script.</span></span>

    ![Een script in een select script Hallo toevoegen](./media/hdinsight-hadoop-customize-cluster-linux/select-script.png)

    <span data-ttu-id="0a931-298">Hallo volgende tabel beschrijft Hallo elementen op Hallo formulier:</span><span class="sxs-lookup"><span data-stu-id="0a931-298">hello following table describes hello elements on hello form:</span></span>

    | <span data-ttu-id="0a931-299">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0a931-299">Property</span></span> | <span data-ttu-id="0a931-300">Waarde</span><span class="sxs-lookup"><span data-stu-id="0a931-300">Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="0a931-301">Selecteer een script</span><span class="sxs-lookup"><span data-stu-id="0a931-301">Select a script</span></span> | <span data-ttu-id="0a931-302">toouse uw eigen script, selecteer __aangepaste__.</span><span class="sxs-lookup"><span data-stu-id="0a931-302">toouse your own script, select __custom__.</span></span> <span data-ttu-id="0a931-303">Anders selecteert u een geleverde script.</span><span class="sxs-lookup"><span data-stu-id="0a931-303">Otherwise, select a provided script.</span></span> |
    | <span data-ttu-id="0a931-304">Naam</span><span class="sxs-lookup"><span data-stu-id="0a931-304">Name</span></span> |<span data-ttu-id="0a931-305">Geef een naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="0a931-305">Specify a name for hello script action.</span></span> |
    | <span data-ttu-id="0a931-306">Bash script URI</span><span class="sxs-lookup"><span data-stu-id="0a931-306">Bash script URI</span></span> |<span data-ttu-id="0a931-307">Geef Hallo URI toohello script is aangeroepen toocustomize Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-307">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> |
    | <span data-ttu-id="0a931-308">Worker-HEAD/Zookeeper</span><span class="sxs-lookup"><span data-stu-id="0a931-308">Head/Worker/Zookeeper</span></span> |<span data-ttu-id="0a931-309">Hallo-knooppunten opgeven (**Head**, **Worker**, of **ZooKeeper**) op waarin aanpassing Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-309">Specify hello nodes (**Head**, **Worker**, or **ZooKeeper**) on which hello customization script is run.</span></span> |
    | <span data-ttu-id="0a931-310">Parameters</span><span class="sxs-lookup"><span data-stu-id="0a931-310">Parameters</span></span> |<span data-ttu-id="0a931-311">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="0a931-311">Specify hello parameters, if required by hello script.</span></span> |

    <span data-ttu-id="0a931-312">Gebruik Hallo __deze scriptactie__ vermelding toomake ervoor Hallo script wordt toegepast tijdens het schalen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-312">Use hello __Persist this script action__ entry toomake sure hello script is applied during scaling operations.</span></span>

5. <span data-ttu-id="0a931-313">Gebruik tot slot Hallo **maken** knop tooapply Hallo script toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-313">Finally, use hello **Create** button tooapply hello script toohello cluster.</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-azure-powershell"></a><span data-ttu-id="0a931-314">Toepassen van een scriptactie tooa cluster uitvoeren vanaf Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a931-314">Apply a Script Action tooa running cluster from Azure PowerShell</span></span>

<span data-ttu-id="0a931-315">Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0a931-315">Before proceeding, make sure you have installed and configured Azure PowerShell.</span></span> <span data-ttu-id="0a931-316">Zie voor meer informatie over het configureren van een werkstation toorun HDInsight PowerShell-cmdlets [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0a931-316">For information about configuring a workstation toorun HDInsight PowerShell cmdlets, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="0a931-317">Hallo volgende voorbeeld laat zien hoe tooapply een script actie tooa actief cluster:</span><span class="sxs-lookup"><span data-stu-id="0a931-317">hello following example demonstrates how tooapply a script action tooa running cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=105-117)]

<span data-ttu-id="0a931-318">Zodra het Hallo-bewerking is voltooid, wordt informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="0a931-318">Once hello operation completes, you receive information similar toohello following text:</span></span>

    OperationState  : Succeeded
    ErrorMessage    :
    Name            : Giraph
    Uri             : https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh
    Parameters      :
    NodeTypes       : {HeadNode, WorkerNode}

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-azure-cli"></a><span data-ttu-id="0a931-319">Toepassen van een scriptactie tooa cluster uitvoert vanuit hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0a931-319">Apply a Script Action tooa running cluster from hello Azure CLI</span></span>

<span data-ttu-id="0a931-320">Voordat u doorgaat, zorg ervoor dat u hebt geïnstalleerd en geconfigureerd hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="0a931-320">Before proceeding, make sure you have installed and configured hello Azure CLI.</span></span> <span data-ttu-id="0a931-321">Zie voor meer informatie [installeren hello Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-321">For more information, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="0a931-322">tooswitch tooAzure modus Resource Manager, gebruikt u na de opdracht op de opdrachtregel Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="0a931-322">tooswitch tooAzure Resource Manager mode, use hello following command at hello command line:</span></span>

        azure config mode arm

2. <span data-ttu-id="0a931-323">Gebruik hello tooauthenticate tooyour Azure-abonnement te volgen.</span><span class="sxs-lookup"><span data-stu-id="0a931-323">Use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

3. <span data-ttu-id="0a931-324">Hallo opdracht tooapply na een script actie tooa actief cluster gebruiken</span><span class="sxs-lookup"><span data-stu-id="0a931-324">Use hello following command tooapply a script action tooa running cluster</span></span>

        azure hdinsight script-action create <clustername> -g <resourcegroupname> -n <scriptname> -u <scriptURI> -t <nodetypes>

    <span data-ttu-id="0a931-325">Als u de parameters voor deze opdracht weglaat, wordt u gevraagd deze.</span><span class="sxs-lookup"><span data-stu-id="0a931-325">If you omit parameters for this command, you are prompted for them.</span></span> <span data-ttu-id="0a931-326">Als script die u met opgeeft Hallo `-u` accepteert parameters, kunt u ze met behulp van Hallo `-p` parameter.</span><span class="sxs-lookup"><span data-stu-id="0a931-326">If hello script you specify with `-u` accepts parameters, you can specify them using hello `-p` parameter.</span></span>

    <span data-ttu-id="0a931-327">Geldige knooppunt-typen zijn `headnode`, `workernode`, en `zookeeper`.</span><span class="sxs-lookup"><span data-stu-id="0a931-327">Valid node types are `headnode`, `workernode`, and `zookeeper`.</span></span> <span data-ttu-id="0a931-328">Als Hallo script knooppunttypen toegepaste toomultiple moet, geef Hallo typen gescheiden door een ';'.</span><span class="sxs-lookup"><span data-stu-id="0a931-328">If hello script should be applied toomultiple node types, specify hello types separated by a ';'.</span></span> <span data-ttu-id="0a931-329">Bijvoorbeeld `-n headnode;workernode`.</span><span class="sxs-lookup"><span data-stu-id="0a931-329">For example, `-n headnode;workernode`.</span></span>

    <span data-ttu-id="0a931-330">toopersist Hallo script, Hallo toevoegen `--persistOnSuccess`.</span><span class="sxs-lookup"><span data-stu-id="0a931-330">toopersist hello script, add hello `--persistOnSuccess`.</span></span> <span data-ttu-id="0a931-331">U kunt ook deze persistent maken Hallo script later met behulp van `azure hdinsight script-action persisted set`.</span><span class="sxs-lookup"><span data-stu-id="0a931-331">You can also persist hello script later by using `azure hdinsight script-action persisted set`.</span></span>

    <span data-ttu-id="0a931-332">Zodra het Hallo-taak is voltooid, wordt uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="0a931-332">Once hello job completes, you receive output similar toohello following text:</span></span>

        info:    Executing command hdinsight script-action create
        + Executing Script Action on HDInsight cluster
        data:    Operation Info
        data:    ---------------
        data:    Operation status:
        data:    Operation ID:  b707b10e-e633-45c0-baa9-8aed3d348c13
        info:    hdinsight script-action create command OK

### <a name="apply-a-script-action-tooa-running-cluster-using-rest-api"></a><span data-ttu-id="0a931-333">Toepassen van een scriptactie tooa actief cluster met behulp van REST-API</span><span class="sxs-lookup"><span data-stu-id="0a931-333">Apply a Script Action tooa running cluster using REST API</span></span>

<span data-ttu-id="0a931-334">Zie [scriptacties uitvoeren op een actief cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span><span class="sxs-lookup"><span data-stu-id="0a931-334">See [Run Script Actions on a running cluster](https://msdn.microsoft.com/library/azure/mt668441.aspx).</span></span>

### <a name="apply-a-script-action-tooa-running-cluster-from-hello-hdinsight-net-sdk"></a><span data-ttu-id="0a931-335">Toepassen van een scriptactie tooa cluster uitvoert vanuit Hallo HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0a931-335">Apply a Script Action tooa running cluster from hello HDInsight .NET SDK</span></span>

<span data-ttu-id="0a931-336">Zie voor een voorbeeld van het gebruik van Hallo .NET SDK tooapply scripts tooa cluster [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="0a931-336">For an example of using hello .NET SDK tooapply scripts tooa cluster, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

## <a name="view-history-promote-and-demote-script-actions"></a><span data-ttu-id="0a931-337">Geschiedenis weergeven en degraderen scriptacties promoveren</span><span class="sxs-lookup"><span data-stu-id="0a931-337">View history, promote, and demote Script Actions</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="0a931-338">Met behulp van hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="0a931-338">Using hello Azure portal</span></span>

1. <span data-ttu-id="0a931-339">Van Hallo [Azure-portal](https://portal.azure.com), selecteer uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-339">From hello [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span>

2. <span data-ttu-id="0a931-340">Selecteer uit Hallo HDInsight-cluster overzicht Hallo **scriptacties** tegel.</span><span class="sxs-lookup"><span data-stu-id="0a931-340">From hello HDInsight cluster overview, select hello **Script Actions** tile.</span></span>

    ![Script acties tegel](./media/hdinsight-hadoop-customize-cluster-linux/scriptactionstile.png)

   > [!NOTE]
   > <span data-ttu-id="0a931-342">U kunt ook selecteren **alle instellingen** en selecteer vervolgens **scriptacties** van Hallo gedeelte instellingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-342">You can also select **All settings** and then select **Script Actions** from hello Settings section.</span></span>

4. <span data-ttu-id="0a931-343">Een geschiedenis van scripts voor dit cluster wordt weergegeven op Hallo scriptacties sectie.</span><span class="sxs-lookup"><span data-stu-id="0a931-343">A history of scripts for this cluster is displayed on hello Script Actions section.</span></span> <span data-ttu-id="0a931-344">Deze informatie omvat een lijst met persistente scripts.</span><span class="sxs-lookup"><span data-stu-id="0a931-344">This information includes a list of persisted scripts.</span></span> <span data-ttu-id="0a931-345">Hallo onderstaande schermafbeelding ziet u dat Hallo Solr script is uitgevoerd op dit cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-345">In hello screenshot below, you can see that hello Solr script has been ran on this cluster.</span></span> <span data-ttu-id="0a931-346">Hallo schermopname weergegeven de persistente scripts niet.</span><span class="sxs-lookup"><span data-stu-id="0a931-346">hello screenshot does not show any persisted scripts.</span></span>

    ![De sectie Acties script](./media/hdinsight-hadoop-customize-cluster-linux/script-action-history.png)

5. <span data-ttu-id="0a931-348">Sectie met eigenschappen voor dit script Hallo selecteren van een script uit Hallo geschiedenis worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a931-348">Selecting a script from hello history displays hello Properties section for this script.</span></span> <span data-ttu-id="0a931-349">U kunt vanaf de bovenkant van de Hallo van welkomstscherm, Hallo script opnieuw uitvoeren of promoveer deze.</span><span class="sxs-lookup"><span data-stu-id="0a931-349">From hello top of hello screen, you can rerun hello script or promote it.</span></span>

    ![Eigenschappen van de script-acties](./media/hdinsight-hadoop-customize-cluster-linux/promote-script-actions.png)

6. <span data-ttu-id="0a931-351">U kunt ook Hallo **...**  toohello rechts van de vermeldingen op Hallo scriptacties sectie tooperform acties.</span><span class="sxs-lookup"><span data-stu-id="0a931-351">You can also use hello **...** toohello right of entries on hello Script Actions section tooperform actions.</span></span>

    ![Acties... script gebruik](./media/hdinsight-hadoop-customize-cluster-linux/deletepromoted.png)

### <a name="using-azure-powershell"></a><span data-ttu-id="0a931-353">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="0a931-353">Using Azure PowerShell</span></span>

| <span data-ttu-id="0a931-354">Gebruik de volgende Hallo...</span><span class="sxs-lookup"><span data-stu-id="0a931-354">Use hello following...</span></span> | <span data-ttu-id="0a931-355">te...</span><span class="sxs-lookup"><span data-stu-id="0a931-355">too...</span></span> |
| --- | --- |
| <span data-ttu-id="0a931-356">Get-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="0a931-356">Get-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="0a931-357">Informatie over persistente scriptacties ophalen</span><span class="sxs-lookup"><span data-stu-id="0a931-357">Retrieve information on persisted script actions</span></span> |
| <span data-ttu-id="0a931-358">Get-AzureRmHDInsightScriptActionHistory</span><span class="sxs-lookup"><span data-stu-id="0a931-358">Get-AzureRmHDInsightScriptActionHistory</span></span> |<span data-ttu-id="0a931-359">Een geschiedenis van script acties toegepast toohello cluster of details voor een specifiek script ophalen</span><span class="sxs-lookup"><span data-stu-id="0a931-359">Retrieve a history of script actions applied toohello cluster, or details for a specific script</span></span> |
| <span data-ttu-id="0a931-360">Set-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="0a931-360">Set-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="0a931-361">Bijdraagt aan een ad-hoc script actie tooa persistent scriptactie</span><span class="sxs-lookup"><span data-stu-id="0a931-361">Promotes an ad hoc script action tooa persisted script action</span></span> |
| <span data-ttu-id="0a931-362">Remove-AzureRmHDInsightPersistedScriptAction</span><span class="sxs-lookup"><span data-stu-id="0a931-362">Remove-AzureRmHDInsightPersistedScriptAction</span></span> |<span data-ttu-id="0a931-363">Selecteert, wordt een persistent script actie tooan ad-hoc-actie</span><span class="sxs-lookup"><span data-stu-id="0a931-363">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="0a931-364">Met behulp van `Remove-AzureRmHDInsightPersistedScriptAction` wordt niet ongedaan gemaakt Hallo-bewerkingen worden uitgevoerd door een script.</span><span class="sxs-lookup"><span data-stu-id="0a931-364">Using `Remove-AzureRmHDInsightPersistedScriptAction` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="0a931-365">Deze cmdlet worden alleen persistent gemaakte vlag Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0a931-365">This cmdlet only removes hello persisted flag.</span></span>

<span data-ttu-id="0a931-366">Hallo volgende voorbeeldscript wordt gedemonstreerd met behulp van Hallo cmdlets toopromote vervolgens degraderen van een script.</span><span class="sxs-lookup"><span data-stu-id="0a931-366">hello following example script demonstrates using hello cmdlets toopromote, then demote a script.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-script-action/use-script-action.ps1?range=123-140)]

### <a name="using-hello-azure-cli"></a><span data-ttu-id="0a931-367">Hello Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="0a931-367">Using hello Azure CLI</span></span>

| <span data-ttu-id="0a931-368">Gebruik de volgende Hallo...</span><span class="sxs-lookup"><span data-stu-id="0a931-368">Use hello following...</span></span> | <span data-ttu-id="0a931-369">te...</span><span class="sxs-lookup"><span data-stu-id="0a931-369">too...</span></span> |
| --- | --- |
| `azure hdinsight script-action persisted list <clustername>` |<span data-ttu-id="0a931-370">Een lijst met persistente scriptacties ophalen</span><span class="sxs-lookup"><span data-stu-id="0a931-370">Retrieve a list of persisted script actions</span></span> |
| `azure hdinsight script-action persisted show <clustername> <scriptname>` |<span data-ttu-id="0a931-371">Ophalen van gegevens op een specifieke persistente scriptacties actie</span><span class="sxs-lookup"><span data-stu-id="0a931-371">Retrieve information on a specific persisted script action</span></span> |
| `azure hdinsight script-action history list <clustername>` |<span data-ttu-id="0a931-372">Een geschiedenis van script acties toegepast toohello cluster ophalen</span><span class="sxs-lookup"><span data-stu-id="0a931-372">Retrieve a history of script actions applied toohello cluster</span></span> |
| `azure hdinsight script-action history show <clustername> <scriptname>` |<span data-ttu-id="0a931-373">Ophalen van informatie over een specifiek script-actie</span><span class="sxs-lookup"><span data-stu-id="0a931-373">Retrieve information on a specific script action</span></span> |
| `azure hdinsight script action persisted set <clustername> <scriptexecutionid>` |<span data-ttu-id="0a931-374">Bijdraagt aan een ad-hoc script actie tooa persistent scriptactie</span><span class="sxs-lookup"><span data-stu-id="0a931-374">Promotes an ad hoc script action tooa persisted script action</span></span> |
| `azure hdinsight script-action persisted delete <clustername> <scriptname>` |<span data-ttu-id="0a931-375">Selecteert, wordt een persistent script actie tooan ad-hoc-actie</span><span class="sxs-lookup"><span data-stu-id="0a931-375">Demotes a persisted script action tooan ad hoc action</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="0a931-376">Met behulp van `azure hdinsight script-action persisted delete` wordt niet ongedaan gemaakt Hallo-bewerkingen worden uitgevoerd door een script.</span><span class="sxs-lookup"><span data-stu-id="0a931-376">Using `azure hdinsight script-action persisted delete` does not undo hello actions performed by a script.</span></span> <span data-ttu-id="0a931-377">Deze cmdlet worden alleen persistent gemaakte vlag Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0a931-377">This cmdlet only removes hello persisted flag.</span></span>

### <a name="using-hello-hdinsight-net-sdk"></a><span data-ttu-id="0a931-378">Met behulp van Hallo HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0a931-378">Using hello HDInsight .NET SDK</span></span>

<span data-ttu-id="0a931-379">Voor een voorbeeld van het gebruik van Hallo .NET SDK tooretrieve script geschiedenis van een cluster promoten of degraderen van scripts, Zie [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span><span class="sxs-lookup"><span data-stu-id="0a931-379">For an example of using hello .NET SDK tooretrieve script history from a cluster, promote or demote scripts, see [https://github.com/Azure-Samples/hdinsight-dotnet-script-action](https://github.com/Azure-Samples/hdinsight-dotnet-script-action).</span></span>

> [!NOTE]
> <span data-ttu-id="0a931-380">Dit voorbeeld wordt ook hoe een HDInsight-toepassing gebruikt tooinstall Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="0a931-380">This example also demonstrates how tooinstall an HDInsight application using hello .NET SDK.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="0a931-381">Ondersteuning voor open-source software gebruikt op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="0a931-381">Support for open-source software used on HDInsight clusters</span></span>

<span data-ttu-id="0a931-382">Hallo Microsoft Azure HDInsight-service gebruikt een ecosysteem van open-source technologieën gevormd rond Hadoop.</span><span class="sxs-lookup"><span data-stu-id="0a931-382">hello Microsoft Azure HDInsight service uses an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="0a931-383">Microsoft Azure biedt een algemeen niveau van ondersteuning voor de open source-technologieën.</span><span class="sxs-lookup"><span data-stu-id="0a931-383">Microsoft Azure provides a general level of support for open-source technologies.</span></span> <span data-ttu-id="0a931-384">Zie voor meer informatie, Hallo **ondersteuning bereik** sectie Hallo [ondersteuning Veelgestelde vragen over Azure-website](https://azure.microsoft.com/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="0a931-384">For more information, see hello **Support Scope** section of hello [Azure Support FAQ website](https://azure.microsoft.com/support/faq/).</span></span> <span data-ttu-id="0a931-385">Hallo HDInsight-service biedt een extra verificatieniveau van ondersteuning voor ingebouwde onderdelen.</span><span class="sxs-lookup"><span data-stu-id="0a931-385">hello HDInsight service provides an additional level of support for built-in components.</span></span>

<span data-ttu-id="0a931-386">Er zijn twee soorten open source-onderdelen die beschikbaar in Hallo HDInsight-service zijn:</span><span class="sxs-lookup"><span data-stu-id="0a931-386">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="0a931-387">**Ingebouwde onderdelen** -deze onderdelen vooraf zijn geïnstalleerd op HDInsight-clusters en geef de kernfunctionaliteit van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-387">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="0a931-388">YARN ResourceManager Hallo Hive query language (HiveQL) en Hallo Mahout bibliotheek bijvoorbeeld behoren toothis categorie.</span><span class="sxs-lookup"><span data-stu-id="0a931-388">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="0a931-389">Een volledige lijst met clusteronderdelen is beschikbaar in [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-389">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight](hdinsight-component-versioning.md).</span></span>
* <span data-ttu-id="0a931-390">**Aangepaste onderdelen** -u, als een gebruiker van het Hallo-cluster kunt installeren of gebruiken in uw werkbelasting een onderdeel is beschikbaar in Hallo community of door u gemaakte.</span><span class="sxs-lookup"><span data-stu-id="0a931-390">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

> [!WARNING]
> <span data-ttu-id="0a931-391">Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0a931-391">Components provided with hello HDInsight cluster are fully supported.</span></span> <span data-ttu-id="0a931-392">Microsoft Support helpt tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.</span><span class="sxs-lookup"><span data-stu-id="0a931-392">Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="0a931-393">Aangepaste onderdelen ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="0a931-393">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="0a931-394">Microsoft ondersteuning mogelijk kunnen tooresolve Hallo probleem of ze kunnen u vragen tooengage beschikbare kanalen voor Hallo open-source technologieën waar grondige kennis van deze technologie kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="0a931-394">Microsoft support may be able tooresolve hello issue OR they may ask you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="0a931-395">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="0a931-395">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

<span data-ttu-id="0a931-396">Hallo HDInsight-service biedt verschillende manieren toouse aangepaste onderdelen.</span><span class="sxs-lookup"><span data-stu-id="0a931-396">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="0a931-397">Hallo hetzelfde niveau van de ondersteuning van toepassing is, ongeacht hoe een onderdeel gebruikt of is geïnstalleerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-397">hello same level of support applies, regardless of how a component is used or installed on hello cluster.</span></span> <span data-ttu-id="0a931-398">Hallo volgende lijst bevat de meest voorkomende manieren Hallo dat aangepaste onderdelen kunnen worden gebruikt op HDInsight-clusters:</span><span class="sxs-lookup"><span data-stu-id="0a931-398">hello following list describes hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="0a931-399">Verzending van taak - Hadoop- of andere typen taken die worden uitgevoerd of het gebruik van aangepaste onderdelen kan worden verzonden toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-399">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>

2. <span data-ttu-id="0a931-400">Aanpassing van de cluster - tijdens het maken van het cluster, kunt u aanvullende instellingen en aangepaste onderdelen die zijn geïnstalleerd op de clusterknooppunten Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="0a931-400">Cluster customization - During cluster creation, you can specify additional settings and custom components that are installed on hello cluster nodes.</span></span>

3. <span data-ttu-id="0a931-401">Steekproeven - voor populaire aangepaste onderdelen, Microsoft en anderen kunnen voorbeelden van hoe deze onderdelen kunnen worden gebruikt op Hallo HDInsight-clusters bieden.</span><span class="sxs-lookup"><span data-stu-id="0a931-401">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="0a931-402">Deze voorbeelden worden geleverd zonder ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="0a931-402">These samples are provided without support.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0a931-403">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="0a931-403">Troubleshooting</span></span>

<span data-ttu-id="0a931-404">Hier kunt u Ambari web UI tooview informatie die wordt geregistreerd door scriptacties.</span><span class="sxs-lookup"><span data-stu-id="0a931-404">You can use Ambari web UI tooview information logged by script actions.</span></span> <span data-ttu-id="0a931-405">Als Hallo-script is mislukt tijdens maken van het cluster, zijn Hallo Logboeken ook beschikbaar in Hallo standaardopslagaccount die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-405">If hello script fails during cluster creation, hello logs are also available in hello default storage account associated with hello cluster.</span></span> <span data-ttu-id="0a931-406">Deze sectie bevat informatie over hoe tooretrieve Hallo registreert met behulp van deze beide opties.</span><span class="sxs-lookup"><span data-stu-id="0a931-406">This section provides information on how tooretrieve hello logs using both these options.</span></span>

### <a name="using-hello-ambari-web-ui"></a><span data-ttu-id="0a931-407">Met behulp van Hallo Ambari-Webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="0a931-407">Using hello Ambari Web UI</span></span>

1. <span data-ttu-id="0a931-408">Navigeer in uw browser toohttps://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0a931-408">In your browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0a931-409">Vervang CLUSTERNAME door Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-409">Replace CLUSTERNAME with hello name of your HDInsight cluster.</span></span>

    <span data-ttu-id="0a931-410">Voer desgevraagd Hallo beheerder naam (admin) en het wachtwoord voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-410">When prompted, enter hello admin account name (admin) and password for hello cluster.</span></span> <span data-ttu-id="0a931-411">Mogelijk hebt u tooreenter Hallo beheerdersreferenties in een webformulier.</span><span class="sxs-lookup"><span data-stu-id="0a931-411">You may have tooreenter hello admin credentials in a web form.</span></span>

2. <span data-ttu-id="0a931-412">Selecteer in de balk Hallo bovenaan Hallo Hallo pagina Hallo **ops** vermelding.</span><span class="sxs-lookup"><span data-stu-id="0a931-412">From hello bar at hello top of hello page, select hello **ops** entry.</span></span> <span data-ttu-id="0a931-413">Een lijst met huidige en vorige bewerkingen die worden uitgevoerd op Hallo cluster door Ambari wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0a931-413">A list of current and previous operations performed on hello cluster through Ambari is displayed.</span></span>

    ![Ambari web UI-balk met ops geselecteerd](./media/hdinsight-hadoop-customize-cluster-linux/ambari-nav.png)

3. <span data-ttu-id="0a931-415">Zoeken naar Hallo vermeldingen waarvoor **uitvoeren\_customscriptaction** in Hallo **Operations** kolom.</span><span class="sxs-lookup"><span data-stu-id="0a931-415">Find hello entries that have **run\_customscriptaction** in hello **Operations** column.</span></span> <span data-ttu-id="0a931-416">Deze vermeldingen worden gemaakt als Hallo scriptacties uitvoert.</span><span class="sxs-lookup"><span data-stu-id="0a931-416">These entries are created when hello Script Actions run.</span></span>

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/ambariscriptaction.png)

    <span data-ttu-id="0a931-418">tooview hello STDOUT en STDERR uitvoer, selecteer Hallo run\customscriptaction post en detailanalyse Hallo koppelingen.</span><span class="sxs-lookup"><span data-stu-id="0a931-418">tooview hello STDOUT and STDERR output, select hello run\customscriptaction entry and drill down through hello links.</span></span> <span data-ttu-id="0a931-419">Deze uitvoer wordt gegenereerd wanneer het Hallo-script wordt uitgevoerd, en mogelijk bevatten nuttige informatie.</span><span class="sxs-lookup"><span data-stu-id="0a931-419">This output is generated when hello script runs, and may contain useful information.</span></span>

### <a name="access-logs-from-hello-default-storage-account"></a><span data-ttu-id="0a931-420">Toegang tot logboeken van het standaardopslagaccount Hallo</span><span class="sxs-lookup"><span data-stu-id="0a931-420">Access logs from hello default storage account</span></span>

<span data-ttu-id="0a931-421">Als Hallo cluster maken vanwege fout in tooa script actie mislukt, zijn Hallo logboeken toegankelijk vanuit Hallo cluster storage-account.</span><span class="sxs-lookup"><span data-stu-id="0a931-421">If hello cluster creation fails due tooa script action error, hello logs can be accessed from hello cluster storage account.</span></span>

* <span data-ttu-id="0a931-422">Hallo opslag logboeken zijn beschikbaar op `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span><span class="sxs-lookup"><span data-stu-id="0a931-422">hello storage logs are available at `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\CLUSTER_NAME\DATE`.</span></span>

    ![Schermopname van bewerkingen](./media/hdinsight-hadoop-customize-cluster-linux/script_action_logs_in_storage.png)

    <span data-ttu-id="0a931-424">In deze map Hallo logboeken afzonderlijk ingedeeld voor headnode, workernode en zookeeper-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="0a931-424">Under this directory, hello logs are organized separately for headnode, workernode, and zookeeper nodes.</span></span> <span data-ttu-id="0a931-425">Een aantal voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="0a931-425">Some examples are:</span></span>

    * <span data-ttu-id="0a931-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="0a931-426">**Headnode** - `<uniqueidentifier>AmbariDb-hn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="0a931-427">**Werkrolknooppunt** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="0a931-427">**Worker node** - `<uniqueidentifier>AmbariDb-wn0-<generated_value>.cloudapp.net`</span></span>

    * <span data-ttu-id="0a931-428">**Zookeeper-knooppunt** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span><span class="sxs-lookup"><span data-stu-id="0a931-428">**Zookeeper node** - `<uniqueidentifier>AmbariDb-zk0-<generated_value>.cloudapp.net`</span></span>

* <span data-ttu-id="0a931-429">Alle stdout en stderr van de bijbehorende host Hallo is geüpload toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="0a931-429">All stdout and stderr of hello corresponding host is uploaded toohello storage account.</span></span> <span data-ttu-id="0a931-430">Er is een **uitvoer -\*.txt** en **fouten -\*.txt** voor elke scriptactie.</span><span class="sxs-lookup"><span data-stu-id="0a931-430">There is one **output-\*.txt** and **errors-\*.txt** for each script action.</span></span> <span data-ttu-id="0a931-431">Hallo uitvoer-txt-bestand bevat informatie over Hallo URI van Hallo-script dat is uitgevoerd op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="0a931-431">hello output-*.txt file contains information about hello URI of hello script that got run on hello host.</span></span> <span data-ttu-id="0a931-432">Bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="0a931-432">For example</span></span>

        'Start downloading script locally: ', u'https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh'

* <span data-ttu-id="0a931-433">Het is mogelijk dat u een script actie cluster herhaaldelijk met de Hallo maken dezelfde naam.</span><span class="sxs-lookup"><span data-stu-id="0a931-433">It's possible that you repeatedly create a script action cluster with hello same name.</span></span> <span data-ttu-id="0a931-434">In dat geval kunt u de relevante Hallo-logboeken op basis van datum-mapnaam Hallo onderscheiden.</span><span class="sxs-lookup"><span data-stu-id="0a931-434">In such case, you can distinguish hello relevant logs based on hello DATE folder name.</span></span> <span data-ttu-id="0a931-435">Hallo-mapstructuur voor een cluster (mijncluster) gemaakt op verschillende datums verschijnt bijvoorbeeld vergelijkbare toohello logboekvermeldingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="0a931-435">For example, hello folder structure for a cluster (mycluster) created on different dates appears similar toohello following log entries:</span></span>

    <span data-ttu-id="0a931-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span><span class="sxs-lookup"><span data-stu-id="0a931-436">`\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-04` `\STORAGE_ACCOUNT_NAME\DEFAULT_CONTAINER_NAME\custom-scriptaction-logs\mycluster\2015-10-05`</span></span>

* <span data-ttu-id="0a931-437">Als u een script actie cluster met de Hallo maakt dezelfde naam op Hallo dezelfde dag, kunt u Hallo uniek voorvoegsel tooidentify Hallo relevante logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="0a931-437">If you create a script action cluster with hello same name on hello same day, you can use hello unique prefix tooidentify hello relevant log files.</span></span>

* <span data-ttu-id="0a931-438">Als u een cluster in de buurt van 12:00 AM (middernacht) maakt, is het mogelijk dat de logboekbestanden Hallo twee dagen overbruggen.</span><span class="sxs-lookup"><span data-stu-id="0a931-438">If you create a cluster near 12:00AM (midnight), it's possible that hello log files span across two days.</span></span> <span data-ttu-id="0a931-439">In dergelijke gevallen kunt u twee andere datum mappen voor Hallo Zie hetzelfde cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-439">In such cases, you see two different date folders for hello same cluster.</span></span>

* <span data-ttu-id="0a931-440">Uploaden logboek bestanden toohello standaardcontainer kan een too5 minuten, met name voor grote clusters in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="0a931-440">Uploading log files toohello default container can take up too5 mins, especially for large clusters.</span></span> <span data-ttu-id="0a931-441">Dus als u tooaccess Hallo logboeken wilt, moet u niet onmiddellijk verwijderen Hallo cluster als een scriptactie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0a931-441">So, if you want tooaccess hello logs, you should not immediately delete hello cluster if a script action fails.</span></span>

### <a name="ambari-watchdog"></a><span data-ttu-id="0a931-442">Ambari watchdog</span><span class="sxs-lookup"><span data-stu-id="0a931-442">Ambari watchdog</span></span>

> [!WARNING]
> <span data-ttu-id="0a931-443">Hallo-wachtwoord voor Hallo Ambari Watchdog (hdinsightwatchdog) op uw Linux gebaseerde HDInsight-cluster niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="0a931-443">Do not change hello password for hello Ambari Watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0a931-444">Wijzigen van Hallo het wachtwoord voor dit account wordt verbroken Hallo mogelijkheid toorun nieuwe scriptacties op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-444">Changing hello password for this account breaks hello ability toorun new script actions on hello HDInsight cluster.</span></span>

### <a name="cant-import-name-blobservice"></a><span data-ttu-id="0a931-445">Naam BlobService kan niet worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-445">Can't import name BlobService</span></span>

<span data-ttu-id="0a931-446">__Symptomen__: Hallo script actie mislukt.</span><span class="sxs-lookup"><span data-stu-id="0a931-446">__Symptoms__: hello script action fails.</span></span> <span data-ttu-id="0a931-447">Wanneer u hello bewerking in Ambari bekijkt tekst vergelijkbare toohello volgende fout weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0a931-447">Text similar toohello following error is displayed when you view hello operation in Ambari:</span></span>

```
Traceback (most recent call list):
  File "/var/lib/ambari-agent/cache/custom_actions/scripts/run_customscriptaction.py", line 21, in <module>
    from azure.storage.blob import BlobService
ImportError: cannot import name BlobService
```

<span data-ttu-id="0a931-448">__Oorzaak__: deze fout treedt op als Hallo Python Azure Storage client bijwerkt die is opgenomen in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-448">__Cause__: This error occurs if you upgrade hello Python Azure Storage client that is included with hello HDInsight cluster.</span></span> <span data-ttu-id="0a931-449">HDInsight verwacht Azure Storage client 0.20.0.</span><span class="sxs-lookup"><span data-stu-id="0a931-449">HDInsight expects Azure Storage client 0.20.0.</span></span>

<span data-ttu-id="0a931-450">__Resolutie__: tooresolve deze fout handmatig verbinding maken met behulp van tooeach cluster knooppunt `ssh` en Hallo gebruik de volgende opdracht tooreinstall Hallo juiste opslag-clientversie:</span><span class="sxs-lookup"><span data-stu-id="0a931-450">__Resolution__: tooresolve this error, manually connect tooeach cluster node using `ssh` and use hello following command tooreinstall hello correct storage client version:</span></span>

```
sudo pip install azure-storage==0.20.0
```

<span data-ttu-id="0a931-451">Zie voor informatie over het maken van verbinding toohello cluster met SSH, [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0a931-451">For information on connecting toohello cluster with SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="history-doesnt-show-scripts-used-during-cluster-creation"></a><span data-ttu-id="0a931-452">Geschiedenis van niet wordt scripts die worden gebruikt tijdens het maken van het cluster weergegeven</span><span class="sxs-lookup"><span data-stu-id="0a931-452">History doesn't show scripts used during cluster creation</span></span>

<span data-ttu-id="0a931-453">Als uw cluster is gemaakt voordat 15 maart 2016, ziet u mogelijk niet een vermelding in de geschiedenis van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="0a931-453">If your cluster was created before March 15, 2016, you may not see an entry in Script Action history.</span></span> <span data-ttu-id="0a931-454">Als u het formaat van Hallo cluster na 15 maart 2016 Hallo scripts met behulp van tijdens het maken van het cluster worden weergegeven in de geschiedenis zoals die worden toegepast toonew knooppunten in cluster als onderdeel van Hallo Hallo vergroten of verkleinen van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="0a931-454">If you resize hello cluster after March 15, 2016, hello scripts using during cluster creation appear in history as they are applied toonew nodes in hello cluster as part of hello resize operation.</span></span>

<span data-ttu-id="0a931-455">Er zijn twee uitzonderingen:</span><span class="sxs-lookup"><span data-stu-id="0a931-455">There are two exceptions:</span></span>

* <span data-ttu-id="0a931-456">Als uw cluster is gemaakt vóór 1 September 2015.</span><span class="sxs-lookup"><span data-stu-id="0a931-456">If your cluster was created before September 1, 2015.</span></span> <span data-ttu-id="0a931-457">Deze datum is wanneer scriptacties zijn geïntroduceerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-457">This date is when Script Actions were introduced.</span></span> <span data-ttu-id="0a931-458">Een cluster is gemaakt voor deze datum kan niet hebben gebruikt scriptacties voor maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="0a931-458">Any cluster created before this date could not have used Script Actions for cluster creation.</span></span>

* <span data-ttu-id="0a931-459">Als u meerdere scriptacties gebruikt tijdens het maken van het cluster en Hallo dezelfde naam voor meerdere scripts of Hallo gebruikt naam dezelfde, dezelfde URI, maar verschillende parameters voor meerdere scripts.</span><span class="sxs-lookup"><span data-stu-id="0a931-459">If you used multiple Script Actions during cluster creation, and used hello same name for multiple scripts, or hello same name, same URI, but different parameters for multiple scripts.</span></span> <span data-ttu-id="0a931-460">In dergelijke gevallen wordt u Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="0a931-460">In these cases, you receive hello following error:</span></span>

    <span data-ttu-id="0a931-461">Op dit cluster vanwege tooconflicting scriptnamen in bestaande scripts worden geen nieuwe script acties kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0a931-461">No new script actions can be ran on this cluster due tooconflicting script names in existing scripts.</span></span> <span data-ttu-id="0a931-462">Scriptnamen die zijn opgegeven bij het cluster moet maken allemaal uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="0a931-462">Script names provided at cluster create must be all unique.</span></span> <span data-ttu-id="0a931-463">Bestaande scripts worden uitgevoerd op formaat.</span><span class="sxs-lookup"><span data-stu-id="0a931-463">Existing scripts are ran on resize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a931-464">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a931-464">Next steps</span></span>

* [<span data-ttu-id="0a931-465">Scriptactie-scripts ontwikkelen voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a931-465">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions-linux.md)
* [<span data-ttu-id="0a931-466">Installeren en gebruiken van Solr op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="0a931-466">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="0a931-467">Installeren en gebruiken van Giraph op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="0a931-467">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="0a931-468">Extra opslagruimte tooan HDInsight-cluster toevoegen</span><span class="sxs-lookup"><span data-stu-id="0a931-468">Add additional storage tooan HDInsight cluster</span></span>](hdinsight-hadoop-add-storage.md)

[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster-linux/HDI-Cluster-state.png "Fasen tijdens het maken van het cluster"

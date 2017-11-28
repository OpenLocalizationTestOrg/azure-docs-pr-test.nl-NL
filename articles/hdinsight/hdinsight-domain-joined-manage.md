---
title: aaaManage domein HDInsight-clusters - Azure | Microsoft Docs
description: Meer informatie over hoe toomanage domein HDInsight-clusters
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="3dd77-103">Domein-HDInsight-clusters (Preview) beheren</span><span class="sxs-lookup"><span data-stu-id="3dd77-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="3dd77-104">Informatie over het Hallo-gebruikers en Hallo rollen in HDInsight domein en hoe toomanage domein HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="3dd77-104">Learn hello users and hello roles in Domain-joined HDInsight, and how toomanage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="3dd77-105">Gebruikers van domein HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="3dd77-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="3dd77-106">Een HDInsight-cluster is niet domein heeft twee accounts van gebruikers die zijn gemaakt tijdens het Hallo-cluster maken:</span><span class="sxs-lookup"><span data-stu-id="3dd77-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during hello cluster creation:</span></span>

* <span data-ttu-id="3dd77-107">**Ambari admin**: dit account wordt ook wel *Hadoop gebruiker* of *HTTP gebruiker*.</span><span class="sxs-lookup"><span data-stu-id="3dd77-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="3dd77-108">Dit account kan worden gebruikt toolog op tooAmbari op https://&lt;clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3dd77-108">This account can be used toolog on tooAmbari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="3dd77-109">Het kan ook gebruikte toorun query's op de Ambari-weergaven worden, -taken via externe hulpprogramma's (dat wil zeggen PowerShell, Templeton, Visual Studio) uitvoeren en verificatie met de Hallo Hive ODBC-stuurprogramma en BI-tools (dat wil zeggen Excel, Power BI of Tableau).</span><span class="sxs-lookup"><span data-stu-id="3dd77-109">It can also be used toorun queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with hello Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="3dd77-110">**SSH-gebruiker**: dit account kan worden gebruikt met SSH en sudo-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3dd77-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="3dd77-111">Hoofdmap bevoegdheden toohello Linux VM's heeft.</span><span class="sxs-lookup"><span data-stu-id="3dd77-111">It has root privileges toohello Linux VMs.</span></span>

<span data-ttu-id="3dd77-112">Een domein HDInsight-cluster bevat drie nieuwe gebruikers toevoegen tooAmbari Admin en SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="3dd77-112">A domain-joined HDInsight cluster has three new users in addition tooAmbari Admin and SSH user.</span></span>

* <span data-ttu-id="3dd77-113">**Zwerver admin**: dit account is lokale Apache Zwerver Hallo-beheeraccount.</span><span class="sxs-lookup"><span data-stu-id="3dd77-113">**Ranger admin**:  This account is hello local Apache Ranger admin account.</span></span> <span data-ttu-id="3dd77-114">Het is niet een gebruiker met active directory-domein.</span><span class="sxs-lookup"><span data-stu-id="3dd77-114">It is not an active directory domain user.</span></span> <span data-ttu-id="3dd77-115">Dit account worden gebruikt toosetup beleidsregels en zorgen dat andere gebruikers, beheerders of gedelegeerde beheerders (zodat die gebruikers u beleid beheren kunnen).</span><span class="sxs-lookup"><span data-stu-id="3dd77-115">This account can be used toosetup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="3dd77-116">Hallo-gebruikersnaam is standaard *admin* en Hallo wachtwoord is hetzelfde als het beheerderswachtwoord Ambari Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dd77-116">By default, hello username is *admin* and hello password is hello same as hello Ambari admin password.</span></span> <span data-ttu-id="3dd77-117">Hallo wachtwoord kan worden bijgewerkt vanuit de instellingenpagina Hallo in Zwerver.</span><span class="sxs-lookup"><span data-stu-id="3dd77-117">hello password can be updated from hello Settings page in Ranger.</span></span>
* <span data-ttu-id="3dd77-118">**Gebruiker met beheerdersrechten domein cluster**: dit account is een active directory-domeingebruiker aangewezen als het Hadoop-cluster admin zoals Ambari en Zwerver Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dd77-118">**Cluster admin domain user**: This account is an active directory domain user designated as hello Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="3dd77-119">Tijdens het maken van het cluster moet u de referenties van deze gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="3dd77-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="3dd77-120">Deze gebruiker heeft Hallo volgende bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="3dd77-120">This user has hello following privileges:</span></span>

  * <span data-ttu-id="3dd77-121">Lid worden van domein van machines toohello en plaats deze in Hallo organisatie-eenheid die u tijdens het maken van het cluster opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3dd77-121">Join machines toohello domain and place them within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="3dd77-122">Service-principals binnen Hallo organisatie-eenheid die u tijdens het maken van een cluster opgeeft maken.</span><span class="sxs-lookup"><span data-stu-id="3dd77-122">Create service principals within hello OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="3dd77-123">Omgekeerde DNS-vermeldingen te maken.</span><span class="sxs-lookup"><span data-stu-id="3dd77-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="3dd77-124">Opmerking Hallo andere AD-gebruikers hebben deze rechten.</span><span class="sxs-lookup"><span data-stu-id="3dd77-124">Note hello other AD users also have these privileges.</span></span>

    <span data-ttu-id="3dd77-125">Er zijn een aantal eindpunten binnen Hallo-cluster (bijvoorbeeld Templeton) die niet worden beheerd door Zwerver en daarom zijn niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="3dd77-125">There are some end points within hello cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="3dd77-126">Deze eindpunten zijn vergrendeld voor alle gebruikers behalve Hallo cluster admin domeingebruiker.</span><span class="sxs-lookup"><span data-stu-id="3dd77-126">These end points are locked down for all users except hello cluster admin domain user.</span></span>
* <span data-ttu-id="3dd77-127">**Reguliere**: tijdens het maken van het cluster, kunt u meerdere active directory-groepen opgeven.</span><span class="sxs-lookup"><span data-stu-id="3dd77-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="3dd77-128">Hallo-gebruikers in deze groepen worden gesynchroniseerde tooRanger en Ambari.</span><span class="sxs-lookup"><span data-stu-id="3dd77-128">hello users in these groups will be synced tooRanger and Ambari.</span></span> <span data-ttu-id="3dd77-129">Deze gebruikers zijn domeingebruikers en heeft toegang tot tooonly Zwerver beheerde eindpunten (bijvoorbeeld Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="3dd77-129">These users are domain users and will have access tooonly Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="3dd77-130">Alle beleidsregels RBAC Hallo en controle zijn van toepassing toothese gebruikers.</span><span class="sxs-lookup"><span data-stu-id="3dd77-130">All hello RBAC policies and auditing will be applicable toothese users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="3dd77-131">Rollen zijn van een domein HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="3dd77-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="3dd77-132">HDInsight domein hebben Hallo rollen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3dd77-132">Domain-joined HDInsight have hello following roles:</span></span>

* <span data-ttu-id="3dd77-133">Clusterbeheer</span><span class="sxs-lookup"><span data-stu-id="3dd77-133">Cluster Administrator</span></span>
* <span data-ttu-id="3dd77-134">Cluster-Operator</span><span class="sxs-lookup"><span data-stu-id="3dd77-134">Cluster Operator</span></span>
* <span data-ttu-id="3dd77-135">Servicebeheerder</span><span class="sxs-lookup"><span data-stu-id="3dd77-135">Service Administrator</span></span>
* <span data-ttu-id="3dd77-136">Service-Operator</span><span class="sxs-lookup"><span data-stu-id="3dd77-136">Service Operator</span></span>
* <span data-ttu-id="3dd77-137">Cluster-gebruiker</span><span class="sxs-lookup"><span data-stu-id="3dd77-137">Cluster User</span></span>

<span data-ttu-id="3dd77-138">**toosee hello machtigingen van deze rollen**</span><span class="sxs-lookup"><span data-stu-id="3dd77-138">**toosee hello permissions of these roles**</span></span>

1. <span data-ttu-id="3dd77-139">Open Hallo Ambari Management gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="3dd77-139">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="3dd77-140">Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="3dd77-140">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="3dd77-141">In het linkermenu hello, klikt u op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="3dd77-141">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="3dd77-142">Klik op Hallo blauw vraagteken toosee Hallo machtigingen:</span><span class="sxs-lookup"><span data-stu-id="3dd77-142">Click hello blue question mark toosee hello permissions:</span></span>

    ![HDInsight-rolmachtigingen domein](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a><span data-ttu-id="3dd77-144">Hallo Ambari Management UI openen</span><span class="sxs-lookup"><span data-stu-id="3dd77-144">Open hello Ambari Management UI</span></span>
1. <span data-ttu-id="3dd77-145">Meld u aan bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3dd77-145">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3dd77-146">Open uw HDInsight-cluster in een blade.</span><span class="sxs-lookup"><span data-stu-id="3dd77-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="3dd77-147">Zie [lijst en geeft weer clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="3dd77-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="3dd77-148">Klik op **Dashboard** van Hallo bovenste menu tooopen Ambari.</span><span class="sxs-lookup"><span data-stu-id="3dd77-148">Click **Dashboard** from hello top menu tooopen Ambari.</span></span>
4. <span data-ttu-id="3dd77-149">Meld u aan tooAmbari met Hallo cluster administrator domeingebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="3dd77-149">Log on tooAmbari using hello cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="3dd77-150">Klik op Hallo **Admin** vervolgkeuzemenu van Hallo rechterbovenhoek en klik vervolgens op **Ambari beheren**.</span><span class="sxs-lookup"><span data-stu-id="3dd77-150">Click hello **Admin** dropdown menu from hello upper right corner, and then click **Manage Ambari**.</span></span>

    ![HDInsight domein Ambari beheren](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="3dd77-152">Hallo UI ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="3dd77-152">hello UI looks like:</span></span>

    ![Domein HDInsight Ambari de gebruikersinterface voor beheer](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="3dd77-154">Lijst van domeingebruikers Hallo gesynchroniseerd vanuit uw Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dd77-154">List hello domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="3dd77-155">Open Hallo Ambari Management gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="3dd77-155">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="3dd77-156">Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="3dd77-156">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="3dd77-157">In het linkermenu hello, klikt u op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="3dd77-157">From hello left menu, click **Users**.</span></span> <span data-ttu-id="3dd77-158">U ziet alle Hallo gebruikers synchroniseren met uw Active Directory toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3dd77-158">You shall see all hello users synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Domein HDInsight Ambari management UI gebruikers weergeven](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="3dd77-160">Lijst Hallo domeingroepen gesynchroniseerd vanuit uw Active Directory</span><span class="sxs-lookup"><span data-stu-id="3dd77-160">List hello domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="3dd77-161">Open Hallo Ambari Management gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="3dd77-161">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="3dd77-162">Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="3dd77-162">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="3dd77-163">In het linkermenu hello, klikt u op **groepen**.</span><span class="sxs-lookup"><span data-stu-id="3dd77-163">From hello left menu, click **Groups**.</span></span> <span data-ttu-id="3dd77-164">U ziet alle Hallo groepen gesynchroniseerd vanuit uw Active Directory toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3dd77-164">You shall see all hello groups synced from your Active Directory toohello HDInsight cluster.</span></span>

    ![Domein HDInsight Ambari-gebruikersinterface lijst beheergroepen](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="3dd77-166">Hive-weergaven machtigingen configureren</span><span class="sxs-lookup"><span data-stu-id="3dd77-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="3dd77-167">Open Hallo Ambari Management gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="3dd77-167">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="3dd77-168">Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="3dd77-168">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="3dd77-169">In het linkermenu hello, klikt u op **weergaven**.</span><span class="sxs-lookup"><span data-stu-id="3dd77-169">From hello left menu, click **Views**.</span></span>
3. <span data-ttu-id="3dd77-170">Klik op **HIVE** tooshow Hallo details.</span><span class="sxs-lookup"><span data-stu-id="3dd77-170">Click **HIVE** tooshow hello details.</span></span>

    ![Domein HDInsight Ambari management UI Hive-weergaven](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="3dd77-172">Klik op Hallo **Hive-weergave** tooconfigure Hive-weergaven koppelen.</span><span class="sxs-lookup"><span data-stu-id="3dd77-172">Click hello **Hive View** link tooconfigure Hive Views.</span></span>
5. <span data-ttu-id="3dd77-173">Schuif omlaag toohello **machtigingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="3dd77-173">Scroll down toohello **Permissions** section.</span></span>

    ![Domein HDInsight Ambari management UI Hive-weergaven machtigingen configureren](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="3dd77-175">Klik op **gebruiker toevoegen** of **groep toevoegen**, en geef vervolgens Hallo gebruikers of groepen die Hive-weergaven kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3dd77-175">Click **Add User** or **Add Group**, and then specify hello users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-hello-roles"></a><span data-ttu-id="3dd77-176">Gebruikers voor Hallo rollen configureren</span><span class="sxs-lookup"><span data-stu-id="3dd77-176">Configure users for hello roles</span></span>
 <span data-ttu-id="3dd77-177">Zie voor een lijst met functies en hun machtigingen toosee [rollen van domein HDInsight-clusters](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="3dd77-177">toosee a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="3dd77-178">Open Hallo Ambari Management gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="3dd77-178">Open hello Ambari Management UI.</span></span>  <span data-ttu-id="3dd77-179">Zie [Open Hallo Ambari Management UI](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="3dd77-179">See [Open hello Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="3dd77-180">In het linkermenu hello, klikt u op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="3dd77-180">From hello left menu, click **Roles**.</span></span>
3. <span data-ttu-id="3dd77-181">Klik op **gebruiker toevoegen** of **groep toevoegen** tooassign gebruikers en groepen toodifferent rollen.</span><span class="sxs-lookup"><span data-stu-id="3dd77-181">Click **Add User** or **Add Group** tooassign users and groups toodifferent roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dd77-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3dd77-182">Next steps</span></span>
* <span data-ttu-id="3dd77-183">Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="3dd77-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="3dd77-184">Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3dd77-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="3dd77-185">Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="3dd77-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>

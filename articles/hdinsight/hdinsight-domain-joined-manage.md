---
title: Domein-HDInsight-clusters - Azure beheren | Microsoft Docs
description: Informatie over het beheren van domein HDInsight-clusters
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
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="070f3-103">Domein-HDInsight-clusters (Preview) beheren</span><span class="sxs-lookup"><span data-stu-id="070f3-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="070f3-104">Informatie over de gebruikers en de rollen in HDInsight domein en het domein van de HDInsight-clusters beheren.</span><span class="sxs-lookup"><span data-stu-id="070f3-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="070f3-105">Gebruikers van domein HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="070f3-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="070f3-106">Een HDInsight-cluster is niet domein heeft twee gebruikersaccounts die zijn gemaakt tijdens het maken van het cluster:</span><span class="sxs-lookup"><span data-stu-id="070f3-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="070f3-107">**Ambari admin**: dit account wordt ook wel *Hadoop gebruiker* of *HTTP gebruiker*.</span><span class="sxs-lookup"><span data-stu-id="070f3-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="070f3-108">Dit account kan worden gebruikt voor aanmelding bij Ambari op https://&lt;clustername >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="070f3-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="070f3-109">Het kan ook worden gebruikt voor query's uitvoeren op de Ambari-weergaven, taken via externe hulpprogramma's (dat wil zeggen PowerShell, Templeton, Visual Studio) uitvoeren en verifiëren met de Hive ODBC-stuurprogramma en de BI-tools (dat wil zeggen Excel, Power BI of Tableau).</span><span class="sxs-lookup"><span data-stu-id="070f3-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="070f3-110">**SSH-gebruiker**: dit account kan worden gebruikt met SSH en sudo-opdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="070f3-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="070f3-111">Deze heeft bevoegdheden van de hoofdmap voor de virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="070f3-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="070f3-112">Een domein HDInsight-cluster heeft drie nieuwe gebruikers naast Ambari Admin en SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="070f3-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="070f3-113">**Zwerver admin**: dit account is het lokale beheerdersaccount van Apache Zwerver.</span><span class="sxs-lookup"><span data-stu-id="070f3-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="070f3-114">Het is niet een gebruiker met active directory-domein.</span><span class="sxs-lookup"><span data-stu-id="070f3-114">It is not an active directory domain user.</span></span> <span data-ttu-id="070f3-115">Dit account kan worden gebruikt beleidsregels instellen en zorgen dat andere gebruikers, beheerders of gedelegeerde beheerders (zodat die gebruikers u beleid beheren kunnen).</span><span class="sxs-lookup"><span data-stu-id="070f3-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="070f3-116">De gebruikersnaam is standaard *admin* en het wachtwoord is hetzelfde als de Ambari Administrator-wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="070f3-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="070f3-117">Het wachtwoord kan worden bijgewerkt via de pagina instellingen in Zwerver.</span><span class="sxs-lookup"><span data-stu-id="070f3-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="070f3-118">**Gebruiker met beheerdersrechten domein cluster**: dit account is een active directory-domeingebruiker aangewezen als de Hadoop-cluster beheerder zoals Ambari en Zwerver.</span><span class="sxs-lookup"><span data-stu-id="070f3-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="070f3-119">Tijdens het maken van het cluster moet u de referenties van deze gebruiker opgeven.</span><span class="sxs-lookup"><span data-stu-id="070f3-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="070f3-120">Deze gebruiker heeft de volgende bevoegdheden:</span><span class="sxs-lookup"><span data-stu-id="070f3-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="070f3-121">Computers toevoegen aan het domein en plaats deze in de organisatie-eenheid die u tijdens het maken van het cluster opgeeft.</span><span class="sxs-lookup"><span data-stu-id="070f3-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="070f3-122">Service-principals binnen de organisatie-eenheid die u tijdens het maken van een cluster opgeeft maken.</span><span class="sxs-lookup"><span data-stu-id="070f3-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="070f3-123">Omgekeerde DNS-vermeldingen te maken.</span><span class="sxs-lookup"><span data-stu-id="070f3-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="070f3-124">Let op dat de AD-gebruikers hebben deze rechten.</span><span class="sxs-lookup"><span data-stu-id="070f3-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="070f3-125">Er zijn een aantal eindpunten binnen het cluster (bijvoorbeeld Templeton) die niet worden beheerd door Zwerver en daarom zijn niet beveiligd.</span><span class="sxs-lookup"><span data-stu-id="070f3-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="070f3-126">Deze eindpunten zijn vergrendeld voor alle gebruikers behalve de domeingebruiker van de cluster-beheerder.</span><span class="sxs-lookup"><span data-stu-id="070f3-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="070f3-127">**Reguliere**: tijdens het maken van het cluster, kunt u meerdere active directory-groepen opgeven.</span><span class="sxs-lookup"><span data-stu-id="070f3-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="070f3-128">De gebruikers in deze groepen worden gesynchroniseerd naar Zwerver en Ambari.</span><span class="sxs-lookup"><span data-stu-id="070f3-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="070f3-129">Deze gebruikers zijn domeingebruikers en hebben toegang tot alleen Zwerver beheerde eindpunten (bijvoorbeeld Hiveserver2).</span><span class="sxs-lookup"><span data-stu-id="070f3-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="070f3-130">Alle het RBAC beleid en de controle zal van toepassing zijn op deze gebruikers.</span><span class="sxs-lookup"><span data-stu-id="070f3-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="070f3-131">Rollen zijn van een domein HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="070f3-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="070f3-132">HDInsight domein hebben de volgende rollen:</span><span class="sxs-lookup"><span data-stu-id="070f3-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="070f3-133">Clusterbeheer</span><span class="sxs-lookup"><span data-stu-id="070f3-133">Cluster Administrator</span></span>
* <span data-ttu-id="070f3-134">Cluster-Operator</span><span class="sxs-lookup"><span data-stu-id="070f3-134">Cluster Operator</span></span>
* <span data-ttu-id="070f3-135">Servicebeheerder</span><span class="sxs-lookup"><span data-stu-id="070f3-135">Service Administrator</span></span>
* <span data-ttu-id="070f3-136">Service-Operator</span><span class="sxs-lookup"><span data-stu-id="070f3-136">Service Operator</span></span>
* <span data-ttu-id="070f3-137">Cluster-gebruiker</span><span class="sxs-lookup"><span data-stu-id="070f3-137">Cluster User</span></span>

<span data-ttu-id="070f3-138">**Om te zien van de machtigingen van deze rollen**</span><span class="sxs-lookup"><span data-stu-id="070f3-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="070f3-139">Ambari Management UI te openen.</span><span class="sxs-lookup"><span data-stu-id="070f3-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="070f3-140">Zie [opent de gebruikersinterface voor het beheer van de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="070f3-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="070f3-141">Klik in het menu links op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="070f3-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="070f3-142">Klik op de blauwe vraagteken om te zien welke machtigingen:</span><span class="sxs-lookup"><span data-stu-id="070f3-142">Click the blue question mark to see the permissions:</span></span>

    ![HDInsight-rolmachtigingen domein](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="070f3-144">De gebruikersinterface voor het beheer van de Ambari openen</span><span class="sxs-lookup"><span data-stu-id="070f3-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="070f3-145">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="070f3-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="070f3-146">Open uw HDInsight-cluster in een blade.</span><span class="sxs-lookup"><span data-stu-id="070f3-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="070f3-147">Zie [lijst en geeft weer clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="070f3-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="070f3-148">Klik op **Dashboard** in het menu bovenaan om Ambari te openen.</span><span class="sxs-lookup"><span data-stu-id="070f3-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="070f3-149">Meld u bij de Ambari met het cluster administrator domeingebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="070f3-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="070f3-150">Klik op de **Admin** vervolgkeuzemenu in de rechterbovenhoek hoek naar rechts en klik vervolgens op **Ambari beheren**.</span><span class="sxs-lookup"><span data-stu-id="070f3-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![HDInsight domein Ambari beheren](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="070f3-152">De gebruikersinterface ziet eruit als:</span><span class="sxs-lookup"><span data-stu-id="070f3-152">The UI looks like:</span></span>

    ![Domein HDInsight Ambari de gebruikersinterface voor beheer](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="070f3-154">Lijst van domeingebruikers gesynchroniseerd vanuit uw Active Directory</span><span class="sxs-lookup"><span data-stu-id="070f3-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="070f3-155">Ambari Management UI te openen.</span><span class="sxs-lookup"><span data-stu-id="070f3-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="070f3-156">Zie [opent de gebruikersinterface voor het beheer van de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="070f3-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="070f3-157">Klik in het menu links op **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="070f3-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="070f3-158">U ziet alle gebruikers gesynchroniseerd vanuit uw Active Directory met het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="070f3-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Domein HDInsight Ambari management UI gebruikers weergeven](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="070f3-160">De domein-groepen die gesynchroniseerd vanuit uw Active Directory</span><span class="sxs-lookup"><span data-stu-id="070f3-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="070f3-161">Ambari Management UI te openen.</span><span class="sxs-lookup"><span data-stu-id="070f3-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="070f3-162">Zie [opent de gebruikersinterface voor het beheer van de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="070f3-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="070f3-163">Klik in het menu links op **groepen**.</span><span class="sxs-lookup"><span data-stu-id="070f3-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="070f3-164">U ziet de groepen die zijn gesynchroniseerd vanuit uw Active Directory met het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="070f3-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![Domein HDInsight Ambari-gebruikersinterface lijst beheergroepen](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="070f3-166">Hive-weergaven machtigingen configureren</span><span class="sxs-lookup"><span data-stu-id="070f3-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="070f3-167">Ambari Management UI te openen.</span><span class="sxs-lookup"><span data-stu-id="070f3-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="070f3-168">Zie [opent de gebruikersinterface voor het beheer van de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="070f3-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="070f3-169">Klik in het menu links op **weergaven**.</span><span class="sxs-lookup"><span data-stu-id="070f3-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="070f3-170">Klik op **HIVE** om de details weer te geven.</span><span class="sxs-lookup"><span data-stu-id="070f3-170">Click **HIVE** to show the details.</span></span>

    ![Domein HDInsight Ambari management UI Hive-weergaven](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="070f3-172">Klik op de **Hive-weergave** koppelen aan het Hive-weergaven configureren.</span><span class="sxs-lookup"><span data-stu-id="070f3-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="070f3-173">Schuif omlaag naar de **machtigingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="070f3-173">Scroll down to the **Permissions** section.</span></span>

    ![Domein HDInsight Ambari management UI Hive-weergaven machtigingen configureren](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="070f3-175">Klik op **gebruiker toevoegen** of **groep toevoegen**, en geef vervolgens de gebruikers of groepen die Hive-weergaven kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="070f3-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="070f3-176">Gebruikers voor de rollen configureren</span><span class="sxs-lookup"><span data-stu-id="070f3-176">Configure users for the roles</span></span>
 <span data-ttu-id="070f3-177">Zie voor een lijst met functies en hun machtigingen [rollen van domein HDInsight-clusters](#roles-of-domain---joined-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="070f3-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="070f3-178">Ambari Management UI te openen.</span><span class="sxs-lookup"><span data-stu-id="070f3-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="070f3-179">Zie [opent de gebruikersinterface voor het beheer van de Ambari](#open-the-ambari-management-ui).</span><span class="sxs-lookup"><span data-stu-id="070f3-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="070f3-180">Klik in het menu links op **rollen**.</span><span class="sxs-lookup"><span data-stu-id="070f3-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="070f3-181">Klik op **gebruiker toevoegen** of **groep toevoegen** gebruikers en groepen toewijzen aan andere rollen.</span><span class="sxs-lookup"><span data-stu-id="070f3-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="070f3-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="070f3-182">Next steps</span></span>
* <span data-ttu-id="070f3-183">Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="070f3-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="070f3-184">Zie [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Hive-beleid configureren voor aan een domein gekoppelde HDInsight-clusters) om Hive-beleid te configureren en Hive-query's uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="070f3-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="070f3-185">Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="070f3-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>

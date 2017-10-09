---
title: beleid voor het Hive in HDInsight domein - Azure aaaConfigure | Microsoft Docs
description: Meer informatie...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="ffd56-103">Hive-beleidsregels configureren in HDInsight dat is gekoppeld aan een domein (voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="ffd56-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="ffd56-104">Meer informatie over hoe tooconfigure Apache Zwerver beleidsregels voor Hive.</span><span class="sxs-lookup"><span data-stu-id="ffd56-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="ffd56-105">In dit artikel maakt u twee Zwerver beleid toorestrict toegang toohello hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="ffd56-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="ffd56-106">Hallo hivesampletable wordt geleverd met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ffd56-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="ffd56-107">Nadat u Hallo beleidsregels hebt geconfigureerd, gebruikt u Excel en ODBC-stuurprogramma tooconnect tooHive tabellen in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ffd56-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ffd56-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ffd56-108">Prerequisites</span></span>
* <span data-ttu-id="ffd56-109">Een HDInsight-cluster dat is gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="ffd56-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="ffd56-110">Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren).</span><span class="sxs-lookup"><span data-stu-id="ffd56-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="ffd56-111">Een werkstation met Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, een zelfstandige versie van Excel 2013 of Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="ffd56-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="ffd56-112">Verbinding maken met tooApache Zwerver Admin-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="ffd56-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="ffd56-113">**tooconnect tooRanger Admin UI**</span><span class="sxs-lookup"><span data-stu-id="ffd56-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="ffd56-114">Verbinding via een browser tooRanger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="ffd56-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="ffd56-115">Hallo-URL is https://&lt;ClusterName >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="ffd56-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ffd56-116">Ranger maakt gebruik van andere referenties dan het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="ffd56-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="ffd56-117">tooprevent browsers referenties uit de cache Hadoop, met nieuwe InPrivate-browser venster tooconnect toohello Zwerver Admin gebruikersinterface gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ffd56-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="ffd56-118">Meld u aan met Hallo cluster administrator domeingebruikersnaam en wachtwoord:</span><span class="sxs-lookup"><span data-stu-id="ffd56-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![Ranger-startpagina van HDInsight dat is gekoppeld aan een domein](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="ffd56-120">Op dit moment werkt Ranger alleen met Yarn en Hive.</span><span class="sxs-lookup"><span data-stu-id="ffd56-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="ffd56-121">Domeingebruikers maken</span><span class="sxs-lookup"><span data-stu-id="ffd56-121">Create Domain users</span></span>
<span data-ttu-id="ffd56-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Aan een domein gekoppelde HDInsight-clusters configureren) hebt u hiveruser1 en hiveuser2 gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ffd56-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="ffd56-123">U gebruikt twee Hallo-gebruikersaccount in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ffd56-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="ffd56-124">Ranger-beleidsregels maken</span><span class="sxs-lookup"><span data-stu-id="ffd56-124">Create Ranger policies</span></span>
<span data-ttu-id="ffd56-125">In deze sectie maakt u twee Ranger-beleidsregels voor toegang tot de hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="ffd56-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="ffd56-126">U geeft de machtiging SELECT op voor verschillende sets kolommen.</span><span class="sxs-lookup"><span data-stu-id="ffd56-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="ffd56-127">Beide gebruikers zijn gemaakt in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Aan een domein gekoppelde HDInsight-clusters configureren).</span><span class="sxs-lookup"><span data-stu-id="ffd56-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="ffd56-128">In de volgende sectie hello, wordt u testen Hallo twee beleidsregels in Excel.</span><span class="sxs-lookup"><span data-stu-id="ffd56-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="ffd56-129">**toocreate Zwerver beleid**</span><span class="sxs-lookup"><span data-stu-id="ffd56-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="ffd56-130">Open de beheerinterface van Ranger.</span><span class="sxs-lookup"><span data-stu-id="ffd56-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="ffd56-131">Zie [tooApache Zwerver Admin gebruikersinterface verbinding](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="ffd56-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="ffd56-132">Klik op **&lt;ClusterName>_hive** onder **Hive**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="ffd56-133">Er worden twee vooraf geconfigureerde beleidsregels weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ffd56-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="ffd56-134">Klik op **nieuw beleid toevoegen**, en voer vervolgens Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="ffd56-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="ffd56-135">Beleidsnaam: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="ffd56-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="ffd56-136">Hive-database: standaard</span><span class="sxs-lookup"><span data-stu-id="ffd56-136">Hive Database: default</span></span>
   * <span data-ttu-id="ffd56-137">Tabel: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="ffd56-137">table: hivesampletable</span></span>
   * <span data-ttu-id="ffd56-138">Hive-kolom:*</span><span class="sxs-lookup"><span data-stu-id="ffd56-138">Hive column: *</span></span>
   * <span data-ttu-id="ffd56-139">Gebruiker selecteren: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="ffd56-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="ffd56-140">Machtigingen: SELECT</span><span class="sxs-lookup"><span data-stu-id="ffd56-140">Permissions: select</span></span>

     ![Ranger Hive-beleidsregels van HDInsight dat is gekoppeld aan een domein configureren](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="ffd56-142">.</span><span class="sxs-lookup"><span data-stu-id="ffd56-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ffd56-143">Als een domeingebruiker niet is ingevuld in Select User, wacht u enkele ogenblikken voor Zwerver toosync bij AAD.</span><span class="sxs-lookup"><span data-stu-id="ffd56-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="ffd56-144">Klik op **toevoegen** toosave Hallo beleid.</span><span class="sxs-lookup"><span data-stu-id="ffd56-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="ffd56-145">Hallo laatste twee stappen toocreate een ander beleid met de volgende eigenschappen Hallo herhalen:</span><span class="sxs-lookup"><span data-stu-id="ffd56-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="ffd56-146">Beleidsnaam: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="ffd56-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="ffd56-147">Hive-database: standaard</span><span class="sxs-lookup"><span data-stu-id="ffd56-147">Hive Database: default</span></span>
   * <span data-ttu-id="ffd56-148">Tabel: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="ffd56-148">table: hivesampletable</span></span>
   * <span data-ttu-id="ffd56-149">Hive-kolom: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="ffd56-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="ffd56-150">Gebruiker selecteren: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="ffd56-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="ffd56-151">Machtigingen: SELECT</span><span class="sxs-lookup"><span data-stu-id="ffd56-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="ffd56-152">Hive ODBC-gegevensbron maken</span><span class="sxs-lookup"><span data-stu-id="ffd56-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="ffd56-153">Hallo-instructies vindt u in [maken Hive ODBC-gegevensbron](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="ffd56-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="ffd56-154">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ffd56-154">Property</span></span>|<span data-ttu-id="ffd56-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ffd56-155">Description</span></span>
    ---|---
    <span data-ttu-id="ffd56-156">Naam van de gegevensbron</span><span class="sxs-lookup"><span data-stu-id="ffd56-156">Data Source Name</span></span>|<span data-ttu-id="ffd56-157">Geef een naam tooyour-gegevensbron</span><span class="sxs-lookup"><span data-stu-id="ffd56-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="ffd56-158">Host</span><span class="sxs-lookup"><span data-stu-id="ffd56-158">Host</span></span>|<span data-ttu-id="ffd56-159">Voer &lt;HDInsightClusterName>.azurehdinsight.net in.</span><span class="sxs-lookup"><span data-stu-id="ffd56-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="ffd56-160">Bijvoorbeeld: myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="ffd56-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="ffd56-161">Poort</span><span class="sxs-lookup"><span data-stu-id="ffd56-161">Port</span></span>|<span data-ttu-id="ffd56-162">Gebruik <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="ffd56-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="ffd56-163">(Deze poort is gewijzigd van 563 too443.)</span><span class="sxs-lookup"><span data-stu-id="ffd56-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="ffd56-164">Database</span><span class="sxs-lookup"><span data-stu-id="ffd56-164">Database</span></span>|<span data-ttu-id="ffd56-165">Gebruik <strong>Standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="ffd56-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="ffd56-166">Type Hive-server</span><span class="sxs-lookup"><span data-stu-id="ffd56-166">Hive Server Type</span></span>|<span data-ttu-id="ffd56-167">Selecteer <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="ffd56-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="ffd56-168">Mechanisme</span><span class="sxs-lookup"><span data-stu-id="ffd56-168">Mechanism</span></span>|<span data-ttu-id="ffd56-169">Selecteer <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="ffd56-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="ffd56-170">HTTP-pad</span><span class="sxs-lookup"><span data-stu-id="ffd56-170">HTTP Path</span></span>|<span data-ttu-id="ffd56-171">Laat dit leeg.</span><span class="sxs-lookup"><span data-stu-id="ffd56-171">Leave it blank.</span></span>
    <span data-ttu-id="ffd56-172">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="ffd56-172">User Name</span></span>|<span data-ttu-id="ffd56-173">Voer hiveuser1@contoso158.onmicrosoft.com. Hallo-domeinnaam bijwerken als deze verschilt.</span><span class="sxs-lookup"><span data-stu-id="ffd56-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="ffd56-174">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="ffd56-174">Password</span></span>|<span data-ttu-id="ffd56-175">Hallo wachtwoord opgeven voor hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="ffd56-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="ffd56-176">Zorg ervoor dat tooclick **Test** voordat u opslaat Hallo-gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="ffd56-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="ffd56-177">Gegevens in Excel importeren vanuit HDInsight</span><span class="sxs-lookup"><span data-stu-id="ffd56-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="ffd56-178">In de laatste sectie hello, kunt u twee beleidsregels hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="ffd56-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="ffd56-179">hiveuser1 heeft Hallo machtiging voor alle Hallo kolommen te selecteren en hiveuser2 Hallo machtiging op twee kolommen te selecteren.</span><span class="sxs-lookup"><span data-stu-id="ffd56-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="ffd56-180">In deze sectie imiteren u Hallo twee gebruikers tooimport gegevens in Excel.</span><span class="sxs-lookup"><span data-stu-id="ffd56-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="ffd56-181">Open een nieuwe of bestaande werkmap in Excel.</span><span class="sxs-lookup"><span data-stu-id="ffd56-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="ffd56-182">Van Hallo **gegevens** tabblad **van andere gegevensbronnen**, en klik vervolgens op **van Wizard Gegevensverbinding** toolaunch hello **Wizard Gegevensverbinding**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="ffd56-183">![Open de Wizard Gegevensverbinding][img hdi simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="ffd56-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="ffd56-184">Selecteer **ODBC DSN** als Hallo gegevensbron en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="ffd56-185">Van ODBC-gegevensbronnen, selecteer Hallo gegevensbron naam die u hebt gemaakt in de vorige stap Hallo en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="ffd56-186">Wachtwoord voor Hallo-cluster in de wizard Hallo Hallo opnieuw invoeren en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="ffd56-187">Wachten op Hallo **Database en tabel selecteren** dialoogvenster tooopen.</span><span class="sxs-lookup"><span data-stu-id="ffd56-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="ffd56-188">Dit kan een paar seconden duren.</span><span class="sxs-lookup"><span data-stu-id="ffd56-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="ffd56-189">Selecteer **hivesampletable** en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="ffd56-190">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-190">Click **Finish**.</span></span>
8. <span data-ttu-id="ffd56-191">In Hallo **importgegevens** dialoogvenster kunt u wijzigen of Hallo query opgeven.</span><span class="sxs-lookup"><span data-stu-id="ffd56-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="ffd56-192">toodo hiervoor, klikt u op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="ffd56-193">Dit kan een paar seconden duren.</span><span class="sxs-lookup"><span data-stu-id="ffd56-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="ffd56-194">Klik op Hallo **definitie** tabblad Hallo opdrachttekst is:</span><span class="sxs-lookup"><span data-stu-id="ffd56-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="ffd56-195">Hallo Zwerver beleid dat u hebt gedefinieerd, heeft hiveuser1 machtiging select voor alle Hallo-kolommen.</span><span class="sxs-lookup"><span data-stu-id="ffd56-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="ffd56-196">Deze query werkt dus met de referenties van hiveuser1, maar niet met de referenties van hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="ffd56-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="ffd56-197">![Verbindingseigenschappen][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="ffd56-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="ffd56-198">Klik op **OK** tooclose Hallo verbindingseigenschappen dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffd56-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="ffd56-199">Klik op **OK** tooclose hello **importgegevens** dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="ffd56-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="ffd56-200">Hallo-wachtwoord voor hiveuser1 opnieuw op en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ffd56-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="ffd56-201">Het duurt een paar seconden voordat gegevens geïmporteerde tooExcel opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ffd56-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="ffd56-202">Wanneer dit is voltooid, worden er 11 kolommen met gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ffd56-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="ffd56-203">tootest hello tweede beleid (lezen hivesampletable devicemake) die u hebt gemaakt in de laatste sectie Hallo</span><span class="sxs-lookup"><span data-stu-id="ffd56-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="ffd56-204">Voeg een nieuw blad in Excel toe.</span><span class="sxs-lookup"><span data-stu-id="ffd56-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="ffd56-205">Ga als volgt Hallo laatste procedure tooimport Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="ffd56-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="ffd56-206">Hallo enige wijziging die u neemt is toouse hiveuser2 van referenties in plaats van hiveuser1 van.</span><span class="sxs-lookup"><span data-stu-id="ffd56-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="ffd56-207">Dit zal mislukken omdat hiveuser2 alleen machtiging toosee twee kolommen heeft.</span><span class="sxs-lookup"><span data-stu-id="ffd56-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="ffd56-208">U moet ophalen Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="ffd56-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="ffd56-209">Volg dezelfde Hallo procedure tooimport gegevens.</span><span class="sxs-lookup"><span data-stu-id="ffd56-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="ffd56-210">Deze tijd gebruik hiveuser2 van referenties en Hallo select-instructie uit te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="ffd56-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="ffd56-211">in:</span><span class="sxs-lookup"><span data-stu-id="ffd56-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="ffd56-212">Wanneer dit is voltooid, worden er twee kolommen met geïmporteerde gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ffd56-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ffd56-213">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ffd56-213">Next steps</span></span>
* <span data-ttu-id="ffd56-214">Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="ffd56-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="ffd56-215">Zie [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Aan een domein gekoppelde HDInsight-clusters beheren) om HDInsight-clusters te beheren die zijn gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="ffd56-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="ffd56-216">Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="ffd56-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="ffd56-217">Zie voor Hive-verbinding te maken met behulp van Hive JDBC, [verbinding tooHive in Azure HDInsight met behulp van Hallo Hive JDBC-stuurprogramma](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="ffd56-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="ffd56-218">Zie voor verbindende Excel tooHadoop met behulp van Hive ODBC [tooHadoop Excel verbinding maken met de Hallo Microsoft Hive ODBC-station](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="ffd56-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="ffd56-219">Zie voor verbindende Excel tooHadoop met Power Query [tooHadoop Excel verbinding maken met Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="ffd56-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>

---
title: Hive-beleid configureren in het domein HDInsight - Azure | Microsoft Docs
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
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="4ce4e-103">Hive-beleidsregels configureren in HDInsight dat is gekoppeld aan een domein (voorbeeld)</span><span class="sxs-lookup"><span data-stu-id="4ce4e-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="4ce4e-104">Hier leert u hoe u Apache Ranger-beleidsregels voor Hive configureert.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="4ce4e-105">In dit artikel maakt u twee Ranger-beleidsregels om toegang tot de hivesampletable te beperken.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="4ce4e-106">De hivesampletable wordt geleverd met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="4ce4e-107">Nadat u de beleidsregels hebt geconfigureerd, gebruikt u Excel en het ODBC-stuurprogramma om verbinding te maken met Hive-tabellen in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ce4e-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4ce4e-108">Prerequisites</span></span>
* <span data-ttu-id="4ce4e-109">Een HDInsight-cluster dat is gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="4ce4e-110">Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren).</span><span class="sxs-lookup"><span data-stu-id="4ce4e-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="4ce4e-111">Een werkstation met Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, een zelfstandige versie van Excel 2013 of Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="4ce4e-112">Verbinding maken met de beheerinterface van Apache Ranger</span><span class="sxs-lookup"><span data-stu-id="4ce4e-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="4ce4e-113">**Verbinding maken met de beheerinterface van Ranger**</span><span class="sxs-lookup"><span data-stu-id="4ce4e-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="4ce4e-114">Maak vanuit een browser verbinding met de beheerinterface van Ranger.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="4ce4e-115">De URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4ce4e-116">Ranger maakt gebruik van andere referenties dan het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="4ce4e-117">Gebruik een nieuw InPrivate-browservenster om verbinding te maken met de beheerinterface van Ranger om te voorkomen dat browsers Hadoop-referenties in de cache gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="4ce4e-118">Meld u aan met de gebruikersnaam en het wachtwoord van het clusterbeheerdomein:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![Ranger-startpagina van HDInsight dat is gekoppeld aan een domein](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="4ce4e-120">Op dit moment werkt Ranger alleen met Yarn en Hive.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="4ce4e-121">Domeingebruikers maken</span><span class="sxs-lookup"><span data-stu-id="4ce4e-121">Create Domain users</span></span>
<span data-ttu-id="4ce4e-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Aan een domein gekoppelde HDInsight-clusters configureren) hebt u hiveruser1 en hiveuser2 gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="4ce4e-123">U gebruikt de twee gebruikersaccounts in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="4ce4e-124">Ranger-beleidsregels maken</span><span class="sxs-lookup"><span data-stu-id="4ce4e-124">Create Ranger policies</span></span>
<span data-ttu-id="4ce4e-125">In deze sectie maakt u twee Ranger-beleidsregels voor toegang tot de hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="4ce4e-126">U geeft de machtiging SELECT op voor verschillende sets kolommen.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="4ce4e-127">Beide gebruikers zijn gemaakt in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Aan een domein gekoppelde HDInsight-clusters configureren).</span><span class="sxs-lookup"><span data-stu-id="4ce4e-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="4ce4e-128">In de volgende sectie test u de twee beleidsregels in Excel.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="4ce4e-129">**Ranger-beleidsregels maken**</span><span class="sxs-lookup"><span data-stu-id="4ce4e-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="4ce4e-130">Open de beheerinterface van Ranger.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="4ce4e-131">Zie [Verbinding maken met de beheerinterface van Apache Ranger](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="4ce4e-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="4ce4e-132">Klik op **&lt;ClusterName>_hive** onder **Hive**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="4ce4e-133">Er worden twee vooraf geconfigureerde beleidsregels weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="4ce4e-134">Klik op **Nieuw beleid toevoegen** en voer de volgende waarden in:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="4ce4e-135">Beleidsnaam: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="4ce4e-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="4ce4e-136">Hive-database: standaard</span><span class="sxs-lookup"><span data-stu-id="4ce4e-136">Hive Database: default</span></span>
   * <span data-ttu-id="4ce4e-137">Tabel: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="4ce4e-137">table: hivesampletable</span></span>
   * <span data-ttu-id="4ce4e-138">Hive-kolom:*</span><span class="sxs-lookup"><span data-stu-id="4ce4e-138">Hive column: *</span></span>
   * <span data-ttu-id="4ce4e-139">Gebruiker selecteren: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="4ce4e-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="4ce4e-140">Machtigingen: SELECT</span><span class="sxs-lookup"><span data-stu-id="4ce4e-140">Permissions: select</span></span>

     ![Ranger Hive-beleidsregels van HDInsight dat is gekoppeld aan een domein configureren](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="4ce4e-142">.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="4ce4e-143">Als een domeingebruiker niet is ingevuld in Gebruiker selecteren, wacht u even, zodat Ranger met AAD kan synchroniseren.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="4ce4e-144">Klik op **Toevoegen** om het beleid op te slaan.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="4ce4e-145">Herhaal de laatste twee stappen, zodat u een ander beleid kunt maken met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="4ce4e-146">Beleidsnaam: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="4ce4e-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="4ce4e-147">Hive-database: standaard</span><span class="sxs-lookup"><span data-stu-id="4ce4e-147">Hive Database: default</span></span>
   * <span data-ttu-id="4ce4e-148">Tabel: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="4ce4e-148">table: hivesampletable</span></span>
   * <span data-ttu-id="4ce4e-149">Hive-kolom: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="4ce4e-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="4ce4e-150">Gebruiker selecteren: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="4ce4e-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="4ce4e-151">Machtigingen: SELECT</span><span class="sxs-lookup"><span data-stu-id="4ce4e-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="4ce4e-152">Hive ODBC-gegevensbron maken</span><span class="sxs-lookup"><span data-stu-id="4ce4e-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="4ce4e-153">De instructies vindt u in [Hive ODBC-gegevensbron maken](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="4ce4e-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="4ce4e-154">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4ce4e-154">Property</span></span>|<span data-ttu-id="4ce4e-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4ce4e-155">Description</span></span>
    ---|---
    <span data-ttu-id="4ce4e-156">Naam van de gegevensbron</span><span class="sxs-lookup"><span data-stu-id="4ce4e-156">Data Source Name</span></span>|<span data-ttu-id="4ce4e-157">Geef uw gegevensbron een naam</span><span class="sxs-lookup"><span data-stu-id="4ce4e-157">Give a name to your data source</span></span>
    <span data-ttu-id="4ce4e-158">Host</span><span class="sxs-lookup"><span data-stu-id="4ce4e-158">Host</span></span>|<span data-ttu-id="4ce4e-159">Voer &lt;HDInsightClusterName>.azurehdinsight.net in.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="4ce4e-160">Bijvoorbeeld: myHDICluster.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="4ce4e-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="4ce4e-161">Poort</span><span class="sxs-lookup"><span data-stu-id="4ce4e-161">Port</span></span>|<span data-ttu-id="4ce4e-162">Gebruik <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="4ce4e-163">(Deze poort is gewijzigd van 563 in 443.)</span><span class="sxs-lookup"><span data-stu-id="4ce4e-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="4ce4e-164">Database</span><span class="sxs-lookup"><span data-stu-id="4ce4e-164">Database</span></span>|<span data-ttu-id="4ce4e-165">Gebruik <strong>Standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="4ce4e-166">Type Hive-server</span><span class="sxs-lookup"><span data-stu-id="4ce4e-166">Hive Server Type</span></span>|<span data-ttu-id="4ce4e-167">Selecteer <strong>Hive Server 2</strong></span><span class="sxs-lookup"><span data-stu-id="4ce4e-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="4ce4e-168">Mechanisme</span><span class="sxs-lookup"><span data-stu-id="4ce4e-168">Mechanism</span></span>|<span data-ttu-id="4ce4e-169">Selecteer <strong>Azure HDInsight Service</strong></span><span class="sxs-lookup"><span data-stu-id="4ce4e-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="4ce4e-170">HTTP-pad</span><span class="sxs-lookup"><span data-stu-id="4ce4e-170">HTTP Path</span></span>|<span data-ttu-id="4ce4e-171">Laat dit leeg.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-171">Leave it blank.</span></span>
    <span data-ttu-id="4ce4e-172">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="4ce4e-172">User Name</span></span>|<span data-ttu-id="4ce4e-173">Voer hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="4ce4e-174">Werk de domeinnaam als deze verschilt.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="4ce4e-175">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="4ce4e-175">Password</span></span>|<span data-ttu-id="4ce4e-176">Voer het wachtwoord van hiveuser1 in.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="4ce4e-177">Zorg ervoor dat u op **Test** klikt voordat u de gegevensbron opslaat.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="4ce4e-178">Gegevens in Excel importeren vanuit HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ce4e-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="4ce4e-179">In de laatste sectie hebt u twee beleidsregels geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="4ce4e-180">hiveuser1 heeft de machtiging SELECT voor alle kolommen en hiveuser2 heeft de machtiging SELECT voor twee kolommen.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="4ce4e-181">In deze sectie imiteert u de twee gebruikers, zodat u gegevens kunt importeren in Excel.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="4ce4e-182">Open een nieuwe of bestaande werkmap in Excel.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="4ce4e-183">Klik op het tabblad **Gegevens** op de optie **Van andere gegevensbronnen** en klik vervolgens op **Van wizard Gegevensverbinding** om de **Wizard Gegevensverbinding** te starten.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="4ce4e-184">![Open de Wizard Gegevensverbinding][img hdi simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="4ce4e-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="4ce4e-185">Selecteer **ODBC DSN** als de gegevensbron en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="4ce4e-186">Selecteer uit ODBC-gegevensbronnen de naam van de gegevensbron die u in de vorige stap hebt gemaakt en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="4ce4e-187">Voer het wachtwoord voor de cluster in de wizard opnieuw in en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="4ce4e-188">Wacht totdat het dialoogvenster **Database en tabel selecteren** wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="4ce4e-189">Dit kan een paar seconden duren.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="4ce4e-190">Selecteer **hivesampletable** en klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="4ce4e-191">Klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-191">Click **Finish**.</span></span>
8. <span data-ttu-id="4ce4e-192">In het dialoogvenster **Gegevens importeren** kunt u de query wijzigen of opgeven.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="4ce4e-193">Als u dit wilt doen, klikt u op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-193">To do so, click **Properties**.</span></span> <span data-ttu-id="4ce4e-194">Dit kan een paar seconden duren.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="4ce4e-195">Klik op het tabblad **Definitie**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-195">Click the **Definition** tab.</span></span> <span data-ttu-id="4ce4e-196">De opdrachttekst is:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="4ce4e-197">Bij de Ranger-beleidsregels hebt u gedefinieerd dat hiveuser1 de machtiging SELECT heeft voor alle kolommen.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="4ce4e-198">Deze query werkt dus met de referenties van hiveuser1, maar niet met de referenties van hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="4ce4e-199">![Verbindingseigenschappen][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="4ce4e-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="4ce4e-200">Klik op **OK** om het dialoogvenster Verbindingseigenschappen te sluiten.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="4ce4e-201">Klik op **OK** om het dialoogvenster **Gegevens importeren** te sluiten.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="4ce4e-202">Voer het wachtwoord van hiveuser1 opnieuw in en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="4ce4e-203">Het duurt een paar seconden voordat de gegevens naar Excel worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="4ce4e-204">Wanneer dit is voltooid, worden er 11 kolommen met gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="4ce4e-205">De tweede beleidsregel (read-hivesampletable-devicemake) testen die u in de laatste sectie hebt gemaakt</span><span class="sxs-lookup"><span data-stu-id="4ce4e-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="4ce4e-206">Voeg een nieuw blad in Excel toe.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="4ce4e-207">Voer de vorige procedure uit om de gegevens te importeren.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="4ce4e-208">De enige wijziging die u aanbrengt, is dat u de referenties van hiveuser2 gebruikt in plaats van die van hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="4ce4e-209">Dit mislukt, omdat hiveuser2 alleen gemachtigd is om twee kolommen te zien.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="4ce4e-210">De volgende fout wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="4ce4e-211">Voer dezelfde procedure uit om gegevens te importeren.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="4ce4e-212">Gebruik deze keer de referenties van hiveuser2 en wijzig ook de SELECT-instructie van:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="4ce4e-213">in:</span><span class="sxs-lookup"><span data-stu-id="4ce4e-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="4ce4e-214">Wanneer dit is voltooid, worden er twee kolommen met geïmporteerde gegevens weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ce4e-215">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ce4e-215">Next steps</span></span>
* <span data-ttu-id="4ce4e-216">Zie [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Aan een domein gekoppelde HDInsight-clusters configureren) om een HDInsight-cluster te configureren dat is gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="4ce4e-217">Zie [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Aan een domein gekoppelde HDInsight-clusters beheren) om HDInsight-clusters te beheren die zijn gekoppeld aan een domein.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="4ce4e-218">Zie voor het uitvoeren van Hive-query's met SSH op domein HDInsight-clusters [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="4ce4e-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="4ce4e-219">Zie [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md) (Verbinding maken met Hive op Azure HDInsight met het Hive JDBC-stuurprogramma) om Hive te verbinden met behulp van Hive JDBC.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="4ce4e-220">Zie [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md) (Excel verbinden met Hadoop met het Microsoft Hive ODBC-station) om Excel te verbinden met Hadoop met behulp van Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="4ce4e-221">Zie [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md) (Excel verbinden met Hadoop via Power Query) om Excel te verbinden met Hadoop met behulp van Power Query.</span><span class="sxs-lookup"><span data-stu-id="4ce4e-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>

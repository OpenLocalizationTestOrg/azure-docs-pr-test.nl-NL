---
title: Een service gesplitste samenvoegen implementeren | Microsoft Docs
description: Splitsen en samenvoegen met hulpprogramma's voor elastische database
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="d8395-103">Een service voor splitsen en samenvoegen implementeren</span><span class="sxs-lookup"><span data-stu-id="d8395-103">Deploy a split-merge service</span></span>
<span data-ttu-id="d8395-104">De splitsing merge-hulpprogramma kunt u gegevens verplaatsen tussen shard-databases.</span><span class="sxs-lookup"><span data-stu-id="d8395-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="d8395-105">Zie [verplaatsen van gegevens tussen cloud uitgebreide databases](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="d8395-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="d8395-106">Downloaden van de pakketten gesplitste samenvoegen</span><span class="sxs-lookup"><span data-stu-id="d8395-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="d8395-107">Download de nieuwste versie van de NuGet van [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="d8395-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="d8395-108">Open een opdrachtprompt en navigeer naar de map waar u nuget.exe gedownload.</span><span class="sxs-lookup"><span data-stu-id="d8395-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="d8395-109">De download bevat PowerShell commmands.</span><span class="sxs-lookup"><span data-stu-id="d8395-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="d8395-110">Download het pakket van de meest recente gesplitste samenvoegen in de huidige map met de onderstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="d8395-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="d8395-111">De bestanden worden geplaatst in een map met de naam **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** waar *x.x.xxx.x* weerspiegelt het versienummer.</span><span class="sxs-lookup"><span data-stu-id="d8395-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="d8395-112">Vinden van de bestanden van de Service gesplitste samenvoegen in de **content\splitmerge\service** onderliggende map en de splitsing samenvoegen PowerShell-scripts (en vereiste client-dll's) in de **content\splitmerge\powershell** onderliggende map.</span><span class="sxs-lookup"><span data-stu-id="d8395-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8395-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d8395-113">Prerequisites</span></span>
1. <span data-ttu-id="d8395-114">Maak een Azure SQL DB-database die wordt gebruikt als de status van de gesplitste samenvoegen-database.</span><span class="sxs-lookup"><span data-stu-id="d8395-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="d8395-115">Ga naar de [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8395-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="d8395-116">Maak een nieuwe **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="d8395-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="d8395-117">Geef een naam op voor de database en maak een nieuwe beheerder en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="d8395-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="d8395-118">Zorg ervoor dat voor het vastleggen van de naam en het wachtwoord voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="d8395-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="d8395-119">Zorg ervoor dat uw Azure SQL DB-server kan Azure-Services tot stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="d8395-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="d8395-120">In de portal in de **firewallinstellingen**, zorg ervoor dat de **toegang tot Azure-Services toestaan** is ingesteld op **op**.</span><span class="sxs-lookup"><span data-stu-id="d8395-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="d8395-121">Klik op het pictogram 'opslaan'.</span><span class="sxs-lookup"><span data-stu-id="d8395-121">Click the "save" icon.</span></span>
   
   ![Toegestane services][1]
3. <span data-ttu-id="d8395-123">Maak een Azure Storage-account dat wordt gebruikt voor diagnostische uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d8395-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="d8395-124">Ga naar de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="d8395-124">Go to the Azure Portal.</span></span> <span data-ttu-id="d8395-125">Klik in de linkerbalk op **nieuw**, klikt u op **gegevens en opslag**, klikt u vervolgens **opslag**.</span><span class="sxs-lookup"><span data-stu-id="d8395-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="d8395-126">Maak een Azure Cloud Service die uw service gesplitste Merge bevat.</span><span class="sxs-lookup"><span data-stu-id="d8395-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="d8395-127">Ga naar de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="d8395-127">Go to the Azure Portal.</span></span> <span data-ttu-id="d8395-128">Klik in de linkerbalk op **nieuw**, klikt u vervolgens **Compute**, **Cloudservice**, en **maken**.</span><span class="sxs-lookup"><span data-stu-id="d8395-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="d8395-129">Configureer uw service gesplitste samenvoegen</span><span class="sxs-lookup"><span data-stu-id="d8395-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="d8395-130">Configuratie gesplitste Merge-service</span><span class="sxs-lookup"><span data-stu-id="d8395-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="d8395-131">In de map waar u de splitsing Merge-assembly's hebt gedownload, maakt u een kopie van de **ServiceConfiguration.Template.cscfg** -bestand dat naast verzonden **SplitMergeService.cspkg** en wijzig deze  **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="d8395-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="d8395-132">Open **ServiceConfiguration.cscfg** in een teksteditor zoals Visual Studio die invoer zoals de indeling van certificaatvingerafdrukken valideert.</span><span class="sxs-lookup"><span data-stu-id="d8395-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="d8395-133">Een nieuwe database maken of kies een bestaande database om te fungeren als de database van de status voor gesplitste samenvoegbewerkingen en de verbindingsreeks van de database ophalen.</span><span class="sxs-lookup"><span data-stu-id="d8395-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="d8395-134">Gebruik de Latijnse sortering op dit moment de status van database (SQL\_Latin1\_algemene\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="d8395-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="d8395-135">Zie voor meer informatie [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="d8395-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="d8395-136">Met Azure SQL DB is de verbindingsreeks meestal van het formulier:</span><span class="sxs-lookup"><span data-stu-id="d8395-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="d8395-137">Deze verbindingsreeks invoeren in het cscfg-bestand in zowel de **SplitMergeWeb** en **SplitMergeWorker** secties van de rol in de instelling ElasticScaleMetadata.</span><span class="sxs-lookup"><span data-stu-id="d8395-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="d8395-138">Voor de **SplitMergeWorker** rol, voer een geldige verbindingsreeks naar Azure-opslag voor de **WorkerRoleSynchronizationStorageAccountConnectionString** instelling.</span><span class="sxs-lookup"><span data-stu-id="d8395-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="d8395-139">Beveiliging configureren</span><span class="sxs-lookup"><span data-stu-id="d8395-139">Configure security</span></span>
<span data-ttu-id="d8395-140">Raadpleeg voor gedetailleerde instructies voor het configureren van de beveiliging van de service de [gesplitste samenvoegen Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d8395-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="d8395-141">Voor de doeleinden van een eenvoudige test-implementatie voor deze zelfstudie wordt een minimaal aantal configuratiestappen worden uitgevoerd voor de service en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d8395-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="d8395-142">Deze stappen alleen het één machine/account inschakelen om te communiceren met de service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d8395-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="d8395-143">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="d8395-143">Create a self-signed certificate</span></span>
<span data-ttu-id="d8395-144">Een nieuwe map maken en uitvoeren vanuit deze map de volgende opdracht uit via een [opdrachtprompt voor ontwikkelaars voor Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) venster:</span><span class="sxs-lookup"><span data-stu-id="d8395-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="d8395-145">U wordt gevraagd om een wachtwoord voor het beveiligen van de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d8395-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="d8395-146">Voer een sterk wachtwoord in en Bevestig het.</span><span class="sxs-lookup"><span data-stu-id="d8395-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="d8395-147">U wordt gevraagd om het wachtwoord voor zodra er meer na die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d8395-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="d8395-148">Klik op **Ja** aan het einde om het te importeren in de vertrouwde certificeringsinstantie instanties basisarchief.</span><span class="sxs-lookup"><span data-stu-id="d8395-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="d8395-149">Een PFX-bestand maken</span><span class="sxs-lookup"><span data-stu-id="d8395-149">Create a PFX file</span></span>
<span data-ttu-id="d8395-150">Voer de volgende opdracht uit hetzelfde venster waar makecert is uitgevoerd. Gebruik hetzelfde wachtwoord dat u gebruikt voor het maken van het certificaat:</span><span class="sxs-lookup"><span data-stu-id="d8395-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="d8395-151">Importeer het clientcertificaat in het persoonlijke archief</span><span class="sxs-lookup"><span data-stu-id="d8395-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="d8395-152">Dubbelklik in Windows Verkenner op **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="d8395-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="d8395-153">In de **Wizard Certificaat importeren** Selecteer **huidige gebruiker** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d8395-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="d8395-154">Bevestig het bestandspad en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d8395-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="d8395-155">Typ het wachtwoord, laat u **alle uitgebreide eigenschappen bevatten** gecontroleerd en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d8395-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="d8395-156">Laat **automatisch het certificaatarchief [...] selecteren**  gecontroleerd en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="d8395-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="d8395-157">Klik op **voltooien** en **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8395-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="d8395-158">Het PFX-bestand uploaden naar de cloudservice</span><span class="sxs-lookup"><span data-stu-id="d8395-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="d8395-159">Ga naar de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d8395-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d8395-160">Selecteer **Cloudservices**.</span><span class="sxs-lookup"><span data-stu-id="d8395-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="d8395-161">Selecteer de cloudservice die u hierboven hebt gemaakt voor de splitsing/Merge-service.</span><span class="sxs-lookup"><span data-stu-id="d8395-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="d8395-162">Klik op **certificaten** in het bovenste menu.</span><span class="sxs-lookup"><span data-stu-id="d8395-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="d8395-163">Klik op **uploaden** in de balk onderaan.</span><span class="sxs-lookup"><span data-stu-id="d8395-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="d8395-164">Selecteer het PFX-bestand en voer hetzelfde wachtwoord als hierboven.</span><span class="sxs-lookup"><span data-stu-id="d8395-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="d8395-165">Als voltooid, kopieert u de vingerafdruk van het certificaat van de nieuwe vermelding in de lijst.</span><span class="sxs-lookup"><span data-stu-id="d8395-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="d8395-166">Het configuratiebestand van de service bijwerken</span><span class="sxs-lookup"><span data-stu-id="d8395-166">Update the service configuration file</span></span>
<span data-ttu-id="d8395-167">Plak de vingerafdruk van het certificaat dat hierboven wordt gekopieerd naar de vingerafdruk kenmerkwaarde van deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="d8395-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="d8395-168">Voor de werkrol:</span><span class="sxs-lookup"><span data-stu-id="d8395-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="d8395-169">Voor de Webrol:</span><span class="sxs-lookup"><span data-stu-id="d8395-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="d8395-170">Dat de implementaties voor productie certificaten scheiden moet worden gebruikt voor de CA, voor versleuteling, het servercertificaat en clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="d8395-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="d8395-171">Zie voor gedetailleerde instructies voor dit [Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="d8395-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="d8395-172">Uw service implementeren</span><span class="sxs-lookup"><span data-stu-id="d8395-172">Deploy your service</span></span>
1. <span data-ttu-id="d8395-173">Ga naar de [Azure Portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="d8395-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="d8395-174">Klik op de **Cloudservices** tabblad aan de linkerkant en selecteer de cloudservice die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d8395-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="d8395-175">Klik op **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="d8395-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="d8395-176">Kies de faseringsomgeving en klik vervolgens op **uploaden van een nieuwe implementatie van de staging**.</span><span class="sxs-lookup"><span data-stu-id="d8395-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Fasering][3]
5. <span data-ttu-id="d8395-178">Voer een implementatielabel in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="d8395-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="d8395-179">Klik voor 'Pakket' en 'Configuration', 'Van Local' en kies de **SplitMergeService.cspkg** bestands- en uw cscfg-bestand dat u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d8395-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="d8395-180">Zorg ervoor dat het selectievakje **toch implementeren als een of meer rollen met één exemplaar** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d8395-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="d8395-181">Druk op de knop maatstreepjes in de rechterbenedenhoek om te beginnen met de implementatie.</span><span class="sxs-lookup"><span data-stu-id="d8395-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="d8395-182">Verwacht een paar minuten duren.</span><span class="sxs-lookup"><span data-stu-id="d8395-182">Expect it to take a few minutes to complete.</span></span>

   ![Uploaden][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="d8395-184">Problemen met de implementatie oplossen</span><span class="sxs-lookup"><span data-stu-id="d8395-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="d8395-185">Als uw Webrol niet online komen, is het waarschijnlijk een probleem met de beveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="d8395-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="d8395-186">Controleer of de SSL is geconfigureerd zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="d8395-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="d8395-187">Als uw werkrol mislukt online worden gezet, maar de Webrol is geslaagd, is het zeer waarschijnlijk een probleem opgetreden bij het verbinden met de status-database die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d8395-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="d8395-188">Zorg ervoor dat de verbindingsreeks in uw cscfg-bestand juist is.</span><span class="sxs-lookup"><span data-stu-id="d8395-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="d8395-189">Controleer of de server en database bestaat en of de gebruikers-id en het wachtwoord juist zijn.</span><span class="sxs-lookup"><span data-stu-id="d8395-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="d8395-190">Voor Azure SQL DB moet de verbindingsreeks van het formulier:</span><span class="sxs-lookup"><span data-stu-id="d8395-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="d8395-191">Zorg ervoor dat de naam van de server begint niet met **https://**.</span><span class="sxs-lookup"><span data-stu-id="d8395-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="d8395-192">Zorg ervoor dat uw Azure SQL DB-server kan Azure-Services tot stand te brengen.</span><span class="sxs-lookup"><span data-stu-id="d8395-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="d8395-193">U doet dit door https://manage.windowsazure.com openen, klikt u op 'SQL Databases' aan de linkerkant, klikt u boven 'Servers' en selecteer uw server.</span><span class="sxs-lookup"><span data-stu-id="d8395-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="d8395-194">Klik op **configureren** aan de bovenkant en zorg ervoor dat de **Azure Services** is ingesteld op "Ja".</span><span class="sxs-lookup"><span data-stu-id="d8395-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="d8395-195">(Zie de sectie vereisten aan het begin van dit artikel).</span><span class="sxs-lookup"><span data-stu-id="d8395-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="d8395-196">De service-implementatie testen</span><span class="sxs-lookup"><span data-stu-id="d8395-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="d8395-197">Verbinding maken met een webbrowser</span><span class="sxs-lookup"><span data-stu-id="d8395-197">Connect with a web browser</span></span>
<span data-ttu-id="d8395-198">Bepaal de web-eindpunt van uw service gesplitste samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="d8395-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="d8395-199">U kunt dit vinden in de klassieke Azure Portal door te gaan naar de **Dashboard** van uw cloudservice en zoeken onder **Site-URL** aan de rechterkant.</span><span class="sxs-lookup"><span data-stu-id="d8395-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="d8395-200">Vervang **http://** met **https://** omdat de standaardbeveiligingsinstellingen het HTTP-eindpunt uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="d8395-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="d8395-201">Laad de pagina voor deze URL in uw browser.</span><span class="sxs-lookup"><span data-stu-id="d8395-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="d8395-202">Testen met PowerShell-scripts</span><span class="sxs-lookup"><span data-stu-id="d8395-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="d8395-203">De implementatie en uw omgeving kunnen worden getest door het uitvoeren van de opgenomen voorbeeld PowerShell-scripts.</span><span class="sxs-lookup"><span data-stu-id="d8395-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="d8395-204">De scriptbestanden opgenomen zijn:</span><span class="sxs-lookup"><span data-stu-id="d8395-204">The script files included are:</span></span>

1. <span data-ttu-id="d8395-205">**SetupSampleSplitMergeEnvironment.ps1** -stelt u een test-gegevenslaag voor gesplitste/Merge (Zie onderstaande tabel voor een gedetailleerde beschrijving)</span><span class="sxs-lookup"><span data-stu-id="d8395-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="d8395-206">**ExecuteSampleSplitMerge.ps1** -test-bewerkingen op de test wordt uitgevoerd gegevens servicetier (Zie onderstaande tabel voor een gedetailleerde beschrijving)</span><span class="sxs-lookup"><span data-stu-id="d8395-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="d8395-207">**GetMappings.ps1** - site op het hoogste voorbeeldscript die de huidige status van de shard-toewijzingen wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="d8395-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="d8395-208">**ShardManagement.psm1** -helper-script waarmee de API ShardManagement verpakt</span><span class="sxs-lookup"><span data-stu-id="d8395-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="d8395-209">**SqlDatabaseHelpers.psm1** -helper-script voor het maken en beheren van de SQL-databases</span><span class="sxs-lookup"><span data-stu-id="d8395-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="d8395-210">PowerShell-bestand</span><span class="sxs-lookup"><span data-stu-id="d8395-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="d8395-211">Stappen</span><span class="sxs-lookup"><span data-stu-id="d8395-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="d8395-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="d8395-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="d8395-213">Hiermee maakt u een manager-database van de shard-kaart</span><span class="sxs-lookup"><span data-stu-id="d8395-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="d8395-214">2 shard-databases maakt.</span><span class="sxs-lookup"><span data-stu-id="d8395-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="d8395-215">Maakt een shard-toewijzing voor deze database (verwijdert alle bestaande shard op die databases toegewezen).</span><span class="sxs-lookup"><span data-stu-id="d8395-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="d8395-216">Hiermee maakt u een kleine voorbeeldtabel in zowel de shards en vult de tabel in een van de shards.</span><span class="sxs-lookup"><span data-stu-id="d8395-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="d8395-217">Verklaart de SchemaInfo voor de shard-tabel.</span><span class="sxs-lookup"><span data-stu-id="d8395-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="d8395-218">PowerShell-bestand</span><span class="sxs-lookup"><span data-stu-id="d8395-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="d8395-219">Stappen</span><span class="sxs-lookup"><span data-stu-id="d8395-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="d8395-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="d8395-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="d8395-221">Een split-aanvraag verzendt naar de web-frontend gesplitste Merge-Service, die half gegevens van de eerste shard naar de tweede shard splitst.</span><span class="sxs-lookup"><span data-stu-id="d8395-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="d8395-222">De web-frontend voor de status van de gesplitste worden opgevraagd en wacht totdat de aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d8395-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="d8395-223">Een merge-aanvraag verzendt naar de frontend web gesplitste Merge-Service, die de gegevens van de tweede shard terug naar de eerste shard.</span><span class="sxs-lookup"><span data-stu-id="d8395-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="d8395-224">De web-frontend voor de status van de aanvraag merge worden opgevraagd en wacht totdat de aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d8395-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="d8395-225">PowerShell gebruiken om uw implementatie te controleren</span><span class="sxs-lookup"><span data-stu-id="d8395-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="d8395-226">Open een nieuw PowerShell-venster en Ga naar de map waar u het pakket gesplitste samenvoegen hebt gedownload en navigeer vervolgens naar de map 'powershell'.</span><span class="sxs-lookup"><span data-stu-id="d8395-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="d8395-227">Maak een Azure SQL database-server (of kies een bestaande server) waar de shard-toewijzing manager en shards wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d8395-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="d8395-228">Het script SetupSampleSplitMergeEnvironment.ps1 maakt alle deze databases op dezelfde server standaard aan het script eenvoudig te houden.</span><span class="sxs-lookup"><span data-stu-id="d8395-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="d8395-229">Dit is geen beperking van de gesplitste Merge-Service zelf.</span><span class="sxs-lookup"><span data-stu-id="d8395-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="d8395-230">Een SQL-aanmelding voor verificatie met lees-/ schrijftoegang tot de databases vereist voor de service gesplitste samenvoegen gegevens verplaatsen en het bijwerken van de shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="d8395-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="d8395-231">Aangezien de splitsing Merge-Service wordt uitgevoerd in de cloud, ondersteunt het momenteel geen geïntegreerde verificatie.</span><span class="sxs-lookup"><span data-stu-id="d8395-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="d8395-232">Zorg ervoor dat de Azure SQL-server is geconfigureerd voor toegang van de IP-adres van de machine uitvoeren van deze scripts.</span><span class="sxs-lookup"><span data-stu-id="d8395-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="d8395-233">U vindt deze instelling onder de Azure SQL-server / configuration / IP-adressen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d8395-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="d8395-234">Voer het script SetupSampleSplitMergeEnvironment.ps1 voor het maken van de voorbeeldomgeving.</span><span class="sxs-lookup"><span data-stu-id="d8395-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="d8395-235">Dit script uitvoert wordt wissen uit een bestaande shard management kaartgegevens structuren op de shard kaart manager-database en de shards.</span><span class="sxs-lookup"><span data-stu-id="d8395-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="d8395-236">Kan het zijn handig voor het script opnieuw uitgevoerd als u wilt de shard-kaart of shards opnieuw te initialiseren.</span><span class="sxs-lookup"><span data-stu-id="d8395-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="d8395-237">Voorbeeld-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="d8395-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="d8395-238">Voer het script Getmappings.ps1 om weer te geven van de toewijzingen die momenteel aanwezig zijn in de voorbeeldomgeving.</span><span class="sxs-lookup"><span data-stu-id="d8395-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="d8395-239">Voer het script ExecuteSampleSplitMerge.ps1 voor het uitvoeren van een splitsbewerking (de helft van de gegevens op de eerste shard verplaatst naar de tweede shard) en vervolgens een merge-bewerking (de gegevens terug verplaatsen naar de eerste shard).</span><span class="sxs-lookup"><span data-stu-id="d8395-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="d8395-240">Als u SSL geconfigureerd en links van het http-eindpunt dat is uitgeschakeld, zorg ervoor dat u gebruikt het eindpunt https://.</span><span class="sxs-lookup"><span data-stu-id="d8395-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="d8395-241">Voorbeeld-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="d8395-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="d8395-242">Als u krijgt de onderstaande fout, is het meest waarschijnlijk een probleem met het certificaat van uw Web-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="d8395-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="d8395-243">Probeer verbinding te maken met de webservice-eindpunt met uw favoriete webbrowser en controleer of er een certificaatfout.</span><span class="sxs-lookup"><span data-stu-id="d8395-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="d8395-244">Als deze is voltooid, de uitvoer moet eruitzien als in het onderstaande:</span><span class="sxs-lookup"><span data-stu-id="d8395-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="d8395-245">Experimenteer met andere gegevenstypen!</span><span class="sxs-lookup"><span data-stu-id="d8395-245">Experiment with other data types!</span></span> <span data-ttu-id="d8395-246">Alle deze scripts duren voordat een optionele - ShardKeyType parameter waarmee u het sleuteltype opgeven.</span><span class="sxs-lookup"><span data-stu-id="d8395-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="d8395-247">De standaardwaarde is Int32, maar u kunt ook opgeven Int64, Guid of binair.</span><span class="sxs-lookup"><span data-stu-id="d8395-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="d8395-248">Aanvragen maken</span><span class="sxs-lookup"><span data-stu-id="d8395-248">Create requests</span></span>
<span data-ttu-id="d8395-249">De service kan worden gebruikt met behulp van de webgebruikersinterface of te importeren en gebruiken van de SplitMerge.psm1 PowerShell-module die wordt uw aanvragen via de Webrol indienen.</span><span class="sxs-lookup"><span data-stu-id="d8395-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="d8395-250">De service kan de gegevens in zowel de shard-tabellen en de verwijzingsdimensies verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="d8395-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="d8395-251">Een shard-tabel heeft een sharding-sleutelkolom en andere rijgegevens in elke shard heeft.</span><span class="sxs-lookup"><span data-stu-id="d8395-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="d8395-252">Een tabel is niet shard zodat deze dezelfde rijgegevens in elke shard bevat.</span><span class="sxs-lookup"><span data-stu-id="d8395-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="d8395-253">Verwijzingsdimensies zijn handig voor gegevens die niet vaak wijzigen en join wordt gebruikt met shard tabellen in query's.</span><span class="sxs-lookup"><span data-stu-id="d8395-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="d8395-254">Om een splitsing merge-bewerking uitvoeren, moet u de shard-tabellen en tabellen die u wilt hebt verplaatst declareren.</span><span class="sxs-lookup"><span data-stu-id="d8395-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="d8395-255">Dit wordt bewerkstelligd met de **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="d8395-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="d8395-256">Deze API is in de **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** naamruimte.</span><span class="sxs-lookup"><span data-stu-id="d8395-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="d8395-257">Voor elke shard-tabel maken van een **ShardedTableInfo** object met een beschrijving van de tabel bovenliggende schemanaam (optioneel, wordt standaard ingesteld op 'dbo'), de tabelnaam en de naam van de kolom in de tabel die de sharding-sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="d8395-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="d8395-258">Maak voor elke tabel verwijzing naar een **ReferenceTableInfo** object met een beschrijving van de tabel bovenliggende schemanaam (optioneel, wordt standaard ingesteld op 'dbo') en de naam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="d8395-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="d8395-259">De bovenstaande TableInfo objecten toevoegen aan een nieuwe **SchemaInfo** object.</span><span class="sxs-lookup"><span data-stu-id="d8395-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="d8395-260">Geen verwijzing ophalen naar een **ShardMapManager** object en de aanroep **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="d8395-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="d8395-261">Toevoegen de **SchemaInfo** naar de **SchemaInfoCollection**, geven de naam van de shard-toewijzing.</span><span class="sxs-lookup"><span data-stu-id="d8395-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="d8395-262">Een voorbeeld hiervan kan worden weergegeven in het script SetupSampleSplitMergeEnvironment.ps1.</span><span class="sxs-lookup"><span data-stu-id="d8395-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="d8395-263">De splitsing Merge-service maakt geen de doeldatabase (of het schema voor alle tabellen in de database) voor u.</span><span class="sxs-lookup"><span data-stu-id="d8395-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="d8395-264">Ze moeten zijn vooraf gemaakte voordat een aanvraag verzonden naar de service.</span><span class="sxs-lookup"><span data-stu-id="d8395-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="d8395-265">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="d8395-265">Troubleshooting</span></span>
<span data-ttu-id="d8395-266">Mogelijk ziet u de onderstaande bericht bij het uitvoeren van de powershell-voorbeeldscripts:</span><span class="sxs-lookup"><span data-stu-id="d8395-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="d8395-267">Deze fout betekent dat uw SSL-certificaat is niet juist geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d8395-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="d8395-268">Volg de instructies in de sectie 'Verbinding maken met een webbrowser'.</span><span class="sxs-lookup"><span data-stu-id="d8395-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="d8395-269">Als u geen aanvragen indienen mogelijk ziet u dit:</span><span class="sxs-lookup"><span data-stu-id="d8395-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="d8395-270">In dit geval uw configuratiebestand controleren, met name de instelling voor **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="d8395-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="d8395-271">Deze fout geeft meestal aan dat de werkrol niet met succes metagegevensdatabase bij het eerste gebruik initialiseren kan.</span><span class="sxs-lookup"><span data-stu-id="d8395-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png


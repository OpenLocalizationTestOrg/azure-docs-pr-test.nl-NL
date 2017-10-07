---
title: een gesplitste samenvoegen service aaaDeploy | Microsoft Docs
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
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="fd1a2-103">Een service voor splitsen en samenvoegen implementeren</span><span class="sxs-lookup"><span data-stu-id="fd1a2-103">Deploy a split-merge service</span></span>
<span data-ttu-id="fd1a2-104">Hallo gesplitste samenvoegen hulpprogramma kunt u gegevens verplaatsen tussen shard-databases.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="fd1a2-105">Zie [verplaatsen van gegevens tussen cloud uitgebreide databases](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="fd1a2-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="fd1a2-106">Hallo gesplitste samenvoegen pakketten downloaden</span><span class="sxs-lookup"><span data-stu-id="fd1a2-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="fd1a2-107">Hallo nieuwste NuGet versie downloaden van [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="fd1a2-108">Open een opdrachtprompt en navigeer toohello map waar u nuget.exe hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="fd1a2-109">Hallo download bevat PowerShell commmands.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="fd1a2-110">Hallo nieuwste gesplitste samenvoegen pakket in de huidige map Hallo Hello onder opdracht downloaden:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="fd1a2-111">Hallo-bestanden worden geplaatst in een map met de naam **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** waar *x.x.xxx.x* Hallo versienummer weerspiegelt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="fd1a2-112">Hallo gesplitste samenvoegen Service-bestanden niet vinden in Hallo **content\splitmerge\service** onderliggende map en Hallo gesplitste samenvoegen PowerShell-scripts (en vereiste client-dll's) in Hallo **content\splitmerge\powershell** onderliggende map.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd1a2-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="fd1a2-113">Prerequisites</span></span>
1. <span data-ttu-id="fd1a2-114">Maak een Azure SQL DB-database die wordt gebruikt als Hallo gesplitste samenvoegen status database.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="fd1a2-115">Ga toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="fd1a2-116">Maak een nieuwe **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="fd1a2-117">Hallo-database van een naam geven en maak een nieuwe beheerder en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="fd1a2-118">Worden ervoor toorecord Hallo naam en het wachtwoord voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="fd1a2-119">Zorg ervoor dat de server van uw Azure SQL DB Azure Services tooconnect tooit toestaat.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="fd1a2-120">In Hallo Hallo Portal **firewallinstellingen**, zorg ervoor dat Hallo **tooAzure-Services toegang toestaan** ingesteld te**op**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="fd1a2-121">Klik op Hallo 'opgeslagen'-pictogram.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-121">Click hello "save" icon.</span></span>
   
   ![Toegestane services][1]
3. <span data-ttu-id="fd1a2-123">Maak een Azure Storage-account dat wordt gebruikt voor diagnostische uitvoer.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="fd1a2-124">Ga toohello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="fd1a2-125">Klik in de linkerbalk Hallo op **nieuw**, klikt u op **gegevens en opslag**, klikt u vervolgens **opslag**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="fd1a2-126">Maak een Azure Cloud Service die uw service gesplitste Merge bevat.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="fd1a2-127">Ga toohello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="fd1a2-128">Klik in de linkerbalk Hallo op **nieuw**, vervolgens **Compute**, **Cloudservice**, en **maken**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="fd1a2-129">Configureer uw service gesplitste samenvoegen</span><span class="sxs-lookup"><span data-stu-id="fd1a2-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="fd1a2-130">Configuratie gesplitste Merge-service</span><span class="sxs-lookup"><span data-stu-id="fd1a2-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="fd1a2-131">Hallo map waar u Hallo gesplitste samenvoegen assembly's hebt gedownload, maakt u een kopie van Hallo **ServiceConfiguration.Template.cscfg** -bestand dat naast verzonden **SplitMergeService.cspkg** en wijzig de naam **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="fd1a2-132">Open **ServiceConfiguration.cscfg** in een teksteditor zoals Visual Studio die invoer zoals Hallo-indeling van certificaatvingerafdrukken valideert.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="fd1a2-133">Een nieuwe database maken of kies een bestaande database tooserve als Hallo status database voor gesplitste samenvoegbewerkingen en Hallo verbindingsreeks van de database ophalen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="fd1a2-134">Op dit moment gebruik Hallo status database Hallo Latijnse sortering (SQL\_Latin1\_algemene\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="fd1a2-135">Zie voor meer informatie [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="fd1a2-136">Met Azure SQL DB heeft Hallo verbindingsreeks doorgaans Hallo vorm:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="fd1a2-137">Deze verbindingsreeks invoeren in Hallo cscfg-bestand in beide Hallo **SplitMergeWeb** en **SplitMergeWorker** rol secties in Hallo ElasticScaleMetadata instelling.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="fd1a2-138">Voor Hallo **SplitMergeWorker** rol, voer een geldige verbinding tekenreeks tooAzure opslag voor Hallo **WorkerRoleSynchronizationStorageAccountConnectionString** instelling.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="fd1a2-139">Beveiliging configureren</span><span class="sxs-lookup"><span data-stu-id="fd1a2-139">Configure security</span></span>
<span data-ttu-id="fd1a2-140">Raadpleeg voor gedetailleerde instructies tooconfigure Hallo beveiliging van de service Hallo toohello [gesplitste samenvoegen Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="fd1a2-141">Een minimale set van configuratie stappen worden uitgevoerd voor Hallo toepassing van een eenvoudige test-implementatie voor deze zelfstudie wordt tooget Hallo service up-to-date en worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="fd1a2-142">Deze stappen alleen Hallo één machine/account inschakelen deze toocommunicate met Hallo service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="fd1a2-143">Een zelfondertekend certificaat maken</span><span class="sxs-lookup"><span data-stu-id="fd1a2-143">Create a self-signed certificate</span></span>
<span data-ttu-id="fd1a2-144">Maak een nieuwe map en van deze directory execute Hallo volgende opdracht met behulp van een [opdrachtprompt voor ontwikkelaars voor Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) venster:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="fd1a2-145">U wordt gevraagd een wachtwoord tooprotect Hallo persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="fd1a2-146">Voer een sterk wachtwoord in en Bevestig het.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="fd1a2-147">U wordt gevraagd voor Hallo wachtwoord toobe zodra er meer daarna gebruikt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="fd1a2-148">Klik op **Ja** op Hallo end tooimport het toohello vertrouwde Certification Authorities basisarchief.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="fd1a2-149">Een PFX-bestand maken</span><span class="sxs-lookup"><span data-stu-id="fd1a2-149">Create a PFX file</span></span>
<span data-ttu-id="fd1a2-150">Uitvoeren van de volgende opdracht uit Hallo Hallo hetzelfde venster waar makecert is uitgevoerd. Gebruik Hallo hetzelfde wachtwoord dat u gebruikt toocreate Hallo certificaat:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="fd1a2-151">Hallo-clientcertificaat importeren in het persoonlijke archief Hallo</span><span class="sxs-lookup"><span data-stu-id="fd1a2-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="fd1a2-152">Dubbelklik in Windows Verkenner op **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="fd1a2-153">In Hallo **Wizard Certificaat importeren** Selecteer **huidige gebruiker** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="fd1a2-154">Hallo-bestandspad bevestigen en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="fd1a2-155">Geef het wachtwoord hello, laat de eigenschap **alle uitgebreide eigenschappen bevatten** gecontroleerd en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="fd1a2-156">Laat **certificaatarchief automatisch Selecteer Hallo [...]**  gecontroleerd en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="fd1a2-157">Klik op **voltooien** en **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="fd1a2-158">Toohello cloudservice voor Hallo PFX-bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="fd1a2-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="fd1a2-159">Ga toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fd1a2-160">Selecteer **Cloudservices**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="fd1a2-161">Selecteer Hallo cloudservice die u hierboven hebt gemaakt voor Hallo gesplitste/Merge-service.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="fd1a2-162">Klik op **certificaten** in het bovenste menu Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="fd1a2-163">Klik op **uploaden** in de balk onderaan Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="fd1a2-164">Selecteer Hallo PFX-bestand en Voer Hallo hetzelfde wachtwoord als hierboven.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="fd1a2-165">Als voltooid, kopiëren van de certificaatvingerafdruk Hallo van Hallo nieuw item in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="fd1a2-166">Hallo serviceconfiguratiebestand bijwerken</span><span class="sxs-lookup"><span data-stu-id="fd1a2-166">Update hello service configuration file</span></span>
<span data-ttu-id="fd1a2-167">Vingerafdruk van het certificaat plakken Hallo gekopieerd hierboven in Hallo vingerafdrukwaarde/kenmerk van deze instellingen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="fd1a2-168">Voor de werkrol Hallo:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="fd1a2-169">Voor de Webrol Hallo:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="fd1a2-170">Houd er rekening mee dat voor implementaties in afzonderlijke certificaten moeten worden gebruikt voor de CA, Hallo voor versleuteling, Hallo servercertificaat en clientcertificaten.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="fd1a2-171">Zie voor gedetailleerde instructies voor dit [Beveiligingsconfiguratie](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="fd1a2-172">Uw service implementeren</span><span class="sxs-lookup"><span data-stu-id="fd1a2-172">Deploy your service</span></span>
1. <span data-ttu-id="fd1a2-173">Ga toohello [Azure-portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fd1a2-174">Klik op Hallo **Cloudservices** tabblad aan de linkerkant hello, en selecteer Hallo cloudservice die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="fd1a2-175">Klik op **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="fd1a2-176">Kies Hallo staging-omgeving en klik vervolgens op **uploaden van een nieuwe implementatie van de staging**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Fasering][3]
5. <span data-ttu-id="fd1a2-178">Voer in het dialoogvenster hello, een implementatielabel.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="fd1a2-179">Klik voor 'Pakket' en 'Configuration', 'Van Local' en kies Hallo **SplitMergeService.cspkg** bestands- en uw cscfg-bestand dat u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="fd1a2-180">Zorg ervoor dat Hallo selectievakje **toch implementeren als een of meer rollen met één exemplaar** is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="fd1a2-181">Klik op Hallo maatstreepjes button in Hallo onderkant rechts toobegin Hallo implementatie.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="fd1a2-182">Verwacht tootake toocomplete met een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Uploaden][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="fd1a2-184">Hallo-implementatie oplossen</span><span class="sxs-lookup"><span data-stu-id="fd1a2-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="fd1a2-185">Als uw Webrol toocome online is mislukt, is het waarschijnlijk een probleem met Hallo beveiligingsconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="fd1a2-186">Controleer dat Hallo die SSL is geconfigureerd zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="fd1a2-187">Als uw werkrol toocome online mislukt, maar de Webrol lukt, is het waarschijnlijk een probleem met de verbinding toohello status database die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="fd1a2-188">Zorg ervoor dat de verbindingsreeks Hallo in uw cscfg nauwkeurig is.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="fd1a2-189">Controleer dat Hallo-server en database bestaan en dat het Hallo-gebruikersnaam en wachtwoord correct zijn.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="fd1a2-190">Voor Azure SQL DB moet de verbindingsreeks Hallo Hallo vorm:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="fd1a2-191">Zorg ervoor dat servernaam Hallo begint niet met **https://**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="fd1a2-192">Zorg ervoor dat de server van uw Azure SQL DB Azure Services tooconnect tooit toestaat.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="fd1a2-193">toodo, https://manage.windowsazure.com open, op 'SQL-Databases' Hallo links, klikt u op 'Servers' hello boven, en selecteer uw server.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="fd1a2-194">Klik op **configureren** op Hallo bovenste en ervoor te zorgen dat Hallo **Azure Services** ingesteld te 'Ja'.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="fd1a2-195">(Zie vereisten Hallo sectie Hallo boven aan dit artikel).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="fd1a2-196">Hallo-service-implementatie testen</span><span class="sxs-lookup"><span data-stu-id="fd1a2-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="fd1a2-197">Verbinding maken met een webbrowser</span><span class="sxs-lookup"><span data-stu-id="fd1a2-197">Connect with a web browser</span></span>
<span data-ttu-id="fd1a2-198">Hallo-web-eindpunt van uw service gesplitste samenvoegen bepalen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="fd1a2-199">U kunt dit vinden in Hallo klassieke Azure-Portal door te gaan toohello **Dashboard** van uw cloudservice en zoeken onder **Site-URL** aan de rechterkant Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="fd1a2-200">Vervang **http://** met **https://** omdat standaardbeveiligingsinstellingen Hallo Hallo HTTP-eindpunt uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="fd1a2-201">Hallo-pagina voor deze URL worden geladen in uw browser.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="fd1a2-202">Testen met PowerShell-scripts</span><span class="sxs-lookup"><span data-stu-id="fd1a2-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="fd1a2-203">Hallo-implementatie en uw omgeving kunnen worden getest door het uitvoeren van de voorbeeldscripts PowerShell Hallo opgenomen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="fd1a2-204">Hallo scriptbestanden opgenomen zijn:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-204">hello script files included are:</span></span>

1. <span data-ttu-id="fd1a2-205">**SetupSampleSplitMergeEnvironment.ps1** -stelt u een test-gegevenslaag voor gesplitste/Merge (Zie onderstaande tabel voor een gedetailleerde beschrijving)</span><span class="sxs-lookup"><span data-stu-id="fd1a2-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="fd1a2-206">**ExecuteSampleSplitMerge.ps1** -test-bewerkingen op Hallo test wordt uitgevoerd gegevens servicetier (Zie onderstaande tabel voor een gedetailleerde beschrijving)</span><span class="sxs-lookup"><span data-stu-id="fd1a2-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="fd1a2-207">**GetMappings.ps1** - site op het hoogste voorbeeldscript die de huidige status Hallo van Hallo shard toewijzingen wordt afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="fd1a2-208">**ShardManagement.psm1** -helper-script dat verpakt Hallo ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="fd1a2-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="fd1a2-209">**SqlDatabaseHelpers.psm1** -helper-script voor het maken en beheren van de SQL-databases</span><span class="sxs-lookup"><span data-stu-id="fd1a2-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="fd1a2-210">PowerShell-bestand</span><span class="sxs-lookup"><span data-stu-id="fd1a2-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="fd1a2-211">Stappen</span><span class="sxs-lookup"><span data-stu-id="fd1a2-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="fd1a2-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="fd1a2-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="fd1a2-213">Hiermee maakt u een manager-database van de shard-kaart</span><span class="sxs-lookup"><span data-stu-id="fd1a2-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="fd1a2-214">2 shard-databases maakt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="fd1a2-215">Maakt een shard-toewijzing voor deze database (verwijdert alle bestaande shard op die databases toegewezen).</span><span class="sxs-lookup"><span data-stu-id="fd1a2-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="fd1a2-216">Maakt een kleine voorbeeldtabel in beide Hallo shards en vult Hallo-tabel in een Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="fd1a2-217">Verklaart Hallo SchemaInfo voor Hallo shard-tabel.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="fd1a2-218">PowerShell-bestand</span><span class="sxs-lookup"><span data-stu-id="fd1a2-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="fd1a2-219">Stappen</span><span class="sxs-lookup"><span data-stu-id="fd1a2-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="fd1a2-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="fd1a2-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="fd1a2-221">Een gesplitste aanvraag toohello gesplitste samenvoegen Service web front, die half Hallo gegevens van Hallo eerste shard toohello tweede shard splitst verzendt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="fd1a2-222">Polls Hallo web frontend voor Hallo gesplitste aanvraagstatus en wacht totdat het Hallo-aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="fd1a2-223">Verzendt een merge aanvraag toohello gesplitste samenvoegen Service web front, die Hallo gegevens vanuit het Hallo tweede shard back toohello eerste shard verplaatst.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="fd1a2-224">Polls Hallo web frontend voor Hallo samenvoegen aanvraagstatus en wordt er gewacht totdat het Hallo-aanvraag is voltooid.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="fd1a2-225">Gebruik PowerShell tooverify uw implementatie</span><span class="sxs-lookup"><span data-stu-id="fd1a2-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="fd1a2-226">Open een nieuw PowerShell-venster en navigeer toohello map waar u Hallo gesplitste samenvoegen pakket hebt gedownload en navigeer vervolgens naar Hallo 'powershell' directory.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="fd1a2-227">Maak een Azure SQL database-server (of kies een bestaande server) waar Hallo shard-toewijzing manager en shards wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fd1a2-228">Hallo SetupSampleSplitMergeEnvironment.ps1 script maakt alle deze databases op Hallo dezelfde server door tookeep Hallo Standaardscript eenvoudig.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="fd1a2-229">Dit is geen beperking Hallo gesplitste samenvoegen Service zelf.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="fd1a2-230">Een SQL-verificatie-aanmelding met lezen/schrijven toegang toohello die databases voor Hallo gesplitste Merge-servicegegevens toomove en updatetoewijzing hello shard vereist.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="fd1a2-231">Aangezien Hallo gesplitste Merge-Service wordt uitgevoerd in de cloud Hallo, ondersteunt het momenteel geen geïntegreerde verificatie.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="fd1a2-232">Controleer of hello Azure SQL-server is geconfigureerd tooallow toegang van Hallo IP-adres van deze scripts Hallo machine.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="fd1a2-233">U vindt deze instelling onder hello Azure SQL-server / configuration / IP-adressen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="fd1a2-234">Hallo SetupSampleSplitMergeEnvironment.ps1 script toocreate Hallo Voorbeeldomgeving uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="fd1a2-235">Dit script uitvoert wordt wissen uit een bestaande shard management kaartgegevens structuren op Hallo shard kaart manager-database en Hallo shards.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="fd1a2-236">Het wellicht handig toorerun Hallo script desgewenst toore initialiseren Hallo shard-kaart of shards.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="fd1a2-237">Voorbeeld-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="fd1a2-238">Hallo Getmappings.ps1 tooview Hallo scripttoewijzingen die momenteel aanwezig zijn in Hallo Voorbeeldomgeving uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="fd1a2-239">Hallo ExecuteSampleSplitMerge.ps1 script tooexecute een splitsbewerking (half Hallo gegevens verplaatst naar een Hallo eerste shard toohello tweede shard) en vervolgens een merge-bewerking (Hallo gegevens terug verplaatsen naar de eerste shard Hallo) worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="fd1a2-240">Als u SSL- en http-eindpunt links Hallo uitgeschakeld hebt geconfigureerd, zorg er dan Hallo https:// eindpunt te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="fd1a2-241">Voorbeeld-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="fd1a2-242">Als u Hallo hieronder fout ontvangt, is het zeer waarschijnlijk een probleem met het certificaat van uw Web-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="fd1a2-243">Probeer verbinding te maken toohello Web-eindpunt met uw favoriete webbrowser en controleer of er een certificaatfout.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="fd1a2-244">Als deze is voltooid, worden Hallo uitvoer moet eruitzien als Hallo hieronder:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="fd1a2-245">Experimenteer met andere gegevenstypen!</span><span class="sxs-lookup"><span data-stu-id="fd1a2-245">Experiment with other data types!</span></span> <span data-ttu-id="fd1a2-246">Alle deze scripts duren een optionele - ShardKeyType parameter waarmee u toospecify Hallo sleuteltype.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="fd1a2-247">Hallo standaard Int32 is, maar u kunt ook opgeven Int64, Guid of binair.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="fd1a2-248">Aanvragen maken</span><span class="sxs-lookup"><span data-stu-id="fd1a2-248">Create requests</span></span>
<span data-ttu-id="fd1a2-249">Hallo-service kan worden gebruikt via het Hallo-webgebruikersinterface of te importeren en gebruiken van Hallo SplitMerge.psm1 PowerShell-module die wordt uw aanvragen via Hallo Webrol indienen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="fd1a2-250">Hallo-service kunt gegevens in zowel de shard-tabellen en de verwijzingsdimensies verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="fd1a2-251">Een shard-tabel heeft een sharding-sleutelkolom en andere rijgegevens in elke shard heeft.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="fd1a2-252">Een verwijzing naar de tabel is niet shard zodat deze Hallo bevat dezelfde gegevens op elke shard rij.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="fd1a2-253">Verwijzingsdimensies zijn handig voor gegevens die niet vaak wijzigen en gebruikte tooJOIN met shard tabellen in query's.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="fd1a2-254">In de volgorde tooperform samenvoegbewerking voor gesplitste, moet u Hallo shard-tabellen en tabellen die u wilt dat toohave verplaatst declareren.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="fd1a2-255">Dit wordt bewerkstelligd met Hallo **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="fd1a2-256">Deze API is in Hallo **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** naamruimte.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="fd1a2-257">Voor elke shard-tabel maken een **ShardedTableInfo** object met een beschrijving van de tabel Hallo bovenliggende schemanaam (optioneel, standaard te 'dbo'), Hallo tabelnaam en Hallo kolomnaam in de tabel die de Hallo sharding sleutel bevat.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="fd1a2-258">Maak voor elke tabel verwijzing naar een **ReferenceTableInfo** object met een beschrijving van de tabel Hallo bovenliggende schemanaam (optioneel, standaardinstellingen te 'dbo') en de tabelnaam Hallo.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="fd1a2-259">Hallo hierboven TableInfo objecten tooa nieuwe toevoegen **SchemaInfo** object.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="fd1a2-260">Ophalen van een verwijzing tooa **ShardMapManager** object en de aanroep **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="fd1a2-261">Hallo toevoegen **SchemaInfo** toohello **SchemaInfoCollection**, bieden Hallo shard toewijzingsnaam.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="fd1a2-262">Een voorbeeld hiervan in Hallo SetupSampleSplitMergeEnvironment.ps1 script weergegeven.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="fd1a2-263">Hallo gesplitste samenvoegen service maakt geen doeldatabase hello (of een schema voor alle tabellen in Hallo database) voor u.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="fd1a2-264">Ze moeten zijn vooraf gemaakte voordat een aanvraag toohello-service worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fd1a2-265">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="fd1a2-265">Troubleshooting</span></span>
<span data-ttu-id="fd1a2-266">Bij het uitvoeren van powershell-Hallo voorbeeldscripts weergegeven Hallo onder bericht:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="fd1a2-267">Deze fout betekent dat uw SSL-certificaat is niet juist geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="fd1a2-268">Volg de instructies Hallo in sectie 'Verbinding maken met een webbrowser'.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="fd1a2-269">Als u geen aanvragen indienen mogelijk ziet u dit:</span><span class="sxs-lookup"><span data-stu-id="fd1a2-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="fd1a2-270">In dit geval, Controleer uw configuratiebestand in de instelling voor bepaalde Hallo **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="fd1a2-271">Deze fout geeft meestal aan dat werkrol Hallo kan metagegevensdatabase Hallo bij het eerste gebruik is niet initialiseren.</span><span class="sxs-lookup"><span data-stu-id="fd1a2-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png


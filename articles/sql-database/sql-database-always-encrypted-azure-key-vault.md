---
title: 'Altijd versleuteld: SQL Database - Azure Sleutelkluis | Microsoft Docs'
description: Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met gegevens met behulp van versleuteling Hallo altijd versleuteld Wizard in SQL Server Management Studio. Bevat ook instructies die wordt uitgelegd hoe u toostore elke versleutelingssleutel in Azure Sleutelkluis.
keywords: versleuteling van gegevens, de versleutelingssleutel, cloud-versleuteling
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="81b8d-105">Altijd versleuteld: Beveiligen van gevoelige gegevens in SQL-Database en de versleutelingssleutels in Azure Sleutelkluis</span><span class="sxs-lookup"><span data-stu-id="81b8d-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="81b8d-106">Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met versleuteling van gegevens met behulp van Hallo [Wizard altijd versleuteld](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="81b8d-107">Bevat ook instructies die wordt uitgelegd hoe u toostore elke versleutelingssleutel in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="81b8d-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="81b8d-108">Altijd versleutelde is een technologie voor versleuteling van nieuwe gegevens in Azure SQL Database en SQL-Server waarmee beveiligen van gevoelige gegevens in rust op Hallo-server tijdens het verkeer tussen client en server, en wanneer deze hello worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81b8d-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="81b8d-109">Altijd versleutelde zorgt ervoor dat gevoelige gegevens nooit wordt weergegeven als tekst zonder opmaak binnen Hallo database-systeem.</span><span class="sxs-lookup"><span data-stu-id="81b8d-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="81b8d-110">Nadat u gegevensversleuteling configureert, alleen clienttoepassingen of appservers met toohello toegangstoetsen hebben toegang tot gecodeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="81b8d-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="81b8d-111">Zie voor gedetailleerde informatie [altijd versleuteld (Database-Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="81b8d-112">Nadat u Hallo database toouse altijd versleuteld configureert, maakt u een clienttoepassing in C# met Visual Studio toowork met Hallo versleutelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="81b8d-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="81b8d-113">Hallo stappen in dit artikel en meer informatie over hoe tooset up altijd versleuteld voor een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="81b8d-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="81b8d-114">In dit artikel leert u hoe tooperform Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="81b8d-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="81b8d-115">Hallo altijd versleuteld wizard gebruiken in SSMS toocreate [sleutels altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="81b8d-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="81b8d-116">Maak een [kolomhoofdsleutel (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="81b8d-117">Maak een [kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="81b8d-118">Een databasetabel maken en kolommen te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="81b8d-119">Maak een toepassing die wordt ingevoegd, selecteert en gegevens uit Hallo versleutelde kolommen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="81b8d-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81b8d-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="81b8d-120">Prerequisites</span></span>
<span data-ttu-id="81b8d-121">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="81b8d-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="81b8d-122">Een Azure-account en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="81b8d-122">An Azure account and subscription.</span></span> <span data-ttu-id="81b8d-123">Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="81b8d-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="81b8d-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versie 13.0.700.242 of hoger.</span><span class="sxs-lookup"><span data-stu-id="81b8d-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="81b8d-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) of hoger (op Hallo van client-computer).</span><span class="sxs-lookup"><span data-stu-id="81b8d-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="81b8d-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="81b8d-127">[Azure PowerShell](/powershell/azure/overview), versie 1.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="81b8d-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="81b8d-128">Type **(Get-Module azure - ListAvailable). Versie** toosee welke versie van PowerShell uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81b8d-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="81b8d-129">Uw client-toepassing tooaccess Hallo SQL Database-service inschakelen</span><span class="sxs-lookup"><span data-stu-id="81b8d-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="81b8d-130">U moet uw client toepassing tooaccess Hallo SQL Database-service inschakelen door het instellen van de vereiste verificatie Hallo en verkrijgen Hallo *ClientId* en *geheim* moet u tooauthenticate uw toepassing in de volgende code Hallo.</span><span class="sxs-lookup"><span data-stu-id="81b8d-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="81b8d-131">Open Hallo [klassieke Azure-portal](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="81b8d-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="81b8d-132">Selecteer **Active Directory** en klik op Hallo Active Directory-exemplaar dat uw toepassing wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="81b8d-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="81b8d-133">Klik op **toepassingen**, en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="81b8d-134">Typ een naam voor uw toepassing (bijvoorbeeld: *myClientApp*), selecteer **WEBTOEPASSING**, en klik op Hallo pijl toocontinue.</span><span class="sxs-lookup"><span data-stu-id="81b8d-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="81b8d-135">Voor Hallo **AANMELDINGS-URL** en **APP ID URI** kunt u een geldige URL invoeren (bijvoorbeeld *http://myClientApp*) en door te gaan.</span><span class="sxs-lookup"><span data-stu-id="81b8d-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="81b8d-136">Klik op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="81b8d-137">Kopieer uw **CLIENT-ID**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="81b8d-138">(U moet deze waarde in uw code later.)</span><span class="sxs-lookup"><span data-stu-id="81b8d-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="81b8d-139">In Hallo **sleutels** sectie **1 jaar** van Hallo **Selecteer duur** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="81b8d-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="81b8d-140">(Kopieert u de sleutel Hallo nadat u hebt opgeslagen in stap 13.)</span><span class="sxs-lookup"><span data-stu-id="81b8d-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="81b8d-141">Schuif naar beneden en klik op **toepassing toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="81b8d-142">Laat **weergeven** instellen te**Microsoft-Apps** en selecteer **Microsoft Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="81b8d-143">Klik op Hallo vinkje toocontinue.</span><span class="sxs-lookup"><span data-stu-id="81b8d-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="81b8d-144">Selecteer **Azure Service Management openen...**  van Hallo **gedelegeerde machtigingen** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="81b8d-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="81b8d-145">Klik op **OPSLAAN**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="81b8d-146">Na het Hallo opslaan is voltooid, Hallo sleutelwaarde in Hallo kopiëren **sleutels** sectie.</span><span class="sxs-lookup"><span data-stu-id="81b8d-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="81b8d-147">(U moet deze waarde in uw code later.)</span><span class="sxs-lookup"><span data-stu-id="81b8d-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="81b8d-148">Een sleutelkluis toostore uw sleutels maken</span><span class="sxs-lookup"><span data-stu-id="81b8d-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="81b8d-149">Nu dat uw client-app is geconfigureerd en u hebt uw client-ID, is tijd toocreate een sleutelkluis en de toegangsbeleid configureren zodat u en uw toepassing toegang krijgen tot Hallo-kluis geheimen (Hallo altijd versleuteld sleutels).</span><span class="sxs-lookup"><span data-stu-id="81b8d-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="81b8d-150">Hallo *maken*, *ophalen*, *lijst*, *aanmelding*, *controleren*, *wrapKey*, en *unwrapKey* machtigingen zijn vereist voor het maken van een nieuwe hoofdsleutel voor kolom- en voor het instellen van versleuteling met SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="81b8d-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="81b8d-151">U kunt snel een sleutelkluis maken door het uitvoeren van script volgen Hallo.</span><span class="sxs-lookup"><span data-stu-id="81b8d-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="81b8d-152">Zie voor een gedetailleerde uitleg van deze cmdlets en meer informatie over het maken en configureren van een sleutelkluis [aan de slag met Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="81b8d-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="81b8d-153">Een lege SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="81b8d-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="81b8d-154">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="81b8d-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="81b8d-155">Ga te**nieuw** > **gegevens en opslag** > **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="81b8d-156">Maak een **leeg** database met de naam **kliniek** op een nieuwe of bestaande server.</span><span class="sxs-lookup"><span data-stu-id="81b8d-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="81b8d-157">Voor gedetailleerde instructies over hoe toocreate een database in Azure-portal Hallo zien [uw eerste Azure SQL database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="81b8d-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Een lege database maken](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="81b8d-159">U moet Hallo verbindingsreeks later in de zelfstudie hello, dus u Hallo database maakt, en blader vervolgens toohello nieuwe kliniek database en kopieer Hallo verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="81b8d-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="81b8d-160">U kunt Hallo-verbindingsreeks ophalen op elk gewenst moment, maar het is gemakkelijk toocopy in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="81b8d-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="81b8d-161">Ga te**SQL-databases** > **kliniek** > **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="81b8d-162">Kopieer de verbindingsreeks Hallo voor **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="81b8d-164">Verbinding maken met toohello database met SSMS</span><span class="sxs-lookup"><span data-stu-id="81b8d-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="81b8d-165">Open SSMS en toohello server verbinden met Hallo kliniek database.</span><span class="sxs-lookup"><span data-stu-id="81b8d-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="81b8d-166">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="81b8d-166">Open SSMS.</span></span> <span data-ttu-id="81b8d-167">(Ga te**Connect** > **Database-Engine** tooopen hello **tooServer verbinding** venster als deze niet geopend is.)</span><span class="sxs-lookup"><span data-stu-id="81b8d-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="81b8d-168">Voer uw servernaam en referenties.</span><span class="sxs-lookup"><span data-stu-id="81b8d-168">Enter your server name and credentials.</span></span> <span data-ttu-id="81b8d-169">Hallo-servernaam kan worden gevonden op de blade Hallo SQL-database en in de verbindingsreeks Hallo u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="81b8d-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="81b8d-170">Type Hallo volledige servernaam, met inbegrip van *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="81b8d-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="81b8d-172">Als hello **nieuwe firewallregel** venster wordt geopend Meld u aan tooAzure en laat SSMS een nieuwe firewallregel voor u.</span><span class="sxs-lookup"><span data-stu-id="81b8d-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="81b8d-173">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="81b8d-173">Create a table</span></span>
<span data-ttu-id="81b8d-174">In deze sectie maakt u een tabel toohold patiënt gegevens.</span><span class="sxs-lookup"><span data-stu-id="81b8d-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="81b8d-175">Het is niet in eerste instantie versleuteld--kunt u versleuteling wilt configureren in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="81b8d-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="81b8d-176">Vouw **Databases**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="81b8d-177">Klik met de rechtermuisknop Hallo **kliniek** database en klik op **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="81b8d-178">Plakken Hallo Transact-SQL (T-SQL) te volgen in de nieuwe queryvenster Hallo en **Execute** deze.</span><span class="sxs-lookup"><span data-stu-id="81b8d-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="81b8d-179">Versleutelen van de kolommen (Configureer altijd versleuteld)</span><span class="sxs-lookup"><span data-stu-id="81b8d-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="81b8d-180">SSMS biedt een wizard waarmee u eenvoudig configureren altijd versleuteld door stellen Hallo kolomhoofdsleutel kolomversleutelingssleutel en versleutelde kolommen voor u.</span><span class="sxs-lookup"><span data-stu-id="81b8d-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="81b8d-181">Vouw **Databases** > **kliniek** > **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="81b8d-182">Klik met de rechtermuisknop Hallo **patiënten** tabel en selecteer **versleutelen kolommen** tooopen Hallo altijd versleuteld wizard:</span><span class="sxs-lookup"><span data-stu-id="81b8d-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Kolommen versleutelen](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="81b8d-184">Hallo altijd versleuteld wizard omvat Hallo uit te voeren: **kolomselectie**, **hoofdsleutel configuratie**, **validatie**, en **samenvatting** .</span><span class="sxs-lookup"><span data-stu-id="81b8d-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="81b8d-185">Kolom selecteren</span><span class="sxs-lookup"><span data-stu-id="81b8d-185">Column Selection</span></span>
<span data-ttu-id="81b8d-186">Klik op **volgende** op Hallo **inleiding** pagina tooopen hello **kolomselectie** pagina.</span><span class="sxs-lookup"><span data-stu-id="81b8d-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="81b8d-187">Op deze pagina wordt u selecteren welke kolommen u wilt dat tooencrypt, [Hallo type versleuteling, en welke kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="81b8d-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="81b8d-188">Versleutelen **SSN** en **geboortedatum** informatie voor elke geduld.</span><span class="sxs-lookup"><span data-stu-id="81b8d-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="81b8d-189">Hallo SSN kolom gebruikt deterministische versleuteling, die ondersteuning biedt voor gelijkheid zoekacties, samenvoegingen en gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="81b8d-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="81b8d-190">Hallo geboortedatum kolom gebruikt willekeurige versleuteling, die geen ondersteuning biedt voor bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="81b8d-191">Set Hallo **versleutelingstype** voor Hallo SSN kolom te**Deterministic** en kolom Geboortedatum te Hallo**Randomized**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="81b8d-192">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-192">Click **Next**.</span></span>

![Kolommen versleutelen](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="81b8d-194">Configuratie van de hoofdsleutel</span><span class="sxs-lookup"><span data-stu-id="81b8d-194">Master Key Configuration</span></span>
<span data-ttu-id="81b8d-195">Hallo **hoofdsleutel configuratie** pagina is waar u uw CMK en instellen Selecteer Hallo sleutelopslagplaatsprovider waar hello CMK worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="81b8d-196">Op dit moment kunt u een CMK opslaan in het certificaatarchief van de Windows hello Azure Key Vault of een hardware security module (HSM).</span><span class="sxs-lookup"><span data-stu-id="81b8d-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="81b8d-197">Deze zelfstudie laat zien hoe toostore uw sleutels in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="81b8d-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="81b8d-198">Selecteer **Azure Sleutelkluis**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="81b8d-199">Selecteer de gewenste sleutelkluis Hallo uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="81b8d-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="81b8d-200">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-200">Click **Next**.</span></span>

![Configuratie van de hoofdsleutel](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="81b8d-202">Validatie</span><span class="sxs-lookup"><span data-stu-id="81b8d-202">Validation</span></span>
<span data-ttu-id="81b8d-203">U kunt nu Hallo kolommen versleutelen of een PowerShell-script toorun later opslaan.</span><span class="sxs-lookup"><span data-stu-id="81b8d-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="81b8d-204">Selecteer voor deze zelfstudie **toofinish nu doorgaan** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="81b8d-205">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="81b8d-205">Summary</span></span>
<span data-ttu-id="81b8d-206">Controleer of Hallo-instellingen juist zijn en klik op **voltooien** toocomplete Hallo setup voor altijd versleuteld.</span><span class="sxs-lookup"><span data-stu-id="81b8d-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Samenvatting](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="81b8d-208">Hallo wizardacties controleren</span><span class="sxs-lookup"><span data-stu-id="81b8d-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="81b8d-209">Nadat het Hallo-wizard is voltooid, wordt uw database instellen voor altijd versleuteld.</span><span class="sxs-lookup"><span data-stu-id="81b8d-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="81b8d-210">Hallo wizard uitgevoerd Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="81b8d-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="81b8d-211">Een hoofdsleutel van kolom gemaakt en opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="81b8d-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="81b8d-212">Een kolomversleutelingssleutel gemaakt en opgeslagen in Azure Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="81b8d-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="81b8d-213">Geconfigureerde Hallo geselecteerde kolommen voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="81b8d-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="81b8d-214">Hallo patiënten tabel momenteel geen gegevens bevat, maar alle bestaande gegevens in de kolommen geselecteerd Hallo nu versleuteld.</span><span class="sxs-lookup"><span data-stu-id="81b8d-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="81b8d-215">U kunt maken van sleutels in SSMS Hallo Hallo controleren door het uitbreiden van **kliniek** > **beveiliging** > **sleutels altijd versleuteld**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="81b8d-216">Maken van een clienttoepassing die met Hallo versleutelde gegevens werkt</span><span class="sxs-lookup"><span data-stu-id="81b8d-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="81b8d-217">Nu dat altijd versleuteld is ingesteld, kunt u een toepassing die wordt uitgevoerd *voegt* en *selecteert* op Hallo versleutelde kolommen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="81b8d-218">Uw toepassing moet gebruiken [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objecten als tekst zonder opmaak gegevens toohello server met kolommen altijd versleuteld wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="81b8d-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="81b8d-219">Letterlijke waarden doorgeven zonder SqlParameter objecten leidt tot een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="81b8d-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="81b8d-220">Open Visual Studio en maak een nieuwe C# **consoletoepassing** (Visual Studio 2015 en eerder) of **Console-App (.NET Framework)** (Visual Studio 2017 en hoger).</span><span class="sxs-lookup"><span data-stu-id="81b8d-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="81b8d-221">Zorg ervoor dat uw project te is ingesteld**.NET Framework 4.6** of hoger.</span><span class="sxs-lookup"><span data-stu-id="81b8d-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="81b8d-222">Naam Hallo project **AlwaysEncryptedConsoleAKVApp** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="81b8d-223">Hallo NuGet-pakketten te volgen door te gaan te installeren**extra** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="81b8d-224">Deze twee regels code worden uitgevoerd in Hallo Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="81b8d-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="81b8d-225">Uw verbinding tekenreeks tooenable altijd versleuteld wijzigen</span><span class="sxs-lookup"><span data-stu-id="81b8d-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="81b8d-226">Deze sectie wordt uitgelegd hoe tooenable altijd versleuteld in de verbindingsreeks voor de database.</span><span class="sxs-lookup"><span data-stu-id="81b8d-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="81b8d-227">tooenable altijd versleuteld, moet u tooadd hello **Kolomversleutelingsinstelling** sleutelwoord tooyour connection string en stel deze in te**ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="81b8d-228">U kunt dit rechtstreeks in de verbindingsreeks Hallo instellen of kunt u dit instellen met behulp van [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="81b8d-229">volgende sectie toont hoe de voorbeeldtoepassing Hallo in Hallo toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="81b8d-230">Altijd versleuteld inschakelen in de verbindingsreeks Hallo</span><span class="sxs-lookup"><span data-stu-id="81b8d-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="81b8d-231">Hallo na sleutelwoord tooyour verbindingsreeks toevoegen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="81b8d-232">Altijd versleuteld met SqlConnectionStringBuilder inschakelen</span><span class="sxs-lookup"><span data-stu-id="81b8d-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="81b8d-233">Hallo van de volgende code wordt getoond hoe tooenable altijd versleuteld door in te stellen [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) te[ingeschakeld](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="81b8d-234">Hello Azure Key Vault provider registreren</span><span class="sxs-lookup"><span data-stu-id="81b8d-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="81b8d-235">Hallo volgende code toont hoe tooregister hello Azure Sleutelkluis-provider met Hallo ADO.NET-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="81b8d-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="81b8d-236">Altijd versleutelde console voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="81b8d-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="81b8d-237">Dit voorbeeld laat zien hoe:</span><span class="sxs-lookup"><span data-stu-id="81b8d-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="81b8d-238">Wijzig uw verbinding tekenreeks tooenable altijd versleuteld.</span><span class="sxs-lookup"><span data-stu-id="81b8d-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="81b8d-239">Azure Key Vault registreren als Hallo sleutelopslagplaatsprovider van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="81b8d-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="81b8d-240">Gegevens invoegen in Hallo versleutelde kolommen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="81b8d-241">Een record met een filter voor een specifieke waarde in een versleutelde kolom selecteren.</span><span class="sxs-lookup"><span data-stu-id="81b8d-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="81b8d-242">Vervang de inhoud Hallo van **Program.cs** Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="81b8d-243">Vervang de verbindingsreeks Hallo voor Hallo globale connectionString variabele in Hallo regel dat direct vóór Hallo Main-methode met uw geldige verbindingsreeks uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="81b8d-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="81b8d-244">Dit is de enige wijziging Hallo u toomake toothis code nodig.</span><span class="sxs-lookup"><span data-stu-id="81b8d-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="81b8d-245">Hallo app toosee altijd versleuteld in actie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81b8d-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="81b8d-246">Controleer of dat Hallo gegevens worden versleuteld</span><span class="sxs-lookup"><span data-stu-id="81b8d-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="81b8d-247">U kunt snel controleren dat actuele gegevens op de server Hallo Hallo worden gecodeerd door een query Hallo patiënten met SSMS (met behulp van de huidige verbinding waarbij **Kolomversleutelingsinstelling** nog niet is ingeschakeld).</span><span class="sxs-lookup"><span data-stu-id="81b8d-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="81b8d-248">Hallo volgende query uit op Hallo kliniek database worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81b8d-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="81b8d-249">U kunt zien Hallo versleutelde kolommen bevatten geen gecodeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="81b8d-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="81b8d-251">toouse SSMS tooaccess Hallo gecodeerde gegevens, kunt u Hallo toevoegen *Kolomversleutelingsinstelling = ingeschakeld* parameter toohello verbinding.</span><span class="sxs-lookup"><span data-stu-id="81b8d-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="81b8d-252">SSMS, met de rechtermuisknop op uw server in **Objectverkenner** en kies **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="81b8d-253">Klik op **Connect** > **Database-Engine** tooopen hello **verbinding tooServer** venster en klik op **opties**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="81b8d-254">Klik op **extra verbindingsparameters** en het type **Kolomversleutelingsinstelling = ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="81b8d-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="81b8d-256">Hallo volgende query uit op Hallo kliniek database worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="81b8d-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="81b8d-257">U ziet nu Hallo gecodeerde gegevens in Hallo versleutelde kolommen.</span><span class="sxs-lookup"><span data-stu-id="81b8d-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="81b8d-259">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="81b8d-259">Next steps</span></span>
<span data-ttu-id="81b8d-260">Nadat u een database die gebruikmaakt van altijd versleuteld maakt, kunt u toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="81b8d-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="81b8d-261">[Draaien en opschonen van uw sleutels](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="81b8d-262">[Migreren van gegevens die al is versleuteld met altijd versleuteld](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="81b8d-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="81b8d-263">Gerelateerde informatie</span><span class="sxs-lookup"><span data-stu-id="81b8d-263">Related information</span></span>
* [<span data-ttu-id="81b8d-264">Altijd versleuteld (ontwikkeling client)</span><span class="sxs-lookup"><span data-stu-id="81b8d-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="81b8d-265">Transparante gegevensversleuteling</span><span class="sxs-lookup"><span data-stu-id="81b8d-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="81b8d-266">SQL Server-versleuteling</span><span class="sxs-lookup"><span data-stu-id="81b8d-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="81b8d-267">Altijd versleutelde wizard</span><span class="sxs-lookup"><span data-stu-id="81b8d-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="81b8d-268">Altijd versleutelde blog</span><span class="sxs-lookup"><span data-stu-id="81b8d-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)


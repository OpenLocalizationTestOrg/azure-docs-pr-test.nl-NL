---
title: 'Altijd versleuteld: Azure SQL Database - Windows-certificaatarchief | Microsoft Docs'
description: Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met versleuteling van de database met behulp van Hallo altijd versleuteld Wizard in SQL Server Management Studio (SSMS). Ook ziet u hoe toostore de versleutelingssleutels in het certificaat van de Windows hello opslaan.
keywords: versleutelen van gegevens, sql-versleuteling, versleuteling van de database, gevoelige gegevens altijd versleuteld.
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: ce7e052e-8bf6-4d7c-9204-4c6f4afeba4b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: sstein
ms.openlocfilehash: 483f9a2120cc42b732142fc07807d3d8830a0c33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-hello-windows-certificate-store"></a><span data-ttu-id="1ce52-105">Altijd versleuteld: Beveiligen van gevoelige gegevens in SQL-Database en de versleutelingssleutels in het certificaatarchief van de Windows hello</span><span class="sxs-lookup"><span data-stu-id="1ce52-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in hello Windows certificate store</span></span>

<span data-ttu-id="1ce52-106">Dit artikel laat zien hoe toosecure gevoelige gegevens in een SQL-database met versleuteling van de database met behulp van Hallo [Wizard altijd versleuteld](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-106">This article shows you how toosecure sensitive data in a SQL database with database encryption by using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="1ce52-107">Ook ziet u hoe toostore de versleutelingssleutels in het certificaat van de Windows hello opslaan.</span><span class="sxs-lookup"><span data-stu-id="1ce52-107">It also shows you how toostore your encryption keys in hello Windows certificate store.</span></span>

<span data-ttu-id="1ce52-108">Versleutelde is altijd een nieuwe technologie voor het versleuteling van gegevens in Azure SQL Database en SQL-Server die helpt beveiligen van gevoelige gegevens in rust op Hallo-server tijdens het verkeer tussen client en server en tijdens het Hallo-gegevens wordt gebruikt, nooit ervoor te zorgen dat gevoelige gegevens weergegeven als de platte tekst binnen Hallo database-systeem.</span><span class="sxs-lookup"><span data-stu-id="1ce52-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use, ensuring that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="1ce52-109">Nadat u gegevens worden versleuteld, alleen clienttoepassingen of appservers met toohello toegangstoetsen hebben toegang tot gecodeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="1ce52-109">After you encrypt data, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="1ce52-110">Zie voor gedetailleerde informatie [altijd versleuteld (Database-Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-110">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="1ce52-111">Na het configureren van Hallo database toouse altijd versleuteld, maakt u een clienttoepassing in C# met Visual Studio toowork met Hallo versleutelde gegevens.</span><span class="sxs-lookup"><span data-stu-id="1ce52-111">After configuring hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="1ce52-112">Stappen Hallo in dit artikel toolearn hoe tooset up altijd versleuteld voor een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="1ce52-112">Follow hello steps in this article toolearn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="1ce52-113">In dit artikel leert u hoe tooperform Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="1ce52-113">In this article, you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="1ce52-114">Hallo altijd versleuteld wizard gebruiken in SSMS toocreate [sleutels altijd versleuteld](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="1ce52-114">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted Keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="1ce52-115">Maak een [hoofdsleutel van kolom (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-115">Create a [Column Master Key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="1ce52-116">Maak een [Kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-116">Create a [Column Encryption Key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="1ce52-117">Een databasetabel maken en kolommen te versleutelen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-117">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="1ce52-118">Maak een toepassing die wordt ingevoegd, selecteert en gegevens uit Hallo versleutelde kolommen worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1ce52-118">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ce52-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1ce52-119">Prerequisites</span></span>
<span data-ttu-id="1ce52-120">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="1ce52-120">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="1ce52-121">Een Azure-account en -abonnement.</span><span class="sxs-lookup"><span data-stu-id="1ce52-121">An Azure account and subscription.</span></span> <span data-ttu-id="1ce52-122">Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1ce52-122">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1ce52-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) versie 13.0.700.242 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1ce52-123">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="1ce52-124">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) of hoger (op Hallo van client-computer).</span><span class="sxs-lookup"><span data-stu-id="1ce52-124">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="1ce52-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-125">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>

## <a name="create-a-blank-sql-database"></a><span data-ttu-id="1ce52-126">Een lege SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="1ce52-126">Create a blank SQL database</span></span>
1. <span data-ttu-id="1ce52-127">Meld u aan toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1ce52-127">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="1ce52-128">Klik op **nieuwe** > **gegevens en opslag** > **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-128">Click **New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="1ce52-129">Maak een **leeg** database met de naam **kliniek** op een nieuwe of bestaande server.</span><span class="sxs-lookup"><span data-stu-id="1ce52-129">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="1ce52-130">Zie voor gedetailleerde instructies over het maken van een database in Azure-portal Hallo [uw eerste Azure SQL database](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1ce52-130">For detailed instructions about creating a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Een lege database maken](./media/sql-database-always-encrypted/create-database.png)

<span data-ttu-id="1ce52-132">Hallo-verbindingsreeks moet u later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ce52-132">You will need hello connection string later in hello tutorial.</span></span> <span data-ttu-id="1ce52-133">Nadat het Hallo-database is gemaakt, gaat u toohello nieuwe kliniek database en kopieer Hallo verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="1ce52-133">After hello database is created, go toohello new Clinic database and copy hello connection string.</span></span> <span data-ttu-id="1ce52-134">U kunt Hallo-verbindingsreeks ophalen op elk gewenst moment, maar het is gemakkelijk toocopy wanneer u zich in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1ce52-134">You can get hello connection string at any time, but it's easy toocopy it when you're in hello Azure portal.</span></span>

1. <span data-ttu-id="1ce52-135">Klik op **SQL-databases** > **kliniek** > **databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-135">Click **SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="1ce52-136">Kopieer de verbindingsreeks Hallo voor **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-136">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="1ce52-138">Verbinding maken met toohello database met SSMS</span><span class="sxs-lookup"><span data-stu-id="1ce52-138">Connect toohello database with SSMS</span></span>
<span data-ttu-id="1ce52-139">Open SSMS en toohello server verbinden met Hallo kliniek database.</span><span class="sxs-lookup"><span data-stu-id="1ce52-139">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="1ce52-140">Open SSMS.</span><span class="sxs-lookup"><span data-stu-id="1ce52-140">Open SSMS.</span></span> <span data-ttu-id="1ce52-141">(Klik op **Connect** > **Database-Engine** tooopen hello **tooServer verbinding** venster als dit niet geopend is).</span><span class="sxs-lookup"><span data-stu-id="1ce52-141">(Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it is not open).</span></span>
2. <span data-ttu-id="1ce52-142">Voer uw servernaam en referenties.</span><span class="sxs-lookup"><span data-stu-id="1ce52-142">Enter your server name and credentials.</span></span> <span data-ttu-id="1ce52-143">Hallo-servernaam kan worden gevonden op de blade Hallo SQL-database en in de verbindingsreeks Hallo u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="1ce52-143">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="1ce52-144">Type Hallo volledige server naam waaronder *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="1ce52-144">Type hello complete server name including *database.windows.net*.</span></span>
   
    ![Kopieer de verbindingsreeks Hallo](./media/sql-database-always-encrypted/ssms-connect.png)

<span data-ttu-id="1ce52-146">Als hello **nieuwe firewallregel** venster wordt geopend Meld u aan tooAzure en laat SSMS een nieuwe firewallregel voor u.</span><span class="sxs-lookup"><span data-stu-id="1ce52-146">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1ce52-147">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="1ce52-147">Create a table</span></span>
<span data-ttu-id="1ce52-148">In deze sectie maakt u een tabel toohold patiënt gegevens.</span><span class="sxs-lookup"><span data-stu-id="1ce52-148">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="1ce52-149">Dit is een normale tabel in eerste instantie--u versleuteling in de volgende sectie hello wilt configureren.</span><span class="sxs-lookup"><span data-stu-id="1ce52-149">This will be a normal table initially--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="1ce52-150">Vouw **Databases**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-150">Expand **Databases**.</span></span>
2. <span data-ttu-id="1ce52-151">Klik met de rechtermuisknop Hallo **kliniek** database en klik op **nieuwe Query**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-151">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="1ce52-152">Plakken Hallo Transact-SQL (T-SQL) te volgen in de nieuwe queryvenster Hallo en **Execute** deze.</span><span class="sxs-lookup"><span data-stu-id="1ce52-152">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

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


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="1ce52-153">Versleutelen van de kolommen (Configureer altijd versleuteld)</span><span class="sxs-lookup"><span data-stu-id="1ce52-153">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="1ce52-154">SSMS biedt een wizard tooeasily configureren altijd versleuteld door stellen Hallo CMK CEK en versleutelde kolommen voor u.</span><span class="sxs-lookup"><span data-stu-id="1ce52-154">SSMS provides a wizard tooeasily configure Always Encrypted by setting up hello CMK, CEK, and encrypted columns for you.</span></span>

1. <span data-ttu-id="1ce52-155">Vouw **Databases** > **kliniek** > **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-155">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="1ce52-156">Klik met de rechtermuisknop Hallo **patiënten** tabel en selecteer **versleutelen kolommen** tooopen Hallo altijd versleuteld wizard:</span><span class="sxs-lookup"><span data-stu-id="1ce52-156">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Kolommen versleutelen](./media/sql-database-always-encrypted/encrypt-columns.png)

<span data-ttu-id="1ce52-158">Hallo altijd versleuteld wizard omvat Hallo uit te voeren: **kolomselectie**, **hoofdsleutel configuratie** (CMK) **validatie**, en  **Samenvatting**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-158">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration** (CMK), **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="1ce52-159">Kolom selecteren</span><span class="sxs-lookup"><span data-stu-id="1ce52-159">Column Selection</span></span>
<span data-ttu-id="1ce52-160">Klik op **volgende** op Hallo **inleiding** pagina tooopen hello **kolomselectie** pagina.</span><span class="sxs-lookup"><span data-stu-id="1ce52-160">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="1ce52-161">Op deze pagina wordt u selecteren welke kolommen u wilt dat tooencrypt, [Hallo type versleuteling, en welke kolomversleutelingssleutel (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="1ce52-161">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="1ce52-162">Versleutelen **SSN** en **geboortedatum** informatie voor elke geduld.</span><span class="sxs-lookup"><span data-stu-id="1ce52-162">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="1ce52-163">Hallo **SSN** kolom deterministische versleuteling, die ondersteuning biedt voor gelijkheid zoekacties, samenvoegingen en gegroepeerd wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1ce52-163">hello **SSN** column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="1ce52-164">Hallo **geboortedatum** kolom willekeurige versleuteling, die geen ondersteuning biedt voor bewerkingen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1ce52-164">hello **BirthDate** column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="1ce52-165">Set Hallo **versleutelingstype** voor Hallo **SSN** kolom te**Deterministic** en Hallo **geboortedatum** kolom te **Ingedeeld**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-165">Set hello **Encryption Type** for hello **SSN** column too**Deterministic** and hello **BirthDate** column too**Randomized**.</span></span> <span data-ttu-id="1ce52-166">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-166">Click **Next**.</span></span>

![Kolommen versleutelen](./media/sql-database-always-encrypted/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="1ce52-168">Configuratie van de hoofdsleutel</span><span class="sxs-lookup"><span data-stu-id="1ce52-168">Master Key Configuration</span></span>
<span data-ttu-id="1ce52-169">Hallo **hoofdsleutel configuratie** pagina is waar u uw CMK en instellen Selecteer Hallo sleutelopslagplaatsprovider waar hello CMK worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-169">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="1ce52-170">Op dit moment kunt u een CMK opslaan in het certificaatarchief van de Windows hello Azure Key Vault of een hardware security module (HSM).</span><span class="sxs-lookup"><span data-stu-id="1ce52-170">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span> <span data-ttu-id="1ce52-171">Deze zelfstudie laat zien hoe toostore uw sleutels in het certificaat van de Windows hello opslaan.</span><span class="sxs-lookup"><span data-stu-id="1ce52-171">This tutorial shows how toostore your keys in hello Windows certificate store.</span></span>

<span data-ttu-id="1ce52-172">Controleer **Windows-certificaatarchief** is geselecteerd en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-172">Verify that **Windows certificate store** is selected and click **Next**.</span></span>

![Configuratie van de hoofdsleutel](./media/sql-database-always-encrypted/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="1ce52-174">Validatie</span><span class="sxs-lookup"><span data-stu-id="1ce52-174">Validation</span></span>
<span data-ttu-id="1ce52-175">U kunt nu Hallo kolommen versleutelen of een PowerShell-script toorun later opslaan.</span><span class="sxs-lookup"><span data-stu-id="1ce52-175">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="1ce52-176">Selecteer voor deze zelfstudie **toofinish nu doorgaan** en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-176">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="1ce52-177">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="1ce52-177">Summary</span></span>
<span data-ttu-id="1ce52-178">Controleer of Hallo-instellingen juist zijn en klik op **voltooien** toocomplete Hallo setup voor altijd versleuteld.</span><span class="sxs-lookup"><span data-stu-id="1ce52-178">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Samenvatting](./media/sql-database-always-encrypted/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="1ce52-180">Hallo wizardacties controleren</span><span class="sxs-lookup"><span data-stu-id="1ce52-180">Verify hello wizard's actions</span></span>
<span data-ttu-id="1ce52-181">Nadat het Hallo-wizard is voltooid, wordt uw database instellen voor altijd versleuteld.</span><span class="sxs-lookup"><span data-stu-id="1ce52-181">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="1ce52-182">Hallo wizard uitgevoerd Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="1ce52-182">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="1ce52-183">Een CMK gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ce52-183">Created a CMK.</span></span>
* <span data-ttu-id="1ce52-184">Een CEK gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1ce52-184">Created a CEK.</span></span>
* <span data-ttu-id="1ce52-185">Geconfigureerde Hallo geselecteerde kolommen voor versleuteling.</span><span class="sxs-lookup"><span data-stu-id="1ce52-185">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="1ce52-186">Uw **patiënten** tabel momenteel geen gegevens bevat, maar alle bestaande gegevens in de kolommen geselecteerd Hallo nu versleuteld.</span><span class="sxs-lookup"><span data-stu-id="1ce52-186">Your **Patients** table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="1ce52-187">U kunt maken van sleutels in SSMS Hallo Hallo controleren door te gaan**kliniek** > **beveiliging** > **sleutels altijd versleuteld**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-187">You can verify hello creation of hello keys in SSMS by going too**Clinic** > **Security** > **Always Encrypted Keys**.</span></span> <span data-ttu-id="1ce52-188">U ziet nu Hallo nieuwe sleutels die Hallo wizard voor u gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="1ce52-188">You can now see hello new keys that hello wizard generated for you.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="1ce52-189">Maken van een clienttoepassing die met Hallo versleutelde gegevens werkt</span><span class="sxs-lookup"><span data-stu-id="1ce52-189">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="1ce52-190">Nu dat altijd versleuteld is ingesteld, kunt u een toepassing die wordt uitgevoerd *voegt* en *selecteert* op Hallo versleutelde kolommen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-190">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span> <span data-ttu-id="1ce52-191">toosuccessfully hello voorbeeldtoepassing uitvoeren, moet u het uitvoeren op Hallo dezelfde computer waarop u Hallo altijd versleuteld wizard uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ce52-191">toosuccessfully run hello sample application, you must run it on hello same computer where you ran hello Always Encrypted wizard.</span></span> <span data-ttu-id="1ce52-192">toorun hello toepassing op een andere computer, moet u uw altijd versleuteld certificaten toohello computer met Hallo client-app implementeren.</span><span class="sxs-lookup"><span data-stu-id="1ce52-192">toorun hello application on another computer, you must deploy your Always Encrypted certificates toohello computer running hello client app.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1ce52-193">Uw toepassing moet gebruiken [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objecten als tekst zonder opmaak gegevens toohello server met kolommen altijd versleuteld wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="1ce52-193">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="1ce52-194">Letterlijke waarden doorgeven zonder SqlParameter objecten leidt tot een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="1ce52-194">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="1ce52-195">Open Visual Studio en maak een nieuwe C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="1ce52-195">Open Visual Studio and create a new C# console application.</span></span> <span data-ttu-id="1ce52-196">Zorg ervoor dat uw project te is ingesteld**.NET Framework 4.6** of hoger.</span><span class="sxs-lookup"><span data-stu-id="1ce52-196">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="1ce52-197">Naam Hallo project **AlwaysEncryptedConsoleApp** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-197">Name hello project **AlwaysEncryptedConsoleApp** and click **OK**.</span></span>

![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/console-app.png)

## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="1ce52-199">Uw verbinding tekenreeks tooenable altijd versleuteld wijzigen</span><span class="sxs-lookup"><span data-stu-id="1ce52-199">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="1ce52-200">Deze sectie wordt uitgelegd hoe tooenable altijd versleuteld in de verbindingsreeks voor de database.</span><span class="sxs-lookup"><span data-stu-id="1ce52-200">This section explains how tooenable Always Encrypted in your database connection string.</span></span> <span data-ttu-id="1ce52-201">Wijzigt u Hallo-consoletoepassing die u zojuist hebt gemaakt in de volgende sectie hello, "Altijd versleuteld console voorbeeldtoepassing."</span><span class="sxs-lookup"><span data-stu-id="1ce52-201">You will modify hello console app you just created in hello next section, "Always Encrypted sample console application."</span></span>

<span data-ttu-id="1ce52-202">tooenable altijd versleuteld, moet u tooadd hello **Kolomversleutelingsinstelling** sleutelwoord tooyour connection string en stel deze in te**ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-202">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="1ce52-203">U kunt dit rechtstreeks in de verbindingsreeks Hallo instellen of kunt u dit instellen met behulp van een [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-203">You can set this directly in hello connection string, or you can set it by using a [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="1ce52-204">volgende sectie toont hoe de voorbeeldtoepassing Hallo in Hallo toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-204">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

> [!NOTE]
> <span data-ttu-id="1ce52-205">Dit is de enige wijziging Hallo vereist in een toepassing specifieke tooAlways versleutelde van client.</span><span class="sxs-lookup"><span data-stu-id="1ce52-205">This is hello only change required in a client application specific tooAlways Encrypted.</span></span> <span data-ttu-id="1ce52-206">Als u een bestaande toepassing die wordt de verbindingsreeks extern opgeslagen (dat wil zeggen, in een configuratiebestand), bent u mogelijk kunnen tooenable altijd versleuteld zonder een code te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-206">If you have an existing application that stores its connection string externally (that is, in a config file), you might be able tooenable Always Encrypted without changing any code.</span></span>
> 
> 

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="1ce52-207">Altijd versleuteld inschakelen in de verbindingsreeks Hallo</span><span class="sxs-lookup"><span data-stu-id="1ce52-207">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="1ce52-208">Hallo sleutelwoord tooyour verbindingsreeks volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1ce52-208">Add hello following keyword tooyour connection string:</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-a-sqlconnectionstringbuilder"></a><span data-ttu-id="1ce52-209">Altijd versleuteld met een SqlConnectionStringBuilder inschakelen</span><span class="sxs-lookup"><span data-stu-id="1ce52-209">Enable Always Encrypted with a SqlConnectionStringBuilder</span></span>
<span data-ttu-id="1ce52-210">Hallo volgende code toont hoe tooenable altijd versleuteld door in te stellen Hallo [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) te[ingeschakeld](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-210">hello following code shows how tooenable Always Encrypted by setting hello [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="1ce52-211">Altijd versleutelde console voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="1ce52-211">Always Encrypted sample console application</span></span>
<span data-ttu-id="1ce52-212">Dit voorbeeld laat zien hoe:</span><span class="sxs-lookup"><span data-stu-id="1ce52-212">This sample demonstrates how to:</span></span>

* <span data-ttu-id="1ce52-213">Wijzig uw verbinding tekenreeks tooenable altijd versleuteld.</span><span class="sxs-lookup"><span data-stu-id="1ce52-213">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="1ce52-214">Gegevens invoegen in Hallo versleutelde kolommen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-214">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="1ce52-215">Een record met een filter voor een specifieke waarde in een versleutelde kolom selecteren.</span><span class="sxs-lookup"><span data-stu-id="1ce52-215">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="1ce52-216">Vervang de inhoud Hallo van **Program.cs** Hello code te volgen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-216">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="1ce52-217">Hallo-verbindingsreeks voor Hallo globale connectionString variabele in Hallo regel rechtstreeks boven Hallo Main-methode vervangen door uw geldige verbindingsreeks uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="1ce52-217">Replace hello connection string for hello global connectionString variable in hello line directly above hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="1ce52-218">Dit is de enige wijziging Hallo u toomake toothis code nodig.</span><span class="sxs-lookup"><span data-stu-id="1ce52-218">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="1ce52-219">Hallo app toosee altijd versleuteld in actie uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ce52-219">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;

    namespace AlwaysEncryptedConsoleApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"Replace with your connection string";

        static void Main(string[] args)
        {
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

            InsertPatient(new Patient() {
                SSN = "999-99-0001", FirstName = "Orlando", LastName = "Gee", BirthDate = DateTime.Parse("01/04/1964") });
            InsertPatient(new Patient() {
                SSN = "999-99-0002", FirstName = "Keith", LastName = "Harris", BirthDate = DateTime.Parse("06/20/1977") });
            InsertPatient(new Patient() {
                SSN = "999-99-0003", FirstName = "Donna", LastName = "Carreras", BirthDate = DateTime.Parse("02/09/1973") });
            InsertPatient(new Patient() {
                SSN = "999-99-0004", FirstName = "Janet", LastName = "Gates", BirthDate = DateTime.Parse("08/31/1985") });
            InsertPatient(new Patient() {
                SSN = "999-99-0005", FirstName = "Lucy", LastName = "Harrington", BirthDate = DateTime.Parse("05/06/1993") });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now let's locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 123-45-6789):");
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


## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="1ce52-220">Controleer of dat Hallo gegevens worden versleuteld</span><span class="sxs-lookup"><span data-stu-id="1ce52-220">Verify that hello data is encrypted</span></span>
<span data-ttu-id="1ce52-221">Kunt u snel controleren dat actuele gegevens op de server Hallo Hallo worden versleuteld door het uitvoeren van query's Hallo **patiënten** gegevens met SSMS.</span><span class="sxs-lookup"><span data-stu-id="1ce52-221">You can quickly check that hello actual data on hello server is encrypted by querying hello **Patients** data with SSMS.</span></span> <span data-ttu-id="1ce52-222">(Gebruik de huidige verbinding waarbij Hallo kolomversleutelingsinstelling nog niet is ingeschakeld.)</span><span class="sxs-lookup"><span data-stu-id="1ce52-222">(Use your current connection where hello column encryption setting is not yet enabled.)</span></span>

<span data-ttu-id="1ce52-223">Hallo volgende query uit op Hallo kliniek database worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ce52-223">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="1ce52-224">U kunt zien Hallo versleutelde kolommen bevatten geen gecodeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="1ce52-224">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/ssms-encrypted.png)

<span data-ttu-id="1ce52-226">toouse SSMS tooaccess Hallo gecodeerde gegevens, kunt u Hallo toevoegen **Kolomversleutelingsinstelling = ingeschakeld** parameter toohello verbinding.</span><span class="sxs-lookup"><span data-stu-id="1ce52-226">toouse SSMS tooaccess hello plaintext data, you can add hello **Column Encryption Setting=enabled** parameter toohello connection.</span></span>

1. <span data-ttu-id="1ce52-227">SSMS, met de rechtermuisknop op uw server in **Objectverkenner**, en klik vervolgens op **Disconnect**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-227">In SSMS, right-click your server in **Object Explorer**, and then click **Disconnect**.</span></span>
2. <span data-ttu-id="1ce52-228">Klik op **Connect** > **Database-Engine** tooopen hello **verbinding tooServer** venster en klik vervolgens op **opties**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-228">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window, and then click **Options**.</span></span>
3. <span data-ttu-id="1ce52-229">Klik op **extra verbindingsparameters** en het type **Kolomversleutelingsinstelling = ingeschakeld**.</span><span class="sxs-lookup"><span data-stu-id="1ce52-229">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/ssms-connection-parameter.png)
4. <span data-ttu-id="1ce52-231">Voer hello volgende query op Hallo **kliniek** database.</span><span class="sxs-lookup"><span data-stu-id="1ce52-231">Run hello following query on hello **Clinic** database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="1ce52-232">U ziet nu Hallo gecodeerde gegevens in Hallo versleutelde kolommen.</span><span class="sxs-lookup"><span data-stu-id="1ce52-232">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nieuwe consoletoepassing](./media/sql-database-always-encrypted/ssms-plaintext.png)



> [!NOTE]
> <span data-ttu-id="1ce52-234">Als u verbinding met SSMS (of een client) vanaf een andere computer maakt, hebben geen toegang tot toohello versleutelingssleutels en worden niet kunnen toodecrypt Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="1ce52-234">If you connect with SSMS (or any client) from a different computer, it will not have access toohello encryption keys and will not be able toodecrypt hello data.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="1ce52-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ce52-235">Next steps</span></span>
<span data-ttu-id="1ce52-236">Nadat u een database die gebruikmaakt van altijd versleuteld maakt, kunt u toodo Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="1ce52-236">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="1ce52-237">Dit voorbeeld uitvoert vanaf een andere computer.</span><span class="sxs-lookup"><span data-stu-id="1ce52-237">Run this sample from a different computer.</span></span> <span data-ttu-id="1ce52-238">Deze hebben geen toegang toohello versleutelingssleutels, zodat deze geen toegang tot toohello gecodeerde gegevens en kan niet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1ce52-238">It won't have access toohello encryption keys, so it will not have access toohello plaintext data and will not run successfully.</span></span>
* <span data-ttu-id="1ce52-239">[Draaien en opschonen van uw sleutels](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-239">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="1ce52-240">[Migreren van gegevens die al is versleuteld met altijd versleuteld](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="1ce52-240">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>
* <span data-ttu-id="1ce52-241">[Certificaten tooother clientcomputers altijd versleuteld implementeren](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (Zie de sectie voor Hallo 'Voor het maken van certificaten beschikbaar tooApplications en gebruikers').</span><span class="sxs-lookup"><span data-stu-id="1ce52-241">[Deploy Always Encrypted certificates tooother client machines](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_1) (see hello "Making Certificates Available tooApplications and Users" section).</span></span>

## <a name="related-information"></a><span data-ttu-id="1ce52-242">Gerelateerde informatie</span><span class="sxs-lookup"><span data-stu-id="1ce52-242">Related information</span></span>
* [<span data-ttu-id="1ce52-243">Altijd versleuteld (ontwikkeling client)</span><span class="sxs-lookup"><span data-stu-id="1ce52-243">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="1ce52-244">Transparante gegevensversleuteling</span><span class="sxs-lookup"><span data-stu-id="1ce52-244">Transparent Data Encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="1ce52-245">SQL Server-versleuteling</span><span class="sxs-lookup"><span data-stu-id="1ce52-245">SQL Server Encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="1ce52-246">Altijd versleutelde Wizard</span><span class="sxs-lookup"><span data-stu-id="1ce52-246">Always Encrypted Wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="1ce52-247">Altijd versleutelde Blog</span><span class="sxs-lookup"><span data-stu-id="1ce52-247">Always Encrypted Blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)


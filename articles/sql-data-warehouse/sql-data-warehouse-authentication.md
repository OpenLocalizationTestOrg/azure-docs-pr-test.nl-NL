---
title: aaaAuthentication tooAzure SQL Data Warehouse | Microsoft Docs
description: Azure Active Directory (AAD) en SQL Server-verificatie tooAzure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="1fdf5-103">Verificatie tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1fdf5-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1fdf5-104">Overzicht van beveiliging</span><span class="sxs-lookup"><span data-stu-id="1fdf5-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="1fdf5-105">Verificatie</span><span class="sxs-lookup"><span data-stu-id="1fdf5-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="1fdf5-106">Versleuteling (Portal)</span><span class="sxs-lookup"><span data-stu-id="1fdf5-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="1fdf5-107">Versleuteling (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="1fdf5-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="1fdf5-108">tooconnect tooSQL Data Warehouse, u moet doorgeven beveiligingsreferenties voor verificatiedoeleinden.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="1fdf5-109">Bij het maken van een verbinding, worden bepaalde verbindingsinstellingen geconfigureerd als onderdeel van uw query-sessie tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="1fdf5-110">Voor meer informatie over beveiliging en hoe tooenable verbindingen tooyour datawarehouse Zie [beveiligen van een database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1fdf5-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="1fdf5-111">SQL-verificatie</span><span class="sxs-lookup"><span data-stu-id="1fdf5-111">SQL authentication</span></span>
<span data-ttu-id="1fdf5-112">tooconnect tooSQL Data Warehouse, moet u Hallo volgende informatie opgeven:</span><span class="sxs-lookup"><span data-stu-id="1fdf5-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="1fdf5-113">Volledig gekwalificeerde servernaam</span><span class="sxs-lookup"><span data-stu-id="1fdf5-113">Fully qualified servername</span></span>
* <span data-ttu-id="1fdf5-114">Geef de SQL-verificatie</span><span class="sxs-lookup"><span data-stu-id="1fdf5-114">Specify SQL authentication</span></span>
* <span data-ttu-id="1fdf5-115">Gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="1fdf5-115">Username</span></span>
* <span data-ttu-id="1fdf5-116">Wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1fdf5-116">Password</span></span>
* <span data-ttu-id="1fdf5-117">Standaard-database (optioneel)</span><span class="sxs-lookup"><span data-stu-id="1fdf5-117">Default database (optional)</span></span>

<span data-ttu-id="1fdf5-118">Standaard uw verbinding toohello *master* database en niet de gebruikersdatabase.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="1fdf5-119">tooconnect tooyour gebruikersdatabase, kunt u toodo twee dingen:</span><span class="sxs-lookup"><span data-stu-id="1fdf5-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="1fdf5-120">Geef de standaarddatabase Hallo bij het registreren van uw server met SQL Server-Objectverkenner in SSDT, SSMS, of in de verbindingsreeks voor de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="1fdf5-121">Zo bevatten Hallo InitialCatalog, is de parameter voor een ODBC-verbinding.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="1fdf5-122">Markeer de gebruikersdatabase Hallo voordat het maken van een sessie in SSDT.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="1fdf5-123">Hallo Transact-SQL-instructie **gebruik MijnDatabase;** wordt niet ondersteund voor het Hallo-database voor een verbinding te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="1fdf5-124">Zie voor instructies over het verbinden van tooSQL Data Warehouse met SSDT toohello [Query met Visual Studio] [ Query with Visual Studio] artikel.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="1fdf5-125">Verificatie met Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="1fdf5-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="1fdf5-126">[Azure Active Directory] [ What is Azure Active Directory] verificatie is een mechanisme voor verbinding te maken met tooMicrosoft Azure SQL Data Warehouse met behulp van identiteiten in Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="1fdf5-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="1fdf5-127">Azure Active Directory-verificatie, kunt u Hallo identiteiten van databasegebruikers en andere Microsoft-services op één centrale locatie centraal beheren.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="1fdf5-128">Centrale ID-beheer biedt één plaats toomanage SQL Data Warehouse-gebruikers en vereenvoudigt het beheer van machtigingen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="1fdf5-129">Voordelen</span><span class="sxs-lookup"><span data-stu-id="1fdf5-129">Benefits</span></span>
<span data-ttu-id="1fdf5-130">Azure Active Directory-voordelen zijn:</span><span class="sxs-lookup"><span data-stu-id="1fdf5-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="1fdf5-131">Biedt een alternatieve tooSQL Server-verificatie.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="1fdf5-132">Helpt bij het stoppen Hallo verspreiding van gebruikersidentiteiten voor databaseservers.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="1fdf5-133">Hiermee kunt wachtwoord draaien op één plaats</span><span class="sxs-lookup"><span data-stu-id="1fdf5-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="1fdf5-134">Databasemachtigingen met behulp van externe (AAD)-groepen beheren.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="1fdf5-135">Elimineert wachtwoorden moet opslaan door het inschakelen van geïntegreerde Windows-verificatie en andere soorten authenticatie wordt ondersteund door Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="1fdf5-136">Maakt gebruik van database gebruikers tooauthenticate identiteiten op Hallo databaseniveau bevat.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="1fdf5-137">Biedt ondersteuning voor verificatie op basis van tokens voor toepassingen die verbinding maken met tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="1fdf5-138">Ondersteunt multi-factor authentication via universele verificatie van Active Directory voor SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="1fdf5-139">Zie voor een beschrijving van multi-factor Authentication [SSMS ondersteuning voor Azure AD MFA met SQL-Database en SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1fdf5-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="1fdf5-140">Azure Active Directory is nog relatief nieuw en bevat enkele beperkingen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="1fdf5-141">tooensure Azure Active Directory is geschikt voor uw omgeving, Zie [Azure AD-functies en beperkingen][Azure AD features and limitations], specifiek Hallo aanvullende overwegingen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="1fdf5-142">Configuratiestappen</span><span class="sxs-lookup"><span data-stu-id="1fdf5-142">Configuration steps</span></span>
<span data-ttu-id="1fdf5-143">Volg deze stappen tooconfigure Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="1fdf5-144">U maakt en vult u een Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1fdf5-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="1fdf5-145">Optioneel: Koppelen of Hallo active directory die is gekoppeld aan uw Azure-abonnement wijzigen</span><span class="sxs-lookup"><span data-stu-id="1fdf5-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="1fdf5-146">Een Azure Active Directory-beheerder voor Azure SQL Data Warehouse maken.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="1fdf5-147">De clientcomputers configureren</span><span class="sxs-lookup"><span data-stu-id="1fdf5-147">Configure your client computers</span></span>
5. <span data-ttu-id="1fdf5-148">Ingesloten databasegebruikers in uw database toegewezen tooAzure AD identiteiten maken</span><span class="sxs-lookup"><span data-stu-id="1fdf5-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="1fdf5-149">Verbinding maken met DataWarehouse tooyour met behulp van Azure AD-identiteiten</span><span class="sxs-lookup"><span data-stu-id="1fdf5-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="1fdf5-150">Azure Active Directory-gebruikers worden momenteel niet weergegeven in de Objectverkenner SSDT.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="1fdf5-151">Als tijdelijke oplossing weergeven Hallo gebruikers in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fdf5-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="1fdf5-152">Hallo-informatie</span><span class="sxs-lookup"><span data-stu-id="1fdf5-152">Find hello details</span></span>
* <span data-ttu-id="1fdf5-153">Hallo stappen tooconfigure en gebruik Azure Active Directory-verificatie zijn bijna identiek zijn voor Azure SQL Database en Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1fdf5-154">Ga als volgt Hallo gedetailleerde stappen in Hallo onderwerp [verbinding maakt met tooSQL Database of SQL Data Warehouse door met behulp van Azure Active Directory-verificatie](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="1fdf5-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="1fdf5-155">Aangepaste databaserollen maken en toevoegen van gebruikers toohello rollen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="1fdf5-156">Verleen gedetailleerde machtigingen toohello rollen.</span><span class="sxs-lookup"><span data-stu-id="1fdf5-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="1fdf5-157">Zie voor meer informatie [aan de slag met machtigingen voor Database-Engine](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="1fdf5-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fdf5-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1fdf5-158">Next steps</span></span>
<span data-ttu-id="1fdf5-159">toostart opvragen van uw datawarehouse met Visual Studio en andere toepassingen, Zie [Query met Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="1fdf5-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations

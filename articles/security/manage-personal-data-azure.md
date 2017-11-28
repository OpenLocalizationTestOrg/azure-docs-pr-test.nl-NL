---
title: aaaManage persoonlijke gegevens in Microsoft Azure | Microsoft Docs
description: hulp bij hoe toocorrect, bijwerken, verwijderen en exporteren van persoonlijke gegevens in Azure Active Directory en Azure SQL Database
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: barclayn
ms.openlocfilehash: 032f70d32377cb9395cb2c35c27dad05001537c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="098b8-103">Persoonlijke gegevens beheren in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="098b8-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="098b8-104">In dit artikel biedt richtlijnen voor hoe toocorrect, bijwerken, verwijderen en exporteren van persoonlijke gegevens in Azure Active Directory en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="098b8-104">This article provides guidance on how toocorrect, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="098b8-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="098b8-105">Scenario</span></span>

<span data-ttu-id="098b8-106">Een bedrijf Dublin gebaseerde biedt hoge einde bestemming bruiloften in Ierland en Hallo wereld voor zowel een lokale en internationale klant base one-stop winkelen.</span><span class="sxs-lookup"><span data-stu-id="098b8-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around hello world for both a local and international customer base.</span></span> <span data-ttu-id="098b8-107">Ze hebben kantoren, klanten, werknemers en leveranciers rond hello world toofully service Hallo plaatsen die ze bieden.</span><span class="sxs-lookup"><span data-stu-id="098b8-107">They have offices, customers, employees, and vendors located around hello world toofully service hello venues they offer.</span></span>

<span data-ttu-id="098b8-108">Tussen veel andere items Hallo bedrijf houdt van geen r.s.v.p. 's die voedselallergieën en via de voeding voorkeuren bevatten.</span><span class="sxs-lookup"><span data-stu-id="098b8-108">Among many other items, hello company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="098b8-109">Bruiloft gasten kunnen worden geregistreerd voor verschillende activiteiten zoals horseback fiets, surfen, is aangewezen ritjes, enz., en zelfs communiceren met elkaar op een centrale webpagina tijdens Hallo maanden voorafgaand toohello gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="098b8-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during hello months leading up toohello event.</span></span> <span data-ttu-id="098b8-110">Hallo bedrijf verzamelt persoonlijke gegevens van werknemers, leveranciers, klanten en bruiloft gasten.</span><span class="sxs-lookup"><span data-stu-id="098b8-110">hello company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="098b8-111">Vanwege Hallo moet internationale aard van de onderneming Hallo Hallo voldoen aan meerdere niveaus van de regelgeving.</span><span class="sxs-lookup"><span data-stu-id="098b8-111">Because of hello international nature of hello business hello company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="098b8-112">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="098b8-112">Problem statement</span></span>

- <span data-ttu-id="098b8-113">Beheerders van gegevens moet kunnen toocorrect onnauwkeurig persoonlijke informatie en update onvolledig of veranderende persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="098b8-113">Data admins must be able toocorrect inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="098b8-114">Gegevens beheerders nodig moet kunnen toodelete persoonlijke gegevens op verzoek Hallo van een onderwerp gegevens.</span><span class="sxs-lookup"><span data-stu-id="098b8-114">Data admins need must be able toodelete personal information upon hello request of a data subject.</span></span>

- <span data-ttu-id="098b8-115">Gegevens admins tooexport gegevens nodig en geef deze tooa gegevens onderwerp in een algemene, gestructureerde indeling op zijn of haar verzoek.</span><span class="sxs-lookup"><span data-stu-id="098b8-115">Data admins need tooexport data and provide it tooa data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="098b8-116">Bedrijfsdoelstellingen</span><span class="sxs-lookup"><span data-stu-id="098b8-116">Company goals</span></span>

- <span data-ttu-id="098b8-117">Onjuiste of onvolledige klant, bruiloft Gast werknemer en persoonlijke gegevens van de leverancier moeten worden gecorrigeerd of bijgewerkt in Azure Active Directory en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="098b8-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="098b8-118">Persoonlijke gegevens, moet op Hallo verzoek van een onderwerp gegevens in Azure Active Directory en Azure SQL Database worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="098b8-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon hello request of a data subject.</span></span>

- <span data-ttu-id="098b8-119">Persoonlijke gegevens moet in een algemene, gestructureerde indeling op Hallo verzoek van een onderwerp gegevens worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="098b8-119">Personal data must be exported in a common, structured format upon hello request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="098b8-120">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="098b8-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="098b8-121">Azure Active Directory: onjuiste of onvolledige persoonlijke gegevens herstellen/corrigeren en persoonlijke gegevens/gebruikersprofielen wissen en verwijderen</span><span class="sxs-lookup"><span data-stu-id="098b8-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="098b8-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) van Microsoft cloud-gebaseerde, multitenant directory en identity management-service is.</span><span class="sxs-lookup"><span data-stu-id="098b8-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="098b8-123">U kunt corrigeren, bijwerken of verwijderen van klanten en werknemers gebruikersprofielen en gebruikersgegevens werk die persoonlijke gegevens bevatten, zoals naam, werk titel, adres of telefoonnummer, een gebruiker in uw [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) omgeving met behulp van Hallo [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="098b8-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="098b8-124">U moet zich aanmelden met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="098b8-124">You must sign in with an account that’s a global admin for hello directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="098b8-125">Hoe corrigeren of bijwerken van gebruikersprofiel en werk ik gegevens in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="098b8-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="098b8-126">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="098b8-126">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="098b8-127">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="098b8-127">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![Media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="098b8-129">Op Hallo **gebruikers en groepen** blade Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="098b8-129">On hello **Users and groups** blade, select **Users**.</span></span>

    ![Media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="098b8-131">Op Hallo **gebruikers en groepen - gebruikers** blade, selecteer een gebruiker in de lijst Hallo en selecteer vervolgens het volgende op de blade voor de geselecteerde gebruiker Hallo Hallo **profiel** tooview Hallo profielgegevens die toobe gecorrigeerd behoeften of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="098b8-131">On hello **Users and groups - Users** blade, select a user from hello list, and then, on hello blade for hello selected user, select **Profile** tooview hello user profile information that needs toobe corrected or updated.</span></span>

    ![Media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="098b8-133">Corrigeer of Hallo-informatie bijwerken en selecteer vervolgens in de opdrachtbalk Hallo **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="098b8-133">Correct or update hello information, and then, in hello command bar, select **Save.**</span></span>

6.  <span data-ttu-id="098b8-134">Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **Info werken** tooview werk gebruikersgegevens die toobe behoeften gecorrigeerd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="098b8-134">On hello blade for hello selected user, select **Work Info** tooview user work information that needs toobe corrected or updated.</span></span>

    ![Media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="098b8-136">Corrigeer of Hallo werk gebruikersgegevens bijwerken en selecteer vervolgens in de opdrachtbalk Hallo **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="098b8-136">Correct or update hello user work information, and then, in hello command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="098b8-137">Hoe verwijder ik een gebruikersprofiel in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="098b8-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="098b8-138">Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="098b8-138">Sign in toohello [Azure portal](https://portal.azure.com) with an account that's a global admin for hello directory.</span></span>

2. <span data-ttu-id="098b8-139">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="098b8-139">Select **More services**, enter **Users and groups** in hello text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="098b8-140">Op Hallo **gebruikers en groepen** blade Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="098b8-140">On hello **Users and groups** blade, select **Users**.</span></span>

    ![Media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="098b8-142">Op Hallo **gebruikers en groepen - gebruikers** blade, selecteert u een gebruiker in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="098b8-142">On hello **Users and groups - Users** blade, select a user from hello list.</span></span>

    ![Media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="098b8-144">Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **overzicht**, en selecteer vervolgens in de opdrachtbalk Hallo **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="098b8-144">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="098b8-145">SQL Database: herstellen/Corrigeer onjuiste of onvolledige persoonsgegevens; wissen en verwijderen van persoonsgegevens; exporteren van persoonlijke gegevens</span><span class="sxs-lookup"><span data-stu-id="098b8-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="098b8-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is een cloud-database die kan softwareontwikkelaars maken en onderhouden van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="098b8-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="098b8-147">Persoonlijke gegevens kunnen worden bijgewerkt [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) met behulp van standaard SQL-query's, en kan ook worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="098b8-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="098b8-148">Bovendien kunnen persoonlijke gegevens uit SQL-Database met verschillende methoden, waaronder hello Azure SQL-Server importeren en de wizard exporteren en in verschillende indelingen, waaronder een Bacpac-bestand worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="098b8-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including hello Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="098b8-149">Hoe ik corrigeren, bijwerken of persoonlijke gegevens in SQL-Database wissen?</span><span class="sxs-lookup"><span data-stu-id="098b8-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="098b8-150">toolearn hoe toocorrect of update persoonlijke gegevens in SQL-Database, gaat u naar Hallo [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [tekst bijwerken](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [bijwerken met algemene tabelexpressie](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), of [ Tekst schrijven bijwerken](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentatie.</span><span class="sxs-lookup"><span data-stu-id="098b8-150">toolearn how toocorrect or update personal data in SQL Database, visit hello [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="098b8-151">toolearn hoe toodelete persoonlijke gegevens in SQL-Database, gaat u naar Hallo [verwijderen (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentatie.</span><span class="sxs-lookup"><span data-stu-id="098b8-151">toolearn how toodelete personal data in SQL Database, visit hello [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a><span data-ttu-id="098b8-152">Hoe exporteer ik persoonlijke gegevens tooa Bacpac-bestand in de SQL-Database</span><span class="sxs-lookup"><span data-stu-id="098b8-152">How do I export personal data tooa BACPAC file in SQL Database?</span></span>

<span data-ttu-id="098b8-153">Een Bacpac-bestand bevat Hallo SQL-Database gegevens en metagegevens en een zip-bestand met een Bacpac-extensie is.</span><span class="sxs-lookup"><span data-stu-id="098b8-153">A BACPAC file includes hello SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="098b8-154">U kunt dit doen met behulp van Hallo [Azure-portal](https://portal.azure.com/), Hallo SQLPackage opdrachtregelprogramma, SQL Server Management Studio (SSMS) of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="098b8-154">This can be done using hello [Azure portal](https://portal.azure.com/), hello SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="098b8-155">toolearn hoe tooexport tooa Bacpac-gegevensbestand, gaat u naar Hallo [een Azure SQL database tooa Bacpac-bestand exporteren](https://docs.microsoft.com/azure/sql-database/sql-database-export) pagina met gedetailleerde instructies voor elke methode die hierboven worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="098b8-155">toolearn how tooexport data tooa BACPAC file, visit hello [Export an Azure SQL database tooa BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="098b8-156">Hoe exporteer persoonlijke gegevens van SQL Database met SQL Server Importeer Hallo Wizard en exporteren?</span><span class="sxs-lookup"><span data-stu-id="098b8-156">How do I export personal data from SQL Database with hello SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="098b8-157">Deze wizard kunt u gegevens kopiëren van een bron tooa doel.</span><span class="sxs-lookup"><span data-stu-id="098b8-157">This wizard helps you copy data from a source tooa destination.</span></span> <span data-ttu-id="098b8-158">Een inleiding toohello wizard, met inbegrip van hoe tooget deze machtigingen informatie en hoe tooget helpen met Hallo hulpprogramma, gaat u naar Hallo [importeren en exporteren van gegevens met Hallo SQL Server importeren en exporteren Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) webpagina.</span><span class="sxs-lookup"><span data-stu-id="098b8-158">For an introduction toohello wizard, including how tooget it, permissions information, and how tooget help with hello tool, visit hello [Import and Export Data with hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="098b8-159">Voor een overzicht van stappen voor het Hallo-wizard, gaat u naar Hallo [stappen in de Wizard exporteren en SQL Server Importeer Hallo](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) webpagina.</span><span class="sxs-lookup"><span data-stu-id="098b8-159">For an overview of steps for hello wizard, visit hello [Steps in hello SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="098b8-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="098b8-160">Next Steps:</span></span>

[<span data-ttu-id="098b8-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="098b8-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="098b8-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="098b8-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)


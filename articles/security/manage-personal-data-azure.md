---
title: Persoonlijke gegevens beheren in Microsoft Azure | Microsoft Docs
description: richtlijnen voor het corrigeren, bijwerken, verwijderen en exporteren van persoonlijke gegevens in Azure Active Directory en Azure SQL Database
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
ms.openlocfilehash: b04c745feb710d3d1d8a1fce23807168d6e6fa3d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-personal-data-in-microsoft-azure"></a><span data-ttu-id="1264c-103">Persoonlijke gegevens beheren in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="1264c-103">Manage personal data in Microsoft Azure</span></span>

<span data-ttu-id="1264c-104">In dit artikel biedt richtlijnen voor het corrigeren, bijwerken, verwijderen en exporteren van persoonlijke gegevens in Azure Active Directory en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1264c-104">This article provides guidance on how to correct, update, delete, and export personal data in Azure Active Directory and Azure SQL Database.</span></span>

## <a name="scenario"></a><span data-ttu-id="1264c-105">Scenario</span><span class="sxs-lookup"><span data-stu-id="1264c-105">Scenario</span></span>

<span data-ttu-id="1264c-106">Een bedrijf Dublin gebaseerde biedt one-stop winkelen voor hoge einde bestemming bruiloften in Ierland en over de hele wereld voor zowel een lokale en internationale klanten.</span><span class="sxs-lookup"><span data-stu-id="1264c-106">A Dublin-based company provides one-stop shopping for high end destination weddings in Ireland and around the world for both a local and international customer base.</span></span> <span data-ttu-id="1264c-107">Ze hebben kantoren, klanten, werknemers en leveranciers over de hele wereld om de plaatsen die ze bieden volledig te verwerken.</span><span class="sxs-lookup"><span data-stu-id="1264c-107">They have offices, customers, employees, and vendors located around the world to fully service the venues they offer.</span></span>

<span data-ttu-id="1264c-108">Tussen veel andere items het bedrijf houdt van geen r.s.v.p. 's die voedselallergieën en via de voeding voorkeuren bevatten.</span><span class="sxs-lookup"><span data-stu-id="1264c-108">Among many other items, the company keeps track of RSVPs that include food allergies and dietary preferences.</span></span> <span data-ttu-id="1264c-109">Bruiloft gasten kunnen worden geregistreerd voor verschillende activiteiten zoals horseback fiets, surfen, is aangewezen ritjes, enz., en zelfs communiceren met elkaar op een centrale webpagina tijdens de maanden voorafgaand aan de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="1264c-109">Wedding guests can register for various activities such as horseback riding, surfing, boat rides, etc., and even interact with one another on a central web page during the months leading up to the event.</span></span> <span data-ttu-id="1264c-110">Het bedrijf verzamelt persoonlijke gegevens van werknemers, leveranciers, klanten en bruiloft gasten.</span><span class="sxs-lookup"><span data-stu-id="1264c-110">The company collects personal information from employees, vendors, customers, and wedding guests.</span></span> <span data-ttu-id="1264c-111">Vanwege de internationale aard van het bedrijf moet het bedrijf met meerdere niveaus van regelgeving voldoen.</span><span class="sxs-lookup"><span data-stu-id="1264c-111">Because of the international nature of the business the company must comply with multiple levels of regulation.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="1264c-112">Probleemformulering</span><span class="sxs-lookup"><span data-stu-id="1264c-112">Problem statement</span></span>

- <span data-ttu-id="1264c-113">Beheerders van gegevens moet kunnen juiste onnauwkeurig persoonlijke informatie en update onvolledig of veranderende persoonlijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="1264c-113">Data admins must be able to correct inaccurate personal information and update incomplete or changing personal information.</span></span>

- <span data-ttu-id="1264c-114">Gegevens beheerders nodig moet kunnen persoonlijke gegevens op verzoek van een onderwerp gegevens verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1264c-114">Data admins need must be able to delete personal information upon the request of a data subject.</span></span>

- <span data-ttu-id="1264c-115">Beheerders van gegevens moet gegevens exporteren en opgeven in een onderwerp van de gegevens in een algemene, gestructureerde indeling op zijn of haar verzoek.</span><span class="sxs-lookup"><span data-stu-id="1264c-115">Data admins need to export data and provide it to a data subject in a common, structured format upon his or her request.</span></span>

## <a name="company-goals"></a><span data-ttu-id="1264c-116">Bedrijfsdoelstellingen</span><span class="sxs-lookup"><span data-stu-id="1264c-116">Company goals</span></span>

- <span data-ttu-id="1264c-117">Onjuiste of onvolledige klant, bruiloft Gast werknemer en persoonlijke gegevens van de leverancier moeten worden gecorrigeerd of bijgewerkt in Azure Active Directory en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1264c-117">Inaccurate or incomplete customer, wedding guest, employee, and vendor personal information must be corrected or updated in Azure Active Directory and Azure SQL Database.</span></span>

- <span data-ttu-id="1264c-118">Persoonlijke gegevens, moet op verzoek van een onderwerp gegevens in Azure Active Directory en Azure SQL Database worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1264c-118">Personal information must be deleted in Azure Active Directory and Azure SQL Database upon the request of a data subject.</span></span>

- <span data-ttu-id="1264c-119">Persoonlijke gegevens moet in een algemene, gestructureerde indeling op verzoek van een onderwerp gegevens worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="1264c-119">Personal data must be exported in a common, structured format upon the request of a data subject.</span></span>

## <a name="solutions"></a><span data-ttu-id="1264c-120">Oplossingen</span><span class="sxs-lookup"><span data-stu-id="1264c-120">Solutions</span></span>

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a><span data-ttu-id="1264c-121">Azure Active Directory: onjuiste of onvolledige persoonlijke gegevens herstellen/corrigeren en persoonlijke gegevens/gebruikersprofielen wissen en verwijderen</span><span class="sxs-lookup"><span data-stu-id="1264c-121">Azure Active Directory: rectify/correct inaccurate or incomplete personal data and erase/delete personal data/user profiles</span></span>

<span data-ttu-id="1264c-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) van Microsoft cloud-gebaseerde, multitenant directory en identity management-service is.</span><span class="sxs-lookup"><span data-stu-id="1264c-122">[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) is Microsoft’s cloud-based, multi-tenant directory and identity management service.</span></span>
<span data-ttu-id="1264c-123">U kunt corrigeren, bijwerken of verwijderen van klanten en werknemers gebruikersprofielen en gebruikersgegevens werk die persoonlijke gegevens bevatten, zoals naam, werk titel, adres of telefoonnummer, een gebruiker in uw [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) omgeving met behulp van de [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="1264c-123">You can correct, update, or delete customer and employee user profiles and user work information that contain personal data, such as a user’s name, work title, address, or phone number, in your [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) environment by using the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="1264c-124">U moet zich aanmelden met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="1264c-124">You must sign in with an account that’s a global admin for the directory.</span></span>

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a><span data-ttu-id="1264c-125">Hoe corrigeren of bijwerken van gebruikersprofiel en werk ik gegevens in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1264c-125">How do I correct or update user profile and work information in Azure Active Directory?</span></span>

1. <span data-ttu-id="1264c-126">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="1264c-126">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="1264c-127">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1264c-127">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![Media/image1.png](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="1264c-129">Op de **gebruikers en groepen** blade Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1264c-129">On the **Users and groups** blade, select **Users**.</span></span>

    ![Media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="1264c-131">Op de **gebruikers en groepen - gebruikers** blade, selecteert u een gebruiker in de lijst en selecteer vervolgens het volgende op de blade voor de geselecteerde gebruiker **profiel** om weer te geven van de gebruikersgegevens voor het profiel dat moet worden gecorrigeerd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1264c-131">On the **Users and groups - Users** blade, select a user from the list, and then, on the blade for the selected user, select **Profile** to view the user profile information that needs to be corrected or updated.</span></span>

    ![Media/image3.png](media/manage-personal-data-azure/image005.png)

5. <span data-ttu-id="1264c-133">Corrigeer of werkt u de gegevens en selecteer vervolgens in de opdrachtbalk **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="1264c-133">Correct or update the information, and then, in the command bar, select **Save.**</span></span>

6.  <span data-ttu-id="1264c-134">Selecteer op de blade voor de geselecteerde gebruiker **Info werken** om weer te geven van gebruikersgegevens werk die moet worden gecorrigeerd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1264c-134">On the blade for the selected user, select **Work Info** to view user work information that needs to be corrected or updated.</span></span>

    ![Media/image4.png](media/manage-personal-data-azure/image007.png)

7. <span data-ttu-id="1264c-136">Corrigeer of bijwerken van de gegevens voor het werk van gebruiker en selecteer vervolgens in de opdrachtbalk **opslaan.**</span><span class="sxs-lookup"><span data-stu-id="1264c-136">Correct or update the user work information, and then, in the command bar, select **Save.**</span></span>

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a><span data-ttu-id="1264c-137">Hoe verwijder ik een gebruikersprofiel in Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="1264c-137">How do I delete a user profile in Azure Active Directory?</span></span>

1. <span data-ttu-id="1264c-138">Aanmelden bij de [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor de map.</span><span class="sxs-lookup"><span data-stu-id="1264c-138">Sign in to the [Azure portal](https://portal.azure.com) with an account that's a global admin for the directory.</span></span>

2. <span data-ttu-id="1264c-139">Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak in en selecteer vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1264c-139">Select **More services**, enter **Users and groups** in the text box, and then select **Enter**.</span></span>

    ![](media/manage-personal-data-azure/image001.png)

3. <span data-ttu-id="1264c-140">Op de **gebruikers en groepen** blade Selecteer **gebruikers**.</span><span class="sxs-lookup"><span data-stu-id="1264c-140">On the **Users and groups** blade, select **Users**.</span></span>

    ![Media/image2.png](media/manage-personal-data-azure/image003.png)

4. <span data-ttu-id="1264c-142">Selecteer op de blade **Gebruikers en groepen - Gebruikers** een gebruiker in de lijst.</span><span class="sxs-lookup"><span data-stu-id="1264c-142">On the **Users and groups - Users** blade, select a user from the list.</span></span>

    ![Media/image3.png](media/manage-personal-data-azure/image007.png)

5. <span data-ttu-id="1264c-144">Selecteer op de blade voor de geselecteerde gebruiker **overzicht**, en selecteer vervolgens in de opdrachtbalk **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="1264c-144">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a><span data-ttu-id="1264c-145">SQL Database: herstellen/Corrigeer onjuiste of onvolledige persoonsgegevens; wissen en verwijderen van persoonsgegevens; exporteren van persoonlijke gegevens</span><span class="sxs-lookup"><span data-stu-id="1264c-145">SQL Database: rectify/correct inaccurate or incomplete personal data; erase/delete personal data; export personal data</span></span> 

<span data-ttu-id="1264c-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is een cloud-database die kan softwareontwikkelaars maken en onderhouden van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="1264c-146">[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is a cloud database that helps developers build and maintain applications.</span></span>

<span data-ttu-id="1264c-147">Persoonlijke gegevens kunnen worden bijgewerkt [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) met behulp van standaard SQL-query's, en kan ook worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1264c-147">Personal data can be updated in [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) using standard SQL queries, and it can also be deleted.</span></span> <span data-ttu-id="1264c-148">Bovendien kunnen persoonlijke gegevens worden geëxporteerd vanuit SQL-Database met een aantal methoden, met inbegrip van de Azure SQL-Server importeren en exporteren van de wizard en in verschillende indelingen, waaronder een Bacpac-bestand.</span><span class="sxs-lookup"><span data-stu-id="1264c-148">Additionally, personal data can be exported from SQL Database using a variety of methods, including the Azure SQL Server import and export wizard, and in a variety of formats, including a BACPAC file.</span></span>

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a><span data-ttu-id="1264c-149">Hoe ik corrigeren, bijwerken of persoonlijke gegevens in SQL-Database wissen?</span><span class="sxs-lookup"><span data-stu-id="1264c-149">How do I correct, update, or erase personal data in SQL Database?</span></span>

<span data-ttu-id="1264c-150">Als u wilt weten hoe u op te lossen of persoonlijke gegevens in SQL-Database bijwerken, gaat u naar de [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [tekst bijwerken](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [bijwerken met algemene tabelexpressie](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), of [Update schrijven tekst](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentatie.</span><span class="sxs-lookup"><span data-stu-id="1264c-150">To learn how to correct or update personal data in SQL Database, visit the [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [Update Text](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [Update with Common Table Expression](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), or [Update Write Text](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentation.</span></span>

<span data-ttu-id="1264c-151">Als u wilt weten hoe u om persoonlijke gegevens in SQL-Database te verwijderen, gaat u naar de [verwijderen (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentatie.</span><span class="sxs-lookup"><span data-stu-id="1264c-151">To learn how to delete personal data in SQL Database, visit the [Delete (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentation.</span></span>

#### <a name="how-do-i-export-personal-data-to-a-bacpac-file-in-sql-database"></a><span data-ttu-id="1264c-152">Hoe exporteer persoonlijke gegevens naar een Bacpac-bestand in SQL-Database?</span><span class="sxs-lookup"><span data-stu-id="1264c-152">How do I export personal data to a BACPAC file in SQL Database?</span></span>

<span data-ttu-id="1264c-153">Een Bacpac-bestand bevat de gegevens van de SQL-Database en de metagegevens en een zip-bestand met een Bacpac-extensie is.</span><span class="sxs-lookup"><span data-stu-id="1264c-153">A BACPAC file includes the SQL Database data and metadata and is a zip file with a BACPAC extension.</span></span> <span data-ttu-id="1264c-154">U kunt dit doen met behulp van de [Azure-portal](https://portal.azure.com/), het opdrachtregelprogramma SQLPackage, SQL Server Management Studio (SSMS) of PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1264c-154">This can be done using the [Azure portal](https://portal.azure.com/), the SQLPackage command-line utility, SQL Server Management Studio (SSMS), or PowerShell.</span></span>

<span data-ttu-id="1264c-155">Voor informatie over het exporteren van gegevens naar een Bacpac-bestand, gaat u naar de [een Azure SQL database naar een Bacpac-bestand exporteren](https://docs.microsoft.com/azure/sql-database/sql-database-export) pagina met gedetailleerde instructies voor elke methode die hierboven worden genoemd.</span><span class="sxs-lookup"><span data-stu-id="1264c-155">To learn how to export data to a BACPAC file, visit the [Export an Azure SQL database to a BACPAC file](https://docs.microsoft.com/azure/sql-database/sql-database-export) page, which includes detailed instructions for each method listed above.</span></span>

<span data-ttu-id="1264c-156">Hoe exporteer persoonlijke gegevens uit SQL-Database met de SQL Server Wizard importeren en exporteren?</span><span class="sxs-lookup"><span data-stu-id="1264c-156">How do I export personal data from SQL Database with the SQL Server Import and Export Wizard?</span></span>

<span data-ttu-id="1264c-157">Deze wizard kunt u gegevens kopiëren van een bron naar doel.</span><span class="sxs-lookup"><span data-stu-id="1264c-157">This wizard helps you copy data from a source to a destination.</span></span> <span data-ttu-id="1264c-158">Voor een inleiding tot de wizard, met inbegrip van het ophalen, machtigingen informatie en hoe u hulp bij het hulpprogramma, gaat u naar de [importeren en exporteren van gegevens met de SQL Server Wizard importeren en exporteren](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) webpagina.</span><span class="sxs-lookup"><span data-stu-id="1264c-158">For an introduction to the wizard, including how to get it, permissions information, and how to get help with the tool, visit the [Import and Export Data with the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) web page.</span></span>

<span data-ttu-id="1264c-159">Voor een overzicht van stappen voor de wizard, gaat u naar de [stappen in de SQL Server Wizard importeren en exporteren](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) webpagina.</span><span class="sxs-lookup"><span data-stu-id="1264c-159">For an overview of steps for the wizard, visit the [Steps in the SQL Server Import and Export Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) web page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1264c-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1264c-160">Next Steps:</span></span>

[<span data-ttu-id="1264c-161">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1264c-161">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[<span data-ttu-id="1264c-162">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1264c-162">Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)


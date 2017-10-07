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
# <a name="manage-personal-data-in-microsoft-azure"></a>Persoonlijke gegevens beheren in Microsoft Azure

In dit artikel biedt richtlijnen voor hoe toocorrect, bijwerken, verwijderen en exporteren van persoonlijke gegevens in Azure Active Directory en Azure SQL Database.

## <a name="scenario"></a>Scenario

Een bedrijf Dublin gebaseerde biedt hoge einde bestemming bruiloften in Ierland en Hallo wereld voor zowel een lokale en internationale klant base one-stop winkelen. Ze hebben kantoren, klanten, werknemers en leveranciers rond hello world toofully service Hallo plaatsen die ze bieden.

Tussen veel andere items Hallo bedrijf houdt van geen r.s.v.p. 's die voedselallergieën en via de voeding voorkeuren bevatten. Bruiloft gasten kunnen worden geregistreerd voor verschillende activiteiten zoals horseback fiets, surfen, is aangewezen ritjes, enz., en zelfs communiceren met elkaar op een centrale webpagina tijdens Hallo maanden voorafgaand toohello gebeurtenis. Hallo bedrijf verzamelt persoonlijke gegevens van werknemers, leveranciers, klanten en bruiloft gasten. Vanwege Hallo moet internationale aard van de onderneming Hallo Hallo voldoen aan meerdere niveaus van de regelgeving.

## <a name="problem-statement"></a>Probleemformulering

- Beheerders van gegevens moet kunnen toocorrect onnauwkeurig persoonlijke informatie en update onvolledig of veranderende persoonlijke gegevens.

- Gegevens beheerders nodig moet kunnen toodelete persoonlijke gegevens op verzoek Hallo van een onderwerp gegevens.

- Gegevens admins tooexport gegevens nodig en geef deze tooa gegevens onderwerp in een algemene, gestructureerde indeling op zijn of haar verzoek.

## <a name="company-goals"></a>Bedrijfsdoelstellingen

- Onjuiste of onvolledige klant, bruiloft Gast werknemer en persoonlijke gegevens van de leverancier moeten worden gecorrigeerd of bijgewerkt in Azure Active Directory en Azure SQL Database.

- Persoonlijke gegevens, moet op Hallo verzoek van een onderwerp gegevens in Azure Active Directory en Azure SQL Database worden verwijderd.

- Persoonlijke gegevens moet in een algemene, gestructureerde indeling op Hallo verzoek van een onderwerp gegevens worden geëxporteerd.

## <a name="solutions"></a>Oplossingen

### <a name="azure-active-directory-rectifycorrect-inaccurate-or-incomplete-personal-data-and-erasedelete-personal-datauser-profiles"></a>Azure Active Directory: onjuiste of onvolledige persoonlijke gegevens herstellen/corrigeren en persoonlijke gegevens/gebruikersprofielen wissen en verwijderen

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/) van Microsoft cloud-gebaseerde, multitenant directory en identity management-service is.
U kunt corrigeren, bijwerken of verwijderen van klanten en werknemers gebruikersprofielen en gebruikersgegevens werk die persoonlijke gegevens bevatten, zoals naam, werk titel, adres of telefoonnummer, een gebruiker in uw [Azure Active Directory](https://azure.microsoft.com/services/active-directory/) (AAD) omgeving met behulp van Hallo [Azure-portal](https://portal.azure.com/).

U moet zich aanmelden met een account met globale beheerdersrechten voor Hallo-directory.

#### <a name="how-do-i-correct-or-update-user-profile-and-work-information-in-azure-active-directory"></a>Hoe corrigeren of bijwerken van gebruikersprofiel en werk ik gegevens in Azure Active Directory?

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.

2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

    ![Media/image1.png](media/manage-personal-data-azure/image001.png)

3. Op Hallo **gebruikers en groepen** blade Selecteer **gebruikers**.

    ![Media/image2.png](media/manage-personal-data-azure/image003.png)

4. Op Hallo **gebruikers en groepen - gebruikers** blade, selecteer een gebruiker in de lijst Hallo en selecteer vervolgens het volgende op de blade voor de geselecteerde gebruiker Hallo Hallo **profiel** tooview Hallo profielgegevens die toobe gecorrigeerd behoeften of bijgewerkt.

    ![Media/image3.png](media/manage-personal-data-azure/image005.png)

5. Corrigeer of Hallo-informatie bijwerken en selecteer vervolgens in de opdrachtbalk Hallo **opslaan.**

6.  Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **Info werken** tooview werk gebruikersgegevens die toobe behoeften gecorrigeerd of bijgewerkt.

    ![Media/image4.png](media/manage-personal-data-azure/image007.png)

7. Corrigeer of Hallo werk gebruikersgegevens bijwerken en selecteer vervolgens in de opdrachtbalk Hallo **opslaan.**

#### <a name="how-do-i-delete-a-user-profile-in-azure-active-directory"></a>Hoe verwijder ik een gebruikersprofiel in Azure Active Directory?

1. Meld u aan toohello [Azure-portal](https://portal.azure.com) met een account met globale beheerdersrechten voor Hallo-directory.

2. Selecteer **meer services**, voer **gebruikers en groepen** in het tekstvak Hallo en selecteer vervolgens **Enter**.

    ![](media/manage-personal-data-azure/image001.png)

3. Op Hallo **gebruikers en groepen** blade Selecteer **gebruikers**.

    ![Media/image2.png](media/manage-personal-data-azure/image003.png)

4. Op Hallo **gebruikers en groepen - gebruikers** blade, selecteert u een gebruiker in de lijst Hallo.

    ![Media/image3.png](media/manage-personal-data-azure/image007.png)

5. Selecteer op de blade voor de geselecteerde gebruiker Hallo Hallo **overzicht**, en selecteer vervolgens in de opdrachtbalk Hallo **verwijderen**.

    ![](media/manage-personal-data-azure/image013.png)

### <a name="sql-database-rectifycorrect-inaccurate-or-incomplete-personal-data-erasedelete-personal-data-export-personal-data"></a>SQL Database: herstellen/Corrigeer onjuiste of onvolledige persoonsgegevens; wissen en verwijderen van persoonsgegevens; exporteren van persoonlijke gegevens 

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) is een cloud-database die kan softwareontwikkelaars maken en onderhouden van toepassingen.

Persoonlijke gegevens kunnen worden bijgewerkt [Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) met behulp van standaard SQL-query's, en kan ook worden verwijderd. Bovendien kunnen persoonlijke gegevens uit SQL-Database met verschillende methoden, waaronder hello Azure SQL-Server importeren en de wizard exporteren en in verschillende indelingen, waaronder een Bacpac-bestand worden geëxporteerd.

#### <a name="how-do-i-correct-update-or-erase-personal-data-in-sql-database"></a>Hoe ik corrigeren, bijwerken of persoonlijke gegevens in SQL-Database wissen?

toolearn hoe toocorrect of update persoonlijke gegevens in SQL-Database, gaat u naar Hallo [Update (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/queries/update-transact-sql), [tekst bijwerken](https://docs.microsoft.com/sql/t-sql/queries/updatetext-transact-sql), [bijwerken met algemene tabelexpressie](https://docs.microsoft.com/sql/t-sql/queries/with-common-table-expression-transact-sql), of [ Tekst schrijven bijwerken](https://docs.microsoft.com/sql/t-sql/queries/writetext-transact-sql) documentatie.

toolearn hoe toodelete persoonlijke gegevens in SQL-Database, gaat u naar Hallo [verwijderen (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/delete-transact-sql) documentatie.

#### <a name="how-do-i-export-personal-data-tooa-bacpac-file-in-sql-database"></a>Hoe exporteer ik persoonlijke gegevens tooa Bacpac-bestand in de SQL-Database

Een Bacpac-bestand bevat Hallo SQL-Database gegevens en metagegevens en een zip-bestand met een Bacpac-extensie is. U kunt dit doen met behulp van Hallo [Azure-portal](https://portal.azure.com/), Hallo SQLPackage opdrachtregelprogramma, SQL Server Management Studio (SSMS) of PowerShell.

toolearn hoe tooexport tooa Bacpac-gegevensbestand, gaat u naar Hallo [een Azure SQL database tooa Bacpac-bestand exporteren](https://docs.microsoft.com/azure/sql-database/sql-database-export) pagina met gedetailleerde instructies voor elke methode die hierboven worden genoemd.

Hoe exporteer persoonlijke gegevens van SQL Database met SQL Server Importeer Hallo Wizard en exporteren?

Deze wizard kunt u gegevens kopiëren van een bron tooa doel. Een inleiding toohello wizard, met inbegrip van hoe tooget deze machtigingen informatie en hoe tooget helpen met Hallo hulpprogramma, gaat u naar Hallo [importeren en exporteren van gegevens met Hallo SQL Server importeren en exporteren Wizard](https://docs.microsoft.com/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard) webpagina.

Voor een overzicht van stappen voor het Hallo-wizard, gaat u naar Hallo [stappen in de Wizard exporteren en SQL Server Importeer Hallo](https://docs.microsoft.com/sql/integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard) webpagina.

## <a name="next-steps"></a>Volgende stappen

[Azure SQL Database](https://azure.microsoft.com/services/sql-database/?v=16.50) 

[Azure Active Directory](https://azure.microsoft.com/services/active-directory/)


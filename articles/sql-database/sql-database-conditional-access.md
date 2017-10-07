---
title: aaaConditional Access - Azure SQL Database en datawarehouse | Microsoft-document
description: Meer informatie over hoe tooconfigure voorwaardelijke toegang voor Azure SQL Database en datawarehouse.
services: sql-database
author: BYHAM
manager: jhubbard
ms.custom: security
ms.service: sql-database
ms.topic: article
ms.date: 06/07/2017
ms.author: rickbyh
ms.openlocfilehash: f49f4708c0f1b3cad1539d630c2efd919f8ece68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-mfa-with-azure-sql-database-and-data-warehouse"></a>Voorwaardelijke toegang (MFA) met Azure SQL Database en datawarehouse  

Ondersteuning voor voorwaardelijke toegang van Microsoft SQL Database- en SQL Data Warehouse. Hallo van de volgende stappen tonen hoe tooconfigure SQL-Database tooenforce beleid voor voorwaardelijke toegang.  

## <a name="prerequisites"></a>Vereisten  
- U moet de SQL-Database of SQL Data Warehouse toosupport Azure Active Directory-verificatie configureren. Zie voor specifieke stappen [configureren en beheren van Azure Active Directory-verificatie met SQL-Database of SQL Data Warehouse](sql-database-aad-authentication-configure.md).  
- Als multi-factor authentication-server is ingeschakeld, moet u verbinding maken met op ondersteunde hulpprogramma, zoals het meest recente SSMS Hallo. Zie voor meer informatie [Azure SQL-Database configureren multi-factor authentication voor SQL Server Management Studio](sql-database-ssms-mfa-authentication-configure.md).  

## <a name="configure-ca-for-azure-sql-dbdw"></a>CA configureren voor Azure SQL DB/DW  
1.  Aanmelden toohello Portal, selecteer **Azure Active Directory**, en selecteer vervolgens **voorwaardelijke toegang**. Zie voor meer informatie [technische documentatie voor Azure Active Directory voorwaardelijke toegang](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-conditional-access-technical-reference).  
  ![blade voor voorwaardelijke toegang](./media/sql-database-conditional-access/conditional-access-blade.png) 
     
2.  In Hallo **-beleid voor voorwaardelijke toegang** blade, klikt u op **nieuw beleid**, Geef een naam op en klik vervolgens op **regels configureren**.  
3.  Onder **toewijzingen**, selecteer **gebruikers en groepen**, Controleer **gebruikers en groepen selecteren**, en selecteer vervolgens het Hallo-gebruiker of groep voor voorwaardelijke toegang. Klik op **Selecteer**, en klik vervolgens op **gedaan** tooaccept uw selectie.  
  ![gebruikers en groepen selecteren](./media/sql-database-conditional-access/select-users-and-groups.png)  

4.  Selecteer **Cloud-apps**, klikt u op **apps selecteren**. Ziet u alle apps beschikbaar voor voorwaardelijke toegang. Selecteer **Azure SQL Database**, Hallo Klik onder aan op **Selecteer**, en klik vervolgens op **gedaan**.  
  ![SQL-Database selecteren](./media/sql-database-conditional-access/select-sql-database.png)  
  Als u niet kunt vinden **Azure SQL Database** wordt vermeld in de derde schermopname na hello, voltooien Hallo stappen te volgen:   
  - Meld u aan tooyour Azure SQL DB/DW-exemplaar met behulp van SSMS met een AAD-beheerdersaccount.  
  - Uitvoeren van `CREATE USER [user@yourtenant.com] FROM EXTERNAL PROVIDER`.  
  - Meld u aan tooAAD en controleer of Azure SQL Database en datawarehouse worden in het Hallo-toepassingen in uw AAD weergegeven.  

5.  Selecteer **toegangscontroles**, selecteer **Grant**, en controleer vervolgens de gewenste tooapply Hallo-beleid. In dit voorbeeld selecteren we **meervoudige authenticatie**.  
  ![Selecteer toegang verlenen](./media/sql-database-conditional-access/grant-access.png)  

## <a name="summary"></a>Samenvatting  
Hallo geselecteerd toepassing (Azure SQL Database) tooconnect tooAzure SQL DB/DW met behulp van Azure AD Premium, zodat worden nu afgedwongen beleid voor voorwaardelijke toegang van Hallo geselecteerd, **vereist multi-factor authentication-server.**  
Voor vragen over Azure SQL Database en datawarehouse met betrekking tot de multi-factor authentication-server contact op met MFAforSQLDB@microsoft.com.  

## <a name="next-steps"></a>Volgende stappen  

Zie voor een zelfstudie [beveiligen van uw Azure SQL Database](sql-database-security-tutorial.md).

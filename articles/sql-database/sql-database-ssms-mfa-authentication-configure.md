---
title: aaaConfigure meerledige verificatie - Azure SQL | Microsoft Docs
description: Gebruik Multi meeberekend verificatie met SSMS voor SQL-Database en SQL datawarehouse.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/17/2017
ms.author: rickbyh
ms.openlocfilehash: acb275965f4199f7d5e1378d5077824a9bbc80e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-multi-factor-authentication-for-sql-server-management-studio-and-azure-ad"></a>Multi-factor authentication voor SQL Server Management Studio en Azure AD configureren

Dit onderwerp leest u hoe toouse Azure Active Directory multi-factor authentication (MFA) met SQL Server Management Studio. Azure AD MFA kan worden gebruikt bij het verbinden van SSMS of SqlPackage.exe tooAzure SQL-Database en Azure SQL Data Warehouse.

Zie voor een overzicht van Azure SQL Database multi-factor authentication [Universal verificatie met SQL-Database en SQL Data Warehouse (SSMS ondersteuning voor MFA)](sql-database-ssms-mfa-authentication.md).

## <a name="configuration-steps"></a>Configuratiestappen

1. **Een Azure Active Directory configureren** - voor meer informatie Zie [beheer van uw Azure AD-directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [uw on-premises identiteiten integreren met Azure Active Directory](../active-directory/active-directory-aadconnect.md), [Toevoegen van uw eigen domein naam tooAzure AD](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [Microsoft Azure biedt nu ondersteuning voor federatie met Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), en [beheren Azure AD dat gebruikmaakt van Windows PowerShell ](https://msdn.microsoft.com/library/azure/jj151815.aspx).
2. **MFA configureren** - voor stapsgewijze instructies, Zie [wat is Azure multi-factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md), [voorwaardelijke toegang (MFA) met Azure SQL Database en datawarehouse](sql-database-conditional-access.md). (Volledige voorwaardelijke toegang is vereist voor een Premium Azure Active Directory (Azure AD). Beperkte MFA is beschikbaar met een standaard Azure AD.)
3. **Configureer SQL-Database of SQL Data Warehouse voor Azure AD Authentication** - voor stapsgewijze instructies Zie [verbinding maakt met tooSQL Database of SQL Data Warehouse door met behulp van Azure Active Directory-verificatie](sql-database-aad-authentication.md).
4. **Downloaden van SSMS** : klik op de clientcomputer Hallo downloaden nieuwste SSMS Hallo van [Download SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Voor alle Hallo-functies in dit onderwerp, gebruikt u ten minste versie 17,2 juli 2017.  

## <a name="connecting-by-using-universal-authentication-with-ssms"></a>Verbinding maken met behulp van universele verificatie met SSMS

Hallo stappen te volgen laten zien hoe tooconnect tooSQL Database of SQL Data Warehouse met behulp van SSMS nieuwste Hallo.

1. met behulp van universele verificatie op Hallo tooconnect **tooServer verbinding** dialoogvenster, **Active Directory - Universal met ondersteuning voor MFA**. (Als u ziet **Universal verificatie van Active Directory** u zich niet op de meest recente versie van SSMS Hallo.)  
   ![1mfa-universal-verbinding][1]  
2. Volledige Hallo **gebruikersnaam** vak met hello Azure Active Directory-referenties, Hallo indeling `user_name@domain.com`.  
   ![1mfa-universal-connect-gebruiker](./media/sql-database-ssms-mfa-auth/1mfa-universal-connect-user.png)   
3. Als u verbinding als gastgebruiker maakt, klikt u op **opties**, en op Hallo **verbindingseigenschap** dialoogvenster, volledige Hallo **AD-domein naam of het tenant-ID** vak. Zie voor meer informatie [Universal verificatie met SQL-Database en SQL Data Warehouse (SSMS ondersteuning voor MFA)](sql-database-ssms-mfa-authentication.md).
   ![MFA-tenant-ssms](./media/sql-database-ssms-mfa-auth/mfa-tenant-ssms.png)   
4. Zoals gebruikelijk voor SQL-Database en SQL Data Warehouse, klikt u op **opties** en geef Hallo-database op Hallo **opties** in het dialoogvenster. (Als Hallo verbonden gebruiker gastgebruiker is (d.w.z. joe@outlook.com), moet u Hallo selectievakje en Hallo huidige AD-domein naam of het tenant-ID toevoegen als onderdeel van de opties. Zie [Universal verificatie met SQL-Database en SQL Data Warehouse (SSMS ondersteuning voor MFA)]()(sql-database-ssms-mfa-authentication.md. Klik vervolgens op **Connect**.  
5. Wanneer Hallo **tooyour account aanmelden** dialoogvenster wordt weergegeven, geven Hallo-account en wachtwoord van uw Azure Active Directory-identiteit. Er is geen wachtwoord is vereist als een gebruiker deel van een domein dat gefedereerd met Azure AD uitmaakt.  
   ![2mfa-aanmeldingspagina][2]  

   > [!NOTE]
   > Voor universele verificatie met een account dat geen MFA vereist, u verbinding maken op dit moment. Voor gebruikers MFA verplicht stellen, blijven Hello stappen te volgen:
   >  
   
6. Twee dialoogvensters voor MFA-setup wordt mogelijk weergegeven. Deze eenmalige bewerking afhankelijk Hallo MFA beheerder instellen, en daarom mogelijk optioneel. Voor een domein MFA ingeschakeld in deze stap is het soms vooraf gedefinieerde (bijvoorbeeld Hallo domein vereist voor gebruikers toouse een smartcard en pincode).  
   ![3mfa setup][3]  
7. Hallo tweede mogelijk één keer in het dialoogvenster u tooselect Hallo details van de verificatiemethode kunt. Hallo mogelijke opties worden geconfigureerd door de beheerder.  
   ![4mfa-controleren 1][4]  
8. Hello Azure Active Directory verzendt Hallo informatie tooyou bevestigen. Wanneer u de verificatiecode Hallo ontvangt, voeren Hallo **Voer de verificatiecode** vak en klikt u op **aanmelden**.  
   ![5mfa-controleren-2][5]  

Als verificatie voltooid is, verbindt SSMS normaal vermoeden geldige referenties en firewalltoegang.

## <a name="next-steps"></a>Volgende stappen

* Zie voor een overzicht van Azure SQL Database multi-factor authentication, Universal verificatie met [SQL-Database en SQL Data Warehouse (SSMS ondersteuning voor MFA)](sql-database-ssms-mfa-authentication.md).
* Anderen tooyour database toegang kunt krijgen: [SQL Database-verificatie en autorisatie: toegang verlenen](sql-database-manage-logins.md)  
Zorg ervoor dat anderen verbinding kunnen maken via de firewall Hallo: [configureren een Azure SQL Database serverniveau firewall regel met hello Azure-portal](sql-database-configure-firewall-settings.md)


[1]: ./media/sql-database-ssms-mfa-auth/1mfa-universal-connect.png
[2]: ./media/sql-database-ssms-mfa-auth/2mfa-sign-in.png
[3]: ./media/sql-database-ssms-mfa-auth/3mfa-setup.png
[4]: ./media/sql-database-ssms-mfa-auth/4mfa-verify-1.png
[5]: ./media/sql-database-ssms-mfa-auth/5mfa-verify-2.png


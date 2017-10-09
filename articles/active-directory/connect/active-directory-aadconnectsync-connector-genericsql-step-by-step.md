---
title: stap aaaGeneric stap door de SQL-Connector | Microsoft Docs
description: Roulatie van dit artikel wordt u via een eenvoudige HR-systeem met behulp van stapsgewijze Hallo algemene SQL-Connector.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 28c1cc60-24fd-4d0d-a36d-b4aba6de86e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b1b5f89ab588de6f92f173a7bc00f97180067669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generic-sql-connector-step-by-step"></a>Algemene SQL Connector, stap voor stap
In dit onderwerp is een stapsgewijze handleiding. Deze maakt een eenvoudig voorbeeld HR-database en deze gebruiken voor het importeren van sommige gebruikers en hun groepslidmaatschap.

## <a name="prepare-hello-sample-database"></a>Hallo-voorbeelddatabase voorbereiden
Op een server met SQL Server, voert u Hallo SQL-script is gevonden in [bijlage A](#appendix-a). Dit script maakt een voorbeelddatabase met Hallo naam GSQLDEMO. Hallo-objectmodel voor Hallo gemaakt database lijkt erop deze afbeelding:  
![Objectmodel](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/objectmodel.png)

Ook een gebruiker die u toouse tooconnect toohello database wilt maken. In dit scenario is Hallo gebruiker FABRIKAM\SQLUser genoemd en in Hallo-domein bevinden.

## <a name="create-hello-odbc-connection-file"></a>Hallo ODBC-verbindingsbestand maken
Hallo algemene SQL-Connector maakt gebruik van ODBC-tooconnect toohello externe server. Eerst moet u een bestand met de Hallo ODBC-verbindingsgegevens toocreate.

1. Start Hallo ODBC-management-hulpprogramma op uw server:  
   ![ODBC](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc.png)
2. Selecteer Hallo tabblad **DSN-bestand**. Klik op **toevoegen...** .  
   ![ODBC1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc1.png)
3. Hallo out-of-box stuurprogramma werkt fijn, dus te selecteren en op **volgende >**.  
   ![ODBC2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc2.png)
4. Hallo-bestand, zoals een naam geven **GenericSQL**.  
   ![ODBC3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc3.png)
5. Klik op **Voltooien**.  
   ![ODBC4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc4.png)
6. Tijd tooconfigure Hallo verbinding. Hallo-gegevensbron een goede beschrijving geven en geef de naam Hallo van Hallo-server met SQL Server.  
   ![ODBC5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc5.png)
7. Selecteren hoe tooauthenticate met SQL. In dit geval gebruiken we Windows-verificatie.  
   ![ODBC6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc6.png)
8. Hallo-naam van de voorbeelddatabase Hallo **GSQLDEMO**.  
   ![ODBC7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc7.png)
9. Houd alles op dit scherm standaard. Klik op **Voltooien**.  
   ![ODBC8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc8.png)
10. tooverify alles werkt zoals verwacht, klikt u op **gegevensbron testen**.  
    ![ODBC9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc9.png)
11. Zorg ervoor dat het Hallo-test is geslaagd.  
    ![ODBC10](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc10.png)
12. Hallo ODBC-configuratiebestand worden nu weergegeven in de DSN-bestand.  
    ![ODBC11](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/odbc11.png)

We hebben nu Hallo bestand we moeten en kunt beginnen met het maken van Hallo Connector.

## <a name="create-hello-generic-sql-connector"></a>Hallo algemene SQL-Connector maken
1. Selecteer in de Hallo Synchronization Service Manager UI, **Connectors** en **maken**. Selecteer **algemene SQL (Microsoft)** en wijs hieraan een beschrijvende naam.  
   ![Connector1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector1.png)
2. Hallo u hebt gemaakt in de vorige sectie Hallo DSN-bestand vinden en upload het toohello-server. Hallo referenties tooconnect toohello database opgeven.  
   ![Connector2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector2.png)
3. In dit overzicht we zijn zodat u gemakkelijk voor ons en er zijn twee objecttypen spreken **gebruiker** en **groep**.
   ![Connector3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector3.png)
4. toofind hello kenmerken, willen we Hallo Connector toodetect die kenmerken door te kijken Hallo tabel zelf. Aangezien **gebruikers** is een gereserveerd woord in SQL, moeten we tooprovide in vierkante haakjes [].  
   ![Connector4](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector4.png)
5. Tijd toodefine hello ankerkenmerk en Hallo DN-kenmerk. Voor **gebruikers**, gebruiken we Hallo combinatie van Hallo twee kenmerken username en werknemer-id. Voor **groep**, gebruiken we GroupName (geen realistisch in de praktijk, maar voor dit scenario werkt).
   ![Connector5](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector5.png)
6. Niet alle kenmerktypen kunnen worden gedetecteerd in een SQL-database. kan met name Hallo kenmerk referentietype niet. Voor het objecttype Hallo-groep moeten we toochange Hallo OwnerID en MemberID tooreference.  
   ![Connector6](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector6.png)
7. Hallo kenmerken we geselecteerd als verwijzingskenmerken in de vorige stap Hallo Hallo objecttype dat u deze waarden een verwijzing naar zijn vereist. In ons geval Hallo objecttype van de gebruiker.  
   ![Connector7](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector7.png)
8. Selecteer op de pagina Hallo globale Parameters **watermerk** als Hallo delta-strategie. Ook in datum-/ tijdnotatie Hallo typen **jjjj-MM-dd: mm: SS**.
   ![Connector8](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector8.png)
9. Op Hallo **configureren partities en hiërarchieën** pagina, selecteert u beide objecttypen.
   ![Connector9](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/connector9.png)
10. Op Hallo **objecttypen selecteren** en **kenmerken selecteren**, objecttypen en alle kenmerken selecteren. Op Hallo **ankers configureren** pagina, klikt u op **voltooien**.

## <a name="create-run-profiles"></a>Uitvoeringsprofielen maken
1. Selecteer in de Hallo Synchronization Service Manager UI, **Connectors**, en **Uitvoeringsprofielen configureren**. Klik op **nieuw profiel**. We beginnen met **volledige Import**.  
   ![Runprofile1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile1.png)
2. Selecteer Hallo type **volledige Import (alleen Faseren)**.  
   ![Runprofile2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile2.png)
3. Selecteer Hallo partitie **OBJECT = gebruiker**.  
   ![Runprofile3](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile3.png)
4. Selecteer **tabel** en het type **[gebruikers]**. Schuif naar beneden toohello met meerdere waarden object type sectie en gegevens zoals in de volgende afbeelding Hallo Hallo invoeren. Selecteer **voltooien** toosave Hallo stap.  
   ![Runprofile4a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4a.png)  
   ![Runprofile4b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile4b.png)  
5. Selecteer **nieuwe stap**. Selecteer deze keer **OBJECT groep =**. Op de laatste pagina Hallo Hallo-configuratie zoals in de volgende afbeelding hello te gebruiken. Klik op **Voltooien**.  
   ![Runprofile5a](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5a.png)  
   ![Runprofile5b](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/runprofile5b.png)  
6. Optioneel: Als u wilt, kunt u extra profielen uitvoeren. Voor dit scenario alleen Hallo volledige Import wordt gebruikt.
7. Klik op **OK** uitvoeringsprofielen toofinish wijzigen.

## <a name="add-some-test-data-and-test-hello-import"></a>Sommige test gegevens en test Hallo importeren toevoegen
Voer enkele testgegevens in de voorbeelddatabase. Wanneer u klaar bent, selecteert u **uitvoeren** en **volledige import**.

Hier volgt een gebruiker met twee telefoonnummers en een groep met een aantal leden.  
![cs1](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs1.png)  
![CS2](./media/active-directory-aadconnectsync-connector-genericsql-step-by-step/cs2.png)  

## <a name="appendix-a"></a>Bijlage A
**Hallo voorbeelddatabase voor SQL-script toocreate**

```SQL
---Creating hello Database---------
Create Database GSQLDEMO
Go
-------Using hello Database-----------
Use [GSQLDEMO]
Go
-------------------------------------
USE [GSQLDEMO]
GO
/****** Object:  Table [dbo].[GroupMembers]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GroupMembers](
    [MemberID] [int] NOT NULL,
    [Group_ID] [int] NOT NULL
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[GROUPS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[GROUPS](
    [GroupID] [int] NOT NULL,
    [GROUPNAME] [nvarchar](200) NOT NULL,
    [DESCRIPTION] [nvarchar](200) NULL,
    [WATERMARK] [datetime] NULL,
    [OwnerID] [int] NULL,
PRIMARY KEY CLUSTERED
(
    [GroupID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
/****** Object:  Table [dbo].[USERPHONE]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
SET ANSI_PADDING ON
GO
CREATE TABLE [dbo].[USERPHONE](
    [USER_ID] [int] NULL,
    [Phone] [varchar](20) NULL
) ON [PRIMARY]

GO
SET ANSI_PADDING OFF
GO
/****** Object:  Table [dbo].[USERS]   ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[USERS](
    [USERID] [int] NOT NULL,
    [USERNAME] [nvarchar](200) NOT NULL,
    [FirstName] [nvarchar](100) NULL,
    [LastName] [nvarchar](100) NULL,
    [DisplayName] [nvarchar](100) NULL,
    [ACCOUNTDISABLED] [bit] NULL,
    [EMPLOYEEID] [int] NOT NULL,
    [WATERMARK] [datetime] NULL,
PRIMARY KEY CLUSTERED
(
    [USERID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_GROUPS] FOREIGN KEY([Group_ID])
REFERENCES [dbo].[GROUPS] ([GroupID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_GROUPS]
GO
ALTER TABLE [dbo].[GroupMembers]  WITH CHECK ADD  CONSTRAINT [FK_GroupMembers_USERS] FOREIGN KEY([MemberID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GroupMembers] CHECK CONSTRAINT [FK_GroupMembers_USERS]
GO
ALTER TABLE [dbo].[GROUPS]  WITH CHECK ADD  CONSTRAINT [FK_GROUPS_USERS] FOREIGN KEY([OwnerID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[GROUPS] CHECK CONSTRAINT [FK_GROUPS_USERS]
GO
ALTER TABLE [dbo].[USERPHONE]  WITH CHECK ADD  CONSTRAINT [FK_USERPHONE_USER] FOREIGN KEY([USER_ID])
REFERENCES [dbo].[USERS] ([USERID])
GO
ALTER TABLE [dbo].[USERPHONE] CHECK CONSTRAINT [FK_USERPHONE_USER]
GO
```

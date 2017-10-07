---
title: aaaAuthentication en gebruikersmachtigingen in Azure Analysis Services | Microsoft Docs
description: Meer informatie over verificatie en gebruikersmachtigingen in Azure Analysis Services.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: dd49fd59eec1f68dfe8a0fe373fa612ac46de4e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-user-permissions"></a>Verificatie en gebruikersmachtigingen
Azure Analysis Services gebruikt Azure Active Directory (Azure AD) voor identity management- en gebruikersverificatie. Een gebruiker maken, beheren of verbinding maken met tooan Azure Analysis Services server moet hebben een geldige gebruikers-id in een [Azure AD-tenant](../active-directory/active-directory-administer.md) in Hallo hetzelfde abonnement.

Azure Analysis Services ondersteunt [Azure AD B2B-samenwerking](../active-directory/active-directory-b2b-what-is-azure-ad-b2b.md). Met B2B, kunnen gebruikers van buiten een organisatie worden uitgenodigd als gastgebruikers in een Azure Active directory. Gasten kunnen afkomstig zijn uit een andere Azure AD-tenant directory of een geldig e-mailadres. Eenmaal uitgenodigd en Hallo gebruiker accepteert Hallo uitnodiging verzonden via e-mail van Azure, hello gebruikersidentiteit toohello tenantmap wordt toegevoegd. Deze identiteiten kunnen vervolgens worden toegevoegd toosecurity groepen of als leden van een server-rol van systeembeheerder of de database.

![Authenticatie-architectuur van Azure Analysis Services](./media/analysis-services-manage-users/aas-manage-users-arch.png)

## <a name="authentication"></a>Authentication
Alle client-toepassingen en hulpprogramma's gebruiken een of meer van de Analysis Services Hallo [clientbibliotheken](analysis-services-data-providers.md) (AMO MSOLAP, ADOMD) tooconnect tooa server. 

Alle drie clientbibliotheken ondersteuning voor Azure AD interactieve stroom en niet-interactieve verificatiemethoden. Hallo twee niet-interactieve methoden, Active Directory-wachtwoord en geïntegreerde verificatie van Active Directory-methoden kunnen worden gebruikt in toepassingen die gebruikmaken van AMOMD en MSOLAP. Deze twee methoden worden nooit leiden tot pop-dialoogvensters.

Clienttoepassingen, zoals Excel en Power BI Desktop en hulpmiddelen zoals SSMS en SSDT installeren de nieuwste versies Hallo Hallo bibliotheken wanneer bijgewerkt met de meest recente versie toohello. Power BI Desktop SSMS en SSDT maandelijks bijgewerkt. Is Excel [bijgewerkt met Office 365](https://support.office.com/en-us/article/When-do-I-get-the-newest-features-in-Office-2016-for-Office-365-da36192c-58b9-4bc9-8d51-bb6eed468516). Office 365-updates zijn minder frequente en sommige organisaties gebruiken Hallo uitgestelde kanaal, betekenis updates up toothree maanden worden uitgesteld.

 Afhankelijk van de client-toepassing hello of hulpprogramma waarmee u kan Hallo type verificatie en hoe u zich aanmeldt afwijken. Elke toepassing kan verschillende functies die ondersteuning voor het verbinden van toocloud services zoals Azure Analysis Services.


### <a name="sql-server-management-studio-ssms"></a>SQL Server Management Studio (SSMS)
Azure Analysis Services-servers ondersteunen verbindingen van [SSMS V17.1](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) en hoger met behulp van Windows-verificatie, Active Directory-wachtwoordverificatie en universele verificatie van Active Directory. In het algemeen kunt dat u Active Directory-Universal-verificatie gebruiken, omdat:

*  Biedt ondersteuning voor interactieve en niet-interactieve verificatiemethoden.

*  Biedt ondersteuning voor Azure B2B gastgebruikers uitgenodigd in Hallo AS Azure-tenant. Wanneer tooa server verbinding kunnen maken, moeten gastgebruikers Universal verificatie van Active Directory selecteren wanneer toohello server verbinding kunnen maken.

*  Biedt ondersteuning voor multi-factor Authentication (MFA). Azure MFA helpt beveiliging toegang toodata en toepassingen met een aantal opties voor verificatie: telefoonoproep, tekstbericht, smartcards en pincode of mobiele app-melding. Interactieve MFA met Azure AD kan resulteren in een pop-dialoogvenster voor validatie.

### <a name="sql-server-data-tools-ssdt"></a>SQL Server Data Tools (SSDT)
SSDT verbindt tooAzure Analysis Services met behulp van Active Directory-Universal-verificatie met MFA-ondersteuning. Gebruikers zijn na vragen aan gebruiker toosign in tooAzure bij de eerste implementatie Hallo met behulp van hun organisatie-ID (e-mail). Gebruikers moeten zich aanmelden tooAzure met een account met administrator-machtigingen voor server op Hallo server die ze implementeert. Als u zich eerst aanmeldt tooAzure hello, is een token toegewezen. SSDT caches Hallo token in het geheugen voor toekomstige aantal hersteld.

### <a name="power-bi-desktop"></a>Power BI Desktop
Power BI Desktop verbindt tooAzure Analysis Services met behulp van Active Directory-Universal-verificatie met ondersteuning voor MFA. Gebruikers zijn na vragen aan gebruiker toosign in tooAzure op Hallo eerste verbinding met behulp van hun organisatie-ID (e-mail). Gebruikers moeten zich aanmelden tooAzure met een account dat is opgenomen in een serverbeheerder of een databaserol.

### <a name="excel"></a>Excel
Excel-gebruikers kunnen tooa server verbinding via een Windows-account, een organisatie-ID (e-mailadres) of een externe e-mailadres. Externe e-identiteiten moeten in hello Azure AD als gastgebruiker bestaan.

## <a name="user-permissions"></a>Gebruikersmachtigingen

**Serverbeheerders** zijn specifieke tooan Azure Analysis Services-serverexemplaar. Ze verbinden met de hulpprogramma's zoals Azure-portal, SSMS en SSDT tooperform taken zoals het toevoegen van databases en gebruikersrollen beheren. Hallo-gebruiker die het Hallo-server maakt wordt standaard automatisch toegevoegd als een Analysis Services-server-beheerder. Andere beheerders kunnen met behulp van Azure-portal of SSMS worden toegevoegd. Serverbeheerders moeten een account hebben in hello Azure AD-tenant in Hallo hetzelfde abonnement. toolearn meer, Zie [serverbeheerders beheren](analysis-services-server-admins.md). 


**Gebruikers van de database** toomodel databases verbinding met behulp van client-toepassingen zoals Excel of Power BI. Gebruikers moeten worden toegevoegd als toodatabase rollen. Databaserollen definiëren administrator, proces of leesmachtigingen voor een database. Het is belangrijk toounderstand databasegebruikers met een rol met beheerdermachtigingen is anders dan serverbeheerders. Standaard zijn serverbeheerders echter ook databasebeheerders. toolearn meer, Zie [databaserollen en gebruikers beheren](analysis-services-database-users.md).

**Azure-resource eigenaars**. Resource-eigenaars beheren resources voor een Azure-abonnement. Resource-eigenaars kunnen toevoegen Inzender rollen of Azure AD-gebruiker identiteiten tooOwner binnen een abonnement met **toegangsbeheer** in Azure portal of met Azure Resource Manager-sjablonen. 

![Toegangsbeheer in Azure-portal](./media/analysis-services-manage-users/aas-manage-users-rbac.png)

Rollen op dit niveau toepassen toousers of accounts die tooperform taken die kunnen worden voltooid in Hallo portal of met behulp van Azure Resource Manager-sjablonen moeten. toolearn meer, Zie [toegangsbeheer op basis van rollen](../active-directory/role-based-access-control-what-is.md). 


## <a name="database-roles"></a>Databaserollen

 Rollen die zijn gedefinieerd voor een model in tabelvorm zijn databaserollen. Dat wil zeggen, Hallo rollen bevatten leden die bestaan uit Azure AD-gebruikers en beveiligingsgroepen die specifieke machtigingen die Hallo actie definieert hebben die leden kunnen uitvoeren op een modeldatabase. Een databaserol wordt gemaakt als een afzonderlijk object in de database Hallo en geldt alleen toohello-database waarin die rol is gemaakt.   
  
 Standaard bij het maken van een nieuw project voor het model in tabelvorm heeft Hallo modelproject geen rollen. Rollen kunnen worden gedefinieerd met behulp van Hallo Role Manager-dialoogvenster in SSDT. Wanneer er rollen zijn gedefinieerd tijdens het modelontwerp project, zijn ze toegepaste alleen toohello werkruimte modeldatabase. Wanneer Hallo model wordt geïmplementeerd, zijn hello dezelfde rollen toegepaste toohello geïmplementeerd model. Nadat een model is geïmplementeerd, server en databasebeheerders kunnen rollen en leden beheren met behulp van SSMS. toolearn meer, Zie [databaserollen en gebruikers beheren](analysis-services-database-users.md).
  


## <a name="next-steps"></a>Volgende stappen

[Tooresources toegang beheren met Azure Active Directory-groepen](../active-directory/active-directory-manage-groups.md)   
[Databaserollen en gebruikers beheren](analysis-services-database-users.md)  
[Serverbeheerders beheren](analysis-services-server-admins.md)  
[Op rollen gebaseerd toegangsbeheer](../active-directory/role-based-access-control-what-is.md)  
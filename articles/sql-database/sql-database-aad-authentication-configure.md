---
title: verificatie van aaaConfigure Azure Active Directory - SQL | Microsoft Docs
description: Meer informatie over hoe tooconnect tooSQL Database en SQL Data Warehouse met behulp van Azure Active Directory-verificatie.
services: sql-database
documentationcenter: 
author: BYHAM
manager: jhubbard
editor: 
tags: 
ms.assetid: 7e2508a1-347e-4f15-b060-d46602c5ce7e
ms.service: sql-database
ms.custom: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/10/2017
ms.author: rickbyh
ms.openlocfilehash: d6222da0b840f96d4bcfbc02964dc7c54d5ea1ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-manage-azure-active-directory-authentication-with-sql-database-or-sql-data-warehouse"></a>Configureren en beheren van Azure Active Directory-verificatie met SQL-Database of SQL Data Warehouse

Dit artikel ziet u hoe toocreate en Azure AD te vullen en vervolgens Azure AD te gebruiken met Azure SQL Database en SQL Data Warehouse. Zie voor een overzicht [Azure Active Directory-verificatie](sql-database-aad-authentication.md).

>  [!NOTE]  
>  Verbinding maken met tooSQL-Server op een virtuele machine in Azure wordt niet ondersteund met een Azure Active Directory-account. Gebruik in plaats daarvan de Active Directory-account van een domein.

## <a name="create-and-populate-an-azure-ad"></a>U maakt en vult u een Azure AD
Maak een Azure AD en deze vullen met gebruikers en groepen. Azure AD kan worden beheerd Hallo eerste domein Azure AD-domein. Azure AD kan ook worden voor een lokale Active Directory Domain Services die met hello Azure AD is gefedereerd.

Zie voor meer informatie [uw on-premises identiteiten integreren met Azure Active Directory](../active-directory/active-directory-aadconnect.md), [toevoegen van uw eigen domein naam tooAzure AD](../active-directory/active-directory-add-domain.md), [Microsoft Azure biedt nu ondersteuning voor federatie met Windows Server Active Directory](https://azure.microsoft.com/blog/2012/11/28/windows-azure-now-supports-federation-with-windows-server-active-directory/), [beheer van uw Azure AD-directory](https://msdn.microsoft.com/library/azure/hh967611.aspx), [beheren Azure AD dat gebruikmaakt van Windows PowerShell](/powershell/azure/overview?view=azureadps-2.0), en [hybride identiteit Vereiste poorten en protocollen](../active-directory/active-directory-aadconnect-ports.md).

## <a name="optional-associate-or-change-hello-active-directory-that-is-currently-associated-with-your-azure-subscription"></a>Optioneel: Koppelen of Hallo active directory die is gekoppeld aan uw Azure-abonnement wijzigen
tooassociate uw database met hello Azure AD-directory voor uw organisatie Hallo directory een vertrouwde map maken voor database Hallo hosting van hello Azure-abonnement. Zie [Hoe Azure-abonnementen worden gekoppeld aan Azure AD](https://msdn.microsoft.com/library/azure/dn629581.aspx) voor meer informatie.

**Aanvullende informatie:** om Azure-abonnement heeft een vertrouwensrelatie met een Azure AD-exemplaar. Dit betekent dat dat tooauthenticate directory wordt vertrouwd gebruikers, services en apparaten. Meerdere abonnementen kunnen vertrouwen, Hallo dezelfde map, maar een abonnement vertrouwt slechts één directory. U kunt zien welke directory wordt vertrouwd door uw abonnement onder Hallo **instellingen** tab aan [https://manage.windowsazure.com/](https://manage.windowsazure.com/). Er is een vertrouwensrelatie die een abonnement met een map heeft in tegenstelling tot Hallo-relatie die een abonnement heeft met alle andere resources in Azure (websites, databases, enzovoort), die meer op onderliggende resources van een abonnement lijken. Als er een abonnement is verlopen, toegang tot toothose andere resources zijn gekoppeld Hallo abonnement ook geblokkeerd. Maar Hallo directory blijft in Azure, en u kunt een ander abonnement koppelen aan die directory en doorgaan toomanage Hallo directory-gebruikers. Zie voor meer informatie over bronnen [informatie over toegang tot bronnen in Azure](https://msdn.microsoft.com/library/azure/dn584083.aspx).

Hallo volgende procedures wordt uitgelegd hoe toochange Hallo directory voor een bepaald abonnement gekoppeld.
1. Verbinding maken met tooyour [klassieke Azure-Portal](https://manage.windowsazure.com/) met behulp van Azure-abonnementbeheerder.
2. Selecteer op de links banner hello, **instellingen**.
3. Uw abonnementen weergegeven in het welkomstscherm van de instellingen. Als Hallo abonnement niet wordt weergegeven gewenst, klikt u op **abonnementen** vervolgkeuzelijst bovenaan Hallo Hallo **FILTER door DIRECTORY** vak en klik vervolgens op Hallo directory selecteren die uw abonnementen bevat **Toepassen**.
   
    ![Abonnement selecteren][4]
4. In Hallo **instellingen** gebied, klikt u op uw abonnement en klik vervolgens op **DIRECTORY bewerken** Hallo Hallo pagina onderaan in.
   
    ![AD-instellingen-portal][5]
5. In Hallo **DIRECTORY bewerken** vak en klik vervolgens op de pijl Hallo voor volgende Selecteer hello Azure Active Directory die is gekoppeld aan uw SQL Server of SQL Data Warehouse.
   
    ![bewerken-directory-selecteren][6]
6. In Hallo **bevestigen** directory dialoogvenster toewijzing, Controleer of '**alle medebeheerders wordt verwijderd.**'
   
    ![bewerken directory bevestigen][7]
7. Klik op Hallo selectievakje tooreload Hallo-portal.

   > [!NOTE]
   > Wanneer u wijzigt Hallo directory, toegang tooall medebeheerders, Azure AD-gebruikers en groepen en gebruikers van de map back-resource worden verwijderd en ze niet langer toegang toothis abonnement of de bijbehorende bronnen hebben. Alleen kunt, als servicebeheerder u toegang voor principals die zijn gebaseerd op Hallo nieuwe map. Deze wijziging kan duren voordat een aanzienlijke hoeveelheid tijd toopropagate tooall resources. Hallo-map wordt gewijzigd, ook wijzigingen hello Azure AD-beheerder voor SQL-Database en SQL Data Warehouse en weigeren van toegang tot de database voor een bestaande Azure AD-gebruikers. Azure AD Hallo beheerder moet het opnieuw instellen (zoals hieronder wordt beschreven) en nieuwe Azure AD-gebruikers moeten worden gemaakt.
   >  

## <a name="create-an-azure-ad-administrator-for-azure-sql-server"></a>Een Azure AD-beheerder voor Azure SQL-server maken
Elke Azure SQL-server (die als host fungeert voor een SQL-Database of SQL Data Warehouse) begint met een administrator-account voor één server Hallo beheerder van Hallo gehele Azure SQL-server. Een tweede SQL Server-beheerder moet worden gemaakt, die een Azure AD-account. Deze principal is gemaakt als de gebruiker van een ingesloten database in de hoofddatabase Hallo. Als beheerder, beheerdersaccounts Hallo-server lid zijn van Hallo **db_owner** rol in elke gebruiker database en de database van elke gebruiker in te voeren als Hallo **dbo** gebruiker. Zie voor meer informatie over beheerdersaccounts Hallo-server, [het beheren van Databases en aanmeldingen in Azure SQL Database](sql-database-manage-logins.md).

Als u Azure Active Directory met geo-replicatie, moet hello Azure Active Directory-beheerder voor Hallo primaire en secundaire servers Hallo worden geconfigureerd. Als een server een Azure Active Directory-beheerder niet beschikt, vervolgens Azure Active Directory-aanmeldingen en gebruikers ontvangen een tooserver 'Kan geen verbinding maken' fout.

> [!NOTE]
> Gebruikers die niet zijn gebaseerd op een Azure AD-account (inclusief hello Azure SQL server-administratoraccount), kan Azure AD-gebruikers, maken, omdat ze geen machtiging toovalidate voorgestelde databasegebruikers Hello Azure AD.
> 

## <a name="provision-an-azure-active-directory-administrator-for-your-azure-sql-server"></a>Een Azure Active Directory-beheerder voor uw Azure SQL-server inrichten

Hallo volgende twee procedures laten zien hoe u een Azure Active Directory-beheerder voor uw Azure SQL-server in hello Azure-portal en met behulp van PowerShell tooprovision.

### <a name="azure-portal"></a>Azure Portal
1. In Hallo [Azure-portal](https://portal.azure.com/), rechterbovenhoek Hallo in, klikt u op uw verbinding toodrop omlaag in een lijst met mogelijke Active Directory's. Kies Hallo corrigeren van Active Directory als Hallo standaard Azure AD. Deze stap koppelingen Hallo abonnement koppeling met Active Directory met Azure SQL-server om ervoor te zorgen dat hetzelfde abonnement Hallo wordt gebruikt voor zowel Azure AD en SQL Server. (hello Azure SQL-server kan worden gehost, Azure SQL Database of Azure SQL Data Warehouse.)   
    ![Kies ad][8]   
    
2. In de banner Selecteer links Hallo **SQL-servers**, selecteer uw **SQL server**, en klik vervolgens in Hallo **SQL Server** blade klikt u op **Active Directory-beheerder**.   
3. In Hallo **Active Directory-beheerder** blade, klikt u op **beheerder instellen**.   
    ![Selecteer active directory](./media/sql-database-aad-authentication/select-active-directory.png)  
    
4. In Hallo **admin toevoegen** blade voor een gebruiker, selecteer Hallo gebruiker of groep toobe beheerder zoeken en klik vervolgens op **Selecteer**. (Hallo Active Directory-beheerder blade ziet u alle leden en groepen van Active Directory. Gebruikers of groepen die grijs worden weergegeven, kunnen niet worden geselecteerd omdat ze worden niet ondersteund als Azure AD-beheerders. (Zie Hallo lijst met ondersteunde beheerders in Hallo **Azure AD-functies en beperkingen** sectie van [Azure Active Directory-verificatie gebruiken voor verificatie bij SQL-Database of SQL Data Warehouse](sql-database-aad-authentication.md).) Op rollen gebaseerde toegangsbeheer (RBAC) geldt alleen toohello portal en is niet doorgegeven tooSQL Server.   
    ![Selecteer beheerder](./media/sql-database-aad-authentication/select-admin.png)  
    
5. Hallo boven aan het Hallo **Active Directory-beheerder** blade, klikt u op **opslaan**.   
    ![beheerder opslaan](./media/sql-database-aad-authentication/save-admin.png)   

Hallo-proces van het wijzigen van Hallo beheerder kan enkele minuten duren. En vervolgens nieuwe beheerder hello wordt weergegeven in Hallo **Active Directory-beheerder** vak.

   > [!NOTE]
   > Bij het instellen van Azure AD Hallo beheerder, kan niet Hallo nieuwe naam van de serverbeheerder (gebruiker of groep) al aanwezig zijn in virtuele hoofddatabase Hallo als de gebruiker van een SQL Server-verificatie. Indien aanwezig, mislukt de installatie van hello Azure AD-beheerder; het maken ervan worden teruggedraaid en waarmee wordt aangegeven dat deze een beheerder (naam) al bestaat. Omdat deze een SQL Server authentication-gebruiker geen deel uit van hello Azure AD maakt, wordt elke inspanning tooconnect toohello server met behulp van Azure AD-verificatie mislukt.
   > 


toolater verwijdert u een beheerder, boven Hallo Hallo **Active Directory-beheerder** blade, klikt u op **admin verwijderen**, en klik vervolgens op **opslaan**.

### <a name="powershell"></a>PowerShell
toorun PowerShell-cmdlets, moet u toohave Azure PowerShell is geïnstalleerd en uitgevoerd. Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

een Azure AD-beheerder tooprovision uitvoeren hello Azure PowerShell-opdrachten te volgen:

* Add-AzureRmAccount
* SELECT-AzureRmSubscription

Cmdlets tooprovision gebruikt en beheren van Azure AD-beheerder:

| Naam van cmdlet | Beschrijving |
| --- | --- |
| [Set-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/set-azurermsqlserveractivedirectoryadministrator) |Voorziet in een Azure Active Directory-beheerder voor Azure SQL-server of Azure SQL Data Warehouse. (Moet uit het huidige abonnement Hallo.) |
| [Verwijder AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/remove-azurermsqlserveractivedirectoryadministrator) |Hiermee verwijdert u een Azure Active Directory-beheerder voor Azure SQL-server of Azure SQL Data Warehouse. |
| [Get-AzureRmSqlServerActiveDirectoryAdministrator](/powershell/module/azurerm.sql/get-azurermsqlserveractivedirectoryadministrator) |Retourneert informatie over een Azure Active Directory-beheerder die momenteel zijn geconfigureerd voor hello Azure SQL-server of Azure SQL Data Warehouse. |

Gebruik PowerShell-opdracht get-help toosee meer gedetailleerde informatie over elk van deze opdrachten, bijvoorbeeld ``get-help Set-AzureRmSqlServerActiveDirectoryAdministrator``.

Hallo met het volgende script bepalingen beheerder Azure AD-groep met de naam **DBA_Group** (object-id `40b79501-b343-44ed-9ce7-da4c8cc7353f`) voor Hallo **demo_server** server in een resourcegroep met de naam **groep 23** :

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group"
```

Hallo **DisplayName** invoerparameter accepteert weergavenaam hello Azure AD of Hallo principalnaam van gebruiker. Bijvoorbeeld: ``DisplayName="John Smith"`` en ``DisplayName="johns@contoso.com"``. Voor Azure AD-groepen alleen hello Azure AD wordt weergavenaam ondersteund.

> [!NOTE]
> Hello Azure PowerShell-opdracht ```Set-AzureRmSqlServerActiveDirectoryAdministrator``` voorkomt niet dat u Azure AD-beheerders voor niet-ondersteunde gebruikers inrichten. Een niet-ondersteunde gebruiker kan worden ingericht, maar kan geen verbinding maken met tooa-database. 
> 

Hallo volgende voorbeeld wordt optioneel Hallo **ObjectID**:

```
Set-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23"
-ServerName "demo_server" -DisplayName "DBA_Group" -ObjectId "40b79501-b343-44ed-9ce7-da4c8cc7353f"
```

> [!NOTE]
> Hello Azure AD **ObjectID** is vereist wanneer hello **DisplayName** is niet uniek. Hallo tooretrieve **ObjectID** en **DisplayName** waarden, gebruik Hallo Active Directory-sectie van de klassieke Azure-Portal en Hallo eigenschappen van een gebruiker of groep weergeven.
> 

Hallo volgende voorbeeld retourneert informatie over Hallo huidige Azure AD-beheerder voor Azure SQL-server:

```
Get-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server" | Format-List
```

Hallo volgende voorbeeld wordt een Azure AD-beheerder verwijderd.

```
Remove-AzureRmSqlServerActiveDirectoryAdministrator -ResourceGroupName "Group-23" -ServerName "demo_server"
```

U kunt ook een Azure Active Directory-beheerder inrichten met behulp van Hallo REST-API's. Zie voor meer informatie [Service Management REST API-verwijzing en bewerkingen voor Azure SQL-Databases bewerkingen voor Azure SQL-Databases](https://msdn.microsoft.com/library/azure/dn505719.aspx)

### <a name="cli"></a>CLI  
U kunt ook een Azure AD-beheerder inrichten door de aanroepende Hallo CLI-opdrachten te volgen:
| Opdracht | Beschrijving |
| --- | --- |
|[AZ sql server ad-beheerder maken](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#create) |Voorziet in een Azure Active Directory-beheerder voor Azure SQL-server of Azure SQL Data Warehouse. (Moet uit het huidige abonnement Hallo.) |
|[AZ sql server ad-beheerder verwijderen](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#delete) |Hiermee verwijdert u een Azure Active Directory-beheerder voor Azure SQL-server of Azure SQL Data Warehouse. |
|[lijst met AZ sql server ad-beheerder](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#list) |Retourneert informatie over een Azure Active Directory-beheerder die momenteel zijn geconfigureerd voor hello Azure SQL-server of Azure SQL Data Warehouse. |
|[update van AZ sql server ad-beheerder](https://docs.microsoft.com/cli/azure/sql/server/ad-admin#update) |Hallo Active Directory-beheerder voor een Azure SQL-server of Azure SQL Data Warehouse-updates. |

Zie voor meer informatie over de CLI-opdrachten, [SQL - az sql](https://docs.microsoft.com/cli/azure/sql/server).  


## <a name="configure-your-client-computers"></a>De clientcomputers configureren
U moet Hallo volgende software installeren op alle clientcomputers waarvan uw toepassingen of gebruikers verbinding maken met tooAzure SQL-Database of Azure SQL Data Warehouse met behulp van Azure AD-identiteiten:

* .NET framework 4.6 of hoger van [https://msdn.microsoft.com/library/5a4x27ek.aspx](https://msdn.microsoft.com/library/5a4x27ek.aspx).
* Azure Active Directory Authentication Library voor SQL Server (**ADALSQL. DLL-bestand**) is beschikbaar in meerdere talen (x x86- en amd64) van Downloadcentrum Hallo op [Microsoft Active Directory Authentication Library voor Microsoft SQL Server](http://www.microsoft.com/download/details.aspx?id=48742).

U kunt voldoen aan deze voorwaarden voldoet:

* Één installeert [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) of [SQL Server Data Tools voor Visual Studio 2015](https://msdn.microsoft.com/library/mt204009.aspx) voldoet aan de vereiste .NET Framework 4.6 Hallo.
* SSMS installeert Hallo x86 versie van **ADALSQL. DLL-bestand**.
* Hallo amd64-versie van SSDT is geïnstalleerd **ADALSQL. DLL-bestand**.
* Hallo meest recente Visual Studio van [Visual Studio-Downloads](https://www.visualstudio.com/downloads/download-visual-studio-vs) voldoet aan de vereisten Hallo .NET Framework 4.6, maar niet geïnstalleerd Hallo vereist amd64-versie van **ADALSQL. DLL-bestand**.

## <a name="create-contained-database-users-in-your-database-mapped-tooazure-ad-identities"></a>Ingesloten databasegebruikers in uw database toegewezen tooAzure AD identiteiten maken

Azure Active Directory-verificatie vereist database gebruikers toobe gemaakt als ingesloten databasegebruikers. Een ingesloten database-gebruiker op basis van een Azure AD-identiteit is een databasegebruiker die geen een aanmelding in de hoofddatabase Hallo en welke identiteit maps tooan in Azure AD-directory die is gekoppeld aan de database Hallo Hallo. Hello Azure AD identity mag een afzonderlijk gebruikersaccount of een groep. Zie voor meer informatie over ingesloten databasegebruikers [opgenomen databasegebruikers maken uw Database draagbare](https://msdn.microsoft.com/library/ff929188.aspx).

> [!NOTE]
> Database-gebruikers (met uitzondering van Hallo van beheerders) kunnen niet worden gemaakt met behulp van de portal. RBAC-rollen zijn niet doorgegeven tooSQL Server, SQL-Database of SQL Data Warehouse. Azure RBAC-rollen worden gebruikt voor het beheren van Azure-Resources en toodatabase machtigingen niet toepassen. Bijvoorbeeld, Hallo **SQL Server Inzender** rol verleent geen toegang tot tooconnect toohello SQL-Database of SQL Data Warehouse. Hallo-machtiging moet rechtstreeks in Hallo-database met behulp van Transact-SQL-instructies worden toegekend.
>

een Azure AD gebaseerde opgenomen databasegebruiker (met uitzondering van Hallo serverbeheerder die eigenaar is van de database Hallo), verbinding toohello database maken met een Azure AD-identiteit als een gebruiker met toocreate ten minste Hallo **elke gebruiker ALTER** machtiging. Gebruik vervolgens Hallo Transact-SQL-syntaxis:

```
CREATE USER <Azure_AD_principal_name> FROM EXTERNAL PROVIDER;
```

*Azure_AD_principal_name* Hallo principal-naam van een Azure AD gebruiker of Hallo weergavenaam voor een Azure AD-groep kan worden.

**Voorbeelden:** toocreate een ingesloten database-gebruiker voor een Azure AD federatief of beheerd domeingebruiker:
```
CREATE USER [bob@contoso.com] FROM EXTERNAL PROVIDER;
CREATE USER [alice@fabrikam.onmicrosoft.com] FROM EXTERNAL PROVIDER;
```

toocreate een ingesloten database-gebruiker die een Azure AD of federatieve domeingroep, bieden Hallo weergegeven naam van een beveiligingsgroep:
```
CREATE USER [ICU Nurses] FROM EXTERNAL PROVIDER;
```

een ingesloten database-gebruiker die een toepassing die verbinding maakt met behulp van een Azure AD-token toocreate:

```
CREATE USER [appName] FROM EXTERNAL PROVIDER;
```

>  [!TIP]
>  U kunt een gebruiker rechtstreeks vanuit een Azure Active Directory dan hello Azure Active Directory die is gekoppeld aan uw Azure-abonnement maken. Echter leden van andere Active Directory's die geïmporteerde gebruikers in Hallo zijn gekoppeld in Active Directory (ook wel externe gebruikers) kan tooan Active Directory-groep worden toegevoegd in Hallo tenant Active Directory. Door het maken van een ingesloten database-gebruiker voor de groep AD hello gebruikers van Hallo externe Active Directory kunnen krijgen toegang tooSQL Database.   

Voor meer informatie over het maken van die gebruikers op basis van identiteiten met Azure Active Directory-database, raadpleegt u [gebruiker maken (Transact-SQL)](http://msdn.microsoft.com/library/ms173463.aspx).

> [!NOTE]
> Verwijderen hello Azure Active Directory-beheerder voor Azure SQL-server wordt voorkomen dat een Azure AD authentication-gebruiker toohello server verbinding kunnen maken. Indien nodig, onbruikbaar Azure AD-gebruikers kunnen handmatig worden verwijderd door de beheerder van een SQL-Database.   

>  [!NOTE]
>  Als u krijgt een **verbinding time-out verstreken**, moet u mogelijk tooset hello `TransparentNetworkIPResolution` parameter van Hallo connection string toofalse. Zie voor meer informatie [time-out verbindingsprobleem met .NET Framework 4.6.1 - wordt met TransparentNetworkIPResolution](https://blogs.msdn.microsoft.com/dataaccesstechnologies/2016/05/07/connection-timeout-issue-with-net-framework-4-6-1-transparentnetworkipresolution/).   

   
Wanneer u een databasegebruiker maakt, krijgt die gebruiker het Hallo **CONNECT** machtiging en verbinding maken met toothat-database als lid van Hallo **openbare** rol. In eerste instantie Hallo alleen machtigingen voor gebruiker beschikbaar toohello worden machtigingen verleend toohello **openbare** rollen of machtigingen die tooany Windows-groepen die ze lid zijn van zijn. Zodra u een Azure AD gebaseerde opgenomen databasegebruiker inricht, kunt u Hallo gebruiker aanvullende machtigingen verlenen Hallo u dezelfde manier als u andere type gebruiker tooany machtiging verlenen. Doorgaans machtigingen verlenen toodatabase rollen en gebruikers tooroles toevoegen. Zie voor meer informatie [Database-Engine machtiging Basics](http://social.technet.microsoft.com/wiki/contents/articles/4433.database-engine-permission-basics.aspx). Zie voor meer informatie over specifieke functies van de SQL-Database, [het beheren van Databases en aanmeldingen in Azure SQL Database](sql-database-manage-logins.md).
Een federatieve gebruiker die is geïmporteerd in een domein beheren moet Hallo beheerd domein identiteit gebruiken.

> [!NOTE]
> Azure AD-gebruikers zijn gemarkeerd in de metagegevens van de database Hallo met het type E (EXTERNAL_USER) en voor groepen met type X (EXTERNAL_GROUPS). Zie voor meer informatie [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx). 
>

## <a name="connect-toohello-user-database-or-data-warehouse-by-using-ssms-or-ssdt"></a>Verbinding maken met toohello gebruiker database of de data warehouse met behulp van SSMS of SSDT  
tooconfirm hello Azure AD-beheerder correct is ingesteld, wordt verbinding gemaakt toohello **master** database met de administrator-account hello Azure AD.
toohello database tooprovision een Azure AD gebaseerde opgenomen databasegebruiker (met uitzondering van Hallo serverbeheerder die eigenaar is van de database Hallo), verbinding met een Azure AD-identiteit die toegang toohello database heeft.

> [!IMPORTANT]
> Ondersteuning voor Azure Active Directory-verificatie is beschikbaar met [SQL Server 2016 Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) en [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) in Visual Studio 2015. Hallo augustus 2016-versie van SSMS biedt ook ondersteuning voor universele verificatie van Active Directory, zodat beheerders toorequire multi-factor Authentication met behulp van een telefoongesprek, tekstbericht, smartcards met pincode of mobiele app-melding.
 
## <a name="using-an-azure-ad-identity-tooconnect-using-ssms-or-ssdt"></a>Met behulp van een Azure AD identity tooconnect met behulp van SSMS of SSDT  

Hallo volgende procedures laten zien hoe tooconnect tooa SQL-database met een Azure AD-identiteit met behulp van SQL Server Management Studio of SQL Server-Database Tools.

### <a name="active-directory-integrated-authentication"></a>Geïntegreerde verificatie van Active Directory

Gebruik deze methode als u bent aangemeld met uw Azure Active Directory-referenties van een federatieve domein tooWindows.

1. Start Management Studio of Data Tools en in Hallo **tooServer verbinding** (of **tooDatabase Engine verbinding**) in het dialoogvenster in Hallo **verificatie** Selecteer **Geïntegreerd met active Directory -**. Er is geen wachtwoord nodig is of omdat de referenties van uw bestaande voor Hallo verbinding krijgt kan worden ingevoerd.   

    ![Selecteer AD-geïntegreerde verificatie][11]
2. Klikt u op Hallo **opties** knop, en op Hallo **verbindingseigenschappen** pagina in Hallo **toodatabase verbinding** vak, Hallo typenaam van de gebruikersdatabase Hallo gewenste tooconnect Aan. (Hallo **AD-domein naam of het tenant-ID**' optie wordt alleen ondersteund voor **Universal met MFA verbinding** opties, anders het wordt grijs.)  

    ![Selecteer de databasenaam Hallo][13]

## <a name="active-directory-password-authentication"></a>Active Directory-wachtwoordverificatie

Gebruik deze methode wanneer u verbinding maakt met een Azure AD principal-naam met behulp van Azure AD Hallo beheerd domein. U kunt deze ook gebruiken voor federatieve account zonder toegang toohello domein, bijvoorbeeld bij het op afstand werkt.

Gebruik deze methode als u tooWindows met referenties van een domein dat niet is gefedereerd met Azure bent aangemeld, of wanneer u Azure AD-verificatie met Azure AD op basis van de eerste Hallo of Hallo van clientdomein.

1. Start Management Studio of Data Tools en in Hallo **tooServer verbinding** (of **tooDatabase Engine verbinding**) in het dialoogvenster in Hallo **verificatie** Selecteer **Active Directory - wachtwoord**.
2. In Hallo **gebruikersnaam** typt u de naam van uw Azure Active Directory-gebruiker in de indeling Hallo  **username@domain.com** . Dit moet een account van hello Azure Active Directory of een account van een domein federeren met hello Azure Active Directory.
3. In Hallo **wachtwoord** vak, typ het wachtwoord van de gebruiker voor hello Azure Active Directory-account of federatieve domeinaccount.

    ![Selecteer verificatie van AD-wachtwoord][12]
4. Klikt u op Hallo **opties** knop, en op Hallo **verbindingseigenschappen** pagina in Hallo **toodatabase verbinding** vak, Hallo typenaam van de gebruikersdatabase Hallo gewenste tooconnect Aan. (Zie afbeelding in de vorige optie Hallo Hallo.)

## <a name="using-an-azure-ad-identity-tooconnect-from-a-client-application"></a>Met behulp van een Azure AD identity tooconnect van een clienttoepassing

Hallo volgende procedures laten zien hoe tooconnect tooa SQL-database met een Azure AD-identiteit van een clienttoepassing.

###  <a name="active-directory-integrated-authentication"></a>Geïntegreerde verificatie van Active Directory

toouse geïntegreerde Windows-verificatie, Active Directory van uw domein moet worden gefedereerd met Azure Active Directory. De clienttoepassing (of een service) verbinding maken met toohello database moet worden uitgevoerd op een machine domein onder de domeinreferenties van een gebruiker.

tooconnect tooa database met geïntegreerde verificatie en de identiteit van een Azure AD, Hallo verificatie-sleutelwoord in de tekenreeks voor databaseverbinding Hallo tooActive Directory Integrated moet worden ingesteld. Hallo volgende C#-codevoorbeeld maakt gebruik van ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Integrated; Initial Catalog=testdb;";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Hallo sleutelwoord van de verbindingsreeks ``Integrated Security=True`` wordt niet ondersteund voor het verbinden van tooAzure SQL-Database. Bij het maken van een ODBC-verbinding, moet u tooremove spaties moeten en stel verificatie too'ActiveDirectoryIntegrated'.

### <a name="active-directory-password-authentication"></a>Active Directory-wachtwoordverificatie

tooconnect tooa database met geïntegreerde verificatie en de identiteit van een Azure AD, Hallo verificatie sleutelwoord tooActive wachtwoord voor Active Directory moet worden ingesteld. Hallo-verbindingsreeks moet gebruikers-ID/UID en het wachtwoord/PWD sleutelwoorden en waarden bevatten. Hallo volgende C#-codevoorbeeld maakt gebruik van ADO .NET.

```
string ConnectionString =
@"Data Source=n9lxnyuzhv.database.windows.net; Authentication=Active Directory Password; Initial Catalog=testdb;  UID=bob@contoso.onmicrosoft.com; PWD=MyPassWord!";
SqlConnection conn = new SqlConnection(ConnectionString);
conn.Open();
```

Meer informatie over Azure AD-verificatiemethoden met Hallo demo-codevoorbeelden beschikbaar op [Azure AD Authentication GitHub Demo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/security/azure-active-directory-auth).

## <a name="azure-ad-token"></a>Azure AD-token
Deze verificatiemethode kan services van de middelste laag tooconnect tooAzure SQL-Database of Azure SQL Data Warehouse door het verkrijgen van een token van Azure Active Directory (AAD). Hiermee kunt geavanceerde scenario's zoals verificatie op basis van certificaten. U moet vier eenvoudige stappen toouse Azure AD-tokenverificatie uitvoeren:

1. Uw toepassing registreren met Azure Active Directory en Hallo client-id niet ophalen voor uw code. 
2. Een gebruiker die Hallo databasetoepassing maken. (Voltooid eerder in stap 6).
3. Een certificaat op Hallo client-computer wordt uitgevoerd Hallo-toepassing maken.
4. Hallo-certificaat als een sleutel voor uw toepassing toevoegen.

Voorbeeld-verbindingsreeks:

```
string ConnectionString =@"Data Source=n9lxnyuzhv.database.windows.net; Initial Catalog=testdb;"
SqlConnection conn = new SqlConnection(ConnectionString);
connection.AccessToken = "Your JWT token"
conn.Open();
```

Zie voor meer informatie [SQL Server Security-Blog](https://blogs.msdn.microsoft.com/sqlsecurity/2016/02/09/token-based-authentication-support-for-azure-sql-db-using-azure-ad-auth/).

### <a name="sqlcmd"></a>sqlcmd

Hallo na instructies, wordt verbinding gemaakt met versie 13,1 van sqlcmd die beschikbaar via Hallo is [Downloadcentrum](http://go.microsoft.com/fwlink/?LinkID=825643).

```
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net  -G  
sqlcmd -S Target_DB_or_DW.testsrv.database.windows.net -U bob@contoso.com -P MyAADPassword -G -l 30
```

## <a name="next-steps"></a>Volgende stappen
- Zie [SQL Database-toegang en -beheer](sql-database-control-access.md) voor een overzicht van toegang en beheer in SQL Database.
- Zie [Aanmeldingen, gebruikers en databaserollen](sql-database-manage-logins.md) voor een overzicht van aanmeldingen, gebruikers en databaserollen in SQL Database.
- Zie [Principals](https://msdn.microsoft.com/library/ms181127.aspx) voor meer informatie over database-principals.
- Zie [Databaserollen](https://msdn.microsoft.com/library/ms189121.aspx) voor meer informatie over databaserollen.
- Zie [SQL Database-firewallregels](sql-database-firewall-configure.md) voor meer informatie over de firewallregels in SQL Database.

<!--Image references-->

[1]: ./media/sql-database-aad-authentication/1aad-auth-diagram.png
[2]: ./media/sql-database-aad-authentication/2subscription-relationship.png
[3]: ./media/sql-database-aad-authentication/3admin-structure.png
[4]: ./media/sql-database-aad-authentication/4select-subscription.png
[5]: ./media/sql-database-aad-authentication/5ad-settings-portal.png
[6]: ./media/sql-database-aad-authentication/6edit-directory-select.png
[7]: ./media/sql-database-aad-authentication/7edit-directory-confirm.png
[8]: ./media/sql-database-aad-authentication/8choose-ad.png
[10]: ./media/sql-database-aad-authentication/10choose-admin.png
[11]: ./media/sql-database-aad-authentication/active-directory-integrated.png
[12]: ./media/sql-database-aad-authentication/12connect-using-pw-auth2.png
[13]: ./media/sql-database-aad-authentication/13connect-to-db2.png


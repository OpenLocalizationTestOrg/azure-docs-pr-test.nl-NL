---
title: 'Zelfstudie: Web-app met een multitenant-database met behulp van Entity Framework en beveiliging'
description: Informatie over het ontwikkelen van een ASP.NET MVC 5-web-app met een multitenant SQL-Database backent, met behulp van Entity Framework en beveiliging.
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Zelfstudie: Web-app met een multitenant-database met behulp van Entity Framework en beveiliging
Deze zelfstudie laat zien hoe u een multitenant-web-app met een '[gedeelde database, gedeelde schema](https://msdn.microsoft.com/library/aa479086.aspx)' tenancymodus model, using Entity Framework en [beveiliging](https://msdn.microsoft.com/library/dn765131.aspx). In dit model, een individuele database bevat gegevens voor tal van tenants en elke rij in elke tabel is gekoppeld aan een 'Tenant-id '. Rij-Level Security (RLS), een nieuwe functie voor Azure SQL Database wordt gebruikt om te voorkomen dat tenants toegang tot elkaars gegevens. Dit is slechts één, kleine wijziging aan de toepassing vereist. Door het centraliseren van de tenant toegang logica in de database zelf RLS vereenvoudigt de toepassingscode en vermindert het risico op onbedoelde lekken van gegevens tussen de tenants.

We beginnen met de eenvoudige Contact Manager-toepassing van [een MVP ASP.NET-app met verificatie en SQL-database maken en implementeren in Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Rechts nu de toepassing kan alle gebruikers (tenants) voor een overzicht van alle contactpersonen:

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Met slechts enkele kleine wijzigingen, wordt er ondersteuning voor multitenancy, toevoegen zodat gebruikers kunnen zien alleen de contactpersonen die deel uitmaken van deze.

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a>Stap 1: Een klasse Interceptor toevoegen in de toepassing de SESSION_CONTEXT instellen
Er is een toepassing wijzigen die we moeten controleren. Omdat alle gebruikers van de toepassing verbinding maken met de database met de verbindingsreeks (dat wil zeggen dezelfde SQL-aanmelding), is er momenteel niet mogelijk voor een beleid RLS weten welke gebruiker te filteren. Deze aanpak is heel gebruikelijk in webtoepassingen omdat hierdoor efficiënt groepsgewijze, maar dan moet een andere manier om te identificeren van de huidige gebruiker van toepassing in de database. De oplossing is de toepassing is een sleutel / waarde-paar ingesteld voor de huidige gebruiker-id in de [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) onmiddellijk na het openen van een verbinding voordat deze wordt uitgevoerd geen query's. SESSION_CONTEXT is een sleutel / waarde-sessiebereik store en ons beleid RLS de gebruikersnaam die is opgeslagen in het identificeren van de huidige gebruiker gebruikt.

We zullen toevoegen een [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (met name een [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), een nieuwe functie in Entity Framework (EF) 6, worden automatisch de huidige gebruiker-id in de SESSION_CONTEXT ingesteld door het uitvoeren van een T-SQL Wanneer een verbinding wordt geopend door EF-instructie.

1. Open het project ContactManager in Visual Studio.
2. Met de rechtermuisknop op de map modellen in Solution Explorer en kiest u toevoegen > klasse.
3. Naam van de nieuwe klasse 'SessionContextInterceptor.cs' en klik op toevoegen.
4. De inhoud van SessionContextInterceptor.cs vervangen door de volgende code.

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

Dit is de wijziging alleen van toepassing is vereist. Opwekken en bouwen en de toepassing te publiceren.

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a>Stap 2: Een gebruikers-id-kolom toevoegen aan het schema van de database
Vervolgens moet een gebruikers-id-kolom toevoegen aan de tabel Contactpersonen elke rij koppelen aan een gebruiker (tenant). We zullen het schema rechtstreeks in de database wijzigen zodat er zijn momenteel geen dit veld opnemen in ons EF-gegevensmodel.

Rechtstreeks verbinding gemaakt met de database, met behulp van SQL Server Management Studio of Visual Studio, en voer vervolgens de volgende T-SQL:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Een gebruikers-id-kolom wordt toegevoegd aan de tabel Contactpersonen. We gebruiken het gegevenstype nvarchar(128) overeenkomen met de opgeslagen in de tabel AspNetUsers gebruikersnamen en maken we een DEFAULT-beperking die de gebruikers-id van nieuw ingevoegde rijen moet de gebruikersnaam die momenteel zijn opgeslagen in SESSION_CONTEXT automatisch ingesteld.

Nu de tabel ziet er als volgt:

![Tabel SSMS contactpersonen](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Wanneer nieuwe contactpersonen worden gemaakt, moeten worden ze automatisch de juiste gebruikers-id toegewezen. Voor demonstratiedoeleinden echter we toewijzen slechts enkele van deze bestaande contactpersonen aan een bestaande gebruiker.

Als u een paar gebruikers in de toepassing al hebt gemaakt (bijvoorbeeld met behulp van lokale, Google of Facebook accounts), ziet u ze in de tabel AspNetUsers. In de onderstaande schermafbeelding is er slechts één gebruiker tot nu toe.

![SSMS AspNetUsers tabel](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Kopieer de Id voor user1@contoso.com, en plak deze in de onderstaande T-SQL-instructie. Uitvoeren van deze instructie drie van de contactpersonen koppelt u deze gebruikers-id.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a>Stap 3: Een rijniveau beveiligingsbeleid maken in de database
De laatste stap is het maken van een beveiligingsbeleid die gebruikmaakt van de gebruikers-id in SESSION_CONTEXT voor het filteren van automatisch de resultaten van query's.

Nog steeds verbinding gemaakt met de database en voert u de volgende T-SQL uit:

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

Deze code biedt drie dingen. Eerst wordt een nieuw schema gemaakt als een best practice voor centraliseren en beperken van toegang tot de RLS-objecten. Vervolgens wordt een predicaatfunctie dat '1' wordt geretourneerd wanneer de gebruiker van een rij-id overeenkomt met de gebruikersnaam in SESSION_CONTEXT gemaakt. Ten slotte wordt gemaakt van een beveiligingsbeleid dat deze functie als een filter en de block-predicaat voor de tabel contactpersonen toegevoegd. Het filterpredicaat worden query's om terug te keren alleen rijen die deel uitmaken van de huidige gebruiker en het block-predicaat fungeert als veiligheidsmaatregel om te voorkomen dat de toepassing van ooit per ongeluk het invoegen van een rij voor de verkeerde gebruiker.

Nu de toepassing uitvoeren en meld u aan als user1@contoso.com. Deze gebruiker ziet nu alleen de contactpersonen die we eerder aan deze gebruikers-id toegewezen:

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

Probeer, om te valideren dit verder te registreren van een nieuwe gebruiker. Ze zien dan geen contactpersonen, omdat er geen aan hen is toegewezen. Als ze een nieuw contact maakt, wordt deze toegewezen aan deze, en kunnen alleen ze kunnen zien.

## <a name="next-steps"></a>Volgende stappen
Dat is alles. De eenvoudige Contact Manager web-app is geconverteerd naar een multitenant een waar elke gebruiker een eigen lijst met contactpersonen heeft. Met behulp van beveiliging, hebben we de complexiteit van het afdwingen van de tenant toegang logica in de toepassingscode vermeden. Kan de toepassing ligt de nadruk op de echte zakelijke probleem bij de hand van deze transparantie en vermindert ook het risico van het per ongeluk gegevens lekken, omdat de toepassing de codebasis groeit.

Deze zelfstudie is horen bij elkaar van de mogelijkheden voor beveiliging op Rijniveau. Bijvoorbeeld, is het mogelijk te hebben meer geavanceerde of gedetailleerde toegang logica, en het opslaan van meer dan alleen de huidige gebruiker-id in de SESSION_CONTEXT's. Het is ook mogelijk om te [RLS integreren met de clientbibliotheken voor hulpprogramma's van elastische database](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) ter ondersteuning van meerdere tenants shards in een scale-out gegevenslaag.

We proberen afgezien van deze mogelijkheden ook zodat RLS nog verder te verbeteren. Als u vragen hebt, ideeën of dingen die u zien wilt, laat ons weten in de opmerkingen. We stellen uw feedback op prijs!


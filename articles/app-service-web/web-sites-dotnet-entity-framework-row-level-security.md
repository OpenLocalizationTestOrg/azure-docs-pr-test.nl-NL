---
title: 'Zelfstudie: Web-app met een multitenant-database met behulp van Entity Framework en beveiliging'
description: Meer informatie over hoe een ASP.NET MVC 5 toodevelop web-app met een multitenant SQL-Database backent, met behulp van Entity Framework en beveiliging.
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
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Zelfstudie: Web-app met een multitenant-database met behulp van Entity Framework en beveiliging
Deze zelfstudie laat zien hoe een multitenant toobuild web-app met een '[gedeelde database, gedeelde schema](https://msdn.microsoft.com/library/aa479086.aspx)' tenancymodus model, using Entity Framework en [beveiliging](https://msdn.microsoft.com/library/dn765131.aspx). In dit model, een individuele database bevat gegevens voor tal van tenants en elke rij in elke tabel is gekoppeld aan een 'Tenant-id '. Rij-Level Security (RLS), een nieuwe functie voor Azure SQL Database is gebruikte tooprevent tenants toegang tot elkaars gegevens. Dit is slechts één, kleine wijziging toohello toepassing vereist. Door centraliseren Hallo tenant toegang logica binnen Hallo-database zelf RLS vereenvoudigt het Hallo-toepassingscode en minder risico op Hallo onbedoeld lekken van gegevens tussen de tenants.

We beginnen met eenvoudige Contact Manager-toepassing hello van [een MVP ASP.NET-app met verificatie en SQL-database maken en implementeren van App Service tooAzure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Rechts nu Hallo toepassing kan alle gebruikers (tenants) toosee alle contactpersonen:

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Met slechts enkele kleine wijzigingen, wordt er ondersteuning voor multitenancy, toevoegen zodat gebruikers het alleen Hallo contactpersonen kunnen toosee, die deel uitmaken van toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Stap 1: Een klasse Interceptor in Hallo toepassing tooset hello SESSION_CONTEXT toevoegen
Er is een wijziging van de aanvraag moet toomake. Omdat alle gebruikers van de toepassing verbinding maken met toohello database met dezelfde verbindingsreeks (dat wil zeggen dezelfde SQL-aanmelding) hello, er is momenteel geen manier voor een RLS beleid tooknow waarmee de gebruiker moet het filteren op. Deze aanpak is heel gebruikelijk in webtoepassingen omdat kunnen efficiënt groepsgewijze, maar dan moet een andere manier tooidentify Hallo huidige gebruiker van toepassing binnen Hallo-database. Hallo oplossing is toohave Hallo toepassing set een sleutel-waardepaar voor huidige UserId in Hallo Hallo [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) onmiddellijk na het openen van een verbinding voordat deze wordt uitgevoerd geen query's. SESSION_CONTEXT is een sleutel / waarde-sessiebereik store en ons beleid RLS gebruikt Hallo UserId in het opgeslagen tooidentify Hallo-huidige gebruiker.

We zullen toevoegen een [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (met name een [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), een nieuwe functie in Entity Framework (EF) 6, tooautomatically set Hallo huidige UserId in Hallo SESSION_CONTEXT door het uitvoeren van een T-SQL-instructie wanneer EF een verbinding wordt geopend.

1. Hallo ContactManager project openen in Visual Studio.
2. Met de rechtermuisknop op de map voor Hallo-modellen in Hallo Solution Explorer en kiest u toevoegen > klasse.
3. Naam van de nieuwe klasse Hallo 'SessionContextInterceptor.cs' en klik op toevoegen.
4. Hallo-inhoud van SessionContextInterceptor.cs vervangen door Hallo code te volgen.

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
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
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

Hallo enige toepassing wijziging vereist is. Opwekken en bouwen en Hallo toepassing publiceren.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Stap 2: Een databaseschema UserId kolom toohello toevoegen
Vervolgens moet een UserId kolom toohello contactpersonen tabel tooassociate tooadd elke rij met een gebruiker (tenant). We wordt Hallo schema rechtstreeks in het Hallo-database wijzigen en er zijn momenteel geen tooinclude dit veld in onze EF-gegevensmodel.

Verbinding maken met toohello database rechtstreeks met behulp van SQL Server Management Studio of Visual Studio, en vervolgens uitvoeren Hallo volgende T-SQL:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Hiermee wordt een tabel met contacten toohello voor UserId kolom toegevoegd. We gebruiken Hallo nvarchar(128) gegevens type toomatch Hallo die gebruikersnamen in Hallo AspNetUsers tabel opgeslagen en maken we een DEFAULT-beperking die Hallo UserId voor nieuw ingevoegde rijen toobe Hallo UserId die momenteel zijn opgeslagen in SESSION_CONTEXT automatisch ingesteld.

Nu Hallo tabel ziet er als volgt:

![Tabel SSMS contactpersonen](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Tijdens het maken van nieuwe contactpersonen worden ze automatisch worden toegewezen Hallo UserId corrigeren. Voor demonstratiedoeleinden echter laten toewijzen slechts enkele van deze bestaande contactpersonen tooan bestaande gebruiker.

Als u een paar gebruikers in Hallo toepassing al hebt gemaakt (bijvoorbeeld met behulp van lokale, Google of Facebook accounts), ziet u ze in Hallo AspNetUsers tabel. In onderstaande Hallo schermafbeelding is er slechts één gebruiker tot nu toe.

![SSMS AspNetUsers tabel](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Kopiëren Hallo Id voor user1@contoso.com, en plak deze in de onderstaande Hallo T-SQL-instructie. Deze instructie tooassociate drie Hallo contactpersonen met deze gebruikersnaam van uitvoeren.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Stap 3: Een rijniveau beveiligingsbeleid in Hallo-database maken
de laatste stap Hallo is toocreate beveiligingsbeleid dat gebruikmaakt van Hallo UserId in SESSION_CONTEXT tooautomatically filter Hallo resultaten geretourneerd door query's.

Uitvoeren tijdens de database nog steeds verbonden toohello, Hallo volgende T-SQL:

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

Deze code biedt drie dingen. Eerst wordt een nieuw schema gemaakt als een best practice voor centraliseren en beperken van toegang toohello RLS objecten. Vervolgens wordt een predicaatfunctie dat '1' wordt geretourneerd wanneer Hallo UserId van een rij overeenkomt met de Hallo UserId in SESSION_CONTEXT gemaakt. Ten slotte wordt gemaakt van een beveiligingsbeleid dat deze functie als een filter en de block-predicaat voor Hallo contactpersonen tabel toegevoegd. Hallo filterpredicaat zorgt ervoor dat query's tooreturn alleen rijen die deel uitmaken van de huidige gebruiker toohello en Hallo block-predicaat fungeert als een toepassing safeguard tooprevent Hallo ooit per ongeluk een rij voor Hallo verkeerde gebruiker invoegen.

Nu Hallo toepassing uitvoeren en meld u aan als user1@contoso.com. Deze gebruiker ziet nu alleen Hallo contactpersonen we toothis UserId eerder toegewezen:

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate deze verder probeert een nieuwe gebruiker registreren. Ze zien dan geen contactpersonen, omdat er geen toothem is toegewezen. Als ze een nieuw contact maken, deze worden toegewezen toothem en ze alleen kunnen toosee worden deze.

## <a name="next-steps"></a>Volgende stappen
Dat is alles. Hallo eenvoudige Contact Manager web-app is geconverteerd naar een multitenant een waar elke gebruiker een eigen lijst met contactpersonen heeft. Met behulp van de beveiliging hebt we Hallo complexiteit van het afdwingen van de tenant toegang logica in onze toepassingscode vermeden. Deze transparantie Hallo toepassing toofocus kan op Hallo echte zakelijke probleem bij de hand en dit verlaagt ook Hallo risico per ongeluk gegevens lekken, zoals toepassing hello de codebasis groeit.

Deze zelfstudie heeft alleen bekraste Hallo oppervlak van de mogelijkheden voor beveiliging op Rijniveau. Bijvoorbeeld, is mogelijk meer geavanceerde toohave of gedetailleerde toegang logica en de mogelijke toostore meer dan alleen huidige UserId in Hallo SESSION_CONTEXT Hallo. Het kan ook te[RLS integreren met Hallo elastische database extra clientbibliotheken](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multitenant shards in een scale-out gegevenslaag.

Afgezien van deze mogelijkheden waarmee we ook toomake RLS nog beter werkt. Als u vragen hebt, ideeën of dingen die u wilt dat toosee, laat ons weten in Hallo opmerkingen. We stellen uw feedback op prijs!


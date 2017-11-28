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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="b50ec-103">Zelfstudie: Web-app met een multitenant-database met behulp van Entity Framework en beveiliging</span><span class="sxs-lookup"><span data-stu-id="b50ec-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="b50ec-104">Deze zelfstudie laat zien hoe een multitenant toobuild web-app met een '[gedeelde database, gedeelde schema](https://msdn.microsoft.com/library/aa479086.aspx)' tenancymodus model, using Entity Framework en [beveiliging](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="b50ec-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="b50ec-105">In dit model, een individuele database bevat gegevens voor tal van tenants en elke rij in elke tabel is gekoppeld aan een 'Tenant-id '.</span><span class="sxs-lookup"><span data-stu-id="b50ec-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="b50ec-106">Rij-Level Security (RLS), een nieuwe functie voor Azure SQL Database is gebruikte tooprevent tenants toegang tot elkaars gegevens.</span><span class="sxs-lookup"><span data-stu-id="b50ec-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="b50ec-107">Dit is slechts één, kleine wijziging toohello toepassing vereist.</span><span class="sxs-lookup"><span data-stu-id="b50ec-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="b50ec-108">Door centraliseren Hallo tenant toegang logica binnen Hallo-database zelf RLS vereenvoudigt het Hallo-toepassingscode en minder risico op Hallo onbedoeld lekken van gegevens tussen de tenants.</span><span class="sxs-lookup"><span data-stu-id="b50ec-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="b50ec-109">We beginnen met eenvoudige Contact Manager-toepassing hello van [een MVP ASP.NET-app met verificatie en SQL-database maken en implementeren van App Service tooAzure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b50ec-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="b50ec-110">Rechts nu Hallo toepassing kan alle gebruikers (tenants) toosee alle contactpersonen:</span><span class="sxs-lookup"><span data-stu-id="b50ec-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="b50ec-112">Met slechts enkele kleine wijzigingen, wordt er ondersteuning voor multitenancy, toevoegen zodat gebruikers het alleen Hallo contactpersonen kunnen toosee, die deel uitmaken van toothem.</span><span class="sxs-lookup"><span data-stu-id="b50ec-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="b50ec-113">Stap 1: Een klasse Interceptor in Hallo toepassing tooset hello SESSION_CONTEXT toevoegen</span><span class="sxs-lookup"><span data-stu-id="b50ec-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="b50ec-114">Er is een wijziging van de aanvraag moet toomake.</span><span class="sxs-lookup"><span data-stu-id="b50ec-114">There is one application change we need toomake.</span></span> <span data-ttu-id="b50ec-115">Omdat alle gebruikers van de toepassing verbinding maken met toohello database met dezelfde verbindingsreeks (dat wil zeggen dezelfde SQL-aanmelding) hello, er is momenteel geen manier voor een RLS beleid tooknow waarmee de gebruiker moet het filteren op.</span><span class="sxs-lookup"><span data-stu-id="b50ec-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="b50ec-116">Deze aanpak is heel gebruikelijk in webtoepassingen omdat kunnen efficiënt groepsgewijze, maar dan moet een andere manier tooidentify Hallo huidige gebruiker van toepassing binnen Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="b50ec-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="b50ec-117">Hallo oplossing is toohave Hallo toepassing set een sleutel-waardepaar voor huidige UserId in Hallo Hallo [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) onmiddellijk na het openen van een verbinding voordat deze wordt uitgevoerd geen query's.</span><span class="sxs-lookup"><span data-stu-id="b50ec-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="b50ec-118">SESSION_CONTEXT is een sleutel / waarde-sessiebereik store en ons beleid RLS gebruikt Hallo UserId in het opgeslagen tooidentify Hallo-huidige gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b50ec-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="b50ec-119">We zullen toevoegen een [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (met name een [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), een nieuwe functie in Entity Framework (EF) 6, tooautomatically set Hallo huidige UserId in Hallo SESSION_CONTEXT door het uitvoeren van een T-SQL-instructie wanneer EF een verbinding wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="b50ec-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="b50ec-120">Hallo ContactManager project openen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b50ec-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="b50ec-121">Met de rechtermuisknop op de map voor Hallo-modellen in Hallo Solution Explorer en kiest u toevoegen > klasse.</span><span class="sxs-lookup"><span data-stu-id="b50ec-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="b50ec-122">Naam van de nieuwe klasse Hallo 'SessionContextInterceptor.cs' en klik op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b50ec-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="b50ec-123">Hallo-inhoud van SessionContextInterceptor.cs vervangen door Hallo code te volgen.</span><span class="sxs-lookup"><span data-stu-id="b50ec-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

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

<span data-ttu-id="b50ec-124">Hallo enige toepassing wijziging vereist is.</span><span class="sxs-lookup"><span data-stu-id="b50ec-124">That's hello only application change required.</span></span> <span data-ttu-id="b50ec-125">Opwekken en bouwen en Hallo toepassing publiceren.</span><span class="sxs-lookup"><span data-stu-id="b50ec-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="b50ec-126">Stap 2: Een databaseschema UserId kolom toohello toevoegen</span><span class="sxs-lookup"><span data-stu-id="b50ec-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="b50ec-127">Vervolgens moet een UserId kolom toohello contactpersonen tabel tooassociate tooadd elke rij met een gebruiker (tenant).</span><span class="sxs-lookup"><span data-stu-id="b50ec-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="b50ec-128">We wordt Hallo schema rechtstreeks in het Hallo-database wijzigen en er zijn momenteel geen tooinclude dit veld in onze EF-gegevensmodel.</span><span class="sxs-lookup"><span data-stu-id="b50ec-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="b50ec-129">Verbinding maken met toohello database rechtstreeks met behulp van SQL Server Management Studio of Visual Studio, en vervolgens uitvoeren Hallo volgende T-SQL:</span><span class="sxs-lookup"><span data-stu-id="b50ec-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="b50ec-130">Hiermee wordt een tabel met contacten toohello voor UserId kolom toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b50ec-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="b50ec-131">We gebruiken Hallo nvarchar(128) gegevens type toomatch Hallo die gebruikersnamen in Hallo AspNetUsers tabel opgeslagen en maken we een DEFAULT-beperking die Hallo UserId voor nieuw ingevoegde rijen toobe Hallo UserId die momenteel zijn opgeslagen in SESSION_CONTEXT automatisch ingesteld.</span><span class="sxs-lookup"><span data-stu-id="b50ec-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="b50ec-132">Nu Hallo tabel ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="b50ec-132">Now hello table looks like this:</span></span>

![Tabel SSMS contactpersonen](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="b50ec-134">Tijdens het maken van nieuwe contactpersonen worden ze automatisch worden toegewezen Hallo UserId corrigeren.</span><span class="sxs-lookup"><span data-stu-id="b50ec-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="b50ec-135">Voor demonstratiedoeleinden echter laten toewijzen slechts enkele van deze bestaande contactpersonen tooan bestaande gebruiker.</span><span class="sxs-lookup"><span data-stu-id="b50ec-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="b50ec-136">Als u een paar gebruikers in Hallo toepassing al hebt gemaakt (bijvoorbeeld met behulp van lokale, Google of Facebook accounts), ziet u ze in Hallo AspNetUsers tabel.</span><span class="sxs-lookup"><span data-stu-id="b50ec-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="b50ec-137">In onderstaande Hallo schermafbeelding is er slechts één gebruiker tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="b50ec-137">In hello screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers tabel](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="b50ec-139">Kopiëren Hallo Id voor user1@contoso.com, en plak deze in de onderstaande Hallo T-SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="b50ec-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="b50ec-140">Deze instructie tooassociate drie Hallo contactpersonen met deze gebruikersnaam van uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b50ec-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="b50ec-141">Stap 3: Een rijniveau beveiligingsbeleid in Hallo-database maken</span><span class="sxs-lookup"><span data-stu-id="b50ec-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="b50ec-142">de laatste stap Hallo is toocreate beveiligingsbeleid dat gebruikmaakt van Hallo UserId in SESSION_CONTEXT tooautomatically filter Hallo resultaten geretourneerd door query's.</span><span class="sxs-lookup"><span data-stu-id="b50ec-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="b50ec-143">Uitvoeren tijdens de database nog steeds verbonden toohello, Hallo volgende T-SQL:</span><span class="sxs-lookup"><span data-stu-id="b50ec-143">While still connected toohello database, execute hello following T-SQL:</span></span>

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

<span data-ttu-id="b50ec-144">Deze code biedt drie dingen.</span><span class="sxs-lookup"><span data-stu-id="b50ec-144">This code does three things.</span></span> <span data-ttu-id="b50ec-145">Eerst wordt een nieuw schema gemaakt als een best practice voor centraliseren en beperken van toegang toohello RLS objecten.</span><span class="sxs-lookup"><span data-stu-id="b50ec-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="b50ec-146">Vervolgens wordt een predicaatfunctie dat '1' wordt geretourneerd wanneer Hallo UserId van een rij overeenkomt met de Hallo UserId in SESSION_CONTEXT gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b50ec-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="b50ec-147">Ten slotte wordt gemaakt van een beveiligingsbeleid dat deze functie als een filter en de block-predicaat voor Hallo contactpersonen tabel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="b50ec-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="b50ec-148">Hallo filterpredicaat zorgt ervoor dat query's tooreturn alleen rijen die deel uitmaken van de huidige gebruiker toohello en Hallo block-predicaat fungeert als een toepassing safeguard tooprevent Hallo ooit per ongeluk een rij voor Hallo verkeerde gebruiker invoegen.</span><span class="sxs-lookup"><span data-stu-id="b50ec-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="b50ec-149">Nu Hallo toepassing uitvoeren en meld u aan als user1@contoso.com. Deze gebruiker ziet nu alleen Hallo contactpersonen we toothis UserId eerder toegewezen:</span><span class="sxs-lookup"><span data-stu-id="b50ec-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="b50ec-151">toovalidate deze verder probeert een nieuwe gebruiker registreren.</span><span class="sxs-lookup"><span data-stu-id="b50ec-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="b50ec-152">Ze zien dan geen contactpersonen, omdat er geen toothem is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="b50ec-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="b50ec-153">Als ze een nieuw contact maken, deze worden toegewezen toothem en ze alleen kunnen toosee worden deze.</span><span class="sxs-lookup"><span data-stu-id="b50ec-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b50ec-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b50ec-154">Next steps</span></span>
<span data-ttu-id="b50ec-155">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="b50ec-155">That's it!</span></span> <span data-ttu-id="b50ec-156">Hallo eenvoudige Contact Manager web-app is geconverteerd naar een multitenant een waar elke gebruiker een eigen lijst met contactpersonen heeft.</span><span class="sxs-lookup"><span data-stu-id="b50ec-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="b50ec-157">Met behulp van de beveiliging hebt we Hallo complexiteit van het afdwingen van de tenant toegang logica in onze toepassingscode vermeden.</span><span class="sxs-lookup"><span data-stu-id="b50ec-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="b50ec-158">Deze transparantie Hallo toepassing toofocus kan op Hallo echte zakelijke probleem bij de hand en dit verlaagt ook Hallo risico per ongeluk gegevens lekken, zoals toepassing hello de codebasis groeit.</span><span class="sxs-lookup"><span data-stu-id="b50ec-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="b50ec-159">Deze zelfstudie heeft alleen bekraste Hallo oppervlak van de mogelijkheden voor beveiliging op Rijniveau.</span><span class="sxs-lookup"><span data-stu-id="b50ec-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="b50ec-160">Bijvoorbeeld, is mogelijk meer geavanceerde toohave of gedetailleerde toegang logica en de mogelijke toostore meer dan alleen huidige UserId in Hallo SESSION_CONTEXT Hallo.</span><span class="sxs-lookup"><span data-stu-id="b50ec-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="b50ec-161">Het kan ook te[RLS integreren met Hallo elastische database extra clientbibliotheken](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multitenant shards in een scale-out gegevenslaag.</span><span class="sxs-lookup"><span data-stu-id="b50ec-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="b50ec-162">Afgezien van deze mogelijkheden waarmee we ook toomake RLS nog beter werkt.</span><span class="sxs-lookup"><span data-stu-id="b50ec-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="b50ec-163">Als u vragen hebt, ideeën of dingen die u wilt dat toosee, laat ons weten in Hallo opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="b50ec-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="b50ec-164">We stellen uw feedback op prijs!</span><span class="sxs-lookup"><span data-stu-id="b50ec-164">We appreciate your feedback!</span></span>


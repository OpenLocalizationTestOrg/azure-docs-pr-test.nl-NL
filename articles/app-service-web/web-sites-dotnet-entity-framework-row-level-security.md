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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="7b19b-103">Zelfstudie: Web-app met een multitenant-database met behulp van Entity Framework en beveiliging</span><span class="sxs-lookup"><span data-stu-id="7b19b-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="7b19b-104">Deze zelfstudie laat zien hoe u een multitenant-web-app met een '[gedeelde database, gedeelde schema](https://msdn.microsoft.com/library/aa479086.aspx)' tenancymodus model, using Entity Framework en [beveiliging](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b19b-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="7b19b-105">In dit model, een individuele database bevat gegevens voor tal van tenants en elke rij in elke tabel is gekoppeld aan een 'Tenant-id '.</span><span class="sxs-lookup"><span data-stu-id="7b19b-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="7b19b-106">Rij-Level Security (RLS), een nieuwe functie voor Azure SQL Database wordt gebruikt om te voorkomen dat tenants toegang tot elkaars gegevens.</span><span class="sxs-lookup"><span data-stu-id="7b19b-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="7b19b-107">Dit is slechts één, kleine wijziging aan de toepassing vereist.</span><span class="sxs-lookup"><span data-stu-id="7b19b-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="7b19b-108">Door het centraliseren van de tenant toegang logica in de database zelf RLS vereenvoudigt de toepassingscode en vermindert het risico op onbedoelde lekken van gegevens tussen de tenants.</span><span class="sxs-lookup"><span data-stu-id="7b19b-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="7b19b-109">We beginnen met de eenvoudige Contact Manager-toepassing van [een MVP ASP.NET-app met verificatie en SQL-database maken en implementeren in Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7b19b-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="7b19b-110">Rechts nu de toepassing kan alle gebruikers (tenants) voor een overzicht van alle contactpersonen:</span><span class="sxs-lookup"><span data-stu-id="7b19b-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="7b19b-112">Met slechts enkele kleine wijzigingen, wordt er ondersteuning voor multitenancy, toevoegen zodat gebruikers kunnen zien alleen de contactpersonen die deel uitmaken van deze.</span><span class="sxs-lookup"><span data-stu-id="7b19b-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="7b19b-113">Stap 1: Een klasse Interceptor toevoegen in de toepassing de SESSION_CONTEXT instellen</span><span class="sxs-lookup"><span data-stu-id="7b19b-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="7b19b-114">Er is een toepassing wijzigen die we moeten controleren.</span><span class="sxs-lookup"><span data-stu-id="7b19b-114">There is one application change we need to make.</span></span> <span data-ttu-id="7b19b-115">Omdat alle gebruikers van de toepassing verbinding maken met de database met de verbindingsreeks (dat wil zeggen dezelfde SQL-aanmelding), is er momenteel niet mogelijk voor een beleid RLS weten welke gebruiker te filteren.</span><span class="sxs-lookup"><span data-stu-id="7b19b-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="7b19b-116">Deze aanpak is heel gebruikelijk in webtoepassingen omdat hierdoor efficiënt groepsgewijze, maar dan moet een andere manier om te identificeren van de huidige gebruiker van toepassing in de database.</span><span class="sxs-lookup"><span data-stu-id="7b19b-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="7b19b-117">De oplossing is de toepassing is een sleutel / waarde-paar ingesteld voor de huidige gebruiker-id in de [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) onmiddellijk na het openen van een verbinding voordat deze wordt uitgevoerd geen query's.</span><span class="sxs-lookup"><span data-stu-id="7b19b-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="7b19b-118">SESSION_CONTEXT is een sleutel / waarde-sessiebereik store en ons beleid RLS de gebruikersnaam die is opgeslagen in het identificeren van de huidige gebruiker gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b19b-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="7b19b-119">We zullen toevoegen een [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (met name een [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), een nieuwe functie in Entity Framework (EF) 6, worden automatisch de huidige gebruiker-id in de SESSION_CONTEXT ingesteld door het uitvoeren van een T-SQL Wanneer een verbinding wordt geopend door EF-instructie.</span><span class="sxs-lookup"><span data-stu-id="7b19b-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="7b19b-120">Open het project ContactManager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b19b-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="7b19b-121">Met de rechtermuisknop op de map modellen in Solution Explorer en kiest u toevoegen > klasse.</span><span class="sxs-lookup"><span data-stu-id="7b19b-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="7b19b-122">Naam van de nieuwe klasse 'SessionContextInterceptor.cs' en klik op toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b19b-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="7b19b-123">De inhoud van SessionContextInterceptor.cs vervangen door de volgende code.</span><span class="sxs-lookup"><span data-stu-id="7b19b-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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

<span data-ttu-id="7b19b-124">Dit is de wijziging alleen van toepassing is vereist.</span><span class="sxs-lookup"><span data-stu-id="7b19b-124">That's the only application change required.</span></span> <span data-ttu-id="7b19b-125">Opwekken en bouwen en de toepassing te publiceren.</span><span class="sxs-lookup"><span data-stu-id="7b19b-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="7b19b-126">Stap 2: Een gebruikers-id-kolom toevoegen aan het schema van de database</span><span class="sxs-lookup"><span data-stu-id="7b19b-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="7b19b-127">Vervolgens moet een gebruikers-id-kolom toevoegen aan de tabel Contactpersonen elke rij koppelen aan een gebruiker (tenant).</span><span class="sxs-lookup"><span data-stu-id="7b19b-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="7b19b-128">We zullen het schema rechtstreeks in de database wijzigen zodat er zijn momenteel geen dit veld opnemen in ons EF-gegevensmodel.</span><span class="sxs-lookup"><span data-stu-id="7b19b-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="7b19b-129">Rechtstreeks verbinding gemaakt met de database, met behulp van SQL Server Management Studio of Visual Studio, en voer vervolgens de volgende T-SQL:</span><span class="sxs-lookup"><span data-stu-id="7b19b-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="7b19b-130">Een gebruikers-id-kolom wordt toegevoegd aan de tabel Contactpersonen.</span><span class="sxs-lookup"><span data-stu-id="7b19b-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="7b19b-131">We gebruiken het gegevenstype nvarchar(128) overeenkomen met de opgeslagen in de tabel AspNetUsers gebruikersnamen en maken we een DEFAULT-beperking die de gebruikers-id van nieuw ingevoegde rijen moet de gebruikersnaam die momenteel zijn opgeslagen in SESSION_CONTEXT automatisch ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7b19b-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="7b19b-132">Nu de tabel ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="7b19b-132">Now the table looks like this:</span></span>

![Tabel SSMS contactpersonen](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="7b19b-134">Wanneer nieuwe contactpersonen worden gemaakt, moeten worden ze automatisch de juiste gebruikers-id toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7b19b-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="7b19b-135">Voor demonstratiedoeleinden echter we toewijzen slechts enkele van deze bestaande contactpersonen aan een bestaande gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b19b-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="7b19b-136">Als u een paar gebruikers in de toepassing al hebt gemaakt (bijvoorbeeld met behulp van lokale, Google of Facebook accounts), ziet u ze in de tabel AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="7b19b-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="7b19b-137">In de onderstaande schermafbeelding is er slechts één gebruiker tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="7b19b-137">In the screenshot below, there is only one user so far.</span></span>

![SSMS AspNetUsers tabel](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="7b19b-139">Kopieer de Id voor user1@contoso.com, en plak deze in de onderstaande T-SQL-instructie.</span><span class="sxs-lookup"><span data-stu-id="7b19b-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="7b19b-140">Uitvoeren van deze instructie drie van de contactpersonen koppelt u deze gebruikers-id.</span><span class="sxs-lookup"><span data-stu-id="7b19b-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="7b19b-141">Stap 3: Een rijniveau beveiligingsbeleid maken in de database</span><span class="sxs-lookup"><span data-stu-id="7b19b-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="7b19b-142">De laatste stap is het maken van een beveiligingsbeleid die gebruikmaakt van de gebruikers-id in SESSION_CONTEXT voor het filteren van automatisch de resultaten van query's.</span><span class="sxs-lookup"><span data-stu-id="7b19b-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="7b19b-143">Nog steeds verbinding gemaakt met de database en voert u de volgende T-SQL uit:</span><span class="sxs-lookup"><span data-stu-id="7b19b-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="7b19b-144">Deze code biedt drie dingen.</span><span class="sxs-lookup"><span data-stu-id="7b19b-144">This code does three things.</span></span> <span data-ttu-id="7b19b-145">Eerst wordt een nieuw schema gemaakt als een best practice voor centraliseren en beperken van toegang tot de RLS-objecten.</span><span class="sxs-lookup"><span data-stu-id="7b19b-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="7b19b-146">Vervolgens wordt een predicaatfunctie dat '1' wordt geretourneerd wanneer de gebruiker van een rij-id overeenkomt met de gebruikersnaam in SESSION_CONTEXT gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b19b-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="7b19b-147">Ten slotte wordt gemaakt van een beveiligingsbeleid dat deze functie als een filter en de block-predicaat voor de tabel contactpersonen toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7b19b-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="7b19b-148">Het filterpredicaat worden query's om terug te keren alleen rijen die deel uitmaken van de huidige gebruiker en het block-predicaat fungeert als veiligheidsmaatregel om te voorkomen dat de toepassing van ooit per ongeluk het invoegen van een rij voor de verkeerde gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b19b-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="7b19b-149">Nu de toepassing uitvoeren en meld u aan als user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="7b19b-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="7b19b-150">Deze gebruiker ziet nu alleen de contactpersonen die we eerder aan deze gebruikers-id toegewezen:</span><span class="sxs-lookup"><span data-stu-id="7b19b-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Neem contact op met de toepassing voordat u inschakelt RLS Manager](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="7b19b-152">Probeer, om te valideren dit verder te registreren van een nieuwe gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7b19b-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="7b19b-153">Ze zien dan geen contactpersonen, omdat er geen aan hen is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="7b19b-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="7b19b-154">Als ze een nieuw contact maakt, wordt deze toegewezen aan deze, en kunnen alleen ze kunnen zien.</span><span class="sxs-lookup"><span data-stu-id="7b19b-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b19b-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b19b-155">Next steps</span></span>
<span data-ttu-id="7b19b-156">Dat is alles.</span><span class="sxs-lookup"><span data-stu-id="7b19b-156">That's it!</span></span> <span data-ttu-id="7b19b-157">De eenvoudige Contact Manager web-app is geconverteerd naar een multitenant een waar elke gebruiker een eigen lijst met contactpersonen heeft.</span><span class="sxs-lookup"><span data-stu-id="7b19b-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="7b19b-158">Met behulp van beveiliging, hebben we de complexiteit van het afdwingen van de tenant toegang logica in de toepassingscode vermeden.</span><span class="sxs-lookup"><span data-stu-id="7b19b-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="7b19b-159">Kan de toepassing ligt de nadruk op de echte zakelijke probleem bij de hand van deze transparantie en vermindert ook het risico van het per ongeluk gegevens lekken, omdat de toepassing de codebasis groeit.</span><span class="sxs-lookup"><span data-stu-id="7b19b-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="7b19b-160">Deze zelfstudie is horen bij elkaar van de mogelijkheden voor beveiliging op Rijniveau.</span><span class="sxs-lookup"><span data-stu-id="7b19b-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="7b19b-161">Bijvoorbeeld, is het mogelijk te hebben meer geavanceerde of gedetailleerde toegang logica, en het opslaan van meer dan alleen de huidige gebruiker-id in de SESSION_CONTEXT's.</span><span class="sxs-lookup"><span data-stu-id="7b19b-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="7b19b-162">Het is ook mogelijk om te [RLS integreren met de clientbibliotheken voor hulpprogramma's van elastische database](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) ter ondersteuning van meerdere tenants shards in een scale-out gegevenslaag.</span><span class="sxs-lookup"><span data-stu-id="7b19b-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="7b19b-163">We proberen afgezien van deze mogelijkheden ook zodat RLS nog verder te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="7b19b-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="7b19b-164">Als u vragen hebt, ideeën of dingen die u zien wilt, laat ons weten in de opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="7b19b-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="7b19b-165">We stellen uw feedback op prijs!</span><span class="sxs-lookup"><span data-stu-id="7b19b-165">We appreciate your feedback!</span></span>


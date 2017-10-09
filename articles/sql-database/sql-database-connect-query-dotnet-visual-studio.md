---
title: aaaUse Visual Studio en .NET tooquery Azure SQL Database | Microsoft Docs
description: Dit onderwerp leest u hoe toouse Visual Studio toocreate een programma dat verbinding tooan Azure SQL Database en de query maakt met behulp van Transact-SQL-instructies.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/05/2017
ms.author: carlrab
ms.openlocfilehash: 038cfb9c680217dfeea5a9996a0abed88cc80559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-net-c-with-visual-studio-tooconnect-and-query-an-azure-sql-database"></a><span data-ttu-id="bec88-103">.NET (C#) gebruikt met Visual Studio tooconnect en query's van een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="bec88-103">Use .NET (C#) with Visual Studio tooconnect and query an Azure SQL database</span></span>

<span data-ttu-id="bec88-104">Deze zelfstudie laat zien hoe toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate een C# programmeren met Visual Studio tooconnect tooan Azure SQL database en Transact-SQL-instructies tooquery gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bec88-104">This quick start tutorial demonstrates how toouse hello [.NET framework](https://www.microsoft.com/net/) toocreate a C# program with Visual Studio tooconnect tooan Azure SQL database and use Transact-SQL statements tooquery data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bec88-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bec88-105">Prerequisites</span></span>

<span data-ttu-id="bec88-106">toocomplete dit snelle zelfstudie begint, controleert u of hebt u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="bec88-106">toocomplete this quick start tutorial, make sure you have hello following:</span></span>

- <span data-ttu-id="bec88-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="bec88-107">An Azure SQL database.</span></span> <span data-ttu-id="bec88-108">Hallo-resources die zijn gemaakt in een van deze snel aan de slag maakt gebruik van deze snel starten:</span><span class="sxs-lookup"><span data-stu-id="bec88-108">This quick start uses hello resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="bec88-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="bec88-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="bec88-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="bec88-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="bec88-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="bec88-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="bec88-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor openbaar IP-adres van de computer Hallo Hallo u gebruiken voor deze zelfstudie voor snel starten.</span><span class="sxs-lookup"><span data-stu-id="bec88-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for hello public IP address of hello computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="bec88-113">Een installatie van [Visual Studio Community 2017, Visual Studio Professional 2017 of Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bec88-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="bec88-114">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="bec88-114">SQL server connection information</span></span>

<span data-ttu-id="bec88-115">Hallo verbinding informatie die nodig is tooconnect toohello Azure SQL-database worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="bec88-115">Get hello connection information needed tooconnect toohello Azure SQL database.</span></span> <span data-ttu-id="bec88-116">U moet Hallo volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures Hallo.</span><span class="sxs-lookup"><span data-stu-id="bec88-116">You will need hello fully qualified server name, database name, and login information in hello next procedures.</span></span>

1. <span data-ttu-id="bec88-117">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="bec88-117">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="bec88-118">Selecteer **SQL-Databases** Hallo links menu en klik op de database op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="bec88-118">Select **SQL Databases** from hello left-hand menu, and click your database on hello **SQL databases** page.</span></span> 
3. <span data-ttu-id="bec88-119">Op Hallo **overzicht** servernaam pagina voor de database, bekijk Hallo volledig gekwalificeerd zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="bec88-119">On hello **Overview** page for your database, review hello fully qualified server name as shown in hello following image.</span></span> <span data-ttu-id="bec88-120">U kunt de muisaanwijzer op Hallo server name toobring up Hallo **klikt u op toocopy** optie.</span><span class="sxs-lookup"><span data-stu-id="bec88-120">You can hover over hello server name toobring up hello **Click toocopy** option.</span></span> 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="bec88-122">Als u de aanmeldingsgegevens van uw Azure SQL Database-server bent vergeten, gaat u toohello SQL server pagina tooview Hallo beheerder databaseservernaam.</span><span class="sxs-lookup"><span data-stu-id="bec88-122">If you forget your Azure SQL Database server login information, navigate toohello SQL Database server page tooview hello server admin name.</span></span> <span data-ttu-id="bec88-123">Indien nodig, kunt u Hallo wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="bec88-123">You can reset hello password if necessary.</span></span>

5. <span data-ttu-id="bec88-124">Klik op **Databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="bec88-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="bec88-125">Bekijk Hallo voltooid **ADO.NET** verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="bec88-125">Review hello complete **ADO.NET** connection string.</span></span>

    ![ADO.NET-verbindingsreeks](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="bec88-127">U moet beschikken over een firewallregel voor het openbare IP-adres Hallo van Hallo-computer waarop u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="bec88-127">You must have a firewall rule in place for hello public IP address of hello computer on which you perform this tutorial.</span></span> <span data-ttu-id="bec88-128">Als u zich op een andere computer of een ander openbaar IP-adres hebben, maakt u een [serverniveau firewall-regel met Azure-portal Hallo](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="bec88-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using hello Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="bec88-129">Een nieuw Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="bec88-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="bec88-130">Kies in Visual Studio **File**, **New**, **Project**.</span><span class="sxs-lookup"><span data-stu-id="bec88-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="bec88-131">In Hallo **nieuw Project** dialoogvenster, en vouw **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="bec88-131">In hello **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="bec88-132">Selecteer **consoletoepassing** en voer *sqltest* voor Hallo projectnaam.</span><span class="sxs-lookup"><span data-stu-id="bec88-132">Select **Console App** and enter *sqltest* for hello project name.</span></span>
4. <span data-ttu-id="bec88-133">Klik op **OK** toocreate en open Hallo nieuw project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bec88-133">Click **OK** toocreate and open hello new project in Visual Studio</span></span>
4. <span data-ttu-id="bec88-134">Klik in Solution Explorer met de rechtermuisknop op **sqltest** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="bec88-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="bec88-135">Op Hallo **Bladeren**, zoekt u ```System.Data.SqlClient``` en, wanneer gevonden, selecteert u deze.</span><span class="sxs-lookup"><span data-stu-id="bec88-135">On hello **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="bec88-136">In Hallo **System.Data.SqlClient** pagina, klikt u op **installeren**.</span><span class="sxs-lookup"><span data-stu-id="bec88-136">In hello **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="bec88-137">Wanneer het Hallo-installatie is voltooid, Controleer Hallo wijzigingen en klik vervolgens op **OK** tooclose hello **Preview** venster.</span><span class="sxs-lookup"><span data-stu-id="bec88-137">When hello install completes, review hello changes and then click **OK** tooclose hello **Preview** window.</span></span> 
8. <span data-ttu-id="bec88-138">Als een venster voor **akkoord gaan met de licentie** wordt weergegeven, klikt u op **Ik ga akkoord**.</span><span class="sxs-lookup"><span data-stu-id="bec88-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-tooquery-sql-database"></a><span data-ttu-id="bec88-139">Code tooquery SQL-database invoegen</span><span class="sxs-lookup"><span data-stu-id="bec88-139">Insert code tooquery SQL database</span></span>
1. <span data-ttu-id="bec88-140">Te schakelen (of open indien nodig) **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="bec88-140">Switch too(or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="bec88-141">Vervang de inhoud Hallo van **Program.cs** Hello volgende code en voeg de juiste waarden Hallo voor uw server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="bec88-141">Replace hello contents of **Program.cs** with hello following code and add hello appropriate values for your server, database, user, and password.</span></span>

```csharp
using System;
using System.Data.SqlClient;
using System.Text;

namespace sqltest
{
    class Program
    {
        static void Main(string[] args)
        {
            try 
            { 
                SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder();
                builder.DataSource = "your_server.database.windows.net"; 
                builder.UserID = "your_user";            
                builder.Password = "your_password";     
                builder.InitialCatalog = "your_database";

                using (SqlConnection connection = new SqlConnection(builder.ConnectionString))
                {
                    Console.WriteLine("\nQuery data example:");
                    Console.WriteLine("=========================================\n");
                    
                    connection.Open();       
                    StringBuilder sb = new StringBuilder();
                    sb.Append("SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName ");
                    sb.Append("FROM [SalesLT].[ProductCategory] pc ");
                    sb.Append("JOIN [SalesLT].[Product] p ");
                    sb.Append("ON pc.productcategoryid = p.productcategoryid;");
                    String sql = sb.ToString();

                    using (SqlCommand command = new SqlCommand(sql, connection))
                    {
                        using (SqlDataReader reader = command.ExecuteReader())
                        {
                            while (reader.Read())
                            {
                                Console.WriteLine("{0} {1}", reader.GetString(0), reader.GetString(1));
                            }
                        }
                    }                    
                }
            }
            catch (SqlException e)
            {
                Console.WriteLine(e.ToString());
            }
            Console.ReadLine();
        }
    }
}
```

## <a name="run-hello-code"></a><span data-ttu-id="bec88-142">Hallo code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bec88-142">Run hello code</span></span>

1. <span data-ttu-id="bec88-143">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bec88-143">Press **F5** toorun hello application.</span></span>
2. <span data-ttu-id="bec88-144">Verifieer dat Hallo top 20 rijen worden geretourneerd en het venster Hallo-toepassing sluit.</span><span class="sxs-lookup"><span data-stu-id="bec88-144">Verify that hello top 20 rows are returned and then close hello application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bec88-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bec88-145">Next steps</span></span>

- <span data-ttu-id="bec88-146">Meer informatie over hoe te[en verbinding en een Azure SQL database met behulp van .NET core query](sql-database-connect-query-dotnet-core.md) op Windows/Linux/Mac OS.</span><span class="sxs-lookup"><span data-stu-id="bec88-146">Learn how too[connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="bec88-147">Meer informatie over [aan de slag met .NET Core op Windows/Linux/Mac-OS, via de opdrachtregel Hallo](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="bec88-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using hello command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="bec88-148">Meer informatie over hoe te[ontwerpen van uw eerste Azure SQL database met behulp van SSMS](sql-database-design-first-database.md) of [ontwerpen van uw eerste Azure SQL database met .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="bec88-148">Learn how too[Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="bec88-149">Raadpleeg de [.NET-documentatie](https://docs.microsoft.com/dotnet/) voor meer informatie over .NET.</span><span class="sxs-lookup"><span data-stu-id="bec88-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>

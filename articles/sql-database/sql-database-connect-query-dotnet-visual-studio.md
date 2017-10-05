---
title: Visual Studio en .NET gebruiken om een query uit te voeren voor een Azure SQL-database | Microsoft Docs
description: In dit onderwerp ziet u hoe u Visual Studio gebruikt om een programma te maken dat is verbonden met een Azure SQL-database, en hoe u een query voor deze database uitvoert met behulp van Transact-SQL-instructies.
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
ms.openlocfilehash: 105dab17823a7e7f6957a604833f4ecad35c14bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-net-c-with-visual-studio-to-connect-and-query-an-azure-sql-database"></a><span data-ttu-id="88246-103">.NET (C#) met Visual Studio gebruiken om verbinding te maken en query's uit te voeren voor een Azure SQL-database</span><span class="sxs-lookup"><span data-stu-id="88246-103">Use .NET (C#) with Visual Studio to connect and query an Azure SQL database</span></span>

<span data-ttu-id="88246-104">In deze beknopte zelfstudie wordt gedemonstreerd hoe u het [.NET Framework](https://www.microsoft.com/net/) gebruikt om een C#-programma te maken met Visual Studio dat verbinding maakt met een Azure SQL-database, en hoe u Transact-SQL-instructies gebruikt om een query uit te voeren voor gegevens.</span><span class="sxs-lookup"><span data-stu-id="88246-104">This quick start tutorial demonstrates how to use the [.NET framework](https://www.microsoft.com/net/) to create a C# program with Visual Studio to connect to an Azure SQL database and use Transact-SQL statements to query data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88246-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="88246-105">Prerequisites</span></span>

<span data-ttu-id="88246-106">Zorg ervoor dat u over het volgende beschikt om deze beknopte zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="88246-106">To complete this quick start tutorial, make sure you have the following:</span></span>

- <span data-ttu-id="88246-107">Een Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="88246-107">An Azure SQL database.</span></span> <span data-ttu-id="88246-108">In deze zelfstudie worden de resources gebruikt die u hebt gemaakt in een van deze Quick Starts:</span><span class="sxs-lookup"><span data-stu-id="88246-108">This quick start uses the resources created in one of these quick starts:</span></span> 

   - [<span data-ttu-id="88246-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="88246-109">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="88246-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="88246-110">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="88246-111">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="88246-111">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="88246-112">Een [firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) voor het openbare IP-adres van de computer die u gebruikt voor deze beknopte zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="88246-112">A [server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule) for the public IP address of the computer you use for this quick start tutorial.</span></span>
- <span data-ttu-id="88246-113">Een installatie van [Visual Studio Community 2017, Visual Studio Professional 2017 of Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="88246-113">An installation of [Visual Studio Community 2017, Visual Studio Professional 2017, or Visual Studio Enterprise 2017](https://www.visualstudio.com/downloads/).</span></span>

## <a name="sql-server-connection-information"></a><span data-ttu-id="88246-114">SQL Server-verbindingsgegevens</span><span class="sxs-lookup"><span data-stu-id="88246-114">SQL server connection information</span></span>

<span data-ttu-id="88246-115">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure SQL-database.</span><span class="sxs-lookup"><span data-stu-id="88246-115">Get the connection information needed to connect to the Azure SQL database.</span></span> <span data-ttu-id="88246-116">U hebt de volledig gekwalificeerde servernaam, databasenaam en aanmeldingsgegevens in de volgende procedures nodig.</span><span class="sxs-lookup"><span data-stu-id="88246-116">You will need the fully qualified server name, database name, and login information in the next procedures.</span></span>

1. <span data-ttu-id="88246-117">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="88246-117">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="88246-118">Selecteer **SQL-databases** in het menu links en klik op uw database op de pagina **SQL-databases**.</span><span class="sxs-lookup"><span data-stu-id="88246-118">Select **SQL Databases** from the left-hand menu, and click your database on the **SQL databases** page.</span></span> 
3. <span data-ttu-id="88246-119">Op de pagina **Overzicht** voor de database controleert u de volledig gekwalificeerde servernaam zoals in de volgende afbeelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="88246-119">On the **Overview** page for your database, review the fully qualified server name as shown in the following image.</span></span> <span data-ttu-id="88246-120">U kunt de cursor boven de servernaam houden om de optie **Klik om te kopiëren** naar boven te halen.</span><span class="sxs-lookup"><span data-stu-id="88246-120">You can hover over the server name to bring up the **Click to copy** option.</span></span> 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

4. <span data-ttu-id="88246-122">Als u de aanmeldingsgegevens voor uw Azure SQL Database-server bent vergeten, gaat u naar de SQL Database-serverpagina om de beheerdersnaam voor de server weer te geven.</span><span class="sxs-lookup"><span data-stu-id="88246-122">If you forget your Azure SQL Database server login information, navigate to the SQL Database server page to view the server admin name.</span></span> <span data-ttu-id="88246-123">U kunt, indien nodig, het wachtwoord opnieuw instellen.</span><span class="sxs-lookup"><span data-stu-id="88246-123">You can reset the password if necessary.</span></span>

5. <span data-ttu-id="88246-124">Klik op **Databaseverbindingsreeksen tonen**.</span><span class="sxs-lookup"><span data-stu-id="88246-124">Click **Show database connection strings**.</span></span>

6. <span data-ttu-id="88246-125">Bekijk de volledige **ADO.NET**-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="88246-125">Review the complete **ADO.NET** connection string.</span></span>

    ![ADO.NET-verbindingsreeks](./media/sql-database-connect-query-dotnet/adonet-connection-string.png)

> [!IMPORTANT]
> <span data-ttu-id="88246-127">U moet een firewallregel hebben ingesteld voor het openbare IP-adres van de computer waarop u deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="88246-127">You must have a firewall rule in place for the public IP address of the computer on which you perform this tutorial.</span></span> <span data-ttu-id="88246-128">Als u een andere computer gebruikt of een ander openbaar IP-adres hebt, maakt u een [firewallregel op serverniveau met behulp van Azure Portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="88246-128">If you are on a different computer or have a different public IP address, create a [server-level firewall rule using the Azure portal](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span> 
>
  
## <a name="create-a-new-visual-studio-project"></a><span data-ttu-id="88246-129">Een nieuw Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="88246-129">Create a new Visual Studio project</span></span>

1. <span data-ttu-id="88246-130">Kies in Visual Studio **File**, **New**, **Project**.</span><span class="sxs-lookup"><span data-stu-id="88246-130">In Visual Studio, choose **File**, **New**, **Project**.</span></span> 
2. <span data-ttu-id="88246-131">Ga naar het dialoogvenster **New Project** en vouw **Visual C#** uit.</span><span class="sxs-lookup"><span data-stu-id="88246-131">In the **New Project** dialog, and expand **Visual C#**.</span></span>
3. <span data-ttu-id="88246-132">Selecteer **Console App** en voer *sqltest* voor de projectnaam in.</span><span class="sxs-lookup"><span data-stu-id="88246-132">Select **Console App** and enter *sqltest* for the project name.</span></span>
4. <span data-ttu-id="88246-133">Klik op **OK** om het nieuwe project in Visual Studio te maken en te openen.</span><span class="sxs-lookup"><span data-stu-id="88246-133">Click **OK** to create and open the new project in Visual Studio</span></span>
4. <span data-ttu-id="88246-134">Klik in Solution Explorer met de rechtermuisknop op **sqltest** en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="88246-134">In Solution Explorer, right-click **sqltest** and click **Manage NuGet Packages**.</span></span> 
5. <span data-ttu-id="88246-135">Zoek in **Bladeren** naar ```System.Data.SqlClient``` en selecteer deze.</span><span class="sxs-lookup"><span data-stu-id="88246-135">On the **Browse**, search for ```System.Data.SqlClient``` and, when found, select it.</span></span>
6. <span data-ttu-id="88246-136">Klik op de pagina **System.Data.SqlClient** op **Installeren**.</span><span class="sxs-lookup"><span data-stu-id="88246-136">In the **System.Data.SqlClient** page, click **Install**.</span></span>
7. <span data-ttu-id="88246-137">Wanneer de installatie is voltooid, controleert u de wijzigingen en klikt u vervolgens op **OK** om het venster **Preview** te sluiten.</span><span class="sxs-lookup"><span data-stu-id="88246-137">When the install completes, review the changes and then click **OK** to close the **Preview** window.</span></span> 
8. <span data-ttu-id="88246-138">Als een venster voor **akkoord gaan met de licentie** wordt weergegeven, klikt u op **Ik ga akkoord**.</span><span class="sxs-lookup"><span data-stu-id="88246-138">If a **License Acceptance** window appears, click **I Accept**.</span></span>

## <a name="insert-code-to-query-sql-database"></a><span data-ttu-id="88246-139">Code invoegen om een query uit te voeren voor een SQL-database</span><span class="sxs-lookup"><span data-stu-id="88246-139">Insert code to query SQL database</span></span>
1. <span data-ttu-id="88246-140">Schakel over naar (of open indien nodig) **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="88246-140">Switch to (or open if necessary) **Program.cs**</span></span>

2. <span data-ttu-id="88246-141">Vervang de inhoud van **Program.cs** door de volgende code en voeg de juiste waarden toe voor de server, de database, de gebruiker en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="88246-141">Replace the contents of **Program.cs** with the following code and add the appropriate values for your server, database, user, and password.</span></span>

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

## <a name="run-the-code"></a><span data-ttu-id="88246-142">De code uitvoeren</span><span class="sxs-lookup"><span data-stu-id="88246-142">Run the code</span></span>

1. <span data-ttu-id="88246-143">Druk op **F5** om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="88246-143">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="88246-144">Controleer of de bovenste 20 rijen worden geretourneerd, en sluit vervolgens het toepassingsvenster.</span><span class="sxs-lookup"><span data-stu-id="88246-144">Verify that the top 20 rows are returned and then close the application window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88246-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88246-145">Next steps</span></span>

- <span data-ttu-id="88246-146">Meer informatie over [verbinding maken met en een query uitvoeren voor een Azure SQL-database met behulp van .NET Core](sql-database-connect-query-dotnet-core.md) in Windows/Linux/macOS.</span><span class="sxs-lookup"><span data-stu-id="88246-146">Learn how to [connect and query an Azure SQL database using .NET core](sql-database-connect-query-dotnet-core.md) on Windows/Linux/macOS.</span></span>  
- <span data-ttu-id="88246-147">Meer informatie over [Aan de slag met .NET Core in Windows/Linux/macOS met behulp van de opdrachtregel](/dotnet/core/tutorials/using-with-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="88246-147">Learn about [Getting started with .NET Core on Windows/Linux/macOS using the command line](/dotnet/core/tutorials/using-with-xplat-cli).</span></span>
- <span data-ttu-id="88246-148">Meer informatie over [Uw eerste Azure SQL-database ontwerpen met behulp van SSMS](sql-database-design-first-database.md) of [Uw eerste Azure SQL-database ontwerpen met behulp van .NET](sql-database-design-first-database-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="88246-148">Learn how to [Design your first Azure SQL database using SSMS](sql-database-design-first-database.md) or [Design your first Azure SQL database using .NET](sql-database-design-first-database-csharp.md).</span></span>
- <span data-ttu-id="88246-149">Raadpleeg de [.NET-documentatie](https://docs.microsoft.com/dotnet/) voor meer informatie over .NET.</span><span class="sxs-lookup"><span data-stu-id="88246-149">For more information about .NET, see [.NET documentation](https://docs.microsoft.com/dotnet/).</span></span>

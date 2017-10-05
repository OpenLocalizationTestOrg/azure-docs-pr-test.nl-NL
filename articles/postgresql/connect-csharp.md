---
title: Vanuit C# verbinding maken met Azure Database voor PostgreSQL | Microsoft Docs
description: Deze snelstartgids bevat een voorbeeld van C# (.NET)-code dat u kunt gebruiken om verbinding te maken met en gegevens op te vragen uit een Azure Database voor PostgreSQL.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: csharp
ms.topic: quickstart
ms.date: 06/23/2017
ms.openlocfilehash: 91e0269e310688dc88d139430ccf386a1d26a61c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-use-net-c-to-connect-and-query-data"></a><span data-ttu-id="8f45d-103">Azure Database voor PostgreSQL: .NET (C#) gebruiken om verbinding te maken en gegevens op te vragen</span><span class="sxs-lookup"><span data-stu-id="8f45d-103">Azure Database for PostgreSQL: Use .NET (C#) to connect and query data</span></span>
<span data-ttu-id="8f45d-104">In deze snelstartgids ziet u hoe u met behulp van een C#-toepassing verbinding maakt met een Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-104">This quickstart demonstrates how to connect to an Azure Database for PostgreSQL using a C# application.</span></span> <span data-ttu-id="8f45d-105">U ziet hier hoe u SQL-instructies gebruikt om gegevens in de database op te vragen, in te voegen, bij te werken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8f45d-105">It shows how to use SQL statements to query, insert, update, and delete data in the database.</span></span> <span data-ttu-id="8f45d-106">In de stappen van dit artikel wordt ervan uitgegaan dat u bekend bent met het ontwikkelen met C#, maar geen ervaring hebt met het werken met Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-106">The steps in this article assume that you are familiar with developing using C#, and that you are new to working with Azure Database for PostgreSQL.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f45d-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8f45d-107">Prerequisites</span></span>
<span data-ttu-id="8f45d-108">In deze snelstartgids worden de resources die in een van deze handleidingen zijn gemaakt, als uitgangspunt gebruikt:</span><span class="sxs-lookup"><span data-stu-id="8f45d-108">This quickstart uses the resources created in either of these guides as a starting point:</span></span>
- [<span data-ttu-id="8f45d-109">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="8f45d-109">Create DB - Portal</span></span>](quickstart-create-server-database-portal.md)
- [<span data-ttu-id="8f45d-110">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="8f45d-110">Create DB - CLI</span></span>](quickstart-create-server-database-azure-cli.md)

<span data-ttu-id="8f45d-111">U moet ook het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="8f45d-111">You also need to:</span></span>
- <span data-ttu-id="8f45d-112">Installeer [.NET Framework](https://www.microsoft.com/net/download).</span><span class="sxs-lookup"><span data-stu-id="8f45d-112">Install [.NET Framework](https://www.microsoft.com/net/download).</span></span> <span data-ttu-id="8f45d-113">Volg de stappen in het gekoppelde artikel om .NET specifiek voor uw platform (Windows, Ubuntu Linux en Mac OS) te installeren.</span><span class="sxs-lookup"><span data-stu-id="8f45d-113">Follow the steps in the linked article to install .NET specifically for your platform (Windows, Ubuntu Linux, or macOS).</span></span> 
- <span data-ttu-id="8f45d-114">Installeer [Visual Studio](https://www.visualstudio.com/downloads/) of Visual Studio Code om code in te voeren en te bewerken.</span><span class="sxs-lookup"><span data-stu-id="8f45d-114">Install [Visual Studio](https://www.visualstudio.com/downloads/) or Visual Studio Code to type and edit code.</span></span>
- <span data-ttu-id="8f45d-115">Installeer de bibliotheek [Npgsql](http://www.npgsql.org/doc/index.html) zoals hieronder wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="8f45d-115">Install [Npgsql](http://www.npgsql.org/doc/index.html) library as described below.</span></span>

## <a name="install-npgsql-references-into-your-visual-studio-solution"></a><span data-ttu-id="8f45d-116">Npgsql-verwijzingen installeren in uw Visual Studio-oplossing</span><span class="sxs-lookup"><span data-stu-id="8f45d-116">Install Npgsql references into your Visual Studio solution</span></span>
<span data-ttu-id="8f45d-117">Gebruik de open source ADO.Net-bibliotheek Npgsql om vanuit de C#-toepassing verbinding te maken met PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-117">To connect from the C# application to PostgreSQL, use the open source ADO.NET library called Npgsql.</span></span> <span data-ttu-id="8f45d-118">NuGet vergemakkelijkt het downloaden en beheren van de verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="8f45d-118">NuGet helps download and manage the references easily.</span></span>

1. <span data-ttu-id="8f45d-119">Maak als volgt een nieuwe C#-oplossing of open een bestaande:</span><span class="sxs-lookup"><span data-stu-id="8f45d-119">Create a new C# solution, or open an existing one:</span></span> 
   - <span data-ttu-id="8f45d-120">Maak in Visual Studio een oplossing door te klikken op het menu Bestand **Nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-120">Within Visual Studio, create a solution, by clicking File menu **New** > **Project**.</span></span>
   - <span data-ttu-id="8f45d-121">In het dialoogvenster Nieuw project vouwt u **Sjablonen** > **Visual C#** uit.</span><span class="sxs-lookup"><span data-stu-id="8f45d-121">In the New Project dialogue, expand **Templates** > **Visual C#**.</span></span> 
   - <span data-ttu-id="8f45d-122">Kies een geschikte sjabloon, bijvoorbeeld **Console-app (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-122">Choose an appropriate template such as **Console App (.NET Core)**.</span></span>

2. <span data-ttu-id="8f45d-123">Gebruik de Nuget Package Manager om Npgsql te installeren:</span><span class="sxs-lookup"><span data-stu-id="8f45d-123">Use the Nuget Package Manager to install Npgsql:</span></span>
   - <span data-ttu-id="8f45d-124">Klik in het menu **Extra** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-124">Click the **Tools** menu > **NuGet Package Manager** > **Package Manager Console**.</span></span>
   - <span data-ttu-id="8f45d-125">Typ `Install-Package Npgsql` in de **Package Manager Console**</span><span class="sxs-lookup"><span data-stu-id="8f45d-125">In the **Package Manager Console**, type `Install-Package Npgsql`</span></span>
   - <span data-ttu-id="8f45d-126">Met de installatieopdracht worden Npgsql.dll en de bijbehorende assembly's gedownload en als afhankelijkheden toegevoegd in de oplossing.</span><span class="sxs-lookup"><span data-stu-id="8f45d-126">The install command downloads the Npgsql.dll and related assemblies and adds them as dependencies in the solution.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="8f45d-127">Verbindingsgegevens ophalen</span><span class="sxs-lookup"><span data-stu-id="8f45d-127">Get connection information</span></span>
<span data-ttu-id="8f45d-128">Haal de verbindingsgegevens op die nodig zijn om verbinding te maken met de Azure Database voor PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-128">Get the connection information needed to connect to the Azure Database for PostgreSQL.</span></span> <span data-ttu-id="8f45d-129">U hebt de volledig gekwalificeerde servernaam en aanmeldingsreferenties nodig.</span><span class="sxs-lookup"><span data-stu-id="8f45d-129">You need the fully qualified server name and login credentials.</span></span>

1. <span data-ttu-id="8f45d-130">Meld u aan bij [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8f45d-130">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8f45d-131">Klik in het menu links in Azure Portal op **Alle resources** en zoek de server die u hebt gemaakt (bijvoorbeeld **mypgserver-20170401**).</span><span class="sxs-lookup"><span data-stu-id="8f45d-131">From the left-hand menu in Azure portal, click **All resources** and search for the server you have created, such as **mypgserver-20170401**.</span></span>
3. <span data-ttu-id="8f45d-132">Klik op de servernaam **mypgserver-20170401**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-132">Click the server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="8f45d-133">Selecteer de pagina **Overzicht** van de server.</span><span class="sxs-lookup"><span data-stu-id="8f45d-133">Select the server's **Overview** page.</span></span> <span data-ttu-id="8f45d-134">Noteer de **servernaam** en de **gebruikersnaam van de serverbeheerder**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-134">Make a note of the **Server name** and **Server admin login name**.</span></span>
 <span data-ttu-id="8f45d-135">![Azure Database voor PostgreSQL - Aanmeldgegevens van de serverbeheerder](./media/connect-csharp/1-connection-string.png)</span><span class="sxs-lookup"><span data-stu-id="8f45d-135">![Azure Database for PostgreSQL - Server Admin Login](./media/connect-csharp/1-connection-string.png)</span></span>
5. <span data-ttu-id="8f45d-136">Als u uw aanmeldingsgegevens voor de server bent vergeten, gaat u naar de pagina **Overzicht** om de aanmeldingsnaam van de serverbeheerder weer te geven en indien nodig het wachtwoord opnieuw in te stellen.</span><span class="sxs-lookup"><span data-stu-id="8f45d-136">If you forget your server login information, navigate to the **Overview** page to view the Server admin login name and, if necessary, reset the password.</span></span>

## <a name="connect-create-table-and-insert-data"></a><span data-ttu-id="8f45d-137">Verbinden, tabel maken en gegevens invoegen</span><span class="sxs-lookup"><span data-stu-id="8f45d-137">Connect, create table, and insert data</span></span>
<span data-ttu-id="8f45d-138">Gebruik de volgende code om verbinding te maken en de gegevens te laden met de SQL-instructies **CREATE TABLE** EN **INSERT INTO**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-138">Use the following code to connect and load the data using **CREATE TABLE** and  **INSERT INTO** SQL statements.</span></span> <span data-ttu-id="8f45d-139">In de code wordt de klasse NpgsqlCommand met de methode [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) gebruikt om een verbinding te maken met PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-139">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="8f45d-140">Vervolgens wordt de methode [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) gebruikt, de eigenschap CommandText ingesteld en de methode [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) aangeroepen om de databaseopdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8f45d-140">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span> 

<span data-ttu-id="8f45d-141">Vervang de parameters Host, DBName, User en Password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="8f45d-141">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresCreate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4}; SSL Mode=Prefer; Trust Server Certificate=true",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "DROP TABLE IF EXISTS inventory;";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished dropping table (if existed)");

            command.CommandText = "CREATE TABLE inventory (id serial PRIMARY KEY, name VARCHAR(50), quantity INTEGER);";
            command.ExecuteNonQuery();
            Console.Out.WriteLine("Finished creating table");

            command.CommandText =
                String.Format(
                    @"
                                INSERT INTO inventory (name, quantity) VALUES ({0}, {1});
                                INSERT INTO inventory (name, quantity) VALUES ({2}, {3});
                                INSERT INTO inventory (name, quantity) VALUES ({4}, {5});
                            ",
                    "\'banana\'", 150,
                    "\'orange\'", 154,
                    "\'apple\'", 100
                    );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows inserted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="read-data"></a><span data-ttu-id="8f45d-142">Gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="8f45d-142">Read data</span></span>
<span data-ttu-id="8f45d-143">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-143">Use the following code to connect and read the data using a **SELECT** SQL statement.</span></span> <span data-ttu-id="8f45d-144">In de code wordt de klasse NpgsqlCommand met de methode [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) gebruikt om een verbinding te maken met PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-144">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="8f45d-145">Vervolgens worden de methoden [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) en [ExecuteReader())](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) gebruikt om de databaseopdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8f45d-145">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) and method [ExecuteReader()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteReader) to run the database commands.</span></span> <span data-ttu-id="8f45d-146">Daarna wordt [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) gebruikt om naar de records in de resultaten te gaan.</span><span class="sxs-lookup"><span data-stu-id="8f45d-146">Next the code uses [Read()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_Read) to advance to the records in the results.</span></span> <span data-ttu-id="8f45d-147">Vervolgens wordt in de code [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) en [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) gebruikt om de waarden in de record te parseren.</span><span class="sxs-lookup"><span data-stu-id="8f45d-147">Then the code uses [GetInt32()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetInt32_System_Int32_) and [GetString()](http://www.npgsql.org/api/Npgsql.NpgsqlDataReader.html#Npgsql_NpgsqlDataReader_GetString_System_Int32_) to parse the values in the record.</span></span>

<span data-ttu-id="8f45d-148">Vervang de parameters Host, DBName, User en Password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="8f45d-148">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresRead
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText = "SELECT * FROM inventory;";

            var reader = command.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(
                    string.Format(
                        "Reading from table=({0}, {1}, {2})",
                        reader.GetInt32(0).ToString(),
                        reader.GetString(1),
                        reader.GetInt32(2).ToString()
                        )
                    );
            }

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```


## <a name="update-data"></a><span data-ttu-id="8f45d-149">Gegevens bijwerken</span><span class="sxs-lookup"><span data-stu-id="8f45d-149">Update data</span></span>
<span data-ttu-id="8f45d-150">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **UPDATE**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-150">Use the following code to connect and read the data using a **UPDATE** SQL statement.</span></span> <span data-ttu-id="8f45d-151">In de code wordt de klasse NpgsqlCommand met de methode [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) gebruikt om een verbinding te maken met PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-151">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="8f45d-152">Vervolgens wordt de methode [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) gebruikt, de eigenschap CommandText ingesteld en de methode [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) aangeroepen om de databaseopdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8f45d-152">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="8f45d-153">Vervang de parameters Host, DBName, User en Password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="8f45d-153">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresUpdate
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("UPDATE inventory SET quantity = {0} WHERE name = {1};",
                200,
                "\'banana\'"
                );

            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows updated={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```


## <a name="delete-data"></a><span data-ttu-id="8f45d-154">Gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="8f45d-154">Delete data</span></span>
<span data-ttu-id="8f45d-155">Gebruik de volgende code om verbinding te maken en de gegevens te lezen met de SQL-instructie **DELETE**.</span><span class="sxs-lookup"><span data-stu-id="8f45d-155">Use the following code to connect and read the data using a **DELETE** SQL statement.</span></span> 

 <span data-ttu-id="8f45d-156">In de code wordt de klasse NpgsqlCommand met de methode [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) gebruikt om een verbinding te maken met PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="8f45d-156">The code uses NpgsqlCommand class with method [Open()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_Open) to establish a connection to PostgreSQL.</span></span> <span data-ttu-id="8f45d-157">Vervolgens wordt de methode [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand) gebruikt, de eigenschap CommandText ingesteld en de methode [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) aangeroepen om de databaseopdrachten uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="8f45d-157">Then the code uses method [CreateCommand()](http://www.npgsql.org/api/Npgsql.NpgsqlConnection.html#Npgsql_NpgsqlConnection_CreateCommand), sets the CommandText property, and calls method [ExecuteNonQuery()](http://www.npgsql.org/api/Npgsql.NpgsqlCommand.html#Npgsql_NpgsqlCommand_ExecuteNonQuery) to run the database commands.</span></span>

<span data-ttu-id="8f45d-158">Vervang de parameters Host, DBName, User en Password door de waarden die u hebt opgegeven tijdens het maken van de server en database.</span><span class="sxs-lookup"><span data-stu-id="8f45d-158">Replace the Host, DBName, User, and Password parameters with the values that you specified when you created the server and database.</span></span> 

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Npgsql;

namespace Driver
{
    public class AzurePostgresDelete
    {
        // Obtain connection string information from the portal
        //
        private static string Host = "mypgserver-20170401.postgres.database.azure.com";
        private static string User = "mylogin@mypgserver-20170401";
        private static string DBname = "mypgsqldb";
        private static string Password = "<server_admin_password>";
        private static string Port = "5432";

        static void Main(string[] args)
        {
            // Build connection string using parameters from portal
            //
            string connString =
                String.Format(
                    "Server={0}; User Id={1}; Database={2}; Port={3}; Password={4};",
                    Host,
                    User,
                    DBname,
                    Port,
                    Password);

            var conn = new NpgsqlConnection(connString);

            Console.Out.WriteLine("Opening connection");
            conn.Open();

            var command = conn.CreateCommand();
            command.CommandText =
            String.Format("DELETE FROM inventory WHERE name = {0};",
                "\'orange\'");
            int nRows = command.ExecuteNonQuery();
            Console.Out.WriteLine(String.Format("Number of rows deleted={0}", nRows));

            Console.Out.WriteLine("Closing connection");
            conn.Close();

            Console.WriteLine("Press RETURN to exit");
            Console.ReadLine();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="8f45d-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f45d-159">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="8f45d-160">Een database migreren met behulp van Exporteren en importeren</span><span class="sxs-lookup"><span data-stu-id="8f45d-160">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)

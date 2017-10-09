
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a><span data-ttu-id="918a5-101">Voorbeeld van C#-programma</span><span class="sxs-lookup"><span data-stu-id="918a5-101">C# program example</span></span>

<span data-ttu-id="918a5-102">Hallo volgende secties van dit artikel vindt u een C#-programma dat gebruikmaakt van ADO.NET toosend Transact-SQL-instructies toohello SQL-database.</span><span class="sxs-lookup"><span data-stu-id="918a5-102">hello next sections of this article present a C# program that uses ADO.NET toosend Transact-SQL statements toohello SQL database.</span></span> <span data-ttu-id="918a5-103">Hallo C#-programma uitvoert Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="918a5-103">hello C# program performs hello following actions:</span></span>

1. <span data-ttu-id="918a5-104">[Maakt verbinding tooour SQL-database met ADO.NET](#cs_1_connect).</span><span class="sxs-lookup"><span data-stu-id="918a5-104">[Connects tooour SQL database using ADO.NET](#cs_1_connect).</span></span>
2. <span data-ttu-id="918a5-105">[Tabellen gemaakt](#cs_2_createtables).</span><span class="sxs-lookup"><span data-stu-id="918a5-105">[Creates tables](#cs_2_createtables).</span></span>
3. <span data-ttu-id="918a5-106">[Hallo-tabellen met gegevens, door uitgifte van INSERT T-SQL-instructies gevuld](#cs_3_insert).</span><span class="sxs-lookup"><span data-stu-id="918a5-106">[Populates hello tables with data, by issuing T-SQL INSERT statements](#cs_3_insert).</span></span>
4. <span data-ttu-id="918a5-107">[Updates van gegevens via het gebruik van een join](#cs_4_updatejoin).</span><span class="sxs-lookup"><span data-stu-id="918a5-107">[Updates data by use of a join](#cs_4_updatejoin).</span></span>
5. <span data-ttu-id="918a5-108">[Hiermee verwijdert u gegevens via het gebruik van een join](#cs_5_deletejoin).</span><span class="sxs-lookup"><span data-stu-id="918a5-108">[Deletes data by use of a join](#cs_5_deletejoin).</span></span>
6. <span data-ttu-id="918a5-109">[Rijen met gegevens via het gebruik van een join selecteert](#cs_6_selectrows).</span><span class="sxs-lookup"><span data-stu-id="918a5-109">[Selects data rows by use of a join](#cs_6_selectrows).</span></span>
7. <span data-ttu-id="918a5-110">Hallo-verbinding (die geen tijdelijke tabellen verwijderd van tempdb) sluit.</span><span class="sxs-lookup"><span data-stu-id="918a5-110">Closes hello connection (which drops any temporary tables from tempdb).</span></span>

<span data-ttu-id="918a5-111">Hallo C#-programma bevat:</span><span class="sxs-lookup"><span data-stu-id="918a5-111">hello C# program contains:</span></span>

- <span data-ttu-id="918a5-112">C#-code tooconnect toohello database.</span><span class="sxs-lookup"><span data-stu-id="918a5-112">C# code tooconnect toohello database.</span></span>
- <span data-ttu-id="918a5-113">Methoden die Hallo T-SQL-bron retourcode.</span><span class="sxs-lookup"><span data-stu-id="918a5-113">Methods that return hello T-SQL source code.</span></span>
- <span data-ttu-id="918a5-114">Twee methoden die Hallo T-SQL toohello database verzenden.</span><span class="sxs-lookup"><span data-stu-id="918a5-114">Two methods that submit hello T-SQL toohello database.</span></span>

#### <a name="toocompile-and-run"></a><span data-ttu-id="918a5-115">toocompile en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="918a5-115">toocompile and run</span></span>

<span data-ttu-id="918a5-116">Dit C#-programma is logisch één .cs-bestand.</span><span class="sxs-lookup"><span data-stu-id="918a5-116">This C# program is logically one .cs file.</span></span> <span data-ttu-id="918a5-117">Hier Hallo programma fysiek is onderverdeeld in meerdere codeblokken, toomake elk blok wordt gemakkelijker toosee en begrijpen.</span><span class="sxs-lookup"><span data-stu-id="918a5-117">But here hello program is physically divided into several code blocks, toomake each block easier toosee and understand.</span></span> <span data-ttu-id="918a5-118">toocompile en dit programma wordt uitgevoerd, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="918a5-118">toocompile and run this program, do hello following:</span></span>

1. <span data-ttu-id="918a5-119">Maak een C#-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="918a5-119">Create a C# project in Visual Studio.</span></span>
    - <span data-ttu-id="918a5-120">Hallo projecttype moet een *console* toepassing van ongeveer Hallo hiërarchie te volgen: **sjablonen** > **Visual C#** > **Classic Windows Desktop** > **Console-App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="918a5-120">hello project type should be a *console* application, from something like hello following hierarchy: **Templates** > **Visual C#** > **Windows Classic Desktop** > **Console App (.NET Framework)**.</span></span>
3. <span data-ttu-id="918a5-121">In Hallo bestand **Program.cs**, Hallo kleine starter regels code wilt wissen.</span><span class="sxs-lookup"><span data-stu-id="918a5-121">In hello file **Program.cs**, erase hello small starter lines of code.</span></span>
3. <span data-ttu-id="918a5-122">In Program.cs Hallo kopiëren en plakken van Hallo na blokken in dezelfde volgorde die ze hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="918a5-122">Into Program.cs, copy and paste each of hello following blocks, in hello same sequence they are presented here.</span></span>
4. <span data-ttu-id="918a5-123">In Program.cs-bewerken Hallo volgende waarden in Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="918a5-123">In Program.cs, edit hello following values in hello **Main** method:</span></span>

   - <span data-ttu-id="918a5-124">**CB. Gegevensbron**</span><span class="sxs-lookup"><span data-stu-id="918a5-124">**cb.DataSource**</span></span>
   - <span data-ttu-id="918a5-125">**cd. Gebruikers-id**</span><span class="sxs-lookup"><span data-stu-id="918a5-125">**cd.UserID**</span></span>
   - <span data-ttu-id="918a5-126">**CB. Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="918a5-126">**cb.Password**</span></span>
   - <span data-ttu-id="918a5-127">**InitialCatalog**</span><span class="sxs-lookup"><span data-stu-id="918a5-127">**InitialCatalog**</span></span>

5. <span data-ttu-id="918a5-128">Die assembly Hallo controleren **System.Data.dll** wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="918a5-128">Verify that hello assembly **System.Data.dll** is referenced.</span></span> <span data-ttu-id="918a5-129">tooverify, vouw Hallo **verwijzingen** knooppunt in Hallo **Solution Explorer** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="918a5-129">tooverify, expand hello **References** node in hello **Solution Explorer** pane.</span></span>
6. <span data-ttu-id="918a5-130">toobuild hello programma in Visual Studio, klikt u op Hallo **bouwen** menu.</span><span class="sxs-lookup"><span data-stu-id="918a5-130">toobuild hello program in Visual Studio, click hello **Build** menu.</span></span>
7. <span data-ttu-id="918a5-131">toorun hello programma vanuit Visual Studio, klikt u op Hallo **Start** knop.</span><span class="sxs-lookup"><span data-stu-id="918a5-131">toorun hello program from Visual Studio, click hello **Start** button.</span></span> <span data-ttu-id="918a5-132">Hallo rapportuitvoer wordt weergegeven in een venster cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="918a5-132">hello report output is displayed in a cmd.exe window.</span></span>

> [!NOTE]
> <span data-ttu-id="918a5-133">U hebt de optie Hallo Hallo T-SQL-tooadd geen voorlooptekens bewerken  **#**  toohello tabelnamen, dat deze als tijdelijke tabellen in maakt **tempdb**.</span><span class="sxs-lookup"><span data-stu-id="918a5-133">You have hello option of editing hello T-SQL tooadd a leading **#** toohello table names, which creates them as temporary tables in **tempdb**.</span></span> <span data-ttu-id="918a5-134">Dit is handig voor demonstratiedoeleinden, wanneer er geen testdatabase beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="918a5-134">This can be useful for demonstration purposes, when no test database is available.</span></span> <span data-ttu-id="918a5-135">Tijdelijke tabellen worden automatisch verwijderd wanneer Hallo verbinding wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="918a5-135">Temporary tables are deleted automatically when hello connection closes.</span></span> <span data-ttu-id="918a5-136">Alle verwijzingen van refererende sleutels worden niet afgedwongen voor tijdelijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="918a5-136">Any REFERENCES for foreign keys are not enforced for temporary tables.</span></span>
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a><span data-ttu-id="918a5-137">C# blok 1: verbinding maken met behulp van de ADO.NET</span><span class="sxs-lookup"><span data-stu-id="918a5-137">C# block 1: Connect by using ADO.NET</span></span>

- [<span data-ttu-id="918a5-138">Volgende</span><span class="sxs-lookup"><span data-stu-id="918a5-138">Next</span></span>](#cs_2_createtables)


```csharp
using System;
using System.Data.SqlClient;   // System.Data.dll 
//using System.Data;           // For:  SqlDbType , ParameterDirection

namespace csharp_db_test
{
   class Program
   {
      static void Main(string[] args)
      {
         try
         {
            var cb = new SqlConnectionStringBuilder();
            cb.DataSource = "your_server.database.windows.net";
            cb.UserID = "your_user";
            cb.Password = "your_password";
            cb.InitialCatalog = "your_database";

            using (var connection = new SqlConnection(cb.ConnectionString))
            {
               connection.Open();

               Submit_Tsql_NonQuery(connection, "2 - Create-Tables",
                  Build_2_Tsql_CreateTables());

               Submit_Tsql_NonQuery(connection, "3 - Inserts",
                  Build_3_Tsql_Inserts());

               Submit_Tsql_NonQuery(connection, "4 - Update-Join",
                  Build_4_Tsql_UpdateJoin(),
                  "@csharpParmDepartmentName", "Accounting");

               Submit_Tsql_NonQuery(connection, "5 - Delete-Join",
                  Build_5_Tsql_DeleteJoin(),
                  "@csharpParmDepartmentName", "Legal");

               Submit_6_Tsql_SelectEmployees(connection);
            }
         }
         catch (SqlException e)
         {
            Console.WriteLine(e.ToString());
         }
         Console.WriteLine("View hello report output here, then press any key tooend hello program...");
         Console.ReadKey();
      }
```


<a name="cs_2_createtables"/>
### <a name="c-block-2-t-sql-toocreate-tables"></a><span data-ttu-id="918a5-139">C# blok 2: T-SQL toocreate tabellen</span><span class="sxs-lookup"><span data-stu-id="918a5-139">C# block 2: T-SQL toocreate tables</span></span>

- <span data-ttu-id="918a5-140">[Vorige](#cs_1_connect) &nbsp;  /  &nbsp; [volgende](#cs_3_insert)</span><span class="sxs-lookup"><span data-stu-id="918a5-140">[Previous](#cs_1_connect) &nbsp; / &nbsp; [Next](#cs_3_insert)</span></span>

```csharp
      static string Build_2_Tsql_CreateTables()
      {
         return @"
DROP TABLE IF EXISTS tabEmployee;
DROP TABLE IF EXISTS tabDepartment;  -- Drop parent table last.


CREATE TABLE tabDepartment
(
   DepartmentCode  nchar(4)          not null
      PRIMARY KEY,
   DepartmentName  nvarchar(128)     not null
);

CREATE TABLE tabEmployee
(
   EmployeeGuid    uniqueIdentifier  not null  default NewId()
      PRIMARY KEY,
   EmployeeName    nvarchar(128)     not null,
   EmployeeLevel   int               not null,
   DepartmentCode  nchar(4)              null
      REFERENCES tabDepartment (DepartmentCode)  -- (REFERENCES would be disallowed on temporary tables.)
);
";
      }
```

#### <a name="entity-relationship-diagram-erd"></a><span data-ttu-id="918a5-141">Diagram van relatie tussen (ERD)</span><span class="sxs-lookup"><span data-stu-id="918a5-141">Entity Relationship Diagram (ERD)</span></span>

<span data-ttu-id="918a5-142">Hallo voorgaande CREATE TABLE-instructies hebben betrekking op Hallo **verwijzingen** sleutelwoord toocreate een *refererende sleutel* (FK) relatie tussen twee tabellen.</span><span class="sxs-lookup"><span data-stu-id="918a5-142">hello preceding CREATE TABLE statements involve hello **REFERENCES** keyword toocreate a *foreign key* (FK) relationship between two tables.</span></span>  <span data-ttu-id="918a5-143">Als u van tempdb gebruikmaakt, uitcommentariëren hello `--REFERENCES` sleutelwoord met behulp van een combinatie van toonaangevende streepjes.</span><span class="sxs-lookup"><span data-stu-id="918a5-143">If you are using tempdb, comment out hello `--REFERENCES` keyword using a pair of leading dashes.</span></span>

<span data-ttu-id="918a5-144">Hierna volgt een Noodhersteldiskette waarin Hallo relatie tussen twee tabellen hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="918a5-144">Next is an ERD that displays hello relationship between hello two tables.</span></span> <span data-ttu-id="918a5-145">Hallo-waarden in Hallo #tabEmployee.DepartmentCode *onderliggende* kolom zijn beperkt toohello waarden aanwezig zijn in Hallo #tabDepartment.Department *bovenliggende* kolom.</span><span class="sxs-lookup"><span data-stu-id="918a5-145">hello values in hello #tabEmployee.DepartmentCode *child* column are limited toohello values present in hello #tabDepartment.Department *parent* column.</span></span>

![Refererende sleutel van ERD weergeven](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a><span data-ttu-id="918a5-147">C# blok 3: T-SQL tooinsert gegevens</span><span class="sxs-lookup"><span data-stu-id="918a5-147">C# block 3: T-SQL tooinsert data</span></span>

- <span data-ttu-id="918a5-148">[Vorige](#cs_2_createtables) &nbsp;  /  &nbsp; [volgende](#cs_4_updatejoin)</span><span class="sxs-lookup"><span data-stu-id="918a5-148">[Previous](#cs_2_createtables) &nbsp; / &nbsp; [Next](#cs_4_updatejoin)</span></span>


```csharp
      static string Build_3_Tsql_Inserts()
      {
         return @"
-- hello company has these departments.
INSERT INTO tabDepartment
   (DepartmentCode, DepartmentName)
      VALUES
   ('acct', 'Accounting'),
   ('hres', 'Human Resources'),
   ('legl', 'Legal');

-- hello company has these employees, each in one department.
INSERT INTO tabEmployee
   (EmployeeName, EmployeeLevel, DepartmentCode)
      VALUES
   ('Alison'  , 19, 'acct'),
   ('Barbara' , 17, 'hres'),
   ('Carol'   , 21, 'acct'),
   ('Deborah' , 24, 'legl'),
   ('Elle'    , 15, null);
";
      }
```


<a name="cs_4_updatejoin"/>
### <a name="c-block-4-t-sql-tooupdate-join"></a><span data-ttu-id="918a5-149">C# blok 4: tooupdate T-SQL-join</span><span class="sxs-lookup"><span data-stu-id="918a5-149">C# block 4: T-SQL tooupdate-join</span></span>

- <span data-ttu-id="918a5-150">[Vorige](#cs_3_insert) &nbsp;  /  &nbsp; [volgende](#cs_5_deletejoin)</span><span class="sxs-lookup"><span data-stu-id="918a5-150">[Previous](#cs_3_insert) &nbsp; / &nbsp; [Next](#cs_5_deletejoin)</span></span>


```csharp
      static string Build_4_Tsql_UpdateJoin()
      {
         return @"
DECLARE @DName1  nvarchar(128) = @csharpParmDepartmentName;  --'Accounting';


-- Promote everyone in one department (see @parm...).
UPDATE empl
   SET
      empl.EmployeeLevel += 1
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName1;
";
      }
```


<a name="cs_5_deletejoin"/>
### <a name="c-block-5-t-sql-toodelete-join"></a><span data-ttu-id="918a5-151">C# blok 5: toodelete T-SQL-join</span><span class="sxs-lookup"><span data-stu-id="918a5-151">C# block 5: T-SQL toodelete-join</span></span>

- <span data-ttu-id="918a5-152">[Vorige](#cs_4_updatejoin) &nbsp;  /  &nbsp; [volgende](#cs_6_selectrows)</span><span class="sxs-lookup"><span data-stu-id="918a5-152">[Previous](#cs_4_updatejoin) &nbsp; / &nbsp; [Next](#cs_6_selectrows)</span></span>


```csharp
      static string Build_5_Tsql_DeleteJoin()
      {
         return @"
DECLARE @DName2  nvarchar(128);
SET @DName2 = @csharpParmDepartmentName;  --'Legal';


-- Right size hello Legal department.
DELETE empl
   FROM
      tabEmployee   as empl
      INNER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   WHERE
      dept.DepartmentName = @DName2

-- Disband hello Legal department.
DELETE tabDepartment
   WHERE DepartmentName = @DName2;
";
      }
```



<a name="cs_6_selectrows"/>
### <a name="c-block-6-t-sql-tooselect-rows"></a><span data-ttu-id="918a5-153">C# blok 6: T-SQL tooselect rijen</span><span class="sxs-lookup"><span data-stu-id="918a5-153">C# block 6: T-SQL tooselect rows</span></span>

- <span data-ttu-id="918a5-154">[Vorige](#cs_5_deletejoin) &nbsp;  /  &nbsp; [volgende](#cs_6b_datareader)</span><span class="sxs-lookup"><span data-stu-id="918a5-154">[Previous](#cs_5_deletejoin) &nbsp; / &nbsp; [Next](#cs_6b_datareader)</span></span>


```csharp
      static string Build_6_Tsql_SelectEmployees()
      {
         return @"
-- Look at all hello final Employees.
SELECT
      empl.EmployeeGuid,
      empl.EmployeeName,
      empl.EmployeeLevel,
      empl.DepartmentCode,
      dept.DepartmentName
   FROM
      tabEmployee   as empl
      LEFT OUTER JOIN
      tabDepartment as dept ON dept.DepartmentCode = empl.DepartmentCode
   ORDER BY
      EmployeeName;
";
      }
```


<a name="cs_6b_datareader"/>
### <a name="c-block-6b-executereader"></a><span data-ttu-id="918a5-155">C# blok 6 ter: ExecuteReader</span><span class="sxs-lookup"><span data-stu-id="918a5-155">C# block 6b: ExecuteReader</span></span>

- <span data-ttu-id="918a5-156">[Vorige](#cs_6_selectrows) &nbsp;  /  &nbsp; [volgende](#cs_7_executenonquery)</span><span class="sxs-lookup"><span data-stu-id="918a5-156">[Previous](#cs_6_selectrows) &nbsp; / &nbsp; [Next](#cs_7_executenonquery)</span></span>

<span data-ttu-id="918a5-157">Deze methode is ontworpen toorun Hallo T-SQL SELECT-instructie die is gebouwd door Hallo **Build_6_Tsql_SelectEmployees** methode.</span><span class="sxs-lookup"><span data-stu-id="918a5-157">This method is designed toorun hello T-SQL SELECT statement that is built by hello **Build_6_Tsql_SelectEmployees** method.</span></span>


```csharp
      static void Submit_6_Tsql_SelectEmployees(SqlConnection connection)
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("Now, SelectEmployees (6)...");

         string tsql = Build_6_Tsql_SelectEmployees();

         using (var command = new SqlCommand(tsql, connection))
         {
            using (SqlDataReader reader = command.ExecuteReader())
            {
               while (reader.Read())
               {
                  Console.WriteLine("{0} , {1} , {2} , {3} , {4}",
                     reader.GetGuid(0),
                     reader.GetString(1),
                     reader.GetInt32(2),
                     (reader.IsDBNull(3)) ? "NULL" : reader.GetString(3),
                     (reader.IsDBNull(4)) ? "NULL" : reader.GetString(4));
               }
            }
         }
      }
```


<a name="cs_7_executenonquery"/>
### <a name="c-block-7-executenonquery"></a><span data-ttu-id="918a5-158">C# blok 7: ExecuteNonQuery</span><span class="sxs-lookup"><span data-stu-id="918a5-158">C# block 7: ExecuteNonQuery</span></span>

- <span data-ttu-id="918a5-159">[Vorige](#cs_6b_datareader) &nbsp;  /  &nbsp; [volgende](#cs_8_output)</span><span class="sxs-lookup"><span data-stu-id="918a5-159">[Previous](#cs_6b_datareader) &nbsp; / &nbsp; [Next](#cs_8_output)</span></span>

<span data-ttu-id="918a5-160">Deze methode is aangeroepen voor bewerkingen waarvoor inhoudsgegevens Hallo van tabellen zonder gegevensrijen terug te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="918a5-160">This method is called for operations that modify hello data content of tables without returning any data rows.</span></span>


```csharp
      static void Submit_Tsql_NonQuery(
         SqlConnection connection,
         string tsqlPurpose,
         string tsqlSourceCode,
         string parameterName = null,
         string parameterValue = null
         )
      {
         Console.WriteLine();
         Console.WriteLine("=================================");
         Console.WriteLine("T-SQL too{0}...", tsqlPurpose);

         using (var command = new SqlCommand(tsqlSourceCode, connection))
         {
            if (parameterName != null)
            {
               command.Parameters.AddWithValue(  // Or, use SqlParameter class.
                  parameterName,
                  parameterValue);
            }
            int rowsAffected = command.ExecuteNonQuery();
            Console.WriteLine(rowsAffected + " = rows affected.");
         }
      }
   } // EndOfClass
}
```


<a name="cs_8_output"/>
### <a name="c-block-8-actual-test-output-toohello-console"></a><span data-ttu-id="918a5-161">C# blok 8: werkelijke test uitvoer toohello console</span><span class="sxs-lookup"><span data-stu-id="918a5-161">C# block 8: Actual test output toohello console</span></span>

- [<span data-ttu-id="918a5-162">Vorige</span><span class="sxs-lookup"><span data-stu-id="918a5-162">Previous</span></span>](#cs_7_executenonquery)

<span data-ttu-id="918a5-163">Deze sectie wordt Hallo-uitvoer die wordt verzonden toohello console Hallo vastgelegd.</span><span class="sxs-lookup"><span data-stu-id="918a5-163">This section captures hello output that hello program sent toohello console.</span></span> <span data-ttu-id="918a5-164">Alleen Hallo guid-waarden verschillen tussen de test wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="918a5-164">Only hello guid values vary between test runs.</span></span>


```text
[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>> csharp_db_test.exe

=================================
Now, CreateTables (10)...

=================================
Now, Inserts (20)...

=================================
Now, UpdateJoin (30)...
2 rows affected, by UpdateJoin.

=================================
Now, DeleteJoin (40)...

=================================
Now, SelectEmployees (50)...
0199be49-a2ed-4e35-94b7-e936acf1cd75 , Alison , 20 , acct , Accounting
f0d3d147-64cf-4420-b9f9-76e6e0a32567 , Barbara , 17 , hres , Human Resources
cf4caede-e237-42d2-b61d-72114c7e3afa , Carol , 22 , acct , Accounting
cdde7727-bcfd-4f72-a665-87199c415f8b , Elle , 15 , NULL , NULL

[C:\csharp_db_test\csharp_db_test\bin\Debug\]
>>
```

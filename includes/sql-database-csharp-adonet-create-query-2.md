
<a name="cs_0_csharpprogramexample_h2"/>

## <a name="c-program-example"></a>Voorbeeld van C#-programma

Hallo volgende secties van dit artikel vindt u een C#-programma dat gebruikmaakt van ADO.NET toosend Transact-SQL-instructies toohello SQL-database. Hallo C#-programma uitvoert Hallo van de volgende activiteiten:

1. [Maakt verbinding tooour SQL-database met ADO.NET](#cs_1_connect).
2. [Tabellen gemaakt](#cs_2_createtables).
3. [Hallo-tabellen met gegevens, door uitgifte van INSERT T-SQL-instructies gevuld](#cs_3_insert).
4. [Updates van gegevens via het gebruik van een join](#cs_4_updatejoin).
5. [Hiermee verwijdert u gegevens via het gebruik van een join](#cs_5_deletejoin).
6. [Rijen met gegevens via het gebruik van een join selecteert](#cs_6_selectrows).
7. Hallo-verbinding (die geen tijdelijke tabellen verwijderd van tempdb) sluit.

Hallo C#-programma bevat:

- C#-code tooconnect toohello database.
- Methoden die Hallo T-SQL-bron retourcode.
- Twee methoden die Hallo T-SQL toohello database verzenden.

#### <a name="toocompile-and-run"></a>toocompile en uitvoeren

Dit C#-programma is logisch één .cs-bestand. Hier Hallo programma fysiek is onderverdeeld in meerdere codeblokken, toomake elk blok wordt gemakkelijker toosee en begrijpen. toocompile en dit programma wordt uitgevoerd, Hallo te volgen:

1. Maak een C#-project in Visual Studio.
    - Hallo projecttype moet een *console* toepassing van ongeveer Hallo hiërarchie te volgen: **sjablonen** > **Visual C#** > **Classic Windows Desktop** > **Console-App (.NET Framework)**.
3. In Hallo bestand **Program.cs**, Hallo kleine starter regels code wilt wissen.
3. In Program.cs Hallo kopiëren en plakken van Hallo na blokken in dezelfde volgorde die ze hier wordt weergegeven.
4. In Program.cs-bewerken Hallo volgende waarden in Hallo **Main** methode:

   - **CB. Gegevensbron**
   - **cd. Gebruikers-id**
   - **CB. Wachtwoord**
   - **InitialCatalog**

5. Die assembly Hallo controleren **System.Data.dll** wordt verwezen. tooverify, vouw Hallo **verwijzingen** knooppunt in Hallo **Solution Explorer** deelvenster.
6. toobuild hello programma in Visual Studio, klikt u op Hallo **bouwen** menu.
7. toorun hello programma vanuit Visual Studio, klikt u op Hallo **Start** knop. Hallo rapportuitvoer wordt weergegeven in een venster cmd.exe.

> [!NOTE]
> U hebt de optie Hallo Hallo T-SQL-tooadd geen voorlooptekens bewerken  **#**  toohello tabelnamen, dat deze als tijdelijke tabellen in maakt **tempdb**. Dit is handig voor demonstratiedoeleinden, wanneer er geen testdatabase beschikbaar is. Tijdelijke tabellen worden automatisch verwijderd wanneer Hallo verbinding wordt gesloten. Alle verwijzingen van refererende sleutels worden niet afgedwongen voor tijdelijke tabellen.
>

<a name="cs_1_connect"/>
### <a name="c-block-1-connect-by-using-adonet"></a>C# blok 1: verbinding maken met behulp van de ADO.NET

- [Volgende](#cs_2_createtables)


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
### <a name="c-block-2-t-sql-toocreate-tables"></a>C# blok 2: T-SQL toocreate tabellen

- [Vorige](#cs_1_connect) &nbsp;  /  &nbsp; [volgende](#cs_3_insert)

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

#### <a name="entity-relationship-diagram-erd"></a>Diagram van relatie tussen (ERD)

Hallo voorgaande CREATE TABLE-instructies hebben betrekking op Hallo **verwijzingen** sleutelwoord toocreate een *refererende sleutel* (FK) relatie tussen twee tabellen.  Als u van tempdb gebruikmaakt, uitcommentariëren hello `--REFERENCES` sleutelwoord met behulp van een combinatie van toonaangevende streepjes.

Hierna volgt een Noodhersteldiskette waarin Hallo relatie tussen twee tabellen hello wordt weergegeven. Hallo-waarden in Hallo #tabEmployee.DepartmentCode *onderliggende* kolom zijn beperkt toohello waarden aanwezig zijn in Hallo #tabDepartment.Department *bovenliggende* kolom.

![Refererende sleutel van ERD weergeven](./media/sql-database-csharp-adonet-create-query-2/erd-dept-empl-fky-2.png)


<a name="cs_3_insert"/>
### <a name="c-block-3-t-sql-tooinsert-data"></a>C# blok 3: T-SQL tooinsert gegevens

- [Vorige](#cs_2_createtables) &nbsp;  /  &nbsp; [volgende](#cs_4_updatejoin)


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
### <a name="c-block-4-t-sql-tooupdate-join"></a>C# blok 4: tooupdate T-SQL-join

- [Vorige](#cs_3_insert) &nbsp;  /  &nbsp; [volgende](#cs_5_deletejoin)


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
### <a name="c-block-5-t-sql-toodelete-join"></a>C# blok 5: toodelete T-SQL-join

- [Vorige](#cs_4_updatejoin) &nbsp;  /  &nbsp; [volgende](#cs_6_selectrows)


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
### <a name="c-block-6-t-sql-tooselect-rows"></a>C# blok 6: T-SQL tooselect rijen

- [Vorige](#cs_5_deletejoin) &nbsp;  /  &nbsp; [volgende](#cs_6b_datareader)


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
### <a name="c-block-6b-executereader"></a>C# blok 6 ter: ExecuteReader

- [Vorige](#cs_6_selectrows) &nbsp;  /  &nbsp; [volgende](#cs_7_executenonquery)

Deze methode is ontworpen toorun Hallo T-SQL SELECT-instructie die is gebouwd door Hallo **Build_6_Tsql_SelectEmployees** methode.


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
### <a name="c-block-7-executenonquery"></a>C# blok 7: ExecuteNonQuery

- [Vorige](#cs_6b_datareader) &nbsp;  /  &nbsp; [volgende](#cs_8_output)

Deze methode is aangeroepen voor bewerkingen waarvoor inhoudsgegevens Hallo van tabellen zonder gegevensrijen terug te wijzigen.


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
### <a name="c-block-8-actual-test-output-toohello-console"></a>C# blok 8: werkelijke test uitvoer toohello console

- [Vorige](#cs_7_executenonquery)

Deze sectie wordt Hallo-uitvoer die wordt verzonden toohello console Hallo vastgelegd. Alleen Hallo guid-waarden verschillen tussen de test wordt uitgevoerd.


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


<!--
includes/sql-database-include-connection-string-20-portalshots.md

Latest Freshness check:  2015-09-02 , GeneMi.

## Connection string
-->


### <a name="obtain-hello-connection-string-from-hello-azure-portal"></a>Hallo-verbindingsreeks ophalen met hello Azure-portal
Gebruik Hallo [Azure-portal](https://portal.azure.com/) tooobtain Hallo-verbindingsreeks nodig zijn voor uw client programma toointeract met Azure SQL Database: 

1. Klik op **Bladeren** > **SQL-databases**.
2. Hallo-naam van uw database invoeren in Hallo filter in het tekstvak in de buurt van de linkerbovenhoek Hallo Hallo **SQL-databases** blade.
3. Klik op de rij Hallo voor uw database.
4. Nadat Hallo blade wordt weergegeven voor uw database, visual gemak klikt u op Hallo standaard minimaliseren besturingselementen toocollapse Hallo blades u gebruikt voor bladeren en het filteren van de database. 
   
    ![Filteren tooisolate uw database][10-FilterDatabase]
5. Klik op de blade voor uw database Hallo **databaseverbindingsreeksen tonen**.
6. Als u van plan toouse Hallo ADO.NET verbindingsbibliotheek bent, kopieert u Hallo tekenreeks met het label **ADO**. 
   
    ![Hallo ADO-verbindingsreeks voor uw database kopiëren][20-CopyAdoConnectionString]
7. In een indeling of een andere Hallo verbindingsinformatie in uw clientcode programma te plakken.

Zie voor meer informatie:<br/>[Verbindingsreeksen en configuratiebestanden](http://msdn.microsoft.com/library/ms254494.aspx).

<!-- Image references. -->

[10-FilterDatabase]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-a.png

[20-CopyAdoConnectionString]: ./media/sql-database-include-connection-string-20-portalshots/connqry-connstr-b.png


<!--
These three includes/ files are a sequenced set, but you can pick and choose:

includes/sql-database-include-connection-string-20-portalshots.md
includes/sql-database-include-connection-string-30-compare.md
includes/sql-database-include-connection-string-40-config.md
-->

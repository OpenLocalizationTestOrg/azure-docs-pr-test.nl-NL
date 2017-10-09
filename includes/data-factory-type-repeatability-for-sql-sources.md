## <a name="repeatability-during-copy"></a>Herhaalbaarheid tijdens het kopiëren
Wanneer een behoeften tookeep herhaalbaarheid kopiëren van gegevens tooAzure SQL/SQL-Server van andere gegevens opslaat in gedachten tooavoid ongewenste resultaten. 

Bij het kopiëren van gegevens tooAzure SQL/SQL Server-Database, wordt de kopieerbewerking door standaard APPEND Hallo gegevensset toohello sink tabel standaard. Bijvoorbeeld, bij het kopiëren van gegevens uit een CSV (door komma's gescheiden waarden) bestand gegevensbron met twee registreert tooAzure SQL/SQL Server-Database, is dit welke Hallo tabel lijkt:

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
```

Stel dat u fouten in het bronbestand als het aantal bijgewerkte Hallo omlaag buis van 2 too4 gevonden in het bronbestand Hallo. Als u het gegevenssegment Hallo opnieuw voor deze periode uitvoeren, vindt u twee nieuwe records tooAzure SQL/SQL Server-Database toegevoegd. Hallo hieronder wordt ervan uitgegaan dat geen van de kolommen in tabel Hallo HALLO hallo primary key-beperking heeft.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    2            2015-05-01 00:00:00
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

tooavoid, moet u toospecify UPSERT semantiek dankzij het gebruik van een van de Hallo hieronder 2 mechanismen die hieronder vermeld.

> [!NOTE]
> Een segment kan automatisch worden opnieuw uitgevoerd in Azure Data Factory volgens het beleid voor opnieuw proberen Hallo opgegeven.
> 
> 

### <a name="mechanism-1"></a>Methode 1
U kunt gebruikmaken van **sqlWriterCleanupScript** eigenschap toofirst opschonen actie uitvoeren wanneer een segment wordt uitgevoerd. 

```json
"sink":  
{ 
  "type": "SqlSink", 
  "sqlWriterCleanupScript": "$$Text.Format('DELETE FROM table WHERE ModifiedDate >= \\'{0:yyyy-MM-dd HH:mm}\\' AND ModifiedDate < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
}
```

Hallo script voor opschoning zou worden uitgevoerd tijdens het kopiëren van een bepaald segment die Hallo gegevens uit Hallo SQL-tabel overeenkomende toothat segment verwijderen zou eerste. Hallo-activiteit wordt vervolgens Hallo gegevens invoegen in Hallo SQL-tabel. 

Als het Hallo-segment is nu opnieuw uitvoeren, dan hebt u Hallo hoeveelheid wordt bijgewerkt vindt als gewenst.

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
6    Flat Washer    3            2015-05-01 00:00:00
7     Down Tube    4            2015-05-01 00:00:00
```

Stel Hallo platte was record wordt verwijderd uit de oorspronkelijke csv Hallo. Vervolgens resulteert opnieuw uit te voeren Hallo segment Hallo resultaat te volgen: 

```
ID    Product        Quantity    ModifiedDate
...    ...            ...            ...
7     Down Tube    4            2015-05-01 00:00:00
```
Niets nieuwe had toobe gedaan. Hallo kopieeractiviteit uitgevoerd Hallo opschonen script toodelete Hallo bijbehorende gegevens voor dit segment. En vervolgens het Hallo-invoer wordt gelezen uit Hallo csv (inhoudt vervolgens slechts 1 record) en ingevoegd Hallo tabel. 

### <a name="mechanism-2"></a>Mechanisme 2
> [!IMPORTANT]
> sliceIdentifierColumnName wordt niet ondersteund voor Azure SQL Data Warehouse op dit moment. 

Een ander mechanisme tooachieve herhaalbaarheid is door een specifieke kolom (**sliceIdentifierColumnName**) in Hallo doel tabel. In deze kolom wordt gebruikt door Azure Data Factory tooensure Hallo bron- en doelserver gesynchroniseerd blijven. Deze methode werkt wanneer er flexibiliteit bij het definiëren van de SQL-tabel doelschema Hallo of wijzigen. 

In deze kolom wordt gebruikt door Azure Data Factory voor herhaalbaarheid doeleinden en in proces hello Azure Data Factory niet brengt geen schema toohello tabel wordt gewijzigd. Manier toouse deze benadering:

1. Een kolom van het type binaire (32) definiëren in Hallo doel-SQL-tabel. Er mag geen beperkingen voor deze kolom. Laten we in deze kolom als 'ColumnForADFuseOnly' naam voor dit voorbeeld.
2. Gebruik deze als volgt in Hallo kopieeractiviteit:
   
    ```json
    "sink":  
    { 
   
        "type": "SqlSink", 
        "sliceIdentifierColumnName": "ColumnForADFuseOnly"
    }
    ```

Azure Data Factory wordt gevuld in deze kolom aan de hand van de noodzaak tooensure Hallo bron- en doelserver gesynchroniseerd blijven. Hallo-waarden van deze kolom mag niet buiten deze context worden gebruikt door de gebruiker Hallo. 

Vergelijkbare toomechanism 1, Kopieeractiviteit wordt automatisch eerste opschonen Hallo-gegevens voor Hallo opgegeven segment van Hallo doel-SQL-tabel en voer de kopieeractiviteit Hallo normaal tooinsert Hallo gegevens uit de bron toodestination voor dit segment. 


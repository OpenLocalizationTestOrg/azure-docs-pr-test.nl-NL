Nu dat u hebt een trigger, de tijd toodo iets interessante met Hallo-gegevens die worden gegenereerd door de trigger Hallo toegevoegd. Volg deze stappen tooadd een Hallo **SFTP - extract map** in te grijpen. Deze actie wordt Hallo inhoud van een bestand uitgepakt als gedefinieerde Hallo voorwaarden wordt voldaan. 

tooconfigure Hallo deze actie, moet u tooprovide Hallo informatie te volgen. U ziet dat het eenvoudig toouse gegevens die zijn gegenereerd door de trigger Hallo als invoer voor een aantal eigenschappen voor het nieuwe bestand Hallo Hallo:

| SFTP - extract map eigenschap | Beschrijving |
| --- | --- |
| Bronbestandspad archief |Dit is Hallo pad voor het Hallo-bestand uitgepakt. U kunt een van de Hallo tokens selecteren uit een eerdere actie of blader Hallo SFTP server toofind Hallo-bestandspad. |
| Pad naar de doelmap |Dit is Hallo pad waar u bestanden hebt uitgepakt hello wordt geplaatst. Een van de tokens Hallo kan uit een eerdere actie als Hallo doelpad of Hallo SFTP-server te bladeren en selecteer een pad. |
| Overschrijven? |Hiermee wordt aangegeven als een bestand met de Hallo dezelfde naam als Hallo uitgepakte bestand in pad van de doelmap Hallo staat als Hallo bestaand bestand moet worden overschreven of niet. |

Aan de slag Hallo actie tooextract Hallo bestanden toe te voegen als het resultaat te Hallo voorwaarde eerder hebt gedefinieerd*True*. 

1. Selecteer **een actie toevoegen**.        
   ![Afbeelding 6 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-6.png)   
2. Selecteer Hallo **SFTP - Extract map** actie      
   ![Afbeelding 7 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-7.png)   
3. Selecteer **bronbestandspad archiveren**              
   ![Afbeelding 9 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-9.png)   
4. Selecteer Hallo **bestandspad** token. Hiermee wordt aangegeven dat u Hallo bestandspad van Hallo-bestand dat Hallo trigger gevonden als Hallo archief bronbestandspad gebruikt.           
   ![Afbeelding 10 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-10.png)   
5. Selecteer **pad naar de doelmap**           
   ![Afbeelding 11 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-11.png)   
6. Selecteer Hallo **bestandspad** token. Hiermee wordt aangegeven dat u Hallo bestandspad van Hallo-bestand dat Hallo trigger gevonden als Hallo doelpad voor Hallo uitgepakt bestanden gebruikt.   
7. Voer *\ExtractedFile* in Hallo **pad naar de doelmap** besturingselement. Doe dit alleen na Hallo bestand padtoken in Hallo bestemming map pad besturingselement.         
   ![Afbeelding 12 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-12.png)   
8. Voer *True* in Hallo **overschrijven?* besturingselement tooindicate die bestaande bestanden overschreven worden moeten als ze hebben dezelfde naam als Hallo Hallo bestanden hebt uitgepakt.      
   ![Afbeelding 13 voorwaarde SFTP](./media/connectors-create-api-sftp/condition-13.png)   
9. Hallo wijzigingen tooyour werkstroom opslaan  


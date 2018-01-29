## <a name="create-a-self-hosted-integration-runtime"></a>Een zelf-hostende Integration Runtime maken

In deze sectie kunt u een zelf-hostende Integration Runtime maken en deze koppelen aan een on-premises computer met de SQL Server-database. De zelf-hostende Integration Runtime is het onderdeel waarmee gegevens worden gekopieerd van SQL Server op uw computer naar Azure Blob Storage. 

1. Maak een variabele voor de naam van de Integration Runtime. Gebruik een unieke naam en noteer deze. U gaat deze verderop in de zelfstudie gebruiken. 

    ```powershell
   $integrationRuntimeName = "ADFTutorialIR"
    ```
2. Een zelf-hostende Integration Runtime maken. 

   ```powershell
   Set-AzureRmDataFactoryV2IntegrationRuntime -Name $integrationRuntimeName -Type SelfHosted -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName
   ```

   Hier volgt een voorbeeld van uitvoer:

   ```json
    Id                : /subscriptions/<subscription ID>/resourceGroups/ADFTutorialResourceGroup/providers/Microsoft.DataFactory/factories/onpremdf0914/integrationruntimes/myonpremirsp0914
    Type              : SelfHosted
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : onpremdf0914
    Name              : myonpremirsp0914
    Description       :
    ```
 
3. Voer de volgende opdracht uit om de status van de gemaakte zelf-hostende Integration Runtime op te halen. Controleer of de waarde van de **status** eigenschap is ingesteld op **NeedRegistration**. 

   ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntime -name $integrationRuntimeName -ResourceGroupName $resourceGroupName -DataFactoryName $dataFactoryName -Status
   ```

   Hier volgt een voorbeeld van uitvoer:

   ```json
   Nodes                     : {}
   CreateTime                : 9/14/2017 10:01:21 AM
   InternalChannelEncryption :
   Version                   :
   Capabilities              : {}
   ScheduledUpdateDate       :
   UpdateDelayOffset         :
   LocalTimeZoneOffset       :
   AutoUpdate                :
   ServiceUrls               : {eu.frontend.clouddatahub.net, *.servicebus.windows.net}
   ResourceGroupName         : <ResourceGroup name>
   DataFactoryName           : <DataFactory name>
   Name                      : <Integration Runtime name>
   State                     : NeedRegistration
   ```

4. Voer de volgende opdracht uit om verificatiesleutels op te halen die worden gebruikt voor de registratie van de zelf-hostende Integration Runtime met Azure Data Factory-service in de cloud: 

   ```powershell
   Get-AzureRmDataFactoryV2IntegrationRuntimeKey -Name $integrationRuntimeName -DataFactoryName $dataFactoryName -ResourceGroupName $resourceGroupName | ConvertTo-Json
   ```

   Hier volgt een voorbeeld van uitvoer:

   ```json
   {
       "AuthKey1":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx=",
       "AuthKey2":  "IR@0000000000-0000-0000-0000-000000000000@xy0@xy@yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy="
   }
   ```    

5. Kopieer een van de sleutels (zonder de dubbele aanhalingstekens) om de zelf-hostende Integration Runtime te registeren die u in de volgende stappen op uw computer gaat installeren.  

## <a name="install-the-integration-runtime"></a>Integration Runtime installeren
1. Als u de Integration Runtime al op uw computer heeft, verwijdert u deze met behulp van **Programma's toevoegen of verwijderen**. 

2. [Download](https://www.microsoft.com/download/details.aspx?id=39717) de zelf-hostende Integration Runtime op een lokale Windows-computer. Voer de installatie uit.

3. Selecteer **Volgende** op de pagina **Welkom bij de installatie van Microsoft Integration Runtime**.

4. Ga op de pagina **Gebruiksrechtovereenkomst** akkoord met de voorwaarden en de gebruiksrechtovereenkomst en selecteer **Volgende**.

5. Selecteer **Volgende** op de pagina **Doelmap**.

6. Selecteer **Installeren** op de pagina **Gereed om Microsoft Integration Runtime te installeren**.

7. Als er een waarschuwingsbericht wordt weergegeven met de melding of de computer moet worden geconfigureerd om in de slaapstand of sluimerstand over te gaan als deze niet in gebruik is, selecteert u **OK**.

8. Als de pagina **Energiebeheer** wordt weergegeven, sluit u deze en gaat u naar de instellingenpagina.

9. Selecteer **Voltooien** op de pagina **De installatie van Microsoft Integration Runtime is voltooid**.

10. Plak de sleutel die u in de vorige sectie hebt opgeslagen op de pagina **Integration Runtime (zelf-hostend) registreren** en selecteer **Registreren**. 

    ![De Integration Runtime registreren](media/data-factory-create-install-integration-runtime/register-integration-runtime.png)

11. U ziet het volgende bericht wanneer de zelf-hostende Integration Runtime is geregistreerd:

    ![Registratie is voltooid](media/data-factory-create-install-integration-runtime/registered-successfully.png)

12. Selecteer **Volgende** op de pagina **Nieuw knooppunt voor Integration Runtime (zelf-hostend)**. 

    ![Pagina Nieuw knooppunt voor Integration Runtime](media/data-factory-create-install-integration-runtime/new-integration-runtime-node-page.png)

13. Op de pagina **Intranetcommunicatiekanaal** selecteert u **Overslaan**. Selecteer een TLS/SSL-certificaat voor het beveiligen van de communicatie tussen knooppunten in een Integration Runtime-omgeving met meerdere knooppunten. 

    ![Pagina Intranetcommunicatiekanaal](media/data-factory-create-install-integration-runtime/intranet-communication-channel-page.png)

14. Op de pagina **Integration Runtime (zelf-hostend) registeren** selecteert u **Configuration Manager starten**.

15. Wanneer het knooppunt is verbonden met de cloudservice, ziet u de volgende pagina:

    ![Pagina Knooppunt is verbonden](media/data-factory-create-install-integration-runtime/node-is-connected.png)

16. Test nu de verbinding met uw SQL Server-database.

    ![Tabblad Diagnostische gegevens](media/data-factory-create-install-integration-runtime/config-manager-diagnostics-tab.png)   

    a. Ga op de pagina **Configuratiebeheer** naar **Diagnostische gegevens**.

    b. Selecteer **SqlServer** als het type gegevensbron.

    c. Voer de naam van de server in.

    d. Voer de naam van de database in.

    e. Selecteer de verificatiemethode.

    f. Voer de gebruikersnaam in.

    g. Voer het wachtwoord voor de gebruikersnaam in.

    h. Selecteer **Test** om te controleren of Integration Runtime verbinding kan maken met SQL Server. U ziet een groen vinkje als het gelukt is om verbinding te maken. U ziet een foutbericht als er geen verbinding kan worden gemaakt. Los eventuele problemen op en zorg ervoor dat de Integration Runtime verbinding met SQL Server kan maken.    

    > [!NOTE]
    > Noteer de waarden voor het verificatietype, de server, de database, de gebruiker en het wachtwoord. U hebt deze waarden verderop in deze zelfstudie nodig. 
    

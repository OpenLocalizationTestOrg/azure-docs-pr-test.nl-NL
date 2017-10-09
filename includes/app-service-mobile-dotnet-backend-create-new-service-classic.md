1. Aanmelden op Hallo [Azure Portal].
2. Klik op **+NIEUW** > **Web en mobiel** > **Mobile App** en geef een naam op voor de nieuwe back-end van Mobile App.
3. Voor Hallo **resourcegroep**, selecteer een bestaande resourcegroep of maak een nieuwe (Hallo met behulp van dezelfde naam als uw app). 
   
    U kunt ofwel een ander App Service-abonnement selecteren of een nieuw maken. Voor meer informatie over het plannen van de App-Services en hoe een nieuw plan in een andere prijscategorie toocreate servicetier en op de gewenste locatie, Zie [gedetailleerd overzicht van Azure App Service-plannen](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Voor Hallo **App Service-abonnement**, Hallo standaardabonnement (in Hallo [standaardcategorie](https://azure.microsoft.com/pricing/details/app-service/)) is geselecteerd. U kunt ook een ander abonnement selecteren of [Maak een nieuwe](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Hallo App Service-abonnement instellingen bepalen Hallo [locatie, functies, kosten en rekenresources](https://azure.microsoft.com/pricing/details/app-service/) die zijn gekoppeld aan uw app. 
   
    Nadat u op Hallo plan besluit, klikt u op **maken**. Hiermee maakt u back-end van Hallo mobiele App. 
5. In Hallo **instellingen** blade voor Hallo nieuwe backend voor mobiele Apps, klikt u op **snel starten** > uw clientplatform app > **verbinding maken met een database**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. In Hallo **gegevensverbinding toevoegen** blade, klikt u op **SQL-Database** > **een nieuwe database maken**, type Hallo database **naam**, Kies een prijscategorie en klik vervolgens op **Server**.  U kunt deze nieuwe database opnieuw gebruiken. Als u al een database in Hallo dezelfde locatie in plaats daarvan kunt u **gebruik een bestaande database**. Hallo-gebruik van een database op een andere locatie wordt niet aanbevolen vanwege toobandwidth kosten en hogere latentie.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. In Hallo **nieuwe server** blade, typt u een unieke naam in Hallo **servernaam** veld, geeft u een gebruikersnaam en wachtwoord, Controleer **toestaan azure-services tooaccess server**, en klik op **OK**. Hiermee maakt u nieuwe Hallo-database.
8. Terug in Hallo **gegevensverbinding toevoegen** blade, klikt u op **verbindingsreeks**, typt u Hallo aanmelding waarden en het wachtwoord voor uw database en klik op **OK**. Wacht enkele minuten tot Hallo database toobe is geïmplementeerd voordat u doorgaat.

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/

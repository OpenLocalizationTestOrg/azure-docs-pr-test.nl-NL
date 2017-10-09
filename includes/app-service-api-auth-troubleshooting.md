De meeste van Hallo tijd verificatiefouten het gevolg van onjuiste of inconsistente configuratie-instellingen. Hier volgen enkele specifieke suggesties voor dingen toocheck.

* Zorg ervoor dat u Hallo niet mist **opslaan** knop elke locatie. Dit is vaak eenvoudig toodo en Hallo resultaat is dat u u naar de juiste waarden Hallo op portal-pagina kijkt zult, maar ze daadwerkelijk in hello Azure-omgeving of Azure AD-toepassing nog niet zijn opgeslagen.
* Voor instellingen die zijn geconfigureerd in Hallo **toepassingsinstellingen** blade van hello Azure-portal, zorg ervoor dat Hallo juiste API-app of web-app is geselecteerd bij het Hallo-instellingen zijn ingevoerd.  Ook voor zorgen dat het Hallo-instellingen worden ingevoerd als **appinstellingen** en niet **verbindingsreeksen**, zoals het Hallo-indeling van Hallo twee secties is vergelijkbaar.
* Voor verificatie tooa JavaScript-front-end, download Hallo manifest opnieuw tooverify die `oauth2AllowImplicitFlow` te is gewijzigd`true`.
* Controleer of u HTTPS gebruikt waar u de URL's geconfigureerd:
  
  * In de projectcode
  * In de CORS
  * In de Azure-omgeving App-instellingen voor elke API-app en web-app
  * In de instellingen van Azure AD-toepassing.
    
    Houd er rekening mee dat als u een API-app-URL van Hallo portal kopieert, vaak er `http://` en hebt u ook wijzigen toomanually`https://`.
* Zorg ervoor dat eventuele codewijzigingen zijn geïmplementeerd. Bijvoorbeeld in een oplossing meerdere projecten is het mogelijk toochange een project de code en per ongeluk een kiezen Hallo anderen wanneer u van plan bent toodeploy Hallo wijzigen.
* Zorg ervoor dat u gaat tooHTTPS URL's in uw browser niet HTTP-URL's. Visual Studio maakt standaard profielen met HTTP-URL's publiceren, en dat is wat in Hallo browser wordt geopend nadat u een project implementeert.
* Voor verificatie tooa JavaScript-front-end, zorg dat CORS correct is geconfigureerd op Hallo API-app die Hallo JavaScript-code aanroepen. Bij twijfel over de vraag of Hallo probleem CORS-gerelateerde probeer ' * ' als Hallo oorsprong URL toegestaan. 
* Open uw browser de Console hulpprogramma's voor ontwikkelaars tabblad tooget meer foutinformatie voor JavaScript-front-end en onderzoeken van HTTP-aanvragen op Hallo netwerk. Console-foutberichten mogelijk misleidend. Als u een bericht met een fout CORS krijgt, Hallo echte probleem wordt mogelijk verificatie. U kunt controleren of dit Hallo geval is door het Hallo-app uitgevoerd met verificatie tijdelijk tijdelijk uitgeschakeld.
* Zorg ervoor dat u krijgt zo veel mogelijk gegevens in foutberichten mogelijk door in te stellen voor een .NET API-app [customErrors mode tooOff](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview).
* Voor een .NET API-app starten een [externe foutopsporingssessie](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), en bekijk het Hallo-waarden van Hallo variabelen die zijn doorgegeven toocode die gebruikmaakt van ADAL tooacquire een bearer-token of code waarmee wordt gecontroleerd of claims tegen Hallo verwacht service principal-ID. Houd er rekening mee dat uw code kan worden opgepikt configuratiewaarden uit verschillende bronnen, dus is het mogelijk toofind verrassingen op deze manier. Bijvoorbeeld, als u een typefout gemaakt tijdens `ida:ClientId` als `ida:ClientID` bij het configureren van instellingen voor Azure App Service-omgeving, Hallo code haalt Hallo `ida:ClientId` waarde die op zoek naar van Hallo Web.config-bestand hello Azure App Service-instelling wordt genegeerd. 
* Als dingen niet in een normale Internet Explorer-venster werken, een bestaande aanmelden mogelijk verstorend werkt; InPrivate en probeer Chrome of Firefox.


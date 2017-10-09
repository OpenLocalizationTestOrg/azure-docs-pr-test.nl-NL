Volg deze stappen tooinstall en MongoDB uitgevoerd op een virtuele machine met Windows Server.

> [!IMPORTANT]
> Beveiligingsfuncties van MongoDB, zoals verificatie en IP-adresbinding zijn niet standaard ingeschakeld. Beveiligingsfuncties moeten worden ingeschakeld voordat u MongoDB tooa productieomgeving implementeert.  Zie voor meer informatie [beveiligings- en](http://www.mongodb.org/display/DOCS/Security+and+Authentication).
>
>

1. Nadat u verbinding hebt met het toohello virtuele machine via Extern bureaublad, Internet Explorer openen vanuit Hallo **Start** menu op Hallo virtuele machine.
2. Selecteer Hallo **extra** knop in de rechterbovenhoek Hallo.  In **Internetopties**, selecteer Hallo **beveiliging** tabblad en selecteer vervolgens Hallo **vertrouwde websites** pictogram en klik tot slot op Hallo **Sites** de knop. Voeg *https://\*. mongodb.org* toohello lijst met vertrouwde sites.
3. Ga te[Downloads - MongoDB](https://www.mongodb.com/download-center#community).
4. Hallo zoeken **huidige stabiele Release** van **Community Server**, selecteer laatste Hallo **64-bits** versie in Hallo Windows kolom. Download en voer vervolgens Hallo MSI-installer.
5. MongoDB wordt doorgaans geïnstalleerd in C:\Program Files\MongoDB. Omgevingsvariabelen zoeken op Hallo bureaublad en Hallo MongoDB binaire bestanden toohello pad padvariabele toevoegen. U kunt bijvoorbeeld Hallo binaire bestanden vinden op C:\Program Files\MongoDB\Server\3.4\bin op uw computer.
6. MongoDB-gegevens en logboekbestanden mappen maken in de gegevensschijf hello (zoals station **F:**) u hebt gemaakt in de vorige stappen Hallo. Van **Start**, selecteer **opdrachtprompt** tooopen een opdrachtpromptvenster.  Type:

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun Hallo-database, uitvoeren:

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    Alle berichten in het logboek zijn gerichte toohello *F:\MongoLogs\mongolog.log* bestand zoals mongod.exe server wordt gestart en preallocates journaal-bestanden. Het kan enkele minuten duren voordat MongoDB toopreallocate Hallo journaal bestanden en beginnen met luisteren voor verbindingen. Hallo-opdrachtprompt blijft gericht zijn op deze taak terwijl het MongoDB-exemplaar wordt uitgevoerd.
8. toostart hello beheerdersrechten MongoDB-shell, opent u een andere opdrachtvenster van **Start** en type Hallo de volgende opdrachten:

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    Hallo-database is gemaakt door Hallo invoegen.
9. U kunt ook mongod.exe installeren als een service:

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    Een service is geïnstalleerd met de naam MongoDB met een beschrijving van "DB met Mongo". Hallo `--logpath` optie moet de gebruikte toospecify een logboekbestand, sinds het Hallo-service uitgevoerd heeft geen toodisplay uitvoer van een venster.  Hallo `--logappend` optie geeft u uitvoer tooappend toohello bestaande logboekbestand zorgt ervoor dat Hallo-service opnieuw wordt opgestart.  Hallo `--dbpath` optie geeft u op Hallo-locatie van map Hallo-gegevens. Zie voor meer service-gerelateerde opdrachtregelopties, [opdrachtregelopties voor het Service-gerelateerde][MongoWindowsSvcOptions].

    toostart hello service, die deze opdracht uitvoeren:

        C:\> net start MongoDB
10. Nu dat MongoDB is geïnstalleerd en actief is, u een poort in Windows Firewall tooopen moet zodat u op afstand kunt verbinding maken met tooMongoDB.  Van Hallo **Start** selecteert u **Systeembeheer** en vervolgens **Windows Firewall met geavanceerde beveiliging**.
11. een) Selecteer in het linkerdeelvenster Hallo **regels voor binnenkomende verbindingen**.  In Hallo **acties** deelvenster op Hallo rechts, selecteer **nieuwe regel...** .

    ![Windows Firewall][Image1]

    b) in Hallo **nieuwe Wizard regel voor binnenkomende**, selecteer **poort** en klik vervolgens op **volgende**.

    ![Windows Firewall][Image2]

    c) Selecteer **TCP** en vervolgens **specifieke lokale poorten**.  Geef een '27017' (Hallo standaardpoort MongoDB luistert op)-poort en klik op **volgende**.

    ![Windows Firewall][Image3]

    d) Selecteer **Hallo verbinding toestaan** en klik op **volgende**.

    ![Windows Firewall][Image4]

    e) Klik op **volgende** opnieuw.

    ![Windows Firewall][Image5]

    f) Geef een naam voor de regel hello, zoals 'MongoPort', en klik op **voltooien**.

    ![Windows Firewall][Image6]

12. Als u niet een eindpunt voor MongoDB configureren wanneer u Hallo virtuele machine hebt gemaakt, kunt u dit nu doen. Moet u zowel de firewallregel Hallo en Hallo eindpunt toobe kunnen tooconnect tooMongoDB op afstand.

  Klik in hello Azure-portal, op **virtuele Machines (klassiek)**Hallo-naam van uw nieuwe virtuele machine op en klik vervolgens op **eindpunten**.

    ![Eindpunten][Image7]

13. Klik op **Add**.

14. Toevoegen van een eindpunt met de naam 'Mongo', protocol **TCP**, en beide **openbare** en **persoonlijke** set-poorten te '27017'. Deze poort opent, kunt MongoDB toobe extern toegankelijk is.

    ![Eindpunten][Image9]

> [!NOTE]
> Hallo is 27017 Hallo standaardpoort die wordt gebruikt door MongoDB. U kunt deze standaardpoort wijzigen door op te geven Hallo `--port` parameter bij het starten van Hallo mongod.exe server. Zorg ervoor dat toogive hetzelfde poortnummer in de firewall Hallo Hallo en Hallo 'Mongo' eindpunt in de voorgaande instructies Hallo.
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png

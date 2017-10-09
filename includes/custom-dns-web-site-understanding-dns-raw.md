Hallo System DNS (Domain Name) is gebruikt toolocate bronnen op Hallo internet. Bijvoorbeeld, wanneer u een web-app-mailadres in uw browser invoeren of klik op een koppeling op een webpagina, gebruikt deze DNS-tootranslate Hallo domein in een IP-adres. Hallo IP-adres is ongeveer zoals een adres, maar het is niet erg menselijke gebruiksvriendelijke. Het is bijvoorbeeld veel eenvoudiger tooremember een DNS-naam zoals **contoso.com** is dan het tooremember een IP-adres zoals 192.168.1.88 of 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hallo DNS-systeem is gebaseerd op *records*. Registreert een specifieke koppelen *naam*, zoals **contoso.com**, met een IP-adres of een andere DNS-naam. Bij een toepassing, zoals een webbrowser, een naam in DNS, zoekt het Hallo-record wordt gevonden en maakt gebruik van wat deze verwijst Hallo tooas adres. Als Hallo deze punten toois een IP-adres waarde, wordt de Hallo browser die waarde gebruikt. Als deze tooanother DNS-naam verwijst, heeft Hallo-toepassing toodo resolutie opnieuw. Alle naamomzetting wordt uiteindelijk eindigen op een IP-adres.

Als u een web-app in App Service maken, een DNS-naam toohello web-app automatisch toegewezen. Deze naam heeft Hallo vorm van  **&lt;yourwebappname&gt;. azurewebsites.net**. Er is ook een virtueel IP-adres beschikbaar voor gebruik bij het maken van DNS registreert, zodat u records dat punt toohello maken kunt **. azurewebsites.net**, of u kunt verwijzen toohello IP-adres.

> [!NOTE]
> Hallo IP-adres van uw web-app wordt gewijzigd als u deze verwijderen en opnieuw maken van uw web-app of Hallo App Service plan modus ook wijzigen**vrije** nadat deze is ingesteld te**Basic**, **gedeelde**, of **standaard**.
> 
> 

Er zijn ook meerdere typen met records, elk met hun eigen functies en -beperkingen, maar voor web-apps alleen belangrijk voor ons ongeveer twee *A* en *CNAME* records.

### <a name="address-record-a-record"></a>Adresrecord (een record)
Een A-record wordt een domein, zoals toegewezen **contoso.com** of **www.contoso.com**, *of een jokertekendomein* zoals  **\*. contoso.com**, tooan IP-adres. In geval van een web-app in App Service Hallo Hallo een virtueel IP-adres van Hallo service of een specifiek IP-adres dat u voor uw web-app hebt aangeschaft.

belangrijkste voordelen van een A-record via een CNAME-record Hallo zijn:

* U kunt bijvoorbeeld een hoofddomein toewijzen **contoso.com** tooan IP-adres; veel registrars alleen toestaan dit met behulp van een records
* U kunt een vermelding die gebruikmaakt van een jokerteken, zoals hebben  **\*. contoso.com**, die zou staat aanvragen verwerken voor meerdere subdomeinen zoals **mail.contoso.com**,  **blogs.contoso.com**, of **www.contso.com**.

> [!NOTE]
> Omdat een A-record is toegewezen tooa statische IP-adres, het automatisch wijzigingen toohello IP-adres van uw web-app kan niet worden omgezet. Een IP-adres voor gebruik met A-records wordt verstrekt wanneer u het aangepaste domein naam instellingen voor uw web-app configureren echter deze waarde kan wijzigen als u deze verwijderen en opnieuw maken van uw web-app of Hallo App Service plan modus tooback ook wijzigen**vrije**.
> 
> 

### <a name="alias-record-cname-record"></a>Record alias (CNAME-record)
Een CNAME-record verwijst een *specifieke* DNS-naam, zoals **mail.contoso.com** of **www.contoso.com**, tooanother (canoniek) domeinnaam. In geval van App Service Web Apps Hallo Hallo canonieke domeinnaam is Hallo  **&lt;yourwebappname >. azurewebsites.net** domeinnaam van uw web-app. Zodra gemaakt, Hallo CNAME maakt een alias voor Hallo  **&lt;yourwebappname >. azurewebsites.net** domeinnaam. Hallo CNAME-vermelding wordt opgelost toohello IP-adres van uw  **&lt;yourwebappname >. azurewebsites.net** domeinnaam automatisch als Hallo IP-adres van de web-app Hallo verandert, u hoeft dus niet tootake geen actie.

> [!NOTE]
> Sommige registrars domein alleen kunnen u toomap subdomeinen wanneer u een CNAME-record zoals **www.contoso.com**, en niet de hoofd-namen, zoals **contoso.com**. Zie voor meer informatie over CNAME-records Hallo documentatie bij uw registrar <a href="http://en.wikipedia.org/wiki/CNAME_record">Hallo vermelding Wikipedia (Engelstalig) op de CNAME-record</a>, of Hallo <a href="http://tools.ietf.org/html/rfc1035">IETF domeinnamen - implementatie en specificatie</a> document.
> 
> 

### <a name="web-app-dns-specifics"></a>Web-app DNS-specificaties
Een A-record met Web-Apps, moet u toofirst maken van een Hallo TXT-records te volgen:

* **Voor het hoofddomein Hallo** -A DNS TXT-record van  **@**  te  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Voor een specifieke subdomein** -naam van een DNS-  **&lt;subdomein >** te**&lt;yourwebappname&gt;. azurewebsites.net**. Bijvoorbeeld: **blogs** als Hallo een record voor **blogs.contoso.com**.
* **Voor Hallo jokertekens sub-dodmains** -A DNS TXT-record van *** te  **&lt;yourwebappname&gt;. azurewebsites.net**.

Deze TXT-record is gebruikte tooverify dat jij de eigenaar u toouse probeert Hallo-domein. Dit is bovendien toocreating een A-record toohello virtuele IP-adres van uw web-app aan te wijzen.

U vindt Hallo IP-adres en **. azurewebsites.net** namen voor uw web-app door te voeren Hallo volgende stappen:

1. Open in uw browser Hallo [Azure Portal](https://portal.azure.com).
2. In Hallo **Web-Apps** blade op Hallo-naam van uw web-app en selecteer vervolgens **aangepaste domeinen** van Hallo onder Hallo.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. In Hallo **aangepaste domeinen** blade ziet u Hallo virtueel IP-adres. Deze gegevens niet opslaan omdat deze worden gebruikt bij het maken van DNS-records
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > U kunt aangepaste domeinnamen met niet gebruiken een **vrije** web-app en Hallo App Service-abonnement moet te upgraden**gedeelde**, **Basic**, **standaard**, of **Premium** laag. Voor meer informatie over het Hallo-App Service plan de Prijscategorieën, met inbegrip van hoe toochange Hallo prijscategorie van uw web-app, Zie [hoe tooscale web-apps](../articles/app-service-web/web-sites-scale.md).
   > 
   > 


Domain Name System (DNS) wordt gebruikt om bronnen te vinden op het internet. Bijvoorbeeld, wanneer u een web-app-mailadres in uw browser invoeren of klik op een koppeling op een webpagina, gebruikt deze DNS te zetten van het domein in een IP-adres. Het IP-adres is ongeveer zoals een adres, maar het is niet erg menselijke gebruiksvriendelijke. Bijvoorbeeld, is het veel eenvoudiger te onthouden een DNS-naam zoals **contoso.com** dan een IP-adres zoals 192.168.1.88 of 2001:0:4137:1f67:24a2:3888:9cce:fea3 onthoudt.

De DNS-systeem is gebaseerd op *records*. Registreert een specifieke koppelen *naam*, zoals **contoso.com**, met een IP-adres of een andere DNS-naam. Wanneer een toepassing, zoals een webbrowser, u een naam in DNS zoekt, zoekt de record en maakt gebruik van wat deze verwijst naar als het adres. Als de waarde die deze naar verwijst een IP-adres is, wordt in de browser die waarde gebruiken. Als deze naar een andere DNS-naam verwijst, klikt u vervolgens heeft de toepassing oplossing opnieuw te doen. Alle naamomzetting wordt uiteindelijk eindigen op een IP-adres.

Wanneer u een web-app in App Service maakt, wordt automatisch een DNS-naam toegewezen aan de web-app. Deze naam heeft de vorm van  **&lt;yourwebappname&gt;. azurewebsites.net**. Er is ook een virtueel IP-adres beschikbaar voor gebruik bij het maken van DNS registreert, zodat u kunt records die naar wijzen maken de **. azurewebsites.net**, of u kunt verwijzen naar het IP-adres.

> [!NOTE]
> Het IP-adres van uw web-app als u wilt verwijderen en opnieuw maken van uw web-app of de App Service plan modus wijzigen gewijzigd **vrije** nadat deze is ingesteld op **Basic**, **gedeelde**, of **Standaard**.
> 
> 

Er zijn ook meerdere typen met records, elk met hun eigen functies en -beperkingen, maar voor web-apps alleen belangrijk voor ons ongeveer twee *A* en *CNAME* records.

### <a name="address-record-a-record"></a>Adresrecord (een record)
Een A-record wordt een domein, zoals toegewezen **contoso.com** of **www.contoso.com**, *of een jokertekendomein* zoals  **\*. contoso.com**, een IP-adres. In het geval van een web-app in App Service adres het virtuele IP-adres van de service of een specifiek IP-adres die u hebt aangeschaft voor uw web-app.

De belangrijkste voordelen van een A-record via een CNAME-record zijn:

* U kunt bijvoorbeeld een hoofddomein toewijzen **contoso.com** een IP-adres; veel registrars alleen toestaan dit met behulp van een records
* U kunt een vermelding die gebruikmaakt van een jokerteken, zoals hebben  **\*. contoso.com**, die zou staat aanvragen verwerken voor meerdere subdomeinen zoals **mail.contoso.com**,  **blogs.contoso.com**, of **www.contso.com**.

> [!NOTE]
> Omdat een A-record is toegewezen aan een statisch IP-adres, kan deze automatisch wijzigingen niet omzetten naar het IP-adres van uw web-app. Een IP-adres voor gebruik met A-records wordt verstrekt wanneer u het aangepaste domein naam instellingen voor uw web-app configureren echter deze waarde kan wijzigen als u wilt verwijderen en opnieuw maken van uw web-app of wijzigen van de App Service plan modus terug naar **vrije**.
> 
> 

### <a name="alias-record-cname-record"></a>Record alias (CNAME-record)
Een CNAME-record verwijst een *specifieke* DNS-naam, zoals **mail.contoso.com** of **www.contoso.com**, naar een andere (canoniek) domeinnaam. In het geval van App Service Web Apps, de canonieke domeinnaam is de  **&lt;yourwebappname >. azurewebsites.net** domeinnaam van uw web-app. Zodra gemaakt, CNAME maakt een alias voor de  **&lt;yourwebappname >. azurewebsites.net** domeinnaam. De CNAME-vermelding wordt omgezet in het IP-adres van uw  **&lt;yourwebappname >. azurewebsites.net** domeinnaam automatisch, zodat als de IP-adres van de web-app wordt gewijzigd, hoeft u geen actie te ondernemen.

> [!NOTE]
> Sommige registrars domein dat u subdomeinen toewijzen wanneer u een CNAME-record, zoals alleen **www.contoso.com**, en niet de hoofd-namen, zoals **contoso.com**. Zie voor meer informatie over de CNAME-records, de documentatie bij uw registrar <a href="http://en.wikipedia.org/wiki/CNAME_record">de vermelding Wikipedia (Engelstalig) op de CNAME-record</a>, of de <a href="http://tools.ietf.org/html/rfc1035">IETF domeinnamen - implementatie en specificatie</a> document.
> 
> 

### <a name="web-app-dns-specifics"></a>Web-app DNS-specificaties
Met behulp van een A-record met Web-Apps, moet u eerst een van de volgende TXT-records maken:

* **Voor het hoofddomein** -A DNS TXT-record van  **@**  naar  **&lt;yourwebappname&gt;. azurewebsites.net**.
* **Voor een specifieke subdomein** -naam van een DNS-  **&lt;subdomein >** naar  **&lt;yourwebappname&gt;. azurewebsites.net**. Bijvoorbeeld: **blogs** als de A-record voor **blogs.contoso.com**.
* **Voor de jokerteken-sub-dodmains** -A DNS TXT-record van *** naar  **&lt;yourwebappname&gt;. azurewebsites.net**.

Deze TXT-record wordt gebruikt om te controleren of de eigenaar van het domein dat u probeert te gebruiken. Dit is niet alleen een A-record die verwijst naar het virtuele IP-adres van uw web-app maken.

U vindt het IP-adres en **. azurewebsites.net** namen voor uw web-app door de volgende stappen uit te voeren:

1. Open in uw browser de [Azure Portal](https://portal.azure.com).
2. In de **Web-Apps** blade, klikt u op de naam van uw web-app en selecteer vervolgens **aangepaste domeinen** van de onderkant van de pagina.
   
    ![](./media/custom-dns-web-site/dncmntask-cname-6.png)
3. In de **aangepaste domeinen** blade ziet u het virtuele IP-adres. Deze gegevens niet opslaan omdat deze worden gebruikt bij het maken van DNS-records
   
    ![](./media/custom-dns-web-site/virtual-ip-address.png)
   
   > [!NOTE]
   > U kunt aangepaste domeinnamen met niet gebruiken een **vrije** web-app en de App Service-abonnement moet upgraden **gedeelde**, **Basic**, **standaard**, of **Premium** laag. Voor meer informatie over de App Service-abonnement de prijzen lagen, waaronder het wijzigen van de prijscategorie van uw web-app, Zie [schalen van web-apps](../articles/app-service-web/web-sites-scale.md).
   > 
   > 


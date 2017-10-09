Hallo System DNS (Domain Name) is gebruikte toolocate dingen op Hallo internet. Bijvoorbeeld, wanneer u een adres in uw browser invoeren of klik op een koppeling op een webpagina, gebruikt deze DNS-tootranslate Hallo domein in een IP-adres. Hallo IP-adres is ongeveer zoals een adres, maar het is niet erg menselijke gebruiksvriendelijke. Het is bijvoorbeeld veel eenvoudiger tooremember een DNS-naam zoals **contoso.com** is dan het tooremember een IP-adres zoals 192.168.1.88 of 2001:0:4137:1f67:24a2:3888:9cce:fea3.

Hallo DNS-systeem is gebaseerd op *records*. Registreert een specifieke koppelen *naam*, zoals **contoso.com**, met een IP-adres of een andere DNS-naam. Bij een toepassing, zoals een webbrowser, een naam in DNS, zoekt het Hallo-record wordt gevonden en maakt gebruik van wat deze verwijst Hallo tooas adres. Als Hallo deze punten toois een IP-adres waarde, wordt de Hallo browser die waarde gebruikt. Als deze tooanother DNS-naam verwijst, heeft Hallo-toepassing toodo resolutie opnieuw. Alle naamomzetting wordt uiteindelijk eindigen op een IP-adres.

Wanneer u een Azure-Website maakt, wordt een DNS-naam automatisch toohello site toegewezen. Deze naam heeft Hallo vorm van  **&lt;yoursitename&gt;. azurewebsites.net**. Wanneer u uw website als een Azure Traffic Manager-eindpunt toevoegt, uw website vervolgens toegankelijk is via Hallo  **&lt;yourtrafficmanagerprofile&gt;. trafficmanager.net** domein.

> [!NOTE]
> Als uw website is geconfigureerd als een Traffic Manager-eindpunt, gebruikt u Hallo **. trafficmanager.net** genomen bij het maken van DNS-records.
> 
> U kunt CNAME-records alleen gebruiken met Traffic Manager
> 
> 

Er zijn ook meerdere typen met records, elk met hun eigen functies en -beperkingen, maar voor websites die zijn geconfigureerd tooas Traffic Manager-eindpunten, alleen belangrijk voor ons over een bepaald; *CNAME* records.

### <a name="cname-or-alias-record"></a>CNAME- of Alias-record
Een CNAME-record verwijst een *specifieke* DNS-naam, zoals **mail.contoso.com** of **www.contoso.com**, tooanother (canoniek) domeinnaam. In geval van Azure Websites met Traffic Manager Hallo Hallo canonieke domeinnaam is Hallo  **&lt;myapp >. trafficmanager.net** domeinnaam van uw Traffic Manager-profiel. Zodra gemaakt, Hallo CNAME maakt een alias voor Hallo  **&lt;myapp >. trafficmanager.net** domeinnaam. Hallo CNAME-vermelding wordt opgelost toohello IP-adres van uw  **&lt;myapp >. trafficmanager.net** domeinnaam automatisch als Hallo IP-adres van de website Hallo verandert, u hoeft dus niet tootake geen actie.

Zodra het verkeer binnenkomt op Traffic Manager, stuurt deze vervolgens Hallo verkeer tooyour website Hallo taakverdelingsmethode die deze is geconfigureerd voor gebruik. Dit is volledig transparant toovisitors tooyour website. Ze zien alleen de aangepaste domeinnaam Hallo in hun browser.

> [!NOTE]
> Sommige registrars domein alleen kunnen u toomap subdomeinen wanneer u een CNAME-record zoals **www.contoso.com**, en niet de hoofd-namen, zoals **contoso.com**. Zie voor meer informatie over CNAME-records Hallo documentatie bij uw registrar <a href="http://en.wikipedia.org/wiki/CNAME_record">Hallo vermelding Wikipedia (Engelstalig) op de CNAME-record</a>, of Hallo <a href="http://tools.ietf.org/html/rfc1035">IETF domeinnamen - implementatie en specificatie</a> document.
> 
> 


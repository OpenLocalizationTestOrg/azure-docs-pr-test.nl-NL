>[!NOTE]
>Voor bronnen die niet worden opgelost, kan u vragen voor Hallo quota toobe gegenereerd, door een ondersteuningsticket openen. Voer **niet** extra Azure Media Services-accounts maken in een poging tooobtain hogere limieten.

| Resource | Standaardlimiet | 
| --- | --- | 
| AMS-accounts (Azure Media Service) in één abonnement | 25 (vast) |
| Gereserveerde media-eenheden (RU's) per AMS-account |25 (S1, S2)<br/>10 (S3) <sup>(1)</sup> | 
| Taken per AMS-account | 50,000<sup>(2)</sup> |
| Gekoppelde taken per taak | 30 (vast) |
| Activa per AMS-account | 1.000.000|
| Activa per taak | 50 |
| Activa per taak | 100 |
| Unieke locators die aan één activum tegelijk zijn gekoppeld | 5<sup>(4)</sup> |
| Live kanalen per AMS-account |5|
| Programma's met de status Gestopt per kanaal |50|
| Programma's met de status Wordt uitgevoerd per kanaal |3|
| Streaming-eindpunten met de status Wordt uitgevoerd per AMS-account|2|
| Streaming-eenheden per streaming-eindpunt |10 |
| Opslagaccounts | 1.000<sup>(5)</sup> (vast) |
| Beleidsregels | 1,000,000<sup>(6)</sup> |
| Bestandsgrootte| In sommige scenario's geldt er een limiet voor maximale bestandsgrootte Hallo ondersteund voor de verwerking van Media Services. <sup>7</sup> |
  
<sup>1</sup> S3-RU's zijn niet beschikbaar in India - west. Hallo max RU limieten opnieuw worden ingesteld als klant Hallo Hallo type (bijvoorbeeld van S2 tooS1) wordt gewijzigd. 

<sup>2</sup> Deze waarde omvat taken in de wachtrij, voltooide taken, actieve taken en geannuleerde taken. Deze bevat geen verwijderde taken. U kunt verwijderen Hallo oude taken met behulp van **IJob.Delete** of Hallo **verwijderen** HTTP-aanvraag.

Vanaf 1 April 2017 worden elke record taak in uw account ouder is dan 90 dagen, automatisch verwijderd, samen met de bijbehorende records van de taak zelfs als Hallo kunt u het totale aantal records lager dan de maximumquotum Hallo is. Als u tooarchive Hallo projecttaak/informatie nodig hebt, kunt u Hallo code beschreven [hier](../articles/media-services/media-services-dotnet-manage-entities.md).

<sup>3</sup> wanneer een aanvraag toolist taak entiteiten, maximaal 1000 per aanvraag worden geretourneerd. Als u moet tookeep bijhouden van alle taken verzonden, kunt u boven/skip zoals beschreven in [OData-query systeemopties](http://msdn.microsoft.com/library/gg309461.aspx).

<sup>4</sup> Locators zijn niet ontworpen om toegangsbeheer per gebruiker te regelen. gebruikers voor toogive verschillende toegangsrechten rechten tooindividual beheer van digitale rechten (DRM) oplossingen gebruiken. Zie [deze](../articles/media-services/media-services-content-protection-overview.md) sectie voor meer informatie.

<sup>5</sup> Hallo Hallo storage-accounts zijn hetzelfde Azure-abonnement.

<sup>6</sup> Er geldt een limiet van 1.000.000 beleidsregels voor verschillende AMS-beleidsitems (bijvoorbeeld voor Locator-beleid of ContentKeyAuthorizationPolicy). 

>[!NOTE]
> Hallo moet u dezelfde beleids-ID als u altijd dezelfde Hallo dagen / toegangsmachtigingen / enz. Zie [dit](../articles/media-services/media-services-dotnet-manage-entities.md#limit-access-policies) gedeelte voor informatie en een voorbeeld.

<sup>7</sup>als u wilt uploaden inhoud tooan actief in Azure Media Services met opzet tooprocess Hallo deze met een Hallo media processors in onze service (dat wil zeggen coderingsprogramma's zoals Media Encoder Standard en Premium werkstroom van Media Encoder of analyse engines zoals Face detectie), vervolgens moet u rekening houden met het Hallo-beperking voor de maximale grootte Hallo. 

Vanaf 15 mei 2017 Hallo maximumgrootte ondersteund voor één blob 195 TB - met bestand largers dan deze limiet is, de taak mislukt. We werken een fix tooaddress deze limiet. Bovendien Hallo-beperking voor de maximale grootte Hallo Hallo Asset is als volgt.

| Type gereserveerde media-eenheid | Invoer maximumgrootte (GB)| 
| --- | --- | 
|S1 | 325|
|S2 | 640|
|S3 | 260|

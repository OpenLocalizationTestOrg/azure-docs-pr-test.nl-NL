Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein. toostart die als host fungeert voor uw domein in Azure DNS, moet u een DNS-zone toocreate voor die domeinnaam. Alle DNS-records voor uw domein worden vervolgens gemaakt binnen deze DNS-zone.

Hallo domein 'contoso.com' kan bijvoorbeeld meerdere DNS-records, zoals 'mail.contoso.com' (voor een e-mailserver) en 'www.contoso.com' (voor een website) bevatten.

Bij het maken van een DNS-zone in Azure DNS:

* Hallo-naam van zone Hallo moet uniek zijn binnen de resourcegroep Hallo en Hallo zone mag niet al bestaan. Anders mislukt het Hallo-bewerking.
* Hallo dezelfde zonenaam kan opnieuw worden gebruikt in een andere resourcegroep of een ander Azure-abonnement.
* Waarbij meerdere zones delen hello dezelfde naam, elk exemplaar is toegewezen andere serveradressen. Slechts één set met adressen kan worden geconfigureerd met Hallo domeinnaamregistrar.

> [!NOTE]
> U hoeft geen tooown een domain name toocreate een DNS-zone met die domeinnaam in Azure DNS. Echter, hoeft u tooown hello tooconfigure hello Azure DNS-naam van servers in het domein als de juiste naam van de servers voor de domeinnaam Hallo met domeinnaamregistrar Hallo Hallo.
> 
> Zie voor meer informatie [delegeren van een domein tooAzure DNS-](../articles/dns/dns-domain-delegation.md).

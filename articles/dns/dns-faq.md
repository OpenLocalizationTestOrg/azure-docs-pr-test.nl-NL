---
title: Veelgestelde vragen over de DNS-aaaAzure | Microsoft Docs
description: Veelgestelde vragen over Azure DNS
services: dns
documentationcenter: na
author: jtuliani
manager: timlt
editor: 
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: jonatul
ms.openlocfilehash: 55006e9d8b311f1e94678eb9d35ce3448b936488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-faq"></a>Veelgestelde vragen over Azure DNS

## <a name="about-azure-dns"></a>Over Azure DNS

### <a name="what-is-azure-dns"></a>Wat is Azure DNS?

Hallo Domain Name System en DNS, is verantwoordelijk voor het omzetten van (of het oplossen van) een website of service name tooits IP-adres. Azure DNS is een hosting service voor DNS-domeinen omzetten van namen met behulp van Microsoft Azure-infrastructuur. U kunt uw DNS beheren door het hosten van uw Azure-domeinen records met dezelfde referenties, API's, hulpprogramma's en facturering Hallo als uw andere Azure-services.

DNS-domeinen in Azure DNS worden gehost op Azure wereldwijd netwerk van DNS-naamservers. We gebruiken Anycast networking zodat elke DNS-query wordt beantwoord door Hallo dichtstbijzijnde beschikbare DNS-server. Dit biedt zowel snelle prestaties en hoge beschikbaarheid voor uw domein.

Hello Azure DNS-service is gebaseerd op Azure Resource Manager. Als zodanig voordelen van Resource Manager-functies zoals rollen gebaseerd toegangsbeheer controlelogboeken en resource vergrendelen. Uw domeinen en records kunnen worden beheerd via hello Azure-portal, Azure PowerShell-cmdlets en Hallo platformoverschrijdende Azure CLI. Toepassingen waarbij automatisch DNS-beheer kunnen integreren met de service via Hallo Hallo REST-API en SDK's.

### <a name="how-much-does-azure-dns-cost"></a>Wat kost Azure DNS?

Hello Azure DNS facturering model is gebaseerd op Hallo aantal DNS-zones die worden gehost in Azure DNS en Hallo aantal DNS-query's die ze ontvangen. Kortingen zijn beschikbaar op basis van gebruik.

Zie voor meer informatie, Hallo [Azure DNS pagina met prijzen](https://azure.microsoft.com/pricing/details/dns/).

### <a name="what-is-hello-sla-for-azure-dns"></a>Wat is Hallo SLA voor Azure DNS?

Wordt gegarandeerd dat geldige DNS-aanvragen wordt een reactie ontvangen van ten minste één Azure DNS-naamserver ten minste 99,99% Hallo tijd.

Zie voor meer informatie, Hallo [Azure DNS-SLA pagina](https://azure.microsoft.com/support/legal/sla/dns).

### <a name="what-is-a-dns-zone-is-it-hello-same-as-a-dns-domain"></a>Wat is een DNS-zone? Is dit hetzelfde als een DNS-domein Hallo? 

Een domein is een unieke naam in Hallo domain name system, bijvoorbeeld 'contoso.com'.

Een DNS-zone is gebruikte toohost Hallo DNS-records voor een bepaald domein. Hallo domein 'contoso.com' kan bijvoorbeeld meerdere DNS-records, zoals 'mail.contoso.com' (voor een e-mailserver) en 'www.contoso.com' (voor een website) bevatten. Deze zou worden gehost in Hallo DNS-zone 'contoso.com'.

Is een domeinnaam *alleen een naam*, terwijl een DNS-zone is een gegevensbron met Hallo DNS-records voor een domeinnaam. Azure DNS kunt u een DNS-zone toohost en Hallo DNS-records voor een domein in Azure beheren. Bovendien wordt DNS-naamservers tooanswer DNS-query's uit Hallo Internet.

### <a name="do-i-need-toopurchase-a-dns-domain-name-toouse-azure-dns"></a>Moet ik een DNS-domein naam toouse Azure DNS toopurchase? 

Dat hoeft niet.

U hoeft niet toopurchase een toohost domein een DNS-zone in Azure DNS. U kunt een DNS-zone op elk gewenst moment maken zonder het Hallo-domeinnaam die eigenaar is. DNS-query's voor deze zone wordt alleen omgezet als ze zijn omgeleid toohello Azure DNS-naamservers toegewezen toohello zone.

U moet toopurchase Hallo domeinnaam als u wilt dat toolink uw DNS-zone naar Hallo globale DNS-hiërarchie – deze kan DNS-query's uit een willekeurige plaats in hello world toofind uw DNS-zone en met de DNS-records worden beantwoord.

## <a name="azure-dns-features"></a>Azure DNS-functies

### <a name="does-azure-dns-support-dns-based-traffic-routing-or-endpoint-failover"></a>Biedt ondersteuning voor Azure DNS DNS-verkeer routeren of eindpunt failover?

Routering en eindpunt failover van verkeer op basis van DNS worden geleverd door Azure Traffic Manager. Dit is een afzonderlijke Azure-service die kan worden gebruikt samen met de Azure DNS. Zie voor meer informatie, Hallo [Traffic Manager-overzicht](../traffic-manager/traffic-manager-overview.md).

Azure DNS ondersteunt alleen 'statische' DNS-domeinen, waarbij elke DNS-query voor een bepaalde DNS-record Hallo altijd ontvangt hosting dezelfde DNS-antwoord.

### <a name="does-azure-dns-support-domain-name-registration"></a>Azure DNS biedt ondersteuning voor registratie van domeinnamen?

Nee. Azure DNS ondersteunt momenteel geen kopen van domeinnamen. Als u wilt dat toopurchase domeinen, moet u toouse een domeinnaamregistrar van derden. Hallo registrar brengt doorgaans een kleine jaarlijkse rekening. Hallo-domeinen kunnen vervolgens worden gehost in Azure DNS voor het beheer van DNS-records. Zie [delegeren van een domein tooAzure DNS-](dns-domain-delegation.md) voor meer informatie.

Dit is een functie die we op onze achterstand volgen. U kunt ook onze site feedback gebruiken[registreren van de ondersteuning voor deze functie](https://feedback.azure.com/forums/217313-networking/suggestions/4996615-azure-should-be-its-own-domain-registrar).

### <a name="does-azure-dns-support-private-domains"></a>Ondersteunt Azure DNS-domeinen 'private'?

Nee. Azure DNS ondersteunt momenteel alleen internetgerichte domeinen.

Dit is een functie die we op onze achterstand volgen. U kunt ook onze site feedback gebruiken[registreren van de ondersteuning voor deze functie](https://feedback.azure.com/forums/217313-networking/suggestions/10737696-enable-split-dns-for-providing-both-public-and-int).

Zie voor informatie over de interne DNS-opties in Azure, [naamomzetting voor VM's en Rolexemplaren](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

### <a name="does-azure-dns-support-dnssec"></a>Azure DNS biedt ondersteuning voor DNSSEC?

Nee. Azure DNS biedt momenteel geen ondersteuning voor DNSSEC.

Dit is een functie die we op onze achterstand volgen. U kunt ook onze site feedback gebruiken[registreren van de ondersteuning voor deze functie](https://feedback.azure.com/forums/217313-networking/suggestions/13284393-azure-dns-needs-dnssec-support).

### <a name="does-azure-dns-support-zone-transfers-axfrixfr"></a>Biedt ondersteuning voor Azure DNS zoneoverdrachten (AXFR/IXFR)?

Nee. Azure DNS ondersteunt momenteel geen zoneoverdrachten. DNS-zones mag [geïmporteerd in Azure DNS met Azure CLI Hallo](dns-import-export.md). DNS-records kunnen vervolgens worden beheerd via Hallo [Azure DNS-beheerportal](dns-operations-recordsets-portal.md), onze [REST-API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell-cmdlets](dns-operations-recordsets.md), of [ CLI-hulpprogramma](dns-operations-recordsets-cli.md).

Dit is een functie die we op onze achterstand volgen. U kunt ook onze site feedback gebruiken[registreren van de ondersteuning voor deze functie](https://feedback.azure.com/forums/217313-networking/suggestions/12925503-extend-azure-dns-to-support-zone-transfers-so-it-c).

### <a name="does-azure-dns-support-url-redirects"></a>Biedt ondersteuning voor Azure DNS URL omleidingen?

Nee. URL-omleiding services zijn niet daadwerkelijk een DNS-service - ze op Hallo HTTP-niveau, in plaats van Hallo DNS-niveau werkt. Sommige providers DNS-toobundle een service van de omleidings-URL als onderdeel van hun algehele aanbieding. Dit wordt momenteel niet ondersteund door Azure DNS.

Deze functie wordt bijgehouden op onze achterstand. U kunt ook onze site feedback gebruiken[registreren van de ondersteuning voor deze functie](https://feedback.azure.com/forums/217313-networking/suggestions/10109736-provide-a-301-permanent-redirect-service-for-ape).

## <a name="using-azure-dns"></a>Met behulp van Azure DNS

### <a name="can-i-co-host-a-domain-using-azure-dns-and-another-dns-provider"></a>Kan ik dezelfde host een domein met behulp van Azure DNS en een andere DNS-provider?

Ja. Azure DNS ondersteunt mede hosting domeinen met een andere DNS-services.

toodo u moet dus toomodify Hallo NS-records voor Hallo-domein (die regelen welke providers DNS ontvangen query's voor Hallo domein) toopoint toohello naamservers van beide providers. Deze NS-records moeten toobe gewijzigd in 3 plaatsen: Hallo in Azure DNS in andere provider en Hallo bovenliggende zone (meestal geconfigureerd via Hallo domeinnaamregistrar). Zie voor meer informatie over DNS-delegering [DNS-domeindelegering](dns-domain-delegation.md).

Bovendien moet u tooensure dat Hallo DNS-records voor Hallo domein gesynchroniseerd tussen beide DNS-providers zijn. Azure DNS ondersteunt momenteel geen DNS-zoneoverdracht. U moet toosynchronize DNS-records met beide Hallo [Azure DNS-beheerportal](dns-operations-recordsets-portal.md), onze [REST-API](https://docs.microsoft.com/powershell/module/azurerm.dns), [SDK](dns-sdk.md), [PowerShell-cmdlets](dns-operations-recordsets.md) , of [CLI-hulpprogramma](dns-operations-recordsets-cli.md).

### <a name="do-i-have-toodelegate-my-domain-tooall-4-azure-dns-name-servers"></a>Heb ik toodelegate mijn domein tooall 4 Azure DNS-naamservers?

Ja. Azure DNS toegewezen naamservers 4 tooeach DNS-zone voor fouttolerantie isolatie en verbeterde herstelmogelijkheden. tooqualify voor hello Azure DNS-SLA, moet u toodelegate na de naamservers van uw domein tooall 4.

### <a name="what-are-hello-usage-limits-for-azure-dns"></a>Wat zijn de gebruikslimieten Hallo voor Azure DNS?

Hallo standaardlimiet van het volgende van toepassing wanneer u Azure DNS:

[!INCLUDE [dns-limits](../../includes/dns-limits.md)]

### <a name="can-i-move-an-azure-dns-zone-between-resource-groups-or-between-subscriptions"></a>Kan ik een Azure DNS-zone verplaatsen tussen resourcegroepen of tussen abonnementen?

Ja. DNS-zones kunnen worden verplaatst tussen resourcegroepen of tussen abonnementen.

Er zijn geen gevolgen voor DNS-query's bij het verplaatsen van een DNS-zone. Hallo-naamservers toegewezen toohello zone blijven Hallo die dezelfde en DNS-query's normaal in de gehele verwerkt worden.

Voor meer informatie en instructies voor het toomove DNS-zones, Zie [verplaatsen van resources tooa nieuwe resourcegroep of abonnement](../azure-resource-manager/resource-group-move-resources.md).

### <a name="how-long-does-it-take-for-dns-changes-tootake-effect"></a>Hoe lang duurt het voor DNS-wijzigingen tootake effect?

Nieuwe DNS-zones en DNS-records worden doorgaans op doorgevoerd hello Azure DNS-naamservers snel binnen een paar seconden.

Wijzigingen tooexisting DNS-records iets langer kunnen duren, maar nog steeds moeten zijn doorgevoerd op Hallo Azure DNS-naamservers binnen 60 seconden. In dit geval DNS-caching buiten Azure DNS (door DNS-clients en DNS-recursieve resolvers) kan ook van invloed Hallo gebruikte tijd voor een DNS-wijziging toobe effectieve. Deze Cacheduur kan worden beheerd met behulp van Hallo Time To Live (TTL)-eigenschap van elke recordset.

### <a name="how-can-i-protect-my-dns-zones-against-accidental-deletion"></a>Hoe kan ik mijn DNS-zones tegen het onbedoeld verwijderen beveiligen?

Azure DNS wordt beheerd met Azure Resource Manager en voordelen van Hallo toegang hebt tot functies die Azure Resource Manager biedt. Toegangsbeheer op basis van rollen kan gebruikte toocontrol welke gebruikers lees- of schrijftoegang tooDNS zones en -recordsets hebben zijn. Resource vergrendelingen kunnen toegepaste tooprevent onbedoelde wijziging of verwijdering van DNS-zones en -recordsets zijn.

Zie voor meer informatie [Protecting DNS-Zones en Records](dns-protect-zones-recordsets.md).

### <a name="how-do-i-set-up-spf-records-in-azure-dns"></a>Hoe stel ik SPF-records in Azure DNS

[!INCLUDE [dns-spf-include](../../includes/dns-spf-include.md)]

### <a name="how-do-i-set-up-an-international-domain-name-idn-in-azure-dns"></a>Hoe stel ik van een internationale domeinnaam (IDN) in Azure DNS

Internationale domeinnamen (IDN's) werkt door codering elke DNS-naam gebruikt '[punycode](https://en.wikipedia.org/wiki/Punycode)'. DNS-query's worden gemaakt met deze namen punycode-codering.

U kunt internationale domeinnamen (IDN's) in Azure DNS configureren met de eerste converteren Hallo zonenaam of toopunycode van de naam van de recordset. Azure DNS ondersteunt momenteel geen ingebouwde conversie van punycode.

## <a name="next-steps"></a>Volgende stappen

[Meer informatie over Azure DNS](dns-overview.md)
<br>
[Meer informatie over DNS-zones en records](dns-zones-records.md)
<br>
[Aan de slag met Azure DNS](dns-getstarted-portal.md)


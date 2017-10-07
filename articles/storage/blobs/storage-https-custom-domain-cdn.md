---
title: aaaUsing hello Azure CDN tooaccess blobs met aangepaste domeinen via HTTPS
description: Meer informatie over hoe toointegrate hello Azure CDN met blob storage tooaccess blobs met aangepaste domeinen via HTTPS
services: storage
documentationcenter: 
author: michaelhauss
manager: vamshik
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: mihauss
ms.openlocfilehash: f6cee36ca5495983545f2f6a8ff140677cf6914b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cdn-tooaccess-blobs-with-custom-domains-over-https"></a>Met behulp van hello Azure CDN tooaccess blobs via HTTPS met aangepaste domeinen

Azure Content Delivery Network (CDN) HTTPS wordt nu ondersteuning biedt voor aangepaste domeinnamen.
U kunt gebruikmaken van deze functie tooaccess storage-blobs gebruik van uw aangepaste domein via HTTPS. toodo geval is, moet u eerst tooenable Azure CDN van uw blob-eindpunt en kaart Hallo CDN tooa aangepaste domeinnaam. Zodra u de volgende stappen uitvoeren, wordt HTTPS inschakelen voor uw aangepaste domein vereenvoudigd, via één klik inschakelen, complete certificaatbeheer en alle met geen extra kosten toonormal CDN prijzen.

Deze mogelijkheid is belangrijk omdat Hiermee kunt u tooprotect Hallo privacy en integriteit van gegevens van uw gevoelige webtoepassingsgegevens onderweg. Met behulp van SSL-protocol tooserve-verkeer via HTTPS Hallo zorgt ervoor dat de gegevens worden versleuteld wanneer deze wordt verzonden via Hallo internet. HTTPS biedt vertrouwensrelatie en de verificatiemethode en uw webtoepassingen worden beschermd tegen aanvallen.

> [!NOTE]
> Bovendien kunt tooproviding SSL-ondersteuning voor aangepaste domeinnamen, hello Azure CDN u de inhoud van uw toepassing toodeliver hoge bandbreedte Hallo wereld schalen.
> toolearn meer, Bekijk [overzicht van Azure CDN Hallo](../../cdn/cdn-overview.md).
>
>

## <a name="quick-start"></a>Snel starten

Dit zijn de Hallo stappen vereist tooenable HTTPS voor het eindpunt van de aangepaste blob-opslag:

1.  [Een Azure storage-account integreren met Azure CDN](../../cdn/cdn-create-a-storage-account-with-cdn.md).
    Dit artikel begeleidt u bij het maken van een opslagaccount in hello Azure Portal als u dit nog niet hebt gedaan.
2.  [Overzicht Azure inhoud tooa aangepaste CDN-domein](../../cdn/cdn-map-content-to-custom-domain.md).
3.  [HTTPS op een aangepast domein van Azure CDN inschakelen](../../cdn/cdn-custom-ssl.md).

## <a name="shared-access-signatures"></a>Handtekeningen voor gedeelde toegang

Als het eindpunt van de blob-opslag geconfigureerde toodisallow anonieme toegang voor lezen is, moet u tooprovide een [Shared Access Signature (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) token bij elke aanvraag u tooyour aangepast domein. Blob storage-eindpunten niet standaard toestaan van anonieme toegang voor lezen. Zie [anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md) voor meer informatie over handtekeningen voor gedeelde toegang.

Azure CDN geen rekening gehouden met eventuele beperkingen toegevoegde toohello SAS-token. Alle SAS-tokens hebben bijvoorbeeld een verlooptijd. Dit betekent dat de inhoud zijn nog steeds toegankelijk met een verlopen SAS totdat deze inhoud is verwijderd uit Hallo CDN edge-knooppunten. U kunt bepalen hoe lang gegevens opgeslagen in de cache op Hallo CDN door Hallo cache antwoordheader instellen. Zie [beheer van verlopen van Azure Storage-blobs in Azure CDN](../../cdn/cdn-manage-expiration-of-blob-content.md) voor instructies.

Als u meerdere SAS-URL's voor Hallo maakt dezelfde eindpunt voor blob, het is raadzaam query opslaan in cache voor uw Azure CDN inschakelen. Dit is tooensure die elke URL wordt behandeld als een unieke entiteit. Zie [beheren van Azure CDN cachegedrag met queryreeksen](../../cdn/cdn-query-string.md) voor meer informatie.

## <a name="http-toohttps-redirection"></a>HTTP-omleiding voor tooHTTPS

U kunt tooredirect HTTP-verkeer tooHTTPS kiezen. U moet hiervoor gebruik van de aanbieding van hello Azure CDN premium van Verizon. U moet te[overschrijven HTTP gedrag met de engine van Azure CDN regels](../../cdn/cdn-rules-engine.md) aan de volgende regel:

![](./media/storage-https-custom-domain-cdn/redirect-to-https.png)

"Cdn-eindpunt-name" verwijst toohello-naam die u hebt geconfigureerd voor uw CDN-eindpunt. U kunt deze waarde uit de vervolgkeuzelijst Hallo selecteren. "Oorsprongpad" verwijst naar Hallo pad binnen uw oorsprong storage-account waarin uw statische inhoud zich bevindt.
Als u alle statische inhoud in een enkele container host, vervangen door 'oorsprongpad' Hallo-naam van die container.

Zie voor meer informatie in regels, Hallo [Azure CDN regels engine functies](../../cdn/cdn-rules-engine-reference-features.md).

## <a name="pricing-and-billing"></a>Prijzen en facturering

Wanneer u toegang blobs via een Azure CDN tot, betaalt u [Blob storage-prijzen](https://azure.microsoft.com/pricing/details/storage/blobs/) voor verkeer tussen Hallo edge-knooppunten en Hallo oorsprong (Blob-opslag), en [prijzen van CDN](https://azure.microsoft.com/pricing/details/cdn/) voor gegevens die worden gebruikt vanaf Hallo edge-knooppunten.

Stel dat u hebt een opslagaccount in VS-West die wordt geopend met behulp van een Azure CDN. Als iemand in Hallo VK een Hallo blobs in dat storage-account via Hallo CDN tooaccess probeert, controleert Azure eerst Hallo edge-knooppunt die het dichtst bij Hallo VK voor blob. Als gevonden, deze toegang heeft tot die kopie van de blob Hallo en maakt gebruik van de prijzen van CDN omdat deze wordt geopend op Hallo CDN. Als dat niet wordt gevonden, Azure kopieert Hallo blob toohello edge-knooppunt, dat in het uitgaande resulteert en kosten van de transactie als Hallo opgegeven in de Blob-opslag-prijzen en vervolgens toegang Hallo-bestand op de edge-knooppunt hello, dat in CDN facturering resulteert.

Wanneer u bekijkt hello [CDN pagina met prijzen](https://azure.microsoft.com/pricing/details/cdn/), Let op: HTTPS-ondersteuning voor aangepaste domeinnamen is alleen beschikbaar voor Azure CDN van Verizon producten (standaard en Premium).

## <a name="next-steps"></a>Volgende stappen

[Een aangepaste domeinnaam configureren voor het eindpunt van de Blob-opslag](storage-custom-domain-name.md)

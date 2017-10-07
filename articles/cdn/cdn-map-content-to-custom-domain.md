---
title: aaaMap Azure inhoud tooa aangepaste CDN-domein | Microsoft Docs
description: Meer informatie over hoe Azure CDN toomap inhoud tooa aangepast domein.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 289f8d9e-8839-4e21-b248-bef320f9dbfc
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d3ee77297f1dd7dbf31a9391191cc2910fbd2cee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="map-azure-cdn-content-tooa-custom-domain"></a>Azure CDN inhoud tooa aangepast domein toewijzen
U kunt een aangepast domein tooa CDN-eindpunt in volgorde toouse uw eigen domeinnaam in URL's toocached inhoud in plaats van een subdomein van azureedge.net toewijzen.

Er zijn twee manieren toomap uw aangepaste domein tooa CDN-eindpunt:

1. [Maken van een CNAME-record bij uw domeinregistrar en toewijzen van uw aangepaste domeinen en subdomeinen toohello CDN-eindpunt](#register-a-custom-domain-for-an-azure-cdn-endpoint).
   
    Een CNAME-record is een DNS-functie waarmee een brondomein zoals `www.contosocdn.com` of `cdn.contoso.com`, tooa doeldomein. In dit geval Hallo brondomein is voor uw aangepaste domeinen en subdomeinen (een subdomein, bijvoorbeeld **www** of **cdn** is altijd vereist). Hallo doeldomein is uw CDN-eindpunt.  
   
    Hallo-proces voor het toewijzen van uw aangepaste domein tooyour CDN-eindpunt kan echter resulteren in een korte periode van uitvaltijd voor Hallo domein terwijl u Hallo domein in hello Azure-Portal registreert.
2. [Toevoegen van een tussenliggende registratiestap met **cdnverify**](#register-a-custom-domain-for-an-azure-cdn-endpoint-using-the-intermediary-cdnverify-subdomain)
   
    Als uw aangepaste domein wordt momenteel ondersteund door een toepassing met een service level agreement (SLA) die vereist dat er geen uitvaltijd, dan kunt u hello Azure **cdnverify** subdomein tooprovide een tussenliggende registratie stap zodat gebruikers zich kunnen tooaccess uw domein tijdens het Hallo DNS toewijzen plaatsvindt.  

Nadat u uw aangepaste domein met een Hallo hierboven procedures geregistreerd, is het raadzaam te[controleren die aangepaste subdomein hello uw CDN-eindpunt verwijst naar](#verify-that-the-custom-subdomain-references-your-cdn-endpoint).

> [!NOTE]
> U moet een CNAME-record maken met uw registrar domein toomap uw domein toohello CDN-eindpunt. CNAME-records wijzen specifieke subdomeinen zoals `www.contoso.com` of `cdn.contoso.com`. Het is niet mogelijk toomap een hoofddomein CNAME-record tooa zoals `contoso.com`.
> 
> Een subdomein kan alleen worden gekoppeld aan een CDN-eindpunt. Hallo CNAME-record die u maakt gericht al het verkeer wordt gerouteerd toohello subdomein toohello opgegeven eindpunt.  Bijvoorbeeld, als u koppelen `www.contoso.com` met uw CDN-eindpunt vervolgens kan niet koppelt u deze met andere Azure-eindpunten, zoals een eindpunt storage-account of een cloud service-eindpunt. U kunt echter verschillende subdomeinen van hello gebruiken hetzelfde domein voor andere service-eindpunten. U kunt ook verschillende subdomeinen toohello toewijzen dezelfde CDN-eindpunt.
> 
> Voor **Azure CDN van Verizon** (standaard en Premium) eindpunten, houd er rekening mee dat deze in beslag te**90 minuten** voor het aangepaste domein toopropagate tooCDN edge-knooppunten wijzigt.
> 
> 

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint"></a>Een aangepast domein voor een Azure CDN-eindpunt registreren
1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).
2. Klik op **Bladeren**, klikt u vervolgens **CDN-profielen**, vervolgens Hallo CDN-profiel met Hallo eindpunt gewenste toomap tooa aangepast domein.  
3. In Hallo **CDN-profiel** blade, klikt u op Hallo CDN-eindpunt waarmee u tooassociate Hallo subdomein wilt.
4. Klik op Hallo Hallo bovenaan de blade een eindpunt Hallo in **aangepast domein toevoegen** knop.  In Hallo **toevoegen van een aangepast domein** blade ziet u Hallo endpoint-hostnaam, afgeleid van uw CDN-eindpunt toouse bij het maken van een nieuwe CNAME-record. Hallo-indeling van het adres Hallo host-naam wordt weergegeven als  **&lt;EndpointName >. azureedge.net**.  U kunt deze naam host toouse kopiëren in Hallo CNAME-record te maken.  
5. Navigeer tooyour domeinregistrar website en Hallo sectie voor het maken van DNS-records gevonden. U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.
6. Hallo sectie voor het beheren van CNAME-records vinden. U kunt toogo tooan geavanceerde instellingenpagina hebben en zoekt Hallo woorden CNAME-, Alias- of subdomeinen.
7. Maak een nieuwe CNAME-record dat is toegewezen uw gekozen subdomein (bijvoorbeeld **www** of **cdn**) toohello-hostnaam die is opgegeven in Hallo **toevoegen van een aangepast domein** blade. 
8. Retourneren van toohello **toevoegen van een aangepast domein** blade en voert u uw aangepaste domein, met inbegrip van subdomein hello, in het dialoogvenster Hallo. Voer bijvoorbeeld domeinnaam Hallo Hallo indeling `www.contoso.com` of `cdn.contoso.com`.   
   
   Azure controleert of Hallo CNAME-record bestaat voor Hallo-domeinnaam die u hebt ingevoerd. Als Hallo CNAME juist is, kan uw aangepaste domein wordt gevalideerd.  Voor **Azure CDN van Verizon** eindpunten (standaard en Premium), het kan duren too90 minuten voor het aangepaste domein instellingen toopropagate tooall CDN edge-knooppunten, maar.  
   
   Merk op dat in sommige gevallen is dit kan tijd vergen voor Hallo CNAME-record toopropagate tooname servers op Hallo Internet. Als uw domein niet onmiddellijk worden gevalideerd en u van mening bent Hallo CNAME-record juist is, wacht een paar minuten en probeer het opnieuw.

## <a name="register-a-custom-domain-for-an-azure-cdn-endpoint-using-hello-intermediary-cdnverify-subdomain"></a>Een aangepast domein voor een Azure CDN-eindpunt met behulp van Hallo tussenliggende cdnverify subdomein registreren
1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).
2. Klik op **Bladeren**, klikt u vervolgens **CDN-profielen**, vervolgens Hallo CDN-profiel met Hallo eindpunt gewenste toomap tooa aangepast domein.  
3. In Hallo **CDN-profiel** blade, klikt u op Hallo CDN-eindpunt waarmee u tooassociate Hallo subdomein wilt.
4. Klik op Hallo Hallo bovenaan de blade een eindpunt Hallo in **aangepast domein toevoegen** knop.  In Hallo **toevoegen van een aangepast domein** blade ziet u Hallo endpoint-hostnaam, afgeleid van uw CDN-eindpunt toouse bij het maken van een nieuwe CNAME-record. Hallo-indeling van het adres Hallo host-naam wordt weergegeven als  **&lt;EndpointName >. azureedge.net**.  U kunt deze naam host toouse kopiëren in Hallo CNAME-record te maken.
5. Navigeer tooyour domeinregistrar website en Hallo sectie voor het maken van DNS-records gevonden. U vindt dit in een gedeelte zoals **Domeinnaam**, **DNS** of **Serverbeheernaam**.
6. Hallo sectie voor het beheren van CNAME-records vinden. U kunt toogo tooan geavanceerde instellingenpagina hebben en zoekt u naar Hallo woorden **CNAME**, **Alias**, of **subdomeinen**.
7. Maak een nieuwe CNAME-record en geef een alias voor een subdomein met Hallo **cdnverify** subdomein. Bijvoorbeeld Hallo subdomein die u opgeeft worden in de indeling Hallo **cdnverify.www** of **cdnverify.cdn**. Geef vervolgens Hallo hostnaam die uw CDN-eindpunt in Hallo-indeling is **cdnverify.&lt; EndpointName >. azureedge.net**. Uw DNS-toewijzing moet eruitzien als:`cdnverify.www.consoto.com   CNAME   cdnverify.consoto.azureedge.net`  
8. Retourneren van toohello **toevoegen van een aangepast domein** blade en voert u uw aangepaste domein, met inbegrip van subdomein hello, in het dialoogvenster Hallo. Voer bijvoorbeeld domeinnaam Hallo Hallo indeling `www.contoso.com` of `cdn.contoso.com`. Houd er rekening mee dat in deze stap maakt u niet toopreface Hallo subdomein met hoeft **cdnverify**.  
   
    Azure controleert of Hallo CNAME-record bestaat voor Hallo cdnverify domein-naam die u hebt ingevoerd.
9. Op dit moment uw aangepaste domein is geverifieerd door Azure, maar verkeer tooyour domein nog geen gerouteerde tooyour CDN-eindpunt wordt. Na een wachttijd lang genoeg tooallow Hallo aangepast domein instellingen toopropagate edge toohello CDN-knooppunten (90 minuten **Azure CDN van Verizon**, 1-2 minuten voor **Azure CDN van Akamai**), tooyour DNS retourneren de website van Registrar en een andere CNAME-record maken die uw subdomein tooyour CDN-eindpunt wordt toegewezen. Geef bijvoorbeeld Hallo subdomein als **www** of **cdn**, en de hostnaam als Hallo  **&lt;EndpointName >. azureedge.net**. Hallo-registratie van uw aangepaste domein is met deze stap is voltooid.
10. Ten slotte kunt u hebt gemaakt met behulp van Hallo CNAME-record verwijderen **cdnverify**, zoals deze alleen als een tussenliggende stap nodig was.  

## <a name="verify-that-hello-custom-subdomain-references-your-cdn-endpoint"></a>Controleer of die aangepaste subdomein hello verwijst naar uw CDN-eindpunt
* Nadat u de registratie van uw aangepaste domein Hallo hebt voltooid, kunt u toegang tot inhoud die in cache is opgeslagen op uw gebruik van het aangepaste domein Hallo CDN-eindpunt.
  Eerst voor zorgen dat u openbare inhoud die in cache is opgeslagen op Hallo eindpunt hebben. Bijvoorbeeld, als uw CDN-eindpunt gekoppeld aan een opslagaccount is, Hallo CDN in de cache opgeslagen inhoud in een openbare blob-containers. tootest hello aangepast domein, zorg ervoor dat de container tooallow openbare toegang is ingesteld en dat deze ten minste één blob bevat.
* Navigeer in uw browser toohello-adres van het gebruik van het aangepaste domein Hallo Hallo-blob. Bijvoorbeeld, als uw aangepaste domein is `cdn.contoso.com`, Hallo URL tooa in de cache opgeslagen blob zijn vergelijkbaar toohello volgende URL: http://cdn.contoso.com/mypubliccontainer/acachedblob.jpg

## <a name="see-also"></a>Zie ook
[Hoe tooEnable Hallo Content Delivery Network (CDN) voor Azure](cdn-create-new-endpoint.md)  


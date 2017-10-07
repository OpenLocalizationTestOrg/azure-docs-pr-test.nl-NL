---
title: een aangepaste domeinnaam in Cloudservices aaaConfigure | Microsoft Docs
description: Meer informatie over hoe tooexpose uw Azure-toepassing of de gegevens op een aangepast domein door DNS-instellingen configureren.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 6a62c2b7-ea47-4cce-9d6a-0cca38357f42
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 71e553a73b40a8d0512b4d40173500561841772c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-an-azure-cloud-service"></a>Een aangepaste domeinnaam voor een Azure-cloud-service configureren
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-custom-domain-name-portal.md)
> * [Klassieke Azure Portal](cloud-services-custom-domain-name.md)
> 
> 

Wanneer u een Cloudservice maakt, kent Azure tooa subdomein van cloudapp.net. Bijvoorbeeld, als uw Cloudservice met de naam 'contoso', uw gebruikers zullen kunnen tooaccess worden uw toepassing op een URL als http://contoso.cloudapp.net. Azure wordt ook een virtueel IP-adres toegewezen.

U kunt echter ook uw toepassing weergegeven op uw eigen domeinnaam bijvoorbeeld contoso.com. Dit artikel wordt uitgelegd hoe tooreserve of een aangepaste domeinnaam configureren voor Cloud Service-web-rollen.

U al begrijpen wat CNAME en A-records zijn? [Korte inleiding voorbij Hallo uitleg](#add-a-cname-record-for-your-custom-domain).

> [!NOTE]
> U gaat sneller! Gebruik hello Azure [scenario begeleide](http://support.microsoft.com/kb/2990804). Het maakt koppelen van een aangepaste domeinnaam en het beveiligen van communicatie (SSL) met Azure Cloud Services of Azure Websites een module.
> 
> 

<p/>

> [!NOTE]
> Hallo procedures in deze taak toepassing tooAzure Cloud Services. Zie voor App-Services, [dit](../app-service-web/web-sites-custom-domain-name.md). Zie voor storage-accounts [dit](../storage/blobs/storage-custom-domain-name.md).
> 
> 

## <a name="understand-cname-and-a-records"></a>Records CNAME en A begrijpen
CNAME (of aliasrecords) en een records zowel kunnen u een domeinnaam met een specifieke server tooassociate (of service in dit geval) echter ze anders werken. Er zijn ook enkele specifieke overwegingen bij het gebruik van A-records met Azure-Cloud-services die u overwegen moet voordat u besluit welke toouse.

### <a name="cname-or-alias-record"></a>CNAME- of Alias-record
Een CNAME-record verwijst een *specifieke* domein, zoals **contoso.com** of **www.contoso.com**, tooa canonieke domeinnaam. In dit geval de canonieke domeinnaam Hallo Hallo is **[myapp] .cloudapp .net** domeinnaam van uw Azure gehoste toepassing. Zodra gemaakt, Hallo CNAME maakt een alias voor Hallo **[myapp] .cloudapp .net**. Hallo CNAME-vermelding wordt opgelost toohello IP-adres van uw **[myapp] .cloudapp .net** service automatisch als Hallo IP-adres van de cloudservice Hallo verandert, u hoeft dus niet tootake geen actie.

> [!NOTE]
> Sommige registrars domein alleen kunnen u toomap subdomeinen wanneer u een CNAME-record, bijvoorbeeld www.contoso.com en geen basis-namen, zoals contoso.com. Zie voor meer informatie over CNAME-records Hallo documentatie bij uw registrar [Hallo vermelding Wikipedia (Engelstalig) op de CNAME-record](http://en.wikipedia.org/wiki/CNAME_record), of Hallo [IETF domeinnamen - implementatie en specificatie](http://tools.ietf.org/html/rfc1035) document.
> 
> 

### <a name="a-record"></a>een record
Een A-record wordt een domein, zoals toegewezen **contoso.com** of **www.contoso.com**, *of een jokertekendomein* zoals  **\*. contoso.com**, tooan IP-adres. In geval van een Azure Cloud Service Hallo Hallo virtueel IP-adres van Hallo-service. Dus Hallo belangrijkste voordeel van een A-record via een CNAME-record is dat u kunt een vermelding die gebruikmaakt van een jokerteken, zoals \* **. contoso.com**, die zou staat aanvragen verwerken voor meerdere subdomeinen zoals  **mail.contoso.com**, **login.contoso.com**, of **www.contso.com**.

> [!NOTE]
> Omdat een A-record is toegewezen tooa statische IP-adres, het automatisch wijzigingen toohello IP-adres van uw Cloud-Service kan niet worden omgezet. Hallo IP-adres wordt gebruikt door uw Cloud-Service is toegewezen Hallo eerste keer dat u implementeert tooan lege sleuf (productie of staging.) Als u Hallo-implementatie voor Hallo sleuf verwijdert, Hallo IP-adres is vrijgegeven door Azure en alle toekomstige implementaties toohello sleuf kan een nieuw IP-adres worden gegeven.
> 
> Hallo IP-adres van een opgegeven implementatiesleuf (productie of staging) is gemakkelijk persistent bij het wisselen tussen fasering en productie-implementaties of het uitvoeren van een in-place upgrade van een bestaande implementatie. Zie voor meer informatie over het uitvoeren van deze acties [hoe toomanage cloudservices](cloud-services-how-to-manage.md).
> 
> 

## <a name="add-a-cname-record-for-your-custom-domain"></a>Voeg een CNAME-record voor uw aangepaste domein
toocreate een CNAME-record, moet u een nieuwe vermelding toevoegen in Hallo DNS-tabel voor uw aangepaste domein met behulp van Hallo-hulpprogramma's van uw registrar. Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een CNAME-record, maar de concepten Hallo Hallo dezelfde.

1. Gebruik een van deze methoden toofind hello **. cloudapp.net** domeinnaam tooyour cloudservice toegewezen.
   
   * Aanmelding toohello [klassieke Azure-portal], selecteer uw cloudservice, selecteert u **Dashboard**, en gaat u naar Hallo **Site-URL** vermelding in Hallo **snelle weergave**  sectie.
     
       ![snelle weergave sectie Hallo site-URL wordt weergegeven][csurl]
     
       **OR**  
   * Installeer en configureer [Azure Powershell](/powershell/azure/overview), en vervolgens gebruik Hallo opdracht:
     
       ```powershell
       Get-AzureDeployment -ServiceName yourservicename | Select Url
       ```
     
     Hallo-domeinnaam die is gebruikt in Hallo-URL die wordt geretourneerd door een van de methoden, zoals u deze hebt bij het maken van een CNAME-record opslaan.
2. Meld u op de website van tooyour DNS-registratieservice en ga toohello pagina voor het beheren van DNS. Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.
3. Nu kunt u selecteren of invoeren van CNAME zoeken. Mogelijk hebt u tooselect Hallo record uit een vervolgkeuzelijst, of Ga tooan geavanceerde voor instellingenpagina. Zoek naar Hallo woorden **CNAME**, **Alias**, of **subdomeinen**.
4. U moet ook opgeven Hallo domein of subdomein alias voor Hallo CNAME, zoals **www** als u een alias voor toocreate wilt **www.customdomain.com**. Als u toocreate een alias voor het hoofddomein hello wilt, kan dit worden vermeld als Hallo '**@**' symbool in DNS-hulpprogramma's van uw registrar.
5. Vervolgens moet u een canonieke hostnaam, uw toepassing is opgeven **cloudapp.net** domein in dit geval.

Bijvoorbeeld, Hallo volgt CNAME-record al het verkeer van stuurt **www.contoso.com** te**contoso.cloudapp.net**, Hallo aangepaste domeinnaam van uw geïmplementeerde toepassing:

| Alias/Host-naam/subdomein | Canonieke domein |
| --- | --- |
| www |Contoso.cloudapp.NET |

Een bezoeker van **www.contoso.com** Zie nooit Hallo true host (contoso.cloudapp.net), zodat Hallo doorstuurproces onzichtbaar toothe eindgebruiker.

> [!NOTE]
> Hallo in bovenstaand voorbeeld is alleen van toepassing tootraffic op Hallo **www** subdomein. Aangezien u kunt geen jokertekens CNAME-records gebruiken, moet u een CNAME voor elk domein/subdomein maken. Als u wilt dat toodirect verkeer van subdomeinen, zoals \*. contoso.com, tooyour cloudapp.net adres, kunt u een **Omleidings-URL** of **URL doorsturen** vermelding in uw DNS-instellingen, of Maak een A-record.
> 
> 

## <a name="add-an-a-record-for-your-custom-domain"></a>Een A-record voor uw aangepaste domein toevoegen
toocreate een A-record, moet u eerst Hallo virtueel IP-adres van uw cloudservice zoeken. Vervolgens voegt een nieuwe vermelding in Hallo DNS-tabel voor uw aangepaste domein met Hallo-hulpprogramma's van uw registrar. Elke registrar heeft een methode vergelijkbaar maar enigszins verschillen van het opgeven van een A-record, maar de concepten Hallo Hallo dezelfde.

1. Gebruik een van de volgende methoden tooget Hallo IP-adres van uw cloudservice Hallo.
   
   * aanmelding toohello [klassieke Azure-portal], selecteer uw cloudservice, selecteert u **Dashboard**, en gaat u naar Hallo **adres van de openbare virtuele IP-adres (VIP)** vermelding in Hallo **snelle weergave** sectie.
     
       ![snelle weergave sectie Hallo VIP wordt weergegeven][vip]
     
       **OR**  
   * Installeer en configureer [Azure Powershell](/powershell/azure/overview), en vervolgens gebruik Hallo opdracht:
     
       ```powershell
       get-azurevm -servicename yourservicename | get-azureendpoint -VM {$_.VM} | select Vip
       ```
     
     Als u meerdere eindpunten die zijn gekoppeld aan uw cloudservice hebt, ontvangt u meerdere regels met Hallo IP-adres, maar alle moet worden weergegeven in dezelfde Hallo adres.
     
     Hallo IP-adres niet opslaan omdat u deze hebt bij het maken van een A-record.
2. Meld u op de website van tooyour DNS-registratieservice en ga toohello pagina voor het beheren van DNS. Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**.
3. Nu kunt u selecteren of invoeren van de record zoeken. Mogelijk hebt u tooselect Hallo record uit een vervolgkeuzelijst, of Ga tooan geavanceerde voor instellingenpagina.
4. Selecteer of typ Hallo domein of subdomein die door deze A-record wordt gebruikt. Selecteer bijvoorbeeld **www** als u een alias voor toocreate wilt **www.customdomain.com**. Als u wilt dat toocreate een vermelding jokerteken voor alle subdomeinen, voert u '__*__'. Hierin vindt u alle subdomeinen zoals **mail.customdomain.com**, **login.customdomain.com**, en **www.customdomain.com**.
   
    Als u toocreate een A-record voor het hoofddomein hello wilt, kan dit worden vermeld als Hallo '**@**' symbool in DNS-hulpprogramma's van uw registrar.
5. Voer Hallo IP-adres van de cloudservice in Hallo opgegeven veld. Dit koppelt Hallo domein vermelding in het Hallo-A-record met Hallo IP-adres van uw cloud service-implementatie gebruikt.

Bijvoorbeeld, een record na Hallo al het verkeer van stuurt **contoso.com** te**137.135.70.239**, IP-adres van de geïmplementeerde toepassing hello:

| Host-naam/subdomein | IP-adres |
| --- | --- |
| @ |137.135.70.239 |

Dit voorbeeld wordt een A-record voor het hoofddomein Hallo maken. Als u een jokerteken vermelding toocover toocreate wenst alle subdomeinen, voert u '__*__' als Hallo subdomein.

> [!WARNING]
> IP-adressen in Azure zijn standaard dynamisch. Wilt u waarschijnlijk toouse een [gereserveerd IP-adres](../virtual-network/virtual-networks-reserved-public-ip.md) tooensure dat uw IP-adres niet verandert.
> 
> 

## <a name="next-steps"></a>Volgende stappen
* [Hoe tooManage Cloud-Services](cloud-services-how-to-manage.md)
* [Hoe tooMap CDN inhoud tooa aangepaste domeinen](../cdn/cdn-map-content-to-custom-domain.md)
* [Algemene configuratie van uw cloudservice](cloud-services-how-to-configure.md).
* Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy.md).
* Configureer [ssl-certificaten](cloud-services-configure-ssl-certificate.md).

[Expose Your Application on a Custom Domain]: #access-app
[Add a CNAME Record for Your Custom Domain]: #add-cname
[Expose Your Data on a Custom Domain]: #access-data
[VIP swaps]: http://msdn.microsoft.com/library/ee517253.aspx
[Create a CNAME record that associates hello subdomain with hello storage account]: #create-cname
[klassieke Azure-portal]: https://manage.windowsazure.com
[Validate Custom Domain dialog box]: http://i.msdn.microsoft.com/dynimg/IC544437.jpg
[vip]: ./media/cloud-services-custom-domain-name/csvip.png
[csurl]: ./media/cloud-services-custom-domain-name/csurl.png

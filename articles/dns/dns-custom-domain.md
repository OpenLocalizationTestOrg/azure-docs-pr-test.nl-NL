---
title: aaaIntegrate Azure DNS met uw Azure-resources | Microsoft Docs
description: Meer informatie over hoe Azure DNS toouse langs tooprovide DNS voor uw Azure-resources.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: gwallace
ms.openlocfilehash: b9b6f829513f0ad9da510190c75bc60dc7431545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-dns-tooprovide-custom-domain-settings-for-an-azure-service"></a>Azure DNS tooprovide aangepast domeininstellingen gebruiken voor een Azure-service

Azure DNS biedt DNS voor een aangepast domein voor een van uw Azure-resources dat ondersteuning van aangepaste domeinen of die een volledig gekwalificeerde domeinnaam (FQDN) hebben. Een voorbeeld is er een Azure-web-app en u wilt dat uw gebruikers tooaccess deze door een van beide contoso.com of www.contoso.com als een FQDN-naam gebruiken. In dit artikel begeleidt u bij het configureren van uw Azure-service met Azure DNS voor het gebruik van aangepaste domeinen.

## <a name="prerequisites"></a>Vereisten

In de volgorde toouse Azure DNS voor uw aangepaste domein, moet u eerst uw domein tooAzure DNS overdragen. Ga naar [delegeren van een domein tooAzure DNS-](./dns-delegate-domain-azure-dns.md) voor instructies over het tooconfigure de naamservers voor overdracht. Als uw domein overgedragen tooyour Azure DNS-zone is, bent u kunnen tooconfigure Hallo DNS-records die nodig zijn.

U kunt een vanity of een aangepast domein voor [Azure functie Apps](#azure-function-app), [Azure IoT](#azure-iot), [openbare IP-adressen](#public-ip-address), [App Service (Web-Apps)](#app-service-web-apps), [Blob storage](#blob-storage), en [Azure CDN](#azure-cdn).

## <a name="azure-function-app"></a>Azure-functie-App

een aangepast domein voor Azure-functie apps tooconfigure, een CNAME-record wordt gemaakt en de configuratie op Hallo functie-app zelf.
 
Navigeer te**andere** > **functie-App** en selecteert u de functie-App. Klik op **platformfuncties** en klikt u onder **NETWORKING** klikt u op **aangepaste domeinen**.

![de functie app-blade](./media/dns-custom-domain/functionapp.png)

Houd er rekening mee Hallo huidige url op Hallo **aangepaste domeinen** blade dit adres wordt gebruikt als alias Hallo voor Hallo DNS-record is gemaakt.

![aangepast domein-blade](./media/dns-custom-domain/functionshostname.png)

Navigeer tooyour DNS-Zone en klik op **+ Recordset**. Hallo volgende informatie op Hallo invullen **recordset toevoegen** blade en klik op **OK** toocreate deze.

|Eigenschap  |Waarde  |Beschrijving  |
|---------|---------|---------|
|Naam     | myfunctionapp        | Deze waarde samen met het domeinnaamlabel Hallo is Hallo FQDN-naam voor de aangepaste domeinnaam Hallo.        |
|Type     | CNAME        | Gebruik een CNAME-record maakt gebruik van een alias.        |
|TTL     | 1        | 1 wordt gebruikt voor 1 uur        |
|TTL-eenheid     | Uren        | Uren worden gebruikt als Hallo tijdmeting         |
|Alias     | adatumfunction.azurewebsites.NET        | Hallo DNS-naam die u maakt Hallo alias, in dit voorbeeld is Hallo adatumfunction.azurewebsites.net DNS-naam op die door standaard toohello functie-app.        |

Navigeer terug tooyour functie-app, klikt u op **platformfuncties**, en klikt u onder **NETWORKING** klikt u op **aangepaste domeinen**, klikt u vervolgens onder **hostnamen**klikt u op **+ toevoegen hostnaam**.

Op Hallo **hostnaam toevoegen** blade Voer Hallo CNAME-record in Hallo **hostnaam** tekstveld en klikt u op **valideren**. Als Hallo record kunnen toobe gevonden, Hallo **hostnaam toevoegen** knop wordt weergegeven. Klik op **hostnaam toevoegen** tooadd Hallo alias.

![functie apps toevoegen host naam blade](./media/dns-custom-domain/functionaddhostname.png)

## <a name="azure-iot"></a>Azure IoT

Azure IoT heeft geen aanpassingen die nodig zijn op Hallo-service zelf. een aangepast domein met een IoT-Hub toouse is alleen een CNAME-record toohello resources waarnaar wordt verwezen vereist.

Navigeer te**Internet der dingen** > **IoT Hub** en selecteer uw IoT-hub. Op Hallo **overzicht** blade Opmerking Hallo FQDN-naam van Hallo IoT-hub.

![Blade IoT Hub](./media/dns-custom-domain/iot.png)

Vervolgens gaat u tooyour DNS-Zone en klikt u op **+ Recordset**. Hallo volgende informatie op Hallo invullen **recordset toevoegen** blade en klik op **OK** toocreate deze.


|Eigenschap  |Waarde  |Beschrijving  |
|---------|---------|---------|
|Naam     | myiothub        | Deze waarde samen met het domeinnaamlabel Hallo is Hallo FQDN voor Hallo iothub.        |
|Type     | CNAME        | Gebruik een CNAME-record maakt gebruik van een alias.
|TTL     | 1        | 1 wordt gebruikt voor 1 uur        |
|TTL-eenheid     | Uren        | Uren worden gebruikt als Hallo tijdmeting         |
|Alias     | adatumIOT.azure devices.net        | Hallo DNS-naam die u maakt Hallo alias, in dit voorbeeld is Hallo adatumIOT.azure devices.net-hostnaam is opgegeven door de Hallo iothub.

Zodra Hallo-record is gemaakt, test u naamomzetting met het gebruik van Hallo CNAME-record`nslookup`

## <a name="public-ip-address"></a>Openbaar IP-adres

tooconfigure een aangepast domein voor services die gebruikmaken van een openbare IP-adres resource zoals Application Gateway, Load Balancer-Cloudservice, Resource Manager virtuele machines, en klassieke virtuele machines, een CNAME-record wordt gebruikt.

Navigeer te**Networking** > **openbaar IP-adres**, selecteer Hallo openbare IP-resource en klikt u op **configuratie**. Specificeren Hallo IP-adres weergegeven.

![openbare IP-blade](./media/dns-custom-domain/publicip.png)

Navigeer tooyour DNS-Zone en klik op **+ Recordset**. Hallo volgende informatie op Hallo invullen **recordset toevoegen** blade en klik op **OK** toocreate deze.


|Eigenschap  |Waarde  |Beschrijving  |
|---------|---------|---------|
|Naam     | mywebserver        | Deze waarde samen met het domeinnaamlabel Hallo is Hallo FQDN-naam voor de aangepaste domeinnaam Hallo.        |
|Type     | A        | Gebruik een A-record zoals Hallo-bron een IP-adres is.        |
|TTL     | 1        | 1 wordt gebruikt voor 1 uur        |
|TTL-eenheid     | Uren        | Uren worden gebruikt als Hallo tijdmeting         |
|IP-adres     | <your ip address>       | Hallo openbare IP-adres.|

![een A-record maken](./media/dns-custom-domain/arecord.png)

Uitvoeren zodra Hallo A-record is gemaakt, `nslookup` toovalidate Hallo record wordt omgezet.

![openbare IP-adres DNS-zoekopdracht](./media/dns-custom-domain/publicipnslookup.png)

## <a name="app-service-web-apps"></a>App Service (Web-Apps)

Hallo gaat volgende stappen u door het configureren van een aangepast domein voor een app service-web-app.

Navigeer te**Web en mobiel** > **App Service** en Hallo resource u configureert een aangepaste domeinnaam en klik op selecteren **aangepaste domeinen**.

Houd er rekening mee Hallo huidige url op Hallo **aangepaste domeinen** blade dit adres wordt gebruikt als alias Hallo voor Hallo DNS-record is gemaakt.

![blade voor aangepaste domeinen](./media/dns-custom-domain/url.png)

Navigeer tooyour DNS-Zone en klik op **+ Recordset**. Hallo volgende informatie op Hallo invullen **recordset toevoegen** blade en klik op **OK** toocreate deze.


|Eigenschap  |Waarde  |Beschrijving  |
|---------|---------|---------|
|Naam     | mywebserver        | Deze waarde samen met het domeinnaamlabel Hallo is Hallo FQDN-naam voor de aangepaste domeinnaam Hallo.        |
|Type     | CNAME        | Gebruik een CNAME-record maakt gebruik van een alias. Als Hallo resource een IP-adres gebruikt, wordt een A-record gebruikt.        |
|TTL     | 1        | 1 wordt gebruikt voor 1 uur        |
|TTL-eenheid     | Uren        | Uren worden gebruikt als Hallo tijdmeting         |
|Alias     | webserver.azurewebsites.NET        | Hallo DNS-naam die u maakt Hallo alias, in dit voorbeeld is Hallo webserver.azurewebsites.net DNS-naam op die door standaard toohello web-app.        |


![Een CNAME-record maken](./media/dns-custom-domain/createcnamerecord.png)

Navigeer terug toohello app service die is geconfigureerd voor de aangepaste domeinnaam Hallo. Klik op **aangepaste domeinen**, klikt u vervolgens op **hostnamen**. tooadd hello CNAME-record dat u hebt gemaakt, klikt u op **+ toevoegen hostnaam**.

![afbeelding 1](./media/dns-custom-domain/figure1.png)

Uitvoeren zodra het Hallo-proces is voltooid, **nslookup** toovalidate naamomzetting werkt.

![afbeelding 1](./media/dns-custom-domain/finalnslookup.png)

toolearn meer informatie over het toewijzen van een aangepast domein tooApp Service, gaat u naar [toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](../app-service-web/app-service-web-tutorial-custom-domain.md?toc=%dns%2ftoc.json).

Als u een aangepast domein toopurchase nodig hebt, gaat u naar [aanschaffen van een aangepaste domeinnaam voor Azure-Web-Apps](../app-service-web/custom-dns-web-site-buydomains-web-app.md) toolearn meer informatie over App Service-domeinen.

## <a name="blob-storage"></a>Blob Storage

Hallo gaat volgende stappen u door het configureren van een CNAME-record voor een blob storage-account via Hallo asverify-methode. Deze methode ervoor zorgt dat er is geen uitvaltijd.

Navigeer te**opslag** > **Opslagaccounts**, selecteer uw storage-account en klikt u op **aangepaste domeinen**. Hallo FQDN onder stap 2 specificeren, wordt deze waarde gebruikt toocreate Hallo eerste CNAME-record

![BLOB storage aangepast domein](./media/dns-custom-domain/blobcustomdomain.png)

Navigeer tooyour DNS-Zone en klik op **+ Recordset**. Hallo volgende informatie op Hallo invullen **recordset toevoegen** blade en klik op **OK** toocreate deze.


|Eigenschap  |Waarde  |Beschrijving  |
|---------|---------|---------|
|Naam     | asverify.mystorageaccount        | Deze waarde samen met het domeinnaamlabel Hallo is Hallo FQDN-naam voor de aangepaste domeinnaam Hallo.        |
|Type     | CNAME        | Gebruik een CNAME-record maakt gebruik van een alias.        |
|TTL     | 1        | 1 wordt gebruikt voor 1 uur        |
|TTL-eenheid     | Uren        | Uren worden gebruikt als Hallo tijdmeting         |
|Alias     | asverify.adatumfunctiona9ed.BLOB.Core.Windows.NET        | Hallo DNS-naam die u maakt Hallo alias, in dit voorbeeld is Hallo asverify.adatumfunctiona9ed.blob.core.windows.net DNS-naam op die door de storage-standaardaccount toohello.        |

Navigeer terug tooyour storage-account door te klikken op **opslag** > **Opslagaccounts**, selecteer uw storage-account en klik op **aangepaste domeinen**. Type in Hallo alias u zonder Hallo asverify voorvoegsel in het tekstvak hello, het selectievakje gemaakt ** indirecte CNAME-validatie gebruiken en op **opslaan**. Nadat deze stap voltooid is, retourneren tooyour DNS-zone en maakt u een CNAME-record zonder Hallo asverify voorvoegsel.  Daarna zijn veilig toodelete Hallo CNAME-record met Hallo cdnverify voorvoegsel.

![BLOB storage aangepast domein](./media/dns-custom-domain/indirectvalidate.png)

DNS-omzetting valideren door te voeren`nslookup`

informatie over het toewijzen van een aangepast domein tooa blob storage-eindpunt toolearn [een aangepaste domeinnaam configureren voor het eindpunt van de Blob-opslag](../storage/blobs/storage-custom-domain-name.md?toc=%dns%2ftoc.json)

## <a name="azure-cdn"></a>Azure CDN

Hallo gaat volgende stappen u door het configureren van een CNAME-record voor een CDN-eindpunt met Hallo cdnverify methode. Deze methode ervoor zorgt dat er is geen uitvaltijd.

Navigeer te**Networking** > **CDN-profielen**, selecteer uw CDN-profiel en klikt u op **eindpunten** onder **algemene**.

Selecteer Hallo eindpunt u werkt met en klikt u op **+ aangepaste domeinen**. Opmerking Hallo **hostnaam van het eindpunt** als deze waarde Hallo record is die Hallo CNAME-record verwijst.

![Aangepaste CDN-domein](./media/dns-custom-domain/endpointcustomdomain.png)

Navigeer tooyour DNS-Zone en klik op **+ Recordset**. Hallo volgende informatie op Hallo invullen **recordset toevoegen** blade en klik op **OK** toocreate deze.

|Eigenschap  |Waarde  |Beschrijving  |
|---------|---------|---------|
|Naam     | cdnverify.mycdnendpoint        | Deze waarde samen met het domeinnaamlabel Hallo is Hallo FQDN-naam voor de aangepaste domeinnaam Hallo.        |
|Type     | CNAME        | Gebruik een CNAME-record maakt gebruik van een alias.        |
|TTL     | 1        | 1 wordt gebruikt voor 1 uur        |
|TTL-eenheid     | Uren        | Uren worden gebruikt als Hallo tijdmeting         |
|Alias     | cdnverify.adatumcdnendpoint.azureedge.NET        | Hallo DNS-naam die u maakt Hallo alias, in dit voorbeeld is Hallo cdnverify.adatumcdnendpoint.azureedge.net DNS-naam op die door de storage-standaardaccount toohello.        |

Navigeer terug tooyour CDN-eindpunt door te klikken op **Networking** > **CDN-profielen**, en selecteer uw CDN-profiel. Klik op **+ aangepaste domeinen** uw CNAME-record alias zonder Hallo cdnverify voorvoegsel invoeren en op **toevoegen**.

Nadat deze stap voltooid is, retourneren tooyour DNS-zone en maakt u een CNAME-record zonder Hallo cdnverify voorvoegsel.  Daarna zijn veilig toodelete Hallo CNAME-record met Hallo cdnverify voorvoegsel. Voor meer informatie over CDN en hoe tooconfigure een aangepast domein zonder Hallo tussenliggende registratiestap naar [kaart Azure CDN inhoud tooa aangepast domein](../cdn/cdn-map-content-to-custom-domain.md?toc=%dns%2ftoc.json).

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe te[omgekeerde DNS voor services die worden gehost in Azure configureren](dns-reverse-dns-for-azure-services.md).

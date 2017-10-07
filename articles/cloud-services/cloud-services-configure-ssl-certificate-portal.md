---
title: aaaConfigure SSL voor een cloudservice | Microsoft Docs
description: Meer informatie over hoe toospecify een HTTPS-eindpunt voor een Webrol en hoe tooupload een SSL-certificaat toosecure uw toepassing. Deze voorbeelden hello Azure-portal gebruiken.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 371ba204-48b6-41af-ab9f-ed1d64efe704
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: b19283bb7b0e95374f2ae9c3532eb1effc7d6a9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-ssl-for-an-application-in-azure"></a>SSL configureren voor een toepassing in Azure
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-configure-ssl-certificate-portal.md)
> * [Klassieke Azure Portal](cloud-services-configure-ssl-certificate.md)
>

Secure Socket Layer (SSL)-versleuteling is Hallo meest gebruikte methode voor het beveiligen van gegevens via Hallo verzonden van internet. Deze algemene taak wordt beschreven hoe toospecify een HTTPS-eindpunt voor een Webrol en hoe tooupload een SSL-certificaat toosecure uw toepassing.

> [!NOTE]
> Hallo procedures in deze taak gelden tooAzure Cloudservices; Zie voor App-Services, [dit](../app-service-web/web-sites-configure-ssl-certificate.md).
>

Deze taak maakt gebruik van een productie-implementatie. Informatie over het gebruik van een gefaseerde installatie-implementatie wordt op Hallo einde van dit onderwerp aangeboden.

Lees [dit](cloud-services-how-to-create-deploy-portal.md) eerste als u nog geen een cloudservice hebt gemaakt.

[!INCLUDE [websites-cloud-services-css-guided-walkthrough](../../includes/websites-cloud-services-css-guided-walkthrough.md)]

## <a name="step-1-get-an-ssl-certificate"></a>Stap 1: Haal een SSL-certificaat
tooconfigure SSL voor een toepassing, moet u eerst tooget een SSL-certificaat dat is ondertekend door een certificeringsinstantie (CA), een vertrouwde derde die certificaten voor dit doel verleent. Als u nog geen een, moet u tooobtain van een bedrijf dat SSL-certificaten verkoopt.

Hallo-certificaat moet voldoen aan Hallo volgens de vereisten voor SSL-certificaten in Azure:

* Hallo-certificaat moet een persoonlijke sleutel bevatten.
* Hallo-certificaat moet worden gemaakt voor sleuteluitwisseling, exporteerbaar tooa Personal Information Exchange (.pfx)-bestand.
* Hallo onderwerpnaam van het certificaat moet overeenkomen met Hallo domein gebruikt tooaccess Hallo-cloudservice. U kunt een SSL-certificaat kan niet verkrijgen van een certificeringsinstantie (CA) voor Hallo cloudapp.net domein. U moet een aangepast domein naam toouse verkrijgen wanneer toegang krijgen tot uw service. Wanneer u een certificaat bij een Certificeringsinstantie aanvraagt, de onderwerpnaam van het Hallo-certificaat moet overeenkomen met Hallo aangepast domein naam die wordt gebruikt tooaccess uw toepassing. Bijvoorbeeld, als uw aangepaste domeinnaam is **contoso.com** zou u een certificaat aanvragen van uw Certificeringsinstantie voor ***. contoso.com** of **www.contoso.com**.
* Hallo-certificaat moet ten minste 2048-bits codering gebruiken.

Voor testdoeleinden kunt u [maken](cloud-services-certs-create.md) en een zelfondertekend certificaat gebruiken. Een zelfondertekend certificaat is niet geverifieerd via een Certificeringsinstantie en Hallo cloudapp.net domein kunt gebruiken als Hallo website-URL. Hallo volgende taak gebruikt bijvoorbeeld een zelfondertekend certificaat in welke Hallo is de algemene naam (CN) in Hallo certificaat gebruikt **sslexample.cloudapp.net**.

Vervolgens moet u informatie over Hallo certificaat opnemen in uw servicedefinitie en configuratiebestanden van de service.

<a name="modify"> </a>

## <a name="step-2-modify-hello-service-definition-and-configuration-files"></a>Stap 2: De bestanden voor het definitie- en configuratie van de Hallo wijzigen
Uw toepassing moet geconfigureerde toouse Hallo certificaat en een HTTPS-eindpunt moet worden toegevoegd. Als gevolg hiervan moeten hello servicedefinitie en configuratiebestanden van de service toobe bijgewerkt.

1. Open in uw ontwikkelomgeving Hallo servicedefinitiebestand (CSDEF), Voeg een **certificaten** sectie binnen Hallo **WebRole** sectie en bevatten Hallo volgende informatie over de certificaat (en tussenliggende certificaten):

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="My"
                        permissionLevel="limitedOrElevated" />
            <!-- IMPORTANT! Unless your certificate is either
            self-signed or signed directly by hello CA root, you
            must include all hello intermediate certificates
            here. You must list them here, even if they are
            not bound tooany endpoints. Failing toolist any of
            hello intermediate certificates may cause hard-to-reproduce
            interoperability problems on some clients.-->
            <Certificate name="CAForSampleCertificate"
                        storeLocation="LocalMachine"
                        storeName="CA"
                        permissionLevel="limitedOrElevated" />
        </Certificates>
    ...
    </WebRole>
    ```

   Hallo **certificaten** sectie definieert Hallo-naam van onze certificaat, de locatie en de naam op Hallo van Hallo store waar deze zich bevinden.

   Machtigingen (`permisionLevel` kenmerk) kan worden ingesteld tooone Hallo de volgende waarden:

   | Waarde van machtiging | Beschrijving |
   | --- | --- |
   | limitedOrElevated |**(Standaard)**  Alle processen van de rol toegang tot de persoonlijke sleutel Hallo. |
   | verhoogde |Alleen processen met verhoogde bevoegdheden hebben toegang tot de persoonlijke sleutel Hallo. |

2. Voeg in het servicedefinitiebestand een **Invoereindpunt** element in Hallo **eindpunten** sectie tooenable HTTPS:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Endpoints>
            <InputEndpoint name="HttpsIn" protocol="https" port="443"
                certificate="SampleCertificate" />
        </Endpoints>
    ...
    </WebRole>
    ```

3. Voeg in het servicedefinitiebestand een **Binding** element in Hallo **Sites** sectie. Dit element wordt toegevoegd een HTTPS-binding toomap de tooyour eindpunt site:

   ```xml
    <WebRole name="CertificateTesting" vmsize="Small">
    ...
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="HttpsIn" endpointName="HttpsIn" />
                </Bindings>
            </Site>
        </Sites>
    ...
    </WebRole>
    ```

   Alle Hallo vereiste wijzigingen toohello servicedefinitiebestand zijn voltooid; maar u moet nog steeds tooadd Hallo-certificaatinformatie naar Hallo serviceconfiguratiebestand.
4. Voeg in uw serviceconfiguratiebestand (CSCFG) ServiceConfiguration.Cloud.cscfg, een **certificaten** waarde met die van uw certificaat. Hallo volgende codevoorbeeld geeft details van Hallo **certificaten** sectie, met uitzondering van de vingerafdrukwaarde Hallo.

   ```xml
    <Role name="Deployment">
    ...
        <Certificates>
            <Certificate name="SampleCertificate"
                thumbprint="9427befa18ec6865a9ebdc79d4c38de50e6316ff"
                thumbprintAlgorithm="sha1" />
            <Certificate name="CAForSampleCertificate"
                thumbprint="79d4c38de50e6316ff9427befa18ec6865a9ebdc"
                thumbprintAlgorithm="sha1" />
        </Certificates>
    ...
    </Role>
    ```

(In dit voorbeeld wordt **sha1** voor Hallo vingerafdruk van het algoritme. Hallo geschikte waarde voor de algoritme van de vingerafdruk van het certificaat opgeven.)

Nu dat Hallo-service definitie- en configuratiebestanden zijn bijgewerkt, het pakket uw implementatie voor het uploaden van tooAzure. Als u **cspack**, gebruik niet de **/generateConfigurationFile** markeren, zoals die de gegevens van het certificaat dat u zojuist hebt ingevoegd wordt overschreven.

## <a name="step-3-upload-a-certificate"></a>Stap 3: Een certificaat uploaden
Verbinding maken met toohello Azure-portal en...

1. In Hallo **alle resources** sectie Hallo-Portal, selecteer uw cloudservice.

    ![Uw cloudservice publiceren](media/cloud-services-configure-ssl-certificate-portal/browse.png)

2. Klik op **certificaten**.

    ![Klik op het pictogram Hallo-certificaten](media/cloud-services-configure-ssl-certificate-portal/certificate-item.png)

3. Klik op **uploaden** bovenaan Hallo Hallo certificaten gebied.

    ![Klik op Hallo uploaden menu-item](media/cloud-services-configure-ssl-certificate-portal/Upload_menu.png)

4. Hallo bieden **bestand**, **wachtwoord**, klikt u vervolgens op **uploaden** Hallo Hallo vermelding gegevensgebied onderaan in.

## <a name="step-4-connect-toohello-role-instance-by-using-https"></a>Stap 4: Toohello rolinstantie verbinding via HTTPS
Nu dat uw implementatie actief in Azure is, kunt u tooit via HTTPS verbinding maken.

1. Klik op Hallo **Site-URL** tooopen up Hallo webbrowser.

   ![Klik op Hallo Site-URL](media/cloud-services-configure-ssl-certificate-portal/navigate.png)

2. Wijzig in uw webbrowser Hallo koppeling toouse **https** in plaats van **http**, en Ga naar de pagina Hallo.

   > [!NOTE]
   > Als u een zelfondertekend certificaat gebruikt wanneer u HTTPS-eindpunt voor tooan die is gekoppeld aan de zelf-ondertekend certificaat Hallo bladert, ziet u mogelijk een certificaatfout in Hallo browser. Met behulp van een certificaat dat is ondertekend door een vertrouwde certificeringsinstantie wordt voorkomen dat u dit probleem; in Hallo kunt u tussentijd Hallo fout negeren. (Een andere optie is certificaatarchief Vertrouwde certificaat tooadd Hallo zelf-ondertekend certificaat toohello van gebruiker.)
   >
   >

   ![Voorbeeld van de site](media/cloud-services-configure-ssl-certificate-portal/show-site.png)

   > [!TIP]
   > Als u toouse SSL voor een gefaseerde installatie-implementatie in plaats van een productie-implementatie wilt, moet u eerst toodetermine Hallo-URL die wordt gebruikt voor Hallo staging-implementatie. Zodra uw cloudservice is geïmplementeerd, Hallo URL toohello staging-omgeving wordt bepaald door Hallo **implementatie-ID** GUID in deze indeling:`https://deployment-id.cloudapp.net/`  
   >
   > Een certificaat maken met de Hallo algemene naam (CN) gelijk toohello op basis van GUID-URL (bijvoorbeeld **328187776e774ceda8fc57609d404462.cloudapp.net**). Gebruik Hallo portal tooadd Hallo certificaat tooyour gefaseerde service in de cloud. Voeg Hallo informatie tooyour CSDEF- en CSCFG-certificaatbestanden, opnieuw inpakken van uw toepassing en uw gefaseerde implementatie toouse Hallo nieuw pakket bijwerken.
   >

## <a name="next-steps"></a>Volgende stappen
* [Algemene configuratie van uw cloudservice](cloud-services-how-to-configure-portal.md).
* Meer informatie over hoe te[implementeren van een cloudservice](cloud-services-how-to-create-deploy-portal.md).
* Configureer een [aangepaste domeinnaam](cloud-services-custom-domain-name-portal.md).
* [Beheren van uw cloudservice](cloud-services-how-to-manage-portal.md).

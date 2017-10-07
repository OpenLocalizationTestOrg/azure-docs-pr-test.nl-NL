---
title: aaaBind een bestaande aangepaste SSL-certificaat tooAzure Web-Apps | Microsoft Docs
description: Meer informatie over tootoobind een aangepaste SSL-certificaat tooyour web-app, back-end voor mobiele app of API-app in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Binden van een bestaande aangepaste SSL-certificaat tooAzure Web-Apps

Azure Web Apps biedt een zeer schaalbaar, zelf patch webhosting-service. Deze zelfstudie laat zien hoe toobind een aangepaste SSL-certificaat die u hebt aangeschaft via een vertrouwde certificeringsinstantie te[Azure Web Apps](app-service-web-overview.md). Wanneer u klaar bent, moet u kunnen tooaccess uw web-app op Hallo HTTPS-eindpunt van uw aangepaste DNS-domein.

![Web-app met aangepaste SSL-certificaat](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Upgrade van uw app-prijscategorie
> * Uw aangepaste SSL-certificaat tooApp Service binden
> * Afdwingen van HTTPS voor uw app
> * SSL-certificaat-binding met scripts automatiseren

> [!NOTE]
> Als u een aangepaste SSL-certificaat tooget nodig, kunt u één in hello Azure-portal rechtstreeks ophalen en bindt dit tooyour web-app. Ga als volgt Hallo [App Service Certificate zelfstudie](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

- [Een App Service-app maken](/azure/app-service/)
- [Toewijzen van een aangepaste DNS-naam tooyour web-app](app-service-web-tutorial-custom-domain.md)
- Een SSL-certificaat van een vertrouwde certificeringsinstantie verkrijgen

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Vereisten voor SSL-certificaat

een certificaat in App Service toouse, Hallo certificaat moet voldoen aan alle Hallo volgens de vereisten:

* Ondertekend door een vertrouwde certificeringsinstantie
* Geëxporteerd als een PFX-wachtwoord is beveiligd bestand
* Persoonlijke sleutel van minstens 2048 bits bevat lang
* Bevat alle tussenliggende certificaten in de certificaatketen Hallo

> [!NOTE]
> **Elliptic Curve Cryptography (ECC)-certificaten** kunt werken met App Service, maar worden niet behandeld in dit artikel wordt beschreven. Werken met uw certificeringsinstantie op Hallo exacte stappen toocreate ECC-certificaten.

## <a name="prepare-your-web-app"></a>Voorbereiden van uw web-app

toobind een aangepaste SSL-certificaat tooyour web-app, uw [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet Hallo **Basic**, **standaard**, of **Premium** laag. In deze stap maakt ervoor u zorgen dat uw web-app wordt in Hallo ondersteund prijscategorie.

### <a name="log-in-tooazure"></a>Meld u bij tooAzure

Open Hallo [Azure-portal](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Navigeer tooyour web-app

In het linkermenu hello, klikt u op **App Services**, en klik vervolgens op Hallo-naam van uw web-app.

![Web-app selecteren](./media/app-service-web-tutorial-custom-ssl/select-app.png)

U bevindt zich in de pagina voor het beheren van uw web-app Hallo.  

### <a name="check-hello-pricing-tier"></a>Hallo prijscategorie controleren

Schuif in de linkernavigatiebalk Hallo van uw app webpagina toohello **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Controleer toomake ervoor dat uw web-app niet wordt Hallo **vrije** of **gedeelde** laag. De huidige tier uw web-app is gemarkeerd met een donker blauw vak.

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

Aangepaste SSL wordt niet ondersteund in Hallo **vrije** of **gedeelde** laag. Als u nodig hebt tooscale, stappen Hallo in de volgende sectie Hallo. Anders sluit Hallo **Kies uw prijscategorie** pagina en te overslaan[uploaden en de SSL-certificaat binden](#upload).

### <a name="scale-up-your-app-service-plan"></a>Uw App Service-abonnement opschalen

Selecteer een van de Hallo **Basic**, **standaard**, of **Premium** lagen.

Klik op **Selecteren**.

![Kies de prijscategorie](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Wanneer u de volgende kennisgeving Hallo ziet, is Hallo schaalbewerking is voltooid.

![Melding opschalen](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>SSL-certificaat binden

U gereed tooupload zijn uw SSL-certificaat tooyour web-app.

### <a name="merge-intermediate-certificates"></a>Tussenliggende certificaten samenvoegen

Als uw certificeringsinstantie meerdere certificaten in de certificaatketen hello geeft, moet u toomerge Hallo certificaten in de volgorde. 

toodo moet dit open elk certificaat u hebt ontvangen in een teksteditor. 

Maak een bestand voor Hallo Samengevoegde certificaat, genaamd _mergedcertificate.crt_. Kopieer Hallo inhoud van elk certificaat in dit bestand in een teksteditor. Hallo-volgorde van uw certificaten moet eruitzien als Hallo sjabloon te volgen:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>TooPFX certificaat exporteren

Uw samengevoegde SSL-certificaat met persoonlijke sleutel Hallo die uw certificaataanvraag is gegenereerd met exporteren.

Als u de certificaataanvraag met het OpenSSL gegenereerd, kunt u een bestand met een persoonlijke sleutel hebt gemaakt. tooexport uw certificaat tooPFX, Hallo volgende opdracht uitvoeren. Vervang de tijdelijke aanduidingen Hallo  _&lt;persoonlijke sleutelbestand >_ en  _&lt;samengevoegd--certificaatbestand >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

Wanneer u wordt gevraagd, moet u een wachtwoord voor export definiëren. U hebt dit wachtwoord gebruiken tijdens het uploaden van uw SSL-certificaat tooApp Service later.

Als u IIS gebruikt of _Certreq.exe_ toogenerate uw certificaataanvraag, installatie Hallo certificaat tooyour lokale computer, en vervolgens [exporteren Hallo certificaat tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Uw SSL-certificaat uploaden

tooupload uw SSL-certificaat, klik op **SSL-certificaten** in Hallo linkernavigatiebalk van uw web-app.

Klik op **-certificaat uploaden**.

In **PFX-certificaatbestand**, selecteer uw PFX-bestand. In **certificaatwachtwoord**, type Hallo wachtwoord die u hebt gemaakt tijdens het exporteren van Hallo PFX-bestand.

Klik op **Uploaden**.

![Certificaat uploaden](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Wanneer de App Service klaar is met uw certificaat uploaden, wordt deze in Hallo **SSL-certificaten** pagina.

![Certificaat geüpload](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>SSL-certificaat binden

In Hallo **SSL-bindingen** sectie, klikt u op **binding toevoegen**.

In Hallo **SSL-Binding toevoegen** pagina, Hallo opgegeven waarin dropdowns tooselect Hallo domain name toosecure en Hallo certificaat toouse gebruiken.

> [!NOTE]
> Als u uw certificaat hebt geüpload, maar niet Hallo domein /-namen in Hallo ziet **hostnaam** vervolgkeuzelijst probeer Hallo browserpagina te vernieuwen.
>
>

In **SSL Type**, selecteer of toouse  **[indicatie voor Server-naam (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  of SSL op basis van IP.

- **Op basis van SNI SSL** -op basis van meerdere SNI SSL-bindingen kunnen worden toegevoegd. Met deze optie kunt u meerdere SSL-certificaten toosecure meerdere domeinen op Hallo hetzelfde IP-adres. De meeste moderne browsers (met inbegrip van Internet Explorer, Chrome, Firefox en Opera) ondersteuning voor SNI (vinden uitgebreidere browser ondersteuningsinformatie op [Servernaamindicatie](http://wikipedia.org/wiki/Server_Name_Indication)).
- **IP-gebaseerde SSL** -slechts één IP-gebaseerde SSL-binding kan worden toegevoegd. Deze optie kan slechts één SSL-certificaat toosecure een specifieke openbare IP-adres. toosecure meerdere domeinen, kunt u beveiligen door ze met behulp van alle Hallo SSL-certificaat. Dit is de traditionele optie Hallo voor SSL-binding.

Klik op **Binding toevoegen**.

![SSL-certificaat binden](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Wanneer de App Service klaar is met uw certificaat uploaden, wordt deze in Hallo **SSL-bindingen** secties.

![Certificaat gebonden tooweb app](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Opnieuw toewijzen van een record voor IP-SSL

Als u geen IP-gebaseerde SSL in uw web-app gebruikt, gaat u verder te[Test HTTPS voor uw aangepaste domein](#test).

Uw web-app maakt standaard gebruik van een gedeelde openbare IP-adres. Wanneer u een certificaat met SSL op basis van IP verbonden, wordt een nieuwe, toegewezen IP-adres voor uw web-app in App Service gemaakt.

Als u een A-record tooyour-web-app hebt gekoppeld, bijwerken van uw domein register met dit nieuwe, toegewezen IP-adres.

Uw web-app **aangepaste domeinen** pagina met Hallo nieuwe, toegewezen IP-adres wordt bijgewerkt. [Kopieer dit IP-adres](app-service-web-tutorial-custom-domain.md#info), klikt u vervolgens [opnieuw toewijzen Hallo een record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nieuwe IP-adres.

<a name="test"></a>

## <a name="test-https"></a>Test HTTPS

Alles wat toodo nu is verdwenen toomake ervoor dat HTTPS voor uw aangepaste domein werkt is. In verschillende browsers te bladeren`https://<your.custom.domain>` toosee die het van uw web-app fungeert.

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Als uw web-app biedt u validatiefouten van het certificaat, gebruikt u waarschijnlijk een zelfondertekend certificaat.
>
> Als dat niet Hallo geval is, mogelijk hebt u weggelaten tussenliggende certificaten wanneer u uw certificaat toohello PFX-bestand exporteren.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>HTTPS afdwingen

App Service biedt *niet* afdwingen HTTPS, zodat iedereen nog steeds toegang tot uw web-app met behulp van HTTP. tooenforce HTTPS voor uw web-app definiëren een regel herschrijven in Hallo _web.config_ -bestand voor uw web-app. App Service maakt gebruik van dit bestand, ongeacht de taalframework Hallo van uw web-app.

> [!NOTE]
> Er is een specifieke taal zijn gebonden omleiding van aanvragen. ASP.NET MVC kunt Hallo [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filter in plaats van de regel voor het herschrijven van Hallo in _web.config_.

Als u een .NET-ontwikkelaar bent, moet u relatief vertrouwd zijn met dit bestand zijn. Het is in de hoofdmap Hallo van uw oplossing.

U kunt ook als u met PHP, Node.js, Python of Java ontwikkelt, is er een kans we dit bestand namens jou gegenereerd in App Service.

Verbinding maken met tooyour van web-app FTP-eindpunt met behulp Hallo-instructies in [implementeren van uw app tooAzure App Service met behulp van FTP/S](app-service-deploy-ftp.md).

Dit bestand moet zich in _/home/site/wwwroot_. Als dit niet het geval is, maakt u een _web.config_ bestand in deze map Hello XML te volgen:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Voor een bestaande _web.config_ bestand, Hallo gehele kopiëren `<rule>` element in uw _web.config_van `configuration/system.webServer/rewrite/rules` element. Als er andere `<rule>` elementen in uw _web.config_, plaats Hallo gekopieerd `<rule>` element voordat andere Hallo `<rule>` elementen.

Deze regel wordt een HTTP 301 (permanente omleiding) toohello HTTPS-protocol wanneer Hallo gebruiker een HTTP-aanvraag tooyour web-app maakt. Bijvoorbeeld, wordt hij omgeleid van `http://contoso.com` te`https://contoso.com`.

Zie voor meer informatie over Hallo herschrijven van IIS URL's module Hallo [herschrijven van URL's](http://www.iis.net/downloads/microsoft/url-rewrite) documentatie.

## <a name="enforce-https-for-web-apps-on-linux"></a>Afdwingen van HTTPS voor Web-Apps op Linux

Op Linux-App Service biedt *niet* afdwingen HTTPS, zodat iedereen nog steeds toegang tot uw web-app met behulp van HTTP. tooenforce HTTPS voor uw web-app definiëren een regel herschrijven in Hallo _.htaccess_ -bestand voor uw web-app. 

Verbinding maken met tooyour van web-app FTP-eindpunt met behulp Hallo-instructies in [implementeren van uw app tooAzure App Service met behulp van FTP/S](app-service-deploy-ftp.md).

In _/home/site/wwwroot_, maak een _.htaccess_ bestand met de volgende code Hallo:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Deze regel wordt een HTTP 301 (permanente omleiding) toohello HTTPS-protocol wanneer Hallo gebruiker een HTTP-aanvraag tooyour web-app maakt. Bijvoorbeeld, wordt hij omgeleid van `http://contoso.com` te`https://contoso.com`.

## <a name="automate-with-scripts"></a>Automatiseren met behulp van scripts

U kunt SSL-bindingen automatiseren voor uw web-app met behulp van scripts, met behulp van Hallo [Azure CLI](/cli/azure/install-azure-cli) of [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>Azure CLI

Hallo na de opdracht een geëxporteerde PFX-bestand uploadt en Hallo vingerafdruk opgehaald.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Hallo voegt volgende opdracht een SNI op basis van een SSL-binding, met de vingerafdruk van het Hallo uit de vorige opdracht Hallo.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Hallo volgende opdracht een geëxporteerde PFX-bestand uploadt en voegt een SNI op basis van een SSL-binding.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Upgrade van uw app-prijscategorie
> * Uw aangepaste SSL-certificaat tooApp Service binden
> * Afdwingen van HTTPS voor uw app
> * SSL-certificaat-binding met scripts automatiseren

Hoe gaan van de volgende zelfstudie toolearn toohello toouse Azure Content Delivery Network.

> [!div class="nextstepaction"]
> [Toevoegen van een Content Delivery Network (CDN) tooan Azure App Service](app-service-web-tutorial-content-delivery-network.md)

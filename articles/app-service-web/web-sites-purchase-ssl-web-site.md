---
title: aaaAdd een SSL-certificaat tooyour Azure App Service-app | Microsoft Docs
description: Meer informatie over hoe tooadd een SSL-certificaat tooyour App Service-app.
services: app-service
documentationcenter: .net
author: ahmedelnably
manager: stefsch
editor: cephalin
tags: buy-ssl-certificates
ms.assetid: cdb9719a-c8eb-47e5-817f-e15eaea1f5f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/19/2016
ms.author: apurvajo
ms.openlocfilehash: f4652794ba745790a073264f6a102c64c73e8db0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="buy-and-configure-an-ssl-certificate-for-your-azure-app-service"></a>Een SSL-certificaat kopen en configureren voor uw Azure App Service

In deze zelfstudie wordt u uw web-app beveiligen door het aanschaffen van een SSL-certificaat voor uw  **[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714)**, veilig opslaan in [Azure Key Vault](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis), en het koppelen van met een aangepast domein.

## <a name="step-1---log-in-tooazure"></a>Stap 1 - logboek in tooAzure

Meld u bij toohello Azure-portal op http://portal.azure.com

## <a name="step-2---place-an-ssl-certificate-order"></a>Stap 2: een SSL-certificaat bestelling plaatsen

U kunt een SSL-certificaat-volgorde plaatsen door het maken van een nieuw [App Service-certificaat](https://portal.azure.com/#create/Microsoft.SSL) In Hallo **Azure-portal**.

![Maken van het certificaat](./media/app-service-web-purchase-ssl-web-site/createssl.png)

Voer een beschrijvende **naam** voor uw SSL-certificaat en Voer Hallo **domeinnaam**

> [!NOTE]
> Dit is een van de meest kritieke onderdelen van het aankoopproces Hallo Hallo. Zorg ervoor dat tooenter hostnaam (aangepast domein) dat u wilt dat tooprotect met dit certificaat te corrigeren. **GEEN** Hallo hostnaam met WWW toevoegen. 
>

Selecteer uw **abonnement**, **resourcegroep**, en **SKU van het certificaat**

> [!WARNING]
> App Service Certificate kan alleen worden gebruikt door andere Services App binnen Hallo hetzelfde abonnement.  
>

## <a name="step-3---store-hello-certificate-in-azure-key-vault"></a>Stap 3 - Store Hallo certificaat in Azure Sleutelkluis

> [!NOTE]
> [Sleutelkluis](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-whatis) is een Azure-service die helpt bij het beschermen van de cryptografische sleutels en geheimen beveiligen die door cloudtoepassingen en -services.
>

Zodra de Hallo SSL-certificaat aankoop is voltooid, moet u tooopen [App Service Certificate](https://portal.azure.com/#blade/HubsExtension/Resources/resourceType/Microsoft.CertificateRegistration%2FcertificateOrders) Resource-blade.

![afbeelding van gereed toostore invoegen in KV](./media/app-service-web-purchase-ssl-web-site/ReadyKV.png)

U ziet dat certificaatstatus **"In behandeling zijnde uitgifte"** omdat er meer stappen moet toocomplete voordat u kunt met dit certificaat.

Klik op **Certificaatconfiguratie** in eigenschappen voor certificaat-blade en klik op **stap 1: Store** toostore dit certificaat in Azure Sleutelkluis.

Van **Sleutelkluis Status** Blade, klikt u op **Sleutelkluis opslagplaats** toochoose een bestaande Sleutelkluis toostore dit certificaat **of maak nieuwe Sleutelkluis** toocreate nieuwe sleutel kluis binnen hetzelfde abonnement en de resource-groep.

> [!NOTE]
> Azure Sleutelkluis heeft minimale kosten voor het opslaan van dit certificaat.
> Zie voor meer informatie  **[prijsinformatie voor Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/)**.
>

Nadat u hebt Hallo Sleutelkluis opslagplaats toostore geselecteerd dit certificaat in, Hallo **Store** optie geslaagd moet worden weergegeven.

![afbeelding van store slagen van KV invoegen](./media/app-service-web-purchase-ssl-web-site/KVStoreSuccess.png)

## <a name="step-4---verify-hello-domain-ownership"></a>Stap 4 - Hallo domein eigendom verifiëren

> [!NOTE]
> Er zijn drie soorten verificatie van het domein wordt ondersteund door App service Certificate: domein, E-mail, handmatige verificatie. Deze worden beschreven in meer informatie in Hallo [geavanceerde sectie](#advanced).

Hallo van dezelfde **Certificaatconfiguratie** blade die u in stap 3 gebruikt, klikt u op **stap 2: Controleer of**.

**Verificatie van domein** dit is de meest geschikte proces Hallo **alleen als** u  **[uw aangepaste domein via Azure App Service hebt aangeschaft.](custom-dns-web-site-buydomains-web-app.md)**
Klik op **controleren** knop toocomplete deze stap.

![afbeelding van domeinverificatie invoegen](./media/app-service-web-purchase-ssl-web-site/DomainVerificationRequired.png)

Wanneer u op **controleren**, hello gebruiken **vernieuwen** knop tot Hallo **controleren** optie geslaagd moet worden weergegeven.

![afbeelding van INSERT verifiëren in KV](./media/app-service-web-purchase-ssl-web-site/KVVerifySuccess.png)

## <a name="step-5---assign-certificate-tooapp-service-app"></a>Stap 5: certificaat tooApp Service-App toewijzen

> [!NOTE]
> Voordat u Hallo stappen in deze sectie, moet een aangepaste domeinnaam hebt gekoppeld aan uw app. Zie voor meer informatie  **[configureren van een aangepaste domeinnaam voor een web-app.](app-service-web-tutorial-custom-domain.md)**
>

In Hallo  **[Azure-portal](https://portal.azure.com/)**, klikt u op Hallo **App Service** optie op Hallo links van het Hallo-pagina.

Klik op Hallo-naam van uw app toowhich gewenste tooassign dit certificaat.

In Hallo **instellingen**, klikt u op **SSL-certificaten**.

Klik op **App Service-certificaat importeren** en selecteer Hallo-certificaat dat u zojuist hebt aangeschaft.

![afbeelding van het certificaat importeren invoegen](./media/app-service-web-purchase-ssl-web-site/ImportCertificate.png)

In Hallo **ssl-bindingen** sectie Klik op **bindingen toevoegen**, Hallo opgegeven waarin dropdowns tooselect Hallo domain name toosecure gebruiken met SSL en Hallo toouse certificaat. U kunt ook selecteren of toouse  **[indicatie voor Server-naam (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  of IP op basis van SSL.

![afbeelding van SSL-bindingen worden ingevoegd](./media/app-service-web-purchase-ssl-web-site/SSLBindings.png)

Klik op **toevoegen Binding** toosave Hallo wijzigingen en SSL in te schakelen.

> [!NOTE]
> Als u hebt geselecteerd **IP SSL gebaseerde** en uw aangepaste domein is geconfigureerd met een A-record, moet u Hallo extra stappen uitvoeren. Deze worden beschreven in meer informatie in Hallo [geavanceerde sectie](#Advanced).

Op dit moment u moet kunnen toovisit uw app met `HTTPS://` in plaats van `HTTP://` tooverify die Hallo certificaat correct is geconfigureerd.

<!--![insert image of https](./media/app-service-web-purchase-ssl-web-site/Https.png)-->

## <a name="step-6---management-tasks"></a>Stap 6: beheertaken

### <a name="azure-cli"></a>Azure CLI

[!code-azurecli[main](../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")] 

### <a name="powershell"></a>PowerShell

[!code-powershell[main](../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]

## <a name="advanced"></a>Geavanceerd

### <a name="verifying-domain-ownership"></a>Domein eigendom verifiëren

Er zijn twee soorten verificatie van het domein wordt ondersteund door App service Certificate: e-Mail en handmatige verificatie.

#### <a name="mail-verification"></a>Controle e-mail

Al is bevestigingsmail verzonden e-mailadres gekoppeld aan dit aangepaste domein toohello.
toocomplete hello e verificatiestap Hallo e-mail openen en klik op Hallo bevestigingslink.

![afbeelding van e-mailverificatie invoegen](./media/app-service-web-purchase-ssl-web-site/KVVerifyEmailSuccess.png)

Als u tooresend Hallo bevestigingsmail nodig hebt, klikt u op Hallo **E-mail opnieuw verzenden** knop.

#### <a name="manual-verification"></a>Handmatige verificatie

> [!IMPORTANT]
> HTML-pagina verificatie (werkt alleen met standaard SKU van het certificaat.)
>

1. Maken van een HTML-bestand met de naam **'starfield.html'**

1. Inhoud van dit bestand moet de exacte naam Hallo Hallo domein verificatie Token. (U kunt Hallo-token van Hallo domein verificatie Status Blade kopiëren)

1. Dit bestand in de hoofdmap Hallo van Hallo-webserver die als host fungeert voor uw domein niet uploaden`/.well-known/pki-validation/starfield.html`

1. Klik op **vernieuwen** tooupdate Hallo certificaatstatus nadat verificatie is voltooid. Het kan enkele minuten duren voordat toocomplete voor verificatie.

> [!TIP]
> Controleer of in een terminal met `curl -G http://<domain>/.well-known/pki-validation/starfield.html` antwoord Hallo Hallo moet bevatten `<verification-token>`.

#### <a name="dns-txt-record-verification"></a>Controle van DNS TXT-Record

1. Maak een TXT-record met uw DNS-beheer op Hallo `@` subdomein met waarde gelijk toohello domein verificatie Token.
1. Klik op **'Vernieuwen'** tooupdate Hallo certificaatstatus nadat verificatie is voltooid.

> [!TIP]
> U moet een TXT-record toocreate op `@.<domain>` met waarde `<verification-token>`.

### <a name="assign-certificate-tooapp-service-app"></a>Toewijzen van certificaat tooApp Service-App

Als u hebt geselecteerd **IP SSL gebaseerde** en uw aangepaste domein is geconfigureerd met een A-record, moet u Hallo extra stappen uitvoeren:

Nadat u hebt geconfigureerd SSL-binding op basis van een IP-adres, een vast IP-adres toegewezen tooyour app. U kunt dit IP-adres vinden op Hallo **aangepaste domeinen** pagina onder de instellingen van uw app, direct boven Hallo **hostnamen** sectie. Deze wordt vermeld als **externe IP-adres**

![afbeelding van IP-SSL invoegen](./media/app-service-web-purchase-ssl-web-site/virtual-ip-address.png)

Houd er rekening mee dat dit IP-adres anders is dan het virtuele IP-adres Hallo eerder tooconfigure Hallo A-record voor uw domein gebruikte. Als u zijn geconfigureerd toouse SNI op basis van SSL, of zijn niet geconfigureerd toouse SSL, er is geen adres wordt vermeld voor dit item.

Met de hulpprogramma's geleverd door uw domeinnaamregistrar Hallo Hallo een record voor uw aangepaste domein naam toopoint toohello IP-adres van de vorige stap Hallo wijzigen.

## <a name="rekey-and-sync-hello-certificate"></a>Opnieuw genereren van sleutels en Sync Hallo certificaat

Als u ooit tooRekey uw certificaat moet, selecteert u **sleutel opnieuw genereren en synchroniseren** optie van **certificaateigenschappen** Blade.

Klik op **sleutel opnieuw genereren** knop tooinitiate Hallo proces. Dit kan toocomplete 1-10 minuten duren.

![afbeelding van de sleutel opnieuw genereren SSL invoegen](./media/app-service-web-purchase-ssl-web-site/Rekey.png)

Het certificaat opnieuw genereren van sleutels wordt Hallo-certificaat met een nieuw certificaat is uitgegeven door de certificeringsinstantie Hallo getotaliseerd.

## <a name="next-steps"></a>Volgende stappen

* [Een Content Delivery Network toevoegen](app-service-web-tutorial-content-delivery-network.md)
---
title: een actieve DNS-server aaaMigrate naam tooAzure App Service | Microsoft Docs
description: Meer informatie over hoe een aangepaste DNS-domeinnaam al tooa toegewezen is toomigrate live site tooAzure App Service zonder uitvaltijd.
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: jimbe
tags: top-support-issue
ms.assetid: 10da5b8a-1823-41a3-a2ff-a0717c2b5c2d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/28/2017
ms.author: cephalin
ms.openlocfilehash: fbc4cc30dcb87efb2e867cb65c5404b667661e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-an-active-dns-name-tooazure-app-service"></a>Migreren van een actieve DNS-naam tooAzure App Service

Dit artikel laat zien hoe toomigrate een actieve DNS-server te naam[Azure App Service](../app-service/app-service-value-prop-what-is.md) zonder uitvaltijd.

Wanneer u een live site en de DNS-domein naam tooApp Service migreert, is al live verkeer voor de DNS-naam. U kunt uitvaltijd in DNS-omzetting tijdens de migratie Hallo voorkomen door de optie preventief Hallo actieve DNS-naam tooyour App Service-app-binding.

Als u niet over uitvaltijd in DNS-omzetting vastgesteld, Zie [toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps](app-service-web-tutorial-custom-domain.md).

## <a name="prerequisites"></a>Vereisten

Deze instructies toocomplete:

- [Zorg ervoor dat uw app in App Service zich niet in de laag gratis](app-service-web-tutorial-custom-domain.md#checkpricing).

## <a name="bind-hello-domain-name-preemptively"></a>Hallo-domeinnaam optie preventief binden

Wanneer u een aangepast domein optie preventief bindt, gedaan beide Hallo volgende voordat u wijzigingen aanbrengt in de DNS-records:

- Domein verifiëren
- Hallo-domeinnaam voor uw app inschakelen

Wanneer u ten slotte uw aangepaste DNS-naam van de oude site toohello App Service-app van Hallo migreert, zal er geen uitvaltijd in DNS-omzetting.

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-domain-verification-record"></a>Domein verificatie-record maken

tooverify domein eigendom, Add een TXT-record. Hallo TXT-record wordt toegewezen uit _awverify.&lt; subdomein >_ too_&lt;appname >. azurewebsites.net_. 

Hallo TXT-record u moet, is afhankelijk van Hallo gewenste toomigrate van DNS-record. Zie voor voorbeelden Hallo tabel (`@` doorgaans vertegenwoordigt hoofddomein Hallo):  

| Voorbeeld van DNS-record | TXT-Host | TXT-waarde |
| - | - | - |
| @ (root) | _awverify_ | _&lt;AppName >. azurewebsites.net_ |
| www (sub) | _awverify.www_ | _&lt;AppName >. azurewebsites.net_ |
| \*(jokertekens) | _awverify.\*_ | _&lt;AppName >. azurewebsites.net_ |

Houd er rekening mee Hallo recordtype Hallo DNS-naam die u wilt dat toomigrate in uw pagina DNS-records. App Service biedt ondersteuning voor toewijzingen van CNAME- en A-records.

### <a name="enable-hello-domain-for-your-app"></a>Hallo-domein voor uw app inschakelen

In Hallo [Azure-portal](https://portal.azure.com), linkernavigatiegedeelte van de pagina app Hallo Hallo in, selecteer **aangepaste domeinen**. 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

In Hallo **aangepaste domeinen** pagina, selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Type Hallo volledig gekwalificeerde domeinnaam Hallo TXT-record, zoals wordt toegevoegd `www.contoso.com`. Voor een jokertekendomein (zoals \*. contoso.com), kunt u een DNS-naam die overeenkomt met de Hallo jokertekendomein. 

Selecteer **valideren**.

Hallo **hostnaam toevoegen** knop wordt geactiveerd. 

Zorg ervoor dat **hostnaam recordtype** toohello DNS-recordtype gewenste toomigrate is ingesteld.

Selecteer **hostnaam toevoegen**.

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina. Vernieuw Hallo browser tooupdate Hallo gegevens.

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Uw aangepaste DNS-naam is nu ingeschakeld in uw app in Azure. 

## <a name="remap-hello-active-dns-name"></a>Opnieuw toewijzen Hallo actieve DNS-naam

Hallo alleen ding links toodo is opnieuw toewijzen van uw actieve DNS-record toopoint tooApp Service. Rechts nu nog steeds verwijst tooyour oude site.

<a name="info"></a>

### <a name="copy-hello-apps-ip-address-a-record-only"></a>Kopiëren van de app Hallo IP-adres (alleen een record)

Als u opnieuw van een CNAME-record toewijzen, moet u deze sectie overslaan. 

tooremap een A-record, moet u Hallo App Service-app van externe IP-adres, die wordt weergegeven in Hallo **aangepaste domeinen** pagina.

Sluit Hallo **hostnaam toevoegen** pagina door te selecteren **X** in de rechterbovenhoek Hallo. 

In Hallo **aangepaste domeinen** pagina, te kopiëren van de app Hallo IP-adres.

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

### <a name="update-hello-dns-record"></a>Hallo DNS-record bijwerken

Selecteer Hallo DNS-record tooremap terug in Hallo DNS-records pagina van de domeinprovider van uw.

Voor Hallo `contoso.com` voorbeeld van domein hoofdmap, Hallo A of CNAME-record zoals Hallo voorbeelden in de volgende tabel Hallo opnieuw toewijzen: 

| FQDN-voorbeeld | Recordtype | Host | Waarde |
| - | - | - | - |
| Contoso.com (root) | A | `@` | IP-adres uit [kopie Hallo app IP-adres](#info) |
| www.contoso.com (sub) | CNAME | `www` | _&lt;AppName >. azurewebsites.net_ |
| \*. contoso.com (jokertekens) | CNAME | _\*_ | _&lt;AppName >. azurewebsites.net_ |

Uw instellingen opslaan.

DNS-query's moeten beginnen met het oplossen van App Service-app tooyour onmiddellijk nadat de DNS-servers gebeurt.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe toobind een aangepaste SSL-certificaat tooApp Service.

> [!div class="nextstepaction"]
> [Binden van een bestaande aangepaste SSL-certificaat tooAzure Web-Apps](app-service-web-tutorial-custom-ssl.md)

---
title: een bestaande aangepaste DNS-server aaaMap naam tooAzure Web-Apps | Microsoft Docs
description: Meer informatie over hoe tooadd een bestaand domein voor aangepaste DNS-naam (vanity domein) tooa web-app, back-end voor mobiele app of API-app in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: dc446e0e-0958-48ea-8d99-441d2b947a7c
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 2c4eea3c56c758ca11355554321ffa52dd2c6b9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="map-an-existing-custom-dns-name-tooazure-web-apps"></a>Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps

[Azure Web Apps](app-service-web-overview.md) biedt een uiterst schaalbare webhostingservice met self-patchfunctie. Deze zelfstudie leert u hoe toomap een bestaande aangepaste DNS-Server name tooAzure Web-Apps.

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> * Een subdomein toewijzen (bijvoorbeeld `www.contoso.com`) met behulp van een CNAME-record
> * Toewijzen van een hoofddomein (bijvoorbeeld `contoso.com`) met behulp van een A-record
> * Toewijzen van een jokertekendomein (bijvoorbeeld `*.contoso.com`) met behulp van een CNAME-record
> * Domein-toewijzing met scripts automatiseren

U kunt ofwel een **CNAME-record** of een **een record** toomap een aangepaste DNS-naam tooApp Service. 

> [!NOTE]
> Het is raadzaam dat u een CNAME voor alle aangepaste DNS-namen, behalve een hoofddomein (bijvoorbeeld `contoso.com`).

toomigrate een live site en de DNS-domein naam tooApp Service, Zie [migreren van een actieve DNS-naam tooAzure App Service](app-service-custom-domain-name-migrate.md).

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie:

* [Een App Service-app maken](/azure/app-service/), of gebruik een app die u hebt gemaakt voor een andere zelfstudie.
* Een domeinnaam kopen en controleer of dat u toegang toohello DNS-register hebt voor uw domeinprovider (zoals GoDaddy).

  Bijvoorbeeld: tooadd DNS-vermeldingen voor `contoso.com` en `www.contoso.com`, moet u kunnen tooconfigure Hallo DNS-instellingen voor Hallo `contoso.com` hoofddomein.

  > [!NOTE]
  > Als u een bestaand domein, Geef een naam, kunt u geen [aanschaffen van een domein via Azure portal Hallo](custom-dns-web-site-buydomains-web-app.md). 

## <a name="prepare-hello-app"></a>Hallo app voorbereiden

een aangepaste DNS-naam tooa van web-app, web-app Hallo toomap [App Service-abonnement](https://azure.microsoft.com/pricing/details/app-service/) moet een betaald laag (**gedeelde**, **Basic**, **standaard**, of  **Premium**). In deze stap maakt ervoor u zorgen dat Hallo App Service-app in Hallo is prijscategorie ondersteund.

### <a name="sign-in-tooazure"></a>Meld u aan tooAzure

Open Hallo [Azure-portal](https://portal.azure.com) en meld u aan met uw Azure-account.

### <a name="navigate-toohello-app-in-hello-azure-portal"></a>Navigeer in hello Azure-portal toohello app

Selecteer in het linkermenu Hallo **App Services**, en selecteer vervolgens de naam Hallo van Hallo-app.

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/select-app.png)

U ziet de pagina voor het beheren van App Service-app Hallo Hallo.  

<a name="checkpricing"></a>

### <a name="check-hello-pricing-tier"></a>Hallo prijscategorie controleren

Schuif in Hallo linkernavigatiebalk van de pagina app hello, toohello **instellingen** sectie en selecteer **opschalen (App Service-abonnement)**.

![Omhoog schalen-menu](./media/app-service-web-tutorial-custom-domain/scale-up-menu.png)

de huidige tier Hallo-app wordt door een rand gemarkeerd. Controleren of die Hallo-app niet Hallo toomake **vrije** laag. Aangepaste DNS wordt niet ondersteund in Hallo **vrije** laag. 

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/check-pricing-tier.png)

Hallo App Service-abonnement is niet als **vrije**, sluit Hallo **Kies uw prijscategorie** pagina en te overslaan[toewijzen van een CNAME-record](#cname).

<a name="scaleup"></a>

### <a name="scale-up-hello-app-service-plan"></a>Hallo opschalen met App Service-abonnement

Selecteer een van de Hallo-free lagen (**gedeelde**, **Basic**, **standaard**, of **Premium**). 

Klik op **Selecteren**.

![Controleer de prijscategorie](./media/app-service-web-tutorial-custom-domain/choose-pricing-tier.png)

Wanneer u de volgende kennisgeving Hallo ziet, is Hallo schaalbewerking is voltooid.

![Schaal bewerking bevestigen](./media/app-service-web-tutorial-custom-domain/scale-notification.png)

<a name="cname"></a>

## <a name="map-a-cname-record"></a>Toewijzen van een CNAME-record

In de zelfstudie voorbeeld hello, u een CNAME-record voor Hallo toevoegen `www` subdomein (bijvoorbeeld `www.contoso.com`).

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Hallo CNAME-record maken

Voeg een CNAME-record toomap een subdomein toohello app standaard hostnaam (`<app_name>.azurewebsites.net`).

Voor Hallo `www.contoso.com` domein voorbeeld, Voeg een CNAME-record die Hallo-naam toegewezen `www` te`<app_name>.azurewebsites.net`.

Nadat u Hallo CNAME toegevoegd, ziet de pagina Hallo DNS-records Hallo voorbeeld te volgen:

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record.png)

### <a name="enable-hello-cname-record-mapping-in-azure"></a>Hallo CNAME-record toewijzen in Azure inschakelen

Selecteer in de Hallo Hallo op de pagina app linkernavigatiebalk in hello Azure-portal, **aangepaste domeinen**. 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

In Hallo **aangepaste domeinen** pagina van het Hallo-app toevoegen Hallo FQDN aangepaste DNS-naam (`www.contoso.com`) toohello lijst.

Selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Type Hallo volledig gekwalificeerde domeinnaam dat u een CNAME-record, zoals toegevoegd `www.contoso.com`. 

Selecteer **valideren**.

Hallo **hostnaam toevoegen** knop wordt geactiveerd. 

Zorg ervoor dat **hostnaam recordtype** te is ingesteld,**CNAME (www.example.com of elk subdomein)**.

Selecteer **hostnaam toevoegen**.

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname.png)

Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina. Vernieuw Hallo browser tooupdate Hallo gegevens.

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added.png)

Als u een stap gemist of hebt u een typefout gemaakt ergens eerder, ziet u een verificatiefout Hallo Hallo pagina onderaan in.

![Fout bij verificatie](./media/app-service-web-tutorial-custom-domain/verification-error-cname.png)

<a name="a"></a>

## <a name="map-an-a-record"></a>Toewijzen van een A-record

Hallo zelfstudie bijvoorbeeld u een A-record voor het hoofddomein Hallo toevoegen (bijvoorbeeld `contoso.com`). 

<a name="info"></a>

### <a name="copy-hello-apps-ip-address"></a>Kopiëren van de app Hallo IP-adres

toomap een A-record, moet u het externe IP-adres Hallo-app. U vindt dit IP-adres in van de app Hallo **aangepaste domeinen** pagina in hello Azure-portal.

Selecteer in de Hallo Hallo op de pagina app linkernavigatiebalk in hello Azure-portal, **aangepaste domeinen**. 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

In Hallo **aangepaste domeinen** pagina, te kopiëren van de app Hallo IP-adres.

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/mapping-information.png)

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-a-record"></a>Hallo-A-record maken

toomap een A-record tooan-app Service-App vereist **twee** DNS-records:

- Een **A** Noteer toomap toohello app IP-adres.
- Een **TXT** toomap toohello app standaard hostnaam vastleggen `<app_name>.azurewebsites.net`. App Service gebruikt deze record alleen tijdens de configuratie, tooverify dat u Hallo aangepast domein bezit. Nadat u uw aangepaste domein is gevalideerd en geconfigureerd in App Service, kunt u deze TXT-record verwijderen. 

Voor Hallo `contoso.com` domein bijvoorbeeld Hallo A en TXT-records volgens de volgende tabel toohello maken (`@` doorgaans vertegenwoordigt hoofddomein Hallo). 

| Recordtype | Host | Waarde |
| - | - | - |
| A | `@` | IP-adres uit [kopie Hallo app IP-adres](#info) |
| TXT | `@` | `<app_name>.azurewebsites.net` |

Wanneer Hallo records worden toegevoegd, ziet er Hallo pagina DNS-records Hallo voorbeeld te volgen:

![Pagina DNS-records](./media/app-service-web-tutorial-custom-domain/a-record.png)

<a name="enable-a"></a>

### <a name="enable-hello-a-record-mapping-in-hello-app"></a>Hallo de toewijzing van een record in Hallo app inschakelen

Terug in Hallo-app **aangepaste domeinen** pagina in hello Azure-portal, het toevoegen van Hallo FQDN aangepaste DNS-naam (bijvoorbeeld `contoso.com`) toohello lijst.

Selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name.png)

Type Hallo volledig gekwalificeerde domeinnaam Hallo A-record voor, zoals wordt geconfigureerd `contoso.com`.

Selecteer **valideren**.

Hallo **hostnaam toevoegen** knop wordt geactiveerd. 

Zorg ervoor dat **hostnaam recordtype** te is ingesteld,**een record (example.com)**.

Selecteer **hostnaam toevoegen**.

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name.png)

Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina. Vernieuw Hallo browser tooupdate Hallo gegevens.

![Een record die is toegevoegd](./media/app-service-web-tutorial-custom-domain/a-record-added.png)

Als u een stap gemist of hebt u een typefout gemaakt ergens eerder, ziet u een verificatiefout Hallo Hallo pagina onderaan in.

![Fout bij verificatie](./media/app-service-web-tutorial-custom-domain/verification-error.png)

<a name="wildcard"></a>

## <a name="map-a-wildcard-domain"></a>Een jokertekendomein toewijzen

In de zelfstudie voorbeeld Hallo, wijst u een [jokertekens DNS-naam](https://en.wikipedia.org/wiki/Wildcard_DNS_record) (bijvoorbeeld `*.contoso.com`) toohello App Service-app door een CNAME-record toe te voegen. 

[!INCLUDE [Access DNS records with domain provider](../../includes/app-service-web-access-dns-records.md)]

### <a name="create-hello-cname-record"></a>Hallo CNAME-record maken

Voeg een CNAME-record toomap een jokerteken naam toohello app standaard hostnaam (`<app_name>.azurewebsites.net`).

Voor Hallo `*.contoso.com` domein bijvoorbeeld Hallo CNAME-record wordt wijst de naam van de Hallo `*` te`<app_name>.azurewebsites.net`.

Wanneer Hallo CNAME wordt toegevoegd, ziet er Hallo pagina DNS-records Hallo voorbeeld te volgen:

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/cname-record-wildcard.png)

### <a name="enable-hello-cname-record-mapping-in-hello-app"></a>Hallo CNAME-record toewijzing in Hallo app inschakelen

U kunt nu elk subdomein dat overeenkomt met de Hallo jokertekens naam toohello app toevoegen (bijvoorbeeld `sub1.contoso.com` en `sub2.contoso.com` overeen met `*.contoso.com`). 

Selecteer in de Hallo Hallo op de pagina app linkernavigatiebalk in hello Azure-portal, **aangepaste domeinen**. 

![Aangepast domein menu](./media/app-service-web-tutorial-custom-domain/custom-domain-menu.png)

Selecteer Hallo  **+**  pictogram volgende te**hostnaam toevoegen**.

![Hostnaam toevoegen](./media/app-service-web-tutorial-custom-domain/add-host-name-cname.png)

Typ een FQDN-naam die overeenkomt met de Hallo jokertekendomein (bijvoorbeeld `sub1.contoso.com`), en selecteer vervolgens **valideren**.

Hallo **hostnaam toevoegen** knop wordt geactiveerd. 

Zorg ervoor dat **hostnaam recordtype** te is ingesteld,**CNAME-record (www.example.com of elk subdomein)**.

Selecteer **hostnaam toevoegen**.

![DNS-naam toohello app toevoegen](./media/app-service-web-tutorial-custom-domain/validate-domain-name-cname-wildcard.png)

Het kan even duren voor Hallo nieuwe hostnaam toobe weerspiegeld in Hallo-app **aangepaste domeinen** pagina. Vernieuw Hallo browser tooupdate Hallo gegevens.

Selecteer Hallo  **+**  pictogram opnieuw tooadd een andere hostnaam die overeenkomt met de Hallo jokertekendomein. Bijvoorbeeld, Voeg `sub2.contoso.com`.

![CNAME-record is toegevoegd](./media/app-service-web-tutorial-custom-domain/cname-record-added-wildcard2.png)

## <a name="test-in-browser"></a>In de browser testen

Blader toohello DNS-namen die u eerder hebt geconfigureerd (bijvoorbeeld `contoso.com`, `www.contoso.com`, `sub1.contoso.com`, en `sub2.contoso.com`).

![Navigatie in de portal tooAzure app](./media/app-service-web-tutorial-custom-domain/app-with-custom-dns.png)

## <a name="automate-with-scripts"></a>Automatiseren met behulp van scripts

U kunt beheer van aangepaste domeinen met behulp van scripts, automatiseren met behulp van Hallo [Azure CLI](/cli/azure/install-azure-cli) of [Azure PowerShell](/powershell/azure/overview). 

### <a name="azure-cli"></a>Azure CLI 

Hallo volgende opdracht voegt een geconfigureerde aangepaste DNS-naam tooan App Service-app. 

```bash 
az appservice web config hostname add \
    --webapp <app_name> \
    --resource-group <resource_group_name> \ 
    --name <fully_qualified_domain_name> 
``` 

Zie voor meer informatie [toewijzen van een aangepast domein tooa web-app](scripts/app-service-cli-configure-custom-domain.md). 

### <a name="azure-powershell"></a>Azure PowerShell 

Hallo volgende opdracht voegt een geconfigureerde aangepaste DNS-naam tooan App Service-app. 

```PowerShell  
Set-AzureRmWebApp `
    -Name <app_name> `
    -ResourceGroupName <resource_group_name> ` 
    -HostNames @("<fully_qualified_domain_name>","<app_name>.azurewebsites.net") 
```

Zie voor meer informatie [toewijzen van een aangepast domein tooa web-app](scripts/app-service-powershell-configure-custom-domain.md).

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> * Een subdomein toewijzen met behulp van een CNAME-record
> * Een hoofddomein toewijzen met behulp van een A-record
> * Een jokertekendomein toewijzen met behulp van een CNAME-record
> * Domein-toewijzing met scripts automatiseren

De volgende zelfstudie toolearn toohello gaan hoe toobind een aangepaste SSL-certificaat tooa web-app.

> [!div class="nextstepaction"]
> [Binden van een bestaande aangepaste SSL-certificaat tooAzure Web-Apps](app-service-web-tutorial-custom-ssl.md)

---
title: aaaConfigure een aangepaste domeinnaam voor een web-app in Azure App Service die gebruikmaakt van Traffic Manager voor taakverdeling.
description: Gebruik een aangepaste domeinnaam voor een een web-app in Azure App Service met Traffic Manager voor taakverdeling.
services: app-service\web
documentationcenter: 
author: cephalin
manager: cfowler
editor: 
ms.assetid: 0f96c0e7-0901-489b-a95a-e3b66ca0a1c2
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: cephalin
ms.openlocfilehash: dfde5fc6b445b30b10e03dcb03e8d072130d9377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-custom-domain-name-for-a-web-app-in-azure-app-service-using-traffic-manager"></a>Configureren van een aangepaste domeinnaam voor een web-app in Azure App Service met behulp van Traffic Manager
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro-traffic-manager.md)]

Dit artikel bevat algemene instructies voor het gebruik van een aangepaste domeinnaam met Azure App Service die Traffic Manager voor taakverdeling gebruiken.

[!INCLUDE [tmwebsitefooter](../../includes/custom-dns-web-site-traffic-manager-notes.md)]

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Informatie over DNS-records
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-traffic-manager.md)]

<a name="bkmk_configsharedmode"></a>

## <a name="configure-your-web-apps-for-standard-mode"></a>Configureren van uw web-apps voor standaardmodus
[!INCLUDE [modes](../../includes/custom-dns-web-site-modes-traffic-manager.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Een DNS-record voor uw aangepaste domein toevoegen
> [!NOTE]
> Als u domein via Azure App Service Web Apps hebt aangeschaft en vervolgens overslaat stappen uit te voeren en raadpleegt u de laatste stap toohello van [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md) artikel.
> 
> 

tooassociate uw aangepaste domein met een web-app in Azure App Service, moet u een nieuwe vermelding toevoegen in Hallo DNS-tabel voor uw aangepaste domein met behulp van hulpprogramma's van Hallo domeinregistrar die u hebt aangeschaft met de domeinnaam van uw uit. Gebruik Hallo toolocate stappen te volgen en Hallo DNS-hulpprogramma's.

1. Meld u aan bij uw domeinregistrar tooyour-account en zoekt u naar een pagina voor het beheren van DNS-records. Zoek naar koppelingen of gebieden van Hallo site met het label **domeinnaam**, **DNS**, of **naam Serverbeheer**. Vaak een koppeling toothis pagina vindt u gegevens over uw account weer te geven en te zoeken naar een koppeling zoals **mijn domeinen**.
2. Wanneer u Hallo management-pagina voor de domeinnaam gevonden hebt, zoekt u een koppeling waarmee u tooedit Hallo DNS-records. Dit worden vermeld als een **zonebestand**, **DNS-Records**, of als een **Geavanceerd** configuratiekoppeling.
   
   * Hallo-pagina heeft hoogstwaarschijnlijk een aantal records dat al is gemaakt, zoals het koppelen van een vermelding '**@**'of'\*' met een pagina 'domein parkeerplaatsen'. Records voor algemene subdomeinen kunnen ook zoals bevatten **www**.
   * Hallo-pagina wordt vermeld **CNAME-records**, of geef een vervolgkeuzelijst tooselect een recordtype. Het kan ook andere records, zoals vermeld **A-records** en **MX-records**. In sommige gevallen CNAME-records wordt aangeroepen door andere namen, zoals een **Alias-Record**.
   * Hallo-pagina heeft ook velden die u in te stellen**kaart** van een **hostnaam** of **domeinnaam** tooanother domeinnaam.
3. Tijdens het Hallo-details van elke registrar variëren, in het algemeen u toewijzen *van* uw aangepaste domeinnaam (zoals **contoso.com**,) *naar* Hallo Traffic Manager-domeinnaam (**contoso.trafficmanager.net**) die voor uw web-app wordt gebruikt.
   
   > [!NOTE]
   > U kunt ook als een record is al in gebruik en u moet toopreemptively binden van uw apps tooit, kunt u een extra CNAME-record maken. Bijvoorbeeld: toopreemptively bind **www.contoso.com** tooyour web-app, maakt u een CNAME-record van **awverify.www** te**contoso.trafficmanager.net**. U kunt vervolgens 'www.contoso.com' tooyour Web-App toevoegen zonder Hallo 'www' CNAME-record. Zie voor meer informatie [maken DNS-records voor een web-app in een aangepast domein][CREATEDNS].
   > 
   > 
4. Zodra u klaar bent met het toevoegen of wijzigen van DNS-records bij uw registrar, sla de wijzigingen van Hallo.

<a name="enabledomain"></a>

## <a name="enable-traffic-manager"></a>Traffic Manager inschakelen
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-traffic-manager.md)]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie, Hallo [Node.js Developer Center](/develop/nodejs/).

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- URL List -->

[CREATEDNS]: ../dns/dns-web-sites-custom-domain.md

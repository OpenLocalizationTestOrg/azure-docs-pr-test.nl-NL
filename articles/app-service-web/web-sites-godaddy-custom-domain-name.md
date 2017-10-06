---
title: aaaConfigure een aangepaste domeinnaam in Azure App Service (GoDaddy)
description: Meer informatie over hoe een domein toouse naam uit GoDaddy met Azure-Web-Apps
services: app-service
documentationcenter: 
author: erikre
manager: erikre
editor: jimbe
ms.assetid: 33233e30-5846-488f-83f3-b32e5c114564
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/12/2016
ms.author: cephalin
ms.openlocfilehash: 48158ee752f9833249bbf85adf80f572d1c68486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Een aangepaste domeinnaam configureren in Azure App Service configureren (rechtstreeks van GoDaddy gekocht)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Als u een domein via Azure App Service Web Apps hebt aangeschaft vervolgens raadpleegt u de laatste stap toohello van [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md).

In dit artikel bevat instructies over het gebruik van een aangepaste domeinnaam die is gekocht rechtstreeks vanuit [GoDaddy](https://godaddy.com) met [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Informatie over DNS-records
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Een DNS-record voor uw aangepaste domein toevoegen
tooassociate uw aangepaste domein met een web-app in App Service, moet u een nieuwe vermelding toevoegen in Hallo DNS-tabel voor uw aangepaste domein met behulp van hulpprogramma's van GoDaddy. Volgende stappen toolocate Hallo DNS-hulpprogramma's voor GoDaddy.com hello gebruiken

1. Meld u aan tooyour-account met GoDaddy.com en selecteer **Mijn Account** en vervolgens **mijn domeinen beheren**. Selecteer Hallo vervolgkeuzelijst voor Hallo-domeinnaam die u toouse met uw Azure-web-app wilt en selecteer **beheren DNS-**.
   
    ![de pagina aangepast domein voor GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Van Hallo **domein details** pagina, schuiven toohello **DNS-zonebestand** tabblad. Dit is gebruikt voor het toevoegen en wijzigen van DNS-records voor uw domeinnaam Hallo-sectie.
   
    ![Tabblad DNS-zonebestand](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Selecteer **Record toevoegen** tooadd een bestaande record.
   
    te**bewerken** een bestaande record, selecteer Hallo pen en papier pictogram naast Hallo record.
   
   > [!NOTE]
   > Voordat u nieuwe records toevoegt, houd er rekening mee dat de GoDaddy al DNS-records voor populaire subdomeinen heeft gemaakt (aangeroepen **Host** in de editor) zoals **e**, **bestanden**, **mail**, en andere. Als het Hallo-naam die u wenst dat toouse al bestaat, wijzigt u Hallo bestaande record in plaats van een nieuwe maken.
   > 
   > 
3. Wanneer u een record toevoegt, moet u eerst het recordtype Hallo selecteren.
   
    ![Selecteer recordtype](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Vervolgens moet u opgeven Hallo **Host** (Hallo aangepast domein of subdomein) en wat de it **verwijst naar**.
   
    ![zone-record toevoegen](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Bij het toevoegen van een **A-record (host)** -u moet instellen Hallo **Host** veld tooeither  **@**  (Hiermee hoofddomeinnaam, zoals  **Contoso.com**,) * (een jokerteken voor meerdere subdomeinen overeenkomende) of subdomein hello gewenst toouse (bijvoorbeeld **www**.) U moet instellen Hallo **verwijst naar** veld toohello IP-adres van uw Azure-web-app.
   * Bij het toevoegen van een **(alias) CNAME-record** -u moet instellen Hallo **Host** veld toohello subdomein gewenste toouse. Bijvoorbeeld: **www**. U moet instellen Hallo **verwijst naar** veld toohello **. azurewebsites.net** domeinnaam van uw Azure-web-app. Bijvoorbeeld: **contoso.azurewebsites.net**.
4. Klik op **toevoegen van een andere**.
5. Selecteer **TXT** als Hallo recordtype, Geef een **Host** waarde van  **@**  en een **verwijst naar** waarde van  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Deze TXT-record wordt gebruikt door Azure toovalidate dat u bezit Hallo domein beschreven door Hallo een record of Hallo eerste TXT-record. Als Hallo domein is toegewezen toohello web-app in Azure Portal hello, kan dit TXT-record item worden verwijderd.
   > 
   > 
6. Wanneer u klaar bent met het toevoegen of wijzigen van records, klikt u op **voltooien** toosave wijzigingen.

<a name="enabledomain"></a>

## <a name="enable-hello-domain-name-on-your-web-app"></a>Hallo-domeinnaam op uw web-app inschakelen
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service. U hebt geen creditcard nodig en u doet geen toezeggingen.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)


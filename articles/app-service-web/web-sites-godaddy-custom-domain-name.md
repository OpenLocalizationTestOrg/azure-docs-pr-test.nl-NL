---
title: Een aangepaste domeinnaam configureren in Azure App Service (GoDaddy)
description: Informatie over het gebruik van een domeinnaam van GoDaddy met Azure-Web-Apps
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
ms.openlocfilehash: 158c5dc06f83e16633d3c2fbb4eb27d3e8af030c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-custom-domain-name-in-azure-app-service-purchased-directly-from-godaddy"></a>Een aangepaste domeinnaam configureren in Azure App Service configureren (rechtstreeks van GoDaddy gekocht)
[!INCLUDE [web-selector](../../includes/websites-custom-domain-selector.md)]

[!INCLUDE [intro](../../includes/custom-dns-web-site-intro.md)]

Als u verwijzen naar de laatste stap van het domein via Azure App Service Web Apps hebt aangeschaft [domein kopen voor Web-Apps](custom-dns-web-site-buydomains-web-app.md).

In dit artikel bevat instructies over het gebruik van een aangepaste domeinnaam die is gekocht rechtstreeks vanuit [GoDaddy](https://godaddy.com) met [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).

[!INCLUDE [introfooter](../../includes/custom-dns-web-site-intro-notes.md)]

<a name="understanding-records"></a>

## <a name="understanding-dns-records"></a>Informatie over DNS-records
[!INCLUDE [understandingdns](../../includes/custom-dns-web-site-understanding-dns-raw.md)]

<a name="bkmk_configurecname"></a>

## <a name="add-a-dns-record-for-your-custom-domain"></a>Een DNS-record voor uw aangepaste domein toevoegen
Uw aangepaste domein koppelt u een web-app in App Service, moet u een nieuwe vermelding in de DNS-tabel voor uw aangepaste domein toevoegen met behulp van hulpprogramma's van GoDaddy. Gebruik de volgende stappen om te vinden van de DNS-hulpprogramma's voor GoDaddy.com

1. Aanmelden bij uw account met GoDaddy.com en selecteer **Mijn Account** en vervolgens **mijn domeinen beheren**. Selecteer de vervolgkeuzelijst voor de domeinnaam die u wilt gebruiken met uw Azure-web-app en selecteer **beheren DNS-**.
   
    ![de pagina aangepast domein voor GoDaddy](./media/web-sites-godaddy-custom-domain-name/godaddy-customdomain.png)
2. Van de **domein details** pagina, bladert u naar de **DNS-zonebestand** tabblad. Dit is de sectie die is gebruikt voor het toevoegen en wijzigen van DNS-records voor uw domeinnaam.
   
    ![Tabblad DNS-zonebestand](./media/web-sites-godaddy-custom-domain-name/godaddy-zonetab.png)
   
    Selecteer **Record toevoegen** een bestaande record toe te voegen.
   
    Naar **bewerken** een bestaande record, selecteer de pen & papier: het pictogram naast de record.
   
   > [!NOTE]
   > Voordat u nieuwe records toevoegt, houd er rekening mee dat de GoDaddy al DNS-records voor populaire subdomeinen heeft gemaakt (aangeroepen **Host** in de editor) zoals **e**, **bestanden**, **mail**, en andere. Als de naam die u wilt gebruiken, al bestaat, wijzigt u de bestaande record in plaats van een nieuwe maken.
   > 
   > 
3. Wanneer u een record toevoegt, moet u eerst het recordtype selecteren.
   
    ![Selecteer recordtype](./media/web-sites-godaddy-custom-domain-name/godaddy-selectrecordtype.png)
   
    Vervolgens moet u opgeven de **Host** (het aangepaste domein of de subdomeinnaam) en wat de it **verwijst naar**.
   
    ![zone-record toevoegen](./media/web-sites-godaddy-custom-domain-name/godaddy-addzonerecord.png)
   
   * Bij het toevoegen van een **A-record (host)** -stelt u de **Host** naar elk veld  **@**  (Hiermee hoofddomeinnaam, zoals **contoso.com** ,) * (een jokerteken voor meerdere subdomeinen overeenkomende) of het onderliggende domein dat u wilt gebruiken (bijvoorbeeld **www**.) U moet instellen de **verwijst naar** veld in de IP-adres van uw Azure-web-app.
   * Bij het toevoegen van een **(alias) CNAME-record** -stelt u de **Host** veld met het onderliggende domein dat u wilt gebruiken. Bijvoorbeeld: **www**. U moet instellen de **verwijst naar** veld de **. azurewebsites.net** domeinnaam van uw Azure-web-app. Bijvoorbeeld: **contoso.azurewebsites.net**.
4. Klik op **toevoegen van een andere**.
5. Selecteer **TXT** als het recordtype geeft een **Host** waarde van  **@**  en een **verwijst naar** waarde van  **&lt;yourwebappname&gt;. azurewebsites.net**.
   
   > [!NOTE]
   > Deze TXT-record wordt gebruikt door Azure valideren waarvan u eigenaar van het domein dat is beschreven door de A-record of de eerste TXT-record. Als het domein is toegewezen aan de web-app in de Azure Portal, kan dit TXT-record item worden verwijderd.
   > 
   > 
6. Wanneer u klaar bent met het toevoegen of wijzigen van records, klikt u op **voltooien** wijzigingen op te slaan.

<a name="enabledomain"></a>

## <a name="enable-the-domain-name-on-your-web-app"></a>De naam van het domein op uw web-app inschakelen
[!INCLUDE [modes](../../includes/custom-dns-web-site-enable-on-web-site.md)]

> [!NOTE]
> Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service. U hebt geen creditcard nodig en u gaat geen verplichtingen aan.
> 
> 

## <a name="whats-changed"></a>Wat is er gewijzigd
* Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)


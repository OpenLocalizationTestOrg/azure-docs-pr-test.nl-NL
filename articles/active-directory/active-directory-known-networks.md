---
title: aaaKnown netwerken in de klassieke Azure-portal Hallo | Microsoft Docs
description: Door bekende netwerken te configureren, kunt u te voorkomen dat IP-adressen die eigendom zijn van uw organisatie die is opgenomen in Hallo aanmelding aanmeldingen vanaf meerdere locaties en aanmelding aanmeldingen vanaf IP-adressen met verdachte activiteitsrapporten.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: f56e042a-78d5-4ea3-be33-94004f2a0fc3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: ec636cdda172cd3baeb1e606dd8d6e1949fbc63b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="known-networks"></a>Bekende netwerken

> [!div class="op_single_selector"]
> * [Klassieke Azure Portal](active-directory-known-networks.md)
> * [Azure Portal](active-directory-known-networks-azure-portal.md)
> 
> 


U kunt toegang tot Azure Active Directory en gebruik rapporten toogain inzicht in Hallo integriteit en beveiliging van de directory van uw organisatie gebruiken. Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's zodat u ze kunnen toomitigate voldoende plannen die risico's kunnen liggen.

Het is mogelijk dat Hallo '*aanmeldingen vanaf meerdere locaties*'en'*aanmeldingen vanaf IP-adressen met verdachte activiteit*' rapporten markeert IP-adressen die eigendom zijn van uw de organisatie. 

Dit kan bijvoorbeeld gebeuren wanneer: 

* Een gebruiker in uw kantoor Boston heeft op afstand tooyour datacenter in San Francisco triggers Hallo 'Aanmelding aanmeldingen vanaf meerdere locaties' rapport aangemeld 
* Een gebruiker van uw organisatie probeert toosign op meerdere keren met een onjuist wachtwoord triggers Hallo 'Aanmelding aanmeldingen vanaf IP-adressen met verdachte activiteit' rapport 

tooprevent deze gevallen van genereren misleidend beveiliging rapporten, moet u de bekende IP-adresbereiken toohello adreslijst van het openbare IP-adres van uw organisatie toevoegen.    

### <a name="tooadd-your-organizations-public-ip-address-ranges-perform-hello-following-steps"></a>tooadd bereiken van het openbare IP-adres van uw organisatie, voert u Hallo stappen te volgen:

1. Eenmalige aanmelding toohello [Azure-beheerportal](https://manage.windowsazure.com).

2. Klik in het linkerdeelvenster Hallo **Active Directory**. 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-01.png)

3. In Hallo **Directory** tabblad, selecteer uw directory.

4. Klik in het menu bovenaan Hallo Hallo **configureren**. 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-02.png)

5. Op tabblad Hallo configureren, gaat u te**uw organisaties openbare IP-adresbereiken** 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-03.png)

6. Klik op **bekende IP-adresbereiken toevoegen**.

7. Toevoegen van uw-adresbereiken in Hallo dialoogvenster dat wordt weergegeven en klik vervolgens op de knop controleren Hallo wanneer u klaar bent. 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-04.png)

**Aanvullende bronnen:**

* [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md)
* [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Aanmeldingen vanaf meerdere locaties](active-directory-reporting-sign-ins-from-multiple-geographies.md)


---
title: Netwerken bekend in de klassieke Azure portal | Microsoft Docs
description: Door bekende netwerken te configureren, kunt u te voorkomen dat IP-adressen die eigendom zijn van uw organisatie die is opgenomen in de modules aanmelding vanaf meerdere locaties en aanmelding aanmeldingen vanaf IP-adressen met verdachte activiteitsrapporten.
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
ms.openlocfilehash: e4d51d1d2f09fca34d749879e21d49f785eac35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="known-networks"></a>Bekende netwerken

> [!div class="op_single_selector"]
> * [Klassieke Azure Portal](active-directory-known-networks.md)
> * [Azure Portal](active-directory-known-networks-azure-portal.md)
> 
> 


U kunt toegang tot Azure Active Directory- en gebruiksrapporten meer inzicht verkrijgen in de integriteit en beveiliging van de directory van uw organisatie. Met deze informatie kunt kan directory-beheerder beter bepalen waar mogelijk beveiligingsrisico's mogelijk liggen zodat ze voldoende plannen kunnen die risico's te beperken.

Het is mogelijk dat de '*aanmeldingen vanaf meerdere locaties*'en'*aanmeldingen vanaf IP-adressen met verdachte activiteit*' rapporten markeert IP-adressen die eigendom zijn door uw organisatie. 

Dit kan bijvoorbeeld gebeuren wanneer: 

* Een gebruiker in uw office is extern aangemeld bij uw datacenter in San Francisco Boston activeert het rapport 'Aanmeldingen vanaf meerdere locaties' 
* Een gebruiker van uw organisatie wil aanmelding meerdere keren met een onjuist wachtwoord triggers het rapport "Aanmeldingen vanaf IP-adressen met verdachte activiteit" 

Om te voorkomen dat dergelijke gevallen misleidend beveiligingsrapporten genereren, moet u de bekende IP-adresbereiken toevoegen aan de lijst met het openbare IP-adres van uw organisatie.    

### <a name="to-add-your-organizations-public-ip-address-ranges-perform-the-following-steps"></a>Als u wilt toevoegen van uw organisatie openbare IP-adresbereiken, moet u de volgende stappen uitvoeren:

1. Aanmelding bij de [Azure-beheerportal](https://manage.windowsazure.com).

2. Klik in het linkerdeelvenster op **Active Directory**. 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-01.png)

3. In de **Directory** tabblad, selecteer uw directory.

4. Klik in het menu bovenaan op **configureren**. 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-02.png)

5. Op het tabblad configureren, gaat u naar **uw organisaties openbare IP-adresbereiken** 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-03.png)

6. Klik op **bekende IP-adresbereiken toevoegen**.

7. Toevoegen van uw-adresbereiken in het dialoogvenster dat wordt weergegeven en klik vervolgens op de knop controleren wanneer u klaar bent. 

    ![Bekende netwerken](./media/active-directory-known-networks/known-netwoks-04.png)

**Aanvullende bronnen:**

* [Uw toegangs- en gebruiksrapporten weergeven](active-directory-view-access-usage-reports.md)
* [Aanmeldingen vanaf IP-adressen met verdachte activiteiten](active-directory-reporting-sign-ins-from-ip-addresses-with-suspicious-activity.md)
* [Aanmeldingen vanaf meerdere locaties](active-directory-reporting-sign-ins-from-multiple-geographies.md)


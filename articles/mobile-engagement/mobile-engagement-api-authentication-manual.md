---
title: aaaAuthenticate met Mobile Engagement REST-API's - handmatige installatie
description: Hierin wordt beschreven hoe toomanually instellen voor verificatie voor Mobile Engagement REST-API 's
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2e79f9c9-41e4-45ac-b427-3b8338675163
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3884f94afcd6b9a62bfcf498fb6ee84bb6e837b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-with-mobile-engagement-rest-apis---manual-setup"></a>Verificatie met de Mobile Engagement REST-API's - handmatige installatie
Dit is een bijlage documentatie te[verifiëren met Mobile Engagement REST-API's](mobile-engagement-api-authentication.md). Zorg ervoor dat u het eerste tooget Hallo context lezen. Hier wordt een andere manier toodo Hallo eenmalige instelling voor het instellen van de verificatie van uw beschreven voor Hallo met behulp van Mobile Engagement REST-API's hello Azure-Portal. 

> [!NOTE]
> Hallo-instructies die hieronder zijn gebaseerd op deze [Active Directory-handleiding](../azure-resource-manager/resource-group-create-service-principal-portal.md) en aangepast voor wat vereist voor verificatie voor Mobile Engagement-API's is. Raadpleeg tooit dus als u wilt dat toounderstand Hallo stappen hieronder in detail besproken. 
> 
> 

1. Aanmelding tooyour Azure-Account via Hallo [klassieke portal](https://manage.windowsazure.com/).
2. Selecteer **Active Directory** in het linkerdeelvenster Hallo.
   
     ![Selecteer Active Directory][1]
3. Kies Hallo **Active standaarddirectory** in uw Azure-portal. 
   
     ![map te kiezen][2]
   
   > [!IMPORTANT]
   > Deze methode werkt alleen als u in Hallo standaard Active Directory van uw account werkt en niet werken als u dit doen in een Active Directory die u hebt gemaakt in uw account. 
   > 
   > 
4. tooview hello toepassingen in uw directory, klikt u op **toepassingen**.
   
     ![toepassingen weergeven][3]
5. Klik op **toevoegen**. 
   
     ![Toepassing toevoegen][4]
6. Klik op **mijn organisatie ontwikkelt toepassing toevoegen**
   
     ![nieuwe toepassing][5]
7. Vul in de naam van de toepassing hello en selecteer Hallo type toepassing als **WEBTOEPASSING en/of WEB-API** en klik op de volgende knop Hallo.
   
     ![de naam van toepassing][6]
8. U kunt opgeven dat alle dummy-URL's voor **AANMELDINGS-URL** en **APP ID URI**. Ze worden niet gebruikt voor ons scenario en URL's Hallo zelf worden niet gevalideerd.  
   
     ![Toepassingseigenschappen][7]
9. Aan het einde van de Hallo hiervan hebt u een AAD-app met Hallo naam die u eerder Hallo volgende. Dit is uw **AD\_APP\_naam** en noteer deze.  
   
     ![App-naam][8]
10. Klik op de naam van de app Hallo en klik op **configureren**.
    
      ![App configureren][9]
11. Maak een notitie van Hallo CLIENT-ID die wordt gebruikt als **CLIENT\_ID** voor uw API-aanroepen. 
    
     ![App configureren][10]
12. Schuif omlaag toohello **sleutels** gedeelte en een sleutel met bij voorkeur 2 jaar (verlopen) duur toevoegen en klik op **opslaan**. 
    
     ![App configureren][11]
13. Kopieer onmiddellijk Hallo-waarde die wordt weergegeven voor de sleutel Hallo omdat deze nu alleen weergegeven wordt en niet opgeslagen wordt zodat u niet steeds opnieuw weergegeven. Als u deze verliest vervolgens hebt u toogenerate een nieuwe sleutel. Dit is Hallo **CLIENT_SECRET** voor uw API-aanroepen. 
    
     ![App configureren][12]
    
    > [!IMPORTANT]
    > Deze sleutel verlopen op Hallo einde van Hallo duur die u hebt opgegeven in dat geval Zorg ervoor dat toorenew wanneer Hallo nadert anders uw API-verificatie niet meer werkt. U kunt ook verwijderen en opnieuw maken van deze sleutel als u denkt dat deze is geschonden.
    > 
    > 
14. Klik op **EINDPUNTEN weergeven** knop nu Hallo die geopend **App eindpunten** in het dialoogvenster. 
    
    ![][13]
15. Hallo App eindpunten in het dialoogvenster kopiëren Hallo **OAUTH 2.0-TOKENEINDPUNT**. 
    
    ![][14]
16. Dit eindpunt worden weergegeven in Hallo formulier te volgen waarbij Hallo GUID in Hallo-URL is uw **TENANT_ID** dus maak een notitie van deze: 
    
        https://login.microsoftonline.com/<GUID>/oauth2/token
17. Er wordt nu tooconfigure Hallo machtigingen voor deze app worden voortgezet. Hiervoor hebt u tooopen up Hallo [Azure-portal](https://portal.azure.com). 
18. Klik op **resourcegroepen** en Hallo zoeken **Mobile Engagement** resourcegroep.  
    
    ![][15]
19. Klik op Hallo **Mobile Engagement** resource groeperen en navigeer toohello **instellingen** blade hier. 
    
    ![][16]
20. Klik op **gebruikers** in Hallo blade instellingen en klik vervolgens op **toevoegen** tooadd een gebruiker. 
    
    ![][17]
21. Klik op **een rol selecteren**
    
    ![][18]
22. Klik op **eigenaar**
    
    ![][19]
23. Zoeken naar de naam van uw toepassing hello **AD\_APP\_naam** in het zoekvak Hallo. U ziet dit hier standaard. Als u deze hebt gevonden, selecteert u deze en klik op **Selecteer** Hallo Hallo blade onderaan in. 
    
    ![][20]
24. Op Hallo **toegang toevoegen** blade, deze wordt weergegeven als **1 gebruiker, 0 groepen**. Klik op **OK** op deze blade tooconfirm Hallo wijziging. 
    
    ![][21]

U hebt nu Hallo vereist AAD-configuratie voltooid en u alle set toocall Hallo API's. 

<!-- Images -->
[1]: ./media/mobile-engagement-api-authentication-manual/active-directory.png
[2]: ./media/mobile-engagement-api-authentication-manual/active-directory-details.png
[3]: ./media/mobile-engagement-api-authentication-manual/view-applications.png
[4]: ./media/mobile-engagement-api-authentication-manual/add-icon.png
[5]: ./media/mobile-engagement-api-authentication-manual/what-do-you-want-to-do.png
[6]: ./media/mobile-engagement-api-authentication-manual/tell-us-about-your-application.png
[7]: ./media/mobile-engagement-api-authentication-manual/app-properties.png
[8]: ./media/mobile-engagement-api-authentication-manual/aad-app.png
[9]: ./media/mobile-engagement-api-authentication-manual/configure-menu.png
[10]: ./media/mobile-engagement-api-authentication-manual/client-id.png
[11]: ./media/mobile-engagement-api-authentication-manual/client_secret.png
[12]: ./media/mobile-engagement-api-authentication-manual/keys.png
[13]: ./media/mobile-engagement-api-authentication-manual/view-endpoints.png
[14]: ./media/mobile-engagement-api-authentication-manual/app-endpoints.png
[15]: ./media/mobile-engagement-api-authentication-manual/resource-groups.png
[16]: ./media/mobile-engagement-api-authentication-manual/resource-groups-settings.png
[17]: ./media/mobile-engagement-api-authentication-manual/add-users.png
[18]: ./media/mobile-engagement-api-authentication-manual/add-role.png
[19]: ./media/mobile-engagement-api-authentication-manual/select-role.png
[20]: ./media/mobile-engagement-api-authentication-manual/add-user-select.png
[21]: ./media/mobile-engagement-api-authentication-manual/add-access-final.png




---
title: aaaWrong set gebruikers worden ingericht tooan Azure AD-galerie toepassing | Microsoft Docs
description: Meer informatie over hoe toofind uit waarom een andere set gebruikers worden ingericht tooan toepassing dan die u verwacht
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: adb90b12a53fb3160ce2b73b2559df92b283438e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="wrong-set-of-users-are-being-provisioned-tooan-azure-ad-gallery-application"></a>Onjuiste reeks gebruikers worden ingericht tooan Azure AD-galerie toepassing

Welke gebruikers zijn ingericht toohello app voornamelijk wordt aangedreven door welke gebruikers en groepen zijn **toegewezen** toohello toepassing.

Gebruik onderstaande toolearn Hallo-bronnen hoe toocheck welke gebruikers en groepen zijn toegewezen tooan toepassing in Azure Active Directory.

## <a name="assign-a-user-directly-as-an-administrator"></a>Een gebruiker toewijzen rechtstreeks als een beheerder

tooassign een of meer gebruikers tooan toepassing rechtstreeks Hallo volgende stappen:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige naam** of **e-mailadres** van Hallo gebruiker u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **gebruiker** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van gebruiker uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één gebruiker**, type in een andere **volledige naam** of **e-mailadres** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd voor deze gebruiker toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met het selecteren van gebruikers, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello gebruikers die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello gebruikers geselecteerd.

Als inrichting is geconfigureerd en actief is voor een app, nieuwe gebruikers ingerichte tooan toepassing in ongeveer 10 minuten moeten. Controleer de Hallo **controlelogboeken** voor meer informatie.

## <a name="assign-a-group-directly-tooan-application-as-an-administrator"></a>Een groep worden toegewezen rechtstreeks tooan toepassing als een beheerder

tooassign een of meer groepen tooan toepassing rechtstreeks Hallo stappen hieronder:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

  * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Hallo-toepassing die u wilt dat een lijst met gebruikers toofrom hello tooassign selecteren.

7.  Nadat de toepassing hello wordt geladen, klikt u op **gebruikers en groepen** uit van de toepassing hello linkerkant navigatiemenu.

8.  Klik op Hallo **toevoegen** knop boven op Hallo **gebruikers en groepen** lijst tooopen hello **toevoegen toewijzing** blade.

9.  Klik op Hallo **gebruikers en groepen** selector van Hallo **toevoegen toewijzing** blade.

10. Type in Hallo **volledige groepsnaam** van Hallo groep u geïnteresseerd bent in het toewijzen van Hallo **zoeken op naam of e-mailadres** zoekvak.

11. Beweeg de muisaanwijzer over Hallo **groep** in Hallo lijst tooreveal een **selectievakje**. Klik op het profiel foto of een logo tooadd Hallo selectievakje volgende toohello van de groep uw gebruiker toohello **geselecteerde** lijst.

12. **Optioneel:** indien te gewenst**toevoegen van meer dan één groep**, type in een andere **volledige groepsnaam** in Hallo **zoeken op naam of e-mailadres** zoekvak en klikt u op Hallo selectievakje tooadd van deze groep toohello **geselecteerde** lijst.

13. Wanneer u klaar bent met groepen te selecteren, klikt u op Hallo **Selecteer** knop tooadd ze toohello lijst met gebruikers en groepen toobe toegewezen toohello toepassing.

14. **Optioneel:** klikt u op Hallo **rol selecteren** selector in Hallo **toevoegen toewijzing** blade tooselect een rol tooassign toohello groepen die u hebt geselecteerd.

15. Klik op Hallo **toewijzen** knop tooassign Hallo toepassing toohello geselecteerde groepen.

Als inrichting geconfigureerd en wordt al uitgevoerd voor een app is, moet de nieuwe gebruikers die zich in de groep Hallo ingerichte tooan toepassing in ongeveer 10 minuten. Controleer de Hallo **controlelogboeken** voor meer informatie.

>[!IMPORTANT]
>Het inrichten van Hallo groepsnaam en details in toevoeging toohello leden, groeperen als ondersteund op bepaalde toepassingen. U kunt inschakelen of uitschakelen van deze functionaliteit met in- of uitschakelen van Hallo **toewijzing** voor een groepsobjecten worden weergegeven in Hallo **inrichten** tabblad. 
>
>

Als inrichting groepen is ingeschakeld, moet u tooreview Hallo kenmerk toewijzingen tooensure een juiste veld wordt gebruikt voor Hallo 'die overeenkomt met de ID'. Dit kan Hallo weergegeven naam of e-mailbericht alias, zoals hello groep en de bijbehorende leden niet worden ingericht als Hallo overeenstemmen van de eigenschap leeg of niet is ingevuld voor een groep in Azure AD.

## <a name="next-steps"></a>Volgende stappen
[Automatisch gebruikers inrichten en Deprovisioning tooSaaS toepassingen met Azure Active Directory](active-directory-saas-app-provisioning.md)

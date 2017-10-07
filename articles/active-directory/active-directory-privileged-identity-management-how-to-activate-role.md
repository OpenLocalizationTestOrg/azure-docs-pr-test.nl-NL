---
title: aaaHow tooactivate een rol of deactiveren | Microsoft Docs
description: Meer informatie over hoe tooactivate rollen voor bevoegde identiteiten met Azure Privileged Identity Management-toepassing hello.
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a>Hoe tooactivate of rollen in Azure AD Privileged Identity Management deactiveren
Azure Active Directory (AD) Privileged Identity Management vereenvoudigt de manier waarop bedrijven beheert tooresources bevoorrechte toegang in Azure AD en andere Microsoft online services zoals Office 365 of Microsoft Intune.  

Als u hebt aangebracht in aanmerking komen voor een beheerderrol, betekent dit dat kunt u die rol wanneer u een bevoegde tooperform acties moet activeren. Bijvoorbeeld, als u af en functies van Office 365 beheren, van uw organisatie bevoorrechte rol administrators mogelijk niet aanbrengen u een permanente hoofdbeheerder omdat die rol van invloed is op andere services te. In plaats daarvan zij u in aanmerking komen voor Azure AD-functies, zoals Exchange Online-beheerder. U kunt tooactivate aanvragen die rol wanneer u de bevoegdheden nodig en vervolgens u controle van de beheerder voor een vooraf vastgestelde periode hebt.

Dit artikel is voor beheerders die tooactivate moeten hun rol in Azure AD Privileged Identity Management (PIM). Het wordt u begeleid Hallo stappen tooactivate een rol wanneer u Hallo machtigingen nodig en Hallo rol deactiveren wanneer u klaar bent. Bevoorrechte rol beheerders kunnen bovendien goedkeuring tooactivate een rol (Preview) vereisen. Meer informatie over [PIM goedkeuringswerkstromen](./privileged-identity-management/azure-ad-pim-approval-workflow.md) hier.

## <a name="add-hello-privileged-identity-management-application"></a>Hallo Privileged Identity Management-toepassing toevoegen
Gebruik hello Azure AD Privileged Identity Management-toepassing in Hallo [Azure-portal](https://portal.azure.com/) toorequest rolactivering, zelfs als u gaat toooperate in een andere portal of PowerShell. Als u geen hello Azure AD Privileged Identity Management-toepassing in uw Azure-portal hebt, volgt u deze stappen tooget gestart.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/).
2. Selecteer uw gebruikersnaam in Hallo rechterbovenhoek van hello Azure-portal en selecteer Hallo directory waar wilt u werkt.
3. Selecteer **meer services** en gebruik Hallo Filter textbox toosearch voor **Azure AD Privileged Identity Management**.
4. Controleer **pincode toodashboard** en klik vervolgens op **maken**. Hallo Privileged Identity Management-toepassing wordt geopend.

## <a name="activate-a-role"></a>Een rol activeren
Wanneer u tootake op een functie nodig hebt, kunt u activering aanvragen door het selecteren van Hallo **mijn rollen** navigatieoptie in hello Azure AD Privileged Identity Management-toepassing de linker navigatie-kolom.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) en selecteer hello Azure AD Privileged Identity Management tegel.
2. Selecteer **mijn rollen**. Een lijst met uw toegewezen in aanmerking komende rollen in Hallo groeperen bovenaan Hallo Hallo pagina weergegeven.
3. Selecteer een rol tooactivate.
4. Selecteer **activeren**. Hallo **rolactivering aanvragen** blade wordt weergegeven.
5. Sommige rollen is multi-factor Authentication (MFA) vereist voordat u de rol Hallo kunt activeren. U hoeft alleen tooauthenticate eenmaal per sessie.
   
    ![Controleer of met MFA voor rolactivering van de - schermafbeelding][2]
6. Hallo reden Hallo activeringsaanvraag worden gedaan in Hallo tekstveld invoeren.  Sommige rollen is vereist toosupply een Ticketnummer problemen.
7. Selecteer **OK**.  Hallo-rol niet goedkeuring vereist, wordt nu wordt geactiveerd als Hallo rol weer te geven in Hallo lijst met actieve rollen (direct onder het Hallo-lijst van in aanmerking komende roltoewijzingen). Als hello [rol is goedkeuring vereist](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, een pop-upmelding wordt kort weergegeven in Hallo rechterbovenhoek van uw browser waarin wordt gemeld Hallo-aanvraag in afwachting van goedkeuring.

    ![Aanvraag in behandeling melding - schermafbeelding][3]

## <a name="deactivate-a-role"></a>Een rol deactiveren
Zodra een rol is geactiveerd, wordt deze automatisch uitgeschakeld wanneer de tijdslimiet (duur in aanmerking komende) is bereikt.

Als u beheertaken vroeg hebt voltooid, kunt u ook een rol handmatig in Azure AD Privileged Identity Management-toepassing hello deactiveren.  Selecteer **mijn rollen**, kies Hallo rol u klaar bent met behulp van Hallo **Active roltoewijzingen** groeperen en selecteer **deactiveren**.  

## <a name="cancel-a-pending-request"></a>Annuleren van een aanvraag in behandeling
In de gebeurtenis Hallo niet hoeven te activeren van een rol die goedkeuring vereist, u kunt een aanvraag in behandeling op elk gewenst moment annuleren. Gewoon Selecteer Hallo **mijn rollen** navigatieoptie in hello Azure AD Privileged Identity Management-toepassing de linker navigatie-kolom.

1. Meld u aan toohello [Azure-portal](https://portal.azure.com/) en selecteer hello Azure AD Privileged Identity Management tegel.
2. Selecteer **mijn rollen**. Een lijst met uw toegewezen in aanmerking komende rollen in Hallo groeperen bovenaan Hallo Hallo pagina weergegeven.
3. Selecteer een rol.
4. Selecteer Hallo **activering is in afwachting van goedkeuring** standaardvaandel op Hallo rol activering details blade.
5. Selecteer **annuleren** bovenaan Hallo Hallo **in afwachting van goedkeuring** blade.

   ![Annuleren van aanvraag in behandeling-schermafbeelding][4]

## <a name="next-steps"></a>Volgende stappen
Als u geïnteresseerd in meer informatie over Azure AD Privileged Identity Management bent, hebben hello volgende koppelingen meer informatie.

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png

---
title: 'Azure Active Directory B2C: Selfservice voor wachtwoordherstel | Microsoft Docs'
description: Een onderwerp te demonstreren hoe tooset up zelf uw wachtwoord opnieuw instellen voor uw consumenten in Azure Active Directory B2C
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: curtand
ms.assetid: c87ed86e-1520-42b1-8c31-46cd44ed5310
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: ff87eea42259b610702da73af35d0a38eb7dd33d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-set-up-self-service-password-reset-for-your-consumers"></a>Azure Active Directory B2C: Selfservice voor wachtwoordherstel voor uw consumenten instellen
Hello selfservice voor wachtwoordherstel functie, uw consumenten (die zich hebben geregistreerd voor lokale accounts) kunnen hun wachtwoorden op hun eigen opnieuw instellen. Dit vermindert het Hallo werkbelasting van uw medewerkers, met name als uw toepassing heeft miljoenen consumenten regelmatig gebruikt. Op dit moment wordt alleen ondersteund als een methode voor het herstellen met behulp van een geverifieerde e-mailadres. In de toekomst Hallo voegen we aanvullende herstelpunten methoden (geverifieerde telefoonnummer, beveiligingsvragen, enz.) toe.

> [!NOTE]
> In dit artikel is van toepassing tooself-service-wachtwoord opnieuw instellen in de context van een beleid voor aanmelden Hallo gebruikt. Als u volledig aanpasbare wachtwoord opnieuw instellen van beleidsregels aangeroepen vanuit uw app nodig hebt, raadpleegt u [in dit artikel](active-directory-b2c-reference-policies.md#create-a-password-reset-policy).
> 
> 

Standaard uw directory geen zelf uw wachtwoord opnieuw instellen is ingeschakeld. Gebruik Hallo volgende stappen tooturn deze op:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com/) zoals Hallo Abonnementsbeheerder. Dit is Hallo dezelfde werken of schoolaccount of hetzelfde Microsoft-account dat u toocreate uw directory gebruikt Hallo.
2. Navigeer toohello Active Directory-extensie op Hallo navigatiebalk aan de linkerkant Hallo.
3. Zoeken naar uw map onder Hallo **Directory** tabblad en klik erop.
4. Klik op Hallo **configureren** tabblad.
5. Schuif omlaag toohello **beleid opnieuw instellen van wachtwoorden** sectie en in-/ uitschakelen Hallo **gebruikers die zijn ingeschakeld voor wachtwoordherstel** te optie**Ja**. U ziet dat Hallo **alternatief e-mailadres** optie is ingeschakeld; ongewijzigd laten.
   
    ![Self-service voor wachtwoord opnieuw instellen](./media/active-directory-b2c-reference-sspr/sspr.png)
6. Klik op **opslaan** Hallo Hallo pagina onderaan in. U bent nu klaar!

tootest, gebruik Hallo 'Nu uitvoeren' functie op elk beleid aanmelden met lokale accounts als een id-provider. Op Hallo lokale account aanmelden pagina (waar u een e-mailadres en wachtwoord, of een gebruikersnaam en wachtwoord), klikt u op **geen toegang tot uw account?** tooverify Hallo consumer ervaring.

> [!NOTE]
> Hallo zelf uw wachtwoord opnieuw instellen van pagina's kunnen worden aangepast met behulp van Hallo [functie huisstijl](../active-directory/active-directory-add-company-branding.md).
> 
> 


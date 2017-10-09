---
title: aaaPreview Office 365-groepen vervaldatum in Azure Active Directory | Microsoft Docs
description: Hoe tooset up verlooptijd voor Office 365 groepen in Azure Active Directory (preview)
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: it-pro
ms.openlocfilehash: a8c99961cff3aad3f4d8b0cc1b2eb8e8a4c9ba95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-office-365-groups-expiration-preview"></a>Verlooptijd van Office 365-groepen (preview) configureren

U kunt nu Hallo levenscyclus van Office 365-groepen beheren door de vervaldatum voor Office 365-groepen die u selecteert. Zodra deze verlooptijd is ingesteld, eigenaars van deze groepen worden gevraagd toorenew als ze nog Hallo groepen moeten de groepen. Een Office 365-groep die niet wordt verlengd worden, verwijderd. Een Office 365-groep is verwijderd, kan door de eigenaars Groepsbeleid Hallo of Hallo beheerder binnen 30 dagen worden hersteld.  


> [!NOTE]
> U kunt instellen dat verlopen voor Office 365-groepen.
>
> Vervaldatum voor O365 groepen is vereist dat een Azure AD Premium-licentie is toegewezen aan
>   - Hallo beheerder Hallo verlopen instellingen voor Hallo tenant configureert
>   - Alle leden van het Hallo-groepen die zijn geselecteerd voor deze instelling

## <a name="set-office-365-groups-expiration"></a>Instellen dat verlopen voor Office 365-groepen

1. Open Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) met een account dat een globale beheerder in uw Azure AD-tenant.

2. Open Azure AD, selecteer **gebruikers en groepen**.

3. Selecteer **groepsinstellingen** en selecteer vervolgens **verlopen** tooopen Hallo verlopen instellingen.
  
  ![Blade verlopen](./media/active-directory-groups-lifecycle-azure-portal/expiration-settings.png)

4. Op Hallo **verlopen** blade kunt u:

  * Hallo groep levensduur in dagen ingesteld. U kunt een van selecteren Hallo vooraf ingestelde waarden of een aangepaste waarde (moet 31 dagen of meer). 
  * Geef een e-mailadres waar Hallo vernieuwing en verlopen-meldingen moeten worden verzonden wanneer een groep geen eigenaar heeft. 
  * Selecteer welke groepen door Office 365 verloopt. U kunt de vervaldatum voor inschakelen **alle** Office 365-groepen die u kunt selecteren uit Hallo Office 365-groepen of u selecteert **geen** verlopen voor alle groepen uitschakelen.
  * Uw instellingen opslaan als u bent met het selecteren van klaar **opslaan**.

Zie voor instructies over hoe toodownload en installeer Microsoft PowerShell-module tooconfigure verlooptijd voor Office 365-groepen via PowerShell hello, [Azure Active Directory V2 PowerShell-Module - openbare Preview-versie 2.0.0.137](https://www.powershellgallery.com/packages/AzureADPreview/2.0.0.137).

E-mailmeldingen zoals deze worden verzonden toohello Office 365-groepeigenaren 30 dagen, 15 dagen en 1 dag voorafgaande tooexpiration van Hallo-groep.

![Verlopen van e-mailmeldingen](./media/active-directory-groups-lifecycle-azure-portal/expiration-notification.png)

Groepseigenaar Hallo kunt selecteren **vernieuwen groep** toorenew Hallo Office 365-groep, of kunt selecteren **gaat toogroup** toosee Hallo leden en andere details over Hallo groep.

Wanneer een groep is verlopen, is één dag na de verloopdatum Hallo door Hallo-groep verwijderd. Een e-mailmelding zoals deze wordt verzonden toohello Office 365-groepeigenaren mededeling over Hallo is verlopen en latere verwijdering van hun Office 365-groep.

![E-mailmeldingen in verwijderen](./media/active-directory-groups-lifecycle-azure-portal/deletion-notification.png)

Hallo-groep kan worden hersteld door het selecteren van **groepsbeleidsobject herstellen** of met behulp van PowerShell-cmdlets, zoals beschreven in [terugzetten van een verwijderde Office 365-groep in Azure Active Directory] (https://docs.microsoft.com/azure/active-directory/ Active-Directory-Groups-Restore-Azure-Portal).
    
Als u terugzet Hallo-groep documenten, SharePoint-sites of andere permanente objecten bevat, duurt het mogelijk up too24 uren toofully terugzetten Hallo groep en de inhoud ervan.

> [!NOTE]
> * Wanneer u instellingen voor verlooptijd Hallo implementeert, is er mogelijk bepaalde groepen die ouder dan Hallo verlopen venster zijn. Deze groepen worden niet onmiddellijk verwijderd, maar zijn too30 dagen tot vervaldatum instellen. Hallo eerste verlenging e-mailmelding wordt verzonden binnen een dag. Bijvoorbeeld groep A 400 dagen geleden is gemaakt en hello verlopen-interval is ingesteld too180 dagen. Wanneer u instellingen voor verlooptijd toepast, heeft groep A 30 dagen voordat deze wordt verwijderd tenzij Hallo eigenaar wordt verlengd.
> * Wanneer een dynamische groep is verwijderd en hersteld, wordt het gezien als een nieuwe groep en opnieuw ingevuld volgens toohello regel. Too24 uur kan duren voordat dit proces.

## <a name="next-steps"></a>Volgende stappen
Deze artikelen bevatten aanvullende informatie over Azure AD-groepen.

* [Zie de bestaande groepen](active-directory-groups-view-azure-portal.md)
* [Instellingen van een groep beheren](active-directory-groups-settings-azure-portal.md)
* [Leden van een groep beheren](active-directory-groups-members-azure-portal.md)
* [Lidmaatschap van een groep beheren](active-directory-groups-membership-azure-portal.md)
* [Dynamische regels voor gebruikers in een groep beheren](active-directory-groups-dynamic-membership-azure-portal.md)

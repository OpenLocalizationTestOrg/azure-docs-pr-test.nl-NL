---
title: aaaHow tooremove een gebruiker de toegang tot de toepassing tooan | Microsoft Docs
description: Begrijpen hoe tooremove een gebruiker de toegang tot de toepassing tooan
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
ms.openlocfilehash: 17017bddb73aad5a0ef3a411ac91bf0423f0b600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooremove-a-users-access-tooan-application"></a>Hoe tooremove een gebruiker de toegang tot de toepassing tooan

In dit artikel kunt u toounderstand hoe tooremove een gebruiker de toegang tot tooan toepassing.

## <a name="i-want-tooremove-a-specific-users-or-groups-assignment-tooan-application"></a>Ik wil tooremove dat een specifieke gebruiker of groep van toewijzing tooan toepassing

een gebruiker of groep toewijzing tooan toepassing tooremove Hallo stappen in Hallo volgen [de toewijzing van een gebruiker of groep verwijderen uit een enterprise-app in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) artikel.

. ## ik wil toodisable alle access tooan-toepassing voor elke gebruiker

toodisable alle aanmeldingen tooan Gebruikerstoepassing, volg Hallo de stappen die worden vermeld in Hallo [gebruikersaanmeldingen een enterprise-App in Azure Active Directory uitschakelen](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) artikel.

## <a name="i-want-toodelete-an-application-entirely"></a>Ik wil dat een toepassing toodelete volledig

te**verwijderen van een toepassing**, volgt u onderstaande instructies voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **hoofdbeheerder** of **Co-beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **bedrijfstoepassingen** van navigatiemenu links aan de Azure Active Directory Hallo.

5.  Klik op **alle toepassingen** tooview een lijst met al uw toepassingen.

   * Als er geen Hallo-toepassing die u wilt dat hier weergegeven, gebruikt u Hallo **Filter** besturingselement bovenaan Hallo Hallo **lijst met alle toepassingen** en set Hallo **weergeven** optie te **Alle aanvragen.**

6.  Selecteer de gewenste toodelete Hallo-toepassing.

7.  Nadat de toepassing hello wordt geladen, klikt u op **verwijderen** pictogram van Hallo bovenste toepassing **overzicht** blade.

## <a name="i-want-toodisable-all-future-user-consent-operations-tooany-application"></a>Ik wil toodisable alle toekomstige toestemming operations tooany-Gebruikerstoepassing

Toestemming van de gebruiker uitschakelt voor uw hele directory voorkomen dat eindgebruikers van ermee akkoord dat tooany toepassing. Beheerders kunnen nog steeds op behalves van de gebruiker toestemming. toolearn meer informatie over de toepassing toestemming geven en waarom u kunt of wilt niet toodo, Lees [wat gebruikers- en toestemming van de beheerder](https://docs.microsoft.com/azure/active-directory/develop/active-directory-devhowto-multi-tenant-overview#understanding-user-and-admin-consent).

te**uitschakelen alle toekomstige gebruikers toestemming bewerkingen in uw hele directory**, volgt u onderstaande instructies voor Hallo:

1.  Open Hallo [ **Azure Portal** ](https://portal.azure.com/) en meld u aan als een **globale beheerder.**

2.  Open Hallo **Azure Active Directory-extensie** door te klikken op **meer services** Hallo Hallo belangrijkste linkerkant navigatiemenu onderaan in.

3.  Typ in **' Azure Active Directory**' in het zoekvak Hallo-filter en selecteer Hallo **Azure Active Directory** item.

4.  Klik op **gebruikers en groepen** in het navigatiemenu Hallo.

5.  Klik op **gebruikersinstellingen**.

6.  Alle toekomstige gebruikers toestemming bewerkingen uitschakelen door Hallo instelling **gebruikers apps tooaccess kunnen toestaan hun gegevens** te schakelen**Nee** en klik op Hallo **opslaan** knop.


# <a name="next-steps"></a>Volgende stappen
[Het beheren van toegang tooapps](active-directory-managing-access-to-apps.md)

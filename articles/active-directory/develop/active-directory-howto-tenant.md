---
title: aaaHow tooget een Azure AD-tenant | Microsoft Docs
description: Hoe tooget een Azure Active Directory-tenant voor het registreren en bouwen van toepassingen.
services: active-directory
documentationcenter: 
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 1f4b24eb-ab4d-4baa-a717-2a0e5b8d27cd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: dcc6b3109528cf763bda9bd527344ea9ab5c0d69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-an-azure-active-directory-tenant"></a>Hoe tooget een Azure Active Directory-tenant
In Azure Active Directory (Azure AD) is een [tenant](https://msdn.microsoft.com/library/azure/jj573650.aspx#BKMK_WhatIsAnAzureADTenant) representatief voor een organisatie.  Het is een toegewezen exemplaar van hello Azure AD-service die een organisatie ontvangt en de eigenaar is wanneer deze zich voor een Microsoft-cloudservice zoals Azure, Microsoft Intune of Office 365 aanmeldt.  Elke Azure AD-tenant is uniek en werkt afzonderlijk van andere Azure AD-tenants.  

Een tenant bevat alle Hallo gebruikers in een bedrijf en Hallo informatie: hun wachtwoorden, gebruikersprofielgegevens, machtigingen en enzovoort.  Het bevat ook groepen, toepassingen en andere informatie over tooan organisatie en de beveiliging.

Azure AD gebruikers toosign tooallow in tooyour toepassing, moet u uw toepassing registreren in een tenant van uzelf.  Het publiceren van een toepassing in een Azure AD-tenant is **helemaal gratis**.  De meeste ontwikkelaars maken verschillende tenants en toepassingen om te experimenten, te ontwikkelen, te faseren en te testen.  Organisaties die zich aanmelden voor en gebruiken van uw toepassing kunt eventueel toopurchase licenties eventueel ze tootake profiteren van geavanceerde directoryfuncties.

Maar hoe kunt u een Azure AD-tenant verkrijgen?  Hallo proces mogelijk enigszins afwijken als u:

* [Een bestaand Office 365-abonnement hebt](#use-an-existing-office-365-subscription)
* [Een bestaand Azure-abonnement hebt dat aan een Microsoft-Account is gekoppeld](#use-an-msa-azure-subscription)
* [Een bestaand Azure-abonnement hebt dat aan een organisatieaccount is gekoppeld](#use-an-organizational-azure-subscription)
* [Geen van bovenstaande Hallo & toostart helemaal wilt](#start-from-scratch)

## <a name="use-an-existing-office-365-subscription"></a>Een bestaand Office 365-abonnement gebruiken
Als u een bestaand Office 365-abonnement hebt, beschikt u al over een Azure AD-tenant. U kunt zich aanmelden in toohello [Azure-portal](https://portal.azure.com) met uw O365-account in en aan de slag met Azure AD.

## <a name="use-an-msa-azure-subscription"></a>Een MSA Azure-abonnement gebruiken
Als u zich eerder hebt geregistreerd voor een Azure-abonnement met uw afzonderlijke Microsoft-account, hebt u al een tenant.  Wanneer u zich aanmeldt toohello [Azure Portal](https://portal.azure.com), wordt u automatisch vastgelegd in tooyour standaard tenant. U staat op het gratis toouse deze tenant als u Zie past - maar gewenste toocreate een organisatie-administrator-account.

toodo dus als volgt.  U kunt ook toocreate desgewenst een nieuwe tenant en een beheerder maken in deze tenant via een vergelijkbare procedure.

1. Meld u aan bij Hallo [Azure Portal](https://portal.azure.com) met uw afzonderlijke account
2. Navigeer toohello 'Azure Active Directory' sectie van de portal hello (gevonden in Hallo linkernavigatiebalk, onder **meer Services**)
3. U moet automatisch aangemeld voor toohello 'Default Directory' als dit niet, kunt u mappen door te klikken op de accountnaam van uw in de rechterbovenhoek Hallo.
4. Van Hallo **snelle taken** sectie **toevoegen van een gebruiker**.
5. In Hallo formulier gebruiker toevoegen, bieden Hallo volgende details:

   * Naam: (kies de gewenste waarde)
   * Gebruikersnaam: (kies een gebruikersnaam op voor deze beheerder)
   * Profiel: (Vul in de juiste waarden voor de naam van de eerste, laatste naam, functietitel en afdeling Hallo)
   * Rol: hoofdbeheerder
6. Wanneer u klaar Hallo formulier gebruiker toevoegen en Hallo tijdelijke wachtwoord voor Hallo nieuwe gebruiker met beheerdersrechten ontvangen, worden ervoor toorecord als u met deze nieuwe gebruiker in volgorde toochange Hallo wachtwoord toologin moet dit wachtwoord. U kunt ook verzenden Hallo wachtwoord rechtstreeks toohello gebruiker met behulp van een alternatief e-mailbericht.
7. Klik op **maken** toocreate Hallo nieuwe gebruiker.
8. toochange hello tijdelijk wachtwoord, meld u aan bij [https://login.microsoftonline.com](https://login.microsoftonline.com) met deze nieuwe gebruiker-account en wijzig Hallo wachtwoord wanneer dit wordt aangevraagd.

## <a name="use-an-organizational-azure-subscription"></a>Een Azure-abonnement voor de organisatie gebruiken
Als u zich eerder hebt geregistreerd voor een Azure-abonnement met uw organisatieaccount, hebt u al een tenant.  In Hallo [Azure Portal](https://portal.azure.com), zult u een tenant wanneer u te navigeren 'Meer Services' en "Azure Active Directory."  U staat op het gratis toouse die deze tenant zoals u ziet past.

## <a name="start-from-scratch"></a>De procedure vanaf het begin uitvoeren
Als alle bovenstaande Hallo informatie tooyou, u hoeft niet.  Ga naar [https://account.windowsazure.com/organization](https://account.windowsazure.com/organization) toosign voor Azure met een nieuwe organisatie.  Nadat u Hallo proces hebt voltooid, hebt u uw eigen Azure AD-tenant met Hallo-domeinnaam die u hebt gekozen tijdens de aanmelding van.  In Hallo [Azure Portal](https://portal.azure.com), kunt u uw tenant vinden door te navigeren 'Azure Active Directory' in hello linkernavigatievenster te gaan.

Als onderdeel van Hallo-proces voor het aanmelden voor Azure, zult u creditcardgegevens tooprovide vereist.  U kunt gerust doorgaan. Er worden namelijk geen kosten in rekening gebracht voor het publiceren van toepassingen in Azure AD of het maken van nieuwe tenants.

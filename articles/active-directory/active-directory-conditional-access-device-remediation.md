---
title: aaaYou geen toegang vanaf nu Hallo van een apparaat met Windows Azure-portal | Microsoft Docs
description: Meer informatie over waar u kunt geen get er hier vandaan en wat u tooavoid die worden uitgevoerd in dit dialoogvenster kan controleren.
services: active-directory
keywords: voorwaardelijke toegang op basis van een apparaat, apparaatregistratie, apparaatregistratie inschakelen, apparaatregistratie en MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a>U kunt daar niet komen vanaf deze locatie op een Windows-apparaat

Tijdens een poging om bijvoorbeeld het SharePoint Online-intranet van uw organisatie te openen, krijgt u een pagina te zien waarop staat dat *u geen toegang hebt*. U ziet deze pagina omdat de beheerder een beleid voor voorwaardelijke toegang waardoor toegang tooyour organisatie resources onder bepaalde omstandigheden heeft geconfigureerd. Het is mogelijk noodzakelijk toocontact helpdesk of uw beheerder tooget dit probleem is opgelost, maar er zijn een aantal dingen die u zelf eerst uitproberen kunt.

Als u een **Windows** apparaat, moet u Hallo volgende controleren:

- Gebruikt u een ondersteunde browser?

- Voert u een ondersteunde versie van Windows uit op het apparaat?

- Is het apparaat compatibel?






## <a name="supported-browser"></a>Ondersteunde browser

Als de beheerder voorwaardelijk toegangsbeleid heeft geconfigureerd, hebt u alleen toegang tot de resources van uw organisatie vanaf een ondersteunde browser. Op een Windows-apparaat worden alleen **Internet Explorer** en **Edge** ondersteund.

U kunt eenvoudig bepalen of u geen toegang een resource vanwege niet-ondersteunde browser tooan tot door te kijken gedeelte van de Hallo details van de foutpagina Hallo:

![Scenario](./media/active-directory-conditional-access-device-remediation/02.png "Berichten over ontoegankelijke toepassingen voor niet-ondersteunde browsers")

Hallo alleen herstel is toouse een browser die de toepassing hello ondersteuning voor uw apparaatplatform biedt. Zie [Ondersteunde browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies) voor een volledige lijst met ondersteunde browsers.  


## <a name="supported-versions-of-windows"></a>Ondersteunde versies van Windows

Hallo volgende moet worden voldaan over Hallo Windows-besturingssysteem op uw apparaat zijn: 

- Als u een besturingssysteem voor Windows-bureaublad op uw apparaat uitvoert, moet deze toobe Windows 7 of hoger.
- Als u een Windows server-besturingssysteem op uw apparaat uitvoert, moet deze toobe Windows Server 2008 R2 of hoger. 


## <a name="compliant-device"></a>Compatibel apparaat

Mogelijk heeft de beheerder een beleid voor voorwaardelijke toegang kunnen resources alleen via compatibele apparaten toegang tooyour organisatie geconfigureerd. compatibel zijn, moet uw apparaat beide gekoppelde tooyour toobe on-premises Active Directory of die lid zijn van tooyour Azure Active Directory.

U kunt eenvoudig bepalen of u geen toegang tot een resource vanwege tooa-apparaat dat is niet compatibel met door te kijken gedeelte van de Hallo details van de foutpagina Hallo:
 
![Scenario](./media/active-directory-conditional-access-device-remediation/01.png "Berichten over ontoegankelijke toepassingen voor niet-geregistreerde apparaten")


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a>Is uw apparaat lid tooan op lokale Active Directory?

**Als uw apparaat is toegevoegd tooan op lokale Active Directory in uw organisatie:**

1. Zorg ervoor dat u zich aanmelden tooWindows met behulp van uw werkaccount (uw Active Directory-account).
2. Verbinding maken met bedrijfsnetwerk via een virtueel particulier netwerk (VPN) of DirectAccess tooyour.
3. Nadat u verbonden bent, drukt u op Hallo Windows-logotoets + L Hallo sleutel toolock uw Windows-sessie.
4. Ontgrendel de Windows-sessie door de referenties voor uw werkaccount in te voeren.
5. Wacht een paar minuten en probeer het vervolgens opnieuw tooaccess Hallo toepassing of service.
6. Als u dezelfde Hallo pagina, klikt u op Hallo **meer details** koppelen en vervolgens contact op met uw beheerder met Hallo details.


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a>Is uw apparaat geen lid zijn van tooan op lokale Active Directory?

Als uw apparaat niet is gekoppeld tooan on-premises Active Directory en Windows 10 wordt uitgevoerd, hebt u twee opties:

* Azure AD Join uitvoeren
* Toevoegen van uw werk of school account tooWindows

Zie [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md) (Windows 10-apparaten gebruiken op uw werkplek) voor informatie over de verschillen tussen deze opties.  
Als het apparaat:

- Tooyour organisatie hoort, moet u Azure AD Join uitvoeren.
- Is een persoonlijk apparaat of een Windows phone, moet u toevoegen van uw werk of school account tooWindows 



#### <a name="azure-ad-join-on-windows-10"></a>Azure AD Join op Windows 10

Hallo stappen toojoin uw apparaat tooAzure AD zijn gekoppeld Hallo-versie van Windows 10 u erop worden uitgevoerd. toodetermine hello versie van het besturingssysteem Windows 10 uitvoeren Hallo **winver** opdracht: 

![Windows-versie](./media/active-directory-conditional-access-device-remediation/03.png )


**Windows 10 Jubileumupdate (versie 1607)**

1. Open Hallo **instellingen** app.
2. Klik op **Accounts** > **Toegang via werk of school**.
3. Klik op **Verbinden**.
4. Klik op **deelnemen aan dit apparaat tooAzure AD**.
5. Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.
6. Meld u af en meld u weer aan met uw werkaccount.
7. Probeer het opnieuw tooaccess Hallo-toepassing.

**Windows 10-update van november 2015 (versie 1511):**

1. Open Hallo **instellingen** app.
2. Klik op **Systeem** > **Info**.
3. Klik op **Lid worden van Azure AD**.
4. Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.
5. Meld u af en meld u weer aan met uw werkaccount (uw Azure AD-account).
6. Probeer het opnieuw tooaccess Hallo-toepassing.


#### <a name="workplace-join-on-windows-81"></a>Workplace Join op Windows 8.1

Als uw apparaat geen lid van een domein is- en Windows 8.1, toodo wordt uitgevoerd een werkplek koppelen en in Microsoft Intune inschrijven, Hallo volgende stappen:

1. Open **Pc-instellingen**.
2. Klik op **Netwerk** > **Werkplek**.
3. Klik op **Deelnemen**.
4. Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.
5. Klik op **Inschakelen**.
6. Probeer het opnieuw tooaccess Hallo-toepassing.



#### <a name="add-your-work-or-school-account-toowindows"></a>Toevoegen van uw werk of school account tooWindows 


**Windows 10 Jubileumupdate (versie 1607)**

1. Open Hallo **instellingen** app.
2. Klik op **Accounts** > **Toegang via werk of school**.
3. Klik op **Verbinden**.
4. Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.
5. Probeer het opnieuw tooaccess Hallo-toepassing.


**Windows 10-update van november 2015 (versie 1511):**

1. Open Hallo **instellingen** app.
2. Klik op **Accounts** > **Uw accounts**.
3. Klik op **Werk- of schoolaccount toevoegen**.
4. Tooyour organisatie verifiëren, bieden meervoudige verificatie als u wordt gevraagd en volg Hallo-stappen die worden weergegeven.
5. Probeer het opnieuw tooaccess Hallo-toepassing.





## <a name="next-steps"></a>Volgende stappen
[Voorwaardelijke toegang van Azure Active Directory](active-directory-conditional-access.md)


---
title: aaaAzure certificaat gebaseerde verificatie van Active Directory voor iOS | Microsoft Docs
description: Meer informatie over Hallo ondersteund scenario's en het Hallo-vereisten voor het configureren van verificatie op basis van certificaten in oplossingen met iOS-apparaten
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>Azure Active Directory gebaseerde verificatie op iOS

Certificaat gebaseerde verificatie (CBA) kunt u toobe geverifieerd door Azure Active Directory met een clientcertificaat op een Windows-, Android of iOS-apparaat verbinding te maken met uw Exchange online-account in: 

* Mobiele Office-toepassingen zoals Microsoft Outlook en Microsoft Word   
* Exchange ActiveSync (EAS)-clients 

Configuratie van deze functie wordt voorkomen dat Hallo nodig tooenter een gebruikersnaam en wachtwoord combinatie in bepaalde e-mail en Microsoft Office-toepassingen op uw mobiele apparaat. 

Dit onderwerp vindt u Hallo vereisten en Hallo ondersteund scenario's voor het configureren van CBA op een apparaat iOS(Android) voor gebruikers van tenants in Office 365 Enterprise, Business, Education, US Government, China en Duitsland plant.

Deze functie is beschikbaar in preview in Office 365 US Government verdediging en Federal plannen.




## <a name="office-mobile-applications-support"></a>Ondersteuning voor mobiele Office-toepassingen

| Apps | Ondersteuning |
| --- | --- |
| Azure Information Protection-app |![Selecteren][1] |
| Microsoft Teams |![Selecteren][1] |
| OneNote |![Selecteren][1] |
| OneDrive |![Selecteren][1] |
| Outlook |![Selecteren][1] |
| Mobiele apps van Power BI |![Selecteren][1] |
| Skype voor bedrijven |![Selecteren][1] |
| Word / Excel / PowerPoint |![Selecteren][1] |
| Yammer |![Selecteren][1] |


## <a name="requirements"></a>Vereisten 

Hallo versie van besturingssysteem van het apparaat moet iOS 9 en hoger 

Een federation-server moet worden geconfigureerd.  

Microsoft Authenticator is vereist voor de Office-toepassingen op iOS.  

Voor Azure Active Directory toorevoke een clientcertificaat bevatten Hallo AD FS-token Hallo claims te volgen:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  (serienummer van het clientcertificaat Hallo Hallo) 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  (Hallo tekenreeks voor de verlener van het clientcertificaat Hallo Hallo) 

Azure Active Directory toegevoegd deze claimtoken voor het vernieuwen van toohello als ze beschikbaar in AD FS-token van het hello (of andere SAML-token zijn). Wanneer het vernieuwingstoken Hallo toobe gevalideerd moet, is deze informatie gebruikte toocheck Hallo intrekken. 

Als een best practice moet u Hallo ADFS foutpagina's bijwerken met de volgende Hallo:

* Hallo vereiste voor het installeren van Microsoft Authenticator Hallo op iOS
* Instructies voor het tooget een gebruikerscertificaat. 

Zie voor meer informatie [Hallo Sign in AD FS's aanpassen](https://technet.microsoft.com/library/dn280950.aspx).

Sommige Office-apps (met moderne verificatie is ingeschakeld) verzenden '*prompt = aanmelding*' tooAzure AD in de aanvraag. Standaard Azure AD zet dit in Hallo aanvraag tooADFS te '*wauth = usernamepassworduri*' (vraagt ADFS toodo U/P auth) en '*wfresh = 0*' (vraagt ADFS tooignore SSO-status en voer een nieuwe verificatie) . Als u wilt dat tooenable op certificaten gebaseerde verificatie voor deze apps, moet u toomodify Hallo standaardgedrag Azure AD. NET set Hallo '*PromptLoginBehavior*' in de federatieve domeininstellingen te '*uitgeschakelde*'. U kunt Hallo [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform deze taak:

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Ondersteuning voor Exchange ActiveSync-clients
In iOS 9 of hoger, wordt Hallo systeemeigen iOS-e-mailclient ondersteund. Voor alle andere toepassingen Exchange ActiveSync toodetermine als deze functie wordt ondersteund, contact op met de ontwikkelaar van uw toepassing.  


## <a name="next-steps"></a>Volgende stappen

Als u tooconfigure certificaat gebaseerde verificatie in uw omgeving wilt, Zie [aan de slag met verificatie op basis van certificaten op Android](active-directory-certificate-based-authentication-get-started.md) voor instructies.


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png

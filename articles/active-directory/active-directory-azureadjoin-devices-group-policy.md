---
title: aaaConnect domeinapparaten tooAzure AD voor Windows 10 optreedt | Microsoft Docs
description: Legt uit hoe beheerders bedrijfsnetwerk Groepsbeleid tooenable apparaten toobe toohello domein kunnen configureren.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a>Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring
Domeinlidmaatschap is Hallo traditionele manier organisaties hebben verbonden apparaten voor werk voor Hallo afgelopen 15 jaar en meer. Deze gebruikers toosign tootheir apparaten ingeschakeld met behulp van hun werk Windows Server Active Directory (Active Directory) of schoolaccounts en toegestane IT toofully deze apparaten te beheren. Organisaties zijn gewoonlijk afhankelijk van de methoden tooprovision apparaten toousers imaging en System Center Configuration Manager (SCCM) of Groepsbeleid toomanage wordt meestal gebruikt ze.


Aan domein toevoegen in Windows 10 biedt Hallo volgende voordelen nadat u verbinding maakt met apparaten tooAzure Active Directory (Azure AD):

* Eenmalige aanmelding (SSO) tooAzure AD bronnen vanaf elke locatie
* Toohello enterprise, Windows Store openen met behulp van werk of school accounts (Er is geen Microsoft-account vereist)
* Enterprise-compatibele zwervende gebruikersinstellingen op apparaten met werk of school accounts (Er is geen Microsoft-account vereist)
* Sterke verificatie en handige aanmelden voor werk of school accounts met Windows Hello voor bedrijven en Windows Hello
* Mogelijkheid toorestrict toegang alleen toodevices die voldoen aan de organisatie-instellingen voor Groepsbeleid

## <a name="prerequisites"></a>Vereisten
Aan domein toevoegen blijft toobe nuttig. Echter tooget hello Azure AD voordelen van eenmalige aanmelding, zwervende instellingen met werk of schoolaccounts, en toegang tot de tooWindows opgeslagen met werk of school accounts, moet u hello te volgen:

* Azure AD-abonnement
* Azure AD Connect tooextend Hallo lokale directory tooAzure AD
* Beleid dat is ingesteld tooconnect domeinapparaten tooAzure AD
* Windows 10-build (build 10551 of nieuwer) voor apparaten

tooenable Windows Hello voor bedrijven en Windows Hello, moet u ook de volgende Hallo:

- **Openbare-sleutelinfrastructuur (PKI)** voor de gebruiker certificaten uitgifte.

- **System Center Configuration Manager Current Branch** -u moet tooinstall versie 1606 of hoger.  
Zie voor meer informatie: 
    - [Documentatie voor System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [System Center Configuration Manager-teamblog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Windows Hello voor bedrijven-instellingen in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

U kunt doen als een implementatievereiste van alternatieve toohello PKI Hallo volgende:

* Enkele domeincontrollers met Windows Server 2016 Active Directory Domain Services hebben.

tooenable voorwaardelijke toegang, kunt u instellingen voor Groepsbeleid waarmee toegang tot apparaten die lid zijn van toodomain met geen extra implementaties. toomanage toegangsbeheer op basis van naleving van Hallo-apparaat, moet u de volgende Hallo:

* System Center Configuration Manager Current Branch (1606 of hoger) voor Windows Hello voor bedrijven-scenario 's

## <a name="deployment-instructions"></a>Implementatie-instructies

toodeploy, volg Hallo de stappen die worden vermeld in [hoe tooconfigure automatische registratie van Windows-domein apparaten met Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Volgende stap
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)


---
title: Domein apparaten verbinden met Azure AD voor Windows 10 optreedt | Microsoft Docs
description: Legt uit hoe beheerders Groepsbeleid zodat apparaten aan het domein met het bedrijfsnetwerk kunnen configureren.
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a>Connect domain-joined devices to Azure AD for Windows 10 experiences (Engelstalig)
Aan domein toevoegen is dat de traditionele manier organisaties hebben verbonden apparaten voor werk voor de afgelopen 15 jaar en meer. Gebruikers kunnen aanmelden met hun apparaten via hun werk Windows Server Active Directory (Active Directory)- of schoolaccounts ingeschakeld en toegestaan IT volledig deze apparaten te beheren. Organisaties zijn gewoonlijk afhankelijk van de installatiekopieën methoden voor het inrichten van apparaten aan gebruikers en meestal System Center Configuration Manager (SCCM) of Groepsbeleid gebruiken om deze te beheren.


Aan domein toevoegen in Windows 10 biedt de volgende voordelen nadat u apparaten op Azure Active Directory (Azure AD aansluit):

* Eenmalige aanmelding (SSO) naar Azure AD-resources vanaf elke locatie
* Toegang tot de Windows Store-onderneming met werk of school accounts (Er is geen Microsoft-account vereist)
* Enterprise-compatibele zwervende gebruikersinstellingen op apparaten met werk of school accounts (Er is geen Microsoft-account vereist)
* Sterke verificatie en handige aanmelden voor werk of school accounts met Windows Hello voor bedrijven en Windows Hello
* Mogelijkheid toegang te beperken tot apparaten die aan de organisatie-instellingen voor Groepsbeleid voldoen

## <a name="prerequisites"></a>Vereisten
Aan domein toevoegen blijft nuttig zijn. Echter te krijgen van de Azure AD-voordelen van eenmalige aanmelding, zwervende instellingen met werk of schoolaccounts en toegang tot Windows Store met werk of school-accounts, moet u het volgende:

* Azure AD-abonnement
* Azure AD Connect uit te breiden de on-premises directory naar Azure AD
* Beleid dat is ingesteld op het domein apparaten verbinden met Azure AD
* Windows 10-build (build 10551 of nieuwer) voor apparaten

Schakel Windows Hello voor bedrijven en Windows Hello door u ook het volgende nodig:

- **Openbare-sleutelinfrastructuur (PKI)** voor de gebruiker certificaten uitgifte.

- **System Center Configuration Manager Current Branch** -u moet versie 1606 of hoger installeren.  
Zie voor meer informatie: 
    - [Documentatie voor System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx)
    - [System Center Configuration Manager-teamblog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [Windows Hello voor bedrijven-instellingen in System Center Configuration Manager](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

Als alternatief voor de vereiste PKI-implementatie kunt u het volgende doen:

* Enkele domeincontrollers met Windows Server 2016 Active Directory Domain Services hebben.

U kunt instellingen voor Groepsbeleid die toegang tot de domein-apparaten met geen extra implementaties geven maken voor het inschakelen van voorwaardelijke toegang. Voor het beheren van toegangsbeheer op basis van naleving van het apparaat, moet u het volgende:

* System Center Configuration Manager Current Branch (1606 of hoger) voor Windows Hello voor bedrijven-scenario 's

## <a name="deployment-instructions"></a>Implementatie-instructies

Volg de stappen in voor het implementeren [automatische registratie van Windows-domein-apparaten met Azure Active Directory configureren](active-directory-conditional-access-automatic-device-registration-setup.md)

## <a name="next-step"></a>Volgende stap
* [Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)
* [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)


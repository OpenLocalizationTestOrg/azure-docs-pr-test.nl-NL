---
title: Instellen van een nieuw apparaat met Azure AD tijdens de installatie | Microsoft Docs
description: Dit onderwerp wordt beschreven hoe gebruikers kunnen Azure AD Join instellen tijdens hun first-run experience.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 06a149f7-4aa1-4fb9-a8ec-ac2633b031fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 4367f453ef7c794653dfa9f305b137a168e0d207
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Instellen van een nieuw apparaat met Azure AD tijdens de installatie
In Windows 10 gebruikers kunnen hun apparaten aanmelden bij Azure Active Directory (Azure AD) in de eerste sessie (FRX). Hierdoor kunnen organisaties krimp apparaten aan hun werknemers of studenten distribueren, of laten kiezen hun eigen apparaten (CYOD).
Als Windows 10 Professional of Windows 10 Enterprise-editie is geïnstalleerd op een apparaat, de ervaring wordt standaard ingesteld op het installatieproces voor apparaten in Bedrijfseigendom.

## <a name="to-join-a-device-to-azure-ad"></a>Een apparaat koppelen aan Azure AD
1. Wanneer u het nieuwe apparaat inschakelen en het installatieproces start, ziet u de **gereed ophalen** bericht. Volg de aanwijzingen voor het instellen van uw apparaat.
2. Start op het aanpassen van uw regio en taal. Accepteer de licentievoorwaarden voor Microsoft-Software.
   ![Aanpassen voor uw regio](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Selecteer het netwerk die u gebruiken wilt om verbinding te maken met Internet.
4. Selecteer of u een persoonlijk apparaat of een apparaat in Bedrijfseigendom. Als het eigendom van het bedrijf, klikt u op **dit apparaat is van mijn organisatie**. Hiermee start u de Azure AD Join-ervaring. Hier volgt een scherm die wordt weergegeven als u Windows 10 Professional.
   <center>
   ![Wie is eigenaar van dit scherm PC](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Geef de referenties die aan u zijn geleverd door uw organisatie.
   <center>
   ![Aanmeldingsscherm](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Nadat u uw gebruikersnaam hebt ingevoerd, wordt een overeenkomende tenant bevindt zich in Azure AD. Als u zich in een federatieve domein, wordt u omgeleid naar uw lokale Secure Token Service (STS) server--bijvoorbeeld Active Directory Federation Services (AD FS).
7. Als u een gebruiker in een niet-gefedereerde domein, Geef uw referenties rechtstreeks op de Azure AD gehost pagina. Als de huisstijl van uw bedrijf is geconfigureerd, wordt u ook Zie logo van uw organisatie en tekst ondersteunen.
8. U wordt gevraagd om een challenge multi-factor authentication-server. Deze uitdaging kan worden geconfigureerd door een IT-beheerder.
9. Azure AD wordt gecontroleerd of deze gebruiker/apparaat is vereist voor inschrijving in beheer van mobiele apparaten.
10. Windows het apparaat in de map van de organisatie wordt geregistreerd in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.
11. Als u een beheerde gebruiker bent, gaat u verder Windows naar het bureaublad door het proces voor automatische aanmelding.
12. Als u een federatieve gebruiker bent, wordt u omgeleid naar het Windows-aanmeldingsscherm uw referenties in te voeren.

> [!NOTE]
> Lidmaatschap van een lokale Windows Server Active Directory-domein in de Windows-out-of-box experience wordt niet ondersteund. Dus als u van plan bent om een computer toevoegen aan een domein, moet u de koppeling **Windows instellen met een lokaal account** in plaats daarvan. U kunt vervolgens deelnemen aan het domein van de instellingen op uw computer als u eerder hebt uitgevoerd.
> 
> 

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 for the enterprise: Ways to use devices for work](active-directory-azureadjoin-windows10-devices-overview.md) (Windows 10 voor de onderneming: manieren om apparaten voor werk te gebruiken)
* [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-user-upgrade.md) (Cloudmogelijkheden uitbreiden naar Windows 10-apparaten met behulp van Azure Active Directory Join)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Connect domain-joined devices to Azure AD for Windows 10 experiences](active-directory-azureadjoin-devices-group-policy.md) (Apparaten die lid zijn van een domein verbinden met Azure AD voor Windows 10-ervaringen)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)


---
title: aaaSet van een nieuw apparaat met Azure AD tijdens de installatie | Microsoft Docs
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
ms.openlocfilehash: 6afce4be7f084f1956a6f9dbddaa8def0605956d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-new-device-with-azure-ad-during-setup"></a>Instellen van een nieuw apparaat met Azure AD tijdens de installatie
In Windows 10, kunnen gebruikers hun apparaten tooAzure Active Directory (Azure AD) toevoegen in de eerste uitvoering van Windows hello (FRX). Dit kan organisaties toodistribute krimp apparaten tootheir werknemers en studenten of kan ze hun eigen apparaten (CYOD) te kiezen.
Als Windows 10 Professional of Windows 10 Enterprise-editie is geïnstalleerd op een apparaat, ervaren Hallo standaardwaarden toohello setup-proces voor apparaten in Bedrijfseigendom.

## <a name="toojoin-a-device-tooazure-ad"></a>een apparaat tooAzure AD toojoin
1. Wanneer u het nieuwe apparaat inschakelen en Hallo-installatieproces start, ziet u Hallo **gereed ophalen** bericht. Ga als volgt Hallo prompts tooset van uw apparaat.
2. Start op het aanpassen van uw regio en taal. Accepteer Hallo Microsoft-softwarelicentievoorwaarden.
   ![Aanpassen voor uw regio](./media/active-directory-azureadjoin/active-directory-azureadjoin-customize-region.png)
3. Selecteer Hallo netwerk gewenste toouse toohello Internet verbinding te maken.
4. Selecteer of u een persoonlijk apparaat of een apparaat in Bedrijfseigendom. Als het eigendom van het bedrijf, klikt u op **dit apparaat is van de organisatie toomy**. Hiermee start u hello Azure AD Join-ervaring. Hier volgt een scherm die wordt weergegeven als u Windows 10 Professional.
   <center>
   ![Wie is eigenaar van dit scherm PC](./media/active-directory-azureadjoin/active-directory-azureadjoin-who-owns-pc.png)
5. Geef referenties op Hallo die tooyou zijn geleverd door uw organisatie.
   <center>
   ![Aanmeldingsscherm](./media/active-directory-azureadjoin/active-directory-azureadjoin-sign-in.png)
6. Nadat u uw gebruikersnaam hebt ingevoerd, wordt een overeenkomende tenant bevindt zich in Azure AD. Als u zich in een federatieve domein, wordt u omgeleid tooyour lokale Secure Token Service (STS) server--bijvoorbeeld Active Directory Federation Services (AD FS) zijn.
7. Als u een gebruiker in een niet-gefedereerde domein, Geef uw referenties rechtstreeks op Hallo Azure AD gehost pagina. Als de huisstijl van uw bedrijf is geconfigureerd, wordt u ook Zie logo van uw organisatie en tekst ondersteunen.
8. U wordt gevraagd om een challenge multi-factor authentication-server. Deze uitdaging kan worden geconfigureerd door een IT-beheerder.
9. Azure AD wordt gecontroleerd of deze gebruiker/apparaat is vereist voor inschrijving in beheer van mobiele apparaten.
10. Windows hello apparaat geregistreerd bij Hallo organisatiemap in Azure AD en beheer van mobiele apparaten inschrijft, indien van toepassing.
11. Als u een beheerde gebruiker bent, gaat u in Windows desktop toohello via automatische Hallo aanmelden proces.
12. Als u een federatieve gebruiker bent, wordt u omgeleid toohello Windows aanmelden scherm tooenter uw referenties.

> [!NOTE]
> Lidmaatschap van een lokale Windows Server Active Directory-domein in Windows hello wordt out-of-box experience niet ondersteund. Als u een domein computer tooa toojoin plant, moet u daarom Hallo koppeling selecteren **Windows instellen met een lokaal account** in plaats daarvan. Vervolgens kunt u Hallo domein uit Hallo-instellingen op uw computer koppelen als u eerder hebt uitgevoerd.
> 
> 

## <a name="additional-information"></a>Aanvullende informatie
* [Windows 10 voor Hallo ondernemingen: manieren toouse apparaten for work.](active-directory-azureadjoin-windows10-devices-overview.md)
* [Cloud-mogelijkheden tooWindows 10-apparaten via Azure Active Directory Join uitbreiden](active-directory-azureadjoin-user-upgrade.md)
* [Identiteiten zonder wachtwoorden via Microsoft Passport verifiëren](active-directory-azureadjoin-passport.md)
* [Learn about usage scenarios for Azure AD Join](active-directory-azureadjoin-deployment-aadjoindirect.md) (Gebruiksscenario’s voor Azure AD Join)
* [Verbinding maken met domein apparaten tooAzure AD voor Windows 10-ervaring](active-directory-azureadjoin-devices-group-policy.md)
* [Azure AD Join instellen](active-directory-azureadjoin-setup.md)


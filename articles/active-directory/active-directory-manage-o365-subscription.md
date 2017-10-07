---
title: aaaManage hello directory voor uw Office 365-abonnement in Azure | Microsoft Docs
description: Een Office 365-abonnement directory met Azure Active Directory en Hallo klassieke Azure-portal beheren
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 746987b7-2dfd-4b35-819d-37c1b65c5c81
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
ms.openlocfilehash: 4faf9936d7e94b85356a18adfcf3d2a48e5b025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-directory-for-your-office-365-subscription-in-azure"></a>Hallo-directory voor uw Office 365-abonnement in Azure beheren
Dit artikel wordt beschreven hoe toomanage een map die is gemaakt voor Office 365-abonnement, met behulp van Hallo klassieke Azure-portal. U moet Hallo servicebeheerder of medebeheerder van een Azure-abonnement toosign in toohello klassieke Azure-portal. Als u nog geen Azure-abonnement hebt, kunt u zich vandaag aanmelden voor een [gratis proefperiode van 30 dagen](https://azure.microsoft.com/trial/get-started-active-directory/) en via deze koppeling binnen vijf minuten uw eerste cloudoplossing implementeren. Worden ervoor toouse Hallo werk- of schoolaccount toosign in tooOffice 365 te gebruiken.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel.

Nadat u hello Azure-abonnement hebt voltooid, kunt u toohello klassieke Azure-portal aanmelden en toegang tot Azure-services. Klik op de Active Directory-extensie Hallo toomanage Hallo dezelfde directory waarmee uw Office 365-gebruikers worden geverifieerd.

Als er al een Azure-abonnement, is Hallo proces toomanage een extra directory ook eenvoudig. Jaap Kleefstra heeft bijvoorbeeld een Office 365-abonnement voor Contoso.com. Hij heeft ook een Azure-abonnement waarbij hij zich heeft geregistreerd met zijn Microsoft-account, msmith@hotmail.com. In dit geval beheert hij twee directory's.

| Abonnement | Office 365 | Azure |
| --- | --- | --- |
|   Weergavenaam |Contoso |De standaarddirectory voor Azure Active Directory (Azure AD) |
|   Domeinnaam |contoso.com |jkleefstrahotmail.onmicrosoft.com |

Hij toomanage Hallo gebruikers-id's in de directory Contoso Hallo terwijl hij is tooAzure met diens Microsoft-account aangemeld zodat hij Azure AD-functies zoals multi-factor authentication kunt inschakelen. Hallo volgende diagram kunt tooillustrate Hallo proces.

![Diagram van twee onafhankelijke directory's toomanage](./media/active-directory-manage-o365-subscription/AAD_O365_03.png)

In dit geval zijn Hallo twee directory's onafhankelijk van elkaar.

## <a name="toomanage-two-independent-directories"></a>toomanage twee onafhankelijke directory 's
In volgorde van Michael Smith toomanage beide directory's terwijl hij is aangemeld met tooAzure als msmith@hotmail.com, moet hij Hallo stappen uitvoeren:

> [!NOTE]
> Deze stappen kunnen alleen worden uitgevoerd wanneer een gebruiker is aangemeld met een Microsoft-account. Als het Hallo-gebruiker is aangemeld met een account voor werk of school, Hallo u optie te**bestaande directory gebruiken** is niet beschikbaar. Een werk- of schoolaccount kan alleen met de basisdirectory (dat wil zeggen, Hallo directory waar hello werk-of schoolaccount is opgeslagen en die Hallo bedrijf of school eigenaar is van) worden geverifieerd.
>
>

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) als msmith@hotmail.com.
2. Klik achtereenvolgens op **Nieuw** > **App Services** > **Active Directory** > **Directory** > **Aangepast maken**.
3. Klik op bestaande directory en selecteer hello gebruiken **ik ben klaar toobe afgemeld** selectievakje.
4. Meld u aan toohello klassieke Azure-portal als globale beheerder van Contoso.onmicrosoft.com (bijvoorbeeld msmith@contoso.com).
5. Als u wordt gevraagd te**gebruik Hallo Contoso-directory met Azure?**, klikt u op **doorgaan**.
6. Klik op **Nu afmelden**.
7. Meld u aan toohello klassieke Azure-portal als msmith@hotmail.com. Hallo Contoso-directory en Hallo standaarddirectory worden weergegeven in Hallo Active Directory-extensie.

Na het voltooien van deze stappen msmith@hotmail.com een globale beheerder in Hallo Contoso-directory.

## <a name="tooadminister-resources-as-hello-global-admin"></a>tooadminister resources als globale beheerder Hallo
Nu gaan we ervan uit dat Dena vloet beheren van websites en databaseresources die zijn gekoppeld aan Azure-abonnement voor Hallo msmith@hotmail.com. Voordat ze dit doen kan, moet Michael Smith toocomplete volgende aanvullende stappen uit:

1. Meld u aan toohello [klassieke Azure-portal](https://manage.windowsazure.com) Hallo Service Administrator-account gebruiken voor hello Azure-abonnement (in dit voorbeeld msmith@hotmail.com).
2. Hallo abonnement toohello Contoso-directory overdragen: klik op **instellingen** > **abonnementen** > Hallo abonnement selecteren > **Directory bewerken** > Selecteer **Contoso (Contoso.com)**. Als onderdeel van Hallo overdracht, werk of school worden accounts die medebeheerder van Hallo abonnement zijn verwijderd.
3. Dena Vloet toevoegen als medebeheerder van Hallo abonnement: klik op **instellingen** > **beheerders** > Selecteer Hallo abonnement > **toevoegen** > type **JohnDoe@Contoso.com**.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over de relatie tussen abonnementen en Directory Hallo [hoe een abonnement is gekoppeld aan een map](active-directory-how-subscriptions-associated-directory.md).

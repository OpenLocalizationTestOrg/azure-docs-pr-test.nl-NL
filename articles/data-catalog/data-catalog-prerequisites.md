---
title: vereisten voor aaaAzure Data Catalog | Microsoft Docs
description: Meer informatie over Hallo vereisten moet u de slag met Azure Data Catalog tooget.
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: ef497a54-dc4d-4820-b5bf-c361b64b964d
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 0c8e768e5846c61b542b746d7ad80121725a9ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-prerequisites"></a>Vereisten voor Azure Data Catalog

U moet tootake antwoord leest voordat u Azure Data Catalog kunt instellen. Maak je geen zorgen, dit proces is niet lang duren.

## <a name="azure-subscription"></a>Azure-abonnement
tooset van Data Catalog, moet u de eigenaar van het Hallo of mede-eigenaar van een Azure-abonnement.

Azure-abonnementen kunnen u toegang tot toocloud service bronnen zoals Data Catalog indelen. Abonnementen kunnen u ook bepalen hoe Resourcegebruik is gerapporteerd, kosten in rekening gebracht en betaald. Elk abonnement kan een afzonderlijke facturerings- en -instellingen hebben, zodat u kunt abonnementen en schema's die per afdeling, project en regionaal kantoor verschillen. Elke cloudservice tooa abonnement behoort en moet u een abonnement toohave voordat u Data Catalog instellen. toolearn meer, Zie [beheren van accounts, abonnementen en beheerdersrollen](../active-directory/active-directory-assign-admin-roles.md).

## <a name="azure-active-directory"></a>Azure Active Directory
tooset van Data Catalog, als u bent aangemeld met een gebruikersaccount van Azure Active Directory (Azure AD).

Azure AD biedt een eenvoudige manier voor uw zakelijke toomanage identiteits- en toegangsbeheer, zowel in Hallo cloud en on-premises. Gebruikers kunnen één werk- of schoolaccount gebruiken voor eenmalige aanmelding tooany cloud en lokale webtoepassing. Data Catalog gebruikt Azure AD tooauthenticate aanmelden. toolearn meer, Zie [wat is Azure Active Directory?](../active-directory/active-directory-whatis.md).

> [!NOTE]
> Met behulp van Hallo [Azure-portal](http://portal.azure.com/), kunt u zich aanmelden met een persoonlijk Microsoft-account of een Azure Active Directory werk- of schoolaccount. tooset van Data Catalog via ofwel hello Azure portal of Hallo [Data Catalog-portal](http://www.azuredatacatalog.com), moet u zich aanmelden met een Azure Active Directory-account, niet een persoonlijk account.
>
>

## <a name="active-directory-policy-configuration"></a>Configuratie van Active Directory-beleid
U kunt een situatie tegenkomen wanneer u zich kunt aanmelden toohello Data Catalog-portal, maar wanneer u probeert toosign in hulpprogramma voor registratie van gegevensbronnen toohello, u ontvangt een foutmelding dat u niet aanmelden. Dit probleem kan gebeuren wanneer je op Hallo bedrijfsnetwerk of het optreden alleen wanneer u verbinding maakt vanaf externe Hallo-netwerk van bedrijf.

hulpprogramma voor registratie van gegevensbronnen Hallo gebruikt formulierverificatie toovalidate uw gebruikersreferenties op basis van Active Directory. toohelp die het aanmelden is gelukt, een Active Directory-beheerder moet formulierverificatie inschakelen in algemeen verificatiebeleid Hallo.

In het globale verificatiebeleid Hallo mag verificatiemethoden ingeschakeld afzonderlijk voor intranet en extranet-verbindingen, zoals wordt weergegeven in de volgende schermafbeelding Hallo. Aanmelden fouten optreden als formulierverificatie niet is ingeschakeld voor het Hallo-netwerk van waaruit u verbinding maakt.

 ![Het globale verificatiebeleid Active Directory](./media/data-catalog-prerequisites/global-auth-policy.png)

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie [Authenticatiebeleid configureren](https://technet.microsoft.com/library/dn486781.aspx).

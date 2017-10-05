---
title: Gebruikers toewijzen aan een aangepast domein in Azure Active Directory | Microsoft Docs
description: Klik hier voor meer informatie over het vullen van een aangepast domein in Azure Active Directory met een gebruikersaccount.
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a>Gebruikers toewijzen aan een aangepast domein
Nadat u uw aangepaste domein aan Azure Active Directory hebt toegevoegd, moet u de gebruikersaccounts voor dit domein toevoegen zodat u kunt beginnen met het verifiëren van deze.

> [!IMPORTANT]
> Microsoft raadt u aan Azure AD te beheren met het [Azure AD-beheercentrum](https://aad.portal.azure.com) in Azure Portal in plaats van de klassieke Azure portal waarnaar in dit artikel wordt verwezen. Voor informatie over het beheren van uw domeinnamen in de Azure AD-beheercentrum, Zie [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Gebruikers synchroniseren met een on-premises adreslijst
Als u hebt al een verbinding ingesteld tussen uw on-premises Active Directory en Azure Active Directory, kan de synchronisatie van de accounts invullen. Zie voor meer informatie over het synchroniseren van Azure Active Directory met uw lokale Active Directory [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-the-cloud"></a>Gebruikers toegevoegd en beheerd in de cloud
Het domein voor een bestaand gebruikersaccount wijzigen:

1. Open de klassieke Azure portal met een account dat is een globale beheerder of de beheerder van een gebruiker.
2. Open uw directory.
3. Selecteer de tab **Gebruikers**.
4. Selecteer de gebruiker in de lijst.
5. Het domein voor de gebruiker te wijzigen en selecteer vervolgens **opslaan**.

Dit kan ook worden gedaan met [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) of de [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Een aangepast domein selecteert bij het maken van een nieuwe gebruiker
1. Open de klassieke Azure portal met een account dat is een globale beheerder of de beheerder van een gebruiker.
2. Open uw directory.
3. Selecteer de tab **Gebruikers**.
4. Selecteer in de opdrachtbalk **toevoegen**.
5. Wanneer u de gebruikersnaam toevoegt, kiest u het aangepaste domein in de domeinlijst.
6. Selecteer **Opslaan**.

## <a name="next-steps"></a>Volgende stappen
* [Met behulp van aangepaste domeinnamen voor het vereenvoudigen van de aanmeldingservaring voor gebruikers](active-directory-add-domain.md)
* [Aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md)
* [Meer informatie over concepten met betrekking tot domeinbeheer in Azure AD](active-directory-add-domain-concepts.md)


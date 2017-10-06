---
title: aaaAssign gebruikers tooa aangepast domein in Azure Active Directory | Microsoft Docs
description: Hoe toopopulate een aangepast domein in Azure Active Directory met een gebruikersaccount.
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
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Gebruikers tooa aangepast domein toewijzen
Nadat u uw aangepaste domein tooAzure Active Directory hebt toegevoegd, moet u de gebruikersaccounts Hallo voor dit domein toevoegen zodat u kunt beginnen met het verifiëren van deze.

> [!IMPORTANT]
> Microsoft raadt aan dat u Azure AD beheren met Hallo [Azure AD-beheercentrum](https://aad.portal.azure.com) in Hallo hello Azure-portal in plaats van de klassieke Azure-portal waarnaar wordt verwezen in dit artikel. Zie voor hoe toomanage uw in hello Azure AD-beheercentrum domeinnamen, [aangepaste domeinnamen in uw Azure Active Directory beheren](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Gebruikers synchroniseren met een on-premises adreslijst
Als u hebt al een verbinding ingesteld tussen uw on-premises Active Directory en Azure Active Directory, kan de synchronisatie Hallo accounts invullen. Voor meer informatie over hoe toosynchronize Azure Active Directory met uw lokale Active Directory, Zie [uw on-premises identiteiten integreren met Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Gebruikers toegevoegd en beheerd in de cloud Hallo
toochange hello domein voor een bestaand gebruikersaccount:

1. Open Hallo klassieke Azure-portal met een account dat is een globale beheerder of de beheerder van een gebruiker.
2. Open uw directory.
3. Selecteer Hallo **gebruikers** tabblad.
4. Hallo-gebruiker in Hallo lijst selecteren.
5. Hallo-domein voor Hallo gebruiker te wijzigen en selecteer vervolgens **opslaan**.

Dit kan ook worden gedaan met [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) of Hallo [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Een aangepast domein selecteert bij het maken van een nieuwe gebruiker
1. Open Hallo klassieke Azure-portal met een account dat is een globale beheerder of de beheerder van een gebruiker.
2. Open uw directory.
3. Selecteer Hallo **gebruikers** tabblad.
4. Selecteer in de opdrachtbalk Hallo **toevoegen**.
5. Wanneer u de naam van de gebruiker Hallo toevoegt, kiest u Hallo aangepast domein uit Hallo Domeinlijst.
6. Selecteer **Opslaan**.

## <a name="next-steps"></a>Volgende stappen
* [Met behulp van aangepast domein namen toosimplify hello aanmeldingservaring voor gebruikers](active-directory-add-domain.md)
* [Aangepaste domeinnamen beheren](active-directory-add-manage-domain-names.md)
* [Meer informatie over concepten met betrekking tot domeinbeheer in Azure AD](active-directory-add-domain-concepts.md)


---
title: 'Azure Active Directory Domain Services: Kerberos-beperkte delegatie inschakelen | Microsoft Docs'
description: Kerberos-beperkte overdracht op beheerde domeinen voor Azure Active Directory Domain Services inschakelen
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Kerberos-beperkte delegatie (KCD) configureren op een beheerd domein
Veel toepassingen moeten tooaccess resources in de context van de gebruiker Hallo Hallo. Active Directory ondersteunt een mechanisme voor Kerberos-overdracht, waardoor deze gebruiksvoorbeeld. U kunt bovendien delegering beperken zodat alleen bepaalde resources in de context van de gebruiker Hallo Hallo toegankelijk zijn. Azure AD Domain Services beheerde domeinen zijn anders dan traditionele Active Directory-domeinen, omdat ze veiliger zijn vergrendeld.

Dit artikel laat zien hoe tooconfigure kerberos-beperkte overdracht op een beheerd domein van Azure AD Domain Services.

## <a name="kerberos-constrained-delegation-kcd"></a>Kerberos-beperkte delegatie (KCD)
Kerberos-overdracht kunt een account tooimpersonate tooaccess principal (zoals een gebruiker) van een andere beveiligingsinformatie. U kunt een webtoepassing die toegang heeft tot een back-end-web-API in Hallo context van een gebruiker. In dit voorbeeld hello webtoepassing (uitgevoerd in de context van een serviceaccount of een computer/computeraccount Hallo) Hallo gebruiker imiteert bij toegang tot Hallo bron (back-end web-API). Kerberos-overdracht is onveilig omdat Hallo resources Hallo imiteren account toegang in de context van de gebruiker Hallo Hallo tot niet wordt beperkt.

Kerberos-beperkte delegatie (KCD) beperkt Hallo services-bronnen toowhich Hallo opgegeven server op Hallo namens de gebruiker kan fungeren. Traditionele KCD domein administrator-bevoegdheden tooconfigure een domeinaccount vereist voor een service en het Hallo-account tooa één domein beperkt.

Traditionele KCD heeft ook een aantal aspecten die zijn gekoppeld. In eerdere besturingssystemen waarin domeinbeheerder Hallo Hallo-service hebt geconfigureerd, had Hallo servicebeheerder geen handige manier tooknow welke front-end-services overgedragen toohello bronservices die of zij eigenaar was. En elke front-endservice die kon worden overgedragen tooa bronservice vertegenwoordigd een potentiële aanvallen met zich mee. Als inbreuk is gemaakt op een server die een front-end-service wordt gehost, en het geconfigureerde toodelegate tooresource services was, kunnen ook Hallo bronservices gevaar.

> [!NOTE]
> Op een beheerd domein van Azure AD Domain Services er geen domeinadministratorrechten. Daarom **traditionele KCD kan niet worden geconfigureerd op een beheerd domein**. Gebruik KCD op basis van bronnen zoals beschreven in dit artikel. Dit mechanisme is ook veiliger.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Op basis van bronnen kerberos-beperkte overdracht
Hallo mogelijkheid tooconfigure beperkte delegering voor Hallo-service is in Windows Server 2012 R2 en Windows Server 2012 overgebracht van Hallo beheerder toohello service domeinbeheerder. Op deze manier kunt Hallo back-end-servicebeheerder toestaan of weigeren van de front-end-services. Dit model wordt ook wel **resources gebaseerde kerberos-beperkte overdracht**.

KCD op basis van een bron is geconfigureerd met behulp van PowerShell. U gebruikt Hallo Set-ADComputer of Set-ADUser cmdlets, afhankelijk van of Hallo imiteren account een computeraccount of de account-/ serviceaccount voor een gebruiker is.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>KCD op basis van bronnen voor een computeraccount configureren op een beheerd domein
Wordt ervan uitgegaan dat u hebt een web-app wordt uitgevoerd op de computer Hallo ' contoso100-webapp.contoso100.com'. Moet tooaccess Hallo resource (een web-API uit te voeren op ' contoso100-api.contoso100.com') in de context van domeingebruikers Hallo. Dit is hoe u resources gebaseerde KCD voor dit scenario zou ingesteld.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>KCD op basis van bronnen voor een gebruikersaccount configureren op een beheerd domein
Stel u hebt een web-app wordt uitgevoerd als een service-account 'appsvc' moet tooaccess Hallo resource (een web-API wordt uitgevoerd als een serviceaccount - 'backendsvc') in de context van domeingebruikers Hallo. Dit is hoe u resources gebaseerde KCD voor dit scenario zou ingesteld.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Gerelateerde inhoud
* [Azure AD Domain Services - handleiding aan de slag](active-directory-ds-getting-started.md)
* [Kerberos-beperkte overdracht overzicht](https://technet.microsoft.com/library/jj553400.aspx)

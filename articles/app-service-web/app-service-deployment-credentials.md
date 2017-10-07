---
title: aaaAzure referenties voor de implementatie van App Service | Microsoft Docs
description: Meer informatie over hoe toouse Hallo referenties voor Azure App Service-implementatie.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/05/2016
ms.author: dariagrigoriu
ms.openlocfilehash: d6f9f5cc1b62a17c42643266f4c9490f827c63f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-credentials-for-azure-app-service"></a>Referenties voor implementatie configureren voor Azure App Service
[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) ondersteunt twee soorten referenties voor [lokale Git-implementatie](app-service-deploy-local-git.md) en [FTP-/ S implementatie](app-service-deploy-ftp.md). Deze zijn niet hetzelfde als uw Azure Active Directory-referenties Hallo.

* **Beveiliging op gebruikersniveau referenties**: één set met referenties voor Hallo volledige Azure-account. Gebruikte toodeploy tooApp Service kan zijn voor elke app in een abonnement dat Azure-account Hallo machtiging tooaccess heeft. Dit zijn Hallo referenties standaardset die u configureert in **App Services** > **&lt;app_naam >** > **implementatiereferenties**. Dit is ook Hallo standaardset die wordt opgehaald in Hallo portal GUI (zoals Hallo **overzicht** en **eigenschappen** van uw app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources)).

    > [!NOTE]
    > Wanneer u toegang tot tooAzure bronnen via op rollen gebaseerd toegangsbeheer (RBAC) of co-beheerder machtigingen delegeren, kunt elke Azure-gebruiker die toegang tooan app ontvangt stelt zijn/haar persoonlijke op gebruikersniveau referenties gebruiken totdat de toegang is ingetrokken. Deze referenties voor implementatie mag niet worden gedeeld met andere Azure-gebruikers.
    >
    >

* **App-niveau referenties**: één set met referenties voor elke app. Het kan gebruikte toodeploy toothat app alleen zijn. Hallo-referenties publiceren voor elke app bij het maken van de app automatisch wordt gegenereerd en is gevonden in het Hallo-app profiel. U kunt geen Hallo referenties handmatig configureren, maar u ze op elk gewenst moment voor een app kunt herstellen.

    > [!NOTE]
    > In de volgorde toogive iemand toegangsreferenties toothese via rollen gebaseerd toegangsbeheer (RBAC), moet u toomake ze Inzender of hoger op Hallo Web-App. Lezers zijn niet toegestaan voor toopublish en daarom geen toegang tot deze referenties.
    >
    >

## <a name="userscope"></a>Instellen en de referenties op gebruikersniveau resetten

U kunt uw referenties op gebruikersniveau configureren in elke app [resourceblade](../azure-resource-manager/resource-group-portal.md#manage-resources). Ongeacht in welke app configureert u deze referenties, maar apps tooall geldt voor alle abonnementen in uw Azure-account. 

tooconfigure uw referenties op gebruikersniveau:

1. In Hallo [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **implementatiereferenties**.

    > [!NOTE]
    > U moet ten minste één app in Hallo-portal hebben voordat u toegang hebt tot blade Hallo implementatie-referenties. Bij Hallo [Azure CLI](app-service-web-app-azure-resource-manager-xplat-cli.md), kunt u de referenties op gebruikersniveau zonder een bestaande app configureren.

2. Configureer Hallo-gebruikersnaam en wachtwoord en klik vervolgens op **opslaan**.

    ![](./media/app-service-deployment-credentials/deployment_credentials_configure.png)

Als u de referenties voor uw implementatie hebt ingesteld, kunt u vinden Hallo *Git* gebruikersnaam van de implementatie in uw app **overzicht**,

![](./media/app-service-deployment-credentials/deployment_credentials_overview.png)

en en *FTP* gebruikersnaam van de implementatie in uw app **eigenschappen**.

![](./media/app-service-deployment-credentials/deployment_credentials_properties.png)

> [!NOTE]
> Uw wachtwoord op gebruikersniveau implementatie wordt niet door Azure worden weergegeven. Als u Hallo wachtwoord vergeet, kunt u het niet ophalen. U kunt echter uw referenties herstellen door Hallo stappen in deze sectie.
>
>  

## <a name="appscope"></a>Ophalen en app-niveau referenties opnieuw instellen
Voor elke app in App Service, de referenties van de app-niveau worden opgeslagen in Hallo publicatieprofiel XML.

tooget hello app-niveau referenties:

1. In Hallo [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **overzicht**.

2. Klik op **... Meer** > **Get publicatieprofiel**, en begint met het downloaden voor een. Bestand met publicatie-instellingen.

    ![](./media/app-service-deployment-credentials/publish_profile_get.png)

3. Open hello. Bestands- en Hallo zoeken met publicatie-instellingen `<publishProfile>` code met het kenmerk Hallo `publishMethod="FTP"`. Haal vervolgens, de `userName` en `password` kenmerken.
Dit zijn Hallo app-niveau referenties.

    ![](./media/app-service-deployment-credentials/publish_profile_editor.png)

    Vergelijkbare toohello op gebruikersniveau referenties, Hallo FTP implementatie gebruikersnaam is in de indeling van Hallo `<app_name>\<username>`, en Hallo Git-implementatie gebruikersnaam NET `<username>` zonder Hallo voorgaande `<app_name>\`.

tooreset hello app-niveau referenties:

1. In Hallo [Azure-portal](https://portal.azure.com), klik op App Service >  **&lt;any_app >** > **overzicht**.

2. Klik op **... Meer** > **Reset publicatieprofiel**. Klik op **Ja** tooconfirm Hallo opnieuw instellen.

    Hallo reset-actie wordt een eerder gedownloade ongeldig. Bestanden met publicatie-instellingen.

## <a name="next-steps"></a>Volgende stappen

Ontdek hoe u kunt toouse deze referenties toodeploy uw app uit [lokale Git](app-service-deploy-local-git.md) of met behulp van [FTP/S](app-service-deploy-ftp.md).

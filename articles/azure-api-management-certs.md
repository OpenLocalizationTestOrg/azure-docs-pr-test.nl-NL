---
title: een Azure-API-Beheercertificaat aaaUpload | Microsoft Docs
description: Meer informatie over hoe tooupload athe Management-API van het certificaat voor Hallo klassieke Azure-Portal.
services: cloud-services
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: 1b813833-39c8-46be-8666-fd0960cfbf04
ms.service: na
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: adegeo
ms.openlocfilehash: 8294d7131cfb01dba664bd4fd04b6fc22c1e93ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-an-azure-management-api-management-certificate"></a>Een Azure Management API Management-certificaat uploaden
Van beheercertificaten kunnen tooauthenticate met het klassieke implementatiemodel Hallo verstrekt door Azure. Veel programma's en hulpprogramma's (zoals Visual Studio of hello Azure SDK) gebruiken deze certificaten tooautomate configuratie en implementatie van verschillende Azure-services. 

> [!WARNING]
> Wees voorzichtig! Deze typen certificaten dat alle gebruikers worden geverifieerd met hen toomanage Hallo abonnement ze zijn gekoppeld.
>
>

Als u meer informatie over Azure-certificaten (zoals het maken een zelfondertekend certificaat), Zie [certificaten voor Azure Cloud Services-overzicht](cloud-services/cloud-services-certs-create.md#what-are-management-certificates).

U kunt ook [Azure Active Directory](https://azure.microsoft.com/en-us/services/active-directory/) tooauthenticate-clientcode voor automatisering doeleinden.

## <a name="upload-a-management-certificate"></a>Een management-certificaat uploaden
Zodra u hebt een beheercertificaat dat is gemaakt, (CER-bestand met alleen Hallo openbare sleutel) kunt u deze bij Hallo portal uploaden. Wanneer Hallo-certificaat beschikbaar in de portal hello is, kan iedereen met een overeenkomend certificaat (persoonlijke sleutel) verbinding maken via Hallo Management API en de toegang tot bronnen van Hallo voor abonnement Hallo die zijn gekoppeld.

1. Meld u bij toohello [Azure-portal](http://portal.azure.com).
2. Klik op **meer services** Hallo onder Azure service lijst Selecteer **abonnementen** in Hallo _algemene_ servicegroep.

    ![Abonnement-menu](./media/azure-api-management-certs/subscriptions_menu.png)

3. Zorg ervoor dat tooselect Hallo juiste abonnement dat u wilt dat tooassociate met Hallo certificaat.     
4. Nadat u het juiste abonnement Hallo hebt geselecteerd, drukt u op **beheercertificaten** in Hallo _instellingen_ groep.

    ![Instellingen](./media/azure-api-management-certs/mgmtcerts_menu.png)

5. Druk op Hallo **uploaden** knop.

    ![Op de pagina certificaten uploaden](./media/azure-api-management-certs/certificates_page.png)
6. Vul Hallo dialoogvenster informatie en druk op **uploaden**.

    ![Instellingen](./media/azure-api-management-certs/certificate_details.png)

## <a name="next-steps"></a>Volgende stappen
Nu u een beheercertificaat dat is gekoppeld aan een abonnement hebt, kunt u (nadat u hebt geïnstalleerd die overeenkomt met certificaat lokaal Hallo) programmatisch koppelen toohello [klassieke implementatiemodel REST-API](https://msdn.microsoft.com/library/azure/mt420159.aspx) en automatiseren Hallo verschillende Azure-resources die ook gekoppeld aan dat abonnement.

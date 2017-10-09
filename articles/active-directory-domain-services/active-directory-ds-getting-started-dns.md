---
title: 'Azure Active Directory Domain Services: Bijwerken DNS-instellingen voor virtuele Azure-netwerk Hallo | Microsoft Docs'
description: Aan de slag met Azure Active Directory Domain Services
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: d4f3e82c-6807-4690-b298-4eabad2b7927
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/27/2017
ms.author: maheshu
ms.openlocfilehash: e6eaff555cb9b7bb89ab7581d8de0b8cfc844529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-preview"></a>Azure Active Directory Domain Services (preview) inschakelen

## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Taak 4: DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk
In de Hallo voorgaande configuratietaken, hebt u Azure Active Directory Domain Services voor uw directory is ingeschakeld. de volgende taak Hallo is tooensure dat computers in het virtuele netwerk Hallo kunnen verbinding maken en gebruiken van deze services. In dit artikel leert bijwerken u Hallo DNS-serverinstellingen voor uw virtuele netwerk toopoint toohello twee IP-adressen waarop Azure Active Directory Domain Services beschikbaar op Hallo virtueel netwerk is.

tooupdate hello DNS-serverinstellingen voor Hallo virtuele netwerk waarin u Azure Active Directory Domain Services voltooid Hallo stappen hebt ingeschakeld:

1. Hallo **overzicht** tabblad bevat een reeks **configuratiestappen vereist** toobe uitgevoerd nadat u uw beheerde domein volledig is ingericht. Hallo eerste configuratiestap is **Update DNS-serverinstellingen voor het virtuele netwerk**.

    ![Domain Services: tabblad Overzicht nadat het domein volledig is ingericht](./media/getting-started/domain-services-provisioned-overview.png)

2. Wanneer uw domein volledig is ingericht, worden er twee IP-adressen weergegeven in deze tegel. Elk IP-adres vertegenwoordigt een domeincontroller voor uw beheerde domein.

3. toocopy hello eerste IP-adres tooclipboard adres, klikt u op Hallo kopie knop volgende tooit. Klik vervolgens op Hallo **configureren van DNS-servers** knop.

4. Hallo eerste IP-adres in Hallo plakken **toevoegen DNS-server** textbox in Hallo **DNS-servers** blade. Horizontaal schuiven toohello links toocopy Hallo tweede IP-adres en plak deze in Hallo **toevoegen DNS-server** textbox.

    ![Domain Services: DNS bijwerken](./media/getting-started/domain-services-update-dns.png)

5. Klik op **opslaan** wanneer u tooupdate Hallo DNS-servers voor het virtuele netwerk Hallo zijn klaar.

> [!NOTE]
> Hallo nieuwe DNS-instellingen voor ophalen virtuele machines in Hallo netwerk alleen na het opnieuw opstarten. Als u ze tooget Hallo bijgewerkt DNS-instellingen meteen moet, activeert u een herstart door het Hallo-portal, PowerShell of CLI Hallo.
>
>

## <a name="next-step"></a>Volgende stap
[Taak 5: wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen](active-directory-ds-getting-started-password-sync.md)

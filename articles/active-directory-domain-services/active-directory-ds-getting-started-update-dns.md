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
ms.openlocfilehash: 484ff1a197a651bccb2b416448056acf69b0d8c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="update-dns-settings-for-hello-azure-virtual-network"></a>DNS-instellingen bijwerken voor Hallo virtuele Azure-netwerk
## <a name="task-4-update-dns-settings-for-hello-azure-virtual-network"></a>Taak 4: Bijwerken van DNS-instellingen voor Hallo virtuele Azure-netwerk
In de Hallo voorgaande configuratietaken, hebt u Azure Active Directory Domain Services voor uw directory is ingeschakeld. de volgende taak Hallo is tooensure dat computers in het virtuele netwerk Hallo kunnen verbinding maken en gebruiken van deze services. In dit artikel leert bijwerken u Hallo DNS-serverinstellingen voor uw virtuele netwerk toopoint toohello twee IP-adressen waarop Azure Active Directory Domain Services beschikbaar op Hallo virtueel netwerk is.

> [!NOTE]
> Nadat u Azure Active Directory Domain Services voor Hallo directory hebt ingeschakeld, houd er rekening mee Hallo IP-adressen voor Azure Active Directory Domain Services die worden weergegeven op Hallo **configureren** tabblad van uw directory.
>
>

tooupdate hello DNS-serverinstellingen voor Hallo virtuele netwerk waarin u Azure Active Directory Domain Services voltooid Hallo stappen hebt ingeschakeld:

1. Ga toohello [klassieke Azure-portal](https://manage.windowsazure.com).
2. Selecteer in het linkerdeelvenster Hallo **netwerken**.  
    Hallo **netwerken** venster wordt geopend.

    ![Venster met virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-network-select.png)
3. Op Hallo **virtuele netwerken** tabblad, selecteer Hallo virtuele netwerk waarin u ingeschakeld Azure Active Directory Domain Services tooview eigenschappen ervan.
4. Klik op Hallo **configureren** tabblad.

    ![Venster met virtuele netwerken](./media/active-directory-domain-services-getting-started/virtual-network-configure-tab.png)
5. In Hallo **DNS-servers** sectie, voert u beide Hallo IP-adressen die werden weergegeven in Hallo **domeinservices** sectie op Hallo **configureren** tabblad van uw directory.
6. toosave hello DNS-serverinstellingen voor dit virtuele netwerk, in het taakvenster Hallo Hallo onder aan Hallo venster, klikt u op **opslaan**.

   ![Hallo DNS-serverinstellingen voor het virtuele netwerk Hallo bijwerken](./media/active-directory-domain-services-getting-started/update-dns.png)

> [!NOTE]
>  Hallo nieuwe DNS-instellingen voor ophalen virtuele machines in Hallo netwerk alleen na het opnieuw opstarten. Als u ze tooget Hallo bijgewerkt DNS-instellingen meteen moet, activeert u een herstart door het Hallo-portal, PowerShell of CLI Hallo.
>
>

## <a name="next-steps"></a>Volgende stappen
Taak 5: [wachtwoord synchronisatie tooAzure Active Directory Domain Services inschakelen](active-directory-ds-getting-started-password-sync.md)

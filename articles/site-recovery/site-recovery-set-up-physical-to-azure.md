---
title: Instellen van Hallo bronomgeving (fysieke servers tooAzure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van fysieke servers waarop Windows of Linux wordt uitgevoerd in Azure.
services: site-recovery
documentationcenter: 
author: AnoopVasudavan
manager: gauravd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/29/2017
ms.author: anoopkv
ms.openlocfilehash: d4702265bf36910015685d2bba99d6e577531bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-physical-server-tooazure"></a>Hallo bronomgeving (fysieke server tooAzure) instellen
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [Fysieke tooAzure](./site-recovery-set-up-physical-to-azure.md)

Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van fysieke servers waarop Windows of Linux wordt uitgevoerd in Azure.

## <a name="prerequisites"></a>Vereisten

Hallo artikel wordt ervan uitgegaan dat u al hebt:
1. Een Recovery Services-kluis in Hallo [Azure-portal](http://portal.azure.com "Azure-portal").
3. Een fysieke computer op welke server tooinstall Hallo configuratie.

### <a name="configuration-server-minimum-requirements"></a>Minimale vereisten voor configuratie-server
Hallo volgende tabel geeft een lijst Hallo minimale hardware, software en netwerkvereisten voor een configuratieserver.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS gebaseerde proxy-servers worden niet ondersteund door de configuratieserver Hallo.

## <a name="choose-your-protection-goals"></a>Uw beveiligingsdoelstellingen kiezen

1. Ga in de Azure-portal hello, toohello **Recovery Services** blade-kluizen en selecteer uw kluis.
2. In Hallo **Resource** menu van Hallo kluis, klikt u op **aan de slag** > **siteherstel** > **stap 1: voorbereiden Infrastructuur** > **beveiligingsdoel**.

    ![Doelstellingen kiezen](./media/site-recovery-set-up-physical-to-azure/choose-goals.png)
3. In **beveiligingsdoel**, selecteer **tooAzure** en **niet gevirtualiseerde/andere**, en klik vervolgens op **OK**.

    ![Doelstellingen kiezen](./media/site-recovery-set-up-physical-to-azure/physical-protection-goal.PNG)

## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen

1. In **bron voorbereiden**, als u een configuratieserver, klikt u op geen **+ configuratieserver** tooadd een.

  ![Bron instellen](./media/site-recovery-set-up-physical-to-azure/plus-config-srv.png)
2. In Hallo **Server toevoegen** blade, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.
5. Hallo kluisregistratiesleutel downloaden. Wanneer u Setup Unified uitvoert moet u de registratiesleutel Hallo. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

    ![Bron instellen](./media/site-recovery-set-up-physical-to-azure/set-source2.png)
6. Uitvoeren op Hallo machine u als de configuratieserver Hallo **Azure Site Recovery Unified Setup** tooinstall Hallo configuratieserver en processerver Hallo Hallo master van de doelserver.

#### <a name="run-azure-site-recovery-unified-setup"></a>Voer Azure Site Recovery Unified Setup

> [!TIP]
> Registratie van de configuratie-server mislukt als Hallo tijd op de systeemklok van de computer afmeldt bij de lokale tijd meer dan vijf minuten. Synchroniseren van uw systeemklok met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) voordat u Hallo installatie start.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Hallo configuratieserver kan worden geïnstalleerd via een opdrachtregel. Zie voor meer informatie [configuratie-server installeren met behulp van de opdrachtregelprogramma's](http://aka.ms/installconfigsrv).


## <a name="common-issues"></a>Algemene problemen

[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Volgende stappen

Volgende stap omvat [instellen van uw doelomgeving](./site-recovery-prepare-target-physical-to-azure.md) in Azure.

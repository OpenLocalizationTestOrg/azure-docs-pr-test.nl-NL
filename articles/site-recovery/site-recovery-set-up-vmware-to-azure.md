---
title: Instellen van Hallo bronomgeving (VMware tooAzure) | Microsoft Docs
description: Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van VMware-virtuele machines tooAzure.
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
ms.openlocfilehash: cbeeffc1061b11223e12ff3e237fa7e55b999aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-hello-source-environment-vmware-tooazure"></a>Hallo bronomgeving (VMware tooAzure) instellen
> [!div class="op_single_selector"]
> * [VMware tooAzure](./site-recovery-set-up-vmware-to-azure.md)
> * [Fysieke tooAzure](./site-recovery-set-up-physical-to-azure.md)

Dit artikel wordt beschreven hoe tooset van uw lokale omgeving toostart repliceren van virtuele machines die wordt uitgevoerd op de VMware-tooAzure.

## <a name="prerequisites"></a>Vereisten

Hallo artikel wordt ervan uitgegaan dat u al hebt gemaakt:
- Een Recovery Services-kluis in Hallo [Azure-portal](http://portal.azure.com "Azure-portal").
- Een speciaal account in uw VMware vCenter die kan worden gebruikt voor [automatische detectie](./site-recovery-vmware-to-azure.md).
- Een virtuele machine op welke server tooinstall Hallo configuratie.

## <a name="configuration-server-minimum-requirements"></a>Minimale vereisten voor configuratie-server
Hallo configuratie serversoftware moet worden geïmplementeerd op een maximaal beschikbare virtuele VMware-machine. Hallo volgende tabel geeft een lijst Hallo minimale hardware, software en netwerkvereisten voor een configuratieserver.
[!INCLUDE [site-recovery-configuration-server-requirements](../../includes/site-recovery-configuration-and-scaleout-process-server-requirements.md)]

> [!NOTE]
> HTTPS gebaseerde proxy-servers worden niet ondersteund door de configuratieserver Hallo.

## <a name="choose-your-protection-goals"></a>Uw beveiligingsdoelstellingen kiezen

1. Ga in de Azure-portal hello, toohello **Recovery Services** blade kluis en selecteer uw kluis.
2. Ga te op Hallo resource menu van Hallo kluis**aan de slag** > **siteherstel** > **stap 1: infrastructuur voorbereiden**  >  **Beveiligingsdoel**.

    ![Doelstellingen kiezen](./media/site-recovery-set-up-vmware-to-azure/choose-goals.png)
3. In **beveiligingsdoel**, selecteer **tooAzure**, en kies **Ja, met VMware vSphere Hypervisor**. Klik vervolgens op **OK**.

    ![Doelstellingen kiezen](./media/site-recovery-set-up-vmware-to-azure/choose-goals2.png)

## <a name="set-up-hello-source-environment"></a>Hallo bronomgeving instellen
Instellen van de bronomgeving Hallo omvat twee belangrijkste activiteiten:

- Installeren en registreren van een server configureren met Site Recovery.
- Uw on-premises virtuele machines detecteren door verbinding te maken van Site Recovery tooyour lokale VMware vCenter of vSphere EXSi hosts.

### <a name="step-1-install-and-register-a-configuration-server"></a>Stap 1: Installeren en registreren van een configuratieserver

1. Klik op **stap 1: infrastructuur voorbereiden** > **bron**. In **bron voorbereiden**, als u een configuratieserver, klikt u op geen **+ configuratieserver** tooadd een.

    ![Bron instellen](./media/site-recovery-set-up-vmware-to-azure/set-source1.png)
2. Op Hallo **Server toevoegen** blade, controleert u of **configuratieserver** wordt weergegeven in **servertype**.
4. Download het installatiebestand van de installatie van Site Recovery-Unified Hallo.
5. Hallo kluisregistratiesleutel downloaden. Wanneer u Setup Unified uitvoert moet u de registratiesleutel Hallo. Hallo-sleutel is vijf dagen na het genereren ervan geldig.

    ![Bron instellen](./media/site-recovery-set-up-vmware-to-azure/set-source2.png)
6. Uitvoeren op Hallo machine u als de configuratieserver Hallo **Azure Site Recovery Unified Setup** tooinstall Hallo configuratieserver en processerver Hallo Hallo master van de doelserver.

#### <a name="run-azure-site-recovery-unified-setup"></a>Voer Azure Site Recovery Unified Setup

> [!TIP]
> Registratie van de configuratie-server mislukt als Hallo tijd op de systeemklok van uw computer van de lokale tijd van meer dan vijf minuten verschilt. Synchroniseren van uw systeemklok met een [tijdserver](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service) voordat u Hallo installatie start.

[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> Hallo configuratieserver kan worden geïnstalleerd via de opdrachtregel. Zie voor meer informatie [Hallo-configuratieserver installeren met behulp van de opdrachtregelprogramma's](http://aka.ms/installconfigsrv).

#### <a name="add-hello-vmware-account-for-automatic-discovery"></a>Hallo VMware-account voor automatische detectie toevoegen

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="step-2-add-a-vcenter"></a>Stap 2: Een vCenter toevoegen
tooallow Azure Site Recovery toodiscover virtuele machines die worden uitgevoerd in uw on-premises-omgeving, moet u tooconnect uw VMware vCenter-Server of vSphere ESXi-hosts met Site Recovery.

Selecteer **+ vCenter** toostart gebruikmaken van een VMware vCenter-server of een VMware vSphere ESXi-host.

[!INCLUDE [site-recovery-add-vcenter](../../includes/site-recovery-add-vcenter.md)]


## <a name="common-issues"></a>Algemene problemen
[!INCLUDE [site-recovery-vmware-to-azure-install-register-issues](../../includes/site-recovery-vmware-to-azure-install-register-issues.md)]


## <a name="next-steps"></a>Volgende stappen
[Instellen van uw doelomgeving](./site-recovery-prepare-target-vmware-to-azure.md) in Azure.

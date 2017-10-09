---
title: schijfversleuteling aaaApply in Azure Security Center | Microsoft Docs
description: Dit document leest u hoe tooimplement hello Azure Security Center aanbeveling ** schijf versleuteling ** van toepassing.
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 6cc7824a-8d6b-4a5f-ab40-e3bbaebc4a91
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/02/2017
ms.author: terrylan
ms.openlocfilehash: cd803f1120018c5c86da91186eec1e59d425ede7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apply-disk-encryption-in-azure-security-center"></a>Schijfversleuteling in Azure Security Center toepassen
Azure Security Center adviseert schijfversleuteling toe te passen als u Windows of Linux-VM-schijven die niet zijn versleuteld met behulp van Azure Disk Encryption hebt. Schijfversleuteling kunt u de schijven voor Windows en Linux IaaS VM versleutelen.  Versleuteling wordt aanbevolen voor zowel hello OS- en gegevensvolumes op de virtuele machine.

Schijfversleuteling maakt gebruik van Hallo-industriestandaard [BitLocker](https://technet.microsoft.com/library/cc732774.aspx) functie van Windows en Hallo [DM-Crypt](https://en.wikipedia.org/wiki/Dm-crypt) functie van Linux. Deze functies bieden OS en data encryption toohelp beveiligen en uw gegevens beschermen en voldoen aan de beveiliging van de organisatie en de naleving verplichtingen. Schijfversleuteling is geïntegreerd met [Azure Key Vault](https://azure.microsoft.com/documentation/services/key-vault/) toohelp u beheren en een Hallo schijf versleutelingssleutels en geheimen in uw abonnement Sleutelkluis terwijl u ervoor zorgt dat alle gegevens op Hallo VM-schijven zijn versleuteld in rust in uw beheren[ Azure Storage](https://azure.microsoft.com/documentation/services/storage/).

> [!NOTE]
> Azure Disk Encryption wordt ondersteund op Hallo Windows-serverbesturingssystemen - Windows Server 2008 R2, Windows Server 2012 en Windows Server 2012 R2 te volgen. Schijfversleuteling wordt ondersteund op Hallo Linux-serverbesturingssystemen - Ubuntu, CentOS, SUSE en SUSE Linux Enterprise Server (SLES) te volgen.
>
>

## <a name="implement-hello-recommendation"></a>Hallo aanbeveling implementeren
1. In Hallo **aanbevelingen** blade Selecteer **schijfversleuteling toepassen**.
2. In Hallo **schijfversleuteling toepassen** blade ziet u een lijst van virtuele machines waarvoor schijfversleuteling wordt aanbevolen.
3. Ga als volgt Hallo instructies tooapply versleuteling toothese virtuele machines.

![][1]

Azure Virtual Machines die zijn geïdentificeerd door Security Center welke tooencrypt, raden we Hallo stappen te volgen:

* Installeer en configureer Azure PowerShell. Hiermee kunt u toorun Hallo PowerShell-opdrachten vereist tooset up Hallo vereisten vereist tooencrypt Azure Virtual Machines.
* Verkrijgen en hello Azure schijf versleuteling vereisten Azure PowerShell-script uitvoeren.
* Versleutel uw virtuele machines.

[Een virtuele Machine van Azure versleutelen](security-center-disk-encryption.md) leidt u door deze stappen.  In dit onderwerp wordt ervan uitgegaan dat u gebruikmaakt van Windows 10 als clientmachine Hallo waarin u schijfversleuteling configureren.

Er zijn veel manieren die kunnen worden gebruikt voor Azure Virtual Machines. Als u al goed bekend bent met Azure PowerShell of Azure CLI, kunt u alternatieve methoden toouse mogelijk liever. toolearn over deze andere benaderingen, Zie [Azure disk encryption](../security/azure-security-disk-encryption.md).

## <a name="see-also"></a>Zie ook
Dit document hebt u geleerd hoe tooimplement Hallo Security Center aanbeveling 'toepassen schijfversleuteling." toolearn meer informatie over schijfversleuteling, Hallo ziet:

* [Versleuteling en sleutel-beheer met Azure Key Vault](https://azure.microsoft.com/documentation/videos/azurecon-2015-encryption-and-key-management-with-azure-key-vault/) (video 36 min 39 sec)--meer informatie over hoe toouse Schijfbeheer versleuteling voor IaaS VM's en Azure Key Vault toohelp beveiligen en uw gegevens beschermen.
* [Een virtuele Machine van Azure versleutelen](security-center-disk-encryption.md) (document)--meer informatie over hoe tooencrypt Azure Virtual Machines.
* [Azure schijfversleuteling](../security/azure-security-disk-encryption.md) (document)--meer informatie over hoe tooenable schijfversleuteling voor Windows en Linux-machines.

toolearn meer informatie over Security Center Hallo ziet:

* [Beveiligingsbeleid instellen in Azure Security Center](security-center-policies.md) --meer informatie over hoe tooconfigure beveiligingsbeleid.
* [Beveiligingsstatus bewaken in Azure Security Center](security-center-monitoring.md) --meer informatie over hoe toomonitor Hallo status van uw Azure-resources.
* [Het beheer van is en reageert toosecurity waarschuwingen in Azure Security Center](security-center-managing-and-responding-alerts.md) --meer informatie over hoe toomanage en gereageerd had toosecurity waarschuwingen.
* [Aanbevelingen voor beveiliging in Azure Security Center beheren](security-center-recommendations.md) --Leer hoe aanbevelingen u uw Azure-resources te beveiligen.
* [Veelgestelde vragen over Azure Security Center](security-center-faq.md) --Raadpleeg Veelgestelde vragen over het gebruik van Hallo-service.
* [Azure-Beveiligingsblog](http://blogs.msdn.com/b/azuresecurity/) --Lees blogberichten over Azure-beveiliging en naleving.

<!--Image references-->
[1]: ./media/security-center-apply-disk-encryption/apply-disk-encryption.png

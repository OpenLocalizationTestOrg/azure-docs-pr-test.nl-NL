---
title: aaaModify hello DATA 0-instellingen op een StorSimple-apparaat | Microsoft Docs
description: Meer informatie over hoe toouse Windows PowerShell voor StorSimple tooreconfigure Hallo DATA 0-netwerkinterface op uw StorSimple-apparaat.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 58e3d509-f425-4a7f-b650-d496a7c85193
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: caec51c3344d953299253301c2a0d7577d553c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-device"></a>Hallo DATA 0 netwerkinterface-instellingen op uw StorSimple-apparaat wijzigen
## <a name="overview"></a>Overzicht
Uw Microsoft Azure StorSimple-apparaat heeft zes netwerkinterfaces, van de DATA 0 tooDATA 5. Hallo DATA 0-interface is altijd geconfigureerd via Windows PowerShell-interface Hallo of Hallo seriële console en is automatisch ingeschakeld voor de cloud. Houd er rekening mee dat u kunt DATA 0-netwerkinterface via de klassieke Azure-portal Hallo niet configureren. 

Hallo DATA 0 interface eerst via de wizard setup Hallo tijdens de eerste installatie van Hallo StorSimple-apparaat is geconfigureerd. Wanneer het Hallo-apparaat is een bedrijfsmodus, moet u wellicht tooreconfigure DATA 0 instellingen. Deze zelfstudie biedt twee methoden toomodify DATA 0 netwerkinstellingen, beide via Windows PowerShell voor StorSimple.

Na het lezen van deze zelfstudie, kunt u zich kunt:

* Wijzigen van de DATA 0-instelling via de wizard setup Hallo-netwerk
* DATA 0 netwerkinstellingen via Hallo wijzigen `Set-HcsNetInterface` cmdlet

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>DATA 0 netwerkinstellingen via de wizard setup wijzigen
U kunt DATA 0-netwerkinstellingen configureren door verbinding te maken van Windows PowerShell-interface toohello van uw StorSimple-apparaat en het starten van een sessie van de wizard setup. Uitvoeren van de volgende stappen toomodify DATA 0 Hallo instellingen:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>toomodify DATA 0 netwerkinstellingen via de wizard setup
1. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**. Als u wordt gevraagd Hallo bieden **wachtwoord apparaatbeheerder**. Hallo standaardwachtwoord is `Password1`.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Invoke-HcsSetupWizard`
3. Een setup-wizard verschijnt toohelp configureren van Hallo DATA 0-interface van het apparaat. Nieuwe waarden opgeven voor Hallo IP-adres, gateway en IP-masker.

> [!NOTE]
> Hallo vaste IP-adressen opnieuw worden geconfigureerd via Hallo toobe moet domeincontrollers **configureren** pagina van Hallo StorSimple-apparaat in Hallo klassieke Azure-portal. Voor meer informatie gaat te[netwerkinterfaces wijzigen](storsimple-modify-device-config.md#modify-network-interfaces).
> 
> 

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>DATA 0 netwerkinstellingen via de cmdlet Set-HcsNetInterface wijzigen
Een andere manier tooreconfigure DATA 0-netwerkinterface via het gebruik van de Hallo Hallo is `Set-HcsNetInterface` cmdlet. Hallo-cmdlet wordt uitgevoerd vanuit de Windows PowerShell-interface Hallo van uw StorSimple-apparaat. Wanneer u deze procedure gebruikt, kan Hallo controller vaste IP-adressen ook hier worden geconfigureerd. Uitvoeren van de volgende stappen toomodify Hallo DATA 0 Hallo instellingen: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>toomodify DATA 0 netwerkinstellingen via de cmdlet Set-HcsNetInterface Hallo
1. In het menu van de seriële console hello, kies optie 1, **aanmelden met volledige toegang**. Als u wordt gevraagd wachtwoord apparaatbeheerder Hallo bieden. Hallo standaardwachtwoord is `Password1`.
2. Typ het volgende achter de opdrachtprompt Hallo:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Typ in de hoek Hallo vierkante haken, Hallo volgende waarden op voor de DATA 0:
   
   * IPv4-adres
   * IPv4-gateway
   * IPv4-subnetmasker
   * Vaste IPv4-adressen voor Controller 0
   * Vaste IPv4-adres voor de Controller 1
     
     Voor meer informatie over Hallo gebruik van deze cmdlet, gaat u te[Windows PowerShell voor StorSimple cmdlet-verwijzing](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Volgende stappen
* tooconfigure netwerkinterfaces, behalve DATA 0, kunt u Hallo [pagina configureren in de klassieke Azure-portal Hallo](storsimple-modify-device-config.md). 
* Als u problemen ondervindt bij het configureren van uw netwerkinterfaces, raadpleeg dan te[implementatieproblemen oplossen](storsimple-troubleshoot-deployment.md).


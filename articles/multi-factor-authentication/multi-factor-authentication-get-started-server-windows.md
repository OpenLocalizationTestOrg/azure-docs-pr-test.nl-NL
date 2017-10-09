---
title: aaaWindows verificatie en Azure MFA-Server | Microsoft Docs
description: Dit is hello Azure multi-factor authentication-pagina die u helpt bij het implementeren van Windows-verificatie en Azure multi-factor Authentication-Server.
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Windows-verificatie en Azure Multi-Factor Authentication-server
Sectie van de Windows-verificatie Hallo van hello Azure multi-factor Authentication-Server tooenable gebruik en configureren van Windows-verificatie voor toepassingen. Voordat u Windows-verificatie instellen, houd Hallo lijst rekening te volgen:

* Na de installatie opnieuw worden opgestart hello Azure multi-factor Authentication voor Terminal Services tootake effect.
* Als 'Overeenkomende Azure multi-factor Authentication-gebruiker vereisen' is ingeschakeld en u zich niet in de gebruikerslijst hello, zich u niet kunnen toolog naar Hallo machine na opnieuw opstarten.
* Goedgekeurde dat IP-adressen is afhankelijk van of de toepassing hello Hallo client-IP-met Hallo-verificatie kan bieden. Momenteel wordt alleen Terminal Services ondersteund.  

> [!NOTE]
> Deze functie is geen ondersteunde toosecure Terminal Services in Windows Server 2012 R2.

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a>toosecure een toepassing met de Windows-verificatie, gebruik Hallo procedure te volgen.
1. Klik op Hallo Windows-verificatie pictogram hello Azure multi-factor Authentication-Server.
   ![Windows-verificatie](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)
2. Controleer de Hallo **Windows-verificatie inschakelen** selectievakje. Dit selectievakje is standaard uitgeschakeld.
3. Hallo op het tabblad toepassingen kan Hallo beheerder tooconfigure een of meer toepassingen voor Windows-verificatie.
4. Selecteer een server of toepassing – opgeven of Hallo servertoepassing is ingeschakeld. Klik op **OK**.
5. Klik op **Toevoegen...**
6. Hallo goedgekeurde IP-adressen tabblad kunt u tooskip Azure multi-factor Authentication voor Windows-sessies die afkomstig zijn van specifieke IP-adressen. Bijvoorbeeld, als beslissen werknemers gebruiken toepassing hello van Hallo kantoor of thuis, u dat u niet wilt dat hun telefoons voor Azure multi-factor Authentication terwijl ze op Hallo office overbodig. Hiervoor geeft u het subnet van kantoor Hallo als goedgekeurde IP-adressen.
7. Klik op **Toevoegen...**
8. Selecteer **één IP-adres** indien tooskip één IP-adres gewenst.
9. Selecteer **IP-bereik** indien tooskip gehele IP-bereik gewenst. Voorbeeld 10.63.193.1-10.63.193.100.
10. Selecteer **Subnet** indien toospecify een bereik gewenst van IP-adressen met subnetnotatie. Geef IP-beginadres van Hallo-subnet en kies vervolgens Hallo relevante netmasker in de vervolgkeuzelijst Hallo.
11. Klik op **OK**.

## <a name="next-steps"></a>Volgende stappen

- [VPN-apparaten van derden configureren voor Azure MFA Server](multi-factor-authentication-advanced-vpn-configurations.md)

- [Uitbreiden van uw bestaande infrastructuur voor verificatie met Hallo NPS-extensie voor Azure MFA](multi-factor-authentication-nps-extension.md)

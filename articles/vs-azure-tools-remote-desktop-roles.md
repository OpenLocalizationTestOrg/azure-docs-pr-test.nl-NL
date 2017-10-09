---
title: Extern bureaublad met de Azure-functies aaaUsing | Microsoft Docs
description: Extern bureaublad gebruiken met Azure-functies
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: f5727ebe-9f57-4d7d-aff1-58761e8de8c1
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d35fd421cde8be9e3caa474db95974a54e528bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-remote-desktop-with-azure-roles"></a>Extern bureaublad gebruiken met Azure-functies
Hello Azure SDK en extern bureaublad-Services gebruikt, kunt u toegang tot Azure-functies en virtuele machines die worden gehost door Azure. U kunt Extern bureaublad-Services configureren vanuit een Azure-cloud service-project in Visual Studio. tooenable extern bureaublad-Services, moet u een project werkt met een of meer rollen maken en vervolgens publiceren tooAzure.

> [!IMPORTANT]
> U moet toegang tot een Azure-functie voor het oplossen van problemen of alleen-ontwikkeling. Hallo doel van elke virtuele machine is een specifieke functie in uw Azure-toepassing, niet toorun toorun andere clienttoepassingen. Als u toouse Azure toohost een virtuele machine die u gebruiken voor enig doel wilt kunt, raadpleegt u toegang tot Azure virtuele Machines in Server Explorer.
> 
> 

## <a name="tooenable-and-use-remote-desktop-for-an-azure-role"></a>tooenable en gebruik extern bureaublad voor een Azure-rol
1. Klik in Solution Explorer open Hallo snelmenu voor uw cloud service-project en kies vervolgens **publiceren**.
   
    Hallo **Publish Azure Application** wizard wordt weergegeven.
   
    ![Opdracht voor een Cloud Service-project publiceren](./media/vs-azure-tools-remote-desktop-roles/IC799161.png)
2. Hallo onderaan in **Microsoft Azure Publish Settings** pagina van wizard hello, selecteer Hallo **extern bureaublad inschakelen** voor alle functies selectievakje. 
   
    Hallo **configuratie voor extern bureaublad** dialoogvenster wordt weergegeven.
3. Hallo Hallo onderaan in **configuratie voor extern bureaublad** dialoogvenster Kies Hallo **meer opties** knop. 
   
    U ziet nu een vervolgkeuzelijst waarmee u Maak of Selecteer een certificaat dat u referenties gegevens versleutelen kunt om verbinding te maken via Extern bureaublad.
4. Kies in de vervolgkeuzelijst Hallo  **&lt;maken >**, of kies een bestaande uit Hallo-lijst. 
   
    Als u een bestaand certificaat kiest, slaat u Hallo stappen te volgen.
   
   > [!NOTE]
   > Hallo-certificaten die u nodig hebt voor een verbinding met extern bureaublad wijken af van het Hallo-certificaten die u voor andere Azure-bewerkingen gebruikt. Hallo RAS-certificaat moet een persoonlijke sleutel hebben.
   > 
   > 
   
    Hallo **certificaat maken** dialoogvenster wordt weergegeven.
   
   1. Geef een beschrijvende naam voor het nieuwe certificaat Hallo en kies vervolgens Hallo **OK** knop. Hallo nieuw certificaat wordt weergegeven in de vervolgkeuzelijst Hallo.
   2. In Hallo **configuratie voor extern bureaublad** dialoogvenster Geef een gebruikersnaam en wachtwoord.
      
       U kunt een bestaand account niet gebruiken. Geen beheerder opgeven als de gebruikersnaam Hallo voor Hallo nieuw account.
      
      > [!NOTE]
      > Als Hallo wachtwoord niet voldoet aan de complexiteitsvereisten hello, verschijnt een rode volgende toohello wachtwoord in het tekstvak. Hallo-wachtwoord moet bevatten hoofdletters, kleine letters en cijfers of symbolen.
      > 
      > 
   3. Kies een datum op welk account Hallo verloopt en na welke Extern bureaublad-verbindingen worden geblokkeerd.
   4. Nadat u hebt opgegeven alle vereiste gegevens hello, kiest u Hallo **OK** knop.
      
       Diverse instellingen waarmee u Remote Access Services worden toohello .cscfg en .csdef-bestanden worden toegevoegd.
5. In Hallo **Microsoft Azure Publish Settings** wizard Hallo kiezen **OK** knop wanneer u bent klaar toopublish uw cloudservice.
   
    Als u niet klaar toopublish bent, kiest u Hallo **annuleren** knop. Hallo-configuratie-instellingen worden opgeslagen en u kunt uw cloudservice later publiceren.

## <a name="connect-tooan-azure-role-by-using-remote-desktop"></a>Tooan Azure rol verbinding met extern bureaublad
Nadat u uw cloudservice op Azure hebt gepubliceerd, kunt u Server Explorer toolog in Hallo virtuele machines die Azure als host fungeert. 

1. Vouw in Server Explorer Hallo **Azure** knooppunt, en vouw vervolgens Hallo knooppunt voor een cloudservice en een van de rollen toodisplay een lijst van exemplaren.
2. Open Hallo snelmenu voor een exemplaar-knooppunt en kies vervolgens **verbinding maken met behulp van extern bureaublad**.
   
    ![Verbinding maken via Extern bureaublad](./media/vs-azure-tools-remote-desktop-roles/IC799162.png)
3. Voer Hallo-gebruikersnaam en wachtwoord die u eerder hebt gemaakt. U bent nu aangemeld bij de externe sessie.


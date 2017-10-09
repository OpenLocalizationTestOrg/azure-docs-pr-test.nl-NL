---
title: aaaEnable verbinding met extern bureaublad voor een rol in Azure Cloud Services | Microsoft Docs
description: Hoe tooconfigure uw azure cloud service-toepassing tooallow extern bureaublad-verbindingen
services: cloud-services
documentationcenter: 
author: mmccrory
manager: timlt
editor: 
ms.assetid: 73ea1d64-1529-4d72-b58e-f6c10499e6bb
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: mmccrory
ms.openlocfilehash: 55d7043df571c2e88b04aa9ef01dc8ae1d6784f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Verbinding met extern bureaublad voor een rol in Azure Cloudservices inschakelen
> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Klassieke Azure Portal](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)
>
>

Extern bureaublad kunt u tooaccess Hallo bureaublad van een functie die wordt uitgevoerd in Azure. U kunt een tootroubleshoot extern bureaublad-verbinding gebruiken en analyseren van problemen met uw toepassing, terwijl deze wordt uitgevoerd.

U kunt een verbinding met extern bureaublad in uw rol tijdens het ontwikkelen van inschakelen door Hallo extern bureaublad-modules in de servicedefinitie van de of u kunt tooenable extern bureaublad via Hallo uitbreidingsmodule Extern bureaublad. Hallo is gewenste aanpak toouse Hallo extern bureaublad-uitbreiding zoals u extern bureaublad inschakelen kunt, zelfs nadat de toepassing hello zonder tooredeploy uw toepassing wordt geïmplementeerd.

## <a name="configure-remote-desktop-from-hello-azure-portal"></a>Extern bureaublad configureren via hello Azure-portal
Hello Azure-portal gebruikt Hallo uitbreidingsmodule Extern bureaublad-benadering, zodat u extern bureaublad inschakelen kunt, zelfs nadat het Hallo-toepassing wordt geïmplementeerd. Hallo **extern bureaublad** blade voor uw cloudservice, kunt u tooenable extern bureaublad, wijziging Hallo lokale Administrator-account gebruikt tooconnect toohello virtuele machines, Hallo certificaat gebruikt bij de verificatie en Hallo instellen de vervaldatum.

1. Klik op **Cloudservices**Hallo-naam van de cloudservice Hallo op en klik vervolgens op **extern bureaublad**.

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop.png)

2. Kies of u tooenable extern bureaublad voor een afzonderlijke functie of voor alle functies wilt en Hallo-waarde van Hallo schakelbaar ook wijzigen**ingeschakeld**.

3. Vul de velden Hallo vereist voor de gebruikersnaam, wachtwoord, verlopen en certificaat.

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Details.png)

   > [!WARNING]
   > Alle exemplaren van de functie wordt opnieuw gestart wanneer u eerst Extern bureaublad inschakelen en klik op OK (vinkje). tooprevent opnieuw worden opgestart, gebruikte tooencrypt Hallo-Hallo certificaatwachtwoord moet worden geïnstalleerd op Hallo-rol. tooprevent opnieuw is opgestart, [upload een certificaat voor de cloudservice hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) en ga daarna terug toothis dialoogvenster.
   >
   >
3. In **rollen**, selecteer Hallo rol of wilt u tooupdate Selecteer **alle** voor alle functies.

4. Wanneer u klaar bent met de updates voor uw configuratie, klikt u op **opslaan**. Het duurt enige tijd duren voordat uw rolinstanties gereed tooreceive verbindingen zijn.

## <a name="remote-into-role-instances"></a>De afstand in rolinstanties
Zodra de extern bureaublad op Hallo-functies is ingeschakeld, kunt u een verbinding rechtstreeks vanuit hello Azure-Portal te starten:

1. Klik op **exemplaren** tooopen hello **exemplaren** blade.
2. Selecteer een rolexemplaar met extern bureaublad die zijn geconfigureerd.
3. Klik op **Connect** toodownload een RDP-bestand voor de rolinstantie Hallo.

    ![Extern bureaublad voor cloud-services](./media/cloud-services-role-enable-remote-desktop-new-portal/CloudServices_Remote_Desktop_Connect.png)

4. Klik op **Open** en vervolgens **Connect** toostart Hallo extern bureaublad-verbinding.

>[!NOTE]
> Als uw cloudservice zich bevindt achter een NSG, moet u mogelijk toocreate regels die verkeer op poorten toestaan **3389** en **20000**.  Extern bureaublad maakt gebruik van poort **3389**.  Cloud Service-exemplaren worden verdeeld, zodat u niet rechtstreeks welke tooconnect exemplaar om te controleren.  Hallo *RemoteForwarder* en *RemoteAccess* agents beheren van RDP-verkeer en Hallo client toosend een RDP-cookie toestaan en opgeven van een afzonderlijke instantie tooconnect aan.  Hallo *RemoteForwarder* en *RemoteAccess* agents vereisen die poort **20000*** worden geopend die worden geblokkeerd als er een NSG.

## <a name="additional-resources"></a>Aanvullende bronnen

[Hoe tooConfigure Cloudservices](cloud-services-how-to-configure.md)
[extern bureaublad-services FAQ - Cloud](cloud-services-faq.md)

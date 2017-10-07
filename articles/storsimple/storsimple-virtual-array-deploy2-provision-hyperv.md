---
title: aaaProvision virtuele StorSimple-matrix in Hyper-V | Microsoft Docs
description: Deze tweede zelfstudie in virtuele StorSimple-matrix implementatie omvat het inrichten van een virtuele-matrix in Hyper-V.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>StorSimple virtuele matrix - inrichten in Hyper-V implementeren
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt beschreven hoe tooprovision een virtueel StorSimple matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2. In dit artikel is van toepassing toohello implementatie van virtuele StorSimple-matrices in Azure portal en Microsoft Azure Government Cloud.

U moet administrator-bevoegdheden tooprovision en configureren van een virtuele-matrix. Hallo inrichting en de initiële installatie kan toocomplete van ongeveer 10 minuten duren.

## <a name="provisioning-prerequisites"></a>Vereiste onderdelen inrichten
Hier vindt u Hallo vereisten tooprovision een virtuele-matrix op een hostsysteem met Hyper-V op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Voor Hallo StorSimple-apparaat Manager-service
Zorg voordat u begint voor het volgende:

* U hebt alle Hallo stappen in [voorbereiden Hallo portal voor virtuele StorSimple-matrix](storsimple-virtual-array-deploy1-portal-prep.md).
* U hebt Hallo virtuele matrix installatiekopie voor Hyper-V van hello Azure-portal gedownload. Zie voor meer informatie **stap 3: Download Hallo virtuele matrix installatiekopie** van [voorbereiden Hallo-portal voor virtuele StorSimple-matrix handleiding](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > Hallo software die wordt uitgevoerd op Hallo virtuele StorSimple-matrix kan alleen worden gebruikt met Hallo StorSimple-apparaat Manager-service.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Hallo voor virtuele StorSimple-matrix
Voordat u een virtuele-matrix implementeert, zorg ervoor dat:

* U hebt toegang tot tooa-hostsysteem met Hyper-V in Windows Server 2008 R2 of hoger dat kan worden gebruikt tooa inrichten met een apparaat.
* Hallo-hostsysteem is kunnen toodedicate Hallo na tooprovision resources van uw virtuele matrix:

  * Een minimum van 4 kernen.
  * Ten minste 8 GB aan RAM-geheugen. Als u van plan tooconfigure Hallo virtuele matrix als bestandsserver bent, ondersteunt 8 GB minder dan 2 miljoen bestanden. U moet 16 GB RAM-geheugen toosupport 2-4 miljoen bestanden.
  * Één netwerkinterface.
  * Een 500 GB virtuele schijf voor gegevens.

### <a name="for-hello-network-in-hello-datacenter"></a>Voor Hallo netwerk in Hallo datacenter
Voordat u begint, Controleer Hallo networking vereisten toodeploy een virtueel StorSimple-matrix en Hallo datacenternetwerk op de juiste wijze configureren. Zie voor meer informatie [virtuele StorSimple-matrix netwerkvereisten](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Stapsgewijze inrichten
tooprovision en verbinding maken met virtuele tooa-matrix, moet u tooperform Hallo stappen te volgen:

1. Zorg ervoor dat het hostsysteem Hallo voldoende bronnen toomeet Hallo minimale virtuele matrix vereisten.
2. Inrichten van een virtuele-matrix in de hypervisor.
3. Hallo virtuele matrix Start en Hallo IP-adres.

Elk van deze stappen wordt uitgelegd in Hallo uit te voeren.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Stap 1: Zorg ervoor dat Hallo hostsysteem aan de minimale virtuele matrix voldoet
toocreate een virtuele-matrix, moet u de:

* Hallo Hyper-V-rol is geïnstalleerd op Windows Server 2012 R2, Windows Server 2012 of Windows Server 2008 R2 SP1.
* Microsoft Hyper-V Manager op een Microsoft Windows-client verbonden toohello host.

Zorg dat de onderliggende hardware (hostsysteem) waarop u virtuele matrix Hallo maakt Hallo kunnen toodedicate Hallo resources tooyour virtuele matrix te volgen:

* Een minimum van 4 kernen.
* Ten minste 8 GB aan RAM-geheugen. Als u van plan tooconfigure Hallo virtuele matrix als bestandsserver bent, ondersteunt 8 GB minder dan 2 miljoen bestanden. U moet 16 GB RAM-geheugen toosupport 2-4 miljoen bestanden.
* Één netwerkinterface.
* 500 GB virtuele schijf voor systeemgegevens.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Stap 2: Een virtuele-matrix in hypervisor inrichten
Volgende stappen tooprovision een apparaat in uw hypervisor Hallo uitvoeren.

#### <a name="tooprovision-a-virtual-array"></a>een virtuele-matrix tooprovision
1. Kopieer Hallo virtuele matrix installatiekopie tooa lokaal station op de host Windows Server. U kunt deze installatiekopie (VHD of VHDX) gedownload via hello Azure-portal. Noteer Hallo locatie waar u Hallo installatiekopie gekopieerd als u deze installatiekopie verderop in Hallo procedure gebruikt.
2. Open **Serverbeheer**. In Hallo rechterbovenhoek, klikt u op **extra** en selecteer **Hyper-V-beheer**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Als u Windows Server 2008 R2 uitvoert, opent u Hallo Hyper-V-beheer. Klik in Serverbeheer op **functies > Hyper-V > Hyper-V-beheer**.
3. In **Hyper-V-beheer**in Hallo bereik deelvenster met de rechtermuisknop op uw systeem knooppunt tooopen Hallo contextmenu en klik op **nieuw** > **virtuele Machine**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. Op Hallo **voordat u begint met** pagina Hallo Wizard Nieuwe virtuele Machine, klik op **volgende**.
5. Op Hallo **naam en locatie opgeven** pagina een **naam** voor uw virtuele matrix. Klik op **Volgende**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. Op Hallo **generatie opgeven** pagina, kies afbeeldingstype Hallo-apparaat en klik op **volgende**. Deze pagina wordt niet weergegeven als u Windows Server 2008 R2.

   * Kies **generatie 2** als u een .vhdx-installatiekopie voor Windows Server 2012 of hoger hebt gedownload.
   * Kies **generatie 1** als u een VHD-installatiekopie voor Windows Server 2008 R2 of hoger hebt gedownload.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. Op Hallo **toewijzen van geheugen** pagina, geeft u een **opstartgeheugen** van ten minste **8192 MB**niet inschakelen van dynamisch geheugen en klik vervolgens op **volgende**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. Op Hallo **netwerk configureren** pagina, geef Hallo virtuele switch die is verbonden toohello Internet en klik vervolgens op **volgende**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. Op Hallo **virtuele harde schijf aansluiten** pagina **gebruik een bestaande virtuele harde schijf**Hallo locatie opgeven van Hallo virtuele matrix afbeelding (vhdx of VHD) en klik vervolgens op **volgende**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Bekijk Hallo **samenvatting** en klik vervolgens op **voltooien** toocreate Hallo virtuele machine.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. toomeet hello minimumvereisten, moet u 4 kernen. tooadd 4 virtuele processors, selecteer uw hostsysteem in Hallo **Hyper-V-beheer** venster. In Hallo rechterdeelvenster onder de lijst met Hallo **virtuele Machines**, zoek Hallo virtuele machine die u zojuist hebt gemaakt. Selecteer en met de rechtermuisknop op de naam van de machine Hallo en selecteer **instellingen**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. Op Hallo **instellingen** pagina in Hallo linkerdeelvenster klikt u op **Processor**. Stel in Hallo rechterdeelvenster **aantal virtuele processors** too4 (of meer). Klik op **Toepassen**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. toomeet hello minimumvereisten, moet u ook een schijf van 500 GB virtuele data tooadd. In Hallo **instellingen** pagina:

    1. Selecteer in het linkerdeelvenster Hallo **SCSI-Controller**.
    2. Selecteer in het rechterdeelvenster Hallo **harde schijf** en klik op **toevoegen**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. Op Hallo **harde schijf** pagina, selecteer Hallo **virtuele hardeschijf** optie en klik op **nieuw**. Hallo **Wizard Nieuwe virtuele hardeschijf** wordt gestart.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. Op Hallo **voordat u begint met** pagina Hallo Wizard Nieuwe virtuele hardeschijf, klikt u op **volgende**.
16. Op Hallo **schijfindeling kiezen pagina**, Hallo standaardoptie accepteren **VHDX** indeling. Klik op **Volgende**. Dit scherm niet wordt weergegeven als Windows Server 2008 R2 wordt uitgevoerd.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. Op Hallo **schijftype kiezen pagina**, instellen van het type virtuele harde schijf als **dynamisch uitbreidbare** (aanbevolen). **Een vaste grootte** schijf wilt werken, maar mogelijk moet u toowait lang duren. Het is raadzaam dat u niet Hallo gebruiken **Differencing** optie. Klik op **Volgende**. In Windows Server 2012 R2 en Windows Server 2012 **dynamisch uitbreidbare** is de standaardoptie Hallo terwijl in Windows Server 2008 R2 Hallo standaard **een vaste grootte**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. Op Hallo **naam en locatie opgeven** pagina een **naam** , evenals **locatie** (u kunt bladeren tooone) voor de gegevensschijf Hallo. Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. Op Hallo **schijf configureren** pagina, selecteer Hallo optie **maken van een nieuwe lege virtuele harde-schijf** en geef Hallo grootte als **500 GB** (of meer). 500 GB is de minimale vereiste hello, kunt u altijd inrichten op een grotere schijf. Houd er rekening mee dat u niet kunt vergroten of te Hallo schijf eenmaal ingericht verkleinen. Bekijk voor meer informatie over Hallo grootte van de schijf tooprovision Hallo sizing sectie in Hallo [best practices document](storsimple-ova-best-practices.md). Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. Op Hallo **samenvatting** pagina bekijkt hello details van de van virtuele gegevensschijf en indien wordt voldaan, op **voltooien** toocreate Hallo schijf. Hallo-wizard wordt gesloten en een virtuele harde schijf tooyour machine toegevoegd.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Retourneren van toohello **instellingen** pagina. Klik op **OK** tooclose hello **instellingen** pagina en terug te keren venster tooHyper-V-beheer.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Stap 3: Hallo virtuele matrix Start en u Hallo IP-adres
Hallo toostart stappen te volgen uw virtuele matrix uitvoeren en tooit verbinding.

#### <a name="toostart-hello-virtual-array"></a>toostart hello virtuele matrix
1. Hallo virtuele matrix worden gestart.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Nadat het Hallo-apparaat wordt uitgevoerd, selecteer Hallo-apparaat, klik met de rechtermuisknop en selecteer **Connect**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. Mogelijk hebt u toowait 5-10 minuten voor Hallo apparaat toobe gereed. Een statusbericht wordt weergegeven op Hallo console tooindicate Hallo uitgevoerd. Nadat het Hallo-apparaat klaar is, gaat u te**actie**. Druk op `Ctrl + Alt + Delete` toolog in toohello virtuele matrix. Hallo standaardgebruiker is *StorSimpleAdmin* en is het standaardwachtwoord Hallo *Wachtwoord1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Uit veiligheidsoverwegingen verloopt beheerderswachtwoord Hallo-apparaat bij de eerste aanmelding Hallo. U bent na vragen aan gebruiker toochange Hallo wachtwoord.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Voer een wachtwoord dat ten minste 8 tekens bevat. Hallo wachtwoord moet voldoen aan ten minste 3 buiten Hallo volgens de vereisten van 4: hoofdletters, kleine letters, numerieke en speciale tekens. Hallo wachtwoord tooconfirm opnieuw het. U wordt gewaarschuwd dat Hallo-wachtwoord is gewijzigd.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Nadat het Hallo-wachtwoord is gewijzigd, kunnen virtuele matrix Hallo mogelijk opnieuw opgestart. Wachten op Hallo apparaat toostart.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    Windows PowerShell-console Hallo Hallo-apparaat wordt samen met een voortgangsbalk weergegeven.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. Stap 6-8 zijn alleen van toepassing wanneer in een omgeving met niet-DHCP-up wordt opgestart. Als u zich in een DHCP-omgeving, slaat u deze stappen over en gaat u toostep 9. Als u van uw apparaat in niet-DHCP-omgeving opgestart, ziet u Hallo scherm te volgen.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Configureer vervolgens Hallo-netwerk.
7. Gebruik Hallo `Get-HcsIpAddress` opdracht toolist Hallo-netwerkinterfaces is ingeschakeld op uw virtuele matrix. Als uw apparaat één netwerkinterface is ingeschakeld heeft, de naam die is toegewezen Hallo-toothis standaardinterface is `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Gebruik Hallo `Set-HcsIpAddress` cmdlet tooconfigure Hallo netwerk. Zie Hallo voorbeeld te volgen:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Nadat het Hallo eerste installatie is voltooid en Hallo apparaat is opgestart, ziet u bannertekst Hallo-apparaat. Noteer Hallo IP-adres en Hallo-URL in Hallo banner tekst toomanage Hallo apparaat weergegeven. Gebruik deze IP-adres tooconnect toohello webgebruikersinterface van uw virtuele matrix en volledige Hallo lokale installatie en registratie.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Optioneel) Deze stap alleen uitvoeren als u uw apparaat bij Hallo Government Cloud implementeert. U kunt nu Hallo Verenigde Staten Federal Information Processing Standard (FIPS) modus op uw apparaat. Hallo FIPS 140-standaard definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door ons Federal government computersystemen voor Hallo bescherming van gevoelige gegevens.

    1. tooenable hello FIPS-modus, Hallo volgende cmdlet uitvoeren:

        `Enable-HcsFIPSMode`
    2. Start opnieuw op uw apparaat wanneer u Hallo FIPS-modus hebt ingeschakeld, zodat de cryptografische validaties Hallo van kracht.

       > [!NOTE]
       > U kunt inschakelen of uitschakelen van FIPS-modus op uw apparaat. Wisselende Hallo apparaat tussen FIPS- en niet FIPS-modus wordt niet ondersteund.
       >
       >

Als uw apparaat voldoet niet aan de minimale configuratievereisten hello, ziet u Hallo volgende fout in Hallo bannertekst (Zie hieronder). Hallo apparaatconfiguratie wijzigen zodat hello machine heeft voldoende bronnen toomeet Hallo minimumvereisten. U kunt vervolgens opnieuw opstarten en toohello apparaat aansluit. Raadpleeg de minimale configuratievereisten voor toohello in [stap 1: Zorg ervoor dat Hallo hostsysteem aan de minimale virtuele matrix voldoet](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Als u een andere fout tijdens de eerste configuratie Hallo Hallo lokale webgebruikersinterface met geconfronteerd, raadpleegt u toohello werkstromen te volgen:

* Diagnostische tests uit te voeren[web UI setup oplossen](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Logboek pakket genereren en logboekbestanden weergeven](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Volgende stappen
* [Uw virtuele StorSimple-matrix instellen als bestandsserver](storsimple-virtual-array-deploy3-fs-setup.md)
* [Uw virtuele StorSimple-matrix ingesteld als een iSCSI-server](storsimple-virtual-array-deploy3-iscsi-setup.md)

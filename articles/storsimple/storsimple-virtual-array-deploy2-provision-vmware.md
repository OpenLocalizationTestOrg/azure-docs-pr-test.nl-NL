---
title: aaaProvision virtuele StorSimple-matrix in VMware | Microsoft Docs
description: Deze tweede zelfstudie in de reeks voor virtuele StorSimple-matrix implementatie omvat het inrichten van een virtueel apparaat in VMware.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>StorSimple virtuele matrix - inrichten in VMware implementeren
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Overzicht
Deze zelfstudie wordt beschreven hoe tooprovision en maak verbinding tooa virtuele StorSimple-matrix op een hostsysteem met VMware ESXi 5.5 en hoger. In dit artikel is van toepassing toohello implementatie van virtuele StorSimple-matrices in Azure portal en Hallo Microsoft Azure Government Cloud.

U moet administrator-bevoegdheden tooprovision en verbinding maken met het virtuele apparaat tooa. Hallo inrichting en de initiële installatie kan toocomplete van ongeveer 10 minuten duren.

## <a name="provisioning-prerequisites"></a>Vereiste onderdelen inrichten
Hallo vereisten tooprovision een virtueel apparaat op een hostsysteem met VMware ESXi 5.5 en hierboven zijn als volgt.

### <a name="for-hello-storsimple-device-manager-service"></a>Voor Hallo StorSimple-apparaat Manager-service
Zorg voordat u begint voor het volgende:

* U hebt alle Hallo stappen in [voorbereiden Hallo portal voor virtuele StorSimple-matrix](storsimple-virtual-array-deploy1-portal-prep.md).
* U hebt de installatiekopie van een virtueel apparaat Hallo voor VMware van hello Azure-portal gedownload. Zie voor meer informatie **stap 3: afbeelding voor het virtuele apparaat downloaden Hallo** van [voorbereiden Hallo-portal voor virtuele StorSimple-matrix handleiding](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Voor Hallo virtuele StorSimple-apparaat
Voordat u een virtueel apparaat implementeert, zorg ervoor dat:

* U hebt toegang tot tooa-hostsysteem met Hyper-V (2008 R2 of hoger) dat kan worden gebruikt tooa inrichten met een apparaat.
* Hallo-hostsysteem is kunnen toodedicate Hallo na tooprovision resources van uw virtuele apparaat:

  * Een minimum van 4 kernen.
  * Ten minste 8 GB aan RAM-geheugen. Als u van plan tooconfigure Hallo virtuele matrix als bestandsserver bent, ondersteunt 8 GB minder dan 2 miljoen bestanden. U moet 16 GB RAM-geheugen toosupport 2-4 miljoen bestanden.
  * Één netwerkinterface.
  * 500 GB virtuele schijf voor systeemgegevens.

### <a name="for-hello-network-in-datacenter"></a>Voor Hallo-netwerk in het datacenter
Zorg voordat u begint voor het volgende:

* U hebt doorgenomen Hallo netwerken vereisten toodeploy een virtueel StorSimple-apparaat en het geconfigureerde Hallo datacenternetwerk volgens Hallo vereisten. 

## <a name="step-by-step-provisioning"></a>Stapsgewijze inrichten
tooprovision en tooa virtueel apparaat verbinding maakt, moet u tooperform Hallo stappen te volgen:

1. Zorg ervoor dat het hostsysteem Hallo voldoende bronnen toomeet Hallo virtueel apparaat minimale vereisten.
2. Een virtueel apparaat in uw hypervisor inrichten.
3. Hallo virtueel apparaat starten en Hallo IP-adres.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Stap 1: Voldoe hostsysteem voldoet aan de vereisten voor minimale virtuele apparaten
een virtueel apparaat toocreate, moet u het:

* Toegang tooa-hostsysteem met VMware ESXi Server 5.5 en hoger.
* VMware vSphere client op uw systeem toomanage hello ESXi-host.

  * Een minimum van 4 kernen.
  * Ten minste 8 GB aan RAM-geheugen. Als u van plan tooconfigure Hallo virtuele matrix als bestandsserver bent, ondersteunt 8 GB minder dan 2 miljoen bestanden. U moet 16 GB RAM-geheugen toosupport 2-4 miljoen bestanden.
  * Netwerkinterfaces verbonden toohello geschikt is voor routering verkeer tooInternet. Hallo minimumbandbreedte Internet moet 5 Mbps tooallow voor optimale werking van Hallo-apparaat.
  * Een 500 GB virtuele schijf voor gegevens.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Stap 2: Een virtueel apparaat in de hypervisor inrichten
Volgende stappen tooprovision een virtueel apparaat in uw hypervisor Hallo uitvoeren.

1. Kopieer Hallo virtueel apparaat afbeelding op uw systeem. U hebt deze installatiekopie van het virtuele via hello Azure-portal hebt gedownload.

   1. Zorg ervoor dat u de meest recente installatiekopiebestand Hallo hebt gedownload. Als u de installatiekopie van het Hallo eerder hebt gedownload, het opnieuw downloaden tooensure die u hebt de meest recente afbeelding Hallo. de meest recente afbeelding Hallo heeft twee bestanden (in plaats van een).
   2. Noteer Hallo locatie waar u Hallo installatiekopie gekopieerd als u deze installatiekopie verderop in Hallo procedure gebruikt.

2. Meld u bij toohello ESXi-server met behulp van Hallo vSphere client. U moet toohave administrator-bevoegdheden toocreate een virtuele machine.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. Selecteer in de Hallo vSphere client in Hallo inventaris sectie in het linkerdeelvenster Hallo Hallo ESXi-Server.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Hallo VMDK toohello ESXi server uploaden. Navigeer toohello **configuratie** tabblad in het rechter deelvenster Hallo. Onder **Hardware**, selecteer **opslag**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. In Hallo rechtermuisknop deelvenster onder **Datastores**, selecteer Hallo datastore waar u tooupload hello VMDK. Hallo datastore moet voldoende beschikbare ruimte voor Hallo besturingssysteem en gegevensschijven hebben.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Met de rechtermuisknop en selecteer **bladeren Datastore**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. Een **Datastore Browser** venster wordt weergegeven.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Klik in de werkbalk hello, ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) pictogram toocreate een nieuwe map. Geef Hallo mapnaam op en noteer deze. U gebruikt deze mapnaam later bij het maken van een virtuele machine (aanbevolen best practice). Klik op **OK**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Hallo nieuwe map wordt weergegeven in het linkerdeelvenster van Hallo Hallo **Datastore Browser**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Klik op Hallo uploaden pictogram ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) en selecteer **-bestand uploaden**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Bladeren en wijst u toohello VMDK-bestanden die u hebt gedownload. Er zijn twee bestanden. Selecteer een bestand tooupload.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Klik op **Open**. Hallo uploaden van Hallo VMDK-bestand toohello opgegeven datastore wordt gestart. Het kan enkele minuten duren voordat Hallo bestand tooupload.
13. Nadat het Hallo uploaden is voltooid, ziet u Hallo-bestand in het gegevensarchief Hallo in Hallo-map die u hebt gemaakt.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Nu uploaden Hallo tweede VMDK-bestand toohello hetzelfde gegevensarchief.
14. Venster van toohello vSphere client retourneren. Met ESXi-server is geselecteerd, klik met de rechtermuisknop en selecteer **nieuwe virtuele Machine**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. Een **nieuwe virtuele Machine maken** venster weergegeven. Op Hallo **configuratie** pagina, selecteer Hallo **aangepaste** optie. Klik op **Volgende**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. Op Hallo **naam en locatie** pagina, geeft u Hallo-naam van uw virtuele machine. Deze naam moet overeenkomen met de Hallo mapnaam (aanbevolen) die u eerder in stap 8 hebt opgegeven.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. Op Hallo **opslag** pagina, selecteert u een gegevensarchief gewenste toouse tooprovision uw virtuele machine.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. Op Hallo **versie van de virtuele Machine** pagina **versie van de virtuele Machine: 8**. Versie 8 too11 worden alle ondersteund.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. Op Hallo **gastbesturingssysteem** pagina, selecteer Hallo **gastbesturingssysteem** als **Windows**. Voor **versie**, selecteert u in de vervolgkeuzelijst hello, **Microsoft Windows Server 2012 (64-bits)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. Op Hallo **CPU's** pagina, Hallo aanpassen **aantal virtuele sockets** en **aantal kernen per virtuele socket** zodat die Hallo **totaal aantal kernen**is 4 (of meer). Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. Op Hallo **geheugen** pagina, geeft u 8 GB (of meer) RAM-geheugen. Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. Op Hallo **netwerk** pagina, geef het aantal netwerkinterfaces Hallo Hallo. Hallo minimumvereiste is één netwerkinterface.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. Op Hallo **SCSI-Controller** pagina, accepteer de standaardinstelling Hallo **LSI Logic SAS-controller**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. Op Hallo **selecteert u een schijf** pagina **gebruik een bestaande virtuele schijf**. Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. Op Hallo **bestaande schijf selecteren** pagina onder **schijf bestandspad**, klikt u op **Bladeren**. Hiermee opent u een **Datastores Bladeren** dialoogvenster. Navigeer toohello locatie waar u Hallo VMDK geüpload. U ziet nu slechts één bestand in het gegevensarchief Hallo zoals Hallo twee bestanden die u in eerste instantie geüpload zijn samengevoegd. Selecteer Hallo-bestand en klik op **OK**. Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. Op Hallo **geavanceerde opties** pagina, accepteer de standaardinstelling Hallo en klikt u op **volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. Op Hallo **gereed tooComplete** controleert u alle Hallo-instellingen die zijn gekoppeld aan de nieuwe virtuele machine Hallo. Controleer **bewerken van instellingen van de virtuele machine Hallo voor voltooiing**. Klik op **gaan**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. Op Hallo **eigenschappen van virtuele Machines** pagina in Hallo **Hardware** tabblad, zoek Hallo apparaat hardware. Selecteer **nieuwe vaste schijf**. Klik op **Add**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. U ziet een **Hardware toevoegen** venster. Op Hallo **apparaattype** pagina onder **Kies Hallo type apparaat dat u wenst dat tooadd**, selecteer **harde schijf**, en klik op **volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. Op Hallo **selecteert u een schijf** pagina **een nieuwe virtuele schijf maken**. Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. Op Hallo **maken van een schijf** pagina, wijzigt u Hallo **schijfgrootte** too500 GB (of meer). 500 GB is de minimale vereiste hello, kunt u altijd inrichten op een grotere schijf. Houd er rekening mee dat u niet kunt vergroten of te Hallo schijf eenmaal ingericht verkleinen. Bekijk voor meer informatie over Hallo grootte van de schijf tooprovision Hallo sizing sectie in Hallo [best practices document](storsimple-ova-best-practices.md). Onder **schijf inrichting**, selecteer **Thin provisioning**. Klik op **Volgende**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. Op Hallo **geavanceerde opties** pagina, accepteer de standaardinstelling Hallo.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. Op Hallo **gereed tooComplete** pagina, bekijkt hello schijfopties. Klik op **Voltooien**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Pagina van de eigenschappen van de virtuele Machine toohello retourneren. Een nieuwe harde schijf wordt tooyour virtuele machine toegevoegd. Klik op **Voltooien**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Navigeer met uw virtuele machine wordt geselecteerd in het rechterdeelvenster hello, toohello **samenvatting** tabblad. Hallo-instellingen voor uw virtuele machine bekijken.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

De virtuele machine is nu ingericht. de volgende stap Hallo toopower op deze machine is en Hallo IP-adres.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Stap 3: Hallo virtueel apparaat starten en u Hallo IP-adres
Volgende stappen toostart Hallo uw virtuele apparaat uitvoeren en maak verbinding tooit.

#### <a name="toostart-hello-virtual-device"></a>toostart hello virtueel apparaat
1. Hallo virtueel apparaat starten. Selecteer het apparaat in Hallo vSphere Configuration Manager in het linkerdeelvenster Hallo en met de rechtermuisknop op toobring up Hallo contextmenu. Selecteer **Power** en selecteer vervolgens **inschakelen**. Dit moet de virtuele machine inschakelen. U kunt Hallo status bekijken in de onderste Hallo **recente taken** deelvenster van Hallo vSphere client.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. Hallo-instellingstaken duurt een paar minuten toocomplete. Nadat de Hallo-apparaat wordt uitgevoerd, gaat u toohello **Console** tabblad. Ctrl + Alt + Delete toolog in toohello apparaat verzenden. U kunt ook verwijzen Hallo cursor in het consolevenster Hallo en druk op Ctrl + Alt + Insert. Hallo standaardgebruiker is *StorSimpleAdmin* en is het standaardwachtwoord Hallo *Wachtwoord1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Uit veiligheidsoverwegingen verloopt beheerderswachtwoord Hallo-apparaat bij de eerste aanmelding Hallo. U bent na vragen aan gebruiker toochange Hallo wachtwoord.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Voer een wachtwoord dat ten minste 8 tekens bevat. Hallo-wachtwoord moet bevatten 3 van 4 van deze vereisten voldoet: hoofdletters, kleine letters, numerieke en speciale tekens. Hallo wachtwoord tooconfirm opnieuw het. U wordt gewaarschuwd dat Hallo-wachtwoord is gewijzigd.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Nadat het Hallo-wachtwoord is gewijzigd, kunnen Hallo virtueel apparaat mogelijk opnieuw opgestart. Wachten op Hallo opnieuw opstarten toocomplete. Windows PowerShell-console Hallo Hallo apparaat mogelijk weergegeven samen met een voortgangsbalk.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. Stap 6-8 zijn alleen van toepassing wanneer in een omgeving met niet-DHCP-up wordt opgestart. Als u zich in een DHCP-omgeving, slaat u deze stappen over en gaat u toostep 9. Als u van uw apparaat in niet-DHCP-omgeving opgestart, ziet u Hallo scherm te volgen.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Configureer vervolgens Hallo-netwerk.
7. Gebruik Hallo `Get-HcsIpAddress` opdracht toolist Hallo-netwerkinterfaces is ingeschakeld op uw virtuele apparaat. Als uw apparaat één netwerkinterface is ingeschakeld heeft, de naam die is toegewezen Hallo-toothis standaardinterface is `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Gebruik Hallo `Set-HcsIpAddress` cmdlet tooconfigure Hallo netwerk. Een voorbeeld wordt hieronder weergegeven:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Nadat het Hallo eerste installatie is voltooid en Hallo apparaat is opgestart, ziet u bannertekst Hallo-apparaat. Noteer Hallo IP-adres en Hallo-URL in Hallo banner tekst toomanage Hallo apparaat weergegeven. U gebruikt dit IP-adres tooconnect toohello webgebruikersinterface van uw virtuele apparaat en volledige Hallo lokale installatie en registratie.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Optioneel) Deze stap alleen uitvoeren als u uw apparaat bij Hallo Government Cloud implementeert. U kunt nu Hallo Verenigde Staten Federal Information Processing Standard (FIPS) modus op uw apparaat. Hallo FIPS 140-standaard definieert cryptografische algoritmen die zijn goedgekeurd voor gebruik door ons Federal government computersystemen voor Hallo bescherming van gevoelige gegevens.

    1. tooenable hello FIPS-modus, Hallo volgende cmdlet uitvoeren:

        `Enable-HcsFIPSMode`
    2. Start opnieuw op uw apparaat wanneer u Hallo FIPS-modus hebt ingeschakeld, zodat de cryptografische validaties Hallo van kracht.

       > [!NOTE]
       > U kunt inschakelen of uitschakelen van FIPS-modus op uw apparaat. Wisselende Hallo apparaat tussen FIPS- en niet FIPS-modus wordt niet ondersteund.
       >
       >

Als uw apparaat voldoet niet aan de minimale configuratievereisten hello, ziet u een fout in Hallo bannertekst (Zie hieronder). U moet toomodify Hallo apparaatconfiguratie zodat er voldoende bronnen toomeet Hallo minimale vereisten voldoet. U kunt vervolgens opnieuw opstarten en toohello apparaat aansluit. Raadpleeg de minimale configuratievereisten voor toohello in [stap 1: Zorg ervoor dat Hallo hostsysteem aan de minimale virtueel apparaat voldoet](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Als u een andere fout tijdens de eerste configuratie Hallo Hallo lokale webgebruikersinterface met geconfronteerd, raadpleegt u toohello werkstromen te volgen:

* Diagnostische tests uit te voeren[web UI setup oplossen](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Logboek pakket genereren en logboekbestanden weergeven](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Volgende stappen
* [Uw virtuele StorSimple-matrix instellen als bestandsserver](storsimple-virtual-array-deploy3-fs-setup.md)
* [Uw virtuele StorSimple-matrix ingesteld als een iSCSI-server](storsimple-virtual-array-deploy3-iscsi-setup.md)

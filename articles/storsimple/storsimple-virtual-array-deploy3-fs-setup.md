---
title: aaaSet up virtuele StorSimple-matrix als bestandsserver | Microsoft Docs
description: "Deze derde zelfstudie in de implementatie van virtuele StorSimple-matrix geïnstrueerd tooset van een virtueel apparaat als bestandsserver."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: f609f6ff-0927-48bb-a68a-6d8985d2fe34
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/17/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 89cade37980f342695c0adee42c4ade0e1d53d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---set-up-as-file-server-via-azure-portal"></a>Implementeer matrix van de virtuele StorSimple - Set up als bestandsserver via Azure portal
![](./media/storsimple-virtual-array-deploy3-fs-setup/fileserver4.png)

## <a name="introduction"></a>Inleiding
Dit artikel wordt beschreven hoe de initiële installatie tooperform, registreren van uw StorSimple-bestandsserver Apparaatinstelling voltooien hello, en maken en koppelen tooSMB shares. Dit is Hallo laatste van het artikel in Hallo reeks zelfstudies voor implementatie vereist toocompletely uw virtuele matrix implementeren als een bestandsserver of een iSCSI-server.

Hallo-installatie- en configuratieproces kan toocomplete van ongeveer 10 minuten duren. Hallo-informatie in dit artikel is van toepassing alleen toohello implementatie van Hallo virtuele StorSimple-matrix. Hallo-implementatie van StorSimple 8000 series apparaten, gaat u naar: [StorSimple 8000 series apparaat met Update 2 implementeren](storsimple-deployment-walkthrough-u2.md).

## <a name="setup-prerequisites"></a>Vereisten voor installatie
Voordat u configureren en van uw virtuele StorSimple-matrix instellen, zorg ervoor dat:

* U hebt ingericht, een virtuele matrix is en verbonden tooit als gedetailleerde in Hallo [inrichten van een virtueel StorSimple-matrix in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) of [inrichten van een virtueel StorSimple-matrix in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
* U hebt de serviceregistratiesleutel Hallo van Hallo Apparaatbeheer StorSimple-service die u hebt een virtueel StorSimple-matrices toomanage gemaakt. Zie voor meer informatie [stap 2: Get Hallo serviceregistratiesleutel](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) voor virtuele StorSimple-matrix.
* Als dit Hallo tweede of volgende virtuele matrix dat u met een bestaande Apparaatbeheer StorSimple-service registreren wilt, moet u de gegevensversleutelingssleutel van Hallo service hebben. Deze sleutel is gegenereerd nadat Hallo eerste apparaat is geregistreerd met deze service. Als u deze sleutel hebt verloren, Zie [Get Hallo service gegevensversleutelingssleutel](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) voor uw virtuele StorSimple-matrix.

## <a name="step-by-step-setup"></a>Stapsgewijze setup
Gebruik Hallo tooset voor stapsgewijze instructies opvolgen en configureren van uw virtuele StorSimple-matrix.

## <a name="step-1-complete-hello-local-web-ui-setup-and-register-your-device"></a>Stap 1: Hallo lokale web UI-installatie te voltooien en Registreer uw apparaat
#### <a name="toocomplete-hello-setup-and-register-hello-device"></a>toocomplete Hallo setup en Hallo-apparaat registreren
1. Open een browservenster en maak verbinding toohello lokale webgebruikersinterface. Type:
   
   `https://<ip-address of network interface>`
   
   Gebruik Hallo verbindings-URL in de vorige stap Hallo hebt genoteerd. Ziet u een foutbericht dat aangeeft dat er een probleem met het beveiligingscertificaat Hallo-website is. Klik op **toothis webpagina gaan**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image2.png)
2. Meld u aan toohello-webgebruikersinterface van uw virtuele matrix als **StorSimpleAdmin**. Voer beheerderswachtwoord van het Hallo-apparaat die u hebt gewijzigd in stap 3: begin Hallo virtuele matrix in [inrichten van een virtueel StorSimple-matrix in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) of in [inrichten van een virtueel StorSimple-matrix in VMware](storsimple-virtual-array-deploy2-provision-vmware.md).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image3.png)
3. Gaat u toohello **Start** pagina. Deze pagina beschrijft Hallo verschillende instellingen die vereist zijn tooconfigure en registreer Hallo virtuele matrix met Hallo Apparaatbeheer StorSimple-service. Hallo **instellingen**, **Web proxy-instellingen**, en **tijdinstellingen** zijn optioneel. alleen instellingen zijn vereist Hallo **apparaatinstellingen** en **Cloudinstellingen**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image4.png)
4. In Hallo **instellingen** pagina onder **netwerkinterfaces**, DATA 0 wordt automatisch voor u geconfigureerd. Elke netwerkinterface wordt ingesteld met standaard tooget IP-adres automatisch (DHCP). Een IP-adres, subnetmasker en gateway worden daarom automatisch toegewezen (voor IPv4 en IPv6).
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image5.png)
   
   Als u meer dan één netwerkinterface tijdens het Hallo inrichten van Hallo-apparaat hebt toegevoegd, kunt u ze hier configureren. Houd er rekening mee dat kunt u de netwerkinterface configureren als IPv4 alleen of als zowel IPv4 als IPv6. Alleen IPv6-configuraties worden niet ondersteund.
5. DNS-servers zijn vereist, omdat ze worden gebruikt wanneer uw apparaat toocommunicate met uw cloudserviceproviders opslag of tooresolve probeert uw apparaat met de naam wanneer geconfigureerd als een bestandsserver. In Hallo **instellingen** pagina onder Hallo **DNS-servers**:
   
   1. Een primaire en secundaire DNS-server worden automatisch geconfigureerd. Als u tooconfigure statische IP-adressen kiest, kunt u DNS-servers. U wordt aangeraden dat u een primaire en secundaire DNS-server configureren voor hoge beschikbaarheid.
   2. Klik op **toepassen** tooapply en netwerkinstellingen hello te valideren.
6. In Hallo **apparaatinstellingen** pagina:
   
   1. Wijs een uniek **naam** tooyour apparaat. Deze naam mag 1-15 tekens lang zijn en mag letter, cijfers en afbreekstreepjes bevatten.
   2. Klik op Hallo **bestandsserver** pictogram ![](./media/storsimple-virtual-array-deploy3-fs-setup/image6.png) voor Hallo **Type** van apparaten die u maakt. Een bestandsserver kunt u toocreate gedeelde mappen.
   3. Als het apparaat een bestandsserver is, moet u toojoin Hallo apparaat tooa domein. Voer een **domeinnaam**.
   4. Klik op **Toepassen**.
7. Een dialoogvenster wordt weergegeven. Geef uw domeinreferenties in de opgegeven indeling Hallo. Klik op het vinkje Hallo. Hallo domeinreferenties worden geverifieerd. U ziet een foutbericht weergegeven als Hallo referenties onjuist zijn.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image7.png)
8. Klik op **Toepassen**. Hiermee wordt de van toepassing en Hallo apparaatinstellingen valideren.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image8.png)
   
   > [!NOTE]
   > Zorg ervoor dat uw virtuele matrix in de eigen organisatie-eenheid (OE) voor Active Directory en geen groepsbeleidsobjecten (GPO), toegepaste tooit zijn of zijn overgenomen. Groepsbeleid mag toepassingen zoals antivirussoftware installeren op Hallo virtuele StorSimple-matrix. Extra software te installeren, wordt niet ondersteund en toodata beschadiging kan leiden. 
   > 
   > 
9. (Optioneel) uw webproxyserver configureren. Hoewel webproxyconfiguratie optioneel is, worden op de hoogte gebracht als u een webproxy gebruikt, u alleen deze hier configureren kunt.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image9.png)
   
   In Hallo **Web proxy** pagina:
   
   1. Geef Hallo **Web-URL voor proxy** in deze indeling: *http://&lt;host-IP-adres of FDQN&gt;: poortnummer*. Houd er rekening mee dat HTTPS-URL's worden niet ondersteund.
   2. Geef **verificatie** als **Basic** of **geen**.
   3. Als u gebruikmaakt van verificatie, moet u ook tooprovide een **gebruikersnaam** en **wachtwoord**.
   4. Klik op **Toepassen**. Hiermee wordt valideren en Hallo geconfigureerd web proxy-instellingen toegepast.
10. (Optioneel) Configureer Hallo tijdinstellingen voor uw apparaat, zoals tijdzone en Hallo primaire en secundaire NTP-servers. NTP-servers zijn vereist, omdat uw apparaat de tijd synchroniseren moet zodat verificatie met uw cloudserviceproviders.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/image10.png)
    
    In Hallo **tijdinstellingen** pagina:
    
    1. Selecteer in de vervolgkeuzelijst Hallo Hallo **tijdzone** op basis van de geografische locatie Hallo in welke Hallo apparaat wordt geïmplementeerd. Hallo standaardtijdzone voor uw apparaat is PST. Het apparaat zal deze tijdzone gebruiken voor alle geplande bewerkingen.
    2. Geef een **primaire NTP-server** voor uw apparaat of accepteer de standaardwaarde Hallo van time.windows.com. Zorg ervoor dat uw netwerk NTP-verkeer toopass van uw datacenter toohello Internet toestaat.
    3. Geef desgewenst een **secundaire NTP-server** voor uw apparaat.
    4. Klik op **Toepassen**. Zo valideren en past u tijdinstellingen Hallo geconfigureerd.
11. Hallo cloudinstellingen configureren voor uw apparaat. In deze stap maakt u Hallo lokale apparaatconfiguratie voltooien en vervolgens Hallo-apparaat registreren bij uw StorSimple-apparaat Manager-service.
    
    1. Voer Hallo **serviceregistratiesleutel** die u hebt verkregen [stap 2: Get Hallo serviceregistratiesleutel](storsimple-virtual-array-deploy1-portal-prep.md#step-2-get-the-service-registration-key) voor virtuele StorSimple-matrix.
    2. Als dit het eerste apparaat registreren bij deze service, u krijgt Hallo **gegevensversleutelingssleutel van Service**. Kopieer deze sleutel en bewaar deze op een veilige plaats. Deze sleutel is vereist bij het Hallo-service registratie sleutel tooregister extra apparaten Hello StorSimple-apparaat Manager-service. 
       
       Als dit geen eerste Hallo-apparaat dat u met deze service registreren is wilt, moet u tooprovide Hallo service gegevensversleutelingssleutel. Raadpleeg voor meer informatie, tooget hello [gegevensversleutelingssleutel van service](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) op uw lokale webgebruikersinterface.
    3. Klik op **registreren**. Dit wordt opnieuw opgestart Hallo-apparaat. U moet mogelijk toowait 2-3 minuten voordat het Hallo-apparaat is geregistreerd. Nadat het Hallo-apparaat opnieuw is opgestart, gaat u toohello aanmelding op de pagina.
       
       ![](./media/storsimple-virtual-array-deploy3-fs-setup/image13.png)
12. Azure-portal toohello retourneren. Ga te**alle resources**, zoeken naar uw StorSimple-apparaat Manager-service.
    
    ![](./media/storsimple-virtual-array-deploy3-fs-setup/searchdevicemanagerservice1.png) 
13. Hallo gefilterde lijst, selecteer uw StorSimple-apparaat Manager-service en blader vervolgens te**Management > apparaten**. In Hallo **apparaten** blade Hallo apparaat verbinding heeft met toohello service en heeft Hallo status controleren **tooset gereed**.
    
    ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png)

## <a name="step-2-configure-hello-device-as-file-server"></a>Stap 2: Hallo-apparaat als bestandsserver configureren
Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/) toocomplete Hallo Apparaatinstelling vereist.

#### <a name="tooconfigure-hello-device-as-file-server"></a>tooconfigure hello apparaat als bestandsserver
1. Ga tooyour Apparaatbeheer StorSimple-service en ga vervolgens te **Management > apparaten**. In Hallo **apparaten** blade, selecteer Hallo-apparaat die u zojuist hebt gemaakt. Dit apparaat wordt weergegeven als **tooset gereed**.
   
   ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs2m.png) 
2. Klik op Hallo-apparaat en u een bannerbericht te zien die aangeeft dat het Hallo-apparaat klaar toosetup.
   
    ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs3m.png)
3. Klik op **configureren** op Hallo opdrachtbalk klikken. Hiermee opent u up Hallo **configureren** blade. In Hallo **configureren** blade Hallo te volgen:
   
    1. naam van de bestandsserver Hello wordt automatisch gevuld.
    
    2. Zorg ervoor dat de versleuteling van cloudopslag hello te is ingesteld**ingeschakeld**. Hiermee wordt alle Hallo gegevens versleutelen die toohello cloud wordt verzonden. 
    
    3. Een AES 256-bits sleutel wordt gebruikt met de gebruiker gedefinieerde Hallo-sleutel voor versleuteling. Een sleutel 32 tekens opgeven en vervolgens een sleutel tooconfirm Hallo deze. Record Hallo sleutel in een app Sleutelbeheer voor toekomstig gebruik.
    
    4. Klik op **vereiste instellingen configureren** toospecify storage-account referenties toobe gebruikt met uw apparaat. Klik op **nieuwe toevoegen** of er geen opslagaccountreferenties geconfigureerd zijn. **Zorg ervoor dat Hallo storage account dat u gebruikt ondersteuning biedt voor blok-blobs. Pagina-blobs worden niet ondersteund.** Meer informatie over [blobs en pagina-blobs geblokkeerd](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs).
   
    ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs6m.png) 
4. In Hallo **toevoegen van een opslagaccountreferenties** blade Hallo te volgen: 

    1. Huidige abonnement kiezen als Hallo storage-account in Hallo hetzelfde abonnement als Hallo-service. Geef andere Hallo opslag is account bevindt zich buiten het Hallo-service-abonnement. 
    
    2. Kies in de vervolgkeuzelijst hello, een bestaand opslagaccount. 
    
    3. Hallo locatie automatisch ingevuld op basis van opgegeven Hallo storage-account. 
    
    4. Schakel SSL tooensure een beveiligd netwerk communicatiekanaal tussen Hallo-apparaat en Hallo cloud.
    
    5. Klik op **toevoegen** tooadd deze opslag account referentie. 
   
        ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs8m.png)

5. Als Hallo storage-account-referentie is gemaakt, Hallo **configureren** blade wordt bijgewerkt toodisplay hello opslagaccountreferenties opgegeven. Klik op **Configureren**
   
   ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs11m.png)
   
   U ziet een dat een bestand server wordt gemaakt. Als de bestandsserver Hallo is gemaakt, wordt u gewaarschuwd.
   
   ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs13m.png)
   
   de apparaatstatus Hello, wijzigt u ook te**Online**.
   
   ![Een bestandsserver configureren](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs14m.png)
   
   U kunt doorgaan tooadd een share.

## <a name="step-3-add-a-share"></a>Stap 3: Een share toevoegen
Uitvoeren van de stappen te volgen in Hallo Hallo [Azure-portal](https://portal.azure.com/) toocreate een share.

#### <a name="toocreate-a-share"></a>toocreate een share
1. Selecteer Hallo bestand server apparaat dat u hebt geconfigureerd in de voorgaande stap Hallo en klikt u op **...**  (of met de rechtermuisknop op). Selecteer in het contextmenu hello, **toevoegen share**. U kunt ook klikken op **+ bestandsshare toevoegen** op Hallo apparaat opdrachtbalk klikken.
   
   ![Share toevoegen](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs15m.png)
2. Geef Hallo instellingen voor delen te volgen:

    1. Een unieke naam voor de share. Hallo-naam moet een tekenreeks die 3 too127 tekens bevat.
    
    2. Een optionele **beschrijving** voor Hallo-share. Hallo beschrijving kunt identificeren Hallo eigenaren van de bestandsshare.
    
    3. Een **Type** voor Hallo-share. Hallo-type kan worden **tiers verdeelde** of **lokaal vastgemaakt**, met gelaagde wordt standaard Hallo. Voor workloads waarvoor lokale garanties, lage latenties en betere prestaties, selecteer een **lokaal vastgemaakt** delen. Voor alle overige gegevens selecteert u een **tiers verdeelde** delen.
    Een lokaal vastgemaakt share is compact ingericht en zorgt ervoor dat de primaire gegevens op de share Hallo Hallo lokale toohello apparaat blijft en komt niet toohello cloud worden gelekt. Een gelaagde share op Hallo is daarentegen dun ingericht. Bij het maken van een gelaagde share 10% van Hallo ruimte is ingericht op de lokale laag Hallo en 90% van Hallo ruimte in de cloud Hallo is ingericht. Hallo bijvoorbeeld gegevenslagen op als u een volume 1 TB ingericht, 100 GB zou bevinden zich in de lokale ruimte Hallo en 900 GB wordt gebruikt in de cloud Hallo wanneer. Dit betekent op zijn beurt als u geen alle Hallo lokale ruimte meer op Hallo apparaat uitvoert, kunt u een gelaagde share kan niet inrichten.
   
    4. In Hallo **standaard volledige machtigingen ingesteld op** veld, Hallo machtigingen toohello gebruiker of groep Hallo die toegang heeft tot deze share toewijzen. Hallo naam opgeven van Hallo-gebruiker of groep in Hallo  *john@contoso.com*  indeling. Het is raadzaam dat u een gebruiker groep (in plaats van een enkele gebruiker) tooallow admin bevoegdheden tooaccess deze shares. Nadat u hier Hallo machtigingen hebt toegewezen, klikt u vervolgens kunt u Windows Verkenner toomodify deze machtigingen.
   
    5. Klik op **toevoegen** toocreate Hallo share. 
    
        ![Share toevoegen](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs18m.png)
   
        U wordt gewaarschuwd dat Hallo share gemaakt wordt.
   
        ![Share toevoegen](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs19m.png)
   
    Nadat het Hallo-share is gemaakt met de Hallo opgegeven instellingen hello **Shares** blade tooreflect Hallo nieuwe share wordt bijgewerkt. Controle- en back-up zijn standaard ingeschakeld voor Hallo-share.
   
    ![Share toevoegen](./media/storsimple-virtual-array-deploy3-fs-setup/deployfs22m.png)

## <a name="step-4-connect-toohello-share"></a>Stap 4: Verbinding maken met share toohello
U moet nu tooconnect tooone of meer shares die u hebt gemaakt in de vorige stap Hallo. Deze stappen uitvoeren op uw Windows Server host verbonden tooyour virtuele StorSimple-matrix.

#### <a name="tooconnect-toohello-share"></a>tooconnect toohello share
1. Druk op ![](./media/storsimple-virtual-array-deploy3-fs-setup/image22.png) + R. Geef in het venster voor het uitvoeren van Hallo Hallo *&#92; &#92;&lt; naam van de bestandsserver&gt;*  als Hallo-pad vervangen *naam van de bestandsserver* met Hallo-apparaat een naam die u toegewezen tooyour bestandsserver. Klik op **OK**.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image23.png)
2. Hiermee opent u Windows Verkenner. Nu moet u kunnen toosee Hallo shares die u hebt gemaakt als de mappen. Selecteer en dubbelklik op een share (map) tooview Hallo-inhoud.
   
   ![](./media/storsimple-virtual-array-deploy3-fs-setup/image24.png)
3. Nu kunt u bestandsshares toothese toevoegen en maak een back-up.

## <a name="next-steps"></a>Volgende stappen
Meer informatie over hoe Hallo toouse lokale webgebruikersinterface te[beheren van uw virtuele StorSimple-matrix](storsimple-ova-web-ui-admin.md).


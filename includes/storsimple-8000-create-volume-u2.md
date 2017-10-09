<!--author=alkohli last changed: 07/19/2017-->

#### <a name="toocreate-a-volume"></a>een volume toocreate
1. Uit in tabelvorm aanbieding van apparaten in Hallo HALLO hallo **apparaten** blade, selecteer uw apparaat. Klik op **Volume toevoegen**.

    ![Een nieuw volume toevoegen](./media/storsimple-8000-create-volume-u2/step5createvol1.png)

2. In Hallo **toevoegen van een volume** blade:
   
   1. Hallo **Selecteer welk apparaat** veld wordt automatisch gevuld met uw huidige apparaat.

   2. Selecteer in de vervolgkeuzelijst hello, Hallo volumecontainer wanneer u een volume tooadd nodig. 

   3.  een **naam** voor het volume. U kunt de naam van een volume niet wijzigen zodra Hallo volume is gemaakt.

   4. Selecteer op de vervolgkeuzelijst hello, Hallo **Type** voor het volume. Voor workloads waarvoor lokale garanties, lage latenties en betere prestaties vereist zijn, selecteert u een **lokaal vastgemaakt** volume. Voor alle overige gegevens selecteert u een **gelaagd** volume. Als u dit volume gebruikt voor de archivering van gegevens, schakelt u **Dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** in.
      
       Een gelaagd volume is dun ingericht (thin provisioning) en kan zeer snel worden gemaakt. Selecteren **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** voor gelaagde volume gericht voor archivering van gegevens wijzigingen Hallo Ontdubbeling chunkgrootte voor het volume too512 KB. Als dit veld niet is ingeschakeld, gebruikt Hallo overeenkomstige gelaagde volume een chunkgrootte van 64 KB. Een grotere chunkgrootte voor Ontdubbeling kunt Hallo apparaat tooexpedite Hallo overdracht van grote hoeveelheden gegevens voor archivering toohello cloud.
       
       Een lokaal vastgemaakt volume is compact ingericht en zorgt ervoor dat de primaire gegevens op Hallo volume Hallo lokale toohello apparaat blijft en komt niet toohello cloud worden gelekt.  Als u een lokaal vastgemaakt volume maakt, Hallo-apparaat controleert op beschikbare ruimte op de lokale lagen Hallo tooprovision Hallo volume Hallo aangevraagde grootte. Hallo-bewerking voor het maken van een lokaal vastgemaakt volume heeft als risico dat bestaande gegevens uit Hallo apparaat toohello cloud kan inhouden en Hallo tijd toocreate Hallo volume mogelijk lang. Hallo totale tijd is afhankelijk van Hallo grootte van het volume Hallo ingericht, beschikbare netwerkbandbreedte en Hallo gegevens op uw apparaat.

   5. Geef Hallo **ingerichte capaciteit** voor het volume. Noteer Hallo capaciteit die beschikbaar is op basis van Hallo volume dat is geselecteerd. Hallo opgegeven volumegrootte mag niet groter zijn dan Hallo beschikbare ruimte.
      
       U kunt lokaal vastgemaakte volumes tot too8.5 TB en gelaagde volumes van too200 TB op Hallo 8100-apparaat inrichten. U kunt lokaal vastgemaakte volumes tot too22.5 TB en gelaagde volumes van too500 TB inrichten op Hallo groter 8600-apparaat. Aangezien lokale ruimte op Hallo apparaat vereist toohost Hallo werkset van gelaagde volumes, het maken van lokaal vastgemaakte volumes invloed is op Hallo beschikbare schijfruimte voor het inrichten van gelaagde volumes. Als u dus een lokaal vastgemaakt volume maakt, wordt de beschikbare schijfruimte voor het maken van gelaagde volumes verminderd. Als een gelaagd volume is gemaakt, wordt op dezelfde manier Hallo beschikbare ruimte voor het maken van lokaal vastgemaakte volumes verminderd.
      
       Als u een lokaal vastgemaakt volume van 8.5 TB (maximaal toegestane grootte) op uw 8100-apparaat inricht, hebt u alle Hallo lokale ruimte beschikbaar is op Hallo apparaat uitgeput. U kunt geen gelaagd volume kan niet maken vanaf dat moment of hoger als er geen lokale ruimte op Hallo apparaat toohost Hallo-werkset Hallo is gelaagd volume. Bestaande gelaagde volumes zijn ook van invloed op Hallo ruimte beschikbaar. Als u bijvoorbeeld een 8100-apparaat hebt met reeds gelaagde volumes van circa 106 TB, is er nog maar 4 TB ruimte beschikbaar voor lokaal vastgemaakte volumes.

    6. In Hallo **verbonden hosts** en klik op de pijl Hallo veld. 

        ![Verbonden hosts](./media/storsimple-8000-create-volume-u2/step5createvol2.png)

    7. In Hallo **verbonden hosts** blade, kiest u een bestaande ACR of Voeg een nieuwe ACR door Hallo volgende stappen uit te voeren:

       1. Geef een **naam** voor uw ACR op.
       2. Onder **iSCSI-initiatornaam**, bieden Hallo iSCSI Qualified Name (IQN) van uw Windows-host. Als u Hallo IQN niet hebt, gaat u verder te[Get Hallo IQN van een Windows Server-host](#get-the-iqn-of-a-windows-server-host).

    9. Klik op **Create**. Een volume wordt gemaakt met de Hallo opgegeven instellingen.

        ![Klik op Maken](./media/storsimple-8000-create-volume-u2/step5createvol3.png)

        > [!NOTE]
        > Let erop dat u hier hebt gemaakt Hallo-volume is niet beveiligd. U moet deze tootake geplande back-ups van volume toocreate en koppelen van de back-upbeleid. 


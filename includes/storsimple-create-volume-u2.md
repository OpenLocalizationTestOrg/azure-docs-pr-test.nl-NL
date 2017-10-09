<!--author=alkohli last changed: 08/16/2016-->

#### <a name="toocreate-a-volume"></a>een volume toocreate
1. Op Hallo apparaat **Quick Start** pagina, klikt u op **toevoegen van een volume** toostart Hallo wizard volume toevoegen.
2. In Hallo onder een wizard volume toevoegen **basisinstellingen**:
   
   1. een **naam** voor het volume.
   2. Selecteer op de vervolgkeuzelijst hello, Hallo **gebruikstype** voor het volume. Voor workloads waarvoor lokale garanties, lage latenties en betere prestaties vereist zijn, selecteert u een **lokaal vastgemaakt** volume. Voor alle overige gegevens selecteert u een **gelaagd** volume. Als u dit volume gebruikt voor de archivering van gegevens, schakelt u **Dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** in. 
      
       Een lokaal vastgemaakt volume is compact ingericht en zorgt ervoor dat de primaire gegevens op Hallo volume Hallo lokale toohello apparaat blijft en komt niet toohello cloud worden gelekt.  Als u een lokaal vastgemaakt volume maakt, Hallo-apparaat controleert op beschikbare ruimte op de lokale lagen Hallo tooprovision Hallo volume Hallo aangevraagde grootte. Hallo-bewerking voor het maken van een lokaal vastgemaakt volume heeft als risico dat bestaande gegevens uit Hallo apparaat toohello cloud kan inhouden en Hallo tijd toocreate Hallo volume mogelijk lang. Hallo totale tijd is afhankelijk van Hallo grootte van het volume Hallo ingericht, beschikbare netwerkbandbreedte en Hallo gegevens op uw apparaat. 
      
       Een gelaagd volume is dun ingericht (thin provisioning) en kan zeer snel worden gemaakt. Selecteren **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** voor gelaagde volume gericht voor archivering van gegevens wijzigingen Hallo Ontdubbeling chunkgrootte voor het volume too512 KB. Als dit veld niet is ingeschakeld, gebruikt Hallo overeenkomstige gelaagde volume een chunkgrootte van 64 KB. Een grotere chunkgrootte voor Ontdubbeling kunt Hallo apparaat tooexpedite Hallo overdracht van grote hoeveelheden gegevens voor archivering toohello cloud.
   3. Geef Hallo **ingerichte capaciteit** voor het volume. Noteer Hallo capaciteit die beschikbaar is op basis van Hallo volume dat is geselecteerd. Hallo opgegeven volumegrootte mag niet groter zijn dan Hallo beschikbare ruimte.
      
       U kunt lokaal vastgemaakte volumes tot too8.5 TB en gelaagde volumes van too200 TB op Hallo 8100-apparaat inrichten. U kunt lokaal vastgemaakte volumes tot too22.5 TB en gelaagde volumes van too500 TB inrichten op Hallo groter 8600-apparaat. Aangezien lokale ruimte op Hallo apparaat vereist toohost Hallo werkset van gelaagde volumes, het maken van lokaal vastgemaakte volumes invloed is op Hallo beschikbare schijfruimte voor het inrichten van gelaagde volumes. Als u dus een lokaal vastgemaakt volume maakt, wordt de beschikbare schijfruimte voor het maken van gelaagde volumes verminderd. Als een gelaagd volume is gemaakt, wordt op dezelfde manier Hallo beschikbare ruimte voor het maken van lokaal vastgemaakte volumes verminderd.
      
       Als u een lokaal vastgemaakt volume van 8.5 TB (maximaal toegestane grootte) op uw 8100-apparaat inricht, hebt u alle Hallo lokale ruimte beschikbaar is op Hallo apparaat uitgeput. U zich niet kunnen toocreate geen gelaagd volume van dat punt en hoger omdat er geen lokale ruimte op Hallo apparaat toohost Hallo-werkset Hallo is gelaagd volume. Bestaande gelaagde volumes zijn ook van invloed op Hallo ruimte beschikbaar. Als u bijvoorbeeld een 8100-apparaat hebt met reeds gelaagde volumes van circa 106 TB, is er nog maar 4 TB ruimte beschikbaar voor lokaal vastgemaakte volumes.
      
       Hallo volgende afbeelding toont Hallo **basisinstellingen** in het dialoogvenster voor een lokaal vastgemaakt volume.
      
        ![Lokaal volume toevoegen](./media/storsimple-create-volume-u2/add-local-volume-include.png)
      
       Hallo volgende afbeelding toont Hallo **basisinstellingen** in het dialoogvenster voor een gelaagd volume.
      
        ![Lokaal volume toevoegen](./media/storsimple-create-volume-u2/add-tiered-volume-include.png)
   
   1. Klik op het pijlpictogram Hallo ![pijltje](./media/storsimple-create-volume-u2/HCS_ArrowIcon-include.png) toogo toohello volgende pagina.
3. In Hallo **extra instellingen** dialoogvenster toevoegen van een nieuwe record voor toegangscontrole (ACR):
   
   1. Geef een **naam** voor uw ACR op.
   2. Onder **iSCSI-initiatornaam**, bieden Hallo iSCSI Qualified Name (IQN) van uw Windows-host. Als u Hallo IQN niet hebt, gaat u verder te[Get Hallo IQN van een Windows Server-host](#get-the-iqn-of-a-windows-server-host).
   3. Onder **standaardback-up voor dit volume?**, selecteer Hallo **inschakelen** selectievakje. Hallo standaardback-up wordt gemaakt van een beleid dat wordt uitgevoerd om 22.30 elke dag (tijd op het apparaat) en maakt een cloudmomentopname van dit volume.
      
      > [!NOTE]
      > Nadat Hallo back-up hier is ingeschakeld, kan niet worden teruggezet. U moet deze instelling tooedit Hallo volume toomodify.
      > 
      > 
      
      ![Volume toevoegen](./media/storsimple-create-volume-u2/AddVolumeAdditionalSettings1.png)
4. Klik op het vinkje Hallo ![vinkje](./media/storsimple-create-volume-u2/HCS_CheckIcon-include.png). Een volume wordt gemaakt met de Hallo opgegeven instellingen.


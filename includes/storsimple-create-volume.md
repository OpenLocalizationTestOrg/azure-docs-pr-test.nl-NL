<!--author=SharS last changed: 02/04/2016-->

#### <a name="toocreate-a-volume"></a>een volume toocreate
1. Op Hallo apparaat **Quick Start** pagina, klikt u op **toevoegen van een volume**. Hallo wizard volume toevoegen wordt gestart.
2. In Hallo onder een wizard volume toevoegen **basisinstellingen**, Hallo te volgen:
   
   1. Geef een **naam** op voor het volume.
   2. Geef Hallo **ingerichte capaciteit** voor het volume in GB of TB. Hallo volumecapaciteit moet liggen tussen 1 GB en 64 TB voor een fysiek apparaat.
   3. Selecteer op de vervolgkeuzelijst hello, Hallo **gebruikstype** voor het volume. 
   4. Als u dit volume voor archivering van gegevens gebruikt, selecteert u Hallo **dit volume gebruiken voor minder frequent gebruikte gearchiveerde gegevens** selectievakje. In alle andere gevallen schakelt u **Gelaagd volume** in. (Gelaagde volumes werden voorheen primaire volumes genoemd.)
      
        ![Volume toevoegen](./media/storsimple-create-volume/ScreenshotUpdate1VolumeFlow.png)
      
      1. Klik op het pijlpictogram Hallo ![pijltje](./media/storsimple-create-volume/HCS_ArrowIcon-include.png) toogo toohello volgende pagina.
3. In Hallo **extra instellingen** dialoogvenster toevoegen van een nieuwe record voor toegangscontrole (ACR):
   
   1. Geef een **naam** voor uw ACR op.
   2. Onder **iSCSI-initiatornaam**, bieden Hallo iSCSI Qualified Name (IQN) van uw Windows-host. Als u Hallo IQN niet hebt, gaat u verder te[Get Hallo IQN van een Windows Server-host](#get-the-iqn-of-a-windows-server-host).
   3. Het is raadzaam dat u een standaardback-up inschakelen door het selecteren van Hallo **een standaardback-up voor dit volume inschakelen** selectievakje. Hallo standaardback-up maakt een beleid dat wordt uitgevoerd om 22.30 elke dag (tijd op het apparaat) en maakt een cloudmomentopname van dit volume.
      
      > [!NOTE]
      > Nadat Hallo back-up hier is ingeschakeld, kan niet worden teruggezet. U moet deze instelling tooedit Hallo volume toomodify.
      > 
      > 
      
        ![Volume toevoegen](./media/storsimple-create-volume/AddVolume2-include.png)
4. Klik op het vinkje Hallo ![vinkje](./media/storsimple-create-volume/HCS_CheckIcon-include.png). Een volume wordt gemaakt met de Hallo opgegeven instellingen.

![Video beschikbaar](./media/storsimple-create-volume/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe toocreate een StorSimple-volume, klik op [hier](https://azure.microsoft.com/documentation/videos/create-a-storsimple-volume/).


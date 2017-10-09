<!--author=SharS last changed: 9/17/15-->

#### <a name="toomount-initialize-and-format-a-volume"></a>toomount, initialiseren en formatteren van een volume
1. Start Hallo Microsoft iSCSI-initiator.
2. In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **detectie** tabblad **Portal detecteren**.
3. In Hallo **doelportaal detecteren** in het dialoogvenster Hallo IP-adres van de netwerkinterface met iSCSI-functionaliteit leveren en klik vervolgens op **OK**. 
4. In Hallo **eigenschappen iSCSI-Initiator** venster op Hallo **doelen** tabblad, zoek Hallo **gedetecteerde doelen**. de apparaatstatus Hallo moet worden weergegeven als **inactief**.
5. Selecteer het doelapparaat Hallo en klik vervolgens op **Connect**. Nadat het Hallo-apparaat is verbonden, Hallo moet statuswijziging te**verbonden**. (Zie voor meer informatie over het gebruik van Hallo Microsoft iSCSI-initiator [installeren en configureren van Microsoft iSCSI-Initiator][1]).
6. Druk op uw Windows-host op Hallo Windows-toets + X en klik vervolgens op **uitvoeren**. 
7. In Hallo **uitvoeren** in het dialoogvenster, type **Diskmgmt.msc**. Klik op **OK**, en Hallo **Schijfbeheer** dialoogvenster wordt weergegeven. Hallo rechterdeelvenster wordt Hallo volumes op uw host weergeven.
8. In Hallo **Schijfbeheer** venster hello gekoppelde volumes weergegeven zoals in de volgende illustratie Hallo. Met de rechtermuisknop op Hallo gedetecteerde volume (Klik op de naam van de schijf Hallo), en klik vervolgens op **Online**.
   
     ![Opmaakvolume initialiseren](./media/storsimple-mount-initialize-format-volume/HCS_InitializeFormatVolume-include.png) 
9. Met de rechtermuisknop op het Hallo-volume (Klik op de naam van de schijf Hallo) opnieuw en klik vervolgens op **initialiseren**.
10. een eenvoudig volume tooformat uitvoeren Hallo stappen te volgen:
    
    1. Selecteer Hallo volume, met de rechtermuisknop op (Klik op de juiste gebied Hallo), en klik op **Nieuw eenvoudig Volume**.
    2. In de wizard Nieuw eenvoudig Volume Hallo Hallo volume en de stationsletter opgeven en Hallo volume configureren als een NTFS-bestandssysteem.
    3. Geef een clustergrootte van 64 kB op. Deze clustergrootte werkt goed samen met de Hallo ontdubbelingsalgoritmen die worden gebruikt in Hallo StorSimple-oplossing.
    4. Voer een snelle formattering uit.

![Video beschikbaar](./media/storsimple-mount-initialize-format-volume/Video_icon.png) **Video beschikbaar**

een video die u laat zien hoe toomount, initialiseren en opmaak een StorSimple-volume, klikt u op toowatch [hier](https://azure.microsoft.com/documentation/videos/mount-initialize-and-format-a-storsimple-volume/).

<!--Link references-->
[1]: https://technet.microsoft.com/library/ee338480(WS.10).aspx

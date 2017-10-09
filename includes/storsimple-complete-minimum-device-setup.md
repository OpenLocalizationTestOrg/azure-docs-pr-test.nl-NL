<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello minimale StorSimple-Apparaatinstelling
1. In Hallo **apparaten** pagina, selecteer Hallo-apparaat, klikt u op Hallo pijl tegen Hallo apparaat naam toogo toohello specifiek Apparaatpagina. 
   
    ![Pagina met apparaten terwijl het apparaat online is](./media/storsimple-complete-minimum-device-setup/HCS_DevicesPageM-include.png) 
2. Klik op het pictogram snel starten ![pictogram Quick Start](./media/storsimple-complete-minimum-device-setup/HCS_QuickStartIcon-include.png) tooaccess Hallo apparaat snel starten-pagina. Klik op **Apparaatinstelling** toostart hello **apparaat configureren** wizard.
   
    ![De pagina Quick Start voor het apparaat](./media/storsimple-complete-minimum-device-setup/Device_Quick_Start_page_1M.png)
3. Op Hallo **basisinstellingen** pagina, Hallo te volgen:
   
   1. Geef een **beschrijvende naam** voor het apparaat op. Hallo standaardapparaatnaam informatie zoals Hallo Apparaatmodel en serienummer. Uw apparaat, kunt u een beschrijvende naam van up too64 tekens toomanage toewijzen.
   2. Set Hallo **tijdzone** op basis van de geografische locatie Hallo in welke Hallo apparaat wordt geïmplementeerd. Het apparaat zal deze tijdzone gebruiken voor alle geplande bewerkingen.
   3. Geef onder **DNS-instellingen** het adres voor uw **secundaire DNS-server** op. Als u IPv6 gebruikt, wordt Hallo veld ingevuld op basis van Hallo IPv6-voorvoegsel dat is opgegeven in de Windows PowerShell-interface Hallo. 
      Als Hallo secundaire DNS-server niet is geconfigureerd, worden niet toegestaan toosave configuratie van uw apparaat.
   4. Schakel onder de iSCSI-interfaces ten minste één netwerk voor iSCSI in. Ten minste één netwerkinterface moet toobe ingeschakeld voor de cloud en één interface moet toobe iSCSI-functionaliteit. DATA 0 is automatisch ingeschakeld voor de cloud.
      
      ![Basisinstellingen voor de minimale StorSimple-apparaatinstelling](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupBasicSettings1-include.png)
4. Klik op het pijlpictogram Hallo. ![StorSimple-pijlpictogram](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
5. Op Hallo **netwerkinterfaces** pagina, bevatten Hallo van vaste IP-adressen voor Controller 0 en Controller 1. Als hello DATA 0 interface is geconfigureerd voor IPv4, hello de vaste IP-adressen moeten toobe is opgegeven in Hallo IPv4-indeling. Als u een voorvoegsel voor IPv6-configuratie hebt opgegeven, wordt Hallo vaste IP-adressen automatisch in deze velden ingevuld.

    > [!NOTE] 
    > - Hallo-controller vaste IP-adressen moet toobe gratis IP-adressen binnen Hallo subnet toegankelijk door Hallo apparaat IP-adres.
    > - Hallo vaste IP-adressen voor controller hello worden gebruikt voor het onderhoud van Hallo updates toohello apparaat en Hallo vaste IP-adressen moet daarom routeerbaar en kunnen tooconnect toohello Internet.

    ![Netwerkinterfaces voor de minimale StorSimple-apparaatinstelling](./media/storsimple-complete-minimum-device-setup/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

1. Klik op het vinkje Hallo ![vinkje voor StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   U keert terug toohello apparaat **Quick Start** pagina.
   
   > [!NOTE]
   > U kunt wijzigen Hallo alle andere apparaatinstellingen op elk gewenst moment via Hallo **configureren** pagina.
   > 
   > 

![Video beschikbaar](./media/storsimple-complete-minimum-device-setup/Video_icon.png) **Video beschikbaar**

toowatch een video die u laat zien hoe toocomplete Hallo minimale Apparaatinstelling, klikt u op [hier](https://azure.microsoft.com/documentation/videos/minimum-storsimple-device-setup/).


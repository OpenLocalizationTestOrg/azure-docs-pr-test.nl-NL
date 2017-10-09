<!--author=alkohli last changed: 9/17/15-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello minimale StorSimple-Apparaatinstelling
1. Selecteer Hallo-apparaat en klikt u op **Quick Start**. Klik op **Apparaatinstelling** wizard apparaat toostart Hallo-configureren.
2. In de wizard voor apparaat configureren Hallo **basisinstellingen** dialoogvenster vak, Hallo te volgen:
   
   1. Geef een **beschrijvende naam** voor het apparaat op. Hallo standaardapparaatnaam informatie zoals Hallo Apparaatmodel en serienummer. Uw apparaat, kunt u een beschrijvende naam van up too64 tekens toomanage toewijzen.
   2. Set Hallo **tijdzone** op basis van de geografische locatie Hallo in welke Hallo apparaat wordt geïmplementeerd. Het apparaat zal deze tijdzone gebruiken voor alle geplande bewerkingen.
   3. Geef onder **DNS-instellingen** het adres voor uw **secundaire DNS-server** op. Als u IPv6 gebruikt, wordt Hallo veld ingevuld op basis van Hallo IPv6-voorvoegsel dat is opgegeven in de Windows PowerShell-interface Hallo. 
      Als Hallo secundaire DNS-server niet is geconfigureerd, worden niet toegestaan toosave configuratie van uw apparaat.
   4. Schakel onder de iSCSI-interfaces ten minste één netwerk voor iSCSI in. Ten minste één netwerkinterface moet toobe ingeschakeld voor de cloud en één interface moet toobe iSCSI-functionaliteit. DATA 0 is automatisch ingeschakeld voor de cloud.
      
      ![Basisinstellingen voor de minimale StorSimple-apparaatinstelling](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupBasicSettings1-include.png)
3. Klik op het pijlpictogram Hallo. ![StorSimple-pijlpictogram](./media/storsimple-complete-minimum-device-setup/HCS_ArrowIcon-include.png)
4. In Hallo **netwerkinterfaces** dialoogvenster Geef Hallo vaste IP-adressen voor Controller 0 en Controller 1. **Hallo-controller vaste IP-adressen moet toobe gratis IP-adressen binnen Hallo subnet toegankelijk door Hallo apparaat IP-adres.** Als hello DATA 0 interface is geconfigureerd voor IPv4, hello de vaste IP-adressen moeten toobe is opgegeven in Hallo IPv4-indeling. Als u een voorvoegsel voor IPv6-configuratie hebt opgegeven, wordt Hallo vaste IP-adressen automatisch in deze velden ingevuld.

    ![Netwerkinterfaces voor de minimale StorSimple-apparaatinstelling](./media/storsimple-complete-minimum-device-setup-u1/HCS_MinDeviceSetupNetworkInterfaces2-include.png)

    Hallo vaste IP-adressen voor controller hello worden gebruikt voor het onderhoud van Hallo updates toohello apparaat en Hallo vaste IP-adressen moet daarom routeerbaar en kunnen tooconnect toohello Internet. U kunt controleren of uw vaste IP-adressen voor de controller routeerbaar zijn met Hallo [Test-HcsmConnection] [ Test] cmdlet. Hallo volgende voorbeeld toont vaste IP-adressen voor controller gerouteerde toohello Internet zijn en toegang tot Hallo Microsoft Update-servers. 

     ![Test-HcsmConnection met routeerbare IP-adressen](./media/storsimple-complete-minimum-device-setup-u1/Test-HcsmConnectionOutputRegisteredDevice.png)

1. Klik op het vinkje Hallo ![vinkje voor StorSimple](./media/storsimple-complete-minimum-device-setup/HCS_CheckIcon-include.png).
   U keert terug toohello apparaat **Quick Start** pagina.
   
   > [!NOTE]
   > U kunt wijzigen Hallo alle andere apparaatinstellingen op elk gewenst moment via Hallo **configureren** pagina.
   > 
   > 

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx
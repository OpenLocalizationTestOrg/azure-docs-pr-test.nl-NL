<!--author=alkohli last changed: 01/12/17-->

#### <a name="toocomplete-hello-minimum-storsimple-device-setup"></a>toocomplete hello minimale StorSimple-Apparaatinstelling

   > [!NOTE]
   > U kunt Hallo apparaatnaam niet wijzigen zodra de minimale Apparaatinstelling Hallo is voltooid.
   
1. Uit Hallo in tabelvorm aanbieding van apparaten in Hallo **apparaten** blade selecteren en op uw apparaat. Hallo-apparaat bevindt zich in een **tooset gereed** status. Hallo **apparaat configureren** blade wordt geopend.

     ![Netwerkinterfaces voor de minimale StorSimple-apparaatinstelling](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig1.png)

2. In Hallo **apparaat configureren** blade:
   
   1. Geef een **beschrijvende naam** voor het apparaat op. Hallo standaardapparaatnaam informatie zoals Hallo Apparaatmodel en serienummer. Uw apparaat, kunt u een beschrijvende naam van up too64 tekens toomanage toewijzen.
   2. Set Hallo **tijdzone** op basis van de geografische locatie Hallo in welke Hallo apparaat wordt geïmplementeerd. Het apparaat gebruikt deze tijdzone gebruiken voor alle geplande bewerkingen.
   3. Onder Hallo **DATA 0 instellingen**:

       1. Uw DATA 0-netwerkinterface bevat ingeschakeld met Hallo-instellingen (IP-subnet, gateway) die zijn geconfigureerd via de wizard setup Hallo netwerk. DATA 0 wordt ook automatisch ingeschakeld voor de cloud, evenals voor iSCSI.

       2. Bevatten Hallo van vaste IP-adressen voor Controller 0 en Controller 1. **Hallo-controller vaste IP-adressen moet toobe gratis IP-adressen binnen Hallo subnet toegankelijk door Hallo apparaat IP-adres.** Als hello DATA 0 interface is geconfigureerd voor IPv4, hello de vaste IP-adressen moeten toobe is opgegeven in Hallo IPv4-indeling. Als u een voorvoegsel voor IPv6-configuratie hebt opgegeven, worden Hallo vaste IP-adressen automatisch in deze velden ingevuld.

            ![Netwerkinterfaces voor de minimale StorSimple-apparaatinstelling](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig2.png)

            Hallo vaste IP-adressen voor controller hello worden gebruikt voor het onderhoud Hallo updates toohello apparaat. Daarom moet Hallo vaste IP-adressen routeerbaar en kunnen tooconnect toohello Internet. U kunt controleren of uw vaste IP-adressen voor de controller routeerbaar zijn met Hallo [Test-HcsmConnection] [ Test] cmdlet. Hallo volgende voorbeeld toont vaste IP-adressen voor controller gerouteerde toohello Internet zijn en toegang tot Hallo Microsoft Update-servers.

            ![Test-HcsmConnection met routeerbare IP-adressen](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig3.png)

1. Klik op **OK**. Hallo apparaatconfiguratie wordt gestart. Wanneer de apparaatconfiguratie Hallo voltooid is, wordt u gewaarschuwd. apparaat-statuswijzigingen te Hallo**Online** in Hallo **apparaten** blade.

    ![Netwerkinterfaces voor de minimale StorSimple-apparaatinstelling](./media/storsimple-8000-complete-minimum-device-setup-u2/step4minconfig4.png)

<!--Link reference-->
[Test]: https://technet.microsoft.com/library/dn715782(v=wps.630).aspx

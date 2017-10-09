<!--author=SharS last changed: 9/17/15-->

#### <a name="tooconnect-through-hello-serial-console"></a>tooconnect via de seriële console Hallo
1. Sluit de seriële kabel toohello-apparaat (rechtstreeks of via een USB-seriële adapter).
2. Open Hallo **Configuratiescherm**, en open vervolgens Hallo **Apparaatbeheer**.
3. Hallo COM-poort herkennen zoals weergegeven in de volgende illustratie Hallo.
   
     ![Verbinding maken via een seriële console](./media/storsimple-use-putty/HCS_ConnectingDeviceS-include.png)
4. Start PuTTY. 
5. Wijzig in het rechterdeelvenster Hallo Hallo **verbindingstype** te**seriële**.
6. Typ in het rechterdeelvenster Hallo Hallo juiste COM-poort. Zorg ervoor dat de Hallo seriële configuratieparameters als volgt zijn ingesteld:
   
   * Snelheid: 115.200
   * Gegevensbits: 8
   * Stopbits: 1
   * Pariteit: Geen
   * Datatransportbesturing: Geen
     
     Deze instellingen worden weergegeven in de volgende illustratie Hallo.
     
     ![Instellingen voor PuTTY](./media/storsimple-use-putty/HCS_PuttyConfig-include.png) 
     
     > [!NOTE]
     > Als Hallo standaard instelling voor datatransportbesturing niet werkt, kunt u Hallo flow control tooXON/XOFF.
     > 
     > 
7. Klik op **Open** toostart een seriële sessie.


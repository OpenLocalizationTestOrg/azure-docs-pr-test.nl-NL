> [!IMPORTANT]
> tooreceive Pushmeldingen van Mobile Engagement, moet u tooenable `Silent Remote Notifications` in uw toepassing. U moet tooadd Hallo externe melding waarde toohello matrix uibackgroundmodes in uw Info.plist-bestand.
> 
> 

1. Open `info.plist` bestand in Hallo-project
2. Klik met de rechtermuisknop op het bovenste item in de lijst Hallo Hallo (`Information Property List`) en een nieuwe rij toegevoegd
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Voer in de nieuwe rij Hallo`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Klik op Hallo pijl-links tooexpand Hallo rij
5. Hallo achter waarde toohello item 0 toevoegen`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Wanneer u Hallo wijzigen, Hallo info.plist XML mag Hallo volgende sleutel en de waarde:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. Als u **Xcode 7+** en **iOS 9+** gebruikt:
   
   * Schakel **Pushmeldingen** in Doelen > uw doelnaam > Mogelijkheden in.


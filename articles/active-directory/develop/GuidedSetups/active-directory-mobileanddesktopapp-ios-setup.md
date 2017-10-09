---
title: aaaAzure AD v2 iOS Getting Started - instellingen | Microsoft Docs
description: Hoe iOS (Swift)-toepassingen met een API waarvoor toegangstokens door Azure Active Directory-v2-eindpunt kunnen aanroepen
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 62c4ee9a2d4ccaec780bee09fb4bc34cff2eb6df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
## <a name="setting-up-your-ios-application"></a>Uw iOS-toepassing instellen

Deze sectie bevat stapsgewijze instructies voor het toocreate een nieuw project toodemonstrate hoe een toepassing voor iOS (Swift) toointegrate met *aanmelden met Microsoft* zodat Web-API's waarvoor een token op te vragen.

> Voorkeur toodownload dit voorbeeld XCode-project in plaats daarvan? [Downloaden van een project](https://github.com/Azure-Samples/active-directory-ios-swift-native-v2/archive/master.zip) - en skip-toohello [configuratiestap](#create-an-application-express) tooconfigure Hallo codevoorbeeld voordat wordt uitgevoerd.


## <a name="install-carthage-toodownload-and-build-msal"></a>Installeer Carthage toodownload en MSAL bouwen
Carthage package manager wordt gebruikt tijdens de evaluatieperiode Hallo van MSAL – het is geïntegreerd met XCode behoud Hallo mogelijkheid voor toohello-bibliotheek van Microsoft toomake wijzigingen.

- Download en installeer de nieuwste versie Hallo van Carthage [hier](https://github.com/Carthage/Carthage/releases "Carthage download-URL")

## <a name="creating-your-application"></a>Maken van de toepassing

1.  Open Xcode en selecteer`Create a new Xcode project`
2.  Selecteer `iOS`  >  `Single view Application` en klik op *volgende*
3.  Geef een productnaam en klik op *volgende*
4.  Selecteer een map toocreate uw app en klik op *maken*

## <a name="build-hello-msal-framework"></a>Hallo MSAL Framework bouwen

Volg onderstaande toopull Hallo-instructies en vervolgens samenstellen Hallo meest recente versie van Carthage MSAL bibliotheken:

1.  Open de Hallo bash terminal en gaat u de hoofdmap van de App toohello
2.  Hallo onderstaande bestand kopiëren en plakken in Hallo bash terminal toocreate een 'Cartfile':

```bash
echo "github \"AzureAD/microsoft-authentication-library-for-objc\" \"master\"" > Cartfile
```
<!-- Workaround for Docs conversion bug -->
<ol start="3">
<li>
Kopieer en plak de onderstaande Hallo. Met deze opdracht haalt afhankelijkheden in een map Carthage/opdrachten om uitchecken vervolgens builds Hallo MSAL bibliotheek:
</li>
</ol>

```bash
carthage update
```

> Hallo proces hierboven is gebruikte toodownload en build Hallo Microsoft Authentication Library (MSAL). MSAL verwerkt aanschaf, opslaan in cache en gebruiker tokens die worden gebruikt tooaccess API's die zijn beveiligd door Azure Active Directory-v2 hello te vernieuwen.

## <a name="add-hello-msal-framework-tooyour-application"></a>Hallo MSAL framework tooyour toepassing toevoegen
1.  Open in Xcode hello `General` tabblad
2.  Ga toohello `Linked Frameworks and Libraries` sectie en klikt u op`+`
3.  Selecteer `Add other…`
4.  Selecteer: `Carthage`  >  `Build`  >  `iOS`  >  `MSAL.framework` en klik op *Open*. U ziet `MSAL.framework` toohello lijst toegevoegd.
5.  Ga te`Build Phases` tabblad en klik op `+` pictogram kiezen`New Run Script Phase`
6.  Hallo inhoud toohello na toevoegen *gebied script*:

```text
/usr/local/bin/carthage copy-frameworks
```

<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Hallo te volgende toevoegen<code>Input Files</code> door te klikken op <code>+</code>:
</li>
</ol>

```text
$(SRCROOT)/Carthage/Build/iOS/MSAL.framework
```

## <a name="creating-your-applications-ui"></a>Maken van de gebruikersinterface van uw toepassing
Een bestand Main.storyboard moet automatisch worden gemaakt als onderdeel van uw project-sjabloon. Volg onderstaande toocreate Hallo app UI Hallo instructies:

1.  Control + klik `Main.storyboard` toobring Hallo contextafhankelijke menu omhoog en klik vervolgens op:`Open As` > `Source Code`
2.  Vervang Hallo `<scenes>` knooppunt met Hallo-code hieronder:

```xml
 <scenes>
    <scene sceneID="tne-QT-ifu">
        <objects>
            <viewController id="BYZ-38-t0r" customClass="ViewController" customModule="MSALiOS" customModuleProvider="target" sceneMemberID="viewController">
                <layoutGuides>
                    <viewControllerLayoutGuide type="top" id="y3c-jy-aDJ"/>
                    <viewControllerLayoutGuide type="bottom" id="wfy-db-euE"/>
                </layoutGuides>
                <view key="view" contentMode="scaleToFill" id="8bC-Xf-vdC">
                    <rect key="frame" x="0.0" y="0.0" width="375" height="667"/>
                    <autoresizingMask key="autoresizingMask" widthSizable="YES" heightSizable="YES"/>
                    <subviews>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Microsoft Authentication Library" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="ifd-fu-zjm">
                            <rect key="frame" x="64" y="28" width="246" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <label opaque="NO" userInteractionEnabled="NO" contentMode="left" horizontalHuggingPriority="251" verticalHuggingPriority="251" fixedFrame="YES" text="Logging" textAlignment="natural" lineBreakMode="tailTruncation" baselineAdjustment="alignBaselines" adjustsFontSizeToFit="NO" translatesAutoresizingMaskIntoConstraints="NO" id="98g-dc-BPL">
                            <rect key="frame" x="16" y="277" width="62" height="21"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <fontDescription key="fontDescription" type="system" pointSize="17"/>
                            <nil key="textColor"/>
                            <nil key="highlightedColor"/>
                        </label>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="2rX-Vv-T1i">
                            <rect key="frame" x="87" y="100" width="200" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Call Microsoft Graph API"/>
                            <connections>
                                <action selector="callGraphButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="Kx0-JL-Bv9"/>
                            </connections>
                        </button>
                        <textView clipsSubviews="YES" multipleTouchEnabled="YES" contentMode="scaleToFill" fixedFrame="YES" editable="NO" textAlignment="natural" selectable="NO" translatesAutoresizingMaskIntoConstraints="NO" id="qXW-2z-J7K">
                            <rect key="frame" x="16" y="324" width="343" height="291"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <color key="backgroundColor" white="1" alpha="1" colorSpace="calibratedWhite"/>
                            <accessibility key="accessibilityConfiguration">
                                <accessibilityTraits key="traits" updatesFrequently="YES"/>
                            </accessibility>
                            <fontDescription key="fontDescription" type="system" pointSize="14"/>
                            <textInputTraits key="textInputTraits" autocapitalizationType="sentences"/>
                        </textView>
                        <button opaque="NO" contentMode="scaleToFill" fixedFrame="YES" contentHorizontalAlignment="center" contentVerticalAlignment="center" buttonType="roundedRect" lineBreakMode="middleTruncation" translatesAutoresizingMaskIntoConstraints="NO" id="9u4-b8-vmX">
                            <rect key="frame" x="137" y="138" width="100" height="30"/>
                            <autoresizingMask key="autoresizingMask" flexibleMaxX="YES" flexibleMaxY="YES"/>
                            <state key="normal" title="Sign-Out"/>
                            <connections>
                                <action selector="signoutButton:" destination="BYZ-38-t0r" eventType="touchUpInside" id="kZT-P8-0Zy"/>
                            </connections>
                        </button>
                    </subviews>
                    <color key="backgroundColor" red="1" green="1" blue="1" alpha="1" colorSpace="custom" customColorSpace="sRGB"/>
                </view>
                <connections>
                    <outlet property="loggingText" destination="qXW-2z-J7K" id="uqO-Yw-AsK"/>
                    <outlet property="signoutButton" destination="9u4-b8-vmX" id="OCh-qk-ldv"/>
                </connections>
            </viewController>
            <placeholder placeholderIdentifier="IBFirstResponder" id="dkx-z0-nzr" sceneMemberID="firstResponder"/>
        </objects>
        <point key="canvasLocation" x="140" y="137.18140929535232"/>
    </scene>
</scenes>
```

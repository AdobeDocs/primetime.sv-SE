---
title: Inledande konfiguration av Flash Access Manager
description: Inledande konfiguration av Flash Access Manager
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Inledande konfiguration av Flash Access Manager {#initial-flash-access-manager-setup}

Gör så här för att konfigurera Flash Access Manager:

1. Distribuera Packager Server. Den här servern bör endast vara tillgänglig för användare i din brandvägg (distribuera inte programvaran på en offentlig dator). Mer information om hur du distribuerar servern finns i [Distribuera licensservern och bevakad mapppaketerare](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Kopiera [!DNL flashaccess-packager.war] till Tomcat&#39;s webapps folder.
   * Kopiera [!DNL flashaccess-refimpl-packager.properties] från resurser till en plats i klassökvägen.
   * Starta servern. Du kommer att se fel på grund av problem i egenskapsfilen. Detta förväntas eftersom egenskaperna inte har fyllts i ännu.

1. Installera Flash Access Manager AIR genom att starta [!DNL .air] (kräver AIR 1.5 eller senare).
1. Starta Flash Access Manager AIR.

   Om servern körs någon annanstans än `https://localhost:8080*`visas fel som anger att programmet inte kan ansluta till servern. Stäng feldialogrutan och fyll i rätt URL för Packager Server-URL på fliken Inställningar. Om servern körs på den angivna URL:en och egenskapsfilen finns i klassökvägen fylls skärmen Inställningar i med värdena i egenskapsfilen. När du har angett URL:en för paketerarservern kommer AIR-programmet att komma ihåg den här inställningen och du behöver inte ange den nästa gång du startar programmet.
1. Fyll i värdena på fliken Inställningar och klicka på **[!UICONTROL Save]**.
1. Om du vill använda Bevakade mappar måste du starta om servern för att kunna återställa efter de fel du såg i steg 3. Om inställningarna är korrekt konfigurerade bör inga fel visas under start.

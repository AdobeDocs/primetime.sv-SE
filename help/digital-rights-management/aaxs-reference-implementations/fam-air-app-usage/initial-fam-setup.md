---
description: 'null'
seo-description: 'null'
seo-title: Inledande konfiguration av Flash Access Manager
title: Inledande konfiguration av Flash Access Manager
uuid: e9041f7c-b098-4121-88bf-ff3e6369e01b
translation-type: tm+mt
source-git-commit: 4f196bbd079edeb1a423afee6b4b7e249d380f40
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---


# Inledande konfiguration av Flash Access Manager {#initial-flash-access-manager-setup}

Gör så här för att konfigurera Flash Access Manager:

1. Distribuera Packager Server. Den här servern bör endast vara tillgänglig för användare i din brandvägg (distribuera inte programvaran på en offentlig dator). Mer information om hur du distribuerar servern finns i [Distribuera licensservern och bevakad mapppaketerare](../../aaxs-reference-implementations/deploying-license-server-and-wfp/deploying-license-server-wfp-overview.md).

   * Kopiera [!DNL flashaccess-packager.war] till Tomcat-webbappen.
   * Kopiera [!DNL flashaccess-refimpl-packager.properties] från resurser till en plats i klassökvägen.
   * Starta servern. Du kommer att se fel på grund av problem i egenskapsfilen; detta förväntas eftersom egenskaperna ännu inte har fyllts i.

1. Installera AIR-programmet för Flash Access Manager genom att starta filen [!DNL .air] (kräver AIR 1.5 eller senare).
1. Starta AIR-programmet för Flash Access Manager.

   Om servern körs någon annanstans än `https://localhost:8080*` visas fel som anger att programmet inte kan ansluta till servern. Stäng feldialogrutan och fyll i rätt URL för Packager Server-URL på fliken Inställningar. Om servern körs på den angivna URL:en och egenskapsfilen finns i klassökvägen fylls skärmen Inställningar i med värdena i egenskapsfilen. När du har angett paketerarserverns URL kommer AIR-programmet ihåg den här inställningen och du behöver inte ange den nästa gång du startar programmet.
1. Fyll i värdena på fliken Inställningar och klicka på **[!UICONTROL Save]**.
1. Om du vill använda Bevakade mappar måste du starta om servern för att kunna återställa efter de fel du såg i steg 3. Om inställningarna är korrekt konfigurerade bör inga fel visas under start.


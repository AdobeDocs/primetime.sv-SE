---
title: Paketera media
description: Paketera media
copied-description: true
exl-id: fc2d1f12-8fab-4e62-8d4c-527911be347f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Paketera media {#package-media}

Använd fliken Paketera media för att paketera innehåll. I avsnittet Packager Properties visas de Packager-inställningar som har angetts på fliken Inställningar. Om du vill ändra inställningarna går du till fliken Inställningar, ändrar inställningarna och sparar.

Om du vill paketera en enskild FLV- eller F4V-fil väljer du **[!UICONTROL Select Single File]** och ange den fullständiga sökvägen till källfilen och den fullständiga sökvägen där den krypterade filen ska sparas.

Om du vill paketera alla filer i en mapp väljer du **[!UICONTROL Select Single Folder]** alternativ. Ange den mapp som innehåller källfilerna. Endast filer i Indatamappen som matchar **[!UICONTROL Input Media File Selection]** kommer att paketeras (filer i undermappar paketeras inte). Välj om du vill kryptera [!DNL .flv] filer, [!DNL .f4v] eller ange ett eget reguljärt uttryck (till exempel &quot;.&#42;&quot; krypterar alla filer i mappen). De krypterade filerna sparas i den angivna utdatamappen med samma filnamn som originalfilen.

>[!NOTE]
>
>Filsökvägarna måste referera till filer som är tillgängliga för paketeringsservern. Om du kör Flash Access Manager på en annan dator än paketeringsservern måste du ange en sökväg som är tillgänglig för servern (antingen på en nätverksenhet eller på själva servern).

I följande tabell beskrivs inställningarna för Paketmedia:

| Inställningar | Beskrivning |
|---|---|
| Principfilnamn | Välj en eller flera profiler i listrutan som du vill tillämpa på innehållet. Om du vill välja flera profiler håller du ned CTRL-tangenten när du väljer profiler. |
| Sekunder okrypterade | Anger antalet sekunder med innehåll som ska lämnas okrypterat i början av filen. Om du vill kryptera från början anger du &quot;0&quot;. |
| Kryptera video | Markera den här kryssrutan om du vill kryptera videodata |
| Krypteringsnivå | Om videokryptering är aktiverat väljer du krypteringsnivå för videodata. Hög krypterar alla videodata. Medel och Låg krypterar selektivt delar av videon. (Endast för F4V med H.264-video) |
| Kryptera ljud | Markera den här kryssrutan om du vill kryptera ljuddata |
| Kryptera skript | Markera den här kryssrutan om du vill kryptera skriptdata (endast FLV) |
| Anpassade egenskaper | Ange anpassade egenskaper som ska inkluderas i det paketerade innehållet. Dessa egenskaper är tillgängliga för licensservern när en licens utfärdas. (Valfritt) |

När paketeringsalternativen är valda klickar du på **[!UICONTROL Package Media]** för att börja paketera filerna.

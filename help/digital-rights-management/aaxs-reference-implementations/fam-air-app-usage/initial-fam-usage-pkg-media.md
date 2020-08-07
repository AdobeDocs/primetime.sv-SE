---
seo-title: Paketera media
title: Paketera media
uuid: f6e877be-d916-4766-bc44-99891a3df3a8
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---


# Paketera media {#package-media}

Använd fliken Paketera media för att paketera innehåll. I avsnittet Packager Properties visas de Packager-inställningar som har angetts på fliken Inställningar. Om du vill ändra inställningarna går du till fliken Inställningar, ändrar inställningarna och sparar.

Om du vill paketera en enskild FLV- eller F4V-fil väljer du **[!UICONTROL Select Single File]** alternativet och anger den fullständiga sökvägen till källfilen och den fullständiga sökvägen där den krypterade filen ska sparas.

Om du vill paketera alla filer i en mapp väljer du **[!UICONTROL Select Single Folder]** alternativet. Ange den mapp som innehåller källfilerna. Endast filer i indatamappen som matchar villkoren kommer att paketeras (filer i undermappar paketeras inte). **[!UICONTROL Input Media File Selection]** Välj om du vill kryptera [!DNL .flv] filer, [!DNL .f4v] filer eller ange ett eget reguljärt uttryck (till exempel &quot;.*&quot; krypterar alla filer i mappen). De krypterade filerna sparas i den angivna utdatamappen med samma filnamn som originalfilen.

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

När paketeringsalternativen har valts klickar du på **[!UICONTROL Package Media]** knappen för att börja paketera filerna.

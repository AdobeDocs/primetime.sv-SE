---
title: Instrumentpanel för konto-IQ
description: Kontrollpanelen hjälper till att identifiera förekomster av lösenordsdelning genom att analysera en mängd olika prenumerationsdata.
exl-id: 616da2a5-c9fe-40ea-90cf-f565bc13e764
source-git-commit: 7706d5fcafdcfb9c0d4cc69936681c6223b0739d
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Kontrollpanelen {#dashboard}

Kontrollpanelen sammanfattar och sammanställer data i en samling diagram och rapporter som utformats för att ge en översikt över omfattningen och effekten av kontodelning. Den innehåller en enda sida med de viktigaste rapporterna och mätvärdena från konto-IQ.

<table><tr><th>

+++Dashboard för programmerare

![kontonamall för IQ](assets/dashboard-capture.png)


*Bild: Kontrollpanelen*

## Genomsnittlig delningspoäng - aggregerad för aktuellt segment {#aggregated-sharing}

Panelen Aggregated Sharing Score (Aggregated Sharing Score) innehåller en översta avläsning som sammanfattar hur stor del av materialet som delas i konton och strömningsvolymer.

Värdena hjälper er att förstå omfattningen av dina prenumeranters delning av autentiseringsuppgifter, vilket ger ett mått på behovet av att agera på den.

![](assets/aggregate-sharing-score.png)


*Bild: Genomsnittlig poängpanel för delning - aggregerad för det aktuella segmentet*

Följande tre mätvärden är komponenter i medeldelningspoängen.

### Delningsnivå {#sharing-level}

Med delningsnivåmätaren visas procentandelen av alla dina prenumerantkonton (i det definierade segmentet) som delas under den valda tidsramen.

Ett värde som beräknas baserat på ett genomsnitt av den sannolikhet för delning som beräknats för varje konto i den uppsättning av valda MVPD-program som har direktuppspelats från en av de valda programmeringskanalerna under den valda tidsramen.

![](assets/sharing-level.png)


*Bild: Delningsnivå*

Trend-indikatorn visar den procentuella förändringen av måttets värde i från föregående tidsram.

### Användning från delade konton {#usage-from-shared-accounts}

Den här mätaren anger hur stor procentandel av användningen av alla prenumerantkonton som kommer från de delade kontona för det definierade segmentet och tidsperioden. Mätaren anger användningsområdena (från delade konton) på skalan 0 till 100 %. Intervallen - Låg, Medel, Hög och Onormal - baseras på genomsnittet i branschen.

Du kan också se Trend-indikatorn, som visar en ökning eller minskning av användningen från delade konton jämfört med föregående tidsram.

![](assets/usage-4mshared-accounts.png)


*Bild: Användning från delade konton*

### Total delning {#overall-sharing-score}

Det övergripande poängdelningspoängen består av delningspoäng som &quot;Delningsnivå&quot; och &quot;z Användning från delade konton&quot;.

Det ger ett värde som återspeglar den relativa effekten av delning jämfört med branschen. Syftet liknar syftet med en kreditpoäng som sammanfattar situationen med ett enda tal. Men i det här fallet är ju högre desto större blir den potentiella skadan.

![](assets/overall-sharing-score.png)


*Bild: Total delning*

<!--### MVPDs in segment {#mvpd-in-segment}

It is a table of risk indices and accounts totals for the top MVPDs ranked by overall usage or account sharing.

![](assets/mvpds-in-segment.png)-->

### Branschövergripande poäng för utbyte av videofiler {#top-mvpds}

I den här tabellen visas en jämförande vy över de olika aggregerade delningspoängen för de programmerade videofilerna i segmentet.

>[!NOTE]
>
>I tabellen används övergripande branschdata för jämförande syften, inte de data som representeras av dessa videoprogrammeringsskyltar i segmentet.

![](assets/top-mvpds.png)


*Bild: MVPD i segment efter totalpoäng*

### Dela poäng via kanaler och videoprogrammeringsfönster {#sharin-score-by-channels-and-mvpds}

I den här tabellen visas en jämförande vy över delningspoängen för de valda kanalerna för de olika programmeringsversionerna i det aktuella segmentet.

![](assets/sharing-scores-by-channels-mvpds.png)


*Bild: Dela bakgrundsmusik per kanal och videoprogrammerare*

### Sannolikhet för kontodelning {#accounts-sharing-probability}

Diagrammet delas upp i intervall med sannolika quinles för delning från mycket låg (0-20 %) till mycket hög (80=100 %).

>[!NOTE]
>
>I stapeldiagrammet används en logaritmisk skala.


![](assets/dashboard-ac-sharing-prob.png)


*Bild: Antal och procentandelar av prenumerantkonton i olika delningssannolikhetsintervall*

### Antal konton och användning genom att dela sannolikhetsnivå {#number-of-accounts-usage-sharing-probability}

Den här panelen ger en tabellvy över konton som är uppdelade i intervall med delning av sannolikhetsknappar från mycket låga (0-20 %) till mycket höga (80-100 %) med varje quintiles associerade användning från delade konton.

![](assets/no-acc-usage-prob-level.png)


*Bild: Antal konton, trender och användningar inom olika sannolikhetsintervall*

+++

</th><th>

+++Dashboard för MVPD-program Kontrollpanelen för MVPD-användare skiljer sig något från programmeringsanvändarnas.

![](assets/dashboard-mvpd.png)


*Bild: MVPD&#39;s Dashboard*

## De viktigaste programmerarna inom segment efter övergripande poängdelning {#}

![](assets/top-programmers-panel.png)


*Bild: Panel med ledande programmerare i ett segment*
+++

</th>
</tr>

</table>

<!--
+++Dashboard for programmers

![dashboard of account IQ](assets/dashboard-capture.png)


*Figure: The dashboard*

## Average sharing score - aggregated for the current segment {#aggregated-sharing}

The Aggregated Sharing Score panel provides a top line readout summarizing the quantity and impact of sharing in terms of accounts and streaming volume.

The values help you understand the magnitude of credential sharing by your subscribers, hence providing a measure of the need to act upon it.

![](assets/aggregate-sharing-score.png)


*Figure: Average sharing score panel - aggregated for the current segment*

The following three metrics are components of the Average Sharing Score.

### Sharing level {#sharing-level}

The sharing level gauge shows the percentage of all your subscriber accounts (in the defined segment) that are shared, during the selected time frame.  

A value calculated based on an average of the sharing probability computed for every account in the set of selected MVPDs that has streamed from a one of the selected programmer channels during the selected time frame.

![](assets/sharing-level.png)


*Figure: Sharing level*

The Trend indicator shows the percentage change in the value of the metric in from the previous time frame.

### Usage from shared accounts {#usage-from-shared-accounts}

This gauge indicates what percent of the usage of all the subscriber accounts is from the shared accounts for the defined segment and time period. The gauge marks the ranges of usage (from shared accounts) on the scale of 0 to 100%. These ranges—named Low, Medium, High, and Abnormal—are based on the industry average.

You can also see the Trend indicator, which depicts a rise or fall in the usage from shared accounts as compared to the previous time frame.

![](assets/usage-4mshared-accounts.png)


*Figure: Usage from shared accounts*

### Overall sharing score {#overall-sharing-score}

Overall sharing score is composite of sharing scores including “Sharing level” and “z Usage from shared accounts”.

It provides a value meant to reflect the relative impact of sharing when compared to the industry. It’s purpose is similar to that of a credit score, summarizing the situation with a single number. But in this case, the higher the number the greater the potential harm.

![](assets/overall-sharing-score.png)


*Figure: Overall sharing score*

<!--### MVPDs in segment {#mvpd-in-segment}

It is a table of risk indices and accounts totals for the top MVPDs ranked by overall usage or account sharing.

![](assets/mvpds-in-segment.png)

### Industrywide overall sharing scores for MVPDs {#top-mvpds}

This table provides a comparative view of the different Aggregated Sharing Scores for the MVPDs in the segment.

>[!NOTE]
>
>This table uses overall industry data for comparative purposes, not the data represented by those MVPDs in the segment.

![](assets/top-mvpds.png)


*Figure: Top MVPDs in segment by overall score*

### Sharing score by channels and MVPDs {#sharin-score-by-channels-and-mvpds}

This table provides a comparative view of sharing scores of the selected channels for the MVPDs in the current segment.

![](assets/sharing-scores-by-channels-mvpds.png)


*Figure: Sharing scores by channels and MVPDs*

### Accounts sharing probability {#accounts-sharing-probability}

This chart partitions accounts into ranges of sharing probability quintiles from very low (0-20%) to very high (80=100%).

>[!NOTE]
>
>The bar graph uses a logarithmic scale.


![](assets/dashboard-ac-sharing-prob.png)


*Figure: Numbers and percentages of subscriber accounts in different sharing probability ranges*

### Number of accounts and usage by sharing probability level {#number-of-accounts-usage-sharing-probability}

This panel provides tabular view of  accounts partitioned into ranges of sharing probability quintiles from very low (0-20%) to very high (80-100%) with each quintile’s associated usage from shared accounts.

![](assets/no-acc-usage-prob-level.png)


*Figure: Number of accounts, trends, and usages falling in various probability ranges*

+++


+++Dashboard for MVPDs
The dashboard for MVPD users is slightly different from those of the programmer users.

![](assets/dashboard-mvpd.png)


*Figure: MVPD's Dashboard*

## Top programmers in segment by overall sharing score {#}

![](assets/top-programmers-panel.png)


*Figure: Panel showing top programmers in a segment*
+++


+++Dashboard for MVPDs
The dashboard for MVPD users is slightly different from those of the programmer users.

![](assets/dashboard-mvpd.png)


*Figure: MVPD's Dashboard*

## Top programmers in segment by overall sharing score {#}


![](assets/top-programmers-panel.png)


*Figure: Panel showing top programmers in a segment*
+++
-->
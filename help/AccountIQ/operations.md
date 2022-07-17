---
title: Operationer i konto IQ
description: Operationer med konto-IQ innefattar att vidta åtgärder för att utföra automatisering och gruppåtgärder på prenumerantkonton och spåra deras effekter.
source-git-commit: e61cca77bad4f01de871e300dc99d7368c283f2a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---


# Operationer {#operations-tab-next-steps}

När du har förstått dina abonnenters användningsmönster och identifierat lösenordsdelning för det valda segmentet (med rapporter och analyser i konto-IQ) kan du vidta riktade åtgärder för att minska lösenordsdelningen.

Funktionerna för åtgärder i konto-IQ hjälper dig att effektivt hantera och hantera delning av autentiseringsuppgifter genom fokuserade procedurer som kallas operationer. Här finns alternativ för att utforma en objektiv, skräddarsy riktade åtgärder (baserat på målet) för en viss grupp av abonnentkonton och automatisera deras utförande för en framtida varaktighet. Genom funktionerna kan ni inte bara skapa och utföra åtgärder, utan även mäta deras påverkan. Genom att mäta påverkan kan ni anpassa er strategi för att optimera effekten, vare sig det gäller konvertering av låntagare eller reducering av delning av autentiseringsuppgifter.

Visa **Operationer** sidmarkering **Operationer** option under **Åtgärder** i vänster navigering i kontots IQ-program. På sidan Åtgärder visas alla åtgärder som redan finns på konto-IQ-systemet tillsammans med deras information.

![](assets/operations-page.png)

*Bild: Lista och information om befintliga åtgärder i konto-IQ*

På sidan Åtgärder kan du:

* Visa en lista över åtgärder som redan finns i konto-IQ

* Visa åtgärdsinformation, till exempel:

   * status (Schemalagd, Körs, Avslutad, Fel eller Stoppad)

   * förlopp (i procent klart)

   * målgrupp (segment som åtgärden ska köras på)

   * schema (start- och slutdatum för åtgärden)

   * datum då operationen skapades och avslutades

* [Skapa ny åtgärd](/help/AccountIQ/operation-affecting-user-segment.md)

* [Visa åtgärdsrapporter](#operation-reports)

<!--* Search from the list of operations using Search field

* Stop an operation.

* Create a duplicate operation.

* [Configure columns of Operations details page](#configure-columns)-->

## Visa åtgärdsrapporter {#operation-reports}

Du kan analysera effekterna av en åtgärd genom att visa dess rapport. Så här visar du en åtgärdsrapport:

1. Markera åtgärdsnamnet på huvudsidan.

   Rapporten visas i form av ett staplat stolpdiagram.

   ![](assets/operation-impact-report.png)

   *Bild: Verksamhetsrapport för att visa verksamhetens konsekvenser*

   X-axeln ritar upp utvärderingsperioden och y-axeln ritar en variabel för att mäta effekten av operationen.

   I ovanstående bild är variabeln på y-axeln antalet konton. Om du tittar på diagrammet kan du jämföra antalet konton som finns i operationssegmentet med antalet konton som ligger utanför operationssegmentet vid en viss tidpunkt (t.ex. vecka 2 i operationsutvärderingsperioden). Därför kan du analysera hur antalet konton varierar inom operationssegmentet och utanför segmentet under utvärderingsperioden.

   Om din åtgärd var att skicka ut varningsmeddelanden till misstänkta konton, och konton i operationssegmentet var sådana med en delningssannolikhet på mer än 90 enheter och som använder mer än 5 enheter för att strömma innehåll, är konton i början av utvärderingsperioden mer än 7 miljoner. Detta antal ändras under utvärderingsperioden enligt diagrammet, vilket visar effekten av åtgärden. Baserat på utvärderingen kan du vidta korrigerande åtgärder för att misstänka konton, eller fortsätta med åtgärden, eller justera din strategi för att få bättre resultat för att förhindra delning av autentiseringsuppgifter.

2. Om du vill stänga rapporten och gå tillbaka till huvudsidan väljer du **Operationer** option under **Åtgärder** i vänster navigering.

<!--

![](assets/operations-details.png)

*Figure: Operation details*
## Configure columns {#configure-columns}

You can select the icon to **Configure columns** on the top of the operations table.

![](assets/config-columns.png)

*Figure: Configure columns of Operations details page*-->
---
seo-title: Uppdatera befintligt DRM-innehåll till molnbaserad DRM (valfritt)
title: Uppdatera befintligt DRM-innehåll till molnbaserad DRM (valfritt)
uuid: cfabeb06-210f-45af-b8a6-8e0b03a76103
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Uppdatera befintligt DRM-innehåll till molnbaserad DRM (valfritt) {#update-existing-drm-content-to-use-cloud-drm-optional}

Om du har ett befintligt bibliotek med innehåll som skyddas av Primetime DRM går det att ändra rubriken för det befintliga innehållet så att du kan använda DRM-tjänsten i Primetime Cloud i stället för att behöva paketera om eller kryptera de ursprungliga källfilerna. Om du ändrar rubriken för innehållet uppdateras DRM-metadata för innehållet i HLS-manifestet. Den utför ingen kryptering/omkryptering av den ursprungliga resursen. Detta kan vara ett bra alternativ om det ursprungliga källinnehållet inte är tillgängligt, eller om det finns problem med mängden resurser som krävs för att paketera om ett stort bibliotek.

Det går att använda Primetime DRM Java SDK för att uppdatera metadata programmatiskt. Dessutom kan kommandoradsverktyget som ingår i det här skyddspaketet även utföra den här uppgiften med hjälp av [!DNL OfflinePackager.jar] `-drm_refresh` alternativet.

## Information om sidhuvud {#section_3F3980D8E775450588C64E02A8448189}

Omrubriker måste uppdatera följande fält för att kunna använda CloudDRM:

* Licensserverns URL (till [!DNL ht<span></span>tps://access.adobeprimetime.com/flashaccessserver/axs_prod])
* Licensservercertifikat (till servercertifikatet för CloudDRM-licensen)
* Transportcertifikat (till CloudDRM-transportcertifikatet)
* Packager Credential (Till de paketerarautentiseringsuppgifter som du har aktiverat för användning med CloudDRM)

## Söka efter DRM-metadata {#section_28721CB7966F40708AEC8637F2E9BB72}

Innehåll som använder HTTP-teknik (till exempel HDS eller HLS) använder ett manifest som refererar till Adobe Access-DRM-metadata. I HDS refereras metadata av `<drmmeta>` -taggen och i HLS refereras det av `#EXT-X-FAXS-CM` -taggen. I båda fallen kan metadata infogas i manifestet som en base-64-kodad blob, eller refereras externt som en binär fil. Om metadata är inbäddade/infogade i manifestet kan du först behöva base64-avkoda metadata till binära data innan du använder dessa data för att instansiera DRM-metadata.

## Använda OfflinePacakger.jar {#section_37C2091856E44AA380D742C72B4DD1A7}

Ange `-drm_refresh option` till kommandoraden. En ny manifestfil skapas med uppdaterade DRM-metadata, men innehållet krypteras inte om.

## Använda Primetime DRM Java SDK för att ändra rubrik {#section_7EDBAC4C78DF4CD5BE8410EEAD8437A2}

Du kan uppdatera befintliga DRM-metadata med hjälp av Primetimes DRM-Java SDK (tidigare Adobe Access DRM) för en programmatisk metod. Mer information finns i kodexemplet i SDK:s [!DNL RegenerateMetadata.java] [!DNL /Reference Implmentation/Command Line Tools/samples/] paket. Adobe Access Java SDK ingår inte i detta CloudDRM Protection Kit och måste hämtas direkt från Adobe. Kontakta din Adobe-kontakt för mer information.
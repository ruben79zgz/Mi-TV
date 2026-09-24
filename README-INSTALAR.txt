TV RUSA PARA SS IPTV - INSTRUCCIONES
====================================

OBJETIVO
-------
Esta carpeta crea una lista M3U para SS IPTV en tu Philips.
La TV solo necesita conocer una URL. El repositorio de GitHub se ocupa de
comprobar los streams cada dia y cambiar a un enlace de respaldo conocido
si el principal deja de responder.

IMPORTANTE
----------
- Se priorizan emisiones gratuitas/publicas y endpoints de las propias
  cadenas o de sus CDN/proveedores conocidos.
- No se intenta saltar bloqueos geograficos.
- Primer Canal (Первый канал) usa MPEG-DASH (.mpd) en su directo web.
  Algunos Philips/SAPHI pueden no reproducir DASH; por eso aparece como
  "experimental". El resto de la lista intenta usar HLS (.m3u8).
- Si una cadena bloquea Espana o restringe el User-Agent, SS IPTV puede no
  reproducirla aunque la URL este viva.

PASO 1 - CREAR EL REPOSITORIO
-----------------------------
1. En GitHub crea un repositorio PUBLICO llamado exactamente:
   TV-Rusa
2. Entra en el repositorio y pulsa "uploading an existing file".
3. Sube TODO el contenido de esta carpeta (no el ZIP).
   Importante: tv-rusa.m3u, channels.json, logos, scripts y .github deben
   quedar dentro del repositorio.
4. Pulsa Commit changes.

NO HACE FALTA GITHUB PAGES.

PASO 2 - URL QUE PONDREMOS EN SS IPTV
-------------------------------------
Si tu usuario de GitHub es ruben79zgz y el repositorio se llama TV-Rusa,
la URL de la lista sera:

https://raw.githubusercontent.com/ruben79zgz/TV-Rusa/main/tv-rusa.m3u

PASO 3 - CONFIGURAR SS IPTV EN LA PHILIPS
-----------------------------------------
1. Abre SS IPTV.
2. Settings / Ajustes.
3. Content / Contenido.
4. External playlists / Listas externas.
5. Add / Anadir.
6. Nombre: TV Rusa
7. URL: pega la URL de arriba.
8. Save / Guardar.
9. Vuelve a la pantalla principal y abre TV Rusa.

PASO 4 - ACTUALIZACION AUTOMATICA
---------------------------------
GitHub Actions ejecutara cada dia:
  scripts/build_playlist.py

El programa:
- comprueba los enlaces conocidos;
- mantiene el anterior si no encuentra uno mejor;
- prueba enlaces alternativos del mismo canal;
- puede consultar la lista publica iptv-org, PERO solo acepta candidatos
  cuyo dominio este expresamente permitido para ese canal en channels.json;
- vuelve a generar tv-rusa.m3u.

Tambien puedes forzar la revision:
GitHub -> Actions -> Revisar streams TV -> Run workflow.

COMO ANADIR O CAMBIAR UN CANAL
------------------------------
Edita channels.json. NO edites tv-rusa.m3u como solucion permanente,
porque el robot puede regenerarlo.

En cada canal, "candidates" contiene las URLs permitidas en orden de
preferencia. Si me pasas una URL nueva, puedo decirte exactamente donde
ponerla.

CANALES INCLUIDOS EN ESTA PRIMERA VERSION
-----------------------------------------
- Первый канал (experimental / DASH)
- Россия 1 HD
- Россия 24 HD
- Россия-Культура HD
- НТВ HD
- ТВ Центр
- МИР HD
- МИР 24
- Москва 24
- Липецкое время
- РБК
- Звезда HD
- Смотрим 100% Детское
- Смотрим 100% Классика

Cuando comprobemos cuales funcionan realmente en TU Philips desde Espana,
podremos ampliar la lista con 5 канал, Карусель, ОТР, РТР-Планета y otros
sin llenar la TV de enlaces dudosos.

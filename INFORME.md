# Informe — Grupo 3


## 2.5 — El secreto

Subimos  un `.env` con una contraseña dentro.
El revisor lo pilló al mirar los commits de la PR y pidió que se quitara.
Se sacó del repo con `git rm --cached .env` (sin borrarlo del ordenador) y
se metió `.env` en el `.gitignore` para que no vuelva a pasar.

Pregunta: la contraseña sigue en el historial de un repo público, ¿qué
habría que hacer en un caso real y por qué quitar el fichero no lo arregla?

Aunque quites el fichero, la contraseña se queda guardada en el commit
donde se subió por primera vez, y como el repo es público cualquiera
puede verla mirando el historial. Quitar el fichero solo hace que ya no
se vea en la versión actual, pero no borra que en algún momento estuvo ahí.

En un caso real lo primero sería cambiar esa contraseña ya, porque hay que
asumir que la ha podido ver cualquiera.

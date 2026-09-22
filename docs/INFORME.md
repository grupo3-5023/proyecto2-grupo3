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

## 3 — Preguntas GitHub Desktop

¿Qué muestra mejor Desktop?
El diff se ve mucho más claro que con git diff, con colores y todo. El
historial con el gráfico de ramas también se entiende mejor de un vistazo
que el --graph de la terminal. Y cuando hay conflicto avisa directamente
de qué fichero es, sin tener que buscarlo a mano.

¿Qué hemos tenido que hacer en la web o terminal porque Desktop no lo hace?
- Cambiar el rol de los colaboradores y gestionar la organización, eso
  solo se puede desde la web
- Crear y configurar la protección de main (branch rules), tampoco está
  en Desktop
- Aprobar las PRs y dejar comentarios de revisión, desde Desktop solo
  puedes crear la PR pero no revisarla
- Nos dio un bug al comitear en main (el botón se quedaba pillado sin
  reaccionar), tuvimos que reintentarlo varias veces

## Capturas

![Shortlog](capturas/1.1-shortlog.png)
![Grafo de la Fase 1](capturas/1.2-graph.png)
![Miembros y roles](capturas/2.1-miembros.png)
![SECURITY.md con última revisión](capturas/2.2-security.png)
![Protección de main](capturas/2.3-proteccion.png)

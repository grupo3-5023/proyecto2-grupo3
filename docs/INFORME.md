# Informe — Grupo 3

## 1.2 — Tipo de merge de contacto-a

Fue fast-forward. Como main no había cambiado desde que creamos la rama,
git solo movió el puntero hacia adelante, no tuvo que mezclar nada. Por eso
en el gráfico no sale como un commit de merge normal, solo sigue en línea
recta hasta el commit de contacto-a.

## 2.2 — Conflicto en pull

Al hacer push por orden (B, C, A), al segundo y tercero les salió esto:

! [rejected]        main -> main (fetch first)
error: failed to push some refs to '...'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally. This is usually caused by another repository pushing to
hint: the same ref.

¿Por qué unos cambios dan conflicto y otros no?
Porque cada uno tocaba una línea distinta del checklist, así que git las
junta solo sin problema. Pero la línea de "Última revisión" la tocábamos
los tres a la vez, entonces git no sabe cuál de las tres versiones dejar
y por eso salta el conflicto. Si tocas líneas distintas no hay lío, pero
si tocáis la misma línea, toca resolverlo a mano sí o sí.

## 2.3 — Proteger main

Al intentar subir directo a main (ya protegida) salió este error:

remote: error: GH013: Repository rule violations found for refs/heads/main.
remote:
remote: - Changes must be made through a pull request.
remote:
! [remote rejected] main -> main (push declined due to repository rule violations)
error: failed to push some refs to '...'

## 2.4 — Conflicto resuelto en el editor web

También resolvimos un conflicto sin usar terminal ni Desktop, directamente
en el editor de conflictos que tiene GitHub en la propia PR (botón
"Resolve conflicts"). Dos ramas cambiaban la misma línea de "Última
revisión" con texto distinto, y al fusionar la segunda salió el conflicto
ahí mismo en la web.

## 2.5 — El secreto

Subimos un `.env` con una contraseña dentro.
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

## 2.5 (extra) — Secret scanning y push protection

El Admin activó Secret Protection y Push Protection en la organización.
Subimos otro .env con un token falso (ghp_1234567890abcdefghijklmnopqrstuvwxyz)
para ver si lo bloqueaba, y el push pasó sin ningún problema, no lo detectó.
Suponemos que es porque GitHub no solo mira el prefijo "ghp_", sino que
valida el formato real del token (longitud y caracteres concretos), y al
ser uno inventado a mano no encaja con el patrón real, así que no salta
la alerta.

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

## Preguntas (Román: 1-3)

**1. ¿Por qué el segundo push fue rechazado y qué hace pull por debajo?**

Porque B ya había subido su commit antes que C, entonces cuando C fue a
subir el suyo, su copia local estaba desactualizada respecto al remoto y
git no te deja hacer push así. git pull en el fondo hace dos cosas: un
fetch (trae los commits nuevos sin tocar tu rama) y luego un merge (los
mete en tu rama local).

**2. Fast-forward vs merge commit en nuestro historial**

La fusión de contacto-a fue fast-forward, porque main no se había movido
desde que creamos la rama, git solo movió el puntero para adelante sin
crear commit nuevo. La de contacto-b sí generó un merge commit, porque
main ya había avanzado y hubo que juntar las dos historias con un commit
nuevo que tiene dos padres.

**3. Por qué las filas no dan conflicto pero última revisión sí**

Porque cada fila está en una línea distinta, entonces git puede meter los
cambios de cada uno sin pisarse. Pero última revisión la tocábamos los
tres a la vez en la misma línea, y ahí git no sabe qué versión quedarse,
así que toca decidirlo a mano.

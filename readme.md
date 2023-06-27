# EJERCICIO 1

### **¿Que comando utilizaste en el paso 11? ¿por qué?**

En este punto, he hecho un **git reset --hard HEAD~1** que desace el último commit (como un **git reset HEAD~1**) y ademas desace los cambios del working copy (como un **git restore**).

### **¿Que comando o comandos utilizaste en el paso 12? ¿por qué?**

Primero realicé un **git reflog** para ver todos los movimientos de HEAD. Busqué la creacción del commit B y copié su hash (769fe7a). A continuación hice un **git reset** al hash copiado, con lo que el HEAD y la rama a la que apunta (styled) se mueven a este commit B, deshaciendo el paso anterior.

### **El merge del paso 13, ¿causó algún conflicto? ¿por qué?**

El merge no causa ningún conflicto. Simplemente dice que ya está al día. Como la rama main no tiene ningún commit que no vea styled en este momento, esta operación no hace nada, ya que main está mergeado (incluido) en styled.

### **El merge del paso 19 ¿Causó algún conflicto? por qué?**

Si. Se genera un conflicto. En el fichero, hemos hecho cambios en las mismas líneas en ambas ramas, por lo que git no sabe con que quedarse. Para solucionarlo, editamos el fichero, observamos donde nos dice que hay conflictos y los solucionamos todos. Nos quedamos con la versión de la rama styled, tal y como dice el enunciado. A continuación hacemos un **git add Gitnuestro.md** y un **git commit -m "D. Mergeadas ramas styled y htmlify"**

### **El merge del paso 21 ¿Causó algún conflicto? ¿por qué?**

Ho causó ningún conflicto, ya que simplemente hemos movido main dentro de rama styled. Se realiza un fast forward y esto no puede generar conflictos

### **¿Qué comando o comandos utilizaste en el paso 25?**

He usado git log, con su versión: **git log --graph --branches --oneline**. Lo tengo definido con un alias (*git gr*).

El grafo queda: 

```
* 9895b66 (HEAD -> main, tag: title) E. Añado título al texto.
*   8580424 D. Mergeadas ramas styled y htmlify. Nos quedamos con los cambios de styled.
|\
| * a7bf404 (tag: htmlify) C. Añadido, al texto original, formato html
* | 769fe7a (tag: styled) B. Modificado archivo con estilo.
|/
* 10ff78f (tag: inicial) A. Commit inicial. Añado el fichero GitNuestro.md
```

### **El merge del paso 26, ¿podría ser un fast forward? ¿por qué?**

Si podria ser, ya que como están ambos en la misma rama, no hay opciones de conflicto.

### **¿Qué comando o comandos utilizaste en el paso 27?**

He usado **git reset HEAD~1**. Compruebo con *git status* que el fichero modificado está en el working área y con *git log*, que la rama main y HEAD están en el commit anterior. El último commit no se ve en el log. Tengo main-HEAD apuntando al commit D y title apuntando al E.

### **¿Qué comando o comandos utilizaste en el paso 28?**

Para descartar los cambios que tengo en el working copy, he hecho un **git restore GitNuestro.md**. Ejecuto *git status* y compruebo que el fichero ya no tiene modificaciones.

### **¿Qué comando o comandos utilizaste en el paso 29?**

He usado el comando **git branch -D title**, ya que no puedo usar **-d** porque me dice que la rama no está completamente mergeada. Al eliminar la rama, los commits E (poner título) y F (merge desecho) no quedan accesibles a ninguna rama.

### **¿Qué comando o comandos utilizaste en el paso 30?**

Para rehacer el merge que hemos desecho, primero uso **git reflog** para ver todos los movimientos de HEAD. Comenzando desde arriba, busco el hash del commit F (f45eb94) para moverme a el. Una vez localizado, hago un **git reset --hard f45eb94** a este hash que me moverá la rama main con el HEAD a este commit.

### **¿Qué comando o comandos utilizaste en el paso 32?**

Para regresar al commit inicial, con **git reflog** busco el hash del primer commit (10ff78f) y voy, con **git reset --hard 10ff78f**, a este hash.

### **¿Qué comando o comandos utilizaste en el paso 33?**

Para volver al estado final, con **git reflog** busco el commit del último merge (f45eb94) y me desplazo a el con un **git reset --hard f45eb94**

El grafo final queda (antes de añadir el readme.md):

```
*   f45eb94 (HEAD -> main) F. Merge de main absorvendo a title.
|\
| * 9895b66 (tag: title) E. Añado título al texto.
|/
*   8580424 D. Mergeadas ramas styled y htmlify. Nos quedamos con los cambios de styled.
|\
| * a7bf404 (tag: htmlify) C. Añadido, al texto original, formato html
* | 769fe7a (tag: styled) B. Modificado archivo con estilo.
|/
* 10ff78f (tag: inicial) A. Commit inicial. Añado el fichero GitNuestro.md
````
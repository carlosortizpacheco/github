![](https://img.shields.io/static/v1?label=technology&message=git&color=blue)
![](https://img.shields.io/static/v1?label=technology&message=github&color=red)
![](https://img.shields.io/static/v1?label=school&message=platzi&color=green)

# Github
Documentación de comandos y tips de github. Tomado del curso de Platzi.

## Que es Git ?
- Git es un sistema de control de versiones que nos ayuda a guardar el historial de cambios y crecimiento de los archivos del proyecto.
- Git está optimizado para guardar todos estos cambios de forma atómica e incremental (aplica cambios sobre los últimos cambios, estos sobre los cambios anteriores y así sucesivamente).
- El comando para iniciar Git es:
`git init`
- El comando que se usa para que nuestro repositorio sepa de la existencia (no almacena los cambios de forma automatica, los aloja en el **staging area**) de un archivo es:
`git add`
- El comando que sirve para almacenar los cambios definitivamente es :
`git commit -m "Mensaje del commit"`
- Si quieres guardar tus cambios en un servidor remoto, utiliza el comando:
`git push`

## Comandos básicos para el manejo de la terminal
- **pwd**, muestra la ruta de carpetas en la que te encuentras ahora mismo.
- **mkdir**, permite crear carpetas `mkdir nombreCarpeta`
- **touch**, permite crear archivos `touch nombreArchivo`
- **rm**, permite borrar archivos o carpetas `rm -rf nombreCarpeta` o `rm nombreArchivo`
- **cat**, permite ver el contenido de un archivo `cat nombreArchivo`
+ **ls**, permite ver una lista de los archivos en la carpeta en la que nos encontremos. 
  + `ls -a` permite ver todos los archivos, incluidos los ocultos.
  + `ls -l` permite ver todos los archivos como una lista.
- **cd**, permite cambiarte a otra carpeta `cd nombreCarpeta`.
- **history**, permite ver un historial de los comandos que hemos ejecutado. `history`
- **!numeroDeHistorial**, permite volver a ejecutar un comando del historial `!5`
- **clear** permite limpiar la terminal.

## Ciclo básico de Git
+ Cuando ejecutamos `git init`, ocurren dos cosas:
  + Crear una carpeta `.git`, donde se guardará toda la base de datos con cambios atómicos de nuestro proyecto.
  + Crear un área que conocemos como **Staging**, que guardará temporalmente nuestros archivos.

### Ciclo de vida o estados de los archivos en Git
+ Cuando trabajamos con Git nuestros archivos pueden vivir y moverse entre 4 diferentes estados:
  + **Archivos Tracked** archivos que viven dentro de `Git`, no tienen cambios pendientes y sus últimas actualizaciones han sido guardadas en el repositorio gracias a los comandos `git add` y `git commit`.
  + **Archivos Staged** archivos en **Staging**. Viven dentro de Git y hay registro de ellos porque han sido afectados por el comando `git add`, aunque no sus últimos cambios. no han sido guardados definitivamente en el repositorio porque falta ejecutar el comando `git commit`.
  + **Archivos Unstaged** entiéndelos como archivos “Tracked pero Unstaged”. Son archivos que viven dentro de Git pero no han sido afectados por el comando `git add` ni mucho menos por `git commit`. Git tiene un registro de estos archivos, pero está desactualizado, sus últimas versiones solo están guardadas en el disco duro.
  + **Archivos Untracked** archivos que NO viven dentro de Git, solo en el disco duro. Nunca han sido afectados por `git add`, así que Git no tiene registros de su existencia.

### Comandos para mover archivos entre los estados de Git
+ `git status` permite ver el estado de todos nuestros archivos y carpetas.
+ `git add` mueve archivos de Untracked o Unstaged al estado Staged. 
  + `git nombre-del-archivo-o-carpeta` añade archivos y carpetas individuales 
  + `git add -A` añade todos los archivos de nuestro proyecto (tanto Untrackeds como unstageds).
- `git reset HEAD` saca archivos del estado Staged para devolverlos a su estado anterior. Si los archivos venían de Unstaged, vuelven allí. Y lo mismo se venían de Untracked.
- `git commit` mueve archivos de Unstaged a Staged (los archivos han sido guardado o actualizados en el repositorio). Git nos pedirá que dejemos un mensaje para recordar los cambios que hicimos y podemos usar el argumento -m para escribirlo `git commit -m "mensaje"`.
+ `git rm` este comando necesita alguno de los siguientes argumentos para poder ejecutarse correctamente:
  + `git rm --cached` mueve los archivos que le indiquemos al estado Untracked.
  + `git rm --force` Elimina los archivos de Git y del disco duro. Git guarda el registro de la existencia de los archivos, por lo que podremos recuperarlos si es necesario.
  
## Branch (rama) y Merge en Git
- Todos los commits se aplican sobre una rama (rama master) y creamos nuevas ramas, a partir de esta, para crear flujos de trabajo independientes.
- Crear una nueva rama es copiar un commit (de cualquier rama), pasarlo a otro lado (a otra rama) y continuar el trabajo de una parte específica de nuestro proyecto sin afectar el flujo de trabajo principal (que continúa en la rama master o la rama principal).
- Todo lo que esté en la rama master va a **producción**, las nuevas features, características y experimentos van en una rama **development** (para unirse a master cuando estén definitivamente listas) y los issues o errores se solucionan en una rama **hotfix** para unirse a master tan pronto como sea posible.
- `git checkout -b nombreNuevaRama`, crea una nueva Rama o Branch

## Analizar cambios con Git
- `git show`, muestra los cambios que han existido sobre un archivo y es muy útil para detectar cuándo se produjeron ciertos cambios, qué se rompió y cómo lo podemos solucionar. 
- `git diff IDcommitA IDcommitB`, si queremos ver la diferencia entre una versión y otra, no necesariamente todos los cambios desde la creación del archivo.
- `git log`, obtener el ID de tus commits.

## Volver en el tiempo con reset y checkout
- `git checkout + ID`, permite viajar en el tiempo. Podemos volver a cualquier versión anterior de un archivo específico o incluso del proyecto entero. Esta también es la forma de crear ramas y movernos entre ellas.
+ `git reset`, forma "ruda" de hacerlo. **No solo “volvemos en el tiempo”, sino que borramos los cambios que hicimos después de este commit**.
  + `git reset --hard`, borrando toda la información que tengamos en el área de staging (**y perdiendo todo para siempre**).
  + `git reset --soft`,  mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior.

 ### git rm
Elimina archivos de Git sin eliminar su historial del sistema de versiones. Esto quiere decir que si necesitamos recuperar el archivo solo debemos “viajar en el tiempo” y recuperar el último commit antes de borrar el archivo en cuestión.

+ Recuerda que `git rm` no puede usarse así nomás. Debemos usar uno de los flags para indicarle a Git cómo eliminar los archivos que ya no necesitamos en la última versión del proyecto.
  + `git rm --cached`, elimina los archivos del área de Staging y del próximo commit pero los mantiene en nuestro disco duro
  + `git rm --force`, elimina los archivos de Git y del disco duro. Git siempre guarda todo, por lo que podemos acceder al registro de la existencia de los archivos, de modo que podremos recuperarlos si es necesario.

### git reset
Este comando nos ayuda a volver en el tiempo. Pero no como git checkout que nos deja ir, mirar, pasear y volver. **Volvemos al pasado sin la posibilidad de volver al futuro. Borramos la historia y la debemos sobreescribir. No hay vuelta atrás**.

- `git reset --hard`, borra toda la información que tengamos en el área de staging (**y perdiendo todo para siempre**). Borra todo. Todo todito, absolutamente todo. Toda la información de los commits y del área de staging se borra del historial.
- `git reset --soft`, mantiene allí los archivos del área de staging para que podamos aplicar nuestros últimos cambios pero desde un commit anterior. Borramos todo el historial y los registros de Git pero guardamos los cambios que tengamos en Staging, así podemos aplicar las últimas actualizaciones a un nuevo commit.
- `git reset HEAD`, saca archivos del área de Staging. No para borrarlos ni nada de eso, solo para que los últimos cambios de estos archivos no se envíen al último commit, a menos que cambiemos de opinión y los incluyamos de nuevo en staging con `git add`.

## Flujo de trabajo básico con un repositorio remoto
- `git clone url_del_servidor_remoto`, descarga los archivos de la última versión de la rama principal y todo el historial de cambios en la carpeta .git.
- `git push`, luego de hacer `git add` y `git commit` debemos ejecutar este comando para mandar los cambios al servidor remoto.
- `git fetch`, lo usamos para traer actualizaciones del servidor remoto y guardarlas en nuestro repositorio local.
- `git merge`, también usamos el comando `git fetch` con servidores remotos. Lo necesitamos para combinar los últimos cambios del servidor remoto y nuestro directorio de trabajo.
- `git pull`, básicamente, `git fetch` y `git merge` al mismo tiempo.

 ### Introducción a las ramas o branches
- Las ramas son la forma de hacer cambios en nuestro proyecto sin afectar el flujo de trabajo de la rama principal.
- La cabecera o HEAD representan la rama y el commit de esa rama donde estamos trabajando. Por defecto, es el último commit de nuestra rama principal. Pero podemos cambiarlo al crear una rama (`git branch rama`, `git checkout -b rama`) o movernos en el tiempo a cualquier otro commit de cualquier otra rama con los comandos (`git reset id-commit`, `git checkout rama-o-id-commit`).

### Fusión de ramas con Git merge
- `git merge`, permite crear un nuevo commit con la combinación de dos ramas (la rama donde nos encontramos cuando ejecutamos el comando y la rama que indiquemos después del comando).
- Al ejecutar el comando `git checkout` para cambiar de rama o commit **puedes perder el trabajo que no hayas guardado. Guarda tus cambios antes de hacer git checkout**.

### Resolución de conflictos al hacer un merge
- Git nunca borra nada a menos que nosotros se lo indiquemos. Cuando usamos los comandos `git merge` o `git checkout` estamos cambiando de rama o creando un nuevo commit, no borrando ramas ni commits (recuerda que puedes borrar commits con `git reset` y ramas con `git branch -d`).
- Siempre debemos crear un nuevo commit para aplicar los cambios del merge. Si Git puede resolver el conflicto hará commit automáticamente.
- Los archivos con conflictos por el comando `git merge` entran en un nuevo estado que conocemos como Unmerged. Funcionan muy parecido a los archivos en estado Unstaged, algo así como un estado intermedio entre Untracked y Unstaged, solo debemos ejecutar `git add` para pasarlos al área de staging y `git commit` para aplicar los cambios en el repositorio.

## Github

### Cómo funcionan las llaves públicas y privadas
- Las llaves públicas y privadas nos ayudan a cifrar y descifrar nuestros archivos de forma que los podamos compartir sin correr el riesgo de que sean interceptados por personas con malas intenciones.
+ La forma de hacerlo es la siguiente:
  + Ambas personas deben crear su llave pública y privada.
  + Ambas personas pueden compartir su llave pública a las otras partes (recuerda que esta llave es pública, no hay problema si la “interceptan”).
  + La persona que quiere compartir un mensaje puede usar la llave pública de la otra persona para cifrar los archivos y asegurarse que solo puedan ser descifrados con la llave privada de la persona con la que queremos compartir el mensaje.
  + El mensaje está cifrado y puede ser enviado a la otra persona sin problemas en caso de que los archivos sean interceptados.
  + La persona a la que enviamos el mensaje cifrado puede usar su llave privada para descifrar el mensaje y ver los archivos.
  + Puedes compartir tu llave pública pero nunca tu llave privada.

### Configura tus llaves SSH en local
- Generar tus llaves SSH. Recuerda que es muy buena idea proteger tu llave privada con una contraseña.
`ssh-keygen -t rsa -b 4096 -C "tu@email.com"`

#### En Windows y Linux:
-Encender el "servidor" de llaves SSH de tu computadora:
`eval $(ssh-agent -s)`
-Añadir tu llave SSH a este "servidor":
`ssh-add ruta-donde-guardaste-tu-llave-privada`

#### En Mac:
-Encender el "servidor" de llaves SSH de tu computadora:
`eval "$(ssh-agent -s)"`

### Conexión a GitHub con SSH
- Luego de crear nuestras llaves SSH podemos entregarle la llave pública a GitHub para comunicarnos de forma segura y sin necesidad de escribir nuestro usuario y contraseña todo el tiempo.
- Entrar a la Configuración de llaves SSH en GitHub, crear una nueva llave con el nombre que le quieras dar y el contenido de la llave pública de tu computadora.
- Ahora podemos actualizar la URL que guardamos en nuestro repositorio remoto, solo que, en vez de guardar la URL con HTTPS, vamos a usar la URL con SSH:

`git remote set-url origin url-ssh-del-repositorio-en-github`


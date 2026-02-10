# infra-cycle

Este repositorio implementa un sistema complejo de entrega de software, desde el código fuente hasta la ejecución, integrado CI/CD, contenedores e infrastructura como código.

### Borrar

---

### Estado incial - ¿Qué tenemos?

- Un repositorio de código
- Código de una aplicación
- Definición de infrastructura
- Definición de pipeline

**Nada ocurre, hasta que alguien haga un cambio**

### Evento disparador - algo cambia

Puede ser: git + [ push, merge, tag, request]

El evento, no ejecuta lógica, sino sólo despierta al sistema

### Pipeline toma control

Un **runner** -> GitHub Actions, Jenkins recibe el evento

`El pipeline se convierte en el **orquestador temporal**`

No se construye, no despliega, tampoco dockeriza. Sino más bien, prepara el entorno y decide qué pasará

### Validación temprana

Antes de gastar los recursos (tests, lint, formato, checks rápidos). El objetivo es que si falla, lo ha rápido y sea barato.

> En caso de falla:
> El sistema se detiene
> Nada se empaqueta
> Nada se publica


### Generación de build de la aplicación

Ahora sí, aquí el código se vuelve algo ejecutable, puede ser: binario, jar, artifacts, lo que sea, de tal manera, que sea un artefacto de una aplicación

**Importante:**
- Todavía no es imagen
- Todavía no vive en el mundo

> Sólo es software listo, para ser empaquetado


### Dockerización

Aquí está el cambio de dominio. El artefacto creado de la aplicación (*build process*)

- Entra en un Dockerfile
- Se convierte en una imagen - blueprint

¿Resultado? Una imagen inmutable

### Registro de imagenes (estado intermedio)

La imagen no se ejecuta, ni se hace algún deploy, se requiere **empujarla** a un registro.

Puede ser: DockerHub, Registry local, registry provado

> El registro es una bodega, no un runtime
> En este registro, la imagen vive, tiene versión, puede ser consumida por otros sistemas

En este paso, se desacopla el **build** de **run**



---



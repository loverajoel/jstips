# Como enviar tu tip

Para agregar tu tip a la lista, debes forkear el repositorio y agregar tu tip en un nuevo archivos en el direcctorio correcto (de acuero el lenguage). El nombre del archivo deberia ser '2016-xx-xx-nombre-de-tu-tip'.

Utilice [este formato](https://github.com/loverajoel/jstips/blob/gh-pages/POST_TEMPLATE.md) para escribir su tip. 

### Requisitos

- Su tip debe ser legible en menos de dos minutos.
- Puede añadir enlaces a otros sitios o videos que dan una visión más clara es bienvenido.
- Se marcará el código JS con ```js
- No Mencione "JavaScript" en el título (como nuestros consejos son respecto de todos modos)
- Use comillas invertidas (`) para marcar código en el campos **title** y/o **tip-tldr**. _Precaucion_: Ambos valores no deben comenzar con acentos abiertos!


Una vez que su tip está listo, [issue a pull request](https://help.github.com/articles/using-pull-requests/) con esta [PR template](https://github.com/loverajoel/jstips/blob/gh-pages/PULL_REQUEST_TEMPLATE.md) y su tip será revisado (véase más adelante).

# Notas

Deje la fecha y el número de tip con **xx**. Cuando el PR es `ready to merge`, le diremos los números correctos. Por favor, también [squash] (https://davidwalsh.name/squash-commits-git) sus confirmaciones.

# Flujo del Tip

**Tip proposal** ⇒ **Tip under review** ⇒ **Tip ready to merge**

- Cuando se envía un tip, tiene que pasar el proceso de revisión y mientras eso sucede, su estado es `under review`.
- Después de que el tip sea revisado por 5 personas y han dado (:shipit:), el tip esta `ready to merge`.
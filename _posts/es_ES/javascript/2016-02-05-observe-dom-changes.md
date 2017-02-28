---
layout: post

title: Observar los cambios del DOM en extensiones.
tip-number: 36
tip-username: beyondns
tip-username-profile: https://github.com/beyondns
tip-tldr: AL desarrollar extensiones de sitios existentes no es tan fácil interactuar con el DOM a causa de la moderna dinamica de javascript.


redirect_from:
  - /es_es/observe-dom-changes/

categories:
    - es_ES
    - javascript
---
[MutationObserver](https://developer.mozilla.org/en/docs/Web/API/MutationObserver) es una solución para escuchar a los cambios del DOM y hacer lo que quiere hacer con los elementos cuando cambiaron. En el siguiente ejemplo, hay una cierta emulación del contenido de la carga dinámica con una ayuda de contadores de tiempo, después de la primera creación del elemento "target" pasa "subTarget".
En código de la extensión en primer lugar rootObserver funciona hasta la apariencia del targetElement luego empieza el elementObserver. Esta observación en cascada ayuda a obtener finalmente el momento en que se encuentra subTargetElement.
Es útil para desarrollar extensiones a los sitios complejos con contenido de carga dinámica.

```js
const observeConfig = {
    attributes: true,
    childList: true,
    characterData: true,
    subtree: true
};

function initExtension(rootElement, targetSelector, subTargetSelector) {
    var rootObserver = new MutationObserver(function(mutations) {
        console.log("Inside root observer");
        targetElement = rootElement.querySelector(targetSelector);
        if (targetElement) {
            rootObserver.disconnect();
            var elementObserver = new MutationObserver(function(mutations) {
                console.log("Inside element observer")
                subTargetElement = targetElement.querySelector(subTargetSelector);
                if (subTargetElement) {
                    elementObserver.disconnect();
                    console.log("subTargetElement found!")
                }
            })
            elementObserver.observe(targetElement, observeConfig);
        }
    })
    rootObserver.observe(rootElement, observeConfig);
}

(function() {

    initExtension(document.body, "div.target", "div.subtarget")

    setTimeout(function() {
        del = document.createElement("div");
        del.innerHTML = "<div class='target'>target</div>"
        document.body.appendChild(del)
    }, 3000);


    setTimeout(function() {
        var el = document.body.querySelector('div.target')
        if (el) {
            del = document.createElement("div");
            del.innerHTML = "<div class='subtarget'>subtarget</div>"
            el.appendChild(del)
        }
    }, 5000);

})()
```


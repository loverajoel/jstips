---
layout: post

title: Observe DOM changes in extensions
tip-number: 36
tip-username: beyondns
tip-username-profile: https://github.com/beyondns
tip-tldr: When you develop extensions to existent sites it's not so easy to play with DOM 'cause of modern dynamic javascript.


redirect_from:
  - /en/observe-dom-changes/

categories:
    - en
    - javascript
---
[MutationObserver](https://developer.mozilla.org/en/docs/Web/API/MutationObserver) is a solution to listen DOM changes and do what you want to do with elements when they changed. In following example there is some emulation of dynamic content loading with help of timers, after first "target" element creation goes "subTarget".
In extension code firstly rootObserver works till targetElement appearance then elementObserver starts. This cascading observing helps finally get moment when subTargetElement found.
This useful to develop extensions to complex sites with dynamic content loading.

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
                console.log("Inside element observer");
                subTargetElement = targetElement.querySelector(subTargetSelector);
                if (subTargetElement) {
                    elementObserver.disconnect();
                    console.log("subTargetElement found!");
                }
            });
            elementObserver.observe(targetElement, observeConfig);
        }
    });
    rootObserver.observe(rootElement, observeConfig);
}

(function() {

    initExtension(document.body, "div.target", "div.subtarget");

    setTimeout(function() {
        del = document.createElement("div");
        del.innerHTML = "<div class='target'>target</div>";
        document.body.appendChild(del);
    }, 3000);


    setTimeout(function() {
        var el = document.body.querySelector('div.target');
        if (el) {
            del = document.createElement("div");
            del.innerHTML = "<div class='subtarget'>subtarget</div>";
            el.appendChild(del);
        }
    }, 5000);

})();
```


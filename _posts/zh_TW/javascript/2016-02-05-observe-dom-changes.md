---
layout: post

title: 觀察在擴充中 DOM 的變化
tip-number: 36
tip-username: beyondns
tip-username-profile: https://github.com/beyondns
tip-tldr: 由於現代動態的 JavaScript，當你在現有的網站開發擴充時，操作 DOM 並不容易。


redirect_from:
  - /zh_tw/observe-dom-changes/

categories:
    - zh_TW
    - javascript
---
[MutationObserver](https://developer.mozilla.org/en/docs/Web/API/MutationObserver) 是一個 listen DOM 的改變以及元素變化時的解決方法。在下面的範例是使用計時器模擬了內容動態載入，在第一個元素「target」建立後，接著建立「subTarget」。
在擴充的程式碼中，首先 `rootObserver` 執行直到 `targetElement` 出現，然後 `elementObserver` 才開始執行。這個級聯觀察有助於直到最後發現 `subTargetElement`。
這個在開發擴充複雜的網站與動態內容載入時相當有用。

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
            })
            elementObserver.observe(targetElement, observeConfig);
        }
    })
    rootObserver.observe(rootElement, observeConfig);
}

(function() {

    initExtension(document.body, "div.target", "div.subtarget");

    setTimeout(function() {
        del = document.createElement("div");
        del.innerHTML = "<div class='target'>target</div>"
        document.body.appendChild(del);
    }, 3000);


    setTimeout(function() {
        var el = document.body.querySelector('div.target');
        if (el) {
            del = document.createElement("div");
            del.innerHTML = "<div class='subtarget'>subtarget</div>"
            el.appendChild(del);
        }
    }, 5000);

})();
```

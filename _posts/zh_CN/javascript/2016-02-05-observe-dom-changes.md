---
layout: post

title: 扩展插件中观察DOM的变化
tip-number: 36
tip-username: beyondns
tip-username-profile: https://github.com/beyondns
tip-tldr: 当你为存在的网站开发扩展插件时，由于现代的动态Javascript，操作DOM并不是很容易。


redirect_from:
  - /zh_cn/observe-dom-changes/

categories:
    - zh_CN
    - javascript
---
[MutationObserver](https://developer.mozilla.org/zh-CN/docs/Web/API/MutationObserver)是监听DOM变化与当元素变化时做适当操作的一个解决方法。在下面的例子中我们使用计时器模拟了内容的动态加载，第一个元素"target"创建后，创建"subTarget"。
在扩展中的代码，`rootObserver`首先开始工作，直到`targetElement`被创建后`rootObserver`停止，然后`elementObserver`开始工作。这个级联观测可以在发现`subTargetElement`时提醒你。
这个方法在为动态加载内容的网站开发扩展插件时，是很有用的。

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


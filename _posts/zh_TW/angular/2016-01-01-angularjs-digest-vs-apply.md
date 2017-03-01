---
layout: post

title: AngularJs - $digest vs $apply
tip-number: 01
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: JavaScript 模組以及建構步驟變得更多更複雜，但對於新的框架樣板呢？
tip-writer-support: https://www.coinbase.com/loverajoel

redirect_from:
  - /zh_tw/angularjs-digest-vs-apply/

categories:
    - zh_TW
    - angular
---

AngularJs 最令人欣賞的特性之一是雙向資料綁定。AngularJS 透過循環方式(`$digest`)來檢查模型和視圖變化來實現這個功能。想要理解框架底層的工作方式，你必須了解這個概念。

當一個事件被觸發時，Angular 會檢查每個 watcher 變化，這是我們所知的 `$digest` 循環。
有時候你需要強迫手動執行一個新的循環，你必須選擇正確的選項，因為這個階段是最影響效能之一。

### `$apply`
這個核心方法可以讓你明確地啟動 `$digest` 循環。意思說所有的 watchers 都會被確認；整個應用程式啟動 `$digest loop`。在內部，執行一個可選的功能參數，它會呼叫 `$rootScope.$digest();`。

### `$digest`
在這個情況下，`$digest` 方法在目前的 scope 和子 scope 啟動 `$digeset` 循環。你應該注意到父 scope 不會被檢查，也不會受影響。

### 建議
- 當瀏覽器 DOM 事件觸發外部的 AngularJS 使用 `$apply` 或 `$digest`。
- 傳送一個函式表達式給 `$apply`，這裡有一個錯誤處理機制，並且允許整合所有在 `$digest` 循環的變化。

```javascript
$scope.$apply(() => {
	$scope.tip = 'Javascript Tip';
});
```

- 如果你只要更新目前的 scope 和子 scope，使用 `$digest` 防止在整個應用程式執行新的 digest 循環。這在性能上的好處是相當明顯的。
- `$apply()` 對電腦來說是一個相當複雜的處理程序，如果過多的 binding 會造成性能上的問題。
- 如果你使用 >AngularJS 1.2.X，使用 `$evalAsync`，這是一個核心方法，可以在目前的循環或下一個循環執行表達式，可以增加你的應用程式效能。

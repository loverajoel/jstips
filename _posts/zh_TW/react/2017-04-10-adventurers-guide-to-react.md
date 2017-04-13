---
layout: post

title: React 冒險者指南（Part I）
tip-number: 72
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: 所以你聽說過 *React* 這件事，實際上或許你通過了一些網頁看過了文件，然後你突然碰到一些莫名其妙的與 Webpack、Browserify、Yarn、Babel、NPM 等等更多相關的東西。

categories:
    - zh_TW
    - react
---

> I used to be an adventurer like you, but then I took a RTFM in the knee...
>
> Guard outside of Castle Reducer in the Land of React

所以你聽說過 *React* 這件事，實際上或許你通過了一些網頁看過了文件，然後你突然碰到一些莫名其妙的與 Webpack、Browserify、Yarn、Babel、NPM 等等更多相關的東西。

因此，你到了它們的官方網站透過文件，只會發現自己為了使用 JavaScript 建立網頁應用程式，而在不斷增加的現代工具集合中所迷失了。

你不一定會害怕。

## Yarn、NPM

它們只是套件依賴管理工具，沒什麼好害怕的。事實上，它們是比較沒這麼恐怖的部分。如果你使用發行版的 GNU/Linux、FreeBSD、在 MacOSX 的 Homebrew、Ruby 和 Bundler、Lisp 和 Quicklisp 只是一些名詞而已，你會熟悉這些概念。

React 只是 JavaScript 或稱 ECMAScript 的一部份。

假設現在你真的想要使用 React 來建立應用程式，去面對這些工具吧，它們是很受歡迎的。傳統的方式是，我們到了 React 這個領域時，去詢問來如何操作這些工具。問題是這非常浪費時間，你必須與他們保持聯繫，如果這些工具都無法使用了，你需要取得新的。

然而，隨著一些 drone 的到來，一些聰明的傢伙開始展了不同城鎮，省市的登記（註：作者使用一些描述的手法來說明）。此外，他們建立特別的 drone 可以將這些工具交給你。

現在，為了要在你的專案使用 React，你需要：

```bash
$ npm init . # 建立你的城鎮
$ npm install --save react # 在商店取得 react 並放入材料
```

很方便不是嗎？而且他是免費的。

## Webpack、Browserify 以及他的朋友們

在過去的時間內，你不得不透過自己來建立你自己小鎮所有的事務。如果你想要一個 John McCarthy 的雕像，你需要取得大理石和一些所需要的 parentheses。隨著*套件依賴管理工具*的出現，得到了一些改善，它可以讓你取得大理石和一些材料。當然，你必須自己組合們。

然而從一些 Copy & Paste（公司）來的人們，開發一些工具，允許你可以按這特定順序來 copy & paste 你的材料。

這是相當酷的，你只要放置所有的材料，並指定他們要如何建造，這段時間都是相當和平的。

但是這個方法可能有些問題，我敢肯定有些人會想嘗試避開。也就是說，你想要透過車子來取代這些材料，你不得不重新建立整個城鎮。對於小型的城鎮沒問題，但是對於大型的城市透過這樣的方式就會遇到問題。

然後這靈感來自強大的主啊，接著 build 和 module bundler 就誕生了。

Module bundler 允許你畫出藍圖，並明確的指示城鎮如何被建造。此外，它們成長得相當快速，只支援重建城鎮的一部份，剩下是其餘的部分。

## Babel

Babel 是一個時空旅行者，它帶來了未來的材料讓你使用，像是 ES6/7/8 的特性。

## 如何將他們混合在一起

通常，你將在你的專案內建立資料夾，取得 dependencies，設定你的 module bundler，它可以知道去哪裡尋找你的程式碼並輸出。此外，你可以能想要連接到開發伺服器，在你 building 時可以即時的得到 feedback。

然而，module bundler 的文件很龐大。對於新手冒險者有需多選擇和選項，可能會讓他失去動力。

## create-react-app 和他的朋友們

因此另一個工具被建立了：

```bash
$ npm install -g create-react-app # 安裝全域的 create-react-app
$ create-react-app my-shiny-new-app
```

這是這樣。它預先幫我們設定好了，所以我們不需要通過 Webpack/Browserify 來測試 React。它幫你帶了測試腳本，和一個開發伺服器等等更多其他東西。

然而，這不是我們歷史的結束。這裡有無數不同的 React builder 和 tool，可以參考這裡：[Complementary-Tools](https://github.com/facebook/react/wiki/Complementary-Tools)。

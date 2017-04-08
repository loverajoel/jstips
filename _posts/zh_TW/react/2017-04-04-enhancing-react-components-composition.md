---
layout: post

title: 增強你的 React component 的組合
tip-number: 69
tip-username: loverajoel
tip-username-profile: https://github.com/loverajoel
tip-tldr: React 對於你如何組織你的 component 是相當靈活的，但這個模式讓你的 app component 可以更有效的利用。
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - zh_TW
    - react
---

> 在 Facebook 上，我們使用上千個 React 的 component，
> 我們找不到任何推薦你使用 component 建立繼承的情況。

*Long live to composition, inheritance is dead.*

所以，你如何在 React *繼承*一個 component？

好吧，相當明顯的，@Facebook 的人認為從父 component 繼承是不恰當的，讓我們看看其他方法：

## 提前規劃
在某些情況，你有一個 component 但是不知道它會不會有 children（大多數人都是這樣）。關於這點，React 給了我們 `props.children`：

``` javascript
function List(props) {
  return (
    <ul className={'List List-' + props.importance}>
      {props.children}
    </ul>
    );
}

function DownloadMenu() {
  return (
    <List importance="High">
      <li>Download SBCL</li>
      <li>Download Racket</li>
      <li>Download Haskell</li>
    </List>
    );
}
```

我們可以看到，`props.children` 接收從 component 開始到結束 tag 內所有的元素。

此外，我們可以利用 `props` 來填補：

``` javascript
function ListWithHeader(props) {
  return (
    <ul className={'List List-' + props.importance}>
      <li className="List List-Header">
        {props.header}
      </li>
      {props.children}
    </ul>
    );
}

function DownloadMenuWithHeader() {
  return (
    <List importance="High" header={ <LispLogo /> }>
      <li>Download SBCL</li>
      ...
    </List>
    );
}
```

## 通用 component 以及客製化

所以，我們有了一個很棒的 *FolderView* component

``` javascript
function FolderView(props) {
  return (
    <div className="FolderView">
      <h1>{props.folderName}</h1>
      <ul className="FolderView FolderView-Actions">
        {props.availableActions}
      </ul>
      <ul className="FolderView FolderView-Files">
        {props.files}
      </ul>
    </div>
    );
}
```

這可以表達我們檔案系統內任何的資料夾，然而我們只想要區別它，所以它顯示圖片和桌面資料夾。

``` javascript
function DesktopFolder(props) {
  return (
    <FolderView folderName="Desktop"
      availableActions={
        <li>Create Folder</li>
        <li>Create Document</li>
      }
      files={props.files}
      />
    );
}

function PicturesFolder(props) {
  return (
    <FolderView
      folderName="Pictures"
      availableActions={
        <li>New Picture</li>
      }
      files={props.files}
      />
    );
}
```

就是這樣，我們*客製化*我們的 component，沒有建立任何的繼承結構。

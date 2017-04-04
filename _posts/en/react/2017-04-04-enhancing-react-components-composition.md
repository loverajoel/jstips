---
layout: post

title: Enhancing React components, Composition
tip-number: 69
tip-username: loverajoel 
tip-username-profile: https://github.com/loverajoel
tip-tldr: React is extremely flexible in terms of how you can structure your components, but this pattern will make your apps more efficient.
tip-writer-support: https://www.coinbase.com/loverajoel

categories:
    - en
    - react
---

> At Facebook, we use React in thousands of components, and we haven't found any
> use cases where we would recommend creating component inheritance hierarchies.

*Long live to composition, inheritance is dead.*

So, how do you *extend* a component in React?

Well, it's pretty obvious that the guys @Facebook consider inappropriate to
inherit from parent components. Let's look at alternatives:

## Planning ahead of time
There might be some cases where you have a component which can't know what its
children will be ahead of time (like most of us). For them, React gifts
`props.children`:

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

As we can see, `props.children` receives everything that's in between the
component's open and closing tag.

Furthermore, we can exploit `props` to fill voids:

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

## Generic components and specialization
So, we've got this great *FolderView* component

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
This could represent any folder in our filesystem, however, we only want to
*specialize* it so it shows only the Pictures and Desktop folders.

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

And just like so, we've *specialized* our component, without creating any
inheritance hierarchy!
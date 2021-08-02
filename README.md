# DOM element vs node

## ex1

- document.getElementById의 반환값: HTMLLIElement 
- document.getElementsByTagName의 반환값: HTMLCollection

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="JS">JavaScript</li>
</ul>
<script>
  var li = document.getElementById("JS");
  console.log(li.constructor.name);
  console.log(li);
  var lis = document.getElementsByTagName("li");
  console.log(lis.constructor.name);
  console.log(lis);
  console.log(lis["JS"]);
</script>
```

<img src="https://user-images.githubusercontent.com/22424891/127809810-83bd0769-12b7-4dc9-95e7-7f32e9bd4bff.png" height="300px" />

반환값이 하나면 HTMLLIElement를 반환하고, 여러 개면 HTMLCollection을 반환한다.

## ex2

HTMLElement는 여러가지 종류가 있다.

```html
<a id="anchor" href="http://google.com/">Google</a>
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="list">JavaScript</li>
</ul>
<input type="button" id="button" value="button" />
<script>
  var target = document.getElementById("list");
  console.log(target.constructor.name);

  var target = document.getElementById("anchor");
  console.log(target.constructor.name);

  var target = document.getElementById("button");
  console.log(target.constructor.name); 
</script>
```

<img src="https://user-images.githubusercontent.com/22424891/127810390-2df43791-9c47-45ff-ae6a-aff9619258e0.png" height="150px" />

- 표준 문서
  - [HTMLLIElement](https://www.w3.org/TR/2003/REC-DOM-Level-2-HTML-20030109/html.html#ID-74680021) 
  - [HTMLAnchorElement](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-48250443) 
  - [HTMLInputElement](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-6043025)

### HTMLLIElement interface

```js
interface HTMLLIElement : HTMLElement {
           attribute DOMString       type;
           attribute long            value;
};
```

### HTMLAnchorElement interface

```js
interface HTMLAnchorElement : HTMLElement {
           attribute DOMString       accessKey;
           attribute DOMString       charset;
           attribute DOMString       coords;
           attribute DOMString       href;
           attribute DOMString       hreflang;
           attribute DOMString       name;
           attribute DOMString       rel;
           attribute DOMString       rev;
           attribute DOMString       shape;
           attribute long            tabIndex;
           attribute DOMString       target;
           attribute DOMString       type;
  void               blur();
  void               focus();
};
```

### HTMLInputElement interface

```js
interface HTMLInputElement : HTMLElement {
           attribute DOMString       defaultValue;
           attribute boolean         defaultChecked;
  readonly attribute HTMLFormElement form;
           attribute DOMString       accept;
           attribute DOMString       accessKey;
           attribute DOMString       align;
           attribute DOMString       alt;
           attribute boolean         checked;
           attribute boolean         disabled;
           attribute long            maxLength;
           attribute DOMString       name;
           attribute boolean         readOnly;
  // Modified in DOM Level 2:
           attribute unsigned long   size;
           attribute DOMString       src;
           attribute long            tabIndex;
  // Modified in DOM Level 2:
           attribute DOMString       type;
           attribute DOMString       useMap;
           attribute DOMString       value;
  void               blur();
  void               focus();
  void               select();
  void               click();
};
```

`HTMLLIElement`, `HTMLAnchorElement`, `HTMLInputElement`는 모두 `HTMLElement`를 상속받고 있음을 알 수 있다.

### HTMLElement interface

```js
interface HTMLElement : Element {
           attribute DOMString       id;
           attribute DOMString       title;
           attribute DOMString       lang;
           attribute DOMString       dir;
           attribute DOMString       className;
};
```

즉, `HTMLElement`의 attribute는 공통적으로 갖고, 세부 특성에 따라 세분화됨을 알 수 있다.

## ex3

HTMLCollection은 유사 배열로 반환되며, HTMLCollection의 목록은 실시간으로 변경된다.

```html
<ul>
  <li id="first">HTML</li>
  <li id="second">CSS</li>
  <li id="third">JavaScript</li>
</ul>
<script>
  var lis = document.getElementsByTagName("li");
  console.log(lis.constructor.name);
  console.group('before');
  console.log(lis);
  console.groupEnd();
  lis[0].remove();
  console.group('after');
  console.log(lis);
  console.groupEnd();
</script>
```

<img src="https://user-images.githubusercontent.com/22424891/127814375-bc391463-22bc-4a99-b93b-c81d420c1d7d.png" height="300px" />

### HTMLCollection interface

```js
interface HTMLCollection {
  readonly attribute unsigned long   length;
  Node               item(in unsigned long index);
  Node               namedItem(in DOMString name);
};
```

마지막으로 HTMLDocument의 interface 이다.

### HTMLDocument interface

```js
interface HTMLDocument : Document {
           attribute DOMString       title;
  readonly attribute DOMString       referrer;
  readonly attribute DOMString       domain;
  readonly attribute DOMString       URL;
           attribute HTMLElement     body;
  readonly attribute HTMLCollection  images;
  readonly attribute HTMLCollection  applets;
  readonly attribute HTMLCollection  links;
  readonly attribute HTMLCollection  forms;
  readonly attribute HTMLCollection  anchors;
           attribute DOMString       cookie;
                                        // raises(DOMException) on setting

  void               open();
  void               close();
  void               write(in DOMString text);
  void               writeln(in DOMString text);
  NodeList           getElementsByName(in DOMString elementName);
};
```
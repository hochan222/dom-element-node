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
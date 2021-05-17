# Styling List Bullets in CSS

The bullet/number markers of list-items can be targeted using their very own pseudo-element: `::marker`. This means we can alter the colour, font, content and animation properties of bullet points, giving us unlimited choices of style and symbol. Especially when used in combination with Font Awesome.

```
<link rel="stylesheet" href="https://ka-f.fontawesome.com/releases/v5.15.3/css/free.min.css">

<style>
::marker {
  color: green;
  content: '\f00c';
  font-size: 0.8rem;
  font-family: "Font Awesome 5 Free";
  font-weight: 700; /* required for Font Awesome 5 Free */
}

li {
  padding: 0.2rem 0.4rem;
}
</style>

<ul>
  <li>one</li>
  <li>two</li>
  <li>three</li>
</ul>
```

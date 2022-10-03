---
sort: 3
---

# Code Blocks

`Some inline code ^^ 500000`

[`inline code inside link`](./)

```
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```

**Highlight:**

```scss
:root {
  @for $level from 1 through 12 {
    @if $level % 4 == 0 {
      --toc-#{$level}: #{darken($theme-white, 4 * 8.8%)};
    } @else {
      --toc-#{$level}: #{darken($theme-white, $level % 4 * 8.8%)};
    }
  }
}
```



The <code>&lt;code&gt;</code> element defines inline code.





| Name | Signature Code                 |
|------|--------------------------------|
| Minhas Kamal | <pre>main(m,k){<br>  for(<br>    ;<br>    m%k--?:(k=m++);<br>    k^1?:printf("%i\|",m)<br>  );<br>}</pre> |





---

<br>

---




<details><summary>CLICK ME</summary>

<p>


#### We can hide anything, even code!

```ruby

  puts "Hello World"

```


</p>

</details>






---


<del>
*foo*
</del>


---


<pre language="haskell"><code>
import Text.HTML.TagSoup

main :: IO ()
main = print $ parseTags tags
</code></pre>


---

<div id="demo">

  HII 

</div>



---


<script type="text/javascript">
// JavaScript example

document.getElementById("demo").innerHTML = "Hello JavaScript!";
</script>
okay



----




<details><summary>CLICK ME 2</summary>

<pre language="haskell"><code>
import Text.HTML.TagSoup

main :: IO ()
main = print $ parseTags tags
</code></pre>

</details>

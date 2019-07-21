## [Haml tutorial](http://haml.info/tutorial.html)

ERB:
```erb
<strong><%= item.title %></strong>
```

HAML:
```haml
%strong= item.title
```

---

HTML:

```html
<strong class="code" id="message">Hello, World!</strong>
```

```haml
%strong{:class => "code", :id => "message"} Hello, World!
```

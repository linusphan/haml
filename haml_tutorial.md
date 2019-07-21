## [Haml tutorial](http://haml.info/tutorial.html)

### Basic ERB to HAML

ERB:
```erb
<strong><%= item.title %></strong>
```

HAML:
```haml
%strong= item.title
```

---

### Attributes

HTML:

```html
<strong class="code" id="message">Hello, World!</strong>
```

HAML: 
```haml
%strong{:class => "code", :id => "message"} Hello, World!
```

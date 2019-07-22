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

```haml
%strong.code#message Hello, World!
```

```haml
.content Hello, World!
```

Defaults to div:

HTML:

```html
<div class="content">Hello, World!</div>
```

---

### More complex:

ERB:

```erb
<div class='item' id='item<%= item.id %>'>
  <%= item.body %>
</div>
```

HAML:

```haml
.item{:id => "item#{item.id}"}= item.body
```

---

### Nesting / whitespace

ERB:

```erb
<div id="content">
  <div class="left column">
    <h2>Welcome to our site!</h2>
    <p><%= print_information %></p>
  </div>
  <div class="right column">
    <%= render :partial => "sidebar" %>
  </div>
</div>
```

HAML:

```haml
#content
  .left.column
    %h2 Welcome to our site!
    %p= print_information
  .right.column
    = render :partial => "sidebar"
```

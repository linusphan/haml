## [Haml reference](http://haml.info/docs/yardoc/file.REFERENCE.html)

The reference is Haml's most complete API.

---

### Using Haml

- install:`gem install haml`
- run: `haml input.haml output.html`
- documentation: `haml --help`
- use with Rails: `gem "haml"`
- instance methods and helpers are available:
  ```ruby
  # file: app/controllers/movies_controller.rb
  class  MoviesController < ApplicationController
    def index
      @title = "Teen Wolf"
    end
  end
  ```

  ```haml
  / file: app/views/movies/index.html.haml
  #content
    .title
      %h1= @title
      = link_to "Home", home_url
  ```

  ```html
  <!-- html -->
  <div id="content">
    <div class="title">
      <h1>Teen Wolf</h1>
      <a href="/">Home</a>
    </div>
  </div>
  ```
- XSS protection via `:escape_html` option
- Ruby Module:
  ```ruby
  engine = Haml::Engine.new("%p Haml code!")
  engine.render # => "<p>Haml code!</p>\n"
  ```
- Options:
  ```ruby
  # in Rails => config/initializers/haml.rb
  Haml::Template.options[:format] = :html5
  ```

  ```ruby
  # outside Rails
  Haml::Options.defaults[:format] = :html5
  ```

  ```ruby
  # in sinatra, can set in global config
  ruby set :haml, { escape_html: true }
  ```
  
  - Or, pass options hash to `Haml::Engine#initialize`

- Encodings: set
  `-# coding: encoding-name` /
  `Encoding.default_internal` /
  `:encoding` option

---

### Plain Text

Not interpreted text:

```haml
/ haml
%gee
  %whiz
    Wow this is cool!
```

```html
<!-- html -->
<gee>
  <whiz>
    Wow this is cool!
  </whiz>
</gee>
```

Plain HTML:

```haml
/ haml
%p
  <div id="blah">Blah!</div>
```

```html
<!-- html -->
<p>
  <div id="blah">Blah!</div>
</p>
```

Escaping:

```haml
/ haml
%title
  = @title
  \= @title
```

```html
<!-- html -->
<title>
  MyPage
  = @title
</title>
```

---

### HTML Elements

Element name: `%`

```haml
/ haml
%one
  %two
    %three Hey there
```

```html
<!-- html -->
<one>
  <two>
    <three>Hey there</three>
  </two>
</one>
```

**Attributes:**

via Ruby hashes

```haml
%html{:xmlns => "http://www.w3.org/1999/xhtml", "xml:lang" => "en", :lang => "en"}
```

```html
<html xmlns='http://www.w3.org/1999/xhtml', xml:lang => 'en', lang='en'></html>
```

newlines after commas

```haml
%script{:type => "text/javascript",
        :src => "javascripts/script_#{2 + 7}"}
```

```html
<script src='javascripts/script_9' type='text/javascripts'></script>
```

class and id

```haml
%div{:id => [@item.type, @item.number], :class => [@item.type, @item.urgency]}
```

equivalent to...

```haml
%div{:id => "#{@item.type}_#{@item.urgency}", :class => "#{@item.type} #{@item.urgency}"}
```

example

```haml
%div{:class => [@item.type, @item === @sortcol && [:sort, @sortdir]] } Contents
```

possible results

```html
<div class="numeric sort ascending">Contents</div>
<div class="numeric">Contents</div>
<div class="sort descending"></div>
<div>Contents</div>
```

false gets ignored

```haml
.item{:class => @item.is_empty? && "empty"}
```

```html
class="item"
class="item empty"
```

**HTML-style Attributes: ()**

```haml
%html(xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" leng="en")
```

omit parenthese for local or instance variables

```html
%a(title=@title href=href) Stuff
```

above same as

```haml
%a{:title => @title, :href => href} Stuff
```

mix both for complicated expressions

```haml
%a(title=@title){:href => @link.href} Stuff
```

using #{}

```haml
%span(class="widget_#{@widget.number}")
```

across multiple lines

```haml
%script(type="text/javascript"
        src="javascripts/script_#{2 + 7}")
```

new hash syntax support

```haml
%a{title: @title, href: href} Stuff
```

From Haml::Helpers

```ruby
def html_attrs(lang = 'en-US')
  {:xmlns => "http://www.w3.org/1999/xhtml", 'xml:lang' => lang, :lang => lang}
end
```

```haml
%html{html_attrs('fr-fr')}
```

compiled to

```html
<html lang='fr-fr' xml:lang='fr-fr' xmlns='http://www.w3.org/1999/xhtml'>
</html>
```

multiple attribute methods

```ruby
def hash1
  {:bread => 'white', :filling => 'peanut butter and jelly'}
end

def hash2
  {:bread => 'whole wheat'}
end
```

methods before hash literal

```haml
%sandwhich{hash1, hash2, :delicious => 'true'}/
```

```html
<sandwhich bread='whole wheat' delicious='true' filling='peanut butter and jelly' />
```

**Boolean attributes**

```
<input selected>

%input{:selected => true}

<!-- xhtml -->
<input selected='selected'> 

%input{:selected => false}

<input>

<!-- html style attributes -->
%input(selected)
%input(selected=true)
%input(selected=false)
```

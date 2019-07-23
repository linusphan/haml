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

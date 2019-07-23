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



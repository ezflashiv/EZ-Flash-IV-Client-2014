- Use `CamelCase` class naming pattern for Components, for example:

        .Tweet { }
        .Button { }
        .InformationPanel { }

- Use "is-*" class naming pattern for Component's state, for example:

        .Button { /* button Component core styles */ }
        .Button.is-disabled { /* styling a button in disabled state */ }

- Use "*--modifier" class naming patter for Component's modifier, for example:

        .Button { /* button Component core styles */ }
        .Button--orange { /* orange skin for a button */ }

- Use Utilities with "u-*" class naming pattern for global states and
  modifiers and use them throughout the project, for example:

        .u-isVisible { visibility: visible !important; }
        .u-isInvisible { visibility: hidden !important; }
        .u-pullLeft { float: left !important; }
        .u-pullRight { float: right !important; }
        .u-sizeFill { display: block; overflow: hidden; width: auto !important; }
        .u-textCenter { text-align: center; }
        etc.

- Prefix classes with "js-" for JavaScript hooks, but don't style them. For
  example:

        <div class="Feed js-toggleExpand">
          ...
        </div>

- Name Component's children after their's parent, like so:

        .Widget { }
        .Widget-title { }

        <div class="Widget">
          <p class="Widget-title">
            ...
          </p>
        </div>

  ..and not this:

        .Widget { }
        .Widget .title { }

        <div class="Widget">
          <p class="title">
            ...
          </p>
        </div>

  ..and surely not this:

        .Widget { }
        .Widget p { }

        <div class="Widget">
          <p>
            ...
          </p>
        </div>


- Consider applying class names directly to element instead of writing
  complex selectors, so do this:

        .subnav { }

  ..and not this:

        #main-nav ul li ul { }

- DON'T style components based on context, so don't do this:

        .Button { }
        .Sidebar .Button { }

        <div class="Sidebar">
          <button class="Button">Button</button>
        </div>

  ..but rather style nested Component with modifier (which can be reused):

        .Button { }
        .Button--sticky { }

        <div class="Sidebar">
          <button class="Button Button--sticky">Button</button>
        </div>

  ..or add HTML markup and style it instead:

        .Button { }
        .Sidebar-button { }

        <div class="Sidebar">
          <div class="Sidebar-button">
            <button class="Button">Button</button>
          </div>
        </div>


- Consider adding HTML markup rather than mixing selectors specificities. So don't do this:

        .btn { /* styles */ }
        .uilist { /* styles */ }
        .uilist a { /* styles */ }

        <nav class="uilist">
          <a href="#">Home</a>
          <a href="#">About</a>
          <a class="btn" href="#">Login</a>
        </nav>

  ..but do this to avoid specificity conflicts:

        .btn { /* styles */ }
        .uilist { /* styles */ }
        .uilist-item { /* styles */ }

        <nav class="uilist">
          <a class="uilist-item" href="#">Home</a>
          <a class="uilist-item" href="#">About</a>
          <span class="uilist-item">
            <a class="btn" href="#">Login</a>
          </span>
        </nav>

- Create composable classes. So, don't do this:

        .Button, .Button--green { /* button core styles */ }
        .Button--green { /* styles specific to Green button */ }

        <button class="Button">Default</button>
        <button class="Button--green">Login</button>

  ..but do this:

        .Button { /* button core styles */ }
        .Button--green { /* styles specific to Green button */ }

        <button class="Button">Default</button>
        <button class="Button Button--green">Login</button>


- When hosting a Component in an element and when there is a requirement to
  style that hosting element, don't do this:

        .Tweet { position: relative; }
        .Dropdown { }

        <article class="Tweet">
          [other content]
          <div class="Dropdown">
            ...
          </div>
        </article>

  ..but rather do this:

        .with-Dropdown { position: relative; }
        .Dropdown { }

        <article class="Tweet with-Dropdown">
          [other content]
          <div class="Dropdown">
            ...
          </div>
        </article>

  ..here is a more complex situation:

        /* Provide ability to toggle Tweet actions visibility on hover of ancestor */
        .with-Tweet-actions--toggleVisibility .Tweet-actions { visibility: hidden; }
        .with-Tweet-actions--toggleVisibility:hover .Tweet-actions { visibility: visible; }

        <div class="Stream-item with-Tweet-actions--toggleVisibility">
          <article class="Tweet">
            [other content]
            <div class="Tweet-actions">
              ...
            </div>
          </article>
        </div>


Theory
------

#### Components

Components are UI patterns. Components should be modular. Components should
know how to style themselves and do that job well, but they should not be
responsible for their layout or positioning nor should they make too many
assumptions about how they'll be spaced in relation to surrounding elements.

In general, components should define how they look, but not their layout or
position.

Avoid composing components on the same element.

#### Utilities

Utilities are simple, shared abstractions that components may depend on. Any
number of utilities may be included in a component's HTML if they help you to
create the intended outcome.

Rules of thumb
--------------

- Think in terms of _components_, not pages
- Think about _types of thing_, not individual things
- Prefer styling with Classes rather with IDs or Tags
- Create composable classes
- Prefer selecting by properly namespaced class rather than building descendent selector
- Keep selectors as short as possible
- Don't rely on styles order, rather arrange styles so that they don't race for specificity without a reason
- Prefer percentages for internal layout dimensions

Some quotes:
------------

- tying css selectors to a specific html structure leads to greater difficulty in changing either html or css [source](http://www.vanseodesign.com/css/block-element-modifier/)

14-redesign 
===========
2014 Site redesign is slowly becoming a 2015 redesign

**Changelog:**

- Oct 20th updated fontawesome 
- added partials folders

SASS Architecture V.1 
===========
Refferences:

1. <http://www.sitepoint.com/architecture-sass-project/>
2. <http://www.sitepoint.com/look-different-sass-architectures/>

“Multiple files in dev, a single file in prod.”
— Bruce Lee

**Here’s how we might organize our files:**

	v1
	sass/ 
	| 
	|– base/ 
	|   |– _reset.scss       # Reset/normalize 
	|   |– _typography.scss  # Typography rules 
	|   ...                  # Etc… 
	| 
	|– components/ 
	|   |– _buttons.scss     # Buttons 
	|   |– _carousel.scss    # Carousel 
	|   |– _cover.scss       # Cover 
	|   |– _dropdown.scss    # Dropdown 
	|   |– _navigation.scss  # Navigation 
	|   ...                  # Etc… 
	| 
	|– helpers/ 
	|   |– _variables.scss   # Sass Variables 
	|   |– _functions.scss   # Sass Functions 
	|   |– _mixins.scss      # Sass Mixins 
	|   |– _helpers.scss     # Class & placeholders helpers 
	|   ...                  # Etc… 
	| 
	|– layout/ 
	|   |– _grid.scss        # Grid system 
	|   |– _header.scss      # Header 
	|   |– _footer.scss      # Footer 
	|   |– _sidebar.scss     # Sidebar 
	|   |– _forms.scss       # Forms 
	|   ...                  # Etc… 
	| 
	|– pages/ 
	|   |– _home.scss        # Home specific styles 
	|   |– _contact.scss     # Contact specific styles 
	|   ...                  # Etc… 
	| 
	|– themes/ 
	|   |– _theme.scss       # Default theme 
	|   |– _admin.scss       # Admin theme 
	|   ...                  # Etc… 
	| 
	|– vendors/ 
	|   |– _bootstrap.scss   # Bootstrap 
	|   |– _jquery-ui.scss   # jQuery UI 
	|   ...                  # Etc… 
	| 
	| 
	`– main.scss             # primary Sass file 

As you can see, there is only one Sass file at the root level: main.scss. All the other files are divided into appropriate folders and prefixed with an underscore (_) to tell Sass they are partial .scss files that shouldn’t be compiled to .css files. Indeed, it is the base file’s role to import and merge all of those.


Let’s now look at each of the folders in our architecture.

**Base**

The ```base/``` folder holds what we might call the boilerplate stuff for your project. In there, you might find the reset (or Normalize.css, or whatever), probably some stuff dealing with typography, and, depending on the project, maybe some other files.

+ ```_reset.scss``` or ```_normalize.scss```
+ ```_typography.scss```

**Helpers**

The ```helpers/``` folder (sometimes called ```utils/```) gathers all Sass tools and helpers we’ll use across the project. Got a function? A mixin? Put it in there. This folder also contains a ```_variables.scss``` file (sometimes ```_config.scss) which holds all global variables for the project (for typography, color schemes, and so on).

+ ```_variables.scss```
+ ```_mixins.scss```
+ ```_functions.scss```
+ ```_placeholders.scss``` (frequently named ```_helpers.scss```)

**Layout**

The ```layout/``` directory (sometimes called ```partials/```) usually contains a number of files, each of them setting some styles for the main sections of the layout (header, footer, and so on). It also contains the ```_grid``` file which is the grid system used to build the layout.

+ _grid.scss
+ _header.scss
+ _footer.scss
+ _sidebar.scss
+ _forms.scss

Having the navigation file (```_navigation.scss```) in this folder could make sense although I use to put it in ```components/``` (see next section). I think it would be better in the ```/layout``` folder but I’ll let you decide.

**Components**

For smaller components, there is the ```components/``` folder (frequently called ```modules/```). While ```layout/``` is kind of *macro* (defining the global wireframe), components/ is more *micro*. It can contain all kinds of specific modules like a slider, a loader, a widget, or anything along those lines. There are usually a lot of files in ```components/``` since your site is should be mostly composed of tiny modules.

+ ```_media.scss```
+ ```_carousel.scss```
+ ```_thumbnails.scss```

**Pages**

If you have page-specific styles, I think it’s cool to put them in a pages/ folder and in a file named after the page. For example, it’s not uncommon to have very specific styles for the home page, so you’d have a _home.scss file in pages/ dealing with this.

+ ```_home.scss```
+ ```_contact.scss```

Depending on your deployment process, those files could be called on their own to avoid merging them with the others in the resulting stylesheet. It is really up to you. Where I work, we decided to make them not-partials in order to include them only on pages requiring them. For example, our home page has a very specific layout, compiling to about 200 lines of CSS. To prevent those rules from being loaded on every page, we include this file only on the home page.

**Themes**

If you are working on a large site with multiple themes like I do, having a ```themes/``` folder can make sense. You can stuff all your theme/design related styles in there. This is definitely project-specific so be sure to include it only if you feel the need.

+ ```_theme.scss```
+ ```_admin.scss```

**Vendors**

And last but not least, you will probably have a ```vendors/``` folder containing all the CSS files from external libraries and frameworks – Bootstrap, jQueryUI, FancyCarouselSliderjQueryPowered, and so on. Putting those aside in the same folder is a good way to tell “Hey, this is not from me, not my code, not my responsibility”.

Example:

+ ```bootstrap.scss```
+ ```jquery-ui.scss```
+ ```select2.scss```

On a side note, where I work we also have a ```vendors-extensions/``` folder where we store files overriding some tiny bits from vendors. For example, we have a ```_bootstrap.scss``` file in there that we can use to change some components in Bootstrap. This is to avoid editing the vendor files themselves, which is generally not a good idea.

That’s pretty much it. This architecture is likely to vary according to the project but I’m sure you get the concept. On nesting folders in folders, I wouldn’t always advise against it but I don’t prefer that. I’ve found that in most cases, a single level of architecture is more than enough to keep things clean and organized without adding too much complexity. But if you think your project deserves a deeper structure, feel free to do so.

Pro tip: if you feel like your architecture isn’t obvious to anyone opening up the ```scss``` folder, you might consider adding a ```README.md``` file at the root level (side by side with ```main.scss```) explaining everything.


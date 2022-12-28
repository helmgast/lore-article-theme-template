# Intro
This is a template repository to get started making a theme for [Lore](https://github.com/helmgast/lore). An theme can be applied to an article, world or publisher, e.g. almost any page in Lore, and the theme can change the look and behaviour of a single article, of a world and all articles in it or a whole publisher. You could create character sheets, articles styled as old scrolls or complete Single Page Apps.

# How it works

Lore is a Content Management System that stores articles in a database (for simplicity, we will refer to also worlds and publishers as articles). When a user visits a Lore URL that represents an article such as [Eon fyller 25](https://helmgast.se/eon/eon-fyller-25-ar) or [Neotech home page](https://helmgast.se/neotech/)), Lore finds the corresponding article data and combines it with an HTML template that is returned to the browser.

When editing an article you can set it's *theme* property, and then it will use that template instead of the default to return the HTML.

## Types of templates
The theme template can operate in 3 ways:

1. It can be just a **static HTML page**, which has the effect of not showing any of the dynamic content belonging to the article being viewed. It also either have a completely different look and feel compared to the rest of the site, or it's hard to keep your static page in sync with the look of the rest of the site.
2. It can be a **root template**, which takes the responsibility to render the full HTML of the page with HEAD and BODY tags, but also include *template blocks* that insert content from the article. This allows 100% control of styling while still showing dynamic content, with the same drawbacks of not syncing with the overall site style as in 1.
3. It can be a **child template**, which means that it's inserted into the existing *template hierarchy*. When a page is rendered, it will start at a root template that contains the top-most HTML elements such as head and body. Inside the root template, we have *blocks* which are parts that can be replaced with child templates or custom content. In this way, we can build a site that shares common header and footer but where the article content in between changes.

We recommend number 3 because it usually looks best for the user and also means less code to write, but it does require you getting into a bit more how templating works inside Lore.

_root.html          pub_root  pub_home world_list world_item article_list article_item
- title                       
- icons             
- opengraph                                                               x
- googlefonts
- cssimports                                      x                       x
- topjs             
- js_globalvars     
- navbar            
 - publisher_brand  
 - navbar_left      x
   - publishers_active
   - social_active
 - search           x
 - navbar_right     
 - breadcrumbs                          x         x          x            x
 - subnavbar                            x         x
 - actionbar                            x         x                       x
- header                       x                                          x
  - header_title                                                          x
    - content_title            x        x         x          x            x
    - content_tagline                   x         x          x            x
- main                         x
  - intro_parent    
    - intro                                       x                       x
  - content                             x         x          x            x
  - post_content                                             x
  - asides                                                   x            x
  - end_main                                                              x
- footer            
- final_html                                                              x
- js_bottom         
- tour              

- _root.html
  - publisher_root / theme
    - publisher_home
    - world_list / theme
      - world_item
        - article_list / theme
          - article_item
  - publisher_list
    - publisher_item
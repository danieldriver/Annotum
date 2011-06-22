# Annotum Readme

## Background

Annotum is a WordPress theme (and child theme) built on the [Carrington theme engine](http://carringtontheme.com/).

All features are packaged within the theme. Once the theme is activated, many settings are available from the WordPress dashboard under the Annotum heading.

## Installation

To checkout the Annotum theme code to an existing WordPress installation:

1. Navigate to the wp-content/themes directory in the WP install
2. Create the annotum directory within the themes directory and change directory into it.
3. On the command line type `git clone git@github.com:Annotum/Annotum.git .` without backticks. 
4. If you are using SVN: `svn co https://username@github.com/Annotum/Annotum.git .`

## User Roles and the Workflow (authors, contributors)

When the workflow is active, the site-wide roles of `author` and `contributor` have the exact same capabilities on the Articles post-type. This is not the case with any other post type.

When the workflow is not active, the `author` and `contributor` roles should act according to their default WordPress capabilities. See [Roles and Capabilities](http://codex.wordpress.org/Roles_and_Capabilities) in the WordPress Codex for more information on the capabilities of these roles.

## Home Page Callouts

You can optionally add 1 or 2 callouts to the home page, that contain announcements, notices or other important info.

To set up callouts, log in to the WordPress admin and go to `Appearance > Theme Options`. You'll see two groups of fields, "Home Page Callout Left" and "Home Page Callout Right". Each has three fields, all optional:

- Title: display a title in the callout.
- URL: a valid URL. If provided, the title of the callout will be linked to this address.
- Content: Free-form content. HTML is OK.

## Annotum in Your Language

Annotum has full support for internationalization. It also supports right-to-left languages. To get Annotum running in your language, you'll want to:

1. Get [WordPress in your language](http://codex.wordpress.org/WordPress_in_Your_Language).
2. Install your Annotum language pack in `annotum-base/languages/`. If you don't have a language pack for Annotum in your language, consider [creating a translation yourself](http://codex.wordpress.org/Translating_WordPress).


## For Theme Developers

Annotum has been developed to be easy to customize with [WordPress Child Themes](http://codex.wordpress.org/Child_Themes).

- All assets are registered via `wp_enqueue` so you can enqueue/dequeue any CSS or JS file.

- Custom template tags are set in `templates.php` to make it easy to access custom functionality like acknowledgements, funding statements, Tweet buttons, etc.

- You can easily customize template tags by extending the class that contains the template tag library (`Anno_Template_Tags`). An easy way to do this is to register your own template tag class after `init:10`. Example:

        class My_Template_Tags extends Anno_Template_Tags { /* Define something... */ }
        function my_init_template_tags() {
            $my_template = new My_Template_Tags();
            Anno_Keeper::keep('template', $my_template);
        }
        add_action('init', 'my_init_template_tags', 11);

## Debugging

- Carrington theme debugging can be enabled/disabled in the functions.php file. This will output the file paths to all Carrington templates loaded into the page and is not recommended in non-development environments: `define('CFCT_DEBUG', true);`
- Some of the expensive `template.php` tags use [transient caching](http://codex.wordpress.org/Transients_API) to make sure things are speedy. If you need to troubleshoot transient caching, you can set `Anno_Template::$use_caches` to `false`. Setting `CFCT_DEBUG` to `true` will also disable the transient caches.

---

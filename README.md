# yoast_breadcrumbs <h1>
# What is This <h2>
A project to help Wordpress / Yoast SEO community customize the appearance of breadcrumbs in their website

# Problems this code solves  <h2>
There's abundant documentation on how to implement Yoast SEO breadcrumbs. However, there's very little clarity around a couple of problems:
* How to make the post title (last element of the breadcrumb) disappear
* How to format breadcrumbs appearance on the website
* How to selectively show / remove breadcrumbs (from specific pages, posts, homepage, blog, etc) 

# Who's This For  <h2>
Developers, webmasters and users that want to configure breadcrumbs above/beyond what Yoast SEO plug interface allows them to, in a simple and elegant way.

# The Solution  <h2>
This code applies to header.php file and to (custom) CSS file in virtually any Wordpress theme out there.
It is modular: you choose which lines you need to add to make it work for you, custom. Just follow the **Instructions** below.

# Instructions - How to Apply and Customize this Code to Your Needs  <h2>
1. To implement breadcrumbs, place the code at the end of your theme's headers.php
_Remember: when you update your theme you may lose this code so create documentation / backup or implement your theme a child theme._ 

``` <!-- Yoast SEO Breadcrumbs implementation -->
<?php
if ( function_exists('yoast_breadcrumb')) {
	yoast_breadcrumb('<p id="breadcrumbs">','</p>');
}
?> 
```

1. Activate breadcrumbs on Yoast SEO plugin interface.
Wordpress panel > SEO > Panel > Advanced > Breadcrumbs. Select "Activate" button and click "Save Changes".
Breadcrumbs are now active on your theme. Now choose from the options below the type of customization you want to apply:

    1. Selective show / remove breadcrumbs from certain pages
        1. Via PHP
        One efficient way to remove certain pages is to implement it via IF statement on PHP on header.php
        This code eliminates breadcrumbs from all pages and from the blog page.
        ``` <!-- Yoast SEO Breadcrumbs implementation -->
        <?php
        if ( function_exists('yoast_breadcrumb') && !is_home() && !is_page()) {
        yoast_breadcrumb('<p id="breadcrumbs">','</p>');
        }
        ?> 
	```
        
        If you want to target an specific page or post, you can implement the IF using is_page or is_post functions, as follows:
        _eliminates breadcrumbs from page ID 2147_
        ``` <!-- Yoast SEO Breadcrumbs implementation -->
        <?php
        if ( function_exists('yoast_breadcrumb') && !is_page( array (2147))) {
        yoast_breadcrumb('<p id="breadcrumbs">','</p>');
        }
        ?> 
	```
        
        For the Blog Page, use is_home() and is_page() together
        For the Homesite, use is_front_page()
        For more options including examples check reference [1].
                
        1. Via CSS
        Yoast SEO implements breadcrumbs as an ID, so you'll use the # symbol on CSS. You can target specific pages using CSS methods .postid and .page-id as follows: 
        _eliminates breadcrumbs from page ID 2984_
        ```.postid-2984 #breadcrumbs {
        display: none !important;
        } 
	```
        
    1. Make post or page title (last element of the breadcrumb disappear) via CSS
    By default, Yoast SEO shows the post / page title on the breadcrumb. To eliminate that redundancy, use this CSS code:
    _Yoast SEO implements the last piece of the breadcrumb as div breadcrumb_lat_
    ``` .breadcrumb_last {
    display: none;
    } 
    ```
    This method is also useful in eliminating page titles in specific posts / pages as explained on the CSS implementation above.
    
    1. Format breadcrumbs appearance via CSS
    My theme had terrible formatting for breadcrumbs, so I aligned it with logo, removed bottom margins, and then set fonts to look like menu items with this code:
    ``` #breadcrumbs {
    margin-left: 400px;
    margin-bottom: 0px;
    font-family:	"Raleway",Helvetica,Arial,sans-serif;
    font-size: 13px;
    font-weight: 600;
    text-transform: uppercase;
    text-decoration: none;
    zoom: 1;
    letter-spacing: 1px;
    }
    ```

# References  <h2>
1. [Conditional Tags on Wordpress](https://codex.wordpress.org/Conditional_Tags) containing many examples
1. [Yoast SEO Breadcrumbs Documentation](https://yoast.com/breadcrumbs-seo/)
1. [How To Implement Yoast SEO Breadcrumb In Your Theme?](https://napitwptech.com/tutorial/wordpress-development/how-to-implement-yoast-seo-breadcrumb-in-your-theme/)


# Want to provide feedback or contribute?  <h1>
Leave a comment! Thanks for reading and using this.

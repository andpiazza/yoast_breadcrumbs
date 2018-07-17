# yoast_breadcrumbs
A project to help Wordpress / Yoast SEO community customize the appearance of breadcrumbs in their website

## Problems this code solves
There's abundant documentation on how to implement Yoast SEO breadcrumbs. However, there's very little clarity around a couple of problems:
* How to make the post title (last element of the breadcrumb) disappear
* How to format breadcrumbs appearance on the website
* How to selectively show / remove breadcrumbs (from specific pages, posts, homepage, blog, etc) 

## Who's This For
Developers, webmasters and users that want to configure breadcrumbs above/beyond what Yoast SEO plug interface allows them to, in a simple and elegant way.

## The Solution
* This code applies to header.php file and to (custom) CSS file in virtually any Wordpress theme out there.
* It is modular: you choose which lines you need to add to make it work for you, custom. Just follow the **Instructions** below.
* This could be easily extended to other breadcrumb plugins, generators like Genesys and others: knowing how your plugin implemented the HTML code (classes, ids, etc) will allow you to easily customize the code that follows.

## Instructions - How to Apply and Customize this Code to Your Needs
**Implement breadcrumbs**: place the code at the end of your theme's headers.php
_Remember: when you update your theme you may lose this code so create documentation / backup or implement your theme a child theme._ 

```
<!-- Yoast SEO Breadcrumbs implementation -->
<?php
if ( function_exists('yoast_breadcrumb')) {
	yoast_breadcrumb('<p id="breadcrumbs">','</p>');
}
?> 
```

**Activate breadcrumbs on Yoast SEO plugin interface**
Wordpress panel > SEO > Panel > Advanced > Breadcrumbs. Select "Activate" button and click "Save Changes".
Breadcrumbs are now active on your theme. 
Now choose from the options below the type of customization you want to apply:

**_Selectively_ show / remove breadcrumbs from certain pages**
**Via PHP**
One efficient way to remove certain pages is to implement it via IF statement on PHP on header.php
This code eliminates breadcrumbs from all pages and from the blog page.

```
<!-- Yoast SEO Breadcrumbs implementation -->
<?php
if ( function_exists('yoast_breadcrumb') && !is_home() && !is_page()) {
yoast_breadcrumb('<p id="breadcrumbs">','</p>');
}
?> 
```
If you want to target a specific page or post, you can implement the IF using is_page or is_post functions, as follows:
_eliminates breadcrumbs from page ID 2147_
        
```
<!-- Yoast SEO Breadcrumbs implementation -->
<?php
if ( function_exists('yoast_breadcrumb') && !is_page( array (2147))) {
yoast_breadcrumb('<p id="breadcrumbs">','</p>');
}
?> 
``` 
For the Blog Page, implement the IF using is_home() and is_page() together:
```
if ( function_exists('yoast_breadcrumb') && !is_page() && !is_home() {
```
For the Homesite, use is_front_page():
```
if ( function_exists('yoast_breadcrumb') && !front_page() {
```
For more options including examples check reference [1].
                
**Via CSS**
Yoast SEO implements breadcrumbs as an ID, so you'll use the # symbol on CSS. You can target specific pages using CSS methods .postid and .page-id as follows: 
_this sample eliminates breadcrumbs from page ID 2984_
```
.postid-2984 #breadcrumbs {
display: none !important;
} 
```
        
**Make the last element of the breadcrumb (post or page title) not show via CSS**
By default, Yoast SEO shows the post / page title on the breadcrumb. To eliminate that redundancy, use this CSS code:
_Yoast SEO implements the last piece of the breadcrumb as div breadcrumb_last_
```
.breadcrumb_last {
display: none;
} 
```
This method is also useful in eliminating page / post titles in specific URLs as explained on the CSS implementation above.
    
**Format breadcrumbs appearance via CSS**
My theme had terrible formatting for breadcrumbs, so I aligned it with logo, removed bottom margins, and then set fonts to look like the menu items using this code. Customize to your needs!
```
#breadcrumbs {
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

## References
1. [Conditional Tags on Wordpress](https://codex.wordpress.org/Conditional_Tags) containing many examples
1. [Yoast SEO Breadcrumbs Documentation](https://yoast.com/breadcrumbs-seo/)
1. [How To Implement Yoast SEO Breadcrumb In Your Theme?](https://napitwptech.com/tutorial/wordpress-development/how-to-implement-yoast-seo-breadcrumb-in-your-theme/)
1. [Breadcrumbs For Web Sites: What, When and How](https://uxplanet.org/breadcrumbs-for-web-sites-what-when-and-how-9273dacf1960) is a great overview of how to properly use breadcrumbs to enhance UX 

## Want to provide feedback or contribute?
Leave a comment! Thanks for reading and using this.

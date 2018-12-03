# Taking a site from HTML to Kirby

---

This tutorial will show the basics of how to take an html website and convert this to Kirby.  This is an easier process because you dont need to be think about layout and design - mostly just the Kirby logic.

We will be looking at:

1. An HTML Site
2. Preparing the Ground
3. Understanding Snippets
4. Template - whats in a template?
5. Content is King
6. Finishing Up
7. The Panel

---

# 1. Download HTML Site

This is a basic HTML Student Portfolio site. That has a Homepage, About and Contact.  Lets check it out. [Download this here.](https://www.dropbox.com/s/biyjju3piu6r817/HTML_Student.zip?dl=0)

![This is the site we will be using](img/Screenshot%202018-12-03%2010.50.26.png)

Upzip this and have this on your desktop. This is just a simple HTML and CSS site.

---

# 2. Preparing the Ground

You need to install a clean version of kirby on your Local server.  We did this in class a few weeks ago.  This gives us a fresh site to work from.

If you cant remember how to do that, [follow the documentation from Kirby Here](https://getkirby.com/docs/installation/on-a-mac) alternatively if you are on Windows, [follow along here](https://getkirby.com/docs/installation/on-a-pc)

![Your should see after install](img/Screenshot%202018-09-25%2014.42.17.png)

Now we are going to switch off the stylesheet so that we are just 				working with content and not worrying about the design and style 				for now.  

Go into your Kirby Install and find /assets/css/index.css - rename the index.css to index1.css

Now your site will look like this

![Dont panic if it looks like this](img/Screenshot%202018-09-25%2014.56.55.png)

You might need to clear your browswer history and cache to see changes.

## Edit the site.txt file

- Edit site.txt file - this alters the title etc.

Go to site.txt inside your content folder.

![Go here](img/Screenshot%202018-09-25%2016.01.34.png) 

![Change it from this](img/Screenshot%202018-09-25%2016.01.52.png)

![To this](img/Screenshot%202018-09-25%2016.03.26.png)

You wil now see that your title has changed as well as your footer copyright text.

 ![Title change](img/Screenshot%202018-09-25%2016.09.06.png)
 
 ---

# 3. Understanding Snippets

To keep your code clean and maintainable you should avoid to repeat yourself at all cost. Snippets are a great way to store code, which is being reused in multiple templates.

All snippets are stored in /site/snippets

Your site can have as many snippets as you need.
![Snippets](img/Screenshot%202018-09-25%2016.16.28.png)

We are going to make three snippets.  One for the header and one for the footer and one for navigation because these are repeated on every page of the site.  So it keeps everything efficient. The last one is for some icons.

Open the index.html file in HTML Student Folder:

![The index.html file.  From line 1 to 31 I want you to copy this into the header.php file in your new setup](img/Screenshot%202018-09-25%2016.20.27.png)

Copy this code into the header.php file in your new setup.  Its ok to delete whats in the header.php file.

````
<!DOCTYPE html>
<html>
<!–– Head details - typefaces and CSS -->
	<head>
        <meta charset="utf-8">        
        <meta name="author" content="Kyle Boyd">
        <meta name="description" content="Jekyll Mockup">
            
        <title>Student Portfolio - HTML</title>
        <link href="https://fonts.googleapis.com/css?family=Rozha+One|Source+Sans+Pro" rel="stylesheet">
        
        <link rel="stylesheet" type="text/css" href="css/styles.css">

    </head>

    <body> 
    <!–– Header H1 and Navigation --> 
    <header>
    <div class="a"><h1>Student Portfolio</h1></div>
    <div class="b">
    <?php snippet('menu') ?>    
    </div>
    
    </header> 

````

Do the same for the footer.  Open the footer.php page and with this code.

````
<a id="contact"></a>
<footer>
    <!–– Copyright -->

    <div class="x">
        <h3>Who owns this?</h3>
    <p><?= $site->copyright() ?></p>
    </div> 
    <!–– Social Medias -->
    <div class="y">
    <h3>Say Hello</h3>
    <ul>
        <li><a href="#">Email</a></li>
        <li><a href="#">Instagram</a></li>
        <li><a href="#">Github</a></li>
        <li><a href="#">Twitter</a></li>
    </ul>
    </div>

    </footer>
     
    </body>
</html>
````  

Now I want you to copy this code into showcase.php in the snippets folder.

````
<section class="box">
    <ul id="grid">
        <?php foreach($page->children()->visible() as $member): ?>
          <li>
            <?php if($image = $member->image()): ?>
                <img src="<?= $image->url() ?>" alt="<?= $member->title()->html() ?>" class="svg"  />
            <?php endif ?>
            <hr>
             <?= $member->title()->html() ?>
          </li>
        <?php endforeach ?>
      </ul>
    </section>

````

I want you to make one more snippet - open menu.php and replace the code with this:

```
<div class="b">
<nav>
  <ul>
    <?php foreach($pages->visible() as $item): ?>
    <li class="menu-item<?= r($item->isOpen(), ' is-active') ?>">
      <a href="<?= $item->url() ?>"><?= $item->title()->html() ?></a>
    </li>
    <?php endforeach ?>
  </ul>
</nav>
</div>
```

We have made four brand new snippets with our own code. One called header.php, one called footer.php, one called showcase.php and one for the menu.  These can be used throughout the website and they must be .php files.

AMAZING. This may seem simple but its incredibly powerful.

In order to use the header snippet in your templates you use '<?php snippet ('header')

This then calls the snippit and displays in in your template. We wil look at this more now.

We will add our new style sheet now.  Simply take the CSS folder from the student example and place it in the root of your new project.  

![Add the CSS file from the student website to the root of your new project](img/Screenshot%202018-12-03%2016.33.14.png)

---

# 4. Template - Whats in a Template?

Kirby's template engine is based on a mixture of simple PHP and HTML. You don't need to know PHP to get started. The methods which are being used to fetch data into your templates are very easy to understand. You should have basic HTML skills though.

A template sets the layout for each page.  You could have a template for the home page, about page and the contact page.  Of course you could use the same template for multiple pages.

We are going to make three templates. One for your home page, one for an about page and one for contact.  These again will be made using the existing code from the student portfolio site.

Open home.php and about.php from the templates folder.

- Home.php
 
 Copy this code and replace it with the code in home.php.  Keep <?php snippet('header') ?> and <?php snippet('footer') ?> So it should look like this.
 
 ````
 <?php snippet('header') ?>

 <main>
    <!–– Main Home Page Banner -->

        <div class="box2 d"><h2>Hi There.</h2> 
            <p>This is a mockup portfolio,<br> made in HTML - for your perusal.</p>
      </div>
      <div class="box2 f"><img src="img/home.jpg"></div>
    </main>
    
   <section id="hello">
   <a id="portfolio"></a>
   <!–– Portfolio Introduction -->

       <h2>The Portfolio</h2>
       <hr>
        <p>Hello there this is a portfolio section. Its really awesome. SO IT IS.</p>   
       
    
    </section>

<?php snippet('footer') ?>
 
 ````
 
 - About.php
 In your about.html page copy lines 33-48 and replace it with the code in about.php.  Keep <?php snippet('header') ?> and <?php snippet('footer') ?>
 
 ````
 <?php snippet('header') ?>

   <section id="hello">
    
       <h2>About Me</h2>
       <hr>       
    
    </section>
        
<section id="about">
      <div class="k">
    <h3>Mr Student</h3>      
    <p>A student of Interaction Design at the Belfast School of Art, Ulster University. This student is interested in UI/UX/Branding/.</p>
    </div>
    <div class="t">
    <img src="img/student.png" alt="Student">
    </div>
    </section>

<?php snippet('footer') ?>
 
 ````
 
 What we have created is two layouts for home page and about page. We can use the about template for the contact page as they layout will be the same - its just the content that will be different.
 
 Now we have created snippets and templates we can begin to work with the content.
 
# 5. Content is King

We have focussed on snippets and templates so far.  Lets look at the content folder.

Firstly we are going to use the menu snippit which we created earlier.  Currently the menu is hardcoded in the header.php.

Replace the navigation from this: 

![Replace codew with <?php snippet('menu') ?>](img/Screenshot%202018-09-26%2016.08.05.png) 

To this using `  <?php snippet('menu') ?>`

![Using the snippet menu](img/Screenshot%202018-09-26%2016.09.13.png)

The php in the menu snippet will now use the file structure in Kirby

We are hoping to update the menu so that we have a home link - instead of projects, blog, about and contact we will change it to Home, About and Contact.

To do this make it like so:

1-Home
2-About
3-Contact

Remove projects and blog by just removing the numbers. They will still be availble just not visible.

![Make this New File Structure](img/Screenshot%202018-09-26%2016.32.32.png)

This is the beauty of Kirby - it just uses a folder for each page.

Each folder contains a text file, which stores all the data for the page. The name of the text file determines, which template should be used to render the page.


|  Data File |  Template Directory      
|---|---|
|  home.txt |   /site/templates/home.php
|  about.txt |   /site/templates/about.php
|  contact.txt |    /site/templates/contact.php 

If there's no template for the text file, Kirby will use /site/templates/default.php to render the page.

### Fields

With a traditional database-driven system you often run into the problem of being stuck with a predefined structure for your data.

With Kirby you gain 100% freedom to add all the data you need for any page of your site. Kirby's text files have a very simple system. You define a field of data with a name, a colon and some content. You separate multiple fields with four dashes:

````
Title: This is my title
----
Text: This is a nice text
----
Date: 2012/01/11
----

````

You are not limited to any number of fields per file. You could have hundreds of them, though that would be quite a mess to read and update – but you could :) 

Go into the content folder and inside 1-home, 2-about and 3-contact you will find home.txt, about.txt and contact.txt.

Replace with the below:

### 1-home

````
Title: Home

----

Welcome: Hi There

----

Intro: 

This is a mockup portfolio,<br> made in Kirby - 
for your perusal. <br>
Yup, Im amazing.

----

Folio: The Portfolio

----

Foliointro: Hello there this is a portfolio section. Its really awesome. SO IT IS.

----

````

### 2-about

````
Title: About Me

----

Minortitle: Hi, Im Kyle

----

Intro: A student of Interaction Design at the Belfast School of Art, Ulster University. This student is interested in UI/UX/Branding.

----


````

### 3-contact

````
Title: Contact

----

Text: 

### Follow Me on Twitter:


Kyle Boyd
(twitter: @kylbyd)


----

Intro: Contact me if you want to discuss my work.

----

Contactoptions: 

- 
  title: Contact
  text: >
    Feel free to drop us a line if you
    have any questions.
  url: mailto:support@getkirby.com
  linktext: Write an email
  icon: contact.svg
````

---

#### Using your fields data in Templates

Once you've added your content, it is very easy to use those fields in your template files. Kirby will try to find a matching template for the name of your text file. So if your text file is project.txt, Kirby will try to load the template site/templates/project.php. If it is not there, it will fall back to site/templates/default.php So you can add specific templates for specific types of data very easily.

Let's say the text file for the current page has a title, text, date and tags field, you can add them to your template like this:

````
<?= $page->title() ?>
<?= $page->text() ?>
<?= $page->date() ?>

````

#### Example: Home Page

Earlier when we changed the code in home.php this was to get the structure but it wouldnt be useful as a cms as all the content was hardcoded.  We want to be bale to access the data from our fields data (the .txt files we just changed).  We are going to do that for the home page.

#### The Content

![Currently the code looks like this in home.php](img/Screenshot%202018-12-03%2016.00.10.png)

![We will change it to this](img/Screenshot%202018-12-03%2016.00.19.png)

See how the fields from our home.txt file are being called to the page. Replace home.pho with the code below.

````

<?php snippet('header') ?>


    <main>
    <!–– Main Home Page Banner -->

        <div class="box2 d"><h2><?= $page->title() ?></h2> 
            <p><?= $page->intro() ?></p>
      </div>
      <div class="box2 f">
          <?php if($image = $page->image('home.jpg')): ?>
            <img src="<?= $image->url() ?>" alt="Home Page">
            <?php endif ?>
          
        </div>
    </main>
    
   <section id="hello">
   <a id="portfolio"></a>
   <!–– Portfolio Introduction -->

       <h2><?= $page->folio() ?></h2>
       <hr>
       <p><?= $page->foliointro() ?></p>   
       
    <hr>
    </section>
        
        <!–– Portfolio Section -->

      <?php snippet('showcase') ?>


<?php snippet('footer') ?>

````

This is the code for the about page

````
<?php snippet('header') ?>

<!–– About Me Section -->  

   <section id="hello">
    
       <h2><?= $page->title() ?></h2>
       <hr>       
    
    </section>
        
<section id="about">
      <div class="k">
    <h3><?= $page->Minortitle() ?></h3>      
    <p><?= $page->intro() ?></p>
    </div>
    <div class="t">
          <?php if($image = $page->image('student.png')): ?>
            <img src="<?= $image->url() ?>" alt="About Me Picture">
            <?php endif ?>
    </div>
    </section>

<?php snippet('footer') ?>


````

This is the code for the contact page.

````
<?php snippet('header') ?>

    
   <section id="hello">
    
       <h2><?= $page->title() ?></h2>
       <hr>       
    
    </section>
    
<section id="about">
      <div class="k">
    <h3><?= $page->Minortitle() ?></h3>      
    <p><?= $page->intro() ?></p>
    </div>
    <div class="t">
          <?php if($image = $page->image('student.png')): ?>
            <img src="<?= $image->url() ?>" alt="About Me Picture">
            <?php endif ?>
        <div class="contact-twitter">
                <?php if($image = $page->image('contact.svg')): ?>
            <img src="<?= $image->url() ?>" class="icon" alt="Contact Me">
            <?php endif ?>
      <?= $page->text()->kirbytext() ?>

    </div>

    </div>
    </section>




<?php snippet('footer') ?>

````

Now all the content from our data files is being called to the pages via data fields.

# 6. Finishing Up

Now we have got most of the structure in place - we are using snippits, templates and data files.  

Your site should now look like this:

![title](img/Screenshot%202018-12-03%2016.37.54.png) ![title](img/Screenshot%202018-12-03%2016.37.58.png) ![title](img/Screenshot%202018-12-03%2016.38.01.png)

But there is a problem - we dont have any images.

In the student portfolio site inside the img folder you will find two images:

1. home.jpg - Put this into the folder content / 1-home / of your new site
2. student.png Put this into the folder content / 3-about / of your new site

Thats the cool ting about images - in order to access them they just need to place them in the folder of the page.

We had already written the logic for this - its in home.php.

![This is the logic to call images](img/Screenshot%202018-12-03%2017.04.43.png)

````
<img src="<?= $page->images()->find('01.png')->url() ?>" />
````

The only issue now is that we cannot see the showcase section of the site - at the bottome of the homepage.  

To see this we need to create a series of folders for the showcase.

Inside 1-home create these folders:

0-app
0-exploring identity
0-illustration
0-ux
0-uxr
0-websites

![So it should look like so...](img/Screenshot%202018-12-03%2017.21.27.png)

Inside these folders create a .txt file called skill.  Like so:

![Should look like this](img/Screenshot%202018-12-03%2017.24.23.png)

Inside each .txt file include this:

````
Title: App Design

----

````

But change the title to whatever portfolio item you want.  Illustration, ux, uxr etc.

Now we need to add images - go to the img folder in HTML Student Portfolio example and copy each .svg into its corresponding folder.

app.svg in 0-app, ux.svg in 0-ux etc. So it looks like this:

![It should look like this](img/Screenshot%202018-12-03%2017.35.40.png)

Now when we refresh the homepage it should look like this:

![A finished site](file:///Users/e10420799/Dropbox/Screenshots/Screenshot%202018-12-03%2017.37.39.png)


---

# 7. The Panel

This is the backend section which you can login to and then update the website via panel. Just add /panel to the end of your URL.

![This is the panel login](img/Screenshot%202018-12-03%2017.39.28.png)

With the fields we have setup we can change content.

![This is the Panel](img/Screenshot%202018-12-03%2017.47.37.png)

You explore this for yourself.

---

Fin





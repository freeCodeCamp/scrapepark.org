# ScrapePark.org

![ScrapePark.org Logo](images/logo.svg)

Welcome to [ScrapePark.org](https://scrapepark.org/), your "web scraping park". 

Apply your web scraping knowledge and skills with this website specially designed for this purpose. Practice safely without affecting third-party platforms, websites, or services.

## Elements

**ScrapePark.org** includes elements to help you practice web scraping, including a table, an iframe, dropdown menus, links, lists, images, buttons, forms, a carousel, menu items, navigation bar items, and more.

![Screenshot of ScrapePark.org](images/screenshot1.png)

## freeCodeCamp.org

This website is hosted by [freeCodeCamp.org](https://www.freecodecamp.org/), a friendly community where you can learn to code for free. It is run by a donor-supported 501(c)(3) nonprofit to help millions of busy adults transition into tech. Our community has already helped more than 40,000 people get their first developer job.

Our full-stack web development and machine learning curriculum is completely free and self-paced. We have thousands of interactive coding challenges to help you expand your skills.

## Contributing

Thank you for your interest in contributing to ScrapePark.org. We welcome your contributions to expand the website and to localize it into multiple languages.

#### Commits and Pull Requests

We recommend using [conventional title and messages](https://www.conventionalcommits.org/en/v1.0.0/) for commits and pull requests. 

Please keep the description short (less than 30 characters) and simple; you can add more information in the PR description box and comments. 

Read our guidelines to [open a pull request](https://contribute.freecodecamp.org/#/how-to-open-a-pull-request). 

## Templates

The website is localized using the [node-static-i18n](https://github.com/claudetech/node-static-i18n) utility. This utility is used to translate static HTML files. 

The `templates` directory has the HTML files that serve as templates for the translated versions of the website. 

In these files, you will find the keys of the key-value pairs of the JSON files for their corresponding languages. 

**Example:**

```HTML
<a class="nav-link" href=#prices data-t>navbar.prices</a>
```

* By adding `data-t`, we are telling the `node-static-i18n` utility that we need to translate the text in this HTML element. 
* The value of `navbar.prices` will be replaced by the corresponding value in the JSON file of the language that is being generated.

If this is part of the JSON file `spanish.json`, when the Spanish version of the website is generated, the value of `navbar.prices` will be `"Precios"`.

```JSON
{
    "navbar": {
        "home": "Inicio",
        "about": "Acerca",
        "testimonials": "Testimonios",
        "products": "Productos",
        "prices": "Precios",
        "contact": "Contacto",
        "contact1": "Contacto 1",
        "contact2": "Contacto 2"
    }

    ....
}
```
### Localize an Attribute

To localize an attribute, add these attributes to the HTML element:

```HTML
data-attr-t <attribute_to_be_localized>-t="<key_in_JSON_file>"
```

**Example:**

```HTML
<input type="text" data-attr-t placeholder-t="form.yourFullName" name="name" required />
```
In this case, the utility will replace the value of `form.yourFullName` from the JSON file and it will assign it as the value of the `placeholder` attribute.

This part:

```HTML 
data-attr-t placeholder-t="form.yourFullName"
```
Will be replaced by `placeholder="<value>"` based on its value in the corresponding JSON file. 

Like this:

```HTML
<input type="text" name="name" required placeholder="Tu nombre completo">
```

## How to Add a New Language

With a command, you can use the HTML templates from the `templates` directory to generate new and translated HTML files. The translated strings are taken from the corresponding JSON file in the `locales` folder. 

You can find more details about this command and the steps to add a new language to the project below.

#### Step 1: Clone the Repository

First, clone the repository to a local copy of all the files and folders. 

You can do this with HTTPS with the command:

```
git clone https://github.com/freeCodeCamp/scrapepark.org.git
```

Alternatively, with SSH:

```
git clone git@github.com:freeCodeCamp/scrapepark.org.git
```

This will create a `scrapepark.org` folder.

#### Step 2: Install node-static-i18n

Next,to generate the new files with the translations, you need to install `node-static-i18n` with this command:

```
npm install -g static-i18n
```

**Note:** this will be installed globally, so you will be able to use it in the command line. 

#### Step 3: Create a New File in `templates/locales`

This new file must be a JSON file with the name of the new language in English. 

For example, to create an Italian version of the website, create this file on this path:

```
templates
|
|- locales
|  |
|  |- italian.json
```

**Note:** it's important to write the full name of the language to generate the path. Please do **not** abbreviate it.

#### Step 4: Add Translations to the JSON File

Once the file is ready, add the new and translated strings following the format of the existing JSON files. The new file should translate all the existing strings and it can have new strings (if this is necessary). 

**Note:** please follow the format of the JSON file found in the `locales` folder. The existing keys should be in the same relative order in all the files. 

#### Step 5: Generate the HTML Files with node-static-i18n

There are multiple ways to write the command that will generate the translated HTML files. 

The general syntax to generate the files for a language is:

```
static-i18n -l english -i <new_language> templates -o .
```

**Note:** for this command to work correctly, you should be in the root directory of the project. This way, the dot `.` in the command will refer to the root directory and the `/<new_language>` folder will be created in the root directory. 

**Example:**

```
static-i18n -l english -i spanish templates -o .
```

This command:
* Runs the static-i18n utility `static-i18n`. 
* Sets `english` as the default locale with `-l english`.
* Sets the locale that will be generated (`spanish` in this case) with `-i spanish`.
* Sets the directory where the files and locales are found (`templates`).
* Sets the output directory to the current directory with `-o .`. This will create a new folder with the name of the locale (`spanish` in this case) in the root directory. This folder will have the translated HTML files.

**Note:** the relative paths for images and resources will be updated automatically. By default, all the HTML files in the `templates` directory will be translated when you run this command. 

#### Step 6: Add the New Language to the Navigation Bar

After the directory and HTML files are generated, add your language to the dropdown menu in the navigation bar.

You should add this element:

```HTML
<li><a href="path_to_new_html_file" data-t>navbar.new_language</a></li>
```

**Note:** please replace **path_to_new_html_file** with the path to the index.html file in your language. For example: `/italian/index.html` and **new_language** with your new language in lowercase. For example: `italian`.

Here:

```HTML
<li class="nav-item dropdown">
    <a class="nav-link dropdown-toggle" href="#" data-toggle="dropdown" role="button" aria-haspopup="true" aria-expanded="true">
    <span class="nav-label" data-t>navbar.language</span>
    </a>
    <ul class="dropdown-menu">
    <li><a href="/index.html" data-t>navbar.english</a></li>
    <li><a href="/spanish/index.html" data-t>navbar.spanish</a></li>
    <!-- HERE, below the existing languages -->
    </ul>
</li>
```

Then, add your new language to the `english.json` file below the existing languages and to the JSON file in your language:

```JSON
{
    "navbar": {
        ...
        "language": "Language",
        "english": "English",
        "spanish": "Spanish",
        -----> HERE <-----
        "contact": "Contact",
        "contact1": "Contact 1",
        "contact2": "Contact 2"
    }
    ...
}
```

## Courses

The `courses` directory of this repository has versions of this website that have been used in courses created for freeCodeCamp. 

These versions **will not accept any pull requests** to guarantee that learners will see the same results when they follow the courses step by step.

## Copyright and Attribution

This website was created from a template in [Free Html Templates](https://html.design/).

* **Gustavo Juantorena** - Spanish translation and template modification.
* **Estefania Cassingena Navone** - Skateboard shop theme and template modification.

## License

Copyright © 2022 freeCodeCamp.org
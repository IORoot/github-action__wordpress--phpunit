
<div id="top"></div>

<div align="center">


<img src="https://svg-rewriter.sachinraja.workers.dev/?url=https%3A%2F%2Fcdn.jsdelivr.net%2Fnpm%2F%40mdi%2Fsvg%406.7.96%2Fsvg%2Fgithub.svg&fill=%23BEF264&width=200px&height=200px" style="width:200px;"/>

<h3 align="center">CI WordPress deployment example</h3>

<p align="center">
This is a working example of using a github action workflow to test a Wordpress plugin.
</p>    
</div>

##  1. <a name='TableofContents'></a>Table of Contents


* 1. [Table of Contents](#TableofContents)
* 2. [About The Project](#AboutTheProject)
	* 2.1. [Built With](#BuiltWith)
	* 2.2. [Installation](#Installation)
		* 2.2.1. [Main.yml](#Main.yml)
		* 2.2.2. [tests/Bootstrap.php](#testsBootstrap.php)
* 3. [Usage](#Usage)
* 4. [ Customising](#Customising)
* 5. [Troubleshooting](#Troubleshooting)
* 6. [Contributing](#Contributing)
* 7. [License](#License)
* 8. [Contact](#Contact)
* 9. [Changelog](#Changelog)



##  2. <a name='AboutTheProject'></a>About The Project

It's using the wordpress phpunit test suite.

This example does the following things:

- Install Ubuntu, MySQL, PHP, PHPUnit & Composer
- Download the current repo
- Download a second 'private' repo using a deploy key secret.
- Install your phpunit tests for the current plugin.
- Run PHPUnit 

<p align="right">(<a href="#top">back to top</a>)</p>


###  2.1. <a name='BuiltWith'></a>Built With

This project was built with the following frameworks, technologies and software.

* [Github](https://github.com/)

<p align="right">(<a href="#top">back to top</a>)</p>


###  2.2. <a name='Installation'></a>Installation


####  2.2.1. <a name='Main.yml'></a>Main.yml 

This file is commented and explains each part of it. Use it in your `/.github/workflows/main.yml` file within your repository.

####  2.2.2. <a name='testsBootstrap.php'></a>tests/Bootstrap.php

This file contains a little bit of customised code to pull in a second dependent plugin to test the original plugin.

My scenario was that I'm using the ACF plugin on the admin pages and needed to pull it in to test my plugin. 

The slight problem was that on my server, the folder structure will be:

    wp-content/
        plugins/
            advanced-custom-fields/
            my-cool-plugin/

But within the Github action container, the ACF plugin is being pulled into the same directory as the current repo, like this:

    wp-content/
        plugins/
            my-cool-plugin/ 
                advanced-custom-fields/

So the bootstrap.php file will check for the difference and load the approriate one, like this:

```php

    $path = '';
    if (!is_dir(dirname(dirname(__FILE__)) . '/second-plugin-to-add'))
    {
        $path = '../';
    }
    require dirname(dirname(__FILE__)) . '/'.$path.'second-plugin-to-add/my_second_plugin.php';		// ACF

```

Now it will run by pulling in ACF from the right location.



<p align="right">(<a href="#top">back to top</a>)</p>


##  3. <a name='Usage'></a>Usage

Github Actions.

##  4. <a name='Customising'></a> Customising

None.

##  5. <a name='Troubleshooting'></a>Troubleshooting

None.

<p align="right">(<a href="#top">back to top</a>)</p>


##  6. <a name='Contributing'></a>Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue.
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>



##  7. <a name='License'></a>License

Distributed under the MIT License.

MIT License

Copyright (c) 2022 Andy Pearson

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.

<p align="right">(<a href="#top">back to top</a>)</p>



##  8. <a name='Contact'></a>Contact

Author Link: [https://github.com/IORoot](https://github.com/IORoot)

<p align="right">(<a href="#top">back to top</a>)</p>

##  9. <a name='Changelog'></a>Changelog

- v1.0.0 - Initial Commit

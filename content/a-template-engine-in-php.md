---
date: "2013-05-22"
title: Building a template engine in PHP
type: post
---

Possibly the most common sign of bad code is tight coupling, especially between logic and presentation. It might seem like a good idea to print out the HTML while the data is being generated, but it more often than not leads to a big incoherent mess of tangled code. It also causes other issues, like what happens if an unexpected error occurs in the middle of the page? By then half the page has already been outputted and it might be too late to handle the error nicely.

There are a lot of problems with mixing logic and presentation, but it's actually very easily solved, especially in PHP. While PHP makes it unnecessarily easy to write shitty code it also provides a lot of ways to avoid it. I'll use this post to show you how ridiculously easy it is to create a template engine in PHP in three easy steps.

So, we begin by setting up a simple class to wrap our template. The $template variable passed in the constructor is the relative path to our template, e.g. if the templates are in a folder called "views" you should pass "views/.php" to the constructor.

    class Template
    {
        protected $template;

        public function __construct($template)
        {
            $this->template = $template;
        }
    }

Then we add variables to it, we use magic getters and setters for this to make handling of our template a little more verbose, but you can of course use regular getters and setters if you prefer that.

    class Template
    {
        protected $template;
        protected $variables = array();

        public function __construct($template)
        {
            $this->template = $template;
        }

        public function __get($key)
        {
            return $this->variables[$key];
        }

        public function __set($key, $value)
        {
            $this->variables[$key] = $value;
        }
    }

Lastly we add the printing of the template, this abuses some pieces of PHP's functionality. Partly that code can be included anywhere and that all the output can be stored and loaded into variables. We load all created variables into the functions variable scope with [extract()][1], this has the nice side effect of not conflicting with variables created outside the function and limiting the template file's access to variables created in the template. Also, by using [chdir()][2] before including the file, we change the working directory to the specified template directory (if any). This allows for including other templates within templates without having to concern ourselves with where the template will be loaded from.  

    public function __toString()
    {
        extract($this->variables);
        chdir(dirname($this->template));
        ob_start();

        include basename($this->template);

        return ob_get_clean();
    }

We can then use it anywhere we want like this. Of course, if you actually need functionality like this you might have more use for a template engine like [Twig][3], which is a bit more extensible and comes with a ton of cool features.  

    $view = new Template("path/to/template.php");

    $view->title = "Hello world!";
    $view->description = "This is a ridiculously simple template";

    echo $view;


 [1]: http://php.net/manual/en/function.extract.php
 [2]: http://php.net/manual/en/function.chdir.php
 [3]: http://twig.sensiolabs.org/

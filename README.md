# Froala WYSIWYG Editor Plugin for CakePHP 3

>CakePHP Plugin for Froala Javascript WYSIWYG Text Editor. For cake >=3.0 <4.0.0

## About
The purpose of placing [Froala WYSIWYG Editor](https://www.froala.com/wysiwyg-editor) in a plugin is to keep it separate from a themed view, the regular webroot or the app in general, which makes it easier to update and overall follows the idea of keeping the code clean and modular.

## Installation
To use Froala WYSIWYG Editor you need to clone git repository:

	git clone git://github.com/froala/wysiwyg-cake.git Plugin/Froala

Or if your CakePHP application is setup as a git repository, you can add it as a submodule:

	git submodule add git://github.com/froala/wysiwyg-cake.git Plugin/Froala

Alternatively, you can download an archive from the [master branch on Github](https://github.com/froala/wysiwyg-cake/archive/master.zip) and extract the contents to `Froala plugin`.


## Usage
The Froala helper is basically just a convenience helper that allows you to use php and CakePHP conventions to generate the configuration for Froala and as an extra it allows you to load configs.

```php
// Loads Froala Editor javascript also will load all the plugins and css for the plugins

<?= $this->Froala->plugin();?>

// Will target one specific html selector on which the editor will be init.
// Second paramenter is mix can be array/object of options that the Froala Editor will take.

<?= $this->Froala->editor('#froala', array('option' => value));?>
```

If your app is not set up to work in the top level of your host / but instead in /yourapp/ the automatic inclusion of the script wont work. You'll manually have to add the js file to your app inisde the helper class. 


```php
$this->Html->css('/yourapp/Froala/css/froala_editor.min.css');
$this->Html->script('/yourapp/Froala/js/froala_editor.min.js');
```

## How to use the helper

Since CakePHP 3.0 it is necessary to activate the plugin in your application. To do so,
edit `app/Config/bootstrap.php` and add the line `CakePlugin::load('Froala');` at the
bottom. If you already have `CakePlugin::loadAll();` to auto-load all plugins then you may skip this step.

Wherever you want to use it, load it in the controller

```php
class AppController extends Controller
{
.
.
	public $helpers = array('Froala.Froala');
```

In the view simply use the plugin() method so all the dependencies are loaded, and editor() method which you can pass options as key/value pairs in an array or object.

This is a simple init example with no options for the Froala Editor.
Check under examples more specific init methods.

```php
$this->Froala->plugin();
$this->Froala->editor('selector');
```

This will instruct Froala to convert the matched element on the page to Froala editor.

A complete list of [Froala configuration options](https://www.froala.com/wysiwyg-editor/docs/options) are on the website.


## Default options

If you want a quick way to configure default values for all the Froala Editors of an application, you could use the 'Froala.editorOptions' configuration.

Here is an example of a line you could have in `bootstrap.php`:

```php
Configure::write('Froala.editorOptions', array('height' => '300px',
                        'lineBreakerTags'=> ['table', 'hr', 'form']));
```

It will make all editors to have a 300px height and apply line braker tags. You may want to override this value for a single editor. To do so, just pass the option to the editor() method and it will override the default value.

## Usage examples

Example of init using array of options

```php

// '#comment'  Represents the html element selector.
// 'array()'   Represents the list of options that are passed to the editor.

$this->Froala->editor('#comment',array('colorsBackground' => ['#61BD6D', '#1ABC9C', '#54ACD2', 'REMOVE'],
                                         'colorsText'       => ['#61BD6D', '#1ABC9C', '#54ACD2', 'REMOVE']
                                        ));
                  
```

Example of RTL LTR Direction Buttons:

```php

// '#comment'  Represents the html element selector.
// 'array()'   Represents the list of options that are passed to the editor.

$this->Froala->editor('#comment',array('colorsBackground'=> ['#61BD6D', '#1ABC9C', '#54ACD2', 'REMOVE'],
                                         'direction' =>'rtl'
                                         ));
                                         
```
Example of limiting the Html tags and removing unwanted tags:

```php

// '#comment'  Represents the html element selector.
// 'array()'   Represents the list of options that are passed to the editor.

$this->Froala->editor('#comment',array('htmlAllowedTags' => ['p', 'h1', 'h2', 'h3', 'h4', 'h5', 'h6'],
	                                     'htmlRemoveTags'  => ['script', 'style', 'base']
                                         ));

```
Example of setting the toolbar buttons and toolbar position:

```php

// '#comment'  Represents the html element selector.
// 'array()'   Represents the list of options that are passed to the editor.

$this->Froala->editor('#comment',array('toolbarButtons' => ['bold', 'italic', 'underline'],
                                         'toolbarBottom' => true
                                         ));

```

Example of code beautifier passing options as object:

```php
// '#comment'  Represents the html element selector.
// '(object)'   Represents the list of options that are passed to the editor.


$this->Froala->editor'#comment',(object)  ['codeBeautifierOptions' =>[
                                              'end_with_newline' => true,
                                              'indent_inner_html'=> true,
                                              'extra_liners' =>['p', 'h1', 'h2', 'h3', 'h4', 'h5', 'h6', 'blockquote', 'pre', 'ul', 'ol', 'table', 'dl'],
                                              'brace_style' =>'expand',
                                              'indent_char' => ' ',
                                              'indent_size' => '4',
                                              'wrap_line_length'=> '0'
                                              ],]);

```

Example of using the editor in inline mode and allowing only some types of images: 

```php 

$this->Froala->editor('#comment',array('imageAllowedTypes' => ['jpeg', 'jpg', 'png'],
                                         'toolbarInline' => true
                                         ));

```


Example of using the tolbar sticky and setting an offeset for it:

```php 

$this->Froala->editor('#comment',array('toolbarSticky' => true,
                                         'toolbarStickyOffset' => '50'
                                         ));

```

## Requirements

* PHP version: PHP 5.2+
* jQuery javascript library <http://jquery.com/>

## Dependency Note

This plugin depends on jQuery (<http://jquery.com>) so you would need to ensure that it is loaded in your layout or the
view in which you want to display your editor. An example of how to load jQuery in your layout is shown below:


```php

<?= $this->Html->script(array('http://code.jquery.com/jquery-1.11.0.min.js')); ?>

<?= $this->fetch('script'); ?>

```

Of course, you can also use a copy of the jQuery library from your app/webroot/js folder.

<h2>License</h2>

The <code>Cakephp wysiwyg plugin</code> project is under MIT license. However, in order to use Cakephp Froala Editor plugin you should purchase a license for it.

Froala Editor has <a href="https://www.froala.com/wysiwyg-editor/pricing"> 3 different</a> licenses for commercial use. For details please see <a href="https://www.froala.com/wysiwyg-editor/terms"> License Agreement.</a>


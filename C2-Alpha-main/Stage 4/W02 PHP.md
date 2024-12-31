# **PHP Fundamentals**

**High-Level Goals**

By the end of this lesson, you will be familiar with the following:

- XAMPP
- First PHP Project
- Variables/Arrays Declaration
- Constants
- echo/ PHP with HTML
- PHP Functions

# **XAMPP**

XAMPP is a PHP development environment, it&#39;s an HTTP cross-platform web server.

Use [this link](https://sourceforge.net/projects/xampp/) to install XAMPP locally on your device.

Once it&#39;s downloaded click it to run the installer.

Once XAMPP is downloaded PHP will be automatically downloaded as well.

The root path of the Apache server is located at C:/Xamp/htdocs,

# **First PHP Project**

1. To create a new PHP project you have to make a new folder inside the Apache server root
2. Make a new file called index.php &#39;the main file of the project &#39;
3. A PHP script can be placed anywhere in the document.
4. A PHP script starts with \&lt;?php and ends with ?\&gt;:

```php
<?php
 
// write your code here
 
?>

```

1. Each PHP line must end with a semicolon (;)
2. A PHP script is executed on the server, and the plain HTML result is sent back to the browser.

# **Variables/Arrays Declaration**

1. All **variable** starts with a dollar sign ($):

```php
 
$name="Jouza";

```

1. **Arrays** are defined in two methods:

1. Method 1 (the classic method):

```php
$names= array("Jouza", "Sarah", "Mai");
```
1. Method 2:
```php
$names= ["Jouza", "Sarah", "Mai"];
```


**Associative Arrays:**

The associative arrays contain keys and values (like JS objects)


```php
$user= [
"name"=>"John",
"age"=>"27", 
"number"=>"123"
];

```

# **Constants**

Constant are unchangeable variables, it is defined in two methods:

1. It can be declared using the (define() ) method and it takes two parameters, the first one is the name of the constant (should always be in capital letters), the second parameter is the value of the constant.

```php
define("YEAR", "2021");
echo YEAR;

```


1. Write the keyword (const) then the constant name in capital letters then the value.

```php
const YEAR= "2021";
echo YEAR;

```

# **echo**

echo is used to output variables, it is not a function but language a construct

```php
echo "Hello", "I'm a PHP program";

```

**Using PHP with HTML tags:**

```php
<input placeholder="<?php echo 'Enter Your name Plz' ; ?>" type="text">


```

This can make fully functional web applications using PHP and HTML.

echo has a shortcut syntax that can be easily used inside HTML tags:
```html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>PHP</title>
</head>
    <body>
 
    <?php
        $user_name = "Sarah" ;
    ?>
 
    <p>Hello <?=$user_name ?> , what's in your mind?</p>
    
    </body>
    
</html>

```

# **PHP Functions**

Functions in PHP are declared using the keyword (function) and called using the name of the function followed with brackets:

```php
<?php
function greeting() {
  echo "Hello world!";
}
 
greeting();
?>



```

PHP has a lot of functions that can be easily used, such as:

**Filter:**

array\_filter: it filters the element of an array using callback functions, by taking two parameters the first is the array, and the second is the function.

```php
array_filter(array , function) ; 

```

Example:

Notice that we used ( print\_r ) instead of ( echo ) which prints the arrays and variables.
```php
<?php
 
    $ages = [15 , 20 ,12 , 50 , 33 , 11 , 18 , 60] ;
 
    // return all ages equles or grater than 18 ;
 
 
 
    $filtered_ages = array_filter($ages , function($value){ return $value >= 18 ; });
 
    print_r($filtered_ages);
?>


```

**Implode:**

It joins array element with a string:
```php
<?php
 
// syntax 
    implode(string , array);
 
// convert array to string and put comma between elements
    $countries = ['Jordan' , 'Egypt'  , 'Syria' , 'KSA'] ;
 
    echo implode(', ' , $countries);
?>


```


# **Pulse Check**

1. Download XAMPP and make your first PHP file, make sure it works by trying to print something using echo
2. Using [PHP documentation](https://www.php.net/) read about at least three functions and write an example about each one of them

php-salarydates
===============

Salary Date calculator for BrightPearl

# Usage

## Installation

Download source from [https://github.com/perchten/salarydates](https://github.com/perchten/salarydates) of `git clone` to any writeable directory.

	git clone git@github.com:perchten/salarydates.git <install_dir>

You will need to make the `install` script executable, and then run it

    $ cd <install_dir>
    $ chmod a+x ./install
    $ ./install
    

## Run the application

The app can be run without arguments, although a number are available. You will be prompted to accept the defaults if you run without arguments.

    $ cd <install_dir>
    $ ./salarydates

##### Arguments

	  -d, --debug             Print debug information to the console.
	  -f, --file <arg>        Set the output file, which will be overwritten if it exists. Default: ./salarydates_<year>.csv
	  -h, --help              Prints help details.
	  -p, --print             Print the calculated dates to the console.
	  -q, --quiet             Suppress all but the most critical or fatal messages. Explicitly requested printouts via the -p flag are unaffected.
	  -t, --dateformat <arg>  Specify the date format. Default: D j/n/Y (i.e. Mon 28/2/2012)
	  -v, --verbose           Print additional information to the console.
	  -y, --year <arg>        Set the year. Default: Current year

###### Output

Calculated dates are written to given file, or the default file under the `/reports` directory.

## Unit Testing

Unit testing uses [PHPUnit](http://phpunit.de/).

For compatibility reasons this project must use PHPUnit v3.7. To assure version compatibility please use the provided phpunit script.

	$ cd <install_dir>
	$ ./phpunit
	
# Project Structure

This project follows a standard directory structure with a `/src` directory containing the source files and a `/test` directory for unit testing.

The project uses [Composer](https://getcomposer.org/) for dependency management and autoloading. Loaded libraries are in the `/vendor` directory.

The main executable is `./salarydates`. This readme can be found at `README.md`.

	.
	├── src/
	├── test/
	├── vendor/
	├── reports/
	├── ...
	├── install
	└── salarydates
	
# Design Decisions

#### Interpretation of the brief

###### The Rules

* Sales staff get a regular monthly fixed base salary and a monthly bonus.
* The base salaries are paid on the last day of the month unless that day is a Saturday or a Sunday (weekend) in which case they are paid on the friday before.
* On the 15th of every month bonuses are paid for the previous month, unless that day is a weekend. In that case, they are paid the first Wednesday after the 15th.
* The output of the utility should be a CSV file containing the payment dates for this year. The CSV file should contain a column for the month name, a column that contains the salary payment date for that month, and a column that contains the bonus payment date.


###### Treatment of ambiguities

The bonuses are paid one month in arrears. It is unclear from the brief whether the outputted date in a row in the csv should be:
* the actual payment date that occurs in the month, but pays for the previous month or
* the date on which that month's bonus is paid, which will display a date in the next month 
 

#### Project Structure and Size

The brief stated a 'small' command line utility. There are a few different interpretations of the word 'small'. Based on the requirements for OOD and unit testing I figured that a straight hack script was not going to be an ideal solution. So I decided to go for a standardised project structure that could easily scale. 

Likewise I decided to make use of inheritance and helper classes split into seperate files to illustrate that scalable opinion. If I needed to rush a project out the door for a client and didn't need scalability, I could just have easily reduced the `/src` contents down to a single file or two, utilising functional programming paradigms.

#### Composer

I decided to use [Composer](https://getcomposer.org/) partly for fun, but also because it allows me to include and version manage some great third party libraries. Particularly 
* [Carbon](https://packagist.org/packages/nesbot/carbon) for the date management 
* [PHPUnit](https://packagist.org/packages/phpunit/phpunit) for unit testing
* [GetOpt](https://packagist.org/packages/ulrichsg/getopt-php), which I perhaps didn't need to use, but I do feel a command line utility should really adhere to standards and expectations if at all possible. Otherwise they can end up being really obtuse

I also took the opportunity to upload [a few additional useful packages](https://packagist.org/packages/perchten/) I've collected and wanted to expose for easier integration.

#### Executable

I figured the easiest and cleanest way to expose the executable was to keep all the core code in the src directory and simply expose a simple runnable script. 
 
	
# Author

Alastair Brayne ([al@perchten.co.uk](mailt:al@perchten.co.uk)). GitHub: [Perchten](https://github.com/perchten)



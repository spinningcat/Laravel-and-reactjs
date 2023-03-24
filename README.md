# Laravel-and-reactjs

# Book Search App

## This project contains two side of development. These are frontend and backend. Lets focus on Laravel first.

# Laravel Side

### Laravel application can be executed with command php artisan serve*


* First step: Creating database with this command -> create database bookdb;*
* You should select db you use with that command -> use bookdb*

In Laravel you need those infos in .env file to connect database and make some operation. In this assigment I am only focusing on **Search** operation

### Code beginning

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=bookdb
DB_USERNAME=root
DB_PASSWORD=qweASD123!

### Code End

* Create model and Migration gfile with this command -> php artisan make:model -m books

### Code beginning

Schema::create('books', function (Blueprint $table) {
    $table->id();
    $table->string("Title");
    $table->string("Author");
    $table->integer("Publication_Year");
    $table->string("Description");
    $table->timestamps();
});
### Code End

* php artisan migrate will create related table. 

## Seeders

* Kaggle has lots of useful dataset i am sure i can use some.

Link: https://www.kaggle.com/datasets/bilalyussef/google-books-dataset-> It is downloadable.

* Now i will insert some data to the database by using seeders.*
* The command we need is -> php artisan make:seeder BookSeeder *

Note: I used .text as type of title and description. It is likely data can be long and exceed the limitation of varchar.

### Code beginning

$table->text("Title");
$table->text("Description");

### Code end

Next step is search api located in BookController.

### Code beginning
I get parametername and parameter value from querystring.*
Later i will check if the parameter name is year or author in order to
construct necessary code line. Please check line 35 and line39*

$parameterName = $Request->get('ParameterName');
$parameterValue = $Request->get('ParameterValue');

### Code end

### Example data 

  Example year -> 2015 
  Example Author -> Hajime Isayama

## React side
  * Install packages with npm install first *
  * React application can be executed with command npm run dev*
  
### Code beginning

  const [inputText, setInputText] = useState('');
  const [post, setPost] = useState([]);
  
### Code end

I user first useState to get the data from inputbox when click event carried out.
Second usestate is for gettinr data from backend with the help of axios.
### Code beginning
 // The piece below is to decide the input is Year or Author. I am using regex for tat.
 // Year does not have letter and author does not have number at least in my dataset.
   if(/^[0-9]+$/.test(inputText)){
     params = new URLSearchParams([["ParameterName", "year"], [ "ParameterValue", inputText  ]]);
    }
    else{
      params = new URLSearchParams([["ParameterName", "author"], [ "ParameterValue", inputText  ]]);
    }
 ### Code End 


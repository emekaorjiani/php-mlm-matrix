MLM Matrix
Library for working with MLM matrices.

What is an MLM matrix?
In MLM on the Internet, the most popular form of marketing plan is matrix. Matrices can be of different types and with different number of levels. Usually there are 3 - 4 levels. For example, a cubic matrix of 3 levels will look like this:

demo

After the matrix is ​​closed, the person at level 1 receives a reward, and the MLM matrix is ​​divided into several matrices (depending on the type, for example, the cubic matrix is ​​divided into 3 new matrices). After that, the new matrices wait for filling and the cycle repeats.

Installation
The preferred way to install this widget is through a composer .

Run in the console

php composer.phar require --prefer-dist nepster-web/php-mlm-matrix "*"
or add

"nepster-web/php-mlm-matrix": "*"
in the file composer.jsonin the require section.

Structure:
Matrix.php - Library for working with matrices.

Render.php - generator html code matrix.

shema / matrix.sql - SQL (MySql) Scheme of tables for matrices.

Examples of using:
Empty matrix generation

$ view  =  2 ; 
$ level  =  3 ; 
$ matrix  =  new  Matrix ( $ view , $ level ); 
$ matrix -> generation (); 
$ matrix -> getArray (); // At the output array array
Fill the matrix with users

$ users  = [ 
    [ 
' level ' => 0 , ' number ' => 0 , ' user ' => ' Nepster ' ,     ] ]; $ matrix = new Matrix ( $ view , $ level ); $ matrix -> generation ( $ users ); $ matrix -> getArray ();          
          
          


   

note

Each array must contain the level and number keys , on the basis of which the position in the matrix is ​​determined.

You can use the callback function for personal tasks:

$ users  = [ 
    [ 
' level ' => 0 , ' number ' => 0 , ' user ' => ' Nepster ' ,     ] ]; $ function = function ( $ l , $ n , $ user , $ matrix ) { $ user [ ' position ' ] = $ matrix -> getPosition ( $ user [ ' level '          
          
          


  
     ], $ user [ ' number ' ]); 
return $ user ; };}; $ matrix = new Matrix ( $ view , $ level ); $ matrix -> generation ( $ users , $ function ); $ matrix -> getArray ();     

   

All available methods

// Generate array array
 generation ( array  $ users  = [], $ callback  =  null )

// Get array array
 getArray ()

// The view
 getView ()

// Number of levels
 getLevels ()
 // Get position coordinates of getCoordByPosition ( $ position )    



// Get the position number
 getPosition ( $ level , $ number )
 // Get the coordinates of the first free position in the getCoordFirstFreePosition () matrix // Get all the free coordinates in the getFreeCoords ()    


    



// Get all the available positions in the matrix
 getFreePositions ()

// Checks if the matrix
 isFilled ()

// Divide the
 division ()
Instructions

For example, this library presents a database schema, which consists of 3 tables:

matrix_type - Типы матриц

matrix - Все матрицы

matrix_users - Пользователи в матрицах
To work with matrices, you need to create an entry in the matrix_type table (for example, Peket # 1 for $ 10), create the matrix itself in the matrix table and activate the users. By activating users, we mean entries in the matrix_users table. To show the matrix on the screen, you need to extract an array of users and generate a matrix, and then refer to the renderer.

After each activation, do not forget to check whether the matrix is ​​full or not. This can be done by calling the isFilled () method , which returns true if there are no more free positions in the matrix. In this case, you need to call the division () method and store the new matrixes in the matrix table, also remember to add new entries to the matrix_users table after the division and close the old matrix assigning it a certain status.

Matrix Render:
use  nepster \ matrix \ Matrix ; 
use  nepster \ matrix \ Render ;

// Matrix generation 
$ users  = [
    [
 ' level ' => 0 , ' number ' => 0 , ' user ' => ' Nepster ' ,    ]]; $ function = function ( $ l , $ n , $ user , $ matrix ) { $ user [ ' position ' ] = $ matrix -> getPosition ( $ user [          
          
          


  
     ' level ' ], $ user [ ' number ' ]); 
return $ user ; };}; $ matrix = new Matrix ( 2 , 3 ); $ matrix -> generation ( $ users , $ function );     

   



// Render the matrix 
$ Render  =  new  Render ( $ matrix ); 
$ Render -> setOptions ([ ' class '  =>  ' matrix ' ]); 
$ Render -> setLevelOptions ([ ' class '  =>  ' level ' ]); 
$ Render -> setGroupSeparatorOptions ([ ' class '  =>  ' matrix-group-separator ' ]); 
$ Render -> setClearOptions ([ ' =>  ' clear: both ' ]); 
$ Render -> setGroupJoinOptions ([ ' class '  =>  ' matrix-join-group ' ]); 
$ Render -> registerLevelCallback ( function ( $ l , $ users ) { 
return ' <div class = "level-counter"> Level ' . ( ++ $ l ) . ' </ Div> ' ; }); $ Render ->       

$ number , $ user , $ matrix ) { 
return ' <div class = "cell"> ' . $ matrix -> getPosition ( $ level , $ number ) . '             <div class = "user">                   Avatar                   <div class = "matrix-user-info">                     More Information                   </ div>             </ div>             Login         </ div> ' ; }); echo $ Render -> show ();     
               









 
Example of HTML and CSS markup:

<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8" />
<title>MLM Матрица</title>
<style type="text/css">
    .matrix {
        margin:auto;
    }

    .matrix .level {
        width: 680px;
        min-height: 20px;
        margin: 20px auto;
        text-align: center;
        clear: both;
        border: dashed 1px #D3D3D3;
    }

    .matrix .level-counter {
        margin-bottom: 10px;
        display: block;
        text-align: left;
        font-size: 13px;
        font-weight: bold;
        padding: 10px 5px 0 10px;
    }

    .matrix .user {
        width: 45px;
        height: 45px;
        border: double 3px silver;
        overflow: hidden;
        font-size: 13px;
        margin: 5px auto;
    }

    .matrix .user .avatar {
        width: 39px;
        height: 39px;
        overflow: hidden;
    }

    .matrix .user .avatar img{
        width: 39px;
        min-height: 39px;
    }

    .matrix .cell {
        width: 60px;
        display: inline-block;
        border: dashed 1px #D3D3D3;
        margin: 10px 0px;
        padding: 5px 1px 5px 1px;
        overflow: hidden;
        text-align: center;
    }

    .matrix .matrix-join-group {
        display:inline-block;
    }

    .matrix .matrix-group-separator {
        width: 10px;
        display: inline-block;
    }

    .matrix .matrix-user-info {
        display: none
    }

    .matrix .user:hover .matrix-user-info {
        display: block;
        position: absolute;
        width: 200px;
        min-height: 30px;
        border: double 3px silver;
        background: #8BAA79;
        padding: 10px;
        margin-left: -3px;
        margin-top: -3px;
        color: white;
        font-size: 12px;
        font-weight: bold;
        letter-spacing: 1px;
    }
</style>

</head>
<body>

    // Рендер матрицы

</body>
</html>

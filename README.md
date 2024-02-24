# Hiding PHP Environment Varaibles

A basic vanilla PHP function to load variables from an `.env` file.

When you are creating a basic vanilla PHP project and want to keep your database credentials and/or API key out of your GitHub repository you can use a `.env` file. 

1. Create a file called `.env` and place it in your project folder.

2. Put your actual database credentials and API keys in your `.env``file:
    
    ```php
    DB_HOST=<DB_HOST>
    DB_DATABASE=<DB_DATABASE>
    DB_USERNAME=<DB_USERNAME>
    DB_PASSWORD=<DB_PASSWORD>
    
    API_SECRET=real_api_key
    ```

3. Create a second copy of your `.env` file and name it `.env.sample`. Use this file to provide instructions to the next programmer using your project code:
    
    ```php
    DB_HOST=localhost
    DB_DATABASE=database
    DB_USERNAME=username
    DB_PASSWORD=password
    
    API_SECRET=api_key
    ```

4. Make sure your GitHub repo does not include the file named `.env`. In your `.gitignore` file add:
    
    ```
    .env
    ```

> [!Note]
> I have excluded this step in this repo so you can view both the `.env` and `.env.sample` files. 

5. If your `.env` file is accessible from a browser, use a `.htaccess` file to hide your `.env` file:
    
    ```sh
    <Files .env>
    order allow,deny
    Deny from all
    </Files>
    ```

6. In your database connection file, add this function to load the variables from the `.env` file, and place them in matching constants:
    
    ```php
    $env = file(__DIR__.'/.env', FILE_IGNORE_NEW_LINES | FILE_SKIP_EMPTY_LINES);
    
    foreach($env as $value)
    {
      $value = explode('=', $value);
      define($value[0], $value[1]);
    }
    ```

7. Finally, you can use the contants in your database connection and any API code:
    
    ```php
    $connect = mysqli_connect(DB_HOST, DB_USERNAME, DB_PASSWORD, DB_DATABASE);
    ```

***

## Repo Sesources

* [Visual Studio Code](https://code.visualstudio.com/) 
* [PHP](https://php.net)

<a href="https://codeadam.ca">
<img src="https://codeadam.ca/images/code-block.png" width="100">
</a>



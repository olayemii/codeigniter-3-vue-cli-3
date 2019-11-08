# CodeIgniter 3 + Vue CLI 3  

- Make a new codeigniter project  
  
- Make a public folder in your codeigniter root directory (build files will live here)  
  
- Copy index.php from root directory into the public directory  
  
- Edit index.php and fix path of system and application to `../system` and `../application` respectively.  
  
- Create a virtual host that points to the `public` directory created.  
  
This demo assumes you are serving this CodeIgniter  at  `civue.test` (using vhost). If you are serving the Codeigniter at a different local URL, modify it accordingly in  `frontend/vue.config.js`.

### To Run the Frontend

``` sh
cd frontend  
npm install  
npm run serve

# build for production:
npm run build
```

### Steps for Scaffolding From Scratch

 1. Create CodeIgniter Project

 2. Create a Vue CLI 3 project in the Codeigniter app

    ``` sh
    vue create frontend
    ```

 3. Copy index.php from root directory into the public directory `frontend/public`

 4. Configure Vue project

    Create `frontend/vue.config.js`:

    ``` js
    module.exports = {
      devServer: {
        proxy: 'http://civue.test'
      },
      // note the "build" script in package.json needs to be modified as well.
      outputDir: '../public',

      // modify the location of the generated HTML file.
      // make sure to do this only in production.
      indexPath: process.env.NODE_ENV === 'production'
        ? '../application/views/home.php'
        : 'index.html'
    }
    ```

    Edit `frontend/package.json`:

    ``` diff
    "scripts": {
      "serve": "vue-cli-service serve",
    - "build": "vue-cli-service build",
    + "build": "rm -rf ../public/{js,css,img} && vue-cli-service build --no-clean",
      "lint": "vue-cli-service lint"
    },
    ```

 5. Configure CodeIgniter for single-page app.

    **application/config/routes.php**

	change `$route['default_controller'] = 'welcome';` to `$route['default_controller'] = 'home';`
	
### Make the Home controller

   **application/controllers/Home.php**

   ```php
   <?php
	defined('BASEPATH') OR exit('No direct script access allowed');    
	class Home extends CI_Controller {    
		public function index()    
		{  
			$this->load->view('home');    
		 } 
	}
   ```
   
**create the home view**  
  
**application/views/home.php**  
  
Leave empty for now




([Credits](https://github.com/yyx990803/laravel-vue-cli-3))

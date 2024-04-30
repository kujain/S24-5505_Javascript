
## WORKFLOW WITHOUT ES6 MODULES

1. Make sure you are running code 18 or higher.
2. Install gulp globally: `npm install gulp gulp-cli -g`
    
    In case of permissions error: `sudo npm install gulp gulp-cli -g`

3. Download the drop in template from here: https://github.com/kujain/S24-5505_Javascript/blob/main/final_boilerplate_template.zip
4. in the folder run: 
  ```
  npm install
  ```
  This will create package.lock and node-modules folder.
5. Run gulp:
```
npm start
```
OR 
```
gulp
```
6. You should see the dist folder created and your index.html file opened in the browser. Verify all is working. Note: always work in the src folder - the dist folder is always overwritten by gulp.
7. Drop in your js, html and scss (or css) filter in the `src` folder where needed. Change as needed. Run `npm start` again to recomplie and test.
8. For packaging for submission or github, please include ALL files EXCEPT: node-modules (Techincally dist folder is also not needed, but it's ok to have it in case npm doesn't work as expected when I review).

## WORKFLOW WITH ES6 MODULES

1. Make sure you are running code 18 or higher.
2. Install gulp globally: `npm install gulp gulp-cli -g`
    
    In case of permissions error: `sudo npm install gulp gulp-cli -g`

3. Download the drop in template from here: https://github.com/kujain/S24-5505_Javascript/blob/main/final_es6_boilerplate_template.zip
4. in the folder run to install all required node packages: 
  ```
  npm install
  ```
  This will create package.lock and node-modules folder.
5. Run gulp:
```
npm start
```
OR 
```
gulp
```
6. You should see the dist folder created and open your index.html file in the browser. Verify all is working.
7. Drop in your es6 js modules, html and scss (or css) filter in the src folder where needed. Change as needed. Run `npm start` again to recomplie and test.
8. For packaging for submission or github, please include ALL files EXCEPT: node-modules (Techincally dist folder is also not needed, but it's ok to have it in case npm doesn't work as expected when I review).

# notebook

### 14/04/2018
When I try to change the default directory of handlebar views
```
server.set('view engine', 'hbs')
server.set('views', path.join(__dirname, 'views'))
server.engine('hbs', hbs({
  extname: 'hbs',
  defaultLayout: 'main'
}))
```
There is an error message:
Error: ENOENT: no such file or directory, open '/Users/frank/Desktop/EDAWorkspace/pp/colorful-life/views/layouts/main.hbs'

google and find the <a href="https://github.com/ericf/express-handlebars/issues/147">solution</a>
But this new change didn't update to npm.  
so in node_modules we need to add below code into express-handlebars.js manually  
```
     if (viewsPath) {
         view = this._getTemplateName(path.relative(viewsPath, viewPath));
+        this.partialsDir = path.join(viewsPath, 'partials/');
+        this.layoutsDir = path.join(viewsPath, 'layouts/');
     }

```

Problem solved.

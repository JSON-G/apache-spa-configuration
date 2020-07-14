<h1>Apache htaccess configuration for (SPA) Single Page Applications</h1>

<p>These are helpful codes for your <code>.htaccess</code></p>
<p>These codes can help route the requests to <code>index.html</code> to enable client-side routing to kick in (e.g., react-router-dom BrowserRouter).</p>

```
RewriteEngine on

# [optional] redirect http to https (provided you have certificate configured)
# RewriteCond %{SERVER_PORT} 80
# RewriteRule ^(.*)$ https://yourwebsite.com/$1 [R,L]

# [spa-implementation] route admin requests to admin subdirectory index.html
# in this case, simply replace `admin` with your subdirectory folder name
RewriteCond %{REQUEST_URI} admin
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule  ^(.*)$ /admin/index.html?path=$1 [NC,L,QSA]

# [spa-implementation] route all requests to index.html to use client-side routing
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ /index.html?path=$1 [NC,L,QSA]
```
<b>Notes:</b><br>
<p>These codes assumes that <code>index.html</code> is the entry point for your SPA</p>
<p>These codes assumes that your project is hosted at root directory (subdirectory for admin) and <code>.htaccess</code> is seated at root as well.</p>

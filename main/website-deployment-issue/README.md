# Solutions to React Router 404 Error on Refresh After Deployment

This document provides solutions for resolving the **404 error** encountered when refreshing URLs in a React application using React Router after deploying to **cPanel or a VPS**.

## cPanel Problem

When deploying a React application to cPanel with React Router for client-side routing, you may encounter a 404 error upon refreshing the URLs. This occurs because cPanel's default behavior does not correctly handle single-page applications (SPAs).

## cPanel Solution

To resolve this issue and ensure that React Router functions correctly after deployment on cPanel, follow these steps:

1. **Create an `.htaccess` File**:

   - Navigate to your cPanel's `public_html` directory (or the directory where your React app is deployed).
   - Create a new file named `.htaccess`.

2. **Add the Following Code**:

   - Open the newly created `.htaccess` file and add the following code:

   ```apache
   <IfModule mod_rewrite.c>
     RewriteEngine On
     RewriteBase /
     RewriteRule ^index\.html$ - [L]
     RewriteCond %{REQUEST_FILENAME} !-f
     RewriteCond %{REQUEST_FILENAME} !-d
     RewriteRule . /index.html [L]
   </IfModule>
   ```

## VPS Problem

Similar to the cPanel issue, when deploying a React application to a VPS and using React Router for client-side routing, you may encounter a 404 error when refreshing the URLs. This is because the server may not be configured to serve the index.html file for all routes.

## VPS Solution

To resolve this issue and ensure that React Router works correctly after deployment on a VPS, follow these steps:

1. **Access URL Rewrite Settings:**:

   - Go to the "Website" or "Website List" section in your server management interface.
   - Click on the site name for which you want to apply the changes.

2. **Configure URL Rewrite:**:

   - Add the following configuration to handle routing:

   ```apache
   location / {
   try_files $uri /index.html;
   }
   ```

---

## Conclusion

By following the above solutions, you should be able to resolve the 404 errors encountered when refreshing URLs in your React application after deployment in cPanel or a VPS server. This will ensure smooth navigation in your application without any issues.

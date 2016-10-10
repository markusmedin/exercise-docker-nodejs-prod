# exercise-docker-node-prod

In this exercise you should try to get a feeling of how to build and create a node application for production mode using docker(-composer). 

#First navigate to your exercise repository
git remote add docker-nodejs-prod https://github.com/1dv032/exercise-docker-node-prod/
git subtree add --prefix=docker-nodejs-prod --squash docker-nodejs-prod master
cd docker-nodejs-prod
You should now have a folder called docker-nodejs-dev in your exercise repo.

## The application
This repository includes the application beeing published. It is just a template application with a simple startpage showing a green text (set by the CSS-rule in the folder app/src/public/css/style.css) saying "Hello template!" and a image (in the folder app/src/public/img/icon.png).

We are going to add a reversed proxy to proxy all request for the node application. The application is a an express application and serve all it static content through the url /static (not /public). Your nginx should point all request starting with /static and not through the node.js application. For more information on how express handles static content: http://expressjs.com/en/starter/static-files.html

The reversed proxy should also set up a self signed HTTPS certificate and also serve all static files (like css, js, imges). The idea is to have a nginx as a reversed proxy and a node application running behind. This means that we can let the nginx-server handle the HTTP encryption to the client (the traffic between nginx and the node-application could use unencrypted HTTP). This exercise only contain two part (the reversed proxy and the application) but ofcourse you can add more servers like a db-server ect.

More information about HTTPS and node.js in production you will find below the requirements.

## Requirements
* The goal is to build a solution with dockerfiles and docker-compose. 
* The reversed proxy should listen to port 80 and port 443. When a client sends a request to port 80 (HTTP) it should be redirected to port 443 (HTTPS) by the reversed proxy. 
* All static contents should be requested (by application design) to /static. This should be done in the reversed proxy.
* When visiting the site the green text and green image with the checkmark should be seen.
* The solution should be able to run with:
  * `docker-compose build` and `docker-compose up`

## Handling the HTTPS
In a real world senario you will have to by a certificate to run HTTPS in your own domain. In the excercise (and course) we could use so called self-signed certificates. This means that the developer self could amke certificates that encrypt the traffic between server and client. This is of course not a good way to do it and your browser will probably screem when visiting the site (you have to manual proceed). This is OK for this course but you could also look inte solutions like ["Lets encrypt"](https://letsencrypt.org/) - You will be needed to own a domain name to use that.

## Running node.js in production

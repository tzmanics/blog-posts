Containerizing your apps is useful in many ways, especially when it comes to creating a consistent environment for testing and deployment. Using Docker with your React application is a great way to take your application to the next level and bring it into the shareable ecosystem. Containerization also gives you the opportunity to start taking advantage of continuous integration practices if you haven’t already.

To start out you can add a `Dockerfile` to your existing React application or on to a new project you create using `create-react-app` to generate it. Here is an initial `Dockerfile` from a great article on [Dockerizing React Applications for Continuous Integration](https://www.telerik.com/blogs/dockerizing-react-applications-for-continuous-integration) from [Taylor Jones](https://www.telerik.com/blogs/author/taylor-jones).

```
# The Node version that we'll be running for our version of React.
# You may have to search the Node directory for a version that fits
# the version of React you're using.
FROM node:8.9-alpine

# Create a work directory and copy over our dependency manifest files.
RUN mkdir /app
WORKDIR /app
COPY /src /app/src
COPY ["package.json", "package-lock.json*", "./"]

# If you're using yarn:
#  yarn build
RUN npm install --production --silent && mv node_modules ../

# Expose PORT 3000 on our virtual machine so we can run our server
EXPOSE 3000
```

Once you have this in place you then need to orchestrate your containers by adding a `docker-compose` file. In this file you configure your container environments and other information to tailor it to your needs. When you have your `docker-compose` file setup you can run a few Docker commands to build and run your containers:

`docker-compose build <service-name>`
`docker-compose up <service-name>`

To get the detailed steps plus learn more about Dockerizing React Applications for Continuous Integration, check out  [Taylor Jones’s](https://www.telerik.com/blogs/author/taylor-jones) [step-by-step article](https://www.telerik.com/blogs/dockerizing-react-applications-for-continuous-integration). Stop fussing with inconsistent testing environments and the pains of debugging differences between development environments and production environments. Containerize your React app to give yourself more consistency and, hopefully, less headaches.

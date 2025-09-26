# Lab 3 (CST8915) <br> pate1595

### Youtube Video link: <br>
https://youtu.be/iCJNPMtYno0

---

### Reflection Questions:

1. What challenges did you encounter when configuring environment variables in the GitHub Actions workflow?<br>
-> The main challenge was that my workflow was looking for a requirements.txt file. Since it was missing at first, the build failed. I had to create the file with the correct dependencies so the workflow could install everything properly.

2. How does deploying microservices on Azure Web App Service differ from running them locally?<br>
-> Running locally is simple because everything uses localhost and works on my own computer. Deploying to Azure is different because each service runs in its own App Service with a unique URL. I also had to configure startup commands, environment variables, and fix CORS issues so that the services could talk to each other.

3. Why is it important to use environment variables for configurations in a cloud environment?<br>
-> Environment variables keep sensitive information (like keys, secrets, and URLs) out of the source code. They also make it easier to change settings between environments (local, test, production) without editing the code. This makes the app safer, more flexible, and easier to manage in the cloud.

---
### Repo links:
https://github.com/Jigarkumar25/order-service-demo <br>
https://github.com/Jigarkumar25/product-service-demo-python-lab3 <br>
https://github.com/Jigarkumar25/store-front-demo   

---
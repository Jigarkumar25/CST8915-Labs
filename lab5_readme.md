# Lab 5 (CST8915) <br> pate1595

### Youtube Video link: <br>

https://youtu.be/Klve7wpP1Tc

---

## docker-compose.yml:
version: '3'

services:
  rabbitmq:
    image: "rabbitmq:3-management"
    ports:
      - "5672:5672"
      - "15672:15672"
    environment:
      - RABBITMQ_DEFAULT_USER=myuser
      - RABBITMQ_DEFAULT_PASS=mypassword

  order-service:
    image: jigarkumar25/order-service:latest
    ports:
      - "3000:3000"
    environment:
      - RABBITMQ_CONNECTION_STRING=amqp://myuser:mypassword@rabbitmq:5672/
      - PORT=3000
    depends_on:
      - rabbitmq

  product-service:
    image: jigarkumar25/product-service:latest
    ports:
      - "3030:3030"
    environment:
      - PORT=3030

  store-front:
    image: jigarkumar25/store-front:latest
    ports:
      - "80:80"
    environment:
       - VUE_APP_ORDER_SERVICE_URL=http://order-service:3000
       - VUE_APP_PRODUCT_SERVICE_URL=http://product-service:3030
    depends_on:
      - product-service
      - order-service


--- 
### Better version to just see in preview(I used &nbsp and br tags):
version: '3' <br>
<br>
services: <br>
&nbsp;&nbsp;rabbitmq: <br>
&nbsp;&nbsp;&nbsp;&nbsp;image: "rabbitmq:3-management" <br>
&nbsp;&nbsp;&nbsp;&nbsp;ports: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- "5672:5672" <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- "15672:15672" <br>
&nbsp;&nbsp;&nbsp;&nbsp;environment: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- RABBITMQ_DEFAULT_USER=myuser <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- RABBITMQ_DEFAULT_PASS=mypassword <br>
<br>
&nbsp;&nbsp;order-service: <br>
&nbsp;&nbsp;&nbsp;&nbsp;image: jigarkumar25/order-service:latest <br>
&nbsp;&nbsp;&nbsp;&nbsp;ports: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- "3000:3000" <br>
&nbsp;&nbsp;&nbsp;&nbsp;environment: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- RABBITMQ_CONNECTION_STRING=amqp://myuser:mypassword@rabbitmq:5672/ <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- PORT=3000 <br>
&nbsp;&nbsp;&nbsp;&nbsp;depends_on: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- rabbitmq <br>
<br>
&nbsp;&nbsp;product-service: <br>
&nbsp;&nbsp;&nbsp;&nbsp;image: jigarkumar25/product-service:latest <br>
&nbsp;&nbsp;&nbsp;&nbsp;ports: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- "3030:3030" <br>
&nbsp;&nbsp;&nbsp;&nbsp;environment: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- PORT=3030 <br>
<br>
&nbsp;&nbsp;store-front: <br>
&nbsp;&nbsp;&nbsp;&nbsp;image: jigarkumar25/store-front:latest <br>
&nbsp;&nbsp;&nbsp;&nbsp;ports: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- "80:80" <br>
&nbsp;&nbsp;&nbsp;&nbsp;environment: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- VUE_APP_ORDER_SERVICE_URL=http://order-service:3000 <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- VUE_APP_PRODUCT_SERVICE_URL=http://product-service:3030 <br>
&nbsp;&nbsp;&nbsp;&nbsp;depends_on: <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- product-service <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;- order-service <br>


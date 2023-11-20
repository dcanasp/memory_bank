#python

library that allows you to make multiple request at a time, you just install

and on a file named "locustfile.py"  ***this is very important***

```python 
from locust import HttpUser, task

class HelloWorldUser(HttpUser):
    @task
    def hello_world(self):
        self.client.get("/hello")
```

to run just write on the command line
```bash
locust
```

and on the [[port]] 8089 the webpage will appear (http://localhost:8089/)

the website will look like this
![[locust.png]]
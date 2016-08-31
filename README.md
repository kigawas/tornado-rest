PyRestful
---------

pyRestful is an API to develop restful services with Tornado Web Server.

We made changes from the last version to improve it and make it more easy.

The last version works with Python 2 and 3.

Installation
------------

You must have installed python version 2.7 or 3.4.

Download the api from github (https://github.com/rancavil/tornado-rest/archive/master.zip).

Unzip the file tornado-rest-master.zip

     $ unzip tornado-rest-master.zip

Go to the directory and install.

     $ cd tornado-rest-master
     $ python setup.py install

Or you can install it using.
     
     $ pip install pyrestful

(https://pypi.python.org/pypi/pyrestful/)

Example
-------

With this API allows service development rest allowing access to resources, 
as follows (see the demos).

The API allows develop a CRUD over the resources. In this example the 
resource is Customer.

GET: http://myserver.domain.com:8080/customer/{id}

     GET /customer/1 HTTP/1.1

     GET it is equivalent to SELECT.

POST: http://myserver.domain.com:8080/customer

     POST /customer HTTP/1.1
     Host: myserver.domain.com
     
     customer_name=Rodrigo&customer_address=Santiago

     POST it is equivalent to INSERT.

PUT: http://myserver.domain.com:8080/customer/{id}

     PUT /customer/1 HTTP/1.1
     Host: myserver.domain.com
     
     customer_name=Rodrigo&customer_address=Santiago
     
     PUT it is equivalent to UPDATE.

DELETE: http://myserver.domain.com:8080/customer/{id}

     DELETE /customer/1 HTTP/1.1

     DELETE it is equivalent to DELETE.

PyRestful implements the verbs get, post, put and delete.


Echo Rest Service
-----------------

This example implements a Echo Rest Service (echo_service.py).

Write the next code and save echo_service.py file.

     import tornado.ioloop
     import pyrestful.rest

     from pyrestful import mediatypes
     from pyrestful.rest import get

     class EchoService(pyrestful.rest.RestHandler):
          @get(_path='/echo/{name}', _produces=mediatypes.APPLICATION_JSON)
          def sayHello(self, name):
               return {'Hello':name}

     if __name__ == '__main__':
          try:
               print('Start the echo service')
               app = pyrestful.rest.RestService([EchoService])
               app.listen(8080)
               tornado.ioloop.IOLoop.instance().start()
          except KeyboardInterrupt:
               print('\nStop the echo service')

Execute the service with.

     $ python echo_service.py

Then in a browser write the url.
     
     http://localhost:8080/echo/rodrigo

You should see the following output in your browser.

     {'Hello': 'rodrigo'}

The Blogapi app is a simple web API study project intended to explore the powerful Django REST Framework. Typical blog full CRUD functionality is implemented – users can register with the app, publish blog posts, etc. This app supports multiple front-ends written in different languages and frameworks.

The Blogapi app is available here
https://blogapi-lugres.fly.dev/api/v1/

App’s functionality was covered by necessary tests. Custom user model was implemented, proper user permissions/authorizations were configured (e.g. only authors of the post can edit/delete them, logged-out users don’t have access) as well as token authentication. Dj-rest-auth and Django-allauth packages were used to ensure log-in, log-out and registration endpoints. Viewsets and a simple router was used to optimize the codebase. A dynamic API schema and documentation were prepared with the help of drf-spectacular package according to the OpenAPI 3 specification (Redoc and SwaggerUI):
https://blogapi-lugres.fly.dev/api/schema/redoc/
https://blogapi-lugres.fly.dev/api/schema/swagger-ui/

You can test the API endpoints by using the above links, or by following the steps with the curl command line tool:
1)	Create an account (use your own username and password!)
curl -XPOST -H "Content-type: application/json" -d '{
      "username": "user1","email": "user1@email.com",
      "password1": "complexpassword123",
      "password2": "complexpassword123"
  }' 'https://blogapi-lugres.fly.dev/api/v1/dj-rest-auth/registration/'
2)	Log in to obtain an authentication token
curl -XPOST -H "Content-type: application/json" -d '{
      "username": "user1",
      "password": "complexpassword123"
  }' 'https://blogapi-lugres.fly.dev/api/v1/dj-rest-auth/login/'
3)	Now pass the token in the Authorization header to fetch the user details
curl -XGET -H 'Authorization: Token be36bc8a282679734531748a71b036d4e4303aa2' \                      
    -H "Content-type: application/json" 'https://blogapi-lugres.fly.dev/api/v1/dj-rest-auth/user/'
4)	By logging-out, the token will be destroyed
curl -XPOST -H 'Authorization: Token be36bc8a282679734531748a71b036d4e4303aa2' \
    -H "Content-type: application/json" 'https://blogapi-lugres.fly.dev/api/v1/dj-rest-auth/logout/'

Ideally, this app would be complemented by dedicated frontend to consume the API, such as React app or Android/iOS app, to ensure an attractive user interface for blog posts, mandatory email verification, etc.

The project is based on the book "Django for APIs v4.0" by William S. Vincent
https://djangoforapis.com/


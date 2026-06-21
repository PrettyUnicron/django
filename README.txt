This Project is made using this video as guide: https://www.youtube.com/watch?v=c-QsfbznSXI&t=1s
Backend Installation Guide(Windows):

1. Enter into a virtual environment
python -m venv env
.\env\Scripts\activate

2. Install Packages
Make a 'requirements.txt' which should contain:
asgiref
Django
django-cors-headers
djangorestframework
djangorestframework-simplejwt
PyJWT
pytz
sqlparse
psycopg2-binary
python-dotenv

Then to install the packages
pip install -r requirements.txt

3. Create a new Django Project
django-admin startproject <name>

4. Create your API
python manage.py startapp api

5. Edit settings.py
Add:
from datetime import timedelta
from dotenv import load_dotenv
import os #If you are using a modern version of Django you don't need to add this

load_dotenv()

Find "ALLOWED_HOSTS" and Edit to "ALLOWED_HOSTS = ["*"]"

Add:
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": (
        "rest_framework_simplejwt.authentication.JWTAuthentication",
    ),
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framwork.permissions.IsAuthenticated",
    ],
}

SIMPLE_JWT = {
    "ACCESS_TOKEN_LIFETIME": timedelta(minutes=30), #Acess token will expire in 30 mins
    "REFRESH_TOKEN_LIFETIME": timedelta(days=1), #Refresh token will expire in 1 day
}

Inside INSTALLED_APPS add:
api
rest_framework
corsheaders

Inside MIDDLEWARE add:
corsheaders.middleware.CorsMiddleware

Go to the very bottom of the file and add:
CORS_ALLOW_ALL_ORIGINS = True #Change this so that it only allows a specific origin
CORS_ALLOWS_CREDENTIALS = True

--------------------------------------------------------------------------------------------------

Whenever starting a new django projects or making significant changes that involve the data model, run migrations:
python manage.py makemigrations
python manage.py migrate

*Migrate whenever you connect to a new database


To run the server use "python manage.py runserver"


Translating from MERN Stack
urls.py works as the routers
views.py works as the controllers
models.py works as the models

serializers convert data to JSON and validate incoming data

------------------------------------------------------------------------------------------------------

Frontend Installation

npm create vite@latest frontend -- -- template react
if it gives you list of which template to use just select react
for the variant you can choose javascript

go to frontend folder
npm install axios react-router-dom jwt-decode

in "src" directory:

    remove .css files
    remove all imports and replace with 'import react from "react"' in App.jsx
    remove imports to .css files in main.jsx

    create folders:
    components
    pages
    styles

    create files:
    api.js
    constants.js

in frontend directory:
    create .env file

in constants.js write:
    export const ACCESS_TOKEN = "access";
    export const REFRESH_TOKEN = "refresh";
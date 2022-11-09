# Problem
Two Factor authentication is a vital requirement these days to enhance application security. It prevents the application against attackers or fraud.
We wish to implement 2da similar to google 2 fa experience so the problem is how to integrate 2fa in django applications similar to google 2fa?



# Environment
Django, Python , HTML, MySQL


# How you fix it
The django package built on top of django-otp named as django two factor auth is installed and proper annotations are included in settings file and the html files are configured according to requirement.
In order to integrate two factor authentication in django there are particular steps that we need to follow and are listed in this file.

# Solution
**Install required packages:**  
pip install django-two-factor-auth  
pip install phonenumbers  
  
**Modifications in Settings.py file:**  
Include apps in INSTALLED APPS section as follows:  
'django_otp',  
'django_otp.plugins.otp_static',  
'django_otp.plugins.otp_totp',  
'two_factor',  
  
Include following Middleware in Middlewares section:  
'django.contrib.auth.middleware.AuthenticationMiddleware',  
'django_otp.middleware.OTPMiddleware',  
  
Update login url and login redirect url:  
LOGIN_URL = 'two_factor:login'  
LOGIN_REDIRECT_URL = "/documents/"  

**Modifications in URL file:**  
path("", include(tf_urls)),  
  
**Make Migrations and Migrate:**  
Execute the following commands in terminal:  
python manage.py makemigrations  
python manage.py migrate  
  
**Download HTML file for two factor auth and link css:**  
Navigate to the link:https://github.com/jazzband/django-two-factor-auth  
Download templates for 2fa and include them in templates folder for django application and link you application css with those templates.  
Cheers we are done!  

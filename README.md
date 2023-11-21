![LandaSoft logo](ci_logo_small.png)

## How to Deploy the local development app

1. Install Django (version as stated in requirements.txt)
2. Migrate and create superuser account
3. Verify Django server works correctly
4. Copy all project files from repository
5. Update env.py with update keys and global information
6. Install all requirements
7. Migrate to create all needed tables 
8. load the example data
9. Change has_size in products table for sizable products and avoid exceptions
    ```
    $ python3 manage.py shell
    In [1]: from products.models import Product
    In [2]: kdbb = ['kitchen_dining', 'bed_bath']
    In [3]: clothes= Product.objects.exclude(category__name__in=kdbb)
    In [4]: clothes.count()
    Out[5]: 130
    In [6]: for item in clothes:
        ...:     if item.sku in ('pp5003270936','pp5003960062','PP5005850180','PP5005940299','PP5007250126'):
        ...:         item.has_sizes=False
        ...:     else:
        ...:         item.has_sizes=True
        ...:     item.save()
    In [7]: Product.objects.filter(has_sizes=True).count()
    Out[8]: 125
    In [9]: exit()
    ```
10. Run server

## How to generate a Django SECRET_KEY
```
# importing the function from utils
from django.core.management.utils import get_random_secret_key

# generating and printing the SECRET_KEY
print(get_random_secret_key())
```
## How to load the example data

The example data is located in /products/fixtures directory
```
$ python3 manage.py loaddata categorie
$ python3 manage.py loaddata products
```

## Codeanywhere Reminders

To run a frontend (HTML, CSS, Javascript only) application in Codeanywhere, in the terminal, type:

`python3 -m http.server`

A button should appear to click: _Open Preview_ or _Open Browser_.

To run a frontend (HTML, CSS, Javascript only) application in Codeanywhere with no-cache, you can use this alias for `python3 -m http.server`.

`http_server`

To run a backend Python file, type `python3 app.py`, if your Python file is named `app.py` of course.

A button should appear to click: _Open Preview_ or _Open Browser_.

In Codeanywhere you have superuser security privileges by default. Therefore you do not need to use the `sudo` (superuser do) command in the bash terminal in any of the lessons.

To log into the Heroku toolbelt CLI:

1. Log in to your Heroku account and go to _Account Settings_ in the menu under your avatar.
2. Scroll down to the _API Key_ and click _Reveal_
3. Copy the key
4. In Codeanywhere, from the terminal, run `heroku_config`
5. Paste in your API key when asked

You can now use the `heroku` CLI program - try running `heroku apps` to confirm it works. This API key is unique and private to you so do not share it. If you accidentally make it public then you can create a new one with _Regenerate API Key_.

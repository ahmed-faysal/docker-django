# docker-django-postgres

Creating boilerplate for setting up a Django environment with Postgresql as database.

### Versions used:
- Python: 3.7-slim
- Django: >=2.2, <2.3
- Postgres: 11-alpine

### Instructions:

In the root directory of the project run the following command
```sh
$ docker-compose build
```
This will create the Docker image named docker-django_web
> Usually the image name is defined as: ROOT-DIRECTORY-NAME_web

Then run the following command to create a Django project
```sh
$ docker-compose run web django-admin.py startproject PROJECT-NAME
```
Replace the PROJECT-NAME with your project name.
At this point the owner of this project is root. So, you would need sudo permission to edit anything in the project.
To overcome this, type the following in the terminal to change the ownership from root to current user.
```sh
$ sudo chown -R $USER:$USER ./src
```
>Run this command from root directory anytime the project asks sudo permission to edit/delete something.

Then use your preferred text editor to edit 'settings.py' in the project to set Postgresql as database.
Find the Databases section and replace the 'Databases = { }' part with the following
```sh
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'PASSWORD': 'abc123',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```
Save it. Get back to terminal and run the following command to run your project.
```sh
docker-compose up
```
Open browser and go to [localhost:8000](http://localhost:8000/).
If you see django landing page, you're all set. Congrats!

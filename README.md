## Description

This is a small Django App to help understand how Celery, Django, Flower and REDIS can be used to manage asynchronous tasks.

## How to Spin it Up

After cloning the repo do the following:

1. From the root of the project build the images by running the command `docker-compose build`
2. Spin up the containers using the command `docker-compose up -d`

If everything goes ok:

1. http://localhost:8010/ should show the Django welcome screen
2. http://localhost:5557/ should show the Flower dashboard

## Spawning a Task

1. Shell into the Django App using the following command `docker-compose exec web python manage.py shell`
2. Then enter the following `from django_celery_example.celery import divide`

To spawn a task enter the follwoing `divide.delay(1,2)`. Immediately in the same window there should be an Async ID displayed for the new task. Also, on the Flower dashboard the task should be reported.

If you want to see a failed task run the following command `divide.delay(1,0)`.

## Viewing the Logs

In a new terminal, enter the following command: `docker-compose logs celery_worker`

## See Tasks in REDIS

To enter the redis container, in a new terminal enter the following command: `docker-compose exec redis sh`

Then type the following: `redis-cli`
Query for a task using its ID (returned to the console when a task is spawned) using the following: `MGET celery-task-meta-<ID FROM SHELL ASYNC RESULT MESSAGE>`

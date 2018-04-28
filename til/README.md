<< [Home](../README.md)

# Today I Learned (TIL)

## 2018

- 04/26/18: What a pytest fixture is 
- 4/23/18: That you have to actual configure S3 to accept user uploads if you want to be able to access the things your users upload later on 
- 04/19/18: How to add rollbar-specific logging to a project 
- 03/25/18: We had dahlias in our front garden! 
- 03/23/18: So much about files in Python/Django. How to cleanly [output a CSV file from a Django view](https://www.endpoint.com/blog/2012/02/22/dowloading-csv-file-with-from-django), how to [zip multiple csv files into one HTTP response](https://stackoverflow.com/questions/25064347/sending-multiple-csv-files-to-zip-without-storing-to-disk-in-python?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa).
- 03/22/18: How to deploy to staging on Kubernetes. [Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
- 02/26/18: Kibana basics 
- 02/15/18: The first steps to debugging an LTI issue in Canvas 
- 02/14/18: How to make an [opsdroid](https://opsdroid.readthedocs.io/en/stable/) skill and connect it to Slack 
- 02/08/18: How to [merge from the command line](https://www.git-tower.com/learn/git/faq/git-merge-branch)
- 02/07/18: How to [add custom permissions to a DSF detail_route](https://stackoverflow.com/a/29356615) that differ from the permissions in the rest of the viewset
- 01/30/18: How to enable [logging in Django](https://lincolnloop.com/blog/django-logging-right-way/)
- 01/25/18: How to enable logging in Celery 
- 01/24/18: How to enable Celery on Docker in a Django project to schedule periodic tasks
- 01/18/18: How to [store a file](https://www.revsys.com/blog/2014/dec/03/loading-django-files-from-code/) in a Django model 
- 01/17/18: How to read a CSV file in Python ([StackOverflow](https://stackoverflow.com/questions/38170071/csv-to-json-convertion-with-python), [example](https://github.com/jefftriplett/trolley/blob/6e440d491bc11c576b6d1470b439df82f667c19a/trolley.py#L75), [more info on the csv module](https://pymotw.com/3/csv/))
- 01/17/18: How to rename my current Git branch (`git branch -m [new-name]`) 
- 01/15/18: About `request.data.getlist` for getting lists from forms or API requests. [More info](https://docs.djangoproject.com/en/2.0/ref/request-response/#django.http.QueryDict.getlist).
- 01/11/18: How to [output a CSV](https://docs.djangoproject.com/en/2.0/howto/outputting-csv/) in Django 
- 01/11/18: About the [`python-dateutil`](https://dateutil.readthedocs.io/en/stable/) library and how easy it makes converting dates received as strings from APIs into datetime objects and comparing them 
- 01/10/18: How to use the [`django-fsm`](https://github.com/kmmbvnr/django-fsm) library 
- 01/05/18: How to use D[jango aggregators](https://docs.djangoproject.com/en/2.0/topics/db/aggregation/#order-of-annotate-and-filter-clauses). (See client project for example code) 

## 2017 and prior 
### 4/25/17: Mailcatcher

[Mailcatcher](https://mailcatcher.me/) is a tool you can use, even on Django projects, to test sending email locally. Its docs are pretty straightforward. Once it's installed and you have configured your settings (see the docs), just run `mailcatcher` in your project and the SMTP server will start in the background. Then run your management commands, or server, and do what you need to do to send email. Navigate to http://127.0.0.1:1080 to see a UI with the mail being sent and received. Use the UI to stop the server. 

### 4/24/17: How to test a manage.py command 
For work I'm using a repo someone else wrote with a small example project to illustrate how to use Stonebranch, a whole other tool that has nothing to do with what I learned. But I had to learn how a custom management command is structured and how to test it! 

Your management commands should be in a directory inside your app called `management` and then inside another directory called `commands`. Your directory structure will look like this.  

```
mysite/ 
    manage.py
    mysite/
        settings.py
    myapp/
        management/
            commands/
                mycommand.py
                __init__.py
```

Your command will be a class that inherits from `BaseCommand`. The command I'm testing was just called `Command` and had the methods `__init__`, `main`, and `handle`. `__init__` is pretty obvious. `handle` seems to be included with most commands. `main` is what the developer who wrote this command called the method where the processing is done. 

This confused me because I kept trying to treat this command, and testing it, like it was a normal class. I kept not getting the result I wanted. Why won't this work? Finally I did what I should have done in the first place: Googled how to test Django management commands. 

```
$ python manage.py mycommand
```

Just change into the directory with your `manage.py` file, the same place you are when you run `runserver`, and then run `python manage.py [the name of your file]`. 

## 4/17/17: How class-based generic views work 
I'm finally getting a handle on how class-based generic views work in Django, and how to customize them. The website [Classy Class-Based Views](https://ccbv.co.uk/) is really helpful, but I had to figure out what it was telling me. 

CCBV (the website) shows you all the attributes and methods attached to a specific generic view. It's not an example of how you might customize your CBGV. It's a peek under the hood at exactly what's going on. This makes using your CBGV much easier. For example, say you're working from the [example in the docs](https://docs.djangoproject.com/en/1.11/ref/class-based-views/generic-display/) of a DetailView:

```
# views.py
from django.views.generic.detail import DetailView
from django.utils import timezone

from articles.models import Article

class ArticleDetailView(DetailView):

    model = Article

    def get_context_data(self, **kwargs):
        context = super(ArticleDetailView, self).get_context_data(**kwargs)
        context['now'] = timezone.now()
        return context
```

The template appears nowhere in this example, because Django just takes it for granted that you're going to call your template `article_detail.html`, following the convention that given a view `SomeDetailView`, the corresponding template will be `some_detail.html`. But what if it's not? What if you're a rebel and want to call it `some_specific.html` or something? 

CCBV taught me that `template_name` is an attribute on the `ListView` class, so I can just add the line `template_name = specific_article.html` and the CBGV takes care of the rest! 

### 4/6/16: [How to generate a requirements.txt file](http://www.idiotinside.com/2015/05/10/python-auto-generate-requirements-txt/)

### 3/9/16: The power of flowcharts! 
That flowcharting is an excellent way to begin the refactoring process. Combining two functions into one was made so much easier by starting with design.

# Stuff to document that now I know 

- How mixins work 
- How to write a custom migration 
- How to write a custom template tag 
- How to write a custom template filter 
- How to add a custom admin command 
- How to do a basic accessibility check on a website with Tota11y 
- How to build a DIY audio booth with pillows and a cat scratcher 
- How to write a Twitter bot
- How to use Pandoc to convert Markdown to Word and other file formats 
- What RAML and YAML files are 
- What tox does 
- How to use coverage.py 
- How to create branches in GitHub/a good GitHub workflow 
- How to pip install a specific version of a package from GitHub before a new release
- How to write a custom manage.py command
- How to use flake8 
- How to use cookiecutter 
- How to make a Slackbot
- How to handle yaml files and Jekyll

# Stuff I want to learn 

- How to add photos to a Twitter bot 
- How to add a CI tool to GitHub 
- How to add a confirmation email to a Google form 


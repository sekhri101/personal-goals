<< [Home](../README.md)

# Today I Learned (TIL)

## 2018

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

# Stuff I want to learn 

- How to make a Slackbot 
- How to add photos to a Twitter bot 
- How to add a CI tool to GitHub 
- How to add a confirmation email to a Google form 
- How to handle yaml files and Jekyll


<< Home](../README.md)

# Today I Learned (TIL)
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

# Archive 
- **4/6/16**: [How to generate a requirements.txt file](http://www.idiotinside.com/2015/05/10/python-auto-generate-requirements-txt/)
- **3/9/16**: That flowcharting is an excellent way to begin the refactoring process. Combining two functions into one was made so much easier by starting with design.

# Stuff I want to learn
There is a lot of stuff I don't know. Some of it is embarrassing to list. But the goal of this project is to make my personal goals public. Putting the embarrassing things I don't know, but would like to make time to learn, out in public will help keep me motivated and accountable!

- [x] Understand virtual environments
- [ ] Conversational Spanish
- [x] To rock climb
- [ ] How to use Heroku
- [x] How to use coverage.py
- [x] How to write an API in DRF
- [ ] How to write unit tests
- [ ] How to write functional tests

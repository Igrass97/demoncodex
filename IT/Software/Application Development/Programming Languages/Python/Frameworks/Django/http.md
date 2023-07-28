#finished 
# Handling HTTP requests

## URL dispatcher

### Request process

1. Checks the ROOT_URLCONF setting. (if the request has a urlconf attribute, it will use that config instead)

2. Django loads that Python module and looks for the variable urlpatterns. This should be a sequence of django.urls.path() and/or django.urls.re_path() instances.

3. Django runs through each URL pattern, in order, and stops at the first one that matches the requested URL, matching against path_info. (path info is only the path part of the URL)

4. Once one of the URL patterns matches, Django imports and calls the given view, which is a Python function (or a class-based view). The view gets passed the following arguments:

- HttpRequest.
- If the matched URL pattern contained no named groups, then the matches from the regular expression are provided as positional arguments.
- The keyword arguments are made up of any named parts matched by the path expression that are provided, overridden by any arguments specified in the optional kwargs argument to django.urls.path() or django.urls.re_path().

5. If no URL pattern matches, or if an exception is raised during any point in this process, Django invokes an appropriate error-handling view.

Example:

``` python
from django.urls import path

from . import views

urlpatterns = [
	path('articles/2003/', views.special_case_2003),
	path('articles/<int:year>/', views.year_archive),
	path('articles/<int:year>/<int:month>/', views.month_archive),
	path('articles/<int:year>/<int:month>/<slug:slug>/', views.article_detail),
]
```

### Cast Path Arguments to other Types

Notice that you can cast the path keyword arguments into another type (it's a string by default).

- str - Matches any non-empty string, excluding the path separator, '/'. This is the default if a converter isn’t included in the expression.
- int - Matches zero or any positive integer. Returns an int.
- slug - Matches any slug string consisting of ASCII letters or numbers, plus the hyphen and underscore characters. For example, building-your-1st-django-site.
- uuid - Matches a formatted UUID. To prevent multiple URLs from mapping to the same page, dashes must be included and letters must be lowercase. For example, 075194d3-6885-417e-a8a8-6c931e272f00. Returns a UUID instance.
- path - Matches any non-empty string, including the path separator, '/'. This allows you to match against a complete URL path rather than a segment of a URL path as with str.

Also, you can add custom converters [Docs](https://docs.djangoproject.com/en/4.1/topics/http/urls/#registering-custom-path-converters)

### Use Regular Expressions as URL Patterns

``` python
from django.urls import path, re_path

from . import views

urlpatterns = [
	path('articles/2003/', views.special_case_2003),
	re_path(r'^articles/(?P<year>[0-9]{4})/$', views.year_archive),
	re_path(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/$', views.month_archive),
	re_path(r'^articles/(?P<year>[0-9]{4})/(?P<month>[0-9]{2})/(?P<slug>[\w-]+)/$', views.article_detail),
]
```

### Default View Arguments

``` python
def page(request, num=1):
	# Output the appropriate page of blog entries, according to num.
	...
```

### Error Handling

The views to use for these cases are specified by four variables. Their default values should suffice for most projects, but further customization is possible by overriding their default values.

They're overriden in your URLConf file.

``` python
handler404 = 'mysite.views.my_custom_page_not_found_view'
handler500 = 'mysite.views.my_custom_error_view'
handler403 = 'mysite.views.my_custom_permission_denied_view'
handler400 = 'mysite.views.my_custom_bad_request_view'
```

## View Decorators

### Allowed HTTP Methods

``` python
from django.views.decorators.http import require_http_methods

@require_http_methods(["GET", "POST"])
def my_view(request):
	# I can assume now that only GET or POST requests make it this far
	# ...
	pass
```

### Other

[Docs](https://docs.djangoproject.com/en/4.1/topics/http/decorators/)

## File Uploads

When Django handles a file upload, the file data ends up placed in request.FILES

``` python
from django import forms

class UploadFileForm(forms.Form):
	title = forms.CharField(max_length=50)
	file = forms.FileField()
```

A view handling this form will receive the file data in request.FILES.

`Request.FILES` will only contain data if the request method was POST, at least one file field was actually posted, and the `<form>` that posted the request has the attribute `enctype="multipart/form-data"`

``` python
from django.http import HttpResponseRedirect
from django.shortcuts import render
from .forms import UploadFileForm

def upload_file(request):
	if request.method == 'POST':
		form = UploadFileForm(request.POST, request.FILES)
		if form.is_valid():
			handle_uploaded_file(request.FILES['file'])
			return HttpResponseRedirect('/success/url/')
	else:
		form = UploadFileForm()
	return render(request, 'upload.html', {'form': form})

def handle_uploaded_file(f):
	with open('some/file/name.txt', 'wb+') as destination:
		for chunk in f.chunks():
			destination.write(chunk)
```

### Using a ModelForm with a FileField

If you’re saving a file on a Model with a FileField, using a ModelForm makes this process much easier. The file object will be saved to the location specified by the upload_to argument of the corresponding FileField when calling form.save():

## Shortcuts

[Docs](https://docs.djangoproject.com/en/4.1/topics/http/shortcuts/)

## Middleware

It globally alters the behaviour of the http request/response process.

A middleware factory is a callable that takes a `get_response` callable and returns a middleware. A middleware is a callable that takes a request and returns a response, just like a view.

``` python
def simple_middleware(get_response):
    # One-time configuration and initialization.

    def middleware(request):
		# Code to be executed for each request before
		# the view (and later middleware) are called.
	
		response = get_response(request)
	
		# Code to be executed for each request/response after
		# the view is called.
	
		return response

    return middleware
```

or

``` python
class SimpleMiddleware:
	def __init__(self, get_response):
		self.get_response = get_response
		# One-time configuration and initialization.
	
	def __call__(self, request):
		# Code to be executed for each request before
		# the view (and later middleware) are called.
	
		response = self.get_response(request)
	
		# Code to be executed for each request/response after
		# the view is called.
	
		return response
```

To activate a middleware component, add it to the MIDDLEWARE list in your Django settings.

``` python
MIDDLEWARE = [
	'django.middleware.security.SecurityMiddleware',
	'django.contrib.sessions.middleware.SessionMiddleware',
	'django.middleware.common.CommonMiddleware',
	'django.middleware.csrf.CsrfViewMiddleware',
	'django.contrib.auth.middleware.AuthenticationMiddleware',
	'django.contrib.messages.middleware.MessageMiddleware',
	'django.middleware.clickjacking.XFrameOptionsMiddleware',
]
```

## Sessions

Sessions are implemented via a piece of middleware `django.contrib.sessions.middleware.SessionMiddleware`.

There are a couple of ways of using session data: `database-backend sessions`, `cached sessions`, `file-based sessions` and `cookie-based sessions`

### Using sessions in views

If you have the SessionMiddleware in place, the request argument will contain a `session` attribute.

``` python
def post_comment(request, new_comment):
	if request.session.get('has_commented', True):
		return HttpResponse("You've already commented.")
	c = comments.Comment(comment=new_comment)
	c.save()
	request.session['has_commented'] = True
	return HttpResponse('Thanks for your comment!')
```

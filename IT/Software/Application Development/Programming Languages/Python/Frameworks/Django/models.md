#finished 
# Models

## Defining models

Models inherits from `models.Model`.

Model's fields are fields in the database

Fields are defined using a `Field` class like `CharField` (imported from models) https://docs.djangoproject.com/en/4.1/ref/models/fields/#model-field-types

Models can have methods

``` python
from django.db import models

class Person(models.Model):
	first_name = models.CharField(max_length=30)
	last_name = models.CharField(max_length=30)

	def get_full_name(self):
		return self.first_name + self.last_name
```


## Create instance and save to DB

Simply instanciate the class and call `.save()`

``` python
from models import Person

p = Person(first_name='Ignacio', last_name='Grassini')
p.save()
```

## Relationships

### One to Many

`django.db.models.ForeignKey`

A one-to-many relationship is a relationship where each record in the first table can correspond to many records in the second table, but each record in the second table corresponds to only one record in the first table.

For example, if a Car model has a Manufacturer – that is, a Manufacturer makes multiple cars but each Car only has one Manufacturer – use the following definitions:

``` python
from django.db import models

class Manufacturer(models.Model):
	name = models.CharField(max_length=30)

class Car(models.Model):
	manufacturer = models.ForeignKey(Manufacturer)
	name = models.CharField(max_length=30)
```

#### Reverse relationships

``` python
from models import Manufacturer, Car

m = Manufacturer(name="Toyota")
m.save()

c1 = Car(name="Corolla", manufacturer_id=m.id)
c2 = Car(name="Yaris", manufacturer_id=m.id)
c1.save()
c2.save()

m.car_set.all()
m.car_set.filter()
m.car_set.count()
```

Also, the Manufacturer can call the following methods to add cars to the car_set:

Adds the specified model objects to the related object set

    add(obj1, obj2, ...)

Creates a new object, saves it and puts it in the related object set. Returns the newly created object.

    create(**kwargs)

Removes the specified model objects from the related object set.

    remove(obj1, obj2, ...)

Removes all objects from the related object set.

    clear()

Replace the set of related objects.

    set(objs)

### Many To Many

`django.db.models.ManyToManyField`

A many-to-many relationship is a relationship where each record in the first table can correspond to many records in the second table, and vice versa.

Each student can enroll in multiple courses, and each course can have multiple students enrolled.

``` python
class Student(models.Model):
	name = models.CharField(max_length=100)
	courses = models.ManyToManyField(Course, related_name='students')

class Course(models.Model):
	name = models.CharField(max_length=100)
```

#### Reverse relationships

Course -> Students

``` python
# get a course object
course = Course.objects.get(pk=1)

# access all students enrolled in the course
students = course.students.all()
```

Student -> Courses

``` python
# get a student object
student = Student.objects.get(pk=1)

# access all courses that the student is enrolled in
courses = student.courses.all()
```

#### Using an intermediary model

It's useful when you want to define extra fields in the relationship

``` python
from django.db import models

class Person(models.Model):
	name = models.CharField(max_length=128)

	def __str__(self):
		return self.name

class Group(models.Model):
	name = models.CharField(max_length=128)
	members = models.ManyToManyField(Person, through='Membership')

	def __str__(self):
		eturn self.name

class Membership(models.Model):
	person = models.ForeignKey(Person, on_delete=models.CASCADE)
	group = models.ForeignKey(Group, on_delete=models.CASCADE)
	date_joined = models.DateField()
	invite_reason = models.CharField(max_length=64)
```

### One-To-One

`django.db.models.OneToOne`

This is most useful on the primary key of an object when that object “extends” another object in some way.

``` python
class Person(models.Model):
	name = models.CharField(max_length=100)

class Profile(models.Model):
	person = models.OneToOneField(Person, on_delete=models.CASCADE, related_name='profile')
	bio = models.TextField()
```

#### Reverse relationships

Person -> Profile

``` python
# get a person object
person = Person.objects.get(pk=1)

# access the associated profile object
profile = person.profile

# print the bio of the person's profile
print(profile.bio)
```

Profile -> Person

``` python
# get a profile object
profile = Profile.objects.get(pk=1)

# access the associated person object
person = profile.person

# print the name of the person
print(person.name)
```

## Meta options

Is anything that is not a field.

[All meta options](https://docs.djangoproject.com/en/4.1/ref/models/options/)

``` python
from django.db import models

class Ox(models.Model):
	horn_length = models.IntegerField()

	class Meta:
		ordering = ["horn_length"]
		verbose_name_plural = "oxen"
		db_table = "oxen"
```

## Manager

Is the interface through which database query operations are provided to Django models. Mainly used to retrieve the instances from the database. The default manager is `Model.objects`

``` python
from myapp.models import MyModel

# Retrieve all objects of MyModel
all_objects = MyModel.objects.all()

# Retrieve a specific object of MyModel based on its primary key (id)
object_with_id_1 = MyModel.objects.get(id=1)

# Retrieve objects of MyModel based on some other criteria
objects_with_field_value = MyModel.objects.filter(field_name=value)

# Create a new object of MyModel
new_object = MyModel(field_name_1=value_1, field_name_2=value_2)

# Save the new object to the database
new_object.save()

# Create and save a new object of MyModel using the create() method
new_object = MyModel.objects.create(field_name_1=value_1, field_name_2=value_2)
```

## Model Instance Methods

Model methods act in a particular instance.

``` python
from django.db import models

class Person(models.Model):
	first_name = models.CharField(max_length=30)
	last_name = models.CharField(max_length=30)
	age = models.IntegerField(min=0)

	def can_drink(self):
		return self.age >= 18

	@property
	def full_name(self):
		return '%s %s' % (self.first_name, self.last_name)
```

[All model instance methods](https://docs.djangoproject.com/en/4.1/ref/models/instances/#model-instance-methods)

### Probably always need to define these methods

`__str__()` returns a string representation of any object.
`get_absolute_url()` tells Django how to calculate the URL for an object.

### Override Instance Methods

Often, you'll want to change the way an object is saved or deleted, you can override this behaviour.

``` python
from django.db import models

class Person(models.Model):
	...fields

	def save(self, *args, **kwargs):
		something()
		super().save(*args, **kwargs) # Call the models.Model.save() method
```

## Model Class Methods

``` python
from django.db import models
from datetime import date

class Person(models.Model):
	name = models.CharField(max_length=100)
	birthdate = models.DateField()

@classmethod
def get_average_age(cls):
	today = date.today()
	total_age = 0
	num_people = cls.objects.count()
	for person in cls.objects.all():
		total_age += # calculate age in current person
	return total_age / num_people if num_people else 0
```

Instead of adding the method as a static method of the class, creating a new Manager is preferred.

``` python
from django.db import models

class PersonManager(models.Manager):
		def get_average_age(self):
			today = date.today()
			total_age = 0
			num_people = self.count()
			for person in self.all():
				total_age += # calculate age in current person
			return total_age / num_people if num_people else 0
```

## Model Inheritance

### 1. Hold common information (Abstract Class)

This model will then not be used to create any database table. Instead, when it is used as a base class for other models, its fields will be added to those of the child class.

``` python
from django.db import models

class CommonInfo(models.Model):
	name = models.CharField(max_length=100)
	age = models.PositiveIntegerField()

	class Meta:
		abstract = True
		this_field_will_be_inherited_as_well = True

class Student(CommonInfo):
	home_group = models.CharField(max_length=5)

class Teacher(CommonInfo):
	area = models.CharField(max_length=30)
```

If you inherit from multiple abstract models, Python will only inherit the `Meta` of the first class passed. So if you want to inherit `Meta` from multiple classes, you'll have to set it explicitly.

``` python
from django.db import models

class Person(models.Model):
	Meta(Model1.Meta, Model2.Meta):
		...
```

### 2. Multi-table inheritance

Each model corresponds to its own database table and can be queried and created individually.

The inheritance relationship introduces links between the child model and each of its parents (via an automatically-created OneToOneField).

``` python
from django.db import models

class Place(models.Model):
	name = models.CharField(max_length=50)
	address = models.CharField(max_length=80)

class Restaurant(Place):
	serves_hot_dogs = models.BooleanField(default=False)
	serves_pizza = models.BooleanField(default=False)

Place.objects.filter(name="Bob's Cafe")
Restaurant.objects.filter(name="Bob's Cafe")
```

### 3. Proxy models

They can change the behaviour of the parent model without creating a new table.

``` python
from django.db import models

class Person(models.Model):
	first_name = models.CharField(max_length=30)
	last_name = models.CharField(max_length=30)

class MyPerson(Person):
	class Meta:
		ordering = ["last_name"]
		proxy = True

def do_something(self):
	# ...
	pass
```

# Queries

## Creating

`model_instance.save()` or `MyModel.objects.create(...values)`

## Updating

`model_instance.field1 = 'new_value'` and `model_instance.save()`

### Update ForeignKey

`model_instance1.foreign_field = model_instance2`

### Update ManyToManyField

`model_instance1.many_to_many_field.add(model_instance2)`

### Update multiple rows

`Entry.objects.filter(pub_date__year=2007).update(headline='Everything is the same')`

### Update multiple rows with foreign keys

    b = Blog.objects.get(pk=1)
    Entry.objects.update(blog=b)

### Update fields based on other value of the same row

`Entry.objects.update(number_of_pingbacks=F('number_of_pingbacks') + 1)`

## Query Sets (retrieving)

### All

`all_records = MyModel.objects.all()`

### Filters

`filtered_records = MyModel.filter(lookup_field=lookup_value)`

`non_excluded_records = MyModel.exclude(exclude_field=exclude_value)`

### Single object

`single_record = MyModel.objects.get(pk=1)`

[All QuerySet methods](https://docs.djangoproject.com/en/4.1/ref/models/querysets/#queryset-api)

### Limiting QuerySets

`limited_records = MyModel.objects.all()[:5]`

Translates into `LIMIT 5` so it's still performant! (you're not really retrieving `all()` objects)

### Field lookups

They're specified as keyword arguments to the QuerySet methods `filter(), exclude() and get()`

`field__lookuptype=value`

`people_that_can_drink` = Person.objects.filter(age\_\_gte=18)`

[All Field Lookup Types](https://docs.djangoproject.com/en/4.1/ref/models/querysets/#field-lookups)

### JOINs

``` python
from django.db import models
class Blog(models.Model):
	name = models.CharField(max_length=30)

class Entry(models.Model):
	blog = models.ForeignKey(Blog)

Entry.objects.filter(blog__name='Beatles Blog')

Blog.objects.filter(entry__headline__contains='Lennon')
```

### Compare with another field of the same model when filtering

Using F, we can compare different fields of the same row when filtering.

``` python
from django.db.models import F

Entry.objects.filter(number_of_comments__gt=F('number_of_pingbacks'))
Entry.objects.filter(number_of_comments__gt=F('number_of_pingbacks') * 2)
Entry.objects.filter(rating__lt=F('number_of_comments') + F('number_of_pingbacks'))
```

We can also compare a value with a nested model value, F will perform the necessary JOINs.

    Entry.objects.filter(author__name=F('blog__name'))

### The PK Shortcut

``` python
Blog.objects.get(id__exact=14) # Explicit form
Blog.objects.get(id=14) # __exact is implied
Blog.objects.get(pk=14) # pk implies id__exact

Blog.objects.filter(pk__in=[1,4,7])
Blog.objects.filter(pk__gt=14)

Entry.objects.filter(blog__id__exact=3) # Explicit form
Entry.objects.filter(blog__id=3)        # __exact is implied
Entry.objects.filter(blog__pk=3)        # __pk implies __id__exact
```

### Complex lookups with Q objects

Keyword argument queries – in filter(), etc. – are “AND”ed together. If you need to execute more complex queries (for example, queries with OR statements), you can use Q objects.

Q objects can be combined using the &, |, and ^ operators. When an operator is used on two Q objects, it yields a new Q object.

`Q(question__startswith='Who') | Q(question__startswith='What')`

Q objects can also be negated `Q(question__startswith='Who') | ~Q(pub_date__year=2005)`

``` python
Poll.objects.get(
	Q(question__startswith='Who'),
	Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6))
)
```

## Deleting

Call `delete()` on the model instance.

    model_instance.delete()

Query Sets also have a `delete()` method.

    Entry.objects.filter(pub_date__year=2005).delete()

# Aggregation

Sometimes you will need to retrieve values that are derived by summarizing or aggregating a collection of objects.

``` python
 from django.db import models

    class Author(models.Model):
        name = models.CharField(max_length=100)
        age = models.IntegerField()

    class Publisher(models.Model):
        name = models.CharField(max_length=300)

    class Book(models.Model):
        name = models.CharField(max_length=300)
        pages = models.IntegerField()
        price = models.DecimalField(max_digits=10, decimal_places=2)
        rating = models.FloatField()
        authors = models.ManyToManyField(Author)
        publisher = models.ForeignKey(Publisher, on_delete=models.CASCADE)
        pubdate = models.DateField()

    class Store(models.Model):
        name = models.CharField(max_length=300)
        books = models.ManyToManyField(Book)
```
   
## Over a QuerySet

QuerySets have an `aggregate()` method.

``` python
from django.db.models import Avg

Book.objects.all().aggregate(Avg('price'))
```

[All Aggregation Functions](https://docs.djangoproject.com/en/4.1/ref/models/querysets/#aggregation-functions)

## Aggregation for EACH value of a QuerySet

Per-object summaries can be generated using the `annotate()` clause.

``` python
from django.db.models import Count

q = Book.objects.annotate(Count('authors'))
q[0].authors__count
```

Specify the aggregate field name:

``` python
from django.db.models import Count

q = Book.objects.annotate(num_authors=Count('authors'))
q[0].num_authors
```

## JOINs and Aggregates

Sometimes the value you want to aggregate will belong to a model that is related to the model you are querying.

``` python
from django.db.models import Max, Min

Store.objects.annotate(min_price=Min('books__price'), max_price=Max('books__price'))
Store.objects.aggregate(youngest_age=Min('books__authors__age'))
```

### Following the relation backwards

``` python
from django.db.models import Avg, Count, Min, Sum

Publisher.objects.annotate(Count('book'))
Publisher.objects.aggregate(oldest_pubdate=Min('book__pubdate'))
Author.objects.annotate(total_pages=Sum('book__pages'))
Author.objects.aggregate(average_rating=Avg('book__rating'))
```

### Filters and Aggregations

``` python
from django.db.models import Avg, Count

    Book.objects.filter(name__startswith="Django").annotate(num_authors=Count('authors'))
Book.objects.filter(name__startswith="Django").aggregate(Avg('price'))

Book.objects.annotate(num_authors=Count('authors')).filter(num_authors__gt=1)
```

If you need two annotations with two separate filters you can use the filter argument with any aggregate. For example, to generate a list of authors with a count of highly rated books:

``` python
highly_rated = Count('book', filter=Q(book__rating__gte=7))
Author.objects.annotate(num_books=Count('book'), highly_rated_books=highly_rated)
```

### Order By Annotation

`Book.objects.annotate(num_authors=Count('authors')).order_by('num_authors')`

### Grouping by values

Get the average price for products on the same category

``` python
from django.db.models import Avg

products = Product.objects.values('category').annotate(avg_price=Avg('price'))
```

# Search

## Standard contains

`Author.objects.filter(name__contains='Terry')`

`Author.objects.filter(name__icontains='terry')`

## Unnacented comparison

``` python
Author.objects.filter(name__unaccent__icontains='Helen')
User.objects.filter(first_name__unaccent__startswith="Jerem")
```

## Trigram similarity

In general, trigram_similar is more useful for finding strings that are similar in terms of their overall character content, while trigram_word_similar is more useful for finding strings that are similar in terms of their word content.

``` python
City.objects.filter(name__trigram_similar="Middlesborough")
Sentence.objects.filter(name__trigram_word_similar='Middlesborough')
```

## Interesting data about searching

[Docs](https://docs.djangoproject.com/en/4.1/topics/db/search/#document-based-search)

## PostgreSQL Search Extension

``` python
from models import Entry

Entry.objects.filter(body_text__search='cheese')

Entry.objects.annotate(
	search=SearchVector('blog__tagline', 'body_text'),
).filter(search='cheese')
```

# Managers

A Manager is the interface through which database query operations are provided to Django models. At least one Manager exists for every model in a Django application.

The default name for the manager is `objects` but you can override it

``` python
from django.db import models

class Person(models.Model):
	people = models.Manager()
```

## Custom Managers

The preferred way to add "table-level" methods to a Model, is to use custom managers.

There are two reasons you might want to customize a Manager: to add extra Manager methods, and/or to modify the initial QuerySet the Manager returns.

### Adding methods

``` python
from django.db import models

class Author(models.Model):
	name = models.CharField(max_length=255)

def __str__(self):
	return self.name

class BookCountManager(models.Manager):
	def with_num_of_books(self):
		return self.annotate(num_of_books=models.Count('book'))

objects = BookCountManager()

class Book(models.Model):
	title = models.CharField(max_length=255)
	author = models.ForeignKey(Author, on_delete=models.CASCADE)

def __str__(self):
	return self.title
```

### Changing the initial queryset

``` python
class DahlBookManager(models.Manager):
	def get_queryset(self):
		return super().get_queryset().filter(author='Roald Dahl')

class Book(models.Model):
	title = models.CharField(max_length=100)
	author = models.CharField(max_length=50)

	objects = models.Manager() # The default manager.
	dahl_objects = DahlBookManager() # The Dahl-specific manager.
```

#### Defining custom QuerySet methods and using them on the Manager

``` python
class PersonQuerySet(models.QuerySet):
	def authors(self):
		return self.filter(role='A')

	def editors(self):
		return self.filter(role='E')

class PersonManager(models.Manager):
	def get_queryset(self):
		return PersonQuerySet(self.model, using=self._db)

	def authors(self):
		return self.get_queryset().authors()

	def editors(self):
		return self.get_queryset().editors()

class Person(models.Model):
	first_name = models.CharField(max_length=50)
	last_name = models.CharField(max_length=50)
	role = models.CharField(max_length=1, choices=[('A', _('Author')), ('E', _('Editor'))])
	people = PersonManager()
```

The short version

``` python
class PersonQuerySet(models.QuerySet):
	def authors(self):
		return self.filter(role='A')

	def editors(self):
		return self.filter(role='E')

class Person(models.Model):
	people = PersonQuerySet.as_manager()
```

For advanced usage you might want both a custom Manager and a custom QuerySet.

``` python
class CustomManager(models.Manager):
	def manager_only_method(self):
		return

class CustomQuerySet(models.QuerySet):
	def manager_and_queryset_method(self):
		return

class MyModel(models.Model):
	objects = CustomManager.from_queryset(CustomQuerySet)()
```

# Raw SQL

[Docs](https://docs.djangoproject.com/en/4.1/topics/db/sql/)

# Database Transactions

Django uses transactions or savepoints automatically to guarantee the integrity of ORM operations that require multiple queries, especially delete() and update() queries.

A common way to handle transactions on the web is to wrap each request in a transaction. Set ATOMIC_REQUESTS to True in the configuration of each database for which you want to enable this behavior.

It works like this. Before calling a view function, Django starts a transaction. If the response is produced without problems, Django commits the transaction. If the view produces an exception, Django rolls back the transaction.

In practice, this feature wraps every view function in the atomic() decorator.

## Prevent Atomic Requests (when ATOMIC_REQUESTS=True)

``` python
@transaction.non_atomic_requests
def my_view(request):
	do_stuff()
```

## Explicit

``` python
from django.db import transaction

@transaction.atomic
def viewfunc(request):
	# This code executes inside a transaction.
	do_stuff()
```

## Using a Context Manager

``` python
from django.db import transaction

def viewfunc(request):
	# This code executes in autocommit mode (Django's default).
	do_stuff()

with transaction.atomic():
	# This code executes inside a transaction.
	do_more_stuff()
```

# Tablespaces

A common paradigm for optimizing performance in database systems is the use of tablespaces to organize disk layout.

``` python
class TablespaceExample(models.Model):
	name = models.CharField(max_length=30, db_index=True, db_tablespace="indexes")
	data = models.CharField(max_length=255, db_index=True)
	shortcut = models.CharField(max_length=7)
	edges = models.ManyToManyField(to="self", db_tablespace="indexes")

	class Meta:
		db_tablespace = "tables"
		indexes = [models.Index(fields=['shortcut'], db_tablespace='other_indexes')]
```

# Database access optimization

## Indexes

A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space to maintain the index data structure.

Use Meta.indexes or Field.db_index to add these from Django. Consider adding indexes to fields that you frequently query using filter(), exclude(), order_by(), etc.

## QuerySet evaluation

### QuerySets are Lazy

The act of creating a QuerySet doesn’t involve any database activity. The query will be only executed when you "ask" for the results.

``` python
q = Entry.objects.filter(headline__startswith="What")
q = q.filter(pub_date__lte=datetime.date.today())
q = q.exclude(body_text__icontains="food")
print(q)
```

This only hits the DB when you print q.

### When QuerySets are evaluated

You can evaluate a QuerySet in the following ways:

1. Iteration
2. Async iteration
3. Slicing
4. Pickling/Caching
5. repr()
6. len()
7. list()
8. bool()

### Caching

Each QuerySet contains a cache to minimize database access.

#### Reuse

``` python
queryset = Entry.objects.all()
print([p.headline for p in queryset]) # Evaluate the query set.
print([p.pub_date for p in queryset]) # Reuse the cache from the evaluation.
```
#### Will not cache (due to the slice)

``` python
queryset = Entry.objects.all()
print(queryset[5]) # Queries the database
print(queryset[5]) # Queries the database again
```

#### The entire queryset is already evaluated, cache will be checked
``` python
queryset = Entry.objects.all()
[entry for entry in queryset] # Queries the database
print(queryset[5]) # Uses cache
print(queryset[5]) # Uses cache
```

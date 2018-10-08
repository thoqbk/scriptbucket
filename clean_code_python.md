## Clean Code Python

- ![Clean Code](https://images.gr-assets.com/books/1436202607l/3735293.jpg)

- [Clean Code PHP](https://github.com/jupeter/clean-code-php)

- [If-statements design: guard clauses may be all you need](https://medium.com/@scadge/if-statements-design-guard-clauses-might-be-all-you-need-67219a1a981a)

### 1. Use the same vocabulary for the same type of variable:
---

**Example 1.** Bad:
```python
get_user_info()
get_user_data()
get_user_profile()
```

Good:
```python
get_user()
```

**Example 2.** Bad:
```python
class ClaimPrepayment(models.Model):
    staff = models.ForeignKey(Staff)
    # ...

class Report(models.Model):
    employee = models.ForeignKey(Staff)
    # ...
```

**Example 3.** Bad:
```python
user_info = User.objects.get(id=pk)
```

Good:
```python
user = User.objects.get(id=pk)
```

**Example 4.** Naming a list, set or even a dictionary. Bad:
```python
user_list = User.objects.filter(status=User.STATUS_ACTIVE)
users_list = User.objects.filter(status=User.STATUS_ACTIVE)
users_lst = User.objects.filter(status=User.STATUS_ACTIVE)
user = User.objects.filter(status=User.STATUS_ACTIVE)
```

Good:
```python
users = User.objects.filter(status=User.STATUS_ACTIVE)
```
### 2. Using guard clauses:
---

**Example 1.** Bad:
```python
if something.is_True():
    # pretty
    # long 
    # logic
    # of
    # running
    # something
```

Good:
```python
if not something.is_True():
    return
# pretty
# long 
# logic
# of
# running
# something
```

**Example 2.** Avoid nesting too deeply:
```python
def is_shop_open(day):
    if day:
        if is_string(day):
            if day == 'friday':
                return True
            elif day == 'saturday':
                return True
            elif day == 'sunday':
                return True
            else:
                return False
        else:
            return False
    else:
        return False
```

Good:
```python
def is_shop_open(day):
    if day is None or len(day) == 0:
        return False
    opening_days = ['friday', 'saturday', 'sunday'];
    return day.lower() in opening_days
}
```

**Example 3.** `get_po_detail@logics.py@Purchase System`

### 3. Don't add unneeded context:
---

**Example 1.** Bad:
```python
class Car(object):
    def __init__(self, car_make, car_model, car_color):
        self.car_make = car_make
        self.car_model = car_model
        self.car_color = car_color
```

Good:
```python
class Car(object):
    def __init__(self, make, model, color):
        self.make = make
        self.model = model
        self.color = color
```

**Example 2.** Purchase System. Bad:
```python
class ProjectType(models.Model):
    type_name = models.CharField(max_length=200)
    # ...

```

Good:
```python
class ProjectType(models.Model):
    name = models.CharField(max_length=200)
    # ...
```

### 4. Don’t repeat yourself (DRY):
---

Do your absolute best to avoid duplicate code. Duplicate code is bad because it means that there's more than one place to alter something if you need to change some logic.

```
import csv as __csv__
```


```
__id_to_data__ = None
__name_to_id__ = None
__years__ = None
```


```
def init(path):
    """init(path) must be called to load data before other calls will work.  You should call it like this: init("car_sales_data.csv") or init("lab.csv")"""

    global __id_to_data__
    global __name_to_id__
    global __years__

    if path != 'car_sales_data.csv':
        print("WARNING!  Opening a path other than car_sales_data.csv.  " +
              "That's fine for testing your code yourself, but car_sales_data.csv " +
              "will be the only file around when we test your code " +
              "for grading.")

    __id_to_data__ = {}
    __name_to_id__ = {}
    __years__ = []

    f = open(path, encoding='utf-8')
    raw_data = list(__csv__.reader(f))
    f.close()

    id_i = raw_data[0].index('id')
    vehicle_i = raw_data[0].index('vehicle')
    for head in raw_data[0]:
        if head not in ('id', 'vehicle'):
            __years__.append(int(head))
    for car in raw_data[1:]:
        __name_to_id__[car[vehicle_i]] = car[id_i]
        __id_to_data__[car[id_i]] = {}
        for i in range(len(car)):
            if i == id_i:
                continue
            elif i == vehicle_i:
                __id_to_data__[car[id_i]][raw_data[0][i]] = car[i]
            else:
                __id_to_data__[car[id_i]][raw_data[0][i]] = int(car[i])
```


```
def dump():
    """prints all the data to the screen"""
    if __id_to_data__ == None:
        raise Exception("you did not call init first")

    for car in sorted(__name_to_id__.keys()):
        car_id = __name_to_id__[car]
        print("%s [ID: %s]" % (car, car_id))
        for year in __years__:
            print("  %s: %d cars sold" % (year, __id_to_data__[car_id][str(year)]))
        print()
```


```
def get_id(car):
    """get_id(car) returns the id of the specified car model."""
    if __name_to_id__ == None:
        raise Exception("you did not call init first")
    if not car in __name_to_id__:
        raise Exception("No car '%s', only these: %s" %
                        (str(car), ', '.join(list(__name_to_id__.keys()))))
    return int(__name_to_id__[car])
```


```
def get_sales(car_id, year=2019):
    """get_sales(car_id, year) returns the number of cars of the specified model sold in the specified year."""
    if __id_to_data__ == None:
        raise Exception("you did not call init first")
    if str(car_id) not in list(__id_to_data__.keys()):
        raise Exception("%s is not an id of any car in the dataset. Did you call get_id?" % (str(car_id)))
    if not str(car_id) in __id_to_data__ or str(year) not in __id_to_data__[str(car_id)]:
        raise Exception("No data for car %s, in year %s" %
                        (str(car_id), str(year)))
    return __id_to_data__[str(car_id)][str(year)]
```


```

```

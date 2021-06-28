ArrayList resides within Java Core Libraries, so you don't need any additional libraries.
In order to use it just add the following import statement:

```import java.util.ArrayList```

List represents an ordered sequence of values where some value may occur more than one time.
Just maintain insert order. The values in array maybe not ordered.


ArrayList is one of the List implementations built atop an array, which is able to dynamically grow and shrinks 
as you add/remove elements. Elements could be easily accessed by their indexes starting from zero. This implementation
has the following properties:
* Random access takes O(1) time
* Adding element takes amortized constant time O(1)
* Inserting/Deleting takes O(n) time
* Searching takes O(n) time for unsorted array and O(logn) for a sorted one

#### create an  ArrayList
* default no-arg constructor
```aidl
List<String> list = new ArrayList<>();
list.isEmpty();
```
* constructor accepting initial capacity
```
List<String> list = new ArrayList<>(20);
```
* Constructor accepting collection
```aidl
Collection<Integer> number = IntStream.range(0, 10).boxed().collect(toSet());

List<Integer> list = new ArrayList<>(number)
```

#### add elements to the ArrayList
```aidl
list<Long> list = new ArrayList<>();

list.add(1L);
list.add(2L);
list.add(3L);
list.addAll(list); // 添加多个元素
```

#### iterate over the ArrayList
There are two types of iterators available: Iterator and ListIterator.
While the former gives you an opportunity to traverse the list in one direction, the latter allows you
to traverse it in both directions.

```aidl
for (int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}
```

```aidl
for (String value : list) {
    System.out.println(value);
}
```

[Iterator](https://www.baeldung.com/java-iterate-list)
```
// iterator
List<String> countries = new ArrayList<>();

Iterator<String> countriesIterator = countries.iterator();
while(countriesIterator.hasNext()) {
    System.out.println(countriesIterator.next());
}
```

```aidl
// ListInterator
ListIterator<String> listIterator = countries.listIterator(countries.size());

while(listIterator.hasPrevious()) {
    System.out.println(listIterator.previous());
}
```

```aidl
countries.forEach(System.out::println);
```

#### search 
searching an unsorted list
```
countries.indexOf("a");
countries.lastIndexOf("a");
```

if you want to find all elements satisfying a predicate, you may filter collection using Java8 Stream API
using Predicate like this:
```aidl
Set<String> matchingStrings = new HashSet<>(Arrays.asList("a", "c", "9"));

List<String> result = countries.stream().filter(matchingStrings::contains).collect(toCollection(ArrayList::new));
```

It is also possible to use a for loop or an interator:
```aidl
Iterator<String> it = stringsToSearch.iterator();
Set<String> matchingStrings = new HashSet<>(Array.asList("a", "c", "9"));

List<String> result = new ArrayList<>();
while (it.hasNext()) {
    String s = it.next();
    if (matchingStrings.contains(s)) {
        result.add(s);
    }
}
```

searching a sorted list
If you have a sorted array, then you may use a binary search algorithm which works faster than linear search
```aidl
List<String> copy = new ArrayList<>(StringsToSearch);
Collections.sort(copy);
int index = Collection.binarySearch(copy, "f");
assertThat(index, not(equalTo(-1)));
```
Notice that if an element is not found then -1 will be returned

#### remove elements from the ArrayList
In order to remove an element, you should find its index and only then perform the removal via remove() method.
An overloaded version of this method, that accepts an object, searches for it and performs removal of the first 
occurrence of an equal element
```aidl
list.remove(0)
list.remove(Integer.valudOf(0));
```
But be careful when working with boxed types such as Integer. In order to remove a particular element, you should
first box in value or otherwise, an element will be removed by its index.

remove by Iterator
```aidl
Iterator<String> it = list.iterator();
while (it.hasNext()) {
    if (anotherList.contains(it.next())) {
        it.remove();
    }
}
```
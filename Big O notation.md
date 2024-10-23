## What is Big O

- definition on Wikipedia: Big O Notation is a mathematical notation that describes the limiting behavior of a function, when the argument tends towards a particular value or infinity.

- Big O Notation, O(n)  
  to describe the **performance** of an algorithm  
  determine if a given algorithm is **scalable**  
  algorithm scale well as the input grows really large.  
  (code executes quickly on a computer doesn't mean perform with a large data set)

- certain operations can be more or less costly depending on what data structure we use.

For example:  
accessing an array element by its index is super fast.  
But arrays have a fixed length 🡪 if you want to constantly add or remove items from them🡪 get resized  
costly if size of input very large  
Better:  
use another data structure, linked list🡪 can grow or shrink very quickly.  
but accessing a linked list element by its index is slow.

---

## O(1) - constant time

```
public void Log(int[] numbers){
    Console.WriteLine(numbers[0]);
}
```

This method takes an array of integers and prints the first item on the console 🡪 no matter how big the array is 🡪 this method has a single operation and takes to run a **constant time** 🡪 represented as **O(1)** (read: big o of 1)  
**runtime complexity** of this method is O(1) 🡪 size of input doesn't matter.

We duplicate the line of code:

```
public void Log(int[] numbers){
    Console.WriteLine(numbers[0]);
    Console.WriteLine(numbers[0]);
}
```

we have 2 operations, both run in constant time 🡪 runtime complexity of this method is **O(2)**

for the runtime complexity:
no care about number of operations  
we care how much an algorithm slows down as the input grows.

no matter number of items: runs in **constant time** 🡪 we simply indicate with O(1).

---

## O(n) -- linear time

```
public void Log(int[] numbers){
    for (int i = 0; i < numbers.Length; i++){
        Console.WriteLine(numbers[i]);
    }
}
```

we iterate over all items in array, and print each item 🡪 size of input matters:  
with 1 item, we have 1 print operation; with million items, we have a million print operations 🡪 the cost of this algorithm grows linearly with the size of input

runtime complexity of this method = O(n)  
where n is the size of the input

We add a print statement before and after the loop.

```
public void Log(int[] numbers){
    Console.WriteLine();
    for (int i = 0; i < numbers.Length; i++){
        Console.WriteLine(numbers[i]);
    }
    Console.WriteLine();
}
```

single operation runs in constant time🡪 O(1)  
loop runs in O(n)  
single operation runs in O(1)  
run time complexity of method is O(1+n+1)🡪 O(2+n) 🡪 O(n)  
if array has one million inputs, adding 2 extra operations no significant inpact on the cost of algorithm 🡪 still increases linearly🡪constants no matter🡪 we drop it

We add another loop:

```
public void Log(int[] numbers){
    for (int i = 0; i < numbers.Length; i++){
        Console.WriteLine(numbers[i]);
    }
    for (int i = 0; i < numbers.Length; i++){
        Console.WriteLine(numbers[i]);
    }
}
```

runtime complexity: O(n+n) 🡪 O(2n) 🡪 O(n)  
n or 2n still represents a linear growth 🡪 drop the constant

we iterate over array of numbers and over the array of names.

```
public void Log(int[] numbers, String[]names){
    foreach (var number in numbers){      //O(n)
        Console.WriteLine(number);
    }
    foreach (var name in names){          //O(m)
        Console.WriteLine(name);
    }
}
```

both loops run in O(n)  
run time complexity: O(n+m)🡪 O(n) (matter that it’s linear)

---

## O(n^2) - quadratic time

Nested loops:  
in outer loop we iterate over 1st array 🡪 O(n)  
in each iteration we iterate over 2nd array🡪 O(n)  
runtime complexity: O ( n \* n) or O(n^2) 🡨🡪 algorithm runs in **quadratic time**

```
public static void Log(int[] numbers, String[]names){
    foreach (var number in numbers){
        foreach (var name in names){                              O(n^2)
            Console.WriteLine(number+"," + name);
        }
    }
}
```

We add another loop: runtime complexity: O(n+n^2) 🡪 we drop n🡪 O(n^2)

```
public static void Log(int[] numbers){
    foreach (var number in numbers){
            Console.WriteLine(number);
    }
    foreach (var number in numbers){
        foreach (var name in names){
            Console.WriteLine(number+"," + name);
        }
    }

}
```

If the array has few items no difference  
if input grows: algorithm that run in O(n^2) became slower than algorithm that run in O(n).

3 nested loop🡪 runtime complexity: O(n^3)

```
public static void Log(int[] numbers){
    foreach (var first in numbers){
        foreach (var second in numbers){
            foreach (var third in numbers){
                    Console.WriteLine(first + "," + second + "," + third);
            }
        }
    }
}
```

---

## ![](/images/curves.png)

## O(log n) - Logarithm Time

logarithmic curve compared with linear:  
linear curve grows at the same rate, but logarithmic curve slows down at some point  
**an Algorithm that runs in logarithmic time is more efficient and more scalable that an algorithm that runs in linear or quadratic time.**

Example: we have an array of sorted numbers  
![](/images/array10.png)
we have to find the number 10

One way:  
iterate using a for loop, until we find a 10  
**linear search**  
worst case scenario:  
number is at the end of the array  
more items 🡪 longer operation 🡪 run time of algorithm increases linearly and in direct proportion with size of our array.

**binary search**  
another searching algorithm🡪 runs in logarithmic time  
much faster then the linear search.  
Assuming array is sorted, we start by looking at the middle item.  
![](/images/array10-1.png)

item is smaller or greater than the searche value? smaller  
target number must be in the right partition of array  
no need to inspect items in the left partition  
narrow down our search by half.

![](/images/array10-2.png)

we look at the middle item🡪 smaller than the target value  
we ignore items on the left🡪focus on the items on the right.
![](/images/array10-3.png)

in every step we narrow down our search by half. if we have 1 milion items in array, we find the target with a maximum of 19 comparisons.

we have logarithmic growth in algorithms where we reduce our work by half in every step (🡪tree and graph)

## O(2^n) - exponential growth

the exponential growth is the opposite of the logaritmic growth.  
the logaritmic curve slows down as the input size grows  
the exponential curve grows faster and faster

![](/images/curves2.png)

an algoritm that runs in exponential time is not scalable at all, it become very slow very soon

## Space Complexity

we use the Big O notation to describe runtime complexity of algorithms.

we would like algorithms
**super fast and scalable**  
take **minimum amount of memory**  
hardly happens: almost always trade off between saving time and saving space.  
Sometimes we have more space🡪we optimize algorithm making it faster and more scalable.  
Other times we have limited space (build an app for a small mobile device) 🡪 we have to optimize for the space, no care of scalability: only one user of our application.

how much space required by an algorithm

greet method takes an array of strings, prints a hi message for every name.

```
public static void Greet(String[] names){
    for (int i = 0; i < names.Length; i++){
        Console.WriteLine("Hi " + names[i]);
    }
}
```

we declare a loop variable🡪 independent of the size of the input🡪allocate some additional memory for this loop variable🡪 takes O(1) space.

We declare a string array and initialize it🡪 length of this array is equal to the length of our input array.

```
public static void Greet(String[] names){
    String[] copy=new String[names.Length];
    for (int i = 0; i < names.Length; i++){
        Console.WriteLine("Hi " + names[i]);
    }
}
```

space complexity: O (n). more items in our input array🡪 more space taken🡪 direct proportion to size of input array.

for space complexity, we only look at the additional space to allocate relative to the size of the input. We always have input of size n🡪 we don't count it, we just analyze how much extra space we need to allocate for this algorithm

we focus on runtime complexity because more tricky,

think about space complexity in algorithms when we hsve limited space and see way to preserve the memory.

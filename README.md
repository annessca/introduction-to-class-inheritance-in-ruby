# Introduction to Ruby Class Inheritance 

## Understanding class inheritance in Ruby
Like most [object-oriented programming languages](https://en.wikipedia.org/wiki/Object-oriented_programming), Ruby has classes used for the purpose of [data abstraction](https://www.defit.org/data-abstraction/), [data encapsulation](https://en.wikipedia.org/wiki/Object-oriented_programming#Encapsulation), [polymorphism](https://www.webopedia.com/TERM/P/polymorphism.html), and [inheritance](https://en.wikipedia.org/wiki/Inheritance_(object-oriented_programming)). But out of the entire four, our focus is on class inheritance in object orirnted Ruby.

## What is a class?
A [class](https://study.com/academy/lesson/oop-object-oriented-programming-objects-classes-interfaces.html) is a means of creating objects which have similar attributes. It means that for classes to be created, there have to be objects with shared or related characteristics who need to be severally and distinctly classified.

Creating a class in Ruby is as simple as defining a _class_ keyword and a class name to identify it with. The end keyword comes last to indicate the end of a particular class.

### An example of a created class
```ruby
class MyClass
end
```
Classes are created to have [single responsibilities](https://en.wikipedia.org/wiki/Single_responsibility_principle). In order for a class to create objects to populate itself, it has to implement some functionalities that are based on the attributes(behaviour and state) of the objects to be created. These functionalities can be achieved through functions, better known as methods. Therefore, the class should have methods that produce results to achieve a particular purpose.

## Functions/Methods

In object-oriented programming, there are typically two types of functions: [class methods and instance methods](https://dev.to/adamlombard/ruby-class-methods-vs-instance-methods-4aje). In Ruby, functions are generally referred to as methods.Consequently, functions that belong to classes and those that exist outside the class are both known as methods.

Methods are vital to the class because all expressions of its state and behaviour are encoded in the method’s procedures and data variables. A method determines what attributes an object should have and the way it should behave. A method can have zero or more arguments depending on it’s definition. Ruby’s class method will not be featured in this article, we'll focus on instance methods. This is because the functionality of objects is contained in the instance method logic. Here is a _sample class_ that has an instance method.

```ruby
# Creating a class named MyClass
class MyClass
    # An instance method
    def an_instance_method()
        puts "My instance method implementation"
    end
end
```

## Objects / Instances

An object is an instance of a class whose type is the class it belongs to. That is why they are known either as class objects or class instances. I'll define objects as members of a class who are created at the program's runtime and stored in variables. The behaviour and atributes of member objects must be pre-determined by the class. However, an empty class like the one in our code snippet does not achieve anything. Objects or instances have to be created by a process called instantiation.

To create an object, you have to declare a variable and assign to it the `NameOfClass.new()`. Here is how to create an object for the sample class.

```ruby
var1 = MyClass.new()
```
We have created an object _var1_ for the _MyClass_. Now that our class has an object and a method, we have to give functionality to the object by calling the method on it.

**Note!** The method **an_instance_method** in our example does not have any parameters. This means that _var1_ object will have to call the method without any arguments.

```ruby
class MyClass
    def an_instance_method()
        puts "My instance method implementation."
    end

    # Create an object
    var1 = MyClass.new

    # calling a mthod on the new object
    var1.an_instance_method()
```

## Class Inheritance

Classes are related to each other when they have similar attributes. If there are obvious similarities in related classes, code repetition will happen.

Inheritance is a concept that takes advantage of the relationship between classes to make specialized versions of classes.

A class becomes a "__parent class__" when another class (a "__child class__") inherits some or all of it's features. The pair is also known as the "__super class__" and "__sub class__", or a "__base class__" and a "__derived class__".

Inheritance allows you to create a class that focuses on a specialized feature. You can even apply the concept of code reusability through inheritance. With class inheritance, a programmer can create a new class that inherits features from an existing class instead of writing those features over again.

Let's consider a class named `Person`. We want our `Person` class to only feature objects with attributes that pertain to people in the real sense of it. In that case the person object should have a name, have a designation, have a gender, and be capable of self introduction.

```ruby
class Person
  def introduction(name, designation, gender)
    puts "I am #{name}, a #{gender} #{designation}." 
  end
end

# creating objects
person = Person.new()
person.introduction(“Petera”, “supervisor”, “female”)
# => I am Petera, a female supervisor
```

Now let's create another class `Teacher`, that should inherit from `Person`:

```ruby
class Teacher < Person
  def portfolio(subject)
    puts "I teach  #{subject}"
  end

  def student_marks(stud1, stud2, stud3)
    puts "Marks recorded: #{stud1}, #{stud2},and #{stud3}"
  end
end
```

The `Teacher` class inherits from `Person` because an object of the `Teacher` class can also introduce itself, has a name, a designation, and gender. So instead of repeating any already existing code in the `Teacher` class, you can take advantage of inheritance to reuse the code in a specialized class.

Now let's create objects for `Teacher` class that should inherit from `Person`.

```ruby
# creating objects
teacher = Teacher.new()

# calling a method from Person on the Teacher objects.
teacher.introduction("John", "teacher", "male")
# => I am John, a male teacher

# calling a method from Person on the Teacher objects.
teacher.portfolio("Biology")# => I teach Biology
teacher.student_marks(80, 60, 100)# => Marks recorded: 80, 60, 100
```

The `Teacher` class may only contain specialized attributes while shared attributes already contained in `Person` class will be reused. By means of inheritance, methods and variables in the parent class are made available to objects of the child class.

### The single inheritance rule
Ruby only supports a single class inheritance. Therefore, a child class(subclass or derived class) can only have one parent class(superclass or base class), and should only inherit from that class.

For example, if `Teacher` is a child to `Person`, then `Student`, which is a child to `Teacher` can inherit from `Person` through `Teacher`.

```ruby
class Student < Teacher
    def subjects(subject1, subject2, subject3)
        puts "I major in  #{subject1}, #{subject2}, and  #{subject3}"
    end
end

student = Student.new()
student.introduction("Jill", "student", "female")
# => I am Jil, a female student
```

Although Ruby does not allow a single class to inherit from multiple classes, it offers alternative means for classes to reuse code from multiple objects. This brings in the concept of [Modules and Mixins](https://www.w3resource.com/ruby/ruby-modules-and-mixins.php).

### Modules and Mixins
A module is an object that has namespaces for variables, methods, and sometimes classes. It's definition is very similar to that of the class, only that instead of a __class__ keyword, you’ll have the __module__ instead. Let's create a __School__ module in a file __school.rb__.

```ruby
# school.rb
module School
  TEACHERS = 50
  STUDENTS = 100
  def verify(id, designation)
      puts "The ID #{id},belongs to a verified #{designation}."
  end

  def population()
      puts "A total of #{TEACHERS + STUDENTS} teachers and students"
  end
end
```

Classes can inherit any code within a module as a mixin. For this to work, you have to require the module's file inside the file where your class belongs. You should also include the module within that class so that objects within the module's namespace become available to it. There are no restrictions on the number of modules a class can get mixins from. Here is how to mix in module objects in a class.


```ruby
$LOAD_PATH << '.'
require "school"

class Teacher < Person
    def portfolio(subject)
        puts "I teach  #{subject}"
    end

    def subject_marks(stud1, stud2, stud3)
        puts "Marks recorded: #{stud1}, #{stud2},and #{stud3}"
    end
end

class Student < Teacher
  include School

  def subjects(subject1, subject2, subject3)
    puts "I major in  #{subject1}, #{subject2}, and  #{subject3} "
  end
end

student = Student.new()
student.introduction("Jill", "student", "female")
student.verify("stud111", "student")
student.population()

# The output
# => I am Jil, a female student
# => The ID stud111 belongs to a verified student.
# => A total of 150 teachers and students am Jil, a female student
```

### Method Overriding
[Method overriding](https://www.codesdope.com/ruby-more-with-oops/) is a feature in object-oriented programming that allows a subclass to bypass the implementation of a method in its superclass (also known as parent class). To achieve this, the subclass defines a method with the same name as the target method in the superclass, but yields a different or specialized outcome. Whenever an object of the subclass makes a call to that method, the superclass' implementation of the method will be replaced by that of the subclass.

```ruby
class Teacher
    def motto
        puts "To lead is to serve"
    end
end

class Student < Teacher
    # A method to override the superclass method
    def motto
        puts "We are tomorrow’s leaders"
    end
end

student = Students.new()
student.motto # => We are tomorrow's leaders
```

### Invoking Methods from the Super Class

When the super class and the subclass share a method with the same signature, a call to that method by an object of the subclass always overrides the method of the superclass. The way to access the parent's version of the method is to invoke the super keyword.

If there are no parameters in the shared method, when __super__ or __super()__ is invoked, the logic of both methods are executed.

```ruby
class Teacher
    def motto
        puts "To lead is to serve"
    end
end

class Student < Teacher
    # A method to override the superclass method
    def motto
        super() # Invoking super would give the same result.
        puts "We are tomorrow's leaders"
    end
end

student = Student.new()
student.motto

# => To lead is to serve
# => We are tomorrow's leaders
```

If there are arguments in the superclass' method, invoking __super()__ will execute those arguments. This is because super() takes no arguments from the subclass.

```ruby
class Teacher
    def get_profile(id = "teach001", name = "James Bart")
        puts "This profile belongs to #{name}, with ID #{id}"
    end
end

class Student < Teacher
    # calling super()
    def profile(id, name)
        super()
        puts "We are tomorrow's leaders"
    end
end

person = Student.new()
person.profile("stud001", "Lisa Green")

# => This profile belongs to James Bart, with ID teach001
# => We are tomorrow's leaders
```

If in the same situation we invoke _super_ without brackets, the arguments from the subclass' method are passed to the parent class to be executed.

```ruby
class Teacher
    def profile(id = "teach001", name = "James Bart")
        puts "This profile belongs to #{name}, with ID #{id}"
    end
end

class Student < Teacher
    # calling super()
    def profile(id, name)
        super
        puts "We are tomorrow's leaders"
    end
end

person = Student.new("stud001", "Lisa Green")
person.profile("stud001", "Lisa Green")

# => This profile belongs to Lisa Green, with ID stud001
# => We are tomorrow's leaders
```

**Note:** One way to prevent the arguments of the  subclass' object from being passed to the superclass is by calling __super()__ in it's method. On the other hand, an effective way to impose the arguments of the subclass' object on the superclass is by calling __super()__ with the parameters of the subclass. For example, calling `super(id, name)` in the subclass.

### Conclusion

Class inheritance is a powerful feature in object oriented programming that prevents your program from having duplicated code. However, it should only be used sparingly when there are features to be shared among objects.






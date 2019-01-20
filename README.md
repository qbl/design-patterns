# Learning Notes on Design Patterns

## 1. Introduction

In short, a pattern is a solution to a problem in a context. Design patterns in Object Oriented scope are descriptions of communicating objects and classes that are customized to solve a general design problem in a particular context.

Design patterns in object oriented are classified by two criteria: purpose and scope. A pattern can have one of the following purpose:
1. Creational Purpose
    Creational patterns concern the process of object creation.
2. Structural Purpose
    Structural patterns deal with the composition of classes or objects.
3. Behavioral Purpose
    Behavioral patterns characterize the ways in which classes or objects interact and distribute responsibility.

### How Design Patterns Solve Design Problems

1. Finding Appropriate Objects

    Object oriented programs are made up of objects. An **object** has both **data** and **methods** that operate on its data. An object performs methods when it receives request from a client. Requests are the only way to get an object to execute its methods. And methods are the only way to change an object's internal data. This concept of hiding object's internal states is called **encapsulation**.

    Encapsulation is an important concept of object oriented programming that is often forgotten when we are not conscious that we are writing programs within OOP paradigm. It is not uncommon to see programs that allow object's internal states to be manipulated from outside instead of through executing its methods. For instance, take a look at the following snippet:

    ```ruby
    class Line
      attr_accessor :x1, :y1, :x2, :y2

      def initialize(x1, y1, x2, y2)
        @x1 = x1
        @y1 = y1
        @x2 = x2
        @y2 = y2
      end
    end

    line = Line.new(0, 0, 3, 4)
    length = Math.sqrt(((line.x2 - line.x1) ** 2) + ((line.y2 - line.y1) ** 2))
    ```

    In the code above, there are several basic OOP objects that we break. First, our `line` object does not have any methods. Second, we expose the internal states of `line` object and therefore we break the encapsulation concept. And third, by making `x1, y1, x2, y2` as `attr_accessor`, we enable manipulation of object's internal states via assignment operations. A better code would be:

    ```ruby
    class Line
      attr_reader :x1, :y1, :x2, :y2

      def initialize(x1, y1, x2, y2)
        @x1 = x1
        @y1 = y1
        @x2 = x2
        @y2 = y2
      end

      def length
        Math.sqrt(((@x2 - @x1) ** 2) + ((@y2 - @y1) ** 2))
      end
    end

    line = Line.new(0, 0, 3, 4)
    length = line.length
    ```

    In the code above, we add a `length` method to our `line` object, hide its internal states, and even though we don't change any internal states of the object, we request its length through a request to execute `length` method.

    Modelling objects is the crux of object oriented programming. Many objects in OOP programs are modeled after real world objects. However, object oriented desgins often end up with objects that has no counterpart in the real world, one of the most obvious example is arrays. Design patterns help us identify less-obvious abstractions and the objects that can capture them. We will see these kind of objects later when we discuss about Composite, Strategy, or State pattern.
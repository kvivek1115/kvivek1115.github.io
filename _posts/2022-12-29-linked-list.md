#### Linked List implementation in Ruby

Linked list is a data structure, which consist of two part Data & Address to Next element.

In this blog, we will implement a class to demostrate working on Ruby Linked List. In Ruby generally we are not dealing with pointer. But idirectly lost of time we uses references.

For Example

```
a = [1,2,3,4]
b = a

b << 5

p b # [1,2,3,4,5]

```

In this example `a` hold the reference of array object and same reference assigned into `b` so modifying it also modified object `a`

with the same logic let's implement Linked list in Ruby.


First lets add `Node` class which hold the value and address location of next item.

```
class Node
  attr_accessor :value, :next

  def initialize(value, next_node = nil)
    @value = value
    @next = next_node
  end
end

```

And the `LinkedList` class which have `append`, `pre_append` and `list` method.

```
class LinkedList
  attr_reader :list, :length
  attr_accessor :head, :tail

  def initialize(value = nil)
    @head = nil
    @tail = nil
    @length = 0

    first_node(value) if value
  end

  def append(value)
    return first_node(value) unless @head

    node = Node.new(value)
    @tail.next = node
    @tail = node
    @length += 1
  end

  def pre_append(value)
    return first_node(value) unless @head

    node = Node.new(value, @head)
    @head = node
    @length += 1
  end

  def first_node(value)
    node = Node.new(value)
    @head = node
    @tail = @head
    @length += 1
  end

  def list
    node = head
    while node != nil
      print node.value
      node = node.next
      print "-->" if node
    end
  end
end
```

Here some operations on linked list class.

```
ll = LinkedList.new
ll.append(12)
ll.append(5)
ll.append(15)
ll.pre_append(30)
ll.list # 30-->12-->5-->15
```

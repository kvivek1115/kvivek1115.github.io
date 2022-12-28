Hash stored key value pair in non lenear momery locations, in ruby we already Hash class & `{}` to store key/value pairs.

In this blog, we will create our own data structure class to manage to key/value pair.

So, naming a class `HashTable` which taking the size as an argument.

```
class HashTable
  attr_accessor :data

  def initialize(size)
    @data = Array.new(size)
  end
end
```

Hash also have hash function to generate idempotent uniq string based on key, In order to keep it simple added `_hash` method which location of array gets calculated on the key.

```
class HashTable
  attr_accessor :data

  def initialize(size)
    @data = Array.new(size)
  end

  private

  def _hash(key)
    hash = 0
    key.chars.each_with_index do |char, index|
      hash = (hash + char.ord * index ) % data.length
    end
    hash
  end
end

```

Implement `set` method to set the key & value into HashTable.

```
class HashTable
  attr_accessor :data

  def initialize(size)
    @data = Array.new(size)
  end

  def set(key, value)
    address = _hash(key)
    unless data[address]
      data[address] = []
    end

    data[address].push([key, value])
  end

  private

  def _hash(key)
    hash = 0
    key.chars.each_with_index do |char, index|
      hash = (hash + char.ord * index ) % data.length
    end
    hash
  end
end
```

Implement `get` method to get the value of given key.

```
class HashTable
  attr_accessor :data

  def initialize(size)
    @data = Array.new(size)
  end

  def set(key, value)
    address = _hash(key)
    unless data[address]
      data[address] = []
    end

    data[address].push([key, value])
  end

  def get(key)
    address = _hash(key)
    bucket = data[address]
    if bucket
      bucket.each do |item|
        return item[1] if item[0] == key
      end
    end
  end

  private

  def _hash(key)
    hash = 0
    key.chars.each_with_index do |char, index|
      hash = (hash + char.ord * index ) % data.length
    end
    hash
  end
end
```

Also to get all the keys of HashTable `keys` methods need to implement.


```
class HashTable
  attr_accessor :data

  def initialize(size)
    @data = Array.new(size)
  end

  def set(key, value)
    address = _hash(key)
    unless data[address]
      data[address] = []
    end

    data[address].push([key, value])
  end

  def get(key)
    address = _hash(key)
    bucket = data[address]
    if bucket
      bucket.each do |item|
        return item[1] if item[0] == key
      end
    end
  end

  def keys
    result = []
    data.each do |bucket|
      if bucket && bucket.length > 0
        bucket.each do |item|
          result << item[0]
        end
      end
    end
    result
  end

  private

  def _hash(key)
    hash = 0
    key.chars.each_with_index do |char, index|
      hash = (hash + char.ord * index ) % data.length
    end
    hash
  end
end

```

Now, lets do couple of iterations on `HashTable` class

```
hash = HashTable.new(50)

hash.set('grapes', 1000)
hash.set('apples', 5000)

p hash.get('grapes') # 1000
p hash.keys # ['grapes', 'apples']

```

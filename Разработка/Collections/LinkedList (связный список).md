### Основные понятия

Суть [[LinkedList (связный список)]] заключается в том, что внутри списка еще есть класс `Node{}`, который имеет 3 поля - предыдущий элемент, типа `Node`, текущий элемент - `тип Т`, и следующий элемент типа `Node`. 

[[Алгоритмическая сложность в ArrayList]] - `LinkedList` вставки в начало или середину коллекции является `0(1)` и такая же сложность удаления.

```java
class Node {
	Node previous;
	T value;
	Node next;
}
```
### Примеры использования:

```java
public class CarLinkedList implements CarList {  
    private Node first;  
    private Node last;  
    private int size = 0;  
  
    @Override  
    public Car get(int index) {  
        return getNode(index).value;  
    }  
  
    @Override  
    public void add(Car car) {  
        // если есть какой-либо элемент в коллекции, то добавляем его  
        if (size == 0) {  
            first = new Node(null, car, null);  
            last = first;  
        } else {  
//            если в коллекции, уже что-то есть, то нужно создать новый объект Node  
//            который станет последним, а элемент, который был последним, станет предпоследним  
            Node secondLast = last;  
            last = new Node(secondLast, car, null);  
            secondLast.next = last;  
        }  
        size++;  
    }  
  
    @Override  
    public void add(Car car, int index) {  
        if (index < 0 || index > size) {  
            throw new IndexOutOfBoundsException();  
        }  
        if (index == size) {  
            add(car);  
            return;  
        }  
        Node nodeNext = getNode(index);  
        Node nodePrevious = nodeNext.previous;  
        Node newNode = new Node(nodePrevious, car, nodeNext);  
        nodeNext.previous = newNode;  
        if (nodePrevious != null) {  
            nodePrevious.next = newNode;  
        } else {  
            first = newNode;  
        }  
        size++;  
    }  
  
    @Override  
    public boolean remove(Car car) {  
        Node node = first;  
        for (int i = 0; i < size; i++) {  
            if (node.value.equals(car)) {  
                return removeAt(i);  
            }  
            node = node.next;  
        }  
        return false;  
    }  
  
    @Override  
    public boolean removeAt(int index) {  
        Node node = getNode(index);  
        Node nodeNext = node.next;  
        Node nodePrevious = node.previous;  
        if (nodeNext != null) {  
            nodeNext.previous = nodePrevious;  
        } else {  
            last = nodePrevious;  
        }  
        if (nodePrevious != null) {  
            nodePrevious.next = nodeNext;  
        } else {  
            first = nodeNext;  
        }  
        size--;  
        return true;  
    }  
  
    @Override  
    public int size() {  
        return size;  
    }  
  
    @Override  
    public void clear() {  
        first = null;  
        last = null;  
        size = 0;  
    }  
  
    private Node getNode(int index) {  
        if (index < 0 || index >= size) {  
            throw new IndexOutOfBoundsException();  
        }  
        Node node = first;  
        for (int i = 0; i < index; i++) {  
            node = node.next;  
        }  
        return node;  
    }  
  
    private static class Node {  
        private Node previous;  
        private Car value;  
        private Node next;  
  
        public Node(Node previous, Car value, Node next) {  
            this.previous = previous;  
            this.value = value;  
            this.next = next;  
        }  
    }  
}
```
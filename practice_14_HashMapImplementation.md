# Implement a HashMap
``` java
class MyHashMap<> {
    public static class Node<K, V> {
        private final K key;
        private V value;
        Node<K, V> next = null;
        public Node(K k, V v) {
            key = k;
            value = v;
        }
        public K getKey() {
            return key;
        }
        public V getValue() {
            return value;
        }
        public void setValue() {
            value = v;
        }
    }

    private static final int INIT_CAP = 16;
    private static final double LOAD_FACTOR = 0.75;

    private Node<K, V>[] array;
    private int size;

    // constructor
    public MyHashMap() {
        array = (Node<K, V>[]) new Node[INIT_CAP];
        size = 0;
    }

    public int size() {
        return size;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public void clear() {
        Arrays.fill(array, null);
        size  = 0;
    }

    public V get(K key) {
        Node<K, V> node = array[index(key)];
        while (node != null) {
            if (equalsKey(node.getKey(), key)) {
                return node.getValue();
            }
            node = node.next;
        }
        return null;
    }

    public boolean containsKey(K key) {
        Node<K, V> node = array[index(key)];
        while (node != null) {
            if (equalsKey(node.getKey(), key)) {
                return true;
            }
            node = node.next;
        }
        return false;
    }

    public V put(K key, V value) {
        int i = index(key);
        Node<K, V> node = array[i];
        while (node != null) {
            if (equalsKey(node.getKey(), key)) {
                V oldValue = node.getValue();
                node.setValue(value);
                return oldValue;
            }
            node = node.next;
        }
        Node<K, V> newEntry = new Node<>(key, value);
        newEntry.next = array[i];
        array[i] = newEntry;
        size++;
        if (needRehashing()) {
            rehash();
        }
        return null;
    }

    public V remove(K key) {
        int i = index(key);
        Node<K, V> prev = null;
        Node<K, V> curr = array[i];
        while (curr != null) {
            if (equalsKey(curr.getKey()), key) {
                if (prev == null) {
                    array[i] = curr.next;
                } else {
                    prev.next = curr.next;
                }
                size--;
                return curr.getValue();
            }
            prev = curr;
            curr = curr.next;
        }
        return null;
    }

    private int hash(K key) {
        if (key == null) return 0;
        int code = key.hashCode();
        return code & 0x7fffffff;
    }

    private int index() {
        return hash(key) % array.length;
    }

    private boolean equalsKey(K a, K b) {
        return a == b || a != null && a.equals(b);
    }

    private boolean needRehashing() {
        return size > LOAD_FACTOR * array.length;
    }

    private void rehash() {
        Entry<K, V>[] old = array;
        array = (Entry<K, V>[]) new Entry[array.length * 2];
        for (Entry<K, V> e : old) {
            while (e != null) {
                Entry<K, V> next = e.next;
                int i = getIndex(e.getKey());
                e.next = array[i]; // put it to the front of the linked list
                array[i] = e; // assign e to the array[i] position,complete the update
                e = next; // move the node on the old linked list
            }
        }
    }
}
```

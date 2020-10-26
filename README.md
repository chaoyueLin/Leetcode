# Leetcode
[知必会](https://github.com/wangzheng0822/algo)
[https://github.com/yuanguangxin/LeetCode](https://github.com/yuanguangxin/LeetCode)

## 146 LRU
运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

    class LRUCache {
    static class Node {
        private int key;
        private int value;
        Node prev, next;
        public Node(int key, int value) {
            this.key = key;
            this.value = value;
        }
    }
    
    private int capacity;
    private Map<Integer, Node> map;
    private Node dummyhead, dummytail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.map = new HashMap<>();
        this.dummyhead = new Node(-1, -1);
        this.dummytail = new Node(-1, -1);
        this.dummyhead.next = this.dummytail;
        this.dummytail.prev = this.dummyhead;
    }
    
    public int get(int key) {
        Node node = getNode(key);
        if(null == node) return -1;
        return node.value;
    }
    
    Node getNode(int key) {
        Node node = map.get(key);
        if(null == node) return null;
        disconnect(node);
        insertHead(node);
        return node;
    }
    
    void disconnect(Node node) {
        node.next.prev = node.prev;
        node.prev.next = node.next;        
    }
    
    void insertHead(Node node) {
        node.next = dummyhead.next;
        dummyhead.next.prev = node;
        node.prev = dummyhead;
        dummyhead.next = node;        
    }
    
    public void put(int key, int value) {
        Node node = getNode(key);
        if(null != node) {
            node.value = value;
        }
        else {
            node = new Node(key, value);
            insertHead(node);
            
            map.put(key, node);
            if(map.size() > capacity) {
                Node tail = dummytail.prev;
                disconnect(tail);
                map.remove(tail.key);
            }
        }
    }
    }

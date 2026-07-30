# Linked List in Java — Complete Beginner Notes

## 1. What is a Linked List?

A **Linked List** is a linear data structure where elements (called **nodes**) are not stored in contiguous memory (unlike arrays). Instead, each node contains:
1. **Data** — the actual value
2. **Next** — a reference/pointer to the next node in the sequence

```
[Data|Next] -> [Data|Next] -> [Data|Next] -> null
```

### Why use Linked List instead of Array?

| Feature | Array | Linked List |
|---|---|---|
| Size | Fixed (static arrays) | Dynamic (grows/shrinks easily) |
| Memory | Contiguous | Non-contiguous (scattered) |
| Insertion/Deletion | Costly (shifting elements) | Easy (just change pointers) |
| Access | O(1) random access | O(n) - must traverse |
| Extra memory | None | Extra memory for storing pointer |

---

## 2. Types of Linked Lists

1. **Singly Linked List** — each node points to the next node only.
2. **Doubly Linked List** — each node has pointers to both next and previous nodes.
3. **Circular Linked List** — the last node points back to the first node (forms a circle).

---

## 3. Singly Linked List — Node Structure in Java

```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

---

## 4. Basic Singly Linked List Implementation

```java
class LinkedList {
    Node head;

    // 1. Insert at the end
    public void insertAtEnd(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            return;
        }
        Node temp = head;
        while (temp.next != null) {
            temp = temp.next;
        }
        temp.next = newNode;
    }

    // 2. Insert at the beginning
    public void insertAtBeginning(int data) {
        Node newNode = new Node(data);
        newNode.next = head;
        head = newNode;
    }

    // 3. Insert at a given position (0-indexed)
    public void insertAtPosition(int data, int position) {
        if (position == 0) {
            insertAtBeginning(data);
            return;
        }
        Node newNode = new Node(data);
        Node temp = head;
        for (int i = 0; i < position - 1 && temp != null; i++) {
            temp = temp.next;
        }
        if (temp == null) return; // position out of range
        newNode.next = temp.next;
        temp.next = newNode;
    }

    // 4. Delete a node by value
    public void deleteByValue(int value) {
        if (head == null) return;
        if (head.data == value) {
            head = head.next;
            return;
        }
        Node temp = head;
        while (temp.next != null && temp.next.data != value) {
            temp = temp.next;
        }
        if (temp.next != null) {
            temp.next = temp.next.next;
        }
    }

    // 5. Search for a value
    public boolean search(int value) {
        Node temp = head;
        while (temp != null) {
            if (temp.data == value) return true;
            temp = temp.next;
        }
        return false;
    }

    // 6. Print the list
    public void printList() {
        Node temp = head;
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }

    // 7. Length of the list
    public int length() {
        int count = 0;
        Node temp = head;
        while (temp != null) {
            count++;
            temp = temp.next;
        }
        return count;
    }
}
```

### Usage Example

```java
public class Main {
    public static void main(String[] args) {
        LinkedList list = new LinkedList();
        list.insertAtEnd(10);
        list.insertAtEnd(20);
        list.insertAtEnd(30);
        list.insertAtBeginning(5);
        list.printList();          // 5 -> 10 -> 20 -> 30 -> null
        list.deleteByValue(20);
        list.printList();          // 5 -> 10 -> 30 -> null
        System.out.println(list.search(10)); // true
        System.out.println(list.length());   // 3
    }
}
```

---

## 5. Doubly Linked List

Each node stores a reference to both the **previous** and **next** node.

```java
class DNode {
    int data;
    DNode prev, next;

    DNode(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}
```

```java
class DoublyLinkedList {
    DNode head;

    public void insertAtEnd(int data) {
        DNode newNode = new DNode(data);
        if (head == null) {
            head = newNode;
            return;
        }
        DNode temp = head;
        while (temp.next != null) temp = temp.next;
        temp.next = newNode;
        newNode.prev = temp;
    }

    public void printForward() {
        DNode temp = head;
        while (temp != null) {
            System.out.print(temp.data + " <-> ");
            temp = temp.next;
        }
        System.out.println("null");
    }
}
```

---

## 6. Circular Linked List

The last node's `next` points back to the `head` instead of `null`.

```java
class CircularLinkedList {
    Node head;

    public void insertAtEnd(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            newNode.next = head;
            return;
        }
        Node temp = head;
        while (temp.next != head) temp = temp.next;
        temp.next = newNode;
        newNode.next = head;
    }

    public void printList() {
        if (head == null) return;
        Node temp = head;
        do {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        } while (temp != head);
        System.out.println("(back to head)");
    }
}
```

---

## 7. Java's Built-in LinkedList (java.util.LinkedList)

Java provides a ready-made doubly linked list implementation:

```java
import java.util.LinkedList;

LinkedList<Integer> list = new LinkedList<>();
list.add(10);
list.add(20);
list.addFirst(5);
list.addLast(30);
list.remove(Integer.valueOf(20));
System.out.println(list); // [5, 10, 30]
```

Useful methods: `add()`, `addFirst()`, `addLast()`, `remove()`, `removeFirst()`, `removeLast()`, `get(i)`, `contains()`, `size()`.

---

## 8. Time Complexity Summary

| Operation | Singly Linked List |
|---|---|
| Access (by index) | O(n) |
| Search | O(n) |
| Insert at head | O(1) |
| Insert at tail | O(n) (O(1) if tail pointer kept) |
| Delete at head | O(1) |
| Delete at tail | O(n) |

---

# Important DSA Questions on Linked List

## Q1. Reverse a Linked List (Iterative)

```java
public Node reverse(Node head) {
    Node prev = null, curr = head;
    while (curr != null) {
        Node nextNode = curr.next;
        curr.next = prev;
        prev = curr;
        curr = nextNode;
    }
    return prev; // new head
}
```
**Time:** O(n) &nbsp; **Space:** O(1)

---

## Q2. Detect a Cycle in a Linked List (Floyd's Cycle Detection / Tortoise-Hare)

```java
public boolean hasCycle(Node head) {
    Node slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}
```
**Idea:** Slow pointer moves 1 step, fast pointer moves 2 steps. If there's a cycle, they will eventually meet.

---

## Q3. Find the Middle of a Linked List

```java
public Node findMiddle(Node head) {
    Node slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow; // middle node
}
```

---

## Q4. Merge Two Sorted Linked Lists

```java
public Node mergeTwoLists(Node l1, Node l2) {
    Node dummy = new Node(-1);
    Node tail = dummy;
    while (l1 != null && l2 != null) {
        if (l1.data <= l2.data) {
            tail.next = l1;
            l1 = l1.next;
        } else {
            tail.next = l2;
            l2 = l2.next;
        }
        tail = tail.next;
    }
    tail.next = (l1 != null) ? l1 : l2;
    return dummy.next;
}
```

---

## Q5. Remove N-th Node from the End

```java
public Node removeNthFromEnd(Node head, int n) {
    Node dummy = new Node(-1);
    dummy.next = head;
    Node fast = dummy, slow = dummy;

    for (int i = 0; i < n; i++) fast = fast.next;

    while (fast.next != null) {
        fast = fast.next;
        slow = slow.next;
    }
    slow.next = slow.next.next;
    return dummy.next;
}
```

---

## Q6. Check if a Linked List is a Palindrome

```java
public boolean isPalindrome(Node head) {
    // Step 1: find middle
    Node slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }
    // Step 2: reverse second half
    Node secondHalf = reverse(slow);
    Node firstHalf = head;
    // Step 3: compare both halves
    while (secondHalf != null) {
        if (firstHalf.data != secondHalf.data) return false;
        firstHalf = firstHalf.next;
        secondHalf = secondHalf.next;
    }
    return true;
}
```

---

## Q7. Find the Intersection Point of Two Linked Lists

```java
public Node getIntersectionNode(Node headA, Node headB) {
    Node a = headA, b = headB;
    while (a != b) {
        a = (a == null) ? headB : a.next;
        b = (b == null) ? headA : b.next;
    }
    return a; // intersection node or null
}
```
**Idea:** Switching heads equalizes the path length difference between both lists.

---

## Q8. Remove Duplicates from an Unsorted Linked List

```java
public void removeDuplicates(Node head) {
    if (head == null) return;
    java.util.HashSet<Integer> seen = new java.util.HashSet<>();
    Node curr = head, prev = null;
    while (curr != null) {
        if (seen.contains(curr.data)) {
            prev.next = curr.next;
        } else {
            seen.add(curr.data);
            prev = curr;
        }
        curr = curr.next;
    }
}
```

---

## Q9. Add Two Numbers Represented as Linked Lists (digits stored in reverse order)

```java
public Node addTwoNumbers(Node l1, Node l2) {
    Node dummy = new Node(-1);
    Node curr = dummy;
    int carry = 0;
    while (l1 != null || l2 != null || carry != 0) {
        int sum = carry;
        if (l1 != null) { sum += l1.data; l1 = l1.next; }
        if (l2 != null) { sum += l2.data; l2 = l2.next; }
        carry = sum / 10;
        curr.next = new Node(sum % 10);
        curr = curr.next;
    }
    return dummy.next;
}
```

---

## Q10. Detect and Find the Starting Point of a Cycle

```java
public Node detectCycleStart(Node head) {
    Node slow = head, fast = head;
    boolean hasCycle = false;

    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) { hasCycle = true; break; }
    }
    if (!hasCycle) return null;

    slow = head;
    while (slow != fast) {
        slow = slow.next;
        fast = fast.next;
    }
    return slow; // start of the cycle
}
```

---

## Q11. Reverse a Linked List in Groups of K

```java
public Node reverseKGroup(Node head, int k) {
    Node curr = head;
    int count = 0;
    while (curr != null && count < k) {
        curr = curr.next;
        count++;
    }
    if (count == k) {
        Node reversedHead = reverseKGroup(curr, k); // reverse remaining
        curr = head;
        Node prev = reversedHead;
        for (int i = 0; i < k; i++) {
            Node nextNode = curr.next;
            curr.next = prev;
            prev = curr;
            curr = nextNode;
        }
        head = prev;
    }
    return head;
}
```

---

## Quick Revision Checklist

- [ ] Can you reverse a linked list without extra space?
- [ ] Do you understand slow/fast pointer (Tortoise-Hare) technique?
- [ ] Can you merge two sorted linked lists?
- [ ] Can you find the middle node in a single pass?
- [ ] Do you know how to detect and locate a cycle?
- [ ] Can you check for a palindrome in O(1) extra space?
- [ ] Can you find the intersection of two linked lists without extra space?

**Tip:** Most linked list problems are solved using one of these patterns:
1. Dummy node technique (simplifies edge cases)
2. Two-pointer / slow-fast pointer technique
3. Recursion (especially for reversal problems)
4. Iterative pointer manipulation (prev, curr, next)
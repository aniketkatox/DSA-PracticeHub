# Python Code

```python
class Node:
    def __init__(self, url):
        """
        Node class to represent a node in the doubly linked list.

        Args:
            url (str): The URL of the web page.
        """
        self.url = url
        self.prev = None
        self.next = None


class BrowserHistory:
    def __init__(self, homepage):
        """
        BrowserHistory class to manage the browser history.

        Args:
            homepage (str): The URL of the homepage.
        """
        self.head = Node(homepage)  # Head node of the browser history
        self.curr = self.head  # Current node representing the current page

    def visit(self, url):
        """
        Visit a new URL and add it to the browser history.

        Args:
            url (str): The URL to visit.
        """
        new_node = Node(url)
        self.curr.next = new_node
        new_node.prev = self.curr
        self.curr = self.curr.next

    def back(self, steps):
        """
        Move back a certain number of steps in the browser history.

        Args:
            steps (int): The number of steps to move back.

        Returns:
            str: The URL of the page after moving back.
        """
        while self.curr.prev is not None and steps > 0:
            self.curr = self.curr.prev
            steps -= 1
        return self.curr.url

    def forward(self, steps):
        """
        Move forward a certain number of steps in the browser history.

        Args:
            steps (int): The number of steps to move forward.

        Returns:
            str: The URL of the page after moving forward.
        """
        while self.curr.next is not None and steps > 0:
            self.curr = self.curr.next
            steps -= 1
        return self.curr.url
```

**Time Complexity**
- The time complexity is primarily determined by the number of steps O(steps) for the back and forward operations. 

**Space Complexity**
- The space complexity of the BrowserHistory class is O(N), where N is the number of URLs visited. This is because we are using additional memory to store the URLs in the doubly linked list.

# C++ Code

```cpp
// Doubly Linked List Node
class Node {
public:
    string url;
    Node* prev;
    Node* next;

    // Node constructor
    Node(string url) {
        this->url = url;
        prev = NULL;
        next = NULL;
    }
};

class BrowserHistory {
public:
    Node* head;  // Head node of the browser history
    Node* curr;  // Current node representing the current page

    // BrowserHistory constructor
    BrowserHistory(string homepage) {
        head = new Node(homepage);
        curr = head;
    }

    /**
     * Visit a new URL and add it to the browser history.
     * @param url The URL to visit.
     */
    void visit(string url) {
        Node* newNode = new Node(url);
        curr->next = newNode;
        newNode->prev = curr;
        curr = curr->next;
    }

    /**
     * Move back a certain number of steps in the browser history.
     * @param steps The number of steps to move back.
     * @return The URL of the page after moving back.
     */
    string back(int steps) {
        while (curr->prev != NULL && steps > 0) {
            curr = curr->prev;
            steps--;
        }
        return curr->url;
    }

    /**
     * Move forward a certain number of steps in the browser history.
     * @param steps The number of steps to move forward.
     * @return The URL of the page after moving forward.
     */
    string forward(int steps) {
        while (curr->next != NULL && steps > 0) {
            curr = curr->next;
            steps--;
        }
        return curr->url;
    }
};
```

### Queue 

1. FIFO
   Opposite of stack
   Doctor queue 
   
1. Specify a stack size while creating MyStack object
2. Constructor 
    1. top = -1
    2. Initalize stack array
3. Push
    1. check if stack is full
    2. `this.stackArr[++top] = entry`
4. Pop
    1. check if stack is empty
    2. `this.stackArr[top--]`
5.Peek - `this.stackArr[top]`   

```
public class MyStack {

    private int size;
    private int top;
    private int[] stackArr;

    public MyStack(int size) {
        this.size = size;
        this.top = -1;
        this.stackArr = new int[size];
    }

    private void push(int entry) throws Exception {

        if (this.isStackFull()) {
            throw new Exception("Stack is full. Can not add element");
        }
        System.out.println("Adding: " + entry);
        this.stackArr[++top] = entry;
    }

    private boolean isStackFull() {
        return (top == size - 1);
    }

    private int peek() {
        return this.stackArr[top];
    }

    private void pop() throws Exception {

        if (this.isStackEmpty()) {
            throw new Exception("Stack is empty. Can not remove element.");
        }
        System.out.println("Removed entry: " + this.stackArr[top--]);
    }

    private boolean isStackEmpty() {
        return top == -1;
    }

    public static void main(String[] args) {

        MyStack myStack = new MyStack(5);

        try {
            myStack.push(1);
            myStack.push(2);
            myStack.push(3);
            myStack.push(4);
            myStack.push(5);
            myStack.pop();
            myStack.pop();
            myStack.pop();

            /*
            Adding: 1
            Adding: 2
            Adding: 3
            Adding: 4
            Adding: 5
            Removed entry: 5
            Removed entry: 4
            Removed entry: 3
            Top element 2*/

            System.out.println("Top element " + myStack.peek());
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```
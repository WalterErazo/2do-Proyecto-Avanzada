# 2do-Proyecto-Avanzada
### En el siguiente proyecto se relizara un preceso de carga de archivos y con la misma se graficaran estas graficas seran de todos las estructuras vista en clase.


## Clase Graficas:
### En esta clase se hace de manera grafica todo el proyecto ya que se hace en Java Formularios.














## Clase Main: 
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author t211
 */
public class Main {

    /**
     * @param args the command line arguments
     */
    public static void main(String[] args) {
        // TODO code application logic here
        
        Graficas obj = new Graficas();
        obj.setVisible(true);
        obj.setLocationRelativeTo(null);
    }
    
}




## Estructuras Vistas en Clase:
### ArrayQueue:
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public class ArrayQueue<E> implements Queue<E> {
	public static final int CAPACITY=1000;
	private E[] data;
	private int f = 0; //Index for front element
	private int sz = 0; //Curent qty
	
	public ArrayQueue( ) {
		this(CAPACITY);
	}

	public ArrayQueue(int capacity) {
		data = (E[ ]) new Object[capacity];
	}
	
	public int size(){
		return sz;
	}
	
	public boolean isEmpty() {
		return (sz == 0);
	}
	
	public void enqueue(E e) {
		int avail = (f + sz) % data.length;
		data[avail] = e;
		sz++;
	}
	
	public E first( ) {
		if (isEmpty()) return null;
		return data[f];
	}
	
	public E dequeue( ) {
		if (isEmpty()) return null;
		E answer = data[f];
		data[f] = null;
		f = (f + 1) % data.length;
		sz--;
		return answer;
	}
}

### ArrayStack: 

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public class ArrayStack<E> implements Stack<E> {
	public static final int CAPACITY=1000;
	private E[] data;
	private int t=-1;
	
	public ArrayStack() {
		this(CAPACITY);
	}

	public ArrayStack(int capacity) {
		data = (E[]) new Object[capacity];
	}

	public int size(){
		return t+1;
	}

	public boolean isEmpty() {
		return (t == -1);
	}

	public void push(E e) {
		data[++t] = e;
	}

	public E top() {
		if (isEmpty()) return null;
		return data[t];
	}

	public E pop() {
		if (isEmpty()) return null;
		E response = data[t];
		data[t] = null;
		t--;
		return response;
	}
}


### CircularLinkedList:

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public class CircularLinkedList<E> {
	private static class Node<E>{
		private E element;
		private Node<E> next;
		public Node(E element, Node<E> next) {
			super();
			this.element = element;
			this.next = next;
		}
		public E getElement() {
			return element;
		}
		public Node<E> getNext() {
			return next;
		}
		public void setNext(Node<E> next) {
			this.next = next;
		}
	}

	private Node<E> tail = null;
	
	private int size = 0;
	
	public int size() {return size;}
	
	public boolean isEmpty() { return size == 0;}
	
	public E first() {
		if (isEmpty()) return null;
		return tail.getNext().getElement();//Primer cambio
	}
	
	public E last() {
		if (isEmpty()) return null;
		return tail.getElement();
	}
	
	public void rotate() {
		if (tail != null)
			tail = tail.getNext();
	}
	
	public void addFirst(E e) {
		
		if(size == 0) {
			tail = new Node<>(e, null);
			tail.setNext(tail);
		}else {
			Node<E> newest = new Node<>(e, tail.getNext());
			tail.setNext(newest);
		}
		size++;
	}
	
	public void addLast(E e) {
		addFirst(e);
		tail = tail.getNext();
	}
	
	public E removeFirst() {
		if(isEmpty()) return null;
		Node<E> head = tail.getNext();
		if(head == tail) tail = null;
		else tail.setNext(head.getNext());
		size--;
		return head.getElement();
	}
}


### DoubleLinkedList


/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public class DoubleLinkedList<E> {

	private static class Node<E> {
		private E element;
		private Node<E> prev;//Anterior
		private Node<E> next;//Siguiente

		public Node(E e, Node<E> p, Node<E> n) {
			element = e;
			prev = p;
			next = n;
		}

		public E getElement() {
			return element;
		}

		public Node<E> getPrev() {
			return prev;
		}

		public void setPrev(Node<E> prev) {
			this.prev = prev;
		}

		public Node<E> getNext() {
			return next;
		}

		public void setNext(Node<E> next) {
			this.next = next;
		}

	}

	private Node<E> header = null;//Referencia
	private Node<E> trailer = null;
	private int size = 0;

	public DoubleLinkedList() {
		header = new Node<>(null, null, null);
		trailer = new Node<>(null, header, null);
		header.setNext(trailer);
	}

	public int size() {
		return size;
	}

	public boolean isEmpty() {
		return size == 0;
	}

	public E first() {
		if (isEmpty())
			return null;
		return header.getNext().getElement();
	}

	public E last() {
		if (isEmpty())
			return null;
		return trailer.getPrev().getElement();
	}

	public void addFirst(E e) {
		addBetween(e, header, header.getNext());
	}

	public void addLast(E e) {
		addBetween(e, trailer.getPrev(), trailer);
	}

	public E removeFirst() {
		if (isEmpty())
			return null;
		return remove(header.getNext());
	}
	public E removeLast() {
		if (isEmpty())
			return null;
		return remove(trailer.getPrev());
	}
	
	private void addBetween(E e, Node<E> predecessor, Node<E> successor) {
		Node<E> newest = new Node<>(e, predecessor, successor);
		predecessor.setNext(newest);
		successor.setPrev(newest);
		size++;
	}
	
	private E remove(Node<E> node) {
		Node<E> predecessor = node.getPrev( );
		Node<E> successor = node.getNext( );
		predecessor.setNext(successor);
		successor.setPrev(predecessor);
		size--;
		return node.getElement( );
	}

}


### LinkedList:

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public class LinkedList<E> implements Stack<E>, Queue<E>{

	/**
	 * Inner class
	 * @author tuxtor
	 *
	 * @param <E>
	 */
	private static class Node<E>{
		private E element; //Valor
		private Node<E> next; //Puntero en la lista
		
		public Node(E element, Node<E> next) {
			super();
			this.element = element;
			this.next = next;
		}
		public E getElement() {
			return element;
		}
		public Node<E> getNext() {
			return next;
		}
		public void setNext(Node<E> next) {
			this.next = next;
		}
	}

	private Node<E> head = null;
	private Node<E> tail = null;
	
	private int size = 0;
	
	public int size() {return size;}
	
	public boolean isEmpty() { return size == 0;}
	
	public E first() {
		if (isEmpty()) return null;
		return head.getElement();
	}
	
	public E last() {
		if (isEmpty()) return null;
		return tail.getElement();
	}
	
	public void addFirst(E e) {
		head = new Node<>(e, head);
		if (size == 0) tail = head;
		size++;
	}
	
	public void addLast(E e) {
		Node<E> newest = new Node<>(e, null);
		if(isEmpty())
			head = newest;
		else
			tail.setNext(newest);
		tail = newest;
		size++;
	}
	
	public E removeFirst() {
		if (isEmpty()) return null;
		E response = head.getElement();
		head = head.getNext( );
		size--;
		if(size == 0) tail = null;
		return response;
	}

	@Override
	public void push(E e) {
		this.addFirst(e);
		
	}

	@Override
	public E top() {
		
		return this.first();
	}

	@Override
	public E pop() {
		
		return this.removeFirst();
	}

	@Override
	public void enqueue(E e) {
		this.addLast(e);
		
	}

	@Override
	public E dequeue() {
		return removeFirst();
	}
	
	
}

### Clase Queue

*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public interface Queue <E> {
    
    /**
	 * Returns queue elements count
	 * @return number of elements in stack
	 */
	int size();
	
	/**
	 * Checks if queue is empty
	 * @return true if queue is empty, false otherwise
	 */
	boolean isEmpty();
	
	/**
	 * Inserts an element in the queue
	 * @param e element to be inserted
	 */
	void enqueue(E e);
	
	/**
	 * Retrieves the first element of the queue without remotion
	 * @return First queue element (null if empty)
	 */
	E first();
	
	/**
	 * Retrieves the first element of the queue removing it
	 * @return First stack element (null if empty)
	 */
	E dequeue();
    
}



### Stack

/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public interface Stack <E> {
    
    /**
	 * Returns stack elements count
	 * @return number of elements in stack
	 */
	int size();
	
	/**
	 * Checks if stack is empty
	 * @return true if stack is empty, false otherwise
	 */
	boolean isEmpty();
	
	/**
	 * Inserts an element in the stack
	 * @param e element to be inserted
	 */
	void push(E e);
	
	/**
	 * Retrieves the last element of the stack without remotion
	 * @return Last stack element (null if empty)
	 */
	E top();
	
	/**
	 * Retrieves the last element of the stack removing it
	 * @return Last stack element (null if empty)
	 */
	E pop();
    
}



### Tree


/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package pkg2doproyecto;

/**
 *
 * @author lupita
 */
public interface Tree<E> extends Iterable<E> {
	Position<E> root();
	Position<E> parent(Position<E> p) throws IllegalArgumentException;
	Iterable<Position<E>> children(Position<E> p) throws IllegalArgumentException;
	int numChildren(Position<E> p) throws IllegalArgumentException;
	boolean isInternal(Position<E> p) throws IllegalArgumentException;
	boolean isExternal(Position<E> p) throws IllegalArgumentException;
	boolean isRoot(Position<E> p) throws IllegalArgumentException;
	int size();
	boolean isEmpty();
	
	Iterable<Position<E>> positions();
}




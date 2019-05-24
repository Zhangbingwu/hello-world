package 我的容器;
public class MyCollection<E> {
	private Object[] elementDate;
	private int size;
	private static final int DEFALT_CAPACITY = 10;
	
	public void MyArrayList() {
		elementDate = new Object[DEFALT_CAPACITY];
	}
	
	public void MyArrayList(int capacity) {
		if(capacity<0) {
			throw new RuntimeException("容器数量不能为负数："+capacity);
		}else if(capacity==0) {
			capacity=DEFALT_CAPACITY;
		}else
			elementDate = new Object[capacity];
	}

	public void add(E e) {
		if(size==elementDate.length) {
			Object[] newArray = new Object[elementDate.length+(elementDate.length>>1)];
			System.arraycopy(elementDate, 0, newArray, 0, elementDate.length);
			elementDate = newArray;
		}
		elementDate[size++] = e;
	}
	
	@Override
	public String toString() {
		StringBuilder sb = new StringBuilder();
		//[a,b,c]
		sb.append("[");

		for(int i=0;i<size;i++) {
			sb.append(elementDate[i]);	
			if(i!=size-1) {
				sb.append(",");
			}
		}

		sb.append("]");
		return sb.toString();
	}
	
	public int length() {
		return elementDate.length;
	}
	//set,get方法；
	public E get(int index) {
		checkRange(index);
		return (E)elementDate[index];
	}
	public void set(E element,int index) {
		checkRange(index);
		elementDate[index]=element;
		
	}
	//索引范围判断;
	public void checkRange(int index) {
		if(index<0||index>elementDate.length-1) {
			throw new RuntimeException("超出索引范围："+index);
		}
	}
	//增加remove方法；
	public void remove(E element) {
		for(int i=0;i<elementDate.length;i++) {
			if(element.equals(get(i))) {
				remove(i);
			}
		}
	}
	//a,b,c,d,e,f,g,h
	//a,b,c,e,f,g,h 
	public void remove(int index) {
		checkRange(index);
		int numMoved = elementDate.length-index-1;
		if(numMoved>0) {
			System.arraycopy(elementDate, index+1, elementDate, index ,numMoved);
		}
			elementDate[--size]=null;
	}
	//容器size；
	public int size() {
		return size;
	}
	//判断是否为空；
	public boolean isEmpty() {
		if(size==0)
			return true;
		else
			return false;
	}
	public static void main(String[] args) {
		MyCollection<String> m = new MyCollection<>();
		m.MyArrayList(20);
		for(int i=0;i<11;i++) {
			char x =(char)('a'+i);
			m.add(x+"");
		}

		System.out.println(m);
		m.remove(0);
		System.out.println(m);
		System.out.println(m.isEmpty());
		System.out.println(m.size());
	}
}

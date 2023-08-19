# 一、数据结构与算法基础

## 1.为什么要学数据结构

1.写出性能更好的程序

2.学习新技术的速度

3.站在更高的角度和思维去考虑代码

4.伴随一整个程序员生涯

## 2.用什么语言来学数据结构与算法

![image-20221112001429669](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20221112001429669.png)

## 3.课程大纲

![uTools_1668183406320](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668183406320.png)

### 1.第一阶段大纲

![uTools_1668183443354](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668183443354.png)

## 4.什么是一个好的算法

1.正确性,可断线，健壮性

2.时间复杂度:程序执行的次数

3.空间复杂度:程序解决问题需要开辟的空间

```java
/*
	1.大O表示法(渐近时间度):忽略常数，系数，低阶
		例如:9>>O(1)
			2n+3>>O(n)
			n^2+2n>>O(n^2)
			4n^3+3n^2>>O(n^3)
			log2^n>>O(logn)
			注意对数:
			logn+n>>O(n)
			logn+nlogn>>O(nlogn)
				所以例如一个for循环其实就是执行n次一般，关注for循环里面的语句
        
		我们关注的是增长的趋势	
		多个数据规模的情况，例如俩个for循环的算法的时间复杂度是O(n+k)
		
	在算法中我们还是比较在意时间复杂度,因为现在的硬件都比较好。
*/
```

**对数阶的细节：**

![uTools_1668269926941](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668269926941.png)

**大O表示判断算法好坏的依据:**

![uTools_1668270378100](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668270378100.png)

**例子：用递归算法实现斐波那契数时的时间复杂度分析**

![uTools_1668303284761](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668303284761.png)

## 5.算法的优化方向

1.用尽量少的存储空间

2.用尽量少的执行步骤

3.空间换时间(PC端内存大)    时间换空间(移动端内存大)

## 6.斐波那契数列的数学解法

![uTools_1668336835767](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668336835767.png)

# 二、什么是数据结构？

## 1.线性表(ArrayList)

![uTools_1668333562626](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668333562626.png)

### 1.数组

![uTools_1668333817564](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668333817564.png)

在很多语言中，数组都是无法动态修改容量的。 我们利用动态数组来解决这个问题。

![uTools_1668334054550](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668334054550.png)

为了使得动态数组可以存储多种数据类型，我们可以使用泛型实现动态数组。

![uTools_1668390339816](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668390339816.png)

**对象数组**

![uTools_1668390573355](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668390573355.png)

对象数组的内存空间申请是不确定的，数组里面存放的地址值，地址值指向内存空间。

数组销毁的时候先销毁的是地址，然后才是存放对象数据的内存空间

**关于new int和new object进行clear的细节差别**

new int 进行clear的时候只需要另size= 0； 因为new int 数组不会像对象数组一样为对象另外开辟空间存储数据

new object要给数组元素赋值null,这样就访问不到了

![uTools_1668427233583](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668427233583.png)

**正确代码:**

![uTools_1668427828994](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668427828994.png)

不能直接用elements = null； 这样的意思是整个数组都进行销毁，下次添加内容还要重新开辟地址。 (就是object连接的数组首地址直接断掉了)

使用for循环为每一个数组元素赋值为null，这样下次使用这个数组可以直接赋值。

**remove**

![uTools_1668427996513](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1668427996513.png)

**关于==和equals**

**在java中 ==对于基本数据类型，比较的是其值；对于对象的引用，比较的是对象的内存地址；**

**我们可以重写equals方法来定义判断两者之间如何相等，如果没有对equals方法进行重写，则比较的是引用类型的变量所指向的对象的内存地址；像integer这种类内部的equals方法都是重写过的，比较的是数值，所以不影响使用。**

**所以我们创建泛型数组时进行判断的时候用equals方法比较通用，这样对象类型可以比较，基本数据类型也可以使用封装类进行比较，int就用integer比较**

**如何做到基本数据类型和对象类型都能存放**

ArrayList<Object> array = nwe ArrayList<>();   //Object任何类都继承它

**E**

E只是实现泛型大家都喜欢使用这个   public class ArrayList<E> {} 在这里写的都要写<E>

### 2.完整的动态数组代码

```java
package com.mj;

@SuppressWarnings("unchecked")
public class ArrayList<E> {
	/**
	 * 元素的数量
	 */
	private int size;
	/**
	 * 所有的元素
	 */
	private E[] elements;
	//数组初始值空间设为10
	private static final int DEFAULT_CAPACITY = 10;
    //程序返回-1
	private static final int ELEMENT_NOT_FOUND = -1;
	
	public ArrayList(int capaticy) {
        	//传进来的数组长度小于10赋值为10,大于10就取传进来的数
		capaticy = (capaticy < DEFAULT_CAPACITY) ? DEFAULT_CAPACITY : capaticy;
		elements = (E[]) new Object[capaticy];
	}
		//无参的方法,用户不设置长度的时候默认取10
	public ArrayList() {
		this(DEFAULT_CAPACITY);
	}
	
	/**
	 * 清除所有元素
	 */
	public void clear() {
        //使用for循环为每一个数组元素赋值为null，这样下次使用这个数组可以直接赋值。
		for (int i = 0; i < size; i++) {
			elements[i] = null;
		}
        //size赋值为0,这样就找不到数组首地址了,相当于清除了数组
		size = 0;
	}

	/**
	 * 元素的数量
	 * @return
	 */
	public int size() {
		return size;
	}

	/**
	 * 是否为空
	 * @return
	 */
	public boolean isEmpty() {
		 return size == 0;
	}

	/**
	 * 是否包含某个元素
	 * @param element
	 * @return
	 */
	public boolean contains(E element) {
        //element值不等于-1时表示元素包含在数组中
		return indexOf(element) != ELEMENT_NOT_FOUND;
	}

	/**
	 * 添加元素到尾部
	 * @param element
	 */
	public void add(E element) {
        //这里调用了下面那个方法,直接在size处添加元素,因为数组最后一个元素的下标是size-1
		add(size, element);
	}

    /**
	 * 在index位置插入一个元素
	 * @param index
	 * @param element
	 */
	public void add(int index, E element) {
        //判断传入的index是否越界
        //这里允许等于size,等于size就是在数组的最后插入元素
		rangeCheckForAdd(index);
		//数组的长度加1,调用这个方法看是否需要扩容
		ensureCapacity(size + 1);
		//把所有的元素往后移动,把index这个位置空出来
		for (int i = size; i > index; i--) {
			elements[i] = elements[i - 1];
		}
        //这里不用担心空值的情况，空值也会直接存在空出来的index这个位置
		elements[index] = element;
        //数组长度+1
		size++;
	}
    
	/**
	 * 获取index位置的元素
	 * @param index
	 * @return
	 */
	public E get(int index) {
         //判断传入的index是否越界
		rangeCheck(index);
		return elements[index];
	}

	/**
	 * 设置index位置的元素
	 * @param index
	 * @param element
	 * @return 原来的元素ֵ
	 */
	public E set(int index, E element) {
         //判断传入的index是否越界
		rangeCheck(index);
		//记录index这个位置原来的元素
		E old = elements[index];
        //将新的元素直接覆盖
		elements[index] = element;
		return old;
	}

	/**
	 * 删除index位置的元素
	 * @param index
	 * @return
	 */
	public E remove(int index) {
          //判断传入的index是否越界
		rangeCheck(index);
		//记录index这个位置原来的元素
		E old = elements[index];
		for (int i = index + 1; i < size; i++) {
            //数组元素前移动
			elements[i - 1] = elements[i];
		}
   
      	/*
      	 *这里相当于 size--;elements[size] = null;  size-1以后赋值为null
      	 *这里最后一个元素必须进行清空,因为未来会有一种情况是要删除倒数第二个元素,而倒数第二个元素是引用最后一个元素的地址,最后一个元素还有值就一直清空不了
         *
         */
		elements[--size] = null;
		return old;
	}

	/**
	 * 查看元素的索引
	 * @param element
	 * @return
	 */
	public int indexOf(E element) {
        	//传进来的element为空值的时候
		if (element == null) {  // 1
			for (int i = 0; i < size; i++) {
				if (elements[i] == null) return i; 
			}
		} else {
			for (int i = 0; i < size; i++) {
                	//elenmt是传进来的元素，此时不为空直接放在前面不会出现空指针异常报错 elements[i]是每一个数组元素
				if (element.equals(elements[i])) return i; // n
			}
		}
		return ELEMENT_NOT_FOUND;
	}
	
//	public int indexOf2(E element) {
//		for (int i = 0; i < size; i++) {
//			if (valEquals(element, elements[i])) return i; // 2n
//		}
//		return ELEMENT_NOT_FOUND;
//	}
//	
//	private boolean valEquals(Object v1, Object v2) {
//		return v1 == null ? v2 == null : v1.equals(v2);
//	}
	
	/**
	 * 保证要有capacity的容量
	 * @param capacity
	 */
	private void ensureCapacity(int capacity) {
        //旧的数组长度进行记录
		int oldCapacity = elements.length;
        //长度够用时不用扩容
		if (oldCapacity >= capacity) return;
		
		// 新容量为旧容量的1.5倍
		int newCapacity = oldCapacity + (oldCapacity >> 1);
        //扩容以后的数组
		E[] newElements = (E[]) new Object[newCapacity];
		for (int i = 0; i < size; i++) {
            //旧的数组元素添加进扩容后的数组
			newElements[i] = elements[i];
		}
		elements = newElements;
		
		System.out.println(oldCapacity + "扩容为" + newCapacity);
	}
	
   //以下这部分是公用的方法,所以直接提取出来,接下来需要用直接调用就行
    
    //返回index和size的方法
	private void outOfBounds(int index) {
		throw new IndexOutOfBoundsException("Index:" + index + ", Size:" + size);
	}
	
    //正常情况下数组越界的判断
	private void rangeCheck(int index) {
		if (index < 0 || index >= size) {
            //这里index大于等于size就是越界了,因为数组最后一个元素的下标是size-1
			outOfBounds(index);
		}
	}
	
    //add时进行的数组越界判断
	private void rangeCheckForAdd(int index) {
		if (index < 0 || index > size) {
            //这里允许index等于size,等于size就是在数组的最后插入元素
			outOfBounds(index);
		}
	}
	
    //字符串拼接
	@Override
	public String toString() {
		// size=3, [99, 88, 77]
		StringBuilder string = new StringBuilder();
		string.append("size=").append(size).append(", [");
		for (int i = 0; i < size; i++) {
			if (i != 0) {
				string.append(", ");
			}
			
			string.append(elements[i]);
			
//			if (i != size - 1) {
//				string.append(", ");
//			}
		}
		string.append("]");
		return string.toString();
	}
}

```

### 3.编程的利用效率

**我们进行编程的时候，记住能循环利用的留下，不能循坏利用的销毁**

## 2.链表(Linked List)

![uTools_1670333595853](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670333595853.png)

![uTools_1670336298823](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670336298823.png)

![uTools_1670338048022](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/uTools_1670338048022.png)

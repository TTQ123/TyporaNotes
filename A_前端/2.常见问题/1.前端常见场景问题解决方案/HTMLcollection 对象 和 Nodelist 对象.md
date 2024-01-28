HTMLCollection是比较HTML发展早期的对象模型，只能包含HTML元素，而NodeList是比较新的模型，相比HTMLCollection更加完善

可以获取HTMLCollection的方法

![image-20231019163011249](https://ttqblogimg.oss-cn-beijing.aliyuncs.com/image-20231019163011249.png)

获取NodeList  

document.querySelector()和document.querySelectorAll()

HTMLCollection的缺点就在于我们在页面操作dom，它的数组是实时更新的，这样会导致很多意想不到的情况，有时候我们会把dom暂存在一个变量上。
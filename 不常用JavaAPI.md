##### list.add的重载形式：

list.add(int index, E element);

用于实现排序，如置顶等需求。

置顶使用：list.add(0, obj);

原理是复制数组，间接实现下标后的元素往后移动一位。
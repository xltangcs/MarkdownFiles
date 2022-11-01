#### vector
```c++
#include <vector>     //头文件
vector<int> a;
vector<vector<int>> a;   //二维数组
a.resize(n);
a.resize(10,2); 
a.back();
a.front();
a.clear(); 
a.empty();
a.pop_back();
a.push_back(5);
a.size();
a.swap(b); 
a==b;
a.assign(b.begin(), b.begin()+3); 
a.assign(4,2);
a.erase(a.begin()+1,a.begin()+3); //删除，时间消耗高
a.insert(a.begin()+1,5); 
a.capacity();
a.reserve(100); 
```

#### set
```c++
#include <set>
Set<int > a;
begin();
end();
clear();
count();
empty();
equal_range();
erase();
find()–返回一个指向被查找到元素的迭代器
get_allocator()–返回集合的分配器
insert()–在集合中插入元素
lower_bound()–返回指向大于（或等于）某值的第一个元素的迭代器
key_comp()–返回一个用于元素间值比较的函数
max_size()–返回集合能容纳的元素的最大限值
rbegin()–返回指向集合中最后一个元素的反向迭代器
rend()–返回指向集合中第一个元素的反向迭代器
size()–集合中元素的数目
swap()–交换两个集合变量
upper_bound()–返回大于某个值元素的迭代器
value_comp()–返回一个用于比较元素间的值的函数
set的遍历
for (set<int>::iterator it=myset.begin(); it!=myset.end(); ++it)
cout << *it<<endl;

```


#### unordered_map


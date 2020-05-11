### 简单的进程内缓存管理包

**本工具只适合进程内少量数据缓存，开发者需评估实际存储数据的内存占用 ，大型数据缓存请使用主流缓存服务，如redis等**

#### Features
- 采用interfac{}存储数据，可存储任意go数据结构
- 简单的LRU淘汰机制
- 可自定义存储数据数量（只能控制存储元素数量，不能控制内存占用）


#### Usage
```shell
go get -u github.com/kasiss-liu/go-memcache
```

```go
cs := NewCacheStore(10, 1)
fmt.Println("Cap:",cs.Cap())
for i := 0; i < 15; i++ {
    cs.Save(fmt.Sprintf("hello%d", i), fmt.Sprintf("world%d", i))
}
fmt.Println("Len:",cs.Len())
fmt.Println("hello0:",cs.Get("hello0"))
fmt.Println("hello14:",cs.Get("hello14"))

fmt.Println("Save:",cs.Save("mapvalue", map[string]string{"1": "aa"}))
fmt.Println("mapvalue",cs.Get("mapvalue"))

/**
Cap: 10
Len: 10
hello0: 
hello14: world14
Save: true
mapvalue: map[1:aa]
*/
```
# 数据存储

GoMicro 为我们提供了 \`github.com/micro/go-micro/store\` 包，里面包含了几种常见的数据存储方案。

本节我们将会详细讲解每一种存储的源码实现。

## 数据存储契约

```go
type Store interface {
	
	// Init initialises the store. It must perform any required setup on the backing storage implementation and check that it is ready for use, returning any errors.
	Init(...Option) error
	
	// Options allows you to view the current options.
	Options() Options
	
	// Read takes a single key name and optional ReadOptions. It returns matching []*Record or an error.
	Read(key string, opts ...ReadOption) ([]*Record, error)
	
	// Write() writes a record to the store, and returns an error if the record was not written.
	Write(r *Record, opts ...WriteOption) error
	
	// Delete removes the record with the corresponding key from the store.
	Delete(key string, opts ...DeleteOption) error
	
	// List returns any keys that match, or an empty list with no error if none matched.
	List(opts ...ListOption) ([]string, error)
	
	// Close the store
	Close() error
	
	// String returns the name of the implementation.
	String() string
}
```




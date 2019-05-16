# About

一个用来管理数据的库，可以设置观察者监听某个数据的变化，当生命周期销毁后自动移除观察者
<br>
关于生命周期分发的库，可以参考[这里](https://github.com/zj565061763/flib_lifecycle)

## Install
* git
```
  flib_live_data:
    git:
      url: git://github.com/zj565061763/flib_live_data
      ref: 1.0.0
```

* pub
```
  dependencies:
    flib_live_data: ^1.0.0
```

## Example
```dart
// 创建LiveData
final FLiveData<int> number = FLiveData(0);

// 赋值
number.value = 1;

// 添加观察者，监听值的变化
number.addObserver((value) {}, this);
```

```dart
  /// 添加观察者
  ///
  /// - [observer] 观察者
  /// - [lifecycleOwner] 观察者要绑定的生命周期
  ///   1. [lifecycleOwner] != null，则[FLifecycleEvent.onDestroy]事件后，会自动移除观察者
  ///   2. [lifecycleOwner] == null，则不会自动移除观察者
  /// - [notifyAfterAdded] 添加观察者之后，如果[_value]不为null的话是否立即通知当前添加的观察者，默认true
  /// - [notifyLazy] 延迟通知策略，是否生命周期状态大于等于[FLifecycleState.started]之后才通知，默认false
  void addObserver(
    FLiveDataObserver<T> observer,
    FLifecycleOwner lifecycleOwner, {
    bool notifyAfterAdded = true,
    bool notifyLazy = false,
  })

  /// 移除观察者
  ///
  /// - [observer] 要移除的观察者
  void removeObserver(Function observer)
```
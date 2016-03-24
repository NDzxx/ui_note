# UIViewController


## UIViewController（控制器）的认识
- 一个控制器负责管理一个大界面
- 控制器负责界面的创建、事件处理等

## 类扩展
- 格式
```objc
@interface 类名()
/** 属性、方法的声明 */
@end
```
- 作用
    - 为某个类增加额外的属性和方法声明
    - 可以写在.h和.m文件中
详细参考oc_note的类扩展项目

## 项目属性
- Product Name
    - 软件名称、产品名称、项目名称
- Organization Name
    - 公司名称、组织名称
- Organization Identifier
    - 公司的唯一标识
    - 一般是公司域名的反写，比如com.520it
- Bundle Identifier
    - 软件的唯一标识
    - 一般是Organization Identifier + Product Name
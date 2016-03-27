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
    - 一般是公司域名的反写，比如cn.com.nd
- Bundle Identifier
    - 软件的唯一标识
    - 一般是Organization Identifier + Product Name  
    
##UIView的常见属性
- NSArray *subviews
    - 所有的子控件
    - 数组元素的顺序决定着子控件的显示层级顺序（下标越大的，越显示在上面）

- @property(nonatomic,readonly,copy)  NSArray *subviews;
 - 获得自己的所有子控件对象

- @property(nonatomic)  NSInteger tag;  
 - 控件的ID(标识)，父控件可以通过tag来找到对应的子控件

- @property(nonatomic)  CGAffineTransform transform;  
 - 控件的形变属性(可以设置旋转角度、比例缩放、平移等属性)

- @property(nonatomic) CGRect frame;
 - 控件矩形框在父控件中的位置和尺寸(以父控件的左上角为坐标原点)

- @property(nonatomic) CGRect bounds;
 - 控件矩形框的位置和尺寸(以自己左上角为坐标原点，所以bounds的x、y一般为0)

- @property(nonatomic) CGPoint center;
 - 控件中点的位置(以父控件的左上角为坐标原点)

## UIView的常见方法
- addSubview:
    - 添加一个子控件
    - 使用这个方法添加的子控件会被塞到subviews数组的最后面
- 可以使用下面的方法调整子控件在subview数组中的顺序

```objc
// 将子控件view插入到subviews数组的index位置
- (void)insertSubview:(UIView *)view atIndex:(NSInteger)index;

// 将子控件view显示到子控件siblingSubview的下面
- (void)insertSubview:(UIView *)view belowSubview:(UIView *)siblingSubview;
// 将子控件view显示到子控件siblingSubview的上面
- (void)insertSubview:(UIView *)view aboveSubview:(UIView *)siblingSubview;

// 将子控件view放到数组的最后面，显示在最上面
- (void)bringSubviewToFront:(UIView *)view;
// 将子控件view放到数组的最前面，显示在最下面
- (void)sendSubviewToBack:(UIView *)view;
```
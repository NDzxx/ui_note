## 九宫格计算思路
- 利用控件的索引index计算出控件所在的行号和列号
- 利用列号计算控件的x值
- 利用行号计算控件的y值  
```
// 每一个商品的尺寸
    CGFloat shopW = 50;
    CGFloat shopH = 70;
    
    // 一行的列数
    int cols = 4;
    
    // 每一列之间的间距
    CGFloat colMargin =
    (self.shopsView.frame.size.width 
    - cols * shopW) / (cols - 1);
    // 每一行之间的间距
    CGFloat rowMargin = 10;
    
    // 创建一个父控件（整体：存放图片和文字）
    UIView *shopView = [[UIView alloc] init];
    shopView.backgroundColor =
    [UIColor redColor];
    
    // 商品的索引 子控件的个数
     NSUInteger index = self.shopsView.subviews.count;
    
    // 商品的x值 索引%列数
    NSUInteger col = index % cols;
    CGFloat shopX = col * (shopW + colMargin);
    
    // 商品的y值  索引/列数
    NSUInteger row = index / cols;
    CGFloat shopY = row * (shopH + rowMargin);
    
    shopView.frame = CGRectMake(shopX, shopY, shopW, shopH);
    [self.shopsView addSubview:shopView];
```  
## HUD
- 其他说法：指示器、遮盖、蒙板
- 半透明HUD的做法
    - 背景色设置为半透明颜色：设置背景色半透明
    - 做法：![1](Snip20160405_1.png)->![2](Snip20160405_2.png)

## 定时任务
- 方法1：performSelector

```objc
// 1.5s后自动调用self的hideHUD方法
[self performSelector:@selector(hideHUD) withObject:nil afterDelay:1.5];
```
- 方法2：GCD

```objc
dispatch_after(dispatch_time(DISPATCH_TIME_NOW,  
(int64_t)(1.5 * NSEC_PER_SEC)), dispatch_get_main_queue(),  
^{
    // 1.5s后自动执行这个block里面的代码
    self.hud.alpha = 0.0;
});
```
- 方法3：NSTimer

```objc
// 1.5s后自动调用self的hideHUD方法
[NSTimer scheduledTimerWithTimeInterval:1.5   
target:self   
selector:@selector(hideHUD)   
userInfo:nil 
repeats:NO];
// repeats如果为YES，意味着每隔1.5s都会调用一次self的hidHUD方法
```
##加载plist
- plist文件和资源文件丢在supporting file文件夹内  
- 使用  
正确加载文件方式：  

 ![plist_load](添加文件到项目时的正确选择.png)
 ```objc  
 
 NSBundle *bundle = [NSBundle mainbundle]//主资源包
 // 利用mainBundle获得plist文件在主资源包中的全路径
    NSString *file = 
    [bundle pathForResource:@"shops" ofType:@"plist"];
    // 传递的是文件的全路径
    self.shops = [NSArray arrayWithContentsOfFile:file];
 ```
- 不可以使用info.plist作为文件名，它是系统默认使用的

## 常见问题
- 项目里面的某个.m文件无法使用
    - 检查：Build Phases -> Compile Sources
- 项目里面的某个资源文件（比如plist、音频等）无法使用
    - 检查：Build Phases -> Copy Bundle Resources

##懒加载
- 使用时候才去加载对应代码，实际就是重载get方法  

```objc  
// 加载plist数据（比较大）
// 懒加载：用到时再去加载，而且也只加载一次
- (NSArray *)shops
{
    if (_shops == nil)  //此处同意不可调用self.shop
    {
        NSString *file = [[NSBundle mainBundle]  
        pathForResource:@"shops" ofType:@"plist"];
        self.shops = [NSArray arrayWithContentsOfFile:file];
//        _shops = [NSArray arrayWithContentsOfFile:file];
//        [self setShops:[NSArray arrayWithContentsOfFile:file]];
    }
    return _shops; //注意此处不可写为self.shop，  
    //否则会造成循环引用,因为此处self.shop调用的是get方法
}
  
  加载数据使用时候调用
  #pragma mark 添加
-(void)add
{
  // 获得index位置对应的商品数据
    NSDictionary *shop = self.shops[index];
}

```
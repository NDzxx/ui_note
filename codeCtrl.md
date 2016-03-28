# 使用代码创建控件

- sel的使用  
用来选择方法  
详细内存参考ocnote block和selctor章节
例子：  
```objc
 [self addButtonWithImage:@"add" 
       highImage:@"add_highlighted" 
       disableImage:@"add_disabled" 
       frame:CGRectMake(30, 30, 50, 50) 
       tag:10 
       action:@selector(add)];//注意此处的sel
```
- 封装控件代码  
 - viewDidLoad 视图加载后所在的操作  
 - 不应该在viewDidLoad方法中写太多冗余代码，应该加以封装  
见例子  

```objc

#pragma mark 添加按钮
- (void)addButtonWithImage:(NSString *)image 
                            highImage:(NSString *)highImage 
                            disableImage:(NSString *)disableImage 
                            frame:(CGRect)frame 
                            tag:(NSInteger)tag 
                            action:(SEL)action
{
    // 创建按钮
    UIButton *btn = [[UIButton alloc] init];
    // 设置背景图片
    [btn setBackgroundImage:[UIImage imageNamed:image] forState:UIControlStateNormal];
    [btn setBackgroundImage:[UIImage imageNamed:highImage] 
         forState:UIControlStateHighlighted];
    [btn setBackgroundImage:[UIImage imageNamed:disableImage] 
         forState:UIControlStateDisabled];
    // 设置位置和尺寸
    btn.frame = frame;
    // 监听按钮点击
    [btn addTarget:self action:action forControlEvents:UIControlEventTouchUpInside];
    // 绑定tag标记
    btn.tag = tag;
    // 添加按钮
    [self.view addSubview:btn];
}
```
- 控件不显示也不报错
  - 缺失了frame
  -  补充类似```objc iconView.frame = CGRectMake(0, 0, 50, 50);```的代码
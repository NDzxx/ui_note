# 使用代码创建控件

sel的使用  
用来选择方法  
例子：  
```objc
 [self addButtonWithImage:@"add" 
       highImage:@"add_highlighted" 
       disableImage:@"add_disabled" 
       frame:CGRectMake(30, 30, 50, 50) 
       tag:10 
       action:@selector(add)];
```

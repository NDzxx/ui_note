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

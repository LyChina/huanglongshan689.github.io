
```
//灰1左间距、高度、垂直位置（因为和红1底部对齐）是确定的，添加约束
[gray1 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.height.mas_equalTo(20);
        make.leading.equalTo(self.view.mas_leading).offset(0);
        make.bottom.equalTo(red1.mas_bottom);
    }];

//红1，宽高、左间距、底间距是确定的，添加约束
    [red1 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.width.mas_equalTo(100);
        make.height.mas_equalTo(50);
        make.left.equalTo(gray1.mas_right);
        make.bottom.equalTo(self.view.mas_bottom).offset(-50);
    }];
//灰2，左间距、高度、垂直位置是确定的，宽度要与灰1一致，是为了能均匀填充，添加约束
    [gray2 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.height.and.width.equalTo(gray1);
        make.leading.equalTo(red1.mas_right);
        make.bottom.equalTo(red1.mas_bottom);
    }];
//红2，宽高、左间距、底间距是确定的，添加约束
    [red2 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.height.and.width.equalTo(red1);
        make.leading.equalTo(gray2.mas_right);
        make.bottom.equalTo(red1.mas_bottom);
    }];
//灰3，左间距、右间距、高度、垂直位置是确定的，添加约束
    [gray3 mas_makeConstraints:^(MASConstraintMaker *make) {
        make.height.and.width.equalTo(gray1);
        make.leading.equalTo(red2.mas_right);
        make.trailing.equalTo(self.view.mas_right);
        make.bottom.equalTo(red1.mas_bottom);
    }];
大家看了上面的讲解后，会发现三个灰色方块都没有设置固定的宽
但是它们三个都等宽，红色方块又是固定的，那么在这5个View间距都为0的情况下，灰色方块不就会去挤压红色方块，直到灰色方块宽度相等，那么红色方块也处在了应有的位置么
这就是我想说的相对，红色方块宽度是固定的，那么水平方向上的间距就需要剩下的三个灰色方块去填充，当界面横屏时，三个灰色方块为了相对自身宽度要相同，相对红色边界，self.view边界，间距保持为0，那么就得牺牲自身宽度的稳定，去维持这些相对的约束
希望我这些话能帮助大家更深刻的理解约束，更多的东西需要大家去做项目慢慢体会
第三个例子
最后这个例子是老例子了，我想给大家看看其实Masonry做动画也和其他的Autolayout方法一样，但是添加约束的代码却非常的少，可以和我之前的另一篇文章比较一下
里面的约束我就不讲解了，看了上面的代码，下面的约束对你来说肯定是小菜一碟
约束代码
 UIView *redView = [[UIView alloc]init];
    redView.backgroundColor = [UIColor redColor];
    [self.view addSubview:redView];
    UIView *greenView = [[UIView alloc]init];
    greenView.backgroundColor = [UIColor greenColor];
    [self.view addSubview:greenView];
    UIView *blueView = [[UIView alloc]init];
    blueView.backgroundColor  = [UIColor blueColor];
    [self.view addSubview:blueView];

    [redView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.equalTo(self.view.mas_left).offset(20);
        make.bottom.equalTo(self.view.mas_bottom).offset(-20);
        make.width.equalTo(self.view.mas_width).multipliedBy(0.2);
        make.height.equalTo(self.view.mas_height).multipliedBy(0.2);
    }];
    [greenView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.equalTo(redView.mas_right).offset(20);
        make.bottom.equalTo(self.view.mas_bottom).offset(-20);
        make.width.equalTo(self.view.mas_width).multipliedBy(0.2);
        make.height.equalTo(self.view.mas_height).multipliedBy(0.2);
    }];
    [blueView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.left.equalTo(greenView.mas_right).offset(20);
        make.bottom.equalTo(self.view.mas_bottom).offset(-20);
        make.width.equalTo(self.view.mas_width).multipliedBy(0.2);
        make.height.equalTo(self.view.mas_height).multipliedBy(0.2);
        make.left.equalTo(redView.mas_right).offset(20).priority(250);
    }];

```
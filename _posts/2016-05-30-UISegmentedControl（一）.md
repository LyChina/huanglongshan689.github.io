---
category:"技术笔记"
title:"2016-05-30-UISegmentedControl"
tags:"IOS","UISegmentedControl"
---

#2016-05-30-UISegmentedControl（一）

先附上苹果开发文档的相关链接[UISegmentedControl Class Reference](https://developer.apple.com/library/ios/documentation/UIKit/Reference/UISegmentedControl_Class/)，一下内容都为参考文档得来。
##概述
+ 1 UISegmentedControl对象是一个由多个分段构成的水平控制水平，每个分段功能都有各自的按钮，每个分段控制都提供紧凑的方式去将一系列的控制组织在一起。


---
___
***

 proportionally    [prəu'pɔ:ʃənəli]<br>
	adv. 成比例地；相称地，适当地<br>
	fading      ['feɪdɪŋ]<br>
	n. 褪色；衰退；凋谢<br>
	v. 使衰落（fade的ing形式）；褪色<br>
	
---
___
***
	
##代码
	NSArray *segmentArray = @[@"关",@"开",];
	  
    // 初始化UISegmentedControl
    UISegmentedControl *segment = [[UISegmentedControl alloc] initWithItems:segmentArray];
    // 设置默认选择项索引
    segment.selectedSegmentIndex = 0;
    segment.tintColor = [UIColor blueColor];
    
    // 设置在点击后是否恢复原样
    segment.momentary = NO; 
    
    
    - (void)segmentClick:(UISegmentedControl *)segmentControl{
    NSInteger idx = segmentControl.selectedSegmentIndex;
    
    NSLog(@"segmentClick%ld", idx);
    switch (idx) {
            
        case 0:   
            break;       
        case 1:
            break;
        default:
            break;  
    	}
    }

+ 2.为UISegmentedControl对象绑定方法	
	+ OC版

		```
		[segmentedControl addTarget:self
                     action:@selector(action:)
          forControlEvents:UICont
          
          rolEventValueChanged];
		```
	+ swift版
		```
		segmentedControl.addTarget(self, action: 
		"action:", forControlEvents: .ValueChanged);
		```
		
		**configure** kən'fɪgə <br>
		vt. 安装；使成形 , 配置<br>
		
		
		**property** prɒpətɪ<br>
		n. 性质，性能；财产；所有权
		
+	3.  如果你设置一个分段控制的风格,当用户触摸它时并不会没有显示自己的选择。披露按钮总是短暂的,不会影响实际的选择。 

		 **disclosure**	dɪs'kləʊʒə<br>
		 信息纰漏<br>
		 在之前版本的iOS 3.0中,如果一个分段控制只有两段,然后像一个switch-tapping当前选中部分导致其他部分被选中。在iOS 3.0和以后,利用当前选中部分不会引起其他部分被选中.
		 在iOS v5.0之后,您可以自定义的外观分段控制使用中所列出的方法定制的外观。你可以定制所有分段控件的外观使用的代理(例如,[UISegmentedControl外观]),或者只是一个单一的控制。
		 When customizing appearance, in general, you should specify a value for the normal state of a property to be used by other states which don’t have a custom value set. Similarly, when a property is dependent on the bar metrics (on the iPhone in landscape orientation, bars have a different height from standard), you should make sure you specify a value for UIBarMetricsDefault.
		 分段控制,外观属性UIBarMetricsLandscapePhone只有尊重小分段控制的导航和工具栏,用于横向在iPhone上。
		 提供完整的定制,你需要为不同的状态组合,提供图像分配器使用setDividerImage:forLeftSegmentState:rightSegmentState:barMetrics::

```
//OC
    // Image between two unselected segments.
    [mySegmentedControl setDividerImage:image1 forLeftSegmentState:UIControlStateNormal
                      rightSegmentState:UIControlStateNormal barMetrics:barMetrics];
    // Image between segment selected on the left and unselected on the right.
    [mySegmentedControl setDividerImage:image1 forLeftSegmentState:UIControlStateSelected
                      rightSegmentState:UIControlStateNormal barMetrics:barMetrics];
    // Image between segment selected on the right and unselected on the right.
    [mySegmentedControl setDividerImage:image1 forLeftSegmentState:UIControlStateNormal
                      rightSegmentState:UIControlStateSelected barMetrics:barMetrics];
    //swift
    // Image between two unselected segments.
    mySegmentedControl.setDividerImage(myImage, forLeftSegmentState: UIControlState.Normal,
                                       rightSegmentState: UIControlState.Normal, barMetrics: UIBarMetrics.Default)
    
    // Image between segment selected on the left and unselected on the right.
    mySegmentedControl.setDividerImage(myImage, forLeftSegmentState: UIControlState.Selected,
                                       rightSegmentState: UIControlState.Normal, barMetrics: UIBarMetrics.Default)
    
    // Image between segment selected on the right and unselected on the left.
    mySegmentedControl.setDividerImage(myImage, forLeftSegmentState: UIControlState.Normal,
                                       rightSegmentState: UIControlState.Selected, barMetrics: UIBarMetrics.Default)		 
```		 	
		
		
这是用来 *演示* 的 _文本_ 哦  *斜体*   <em>斜体</em>
这是用来 **演示** 的 __文本__  **粗体**  __粗体__  <strong>粗体</strong>

这就是 ~~删除线~~

>引用内容<br>




>多行引用
>可以在每行前加 `>`




>也可以在引用中
>>使用嵌套的引用




name | age
---- | ---
LearnShare | 12
Mike |  32



|    name    | age |
| ---------- | --- |
| LearnShare |  12 |
| Mike       |  32 |


| left | center | right |
| :--- | :----: | ----: |
| aaaa | bbbbbb | ccccc |
| a    | b      | c     |


|     name     | age |             blog                |
| ------------ | --- | ------------------------------- |
| _LearnShare_ |  12 | [LearnShare](http://xianbai.me) |
| __Mike__     |  32 | [Mike](http://mike.me)          |



- [ ] Eat
- [x] Code
  - [x] HTML
  - [x] CSS
  - [x] JavaScript
- [ ] Sleep
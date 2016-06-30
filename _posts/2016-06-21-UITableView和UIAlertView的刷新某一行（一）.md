---
UITableView   	单选代理方法
UIAlertView   	代理方法
UITableViewCell	刷新某一行

---
#2016-06-21-UITableView和UIAlertView的刷新某一行（一）

##代码

+ 1. UITableView 代理方法 
``- (void)tableView:(UITableView *)tableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{``
    
    1.先取出模型<br>
    ``CZHero *hero=self.heros[indexPath.row];``<br>
    2.创建消息框UIAlertVIew<br>
    `UIAlertView *alert=[[UIAlertView alloc] initWithTitle:@"修改操作" message:@"请输入新的名称" delegate:self cancelButtonTitle:@"取消" otherButtonTitles:@"确定", nil];`<br>

    指定Alert的代理<br>
    `alert.delegate=self;`<br>
    2.1修改alert的显示属性<br>
    `alert.alertViewStyle=UIAlertViewStylePlainTextInput;`<br>
    
     UIAlertViewStyleDefault = 0,<br>
     UIAlertViewStyleSecureTextInput,<br>
     UIAlertViewStylePlainTextInput,<br>
     UIAlertViewStyleLoginAndPasswordInput<br>
     
    
    2.2为alert中的文本框赋值--得先获取alert中的文本框<br>
    `UITextField *uf= [alert textFieldAtIndex:0];`<br>
    
     Retrieve a text field at an index<br>
     检索索引的文本字段<br>
     The field at index 0 will be the first text field (the single field or the login field), the field at index 1 will be the password field.<br>
     字段索引0将成为第一个文本字段(单一字段或登录字段),字段索引1密码字段。<br>
     
    `uf.text=hero.name;`<br>
    3.将当前的indexPath.row存储到alertView的tag值中666666666666<br>
    `alert.tag=indexPath.row;`<br>
    4.显示消息框<br>
    `[alert show];<br>
}`<br>


+ 2. UIAlertVIew的代理方法<br>
``- (void) alertView:(UIAlertView *)alertView clickedButtonAtIndex:(NSInteger)buttonIndex
{``
    
     取消 0
     正确 1
     
    
    ``if (buttonIndex==1) {``<br>
        1.取出alertView中文本框的值<br>
        ``NSString *newName=[alertView textFieldAtIndex:0].text;``<br>
        2.赋值给当前被点击的行所对应的数据模型<br>
        ``NSInteger index=alertView.tag;``<br>
        ``CZHero *hero=self.heros[index];``<br>
        3.修改模型数据<br>
        ``hero.name=newName;``<br>
        4.刷新数据源<br>
        alertView会重新刷新tableView的所有数据，其实没有必要，我们应该只刷新当前被修改的这一行数据<br>
        ``[self.tableView reloadData];``<br>
        4.1只刷新当前被修改的数据行--更合理<br>
        4.1.1首先你得告诉我刷新 那一组  那一行数据  可以刷新 多行<br>
        ``NSIndexPath *indexPath=[NSIndexPath indexPathForRow:index inSection:0];``<br>
        
        [self.tableView reloadRowsAtIndexPaths:@[indexPath] withRowAnimation:UITableViewRowAnimationFade];``<br>
   ``}``<br>
``}``<br>

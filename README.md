# qt-tablewidget-
关于 父窗口，子窗口，tablewidget 的知识点
##　1.父窗口添加子窗口
  child_widget = new Widget();
  ui->verticalLayout->addWidget(child_widget);

##　2.滚动条设置
父窗口添加子窗口，子窗口很多，需要使用滚动条。
main_widget 里添加一个scrollArea控件，在scrollArea里放置一个verticalLayout(用于添加子窗口)，最后(重点)，scrollArea里还需设置一个布局（右键-布局-...）；
 ui->verticalLayout->addWidget(child_widget);
 child_widget->setFixHeight(100);  //设置窗口固定高度
 child_widget->setFixWidth(200);   //设置窗口固定宽度
 添加多个子窗口，设置宽度高度....
 ui->verticalLayput->addStretch();  
 ui->scrollArea->verticalScrollBar()->setValue(0);  初始化滚动条放顶部

 3.tablewidget界面
 ui->tableWidget->setRowCount(3) //设置3行表格(不包含表头)
 ui->tableWidget->setColumCount(3); //设置3列
 ui->tableWidget->setColumWidth(0,100); //设置0列宽
 ui->tableWidget->setRowHeight(0,30); //设置0行高
 //设置表头
 QStringList title;
 title<<tr("参数")<<tr("参数值")<<tr("备注");
 ui->tableWidget->setHorizontalHeaderLables(title);

 4.删除主窗口上所有子窗口
 QLayoutItem *child;
 while((child = ui->verticalLayout->takeAt(0))!=0){
       //setParent为NULL，防止删除页面之后界面不消失
       if(child->widget())
       {
           child->widget()->setParent(NULL);
       }
       delete child;
 }

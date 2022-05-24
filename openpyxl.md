# 打开读取表格数据
    1.打开工作簿
    workbook=load_workbook(文件名)  workbook.sheetnames获取所有工作表
    2.获取工作表
    workbook[sheet名称]  workbook.active
    3.获取表格尺寸
    sheet.dimensions
    4.获取表格内某个格子的数据
    cell=sheet['A1']  cell.value
    5.获取一系列格式
    sheet['A1':'C5']
    6.获取某列
    cols=sheet['D']
# 向excel写入内容
    1.新建一个工作簿
    workbook=workbook(....)
    2.保存
    workbook.save(...)
    3.向某个格子写入内容
    sheet['A1']='hello'        cell.value='python'
    4.使用python列表数据插入一行
    sheet.append(python列表)
    5.插入公式
    直接复制公式字符串(from openpyxl.utils import formulae)
    sheet['A1']='=sum(B5:B8)'
    6.插入一列
    sheet.insert_cols(inx=数字编号)
    7.插入多列
    sheet.insert_cols(inx=数字编号，amount=要插入几列)
    8.插入多行
    sheet.insert_rows(inx=数字编号，amount=要插入几列)
    9.删除多行、多列
    sheet.delete_rows(inx=1(包含),amount=3)
    10.移动格子(左上角原点)向下3，向右2
    sheet.move_range('A3:B5',rows=3，cols=2)
# 对sheet的操作
    1.创建sheet
    workbook.create_sheet(名称)
    2.删除一个sheet
    workbook.remove(sheet实例)
    3.复制一个sheet
    workbook.copy_worksheet(sheet实例)
    4.修改表格名称
    sheet.title
    5.冻结窗格
    sheet.freeze_panes='A2'
    6.添加筛选
    sheet.auto_filter.ref=sheet.dimensions
# 样式
    1.修改字体样式（from openpyxl.styles import Font）
    Font（name=字体名称，size=字体大小，bold=是否加粗，italic=是否斜体，color=字体颜色）
    2.获取表格中字体的样式
    cell.font.属性
    3.设置对齐样式(from openpyxl.styles import Alignment)
    alig=alignment(horizontal='center',vertical=垂直对齐方式，text_rotation=旋转角度，wrap_text=是否自动换行)
    cell.alignment=alig
    4.设置边框样式
    side=Side(style=边线样式，color=边线颜色)
    Border(left=side,top=side,right=side,bottom=side)
    cell.border=border
    5.设置填充样式(from openpyxl.styles import PatternFill)
    pattern_fill=PatternFill（fill_type=填充样式，fgcolor=填充颜色）
    cell.fill=pattern_fill
    6.设置行高和列宽
    sheet.row_dimensions[2].height=50
    sheet.column_dimensions['B'].width=50
    7.合并单元格
    sheet.merge_cells("D1:G2")
    sheet.merge_cells(start_row=1,start_column=8,end_row=2,end_column=18)
    8.取消单元格
    unmerge
ImagesetEditor
==============

C# 开发于 Visual Studio 2013

概述
==============

添加图片快速合并它们并且导出位置数据的简易工具。

支持输入格式：BMP/JPG/PNG

支持输出的格式：PNG

![preview](http://www.frimin.com/imageset.jpg "preview")

###纯文本导出：
    "image01" 228,0 76,76
    "image02" 0,0 76,76
    "image03" 52,356 76,76
    "image04" 408,228 76,76
    "image05" 408,152 76,76
	...
    
###Xml导出：
    <?xml version="1.0" encoding="utf-8"?>
    <Imageset>
      <Image Name="image01" XPos="228" YPos="0" Width="76" Height="76" />
      <Image Name="image02" XPos="0" YPos="0" Width="76" Height="76" />
      <Image Name="image03" XPos="52" YPos="356" Width="76" Height="76" />
      <Image Name="image04" XPos="408" YPos="228" Width="76" Height="76" />
      <Image Name="image05" XPos="408" YPos="152" Width="76" Height="76" />
	  ...
    </Imageset>
    
###重新编写输出接口以自定义文本格式输出
    class MyExport : IImagesetExport
    {
        void OnExportBegin(ICanvas canvas)
        {
            // 输出图片信息之前被调用
        }

        void OnExportImage(IImage image)
        {
            // 输出图片信息被调用
            // IImage 接口可获取图片的 位置、尺寸、文件路径、名称
        }

        string OnExportEnd()
        {
            // 输出图片信息结束时被调用
            // 返回的字符串为合并的图片的导出路径，如果返回 null 或 "" 则不导出。
        }
        
        MyExport()
        {
            // ...
        }
    }
    
    // ...
    
    ImagesetEditControl.Export(new MyExport());

如何使用
==============

1.在左侧 **图片组** 视图菜单中点击 **添加** 按钮来添加一个或多个图片。

2.在左侧列表框中或者右侧画布视图中选择一个或者多个图片来移动他们，如果所选的图片与其他图片重叠，则会出现八个方向的停靠箭头。光标移动到箭头上会显示要停靠到的位置。如果你选中了多个图片，则以它们组成一个更大的矩形来计算重叠。

3.选中单个图片时，画布视图的工具栏中的属性文本框可用，你可以编辑图片的名称和位置。

4.**文件** 菜单中 **保存项目** 来保存你的项目至 imageset 文件，如果项目中的图片文件处于项目文件的同目录或者子目录下时，存储的路径是相对路径。

5.使用 **文件** 菜单中 **导出** 来导出特定格式。

更新
==============

**2014.02.25** 0.1.3 -> 0.2.0

添加多国语言

**2014.02.25** 0.1.2 -> 0.1.3

添加选择多个图片进行停靠的功能

**2014.02.24** 0.1.1 -> 0.1.2

添加图片对齐功能，在选择对齐位置时会有辅助线段显示

添加"修改工作区颜色"选项并且记录至项目中

将画布尺寸的设置由选择一些固定的数值修改为输入任意数值应用

修复没有显示停靠箭头的情况下鼠标移动到其位置依然会修改光标为"手型"的情况

**2014.02.23** 0.1.0 -> 0.1.1

添加当图片移出工作区域的停靠功能

添加"始终显示图片边框"选项记录至项目中

修改工作区域边框的绘制顺序

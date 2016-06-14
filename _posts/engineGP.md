---
title: ArcGIS Engine中调用地理处理工具（gp工具）的方法与注意事项
date: 2016-06-14 16:49:06
tags: [ArcGIS,Engine]
categories: Technology
---
(以10.3版本下使用C#调用系统工具为例)

# 1. 在程序中调用gp是否需要安装Desktop软件？   #
不用安装Desktop软件，安装ArcGIS Engine运行时以后就可以调用gp工具。  

# 2. 如何查看gp工具的许可级别？  
可以直接在Desktop的帮助文档中定位到该工具的帮助页面，或者在Desktop软件中开启gp工具的执行页面，点击右下角的“tool help”按钮，也会弹出该工具的帮助页面。在帮助中，每个工具的许可级别都在页面的最上方的“License level”处标示出来。Desktop许可的Basic级别与esriLicenseProductCodeEngine许可相对应，Desktop许可的Standard级别与esriLicenseProductCodeEngineGeoDB相对应，而engine程序无法使用只有Desktop Advanced级别许可才能用的gp工具。  

# 3. 如何通过代码调用gp工具？ 
engine程序调用gp工具时使用的是相同的框架，只需要改变其中的具体的工具及参数即可，基本的框架可以使用以下代码：  
  

	public void RunGP()  
	{  
	Geoprocessor gp = new Geoprocessor { OverwriteOutput = true };  
	try  
	{  
	ESRI.ArcGIS.AnalysisTools.Buffer tool = new ESRI.ArcGIS.AnalysisTools.Buffer();  
	tool.in_features = @"D:\in.shp";  
	tool.out_feature_class = @"D:\out.shp";  
	tool.buffer_distance_or_field = "10";  
	IGeoProcessorResult2 result = gp.Execute(tool, null) as IGeoProcessorResult2;  
	}  
	catch (Exception ex)  
	{  
	MessageBox.Show(ex.Message, "GP Error");  
	}  
	finally  
	{  
	System.Text.StringBuilder sb = new System.Text.StringBuilder();  
	for (int i = 0; i < gp.MessageCount; i++)  
	sb.AppendLine(gp.GetMessage(i));  
	if (sb.Capacity > 0) MessageBox.Show(sb.ToString(), "GP Messages");  
	}  
	} 
代码中调用的是Buffer工具，如果要调用其他工具的话只需替换成对应的工具并按工具要求填写参数即可。  

# 4. 不知道参数如何填写怎么办？   
可以先在Desktop中使用想要的参数执行gp成功，然后在菜单栏-->geoprocessing-->results中打开results窗口，查看刚才执行成功的gp历史，在inputs项中查看或直接复制各参数的填写方式到代码中即可。  

# 5. 可以使用AO对象如IFeatureClass作为gp工具的参数吗？  
强烈建议不要用AO对象作为gp参数，而使用硬盘上的绝对路径或字符串作为参数。只有极少数工具可以接收AO对象作为参数，但是官方并没有公布是哪些工具，所以为了避免执行失败，最好都用绝对路径。  

# 6. SDE中的数据作为参数的话如何填写？  
填写 .sde结尾的SDE连接文件的绝对路径作为参数，如“D:\connection to oracle.sde\SDE.myFeatureClass”。如果已经通过Desktop成功连接过SDE的话，那么会默认创建一个.sde连接文件，如C:\Users\Administrator\AppData\Roaming\ESRI\Desktop10.3\ArcCatalog\Connection tooracle.sde，  
如果没有连接过的话，可以通过IWorkspaceFactory.Create()或gp工具Create ArcSDE Connection File来创建。  

# 7. 执行失败怎么办？   
如上面的示例代码中的方式，把执行gp的语句放进try-catch-finally的结构体中，并用IGeoProcessor.GetMessage尝试获取具体的报错信息，如许可级别不够、参数填写错误等。  

# 8. 关于在engine中调用gp是否有官方帮助文档？   
有，10.3版本在线帮助地址：  
http://resources.arcgis.com/en/help/arcobjects-net/conceptualhelp/#/Using_geoprocessing/0001000004mm000000/  

调用自定义gp工具、gp服务、和其他高级技能都可以参考官方帮助文档。 
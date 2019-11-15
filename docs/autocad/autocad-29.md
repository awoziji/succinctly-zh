## 块

块是由其他对象组成的单个对象，块中的每个元素可以具有自己的属性集。

块是时间和文件大小的储存器。定义块时，AutoCAD 会将其存储在当前图形的内部库中，称为“块表”。即使未在任何地方使用（插入），图形中也可能存在块，如果通过重新插入或复制创建块的多个实例，则所有实例都引用块库。如果编辑单个块引用，则同样更新所有其他块。

### 创建块

命令：BLOCK

别名：B 或 BL

在创建块之前，首先像创建任何绘图时一样绘制元素。为了说明创建一个块，我们将处理我们在前面章节中创建的 Column Base 图。

如果尚未打开 AutoCAD，请立即打开它，然后打开位于**第 05 章**文件夹中的图 **ColumnBase.dwg** 。

图形由定义柱基轮廓的蓝色折线和定义柱基过渡的灰线组成。

元素在已定义的图层上正确设置，但是有些做法虽然不是必需的，但在使用这样的简单块时变得非常方便：

*   将所有对象设置为图层 **0** 。第 0 层是一个“神奇”层，在隐藏或冻结图层时可以进行许多操作。
*   将所有属性设置为 **ByBlock** 。这将允许用户通过更改块属性来更改块元素的外观，如果块（对象）属性设置为 **ByLayer** ，则块将继承图层属性。如果设置为 **ByLayer** ，则块继承**图层属性**，块属性的更改不会影响块元素。
*   定义有意义的基点（插入点）。

同样，这些不是规则，但在低密度块上变得很方便。对于更复杂的块（例如详细信息），您可能希望维护所有属性，以便可以通过其他方式进行管理。

让我们改变这个块的对象属性：

1.  按窗口或窗口交叉选择所有对象。
2.  从 **Home 选项卡**， **Layers Panel** 中，从图层列表中选择 **Layer 0** 。
3.  从**属性**面板，将所有属性更改为 **ByBlock** （当前显示为 **ByLayer** ）。
4.  按 **Esc** 取消选择所有对象。
5.  从**图层面板**中，将图层 **0** 设置为当前图层。
6.  从 **Home** 选项卡， **Block** 面板，单击 **Create** 工具打开 **Block Definition** 对话框。
7.  在**名称**字段中输入 **Column Base** 。
8.  在**基点**区域中，单击**拾取点**。
9.  按住 **Shift** ，右键单击鼠标，然后从上下文菜单中选择 **Midpoint** 。
10.  单击最低水平线的中点附近。
11.  在**对象**区域中，单击**选择对象**。
12.  选择定义列基的所有对象，然后按**确定**。
13.  在**选择对象**区域中，单击**转换为块**。
14.  单击**确定**。

现在擦除源对象，并在当前层中插入新创建的块引用，源对象在此之前。

1.  选择块插入。
2.  从 **Home** 选项卡， **Layers** 面板，将块 Layer 更改为 **Column Base** ，然后按 **Esc** 清除选择。该块继承了 Layer 属性。
3.  将绘图另存为 **MyBlocks** 。

### 插入块

插入当前图形的块表中存在的块

命令：INSERT

别名：我或 INS

现在我们有了一个块，我们可以在图形中插入块的其他实例，或者您可以复制现有的实例。现在，让我们看看如何插入一个块：

1.  缩小到足以使您可以在绘图区域中至少再放置一个列基块。
2.  将 **ColumnBase** 设置为当前 **Layer** 。
3.  从 **Home** 选项卡， **Block** 面板，单击 **Insert** 工具，或键入 **I** （或 **INSERT** ）然后按**输入**或**空格键**。
4.  出现可用块列表。选择 **Column Base** 块。如果图形的块表中没有可用的块，则会显示“插入”对话框，因此您可以加载要作为块插入的图形。
5.  表示块的字形显示在光标处，单击绘图区域中的任意位置以插入块。
6.  尝试复制块，就像上一章中对植物块一样。

将现有图形作为块插入

通常，您需要从先前从制造商的网站创建或下载的文件库中插入图纸。理想情况下，要插入的图形是常规图形而不是图形中的已定义块，因为在插入时会创建包含所选图形中的元素的新块定义。

要将现有图形作为块插入当前图形中：

1.  从 **Home** 选项卡， **Block** 面板，单击 **Insert** 工具，然后单击 **More Options** 打开 **Insert** 对话框。
2.  单击**浏览**按钮并导航到您下载本书的练习文件的位置。在**第 05 章**文件夹中，选择名为 **sink.dwg** 的图形，然后单击**打开**。
3.  如果需要，您可以为块输入新名称。插入具有已存在于块表中的名称的图形将重新定义现有块。
4.  确保选中**指定屏幕上的**复选框，以便在绘图区域中选择插入点。
5.  单击**确定**。
6.  块标志符号出现在十字光标中;单击图形中的任意位置以插入块。
7.  该块插入当前层。

### 编辑块

命令：BEDIT

别名：BE

您可能需要对块进行更改。例如：我真的不喜欢显示列基过渡线的方式，并且它们可能会绘制为粗体，具体取决于绘图样式定义。我们将编辑列基块，以便过渡线为灰色：

1.  选择一个列基本块实例。
2.  右键单击鼠标，然后从上下文菜单中选择**块编辑器**。

绘图区域背景颜色更改为灰色，块编辑器上下文选项卡将加载到功能区中。您现在处于块编辑器模式。

![](img/00157.jpeg)

图 100：块编辑器上下文选项卡

1.  选择连接整个柱基的所有七条线（不要选择轮廓折线）。
2.  如果看不到“特性”选项板，请按 **Ctrl + 1** 显示“特性”选项板。
3.  在**属性**调色板，**常规属性**上，单击颜色下拉菜单，然后从列表中选择**选择颜色**。
4.  在颜色文本框中，输入 **9** 并单击 **OK** 以设置所选对象的颜色。
5.  按 **Esc** 清除选择。
6.  单击**块编辑器**上下文选项卡中的**关闭块编辑器**。
7.  单击**保存**将更改保存到 **Column Base** 。
8.  块的所有实例都会更新。

| ![](img/00033.jpeg) | 提示：创建块时，您可以选择避免块被爆炸。这对于避免意外爆炸块非常有帮助。在块编辑器模式下，可以从“特性”选项板更改此属性。 |

爆炸水槽块：

命令： X 8 EXPLODE

选择对象：选择接收器块，然后按 Enter 或空格键。

该对象不再是一个块。

命令： I 8

“插入”对话框打开;从 名称 中选择 接收 列表并单击 确定 。

指定插入点或[基点/比例/ X / Y / Z /旋转]：在绘图区域中选择一个点。

插入了接收器块的新实例，因为接收器块定义保留在图形的块表中。

### 将块写入文件

您经常需要编写一个文件块，以便在将来的图纸中重复使用。要将块写入文件，选择不必是块;它可以是任何选择集，包括包含块和其他非块对象的集合。

命令：WBLOCK

别名：WB

让我们将 Column Base 块写入文件：

1.  From the **Insert** tab, **Block Definition** panel, select **Write Block**, as shown in the following figure:

    ![](img/00158.jpeg)

    图 101：写入块

2.  从选项中选择 **Block** 。
3.  从**块**列表中，选择 **Column Base** 。
4.  在目标区域中，单击 **...** 按钮以显示**浏览图形文件**对话框。浏览到您偏好的位置。
5.  在**文件名**文本框中，输入 **My Column Base.dwg** 并单击**保存**。
6.  单击 **OK** 保存块。

该块现已保存，您可以在以后的任何图纸中重复使用。

保存并关闭图形。

| ![](img/00024.gif) | 注意：生成的保存文件不包含块;它包含组成所选块的对象。 |

| ![](img/00033.jpeg) | 提示：您可以使用 Ctrl + C 从图形中复制对象，使用 Ctrl + V 粘贴到另一个图形中。 |
# Auto-weekly-report(Kunshan)
**The goal**:
My collegues input some data or variables,a report will be generated in a few seconds via AI agent.


# 工作流程
先从chatbot开始，唯一的变量是type，因为不同主题之间选用的扩充润色词汇不尽相同。

Prompt是主要的来源

优化点：
1.COT，SC，TOT等方法的叠加；

2.改成英文；

3.怎么能控制它不要乱说话？；

4.怎么能让它学到更多的例子？；

5.我想要和写日报的同事交流一下。

# 测试用例
** 以Safety 为例：Kunshan，0722 **

假设的输入：
20个外包司机能力测试都过关了

自由滚筒全面检查消除了4处危险夹点，更新了OPL

FF车间加入冷风机防中暑


| 模型 | 提示词 | 输出 |评价|
| ---- | ---- | ---- |----|
| 真实值 |   | 1. 完成了对全部 20 名外包司机的能力测试，合格率 100%；2. 对自由滚筒进行了全面的夹点安全检查，识别并消除了 4 处危险夹点，并制定了新的 OPL；3. 在夏季持续关注员工身心健康，在 FF 车间的高温工位安装了冷风机。|
| Few shot | 1. 首先识别报告的类型{{type}}<br>2. 然后你要根据不同类型的问题来决定扩充润色报告时适宜的词，例如在Safety类型中，更常用Check，Complete，Strict等。 | 所有20名外包司机已完成能力测试，测试结果全部达标，确保了运输作业的安全性与合规性；对自由滚筒区域进行全面检查，成功识别并消除4处潜在危险夹点，相关整改已闭环；同步更新了对应OPL（操作指导卡），强化一线员工风险意识与操作规范；FF车间已正式加装冷风机，有效改善高温作业环境，预防中暑风险，切实落实防暑降温措施，保障员工健康与生产连续性。 |  不够简洁   |
| COT | 1. 首先识别报告的类型{{type}}<br>2. 然后你要根据不同类型的问题来决定扩充润色报告时适宜的词，例如在Safety类型中，更常用Check，Complete，Strict等。你可以通过<example>学习，也可以自己通过浏览相关制造业公司的周报来学习这种语言风格<br>3. 然后对用户输入的内容进行“去口语化操作”<br>4. 利用步骤2中学习到的语言风格和词汇风格来润色这段话。 | 所有 20 名外包司机已完成能力测试，测试结果全部达标，确保运输作业安全合规；对自由滚筒区域进行全面检查，识别并消除 4 处潜在危险夹点，相关整改措施已闭环；更新对应 OPL（标准作业指导卡），强化作业人员对关键风险点的认知与防范意识；FF 车间已部署冷风机，有效改善高温作业环境，落实防中暑措施，保障员工健康与作业安全。 |   还不错，基本没有大的失误 ，不够简洁   |
| COT+SC | 1. 首先识别报告的类型{{type}}<br>2. 然后你要根据不同类型的问题来决定扩充润色报告时适宜的词，例如在Safety类型中，更常用Check，Complete，Strict等。你可以通过<example>学习，也可以自己通过浏览相关制造业公司的周报来学习这种语言风格<br>3. 然后对用户输入的内容进行“去口语化操作”<br>4. 利用步骤2中学习到的语言风格和词汇风格来润色这段话，得到三种不同的润色版本<br>5. 步骤4中生成的3种版本，或多或少的存在你主观臆断，或言过其实，或表意不清的地方，你针对这些问题改一改，得到输出的三个版本<br>6. 步骤5中生成的这些版本，请你选择一个最符合我要求的给我输出。 | 所有 20 名外包司机已完成能力测试，测试结果全部合格，相关记录已归档并完成备案；完成自由滚筒区域全面安全检查，识别并消除 4 处机械夹点风险，整改措施已验证有效，对应 OPL 文件已完成更新并下发至现场；在 FF 车间实施冷风机防中暑措施，覆盖高温作业区域，确保作业人员在高温环境下安全作业。 |   添油加醋，杜撰，例如：“机械夹点”  |
| TOT | 1. 首先识别报告的类型{{type}}<br>2. 然后你要根据不同类型的问题来决定扩充润色报告时适宜的词，例如在Safety类型中，更常用Check，Complete，Strict等。你可以通过<example>学习，也可以自己通过浏览相关制造业公司的周报来学习这种语言风格<br>3. 然后对用户输入的内容进行“去口语化操作”<br>4. 利用步骤2中学习到的语言风格和词汇风格来润色这段话，得到三种不同的润色版本<br>5. 步骤4中生成的3种版本，或多或少的存在你主观臆断，或言过其实，或表意不清的地方，你针对这些问题，选出一个你认为相对还凑合的版本<br>6. 步骤5中相对还凑合的这个版本，你按照我的要求给我优化出三种版本<br>7. 步骤6中生成的三个版本，按照我的要求（表意清晰，词汇风格与主题一致，没有夸大成分），给我选出一个最好的，最后只输出这一个就好。 | 20名外包司机已完成能力测试，全部通过，符合上岗标准；对自由滚筒区域进行全面检查，已消除4处危险夹点，并同步更新对应OPL（操作指导卡）；FF车间已加装冷风机，有效提升作业环境降温效果，预防高温中暑风险。 | 最符合要求，表意不拖泥带水，也没有内容的残缺  |
| Step-back | 1. 首先识别报告的类型{{type}}，需要什么？<br>2. 然后你根据示例以及从网页上浏览到的制造业公司周报的语言风格思考一下，如果想将用户输入的不规范的，零散的语言转化成符合这些报告规范的语言<br>3. 这些问题的答案是什么？<br>4. 你带着这份答案，去处理一下用户输入。 | 完成20名外包司机的能力测试，全员通过，确保运输作业人员资质合规，降低外部作业安全风险；对自由滚筒区域进行全面安全检查，识别并消除4处潜在夹点隐患，同步更新对应OPL（操作指导卡），强化员工风险意识与标准化操作；FF车间已加装冷风机，落实防暑降温措施，有效应对高温作业环境，保障员工健康与作业安全。 | 太多修饰词  |


# How to evaluate?
*单次评估*（根据我了解到的知识库不断更新）
1.各种计算文本相似度的库，如：jieba
2.将AI生成结果质量从“准确度，覆盖度，可扩展度......”等多个方面评估得分并加权



# From chatbot to workflow
在开发chatbot并和mentor讨论以后，我们发现了聊天机器人的问题:

1.无法在提示词出引用变量

2.依赖知识库

3.基于LLM，每次只能对多个步骤做一次处理，很多有价值的步骤被当作修饰语被忽略

因此我们一致认为应该开发一个工作流，解决上面的问题。

改进点集中于：<br>
1.取消type变量和is_done变量，改为AI自动识别



# workflow 初步尝试：以safety为例
Few shot
example在prompt中，分类由分类器实现；
每种类别学习不同的例子；
LLM做英文转换；
结果示例：
标准：
1. Launch the targeted project (door interlock mechanism) to enhance safety protocols and risk mitigation for the Z-Calender 
2. Deliver health and safety training based on occupational health screening results
3. Finalize comprehensive EHS inspections before shutdown, with emphasis on VOC protocols to prevent regulatory exceedances

AI输出：
1. Initiate the door lock project and continue advancing the safety upgrade of the Z-rolling machine to enhance equipment operational safety and operational reliability;  
2. Conduct targeted health and safety training based on employee health examination results to strengthen employees' health awareness and risk prevention capabilities;  
3. Strictly enforce the pre-shutdown EHS inspection procedure, with particular focus on verifying VOC emission limits, ensuring compliance with environmental protection standards and on-site safety requirements.

# workflow 改进：用户会把一大坨东西输入进来，进行自动识别然后再fewshot，最后整体输出分点列项的文字。
最重要的问题就是分类，如何把用户一大坨的输入分成不同的类别是重中之重。

在经过分类器/迭代/条件分支等一系列尝试后失败，最后选择了用LLM分类。

# 如何整合文本
变量聚合器是一定要使用的，但是变量聚合器它只是将变量放在了一起，你还是需要想办法调用它们，由于任务简单，所以在后面再次加入一个LLM作为整合机器。

这里的提示词，我通过一个更简单的测试用例探索出。

初级版本：prompt中只引用了聚合器的output变量，并将五个段落笼统的称呼为：“那五个变量”。

***这样是不行的，会导致LLM只能识别到LLM1，后面4个都无法识别。***

迭代：所有的变量指名道姓：

*任务：
读取{{#context#}}里面获得{{#1755589324439.text#}}，{{#1755589329535.text#}}，{{#1755589332438.text#}}，{{#1755589339103.text#}}，{{#1755589341390.text#}}的内容，然后将它们整合到一起输出。*

*约束：
不要更改{{#1755758855651.Group1.output#}}中五个变量的任何内容，只是起到一个聚合器的作用。*

# 优化 8.21
总结来说，大问题就是两点：

1.分类不准；2.优化过度

分类不准的问题要靠增加训练集，提升个人对业务的理解来解决；
而优化过度，集中在误删具体数据，先把提示词修改一下。
# 优化8.25
分类不准，重复利用同一句话的问题被解决了。在初始位置添加一个LLM，生成一个list，后续的“分类LLM”从list中挑选，避免重复和分类不准的问题，此外加入数据库来给这个LLM学习分类的标准。

提示词目前的策略是：出现一个问题，改进一个问题，直到贴近标准版本。
# 版本初具雏形，下面可以优化的点
1.增加训练集(最好是user的真实输入）；

2.语言风格人机，喜欢说废话；

3.英文

4.更加灵活？比如在我输入的内容中缺失一些部分的时候，模型能否“坚定的”放弃这个分类？至于时间分类，我暂时不认为这个可以被抛弃，因为在中文版本下，并没有能完美实现二者区分的规则，只能麻烦我的users们动动手指简单分个类。



# 双语输入：能用大模型解决的问题没必要拖给新的工具包
最影响结果的操作是：在哪一个位置选择将中文变成英文。

结果证明，在大白话被优化到英文之前，我都不建议去做翻译：因为事实上，我们只有英文版本的ppt，中文翻译的ppt并不是完全准确的，而真实值只能在polish/refine的环节才能出现，所以此环节可以直接给出一个example。

example：无论input是中文还是英文，output都是ppt上的英文内容。

这要求我们在此前的步骤中，要尽可能的保持同一种语言，中文就是中文，英文就是英文，防止误差累积。

# User-friendly
假设这个workflow被欧洲分公司的employee获得，我并没有告诉他们输入要按照什么格式。

Robert在输入周报内容的时候，不知道要将其分为两类，我的agent以为这只是positive，会把许多watch out的内容搞到后面去，这显然不是我们想看到的。

By discussion，把输入变量裂成两份，这样一来，即便users午饭前只写出了positive的内容，也不必担心回来的时候数据被人删掉，可以直接运行。

我的agent会十分清晰的意识到watch out那里什么都没有，进而输出“Please supply more information”

# 与Data Engineers们的交流
事实上，上面的工作流开发集中在“润色，修补”，但我还是需要很多大白话的输入，那这些大白话从何而来？经过与技术部门的讨论，我获得了如下信息。

1.Power BI生成了ppt上的图片

2.主要来源于四个整理好的BI数据集，和一个动态的网页数据集，从全球公司收集而来。

3.五个数据集里面的数据经过7-8种函数的处理，得到PPT图片上面的指数

**如果可以把数据直接转换成ppt文字，那就彻底没有人为的误差了，是一个非常优美的监督学习，x是数据，y是ppt里面的内容。**

# 上面的是润色，下面即将开始做的是如何从数据直接变成报告
先用文件提取器，把excel转成markdown，然后加入一个code，先把数据转成可以读的格式，然后在代码里计算数据，得出结果以后，调用一个api，这个api是一个agent，这个agent会根据知识库（如何把数据变成报告语言）来生成语言。

# 我做出来了一个小demo
先拆解“ILD.xlsx”为markdown语法，然后写一个代码，这个代码的内容是计算ILD，接着添加一个LLM，提示词是有关data 2 text的例子。

# 9.16我和Derek开了个会
内容是关于原有规范报告的结构，使得生产的流程减少人工的干预。

实现从数据直接到文本的交互，输入n个excel文件，直接生成对应格式的报告。

先前不同地区的报告内容分类差异很大，并且内容的主观性很强，Derek认为这不便于在global传递信息。（菲律宾，印度，印度尼西亚官方语言都是英语，泰国也是英语为主流）

目前还需要沟通的细节是：

1.数据? 怎么输出？ 从哪里循环？ 时间复杂度？

2.每一个指标如何对应到具体的文本?(捕捉数据的趋势？变化？是否需要额外的处理计算？）

3.最困难的是规范报告小标题的分类，我目前的想法是小标题按照那五个分类，然后根据图片里面的数据再加入一层小标题，即Safety下标准化的三个点，例如Safety Rule；Safety Network；Safety Staff，由数据驱动。

# 思路上的转变
在经过一天不断的数据审查，小标题选取之后，我发现了一个问题，就是我们现在也不确定到底要算哪些数，用数字生成哪些文字，一旦按照原有的思路去做，修改起来难度很大（涉及提示词，代码，模块链接的大修改）。

所以我决定将Derek的问题分成三个模块，第一个是用Dify算数，这里可能会问，为什么不用Power BI算，答案是麻烦，因为要筛选很多条件，还要设置一大堆中间变量。

第二个是数据到文本，此处的核心是LLM的提示词。

第三个已经做好了，refine自然语言。

# 如何调用外部的python
在dify中安装一个包是解决不了这个问题的，因为数据集太大了，在沙盒中根本跑不起来。

Flask/Fastapi是一个编写api的包，也就是将python作为一个开源的软件，利用dify中code节点的request请求，使其在外部独立运行。

```python
import requests

def main():
    files = {"file": open("data.csv", "rb")}
    resp = requests.post("http://localhost:8000/process", files=files)
    return resp.json()
```
这是在dify中运行的代码，其中files = /input{raw_file}

```python
from fastapi import FastAPI, File, UploadFile
import pandas as pd

app = FastAPI()

@app.post("/process")
async def process(file: UploadFile = File(...)):
    df = pd.read_csv(file.file)  
    result = df["value"].mean()  
    return {"mean": result}
```
这是在Vscode中运行的内容，**process**是主函数，file一定要和代码在同一个目录下，不然是无法识别的。

**不推荐使用这种方法，因为这需要搭建一个云数据库，访问的时候很容易掉线**

多嘴说一句，直接在dify中安装库是没有必要的，docker环境对于user并不友好，操作难度大。

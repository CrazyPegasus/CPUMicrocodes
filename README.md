# CPUMicrocodes
Intel，AMD和VIA CPU微码存储库

CPU微码存储库新闻源
https://twitter.com/platomaniac
CPU微代码存储库讨论主题
https://www.win-raid.com/t3355f47-Intel-AMD-amp-VIA-CPU-Microcode-Repositories.html
MC Extractor
https://github.com/platomav/MCExtractor
MC Extractor讨论主题
https://www.win-raid.com/t2199f47-MC-Extractor-Intel-AMD-VIA-amp-Freescale-Microcode-Extraction-Tool-Discussion.html
这是我们发现的每个最新生产的 Intel，AMD和VIA CPU微代码的集合。您可以使用MC Extractor立即检查微码是否已存在于存储库中。

收集CPU微码对于升级目的非常重要，可以创建通用工具，帮助人们了解他们使用的微码，研究通用技术的工作原理，对于没有供应商代表想要在给定平台上工作的开发人员等。

免责声明：以下所有微代码仅来自官方BIOS / UEFI更新，Intel / AMD Linux微代码更新，Linux发行版，Windows更新等，由各个制造商提供并公布！始终建议请求和/或等待您的OEM / OS发布更新的修复程序。聚集和提供微代码的唯一目的是帮助那些没有其他可行解决方案的人。因此，对于那些由于无差异和/或系统年龄而制造商拒绝提供帮助的系统存在重大问题的人来说，它们非常有用。

存储库中的所有微代码都具有一些共同属性，并根据它们进行分类，如下所示：

每个微码都针对一个特定的CPUID，它对家庭，代，模型，步进等信息进行编码。例如，Intel 0x000906EB或AMD 0x00810F10或VIA 0x00010690。
每个微代码都有一个更新版本，在修复时会增加。例如，0x00000A0B <0x00000A0E。每个CPUID的最新微码都包含在存储库中。
每个微码都有一个与其公开发布有关的日期，采用ISO8601 YYYY-MM-DD格式。例如，2018-01-02或2016-12-09。
每个微代码都包含一个校验和，用于在部署到制造商期间检查其有效性。例如0x1B3E0B0E。CPUID> = 0x00500F00的所有AMD微代码都没有正式的校验和，因此MC Extractor会生成自己的。
英特尔微代码具有平台ID字段，该字段以二进制形式对支持的CPU套接字/平台类型进行编码。例如，0xC0 = 6,7或0x03 = 0,1或0x76 = 1,2,4,5,6。
英特尔微码发布/类型状态区分为生产（PRD）和预生产（PRE）。只有生产（PRD）微码包含在存储库中。
VIA微码具有一个Signature，以人类可读的形式显示CPUID和Update Revision。例如，BJ_6FE_0205或06FA003BB。
为了正确构建微代码存储库，需要遵循一定的心态：

每个固件文件名如下结构的CPU CPUID_ 高原 PlatformID（英特尔）_ 版本 UpdateRevision_Date_Release（英特尔）_Checksum并具有扩展名为.bin。例如：Intel cpu906EB_plat02_ver0000007C_2017-12-03_PRD_5046D998，AMD cpu00800F11_ver08001129_2017-07-14_4F426450或VIA cpu10690_ver00000001_sig [BJ_10690.020] _2017-01-09_A8B24DC2。
MC Extractor检查所有微码以验证其健康状况，大小等。请查看MCE的说明以了解其更多功能。
由于CPU微码太多，所有内容都放在一个特定于供应商的文件夹中，用户负责查找所需的正确CPUID和平台ID。
所有CPU微码的更新状态（Last Yes / No）依赖于其CPUID，Update Revision和Date。
英特尔微代码的更新状态还依赖于其发布/类型，即生产（PRD）或预生产（PRE）。例如，假设的微码cpu206A6_plat12_ver00000028_2010-09-15_PRD与“最后一个”相比是“最后一个”cpu206A6_plat12_ver00000022_2010-07-07_PRD，但cpu206A6_plat12_ver00000028_2010-09-15_PRE也是如此。这是因为，与其他两个相比，它是预生产，而不是生产。请注意，MC Extractor也可以检测到它，并且由于它们在发布/类型上的不同而将显示为“最后是”，即使其他所有内容相同或有利于其中一个或另一个。
英特尔微代码的平台ID字段最多可包含8个受支持的套接字（LGA775，LGA1366等）或平台类型（桌面，移动等），具体取决于CPU生成，采用编码二进制形式（位掩码）。用户需要确定他们所选择的微代码更新是否具有与来自BIOS或OS的当前加载的CPU微代码相同或更多的平台ID。您可以使用MC Extractor检查每个Intel微码支持的平台ID。例如，如果您当前的微码具有CPUID 0x00000F4A和平台ID 0x5C（2,3,4,6），则可以更新为具有相同CPUID 0x00000F4A但平台ID为0x5D（0,2,3,4， 6）因为它还包括平台“0”。另一方面，您无法更新到具有相同CPUID 0x00000F4A但平台ID为0x58（3,4,6）的较新微码，因为它不包含原始“2”并且您的套接字/平台类型可能不受支持。请注意MC Extractor也可以检测到这一点，因此，如果您无法在存储库中找到确切的CPUID和平台ID组合，就像您当前拥有的那样，可能是因为存在另一个具有相同CPUID但具有更多支持的平台ID的微代码。例如，在2017年，具有CPUID 0x000906E9和平台ID 0x22（1,5）的微代码由CPUID 0x000906E9和平台ID 0x2A（1,3,5）继承，以便在KBL添加LGA2066套接字/ HEDT平台类型支持（ - X）CPUID。

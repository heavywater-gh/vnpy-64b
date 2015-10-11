

修改了家俊桑之前的make脚本。目前只修改了vn.ctp目录及子目录下的make脚本。

********************之前**************************

$(CXX) $(COMMON_FLAGS) -shared -Wl,-soname,vnctpmd.so -o vnctpmd.so vnctpmd.o -L$(ROOTPATH)/vn.ctp/ctpapi  $(LIBRARIES) -l:thostmduserapi.so -l:thosttraderapi.so

********************之后**************************
$(CXX) $(COMMON_FLAGS) -shared -Wl,-soname,vnctpmd.so -o vnctpmd.so vnctpmd.o -L/usr/local/lib  $(LIBRARIES) -l:thostmduserapi.so -l:thosttraderapi.so

之前的做法会导致在迁移环境时必需要重建与编译环境完全相同的目录。改了之后只需把需要的库拷贝到/usr/local/lib中。

具体的问题我也不太清楚，似乎python会从so文件中获得它编译时依赖的库的路径，然后要求相同的路径。是python的bug吗？请知道的同学不吝赐教。



以下是@家俊桑原来的readme
## 关于Linux下编译运行的说明 ##

知乎：@家俊桑

已初步验证vnpy仅需少量跨平台兼容性修改，再加上华宝的Linux动态链接库文件即可在Linux上编译运行 (仅在Ubuntu x64下测试)

如需在Linux下编译运行，请在bashrc中设置环境变量 LD_LIBRARY_PATH 以及 PYTHON_PATH， 例如：

```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/home/user/vnpy/vn.lts/vnltsmd/pyltsmd:/home/user/vnpy/vn.lts/ltsapi:/home/user/vnpy/vn.lts/ltsl2:/home/user/vnpy/vn.ctp/ctpapi

export PYTHON_PATH=$PYTHON_PATH:/home/user/vnpy/vn.lts/vnltsmd/pyltsmd:/home/user/vnpy/vn.lts/ltsapi:/home/user/vnpy/vn.lts/ltsl2:/home/user/vnpy/vn.ctp/ctpapi
```

然后cd至vnpy项目根目录并使用make
vnpy$ make all

ctp及lts api的封装库将以.so的形式被创建，并会被自动拷贝至demo和strategy目录

Linux下代码所需改动主要有
1）使用条件编译移除对stdafx.h的引用

<------------------
```
#include "stdafx.h"
```
------------------>
```
#ifndef __GNU__
#include "stdafx.h"
#endif
```

2) 使用GNU C的strncpy替代MSVC的strcpy_s函数

<------------------

------------------>
```
#ifdef __GNU__
#define strcpy_s(dest, len, src)  strncpy(dest, src, len)
#endif
```

3）demoMain 文件中取消不必要的 windows 函数调用


因为数据和帐号原因，Linux版本并未得到完整测试，权当抛砖引玉

如果在Linux 32位上运行，需要去华宝下载32位的动态链接库
http://www.sfit.com.cn/5_2_DocumentDown.htm

## License ##
MIT


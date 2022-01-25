# fmemopen_windows
a lib to provide **FILE\*** handler based on memory backend for fread,fwrite etc just like fmemopen on linux on windows.


# Usage
1.include the header.  
2.include the libary depend on your platform32/64.  
3.using ``fmemopen``.  

### usage sample:
```
#include <stdio.h>
#include "libfmemopen.h"

int main(){
	FILE * fh;
	char buf[1024] = "jacksonsonsosnososnsljgweoigjiedjgkdrjshnjklfcgsdntildhgd fjklhndrhpadk thiohkaerheil ghksbjd ghbjcghkwe4pt hphq tgjh";
	//put your stuff in buffer
	fh = fmemopen(buf, 1024, "wb");
	printf("FileHandler:%d\n", fh);
	getchar();
	fseek(fh, 0, SEEK_SET);
	char * bux[1024];
	int readbytes = fread(bux, 1, 1024, fh);
	printf("\nbuffer:%s\n", bux);
	printf("Readed_bytes:%d\n", readbytes);
	getchar();
	fclose(fh);//don't forgot fclose it,call fclose on a handler created by fmemopen_windows libary will automatically free it(include deep layer).
	return 0;
}
```


---


A bad example:

>there may got some security risk in this version,look the code below.I'll dig it later.

```
#include <stdio.h>
#include "libfmemopen.h"

int main(){
	FILE * fh;
	char buf[1024] = "jacksonsonsosnososnsljgweoigjiedjgkdrjshnjklfcgsdntildhgd fjklhndrhpadk thiohkaerheil ghksbjd ghbjcghkwe4pt hphq tgjh";
	//put your stuff in buffer
	fh = fmemopen(buf, 1024, "wb");
	printf("FileHandler:%d\n", fh);
	getchar();
	fseek(fh, 0, SEEK_SET);
	char ddbuf[1028] = "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaABB";
	int johnlet=fwrite(ddbuf, 1028, 1, fh);
	printf("actually_write_long:%d\n", johnlet);
	fseek(fh, 0, SEEK_SET);
	char * bux[1030];
	int readbytes = fread(bux, 1, 1030, fh);
	printf("\nbuffer:%s\n", bux);
	printf("Readed_bytes:%d\n", readbytes);
	printf("\n\nTheOriginalBuf:%s", buf);
	getchar();
	fclose(fh);//don't forgot fclose it,call fclose on a handler created by fmemopen_windows libary will automatically free it(include deep layer).
	return 0;
}
```


```
#include <stdio.h>
#include "libfmemopen.h"

int main(){
	FILE * fh;
	char buf[1024] = "jacksonsonsosnososnsljgweoigjiedjgkdrjshnjklfcgsdntildhgd fjklhndrhpadk thiohkaerheil ghksbjd ghbjcghkwe4pt hphq tgjh";
	//put your stuff in buffer
	fh = fmemopen(buf, 1024, "wb");
	printf("FileHandler:%d\n", fh);
	//sizer

	fseek(fh, 0, SEEK_END);   ///将文件指针移动文件结尾
	long size = ftell(fh);
	printf("size:%d\n", size);
	//size
	getchar();
	fseek(fh, 0, SEEK_SET);
	char ddbuf[1028] = "aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaABBCCDDEE";
	int johnlet=fwrite(ddbuf, 1028, 1, fh);
	//size
	printf("actually_write_long:%d\n", johnlet);
	fseek(fh, 0, SEEK_END);   ///将文件指针移动文件结尾
	size = ftell(fh);
	printf("size:%d\n", size);
	//size
	fflush(fh);
	//size
	fseek(fh, 0, SEEK_END);   ///将文件指针移动文件结尾
	size = ftell(fh);
	printf("size:%d\n", size);
	//size
	fseek(fh, 0, SEEK_SET);

	char * bux[1030];
	int readbytes = fread(bux, 1, 1030, fh);
	printf("\nbuffer:%s\n", bux);
	printf("Readed_bytes:%d\n", readbytes);
	printf("\n\nTheOriginalBuf:%s", buf);
	getchar();
	fclose(fh);//don't forgot fclose it,call fclose on a handler created by fmemopen_windows libary will automatically free it(include deep layer).
	return 0;
}
```

---

during these days I've been try alot way to simulate fmemopen on windows,this lib is the best solution I found at the end.


the way I think we can done this:
- completely rewrite fread,fwrite.... X 
- mmioOpen
>a good way to perform pure memory File I/O,but the return handler is ``HMMIO`` cannot cast to ``FILE*``
>https://docs.microsoft.com/en-us/windows/win32/multimedia/performing-memory-file-i-o
>and You must call mmioClose to close a file opened by using mmioOpen. Open files are not automatically closed when an application exits. and seems like poor support after win2k.

- using ramdisk
>need to load driver,and perform 'disk' format etc,too heavy.

- using _open
>https://docs.microsoft.com/zh-tw/previous-versions/z0kc8e3z%28v%3dvs.120%29
>this is the way,due to the lack support of windows kernel,we have to create a temp file on disk then use _open to create a FILE* type handler for use,and by control the create of temp file,we can avoid any actually disk write operation to the temp file(you fmemopen a 100mb file in memory and it's still 0 bits on disk),it's like a pointer which we must need due to the windows kernel.

with few experiments the _open is optional way,but it's deprecated and microsoft say they have a newer secure version ``_sopen_s`` and ``_wsopen_s``,so this libary will use ``_sopen_s``.

across the description by msdn,the _sopen_s still got a chance to write things to disk,when memory not enough,so you may better not cache your secret key etc in it. 








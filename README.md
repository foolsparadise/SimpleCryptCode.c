# SimpleCryptCode.c  
## 说明 Readme  
```
C语言字符串的简单的加解密  
参考来源：  
https://blog.csdn.net/Ibelievesunshine/article/details/80056903  
在原基础上有改动，添加搜索判断处理key，进行区分对待  
```
#### 函数block
```
char *Crypt_Array[] = { "Login", "Password"};

//函数encode()将字母顺序推后n位，实现文件加密功能
char *encode(char *str){
	int n=6;
    char c;
    int i;
    for(i=0;i<strlen(str);++i){  //遍历字符串
        c=str[i];
        if(c>='a' && c<='z'){  //c是小写字母
            if(c+n%26<='z'){  //若加密后不超出小写字母范围
                str[i]=(char)(c+n%26);  //加密函数
            }else{  //加密后超出小写字母范围,从头开始循环小写字母
                str[i]=(char)(c+n%26-26);
            }
        }else if(c>='A' && c<='Z'){ //c为大写字母
            if(c + n%26 <= 'Z'){  //加密后不超出大写字母范围
                str[i]=(char)(c+n%26);
            }else{  //加密后超出大写字母范围,从头开始循环大写字母
                str[i]=(char)(c+n%26-26);
            }
        }else{  //不是字母，不加密
            str[i]=c;
        }
    }
    printf("\nAfter encode: \n");
    //puts(str);  //输出加密后的字符串
	return str;
}
//decode()实现解密功能，将字母顺序前移n位
char const *decode(char *str){
	int n=6;
    char c;
    int i;
    //遍历字符串
    for(i=0;i<strlen(str);++i){
        c=str[i];
        //c为小写字母
        if(c>='a' && c<='z'){
            //解密后还为小写字母，直接解密
            if(c-n%26>='a'){
                str[i]=(char)(c-n%26);
            }else{
                //解密后不为小写字母了，通过循环小写字母处理为小写字母
                str[i]=(char)(c-n%26+26);
            }
        }else if(c >= 'A' && c<='Z'){  //c为大写字母
            if(c-n%26>='A'){  //解密后还为大写字母
                str[i]=(char)(c-n%26);
            }else{  //解密后不为大写字母了,循环大写字母,处理为大写字母
                str[i]=(char)(c-n%26+26);
            }
        }else{  //非字母不处理
            str[i]=c;
        }
    }
    printf("\nAfter decode: \n");
    //puts(str);  //输出解密后的字符串
	return str;
}//该函数代码有冗余，读者可改进
//定义查找方法
int Is_Crypted(char *value/*查到的值*/){
	int count = sizeof(Crypt_Array)/sizeof(0);
	int i=0;
    for(i=0;i<count;i++){//循环数组中的每一个元素
        if(0==strncmp(value,Crypt_Array[i],strlen(value))){//判断该元素是否是查找的值
            return i;//已找到，返回找到该值在数组中的索引
        }
    }
    return -1;//没有找到，返回-1
}

```
#### 使用
```
char *key
if(Is_Crypted(key)>=0) { 
				//在名单里
				//encode(value)或decode(value);       
			}
```

# 平台部C语言编程规范

<!-- [[_TOC_]] -->


## 1 排版

**1-1（强制）：程序块要采用缩进风格编写，缩进的空格数为4个。**

说明：对于由开发工具自动生成的代码可以有不一致，不要用tab，用空格。

如果使用vim编辑器，可以进行如下设置：

set tabstop=4

在.vimrc中添加以下代码后，重启vim即可实现按TAB产生4个空格：

set ts=4 (注：ts是tabstop的缩写，设TAB宽4个空格)

**1-2（强制）：相对独立的程序块之间、变量说明之后必须加空行。**

示例：如下例子不符合规范。

```c
if (!valid_ni(ni))
{
    ...
}
repssn_ind = ssn_data[index].repssn_index;
repssn_ni = ssn_data[index].ni;
```

应如下书写

```c
if (!valid_ni(ni))
{
    ...
}

repssn_ind = ssn_data[index].repssn_index;
repssn_ni = ssn_data[index].ni;
```

**1-3（强制）：较长的语句（\>80字符）要分成多行书写。**

长表达式要在低优先级操作符处划分新行，操作符放在新行之首，划分出的新行要进行适当的缩进，使排版整齐，语句可读。

示例：

```c
if ((flag_var == TEST_FLAG)
    &&(((counter_var - TEST_COUNT_BEGIN) % TEST_COUNT_MODULE) >= TEST_COUNT_THRESHOLD))
{
    // process code
}
```

**1-4（强制）：不允许把多个短语句（包括赋值语句）写在一行中，即一行只写一条语句。**

示例：如下例子不符合规范。

```c
rect.length = 0; rect.width = 0;
```

应如下书写

```c
rect.length = 0;
rect.width = 0;
```

**1-5（强制）：if、for、do、while、case、switch、default等语句自占一行，且if、for、do、while等语句的执行语句部分无论多少都要加括号{}。**

示例：如下例子不符合规范。

```c
if (p_use_cr == NULL) return;
```

应如下书写：

```c
if (p_use_cr == NULL)
{
    return;
}
```

**1-6（强制）：函数或过程的开始、结构的定义及循环、判断等语句中的代码都要采用缩进风格，case语句下的情况处理语句也要遵从语句缩进要求。**

示例：如下例子不符合规范

```c
int32_t gpio_init(PIN_NUM pin_num)
{
int32_t fd_loc = -1;

if(pin_num >= GPIO_MAX)
{
return TOPS_ERR;
}

switch(pin_num)
{
case HEAT_LCD:
fd_loc = open(g_heat_lcd, O_RDWR);
break;
...
default:
return TOPS_ERR;
}

return fd_loc;
}
```

应如下书写：

```c
int32_t gpio_init(PIN_NUM pin_num)
{
    int32_t fd_loc = -1;

    if(pin_num >= GPIO_MAX)
    {
        return TOPS_ERR;
    }

    switch(pin_num)
    {
        case HEAT_LCD:
            fd_loc = open(g_heat_lcd, O_RDWR);
            break;
        ...
        default:
            return TOPS_ERR;
    }

    return fd_loc;
}
```

**1-7（强制）：在两个以上的关键字、变量、常量进行对等操作时，它们之间的操作符之前、之后或者前后要加空格；进行非对等操作时，如果是关系密切的立即操作符（如－\>），后不应加空格。**

说明：采用这种松散方式编写代码的目的是使代码更加清晰。

由于留空格所产生的清晰性是相对的，所以，在已经非常清晰的语句中没有必要再留空格，如果语句已足够清晰则括号内侧(即左括号后面和右括号前面)不需要加空格，多重括号间不必加空格，因为在C/C++语言中括号已经是最清晰的标志了。

在长语句中，如果需要加的空格非常多，那么应该保持整体清晰，而在局部不加空格。给操作符留空格时不要连续留两个以上空格。

示例：

(1) 逗号、分号只在后面加空格。

```c
int a, b, c;
```

(2)比较操作符, 赋值操作符"="、
"+="，算术操作符"+"、"%"，逻辑操作符"&&"，位域操作符"\<\<"、"\^"、"&"等双目操作符的前后加空格。

```c
if (current_time >= MAX_TIME_VALUE)
a = b + c;
a *= 2;
a = b ^ 2;
```

(3)"!"、"\~"、"++"、"--"、"&"（地址运算符）等单目操作符前后不加空格。

```c
*p = 'a';         /* 内容操作"*"与内容之间 */
flag = !isEmpty;  /* 非操作"!"与内容之间 */
p = &mem;         /* 地址操作"&" 与内容之间 */
i++;              /* "++","--"与内容之间 */
```

(4)"-\>"、"."前后不加空格。

```c
p->id = pid; /* "->"指针前后不加空格 */
```

(5)if、for、while、switch等与后面的括号间应加空格，使if等关键字更为突出、明显。

```c
if (a >= b && c > d) 
```

**1-8（建议）：程序中关系较为紧密的代码应尽可能相邻。**

说明：便于程序阅读和查找。

示例：以下代码布局不太合理。

```c
rect.length = 10;
char_poi = str;
rect.width = 5;
```

若按如下形式书写，可能更清晰一些。

```c
rect.length = 10;
rect.width = 5; /* 矩形的长与宽的关系较密切，放在一起。*/
char_poi = str;
```

## 2 注释

**2-1（强制）：文件头部应进行注释。**

注释必须列出：版权说明，文件名，作者，概述等。

示例：下面这段头文件的头注释比较标准，当然，并不局限于此格式，但上述信息建议要包含在内。

```c
/************************************************************************

    Copyright © XXXXX Inc. 2008-2020. All rights reserved.*
    File name:         // 文件名
    Author:            // 作者
    Description:       // 用于详细说明此程序文件完成的主要功能，与其他模块
                      // 或函数的接口，输出值、取值范围、含义及参数间的控
                      // 制、顺序、独立或依赖等关系*
    Others:           // 其它内容的说明

**************************************************************************/
```

**2-2（强制）：函数声明处头部应进行注释。**

列出：函数的函数名，描述，输入，输出，其他说明等。

示例：下面这段函数的注释比较标准，当然，并不局限于此格式，但上述信息建议要包含在内。

```c
/************************************************************************
    Function:           // 函数名称
    Description:        // 函数功能、性能等的描述
    Input:              // 输入参数说明，包括每个参数的作
                        // 用、取值说明及参数间关系。
    Output:             // 对输出参数和返回值的说明。
    Others:             // 其它说明
**************************************************************************/
```

**2-3（强制）：注释与代码的一致性。**

说明：边写代码边注释，修改代码同时修改相应的注释，不再有用的注释要删除。

**2-4（强制）：注释的内容要清楚、明了，含义准确，防止注释二义性。**

说明：错误的注释不但无益反而有害。

**2-5（强制）：避免在注释中使用缩写，特别是非常用缩写。**

说明：在使用缩写时或之前，应对缩写进行必要的说明。

**2-6（强制）：对代码的注释应放在其上方或右方（对单条语句的注释）相邻位置，不可放在下面，如放于上方则需与其上面的代码用空行隔开，且与下方代码缩进相同。**

示例：如下例子不符合规范。

例1：

```c
/* 获取子系统索引值和网络指示标志值 */

repssn_ind = ssn_data[index].repssn_index;
repssn_ni = ssn_data[index].ni;
```

例2：

```c
repssn_ind = ssn_data[index].repssn_index;
repssn_ni = ssn_data[index].ni;
/* 获取子系统索引值和网络指示标志值 */
```

应如下书写

```c
/* 获取子系统索引值和网络指示标志值 */
repssn_ind = ssn_data[index].repssn_index;
repssn_ni = ssn_data[index].ni;
```

**2-7（强制）：对于所有有物理含义的变量、常量，如果其命名不是充分自注释的，在声明时都必须加以注释，说明其物理含义。变量、常量、宏的注释应放在其上方相邻位置或右方。**

示例：

```c
/* 最大活动任务个数 */
#define MAX_ACT_TASK_NUMBER 1000
```

**2-8（强制）：数据结构声明(包括数组、结构、类、枚举等)，如果其命名不是充分自注释的，必须加以注释。对数据结构的注释应放在其上方相邻位置，不可放在下面；对结构中的每个域的注释放在此域的右方。**

示例：可按如下形式说明枚举/数据/联合结构。

```c
/* sccp interface with sccp user primitive message name */
enum SCCP_USER_PRIMITIVE_E
{
    N_UNITDATA_IND, /* sccp notify sccp user unit data come */
    N_NOTICE_IND,  /* notify user the No.7 network can't trans this message */
    N_UNITDATA_REQ,/* sccp user's unit data transmission request*/
};
```

**2-9（强制）：全局变量要有较详细的注释，包括对其功能、取值范围、哪些函数或过程存取它以及存取时注意事项等的说明。**

示例：

```c
/* 
* The ErrorCode when SCCP translate
* Global Title failure, as follows 
* 0 － SUCCESS   1 － GT Table error
* 2 － GT error  Others － no use  
* only  function  SCCPTranslate() in
* this modual can modify it,  and  other
* module can visit it through call
* the  function GetGTTransErrorCode() 
*/
BYTE g_GTTranErrorCode;
```

**2-10（强制）：字符序列 /\* 不应出现在注释中。**

C 不支持注释的嵌套，尽管一些编译器支持它以作为语言扩展。一段注释以/\*开头，直到

第一个\*/为止，在这当中出现的任何/\*都违反了本规则。

考虑如下代码段：

```c
/* some comment, end comment marker accidentally omitted
	<<New Page>>
Perform_Critical_Safety_Function (X);
/* this comment is not compliant */
```

在检查包含函数调用的页中，假设它是可执行代码。

因为可能会省略掉注释的结束标记，那么对安全关键函数的调用将不会被执行。

**2-11（强制）：对于switch语句下的case语句，如果因为特殊情况需要处理完一个case后进入下一个case处理，必须在该case语句处理完、下一个case语句前加上明确的注释。**

说明：这样比较清楚程序编写者的意图，有效防止无故遗漏break语句。

示例：

```c
case CMD_FWD:  
    ProcessFwd(); 
    
    if (...)
    {
        ...
        break;
    }
    else
    {
        ProcessCFW_B();   /* now jump into case CMD_A */
    }

case CMD_A:    
    ProcessA();    
    break;

...
```

**2-12（建议）：避免在一行代码或表达式的中间插入注释。**

说明：除非必要，不应在代码或表达中间插入注释，否则容易使代码可理解性变差。

例：

```c
char level_output_info[6][6] =
    {
        {"TRACE"}, {"DEBUG"}, /* Debug Info */ {"INFO"},
        {"WARN"}, {"ERROR"}, {"FATAL"}
    };
```

**2-13（建议）：通过对函数或过程、变量、结构等正确的命名以及合理地组织代码的结构，使代码能够自注释。**

说明：清晰准确的函数、变量等的命名，可增加代码可读性，并减少不必要的注释。

**2-14（建议）：在代码的功能、意图层次上进行注释，提供有用、额外的信息。**

说明：注释的目的是解释代码的目的、功能和采用的方法，提供代码以外的信息，帮助读者理解代码，防止没必要的重复注释信息。

示例：如下注释意义不大。

```c
char level_output_info[6][6] =
    {
        {"TRACE"}, {"DEBUG"}, /* Debug Info */ {"INFO"},
        {"WARN"}, {"ERROR"}, {"FATAL"}
    };
```

**2-15（建议）：在程序块的结束行右方加注释标记，以表明某程序块的结束。**

说明：当代码段较长，特别是多重嵌套时，这样做可以使代码更清晰，更便于阅读。

示例：参见如下例子。

```c
if (...)
{
    ...
    while (index < MAX_INDEX)
    {
        ...
    } /*while (index < MAX_INDEX) 循环结束 */ 
} /* 结束if (...)*/
```

**2-16（强制）：注释格式尽量统一，统一使用“/\* ……*/”，代码右方单行注释可以使用“//”。**

**2-17（强制）：注释应考虑程序易读及外观排版的因素，使用的语言若是中、英兼有的，统一使用中文。**

说明：注释语言不统一，影响程序易读性和外观排版，出于对维护人员的考虑，建议使用中文。

## 3 标识符命名

**3-1（强制）：标识符的命名要清晰、明了，有明确含义，同时使用完整的单词或大家基本可以理解的缩写，避免使人产生误解。**

说明：较短的单词可通过去掉“元音”形成缩写；较长的单词可取单词的头几个字母形成缩写；

示例：如下单词的缩写能够被大家基本认可。

temp 可缩写为 tmp ;

flag 可缩写为 flg ;

statistic 可缩写为 stat ;

increment 可缩写为 inc ;

message 可缩写为 msg ;

**3-2（强制）：命名中若使用特殊约定或缩写，则要有注释说明。**

说明：应该在源文件的开始之处，对文件中所使用的缩写或约定，特别是特殊的缩写，进行必要的注释说明。

**3-3（强制）：对于变量命名，禁止取单个字符（如i、j、k...），要有具体含义，但i、j、k作局部循环变量是允许的。**

说明：变量，尤其是局部变量，如果用单个字符表示，很容易敲错（如i写成j），而编译时又检查不出来，有可能为了这个小小的错误而花费大量的查错时间。

示例：如下命名不符合规范

```c
int i;
int j;
i = get_max_length();
j = get_min_length();
```

下面的命名符合规范：

```c
int max_len;
int min_ len;
max_len = get_max_length();
min_ len =get_min_length();
```

例外：i, j等单个字符作为局部循环变量使用是可以的。

```c
int max_len;
int min_ len;
max_len = get_max_length();
min_ len =get_min_length();
```

**3-4（强制）：命名规范采用UNIX命名风格。**

变量统一使用小写下划线方式命名；宏和枚举命名采用“大写+下划线”方式命名；函数统一使用小写下划线方式命名(注意：平台公共库里的函数名字前面必须加plm\_以同app自己定义的函数区分，lcp，vcp库函数也要加上lcp\_,
vcp\_)；文件名统一使用小写下划线方式命名。

示例：

变量命名（局部变量）：

```c
int max_len = 0;
```

宏命名：

```c
#define TH_MGR_MAIN    "mgr_main"
```

枚举命名：

```c
typedef enum
{
    STATION_CHN_WWAN,
    STATION_CHN_ETHER
}STATION_CHANNEL_E;
```

函数命名

```c
void plm_lcp_run()
{
     ipc_run();
}
```

文件命名：

```c
thread_monitor.c thread_monitor.h
```

**3-5（强制）：全局变量应该增加“g_”前缀，结构体定义加\_t后缀，枚举定义加\_E后缀。**

示例：

全局变量命名：

```c
app_param_t g_app_param = {0};
```

结构体命名：

```c
typedef struct
{
    bool           en_connect;
    bool           en_enc_dec;
    bool           en_dc_protocol;
    uint8_t        device_id[20];
    up_channel_t   up_channel;
    down_channel_t down_channel;
}app_param_t;
```

枚举命名：

```c
typedef enum
{
    STATION_CHN_WWAN,
    STATION_CHN_ETHER
}STATION_CHANNEL_E;
```

**3-6（建议）：除非必要，不要用数字或较奇怪的字符来定义标识符。**

示例：如下命名，使人产生疑惑。

```c
#define EXAMPLE_0_TEST
#define EXAMPLE_1_TEST
void set_sls00( uint8_t sls );
```

应改为有意义的单词命名

```c
#define EXAMPLE_UNIT_TEST
#define EXAMPLE_ASSERT_TEST
void set_udt_msg_sls( uint8_t sls )
```

**3-7（建议）：用正确的反义词组命名具有互斥意义的变量或相反动作的函数等。**

说明：下面是一些在软件中常用的反义词组。

add / remove begin / end create / destroy

insert / delete first / last get / release

increment / decrement put / get

add / delete lock / unlock open / close

min / max old / new start / stop

next / previous source / target show / hide

send / receive source / destination

cut / paste up / down

示例：

```c
int  min_sum;
int  max_sum;
int  add_user( BYTE *user_name );
int  delete_user( BYTE *user_name );
```

**3-8（建议）：除了编译开关/头文件等特殊应用，应避免使用\_EXAMPLE_TEST\_之类以下划线开始和结尾的定义。**

**3-9（建议）：函数命名应以函数要执行的动作命名，一般采用动词或者动词＋名词的结构。**

示例：参照如下方式命名函数。

```c
void print_record(unsigned int rec_ind);
int input_record(void);
unsigned char get_current_color(void);
```

## 4 变量、结构

**4-1（强制）：去掉没必要的全局变量。**

说明：全局变量是增大模块间耦合的原因之一，故应减少没必要的全局变量以降低模块间的耦合度。

**4-2（强制）：当向全局变量传递数据时，要十分小心，防止赋予不合理的值或越界等现象发生。**

说明：对全局变量赋值时，若有必要应进行合法性检查，以提高代码的可靠性、稳定性。

**4-3（强制）：防止局部变量与全局变量同名。**

说明：若使用了较好的命名规则，那么此问题可自动消除。

**4-4（强制）：严禁使用未经初始化的变量作为右值。**

说明：未初始化变量是C和C++程序中错误的常见来源。在变量首次使用前确保正确初始化。

在较好的方案中，变量的定义和初始化要做到亲密无间。

错误示例：

```c
int speedup_factor;
if (condition)
{
    speedup_factor = 2;
}
int tmp_factor = speedup_factor;
```

正确示例：

```c
int speedup_factor = -1;
if (condition)
{
    speedup_factor = 2;
}
int tmp_factor = speedup_factor;
```

**4-5（建议）：构造仅有一个模块或函数可以修改、创建，而其余有关模块或函数只访问的全局变量，防止多个不同模块或函数都可以修改、创建同一全局变量的现象。**

说明：降低全局变量耦合度。

**4-6（建议）：结构中元素的个数应适中。若结构中元素个数过多可考虑依据某种原则把元素组成不同的子结构，以减少原结构中元素的个数。**

说明：增加结构的可理解性、可操作性和可维护性。

对于如下结构：

```c
typedef struct
{
    unsigned char name[8];
    unsigned char age;
    unsigned char gender;
    unsigned char addr[40];
    unsigned char city[15];
    unsigned char tel;
} person_t;
```

如果认为结构元素过多，可以进行如下拆分：

```c
typedef struct
{
    unsigned char name[8];
    unsigned char age;
    unsigned char gender;
} person_base_info_t;

typedef struct
{
    unsigned char addr[40];
    unsigned char city[15];
    unsigned char tel;
} person_address_t;

typedef struct
{
    person_base_info_t person_base;
    person_address_t person_addr;
} person_t;
```

**4-7（建议）：仔细设计结构中元素的布局与排列顺序，使结构容易理解、节省占用空间，并减少引起误用现象。**

说明：合理排列结构中元素顺序，可节省空间并增加可理解性。

示例：如下结构中的位域排列，将占较大空间，可读性也稍差。

```c
typedef struct example_struct_s
{
     unsigned int valid: 1;
     person_t person;
     unsigned int set_flg: 1;
} example_t;
```

若改成如下形式，不仅可节省1字节空间，可读性也变好了。

```c
typedef struct example_s
{
     unsigned int valid: 1;
     unsigned int set_flg: 1;
     person_t person ;
} example_t;
```

**4-8（建议）：留心具体语言及编译器处理不同数据类型的原则及有关细节。**

说明：如在C语言中，static局部变量存储在全局/静态存储区，而非static局部变量存储在栈区。全局变量也存在全局/静态存储区。这些细节对程序质量的保证非常重要。

由于局部变量是存储在栈里的，所以函数调用时候于大的数据结构，尽量传指针，如果直接传变量有可能引起栈帧溢出，函数传参尽量多用指针。

示例：

```c
typedef struct 
{
    uint16_t tag;
    uint16_t len;
    uint8_t *data;
    uint8_t resp[MAX_BODY_BUF];
}subdata_t;

bool set_check_common_connect_station(subdata_t *request_tlv)
{
    if(request_tlv->len < 1)
    {
        return false;
    }
    return true;
}
```

**4-9（建议）：尽量减少没有必要的数据类型默认转换与强制转换。**

说明：当进行数据类型强制转换时，其数据的意义、转换后的取值等都有可能发生变化，而这些细节若考虑不周，就很有可能留下隐患。

**基本的数据类型转换规则：**

-   当出现在表达式中时，有符号和无符号的char和short类型都将自动转换为int（32位系统）\[数值提升\]。
    示例：

    ```c
    uint8_t port = 0x5aU;
    uint8_t master_ns;
    master_ns= (~port) >> 0x4;
    ```

    在此例子中，如果不了解表达式中的类型提升，认为运算过程中*port*一直是uint8\_t类型的, \~*port* 的结果为0xa5, 0xa5\>\>4结果为0x0a，这是我们的预期结果，但是由于在运算过程中，*port*被提升成了int类型, \~ *port*结果为0xffffffa5, 0xffffffa5\>\>4结果为0x0ffffffa，赋值给master_ns，发生截断，master_ns = 0xfa，跟我们预期结果不符，应做如下修改：

    ```c
    uint8_t port = 0x5aU;
    uint8_t master_ns;
    master_ns= (uint8_t)(~ port) >> 0x4;
    ```

    还有一个例子：

    ```c
    int8_t a = 0x80;
    if (a == 0x80)
    {
        printf("equal\n");
    }
    ```

    实际上不会打印equal，根据转换规则，a先转换成0xffffff80，再和0x80做比较。

-   在包含两种数据类型的任何运算中，较低级别类型将会转为运算中另一个较高级别的数据类型。

-   数据类型级别从高到低的顺序是long double、double、float、unsigned long long、long long unsigned long、long、 unsigned int、int一个可能的例外是当long和int具有相同大小时，unsigned int级别高于long，short和char由规则1被提升到int。

-   在赋值语句中，计算结果将被转换为要被赋值的那个变量的类型，这个过程可能导致级别提升(被赋值的类型级别高)或者降级(被赋值的类型级别低)，提升通常是一个平滑无损的过程，然而降级可能导致真正的问题。

-   作为函数的参数被传递时，char和short会被转为int，float转为double，但可以通过函数原型的指定阻止自动提升的发生。
    
    例：

    ```c
    long int sum_val;
    int val= 100000;
    sum_val =(long int) val * val
    ```

    val\*val的结果太大，以致于在某些机器上无法表示成int类型。
    
    强制运算符的优先级高于\*，所以第一个变量val会转换成long int，同时也迫使第二个val进行转换。
    
    注意
    
    ```c
    sum_val =(long int)( val * val)   /* 错误*/
    ```

    溢出在强制类型转换之前就己经发生了.

- 当同时需要在不同数据大小及有符号无符号之间转换时，c语言标准是先进行数据大小的转换，

  再进行有符号和无符号之前的转换，为了避免对此规则不熟悉而引起错误，应尽量不要同时进行

  数据大小和有无符号的转换。

  例:

  ```c
  uint64_t abs_value(int64_t data)
  {
      uint64_t temp;
  
      if(data>0)
      {
          temp = (uint64_t)data;
      }
      else
      {
          temp = (uint64_t)(0 - data);
      }
  
      return temp;
  }
  
  uint32_t freq_delt;
  uint32_t val1 = 0;
  uint32_t val2 = 1;
  freq_delt=(uint32_t)(abs_value((int64_t)(val1 - val2)));
  ```

  此示例的预期是val1-val2=-1，取绝对值得到freq_delt为1，但是，由于先进行了数据大小的转换, val1-val2结果为0xffffffff，首先转化成为了uint64\_t类型，为0x00000000ffffffff，再转为为int64_t，最终结果为0x00000000ffffffff，取绝对值为结果为0x00000000ffffffff，再转化为uint32_t赋值给
  *freq_delt，发生截断，freq_delt=0x*ffffffff，与预期结果不符，如果是新增代码，建议修改如下：

  ```c
  ...
  uint32_t freq_delt;
  int64_t val1 = 0;
  int64_t val2 = 1;
  freq_delt=(uint32_t)(abs_value(val1 - val2));
  ```

  如果是在老代码基础上修改，val1和val2的数据类型无法修改，最后一行代码建议修改如下：

  ```c
  freq_delt=(uint32_t)(abs_value((int64_t)((uint64_t) val1 - (uint64_t) val2)));
  ```

**4-10（建议）：明确全局变量的初始化顺序，避免跨模块的初始化依赖。**

说明：系统启动阶段，使用全局变量前，要考虑到该全局变量在什么时候初始化，使用全局变量和初始化全局变量，两者之间的时序关系，谁先谁后，一定要分析清楚。

**4-11（强制）：禁止使用位置对应赋值方式对结构体变量进行初始化。**

说明：结构体变量初始化方式可以分为三种：位置对应赋值，点号访问赋值和冒号指示赋值方式。

示例：

结构体定义

```c
typedef struct channel_service_t
{
    uint8_t have_net_channel;
    uint8_t recv_thread_running;
    uint8_t recv_thread_stop_en;
    uint8_t recv_thread_stop_ok;
    uint8_t send_thread_running;
    uint8_t send_thread_stop_en;
    uint8_t send_thread_stop_ok;
    int     epoll_wait_time;
    int64_t bypassing;                 //是否有未bypass完的数据
    linux_fast_csem_t send_sem;       //发送线程使用的信号量
    pthread_mutex_t socket_mutex;    //socket线程互斥锁
}chn_service_t;
```

位置对应赋值

```c
chn_service_t g_chn_service = 
{
    0, 
    0, 
    0, 
    0, 
    0, 
    0, 
    0, 
    EPOLL_WAIT_TIME, 
    0, 
    {PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER, 0, 0}, 
    PTHREAD_MUTEX_INITIALIZER
};
```

按序列未列出的即为无关参数，但是缺省数必须排在最后, 如果中间参数缺省，则会发生错误；

```c
chn_service_t g_chn_service = 
{
    EPOLL_WAIT_TIME, 
    0, 
    {PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER, 0, 0}, 
    PTHREAD_MUTEX_INITIALIZER
};
```

点号访问赋值, 可以只对感兴趣的参数赋值，无关参数缺省，赋值项清晰明了

```c
chn_service_t g_chn_service = 
{
    .have_net_channel = 0,
    .recv_thread_running = 0, 
    .recv_thread_stop_en = 0, 
    .recv_thread_stop_ok = 0, 
    .send_thread_running = 0, 
    .send_thread_stop_en = 0, 
    .send_thread_stop_ok = 0, 
    .epoll_wait_time = EPOLL_WAIT_TIME, 
    .bypassing = 0, 
    .send_sem = {PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER, 0, 0}, 
    .socket_mutex = PTHREAD_MUTEX_INITIALIZER
};
```

冒号指示赋值

```c
chn_service_t g_chn_service = 
{
    have_net_channel : 0,
    recv_thread_running : 0, 
    recv_thread_stop_en : 0, 
    recv_thread_stop_ok : 0, 
    send_thread_running : 0, 
    send_thread_stop_en : 0, 
    send_thread_stop_ok: 0, 
    epoll_wait_time : EPOLL_WAIT_TIME, 
    bypassing : 0, 
    send_sem : {PTHREAD_MUTEX_INITIALIZER, PTHREAD_COND_INITIALIZER, 0, 0}, 
    socket_mutex : PTHREAD_MUTEX_INITIALIZER
};
```

## 5 函数、过程

**5-1（强制）：对所调用函数的错误返回码要仔细、全面地处理。**

错误示例：

```c
int8_t plm_enable_ctrl_module()
{
    int32_t ret;

    (void)plm_gpio_pin_dir_out(CTRL_EN);

    ret = plm_gpio_pin_write(CTRL_EN,PIN_HIGH);
    return ret;
}
```

正确示例：

```c
int8_t plm_enable_ctrl_module()
{
    int32_t ret;

    ret = plm_gpio_pin_dir_out(CTRL_EN);
    if (ret == TOPS_OK)
    {
        ret = plm_gpio_pin_write(CTRL_EN,PIN_HIGH);
        return ret;
    }
    else
    {
        return TOPS_ERR;
    }
}
```

**5-2（强制）：编写可重入函数时，若使用共享变量，则应通过关中断、信号量等手段对其加以保护。**

说明：若对所使用的共享变量不加以保护，则此函数就不具有可重入性，即当多个线程调用此函数时，很有可能使有关共享变量变为不可知状态。共享变量指的是全局变量和static变量

示例：假设exam是int型全局变量，函数square\_exam返回exam平方值。那么如下函数不具有可重入性。

```c
unsigned int example( int para )
{
    unsigned int temp;

    exam = para; 			/* （**） */
    temp = square_exam( );

    return temp;
}
```

此函数若被多个线程调用的话，其结果可能是未知的，因为当（**）语句刚执行完后，另外一个使用本函数的线程可能正好被激活，那么当新激活的线程执行到此函数时，将使exam赋与另一个不同的para值，所以当控制重新回到“temp= square\_exam( )”后，计算出的temp很可能不是预想中的结果。此函数应如下改进。

```c
unsigned int example( int para )
{
    unsigned int temp;

   /* 
    * 若申请不到“信号量”，说明另外的进程正处于
    * 给Exam赋值并计算其平方过程中（即正在使用此
    * 信号），本进程必须等待其释放信号后，才可继
    * 续执行。若申请到信号，则可继续执行，但其
    * 它进程必须等待本进程释放信号量后，才能再使
    * 用本信号。
    */

    //[申请信号量操作]
    exam = para;
    temp = square_exam( );
    //[释放信号量操作]  
    return temp;
}
```

**5-3（强制）：接口函数参数的合法性检查由接口函数本身负责。**

说明：对于模块间接口函数的参数的合法性检查这一问题，往往有两个极端现象，即：要么是调用者和被调用者对参数均不作合法性检查，结果就遗漏了合法性检查这一必要的处理过程，造成问题隐患；要么就是调用者和被调用者均对参数进行合法性检查，这种情况虽不会造成问题，但产生了冗余代码，降低了效率。

示例：

```c
int32_t gpio_init(PIN_NUM pin_num)
{
    int32_t fd_loc = -1;

    if(pin_num >= GPIO_MAX)
    {
        return TOPS_ERR;
    }
    ...
}
```

**5-4（强制）：防止将函数的参数作为工作变量。**

说明：将函数的参数作为工作变量，有可能错误地改变参数内容，所以很危险。对必须改变的参数，最好先用局部变量代之，最后再将该局部变量的内容赋给该参数。

示例：下函数的实现不太好。

```c
void sum_data( unsigned int num, int *data, int *sum )
{
    unsigned int count;
    
    *sum = 0;
    for (count = 0; count < num; count++)
    {
        *sum  += data[count];  /*sum成了工作变量，不太好*/
    }
}
```

若改为如下，则更好些。

```c
void sum_data( unsigned int num, int *data, int *sum )
{
    unsigned int count ;
    int sum_temp;
    
    sum_temp = 0;
    for (count = 0; count < num; count ++)
    {
        sum_temp  += data[count]; 
    }
    
    *sum = sum_temp;
}
```

**5-5（建议）：函数的规模不超过200行。**

说明：不包括注释和空格行*。*

**5-6（强制）：一个函数仅完成一件功能。**

说明：非调度函数应减少或防止控制参数，尽量只使用数据参数。本建议目的是防止函数间的控制耦合。调度函数是指根据输入的消息类型或控制命令，来启动相应的功能实体（即函数或过程），而本身并不完成具体功能。控制参数是指改变函数功能行为的参数，即函数要根据此参数来决定具体怎样工作。非调度函数的控制参数增加了函数间的控制耦合，很可能使函数间的耦合度增大，并使函数的功能不唯一。

示例：如下函数构造不太合理。

```c
int add_sub( int a, int b, unsigned char add_sub_flg )
{
    if (add_sub_flg == INTEGER_ADD)
    {
        return (a + b);
    }
    else
    {
        return (a - b);
    }
}
```

不如分为如下两个函数清晰。

```c
int add( int a, int b )
{
    return (a + b);
}

int sub( int a, int b ) 
{
    return (a - b);
}
```

**5-7（建议）：函数应避免使用全局变量、静态局部变量和I/O操作，不可避免的地方应集中使用。**

说明：带有内部“存储器”的函数的功能可能是不可预测的，因为它的输出可能取决于内部存储器（如某标记）的状态。这样的函数既不易于理解又不利于测试和维护。在C语言中，函数的static局部变量是函数的内部存储器，有可能使函数的功能不可预测，然而，当某函数的返回值为指针类型时，则必须是STATIC的局部变量的地址作为返回值。

示例：如下函数，其返回值（即功能）是不可预测的。

```c
unsigned int integer_sum( unsigned int base )
{
    unsigned int index;
    static unsigned int sum = 0; 	

    for (index = 1; index <= base; index++)
    {
        sum += index;
    }

    return sum;
}
```

应改为如下：

```c
unsigned int integer_sum( unsigned int base )
{
    unsigned int index;
    unsigned int sum = 0; 	

    for (index = 1; index <= base; index++)
    {
        sum += index;
    }

    return sum;
}
```

**5-8（建议）：函数的参数个数不超过5个。**

说明：目的减少函数间接口的复杂度。

**5-9（建议）：检查函数所有非参数输入的有效性，如数据文件、全局变量等。**

说明：函数的输入主要有两种：一种是参数输入；另一种是全局变量、数据文件的输入，即非参数输入。函数在使用输入之前，应进行必要的检查。

示例：

```c
int *g_score_list = NULL;
...
int acquire_score_by_index(uint32_t index)
{
    int score_val ;
    if(g_score_list == NULL)
    {
        return  TOPS_ERROR;
    }
    .../*具体的处理*/
    return score_val;
}
```

**5-10（建议）：函数的返回值要清楚、明了，让使用者不容易忽视错误情况。**

说明：函数的每种出错返回值的意义要清晰、明了、准确，防止使用者误用、理解错误或忽视错误返回码。

**5-11（强制）：废弃代码（没有被调用的函数和变量）要及时清除。**

说明：程序中的垃圾代码不仅占用额外的空间，而且还常常影响程序的功能与性能，很可能给程序的测试、维护等造成不必要的麻烦。

**5-12（建议）：重复代码应该尽可能提炼成函数。**

说明：若此段代码各语句之间有实质性关联并且是完成同一件功能的，那么可考虑把此段代码构造成一个新的函数。

**5-13（强制）：设计高扇入、合理扇出（小于7）的函数。**

说明：扇出是指一个函数直接调用（控制）其它函数的数目，而扇入是指有多少上级函数调用它。

扇出过大，表明函数过分复杂，需要控制和协调过多的下级函数；而扇出过小，如总是1，表明函数的调用层次可能过多，这样不利程序阅读和函数结构的分析，并且程序运行时会对系统资源如堆栈空间等造成压力。函数较合理的扇出（调度函数除外）通常是3-5。扇出太大，一般是由于缺乏中间层次，可适当增加中间层次的函数。扇出太小，可把下级函数进一步分解多个函数，或合并到上级函数中。当然分解或合并函数时，不能改变要实现的功能，也不能违背函数间的独立性。

扇入越大，表明使用此函数的上级函数越多，这样的函数使用效率高，但不能违背函数间的独立性而单纯地追求高扇入。公共模块中的函数及底层函数应该有较高的扇入。

较良好的软件结构通常是顶层函数的扇出较高，中层函数的扇出较少，而底层函数则扇入到公共模块中。

**5-14（建议）：减少函数本身或函数间的递归调用。**

说明：递归调用特别是函数间的递归调用（如A-\>B-\>C-\>A），影响程序的可理解性；递归调用一般都占用较多的系统资源（如栈空间）；递归调用对程序的测试有一定影响。故除非为某些算法或功能的实现方便，应减少没必要的递归调用。

**5-15（建议）：当一个过程（函数）中对较长变量（一般是结构的成员）有较多引用时，可以用一个意义相当的宏代替, 且定义在离过程（函数）比较近的位置。**

说明：这样可以增加编程效率和程序的可读性。

示例：在某过程中较多引用*TheReceiveBuffer[FirstSocket].byDataPtr，*

则可以通过以下宏定义来代替：

```c
# define pSOCKDATA TheReceiveBuffer[FirstScoket].byDataPtr
```

**5-16（强制）：避免函数的代码块嵌套过深，新增函数的代码块嵌套不超过4层。**

如下是一个不好的例子：

```c
if(lxc_info != NULL )
    {
        cJSON *client_list_lxc  = lxc_info->child;
        while( client_list_lxc != NULL )
        {
            if(strcmp(c_local_name, container) == 0)
            {
                    /*container_name 所包含 app 的信息*/
                cJSON *app_info = cJSON_GetObjectItem( client_list_lxc, "apps");  
                if( NULL != app_info )
                {
                    cJSON *client_list_app = app_info->child;
                    while( client_list_app != NULL )
                    {
                            if(srv_info != NULL)
                            {
                                cJSON *client_list_srv = srv_info->child;
                                while( client_list_srv != NULL )
                                {
                                    static_info_ptr->srv_num ++;
                                    ...
                                }
                            }
                        }
                        client_list_app = client_list_app->next;
                        round ++;
                    }
                    break;
                }
            }
            client_list_lxc = client_list_lxc->next;
        }
```

减少嵌套的建议方法：

1.  对于if else语句，可以先判断相反条件，例如：

```c
void func_test(int a, int b)
{
 
    if(a > 10)
    {
        ...... 
    }
    else
    {
        return;
    }
}
```

可以改成：

```c
    void func_test(int a, int b)
    {
    
         if(a <= 10)
         {
            return;
             
         }
         
        ......
    }
```

2.比较复杂的功能提炼成函数。

**5-17（建议）：函数不变参数加const。**

**5-18（建议）：在文件范围内声明和定义的所有对象或者函数应除非外部可见，否则应加static。**



## 6 头文件

**6-1（强制）：每一个.c文件都应该有一个同名的.h文件，用于声明需要对外公开的接口。**

如果一个.c文件不需要对外公开任何接口，那么其就不应该存在，除非它是程序的入口，比如main函数；

**6-2（强制）：禁止头文件循环依赖。**

说明： 头文件循环依赖，指a.h包含b.h， b.h包含c.h，
c.h包含a.h之类导致任何一个头文件修改，都导致所有包含了a.h/b.h/c.h的代码全部重新编译一遍。而如果是单向依赖，如a.h包含b.h，
b.h包含c.h，而c.h不包含任何头文件，则修改a.h不会导致包含了b.h/c.h的源代码重新编译。

**6-3（强制）：.c/.h文件禁止包含用不到的头文件。**

说明：
很多系统中头文件包含关系复杂，开发人员为了省事起见，可能不会去一一钻研，直接包含一切想到的头文件，甚至有些产品干脆发布了一个god.h，其中包含了所有头文件，然后发布给各个项目组使用，这种只图一时省事的做法，导致整个系统的编译时间进一步恶化，并对后来人的维护造成了巨大的麻烦。

**6-4（强制）：头文件应当自包含。**

说明： 简单的说，自包含就是任意一个头文件均可独立编译。
如果一个文件包含某个头文件，还要包含另外一个头文件才能工作的话，就会增加交流障碍，给这个头文件的用户增添不必要的负担。

示例：

如果a.h不是自包含的，需要包含b.h才能编译，会带来的危害：

每个使用a.h头文件的.c文件，为了让引入的a.h的内容编译通过，都要包含额外的头文件b.h。

额外的头文件b.h必须在a.h之前进行包含，这在包含顺序上产生了依赖。

注意：该规则需要与“.c/.h文件禁止包含用不到的头文件”规则一起使用，不能为了让a.h自包含，

而在a.h中包含不必要的头文件。
a.h要刚刚可以自包含，不能在a.h中多包含任何满足自包含之外的其他头文件。

**6-5（强制）：头文件总是编写内部\#define保护符。**

说明：通常的手段就是为每个文件配置一个宏，当头文件第一次被包含时就定义这个宏，并在头文件被再次包含时使用它以排除文件内容。定义保护符时，应该遵守如下规则：1）保护符使用唯一名称；2）不要在受保护部分的前后放置代码或者注释；3）保护符命名规则为\_文件名大写\_H\_，例如文件名为ini.param.h的头文件的保护符应命名为\_INI_PARAM_H\_

**6-6（强制）：禁止在头文件中定义变量。**

说明：
在头文件中定义变量，将会由于头文件被其他.c文件包含而导致变量重复定义。

**6-7（强制）：只能通过包含头文件的方式使用其他.c提供的接口，禁止在.c中通过extern的方式使用外部函数接口、变量。**

说明：若a.c中使用了b.c定义的foo()函数，则应当在b.h中声明该函数，并在a.c中通过\#include "b.h"来使用foo。
禁止通过在a.c中直接extern int foo();来使用foo，后面这种写法容易在foo改变时可能导致声明和定义不一致。

错误示例：有三个文件，example.h，example.c和test.c，example.c编译到libexample.so里面，test.c通过链接libexample.so来调用其中的库函数。

```c
//example.h
int foo(int param1, int param2);

example.c 
#include "example.h"
int foo(int param1, int param2)
{
    ...
}

//test.c
extern int foo(int param1, int param2);

int test()
{
    int ret;
    ...
    ret = foo(num1, num2);
}  

//test.c 应做如下修改
#include "example.h"
int test()
{
    int ret;
    ...
    ret = foo(num1, num2);
}
```

如果错误示例中的方式，当lib库中的foo函数参数或者返回值改变时，在test.c中
extern的地方忘记修改时，编译时不会报错，运行时才会报错。

## 7 表达式

**7-1（强制）：表达式的值在标准允许的任何运算次序下都应该是相同的。**

说明：除了少数操作符（函数调用操作符 ( )、 &&、 \| \|、 ? : 和 , （逗号））
之外，子表达式所依据的运算次序是未指定的并会随时更改。注意，运算次序的问题不能使用括号来解决，因为这不是优先级的问题。将复合表达式分开写成若干个简单表达式，明确表达式的运算次序，就可以有效消除非预期副作用。

-   自增或自减操作符  
    示例：
    ```c
    x = b[i] + i++;
    ```
    b[i] 的运算是先于还是后于 i ++的运算，表达式会产生不同的结果，把自增运算做为单独的语句，可以避免这个问题。
    
    ```c
    x = b[i] + i;
    i ++;
    ```

-   函数参数  
    说明：函数参数通常从右到左压栈，但函数参数的计算次序不一定与压栈次序相同。  
    示例：

    ```c
    x = func( i++, i);
    ```

    应该修改代码明确先计算第一个参数：

    ```c
    i++;
    x = func(i, i);
    ```

-   函数指针  
    说明：函数参数和函数自身地址的计算次序未定义。  
    示例：

    ```c
    p->task_start_fn(p++);
    ```

    求函数地址p与计算p++无关，必须单独计算p++：

    ```c
    p->task_start_fn(p);
    p++;
    ```

-   函数调用  
    函数在被调用时可以具有附加的作用（如，修改某些全局数据）。可以通过在使用函  
    数的表达式之前调用函数并为值采用临时变量的方法避免对运算次序的依赖。  
    例如
    
    ```c
    x = f (a) + g (a);
    ```

    可以写成
    
    ```c
    x = f (a);
    x += g (a);
    ```

-   嵌套赋值语句  
    说明：表达式中嵌套的赋值可以产生附加的副作用。不给这种能导致对运算次序的依赖提供任何机会的最好做法是，不要在表达式中嵌套赋值语句。  
    示例：
    
    ```c
    x = y = y = z / 3;
    x = y = y++;
    ```
    
-   volatile访问  
    说明：限定符volatile表示可能被其它途径更改的变量，例如硬件自动更新的寄存器。编译器不会优化对volatile变量的读取。示例：下面的写法可能无法实现作者预期的功能：  
    ```c
    volatile uint16_t v;
    uint16_t x = (v << 3) | v;
    x = v;
    ```

​    

**7-2（建议）：函数调用不要作为另外一个函数的参数使用。**

说明： 如下代码不合理，仅用于说明当函数作为参数时，由于参数压栈顺序不是代码可以控制的，可能造成未知的输出：

```c
int g_var;
int fun1()
{
    g_var += 10;
    return g_var;
}
int fun2()
{
    g_var += 100;
    return g_var;
}
int main(int argc, char *argv[], char *envp[])
{
    g_var = 1;
    printf("func1: %d, func2: %d\n", fun1(), fun2());
    g_var = 1;
    printf("func2: %d, func1: %d\n", fun2(), fun1());
}
```

main函数作如下修改则更合理：

```c
int main(int argc, char *argv[], char *envp[])
{
    int ret_fun1, ret_fun2;
    g_var = 1;
    ret_fun1 = fun1();
    ret_fun2 = fun2(); 
    printf("func1: %d, func2: %d\n", ret_fun1, ret_fun2);

    g_var = 1;
    ret_fun2 = fun2();
    ret_fun1 = fun1();
    printf("func2: %d, func1: %d\n", ret_fun2, ret_fun1);
}
```



**7-3（强制）：赋值语句不要写在if等语句中，或者作为函数的参数使用。**

说明：
因为if语句中，会根据条件依次判断，如果前一个条件已经可以判定整个条件，则后续条件语句不会再运行，所以可能导致期望的部分赋值没有得到运行。

示例：

```c
int main(int argc, char *argv[], char *envp[])
{
    int a = 0;
    int b;
    if ((a == 0) || ((b = fun1()) > 10)))
    {
        printf("a: %d\n", a);
    }
    printf("b: %d\n", b);
}
```

以下为一个正确的示例：

```c
int main(int argc, char *argv[], char *envp[])
{
    int a = 0;
    int b = fun1();
    if ((a == 0) || b > 10))
    {
        printf("a: %d\n", a);
    }
    printf("b: %d\n", b);
}
```

作用函数参数来使用，参数的压栈顺序不同可能导致结果未知。

**7-4（建议）：不要过分依赖** C **表达式中的运算符优先规则。**

说明：括号的使用除了可以覆盖缺省的运算符优先级以外，还可以用来强调所使用的运算符。使用相当复杂的C运算符优先级规则很容易引起错误，那么这种方法就可以帮助避免这样的错误，并且可以使得代码更为清晰可读。然而，过多的括号会分散代码使其降低了可读性。

-   一元操作符，不需要使用括号

    ```c
    x = ~a; /* 一元操作符，不需要括号*/
    x = -a; /* 一元操作符，不需要括号*/
    ```
    
-   二元以上操作符，如果涉及多种操作符，则应该使用括号 

    ```c
    x = a + b + c; /* 操作符相同，不需要括号*/
    x = (a * 3) + c + d; /* 操作符不同，需要括号*/
    ```

-   即使所有操作符都是相同的，如果涉及类型转换或者量级提升，也应该使用括号控制计算的次序以下代码将3个浮点数相加：

   ```c
   /* 除了逗号(,)，逻辑与(&&)，逻辑或(\|\|)之外，
   C标准没有规定同级操作符是从左还是从右开始计算，以上表达式存在两种计算次序：
   f4 = (f1 + f2) + f3 或f4 = f1 + (f2 +
   f3)，浮点数计算过程中可能四舍五入，量级提升，计算次序的不同会导致f4的结果不同，以上表达式在不同编译器上的计算结果可能不一样，建议增加括号明确计算顺序
   */
   f4 = f1 + f2 + f3;
   ```

**7-5（建议）：赋值运算符不能使用在产生布尔值的表达式上。**

说明：如果布尔值表达式需要赋值操作，那么赋值操作必须在操作数之外分别进行。
这可以帮助避免=和= =的混淆，帮助我们静态地检查错误。

示例：

```c
x = y;
if (x != 0)
{
    foo ();
}
```

不能写成：

```c
if (( x = y ) != 0)
{
    foo ();
}
```

或者更坏的

```c
if (( x = y ) != 0)
{
    foo ();
}
```

**7-6（建议）：不要使用难懂的技巧性很高的语句，除非很有必要时。**

说明：高技巧语句不等于高效率的程序，实际上程序的效率关键在于算法。

示例：如下表达式，考虑不周就可能出问题，也较难理解。

```c
* stat_poi ++ += 1;
++ *stat_poi += 1;
```

应分别改为如下。

```c
*stat_poi += 1;
stat_poi++;     /* 此二语句功能相当于 " * stat_poi ++ += 1; " */

++ stat_poi;
*stat_poi += 1; /* 此二语句功能相当于 " ++ *stat_poi += 1; " */
```

## 8 宏、常量

**8-1（强制）：用宏定义表达式时，要使用完备的括号。**

说明：因为宏只是简单的代码替换，不会像函数一样先将参数计算后，再传递。

示例：如下定义的宏都存在一定的风险

```c
#define RECTANGLE_AREA(a, b) a * b
#define RECTANGLE_AREA(a, b) (a * b)
#define RECTANGLE_AREA(a, b) (a) * (b)
```

正确的定义应为：

```c
#define RECTANGLE_AREA(a, b) ((a) * (b))
```

这是因为：

如果定义*\#define RECTANGLE_AREA(a, b) a \* b*

则*c/RECTANGLE_AREA(a, b)* 将扩展成*c/a \* b* , c 与b
本应该是除法运算，结果变成了乘法运算，造成错误。

如果定义*\#define RECTANGLE_AREA(a, b) (a \* b)*

则*RECTANGLE_AREA(c + d, e + f)*将扩展成： *(c + d \* e + f)*, d与e
先运算，造成错误。

**8-2（强制）：将宏所定义的多条表达式放在大括号中。**

说明：更好的方法是多条语句写成do while(0)的方式。

示例：看下面的语句，只有宏的第一条表达式被执行。

```c
#define FOO(x) \
printf("arg is %d\n", x); \
do_something_useful(x);
```

为了说明问题， 下面for语句的书写稍不符规范

```c
for (blah = 1; blah < 10; blah++)
    FOO(blah)
```

用大括号定义的方式可以解决上面的问题： 

```c
#define FOO(x) { \
printf("arg is %s\n", x); \
do_something_useful(x); \
}
```

但是如果有人这样调用： 

```c
if (condition == 1)
    FOO(10);
else
    FOO(20);
```

那么这个宏还是不能正常使用，所以必须这样定义才能避免各种问题：

```c
#define FOO(x) do { \
printf("arg is %s\n", x); \
do_something_useful(x); \
} while(0)
```

用do-while(0)方式定义宏，完全不用担心使用者如何使用宏，也不用给使用者加什么约束。

**8-3（强制）：使用宏时，不允许参数发生变化。**

示例：如下用法可能导致错误。

```c
#define SQUARE(a) ((a) * (a))
int a = 5;
int b;
b = SQUARE(a++); // 结果： a = 7，即执行了两次增。
```

正确的用法是：

```c
b = SQUARE(a);
a++; // 结果： a = 6，即只执行了一次增。
```

同时也建议即使函数调用，也不要在参数中做变量变化操作，因为可能引用的接口函数，在某个版本升级后，变成了一个兼容老版本所做的一个宏，结果可能不可预知。

**8-4（强制）：不允许直接使用魔鬼数字。**

说明：使用魔鬼数字的弊端：代码难以理解；如果一个有含义的数字多处使用，一旦需要修改这个数值，代价惨重。

使用明确的物理状态或物理意义的名称能增加信息，并能提供单一的维护点。

解决途径：

对于局部使用的唯一含义的魔鬼数字，可以在代码周围增加说明注释，也可以定义局部const变量，变量命名自注释。

对于广泛使用的数字，必须定义const全局变量/宏；同样变量/宏命名应是自注释的。

0作为一个特殊的数字，作为一般默认值使用没有歧义时，不用特别定义。

如下是一个不太好的例子：

```c
int compute_default_area()
{
    int temp_are;
    temp_area = 42*36;
    return temp_area;
}
```

建议做如下修改：

```c
#define DEFAULT_LENGTH    42
#define DEFAULT_WIDTH     36
int compute_default_area()
{
    int temp_are;
    temp_area = DEFAULT_LENGTH * DEFAULT_WIDTH;
    return temp_area;
}
```

**8-5（建议）：除非必要，应尽可能使用函数代替宏。**

说明：宏对比函数，有一些明显的缺点：

宏缺乏类型检查，不如函数调用检查严格。

宏展开可能会产生意想不到的副作用，如\#*define SQUARE(a) (a) \*
(a)*这样的定义，如果是*SQUARE(i++)*，就会导致i被加两次；如果是函数调用*double
square(double a) {return a \* a;}*则不会有此副作用。

以宏形式写的代码难以调试难以打断点，不利于定位问题。

宏如果调用的很多，会造成代码空间的浪费，不如函数空间效率高。

示例：下面的代码无法得到想要的结果：

```c
#define MAX_MACRO(a, b) ((a) > (b) ? (a) : (b))
int max_func(int a, int b)
{
    return ((a) > (b) ? (a) : (b));
}
int test_func()
{
    unsigned int a = 1;
    int b = -1;
    printf("MACRO: max of a and b is: %d\n", MAX_MACRO(++a, b));
    printf("FUNC : max of a and b is: %d\n", max_func(a, b));
    return 0;
}
```

上面宏代码调用中，结果是(a \< b)，所以a只加了一次，所以最终的输出结果是：

MACRO: max of a and b is: -1*

FUNC : max of a and b is: 2*

**8-6（建议）：宏定义中尽量不使用return、 goto、 continue、break等改变程序流程的语句。**

说明：如果在宏定义中使用这些改变流程的语句，很容易引起资源泄漏问题，使用者很难自己察觉。

示例：在某头文件中定义宏*CHECK_AND_RETURN：*

```c
#define CHECK_AND_RETURN(cond, ret) {if (cond == NULL) {return ret;}}
```

然后在某函数中使用(只说明问题，代码并不完整):

```c
p_mem1 = malloc(...);
CHECK_AND_RETURN(p_mem1 , ERR_CODE_XXX)
p_mem2 = malloc(...);
CHECK_AND_RETURN(p_mem2, ERR_CODE_XXX) /*此时如果p_mem2==NULL_PTR，则p_mem1未释放函数就返回了，造成内存泄漏。 */
```

所以说，类似于*CHECK_AND_RETURN*这些宏，虽然能使代码简洁，但是隐患很大，使用须谨慎。

## 9 安全性

**9-1（强制）：指向资源句柄或描述符的变量，在资源释放后立即赋予新值。**

说明：资源释放后，对应的变量应该立即赋予初值，防止后续又被重新引用。

示例1：

```c
char *msg = NULL;
msg = malloc(...);
...
free(msg);
msg = NULL; //msg变量又被赋予新值；
```

示例2（linux 平台）：

```c
int fd = -1;
fd = open(path);
...
close(fd);
fd = -1;
```

**9-2（强制）：严禁对指针变量进行sizeof操作。**

说明：将指针误当数组进行sizeof操作，往往会导致实际的结果与预期不符。下面的代码，buffer

和path分别是指针和数组，编码人员想对这两个内存进行清0操作，但是由于编码人员的疏忽，

第5行代码将内存大小误写成了sizeof，与预期不符。

示例：

```c
char *buffer = malloc(size);
char path[MAX_PATH] = {0};
...
memset(path, 0, sizeof(path));
memset(buffer, 0, sizeof(buffer));
```

如果要判断当前指针类型的大小，请使用sizeof(char \*);

注意，数组作为参数传递时本质上也是传的指针。

**9-3（强制）：数组作为函数参数时，必须同时将其长度作为函数的参数。**

说明：通过函数参数传递数组或一块内存进行写操作时，函数参数必须同时传递数组元素的个数或者所传递内存块的大小，否则在使用数组下表或者访问内存偏移时，无法判断下标或者偏移的合法范围，产生越界访问的漏洞，且coverity无法扫描到此错误。以下代码中，函数parse_msg不知道msg的范围，容易产生内存访问越界的漏洞。

下面是一个不好的例子：

```c
int parse_msg(char * msg)
{
}
...
int len = ...;
char * msg = malloc(len);
...
parse_msg(msg);
```

正确的做法是将msg的大小作为参数传递到parse_msg中：

```c
int parse_msg(char * msg, int len)
{
}
...
int len = ...;
char * msg = malloc(len);
...
parse_msg(msg, len);
```

msg是固定长度数组时，也必须将数组大小作为函数的参数：

```c
int parse_msg(char * msg, int len)
{
}
...
int len = ...;
char msg[MAX_MSG_LEN] = {0};
...
parse_msg(msg, len);
```

对于const char\*类型的参数，它的长度可以通过”\\0”的位置算出来，可以不用传递参数

```c
int parse_msg(const char * msg)
{
}
...
const char * msg = "msgmsg";
...
parse_msg(msg);
```

如果一个函数中需要多次访问数组不同下标或者内存不同偏移，无法一次进行合法性判断，可以分多次进行，但必须在每一次访问之前做判断

```c
int fill_in_oop_top_result(const TOPOLOGY_RESULT *result, uint8_t *buf, uint8_t max_len)
{
    uint32_t pos = 0;
    uint32_t tmp;

    //此检查是为了防止标注1的代码越界
    if(pos + 2 >= max_len) //头部信息长度为2
    {
        return pos;
    }

    //此段代码为标注1
    buf[pos++] = DT_STRUCTURE;
    buf[pos++] = 7;

    //此检查是为了防止标注2的代码越界
    if(pos + 8 >= max_len) //识别时间信息长度为8
    {
        return pos;
    }

    //识别时间
    //此段代码为标注2
    buf[pos++] = DT_DATETIME_S;
    tmp = 2000 + result->time.year;
    buf[pos++] = (tmp >> 8) & 0xFF;
    buf[pos++] = tmp & 0xFF;
    buf[pos++] = result->time.mon;
    buf[pos++] = result->time.day;
    buf[pos++] = result->time.hour;
    buf[pos++] = result->time.min;
    buf[pos++] = result->time.sec;

    //此检查是为了防止标注3的代码越界
    if(pos + 2 >= max_len) //相位信息长度为2
    {
        return pos;
    }

    //相位
    //此段代码为标注3
    buf[pos++] = DT_ENUM;
    buf[pos++] = result->channel;

    ...

    return pos;
}
```

如果函数实现中需要修改函数出参buffer所需长度，修改者须负责检查调用者传递的buffer长度是否足够大。

比如，下面的例子中，parse_msg函数中本来需要的buffer长度为2。

```c
int parse_msg(char * msg, int len)
{
    int pos = 0;

    if(len < 2)
    {
        return pos;
    }

    msg[pos++] = 'a';
    msg[pos++] = 'b';

    return pos
}

...

int msg_process()
{
    int ret = 0;
    ...
    char msg[2] = {0};
    ret = parse_msg(msg, 2);
    ...
}
```

如果parse_msg函数中所需要的msg的长度增大，变为3，msg_process函数中分配的buffer长度就不够了

```c
int parse_msg(char * msg, int len)
{
    int pos = 0;

    if(len < 2)
    {
        return pos;
    }

    msg[pos++] = 'a';
    msg[pos++] = 'b';
    msg[pos++] = 'c';

    return pos
}
```

此时，parse_msg函数的修改者需要负责检查调用parse_msg函数的msg_process函数中传递的buffer是否够大，如果不够大，需要进行修改

```c
int msg_process()
{
    int ret = 0;
    ...
    char msg[3] = {0};
    ret = parse_msg(msg, 3);
    ...
}
```



**9-4（强制）：不对内容进行修改的指针型参数，定义为const。**

如果参数是指针型参数，且内容不会被修改，请定义为const类型。

示例：

```c
int foo(const char *file_path)
{
    ...
   int fd = open(file_path,...);
    ...
}
```

**9-5（强制）：为了防止数组越界，在定义数组时，分配空间要大于可能存储的最大长度，留有余量，并注释说明数组大小的依据，对于长度不能确定的，要评审决定。**

部分字符串处理函数由于设计时安全考虑不足，或者存在一些隐含的目的缓冲区长度要求，使用时容易出现错误，导致缓冲区写溢出。

以下的代码， str的长度太小了，可能会溢出。

```c
int num = ...;
char str[8] = {0};
itoa(num, str, 10); //10进制整数的最大存储长度是12个字节
```

如下是gprs中的一段代码，at_cmd_buff的长度为64，GPRS_info.gprs_ppp_user
和GPRS_info.gprs_ppp_password的最大可能长度是33，所以可能会溢出:

```c
#define AT_CMD_BUFF_LEN  64
char at_cmd_buff[AT_CMD_BUFF_LEN] = {0};
if(GPRS_info.nonuse_1376_3_cmd != 0xAA)
{
    memset(at_cmd_buff, 0, sizeof(at_cmd_buff));
    snprintf(at_cmd_buff, AT_CMD_BUFF_LEN , "AT$MYNETCON=0,\"USERPWD\",\"%s,%s\"\r",
            ((GPRS_info.gprs_ppp_user[0] == 0)?"card":GPRS_info.gprs_ppp_user),
            ((GPRS_info.gprs_ppp_password[0] == 0)?"card":(GPRS_info.gprs_ppp_password)));
    chat(GPRS_info.uart_dlc1_fd, at_cmd_buff, recv_buff, sizeof(recv_buff), delay_second);
}
```



正确做法应该在at_cmd_buff定义的时候思考最大可能长度，分配的长度要大于最大长度，留有余量，并且要注释说明数组大小依据，如果长度不能确定，需评审确定。可参照如下示例修改；

```c
/*由于各个厂家的指令都可能会扩展，AT指令最大长度具有不确定性，现**项目中涉及到的最长AT指令长度为166，经评审决定，长度分配256 */
#define AT_CMD_BUFF_LEN  256
```

**9-6（强制）：对字符串进行存储操作，确保字符串有’\\0’结束符。**

说明：对于字符串进行存储操作，必须确保字符串有‘\\0’结束符，否则在后续调用strlen等操作中，可能会导致内存访问越界漏洞；

下面是一个不好的例子：

```c
strncpy(path, src, sizeof(path) - 1);
len = strlen(path);
```

strncpy不会在目标缓冲区的结尾自动加上字串结束标志符'\\0，所以strlen计算path长度时可能会出错，建议修改如下：

```c
strncpy(path, src, sizeof(path) - 1);
path[sizeof(path) - 1] = '\0';
len = strlen(path);
```

**9-7（强制）：外部数据作为数组索引时必须确保在数组大小范围内。**

外部数据作为数组索引对内存进行访问时，必须对数据的大小进行严格的校验，否则可能会导致严重的错误。

下面是一个不好的例子， buffer[offset]的访问可能会越界：

```c
int foo(char *buffer)
{
    ...
    int offset = read_int_from_msg();
    char c = buffer[offset];
    ...
}
```

应做如下修改：

```c
int foo(char *buffer, int size)
{
    ...
    int offset = read_int_from_msg();
    if(offset >= 0 && offset < size)
    {
        char c = buffer[offset];
        ...
    }
    ...
}
```

**9-8（强制）：外部输入作为内存操作相关函数的复制长度时，需要校验其合法性。**

说明：在调用内存操作相关函数时，如果复制长度是外部输入，则必须校验其合法性，否则容易导致内存溢出。

示例：

```c
typedef struct
{
    uint32_t length;
    char val[MAX_INT_DIGITS];
}big_int_t;

big_int_t *char_to_bigint(char * input, uint32_t len)
{
    big_int_t big_bumber = {0};
    ...
    for(i = 0; i < len; i++)
    {
        big_number.val[i] = input[i];
    }
    ...
}
```

**9-9（强制）：调用格式化函数时，禁止format参数由外部可控。**

说明：调用格式化函数时，如果format参数由外部可控，会造成字符串格式化漏洞

错误示例：

```c
char * msg = get_msg();
...
printf(msg);
```

应改成如下：

```c
char *msg = get_msg();
...
printf("%s\n", msg);
```

**9-10（强制）：整数之间运算时必须严格检查，确保不会出现溢出、反转、除0。**

示例：如下程序将造成变量下溢。

```c
unsigned char size ;
while (size-- >=0) // 将出现下溢
{
   ... // program code
}
```

当size等于0时，再减1不会小于0，而是0xFF，故程序是一个死循环。应如下修改。

```c
char size; // 从unsigned char 改为char
while (size-- >=0)
{
   ... // program code
}
```

例外：当计算校验和等需要自然溢出的除外

**9-11（强制）：禁止对有符号数进行位操作符运算。**

说明：位操作符（\~、 \>\>、\<\< 、 &、 \^、\|）应该只用于无符号整形操作数。下面是一个错误的例子：

```c
int data_tmp = read_byte();
int data = data_tmp >> 24;
```

应做如下修改：

```c
unsigned int data_tmp = (unsigned int)read_byte();
unsigned int data = data_tmp >> 24;
```

下面是一个有符号数移位操作使用不当导致死循环的例子

```c
static void divide_by_two(int num)
{
    while (num) {
        printf("%d\n", num);
        num = num >> 1;
    }
}
```

有符号数的右移高位补0还是补1跟编译器有关，如果num传-1，在Linux上GCC的实现中，有符号数的右移操作的实现为使用符号位作为补充位，因此-1的右移操作仍然为0xFFFFFFFF，会导致死循环。

**9-12（强制）：禁止整数与指针间的互相转化。**

说明：指针的大小随着平台的不同而不同，强行进行整数与指针间的互相转化，降低了程序的

兼容性，在转换过程中可能引起指针高位信息的丢失

错误示例：

```c
char *ptr = ...;
unsigned int number = (unsigned int)ptr;
```

正确做法：

```c
char *ptr = ...;
uintptr_t number = (uintptr_t)ptr;
```

本条规范仅适用于应用层。

**9-13（强制）：禁止对指针进行逻辑或位运算。**

说明：对指针进行逻辑运算，会导致指针的性质改变，可能产生内存非法访问的问题，下面是错误的用法：

```c
bool data_process(char *str1, char *str2)
{
    ...
    if(str1)
    ...
    if(!str2)
    ...
}
```

正确做法：

```c
bool data_process(char *str1, char *str2)
{
    ...
    if(str1 !=NULL)
    ...
    if(str2 == NULL)
    ...
}
```

仅适用于应用层。

**9-14（强制）：循环次数如果受到外部数据控制，需要校验其合法性。**

说明：循环次数如果受外部控制，但是没有对其合法性进行校验，可能会进入死循环

示例：

```c
unsigned char *find_attr(unsigned char type, unsigned char *msg, size_t input_msg_len)
{
    ...
    msg_length = ntohs(*(unsigned short *)&msg[RD_LEA_PKT_LENGTH]);
    ...
    while (msg_length != 0)
    {
        attr_type = msg[0];
        attr_length = msg[RD_LEA_PKT_LENGTH];
        ...
        msg_length -= attr_length;
        msg += attr_length;
    }
    ...
}
```

**9-15（强制）：嵌入式软件通常不允许使用动态内存，除非非常有必要。**

说明：如果软件实现必须要使用动态内存，需要在部门内提出，评审通过后才可以使用。

**9-16（强制）：内存申请前，必须对申请内存的大小进行合法性校验。**

说明：内存申请的大小可能来自于外部数据，必须检查其合法性，不能申请长度为0的内存。

示例：

```c
int foo(int size)
{
    if(size <= 0)
    {
        //error
        ...
    }
    ...
    char *msg = (char *)malloc(size);
    ...
}
```

**9-17（强制）：内存分配后必须判断是否成功。**

示例：

```c
char *msg = (char*)malloc(size);
if(msg != NULL)
{
    ...
}
```

**9-18（强制）：禁止引用未初始化的内存。**

说明：malloc分配出来的内存没有被初始化为0，要确保内存被引用之前是被初始化的。

错误示例：

```c
int * foo(int size, int *param)
{
    int *result = NULL;
    ...
    result = malloc(size);
    ...
    result[0] = param[0];
    ...
    return result;
}
```

**9-19（强制）：字符串操作推荐使用带长度的安全函数。**

说明： 例如strcat是不安全的函数，strncat是较安全的函数，strcpy是不安全的函数，

strncpy是较安全的函数，sprintf是不安全的函数，snprintf是较安全的函数，strcmp是不安全的

函数，strncmp是较安全的函数。

注意：strncpy不会在目标缓冲区的结尾自动加上字串结束标志符'\\0',
需要在程序中手工在结束处

置'\\0'.

示例：

```c
strncpy(path, src, sizeof(path) - 1);
path[sizeof(path) - 1] = '\0';
len = strlen(path);
```

**9-20（建议）：当需要复制或拼接多个字符串到一个字符串时，推荐使用snprintf替代strcat和strcpy。**

示例：

```c
strcpy(full_path, file_path);
strcat(full_path, "/");
strcat(full_path, file_name);
```

如果使用snprintf只需要一行代码：

```c
snprintf(full_path, FULL_PATH_LEN, "%s/%s",  file_path,  file_name);
```

**9-21（强制）：linux系统中写完重要文件之后(比如参数文件)，要调用fflush和fsync，让系统把更改写入flash中，防止设备异常掉电，信息丢失。**

说明：通过open函数打开，write函数写入的，写完需要调用fsync，通过fopen函数打开，fwrite

写入的，写完需要调用fflush和fsync。

**9-22（强制）：资源泄露和内存破坏类别的coverity告警，无论类别高低必须分析。**

**9-23（强制）：linux系统中，当关闭文件描述符，特别是当文件描述符来自外部数据时，应仔细检查其正确性，防止错误或者重复关闭文件描述符。**

说明：当一个文件描述符fd被关闭之后，此文件描述符可能被再次分配，如果重复或者错误close

fd可能会带来严重问题，且不好定位。下面是一个由于错误使用inotify而导致错误关闭文件描

述符的例子。

国网集中器和国网二型集中器添加了安全防护功能。该功能会监控/opt目录内文件的增删，发

出告警。由于升级时一般会在/opt目录增删大量文件，此时为合法操作，因此升级过程会暂时

关闭安全防护功能。防护功能使用inotify监控目录方式实现

创建监控事件：

```c
void create_watch_opt_folder_event()
{
    inotify_fds.opt = inotify_init1(IN_NONBLOCK);
    if(inotify_fds.opt == TOPS_ERR)
    {
        plm_tlog_error(TLOG_UPGRADE_TAG, "Inotify_init failed, 
                      errno[%d]\n", errno);
        return;
    }

    inotify_wds.opt = inotify_add_watch(inotify_fds.opt, "/opt/sbin", 
                                        IN_CREATE|IN_DELETE|IN_ATTRIB|IN_MODIFY|IN_MOVED_FROM|IN_MOVED_TO);
    if(inotify_wds.opt == TOPS_ERR)
    {
        plm_tlog_error(TLOG_UPGRADE_TAG, "Inotify add watch failed, 
                       errno[%d]\n", errno);
        return;
    }
    te_create_file_event(inotify_fds.opt, TE_READABLE, watch_opt_handler, NULL);
}
```

删除监控事件

```c
void delete_watch_opt_folder_event()
{
    if(inotify_fds.opt >= 0)
    {
        te_delete_file_event(inotify_fds.opt);
        inotify_fds.opt = -1;
        close(inotify_wds.opt);
        inotify_wds.opt = -1;
    }
}
```

代码中创建监控事件时inotify_add_watch接口返回的是watch标识符，而不是文件描述符，不能用close关闭。假设返回的watch标识符的值为1，升级过程中会调用delete_watch_opt_folder_event删除监控事件，删除监控事件时调用close实际是将fd为1的文件描述符给关闭了，此操作可能会导致很严重的后果，比如当看门狗设备节点的fd为1时，看门狗节点被错误关闭，会导致无法继续喂狗，系统被重启。

删除监控代码应修改如下：

```c
void delete_watch_opt_folder_event()
{
    if(inotify_fds.opt >= 0)
    {
        inotify_rm_watch(inotify_fds.opt, inotify_wds.opt);
        te_delete_file_event(inotify_fds.opt);
        inotify_fds.opt = -1;
        inotify_wds.opt = -1;
    }
}
```

**9.24（强制）：禁用goto关键字。**

由于 goto 语句可以灵活跳转，如果不加限制，它会破坏结构化设计风格；其次，goto 语句经常带来错误或隐患。它可能跳过了变量的初始化、重要的计算等语句，例如：

```c
struct student *p = NULL;
…
goto state;
p = (struct student *)malloc(…); //被 goto 跳过,没有初始化
⋯
state:
//使用 p 指向的内存里的值的代码
⋯
```

如果编译器不能发觉此类错误，每用一次 goto 语句都可能留下隐患。

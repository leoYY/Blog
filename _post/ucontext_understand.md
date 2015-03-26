## ucontext 接口理解 ##
 - getcontext(struct ucontext_t*)
 初始化struct ucontext_t结构体，且默认记录当前上下文作为调用setcontext时恢复的入口点
 - setcontext(const struct ucontext_t*)
 根据传入 struct ucontext_t结构体，跳转到指定入口点，且该接口调用处的上下文不可恢复
 - makecontext(struct ucontext_t*, func, int, ...)
 设置指定函数以及参数列表作为struct ucontext_t上下文的入口点
 - swapcontext(struct ucontext_t* a, struct ucontext_t* b)
 记录当前上下文到a，并切换到上下文b，在执行后可通过反向swapcontext(b, a); 且还回节点

### example[^code]
```c
#include <stdlib.h>
#include <stdio.h>
#include <ucontext.h>

ucontext_t g_context;

int
main() {
 printf("get context this point\n");
 getcontext(&g_context);
 printf("exec \n");
 setcontext(&g_context);
 return EXIT_SUCCESS;
}
```
getcontext记录了当前执行上下文，并以该点为继续执行点
```c
#include <stdlib.h>
#include <stdio.h>
#include <ucontext.h>

#define STACK_SIZE (1024 * 1024)
ucontext_t g_context, user_context;
char stack[STACK_SIZE];

void foo {
 printf("in func\n");
 swapcontext(&user_context, &g_context);
}

int
main() {
 getcontext(&user_context);
 user_context.uc_stack.ss_sp = stack;
 user_context.uc_stack.ss_size = STACK_SIZE;
 user_context.uc_link = &g_context;
 makecontext(&user_context, (void(*)(void))foo, 0);
 swapcontext(&g_context, &user_context);
 printf("finish main\n");
 swapcontext(&g_context, &user_context);
 return EXIT_SUCCESS;
}
```
此处swapcontext,有对g_context进行初始化，相当于记录当前运行上下文并且以当前执行点为入口点初始化g_context
而往往对于函数foo中得swapcontext，类似lua或go语言中得yield关键字作用，但是由于swapcontext重新初始化了第一
个参数得context，因此在实现yield得时候需要记录当前context得栈上下文.
